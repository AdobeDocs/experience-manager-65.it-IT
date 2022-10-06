---
title: Visualizzazione dei dati analitici sulle pagine
seo-title: Seeing Page Analytics Data
description: Utilizza i dati analitici pagina per misurare l'efficacia del contenuto della pagina
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
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 84%

---

# Visualizzazione dei dati analitici sulle pagine{#seeing-page-analytics-data}

Utilizza i dati analitici pagina per misurare l&#39;efficacia del contenuto della pagina.

## Dati analitici visibili dalla console {#analytics-visible-from-the-console}

![spad-01](assets/spad-01.png)

I dati analitici pagina vengono visualizzati nella [Vista a elenco](/help/sites-authoring/basic-handling.md#list-view) della console Sites. Quando le pagine vengono visualizzate nel formato elenco, sono disponibili le colonne seguenti per impostazione predefinita:

* Visualizzazioni pagina
* Visitatori univoci
* Tempo sulla pagina

Ciascuna colonna mostra un valore per il periodo di generazione rapporti in corso e indica anche se tale valore è aumentato o diminuito rispetto al periodo di generazione rapporti precedente. I dati visualizzati vengono aggiornati ogni 12 ore.

>[!NOTE]
>
>Per modificare il periodo di aggiornamento, [configura l&#39;intervallo di importazione](/help/sites-administering/adobeanalytics-connect.md#configuring-the-import-interval).

1. Apri **Sites** console; per esempio [https://localhost:4502/sites.html/content](https://localhost:4502/sites.html/content)
1. Nella parte all&#39;estrema destra della barra degli strumenti (angolo in alto a destra), tocca o fai clic sull&#39;icona per selezionare **Vista a elenco** (l&#39;icona mostrata dipende dalla [vista corrente](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)).

1. Di nuovo, all&#39;estrema destra della barra degli strumenti (angolo in alto a destra) tocca o fai clic sull&#39;icona **Visualizza impostazioni**. Si aprirà la finestra di dialogo **Configura colonne**. Apporta le modifiche necessarie e conferma con **Aggiorna**.

   ![spad-02](assets/spad-02.png)

### Selezione del periodo di generazione rapporti {#selecting-the-reporting-period}

Seleziona il periodo di generazione rapporti per il quale i dati di Analytics vengono visualizzati sulla console Sites:

* Dati degli ultimi 30 giorni
* Dati degli ultimi 90 giorni
* Dati di quest&#39;anno

Il periodo di rigenerazione rapporti corrente viene visualizzato nella barra degli strumenti della console Sites (a destra della barra degli strumenti superiore). Utilizza il menu a discesa per selezionare il periodo di generazione rapporti desiderato.

![aa-05](assets/aa-05.png)

### Configurazione delle colonne di dati disponibili {#configuring-available-data-columns}

I membri del gruppo utenti amministratori-analytics possono configurare la console Sites per consentire agli autori di vedere ulteriori colonne di Analytics.

>[!NOTE]
>
>Quando una struttura ad albero di pagine contiene elementi secondari associati a diverse configurazioni cloud di Adobe Analytics, non potrai configurare le colonne di dati disponibili per le pagine.

1. Nella Vista a elenco, utilizza i selettori di visualizzazione (a destra della barra degli strumenti), seleziona **Visualizza impostazioni** e poi **Aggiungi dati di Analytics personalizzati**.

   ![spad-03](assets/spad-03.png)

1. Seleziona le metriche che desideri esporre agli autori nella console Sites, quindi fai clic su **Aggiungi**.

   Le colonne visualizzate vengono recuperate da Adobe Analytics.

   ![aa-16](assets/aa-16.png)

### Apertura di approfondimenti sui contenuti da Sites {#opening-content-insights-from-sites}

Apri [Approfondimenti contenuto](/help/sites-authoring/content-insights.md) dalla console Sites per approfondire l’efficacia della pagina.

1. Nella console Sites, seleziona la pagina per la quale desideri visualizzare gli approfondimenti dei contenuti.
1. Nella barra degli strumenti, fai clic sull’icona di Analytics e Recommendations.

   ![](do-not-localize/chlimage_1-14.png)

## Dati analitici visibili dall’Editor pagine (Mappa attività) {#analytics-visible-from-the-page-editor-activity-map}

>[!CAUTION]
>
>In seguito a modifiche di sicurezza nell’API di Adobe Analytics, non è più possibile utilizzare la versione di Activity Map inclusa in AEM.
>
>La [Plug-in ActivityMap fornito da Adobe Analytics](https://docs.adobe.com/content/help/it/analytics/analyze/activity-map/getting-started/get-started-users/activitymap-install.html) Da utilizzare.
