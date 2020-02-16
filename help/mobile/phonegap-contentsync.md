---
title: Mobile con sincronizzazione dei contenuti
seo-title: Mobile con sincronizzazione dei contenuti
description: Seguite questa pagina per informazioni su Content Sync for Adobe PhoneGap Enterprise with AEM (Sincronizzazione dei contenuti per Adobe PhoneGap Enterprise con AEM).
seo-description: Seguite questa pagina per informazioni su Content Sync for Adobe PhoneGap Enterprise with AEM (Sincronizzazione dei contenuti per Adobe PhoneGap Enterprise con AEM).
uuid: c3a82171-e070-4e32-b1ef-26e65ae23d99
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 923fc031-1a06-4a9d-94da-a2a4e82c54ee
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Mobile con sincronizzazione dei contenuti{#mobile-with-content-sync}

>[!NOTE]
>
>Adobe consiglia di utilizzare SPA Editor per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Questo documento fa parte della Guida [introduttiva di AEM Mobile](/help/mobile/getting-started-aem-mobile.md) , un punto di partenza consigliato per il riferimento AEM Mobile.

Utilizzate Content Sync (Sincronizzazione contenuti) per creare pacchetti di contenuto in modo che possa essere utilizzato nelle applicazioni mobili native. Le pagine create in AEM possono essere utilizzate come contenuto dell&#39;app, anche quando il dispositivo è offline. Inoltre, poiché le pagine AEM sono basate su standard Web, funzionano su più piattaforme e possono essere incorporate in qualsiasi wrapper nativo. Questa strategia riduce il lavoro di sviluppo e consente di aggiornare facilmente il contenuto delle app.

>[!NOTE]
>
>Le app PhoneGap create con gli strumenti AEM sono già configurate per utilizzare le pagine AEM come contenuto tramite Content Sync.

Il framework Content Sync crea un file di archivio che contiene il contenuto Web. Il contenuto può essere costituito da pagine semplici, immagini e file PDF o da intere applicazioni Web. L&#39;API Content Sync consente di accedere al file di archivio dalle app mobili o dai processi di creazione in modo che il contenuto possa essere recuperato e incluso nell&#39;app.

La seguente sequenza di passaggi illustra un caso d’uso tipico per la sincronizzazione dei contenuti:

1. Lo sviluppatore AEM crea una configurazione Content Sync che specifica il contenuto da includere.
1. Il framework Content Sync raccoglie e memorizza nella cache il contenuto.
1. Su un dispositivo mobile, l’applicazione mobile viene avviata e richiede il contenuto dal server, che viene distribuito in un file ZIP.
1. Il client scomprime il contenuto ZIP nel file system locale. La struttura delle cartelle nel file ZIP simula i percorsi che un client (ad es. un browser) richiederebbe normalmente dal server.
1. Il client apre il contenuto in un browser incorporato o lo utilizza in altro modo.
1. Successivamente, il client richiede il contenuto aggiornato dal server. Il framework Content Sync offre aggiornamenti incrementali per ridurre le dimensioni e il tempo di download, che possono essere importanti per i dispositivi mobili a causa di larghezza di banda o volumi di dati limitati.

>[!NOTE]
>
>Per ulteriori informazioni sulle linee guida per lo sviluppo di gestori di sincronizzazione dei contenuti e per consultare i gestori di app disponibili, consulta [Sviluppo di gestori](/help/mobile/contentsync-app-handlers.md)di sincronizzazione dei contenuti.

## Configurazione di Content Sync Content Content {#configuring-the-content-sync-content}

Create una configurazione di sincronizzazione dei contenuti per specificare il contenuto del file ZIP consegnato al client. Potete creare un numero qualsiasi di configurazioni di sincronizzazione dei contenuti. Ogni configurazione ha un nome a scopo di identificazione.

Per creare una configurazione di sincronizzazione dei contenuti, aggiungete un `cq:ContentSyncConfig` nodo alla directory archivio, con la `sling:resourceType` proprietà impostata su `contentsync/config`. Il `cq:ContentSyncConfig` nodo può trovarsi ovunque nell&#39;archivio, ma deve essere accessibile agli utenti dell&#39;istanza di pubblicazione AEM. Pertanto, è necessario aggiungere il nodo seguente `/content`.

Per specificare il contenuto del file ZIP Content Sync, aggiungete nodi secondari al nodo cq:ContentSyncConfig. Le seguenti proprietà di ciascun nodo figlio identificano un elemento di contenuto da includere e come viene elaborato al momento dell&#39;aggiunta:

* `path`: Posizione del contenuto.
* `type`: Nome del tipo di configurazione da utilizzare per l&#39;elaborazione del contenuto. Diversi tipi sono disponibili e sono descritti in Tipi di configurazione.

Consultate Esempio di configurazione della sincronizzazione dei contenuti.

Dopo aver creato la configurazione di sincronizzazione dei contenuti, questa viene visualizzata nella console di sincronizzazione dei contenuti.

>[!NOTE]
>
>Il framework Content Sync non verifica che le dipendenze delle risorse e dei file relativi alla progettazione siano inclusi nei pacchetti Content Sync. Accertatevi di includere tutti i file richiesti nel file ZIP.

### Configurazione dell&#39;accesso ai download della sincronizzazione dei contenuti {#configuring-access-to-content-sync-downloads}

Specificate un utente o un gruppo che possa scaricare da Content Sync. Potete configurare l’utente o il gruppo predefinito che può essere scaricato da tutte le cache di sincronizzazione dei contenuti, nonché ignorare i valori predefiniti e configurare l’accesso per una specifica configurazione di sincronizzazione dei contenuti.

Quando AEM è installato, i membri del gruppo di amministratori possono scaricare da Content Sync per impostazione predefinita.

### Impostazione dell&#39;accesso predefinito per i download di sincronizzazione dei contenuti {#setting-the-default-access-for-content-sync-downloads}

Il servizio Day CQ Content Sync Manager controlla l&#39;accesso a Content Sync. Configurate questo servizio per specificare l&#39;utente o il gruppo che può scaricare da Content Sync per impostazione predefinita.

Se state [configurando il servizio tramite la console](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)Web, digitate il nome dell&#39;utente o del gruppo come valore della proprietà Autorizzabile cache di fallback.

Se state [configurando il repository](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository), utilizzate le seguenti informazioni sul servizio:

* PID: com.day.cq.contentsync.impl.ContentSyncManagerImpl
* Nome proprietà: contentsync.fallback.authorizable

#### Sostituzione dell&#39;accesso per il download per una cache di sincronizzazione dei contenuti {#overriding-download-access-for-a-content-sync-cache}

Per configurare l&#39;accesso al download per una configurazione specifica di Content Sync, aggiungete la seguente proprietà al `cq:ContentSyncConfig` nodo:

* Nome: autorizzabile
* Tipo:Stringa
* Valore: Nome dell’utente o del gruppo che può essere scaricato.

Ad esempio, l&#39;app consente agli utenti di installare gli aggiornamenti direttamente da Content Sync. Per consentire a tutti gli utenti di scaricare l&#39;aggiornamento, impostate il valore della proprietà autorizzabile su `everyone`.

Se il `cq:ContentSyncConfig` nodo non dispone di proprietà autorizzabile, l’utente o il gruppo predefinito configurato per la proprietà Autorizzabile cache di fallback del servizio Gestione sincronizzazione contenuti di Day CQ determina chi può scaricare.

### Configurazione dell’utente per l’aggiornamento di una cache di sincronizzazione dei contenuti {#configuring-the-user-for-updating-a-content-sync-cache}

Quando un utente esegue un aggiornamento alla cache di sincronizzazione dei contenuti, un account utente specifico esegue l&#39;azione per conto dell&#39;utente. L&#39;utente anonimo aggiorna tutte le cache di sincronizzazione dei contenuti per impostazione predefinita.

Potete ignorare l’utente predefinito e specificare un utente o un gruppo che aggiorna una cache di sincronizzazione dei contenuti specifica.

Per ignorare l’utente predefinito, specificate un utente o un gruppo che esegue gli aggiornamenti per una specifica configurazione Content Sync aggiungendo la seguente proprietà al nodo cq:ContentSyncConfig:

* Nome: updateuser
* Tipo:Stringa
* Valore: Nome dell’utente o del gruppo che può eseguire gli aggiornamenti.

Se il nodo cq:ContentSyncConfig non dispone di proprietà updateuser, l&#39;utente anonimo predefinito aggiorna la cache.

### Tipi di configurazione {#configuration-types}

L&#39;elaborazione può variare dal rendering di JSON semplice al rendering completo delle pagine, incluse le risorse di riferimento. In questa sezione sono elencati i tipi di configurazione disponibili e i relativi parametri specifici:

**copia** È sufficiente copiare file e cartelle.

* **percorso** - Se il percorso punta a un singolo file, viene copiato solo il file. Se punta a una cartella (che include i nodi di pagina), verranno copiati tutti i file e le cartelle sottostanti.

**contenuto** Rendering del contenuto tramite l&#39;elaborazione standard di richieste Sling.

* **percorso** - Percorso della risorsa da restituire.
* **estensione** - Estensione da utilizzare nella richiesta. Esempi comuni sono *html* e *json*, ma qualsiasi altra estensione è possibile.

* **selettore** - Selettori opzionali separati da punto. Esempi comuni sono *touch* per il rendering delle versioni mobili di una pagina o *infinito* per l’output JSON.

**clientlib** Creare un pacchetto con una libreria client Javascript o CSS.

* **percorso** - Percorso della directory principale della libreria client.
* **extension** - Tipo di libreria client. Al momento dovrebbe essere impostato su *js* o *css* .

* **includeFolders** - Type è un array di stringhe che consente all&#39;utente di specificare ulteriori cartelle da analizzare nella libreria client per recuperare i file (ad esempio font personalizzati).

**assets**

Raccogliere le rappresentazioni originali delle risorse.

* **percorso** - Percorso di una cartella di risorse sotto /content/dam.
* **rappresentazioni** - Tipo è un array di stringhe che consente all&#39;utente di specificare quali rappresentazioni utilizzare invece dell&#39;immagine predefinita. Nell&#39;elenco seguente sono riepilogate alcune rappresentazioni pronte all&#39;uso, ma è anche possibile utilizzare qualsiasi rappresentazione creata dal flusso di lavoro:

   * *originale*
   * *cq5dam.thumbnail.48.48.png*
   * *cq5dam.thumbnail.319.319.png*
   * *cq5dam.thumbnail.140.100.png*
   * *cq5dam.web.1280.1280.png*

**immagine** Consente di raccogliere un’immagine.

* **percorso** - Percorso di una risorsa immagine.

Il tipo di immagine viene utilizzato per includere il logo We.Retail nel file zip.

**pagine** Rendering delle pagine AEM e raccolta delle risorse di riferimento.

* **percorso** - Percorso di una pagina.
* **estensione** - Estensione da utilizzare nella richiesta. Per le pagine questo è quasi sempre *html*, ma altri sono ancora possibili.

* **selettore** - Selettori opzionali separati da punto. Esempi comuni sono *touch* per il rendering delle versioni mobili di una pagina.

* **deep** - Proprietà booleana opzionale che determina se includere anche le pagine figlie. The default value is *true.*

* **includeImages** - Proprietà booleana opzionale che determina se le immagini devono essere incluse. The default value is *true*.
Per impostazione predefinita, sono considerati per l’inclusione solo i componenti immagine con un tipo di risorsa di base/componenti/immagine. È possibile aggiungere altri tipi di risorse configurando il gestore **di aggiornamento delle pagine CQ WCM** Day nella console Web.

**riscrittura** Il nodo di riscrittura definisce il modo in cui i collegamenti vengono riscritti nella pagina esportata. I collegamenti riscritti possono puntare ai file inclusi nel file zip o alle risorse sul server.

Il `rewrite` nodo deve trovarsi sotto il `page` nodo.

Il `rewrite` nodo può avere una o più delle seguenti proprietà:

* `clientlibs`: riscrive i percorsi clientlibs.

* `images`: riscrive i percorsi delle immagini.
* `links`: riscrive i percorsi dei collegamenti.

Ogni proprietà può avere uno dei seguenti valori:

* `REWRITE_RELATIVE`: riscrive il percorso con una posizione relativa al file .html della pagina nel file system.

* `REWRITE_EXTERNAL`: riscrive il percorso puntando la risorsa sul server, utilizzando il servizio [AEM](/help/sites-developing/externalizer.md)Externalizer.

Il servizio AEM denominato **PathRewriterTransformerFactory** consente di configurare gli attributi HTML specifici che verranno riscritti. Il servizio può essere configurato nella console Web e dispone di una configurazione per ciascuna proprietà del `rewrite` nodo: `clientlibs`, `images` e `links`.

Questa funzione è stata aggiunta in AEM 5.5.

### Esempio di configurazione della sincronizzazione dei contenuti {#example-content-sync-configuration}

L&#39;elenco seguente mostra una configurazione di esempio per Content Sync.

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

**etc.designs.default e etc.designs.mobile** Le prime due voci della configurazione dovrebbero essere abbastanza ovvie. Poiché includeremo una serie di pagine mobili, abbiamo bisogno dei relativi file di progettazione qui sotto /etc/designs. E poiché non è richiesta ulteriore elaborazione, la copia è sufficiente.

**events.plist** Questa voce è un po&#39; speciale. Come indicato nell&#39;introduzione, l&#39;applicazione deve fornire una visualizzazione mappa con gli indicatori delle posizioni degli eventi. Forniremo le informazioni di posizione necessarie come file separato in formato PLIST. A tal fine, il componente dell&#39;elenco eventi utilizzato nella pagina di indice ha uno script denominato plist.jsp. Questo script viene eseguito quando la risorsa del componente viene richiesta con l&#39;estensione .plist. Come al solito, il percorso dei componenti viene indicato nella proprietà path e il tipo è impostato su content, perché desideriamo sfruttare l&#39;elaborazione delle richieste Sling.

**events.touch.html** Verrà visualizzata la pagina effettiva nell&#39;app. La proprietà path è impostata sulla pagina principale dell&#39;evento. Vengono incluse anche tutte le pagine dell&#39;evento al di sotto di tale pagina, poiché per impostazione predefinita la proprietà deep è impostata su true. Utilizziamo le pagine come tipo di configurazione, in modo che vengano incluse tutte le immagini o altri file a cui può fare riferimento un’immagine o un componente per il download in una pagina. Inoltre, l’impostazione del selettore touch offre una versione mobile delle pagine. La configurazione nel pacchetto di caratteristiche contiene più voci di questo tipo, ma qui sono lasciate fuori per semplicità.

**logo** Il tipo di configurazione del logo non è stato menzionato finora e non è uno dei tipi predefiniti. Tuttavia, il framework Content Sync (Sincronizzazione contenuti) è estensibile in qualche misura e questo è un esempio di ciò, che sarà trattato nella sezione successiva.

**manifest** È spesso consigliabile includere nel file ZIP qualche tipo di metadati, ad esempio la pagina iniziale del contenuto. Tuttavia, la codifica di tali informazioni non consente di modificarle facilmente in un secondo momento. Il framework Content Sync supporta questo caso di utilizzo cercando un nodo manifesto nella configurazione, che è semplicemente identificato per nome e non richiede un tipo di configurazione. Ogni proprietà definita su quel particolare nodo viene aggiunta a un file, che viene anche chiamato manifest e risiede nella radice del file zip.

Nell&#39;esempio, la pagina di elenco eventi deve essere la pagina iniziale. Queste informazioni vengono fornite nella proprietà **indexPage** e possono quindi essere facilmente modificate in qualsiasi momento. Una seconda proprietà definisce il percorso del file *events.plist* . Come vedremo in seguito, l&#39;applicazione client ora può leggere il manifesto e agire in base ad esso.

Non appena la configurazione è configurata, il contenuto può essere scaricato con un browser o con qualsiasi altro client HTTP, o se si sta sviluppando per iOS, è possibile utilizzare la libreria client WAppKitSync dedicata. Il percorso di download è composto dal percorso di configurazione e dall’estensione *.zip* , ad esempio quando si utilizza un’istanza AEM locale: *https://localhost:4502/content/weretail_go.zip*

### Console di sincronizzazione dei contenuti {#the-content-sync-console}

La console Content Sync elenca tutte le configurazioni di Content Sync presenti nella directory archivio (tutti i nodi di tipo `cq:ContentSyncConfig`) e per ogni configurazione è possibile effettuare le seguenti operazioni:

* Aggiornare la cache.
* Cancellate la cache.
* Scaricate un file ZIP completo.
* Scaricate un file ZIP diverso da ora a una data e ora specifiche.

Può essere utile per lo sviluppo e la risoluzione dei problemi.

È possibile accedere alla console all’indirizzo:

`https://localhost:4502/libs/cq/contentsync/content/console.html`

Si presenta come segue:

![chlimage_1](assets/chlimage_1.png)

### Estensione del framework Content Sync {#extending-the-content-sync-framework}

Anche se il numero di opzioni di configurazione è già abbastanza ampio, potrebbe non coprire tutti i requisiti del caso d&#39;uso specifico. Questa sezione descrive i punti di estensione del framework Content Sync e come creare tipi di configurazione personalizzati.

Per ogni tipo di configurazione, è presente un gestore *di aggiornamento* contenuto, ovvero un componente factory OSGi registrato per quel tipo specifico. Questi gestori raccolgono il contenuto, lo elaborano e lo aggiungono a una cache gestita dal framework Content Sync. Implementa la seguente interfaccia o classe base astratta:

* `com.day.cq.contentsync.handler.ContentUpdateHandler` - Interfaccia che tutti i gestori di aggiornamenti devono implementare
* `com.day.cq.contentsync.handler.AbstractSlingResourceUpdateHandler` - Una classe astratta che semplifica il rendering delle risorse utilizzando Sling

Registra la classe come componente factory OSGi e distribuiscila nel contenitore OSGi in un bundle. Questo può essere fatto utilizzando il plugin [](https://felix.apache.org/site/apache-felix-maven-scr-plugin.html) Maven SCR sia tramite i tag JavaDoc o le annotazioni. L&#39;esempio seguente mostra la versione JavaDoc:

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

La definizione *factory* contiene l&#39;interfaccia comune e il tipo personalizzato separati da una barra. Questa strategia consente al framework Content Sync di trovare e creare un&#39;istanza della classe personalizzata in quanto riconosce il tipo personalizzato in una voce di configurazione. Nella sezione successiva è riportato un esempio concreto di un gestore di aggiornamenti personalizzato.

>[!CAUTION]
>
>Quando si crea sulla classe base AbstractSlingResourceUpdateHandler, è necessario aggiungere la definizione di *ereditarietà* . In caso contrario, il contenitore OSGi non imposta i riferimenti richiesti dichiarati nella classe base.

### Implementazione di un gestore di aggiornamenti personalizzato {#implementing-a-custom-update-handler}

Ogni pagina Mobile We.Retail contiene un logo nell&#39;angolo in alto a sinistra che vorremmo includere nel file zip, ovviamente. Tuttavia, per l’ottimizzazione della cache, AEM non fa riferimento alla posizione reale del file immagine nell’archivio, il che ci impedisce di utilizzare semplicemente il tipo di configurazione della **copia** . Ciò che dobbiamo fare è fornire il nostro tipo di configurazione del **logo** che renda l’immagine disponibile nella posizione richiesta da AEM. Il seguente elenco di codici mostra l’implementazione completa del gestore di aggiornamenti per il logo:

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

La `LogoUpdateHandler` classe implementa il metodo dell&#39; `ContentUpdateHandler` interfaccia `updateCacheEntry(ConfigEntry, Long, String, Session, Session)` , che prende una serie di argomenti:

* Un&#39; `ConfigEntry` istanza che fornisce l&#39;accesso alla voce di configurazione, per la quale viene chiamato il gestore, e alle relative proprietà.
* Una `lastUpdated` marca temporale che indica l&#39;ultima volta che Content Sync ha aggiornato la propria cache. Il contenuto che non è stato modificato dopo tale marca temporale non deve essere aggiornato dal gestore.
* Un `configCacheRoot` argomento che specifica il percorso principale della cache. Tutti i file aggiornati devono essere memorizzati sotto questo percorso per essere aggiunti al file zip.
* Sessione amministrativa da utilizzare per tutte le operazioni di repository correlate alla cache.
* Una sessione utente che può essere utilizzata per aggiornare il contenuto nel contesto di un determinato utente e fornire quindi un tipo di contenuto personalizzato.

Per implementare il gestore personalizzato, create innanzitutto un&#39;istanza della classe Image basata sulla risorsa specificata nella voce di configurazione. Questa è sostanzialmente la stessa procedura usata dal componente logo nelle nostre pagine. Assicurarsi che il percorso di destinazione dell&#39;immagine sia lo stesso di quello a cui si fa riferimento in una pagina.

Quindi, verificate che la risorsa sia stata modificata dopo l’ultimo aggiornamento. Le implementazioni personalizzate devono evitare gli aggiornamenti non necessari della cache e restituire false in caso di mancata modifica. Se la risorsa è stata modificata, copiate l’immagine nella posizione di destinazione prevista relativa alla directory principale della cache. Infine, `true` viene restituito per indicare al framework che la cache è stata aggiornata.

## Utilizzo del contenuto sul client {#using-the-content-on-the-client}

Per utilizzare il contenuto in un&#39;app mobile fornita da Content Sync, è necessario richiedere il contenuto tramite una connessione HTTP o HTTPS. Di conseguenza, il contenuto recuperato (compresso in un file ZIP) può essere estratto e memorizzato localmente sul dispositivo mobile. Si noti che il contenuto non si riferisce solo ai dati ma anche alla logica, vale a dire alle applicazioni Web complete; in modo da consentire all&#39;utente mobile di eseguire applicazioni Web recuperate e dati corrispondenti anche senza connettività di rete.

Content Sync distribuisce contenuti in modo intelligente: Vengono distribuite solo le modifiche apportate ai dati dall’ultima sincronizzazione dei dati riuscita, riducendo così il tempo necessario per il trasferimento dei dati. Al primo avvio di un&#39;applicazione le modifiche ai dati sono richieste dal 1° gennaio 1970, mentre successivamente sono richiesti solo i dati modificati dall&#39;ultima sincronizzazione riuscita. AEM utilizza un framework di comunicazione client per iOS per semplificare la comunicazione e il trasferimento dei dati, in modo che sia necessaria una quantità minima di codice nativo per abilitare un&#39;applicazione Web basata su iOS.

Tutti i dati trasferiti possono essere estratti nella stessa struttura di directory. Durante l&#39;estrazione dei dati non sono necessari passaggi aggiuntivi (ad es. controlli delle dipendenze). Nel caso di iOS, tutti i dati vengono memorizzati in una sottocartella all&#39;interno della cartella Documenti dell&#39;app iOS.

Percorso di esecuzione tipico di un&#39;app AEM Mobile basata su iOS:

* L&#39;utente avvia l&#39;app sul dispositivo iOS.
* L&#39;app tenta di connettersi al backend AEM e richiede modifiche ai dati dall&#39;ultima esecuzione.
* Il server recupera i dati in questione e li comprime in un file.
* I dati vengono restituiti al dispositivo client in cui sono estratti nella cartella dei documenti.
* Il componente UIWebView viene avviato/aggiornato.

Se non è stato possibile stabilire una connessione, verranno visualizzati i dati scaricati in precedenza.

### Come {#getting-ahead}

Per informazioni su ruoli e responsabilità di un amministratore e sviluppatore, consulta le risorse seguenti:

* [Authoring per Adobe PhoneGap Enterprise con AEM](/help/mobile/phonegap.md)
* [Amministrazione di contenuti per Adobe PhoneGap Enterprise con AEM](/help/mobile/administer-phonegap.md)

