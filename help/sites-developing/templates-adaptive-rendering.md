---
title: Rendering modello adattivo
seo-title: Adaptive Template Rendering
description: Rendering modello adattivo
seo-description: null
uuid: 97226ae1-e42a-40ae-a5e0-886cd77559d8
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f5cb0e98-0d6e-4f14-9b94-df1a9d8cbe5b
exl-id: 58cac3b1-b7cd-44b2-b89b-f5ee8811c198
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 1%

---

# Rendering modello adattivo{#adaptive-template-rendering}

Il rendering di modelli adattivi consente di gestire una pagina con varianti. Originariamente utile per fornire vari output HTML per dispositivi mobili (ad esempio, telefono cellulare o smartphone), questa funzione è utile quando le esperienze devono essere consegnate a vari dispositivi che richiedono un output markup o HTML diverso.

## Panoramica {#overview}

I modelli sono generalmente basati su una griglia reattiva e le pagine create in base a questi modelli sono completamente reattive, adattandosi automaticamente al riquadro di visualizzazione del dispositivo client. Utilizzando la barra degli strumenti Emulatore nell’editor di pagine, gli autori possono indirizzare i layout a dispositivi specifici.

È inoltre possibile impostare modelli per supportare il rendering adattivo. Quando i gruppi di dispositivi sono configurati correttamente, la pagina viene riprodotta con un selettore diverso nell’URL quando si seleziona un dispositivo in modalità emulatore. Utilizzando un selettore, è possibile chiamare direttamente un rendering di pagina specifico tramite l’URL.

Ricorda quando configuri i gruppi di dispositivi:

* Ogni dispositivo deve appartenere ad almeno un gruppo di dispositivi.
* Un dispositivo può trovarsi in più gruppi di dispositivi.
* Poiché i dispositivi possono trovarsi in più gruppi di dispositivi, i selettori possono essere combinati.
* La combinazione di selettori viene valutata dall’alto al basso in quanto vengono mantenuti nell’archivio.

>[!NOTE]
>
>Il gruppo di dispositivi **Dispositivi reattivi** non avrà mai un selettore, perché si presume che i dispositivi riconosciuti come dispositivi di supporto per il design reattivo non richiedano un layout adattivo

## Configurazione {#configuration}

I selettori di rendering adattivo possono essere configurati per gruppi di dispositivi esistenti o per [gruppi creati personalmente.](/help/sites-developing/mobile.md#device-groups)

Per questo esempio, configureremo il gruppo di dispositivi esistente **Smartphone** per avere un selettore di rendering adattivo come parte del **Pagina esperienza** modello in We.Retail.

1. Modificare il gruppo di dispositivi che richiede un selettore adattivo in `http://localhost:4502/miscadmin#/etc/mobile/groups`

   Imposta l’opzione **Disabilita emulatore** e salva.

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. Il selettore sarà disponibile per **Blackberry** e **IPHONE 4** ha fornito il gruppo di dispositivi **Smart Phone** viene aggiunto alle strutture di modello e pagina nei passaggi seguenti.

   ![chlimage_1-158](assets/chlimage_1-158.png)

1. Utilizzando CRX DE Lite, consenti l’utilizzo del gruppo di dispositivi sul modello aggiungendolo alla proprietà della stringa con più valori. `cq:deviceGroups` nella struttura del modello.

   `/conf/<your-site>/settings/wcm/templates/<your-template>/structure/jcr:content`

   Ad esempio, se desideri aggiungere il gruppo di dispositivi Smart Phone:

   `/conf/we-retail/settings/wcm/templates/experience-page/structure/jcr:content`

   ![chlimage_1-159](assets/chlimage_1-159.png)

1. Utilizzando CRX DE Lite, consenti l’utilizzo del gruppo di dispositivi sul tuo sito aggiungendolo alla proprietà della stringa con più valori `cq:deviceGroups` sulla struttura del sito.

   `/content/<your-site>/jcr:content`

   Ad esempio, se desideri consentire **Smart Phone** gruppo di dispositivi:

   `/content/we-retail/jcr:content`

   ![chlimage_1-160](assets/chlimage_1-160.png)

Ora quando si utilizza [emulatore](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints) nell’editor pagina (ad esempio quando [modifica del layout](/help/sites-authoring/responsive-layout.md)) e scegli un dispositivo del gruppo di dispositivi configurato, la pagina verrà sottoposta a rendering con un selettore come parte dell&#39;URL.

Nel nostro esempio, quando modifichi una pagina basata su **Pagina esperienza** e selezionando iPhone 4 nell’emulatore, viene eseguito il rendering della pagina, incluso il selettore come `arctic-surfing-in-lofoten.smart.html` invece di `arctic-surfing-in-lofoten.html`

La pagina può anche essere chiamata direttamente utilizzando questo selettore.

![chlimage_1-161](assets/chlimage_1-161.png)
