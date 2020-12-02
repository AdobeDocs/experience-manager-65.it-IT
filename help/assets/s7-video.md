---
title: Video
description: Scopri la gestione centralizzata delle risorse video  AEM Assets, dove puoi caricare i video per la codifica automatica in Dynamic Media Classic e accedere ai video Dynamic Media Classic direttamente da  AEM Assets. L’integrazione video Dynamic Media Classic estende la portata dei video ottimizzati a tutti gli schermi.
uuid: 8b3423f1-d96b-44d9-bdb7-e3b77875b25d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: managing-assets
content-type: reference
discoiquuid: 2685f9f3-0973-40a9-89b8-e7db0a6a75f2
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '1627'
ht-degree: 55%

---


# Video {#video}

Risorse offre una gestione centralizzata delle risorse video in cui è possibile caricare i video direttamente su Risorse per la codifica automatica in Dynamic Media Classic (Scene7) e accedere ai video Dynamic Media Classic direttamente da Risorse per l’authoring delle pagine.

L’integrazione video Dynamic Media Classic estende la portata dei video ottimizzati a tutti gli schermi (rilevamento automatico della periferica e della larghezza di banda).

* Il componente **[!UICONTROL Scene7 Video]** esegue automaticamente il rilevamento del dispositivo e della larghezza di banda per riprodurre il formato corretto e la qualità video corretta su computer desktop, tablet e dispositivi mobili.
* Risorse: è possibile includere set di video adattivi anziché risorse con un singolo video. Un set di video adattivo è un contenitore di tutte le rappresentazioni video necessarie a consentirne la riproduzione su diversi tipi di schermi. Un set video adattivo raggruppa versioni dello stesso video codificate con diversi bitrate e formati quali 400, 800 e 1000 kbps. Utilizza un set video adattivo, insieme al componente video S7, per lo streaming video adattivo per schermi diversi, come computer desktop e dispositivi mobili iOS, Android, Blackberry e Windows. Per ulteriori informazioni, vedi [la documentazione di Scene7 sui set di video adattivi](https://help.adobe.com/en_US/scene7/using/WS53492AE1-6029-45d8-BF80-F4B5CF33EB08.html).

## Informazioni su FFMPEG e Dynamic Media Classic {#about-ffmpeg-and-scene}

Il processo di codifica video predefinito si basa sull’utilizzo dell’integrazione con i profili video basata su FFMPEG. Di conseguenza, il flusso di lavoro di assimilazione DAM predefinito contiene le due seguenti fasi del flusso di lavoro basate su ffmpeg:

* Miniature FFMPEG
* Codifica FFMPEG

Attenzione: l&#39;abilitazione e la configurazione dell&#39;integrazione di Dynamic Media Classic non rimuove o disattiva automaticamente questi due passaggi del flusso di lavoro dal flusso di lavoro di caricamento out-of-the-box DAM. Se utilizzi già la codifica video basata su FFMPEG in AEM, è probabile che FFMPEG sia già installato negli ambienti di authoring. In questo caso, un nuovo video caricato con DAM verrebbe codificato due volte: una volta dall&#39;encoder FFMPEG e una dall&#39;integrazione Dynamic Media Classic.

Se la codifica video basata su FFMPEG è configurata e installata in AEM,  Adobe consiglia di rimuovere i due flussi di lavoro FFMPEG dai flussi di lavoro di assimilazione DAM.

## Formati supportati {#supported-formats}

Il componente video Scene7 supporta i seguenti formati:

* F4V H.264
* MP4 H.264

## Decidere dove caricare il video {#deciding-where-to-upload-your-video}

La decisione su dove caricare le risorse video dipende da quanto segue:

* Hai bisogno di un flusso di lavoro per la risorsa video?
* Hai bisogno della funzione di controllo delle versioni per la risorsa video?

Se la risposta è “sì” ad almeno una di queste domande, carica il video direttamente in Adobe DAM. Se la risposta è &quot;no&quot; a entrambe le domande, caricate il video direttamente in Dynamic Media Classic. Il flusso di lavoro per ogni scenario è descritto nella sezione seguente.

### Se caricate il video direttamente in  Adobe DAM {#if-you-are-uploading-your-video-directly-to-adobe-dam}

Se avete bisogno di un flusso di lavoro o di un controllo delle versioni per le risorse, dovete prima caricare  Adobe DAM. Di seguito è riportato il flusso di lavoro consigliato:

1. Caricate la risorsa video in  Adobe DAM e codificatela e pubblicatela automaticamente in Dynamic Media Classic.
1. In AEM, accedi alle risorse video in WCM nella scheda **[!UICONTROL Filmati]** del Content Finder.
1. Creazione con il componente **[!UICONTROL Scene7 Video]** o **[!UICONTROL Foundation Video]**.

### Se stai caricando il video in Scene7 {#if-you-are-uploading-your-video-to-scene}

Se non hai bisogno di un flusso di lavoro o di gestire le versioni delle tue risorse, caricale in Scene7. Di seguito è riportato il flusso di lavoro consigliato:

1. In Dynamic Media Classic, [impostare un caricamento e una codifica FTP pianificati su Scene7 (automatizzato del sistema)](https://help.adobe.com/en_US/scene7/using/WS70B173EC-4CAD-4b4c-BF9C-43A11F3A5950.html).
1. In AEM, accedi alle risorse video in WCM della scheda **[!UICONTROL Scene7]** del Content Finder.
1. Creare contenuti con il componente **[!UICONTROL Scene7 Video]**.

## Configurazione dell’integrazione con video Scene7 {#configuring-integration-with-scene-video}

Per configurare i predefiniti universali:

1. In **[!UICONTROL Servizi cloud]**, accedi alla tua configurazione di **[!UICONTROL Scene7]** e fai clic su **[!UICONTROL Modifica.]**
1. Seleziona la scheda **[!UICONTROL Video]**.

   ![chlimage_1-363](assets/chlimage_1-363.png)

   >[!NOTE]
   >
   >La scheda **[!UICONTROL Video]** non viene visualizzata se la pagina non ha una configurazione cloud.

1. Seleziona il profilo di codifica video adattivo, uno dei profili di codifica per video singolo preconfigurati oppure un profilo di codifica video personalizzato.

   >[!NOTE]
   >
   >Per ulteriori informazioni sul significato dei predefiniti per video, consultate la [Documentazione di Dynamic Media Classic](https://help.adobe.com/en_US/scene7/using/WSE86ACF2B-BD50-4c48-A1D7-9CD4405B62D0.html).
   >
   >Adobe consiglia di selezionare entrambi i set video adattivi per la configurazione dei predefiniti universali o di selezionare l’opzione **[!UICONTROL Codifica video adattiva]**.

1. I profili di codifica selezionati vengono applicati automaticamente a tutti i video caricati nella cartella di destinazione CQ DAM impostata per questa configurazione cloud di Scene7. Puoi impostare più configurazioni cloud di Scene7 con diverse cartelle di destinazione, per applicare profili di codifica diversi a seconda delle esigenze.

## Aggiornamento del visualizzatore e dei predefiniti di codifica  {#updating-viewer-and-encoding-presets}

Se devi aggiornare il visualizzatore e i predefiniti di codifica video in AEM, perché i predefiniti sono stati aggiornati in Scene7, accedi alla configurazione di Scene7 nella configurazione del cloud, quindi fai clic su **[!UICONTROL Aggiorna visualizzatore e predefiniti di codifica.]**

![chlimage_1-364](assets/chlimage_1-364.png)

## Caricamento del video sorgente principale su Scene7 da  Adobe DAM {#uploading-your-master-video}

1. Individua la cartella di destinazione CQ DAM in cui hai impostato la configurazione cloud con i profili di codifica di Scene7.
1. Fate clic su **[!UICONTROL Carica]** per caricare il video sorgente principale. Il caricamento e la codifica dei video sono completati dopo il completamento del flusso di lavoro [!UICONTROL DAM Update Asset] e dopo che **[!UICONTROL Publish to Scene7]** ha un segno di spunta.

   >[!NOTE]
   >
   >La generazione delle miniature video potrebbe richiedere del tempo.

   Trascinate il video sorgente principale DAM sul componente video per accedere alle rappresentazioni proxy codificate Scene7 *all* per la distribuzione.

## Componente video di base e componente video di Scene7 {#foundation-video-component-versus-scene-video-component}

Quando utilizzi AEM, hai accesso sia al componente video disponibile in Sites che al componente video di Scene7. Questi componenti non sono intercambiabili.

Il componente video di Scene7 funziona solo per i video di Scene7. Il componente di base funziona con i video memorizzati da AEM (con FFMPEG) e con i video di Scene7.

La matrice seguente spiega quando utilizzare questi componenti:

![chlimage_1-365](assets/chlimage_1-365.png)

>[!NOTE]
>
>Come impostazione predefinita, il componente video S7 utilizza il profilo video universale. Tuttavia, potete ottenere il lettore video basato su HTML5 da usare AEM effettuando una delle seguenti operazioni in Scene7: copiate il codice da incorporare del lettore video HTML5 predefinito e inseritelo nella pagina AEM.

## Componente video AEM {#aem-video-component}

Anche se si consiglia di utilizzare il componente video di Scene7 per la visualizzazione dei video di Scene7, per una maggiore completezza questa sezione descrive come utilizzare i video di Scene7 con il componente video di base in AEM.

### Video AEM e video Scene7  {#aem-video-and-scene-video-comparison}

La tabella seguente fornisce un confronto ad alto livello delle capacità supportate tra il componente video di base di AEM e il componente video di Scene7:

|  | Video di base di AEM | Video di Scene7 |
|---|---|---|
| Approccio | Primo approccio HTML5. Flash viene utilizzato solo per il fallback non HTML5. | Flash è utilizzato sulla maggior parte dei computer desktop. HTML5 è usato per dispositivi mobili e tablet. |
| Consegna | Progressivo | Streaming adattivo |
| Tracciamento | Sì | Sì |
| Estensibilità | Sì | Sì (con visualizzatore SDK di Scene7) |
| Video mobile | Sì | Sì |

### Impostazione  {#setting-up}

#### Creazione di profili video {#creating-video-profiles}

Le varie codifiche video vengono create in base ai predefiniti di codifica S7 selezionati nella configurazione cloud S7. Affinché il componente video foundation possa utilizzarli, per ogni predefinito di codifica S7 selezionato deve essere creato un profilo video. Il componente video potrà quindi selezionare le rappresentazioni DAM appropriate.

>[!NOTE]
>
>Per la pubblicazione, i nuovi profili video e le relative modifiche devono essere attivati.

1. In AEM, toccare **[!UICONTROL Strumenti] > [!UICONTROL Console di configurazione]**.
1. Nella **[!UICONTROL console di configurazione]** passare a **[!UICONTROL Strumenti > DAM > Profili video]** nella struttura di navigazione.
1. Crea un nuovo profilo video S7. In **[!UICONTROL Nuovo...]**, selezionare **[!UICONTROL Crea pagina]**, quindi selezionare il modello Profilo video Scene7. Assegna un nome alla nuova pagina del profilo video e fai clic su **[!UICONTROL Crea.]**

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. Modifica il nuovo profilo video. Seleziona prima la configurazione cloud. Quindi seleziona lo stesso predefinito di codifica selezionato nella configurazione cloud.

   ![chlimage_1-367](assets/chlimage_1-367.png)

   | Proprietà | Descrizione |
   |---|---|
   | Configurazione cloud Scene7 | Configurazione cloud da utilizzare per i predefiniti di codifica. |
   | Predefinito di codifica Scene7 | Il predefinito di codifica con cui mappare il profilo video. |
   | Tipo video HTML5 | Questa proprietà consente di impostare il valore della proprietà type dell’elemento sorgente video HTML5. Queste informazioni non vengono fornite dai predefiniti di codifica S7, ma sono necessarie per la corretta esecuzione del rendering dei video mediante l’elemento video HTML5. Viene fornito un elenco dei formati più comuni, che può tuttavia essere sovrascritto per altri formati. |

   Ripeti questo passaggio per tutti i predefiniti di codifica selezionati nella configurazione cloud da usare nel componente video.

#### Configurazione della progettazione {#configuring-design}

Il componente **[!UICONTROL Foundation Video]** deve conoscere i profili video da utilizzare per creare l&#39;elenco delle sorgenti video. È necessario aprire la finestra di dialogo di progettazione dei componenti video e configurare la progettazione dei componenti per l’uso dei nuovi profili video.

>[!NOTE]
>
>Se utilizzate il componente **[!UICONTROL Foundation Video]** su una pagina mobile, potrebbe essere necessario ripetere questi passaggi nella progettazione della pagina mobile.

>[!NOTE]
>
>Le modifiche apportate alla progettazione richiedono l’attivazione della progettazione per avere effetto al momento della pubblicazione.

1. Aprire la finestra di dialogo di progettazione del componente **[!UICONTROL Foundation Video]** e passare alla scheda **[!UICONTROL Profili]**. Quindi eliminate i profili predefiniti e aggiungete i nuovi profili video S7. L&#39;ordine dell&#39;elenco dei profili nella finestra di dialogo della progettazione definisce l&#39;ordine dell&#39;elemento delle sorgenti video durante il rendering.
1. Per i browser che non supportano HTML5, il componente video consente di configurare un fallback di Flash. Aprite la finestra di dialogo di progettazione dei componenti video e passate alla scheda **[!UICONTROL Flash]**. Configurare le impostazioni del lettore Flash e assegnare un profilo di fallback al lettore Flash.

#### Elenco di controllo {#checklist}

1. Crea una configurazione cloud S7. Assicurati che i predefiniti di codifica video siano impostati e che il modulo di importazione sia in esecuzione.
1. Crea un profilo video S7 per ogni predefinito di codifica video selezionato nella configurazione cloud.
1. I profili video devono essere attivati.
1. Configurare la progettazione del componente **[!UICONTROL Foundation Video]** sulla pagina.
1. Dopo aver apportato le modifiche, attiva la progettazione.

