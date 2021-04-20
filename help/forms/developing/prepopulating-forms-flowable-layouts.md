---
title: Precompilazione di Forms con layout fluidi
seo-title: Precompilazione di Forms con layout fluidi
description: Precompilare i moduli con layout scorrevole per mostrare i dati agli utenti all’interno di un modulo di cui è stato effettuato il rendering utilizzando l’API Java e l’API Web Service.
seo-description: Precompilare i moduli con layout scorrevole per mostrare i dati agli utenti all’interno di un modulo di cui è stato effettuato il rendering utilizzando l’API Java e l’API Web Service.
uuid: 93ccb496-e1c2-4b79-8e89-7a2abfce1537
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 30a12fc6-07b8-4c7c-b9e2-caa2bec0ac48
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '3534'
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

Ad esempio, puoi precompilare un modulo, ad esempio il modulo di conferma di esempio. (Vedere &quot;Modulo di conferma&quot; in [Rendering di PDF forms interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md).)

Per precompilare il modulo di conferma di esempio, è necessario creare un’origine dati XML contenente tre elementi XML che corrispondono ai tre campi del modulo. Questo modulo contiene i tre campi seguenti: `FirstName`, `LastName` e `Amount`. Il primo passaggio consiste nel creare un’origine dati XML contenente elementi XML che corrispondono ai campi presenti nella struttura del modulo. Il passaggio successivo consiste nell&#39;assegnare valori di dati agli elementi XML, come mostrato nel seguente codice XML.

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

Ciascun sottogruppo di dati deve contenere elementi XML che corrispondono ai nomi dei campi nel sottomodulo. Il sottomodulo `detail` presente nella struttura del modulo contiene i campi seguenti:

* txtPartNum
* txtDescription
* numQty
* numUnitPrice

>[!NOTE]
>
>Se si tenta di precompilare un modulo con un’origine dati contenente elementi XML ripetuti e si imposta l’opzione `RenderAtClient` su `No`, nel modulo viene unito solo il primo record di dati. Per assicurarsi che tutti i record di dati siano uniti nel modulo, impostare `RenderAtClient` su `Yes`. Per informazioni sull&#39;opzione `RenderAtClient`, vedere [Rendering Forms sul client](/help/forms/developing/rendering-forms-client.md).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, consulta [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

È possibile utilizzare le classi `org.w3c.dom` per creare un&#39;origine dati XML in memoria per precompilare un modulo con un layout scorrevole. È necessario inserire i dati in un’origine dati XML conforme al modulo. Per informazioni sulla relazione tra un modulo con layout scorrevole e l&#39;origine dati XML, vedere [Informazioni sui sottogruppi di dati](#understanding-data-subgroups).

**Convertire l’origine dati XML**

Un’origine dati XML in memoria creata utilizzando le classi `org.w3c.dom` può essere convertita in un oggetto `com.adobe.idp.Document` prima di poter essere utilizzata per precompilare un modulo. Un’origine dati XML in memoria può essere convertita utilizzando le classi di trasformazione Java XML.

>[!NOTE]
>
>Se si utilizza il WSDL del servizio Forms per precompilare un modulo, è necessario convertire un oggetto `org.w3c.dom.Document` in un oggetto `BLOB`.

**Rendering di un modulo precompilato**

È possibile eseguire il rendering di un modulo precompilato come un altro modulo. L’unica differenza consiste nell’utilizzare l’oggetto `com.adobe.idp.Document` contenente l’origine dati XML per precompilare il modulo.

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendering di PDF forms interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Precompilazione dei moduli utilizzando l’API Java {#prepopulating-forms-using-the-java-api}

Per precompilare un modulo con un layout scorrevole utilizzando l’API Forms (Java), effettua le seguenti operazioni:

1. Includi file di progetto

   Includi file JAR client, come adobe-forms-client.jar, nel percorso di classe del progetto Java. Per informazioni sulla posizione di questi file, consulta [Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Creare un’origine dati XML in memoria

   * Crea un oggetto Java `DocumentBuilderFactory` chiamando il metodo `DocumentBuilderFactory` class’ `newInstance` .
   * Crea un oggetto Java `DocumentBuilder` chiamando il metodo `DocumentBuilderFactory` dell&#39;oggetto `newDocumentBuilder` .
   * Chiama il metodo `newDocument` dell&#39;oggetto `DocumentBuilder` per creare un&#39;istanza di un oggetto `org.w3c.dom.Document`.
   * Creare l’elemento principale dell’origine dati XML richiamando il metodo `createElement` dell’oggetto `org.w3c.dom.Document`. Questo crea un oggetto `Element` che rappresenta l&#39;elemento principale. Passa al metodo `createElement` un valore stringa che rappresenta il nome dell&#39;elemento. Imposta il valore restituito su `Element`. Quindi, aggiungi l’elemento principale al documento chiamando il metodo `appendChild` dell’oggetto `Document` e passa l’oggetto elemento principale come argomento. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * Creare l’elemento di intestazione dell’origine dati XML chiamando il metodo `Document` dell’oggetto `createElement` . Passa al metodo `createElement` un valore stringa che rappresenta il nome dell&#39;elemento. Imposta il valore restituito su `Element`. Quindi, aggiungi l’elemento header all’elemento root chiamando il metodo `appendChild` dell’oggetto `root` e passa l’oggetto header come argomento. Gli elementi XML aggiunti all’elemento header corrispondono alla parte statica del modulo. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * Crea un elemento figlio che appartiene all’elemento header chiamando il metodo `createElement` dell’oggetto `Document` e passa un valore stringa che rappresenta il nome dell’elemento. Imposta il valore restituito su `Element`. Quindi, imposta un valore per l’elemento figlio chiamandone il metodo `appendChild` e passa il metodo `Document` dell’oggetto `createTextNode` come argomento. Specifica un valore di stringa che viene visualizzato come valore dell&#39;elemento figlio. Infine, aggiungi l’elemento figlio all’elemento header chiamando il metodo `appendChild` dell’elemento header e passa l’oggetto element figlio come argomento. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`


   * Aggiungi tutti gli elementi rimanenti all&#39;elemento intestazione ripetendo l&#39;ultimo passaggio secondario per ciascun campo visualizzato nella parte statica del modulo (nel diagramma dell&#39;origine dati XML, questi campi sono visualizzati nella sezione A. (Vedere [Informazioni sui sottogruppi di dati](#understanding-data-subgroups)).
   * Creare l’elemento di dettaglio dell’origine dati XML chiamando il metodo `Document` dell’oggetto `createElement` . Passa al metodo `createElement` un valore stringa che rappresenta il nome dell&#39;elemento. Imposta il valore restituito su `Element`. Quindi, aggiungi l’elemento dettaglio all’elemento principale chiamando il metodo `appendChild` dell’oggetto `root` e passa l’oggetto elemento dettaglio come argomento. Gli elementi XML aggiunti all’elemento dettaglio corrispondono alla parte dinamica del modulo. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * Crea un elemento figlio che appartiene all’elemento dettaglio chiamando il metodo `createElement` dell’oggetto `Document` e passa un valore stringa che rappresenta il nome dell’elemento. Imposta il valore restituito su `Element`. Quindi, imposta un valore per l’elemento figlio chiamandone il metodo `appendChild` e passa il metodo `Document` dell’oggetto `createTextNode` come argomento. Specifica un valore di stringa che viene visualizzato come valore dell&#39;elemento figlio. Infine, aggiungi l’elemento figlio all’elemento dettaglio chiamando il metodo `appendChild` dell’elemento dettaglio e passa l’oggetto elemento figlio come argomento. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * Ripeti l’ultimo passaggio secondario affinché tutti gli elementi XML vengano aggiunti all’elemento dettaglio. Per creare correttamente l&#39;origine dati XML utilizzata per compilare il modulo dell&#39;ordine di acquisto, è necessario aggiungere i seguenti elementi XML all&#39;elemento dettaglio: `txtDescription`, `numQty` e `numUnitPrice`.
   * Ripetere gli ultimi due passaggi secondari per tutti gli elementi dati utilizzati per precompilare il modulo.

1. Convertire l’origine dati XML

   * Creare un oggetto `javax.xml.transform.Transformer` richiamando il metodo statico `javax.xml.transform.Transformer` dell&#39;oggetto `newInstance`.
   * Creare un oggetto `Transformer` richiamando il metodo `TransformerFactory` dell&#39;oggetto `newTransformer`.
   * Creare un oggetto `ByteArrayOutputStream` utilizzando il relativo costruttore.
   * Creare un oggetto `javax.xml.transform.dom.DOMSource` utilizzando il relativo costruttore e passando l&#39;oggetto `org.w3c.dom.Document` creato nel passaggio 1.
   * Creare un oggetto `javax.xml.transform.dom.DOMSource` utilizzando il relativo costruttore e passando l&#39;oggetto `ByteArrayOutputStream`.
   * Compilare l’oggetto Java `ByteArrayOutputStream` richiamando il metodo `javax.xml.transform.Transformer` dell’oggetto `transform` e passando gli oggetti `javax.xml.transform.dom.DOMSource` e `javax.xml.transform.stream.StreamResult`.
   * Creare una matrice di byte e allocare la dimensione dell&#39;oggetto `ByteArrayOutputStream` all&#39;array di byte.
   * Compilare la matrice dei byte richiamando il metodo `toByteArray` dell&#39;oggetto `ByteArrayOutputStream`.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando la matrice dei byte.

1. Rendering di un modulo precompilato

   Richiama il metodo `renderPDFForm` dell&#39;oggetto `FormsServiceClient` e passa i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file.
   * Un oggetto `com.adobe.idp.Document` contenente i dati da unire al modulo. Assicurati di utilizzare l&#39;oggetto `com.adobe.idp.Document` creato nei passaggi uno e due.
   * Un oggetto `PDFFormRenderSpec` che memorizza le opzioni di esecuzione.
   * Un oggetto `URLSpec` contenente valori URI richiesti dal servizio Forms.
   * Un oggetto `java.util.HashMap` che memorizza gli allegati di file. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.

   Il metodo `renderPDFForm` restituisce un oggetto `FormsResult` contenente un flusso di dati del modulo che deve essere scritto nel browser Web client.

   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per inviare un flusso di dati del modulo al browser Web client.
   * Creare un oggetto `com.adobe.idp.Document` richiamando il metodo `FormsResult` object ‘s `getOutputContent` .
   * Creare un oggetto `java.io.InputStream` richiamando il metodo `com.adobe.idp.Document` dell&#39;oggetto `getInputStream`.
   * Creare un array di byte popolarlo con il flusso di dati del modulo richiamando il metodo `read` dell&#39;oggetto `InputStream` e passando l&#39;array di byte come argomento.
   * Richiamare il metodo `write` dell’oggetto `javax.servlet.ServletOutputStream` per inviare il flusso di dati del modulo al browser Web client. Passa l&#39;array di byte al metodo `write` .


**Consulta anche**

[Avvio rapido (modalità SOAP): Precompilazione di Forms con layout fluidi tramite l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Precompilazione dei moduli tramite l’API del servizio Web {#prepopulating-forms-using-the-web-service-api}

Per precompilare un modulo con un layout scorrevole utilizzando l’API Forms (servizio Web), esegui le seguenti operazioni:

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio WSDL di Forms. (Consulta [Creazione di classi proxy Java tramite Apache Axis](/help/forms/developing/invoking-aem-forms-using-web.md#creating-java-proxy-classes-using-apache-axis).)
   * Includi le classi proxy Java nel percorso della classe.

1. Creare un’origine dati XML in memoria

   * Crea un oggetto Java `DocumentBuilderFactory` chiamando il metodo `DocumentBuilderFactory` class’ `newInstance` .
   * Crea un oggetto Java `DocumentBuilder` chiamando il metodo `DocumentBuilderFactory` dell&#39;oggetto `newDocumentBuilder` .
   * Chiama il metodo `newDocument` dell&#39;oggetto `DocumentBuilder` per creare un&#39;istanza di un oggetto `org.w3c.dom.Document`.
   * Creare l’elemento principale dell’origine dati XML richiamando il metodo `createElement` dell’oggetto `org.w3c.dom.Document`. Questo crea un oggetto `Element` che rappresenta l&#39;elemento principale. Passa al metodo `createElement` un valore stringa che rappresenta il nome dell&#39;elemento. Imposta il valore restituito su `Element`. Quindi, aggiungi l’elemento principale al documento chiamando il metodo `appendChild` dell’oggetto `Document` e passa l’oggetto elemento principale come argomento. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * Creare l’elemento di intestazione dell’origine dati XML chiamando il metodo `Document` dell’oggetto `createElement` . Passa al metodo `createElement` un valore stringa che rappresenta il nome dell&#39;elemento. Imposta il valore restituito su `Element`. Quindi, aggiungi l’elemento header all’elemento root chiamando il metodo `appendChild` dell’oggetto `root` e passa l’oggetto header come argomento. Gli elementi XML aggiunti all’elemento header corrispondono alla parte statica del modulo. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * Crea un elemento figlio che appartiene all’elemento header chiamando il metodo `createElement` dell’oggetto `Document` e passa un valore stringa che rappresenta il nome dell’elemento. Imposta il valore restituito su `Element`. Quindi, imposta un valore per l’elemento figlio chiamandone il metodo `appendChild` e passa il metodo `Document` dell’oggetto `createTextNode` come argomento. Specifica un valore di stringa che viene visualizzato come valore dell&#39;elemento figlio. Infine, aggiungi l’elemento figlio all’elemento header chiamando il metodo `appendChild` dell’elemento header e passa l’oggetto element figlio come argomento. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`

   * Aggiungi tutti gli elementi rimanenti all&#39;elemento intestazione ripetendo l&#39;ultimo passaggio secondario per ciascun campo visualizzato nella parte statica del modulo (nel diagramma dell&#39;origine dati XML, questi campi sono visualizzati nella sezione A. (Vedere [Informazioni sui sottogruppi di dati](#understanding-data-subgroups)).
   * Creare l’elemento di dettaglio dell’origine dati XML chiamando il metodo `Document` dell’oggetto `createElement` . Passa al metodo `createElement` un valore stringa che rappresenta il nome dell&#39;elemento. Imposta il valore restituito su `Element`. Quindi, aggiungi l’elemento dettaglio all’elemento principale chiamando il metodo `appendChild` dell’oggetto `root` e passa l’oggetto elemento dettaglio come argomento. Gli elementi XML aggiunti all’elemento dettaglio corrispondono alla parte dinamica del modulo. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * Crea un elemento figlio che appartiene all’elemento dettaglio chiamando il metodo `createElement` dell’oggetto `Document` e passa un valore stringa che rappresenta il nome dell’elemento. Imposta il valore restituito su `Element`. Quindi, imposta un valore per l’elemento figlio chiamandone il metodo `appendChild` e passa il metodo `Document` dell’oggetto `createTextNode` come argomento. Specifica un valore di stringa che viene visualizzato come valore dell&#39;elemento figlio. Infine, aggiungi l’elemento figlio all’elemento dettaglio chiamando il metodo `appendChild` dell’elemento dettaglio e passa l’oggetto elemento figlio come argomento. Le seguenti righe di codice mostrano questa logica di applicazione:

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * Ripeti l’ultimo passaggio secondario affinché tutti gli elementi XML vengano aggiunti all’elemento dettaglio. Per creare correttamente l&#39;origine dati XML utilizzata per compilare il modulo dell&#39;ordine di acquisto, è necessario aggiungere i seguenti elementi XML all&#39;elemento dettaglio: `txtDescription`, `numQty` e `numUnitPrice`.
   * Ripetere gli ultimi due passaggi secondari per tutti gli elementi dati utilizzati per precompilare il modulo.

1. Convertire l’origine dati XML

   * Creare un oggetto `javax.xml.transform.Transformer` richiamando il metodo statico `javax.xml.transform.Transformer` dell&#39;oggetto `newInstance`.
   * Creare un oggetto `Transformer` richiamando il metodo `TransformerFactory` dell&#39;oggetto `newTransformer`.
   * Creare un oggetto `ByteArrayOutputStream` utilizzando il relativo costruttore.
   * Creare un oggetto `javax.xml.transform.dom.DOMSource` utilizzando il relativo costruttore e passando l&#39;oggetto `org.w3c.dom.Document` creato nel passaggio 1.
   * Creare un oggetto `javax.xml.transform.dom.DOMSource` utilizzando il relativo costruttore e passando l&#39;oggetto `ByteArrayOutputStream`.
   * Compilare l’oggetto Java `ByteArrayOutputStream` richiamando il metodo `javax.xml.transform.Transformer` dell’oggetto `transform` e passando gli oggetti `javax.xml.transform.dom.DOMSource` e `javax.xml.transform.stream.StreamResult`.
   * Creare una matrice di byte e allocare la dimensione dell&#39;oggetto `ByteArrayOutputStream` all&#39;array di byte.
   * Compilare la matrice dei byte richiamando il metodo `toByteArray` dell&#39;oggetto `ByteArrayOutputStream`.
   * Creare un oggetto `BLOB` utilizzando il relativo costruttore, richiamare il relativo metodo `setBinaryData` e passare l&#39;array di byte.

1. Rendering di un modulo precompilato

   Richiama il metodo `renderPDFForm` dell&#39;oggetto `FormsService` e passa i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file.
   * Un oggetto `BLOB` contenente i dati da unire al modulo. Assicurati di utilizzare l&#39;oggetto `BLOB` creato nei passaggi uno e due.
   * Un oggetto `PDFFormRenderSpecc` che memorizza le opzioni di esecuzione. Per ulteriori informazioni, consulta [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Un oggetto `URLSpec` contenente valori URI richiesti dal servizio Forms.
   * Un oggetto `java.util.HashMap` che memorizza gli allegati di file. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.
   * Un oggetto `com.adobe.idp.services.holders.BLOBHolder` vuoto compilato dal metodo . Viene utilizzato per memorizzare il modulo PDF di cui è stato effettuato il rendering.
   * Un oggetto `javax.xml.rpc.holders.LongHolder` vuoto compilato dal metodo . Questo argomento memorizza il numero di pagine nel modulo.
   * Un oggetto `javax.xml.rpc.holders.StringHolder` vuoto compilato dal metodo . (Questo argomento memorizza il valore delle impostazioni internazionali).
   * Un oggetto `com.adobe.idp.services.holders.FormsResultHolder` vuoto che conterrà i risultati dell&#39;operazione.

   Il metodo `renderPDFForm` popola l&#39;oggetto `com.adobe.idp.services.holders.FormsResultHolder` passato come ultimo valore dell&#39;argomento con un flusso di dati del modulo che deve essere scritto nel browser Web client.

   * Creare un oggetto `FormResult` ottenendo il valore del membro dati `com.adobe.idp.services.holders.FormsResultHolder` dell&#39;oggetto `value`.
   * Creare un oggetto `BLOB` che contiene dati del modulo richiamando il metodo `FormsResult` dell&#39;oggetto `getOutputContent`.
   * Ottenere il tipo di contenuto dell&#39;oggetto `BLOB` richiamandone il metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamandone il metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `BLOB`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il metodo `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream`.
   * Creare una matrice di byte e compilarla richiamando il metodo `getBinaryData` dell&#39;oggetto `BLOB`. Questa attività assegna il contenuto dell&#39;oggetto `FormsResult` all&#39;array di byte.
   * Richiamare il metodo `write` dell’oggetto `javax.servlet.http.HttpServletResponse` per inviare il flusso di dati del modulo al browser Web client. Passa l&#39;array di byte al metodo `write` .

   >[!NOTE]
   >
   >Il metodo `renderPDFForm` popola l&#39;oggetto `com.adobe.idp.services.holders.FormsResultHolder` passato come ultimo valore dell&#39;argomento con un flusso di dati del modulo che deve essere scritto nel browser Web client.

**Consulta anche**

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

