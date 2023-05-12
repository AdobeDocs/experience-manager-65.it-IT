---
title: Informazioni sulle risorse
description: Scopri come la funzione Assets Insights ti consente di monitorare le valutazioni degli utenti e le statistiche di utilizzo delle immagini utilizzate in siti web di terze parti, campagne di marketing e soluzioni creative di Adobe.
contentOwner: AG
role: User, Admin
feature: Asset Insights,Asset Reports
exl-id: 0130ac40-a72b-4caf-a10f-3c7d76eaa1e6
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 7%

---

# Informazioni sulle risorse {#asset-insights}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/assets-insights.html?lang=en) |
| AEM 6.5 | Questo articolo |

La funzione Assets Insights ti consente di monitorare le valutazioni degli utenti e le statistiche di utilizzo delle immagini utilizzate in siti web di terze parti, campagne di marketing e soluzioni creative di Adobe. Aiuta a trarre informazioni sulle loro prestazioni e popolarità.

[!DNL Assets] Insights acquisisce i dettagli dell’attività dell’utente, ad esempio il numero di volte in cui un’immagine viene valutata, su cui è stato fatto clic e le impression (numero di volte in cui un’immagine viene caricata sul sito web). Assegna punteggi alle immagini in base a queste statistiche. Puoi utilizzare i punteggi e le statistiche sulle prestazioni per selezionare le immagini più comuni da includere nei cataloghi, nelle campagne di marketing e così via. Puoi anche formulare politiche di archiviazione e rinnovo delle licenze basate su queste statistiche.

Per [!DNL Assets] Informazioni per acquisire le statistiche di utilizzo per le immagini da un sito web, è necessario includere il codice di incorporamento per l’immagine nel codice del sito web.

Per consentire a Assets Insights di visualizzare le statistiche di utilizzo delle risorse, configura prima la funzione per recuperare i dati di reporting da Adobe Analytics. Per maggiori dettagli, vedi [Configurare Assets Insights](/help/assets/configure-asset-insights.md). Per utilizzare questa funzione in un’installazione on-premise, acquista [!DNL Adobe Analytics] licenza separatamente. Clienti su [!DNL Managed Services] ricevere [!DNL Analytics] licenza abbinata a [!DNL Experience Manager]. Vedi [Descrizione del prodotto Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html).

>[!NOTE]
>
>Gli approfondimenti sono supportati e forniti solo per le immagini.

## Visualizzare le statistiche per un’immagine {#viewing-statistics-for-an-image}

Puoi visualizzare i punteggi di Assets Insights dalla pagina dei metadati.

1. Da [!DNL Assets] interfaccia utente, seleziona l’immagine e fai clic su **[!UICONTROL Proprietà]** dalla barra degli strumenti.
1. Dalla pagina Proprietà , fai clic sul pulsante **[!UICONTROL Informazioni approfondite]** scheda .
1. Esamina i dettagli di utilizzo della risorsa nella sezione **[!UICONTROL Informazioni approfondite]** scheda . La **[!UICONTROL Punteggio]** la sezione descrive l’utilizzo totale delle risorse e le origini delle prestazioni di una risorsa .

   Il punteggio di utilizzo descrive il numero di volte in cui la risorsa viene utilizzata in varie soluzioni.

   La **[!UICONTROL Impressioni]** punteggio è il numero di volte in cui la risorsa viene caricata sul sito web. Numero visualizzato sotto **[!UICONTROL Clic]** è il numero di volte in cui viene fatto clic sulla risorsa.

1. Consulta la sezione **[!UICONTROL Statistiche di utilizzo]** per sapere di quali entità faceva parte la risorsa e quali soluzioni creative l’ha utilizzata di recente. Maggiore è l’utilizzo, maggiori sono le probabilità che la risorsa sia popolare tra gli utenti. I dati di utilizzo vengono visualizzati sotto le seguenti intestazioni:

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

1. Per ottenere il codice di incorporamento della risorsa inclusa nei siti web per ottenere i dati sulle prestazioni, fai clic su **[!UICONTROL Ottieni codice di incorporamento]** sotto la miniatura della risorsa. Per ulteriori informazioni su come includere il codice da incorporare in pagine web di terze parti, consulta [Utilizzo del tracciamento pagina e del codice di incorporamento nelle pagine web](/help/assets/use-page-tracker.md).

   ![chlimage_1-98](assets/chlimage_1-303.png)

## Visualizzare le statistiche aggregate per le immagini {#viewing-aggregate-statistics-for-images}

Dalla **[!UICONTROL Visualizzazione approfondimenti]** puoi visualizzare simultaneamente un punteggio di tutte le risorse presenti all’interno di una cartella.

1. In [!DNL Assets] nell’interfaccia utente , passa alla cartella contenente le risorse per le quali desideri visualizzare le informazioni.
1. Fare clic su Layout nella barra degli strumenti, quindi scegliere **[!UICONTROL Visualizzazione approfondimenti]**.
1. Nella pagina vengono visualizzati i punteggi di utilizzo delle risorse. Confronta le valutazioni delle varie risorse e trai informazioni approfondite.

## Pianifica processo in background {#scheduling-background-job}

Assets Insights recupera periodicamente i dati di utilizzo per le risorse dalle suite di rapporti di Adobe Analytics. Per impostazione predefinita, Assets Insights esegue un processo in background ogni 24 ore alle 2 del mattino fino ai dati di recupero. Tuttavia, puoi modificare sia la frequenza che il tempo configurando il **[!UICONTROL Processo di sincronizzazione dei rapporti sulle prestazioni delle risorse DAM di Adobe CQ]** servizio dalla console web.

1. Fai clic sul pulsante [!DNL Experience Manager] e vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console web]**.
1. Apri **[!UICONTROL Processo di sincronizzazione dei rapporti sulle prestazioni delle risorse DAM di Adobe CQ]** configurazione del servizio.

   ![chlimage_1-99](assets/chlimage_1-304.png)

1. Specifica la frequenza di pianificazione desiderata e l’ora di inizio del processo nell’espressione di pianificazione delle proprietà. Salva le modifiche.
