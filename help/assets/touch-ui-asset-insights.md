---
title: Informazioni sulla risorsa
description: Scopri come la funzione Asset Insights consente di tenere traccia delle valutazioni degli utenti e delle statistiche di utilizzo delle immagini utilizzate nei siti Web di terze parti, nelle campagne di marketing e nelle soluzioni creative di Adobe.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 7%

---


# Informazioni sulla risorsa {#asset-insights}

La funzione Asset Insights consente di tenere traccia delle valutazioni degli utenti e delle statistiche di utilizzo delle immagini utilizzate nei siti Web di terze parti, nelle campagne di marketing e nelle soluzioni creative di Adobe. Consente di ricavare informazioni sulle loro prestazioni e popolarità.

Assets Insights acquisisce i dettagli dell’attività dell’utente, ad esempio il numero di volte in cui un’immagine viene valutata, di cui è stato fatto clic e di impression (numero di volte in cui un’immagine viene caricata sul sito Web). Assegnano dei punteggi alle immagini in base a queste statistiche. Puoi usare le statistiche sui punteggi e sulle prestazioni per selezionare le immagini più comuni da includere nei cataloghi, nelle campagne di marketing e così via. È anche possibile formulare criteri per l&#39;archiviazione e il rinnovo delle licenze basati su tali statistiche.

Per acquisire le statistiche di utilizzo per le immagini da un sito Web, è necessario includere nel codice del sito Web il codice da incorporare per l’immagine.

Per consentire a Informazioni sulle risorse di visualizzare le statistiche di utilizzo per le risorse, configura prima la funzione per recuperare i dati di reporting da Adobe Analytics. Per informazioni dettagliate, consultate [Configurare approfondimenti](/help/assets/touch-ui-configuring-asset-insights.md)risorse.

>[!NOTE]
>
>Le informazioni approfondite sono supportate e fornite solo per le immagini.

## Visualizzare le statistiche per un’immagine {#viewing-statistics-for-an-image}

Potete visualizzare i punteggi di Asset Insights dalla pagina dei metadati.

1. Nell’interfaccia utente di Risorse, seleziona l’immagine e fai clic su **[!UICONTROL Proprietà]** nella barra degli strumenti.
1. Nella pagina Proprietà, fai clic sulla scheda **[!UICONTROL Insights]** (Approfondimenti).
1. Consultate i dettagli di utilizzo della risorsa nella scheda **[!UICONTROL Insights]** (Approfondimenti). Nella sezione **[!UICONTROL Punteggio]** sono descritte le risorse totali utilizzate e le risorse disponibili per le prestazioni di una risorsa.

   La valutazione dell&#39;utilizzo descrive il numero di volte in cui la risorsa viene utilizzata in varie soluzioni.

   Il punteggio **[!UICONTROL Impression]** indica quante volte la risorsa viene caricata sul sito Web. Il numero visualizzato in **[!UICONTROL Clic]** indica quante volte è possibile fare clic sulla risorsa.

1. Consultate la sezione Statistiche **[!UICONTROL di]** utilizzo per sapere di quali entità faceva parte la risorsa e di quali soluzioni creative ha utilizzato di recente. Maggiore è l’utilizzo, maggiori saranno le probabilità che la risorsa sia popolare tra gli utenti. I dati di utilizzo vengono visualizzati sotto le intestazioni seguenti:

   * **Risorsa**: Il numero di volte in cui la risorsa faceva parte di una raccolta o di una risorsa composta
   * **Web e dispositivi mobili**: Il numero di volte in cui la risorsa faceva parte di siti Web e app
   * **Social**: Il numero di volte in cui la risorsa è stata utilizzata nelle soluzioni, come Adobe Social e Adobe Campaign
   * **E-mail**: Numero di volte in cui la risorsa è stata utilizzata nelle campagne e-mail
   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >Poiché la funzione Asset Insights in genere raccoglie i dati delle soluzioni da Adobe Analytics in modo periodico, la sezione Soluzioni potrebbe non visualizzare i dati più recenti. Il periodo di tempo per il quale i dati vengono visualizzati dipende dalla pianificazione dell&#39;operazione di recupero eseguita da Asset Insights per recuperare i dati Analytics.

1. Per visualizzare graficamente le statistiche sulle prestazioni della risorsa in un arco di tempo, seleziona il periodo nella sezione **[!UICONTROL Statistiche di prestazioni]**. I dettagli, compresi clic e impression, vengono visualizzati come linee di tendenza di un grafico.

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >A differenza dei dati nella sezione Soluzioni, nella sezione Statistiche prestazioni vengono visualizzati i dati più recenti.

1. Per ottenere il codice da incorporare per la risorsa che includete nei siti Web per ottenere i dati sulle prestazioni, fate clic su **[!UICONTROL Ottieni codice]** da incorporare sotto la miniatura della risorsa. Per ulteriori informazioni su come includere il codice da incorporare nelle pagine Web di terze parti, consultate [Utilizzo del tracciatore di pagina e codice da incorporare nelle pagine](/help/assets/touch-ui-using-page-tracker.md)Web.

   ![chlimage_1-98](assets/chlimage_1-303.png)

## Visualizzare le statistiche aggregate per le immagini {#viewing-aggregate-statistics-for-images}

Dalla **[!UICONTROL Visualizzazione approfondimenti]** puoi visualizzare simultaneamente un punteggio di tutte le risorse presenti all’interno di una cartella.

1. Nell’interfaccia utente Risorse, passa alla cartella contenente le risorse per le quali vuoi visualizzare le informazioni.
1. Fate clic sull’icona Layout dalla barra degli strumenti, quindi scegliete Visualizzazione **[!UICONTROL approfondimenti]**.
1. Nella pagina vengono visualizzati i punteggi di utilizzo delle risorse. Confronta le valutazioni delle varie risorse e trai informazioni approfondite.

## Pianificazione processo in background {#scheduling-background-job}

Asset Insights recupera periodicamente i dati di utilizzo delle risorse dalle suite di rapporti di Adobe Analytics. Per impostazione predefinita, Asset Insights esegue un processo in background ogni 24 ore alle 2 del mattino fino ai dati di recupero. Tuttavia, potete modificare sia la frequenza che l’ora configurando il servizio **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** Service dalla console Web.

1. Click the AEM logo, and go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Aprite la configurazione del servizio di sincronizzazione dei processi **[!UICONTROL di]** Adobe CQ DAM Asset Performance Report.

   ![chlimage_1-99](assets/chlimage_1-304.png)

1. Specificate la frequenza di pianificazione desiderata e l&#39;ora di inizio del processo nell&#39;espressione utilità di pianificazione delle proprietà. Salva le modifiche.
