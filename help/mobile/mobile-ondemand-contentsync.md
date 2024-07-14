---
title: Dispositivi mobili con sincronizzazione contenuti
description: Segui questa pagina per scoprire di più sulla sincronizzazione dei contenuti. Le pagine create in Adobe Experience Manager (AEM) possono essere utilizzate come contenuto dell’app, anche quando il dispositivo è offline. Inoltre, poiché le pagine AEM sono basate su standard web, funzionano su più piattaforme e consentono di incorporarle in qualsiasi wrapper nativo. Questa strategia riduce lo sforzo di sviluppo e consente di aggiornare facilmente i contenuti dell’app.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: a6e59334-09e2-4bb8-b445-1868035da556
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2971'
ht-degree: 0%

---

# Dispositivi mobili con sincronizzazione contenuti{#mobile-with-content-sync}

>[!NOTE]
>
>L’Adobe consiglia di utilizzare l’Editor SPA per i progetti che richiedono il rendering lato client basato su framework di applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

Utilizza Sincronizzazione contenuti per creare pacchetti di contenuti in modo che possano essere utilizzati nelle applicazioni native per dispositivi mobili. Le pagine create in Adobe Experience Manager (AEM) possono essere utilizzate come contenuto dell’app, anche quando il dispositivo è offline. Inoltre, poiché le pagine AEM sono basate su standard web, funzionano su più piattaforme e consentono di incorporarle in qualsiasi wrapper nativo. Questa strategia riduce lo sforzo di sviluppo e consente di aggiornare facilmente i contenuti dell’app.

Il framework di sincronizzazione dei contenuti crea un file di archivio contenente il contenuto web. Il contenuto può essere qualsiasi cosa, da semplici pagine, immagini e file PDF o intere applicazioni Web. L’API di sincronizzazione dei contenuti consente di accedere al file di archivio dalle app per dispositivi mobili o dai processi di generazione, in modo che il contenuto possa essere recuperato e incluso nell’app.

La sequenza di passaggi seguente illustra un caso d’uso tipico della sincronizzazione dei contenuti:

1. Lo sviluppatore AEM crea una configurazione di Sincronizzazione contenuti che specifica il contenuto da includere.
1. Il framework Content Sync raccoglie e memorizza in cache il contenuto.
1. Su un dispositivo mobile, l’app mobile viene avviata e richiede il contenuto dal server, che viene distribuito in un file ZIP.
1. Il client decomprime il contenuto ZIP nel file system locale. La struttura di cartelle nel file ZIP simula i percorsi che un client (ad esempio, un browser) richiederebbe normalmente dal server.
1. Il client apre il contenuto in un browser incorporato o lo utilizza in qualche altro modo.
1. Successivamente, il client richiede il contenuto aggiornato dal server. Il framework di sincronizzazione dei contenuti fornisce aggiornamenti incrementali per ridurre le dimensioni e i tempi di download, che possono essere importanti per i dispositivi mobili a causa della larghezza di banda limitata o dei volumi di dati.

## Sviluppo dei gestori di sincronizzazione dei contenuti {#developing-the-content-sync-handlers}

Di seguito sono riportate alcune linee guida per lo sviluppo di gestori di sincronizzazione dei contenuti:

* I gestori devono implementare *com.day.cq.contentsync.handler.ContentUpdateHandler* (direttamente o estendendo una classe che esegue)
* I gestori possono estendere *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* Il gestore deve segnalare true solo se aggiorna la cache di ContentSync. Se si segnala erroneamente true, l’AEM crea un aggiornamento quando in realtà non si è verificato un aggiornamento.
* Il gestore deve aggiornare la cache solo se il contenuto viene modificato. Non scrivere nella cache se non è necessario un bianco. Questo comporta la creazione di un aggiornamento non necessario.

>[!NOTE]
>
>Abilita la *registrazione debug ContentSync* tramite le configurazioni del logger OSGI nel pacchetto *com.day.cq.contentsync*. Questo consente di tenere traccia di quali gestori hanno eseguito e se hanno aggiornato la cache e segnalato l’aggiornamento della cache.

## Configurazione del contenuto di sincronizzazione contenuti {#configuring-the-content-sync-content}

Crea una configurazione di sincronizzazione contenuti per specificare il contenuto del file ZIP che viene distribuito al client. Puoi creare un numero qualsiasi di configurazioni di sincronizzazione dei contenuti. Ogni configurazione ha un nome a scopo di identificazione.

Per creare una configurazione di sincronizzazione dei contenuti, aggiungere un nodo `cq:ContentSyncConfig` all&#39;archivio con la proprietà `sling:resourceType` impostata su `contentsync/config`. Il nodo `cq:ContentSyncConfig` può trovarsi in qualsiasi punto del repository, tuttavia il nodo deve essere accessibile agli utenti nell&#39;istanza di pubblicazione AEM. Pertanto, aggiungere il nodo sotto `/content`.

Per specificare il contenuto del file ZIP di sincronizzazione contenuti, aggiungi nodi secondari al nodo cq:ContentSyncConfig. Le seguenti proprietà di ciascun nodo figlio identificano un elemento di contenuto da includere e come viene elaborato quando lo si aggiunge:

* `path`: posizione del contenuto.
* `type`: nome del tipo di configurazione da utilizzare per elaborare il contenuto. Sono disponibili diversi tipi descritti nella sezione *Tipi di configurazione*.

Per ulteriori informazioni, vedere *Esempio di configurazione di sincronizzazione dei contenuti*.

Dopo aver creato la configurazione di Sincronizzazione contenuti, questa viene visualizzata nella console Sincronizzazione contenuti.

>[!NOTE]
>
>Il framework di sincronizzazione dei contenuti non controlla che le dipendenze delle risorse e dei file relativi alla progettazione siano inclusi nei pacchetti di sincronizzazione dei contenuti. Assicurati di includere tutti i file richiesti nel file ZIP.

### Configurazione dell’accesso ai download di sincronizzazione dei contenuti {#configuring-access-to-content-sync-downloads}

Specifica un utente o un gruppo che può scaricare da Sincronizzazione contenuti. Puoi configurare l’utente o il gruppo predefinito che può essere scaricato da tutte le cache di Sincronizzazione contenuto, nonché ignorare l’impostazione predefinita e configurare l’accesso per una specifica configurazione di Sincronizzazione contenuto.

Quando AEM è installato, i membri del gruppo dell&#39;amministratore possono scaricare da Sincronizzazione contenuti per impostazione predefinita.

#### Impostazione dell’accesso predefinito per i download di sincronizzazione dei contenuti {#setting-the-default-access-for-content-sync-downloads}

Il servizio Day CQ Content Sync Manager controlla l’accesso a Content Sync. Configura questo servizio per specificare l&#39;utente o il gruppo che può scaricare da Sincronizzazione contenuti per impostazione predefinita.

Se si sta [configurando il servizio utilizzando la console Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console), digitare il nome dell&#39;utente o del gruppo come valore della proprietà Autorizzabile della cache di fallback.

Se si sta [configurando nel repository](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository), utilizzare le seguenti informazioni sul servizio:

* PID: com.day.cq.contentsync.impl.ContentSyncManagerImpl
* Nome proprietà: contentsync.fallback.authorizable

#### Ignorare l’accesso ai download per una cache di sincronizzazione dei contenuti {#overriding-download-access-for-a-content-sync-cache}

Per configurare l&#39;accesso al download per una configurazione specifica di Sincronizzazione contenuto, aggiungere la seguente proprietà al nodo `cq:ContentSyncConfig`:

* Nome: autorizzabile
* Tipo: String
* Valore: il nome dell’utente o del gruppo che può scaricare.

Ad esempio, la tua app consente agli utenti di installare gli aggiornamenti direttamente da Sincronizzazione contenuti. Per consentire a tutti gli utenti di scaricare l&#39;aggiornamento, impostare il valore della proprietà autorizzabile su `everyone`.

Se il nodo `cq:ContentSyncConfig` non dispone di una proprietà autorizzabile, l&#39;utente o il gruppo predefinito configurato per la proprietà Autorizzabile cache di fallback del servizio Day CQ Content Sync Manager determina chi può scaricare.

### Configurazione dell’utente per l’aggiornamento di una cache di sincronizzazione contenuti {#configuring-the-user-for-updating-a-content-sync-cache}

Quando un utente esegue un aggiornamento alla cache di sincronizzazione contenuti, l’azione viene eseguita da un account utente specifico per conto dell’utente. Per impostazione predefinita, l’utente anonimo aggiorna tutte le cache di Sincronizzazione contenuto.

Puoi sovrascrivere l’utente predefinito e specificare un utente o un gruppo che aggiorna una cache di sincronizzazione contenuti specifica.

Per ignorare l&#39;utente predefinito, specificare un utente o un gruppo che esegua aggiornamenti per una configurazione di Sincronizzazione contenuto specifica aggiungendo la seguente proprietà al nodo cq:ContentSyncConfig:

* Nome: `updateuser`
* Tipo: `String`
* Valore: nome dell&#39;utente o del gruppo che può eseguire gli aggiornamenti.

Se il nodo `cq:ContentSyncConfig` non ha una proprietà `updateuser`, l&#39;utente predefinito `anonymous` aggiorna la cache.

### Tipi di configurazione {#configuration-types}

L’elaborazione può variare dal rendering di un JSON semplice al rendering completo delle pagine, incluse le relative risorse di riferimento. In questa sezione sono elencati i tipi di configurazione disponibili e i relativi parametri specifici:

**copia** - Copia file e cartelle.

* **percorso** - Se il percorso punta a un singolo file, viene copiato solo il file. Se punta a una cartella (inclusi i nodi della pagina), verranno copiati tutti i file e le cartelle sottostanti.

**content** Esegui il rendering del contenuto utilizzando [Elaborazione richiesta Sling](/help/sites-developing/the-basics.md#sling-request-processing) standard.

* **percorso** - Percorso della risorsa da restituire.
* **estensione** - Estensione da utilizzare nella richiesta. Esempi comuni sono *html* e *json*, ma qualsiasi altra estensione è possibile.

* **selettore** - Selettori opzionali separati da un punto. Esempi comuni sono *touch* per il rendering delle versioni mobili di una pagina o *infinity* per l&#39;output JSON.

**clientlib** - Crea un pacchetto con una libreria client JavaScript o CSS.

* **percorso** - Percorso della directory principale della libreria client.
* **estensione** - Tipo di libreria client. Al momento deve essere impostato su *js* o *css*.

**risorse**

Raccogli le rappresentazioni originali delle risorse.

* **percorso** - Percorso di una cartella di risorse in /content/dam.

**immagine** - Raccogli un&#39;immagine.

* **percorso** - Percorso di una risorsa immagine.

Il tipo di immagine viene utilizzato per includere il logo We Retail nel file zip.

**pagine** - Eseguire il rendering delle pagine AEM e raccogliere le risorse di riferimento.

* **percorso** - Percorso di una pagina.
* **estensione** - Estensione da utilizzare nella richiesta. Per le pagine si tratta quasi sempre di *html*, ma altri sono ancora possibili.

* **selettore** - Selettori opzionali separati da un punto. Esempi comuni sono *touch* per il rendering delle versioni mobili di una pagina.

* **deep** - Proprietà booleana opzionale che determina se includere anche le pagine figlie. Il valore predefinito è *true.*

* **includeImages** - Proprietà booleana opzionale che determina se le immagini devono essere incluse. Il valore predefinito è *true*.

  Per impostazione predefinita, solo i componenti immagine con un tipo di risorsa fondazione/componenti/immagine vengono considerati per l’inclusione. È possibile aggiungere altri tipi di risorse configurando il gestore di aggiornamento **Day CQ WCM Pages** nella console Web.

**riscrittura** - Il nodo di riscrittura definisce la modalità di riscrittura dei collegamenti nella pagina esportata. I collegamenti riscritti possono puntare ai file inclusi nel file zip o alle risorse sul server.

Il nodo `rewrite` deve trovarsi sotto il nodo `page`.

Il nodo `rewrite` può avere una o più delle seguenti proprietà:

* `clientlibs`: riscrive i percorsi clientlibs.

* `images`: riscrive i percorsi delle immagini.
* `links`: riscrive i percorsi dei collegamenti.

Ogni proprietà può avere uno dei seguenti valori:

* `REWRITE_RELATIVE`: riscrive il percorso con una posizione relativa al file html della pagina nel file system.

* `REWRITE_EXTERNAL`: riscrive il percorso puntando alla risorsa sul server, utilizzando il servizio [Externalizer](/help/sites-developing/externalizer.md) dell&#39;AEM.

Il servizio AEM denominato **PathRewriterTransformerFactory** consente di configurare gli attributi html specifici che verranno riscritti. Il servizio può essere configurato nella console Web e dispone di una configurazione per ogni proprietà del nodo `rewrite`: `clientlibs`, `images` e `links`.

Questa funzione è stata aggiunta all’AEM 5.5.

### Esempio di configurazione della sincronizzazione dei contenuti {#example-content-sync-configuration}

L’elenco seguente mostra un esempio di configurazione per Sincronizzazione contenuti.

```xml
+ weretail_go [cq:ContentSyncConfig]
  - sling:resourceType = "contentsync/config"

  + etc.designs.default [nt:unstructured]
    - path = "/etc/designs/default"
    - type = "copy"

  + etc.designs.mobile [nt:unstructured]
    - path = "/etc/designs/mobile"
    - type = "copy"

  + events.plist [nt:unstructured]
    - path = "/content/weretail_mobile/en/events/jcr:content/par/events"
    - type = "content"
    - extension = "plist"

  + events.touch.html [nt:unstructured]
    - path = "/content/weretail_mobile/en/events"
    - type = "pages"
    - extension = "html"
    - selector = "touch"

  + logo [nt:unstructured]
    - path = "/etc/designs/mobile/jcr:content/mobilecontentpage/logo"
    - type = "logo"

  + manifest [nt:unstructured]
    - indexPage = "/content/weretail_mobile/en/events.touch.html"
    - metadataPlist = "/content/weretail_mobile/en/events/_jcr_content/par/events.plist"

  + ...
```

**etc.designs.default e etc.designs.mobile** - Le prime due voci della configurazione sono ovvie. Poiché stai per includere diverse pagine mobili, devi disporre dei relativi file di progettazione sotto /etc/designs. E poiché non è richiesta alcuna elaborazione aggiuntiva, la copia è sufficiente.

**events.plist** - Questa voce è un po&#39; speciale. Come accennato nell’introduzione, l’applicazione deve fornire una vista a mappa con i marcatori della posizione degli eventi. Le informazioni necessarie sulla posizione verranno fornite come file separato in formato PLIST. Affinché ciò funzioni, il componente elenco eventi utilizzato nella pagina indice dispone di uno script denominato plist.jsp. Questo script viene eseguito quando la risorsa del componente viene richiesta con l&#39;estensione `.plist`. Come sempre, il percorso dei componenti è specificato nella proprietà percorso e il tipo è impostato sul contenuto, perché si desidera utilizzare [Elaborazione richiesta Sling](/help/sites-developing/the-basics.md#sling-request-processing).

**events.touch.html** - Successivamente vengono visualizzate le pagine effettive visualizzate nell&#39;app. La proprietà path viene impostata sulla pagina principale degli eventi. Verranno incluse anche tutte le pagine evento al di sotto di quella pagina, perché la proprietà deep (deep) è impostata per impostazione predefinita su true. Utilizza le pagine come tipo di configurazione, in modo da includere tutte le immagini o altri file a cui si può fare riferimento da un componente immagine o download in una pagina. Inoltre, l’impostazione del selettore touch fornisce una versione mobile delle pagine. La configurazione nel feature pack contiene più voci di questo tipo, ma qui sono escluse per semplicità.

**logo** - Il tipo di configurazione del logo non è stato menzionato finora e non è nessuno dei tipi incorporati. Tuttavia, il framework di sincronizzazione dei contenuti è in certa misura estensibile, come illustrato nella sezione successiva.

**manifest** - È spesso consigliabile includere nel file zip alcuni tipi di metadati, ad esempio la pagina iniziale del contenuto. Tuttavia, la codifica fissa di tali informazioni impedisce di modificarle in un secondo momento. Il framework di sincronizzazione dei contenuti supporta questo caso d’uso cercando un nodo manifesto nella configurazione, identificato per nome e che non richiede un tipo di configurazione. Ogni proprietà definita in quel particolare nodo viene aggiunta a un file, che è anche chiamato manifesto e risiede nella radice del file zip.

Nell’esempio, la pagina di elenco degli eventi deve essere la pagina iniziale. Queste informazioni sono fornite nella proprietà **indexPage** e possono quindi essere facilmente modificate in qualsiasi momento. Una seconda proprietà definisce il percorso del file *events.plist*. Come vedrai in seguito, l’applicazione client ora può leggere il manifesto e agire in base a esso.

Una volta configurata la configurazione, il contenuto può essere scaricato con un browser o con qualsiasi altro client HTTP oppure, se stai sviluppando per iOS, puoi utilizzare la libreria client WAppKitSync dedicata. Il percorso di download è costituito dal percorso della configurazione e dall&#39;estensione *.zip*, ad esempio, quando si lavora con un&#39;istanza AEM locale: *http://localhost:4502/content/weretail_go.zip*

### Console di sincronizzazione contenuti {#the-content-sync-console}

La console Sincronizzazione contenuti elenca tutte le configurazioni di Sincronizzazione contenuti nell&#39;archivio (tutti i nodi di tipo `cq:ContentSyncConfig`) e per ogni configurazione consente di effettuare le seguenti operazioni:

* Aggiorna la cache.
* Cancella la cache.
* Scarica un file ZIP completo.
* Scarica un file ZIP diverso da adesso a una data e un’ora specifiche.

Può essere utile per lo sviluppo e la risoluzione dei problemi.

La console è accessibile al seguente indirizzo:

`http://localhost:4502/libs/cq/contentsync/content/console.html`

Si presenta come segue:

![chlimage_1-50](assets/chlimage_1-50.png)

### Estensione del framework Content Sync {#extending-the-content-sync-framework}

Anche se il numero di opzioni di configurazione è già ampio, potrebbe non coprire tutti i requisiti del caso d’uso specifico. Questa sezione descrive i punti di estensione del framework di sincronizzazione dei contenuti e come creare tipi di configurazione personalizzati.

Per ogni tipo di configurazione esiste un *Gestore aggiornamento contenuto*, ovvero una factory del componente OSGi registrata per il tipo specifico. Questi gestori raccolgono il contenuto, lo elaborano e lo aggiungono a una cache gestita dal framework Content Sync. Implementa la seguente classe di interfaccia o di base astratta:

* `com.day.cq.contentsync.handler.ContentUpdateHandler` - Interfaccia che tutti i gestori di aggiornamenti devono implementare
* `com.day.cq.contentsync.handler.AbstractSlingResourceUpdateHandler` - Classe astratta che semplifica il rendering delle risorse tramite Sling

Registra la classe come fabbrica di componenti OSGi e implementala nel contenitore OSGi in un bundle. Questa operazione può essere eseguita utilizzando il plug-in [Maven SCR](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/apache-felix-maven-scr-plugin-use.html) utilizzando tag JavaDoc o annotazioni. L’esempio seguente mostra la versione di JavaDoc:

```java
/*
 * @scr.component metatype="no"
 * factory="com.day.cq.contentsync.handler.ContentUpdateHandler/customtype"
 */
public class CustomTypeUpdateHandler implements ContentUpdateHandler {
    // add your code here
}

/*
 * @scr.component metatype="no" inherit="true"
 * factory="com.day.cq.contentsync.handler.ContentUpdateHandler/othertype"
 */
public class OtherTypeUpdateHandler extends AbstractSlingResourceUpdateHandler {
    // add your code here
}
```

La definizione di *factory* contiene l&#39;interfaccia comune e il tipo personalizzato separati da una barra. Questa strategia consente al framework Content Sync di trovare e creare un&#39;istanza della classe personalizzata che riconosce il tipo personalizzato in una voce di configurazione. Nella sezione successiva viene fornito un esempio concreto di un gestore di aggiornamento personalizzato.

>[!CAUTION]
>
>Quando si utilizza la classe di base AbstractSlingResourceUpdateHandler, è necessario aggiungere la definizione *inherit*. In caso contrario, il contenitore OSGi non imposterà i riferimenti richiesti dichiarati nella classe base.

### Implementazione di un gestore di aggiornamento personalizzato {#implementing-a-custom-update-handler}

Ogni pagina di We.Retail Mobile contiene un logo nell&#39;angolo superiore sinistro che deve essere incluso nel file zip. Tuttavia, per l&#39;ottimizzazione della cache, AEM non fa riferimento alla posizione reale del file di immagine nell&#39;archivio, il che impedisce di utilizzare semplicemente il tipo di configurazione **copy**. In alternativa, devi fornire il tipo di configurazione **logo** che rende l&#39;immagine disponibile nel percorso richiesto dall&#39;AEM. Il seguente elenco di codici mostra la completa implementazione del gestore di aggiornamento del logo:

#### LogoUpdateHandler.java {#logoupdatehandler-java}

```java
package com.day.cq.wcm.apps.weretail.impl;

import javax.jcr.Node;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.day.cq.commons.jcr.JcrUtil;
import com.day.cq.contentsync.config.ConfigEntry;
import com.day.cq.contentsync.handler.ContentUpdateHandler;
import com.day.cq.wcm.foundation.Image;
import com.day.text.Text;

/**
 * The <code>LogoUpdateHandler</code> is used to update the content sync cache
 * with a page logo added using a logo component.
 *
 * @scr.component metatype="no"
 * factory="com.day.cq.contentsync.handler.ContentUpdateHandler/logo"
 */
public class LogoUpdateHandler implements ContentUpdateHandler {

    private static final Logger log = LoggerFactory.getLogger(LogoUpdateHandler.class);

    /** @scr.reference policy="static" */
    protected JcrResourceResolverFactory resolverFactory;

    public boolean updateCacheEntry(ConfigEntry configEntry, Long lastUpdated, String configCacheRoot, Session admin, Session session) {
        ResourceResolver resolver = resolverFactory.getResourceResolver(admin);
        Resource resource = resolver.getResource(configEntry.getContentPath());

        Image img = new Image(resource);
        img.setItemName(Image.NN_FILE, "image");
        img.setItemName(Image.PN_REFERENCE, "imageReference");
        img.setSelector("img");

        try {
            if(img.getLastModified() == null || lastUpdated < img.getLastModified().getTime().getTime()) {
                String src = img.getSrc();
                String parentPath = configCacheRoot + Text.getRelativeParent(src, 1);

                Node parent = JcrUtil.createPath(parentPath, "sling:Folder", admin);
                Node image = resolver.getResource(resource.getPath() + "/image").adaptTo(Node.class);
                JcrUtil.copy(image, parent, Text.getName(src));

                admin.save();

                return true;
            }
        } catch (RepositoryException e) {
            log.error("Unexpected error while updating logo: ", e);
        }

        return false;
    }
}
```

La classe `LogoUpdateHandler` implementa il metodo `updateCacheEntry(ConfigEntry, Long, String, Session, Session)` dell&#39;interfaccia `ContentUpdateHandler`, che accetta diversi argomenti:

* Istanza `ConfigEntry` che consente di accedere alla voce di configurazione per la quale viene chiamato il gestore e alle relative proprietà.
* Timestamp `lastUpdated` che indica l&#39;ultimo aggiornamento della cache da parte di Content Sync. Il contenuto che non è stato modificato dopo tale marca temporale non deve essere aggiornato dal gestore.
* Argomento `configCacheRoot` che specifica il percorso radice della cache. Tutti i file aggiornati devono essere memorizzati in questo percorso per essere aggiunti al file zip.
* Sessione amministrativa da utilizzare per tutte le operazioni dell&#39;archivio relative alla cache.
* Sessione utente che può essere utilizzata per aggiornare il contenuto nel contesto di un determinato utente e quindi per fornire un tipo di contenuto personalizzato.

Per implementare il gestore personalizzato, crea innanzitutto un’istanza della classe Image in base alla risorsa specificata nella voce di configurazione. Questa è la stessa procedura utilizzata dal componente logo nelle nostre pagine. Verifica che il percorso di destinazione dell’immagine sia lo stesso di quello a cui si fa riferimento da una pagina.

Quindi, controlla se la risorsa è stata modificata dall’ultimo aggiornamento. Le implementazioni personalizzate devono evitare aggiornamenti non necessari della cache e restituire false in caso di modifiche. Se la risorsa è stata modificata, copia l’immagine nella posizione di destinazione prevista relativa alla directory principale della cache. Infine, viene restituito `true` per indicare al framework che la cache è stata aggiornata.

## Utilizzo del contenuto sul client {#using-the-content-on-the-client}

Per utilizzare il contenuto in un’app mobile fornita da Sincronizzazione contenuti, devi richiedere il contenuto tramite una connessione HTTP o HTTPS. Di conseguenza, il contenuto recuperato (compresso in un file ZIP) può essere estratto e memorizzato localmente sul dispositivo mobile. Il contenuto non si riferisce solo ai dati ma anche alla logica, ovvero alle applicazioni web complete; pertanto, l’utente mobile può eseguire le applicazioni web recuperate e i dati corrispondenti anche senza connettività di rete.

La sincronizzazione dei contenuti offre i contenuti in modo intelligente: vengono trasmesse solo le modifiche apportate ai dati dall’ultima sincronizzazione dei dati eseguita correttamente, riducendo così il tempo necessario per il trasferimento. Alla prima esecuzione di un&#39;applicazione, vengono richieste modifiche ai dati a partire dal 1 gennaio 1970, mentre successivamente vengono richiesti solo i dati che sono stati modificati dopo l&#39;ultima sincronizzazione riuscita. AEM utilizza un framework di comunicazione client per iOS per semplificare la comunicazione e il trasferimento dei dati in modo da richiedere una quantità minima di codice nativo per abilitare un’applicazione web basata su iOS.

Tutti i dati trasferiti possono essere estratti nella stessa struttura di directory; non sono necessari passaggi aggiuntivi (ad esempio, controlli di dipendenza) durante l’estrazione dei dati. Se è presente iOS, tutti i dati vengono memorizzati in una sottocartella all’interno della cartella Documenti dell’app iOS.

Percorso di esecuzione tipico di un’app AEM Mobile basata su iOS:

* L’utente avvia l’app sul dispositivo iOS.
* L’app tenta di connettersi al backend AEM e richiede modifiche ai dati dall’ultima esecuzione.
* Il server recupera i dati in questione e li comprime in un file.
* I dati vengono restituiti al dispositivo client da cui vengono estratti nella cartella documenti.
* Il componente UIWebView viene avviato/aggiornato.

Se non è stato possibile stabilire una connessione in precedenza, vengono visualizzati i dati scaricati.

### Risorse aggiuntive {#additional-resources}

Per informazioni sui ruoli e sulle responsabilità di un amministratore e di un autore, consulta le risorse seguenti:

* [Authoring di contenuti AEM per AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md)
* [Amministrazione di contenuti per l’utilizzo di AEM Mobile On-demand Services](/help/mobile/aem-mobile.md)
