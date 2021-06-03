---
title: Profili video
description: Dynamic Media dispone già di un profilo di codifica video adattivo predefinito. Le impostazioni di questo profilo predefinito sono ottimizzate per offrire ai clienti la migliore esperienza di visualizzazione possibile. Puoi anche aggiungere ritaglio avanzato ai video.
uuid: 26a20984-db63-41e9-b16c-6e164b7596a0
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
discoiquuid: 3b8791c8-2c97-42b7-b4a9-e1157ac9ea02
docset: aem65
feature: Profili video
role: Business Practitioner, Administrator
exl-id: b290fac2-7259-45d7-b733-70419d632b07
source-git-commit: b1e0ea01688095b29d8fb18baf6fa0bda660dad5
workflow-type: tm+mt
source-wordcount: '3704'
ht-degree: 18%

---

# Profili video {#video-profiles}

Dynamic Media dispone già di un profilo di codifica video adattivo predefinito. Le impostazioni di questo profilo predefinito sono ottimizzate per offrire ai clienti la migliore esperienza di visualizzazione possibile. Quando si codificano i video sorgente primari utilizzando il profilo di codifica video adattivo, durante la riproduzione il lettore video regola automaticamente la qualità del flusso video in base alla velocità di connessione Internet dei clienti. Questo è noto come streaming adattivo.

Di seguito sono riportati altri fattori che determinano la qualità dei video:

* **Risoluzione del video sorgente principale caricato**

   Se il video MP4 è stato registrato a una risoluzione inferiore, ad esempio 240p o 360p, non può essere trasmesso in alta definizione.

* **Dimensioni del lettore video**

   Per impostazione predefinita, la proprietà &quot;Width&quot; nel profilo di codifica video adattiva è impostata su &quot;Auto&quot;. Anche in questo caso, durante la riproduzione, viene utilizzata la migliore qualità in base alle dimensioni del lettore.

Consulta [Best practice per la codifica video](/help/assets/video.md#best-practices-for-encoding-videos).

Consulta anche [Tecniche consigliate per l’organizzazione delle risorse digitali per l’utilizzo dei profili di elaborazione](/help/assets/organize-assets.md).

>[!NOTE]
>
>Per generare i metadati di un video e le miniature delle immagini video associate, il video stesso deve seguire il processo di codifica di Dynamic Media. In AEM, il flusso di lavoro **[!UICONTROL Codifica video Dynamic Media]** codifica i video se hai abilitato Dynamic Media e hai impostato Cloud Services per i video. Questo flusso di lavoro acquisisce la cronologia del processo del flusso di lavoro e le informazioni di errore. Consulta la sezione [Monitoraggio della codifica video e stato della pubblicazione su YouTube](/help/assets/video.md#monitoring-video-encoding-and-youtube-publishing-progress). Se hai abilitato Dynamic Media e hai impostato Cloud Services per i video, il flusso di lavoro **[!UICONTROL Codifica video Dynamic Media]** ha effetto automaticamente al momento del caricamento di un video. (Se non utilizzi Dynamic Media, il flusso di lavoro **[!UICONTROL Aggiorna risorsa DAM]** ha effetto.)
>
>I metadati sono utili nella ricerca delle risorse. Le miniature sono immagini video statiche generate durante la codifica. Sono richieste dal sistema di AEM e utilizzate nell’interfaccia utente per identificare visivamente i video nella vista Schede, nella vista Risultati ricerca e nella vista Elenco risorse. Puoi visualizzare le miniature generate toccando l’icona Rappresentazioni (una palette del pittore) di un video codificato.

Al termine della creazione del profilo video, lo si applica a una cartella o a più cartelle. Consulta [Applicazione di un profilo video alle cartelle.](#applying-a-video-profile-to-folders)

Per definire parametri di elaborazione avanzati per altri tipi di risorse, consulta [Configurazione dell’elaborazione delle risorse](/help/assets/config-dms7.md#configuring-asset-processing).

Vedere anche [Profili per l&#39;elaborazione di metadati, immagini e video](processing-profiles.md).

## Predefiniti di codifica video adattivo {#adaptive-video-encoding-presets}

La tabella seguente identifica i profili di codifica best practice per lo streaming di video adattivo su dispositivi mobili e tablet e computer desktop. Puoi usare questi predefiniti per qualsiasi video con proporzioni.

<table>
 <tbody>
  <tr>
   <td><strong>Codec formato video</strong></td>
   <td><strong>Dimensioni video - Larghezza (px)</strong></td>
   <td><strong>Dimensioni video - Altezza (px)</strong></td>
   <td><strong>Mantieni proporzioni?</strong></td>
   <td><strong>Bitrate video (Kbps)</strong></td>
   <td><strong>Frame rate video (Fps)</strong></td>
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

La funzione di ritaglio avanzato per i video, una funzione opzionale disponibile in Profili video, è uno strumento che utilizza la potenza dell’intelligenza artificiale in Adobe Sensei per rilevare e ritagliare automaticamente il punto focale in qualsiasi video adattivo o video progressivo caricato, indipendentemente dalle dimensioni.

I formati video supportati per il ritaglio intelligente includono MP4, MKV, MOV, AVI, FLV e WMV.

La dimensione massima supportata del file video per il ritaglio avanzato è il seguente criterio:

* Durata di cinque minuti.
* 30 frame al secondo (FPS).
* Dimensione del file di 300 MB.

Adobe Sensei è attualmente limitato a 9000 fotogrammi. Cioè, cinque minuti a 30 fps. Se il video ha un valore FPS più alto, la durata massima del video supportato diminuisce. Ad esempio, un video a 60 fps deve essere lungo due minuti e mezzo per essere supportato da Adobe Sensai e Smart crop.

![Ritaglio avanzato per video](assets/smart-crop-video.png)

>[!IMPORTANT]
>
>Affinché il ritaglio avanzato funzioni correttamente nel video, è necessario includere uno o più predefiniti di codifica video con il profilo video.

Per utilizzare il ritaglio avanzato per i video, crea un profilo di codifica video adattivo o progressivo. Come parte del profilo, utilizza lo strumento **[!UICONTROL Smart Crop Ratio]** per selezionare le proporzioni predefinite. Ad esempio, dopo aver definito i predefiniti di codifica video, puoi aggiungere una definizione di &quot;Mobile Landscape&quot; con proporzioni pari a 16x9 e una definizione di &quot;Mobile Portrait&quot; con proporzioni pari a 9x16. Altri rapporti di formato o ritaglio da cui è possibile scegliere sono 1x1, 4x3 e 4x5.

![Modifica di un profilo di codifica video con lo smart crop](assets/edit-smart-crop-video2.png)

Nel profilo video puoi attivare o disattivare il ritaglio avanzato video, semplicemente utilizzando il cursore posto all’estrema destra di **[!UICONTROL Smart Crop Ratio (Proporzioni ritaglio avanzate)]** nell’interfaccia utente.

Dopo aver creato e salvato il profilo video, puoi applicarlo alle cartelle desiderate.

Consulta [Applicazione di profili video a cartelle specifiche](#applying-video-profiles-to-specific-folders) o [Applicazione di un profilo video a livello globale](#applying-a-video-profile-globally).

Vedi anche [Ritaglio avanzato per le immagini](image-profiles.md).

## Creazione di un profilo video per lo streaming adattivo {#creating-a-video-encoding-profile-for-adaptive-streaming}

Dynamic Media è già dotato di un profilo di codifica video adattivo predefinito, un gruppo di impostazioni di caricamento video per MP4 H.264, ottimizzato per la migliore esperienza di visualizzazione. Puoi usare questo profilo quando carichi i tuoi video.

Tuttavia, se questo profilo predefinito non soddisfa le tue esigenze, puoi scegliere di creare un tuo profilo di codifica video adattivo. Quando utilizzi l’impostazione **[!UICONTROL Codifica per lo streaming adattivo]**, come best practice, vengono convalidati tutti i predefiniti di codifica aggiunti al profilo per garantire che tutte le immagini video abbiano le stesse proporzioni. Inoltre, i video codificati vengono trattati come un set a più bit rate per lo streaming.

Quando crei il profilo di codifica video, noterai che la maggior parte delle opzioni di codifica sono precompilate con le impostazioni predefinite consigliate per aiutarti. Tuttavia, se selezioni un valore diverso da quello predefinito consigliato, tieni presente che potrebbe causare problemi di qualità video durante la riproduzione e altri problemi di prestazioni.

Pertanto, per tutti i predefiniti di codifica video MP4 H.264 presenti nel profilo, i seguenti valori vengono convalidati per garantire che siano gli stessi tra i singoli predefiniti di codifica nel profilo, consentendo in tal modo lo streaming adattivo:

* Codec video formato - MP4 H.264 (.mp4)
* Codec audio
* Bitrate audio
* Mantieni proporzioni
* Codifica a due passate
* Bitrate costante
* Profilo H264
* Frequenza di campionamento audio

Se i valori non sono uguali, puoi continuare a creare il profilo così com’è. Tuttavia, lo streaming adattivo non sarà possibile. Gli utenti sperimenteranno invece lo streaming a bitrate singolo. È consigliabile modificare le impostazioni di codifica per utilizzare gli stessi valori tra i singoli predefiniti di codifica nel profilo. Se è abilitato &quot;Encode for adaptive streaming&quot;, l’editor del profilo video/predefinito deve applicare la parità delle impostazioni di codifica dei video adattivi.

Vedi anche [Creazione di un profilo di codifica video per lo streaming progressivo](#creating-a-video-encoding-profile-for-progressive-streaming).

Vedere anche [Best practice per la codifica video](/help/assets/video.md#best-practices-for-encoding-videos).

Per definire parametri di elaborazione avanzati per altri tipi di risorse, consulta [Configurazione dell’elaborazione delle risorse](/help/assets/config-dms7.md#configuring-asset-processing).

**Per creare un profilo video per lo streaming** adattivo,

1. Tocca il logo AEM e seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili video]**.
1. Tocca o fai clic su **[!UICONTROL Crea]** per aggiungere un nuovo profilo video.

1. Immetti un nome e una descrizione per il profilo.
1. Nella pagina Crea/Modifica predefiniti di codifica video , tocca **[!UICONTROL Aggiungi predefinito di codifica video]**.
1. Nella scheda **[!UICONTROL Base]** , imposta le opzioni video e audio.
Toccare l’icona delle informazioni accanto a ciascuna opzione per ottenere descrizioni aggiuntive o impostazioni consigliate in base al codec del formato video selezionato.
1. Sotto l&#39;intestazione Dimensione video, assicurarsi che sia selezionato **[!UICONTROL Mantieni rapporto di formato]**.
1. Imposta la risoluzione del fotogramma video in pixel. Utilizzare il valore **[!UICONTROL Auto]** per ridimensionare automaticamente in modo che corrisponda alle proporzioni della sorgente (rapporto larghezza/altezza). Ad esempio, Auto x 480 o 640 x Auto.

1. Effettua una delle operazioni seguenti:

   * Nel campo **[!UICONTROL Larghezza]**, immetti **[!UICONTROL auto]**. Nel campo **[!UICONTROL Altezza]**, immetti un valore in pixel.

   * Per visualizzare le dimensioni del video, tocca l’icona Informazioni (i) a destra di **[!UICONTROL Altezza]** per aprire la pagina Calcolatore dimensioni . Utilizza **[!UICONTROL Calcolatore dimensioni]** per impostare le dimensioni video (rappresentate dalla casella blu) desiderate. Al termine, tocca **[!UICONTROL X]** nell’angolo superiore destro.

1. (Facoltativo) Tocca la scheda **[!UICONTROL Avanzate]** e assicurati che la casella di controllo **[!UICONTROL Usa valori predefiniti]** sia selezionata (scelta consigliata). In alternativa, puoi modificare le impostazioni audio e video avanzate.
1. Nell’angolo in alto a destra della pagina, tocca **[!UICONTROL Salva]** per salvare il predefinito.
1. Effettua una delle operazioni seguenti:
   * Ripeti i passaggi 4-10 per creare altri predefiniti di codifica. Lo streaming video adattivo richiede più di un predefinito video.
   * Procedi al passaggio successivo.

1. (Facoltativo) Per aggiungere video di ritaglio avanzato ai video a cui verrà applicato questo profilo, procedi come segue:
   * Nella pagina Modifica profilo video, a destra dell’intestazione Rapporto ritaglio avanzato , tocca **[!UICONTROL Aggiungi nuovo]**.
   * Nel campo Nome , digita un nome per il rapporto di ritaglio che ti aiuterà a identificarlo facilmente.
   * Dall&#39;elenco a discesa **[!UICONTROL Rapporto ritaglio]**, selezionare il rapporto da utilizzare.

1. Effettua una delle operazioni seguenti:

   * Continua ad aggiungere nuovi rapporti di ritaglio in base alle esigenze.
   * Procedi al passaggio successivo.

1. Nell’angolo in alto a destra della pagina, tocca di nuovo **[!UICONTROL Salva]** per salvare il profilo.

Ora puoi applicare il profilo alle cartelle che contengono video. Consulta [Applicazione di un profilo video alle cartelle](#applying-a-video-profile-to-folders) o [Applicazione di un profilo video a livello globale](#applying-a-video-profile-globally).

## Creazione di un profilo video per lo streaming progressivo {#creating-a-video-encoding-profile-for-progressive-streaming}

Se scegli di non utilizzare l’opzione **[!UICONTROL Codifica per lo streaming adattivo]**, tutti i predefiniti di codifica aggiunti al profilo vengono trattati come rappresentazioni video individuali per lo streaming a bitrate singolo o per la distribuzione progressiva di video. Inoltre, non esiste una convalida per garantire che tutte le rappresentazioni video abbiano le stesse proporzioni.

A seconda della modalità di esecuzione, i codec del formato video supportati sono i seguenti:

* Modalità Dynamic Media-Scene7: H.264 (mp4)
* Modalità Dynamic Media-Hybrid: H.264 (.mp4), WebM

Vedi anche [Creazione di un profilo di codifica video per lo streaming adattivo](#creating-a-video-encoding-profile-for-adaptive-streaming).

Vedere anche [Best practice per la codifica video](/help/assets/video.md#best-practices-for-encoding-videos).

Per definire parametri di elaborazione avanzati per altri tipi di risorse, consulta [Configurazione dell’elaborazione delle risorse](/help/assets/config-dms7.md#configuring-asset-processing).

**Per creare un profilo video per lo streaming progressivo:**

1. Tocca il logo AEM e seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili video]**.
1. Tocca **[!UICONTROL Crea]** per aggiungere un nuovo profilo video.
1. Immetti un nome e una descrizione per il profilo.
1. Nella pagina Crea/Modifica predefiniti di codifica video , tocca **[!UICONTROL Aggiungi predefinito di codifica video]**.
1. Nella scheda **[!UICONTROL Base]** , imposta le opzioni video e audio.
Toccare l’icona delle informazioni accanto a ciascuna opzione per ottenere descrizioni aggiuntive o impostazioni consigliate in base al codec del formato video selezionato.
1. (Facoltativo) Sotto l&#39;intestazione Dimensione video, deseleziona **[!UICONTROL Mantieni proporzioni]**.
1. Effettua le seguenti operazioni:
   * Nel campo **[!UICONTROL Larghezza]**, immetti **[!UICONTROL auto]**.
   * Nel campo **[!UICONTROL Altezza]**, immetti un valore in pixel.
Per visualizzare le dimensioni del video, tocca l’icona delle informazioni dell’altezza per aprire la pagina **[!UICONTROL Calcolatore dimensioni]** . Utilizza la pagina **[!UICONTROL Calcolatore dimensioni]** per impostare ulteriormente la dimensione video (casella blu) in base alle tue preferenze. Al termine, nell’angolo superiore destro della finestra di dialogo, tocca **[!UICONTROL X]**.
1. (Facoltativo) Effettua una delle seguenti operazioni:

   * Tocca la scheda **[!UICONTROL Avanzate]** e assicurati che la casella di controllo **[!UICONTROL Usa valori predefiniti]** sia selezionata (scelta consigliata).

   * Deselezionare la casella di controllo **[!UICONTROL Usa valori predefiniti]** e specificare le impostazioni video e audio desiderate.
Toccare l’icona delle informazioni accanto a ciascuna opzione per ottenere descrizioni aggiuntive o impostazioni consigliate in base al codec del formato video selezionato.

1. Nell’angolo in alto a destra della pagina, tocca **[!UICONTROL Salva]** per salvare il predefinito.
1. Effettua una delle operazioni seguenti:

   * Ripeti i passaggi 4-9 per creare altri predefiniti di codifica.
   * Procedi al passaggio successivo.

1. (Facoltativo) Per aggiungere video di ritaglio avanzato ai video a cui verrà applicato questo profilo, procedi come segue:

   * Nella pagina Modifica profilo video, a destra dell’intestazione Rapporto ritaglio avanzato , tocca **[!UICONTROL Aggiungi nuovo]**.
   * Nel campo Nome , digita un nome per il rapporto di ritaglio che ti aiuterà a identificarlo facilmente.
   * Dall&#39;elenco a discesa **[!UICONTROL Rapporto ritaglio]**, selezionare il rapporto da utilizzare.

1. Effettua una delle operazioni seguenti:

   * Continua ad aggiungere nuovi rapporti di ritaglio in base alle esigenze.
   * Procedi al passaggio successivo.

1. Nell’angolo superiore destro della pagina, tocca **[!UICONTROL Salva]** per salvare il profilo.

Ora puoi applicare il profilo alle cartelle che contengono video. Consulta [Applicazione di un profilo video alle cartelle](#applying-a-video-profile-to-folders) o [Applicazione di un profilo video a livello globale](#applying-a-video-profile-globally).

## Utilizzo di parametri di codifica video personalizzati {#using-custom-added-video-encoding-parameters}

Puoi modificare un profilo di codifica video esistente per sfruttare parametri di codifica video avanzati che non sono disponibili nell’interfaccia utente quando crei o modifichi un profilo video in AEM. Puoi aggiungere al profilo esistente uno o più parametri avanzati, ad esempio minBitrate e maxBitrate.

**Per utilizzare parametri** di codifica video personalizzati:

1. Tocca il logo AEM, quindi seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Generale]** > **[!UICONTROL CRXDE Lite]**.
1. Dalla pagina CRXDE Lite, nel pannello Explorer a sinistra, passa alla pagina seguente:

   `/conf/global/settings/dam/dm/presets/video/*name_of_video_encoding_profile_to_edit`

1. Nel pannello in basso a destra della pagina, dalla scheda Proprietà, specifica **[!UICONTROL Nome]**, **[!UICONTROL Tipo]** e **[!UICONTROL Valore]** del parametro da utilizzare.

   Sono disponibili i seguenti parametri avanzati da utilizzare:

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
   <td>Livello H.264 da utilizzare per la codifica. Normalmente questo viene determinato automaticamente in base alle impostazioni di codifica in uso.</td>
   <td><code>String</code></td>
   <td><p>10 * livello h264</p> <p>Ad esempio, 3,0 = 30, 1,3 = 13)</p> <p>Nessun valore predefinito.</p> </td>
  </tr>
  <tr>
   <td><code>keyframe</code></td>
   <td>Il numero di fotogrammi di destinazione tra i fotogrammi chiave. Calcola questo valore per generare un fotogramma chiave ogni 2-10 secondi. Ad esempio, a 30 fotogrammi al secondo, l'intervallo del fotogramma chiave dovrebbe essere 60-300.<br /> <br /> Intervalli di fotogrammi chiave più bassi migliorano il comportamento di ricerca e commutazione del flusso per le codifiche video adattive e possono anche migliorare la qualità dei video che hanno molto movimento. Tuttavia, poiché i fotogrammi chiave aumentano le dimensioni di un file, un intervallo di fotogrammi chiave inferiore di solito si traduce in una qualità video complessiva inferiore a un dato bitrate.</td>
   <td><code>String</code></td>
   <td><p>Numero positivo.</p> <p>Il valore predefinito è 300.</p> <p>Il valore consigliato per HLS (HTTP Live Streaming) è 60-90.</p> </td>
  </tr>
  <tr>
   <td><code>minBitrate</code></td>
   <td><p>Bitrate minimo per consentire codifiche a bit rate variabile, in Kbps (kilobit al secondo).</p> <p>Questo parametro si applica solo quando<strong> Use Constant Bitrate</strong> è deselezionato nella scheda Avanzate quando crei o modifichi un profilo di codifica video.</p> <p>Vedere anche <a href="/help/assets/video.md#bitrate">Bitrate</a>.</p> </td>
   <td><code>String</code></td>
   <td><p>Numero positivo, in Kbps.</p> <p>Nessun valore predefinito.</p> </td>
  </tr>
  <tr>
   <td><code>maxBitrate</code></td>
   <td><p>Bitrate massimo per consentire codifiche a bit rate variabile, in Kbps.</p> <p>Questo parametro si applica solo quando<strong> Use Constant Bitrate</strong> è deselezionato nella scheda Avanzate quando crei o modifichi un profilo di codifica video.</p> <p>Vedere anche <a href="/help/assets/video.md#bitrate">Bitrate</a>.</p> </td>
   <td><code>String</code></td>
   <td><p>Numero positivo, in Kbps.</p> <p>Nessun valore predefinito. Tuttavia, il valore consigliato è fino a due volte il bitrate di codifica.</p> </td>
  </tr>
  <tr>
   <td><code>audioBitrateCustom</code></td>
   <td>Impostare il valore su <code>true</code> per forzare un bitrate costante per lo streaming audio, se supportato dal codec audio.</td>
   <td><code>String</code></td>
   <td><p><code>true</code>/<code>false</code></p> <p>Il valore predefinito è <code>false</code>.</p> <p>Il valore consigliato per HLS (HTTP Live Streaming) è <code>false</code>.</p> <p> </p> </td>
  </tr>
 </tbody>
</table>

![chlimage_1-516](assets/chlimage_1-516.png)

1. Vicino all’angolo inferiore destro della pagina, tocca **[!UICONTROL Aggiungi]**.
1. Effettua una delle operazioni seguenti:

   * Ripeti i passaggi 3 e 4 per aggiungere un altro parametro al profilo di codifica video.
   * Nell’angolo in alto a sinistra della pagina, tocca **[!UICONTROL Salva tutto]**.

1. Nell’angolo in alto a sinistra della pagina CRXDE Lite, tocca l’icona **[!UICONTROL Indietro Home]** per tornare a AEM.

### Modifica di un profilo video {#editing-a-video-encoding-profile}

Puoi modificare qualsiasi profilo video creato per aggiungere, modificare o eliminare i predefiniti video all’interno di tale profilo.

Per impostazione predefinita, non è possibile modificare il profilo predefinito **[!UICONTROL Codifica video adattiva]** fornito con Dynamic Media. Puoi invece copiare facilmente il profilo e salvarlo con un nuovo nome. Puoi quindi modificare i predefiniti desiderati nel profilo copiato.

Vedere anche [Best practice per la codifica video](/help/assets/video.md#best-practices-for-encoding-videos).

Per definire parametri di elaborazione avanzati per altri tipi di risorse, consulta [Configurazione dell’elaborazione delle risorse](/help/assets/config-dms7.md#configuring-asset-processing).

**Per modificare un profilo** video:

1. Tocca il logo AEM e seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili video]**.
1. Nella pagina Profili video , controlla un nome di profilo video.
1. Sulla barra degli strumenti, tocca **[!UICONTROL Modifica]**.
1. Nella pagina Profilo di codifica video , modifica il nome e la descrizione desiderati.
1. Come best practice, accertati che la casella di controllo **[!UICONTROL Codifica per streaming adattivo]** sia selezionata.
Per una descrizione dello streaming adattivo, tocca l’icona delle informazioni. Se stai modificando un profilo video progressivo, non selezionare questa casella di controllo.
1. Nell’intestazione Predefiniti di codifica video , aggiungi, modifica o elimina i predefiniti di codifica video che compongono il profilo.

   Per ottenere descrizioni aggiuntive o impostazioni consigliate per il codec del formato video selezionato, tocca l’icona delle informazioni posta accanto a ciascuna opzione nelle schede **[!UICONTROL Base]** e **[!UICONTROL Avanzate]**.

1. Nell’angolo in alto a destra della pagina, tocca **[!UICONTROL Salva]**.

### Copia di un profilo video {#copying-a-video-encoding-profile}

1. Tocca il logo AEM e seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili video]**.
1. Nella pagina Profili video , controlla un nome di profilo video.
1. Sulla barra degli strumenti, tocca **[!UICONTROL Copia]**.
1. Nella pagina Profilo di codifica video , immetti un nuovo nome per il profilo.
1. Come best practice, accertati che la casella di controllo **[!UICONTROL Codifica per streaming adattivo]** sia selezionata. Per una descrizione dello streaming adattivo, tocca l’icona delle informazioni. Se copi un profilo video progressivo, non selezionare la casella di controllo.

   In modalità Dynamic Media - Hybrid, se un predefinito video WebM fa parte del profilo video, non è possibile codificare **[!UICONTROL per lo streaming adattivo]** perché tutti i predefiniti devono essere MP4.
1. Nell’intestazione Predefiniti di codifica video , aggiungi, modifica o elimina i predefiniti di codifica video che compongono il profilo.

   Per le impostazioni e le descrizioni consigliate, tocca l’icona delle informazioni posta accanto a ciascuna opzione nelle schede Base e Avanzate .

1. Nell’angolo in alto a destra della pagina, tocca **[!UICONTROL Salva]**.

### Eliminazione di un profilo video {#deleting-a-video-encoding-profile}

1. Tocca il logo AEM e seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili video]**.
1. Nella pagina Profili video , controlla uno o più nomi di profilo video.
1. Sulla barra degli strumenti, tocca **[!UICONTROL Elimina]**.
1. Toccare **[!UICONTROL OK]**.

## Applicazione di un profilo video alle cartelle {#applying-a-video-profile-to-folders}

Quando assegni un profilo video a una cartella, qualsiasi sottocartella eredita automaticamente il profilo dalla relativa cartella principale. Questo significa che puoi assegnare un solo profilo video a una cartella. Considera attentamente la struttura delle cartelle in cui caricare, archiviare, utilizzare e archiviare le risorse.

Se hai assegnato un profilo video diverso a una cartella, il nuovo profilo sostituisce il profilo precedente. Le risorse della cartella esistenti in precedenza rimangono invariate. Il nuovo profilo viene applicato alle risorse aggiunte successivamente alla cartella.

Le cartelle a cui è assegnato un profilo sono indicate nell&#39;interfaccia utente in base al nome del profilo visualizzato nel nome della scheda.

![chlimage_1-517](assets/chlimage_1-517.png)

Puoi applicare i profili video a cartelle specifiche o globalmente a tutte le risorse.

Puoi rielaborare le risorse in una cartella che dispone già di un profilo video esistente che hai successivamente modificato. Consulta [Rielaborazione delle risorse in una cartella dopo la modifica del profilo di elaborazione](processing-profiles.md#reprocessing-assets).

### Applicazione di un profilo video a cartelle specifiche {#applying-video-profiles-to-specific-folders}

Puoi applicare un profilo video a una cartella direttamente dal menu **[!UICONTROL Strumenti]** oppure, se ti trovi nella cartella, da **[!UICONTROL Proprietà]**. Questa sezione descrive come applicare i profili video alle cartelle con entrambe le soluzioni.

Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

Vedi anche [Rielaborazione delle risorse in una cartella dopo aver modificato il profilo di elaborazione](processing-profiles.md#reprocessing-assets).

#### Applicazione di un profilo video alle cartelle tramite l’interfaccia utente Profili {#applying-video-profiles-to-folders-by-way-of-the-profiles-user-interface}

1. Tocca il logo AEM e seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili video]**.
1. Seleziona il profilo video da applicare a una o più cartelle.
1. Tocca **[!UICONTROL Applica profilo a cartelle]** e seleziona una o più cartelle da utilizzare per ricevere le risorse appena caricate, quindi tocca **[!UICONTROL Applica]**. Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella in **[!UICONTROL Vista a schede]**.
Puoi [monitorare l&#39;avanzamento di un processo di elaborazione di un profilo video](#monitoring-the-progress-of-an-encoding-job).

#### Applicazione di un profilo video alle cartelle da Proprietà {#applying-video-profiles-to-folders-from-properties}

1. Tocca o fai clic sul logo AEM, vai a **[!UICONTROL Risorse]** e quindi alla cartella a cui desideri applicare un profilo video.
1. Sulla cartella, tocca il segno di spunta per selezionarlo, quindi tocca **[!UICONTROL Proprietà]**.
1. Seleziona la scheda **[!UICONTROL Profili video]** e fai clic sul profilo dal menu a discesa, infine tocca **[!UICONTROL Salva e chiudi]**. Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.

   ![chlimage_1-518](assets/chlimage_1-518.png)
Puoi  [monitorare l’avanzamento di un processo di elaborazione di un profilo video](#monitoring-the-progress-of-an-encoding-job).

### Applicazione globale di un profilo video {#applying-a-video-profile-globally}

Oltre ad applicare un profilo a una cartella, puoi anche applicarne uno a livello globale in modo che a qualsiasi contenuto caricato AEM risorse in una cartella sia applicato il profilo selezionato.

Vedi anche [Rielaborazione delle risorse in una cartella dopo aver modificato il profilo di elaborazione](processing-profiles.md#reprocessing-assets).

**Per applicare un profilo video a livello globale:**

* Passa a CRXDE Lite al seguente nodo: `/content/dam/jcr:content`. Aggiungi la proprietà `videoProfile:/libs/settings/dam/video/dynamicmedia/<name of video encoding profile>` e tocca **[!UICONTROL Salva tutto]**.

   ![chlimage_1-519](assets/chlimage_1-519.png)
* Puoi [monitorare l&#39;avanzamento di un processo di elaborazione di un profilo video](#monitoring-the-progress-of-an-encoding-job).

## Monitoraggio dell’avanzamento di un processo di elaborazione di un profilo video {#monitoring-the-progress-of-an-encoding-job}

Viene visualizzato un indicatore di elaborazione (o barra di avanzamento) che consente di monitorare visivamente l’avanzamento di un processo di elaborazione del profilo video.

È inoltre possibile visualizzare il file `error.log` per monitorare l’avanzamento di un processo di codifica, verificare se la codifica è stata completata o visualizzare eventuali errori di processo. La cartella `error.log` si trova nella cartella `logs` in cui è installata l&#39;istanza di AEM.

## Rimozione di un profilo video dalle cartelle {#removing-a-video-profile-from-folders}

Quando rimuovi un profilo video da una cartella, tutte le sottocartelle ereditano automaticamente la rimozione del profilo dalla relativa cartella principale. Tuttavia, l’elaborazione dei file che si è verificata all’interno delle cartelle rimane intatta.

Puoi rimuovere un profilo video da una cartella direttamente dal menu **[!UICONTROL Strumenti]** oppure, se ti trovi nella cartella, da **[!UICONTROL Impostazioni cartella]**. Questa sezione descrive come rimuovere i profili video dalle cartelle con entrambe le soluzioni.

### Rimozione di un profilo video dalle cartelle tramite l’interfaccia utente Profili {#removing-video-profiles-from-folders-by-way-of-the-profiles-user-interface}

1. Tocca il logo AEM e seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Profili video]**.
1. Seleziona il profilo video da rimuovere da una o più cartelle.
1. Tocca **[!UICONTROL Rimuovi profilo da cartelle]** e seleziona una o più cartelle da cui vuoi rimuovere il profilo, infine tocca **[!UICONTROL Rimuovi]**.

   Puoi confermare che il profilo video non viene più applicato a una cartella perché il nome non viene più visualizzato sotto il nome della cartella.

### Rimozione di un profilo video dalle cartelle tramite Proprietà {#removing-video-profiles-from-folders-by-way-of-properties}

1. Tocca o fai clic sul logo AEM, vai a **[!UICONTROL Risorse]** e quindi alla cartella da cui vuoi rimuovere un profilo video.
1. Sulla cartella, tocca il segno di spunta per selezionarlo, quindi tocca **[!UICONTROL Proprietà]**.
1. Seleziona la scheda **[!UICONTROL Profili video]**, fai clic su **[!UICONTROL Nessuno]** dal menu a discesa e infine tocca **[!UICONTROL Salva e chiudi]**. Le cartelle a cui è già stato assegnato un profilo sono indicate dalla visualizzazione del nome del profilo che è posto direttamente sotto il nome della cartella.
