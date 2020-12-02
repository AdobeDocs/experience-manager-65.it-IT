---
title: 'Stile del modulo adattivo '
seo-title: 'Stile del modulo adattivo '
description: 'Scoprite come creare un tema personalizzato, personalizzare lo stile dei singoli componenti e utilizzare i font Web in un tema '
seo-description: 'Scoprite come creare un tema personalizzato, personalizzare lo stile dei singoli componenti e utilizzare i font Web in un tema '
page-status-flag: de-activated
uuid: ffb2cc22-baaf-4525-a2e3-29f39271c670
topic-tags: introduction
discoiquuid: 655303a4-99bb-4ba3-9d50-a178f5edcf85
translation-type: tm+mt
source-git-commit: 263a25b70fe4a3e7de65b47f07932d2e5f3d0197
workflow-type: tm+mt
source-wordcount: '2057'
ht-degree: 8%

---


# Stile del modulo adattivo {#do-not-publish-style-your-adaptive-form}

Scoprite come creare un tema personalizzato, personalizzare lo stile dei singoli componenti e utilizzare i font Web in un tema

![](do-not-localize/08-style_your_adaptiveformmain.png)

Questa esercitazione è un passaggio della serie [Crea il tuo primo modulo adattivo](https://helpx.adobe.com/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html). Si consiglia di seguire le serie in sequenza cronologica per comprendere, eseguire e dimostrare l&#39;uso completo dell&#39;esercitazione.

## Informazioni sull&#39;esercitazione {#about-the-tutorial}

È possibile utilizzare i temi per fornire un aspetto e uno stile univoci a un modulo adattivo. È possibile applicare temi out-of-box forniti con l&#39;editor di moduli adattivi o creare temi personalizzati. AEM [!DNL Forms] fornire un [editor di temi](https://helpx.adobe.com/experience-manager/6-3/forms/using/themes.html) per creare temi personalizzati. Un singolo tema può fornire un aspetto diverso allo stesso modulo adattivo aperto su dispositivi mobili, tablet o desktop. Qualsiasi conoscenza precedente di CSS o LESS non è necessaria per utilizzare l&#39;editor di temi, ma è desiderato.

Al termine dell&#39;esercitazione, imparerete a:

* Applicazione di un tema out-of-box a un modulo adattivo
* Creare un tema per un modulo adattivo utilizzando l&#39;editor di temi
* Stile di singoli componenti
* Sezione Bonus: Utilizzo di font Web in un tema personalizzato

Dopo aver completato l&#39;esercitazione, il modulo avrà un aspetto simile al seguente:

![Modulo con tema personalizzato](assets/styled-adaptive-form.png)

## Prima di iniziare {#before-you-start}

Scaricate nel computer locale le immagini in stile di intestazione e logo riportate di seguito. L&#39;intestazione del modulo `shipping-address-add-update-form` adattivo utilizza le immagini in stile di intestazione e logo. L’immagine in stile intestazione viene visualizzata sul lato destro dell’intestazione.

[Ottieni file](assets/header-style.png)

[Ottieni file](assets/logo-1.png)

## Passaggio 1: Applicare un tema al modulo adattivo {#step-apply-a-theme-to-your-adaptive-form}

L&#39;editor di moduli adattivi offre diversi temi out-of-the-box. Se non si intende utilizzare uno stile personalizzato per il modulo adattivo, è anche possibile pubblicare i moduli adattivi con un tema out-of-the-box. I temi sono indipendenti dai moduli adattivi. È possibile applicare lo stesso tema a più moduli adattivi. Per applicare un tema a un modulo adattivo:

1. Aprire il modulo adattivo per la modifica.

   [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

1. Aprire le proprietà di **[!UICONTROL Contenitore modulo adattivo]**. Nel browser delle proprietà, passare a **[!UICONTROL Base]** > **[!UICONTROL Tema modulo adattivo]**. Il campo **[!UICONTROL Tema modulo adattivo]** elenca tutti i temi predefiniti e personalizzati. Per impostazione predefinita, viene applicato il tema Canvas.
1. Selezionare un tema dal campo **[!UICONTROL Tema modulo adattivo]**. Ad esempio, **Tema sondaggio**. Toccate ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) per applicare il tema selezionato.

   ![Modulo adattivo con tema predefinito](assets/default-adaptive-form.png)

   **Figura:Modulo** *adattivo con tema predefinito*

   ![Modulo adattivo con il tema del sondaggio](assets/adaptive-form-with-survey-theme.png)

   **Figura:Modulo** *adattivo con il tema del sondaggio*

## Passaggio 2: Aggiornare il modulo adattivo {#step-update-your-adaptive-form}

La struttura visualizzata sopra richiede modifiche nel testo segnaposto e nel logo del modulo adattivo esistente. Effettuate le seguenti operazioni per apportare le modifiche richieste:

1. Modificate il logo e il testo esistenti dell’intestazione. Per rimuovere il logo:

   1. Aprire il modulo nell&#39;editor del modulo.

      [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

   1. Toccate l&#39;immagine del logo nel componente [!UICONTROL header] e toccate ![cmppr](assets/cmppr.png) **[!UICONTROL properties]**. Nella proprietà [!UICONTROL image], toccate X per rimuovere l&#39;immagine del logo esistente.
   1. Toccate **[!UICONTROL upload]**, selezionate il logo.png, quindi toccate ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) per salvare le modifiche. L&#39;immagine è stata scaricata nella sezione [Prima di iniziare](/help/forms/using/style-your-adaptive-form.md#before-you-start).
   1. Toccate il testo dell&#39;intestazione, `We.Retail`, quindi toccate ![aem_6_3_edit](assets/aem_6_3_edit.png) **[!UICONTROL edit]**. Cambia il testo dell&#39;intestazione in `we retail`. Applica la formattazione in grassetto solo a `we`in `we retail`.

      ![we-retail-logo-text](assets/we-retail-logo-text.png)

1. Rimuovete il titolo e aggiungete il testo segnaposto:

   1. Toccate il campo ID cliente e toccate le proprietà ![cmppr](assets/cmppr.png).
   1. Copiare il contenuto del campo **[!UICONTROL Titolo]** nel campo **[!UICONTROL Testo segnaposto]**.
   1. Eliminate il contenuto del campo **[!UICONTROL Titolo]** e toccate ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
   1. Ripetere i tre passaggi precedenti per tutte le caselle di testo, le caselle numeriche e i campi e-mail del modulo.

      ![aggiornato-adattivo-modulo](assets/updated-adaptive-form.png)

## Passaggio 3: Creare un tema personalizzato per il modulo adattivo {#step-create-a-custom-theme-for-your-adaptive-form}

È possibile utilizzare [editor di temi](/help/forms/using/themes.md) per creare temi personalizzati. L&#39;editor di temi è un potente editor WYSIWYG. È un metodo visivo per applicare CSS a vari componenti di un modulo adattivo. Fornisce controlli più precisi per lo stile dei componenti e dei pannelli di un modulo adattivo.

Un tema è un&#39;entità separata come i moduli adattivi. Contiene stili (CSS) per i componenti e i pannelli di un modulo adattivo. Gli stili includono proprietà CSS quali i colori di sfondo, i colori dello stato, la trasparenza, l&#39;allineamento e le dimensioni. Quando si applica un tema, lo stile specificato viene applicato ai componenti corrispondenti di un modulo adattivo.

In questa esercitazione verranno formattati intestazione e piè di pagina, componenti di testo e numerici, componenti allegati e pulsanti. Cominciamo con la creazione di un tema:

### Creare un tema {#create-a-theme}

1. Accedete all&#39;istanza di authoring AEM e andate a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Temi]**. L&#39;URL predefinito è [http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes).
1. Toccate **[!UICONTROL Crea]** e selezionate **[!UICONTROL Tema]**. Viene visualizzata la pagina [!UICONTROL Create Theme] con i campi necessari per creare un tema. I campi **[!UICONTROL Title]** e **[!UICONTROL Name]** sono obbligatori:

   * **Titolo:** specificate un titolo del tema. Ad esempio, **Tema globale.** Il titolo consente di identificare il tema dall’elenco dei temi.
   * **Nome:** specificate il nome del tema. Ad esempio, **Tema globale.** Nella directory archivio viene creato un nodo con il nome specificato. Quando si inizia a digitare un titolo, viene automaticamente generato il valore relativo al campo del nome. È possibile modificare il valore suggerito. Il campo del nome può includere solo caratteri alfanumerici, trattini e caratteri di sottolineatura. Tutti gli input non validi vengono sostituiti con un trattino.

1. Toccate **[!UICONTROL Crea]**. Viene creato un tema e viene visualizzata una finestra di dialogo per aprire il modulo per la modifica. Toccate **[!UICONTROL Apri]** per aprire il tema appena creato in una nuova scheda. Il tema si apre nell&#39;editor di temi. Per lo stile, l&#39;editor di temi utilizza un modulo adattivo fornito con AEM [!DNL Forms].

   Per informazioni sull&#39;utilizzo dell&#39;interfaccia utente dell&#39;editor di temi, vedere [Informazioni sull&#39;editor di temi](/help/forms/using/themes.md#aboutthethemeeditor).

1. Toccate **[!UICONTROL Opzioni tema]** ![opzioni tema](assets/theme-options.png) > **[!UICONTROL Configura]**. Nel campo **[!UICONTROL Modulo di anteprima]**, selezionare il modulo adattivo **shipping-address-add-update-form**, toccare ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png), toccare **[!UICONTROL Save]**. Ora, l&#39;editor di temi è configurato per utilizzare un modulo adattivo personalizzato invece del modulo adattivo predefinito. Toccate **[!UICONTROL Annulla]** per tornare all&#39;editor di temi.

   ![tema personalizzato](assets/custom-theme.png)

   **Figura:Editor** *tema con il modulo adattivo shipping-address-add-update-form*

   ![create-a-tema](assets/create-a-theme.png)

   **Figura:Modulo** *adattivo con il modulo predefinito*

### Intestazione e piè di pagina dello stile {#style-header-and-footer}

Intestazione e piè di pagina forniscono un aspetto coerente e distintivo a un modulo adattivo. In genere, l&#39;intestazione contiene il logo e il nome dell&#39;organizzazione, il piè di pagina contiene le informazioni sul copyright e questi rimangono identici in più forme di un&#39;organizzazione. Per formattare l’intestazione e il piè di pagina del modulo adattivo per l’indirizzo di spedizione-add-update-form:

1. Spostatevi sull&#39;opzione **[!UICONTROL Header]** > **[!UICONTROL Text]** nel pannello Selettori. Il pannello Selettori si trova a sinistra dell’editor di temi. Se il pannello non è visibile, toccate il pulsante ![per attivare/disattivare il pannello laterale](assets/toggle-side-panel.png).

1. Impostate le seguenti proprietà nell&#39;**[!UICONTROL Text]** Accordion e toccate ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Proprietà | Valore |
   |---|---|
   | Famiglia font | Arial |
   | Colore font | FFFFFF |
   | Dimensione font | 54 px |

1. Toccate il widget [!UICONTROL header] e toccate **[!UICONTROL Header]**. Le opzioni per lo stile del widget Intestazione sono visualizzate a sinistra. Espandete il pannello **[!UICONTROL Dimension e posizione]**, impostate l&#39;opzione **[!UICONTROL Altezza]** su `120px` e toccate ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
1. Espandere la struttura **[!UICONTROL Sfondo]** del widget di intestazione, impostare **[!UICONTROL Colore di sfondo]** su `F6921E.`

   Passa il cursore del mouse su **[!UICONTROL Immagine e sfumatura]** > **[!UICONTROL + Aggiungi]**, tocca **[!UICONTROL Immagine]**. Impostate le seguenti proprietà e toccate ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | Proprietà | Valore |
   |---|---|
   | immagine | Caricate il file header-style.png. L&#39;immagine è stata scaricata nella sezione [Prima di iniziare](/help/forms/using/style-your-adaptive-form.md#before-you-start). |
   | Posizione | A destra in basso |
   | Divisione in porzioni | Nessuna ripetizione |

1. Nell&#39;editor di temi, toccate il logo nell&#39;intestazione e toccate **[!UICONTROL Logo intestazione]**. Espandete il pannello di controllo Dimension e posizione, impostate le seguenti proprietà e toccate ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>immagine</b></td> 
      <td><b>Valore</b></td> 
     </tr> 
     <tr> 
      <td>immagine</td> 
      <td> 
       <ul> 
        <li>In alto: 1,5 rem</li> 
        <li>In basso: -35 px</li> 
        <li>A sinistra: 1rem<strong><br /> </strong></li> 
       </ul> <p><strong>Suggerimento: </strong> toccate l’icona del  <img src="assets/link.png"> collegamento per fornire un valore diverso a ciascun campo.<br /> </p> </td> 
     </tr> 
     <tr> 
      <td>Altezza</td> 
      <td>4,75 rem</td> 
     </tr> 
    </tbody> 
   </table>

1. Toccate il widget piè di pagina e toccate **[!UICONTROL Piè di pagina]**. Espandete il **[!UICONTROL Sfondo]**, impostate il **[!UICONTROL Colore di sfondo]** su `F6921E` e toccate ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

### Applicare uno stile al componente di acquisizione dei dati e uno sfondo al modulo adattivo {#style-the-data-capture-component-and-apply-a-background-to-the-adaptive-form}

È possibile utilizzare più componenti in un modulo adattivo per acquisire i dati. Ad esempio, casella di testo e casella numerica. È possibile fornire uno stile identico a tutti i componenti di acquisizione dati o uno stile separato per ciascun componente. In questa esercitazione, uno stile identico viene applicato alle caselle numeriche (ID cliente, CAP) e alle caselle di testo (ID cliente, Nome, Indirizzo spedizione, Stato, E-mail). Per formattare i componenti di acquisizione dati:

1. Toccate il campo **[!UICONTROL ID cliente]** e toccate l&#39;opzione **[!UICONTROL Widget campo]**. Impostate le seguenti proprietà e toccate ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>Pannello a soffietto</b></td> 
      <td><b>Proprietà</b></td> 
      <td><b>Valore</b></td> 
     </tr> 
     <tr> 
      <td>Bordo</td> 
      <td>Colore bordo</td> 
      <td>A7A9AC</td> 
     </tr> 
     <tr> 
      <td>Bordo</td> 
      <td>Raggio bordo </td> 
      <td> 
       <ul> 
        <li>In alto: 7px<br /> </li> 
        <li>Destra: 7px<br /> </li> 
        <li>In basso: 7px<br /> </li> 
        <li>A sinistra: 7px<br /> </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>Testo</td> 
      <td>Famiglia font</td> 
      <td>Arial</td> 
     </tr> 
     <tr> 
      <td>Testo</td> 
      <td>Colore font</td> 
      <td>939598<br /> </td> 
     </tr> 
     <tr> 
      <td>Testo</td> 
      <td>Dimensione font</td> 
      <td>18 px</td> 
     </tr> 
     <tr> 
      <td>Dimension e posizione</td> 
      <td>Larghezza</td> 
      <td>60%</td> 
     </tr> 
     <tr> 
      <td>Dimension e posizione</td> 
      <td>immagine</td> 
      <td> 
       <ul> 
        <li>A sinistra: 10 rem</li> 
       </ul> </td> 
     </tr> 
    </tbody> 
    </table>

1. Toccate l&#39;area vuota sopra il campo **[!UICONTROL ID cliente]** e toccate **[!UICONTROL Contenitore pannello reattivo]**. Impostate **[!UICONTROL Background]** > **[!UICONTROL Background Color]** su F1F2F2. Toccate ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   ![](do-not-localize/responsive-panel-container.png)

### Stile dei pulsanti {#style-the-buttons}

È possibile utilizzare un tema personalizzato per applicare uno stile identico a tutti i pulsanti del modulo adattivo e [stile in linea](/help/forms/using/inline-style-adaptive-forms.md) per applicare uno stile a un pulsante specifico. Per formattare i pulsanti:

1. Toccate il pulsante **[!UICONTROL Invia]** e toccate l&#39;opzione **[!UICONTROL Pulsante]**. Impostate le seguenti proprietà e toccate ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>Pannello a soffietto</b></td> 
      <td><b>Proprietà</b></td> 
      <td><b>Valore</b></td> 
     </tr> 
     <tr> 
      <td>Sfondo</td> 
      <td>Colore di sfondo</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>Bordo<br /> </td> 
      <td>Colore bordo</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>Bordo</td> 
      <td>Raggio bordo </td> 
      <td> 
       <ul> 
        <li>In alto: 7px<br /> </li> 
        <li>Destra: 7px<br /> </li> 
        <li>In basso: 7px<br /> </li> 
        <li>A sinistra: 7 px</li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>Testo<br /> </td> 
      <td>Famiglia font</td> 
      <td>Arial</td> 
     </tr> 
     <tr> 
      <td>Testo</td> 
      <td>Colore font</td> 
      <td>FFFFFF</td> 
     </tr> 
     <tr> 
      <td>Testo</td> 
      <td>Dimensione font</td> 
      <td>18 px</td> 
     </tr> 
    </tbody> 
   </table>

1. [Applicare il tema](/help/forms/using/style-your-adaptive-form.md#step-apply-a-theme-to-your-adaptive-form) personalizzato Tema globale al modulo adattivo. Se lo stile non si riflette sul modulo adattivo, cancellare la cache del browser e riprovare.

   ![style-data-capture-components](assets/style-data-capture-components.png)

## Passaggio 4: Stile di singoli componenti {#step-style-individual-components}

Alcuni stili si applicano solo a un componente specifico. Tali componenti sono formattati nell’editor di moduli adattivi.

1. Aprire il modulo adattivo per la modifica. [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)
1. Nella barra superiore, selezionare l&#39;opzione **[!UICONTROL Stile]**.

   ![style-option](assets/style-option.png)

1. Toccate il pulsante **[!UICONTROL Allega]** e toccate l&#39;icona ![aem_6_3_edit](assets/aem_6_3_edit.png). Impostare le seguenti proprietà in **[!UICONTROL Dimension e Posizione]** Accordion:

   | Proprietà | Valore |
   |---|---|
   | Mobile | Sinistra |
   | Larghezza | 10% |

1. Toccate l&#39;opzione **[!UICONTROL Correzione dell&#39;indirizzo approvata dal governo]** e toccate l&#39;icona ![aem_6_3_edit](assets/aem_6_3_edit.png). Impostate le seguenti proprietà:

   <table> 
    <tbody> 
     <tr> 
      <td><b>Pannello a soffietto</b></td> 
      <td><b>Proprietà</b></td> 
      <td><b>Valore</b></td> 
     </tr> 
     <tr> 
      <td>Dimensioni e posizione</td> 
      <td>Mobile</td> 
      <td>Sinistra</td> 
     </tr> 
     <tr> 
      <td>Dimensioni e posizione</td> 
      <td>Larghezza</td> 
      <td>73%</td> 
     </tr> 
     <tr> 
      <td>Dimensioni e posizione</td> 
      <td>Riempimento</td> 
      <td> 
       <ul> 
        <li>A sinistra: 10 px</li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>Dimensioni e posizione</td> 
      <td>Altezza</td> 
      <td>40 px</td> 
     </tr> 
     <tr> 
      <td>Dimensioni e posizione<br /> </td> 
      <td>immagine</td> 
      <td><br /> 
       <ul> 
        <li>Destra: 2rem</li> 
        <li>A sinistra: 10 rem </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>Sfondo</td> 
      <td>Colore di sfondo</td> 
      <td>FFFFFF</td> 
     </tr> 
     <tr> 
      <td>Bordo</td> 
      <td>Spessore bordo</td> 
      <td>1 px</td> 
     </tr> 
     <tr> 
      <td>Bordo</td> 
      <td>Stile bordo</td> 
      <td>Uniforme</td> 
     </tr> 
     <tr> 
      <td>Bordo</td> 
      <td>Colore bordo</td> 
      <td>A7A9AC</td> 
     </tr> 
     <tr> 
      <td>Bordo</td> 
      <td>Raggio bordo</td> 
      <td>7 px</td> 
     </tr> 
     <tr> 
      <td>Testo</td> 
      <td>Famiglia font</td> 
      <td>Arial</td> 
     </tr> 
     <tr> 
      <td>Testo</td> 
      <td>Colore font</td> 
      <td>BCBEC0</td> 
     </tr> 
     <tr> 
      <td>Testo</td> 
      <td>Dimensione font</td> 
      <td>18 px</td> 
     </tr> 
     <tr> 
      <td>Testo</td> 
      <td>Altezza riga</td> 
      <td>2</td> 
     </tr> 
     </tr> 
    </tbody> 
   </table>

1. Toccate il pulsante **[!UICONTROL Invia]** e toccate l&#39;icona ![aem_6_3_edit](assets/aem_6_3_edit.png). Impostate le seguenti proprietà:

   <table> 
    <tbody> 
     <tr> 
      <td><b>Pannello a soffietto</b></td> 
      <td><b>Proprietà</b></td> 
      <td><b>Valore</b></td> 
     </tr> 
     <tr> 
      <td>Dimension e posizione</td> 
      <td>Mobile</td> 
      <td>Destra</td> 
     </tr> 
     <tr> 
      <td>Dimension e posizione</td> 
      <td>immagine</td> 
      <td> 
       <ul> 
        <li>In alto: 5rem</li> 
        <li>Destra: 14 rem</li> 
        <li>In basso: 20 px</li> 
        <li>A sinistra: 20px<br /> </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>Sfondo</td> 
      <td>Colore di sfondo</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>Bordo</td> 
      <td>Colore bordo</td> 
      <td>F6921E</td> 
     </tr> 
    </tbody> 
   </table>

   ![styled-adaptive-form-1](assets/styled-adaptive-form-1.png)

## Passaggio 5: Sezione Bonus: Utilizzo di font Web in un tema personalizzato {#step-bonus-section-using-web-fonts-in-a-custom-theme}

È possibile utilizzare vari font per progettare un modulo adattivo. Tutti i dispositivi su cui è visualizzato il modulo adattivo potrebbero non avere i font utilizzati per progettare il modulo adattivo. È possibile utilizzare un servizio di font Web per distribuire i font richiesti al dispositivo di destinazione.

[!DNL Adobe Fonts] è un servizio di font Web. È possibile configurare e utilizzare il servizio con moduli adattivi. Per utilizzare [!DNL Adobe Fonts] in un modulo adattivo:

>[!NOTE]
>
>![typekit-to-adobe-](assets/typekit-to-adobe-fonts.png) [!DNL Typekit] fontsis ora chiamato  Adobe Fonts ed è incluso con Creative Cloud e altre iscrizioni. [Per saperne di più](https://fonts.adobe.com/).

1. Create un account [ Adobe Fonts](https://typekit.com/), create un kit, aggiungete il font Myriad Pro al kit, pubblicate il kit e ottenete l&#39;ID kit. È necessario utilizzare [!DNL Adobe Fonts] (font Web) in un modulo adattivo.
1. Nel server AEM [!DNL Forms], andate a ![adobeexperience emanager](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Adobe Fonts]**. A questo punto, aprite una cartella di configurazione. Se una configurazione è già disponibile, fare clic sul pulsante **[!UICONTROL Crea]** per creare una nuova istanza.

   Nella finestra di dialogo Crea configurazione, specificate un **Titolo** per la configurazione e fate clic su **[!UICONTROL Crea]**. Viene nuovamente visualizzata la pagina di configurazione. Nella finestra di dialogo [!UICONTROL Modifica componente] visualizzata, fornire l&#39; **ID kit** e fare clic su **[!UICONTROL OK]**.

1. Configurate il tema per utilizzare la configurazione [!DNL Adobe Fonts]. Nell&#39;istanza di creazione, aprite **[!UICONTROL Tema globale]** nell&#39;editor di temi. Nell&#39;editor di temi, passare a **[!UICONTROL Opzioni tema]** ![opzioni tema](assets/theme-options.png) > **[!UICONTROL Configura]**. Nel campo **[!UICONTROL Adobe Fonts Configuration]**, selezionare il kit e fare clic su **[!UICONTROL Save]**.

   I font aggiunti al **[!UICONTROL Adobe Fonts]** sono disponibili per la selezione nel **[!UICONTROL Text]** pannello di controllo di tutti i componenti.

