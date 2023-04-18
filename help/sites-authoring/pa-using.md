---
title: Visualizzazione dei dati analitici pagina per misurare l’efficacia del contenuto della pagina
description: Utilizza i dati analitici pagina per misurare l’efficacia del contenuto della pagina
uuid: 8dda89be-13e3-4a13-9a44-0213ca66ed9c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 42d2195a-1327-45c0-a14c-1cf5ca196cfc
exl-id: 554b10c2-6157-4821-a6a7-f2fb6666cdff
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 4%

---

# Visualizzazione dei dati di analisi delle pagine{#seeing-page-analytics-data}

Utilizza i dati analitici pagina per misurare l’efficacia del contenuto della pagina.

## Analytics visibile dalla console {#analytics-visible-from-the-console}

![aa-10](assets/aa-10.png)

I dati analitici pagina vengono visualizzati in [Vista a elenco](/help/sites-authoring/basic-handling.md#list-view) della console Sites . Quando le pagine vengono visualizzate in formato elenco, per impostazione predefinita sono disponibili le colonne seguenti:

* Visualizzazioni pagina
* Visitatori univoci
* Tempo sulla pagina

Ogni colonna mostra un valore per il periodo di reporting corrente e indica anche se il valore è aumentato o diminuito rispetto al periodo di reporting precedente. I dati visualizzati vengono aggiornati ogni 12 ore.

>[!NOTE]
>
>Per modificare il periodo di aggiornamento, [configurare l’intervallo di importazione](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval).

1. Apri **Sites** console; per esempio [http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content)
1. All’estrema destra della barra degli strumenti (angolo in alto a destra), tocca o fai clic sull’icona per selezionare **Vista a elenco** L’icona visualizzata dipende dal [vista corrente](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)).

1. Di nuovo, all’estrema destra della barra degli strumenti (angolo in alto a destra), tocca o fai clic sull’icona e seleziona **Visualizza impostazioni**. La **Configura colonne** si aprirà la finestra di dialogo . Apporta le modifiche necessarie e conferma con **Aggiorna**.

   ![aa-04](assets/aa-04.png)

### Selezione del periodo di riferimento {#selecting-the-reporting-period}

Seleziona il periodo di reporting per il quale i dati di Analytics vengono visualizzati nella console Sites:

* Dati degli ultimi 30 giorni
* Dati degli ultimi 90 giorni
* Dati di quest&#39;anno

Il periodo di reporting corrente viene visualizzato sulla barra degli strumenti della console Sites (a destra della barra degli strumenti superiore). Utilizza il menu a discesa per selezionare il periodo di reporting richiesto.
![aa-05](assets/aa-05.png)

### Configurazione delle colonne di dati disponibili {#configuring-available-data-columns}

I membri del gruppo di utenti amministratori di analytics possono configurare la console Sites per consentire agli autori di visualizzare ulteriori colonne di Analytics.

>[!NOTE]
>
>Quando una struttura ad albero di pagine contiene elementi secondari associati a diverse configurazioni cloud di Adobe Analytics, non è possibile configurare le colonne di dati disponibili per le pagine.

1. Nella Vista a elenco, utilizza i selettori di visualizzazione (a destra della barra degli strumenti), seleziona **Visualizza impostazioni** e poi **Aggiungi dati di Analytics personalizzati**.

   ![aa-15](assets/aa-15.png)

1. Seleziona le metriche da esporre agli autori nella console Sites e fai clic su **Aggiungi**.

   Le colonne visualizzate vengono recuperate da Adobe Analytics.

   ![aa-16](assets/aa-16.png)

### Apertura di Approfondimenti contenuto da Sites {#opening-content-insights-from-sites}

Apri [Approfondimenti contenuto](/help/sites-authoring/content-insights.md) dalla console Sites per approfondire l’efficacia della pagina.

1. Nella console Siti , seleziona la pagina per la quale desideri visualizzare Approfondimenti contenuto.
1. Nella barra degli strumenti, fai clic sull’icona Analytics e Recommendations .

   ![](do-not-localize/chlimage_1-16a.png)

## Analytics visibile dall’Editor pagina (Activity Map) {#analytics-visible-from-the-page-editor-activity-map}

>[!NOTE]
>
>Questo verrà mostrato se [Activity Map è stato configurato](/help/sites-administering/adobeanalytics-connect.md#configuring-for-the-activity-map) per il sito web.

>[!NOTE]
>
>I dati per Activity Map vengono ricavati da Adobe Analytics.

Quando il sito web è stato [configurato per Adobe Analytics](/help/sites-administering/adobeanalytics-connect.md), puoi utilizzare la [mode Activity Map](/help/sites-authoring/author-environment-tools.md#page-modes) per visualizzare i dati pertinenti. Ad esempio:

![aa-07](assets/aa-07.png)

### Accesso ad Activity Map {#accessing-the-activity-map}

Dopo aver selezionato la [Activity Map](/help/sites-authoring/author-environment-tools.md#page-modes) In modalità , ti verrà richiesto di immettere le tue credenziali Adobe Analytics.

![aa-03](assets/aa-03.png)

La **Analytics** viene visualizzata la barra degli strumenti mobile; qui puoi:

* modificare il formato della barra degli strumenti utilizzando le frecce doppie (**>>**)
* Attiva/disattiva dettagli pagina (icona occhio)
* Configura le impostazioni di Activity Map (icona ingranaggio)
* Seleziona l’analisi da visualizzare (vari selettori a discesa)
* Esci da Activity Map e chiudi la barra degli strumenti (x)

![aa-09](assets/aa-09.png)

### Selezione di Analytics da visualizzare {#selecting-the-analytics-to-show}

Puoi selezionare i dati analitici da visualizzare e come visualizzarli, utilizzando i vari criteri:

* **Standard**/**Live**

* tipo di evento
* gruppo utenti
* **Bolle**/**Sfumatura**/**Guadagni e perdenti**/**Disattivato**

* periodo da visualizzare

![aa-13](assets/aa-13.png)

### Configurazione di Activity Map {#configuring-the-activity-map}

Utilizza la **Mostra impostazioni** per aprire **Impostazioni di Activity Map** finestra di dialogo.

![aa-04-1](assets/aa-04-1.png)

La **Impostazioni di Activity Map** La finestra di dialogo fornisce una serie di opzioni su tre schede:

![aa-06](assets/aa-06.png)

* Generale

   * Suite per report
   * Nome pagina
   * Lingua
   * Sovrapposizioni etichette con
   * Dimensione font etichetta
   * Colore sfumatura
   * Colore bolle
   * Sfumatura colore basata su
   * Trasparenza sfumatura

* Standard

   * Visualizzazione (tipo e numero di collegamenti)
   * Nascondere le sovrapposizioni per i collegamenti che non hanno ricevuto hit

* Live

   * Display Top (vincitori o perdenti)
   * Escludi % inferiore
   * Aggiornamento automatico (dati e periodo)
