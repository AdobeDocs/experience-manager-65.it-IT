---
title: Approfondimenti Assets
description: Scopri come la funzione Approfondimenti di Assets consente di monitorare le valutazioni degli utenti e le statistiche di utilizzo delle immagini utilizzate in siti web di terze parti, campagne di marketing e soluzioni creative di Adobe.
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

# Approfondimenti Assets {#asset-insights}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/assets-insights.html?lang=it) |
| AEM 6.5 | Questo articolo |

La funzione Approfondimenti di Assets consente di monitorare le valutazioni degli utenti e le statistiche di utilizzo delle immagini utilizzate in siti web di terze parti, campagne di marketing e soluzioni creative di Adobe. Consente di ricavare informazioni sulla loro performance e popolarità.

[!DNL Assets] Insights acquisisce i dettagli dell&#39;attività dell&#39;utente, ad esempio il numero di volte in cui un&#39;immagine viene valutata, cliccata e impressioni (il numero di volte in cui un&#39;immagine viene caricata sul sito Web). Assegna punteggi alle immagini in base a queste statistiche. Puoi utilizzare i punteggi e le statistiche sulle prestazioni per selezionare le immagini più comuni da includere in cataloghi, campagne di marketing e così via. È inoltre possibile formulare criteri di archiviazione e rinnovo delle licenze in base a tali statistiche.

Affinché [!DNL Assets] Insights possa acquisire le statistiche di utilizzo delle immagini da un sito Web, è necessario includere il codice di incorporamento dell&#39;immagine nel codice del sito Web.

Per consentire a Assets Insights di visualizzare le statistiche di utilizzo delle risorse, configura innanzitutto la funzione per recuperare i dati di reporting da Adobe Analytics. Per ulteriori dettagli, vedere [Configurare Assets Insights](/help/assets/configure-asset-insights.md). Per utilizzare questa funzionalità in un&#39;installazione locale, acquistare separatamente la licenza [!DNL Adobe Analytics]. I clienti su [!DNL Managed Services] ricevono [!DNL Analytics] licenza in bundle con [!DNL Experience Manager]. Vedi [descrizione del prodotto Managed Services](https://helpx.adobe.com/it/legal/product-descriptions/adobe-experience-manager-managed-services.html).

>[!NOTE]
>
>Gli approfondimenti sono supportati e forniti solo per le immagini.

## Visualizzare le statistiche di un’immagine {#viewing-statistics-for-an-image}

Puoi visualizzare i punteggi di Assets Insights dalla pagina dei metadati.

1. Dall&#39;interfaccia utente di [!DNL Assets], selezionare l&#39;immagine e quindi fare clic su **[!UICONTROL Proprietà]** nella barra degli strumenti.
1. Dalla pagina Proprietà, fai clic sulla scheda **[!UICONTROL Informazioni]**.
1. Rivedi i dettagli di utilizzo della risorsa nella scheda **[!UICONTROL Informazioni]**. La sezione **[!UICONTROL Punteggio]** descrive l&#39;utilizzo totale delle risorse e l&#39;andamento delle prestazioni di una risorsa.

   Il punteggio di utilizzo descrive il numero di volte in cui la risorsa viene utilizzata in varie soluzioni.

   Il punteggio **[!UICONTROL Impression]** è il numero di volte in cui la risorsa viene caricata sul sito Web. Il numero visualizzato in **[!UICONTROL Clic]** è il numero di volte in cui si fa clic sulla risorsa.

1. Rivedi la sezione **[!UICONTROL Statistiche di utilizzo]** per sapere di quali entità faceva parte la risorsa e quali soluzioni creative l&#39;hanno utilizzata di recente. Maggiore è l’utilizzo, maggiori sono le probabilità che la risorsa sia popolare tra gli utenti. I dati di utilizzo vengono visualizzati sotto le seguenti intestazioni:

   * **Risorsa**: il numero di volte in cui la risorsa faceva parte di una raccolta o di una risorsa composta
   * **Web e dispositivi mobili**: il numero di volte in cui la risorsa faceva parte di siti Web e app
   * **Social**: il numero di volte in cui la risorsa è stata utilizzata nelle soluzioni, ad esempio Adobe Social e Adobe Campaign
   * **E-mail**: il numero di volte in cui la risorsa è stata utilizzata nelle campagne e-mail

   ![statistiche_di_utilizzo](assets/usage_statistics.png)

   >[!NOTE]
   >
   >Poiché la funzione Approfondimenti di Assets in genere recupera i dati delle soluzioni da Adobe Analytics in modo periodico, nella sezione Soluzioni potrebbe non essere visualizzato quello più recente. Il periodo di tempo per il quale vengono visualizzati i dati dipende dalla pianificazione dell’operazione di recupero eseguita da Assets Insights per recuperare i dati di Analytics.

1. Per visualizzare graficamente le statistiche sulle prestazioni della risorsa in un arco di tempo, seleziona il periodo nella sezione **[!UICONTROL Statistiche di prestazioni]**. I dettagli, compresi clic e impression, vengono visualizzati come linee di tendenza di un grafico.

   ![chlimage_1-3](assets/chlimage_1-3.jpeg)

   >[!NOTE]
   >
   >A differenza dei dati nella sezione Soluzioni, la sezione Statistiche di prestazioni visualizza i dati più recenti.

1. Per ottenere il codice di incorporamento per la risorsa inclusa nei siti Web per ottenere i dati sulle prestazioni, fai clic su **[!UICONTROL Ottieni codice di incorporamento]** sotto la miniatura della risorsa. Per ulteriori informazioni su come includere il codice da incorporare nelle pagine Web di terze parti, vedere [Utilizzo di Tracciamento pagina e codice da incorporare nelle pagine Web](/help/assets/use-page-tracker.md).

   ![chlimage_1-98](assets/chlimage_1-303.png)

## Visualizzare le statistiche di aggregazione per le immagini {#viewing-aggregate-statistics-for-images}

Dalla **[!UICONTROL Visualizzazione approfondimenti]** puoi visualizzare simultaneamente un punteggio di tutte le risorse presenti all’interno di una cartella.

1. Nell&#39;interfaccia utente di [!DNL Assets], passa alla cartella contenente le risorse per le quali desideri visualizzare le informazioni.
1. Fare clic su Layout nella barra degli strumenti, quindi scegliere **[!UICONTROL Visualizzazione approfondimenti]**.
1. Nella pagina vengono visualizzati i punteggi di utilizzo delle risorse. Confronta le valutazioni delle varie risorse e trae informazioni.

## Pianifica processo in background {#scheduling-background-job}

Assets Insights recupera periodicamente i dati di utilizzo delle risorse dalle suite di rapporti di Adobe Analytics. Per impostazione predefinita, Assets Insights esegue un processo in background ogni 24 ore alle 2 del mattino per recuperare i dati. Tuttavia, puoi modificare sia la frequenza che l&#39;ora configurando il **[!UICONTROL processo di sincronizzazione report prestazioni risorse DAM Adobe CQ]** dalla console Web.

1. Fare clic sul logo [!DNL Experience Manager] e passare a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console Web]**.
1. Apri la configurazione del servizio **[!UICONTROL Adobe CQ DAM Asset Performance Report Sync Job]**.

   ![chlimage_1-99](assets/chlimage_1-304.png)

1. Specifica la frequenza di pianificazione desiderata e l&#39;ora di inizio per il processo nell&#39;espressione di pianificazione delle proprietà. Salva le modifiche.
