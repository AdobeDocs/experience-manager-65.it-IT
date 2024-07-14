---
title: Pianificazione
description: Scopri cosa devi sapere per pianificare il test di Adobe Experience Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
exl-id: ed662279-0679-4ba3-b744-6649fb8dda17
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 0%

---

# Pianificazione{#planning}

Questo documento descrive cosa devi sapere per pianificare il test. Inoltre, è necessario rispondere alle seguenti domande prima di eseguire i test:

* [Quali ambienti di test saranno necessari?](/help/sites-developing/test-environments.md)
* [Definizione dei test case](/help/sites-developing/test-cases.md)
* [Test: quando e con chi?](/help/sites-developing/when-who.md)

## Prima di iniziare {#before-you-start}

Prima di iniziare con l&#39;analisi e la definizione effettive dei test, esaminare le informazioni riportate di seguito.

**Architettura AEM** - Consulta Concetti di base per conoscere l&#39;architettura e i principi di base dell&#39;AEM.

**Documentazione** - Per ulteriori informazioni, consulta una delle sezioni della documentazione o gli articoli Come fare.

**Principi di base dei test** - È necessario conoscere i principi di base dei test software e della garanzia di qualità. È preferibile che tu abbia esperienza con i progetti di test.

Ci sono molti siti web, libri e corsi che trattano di tali principi e quindi non saranno trattati in dettaglio in questo documento.

**Presupposti da evitare** - Il presupposto più importante è che il sito Web debba soddisfare milioni di richieste ogni giorno. In determinate circostanze può essere vero, ma non può essere presunto.

Anche se i numeri futuri non possono essere previsti con una precisione del 100%, l’osservazione del sito esistente e del traffico esperienza fornirà una buona indicazione. Puoi quindi effettuare delle stime in base al fattore previsto/previsto di aumento del traffico.

**Impegno per la qualità** - È di fondamentale importanza che tutti gli utenti che eseguono i test rimangano neutrali e riportino semplicemente i risultati dei test eseguiti.

È responsabilità del Project Manager decidere e avviare azioni in base ai risultati.

**Partecipa** - Anche se è responsabilità del Project Manager assicurarsi che tutte le parti siano pienamente coinvolte in tutte le riunioni (stato, workshop e così via), è necessario cercare di partecipare il prima possibile al ciclo del progetto, inclusi i processi di raccolta delle informazioni e di analisi dei requisiti.

**Coinvolgi il cliente**. Su un tema simile, prova a coinvolgere il cliente (ove possibile) durante la definizione dei test case e del piano.

## Tipi di test {#types-of-tests}

Esistono varie classificazioni standard dei test che sono appropriate per l&#39;uso quando si esegue un test su un progetto AEM. Dovresti avere familiarità con questi elementi per decidere quale usare:

>[!NOTE]
>
>Questi sono elencati nel loro ordine cronologico di applicazione.

**Test unità** - Test eseguiti (in genere) dal team di sviluppo per verificare il corretto funzionamento dei singoli elementi, anche se isolati.

**Integration test** - Moduli di test quando combinati. Questi test vengono eseguiti dopo l&#39;esecuzione dell&#39;unit test, ma prima dell&#39;esecuzione del test del sistema.

**Test antifumo** - Si tratta di test rapidi e sporchi utilizzati per dimostrare che il software è in esecuzione e che sono disponibili funzionalità di alto livello. I dettagli non vengono testati.

**Test funzionali**: utilizzati per testare la funzionalità del software. Una serie di prove sarà concepita per coprire tutti i dettagli funzionali, con dati sia previsti che imprevisti e/o errati.

I test Black-box sono test funzionali di un&#39;unità/componente/modulo completo, eseguiti senza conoscere il funzionamento interno dell&#39;elemento in questione.

**Test di sistema**: questi test consentono di eseguire il test dell&#39;intero sistema una volta che è stato completamente integrato e installato su una piattaforma appropriata.

Testano la funzionalità su base black-box.

**Test delle prestazioni** - I test delle prestazioni sono fondamentali per il test dell&#39;AEM.

Vengono utilizzati per illustrare le prestazioni in condizioni diverse:

* Normale

  Condizioni in cui si troverà il sito, ad esempio, il 90% del tempo. Ad esempio, quando solo una parte degli autori utilizza il sistema.

* Picco

  Condizioni che si verificheranno per un periodo di tempo proporzionalmente breve a causa di circostanze particolari; ad esempio, quando tutti gli autori utilizzano il sistema contemporaneamente o quando vengono pubblicati nuovi contenuti e un numero maggiore di visitatori visualizza il sito.

* Estrema

  Può essere utilizzato per emulare la previsione delle prestazioni quando vengono pubblicati nuovi contenuti estremamente interessanti sul sito web. Quindi può essere visto un picco estremo - anche se questo può non essere sempre completamente prevedibile.

  Queste circostanze si verificano talvolta quando vengono messi a disposizione biglietti per eventi specifici o quando viene pubblicato per la prima volta un sito web molto atteso.

I risultati vengono quindi utilizzati per ottimizzare l’applicazione.

**Stress test**: gli stress test vengono eseguiti per confermare il comportamento di un componente o di un&#39;applicazione in condizioni estreme. In particolare, questi test vengono utilizzati per mostrare come il comportamento si deteriora, quando l’elemento avrà esito negativo e come.

**Test di regressione** - I test di regressione vengono utilizzati per confermare che le funzionalità già verificate in una versione precedente del software funzionano ancora correttamente.

I test di regressione sono buoni candidati per l&#39;automazione (se possibile) per garantire che possano essere ripetuti in modo rapido e coerente.

**Test di accettazione** - I test di accettazione sono una categoria speciale in quanto vengono utilizzati per indicare l&#39;accettazione del progetto da parte del cliente.

L&#39;elenco dei test di accettazione può contenere una combinazione di test delle varie categorie sopra indicate e viene selezionato per verificare che il progetto soddisfi i requisiti del cliente

Per ulteriori dettagli, vedere [Accettazione e disconnessione](/help/sites-developing/acceptance-signoff.md).

## Guida introduttiva {#getting-started}

Prima di iniziare a utilizzare i test case e il piano di test dettagliati, è possibile:

**Definisci gli obiettivi**: definisci gli obiettivi di alto livello da usare come punto di partenza per l&#39;ottimizzazione man mano che il test procede. Si desidera:

* Testare la funzionalità in base alle specifiche dettagliate dei requisiti.
* Prestazioni di test in base alle [metriche di destinazione](/help/managing/best-practices-further-reference.md#key-performance-indicators-and-target-metrics).

tra gli altri.

**Raccogli statistiche sul traffico dal sito Web esistente**. Queste informazioni possono essere estratte dai file di registro. Per ulteriori dettagli, vedere Monitoraggio delle prestazioni.

Queste cifre forniranno un’indicazione del traffico attuale (volume e diffusione) sul sito web esistente e possono essere utilizzate per formare un punto di base per il nuovo sito web.

**Raccogliere le statistiche sul traffico da siti Web esterni** - Se possibile, provare a raccogliere le statistiche sul traffico da altri siti Web per il confronto, ma queste cifre non vengono sempre pubblicate.

**Conferma metriche di destinazione**: le metriche vengono utilizzate per definire misurazioni quantitative per la qualità del sito Web, in quanto rappresentano gli obiettivi di prestazioni da raggiungere.

Devono essere definite all’inizio del progetto, insieme al cliente. Per ulteriori informazioni, vedere [Metriche di destinazione](/help/sites-developing/planning.md).
