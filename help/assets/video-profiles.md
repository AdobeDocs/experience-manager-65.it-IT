---
title: Profili video
description: Gli elementi multimediali dinamici dispongono già di un profilo di codifica video adattiva predefinito. Le impostazioni incluse in questo profilo out-of-the-box sono ottimizzate per offrire ai clienti la migliore esperienza di visualizzazione possibile. Potete anche aggiungere ritaglio avanzato ai video.
uuid: 26a20984-db63-41e9-b16c-6e164b7596a0
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
discoiquuid: 3b8791c8-2c97-42b7-b4a9-e1157ac9ea02
docset: aem65
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '3707'
ht-degree: 20%

---


# Video profiles {#video-profiles}

Gli elementi multimediali dinamici dispongono già di un profilo di codifica video adattiva predefinito. Le impostazioni incluse in questo profilo out-of-the-box sono ottimizzate per offrire ai clienti la migliore esperienza di visualizzazione possibile. Quando codificate i video sorgente principali utilizzando il profilo di codifica video adattiva, durante la riproduzione il lettore video regola automaticamente la qualità del flusso video in base alla velocità di connessione Internet dei clienti. È noto come streaming adattivo.

Di seguito sono riportati altri fattori che determinano la qualità dei video:

* **Risoluzione del video sorgente principale caricato**

   Se il video MP4 veniva registrato a una risoluzione inferiore, ad esempio 240p o 360p, non poteva essere trasmesso in streaming in alta definizione.

* **Dimensioni del lettore video**

   Per impostazione predefinita, la larghezza nel profilo Codifica video adattiva è impostata su &quot;Auto&quot;. Anche in questo caso, durante la riproduzione, viene utilizzata la qualità migliore in base alle dimensioni del lettore.

Consultate [Best practice per la codifica](/help/assets/video.md#best-practices-for-encoding-videos)video.

Consultate anche [Best practice per l’organizzazione delle risorse digitali per l’utilizzo dei profili](/help/assets/organize-assets.md)di elaborazione.

>[!NOTE]
>
>Per generare i metadati di un video e le miniature delle immagini video associate, il video stesso deve seguire il processo di codifica di Dynamic Media. Se hai attivato gli elementi multimediali dinamici e hai impostato Cloud Services per i video, il flusso di lavoro **[!UICONTROL Codifica video elementi multimediali dinamici]** di AEM ti consente di eseguire la codifica dei video. Questo flusso di lavoro acquisisce la cronologia del processo del flusso di lavoro e le informazioni di errore. Consulta la sezione [Monitoraggio della codifica video e stato della pubblicazione su YouTube](/help/assets/video.md#monitoring-video-encoding-and-youtube-publishing-progress). Se hai attivato gli elementi multimediali dinamici e hai impostato Cloud Services per i video, il flusso di lavoro **[!UICONTROL Codifica video elementi multimediali dinamici]** viene applicato automaticamente al momento di caricare un video. Se non utilizzi gli elementi multimediali dinamici, viene applicato il flusso di lavoro **[!UICONTROL Risorsa di aggiornamento DAM]**.
>
>I metadati sono utili per la ricerca delle risorse. Le miniature sono immagini video statiche generate durante la codifica. Sono richieste dal sistema AEM e utilizzate nell’interfaccia utente per identificare visivamente i video nelle viste Schede, Risultati ricerca e Elenco risorse. Potete visualizzare le miniature generate toccando l&#39;icona Rappresentazioni (la palette del pittore) di un video codificato.

Una volta creato il profilo video, questo viene applicato a una cartella o più cartelle. See [Applying a video profile to folders.](#applying-a-video-profile-to-folders)

Per definire parametri di elaborazione avanzati per altri tipi di risorse, consulta [Configurazione dell’elaborazione](/help/assets/config-dms7.md#configuring-asset-processing)delle risorse.

Consultate anche [Profili per l’elaborazione di metadati, immagini e video](processing-profiles.md).

## Predefiniti di codifica video adattiva {#adaptive-video-encoding-presets}

Nella tabella seguente sono riportati i profili di codifica best practice per lo streaming di video adattivi per dispositivi mobili, tablet e computer desktop. Potete usare questi predefiniti per qualsiasi video con proporzioni qualsiasi.

<table>
 <tbody>
  <tr>
   <td><strong>Codec formato video</strong></td>
   <td><strong>Dimensioni video - Larghezza (px)</strong></td>
   <td><strong>Dimensioni video - Altezza (px)</strong></td>
   <td><strong>Mantieni proporzioni?</strong></td>
   <td><strong>Bitrate video (Kbps)</strong></td>
   <td><strong>Frame Rate Video (Fps)</strong></td>
   <td><strong>Codec audio</strong></td>
   <td><strong>Bitrate audio (Kbps)</strong></td>
  </tr>
  <tr>
   <td><p>MP4 H.264 (mp4)</p> </td>
   <td>auto</td>
   <td>360</td>
   <td>Sì</td>
   <td>730</td>
   <td>30</td>
   <td>Dolby HE-AAC</td>
   <td>128</td>
  </tr>
  <tr>
   <td><p>MP4 H.264 (mp4)</p> </td>
   <td>auto</td>
   <td>540</td>
   <td>Sì</td>
   <td>2000<br /> </td>
   <td>30</td>
   <td>Dolby HE-AAC</td>
   <td>128</td>
  </tr>
  <tr>
   <td><p>MP4 H.264 (mp4)</p> </td>
   <td>auto</td>
   <td>720<br /> </td>
   <td>Sì</td>
   <td>3000<br /> </td>
   <td>30</td>
   <td>Dolby HE-AAC</td>
   <td>128</td>
  </tr>
 </tbody>
</table>

## Utilizzo del ritaglio avanzato nei profili video {#about-smart-crop-video}

La funzione di ritaglio avanzato per i video - una funzione opzionale disponibile nei profili video - è uno strumento che utilizza l&#39;intelligenza artificiale di  Adobe Sensei per rilevare e ritagliare automaticamente il punto focale in qualsiasi video adattivo o progressivo caricato, indipendentemente dalle dimensioni.

I formati video supportati per il ritaglio avanzato includono MP4, MKV, MOV, AVI, FLV e WMV.

La dimensione massima del file video supportato per il ritaglio avanzato è il seguente criterio:

* Durata di cinque minuti.
* 30 fotogrammi al secondo (FPS).
* 300 MB di dimensione file.

 Adobe Sensei è attualmente limitato a 9000 fotogrammi. Cioè, cinque minuti a 30 fps. Se il video ha un valore FPS superiore, la durata video massima supportata diminuisce. Ad esempio, un video a 60 fps deve avere una durata di due minuti e mezzo per essere supportato dal sensore  Adobe e dal ritaglio avanzato.

![Ritaglio avanzato per video](assets/smart-crop-video.png)

>[!IMPORTANT]
>
>Per il corretto funzionamento del ritaglio avanzato video, dovete includere uno o più predefiniti di codifica video con il vostro profilo video.

Per utilizzare il ritaglio avanzato per i video, potete creare un profilo di codifica video adattivo o progressivo. Come parte del profilo, usate lo strumento **[!UICONTROL Smart Crop Ratio (Proporzioni]** avanzate) per selezionare le proporzioni predefinite. Ad esempio, dopo aver definito i predefiniti di codifica video, potete aggiungere una definizione di &quot;Mobile Landscape&quot; con proporzioni pari a 16x9 e una definizione di &quot;Mobile Portrait&quot; con proporzioni pari a 9x16. Altre proporzioni o proporzioni di ritaglio tra cui potete scegliere tra 1x1, 4x3 e 4x5.

![Modifica di un profilo di codifica video con il ritaglio avanzato](assets/edit-smart-crop-video2.png)

Nel profilo video puoi attivare o disattivare il ritaglio avanzato video, semplicemente utilizzando il cursore posto all’estrema destra di **[!UICONTROL Smart Crop Ratio (Proporzioni ritaglio avanzate)]** nell’interfaccia utente.

Dopo aver creato e salvato il profilo video, potete applicarlo alle cartelle desiderate.

Consultate [Applicazione dei profili video a cartelle](#applying-video-profiles-to-specific-folders) specifiche o [Applicazione globale](#applying-a-video-profile-globally)di un profilo video.

Consultate anche [Ritaglio avanzato per le immagini](image-profiles.md).

## Creazione di un profilo video per lo streaming adattivo {#creating-a-video-encoding-profile-for-adaptive-streaming}

Gli elementi multimediali dinamici sono già dotati di un profilo di codifica video adattiva predefinito, un gruppo di impostazioni di caricamento video per MP4 H.264, ottimizzato per garantire una migliore esperienza di visualizzazione. Potete usare questo profilo quando caricate i video.

Tuttavia, se questo profilo predefinito non soddisfa le esigenze, potete scegliere di creare un profilo di codifica video adattivo personalizzato. Quando utilizzate l’impostazione **[!UICONTROL Codifica per lo streaming]** adattivo, come best practice, vengono convalidati tutti i predefiniti di codifica che aggiungete al profilo, in modo da garantire che tutti i video abbiano le stesse proporzioni. Inoltre, i video codificati vengono trattati come un set di bitrate multipli per lo streaming.

Quando create il profilo di codifica video, noterete che la maggior parte delle opzioni di codifica sono precompilate con le impostazioni predefinite consigliate per facilitare l’utente. Tuttavia, se selezionate un valore diverso da quello predefinito consigliato, tenete presente che potrebbe causare problemi di qualità video durante la riproduzione e altre prestazioni.

Pertanto, per tutti i predefiniti di codifica video MP4 H.264 presenti nel profilo, i seguenti valori vengono convalidati per garantire che siano identici tra i singoli predefiniti di codifica nel profilo, rendendo possibile lo streaming adattivo:

* Codec formato video - MP4 H.264 (.mp4)
* Codec audio
* Bitrate audio
* Mantieni proporzioni
* Codifica a due passate
* Bitrate costante
* Profilo H264
* Frequenza di campionamento audio

Se i valori non sono identici, potete continuare a creare il profilo così com&#39;è. Tuttavia, lo streaming adattivo non sarà possibile. Gli utenti possono invece utilizzare lo streaming a bitrate singolo. È consigliabile modificare le impostazioni di codifica in modo da utilizzare gli stessi valori per i singoli predefiniti di codifica presenti nel profilo. Tenete presente che l’editor del profilo video/predefinito deve applicare la parità delle impostazioni di codifica video adattiva se è abilitata l’opzione &quot;Codifica per lo streaming adattivo&quot;.

Consultate anche [Creazione di un profilo di codifica video per lo streaming](#creating-a-video-encoding-profile-for-progressive-streaming)progressivo.

Consultate anche [Best practice per la codifica](/help/assets/video.md#best-practices-for-encoding-videos)video.

Per definire parametri di elaborazione avanzati per altri tipi di risorse, consulta [Configurazione dell’elaborazione](/help/assets/config-dms7.md#configuring-asset-processing)delle risorse.

**Per creare un profilo video per lo streaming** adattivo,

1. Tocca il logo AEM e seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili video.]**
1. Tocca o fai clic su **[!UICONTROL Crea]** per aggiungere un nuovo profilo video.

1. Immettete un nome e una descrizione per il profilo.
1. Nella pagina Crea/Modifica predefiniti di codifica video, toccate **[!UICONTROL Aggiungi predefinito di codifica video.]**
1. Nella scheda **[!UICONTROL Base]** , impostate le opzioni video e audio.
Toccate l’icona delle informazioni accanto a ciascuna opzione per ottenere descrizioni aggiuntive o impostazioni consigliate in base al codec del formato video selezionato.
1. Nella sezione Dimensione video, accertatevi che le proporzioni **[!UICONTROL Mantieni siano selezionate]** .
1. Impostate la risoluzione del fotogramma video in pixel. Usate il valore **[!UICONTROL Auto]** per ridimensionare automaticamente in base alle proporzioni sorgente (rapporto larghezza/altezza). Ad esempio, Auto x 480 o 640 x Auto.

1. Effettua una delle operazioni seguenti:

   * In the **[!UICONTROL Width]** field, enter **[!UICONTROL auto.]** Nel campo **[!UICONTROL Altezza]** , inserite un valore in pixel.

   * Per visualizzare le dimensioni del video, toccate l’icona Informazioni (i) a destra di **[!UICONTROL Altezza]** per aprire la pagina Calcolatore dimensioni. Utilizzate **[!UICONTROL Calcolatore]** dimensioni per impostare le dimensioni video (rappresentate dalla casella blu) desiderate. Toccate **[!UICONTROL X]** nell&#39;angolo superiore destro al termine.

1. (Facoltativo) Toccate la scheda **[!UICONTROL Avanzate]** e verificate che la casella di controllo **[!UICONTROL Usa valori]** predefiniti sia selezionata (opzione consigliata). In alternativa, modificate le impostazioni audio e video avanzate.
1. In the upper-right corner of the page, tap **[!UICONTROL Save]** to save the preset.
1. Effettua una delle operazioni seguenti:
   * Ripetete i passaggi da 4 a 10 per creare altri predefiniti di codifica. Lo streaming di video adattivi richiede più di un predefinito video.
   * Passate al passaggio successivo.

1. (Facoltativo) Per aggiungere video smart crop ai video a cui verrà applicato questo profilo, effettuate le seguenti operazioni:
   * Nella pagina Modifica profilo video, toccate **[!UICONTROL Aggiungi nuovo a destra dell’intestazione Rapporto di ritaglio avanzato.]**
   * Nel campo Nome, digitate un nome per il rapporto di ritaglio che vi consentirà di identificarlo facilmente.
   * Dall’elenco a discesa **[!UICONTROL Rapporto]** di ritaglio, selezionate il rapporto da usare.

1. Effettua una delle operazioni seguenti:

   * Continuate ad aggiungere nuove proporzioni di ritaglio, se necessario.
   * Passate al passaggio successivo.

1. In the upper-right corner of the page, tap **[!UICONTROL Save]** again to save the profile.

Ora potete applicare il profilo alle cartelle che contengono video. Consultate [Applicazione di un profilo video alle cartelle](#applying-a-video-profile-to-folders) o [Applicazione globale](#applying-a-video-profile-globally)di un profilo video.

## Creazione di un profilo video per lo streaming progressivo {#creating-a-video-encoding-profile-for-progressive-streaming}

Se scegli di non utilizzare l’opzione **[!UICONTROL Codifica per lo streaming adattivo]**, tutti i predefiniti di codifica aggiunti al profilo vengono trattati come rappresentazioni video individuali per lo streaming a bitrate singolo o per la distribuzione progressiva di video. Inoltre, non esiste una convalida per garantire che tutte le rappresentazioni video abbiano le stesse proporzioni.

A seconda della modalità in esecuzione, i codec supportati sono:

* Modalità Dynamic Media-Scene7: H.264 (.mp4)
* Modalità Dynamic Media-Hybrid: H.264 (.mp4), WebM

Consultate anche [Creazione di un profilo di codifica video per lo streaming](#creating-a-video-encoding-profile-for-adaptive-streaming)adattivo.

Consultate anche [Best practice per la codifica](/help/assets/video.md#best-practices-for-encoding-videos)video.

Per definire parametri di elaborazione avanzati per altri tipi di risorse, consulta [Configurazione dell’elaborazione](/help/assets/config-dms7.md#configuring-asset-processing)delle risorse.

**Per creare un profilo video per lo streaming progressivo:**

1. Tocca il logo AEM e seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili video.]**
1. Toccate **[!UICONTROL Crea]** per aggiungere un nuovo profilo video.
1. Immettete un nome e una descrizione per il profilo.
1. Nella pagina Crea/Modifica predefiniti di codifica video, toccate **[!UICONTROL Aggiungi predefinito di codifica video.]**
1. Nella scheda **[!UICONTROL Base]** , impostate le opzioni video e audio.
Toccate l’icona delle informazioni accanto a ciascuna opzione per ottenere descrizioni aggiuntive o impostazioni consigliate in base al codec del formato video selezionato.
1. (Facoltativo) Sotto l’intestazione Dimensione video, deselezionate **[!UICONTROL Mantieni proporzioni.]**
1. Effettua le seguenti operazioni:
   * In the **[!UICONTROL Width]** field, enter **[!UICONTROL auto.]**
   * In the **[!UICONTROL Height]** field, enter a value in pixels.
To help you visualize the size of the video, tap the Height&#39;s information icon to open the **[!UICONTROL Size Calculator]** page. Use the **[!UICONTROL Size Calculator]** page to further set the video dimension (blue box) how you want. When you are done, in the upper-right corner of the dialog box, tap **[!UICONTROL X.]**
1. (Facoltativo) Effettuate una delle seguenti operazioni:

   * Toccate la scheda **[!UICONTROL Avanzate]** e verificate che la casella di controllo **[!UICONTROL Usa valori]** predefiniti sia selezionata (opzione consigliata).

   * Deselezionate la casella di controllo **[!UICONTROL Usa valori]** predefiniti e specificate le impostazioni video e audio desiderate.
Toccate l’icona delle informazioni accanto a ciascuna opzione per ottenere descrizioni aggiuntive o impostazioni consigliate in base al codec del formato video selezionato.

1. In the upper-right corner of the page, tap **[!UICONTROL Save]** to save the preset.
1. Effettua una delle operazioni seguenti:

   * Ripetete i passaggi da 4 a 9 per creare altri predefiniti di codifica.
   * Passate al passaggio successivo.

1. (Facoltativo) Per aggiungere video smart crop ai video a cui verrà applicato questo profilo, effettuate le seguenti operazioni:

   * Nella pagina Modifica profilo video, toccate **[!UICONTROL Aggiungi nuovo a destra dell’intestazione Rapporto di ritaglio avanzato.]**
   * Nel campo Nome, digitate un nome per il rapporto di ritaglio che vi consentirà di identificarlo facilmente.
   * Dall’elenco a discesa **[!UICONTROL Rapporto]** di ritaglio, selezionate il rapporto da usare.

1. Effettua una delle operazioni seguenti:

   * Continuate ad aggiungere nuove proporzioni di ritaglio, se necessario.
   * Passate al passaggio successivo.

1. Nell’angolo superiore destro della pagina, tocca **[!UICONTROL Salva]** per salvare il profilo.

Ora potete applicare il profilo alle cartelle che contengono video. Consultate [Applicazione di un profilo video alle cartelle](#applying-a-video-profile-to-folders) o [Applicazione globale](#applying-a-video-profile-globally)di un profilo video.

## Utilizzo di parametri di codifica video personalizzati {#using-custom-added-video-encoding-parameters}

Potete modificare un profilo di codifica video esistente per sfruttare i parametri di codifica video avanzati che non sono disponibili nell’interfaccia utente al momento della creazione o della modifica di un profilo video in AEM. Potete aggiungere uno o più parametri avanzati al profilo esistente, ad esempio minBitrate e maxBitrate.

**Per utilizzare parametri** di codifica video personalizzati:

1. Tocca il logo AEM, quindi seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL CRXDE Lite.]**
1. Dalla pagina CRXDE Lite, nel pannello Explorer a sinistra, individuate le seguenti opzioni:

   `/conf/global/settings/dam/dm/presets/video/*name_of_video_encoding_profile_to_edit`

1. Nel pannello in basso a destra della pagina, dalla scheda Proprietà, specifica **[!UICONTROL Nome]**, **[!UICONTROL Tipo]** e **[!UICONTROL Valore]** del parametro da utilizzare.

   Sono disponibili i seguenti parametri avanzati:

<table>
 <tbody>
  <tr>
   <td><strong>Nome</strong></td>
   <td><strong>Descrizione</strong><br /> </td>
   <td><strong>Tipo</strong><br /> </td>
   <td><strong>Valore</strong></td>
  </tr>
  <tr>
   <td><code>h264Level</code></td>
   <td>Livello H.264 da usare per la codifica. In genere questo viene determinato automaticamente in base alle impostazioni di codifica utilizzate.</td>
   <td><code>String</code></td>
   <td><p>10 * livello h264</p> <p>Ad esempio, 3.0 = 30, 1.3 = 13)</p> <p>Nessun valore predefinito.</p> </td>
  </tr>
  <tr>
   <td><code>keyframe</code></td>
   <td>Il numero target di fotogrammi tra i fotogrammi chiave. Calcolate questo valore per generare un fotogramma chiave ogni 2-10 secondi. Ad esempio, a 30 fotogrammi al secondo, l’intervallo del fotogramma chiave dovrebbe essere compreso tra 60 e 300.<br /> <br /> Intervalli di fotogrammi chiave più bassi migliorano la ricerca del flusso e il comportamento di commutazione del flusso per le codifiche video adattive e possono anche migliorare la qualità dei video con molto movimento. Tuttavia, poiché i fotogrammi chiave aumentano le dimensioni di un file, un intervallo di fotogrammi chiave inferiore in genere riduce la qualità video complessiva a un dato bitrate.</td>
   <td><code>String</code></td>
   <td><p>Numero positivo.</p> <p>Il valore predefinito è 300.</p> <p>Il valore consigliato per HLS (HTTP Live Streaming) è 60-90.</p> </td>
  </tr>
  <tr>
   <td><code>minBitrate</code></td>
   <td><p>Bitrate minimo per consentire codifiche con bitrate variabile, in Kbps (kilobit al secondo).</p> <p>Questo parametro si applica solo quando<strong> l’opzione Usa bitrate</strong> costante è deselezionata nella scheda Avanzate quando si crea o si modifica un profilo di codifica video.</p> <p>Vedere anche <a href="/help/assets/video.md#bitrate">Bitrate</a>.</p> </td>
   <td><code>String</code></td>
   <td><p>Numero positivo, in Kbps.</p> <p>Nessun valore predefinito.</p> </td>
  </tr>
  <tr>
   <td><code>maxBitrate</code></td>
   <td><p>Bitrate massimo per consentire codifiche con bitrate variabile, in Kbps.</p> <p>Questo parametro si applica solo quando<strong> l’opzione Usa bitrate</strong> costante è deselezionata nella scheda Avanzate quando si crea o si modifica un profilo di codifica video.</p> <p>Vedere anche <a href="/help/assets/video.md#bitrate">Bitrate</a>.</p> </td>
   <td><code>String</code></td>
   <td><p>Numero positivo, in Kbps.</p> <p>Nessun valore predefinito. Tuttavia, il valore consigliato è fino a due volte il bitrate di codifica.</p> </td>
  </tr>
  <tr>
   <td><code>audioBitrateCustom</code></td>
   <td>Impostate un valore <code>true</code> per forzare un bitrate costante per lo streaming audio, se supportato dal codec audio.</td>
   <td><code>String</code></td>
   <td><p><code>true</code>/<code>false</code></p> <p>Default is <code>false</code>.</p> <p>Il valore consigliato per HLS (HTTP Live Streaming) è <code>false</code>.</p> <p> </p> </td>
  </tr>
 </tbody>
</table>

![chlimage_1-516](assets/chlimage_1-516.png)

1. Nell’angolo inferiore destro della pagina, toccate **[!UICONTROL Aggiungi.]**
1. Effettua una delle operazioni seguenti:

   * Ripetete i passaggi 3 e 4 per aggiungere un altro parametro al profilo di codifica video.
   * Nell’angolo in alto a sinistra della pagina, toccate **[!UICONTROL Salva tutto.]**

1. Nell&#39;angolo superiore sinistro della pagina CRXDE Lite, toccate l&#39;icona **[!UICONTROL Indietro Home]** per tornare alla AEM.

### Modifica di un profilo video {#editing-a-video-encoding-profile}

Potete modificare qualsiasi profilo video creato per aggiungere, modificare o eliminare i predefiniti video all’interno di tale profilo.

Per impostazione predefinita, non è possibile modificare il profilo predefinito per la codifica **[!UICONTROL video]** adattiva fornito con gli elementi multimediali dinamici. Potete invece copiare facilmente il profilo e salvarlo con un nuovo nome. Potete quindi modificare i predefiniti desiderati nel profilo copiato.

Consultate anche [Best practice per la codifica](/help/assets/video.md#best-practices-for-encoding-videos)video.

Per definire parametri di elaborazione avanzati per altri tipi di risorse, consulta [Configurazione dell’elaborazione](/help/assets/config-dms7.md#configuring-asset-processing)delle risorse.

**Per modificare un profilo** video:

1. Tocca il logo AEM e seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili video.]**
1. Nella pagina Profili video, verificate il nome di un profilo video.
1. Sulla barra degli strumenti, toccate **[!UICONTROL Modifica.]**
1. Nella pagina Profilo codifica video, modificate il nome e la descrizione come desiderate.
1. Come best practice, accertati che la casella di controllo **[!UICONTROL Codifica per streaming adattivo]** sia selezionata.
Per una descrizione dello streaming adattivo, tocca l’icona delle informazioni. (Se state modificando un profilo video progressivo, non selezionate questa casella di controllo.)
1. Nell’intestazione Predefiniti codifica video, potete aggiungere, modificare o eliminare predefiniti di codifica video che compongono il profilo.

   Per ottenere descrizioni aggiuntive o impostazioni consigliate per il codec del formato video selezionato, tocca l’icona delle informazioni posta accanto a ciascuna opzione nelle schede **[!UICONTROL Base]** e **[!UICONTROL Avanzate]**.

1. Nell&#39;angolo superiore destro della pagina, toccate **[!UICONTROL Salva.]**

### Copia di un profilo video {#copying-a-video-encoding-profile}

1. Tocca il logo AEM e seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili video.]**
1. Nella pagina Profili video, verificate il nome di un profilo video.
1. Sulla barra degli strumenti, toccate **[!UICONTROL Copia.]**
1. Nella pagina Profilo codifica video, immettete un nuovo nome per il profilo.
1. Come best practice, accertati che la casella di controllo **[!UICONTROL Codifica per streaming adattivo]** sia selezionata. Per una descrizione dello streaming adattivo, tocca l’icona delle informazioni. Se copi un profilo video progressivo, non selezionare la casella di controllo.

   In modalità Dynamic Media - Hybrid, se un predefinito video WebM fa parte del profilo video, **[!UICONTROL Codifica per lo streaming]** adattivo non è possibile perché tutti i predefiniti devono essere MP4.
1. Nell’intestazione Predefiniti codifica video, potete aggiungere, modificare o eliminare predefiniti di codifica video che compongono il profilo.

   Toccate l&#39;icona delle informazioni accanto a ciascuna opzione nelle schede Base e Avanzate per le impostazioni e le descrizioni consigliate.

1. Nell&#39;angolo superiore destro della pagina, toccate **[!UICONTROL Salva.]**

### Eliminazione di un profilo video {#deleting-a-video-encoding-profile}

1. Tocca il logo AEM e seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili video.]**
1. Nella pagina Profili video, verificate i nomi di uno o più profili video.
1. Sulla barra degli strumenti, toccate **[!UICONTROL Elimina.]**
1. Toccate **[!UICONTROL OK.]**

## Applicazione di un profilo video alle cartelle {#applying-a-video-profile-to-folders}

Quando assegnate un profilo video a una cartella, tutte le sottocartelle ereditano automaticamente il profilo dalla cartella principale. Questo significa che potete assegnare un solo profilo video a una cartella. Considerate quindi attentamente la struttura delle cartelle in cui caricare, memorizzare, usare e archiviare le risorse.

Se avete assegnato un profilo video diverso a una cartella, il nuovo profilo sostituisce il profilo precedente. Le risorse di cartella esistenti in precedenza restano invariate. Il nuovo profilo viene applicato alle risorse aggiunte successivamente alla cartella.

Le cartelle a cui è assegnato un profilo sono indicate nell&#39;interfaccia utente in base al nome del profilo visualizzato nel nome della scheda.

![chlimage_1-517](assets/chlimage_1-517.png)

Potete applicare i profili video a cartelle specifiche o globalmente a tutte le risorse.

Potete rielaborare le risorse in una cartella che dispone già di un profilo video esistente modificato in seguito. Consulta [Rielaborazione delle risorse in una cartella dopo la modifica del profilo di elaborazione](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile).

### Applicazione di un profilo video a cartelle specifiche {#applying-video-profiles-to-specific-folders}

Puoi applicare un profilo video a una cartella direttamente dal menu **[!UICONTROL Strumenti]** oppure, se ti trovi nella cartella, da **[!UICONTROL Proprietà.]** Questa sezione descrive come applicare i profili video alle cartelle con entrambe le soluzioni.

Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

See also [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile).

#### Applicazione di un profilo video alle cartelle tramite l’interfaccia utente Profili {#applying-video-profiles-to-folders-by-way-of-the-profiles-user-interface}

1. Tocca il logo AEM e seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili video.]**
1. Selezionate il profilo video da applicare a una o più cartelle.
1. Tocca **[!UICONTROL Applica profilo a cartelle]** e seleziona una o più cartelle da usare per ricevere le risorse appena caricate, quindi fai clic su **[!UICONTROL Applica.]** Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella in **[!UICONTROL Vista a schede.]**
Potete [monitorare l’avanzamento di un processo](#monitoring-the-progress-of-an-encoding-job)di elaborazione del profilo video.

#### Applicazione di un profilo video alle cartelle da Proprietà {#applying-video-profiles-to-folders-from-properties}

1. Toccate o fate clic sul logo AEM, accedete a **[!UICONTROL Risorse]** e quindi alla cartella a cui desiderate applicare un profilo video.
1. Sulla cartella, toccate il segno di spunta per selezionarlo, quindi toccate **[!UICONTROL Proprietà.]**
1. Seleziona la scheda **[!UICONTROL Profili video]** e fai clic sul profilo dal menu a discesa, infine tocca **[!UICONTROL Salva e chiudi.]** Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

   ![chlimage_1-518](assets/chlimage_1-518.png)È possibile [monitorare l’avanzamento di un processo](#monitoring-the-progress-of-an-encoding-job)di elaborazione del profilo video.

### Applicazione di un profilo video a livello globale {#applying-a-video-profile-globally}

Oltre ad applicare un profilo a una cartella, potete anche applicarne uno a livello globale in modo che a qualsiasi contenuto caricato AEM risorse di qualsiasi cartella sia applicato il profilo selezionato.

See also [Reprocessing assets in a folder after you have edited its processing profile](processing-profiles.md#reprocessing-assets-in-a-folder-after-you-have-edited-its-processing-profile).

**Per applicare un profilo video a livello globale**,

* Passa al CRXDE Lite al seguente nodo: `/content/dam/jcr:content`. Aggiungete la proprietà `videoProfile:/libs/settings/dam/video/dynamicmedia/<name of video encoding profile>` e toccate **[!UICONTROL Salva tutto.]**

   ![chlimage_1-519](assets/chlimage_1-519.png)
* Potete [monitorare l’avanzamento di un processo](#monitoring-the-progress-of-an-encoding-job)di elaborazione del profilo video.

## Monitoraggio dell’avanzamento di un processo di elaborazione del profilo video {#monitoring-the-progress-of-an-encoding-job}

Viene visualizzato un indicatore di elaborazione (o una barra di avanzamento) che consente di monitorare visivamente l’avanzamento di un processo di elaborazione del profilo video.

Potete inoltre visualizzare il `error.log` file per monitorare l’avanzamento di un processo di codifica, verificare se la codifica è terminata o visualizzare eventuali errori di processo. L’ `error.log` elemento si trova nella `logs` cartella in cui è installata l’istanza di AEM.

## Rimozione di un profilo video dalle cartelle {#removing-a-video-profile-from-folders}

Quando rimuovete un profilo video da una cartella, tutte le sottocartelle ereditano automaticamente la rimozione del profilo dalla cartella principale. Tuttavia, l&#39;elaborazione dei file che si è verificata all&#39;interno delle cartelle rimane intatta.

Puoi rimuovere un profilo video da una cartella direttamente dal menu **[!UICONTROL Strumenti]** oppure, se ti trovi nella cartella, da **[!UICONTROL Impostazioni cartella.]** Questa sezione descrive come rimuovere i profili video dalle cartelle con entrambe le soluzioni.

### Rimozione di un profilo video dalle cartelle tramite l’interfaccia utente Profili {#removing-video-profiles-from-folders-by-way-of-the-profiles-user-interface}

1. Tocca il logo AEM e seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili video.]**
1. Selezionate il profilo video da rimuovere da una o più cartelle.
1. Tocca **[!UICONTROL Rimuovi profilo da cartelle]** e seleziona una o più cartelle da cui vuoi rimuovere il profilo, infine tocca **[!UICONTROL Rimuovi.]**

   Potete confermare che il profilo video non viene più applicato a una cartella perché il nome non viene più visualizzato sotto il nome della cartella.

### Rimozione di un profilo video dalle cartelle tramite Proprietà {#removing-video-profiles-from-folders-by-way-of-properties}

1. Toccate o fate clic sul logo AEM, accedete a **[!UICONTROL Risorse]** e quindi alla cartella da cui desiderate rimuovere un profilo video.
1. Sulla cartella, toccate o fate clic sul segno di spunta per selezionarlo, quindi toccate o fate clic su **[!UICONTROL Proprietà.]**
1. Seleziona la scheda **[!UICONTROL Profili video]**, fai clic su **[!UICONTROL Nessuno]** dal menu a discesa e infine tocca **[!UICONTROL Salva e chiudi.]** Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

