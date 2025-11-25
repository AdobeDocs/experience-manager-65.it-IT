---
title: Visualizzazione dei dati di analisi delle pagine per misurare l’efficacia del contenuto di una pagina
description: Utilizzare i dati di analisi delle pagine per misurare l’efficacia del contenuto delle pagine
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
docset: aem65
legacypath: /content/help/en/experience-manager/6-4/help/sites-authoring/pa-using.html
exl-id: 2e406512-47fb-451d-b837-0a3898ae1f08
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 5%

---

# Visualizzazione dei dati analitici sulle pagine{#seeing-page-analytics-data}

Utilizza i dati di analisi della pagina per misurare l’efficacia del contenuto della pagina.

## Analytics visibile dalla console {#analytics-visible-from-the-console}

![spad-01](assets/spad-01.png)

I dati di analisi delle pagine vengono visualizzati in [Vista a elenco](/help/sites-authoring/basic-handling.md#list-view) della console Sites. Quando le pagine vengono visualizzate in formato elenco, per impostazione predefinita sono disponibili le seguenti colonne:

* Visualizzazioni pagina
* Visitatori univoci
* Tempo sulla pagina

Ogni colonna mostra un valore per il periodo di reporting corrente e indica anche se il valore è aumentato o diminuito rispetto al periodo di reporting precedente. I dati visualizzati vengono aggiornati ogni 12 ore.

>[!NOTE]
>
>Per modificare il periodo di aggiornamento, [configurare l&#39;intervallo di importazione](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval).

1. Apri la console **Sites**, ad esempio [https://localhost:4502/sites.html/content](https://localhost:4502/sites.html/content)
1. Nell&#39;angolo superiore destro della barra degli strumenti fare clic sull&#39;icona per selezionare **Vista elenco** (l&#39;icona visualizzata dipenderà dalla [vista corrente](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)).

1. Di nuovo, all&#39;estrema destra della barra degli strumenti (angolo superiore destro), fai clic sull&#39;icona e seleziona **Visualizza impostazioni**. Viene visualizzata la finestra di dialogo **Configura colonne**. Apporta le modifiche necessarie e conferma con **Aggiorna**.

   ![spad-02](assets/spad-02.png)

### Selezione del periodo di reporting {#selecting-the-reporting-period}

Seleziona il periodo di reporting per il quale i dati di Analytics vengono visualizzati nella console Sites:

* Dati degli ultimi 30 giorni
* Dati degli ultimi 90 giorni
* Dati di quest&#39;anno

Il periodo di reporting corrente viene visualizzato sulla barra degli strumenti della console Sites (a destra della barra degli strumenti superiore). Utilizza l’elenco a discesa per selezionare il periodo di reporting richiesto.

![aa-05](assets/aa-05.png)

### Configurazione delle colonne di dati disponibili {#configuring-available-data-columns}

I membri del gruppo di utenti amministratori di Analytics possono configurare la console Sites per consentire agli autori di visualizzare colonne aggiuntive di Analytics.

>[!NOTE]
>
>Quando una struttura ad albero di pagine contiene elementi secondari associati a diverse configurazioni cloud di Adobe Analytics, non è possibile configurare le colonne di dati disponibili per le pagine.

1. In Vista a elenco, utilizza i selettori di visualizzazione (a destra della barra degli strumenti), seleziona **Impostazioni visualizzazione** e quindi **Aggiungi dati di analisi personalizzati**.

   ![spad-03](assets/spad-03.png)

1. Selezionare le metriche da esporre agli autori nella console Sites, quindi fare clic su **Aggiungi**.

   Le colonne visualizzate vengono recuperate da Adobe Analytics.

   ![aa-16](assets/aa-16.png)

### Apertura di Content Insights da Sites {#opening-content-insights-from-sites}

Apri [Content Insight](/help/sites-authoring/content-insights.md) dalla console Sites per ulteriori informazioni sull&#39;efficacia della pagina.

1. Nella console Sites, seleziona la pagina per la quale desideri visualizzare Content Insights.
1. Sulla barra degli strumenti, fai clic sull’icona Analytics e Recommendations.

   ![Icona Analytics and Recommendations](do-not-localize/chlimage_1-14.png)

## Analytics visibile dall’Editor pagina (Activity Map) {#analytics-visible-from-the-page-editor-activity-map}

>[!CAUTION]
>
>A causa di modifiche di sicurezza nell’API di Adobe Analytics, non è più possibile utilizzare la versione di Activity Map inclusa in AEM.
>
>È ora necessario utilizzare il plug-in [ActivityMap fornito da Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html?lang=it).
