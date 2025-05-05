---
title: Video in Sites Classic Authoring
description: Assets fornisce la gestione centralizzata delle risorse video, in cui puoi caricare i video direttamente in Assets per la codifica automatica in Dynamic Media Classic e accedere ai video giornalieri direttamente da Assets per l’authoring delle pagine.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
exl-id: c540aa49-9981-4e8c-97df-972085b26490
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1662'
ht-degree: 1%

---

# Video{#video}

Assets fornisce la gestione centralizzata delle risorse video, in cui puoi caricare i video direttamente in Assets per la codifica automatica in Dynamic Media Classic e accedere ai video Dynamic Media Classic direttamente da Assets per l’authoring delle pagine.

L&#39;integrazione video Dynamic Media Classic estende la portata del video ottimizzato a tutti gli schermi (rilevamento automatico di dispositivi e larghezza di banda).

* Il componente video Dynamic Media Classic esegue automaticamente il rilevamento del dispositivo e della larghezza di banda per riprodurre il formato e la qualità video corretti su desktop, tablet e dispositivi mobili.
* Assets: puoi includere set di video adattivi anziché solo singole risorse video. Un set video adattivo è un contenitore per tutte le rappresentazioni video necessarie per riprodurre il video in modo fluido su più schermi. Un set video adattivo raggruppa le versioni dello stesso video che sono codificate in diversi formati e bit rate, ad esempio 400 kbps, 800 kbps e 1000 kbps. Utilizzi un set video adattivo, insieme al componente video S7, per lo streaming video adattivo su più schermi, inclusi desktop, iOS, Android™, BlackBerry® e dispositivi mobili Windows. Per ulteriori informazioni, consulta la [documentazione di Dynamic Media Classic sui set di video adattivi](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/video/quick-start-video.html?lang=it#video).

## Informazioni su FFMPEG e Dynamic Media Classic {#about-ffmpeg-and-scene}

Il processo di codifica video predefinito si basa sull’utilizzo dell’integrazione basata su FFMPEG con i profili video. Pertanto, il flusso di lavoro predefinito [!UICONTROL Risorsa di aggiornamento DAM] contiene i due passaggi seguenti del flusso di lavoro basati su ffmpeg:

* Miniature FFMPEG
* Codifica FFMPEG

L&#39;abilitazione e la configurazione dell&#39;integrazione di Dynamic Media Classic non rimuovono o disattivano automaticamente questi due passaggi del flusso di lavoro dal flusso di lavoro predefinito per l&#39;acquisizione di [!UICONTROL Risorsa di aggiornamento DAM]. Se in Adobe Experience Manager utilizzi già la codifica video basata su FFMPEG, è probabile che negli ambienti di authoring sia installato FFMPEG. In questo caso, un nuovo video acquisito utilizzando Experience Manager Assets viene codificato due volte: una volta dal codificatore FFMPEG e una volta dall’integrazione Dynamic Media Classic.

Se hai configurato la codifica video basata su FFMPEG in Experience Manager e hai installato FFMPEG, Adobe consiglia di rimuovere i due flussi di lavoro FFMPEG dai flussi di lavoro [!UICONTROL Risorsa di aggiornamento DAM].

### Formati supportati {#supported-formats}

Per il componente Video Dynamic Media Classic sono supportati i seguenti formati:

* F4V H.264
* MP4 H.264

### Decidi dove caricare il video {#deciding-where-to-upload-your-video}

La scelta del percorso in cui caricare le risorse video dipende da quanto segue:

* È necessario un flusso di lavoro per la risorsa video?
* È necessario il controllo della versione per la risorsa video?

Se la risposta è &quot;sì&quot; a una o entrambe queste domande, carica il video direttamente in Adobe DAM. Se la risposta è &quot;no&quot; a entrambe le domande, carica il video direttamente in Dynamic Media Classic. Il flusso di lavoro per ogni scenario è descritto nella sezione seguente.

#### Se carichi il video direttamente in Adobe Assets {#if-you-are-uploading-your-video-directly-to-adobe-assets}

Se hai bisogno di un flusso di lavoro o di un controllo delle versioni per le risorse, devi prima caricarlo in Adobe Assets. Di seguito è riportato il flusso di lavoro consigliato:

1. Carica la risorsa video in Adobe Assets e codificala e pubblicala automaticamente in Dynamic Media Classic.
1. Ad Experience Manager, accedi alle risorse video in WCM nella scheda **[!UICONTROL Filmati]** di Content Finder.
1. Crea con video Dynamic Media Classic o componente video di base.

#### Se stai caricando il tuo video su Dynamic Media Classic {#if-you-are-uploading-your-video-to-scene}

Se non hai bisogno di un flusso di lavoro o di un controllo delle versioni per le risorse, carica le risorse in Dynamic Media Classic. Di seguito è riportato il flusso di lavoro consigliato:

1. Nell&#39;app desktop Dynamic Media Classic, [configurare un caricamento e una codifica FTP pianificati in Dynamic Media Classic (sistema automatizzato)](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/uploading-files.html?lang=it#upload-options).
1. Ad Experience Manager, accedi alle risorse video in WCM nella scheda **[!UICONTROL Dynamic Media Classic]** di Content Finder.
1. Creare con il componente video Dynamic Media Classic.

### Configurare l’integrazione con Dynamic Media Classic Video {#configuring-integration-with-scene-video}

1. In **[!UICONTROL Cloud Service]**, passa alla configurazione di **[!UICONTROL Dynamic Media Classic]** e seleziona **[!UICONTROL Modifica]**.
1. Selezionare la scheda **[!UICONTROL Video]**.

   >[!NOTE]
   >
   >La scheda **[!UICONTROL Video]** non viene visualizzata se la pagina non dispone di una configurazione cloud. Vedere [Abilitare Dynamic Media Classic per WCM](#enablingscene7forwcm).

1. Seleziona il profilo di codifica video adattivo, un profilo di codifica video singolo predefinito o un profilo di codifica video personalizzato.

   >[!NOTE]
   >
   >Per ulteriori informazioni sul significato dei predefiniti video, vedere [Predefiniti video per la codifica dei file video](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html?lang=it#video-presets-for-encoding-video-files).
   >
   >L&#39;Adobe consiglia di selezionare entrambi i set di video adattivi durante la configurazione dei predefiniti universali o di selezionare l&#39;opzione **[!UICONTROL Codifica video adattivo]**.

1. I profili di codifica selezionati vengono applicati automaticamente a tutti i video caricati nella cartella di destinazione CQ DAM configurata per questa configurazione cloud di Dynamic Media Classic. Puoi impostare più configurazioni cloud di Dynamic Media Classic con diverse cartelle di destinazione per applicare diversi profili di codifica, in base alle esigenze.

### Aggiornamento del visualizzatore e dei predefiniti di codifica {#updating-viewer-and-encoding-presets}

Aggiorna il visualizzatore e i predefiniti di codifica per il video in Experience Manager se i predefiniti sono stati aggiornati in Dynamic Media Classic. In questo caso, passa alla configurazione Dynamic Media Classic nella configurazione cloud e seleziona **Aggiorna il visualizzatore e i predefiniti di codifica**.

![chlimage_1-131](assets/chlimage_1-131.png)

### Carica il video sorgente principale {#uploading-your-master-video}

Per caricare il video sorgente principale su Dynamic Media Classic da Adobe DAM:

1. Passa alla cartella di destinazione CQ DAM in cui hai impostato la configurazione cloud con i profili di codifica Dynamic Media Classic.
1. Seleziona **[!UICONTROL Carica]** per caricare il video di origine principale. Il caricamento e la codifica del video sono stati completati dopo il completamento del flusso di lavoro [!UICONTROL Risorsa di aggiornamento DAM] e dopo il segno di spunta **[!UICONTROL da Publish a Dynamic Media Classic]**.

   >[!NOTE]
   >
   >La generazione delle miniature video potrebbe richiedere del tempo.

   Quando trascini il video sorgente principale DAM sul componente video, questo accede a *tutte* le rappresentazioni proxy con codifica Dynamic Media Classic per la consegna.

### Componente video di base e componente video Dynamic Media Classic {#foundation-video-component-versus-scene-video-component}

Quando utilizzi Experience Manager, puoi accedere sia al componente Video disponibile in Sites che al componente video Dynamic Media Classic. Questi componenti non sono intercambiabili.

Il componente video Dynamic Media Classic funziona solo per i video Dynamic Media Classic. Il componente base funziona con i video memorizzati da Experience Manager (utilizzando ffmpeg) e Dynamic Media Classic.

La seguente matrice spiega quando utilizzare quale componente:

![chlimage_1-132](assets/chlimage_1-132.png)

>[!NOTE]
>
>Il componente video Dynamic Media Classic utilizza come predefinito il profilo video universale. È tuttavia possibile ottenere il lettore video basato su HTML5 per l&#39;utilizzo da parte di Experience Manager. In Dynamic Media Classic, copia il codice da incorporare del lettore video predefinito di HTML5 e inseriscilo nella pagina di Experience Manager.
>

## Componente video Experience Manager {#aem-video-component}

Anche se l&#39;utilizzo del componente video Dynamic Media Classic è consigliato per la visualizzazione dei video Dynamic Media Classic, in questa sezione viene descritto l&#39;utilizzo dei video Dynamic Media Classic con il [!UICONTROL componente video Foundation] nell&#39;Experience Manager per la completezza.

### Confronto tra video Experience Manager e video Dynamic Media Classic {#aem-video-and-scene-video-comparison}

La tabella seguente fornisce un confronto ad alto livello delle funzionalità supportate tra il componente Video di base di Experience Manager e il componente Video di Dynamic Media Classic:

|   | Video di Experience Manager Foundation | Video Dynamic Media Classic |
|---|---|---|
| Approccio | Primo avvicinamento HTML5. Il Flash viene utilizzato solo per il fallback non HTML5. | Flash sulla maggior parte dei desktop. HTML5 viene utilizzato per i dispositivi mobili e i tablet. |
| Distribuzione | Progressivo | Streaming adattivo |
| Tracciamento | Sì | Sì |
| Estensibilità | Sì | No |
| Video mobile | Sì | Sì |

### Configurazione {#setting-up}

#### Creare profili video {#creating-video-profiles}

Le varie codifiche video vengono create in base ai predefiniti di codifica Dynamic Media Classic selezionati nella configurazione cloud di Dynamic Media Classic. Affinché il componente video di base possa utilizzarli, è necessario creare un profilo video per ogni predefinito di codifica Dynamic Media Classic selezionato. Consente al componente video di selezionare le relative rappresentazioni DAM.

>[!NOTE]
>
>Per poter pubblicare, è necessario attivare nuovi profili video e le relative modifiche.

1. Ad Experience Manager, vai a **[!UICONTROL Strumenti]**, quindi seleziona **[!UICONTROL Console di configurazione]**.
1. Nella console di configurazione, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Profili video]** nella struttura di navigazione.
1. Crea un profilo video Dynamic Media Classic. Nel menu **[!UICONTROL Nuovo]**, seleziona **[!UICONTROL Crea pagina]**.
1. Seleziona il modello di profilo Video Dynamic Media Classic. Assegna un nome alla nuova pagina del profilo video e seleziona **[!UICONTROL Crea]**.

   ![chlimage_1-133](assets/chlimage_1-133.png)

1. Modifica il nuovo profilo video. Seleziona prima la configurazione cloud. Quindi seleziona lo stesso predefinito di codifica selezionato nella configurazione cloud.

   ![chlimage_1-134](assets/chlimage_1-134.png)

   | Proprietà | Descrizione |
   |---|---|
   | Configurazione cloud Dynamic Media Classic | Configurazione cloud da utilizzare per i predefiniti di codifica. |
   | Predefinito di codifica Dynamic Media Classic | Predefinito di codifica con cui mappare questo profilo video. |
   | Tipo video HTML5 | Questa proprietà consente di impostare il valore della proprietà type dell&#39;elemento sorgente video HTML5. Queste informazioni non vengono fornite dai predefiniti di codifica Dynamic Media Classic, ma sono necessarie per il corretto rendering dei video tramite l’elemento video HTML5. Viene fornito un elenco per i formati comuni, ma può essere sovrascritto per altri formati. |

   Ripeti questo passaggio per tutti i predefiniti di codifica selezionati nella configurazione cloud che desideri utilizzare nel componente video.

#### Configura progettazione {#configuring-design}

Il componente video di base deve sapere quali profili video utilizzare per creare l’elenco delle sorgenti video. Apri la finestra di dialogo di progettazione dei componenti video e configura la progettazione dei componenti per l’utilizzo dei nuovi profili video.

>[!NOTE]
>
>Se utilizzi il componente video di base su una pagina mobile, ripeti questi passaggi nella progettazione della pagina mobile.

>[!NOTE]
>
>Le modifiche apportate al progetto richiedono l’attivazione del progetto per avere effetto al momento della pubblicazione.

1. Apri la finestra di dialogo per progettazione del componente video di base e passa alla scheda **[!UICONTROL Profili]**. Quindi elimina i profili predefiniti e aggiungi i nuovi profili video Dynamic Media Classic. L’ordine dell’elenco dei profili nella finestra di dialogo per progettazione definisce anche l’ordine dell’elemento sorgenti video durante il rendering.
1. Per i browser che non supportano HTML5, il componente Video consente di configurare un fallback flash. Apri la finestra di dialogo di progettazione dei componenti video e passa alla scheda **[!UICONTROL Flash]**. Configura le impostazioni del lettore Flash e assegna un profilo di fallback al lettore Flash.

#### Elenco di controllo {#checklist}

1. Creare una configurazione cloud di Dynamic Media Classic. Assicurati che i predefiniti di codifica video siano impostati e che l’importazione sia in esecuzione.
1. Crea un profilo video Dynamic Media Classic per ogni predefinito di codifica video selezionato nella configurazione cloud.
1. È necessario attivare i profili video.
1. Configura la progettazione del componente video di base sulla pagina.
1. Attiva la progettazione al termine delle modifiche.
