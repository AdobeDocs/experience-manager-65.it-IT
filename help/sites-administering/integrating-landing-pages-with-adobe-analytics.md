---
title: Integrazione delle pagine di destinazione con Adobe Analytics
seo-title: Integrating Landing Pages with Adobe Analytics
description: Scopri come integrare le pagine di destinazione con Adobe Analytics.
seo-description: Learn how to integrate landing pages with Adobe Analytics.
uuid: 8f6672d1-497f-4ccb-b3cc-f6120fc467ba
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 8ae7ccec-489b-4d20-ac56-6101402fb18a
exl-id: da3f7b7e-87e5-446a-9a77-4b12b850a381
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 21%

---

# Integrazione delle pagine di destinazione con Adobe Analytics{#integrating-landing-pages-with-adobe-analytics}

AEM ha integrato la soluzione delle pagine di destinazione con [Adobe Analytics](https://www.omniture.com/en/products/analytics/sitecatalyst) utilizzando i seguenti componenti invito all’azione (CTA, Call-to-action):

1. Componente Collegamento ClickThrough
1. Componente Collegamento grafico

Questi componenti espongono alcuni attributi che possono essere mappati tramite variabili di Adobe Analytics (Traffico, variabili di conversione) ed eventi di successo per inviare informazioni ad Adobe Analytics.

## Prerequisiti {#prerequisites}

L’Adobe consiglia di passare attraverso [integrazione esistente AEM-Adobe Analytics](/help/sites-administering/adobeanalytics.md) per comprendere come funziona questa integrazione.

## Componenti disponibili per la mappatura {#components-available-for-mapping}

In AEM, il **Invito all&#39;azione** componenti - **ClickThroughLink** e **Collegamento grafico** - qui nella barra laterale, può essere mappato su variabili Adobe Analytics.

![chlimage_1-21](assets/chlimage_1-21a.jpeg)

### Mappatura dei componenti di una pagina di destinazione su Adobe Analytics {#mapping-landing-page-components-to-adobe-analytics}

Per mappare i componenti della pagina di destinazione su Adobe Analytics:

1. Dopo aver creato la configurazione di Adobe Analytics e un nuovo framework, seleziona la suite di rapporti appropriata dal menu a discesa. In questo modo le variabili Adobe Analytics vengono recuperate e visualizzate in Content Finder.
1. Trascinate i componenti Invito all’azione (CTA) dalla barra laterale all’area di mappatura al centro della pagina.

<table>
 <tbody>
  <tr>
   <td><strong>Nome componente</strong></td>
   <td><strong>Attributi disponibili</strong></td>
   <td><strong>Significato dell’attributo</strong></td>
  </tr>
  <tr>
   <td><strong>Collegamento ClickThrough CTA</strong></td>
   <td><i>eventdata.clickthroughLinkLabel</i> <br /> </td>
   <td>Etichetta o testo del collegamento </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickthroughLinkTarget</i> <br /> </td>
   <td>Destinazione a cui si passa quando si fa clic sul collegamento </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clickthroughLinkClick</i> <br /> </td>
   <td>Evento clic </td>
  </tr>
  <tr>
   <td><strong>Collegamento grafico CTA</strong></td>
   <td><i>eventdata.clickthroughImageLabel</i> <br /> </td>
   <td>Titolo dell’immagine CTA </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickthroughImageTarget</i> <br /> </td>
   <td>Destinazione a cui si passa quando si fa clic sull’immagine del collegamento</td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.clickthroughImageAsset</i> <br /> </td>
   <td>Percorso della risorsa immagine nell’archivio </td>
  </tr>
  <tr>
   <td><br type="_moz" /> </td>
   <td><i>eventdata.events.clickthroughImageClick</i> <br /> </td>
   <td>Evento clic</td>
  </tr>
 </tbody>
</table>

1. Mappa questi attributi esposti con qualsiasi variabile Adobe Analytics da Content Finder. Il framework è ora pronto per essere utilizzato.
1. Ora puoi creare una nuova pagina di destinazione o aprirne una esistente con i componenti CTA esistenti, quindi fai clic su **Cloud Services** scheda in **Proprietà pagina** dalla barra laterale (nell’interfaccia touch, seleziona **Apri proprietà** e fai clic su **Cloud Services**) e configura il framework da utilizzare con la pagina di destinazione. Selezionate il framework dall’elenco a comparsa.

   ![chlimage_1-25](assets/chlimage_1-25a.png)

1. Dopo aver configurato il framework con la pagina di destinazione, ora puoi utilizzare i componenti strumentati e tutti i clic su CTA vengono registrati in Adobe Analytics.
