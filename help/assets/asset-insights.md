---
title: Informazioni sulle risorse
description: Scopri come la funzione Assets Insights ti consente di monitorare le valutazioni degli utenti e le statistiche di utilizzo delle immagini utilizzate in siti web di terze parti, campagne di marketing e soluzioni creative di Adobe.
contentOwner: AG
role: Business Practitioner, Administrator
feature: Informazioni sulla risorsa, rapporti sulle risorse
exl-id: 0130ac40-a72b-4caf-a10f-3c7d76eaa1e6
source-git-commit: 68c36d4e3a14567a4d115ee64a4474bcaf9aa386
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 6%

---

# Informazioni sulle risorse {#asset-insights}

La funzione Assets Insights ti consente di monitorare le valutazioni degli utenti e le statistiche di utilizzo delle immagini utilizzate in siti web di terze parti, campagne di marketing e soluzioni creative di Adobe. Aiuta a trarre informazioni sulle loro prestazioni e popolarità.

[!DNL Assets] Insights acquisisce i dettagli dell’attività dell’utente, ad esempio il numero di volte in cui un’immagine viene valutata, su cui è stato fatto clic e le impression (numero di volte in cui un’immagine viene caricata sul sito web). Assegna punteggi alle immagini in base a queste statistiche. Puoi utilizzare i punteggi e le statistiche sulle prestazioni per selezionare le immagini più comuni da includere nei cataloghi, nelle campagne di marketing e così via. Puoi anche formulare politiche di archiviazione e rinnovo delle licenze basate su queste statistiche.

Affinché [!DNL Assets] Informazioni utili per acquisire le statistiche di utilizzo per le immagini da un sito web, è necessario includere il codice di incorporamento per l’immagine nel codice del sito web.

Per consentire a Assets Insights di visualizzare le statistiche di utilizzo delle risorse, configura prima la funzione per recuperare i dati di reporting da Adobe Analytics. Per informazioni dettagliate, consulta [Configurare Assets Insights](/help/assets/configure-asset-insights.md). Per utilizzare questa funzione in un’installazione on-premise, acquista la licenza [!DNL Adobe Analytics] separatamente. I clienti su [!DNL Managed Services] ricevono la licenza [!DNL Analytics] inclusa in [!DNL Experience Manager]. Consulta [Descrizione del prodotto Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html).

>[!NOTE]
>
>Gli approfondimenti sono supportati e forniti solo per le immagini.

## Visualizzare le statistiche di un&#39;immagine {#viewing-statistics-for-an-image}

Puoi visualizzare i punteggi di Assets Insights dalla pagina dei metadati.

1. Dall’ [!DNL Assets] interfaccia utente (UI), seleziona l’immagine e fai clic su **[!UICONTROL Proprietà]** nella barra degli strumenti.
1. Dalla pagina Proprietà, fai clic sulla scheda **[!UICONTROL Insights]** .
1. Controlla i dettagli di utilizzo della risorsa nella scheda **[!UICONTROL Informazioni]** . La sezione **[!UICONTROL Punteggio]** descrive l’utilizzo totale delle risorse e le origini delle prestazioni di una risorsa .

   Il punteggio di utilizzo descrive il numero di volte in cui la risorsa viene utilizzata in varie soluzioni.

   Il punteggio **[!UICONTROL Impression]** è il numero di volte in cui la risorsa viene caricata sul sito web. Il numero visualizzato in **[!UICONTROL Clic]** indica il numero di volte in cui la risorsa viene selezionata.

1. Consulta la sezione **[!UICONTROL Statistiche di utilizzo]** per sapere di quali entità faceva parte la risorsa e di quali soluzioni creative l’ha utilizzata di recente. Maggiore è l’utilizzo, maggiori sono le probabilità che la risorsa sia popolare tra gli utenti. I dati di utilizzo vengono visualizzati sotto le seguenti intestazioni:

   * **Risorsa**: Il numero di volte in cui la risorsa faceva parte di una raccolta o di una risorsa composta
   * **Web e dispositivi mobili**: Il numero di volte in cui la risorsa faceva parte di siti web e app
   * **Social**: Il numero di volte in cui la risorsa è stata utilizzata nelle soluzioni, come Adobe Social e Adobe Campaign
   * **E-mail**: Il numero di volte in cui la risorsa è stata utilizzata nelle campagne e-mail

   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >Poiché la funzione Asset Insights in genere recupera i dati delle soluzioni da Adobe Analytics in modo periodico, la sezione Soluzioni potrebbe non visualizzare i dati più recenti. Il periodo di tempo per il quale vengono visualizzati i dati dipende dalla pianificazione dell’operazione di recupero eseguita da Assets Insights per il recupero dei dati di Analytics.

1. Per visualizzare graficamente le statistiche sulle prestazioni della risorsa in un arco di tempo, seleziona il periodo nella sezione **[!UICONTROL Statistiche di prestazioni]**. I dettagli, compresi clic e impression, vengono visualizzati come linee di tendenza di un grafico.

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >A differenza dei dati nella sezione Soluzioni , la sezione Statistiche di prestazioni visualizza i dati più recenti.

1. Per ottenere il codice di incorporamento della risorsa inclusa nei siti web per ottenere i dati sulle prestazioni, fai clic su **[!UICONTROL Ottieni codice di incorporamento]** sotto la miniatura della risorsa. Per ulteriori informazioni su come includere il codice da incorporare in pagine web di terze parti, consulta [Utilizzo di tracciamento pagina e codice da incorporare nelle pagine web](/help/assets/use-page-tracker.md).

   ![chlimage_1-98](assets/chlimage_1-303.png)

## Visualizza le statistiche aggregate per le immagini {#viewing-aggregate-statistics-for-images}

Dalla **[!UICONTROL Visualizzazione approfondimenti]** puoi visualizzare simultaneamente un punteggio di tutte le risorse presenti all’interno di una cartella.

1. Nell’interfaccia utente di [!DNL Assets] , individua la cartella contenente le risorse di cui desideri visualizzare le informazioni.
1. Fai clic su Layout dalla barra degli strumenti, quindi scegli **[!UICONTROL Visualizzazione approfondimenti]**.
1. Nella pagina vengono visualizzati i punteggi di utilizzo delle risorse. Confronta le valutazioni delle varie risorse e trai informazioni approfondite.

## Pianifica processo in background {#scheduling-background-job}

Assets Insights recupera periodicamente i dati di utilizzo per le risorse dalle suite di rapporti di Adobe Analytics. Per impostazione predefinita, Assets Insights esegue un processo in background ogni 24 ore alle 2 del mattino fino ai dati di recupero. Tuttavia, puoi modificare sia la frequenza che l’ora configurando il servizio **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** dalla console Web.

1. Fai clic sul logo [!DNL Experience Manager] e vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console web]**.
1. Apri la configurazione del servizio **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]** .

   ![chlimage_1-99](assets/chlimage_1-304.png)

1. Specifica la frequenza di pianificazione desiderata e l’ora di inizio del processo nell’espressione di pianificazione delle proprietà. Salva le modifiche.
