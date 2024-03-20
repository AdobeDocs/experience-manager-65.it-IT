---
title: Informazioni su Assets
description: Scopri come la funzione Assets Insights consente di monitorare le valutazioni degli utenti e le statistiche di utilizzo delle immagini utilizzate nei siti web di terze parti, nelle campagne di marketing e nelle soluzioni creative di Adobe.
contentOwner: AG
role: User, Admin
feature: Asset Insights,Asset Reports
exl-id: 0130ac40-a72b-4caf-a10f-3c7d76eaa1e6
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 9%

---

# Informazioni su Assets {#asset-insights}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/assets-insights.html?lang=en) |
| AEM 6.5 | Questo articolo |

La funzione Assets Insights consente di monitorare le valutazioni degli utenti e le statistiche di utilizzo delle immagini utilizzate nei siti web di terze parti, nelle campagne di marketing e nelle soluzioni creative di Adobe. Consente di ricavare informazioni sulla loro performance e popolarità.

[!DNL Assets] Insights acquisisce i dettagli dell’attività dell’utente, ad esempio il numero di volte in cui un’immagine viene valutata, cliccata e impression (numero di volte in cui un’immagine viene caricata sul sito web). Assegna punteggi alle immagini in base a queste statistiche. Puoi utilizzare i punteggi e le statistiche sulle prestazioni per selezionare le immagini più comuni da includere in cataloghi, campagne di marketing e così via. È inoltre possibile formulare criteri di archiviazione e rinnovo delle licenze in base a tali statistiche.

Per [!DNL Assets] Informazioni per acquisire statistiche di utilizzo per le immagini da un sito Web, devi includere il codice di incorporamento per l&#39;immagine nel codice del sito Web.

Per consentire a Assets Insights di visualizzare le statistiche di utilizzo delle risorse, configura innanzitutto la funzione per recuperare i dati di reporting da Adobe Analytics. Per ulteriori informazioni, consulta [Configurare Assets Insights](/help/assets/configure-asset-insights.md). Per utilizzare questa funzione in un’installazione on-premise, acquista [!DNL Adobe Analytics] licenza separatamente. Clienti il [!DNL Managed Services] ricevere [!DNL Analytics] licenza fornita con [!DNL Experience Manager]. Consulta [Descrizione del prodotto Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html).

>[!NOTE]
>
>Gli approfondimenti sono supportati e forniti solo per le immagini.

## Visualizzare le statistiche di un’immagine {#viewing-statistics-for-an-image}

Puoi visualizzare i punteggi di Assets Insights dalla pagina dei metadati.

1. Dalla sezione [!DNL Assets] interfaccia utente (UI), seleziona l’immagine e fai clic su **[!UICONTROL Proprietà]** dalla barra degli strumenti.
1. Dalla pagina Proprietà, fai clic su **[!UICONTROL Approfondimenti]** scheda.
1. Rivedi i dettagli di utilizzo della risorsa in **[!UICONTROL Approfondimenti]** scheda. Il **[!UICONTROL Punteggio]** La sezione descrive l’utilizzo totale delle risorse e le sequenze di prestazioni di una risorsa.

   Il punteggio di utilizzo descrive il numero di volte in cui la risorsa viene utilizzata in varie soluzioni.

   Il **[!UICONTROL Impression]** punteggio è il numero di volte in cui la risorsa viene caricata sul sito web. Numero visualizzato in **[!UICONTROL Clic]** è il numero di volte in cui si fa clic sulla risorsa.

1. Rivedi **[!UICONTROL Statistiche di utilizzo]** sezione per sapere di quali entità faceva parte la risorsa e quali soluzioni creative l’hanno recentemente utilizzata. Maggiore è l’utilizzo, maggiori sono le probabilità che la risorsa sia popolare tra gli utenti. I dati di utilizzo vengono visualizzati sotto le seguenti intestazioni:

   * **Risorsa**: numero di volte in cui la risorsa faceva parte di una raccolta o di una risorsa composta
   * **Web e mobile**: numero di volte in cui la risorsa faceva parte di siti web e app
   * **Social**: numero di volte in cui la risorsa è stata utilizzata in soluzioni quali Adobe Social e Adobe Campaign
   * **E-mail**: numero di volte in cui la risorsa è stata utilizzata nelle campagne e-mail

   ![usage_statistics](assets/usage_statistics.png)

   >[!NOTE]
   >
   >Poiché la funzione Assets Insights in genere recupera i dati delle soluzioni da Adobe Analytics in modo periodico, la sezione Soluzioni potrebbe non visualizzare i dati più recenti. Il periodo di tempo per il quale vengono visualizzati i dati dipende dalla pianificazione dell’operazione di recupero eseguita da Assets Insights per recuperare i dati di Analytics.

1. Per visualizzare graficamente le statistiche sulle prestazioni della risorsa in un arco di tempo, seleziona il periodo nella sezione **[!UICONTROL Statistiche di prestazioni]**. I dettagli, compresi clic e impression, vengono visualizzati come linee di tendenza di un grafico.

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >A differenza dei dati nella sezione Soluzioni, la sezione Statistiche di prestazioni visualizza i dati più recenti.

1. Per ottenere il codice di incorporamento della risorsa da includere nei siti Web per ottenere i dati sulle prestazioni, fai clic su **[!UICONTROL Ottieni codice di incorporamento]** sotto la miniatura della risorsa. Per ulteriori informazioni su come includere il codice da incorporare nelle pagine Web di terze parti, consulta [Utilizzo del tracciamento delle pagine e del codice di incorporamento nelle pagine web](/help/assets/use-page-tracker.md).

   ![chlimage_1-98](assets/chlimage_1-303.png)

## Visualizzare le statistiche di aggregazione per le immagini {#viewing-aggregate-statistics-for-images}

Dalla **[!UICONTROL Visualizzazione approfondimenti]** puoi visualizzare simultaneamente un punteggio di tutte le risorse presenti all’interno di una cartella.

1. In [!DNL Assets] nell’interfaccia utente, passa alla cartella contenente le risorse per le quali desideri visualizzare le informazioni.
1. Fare clic su Layout nella barra degli strumenti, quindi scegliere **[!UICONTROL Visualizzazione approfondimenti]**.
1. Nella pagina vengono visualizzati i punteggi di utilizzo delle risorse. Confronta le valutazioni delle varie risorse e trae informazioni.

## Pianifica processo in background {#scheduling-background-job}

Assets Insights recupera periodicamente i dati di utilizzo delle risorse dalle suite di rapporti di Adobe Analytics. Per impostazione predefinita, Assets Insights esegue un processo in background ogni 24 ore alle 2 del mattino per recuperare i dati. Tuttavia, è possibile modificare sia la frequenza che l&#39;ora configurando **[!UICONTROL Processo di sincronizzazione report prestazioni risorse DAM Adobe CQ]** dalla console web.

1. Fai clic su [!DNL Experience Manager] e vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console web]**.
1. Apri **[!UICONTROL Processo di sincronizzazione report prestazioni risorse DAM Adobe CQ]** configurazione del servizio.

   ![chlimage_1-99](assets/chlimage_1-304.png)

1. Specifica la frequenza di pianificazione desiderata e l&#39;ora di inizio per il processo nell&#39;espressione di pianificazione delle proprietà. Salva le modifiche.
