---
title: Utilizzo di Smart Imaging con proporzioni pixel del dispositivo lato client
description: Scopri come utilizzare le proporzioni pixel del dispositivo lato client con Smart Imaging in Adobe Experience Manager as a Cloud Service con Dynamic Media.
role: Admin,User
exl-id: e38f522a-242a-4ea9-a866-d8d129950831
solution: Experience Manager, Experience Manager Assets
feature: Smart Imaging
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: bd0d2470-932c-4269-8eca-6d939b72d9ef
    internal-label: Dynamic Media
subfeature_v2:
  - id: b39a6d56-d787-413f-8024-351803c28d44
    internal-label: Smart Imaging
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%
---
# Informazioni sulla tecnologia Smart Imaging con rapporto pixel del dispositivo lato client (DPR) {#client-side-dpr}

La soluzione di Smart Imaging corrente utilizza stringhe dell’agente utente per determinare il tipo di dispositivo (desktop, tablet, dispositivi mobili e così via) utilizzato.

Le funzionalità di rilevamento dei dispositivi (DPR basato sulle stringhe dell’agente utente) sono spesso imprecise, soprattutto per i dispositivi Apple. Inoltre, ogni volta che viene avviato un nuovo dispositivo, questo deve essere convalidato.

Il DPR lato client fornisce valori accurati al 100% e funziona per qualsiasi dispositivo, sia esso Apple o qualsiasi altro nuovo dispositivo avviato.

## Utilizzare il codice DPR lato client

**App sottoposte a rendering lato server**

1. Caricare il processo di lavoro del servizio iniziando (`srvinit.js`) includendo lo script seguente nella sezione dell&#39;intestazione della pagina HTML:

   ```javascript
   <script type="text/javascript" src="srvinit.js"></script>
   ```

   Adobe consiglia di caricare lo script _prima_ di qualsiasi altro script in modo che il service worker inizi immediatamente l&#39;inizializzazione.

1. Includi il seguente codice tag immagine DPR nella parte superiore della sezione body della pagina HTML:

   ```html
   <img src="aem_dm_dpr_1x.jpg" style="width:1px;height:1px;display:none"
       srcset="aem_dm_dpr_1x.jpg 1x, aem_dm_dpr_1.1x.jpg 1.1x, aem_dm_dpr_1.2x.jpg 1.2x, aem_dm_dpr_1.3x.jpg 1.3x, aem_dm_dpr_1.4x.jpg 1.4x, aem_dm_dpr_1.5x.jpg 1.5x, aem_dm_dpr_1.6x.jpg 1.6x,          aem_dm_dpr_1.7x.jpg 1.7x, aem_dm_dpr_1.8x.jpg 1.8x, aem_dm_dpr_1.9x.jpg 1.9x,
       aem_dm_dpr_2x.jpg 2x, aem_dm_dpr_2.1x.jpg 2.1x, aem_dm_dpr_2.2x.jpg 2.2x, aem_dm_dpr_2.3x.jpg 2.3x, aem_dm_dpr_2.4x.jpg 2.4x, aem_dm_dpr_2.5x.jpg 2.5x, aem_dm_dpr_2.6x.jpg 2.6x, aem_dm_dpr_2.7x.jpg 2.7x, aem_dm_dpr_2.8x.jpg 2.8x, aem_dm_dpr_2.9x.jpg 2.9x,
       aem_dm_dpr_3x.jpg 3x, aem_dm_dpr_3.1x.jpg 3.1x, aem_dm_dpr_3.2x.jpg 3.2x, aem_dm_dpr_3.3x.jpg 3.3x, aem_dm_dpr_3.4x.jpg 3.4x, aem_dm_dpr_3.5x.jpg 3.5x, aem_dm_dpr_3.6x.jpg 3.6x, aem_dm_dpr_3.7x.jpg 3.7x, aem_dm_dpr_3.8x.jpg 3.8x, aem_dm_dpr_3.9x.jpg 3.9x,
       aem_dm_dpr_4x.jpg 4x, aem_dm_dpr_4.1x.jpg 4.1x, aem_dm_dpr_4.2x.jpg 4.2x, aem_dm_dpr_4.3x.jpg 4.3x, aem_dm_dpr_4.4x.jpg 4.4x, aem_dm_dpr_4.5x.jpg 4.5x, aem_dm_dpr_4.6x.jpg 4.6x, aem_dm_dpr_4.7x.jpg 4.7x, aem_dm_dpr_4.8x.jpg 4.8x, aem_dm_dpr_4.9x.jpg 4.9x,
       aem_dm_dpr_5x.jpg 5x">
   ```

   È necessario includere il codice tag immagine DPR _prima_ di tutte le immagini statiche nella pagina HTML.

**App sottoposte a rendering lato client**

1. Includi i seguenti script DPR nella sezione di intestazione della pagina HTML:

   ```javascript
   <script type="text/javascript" src="srvinit.js"></script>
   <script type="text/javascript" src="dprImageInjection.js"></script>
   ```

   È possibile combinare entrambi gli script DPR in uno per evitare più richieste di rete.

   Adobe consiglia di caricare questi script _prima_ di qualsiasi altro script nella pagina HTML.
   Adobe consiglia inoltre di usare l’app per Bootstrap con il tag HTML diff anziché con un elemento body. Il motivo è che `dprImageInjection.js` inserisce dinamicamente il tag immagine nella parte superiore della sezione body nella pagina HTML.

## Download di file JavaScript {#client-side-dpr-script}

I seguenti file JavaScript nel download sono forniti solo come riferimento di esempio. Se intendi utilizzare questi file nelle pagine di HTML, assicurati di modificare il codice di ciascun file in base alle tue esigenze.

* `dprImageInjection.js`
* `srvinit.js`
* `srvwrk.js`

[Download di file JavaScript](/help/assets/assets-dm/aem-dynamicmedia-smartimaging-dpr.zip)

>[!MORELIKETHIS]
>
>* [Imaging avanzato](/help/assets/imaging-faq.md)
