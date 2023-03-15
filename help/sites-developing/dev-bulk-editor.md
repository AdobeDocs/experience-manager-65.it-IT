---
title: Sviluppo dell’editor in blocco
seo-title: Developing the Bulk Editor
description: L’assegnazione tag consente di classificare e organizzare i contenuti
seo-description: Tagging allows content to be categorized and organized
uuid: 3cd04c52-5bdb-47f6-9fa3-d7a4937e8e20
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e9a1ff95-e88e-41f0-9731-9a59159b4653
exl-id: 8753aaab-959f-459b-bdb6-057cbe05d480
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1837'
ht-degree: 2%

---

# Sviluppo dell’editor in blocco{#developing-the-bulk-editor}

Questa sezione descrive come sviluppare lo strumento Modifiche in serie e come estendere il componente Elenco prodotti, basato sull&#39;editor in serie.

## Parametri query dell’editor bulk {#bulk-editor-query-parameters}

Quando lavori con l’editor in blocco, puoi aggiungere all’URL diversi parametri di query per chiamare l’editor in blocco con una configurazione specifica. Se desideri che l’editor in blocco sia sempre utilizzato con una determinata configurazione, ad esempio, come nel componente Elenco prodotti, devi modificare bulkeditor.jsp (che si trova in /libs/wcm/core/components/bulkeditor) o creare un componente con la configurazione specifica. Le modifiche apportate utilizzando i parametri di query non sono permanenti.

Ad esempio, se immetti quanto segue nell’URL del browser:

`https://<servername><port_number>/etc/importers/bulkeditor.html?rootPath=/content/geometrixx/en&queryParams=geometrixx&initialSearch=true&hrp=true`

l&#39;editor in serie viene visualizzato senza **Percorso radice** come hrp=true nasconde il campo. Con il parametro hrp=false, viene visualizzato il campo (il valore predefinito).

Di seguito è riportato un elenco dei parametri di query dell’editor in blocco:

>[!NOTE]
>
>Ogni parametro può avere un nome lungo e breve. Ad esempio, il nome lungo del percorso principale di ricerca è `rootPath`, quello breve è `rp`. Se il nome lungo non è definito, quello breve viene letto dalla richiesta.

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
   <td> rootPath / rp<br /> </td>
   <td> Stringa </td>
   <td> percorso principale di ricerca</td>
  </tr>
  <tr>
   <td> queryParams / qp<br /> </td>
   <td> Stringa</td>
   <td> query di ricerca</td>
  </tr>
  <tr>
   <td> contentMode / cm<br /> </td>
   <td> Booleano</td>
   <td> se true, la modalità contenuto è abilitata<br /> </td>
  </tr>
  <tr>
   <td> colsValue / cv<br /> </td>
   <td> Stringa[]</td>
   <td> proprietà di ricerca (valori selezionati da colsSelection visualizzati come caselle di controllo)</td>
  </tr>
  <tr>
   <td> extraCols / ec<br /> </td>
   <td> Stringa[]</td>
   <td> ulteriori proprietà di ricerca (visualizzate in un campo di testo separato da virgole)</td>
  </tr>
  <tr>
   <td> initialSearch / is<br /> </td>
   <td> Booleano</td>
   <td> se true, la query viene eseguita al caricamento della pagina<br /> </td>
  </tr>
  <tr>
   <td> colsSelection / cs<br /> </td>
   <td> Stringa[]</td>
   <td> selezione delle proprietà cercate (visualizzate come caselle di controllo)</td>
  </tr>
  <tr>
   <td> showGridOnly / sgo<br /> </td>
   <td> Booleano</td>
   <td> se true, mostra solo la griglia e non il pannello di ricerca <br /> </td>
  </tr>
  <tr>
   <td> searchPanelCollapsed / spc</td>
   <td> Booleano</td>
   <td> se true, il pannello di ricerca viene compresso al caricamento</td>
  </tr>
  <tr>
   <td> hideRootPath / hrp</td>
   <td> Booleano</td>
   <td> quando true, nasconde il campo del percorso principale</td>
  </tr>
  <tr>
   <td> hideQueryParams / hqp</td>
   <td> Booleano</td>
   <td> quando true, nasconde il campo query</td>
  </tr>
  <tr>
   <td> hideContentMode / hcm</td>
   <td> Booleano</td>
   <td> quando è true, nasconde il campo modalità contenuto</td>
  </tr>
  <tr>
   <td> hideColsSelection / hcs</td>
   <td> Booleano</td>
   <td> quando è true, nasconde il campo di selezione delle colonne</td>
  </tr>
  <tr>
   <td> hideExtraCols / hec</td>
   <td> Booleano</td>
   <td> quando è true, nasconde il campo colonne extra</td>
  </tr>
  <tr>
   <td> hideSearchButton</td>
   <td> Booleano</td>
   <td> se true, nasconde il pulsante di ricerca</td>
  </tr>
  <tr>
   <td> hideSaveButton / hsavep</td>
   <td> Booleano</td>
   <td> se true, nasconde il pulsante salva</td>
  </tr>
  <tr>
   <td> hideExportButton / hexpb</td>
   <td> Booleano</td>
   <td> quando è true, nasconde il pulsante di esportazione</td>
  </tr>
  <tr>
   <td> hideImportButton / hib</td>
   <td> Booleano</td>
   <td> se true, nasconde il pulsante di importazione</td>
  </tr>
  <tr>
   <td> hideResultNumber / hrn</td>
   <td> Booleano</td>
   <td> se true, nasconde il testo del numero del risultato della ricerca griglia</td>
  </tr>
  <tr>
   <td> hideInsertButton / hinsertb</td>
   <td> Booleano</td>
   <td> se true, nasconde il pulsante di inserimento griglia</td>
  </tr>
  <tr>
   <td> hideDeleteButton / hdelb</td>
   <td> Booleano</td>
   <td> se true, nasconde il pulsante di eliminazione griglia</td>
  </tr>
  <tr>
   <td> hidePathCol / hpc</td>
   <td> Booleano</td>
   <td> quando è true, nasconde la colonna "path" della griglia</td>
  </tr>
 </tbody>
</table>

### Sviluppo di un componente basato su Modifiche in serie: il componente Elenco prodotti {#developing-a-bulk-editor-based-component-the-product-list-component}

Questa sezione fornisce una panoramica sull’utilizzo dell’editor in blocco e fornisce una descrizione del componente di Geometrixx esistente in base all’editor in serie: il componente Elenco prodotti .

Il componente Elenco prodotti consente agli utenti di visualizzare e modificare una tabella di dati. Ad esempio, puoi utilizzare il componente Elenco prodotti per rappresentare i prodotti in un catalogo. Le informazioni vengono presentate in una tabella HTML standard ed eventuali modifiche vengono eseguite nel **Modifica** che contiene un widget BulkEditor. (Questo Modifiche collettive è esattamente lo stesso di quello accessibile da /etc/importers/bulkeditor.html o dal menu Strumenti). Il componente Elenco prodotti è stato configurato per funzionalità specifiche e limitate dell’editor in blocco. È possibile configurare ogni parte dell’editor di massa (o dei componenti derivati dall’editor di massa).

Con l’editor di massa puoi aggiungere, modificare, eliminare, filtrare ed esportare le righe, salvare le modifiche e importare un set di righe. Ogni riga viene memorizzata come nodo nell’istanza del componente Elenco prodotti stessa. Ogni cella è una proprietà di ogni nodo. Si tratta di una scelta progettuale che può essere facilmente modificata, ad esempio, è possibile memorizzare nodi in un altro punto dell&#39;archivio. Il ruolo del servlet di query consiste nel restituire l’elenco dei nodi da visualizzare; il percorso di ricerca è definito come un’istanza dell’elenco dei prodotti.

Il codice sorgente del componente Elenco prodotti è disponibile nell’archivio in /apps/geometrixx/components/productlist ed è composto da diverse parti come tutti i componenti AEM:

* Rendering di HTML: il rendering viene eseguito in un file JSP (/apps/geometrixx/components/productlist/productlist.jsp). Il JSP legge i sottonodi del componente Elenco prodotti corrente e li visualizza come riga di una tabella HTML.
* Finestra di dialogo Modifica, in cui è possibile definire la configurazione dell’editor bulk. Configura la finestra di dialogo in base alle esigenze del componente: colonne disponibili e possibili azioni eseguite sulla griglia o sulla ricerca. Vedi [proprietà di configurazione dell’editor in serie](#bulk-editor-configuration-properties) per informazioni su tutte le proprietà di configurazione.

Ecco una rappresentazione XML dei sotto-nodi della finestra di dialogo:

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

È possibile configurare ogni parte dell’editor in blocco. Nella tabella seguente sono elencate tutte le proprietà di configurazione per l’editor in blocco.

<table>
 <tbody>
  <tr>
   <td>Nome proprietà</td>
   <td>Definizione</td>
  </tr>
  <tr>
   <td>rootPath</td>
   <td>Percorso radice di ricerca</td>
  </tr>
  <tr>
   <td>queryParams</td>
   <td>Query di ricerca</td>
  </tr>
  <tr>
   <td>contentMode</td>
   <td>True per abilitare la modalità contenuto: le proprietà vengono lette sul nodo jcr:content e non sul nodo dei risultati di ricerca</td>
  </tr>
  <tr>
   <td>colsValue</td>
   <td>Proprietà cercate (valori selezionati da colsSelection visualizzati come caselle di controllo)</td>
  </tr>
  <tr>
   <td>extraCols</td>
   <td>Proprietà di ricerca extra (visualizzate in un campo di testo separato da virgole)</td>
  </tr>
  <tr>
   <td>initialSearch</td>
   <td>True per eseguire la query al caricamento della pagina</td>
  </tr>
  <tr>
   <td>colsSelection</td>
   <td>Selezione di proprietà cercate (visualizzate come caselle di controllo)</td>
  </tr>
  <tr>
   <td>showGridOnly</td>
   <td>True per mostrare solo la griglia e non il pannello di ricerca (non dimenticare di impostare initialSearch su true)</td>
  </tr>
  <tr>
   <td>searchPanelCollapsed</td>
   <td>True per comprimere il pannello di ricerca per impostazione predefinita</td>
  </tr>
  <tr>
   <td>hideRootPath</td>
   <td>Nascondi campo percorso principale</td>
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
   <td>Nascondi campo selezione colori</td>
  </tr>
  <tr>
   <td>hideExtraCols</td>
   <td>Nascondi campo punti extra</td>
  </tr>
  <tr>
   <td>hideSearchButton</td>
   <td>Pulsante Nascondi ricerca</td>
  </tr>
  <tr>
   <td>hideSaveButton</td>
   <td>Pulsante Nascondi salvataggio</td>
  </tr>
  <tr>
   <td>hideExportButton</td>
   <td>Pulsante Nascondi esportazione</td>
  </tr>
  <tr>
   <td>hideImportButton</td>
   <td>Pulsante Nascondi importazione</td>
  </tr>
  <tr>
   <td>hideResultNumber</td>
   <td>Nascondi testo del numero del risultato della ricerca griglia</td>
  </tr>
  <tr>
   <td>hideInsertButton</td>
   <td>Pulsante Nascondi inserimento griglia</td>
  </tr>
  <tr>
   <td>hideDeleteButton</td>
   <td>Pulsante Nascondi eliminazione griglia</td>
  </tr>
  <tr>
   <td>hidePathCol</td>
   <td>Nascondi la colonna "percorso" della griglia</td>
  </tr>
  <tr>
   <td>queryURL</td>
   <td>Percorso del servlet di query</td>
  </tr>
  <tr>
   <td>exportURL</td>
   <td>Percorso del servlet di esportazione</td>
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
   <td>Configurazione widget pulsante di esportazione</td>
  </tr>
  <tr>
   <td>importButton</td>
   <td>Configurazione widget pulsante di importazione</td>
  </tr>
  <tr>
   <td>searchPanel</td>
   <td>Configurazione widget del pannello di ricerca</td>
  </tr>
  <tr>
   <td>griglia</td>
   <td>Configurazione widget griglia</td>
  </tr>
  <tr>
   <td>archiviare</td>
   <td>Configurazione store</td>
  </tr>
  <tr>
   <td>colModel</td>
   <td>Configurazione del modello a colonne griglia</td>
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
   <td>configurazione widget colsSelection</td>
  </tr>
  <tr>
   <td>extraColsInput</td>
   <td>configurazione widget extraCols</td>
  </tr>
  <tr>
   <td>colsMetadata</td>
   <td>Configurazione dei metadati della colonna. Le proprietà possibili sono (applicate a tutte le celle della colonna): <br />
    <ul>
     <li>cellStyle: stile html </li>
     <li>cellCls: classe css </li>
     <li>readOnly: true per non essere in grado di modificare il valore </li>
     <li>casella di controllo: true per definire tutte le celle della colonna come caselle di controllo (valori true/false) </li>
     <li>forcePosition: valore intero per specificare dove posizionare la colonna nella griglia (tra 0 e numero di colonne-1)<p><br /> </p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Configurazione metadati colonne {#columns-metadata-configuration}

Puoi configurare per ogni colonna:

* proprietà di visualizzazione: stile html, classe CSS e sola lettura

* una casella di controllo
* posizione forzata

Colonne CSS e di sola lettura

L’editor in serie dispone di tre configurazioni di colonna:

* Nome classe CSS cella (cellCls): un nome di classe CSS aggiunto a ciascuna cella della colonna configurata.
* Stile cella (cellStyle): uno stile HTML aggiunto a ciascuna cella della colonna configurata.
* Sola lettura (sola lettura): per ogni cella della colonna configurata viene impostata la sola lettura.

La configurazione deve essere definita come segue:

```
"colsMetadata": {
"Column name": {
     "cellStyle": "html style",
     "cellCls": "CSS class",
     "readOnly": true/false
}
}
```

L’esempio seguente è disponibile nel componente elenco prodotti (/apps/geometrixx/components/productlist/dialog/items/editor/colsMetadata):

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

**Casella di selezione**

Se la proprietà di configurazione della casella di controllo è impostata su true, tutte le celle della colonna vengono sottoposte a rendering come caselle di controllo. Una casella di controllo invia **true** al servlet di salvataggio del server, **false** altrimenti. Nel menu dell’intestazione è inoltre possibile **seleziona tutto** o **seleziona nessuno**. Queste opzioni sono abilitate se l’intestazione selezionata è l’intestazione di una colonna di controllo.

Nell’esempio precedente la colonna di selezione contiene solo le caselle di controllo come check=&quot;true&quot;.

**Posizione forzata**

I metadati di posizione forzata, l&#39;opzione di posizione forzata ForzaPosition consente di specificare la posizione della colonna all&#39;interno della griglia: 0 è il primo posto e &lt;number of=&quot;&quot; columns=&quot;&quot;>-1 è l&#39;ultima posizione. Qualsiasi altro valore viene ignorato.

Nell&#39;esempio precedente la colonna di selezione è la prima colonna come forzatoPosition=&quot;0&quot;.

### Servlet query {#query-servlet}

Per impostazione predefinita, il servlet Query si trova in `/libs/wcm/core/components/bulkeditor/json.java`. Puoi configurare un altro percorso per recuperare i dati.

Il servlet Query funziona come segue: riceve una query GQL e le colonne da restituire, calcola i risultati e invia di nuovo i risultati all’editor in blocco come flusso JSON.

Nel caso del componente Elenco prodotti , i due parametri inviati al servlet Query sono i seguenti:

* query: &quot;path:/content/geometrixx/en/Customers/jcr:content/par/productlist Cube&quot;
* punti: &quot;Selection,ProductId,ProductName,Color,CatalogCode,SellingSku&quot;

e il flusso JSON restituito è il seguente:

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

Ogni hit corrisponde a un nodo e alle sue proprietà e viene visualizzato come una riga nella griglia.

È possibile estendere il servlet Query per restituire un modello di ereditarietà complesso o i nodi di ritorno memorizzati in una posizione logica specifica. Il servlet Query può essere utilizzato per eseguire qualsiasi tipo di calcolo complesso. La griglia può quindi visualizzare le righe che sono un aggregato di più nodi nel repository. La modifica e il salvataggio di queste righe devono in tal caso essere gestiti dal servlet Save.

### Salva servlet {#save-servlet}

Nella configurazione predefinita dell&#39;editor in serie ogni riga è un nodo e il percorso di questo nodo è memorizzato nel record di riga. L&#39;editor in blocco mantiene il collegamento tra la riga e il nodo attraverso il percorso jcr. Quando un utente modifica la griglia, viene generato un elenco di tutte le modifiche. Quando un utente fa clic su **Salva**, viene inviata una query POST a ogni percorso con i valori delle proprietà aggiornati. Questa è la base del concetto Sling e funziona bene se ogni cella è una proprietà del nodo. Tuttavia, se il servlet Query è implementato per eseguire il calcolo dell’ereditarietà, questo modello non può funzionare come proprietà restituita dal servlet Query può essere ereditato da un altro nodo.

Il concetto di servlet Save è che le modifiche non vengono pubblicate direttamente su ciascun nodo ma vengono pubblicate su un servlet che esegue il processo di salvataggio. Questo dà a questo servlet la possibilità di analizzare le modifiche e salvare le proprietà sul nodo destro.

Ogni proprietà aggiornata viene inviata al servlet nel seguente formato:

* Nome parametro: &lt;jcr path=&quot;&quot;>/&lt;property name=&quot;&quot;>

   Esempio: /content/geometrixx/en/products/jcr:content/par/productlist/1258674859000/SellingSku

* Valore: &lt;value>

   Esempio: 12123

Il servlet deve sapere dove è memorizzata la proprietà catalogCode.

Un’implementazione predefinita del servlet Save è disponibile all’indirizzo /libs/wcm/bulkeditor/save/POST.jsp e viene utilizzata nel componente Elenco prodotti . Prende tutti i parametri dalla richiesta (con un &lt;jcr path=&quot;&quot;>/&lt;property name=&quot;&quot;> format) e scrive le proprietà sui nodi utilizzando l&#39;API JCR. Crea anche un nodo se non esistono (righe inserite nella griglia).

Il codice predefinito non deve essere utilizzato così com&#39;è in quanto reimplementa ciò che il server fa in modo nativo (un POST su &lt;jcr path=&quot;&quot;>/&lt;property name=&quot;&quot;>) ed è quindi solo un buon punto di partenza per la creazione di un servlet Save che gestirà un modello di ereditarietà di proprietà.
