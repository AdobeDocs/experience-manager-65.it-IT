---
title: Applicare firme elettroniche a un modulo utilizzando le firme scarabocchio
description: Scopri come firmare AEM Adaptive Forms utilizzando la firma a mano. È possibile utilizzare la firma a mano e il passaggio della firma per disegnare la firma in un modulo.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: 096f61b0-59f4-4699-9093-8fb1ed81fded
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 2%

---

# Applicare firme elettroniche a un modulo utilizzando le firme scarabocchio{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

<span class="preview"> Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>


| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-components-to-an-adaptive-form/signing-forms-using-scribble.html) |
| AEM 6.5 | Questo articolo |


È possibile utilizzare il componente **Firma scarabocchio** e il componente **Passaggio firma** per disegnare la firma (scarabocchio) in un modulo adattivo. Il componente del passaggio Firma visualizza una versione PDF del modulo adattivo. Per utilizzare il componente Passaggio firma, è necessario che sia abilitata l’opzione Documento di record o che i moduli adattivi basati su modelli di modulo siano impostati.

![Finestra di dialogo del segno a mano](/help/forms/using/assets/scribble-signature.png)

## Varie opzioni disponibili nella finestra Firma

* **A:** Fai clic sull&#39;icona **Pennello pittura** per disegnare la firma su un&#39;area di lavoro.
* **B:** Fai clic sull&#39;icona **Cancella** per cancellare la firma nell&#39;area di lavoro.
* **C:** Fai clic sull&#39;icona **Geolocation** per aggiungere la geolocalizzazione insieme alla firma.
* **D:** Fai clic sull&#39;icona **Tastiera** per digitare il tuo nome nell&#39;area di lavoro.

Dopo aver selezionato l&#39;icona Fine![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) nella finestra della firma scarabocchio, non è possibile modificare la firma. Nel caso in cui si desideri modificare la firma, è necessario ignorare la firma corrente e riapporla utilizzando l&#39;opzione Pennello/Tastiera.

È possibile selezionare l&#39;icona **Configura** ![configura](assets/configure.png) per impostare le proporzioni dell&#39;area di lavoro Firma scarabocchio.
* Quando le proporzioni dell’area di lavoro Firma a mano sono inferiori a 1, le informazioni sulla geolocalizzazione vengono aggiunte nella parte inferiore dell’area di lavoro Firma a mano.

* Quando le proporzioni dell’area di lavoro Firma scarabocchio sono superiori a 1, le informazioni sulla geolocalizzazione vengono aggiunte al lato destro dell’area di lavoro Firma scarabocchio.

![firma a mano libera](/help/forms/using/assets/scribble-signature-aspectratio.PNG)


>[!NOTE]
>
>Le firme vengono sempre salvate in formato PNG.
>

## Configurare un modulo adattivo per l’utilizzo della firma scarabocchio {#configure-an-adaptive-form-to-use-scribble-signature}

1. Crea un modulo adattivo basato su modello di modulo o con l’opzione Documento di record abilitata. Per informazioni dettagliate, consulta [Creazione di un modulo adattivo](../../forms/using/creating-adaptive-form.md).
1. Trascina il componente **Firma scarabocchio** dal browser componenti al modulo adattivo.
1. Seleziona l&#39;icona **Configura** ![configura](assets/configure.png). Apre il browser delle proprietà e visualizza le proprietà del componente Firma scarabocchio. Configura le proprietà del componente Firma scarabocchio.
1. Trascina il componente Passaggio firma dal browser componenti al modulo adattivo.

   >[!NOTE]
   >
   >Il componente Passaggio di firma occupa l’intera larghezza disponibile per il modulo. Si consiglia di non avere altri componenti nella sezione contenente il componente Passaggio di firma.
   >

1. Nel browser Contenuto, selezionare **Contenitore modulo** e l&#39;icona **Configura** ![configura](/help/forms/using/assets/configure.png). Apre il browser delle proprietà e visualizza le proprietà del contenitore Modulo adattivo. Passa a **Contenitore modulo adattivo** > **Firma elettronica** e deseleziona l&#39;opzione **Abilita Adobe Sign**. Seleziona l&#39;icona Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) per salvare le modifiche.

   >[!NOTE]
   >
   >Quando aggiungi un componente Passaggio di firma a un modulo adattivo, l’opzione Abilita Adobe Sign viene selezionata automaticamente.
   >

1. Seleziona l&#39;icona **Configura** ![configura](assets/configure.png). Apre il browser delle proprietà e visualizza le proprietà del passaggio Firma. Configura le seguenti proprietà:

   * **Nome elemento**: specificare il nome del componente.

   * **Titolo:** Specifica il titolo univoco del componente.
   * **Messaggio modello:** Specificare il messaggio da visualizzare durante il caricamento del PDF della firma. I servizi Adobe Sign impiegano un po’ di tempo per preparare e caricare signature PDF.
   * **Servizio di firma:** Selezionare l&#39;opzione **Firma scarabocchio**.

   * **Classe CSS**: specificare la classe CSS della libreria client, se presente. Utilizza [temi](../../forms/using/themes.md) e [stili in linea](../../forms/using/inline-style-adaptive-forms.md) invece della classe CSS.

   Seleziona l&#39;icona Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) per salvare le modifiche. La firma è stata configurata correttamente.

   Ora, quando si compila un modulo, viene visualizzata una versione PDF del modulo adattivo e vengono fornite le opzioni per la firma del documento PDF. Per informazioni dettagliate, consulta [Firmare un modulo adattivo utilizzando la firma scarabocchio](../../forms/using/signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature).

## Firmare un modulo adattivo utilizzando la firma scarabocchio {#sign-an-adaptive-form-using-scribble-signature}

1. Dopo aver compilato un modulo adattivo e aver raggiunto la pagina Passaggio firma, viene visualizzata la schermata della firma.

   ![Finestra di dialogo del segno a mano](/help/forms/using/assets/esignscribblesign.jpg)

1. Fai clic su **[!UICONTROL Firma]**. Viene visualizzata la finestra di dialogo del segno scarabocchio. Firma il modulo e fai clic sull&#39;icona Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) per salvare la firma.

   ![Finestra di dialogo del segno a mano](/help/forms/using/assets/scribblewidget.png)

1. Fare clic su Completa per completare il processo di firma.

   ![Completare il processo di firma](/help/forms/using/assets/scribblecomplete.jpg)

Le firme vengono aggiunte al modulo e il controllo modulo passa al pannello successivo.
