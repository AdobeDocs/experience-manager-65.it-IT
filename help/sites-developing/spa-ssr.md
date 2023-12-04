---
title: Rendering lato server e SPA
description: Scopri SPA e il rendering lato server in Adobe Experience Manager.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
docset: aem65
exl-id: a80bc883-e0f6-4714-bd28-108262f96d77
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '1659'
ht-degree: 1%

---

# Rendering lato server e SPA{#spa-and-server-side-rendering}

>[!NOTE]
>
>L’editor SPA è la soluzione consigliata per i progetti che richiedono il rendering lato client basato sul framework SPA (ad esempio, React o Angular).

>[!NOTE]
>
>Per utilizzare le funzioni di rendering lato server dell’SPA descritte nel presente documento, è necessario disporre di Adobe Experience Manager (AEM) 6.5.1.0 o versione successiva.

## Panoramica {#overview}

Le applicazioni a pagina singola (SPA) possono offrire all’utente un’esperienza ricca e dinamica che reagisce e si comporta in modo familiare, spesso come un’applicazione nativa. [Ciò si ottiene affidandosi al client per caricare il contenuto in primo piano e poi fare il pesante sollevamento dell&#39;interazione dell&#39;utente](/help/sites-developing/spa-walkthrough.md#how-does-a-spa-work) riducendo al minimo la quantità di comunicazione necessaria tra client e server, rendendo l’app più reattiva.

Tuttavia, questo può portare a tempi di caricamento iniziali più lunghi, soprattutto se l’SPA è grande e ricco di contenuti. Per ottimizzare i tempi di caricamento, è possibile eseguire il rendering di alcuni contenuti lato server. L’utilizzo del rendering lato server (SSR) può accelerare il caricamento iniziale della pagina e quindi trasmettere un ulteriore rendering al client.

## Quando utilizzare SSR {#when-to-use-ssr}

SSR non è richiesto per tutti i progetti. Sebbene l’AEM supporti completamente la SSR JS per l’SPA, l’Adobe sconsiglia di attuarla sistematicamente per ogni progetto.

Quando decidi di implementare SSR, devi innanzitutto stimare quali ulteriori complessità, sforzi e costi aggiuntivi SSR rappresentano in modo realistico per il progetto, inclusa la manutenzione a lungo termine. Un’architettura SSR dovrebbe essere scelta solo quando il valore aggiunto supera chiaramente i costi stimati.

In genere, SSR fornisce un valore quando è presente un &quot;sì&quot; chiaro a una delle seguenti domande:

* **SEO:** SSR è ancora necessario per la corretta indicizzazione del sito da parte dei motori di ricerca che generano traffico? Tieni presente che i crawler del motore di ricerca principale ora valutano JS.
* **Velocità pagina:** SSR fornisce un miglioramento della velocità misurabile in ambienti reali e contribuisce all&#39;esperienza complessiva dell&#39;utente?

Solo quando ad almeno una di queste due domande viene risposto con un chiaro &quot;sì&quot; per il progetto, Adobe consiglia di implementare SSR. Le sezioni seguenti descrivono come eseguire questa operazione utilizzando Adobe I/O Runtime.

## Adobe I/O Runtime {#adobe-i-o-runtime}

Se [sono certi che il tuo progetto richieda l&#39;implementazione di SSR](/help/sites-developing/spa-ssr.md#when-to-use-ssr), la soluzione consigliata da Adobe è l’utilizzo di Adobe I/O Runtime.

Per ulteriori informazioni su Adobe I/O Runtime, vedi:

* [https://developer.adobe.com/runtime/](https://developer.adobe.com/runtime/) - Panoramica del servizio
* [https://developer.adobe.com/runtime/docs/](https://developer.adobe.com/runtime/docs/) - per la documentazione dettagliata sulla piattaforma

Le sezioni seguenti descrivono come Adobe I/O Runtime può essere utilizzato per implementare SSR per l’SPA in due modelli diversi:

* [Flusso di comunicazione basato sull’AEM](/help/sites-developing/spa-ssr.md#aem-driven-communication-flow)
* [Flusso di comunicazione basato su Adobe I/O Runtime](/help/sites-developing/spa-ssr.md#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>L’Adobe consiglia un’area di lavoro Adobe I/O Runtime separata per ogni ambiente (stage, prod, test e così via). Ciò consente di implementare i modelli SDLC (System Development Life Cycle) tipici con versioni diverse di una singola applicazione distribuite in ambienti diversi. Consulta il documento [CI/CD per applicazioni Project App Builder](https://developer.adobe.com/app-builder/docs/guides/deployment/ci_cd_for_firefly_apps/) per ulteriori informazioni.
>
>Un’area di lavoro separata non è necessaria per ogni istanza (Author, Publish) a meno che non vi siano differenze nell’implementazione runtime per tipo di istanza.

## Configurazione Remote Renderer {#remote-renderer-configuration}

L’AEM deve sapere dove è possibile recuperare i contenuti renderizzati in remoto. Indipendentemente da [il modello che si sceglie di implementare per SSR,](#adobe-i-o-runtime), è necessario specificare a AEM come accedere a questo servizio di rendering remoto.

Questa operazione viene eseguita tramite **RemoteContentRenderer - Servizio OSGi di Configuration Factory**. Cerca la stringa &quot;RemoteContentRenderer&quot; nella console di configurazione della console Web all&#39;indirizzo `http://<host>:<port>/system/console/configMgr`.

![Configurazione rendering](assets/rendererconfig.png)

Per la configurazione sono disponibili i seguenti campi:

* **Schema percorso contenuto** : espressione regolare che corrisponde a una parte del contenuto, se necessario
* **URL endpoint remoto** : URL dell’endpoint responsabile della generazione del contenuto
   * Utilizza il protocollo HTTPS protetto se non si trova nella rete locale.
* **Intestazioni di richiesta aggiuntive** - Intestazioni aggiuntive da aggiungere alla richiesta inviata all’endpoint remoto
   * Pattern: `key=value`
* **Timeout richiesta** - Timeout della richiesta dell&#39;host remoto in millisecondi

>[!NOTE]
>
>Indipendentemente da se scegli di implementare [Flusso di comunicazione basato sull&#39;AEM](#aem-driven-communication-flow) o [Flusso basato su Adobe I/O Runtime](#adobe-i-o-runtime-driven-communication-flow) è necessario definire una configurazione del renderer del contenuto remoto.
>
>Questa configurazione deve essere definita anche se scegli di [utilizzare un server Node.js personalizzato.](#using-node-js)

>[!NOTE]
>
>Questa configurazione utilizza [Rendering contenuto remoto,](#remote-content-renderer) che dispone di opzioni di estensione e personalizzazione aggiuntive.

## Flusso di comunicazione basato sull’AEM {#aem-driven-communication-flow}

Quando si utilizza SSR, il [flusso di lavoro di interazione dei componenti](/help/sites-developing/spa-overview.md#workflow) dell’SPA nell’AEM include una fase in cui il contenuto iniziale dell’app viene generato su Adobe I/O Runtime.

1. Il browser richiede il contenuto SSR all’AEM.

1. L&#39;AEM pubblica il modello su Adobe I/O Runtime.

1. Adobe I/O Runtime restituisce il contenuto generato.

1. AEM fornisce le HTML restituite da Adobe I/O Runtime tramite il modello HTL del componente pagina back-end.

![server-side-rendering-cms-drivenaemnode-adobeio](assets/server-side-rendering-cms-drivenaemnode-adobeio.png)

## Flusso di comunicazione basato su Adobe I/O Runtime {#adobe-i-o-runtime-driven-communication-flow}

La sezione precedente descrive l’implementazione standard e consigliata del rendering lato server per quanto riguarda l’SPA nell’AEM, in cui l’AEM esegue il bootstrapping e la distribuzione dei contenuti.

In alternativa, SSR può essere implementato in modo che Adobe I/O Runtime sia responsabile dell&#39;avvio, invertendo efficacemente il flusso di comunicazione.

Entrambi i modelli sono validi e supportati dall’AEM. Tuttavia, si dovrebbero considerare i vantaggi e gli svantaggi di ciascuno prima di implementare un particolare modello.

<table>
 <tbody>
  <tr>
   <th><strong>Bootstrap</strong></th>
   <th><strong>Vantaggi</strong></th>
   <th><strong>Svantaggi</strong></th>
  </tr>
  <tr>
   <th><strong>tramite AEM</strong><br /> </th>
   <td>
    <ul>
     <li>L'AEM gestisce le librerie di iniezione dove necessario</li>
     <li>Gestisci solo risorse su AEM<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>Possibilmente non familiare allo sviluppatore SPA<br /> </li>
    </ul> </td>
  </tr>
  <tr>
   <th><strong>tramite Adobe I/O Runtime<br /> </strong></th>
   <td>
    <ul>
     <li>Più familiare agli sviluppatori SPA<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>Le risorse Clientlib richieste dall’applicazione, come CSS e JavaScript, devono essere rese disponibili dallo sviluppatore AEM tramite <code><a href="/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet">allowProxy</a></code> proprietà<br /> </li>
     <li>Le risorse devono essere sincronizzate tra AEM e Adobe I/O Runtime<br /> </li>
     <li>Per abilitare la creazione dell'SPA, potrebbe essere necessario un server proxy per Adobe I/O Runtime</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Pianificazione per SSR {#planning-for-ssr}

È necessario eseguire il rendering lato server solo di una parte dell&#39;applicazione. L’esempio comune è il contenuto visualizzato sopra la piega al caricamento iniziale della pagina, di cui viene eseguito il rendering sul lato server. In questo modo si risparmia tempo distribuendo al client contenuti già sottoposti a rendering. Quando l’utente interagisce con l’SPA, il contenuto aggiuntivo viene riprodotto dal client.

Se stai valutando l’implementazione del rendering lato server per l’SPA, controlla quali parti dell’app sono necessarie.

## Sviluppo di un SPA utilizzando la SSR {#developing-an-spa-using-ssr}

Il rendering dei componenti SPA poteva essere eseguito dal client (nel browser) o dal lato server. Quando viene eseguito il rendering lato server, le proprietà del browser come le dimensioni della finestra e la posizione non sono presenti. Pertanto, i componenti dell’SPA devono essere isomorfi, senza presupporre dove saranno resi.

Per utilizzare SSR, distribuisci il codice in AEM e su Adobe I/O Runtime, responsabile del rendering lato server. La maggior parte del codice sarà lo stesso, tuttavia, le attività specifiche del server saranno diverse.

## SSR per l’SPA nell’AEM {#ssr-for-spas-in-aem}

La SSR per l’SPA nell’AEM richiede Adobe I/O Runtime, che è chiamato per il rendering del lato server del contenuto dell’app. All’interno dell’HTL dell’app, viene chiamata una risorsa su Adobe I/O Runtime per eseguire il rendering del contenuto.

Proprio come l’AEM supporta i framework SPA Angular e React pronti all’uso, è supportato anche il rendering lato server, ad Angular per le app React. Per ulteriori dettagli, consulta la documentazione NPM per entrambi i framework.

* React: [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)
* Angular: [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/angular-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/angular-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)

Per un esempio semplicistico, vedi [App We.Retail Journal](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal). Viene eseguito il rendering dell&#39;intero lato server applicazioni. Anche se non si tratta di un esempio reale, questo illustra ciò che è necessario per implementare la SSR.

>[!CAUTION]
>
>Il [App We.Retail Journal](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) è solo a scopo dimostrativo e quindi utilizza Node.js come semplice esempio al posto del Adobe I/O Runtime consigliato. Non utilizzare questo esempio per alcun lavoro di progetto.

>[!NOTE]
>
>Qualsiasi progetto AEM deve utilizzare l’[archetipo di progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it), che supporta progetti SPA utilizzando React o Angular e sfrutta l’SDK di SPA.

## Utilizzo di Node.js {#using-node-js}

Adobe I/O Runtime è la soluzione consigliata per l’implementazione della SSR per l’SPA nell’AEM.

Per le istanze AEM locali, è anche possibile implementare SSR utilizzando un’istanza Node.js personalizzata nello stesso modo descritto in precedenza. Sebbene supportato da Adobe, non è consigliato.

>[!NOTE]
>
>Node.js non è supportato per le istanze AEM ospitate da Adobe.

>[!NOTE]
>
>Se SSR deve essere implementato tramite Node.js, l’Adobe consiglia un’istanza di Node.js separata per ogni ambiente AEM (authoring, pubblicazione, stage e così via).

## Rendering contenuto remoto {#remote-content-renderer}

Il [Configurazione rendering contenuto remoto](#remote-content-renderer-configuration) che è necessario per utilizzare SSR con il tuo SPA in AEM si inserisce in un servizio di rendering più generalizzato che può essere esteso e personalizzato per soddisfare le tue esigenze.

### Servizio RemoteContentRendering {#remotecontentrenderingservice}

`RemoteContentRenderingService` è un servizio OSGi per recuperare il contenuto di cui è stato eseguito il rendering su un server remoto, ad esempio da Adobe I/O. Il contenuto inviato al server remoto si basa sul parametro di richiesta passato.

`RemoteContentRenderingService` può essere inserito tramite inversione delle dipendenze in un modello Sling personalizzato o in un servlet quando è necessaria un’ulteriore manipolazione del contenuto.

Questo servizio è utilizzato internamente da [RemoteContentRendererRequestHandlerServlet](#remotecontentrendererrequesthandlerservlet).

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

Il `RemoteContentRendererRequestHandlerServlet` può essere utilizzato per impostare a livello di programmazione la configurazione della richiesta. `DefaultRemoteContentRendererRequestHandlerImpl`, l’implementazione predefinita del gestore di richieste fornita, ti consente di creare più configurazioni OSGi per mappare una posizione nella struttura del contenuto su un endpoint remoto.

Per aggiungere un gestore di richieste personalizzato, implementa `RemoteContentRendererRequestHandler` di rete. Assicurarsi di impostare `Constants.SERVICE_RANKING` proprietà del componente a un numero intero maggiore di 100, che corrisponde alla classificazione `DefaultRemoteContentRendererRequestHandlerImpl`.

```
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### Configurare la configurazione OSGi del gestore predefinito {#configure-default-handler}

La configurazione del gestore predefinito deve essere configurata come descritto nella sezione [Configurazione rendering contenuto remoto](#remote-content-renderer-configuration).

### Utilizzo di Remote Content Renderer {#usage}

Per recuperare un servlet e restituire parte del contenuto che può essere inserito nella pagina:

1. Verificare che il server remoto sia accessibile.
1. Aggiungi uno dei seguenti snippet al modello HTL di un componente AEM.
1. Facoltativamente, crea o modifica le configurazioni OSGi.
1. Sfogliare il contenuto del sito

Di solito, il modello HTL di un componente pagina è il destinatario principale di tale funzione.

```
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### Requisiti {#requirements}

I servlet utilizzano Sling Model Exporter per serializzare i dati del componente. Per impostazione predefinita, entrambe le opzioni `com.adobe.cq.export.json.ContainerExporter` e `com.adobe.cq.export.json.ComponentExporter` sono supportati come adattatori del modello Sling. Se necessario, puoi aggiungere le classi a cui la richiesta deve essere adattata utilizzando `RemoteContentRendererServlet` e l&#39;implementazione `RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`. Le classi aggiuntive devono estendere `ComponentExporter`.
