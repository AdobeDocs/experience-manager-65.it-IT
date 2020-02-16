---
title: Utilizzo ed estensione dei widget (interfaccia classica)
seo-title: Utilizzo ed estensione dei widget (interfaccia classica)
description: L'interfaccia basata sul Web di AEM utilizza AJAX e altre moderne tecnologie browser per consentire agli autori di modificare e formattare i contenuti WYSIWYG direttamente sulla pagina Web
seo-description: L'interfaccia basata sul Web di AEM utilizza AJAX e altre moderne tecnologie browser per consentire agli autori di modificare e formattare i contenuti WYSIWYG direttamente sulla pagina Web
uuid: eb3da415-cbef-4766-a28e-837e238a4156
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 7b234f1f-4470-4de1-a3c3-ab19e5e001ad
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# Utilizzo ed estensione dei widget (interfaccia classica){#using-and-extending-widgets-classic-ui}

>[!NOTE]
>
>Questa pagina descrive l’utilizzo dei widget nell’interfaccia classica, obsoleto in AEM 6.4.
>
>Adobe consiglia di utilizzare la moderna interfaccia [touch basata sull’interfaccia utente](/help/sites-developing/touch-ui-concepts.md) [Coral e l’interfaccia utente](/help/sites-developing/touch-ui-concepts.md#coral-ui) Granite [](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components).

L&#39;interfaccia basata su Web di Adobe Experience Manager utilizza AJAX e altre moderne tecnologie browser per consentire agli autori di modificare e formattare i contenuti WYSIWYG direttamente sulla pagina Web.

Adobe Experience Manager (AEM) utilizza la libreria di widget [ExtJS](https://www.sencha.com/) , che fornisce gli elementi dell’interfaccia utente altamente lucidi che funzionano su tutti i browser più importanti e consentono la creazione di esperienze dell’interfaccia utente per desktop.

Questi widget sono inclusi in AEM e, oltre a essere utilizzati direttamente da AEM, possono essere utilizzati da qualsiasi sito Web creato tramite AEM.

Per un riferimento completo a tutti i widget disponibili in AEM, consulta la documentazione [API relativa ai](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html) widget o l’ [elenco degli xtype](/help/sites-developing/xtypes.md)esistenti. Inoltre, molti esempi che mostrano come utilizzare il framework ExtJS sono disponibili sul sito [Sencha](https://www.sencha.com/products/extjs/examples/) , il proprietario del framework.

Questa pagina fornisce alcune informazioni su come utilizzare ed estendere i widget. In primo luogo, descrive come [includere il codice lato client in una pagina](#including-the-client-sided-code-in-a-page). Vengono quindi descritti alcuni componenti di esempio creati per illustrare l’uso e l’estensione di base. Tali componenti sono disponibili nel pacchetto **Using ExtJS Widget** on **Package Share**(Utilizzo di widgetJS in Package Share).

Il pacchetto include esempi di:

* [Finestre di dialogo](#basic-dialogs) di base con widget integrati.
* [Finestra di dialogo](#dynamic-dialogs) dinamica con widget predefiniti e logica JavaScript personalizzata.
* Finestre di dialogo basate su widget [](#custom-widgets)personalizzati.
* Un pannello [](#tree-overview) ad albero che visualizza una struttura JCR sotto un determinato percorso.
* Pannello [](#grid-overview) griglia che visualizza i dati in formato tabulare.

>[!NOTE]
>
>L’interfaccia classica di Adobe Experience Manager è basata su [ExtJS 3.4.0](https://extjs.cachefly.net/ext-3.4.0/docs/).

## Inclusione del codice lato client in una pagina {#including-the-client-sided-code-in-a-page}

Il codice javascript e del foglio di stile lato client deve essere inserito in una libreria client.

Per creare una libreria client:

1. Crea un nodo di seguito `/apps/<project>` con le seguenti proprietà:

   * name=&quot;clientlib&quot;
   * jcr:mixinTypes=&quot;[mix:lockable]&quot;
   * jcr:PrimaryType=&quot;cq:ClientLibraryFolder&quot;
   * sling:resourceType=&quot;widgets/clientlib&quot;
   * category=&quot;[&lt;category-name>]&quot;
   * dependencies=&quot;[cq.widgets]&quot;
   `Note: <category-name> is the name of the custom library (e.g. "cq.extjstraining") and is used to include the library on the page.`

1. Di seguito `clientlib` create le cartelle `css` e `js` (nt:folder).

1. Sotto `clientlib` create i file `css.txt` e `js.txt` (nt:files). Tali file .txt elencano i file inclusi nella libreria.

1. Modifica `js.txt`: deve iniziare con &#39; `#base=js`&#39; seguito dall&#39;elenco dei file che saranno aggregati dal servizio di libreria client CQ, ad esempio:

   ```
   #base=js
    components.js
    exercises.js
    CustomWidget.js
    CustomBrowseField.js
    InsertTextPlugin.js
   ```

1. Modifica `css.txt`: deve iniziare con &#39; `#base=css`&#39; seguito dall&#39;elenco dei file che saranno aggregati dal servizio di libreria client CQ, ad esempio:

   ```
   #base=css
    components.css
   ```

1. Sotto la `js` cartella, inserite i file javascript che appartengono alla libreria.

1. Sotto la `css` cartella, inserite i `.css` file e le risorse utilizzate dai file css (ad es. `my_icon.png`).

>[!NOTE]
>
>La gestione dei fogli di stile descritti in precedenza è facoltativa.

Per includere la libreria client nell’jsp del componente pagina:

* per includere sia il codice JavaScript che i fogli di stile:
   `<ui:includeClientLib categories="<category-name1>, <category-name2>, ..."/>`
dove `<category-nameX>` è il nome della libreria sul lato client.

* per includere solo il codice JavaScript:
   `<ui:includeClientLib js="<category-name>"/>`

Per ulteriori dettagli, fare riferimento alla descrizione del tag [&lt;ui:includeClientLib>](/help/sites-developing/taglib.md#lt-ui-includeclientlib) .

In alcuni casi, una libreria client dovrebbe essere disponibile solo in modalità di creazione e dovrebbe essere esclusa in modalità di pubblicazione. Può essere realizzato come segue:

```xml
    if (WCMMode.fromRequest(request) != WCMMode.DISABLED) {
        %><ui:includeClientLib categories="cq.collab.blog"/><%
    }
```

### Guida introduttiva agli esempi {#getting-started-with-the-samples}

Per seguire le esercitazioni riportate in questa pagina, installate il pacchetto denominato **Using ExtJS Widgets** in un’istanza AEM locale e create una pagina di esempio in cui i componenti saranno inclusi. A questo scopo:

1. Nell’istanza di AEM, scaricate il pacchetto denominato **Utilizzo dei widget ExtJS (v01)** da Package Share e installate il pacchetto. Crea il progetto `extjstraining` sottostante `/apps` nella directory archivio.
1. Includete la libreria client contenente gli script (js) e il foglio di stile (css) nel tag head del jsp pagina geometrixx, in quanto includerete i componenti di esempio in una nuova pagina del ramo **Geometrixx** :
in **CRXDE Lite** aprite il file `/apps/geometrixx/components/page/headlibs.jsp` e aggiungete la `cq.extjstraining` categoria al `<ui:includeClientLib>` tag esistente come segue:
   `%><ui:includeClientLib categories="apps.geometrixx-main, cq.extjstraining"/><%`
1. Create una nuova pagina nel ramo **Geometrixx** qui sotto `/content/geometrixx/en/products` e chiamatela **utilizzando i widgetJS**.
1. Passate alla modalità di progettazione e aggiungete tutti i componenti del gruppo denominato **Utilizzo dei widgetJS** alla progettazione di Geometrixx
1. Torna alla modalità di modifica: i componenti del gruppo **Utilizzo dei widget** ExtJS sono disponibili nella barra laterale.

>[!NOTE]
>
>Gli esempi presenti in questa pagina si basano sul contenuto di esempio Geometrixx, che non viene più fornito con AEM, dopo essere stato sostituito da We.Retail. Per informazioni su come scaricare e installare Geometrixx, consultate il documento [We.Retail Reference Implementation](/help/sites-developing/we-retail.md#we-retail-geometrixx) .

### Finestre di dialogo di base {#basic-dialogs}

Le finestre di dialogo vengono in genere utilizzate per modificare il contenuto, ma possono anche visualizzare solo informazioni. Un modo semplice per visualizzare una finestra di dialogo completa è accedere alla relativa rappresentazione in formato json. A tale scopo, indicate il browser in uso per:

`https://localhost:4502/<path-to-dialog>.-1.json`

Il primo componente del gruppo **Utilizzo dei widget** ExtJS nella barra laterale è denominato **1. Nozioni di base sulle** finestre di dialogo e comprende quattro finestre di dialogo di base, integrate con widget predefiniti e senza logica JavaScript personalizzata. Le finestre di dialogo sono memorizzate di seguito `/apps/extjstraining/components/dialogbasics`. Le finestre di dialogo di base sono:

* la finestra di dialogo Completa ( `full` nodo): viene visualizzata una finestra con 3 schede, ciascuna con 2 campi di testo.
* la finestra di dialogo Pannello singolo ( `singlepanel` nodo): viene visualizzata una finestra con 1 scheda con 2 campi di testo.
* la finestra di dialogo Pannello multiplo ( `multipanel` nodo): la visualizzazione è la stessa della finestra di dialogo Completa, ma viene creata in modo diverso.
* la finestra di dialogo Progettazione ( `design` nodo): visualizza una finestra con 2 schede. La prima scheda include un campo di testo, un menu a discesa e un&#39;area di testo comprimibile. La seconda scheda dispone di un campo con 4 campi di testo e un campo comprimibile con 2 campi di testo.

Includete il **1. Finestra di dialogo Nozioni di base** nella pagina di esempio:

1. Aggiungete il **1. Nozioni di base sulle** finestre di dialogo per visualizzare la pagina di esempio dalla scheda **Utilizzo dei widget** ExtJS nella barra **laterale**.
1. Il componente visualizza un titolo, un testo e un collegamento **PROPERTIES** : fate clic sul collegamento per visualizzare le proprietà del paragrafo memorizzato nella directory archivio. Fate nuovamente clic sul collegamento per nascondere le proprietà.

Il componente viene visualizzato come segue:

![chlimage_1-60](assets/chlimage_1-60.png)

#### Esempio 1: Finestra di dialogo completa {#example-full-dialog}

Nella finestra di dialogo **Completa** viene visualizzata una finestra con tre schede, ciascuna con due campi di testo. Si tratta della finestra di dialogo predefinita del componente **Dialog Basics** . Le sue caratteristiche sono:

* È definito da un nodo: tipo node = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`.
* Visualizza 3 schede (tipo di nodo = `cq:Panel`).
* Ogni scheda ha 2 campi di testo (tipo di nodo = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`).
* È definito dal nodo:
   `/apps/extjstraining/components/dialogbasics/full`
* Viene eseguito il rendering in formato JSON richiedendo:
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/full.-1.json`

La finestra di dialogo viene visualizzata come segue:

![screen_shot_2012-01-31at45411pm](assets/screen_shot_2012-01-31at45411pm.png)

#### Esempio 2: Finestra di dialogo Pannello singolo {#example-single-panel-dialog}

Nella finestra di dialogo **Pannello** singolo viene visualizzata una finestra con una scheda contenente due campi di testo. Le sue caratteristiche sono:

* Visualizza 1 scheda (tipo di nodo = `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`)
* La scheda ha due campi di testo (tipo di nodo = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`)
* È definito dal nodo:
   `/apps/extjstraining/components/dialogbasics/singlepanel`
* Viene eseguito il rendering in formato json richiedendo:
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/singlepanel.-1.json`
* Un vantaggio rispetto alla finestra di dialogo **** completa è che è necessaria una minore configurazione.
* Utilizzo consigliato: per finestre di dialogo semplici che visualizzano informazioni o che contengono solo alcuni campi.

Per utilizzare la finestra di dialogo Pannello singolo:

1. Sostituisce la finestra di dialogo del componente **Finestra di dialogo Nozioni di base** con la finestra di dialogo Pannello **** singolo:
   1. In **CRXDE Lite**, eliminare il nodo: `/apps/extjstraining/components/dialogbasics/dialog`
   1. Fate clic su **Salva tutto** per salvare le modifiche.
   1. Copia il nodo: `/apps/extjstraining/components/dialogbasics/singlepanel`
   1. Incolla il nodo copiato di seguito: `/apps/extjstraining/components/dialogbasics`
   1. Selezionare il nodo: `/apps/extjstraining/components/dialogbasics/Copy of singlepanel`e rinominarlo `dialog`.
1. Modificate il componente: la finestra di dialogo viene visualizzata come segue:

![screen_shot_2012-01-31at45952pm](assets/screen_shot_2012-01-31at45952pm.png)

#### Esempio 3: Finestra di dialogo multipannello {#example-multi-panel-dialog}

La finestra di dialogo **Pannello** multiplo ha la stessa visualizzazione della finestra di dialogo **Completa** , ma è costruita in modo diverso. Le sue caratteristiche sono:

* È definito da un nodo (tipo di nodo = `cq:Dialog`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`).
* Visualizza 3 schede (tipo di nodo = `cq:Panel`).
* Ogni scheda ha 2 campi di testo (tipo di nodo = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`).
* È definito dal nodo:
   `/apps/extjstraining/components/dialogbasics/multipanel`
* Viene eseguito il rendering in formato json richiedendo:
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/multipanel.-1.json`
* Un vantaggio rispetto al Dialogo **** completo è che ha una struttura semplificata.
* Utilizzo consigliato: per finestre di dialogo con più schede.

Per utilizzare la finestra di dialogo Pannello multiplo:

1. Sostituisce la finestra di dialogo del componente **Finestra di dialogo Nozioni di base** con la finestra di dialogo **Pannello** multiplo:
seguite i passaggi descritti per l&#39; [esempio 2: Finestra di dialogo Pannello singolo](#example-single-panel-dialog)
1. Modificate il componente: la finestra di dialogo viene visualizzata come segue:

![screen_shot_2012-01-31at50119pm](assets/screen_shot_2012-01-31at50119pm.png)

#### Esempio 4: Finestra di dialogo RTF {#example-rich-dialog}

Nella finestra di dialogo **Rich** (Rich) è visualizzata una finestra con due schede. La prima scheda include un campo di testo, un menu a discesa e un&#39;area di testo comprimibile. La seconda scheda presenta un campo con quattro campi di testo e un campo comprimibile con due campi di testo. Le sue caratteristiche sono:

* È definito da un nodo (tipo di nodo = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Visualizza 2 schede (tipo di nodo = `cq:Panel`).
* La prima scheda ha un ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` widget con un ` [textfield](/help/sites-developing/xtypes.md#textfield)` e un ` [selection](/help/sites-developing/xtypes.md#selection)` widget con 3 opzioni, e un comprimibile ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` con un ` [textarea](/help/sites-developing/xtypes.md#textarea)` widget.
* La seconda scheda è dotata di un ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` widget con 4 ` [textfield](/help/sites-developing/xtypes.md#textfield)` widget e un comprimibile `dialogfieldset` con 2 ` [textfield](/help/sites-developing/xtypes.md#textfield)` widget.
* È definito dal nodo:
   `/apps/extjstraining/components/dialogbasics/rich`
* Viene eseguito il rendering in formato json richiedendo:
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/rich.-1.json`

Per utilizzare la finestra di dialogo **Rich** :

1. Sostituire la finestra di dialogo del componente **Finestra di dialogo Nozioni di base** con la finestra di dialogo **RTF** :
seguite i passaggi descritti per l&#39; [esempio 2: Finestra di dialogo Pannello singolo](#example-single-panel-dialog)
1. Modificate il componente: la finestra di dialogo viene visualizzata come segue:

![screen_shot_2012-01-31at50429pm](assets/screen_shot_2012-01-31at50429pm.png) ![screen_shot_2012-01-31at50519pm](assets/screen_shot_2012-01-31at50519pm.png)

### Finestre di dialogo dinamiche {#dynamic-dialogs}

Il secondo componente del gruppo **Utilizzo dei widget** ExtJS nella barra laterale è denominato **2. Dialoghi** dinamici e includono tre finestre di dialogo dinamiche costruite con widget predefiniti e **con logica** JavaScript personalizzata. Le finestre di dialogo sono memorizzate di seguito `/apps/extjstraining/components/dynamicdialogs`. Le finestre di dialogo dinamiche sono:

* finestra di dialogo Switch Tabs ( `switchtabs` nodo): viene visualizzata una finestra con due schede. La prima scheda dispone di una selezione di pulsanti di scelta con tre opzioni: quando è selezionata un&#39;opzione, viene visualizzata una scheda relativa all&#39;opzione. La seconda scheda contiene due campi di testo.
* la finestra di dialogo arbitraria ( `arbitrary` nodo): viene visualizzata una finestra con una scheda. Nella scheda è presente un campo da cui rilasciare o caricare una risorsa e un campo in cui sono visualizzate informazioni sulla pagina contenitore e sulla risorsa, se vi si fa riferimento.
* finestra di dialogo Attiva/disattiva campi ( `togglefield` nodo): viene visualizzata una finestra con una scheda. La scheda dispone di una casella di controllo: quando viene selezionato, viene visualizzato un set di campi con due campi di testo.

Per includere il **2. Finestra di dialogo** dinamica nella pagina di esempio:

1. Aggiungete il **2. Finestra di dialogo** dinamica nella pagina di esempio dalla scheda **Utilizzo dei widget** ExtJS nella barra **laterale**.
1. Il componente visualizza un titolo, un testo e un collegamento **PROPERTIES** : fare clic per visualizzare le proprietà del paragrafo memorizzato nella directory archivio. Fate di nuovo clic per nascondere le proprietà.

Il componente viene visualizzato come segue:

![chlimage_1-61](assets/chlimage_1-61.png)

#### Esempio 1: Finestra di dialogo Cambia schede {#example-switch-tabs-dialog}

Nella finestra di dialogo **Switch Tabs** (Switch Tabs) è visualizzata una finestra con due schede. La prima scheda dispone di una selezione di pulsanti di scelta con tre opzioni: quando è selezionata un&#39;opzione, viene visualizzata una scheda relativa all&#39;opzione. La seconda scheda contiene due campi di testo.

Le sue caratteristiche principali sono:

* È definito da un nodo (tipo di nodo = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Visualizza 2 schede (tipo di nodo = `cq:Panel`): 1 scheda di selezione, la seconda scheda dipende dalla selezione nella prima scheda (3 opzioni).
* Sono disponibili 3 schede facoltative (tipo di nodo = `cq:Panel`), ognuna con 2 campi di testo (tipo di nodo = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`). Viene visualizzata una sola scheda opzionale alla volta.
* È definito dal `switchtabs` nodo in:
   `/apps/extjstraining/components/dynamicdialogs/switchtabs`
* Viene eseguito il rendering in formato json richiedendo:
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/switchtabs.-1.json`

La logica è implementata tramite i listener di eventi e il codice JavaScript come segue:

* Il nodo di dialogo ha un listener &quot; `beforeshow`&quot; che nasconde tutte le schede facoltative prima della visualizzazione della finestra di dialogo:
   `beforeshow="function(dialog){Ejst.x2.manageTabs(dialog.items.get(0));}"`
   `dialog.items.get(0)` ottiene la scheda contenente il pannello di selezione e i 3 pannelli opzionali.
* L&#39; `Ejst.x2` oggetto è definito nel `exercises.js` file in:
   `/apps/extjstraining/clientlib/js/exercises.js`
* Nel `Ejst.x2.manageTabs()` metodo, poiché il valore di `index` è -1, tutte le schede facoltative sono nascoste (i va da 1 a 3).
* Nella scheda di selezione sono presenti due listener: una che mostra la scheda selezionata quando la finestra di dialogo viene caricata (evento&quot; `loadcontent`&quot;) e una che mostra la scheda selezionata quando la selezione viene modificata (evento&quot; `selectionchanged`&quot;):
   `loadcontent="function(field,rec,path){Ejst.x2.showTab(field);}"`
   `selectionchanged="function(field,value){Ejst.x2.showTab(field);}"`
* Nel `Ejst.x2.showTab()` metodo:
   `field.findParentByType('tabpanel')` ottiene la scheda contenente tutte le schede ( `field` rappresenta il widget di selezione)
   `field.getValue()` ottiene il valore della selezione, ad esempio: tab2
   `Ejst.x2.manageTabs()` visualizza la scheda selezionata.
* Ogni scheda opzionale ha un listener che nasconde la scheda sull&#39;evento &quot; `render`&quot;:
   `render="function(tab){Ejst.x2.hideTab(tab);}"`
* Nel `Ejst.x2.hideTab()` metodo:
   `tabPanel` è la scheda che contiene tutte le schede
   `index` è l&#39;indice della scheda opzionale
   `tabPanel.hideTabStripItem(index)` nasconde la scheda

Viene visualizzato come segue:

![screen_shot_2012-02-01at114745am](assets/screen_shot_2012-02-01at114745am.png)

#### Esempio 2: Dialogo arbitrario {#example-arbitrary-dialog}

Molto spesso viene visualizzata una finestra di dialogo con il contenuto del componente sottostante. La finestra di dialogo qui descritta, denominata **finestra di dialogo arbitraria** , estrae il contenuto da un altro componente.

Nella finestra di dialogo **arbitrario** viene visualizzata una finestra con una scheda. La scheda presenta due campi: uno per rilasciare o caricare una risorsa e uno per visualizzare informazioni sulla pagina contenitore e sulla risorsa, se esiste un riferimento.

Le sue caratteristiche principali sono:

* È definito da un nodo (tipo di nodo = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Visualizza 1 widget del pannello tabulazioni (tipo di nodo = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`) con 1 pannello (tipo di nodo = `cq:Panel`)
* Il pannello ha un widget smartfile (tipo di nodo = `cq:Widget`, xtype = ` [smartfile](/help/sites-developing/xtypes.md#smartfile)`) e un widget di disegno proprietario (tipo di nodo = `cq:Widget`, xtype = ` [ownerdraw](/help/sites-developing/xtypes.md#ownerdraw)`)
* È definito dal `arbitrary` nodo in:
   `/apps/extjstraining/components/dynamicdialogs/arbitrary`
* Viene eseguito il rendering in formato json richiedendo:
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/arbitrary.-1.json`

La logica è implementata tramite i listener di eventi e il codice JavaScript come segue:

* Il widget di proprietà dispone di un listener &quot; `loadcontent`&quot; che mostra informazioni sulla pagina contenente il componente e la risorsa a cui fa riferimento il widget smartfile quando il contenuto viene caricato:
   `loadcontent="function(field,rec,path){Ejst.x2.showInfo(field,rec,path);}"`
   `field` è impostato con l&#39;oggetto ownerdraw
   `path` è impostato con il percorso del contenuto del componente (ad es.: /content/geometrixx/it/products/triangle/ui-tutorial/jcr:content/par/dynamicdialogs)
* L&#39; `Ejst.x2` oggetto è definito nel `exercises.js` file in:
   `/apps/extjstraining/clientlib/js/exercises.js`
* Nel `Ejst.x2.showInfo()` metodo:
   `pagePath` è il percorso della pagina contenente il componente
   `pageInfo` rappresenta le proprietà della pagina in formato json
   `reference` è il percorso della risorsa di riferimento
   `metadata` rappresenta i metadati della risorsa in formato json
   `ownerdraw.getEl().update(html);` visualizza il codice HTML creato nella finestra di dialogo

Per utilizzare la finestra di dialogo **arbitrario** :

1. Sostituire la finestra di dialogo del componente Dialogo **** dinamico con la finestra di dialogo **arbitrario** :
seguite i passaggi descritti per l&#39; [esempio 2: Finestra di dialogo Pannello singolo](#example-single-panel-dialog)
1. Modificate il componente: la finestra di dialogo viene visualizzata come segue:

![screen_shot_2012-02-01at115300 am](assets/screen_shot_2012-02-01at115300am.png)

#### Esempio 3: Attiva/Disattiva finestra di dialogo Campi {#example-toggle-fields-dialog}

Nella finestra di dialogo **Attiva/disattiva campi** viene visualizzata una finestra con una scheda. La scheda dispone di una casella di controllo: quando viene selezionato, viene visualizzato un set di campi con due campi di testo.

Le sue caratteristiche principali sono:

* È definito da un nodo (tipo di nodo = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Visualizza 1 widget del pannello tabulazioni (tipo di nodo = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#textpanel)`) con 1 pannello (tipo di nodo = `cq:Panel`).
* Il pannello dispone di un widget di selezione/casella di controllo (tipo di nodo = `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`, tipo = ` [checkbox](/help/sites-developing/xtypes.md#checkbox)`) e di un widget di tipo dialogfieldghforma comprimibile (tipo di nodo = `cq:Widget`, xtype = ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`) nascosto per impostazione predefinita, con 2 widget campo di testo (tipo di nodo = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`).
* È definito dal `togglefields` nodo in:
   `/apps/extjstraining/components/dynamicdialogs/togglefields`
* Viene eseguito il rendering in formato json richiedendo:
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/togglefields.-1.json`

La logica è implementata tramite i listener di eventi e il codice JavaScript come segue:

* nella scheda di selezione sono presenti due listener: uno che mostra lo stato di dialogfieldè quando il contenuto viene caricato (&quot;evento&quot; `loadcontent`&quot;) e uno che mostra lo stato di dialogfieldità quando la selezione viene modificata (&quot; evento `selectionchanged`&quot;):
   `loadcontent="function(field,rec,path){Ejst.x2.toggleFieldSet(field);}"`
   `selectionchanged="function(field,value){Ejst.x2.toggleFieldSet(field);}"`
* L&#39; `Ejst.x2` oggetto è definito nel `exercises.js` file in:
   `/apps/extjstraining/clientlib/js/exercises.js`
* Nel `Ejst.x2.toggleFieldSet()` metodo:
   `box` è l&#39;oggetto selezione
   `panel` è il pannello che contiene la selezione e i widget di dialogfieldset
   `fieldSet` è l&#39;oggetto dialogfieldset
   `show` è il valore della selezione (true o false) in base a &#39; `show`&#39; viene visualizzato o meno il valore dialogfielddell

Per utilizzare la finestra di dialogo **Attiva/disattiva campi** :

1. Sostituire la finestra di dialogo del componente Finestra di dialogo **** dinamica con la finestra di dialogo **Attiva campi** :
seguite i passaggi descritti per l&#39; [esempio 2: Finestra di dialogo Pannello singolo](#example-single-panel-dialog)
1. Modificate il componente: la finestra di dialogo viene visualizzata come segue:

![screen_shot_2012-02-01at115518am](assets/screen_shot_2012-02-01at115518am.png)

### Widget personalizzati {#custom-widgets}

I widget forniti con AEM dovrebbero includere la maggior parte dei casi di utilizzo. Tuttavia, a volte potrebbe essere necessario creare un widget personalizzato per soddisfare un requisito specifico del progetto. È possibile creare widget personalizzati estendendone quelli esistenti. Per iniziare a utilizzare questa personalizzazione, il pacchetto **Using ExtJS Widgets** include tre finestre di dialogo che utilizzano tre widget personalizzati diversi:

* la finestra di dialogo Campo multiplo ( `multifield` nodo) visualizza una finestra con una scheda. La scheda dispone di un widget multicampo personalizzato con due campi: un menu a discesa con due opzioni e un campo di testo. Poiché si basa sul `multifield` widget out-of-the-box (che dispone solo di un campo di testo), ha tutte le funzioni del `multifield` widget.
* la finestra di dialogo Sfoglia struttura ( `treebrowse` nodo) visualizza una finestra con una scheda contenente un widget di ricerca percorso: quando si fa clic sulla freccia, si apre una finestra in cui è possibile esplorare una gerarchia e selezionare un elemento. Il percorso dell’elemento viene quindi aggiunto al campo percorso e viene mantenuto alla chiusura della finestra di dialogo.
* una finestra di dialogo basata sul plug-in Editor Rich Text ( `rteplugin` nodo) che aggiunge un pulsante personalizzato all&#39;Editor Rich Text per inserire del testo personalizzato nel testo principale. È costituito da un `richtext` widget (RTE) e da una funzione personalizzata che viene aggiunta tramite il meccanismo plug-in RTE.

I widget personalizzati e il plug-in sono inclusi nel componente denominato **3. Widget** personalizzati del pacchetto **Using ExtJS Widgets** . Per includere questo componente nella pagina di esempio:

1. Aggiungete il **3. Il componente Widget** personalizzato viene inviato alla pagina di esempio dalla scheda **Utilizzo dei widget** ExtJS nella barra **laterale**.
1. Il componente visualizza un titolo, un testo e, quando si fa clic sul collegamento **PROPERTIES** , le proprietà del paragrafo memorizzato nella directory archivio. Facendo di nuovo clic le proprietà vengono nascoste.
Il componente viene visualizzato come segue:

![chlimage_1-62](assets/chlimage_1-62.png)

#### Esempio 1: Widget multicampo personalizzato {#example-custom-multifield-widget}

Nella finestra di dialogo **personalizzata basata su widget multicampo** viene visualizzata una finestra con una scheda. La scheda dispone di un widget multicampo personalizzato che, a differenza di quello standard con un campo, ha due campi: un menu a discesa con due opzioni e un campo di testo.

Finestra di dialogo **Custom Multifield** basata su:

* È definito da un nodo (tipo di nodo = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Visualizza 1 widget del pannello tabulazioni (tipo di nodo = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`) contenente un pannello (tipo di nodo = `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`).
* Il pannello ha un `multifield` widget (tipo di nodo = `cq:Widget`, xtype = ` [multifield](/help/sites-developing/xtypes.md#multifield)`).
* Il `multifield` widget ha un file config (tipo di nodo = `nt:unstructured`, xtype = `ejstcustom`, optionsProvider = `Ejst.x3.provideOptions`) basato sul xtype personalizzato &#39; `ejstcustom`&#39;:
   * &#39; `fieldconfig`&#39; è un&#39;opzione di configurazione dell&#39; ` [CQ.form.MultiField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MultiField)` oggetto.
   * &#39; `optionsProvider`&#39; è una configurazione del `ejstcustom` widget. Viene impostato con il `Ejst.x3.provideOptions` metodo definito in `exercises.js` :
      `/apps/extjstraining/clientlib/js/exercises.js`
e restituisce 2 opzioni.
* È definito dal `multifield` nodo in:
   `/apps/extjstraining/components/customwidgets/multifield`
* Viene eseguito il rendering in formato json richiedendo:
   `https://localhost:4502/apps/extjstraining/components/customwidgets/multifield.-1.json`

Il widget multicampo personalizzato (xtype = `ejstcustom`):

* È un oggetto JavaScript denominato `Ejst.CustomWidget`.
* È definito nel file `CustomWidget.js` javascript in:
   `/apps/extjstraining/clientlib/js/CustomWidget.js`
* Estende il ` [CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField)` widget.
* Contiene 3 campi: `hiddenField` (Campo di testo), `allowField` (Casella combinata) e `otherField` (Campo di testo)
* Ignora `CQ.Ext.Component#initComponent` per aggiungere 3 campi:
   * `allowField` è un oggetto [CQ.form.Selection](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Selection) di tipo &#39;select&#39;. optionsProvider è una configurazione dell&#39;oggetto Selection creata con la configurazione optionsProvider del CustomWidget definito nella finestra di dialogo
   * `otherField` è un oggetto [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField)
* Sostituisce i metodi `setValue``getValue` e `getRawValue` di [CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField) per impostare e recuperare il valore di CustomWidget con il formato:
   `<allowField value>/<otherField value>, e.g.: 'Bla1/hello'`.
* Si registra come &#39; `ejstcustom`&#39; xtype:
   `CQ.Ext.reg('ejstcustom', Ejst.CustomWidget);`

La finestra di dialogo **personalizzata basata su widget multicampo** viene visualizzata come segue:

![screen_shot_2012-02-01at115840am](assets/screen_shot_2012-02-01at115840am.png)

#### Esempio 2: Widget personalizzato con righe iniziali {#example-custom-treebrowse-widget}

La finestra di dialogo personalizzata basata su widget **Sfoglia** presenta una finestra con una scheda contenente un widget di ricerca del percorso personalizzato: quando si fa clic sulla freccia, si apre una finestra in cui è possibile esplorare una gerarchia e selezionare un elemento. Il percorso dell’elemento viene quindi aggiunto al campo percorso e viene mantenuto alla chiusura della finestra di dialogo.

Finestra di dialogo delle risorse personalizzate:

* È definito da un nodo (tipo di nodo = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Visualizza 1 widget del pannello tabulazioni (tipo di nodo = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`) contenente un pannello (tipo di nodo = `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`).
* Il pannello ha un widget personalizzato (tipo di nodo = `cq:Widget`, xtype = `ejstbrowse`)
* È definito dal `treebrowse` nodo in:
   `/apps/extjstraining/components/customwidgets/treebrowse`
* Viene eseguito il rendering in formato json richiedendo:
   `https://localhost:4502/apps/extjstraining/components/customwidgets/treebrowse.-1.json`

Il widget personalizzato della barra degli strumenti (xtype = `ejstbrowse`):

* È un oggetto JavaScript denominato `Ejst.CustomWidget`.
* È definito nel file `CustomBrowseField.js` javascript in:
   `/apps/extjstraining/clientlib/js/CustomBrowseField.js`
* Si Estende ` [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)`.
* Definisce una finestra di ricerca denominata `browseWindow`.
* Sostituisce ` [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)#onTriggerClick` la finestra di ricerca quando si fa clic sulla freccia.
* Definisce un oggetto [CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel) :
   * Ottiene i dati chiamando il servlet registrato a `/bin/wcm/siteadmin/tree.json`.
   * La radice è &quot; `apps/extjstraining`&quot;.
* Definisce un `window` oggetto ( ` [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)`):
   * Basato sul pannello predefinito.
   * Con un pulsante **OK** che imposta il valore del percorso selezionato e nasconde il pannello.
* La finestra è ancorata sotto il campo **Percorso** .
* Il percorso selezionato viene passato dal campo di ricerca alla finestra dell&#39; `show` evento.
* Si registra come &#39; `ejstbrowse`&#39; xtype:
   `CQ.Ext.reg('ejstbrowse', Ejst.CustomBrowseField);`

Per utilizzare la finestra di dialogo basata su widget **personalizzato** Sfoglia:

1. Sostituisce la finestra di dialogo del componente Widget **** personalizzati con la finestra di dialogo **Sfoglia** personalizzata:
seguite i passaggi descritti per l&#39; [esempio 2: Finestra di dialogo Pannello singolo](#example-single-panel-dialog)
1. Modificate il componente: la finestra di dialogo viene visualizzata come segue:

![screen_shot_2012-02-01 alle120104pm](assets/screen_shot_2012-02-01at120104pm.png)

#### Esempio 3: Plug-in Editor Rich Text (RTE) {#example-rich-text-editor-rte-plug-in}

La finestra di dialogo **Rich Text Editor (RTE) basata sui plug-in** è una finestra di dialogo basata su Editor Rich Text con un pulsante personalizzato per l&#39;inserimento di testo personalizzato tra parentesi quadre. Il testo personalizzato può essere analizzato da una logica lato server (non implementata in questo esempio), ad esempio per aggiungere del testo definito nel percorso specificato:

Finestra di dialogo basata sui plug-in **RTE** :

* È definito dal nodo reteplugin in in:
   `/apps/extjstraining/components/customwidgets/rteplugin`
* Viene eseguito il rendering in formato json richiedendo:
   `https://localhost:4502/apps/extjstraining/components/customwidgets/rteplugin.-1.json`
* Il `rtePlugins` nodo ha un nodo figlio `inserttext` (tipo di nodo = `nt:unstructured`) a cui viene assegnato il nome dopo il plug-in. Ha una proprietà denominata `features`, che definisce quale delle funzioni plug-in è disponibile per l’editor Rich Text.

Il plug-in RTE:

* È un oggetto JavaScript denominato `Ejst.InsertTextPlugin`.
* È definito nel file `InsertTextPlugin.js` javascript in:
   `/apps/extjstraining/clientlib/js/InsertTextPlugin.js`
* Estende l&#39; ` [CQ.form.rte.plugins.Plugin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)` oggetto.
* I seguenti metodi definiscono l&#39; ` [CQ.form.rte.plugins.Plugin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)` oggetto e vengono sostituiti nel plug-in di implementazione:
   * `getFeatures()` restituisce un array di tutte le funzioni che il plug-in rende disponibili.
   * `initializeUI()` aggiunge il nuovo pulsante alla barra degli strumenti dell’editor Rich Text.
   * `notifyPluginConfig()` visualizza titolo e testo quando il pulsante è tenuto premuto.
   * `execute()` viene chiamato quando si fa clic sul pulsante ed esegue l&#39;azione del plug-in: viene visualizzata una finestra che consente di definire il testo da includere.
* `insertText()` inserisce un testo utilizzando l&#39;oggetto finestra di dialogo corrispondente `Ejst.InsertTextPlugin.Dialog` (vedere dopo).
* `executeInsertText()` viene chiamato dal `apply()` metodo della finestra di dialogo, che viene attivato quando si fa clic sul pulsante **OK** .
* Si registra come plug-in &#39; `inserttext`&#39;:
   `CQ.form.rte.plugins.PluginRegistry.register("inserttext", Ejst.InsertTextPlugin);`
* l&#39; `Ejst.InsertTextPlugin.Dialog` oggetto definisce la finestra di dialogo che viene aperta quando si fa clic sul pulsante del plug-in. La finestra di dialogo è composta da un pannello, un modulo, un campo di testo e due pulsanti (**OK** e **Annulla**).

Per utilizzare la finestra di dialogo basata sul plug-in Editor **Rich Text (RTE)** :

1. Sostituisce la finestra di dialogo del componente Widget **** personalizzati con la finestra di dialogo basata sul plug-in Editor di testo **RTF (Rich Text Editor)** :
seguite i passaggi descritti per l&#39; [esempio 2: Finestra di dialogo Pannello singolo](#example-single-panel-dialog)
1. Modificate il componente.
1. Fate clic sull’ultima icona a destra (quella con quattro frecce). Immettete un percorso e fate clic su **OK**:
Il percorso viene visualizzato tra parentesi ([ ]).
1. Fare clic su **OK** per chiudere l&#39;Editor Rich Text.

La finestra di dialogo basata sul plug-in Editor **** Rich Text (RTE) viene visualizzata come segue:

![screen_shot_2012-02-01 alle 12.20254pm](assets/screen_shot_2012-02-01at120254pm.png)

>[!NOTE]
>
>Questo esempio mostra solo come implementare la parte client della logica: i segnaposto (*[testo]*) devono quindi essere analizzati esplicitamente sul lato server (ad es. nel JSP componente).

### Panoramica struttura {#tree-overview}

L&#39;oggetto out-of-the-box ` [CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)` offre una rappresentazione ad albero dell&#39;interfaccia utente di dati strutturati ad albero. Il componente Panoramica struttura incluso nel pacchetto **Utilizzo dei widget** ExtJS mostra come utilizzare l&#39; `TreePanel` oggetto per visualizzare una struttura JCR sotto un determinato percorso. La finestra stessa può essere agganciata/sganciata. In questo esempio, la logica della finestra è incorporata nel jsp del componente tra i tag &lt;script>&lt;/script>.

Per includere il componente **Panoramica** albero nella pagina di esempio:

1. Aggiungete il **4. Panoramica** albero nella pagina di esempio dalla scheda **Utilizzo dei widget** ExtJS nella barra **laterale**.
1. Viene visualizzato il componente:
   * un titolo, con del testo
   * un collegamento **PROPERTIES** : fare clic per visualizzare le proprietà del paragrafo memorizzato nella directory archivio. Fate di nuovo clic per nascondere le proprietà.
   * una finestra mobile con una struttura ad albero che può essere espansa.

Il componente viene visualizzato come segue:

![screen_shot_2012-02-01 alle120639pm](assets/screen_shot_2012-02-01at120639pm.png)

Il componente Panoramica struttura:

* È definito in:
   `/apps/extjstraining/components/treeoverview`

* La finestra di dialogo consente di impostare le dimensioni della finestra e di agganciare o sganciare la finestra (vedere i dettagli di seguito).

Il componente jsp:

* Recupera la larghezza, l&#39;altezza e le proprietà agganciate dalla directory archivio.
* Visualizza del testo sul formato dei dati della panoramica della struttura.
* Incorpora la logica della finestra nel componente jsp tra i tag javascript.
* È definito in:
   `apps/extjstraining/components/treeoverview/content.jsp`

Il codice JavaScript incorporato nel componente jsp:

* Definisce un `tree` oggetto cercando di recuperare una finestra ad albero dalla pagina.
* Se la finestra che visualizza la struttura non esiste, `treePanel` ([CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)) viene creato:
   * `treePanel` contiene i dati utilizzati per creare la finestra.
   * I dati vengono recuperati chiamando il servlet registrato in:
      `/bin/wcm/siteadmin/tree.json`
* Il `beforeload` listener verifica che il nodo su cui si fa clic sia caricato.
* L&#39; `root` oggetto imposta il percorso `apps/extjstraining` come radice della struttura.
* `tree` ( ` [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)`) è impostato in base alla definizione predefinita `treePanel`, ed è visualizzato con:
   `tree.show();`
* Se la finestra esiste già, viene visualizzata in base alle proprietà larghezza, altezza e agganciata recuperate dalla directory archivio.

Finestra di dialogo del componente:

* Visualizza 1 scheda con 2 campi per impostare le dimensioni (larghezza e altezza) della finestra della panoramica struttura e 1 campo per agganciare/sganciare la finestra
* È definito da un nodo (tipo di nodo = `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`).
* Il pannello ha un widget di dimensioni (tipo di nodo = `cq:Widget`, xtype = ` [sizefield](/help/sites-developing/xtypes.md#sizefield)`) e un widget di selezione (tipo di nodo = `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`, tipo = `radio`) con 2 opzioni (true/false)
* È definito dal nodo della finestra di dialogo in:
   `/apps/extjstraining/components/treeoverview/dialog`
* Viene eseguito il rendering in formato json richiedendo:
   `https://localhost:4502/apps/extjstraining/components/treeoverview/dialog.-1.json`
* Visualizza come segue:

![screen_shot_2012-02-01 alle120745pm](assets/screen_shot_2012-02-01at120745pm.png)

### Panoramica sulla griglia {#grid-overview}

Un pannello Griglia rappresenta i dati in un formato tabulare di righe e colonne. È composto dai seguenti elementi:

* Store: il modello che contiene i record di dati (righe).
* Modello colonna: il trucco delle colonne.
* Visualizza : incapsula l&#39;interfaccia utente.
* Modello di selezione : il comportamento di selezione.

Il componente Panoramica griglia incluso nel pacchetto **Utilizzo dei widget** ExtJS mostra come visualizzare i dati in formato tabulare:

* Nell&#39;esempio 1 vengono utilizzati dati statici.
* Nell&#39;esempio 2 vengono utilizzati i dati recuperati dall&#39;archivio.

Per includere il componente Panoramica griglia nella pagina di esempio:

1. Aggiungete il **5. Panoramica** griglia sulla pagina di esempio dalla scheda **Utilizzo dei widget** ExtJS nella barra **laterale**.
1. Viene visualizzato il componente:
   * un titolo con del testo
   * un collegamento **PROPERTIES** : fare clic per visualizzare le proprietà del paragrafo memorizzato nella directory archivio. Fate di nuovo clic per nascondere le proprietà.
   * una finestra mobile contenente dati in formato tabulare.

Il componente viene visualizzato come segue:

![screen_shot_2012-02-01 alle121109pm](assets/screen_shot_2012-02-01at121109pm.png)

#### Esempio 1: Griglia predefinita {#example-default-grid}

Nella versione standard, il componente **Panoramica** griglia presenta una finestra con dati statici in formato tabulare. In questo esempio, la logica è incorporata nel jsp componente in due modi:

* la logica generica è definita tra i tag &lt;script>&lt;/script>
* la logica specifica è disponibile in un file .js separato ed è collegata nel jsp. Questa configurazione consente di passare facilmente tra le due logiche (statiche/dinamiche) commentando i tag &lt;script> desiderati.

Il componente Panoramica sulla griglia:

* È definito in:
   `/apps/extjstraining/components/gridoverview`
* La finestra di dialogo consente di impostare le dimensioni della finestra e di agganciare o sganciare la finestra.

Il componente jsp:

* Recupera la larghezza, l&#39;altezza e le proprietà agganciate dalla directory archivio.
* Visualizza parte del testo come introduzione al formato dati della panoramica della griglia.
* Fa riferimento al codice JavaScript che definisce l&#39;oggetto GridPanel:
   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script>`
   `defaultgrid.js` definisce alcuni dati statici come base per l&#39;oggetto GridPanel.
* Incorpora il codice JavaScript tra i tag javascript che definisce l&#39;oggetto Window che utilizza l&#39;oggetto GridPanel.
* È definito in:
   `apps/extjstraining/components/gridoverview/content.jsp`

Il codice JavaScript incorporato nel componente jsp:

* Definisce l’ `grid` oggetto cercando di recuperare il componente finestra dalla pagina:
   `var grid = CQ.Ext.getCmp("<%= node.getName() %>-grid");`
* Se `grid` non esiste, viene definito un oggetto [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) ( `gridPanel`) chiamando il `getGridPanel()` metodo (vedere di seguito). Questo metodo è definito in `defaultgrid.js`.
* `grid` è un ` [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)` oggetto, basato sul GridPanel predefinito, ed è visualizzato: `grid.show();`
* Se `grid` esiste già, viene visualizzato in base alle proprietà larghezza, altezza e agganciato recuperate dalla directory archivio.

Il file javascript ( `defaultgrid.js`) a cui si fa riferimento nel componente jsp definisce il `getGridPanel()` metodo chiamato dallo script incorporato nel JSP e restituisce un ` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` oggetto, basato su dati statici. La logica è la seguente:

* `myData` è un array di dati statici formattati come tabella di 5 colonne e 4 righe.
* `store` è un `CQ.Ext.data.Store` oggetto che consuma `myData`.
* `store` è caricato in memoria:
   `store.load();`
* `gridPanel` è un ` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` oggetto che consuma `store`:
   * le larghezze delle colonne vengono sempre riproporzioni:
      `forceFit: true`
   * è possibile selezionare una sola riga alla volta:
      `singleSelect:true`

#### Esempio 2: Griglia di ricerca di riferimento {#example-reference-search-grid}

Quando installate il pacchetto, `content.jsp` il componente Panoramica **sulla** griglia presenta una griglia basata su dati statici. È possibile modificare il componente per visualizzare una griglia con le seguenti caratteristiche:

* Ha tre colonne.
* Si basa sui dati recuperati dall&#39;archivio chiamando un servlet.
* È possibile modificare le celle dell&#39;ultima colonna. Il valore viene mantenuto in una `test` proprietà sotto il nodo definito dal percorso visualizzato nella prima colonna.

Come spiegato nella sezione precedente, l&#39;oggetto window ottiene il proprio ` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` oggetto chiamando il `getGridPanel()` metodo definito nel `defaultgrid.js` file in corrispondenza di `/apps/extjstraining/components/gridoverview/defaultgrid.js`. Il componente **Grid Overview **fornisce un&#39;implementazione diversa per il `getGridPanel()` metodo, definito nel `referencesearch.js` file in `/apps/extjstraining/components/gridoverview/referencesearch.js`. Cambiando il file .js a cui si fa riferimento nel jsp componente, la griglia sarà basata sui dati recuperati dal repository.

Cambiate il file .js a cui viene fatto riferimento nel componente jsp:

1. In **CRXDE Lite**, nel `content.jsp` file del componente, commentare la riga che include il `defaultgrid.js` file, in modo che abbia il seguente aspetto:
   `<!-- script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script-->`
1. Rimuovere il commento dalla riga che include il `referencesearch.js` file, in modo che abbia l&#39;aspetto seguente:
   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/referencesearch.js"></script>`
1. Salva le modifiche.
1. Aggiorna la pagina di esempio.

Il componente viene visualizzato come segue:

![screen_shot_2012-02-01 alle121429pm](assets/screen_shot_2012-02-01at121429pm.png)

Il codice javascript a cui si fa riferimento nel componente jsp ( `referencesearch.js`) definisce il `getGridPanel()` metodo chiamato dal componente jsp e restituisce un ` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` &#39;oggetto, in base ai dati recuperati dinamicamente dall&#39;archivio. La logica in `referencesearch.js` definisce alcuni dati dinamici come base per il GridPanel:

* `reader` è un ` [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader)`oggetto che legge la risposta del servlet in formato json per 3 colonne.
* `cm` è un ` [CQ.Ext.grid.ColumnModel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel)` oggetto per 3 colonne.
Le celle di colonna &quot;Test&quot; possono essere modificate in base alla definizione con un editor:
   `editor: new [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField)({})`
* le colonne sono ordinabili:
   `cm.defaultSortable = true;`
* `store` è un ` [CQ.Ext.data.GroupingStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)` oggetto:
   * ottiene i suoi dati chiamando il servlet registrato in &quot; `/bin/querybuilder.json`&quot; con alcuni parametri utilizzati per filtrare la query
   * è basato su `reader`, definito in precedenza
   * la tabella è ordinata in base alla colonna &#39;**jcr:path**&#39; in ordine crescente
* `gridPanel` è un ` [CQ.Ext.grid.EditorGridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)` oggetto che può essere modificato:
   * si basa sul modello predefinito `store` e sul modello a colonne `cm`
   * è possibile selezionare una sola riga alla volta:
      `sm: new [CQ.Ext.grid.RowSelectionModel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.RowSelectionModel)({singleSelect:true})`
   * il `afteredit` listener si accerta che dopo la modifica di una cella nella colonna &quot;**Test**&quot;:
      * la proprietà &#39; `test`&#39; del nodo nel percorso definito dalla colonna &quot;**jcr:path**&quot; è impostata nell&#39;archivio con il valore della cella
      * se il POST ha esito positivo, il valore viene aggiunto all&#39; `store` oggetto, altrimenti viene rifiutato
