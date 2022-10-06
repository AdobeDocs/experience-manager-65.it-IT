---
title: 'Tutorial: Creare un modulo adattivo"'
seo-title: Create an adaptive form
description: Scopri come creare, impostare il layout e visualizzare in anteprima un modulo adattivo. Inoltre, scopri come configurare le azioni di invio.
seo-description: Learn to create, layout, and preview an adaptive form. Also, learn to configure submit actions.
page-status-flag: de-activated
uuid: 0010d274-a683-499e-9fa6-ce355d7898a0
discoiquuid: 55c08940-8c25-4938-8e49-25bce20aaf22
feature: Adaptive Forms
exl-id: c0a2adcd-528a-41af-99b5-d8b423cd6605
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1376'
ht-degree: 3%

---

# Esercitazione: Creare un modulo adattivo {#do-not-publish-tutorial-create-an-adaptive-form}

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

Questa esercitazione è un passaggio nel [Creare il primo modulo adattivo](/help/forms/using/create-your-first-adaptive-form.md) serie. Si consiglia di seguire la serie in sequenza cronologica per comprendere, eseguire e illustrare il caso d’uso completo dell’esercitazione.

## Informazioni sull’esercitazione {#about-the-tutorial}

I moduli adattivi sono moduli di nuova generazione dinamici e reattivi. Puoi utilizzare i moduli adattivi per fornire esperienze personalizzate. È inoltre possibile integrare i moduli adattivi con [!DNL Adobe Analytics] per le statistiche di utilizzo e [!DNL Adobe Campaign] per la gestione delle campagne. Per ulteriori informazioni sulle funzionalità dei moduli adattivi, consulta [Introduzione alla creazione di moduli adattivi](/help/forms/using/introduction-forms-authoring.md).

È più facile creare e gestire i moduli seguendo un processo appropriato. In questo articolo viene illustrato come:

* [Creare un modulo adattivo che consenta a un cliente di aggiungere un indirizzo di spedizione](/help/forms/using/create-adaptive-form.md#step-create-the-adaptive-form)

* [Layout dei campi di un modulo adattivo per visualizzare e accettare le informazioni di un cliente](/help/forms/using/create-adaptive-form.md#step-add-header-and-footer)

* [Creare un’azione di invio per inviare un’e-mail contenente il contenuto del modulo](/help/forms/using/create-adaptive-form.md#step-add-components-to-capture-and-display-information)
* [Anteprima e invio di un modulo adattivo](/help/forms/using/create-adaptive-form.md)

Avrai un modulo simile al seguente alla fine dell’articolo:\
[![](do-not-localize/form-preview-mobile.gif)](do-not-localize/form-preview-mobile.gif)

## Passaggio 1: Creare il modulo adattivo {#step-create-the-adaptive-form}

1. Accedi all&#39;istanza di authoring AEM e passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms e documenti]**. L’URL predefinito è [http://localhost:4502/aem/forms.html/content/dam/formsanddocuments](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments).
1. Tocca **[!UICONTROL Crea]** e seleziona **[!UICONTROL Modulo adattivo]**. Viene visualizzata un’opzione per selezionare un modello. Tocca **[!UICONTROL Vuoto]** modello per selezionarlo e toccare **[!UICONTROL Successivo]**.

1. Opzione per **[!UICONTROL Aggiungi proprietà]** appare. La **[!UICONTROL Titolo]** e **[!UICONTROL Nome]** i campi sono obbligatori:

   * **Titolo:** Specifica `Add new or update shipping address` in **[!UICONTROL Titolo]** campo . Il campo titolo specifica il nome visualizzato del modulo. Il titolo consente di identificare il modulo nel AEM [!DNL Forms] interfaccia utente.
   * **Nome:** Specifica `shipping-address-add-update-form` in **[!UICONTROL Nome]** campo . Il campo Nome specifica il nome del modulo. Nel repository viene creato un nodo con il nome specificato. Quando si inizia a digitare un titolo, il valore del campo nome viene generato automaticamente. È possibile modificare il valore suggerito. Il campo name può includere solo caratteri alfanumerici, trattini e caratteri di sottolineatura. Tutti gli input non validi vengono sostituiti con un trattino.

1. Tocca **[!UICONTROL Crea]**. Viene creato un modulo adattivo e viene visualizzata una finestra di dialogo per aprire il modulo per la modifica. Tocca **[!UICONTROL Apri]** per aprire il modulo appena creato in una nuova scheda. Il modulo viene aperto per la modifica. Visualizza inoltre la barra laterale per personalizzare il modulo appena creato in base alle esigenze.

   Per informazioni sull’interfaccia per la creazione di moduli adattivi e sui componenti disponibili, consulta [Introduzione alla creazione di moduli adattivi](/help/forms/using/creating-adaptive-form.md).

   ![modulo adattivo appena creato](assets/newly-created-adaptive-form.png)

## Passaggio 2: Aggiungi intestazione e piè di pagina {#step-add-header-and-footer}

AEM [!DNL Forms] fornisce molti componenti per visualizzare informazioni su un modulo adattivo. I componenti Intestazione e Piè di pagina forniscono un aspetto e un aspetto uniformi del modulo. Un&#39;intestazione include in genere il logo di una società, il titolo del modulo e il riepilogo. In genere, un piè di pagina include informazioni sul copyright e collegamenti ad altre pagine.

1. Tocca ![pannello laterale di attivazione](assets/toggle-side-panel.png) > ![treeexpandall](assets/treeexpandall.png). Viene visualizzato il browser Componenti. Trascina **[!UICONTROL Intestazione]** dal browser Componenti al modulo adattivo.
1. Tocca **[!UICONTROL Logo]**. Viene visualizzata la barra degli strumenti. Tocca ![aem_6_3_edit](assets/aem_6_3_edit.png) sulla barra degli strumenti, digita **We.Retail**, e tocca ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

1. Tocca Immagine . Viene visualizzata la barra degli strumenti. Tocca ![cmppr](assets/cmppr.png). Il browser delle proprietà si apre a sinistra dello schermo. **[!UICONTROL Sfoglia]** e carica l&#39;immagine del logo. Tocca ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). L&#39;immagine viene visualizzata nell&#39;intestazione.

   Tocca Ottieni file per scaricare il logo utilizzato in questo articolo, se non ne hai uno.

[Ottieni file](assets/logo.png)

1. Trascina **[!UICONTROL Piè di pagina]** componente da ![treeexpandall](assets/treeexpandall.png) al modulo adattivo. A questo punto, il modulo si presenta come segue:

   ![adattivo-form-with-headers-and-footers](assets/adaptive-form-with-headers-and-footers.png)

## Passaggio 3: Aggiungere componenti per acquisire e visualizzare informazioni {#step-add-components-to-capture-and-display-information}

I componenti sono blocchi predefiniti di un modulo adattivo. AEM [!DNL Forms] fornisce molti componenti per acquisire e visualizzare informazioni in un modulo adattivo. Puoi trascinare i componenti da ![treeexpandall](assets/treeexpandall.png) a un modulo. Per informazioni sui componenti disponibili e sulle funzionalità corrispondenti, consulta [Introduzione alla creazione di moduli adattivi](/help/forms/using/introduction-forms-authoring.md).

1. Trascina **[!UICONTROL Componente Casella numerica]** al modulo adattivo. Posizionarlo prima del componente piè di pagina. Apri proprietà del componente, modifica **[!UICONTROL Titolo]** del componente **`Customer ID`**, modifica **[!UICONTROL Nome elemento]** a **`customer_ID`**, abilita **[!UICONTROL Campo obbligatorio]** abilita **[!UICONTROL Usa tipo di input numero HTML5]** e tocca ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
1. Trascina tre componenti Casella di testo nel modulo adattivo. Posizionare questi elementi prima del componente piè di pagina. Impostare le seguenti proprietà per queste caselle di testo.:

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

1. Trascina un **[!UICONTROL Casella numerica]** prima del componente piè di pagina. Apri le proprietà del componente, imposta i valori elencati nella tabella seguente, Tocca ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Proprietà | Valore |
   |---|---|
   | Titolo | CAP |
   | Nome elemento | customer_ZIPCode |
   | Numero massimo di cifre | 6 |
   | Campo obbligatorio | Abilitato |
   | Tipo di pattern di visualizzazione | Nessun pattern |

1. Trascina un **[!UICONTROL E-mail]** prima del componente piè di pagina. Apri le proprietà del componente, imposta i valori elencati nella tabella seguente e tocca ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Proprietà | Valore |
   |---|---|
   | Titolo | E-mail |
   | Nome elemento | customer_Email |
   | Campo obbligatorio | Abilitato |

1. Trascina un **[!UICONTROL File allegato]** prima del componente piè di pagina. Apri le proprietà del componente, imposta i valori elencati nella tabella seguente e tocca ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>Proprietà</b></td> 
      <td><b>Valore</b></td> 
     </tr> 
     <tr> 
      <td>Titolo</td> 
      <td>Documento d'indirizzo approvato dal governo<br /> </td> 
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

1. Trascina un **[!UICONTROL Pulsante Invia]** al modulo adattivo. Posizionarlo prima del componente piè di pagina. Apri le proprietà del componente, modifica Nome elemento in `address_addition_update_submit`, tocca ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). Il layout del modulo è completo e il modulo ha un aspetto simile al seguente:

   ![adattivo-form-with-all-the-components](assets/adaptive-form-with-all-the-components.png)

## Passaggio 4: Configurare l’azione di invio per il modulo adattivo {#step-configure-submit-action-for-the-adaptive-form}

Un’azione di invio viene attivata quando un utente tocca il pulsante Invia su un modulo adattivo. È possibile utilizzare un’azione di invio per salvare i dati del modulo nell’archivio locale, inviare i dati del modulo a un endpoint REST, inviare i dati del modulo come e-mail e altro ancora. Nei moduli adattivi sono disponibili alcune azioni di invio predefinite. Per informazioni dettagliate, consulta [Configurazione dell’azione Invia](/help/forms/using/configuring-submit-actions.md).

Utilizzando i passaggi seguenti, è possibile configurare l’azione di invio per e-mail e l’azione di invio demo del modulo:

1. Configura il server e-mail. Per maggiori dettagli, vedi [Configurazione della notifica e-mail](/help/sites-administering/notification.md).


1. Tocca **[!UICONTROL Contenitore modulo]** nel browser Contenuto e tocca ![cmppr](assets/cmppr.png). Il browser delle proprietà si apre a sinistra.
1. Vai a **[!UICONTROL Invio]** >  **[!UICONTROL Invia azione]**. Seleziona **[!UICONTROL Invia e-mail]**. Specifica i seguenti valori e tocca ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Proprietà | Valore |
   |--- |--- |
   | Da | `donotreply@weretail.com` |
   | A | `${customer_Email}` |
   | Oggetto | Riconoscimento: Hai aggiunto l&#39;indirizzo di spedizione sul sito web We.Retail. |
   | Modello e-mail | Ciao `${customer_Name}`, viene aggiunto il seguente indirizzo come indirizzo di spedizione per il tuo account: <br>`${customer_Name}`, `${customer_Shipping_Address}`, `${customer_State}`, `${customer_ZIPCode}`<br> Considerazioni, We.Retail |
   | Includi allegati | Abilitato |

   Il modulo è pronto. Ora è possibile visualizzare in anteprima il modulo e verificare la funzionalità. Se si è utilizzato il nome menzionato nell’esercitazione e si accede al modulo sul computer che esegue AEM [!DNL Forms] server, quindi il modulo è disponibile in [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html).

## Passaggio 5: Anteprima e invio del modulo adattivo {#step-preview-and-submit-the-adaptive-form}

È possibile utilizzare **[!UICONTROL Opzione Anteprima]** per valutare l’aspetto e il comportamento di un modulo. È possibile inviare un modulo in modalità di anteprima e controllare anche le convalide applicate a un modulo. Ad esempio, se viene visualizzato un errore quando un campo obbligatorio viene lasciato vuoto.

I moduli adattivi forniscono anche un’opzione per emulare l’esperienza di un modulo per diversi dispositivi. Ad esempio, iPhone, iPad e Desktop. Puoi utilizzare entrambi **[!UICONTROL Anteprima]** e **[!UICONTROL Emulatore]** ![righello](assets/ruler.png) opzioni in combinazione tra di loro per visualizzare in anteprima un modulo per dispositivi con diverse dimensioni dello schermo.

1. Tocca **[!UICONTROL Anteprima]** sul lato destro dell’editor moduli. Il modulo viene aperto in modalità anteprima. Se hai utilizzato il nome menzionato nell’esercitazione, l’URL di anteprima del modulo è [http://localhost:4502/content/dam/formsanddocuments/shipping-address-add-update-form/jcr:content?wcmmode=disabled](http://localhost:4502/content/dam/formsanddocuments/shipping-address-addition-updation-form/jcr:content?wcmmode=disabled)
1. Utilizzo ![righello](assets/ruler.png) per visualizzare l’aspetto del modulo su vari dispositivi.
1. Compila i campi del modulo e tocca **[!UICONTROL Invia]**. Il modulo viene inviato e l’utente viene reindirizzato all’impostazione predefinita **Grazie** pagina. Puoi anche specificare una pagina di ringraziamento personalizzata. Per maggiori dettagli, vedi [Configurazione della pagina di reindirizzamento](/help/forms/using/configuring-redirect-page.md).

Il modulo adattivo per aggiungere un indirizzo è pronto. Se si è utilizzato il nome indicato nell&#39;esercitazione e si accede al modulo sul computer che esegue il server AEM Forms, il modulo è disponibile in [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html).
