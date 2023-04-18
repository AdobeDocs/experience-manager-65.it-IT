---
title: Visualizzazione dei dati di analisi delle pagine per misurare l’efficacia del contenuto della pagina
seo-title: Seeing Page Analytics Data
description: Utilizza i dati analitici pagina per misurare l’efficacia del contenuto della pagina
seo-description: Use page analytics data to gauge the effectiveness of their page content
uuid: 5398a5d5-0239-4194-a403-77f5e6fcd741
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 5d192a48-c86f-4803-bb0d-0411ac7470f5
docset: aem65
legacypath: /content/help/en/experience-manager/6-4/help/sites-authoring/pa-using.html
exl-id: 2e406512-47fb-451d-b837-0a3898ae1f08
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 11%

---

# Visualizzazione dei dati di analisi delle pagine{#seeing-page-analytics-data}

Utilizza i dati analitici pagina per misurare l’efficacia del contenuto della pagina.

## Analytics visibile dalla console {#analytics-visible-from-the-console}

![spad-01](assets/spad-01.png)

I dati analitici pagina vengono visualizzati in [Vista a elenco](/help/sites-authoring/basic-handling.md#list-view) della console Sites . Quando le pagine vengono visualizzate in formato elenco, per impostazione predefinita sono disponibili le colonne seguenti:

* Visualizzazioni pagina
* Visitatori univoci
* Tempo sulla pagina

Ogni colonna mostra un valore per il periodo di reporting corrente e indica anche se il valore è aumentato o diminuito rispetto al periodo di reporting precedente. I dati visualizzati vengono aggiornati ogni 12 ore.

>[!NOTE]
>
>Per modificare il periodo di aggiornamento, [configurare l’intervallo di importazione](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval).

1. Apri **Sites** console; per esempio [https://localhost:4502/sites.html/content](https://localhost:4502/sites.html/content)
1. All’estrema destra della barra degli strumenti (angolo in alto a destra), tocca o fai clic sull’icona per selezionare **Vista a elenco** L’icona visualizzata dipende dal [vista corrente](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)).

1. Di nuovo, all’estrema destra della barra degli strumenti (angolo in alto a destra), tocca o fai clic sull’icona e seleziona **Visualizza impostazioni**. La **Configura colonne** si aprirà la finestra di dialogo . Apporta le modifiche necessarie e conferma con **Aggiorna**.

   ![spad-02](assets/spad-02.png)

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

   ![spad-03](assets/spad-03.png)

1. Seleziona le metriche da esporre agli autori nella console Sites e fai clic su **Aggiungi**.

   Le colonne visualizzate vengono recuperate da Adobe Analytics.

   ![aa-16](assets/aa-16.png)

### Apertura di Approfondimenti contenuto da Sites {#opening-content-insights-from-sites}

Apri [Approfondimenti contenuto](/help/sites-authoring/content-insights.md) dalla console Sites per approfondire l’efficacia della pagina.

1. Nella console Siti , seleziona la pagina per la quale desideri visualizzare Approfondimenti contenuto.
1. Nella barra degli strumenti, fai clic sull’icona Analytics e Recommendations .

   ![](do-not-localize/chlimage_1-14.png)

## Analytics visibile dall’Editor pagina (Activity Map) {#analytics-visible-from-the-page-editor-activity-map}

>[!CAUTION]
>
>In seguito a modifiche di sicurezza nell’API di Adobe Analytics, non è più possibile utilizzare la versione di Activity Map inclusa in AEM.
>
>La [Plug-in ActivityMap fornito da Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=it) Da utilizzare.
