---
title: Misurare e migliorare l’efficacia e la conversione dei moduli
description: AEM Forms si integra con le soluzioni Adobe Target e Adobe Analytics che consentono di misurare e migliorare le prestazioni e il tasso di conversione dei moduli.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
docset: aem65
exl-id: 4f45ad22-611b-4b4f-8e89-cb64a122b70a
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 0%

---

# Misurare e migliorare l’efficacia e la conversione dei moduli{#measure-and-improve-effectiveness-and-conversion-of-forms}

## La sfida {#the-challenge-br}

Le organizzazioni stanno rendendo sempre più autonomi e incoraggiano i propri clienti a negoziare utilizzando i self-service digitali su più canali. Tuttavia, in assenza di un meccanismo di feedback individuale, diventa difficile misurare il successo e sperimentare con i moduli digitali per migliorare l’esperienza del cliente e aumentare le conversioni.

Per massimizzare il ROI, le organizzazioni devono monitorare il modo in cui i clienti interagiscono con i servizi e sperimentare con i loro artefatti digitali (moduli) per migliorare l’esperienza del cliente. Per misurare il successo e definire una strategia di miglioramento, le organizzazioni hanno bisogno di risposte a domande come:

* Quanti clienti hanno provato ad accedere o a effettuare transazioni con i moduli?
* Quanti di loro hanno completato correttamente la transazione?
* Quanti di loro hanno abbandonato il modulo?
* Quali sono le aree problematiche in cui i clienti si trovano ad affrontare i problemi?
* Quali cambiamenti introduco e come posso verificare quale causa ha una conversione migliore?

## La soluzione {#the-solution}

AEM Forms si integra con [Adobe Marketing Cloud](https://www.adobe.com/marketing-cloud.html) soluzioni - [Adobe Analytics](https://www.adobe.com/marketing-cloud/web-analytics.html) e [Adobe Target](https://www.adobe.com/marketing-cloud/testing-targeting.html) : consente di monitorare e analizzare le prestazioni dei moduli e di sperimentare e identificare l’esperienza che porta a un migliore tasso di conversione.

## Il flusso di lavoro {#the-workflow}

Passiamo ora ai dettagli su come misurare le prestazioni e migliorare i tassi di conversione per i moduli.

### Pubblico di destinazione {#target-audience}

* Utenti e analisti aziendali responsabili delle strategie di marketing e del successo
* Personale IT che si occupa della configurazione e della manutenzione dell&#39;infrastruttura e delle soluzioni

### Componenti e funzioni di AEM Forms interessati {#aem-forms-components-and-features-involved}

* Moduli adattivi
* Integrazione con Adobe Analytics per raccogliere, organizzare e segnalare le interazioni dei clienti con i moduli adattivi
* Integrazione con Adobe Target per eseguire test A/B per i moduli adattivi

### Presupposti {#assumptions}

* Hai già un account Adobe Marketing Cloud e sei registrato per le soluzioni Analytics e Target.
* Disponi di un modulo adattivo pubblicato a cui i clienti possono accedere.

### Passaggi del flusso di lavoro {#workflow-steps}

#### Passaggio 1: configurare Analytics e Target in AEM Forms  {#step-configure-analytics-and-target-in-aem-forms-br}

**Configurare Analytics**

Per ottenere informazioni approfondite sulle interazioni dei clienti con i moduli, devi prima configurare Analytics in AEM Forms. Effettua le seguenti operazioni:

1. Creare una suite di rapporti in Adobe Analytics
1. Creare la configurazione del servizio cloud in AEM
1. Creare un framework per servizi cloud in AEM
1. Configurare il servizio di configurazione di AEM Forms Analytics nell’AEM
1. Abilitare l’analisi sul modulo in AEM

Per i passaggi dettagliati, consulta [Configurazione di analisi e rapporti per moduli adattivi](../../forms/using/configure-analytics-forms-documents.md).

**Configurare Target**

Per creare ed eseguire test A/B per i moduli adattivi, configura Target in AEM Forms come descritto in [Configurare e integrare Target in AEM Forms](../../forms/using/ab-testing-adaptive-forms.md#p-set-up-and-integrate-target-in-aem-forms-p).

#### Passaggio 2: visualizzare il rapporto di analisi {#step-view-analytics-report-br}

Man mano che i tuoi clienti accedono e interagiscono con i moduli su cui hai abilitato Analytics, le loro interazioni vengono acquisite in database di Analytics altamente sicuri. I database sono segmentati dai client e accessibili tramite connessioni sicure.

Puoi visualizzare un rapporto dall’AEM per i moduli abilitati per l’analisi e analizzare i dati. Per visualizzare il rapporto:

1. Nel server AEM, passa a **Forms > Forms e documenti**.
1. Selezionare la maschera per la quale si desidera creare il rapporto di analisi.
1. Fai clic sull’icona Rapporti di Analytics. Il report viene visualizzato.

Esaminiamo i punti dati che Analytics raccoglie e segnala per i moduli.

**rapporto di Forms analytics**

Il rapporto di Analytics per i moduli adattivi acquisisce i seguenti indicatori prestazioni chiave (KPI, Key Performance Indicators) a livello di modulo:

* **Tempo medio di riempimento**: tempo medio impiegato per la compilazione del modulo
* **Impression**: numero di volte in cui il modulo è apparso nei risultati di ricerca

* **Rappresentazioni**: numero di volte in cui il modulo è stato renderizzato o aperto
* **Bozze**: numero di volte in cui il modulo è stato salvato come bozza

* **Invii**: numero di volte in cui il modulo è stato inviato
* **Interrompi**: numero di volte in cui gli utenti sono rimasti senza completare il modulo
* **Visite/Invii**: rapporto delle visite per invio

Inoltre, puoi ottenere i seguenti dettagli su ciascun pannello nel modulo:

* **Ora**: tempo medio (secondi) trascorso sul pannello e sui relativi campi

* **Errore**: numero di errori riscontrati nel pannello e nei relativi campi per 1000 rappresentazioni di moduli

* **Aiuto**: numero di volte in cui gli utenti hanno effettuato l’accesso alla guida contestuale per il pannello e i relativi campi per 1000 rappresentazioni di moduli

![Un report di analisi di esempio per un modulo adattivo](assets/summary-report.png)

Per ulteriori dettagli sui rapporti di Forms Analytics, vedi [Visualizzazione e comprensione dei rapporti di AEM Forms Analytics](../../forms/using/view-understand-aem-forms-analytics-reports.md).

>[!NOTE]
>
>Puoi visualizzare rapporti dettagliati e ottenere informazioni più approfondite sui tuoi clienti e sulle loro interazioni con i moduli dal tuo account Analytics su Adobe Marketing Cloud.

#### Passaggio 3: analizzare i punti dati {#step-analyze-data-points}

In questo passaggio verranno analizzati i punti dati nel rapporto di Analytics e verranno dedotte le prestazioni del modulo. Se non soddisfa i KPI di successo, verranno create ipotesi basate sui dati e verranno trovate possibili soluzioni per risolvere i problemi. Ad esempio:

* Se il tempo medio di compilazione del modulo è superiore alle aspettative, è possibile che il modulo sia complesso da comprendere per i clienti, che non utilizzi terminologie standard, che sia troppo lungo e così via. In questo caso, potrebbe essere utile semplificare la struttura e i campi del modulo, rielaborare la struttura del modulo, ridurre la lunghezza del modulo o aggiungere descrizioni ed esempi di aiuto per i campi modulo non standard.
* Se i dati indicano che la maggior parte dei clienti accede all’Aiuto per un pannello di modulo, è evidente che i clienti non sanno esattamente quali informazioni compilare. È possibile utilizzare una terminologia alternativa o aggiungere alcuni input di esempio e una descrizione dell’Aiuto per tale pannello.
* Se il tasso di interruzione o abbandono per un modulo è superiore al previsto, è possibile che il rendering del modulo richieda molto tempo, che i clienti stiano inavvertitamente effettuando l’arrivo o che il modulo sia troppo complicato. In questo caso, è possibile ottimizzare la descrizione del modulo visualizzata nei risultati della ricerca, semplificare il modulo, ottimizzarlo per velocizzarne il caricamento e così via.

Dopo aver analizzato questi punti di dati e aver raggiunto un’ipotesi, apporta le modifiche necessarie nel modulo.

#### Passaggio 4: Convalidare l’analisi e le correzioni {#step-validate-your-analysis-and-fixes}

In questo passaggio verranno convalidate le modifiche apportate nel modulo e verrà verificato se influiscono sul tasso di conversione.

**Eseguire un test A/B**

L’integrazione di AEM Forms con Target consente la creazione di test A/B per i moduli adattivi. Nei test A/B, puoi presentare in modo casuale ai clienti diverse esperienze di un modulo in tempo reale, per sapere quale esperienza funziona meglio o causa più conversioni. Una volta che disponi di dati significativi che indicano che un’esperienza offre una conversione migliore rispetto all’altra, puoi dichiararla vincitrice e, in futuro, diventa l’esperienza predefinita visibile a tutti i clienti.

Per ulteriori informazioni sulla creazione di un test A/B per un modulo adattivo, consulta [Test A/B dei moduli adattivi](../../forms/using/ab-testing-adaptive-forms.md).

![Un report riepilogativo di esempio di test A/B per un modulo adattivo](assets/ab-test-report-4.png)

## Best practice {#best-practices}

Le vere best practice sono quelle che ti identifichi mentre esegui questo flusso di lavoro. Sono specifici per l’ambiente e i requisiti aziendali. Acquisisci i tuoi insegnamenti tramite il flusso di lavoro e documentali come best practice.

Di seguito sono riportati alcuni consigli sulla progettazione di moduli e sull’esecuzione di test A/B:

**Progettazione Forms**

* Mantenere il modulo semplice, breve e facile da navigare. Utilizza suggerimenti direzionali per la navigazione.
* Utilizza terminologie standard o comuni per i campi modulo.
* Spiega il campo e l’input richiesto, con esempi o aiuto, in cui gli utenti possono confondersi.
* Se possibile, convalida i dati immessi dall&#39;utente durante la digitazione per evitare errori durante l&#39;invio del modulo.
* Ottimizza i layout per desktop e dispositivi mobili.
* Compila automaticamente le informazioni per gli utenti noti.

**Test A/B**

* Crea un’ipotesi e identifica le metriche di successo prima di eseguire il test A/B.
* Effettua variazioni minime (idealmente una alla volta) nell’esperienza alternativa per sapere cosa ha interessato il tasso di conversione.
* Eseguire frequenti test per eliminare le inefficienze.
