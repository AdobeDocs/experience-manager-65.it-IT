---
title: Rendering di modelli adattivi
seo-title: Adaptive Template Rendering
description: Rendering di modelli adattivi
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

# Rendering di modelli adattivi{#adaptive-template-rendering}

Il rendering del modello adattivo fornisce un modo per gestire una pagina con varianti. Originariamente utile per fornire diversi output di HTML per dispositivi mobili (ad esempio, telefono cellulare con funzioni o smartphone), questa funzione è utile quando le esperienze devono essere distribuite a vari dispositivi che necessitano di markup o output di HTML diversi.

## Panoramica {#overview}

I modelli sono generalmente costruiti intorno a una griglia reattiva e le pagine create in base a questi modelli sono completamente reattive, adattandosi automaticamente al riquadro di visualizzazione del dispositivo client. Tramite la barra degli strumenti Emulatore nell’editor di pagine, gli autori possono eseguire il targeting dei layout per dispositivi specifici.

È inoltre possibile impostare modelli per supportare il rendering adattivo. Quando i gruppi di dispositivi sono configurati correttamente, alla pagina verrà eseguito il rendering con un selettore diverso nell’URL quando si seleziona un dispositivo in modalità emulatore. L’utilizzo di un selettore consente di richiamare direttamente un rendering della pagina tramite l’URL.

Ricorda quando configuri gruppi di dispositivi:

* Ogni dispositivo deve trovarsi in almeno un gruppo di dispositivi.
* Un dispositivo può trovarsi in più gruppi di dispositivi.
* Poiché i dispositivi possono trovarsi in più gruppi di dispositivi, i selettori possono essere combinati.
* La combinazione di selettori viene valutata dall’alto verso il basso in quanto persistono nell’archivio.

>[!NOTE]
>
>Gruppo di dispositivi **Dispositivi reattivi** non avrà mai un selettore perché i dispositivi riconosciuti come dispositivi che supportano la progettazione reattiva non necessitano di un layout adattivo

## Configurazione {#configuration}

I selettori di rendering adattivi possono essere configurati per gruppi di dispositivi esistenti o per [gruppi creati da te.](/help/sites-developing/mobile.md#device-groups)

Per questo esempio, configureremo il gruppo di dispositivi esistente **Telefoni intelligenti** per disporre di un selettore di rendering adattivo come parte del **Pagina Esperienza** all’interno di We.Retail.

1. Modifica il gruppo di dispositivi che richiede un selettore adattivo in `http://localhost:4502/miscadmin#/etc/mobile/groups`

   Imposta l’opzione **Disattiva emulatore** e salva.

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. Il selettore sarà disponibile per il **Blackberry** e **iPhone 4** forniva il gruppo di dispositivi **Telefono avanzato** viene aggiunto al modello e alle strutture di pagina nei passaggi seguenti.

   ![chlimage_1-158](assets/chlimage_1-158.png)

1. Utilizzando CRX DE Lite, consenti al gruppo di dispositivi di essere utilizzato sul modello aggiungendolo alla proprietà della stringa con più valori `cq:deviceGroups` nella struttura del modello.

   `/conf/<your-site>/settings/wcm/templates/<your-template>/structure/jcr:content`

   Ad esempio, per aggiungere il gruppo di dispositivi Smart Phone:

   `/conf/we-retail/settings/wcm/templates/experience-page/structure/jcr:content`

   ![chlimage_1-159](assets/chlimage_1-159.png)

1. Utilizzando CRX DE Lite, consenti al gruppo di dispositivi di essere utilizzato sul tuo sito aggiungendolo alla proprietà della stringa con più valori `cq:deviceGroups` nella struttura del sito.

   `/content/<your-site>/jcr:content`

   Ad esempio, se desideri consentire la **Telefono avanzato** gruppo di dispositivi:

   `/content/we-retail/jcr:content`

   ![chlimage_1-160](assets/chlimage_1-160.png)

Ora quando si utilizza il [emulatore](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints) nell’editor pagina (ad esempio quando [modifica del layout](/help/sites-authoring/responsive-layout.md)) e scegli un dispositivo del gruppo di dispositivi configurato, la pagina verrà riprodotta con un selettore come parte dell’URL.

Nel nostro esempio, quando modifichi una pagina basata sui **Pagina Esperienza** e scegliendo iPhone 4 nell’emulatore, la pagina viene sottoposta a rendering includendo il selettore come `arctic-surfing-in-lofoten.smart.html` anziché `arctic-surfing-in-lofoten.html`

La pagina può anche essere chiamata direttamente utilizzando questo selettore.

![chlimage_1-161](assets/chlimage_1-161.png)
