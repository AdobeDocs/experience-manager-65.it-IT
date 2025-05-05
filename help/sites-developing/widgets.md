---
title: Utilizzo ed estensione dei widget (interfaccia classica)
description: L'interfaccia Web di Adobe Experience Manager utilizza l'AJAX e altre tecnologie di browser moderne per consentire agli autori di modificare e formattare i contenuti WYSIWYG direttamente sulla pagina Web
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
docset: aem65
exl-id: 56a9591c-cd78-42e8-a5d7-6b48581d6af6
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '4896'
ht-degree: 0%

---

# Utilizzo ed estensione dei widget (interfaccia classica){#using-and-extending-widgets-classic-ui}

>[!NOTE]
>
>Questa pagina descrive l’utilizzo dei widget nell’interfaccia utente classica, che in AEM 6.4 è stata dichiarata obsoleta.
>
>L&#39;Adobe consiglia di utilizzare la [interfaccia utente touch](/help/sites-developing/touch-ui-concepts.md) moderna basata su [interfaccia utente Coral](/help/sites-developing/touch-ui-concepts.md#coral-ui) e [interfaccia utente Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components).

L’interfaccia web di Adobe Experience Manager (AEM) utilizza l’AJAX e altre moderne tecnologie di browser per consentire agli autori di modificare e formattare i contenuti WYSIWYG direttamente sulla pagina web.

AEM utilizza la libreria di widget [ExtJS](https://www.sencha.com/), che fornisce elementi dell&#39;interfaccia utente altamente sofisticati che funzionano in tutti i browser più importanti e consentono la creazione di esperienze dell&#39;interfaccia utente di livello desktop.

Questi widget sono inclusi nell&#39;AEM e, oltre ad essere utilizzati dall&#39;AEM stesso, possono essere utilizzati da qualsiasi sito web creato utilizzando l&#39;AEM.

Per un riferimento completo di tutti i widget disponibili in AEM, consulta la [documentazione API widget](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) o l&#39;[elenco degli xtype esistenti](/help/sites-developing/xtypes.md). Inoltre, molti esempi che mostrano come utilizzare il framework ExtJS sono disponibili sul sito [Sencha](https://examples.sencha.com/extjs/7.6.0/), il proprietario del framework.

Questa pagina fornisce informazioni su come utilizzare ed estendere i widget. Descrive innanzitutto come [includere codice lato client in una pagina](#including-the-client-sided-code-in-a-page). Vengono quindi descritti alcuni componenti di esempio creati per illustrare alcuni utilizzi e estensioni di base. Questi componenti sono disponibili nel pacchetto **Using ExtJS Widgets** in **Package Share**.

Il pacchetto include esempi di:

* [Finestre di dialogo di base](#basic-dialogs) create con widget predefiniti.
* [Finestre di dialogo dinamiche](#dynamic-dialogs) create con widget predefiniti e logica JavaScript personalizzata.
* Finestre di dialogo basate su [widget personalizzati](#custom-widgets).
* Un [pannello struttura](#tree-overview) che visualizza una struttura JCR sotto un determinato percorso.
* Un [pannello griglia](#grid-overview) che visualizza i dati in formato tabulare.

>[!NOTE]
>
>L&#39;interfaccia utente classica di Adobe Experience Manager è basata su [ExtJS 3.4.0](https://extjs.cachefly.net/ext-3.4.0/docs/).

## Inclusione del codice lato client in una pagina {#including-the-client-sided-code-in-a-page}

Il codice JavaScript lato client e il codice del foglio di stile devono essere inseriti in una libreria client.

Per creare una libreria client:

1. Crea un nodo sotto `/apps/<project>` con le seguenti proprietà:

   * name=&quot;clientlib&quot;
   * jcr:mixinTypes=&quot;[mix:lockable]&quot;
   * jcr:primaryType=&quot;cq:ClientLibraryFolder&quot;
   * sling:resourceType=&quot;widgets/clientlib&quot;
   * Categories=&quot;[&lt;nome-categoria>]&quot;
   * dependencies=&quot;[cq.widgets]&quot;

   `Note: <category-name> is the name of the custom library (for example, "cq.extjstraining") and is used to include the library on the page.`

1. Di seguito `clientlib` creare le cartelle `css` e `js` (nt:folder).

1. Di seguito `clientlib` creare i file `css.txt` e `js.txt` (nt:files). Tali file .txt elencano i file inclusi nella libreria.

1. Modifica `js.txt`: deve iniziare con &#39;`#base=js`&#39; seguito dall&#39;elenco dei file aggregati dal servizio libreria client CQ, ad esempio:

   ```
   #base=js
    components.js
    exercises.js
    CustomWidget.js
    CustomBrowseField.js
    InsertTextPlugin.js
   ```

1. Modifica `css.txt`: deve iniziare con &#39;`#base=css`&#39; seguito dall&#39;elenco dei file aggregati dal servizio libreria client CQ, ad esempio:

   ```
   #base=css
    components.css
   ```

1. Sotto la cartella `js`, inserire i file JavaScript che appartengono alla raccolta.

1. Sotto la cartella `css`, inserire i file `.css` e le risorse utilizzate dai file css, ad esempio `my_icon.png`.

>[!NOTE]
>
>La gestione dei fogli di stile descritti in precedenza è facoltativa.

Per includere la libreria client nel componente jsp della pagina:

* per includere sia il codice JavaScript che i fogli di stile:
  `<ui:includeClientLib categories="<category-name1>, <category-name2>, ..."/>`
dove `<category-nameX>` è il nome della libreria lato client.

* per includere solo il codice JavaScript:
  `<ui:includeClientLib js="<category-name>"/>`

Per ulteriori dettagli, consulta la descrizione del [&lt;ui:includeClientLib>](/help/sites-developing/taglib.md#lt-ui-includeclientlib) tag.&lt;/ui:includeClientLib>

A volte un libreria client dovrebbe essere disponibile solo in modalità autore e dovrebbe essere escluso in modalità pubblicare. Può essere ottenuto come segue:

```xml
    if (WCMMode.fromRequest(request) != WCMMode.DISABLED) {
        %><ui:includeClientLib categories="cq.collab.blog"/><%
    }
```

### Guida introduttiva con gli esempi {#getting-started-with-the-samples}

Per seguire i tutorial su questa pagina, installa il pacchetto **Utilizzo dei widget ExtJS** in un&#39;istanza AEM locale e crea una pagina di esempio in cui sono inclusi i componenti. A tale scopo, eseguire le operazioni seguenti:

1. Nell&#39;istanza AEM scaricare il pacchetto denominato **Utilizzo dei widget ExtJS (v01)** da Condivisione pacchetti e installarlo. Crea il progetto `extjstraining` sotto `/apps` nell&#39;archivio.
1. Includi la libreria client contenente gli script (js) e il foglio di stile (css) nel tag head della jsp della pagina Geometrixx. Stai per includere i componenti di esempio in una nuova pagina del ramo **Geometrixx**:
in **CRXDE Liti** apri il file `/apps/geometrixx/components/page/headlibs.jsp` e aggiungi la categoria `cq.extjstraining` al tag `<ui:includeClientLib>` esistente come segue:
   `%><ui:includeClientLib categories="apps.geometrixx-main, cq.extjstraining"/><%`
1. Crea una pagina nel ramo **Geometrixx** sotto `/content/geometrixx/en/products` e chiamala **utilizzando i widget ExtJS**.
1. Passa alla modalità progettazione e aggiungi tutti i componenti del gruppo denominato **Utilizzo di widget ExtJS** alla progettazione di Geometrixx
1. Torna indietro in modalità di modifica: i componenti del gruppo **con widget ExtJS** sono disponibili nel Sidekick.

>[!NOTE]
>
>Gli esempi in questa pagina si basano sul contenuto del Geometrixx, che non viene più fornito con AEM ed è stato sostituito da We.Retail. Per informazioni su come scaricare e installare Geometrixx, consulta la [Implementazione di riferimento We.Retail](/help/sites-developing/we-retail.md#we-retail-geometrixx).

### Finestre di dialogo di base {#basic-dialogs}

Le finestre di dialogo vengono in genere utilizzate per modificare il contenuto, ma possono anche visualizzare informazioni. Un modo semplice per visualizzare una finestra di dialogo completa è accedere alla sua rappresentazione in formato JSON. A tale scopo, puntare il browser a:

`https://localhost:4502/<path-to-dialog>.-1.json`

Il primo componente del Sidekick **Utilizzo dei widget ExtJS** è denominato **1. Nozioni di base sulle finestre di dialogo** e include quattro finestre di dialogo di base create con widget predefiniti e senza logica JavaScript personalizzata. Le finestre di dialogo sono memorizzate sotto `/apps/extjstraining/components/dialogbasics`. Le finestre di dialogo di base sono:

* la finestra di dialogo Completa (nodo `full`): visualizza una finestra con tre schede, ciascuna con due campi di testo.
* la finestra di dialogo Pannello singolo (nodo `singlepanel`): visualizza una finestra con una scheda contenente due campi di testo.
* Finestra di dialogo a più pannelli (nodo `multipanel`): la visualizzazione è la stessa della finestra di dialogo Completa, ma viene generata in modo diverso.
* La finestra di dialogo per progettazione (nodo `design`): visualizza una finestra con due schede. La prima scheda contiene un campo di testo, un menu a discesa e un&#39;area di testo comprimibile. La seconda scheda contiene un set di campi con quattro campi di testo e un set di campi comprimibili con due campi di testo.

Includi **1. Componente di base** della finestra di dialogo nella pagina di esempio:

1. Aggiungi **1. Componente di base per finestre di dialogo** nella pagina di esempio dalla scheda **Utilizzo di widget ExtJS** nel **Sidekick**.
1. Il componente visualizza un titolo, del testo e un collegamento **PROPRIETÀ**. Selezionando il collegamento vengono visualizzate le proprietà del paragrafo memorizzato nel repository. Seleziona nuovamente il collegamento per nascondere le proprietà.

Il componente viene visualizzato come segue:

![chlimage_1-60](assets/chlimage_1-60.png)

#### Esempio 1: finestra di dialogo completa {#example-full-dialog}

Nella finestra di dialogo **Completo** viene visualizzata una finestra con tre schede, ognuna con due campi di testo. È la finestra di dialogo predefinita del componente **Nozioni di base sulla finestra di dialogo**. Le sue caratteristiche sono:

* È definito da un nodo: tipo di nodo = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`.
* Visualizza tre schede (tipo di nodo = `cq:Panel`).
* Ogni scheda ha due campi di testo (tipo nodo = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`).
* È definito dal nodo:
  `/apps/extjstraining/components/dialogbasics/full`
* Viene eseguito il rendering in formato JSON richiedendo:
  `https://localhost:4502/apps/extjstraining/components/dialogbasics/full.-1.json`

La finestra di dialogo viene visualizzata come segue:

![schermata_shot_2012-01-31at45411pm](assets/screen_shot_2012-01-31at45411pm.png)

#### Esempio 2: finestra di dialogo con pannello singolo {#example-single-panel-dialog}

La finestra di dialogo **Pannello singolo** visualizza una finestra con una scheda contenente due campi di testo. Le sue caratteristiche sono:

* Visualizza una scheda (tipo di nodo = `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`)
* La scheda ha due campi di testo (tipo nodo = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`)
* È definito dal nodo:
  `/apps/extjstraining/components/dialogbasics/singlepanel`
* Viene eseguito in formato json richiedendo:
  `https://localhost:4502/apps/extjstraining/components/dialogbasics/singlepanel.-1.json`
* Un vantaggio rispetto alla **Finestra di dialogo completa** è la minore necessità di configurazione.
* Utilizzo consigliato: per finestre di dialogo semplici che visualizzano informazioni o che hanno solo pochi campi.

Per utilizzare la finestra di dialogo Pannello singolo:

1. Sostituisci la finestra di dialogo del componente **Nozioni di base sul dialogo** con la finestra di dialogo **Pannello singolo**:
   1. In **CRXDE Liti**, eliminare il nodo: `/apps/extjstraining/components/dialogbasics/dialog`
   1. Fai clic su **Salva tutto** per salvare le modifiche.
   1. Copia il nodo: `/apps/extjstraining/components/dialogbasics/singlepanel`
   1. Incolla il nodo copiato di seguito: `/apps/extjstraining/components/dialogbasics`
   1. Selezionare il nodo `/apps/extjstraining/components/dialogbasics/Copy of singlepanel` e rinominarlo `dialog`.
1. Modifica il componente: la finestra di dialogo viene visualizzata come segue:

![schermata_shot_2012-01-31at45952pm](assets/screen_shot_2012-01-31at45952pm.png)

#### Esempio 3: finestra di dialogo a più pannelli {#example-multi-panel-dialog}

La finestra di dialogo **Multi Panel** ha la stessa visualizzazione della finestra di dialogo **Full**, ma viene generata in modo diverso. Le sue caratteristiche sono:

* È definito da un nodo (tipo di nodo = `cq:Dialog`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`).
* Visualizza tre schede (tipo di nodo = `cq:Panel`).
* Ogni scheda ha due campi di testo (node type = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`).
* È definito dal nodo:
  `/apps/extjstraining/components/dialogbasics/multipanel`
* Viene eseguito in formato json richiedendo:
  `https://localhost:4502/apps/extjstraining/components/dialogbasics/multipanel.-1.json`
* Uno dei vantaggi rispetto alla **Finestra di dialogo completa** è la struttura semplificata.
* Utilizzo consigliato: per finestre di dialogo con più schede.

Per utilizzare la finestra di dialogo Multipannello:

1. Sostituisci la finestra di dialogo del componente **Nozioni di base del dialogo** con la finestra di dialogo **Pannello multiplo**:
segui i passaggi descritti per [Esempio 2: Finestra di dialogo a pannello singolo](#example-single-panel-dialog)
1. Modifica il componente: la finestra di dialogo viene visualizzata come segue:

![schermata_shot_2012-01-31at50119pm](assets/screen_shot_2012-01-31at50119pm.png)

#### Esempio 4: finestra di dialogo ricca di contenuti {#example-rich-dialog}

Nella finestra di dialogo **Rich** viene visualizzata una finestra con due schede. La prima scheda contiene un campo di testo, un menu a discesa e un&#39;area di testo comprimibile. La seconda scheda contiene un set di campi con quattro campi di testo e un set di campi comprimibili con due campi di testo. Le sue caratteristiche sono:

* È definito da un nodo (tipo di nodo = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Visualizza due schede (tipo di nodo = `cq:Panel`).
* La prima scheda contiene un widget ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` con un widget ` [textfield](/help/sites-developing/xtypes.md#textfield)` e un widget ` [selection](/help/sites-developing/xtypes.md#selection)` con tre opzioni e un widget ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` comprimibile con un widget ` [textarea](/help/sites-developing/xtypes.md#textarea)`.
* La seconda scheda contiene un widget ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` con quattro widget ` [textfield](/help/sites-developing/xtypes.md#textfield)` e un widget `dialogfieldset` comprimibile con due widget ` [textfield](/help/sites-developing/xtypes.md#textfield)`.
* È definito dal nodo:
  `/apps/extjstraining/components/dialogbasics/rich`
* Viene eseguito in formato json richiedendo:
  `https://localhost:4502/apps/extjstraining/components/dialogbasics/rich.-1.json`

Per utilizzare la finestra di dialogo **Rich**:

1. Sostituisci la finestra di dialogo del componente **Nozioni di base sul dialogo** con la finestra di dialogo **Ricco**:
segui i passaggi descritti per [Esempio 2: Finestra di dialogo a pannello singolo](#example-single-panel-dialog)
1. Modifica il componente: la finestra di dialogo viene visualizzata come segue:

![screen_shot_2012-01-31at50429pm](assets/screen_shot_2012-01-31at50429pm.png) ![screen_shot_2012-01-31at50519pm](assets/screen_shot_2012-01-31at50519pm.png)

### Finestre di dialogo dinamiche {#dynamic-dialogs}

Il secondo componente del Sidekick **Utilizzo di widget ExtJS** è denominato **2. Dialoghi dinamici** e include tre dialoghi dinamici generati con widget predefiniti e **con logica JavaScript personalizzata**. Le finestre di dialogo sono memorizzate sotto `/apps/extjstraining/components/dynamicdialogs`. Le finestre di dialogo dinamiche sono:

* finestra di dialogo Cambia schede ( `switchtabs` nodo): viene visualizzata una finestra con due schede. La prima scheda dispone di una selezione di scelta con tre opzioni: quando viene selezionata un’opzione, viene visualizzata una scheda relativa all’opzione. La seconda scheda contiene due campi di testo.
* la finestra di dialogo Arbitrario (nodo `arbitrary`): visualizza una finestra con una scheda. La scheda contiene un campo per rilasciare o caricare una risorsa e un campo che visualizza alcune informazioni sulla pagina che la contiene e sulla risorsa, se presente.
* finestra di dialogo Attiva/disattiva campi (nodo `togglefield`): viene visualizzata una finestra con una scheda. La scheda ha una casella di controllo: quando è selezionata, viene visualizzato un set di campi con due campi di testo.

Per includere **2. Componente finestre di dialogo dinamiche** nella pagina di esempio:

1. Aggiungi **2. Componente Dialoghi dinamici** nella pagina di esempio dalla scheda **Utilizzo di widget ExtJS** nel **Sidekick**.
1. Il componente visualizza un titolo, del testo e un collegamento **PROPRIETÀ**. Selezionando il collegamento vengono visualizzate le proprietà del paragrafo memorizzato nel repository. Seleziona nuovamente il collegamento per nascondere le proprietà.

Il componente viene visualizzato come segue:

![chlimage_1-61](assets/chlimage_1-61.png)

#### Esempio 1: finestra di dialogo Cambia schede {#example-switch-tabs-dialog}

Nella finestra di dialogo **Cambia schede** viene visualizzata una finestra con due schede. La prima scheda dispone di una selezione di scelta con tre opzioni: quando viene selezionata un’opzione, viene visualizzata una scheda relativa all’opzione. La seconda scheda contiene due campi di testo.

Le sue caratteristiche principali sono:

* È definito da un nodo (tipo di nodo = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Visualizza due schede (tipo di nodo = `cq:Panel`): una scheda di selezione, la seconda scheda dipende dalla selezione nella prima scheda (tre opzioni).
* Dispone di tre schede facoltative (tipo di nodo = `cq:Panel`), ognuna con due campi di testo (tipo di nodo = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`). Viene visualizzata una sola scheda opzionale alla volta.
* È definito dal nodo `switchtabs` in:
  `/apps/extjstraining/components/dynamicdialogs/switchtabs`
* Viene eseguito in formato json richiedendo:
  `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/switchtabs.-1.json`

La logica viene implementata tramite i listener di eventi e il codice JavaScript come segue:

* Il nodo della finestra di dialogo ha un listener &quot; `beforeshow`&quot; che nasconde tutte le schede facoltative prima della visualizzazione della finestra di dialogo:
  `beforeshow="function(dialog){Ejst.x2.manageTabs(dialog.items.get(0));}"`
  `dialog.items.get(0)` ottiene `tabpanel` che contiene il pannello di selezione e i tre pannelli facoltativi.
* L&#39;oggetto `Ejst.x2` è definito nel file `exercises.js` in:
  `/apps/extjstraining/clientlib/js/exercises.js`
* Nel metodo `Ejst.x2.manageTabs()`, poiché il valore di `index` è -1, tutte le schede facoltative sono nascoste (i va da 1 a 3).
* La scheda di selezione dispone di due listener: uno che visualizza la scheda selezionata al caricamento della finestra di dialogo (evento `loadcontent`) e uno che visualizza la scheda selezionata quando la selezione viene modificata (evento `selectionchanged`):
  `loadcontent="function(field,rec,path){Ejst.x2.showTab(field);}"`
  `selectionchanged="function(field,value){Ejst.x2.showTab(field);}"`
* Per il metodo `Ejst.x2.showTab()`:
  `field.findParentByType('tabpanel')` ottiene `tabpanel` che contiene tutte le schede ( `field` rappresenta il widget di selezione)
  `field.getValue()` ottiene il valore della selezione, ad esempio tab2
  `Ejst.x2.manageTabs()` visualizza la scheda selezionata.
* Ogni scheda facoltativa ha un listener che nasconde la scheda sull&#39;evento &quot; `render`&quot;:
  `render="function(tab){Ejst.x2.hideTab(tab);}"`
* Per il metodo `Ejst.x2.hideTab()`:
  `tabPanel` è il `tabpanel` che contiene tutte le schede
  `index` è l&#39;indice della scheda facoltativa
  `tabPanel.hideTabStripItem(index)` nasconde la scheda

Viene visualizzato come segue:

![schermata_shot_2012-02-01at114745am](assets/screen_shot_2012-02-01at114745am.png)

#### Esempio 2: dialogo arbitrario {#example-arbitrary-dialog}

Spesso una finestra di dialogo visualizza il contenuto del componente sottostante. La finestra di dialogo qui descritta, denominata **Finestra di dialogo arbitraria**, richiama il contenuto da un componente diverso.

Nella finestra di dialogo **Arbitrario** viene visualizzata una finestra con una scheda. La scheda contiene due campi: uno per rilasciare o caricare una risorsa e uno per visualizzare alcune informazioni sulla pagina che la contiene e sulla risorsa, se ne è stato fatto riferimento.

Le sue caratteristiche principali sono:

* È definito da un nodo (tipo di nodo = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Visualizza un widget `tabpanel` (tipo nodo = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`) con un pannello (tipo nodo = `cq:Panel`)
* Il pannello ha un widget smartfile (tipo nodo = `cq:Widget`, xtype = ` [smartfile](/help/sites-developing/xtypes.md#smartfile)`) e un widget ownerdraw (tipo nodo = `cq:Widget`, xtype = ` [ownerdraw](/help/sites-developing/xtypes.md#ownerdraw)`)
* È definito dal nodo `arbitrary` in:
  `/apps/extjstraining/components/dynamicdialogs/arbitrary`
* Viene eseguito in formato json richiedendo:
  `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/arbitrary.-1.json`

La logica viene implementata tramite i listener di eventi e il codice JavaScript come segue:

* Il widget `ownerdraw` ha un listener &quot; `loadcontent`&quot; che mostra informazioni sulla pagina contenente il componente. Ossia, la risorsa a cui fa riferimento il widget smartfile al caricamento del contenuto:
  `loadcontent="function(field,rec,path){Ejst.x2.showInfo(field,rec,path);}"`
  `field` è impostato con l&#39;oggetto `ownerdraw`
  `path` è impostato con il percorso del contenuto del componente (ad esempio, `/content/geometrixx/en/products/triangle/ui-tutorial/jcr:content/par/dynamicdialogs`)
* L&#39;oggetto `Ejst.x2` è definito nel file `exercises.js` in:
  `/apps/extjstraining/clientlib/js/exercises.js`
* Per il metodo `Ejst.x2.showInfo()`:
  `pagePath` è il percorso della pagina contenente il componente;
  `pageInfo` rappresenta le proprietà della pagina in formato json;
  `reference` è il percorso della risorsa di riferimento;
  `metadata` rappresenta i metadati della risorsa in formato json;
  `ownerdraw.getEl().update(html);` visualizza l&#39;html creato nella finestra di dialogo

Per utilizzare la finestra di dialogo **Arbitrario**:

1. Sostituisci la finestra di dialogo del componente Finestra di dialogo **dinamica con la** finestra di **dialogo Arbitraria**:
seguire i passaggi descritti nell&#39;Esempio [2: Finestra di dialogo a pannello singolo](#example-single-panel-dialog)
1. Modifica il componente: La finestra di dialogo viene visualizzata come segue:

![schermata_shot_2012-02-01at115300am](assets/screen_shot_2012-02-01at115300am.png)

#### Esempio 3: finestra di dialogo Attiva/Disattiva campi {#example-toggle-fields-dialog}

Nella finestra di dialogo **Attiva/Disattiva campi** viene visualizzata una finestra con una scheda. La scheda ha una casella di controllo: quando è selezionata viene visualizzato un set di campi con due campi di testo.

Le sue caratteristiche principali sono:

* È definito da un nodo (node type = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Visualizza un `tabpanel` widget (node type = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#textpanel)`) con un pannello (node type = `cq:Panel`).
* Il pannello ha un widget selezione/casella di controllo (node type = `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`, type = ` [checkbox](/help/sites-developing/xtypes.md#checkbox)`) e un widget dialogfieldset comprimibile (node type = `cq:Widget`, xtype = ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`) che è nascosto per impostazione predefinita, con due widget campo di testo (node type = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`).
* È definito dal nodo `togglefields` in:
  `/apps/extjstraining/components/dynamicdialogs/togglefields`
* Viene eseguito in formato json richiedendo:
  `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/togglefields.-1.json`

La logica viene implementata tramite i listener di eventi e il codice JavaScript come segue:

* la scheda selezione include due listener: uno che visualizza il set di campi di dialogo quando il contenuto viene caricato (evento `loadcontent`) e uno che visualizza il set di campi di dialogo quando la selezione viene modificata (evento `selectionchanged`):
  `loadcontent="function(field,rec,path){Ejst.x2.toggleFieldSet(field);}"`
  `selectionchanged="function(field,value){Ejst.x2.toggleFieldSet(field);}"`
* L&#39;oggetto `Ejst.x2` è definito nel file `exercises.js` in:
  `/apps/extjstraining/clientlib/js/exercises.js`
* Per il metodo `Ejst.x2.toggleFieldSet()`:
  `box` è l&#39;oggetto di selezione;
  `panel` è il pannello contenente la selezione e i widget di set di campi di dialogo;
  `fieldSet` è l&#39;oggetto dialogfieldset;
  `show` è il valore della selezione (vero o falso);
in base a &#39; `show`&#39; il dialogfieldset viene visualizzato o meno

Per utilizzare la finestra di dialogo **Attiva/disattiva campi**, eseguire le operazioni seguenti:

1. Sostituisci la finestra di dialogo del componente **Finestra di dialogo dinamica** con la finestra di dialogo **Attiva/Disattiva campi**:
segui i passaggi descritti per [Esempio 2: Finestra di dialogo a pannello singolo](#example-single-panel-dialog)
1. Modifica il componente: la finestra di dialogo viene visualizzata come segue:

![schermata_shot_2012-02-01at115518am](assets/screen_shot_2012-02-01at115518am.png)

### Widget personalizzati {#custom-widgets}

I widget preconfigurati forniti con AEM devono coprire la maggior parte dei casi d’uso. Tuttavia, a volte potrebbe essere necessario creare un widget personalizzato per coprire un requisito specifico del progetto. I widget personalizzati possono essere creati estendendo quelli esistenti. Per aiutarti a iniziare con questa personalizzazione, il pacchetto **`Using ExtJS Widgets`** include tre finestre di dialogo che utilizzano tre diversi widget personalizzati:

* nella finestra di dialogo Campo multiplo (`multifield` nodo) viene visualizzata una finestra con una scheda. La scheda ha un widget multicampo personalizzato con due campi: un menu a discesa con due opzioni e un campo di testo. Poiché si basa sul widget predefinito `multifield` (che ha solo un campo di testo), presenta tutte le caratteristiche del widget `multifield`.
* nella finestra di dialogo Sfoglia struttura (nodo `treebrowse`) viene visualizzata una finestra con una scheda contenente un widget Sfoglia percorso: quando si fa clic sulla freccia, viene visualizzata una finestra in cui è possibile sfogliare una gerarchia e selezionare un elemento. Il percorso dell’elemento viene quindi aggiunto al campo percorso e viene mantenuto quando la finestra di dialogo viene chiusa.
* una finestra di dialogo basata sul plug-in dell&#39;editor Rich Text (nodo `rteplugin`) che aggiunge un pulsante personalizzato all&#39;editor Rich Text per inserire del testo personalizzato nel testo principale. È costituito da un widget `richtext` e da una funzionalità personalizzata aggiunta tramite il meccanismo del plug-in dell&#39;editor Rich Text.

I widget personalizzati e il plug-in sono inclusi nel componente denominato **3. Widget** personalizzati del **pacchetto Utilizzo di ExtJS Widgets** . Per includere questo componente nella pagina di esempio:

1. Aggiungi il **3. Widget** personalizzati nella pagina di esempio dalla **scheda Utilizzo dei widget** ExtJS nella **barra laterale**.
1. Il componente visualizza un titolo, del testo e, quando si fa clic sulla **collegare PROPRIETÀ** , le proprietà del paragrafo memorizzate nella archivio. Facendo di nuovo clic, le proprietà vengono nascoste.
Il componente viene visualizzato come segue:

![chlimage_1-62](assets/chlimage_1-62.png)

#### Esempio 1: widget multicampo personalizzato {#example-custom-multifield-widget}

Nella finestra di dialogo **Multifield personalizzato** basato su widget viene visualizzata una finestra con una scheda. La scheda ha un widget multicampo personalizzato che, a differenza di quello standard che ha un campo, ha due campi: un menu a discesa con due opzioni e un campo di testo.

Finestra di dialogo **Multifield personalizzato** basato su widget:

* È definito da un nodo (tipo di nodo = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Visualizza un widget `tabpanel` (tipo nodo = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`) contenente un pannello (tipo nodo = `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`).
* Il pannello ha un widget `multifield` (tipo di nodo = `cq:Widget`, xtype = ` [multifield](/help/sites-developing/xtypes.md#multifield)`).
* Il widget `multifield` dispone di un file fieldconfig (tipo di nodo = `nt:unstructured`, xtype = `ejstcustom`, optionsProvider = `Ejst.x3.provideOptions`) basato sull&#39;xtype personalizzato &#39; `ejstcustom`&#39;:
   * &#39;`fieldconfig`&#39; è un&#39;opzione di configurazione dell&#39;oggetto ` [CQ.form.MultiField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.MultiField)`.
   * &#39;`optionsProvider`&#39; è una configurazione del widget `ejstcustom`. È impostato con il metodo `Ejst.x3.provideOptions` definito in `exercises.js` in:

     `/apps/extjstraining/clientlib/js/exercises.js`
e restituisce due opzioni.
* È definito dal nodo `multifield` in:
  `/apps/extjstraining/components/customwidgets/multifield`
* Viene eseguito in formato json richiedendo:
  `https://localhost:4502/apps/extjstraining/components/customwidgets/multifield.-1.json`

Il widget `multifield` personalizzato (xtype = `ejstcustom`):

* È un oggetto JavaScript denominato `Ejst.CustomWidget`
* È definito nel file JavaScript `CustomWidget.js` in:
  `/apps/extjstraining/clientlib/js/CustomWidget.js`
* Estende il widget ` [CQ.form.CompositeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.CompositeField)`.
* Ha tre campi: `hiddenField` (Textfield), `allowField` (ComboBox) e `otherField` (Textfield)
* Sostituisce `CQ.Ext.Component#initComponent` per aggiungere i tre campi:
   * `allowField` è un oggetto [CQ.form.Selection](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.Selection) di tipo &#39;select&#39;. optionsProvider è una configurazione dell&#39;oggetto Selection di cui viene creata un&#39;istanza con la configurazione optionsProvider dell&#39;oggetto CustomWidget definito nella finestra di dialogo
   * `otherField` è un oggetto [CQ.Ext.form.TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TextField)
* Sostituisce i metodi `setValue`, `getValue`, e `getRawValue` di [CQ.form.CompositeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.CompositeField) per impostare e recuperare il valore di CustomWidget con il formato:
  `<allowField value>/<otherField value>, for example: 'Bla1/hello'`.
* Registra se stesso come xtype &#39; `ejstcustom`&#39;:
  `CQ.Ext.reg('ejstcustom', Ejst.CustomWidget);`

La finestra di dialogo **Multifield personalizzato** basata su widget viene visualizzata come segue:

![schermata_shot_2012-02-01at115840am](assets/screen_shot_2012-02-01at115840am.png)

#### Esempio 2: Widget personalizzato `Treebrowse` {#example-custom-treebrowse-widget}

La finestra di dialogo basata su widget personalizzato **`Treebrowse`** visualizza una finestra con una scheda contenente un widget di navigazione del percorso personalizzato. Quando si seleziona la freccia, viene visualizzata una finestra in cui è possibile esplorare una gerarchia e selezionare un elemento. Il percorso dell&#39;elemento viene quindi aggiunto al campo percorso e viene mantenuto quando la finestra di dialogo viene chiusa.

La finestra di dialogo personalizzata `treebrowse` :

* È definito da un nodo (node type = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Visualizza un widget `tabpanel` (tipo nodo = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`) contenente un pannello (tipo nodo = `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`).
* Il pannello ha un widget personalizzato (tipo di nodo = `cq:Widget`, xtype = `ejstbrowse`)
* È definito dal nodo `treebrowse` in:
  `/apps/extjstraining/components/customwidgets/treebrowse`
* Viene eseguito in formato json richiedendo:
  `https://localhost:4502/apps/extjstraining/components/customwidgets/treebrowse.-1.json`

Il widget personalizzato per la ricerca ad albero (xtype = `ejstbrowse`):

* È un oggetto JavaScript denominato `Ejst.CustomWidget`
* È definito nel file JavaScript `CustomBrowseField.js` in:
  `/apps/extjstraining/clientlib/js/CustomBrowseField.js`
* Estende ` [CQ.Ext.form.TriggerField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TriggerField)`.
* Definisce una finestra di esplorazione denominata `browseWindow`.
* Sostituisce ` [CQ.Ext.form.TriggerField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TriggerField)#onTriggerClick` per visualizzare la finestra Sfoglia quando si fa clic sulla freccia.
* Definisce un oggetto [CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.tree.TreePanel):
   * Ottiene i dati chiamando il servlet registrato in `/bin/wcm/siteadmin/tree.json`.
   * La radice è &quot; `apps/extjstraining`&quot;.
* Definisce un oggetto `window` ( ` [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window)`):
   * In base al pannello predefinito.
   * Ha un pulsante **OK** che imposta il valore del percorso selezionato e nasconde il pannello.
* La finestra è ancorata sotto il campo **Percorso**.
* Il percorso selezionato viene passato dal campo Sfoglia alla finestra nell&#39;evento `show`.
* Registra se stesso come xtype &#39; `ejstbrowse`&#39;:
  `CQ.Ext.reg('ejstbrowse', Ejst.CustomBrowseField);`

Per utilizzare la **finestra di dialogo personalizzata basata su widget albero**:

1. Sostituisci la finestra di dialogo del componente **Widget personalizzati** con la finestra di dialogo **Sfoglia di albero personalizzata**:
segui i passaggi descritti per [Esempio 2: Finestra di dialogo a pannello singolo](#example-single-panel-dialog)
1. Modifica il componente: la finestra di dialogo viene visualizzata come segue:

![schermata_shot_2012-02-01at120104pm](assets/screen_shot_2012-02-01at120104pm.png)

#### Esempio 3: plug-in dell&#39;editor Rich Text {#example-rich-text-editor-rte-plug-in}

La finestra di dialogo basata su plug-in **dell&#39;Editor** Rich Text è una finestra di dialogo basata su Editor Rich Text che dispone di un pulsante personalizzato per inserire del testo personalizzato tra parentesi quadre. Il testo personalizzato può essere analizzato da una logica lato server (non implementata in questo esempio), ad esempio, per aggiungere del testo definito nel percorso specificato:

La finestra di dialogo basata su plugin **dell&#39;Editor** Rich Text:

* È definito dal nodo del plug-in in:
  `/apps/extjstraining/components/customwidgets/rteplugin`
* Viene eseguito in formato json richiedendo:
  `https://localhost:4502/apps/extjstraining/components/customwidgets/rteplugin.-1.json`
* Il nodo `rtePlugins` ha un nodo figlio `inserttext` (tipo di nodo = `nt:unstructured`) che prende il nome dal plug-in. La proprietà `features` definisce le funzionalità del plug-in disponibili per l&#39;editor Rich Text.

Il plug-in dell’editor Rich Text:

* È un oggetto JavaScript denominato `Ejst.InsertTextPlugin`
* È definito nel file JavaScript `InsertTextPlugin.js` in:
  `/apps/extjstraining/clientlib/js/InsertTextPlugin.js`
* Estende l&#39;oggetto ` [CQ.form.rte.plugins.Plugin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)`.
* I seguenti metodi definiscono l&#39;oggetto ` [CQ.form.rte.plugins.Plugin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)` e vengono sostituiti nel plug-in di implementazione:
   * `getFeatures()` restituisce un array di tutte le funzionalità rese disponibili dal plug-in.
   * `initializeUI()` aggiunge il nuovo pulsante alla barra degli strumenti dell&#39;editor Rich Text.
   * `notifyPluginConfig()` visualizza il titolo e il testo quando si passa il puntatore sul pulsante.
   * `execute()` viene chiamato quando si fa clic sul pulsante ed esegue l&#39;azione del plug-in: viene visualizzata una finestra utilizzata per definire il testo da includere.
* `insertText()` inserisce un testo utilizzando l&#39;oggetto finestra di dialogo corrispondente `Ejst.InsertTextPlugin.Dialog` (vedere in seguito).
* `executeInsertText()` è chiamato dal metodo `apply()` della finestra di dialogo, che viene attivato quando si fa clic sul pulsante **OK**.
* Registra se stesso come plug-in &#39; `inserttext`&#39;:
  `CQ.form.rte.plugins.PluginRegistry.register("inserttext", Ejst.InsertTextPlugin);`
* l&#39;oggetto `Ejst.InsertTextPlugin.Dialog` definisce la finestra di dialogo aperta quando si fa clic sul pulsante del plug-in. La finestra di dialogo è costituita da un pannello, un modulo, un campo di testo e due pulsanti (**OK** e **Annulla**).

Per utilizzare la finestra di dialogo basata sul plug-in **Editor Rich Text**:

1. Sostituisci la finestra di dialogo del componente **Widget personalizzati** con la finestra di dialogo basata sul plug-in **Rich Text Editor (RTE)**:
segui i passaggi descritti per [Esempio 2: Finestra di dialogo a pannello singolo](#example-single-panel-dialog)
1. Modifica il componente.
1. Fai clic sull’ultima icona a destra (quella con quattro frecce). Immettere un percorso e fare clic su **OK**:
Il percorso viene visualizzato tra parentesi quadre ([ ]).
1. Fai clic su **OK** per chiudere l&#39;editor Rich Text.

La finestra di dialogo basata su plug-in **dell&#39;Editor** Rich Text viene visualizzata come segue:

![screen_shot_2012-02-01AT120254PM](assets/screen_shot_2012-02-01at120254pm.png)

>[!NOTE]
>
>Questo esempio mostra solo come implementare la parte lato client della logica: i segnaposto (*[testo]*) devono quindi essere analizzati esplicitamente sul lato server (ad esempio, nel componente JSP).

### Panoramica struttura {#tree-overview}

L&#39;oggetto predefinito ` [CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)` fornisce una rappresentazione dell&#39;interfaccia utente con struttura ad albero dei dati con struttura ad albero. Il componente Tree Overview incluso nel **pacchetto Using ExtJS Widgets** mostra come utilizzare l&#39;oggetto `TreePanel` per visualizzare un albero JCR sotto un determinato percorso. La finestra stessa può essere agganciata o sganciata. In questo esempio, la logica della finestra è incorporata nel componente jsp tra &lt;script> i tag.

Per includere il componente Panoramica **struttura** nella pagina di esempio:

1. Aggiungi il **4. Componente Panoramica** struttura alla pagina di esempio dalla **scheda Utilizzo dei widget** ExtJS nella **barra laterale**.
1. Il componente visualizza:
   * un titolo, con del testo
   * un collegamento **PROPRIETÀ**: fare clic per visualizzare le proprietà del paragrafo memorizzato nell&#39;archivio. Fai di nuovo clic su per nascondere le proprietà.
   * una finestra mobile con una rappresentazione ad albero dell’archivio che può essere espansa.

Il componente viene visualizzato come segue:

![schermata_shot_2012-02-01at120639pm](assets/screen_shot_2012-02-01at120639pm.png)

Il componente Panoramica struttura:

* È definito in:
  `/apps/extjstraining/components/treeoverview`

* La finestra di dialogo consente di impostare le dimensioni della finestra e di ancorarla o disancorarla (vedere i dettagli riportati di seguito).

Il componente jsp:

* Recupera le proprietà width, height e docked dal repository.
* Visualizza parte del testo sul formato dei dati della panoramica della struttura.
* Incorpora la logica della finestra nel jsp del componente tra i tag JavaScript.
* È definito in:
  `apps/extjstraining/components/treeoverview/content.jsp`

Il codice JavaScript incorporato nel componente jsp:

* Definisce un oggetto `tree` tentando di recuperare una finestra della struttura dalla pagina.
* Se la finestra che visualizza la struttura non esiste, viene creato `treePanel` ([CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)):
   * `treePanel` contiene i dati utilizzati per creare la finestra.
   * I dati vengono recuperati chiamando il servlet registrato in:

     `/bin/wcm/siteadmin/tree.json`
* Il listener `beforeload` verifica che il nodo selezionato sia caricato.
* L&#39;oggetto `root` imposta il percorso `apps/extjstraining` come directory principale della struttura.
* `tree` ( ` [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window)`) è impostato in base a `treePanel` predefinito e viene visualizzato con:
  `tree.show();`
* Se la finestra esiste, viene visualizzata in base alla larghezza, all&#39;altezza e alle proprietà ancorate recuperate dal repository.

La finestra di dialogo del componente:

* Visualizza una scheda con due campi per impostare le dimensioni (larghezza e altezza) della finestra della panoramica della struttura ad albero e un campo per ancorare/disancorare la finestra
* È definito da un nodo (tipo di nodo = `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`).
* Il pannello ha un widget sizefield (tipo nodo = `cq:Widget`, xtype = ` [sizefield](/help/sites-developing/xtypes.md#sizefield)`) e un widget di selezione (tipo nodo = `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`, tipo = `radio`) con due opzioni (true/false)
* È definito dal nodo della finestra di dialogo in:
  `/apps/extjstraining/components/treeoverview/dialog`
* Viene eseguito in formato json richiedendo:
  `https://localhost:4502/apps/extjstraining/components/treeoverview/dialog.-1.json`
* Visualizza come segue:

![schermata_shot_2012-02-01at120745pm](assets/screen_shot_2012-02-01at120745pm.png)

### Panoramica sulla griglia {#grid-overview}

Un pannello Griglia rappresenta i dati in un formato tabulare di righe e colonne. È composto dai seguenti elementi:

* Store : il modello contenente i record di dati (righe).
* Modello colonna : il componente colonna.
* Visualizza : incapsula l&#39;interfaccia utente.
* Modello di selezione : il comportamento di selezione.

Il componente Panoramica griglia incluso nel pacchetto **Utilizzo di widget ExtJS** mostra come visualizzare i dati in formato tabulare:

* Nell&#39;esempio 1 vengono utilizzati dati statici.
* Nell’esempio 2 vengono utilizzati i dati recuperati dall’archivio.

Per includere il componente Panoramica griglia nella pagina di esempio:

1. Aggiungi **5. Componente Panoramica griglia** nella pagina di esempio dalla scheda **Utilizzo di widget ExtJS** nel **Sidekick**.
1. Il componente visualizza:
   * un titolo con testo
   * un collegamento **PROPRIETÀ**: fare clic per visualizzare le proprietà del paragrafo memorizzato nell&#39;archivio. Fai di nuovo clic su per nascondere le proprietà.
   * una finestra mobile contenente dati in formato tabulare.

Il componente viene visualizzato come segue:

![schermata_shot_2012-02-01at121109pm](assets/screen_shot_2012-02-01at121109pm.png)

#### Esempio 1: griglia predefinita {#example-default-grid}

Nella sua versione predefinita, il **componente Panoramica** griglia visualizza una finestra con dati statici in formato tabulare. In questo esempio, la logica è incorporata nel componente jsp in due modi:

* La logica generica è definita tra &lt;script> i tag
* la logica specifica è disponibile in un file .js separato ed è collegata a nel jsp. Questa configurazione consente di passare da una logica all&#39;altra (statica/dinamica) commentando i tag &lt;script> desiderati.

Il componente Panoramica griglia:

* È definito in:
  `/apps/extjstraining/components/gridoverview`
* La finestra di dialogo consente di impostare le dimensioni della finestra e di agganciare o sganciare la finestra.

Il componente jsp:

* Recupera la larghezza, l&#39;altezza e le proprietà ancorate dal archivio.
* Visualizza del testo come introduzione al formato di dati di panoramica griglia.
* Fa riferimento al codice JavaScript che definisce l&#39;oggetto GridPanel:
  `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script>`
  `defaultgrid.js` definisce alcuni dati statici come base per l&#39;oggetto GridPanel.
* Incorpora il codice JavaScript tra i tag JavaScript che definisce l&#39;oggetto Window che utilizza l&#39;oggetto GridPanel.
* È definito in:
  `apps/extjstraining/components/gridoverview/content.jsp`

Il codice JavaScript incorporato nel componente jsp:

* Definisce l&#39;oggetto `grid` tentando di recuperare il componente finestra dalla pagina:
  `var grid = CQ.Ext.getCmp("<%= node.getName() %>-grid");`
* Se `grid` non esiste, viene definito un oggetto [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) ( `gridPanel`) chiamando il metodo `getGridPanel()` (vedere di seguito). Metodo definito in `defaultgrid.js`.
* `grid` è un oggetto ` [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window)` basato sul GridPanel predefinito ed è visualizzato: `grid.show();`
* Se `grid` esiste, viene visualizzato in base alla larghezza, all&#39;altezza e alle proprietà ancorate recuperate dal repository.

Il file JavaScript ( `defaultgrid.js`) a cui si fa riferimento nel componente jsp definisce il metodo `getGridPanel()` chiamato dallo script incorporato nel JSP e restituisce un oggetto ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)`, basato su dati statici. La logica è la seguente:

* `myData` è un array di dati statici formattati come tabella di cinque colonne e quattro righe.
* `store` è un oggetto `CQ.Ext.data.Store` che utilizza `myData`.
* `store` è caricato in memoria:
  `store.load();`
* `gridPanel` è un oggetto ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` che utilizza `store`:
   * le larghezze delle colonne vengono sempre riproporzionate:

     `forceFit: true`
   * è possibile selezionare una sola riga alla volta:

     `singleSelect:true`

#### Esempio 2: griglia di ricerca di riferimento {#example-reference-search-grid}

Quando si installa il pacchetto, `content.jsp` del componente **Panoramica griglia** visualizza una griglia basata su dati statici. È possibile modificare il componente per visualizzare una griglia con le seguenti caratteristiche:

* Ha tre colonne.
* Si basa sui dati recuperati dall’archivio chiamando un servlet.
* È possibile modificare le celle dell&#39;ultima colonna. Il valore viene mantenuto in una proprietà `test` sotto il nodo definito dal percorso visualizzato nella prima colonna.

Come spiegato nella sezione precedente, l&#39;oggetto window ottiene l&#39;oggetto ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` chiamando il metodo `getGridPanel()` definito nel file `defaultgrid.js` in `/apps/extjstraining/components/gridoverview/defaultgrid.js`. Il componente **Panoramica griglia &#x200B;** fornisce un&#39;implementazione diversa per il metodo `getGridPanel()`, definito nel file `referencesearch.js` in `/apps/extjstraining/components/gridoverview/referencesearch.js`. Cambiando il file .js a cui si fa riferimento nel componente jsp, la griglia si basa sui dati recuperati dall’archivio.

Cambia il file .js a cui si fa riferimento nel jsp del componente:

1. In **CRXDE Liti**, nel file `content.jsp` del componente, commentare la riga che include il file `defaultgrid.js`, in modo che appaia come segue:
   `<!-- script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script-->`
1. Rimuovere il commento dalla riga che include il file `referencesearch.js`, in modo che venga visualizzato come segue:
   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/referencesearch.js"></script>`
1. Salva le modifiche.
1. Aggiorna la pagina di esempio.

Il componente viene visualizzato come segue:

![schermata_shot_2012-02-01at121429pm](assets/screen_shot_2012-02-01at121429pm.png)

Il codice JavaScript a cui si fa riferimento nel componente jsp ( `referencesearch.js`) definisce il metodo `getGridPanel()` chiamato dal componente jsp e restituisce un oggetto ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)`, in base ai dati recuperati dinamicamente dall&#39;archivio. La logica in `referencesearch.js` definisce alcuni dati dinamici come base per GridPanel:

* `reader` è un oggetto ` [CQ.Ext.data.JsonReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.JsonReader)` che legge la risposta del servlet in formato json per tre colonne.
* `cm` è un oggetto ` [CQ.Ext.grid.ColumnModel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel)` per tre colonne.
Le celle della colonna &quot;Test&quot; possono essere modificate così come sono definite con un editor:
  `editor: new [CQ.Ext.form.TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TextField)({})`
* le colonne possono essere ordinate:
  `cm.defaultSortable = true;`
* `store` è un oggetto ` [CQ.Ext.data.GroupingStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)`:
   * ottiene i dati chiamando il servlet registrato in &quot; `/bin/querybuilder.json`&quot; con alcuni parametri utilizzati per filtrare la query
   * si basa su `reader`, definito in precedenza
   * la tabella è ordinata in base alla colonna &#39;**jcr:path**&#39; in ordine crescente
* `gridPanel` è un oggetto ` [CQ.Ext.grid.EditorGridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)` che può essere modificato:
   * è basato su `store` predefinito e sul modello di colonna `cm`
   * è possibile selezionare una sola riga alla volta:

     `sm: new [CQ.Ext.grid.RowSelectionModel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.RowSelectionModel)({singleSelect:true})`
   * il listener `afteredit` si assicura che dopo la modifica di una cella nella colonna &quot;**Test**&quot;:
      * la proprietà &#39;`test`&#39; del nodo nel percorso definito dalla colonna &quot;**jcr:path**&quot; è impostata nell&#39;archivio con il valore della cella
      * se il POST ha esito positivo, il valore viene aggiunto all&#39;oggetto `store`, altrimenti viene rifiutato
