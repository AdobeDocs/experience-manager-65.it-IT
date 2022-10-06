---
title: Misurare e migliorare l’efficacia e la conversione dei moduli
seo-title: Measure and improve effectiveness and conversion of forms
description: AEM Forms si integra con le soluzioni Adobe Target e Adobe Analytics che consentono di misurare e migliorare le prestazioni e il tasso di conversione dei moduli.
seo-description: AEM Forms integrates with Adobe Target and Adobe Analytics solutions that allows you to measure and improve the performance and conversion rate of your forms.
uuid: fd2f087c-39f5-457d-8b44-c3ec4400b3fc
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: a128877d-239c-4272-99c2-72d6486d5703
docset: aem65
exl-id: 4f45ad22-611b-4b4f-8e89-cb64a122b70a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1278'
ht-degree: 0%

---

# Misurare e migliorare l’efficacia e la conversione dei moduli{#measure-and-improve-effectiveness-and-conversion-of-forms}

## La sfida {#the-challenge-br}

Le organizzazioni stanno sempre più dando potere e incoraggiando i loro clienti a negoziare utilizzando i servizi di self-service digitali su più canali. Tuttavia, in assenza di un meccanismo di feedback uno a uno, diventa difficile misurare il successo e sperimentare i moduli digitali per migliorare la customer experience e aumentare le conversioni.

Per massimizzare il ROI, le organizzazioni devono monitorare il modo in cui i clienti interagiscono con i servizi e sperimentare con i propri artefatti digitali (moduli) per migliorare le esperienze dei clienti. Per misurare il successo e definire una strategia di miglioramento, le organizzazioni hanno bisogno di risposte a domande come:

* Quanti clienti hanno provato ad accedere o a negoziare con i moduli?
* Quanti di loro hanno completato con successo la transazione?
* Quanti di loro hanno abbandonato il modulo?
* Quali sono le aree problematiche in cui i clienti devono affrontare i problemi?
* Quali modifiche introduco e come posso verificare quale causa una conversione migliore?

## La soluzione {#the-solution}

AEM Forms si integra con [Adobe Marketing Cloud](https://www.adobe.com/marketing-cloud.html) soluzioni - [Adobe Analytics](https://www.adobe.com/marketing-cloud/web-analytics.html) e [Adobe Target](https://www.adobe.com/marketing-cloud/testing-targeting.html) - che consente di monitorare e analizzare le prestazioni dei moduli e di sperimentare e identificare l’esperienza che porta a un migliore tasso di conversione.

## Il flusso di lavoro {#the-workflow}

Passiamo ai dettagli su come misurare le prestazioni e migliorare i tassi di conversione per i moduli.

### Pubblico di destinazione {#target-audience}

* Utenti e analisti aziendali responsabili delle strategie di marketing e del successo
* Personale IT che si occupa della configurazione e della manutenzione dell&#39;infrastruttura e delle soluzioni

### Componenti e funzionalità di AEM Forms interessati {#aem-forms-components-and-features-involved}

* Moduli adattivi
* Integrazione con Adobe Analytics per raccogliere, organizzare e segnalare le interazioni dei clienti con i moduli adattivi
* Integrazione con Adobe Target per eseguire test A/B per i moduli adattivi

### Ipotesi {#assumptions}

* Hai già un account Adobe Marketing Cloud e ti sei registrato per le soluzioni Analytics e Target.
* È disponibile un modulo adattivo pubblicato a cui i clienti possono accedere.

### Passaggi del flusso di lavoro {#workflow-steps}

#### Passaggio 1: Configurare Analytics e Target in AEM Forms  {#step-configure-analytics-and-target-in-aem-forms-br}

**Configura Analytics**

Per ottenere informazioni approfondite sulle interazioni dei clienti con i moduli, devi prima configurare Analytics in AEM Forms. Esegui i seguenti passaggi:

1. Creare una suite di rapporti in Adobe Analytics
1. Creare la configurazione del servizio cloud in AEM
1. Crea framework di servizi cloud in AEM
1. Configurare il servizio di configurazione di AEM Forms Analytics in AEM
1. Abilitare l’analisi del modulo in AEM

Per i passaggi dettagliati vedi [Configurazione di analisi e rapporti per i moduli adattivi](../../forms/using/configure-analytics-forms-documents.md).

**Configurare Target**

Per creare ed eseguire test A/B per i moduli adattivi, configura Target in AEM Forms come descritto in [Configurazione e integrazione di Target in AEM Forms](../../forms/using/ab-testing-adaptive-forms.md#p-set-up-and-integrate-target-in-aem-forms-p).

#### Passaggio 2: Visualizzare il rapporto di analisi {#step-view-analytics-report-br}

Man mano che i clienti accedono e interagiscono con i moduli su cui hai abilitato Analytics, le loro interazioni vengono acquisite in database Analytics altamente protetti. I database sono segmentati dai client e accessibili tramite connessioni sicure.

È possibile visualizzare un rapporto dall’interno di AEM per i moduli abilitati per Analytics e analizzare i dati. Per visualizzare il rapporto:

1. Su AEM server, passa a **Forms > Forms e documenti**.
1. Selezionare il modulo per il quale si desidera visualizzare il rapporto di analisi.
1. Fai clic sull’icona Rapporti di Analytics . Viene visualizzato il rapporto.

Diamo un&#39;occhiata ai punti di dati che Analytics raccoglie e crea rapporti per i moduli.

**Rapporto di analisi Forms**

Il rapporto di analisi per i moduli adattivi acquisisce i seguenti indicatori prestazioni chiave (KPI, Key Performance Indicators) a livello di modulo:

* **Tempo medio di riempimento**: Tempo medio impiegato per compilare il modulo
* **Impressioni**: Numero di volte in cui il modulo è stato visualizzato nei risultati della ricerca

* **Rendering**: Numero di volte in cui è stato eseguito il rendering o l’apertura del modulo
* **Bozze**: Numero di volte in cui il modulo è stato salvato come bozza

* **Invii**: Numero di volte in cui il modulo è stato inviato
* **Interrompere**: Numero di volte in cui gli utenti rimangono senza compilare il modulo
* **Visite/Invii**: Rapporto di visite per presentazione

Inoltre, vengono visualizzati i seguenti dettagli su ciascun pannello del modulo:

* **Time**: Tempo medio trascorso (secondi) sul pannello e sui relativi campi

* **Errore**: Numero di errori riscontrati nel pannello e nei relativi campi per 1000 rappresentazioni dei moduli

* **Aiuto**: Numero di volte in cui gli utenti hanno effettuato l’accesso alla guida contestuale per il pannello e i relativi campi per 1000 rappresentazioni dei moduli

![Un esempio di rapporto di analisi per un modulo adattivo](assets/summary-report.png)

Per ulteriori dettagli sui rapporti di analisi dei moduli, consulta [Visualizzazione e comprensione dei rapporti di AEM Forms Analytics](../../forms/using/view-understand-aem-forms-analytics-reports.md).

>[!NOTE]
>
>Puoi visualizzare rapporti dettagliati e ottenere informazioni più approfondite sui clienti e sulle loro interazioni con i moduli dal tuo account Analytics su Adobe Marketing Cloud.

#### Passaggio 3: Analizzare i punti dati {#step-analyze-data-points}

In questo passaggio, analizzerai i punti dati nel rapporto di analisi e determinerai le prestazioni del modulo. Se non soddisfa i KPI di successo, puoi creare ipotesi basate sui dati e trovare possibili soluzioni per risolvere i problemi. Esempio:

* Se il tempo medio di compilazione del modulo è superiore alle aspettative, è possibile che il modulo sia complesso da comprendere, che il modulo non utilizzi terminologie standard, che il modulo sia troppo lungo e così via. In questo caso, è possibile semplificare la struttura del modulo e i campi, rielaborare la struttura del modulo, ridurre la lunghezza del modulo o aggiungere descrizioni ed esempi della guida per i campi modulo non standard.
* Se i dati indicano che la maggior parte dei clienti accede all’Aiuto per un pannello dei moduli, è evidente che i clienti sono perplessi sulle informazioni da compilare. È possibile utilizzare la terminologia alternativa o aggiungere alcuni input di esempio e una descrizione della guida per quel pannello.
* Se il tasso di interruzione o abbandono di un modulo è superiore a quello previsto, potrebbe essere dovuto al tempo di rendering del modulo, l’accesso del cliente al modulo è involontariamente intenzionale o è troppo complicato. In questo caso, è consigliabile ottimizzare la descrizione del modulo visualizzata nei risultati della ricerca, semplificare il modulo, ottimizzare il modulo per velocizzarne il caricamento e così via.

Una volta analizzati questi punti dati e arrivati a un&#39;ipotesi, apportare le modifiche necessarie nel modulo.

#### Passaggio 4: Convalida l&#39;analisi e le correzioni {#step-validate-your-analysis-and-fixes}

In questo passaggio, convalida le modifiche apportate al modulo e verifica se questo influisce sul tasso di conversione.

**Eseguire un test A/B**

L’integrazione di AEM Forms con Target consente di creare test A/B per i moduli adattivi. Nei test A/B, puoi presentare in modo casuale ai clienti esperienze diverse di un modulo in tempo reale per sapere quale esperienza funziona meglio o causa più conversioni. Una volta che disponi di dati significativi che indicano un’esperienza che offre una conversione migliore rispetto all’altra, puoi dichiarare che le esperienze sono vincenti e, andando avanti, diventa l’esperienza predefinita visibile a tutti i clienti.

Per ulteriori informazioni sulla creazione di un test A/B per un modulo adattivo, consulta [Test A/B dei moduli adattivi](../../forms/using/ab-testing-adaptive-forms.md).

![Un esempio di rapporto di riepilogo del test A/B per un modulo adattivo](assets/ab-test-report-4.png)

## Best practice {#best-practices}

Le best practice effettive sono quelle che ti identifichi durante l’esecuzione di questo flusso di lavoro. Sono esclusivi per il tuo ambiente e le tue esigenze. Acquisisci le informazioni attraverso il flusso di lavoro e documentale come best practice.

Alcune raccomandazioni sulla progettazione dei moduli e sull’esecuzione di test A/B sono le seguenti:

**Progettazione Forms**

* Mantenere il modulo semplice, breve e facile da navigare. Usa indicazioni direzionali per la navigazione.
* Utilizzare terminologie standard o comuni per i campi del modulo.
* Spiega il campo e l’input richiesto, con esempi o aiuto, in cui gli utenti possono confondersi.
* Convalida gli input degli utenti durante la digitazione, laddove possibile, per evitare errori durante l’invio del modulo.
* Ottimizza i layout per desktop e dispositivi mobili.
* Compilazione automatica delle informazioni per gli utenti noti.

**Test A/B**

* Crea un’ipotesi e identifica le metriche di successo prima di eseguire il test A/B.
* Fai minime variazioni (idealmente una alla volta) nell’esperienza alternativa per sapere cosa ha influenzato il tasso di conversione.
* Esegui frequenti test per eliminare le inefficienze.
