---
title: Rendering lato server e applicazioni a pagina singola
seo-title: Rendering lato server e applicazioni a pagina singola
description: 'null'
seo-description: 'null'
uuid: 27e26e3f-65d4-4069-b570-58b8b9e2a1ae
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 844e5c96-2a18-4869-b4c8-2fb9efe0332a
docset: aem65
translation-type: tm+mt
source-git-commit: 41e30a668c8c02f2c43e509ed708c4b9fa39a269
workflow-type: tm+mt
source-wordcount: '1691'
ht-degree: 1%

---


# Rendering lato server e applicazioni a pagina singola{#spa-and-server-side-rendering}

>[!NOTE]
>
>L’Editor SPA è la soluzione consigliata per i progetti che richiedono il rendering lato client basato su framework SPA (ad esempio React o Angular).

>[!NOTE]
>
>Per utilizzare le funzioni di rendering lato server SPA come descritto in questo documento, è necessario AEM 6.5.1.0 o versioni successive.

## Panoramica {#overview}

Le applicazioni a pagina singola (SPA) possono offrire all’utente un’esperienza ricca e dinamica che reagisce e si comporta in modo familiare, spesso come un’applicazione nativa. [Questo si ottiene facendo affidamento sul client per caricare i contenuti in anticipo e poi fare il pesante sollevamento della gestione dell&#39;](/help/sites-developing/spa-walkthrough.md#how-does-a-spa-work) interazione dell&#39;utente e quindi ridurre al minimo la quantità di comunicazione necessaria tra il client e il server, rendendo l&#39;app più reattiva.

Tuttavia, questo può causare tempi di caricamento iniziali più lunghi, soprattutto se l’applicazione a pagina singola è grande e ricca di contenuti. Per ottimizzare i tempi di caricamento, è possibile eseguire il rendering di alcuni contenuti lato server. L’utilizzo del rendering lato server (SSR) può accelerare il caricamento iniziale della pagina e quindi passare ulteriori rendering al client.

## Quando utilizzare SSR {#when-to-use-ssr}

SSR non è richiesto per tutti i progetti. Anche se AEM supporta completamente JS SSR per SPA, Adobe consiglia di non implementarlo sistematicamente per ogni progetto.

Quando si decide di implementare SSR, è innanzitutto necessario stimare la complessità, lo sforzo e i costi aggiuntivi che l’SSR rappresenta realisticamente per il progetto, inclusa la manutenzione a lungo termine. È opportuno scegliere un’architettura SSR solo quando il valore aggiunto supera chiaramente i costi stimati.

SSR di solito fornisce un certo valore quando c&#39;è un chiaro &quot;sì&quot; a una delle seguenti domande:

* **SEO:** SSR è ancora effettivamente necessario per il tuo sito per essere indicizzato correttamente dai motori di ricerca che portano traffico? Tieni presente che i principali crawler del motore di ricerca ora valutano JS.
* **Velocità di pagina:** l’SSR fornisce un miglioramento della velocità misurabile negli ambienti reali e aggiunge all’esperienza utente complessiva?

Solo quando almeno una di queste due domande riceve risposta con un chiaro &quot;sì&quot; per il progetto, Adobe consiglia di implementare SSR. Nelle sezioni seguenti viene descritto come eseguire questa operazione utilizzando Adobe I/O Runtime.

## Adobe I/O Runtime {#adobe-i-o-runtime}

Se [sei sicuro che il tuo progetto richiede l&#39;implementazione di SSR](/help/sites-developing/spa-ssr.md#when-to-use-ssr), la soluzione consigliata da Adobe è quella di utilizzare Adobe I/O Runtime.

Per ulteriori informazioni su Adobe I/O Runtime, consulta

* [https://www.adobe.io/apis/experienceplatform/runtime.html](https://www.adobe.io/apis/experienceplatform/runtime.html)  - per una panoramica del servizio
* [https://www.adobe.io/apis/experienceplatform/runtime/docs.html](https://www.adobe.io/apis/experienceplatform/runtime/docs.html)  - per la documentazione dettagliata sulla piattaforma

Nelle sezioni seguenti viene illustrato come Adobe I/O Runtime può essere utilizzato per implementare SSR per la tua SPA in due modelli diversi:

* [Flusso di comunicazione basato su AEM](/help/sites-developing/spa-ssr.md#aem-driven-communication-flow)
* [Flusso di comunicazione basato su runtime di Adobe I/O](/help/sites-developing/spa-ssr.md#adobe-i-o-runtime-driven-communication-flow)

>[!NOTE]
>
>Adobe consiglia un’istanza Adobe I/O Runtime separata per ogni ambiente AEM (authoring, pubblicazione, stage, ecc.).

## Configurazione del modulo di rendering remoto {#remote-renderer-configuration}

AEM deve sapere dove è possibile recuperare il contenuto di cui è stato eseguito il rendering in remoto. A prescindere da [quale modello scegli di implementare per SSR,](#adobe-i-o-runtime) dovrai specificare ad AEM come accedere a questo servizio di rendering remoto.

Questo viene fatto tramite il servizio **RemoteContentRenderer - Configuration Factory OSGi Service**. Cerca la stringa &quot;RemoteContentRenderer&quot; nella console di configurazione della console Web in `http://<host>:<port>/system/console/configMgr`.

![Configurazione del renderer](assets/rendererconfig.png)

Per la configurazione sono disponibili i campi seguenti:

* **Pattern di percorso del contenuto** : espressione regolare per far corrispondere una parte del contenuto, se necessario
* **URL**  endpoint remoto: URL dell&#39;endpoint responsabile della generazione del contenuto
   * Utilizzare il protocollo HTTPS protetto se non nella rete locale.
* **Intestazioni**  di richiesta aggiuntive - Intestazioni aggiuntive da aggiungere alla richiesta inviata all&#39;endpoint remoto
   * Pattern: `key=value`
* **Timeout richiesta**  - Timeout richiesta host remoto in millisecondi

>[!NOTE]
>
>Indipendentemente dalla scelta di implementare il [flusso di comunicazione basato su AEM](#aem-driven-communication-flow) o il [flusso basato su Adobe I/O Runtime,](#adobe-i-o-runtime-driven-communication-flow) è necessario definire una configurazione di rendering del contenuto remoto.
>
>Questa configurazione deve essere definita anche se scegli di [utilizzare un server Node.js personalizzato.](#using-node-js)

>[!NOTE]
>
>Questa configurazione sfrutta il [Remote Content Renderer,](#remote-content-renderer) che dispone di ulteriori opzioni di estensione e personalizzazione.

## Flusso di comunicazione basato su AEM {#aem-driven-communication-flow}

Quando utilizzi SSR, il [flusso di lavoro di interazione dei componenti](/help/sites-developing/spa-overview.md#workflow) delle applicazioni a pagina singola in AEM include una fase in cui il contenuto iniziale dell’app viene generato in Adobe I/O Runtime.

1. Il browser richiede il contenuto SSR da AEM.

1. AEM pubblica il modello in Adobe I/O Runtime.

1. Adobe I/O Runtime restituisce il contenuto generato.

1. AEM fornisce l’HTML restituito da Adobe I/O Runtime tramite il modello HTL del componente della pagina di back-end.

![server-side-rendering-cms-Drivenaemnode-adobeio](assets/server-side-rendering-cms-drivenaemnode-adobeio.png)

## Flusso di comunicazione basato su runtime di Adobe I/O {#adobe-i-o-runtime-driven-communication-flow}

La sezione precedente descrive l’implementazione standard e consigliata del rendering lato server per quanto riguarda le applicazioni a pagina singola in AEM, dove AEM esegue il bootstrap e il serving del contenuto.

In alternativa, è possibile implementare SSR in modo che Adobe I/O Runtime sia responsabile dell’avvio, invertendo in modo efficace il flusso di comunicazione.

Entrambi i modelli sono validi e supportati da AEM. Tuttavia, è opportuno considerare i vantaggi e gli svantaggi di ciascuno prima di implementare un particolare modello.

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
     <li>AEM gestisce l’inserimento delle librerie laddove necessario</li>
     <li>Le risorse devono essere mantenute solo su AEM<br /> </li>
    </ul> </td>
   <td>
    <ul>
     <li>Possibilmente sconosciuto allo sviluppatore SPA<br /> </li>
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
     <li>Le risorse clientlib richieste dall’applicazione, come CSS e JavaScript, dovranno essere rese disponibili dallo sviluppatore AEM tramite la proprietà <code><a href="/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet">allowProxy</a></code><br /> </li>
     <li>Le risorse devono essere sincronizzate tra AEM e Adobe I/O Runtime<br /> </li>
     <li>Per abilitare l’authoring dell’applicazione a pagina singola, potrebbe essere necessario un server proxy per Adobe I/O Runtime</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Pianificazione per SSR {#planning-for-ssr}

Generalmente solo una parte di un&#39;applicazione deve essere sottoposta a rendering sul lato server. L’esempio comune è il contenuto che verrà visualizzato sopra la piega al caricamento iniziale della pagina viene rappresentato sul lato server. Questo consente di risparmiare tempo distribuendo al client contenuti già sottoposti a rendering. Quando l’utente interagisce con l’applicazione a pagina singola, il contenuto aggiuntivo viene rappresentato dal client.

Quando consideri l’implementazione del rendering lato server per la tua applicazione a pagina singola, devi verificare quali parti dell’app saranno necessarie.

## Sviluppo di un’applicazione a pagina singola utilizzando SSR {#developing-an-spa-using-ssr}

I componenti SPA possono essere sottoposti a rendering dal lato client (nel browser) o server. Quando viene eseguito il rendering sul lato server, le proprietà del browser, ad esempio le dimensioni e la posizione della finestra, non sono presenti. Pertanto, i componenti SPA dovrebbero essere isomorfi, senza fare alcun presupposto su dove saranno resi.

Per sfruttare SSR, è necessario implementare il codice in AEM e in Adobe I/O Runtime, responsabile del rendering lato server. La maggior parte del codice sarà la stessa, ma le attività specifiche del server saranno diverse.

## SSR per applicazioni a pagina singola in AEM {#ssr-for-spas-in-aem}

SSR per le applicazioni a pagina singola in AEM richiede Adobe I/O Runtime, che è chiamato per il rendering del lato server dei contenuti dell’app. All’interno dell’HTL dell’app, viene chiamata una risorsa su Adobe I/O Runtime per eseguire il rendering del contenuto.

Proprio come AEM supporta i framework Angular e React SPA out-of-the-box, il rendering lato server è supportato anche per le app Angular e React. Per ulteriori informazioni, consulta la documentazione NPM per entrambi i framework.

* Reagire: [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)
* Angolare: [https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component](https://github.com/adobe/aem-sample-we-retail-journal/blob/master/react-app/DEVELOPMENT.md#enabling-the-server-side-rendering-using-the-aem-page-component)

Per un esempio semplicistico, fai riferimento all&#39; [App We.Retail Journal](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal). Esegue il rendering dell&#39;intero lato server dell&#39;applicazione. Anche se questo non è un esempio reale, illustra ciò che è necessario per implementare SSR.

>[!CAUTION]
>
>L’ [App We.Retail Journal](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) è solo a scopo dimostrativo e pertanto utilizza Node.js come esempio semplice invece di Adobe I/O Runtime consigliato. Questo esempio non deve essere utilizzato per alcun lavoro di progetto.

>[!NOTE]
>
>Qualsiasi progetto AEM deve sfruttare il [Archetipo di progetto AEM](https://docs.adobe.com/content/help/it/experience-manager-core-components/using/developing/archetype/overview.html), che supporta i progetti SPA utilizzando React o Angular e sfrutta l’SDK per applicazioni a pagina singola.

## Utilizzo di Node.js {#using-node-js}

Adobe I/O Runtime è la soluzione consigliata per l’implementazione di SSR per le applicazioni a pagina singola in AEM.

Per le istanze AEM on-premesis, è anche possibile implementare SSR utilizzando un&#39;istanza Node.js personalizzata nello stesso modo descritto sopra. Anche se supportato da Adobe, non è consigliato.

>[!NOTE]
>
>Node.js non è supportato per le istanze AEM ospitate da Adobe.

>[!NOTE]
>
>Se SSR deve essere implementato tramite Node.js, Adobe consiglia un&#39;istanza Node.js separata per ogni ambiente AEM (authoring, pubblicazione, stage, ecc.).

## Renderer di contenuti remoti {#remote-content-renderer}

La [Configurazione del modulo di rendering dei contenuti remoti](#remote-content-renderer-configuration) necessaria per utilizzare SSR con la tua applicazione a pagina singola in AEM viene utilizzata in un servizio di rendering più generalizzato che può essere esteso e personalizzato in base alle tue esigenze.

### RemoteContentRenderingService {#remotecontentrenderingservice}

`RemoteContentRenderingService` è un servizio OSGi per recuperare il contenuto di cui è stato eseguito il rendering su un server remoto, ad esempio da Adobe I/O. Il contenuto inviato al server remoto si basa sul parametro della richiesta trasmesso.

`RemoteContentRenderingService` può essere inserito dall’inversione della dipendenza in un modello Sling personalizzato o in un servlet quando è necessaria un’ulteriore manipolazione del contenuto.

Questo servizio viene utilizzato internamente da [RemoteContentRendererRequestHandlerServlet](#remotecontentrendererrequesthandlerservlet).

### RemoteContentRendererRequestHandlerServlet {#remotecontentrendererrequesthandlerservlet}

È possibile utilizzare `RemoteContentRendererRequestHandlerServlet` per impostare programmaticamente la configurazione della richiesta. `DefaultRemoteContentRendererRequestHandlerImpl`, l’implementazione predefinita del gestore delle richieste fornita, consente di creare più configurazioni OSGi per mappare una posizione nella struttura del contenuto a un endpoint remoto.

Per aggiungere un gestore di richieste personalizzato, implementa l’interfaccia `RemoteContentRendererRequestHandler` . Assicurati di impostare la proprietà del componente `Constants.SERVICE_RANKING` su un numero intero superiore a 100, che è la classificazione del `DefaultRemoteContentRendererRequestHandlerImpl`.

```
@Component(immediate = true,
        service = RemoteContentRendererRequestHandler.class,
        property={
            Constants.SERVICE_RANKING +":Integer=1000"
        })
public class CustomRemoteContentRendererRequestHandlerImpl implements RemoteContentRendererRequestHandler {}
```

### Configura la configurazione OSGi del gestore predefinito {#configure-default-handler}

La configurazione del gestore predefinito deve essere configurata come descritto nella sezione [Configurazione del modulo di rendering del contenuto remoto](#remote-content-renderer-configuration).

### Utilizzo del modulo di rendering dei contenuti remoti {#usage}

Per ottenere un servlet di recupero e restituire alcuni contenuti che possono essere inseriti nella pagina:

1. Verificare che il server remoto sia accessibile.
1. Aggiungi uno dei seguenti snippet al modello HTL di un componente AEM.
1. Facoltativamente, crea o modifica le configurazioni OSGi.
1. Sfoglia il contenuto del sito

Di solito, il modello HTL di un componente pagina è il destinatario principale di tale funzione.

```
<sly data-sly-resource="${resource @ resourceType='cq/remote/content/renderer/request/handler'}" />
```

### Requisiti {#requirements}

I servlet sfruttano l’esportatore di modelli Sling per serializzare i dati dei componenti. Per impostazione predefinita, le schede `com.adobe.cq.export.json.ContainerExporter` e `com.adobe.cq.export.json.ComponentExporter` sono supportate come schede di rete Sling Model. Se necessario, puoi aggiungere le classi alle quali la richiesta deve essere adattata utilizzando `RemoteContentRendererServlet` e implementando `RemoteContentRendererRequestHandler#getSlingModelAdapterClasses`. Le classi aggiuntive devono estendere il campo `ComponentExporter`.
