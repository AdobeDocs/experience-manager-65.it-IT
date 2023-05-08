---
title: Sincronizzazione dei contenuti per Adobe PhoneGap Enterprise con AEM
description: Segui questa pagina per informazioni su Sincronizzazione dei contenuti per Adobe PhoneGap Enterprise con AEM.
uuid: c3a82171-e070-4e32-b1ef-26e65ae23d99
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 923fc031-1a06-4a9d-94da-a2a4e82c54ee
docset: aem65
exl-id: 2cadd9c5-4335-48d0-8d1c-941fca717409
source-git-commit: 85d39e59b82fdfdcd310be61787a315668aebe38
workflow-type: tm+mt
source-wordcount: '2977'
ht-degree: 0%

---

# Mobile con sincronizzazione dei contenuti{#mobile-with-content-sync}

>[!NOTE]
>
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Questo documento fa parte del [Guida introduttiva ad AEM Mobile](/help/mobile/getting-started-aem-mobile.md) Guida, un punto di partenza consigliato per riferimento AEM Mobile.

Utilizza Content Sync per creare un pacchetto di contenuti in modo che possa essere utilizzato nelle applicazioni mobili native. Le pagine create in AEM possono essere utilizzate come contenuto dell’app, anche quando il dispositivo è offline. Inoltre, poiché le pagine AEM sono basate su standard web, funzionano su più piattaforme e consentono di incorporarle in qualsiasi wrapper nativo. Questa strategia riduce lo sforzo di sviluppo e consente di aggiornare facilmente il contenuto delle app.

>[!NOTE]
>
>Le app PhoneGap create con strumenti AEM sono già configurate per utilizzare AEM pagine come contenuto tramite Content Sync.

Il framework Content Sync crea un file di archivio contenente il contenuto web. Il contenuto può essere qualsiasi cosa proveniente da pagine semplici, immagini e file PDF o da intere applicazioni Web. L’API Content Sync consente di accedere al file di archivio dalle app mobili o dai processi di creazione in modo che il contenuto possa essere recuperato e incluso nell’app.

La seguente sequenza di passaggi illustra un caso d’uso tipico per la sincronizzazione dei contenuti:

1. Lo sviluppatore AEM crea una configurazione Content Sync che specifica il contenuto da includere.
1. Il framework Content Sync raccoglie e memorizza in cache il contenuto.
1. Su un dispositivo mobile, l’app mobile viene avviata e richiede contenuto dal server, che viene consegnato in un file ZIP.
1. Il client scomprime il contenuto ZIP nel file system locale. La struttura delle cartelle nel file ZIP simula i percorsi che un client (ad esempio un browser) normalmente richiederebbe dal server.
1. Il client apre il contenuto in un browser incorporato o lo utilizza in altri modi.
1. Successivamente, le richieste client hanno aggiornato il contenuto dal server. Il framework Content Sync fornisce aggiornamenti incrementali per ridurre le dimensioni e il tempo di download, che possono essere importanti per i dispositivi mobili a causa di larghezza di banda o volumi di dati limitati.

>[!NOTE]
>
>Per ulteriori informazioni sulle linee guida per lo sviluppo dei gestori di sincronizzazione dei contenuti e dei gestori di app pronti all’uso, consulta [Sviluppo di gestori di sincronizzazione dei contenuti](/help/mobile/contentsync-app-handlers.md).

## Configurazione del contenuto di sincronizzazione dei contenuti {#configuring-the-content-sync-content}

Crea una configurazione di sincronizzazione dei contenuti per specificare il contenuto del file ZIP che viene inviato al client. Puoi creare un numero qualsiasi di configurazioni di Sincronizzazione dei contenuti. Ogni configurazione ha un nome a scopo di identificazione.

Per creare una configurazione di Content Sync, aggiungi una `cq:ContentSyncConfig` nodo del repository, con `sling:resourceType` proprietà impostata su `contentsync/config`. La `cq:ContentSyncConfig` Il nodo può trovarsi in qualsiasi punto dell&#39;archivio, tuttavia il nodo deve essere accessibile agli utenti nell&#39;istanza di pubblicazione AEM. Pertanto, devi aggiungere il nodo seguente `/content`.

Per specificare il contenuto del file ZIP di sincronizzazione del contenuto, aggiungi nodi figlio al nodo cq:ContentSyncConfig. Le seguenti proprietà di ciascun nodo figlio identificano un elemento di contenuto da includere e come viene elaborato quando lo si aggiunge:

* `path`: Posizione del contenuto.
* `type`: Nome del tipo di configurazione da utilizzare per l’elaborazione del contenuto. Sono disponibili diversi tipi descritti in Tipi di configurazione.

Consulta Esempio di configurazione della sincronizzazione dei contenuti .

Dopo aver creato la configurazione Content Sync, questa viene visualizzata nella console Content Sync.

>[!NOTE]
>
>Il framework Content Sync non controlla che le dipendenze delle risorse e dei file relativi alla progettazione siano inclusi nei pacchetti Content Sync. Assicurati di includere tutti i file richiesti nel file ZIP.

### Configurazione dell’accesso ai download della sincronizzazione dei contenuti {#configuring-access-to-content-sync-downloads}

Specifica un utente o un gruppo che può scaricare da Content Sync. È possibile configurare l’utente o il gruppo predefinito che può essere scaricato da tutte le cache di Sincronizzazione contenuto, nonché ignorare il valore predefinito e configurare l’accesso per una configurazione di Sincronizzazione contenuto specifica.

Quando AEM è installato, i membri del gruppo di amministratori possono scaricare da Content Sync per impostazione predefinita.

### Impostazione dell’accesso predefinito per i download della sincronizzazione dei contenuti {#setting-the-default-access-for-content-sync-downloads}

Il servizio Day CQ Content Sync Manager controlla l’accesso a Content Sync. Configura questo servizio per specificare l&#39;utente o il gruppo che può scaricare da Content Sync per impostazione predefinita.

Se sei [configurazione del servizio tramite la console Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console), digita il nome dell’utente o del gruppo come valore della proprietà Fallback Cache Authorizable .

Se sei [configurazione nell’archivio](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository), utilizza le seguenti informazioni sul servizio:

* PID: com.day.cq.contentsync.impl.ContentSyncManagerImpl
* Nome proprietà: contentsync.fallback.authorizable

#### Sovrascrittura dell’accesso al download per una cache di sincronizzazione dei contenuti {#overriding-download-access-for-a-content-sync-cache}

Per configurare l&#39;accesso per il download per una configurazione specifica di Content Sync, aggiungi la seguente proprietà alla `cq:ContentSyncConfig` nodo:

* Nome: autorizzabile
* Tipo: Stringa
* Valore: Nome dell&#39;utente o del gruppo che può essere scaricato.

Ad esempio, la tua app consente agli utenti di installare gli aggiornamenti direttamente da Content Sync. Per consentire a tutti gli utenti di scaricare l&#39;aggiornamento, impostare il valore della proprietà authorizable su `everyone`.

Se la `cq:ContentSyncConfig` Il nodo non dispone di proprietà autorizzabile. L&#39;utente o il gruppo predefinito configurato per la proprietà Autorizzabile della cache di fallback del servizio Day CQ Content Sync Manager determina chi può scaricare.

### Configurazione dell’utente per l’aggiornamento di una cache di sincronizzazione dei contenuti {#configuring-the-user-for-updating-a-content-sync-cache}

Quando un utente esegue un aggiornamento della cache di sincronizzazione dei contenuti, un account utente specifico esegue l’azione per conto dell’utente. Per impostazione predefinita, l’utente anonimo aggiorna tutte le cache di sincronizzazione dei contenuti.

È possibile ignorare l’utente predefinito e specificare un utente o un gruppo che aggiorna una cache di sincronizzazione dei contenuti specifica.

Per ignorare l&#39;utente predefinito, specifica un utente o un gruppo che esegue gli aggiornamenti per una configurazione specifica di Content Sync aggiungendo la seguente proprietà al nodo cq:ContentSyncConfig:

* Nome: updateuser
* Tipo: Stringa
* Valore: Nome dell&#39;utente o del gruppo che può eseguire gli aggiornamenti.

Se il nodo cq:ContentSyncConfig non ha alcuna proprietà updateuser, l&#39;utente anonimo predefinito aggiorna la cache.

### Tipi di configurazione {#configuration-types}

L’elaborazione può variare dal rendering di JSON semplice al rendering completo delle pagine, incluse le relative risorse di riferimento. In questa sezione sono elencati i tipi di configurazione disponibili e i relativi parametri specifici:

**copia** È sufficiente copiare file e cartelle.

* **path** - Se il percorso punta a un singolo file, viene copiato solo il file. Se punta a una cartella (inclusi i nodi di pagina), verranno copiati tutti i file e le cartelle seguenti.

**content** Esegui il rendering del contenuto utilizzando l’elaborazione standard delle richieste Sling.

* **path** - Percorso della risorsa da restituire.
* **estensione** - Estensione da utilizzare nella richiesta. Esempi comuni *html* e *json*, ma è possibile qualsiasi altra estensione.

* **selettore** - Selettori opzionali separati da punto. Esempi comuni *tocco* per il rendering delle versioni mobili di una pagina o *infinito* per l’output JSON.

**clientlib** Crea un pacchetto per una libreria client Javascript o CSS.

* **path** - Percorso della directory principale della libreria client.
* **estensione** - Tipo di libreria client. Questo valore deve essere impostato su *js* o *css* al momento.

* **includeFolders** - Tipo è un array di stringhe e consente all&#39;utente di specificare ulteriori cartelle da analizzare nella libreria client per recuperare file (come i font personalizzati).

**assets**

Raccogliere rappresentazioni originali delle risorse.

* **path** - Percorso di una cartella di risorse sotto /content/dam.
* **rendering** - Tipo è una matrice di stringhe che consente all&#39;utente di specificare quali rappresentazioni utilizzare invece dell&#39;immagine predefinita. Nell’elenco seguente sono riepilogate alcune rappresentazioni predefinite, ma è anche possibile utilizzare qualsiasi rappresentazione creata dal flusso di lavoro:

   * *originale*
   * *cq5dam.thumbnail.48.48.png*
   * *cq5dam.thumbnail.319.319.png*
   * *cq5dam.thumbnail.140.100.png*
   * *cq5dam.web.1280.1280.png*

**immagine** Raccogli un’immagine.

* **path** - Percorso di una risorsa immagine.

Il tipo di immagine viene utilizzato per includere il logo We.Retail nel file zip.

**pagine** Esegui il rendering AEM pagine e raccogli le risorse di riferimento.

* **path** - Percorso di una pagina.
* **estensione** - Estensione da utilizzare nella richiesta. Per le pagine questo è quasi sempre *html* Ma altri sono ancora possibili.

* **selettore** - Selettori opzionali separati da punto. Esempi comuni *tocco* per il rendering delle versioni mobili di una pagina.

* **profondo** - Proprietà booleana opzionale che determina se includere anche le pagine figlie. Il valore predefinito è *vero.*

* **includeImages** - Proprietà booleana opzionale che determina se le immagini devono essere incluse. Il valore predefinito è *true*.
Per impostazione predefinita, sono considerati per l’inclusione solo i componenti immagine con un tipo di risorsa foundation/components/image. Puoi aggiungere altri tipi di risorse configurando la variabile **Day CQ WCM Pages Update Handler** nella console Web.

**riscrittura** Il nodo di riscrittura definisce il modo in cui i collegamenti vengono riscritti nella pagina esportata. I collegamenti riscritti possono puntare ai file inclusi nel file zip o alle risorse sul server.

La `rewrite` il nodo deve essere posizionato sotto il `page` nodo.

La `rewrite` il nodo può avere una o più delle seguenti proprietà:

* `clientlibs`: riscrive i percorsi clientlibs.

* `images`: riscrive i percorsi delle immagini.
* `links`: riscrive i percorsi dei collegamenti.

Ogni proprietà può avere uno dei seguenti valori:

* `REWRITE_RELATIVE`: riscrive il percorso con una posizione relativa al file .html della pagina sul file system.

* `REWRITE_EXTERNAL`: riscrive il percorso indicando la risorsa sul server, utilizzando il AEM [Servizio Externalizer](/help/sites-developing/externalizer.md).

Il servizio AEM denominato **PathRewriterTransformerFactory** consente di configurare gli attributi html specifici che verranno riscritti. Il servizio può essere configurato nella console Web e dispone di una configurazione per ogni proprietà della `rewrite` nodo: `clientlibs`, `images` e `links`.

Questa funzione è stata aggiunta nella AEM 5.5.

### Esempio di configurazione della sincronizzazione dei contenuti {#example-content-sync-configuration}

L’elenco seguente mostra una configurazione di esempio per Sincronizzazione contenuto.

```java
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

**etc.designs.default e etc.designs.mobile** Le prime due voci della configurazione dovrebbero essere abbastanza ovvie. Poiché includeremo diverse pagine mobili, abbiamo bisogno dei relativi file di progettazione sotto /etc/designs. E poiché non è necessaria alcuna ulteriore elaborazione, la copia è sufficiente.

**events.plist** Questa voce è un po&#39; speciale. Come indicato nell’introduzione, l’applicazione deve fornire una vista mappa con i marcatori delle posizioni degli eventi. Forniremo le informazioni sulla posizione necessarie come file separato in formato PLIST. Affinché ciò funzioni, il componente elenco eventi utilizzato nella pagina indice ha uno script chiamato plist.jsp. Questo script viene eseguito quando la risorsa del componente viene richiesta con estensione .plist . Come al solito, il percorso dei componenti viene indicato nella proprietà path e il tipo è impostato su content, perché vogliamo sfruttare l&#39;elaborazione delle richieste Sling.

**events.touch.html** Vengono quindi visualizzate le pagine effettive nell’app. La proprietà path è impostata sulla pagina principale degli eventi. Saranno incluse anche tutte le pagine dell’evento al di sotto di tale pagina, perché la proprietà deep viene impostata per impostazione predefinita su true. Utilizziamo le pagine come tipo di configurazione, in modo che vengano incluse tutte le immagini o altri file a cui si può fare riferimento da un&#39;immagine o da un componente di download su una pagina. Inoltre, l’impostazione del selettore touch offre una versione mobile delle pagine. La configurazione nel feature pack contiene più voci di questo tipo, ma qui sono lasciate fuori per semplicità.

**logo** Il tipo di configurazione del logo non è stato menzionato finora e non è uno dei tipi incorporati. Tuttavia, il framework Content Sync è estensibile in un certo senso e questo è un esempio di ciò, che sarà trattato nella sezione successiva.

**manifest** Spesso è auspicabile che nel file zip sia incluso un qualche tipo di metadati, ad esempio la pagina iniziale del contenuto. Tuttavia, la codifica fissa di tali informazioni impedisce di modificarle facilmente in un secondo momento. Il framework Content Sync supporta questo caso d’uso cercando un nodo manifest nella configurazione, che è semplicemente identificato dal nome e non richiede un tipo di configurazione. Ogni proprietà definita su quel particolare nodo viene aggiunta a un file, che è anche chiamato manifest e risiede nella radice del file zip.

Nell’esempio, la pagina di elenco eventi deve essere la pagina iniziale. Queste informazioni sono fornite nella **indexPage** e può quindi essere facilmente modificato in qualsiasi momento. Una seconda proprietà definisce il percorso del *events.plist* file. Come vedremo più tardi, l&#39;applicazione client ora può leggere il manifesto e agire in base ad esso.

Non appena la configurazione viene configurata, il contenuto può essere scaricato con un browser o qualsiasi altro client HTTP, oppure se si sta sviluppando per iOS, è possibile utilizzare la libreria client WAppKitSync dedicata. Il percorso di download è costituito dal percorso della configurazione e dal *.zip* estensione, ad esempio quando si lavora con un&#39;istanza AEM locale: *https://localhost:4502/content/weretail_go.zip*

### Console Content Sync {#the-content-sync-console}

Nella console Content Sync sono elencate tutte le configurazioni di Content Sync nella directory archivio (tutti i nodi di tipo `cq:ContentSyncConfig`) e per ogni configurazione consente di effettuare le seguenti operazioni:

* Aggiorna la cache.
* Svuota la cache.
* Scarica uno zip completo.
* Scarica un file ZIP a confronto tra una data e un’ora specifiche.

Può essere utile per lo sviluppo e la risoluzione dei problemi.

Puoi accedere alla console da:

`https://localhost:4502/libs/cq/contentsync/content/console.html`

Si presenta come segue:

![chlimage_1](assets/chlimage_1.png)

### Estensione del framework di Content Sync {#extending-the-content-sync-framework}

Anche se il numero di opzioni di configurazione è già abbastanza ampio, potrebbe non coprire tutti i requisiti del tuo caso d&#39;uso specifico. Questa sezione descrive i punti di estensione del framework Content Sync e come creare tipi di configurazione personalizzati.

Per ogni tipo di configurazione, è disponibile un *Gestore dell’aggiornamento dei contenuti*, che è una fabbrica di componenti OSGi registrata per quel tipo specifico. Questi gestori raccolgono il contenuto, lo elaborano e lo aggiungono a una cache gestita dal framework Content Sync. Implementa la seguente interfaccia o classe base astratta:

* `com.day.cq.contentsync.handler.ContentUpdateHandler` - Interfaccia che tutti i gestori di aggiornamento devono implementare
* `com.day.cq.contentsync.handler.AbstractSlingResourceUpdateHandler` - Classe astratta che semplifica il rendering delle risorse utilizzando Sling

Registra la classe come componente factory OSGi e distribuiscila nel contenitore OSGi in un bundle. Questa operazione può essere eseguita utilizzando [Plug-in Maven SCR](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/apache-felix-maven-scr-plugin-use.html) utilizzando tag JavaDoc o annotazioni. L&#39;esempio seguente mostra la versione di JavaDoc:

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

Tieni presente che *fabbrica* La definizione contiene l&#39;interfaccia comune e il tipo personalizzato separati da barra. Questa strategia consente al framework Content Sync di trovare e creare un&#39;istanza della classe personalizzata in quanto riconosce il tipo personalizzato in una voce di configurazione. Nella sezione successiva viene illustrato un esempio concreto di un gestore di aggiornamento personalizzato.

>[!CAUTION]
>
>Quando si crea la classe base AbstractSlingResourceUpdateHandler, è necessario aggiungere il *ereditare* definizione. In caso contrario, il contenitore OSGi non imposta i riferimenti richiesti dichiarati nella classe base.

### Implementazione di un gestore di aggiornamento personalizzato {#implementing-a-custom-update-handler}

Ogni pagina mobile We.Retail contiene nell’angolo in alto a sinistra un logo che vorremmo includere nel file zip, ovviamente. Tuttavia, per l’ottimizzazione della cache, AEM non fa riferimento alla posizione reale del file immagine nell’archivio, il che ci impedisce di utilizzare semplicemente il **copia** tipo di configurazione. Quello che dobbiamo fare invece è fornire il nostro **logo** tipo di configurazione che rende l&#39;immagine disponibile nella posizione richiesta da AEM. Il seguente elenco di codici mostra la piena implementazione del gestore di aggiornamenti del logo:

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

La `LogoUpdateHandler` la classe implementa `ContentUpdateHandler` dell&#39;interfaccia `updateCacheEntry(ConfigEntry, Long, String, Session, Session)` metodo , che accetta diversi argomenti:

* A `ConfigEntry` istanza che fornisce l&#39;accesso alla voce di configurazione, per la quale è chiamato questo gestore, e alle relative proprietà.
* A `lastUpdated` marca temporale che indica l’ultima volta che la sincronizzazione dei contenuti ha aggiornato la cache. Il contenuto che non è stato modificato dopo tale marca temporale non deve essere aggiornato dal gestore.
* A `configCacheRoot` argomento che specifica il percorso principale della cache. Tutti i file aggiornati devono essere memorizzati sotto questo percorso per essere aggiunti al file zip.
* Una sessione amministrativa che deve essere utilizzata per tutte le operazioni di archivio relative alla cache.
* Sessione utente che può essere utilizzata per aggiornare il contenuto nel contesto di un determinato utente e quindi per fornire un tipo di contenuto personalizzato.

Per implementare il gestore personalizzato, crea prima un’istanza della classe Image basata sulla risorsa specificata nella voce di configurazione. Questa è sostanzialmente la stessa procedura del componente logo effettivo sulle nostre pagine. Assicurati che il percorso di destinazione dell&#39;immagine sia lo stesso di quello a cui si fa riferimento da una pagina.

Quindi, controlla se la risorsa è stata modificata dopo l’ultimo aggiornamento. Le implementazioni personalizzate devono evitare inutili aggiornamenti della cache e restituire false se non cambia nulla. Se la risorsa è stata modificata, copia l’immagine nella posizione di destinazione prevista relativa alla directory principale della cache. Infine, `true` viene restituito per indicare al framework che la cache è stata aggiornata.

## Utilizzo del contenuto sul client {#using-the-content-on-the-client}

Per utilizzare il contenuto in un’app mobile fornita da Content Sync, è necessario richiedere il contenuto tramite una connessione HTTP o HTTPS. Di conseguenza, il contenuto recuperato (compresso in un file ZIP) può essere estratto e memorizzato localmente sul dispositivo mobile. Si noti che il contenuto non si riferisce solo ai dati ma anche alla logica, vale a dire alle applicazioni web complete; consentendo così all’utente mobile di eseguire le applicazioni web recuperate e i dati corrispondenti anche senza connettività di rete.

La sincronizzazione dei contenuti offre contenuti in modo intelligente: Vengono distribuite solo le modifiche apportate ai dati dall’ultima sincronizzazione dei dati riuscita, riducendo così il tempo necessario per il trasferimento dei dati. Al primo avvio di un&#39;applicazione le modifiche ai dati sono richieste a partire dal 1° gennaio 1970, mentre successivamente vengono richiesti solo i dati modificati dall&#39;ultima sincronizzazione riuscita. AEM utilizza un framework di comunicazione client per iOS per semplificare la comunicazione e il trasferimento dei dati in modo che sia necessaria una quantità minima di codice nativo per abilitare un’applicazione web basata su iOS.

Tutti i dati trasferiti possono essere estratti nella stessa struttura di directory, non sono necessari passaggi aggiuntivi (ad esempio controlli di dipendenza) durante l’estrazione dei dati. Nel caso di iOS, tutti i dati vengono memorizzati in una sottocartella all’interno della cartella Documenti dell’app iOS.

Percorso di esecuzione tipico di un’app AEM Mobile basata su iOS:

* L&#39;utente avvia l&#39;app sul dispositivo iOS.
* L’app tenta di connettersi AEM backend e richiede modifiche ai dati dall’ultima esecuzione.
* Il server recupera i dati in questione e li comprime in un file.
* I dati vengono restituiti al dispositivo client in cui sono estratti nella cartella dei documenti.
* Il componente UIWebView avvia/aggiorna.

Se non è stato possibile stabilire una connessione, verranno visualizzati i dati scaricati in precedenza.

### Come procedere {#getting-ahead}

Per informazioni sui ruoli e le responsabilità di un amministratore e sviluppatore, consulta le risorse seguenti:

* [Authoring per Adobe PhoneGap Enterprise con AEM](/help/mobile/phonegap.md)
* [Amministrazione di contenuti per Adobe PhoneGap Enterprise con AEM](/help/mobile/administer-phonegap.md)
