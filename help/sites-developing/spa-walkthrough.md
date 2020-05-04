---
title: Introduzione e introduzione SPA
seo-title: Introduzione e introduzione SPA
description: Questo articolo introduce i concetti di SPA e illustra come utilizzare un’applicazione SPA di base per l’authoring, mostrando il suo rapporto con l’Editor AEM SPA sottostante.
seo-description: Questo articolo introduce i concetti di SPA e illustra come utilizzare un’applicazione SPA di base per l’authoring, mostrando il suo rapporto con l’Editor AEM SPA sottostante.
uuid: 4b0a9e53-3892-4d60-8bd3-7ff740d2f137
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 0478afcb-b029-4ce6-b3e6-cee4bb5408ce
docset: aem65
translation-type: tm+mt
source-git-commit: 14cc66dfef7bc7781907bdd6093732912c064579

---


# Introduzione e introduzione SPA{#spa-introduction-and-walkthrough}

Le applicazioni SPA (Single Page Applications) possono offrire esperienze coinvolgenti agli utenti di siti Web. Gli sviluppatori desiderano essere in grado di creare siti utilizzando i framework SPA e gli autori desiderano modificare facilmente i contenuti in AEM per un sito creato utilizzando tali framework.

SPA Editor offre una soluzione completa per il supporto degli SPA in AEM. Questo articolo descrive l’utilizzo di un’applicazione SPA di base per l’authoring e illustra i rapporti con l’Editor AEM SPA sottostante.

>[!NOTE]
>
>SPA Editor è la soluzione consigliata per i progetti che richiedono il rendering lato client basato su SPA (ad esempio React o Angular).

## Introduzione {#introduction}

### Articolo Obiettivo {#article-objective}

Questo articolo introduce i concetti di base degli SPA prima di guidare il lettore attraverso una panoramica dettagliata dell&#39;editor SPA, utilizzando una semplice applicazione SPA per dimostrare l&#39;editing di base dei contenuti. Viene quindi descritto come creare la pagina e come l’applicazione SPA si collega e interagisce con AEM SPA Editor.

L’obiettivo di questa introduzione e di questa procedura dettagliata è dimostrare a uno sviluppatore AEM perché le app SPA sono rilevanti, come funzionano generalmente, come un’app SPA viene gestita dall’editor AEM SPA e come è diversa da un’applicazione AEM standard.

La procedura dettagliata si basa sulle funzionalità standard di AEM e sull’app di esempio We.Retail Journal. Devono essere soddisfatti i seguenti requisiti:

* [AEM versione 6.4 con service pack 2 o successiva
   ](/help/release-notes/sp-release-notes.md)
* [Installa l&#39;app di esempio We.Retail Journal disponibile su GitHub qui.](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)

>[!CAUTION]
>
>Questo documento utilizza l&#39;app [](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) We.Retail Journal solo a scopo dimostrativo. Non deve essere utilizzato per nessun progetto.
>
>Qualsiasi progetto AEM deve sfruttare il tipo di archivio dei progetti [AEM](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/developing/archetype/overview.html), che supporta i progetti SPA mediante React o Angular e sfrutta l’SDK SPA.

### Che cos&#39;è un SPA? {#what-is-a-spa}

Un&#39;applicazione a pagina singola (SPA) differisce da una pagina tradizionale in quanto viene sottoposta a rendering sul lato client ed è principalmente guidata da Javascript, basandosi sulle chiamate Ajax per caricare i dati e aggiornare dinamicamente la pagina. La maggior parte o tutto il contenuto viene recuperato una volta in un singolo caricamento di pagina con risorse aggiuntive caricate in modo asincrono in base alle esigenze, in base all&#39;interazione dell&#39;utente con la pagina.

Questo riduce la necessità di aggiornare le pagine e offre all&#39;utente un&#39;esperienza semplice, rapida e più simile a un&#39;esperienza app nativa.

AEM SPA Editor consente agli sviluppatori front-end di creare SPA da integrare in un sito AEM, consentendo agli autori di modificare i contenuti SPA con la stessa facilità con cui si trovano tutti gli altri contenuti AEM.

### Perché una SPA? {#why-a-spa}

Grazie a un&#39;applicazione nativa più veloce, fluida e semplice, l&#39;SPA diventa un&#39;esperienza molto interessante non solo per il visitatore della pagina Web, ma anche per gli esperti di marketing e gli sviluppatori, a causa della natura del funzionamento degli SPA.

![screen_shot_2018-08-20at135550](assets/screen_shot_2018-08-20at135550.png)

**Visitatori**

* I visitatori desiderano esperienze simili a quelle native quando interagiscono con i contenuti.
* Esistono dati chiari che più veloce sarà una pagina, più probabile sarà una conversione.

**Marketing**

* Gli esperti di marketing desiderano offrire esperienze ricche e native per consentire ai visitatori di interagire pienamente con i contenuti.
* La personalizzazione può rendere queste esperienze ancora più coinvolgenti.

**Sviluppatori**

* Gli sviluppatori desiderano una netta separazione tra contenuti e presentazioni.
* La separazione pulita rende il sistema più estensibile e consente uno sviluppo front-end indipendente.

### Come funziona una SPA? {#how-does-a-spa-work}

L&#39;idea principale alla base di uno SPA è che le chiamate e la dipendenza da un server vengono ridotte al fine di ridurre al minimo i ritardi causati dalle chiamate server in modo che l&#39;SPA si avvicini alla reattività di un&#39;applicazione nativa.

In una pagina Web sequenziale tradizionale, vengono caricati solo i dati necessari per la pagina immediata. Questo significa che quando il visitatore si sposta in un’altra pagina, il server viene chiamato per le risorse aggiuntive. Potrebbero essere necessarie ulteriori chiamate quando il visitatore interagisce con gli elementi sulla pagina. Queste chiamate multiple possono dare un senso di ritardo o ritardo, in quanto la pagina deve essere in grado di soddisfare le richieste del visitatore.

![screen_shot_2018-08-20at140449](assets/screen_shot_2018-08-20at140449.png)

Per un&#39;esperienza più fluida, che si avvicina alle aspettative di un visitatore dalle app native per dispositivi mobili, un&#39;app SPA carica tutti i dati necessari per il visitatore al primo caricamento. Anche se inizialmente l&#39;operazione potrebbe richiedere un po&#39; più di tempo, elimina la necessità di ulteriori chiamate server.

Rendering sul lato client, l’elemento di pagina reagisce più rapidamente e le interazioni con la pagina da parte del visitatore sono immediate. Eventuali dati aggiuntivi che potrebbero essere necessari vengono denominati in modo asincrono per massimizzare la velocità della pagina.

>[!NOTE]
>
>Per informazioni tecniche sul funzionamento degli SPA in AEM, consultate l’articolo [Guida introduttiva alle app SPA in AEM](/help/sites-developing/spa-getting-started-react.md).
>
>Per un&#39;occhiata più dettagliata alla progettazione, all&#39;architettura e al flusso di lavoro tecnico dell&#39;editor SPA, consultate l&#39;articolo Panoramica [dell&#39;editor](/help/sites-developing/spa-overview.md)SPA.

## Esperienza di editing dei contenuti con SPA {#content-editing-experience-with-spa}

Quando un&#39;app SPA è creata per sfruttare l&#39;Editor AEM SPA, l&#39;autore del contenuto non nota alcuna differenza quando si modifica e si crea contenuto. È disponibile una comune funzionalità di AEM e non sono necessarie modifiche al flusso di lavoro dell’autore.

>[!NOTE]
>
>La procedura dettagliata si basa sulle funzionalità standard di AEM e sull’app di esempio We.Retail Journal. Devono essere soddisfatti i seguenti requisiti:
>
>* [AEM versione 6.4 con service pack 2](/help/release-notes/sp-release-notes.md)
>* [Installa l&#39;app di esempio We.Retail Journal disponibile su GitHub qui.](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal)
>



1. Modificate l&#39;app We.Retail Journal in AEM.

   `https://localhost:4502/editor.html/content/we-retail-journal/react.html`

   ![screen_shot_2018-06-07at142533](assets/screen_shot_2018-06-07at142533.png)

1. Selezionate un componente di intestazione e osservate che la barra degli strumenti è simile a quella di qualsiasi altro componente. Seleziona **Modifica**.

   ![screen_shot_2018-06-07at142937](assets/screen_shot_2018-06-07at142937.png)

1. Modificate il contenuto come normale in AEM e tenete presente che le modifiche sono persistenti.

   ![screen_shot_2018-06-07at143419](assets/screen_shot_2018-06-07at143419.png)

   >[!NOTE]
   >Per ulteriori informazioni sull’editor di testo e sulle app [SPA, consultate Panoramica](spa-overview.md#requirements-limitations) sull’editor di testo locale.

1. Usate il Browser risorse per trascinare una nuova immagine in un componente immagine.

   ![screen_shot_2018-06-07at143530](assets/screen_shot_2018-06-07at143530.png)

1. La modifica è persistente.

   ![screen_shot_2018-06-07at143732](assets/screen_shot_2018-06-07at143732.png)

Sono supportati ulteriori strumenti di authoring, come il trascinamento di componenti aggiuntivi sulla pagina, la ridisposizione dei componenti e la modifica del layout, come in qualsiasi applicazione non SPA.

>[!NOTE]
>
>L’editor SPA non modifica il DOM dell’applicazione. La stessa SPA è responsabile del DOM.
>
>Per vedere come funziona, continuate con la sezione successiva di questo articolo App [SPA e Editor](/help/sites-developing/spa-walkthrough.md#spa-apps-and-the-aem-spa-editor)AEM SPA.

## App SPA e AEM SPA Editor {#spa-apps-and-the-aem-spa-editor}

L&#39;esperienza di comportamento di un&#39;app SPA per l&#39;utente finale e quindi l&#39;analisi della pagina SPA consentono di comprendere meglio in che modo un&#39;app SAP funziona con l&#39;editor SPA in AEM.

### Utilizzo di un&#39;applicazione SPA {#using-an-spa-application}

1. Caricate l’applicazione We.Retail Journal sul server di pubblicazione o utilizzando l’opzione **Visualizza come pubblicato** dal menu Informazioni **** pagina nell’editor pagina.

   `/content/we-retail-journal/react.html`

   ![screen_shot_2018-06-08at102650](assets/screen_shot_2018-06-08at102650.png)

   Prendete nota della struttura delle pagine, inclusa la navigazione verso pagine figlie, widget meteo e articoli.

1. Passa a una pagina figlia utilizzando il menu e verifica che la pagina venga caricata immediatamente senza che sia necessario effettuare un aggiornamento.

   ![screen_shot_2018-06-08at102815](assets/screen_shot_2018-06-08at102815.png)

1. Aprite gli strumenti di sviluppo integrati del browser e monitorate l&#39;attività di rete mentre vi spostate nelle pagine figlie.

   ![screen_shot_2018-06-08at103922](assets/screen_shot_2018-06-08at103922.png)

   Il traffico si riduce notevolmente quando si passa da una pagina all&#39;altra nell&#39;app. La pagina non viene ricaricata e vengono richieste solo le nuove immagini.

   L&#39;SPA gestisce i contenuti e l&#39;indirizzamento interamente sul lato client.

Quindi, se la pagina non viene ricaricata durante la navigazione tra le pagine figlie, come viene caricata?

La sezione successiva, [Caricamento di un&#39;applicazione](/help/sites-developing/spa-walkthrough.md#loading-an-spa-application)SPA, approfondisce la procedura di caricamento dell&#39;SPA e spiega come è possibile caricare il contenuto in modo sincrono e asincrono.

### Caricamento di un&#39;applicazione SPA {#loading-an-spa-application}

1. Se non è già stato caricato, caricate l’applicazione We.Retail Journal sul server di pubblicazione o utilizzando l’opzione **Visualizza come pubblicato** dal menu Informazioni **** pagina nell’editor pagina.

   `/content/we-retail-journal/react.html`

   ![screen_shot_2018-06-07at144736](assets/screen_shot_2018-06-07at144736.png)

1. Utilizzate lo strumento incorporato del browser per visualizzare l’origine della pagina.
1. Il contenuto dell&#39;origine è estremamente limitato.

   ```
   <!DOCTYPE HTML>
   <html lang="en-CH">
       <head>
       <meta charset="UTF-8">
       <title>We.Retail Journal</title>
   
       <meta name="template" content="we-retail-react-template"/>
   
   <link rel="stylesheet" href="/etc.clientlibs/we-retail-journal/react/clientlibs/we-retail-journal-react.css" type="text/css">
   
   <link rel="stylesheet" href="/libs/wcm/foundation/components/page/responsive.css" type="text/css">
   
   </head>
       <body class="page basicpage">
   
   <div id="page"></div>
   
   <script type="text/javascript" src="/etc.clientlibs/we-retail-journal/react/clientlibs/we-retail-journal-react.js"></script>
   
       </body>
   </html>
   ```

   La pagina non ha alcun contenuto all’interno del suo corpo. È composta principalmente da fogli di stile e una chiamata a uno script React, `we-retail-journal-react.js`.

   Questo script React è il driver principale di questa applicazione ed è responsabile del rendering di tutto il contenuto.

1. Utilizzate gli strumenti integrati del browser per ispezionare la pagina. Visualizzare il contenuto del DOM completamente caricato.

   ![screen_shot_2018-06-07at151848](assets/screen_shot_2018-06-07at151848.png)

1. Passate alla scheda Rete in Ispettore e ricaricate la pagina.

   Ignorando le richieste di immagini, tenete presente che le risorse principali caricate per la pagina sono la pagina stessa, CSS, il JavaScript React, le sue dipendenze e i dati JSON per la pagina.

   ![screen_shot_2018-06-07at152155](assets/screen_shot_2018-06-07at152155.png)

1. Caricate il file `react.model.json` in una nuova scheda.

   `/content/we-retail-journal/react.model.json`

   ![screen_shot_2018-06-07at152636](assets/screen_shot_2018-06-07at152636.png)

   AEM SPA Editor sfrutta [AEM Content Services](/help/assets/content-fragments.md) per distribuire l’intero contenuto della pagina come modello JSON.

   Implementando interfacce specifiche, Sling Models fornisce le informazioni necessarie alla SPA. La consegna dei dati JSON viene delegata verso il basso a ciascun componente (dalla pagina al paragrafo, al componente, ecc.).

   Ciascun componente sceglie le funzioni esposte e di rendering (lato server con HTL o lato client con React). Naturalmente questo articolo si concentra sul rendering lato client con React.

1. Il modello può anche raggruppare le pagine in modo che vengano caricate in modo sincrono, riducendo il numero di ricariche di pagina necessarie.

   Nell&#39;esempio di We.Retail Journal, le `home`, `blog`e `aboutus` le pagine vengono caricate in modo sincrono, poiché i visitatori visitano comunemente tutte queste pagine. Tuttavia, la `weather` pagina viene caricata in modo asincrono, poiché i visitatori hanno meno probabilità di visitarla.

   Questo comportamento non è obbligatorio ed è completamente definibile.

   ![screen_shot_2018-06-07at153945](assets/screen_shot_2018-06-07at153945.png)

1. Per visualizzare questa differenza di comportamento, ricaricare la pagina e cancellare l&#39;attività di rete della finestra di ispezione. Nel menu della pagina, andate al blog e alle pagine su di noi e scoprite che non è stata segnalata alcuna attività di rete.

   Passate alla pagina meteo e verificate che la chiamata `weather.model.json` sia chiamata in modo asincrono.

   ![screen_shot_2018-06-07at155738](assets/screen_shot_2018-06-07at155738.png)

### Interazione con l&#39;editor SPA {#interaction-with-the-spa-editor}

Utilizzando l&#39;applicazione di esempio We.Retail Journal, è chiaro come l&#39;app si comporta e viene caricata quando viene pubblicata, sfruttando i servizi di contenuto per la distribuzione dei contenuti JSON e il caricamento asincrono delle risorse.

Inoltre, per l’autore di contenuti, la creazione di contenuti tramite un editor SPA è semplice in AEM.

Nella sezione seguente verrà illustrato il contratto che consente all’editor SPA di correlare i componenti dell’SPA ai componenti di AEM e di ottenere questa esperienza di modifica senza soluzione di continuità.

1. Caricate l&#39;applicazione We.Retail Journal nell&#39;editor e passate alla modalità **Anteprima** .

   `https://localhost:4502/editor.html/content/we-retail-journal/react.html`

1. Utilizzando gli strumenti di sviluppo incorporati del browser, controllate il contenuto della pagina. Con lo strumento selezione, selezionate un componente modificabile sulla pagina e visualizzate il dettaglio dell’elemento.

   Il componente ha un nuovo attributo dati `data-cq-data-path`.

   ![screen_shot_2018-06-08at095124](assets/screen_shot_2018-06-08at095124.png)

   Ad esempio

   `data-cq-data-path="root/responsivegrid/paragraph_1`

   Questi percorsi consentono il recupero e l&#39;associazione dell&#39;oggetto di configurazione del contesto di modifica di ciascun componente.

   Si tratta dell’unico attributo di markup richiesto all’editor per riconoscere questo componente come modificabile all’interno dell’area di protezione speciale. In base a questo attributo, l&#39;editor SPA determinerà quale configurazione modificabile è associata al componente, in modo che il frame, la barra degli strumenti e così via siano corretti. è caricato.

   Alcuni nomi di classe specifici vengono aggiunti anche per i segnaposto di marketing e per la funzionalità di trascinamento della risorsa.

   >[!NOTE]
   >
   >Si tratta di una modifica nel comportamento delle pagine sottoposte a rendering sul lato server in AEM, in cui è inserito un `cq` elemento per ciascun componente modificabile.
   >
   >
   >Questo approccio in SPA elimina la necessità di inserire elementi personalizzati, basandosi solo su un attributo di dati aggiuntivo, semplificando il markup per lo sviluppatore frontend.

## Passaggi successivi {#next-steps}

Ora che hai compreso l&#39;esperienza di editing SPA in AEM e come l&#39;SPA si relaziona con l&#39;Editor SPA, approfondisci la tua conoscenza di come è stata creata l&#39;SPA.

* [La Guida introduttiva alle app SPA in AEM](/help/sites-developing/spa-getting-started-react.md) illustra come è possibile creare un&#39;app SPA di base per l&#39;utilizzo con l&#39;editor SPA in AEM
* [Panoramica](/help/sites-developing/spa-overview.md) dell&#39;editor SPA approfondisce il modello di comunicazione tra AEM e l&#39;SPA.
* [Lo sviluppo di SPA per AEM](/help/sites-developing/spa-architecture.md) descrive come coinvolgere gli sviluppatori front-end nello sviluppo di una SPA per AEM e come le SPA interagiscono con l’architettura di AEM.
