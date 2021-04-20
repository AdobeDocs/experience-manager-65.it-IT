---
title: '"Esercitazione: Creare un modulo adattivo"'
seo-title: '"Creare un modulo adattivo"'
description: Scopri come creare, impostare il layout e visualizzare in anteprima un modulo adattivo. Inoltre, scopri come configurare le azioni di invio.
seo-description: Scopri come creare, impostare il layout e visualizzare in anteprima un modulo adattivo. Inoltre, scopri come configurare le azioni di invio.
page-status-flag: de-activated
uuid: 0010d274-a683-499e-9fa6-ce355d7898a0
discoiquuid: 55c08940-8c25-4938-8e49-25bce20aaf22
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1397'
ht-degree: 3%

---


# Esercitazione: Creare un modulo adattivo {#do-not-publish-tutorial-create-an-adaptive-form}

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

Questa esercitazione è un passaggio della serie [Crea il tuo primo modulo adattivo](/help/forms/using/create-your-first-adaptive-form.md) . Si consiglia di seguire la serie in sequenza cronologica per comprendere, eseguire e illustrare il caso d’uso completo dell’esercitazione.

## Informazioni sull&#39;esercitazione {#about-the-tutorial}

I moduli adattivi sono moduli di nuova generazione dinamici e reattivi. Puoi utilizzare i moduli adattivi per fornire esperienze personalizzate. È inoltre possibile integrare i moduli adattivi con [!DNL Adobe Analytics] per le statistiche di utilizzo e [!DNL Adobe Campaign] per la gestione delle campagne. Per ulteriori informazioni sulle funzionalità dei moduli adattivi, consulta [Introduzione alla creazione di moduli adattivi](/help/forms/using/introduction-forms-authoring.md).

È più facile creare e gestire i moduli seguendo un processo appropriato. In questo articolo viene illustrato come:

* [Creare un modulo adattivo che consenta a un cliente di aggiungere un indirizzo di spedizione](/help/forms/using/create-adaptive-form.md#step-create-the-adaptive-form)

* [Layout dei campi di un modulo adattivo per visualizzare e accettare le informazioni di un cliente](/help/forms/using/create-adaptive-form.md#step-add-header-and-footer)

* [Creare un’azione di invio per inviare un’e-mail contenente il contenuto del modulo](/help/forms/using/create-adaptive-form.md#step-add-components-to-capture-and-display-information)
* [Anteprima e invio di un modulo adattivo](/help/forms/using/create-adaptive-form.md)

Avrai un modulo simile al seguente alla fine dell’articolo:\
[![](do-not-localize/form-preview-mobile.gif)](do-not-localize/form-preview-mobile.gif)

## Passaggio 1: Crea il modulo adattivo {#step-create-the-adaptive-form}

1. Accedi all&#39;istanza di authoring AEM e passa a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**. L&#39;URL predefinito è [http://localhost:4502/aem/forms.html/content/dam/formsanddocuments](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments).
1. Tocca **[!UICONTROL Crea]** e seleziona **[!UICONTROL Modulo adattivo]**. Viene visualizzata un’opzione per selezionare un modello. Tocca il modello **[!UICONTROL Vuoto]** per selezionarlo e tocca **[!UICONTROL Avanti]**.

1. Viene visualizzata un&#39;opzione per **[!UICONTROL Aggiungi proprietà]**. I campi **[!UICONTROL Titolo]** e **[!UICONTROL Nome]** sono obbligatori:

   * **Titolo:** specifica  `Add new or update shipping address` nel campo  **** Titolo. Il campo titolo specifica il nome visualizzato del modulo. Il titolo consente di identificare il modulo nell’interfaccia utente AEM [!DNL Forms] .
   * **Nome:** specifica  `shipping-address-add-update-form` nel campo  **** Nome. Il campo Nome specifica il nome del modulo. Nel repository viene creato un nodo con il nome specificato. Quando si inizia a digitare un titolo, il valore del campo nome viene generato automaticamente. È possibile modificare il valore suggerito. Il campo name può includere solo caratteri alfanumerici, trattini e caratteri di sottolineatura. Tutti gli input non validi vengono sostituiti con un trattino.

1. Tocca **[!UICONTROL Crea]**. Viene creato un modulo adattivo e viene visualizzata una finestra di dialogo per aprire il modulo per la modifica. Tocca **[!UICONTROL Apri]** per aprire il modulo appena creato in una nuova scheda. Il modulo viene aperto per la modifica. Visualizza inoltre la barra laterale per personalizzare il modulo appena creato in base alle esigenze.

   Per informazioni sull’interfaccia per la creazione di moduli adattivi e sui componenti disponibili, consulta [Introduzione alla creazione di moduli adattivi](/help/forms/using/creating-adaptive-form.md).

   ![modulo adattivo appena creato](assets/newly-created-adaptive-form.png)

## Passaggio 2: Aggiungi intestazione e piè di pagina {#step-add-header-and-footer}

AEM [!DNL Forms] fornisce molti componenti per visualizzare informazioni su un modulo adattivo. I componenti Intestazione e Piè di pagina forniscono un aspetto e un aspetto uniformi del modulo. Un&#39;intestazione include in genere il logo di una società, il titolo del modulo e il riepilogo. In genere, un piè di pagina include informazioni sul copyright e collegamenti ad altre pagine.

1. Tocca ![interruttore-side-panel](assets/toggle-side-panel.png) > ![treeexpandall](assets/treeexpandall.png). Viene visualizzato il browser Componenti. Trascina il componente **[!UICONTROL Intestazione]** dal browser Componenti al modulo adattivo.
1. Tocca **[!UICONTROL Logo]**. Viene visualizzata la barra degli strumenti. Tocca ![aem_6_3_edit](assets/aem_6_3_edit.png) sulla barra degli strumenti, digita **We.Retail** e tocca ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

1. Tocca Immagine . Viene visualizzata la barra degli strumenti. Tocca ![cmppr](assets/cmppr.png). Il browser delle proprietà si apre a sinistra dello schermo. **** Naviga e carica l’immagine del logo. Tocca ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). L&#39;immagine viene visualizzata nell&#39;intestazione.

   Tocca Ottieni file per scaricare il logo utilizzato in questo articolo, se non ne hai uno.

   [Ottieni file](assets/logo.png)

1. Trascina il componente **[!UICONTROL Piè di pagina]** da ![espandi ad albero](assets/treeexpandall.png) al modulo adattivo. A questo punto, il modulo si presenta come segue:

   ![adattivo-form-with-headers-and-footers](assets/adaptive-form-with-headers-and-footers.png)

## Passaggio 3: Aggiungere componenti per acquisire e visualizzare informazioni {#step-add-components-to-capture-and-display-information}

I componenti sono blocchi predefiniti di un modulo adattivo. AEM [!DNL Forms] fornisce molti componenti per acquisire e visualizzare informazioni in un modulo adattivo. È possibile trascinare i componenti da ![ad albero](assets/treeexpandall.png) a un modulo. Per informazioni sui componenti disponibili e sulle funzionalità corrispondenti, consulta [Introduzione alla creazione di moduli adattivi](/help/forms/using/introduction-forms-authoring.md).

1. Trascina il **[!UICONTROL componente Casella numerica]** nel modulo adattivo. Posizionarlo prima del componente piè di pagina. Apri le proprietà del componente, cambia **[!UICONTROL Titolo]** del componente in **`Customer ID`**, cambia **[!UICONTROL Nome elemento]** in **`customer_ID`**, abilita l&#39;opzione **[!UICONTROL Campo richiesto]**, abilita l&#39;opzione **[!UICONTROL Usa tipo di input numero HTML5]** e tocca ![aem_6_3 _forms_save](assets/aem_6_3_forms_save.png).
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

1. Trascinare un componente **[!UICONTROL Casella numerica]** prima del componente piè di pagina. Apri le proprietà del componente, imposta i valori elencati nella tabella seguente, Tocca ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Proprietà | Valore |
   |---|---|
   | Titolo | CAP |
   | Nome elemento | customer_ZIPCode |
   | Numero massimo di cifre | 6 |
   | Campo obbligatorio | Abilitato |
   | Tipo di pattern di visualizzazione | Nessun pattern |

1. Trascina un componente **[!UICONTROL E-mail]** prima del componente piè di pagina. Apri le proprietà del componente, imposta i valori elencati nella tabella seguente e tocca ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Proprietà | Valore |
   |---|---|
   | Titolo | E-mail |
   | Nome elemento | customer_Email |
   | Campo obbligatorio | Abilitato |

1. Trascinare un componente **[!UICONTROL File allegato]** prima del componente piè di pagina. Apri le proprietà del componente, imposta i valori elencati nella tabella seguente e tocca ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>Proprietà</b></td> 
      <td><b>Valore</b></td> 
     </tr> 
     <tr> 
      <td>Titolo</td> 
      <td>Prova dell'indirizzo approvata governativa<br /> </td> 
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

1. Trascina un componente **[!UICONTROL Pulsante di invio]** nel modulo adattivo. Posizionarlo prima del componente piè di pagina. Apri le proprietà del componente, modifica Nome elemento in `address_addition_update_submit`, tocca ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). Il layout del modulo è completo e il modulo ha un aspetto simile al seguente:

   ![adattivo-form-with-all-the-components](assets/adaptive-form-with-all-the-components.png)

## Passaggio 4: Configurare l’azione di invio per il modulo adattivo {#step-configure-submit-action-for-the-adaptive-form}

Un’azione di invio viene attivata quando un utente tocca il pulsante Invia su un modulo adattivo. È possibile utilizzare un’azione di invio per salvare i dati del modulo nell’archivio locale, inviare i dati del modulo a un endpoint REST, inviare i dati del modulo come e-mail e altro ancora. Nei moduli adattivi sono disponibili alcune azioni di invio predefinite. Per informazioni dettagliate, consulta [Configurazione dell’azione Invia](/help/forms/using/configuring-submit-actions.md).

Utilizzando i passaggi seguenti, è possibile configurare l’azione di invio per e-mail e l’azione di invio demo del modulo:

1. Configura il server e-mail. Per informazioni dettagliate, consulta [Configurazione della notifica e-mail](/help/sites-administering/notification.md).


1. Tocca **[!UICONTROL Contenitore modulo]** nel browser Contenuto e tocca ![cmppr](assets/cmppr.png). Il browser delle proprietà si apre a sinistra.
1. Vai a **[!UICONTROL Invio]** > **[!UICONTROL Invia azione]**. Selezionare **[!UICONTROL Invia e-mail]**. Specifica i seguenti valori e tocca ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Proprietà | Valore |
   |--- |--- |
   | Da | `donotreply@weretail.com` |
   | A | `${customer_Email}` |
   | Oggetto | Riconoscimento: Hai aggiunto l&#39;indirizzo di spedizione sul sito web We.Retail. |
   | Modello e-mail | Ciao `${customer_Name}`, viene aggiunto il seguente indirizzo come indirizzo di spedizione per il tuo account: <br>`${customer_Name}`, `${customer_Shipping_Address}`, `${customer_State}`, `${customer_ZIPCode}`<br> Considerazioni, We.Retail |
   | Includi allegati | Abilitato |

   Il modulo è pronto. Ora è possibile visualizzare in anteprima il modulo e verificare la funzionalità. Se si è utilizzato il nome indicato nell&#39;esercitazione e si accede al modulo sul computer che esegue AEM server [!DNL Forms], il modulo è disponibile all&#39;indirizzo [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html).

## Passaggio 5: Anteprima e invio del modulo adattivo {#step-preview-and-submit-the-adaptive-form}

È possibile utilizzare l&#39;opzione **[!UICONTROL Anteprima]** per valutare l&#39;aspetto e il comportamento di un modulo. È possibile inviare un modulo in modalità di anteprima e controllare anche le convalide applicate a un modulo. Ad esempio, se viene visualizzato un errore quando un campo obbligatorio viene lasciato vuoto.

I moduli adattivi forniscono anche un’opzione per emulare l’esperienza di un modulo per diversi dispositivi. Ad esempio, iPhone, iPad e Desktop. È possibile utilizzare le opzioni **[!UICONTROL Anteprima]** e **[!UICONTROL Emulatore]** ![righer](assets/ruler.png) insieme per visualizzare un&#39;anteprima del modulo per dispositivi di diverse dimensioni dello schermo.

1. Toccare l’opzione **[!UICONTROL Anteprima]** sul lato destro dell’editor moduli. Il modulo viene aperto in modalità anteprima. Se hai usato il nome menzionato l’esercitazione, l’URL di anteprima del modulo è [http://localhost:4502/content/dam/formsanddocuments/shipping-address-add-update-form/jcr:content?wcmmode=disabled](http://localhost:4502/content/dam/formsanddocuments/shipping-address-addition-updation-form/jcr:content?wcmmode=disabled)
1. Utilizzare ![righello](assets/ruler.png) per visualizzare l&#39;aspetto del modulo su vari dispositivi.
1. Compila i campi del modulo e tocca **[!UICONTROL Invia]**. Il modulo viene inviato e viene reindirizzato alla pagina **Grazie** predefinita. Puoi anche specificare una pagina di ringraziamento personalizzata. Per informazioni dettagliate, consulta [Configurazione della pagina di reindirizzamento](/help/forms/using/configuring-redirect-page.md).

Il modulo adattivo per aggiungere un indirizzo è pronto. Se si è utilizzato il nome indicato nell&#39;esercitazione e si accede al modulo sul computer che esegue il server AEM Forms, il modulo è disponibile all&#39;indirizzo [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html).
