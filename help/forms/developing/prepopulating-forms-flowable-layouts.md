---
title: Precompilazione di Forms con layout fluidi
seo-title: Prepopulating Forms with Flowable Layouts
description: Precompilare i moduli con layout scorrevole per mostrare i dati agli utenti all’interno di un modulo di cui è stato effettuato il rendering utilizzando l’API Java e l’API Web Service.
seo-description: Prepopulate forms with flowable layout to display data to users within a rendered form using the Java API and the Web Service API.
uuid: 93ccb496-e1c2-4b79-8e89-7a2abfce1537
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 30a12fc6-07b8-4c7c-b9e2-caa2bec0ac48
role: Developer
exl-id: ff087084-fb1c-43a4-ae54-cc77eb862493
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '3505'
ht-degree: 0%

---

# Precompilazione di Forms con layout fluidi {#prepopulating-forms-with-flowable-layouts1}

## Precompilazione di Forms con layout fluidi {#prepopulating-forms-with-flowable-layouts2}

La precompilazione dei moduli visualizza i dati per gli utenti all’interno di un modulo di cui è stato effettuato il rendering. Ad esempio, si supponga che un utente effettui l’accesso a un sito web con un nome utente e una password. Se l&#39;autenticazione ha esito positivo, l&#39;applicazione client invia una query a un database per ottenere informazioni sull&#39;utente. I dati vengono uniti nel modulo, quindi l’utente esegue il rendering del modulo. Di conseguenza, l’utente può visualizzare dati personalizzati all’interno del modulo.

La precompilazione di un modulo presenta i seguenti vantaggi:

* Consente all’utente di visualizzare i dati personalizzati in un modulo.
* Riduce la quantità di digitazione che l’utente fa per compilare un modulo.
* Assicura l’integrità dei dati controllando dove vengono inseriti i dati.

È possibile precompilare un modulo con le due origini dati XML seguenti:

* Un’origine dati XDP, XML conforme alla sintassi XFA (o dati XFDF per precompilare un modulo creato con Acrobat).
* Un’origine dati XML arbitraria che contiene coppie nome/valore corrispondenti ai nomi dei campi del modulo (gli esempi in questa sezione utilizzano un’origine dati XML arbitraria).

Per ogni campo del modulo che si desidera precompilare deve esistere un elemento XML. Il nome dell&#39;elemento XML deve corrispondere al nome del campo. Un elemento XML viene ignorato se non corrisponde a un campo modulo o se il nome dell’elemento XML non corrisponde al nome del campo. Non è necessario stabilire una corrispondenza con l&#39;ordine di visualizzazione degli elementi XML, purché siano specificati tutti gli elementi XML.

Quando si precompila un modulo che contiene già dati, è necessario specificare i dati già visualizzati nell’origine dati XML. Si supponga che un modulo contenente 10 campi includa dati in quattro campi. Quindi, si supponga di voler precompilare i sei campi rimanenti. In questa situazione, è necessario specificare 10 elementi XML nell’origine dati XML utilizzata per precompilare il modulo. Se specifichi solo sei elementi, i quattro campi originali sono vuoti.

Ad esempio, puoi precompilare un modulo, ad esempio il modulo di conferma di esempio. (Vedi &quot;Modulo di conferma&quot; in [Rendering di PDF forms interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md).)

Per precompilare il modulo di conferma di esempio, è necessario creare un’origine dati XML contenente tre elementi XML che corrispondono ai tre campi del modulo. Questo modulo contiene i tre campi seguenti: `FirstName`, `LastName`e `Amount`. Il primo passaggio consiste nel creare un’origine dati XML contenente elementi XML che corrispondono ai campi presenti nella struttura del modulo. Il passaggio successivo consiste nell&#39;assegnare valori di dati agli elementi XML, come mostrato nel seguente codice XML.

```xml
     <Untitled>
         <FirstName>Jerry</FirstName>
         <LastName>Johnson</LastName>
         <Amount>250000</Amount>
     </Untitled>
```

Dopo aver precompilato il modulo di conferma con questa origine dati XML ed eseguito il rendering del modulo, vengono visualizzati i valori dei dati assegnati agli elementi XML, come illustrato nel diagramma seguente.

![pf_pf_Confirm3](assets/pf_pf_confirmxml3.png)

### Precompilazione dei moduli con layout scorrevole {#prepopulating_forms_with_flowable_layouts-1}

Forms con layout scorrevole è utile per visualizzare agli utenti una quantità indeterminata di dati. Poiché il layout del modulo si regola automaticamente sulla quantità di dati unita, non è necessario determinare un layout fisso o un numero di pagine per il modulo come è necessario fare con un modulo con layout fisso.

Un modulo viene in genere compilato con i dati ottenuti durante l’esecuzione. Di conseguenza, è possibile precompilare un modulo creando un’origine dati XML in-memory e inserendo i dati direttamente nell’origine dati XML in-memory.

Considera un&#39;applicazione basata sul web, ad esempio un negozio online. Al termine dell’acquisto di un acquirente online, tutti gli articoli acquistati vengono inseriti in un’origine dati XML in memoria utilizzata per precompilare un modulo. Il diagramma seguente illustra questo processo, illustrato nella tabella che segue il diagramma.

![pf_pf_finsrv_webapp_v1](assets/pf_pf_finsrv_webapp_v1.png)

La tabella seguente descrive i passaggi descritti in questo diagramma.

<table>
 <thead>
  <tr>
   <th><p>Incremento</p></th>
   <th><p>Descrizione</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>Un utente acquista articoli da un negozio online basato sul web. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Al termine dell’acquisto degli articoli e dopo aver fatto clic sul pulsante Invia, viene creata un’origine dati XML in memoria. Gli elementi acquistati e le informazioni utente vengono inseriti nell’origine dati XML in memoria. </p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>L'origine dati XML viene utilizzata per precompilare un modulo di ordine di acquisto (un esempio di questo modulo viene mostrato nella tabella seguente). </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Viene eseguito il rendering del modulo dell’ordine di acquisto nel browser Web del client. </p></td>
  </tr>
 </tbody>
</table>

Il diagramma seguente mostra un esempio di modulo di ordine di acquisto. Le informazioni contenute nella tabella possono adattarsi al numero di record presenti nei dati XML.

![pf_pf_poform](assets/pf_pf_poform.png)

>[!NOTE]
>
>Un modulo può essere precompilato con dati provenienti da altre origini, ad esempio da un database aziendale o da applicazioni esterne.

### Considerazioni sulla struttura del modulo {#form-design-considerations}

Forms con layout scorrevole si basa sulle strutture del modulo create in Designer. Una struttura del modulo specifica un insieme di regole di layout, presentazione e acquisizione dati, incluso il calcolo dei valori in base all’input dell’utente. Le regole vengono applicate quando i dati vengono immessi in un modulo. I campi aggiunti a un modulo sono sottomoduli che si trovano all’interno della struttura del modulo. Ad esempio, nel modulo dell&#39;ordine di acquisto visualizzato nel diagramma precedente, ogni riga è un sottomodulo. Per informazioni sulla creazione di una struttura del modulo contenente sottomoduli, vedere [Creazione di un modulo di ordine di acquisto con layout scorrevole](https://www.adobe.com/go/learn_aemforms_qs_poformflowable_9).

### Informazioni sui sottogruppi di dati {#understanding-data-subgroups}

Un’origine dati XML viene utilizzata per precompilare i moduli con layout fissi e scorrevoli. Tuttavia, la differenza consiste nel fatto che un’origine dati XML che precompila un modulo con layout scorrevole contiene elementi XML ripetuti utilizzati per precompilare i sottomoduli che vengono ripetuti all’interno del modulo. Questi elementi XML ripetuti sono denominati sottogruppi di dati.

Un’origine dati XML utilizzata per precompilare il modulo dell’ordine di acquisto visualizzato nel diagramma precedente contiene quattro sottogruppi di dati ripetuti. Ogni sottogruppo di dati corrisponde a un articolo acquistato. Gli articoli acquistati sono un monitor, una lampada da tavolo, un telefono e una rubrica.

La seguente origine dati XML viene utilizzata per precompilare il modulo dell&#39;ordine di acquisto.

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

Tieni presente che ogni sottogruppo di dati contiene quattro elementi XML corrispondenti a queste informazioni:

* Numero parte elementi
* Descrizione elementi
* Quantità di articoli
* Prezzo unitario

Il nome dell’elemento XML padre di un sottogruppo di dati deve corrispondere al nome del sottomodulo che si trova nella struttura del modulo. Ad esempio, nel diagramma precedente, notare che il nome dell’elemento XML principale del sottogruppo di dati è `detail`. Questo corrisponde al nome del sottomodulo che si trova nella struttura del modulo su cui è basato il modulo dell&#39;ordine di acquisto. Se il nome dell’elemento XML padre del sottogruppo di dati e il sottomodulo non corrispondono, un modulo lato server non viene precompilato.

Ciascun sottogruppo di dati deve contenere elementi XML che corrispondono ai nomi dei campi nel sottomodulo. La `detail` il sottomodulo che si trova nella struttura del modulo contiene i campi seguenti:

* txtPartNum
* txtDescription
* numQty
* numUnitPrice

>[!NOTE]
>
>Se si tenta di precompilare un modulo con un&#39;origine dati che contiene elementi XML ripetuti e si imposta la proprietà `RenderAtClient` opzione per `No`, nel modulo viene unito solo il primo record di dati. Per garantire l’unione di tutti i record di dati nel modulo, impostare la `RenderAtClient` a `Yes`. Per informazioni sulla `RenderAtClient` opzione , vedi [Rendering di Forms sul client](/help/forms/developing/rendering-forms-client.md).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per precompilare un modulo con un layout scorrevole, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un&#39;origine dati XML in memoria.
1. Convertire l&#39;origine dati XML.
1. Eseguire il rendering di un modulo precompilato.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un’origine dati XML in memoria**

È possibile utilizzare `org.w3c.dom` classi per creare un’origine dati XML in memoria per precompilare un modulo con un layout scorrevole. È necessario inserire i dati in un’origine dati XML conforme al modulo. Per informazioni sul rapporto tra un modulo con layout scorrevole e l&#39;origine dati XML, vedere [Informazioni sui sottogruppi di dati](#understanding-data-subgroups).

**Convertire l’origine dati XML**

Origine dati XML in memoria creata utilizzando `org.w3c.dom` le classi possono essere convertite in un `com.adobe.idp.Document` prima di poter essere utilizzato per precompilare un modulo. Un’origine dati XML in memoria può essere convertita utilizzando le classi di trasformazione Java XML.

>[!NOTE]
>
>Se si utilizza il WSDL del servizio Forms per precompilare un modulo, è necessario convertire un `org.w3c.dom.Document` oggetto in un `BLOB` oggetto.

**Rendering di un modulo precompilato**

È possibile eseguire il rendering di un modulo precompilato come un altro modulo. L’unica differenza è che utilizzi il `com.adobe.idp.Document` oggetto che contiene l’origine dati XML per precompilare il modulo.

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendering di PDF forms interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Precompilazione dei moduli tramite l’API Java {#prepopulating-forms-using-the-java-api}

Per precompilare un modulo con un layout scorrevole utilizzando l’API Forms (Java), effettua le seguenti operazioni:

1. Includi file di progetto

   Includi file JAR client, come adobe-forms-client.jar, nel percorso di classe del progetto Java. Per informazioni sulla posizione di questi file, vedi [Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Creare un’origine dati XML in memoria

   * Creare un Java `DocumentBuilderFactory` chiamando `DocumentBuilderFactory` classe&quot; `newInstance` metodo .
   * Creare un Java `DocumentBuilder` chiamando `DocumentBuilderFactory` dell’oggetto `newDocumentBuilder` metodo .
   * Chiama il `DocumentBuilder` dell’oggetto `newDocument` per creare un&#39;istanza di un `org.w3c.dom.Document` oggetto.
   * Crea l’elemento principale dell’origine dati XML richiamando il `org.w3c.dom.Document` dell’oggetto `createElement` metodo . Questo crea un `Element` oggetto che rappresenta l&#39;elemento principale. Passa un valore stringa che rappresenta il nome dell&#39;elemento al `createElement` metodo . Imposta il valore restituito su `Element`. Quindi, aggiungi l&#39;elemento principale al documento chiamando il `Document` dell’oggetto `appendChild` e passare l&#39;oggetto elemento principale come argomento. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * Crea l’elemento intestazione dell’origine dati XML chiamando il `Document` dell’oggetto `createElement` metodo . Passa un valore stringa che rappresenta il nome dell&#39;elemento al `createElement` metodo . Imposta il valore restituito su `Element`. Quindi, aggiungi l’elemento header all’elemento root chiamando il `root` dell’oggetto `appendChild` e passare l&#39;oggetto header come argomento. Gli elementi XML aggiunti all’elemento header corrispondono alla parte statica del modulo. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * Crea un elemento figlio che appartiene all’elemento header chiamando il `Document` dell’oggetto `createElement` e passare un valore stringa che rappresenta il nome dell&#39;elemento. Imposta il valore restituito su `Element`. Quindi, imposta un valore per l’elemento figlio chiamando il relativo `appendChild` e passare il `Document` dell’oggetto `createTextNode` come argomento. Specifica un valore di stringa che viene visualizzato come valore dell&#39;elemento figlio. Infine, aggiungi l’elemento figlio all’elemento header chiamando l’elemento header `appendChild` e passare l&#39;oggetto elemento figlio come argomento. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`


   * Aggiungi tutti gli elementi rimanenti all’elemento intestazione ripetendo l’ultimo passaggio secondario per ciascun campo visualizzato nella parte statica del modulo (nel diagramma dell’origine dati XML, questi campi sono visualizzati nella sezione A. (Vedere [Informazioni sui sottogruppi di dati](#understanding-data-subgroups).)
   * Crea l’elemento di dettaglio dell’origine dati XML chiamando il `Document` dell’oggetto `createElement` metodo . Passa un valore stringa che rappresenta il nome dell&#39;elemento al `createElement` metodo . Imposta il valore restituito su `Element`. Quindi, aggiungi l’elemento dettaglio all’elemento principale chiamando il `root` dell’oggetto `appendChild` e passare l&#39;oggetto dell&#39;elemento dettaglio come argomento. Gli elementi XML aggiunti all’elemento dettaglio corrispondono alla parte dinamica del modulo. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * Crea un elemento figlio che appartiene all’elemento dettaglio chiamando il `Document` dell’oggetto `createElement` e passare un valore stringa che rappresenta il nome dell&#39;elemento. Imposta il valore restituito su `Element`. Quindi, imposta un valore per l’elemento figlio chiamando il relativo `appendChild` e passare il `Document` dell’oggetto `createTextNode` come argomento. Specifica un valore di stringa che viene visualizzato come valore dell&#39;elemento figlio. Infine, aggiungi l’elemento figlio all’elemento dettaglio chiamando l’elemento dettaglio `appendChild` e passare l&#39;oggetto elemento figlio come argomento. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * Ripeti l’ultimo passaggio secondario affinché tutti gli elementi XML vengano aggiunti all’elemento dettaglio. Per creare correttamente l&#39;origine dati XML utilizzata per compilare il modulo dell&#39;ordine di acquisto, è necessario aggiungere i seguenti elementi XML all&#39;elemento dettaglio: `txtDescription`, `numQty`e `numUnitPrice`.
   * Ripetere gli ultimi due passaggi secondari per tutti gli elementi dati utilizzati per precompilare il modulo.

1. Convertire l’origine dati XML

   * Crea un `javax.xml.transform.Transformer` richiamando l&#39;oggetto `javax.xml.transform.Transformer` statico dell’oggetto `newInstance` metodo .
   * Crea un `Transformer` richiamando l&#39;oggetto `TransformerFactory` dell’oggetto `newTransformer` metodo .
   * Crea un `ByteArrayOutputStream` utilizzando il relativo costruttore.
   * Crea un `javax.xml.transform.dom.DOMSource` utilizzando il relativo costruttore e passando `org.w3c.dom.Document` oggetto creato al passaggio 1.
   * Crea un `javax.xml.transform.dom.DOMSource` utilizzando il relativo costruttore e passando `ByteArrayOutputStream` oggetto.
   * Popolare Java `ByteArrayOutputStream` richiamando l&#39;oggetto `javax.xml.transform.Transformer` dell’oggetto `transform` e passare `javax.xml.transform.dom.DOMSource` e `javax.xml.transform.stream.StreamResult` oggetti.
   * Creare un array di byte e allocare le dimensioni del `ByteArrayOutputStream` all&#39;array di byte.
   * Compilare l’array di byte richiamando il `ByteArrayOutputStream` dell’oggetto `toByteArray` metodo .
   * Crea un `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;array di byte.

1. Rendering di un modulo precompilato

   Richiama il `FormsServiceClient` dell’oggetto `renderPDFForm` e passare i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file.
   * A `com.adobe.idp.Document` oggetto contenente i dati da unire al modulo. Assicurati di utilizzare `com.adobe.idp.Document` oggetto creato nei passaggi uno e due.
   * A `PDFFormRenderSpec` oggetto che memorizza le opzioni di esecuzione.
   * A `URLSpec` oggetto che contiene i valori URI richiesti dal servizio Forms.
   * A `java.util.HashMap` oggetto che memorizza gli allegati di file. Si tratta di un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.

   La `renderPDFForm` restituisce un `FormsResult` oggetto che contiene un flusso di dati del modulo che deve essere scritto nel browser Web client.

   * Crea un `javax.servlet.ServletOutputStream` oggetto utilizzato per inviare un flusso di dati del modulo al browser Web client.
   * Crea un `com.adobe.idp.Document` richiamando l&#39;oggetto `FormsResult` oggetto ‘s `getOutputContent` metodo .
   * Crea un `java.io.InputStream` richiamando l&#39;oggetto `com.adobe.idp.Document` dell’oggetto `getInputStream` metodo .
   * Creare un array di byte popolarlo con il flusso di dati del modulo richiamando il `InputStream` dell’oggetto `read` e passare l&#39;array di byte come argomento.
   * Richiama il `javax.servlet.ServletOutputStream` dell’oggetto `write` per inviare il flusso di dati del modulo al browser Web client. Passa l&#39;array di byte al `write` metodo .


**Consulta anche**

[Avvio rapido (modalità SOAP): Precompilazione di Forms con layout fluidi tramite l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Precompilazione dei moduli tramite l’API del servizio Web {#prepopulating-forms-using-the-web-service-api}

Per precompilare un modulo con un layout scorrevole utilizzando l’API Forms (servizio Web), esegui le seguenti operazioni:

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio WSDL di Forms. (Vedi [Creazione di classi proxy Java utilizzando Apache Axis](/help/forms/developing/invoking-aem-forms-using-web.md#creating-java-proxy-classes-using-apache-axis).)
   * Includi le classi proxy Java nel percorso della classe.

1. Creare un’origine dati XML in memoria

   * Creare un Java `DocumentBuilderFactory` chiamando `DocumentBuilderFactory` classe&quot; `newInstance` metodo .
   * Creare un Java `DocumentBuilder` chiamando `DocumentBuilderFactory` dell’oggetto `newDocumentBuilder` metodo .
   * Chiama il `DocumentBuilder` dell’oggetto `newDocument` per creare un&#39;istanza di un `org.w3c.dom.Document` oggetto.
   * Crea l’elemento principale dell’origine dati XML richiamando il `org.w3c.dom.Document` dell’oggetto `createElement` metodo . Questo crea un `Element` oggetto che rappresenta l&#39;elemento principale. Passa un valore stringa che rappresenta il nome dell&#39;elemento al `createElement` metodo . Imposta il valore restituito su `Element`. Quindi, aggiungi l&#39;elemento principale al documento chiamando il `Document` dell’oggetto `appendChild` e passare l&#39;oggetto elemento principale come argomento. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * Crea l’elemento intestazione dell’origine dati XML chiamando il `Document` dell’oggetto `createElement` metodo . Passa un valore stringa che rappresenta il nome dell&#39;elemento al `createElement` metodo . Imposta il valore restituito su `Element`. Quindi, aggiungi l’elemento header all’elemento root chiamando il `root` dell’oggetto `appendChild` e passare l&#39;oggetto header come argomento. Gli elementi XML aggiunti all’elemento header corrispondono alla parte statica del modulo. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * Crea un elemento figlio che appartiene all’elemento header chiamando il `Document` dell’oggetto `createElement` e passare un valore stringa che rappresenta il nome dell&#39;elemento. Imposta il valore restituito su `Element`. Quindi, imposta un valore per l’elemento figlio chiamando il relativo `appendChild` e passare il `Document` dell’oggetto `createTextNode` come argomento. Specifica un valore di stringa che viene visualizzato come valore dell&#39;elemento figlio. Infine, aggiungi l’elemento figlio all’elemento header chiamando l’elemento header `appendChild` e passare l&#39;oggetto elemento figlio come argomento. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`

   * Aggiungi tutti gli elementi rimanenti all’elemento intestazione ripetendo l’ultimo passaggio secondario per ciascun campo visualizzato nella parte statica del modulo (nel diagramma dell’origine dati XML, questi campi sono visualizzati nella sezione A. (Vedere [Informazioni sui sottogruppi di dati](#understanding-data-subgroups).)
   * Crea l’elemento di dettaglio dell’origine dati XML chiamando il `Document` dell’oggetto `createElement` metodo . Passa un valore stringa che rappresenta il nome dell&#39;elemento al `createElement` metodo . Imposta il valore restituito su `Element`. Quindi, aggiungi l’elemento dettaglio all’elemento principale chiamando il `root` dell’oggetto `appendChild` e passare l&#39;oggetto dell&#39;elemento dettaglio come argomento. Gli elementi XML aggiunti all’elemento dettaglio corrispondono alla parte dinamica del modulo. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * Crea un elemento figlio che appartiene all’elemento dettaglio chiamando il `Document` dell’oggetto `createElement` e passare un valore stringa che rappresenta il nome dell&#39;elemento. Imposta il valore restituito su `Element`. Quindi, imposta un valore per l’elemento figlio chiamando il relativo `appendChild` e passare il `Document` dell’oggetto `createTextNode` come argomento. Specifica un valore di stringa che viene visualizzato come valore dell&#39;elemento figlio. Infine, aggiungi l’elemento figlio all’elemento dettaglio chiamando l’elemento dettaglio `appendChild` e passare l&#39;oggetto elemento figlio come argomento. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * Ripeti l’ultimo passaggio secondario affinché tutti gli elementi XML vengano aggiunti all’elemento dettaglio. Per creare correttamente l&#39;origine dati XML utilizzata per compilare il modulo dell&#39;ordine di acquisto, è necessario aggiungere i seguenti elementi XML all&#39;elemento dettaglio: `txtDescription`, `numQty`e `numUnitPrice`.
   * Ripetere gli ultimi due passaggi secondari per tutti gli elementi dati utilizzati per precompilare il modulo.

1. Convertire l’origine dati XML

   * Crea un `javax.xml.transform.Transformer` richiamando l&#39;oggetto `javax.xml.transform.Transformer` statico dell’oggetto `newInstance` metodo .
   * Crea un `Transformer` richiamando l&#39;oggetto `TransformerFactory` dell’oggetto `newTransformer` metodo .
   * Crea un `ByteArrayOutputStream` utilizzando il relativo costruttore.
   * Crea un `javax.xml.transform.dom.DOMSource` utilizzando il relativo costruttore e passando `org.w3c.dom.Document` oggetto creato al passaggio 1.
   * Crea un `javax.xml.transform.dom.DOMSource` utilizzando il relativo costruttore e passando `ByteArrayOutputStream` oggetto.
   * Popolare Java `ByteArrayOutputStream` richiamando l&#39;oggetto `javax.xml.transform.Transformer` dell’oggetto `transform` e passare `javax.xml.transform.dom.DOMSource` e `javax.xml.transform.stream.StreamResult` oggetti.
   * Creare un array di byte e allocare le dimensioni del `ByteArrayOutputStream` all&#39;array di byte.
   * Compilare l’array di byte richiamando il `ByteArrayOutputStream` dell’oggetto `toByteArray` metodo .
   * Crea un `BLOB` utilizzando il relativo costruttore e richiamandone il `setBinaryData` e passare l&#39;array di byte.

1. Rendering di un modulo precompilato

   Richiama il `FormsService` dell’oggetto `renderPDFForm` e passare i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file.
   * A `BLOB` oggetto contenente i dati da unire al modulo. Assicurati di utilizzare `BLOB` oggetto creato nei passaggi uno e due.
   * A `PDFFormRenderSpecc` oggetto che memorizza le opzioni di esecuzione. Per ulteriori informazioni, consulta [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * A `URLSpec` oggetto che contiene i valori URI richiesti dal servizio Forms.
   * A `java.util.HashMap` oggetto che memorizza gli allegati di file. Si tratta di un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.
   * Un vuoto `com.adobe.idp.services.holders.BLOBHolder` oggetto popolato dal metodo . Viene utilizzato per memorizzare il modulo PDF di cui è stato eseguito il rendering.
   * Un vuoto `javax.xml.rpc.holders.LongHolder` oggetto popolato dal metodo . Questo argomento memorizza il numero di pagine nel modulo.
   * Un vuoto `javax.xml.rpc.holders.StringHolder` oggetto popolato dal metodo . (Questo argomento memorizza il valore delle impostazioni internazionali).
   * Un vuoto `com.adobe.idp.services.holders.FormsResultHolder` oggetto che conterrà i risultati dell&#39;operazione.

   La `renderPDFForm` popola il `com.adobe.idp.services.holders.FormsResultHolder` oggetto passato come ultimo valore argomento con un flusso di dati del modulo che deve essere scritto nel browser Web client.

   * Crea un `FormResult` ottenendo il valore del `com.adobe.idp.services.holders.FormsResultHolder` dell’oggetto `value` membro dati.
   * Crea un `BLOB` oggetto che contiene i dati del modulo richiamando il `FormsResult` dell’oggetto `getOutputContent` metodo .
   * Ottieni il tipo di contenuto del `BLOB` richiamandone l&#39;oggetto `getContentType` metodo .
   * Imposta la `javax.servlet.http.HttpServletResponse` tipo di contenuto dell’oggetto richiamandone il tipo `setContentType` e passare il tipo di contenuto `BLOB` oggetto.
   * Crea un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il `javax.servlet.http.HttpServletResponse` dell’oggetto `getOutputStream` metodo .
   * Creare un array di byte e compilarlo richiamando il `BLOB` dell’oggetto `getBinaryData` metodo . Questa attività assegna il contenuto del `FormsResult` all&#39;array di byte.
   * Richiama il `javax.servlet.http.HttpServletResponse` dell’oggetto `write` per inviare il flusso di dati del modulo al browser Web client. Passa l&#39;array di byte al `write` metodo .

   >[!NOTE]
   >
   >La `renderPDFForm` popola il `com.adobe.idp.services.holders.FormsResultHolder` oggetto passato come ultimo valore argomento con un flusso di dati del modulo che deve essere scritto nel browser Web client.

**Consulta anche**

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
