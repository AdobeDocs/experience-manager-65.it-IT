---
title: Mobile con sincronizzazione dei contenuti
seo-title: Mobile con sincronizzazione dei contenuti
description: Seguite questa pagina per informazioni sulla sincronizzazione dei contenuti. Le pagine create in AEM possono essere utilizzate come contenuto dell'app, anche quando il dispositivo è offline. Inoltre, poiché AEM pagine sono basate su standard Web, funzionano su più piattaforme e consentono di incorporarle in qualsiasi wrapper nativo. Questa strategia riduce il lavoro di sviluppo e consente di aggiornare facilmente il contenuto delle app.
seo-description: Seguite questa pagina per informazioni sulla sincronizzazione dei contenuti. Le pagine create in AEM possono essere utilizzate come contenuto dell'app, anche quando il dispositivo è offline. Inoltre, poiché AEM pagine sono basate su standard Web, funzionano su più piattaforme e consentono di incorporarle in qualsiasi wrapper nativo. Questa strategia riduce il lavoro di sviluppo e consente di aggiornare facilmente il contenuto delle app.
uuid: 11f74cc5-99a5-4186-9b60-b19351305432
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 8fb70ca4-86fc-477d-9773-35b84d5e85a8
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '3057'
ht-degree: 0%

---


# Mobile con Content Sync{#mobile-with-content-sync}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Utilizzate Content Sync (Sincronizzazione contenuti) per creare pacchetti di contenuto in modo che possa essere utilizzato nelle applicazioni mobili native. Le pagine create in AEM possono essere utilizzate come contenuto dell&#39;app, anche quando il dispositivo è offline. Inoltre, poiché AEM pagine sono basate su standard Web, funzionano su più piattaforme e consentono di incorporarle in qualsiasi wrapper nativo. Questa strategia riduce il lavoro di sviluppo e consente di aggiornare facilmente il contenuto dell&#39;app.

Il framework Content Sync crea un file di archivio che contiene il contenuto Web. Il contenuto può essere costituito da pagine semplici, immagini e file PDF o da intere applicazioni Web. L&#39;API Content Sync consente di accedere al file di archivio dalle app mobili o dai processi di creazione in modo che il contenuto possa essere recuperato e incluso nell&#39;app.

La seguente sequenza di passaggi illustra un caso d’uso tipico per la sincronizzazione dei contenuti:

1. Lo sviluppatore AEM crea una configurazione Content Sync che specifica il contenuto da includere.
1. Il framework Content Sync raccoglie e memorizza nella cache il contenuto.
1. Su un dispositivo mobile, l’applicazione mobile viene avviata e richiede il contenuto dal server, che viene distribuito in un file ZIP.
1. Il client scomprime il contenuto ZIP nel file system locale. La struttura delle cartelle nel file ZIP simula i percorsi che un client (ad es. un browser) richiederebbe normalmente dal server.
1. Il client apre il contenuto in un browser incorporato o lo utilizza in altro modo.
1. Successivamente, il client richiede il contenuto aggiornato dal server. Il framework Content Sync offre aggiornamenti incrementali per ridurre le dimensioni e il tempo di download, che possono essere importanti per i dispositivi mobili a causa di larghezza di banda o volumi di dati limitati.

## Sviluppo dei gestori di sincronizzazione dei contenuti {#developing-the-content-sync-handlers}

Alcune delle linee guida per lo sviluppo di gestori di sincronizzazione dei contenuti sono le seguenti:

* I gestori devono implementare *com.day.cq.contentsync.handler.ContentUpdateHandler* (direttamente o estendendo una classe che lo supporta)
* I gestori possono estendere *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* Il gestore deve segnalare true solo se aggiorna la cache ContentSync. Se si segnala erroneamente true, AEM creare un aggiornamento quando non si verifica effettivamente un aggiornamento.
* Il gestore deve aggiornare la cache solo se il contenuto è effettivamente cambiato. Non scrivere nella cache se non è necessario un bianco. Questo determina la creazione di un aggiornamento non necessario.

>[!NOTE]
>
>Abilitare *Registrazione debug ContentSync* tramite le configurazioni del logger OSGI sul pacchetto *com.day.cq.contentsync*. Questo consente di tenere traccia dei gestori eseguiti e se hanno aggiornato la cache e segnalato l&#39;aggiornamento della cache.

## Configurazione del contenuto di sincronizzazione dei contenuti {#configuring-the-content-sync-content}

Create una configurazione di sincronizzazione dei contenuti per specificare il contenuto del file ZIP consegnato al client. Potete creare un numero qualsiasi di configurazioni di sincronizzazione dei contenuti. Ogni configurazione ha un nome a scopo di identificazione.

Per creare una configurazione di sincronizzazione dei contenuti, aggiungete un nodo `cq:ContentSyncConfig` alla directory archivio, con la proprietà `sling:resourceType` impostata su `contentsync/config`. Il nodo `cq:ContentSyncConfig` può trovarsi ovunque nell&#39;archivio, ma il nodo deve essere accessibile agli utenti nell&#39;istanza di pubblicazione AEM. Pertanto, è necessario aggiungere il nodo sotto `/content`.

Per specificare il contenuto del file ZIP Content Sync, aggiungete nodi secondari al nodo cq:ContentSyncConfig. Le seguenti proprietà di ciascun nodo figlio identificano un elemento di contenuto da includere e come viene elaborato al momento dell&#39;aggiunta:

* `path`: Posizione del contenuto.
* `type`: Nome del tipo di configurazione da utilizzare per l&#39;elaborazione del contenuto. Diversi tipi sono disponibili e sono descritti nella sezione *Tipi di configurazione*.

Per ulteriori informazioni, vedere *Esempio di configurazione della sincronizzazione dei contenuti*.

Dopo aver creato la configurazione Content Sync (Sincronizzazione contenuto), questa viene visualizzata nella console Content Sync (Sincronizzazione contenuto).

>[!NOTE]
>
>Il framework Content Sync non verifica che le dipendenze delle risorse e dei file relativi alla progettazione siano inclusi nei pacchetti Content Sync. Accertatevi di includere tutti i file richiesti nel file ZIP.

### Configurazione dell&#39;accesso ai download della sincronizzazione dei contenuti {#configuring-access-to-content-sync-downloads}

Specificate un utente o un gruppo che possa scaricare da Content Sync (Sincronizzazione contenuto). Potete configurare l’utente o il gruppo predefinito che può essere scaricato da tutte le cache di sincronizzazione dei contenuti, nonché ignorare i valori predefiniti e configurare l’accesso per una specifica configurazione di sincronizzazione dei contenuti.

Quando AEM è installato, per impostazione predefinita i membri del gruppo di amministratori possono scaricare da Content Sync (Sincronizzazione contenuto).

#### Impostazione dell&#39;accesso predefinito per i download di sincronizzazione dei contenuti {#setting-the-default-access-for-content-sync-downloads}

Il servizio Day CQ Content Sync Manager controlla l&#39;accesso a Content Sync. Configurate questo servizio per specificare l&#39;utente o il gruppo che può scaricare da Content Sync per impostazione predefinita.

Se si sta [configurando il servizio tramite la console Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console), digitare il nome dell&#39;utente o del gruppo come valore della proprietà Autorizzabile cache di fallback.

Se si sta [configurando nell&#39;archivio](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository), utilizzare le seguenti informazioni sul servizio:

* PID: com.day.cq.contentsync.impl.ContentSyncManagerImpl
* Nome proprietà: contentsync.fallback.authorizable

#### Sostituzione dell&#39;accesso per il download per una cache di sincronizzazione dei contenuti {#overriding-download-access-for-a-content-sync-cache}

Per configurare l&#39;accesso al download per una configurazione specifica di Content Sync, aggiungete la seguente proprietà al nodo `cq:ContentSyncConfig`:

* Nome: autorizzabile
* Tipo: Stringa
* Valore: Nome dell’utente o del gruppo che può essere scaricato.

Ad esempio, l&#39;app consente agli utenti di installare gli aggiornamenti direttamente da Content Sync. Per consentire a tutti gli utenti di scaricare l&#39;aggiornamento, impostate il valore della proprietà autorizzabile su `everyone`.

Se il nodo `cq:ContentSyncConfig` non dispone di proprietà autorizzabile, l&#39;utente o il gruppo predefinito configurato per la proprietà Autorizzabile cache di fallback del servizio Gestione sincronizzazione contenuti di Day CQ determina chi può scaricare.

### Configurazione dell&#39;utente per l&#39;aggiornamento di una cache di sincronizzazione dei contenuti {#configuring-the-user-for-updating-a-content-sync-cache}

Quando un utente esegue un aggiornamento alla cache di sincronizzazione dei contenuti, un account utente specifico esegue l&#39;azione per conto dell&#39;utente. L&#39;utente anonimo aggiorna tutte le cache di sincronizzazione dei contenuti per impostazione predefinita.

Potete ignorare l’utente predefinito e specificare un utente o un gruppo che aggiorna una cache di sincronizzazione dei contenuti specifica.

Per ignorare l’utente predefinito, specificate un utente o un gruppo che esegue gli aggiornamenti per una specifica configurazione Content Sync aggiungendo la seguente proprietà al nodo cq:ContentSyncConfig:

* Nome: `updateuser`
* Tipo: `String`
* Valore: Nome dell’utente o del gruppo che può eseguire gli aggiornamenti.

Se il nodo `cq:ContentSyncConfig` non ha proprietà `updateuser`, l&#39;utente predefinito `anonymous` aggiorna la cache.

### Tipi di configurazione {#configuration-types}

L&#39;elaborazione può variare dal rendering di JSON semplice al rendering completo delle pagine, incluse le risorse di riferimento. In questa sezione sono elencati i tipi di configurazione disponibili e i relativi parametri specifici:

**** copiareÈ sufficiente copiare file e cartelle.

* **path**  - Se il percorso punta a un singolo file, viene copiato solo il file. Se punta a una cartella (che include i nodi di pagina), verranno copiati tutti i file e le cartelle sottostanti.

**contenuto** contentRender utilizzando l&#39;elaborazione [ standard della richiesta ](/help/sites-developing/the-basics.md#sling-request-processing)Sling.

* **percorso**  - Percorso della risorsa da restituire.
* **extension** - Estensione da utilizzare nella richiesta. Esempi comuni sono *html* e *json*, ma è possibile eseguire qualsiasi altra estensione.

* **selettore** - Selettori opzionali separati da punto. Esempi comuni sono *touch* per il rendering delle versioni mobili di una pagina o *infinity* per l&#39;output JSON.

**clientlibCreate un pacchetto per la libreria client Javascript o CSS.** 

* **percorso**  - Percorso della directory principale della libreria client.
* **extension** - Tipo di libreria client. Deve essere impostato al momento su *js* o *css*.

**assets**

Raccogliere le rappresentazioni originali delle risorse.

* **percorso**  - Percorso di una cartella di risorse sotto /content/dam.

**** imageRaccogliere un’immagine.

* **percorso**  - Percorso di una risorsa immagine.

Il tipo di immagine viene utilizzato per includere il logo We Retail nel file zip.

**** pagineRendering AEM pagine e raccolta delle risorse di riferimento.

* **percorso**  - Percorso di una pagina.
* **extension** - Estensione da utilizzare nella richiesta. Per le pagine questo è quasi sempre *html*, ma altri sono ancora possibili.

* **selettore** - Selettori opzionali separati da punto. Esempi comuni sono *touch* per il rendering delle versioni mobili di una pagina.

* **deep**  - Proprietà booleana opzionale che determina se includere anche le pagine figlie. Il valore predefinito è *true.*

* **includeImages**  - Proprietà booleana opzionale che determina se le immagini devono essere incluse. Il valore predefinito è *true*.

   Per impostazione predefinita, sono considerati per l’inclusione solo i componenti immagine con un tipo di risorsa di base/componenti/immagine. È possibile aggiungere altri tipi di risorse configurando il **Day CQ WCM Pages Update Handler** nella console Web.

**** rewriteIl nodo di riscrittura definisce il modo in cui i collegamenti vengono riscritti nella pagina esportata. I collegamenti riscritti possono puntare ai file inclusi nel file zip o alle risorse sul server.

Il nodo `rewrite` deve trovarsi sotto il nodo `page`.

Il nodo `rewrite` può avere una o più delle seguenti proprietà:

* `clientlibs`: riscrive i percorsi clientlibs.

* `images`: riscrive i percorsi delle immagini.
* `links`: riscrive i percorsi dei collegamenti.

Ogni proprietà può avere uno dei seguenti valori:

* `REWRITE_RELATIVE`: riscrive il percorso con una posizione relativa al file .html della pagina nel file system.

* `REWRITE_EXTERNAL`: riscrive il percorso puntando la risorsa sul server, utilizzando il servizio [ AEM ](/help/sites-developing/externalizer.md)Externalizer.

Il servizio AEM denominato **PathRewriterTransformerFactory** consente di configurare gli attributi HTML specifici che verranno riscritti. Il servizio può essere configurato nella console Web e dispone di una configurazione per ciascuna proprietà del nodo `rewrite`: `clientlibs`, `images` e `links`.

Questa funzione è stata aggiunta nella AEM 5.5.

### Esempio di configurazione della sincronizzazione dei contenuti {#example-content-sync-configuration}

L&#39;elenco seguente mostra una configurazione di esempio per Content Sync.

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

**etc.designs.default e etc.designs.** mobileLe prime due voci della configurazione dovrebbero essere abbastanza ovvie. Poiché includeremo un certo numero di pagine mobili, abbiamo bisogno dei relativi file di progettazione qui sotto /etc/designs. E poiché non è richiesta ulteriore elaborazione, la copia è sufficiente.

**events.** plistQuesta voce è un po&#39; speciale. Come indicato nell&#39;introduzione, l&#39;applicazione deve fornire una visualizzazione mappa con i marcatori delle posizioni degli eventi. Forniremo le informazioni di posizione necessarie come file separato in formato PLIST. A tal fine, il componente dell&#39;elenco eventi utilizzato nella pagina di indice ha uno script denominato plist.jsp. Questo script viene eseguito quando la risorsa del componente viene richiesta con l&#39;estensione .plist. Come al solito, il percorso dei componenti è indicato nella proprietà path e il tipo è impostato su content, perché vogliamo sfruttare l&#39;elaborazione della [richiesta Sling](/help/sites-developing/the-basics.md#sling-request-processing).

**events.touch.** htmlVerranno visualizzate le pagine effettive nell&#39;app. La proprietà path è impostata sulla pagina principale dell&#39;evento. Vengono incluse anche tutte le pagine dell&#39;evento al di sotto di tale pagina, poiché per impostazione predefinita la proprietà deep è impostata su true. Utilizziamo le pagine come tipo di configurazione, in modo che vengano incluse tutte le immagini o altri file a cui può fare riferimento un’immagine o un componente per il download in una pagina. Inoltre, l’impostazione del selettore touch offre una versione mobile delle pagine. La configurazione nel pacchetto di caratteristiche contiene più voci di questo tipo, ma qui sono lasciate fuori per semplicità.

**** logoIl tipo di configurazione del logo non è stato menzionato finora e non è uno dei tipi predefiniti. Tuttavia, il framework Content Sync (Sincronizzazione contenuti) è estensibile in qualche misura e questo è un esempio di ciò, che sarà trattato nella sezione successiva.

**** manifestÈ spesso consigliabile includere nel file ZIP qualche tipo di metadati, ad esempio la pagina iniziale del contenuto. Tuttavia, la codifica di tali informazioni non consente di modificarle facilmente in un secondo momento. Il framework Content Sync supporta questo caso di utilizzo cercando un nodo manifesto nella configurazione, che è semplicemente identificato per nome e non richiede un tipo di configurazione. Ogni proprietà definita su quel particolare nodo viene aggiunta a un file, che viene anche chiamato manifest e risiede nella radice del file zip.

Nell&#39;esempio, la pagina di elenco eventi deve essere la pagina iniziale. Queste informazioni vengono fornite nella proprietà **indexPage** e possono quindi essere facilmente modificate in qualsiasi momento. Una seconda proprietà definisce il percorso del file *events.plist*. Come vedremo in seguito, l&#39;applicazione client ora può leggere il manifesto e agire in base ad esso.

Non appena la configurazione è configurata, il contenuto può essere scaricato con un browser o con qualsiasi altro client HTTP, o se si sta sviluppando per iOS, è possibile utilizzare la libreria client WAppKitSync dedicata. Il percorso di download è composto dal percorso di configurazione e dall&#39;estensione *.zip*, ad esempio quando si utilizza un&#39;istanza AEM locale: *http://localhost:4502/content/weretail_go.zip*

### Console di sincronizzazione dei contenuti {#the-content-sync-console}

La console Content Sync elenca tutte le configurazioni di Content Sync presenti nella directory archivio (tutti i nodi di tipo `cq:ContentSyncConfig`) e per ogni configurazione è possibile effettuare le seguenti operazioni:

* Aggiornare la cache.
* Cancellate la cache.
* Scaricate un file ZIP completo.
* Scaricate un file ZIP diverso da ora a una data e un&#39;ora specifiche.

Può essere utile per lo sviluppo e la risoluzione dei problemi.

È possibile accedere alla console all’indirizzo:

`http://localhost:4502/libs/cq/contentsync/content/console.html`

Si presenta come segue:

![chlimage_1-50](assets/chlimage_1-50.png)

### Estensione del framework di sincronizzazione dei contenuti {#extending-the-content-sync-framework}

Anche se il numero di opzioni di configurazione è già abbastanza ampio, potrebbe non coprire tutti i requisiti del caso d&#39;uso specifico. Questa sezione descrive i punti di estensione del framework Content Sync e come creare tipi di configurazione personalizzati.

Per ciascun tipo di configurazione, è presente un *Gestore aggiornamento contenuto*, ovvero una fabbrica di componenti OSGi registrata per quel tipo specifico. Questi gestori raccolgono il contenuto, lo elaborano e lo aggiungono a una cache gestita dal framework Content Sync. Implementa la seguente interfaccia o classe base astratta:

* `com.day.cq.contentsync.handler.ContentUpdateHandler` - Interfaccia che tutti i gestori di aggiornamenti devono implementare
* `com.day.cq.contentsync.handler.AbstractSlingResourceUpdateHandler` - Una classe astratta che semplifica il rendering delle risorse utilizzando Sling

Registra la classe come componente factory OSGi e distribuiscila nel contenitore OSGi in un bundle. Questo può essere fatto utilizzando il plugin [Maven SCR](https://felix.apache.org/site/apache-felix-maven-scr-plugin.html) utilizzando i tag JavaDoc o le annotazioni. L&#39;esempio seguente mostra la versione JavaDoc:

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

Tenere presente che la definizione *factory* contiene l&#39;interfaccia comune e il tipo personalizzato separati da una barra. Questa strategia consente al framework Content Sync di trovare e creare un&#39;istanza della classe personalizzata in quanto riconosce il tipo personalizzato in una voce di configurazione. Nella sezione successiva è riportato un esempio concreto di un gestore di aggiornamenti personalizzato.

>[!CAUTION]
>
>Quando si crea sulla classe base AbstractSlingResourceUpdateHandler, è necessario aggiungere la definizione *inherit*. In caso contrario, il contenitore OSGi non imposta i riferimenti richiesti dichiarati nella classe base.

### Implementazione di un gestore di aggiornamento personalizzato {#implementing-a-custom-update-handler}

Ogni pagina Mobile We.Retail contiene un logo nell&#39;angolo in alto a sinistra che vorremmo includere nel file zip, ovviamente. Tuttavia, per l&#39;ottimizzazione della cache, AEM non fa riferimento alla posizione reale del file immagine nell&#39;archivio, il che ci impedisce di utilizzare semplicemente il tipo di configurazione **copy**. Ciò che dobbiamo fare è fornire il nostro tipo di configurazione **logo** che rende l&#39;immagine disponibile nella posizione richiesta da AEM. Il seguente elenco di codici mostra l’implementazione completa del gestore di aggiornamenti per il logo:

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

La classe `LogoUpdateHandler` implementa il metodo `ContentUpdateHandler` dell&#39;interfaccia `updateCacheEntry(ConfigEntry, Long, String, Session, Session)`, che accetta diversi argomenti:

* Un&#39;istanza `ConfigEntry` che fornisce l&#39;accesso alla voce di configurazione, per la quale viene chiamato il gestore, e alle relative proprietà.
* Una marca temporale `lastUpdated` che indica l&#39;ultima volta che Content Sync ha aggiornato la propria cache. Il contenuto che non è stato modificato dopo tale marca temporale non deve essere aggiornato dal gestore.
* Argomento `configCacheRoot` che specifica il percorso principale della cache. Tutti i file aggiornati devono essere memorizzati sotto questo percorso per essere aggiunti al file zip.
* Sessione amministrativa da utilizzare per tutte le operazioni di repository correlate alla cache.
* Una sessione utente che può essere utilizzata per aggiornare il contenuto nel contesto di un determinato utente e fornire quindi un tipo di contenuto personalizzato.

Per implementare il gestore personalizzato, create innanzitutto un&#39;istanza della classe Image basata sulla risorsa specificata nella voce di configurazione. Questa è sostanzialmente la stessa procedura usata dal componente logo nelle nostre pagine. Assicurarsi che il percorso di destinazione dell&#39;immagine sia lo stesso di quello a cui si fa riferimento in una pagina.

Quindi, verificate che la risorsa sia stata modificata dopo l’ultimo aggiornamento. Le implementazioni personalizzate devono evitare gli aggiornamenti non necessari della cache e restituire false in caso di mancata modifica. Se la risorsa è stata modificata, copiate l’immagine nella posizione di destinazione prevista relativa alla directory principale della cache. Infine, `true` viene restituito per indicare al framework che la cache è stata aggiornata.

## Utilizzo del contenuto sul client {#using-the-content-on-the-client}

Per utilizzare il contenuto in un&#39;app mobile fornita da Content Sync, è necessario richiedere il contenuto tramite una connessione HTTP o HTTPS. Di conseguenza, il contenuto recuperato (compresso in un file ZIP) può essere estratto e memorizzato localmente sul dispositivo mobile. Si noti che il contenuto non si riferisce solo ai dati ma anche alla logica, vale a dire alle applicazioni Web complete; in modo da consentire all&#39;utente mobile di eseguire le applicazioni Web recuperate e i dati corrispondenti anche senza connettività di rete.

Content Sync distribuisce i contenuti in modo intelligente: Vengono distribuite solo le modifiche apportate ai dati dall’ultima sincronizzazione dei dati riuscita, riducendo così il tempo necessario per il trasferimento dei dati. Al primo avvio di un&#39;applicazione le modifiche ai dati sono richieste dal 1° gennaio 1970, mentre successivamente sono richiesti solo i dati modificati dall&#39;ultima sincronizzazione riuscita. AEM utilizza un framework di comunicazione client per iOS per semplificare la comunicazione e il trasferimento dei dati, in modo che sia necessaria una quantità minima di codice nativo per abilitare un&#39;applicazione Web basata su iOS.

Tutti i dati trasferiti possono essere estratti nella stessa struttura di directory. Durante l&#39;estrazione dei dati non sono necessari passaggi aggiuntivi (ad es. controlli delle dipendenze). Nel caso di iOS, tutti i dati vengono memorizzati in una sottocartella all&#39;interno della cartella Documenti dell&#39;app iOS.

Percorso di esecuzione tipico di un&#39;app AEM Mobile basata su iOS :

* L&#39;utente avvia l&#39;app sul dispositivo iOS.
* L&#39;app tenta di connettersi a AEM backend e richiede modifiche ai dati dall&#39;ultima esecuzione.
* Il server recupera i dati in questione e li comprime in un file.
* I dati vengono restituiti al dispositivo client in cui sono estratti nella cartella dei documenti.
* Il componente UIWebView viene avviato/aggiornato.

Se non è stato possibile stabilire una connessione, verranno visualizzati i dati scaricati in precedenza.

### Risorse aggiuntive {#additional-resources}

Per informazioni su ruoli e responsabilità di un amministratore e di un autore, consulta le risorse seguenti:

* [Creazione AEM contenuto per  AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md)
* [Amministrazione di contenuti da utilizzare  AEM Mobile On-demand Services](/help/mobile/aem-mobile.md)

