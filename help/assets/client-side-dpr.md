---
title: Utilizzare l’imaging intelligente con il rapporto pixel del dispositivo lato client
description: Scopri come utilizzare il rapporto pixel del dispositivo lato client con Smart imaging in Adobe Experience Manager as a Cloud Service con Dynamic Media.
role: Admin,User
exl-id: e38f522a-242a-4ea9-a866-d8d129950831
source-git-commit: c8682118f15132063073df5cdc2b576b6e62a0c8
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# Informazioni sull’imaging intelligente con rapporto pixel del dispositivo lato client (DPR) {#client-side-dpr}

La soluzione di imaging avanzato corrente utilizza le stringhe dell&#39;agente utente per determinare il tipo di dispositivo (desktop, tablet, dispositivi mobili e così via) utilizzato.

Le funzionalità di rilevamento dei dispositivi (DPR basato su stringhe dell’agente utente) sono spesso imprecise, soprattutto per i dispositivi Apple. Inoltre, ogni volta che un nuovo dispositivo viene avviato, deve essere convalidato.

Il DPR lato client fornisce valori precisi al 100% e funziona per qualsiasi dispositivo, sia che si tratti di Apple o di qualsiasi altro nuovo dispositivo avviato.

## Usa il codice DPR lato client

**App rappresentate lato server**

1. Carica iniziale lavoratore del servizio (`srvinit.js`) includendo il seguente script nella sezione intestazione della pagina HTML:

   ```javascript
   <script type="text/javascript" src="srvinit.js"></script>
   ```

   Adobe consiglia di caricare questo script _prima_ qualsiasi altro script in modo che il service worker inizi immediatamente l&#39;inizializzazione.

1. Includi il seguente codice tag immagine DPR nella parte superiore della sezione corpo della pagina HTML:

   ```html
   <img src="aem_dm_dpr_1x.jpg" style="width:1px;height:1px;display:none"
       srcset="aem_dm_dpr_1x.jpg 1x, aem_dm_dpr_1.1x.jpg 1.1x, aem_dm_dpr_1.2x.jpg 1.2x, aem_dm_dpr_1.3x.jpg 1.3x, aem_dm_dpr_1.4x.jpg 1.4x, aem_dm_dpr_1.5x.jpg 1.5x, aem_dm_dpr_1.6x.jpg 1.6x,          aem_dm_dpr_1.7x.jpg 1.7x, aem_dm_dpr_1.8x.jpg 1.8x, aem_dm_dpr_1.9x.jpg 1.9x,
       aem_dm_dpr_2x.jpg 2x, aem_dm_dpr_2.1x.jpg 2.1x, aem_dm_dpr_2.2x.jpg 2.2x, aem_dm_dpr_2.3x.jpg 2.3x, aem_dm_dpr_2.4x.jpg 2.4x, aem_dm_dpr_2.5x.jpg 2.5x, aem_dm_dpr_2.6x.jpg 2.6x, aem_dm_dpr_2.7x.jpg 2.7x, aem_dm_dpr_2.8x.jpg 2.8x, aem_dm_dpr_2.9x.jpg 2.9x,
       aem_dm_dpr_3x.jpg 3x, aem_dm_dpr_3.1x.jpg 3.1x, aem_dm_dpr_3.2x.jpg 3.2x, aem_dm_dpr_3.3x.jpg 3.3x, aem_dm_dpr_3.4x.jpg 3.4x, aem_dm_dpr_3.5x.jpg 3.5x, aem_dm_dpr_3.6x.jpg 3.6x, aem_dm_dpr_3.7x.jpg 3.7x, aem_dm_dpr_3.8x.jpg 3.8x, aem_dm_dpr_3.9x.jpg 3.9x,
       aem_dm_dpr_4x.jpg 4x, aem_dm_dpr_4.1x.jpg 4.1x, aem_dm_dpr_4.2x.jpg 4.2x, aem_dm_dpr_4.3x.jpg 4.3x, aem_dm_dpr_4.4x.jpg 4.4x, aem_dm_dpr_4.5x.jpg 4.5x, aem_dm_dpr_4.6x.jpg 4.6x, aem_dm_dpr_4.7x.jpg 4.7x, aem_dm_dpr_4.8x.jpg 4.8x, aem_dm_dpr_4.9x.jpg 4.9x,
       aem_dm_dpr_5x.jpg 5x">
   ```

   È obbligatorio includere questo codice di tag immagine DPR _prima_ tutte le immagini statiche presenti nella pagina HTML.

**App sottoposte a rendering lato client**

1. Includi i seguenti script DPR nella sezione di intestazione della pagina HTML:

   ```javascript
   <script type="text/javascript" src="srvinit.js"></script>
   <script type="text/javascript" src="dprImageInjection.js"></script>
   ```

   È possibile combinare entrambi gli script DPR in uno per evitare più richieste di rete.

   Adobe consiglia di caricare questi script _prima_ qualsiasi altro script nella pagina HTML.
Adobe consiglia inoltre di Bootstrap l’app sotto il tag HTML diff anziché un elemento body. Il motivo è che `dprImageInjection.js` inserisce dinamicamente il tag immagine nella parte superiore della sezione corpo della pagina HTML.

## Download di file JavaScript {#client-side-dpr-script}

I seguenti file JavaScript nel download vengono forniti solo come riferimento di esempio. Se si desidera utilizzare questi file nelle pagine di HTML, assicurarsi di modificare il codice di ciascun file in base alle proprie esigenze.

* `dprImageInjection.js`
* `srvinit.js`
* `srvwrk.js`

[Download di file JavaScript](/help/assets/assets-dm/aem-dynamicmedia-smartimaging-dpr.zip)

>[!MORELIKETHIS]
>
>* [Imaging avanzato](/help/assets/imaging-faq.md)

