---
title: Visualizzazione e comprensione  report di analisi AEM Forms
seo-title: Visualizzazione e comprensione  report di analisi AEM Forms
description: ' AEM Forms si integra con  Adobe Analytics e fornisce analisi sintetiche e dettagliate sui moduli adattivi pubblicati.'
seo-description: ' AEM Forms si integra con  Adobe Analytics e fornisce analisi sintetiche e dettagliate sui moduli adattivi pubblicati.'
uuid: b15ba5f3-aea7-40f5-893e-aaf3834cbc33
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 3690fa80-6332-4df8-afea-77b5490fe0d1
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 0%

---


# Visualizzazione e comprensione  report di analisi AEM Forms {#view-and-understand-aem-forms-analytics-reports}

 Adobe Experience Manager Forms si integra con  Adobe Analytics che consente di acquisire e monitorare le metriche delle prestazioni per i moduli e i documenti pubblicati. L&#39;obiettivo dell&#39;analisi di queste metriche è di rendere più utilizzabili moduli o documenti con decisioni informate basate sui dati richiesti.

## Impostazione dell&#39;analisi {#setting-up-analytics}

La funzione di analisi in  AEM Forms è disponibile come parte del pacchetto  del componente aggiuntivo AEM Forms. Per informazioni sull&#39;installazione del pacchetto del componente aggiuntivo, consultate [Installazione e configurazione  AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md).

Oltre al pacchetto del componente aggiuntivo, è necessario un account Adobe Analytics . Per informazioni sulla soluzione, vedere [ Adobe Analytics](https://www.adobe.com/solutions/digital-analytics.html).

Una volta ottenuto il pacchetto  del componente aggiuntivo AEM Forms e un account  Adobe Analytics, è possibile integrare  account Adobe Analytics con  AEM Forms e abilitare il tracciamento dei moduli o dei documenti come descritto in [Configura analisi e report](../../forms/using/configure-analytics-forms-documents.md).

### Registrazione delle informazioni sull&#39;interazione con l&#39;utente {#how-user-interaction-information-is-recorded}

Quando un utente interagisce con il modulo, le interazioni vengono registrate e inviate al server Analytics. Il seguente elenco indica le chiamate server per diverse attività utente:

* 2 chiamate per campo per visita
* 1 per la visita del panel
* 1 per risparmiare
* 2 per l&#39;invio
* 2 per risparmiare
* 1 per assistenza
* 1 per ogni errore di convalida
* 1 per la rappresentazione del modulo + 1 per il pannello predefinito visita + 1 per la prima visita del campo predefinita
* 2 per l&#39;abbandono del modulo

>[!NOTE]
>
>Questo elenco non è esaustivo.

### Visualizzazione dei report di analisi {#summary-report}

Per visualizzare i rapporti di analisi, effettuate le seguenti operazioni:

1. Accedete al portale AEM all&#39;indirizzo `https://[hostname]:'port'`
1. Fare clic su **Forms > Forms &amp; Documents**.
1. Selezionare il modulo per il quale si desidera visualizzare i report di analisi.
1. Selezionare **Altro > Analytics Reports**.

![analyticsreport](assets/analyticsreport.png)

**A.** Analytics Report, comando

 AEM Forms visualizza i report di analisi per il modulo e per ciascun pannello del modulo, come mostrato di seguito.

![Report di riepilogo di un modulo adattivo](assets/analyticsdashboard_callout.png)

**A.** Conversioni  **B.Riepilogo a livello di** modulo  **C.** Riepilogo a livello di pannello  **D.** Browser di visitatori - filtro  **E.** OS di visitatori - filtro  **** F.Lingua dei visitatori - filtro

Per impostazione predefinita, viene visualizzato il rapporto di analisi per gli ultimi sette giorni. Puoi visualizzare i rapporti degli ultimi 15 giorni, degli ultimi 1 mese e così via, oppure specificare un intervallo di date.

>[!NOTE]
>
>Le opzioni come Ultimi 7 giorni e Ultimi 15 giorni non includono i dati per il giorno in cui state generando il rapporto di analisi. Per includere i dati del giorno corrente, è necessario specificare l&#39;intervallo di date che include il giorno corrente, quindi eseguire il rapporto.

![intervallo date](assets/date-range.png)

### Grafico Conversioni per moduli adattivi e HTML5 {#conversions-graph-for-adaptive-and-html-forms}

Il grafico delle conversioni a livello di modulo fornisce informazioni approfondite sulle prestazioni del modulo in base ai seguenti indicatori prestazioni chiave (KPI):

* **Rappresentazioni**: Numero di volte in cui un modulo viene aperto
* **Visitatori**: Numero di visitatori del modulo
* **Invii**: Numero di volte in cui il modulo viene inviato

![conversion-graph](assets/conversion-graph.png)

### Report di analisi per moduli adattivi e HTML5 {#analytics-report-for-adaptive-and-html-forms}

La sezione di riepilogo a livello di modulo fornisce informazioni approfondite sulle prestazioni del modulo in relazione ai seguenti indicatori prestazioni chiave (KPI):

* **Tempo** medio di riempimento: Tempo medio impiegato per compilare il modulo. Quando gli utenti passano del tempo sul modulo ma non inviano, tale tempo non viene incluso nel calcolo.
* **Rappresentazioni**: Numero di volte in cui è stato eseguito il rendering o l&#39;apertura del modulo
* **Bozze**: Numero di volte in cui il modulo è stato salvato come bozza
* **Invii**: Numero di volte in cui il modulo è stato inviato
* **Interrompi**: Numero di volte in cui gli utenti hanno iniziato a compilare il modulo e poi se ne sono andati senza compilare il modulo
* **Visitatori** univoci: Numero di volte in cui il modulo viene rappresentato da visitatori univoci. Per ulteriori informazioni sui visitatori univoci, vedi [Visitatori unici, Visite e comportamento dei clienti](https://helpx.adobe.com/analytics/kb/unique-visitors-visitor-behavior.html).

![Report di analisi di riepilogo a livello di modulo esteso](assets/analytics-report.png)

### Rapporto pannello {#bottom-summary-report}

La sezione di riepilogo a livello di pannello contiene le seguenti informazioni su ciascun pannello del modulo:

* **Tempo** medio di riempimento: Tempo medio trascorso sul pannello, che il modulo sia stato inviato o meno
* **Errori riscontrati**: Numero medio di errori riscontrati dagli utenti sui campi di un pannello. Gli errori riscontrati vengono generati dividendo gli errori totali in un campo per numero di rappresentazioni del modulo.
* **Aiuto accessibile**: Numero medio di volte in cui gli utenti hanno eseguito l’accesso alla guida contestuale per i campi nel pannello. L&#39;Aiuto accessibile viene fornito suddividendo il numero totale di volte in cui l&#39;Aiuto è accessibile per un campo in base al numero di rappresentazioni del modulo.

#### Rapporto dettagliato sul pannello {#detailed-panel-report}

Potete anche visualizzare i dettagli di ciascun pannello facendo clic sul nome di un pannello in Rapporto pannello.

![Report dettagliato del pannello](assets/panel-report-detailed.png)

Il rapporto dettagliato mostra i valori per tutti i campi del pannello.

Report pannello ha tre schede:

* **Rapporto** ora (predefinito): Visualizza il tempo, in secondi, trascorso a compilare ciascuno dei campi nel pannello
* **Report** errore: Visualizza il numero di errori riscontrati dagli utenti durante la compilazione dei campi
* **Rapporto** Aiuto: Numero di volte in cui è stato eseguito l&#39;accesso all&#39;aiuto per un particolare campo

Potete spostarvi tra i pannelli, se sono disponibili più pannelli.

### Filtri: Browser, sistema operativo e lingua {#filters-browser-os-and-language}

Le tabelle Distribuzione browser, Distribuzione sistema operativo e Distribuzione lingua mostrano le rappresentazioni, i visitatori e gli invii in base a browser, sistema operativo e lingua degli utenti dei moduli. Per impostazione predefinita, nelle tabelle sono visualizzate fino a cinque voci. Potete fare clic su Show More (Mostra altro) per visualizzare più voci e fare clic su Show Less (Mostra meno) per tornare alle cinque voci normali o meno.

Per filtrare ulteriormente i dati di analisi, potete fare clic su una voce in una qualsiasi delle tabelle. Ad esempio, se fai clic su Google Chrome nella tabella di distribuzione del browser, il rapporto viene riprodotto con i dati relativi al browser Google Chrome come segue:

![Filtro applicato al report di Analytics - Google Chrome  ](assets/filter-1.png)

Se visualizzate il rapporto del pannello dopo aver applicato un filtro, i dati del rapporto del pannello vengono visualizzati anche in base al filtro applicato.

Una volta applicato il filtro:

* Le tabelle di distribuzione diventano di sola lettura, in quanto è possibile applicare un solo filtro alla volta.
* La tabella del filtro applicato scompare.
* Per rimuovere il filtro applicato, fate clic sul pulsante Chiudi (evidenziato di seguito).

![Pulsante Chiudi per rimuovere il filtro applicato](assets/close-filter.png)

### Test A/B {#a-b-testing}

Se il test A/B è abilitato e configurato per il modulo, nella pagina del rapporto è disponibile un elenco a discesa che è possibile utilizzare per visualizzare il rapporto di test A/B. Il rapporto di test A/B mostra le prestazioni comparative di due versioni del modulo configurate.

Per ulteriori informazioni sui test A/B, vedere [Creazione e gestione di test A/B per i moduli adattivi](../../forms/using/ab-testing-adaptive-forms.md).
