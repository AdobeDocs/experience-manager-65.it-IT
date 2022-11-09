---
title: Sviluppo di componenti AEM (interfaccia classica)
seo-title: Developing AEM Components (Classic UI)
description: L’interfaccia classica utilizza ExtJS per creare widget che forniscono l’aspetto dei componenti. HTL non è il linguaggio di script consigliato per AEM.
seo-description: The classic UI uses ExtJS to create widgets that provide the look-and-feel of the components. HTL is not the recommended scripting language for AEM.
uuid: ed53d7c6-5996-4892-81a4-4ac30df85f04
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: c68f724f-f9b3-4018-8d3a-1680c53d73f8
legacypath: /content/docs/en/aem/6-2/develop/components/components-classic
exl-id: 3f078139-73fd-4913-9d67-264fb2515f8a
source-git-commit: 43a30b5ba76ea470cc50a962d4f04b4a1508964d
workflow-type: tm+mt
source-wordcount: '2392'
ht-degree: 1%

---

# Sviluppo di componenti AEM (interfaccia classica){#developing-aem-components-classic-ui}

L’interfaccia classica utilizza ExtJS per creare widget che forniscono l’aspetto dei componenti. A causa della natura di questi widget, vi sono alcune differenze tra il modo in cui i componenti interagiscono con l’interfaccia classica e il [interfaccia touch](/help/sites-developing/developing-components.md).

>[!NOTE]
>
>Molti aspetti dello sviluppo dei componenti sono comuni sia all’interfaccia classica che a quella touch, quindi **devi leggere [Componenti AEM - Nozioni di base](/help/sites-developing/components-basics.md) prima** utilizzo di questa pagina, che tratta le specifiche dell’interfaccia classica.

>[!NOTE]
>
>Sebbene sia HTML Template Language (HTL) che JSP possano essere utilizzati per lo sviluppo di componenti per l’interfaccia classica, questa pagina illustra lo sviluppo con JSP. Ciò è dovuto esclusivamente alla cronologia dell’utilizzo di JSP nell’interfaccia classica.
>
>HTL è ora il linguaggio di script consigliato per AEM. Vedi [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) e [Sviluppo di componenti AEM](/help/sites-developing/developing-components.md) per confrontare i metodi.

## Struttura {#structure}

La struttura di base di un componente viene illustrata nella pagina [Componenti AEM - Nozioni di base](/help/sites-developing/components-basics.md#structure), che applica sia le interfacce touch che classica. Anche se non è necessario utilizzare le impostazioni per l’interfaccia touch nel nuovo componente, può essere utile conoscerle quando si eredita da componenti esistenti.

## Script JSP {#jsp-scripts}

Gli script o i servlet JSP possono essere utilizzati per il rendering dei componenti. Secondo le regole di elaborazione della richiesta di Sling il nome per lo script predefinito è:

`<*componentname*>.jsp`

## global.jsp {#global-jsp}

Il file di script JSP `global.jsp` viene utilizzato per fornire un accesso rapido a oggetti specifici (ad esempio per accedere al contenuto) a qualsiasi file di script JSP utilizzato per il rendering di un componente.

Pertanto `global.jsp` deve essere incluso in ogni script JSP di rendering del componente in cui uno o più oggetti forniti in `global.jsp` sono utilizzati.

Posizione dell&#39;impostazione predefinita `global.jsp` è:

`/libs/foundation/global.jsp`

>[!NOTE]
>
>Il percorso `/libs/wcm/global.jsp`, utilizzato dalle versioni CQ 5.3 e precedenti, ora è obsoleto.

### Funzione di global.jsp, API utilizzate e Taglibs {#function-of-global-jsp-used-apis-and-taglibs}

Di seguito sono elencati gli oggetti più importanti forniti dall’impostazione predefinita `global.jsp`:

Riepilogo:

* `<cq:defineObjects />`

   * `slingRequest` - L&#39;oggetto di richiesta con wrapping ( `SlingHttpServletRequest`).
   * `slingResponse` - L&#39;oggetto di risposta racchiuso ( `SlingHttpServletResponse`).
   * `resource` - L&#39;Oggetto Risorsa Sling ( `slingRequest.getResource();`).
   * `resourceResolver` - L&#39;Oggetto Sling Resource Resolver ( `slingRequest.getResoucreResolver();`).
   * `currentNode` - Il nodo JCR risolto per la richiesta.
   * `log` - Il logger predefinito ().
   * `sling` - L&#39;helper dello script Sling.
   * `properties` - Le proprietà della risorsa gestita ( `resource.adaptTo(ValueMap.class);`).
   * `pageProperties` - Le proprietà della pagina della risorsa gestita.
   * `pageManager` - Gestione delle pagine per l&#39;accesso AEM pagine di contenuto ( `resourceResolver.adaptTo(PageManager.class);`).
   * `component` - L&#39;oggetto componente del componente AEM corrente.
   * `designer` - L&#39;oggetto designer per il recupero delle informazioni di progettazione ( `resourceResolver.adaptTo(Designer.class);`).
   * `currentDesign` - Progettazione della risorsa gestita.
   * `currentStyle` - Stile della risorsa gestita.

### Accesso al contenuto {#accessing-content}

Sono disponibili tre metodi per accedere al contenuto in AEM WCM:

* Tramite l&#39;oggetto properties introdotto in `global.jsp`:

   L&#39;oggetto properties è un&#39;istanza di ValueMap (vedi [API Sling](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ValueMap.html)) e contiene tutte le proprietà della risorsa corrente.

   Esempio: `String pageTitle = properties.get("jcr:title", "no title");` utilizzato nello script di rendering di un componente pagina.

   Esempio: `String paragraphTitle = properties.get("jcr:title", "no title");` utilizzato nello script di rendering di un componente paragrafo standard.

* Tramite il `currentPage` oggetto introdotto in `global.jsp`:

   La `currentPage` l&#39;oggetto è un&#39;istanza di una pagina (vedi [API AEM](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.mhtml)). La classe page fornisce alcuni metodi per accedere al contenuto.

   Esempio: `String pageTitle = currentPage.getTitle();`

* Via `currentNode` oggetto introdotto in `global.jsp`:

   La `currentNode` l&#39;oggetto è un&#39;istanza di un nodo (vedi [API JCR](https://jackrabbit.apache.org/api/2.16/org/apache/jackrabbit/standalone/cli/core/CurrentNode.html)). Le proprietà di un nodo sono accessibili dal `getProperty()` metodo .

   Esempio: `String pageTitle = currentNode.getProperty("jcr:title");`

## Librerie di tag JSP {#jsp-tag-libraries}

Le librerie di tag CQ e Sling consentono di accedere a funzioni specifiche da utilizzare nello script JSP dei modelli e dei componenti.

Per ulteriori informazioni, consulta il documento [Librerie di tag](/help/sites-developing/taglib.md).

## Utilizzo delle librerie HTML lato client {#using-client-side-html-libraries}

I siti web moderni si basano fortemente sull’elaborazione lato client basata su codice JavaScript e CSS complessi. Organizzare e ottimizzare il servizio di questo codice può essere un problema complicato.

Per risolvere questo problema, AEM fornisce **Cartelle libreria lato client**, che ti consente di memorizzare il codice lato client nell’archivio, organizzarlo in categorie e definire quando e come ogni categoria di codice deve essere trasmessa al client. Il sistema di libreria lato client si occupa quindi di produrre i collegamenti corretti nella pagina web finale per caricare il codice corretto.

Vedere il documento [Utilizzo delle librerie HTML lato client](/help/sites-developing/clientlibs.md) per ulteriori informazioni.

## Finestra di dialogo {#dialog}

Per aggiungere e configurare il contenuto, è necessaria una finestra di dialogo per gli autori.

Vedi [Componenti AEM - Nozioni di base](/help/sites-developing/components-basics.md#dialogs) per ulteriori dettagli.

## Configurazione del comportamento di modifica {#configuring-the-edit-behavior}

Puoi configurare il comportamento di modifica di un componente. Ciò include attributi come le azioni disponibili per il componente, le caratteristiche dell’editor locale e i listener relativi agli eventi sul componente. La configurazione è comune sia alle interfacce touch che alle interfacce classica, anche se con alcune specifiche differenze.

La [è configurato il comportamento di modifica di un componente](/help/sites-developing/components-basics.md#edit-behavior) aggiungendo un `cq:editConfig` nodo di tipo `cq:EditConfig` sotto il nodo del componente (di tipo `cq:Component`) e aggiungendo proprietà specifiche e nodi secondari.

## Utilizzo ed estensione dei widget ExtJS {#using-and-extending-extjs-widgets}

Vedi [Utilizzo ed estensione dei widget ExtJS](/help/sites-developing/widgets.md) per ulteriori dettagli.

## Utilizzo di xtypes per i widget ExtJS {#using-xtypes-for-extjs-widgets}

Vedi [Utilizzo di xtypes](/help/sites-developing/xtypes.md) per ulteriori dettagli.

## Sviluppo di nuovi componenti {#developing-new-components}

Questa sezione descrive come creare i propri componenti e aggiungerli al sistema paragrafo.

Un modo rapido per iniziare consiste nel copiare un componente esistente e quindi apportare le modifiche desiderate.

Un esempio di come sviluppare un componente è descritto in dettaglio in [Estensione del componente Testo e immagine - Un esempio.](#extending-the-text-and-image-component-an-example)

### Sviluppa un nuovo componente (adatta componente esistente) {#develop-a-new-component-adapt-existing-component}

Per sviluppare nuovi componenti per AEM basati sul componente esistente è possibile copiare il componente, creare un file javascript per il nuovo componente e archiviarlo in una posizione accessibile a AEM (vedi anche [Personalizzazione di componenti e altri elementi](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)):

1. Utilizzando CRXDE Lite, crea una nuova cartella di componenti in:

   / `apps/<myProject>/components/<myComponent>`

   Ricrea la struttura del nodo come in libs, quindi copia la definizione di un componente esistente, ad esempio il componente Testo . Ad esempio, per personalizzare la copia del componente Testo :

   * da `/libs/foundation/components/text`
   * a `/apps/myProject/components/text`

1. Modifica la `jcr:title` per riflettere il nuovo nome.
1. Apri la nuova cartella dei componenti e apporta le modifiche necessarie. Inoltre, elimina eventuali informazioni estranee presenti nella cartella.

   Puoi apportare modifiche quali:

   * aggiunta di un nuovo campo nella finestra di dialogo

      * `cq:dialog` - Finestra di dialogo per l’interfaccia touch
      * `dialog` - Finestra di dialogo per l’interfaccia classica
   * sostituzione del `.jsp` file (denominalo dopo il nuovo componente)
   * o rielaborazione completa dell’intero componente, se lo si desidera

   Ad esempio, se scegli una copia del componente Testo standard, puoi aggiungere un campo aggiuntivo alla finestra di dialogo e quindi aggiornare il `.jsp` per elaborare l&#39;input effettuato in quel punto.

   >[!NOTE]
   >
   >Un componente per:
   >
   >* L’interfaccia touch utilizza [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html) componenti
   >* L’interfaccia classica utilizza [Widget ExtJS](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html)


   >[!NOTE]
   >
   >Una finestra di dialogo definita per l’interfaccia classica funziona all’interno dell’interfaccia touch.
   >
   >Una finestra di dialogo definita per l’interfaccia touch non funziona nell’interfaccia classica.
   >
   >A seconda dell’ambiente di istanza e authoring, è possibile definire entrambi i tipi di finestra di dialogo per il componente.

1. Uno dei seguenti nodi deve essere presente e inizializzato correttamente affinché venga visualizzato il nuovo componente:

   * `cq:dialog` - Finestra di dialogo per l’interfaccia touch
   * `dialog` - Finestra di dialogo per l’interfaccia classica
   * `cq:editConfig` - comportamento dei componenti nell’ambiente di modifica (ad esempio, trascinamento)
   * `design_dialog` - finestra di dialogo per la modalità di progettazione (solo interfaccia classica)

1. Attiva il nuovo componente nel sistema paragrafo:

   * utilizzo di CRXDE Lite per aggiungere il valore `<path-to-component>` (ad esempio, `/apps/geometrixx/components/myComponent`) ai componenti di proprietà del nodo `/etc/designs/geometrixx/jcr:content/contentpage/par`
   * seguendo le istruzioni riportate in [Aggiunta di nuovi componenti ai sistemi paragrafo](#adding-a-new-component-to-the-paragraph-system-design-mode)

1. In AEM WCM, apri una pagina del sito Web e inserisci un nuovo paragrafo del tipo appena creato per verificare che il componente funzioni correttamente.

>[!NOTE]
>
>Per visualizzare le statistiche di temporizzazione per il caricamento della pagina, puoi utilizzare Ctrl-Maiusc-U con `?debugClientLibs=true` nell’URL.

### Aggiunta di un nuovo componente al sistema paragrafo (modalità Progettazione) {#adding-a-new-component-to-the-paragraph-system-design-mode}

Una volta sviluppato il componente, lo aggiungi al sistema di paragrafi, consentendo agli autori di selezionare e utilizzare il componente durante la modifica di una pagina.

1. Accedere a una pagina dell’ambiente di authoring che utilizza il sistema paragrafo, ad esempio `<contentPath>/Test.html`.
1. Passa alla modalità Progettazione effettuando una delle seguenti operazioni:

   * aggiunta `?wcmmode=design` alla fine dell’URL e accedi di nuovo, ad esempio:

      `<contextPath>/ Test.html?wcmmode=design`

   * clic su Progettazione nella barra laterale

   Ora sei in modalità progettazione e puoi modificare il sistema paragrafo.

1. Fai clic su Modifica.

   Viene visualizzato un elenco dei componenti appartenenti al sistema paragrafo. È elencato anche il nuovo componente.

   I componenti possono essere attivati (o disattivati) per determinare quali vengono offerti all’autore durante la modifica di una pagina.

1. Attiva il componente, quindi torna alla modalità di modifica normale per verificare che sia disponibile per l’uso.

### Estensione del componente Testo e Immagine - Un esempio {#extending-the-text-and-image-component-an-example}

Questa sezione fornisce un esempio su come estendere il componente di testo e immagine standard, ampiamente utilizzato, con una funzione di posizionamento dell’immagine configurabile.

L’estensione al componente testo e immagine consente agli editor di utilizzare tutte le funzionalità esistenti del componente, oltre a un’opzione aggiuntiva per specificare il posizionamento dell’immagine:

* Sul lato sinistro del testo (comportamento corrente e nuovo predefinito)
* nonché sul lato destro

Dopo aver esteso questo componente, puoi configurare il posizionamento dell’immagine tramite la finestra di dialogo del componente.

In questo esercizio sono descritte le seguenti tecniche:

* Copiare il nodo componente esistente e modificarne i metadati
* Modifica della finestra di dialogo del componente, inclusa l’ereditarietà dei widget dalle finestre di dialogo padre
* Modifica dello script del componente per implementare la nuova funzionalità

>[!NOTE]
>
>Questo esempio è destinato all’interfaccia classica.

>[!NOTE]
>
>Questo esempio si basa sul contenuto di esempio di Geometrixx, che non viene più fornito con AEM, essendo stato sostituito da We.Retail. Vedere il documento [Implementazione di riferimento di We.Retail](/help/sites-developing/we-retail.md#we-retail-geometrixx) per informazioni su come scaricare e installare Geometrixx.

#### Estensione del componente Testo esistente {#extending-the-existing-textimage-component}

Per creare il nuovo componente, utilizziamo il componente di testo standard come base e lo modifichiamo. Il nuovo componente viene memorizzato nell’applicazione di esempio Geometrixx AEM WCM.

1. Copia il componente di testo standard da `/libs/foundation/components/textimage` nella cartella del componente Geometrixx, `/apps/geometrixx/components`, utilizzando il textimage come nome del nodo di destinazione. Copia il componente accedendo al componente, facendo clic con il pulsante destro del mouse e selezionando Copia e navigando nella directory di destinazione.

   ![chlimage_1-59](assets/chlimage_1-59a.png)

1. Per semplificare questo esempio, passa al componente copiato ed elimina tutti i sottonodi del nuovo nodo di textimage, tranne i seguenti:

   * definizione finestra di dialogo: `textimage/dialog`
   * script componente: `textimage/textimage.jsp`
   * modifica il nodo di configurazione (che consente il trascinamento della selezione delle risorse): `textimage/cq:editConfig`

   >[!NOTE]
   >
   >La definizione della finestra di dialogo dipende dall’interfaccia utente:
   >
   >* Interfaccia touch: `textimage/cq:dialog`
   >* Interfaccia classica: `textimage/dialog`


1. Modifica i metadati del componente:

   * Nome componente

      * Imposta `jcr:description` a `Text Image Component (Extended)`
      * Imposta `jcr:title` a `Text Image (Extended)`
   * Gruppo, in cui il componente è elencato nella barra laterale (lascia così com’è)

      * Esci `componentGroup` impostato su `General`
   * Componente principale per il nuovo componente (il componente di testo standard)

      * Imposta `sling:resourceSuperType` a `foundation/components/textimage`

   Dopo questo passaggio, il nodo del componente si presenta così:

   ![chlimage_1-60](assets/chlimage_1-60a.png)

1. Modificare la `sling:resourceType` proprietà del nodo di configurazione modifica dell&#39;immagine (proprietà: `textimage/cq:editConfig/cq:dropTargets/image/parameters/sling:resourceType`) a `geometrixx/components/textimage.`

   In questo modo, quando un’immagine viene rilasciata al componente sulla pagina, la `sling:resourceType` la proprietà del componente testo esteso è impostata su: `geometrixx/components/textimage.`

1. Modificare la finestra di dialogo del componente in modo da includere la nuova opzione. Il nuovo componente eredita le parti della finestra di dialogo uguali a quelle dell’originale. L&#39;unica aggiunta che facciamo è quella di estendere **Avanzate** scheda , aggiunta di un **Posizione immagine** elenco a discesa, con opzioni **Sinistra** e **Destra**:

   * Lascia la `textimage/dialog`proprietà invariate.

   Nota come `textimage/dialog/items` presenta quattro sottonodi, da tab1 a tab4, che rappresentano le quattro schede della finestra di dialogo della textimage.

   * Per le prime due schede (tab1 e tab2):

      * Cambia xtype in cqinclude (per ereditare dal componente standard).
      * Aggiungere una proprietà del percorso con i valori `/libs/foundation/components/textimage/dialog/items/tab1.infinity.json`e `/libs/foundation/components/textimage/dialog/items/tab2.infinity.json`, rispettivamente.
      * Rimuovere tutte le altre proprietà o sottonodi.
   * Per la scheda 3:

      * Lascia le proprietà e i sottonodi senza modifiche
      * Aggiungi una nuova definizione di campo a `tab3/items`, posizione del nodo del tipo `cq:Widget`
      * Imposta le seguenti proprietà (di tipo String) per il nuovo `tab3/items/position`nodo:

         * `name`: `./imagePosition`
         * `xtype`: `selection`
         * `fieldLabel`: `Image Position`
         * `type`: `select`
      * Aggiungi nodo secondario `position/options` di tipo `cq:WidgetCollection` per rappresentare le due scelte per il posizionamento dell&#39;immagine, e sotto di esso creare due nodi, o1 e o2 di tipo `nt:unstructured`.
      * Per nodo `position/options/o1` imposta le proprietà: `text` a `Left` e `value` a `left.`
      * Per nodo `position/options/o2` imposta le proprietà: `text` a `Right` e `value` a `right`.
   * Elimina scheda4.

   La posizione dell&#39;immagine viene mantenuta nel contenuto come `imagePosition`proprietà del nodo che rappresenta `textimage` paragrafo. Dopo questi passaggi, la finestra di dialogo del componente si presenta così:

   ![chlimage_1-61](assets/chlimage_1-61a.png)

1. Estende lo script del componente, `textimage.jsp`, con ulteriore gestione del nuovo parametro:

   ```xml
   Image image = new Image(resource, "image");
   
   if (image.hasContent() || WCMMode.fromRequest(request) == WCMMode.EDIT) {
        image.loadStyleData(currentStyle);
   ```

   Sostituiremo il frammento di codice sottolineato *%>&lt;div class=&quot;image&quot;>&lt;%* con nuovo codice che genera uno stile personalizzato per questo tag.

   ```xml
   // todo: add new CSS class for the 'right image' instead of using
   // the style attribute
   String style="";
        if (properties.get("imagePosition", "left").equals("right")) {
             style = "style=\"float:right\"";
        }
        %><div <%= style %> class="image"><%
   ```

1. Salva il componente nella directory archivio. Il componente è pronto per il test.

#### Controllo del nuovo componente {#checking-the-new-component}

Una volta sviluppato il componente, è possibile aggiungerlo al sistema di paragrafi, consentendo agli autori di selezionare e utilizzare il componente durante la modifica di una pagina. Questi passaggi consentono di testare il componente.

1. Apri una pagina in Geometrixx, ad esempio Inglese / Azienda.
1. Passate alla modalità di progettazione facendo clic su Progettazione nella barra laterale.
1. Modificate la struttura del sistema di paragrafi facendo clic su Modifica nel sistema di paragrafi al centro della pagina. Viene visualizzato un elenco di componenti che possono essere inseriti nel sistema di paragrafi e deve includere il componente appena sviluppato, Immagine testo (estesa) . Attivalo per il sistema di paragrafi selezionandolo e facendo clic su OK .
1. Torna alla modalità di modifica.
1. Aggiungi il paragrafo Testo e immagine (Extended) al sistema di paragrafi, inizializza testo e immagine con contenuto di esempio. Salva le modifiche.
1. Apri la finestra di dialogo del testo e del paragrafo dell’immagine e modifica la posizione dell’immagine nella scheda Avanzate a destra , quindi fai clic su OK per salvare le modifiche.
1. Viene eseguito il rendering del paragrafo con l’immagine a destra.
1. Il componente è ora pronto per l’uso.

Il componente memorizza il suo contenuto in un paragrafo della pagina Società.

### Disattiva la funzionalità di caricamento del componente immagine {#disable-upload-capability-of-the-image-component}

Per disabilitare questa funzionalità, utilizziamo il componente immagine standard come base e lo modifichiamo. Il nuovo componente viene memorizzato nell’applicazione di Geometrixx.

1. Copia il componente immagine standard da `/libs/foundation/components/image` nella cartella del componente Geometrixx, `/apps/geometrixx/components`, utilizzando l’immagine come nome del nodo di destinazione.

   ![chlimage_1-62](assets/chlimage_1-62a.png)

1. Modifica i metadati del componente:

   * Imposta **jcr:title** a `Image (Extended)`

1. Accedi a `/apps/geometrixx/components/image/dialog/items/image`.
1. Aggiungi una nuova proprietà:

   * **Nome**: `allowUpload`
   * **Tipo**: `String`
   * **Valore**: `false`

   ![chlimage_1-63](assets/chlimage_1-63a.png)

1. Fai clic su **Salva tutto**. Il componente è pronto per il test.
1. Apri una pagina in Geometrixx, ad esempio Inglese / Azienda.
1. Passa alla modalità di progettazione e attiva l&#39;immagine (Extended).
1. Torna alla modalità di modifica e aggiungilo al sistema paragrafo. Nelle immagini successive, è possibile vedere le differenze tra il componente immagine originale e quello appena creato.

   Componente immagine originale:

   ![chlimage_1-64](assets/chlimage_1-64a.png)

   Il nuovo componente immagine:

   ![chlimage_1-65](assets/chlimage_1-65a.png)

1. Il componente è ora pronto per l’uso.
