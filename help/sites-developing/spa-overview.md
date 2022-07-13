---
title: Panoramica dell’editor di SPA
seo-title: SPA Editor Overview
description: Questo articolo offre una panoramica completa dell’Editor di SPA e del suo funzionamento includeva flussi di lavoro dettagliati relativi all’interazione dell’Editor di SPA in AEM.
seo-description: This article gives a comprehensive overview of the SPA Editor and how it works included detailed workflows of interaction of the SPA Editor within AEM.
uuid: c283abab-f5bc-414a-bc81-bf3bdce38534
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 06b8c0be-4362-4bd1-ad57-ea5503616b17
docset: aem65
exl-id: 7b34be66-bb61-4697-8cc8-428f7c63a887
source-git-commit: a547b2e24205c63284a0e77f2e7f5678ae24968b
workflow-type: tm+mt
source-wordcount: '1657'
ht-degree: 1%

---

# Panoramica dell’editor di SPA{#spa-editor-overview}

Le applicazioni a pagina singola (SPA) possono offrire esperienze coinvolgenti agli utenti di siti web. Gli sviluppatori desiderano poter creare siti utilizzando framework SPA e gli autori desiderano modificare facilmente i contenuti all’interno di AEM per un sito creato utilizzando tali framework.

SPA Editor offre una soluzione completa per il supporto dei SPA in AEM. Questa pagina offre una panoramica di come SPA supporto è strutturato in AEM, come funziona l’Editor SPA e come il framework SPA e AEM mantenere la sincronizzazione.

>[!NOTE]
>
>L’editor di SPA è la soluzione consigliata per i progetti che richiedono SPA rendering lato client basato su framework (ad esempio, React o Angular).

## Introduzione {#introduction}

I siti costruiti utilizzando framework SPA comuni come React e Angular caricano il contenuto tramite JSON dinamico e non forniscono la struttura di HTML necessaria affinché l’Editor pagina AEM possa inserire controlli di modifica.

Per abilitare la modifica di SPA all’interno di AEM, è necessaria una mappatura tra l’output JSON dell’SPA e il modello di contenuto nell’archivio AEM per salvare le modifiche al contenuto.

SPA supporto in AEM introduce un livello JS sottile che interagisce con il codice JS SPA caricato nell’Editor pagina con cui è possibile inviare eventi e attivare la posizione dei controlli di modifica per consentire la modifica nel contesto. Questa funzione si basa sul concetto di endpoint API di Content Services, in quanto il contenuto del SPA deve essere caricato tramite Content Services.

Per ulteriori dettagli sulle SPA in AEM, consulta i seguenti documenti:

* [Blueprint SPA](/help/sites-developing/spa-blueprint.md) per i requisiti tecnici di un SPA
* [Guida introduttiva a SPA in AEM](/help/sites-developing/spa-getting-started-react.md) per un rapido tour di un semplice SPA

## Design {#design}

Il componente page per un SPA non fornisce gli elementi HTML dei suoi componenti figlio tramite il file JSP o HTL. Questa operazione è delegata al framework SPA. La rappresentazione dei componenti o del modello figlio viene recuperata come struttura dati JSON dal JCR. I componenti SPA vengono quindi aggiunti alla pagina in base a tale struttura. Questo comportamento differenzia la composizione iniziale del corpo del componente della pagina dalle controparti non SPA.

### Gestione dei modelli di pagina {#page-model-management}

La risoluzione e la gestione del modello di pagina sono delegate a un `PageModel` libreria. Il SPA deve utilizzare la libreria Modello pagina per essere inizializzato e creato dall’editor SPA. La libreria Modello di pagina fornita indirettamente al componente Pagina AEM tramite il `aem-react-editable-components` npm. Il Modello pagina è un interprete tra AEM e il SPA e quindi deve essere sempre presente. Quando la pagina viene creata, viene creata una libreria aggiuntiva `cq.authoring.pagemodel.messaging` deve essere aggiunto per abilitare la comunicazione con l’editor di pagine.

Se il componente pagina SPA eredita dal componente core della pagina, sono disponibili due opzioni per rendere il `cq.authoring.pagemodel.messaging` categoria libreria client disponibile:

* Se il modello è modificabile, aggiungilo al criterio della pagina.
* Oppure aggiungi le categorie utilizzando il `customfooterlibs.html`.

Per ogni risorsa nel modello esportato, il SPA mappa un componente effettivo che esegue il rendering. Viene quindi eseguito il rendering del modello, rappresentato come JSON, utilizzando le mappature dei componenti all’interno di un contenitore.
![screen_shot_2018-08-20at144152](assets/screen_shot_2018-08-20at144152.png)

>[!CAUTION]
>
>L&#39;inclusione della `cq.authoring.pagemodel.messaging` La categoria deve essere limitata al contesto dell’editor SPA.

### Tipo di dati di comunicazione {#communication-data-type}

Quando il `cq.authoring.pagemodel.messaging` viene aggiunta una categoria alla pagina e invia un messaggio all’Editor pagina per stabilire il tipo di dati di comunicazione JSON. Quando il tipo di dati di comunicazione è impostato su JSON, le richieste di GET comunicheranno con i punti finali del modello Sling di un componente. Dopo che si verifica un aggiornamento nell’editor di pagine, la rappresentazione JSON del componente aggiornato viene inviata alla libreria Modello pagina. La libreria Modello pagina informa quindi il SPA degli aggiornamenti.

![screen_shot_2018-08-20at143628](assets/screen_shot_2018-08-20at143628.png)

## Flusso di lavoro {#workflow}

È possibile comprendere il flusso dell’interazione tra SPA e AEM pensando all’Editor SPA come mediatore tra i due.

* La comunicazione tra l’editor di pagine e il SPA viene effettuata utilizzando JSON invece di HTML.
* L’editor pagina fornisce all’SPA la versione più recente del modello di pagina tramite l’API iframe e messaging.
* Il gestore dei modelli di pagina notifica all’editor che è pronto per essere modificato e trasmette il modello di pagina come struttura JSON.
* L’editor non modifica né accede nemmeno alla struttura DOM della pagina in fase di creazione, ma fornisce l’ultimo modello di pagina.

![screen_shot_2018-08-20at144324](assets/screen_shot_2018-08-20at144324.png)

### Flusso di lavoro dell&#39;editor di SPA di base {#basic-spa-editor-workflow}

Tenendo presenti gli elementi chiave dell’Editor SPA, il flusso di lavoro di alto livello per la modifica di un SPA in AEM viene visualizzato all’autore come segue.

![senza titolo1](assets/untitled1.gif)

1. SPA viene caricato l’editor.
1. SPA viene caricato in un frame separato.
1. SPA richiede contenuti JSON ed esegue il rendering dei componenti lato client.
1. SPA Editor rileva i componenti renderizzati e genera sovrapposizioni.
1. L’autore fa clic su sovrapponi e visualizza la barra degli strumenti di modifica del componente.
1. SPA Editor persiste nelle modifiche con una richiesta di POST al server.
1. Le richieste dell’editor SPA hanno aggiornato JSON all’editor SPA, che viene inviato al SPA con un evento DOM.
1. SPA riesegue il rendering del componente interessato, aggiornandone il DOM.

>[!NOTE]
>
>Nota bene:
>
>* Il SPA è sempre responsabile del display.
>* L’Editor SPA è isolato dal SPA stesso.
>* In produzione (pubblicazione), l’editor SPA non viene mai caricato.
>


### Flusso di lavoro di modifica delle pagine del server client {#client-server-page-editing-workflow}

Questa è una panoramica più dettagliata dell’interazione client-server durante la modifica di un SPA.

![page_editor_spa_authoringmediator-2](assets/page_editor_spa_authoringmediator-2.png)

1. L’SPA si inizializza e richiede il modello di pagina dall’esportatore di modelli Sling.
1. Sling Model Exporter richiede le risorse che compongono la pagina dall&#39;archivio.
1. L’archivio restituisce le risorse.
1. Sling Model Exporter restituisce il modello della pagina.
1. L’SPA crea un’istanza dei suoi componenti in base al modello di pagina.
1. **6 bis** Il contenuto informa l’editor che è pronto per l’authoring.

   **6 ter** L’editor pagina richiede le configurazioni di authoring dei componenti.

   **6c** L’editor pagina riceve le configurazioni del componente.
1. Quando l’autore modifica un componente, l’editor pagina pubblica una richiesta di modifica al servlet POST predefinito.
1. La risorsa viene aggiornata nella directory archivio.
1. La risorsa aggiornata viene fornita al servlet POST.
1. Il servlet POST predefinito informa l’editor di pagine che la risorsa è stata aggiornata.
1. L’editor pagina richiede il nuovo modello di pagina.
1. Le risorse che compongono la pagina sono richieste dall’archivio.
1. Le risorse che compongono la pagina vengono fornite dall’archivio all’Esportatore del modello Sling.
1. Il modello di pagina aggiornato viene restituito all’editor.
1. L’editor pagina aggiorna il riferimento del modello di pagina del SPA.
1. Il SPA aggiorna i suoi componenti in base al nuovo riferimento al modello di pagina.
1. Le configurazioni dei componenti degli editor di pagina vengono aggiornate.

   **17 bis** Il SPA segnala all’editor di pagine che il contenuto è pronto.

   **17 ter** L’editor pagina fornisce l’SPA con le configurazioni dei componenti.

   **17 quater** Il SPA fornisce configurazioni di componenti aggiornate.

### Flusso di lavoro di authoring {#authoring-workflow}

Questa è una panoramica più dettagliata incentrata sull’esperienza di authoring.

![spa_content_authoringmodel](assets/spa_content_authoringmodel.png)

1. Il SPA recupera il modello di pagina.
1. **2 bis** Il modello di pagina fornisce all’editor i dati necessari per l’authoring.

   **2 ter** Quando viene notificata, l’orchestrazione dei componenti aggiorna la struttura del contenuto della pagina.
1. L’orchestrazione dei componenti esegue una query sulla mappatura tra un tipo di risorsa AEM e un componente SPA.
1. L’orchestrazione dei componenti crea un’istanza dinamica del componente SPA in base al modello di pagina e alla mappatura dei componenti.
1. L’editor pagina aggiorna il modello di pagina.
1. **6 bis** Il modello pagina fornisce dati di authoring aggiornati all’editor pagina.

   **6 ter** Il modello di pagina invia le modifiche all’orchestrazione dei componenti.
1. L’orchestrazione dei componenti recupera la mappatura dei componenti.
1. L’orchestrazione dei componenti aggiorna il contenuto della pagina.
1. Quando il SPA completa l’aggiornamento del contenuto della pagina, l’editor di pagine carica l’ambiente di authoring.

## Requisiti e limitazioni {#requirements-limitations}

Per consentire all’autore di utilizzare l’editor di pagine per modificare il contenuto di un SPA, l’applicazione SPA deve essere implementata per interagire con l’SDK dell’editor di SPA di AEM. Vedi la [Guida introduttiva a SPA in AEM](/help/sites-developing/spa-getting-started-react.md) documentazione per il minimo che devi sapere per far funzionare il tuo.

### Framework supportati {#supported-frameworks}

L’SDK per l’editor di SPA supporta le seguenti versioni minime:

* React 16.x e versioni successive
* Angular 6.x e versioni successive

Le versioni precedenti di questi framework possono funzionare con l’SDK dell’editor di SPA AEM, ma non sono supportate.

### Framework aggiuntivi {#additional-frameworks}

Puoi implementare altri framework SPA per lavorare con l’SDK dell’editor di SPA AEM. Vedi la [Blueprint SPA](/help/sites-developing/spa-blueprint.md) documento dei requisiti che un framework deve soddisfare per creare un livello specifico del framework composto da moduli, componenti e servizi per lavorare con l&#39;editor SPA AEM.

### Utilizzo di più selettori {#multiple-selectors}

È possibile definire e utilizzare selettori personalizzati aggiuntivi come parte di un SPA sviluppato per l’SDK di AEM SPA. Tuttavia, questo supporto richiede che `model` Il selettore deve essere il primo selettore e l’estensione deve essere `.json` come [richiesto da JSON Exporter.](json-exporter-components.md#multiple-selectors)

### Requisiti dell’editor di testo {#text-editor-requirements}

Se desideri utilizzare l’editor locale di un componente di testo creato in SPA è necessaria una configurazione aggiuntiva.

1. Imposta un attributo (può essere qualsiasi) sull&#39;elemento wrapper del contenitore contenente il testo HTML. Nel caso del contenuto di esempio di WKND Journal, è un `<div>` e il selettore utilizzato è `data-rte-editelement`.
1. Imposta la configurazione `editElementQuery` sul componente di testo AEM corrispondente `cq:InplaceEditingConfig` che punta a quel selettore, ad esempio `data-rte-editelement`. Questo consente all’editor di sapere quale elemento HTML applica al testo di HTML.

Per un esempio di come eseguire questa operazione, consulta [Contenuto di esempio del Journal WKND.](https://github.com/adobe/aem-sample-we-retail-journal/pull/16/files)

Per ulteriori informazioni sulla `editElementQuery` e la configurazione dell&#39;editor Rich Text, vedi [Configura l’editor Rich Text.](/help/sites-administering/rich-text-editor.md)

### Limitazioni  {#limitations}

L&#39;SDK dell&#39;editor SPA AEM è stato introdotto con AEM 6.4 service pack 2. È completamente supportato dall’Adobe e continua a essere migliorato ed esteso. Le seguenti funzioni AEM non sono ancora supportate dall’editor SPA:

* Modalità di destinazione
* ContextHub
* Modifica delle immagini in linea
* Modificare le configurazioni (ad esempio ascoltatori)
* Annulla/Ripristina
* Differf pagina e Alterazione ora
* Funzionalità che eseguono la riscrittura sul lato server di HTML, come Link Checker, servizio di rewriter CDN, accorciamento degli URL, ecc.
* Modalità Sviluppatore
* Lanci AEM
