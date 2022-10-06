---
title: Pianificazione
seo-title: Planning
description: Informazioni necessarie per pianificare il test
seo-description: What you need to know to plan for your test
uuid: 29b1127a-da85-46ed-98e7-1c983eb40cfe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 12268c43-93f9-42c1-8dd7-f17f9ae2219b
exl-id: ed662279-0679-4ba3-b744-6649fb8dda17
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 0%

---

# Pianificazione{#planning}

Questo documento descrive cosa è necessario sapere per pianificare il test. Inoltre, è necessario rispondere a queste domande prima di eseguire i test:

* [Quali ambienti di test saranno necessari?](/help/sites-developing/test-environments.md)
* [Definizione dei casi di test](/help/sites-developing/test-cases.md)
* [Test - quando e con chi?](/help/sites-developing/when-who.md)

## Prima di iniziare {#before-you-start}

Prima di iniziare con l’analisi e la definizione effettive dei test, controlla le seguenti informazioni:

**Architettura AEM** - Vedere Concetti di base per presentarsi all&#39;architettura e ai principi di base di AEM.

**Documentazione** - Per ulteriori informazioni, vedere le sezioni della documentazione o gli articoli Come fare per .

**Principi di base delle prove** - È necessario essere consapevoli dei principi di base di Software Testing e Quality Assurance. Preferibilmente dovresti avere esperienza dei progetti di test.

Ci sono molti siti web, libri e corsi che si occupano di tali principi e quindi non saranno trattati in dettaglio in questo documento.

**Ipotesi di evitare** - Il più grande presupposto (fatto regolarmente) è che il tuo sito web dovrà soddisfare milioni di richieste ogni giorno. In alcune circostanze ciò può essere vero, ma non si può presumere.

Anche se i numeri futuri non possono essere previsti con precisione del 100%, l’osservazione del sito esistente e del traffico registrato darà una buona indicazione. È quindi possibile rendere le stime dipendenti dal fattore in base al quale si prevede / si spera che il traffico aumenti.

**Impegno per la qualità** - È di fondamentale importanza che chiunque effettui i test rimanga neutrale e riferisca semplicemente i risultati dei test effettuati.

È responsabilità del Project Manager decidere e avviare azioni in base ai risultati.

**Diventa coinvolto** - Anche se è responsabilità del Project Manager garantire che tutte le parti siano pienamente coinvolte in tutte le riunioni (stato, workshop, ecc.), è anche necessario cercare di partecipare il prima possibile al ciclo di progetto, inclusi i processi di raccolta delle informazioni e di analisi dei requisiti.

**Coinvolgere il cliente** - Su un tema simile, cerca di coinvolgere il cliente (ove possibile) quando definisci i casi di test e pianifica.

## Tipi di test {#types-of-tests}

Esistono varie classificazioni standard di test che sono appropriate per l’utilizzo durante il test di un progetto AEM. È necessario avere familiarità con questi per decidere quale utilizzare:

>[!NOTE]
>
>Questi sono elencati nel loro ordine cronologico di applicazione.

**Prove sulle unità** - Test (solitamente) effettuati dal team di sviluppo per garantire che i singoli elementi si comportino correttamente, anche se in modo isolato.

**Test di integrazione** - Prove i moduli se combinati. Questi test vengono eseguiti dopo il testing di unità, ma prima del test di sistema.

**Prove di fumo** - Si tratta di test rapidi e sporchi utilizzati per dimostrare che il software è in esecuzione e che sono disponibili funzionalità di alto livello. I dettagli non vengono testati.

**Test funzionali** - Utilizzati per testare la funzionalità del software. Una serie di test sarà progettata per coprire tutti i dettagli funzionali, con input sia previsto che inatteso e/o errato.

Le prove della scatola nera sono prove funzionali di un&#39;unità/componente/modulo completo, eseguite senza conoscere il funzionamento interno dell&#39;elemento in questione.

**Test di sistema** - Questi testano l&#39;intero sistema una volta che è stato completamente integrato e installato su una piattaforma adeguata.

Testano la funzionalità in base alla scatola nera.

**Test delle prestazioni** - I test di prestazione sono cruciali quando i test AEM.

Vengono utilizzati per illustrare le prestazioni in condizioni diverse:

* Normale

   Condizioni che il sito sperimenterà per esempio il 90% del tempo. Ad esempio, quando solo una parte degli autori utilizza il sistema.

* Picco

   Condizioni che saranno sperimentate per un periodo di tempo proporzionalmente breve a causa di circostanze particolari; ad esempio, quando tutti gli autori utilizzano contemporaneamente il sistema o quando vengono pubblicati nuovi contenuti e un numero maggiore di visitatori visualizza il sito.

* Estrema

   Può essere utilizzato per emulare le previsioni sulle prestazioni quando vengono pubblicati nuovi contenuti estremamente interessanti sul tuo sito web. Allora si può vedere un picco estremo - anche se questo potrebbe non essere sempre del tutto prevedibile.

   Queste circostanze si verificano a volte quando sono disponibili biglietti per eventi specifici, o quando per la prima volta viene pubblicato un sito web molto atteso.

I risultati vengono quindi utilizzati per ottimizzare l’applicazione.

**Test di stress** - Vengono eseguiti test di stress per confermare il funzionamento di un componente o di un&#39;applicazione in condizioni estreme. In particolare, questi test vengono utilizzati per mostrare il deterioramento del comportamento, quando l’elemento avrà esito negativo e come.

**Test di regressione** - I test di regressione vengono utilizzati per confermare che le funzionalità già comprovate in una versione precedente del software continuano a funzionare correttamente.

I test di regressione sono buoni candidati all&#39;automazione (se possibile) per garantire che possano essere ripetuti in modo rapido e coerente.

**Prove di accettazione** - I test di accettazione sono una categoria speciale in quanto sono utilizzati per indicare l&#39;accettazione del progetto da parte del cliente.

L&#39;elenco dei test di accettazione può contenere una combinazione di test delle varie categorie di cui sopra e viene selezionato per verificare che il progetto soddisfi i requisiti del cliente

Vedi [Accettazione e disconnessione](/help/sites-developing/acceptance-signoff.md) per ulteriori dettagli.

## Guida introduttiva {#getting-started}

Prima di iniziare con i casi di test e il piano di test dettagliati puoi effettuare le seguenti operazioni:

**Definire gli obiettivi** - Definisci gli obiettivi di alto livello da utilizzare come punto di partenza per l’ottimizzazione man mano che il test procede. Desideri:

* Verificare la funzionalità in base alla specifica dettagliata del requisito.
* Prestazioni del test in base alla [Metriche di Target](/help/managing/best-practices-further-reference.md#key-performance-indicators-and-target-metrics).

tra gli altri.

**Raccolta di statistiche sul traffico dal sito web esistente** - Queste informazioni possono essere estratte dai file di registro. Per ulteriori informazioni, consulta Monitoraggio delle prestazioni .

Questi dati indicheranno il traffico attuale (volume e diffusione) sul sito web esistente e possono essere utilizzati per costituire un punto di base per il nuovo sito web.

**Raccolta di statistiche sul traffico da siti web esterni** - Se possibile è possibile cercare di raccogliere statistiche sul traffico da altri siti web per il confronto, ma queste cifre non sono sempre pubblicate.

**Conferma delle metriche di Target** - Le metriche sono utilizzate per definire misurazioni quantitative per la qualità del sito web, in quanto rappresentano gli obiettivi prestazionali da raggiungere.

Devono essere definiti all&#39;inizio del progetto insieme al cliente. Vedi [Metriche di Target](/help/sites-developing/planning.md) per ulteriori informazioni.
