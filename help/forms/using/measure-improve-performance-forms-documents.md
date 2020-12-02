---
title: Misurazione e miglioramento dell'efficacia e della conversione dei moduli
seo-title: Misurazione e miglioramento dell'efficacia e della conversione dei moduli
description: ' AEM Forms si integra con  soluzioni Adobe Target e  Adobe Analytics che consentono di misurare e migliorare le prestazioni e il tasso di conversione dei moduli.'
seo-description: ' AEM Forms si integra con  soluzioni Adobe Target e  Adobe Analytics che consentono di misurare e migliorare le prestazioni e il tasso di conversione dei moduli.'
uuid: fd2f087c-39f5-457d-8b44-c3ec4400b3fc
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: a128877d-239c-4272-99c2-72d6486d5703
docset: aem65
translation-type: tm+mt
source-git-commit: befbdfd574949a7f7449b70a15480e7c105418fe
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 0%

---


# Misurazione e miglioramento dell&#39;efficacia e della conversione dei moduli{#measure-and-improve-effectiveness-and-conversion-of-forms}

## La sfida {#the-challenge-br}

Le organizzazioni stanno sempre più dando potere e incoraggiando i loro clienti a commercializzare utilizzando i servizi auto digitali su più canali. Tuttavia, in assenza di un meccanismo di feedback uno-a-uno, diventa difficile misurare il successo e sperimentare i moduli digitali per migliorare l&#39;esperienza dei clienti e aumentare le conversioni.

Per massimizzare il ROI, le organizzazioni devono monitorare il modo in cui i clienti interagiscono con i servizi e sperimentare i loro artifact digitali (moduli) per migliorare l&#39;esperienza dei clienti. Per misurare il successo e definire una strategia di miglioramento, le organizzazioni devono rispondere a domande come:

* Quanti clienti hanno provato ad accedere o a gestire i moduli?
* Quanti di essi hanno completato con successo la transazione?
* Quanti di loro hanno abbandonato il modulo?
* Quali sono le aree problematiche in cui i clienti si trovano ad affrontare problemi?
* Quali modifiche vengono apportate e come si verifica la causa di una conversione migliore?

## La soluzione {#the-solution}

 AEM Forms si integra con soluzioni [Adobe Marketing Cloud](https://www.adobe.com/marketing-cloud.html) - [ Adobe Analytics](https://www.adobe.com/marketing-cloud/web-analytics.html) e [ Adobe Target](https://www.adobe.com/marketing-cloud/testing-targeting.html) - che possono aiutarti a monitorare e analizzare le prestazioni dei moduli e consentirti di sperimentare e identificare l&#39;esperienza che porta a un migliore tasso di conversione.

## Flusso di lavoro {#the-workflow}

Analizziamo i dettagli di come misurare le prestazioni e migliorare i tassi di conversione per i moduli.

### Destinatari {#target-audience}

* Utenti e analisti aziendali responsabili di strategie di marketing e di successo
* Personale IT che si occupa della configurazione e manutenzione dell&#39;infrastruttura e delle soluzioni

###  componenti e funzionalità di AEM Forms coinvolti {#aem-forms-components-and-features-involved}

* Moduli adattivi
* Integrazione con  Adobe Analytics per raccogliere, organizzare e segnalare le interazioni dei clienti con i moduli adattivi
* Integrazione con  Adobe Target per eseguire test A/B per i moduli adattivi

### Ipotesi {#assumptions}

* Hai già un account Adobe Marketing Cloud e ti sei registrato per le soluzioni Analytics e Target.
* È disponibile un modulo adattivo pubblicato a cui i clienti possono accedere.

### Passaggi del flusso di lavoro {#workflow-steps}

#### Passaggio 1: Configurare Analytics e Target in  AEM Forms {#step-configure-analytics-and-target-in-aem-forms-br}

**Configura Analytics**

Per ottenere informazioni approfondite sulle interazioni dei clienti con i moduli, è innanzitutto necessario configurare Analytics in  AEM Forms. Effettuate le seguenti operazioni:

1. Creare una suite di rapporti in  Adobe Analytics
1. Crea configurazione del servizio cloud in AEM
1. Crea framework di servizi cloud in AEM
1. Configurare  servizio di configurazione AEM Forms Analytics in AEM
1. Abilitare l&#39;analisi del modulo in AEM

Per i passaggi dettagliati, vedere [Configurazione di analisi e rapporti per i moduli adattivi](../../forms/using/configure-analytics-forms-documents.md).

**Configurare Target**

Per creare ed eseguire test A/B per i moduli adattivi, configurare Target in  AEM Forms come descritto in [Configurare e integrare Target in  AEM Forms](../../forms/using/ab-testing-adaptive-forms.md#p-set-up-and-integrate-target-in-aem-forms-p).

#### Passaggio 2: Visualizza report di analisi {#step-view-analytics-report-br}

Quando i clienti accedono e interagiscono con i moduli su cui hai attivato Analytics, le loro interazioni vengono acquisite in database Analytics altamente protetti. I database sono segmentati dai client e accessibili tramite connessioni sicure.

È possibile visualizzare un rapporto dall&#39;interno AEM per i moduli abilitati per l&#39;analisi e analizzare i dati. Per visualizzare il rapporto:

1. Sul AEM server, andate a **Forms > Forms &amp; Documents**.
1. Selezionare il modulo per il quale si desidera visualizzare il rapporto di analisi.
1. Fate clic sull&#39;icona Rapporti di Analytics. Il rapporto viene visualizzato.

Esaminiamo i punti dati raccolti e i rapporti di Analytics per i moduli.

**Report di analisi Forms**

Il rapporto di analisi per i moduli adattivi acquisisce i seguenti indicatori prestazioni chiave (KPI) a livello di modulo:

* **Tempo** medio di riempimento: Tempo medio impiegato per compilare il modulo
* **Impressioni**: Numero di volte in cui il modulo è stato visualizzato nei risultati della ricerca

* **Rappresentazioni**: Numero di volte in cui è stato eseguito il rendering o l&#39;apertura del modulo
* **Bozze**: Numero di volte in cui il modulo è stato salvato come bozza

* **Invii**: Numero di volte in cui il modulo è stato inviato
* **Interrompi**: Numero di volte che gli utenti restano senza compilare il modulo
* **Visite/Invii**: Rapporto di visite per presentazione

Inoltre, vengono forniti i seguenti dettagli su ciascun pannello del modulo:

* **Ora**: Tempo medio trascorso (secondi) nel pannello e nei relativi campi

* **Errore**: Numero di errori riscontrati nel pannello e nei relativi campi per 1000 rappresentazioni dei moduli

* **Aiuto**: Numero di volte in cui gli utenti accedevano alla guida contestuale del pannello e dei relativi campi per 1000 rappresentazioni dei moduli

![Report di analisi di esempio per un modulo adattivo](assets/summary-report.png)

Per ulteriori dettagli sui report di analisi dei moduli, vedere [Visualizzazione e comprensione  report di analisi AEM Forms](../../forms/using/view-understand-aem-forms-analytics-reports.md).

>[!NOTE]
>
>Puoi visualizzare rapporti dettagliati e ottenere informazioni più approfondite sui clienti e sulle loro interazioni con i moduli dall&#39;account Analytics su Adobe Marketing Cloud.

#### Passaggio 3: Analizzare i punti dati {#step-analyze-data-points}

In questo passaggio, si analizzeranno i punti dati nel report di analisi e si noterà le prestazioni del modulo. Se non soddisfa i KPI di successo, verranno create ipotesi, basate sui dati, e verranno trovate possibili soluzioni per risolvere i problemi. Esempio:

* Se il tempo medio di compilazione del modulo è superiore alle aspettative, è possibile che il modulo sia complesso per consentire agli utenti di comprenderlo, che il modulo non utilizzi terminologie standard, che il modulo sia troppo lungo e così via. In questo caso, potrebbe essere necessario semplificare la struttura del modulo e i campi, rielaborare la struttura del modulo, ridurre la lunghezza del modulo o aggiungere descrizioni ed esempi di aiuto per i campi modulo non standard.
* Se i dati indicano che la maggior parte dei clienti accede all’Aiuto per un pannello di moduli, è evidente che i clienti sono perplessi sulle informazioni da compilare. È possibile utilizzare una terminologia alternativa o aggiungere alcuni input di esempio e una descrizione della guida per tale pannello.
* Se il tasso di interruzione o di abbandono di un modulo è superiore a quello previsto, il rendering del modulo potrebbe richiedere molto tempo, l&#39;utente atterrerà inavvertitamente sul modulo o lo sarà troppo complicato. In questo caso, è possibile ottimizzare la descrizione del modulo visualizzata nei risultati della ricerca, semplificare il modulo, ottimizzare il modulo per velocizzare il caricamento e così via.

Una volta analizzati questi punti dati e arrivati a un&#39;ipotesi, apportare le modifiche necessarie nel modulo.

#### Passaggio 4: Convalida dell&#39;analisi e correzioni {#step-validate-your-analysis-and-fixes}

In questo passaggio sarà possibile convalidare le modifiche apportate nel modulo e verificare se influiscono sul tasso di conversione.

**Eseguire un test A/B**

L&#39;integrazione di  AEM Forms con Target consente di creare test A/B per i moduli adattivi. Nei test A/B, potete presentare in tempo reale ai clienti diverse esperienze di un modulo per sapere quale funziona meglio o genera più conversioni. Una volta ottenuti dati significativi che indicano un&#39;esperienza di conversione migliore dell&#39;altra, potete dichiarare che le esperienze sono vincenti e, andando avanti, diventerà l&#39;esperienza predefinita visibile a tutti i clienti.

Per ulteriori informazioni sulla creazione di un test A/B per un modulo adattivo, vedere [Test A/B dei moduli adattivi](../../forms/using/ab-testing-adaptive-forms.md).

![Un esempio di rapporto sintetico del test A/B per un modulo adattivo](assets/ab-test-report-4.png)

## Best practice {#best-practices}

Le best practice effettive sono quelle che ti identifichi mentre esegui questo flusso di lavoro. Sono esclusivi per il tuo ambiente e i tuoi requisiti. Acquisite le informazioni nel flusso di lavoro e documentatele come best practice.

Alcune raccomandazioni sulla progettazione di moduli e l&#39;esecuzione di test A/B sono le seguenti:

**Progettazione Forms**

* Semplificare, ridurre e semplificare la navigazione del modulo. Utilizzate suggerimenti direzionali per la navigazione.
* Utilizzare terminologie standard o comuni per i campi del modulo.
* Spiegate il campo e l&#39;input richiesti, con esempi o aiuto, dove gli utenti possono essere confusi.
* Convalidare gli input degli utenti durante la digitazione, ovunque possibile, per evitare errori durante l&#39;invio del modulo.
* Ottimizzate i layout per desktop e dispositivi mobili.
* Compilare automaticamente le informazioni per gli utenti noti.

**Test A/B**

* Create un&#39;ipotesi e identificate le metriche di successo prima di eseguire il test A/B.
* Fate delle variazioni minime (idealmente una alla volta) nell&#39;esperienza alternativa per sapere cosa ha inciso sul tasso di conversione.
* Testare frequentemente per eliminare le inefficienze.

