---
title: Gestire le risorse video
description: Caricare, visualizzare in anteprima, annotare e pubblicare risorse video in [!DNL Adobe Experience Manager].
contentOwner: AG
role: User
feature: Asset Management
exl-id: 21d3e0bd-5955-470a-8ca2-4d995c17eb4c
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 8%

---

# Gestire le risorse video {#manage-video-assets}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/manage-video-assets.html?lang=en) |
| AEM 6.5 | Questo articolo |
| AEM 6.4 | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-64/assets/managing/managing-video-assets.html?lang=en) |

Il formato video è una parte fondamentale delle risorse digitali di un&#39;organizzazione. [!DNL Adobe Experience Manager] offre offerte e funzionalità mature per gestire l’intero ciclo di vita delle risorse video dopo la loro creazione.

Scopri come gestire e modificare le risorse video in [!DNL Adobe Experience Manager Assets]. La codifica e la transcodifica video, ad esempio la transcodifica FFmpeg, è possibile utilizzando [!DNL Dynamic Media] integrazione.

## Caricare e visualizzare in anteprima le risorse video {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] genera le anteprime per le risorse video con l’estensione MP4. Se il formato della risorsa non è MP4, installa il pacchetto FFmpeg per generare un&#39;anteprima. FFmpeg crea rappresentazioni video di tipo OGG e MP4. È possibile visualizzare in anteprima le rappresentazioni nel [!DNL Assets] interfaccia utente.

1. Nella cartella o nelle sottocartelle delle risorse digitali, individua il percorso in cui desideri aggiungere le risorse digitali.
1. Per caricare la risorsa, fai clic su **[!UICONTROL Crea]** dalla barra degli strumenti e scegli **[!UICONTROL File]**. In alternativa, trascinare un file sull’interfaccia utente. Vedi [caricare le risorse](manage-assets.md#uploading-assets) per i dettagli.
1. Per visualizzare un video in anteprima nella vista a schede, fai clic sul pulsante **[!UICONTROL Play]** ![opzione di riproduzione](assets/do-not-localize/play.png) sulla risorsa video. È possibile mettere in pausa o riprodurre video solo nella vista a schede. La [!UICONTROL Play] e [!UICONTROL Pausa] le opzioni non sono disponibili nella vista a elenco.

1. Per visualizzare l’anteprima del video nella pagina dei dettagli della risorsa, fai clic su **[!UICONTROL Modifica]** sulla carta. Il video viene riprodotto nel lettore video nativo del browser. È possibile riprodurre, mettere in pausa, controllare il volume e ingrandire il video a schermo intero.

   ![Controlli di riproduzione video](assets/video-playback-controls.png)

## Configurazione per caricare risorse di dimensioni superiori a 2 GB {#configuration-to-upload-assets-that-are-larger-than-gb}

Per impostazione predefinita, [!DNL Assets] non consente di caricare risorse di dimensioni superiori a 2 GB a causa di un limite di dimensione del file. Tuttavia, puoi sovrascrivere questo limite andando in CRXDE Lite e creando un nodo sotto il `/apps` directory. Il nodo deve avere lo stesso nome del nodo, la struttura della directory e le proprietà del nodo confrontabili dell&#39;ordine.

Oltre a [!DNL Assets] configurazione, modifica le seguenti configurazioni per caricare risorse di grandi dimensioni:

* Aumenta il tempo di scadenza del token. Vedi [!UICONTROL Servlet CSRF Granite Adobe] nella console Web all&#39;indirizzo `https://[aem_server]:[port]/system/console/configMgr`. Per ulteriori informazioni, consulta [Protezione CSRF](/help/sites-developing/csrf-protection.md).
* Aumenta il `receiveTimeout` nella configurazione del Dispatcher. Per ulteriori informazioni, consulta [Configurazione di Experience Manager Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options).

>[!NOTE]
>
>La [!DNL Experience Manager] L&#39;interfaccia utente classica non ha un limite di dimensione del file di 2 GB. Inoltre, il flusso di lavoro end-to-end per video di grandi dimensioni non è completamente supportato.

Per configurare un limite di dimensione file più elevato, esegui i seguenti passaggi nel `/apps` directory.

1. In [!DNL Experience Manager], fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL CRXDE Lite]**.
1. In CRXDE Lite, passa a `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`. Per visualizzare la finestra della directory, fai clic sul pulsante `>>`.
1. Dalla barra degli strumenti, fai clic sul pulsante **[!UICONTROL Nodo di sovrapposizione]**. In alternativa, seleziona **[!UICONTROL Sovrapponi nodo]** dal menu di scelta rapida.
1. In **[!UICONTROL Nodo di sovrapposizione]** finestra di dialogo, fai clic su **[!UICONTROL OK]**.

   ![nodo di sovrapposizione](assets/overlay-node-path.png)

1. Aggiorna il browser. Il nodo di sovrapposizione `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` è selezionato.
1. In **[!UICONTROL Proprietà]** immetti il valore appropriato in byte per aumentare il limite di dimensione alle dimensioni desiderate. Ad esempio, per aumentare il limite di dimensione a 30 GB, immetti `32212254720` valore.

1. Dalla barra degli strumenti, fai clic su **[!UICONTROL Salva tutto]**.
1. In [!DNL Experience Manager], fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console web]**.
1. Sulla [!DNL Adobe Experience Manager] [!UICONTROL Bundle della console Web] nella colonna Nome della tabella individuare e fare clic su **[!UICONTROL Adobe Granite Workflow External Process Job Handler]**.
1. Sulla [!UICONTROL Adobe Granite Workflow External Process Job Handler] imposta i secondi per entrambi **[!UICONTROL Timeout predefinito]** e **[!UICONTROL Timeout massimo]** campi `18000` (cinque ore). Fai clic su **[!UICONTROL Salva]**.
1. In [!DNL Experience Manager], fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.
1. Nella pagina Modelli di flusso di lavoro , seleziona **[!UICONTROL Codifica video Dynamic Media]**, quindi fai clic su **[!UICONTROL Modifica]**.
1. Nella pagina del flusso di lavoro, fai doppio clic sul pulsante **[!UICONTROL Processo di Dynamic Media Video Service]** componente.
1. Nella finestra di dialogo [!UICONTROL Step Properties (Proprietà passo)], nella scheda **[!UICONTROL Common (Comune)]**, espandi **Impostazioni avanzate**.
1. In **[!UICONTROL Timeout]** campo , specifica un valore di `18000`, quindi fai clic su **[!UICONTROL OK]** per tornare al **[!UICONTROL Codifica video Dynamic Media]** pagina del flusso di lavoro.
1. Vicino alla parte superiore della pagina, sotto il [!UICONTROL Codifica video Dynamic Media] titolo della pagina, fai clic su **[!UICONTROL Salva]**.

## Pubblicare risorse video {#publish-video-assets}

Dopo la pubblicazione, puoi includere le risorse video in una pagina web come URL o incorporarle direttamente. Per maggiori dettagli, vedi [pubblicare risorse Dynamic Media](/help/assets/publishing-dynamicmedia-assets.md).

## Annotare risorse video {#annotate-video-assets}

1. Da [!DNL Assets] console, seleziona **[!UICONTROL Modifica]** nella scheda della risorsa per visualizzare la pagina dei dettagli della risorsa.
1. Per riprodurre il video, fai clic su **[!UICONTROL Anteprima]**.
1. Per annotare il video, fai clic su **[!UICONTROL Annota]**. Viene aggiunta un’annotazione alla data e all’ora specifiche (fotogramma) del video. Durante l&#39;annotazione, potete disegnare sull&#39;area di lavoro e includere un commento nel disegno. I commenti vengono salvati automaticamente. Per uscire dalla procedura guidata dell’annotazione, fai clic su **[!UICONTROL Chiudi]**.

   ![Disegnare e annotare su un fotogramma video](assets/annotate-video.png)

1. Individua un punto specifico del video, specifica il tempo in secondi nel campo di **testo**, infine fai clic su **Jump (Passa a)**. Ad esempio, per saltare i primi 20 secondi del video, inserisci 20 nel campo di testo.

   ![Cerca un&#39;ora in un video da saltare per secondi specificati](assets/seek-in-video.png)

1. Per visualizzarlo nella timeline, fate clic su un’annotazione. Per eliminare l’annotazione dalla timeline, fai clic su **[!UICONTROL Elimina]**.

   ![Visualizzare annotazioni e dettagli nella timeline](assets/timeline-view-annotation.png)

>[!MORELIKETHIS]
>
>* [Gestione delle risorse digitali in Experience Manager Assets](/help/assets/manage-assets.md)
>* [Gestire le raccolte in Experience Manager Assets](/help/assets/manage-collections.md)
>* [Documentazione video Dynamic Media](/help/assets/video.md).

