---
title: "Tutorial: creare un modulo adattivo"
description: Scopri come creare, creare il layout e visualizzare in anteprima un modulo adattivo. Inoltre, scopri come configurare le azioni di invio.
feature: Adaptive Forms
exl-id: c0a2adcd-528a-41af-99b5-d8b423cd6605
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1314'
ht-degree: 8%

---

# Tutorial: creare un modulo adattivo {#do-not-publish-tutorial-create-an-adaptive-form}

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

Questo tutorial è un passaggio della serie [Creare il primo modulo adattivo](/help/forms/using/create-your-first-adaptive-form.md). Si consiglia di seguire la serie in sequenza cronologica per comprendere, eseguire e dimostrare il caso di utilizzo completo dell’esercitazione.

## Informazioni sull’esercitazione {#about-the-tutorial}

I moduli adattivi sono moduli di nuova generazione dinamici e reattivi. Puoi utilizzare i moduli adattivi per fornire esperienze personalizzate. È inoltre possibile integrare i moduli adattivi con [!DNL Adobe Analytics] per le statistiche di utilizzo e [!DNL Adobe Campaign] per la gestione delle campagne. Per ulteriori informazioni sulle funzionalità dei moduli adattivi, consulta [Introduzione alla creazione di moduli adattivi](/help/forms/using/introduction-forms-authoring.md).

La creazione e la gestione dei moduli è più semplice se si segue un processo appropriato. In questo articolo imparerai a:

* [Crea un modulo adattivo che consenta a un cliente di aggiungere un indirizzo di spedizione](/help/forms/using/create-adaptive-form.md#step-create-the-adaptive-form)

* [Layout dei campi di un modulo adattivo per visualizzare e accettare informazioni da un cliente](/help/forms/using/create-adaptive-form.md#step-add-header-and-footer)

* [Crea un’azione di invio per inviare un’e-mail contenente il contenuto del modulo](/help/forms/using/create-adaptive-form.md#step-add-components-to-capture-and-display-information)
* [Anteprima e invio di un modulo adattivo](/help/forms/using/create-adaptive-form.md)

Avrai un modulo simile al seguente entro la fine dell’articolo:\
[![Anteprima modulo in dispositivi mobili](do-not-localize/form-preview-mobile.gif)](do-not-localize/form-preview-mobile.gif)

## Passaggio 1: creare il modulo adattivo {#step-create-the-adaptive-form}

1. Accedi all&#39;istanza di creazione dell&#39;AEM e passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**. URL predefinito: [http://localhost:4502/aem/forms.html/content/dam/formsanddocuments](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments).
1. Seleziona **[!UICONTROL Crea]** e **[!UICONTROL Modulo adattivo]**. Viene visualizzata un&#39;opzione per selezionare un modello. Seleziona il modello **[!UICONTROL Vuoto]** per selezionarlo e scegli **[!UICONTROL Successivo]**.

1. Viene visualizzata un&#39;opzione per **[!UICONTROL Aggiungi proprietà]**. I campi **[!UICONTROL Titolo]** e **[!UICONTROL Nome]** sono obbligatori:

   * **Titolo:** Specificare `Add new or update shipping address` nel campo **[!UICONTROL Titolo]**. Il campo titolo specifica il nome visualizzato del modulo. Il titolo consente di identificare il modulo nell&#39;interfaccia utente [!DNL Forms] dell&#39;AEM.
   * **Nome:** Specificare `shipping-address-add-update-form` nel campo **[!UICONTROL Nome]**. Il campo Nome specifica il nome del modulo. Nell’archivio viene creato un nodo con il nome specificato. Quando si inizia a digitare un titolo, il valore del campo nome viene generato automaticamente. Puoi modificare il valore suggerito. Il campo nome può contenere solo caratteri alfanumerici, trattini e caratteri di sottolineatura. Tutti gli input non validi vengono sostituiti da un trattino.

1. Seleziona **[!UICONTROL Crea]**. Viene creato un modulo adattivo e viene visualizzata una finestra di dialogo per aprire il modulo per la modifica. Seleziona **[!UICONTROL Apri]** per aprire il nuovo modulo creato in una nuova scheda. Il modulo viene aperto per la modifica. Viene visualizzata inoltre la barra laterale per personalizzare il modulo appena creato in base alle esigenze.

   Per informazioni sull&#39;interfaccia per l&#39;authoring di moduli adattivi e sui componenti disponibili, consulta [Introduzione all&#39;authoring di moduli adattivi](/help/forms/using/creating-adaptive-form.md).

   ![Modulo adattivo appena creato.](assets/newly-created-adaptive-form.png)

## Passaggio 2: aggiungere intestazione e piè di pagina {#step-add-header-and-footer}

L&#39;AEM [!DNL Forms] fornisce molti componenti per visualizzare informazioni su un modulo adattivo. I componenti Intestazione e Piè di pagina consentono di conferire a un modulo un aspetto coerente. In genere, un’intestazione include il logo di un’azienda, il titolo del modulo e il riepilogo. Un piè di pagina include in genere informazioni sul copyright e collegamenti ad altre pagine.

1. Seleziona ![pannello laterale di attivazione](assets/toggle-side-panel.png) > ![treeexpandall](assets/treeexpandall.png). Viene visualizzato il browser Componenti (Component). Trascina il componente **[!UICONTROL Intestazione]** dal browser componenti al modulo adattivo.
1. Seleziona **[!UICONTROL Logo]**. Viene visualizzata la barra degli strumenti. Seleziona ![aem_6_3_edit](assets/aem_6_3_edit.png) sulla barra degli strumenti, digita **We.Retail** e seleziona ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

1. Seleziona Immagine. Viene visualizzata la barra degli strumenti. Selezionare ![cmppr](assets/cmppr.png). Il browser delle proprietà si apre a sinistra dello schermo. **[!UICONTROL Sfoglia]** e carica l&#39;immagine del logo. Seleziona ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). L&#39;immagine viene visualizzata nell&#39;intestazione.

   Se non ne hai uno, seleziona Ottieni file per scaricare il logo utilizzato in questo articolo.

[Ottieni file](assets/logo.png)

1. Trascina il componente **[!UICONTROL Footer]** da ![treeexpandall](assets/treeexpandall.png) nel modulo adattivo. In questa fase, il modulo si presenta come segue:

   ![modulo adattivo con intestazioni e piè di pagina](assets/adaptive-form-with-headers-and-footers.png)

## Passaggio 3: aggiungere componenti per acquisire e visualizzare informazioni {#step-add-components-to-capture-and-display-information}

I componenti sono elementi costitutivi di un modulo adattivo. L&#39;AEM [!DNL Forms] fornisce molti componenti per acquisire e visualizzare informazioni in un modulo adattivo. Puoi trascinare i componenti da ![treeexpandall](assets/treeexpandall.png) a un modulo. Per informazioni sui componenti disponibili e sulle funzionalità corrispondenti, consulta [Introduzione alla creazione di moduli adattivi](/help/forms/using/introduction-forms-authoring.md).

1. Trascina il componente **[!UICONTROL Casella numerica]** nel modulo adattivo. Posizionalo prima del componente Piè di pagina. Apri le proprietà del componente, cambia **[!UICONTROL Titolo]** del componente in **`Customer ID`**, cambia **[!UICONTROL Nome elemento]** in **`customer_ID`**, abilita l&#39;opzione **[!UICONTROL Campo richiesto]**, abilita l&#39;opzione **[!UICONTROL Usa tipo di input numero HTML5]** e seleziona ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
1. Trascina tre componenti Casella di testo nel modulo adattivo. Posizionale prima del componente Piè di pagina. Impostare le seguenti proprietà per queste caselle di testo.:

   <table> 
    <tbody> 
     <tr> 
      <td><b>Proprietà</b></td> 
      <td><b>Riquadro 1<br/></b></td> 
      <td><b>Casella di testo 2<br/></b></td> 
      <td><b>Riquadro 3</b></td> 
     </tr> 
     <tr> 
      <td>Titolo</td> 
      <td>Nome<br /> </td> 
      <td>Indirizzo di spedizione</td> 
      <td>Stato</td> 
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
      <td>Consenti più righe<br /> </td> 
      <td>Disattivato</td> 
      <td>Abilitato</td> 
      <td>Disattivato</td> 
     </tr> 
    </tbody> 
   </table>

1. Trascina un componente **[!UICONTROL Casella numerica]** prima del componente piè di pagina. Apri le proprietà del componente, imposta i valori elencati nella tabella seguente, seleziona ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Proprietà | Valore |
   |---|---|
   | Titolo | Codice postale |
   | Nome elemento | customer_ZIPCode |
   | Numero massimo di cifre | 6 |
   | Campo obbligatorio | Abilitato |
   | Tipo di pattern di visualizzazione | Nessun pattern |

1. Trascina un componente **[!UICONTROL E-mail]** prima del componente piè di pagina. Apri le proprietà del componente, imposta i valori elencati nella tabella seguente e seleziona ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Proprietà | Valore |
   |---|---|
   | Titolo | E-mail |
   | Nome elemento | customer_Email |
   | Campo obbligatorio | Abilitato |

1. Trascina un componente **[!UICONTROL File allegato]** prima del componente piè di pagina. Apri le proprietà del componente, imposta i valori elencati nella tabella seguente e seleziona ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>Proprietà</b></td> 
      <td><b>Valore</b></td> 
     </tr> 
     <tr> 
      <td>Titolo</td> 
      <td>Bozza indirizzo approvato dal governo<br /> </td> 
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

1. Trascina un componente **[!UICONTROL Pulsante di invio]** nel modulo adattivo. Posizionalo prima del componente Piè di pagina. Apri le proprietà del componente, cambia il nome elemento in `address_addition_update_submit`, seleziona ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). Il layout del modulo è completo e l&#39;aspetto del modulo è il seguente:

   ![modulo adattivo-con-tutti-i-componenti](assets/adaptive-form-with-all-the-components.png)

## Passaggio 4: configurare l’azione di invio per il modulo adattivo {#step-configure-submit-action-for-the-adaptive-form}

Un’azione di invio viene attivata quando un utente tocca il pulsante Invia in un modulo adattivo. È possibile utilizzare un’azione di invio per salvare i dati del modulo nell’archivio locale, inviare i dati del modulo a un endpoint REST, inviare i dati del modulo come e-mail e altro ancora. I moduli adattivi forniscono alcune ulteriori azioni di invio pronte all’uso. Per informazioni dettagliate, vedere [Configurazione dell&#39;azione Invia](/help/forms/using/configuring-submit-actions.md).

La procedura seguente consente di configurare l’azione di invio e-mail e l’azione di invio demo del modulo:

1. Configura il server e-mail. Per ulteriori dettagli, vedere [Configurazione della notifica e-mail](/help/sites-administering/notification.md).


1. Selezionare **[!UICONTROL Contenitore modulo]** nel browser Contenuti e selezionare ![cmppr](assets/cmppr.png). Il browser delle proprietà si apre a sinistra.
1. Vai a **[!UICONTROL Invio]** > **[!UICONTROL Azione invio]**. Seleziona **[!UICONTROL Invia e-mail]**. Specifica i seguenti valori e seleziona ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Proprietà | Valore |
   |--- |--- |
   | Da | `donotreply@weretail.com` |
   | A | `${customer_Email}` |
   | Oggetto | Conferma: hai aggiunto l&#39;indirizzo di spedizione sul sito Web We.Retail. |
   | Modello e-mail | Salve `${customer_Name}`, il seguente indirizzo viene aggiunto come indirizzo di spedizione per il tuo account: <br>`${customer_Name}`, `${customer_Shipping_Address}`, `${customer_State}`, `${customer_ZIPCode}`<br> Cordiali saluti, We.Retail |
   | Includi allegati | Abilitato |

   Modulo pronto. Ora è possibile visualizzare in anteprima il modulo e verificarne la funzionalità. Se si è utilizzato il nome indicato nell&#39;esercitazione e si accede al modulo nel computer che esegue il server AEM [!DNL Forms], il modulo sarà disponibile all&#39;indirizzo [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html).

## Passaggio 5: visualizzare in anteprima e inviare il modulo adattivo {#step-preview-and-submit-the-adaptive-form}

È possibile utilizzare l&#39;opzione **[!UICONTROL Anteprima]** per valutare l&#39;aspetto e il comportamento di un modulo. Puoi inviare un modulo in modalità anteprima e controllare anche le convalide applicate a un modulo. Ad esempio, se viene visualizzato un errore quando un campo obbligatorio viene lasciato vuoto.

I moduli adattivi offrono anche un’opzione per emulare l’esperienza di un modulo per vari dispositivi. Ad esempio, iPhone, iPad e Desktop. Puoi utilizzare entrambe le opzioni **[!UICONTROL Anteprima]** e **[!UICONTROL Emulatore]** ![righello](assets/ruler.png) insieme per visualizzare in anteprima un modulo per dispositivi con dimensioni di schermo diverse.

1. Seleziona l&#39;opzione **[!UICONTROL Anteprima]** sul lato destro dell&#39;editor di moduli. Il modulo viene aperto in modalità anteprima. Se hai usato il nome menzionato nell&#39;esercitazione, l&#39;URL di anteprima del modulo è [http://localhost:4502/content/dam/formsanddocuments/shipping-address-add-update-form/jcr:content?wcmmode=disabled](http://localhost:4502/content/dam/formsanddocuments/shipping-address-addition-updation-form/jcr:content?wcmmode=disabled)
1. Utilizza ![righello](assets/ruler.png) per visualizzare l&#39;aspetto del modulo su vari dispositivi.
1. Compila i campi del modulo e seleziona **[!UICONTROL Invia]**. Il modulo è stato inviato e si è reindirizzati alla pagina predefinita **Grazie**. È inoltre possibile specificare una pagina di ringraziamento personalizzata. Per ulteriori dettagli, vedere [Configurazione della pagina di reindirizzamento](/help/forms/using/configuring-redirect-page.md).

Il modulo adattivo per aggiungere un indirizzo è pronto. Se è stato utilizzato il nome indicato nell&#39;esercitazione e si accede al modulo nel computer che esegue il server AEM Forms, il modulo sarà disponibile all&#39;indirizzo [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html).
