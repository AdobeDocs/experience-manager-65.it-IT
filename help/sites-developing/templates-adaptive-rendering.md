---
title: Rendering modello adattivo
description: Scopri il rendering di modelli adattivi in Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 58cac3b1-b7cd-44b2-b89b-f5ee8811c198
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 2%

---

# Rendering modello adattivo{#adaptive-template-rendering}

Il rendering di modelli adattivi consente di gestire una pagina con varianti. Originariamente utile per fornire varie uscite HTML per dispositivi mobili (ad esempio, telefono cellulare rispetto a smartphone), questa funzione è utile quando le esperienze devono essere consegnate a vari dispositivi che richiedono markup o output HTML diversi.

## Panoramica {#overview}

I modelli sono basati su una griglia reattiva e le pagine create in base a tali modelli sono completamente reattive, adattandosi automaticamente al riquadro di visualizzazione del dispositivo client. Utilizzando la barra degli strumenti Emulatore nell’editor di pagine, gli autori possono indirizzare i layout a dispositivi specifici.

È inoltre possibile impostare modelli per supportare il rendering adattivo. Quando i gruppi di dispositivi sono configurati correttamente, la pagina viene sottoposta a rendering con un selettore diverso nell’URL quando si seleziona un dispositivo in modalità emulatore. Utilizzando un selettore, è possibile chiamare direttamente un rendering di pagina specifico tramite l’URL.

Ricorda quando configuri i gruppi di dispositivi:

* Ogni dispositivo deve appartenere ad almeno un gruppo di dispositivi.
* Un dispositivo può trovarsi in più gruppi di dispositivi.
* Poiché i dispositivi possono trovarsi in più gruppi di dispositivi, i selettori possono essere combinati.
* La combinazione di selettori viene valutata dall’alto al basso in quanto vengono mantenuti nell’archivio.

>[!NOTE]
>
>Il gruppo di dispositivi **i dispositivi reattivi non dispongono mai di un selettore, in quanto si presume che i dispositivi riconosciuti come in grado di supportare la progettazione reattiva non necessitino di un layout adattivo

## Configurazione {#configuration}

I selettori di rendering adattivo possono essere configurati per gruppi di dispositivi esistenti o per [gruppi creati personalmente.](/help/sites-developing/mobile.md#device-groups)

In questo esempio, stai per configurare il gruppo di dispositivi esistente **Smart Phone** in modo che abbia un selettore di rendering adattivo come parte del modello **Pagina esperienza** in We.Retail.

1. Modifica il gruppo di dispositivi che richiede un selettore adattivo in `http://localhost:4502/miscadmin#/etc/mobile/groups`

   Imposta l&#39;opzione **Disabilita emulatore** e salva.

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. Il selettore è disponibile per **BlackBerry®** e **iPhone 4** a condizione che il gruppo di dispositivi **Smart Phone** sia aggiunto alle strutture di modello e pagina nei passaggi seguenti.

   ![chlimage_1-158](assets/chlimage_1-158.png)

1. Con CRXDE Lite, consenti l&#39;utilizzo del gruppo di dispositivi nel modello aggiungendolo alla proprietà di stringa con più valori `cq:deviceGroups` nella struttura del modello.

   `/conf/<your-site>/settings/wcm/templates/<your-template>/structure/jcr:content`

   Ad esempio, se desideri aggiungere il gruppo di dispositivi Smart Phone:

   `/conf/we-retail/settings/wcm/templates/experience-page/structure/jcr:content`

   ![chlimage_1-159](assets/chlimage_1-159.png)

1. Con CRXDE Lite, consenti l&#39;utilizzo del gruppo di dispositivi sul tuo sito aggiungendolo alla proprietà di stringa con più valori `cq:deviceGroups` nella struttura del sito.

   `/content/<your-site>/jcr:content`

   Ad esempio, se desideri consentire il gruppo di dispositivi **Smart Phone**:

   `/content/we-retail/jcr:content`

   ![chlimage_1-160](assets/chlimage_1-160.png)

Ora quando utilizzi l&#39;[emulatore](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints) nell&#39;editor pagina (ad esempio quando [modifichi il layout](/help/sites-authoring/responsive-layout.md)) e scegli un dispositivo del gruppo di dispositivi configurato, la pagina viene riprodotta con un selettore come parte dell&#39;URL.

In questo esempio, quando si modifica una pagina basata sul modello **Pagina esperienza** e si sceglie iPhone 4 nell&#39;emulatore, viene eseguito il rendering della pagina includendo il selettore come `arctic-surfing-in-lofoten.smart.html` invece di `arctic-surfing-in-lofoten.html`

La pagina può anche essere chiamata direttamente utilizzando questo selettore.

![chlimage_1-161](assets/chlimage_1-161.png)
