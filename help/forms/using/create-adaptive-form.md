---
title: '"Esercitazione: Creare un modulo adattivo"'
seo-title: '"Crea un modulo adattivo"'
description: Creazione, layout e anteprima di un modulo adattivo. Inoltre, scopri come configurare le azioni di invio.
seo-description: Creazione, layout e anteprima di un modulo adattivo. Inoltre, scopri come configurare le azioni di invio.
page-status-flag: de-activated
uuid: 0010d274-a683-499e-9fa6-ce355d7898a0
discoiquuid: 55c08940-8c25-4938-8e49-25bce20aaf22
translation-type: tm+mt
source-git-commit: 78768e6eab65f452421d8809384500c6eab6b97f
workflow-type: tm+mt
source-wordcount: '1395'
ht-degree: 3%

---


# Esercitazione: Creare un modulo adattivo {#do-not-publish-tutorial-create-an-adaptive-form}

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

Questa esercitazione è un passaggio della serie [Crea il tuo primo modulo adattivo](/help/forms/using/create-your-first-adaptive-form.md). Si consiglia di seguire le serie in sequenza cronologica per comprendere, eseguire e dimostrare l&#39;uso completo dell&#39;esercitazione.

## Informazioni sull&#39;esercitazione {#about-the-tutorial}

I moduli adattivi sono moduli di nuova generazione dinamici e reattivi. È possibile utilizzare i moduli adattivi per distribuire esperienze personalizzate. È inoltre possibile integrare moduli adattivi con [!DNL Adobe Analytics] per le statistiche di utilizzo e con [!DNL Adobe Campaign] per la gestione delle campagne. Per ulteriori informazioni sulle funzionalità dei moduli adattivi, vedere [Introduzione alla creazione di moduli adattivi](/help/forms/using/introduction-forms-authoring.md).

È più facile creare e gestire i moduli quando si segue un processo appropriato. In questo articolo viene illustrato come:

* [Creare un modulo adattivo che consenta al cliente di aggiungere un indirizzo di spedizione](/help/forms/using/create-adaptive-form.md#step-create-the-adaptive-form)

* [Campi di layout di un modulo adattivo per visualizzare e accettare le informazioni di un cliente](/help/forms/using/create-adaptive-form.md#step-add-header-and-footer)

* [Creare un&#39;azione di invio per inviare un&#39;e-mail contenente il contenuto del modulo](/help/forms/using/create-adaptive-form.md#step-add-components-to-capture-and-display-information)
* [Anteprima e invio di un modulo adattivo](/help/forms/using/create-adaptive-form.md)

Alla fine dell&#39;articolo sarà disponibile un modulo simile al seguente:\
[![](do-not-localize/form-preview-mobile.gif)](do-not-localize/form-preview-mobile.gif)

## Passaggio 1: Creare il modulo adattivo {#step-create-the-adaptive-form}

1. Accedete all&#39;istanza di creazione AEM e andate a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**. L&#39;URL predefinito è [http://localhost:4502/aem/forms.html/content/dam/formsanddocuments](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments).
1. Toccate **[!UICONTROL Crea]** e selezionate **[!UICONTROL Modulo adattivo]**. Viene visualizzata un’opzione per selezionare un modello. Toccate il modello **[!UICONTROL Blank]** per selezionarlo e toccate **[!UICONTROL Next]**.

1. Viene visualizzata l&#39;opzione **[!UICONTROL Aggiungi proprietà]**. I campi **[!UICONTROL Title]** e **[!UICONTROL Name]** sono obbligatori:

   * **Titolo:** specificate  `Add new or update shipping address` nel campo  **** Titolo. Il campo title specifica il nome visualizzato del modulo. Il titolo consente di identificare il modulo nell&#39;interfaccia AEM [!DNL Forms] utente.
   * **Nome:** specificate  `shipping-address-add-update-form` nel campo  **** Nome. Il campo Nome specifica il nome del modulo. Nella directory archivio viene creato un nodo con il nome specificato. Quando si inizia a digitare un titolo, viene automaticamente generato il valore relativo al campo del nome. È possibile modificare il valore suggerito. Il campo del nome può includere solo caratteri alfanumerici, trattini e caratteri di sottolineatura. Tutti gli input non validi vengono sostituiti con un trattino.

1. Toccate **[!UICONTROL Crea]**. Viene creato un modulo adattivo e viene visualizzata una finestra di dialogo per aprire il modulo per la modifica. Toccate **[!UICONTROL Apri]** per aprire il modulo appena creato in una nuova scheda. Il modulo viene aperto per la modifica. Inoltre, consente di visualizzare la barra laterale per personalizzare il modulo appena creato in base alle esigenze.

   Per informazioni sull&#39;interfaccia per la creazione di moduli adattivi e sui componenti disponibili, vedere [Introduzione alla creazione di moduli adattivi](/help/forms/using/creating-adaptive-form.md).

   ![nuovo modulo adattivo](assets/newly-created-adaptive-form.png)

## Passaggio 2: Aggiungi intestazione e piè di pagina {#step-add-header-and-footer}

AEM [!DNL Forms] fornisce molti componenti per visualizzare informazioni su un modulo adattivo. I componenti Intestazione e Piè di pagina offrono un aspetto e un aspetto uniformi ai moduli. Un&#39;intestazione include in genere il logo di una società, il titolo del modulo e il riepilogo. Un piè di pagina include in genere informazioni sul copyright e collegamenti verso altre pagine.

1. Toccate ![interruttore-side-panel](assets/toggle-side-panel.png) > ![treeexpandall](assets/treeexpandall.png). Si apre il Browser componenti. Trascinate il componente **[!UICONTROL Header]** dal browser componenti al modulo adattivo.
1. Toccate **[!UICONTROL Logo]**. Viene visualizzata la barra degli strumenti. Toccate ![aem_6_3_edit](assets/aem_6_3_edit.png) sulla barra degli strumenti, digitate **We.Retail**, quindi toccate ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

1. Toccate Immagine. Viene visualizzata la barra degli strumenti. Toccate ![cmppr](assets/cmppr.png). Il browser delle proprietà si apre a sinistra dello schermo. **[!UICONTROL Esplorate]** e caricate l’immagine del logo. Toccate ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). L’immagine viene visualizzata nell’intestazione.

   Toccate Ottieni file per scaricare il logo utilizzato in questo articolo, se non ne avete uno.

   [Ottieni file](assets/logo.png)

1. Trascinare il componente **[!UICONTROL Piè di pagina]** da ![treeexpandall](assets/treeexpandall.png) al modulo adattivo. A questo punto, il modulo si presenta come segue:

   ![forma adattiva con intestazioni e piè di pagina](assets/adaptive-form-with-headers-and-footers.png)

## Passaggio 3: Aggiunta di componenti per acquisire e visualizzare informazioni {#step-add-components-to-capture-and-display-information}

I componenti sono elementi costitutivi di un modulo adattivo. AEM [!DNL Forms] offre molti componenti per acquisire e visualizzare informazioni in un modulo adattivo. È possibile trascinare i componenti da ![treeexpandall](assets/treeexpandall.png) a un modulo. Per informazioni sui componenti disponibili e sulle funzionalità corrispondenti, vedere [Introduzione alla creazione di moduli adattivi](/help/forms/using/introduction-forms-authoring.md).

1. Trascinare il componente **[!UICONTROL Casella numerica]** nel modulo adattivo. Posizionarlo prima del componente piè di pagina. Aprite le proprietà del componente, modificate **[!UICONTROL Titolo]** del componente in **`Customer ID`**, modificate **[!UICONTROL Nome elemento]** in **`customer_ID`**, abilitate l&#39;opzione **[!UICONTROL Campo richiesto]**, abilitate l&#39;opzione **[!UICONTROL Usa tipo di input di numero HTML5]** e toccate ![aem_6_forms_save](assets/aem_6_3_forms_save.png).
1. Trascinare tre componenti Casella di testo nel modulo adattivo. Posizionare questi elementi prima del componente piè di pagina. Impostare le seguenti proprietà per queste caselle di testo.:

   <table> 
    <tbody> 
     <tr> 
      <td><b>Proprietà</b></td> 
      <td><b>Casella di testo 1<br/></b></td> 
      <td><b>Casella di testo 2<br/></b></td> 
      <td><b>Casella di testo 3</b></td> 
     </tr> 
     <tr> 
      <td>Titolo</td> 
      <td>Nome<br /> </td> 
      <td>Indirizzo di spedizione</td> 
      <td>Stadio</td> 
     </tr> 
     <tr> 
      <td>Nome elemento</td> 
      <td>customer_Name<br /> </td> 
      <td>customer_Shipping_Address</td> 
      <td>customer_State</td> 
     </tr> 
     <tr> 
      <td>Campo obbligatorio</td> 
      <td>Abilitato</td> 
      <td>Abilitato</td> 
      <td>Abilitato</td> 
     </tr> 
     <tr> 
      <td>Consenti righe multiple<br /> </td> 
      <td>Disattivato</td> 
      <td>Abilitato</td> 
      <td>Disattivato</td> 
     </tr> 
    </tbody> 
   </table>

1. Trascinare un componente **[!UICONTROL Casella numerica]** prima del componente piè di pagina. Aprire le proprietà del componente, impostare i valori elencati nella tabella seguente, Toccare ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Proprietà | Valore |
   |---|---|
   | Titolo | Codice ZIP |
   | Nome elemento | customer_ZIPCode |
   | Numero massimo di cifre | 6 |
   | Campo obbligatorio | Abilitato |
   | Tipo di pattern di visualizzazione | Nessun pattern |

1. Trascinare un componente **[!UICONTROL E-mail]** prima del componente piè di pagina. Aprite le proprietà del componente, impostate i valori elencati nella tabella seguente e toccate ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Proprietà | Valore |
   |---|---|
   | Titolo | E-mail |
   | Nome elemento | customer_Email |
   | Campo obbligatorio | Abilitato |

1. Trascinare un componente **[!UICONTROL File Attachment]** prima del componente piè di pagina. Aprite le proprietà del componente, impostate i valori elencati nella tabella seguente e toccate ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>Proprietà</b></td> 
      <td><b>Valore</b></td> 
     </tr> 
     <tr> 
      <td>Titolo</td> 
      <td>Prova indirizzo approvata governativa<br /> </td> 
     </tr> 
     <tr> 
      <td>Nome elemento</td> 
      <td>customer_Address_Proof</td> 
     </tr> 
     <tr> 
      <td>Campo obbligatorio</td> 
      <td>Abilitato</td> 
     </tr> 
    </tbody> 
   </table>

1. Trascinare un componente **[!UICONTROL Pulsante Invia]** nel modulo adattivo. Posizionarlo prima del componente piè di pagina. Aprite le proprietà del componente, modificate Nome elemento in `address_addition_update_submit`, toccate ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). Il layout del modulo è completo e il modulo ha il seguente aspetto:

   ![forma adattiva con tutti i componenti](assets/adaptive-form-with-all-the-components.png)

## Passaggio 4: Configurare l&#39;azione di invio per il modulo adattivo {#step-configure-submit-action-for-the-adaptive-form}

Un&#39;azione di invio viene attivata quando un utente tocca il pulsante Invia su un modulo adattivo. È possibile utilizzare un&#39;azione di invio per salvare i dati del modulo nell&#39;archivio locale, inviare i dati del modulo a un endpoint REST, inviare i dati del modulo come messaggio e-mail e altro ancora. Nei moduli adattivi sono disponibili ulteriori azioni di invio pronte all’uso. Per informazioni dettagliate, vedere [Configurazione dell&#39;azione di invio](/help/forms/using/configuring-submit-actions.md).

Utilizzando i passaggi seguenti, è possibile configurare l&#39;azione di invio tramite e-mail e l&#39;azione di invio tramite demo del modulo:

1. Configurare il server e-mail. Per informazioni dettagliate, vedere [Configurazione delle notifiche e-mail](/help/sites-administering/notification.md).


1. Toccate **[!UICONTROL Contenitore modulo]** nel browser Contenuto e toccate ![cmppr](assets/cmppr.png). Il browser delle proprietà si apre a sinistra.
1. Vai a **[!UICONTROL Invio]** > **[!UICONTROL Invia azione]**. Selezionare **[!UICONTROL Invia e-mail]**. Specificate i seguenti valori e toccate ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Proprietà | Valore |
   |--- |--- |
   | Da | `donotreply@weretail.com` |
   | A | `${customer_Email}` |
   | Oggetto | Riconoscimento: Avete aggiunto l&#39;indirizzo di spedizione sul sito Web We.Retail. |
   | Modello e-mail | Ciao `${customer_Name}`, il seguente indirizzo è aggiunto come indirizzo di spedizione per il tuo account: <br>`${customer_Name}`, `${customer_Shipping_Address}`, `${customer_State}`, `${customer_ZIPCode}`<br> Considerazioni, We.Retail |
   | Includi allegati | Abilitato |

   Il modulo è pronto. Ora è possibile visualizzare l&#39;anteprima del modulo e verificare la funzionalità. Se si è utilizzato il nome indicato nell&#39;esercitazione e si accede al modulo sul computer che esegue AEM server [!DNL Forms], il modulo è disponibile all&#39;indirizzo [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html).

## Passaggio 5: Visualizzare l&#39;anteprima e inviare il modulo adattivo {#step-preview-and-submit-the-adaptive-form}

È possibile utilizzare l&#39;opzione **[!UICONTROL Anteprima]** per valutare l&#39;aspetto e il funzionamento di un modulo. È possibile inviare un modulo in modalità di anteprima e controllare anche le convalide applicate a un modulo. Ad esempio, se viene visualizzato un errore quando un campo obbligatorio viene lasciato vuoto.

I moduli adattivi offrono inoltre la possibilità di emulare l&#39;esperienza di un modulo per diversi dispositivi. Ad esempio, iPhone, iPad e Desktop. È possibile utilizzare le opzioni **[!UICONTROL Anteprima]** e **[!UICONTROL Emulatore]** ![righello](assets/ruler.png) in combinazione tra loro per visualizzare in anteprima un modulo per dispositivi di diverse dimensioni dello schermo.

1. Toccare l&#39;opzione **[!UICONTROL Anteprima]** a destra dell&#39;editor del modulo. Il modulo si apre in modalità di anteprima. Se si è utilizzato il nome indicato nell&#39;esercitazione, l&#39;URL di anteprima del modulo è [http://localhost:4502/content/dam/formsanddocuments/shipping-address-add-update-form/jcr:content?wcmmode=disabled](http://localhost:4502/content/dam/formsanddocuments/shipping-address-addition-updation-form/jcr:content?wcmmode=disabled)
1. Utilizzare ![righello](assets/ruler.png) per visualizzare l&#39;aspetto del modulo su vari dispositivi.
1. Compila i campi del modulo e tocca **[!UICONTROL Invia]**. Il modulo viene inviato e si viene reindirizzati alla pagina **Grazie** predefinita. Potete anche specificare una pagina di ringraziamento personalizzata. Per informazioni dettagliate, vedere [Configurazione della pagina di reindirizzamento](/help/forms/using/configuring-redirect-page.md).

Il modulo adattivo per aggiungere un indirizzo è pronto. Se si è utilizzato il nome indicato nell&#39;esercitazione e si accede al modulo sul computer che esegue  server AEM Forms, il modulo è disponibile all&#39;indirizzo [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html).
