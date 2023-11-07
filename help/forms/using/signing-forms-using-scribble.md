---
title: Applicare firme elettroniche a un modulo utilizzando le firme scarabocchio
description: Scopri come firmare AEM Adaptive Forms utilizzando la firma a mano. È possibile utilizzare la firma scarabocchio e il passaggio della firma per disegnare la firma su un modulo.
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 76d178d1-8e40-41b3-80d4-66b2f8d04211
docset: aem65
feature: Adaptive Forms
exl-id: 096f61b0-59f4-4699-9093-8fb1ed81fded
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 2%

---

# Applicare firme elettroniche a un modulo utilizzando le firme scarabocchio{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

<span class="preview"> L’Adobe consiglia di utilizzare l’acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>


| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-components-to-an-adaptive-form/signing-forms-using-scribble.html) |
| AEM 6.5 | Questo articolo |


È possibile utilizzare **Firma a mano** componente e **Passaggio di firma** componente per disegnare una firma (a mano libera) su un modulo adattivo. Il componente del passaggio Firma visualizza una versione PDF del modulo adattivo. Per utilizzare il componente Passaggio firma, è necessario che sia abilitata l’opzione Documento di record o che i moduli adattivi basati su modelli di modulo siano impostati.

![Finestra di dialogo Simbolo a mano](/help/forms/using/assets/scribble-signature.png)

## Varie opzioni disponibili nella finestra Firma

* **R:** Fai clic su **Pennello vernice** per disegnare la firma sull&#39;area di lavoro.
* **B:** Fai clic su **Cancella** per cancellare la firma dall&#39;area di lavoro.
* **C:** Fai clic su **Geolocalizzazione** per aggiungere la geolocalizzazione insieme alla firma.
* **D:** Fai clic su **Tastiera** per digitare il proprio nome nell&#39;area di lavoro.

Una volta toccato il pulsante Fine![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) nella finestra Firma scarabocchio, non è possibile modificare la firma. Nel caso in cui si desideri modificare la firma, è necessario ignorare la firma corrente e riapporla utilizzando l&#39;opzione Pennello/Tastiera.

Puoi toccare il **Configura** ![configura](assets/configure.png) per impostare le proporzioni dell’area di lavoro della firma scarabocchio.
* Quando le proporzioni dell’area di lavoro Firma a mano sono inferiori a 1, le informazioni sulla geolocalizzazione vengono aggiunte nella parte inferiore dell’area di lavoro Firma a mano.

* Quando le proporzioni dell’area di lavoro Firma scarabocchio sono superiori a 1, le informazioni sulla geolocalizzazione vengono aggiunte al lato destro dell’area di lavoro Firma scarabocchio.

![firma scarabocchio-inferiore](/help/forms/using/assets/scribble-signature-aspectratio.PNG)


>[!NOTE]
>
>Le firme vengono sempre salvate in formato PNG.
>

## Configurare un modulo adattivo per l’utilizzo della firma scarabocchio {#configure-an-adaptive-form-to-use-scribble-signature}

1. Crea un modulo adattivo basato su modello di modulo o con l’opzione Documento di record abilitata. Per informazioni dettagliate, consulta [Creazione di un modulo adattivo](../../forms/using/creating-adaptive-form.md).
1. Trascina la selezione **Firma a mano** dal browser componenti al modulo adattivo.
1. Tocca il **Configura** ![configura](assets/configure.png) icona. Apre il browser delle proprietà e visualizza le proprietà del componente Firma scarabocchio. Configura le proprietà del componente Firma scarabocchio.
1. Trascina il componente Passaggio firma dal browser componenti al modulo adattivo.

   >[!NOTE]
   >
   >Il componente Passaggio di firma occupa l’intera larghezza disponibile per il modulo. Si consiglia di non avere altri componenti nella sezione contenente il componente Passaggio di firma.
   >

1. Nel browser Contenuti, tocca **Contenitore modulo**, e tocca il **Configura** ![configura](/help/forms/using/assets/configure.png) icona. Apre il browser delle proprietà e visualizza le proprietà del contenitore Modulo adattivo. Accedi a **Contenitore modulo adattivo** > **Firma elettronica** e deseleziona la **Abilita Adobe Sign** opzione. Tocca Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) per salvare le modifiche.

   >[!NOTE]
   >
   >Quando aggiungi un componente Passaggio di firma a un modulo adattivo, l’opzione Abilita Adobe Sign viene selezionata automaticamente.
   >

1. Tocca il **Configura** ![configura](assets/configure.png) icona. Apre il browser delle proprietà e visualizza le proprietà del passaggio Firma. Configura le seguenti proprietà:

   * **Nome elemento**: specifica il nome del componente.

   * **Titolo:** Specifica un titolo univoco per il componente.
   * **Messaggio modello:** Specificare il messaggio da visualizzare durante il caricamento del PDF della firma. I servizi Adobe Sign impiegano un po’ di tempo per preparare e caricare signature PDF.
   * **Servizio di firma:** Seleziona la **Firma a mano** opzione.

   * **Classe CSS**: specifica la classe CSS della libreria client, se presente. Utilizzare [temi](../../forms/using/themes.md) e [stili in linea](../../forms/using/inline-style-adaptive-forms.md) anziché Classe CSS.

   Tocca Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) per salvare le modifiche. La firma è stata configurata correttamente.

   Ora, quando si compila un modulo, viene visualizzata una versione PDF del modulo adattivo e vengono fornite le opzioni per la firma del documento PDF. Per informazioni dettagliate, consulta [Firmare un modulo adattivo utilizzando la firma scarabocchio](../../forms/using/signing-forms-using-scribble.md#sign-an-adaptive-form-using-scribble-signature).

## Firmare un modulo adattivo utilizzando la firma scarabocchio {#sign-an-adaptive-form-using-scribble-signature}

1. Dopo aver compilato un modulo adattivo e aver raggiunto la pagina Passaggio firma, viene visualizzata la schermata della firma.

   ![Finestra di dialogo Simbolo a mano](/help/forms/using/assets/esignscribblesign.jpg)

1. Clic **[!UICONTROL Firma]**. Viene visualizzata la finestra di dialogo del segno scarabocchio. Firma il modulo e fai clic su Fine ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) per salvare la firma.

   ![Finestra di dialogo Simbolo a mano](/help/forms/using/assets/scribblewidget.png)

1. Fare clic su Completa per completare il processo di firma.

   ![Completa il processo di firma](/help/forms/using/assets/scribblecomplete.jpg)

Le firme vengono aggiunte al modulo e il controllo modulo passa al pannello successivo.
