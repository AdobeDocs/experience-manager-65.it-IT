---
title: Applicazione di firme elettroniche a un modulo utilizzando firme a script (obsolete)
seo-title: Applicazione di firme elettroniche a un modulo utilizzando firme a script (obsolete)
description: Firma di moduli tramite script
seo-description: Firma di moduli tramite script
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 76d178d1-8e40-41b3-80d4-66b2f8d04211
docset: aem65
translation-type: tm+mt
source-git-commit: 92a64c8a1ba38f592d18355b8233cb79a2575301

---


# Applicazione di firme elettroniche a un modulo utilizzando firme a script (obsolete){#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

È possibile utilizzare il componente **Firma** scarabocchio (obsoleto) e il componente Passaggio **** firma per disegnare (scarabocchio) una firma su un modulo adattivo. Il componente Fase firma visualizza una versione PDF del modulo adattivo. Per utilizzare il componente Fase firma è necessario abilitare l&#39;opzione Documento di registrazione o i moduli adattivi basati su modelli di modulo.

Entrambi i componenti dispongono di una finestra, visualizzata di seguito, per firmare un modulo. È inoltre possibile fare clic sull&#39;icona di geolocalizzazione ![aem_6_3_geolocalizzazione](assets/aem_6_3_geolocation.png) per aggiungere una geolocalizzazione alla firma.

![Finestra di dialogo Firma scarabocchio](assets/scribble-signature.png)

## Configurare un modulo adattivo per l&#39;utilizzo della firma scarabocchio {#configure-an-adaptive-form-to-use-scribble-signature}

1. Crea un modulo adattivo basato su modello o abilitato per l&#39;opzione Documento di registrazione. Per informazioni dettagliate, vedere [Creazione di un modulo](../../forms/using/creating-adaptive-form.md)adattivo.
1. Trascinare il componente **Firma** scarabocchio dal browser Componenti al modulo adattivo.
1. Toccate l&#39;icona **Configura** ![configurazione](assets/configure.png) . Apre il browser delle proprietà e visualizza le proprietà del componente Firma scarabocchio. Configurare le proprietà del componente Firma scarabocchio.
1. Trascinare il componente Passaggio firma dal browser Componenti al modulo adattivo.

   >[!NOTE]
   >
   >Il componente Passaggio firma occupa la larghezza totale disponibile per il modulo. Si consiglia di non avere altri componenti nella sezione contenente il componente Passaggio firma.

1. Nel browser Contenuto, toccate Contenitore **** modulo e toccate l&#39;icona **Configura** ![](/help/forms/using/assets/configure.png) . Apre il browser delle proprietà e visualizza le proprietà del contenitore Modulo adattivo. Passare a Contenitore **modulo** adattivo > Firma **** elettronica e deselezionare l&#39;opzione **Abilita Adobe Sign** . Toccate l&#39;icona Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) per salvare le modifiche.

   >[!NOTE]
   >
   >Quando si aggiunge un componente Passaggio firma a un modulo adattivo, l&#39;opzione Abilita Adobe Sign viene selezionata automaticamente.

1. Toccate l&#39;icona **Configura** ![configurazione](assets/configure.png) . Apre il browser delle proprietà e visualizza le proprietà dei passaggi firma. Configurare le seguenti proprietà:

   * **Nome** elemento: Specificate il nome del componente.

   * **** Titolo: Specificate un titolo univoco del componente.
   * **** Messaggio modello: Specificare il messaggio da visualizzare durante il caricamento del PDF della firma. I servizi Adobe Sign richiedono del tempo per preparare e caricare il PDF della firma.
   * **** Servizio di firma: Selezionare l&#39;opzione **Firma** scarabocchio.

   * **Classe** CSS: Specificate la classe CSS della libreria client, se presente. Si consiglia di utilizzare [temi](../../forms/using/themes.md) e stili [](../../forms/using/inline-style-adaptive-forms.md) in linea al posto di CSS Class.
   Toccate l&#39;icona Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) per salvare le modifiche. La firma è configurata correttamente.

   Ora, quando si compila un modulo, viene visualizzata una versione PDF del modulo adattivo e sono disponibili opzioni per firmare il documento PDF. Per informazioni dettagliate, vedere [Firmare un modulo adattivo utilizzando la firma](../../forms/using/signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature)scarabocchio.

## Firmare un modulo adattivo utilizzando la firma scarabocchio {#sign-an-adaptive-form-using-scribble-signature}

1. Dopo aver compilato un modulo adattivo e aver raggiunto la pagina Passaggio firma, viene visualizzata la schermata della firma.

   ![Schermata di firma per la pagina EchoSign](assets/esignscribblesign.jpg)

1. Fare clic su **[!UICONTROL Firma]**. Viene visualizzata la finestra di dialogo del segno di script. Firmare il modulo e fare clic sull&#39;icona Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) per salvare la firma.

   ![Finestra di dialogo Firma scarabocchio](assets/scribblewidget.jpg)

1. Fare clic su Completa per completare il processo di firma.

   ![Completare il processo di firma](assets/scribblecomplete.jpg)

Le firme vengono aggiunte al modulo e il controllo del modulo passa al pannello successivo.

