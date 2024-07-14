---
title: Precompilazione di Forms con layout fluibili
description: Precompila i moduli con layout fluibile per visualizzare i dati agli utenti all’interno di un modulo renderizzato utilizzando l’API Java e l’API del servizio Web.
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: ff087084-fb1c-43a4-ae54-cc77eb862493
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '3478'
ht-degree: 0%

---

# Precompilazione di Forms con layout fluibili {#prepopulating-forms-with-flowable-layouts1}

## Precompilazione di Forms con layout fluibili {#prepopulating-forms-with-flowable-layouts2}

La precompilazione dei moduli consente di visualizzare i dati agli utenti all’interno di un modulo di cui è stato eseguito il rendering. Ad esempio, supponiamo che un utente acceda a un sito web con un nome utente e una password. Se l&#39;autenticazione ha esito positivo, l&#39;applicazione client esegue una query su un database per ottenere informazioni sull&#39;utente. I dati vengono uniti nel modulo, quindi il modulo viene sottoposto a rendering per l’utente. L’utente può quindi visualizzare dati personalizzati all’interno del modulo.

La precompilazione di un modulo presenta i seguenti vantaggi:

* Consente all&#39;utente di visualizzare dati personalizzati in un modulo.
* Riduce la quantità di digitazioni che l’utente compila per compilare un modulo.
* Garantisce l’integrità dei dati controllando dove vengono inseriti i dati.

Un modulo può essere precompilato dalle due origini dati XML seguenti:

* Un’origine dati XDP, XML conforme alla sintassi XFA (o dati XFDF per precompilare un modulo creato utilizzando Acrobat).
* Origine dati XML arbitraria contenente coppie nome/valore corrispondenti ai nomi dei campi del modulo. Gli esempi in questa sezione utilizzano un&#39;origine dati XML arbitraria.

È necessario che esista un elemento XML per ogni campo modulo che si desidera precompilare. Il nome dell&#39;elemento XML deve corrispondere al nome del campo. Un elemento XML viene ignorato se non corrisponde a un campo modulo o se il nome dell&#39;elemento XML non corrisponde al nome del campo. Non è necessario che corrispondano all&#39;ordine di visualizzazione degli elementi XML, purché siano specificati tutti gli elementi XML.

Quando si precompila un modulo che contiene già dati, è necessario specificare i dati già visualizzati nell&#39;origine dati XML. Si supponga che un modulo contenente 10 campi contenga dati in quattro campi. Quindi, si supponga di voler precompilare i sei campi rimanenti. In questa situazione è necessario specificare 10 elementi XML nell&#39;origine dati XML utilizzata per precompilare il modulo. Se specifichi solo sei elementi, i quattro campi originali sono vuoti.

Ad esempio, puoi precompilare un modulo come il modulo di conferma di esempio. (Vedi &quot;Modulo di conferma&quot; in [Rendering dei PDF forms interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md).)

Per precompilare il modulo di conferma di esempio, è necessario creare un&#39;origine dati XML contenente tre elementi XML corrispondenti ai tre campi del modulo. Questo modulo contiene i tre campi seguenti: `FirstName`, `LastName` e `Amount`. Il primo passaggio consiste nel creare un&#39;origine dati XML contenente elementi XML corrispondenti ai campi della struttura del modulo. Il passaggio successivo consiste nell&#39;assegnare valori di dati agli elementi XML, come illustrato nel codice XML riportato di seguito.

```xml
     <Untitled>
         <FirstName>Jerry</FirstName>
         <LastName>Johnson</LastName>
         <Amount>250000</Amount>
     </Untitled>
```

Dopo aver precompilato il modulo di conferma con questa origine dati XML e aver eseguito il rendering del modulo, vengono visualizzati i valori dei dati assegnati agli elementi XML, come illustrato nel diagramma seguente.

![pf_pf_confirmxml3](assets/pf_pf_confirmxml3.png)

### Precompilazione dei moduli con layout scorrevoli {#prepopulating_forms_with_flowable_layouts-1}

I Forms con layout scorrevoli sono utili per mostrare agli utenti una quantità indeterminata di dati. Poiché il layout del modulo viene regolato automaticamente in base alla quantità di dati uniti, non è necessario predeterminare un layout fisso o un numero di pagine per il modulo, come invece è necessario fare con un modulo con un layout fisso.

Un modulo viene generalmente compilato con i dati ottenuti durante la fase di esecuzione. È quindi possibile precompilare un modulo creando un&#39;origine dati XML in memoria e inserendo i dati direttamente nell&#39;origine dati XML in memoria.

Considera un’applicazione basata su web, ad esempio un negozio online. Al termine dell&#39;acquisto, tutti gli articoli acquistati vengono inseriti in un&#39;origine dati XML in memoria utilizzata per precompilare un modulo. Il diagramma seguente illustra questo processo, illustrato nella tabella che segue il diagramma.

![pf_pf_finsrv_webapp_v1](assets/pf_pf_finsrv_webapp_v1.png)

Nella tabella seguente vengono descritti i passaggi del diagramma.

<table>
 <thead>
  <tr>
   <th><p>Passaggio</p></th>
   <th><p>Descrizione</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>Un utente acquista articoli da un negozio online basato su Web. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Al termine dell'acquisto degli elementi e dopo aver fatto clic sul pulsante Invia, viene creata un'origine dati XML in memoria. Gli articoli acquistati e le informazioni utente vengono inseriti nell'origine dati XML in memoria. </p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>L'origine dati XML viene utilizzata per precompilare un modulo dell'ordine di acquisto (un esempio di questo modulo è riportato in questa tabella). </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Il modulo dell’ordine di acquisto viene inviato al browser web client. </p></td>
  </tr>
 </tbody>
</table>

Nel diagramma seguente viene illustrato un esempio di modulo ordine fornitore. Le informazioni contenute nella tabella possono essere modificate in base al numero di record nei dati XML.

![pf_pf_poform](assets/pf_pf_poform.png)

>[!NOTE]
>
>È possibile precompilare un modulo con dati provenienti da altre origini, ad esempio un database aziendale o applicazioni esterne.

### Considerazioni sulla progettazione dei moduli {#form-design-considerations}

I Forms con layout scorrevoli si basano sulle progettazioni dei moduli create in Designer. La progettazione di un modulo specifica un set di regole di layout, presentazione e acquisizione dati, inclusi i valori di calcolo basati su input dell&#39;utente. Le regole vengono applicate quando i dati vengono immessi in un modulo. I campi aggiunti a un modulo sono sottomaschere incluse nella struttura del modulo. Ad esempio, nel modulo ordine fornitore visualizzato nel diagramma precedente, ogni linea è una sottomaschera. Per informazioni sulla creazione di una struttura di modulo contenente sottomaschere, vedere [Creazione di un modulo ordine fornitore con un layout scorrevole](https://www.adobe.com/go/learn_aemforms_qs_poformflowable_9).

### Informazioni sui sottogruppi di dati {#understanding-data-subgroups}

Un&#39;origine dati XML viene utilizzata per precompilare i moduli con layout fissi e con layout scorrevoli. Tuttavia, la differenza consiste nel fatto che un&#39;origine dati XML che precompila un modulo con un layout scorrevole contiene elementi XML ripetuti utilizzati per precompilare sottomaschere ripetute all&#39;interno del modulo. Questi elementi XML ripetuti sono denominati sottogruppi di dati.

Un&#39;origine dati XML utilizzata per precompilare il modulo dell&#39;ordine di acquisto mostrato nel diagramma precedente contiene quattro sottogruppi di dati ripetuti. Ogni sottogruppo di dati corrisponde a un articolo acquistato. Gli articoli acquistati sono un monitor, una lampada da tavolo, un telefono e una rubrica.

Per precompilare il modulo dell&#39;ordine fornitore viene utilizzata la seguente origine dati XML.

```xml
     <header>
         <!-- XML elements used to prepopulate non-repeating fields such as address
         <!and city
         <txtPONum>8745236985</txtPONum>
         <dtmDate>2004-02-08</dtmDate>
         <txtOrderedByCompanyName>Any Company Name</txtOrderedByCompanyName>
         <txtOrderedByAddress>555, Any Blvd.</txtOrderedByAddress>
         <txtOrderedByCity>Any City</txtOrderedByCity>
         <txtOrderedByStateProv>ST</txtOrderedByStateProv>
         <txtOrderedByZipCode>12345</txtOrderedByZipCode>
         <txtOrderedByCountry>Any Country</txtOrderedByCountry>
         <txtOrderedByPhone>(123) 456-7890</txtOrderedByPhone>
         <txtOrderedByFax>(123) 456-7899</txtOrderedByFax>
         <txtOrderedByContactName>Contact Name</txtOrderedByContactName>
         <txtDeliverToCompanyName>Any Company Name</txtDeliverToCompanyName>
         <txtDeliverToAddress>7895, Any Street</txtDeliverToAddress>
         <txtDeliverToCity>Any City</txtDeliverToCity>
         <txtDeliverToStateProv>ST</txtDeliverToStateProv>
         <txtDeliverToZipCode>12346</txtDeliverToZipCode>
         <txtDeliverToCountry>Any Country</txtDeliverToCountry>
         <txtDeliverToPhone>(123) 456-7891</txtDeliverToPhone>
         <txtDeliverToFax>(123) 456-7899</txtDeliverToFax>
         <txtDeliverToContactName>Contact Name</txtDeliverToContactName>
     </header>
     <detail>
         <!-- A data subgroup that contains information about the monitor>
         <txtPartNum>00010-100</txtPartNum>
         <txtDescription>Monitor</txtDescription>
         <numQty>1</numQty>
         <numUnitPrice>350.00</numUnitPrice>
     </detail>
     <detail>
         <!-- A data subgroup that contains information about the desk lamp>
         <txtPartNum>00010-200</txtPartNum>
         <txtDescription>Desk lamps</txtDescription>
         <numQty>3</numQty>
         <numUnitPrice>55.00</numUnitPrice>
     </detail>
     <detail>
         <!-- A data subgroup that contains information about the Phone>
             <txtPartNum>00025-275</txtPartNum>
             <txtDescription>Phone</txtDescription>
             <numQty>5</numQty>
             <numUnitPrice>85.00</numUnitPrice>
     </detail>
     <detail>
         <!-- A data subgroup that contains information about the address book>
         <txtPartNum>00300-896</txtPartNum>
         <txtDescription>Address book</txtDescription>
         <numQty>2</numQty>
         <numUnitPrice>15.00</numUnitPrice>
     </detail>
```

Si noti che ogni sottogruppo di dati contiene quattro elementi XML corrispondenti a queste informazioni:

* Numero parte articoli
* Descrizione elementi
* Quantità di articoli
* Prezzo unitario

Il nome dell&#39;elemento XML padre di un sottogruppo di dati deve corrispondere al nome del sottomodulo incluso nella struttura del modulo. Ad esempio, nel diagramma precedente, si noti che il nome dell&#39;elemento XML padre del sottogruppo di dati è `detail`. Corrisponde al nome della sottomaschera presente nella struttura della maschera su cui si basa la maschera dell&#39;ordine fornitore. Se il nome dell&#39;elemento XML padre del sottogruppo di dati e il sottomodulo non corrispondono, un modulo lato server non viene precompilato.

Ogni sottogruppo di dati deve contenere elementi XML corrispondenti ai nomi dei campi nel sottomodulo. Il sottomodulo `detail` nella struttura del modulo contiene i campi seguenti:

* txtPartNum
* txtDescription
* numQtà
* numUnitPrice

>[!NOTE]
>
>Se si tenta di precompilare un modulo con un&#39;origine dati contenente elementi XML ripetuti e si imposta l&#39;opzione `RenderAtClient` su `No`, nel modulo verrà unito solo il primo record di dati. Per garantire che tutti i record di dati vengano uniti nel modulo, impostare `RenderAtClient` su `Yes`. Per informazioni sull&#39;opzione `RenderAtClient`, vedere [Rendering di Forms nel client](/help/forms/developing/rendering-forms-client.md).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per precompilare un modulo con un layout scorrevole, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un&#39;origine dati XML in memoria.
1. Convertire l&#39;origine dati XML.
1. Eseguire il rendering di un modulo precompilato.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un&#39;origine dati XML in memoria**

È possibile utilizzare `org.w3c.dom` classi per creare un&#39;origine dati XML in memoria per precompilare un modulo con un layout scorrevole. Inserire i dati in un&#39;origine dati XML conforme al modulo. Per informazioni sulla relazione tra un modulo con un layout scorrevole e l&#39;origine dati XML, vedere [Informazioni sui sottogruppi di dati](#understanding-data-subgroups).

**Convertire l&#39;origine dati XML**

Un&#39;origine dati XML in memoria creata mediante le classi `org.w3c.dom` può essere convertita in un oggetto `com.adobe.idp.Document` prima di poter essere utilizzata per precompilare un modulo. Un&#39;origine dati XML in memoria può essere convertita utilizzando le classi di trasformazione XML Java.

>[!NOTE]
>
>Se si utilizza il file WSDL del servizio Forms per precompilare un modulo, è necessario convertire un oggetto `org.w3c.dom.Document` in un oggetto `BLOB`.

**Eseguire il rendering di un modulo precompilato**

Si esegue il rendering di un modulo precompilato come di un altro modulo. L&#39;unica differenza consiste nell&#39;utilizzo dell&#39;oggetto `com.adobe.idp.Document` che contiene l&#39;origine dati XML per precompilare il modulo.

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Guida introduttiva all’API di servizio Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendering dei PDF forms interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Precompilazione dei moduli tramite API Java {#prepopulating-forms-using-the-java-api}

Per precompilare un modulo con un layout scorrevole utilizzando l’API Forms (Java), effettua le seguenti operazioni:

1. Includi file di progetto

   Includi i file JAR client, ad esempio adobe-forms-client.jar, nel percorso di classe del progetto Java. Per informazioni sul percorso di questi file, vedere [Inclusi i file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Creare un&#39;origine dati XML in memoria

   * Creare un oggetto Java `DocumentBuilderFactory` chiamando il metodo `newInstance` della classe `DocumentBuilderFactory`.
   * Creare un oggetto Java `DocumentBuilder` chiamando il metodo `newDocumentBuilder` dell&#39;oggetto `DocumentBuilderFactory`.
   * Chiamare il metodo `newDocument` dell&#39;oggetto `DocumentBuilder` per creare un&#39;istanza di un oggetto `org.w3c.dom.Document`.
   * Creare l&#39;elemento radice dell&#39;origine dati XML richiamando il metodo `createElement` dell&#39;oggetto `org.w3c.dom.Document`. Viene creato un oggetto `Element` che rappresenta l&#39;elemento radice. Passa un valore stringa che rappresenta il nome dell&#39;elemento al metodo `createElement`. Eseguire il cast del valore restituito in `Element`. Aggiungere quindi l&#39;elemento radice al documento chiamando il metodo `appendChild` dell&#39;oggetto `Document` e passare l&#39;oggetto elemento radice come argomento. Le seguenti righe di codice mostrano questa logica dell’applicazione:

     ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * Creare l&#39;elemento di intestazione dell&#39;origine dati XML chiamando il metodo `createElement` dell&#39;oggetto `Document`. Passa un valore stringa che rappresenta il nome dell&#39;elemento al metodo `createElement`. Eseguire il cast del valore restituito in `Element`. Aggiungere quindi l&#39;elemento header all&#39;elemento root chiamando il metodo `appendChild` dell&#39;oggetto `root` e passare l&#39;oggetto header come argomento. Gli elementi XML accodati all&#39;elemento header corrispondono alla parte statica del modulo. Le seguenti righe di codice mostrano questa logica dell’applicazione:

     ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * Creare un elemento figlio appartenente all&#39;elemento header chiamando il metodo `createElement` dell&#39;oggetto `Document` e passare un valore string che rappresenta il nome dell&#39;elemento. Eseguire il cast del valore restituito in `Element`. Impostare quindi un valore per l&#39;elemento figlio chiamando il relativo metodo `appendChild` e passare il metodo `createTextNode` dell&#39;oggetto `Document` come argomento. Specifica un valore stringa che viene visualizzato come valore dell&#39;elemento figlio. Infine, accodare l&#39;elemento figlio all&#39;elemento header chiamando il metodo `appendChild` dell&#39;elemento header e passare l&#39;oggetto elemento figlio come argomento. Le seguenti righe di codice mostrano questa logica dell’applicazione:

     ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`


   * Aggiungere tutti gli elementi rimanenti all&#39;elemento header ripetendo l&#39;ultimo passaggio secondario per ogni campo visualizzato nella parte statica del modulo (nel diagramma origine dati XML questi campi sono visualizzati nella sezione A. Vedere [Informazioni sui sottogruppi di dati](#understanding-data-subgroups).)
   * Creare l&#39;elemento dettaglio dell&#39;origine dati XML chiamando il metodo `createElement` dell&#39;oggetto `Document`. Passa un valore stringa che rappresenta il nome dell&#39;elemento al metodo `createElement`. Eseguire il cast del valore restituito in `Element`. Aggiungere quindi l&#39;elemento di dettaglio all&#39;elemento radice chiamando il metodo `appendChild` dell&#39;oggetto `root` e passare l&#39;oggetto elemento di dettaglio come argomento. Gli elementi XML accodati all&#39;elemento dettaglio corrispondono alla parte dinamica del modulo. Le seguenti righe di codice mostrano questa logica dell’applicazione:

     ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * Creare un elemento figlio che appartiene all&#39;elemento dettaglio chiamando il metodo `createElement` dell&#39;oggetto `Document` e passare un valore stringa che rappresenta il nome dell&#39;elemento. Eseguire il cast del valore restituito in `Element`. Impostare quindi un valore per l&#39;elemento figlio chiamando il relativo metodo `appendChild` e passare il metodo `createTextNode` dell&#39;oggetto `Document` come argomento. Specifica un valore stringa che viene visualizzato come valore dell&#39;elemento figlio. Infine, aggiungere l&#39;elemento figlio all&#39;elemento dettaglio chiamando il metodo `appendChild` dell&#39;elemento dettaglio e passare l&#39;oggetto elemento figlio come argomento. Le seguenti righe di codice mostrano questa logica dell’applicazione:

     ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * Ripetere l&#39;ultimo passaggio secondario per tutti gli elementi XML da aggiungere all&#39;elemento dettaglio. Per creare correttamente l&#39;origine dati XML utilizzata per compilare il modulo dell&#39;ordine fornitore, è necessario aggiungere i seguenti elementi XML all&#39;elemento dettaglio: `txtDescription`, `numQty` e `numUnitPrice`.
   * Ripeti gli ultimi due passaggi secondari per tutti gli elementi di dati utilizzati per precompilare il modulo.

1. Convertire l&#39;origine dati XML

   * Creare un oggetto `javax.xml.transform.Transformer` richiamando il metodo `newInstance` statico dell&#39;oggetto `javax.xml.transform.Transformer`.
   * Creare un oggetto `Transformer` richiamando il metodo `newTransformer` dell&#39;oggetto `TransformerFactory`.
   * Creare un oggetto `ByteArrayOutputStream` utilizzando il relativo costruttore.
   * Creare un oggetto `javax.xml.transform.dom.DOMSource` utilizzando il relativo costruttore e passando l&#39;oggetto `org.w3c.dom.Document` creato nel passaggio 1.
   * Creare un oggetto `javax.xml.transform.dom.DOMSource` utilizzando il relativo costruttore e passando l&#39;oggetto `ByteArrayOutputStream`.
   * Compilare l&#39;oggetto Java `ByteArrayOutputStream` richiamando il metodo `transform` dell&#39;oggetto `javax.xml.transform.Transformer` e passando gli oggetti `javax.xml.transform.dom.DOMSource` e `javax.xml.transform.stream.StreamResult`.
   * Creare una matrice di byte e allocare le dimensioni dell&#39;oggetto `ByteArrayOutputStream` alla matrice di byte.
   * Compilare la matrice di byte richiamando il metodo `toByteArray` dell&#39;oggetto `ByteArrayOutputStream`.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando la matrice di byte.

1. Rendering di un modulo precompilato

   Richiama il metodo `renderPDFForm` dell&#39;oggetto `FormsServiceClient` e passa i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file.
   * Oggetto `com.adobe.idp.Document` contenente dati da unire al modulo. Assicurarsi di utilizzare l&#39;oggetto `com.adobe.idp.Document` creato nei passaggi uno e due.
   * Un oggetto `PDFFormRenderSpec` che memorizza le opzioni di runtime.
   * Oggetto `URLSpec` contenente i valori URI richiesti dal servizio Forms.
   * Oggetto `java.util.HashMap` che memorizza gli allegati. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.

   Il metodo `renderPDFForm` restituisce un oggetto `FormsResult` che contiene un flusso di dati del modulo che deve essere scritto nel browser Web client.

   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per inviare un flusso di dati modulo al browser Web client.
   * Creare un oggetto `com.adobe.idp.Document` richiamando il metodo `getOutputContent` dell&#39;oggetto `FormsResult`.
   * Creare un oggetto `java.io.InputStream` richiamando il metodo `getInputStream` dell&#39;oggetto `com.adobe.idp.Document`.
   * Creare una matrice di byte popolarla con il flusso di dati del modulo richiamando il metodo `read` dell&#39;oggetto `InputStream` e passando la matrice di byte come argomento.
   * Richiama il metodo `write` dell&#39;oggetto `javax.servlet.ServletOutputStream` per inviare il flusso di dati del modulo al browser Web client. Passare la matrice di byte al metodo `write`.

**Consulta anche**

[Quick Start (modalità SOAP): precompilazione di Forms con layout accessibili tramite API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Precompilazione dei moduli tramite l’API del servizio web {#prepopulating-forms-using-the-web-service-api}

Per precompilare un modulo con un layout scorrevole utilizzando l’API di Forms (servizio web), effettua le seguenti operazioni:

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio Forms WSDL. (Vedi [Creazione di classi proxy Java tramite l&#39;asse Apache](/help/forms/developing/invoking-aem-forms-using-web.md#creating-java-proxy-classes-using-apache-axis).)
   * Includi le classi proxy Java nel percorso della classe.

1. Creare un&#39;origine dati XML in memoria

   * Creare un oggetto Java `DocumentBuilderFactory` chiamando il metodo `newInstance` della classe `DocumentBuilderFactory`.
   * Creare un oggetto Java `DocumentBuilder` chiamando il metodo `newDocumentBuilder` dell&#39;oggetto `DocumentBuilderFactory`.
   * Chiamare il metodo `newDocument` dell&#39;oggetto `DocumentBuilder` per creare un&#39;istanza di un oggetto `org.w3c.dom.Document`.
   * Creare l&#39;elemento radice dell&#39;origine dati XML richiamando il metodo `createElement` dell&#39;oggetto `org.w3c.dom.Document`. Viene creato un oggetto `Element` che rappresenta l&#39;elemento radice. Passa un valore stringa che rappresenta il nome dell&#39;elemento al metodo `createElement`. Eseguire il cast del valore restituito in `Element`. Aggiungere quindi l&#39;elemento radice al documento chiamando il metodo `appendChild` dell&#39;oggetto `Document` e passare l&#39;oggetto elemento radice come argomento. Le seguenti righe di codice mostrano questa logica dell’applicazione:

     ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * Creare l&#39;elemento di intestazione dell&#39;origine dati XML chiamando il metodo `createElement` dell&#39;oggetto `Document`. Passa un valore stringa che rappresenta il nome dell&#39;elemento al metodo `createElement`. Eseguire il cast del valore restituito in `Element`. Aggiungere quindi l&#39;elemento header all&#39;elemento root chiamando il metodo `appendChild` dell&#39;oggetto `root` e passare l&#39;oggetto header come argomento. Gli elementi XML accodati all&#39;elemento header corrispondono alla parte statica del modulo. Le seguenti righe di codice mostrano questa logica dell’applicazione:

     ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * Creare un elemento figlio appartenente all&#39;elemento header chiamando il metodo `createElement` dell&#39;oggetto `Document` e passare un valore string che rappresenta il nome dell&#39;elemento. Eseguire il cast del valore restituito in `Element`. Impostare quindi un valore per l&#39;elemento figlio chiamando il relativo metodo `appendChild` e passare il metodo `createTextNode` dell&#39;oggetto `Document` come argomento. Specifica un valore stringa che viene visualizzato come valore dell&#39;elemento figlio. Infine, accodare l&#39;elemento figlio all&#39;elemento header chiamando il metodo `appendChild` dell&#39;elemento header e passare l&#39;oggetto elemento figlio come argomento. Le seguenti righe di codice mostrano questa logica dell’applicazione:

     ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`

   * Aggiungere tutti gli elementi rimanenti all&#39;elemento header ripetendo l&#39;ultimo passaggio secondario per ogni campo visualizzato nella parte statica del modulo (nel diagramma origine dati XML questi campi sono visualizzati nella sezione A. Vedere [Informazioni sui sottogruppi di dati](#understanding-data-subgroups).)
   * Creare l&#39;elemento dettaglio dell&#39;origine dati XML chiamando il metodo `createElement` dell&#39;oggetto `Document`. Passa un valore stringa che rappresenta il nome dell&#39;elemento al metodo `createElement`. Eseguire il cast del valore restituito in `Element`. Aggiungere quindi l&#39;elemento di dettaglio all&#39;elemento radice chiamando il metodo `appendChild` dell&#39;oggetto `root` e passare l&#39;oggetto elemento di dettaglio come argomento. Gli elementi XML accodati all&#39;elemento dettaglio corrispondono alla parte dinamica del modulo. Le seguenti righe di codice mostrano questa logica dell’applicazione:

     ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * Creare un elemento figlio che appartiene all&#39;elemento dettaglio chiamando il metodo `createElement` dell&#39;oggetto `Document` e passare un valore stringa che rappresenta il nome dell&#39;elemento. Eseguire il cast del valore restituito in `Element`. Impostare quindi un valore per l&#39;elemento figlio chiamando il relativo metodo `appendChild` e passare il metodo `createTextNode` dell&#39;oggetto `Document` come argomento. Specifica un valore stringa che viene visualizzato come valore dell&#39;elemento figlio. Infine, aggiungere l&#39;elemento figlio all&#39;elemento dettaglio chiamando il metodo `appendChild` dell&#39;elemento dettaglio e passare l&#39;oggetto elemento figlio come argomento. Le seguenti righe di codice mostrano questa logica dell’applicazione:

     ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * Ripetere l&#39;ultimo passaggio secondario per tutti gli elementi XML da aggiungere all&#39;elemento dettaglio. Per creare correttamente l&#39;origine dati XML utilizzata per compilare il modulo dell&#39;ordine fornitore, è necessario aggiungere i seguenti elementi XML all&#39;elemento dettaglio: `txtDescription`, `numQty` e `numUnitPrice`.
   * Ripeti gli ultimi due passaggi secondari per tutti gli elementi di dati utilizzati per precompilare il modulo.

1. Convertire l&#39;origine dati XML

   * Creare un oggetto `javax.xml.transform.Transformer` richiamando il metodo `newInstance` statico dell&#39;oggetto `javax.xml.transform.Transformer`.
   * Creare un oggetto `Transformer` richiamando il metodo `newTransformer` dell&#39;oggetto `TransformerFactory`.
   * Creare un oggetto `ByteArrayOutputStream` utilizzando il relativo costruttore.
   * Creare un oggetto `javax.xml.transform.dom.DOMSource` utilizzando il relativo costruttore e passando l&#39;oggetto `org.w3c.dom.Document` creato nel passaggio 1.
   * Creare un oggetto `javax.xml.transform.dom.DOMSource` utilizzando il relativo costruttore e passando l&#39;oggetto `ByteArrayOutputStream`.
   * Compilare l&#39;oggetto Java `ByteArrayOutputStream` richiamando il metodo `transform` dell&#39;oggetto `javax.xml.transform.Transformer` e passando gli oggetti `javax.xml.transform.dom.DOMSource` e `javax.xml.transform.stream.StreamResult`.
   * Creare una matrice di byte e allocare le dimensioni dell&#39;oggetto `ByteArrayOutputStream` alla matrice di byte.
   * Compilare la matrice di byte richiamando il metodo `toByteArray` dell&#39;oggetto `ByteArrayOutputStream`.
   * Creare un oggetto `BLOB` utilizzando il costruttore, richiamare il metodo `setBinaryData` e passare la matrice di byte.

1. Rendering di un modulo precompilato

   Richiama il metodo `renderPDFForm` dell&#39;oggetto `FormsService` e passa i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file.
   * Oggetto `BLOB` contenente dati da unire al modulo. Assicurarsi di utilizzare l&#39;oggetto `BLOB` creato nei passaggi uno e due.
   * Un oggetto `PDFFormRenderSpecc` che memorizza le opzioni di runtime. Per ulteriori informazioni, consulta [Riferimento API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Oggetto `URLSpec` contenente i valori URI richiesti dal servizio Forms.
   * Oggetto `java.util.HashMap` che memorizza gli allegati. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.
   * Oggetto `com.adobe.idp.services.holders.BLOBHolder` vuoto popolato dal metodo. Viene utilizzato per memorizzare il modulo PDF di cui è stato eseguito il rendering.
   * Oggetto `javax.xml.rpc.holders.LongHolder` vuoto popolato dal metodo. Questo argomento consente di memorizzare il numero di pagine nel modulo.
   * Oggetto `javax.xml.rpc.holders.StringHolder` vuoto popolato dal metodo. Questo argomento consente di memorizzare il valore delle impostazioni locali.
   * Oggetto `com.adobe.idp.services.holders.FormsResultHolder` vuoto che conterrà i risultati dell&#39;operazione.

   Il metodo `renderPDFForm` popola l&#39;oggetto `com.adobe.idp.services.holders.FormsResultHolder` passato come ultimo valore di argomento con un flusso di dati del modulo che deve essere scritto nel browser Web client.

   * Creare un oggetto `FormResult` ottenendo il valore del membro dati `value` dell&#39;oggetto `com.adobe.idp.services.holders.FormsResultHolder`.
   * Creare un oggetto `BLOB` contenente dati del modulo richiamando il metodo `getOutputContent` dell&#39;oggetto `FormsResult`.
   * Ottenere il tipo di contenuto dell&#39;oggetto `BLOB` richiamando il relativo metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamando il relativo metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `BLOB`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il metodo `getOutputStream` dell&#39;oggetto `javax.servlet.http.HttpServletResponse`.
   * Creare una matrice di byte e popolarla richiamando il metodo `getBinaryData` dell&#39;oggetto `BLOB`. Questa attività assegna il contenuto dell&#39;oggetto `FormsResult` alla matrice di byte.
   * Richiama il metodo `write` dell&#39;oggetto `javax.servlet.http.HttpServletResponse` per inviare il flusso di dati del modulo al browser Web client. Passare la matrice di byte al metodo `write`.

   >[!NOTE]
   >
   >Il metodo `renderPDFForm` popola l&#39;oggetto `com.adobe.idp.services.holders.FormsResultHolder` passato come ultimo valore di argomento con un flusso di dati del modulo che deve essere scritto nel browser Web client.

**Consulta anche**

[Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
