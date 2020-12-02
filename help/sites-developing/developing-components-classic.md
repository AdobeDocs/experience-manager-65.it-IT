---
title: Sviluppo di componenti AEM (interfaccia classica)
seo-title: Sviluppo di componenti AEM (interfaccia classica)
description: L’interfaccia classica utilizza ExtJS per creare widget che forniscono l’aspetto dei componenti. HTL non è il linguaggio di script consigliato per AEM.
seo-description: L’interfaccia classica utilizza ExtJS per creare widget che forniscono l’aspetto dei componenti. HTL non è il linguaggio di script consigliato per AEM.
uuid: ed53d7c6-5996-4892-81a4-4ac30df85f04
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: c68f724f-f9b3-4018-8d3a-1680c53d73f8
legacypath: /content/docs/en/aem/6-2/develop/components/components-classic
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835
workflow-type: tm+mt
source-wordcount: '2423'
ht-degree: 1%

---


# Sviluppo di componenti AEM (interfaccia classica){#developing-aem-components-classic-ui}

L’interfaccia classica utilizza ExtJS per creare widget che forniscono l’aspetto dei componenti. A causa della natura di questi widget, vi sono alcune differenze tra il modo in cui i componenti interagiscono con l&#39;interfaccia classica e l&#39; [interfaccia touch](/help/sites-developing/developing-components.md).

>[!NOTE]
>
>Molti aspetti dello sviluppo di componenti sono comuni sia all&#39;interfaccia classica che all&#39;interfaccia touch, pertanto **è necessario leggere [Componenti AEM - Le nozioni di base](/help/sites-developing/components-basics.md) prima di** utilizzando questa pagina, che tratta delle specifiche dell&#39;interfaccia classica.

>[!NOTE]
>
>Sebbene sia il linguaggio HTL (HTML Template Language) che il linguaggio JSP possano essere utilizzati per lo sviluppo di componenti per l’interfaccia classica, questa pagina illustra lo sviluppo con JSP. Ciò è dovuto esclusivamente alla cronologia dell’utilizzo di JSP nell’interfaccia classica.
>
>HTL è ora il linguaggio di script consigliato per AEM. Per confrontare i metodi, vedere [HTL](https://docs.adobe.com/content/help/it-IT/experience-manager-htl/using/overview.html) e [Sviluppo di componenti AEM](/help/sites-developing/developing-components.md).

## Struttura {#structure}

La struttura di base di un componente è coperta dalla pagina [Componenti AEM - The Basics](/help/sites-developing/components-basics.md#structure), che applica sia l&#39;interfaccia touch sia l&#39;interfaccia classica. Anche se non è necessario utilizzare le impostazioni per l’interfaccia touch nel nuovo componente, può essere utile essere consapevoli di tali impostazioni quando si eredita da componenti esistenti.

## Script JSP {#jsp-scripts}

Gli script JSP o i servlet possono essere utilizzati per il rendering dei componenti. Secondo le regole di elaborazione della richiesta di Sling il nome per lo script predefinito è:

`<*componentname*>.jsp`

## global.jsp {#global-jsp}

Il file di script JSP `global.jsp` è utilizzato per fornire accesso rapido a oggetti specifici (ad esempio per accedere al contenuto) a qualsiasi file di script JSP utilizzato per il rendering di un componente.

Di conseguenza, `global.jsp` deve essere incluso in ogni script JSP di rendering dei componenti in cui viene utilizzato uno o più oggetti forniti in `global.jsp`.

Il percorso predefinito `global.jsp` è:

`/libs/foundation/global.jsp`

>[!NOTE]
>
>Il percorso `/libs/wcm/global.jsp`, utilizzato dalle versioni CQ 5.3 e precedenti, è ora obsoleto.

### Funzione di global.jsp, API utilizzate e Taglibs {#function-of-global-jsp-used-apis-and-taglibs}

Di seguito sono elencati gli oggetti più importanti forniti dal valore predefinito `global.jsp`:

Riepilogo:

* `<cq:defineObjects />`

   * `slingRequest` - L&#39;oggetto di richiesta racchiusa (  `SlingHttpServletRequest`).
   * `slingResponse` - L&#39;oggetto di risposta racchiuso (  `SlingHttpServletResponse`).
   * `resource` - L&#39;Oggetto Sling Resource (  `slingRequest.getResource();`).
   * `resourceResolver` - L&#39;Oggetto Sling Resource Resolver (  `slingRequest.getResoucreResolver();`).
   * `currentNode` - Il nodo JCR risolto per la richiesta.
   * `log` - Il logger Predefinito ().
   * `sling` - L&#39;helper di script Sling.
   * `properties` - Le proprietà della risorsa indirizzata (  `resource.adaptTo(ValueMap.class);`).
   * `pageProperties` - Proprietà della pagina della risorsa indirizzata.
   * `pageManager` - Gestione pagine per l&#39;accesso AEM pagine di contenuto (  `resourceResolver.adaptTo(PageManager.class);`).
   * `component` - L&#39;oggetto componente del componente AEM corrente.
   * `designer` - L&#39;oggetto designer per il recupero delle informazioni di progettazione (  `resourceResolver.adaptTo(Designer.class);`).
   * `currentDesign` - La progettazione della risorsa indirizzata.
   * `currentStyle` - Lo stile della risorsa indirizzata.

### Accesso al contenuto {#accessing-content}

Esistono tre metodi per accedere al contenuto in AEM WCM:

* Tramite l&#39;oggetto properties introdotto in `global.jsp`:

   L&#39;oggetto properties è un&#39;istanza di ValueMap (vedere [Sling API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ValueMap.html)) e contiene tutte le proprietà della risorsa corrente.

   Esempio: `String pageTitle = properties.get("jcr:title", "no title");` utilizzato nello script di rendering di un componente di pagina.

   Esempio: `String paragraphTitle = properties.get("jcr:title", "no title");` utilizzato nello script di rendering di un componente paragrafo standard.

* Tramite l&#39;oggetto `currentPage` introdotto in `global.jsp`:

   L&#39;oggetto `currentPage` è un&#39;istanza di una pagina (vedere [AEM API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.mhtml)). La classe page fornisce alcuni metodi per accedere al contenuto.

   Esempio: `String pageTitle = currentPage.getTitle();`

* Mediante l&#39;oggetto `currentNode` introdotto in `global.jsp`:

   L&#39;oggetto `currentNode` è un&#39;istanza di un nodo (vedere [API JCR](https://jackrabbit.apache.org/api/2.16/org/apache/jackrabbit/standalone/cli/core/CurrentNode.html)). È possibile accedere alle proprietà di un nodo tramite il metodo `getProperty()`.

   Esempio: `String pageTitle = currentNode.getProperty("jcr:title");`

## Librerie di tag JSP {#jsp-tag-libraries}

Le librerie di tag CQ e Sling consentono di accedere a funzioni specifiche da utilizzare nello script JSP dei modelli e dei componenti.

Per ulteriori informazioni, vedere il documento [Tag Libraries](/help/sites-developing/taglib.md).

## Utilizzo di librerie HTML lato client {#using-client-side-html-libraries}

I siti Web moderni si affidano in larga misura all&#39;elaborazione sul lato client basata su codice JavaScript e CSS complessi. L&#39;organizzazione e l&#39;ottimizzazione della gestione di questo codice può essere un problema complicato.

Per risolvere il problema, AEM fornisce **Cartelle libreria lato client** che consentono di memorizzare il codice lato client nell&#39;archivio, organizzarlo in categorie e definire quando e come ciascuna categoria di codice deve essere distribuita al client. Il sistema di libreria lato client si occupa quindi di generare i collegamenti corretti nella pagina Web finale per caricare il codice corretto.

Per ulteriori informazioni, vedere il documento [Utilizzo di librerie HTML lato client](/help/sites-developing/clientlibs.md).

## Finestra di dialogo {#dialog}

Per aggiungere e configurare il contenuto, sarà necessaria una finestra di dialogo per gli autori.

Per ulteriori informazioni, vedere [AEM Componenti - The Basics](/help/sites-developing/components-basics.md#dialogs).

## Configurazione del comportamento di modifica {#configuring-the-edit-behavior}

È possibile configurare il comportamento di modifica di un componente. Questo include attributi quali le azioni disponibili per il componente, le caratteristiche dell’editor locale e i listener relativi agli eventi sul componente. La configurazione è comune a entrambe le interfacce touch e classica, anche se con alcune specifiche differenze.

Il comportamento di [modifica di un componente è configurato](/help/sites-developing/components-basics.md#edit-behavior) aggiungendo un nodo `cq:editConfig` di tipo `cq:EditConfig` sotto il nodo del componente (di tipo `cq:Component`) e aggiungendo proprietà e nodi secondari specifici.

## Utilizzo ed estensione dei widget ExtJS {#using-and-extending-extjs-widgets}

Per ulteriori informazioni, vedere [Utilizzo ed estensione dei widget ExtJS](/help/sites-developing/widgets.md).

## Utilizzo di xtype per i widget ExtJS {#using-xtypes-for-extjs-widgets}

Per ulteriori informazioni, vedere [Utilizzo di xtype](/help/sites-developing/xtypes.md).

## Sviluppo di nuovi componenti {#developing-new-components}

Questa sezione descrive come creare componenti personalizzati e aggiungerli al sistema di paragrafi.

Un modo rapido per iniziare consiste nel copiare un componente esistente e quindi apportare le modifiche desiderate.

Un esempio di come sviluppare un componente è descritto in dettaglio in [Estensione del componente Testo e immagine - Un esempio.](#extending-the-text-and-image-component-an-example)

### Sviluppare un nuovo componente (Adatta componente esistente) {#develop-a-new-component-adapt-existing-component}

Per sviluppare nuovi componenti per AEM basati sul componente esistente, potete copiare il componente, creare un file javascript per il nuovo componente e memorizzarlo in una posizione accessibile a AEM (vedere anche [Personalizzazione di componenti e altri elementi](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)):

1. Con CRXDE Lite , create una nuova cartella di componenti in:

   / `apps/<myProject>/components/<myComponent>`

   Ricreare la struttura del nodo come in libs, quindi copiare la definizione di un componente esistente, ad esempio il componente Testo. Ad esempio, per personalizzare la copia del componente Testo:

   * da `/libs/foundation/components/text`
   * a `/apps/myProject/components/text`

1. Modificate il `jcr:title` in modo che rifletta il nuovo nome.
1. Apri la nuova cartella dei componenti e apporta le modifiche necessarie. Inoltre, eliminate eventuali informazioni estranee presenti nella cartella.

   È possibile apportare modifiche quali:

   * aggiunta di un nuovo campo nella finestra di dialogo

      * `cq:dialog` - finestra di dialogo per l’interfaccia touch
      * `dialog` - finestra di dialogo per l’interfaccia classica
   * sostituzione del file `.jsp` (denominarlo dopo il nuovo componente)
   * oppure rielaborare completamente l’intero componente, se lo si desidera

   Ad esempio, se si prende una copia del componente Testo standard, è possibile aggiungere un campo aggiuntivo alla finestra di dialogo, quindi aggiornare il simbolo `.jsp` per elaborare l&#39;input immesso.

   >[!NOTE]
   >
   >Un componente per:
   >
   >* L&#39;interfaccia touch utilizza i componenti [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
   >* L&#39;interfaccia classica utilizza [widget ExtJS](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html)


   >[!NOTE]
   >
   >All’interno dell’interfaccia touch viene visualizzata una finestra di dialogo definita per l’interfaccia classica.
   >
   >Una finestra di dialogo definita per l’interfaccia touch non funziona nell’interfaccia classica.
   >
   >A seconda dell’istanza e dell’ambiente di authoring, è possibile definire entrambi i tipi di dialogo per il componente.

1. Uno dei seguenti nodi deve essere presente e inizializzato correttamente affinché venga visualizzato il nuovo componente:

   * `cq:dialog` - finestra di dialogo per l’interfaccia touch
   * `dialog` - finestra di dialogo per l’interfaccia classica
   * `cq:editConfig` - funzionamento dei componenti nell’ambiente di modifica (ad esempio trascinamento)
   * `design_dialog` - finestra di dialogo per la modalità di progettazione (solo interfaccia classica)

1. Attivate il nuovo componente nel sistema paragrafo:

   * utilizzo di CRXDE Lite per aggiungere il valore `<path-to-component>` (ad esempio, `/apps/geometrixx/components/myComponent`) ai componenti delle proprietà del nodo `/etc/designs/geometrixx/jcr:content/contentpage/par`
   * seguendo le istruzioni riportate in [Aggiunta di nuovi componenti ai sistemi paragrafo](#adding-a-new-component-to-the-paragraph-system-design-mode)

1. In AEM WCM, aprite una pagina nel sito Web e inserite un nuovo paragrafo del tipo appena creato per essere certi che il componente funzioni correttamente.

>[!NOTE]
>
>Per visualizzare le statistiche sui tempi di caricamento della pagina, potete utilizzare Ctrl+Maiusc+U - con `?debugClientLibs=true` impostato nell&#39;URL.

### Aggiunta di un nuovo componente al sistema paragrafo (modalità Progettazione) {#adding-a-new-component-to-the-paragraph-system-design-mode}

Dopo che il componente è stato sviluppato, è possibile aggiungerlo al sistema di paragrafi, che consente agli autori di selezionare e utilizzare il componente durante la modifica di una pagina.

1. Accedere a una pagina all’interno dell’ambiente di authoring che utilizza il sistema paragrafo, ad esempio `<contentPath>/Test.html`.
1. Passate alla modalità Progettazione:

   * aggiunta di `?wcmmode=design` alla fine dell&#39;URL e successivo accesso, ad esempio:

      `<contextPath>/ Test.html?wcmmode=design`

   * clic su Progettazione nella barra laterale

   Ora è attiva la modalità di progettazione e può modificare il sistema di paragrafi.

1. Fai clic su Modifica.

   Viene visualizzato un elenco dei componenti appartenenti al sistema paragrafo. È elencato anche il nuovo componente.

   I componenti possono essere attivati (o disattivati) per determinare quali vengono offerti all’autore durante la modifica di una pagina.

1. Attivate il componente, quindi tornate alla modalità di modifica normale per verificare che sia disponibile per l’uso.

### Estensione del componente Testo e immagine - Esempio {#extending-the-text-and-image-component-an-example}

In questa sezione viene fornito un esempio su come estendere il componente standard per testo e immagini, ampiamente utilizzato, con una funzione di posizionamento delle immagini configurabile.

L’estensione al componente testo e immagine consente agli editor di utilizzare tutte le funzionalità esistenti del componente, più un’opzione aggiuntiva per specificare la posizione dell’immagine:

* A sinistra del testo (comportamento corrente e nuovo predefinito)
* nonché sul lato destro

Dopo aver esteso questo componente, potete configurare la posizione dell’immagine mediante la finestra di dialogo del componente.

In questo esercizio sono descritte le seguenti tecniche:

* Copia del nodo componente esistente e modifica dei relativi metadati
* Modifica della finestra di dialogo del componente, compresa l’ereditarietà dei widget dalle finestre di dialogo padre
* Modifica dello script del componente per implementare le nuove funzionalità

>[!NOTE]
>
>Questo esempio è indirizzato all’interfaccia classica.

>[!NOTE]
>
>Questo esempio si basa sul contenuto di Geometrixx, che non viene più fornito con AEM, essendo stato sostituito da We.Retail. Per informazioni su come scaricare e installare Geometrixx, consultate il documento [We.Retail Reference Implementation](/help/sites-developing/we-retail.md#we-retail-geometrixx).

#### Estensione del componente textimage esistente {#extending-the-existing-textimage-component}

Per creare il nuovo componente, utilizzeremo il componente di textimage standard come base e lo modificheremo. Il nuovo componente viene memorizzato nell’applicazione di esempio di Geometrixx AEM WCM.

1. Copiate il componente di testo standard da `/libs/foundation/components/textimage` nella cartella del componente di Geometrixx, `/apps/geometrixx/components`, utilizzando il testo come nome del nodo di destinazione. (Copiate il componente spostandovi sul componente, facendo clic con il pulsante destro del mouse e selezionando Copia e accedendo alla directory di destinazione.)

   ![chlimage_1-59](assets/chlimage_1-59a.png)

1. Per semplificare questo esempio, andate al componente che avete copiato ed eliminate tutti i nodi secondari del nuovo nodo del testo, ad eccezione dei seguenti:

   * definizione finestra di dialogo: `textimage/dialog`
   * script componente: `textimage/textimage.jsp`
   * modifica il nodo di configurazione (consente il trascinamento delle risorse): `textimage/cq:editConfig`

   >[!NOTE]
   >
   >La definizione della finestra di dialogo dipende dall’interfaccia:
   >
   >* Interfaccia touch: `textimage/cq:dialog`
   >* Interfaccia classica: `textimage/dialog`


1. Modificate i metadati del componente:

   * Nome componente

      * Impostare `jcr:description` su `Text Image Component (Extended)`
      * Impostare `jcr:title` su `Text Image (Extended)`
   * Gruppo, dove il componente è elencato nella barra laterale (lasciare invariato)

      * Lascia `componentGroup` impostato su `General`
   * Componente principale per il nuovo componente (il componente textimage standard)

      * Impostare `sling:resourceSuperType` su `foundation/components/textimage`

   Dopo questo passaggio, il nodo del componente si presenta come segue:

   ![chlimage_1-60](assets/chlimage_1-60a.png)

1. Modificare la proprietà `sling:resourceType` del nodo di configurazione di modifica dell&#39;immagine (proprietà: `textimage/cq:editConfig/cq:dropTargets/image/parameters/sling:resourceType`) a `geometrixx/components/textimage.`

   In questo modo, quando un&#39;immagine viene rilasciata al componente sulla pagina, la proprietà `sling:resourceType` del componente di testo esteso viene impostata su: `geometrixx/components/textimage.`

1. Modificare la finestra di dialogo del componente in modo da includere la nuova opzione. Il nuovo componente eredita le parti della finestra di dialogo che sono le stesse dell’originale. L&#39;unica aggiunta che facciamo è estendere la scheda **Avanzate**, aggiungendo un elenco a discesa **Posizione immagine**, con le opzioni **Left** e **Right**:

   * Lasciare invariate le proprietà `textimage/dialog`.

   Tenere presente che `textimage/dialog/items` ha quattro nodi secondari, da tab1 a tab4, che rappresentano le quattro schede della finestra di dialogo del testo.

   * Per le prime due schede (tab1 e tab2):

      * Cambia xtype in cqinclude (per ereditare dal componente standard).
      * Aggiungete una proprietà path con i valori `/libs/foundation/components/textimage/dialog/items/tab1.infinity.json`e `/libs/foundation/components/textimage/dialog/items/tab2.infinity.json` rispettivamente.
      * Rimuovere tutte le altre proprietà o i sottonodi.
   * Per tab3:

      * Lasciare le proprietà e i nodi secondari senza modifiche
      * Aggiungere una nuova definizione di campo a `tab3/items`, posizione del nodo di tipo `cq:Widget`
      * Impostare le seguenti proprietà (di tipo String) per il nuovo nodo `tab3/items/position`:

         * `name`: `./imagePosition`
         * `xtype`:  `selection`
         * `fieldLabel`:  `Image Position`
         * `type`:  `select`
      * Aggiungete il nodo secondario `position/options` di tipo `cq:WidgetCollection` per rappresentare le due scelte per la posizione dell&#39;immagine, e al suo interno create due nodi, o1 e o2 di tipo `nt:unstructured`.
      * Per il nodo `position/options/o1` impostare le proprietà: `text` a `Left` e `value` a `left.`
      * Per il nodo `position/options/o2` impostare le proprietà: `text` a `Right` e `value` a `right`.
   * Elimina, scheda4.

   La posizione dell&#39;immagine è persistente nel contenuto come proprietà `imagePosition`del nodo che rappresenta `textimage` il paragrafo. Dopo questa procedura, la finestra di dialogo del componente si presenta come segue:

   ![chlimage_1-61](assets/chlimage_1-61a.png)

1. Estende lo script del componente, `textimage.jsp`, con una gestione aggiuntiva del nuovo parametro:

   ```xml
   Image image = new Image(resource, "image");
   
   if (image.hasContent() || WCMMode.fromRequest(request) == WCMMode.EDIT) {
        image.loadStyleData(currentStyle);
   ```

   Sostituiremo il frammento di codice evidenziato *%>&lt;div class=&quot;image&quot;>&lt;%* con un nuovo codice che genererà uno stile personalizzato per questo tag.

   ```xml
   // todo: add new CSS class for the 'right image' instead of using
   // the style attribute
   String style="";
        if (properties.get("imagePosition", "left").equals("right")) {
             style = "style=\"float:right\"";
        }
        %><div <%= style %> class="image"><%
   ```

1. Salvare il componente nell’archivio. Il componente è pronto per essere testato.

#### Controllo del nuovo componente {#checking-the-new-component}

Una volta sviluppato il componente, è possibile aggiungerlo al sistema paragrafo, che consente agli autori di selezionare e utilizzare il componente durante la modifica di una pagina. Questi passaggi consentono di verificare il componente.

1. Aprite una pagina in Geometrixx quali Inglese/Società.
1. Passate alla modalità di progettazione facendo clic su Progettazione nella barra laterale.
1. Modificate la struttura del sistema di paragrafi facendo clic su Modifica nel sistema di paragrafi al centro della pagina. Viene visualizzato un elenco di componenti che possono essere inseriti nel sistema di paragrafi e deve includere il componente di recente sviluppo, Testo immagine (esteso). Attivarla per il sistema di paragrafi selezionandolo e facendo clic su OK .
1. Tornate alla modalità di modifica.
1. Aggiungete il paragrafo Testo e immagine (esteso) al sistema di paragrafi, inizializzate testo e immagine con contenuto di esempio. Salva le modifiche.
1. Aprite la finestra di dialogo del testo e del paragrafo dell’immagine e modificate la posizione dell’immagine nella scheda Avanzate a destra, quindi fate clic su OK per salvare le modifiche.
1. Viene eseguito il rendering del paragrafo con l’immagine a destra.
1. Il componente è ora pronto per l’uso.

Il componente memorizza il contenuto in un paragrafo nella pagina Società.

### Disattiva la funzionalità di caricamento del componente immagine {#disable-upload-capability-of-the-image-component}

Per disattivare questa funzionalità, utilizzeremo il componente immagine standard come base e lo modificheremo. Il nuovo componente viene memorizzato nell’applicazione di Geometrixx.

1. Copiate il componente immagine standard da `/libs/foundation/components/image` nella cartella del componente Geometrixx, `/apps/geometrixx/components`, utilizzando l&#39;immagine come nome del nodo di destinazione.

   ![chlimage_1-62](assets/chlimage_1-62a.png)

1. Modificate i metadati del componente:

   * Impostare **jcr:title** su `Image (Extended)`

1. Accedi a `/apps/geometrixx/components/image/dialog/items/image`.
1. Aggiungi una nuova proprietà:

   * **Nome**: `allowUpload`
   * **Tipo**: `String`
   * **Valore**:  `false`

   ![chlimage_1-63](assets/chlimage_1-63a.png)

1. Fare clic su **Salva tutto**. Il componente è pronto per essere testato.
1. Aprite una pagina in Geometrixx quali Inglese/Società.
1. Passate alla modalità di progettazione e attivate Immagine (estesa).
1. Tornate alla modalità di modifica e aggiungetela al sistema di paragrafi. Nelle immagini successive, potete vedere le differenze tra il componente immagine originale e quello appena creato.

   Componente immagine originale:

   ![chlimage_1-64](assets/chlimage_1-64a.png)

   Il nuovo componente immagine:

   ![chlimage_1-65](assets/chlimage_1-65a.png)

1. Il componente è ora pronto per l’uso.

