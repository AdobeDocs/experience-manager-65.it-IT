---
title: Sviluppo dell’editor in blocco
description: L’assegnazione tag consente di categorizzare e organizzare i contenuti
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 8753aaab-959f-459b-bdb6-057cbe05d480
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1833'
ht-degree: 1%

---

# Sviluppo dell’editor in blocco{#developing-the-bulk-editor}

Questa sezione descrive come sviluppare lo strumento Bulk Editor e come estendere il componente Product List, basato sull’Bulk Editor.

## Parametri di query dell’editor in blocco {#bulk-editor-query-parameters}

Quando si lavora con l’editor in blocco, è possibile aggiungere diversi parametri di query all’URL per chiamare l’editor in blocco con una configurazione specifica. Se desideri utilizzare sempre l’Editor collettivo con una determinata configurazione, ad esempio nel componente Elenco prodotti, devi modificare `bulkeditor.jsp` (in /libs/wcm/core/components/bulkeditor) o crea un componente con la configurazione specifica. Le modifiche apportate utilizzando i parametri di query non sono permanenti.

Ad esempio, se digiti quanto segue nell’URL del browser:

`https://<servername><port_number>/etc/importers/bulkeditor.html?rootPath=/content/geometrixx/en&queryParams=geometrixx&initialSearch=true&hrp=true`

L’Editor collettivo viene visualizzato senza **Percorso directory principale** field as hrp=true nasconde il campo. Con il parametro hrp=false, viene visualizzato il campo (il valore predefinito).

Di seguito è riportato un elenco dei parametri di query dell’editor di massa:

>[!NOTE]
>
>Ogni parametro può avere un nome lungo e breve. Ad esempio, il nome lungo per il percorso della directory principale di ricerca è `rootPath`, quello breve è `rp`. Se il nome lungo non è definito, quello breve viene letto dalla richiesta.

<table>
 <tbody>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p> Parametro</p> <p>(nome lungo/nome breve)<br /> </p> </td>
   <td> Tipo <br /> </td>
   <td> Descrizione <br /> </td>
  </tr>
  <tr>
   <td> rootPath/rp<br /> </td>
   <td> Stringa </td>
   <td> percorso directory principale di ricerca</td>
  </tr>
  <tr>
   <td> queryParams / qp<br /> </td>
   <td> Stringa</td>
   <td> query di ricerca</td>
  </tr>
  <tr>
   <td> contentMode/cm<br /> </td>
   <td> Booleano</td>
   <td> se true, la modalità contenuto è abilitata<br /> </td>
  </tr>
  <tr>
   <td> colsValue/cv<br /> </td>
   <td> String[]</td>
   <td> proprietà ricercate (valori selezionati da colonneCaselle di controllo visualizzate in Selection)</td>
  </tr>
  <tr>
   <td> extraCols/ec<br /> </td>
   <td> String[]</td>
   <td> proprietà ricercate aggiuntive (visualizzate in un campo di testo separato da virgole)</td>
  </tr>
  <tr>
   <td> initialSearch / is<br /> </td>
   <td> Booleano</td>
   <td> se true, la query viene eseguita al caricamento della pagina<br /> </td>
  </tr>
  <tr>
   <td> colsSelection/cs<br /> </td>
   <td> String[]</td>
   <td> selezione delle proprietà cercate (visualizzate come caselle di controllo)</td>
  </tr>
  <tr>
   <td> showGridOnly/sgo<br /> </td>
   <td> Booleano</td>
   <td> se true, mostra solo la griglia e non il pannello di ricerca <br /> </td>
  </tr>
  <tr>
   <td> searchPanelCollapsed/spc</td>
   <td> Booleano</td>
   <td> se true, il pannello di ricerca viene compresso al caricamento</td>
  </tr>
  <tr>
   <td> hideRootPath/hrp</td>
   <td> Booleano</td>
   <td> se true, nasconde il campo percorso radice</td>
  </tr>
  <tr>
   <td> hideQueryParams/hqp</td>
   <td> Booleano</td>
   <td> se true, nasconde il campo query</td>
  </tr>
  <tr>
   <td> hideContentMode / hcm</td>
   <td> Booleano</td>
   <td> se true, nasconde il campo in modalità contenuto</td>
  </tr>
  <tr>
   <td> hideColsSelection/hcs</td>
   <td> Booleano</td>
   <td> se è true, nasconde il campo di selezione delle colonne</td>
  </tr>
  <tr>
   <td> hideExtraCols / hec</td>
   <td> Booleano</td>
   <td> se true, nasconde il campo colonne aggiuntive</td>
  </tr>
  <tr>
   <td> hideSearchButton</td>
   <td> Booleano</td>
   <td> se true, nasconde il pulsante di ricerca</td>
  </tr>
  <tr>
   <td> hideSaveButton/hsavep</td>
   <td> Booleano</td>
   <td> se true, nasconde il pulsante salva</td>
  </tr>
  <tr>
   <td> hideExportButton/hexpb</td>
   <td> Booleano</td>
   <td> se true, nasconde il pulsante esporta</td>
  </tr>
  <tr>
   <td> hideImportButton/hib</td>
   <td> Booleano</td>
   <td> se true, nasconde il pulsante importa</td>
  </tr>
  <tr>
   <td> hideResultNumber/hrn</td>
   <td> Booleano</td>
   <td> se true, nasconde il testo del numero di risultati della ricerca griglia</td>
  </tr>
  <tr>
   <td> hideInsertButton / hinsertb</td>
   <td> Booleano</td>
   <td> se true, nasconde il pulsante inserimento griglia</td>
  </tr>
  <tr>
   <td> hideDeleteButton/hdelb</td>
   <td> Booleano</td>
   <td> se true, nasconde il pulsante elimina griglia</td>
  </tr>
  <tr>
   <td> hidePathCol/hpc</td>
   <td> Booleano</td>
   <td> se true, nasconde la colonna "percorso" della griglia</td>
  </tr>
 </tbody>
</table>

### Sviluppo di un componente basato su Editor in blocco: il componente Elenco prodotti {#developing-a-bulk-editor-based-component-the-product-list-component}

Questa sezione fornisce una panoramica sull’utilizzo dell’Editor collettivo e fornisce una descrizione del componente Geometrixx esistente basato sull’Editor collettivo: il componente Elenco prodotti.

Il componente Elenco prodotti consente agli utenti di visualizzare e modificare una tabella di dati. Ad esempio, puoi utilizzare il componente Elenco prodotti per rappresentare i prodotti in un catalogo. Le informazioni vengono presentate in una tabella standard di HTML e tutte le modifiche vengono eseguite in **Modifica** contenente un widget BulkEditor. Questo Bulk Editor è lo stesso di quello accessibile da /etc/importers/bulkeditor.html o dal menu Strumenti. Il componente Elenco prodotti è stato configurato per funzionalità specifiche e limitate dell’editor in blocco. È possibile configurare ogni parte dell’Editor collettivo (o dei componenti derivati dall’Editor collettivo).

Con l’Editor collettivo, puoi aggiungere, modificare, eliminare, filtrare ed esportare le righe, salvare le modifiche e importare un set di righe. Ogni riga viene memorizzata come nodo sotto l’istanza del componente Elenco prodotti stessa. Ogni cella è una proprietà di ogni nodo. Si tratta di una scelta di progettazione che può essere facilmente modificata. Ad esempio, è possibile memorizzare i nodi altrove nell’archivio. Il ruolo del servlet di query consiste nel restituire l’elenco dei nodi da visualizzare; il percorso di ricerca è definito come istanza dell’elenco di prodotti.

Il codice sorgente del componente Elenco prodotti è disponibile nell’archivio in /apps/geometrixx/components/productlist ed è composto da diverse parti come tutti i componenti di Adobe Experience Manager (AEM):

* Rendering HTML: il rendering viene eseguito in un file JSP (/apps/geometrixx/components/productlist/productlist.jsp). JSP legge i sottonodi del componente Elenco prodotti corrente e li visualizza come riga di una tabella HTML.
* Finestra di dialogo per modifica, in cui puoi definire la configurazione dell’editor di massa. Configura la finestra di dialogo in base alle esigenze del componente: colonne disponibili e possibili azioni eseguite sulla griglia o sulla ricerca. Consulta [Proprietà di configurazione dell’editor in blocco](#bulk-editor-configuration-properties) per informazioni su tutte le proprietà di configurazione.

Ecco una rappresentazione XML dei sottonodi della finestra di dialogo:

```xml
        <editor
            jcr:primaryType="cq:Widget"
            colsSelection="[ProductId,ProductName,Color,CatalogCode,SellingSku]"
            colsValue="[ProductId,ProductName,Color,CatalogCode,SellingSku]"
            contentMode="false"
            exportURL="/etc/importers/bulkeditor/export.tsv"
            extraCols="Selection"
            hideColsSelection="false"
            hideContentMode="true"
            hideDeleteButton="false"
            hideExportButton="false"
            hideExtraCols="true"
            hideImportButton="false"
            hideInsertButton="false"
            hideMoveButtons="false"
            hidePathCol="true"
            hideRootPath="true"
            hideSaveButton="false"
            hideSearchButton="false"
            importURL="/etc/importers/bulkeditor/import"
            initialSearch="true"
            insertedResourceType="geometrixx/components/productlist/sku"
            queryParams=""
            queryURL="/etc/importers/bulkeditor/query.json"
            saveURL="/etc/importers/bulkeditor/save"
            xtype="bulkeditor">
            <saveButton
                jcr:primaryType="nt:unstructured"
                text="Save modifications"/>
            <searchButton
                jcr:primaryType="nt:unstructured"
                text="Apply filter"/>
            <queryParamsInput
                jcr:primaryType="nt:unstructured"
                fieldDescription="Enter here your filters"
                fieldLabel="Filters"/>
            <searchPanel
                jcr:primaryType="nt:unstructured"
                height="200">
                <defaults
                    jcr:primaryType="nt:unstructured"
                    labelWidth="150"/>
            </searchPanel>
            <grid
                jcr:primaryType="nt:unstructured"
                height="275"/>
            <store jcr:primaryType="nt:unstructured">
                <sortInfo
                    jcr:primaryType="nt:unstructured"
                    direction="ASC"
                    field="CatalogCode"/>
            </store>
            <colModel
                jcr:primaryType="nt:unstructured"
                width="150"/>
            <colsMetadata jcr:primaryType="nt:unstructured">
                <Selection
                    jcr:primaryType="nt:unstructured"
                    checkbox="true"
                    forcedPosition="0"
                    headerText=""/>
                <ProductId
                    jcr:primaryType="nt:unstructured"
                    cellCls="productlist-cell-productid"
                    headerText="Product Id"/>
                <ProductName
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #FFCC99;"
                    headerText="Product Name"/>
                <CatalogCode
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #EDEDED;"
                    headerText="Catalog Code"/>
                <Color jcr:primaryType="nt:unstructured">
                    <editor
                        jcr:primaryType="nt:unstructured"
                        store="[Blue,Red,Yellow]"
                        triggerAction="all"
                        typeAhead="true"
                        xtype="combo"/>
                </Color>
                <SellingSku
                    jcr:primaryType="nt:unstructured"
                    headerText="Sku Id"/>
            </colsMetadata>
        </editor>
```

### Proprietà di configurazione dell’editor in blocco {#bulk-editor-configuration-properties}

È possibile configurare ogni parte dell’editor di massa. Nella tabella seguente sono elencate tutte le proprietà di configurazione per l&#39;editor in blocco.

<table>
 <tbody>
  <tr>
   <td>Nome proprietà</td>
   <td>Definizione</td>
  </tr>
  <tr>
   <td>rootPath</td>
   <td>Percorso directory principale ricerca</td>
  </tr>
  <tr>
   <td>queryParams</td>
   <td>Query di ricerca</td>
  </tr>
  <tr>
   <td>contentMode</td>
   <td>True per attivare la modalità contenuto: le proprietà vengono lette nel nodo jcr:content e non nel nodo dei risultati di ricerca</td>
  </tr>
  <tr>
   <td>colsValue</td>
   <td>Proprietà cercate (valori selezionati da colonneCaselle di controllo visualizzate in Selection)</td>
  </tr>
  <tr>
   <td>extraCols</td>
   <td>Proprietà ricercate aggiuntive (visualizzate in un campo di testo separato da virgole)</td>
  </tr>
  <tr>
   <td>initialSearch</td>
   <td>True per eseguire una query al caricamento della pagina</td>
  </tr>
  <tr>
   <td>colsSelection</td>
   <td>Selezione delle proprietà cercate (visualizzate come caselle di controllo)</td>
  </tr>
  <tr>
   <td>showGridOnly</td>
   <td>True per visualizzare solo la griglia e non il pannello di ricerca (non dimenticare di impostare initialSearch su true)</td>
  </tr>
  <tr>
   <td>searchPanelCollapsed</td>
   <td>True per comprimere il pannello di ricerca per impostazione predefinita</td>
  </tr>
  <tr>
   <td>hideRootPath</td>
   <td>Nascondi campo percorso directory principale</td>
  </tr>
  <tr>
   <td>hideQueryParams</td>
   <td>Nascondi campo query</td>
  </tr>
  <tr>
   <td>hideContentMode</td>
   <td>Nascondi campo modalità contenuto</td>
  </tr>
  <tr>
   <td>hideColsSelection</td>
   <td>Nascondi campo di selezione colonne</td>
  </tr>
  <tr>
   <td>hideExtraCols</td>
   <td>Nascondi campo dei punti aggiuntivi</td>
  </tr>
  <tr>
   <td>hideSearchButton</td>
   <td>Nascondi pulsante di ricerca</td>
  </tr>
  <tr>
   <td>hideSaveButton</td>
   <td>Nascondi pulsante di salvataggio</td>
  </tr>
  <tr>
   <td>hideExportButton</td>
   <td>Nascondi pulsante di esportazione</td>
  </tr>
  <tr>
   <td>hideImportButton</td>
   <td>Nascondi pulsante di importazione</td>
  </tr>
  <tr>
   <td>hideResultNumber</td>
   <td>Nascondi testo numero risultati ricerca griglia</td>
  </tr>
  <tr>
   <td>hideInsertButton</td>
   <td>Nascondi pulsante inserimento griglia</td>
  </tr>
  <tr>
   <td>hideDeleteButton</td>
   <td>Nascondi pulsante di eliminazione griglia</td>
  </tr>
  <tr>
   <td>hidePathCol</td>
   <td>Nascondi colonna "percorso" griglia</td>
  </tr>
  <tr>
   <td>queryURL</td>
   <td>Percorso del servlet di query</td>
  </tr>
  <tr>
   <td>exportURL</td>
   <td>Percorso per esportare il servlet</td>
  </tr>
  <tr>
   <td>importURL</td>
   <td>Percorso del servlet di importazione</td>
  </tr>
  <tr>
   <td>insertResourceType</td>
   <td>Tipo di risorsa aggiunto al nodo quando viene inserita una riga</td>
  </tr>
  <tr>
   <td>saveButton</td>
   <td>Configurazione widget pulsante Salva</td>
  </tr>
  <tr>
   <td>searchButton</td>
   <td>Configurazione widget pulsante di ricerca</td>
  </tr>
  <tr>
   <td>exportButton</td>
   <td>Configurazione widget pulsante Esporta</td>
  </tr>
  <tr>
   <td>importButton</td>
   <td>Configurazione widget pulsante Importa</td>
  </tr>
  <tr>
   <td>searchPanel</td>
   <td>Configurazione widget pannello di ricerca</td>
  </tr>
  <tr>
   <td>griglia</td>
   <td>Configurazione widget griglia</td>
  </tr>
  <tr>
   <td>archiviare</td>
   <td>Configurazione archivio</td>
  </tr>
  <tr>
   <td>colModel</td>
   <td>Configurazione modello colonna griglia</td>
  </tr>
  <tr>
   <td>rootPathInput</td>
   <td>configurazione widget rootPath</td>
  </tr>
  <tr>
   <td>queryParamsInput</td>
   <td>configurazione widget queryParams</td>
  </tr>
  <tr>
   <td>contentModeInput</td>
   <td>configurazione widget contentMode</td>
  </tr>
  <tr>
   <td>colsSelectionInput</td>
   <td>config widget colsSelection</td>
  </tr>
  <tr>
   <td>extraColsInput</td>
   <td>configurazione widget extraCols</td>
  </tr>
  <tr>
   <td>colsMetadata</td>
   <td>Configurazione metadati colonna. Le possibili proprietà sono (applicate a tutte le celle della colonna): <br />
    <ul>
     <li>cellStyle: stile html </li>
     <li>cellCls: classe css </li>
     <li>readOnly: true per non essere in grado di modificare il valore </li>
     <li>casella di controllo: true per definire tutte le celle della colonna come caselle di controllo (valori true/false) </li>
     <li>forcedPosition: valore intero per specificare la posizione della colonna nella griglia (tra 0-numero di colonne-1)<p><br /> </p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Configurazione metadati colonne {#columns-metadata-configuration}

Puoi configurare per ciascuna colonna:

* proprietà di visualizzazione: stile html, classe CSS e sola lettura

* una casella di controllo
* una posizione forzata

Colonne CSS e di sola lettura

L’editor collettivo dispone di tre configurazioni di colonna:

* Cell CSS class name (cellCls): nome di classe CSS aggiunto a ogni cella della colonna configurata.
* Stile cella (cellStyle): stile HTML aggiunto a ogni cella della colonna configurata.
* Sola lettura (sola lettura): la sola lettura è impostata per ogni cella della colonna configurata.

La configurazione deve essere definita come la seguente:

```
"colsMetadata": {
"Column name": {
     "cellStyle": "html style",
     "cellCls": "CSS class",
     "readOnly": true/false
}
}
```

Il seguente esempio si trova nel componente productlist (/apps/geometrixx/components/productlist/dialog/items/editor/colsMetadata):

```xml
            <colsMetadata jcr:primaryType="nt:unstructured">
                <Selection
                    jcr:primaryType="nt:unstructured"
                    checkbox="true"
                    forcedPosition="0"
                    headerText=""/>
                <ProductId
                    jcr:primaryType="nt:unstructured"
                    cellCls="productlist-cell-productid"
                    headerText="Product Id"/>
                <ProductName
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #FFCC99;"
                    headerText="Product Name"/>
                <CatalogCode
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #EDEDED;"
                    headerText="Catalog Code"/>
                <Color jcr:primaryType="nt:unstructured">
                    <editor
                        jcr:primaryType="nt:unstructured"
                        store="[Blue,Red,Yellow]"
                        triggerAction="all"
                        typeAhead="true"
                        xtype="combo"/>
                </Color>
                <SellingSku
                    jcr:primaryType="nt:unstructured"
                    headerText="Sku Id"/>
            </colsMetadata>
```

**Casella di controllo**

Se la proprietà di configurazione della casella di controllo è impostata su true, tutte le celle della colonna vengono visualizzate come caselle di controllo. Una casella selezionata invia **true** al server Salva servlet, **false** altrimenti. Nel menu dell’intestazione puoi anche **seleziona tutto** o **seleziona nessuno**. Queste opzioni sono attivate se l&#39;intestazione selezionata è l&#39;intestazione di una colonna di una casella di controllo.

Nell&#39;esempio precedente, la colonna di selezione contiene solo caselle di controllo come checkbox=&quot;true&quot;.

**Posizione forzata**

I metadati di posizione forzati forcedPosition consentono di specificare la posizione della colonna all&#39;interno della griglia: 0 è la prima posizione e &lt;number of=&quot;&quot; columns=&quot;&quot;>-1 è l&#39;ultima posizione. Qualsiasi altro valore viene ignorato.

Nell&#39;esempio precedente, la colonna di selezione è la prima colonna denominata forcedPosition=&quot;0&quot;.

### Query Servlet {#query-servlet}

Per impostazione predefinita, il servlet Query si trova in `/libs/wcm/core/components/bulkeditor/json.java`. Puoi configurare un altro percorso per recuperare i dati.

Il servlet Query funziona come segue: riceve una query GQL e le colonne da restituire, calcola i risultati e li invia nuovamente all’editor bulk come flusso JSON.

Nel caso del componente Elenco prodotti, i due parametri inviati al servlet Query sono i seguenti:

* query: &quot;path:/content/geometrixx/en/customers/jcr:content/par/productlist Cube&quot;
* colonne: &quot;Selection,ProductId,ProductName,Color,CatalogCode,SellingSku&quot;

Il flusso JSON viene restituito come segue:

```
{
  "hits": [{
      "jcr:path": "/content/geometrixx/en/products/jcr:content/par/productlist/1258674828905",
      "ProductId": "21",
      "ProductName": "Cube",
      "Color": "Blue",
      "CatalogCode": "43244",
      "SellingSku": "32131"
    }
  ],
  "results": 1
}
```

Ogni hit corrisponde a un nodo e alle relative proprietà e viene visualizzato come riga nella griglia.

Puoi estendere il servlet Query per restituire un modello di ereditarietà complesso o restituire nodi memorizzati in una posizione logica specifica. Il servlet Query può essere utilizzato per eseguire qualsiasi tipo di calcolo complesso. La griglia può quindi visualizzare righe che sono un aggregato di diversi nodi nell’archivio. In tal caso, la modifica e il salvataggio di queste righe devono essere gestiti dal servlet di salvataggio.

### Salva servlet {#save-servlet}

Nella configurazione predefinita dell’Editor collettivo ogni riga è un nodo e il percorso di questo nodo viene memorizzato nel record di riga. L’Editor collettivo mantiene il collegamento tra la riga e il nodo attraverso il percorso jcr. Quando un utente modifica la griglia, viene creato un elenco di tutte le modifiche. Quando un utente fa clic su **Salva**, a ogni percorso viene inviata una query POST con i valori delle proprietà aggiornati. Questa è la base del concetto Sling e funziona bene se ogni cella è una proprietà del nodo. Tuttavia, se il servlet Query viene implementato per eseguire il calcolo dell’ereditarietà, questo modello non può funzionare in quanto una proprietà restituita dal servlet Query può essere ereditata da un altro nodo.

Il concetto del servlet di salvataggio è che le modifiche non vengono inviate direttamente a ciascun nodo, ma a un servlet che esegue il processo di salvataggio. Questo consente a questo servlet di analizzare le modifiche e salvare le proprietà sul nodo giusto.

Ogni proprietà aggiornata viene inviata al servlet nel seguente formato:

* Nome parametro: &lt;jcr path=&quot;&quot;>/&lt;property name=&quot;&quot;>

  Esempio: /content/geometrixx/en/products/jcr:content/par/productlist/1258674859000/SellingSku

* Valore: &lt;value>

  Esempio: 12123

Il servlet deve sapere dove è memorizzata la proprietà catalogCode.

Un’implementazione predefinita del servlet Save è disponibile all’indirizzo /libs/wcm/bulkeditor/save/POST.jsp e viene utilizzata nel componente Elenco prodotti. Prende tutti i parametri dalla richiesta (con un &lt;jcr path=&quot;&quot;>/&lt;property name=&quot;&quot;> e scrive le proprietà sui nodi utilizzando l’API JCR. Crea anche un nodo se non esiste (righe inserite nella griglia).

Non utilizzare il codice predefinito così com&#39;è perché reimplementa ciò che il server fa in modo nativo (un POST su &lt;jcr path=&quot;&quot;>/&lt;property name=&quot;&quot;>) ed è quindi solo un buon punto di partenza per la creazione di un servlet Save in grado di gestire un modello di ereditarietà delle proprietà.
