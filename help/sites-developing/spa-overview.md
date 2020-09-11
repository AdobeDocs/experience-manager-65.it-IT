---
title: Panoramica di SPA Editor
seo-title: Panoramica di SPA Editor
description: Questo articolo fornisce una panoramica completa dell'editor SPA e del suo funzionamento, con flussi di lavoro dettagliati dell'interazione dell'editor SPA in AEM.
seo-description: Questo articolo fornisce una panoramica completa dell'editor SPA e del suo funzionamento, con flussi di lavoro dettagliati dell'interazione dell'editor SPA in AEM.
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


# Panoramica di SPA Editor{#spa-editor-overview}

Le applicazioni SPA (Single Page Applications) possono offrire esperienze coinvolgenti agli utenti di siti Web. Gli sviluppatori desiderano essere in grado di creare siti utilizzando i framework SPA e gli autori desiderano modificare i contenuti all&#39;interno AEM per un sito creato utilizzando tali framework.

L&#39;editor SPA offre una soluzione completa per supportare gli SPA in AEM. Questa pagina fornisce una panoramica di come il supporto SPA è strutturato in AEM, come funziona l&#39;Editor SPA, e come la struttura SPA e AEM mantenere sincronizzato.

>[!NOTE]
>
>SPA Editor è la soluzione consigliata per i progetti che richiedono il rendering lato client basato su SPA (ad esempio React o Angular).

## Introduzione {#introduction}

I siti creati con framework SPA comuni come React e Angular caricano i propri contenuti tramite JSON dinamico e non forniscono la struttura HTML necessaria per l&#39;Editor pagina AEM per inserire controlli di modifica.

Per abilitare la modifica degli SPA all&#39;interno di AEM, per salvare le modifiche al contenuto è necessaria una mappatura tra l&#39;output JSON dell&#39;SPA e il modello di contenuto nell&#39;archivio AEM.

Il supporto SPA in AEM introduce un sottile livello JS che interagisce con il codice SPA JS quando viene caricato nell&#39;Editor pagina con cui gli eventi possono essere inviati e la posizione dei controlli di modifica può essere attivata per consentire la modifica contestuale. Questa funzione si basa sul concetto di endpoint API di Content Services, in quanto il contenuto dell&#39;API deve essere caricato tramite Content Services.

Per ulteriori dettagli sulle ZPS in AEM, consulta i seguenti documenti:

* [SPA Blueprint](/help/sites-developing/spa-blueprint.md) per i requisiti tecnici di un&#39;SPA
* [Guida introduttiva alle SPA in AEM](/help/sites-developing/spa-getting-started-react.md) per un rapido tour di una semplice SPA

## Progettazione {#design}

Il componente di pagina per un’app SPA non fornisce gli elementi HTML dei componenti secondari tramite il file JSP o HTL. Questa operazione è delegata al framework SPA. La rappresentazione dei componenti secondari o del modello viene recuperata come struttura di dati JSON dal JCR. I componenti SPA vengono quindi aggiunti alla pagina in base a tale struttura. Questo comportamento distingue la composizione iniziale del corpo del componente della pagina da quelle non-SPA.

### Gestione dei modelli di pagina {#page-model-management}

La risoluzione e la gestione del modello di pagina sono delegate a una `PageModel` libreria specificata. Per poter essere inizializzata e creata dall’editor SPA, l’SPA deve utilizzare la libreria Modello pagina. Libreria Modello pagina fornita indirettamente al componente Pagina AEM tramite `aem-react-editable-components` npm. Il Modello pagina è un interprete tra AEM e l&#39;SPA e pertanto deve essere sempre presente. Quando la pagina viene creata, `cq.authoring.pagemodel.messaging` deve essere aggiunta una libreria aggiuntiva per abilitare la comunicazione con l’editor pagina.

Se il componente della pagina SPA eredita dal componente core della pagina, sono disponibili due opzioni per rendere disponibile la categoria della libreria `cq.authoring.pagemodel.messaging` client:

* Se il modello è modificabile, aggiungetelo al criterio pagina.
* Oppure aggiungete le categorie utilizzando l&#39;icona `customfooterlibs.html`.

Per ogni risorsa nel modello esportato, l’area di protezione dati mappa un componente effettivo che eseguirà il rendering. Il modello, rappresentato come JSON, viene quindi rappresentato utilizzando le mappature dei componenti all&#39;interno di un contenitore.
![screen_shot_2018-08-20at144152](assets/screen_shot_2018-08-20at144152.png)

>[!CAUTION]
>
>L&#39;inclusione della `cq.authoring.pagemodel.messaging` categoria dovrebbe essere limitata al contesto dell&#39;editor SPA.

### Tipo di dati di comunicazione {#communication-data-type}

Quando la `cq.authoring.pagemodel.messaging` categoria viene aggiunta alla pagina, invia un messaggio all’Editor pagina per stabilire il tipo di dati di comunicazione JSON. Quando il tipo di dati di comunicazione è impostato su JSON, le richieste di GET comunicano con i punti finali del modello Sling di un componente. Quando si verifica un aggiornamento nell’editor di pagina, la rappresentazione JSON del componente aggiornato viene inviata alla libreria Modello pagina. La libreria Modello pagina informa quindi l&#39;SPA degli aggiornamenti.

![screen_shot_2018-08-20at143628](assets/screen_shot_2018-08-20at143628.png)

## Flusso di lavoro {#workflow}

È possibile comprendere il flusso dell&#39;interazione tra SPA e AEM pensando all&#39;editor SPA come mediatore tra i due.

* La comunicazione tra l’editor pagina e l’SPA viene effettuata utilizzando JSON invece di HTML.
* L&#39;Editor pagina fornisce all&#39;SPA la versione più recente del modello di pagina tramite l&#39;API iframe e messaging.
* Il manager del modello di pagina notifica all’editor che è pronto per essere pubblicato e trasmette il modello di pagina come struttura JSON.
* L’editor non modifica o non accede neanche alla struttura DOM della pagina in fase di creazione, ma fornisce il modello di pagina più recente.

![screen_shot_2018-08-20at144324](assets/screen_shot_2018-08-20at144324.png)

### Flusso di lavoro di base per l&#39;editor SPA {#basic-spa-editor-workflow}

Tenendo presente gli elementi chiave dell&#39;editor SPA, il flusso di lavoro di alto livello per la modifica di un&#39;app AEM all&#39;interno dell&#39;app viene visualizzato all&#39;autore come segue.

![untitled1](assets/untitled1.gif)

1. Viene caricato SPA Editor.
1. SPA viene caricato in un frame separato.
1. SPA richiede il contenuto JSON ed esegue il rendering dei componenti lato client.
1. L’editor SPA rileva i componenti sottoposti a rendering e genera sovrapposizioni.
1. L’autore fa clic su sovrapposizione e visualizza la barra degli strumenti di modifica del componente.
1. SPA Editor persiste nelle modifiche con una richiesta di POST al server.
1. L&#39;editor SPA richiede l&#39;aggiornamento di JSON all&#39;Editor SPA, che viene inviato all&#39;SPA con un evento DOM.
1. SPA esegue di nuovo il rendering del componente interessato, aggiornando il suo DOM.

>[!NOTE]
>
>Ricorda:
>
>* L&#39;SPA è sempre responsabile del suo display.
>* L&#39;Editor SPA è isolato dall&#39;SPA stessa.
>* In produzione (pubblicazione), l&#39;editor SPA non viene mai caricato.

>



### Flusso di lavoro di modifica delle pagine client-server {#client-server-page-editing-workflow}

Questa è una panoramica più dettagliata dell&#39;interazione client-server durante la modifica di una SPA.

![page_editor_spa_authoringmediator-2](assets/page_editor_spa_authoringmediator-2.png)

1. SPA si inizializza e richiede il modello di pagina da Sling Model Exporter.
1. Sling Model Exporter richiede le risorse che compongono la pagina dalla directory archivio.
1. Il repository restituisce le risorse.
1. Sling Model Exporter restituisce il modello della pagina.
1. L’SPA crea un’istanza dei suoi componenti in base al modello di pagina.
1. **6a** Il contenuto informa l’editor che è pronto per l’authoring.

   **6b** L’editor pagina richiede le configurazioni di authoring dei componenti.

   **6c** L’editor pagina riceve le configurazioni dei componenti.
1. Quando l’autore modifica un componente, l’editor pagina invia una richiesta di modifica al servlet POST predefinito.
1. La risorsa viene aggiornata nella directory archivio.
1. La risorsa aggiornata viene fornita al servlet POST.
1. Il servlet POST predefinito informa l’editor di pagina che la risorsa è stata aggiornata.
1. L’editor pagina richiede il nuovo modello di pagina.
1. Le risorse che compongono la pagina vengono richieste dalla directory archivio.
1. Le risorse che compongono la pagina vengono fornite dalla directory archivio di Sling Model Exporter.
1. Il modello di pagina aggiornato viene restituito all’editor.
1. L’editor pagina aggiorna il riferimento del modello di pagina dell’area di protezione.
1. L’area SPA aggiorna i suoi componenti in base al nuovo riferimento al modello di pagina.
1. Le configurazioni dei componenti degli editor di pagina vengono aggiornate.

   **17a** L&#39;SPA segnala all&#39;editor di pagina che il contenuto è pronto.

   **17b** L’editor pagina fornisce all’SPA configurazioni di componenti.

   **17c** L&#39;SPA fornisce configurazioni di componenti aggiornate.

### Flusso di lavoro di authoring {#authoring-workflow}

Questa è una panoramica più dettagliata che si concentra sull’esperienza di authoring.

![spa_content_authoringmodel](assets/spa_content_authoringmodel.png)

1. L’SPA recupera il modello di pagina.
1. **2a** Il modello di pagina fornisce all’editor i dati necessari per l’authoring.

   **2b** Quando viene notificato, il orchestratore di componenti aggiorna la struttura del contenuto della pagina.
1. Il orchestratore di componenti esegue una query sulla mappatura tra un tipo di risorsa AEM e un componente SPA.
1. L’orchestrazione di componenti crea dinamicamente un’istanza del componente SPA in base al modello di pagina e alla mappatura del componente.
1. L’editor pagina aggiorna il modello di pagina.
1. **6a** Il modello di pagina fornisce dati di authoring aggiornati all’editor pagina.

   **6b** Il modello di pagina invia le modifiche all’orchestrazione dei componenti.
1. L’orchestrazione dei componenti recupera la mappatura dei componenti.
1. Il orchestratore di componenti aggiorna il contenuto della pagina.
1. Una volta completato l’aggiornamento del contenuto della pagina da parte dell’API, l’editor pagina carica l’ambiente di authoring.

## Requisiti e limitazioni {#requirements-limitations}

Per consentire all’autore di utilizzare l’editor pagina per modificare il contenuto di un’app SPA, l’applicazione SPA deve essere implementata per interagire con l’SDK dell’AEM SPA Editor. Consulta la [Guida introduttiva agli SPA in AEM](/help/sites-developing/spa-getting-started-react.md) documento per ottenere il minimo necessario per l&#39;esecuzione.

### Framework supportati {#supported-frameworks}

L’SDK per l’editor SPA supporta le seguenti versioni minime:

* 16.x e versioni successive
* Angular 6.x e superiore

Le versioni precedenti di questi framework potrebbero funzionare con l’SDK AEM SPA Editor, ma non sono supportate.

### Framework aggiuntivi {#additional-frameworks}

Possono essere implementati altri framework SPA per l&#39;utilizzo con l&#39;SDK AEM SPA Editor. Consultate il documento [SPA Blueprint](/help/sites-developing/spa-blueprint.md) per i requisiti che un framework deve soddisfare per creare un livello specifico del framework composto da moduli, componenti e servizi per l&#39;utilizzo con l&#39;editor SPA AEM.

### Utilizzo di più selettori {#multiple-selectors}

Altri selettori personalizzati possono essere definiti e utilizzati nell’ambito di un’app SPA sviluppata per AEM SPA SDK. Tuttavia, questo supporto richiede che il `model` selettore sia il primo e che l&#39;estensione sia `.json` come [richiesto da JSON Exporter.](json-exporter-components.md#multiple-selectors)

### Requisiti dell&#39;editor di testo {#text-editor-requirements}

Se desiderate utilizzare l’editor locale di un componente di testo creato in SPA, è necessaria una configurazione aggiuntiva.

1. Impostate un attributo (che può essere uno qualsiasi) sull’elemento wrapper contenitore contenente il testo HTML. Nel caso del contenuto di esempio WKND Journal, si tratta di un `<div>` elemento e il selettore utilizzato è `data-rte-editelement`.
1. Impostate la configurazione `editElementQuery` sul componente di testo AEM corrispondente `cq:InplaceEditingConfig` che punti a tale selettore, ad esempio `data-rte-editelement`. Questo consente all&#39;editor di sapere quale elemento HTML racchiude il testo HTML.

Per un esempio di come avviene, consultate il contenuto di esempio [WKND Journal.](https://github.com/adobe/aem-sample-we-retail-journal/pull/16/files)

Per ulteriori informazioni sulla `editElementQuery` proprietà e sulla configurazione dell’editor Rich Text, consultate [Configurare l’Editor Rich Text.](/help/sites-administering/rich-text-editor.md)

### Limitazioni  {#limitations}

L’SDK AEM SPA Editor è stato introdotto con AEM Service Pack 2 6.4. È completamente supportato da  Adobe, e come nuova funzione continua ad essere migliorato ed espanso. Le seguenti funzioni AEM non sono ancora supportate dall&#39;editor SPA:

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
