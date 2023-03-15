---
title: Video in Sites Classic Authoring
description: Le risorse forniscono una gestione centralizzata delle risorse video che consente di caricare i video direttamente in Assets per la codifica automatica in Dynamic Media Classic e di accedere ai video Dy direttamente da Assets per la creazione delle pagine.
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

Le risorse forniscono una gestione centralizzata delle risorse video che consente di caricare i video direttamente in Assets per la codifica automatica in Dynamic Media Classic e di accedere ai video Dynamic Media Classic direttamente da Assets per la creazione delle pagine.

L&#39;integrazione video Dynamic Media Classic estende la portata dei video ottimizzati a tutti gli schermi (rilevamento automatico della periferica e della larghezza di banda).

* Il componente video Dynamic Media Classic esegue automaticamente il rilevamento del dispositivo e della larghezza di banda per riprodurre il formato e la qualità video appropriati su desktop, tablet e dispositivi mobili.
* Risorse: è possibile includere set di video adattivi anziché risorse con un singolo video. Un set video adattivo è un contenitore per tutte le rappresentazioni video necessarie per riprodurre video in modo trasparente su più schermi. Un Adaptive Video Set raggruppa versioni dello stesso video codificate con diversi bit rate e formati come 400 kbps, 800 kbps e 1000 kbps. È possibile utilizzare un set video adattivo, insieme al componente video S7, per lo streaming video adattivo su più schermi, tra cui desktop, iOS, Android™, BlackBerry® e dispositivi mobili Windows. Vedi [Documentazione di Dynamic Media Classic sui set video adattivi per ulteriori informazioni](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/video/quick-start-video.html#video).

## FFMPEG e Dynamic Media Classic {#about-ffmpeg-and-scene}

Il processo di codifica video predefinito si basa sull’utilizzo dell’integrazione con i profili video basata su FFMPEG. Pertanto, l’ [!UICONTROL Risorsa di aggiornamento DAM] il flusso di lavoro contiene i due passaggi seguenti del flusso di lavoro basato su ffmpeg:

* Miniature FFMPEG
* Codifica FFMPEG

L’abilitazione e la configurazione dell’integrazione Dynamic Media Classic non rimuovono o disattivano automaticamente questi due passaggi del flusso di lavoro dall’impostazione predefinita [!UICONTROL Risorsa di aggiornamento DAM] flusso di lavoro di acquisizione. Se utilizzi già la codifica video basata su FFMPEG in Adobe Experience Manager, è probabile che FFMPEG sia installato negli ambienti di authoring. In questo caso, un nuovo video acquisito tramite Experience Manager Assets viene codificato due volte: una volta dall&#39;encoder FFMPEG e una dall&#39;integrazione Dynamic Media Classic.

Se in Experience Manager è configurata la codifica video basata su FFMPEG e FFMPEG installata, Adobe consiglia di rimuovere i due flussi di lavoro FFMPEG dal [!UICONTROL Risorsa di aggiornamento DAM] flussi di lavoro.

### Formati supportati {#supported-formats}

Per il componente Video di Dynamic Media Classic sono supportati i seguenti formati:

* F4V H.264
* MP4 H.264

### Decidi dove caricare il video {#deciding-where-to-upload-your-video}

La decisione su dove caricare le risorse video dipende da quanto segue:

* Hai bisogno di un flusso di lavoro per la risorsa video?
* Hai bisogno della funzione di controllo delle versioni per la risorsa video?

Se la risposta è “sì” ad almeno una di queste domande, carica il video direttamente in Adobe DAM. Se la risposta è &quot;no&quot; a entrambe le domande, carica il video direttamente in Dynamic Media Classic. Il flusso di lavoro per ogni scenario è descritto nella sezione seguente.

#### Se stai caricando il video direttamente in Adobe Assets {#if-you-are-uploading-your-video-directly-to-adobe-assets}

Se hai bisogno di un flusso di lavoro o della gestione delle versioni per le tue risorse, devi prima caricarle in Adobe Assets. Di seguito è riportato il flusso di lavoro consigliato:

1. Carica la risorsa video in Adobe Assets e codifica e pubblica automaticamente in Dynamic Media Classic.
1. Ad Experience Manager, puoi accedere alle risorse video in WCM nel **[!UICONTROL Filmati]** scheda di Content Finder.
1. Crea con il componente video Dynamic Media Classic o video di base.

#### Se carichi il video in Dynamic Media Classic {#if-you-are-uploading-your-video-to-scene}

Se non hai bisogno di un flusso di lavoro o di un controllo delle versioni per le tue risorse, carica le risorse in Dynamic Media Classic. Di seguito è riportato il flusso di lavoro consigliato:

1. Nell’app desktop Dynamic Media Classic, [configurare un caricamento e una codifica FTP pianificati su Dynamic Media Classic (sistema automatizzato)](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/uploading-files.html#upload-options).
1. Ad Experience Manager, puoi accedere alle risorse video in WCM nel **[!UICONTROL Dynamic Media Classic]** scheda di Content Finder.
1. Crea con il componente video Dynamic Media Classic.

### Configurare l’integrazione con video Dynamic Media Classic {#configuring-integration-with-scene-video}

1. In **[!UICONTROL Cloud Services]**, vai alla **[!UICONTROL Dynamic Media Classic]** configurazione e seleziona **[!UICONTROL Modifica]**.
1. Seleziona la scheda **[!UICONTROL Video]**.

   >[!NOTE]
   >
   >La scheda **[!UICONTROL Video]** non viene visualizzata se la pagina non ha una configurazione cloud. Vedi [Abilita Dynamic Media Classic per WCM](#enablingscene7forwcm).

1. Seleziona il profilo di codifica video adattivo, uno dei profili di codifica per video singolo preconfigurati oppure un profilo di codifica video personalizzato.

   >[!NOTE]
   >
   >Per ulteriori informazioni sul significato dei predefiniti video, consulta [Predefiniti video per la codifica dei file video](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html#video-presets-for-encoding-video-files).
   >
   >Adobe consiglia di selezionare entrambi i set video adattivi per la configurazione dei predefiniti universali o di selezionare l’opzione **[!UICONTROL Codifica video adattiva]**.

1. I profili di codifica selezionati vengono applicati automaticamente a tutti i video caricati nella cartella di destinazione CQ DAM impostata per questa configurazione cloud Dynamic Media Classic. Puoi impostare più configurazioni cloud di Dynamic Media Classic con diverse cartelle di destinazione per applicare profili di codifica diversi in base alle esigenze.

### Aggiornamento del visualizzatore e dei predefiniti di codifica {#updating-viewer-and-encoding-presets}

Se i predefiniti sono stati aggiornati in Dynamic Media Classic, aggiorna ad Experience Manager il visualizzatore e i predefiniti di codifica video . In questo caso, accedi alla configurazione Dynamic Media Classic nella configurazione cloud e seleziona **Aggiornare il visualizzatore e i predefiniti di codifica**.

![chlimage_1-131](assets/chlimage_1-131.png)

### Caricare il video sorgente principale {#uploading-your-master-video}

Per caricare il video sorgente principale su Dynamic Media Classic da DAM Adobe:

1. Passa alla cartella di destinazione CQ DAM in cui hai configurato la configurazione cloud con i profili di codifica Dynamic Media Classic.
1. Seleziona **[!UICONTROL Carica]** per caricare il video sorgente principale. Il caricamento e la codifica dei video vengono completati dopo la [!UICONTROL Risorsa di aggiornamento DAM] il flusso di lavoro è completato e **[!UICONTROL Pubblicare su Dynamic Media Classic]** ha un segno di spunta.

   >[!NOTE]
   >
   >La generazione delle miniature video potrebbe richiedere del tempo.

   Quando si trascina il video sorgente principale DAM sul componente video, si accede al *tutto* Rappresentazioni proxy codificate di Dynamic Media Classic per la distribuzione.

### Componente Video di base e componente Video di Dynamic Media Classic {#foundation-video-component-versus-scene-video-component}

Quando utilizzi Experience Manager, puoi accedere sia al componente Video disponibile in Sites che al componente video Dynamic Media Classic. Questi componenti non sono intercambiabili.

Il componente video Dynamic Media Classic funziona solo per i video Dynamic Media Classic. Il componente foundation funziona con i video archiviati da Experience Manager (utilizzando ffmpeg) e i video Dynamic Media Classic.

La matrice seguente spiega quando utilizzare questi componenti:

![chlimage_1-132](assets/chlimage_1-132.png)

>[!NOTE]
>
>Il componente video Dynamic Media Classic utilizza il profilo video universale. Tuttavia, è possibile ottenere il lettore video basato su HTML5 da utilizzare per Experience Manager. In Dynamic Media Classic, copia il codice di incorporamento del lettore video HTML5 predefinito e inseriscilo nella pagina dell’Experience Manager.

## Componente video Experience Manager {#aem-video-component}

Anche se per visualizzare i video Dynamic Media Classic si consiglia di utilizzare il componente Video di Dynamic Media Classic, questa sezione descrive l’utilizzo dei video di Dynamic Media Classic con [!UICONTROL Componente video di base] in Experience Manager per completezza.

### Confronto tra video e video Dynamic Media Classic di Experience Manager {#aem-video-and-scene-video-comparison}

La tabella seguente fornisce un confronto ad alto livello delle funzionalità supportate tra il componente Video di base di Experience Manager e il componente Video di Dynamic Media Classic:

|  | Video Experience Manager Foundation | Video Dynamic Media Classic |
|---|---|---|
| Approccio | Primo approccio HTML5. Flash viene utilizzato solo per il fallback non HTML5. | Flash è utilizzato sulla maggior parte dei computer desktop. HTML5 è usato per dispositivi mobili e tablet. |
| Distribuzione | Progressivo | Streaming adattivo |
| Tracciamento | Sì | Sì |
| Estensibilità | Sì | No |
| Video mobile | Sì | Yes |

### Configurazione {#setting-up}

#### Creare profili video {#creating-video-profiles}

Le varie codifiche video vengono create in base ai predefiniti di codifica Dynamic Media Classic selezionati in Dynamic Media Classic Cloud Configuration. Affinché il componente Video di base possa utilizzarli, è necessario creare un profilo video per ogni predefinito di codifica Dynamic Media Classic selezionato. Consente al componente video di selezionare di conseguenza le rappresentazioni DAM.

>[!NOTE]
>
>Per la pubblicazione, i nuovi profili video e le relative modifiche devono essere attivati.

1. In Experience Manager, vai a **[!UICONTROL Strumenti]**, quindi seleziona **[!UICONTROL Console di configurazione]**.
1. Nella console di configurazione, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili video]** nella struttura di navigazione.
1. Crea un profilo video Dynamic Media Classic. In **[!UICONTROL Nuovo]** menu, seleziona **[!UICONTROL Crea pagina]**.
1. Seleziona il modello di profilo Dynamic Media Classic Video . Assegna un nome alla nuova pagina del profilo video e seleziona **[!UICONTROL Crea]**.

   ![chlimage_1-133](assets/chlimage_1-133.png)

1. Modifica il nuovo profilo video. Seleziona prima la configurazione cloud. Quindi seleziona lo stesso predefinito di codifica selezionato nella configurazione cloud.

   ![chlimage_1-134](assets/chlimage_1-134.png)

   | Proprietà | Descrizione |
   |---|---|
   | Configurazione cloud Dynamic Media Classic | Configurazione cloud da utilizzare per i predefiniti di codifica. |
   | Predefinito di codifica Dynamic Media Classic | Predefinito di codifica con cui mappare il profilo video. |
   | Tipo video HTML5 | Questa proprietà consente di impostare il valore della proprietà type dell&#39;elemento video source HTML5. Queste informazioni non vengono fornite dai predefiniti di codifica Dynamic Media Classic, ma sono necessarie per il corretto rendering dei video con l’elemento video HTML5. Viene fornito un elenco dei formati più comuni, che può tuttavia essere sovrascritto per altri formati. |

   Ripeti questo passaggio per tutti i predefiniti di codifica selezionati nella configurazione cloud da usare nel componente video.

#### Configurare la progettazione {#configuring-design}

Il componente video di base deve sapere quali profili video utilizzare per creare l’elenco di sorgenti video. Apri la finestra di dialogo di progettazione dei componenti video e configura la progettazione dei componenti per l’utilizzo dei nuovi profili video.

>[!NOTE]
>
>Se utilizzi il componente Video di base su una pagina mobile, ripeti questi passaggi nella progettazione della pagina mobile.

>[!NOTE]
>
>Le modifiche apportate alla progettazione richiedono l’attivazione della progettazione per avere effetto al momento della pubblicazione.

1. Apri la finestra di dialogo di progettazione del componente video di base e passa alla scheda **[!UICONTROL Profili]**. Quindi elimina i profili predefiniti e aggiungi i nuovi profili video Dynamic Media Classic. L’ordine dell’elenco dei profili nella finestra di dialogo di progettazione definisce anche l’ordine dell’elemento delle sorgenti video durante il rendering.
1. Per i browser che non supportano HTML5, il componente Video consente di configurare un fallback flash. Apri la finestra di dialogo di progettazione dei componenti video e passa alla scheda **[!UICONTROL Flash]**. Configura le impostazioni del lettore Flash e assegna un profilo di fallback per il lettore Flash.

#### Elenco di controllo {#checklist}

1. Crea una configurazione cloud Dynamic Media Classic. Assicurati che i predefiniti di codifica video siano impostati e che l’importazione sia in esecuzione.
1. Crea un profilo video Dynamic Media Classic per ogni predefinito di codifica video selezionato nella configurazione cloud.
1. I profili video devono essere attivati.
1. Configura la struttura del componente video di base sulla pagina.
1. Dopo aver apportato le modifiche, attiva la progettazione.
