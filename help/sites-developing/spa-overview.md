---
title: Panoramica dell’editor di SPA
seo-title: SPA Editor Overview
description: Questo articolo offre una panoramica completa dell’editor di SPA e del suo funzionamento, inclusi flussi di lavoro dettagliati relativi all’interazione dell’editor di SPA in AEM.
seo-description: This article gives a comprehensive overview of the SPA Editor and how it works included detailed workflows of interaction of the SPA Editor within AEM.
uuid: c283abab-f5bc-414a-bc81-bf3bdce38534
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 06b8c0be-4362-4bd1-ad57-ea5503616b17
docset: aem65
exl-id: 7b34be66-bb61-4697-8cc8-428f7c63a887
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '1659'
ht-degree: 91%

---

# Panoramica dell’editor di SPA{#spa-editor-overview}

Le applicazioni a pagina singola (SPA) possono offrire esperienze coinvolgenti agli utenti di siti web. Gli sviluppatori desiderano essere in grado di creare siti utilizzando framework SPA e gli autori desiderano modificare i contenuti all’interno di AEM per un sito creato utilizzando tali frameworks.

L’editor di SPA offre una soluzione completa per il supporto di SPA in AEM. Questa pagina offre una panoramica di come è strutturato il supporto SPA in AEM, come funziona l’editor di SPA e come il framework SPA mantiene la sincronizzazione con AEM.

>[!NOTE]
>
>L’editor SPA è la soluzione consigliata per i progetti che richiedono un rendering lato client basato sul framework SPA (ad esempio, React o Angular).

## Introduzione {#introduction}

I siti costruiti utilizzando framework SPA comuni come React e Angular caricano il contenuto tramite JSON dinamico e non forniscono la struttura di HTML necessaria affinché l’editor pagina di AEM possa inserire controlli di modifica.

Per abilitare la modifica delle SPA all’interno di AEM, è necessaria una mappatura tra l’output JSON della SPA e il modello di contenuto nell’archivio AEM per salvare le modifiche al contenuto.

Il supporto SPA in AEM introduce un livello JS sottile che interagisce con il codice JS SPA caricato nell’Editor pagina con cui è possibile inviare eventi e attivare la posizione dei controlli di modifica per consentire la modifica nel contesto. Questa funzione si basa sul concetto di endpoint API di Content Services, in quanto il contenuto dell’SPA deve essere caricato tramite Content Services.

Per ulteriori dettagli su SPA in AEM, consulta i seguenti documenti:

* [Blueprint SPA](/help/sites-developing/spa-blueprint.md) per i requisiti tecnici di una SPA
* [Guida introduttiva dell’SPA nell’AEM](/help/sites-developing/spa-getting-started-react.md) per una rapida presentazione di un semplice SPA

## Design {#design}

Il componente pagina per una SPA non fornisce gli elementi HTML dei suoi componenti figlio tramite il file JSP o HTL. Questa operazione è delegata al framework SPA. La rappresentazione dei componenti o del modello figlio viene recuperata come struttura dati JSON dal JCR. I componenti SPA vengono quindi aggiunti alla pagina in base a tale struttura. Questo comportamento differenzia la composizione iniziale del corpo del componente della pagina dalle controparti non SPA.

### Gestione dei modelli di pagina {#page-model-management}

La risoluzione e la gestione del modello di pagina sono delegate a una libreria `PageModel`. La SPA deve utilizzare la libreria Modello di pagina per essere inizializzata e creata dall’editor di SPA. La libreria Modello di pagina fornita indirettamente al componente Pagina AEM tramite l’npm `aem-react-editable-components`. Il Modello di pagina è un interprete tra AEM e SPA e quindi deve essere sempre presente. Quando si crea la pagina, deve essere aggiunta una libreria addizionale `cq.authoring.pagemodel.messaging` per abilitare la comunicazione con l’editor pagina.

Se il componente pagina SPA eredita dal componente core della pagina, sono disponibili due opzioni per rendere la categoria libreria client `cq.authoring.pagemodel.messaging` disponibile:

* Se il modello è modificabile, aggiungilo al criterio della pagina.
* Oppure aggiungi le categorie utilizzando il `customfooterlibs.html`.

Per ogni risorsa nel modello esportato, la SPA mappa un componente effettivo che esegue il
rendering. Viene quindi eseguito il rendering del modello, rappresentato come JSON, utilizzando le mappature dei componenti all’interno di un contenitore.
![screen_shot_2018-08-20at144152](assets/screen_shot_2018-08-20at144152.png)

>[!CAUTION]
>
>L’inclusione della categoria `cq.authoring.pagemodel.messaging` deve essere limitata al contesto dell’editor di SPA.

### Tipo di dati di comunicazione {#communication-data-type}

Quando viene aggiunta la categoria `cq.authoring.pagemodel.messaging` alla pagina, invia un messaggio all’editor pagina per stabilire il tipo di dati di comunicazione JSON. Quando il tipo di dati di comunicazione è impostato su JSON, le richieste di GET comunicheranno con i punti finali del modello Sling di un componente. Dopo che si verifica un aggiornamento nell’editor di pagine, la rappresentazione JSON del componente aggiornato viene inviata alla libreria Modello di pagina. La libreria Modello di pagina informa quindi la SPA degli aggiornamenti.

![screen_shot_2018-08-20at143628](assets/screen_shot_2018-08-20at143628.png)

## Flusso di lavoro {#workflow}

È possibile comprendere il flusso dell’interazione tra SPA e AEM pensando all’editor di SPA come mediatore tra i due.

* La comunicazione tra l’editor di pagine e la SPA viene effettuata utilizzando JSON invece di HTML.
* L’editor di pagina fornisce alla SPA la versione più recente del modello di pagina tramite l’API iframe e messagistica.
* Il gestore dei modelli di pagina notifica all’editor che è pronto per essere modificato e trasmette il modello di pagina come struttura JSON.
* L’editor non modifica né accede nemmeno alla struttura DOM della pagina in fase di creazione, ma fornisce l’ultimo modello di pagina.

![screen_shot_2018-08-20at144324](assets/screen_shot_2018-08-20at144324.png)

### Flusso di lavoro dell’editor di SPA di base {#basic-spa-editor-workflow}

Tenendo presenti gli elementi chiave dell’editor di SPA, il flusso di lavoro di alto livello per la modifica di una SPA in AEM viene visualizzato dall’autore come segue.

![untitled1](assets/untitled1.gif)

1. Viene caricato l’editor di SPA.
1. SPA viene caricato in un frame separato.
1. SPA richiede contenuti JSON ed esegue il rendering dei componenti lato client.
1. L’editor di SPA rileva i componenti renderizzati e genera sovrapposizioni.
1. L’autore fa clic su sovrapponi e visualizza la barra degli strumenti di modifica del componente.
1. L’Editor SPA mantiene le modifiche con una richiesta POST al server.
1. L’editor SPA richiede JSON aggiornato all’editor SPA, che viene inviato alla SPA con un evento DOM.
1. La SPA riesegue il rendering del componente interessato, aggiornandone il DOM.

>[!NOTE]
>
>Nota bene:
>
>* Alla SPA è sempre affidata la sua visualizzazione.
>* L’Editor SPA è isolato dalla SPA stessa.
>* Nella produzione (pubblicazione), l’editor SPA non viene mai caricato.
>

### Flusso di lavoro client-server di modifica delle pagine {#client-server-page-editing-workflow}

Questa è una panoramica più dettagliata dell’interazione client-server durante la modifica di una SPA.

![page_editor_spa_authoringmediator-2](assets/page_editor_spa_authoringmediator-2.png)

1. La SPA si inizializza e richiede il modello di pagina a Sling Model Exporter.
1. Sling Model Exporter richiede le risorse che compongono la pagina dall’archivio.
1. L’archivio restituisce le risorse.
1. Sling Model Exporter restituisce il modello della pagina.
1. La SPA crea un’istanza dei suoi componenti in base al modello di pagina.
1. **6a** Il contenuto informa l’editor che è pronto per l’authoring.

   **6b** L’editor pagina richiede le configurazioni di authoring dei componenti.

   **6c** L’editor pagina riceve le configurazioni dei componenti.
1. Quando l’autore modifica un componente, l’editor pagina pubblica una richiesta di modifica al POST servlet predefinito.
1. La risorsa viene aggiornata nell’archivio.
1. La risorsa aggiornata viene fornita al POST servlet.
1. Il POST servlet predefinito informa l’editor pagina che la risorsa è stata aggiornata.
1. L’editor pagina richiede il nuovo modello di pagina.
1. Le risorse che compongono la pagina sono richieste all’archivio.
1. Le risorse che compongono la pagina vengono fornite dall’archivio a Sling Model Exporter.
1. Il modello di pagina aggiornato viene restituito all’editor.
1. L’editor pagina aggiorna il riferimento al modello di pagina della SPA.
1. La SPA aggiorna i suoi componenti in base al riferimento al nuovo modello di pagina.
1. Le configurazioni dei componenti degli editor pagina vengono aggiornate.

   **17a** La SPA segnala all’editor pagina che il contenuto è pronto.

   **17b** L’editor pagina fornisce alla SPA le configurazioni dei componenti.

   **17c** La SPA fornisce le configurazioni dei componenti aggiornate.

### Flusso di lavoro di authoring {#authoring-workflow}

Questa è una panoramica più dettagliata incentrata sull’esperienza di authoring.

![spa_content_authoringmodel](assets/spa_content_authoringmodel.png)

1. La SPA recupera il modello di pagina.
1. **2a** Il modello di pagina fornisce all’editor i dati necessari per l’authoring.

   **2b** Quando viene notificata, il componente di orchestrazione aggiorna la struttura del contenuto della pagina.
1. L’orchestratore dei componenti esegue una query della mappatura tra un tipo di risorsa AEM e un componente SPA.
1. L’orchestratore dei componenti crea un’istanza dinamica del componente SPA in base al modello di pagina e alla mappatura dei componenti.
1. L’editor pagina aggiorna il modello di pagina.
1. **6a** Il modello di pagina fornisce dati di authoring aggiornati all’editor pagina.

   **6b** Il modello di pagina invia le modifiche all’orchestratore dei componenti.
1. L’orchestratore dei componenti recupera la mappatura dei componenti.
1. L’orchestratore dei componenti aggiorna il contenuto della pagina.
1. Quando la SPA completa l’aggiornamento del contenuto della pagina, l’editor pagina carica l’ambiente di authoring.

## Requisiti e limitazioni {#requirements-limitations}

Per consentire all’autore di utilizzare l’editor pagina per modificare il contenuto di una SPA, la tua applicazione SPA deve essere implementata per interagire con l’SDK dell’editor SPA di AEM. Consulta la sezione [Guida introduttiva dell’SPA nell’AEM](/help/sites-developing/spa-getting-started-react.md) documenti che è necessario conoscere almeno per avviare il tuo sistema.

### Framework supportati {#supported-frameworks}

L’SDK per l’editor di SPA supporta le seguenti versioni minime:

* React 16.x e versioni successive
* Angular 6.x e versioni successive

Le versioni precedenti di questi framework possono funzionare con l’SDK dell’editor di SPA di AEM, ma non sono supportate.

### Framework aggiuntivi {#additional-frameworks}

Puoi implementare altri framework SPA per lavorare con l’SDK dell’editor di SPA di AEM. Vedi il documento [Blueprint SPA](/help/sites-developing/spa-blueprint.md) per i requisiti che un framework deve soddisfare per creare un livello specifico del framework composto da moduli, componenti e servizi per lavorare con l’editor di SPA di AEM.

### Utilizzo di più selettori {#multiple-selectors}

È possibile definire e utilizzare selettori personalizzati aggiuntivi come parte di una SPA sviluppata per l’SDK di SPA di AEM. Tuttavia, questo supporto richiede che il `model` selettore sia il primo e l’estensione sia `.json`[ come richiesto dall’esportatore JSON.](json-exporter-components.md#multiple-selectors)

### Requisiti dell’editor di testo {#text-editor-requirements}

Se desideri utilizzare l’editor locale di un componente di testo creato in SPA è necessaria una configurazione aggiuntiva.

1. Imposta un attributo (può essere qualsiasi) sull’elemento wrapper del contenitore contenente il testo HTML. Nel caso del contenuto di esempio di WKND Journal, è un `<div>` e il selettore che è stato utilizzato è `data-rte-editelement`.
1. Imposta la configurazione `editElementQuery` sul componente di testo AEM corrispondente `cq:InplaceEditingConfig` che punta a tale selettore, ad esempio, `data-rte-editelement`. Questo consente all’editor di sapere quale elemento HTML si applica al testo di HTML.

Per un esempio di questa procedura, vedere [Contenuto di esempio del diario WKND.](https://github.com/adobe/aem-sample-we-retail-journal/pull/16/files)

Per ulteriori informazioni sulla proprietà `editElementQuery` e la configurazione dell’editor Rich Text, vedi [Configura l’editor Rich Text.](/help/sites-administering/rich-text-editor.md)

### Limitazioni {#limitations}

L’SDK dell’editor SPA dell’AEM è stato introdotto con il service pack 2 per AEM 6.4. È completamente supportato da Adobe, e continua a essere migliorato ed espanso. Le seguenti funzioni di AEM non sono ancora supportate dall’editor di SPA:

* Modalità di destinazione
* ContextHub
* Modifica delle immagini in linea
* Modifica le configurazioni (ad esempio ascoltatori)
* Annulla/Ripeti
* Differenze tra pagine e alterazione ora
* Funzionalità che eseguono la riscrittura sul lato server di HTML, come Link Checker, servizio di rewriter CDN, accorciamento degli URL, ecc.
* Modalità sviluppatore
* Lanci AEM
