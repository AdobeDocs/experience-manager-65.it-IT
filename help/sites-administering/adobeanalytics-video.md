---
title: Configurazione del tracciamento video per  Adobe Analytics
seo-title: Configurazione del tracciamento video per  Adobe Analytics
description: Scoprite come configurare il tracciamento video per SiteCatalyst.
seo-description: Scoprite come configurare il tracciamento video per SiteCatalyst.
uuid: 5a862f05-abfa-42a2-ad40-4c1c32f1bd75
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: a18ddac1-9e4c-4857-9cb3-4d5eeb8dd9ec
docset: aem65
translation-type: tm+mt
source-git-commit: 90c99e527a40bb663d4f32d8746b46cf34a2319f
workflow-type: tm+mt
source-wordcount: '1766'
ht-degree: 1%

---


# Configurazione del tracciamento video per  Adobe Analytics{#configuring-video-tracking-for-adobe-analytics}

Esistono diversi metodi per tenere traccia degli eventi video, due dei quali sono opzioni precedenti per le versioni precedenti di  Adobe Analytics. Queste opzioni precedenti sono: Precedenti pietre miliari e Secondi legacy.

>[!NOTE]
>
>Prima di continuare, accertatevi di disporre di un video **** riproducibilecaricato all’interno di AEM.
>
>Per essere certi che i video vengano riprodotti sulla pagina, consultate **[questa esercitazione](/help/sites-authoring/default-components-foundation.md#video)** per informazioni su come transcodificare i file video in AEM.

Per impostare un framework per il tracciamento video con ciascun metodo, utilizzate la procedura seguente.

>[!NOTE]
>
>Per le nuove implementazioni, si consiglia di **non utilizzare** le opzioni legacy per il tracciamento video. Utilizzare invece il metodo **Milestones** .

## Passaggi comuni {#common-steps}

1. Per impostare una pagina Web, trascinate un componente **** video dalla barra laterale e aggiungete un **video riproducibile come risorsa** per il componente

1. [Creare una configurazione e un framework](/help/sites-administering/adobeanalytics.md)Adobe Analytics .

   * Gli esempi nelle sezioni seguenti utilizzano il nome **my-sc-configuration** per la configurazione e il **video** per il framework.

1. Nella pagina del framework, selezionate un RSID e impostate l’utilizzo su tutti. ([https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html](https://localhost:4502/cf#/etc/cloudservices/sitecatalyst/videoconf/videofw.html))
1. Dalla categoria del componente Generale nella barra laterale, trascinate il componente Video nella cornice.
1. Selezionare un metodo di tracciamento:

   * [Pietre miliari](/help/sites-administering/adobeanalytics.md)
   * [Pietre miliari non legacy](/help/sites-administering/adobeanalytics.md)
   * [Precedenti pietre miliari](/help/sites-administering/adobeanalytics.md)
   * [Secondi legacy](/help/sites-administering/adobeanalytics.md)

1. Quando si seleziona un metodo di tracciamento, l’elenco delle variabili CQ cambia di conseguenza. Utilizzate le sezioni seguenti per informazioni su come configurare ulteriormente il componente e mappare le variabili CQ con  proprietà Adobe Analytics.

## Milestones {#milestones}

Il metodo Milestones monitora la maggior parte delle informazioni sul video, è altamente personalizzabile e facile da configurare.

Per utilizzare il metodo Milestones, specificate gli offset di traccia basati sul tempo per definire le pietre miliari. Quando la riproduzione di un video supera una fase cardine, la pagina chiama  Adobe Analytics per tenere traccia dell’evento. Per ogni pietra miliare definita, il componente crea una variabile CQ che è possibile mappare a una proprietà Adobe Analytics . Il nome di queste variabili CQ utilizza il formato seguente:

```shell
eventdata.events.milestoneXX
```

Il suffisso XX è l’offset della traccia che definisce la pietra miliare. Ad esempio, se specificate gli offset di traccia di 4, 8, 16, 20 e 28 secondi, vengono generate le seguenti variabili CQ:

* `eventdata.events.milestone4`
* `eventdata.events.milestone8`
* `eventdata.events.milestone16`
* `eventdata.events.milestone20`
* `eventdata.events.milestone28`

Nella tabella seguente sono descritte le variabili CQ predefinite fornite per il metodo Milestones:

<table>
 <tbody>
  <tr>
   <th>Variabili CQ</th>
   <th> delle proprietà Adobe Analytics</th>
  </tr>
  <tr>
   <td>eventdata.videoName </td>
   <td>Le variabili mappate a questo file conterranno il nome <strong>intuitivo</strong> (<strong>Titolo</strong>) del video, se impostato in DAM; se non è impostato, viene inviato il nome <strong>del</strong> file del video. È stato inviato solo una volta, all’inizio della riproduzione di un video.</td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>Le variabili mappate a questo file conterranno il nome del file. Inviato solo con eventdata.events.a.media.view </td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>Le variabili mappate a questo file conterranno il percorso del file sul server. Inviato solo con eventdata.events.a.media.view </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.segmentView </td>
   <td>Inviato ogni volta che viene superata una fase cardine del segmento </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.timePlayed</td>
   <td>Inviato ogni volta che viene attivata una pietra miliare, viene inviato anche il numero di secondi trascorsi dall'utente durante la visione di un dato segmento. ad esempio eventX=21<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.view </td>
   <td>Inviato all’inizializzazione della visualizzazione video</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.complete </td>
   <td>Inviato al termine della riproduzione del video<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.milestoneX </td>
   <td>Inviato quando il milestone viene passato, X indica il secondo in cui il cardine viene attivato a<br /> </td>
  </tr>
  <tr>
   <td>eventdata.a.contentType </td>
   <td>Inviato su ogni pietra miliare; viene visualizzato come pev3 nella chiamata Adobe Analytics , solitamente inviato come "video"<br /> </td>
  </tr>
  <tr>
   <td>eventdata.a.media.name </td>
   <td>Corrisponde esattamente a eventdata.videoName </td>
  </tr>
  <tr>
   <td>eventdata.a.media.segment </td>
   <td>Contiene informazioni sul segmento visualizzato, ad esempio 2:O:4-8 </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Potete impostare un nome **semplice** per un video aprendo il video per la modifica in DAM e impostando il campo di metadati **Titolo** sul nome desiderato.

1. Dopo aver selezionato Valori intermedi come metodo di tracciamento, nella casella Offset traccia immettete un elenco separato da virgole di scostamenti di tracciamento in secondi. Ad esempio, il seguente valore definisce le pietre miliari a 4, 8, 16, 20 e 28 secondi dall’inizio del video:

   ```xml
   4,8,16,20,24
   ```

   I valori di offset devono essere numeri interi maggiori di 0. Il valore predefinito è `10,25,50,75`.

1. Per mappare le variabili CQ su  proprietà Adobe Analytics, trascinate le proprietà  Adobe Analytics da ContentFinder accanto alla variabile CQ sul componente.

   Per informazioni sull’ottimizzazione delle mappature, consultate la guida [Measuring Video in  Adobe Analytics](https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html) guide.

1. [Aggiungete il framework](/help/sites-administering/adobeanalytics.md) alla pagina.
1. Per verificare l’impostazione in modalità **** Anteprima, riprodurre il video per attivare  chiamate Adobe Analytics.

Gli esempi  di dati di tracciamento Adobe Analytics che seguono si applicano al tracciamento delle attività cardine utilizzando gli offset di tracciamento di 4,8,16,20 e 24, e le mappature seguenti per le variabili CQ:

<table>
 <tbody>
  <tr>
   <th>Variabile CQ</th>
   <th>, proprietà Adobe Analytics</th>
  </tr>
  <tr>
   <td>eventdata.videoName </td>
   <td>prop2</td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>prop3 </td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>prop4</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.segmentView </td>
   <td>event1</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.timePlayed</td>
   <td>event2<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.view </td>
   <td>event3</td>
  </tr>
  <tr>
   <td>eventdata.events.a.media.complete </td>
   <td>event4<br /> </td>
  </tr>
  <tr>
   <td>eventdata.events.milestone4</td>
   <td>event10</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone8</td>
   <td>event11</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone16</td>
   <td>event12</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone20</td>
   <td>event13</td>
  </tr>
  <tr>
   <td>eventdata.events.milestone24</td>
   <td>event14</td>
  </tr>
  <tr>
   <td>eventdata.a.contentType </td>
   <td>eVar3</td>
  </tr>
  <tr>
   <td>eventdata.a.media.name </td>
   <td> eVar 1, prop1 </td>
  </tr>
  <tr>
   <td>eventdata.a.media.segment </td>
   <td>eVar2</td>
  </tr>
 </tbody>
</table>

Per questo esempio, il componente Video viene visualizzato come segue nella pagina del framework:

![video1](assets/video1.png)

>[!NOTE]
>
>Per visualizzare le chiamate effettuate a  Adobe Analytics utilizzate uno strumento appropriato, come DigitalPulse Debugger o Fiddler.

Le chiamate a  Adobe Analytics utilizzando l&#39;esempio fornito dovrebbero essere simili a quelle riportate di seguito quando vengono visualizzate con DigitalPulse Debugger:

![chlimage_1-128](assets/chlimage_1-128.png)

*Si tratta della **prima chiamata**effettuata a  Adobe Analytics contenente i valori seguenti:*

* *prop1 e  eVar1 per eventdata.a.media.name,*
* *props2-4, insieme a  eVar2 e eVar3 contenente contentType (video) e segmento (1:O:1-4)*
* *event3 mappato a eventdata.events.a.media.view.*

![chlimage_1-129](assets/chlimage_1-129.png)

*Questa è la **terza chiamata**effettuata a  Adobe Analytics:*

* *prop1 e  eVar1 contengono a.media.name;*
* *event1 perché è stato visualizzato un segmento*
* *event2 inviato con tempo riprodotto = 4*
* *event11 inviato perché è stato raggiunto eventdata.events.milestone8*
* *prop2-4 non vengono inviati (poiché eventdata.events.a.media.view non è stato attivato)*

## Pietre miliari non legacy {#non-legacy-milestones}

Il metodo Milestones non legacy è simile al metodo Milestones, tranne che per le pietre miliari, che vengono definite utilizzando percentuali della lunghezza del binario. I comuni sono i seguenti:

* Quando la riproduzione di un video supera una fase cardine, la pagina chiama  Adobe Analytics per tenere traccia dell’evento.
* Set [statico di variabili](#cqvars) CQ definite per la mappatura con  proprietà Adobe Analytics.
* Per ogni pietra miliare definita, il componente crea una variabile CQ che è possibile mappare a una proprietà Adobe Analytics .

Il nome di queste variabili CQ utilizza il formato seguente:

Il suffisso XX è la percentuale di lunghezza del brano che definisce il cardine. Se ad esempio si specificano percentuali pari a 10, 25, 50 e 75, vengono generate le seguenti variabili CQ:

* `eventdata.events.milestone10`
* `eventdata.events.milestone25`
* `eventdata.events.milestone50`
* `eventdata.events.milestone75`

```shell
eventdata.events.milestoneXX
```

1. Dopo aver selezionato Milestoni non legacy come metodo di tracciamento, nella casella Offset traccia immettete un elenco separato da virgole di percentuali di lunghezza del brano. Ad esempio, il seguente valore predefinito definisce le tappe a 10, 25, 50 e 75 percento della lunghezza della traccia:

   ```xml
   10,25,50,75
   ```

   I valori di offset devono essere numeri interi maggiori di 0.

1. Per mappare le variabili CQ su  proprietà Adobe Analytics, trascinate le proprietà  Adobe Analytics da ContentFinder accanto alla variabile CQ sul componente.

   Per informazioni sull’ottimizzazione delle mappature, consultate la guida [Measuring Video in  Adobe Analytics](https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html) guide.

1. [Aggiungete il framework](/help/sites-administering/adobeanalytics.md) alla pagina.
1. Per verificare l’impostazione in modalità **** Anteprima, riprodurre il video per attivare  chiamate Adobe Analytics.

## Precedenti pietre miliari {#legacy-milestones}

Questo metodo è simile al metodo Pietre miliari con la differenza che le pietre miliari specificate nel campo Offset ** tracciamento sono percentuali invece che punti impostati all’interno del video.

>[!NOTE]
>
>Il campo Offset tracciamento accetta solo un elenco separato da virgole contenente numeri interi compresi tra 1 e 100.

1. Impostare l&#39;offset della traccia.

   * e.g.10,50,75,100

   Inoltre, le informazioni inviate a  Adobe Analytics sono meno personalizzabili; sono disponibili solo 3 variabili per la mappatura:

<table>
 <tbody>
  <tr>
   <td>eventdata.videoName <br /> </td>
   <td>Le variabili mappate a questo file conterranno il nome <strong>intuitivo</strong> (<strong>Titolo</strong>) del video, se impostato in DAM; se il Titolo non è impostato, viene inviato il nome <strong>del</strong> file del video. È stato inviato solo una volta, all’inizio della riproduzione di un video.<br /> </td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>Le variabili mappate a questo file conterranno il nome del file. È stato inviato solo una volta, all’inizio della riproduzione di un video.</td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>La variabile mappata a questo conterrà il percorso del file sul server. È stato inviato solo una volta, all’inizio della riproduzione di un video.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Potete impostare un nome **semplice** per un video aprendo il video per la modifica in DAM e impostando il campo di metadati **Titolo** sul nome desiderato. È inoltre necessario salvare le modifiche apportate al termine.

1. Mappatura di queste variabili su prop da 1 a 3

   Il **resto delle informazioni** pertinenti nella chiamata sarà inviato concatenato in **una** variabile denominata **pev3**.

   **Le chiamate** di esempio per  Adobe Analytics utilizzando l&#39;esempio fornito dovrebbero essere simili a quelle riportate di seguito quando vengono visualizzate con DigitalPulse Debugger:

   ![lmilestones1](assets/lmilestones1.png)

   *La variabile **pev3**inviata nella chiamata contiene le informazioni seguenti:*

   * *Nome* - Il nome del file video (*film.avi*)

   * *Lunghezza* : lunghezza del file video, in secondi (*100*)

   * *Nome* lettore - Il lettore video utilizzato per riprodurre il file video (video ** HTML5)

   * *Secondi totali riprodotti* - Il numero totale di secondi di riproduzione del video (*25*)

   * *Timestamp* di inizio - Timestamp che identifica l&#39;avvio della riproduzione video (*1331035567*)

   * *Riproduci sessione* - I dettagli della sessione di riproduzione. Questo campo indica in che modo l’utente ha interagito con il video. Ciò potrebbe includere dati quali la posizione di inizio della riproduzione del video, l’utilizzo del cursore video per far avanzare il video e la posizione in cui si è interrotta la riproduzione del video (*L10E24S58L58 - video arrestato al secondo. 25 della sezione L10, quindi saltato al secondo. 48*)

## Secondi precedenti {#legacy-seconds}

Quando si utilizza il metodo** dei secondi precedenti**,  chiamate Adobe Analytics vengono attivate ogni N-esimo secondo, dove N è specificato nel campo dell&#39;offset del brano.

1. Imposta l&#39;offset della traccia su un numero qualsiasi di secondi,

   * ad esempio 6
   >[!NOTE]
   >
   >Il campo Offset tracciamento accetta solo numeri interi superiori a 0

   Le informazioni inviate a  Adobe Analytics sono meno personalizzabili. Sono disponibili solo 3 variabili per la mappatura:

<table>
 <tbody>
  <tr>
   <td>eventdata.videoName <br /> </td>
   <td>Le variabili mappate a questo file conterranno il nome <strong>intuitivo</strong> (<strong>Titolo</strong>) del video, se impostato in DAM; se il Titolo non è impostato, viene inviato il nome <strong>del</strong> file del video. È stato inviato solo una volta, all’inizio della riproduzione di un video.<br /> </td>
  </tr>
  <tr>
   <td>eventdata.videoFileName </td>
   <td>La variabile mappata a questo conterrà il nome del file. È stato inviato solo una volta, all’inizio della riproduzione di un video.</td>
  </tr>
  <tr>
   <td>eventdata.videoFilePath </td>
   <td>La variabile mappata a questo conterrà il percorso del file sul server. È stato inviato solo una volta, all’inizio della riproduzione di un video.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Potete impostare un nome **semplice** per un video aprendo il video per la modifica in DAM e impostando il campo di metadati **Titolo** sul nome desiderato. È inoltre necessario salvare le modifiche apportate al termine.

1. Mappare queste variabili a prop1, prop2 e prop3

   Il **resto delle informazioni** pertinenti nella chiamata sarà inviato concatinato in **una** variabile denominata **pev3**.

   Le chiamate a  Adobe Analytics utilizzando l&#39;esempio fornito dovrebbero essere simili a quelle riportate di seguito quando vengono visualizzate con DigitalPulse Debugger:

   ![lsecondi](assets/lseconds.png)

   *La chiamata è simile alla precedente chiamata Legacy Milestones. Si prega di vedere le informazioni su pev3 **[fornito lì](/help/sites-administering/adobeanalytics.md)**.*

**Riferimenti utilizzati in questa esercitazione:**

[0] [https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html](https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html)
