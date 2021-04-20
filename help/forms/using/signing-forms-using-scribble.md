---
title: Applicazione di firme elettroniche a un modulo utilizzando firme a mano libera
seo-title: Applicazione di firme elettroniche a un modulo utilizzando firme a mano libera
description: Firma dei moduli tramite scarabocchio
seo-description: Firma dei moduli tramite scarabocchio
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 76d178d1-8e40-41b3-80d4-66b2f8d04211
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---


# Applicare le firme elettroniche a un modulo utilizzando le firme a mano libera{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

È possibile utilizzare il componente **Firma digitale** e il componente **Passaggio firma** per disegnare la firma su un modulo adattivo. Il componente Passaggio firma visualizza una versione PDF del modulo adattivo. Per utilizzare il componente Passaggio firma è necessaria l’opzione Documento di record abilitata o i moduli adattivi basati su modelli di modulo.

Entrambi i componenti dispongono di una finestra, come illustrato di seguito, per firmare un modulo. È inoltre possibile fare clic sull&#39;icona di geolocalizzazione ![aem_6_3_geolocation](assets/aem_6_3_geolocation.png) per aggiungere la geolocalizzazione alla firma.

![Finestra di dialogo dei segni di scorrimento](assets/scribble-signature.png)

## Configurare un modulo adattivo per l’utilizzo della firma digitale {#configure-an-adaptive-form-to-use-scribble-signature}

1. Crea un modulo adattivo basato su modello di modulo abilitato per l’opzione Documento di record. Per informazioni dettagliate, consulta [Creazione di un modulo adattivo](../../forms/using/creating-adaptive-form.md).
1. Trascina il componente **Firma digitale** dal browser Componenti al modulo adattivo.
1. Tocca l’icona **Configura** ![configura](assets/configure.png) . Apre il browser delle proprietà e visualizza le proprietà del componente Firma digitale. Configura le proprietà del componente Firma digitale.
1. Trascina il componente Passaggio firma dal browser Componenti al modulo adattivo.

   >[!NOTE]
   >
   >Il componente Passaggio firma occupa la larghezza completa disponibile per il modulo. Si consiglia di non avere alcun altro componente nella sezione contenente il componente Passaggio firma.

1. Nel browser Contenuto, tocca **Contenitore modulo** e tocca l&#39;icona **Configura** ![](/help/forms/using/assets/configure.png) . Apre il browser delle proprietà e visualizza le proprietà del contenitore Modulo adattivo. Passa a **Contenitore di moduli adattivi** > **Firma elettronica** e deseleziona l&#39;opzione **Abilita Adobe Sign**. Tocca l’icona Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) per salvare le modifiche.

   >[!NOTE]
   >
   >Quando si aggiunge un componente Passaggio firma a un modulo adattivo, l’opzione Abilita Adobe Sign viene selezionata automaticamente.

1. Tocca l’icona **Configura** ![configura](assets/configure.png) . Apre il browser delle proprietà e visualizza le proprietà del passaggio Firma. Configura le seguenti proprietà:

   * **Nome** elemento: Specifica il nome del componente.

   * **Titolo:** specifica un titolo univoco del componente.
   * **Messaggio modello:** specifica il messaggio da visualizzare durante il caricamento del PDF della firma. I servizi Adobe Sign richiedono del tempo per preparare e caricare il PDF della firma.
   * **Servizio di firma:** selezionare l’opzione  **Firma** scarabocchio.

   * **Classe** CSS: Specifica la classe CSS della libreria client, se presente. Si consiglia di utilizzare [temi](../../forms/using/themes.md) e [stili in linea](../../forms/using/inline-style-adaptive-forms.md) invece di Classe CSS.

   Tocca l’icona Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) per salvare le modifiche. La firma è configurata correttamente.

   Ora, quando si compila un modulo, viene visualizzata una versione PDF del modulo adattivo e vengono fornite le opzioni per firmare il documento PDF. Per informazioni dettagliate, consultare [Firma di un modulo adattivo utilizzando Scribble Signature](../../forms/using/signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature).

## Firma di un modulo adattivo utilizzando la firma digitale {#sign-an-adaptive-form-using-scribble-signature}

1. Dopo aver compilato un modulo adattivo e aver raggiunto la pagina Passaggio firma, viene visualizzata la schermata della firma.

   ![Schermata della firma per la pagina EchoSign](assets/esignscribblesign.jpg)

1. Fare clic su **[!UICONTROL Firma]**. Viene visualizzata la finestra di dialogo del segno di scarabocchio. Firma il modulo e fai clic sull’icona Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) per salvare la firma.

   ![Finestra di dialogo dei segni di scorrimento](assets/scribblewidget.jpg)

1. Fare clic su completa per completare il processo di firma.

   ![Completare il processo di firma](assets/scribblecomplete.jpg)

Le firme vengono aggiunte al modulo e il controllo modulo si sposta nel pannello successivo.

