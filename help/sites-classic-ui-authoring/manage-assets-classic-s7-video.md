---
title: Video in Sites Classic Authoring
description: Assets offre la gestione centralizzata delle risorse video, in cui puoi caricare i video direttamente in Assets per la codifica automatica in Dynamic Media Classic e accedere ai video giornalieri direttamente da Assets per l’authoring delle pagine.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: dfaa4b3f-f65a-4fe3-87a7-f3bc71015e56
exl-id: c540aa49-9981-4e8c-97df-972085b26490
source-git-commit: 59e182c165f6fd4b822eaf0e34f6e4b3bb18eb14
workflow-type: tm+mt
source-wordcount: '1682'
ht-degree: 26%

---

# Video{#video}

Le risorse forniscono una gestione centralizzata delle risorse video in cui puoi caricare i video direttamente in Assets per la codifica automatica in Dynamic Media Classic e accedere ai video Dynamic Media Classic direttamente da Assets per l’authoring delle pagine.

L&#39;integrazione video di Dynamic Media Classic estende la portata del video ottimizzato a tutti gli schermi (rilevamento automatico di dispositivi e larghezza di banda).

* Il componente video Dynamic Media Classic esegue automaticamente il rilevamento del dispositivo e della larghezza di banda per riprodurre il formato e la qualità video corretti su desktop, tablet e dispositivi mobili.
* Risorse: è possibile includere set di video adattivi anziché risorse con un singolo video. Un set video adattivo è un contenitore per tutte le rappresentazioni video necessarie per riprodurre il video in modo fluido su più schermi. Un set video adattivo raggruppa le versioni dello stesso video che sono codificate in diversi formati e bit rate, ad esempio 400 kbps, 800 kbps e 1000 kbps. Utilizzi un set video adattivo, insieme al componente video S7, per lo streaming video adattivo su più schermi, tra cui dispositivi mobili desktop, iOS, Android™, BlackBerry® e Windows. Consulta [Per ulteriori informazioni, consulta la documentazione di Dynamic Media Classic sui set video adattivi](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/video/quick-start-video.html#video).

## Informazioni su FFMPEG e Dynamic Media Classic {#about-ffmpeg-and-scene}

Il processo di codifica video predefinito si basa sull’utilizzo dell’integrazione con i profili video basata su FFMPEG. Pertanto, il [!UICONTROL Aggiorna risorsa DAM] il flusso di lavoro contiene i due passaggi seguenti, basati su ffmpeg:

* Miniature FFMPEG
* Codifica FFMPEG

L’abilitazione e la configurazione dell’integrazione di Dynamic Media Classic non rimuovono o disattivano automaticamente questi due passaggi del flusso di lavoro dalla configurazione standard [!UICONTROL Aggiorna risorsa DAM] flusso di lavoro di acquisizione. Se in Adobe Experience Manager utilizzi già la codifica video basata su FFMPEG, è probabile che negli ambienti di authoring sia installato FFMPEG. In questo caso, un nuovo video acquisito utilizzando Experience Manager Assets viene codificato due volte: una volta dal codificatore FFMPEG e una volta dall’integrazione Dynamic Media Classic.

Se hai configurato la codifica video basata su FFMPEG in Experience Manager e hai installato FFMPEG, Adobe consiglia di rimuovere i due flussi di lavoro FFMPEG dal [!UICONTROL Aggiorna risorsa DAM] flussi di lavoro.

### Formati supportati {#supported-formats}

Per il componente Video Dynamic Media Classic sono supportati i seguenti formati:

* F4V H.264
* MP4 H.264

### Decidi dove caricare il video {#deciding-where-to-upload-your-video}

La decisione su dove caricare le risorse video dipende da quanto segue:

* Hai bisogno di un flusso di lavoro per la risorsa video?
* Hai bisogno della funzione di controllo delle versioni per la risorsa video?

Se la risposta è “sì” ad almeno una di queste domande, carica il video direttamente in Adobe DAM. Se la risposta è &quot;no&quot; a entrambe le domande, carica il video direttamente in Dynamic Media Classic. Il flusso di lavoro per ogni scenario è descritto nella sezione seguente.

#### Se stai caricando il video direttamente in Adobe Assets {#if-you-are-uploading-your-video-directly-to-adobe-assets}

Se hai bisogno di un flusso di lavoro o della gestione delle versioni per le tue risorse, devi prima caricarle in Adobe Assets. Di seguito è riportato il flusso di lavoro consigliato:

1. Carica la risorsa video in Adobe Assets, quindi codifica e pubblica automaticamente in Dynamic Media Classic.
1. Ad Experience Manager, accedi alle risorse video in WCM nella sezione **[!UICONTROL Filmati]** della finestra di dialogo Content Finder.
1. Crea con video Dynamic Media Classic o componente video di base.

#### Se stai caricando il tuo video su Dynamic Media Classic {#if-you-are-uploading-your-video-to-scene}

Se non hai bisogno di un flusso di lavoro o di un controllo delle versioni per le risorse, carica le risorse in Dynamic Media Classic. Di seguito è riportato il flusso di lavoro consigliato:

1. Nell’app desktop Dynamic Media Classic, [configurare un caricamento e una codifica FTP pianificati per Dynamic Media Classic (sistema automatizzato)](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/uploading-files.html#upload-options).
1. Ad Experience Manager, accedi alle risorse video in WCM nella sezione **[!UICONTROL Dynamic Media Classic]** della finestra di dialogo Content Finder.
1. Creare con il componente video Dynamic Media Classic.

### Configurare l’integrazione con Dynamic Media Classic Video {#configuring-integration-with-scene-video}

1. In entrata **[!UICONTROL Cloud Services]**, passare al **[!UICONTROL Dynamic Media Classic]** configurazione e selezione **[!UICONTROL Modifica]**.
1. Seleziona la scheda **[!UICONTROL Video]**.

   >[!NOTE]
   >
   >La scheda **[!UICONTROL Video]** non viene visualizzata se la pagina non ha una configurazione cloud. Consulta [Abilita Dynamic Media Classic per WCM](#enablingscene7forwcm).

1. Seleziona il profilo di codifica video adattivo, uno dei profili di codifica per video singolo preconfigurati oppure un profilo di codifica video personalizzato.

   >[!NOTE]
   >
   >Per ulteriori informazioni sul significato dei predefiniti video, consultate [Predefiniti video per la codifica di file video](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html#video-presets-for-encoding-video-files).
   >
   >Adobe consiglia di selezionare entrambi i set video adattivi per la configurazione dei predefiniti universali o di selezionare l’opzione **[!UICONTROL Codifica video adattiva]**.

1. I profili di codifica selezionati vengono applicati automaticamente a tutti i video caricati nella cartella di destinazione CQ DAM configurata per questa configurazione cloud di Dynamic Media Classic. Puoi impostare più configurazioni cloud di Dynamic Media Classic con diverse cartelle di destinazione per applicare diversi profili di codifica, in base alle esigenze.

### Aggiornamento del visualizzatore e dei predefiniti di codifica {#updating-viewer-and-encoding-presets}

Aggiorna il visualizzatore e i predefiniti di codifica per il video in Experience Manager se i predefiniti sono stati aggiornati in Dynamic Media Classic. In questo caso, accedi alla configurazione Dynamic Media Classic nella configurazione cloud e seleziona **Aggiornare il visualizzatore e i predefiniti di codifica**.

![chlimage_1-131](assets/chlimage_1-131.png)

### Carica il video sorgente principale {#uploading-your-master-video}

Per caricare il video sorgente principale su Dynamic Media Classic da Adobe DAM:

1. Passa alla cartella di destinazione CQ DAM in cui hai impostato la configurazione cloud con i profili di codifica Dynamic Media Classic.
1. Seleziona **[!UICONTROL Carica]** per caricare il video sorgente principale. Il caricamento e la codifica del video vengono completati dopo il [!UICONTROL Aggiorna risorsa DAM] il flusso di lavoro è completo e **[!UICONTROL Pubblica su Dynamic Media Classic]** ha un segno di spunta.

   >[!NOTE]
   >
   >La generazione delle miniature video potrebbe richiedere del tempo.

   Quando trascini il video sorgente principale DAM sul componente video, questo vi accede *tutto* Rappresentazioni proxy con codifica Dynamic Media Classic per la distribuzione.

### Componente video di base e componente video Dynamic Media Classic {#foundation-video-component-versus-scene-video-component}

Quando utilizzi Experience Manager, puoi accedere sia al componente Video disponibile in Sites che al componente video Dynamic Media Classic. Questi componenti non sono intercambiabili.

Il componente video Dynamic Media Classic funziona solo per i video Dynamic Media Classic. Il componente base funziona con i video memorizzati da Experience Manager (utilizzando ffmpeg) e Dynamic Media Classic.

La matrice seguente spiega quando utilizzare questi componenti:

![chlimage_1-132](assets/chlimage_1-132.png)

>[!NOTE]
>
>Il componente video Dynamic Media Classic utilizza come predefinito il profilo video universale. È tuttavia possibile ottenere il lettore video basato su HTML5 per l&#39;utilizzo da parte di Experience Manager. In Dynamic Media Classic, copia il codice da incorporare del lettore video predefinito di HTML5 e inseriscilo nella pagina di Experience Manager.

## Componente video Experience Manager {#aem-video-component}

Anche se l’utilizzo del componente Video di Dynamic Media Classic è consigliato per la visualizzazione dei video Dynamic Media Classic, in questa sezione viene descritto come utilizzare i video Dynamic Media Classic con [!UICONTROL Componente video di base] ad Experience Manager per completezza.

### Confronto tra video Experience Manager e video Dynamic Media Classic {#aem-video-and-scene-video-comparison}

La tabella seguente fornisce un confronto ad alto livello delle funzionalità supportate tra il componente Video di base di Experience Manager e il componente Video di Dynamic Media Classic:

|  | Video di Experience Manager Foundation | Video Dynamic Media Classic |
|---|---|---|
| Approccio | Primo approccio HTML5. Flash viene utilizzato solo per il fallback non HTML5. | Flash è utilizzato sulla maggior parte dei computer desktop. HTML5 è usato per dispositivi mobili e tablet. |
| Distribuzione | Progressivo | Streaming adattivo |
| Tracciamento | Sì | Sì |
| Estensibilità | Sì | No |
| Video mobile | Sì | Yes |

### Configurazione {#setting-up}

#### Creare profili video {#creating-video-profiles}

Le varie codifiche video vengono create in base ai predefiniti di codifica Dynamic Media Classic selezionati nella configurazione cloud di Dynamic Media Classic. Affinché il componente video di base possa utilizzarli, è necessario creare un profilo video per ogni predefinito di codifica Dynamic Media Classic selezionato. Consente al componente video di selezionare le relative rappresentazioni DAM.

>[!NOTE]
>
>Per la pubblicazione, i nuovi profili video e le relative modifiche devono essere attivati.

1. Ad Experience Manager, vai a **[!UICONTROL Strumenti]**, quindi seleziona **[!UICONTROL Console di configurazione]**.
1. Nella console di configurazione, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili video]** nella struttura di navigazione.
1. Crea un profilo video Dynamic Media Classic. In **[!UICONTROL Nuovo]** menu, seleziona **[!UICONTROL Crea pagina]**.
1. Seleziona il modello di profilo Video Dynamic Media Classic. Assegna un nome alla nuova pagina del profilo video e seleziona **[!UICONTROL Crea]**.

   ![chlimage_1-133](assets/chlimage_1-133.png)

1. Modifica il nuovo profilo video. Seleziona prima la configurazione cloud. Quindi seleziona lo stesso predefinito di codifica selezionato nella configurazione cloud.

   ![chlimage_1-134](assets/chlimage_1-134.png)

   | Proprietà | Descrizione |
   |---|---|
   | Configurazione cloud Dynamic Media Classic | Configurazione cloud da utilizzare per i predefiniti di codifica. |
   | Predefinito di codifica Dynamic Media Classic | Predefinito di codifica con cui mappare questo profilo video. |
   | Tipo video HTML5 | Questa proprietà consente di impostare il valore della proprietà type dell&#39;elemento sorgente video HTML5. Queste informazioni non vengono fornite dai predefiniti di codifica Dynamic Media Classic, ma sono necessarie per il corretto rendering dei video tramite l’elemento video HTML5. Viene fornito un elenco dei formati più comuni, che può tuttavia essere sovrascritto per altri formati. |

   Ripeti questo passaggio per tutti i predefiniti di codifica selezionati nella configurazione cloud da usare nel componente video.

#### Configura progettazione {#configuring-design}

Il componente video di base deve sapere quali profili video utilizzare per creare l’elenco di sorgenti video. Apri la finestra di dialogo di progettazione dei componenti video e configura la progettazione dei componenti per l’utilizzo dei nuovi profili video.

>[!NOTE]
>
>Se utilizzi il componente video di base su una pagina mobile, ripeti questi passaggi nella progettazione della pagina mobile.

>[!NOTE]
>
>Le modifiche apportate alla progettazione richiedono l’attivazione della progettazione per avere effetto al momento della pubblicazione.

1. Apri la finestra di dialogo di progettazione del componente video di base e passa alla scheda **[!UICONTROL Profili]**. Quindi elimina i profili predefiniti e aggiungi i nuovi profili video Dynamic Media Classic. L’ordine dell’elenco dei profili nella finestra di dialogo per progettazione definisce anche l’ordine dell’elemento sorgenti video durante il rendering.
1. Per i browser che non supportano HTML5, il componente Video consente di configurare un fallback flash. Apri la finestra di dialogo di progettazione dei componenti video e passa alla scheda **[!UICONTROL Flash]**. Configura le impostazioni del lettore Flash e assegna un profilo di fallback per il lettore Flash.

#### Elenco di controllo {#checklist}

1. Creare una configurazione cloud di Dynamic Media Classic. Assicurati che i predefiniti di codifica video siano impostati e che l’importazione sia in esecuzione.
1. Crea un profilo video Dynamic Media Classic per ogni predefinito di codifica video selezionato nella configurazione cloud.
1. I profili video devono essere attivati.
1. Configura la struttura del componente video di base sulla pagina.
1. Dopo aver apportato le modifiche, attiva la progettazione.
