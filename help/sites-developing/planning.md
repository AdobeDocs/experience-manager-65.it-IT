---
title: Pianificazione
seo-title: Pianificazione
description: Cosa devi sapere per pianificare il test
seo-description: Cosa devi sapere per pianificare il test
uuid: 29b1127a-da85-46ed-98e7-1c983eb40cfe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 12268c43-93f9-42c1-8dd7-f17f9ae2219b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 0%

---


# Pianificazione{#planning}

In questo documento viene descritto ciò che è necessario sapere per pianificare il test. Prima di eseguire i test è inoltre necessario rispondere alle seguenti domande:

* [Quali ambienti di test saranno necessari?](/help/sites-developing/test-environments.md)
* [Definizione dei casi di test](/help/sites-developing/test-cases.md)
* [Test - quando e con chi?](/help/sites-developing/when-who.md)

## Prima di iniziare {#before-you-start}

Prima di iniziare con l’analisi e la definizione effettive dei test, controllate le informazioni seguenti:

**AEM Architettura** - Vedere Concetti di base per presentarsi all&#39;architettura e ai principi di base di AEM.

**Documentazione**  - Per ulteriori informazioni, vedere le sezioni della documentazione o gli articoli How To.

**Principi di base dei test** - È necessario essere consapevoli dei principi di base dei test software e della garanzia della qualità. Preferibilmente dovreste avere esperienza nel testing di progetti.

Ci sono molti siti web, libri e corsi che si occupano di tali principi e quindi non saranno trattati nei dettagli in questo documento.

**Ipotesi da evitare**  - Il più grande presupposto (fatto regolarmente) è che il tuo sito web avrà bisogno di servire milioni di richieste ogni giorno. In alcune circostanze ciò può essere vero, ma non si può presupporre.

Anche se i numeri futuri non possono essere previsti con una precisione del 100%, osservare il sito esistente e il traffico sperimentato darà una buona indicazione. È quindi possibile fare delle stime in base al fattore in base al quale si prevede / si spera che il traffico aumenterà.

**Impegno per la Qualità**  - È di fondamentale importanza che chiunque effettui test rimanga neutrale e riferisca semplicemente i risultati dei test effettuati.

È responsabilità del Project Manager decidere e avviare azioni in base ai risultati.

**Diventa Coinvolto**  - Anche se è responsabilità del Project Manager garantire che tutte le parti siano pienamente coinvolte a qualsiasi riunione (stato, workshop, ecc.), è necessario anche cercare di essere coinvolti il prima possibile nel ciclo di progetto, compresi i processi di raccolta delle informazioni e analisi dei requisiti.

**Coinvolgi il cliente** - Su un tema simile, cerca di coinvolgere il cliente (ove possibile) nella definizione dei casi di test e del piano.

## Tipi di test {#types-of-tests}

Esistono diverse classificazioni standard di test che possono essere utilizzate per il test di un progetto AEM. È necessario avere familiarità con questi per decidere quale utilizzare:

>[!NOTE]
>
>Questi sono elencati nel loro ordine cronologico di applicazione.

**Prove**  di unità - Test (solitamente) effettuati dal team di sviluppo per garantire che i singoli elementi funzionino correttamente, anche se in modo isolato.

**Prove**  di integrazione - Moduli di test se combinati. Questi test vengono eseguiti dopo il testing di unità, ma prima del test di sistema.

**Test**  di fumo - Questi sono test veloci e sporchi utilizzati per dimostrare che il software è in esecuzione e le funzionalità di alto livello sono disponibili. I dettagli non vengono testati.

**Test**  funzionali - Utilizzati per testare la funzionalità del software. Una serie di test sarà progettata per coprire tutti i dettagli funzionali, con input sia previsto che imprevisti e/o errati.

Le prove in scatola nera sono prove funzionali di un&#39;unità/componente/modulo completo, eseguite senza conoscere il funzionamento interno dell&#39;elemento in questione.

**Test**  di sistema: questi consentono di testare l&#39;intero sistema una volta che è stato completamente integrato e installato su una piattaforma adeguata.

La funzionalità viene verificata a livello di scatola nera.

**Test**  delle prestazioni - I test delle prestazioni sono fondamentali quando si esegue il test AEM.

Sono utilizzati per illustrare le prestazioni in condizioni diverse:

* Normale

   Condizioni che il sito sperimenterà per dire il 90% del tempo. Ad esempio, quando solo una parte degli autori utilizza il sistema.

* Picco

   Condizioni che saranno sperimentate per un periodo di tempo proporzionalmente breve a causa di circostanze particolari; ad esempio, quando tutti gli autori utilizzano il sistema in modo simultaneo o quando viene pubblicato nuovo contenuto e un numero crescente di visitatori visualizza il sito.

* Estremo

   Può essere usato per emulare le previsioni di prestazioni quando nuovi contenuti estremamente interessanti vengono pubblicati sul sito Web. Poi può essere visto un picco estremo - anche se questo potrebbe non essere sempre del tutto prevedibile.

   Queste circostanze vengono a volte visualizzate quando i biglietti per eventi specifici sono disponibili, o un sito web molto atteso viene pubblicato per la prima volta.

I risultati vengono quindi utilizzati per sintonizzare l’applicazione.

**Test**  di stress - I test di stress vengono eseguiti per confermare il comportamento di un componente o di un’applicazione in condizioni estreme. In particolare, questi test vengono utilizzati per mostrare il deterioramento del comportamento, quando l&#39;elemento avrà esito negativo e come.

**Prove**  di regressione - I test di regressione vengono utilizzati per confermare che la funzionalità già provata in una versione precedente del software è ancora in funzione correttamente.

I test di regressione sono buoni candidati per l&#39;automazione (se possibile) per garantire che possano essere ripetuti rapidamente e coerentemente.

**Test**  di accettazione - I test di accettazione sono una categoria speciale in quanto sono utilizzati per indicare l&#39;accettazione del progetto da parte del cliente.

L&#39;elenco dei test di accettazione può contenere una combinazione di test delle varie categorie sopra elencate e viene selezionato per verificare che il progetto soddisfi i requisiti del cliente

Per ulteriori informazioni, vedere [Accettazione e disconnessione](/help/sites-developing/acceptance-signoff.md).

## Guida introduttiva {#getting-started}

Prima di iniziare il test case e il piano di test dettagliati puoi:

**Definizione degli obiettivi**  - Definite gli obiettivi di alto livello da utilizzare come punto di partenza per l&#39;ottimizzazione man mano che i test procedono. Si desidera:

* Verificate la funzionalità in base alla specifica dettagliata dei requisiti.
* Prestazioni del test in base alle [Metriche di destinazione](/help/managing/best-practices-further-reference.md#key-performance-indicators-and-target-metrics).

tra gli altri.

**Raccogliere le statistiche sul traffico dal sito Web**  esistente - Queste informazioni possono essere estratte dai file di registro - vedere Monitoraggio delle prestazioni per ulteriori dettagli.

Queste cifre indicheranno il traffico corrente (volume e diffusione) sul sito Web esistente e potranno essere utilizzate per costituire un punto di base per il nuovo sito.

**Raccolta di statistiche sul traffico da siti**  esterni - Se possibile è possibile cercare di raccogliere statistiche sul traffico da altri siti Web per il confronto, ma queste cifre non vengono sempre pubblicate.

**Conferma metriche**  Target: le metriche vengono utilizzate per definire le misurazioni quantitative per la qualità del sito Web, in quanto rappresentano gli obiettivi prestazionali da raggiungere.

Devono essere definiti all&#39;inizio del progetto insieme al cliente. Per ulteriori informazioni, vedere [Metriche di destinazione](/help/sites-developing/planning.md).
