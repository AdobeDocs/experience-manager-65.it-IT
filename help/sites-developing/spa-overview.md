---
title: Panoramica dell’editor SPA
seo-title: Panoramica dell’editor SPA
description: Questo articolo offre una panoramica completa dell’Editor SPA e del suo funzionamento, con flussi di lavoro dettagliati legati all’interazione dell’Editor SPA in AEM.
seo-description: Questo articolo offre una panoramica completa dell’Editor SPA e del suo funzionamento, con flussi di lavoro dettagliati legati all’interazione dell’Editor SPA in AEM.
uuid: c283abab-f5bc-414a-bc81-bf3bdce38534
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 06b8c0be-4362-4bd1-ad57-ea5503616b17
docset: aem65
translation-type: tm+mt
source-git-commit: 4c9a0bd73e8d87d3869c6a133f5d1049f8430cd1
workflow-type: tm+mt
source-wordcount: '1691'
ht-degree: 0%

---


# Panoramica dell&#39;editor SPA{#spa-editor-overview}

Le applicazioni a pagina singola (SPA) possono offrire esperienze coinvolgenti agli utenti di siti Web. Gli sviluppatori desiderano essere in grado di creare siti utilizzando SPA framework e gli autori desiderano modificare i contenuti all&#39;interno di AEM per un sito creato utilizzando tali framework.

SPA Editor offre una soluzione completa per SPA di supporto in AEM. In questa pagina viene fornita una panoramica di come SPA supporto è strutturato in AEM, come funziona l’Editor SPA, e di come il framework SPA e AEM mantengono la sincronizzazione.

>[!NOTE]
>
>SPA Editor è la soluzione consigliata per i progetti che richiedono SPA rendering lato client basato su framework (ad es. React o Angular).

## Introduzione {#introduction}

I siti creati con framework SPA comuni come React e Angular caricano i propri contenuti tramite JSON dinamico e non forniscono la struttura HTML necessaria affinché l’Editor pagina AEM possa inserire controlli di modifica.

Per abilitare la modifica di SPA all&#39;interno di AEM, è necessario un mapping tra l&#39;output JSON del SPA e il modello di contenuto nel repository AEM per salvare le modifiche al contenuto.

SPA supporto in AEM introduce un sottile livello JS che interagisce con il codice JS SPA quando viene caricato nell’Editor pagina con cui gli eventi possono essere inviati e la posizione dei controlli di modifica può essere attivata per consentire la modifica contestuale. Questa funzione si basa sul concetto di endpoint API di Content Services, in quanto il contenuto del SPA deve essere caricato tramite Content Services.

Per ulteriori dettagli sulle SPA in AEM, consulta i documenti seguenti:

* [SPA ](/help/sites-developing/spa-blueprint.md) Blueprintfor per i requisiti tecnici di un SPA
* [Guida introduttiva alle SPA in ](/help/sites-developing/spa-getting-started-react.md) AEM per una breve presentazione di un semplice SPA

## Progettazione {#design}

Il componente della pagina per un SPA non fornisce gli elementi HTML dei suoi componenti secondari tramite il file JSP o HTL. Questa operazione è delegata al framework SPA. La rappresentazione dei componenti secondari o del modello viene recuperata come struttura di dati JSON dal JCR. I componenti SPA vengono quindi aggiunti alla pagina in base a tale struttura. Questo comportamento distingue la composizione iniziale del corpo del componente della pagina da quella SPA.

### Gestione dei modelli di pagina {#page-model-management}

La risoluzione e la gestione del modello di pagina sono delegate a una `PageModel` libreria fornita. Per poter essere inizializzata e creata dall&#39;editor SPA, il SPA deve utilizzare la libreria Modello pagina. La libreria Modello pagina viene fornita indirettamente al componente Pagina AEM tramite il file npm `aem-react-editable-components`. Il Modello pagina è un interprete tra AEM e il SPA e pertanto deve essere sempre presente. Quando la pagina viene creata, è necessario aggiungere una libreria aggiuntiva `cq.authoring.pagemodel.messaging` per abilitare la comunicazione con l&#39;editor pagina.

Se il componente SPA pagina eredita dal componente core della pagina, sono disponibili due opzioni per rendere disponibile la categoria della libreria client `cq.authoring.pagemodel.messaging`:

* Se il modello è modificabile, aggiungetelo al criterio pagina.
* Oppure aggiungete le categorie utilizzando il simbolo `customfooterlibs.html`.

Per ogni risorsa nel modello esportato, il SPA mapperà un componente effettivo che eseguirà la
rendering. Il modello, rappresentato come JSON, viene quindi rappresentato utilizzando le mappature dei componenti all&#39;interno di un contenitore.
![screen_shot_2018-08-20at144152](assets/screen_shot_2018-08-20at144152.png)

>[!CAUTION]
>
>L&#39;inclusione della categoria `cq.authoring.pagemodel.messaging` dovrebbe essere limitata al contesto dell&#39;editor SPA.

### Tipo di dati di comunicazione {#communication-data-type}

Quando la categoria `cq.authoring.pagemodel.messaging` viene aggiunta alla pagina, invia un messaggio all&#39;Editor pagina per stabilire il tipo di dati di comunicazione JSON. Quando il tipo di dati di comunicazione è impostato su JSON, le richieste di GET comunicano con i punti finali del modello Sling di un componente. Quando si verifica un aggiornamento nell’editor di pagina, la rappresentazione JSON del componente aggiornato viene inviata alla libreria Modello pagina. La libreria Modello pagina informa quindi il SPA degli aggiornamenti.

![screen_shot_2018-08-20at143628](assets/screen_shot_2018-08-20at143628.png)

## Flusso di lavoro {#workflow}

Potete comprendere il flusso dell&#39;interazione tra SPA e AEM pensando all&#39;Editor SPA come mediatore tra i due.

* La comunicazione tra l’editor pagina e il SPA viene effettuata utilizzando JSON invece di HTML.
* L&#39;Editor pagina fornisce la versione più recente del modello di pagina al SPA tramite l&#39;API iframe e messaging.
* Il manager del modello di pagina notifica all’editor che è pronto per essere pubblicato e trasmette il modello di pagina come struttura JSON.
* L’editor non modifica o non accede neanche alla struttura DOM della pagina in fase di creazione, ma fornisce il modello di pagina più recente.

![screen_shot_2018-08-20at144324](assets/screen_shot_2018-08-20at144324.png)

### Flusso di lavoro di base dell&#39;editor SPA {#basic-spa-editor-workflow}

Tenendo presenti gli elementi chiave dell’Editor SPA, il flusso di lavoro di alto livello per la modifica di un SPA in AEM viene visualizzato all’autore come segue.

![senza titolo1](assets/untitled1.gif)

1. Viene caricato SPA Editor.
1. SPA viene caricato in un frame separato.
1. SPA richiede il contenuto JSON ed esegue il rendering dei componenti lato client.
1. SPA Editor rileva i componenti sottoposti a rendering e genera sovrapposizioni.
1. L’autore fa clic su sovrapposizione e visualizza la barra degli strumenti di modifica del componente.
1. SPA Editor persiste nelle modifiche con una richiesta di POST al server.
1. SPA Editor richiede un JSON aggiornato all’editor SPA, che viene inviato al SPA con un evento DOM.
1. SPA il rendering del componente interessato, aggiornandone il DOM.

>[!NOTE]
>
>Ricorda:
>
>* Il SPA è sempre responsabile del display.
>* L’editor SPA è isolato dal SPA stesso.
>* In produzione (pubblicazione), l&#39;editor SPA non viene mai caricato.

>



### Flusso di lavoro di modifica delle pagine client-server {#client-server-page-editing-workflow}

Questa è una panoramica più dettagliata dell&#39;interazione client-server durante la modifica di un SPA.

![page_editor_spa_authoringmediator-2](assets/page_editor_spa_authoringmediator-2.png)

1. Il SPA inizializza se stesso e richiede il modello di pagina da Sling Model Exporter.
1. Sling Model Exporter richiede le risorse che compongono la pagina dalla directory archivio.
1. Il repository restituisce le risorse.
1. Sling Model Exporter restituisce il modello della pagina.
1. Il SPA crea un&#39;istanza dei componenti in base al modello di pagina.
1. **6** aIl contenuto informa l’editor che è pronto per l’authoring.

   **6** bL’editor di pagina richiede le configurazioni di authoring dei componenti.

   **6** cL’editor pagina riceve le configurazioni dei componenti.
1. Quando l’autore modifica un componente, l’editor pagina invia una richiesta di modifica al servlet POST predefinito.
1. La risorsa viene aggiornata nella directory archivio.
1. La risorsa aggiornata viene fornita al servlet POST.
1. Il servlet POST predefinito informa l’editor di pagina che la risorsa è stata aggiornata.
1. L’editor pagina richiede il nuovo modello di pagina.
1. Le risorse che compongono la pagina vengono richieste dalla directory archivio.
1. Le risorse che compongono la pagina vengono fornite dalla directory archivio di Sling Model Exporter.
1. Il modello di pagina aggiornato viene restituito all’editor.
1. L’editor pagina aggiorna il riferimento del modello di pagina del SPA.
1. Il SPA aggiorna i propri componenti in base al nuovo riferimento al modello di pagina.
1. Le configurazioni dei componenti degli editor di pagina vengono aggiornate.

   **17** aIl SPA segnala all’editor di pagina che il contenuto è pronto.

   **17** bL’editor pagina fornisce al SPA le configurazioni dei componenti.

   **17** cIl SPA fornisce configurazioni aggiornate dei componenti.

### Flusso di lavoro di authoring {#authoring-workflow}

Questa è una panoramica più dettagliata che si concentra sull’esperienza di authoring.

![spa_content_authoringmodel](assets/spa_content_authoringmodel.png)

1. Il SPA recupera il modello di pagina.
1. **2** aIl modello di pagina fornisce all’editor i dati necessari per l’authoring.

   **2** bQuando viene notificato, l’orchestratore di componenti aggiorna la struttura del contenuto della pagina.
1. L&#39;orchestratore di componenti esegue una query sulla mappatura tra un tipo di risorsa AEM e un componente SPA.
1. L’orchestrazione di componenti crea dinamicamente un’istanza del componente SPA in base al modello di pagina e alla mappatura del componente.
1. L’editor pagina aggiorna il modello di pagina.
1. **6** aIl modello di pagina fornisce dati di authoring aggiornati all’editor pagina.

   **6** bIl modello di pagina invia le modifiche all’orchestrazione dei componenti.
1. L’orchestrazione dei componenti recupera la mappatura dei componenti.
1. Il orchestratore di componenti aggiorna il contenuto della pagina.
1. Al termine dell’SPA, l’editor pagina carica l’ambiente di authoring.

## Requisiti e limitazioni {#requirements-limitations}

Per consentire all’autore di utilizzare l’editor pagina per modificare il contenuto di un SPA, l’applicazione SPA deve essere implementata per interagire con l’SDK AEM SPA Editor. Per informazioni sul funzionamento, vedere la [Guida introduttiva alle SPA in AEM](/help/sites-developing/spa-getting-started-react.md).

### Framework supportati {#supported-frameworks}

L’SDK di SPA Editor supporta le seguenti versioni minime:

* 16.x e versioni successive
* Angular 6.x e superiore

Le versioni precedenti di questi framework potrebbero funzionare con l’SDK dell’editor SPA AEM, ma non sono supportate.

### Framework aggiuntivi {#additional-frameworks}

Possono essere implementati altri framework SPA per lavorare con l’SDK AEM SPA Editor. Per i requisiti che un framework deve soddisfare per creare un livello specifico del framework composto da moduli, componenti e servizi da utilizzare con l&#39;editor SPA AEM, consultare il documento [SPA Blueprint](/help/sites-developing/spa-blueprint.md).

### Utilizzo di più selettori {#multiple-selectors}

Altri selettori personalizzati possono essere definiti e utilizzati come parte di un SPA sviluppato per l’SDK SPA AEM. Tuttavia, questo supporto richiede che il selettore `model` sia il primo selettore e che l&#39;estensione sia `.json` come [richiesto da JSON Exporter.](json-exporter-components.md#multiple-selectors)

### Requisiti dell&#39;editor di testo {#text-editor-requirements}

Per utilizzare l’editor locale di un componente di testo creato in SPA è necessaria una configurazione aggiuntiva.

1. Impostate un attributo (che può essere uno qualsiasi) sull’elemento wrapper contenitore contenente il testo HTML. Nel caso del contenuto di esempio WKND Journal, si tratta di un elemento `<div>` e il selettore utilizzato è `data-rte-editelement`.
1. Impostate la configurazione `editElementQuery` sull&#39;elemento `cq:InplaceEditingConfig` del componente di testo AEM corrispondente che punta a tale selettore, ad esempio `data-rte-editelement`. Questo consente all&#39;editor di sapere quale elemento HTML racchiude il testo HTML.

Per un esempio di come viene fatto, vedere il contenuto di esempio di [WKND Journal.](https://github.com/adobe/aem-sample-we-retail-journal/pull/16/files)

Per ulteriori informazioni sulla proprietà `editElementQuery` e sulla configurazione dell&#39;editor Rich Text, vedere [Configurare l&#39;Editor Rich Text.](/help/sites-administering/rich-text-editor.md)

### Limitazioni  {#limitations}

L’SDK dell’editor SPA AEM è stato introdotto con AEM 6.4 service pack 2. È completamente supportato da  Adobe, e come nuova funzione continua ad essere migliorato ed espanso. Le seguenti funzioni AEM non sono ancora supportate dall’editor SPA:

* Modalità di destinazione
* ContextHub
* Modifica di immagini in linea
* Modificare le configurazioni (ad esempio listener)
* Sistema di stili
* Annulla/Ripristina
* Differf pagina e Alterazione ora
* Funzioni che eseguono la riscrittura HTML lato server, come Controllo collegamenti, servizio di riscrittura CDN, riduzione URL ecc.
* Modalità Sviluppatore
* AEM lanci
