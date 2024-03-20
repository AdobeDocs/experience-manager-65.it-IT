---
title: Creare e configurare le pagine dell’Editor risorse
description: Scopri come creare pagine personalizzate dell’Editor risorse e modificare più risorse contemporaneamente.
contentOwner: AG
role: User, Admin
feature: Developer Tools,Asset Management
exl-id: 53e310a9-c511-447a-91bd-8c5b2760dc03
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2088'
ht-degree: 1%

---

# Creare e configurare le pagine dell’Editor risorse {#creating-and-configuring-asset-editor-pages}

Questo documento descrive quanto segue:

* Perché creare pagine personalizzate dell’Editor risorse.
* Come creare e personalizzare le pagine dell’Editor risorse, ovvero pagine WCM che consentono di visualizzare e modificare i metadati ed eseguire azioni sulla risorsa.
* Come modificare più risorse contemporaneamente.

<!-- TBD: Add UICONTROL tags. Need PM review. Flatten the structure a bit. Re-write to remove Geometrixx mentions and to adhere to 6.5 default samples. -->

>[!NOTE]
>
>Condivisione risorse è disponibile come implementazione di riferimento open-source. Consulta [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/). Non è ufficialmente supportato.

## Perché creare e configurare pagine dell’Editor risorse? {#why-create-and-configure-asset-editor-pages}

Digital Asset Management viene utilizzato in più scenari. Quando si passa da una soluzione su piccola scala per un piccolo gruppo di utenti con formazione professionale - ad esempio fotografi o tassonomisti - a gruppi di utenti più ampi e diversificati (ad esempio, utenti aziendali, autori WCM e giornalisti), la potente interfaccia utente di [!DNL Adobe Experience Manager Assets] può fornire troppe informazioni. Le parti interessate iniziano a richiedere interfacce utente o applicazioni specifiche per accedere alle risorse digitali che le riguardano.

Queste applicazioni incentrate sulle risorse possono essere semplici gallerie fotografiche in una rete Intranet in cui i dipendenti possono caricare foto dalle visite alle fiere o da un centro stampa in un sito web pubblico. Le applicazioni incentrate sulle risorse possono essere estese anche a soluzioni complete, inclusi carrelli, pagamento e processi di verifica.

La creazione di un’applicazione incentrata sulle risorse diventa un processo di configurazione che non richiede la codifica, ma solo la conoscenza dei gruppi di utenti e delle loro esigenze e la conoscenza dei metadati utilizzati. Applicazioni basate su risorse create con [!DNL Assets] sono estensibili: con un moderato sforzo di codifica, è possibile creare componenti riutilizzabili per la ricerca, la visualizzazione e la modifica delle risorse.

Applicazione incentrata sulle risorse in [!DNL Experience Manager] è costituita da una pagina Editor risorse, che può essere utilizzata per ottenere una visualizzazione dettagliata di una risorsa specifica. Una pagina Editor risorse consente inoltre di modificare i metadati, purché l’utente che accede alla risorsa disponga delle autorizzazioni necessarie.

<!--
## Create and configure an Asset Share page {#creating-and-configuring-an-asset-share-page}

You customize the DAM Finder functionality and create pages that have all the functionality you require, which are called Asset Share pages. To create an Asset Share page, you add the page using the Geometrixx Asset Share template and then you customize the actions users can perform on that page, determine how viewers see the assets, and decide how users can build their queries.

Here are some use cases for creating a customized Asset Share page:

* Press Center for Journalists.
* Image Search Engine for internal business users.
* Image Database for website users.
* Media Tagging Interface for metadata editors.

### Create an Asset Share page {#creating-an-asset-share-page}

To create an Asset Share page, you can either create it when you are working on web sites or from the digital asset manager.

>[!NOTE]
>
>By default, when you create an Asset Share page from **New** in the digital asset manager, an Asset viewer and Asset editor are automatically created for you.

To create an new Asset Share page in the **Websites** console:

1. In the **Websites** tab, navigate to the place where you want to create an asset share page and click **New**.

1. Select the **Asset Share** page and click **Create**. The new page is created and the asset share page is listed in the **Websites** tab.

![dam8](assets/dam8.png)

The basic page created using the Geometrixx DAM Asset Share template looks as follows:

![screen_shot_2012-04-18at115456am](assets/screen_shot_2012-04-18at115456am.png)

To customize your Asset Share page, you use elements from the sidekick and you also edit query builder properties. The page **Geometrixx Press Center** is a customized version of a page based on this template:

![screen_shot_2012-04-19at123048pm](assets/screen_shot_2012-04-19at123048pm.png)

To create an asset share page by way of the digital asset manager:

1. In the digital asset manager, in **New**, select **New Asset Share**.
1. In the **Title**, enter the name of the asset share page. If desired, enter a name for the URL.

   ![screen_shot_2012-04-19at23626pm](assets/screen_shot_2012-04-19at23626pm.png)

1. Double-click the asset share page to open it and configure the page.

   ![screen_shot_2012-04-19at24114pm](assets/screen_shot_2012-04-19at24114pm.png)

   By default, when you create an Asset Share page from **New**, an Asset viewer and Asset editor are automatically created for you.

#### Customize actions {#customizing-actions}

You can determine what actions users can perform on selected digital assets from a selection of predefined actions.

To add actions to the Asset Share page:

1. In the Asset Share page that you want to customize, click **Actions** in the sidekick.

The following actions are available:

 | Action | Description |
 |---|---|
 | [!UICONTROL Delete Action] | Users can delete the selected assets. |
 | [!UICONTROL Download Action] | Lets users download selected assets to their computers. |
 | [!UICONTROL Lightbox Action] | Saves assets to a "lightbox"   where you can perform other actions on them. This comes in handy when working   with assets across multiple pages. The lightbox can also be used as a   shopping cart for assets. |
 | [!UICONTROL Move Action] | Users can move the asset to another   location |
 | [!UICONTROL Tags Action] | Lets users add tags to selected assets |
 | [!UICONTROL View Asset Action] | Opens the asset in the Asset editor for   user manipulation. |

1. Drag the appropriate action to the **Actions** area on the page. Doing so creates a button that is used to execute that action.

![chlimage_1-159](assets/chlimage_1-387.png)

#### Determine how search results are presented {#determining-how-search-results-are-presented}

You determine how results are displayed from a predefined list of lenses.

To change how search results are viewed:

1. In the Asset Share page that you want to customize, click Search.

![chlimage_1](assets/assetshare3.png)

1. Drag the appropriate lens to the top center of the page. In the Press Center, the lenses are already available. Users press the appropriate lens icon to display search results as desired.

The following lenses are available:

| Lens | Description |
|---|---|
| **[!UICONTROL List Lens]** |Presents the assets in a list fashion with details. |
| **[!UICONTROL Mosaic Lens]** |Presents assets in a mosaic fashion. |

#### Mosaic Lens {#mosaic-lens}

![chlimage_1-160](assets/chlimage_1-388.png)

#### List Lens {#list-lens}

![chlimage_1-161](assets/chlimage_1-389.png)

#### Customize the Query Builder {#customizing-the-query-builder}

The query builder lets you enter search terms and create content for the Asset Share page. When you edit the query builder, you also get to determine how many search results are displayed per page, which asset editor opens when you double-click an asset, the path the query searches, and customizes nodetypes.

To customize the query builder:

1. In the Asset Share page that you want to customize, click **Edit** in the Query Builder. By default, the **General** tab opens.
1. Select the number of results per page, the path of the asset editor (if you have a customized asset editor) and the Actions title.

![screen_shot_2012-04-23at15055pm](assets/screen_shot_2012-04-23at15055pm.png)

1. Click the **Paths** tab. Enter a path or multiple paths that the search will run. These paths are overwritten if the user uses the Paths predicate.

![screen_shot_2012-04-23at15150pm](assets/screen_shot_2012-04-23at15150pm.png)

1. Enter another node type, if desired.

1. In the **Query Builder URL** field, you can override or wrap the query builder and enter the new servlet URLs with the existing query builder component. In the **Feed URL** field, you can override the Feed URL as well.

![screen_shot_2012-04-23at15313pm](assets/screen_shot_2012-04-23at15313pm.png)

1. In the **Text** field, enter the text you want to appear for results and page numbers of results. Click **OK** when finished making changes.

![screen_shot_2012-04-23at15300pm](assets/screen_shot_2012-04-23at15300pm.png)

#### Add predicates {#adding-predicates}

Experience Manager Assets includes several predicates that you can add to the Asset Share page. These let your users further narrow searches. In some cases, they may override a query builder parameter (for example, the Path parameter).

To add predicates:

1. In the Asset Share page that you want to customize, click **Search**.

![assetshare3](assets/assetshare3.png)

1. Drag the appropriate predicates to the Asset Share page underneath the query builder. Doing so creates the appropriate fields.

![assetshare4](assets/assetshare4.png)

The following predicates are available:

| Predicate | Description |
|---|---|
| **[!UICONTROL Date Predicate]** |Lets users search for assets that were modified before and after certain dates. |
| **[!UICONTROL Options Predicate]** |The site owner can specify a property to search for (as in the property predicate, for example, cq:tags) and a content tree to populate the options from (for example, the tag tree). Doing so generates a list of options where the users can select the values (tags) that the selected property (tag property) should have. This predicate lets you build list controls like the list of tags, file types, image orientations, and so on. It is great for a fixed set of options. |
| **[!UICONTROL Path Predicate]** |Lets users define the path and subfolders, if desired. |
| **[!UICONTROL Property Predicate]** |The site owner specifies a property to search for, for example, tiff:ImageLength and the user can then enter a value, for example, 800. This returns all images that are 800 pixels high. Useful predicate if your property can have arbitrary values. |

For more information, see the [predicate Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/package-summary.html).

1. To configure the predicate further, double-click it. For example, when you open the Path Predicate, you need to assign the root path.

![screen_shot_2012-04-23at15640pm](assets/screen_shot_2012-04-23at15640pm.png)
-->

## Creare e configurare una pagina Editor risorse {#creating-and-configuring-an-asset-editor-page}

Puoi personalizzare l’Editor risorse per determinare come gli utenti possono visualizzare e modificare le risorse digitali. A questo scopo, puoi creare una pagina Editor risorse e quindi personalizzare le visualizzazioni e le azioni che gli utenti possono eseguire su tale pagina.

>[!NOTE]
>
>Per aggiungere campi personalizzati all’Editor risorse DAM, aggiungi nuovo `cq:Widget` nodi a `/apps/dam/content/asseteditors.`

### Creare una pagina Editor risorse {#creating-the-asset-editor-page}

Quando si crea la pagina Editor risorse, è buona norma creare la pagina direttamente sotto la pagina Condivisione risorse.

Per creare una pagina Editor risorse:

1. In **[!UICONTROL Siti Web]** , passa alla posizione in cui desideri creare una pagina Editor risorse e fai clic su **Nuovo**.
1. Seleziona **Editor risorse Geometrixx** e fai clic su **Crea**. La nuova pagina viene creata e la pagina è elencata in **Siti Web** scheda.

![screen_shot_2012-04-23at15858pm](assets/screen_shot_2012-04-23at15858pm.png)

La pagina di base creata utilizzando il modello Editor risorse di Geometrixx ha il seguente aspetto:

![assetshare5](assets/assetshare5.png)

Per personalizzare la pagina Editor risorse, utilizza gli elementi della barra laterale. La pagina Editor risorse a cui si accede da **Centro stampa Geometrixx** è la versione personalizzata di una pagina basata su questo modello:

![assetshare6](assets/assetshare6.png)

#### Impostare un editor risorse da aprire da una pagina Condivisione risorse {#setting-which-asset-editor-opens-from-an-asset-share-page}

Dopo aver creato la pagina personalizzata dell’Editor risorse, accertati che quando fai doppio clic sulle risorse create con Condivisione risorse, queste vengano aperte nella pagina personalizzata dell’Editor.

Per impostare la pagina Editor risorse:

1. Nella pagina Condivisione risorse, fai clic su **Modifica** accanto al Generatore di query.

![screen_shot_2012-04-23at20123pm](assets/screen_shot_2012-04-23at20123pm.png)

1. Fai clic su **Generale** , se non è già selezionata.

1. In **Percorso dell’editor risorse** , immetti il percorso dell’Editor risorse in cui desideri aprire le risorse nella pagina Condivisione risorse e fai clic su **OK**.

![screen_shot_2012-04-23at21653pm](assets/screen_shot_2012-04-23at21653pm.png)

#### Aggiungere componenti Editor risorse {#adding-asset-editor-components}

Per determinare la funzionalità di un Editor risorse aggiungere componenti alla pagina.

Per aggiungere componenti Editor risorse:

1. Nella pagina Editor risorse da personalizzare, seleziona **Editor risorse** nella barra laterale. Vengono visualizzati tutti i componenti disponibili dell’Editor risorse.

>[!NOTE]
>
>Ciò che puoi personalizzare dipende dai componenti disponibili. Per abilitare i componenti, passa alla modalità Progettazione e seleziona i componenti da abilitare.

1. Trascina i componenti dalla barra laterale all’Editor risorse e apporta eventuali modifiche nelle finestre di dialogo dei componenti. I componenti sono descritti nella tabella seguente e descritti nelle istruzioni dettagliate riportate di seguito.

>[!NOTE]
>
>Durante la progettazione della pagina Editor risorse, puoi creare componenti di sola lettura o modificabili. Gli utenti sanno che un campo può essere modificato se in quel componente viene visualizzata l’immagine di una matita. Per impostazione predefinita, la maggior parte dei componenti è impostata come di sola lettura.

| Componente | Descrizione |
|---|---|
| **[!UICONTROL Modulo metadati] e [!UICONTROL Campo di testo metadati]** | Consente di aggiungere metadati aggiuntivi a una risorsa ed eseguire un’azione, ad esempio l’invio, su tale risorsa. |
| **[!UICONTROL Risorse secondarie]** | Consente di personalizzare le risorse secondarie. |
| **Tag** | Consente agli utenti di selezionare e aggiungere tag a una risorsa. |
| **[!UICONTROL Miniatura]** | Mostra una miniatura della risorsa, il nome del file e consente di aggiungere un testo alternativo. È possibile aggiungere azioni Editor risorse anche qui. |
| **[!UICONTROL Titolo]** | Visualizza il titolo della risorsa, che può essere personalizzato. |

![screen_shot_2012-04-23at22743pm](assets/screen_shot_2012-04-23at22743pm.png)

#### Modulo metadati e campo di testo - Configurazione del componente Visualizza metadati {#metadata-form-and-text-field-configuring-the-view-metadata-component}

Il modulo metadati è un modulo che include un’azione di inizio e di fine. Nel mezzo, immetti **Testo** campi. Consulta [Forms](/help/sites-authoring/default-components-foundation.md#form-component) per ulteriori informazioni sull&#39;utilizzo dei moduli.

1. Creare un’azione iniziale facendo clic su **Modifica** nell&#39;area Inizio del modulo. Se necessario, è possibile immettere il titolo di una casella. Per impostazione predefinita, il titolo della casella è **Metadati**. Selezionare la casella di controllo Convalida client se si desidera generare il codice client JavaScript per la convalida.

![screen_shot_2012-04-23at22911pm](assets/screen_shot_2012-04-23at22911pm.png)

1. Creare un’azione Fine facendo clic su **Modifica** nell&#39;area Fine del modulo. Ad esempio, potrebbe essere utile creare un’ **[!UICONTROL Invia]** per consentire agli utenti di inviare le modifiche ai metadati. Facoltativamente, puoi aggiungere una **Reimposta** che ripristina lo stato originale dei metadati.

![screen_shot_2012-04-23at23138pm](assets/screen_shot_2012-04-23at23138pm.png)

1. Tra le **Inizio modulo** e **Fine modulo**, trascinare i campi di testo dei metadati nel modulo. Gli utenti compilano i metadati in questi campi di testo, che possono inviare o completare un’altra azione su.

1. Fare doppio clic sul nome del campo, ad esempio **Titolo** per aprire il campo metadati e apportare modifiche. In **Generale** scheda di **Modifica componente** , puoi definire lo spazio dei nomi e l’etichetta e il tipo del campo, ad esempio: `dc:title`.

![screen_shot_2012-04-23at23305pm](assets/screen_shot_2012-04-23at23305pm.png)

Consulta [Personalizzazione ed estensione delle risorse](/help/assets/extending-assets.md) per informazioni sulla modifica degli spazi dei nomi disponibili nel modulo metadati,

1. Fai clic su **Vincoli** scheda. Qui puoi selezionare se un campo è obbligatorio e, se necessario, aggiungere eventuali vincoli.

![screen_shot_2012-04-23at23435pm](assets/screen_shot_2012-04-23at23435pm.png)

1. Fai clic su **Visualizzazione** scheda. Qui puoi immettere una nuova larghezza e un nuovo numero di righe per il campo metadati. Seleziona la **Campo di sola lettura** per consentire agli utenti di modificare i metadati.

![screen_shot_2012-04-23at23446pm](assets/screen_shot_2012-04-23at23446pm.png)

Di seguito è riportato un esempio di modulo Metadati con vari campi:

![metadati](assets/chlimage_1-390.png)

Nella pagina Editor risorse, gli utenti possono quindi immettere i valori nei campi di metadati (se sono modificabili) ed eseguire l’azione finale (ad esempio, l’invio delle modifiche).

#### Risorse secondarie {#sub-assets}

Il componente Risorse secondarie è il punto in cui puoi visualizzare e selezionare le risorse secondarie. È possibile determinare i nomi da visualizzare sotto [risorsa principale](/help/assets/assets.md#what-are-digital-assets) e risorse secondarie.

Fai doppio clic sul componente Risorse secondarie per aprire la finestra di dialogo Risorse secondarie in cui puoi modificare i titoli della risorsa principale e di eventuali risorse secondarie. I valori predefiniti vengono visualizzati sotto il campo corrispondente.

![screen_shot_2012-04-23at23907pm](assets/screen_shot_2012-04-23at23907pm.png)

Di seguito è riportato un esempio di componente Risorse secondarie popolato:

![screen_shot_2012-04-23at24442pm](assets/screen_shot_2012-04-23at24442pm.png)

Ad esempio, se selezioni una risorsa secondaria, osserva come il componente visualizza la pagina appropriata e il titolo della casella cambia da Risorse secondarie a Pari livello.

![screen_shot_2012-04-23at24552pm](assets/screen_shot_2012-04-23at24552pm.png)

#### Tag {#tags}

Il componente Tag è un componente in cui gli utenti possono assegnare tag esistenti a una risorsa, per facilitarne l’organizzazione e il recupero in un secondo momento. È possibile rendere questo componente di sola lettura, in modo che gli utenti non possano aggiungere tag, ma solo visualizzarli.

![screen_shot_2012-04-23at25031pm](assets/screen_shot_2012-04-23at25031pm.png)

Fai doppio clic sul componente Tag per aprire la finestra di dialogo Tag in cui puoi modificare il titolo da Tag, se necessario, e selezionare gli spazi dei nomi allocati. Per rendere modificabile questo campo, cancella **[!UICONTROL Nascondi modifica]** casella di controllo. Per impostazione predefinita, i tag sono modificabili.

![screen_shot_2012-04-23at24731pm](assets/screen_shot_2012-04-23at24731pm.png)

Se gli utenti possono modificare i tag, possono fare clic sulla matita per aggiungere i tag selezionandoli dal menu a discesa Tag.

![screen_shot_2012-04-23at25150pm](assets/screen_shot_2012-04-23at25150pm.png)

Di seguito è riportato un componente Tag popolato:

![screen_shot_2012-04-23at25244pm](assets/screen_shot_2012-04-23at25244pm.png)

#### Miniatura  {#thumbnail}

Il componente Miniatura è il punto in cui la risorsa visualizza la miniatura selezionata (per molti dei formati la miniatura viene estratta automaticamente). Inoltre, il componente visualizza il nome del file e [azioni che è possibile modificare](/help/assets/assets-finder-editor.md#adding-asset-editor-actions).

![screen_shot_2012-04-23at25452pm](assets/screen_shot_2012-04-23at25452pm.png)

Fai doppio clic sul componente miniatura per aprire la finestra di dialogo delle miniature in cui modificare il testo alternativo. Per impostazione predefinita, il testo alternativo della miniatura è **Fai clic per scaricare** risorsa.

![screen_shot_2012-04-23at25604pm](assets/screen_shot_2012-04-23at25604pm.png)

Di seguito è riportato un esempio di un componente Thumbnail popolato:

![screen_shot_2012-04-23at34815pm](assets/screen_shot_2012-04-23at34815pm.png)

#### Titolo {#title}

Il componente Titolo visualizza il titolo della risorsa e una descrizione.

Per impostazione predefinita, è in modalità di sola lettura, pertanto gli utenti non possono modificarla. Per renderlo modificabile, fai doppio clic sul componente e cancella il **Nascondi pulsante di modifica** casella di controllo. Inoltre, inserisci un titolo per più risorse.

![screen_shot_2012-04-23at35100pm](assets/screen_shot_2012-04-23at35100pm.png)

Se è possibile modificare il Titolo, è possibile aggiungere un titolo e una descrizione facendo clic sulla matita per aprire **Proprietà risorsa** finestra. Inoltre, puoi attivare e disattivare la risorsa selezionando la data e l’ora.

Durante la modifica di [!UICONTROL Titolo], gli utenti possono modificare **Titolo**, **Descrizione**, e immetti **On** e **Tempi di disattivazione** per attivare e disattivare la risorsa.

![screen_shot_2012-04-23at35241pm](assets/screen_shot_2012-04-23at35241pm.png)

Di seguito è riportato un esempio di un componente Titolo popolato:

![chlimage_1-164](assets/chlimage_1-392.png)

#### Aggiungere azioni dell’Editor risorse {#adding-asset-editor-actions}

È possibile determinare le azioni che gli utenti possono eseguire sulle risorse digitali selezionate da una selezione di azioni predefinite.

Per aggiungere azioni alla pagina Editor risorse:

1. Nella pagina Editor risorse da personalizzare fai clic su **Editor risorse** nella barra laterale.

![screen_shot_2012-04-23at35515pm](assets/screen_shot_2012-04-23at35515pm.png)

Sono disponibili le seguenti azioni:

| Azione | Descrizione |
|---|---|
| [!UICONTROL Download] | Consente agli utenti di scaricare le risorse selezionate sui propri computer. |
| [!UICONTROL Editor] | Consente agli utenti di modificare un’immagine (modifica interattiva) |
| [!UICONTROL Lightbox] | Salva le risorse in una &quot;lightbox&quot; in cui è possibile eseguire altre azioni. Questa funzione si rivela utile quando si lavora con risorse su più pagine. |
| [!UICONTROL Blocco] | Consente agli utenti di bloccare una risorsa. Questa funzionalità non è abilitata per impostazione predefinita e deve essere abilitata nell’elenco dei componenti. |
| [!UICONTROL Riferimenti] | Fai clic su questo pulsante per mostrare su quali pagine viene utilizzata la risorsa. |
| [!UICONTROL Controllo delle versioni] | Consente di creare e ripristinare le versioni di una risorsa. |

1. Trascina l’azione appropriata nella sezione **Azioni** nella pagina. Crea un’opzione utilizzata per eseguire l’azione trascinata sulla pagina.

![chlimage_1-165](assets/chlimage_1-393.png)

## Modificare più risorse con la pagina Editor risorse {#multi-editing-assets-with-the-asset-editor-page}

Con [!DNL Experience Manager Assets], puoi modificare diverse risorse contemporaneamente. Dopo aver selezionato le risorse, puoi modificare simultaneamente tag e metadati.

Per modificare più risorse con la pagina Editor risorse:

1. Apri la Geometrixx **Centro stampa** pagina:
   `https://localhost:4502/content/geometrixx/en/company/press.html`

1. Seleziona le risorse:

   * in Windows: `Ctrl + click` ogni risorsa.
   * su Mac: `Cmd + click` ogni risorsa.

   Per selezionare un intervallo di risorse: fai clic sulla prima risorsa, quindi `Shift + click` l’ultima risorsa.

1. Clic **Modifica metadati** nel **Azioni** (parte sinistra della pagina).
1. Il Geometrixx **Press Center Asset Editor** pagina viene aperta in una nuova scheda. I metadati delle risorse vengono visualizzati come segue:

   * Viene visualizzato in corsivo un tag che non si applica a tutte le risorse, ma solo ad alcune.
   * Un tag applicato a tutte le risorse viene visualizzato con un font normale.
   * Metadati diversi dai tag: il valore del campo viene visualizzato solo se è lo stesso per tutte le risorse selezionate.

1. Clic **Scarica** per scaricare un file ZIP contenente le rappresentazioni originali delle risorse.
1. Fai clic su Modifica l’opzione dei tag accanto al **Tag** campo.

   * Un tag che non si applica a tutte le risorse, ma solo ad alcune di esse, ha uno sfondo grigio.
   * Un tag applicato a tutte le risorse ha uno sfondo bianco.

   Operazioni disponibili:

   * Clic `x` per rimuovere il tag per tutte le risorse.
   * Clic `+` per aggiungere il tag a tutte le risorse.
   * Fai clic su **freccia** e seleziona un tag per aggiungere un nuovo tag a tutte le risorse.

   Clic **OK** per scrivere le modifiche nel modulo. La casella accanto al **Tag** viene selezionato automaticamente.

1. Modifica il campo Descrizione. Ad esempio, impostalo su:

   `This is a common description`

   Quando si modifica un campo, il relativo valore sovrascrive i valori esistenti delle risorse selezionate al momento dell’invio del modulo.

   Nota: la casella accanto al campo viene selezionata automaticamente quando il campo viene modificato.

1. Clic **Aggiorna metadati** per inviare il modulo e salvare le modifiche per tutte le risorse.

   Nota: vengono modificati solo i metadati selezionati.
