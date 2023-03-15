---
title: Percorso della tua prima esperienza con AEM Headless
description: In questa parte del Percorso per sviluppatori headless AEM, comprenderai i passaggi per implementare la tua prima esperienza headless in AEM incluse considerazioni sulla pianificazione e apprenderai le best practice per rendere il percorso il più semplice possibile.
exl-id: 64a87b6b-67ff-4d88-9dfb-c3e5de65bbe6
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1982'
ht-degree: 99%

---

# Percorso della tua prima esperienza con AEM Headless {#path-to-first-experience}

In questa parte del [Percorso per sviluppatori headless AEM,](overview.md) comprenderai i passaggi per implementare la tua prima esperienza headless in AEM incluse considerazioni sulla pianificazione e apprenderai le best practice per rendere il percorso il più semplice possibile.

## Percorso affrontato finora {#story-so-far}

Nel documento precedente del percorso di AEM Headless, [Guida introduttiva a AEM Headless ](getting-started.md) hai imparato la teoria di base su cosa sia un CMS headless e ora dovresti:

* Comprendere le nozioni di base delle funzioni headless di AEM.
* Conoscere i prerequisiti per l’utilizzo delle funzionalità headless di AEM.
* Essere a conoscenza dei livelli di integrazione headless di AEM.
* Essere in grado di definire il tuo progetto in termini di ambito.

Questo articolo si basa su questi fondamentali in modo da capire come preparare il tuo progetto AEM headless.

## Obiettivo {#objective}

Questo documento illustra i passaggi necessari per implementare il primo progetto. Dopo averlo letto dovresti:

* Comprendere importanti considerazioni sulla pianificazione per la progettazione dei contenuti.
* Comprendere i passaggi per implementare headless in AEM.
* Sapere quali strumenti e configurazioni AEM sono necessari.
* Conoscere le best practice per semplificare il tuo percorso headless, garantire la distribuzione rapida dei contenuti e l’efficienza nella loro generazione.

## Requisiti {#requirements}

Prima di continuare con questo documento, accertati di aver rivisto il documento precedente nel Percorso per sviluppatori headless AEM, [Guida introduttiva a AEM Headless ](getting-started.md) assicurandoti di:

* Soddisfare i requisiti elencati.
* Aver preso in considerazione la definizione del tuo progetto, compresi ambito, ruoli e prestazioni.

## Pianificazione del successo {#planning-for-success}

Per avviare il tuo primo progetto AEM headless devi disporre di un modello di contenuto che supporti la personalizzazione e gli aggiornamenti che desideri eseguire su tutti i tuoi canali.

Separato da AEM, assicurati anche di disporre di una configurazione dell’ambiente di sviluppo appropriata se stai creando un’applicazione lato client in modo da poter testare il client rispetto alle chiamate API a AEM.

### Definizione di modelli di contenuto e API {#defining-models}

Vuoi creare un’esperienza coerente e gestire campagne personalizzate tra i canali, in modo da poter esaminare ogni singolo canale e superficie come una propria struttura di contenuti distinta a cui distribuire. Tuttavia, un modello di contenuto a disposizione per ogni canale sarà difficile da mantenere.

È invece necessario considerare il modo in cui il contenuto su superfici diverse è correlato in base a principi di organizzazione quali gerarchie di marchi e prodotti, categorie di beni o superfici o passaggi nel percorso del cliente. Ad esempio, se disponi di un insieme di superfici che supportano un marchio specifico di auto prodotte, potresti voler iniziare con un modello di contenuto per informazioni generali che sarebbe vero per l’intera auto e poi avere elementi più specifici come il contenuto necessario da quando l’auto si avvia a quando ci sono problemi di servizio. Un modello di questo tipo applicherà l’ereditarietà del contenuto generale del marchio automobilistico, consentendo al tempo stesso turni in base al contesto specifico necessario. Aiuta anche nella gestione futura degli aggiornamenti di questo contenuto in quanto puoi applicare il controllo in base a ruoli come l’addetto marketing o il responsabile prodotto per l’intero marchio automobilistico rispetto a un autore responsabile dell’esperienza di “avvio automobile”.

Una volta ottenuto il modello di contenuto e una visualizzazione chiara dei vari client su cui deve essere mostrato il contenuto, è necessario assicurarsi che le API/GraphQL associate all’accesso a vari modelli di contenuto siano pubblicate per tutti i client che necessitano di tale contenuto. Esistono diverse opzioni per accedere a determinati contenuti. Puoi richiedere un contenuto specifico statico che consenta la memorizzazione in cache del contenuto e prestazioni migliori. Puoi anche richiedere contenuti generati dinamicamente che richiederanno un’elaborazione maggiore. Assicurati che i client sfruttino le API più efficienti per le loro esigenze aziendali.

## Informazioni sugli ambienti {#understanding-environments}

All’interno di AEM esistono tre tipi di ambienti: sviluppo, staging e produzione.

Gli ambienti di sviluppo (se ne possono avere diversi) sono un luogo sicuro in cui sperimentare e testare idee. Durante la fase iniziale del progetto, Adobe consiglia di utilizzare gli ambienti di sviluppo per provare le varianti dei modelli di contenuto e vedere quali forniscono l’output previsto per le superfici.

L’ambiente di staging per i progetti headless viene utilizzato per convalidare le nuove versioni di prodotto AEM prima che vengano lanciate in produzione. Tieni un elenco aggiornato dei modelli di contenuto di produzione e un sottoinsieme di contenuto, in modo da poter fare eseguire il rendering dei file JSON per confrontare se forniscono ancora lo stesso output mentre apporti modifiche o se la versione di AEM introduce modifiche

La produzione è il luogo in cui gli autori di contenuti creano e gestiscono il contenuto effettivo. I cambiamenti del modello nella produzione devono essere effettuati con cura e tenendo presente la compatibilità con le versioni precedenti.

Durante la fase di sviluppo, si consiglia di lavorare con un ambiente di sviluppo e di staging. Passando al test delle prestazioni, dovrai passare all’ambiente di produzione.

### Cooperazione tra sviluppatori e autori di contenuti {#cooperation}

Gli sviluppatori devono disporre di un ambiente di sviluppo AEM configurato con i modelli di contenuto popolati. Lo sviluppatore sviluppa il client che utilizzerà i contenuti da AEM headless, in quanto gli autori dei contenuti stanno ancora creando i contenuti. Ecco perché le definizioni API sono molto importanti. Sfruttando l’SDK di AEM, lo sviluppatore può creare un hook di prova in modo da poter creare client test e unit test per assicurarsi che il client sia in grado di eseguire correttamente il rendering del contenuto.

Gli autori e le autrici dei contenuti creano contenuti in base ai modelli di contenuto definiti nell’ambiente di staging. Utilizzando lo strumento per l’authoring dei frammenti di contenuto, l’autore crea un nuovo frammento di contenuto o ne modifica uno esistente. Prima di pubblicarlo, l’autore o l&#39;autrice può visualizzare un’anteprima dell’aspetto che avrà nel client collaborando con lo sviluppatore per inviare il modello di contenuto allo sviluppo o impostare un ambiente per sviluppatori in modo che gli autori e le autrici possano visualizzare in anteprima l’aspetto che avrà nel client.

## Configurazione {#setup}

Prima di iniziare a utilizzare le funzionalità headless in AEM, assicurati che tutte le funzioni richieste siano abilitate. Questa sezione descrive i requisiti necessari. I passi effettivi per eseguire questi passaggi sono descritti più avanti nel [Percorso per sviluppatori headless di AEM.](#overview.md)

Facoltativamente, puoi anche fare riferimento alle [risorse aggiuntive](#additional-resources) per ulteriori informazioni sui singoli argomenti.

### Configurazione {#configuration}

1. Abilitare frammenti di contenuto
1. Abilitare GraphQL
1. Configurazione di SDK headless

## Implementazione della prima app AEM headless

Questa è una panoramica di ciò che è necessario per implementare la prima app headless utilizzando AEM per distribuire i contenuti. Come eseguire questi passaggi sarà descritto in dettaglio nelle parti successive del Percorso per Sviluppatori Headless.

1. Creare modelli di frammenti di contenuto
1. Creare frammenti di contenuto
1. Query del contenuto con GraphQL

## Best practice   {#best-practices}

Un progetto headless non solo ha successo grazie alla tecnologia implementata, ma anche grazie alla buona pianificazione e alla governance dei progetti. Di seguito sono riportate alcune best practice che gli autori e gli sviluppatori di contenuti devono tenere a mente durante la pianificazione del progetto.

### Organizzazione dei contenuti {#organizing-content}

* Crea una struttura complessa quanto è necessario, ma rendila il più semplice possibile. Strutture dei contenuti più semplici consentono di semplificare la governance dei contenuti e di migliorare le prestazioni del sistema.
* Dare priorità al riutilizzo dei contenuti nella tua strategia. Creare sottomodelli e riferimenti al contenuto che possono essere riutilizzati su più modelli e canali di livello superiore.
* Rendi le strutture dei contenuti il più possibile autoesplicative, in modo che gli autori dei contenuti possano imparare e adattarsi rapidamente alle attività di authoring.
* Se disponi di restrizioni di accesso, prova ad allineare il modello di contenuto ai requisiti di accesso.
* Quando si dispone dei requisiti di accesso, questi devono guidare la gerarchia dei contenuti. Raggruppare i contenuti che vengono modificati dallo stesso gruppo di persone.
* Raggruppare contenuti simili in una cartella.
   * È più probabile che un autore o un’autrice di contenuti copi e incolli contenuti esistenti per creare nuovi contenuti. Pertanto, farlo fare nella stessa cartella rende tutto più efficiente.
   * AEM consente di impostare i modelli per cartella in modo che il pulsante **Crea nuovo** mostrerà solo i modelli supportati in tale posizione.
* La creazione di nuovi frammenti di contenuto nell’editor frammenti di contenuto in linea può essere semplificata se la cartella principale è impostata nel modello. Quindi il professionista o la professionista non deve scegliere una posizione, ma deve solo fornire un nome e può iniziare a modificare il nuovo riferimento.

### Creazione di contenuti {#authoring}

* Per le versioni del contenuto specifiche del canale, è consigliabile utilizzare varianti di frammento di contenuto. Le varianti vengono sincronizzate con lo schema del contenuto per semplificare la gestione delle modifiche al contenuto.
* Invitare altri produttori di contenuti a esaminare i contenuti e fornire feedback con annotazioni e commenti, disponibili nell’editor dei frammenti di contenuto e a livello globale tra i vari frammenti nell’Admin Console dei frammenti di contenuto.
* Mantenere le cose in movimento con il minor numero possibile di elementi obbligatori. Gli elementi obbligatori possono bloccare il flusso di lavoro.

### Creazione di contenuti globali {#localization}

* Stabilire regole e governance per la traduzione dei contenuti. Per ridurre il carico del sistema, impostare la traduzione come processo asincrono che può essere eseguito a intervalli più lunghi. Concedere del tempo per il controllo della qualità della localizzazione e la correzione dei bug.
* Sfruttare tutte le funzionalità offerte dal sistema di tecnologia di traduzione che è possibile integrare con AEM come memoria di traduzione.
* Comprendere se i contenuti multimediali complessi, come immagini e video, devono essere localizzati.

## Passaggio successivo {#what-is-next}

Ora che hai completato questa parte del percorso per sviluppatori headless di AEM, dovresti:

* Comprendere importanti considerazioni sulla pianificazione per la progettazione dei contenuti.
* Comprendere i passaggi per implementare headless in AEM.
* Sapere quali strumenti e configurazioni AEM sono necessari.
* Conoscere le best practice per semplificare il tuo percorso headless, garantire la distribuzione rapida dei contenuti e l’efficienza nella loro generazione.

Vogliamo che tu sfrutti questa conoscenza fondamentale per comprendere appieno il potere e la flessibilità di AEM Headless in modo da poterne trarre vantaggio nei tuoi progetti. Per fare questo, hai diverse possibilità.

### Scegli la tua avventura {#choose-your-path}

Indipendentemente dal tuo stile di apprendimento, Adobe vuole che tu abbia successo quando inizi con il tuo progetto AEM Headless.

* Se preferisci continuare a **scoprire i concetti headless e le tecnologie headless di AEM**, dovresti continuare il tuo percorso AEM headless studiando il documento [Come modellare il contenuto come modelli di contenuto AEM](model-your-content.md) che illustra come modellare la struttura del contenuto in AEM.
* Se preferisci **imparare facendo**, puoi passare al [Tutorial pratico di introduzione ad AEM Headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=it) che ti consente di iniziare direttamente con lo sviluppo AEM Headless implementando un semplice progetto che espone il contenuto headless AEM.

## Risorse aggiuntive {#additional-resources}

Sebbene sia consigliabile passare alla parte successiva del percorso di sviluppo headless consultando il documento [Come modellare i contenuti come Modelli di contenuto AEM](model-your-content.md) le seguenti sono alcune risorse aggiuntive e opzionali che approfondiscono alcuni concetti menzionati in questo documento, ma non sono indispensabili per continuare il percorso headless.

* [Percorso di traduzione AEM headless](/help/journey-headless/translation/overview.md): questo percorso di documentazione ti offre un’ampia comprensione della tecnologia headless, dell’utilizzo di AEM dei contenuti headless e di come tradurli.
* [Sviluppo headless per AEM Sites ](/help/sites-developing/headless/introduction.md): una rapida introduzione per orientare lo sviluppatore AEM Headless nell’utilizzo delle funzioni necessarie
* [Esercitazioni di AEM Headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=it) - Segui queste esercitazioni pratiche per scoprire come utilizzare le varie opzioni per distribuire contenuti agli endpoint headless con AEM e scegliere quello adatto a te.
* [Gestione dei contenuti headless tramite le API GraphQL](https://experienceleague.adobe.com/?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;launch=ExperienceManager-D-1-2020.1.headless&amp;lang=it#courses) - Segui questo corso per una panoramica dell’API GraphQL implementata in AEM. È necessaria l’autenticazione tramite AdobeID.
* [Guida AEM WKND - GraphQL](https://github.com/adobe/aem-guides-wknd-graphql) - Questo progetto GitHub include applicazioni di esempio che mettono in evidenza le API GraphQL di AEM.
* [Guida introduttiva a Headless](/help/sites-developing/headless/introduction.md#getting-started) - Introduzione rapida alle funzioni AEM headless per gli utenti già esperti di AEM.
* [Creare modelli di frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md): documentazione tecnica sui modelli per frammenti di contenuto
* [Creare frammenti di contenuto](/help/assets/content-fragments/content-fragments.md): documentazione tecnica sui frammenti di contenuto
* [Query del contenuto con GraphQL](/help/assets/content-fragments/graphql-api-content-fragments.md): documentazione tecnica sull’API GraphQL
