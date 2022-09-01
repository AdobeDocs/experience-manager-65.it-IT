---
title: Applicazione di firme elettroniche a un modulo utilizzando firme a mano libera
seo-title: Apply electronic signatures to a form using scribble signatures
description: Firma dei moduli tramite scarabocchio
seo-description: Signing forms using scribble
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 76d178d1-8e40-41b3-80d4-66b2f8d04211
docset: aem65
feature: Adaptive Forms
exl-id: 096f61b0-59f4-4699-9093-8fb1ed81fded
source-git-commit: 9ee8e79777b89fbf4d6e5b5fd1dbb1ef3bc9ad5d
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---

# Applicazione di firme elettroniche a un modulo utilizzando firme a mano libera{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

È possibile utilizzare **Firma scarabocchio** componente e **Passaggio firma** componente da disegnare (scarabocchio) in un modulo adattivo. Il componente Passaggio firma visualizza una versione PDF del modulo adattivo. Per utilizzare il componente Passaggio firma è necessaria l’opzione Documento di record abilitata o i moduli adattivi basati su modelli di modulo.

![Finestra di dialogo dei segni di scorrimento](/help/forms/using/assets/scribble-signature.png)

## Varie opzioni disponibili nella finestra Firma

* **R:** Fai clic sul pulsante **Pennello** per disegnare la firma su tela.
* **B:** Fai clic sul pulsante **Cancella** per cancellare la firma sull’area di lavoro.
* **C:** Fai clic sul pulsante **Geolocalizzazione** per aggiungere una geolocalizzazione insieme alla firma.
* **D:** Fai clic sul pulsante **Tastiera** per digitare il nome nell’area di lavoro.

Una volta toccato Fine![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) nella finestra Firma scarabocchio non è possibile modificare la firma. Se si desidera modificare la firma, è necessario ignorare la firma corrente e firmare nuovamente utilizzando l’opzione Pennello/Tastiera di disegno di cui sopra.

Puoi toccare il pulsante **Configura** ![configurare](assets/configure.png) per impostare le proporzioni dell’area di lavoro Firma scarabocchio.
* Se le proporzioni dell’area di lavoro Firma scarabocchio sono inferiori a 1, le informazioni sulla geolocalizzazione vengono aggiunte nella parte inferiore dell’area di lavoro Firma scarabocchio.

* Quando le proporzioni dell’area di lavoro Firma scarabocchio sono superiori a 1, le informazioni sulla geolocalizzazione vengono aggiunte a destra dell’area di lavoro Firma scarabocchio.

![scarabocchio firma-fondo](/help/forms/using/assets/scribble-signature-aspectratio.PNG)


>[!NOTE]
>
>Le firme vengono sempre salvate in formato PNG.

## Configurare un modulo adattivo per l’utilizzo della firma digitale {#configure-an-adaptive-form-to-use-scribble-signature}

1. Crea un modulo adattivo basato su modello di modulo abilitato per l’opzione Documento di record. Per informazioni dettagliate, consulta [Creazione di un modulo adattivo](../../forms/using/creating-adaptive-form.md).
1. Trascina e rilascia la **Firma scarabocchio** dal browser Componenti al modulo adattivo.
1. Tocca **Configura** ![configurare](assets/configure.png) icona. Apre il browser delle proprietà e visualizza le proprietà del componente Firma digitale. Configura le proprietà del componente Firma digitale.
1. Trascina il componente Passaggio firma dal browser Componenti al modulo adattivo.

   >[!NOTE]
   >
   >Il componente Passaggio firma occupa la larghezza completa disponibile per il modulo. Si consiglia di non avere alcun altro componente nella sezione contenente il componente Passaggio firma.

1. Nel browser Contenuto, tocca **Contenitore modulo** e tocca **Configura** ![](/help/forms/using/assets/configure.png) icona. Apre il browser delle proprietà e visualizza le proprietà del contenitore Modulo adattivo. Passa a **Contenitore di moduli adattivi** > **Firma elettronica** e deselezionare la **Abilita Adobe Sign** opzione . Tocca Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) per salvare le modifiche.

   >[!NOTE]
   >
   >Quando si aggiunge un componente Passaggio firma a un modulo adattivo, l’opzione Abilita Adobe Sign viene selezionata automaticamente.

1. Tocca **Configura** ![configurare](assets/configure.png) icona. Apre il browser delle proprietà e visualizza le proprietà del passaggio Firma. Configura le seguenti proprietà:

   * **Nome elemento**: Specifica il nome del componente.

   * **Titolo:** Specifica un titolo univoco del componente.
   * **Messaggio del modello:** Specificare il messaggio da visualizzare durante il caricamento del PDF firma. I servizi Adobe Sign impiegano un po&#39; di tempo per preparare e caricare signature PDF.
   * **Servizio di firma:** Seleziona la **Firma scarabocchio** opzione .

   * **Classe CSS**: Specifica la classe CSS della libreria client, se presente. Si consiglia di utilizzare [temi](../../forms/using/themes.md) e [stili in linea](../../forms/using/inline-style-adaptive-forms.md) anziché CSS Class.

   Tocca Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) per salvare le modifiche. La firma è configurata correttamente.

   Ora, quando si compila un modulo, viene visualizzata una versione PDF del modulo adattivo e vengono fornite le opzioni per firmare il documento PDF. Per informazioni dettagliate, consulta [Firma digitale di un modulo adattivo](../../forms/using/signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature).

## Firma digitale di un modulo adattivo {#sign-an-adaptive-form-using-scribble-signature}

1. Dopo aver compilato un modulo adattivo e aver raggiunto la pagina Passaggio firma, viene visualizzata la schermata della firma.

   ![Finestra di dialogo dei segni di scorrimento](/help/forms/using/assets/esignscribblesign.jpg)

1. Fai clic su **[!UICONTROL Sign]**. Viene visualizzata la finestra di dialogo del segno di scarabocchio. Firma il modulo e fai clic su Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) per salvare la firma.

   ![Finestra di dialogo dei segni di scorrimento](/help/forms/using/assets/scribblewidget.png)

1. Fare clic su completa per completare il processo di firma.

   ![Completare il processo di firma](/help/forms/using/assets/scribblecomplete.jpg)

Le firme vengono aggiunte al modulo e il controllo modulo si sposta nel pannello successivo.
