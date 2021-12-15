---
title: Percorso per la prima esperienza con AEM Headless
description: In questa parte del Percorso di sviluppatori headless AEM, comprenderai i passaggi per implementare la tua prima esperienza headless in AEM incluse considerazioni sulla pianificazione e apprendi le best practice per rendere il percorso il più semplice possibile.
source-git-commit: 0458a811b5bd062abbe8a42ec141bc786491e19e
workflow-type: tm+mt
source-wordcount: '1982'
ht-degree: 0%

---

# Percorso per la prima esperienza con AEM Headless {#path-to-first-experience}

In questa parte del [AEM Percorso di sviluppo headless,](overview.md) comprenderai i passaggi per implementare la tua prima esperienza headless in AEM incluse considerazioni sulla pianificazione e apprendi le best practice per rendere il percorso il più semplice possibile.

## La storia finora {#story-so-far}

Nel documento precedente del percorso senza testa AEM, [Guida introduttiva di AEM Headless](getting-started.md) hai imparato la teoria di base su cosa sia un CMS headless e dovresti ora:

* Comprendere le nozioni di base AEM funzioni headless.
* Conoscere i prerequisiti per l&#39;utilizzo di AEM funzionalità headless.
* Presta attenzione AEM livelli di integrazione headless.
* Puoi definire il tuo progetto in termini di ambito.

Questo articolo si basa su questi fondamentali in modo da capire come preparare il tuo progetto AEM headless.

## Obiettivo {#objective}

Questo documento illustra i passaggi necessari per implementare il primo progetto. Dopo la lettura dovrebbe:

* Comprendere importanti considerazioni sulla pianificazione per la progettazione dei contenuti.
* Comprendi i passaggi per implementare headless in AEM.
* Scopri quali strumenti e configurazioni AEM sono necessari.
* Scopri le best practice per semplificare il tuo percorso headless, garantire l’efficienza nella generazione dei contenuti e la distribuzione rapida dei contenuti.

## Requisiti {#requirements}

Prima di continuare con questo documento, accertati di aver rivisto il documento precedente nel Percorso di sviluppatori AEM Headless, [Guida introduttiva di AEM Headless](getting-started.md) assicurati di:

* Soddisfare i requisiti elencati.
* Hai preso in considerazione la definizione del tuo progetto, compresi ambito, ruoli e prestazioni.

## Pianificazione del successo {#planning-for-success}

Per avviare il tuo primo progetto AEM headless devi disporre di un modello di contenuto che supporti la personalizzazione e gli aggiornamenti che desideri eseguire su tutti i tuoi canali.

Separati da AEM, assicurati anche di disporre di un ambiente di sviluppo appropriato impostato se stai creando un&#39;applicazione lato client in modo da poter testare il client rispetto alle chiamate API a AEM.

### Definizione di modelli di contenuto e API {#defining-models}

Vuoi creare un’esperienza coerente e gestire campagne personalizzate tra i canali, in modo da poter esaminare ogni singolo canale e superficie come una propria struttura di contenuti distinta a cui eseguire la distribuzione. Tuttavia, disporre di un proprio modello di contenuto per ogni canale sarà difficile da mantenere.

È invece necessario considerare il modo in cui il contenuto su superfici diverse è correlato in base a principi di organizzazione quali gerarchie di marchi e prodotti, categorie di beni o superfici o passaggi nel percorso di clienti. Ad esempio, se si dispone di un insieme di superfici che supportano una marca specifica di auto prodotte, si può voler iniziare con un modello di contenuto per informazioni generali che sarebbe vero per l&#39;intera auto e poi avere elementi più specifici come il contenuto necessario quando l&#39;auto sta iniziando a quando ci sono problemi di servizio. Un modello di questo tipo applicherà l&#39;ereditarietà del contenuto generale del marchio automobilistico, consentendo al tempo stesso turni in base al contesto specifico necessario. Aiuta anche nella gestione futura degli aggiornamenti di questo contenuto in quanto puoi applicare il controllo in base a ruoli come l’addetto al marketing o il responsabile prodotto per l’intero marchio automobilistico rispetto a un autore responsabile dell’esperienza di &quot;automobile di partenza&quot;.

Una volta ottenuto il modello di contenuto e una visualizzazione chiara dei vari client a cui deve essere applicato il contenuto, è necessario assicurarsi che le API/GraphQL associate all’accesso a vari modelli di contenuto siano pubblicate su tutti i client che necessitano tale contenuto. Esistono diverse opzioni per accedere a determinati contenuti. Puoi richiedere un contenuto specifico statico che consenta il caching del contenuto e prestazioni migliori. Puoi anche richiedere contenuti generati dinamicamente che richiederanno un’elaborazione maggiore. Assicurati che i clienti sfruttino le API più efficienti per le loro esigenze aziendali.

## Informazioni sugli ambienti {#understanding-environments}

All&#39;interno di AEM esistono tre tipi di ambienti: sviluppo, staging e produzione.

Gli ambienti di sviluppo (se ne possono avere diversi) sono un luogo sicuro in cui sperimentare e sperimentare idee. Durante la fase iniziale del progetto, Adobe consiglia di utilizzare gli ambienti di sviluppo per provare le varianti dei modelli di contenuto e vedere quali forniscono l’output previsto per le superfici.

L’ambiente di staging per i progetti headless viene utilizzato per convalidare le nuove versioni di prodotto AEM prima che vengano implementate in produzione. Tieni un elenco aggiornato dei modelli di contenuto di produzione e un sottoinsieme di contenuto, in modo da poter fare eseguire il rendering dei file JSON per confrontare i file che comunque forniscono lo stesso output, come si apporta modifiche o la versione di AEM introduce modifiche

La produzione è il luogo in cui gli autori di contenuti creano e gestiscono il contenuto effettivo. I cambiamenti del modello nella produzione devono essere effettuati con cura e con la compatibilità con le versioni precedenti.

Durante la fase di sviluppo, si consiglia di lavorare con un ambiente di sviluppo e di staging. Passando al test delle prestazioni, dovrai passare all’ambiente di produzione.

### Cooperazione tra sviluppatori e autori di contenuti {#cooperation}

Gli sviluppatori devono disporre di un ambiente di sviluppo AEM configurato con i modelli di contenuto popolati. Lo sviluppatore sviluppa il client che utilizzerà i contenuti da AEM headless, in quanto gli autori dei contenuti stanno ancora creando i contenuti. Ecco perché le definizioni API sono molto importanti. Sfruttando l’SDK AEM, lo sviluppatore può creare un gancio di test in modo da poter creare test client e di unità per assicurarsi che il client sia in grado di eseguire correttamente il rendering del contenuto.

Gli autori dei contenuti creano contenuti in base ai modelli di contenuto definiti nell’ambiente di staging. Utilizzando lo strumento per l’authoring dei frammenti di contenuto, l’autore crea un nuovo frammento di contenuto o ne modifica uno esistente. Prima di pubblicarlo, l’autore può visualizzare un’anteprima dell’aspetto che avrà nel client collaborando con lo sviluppatore per inviare il modello di contenuto allo sviluppo o impostare un ambiente per sviluppatori, in modo che gli autori possano visualizzare in anteprima l’aspetto che avrà nel client.

## Configurazione {#setup}

Prima di iniziare a utilizzare le funzionalità headless in AEM, assicurati che tutte le funzioni richieste siano abilitate. Questa sezione descrive i requisiti necessari. I passi effettivi per eseguire questi passaggi sono descritti più avanti nella sezione [AEM Percorso di sviluppo headless.](#overview.md)

Facoltativamente, puoi anche fare riferimento al [risorse aggiuntive](#additional-resources) per ulteriori informazioni sui singoli argomenti.

### Configurazione {#configuration}

1. Abilita frammenti di contenuto
1. Abilita GraphQL
1. Configurare l&#39;SDK per headless

## Implementazione della prima app AEM headless

Questa è una panoramica di ciò che è necessario per implementare la prima app headless utilizzando AEM per distribuire i contenuti. Come eseguire questi passaggi sarà descritto in dettaglio nelle parti successive del Percorso Headless Developer.

1. Creare modelli di frammenti di contenuto
1. Creare frammenti di contenuto
1. Query del contenuto con GraphQL

## Best practice   {#best-practices}

Un progetto senza testa non solo ha successo grazie alla tecnologia implementata, ma anche grazie alla buona pianificazione e alla governance dei progetti. Di seguito sono riportate alcune best practice che gli autori e gli sviluppatori di contenuti devono tenere a mente durante la pianificazione del progetto.

### Organizzazione dei contenuti {#organizing-content}

* Rendere la struttura il più complessa possibile, ma mantenerla il più semplice possibile. La semplicità delle strutture dei contenuti consente di semplificare la governance dei contenuti e di migliorare le prestazioni del sistema.
* Dai priorità al riutilizzo dei contenuti nella tua strategia. Crea modelli secondari e riferimenti di contenuto che possono essere riutilizzati su più modelli e canali di livello superiore.
* Rendere le strutture dei contenuti il più possibile esplicative, in modo che gli autori possano imparare e adattarsi rapidamente alle attività di authoring.
* Se disponi di restrizioni di accesso, prova ad allineare il modello di contenuto ai requisiti di accesso.
* Quando si dispone dei requisiti di accesso, questi devono guidare la gerarchia dei contenuti. Raggruppa i contenuti che vengono modificati dallo stesso gruppo di persone.
* Raggruppa contenuti simili in una cartella.
   * È più probabile che un autore di contenuti copia e incolla contenuti esistenti per creare nuovi contenuti. Pertanto, farlo fare nella stessa cartella lo rende più efficiente.
   * AEM consente di impostare i modelli per cartella in modo che **Crea nuovo** mostrerà solo i modelli supportati in tale posizione.
* La creazione di nuovi frammenti di contenuto nell’editor frammento di contenuto in linea può essere semplificata se la cartella principale è impostata nel modello. Quindi il professionista non deve scegliere una posizione, ma deve solo fornire un nome e può iniziare a modificare il nuovo riferimento.

### Creazione di contenuti {#authoring}

* Per le versioni del contenuto specifiche per canale, è consigliabile utilizzare varianti di frammento di contenuto. Le varianti vengono sincronizzate con lo schema del contenuto per semplificare la gestione delle modifiche al contenuto.
* Invita altri produttori di contenuti a esaminare i contenuti e fornire feedback con annotazioni e commenti, disponibili nell’editor dei frammenti di contenuto e a livello globale tra i vari frammenti nell’Admin Console dei frammenti di contenuto.
* Mantenere le cose in movimento con il minor numero possibile di elementi obbligatori. Gli elementi obbligatori possono bloccare il flusso di lavoro.

### Creazione di contenuti globali {#localization}

* Stabilire regole e governance per la traduzione dei contenuti. Per ridurre il carico del sistema, stabilisci la traduzione come processo asincrono che può essere eseguito a intervalli più lunghi. Consenti per tempo il controllo della qualità della localizzazione e la correzione dei bug.
* Sfrutta tutte le funzionalità offerte dal tuo sistema di tecnologia di traduzione che puoi integrare con AEM come la memoria di traduzione.
* Comprendere se i contenuti rich media, come immagini e video, devono essere localizzati.

## Novità {#what-is-next}

Dopo aver completato questa parte del Percorso di sviluppatori AEM Headless, devi:

* Comprendere importanti considerazioni sulla pianificazione per la progettazione dei contenuti.
* Comprendi i passaggi per implementare headless in AEM.
* Scopri quali strumenti e configurazioni AEM sono necessari.
* Scopri le best practice per semplificare il tuo percorso headless, garantire l’efficienza nella generazione dei contenuti e la distribuzione rapida dei contenuti.

Vogliamo che si basi su questa conoscenza fondamentale per comprendere appieno il potere e la flessibilità di AEM Headless in modo da poterne trarre vantaggio per i propri progetti. Per fare questo, hai delle opzioni.

### Scegli la tua avventura {#choose-your-path}

Indipendentemente dal tuo stile di apprendimento, l&#39;Adobe vuole che tu abbia successo quando inizi con il tuo progetto AEM Headless.

* Se preferisci continuare a **scopri i concetti senza testa e le tecnologie senza testa AEM**, dovresti continuare il tuo percorso AEM headless rivedendo il documento [Come modellare il contenuto come modelli di contenuto AEM](model-your-content.md) dove viene illustrato come modellare la struttura del contenuto in AEM.
* Se preferisci **imparare facendo**, puoi passare alla [Guida introduttiva a AEM tutorial pratico headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) dove puoi passare direttamente AEM sviluppo Headless implementando un semplice progetto per esporre AEM contenuto headless.

## Risorse aggiuntive {#additional-resources}

Mentre è consigliabile passare alla parte successiva del percorso di sviluppo headless rivedendo il documento [Come modellare il contenuto come modelli di contenuto AEM,](model-your-content.md) di seguito sono riportate alcune risorse aggiuntive facoltative che approfondiscono alcuni concetti menzionati in questo documento, ma non è necessario che continuino sul percorso headless.

* [AEM Percorso di traduzione headless](/help/journey-headless/translation/overview.md) - Questo percorso di documentazione ti offre un’ampia comprensione della tecnologia headless, di come AEM i contenuti headless e di come tradurli.
* [Sviluppo headless per AEM Sites](/help/sites-developing/headless/introduction.md) - Una rapida introduzione per orientare lo sviluppatore AEM Headless con le funzioni necessarie
* [AEM Tutorials headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html) - Segui questi tutorial pratici per scoprire come utilizzare le varie opzioni per distribuire contenuti agli endpoint headless con AEM e scegliere quello che fa per te.
* [Gestione dei contenuti headless tramite API GraphQL](https://experienceleague.adobe.com/?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;launch=ExperienceManager-D-1-2020.1.headless#courses) - Segui questo corso per una panoramica dell’API GraphQL implementata in AEM. È necessaria l’autenticazione tramite AdobeID.
* [Guide AEM WKND - GraphQL](https://github.com/adobe/aem-guides-wknd-graphql) - Questo progetto GitHub include applicazioni di esempio che evidenziano AEM API GraphQL.
* [Guida introduttiva a Headless](/help/sites-developing/headless/introduction.md#getting-started) - Introduzione rapida alle funzioni AEM headless per gli utenti già esperti di AEM.
* [Creare modelli di frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md) - Documentazione tecnica sui modelli di frammenti di contenuto
* [Creare frammenti di contenuto](/help/assets/content-fragments/content-fragments.md) - Documentazione tecnica sui frammenti di contenuto
* [Query del contenuto con GraphQL](/help/assets/content-fragments/graphql-api-content-fragments.md) - Documentazione tecnica sull’API GraphQL

<!-- HM-Links
* [Introduction to the Architecture of Adobe Experience Manager as a Cloud Service](/help/overview/architecture.md) - A complete overview of AEM's architecture
* [Headless Getting Started Guide](/help/implementing/developing/headless/introduction.md#getting-started) - A quick introduction to AEM's headless features for users already knowledgeable of AEM.
* [Create Content Fragment Models](/help/assets/content-fragments/content-fragments-models.md) - Technical documentation on Content Fragment Models
* [Create Content Fragments](/help/assets/content-fragments/content-fragments.md) - Technical documentation on Content Fragments
* [Query content with GraphQL](/help/assets/content-fragments/graphql-api-content-fragments.md) - Technical documentation on the GraphQL API

-->