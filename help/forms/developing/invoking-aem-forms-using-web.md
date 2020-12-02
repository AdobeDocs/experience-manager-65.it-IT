---
title: Chiamata  AEM Forms tramite servizi Web
seo-title: Chiamata  AEM Forms tramite servizi Web
description: 'null'
seo-description: 'null'
uuid: 66bcd010-c476-4b66-831d-a48307d8d67a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: d5722281-bea9-4fc7-abdc-e678899e0a15
translation-type: tm+mt
source-git-commit: e5c2385c29e2d20d453e2d1496f7d459d1c55876
workflow-type: tm+mt
source-wordcount: '9966'
ht-degree: 0%

---


# Chiamata  AEM Forms tramite servizi Web {#invoking-aem-forms-using-web-services}

La maggior parte  servizi AEM Forms nel contenitore di servizi sono configurati per esporre un servizio Web, con il supporto completo per la generazione del linguaggio WSDL (Web Service Definition Language). In altre parole, potete creare oggetti proxy che utilizzano lo stack SOAP nativo di un servizio AEM Forms . Di conseguenza,  servizi AEM Forms possono scambiare ed elaborare i seguenti messaggi SOAP:

* **Richiesta** SOAP: Inviato a un servizio Forms da un&#39;applicazione client che richiede un&#39;azione.
* **Risposta** SOAP: Inviato a un&#39;applicazione client da un servizio Forms dopo l&#39;elaborazione di una richiesta SOAP.

I servizi Web consentono di eseguire le stesse operazioni  servizi AEM Forms che è possibile utilizzare l&#39;API Java. L&#39;utilizzo di servizi Web per richiamare  servizi AEM Forms consente di creare un&#39;applicazione client in un ambiente di sviluppo che supporta SOAP. Un&#39;applicazione client non è associata a un ambiente di sviluppo o a un linguaggio di programmazione specifico. Ad esempio, è possibile creare un&#39;applicazione client utilizzando Microsoft Visual Studio .NET e C# come linguaggio di programmazione.

 servizi AEM Forms sono esposti attraverso il protocollo SOAP e sono conformi al profilo di base WSI 1.1. Web Services Interoperability (WSI) è un&#39;organizzazione standard aperta che promuove l&#39;interoperabilità dei servizi Web tra piattaforme. Per informazioni, vedere [https://www.ws-i.org/](https://www.ws-i.org).

 AEM Forms supporta i seguenti standard di servizi Web:

* **Codifica**: Supporta solo la codifica documentale e letterale (che è la codifica preferita in base al profilo di base WSI). (Vedere [Richiamo  AEM Forms con codifica Base64](#invoking-aem-forms-using-base64-encoding).)
* **MTOM**: Rappresenta un modo per codificare gli allegati con le richieste SOAP. (Vedere [Chiamata  AEM Forms tramite MTOM](#invoking-aem-forms-using-mtom).)
* **SwaRef**: Rappresenta un altro modo per codificare gli allegati con le richieste SOAP. (Vedere [Chiamata  AEM Forms tramite SwaRef](#invoking-aem-forms-using-swaref).)
* **SOAP con allegati**: Supporta sia MIME che DIME (Direct Internet Message Encapsulation). Questi protocolli sono metodi standard per inviare allegati via SOAP. Le applicazioni Microsoft Visual Studio .NET utilizzano DIME. (Vedere [Richiamo  AEM Forms con codifica Base64](#invoking-aem-forms-using-base64-encoding).)
* **WS-Security**: Supporta un profilo token password di nome utente, che è un modo standard di inviare nomi utente e password come parte dell&#39;intestazione SOAP di WS Security.  AEM Forms supporta anche l&#39;autenticazione di base HTTP. (Vedere [Trasmissione delle credenziali tramite WS-Security header](https://www.adobe.com/devnet/livecycle/articles/passing_credentials.html).)

Per richiamare  servizi AEM Forms utilizzando un servizio Web, in genere si crea una libreria proxy che utilizza il servizio WSDL. La sezione *Richiamo  AEM Forms tramite Web Services* utilizza JAX-WS per creare classi proxy Java per richiamare i servizi. (Vedere [Creazione di classi proxy Java tramite JAX-WS](#creating-java-proxy-classes-using-jax-ws).)

Potete recuperare un servizio WDSL specificando la seguente definizione URL (gli elementi tra parentesi sono facoltativi):

```java
 https://<your_serverhost>:<your_port>/soap/services/<service_name>?wsdl[&version=<version>][&async=true|false][lc_version=<lc_version>]
```

dove:

* *your_* serverhostrema l&#39;indirizzo IP del server applicazione J2EE che ospita  AEM Forms.
* *your_* portrappresenta la porta HTTP utilizzata dal server applicazione J2EE.
* *service_* namerepresenta il nome del servizio.
* *La* versione rappresenta la versione di destinazione di un servizio (per impostazione predefinita viene utilizzata la versione più recente del servizio).
* `async` specifica il valore  `true` per abilitare ulteriori operazioni di chiamata asincrona ( `false` per impostazione predefinita).
* *lc_* versionrappresenta la versione di  AEM Forms che si desidera richiamare.

Nella tabella seguente sono elencate le definizioni WSDL del servizio (supponendo che  AEM Forms sia distribuito sull&#39;host locale e che il post sia 8080).

<table>
 <thead>
  <tr>
   <th><p>Servizio</p></th>
   <th><p>Definizione WSDL</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Assemblatore</p></td>
   <td><p><code>http://localhost:8080/soap/services/ AssemblerService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Indietro e ripristinare</p></td>
   <td><p><code>http://localhost:8080/soap/services/BackupService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Barcoded Forms</p></td>
   <td><p><code>http://localhost:8080/soap/services/ BarcodedFormsService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Converti PDF</p></td>
   <td><p><code>http://localhost:8080/soap/services/ ConvertPDFService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Distiller</p></td>
   <td><p><code>http://localhost:8080/soap/services/ DistillerService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>DocConverter </p></td>
   <td><p><code>http://localhost:8080/soap/services/DocConverterService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>DocumentManagement</p></td>
   <td><p><code>http://localhost:8080/soap/services/DocumentManagementService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>Cifratura </p></td>
   <td><p><code>http://localhost:8080/soap/services/EncryptionService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Forms</p></td>
   <td><p><code>http://localhost:8080/soap/services/FormsService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Integrazione dei dati del modulo</p></td>
   <td><p><code>http://localhost:8080/soap/services/FormDataIntegration?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Genera PDF</p></td>
   <td><p><code>http://localhost:8080/soap/services/ GeneratePDFService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Genera PDF 3D</p></td>
   <td><p><code>http://localhost:8080/soap/services/Generate3dPDFService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>Output</p></td>
   <td><p><code>http://localhost:8080/soap/services/ OutputService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Utilità PDF </p></td>
   <td><p><code>http://localhost:8080/soap/services/ PDFUtilityService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Estensioni Acrobat Reader DC</p></td>
   <td><p><code>http://localhost:8080/soap/services/ ReaderExtensionsService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Archivio</p></td>
   <td><p><code>http://localhost:8080/soap/services/ RepositoryService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Rights Management </p></td>
   <td><p><code>http://localhost:8080/soap/services/ RightsManagementService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Firma </p></td>
   <td><p><code>http://localhost:8080/soap/services/ SignatureService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Utilità XMP</p></td>
   <td><p><code>http://localhost:8080/soap/services/ XMPUtilityService?wsdl</code></p></td>
  </tr>
 </tbody>
</table>

**definizioni WSDL di AEM Forms Process**

È necessario specificare il nome dell&#39;applicazione e il nome del processo all&#39;interno della definizione WSDL per accedere a un WSDL appartenente a un processo creato in Workbench. Si supponga che il nome dell&#39;applicazione sia `MyApplication` e che il nome del processo sia `EncryptDocument`. In questa situazione, specificare la seguente definizione WSDL:

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl
```

>[!NOTE]
>
>Per informazioni sull&#39;esempio `MyApplication/EncryptDocument` processo di breve durata, vedere [Esempio di processo di breve durata](/help/forms/developing/aem-forms-processes.md).

>[!NOTE]
>
>Un&#39;applicazione può contenere cartelle. In questo caso, specificate i nomi delle cartelle nella definizione WSDL:

```java
 http://localhost:8080/soap/services/MyApplication/[<folderA>/.../<folderZ>/]EncryptDocument?wsdl
```

**Accesso a nuove funzionalità tramite i servizi Web**

È possibile accedere  nuova funzionalità del servizio AEM Forms tramite i servizi Web. Ad esempio, in  AEM Forms viene introdotta la possibilità di codificare gli allegati utilizzando MTOM. (Vedere [Chiamata  AEM Forms tramite MTOM](#invoking-aem-forms-using-mtom).)

Per accedere alle nuove funzionalità introdotte in  AEM Forms, specificate l&#39;attributo `lc_version` nella definizione WSDL. Ad esempio, per accedere alle nuove funzionalità del servizio (incluso il supporto MTOM), specificate la seguente definizione WSDL:

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl&lc_version=9.0.1
```

>[!NOTE]
>
>Quando si imposta l&#39;attributo `lc_version`, assicurarsi di utilizzare tre cifre. Ad esempio, 9.0.1 è uguale alla versione 9.0.

**Tipo di dati BLOB del servizio Web**

 WSDL del servizio AEM Forms definiscono molti tipi di dati. Uno dei tipi di dati più importanti esposti in un servizio Web è un tipo `BLOB`. Questo tipo di dati viene mappato sulla classe `com.adobe.idp.Document` quando si utilizzano  API Java AEM Forms. (Vedere [Trasmissione di dati a  servizi AEM Forms tramite Java API](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api).)

Un oggetto `BLOB` invia e recupera dati binari (ad esempio, file PDF, dati XML e così via) da e verso  servizi AEM Forms. Il tipo `BLOB` è definito in un servizio WSDL come segue:

```xml
 <complexType name="BLOB">
     <sequence>
         <element maxOccurs="1" minOccurs="0" name="contentType"
             type="xsd:string"/>
         <element maxOccurs="1" minOccurs="0" name="binaryData"
             type="xsd:base64Binary"/>
         <element maxOccurs="1" minOccurs="0" name="attachmentID"
             type="xsd:string"/>
         <element maxOccurs="1" minOccurs="0" name="remoteURL"
             type="xsd:string"/>
         <element maxOccurs="1" minOccurs="0" name="MTOM"
             type="xsd:base64Binary"
             xmime:expectedContentTypes="*/*"
             xmlns:xmime="https://www.w3.org/2005/05/xmlmime"/>
         <element maxOccurs="1" minOccurs="0" name="swaRef"
             type="tns1:swaRef"/>
         <element maxOccurs="1" minOccurs="0" name="attributes"
             type="impl:MyMapOf_xsd_string_To_xsd_anyType"/>
     </sequence>
 </complexType>
```

I campi `MTOM` e `swaRef` sono supportati solo in  AEM Forms. Potete utilizzare questi nuovi campi solo se specificate un URL che include la proprietà `lc_version`.

**Fornitura di oggetti BLOB nelle richieste di servizio**

Se un&#39;operazione del servizio AEM Forms  richiede un tipo `BLOB` come valore di input, creare un&#39;istanza del tipo `BLOB` nella logica dell&#39;applicazione. (Molti degli avvii rapidi del servizio Web che si trovano in *Programmazione con moduli AEM* mostrano come utilizzare un tipo di dati BLOB.)

Assegnare valori ai campi che appartengono all&#39;istanza `BLOB` come segue:

* **Base64**: Per trasmettere dati come testo codificato in formato Base64, impostare i dati nel  `BLOB.binaryData` campo e impostare il tipo di dati nel formato MIME (ad esempio  `application/pdf`) del  `BLOB.contentType` campo. (Vedere [Richiamo  AEM Forms con codifica Base64](#invoking-aem-forms-using-base64-encoding).)
* **MTOM**: Per trasmettere dati binari in un allegato MTOM, impostare i dati nel  `BLOB.MTOM` campo. Questa impostazione associa i dati alla richiesta SOAP utilizzando il framework Java JAX-WS o l&#39;API nativa del framework SOAP. (Vedere [Chiamata  AEM Forms tramite MTOM](#invoking-aem-forms-using-mtom).)
* **SwaRef**: Per trasmettere dati binari in un allegato SwaRef WS-I, impostare i dati nel  `BLOB.swaRef` campo. Questa impostazione allega i dati alla richiesta SOAP utilizzando il framework Java JAX-WS. (Vedere [Chiamata  AEM Forms tramite SwaRef](#invoking-aem-forms-using-swaref).)
* **Allegato** MIME o DIME: Per trasmettere i dati in un allegato MIME o DIME, allegare i dati alla richiesta SOAP utilizzando l&#39;API nativa del framework SOAP. Impostare l&#39;identificatore allegato nel campo `BLOB.attachmentID`. (Vedere [Richiamo  AEM Forms con codifica Base64](#invoking-aem-forms-using-base64-encoding).)
* **URL** remoto: Se i dati sono in hosting su un server Web e sono accessibili tramite un URL HTTP, impostate l’URL HTTP nel  `BLOB.remoteURL` campo. (Vedere [Chiamata  AEM Forms tramite dati BLOB su HTTP](#invoking-aem-forms-using-blob-data-over-http).)

**Accesso ai dati in oggetti BLOB restituiti dai servizi**

Il protocollo di trasmissione per gli oggetti restituiti `BLOB` dipende da diversi fattori, considerati nell&#39;ordine seguente, che si arrestano quando la condizione principale è soddisfatta:

1. **L&#39;URL di destinazione specifica il protocollo** di trasmissione. Se l&#39;URL di destinazione specificato alla chiamata SOAP contiene il parametro `blob="`*BLOB_TYPE*&quot;, il protocollo di trasmissione è determinato da *BLOB_TYPE*. *BLOB_* TYPE è un segnaposto per base64, dime, mime, http, mtom o swaref.
1. **L&#39;endpoint SOAP del servizio è Smart**. Se le seguenti condizioni sono vere, i documenti di output vengono restituiti utilizzando lo stesso protocollo di trasmissione dei documenti di input:

   * Il protocollo predefinito del parametro endpoint SOAP del servizio per gli oggetti BLOB di output è impostato su Smart.

      Per ogni servizio con un endpoint SOAP, la console di amministrazione consente di specificare il protocollo di trasmissione per tutti i BLOB restituiti. (Vedere [guida di amministrazione](https://www.adobe.com/go/learn_aemforms_admin_63).)

   *  servizio AEM Forms accetta uno o più documenti come input.

1. **L&#39;endpoint SOAP del servizio non è Smart**. Il protocollo configurato determina il protocollo di trasmissione del documento e i dati vengono restituiti nel campo `BLOB` corrispondente. Ad esempio, se l&#39;endpoint SOAP è impostato su DIME, il BLOB restituito si trova nel campo `blob.attachmentID` indipendentemente dal protocollo di trasmissione di qualsiasi documento di input.
1. **In caso contrario**. Se un servizio non accetta il tipo di documento come input, i documenti di output vengono restituiti nel campo `BLOB.remoteURL` attraverso il protocollo HTTP.

Come descritto nella prima condizione, potete garantire il tipo di trasmissione per tutti i documenti restituiti estendendo l&#39;URL dell&#39;endpoint SOAP con un suffisso come segue:

```java
     https://<your_serverhost>:<your_port>/soap/services/<service
     name>?blob=base64|dime|mime|http|mtom|swaref
```

Di seguito è riportata la correlazione tra i tipi di trasmissione e il campo da cui si ottengono i dati:

* **Formato** Base64: Impostate il  `blob` suffisso  `base64` per restituire i dati nel  `BLOB.binaryData` campo.
* **Allegato** MIME o DIME: Impostare il  `blob` suffisso su  `DIME` o  `MIME` per restituire i dati come tipo di allegato corrispondente con l&#39;identificatore di allegato restituito nel  `BLOB.attachmentID` campo. Utilizzare l&#39;API proprietaria del framework SOAP per leggere i dati dall&#39;allegato.
* **URL** remoto: Impostate il  `blob` suffisso  `http` per mantenere i dati sul server dell’applicazione e restituire l’URL che punta ai dati nel  `BLOB.remoteURL` campo.
* **MTOM o SwaRef**: Impostare il  `blob` suffisso su  `mtom` o  `swaref` per restituire i dati come tipo di allegato corrispondente con l&#39;identificatore di allegato restituito nei  `BLOB.MTOM` campi o  `BLOB.swaRef` nei campi. Utilizzare l&#39;API nativa del framework SOAP per leggere i dati dall&#39;allegato.

>[!NOTE]
>
>È consigliabile non superare i 30 MB quando si compila un oggetto `BLOB` richiamandone il metodo `setBinaryData`. In caso contrario, esiste la possibilità che si verifichi un&#39;eccezione `OutOfMemory`.

>[!NOTE]
>
>Le applicazioni basate su JAX WS che utilizzano il protocollo di trasmissione MTOM sono limitate a 25 MB di dati inviati e ricevuti. Questa limitazione è dovuta a un bug in JAX-WS. Se la dimensione combinata dei file inviati e ricevuti supera i 25 MB, utilizzate il protocollo di trasmissione SwaRef invece di quello MTOM. In caso contrario, esiste la possibilità di un&#39;eccezione `OutOfMemory`.

**Trasmissione MTOM di array di byte con codifica base64**

Oltre all&#39;oggetto `BLOB`, il protocollo MTOM supporta qualsiasi parametro di matrice di byte o campo di matrice di byte di un tipo complesso. Ciò significa che i framework SOAP client che supportano MTOM possono inviare qualsiasi elemento `xsd:base64Binary` come allegato MTOM (invece di un testo con codifica base64).  endpoint SOAP AEM Forms è in grado di leggere questo tipo di codifica matrice byte. Tuttavia, il servizio AEM Forms  restituisce sempre un tipo di array di byte come testo con codifica base64. I parametri dell&#39;array di byte di output non supportano MTOM.

 servizi AEM Forms che restituiscono una grande quantità di dati binari utilizzano il tipo Document/BLOB anziché il tipo di matrice byte. Il tipo di documento è molto più efficiente per la trasmissione di grandi quantità di dati.

## Tipi di dati del servizio Web {#web-service-data-types}

La tabella seguente elenca i tipi di dati Java e mostra il tipo di dati del servizio Web corrispondente.

<table>
 <thead>
  <tr>
   <th><p>Tipo di dati Java</p></th>
   <th><p>Tipo di dati del servizio Web</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>java.lang.byte[]</code></p></td>
   <td><p><code>xsd:base64Binary</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Boolean</code></p></td>
   <td><p><code>xsd:boolean</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Date</code></p></td>
   <td><p>Il tipo <code>DATE</code>, definito in un WSDL di servizio come segue:</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>Se un'operazione  servizio AEM Forms richiede un valore <code>java.util.Date</code> come input, l'applicazione client SOAP deve passare la data nel campo <code>DATE.date</code>. L'impostazione del campo <code>DATE.calendar</code> in questo caso causa un'eccezione di runtime. Se il servizio restituisce un valore <code>java.util.Date</code>, la data viene restituita nel campo <code>DATE.date</code>.</p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Calendar</code></p></td>
   <td><p>Il tipo <code>DATE</code>, definito in un WSDL di servizio come segue:</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>Se un'operazione  servizio AEM Forms richiede un valore <code>java.util.Calendar</code> come input, l'applicazione client SOAP deve passare la data nel campo <code>DATE.caledendar</code>. L'impostazione del campo <code>DATE.date</code> in questo caso causa un'eccezione di runtime. Se il servizio restituisce un valore <code>java.util.Calendar</code>, la data viene restituita nel campo <code>DATE.calendar</code>. </p></td>
  </tr>
  <tr>
   <td><p><code>java.math.BigDecimal</code></p></td>
   <td><p><code>xsd:decimal</code></p></td>
  </tr>
  <tr>
   <td><p><code>com.adobe.idp.Document</code></p></td>
   <td><p><code>BLOB</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Double</code></p></td>
   <td><p><code>xsd:double</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Float</code></p></td>
   <td><p><code>xsd:float</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Integer</code></p></td>
   <td><p><code>xsd:int</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.util.List</code></p></td>
   <td><p><code>MyArrayOf_xsd_anyType</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Long</code></p></td>
   <td><p><code>xsd:long</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Map</code></p></td>
   <td><p><code>apachesoap:Map</code>, definito in un servizio WSDL come segue:</p><p><code>&lt;schema elementFormDefault="qualified" targetNamespace="https://xml.apache.org/xml-soap" xmlns="https://www.w3.org/2001/XMLSchema"&gt;</code></p><p><code>&lt;complexType name="mapItem"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element name="key" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;element name="value" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;complexType name="Map"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="unbounded" minOccurs="0" name="item" </code><code>type="apachesoap:mapItem"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;/schema&gt;</code></p><p>La mappa è rappresentata come una sequenza di coppie chiave/valore.</p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Object</code></p></td>
   <td><p><code>$1</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Short</code></p></td>
   <td><p><code>xsd:short</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.String</code></p></td>
   <td><p><code>xsd:string</code></p></td>
  </tr>
  <tr>
   <td><p><code>org.w3c.dom.Document</code></p></td>
   <td><p>Il tipo XML, definito in un servizio WSDL come segue:</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>Se un'operazione del servizio AEM Forms  accetta un valore <code>org.w3c.dom.Document</code>, trasmettere i dati XML nel campo <code>XML.document</code>.</p><p>L'impostazione del campo <code>XML.element</code> causa un'eccezione di runtime. Se il servizio restituisce un elemento <code>org.w3c.dom.Document</code>, i dati XML vengono restituiti nel campo <code>XML.document</code>.</p></td>
  </tr>
  <tr>
   <td><p><code>org.w3c.dom.Element</code></p></td>
   <td><p>Il tipo XML, definito in un servizio WSDL come segue:</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>Se un'operazione del servizio AEM Forms  richiede un <code>org.w3c.dom.Element</code> come input, trasmettere i dati XML nel campo <code>XML.element</code>.</p><p>L'impostazione del campo <code>XML.document</code> causa un'eccezione di runtime. Se il servizio restituisce un elemento <code>org.w3c.dom.Element</code>, i dati XML vengono restituiti nel campo <code>XML.element</code>.</p></td>
  </tr>
 </tbody>
</table>

**Sito Web  Adobe per sviluppatori**

Il sito Web  Adobe Developer contiene il seguente articolo che descrive come richiamare  servizi AEM Forms mediante l&#39;API del servizio Web:

[Creazione di applicazioni ASP.NET per il rendering dei moduli](https://www.adobe.com/devnet/livecycle/articles/asp_net.html)

[Chiamata di servizi Web mediante componenti personalizzati](https://www.adobe.com/devnet/livecycle/articles/extend_webservices.html)

>[!NOTE]
>
>L&#39;invocazione di servizi Web tramite componenti personalizzati descrive come creare un componente AEM Forms  che richiama servizi Web di terze parti.

## Creazione di classi proxy Java tramite JAX-WS {#creating-java-proxy-classes-using-jax-ws}

È possibile utilizzare JAX-WS per convertire un WSDL del servizio Forms in classi proxy Java. Queste classi consentono di richiamare  operazioni dei servizi AEM Forms. Apache Ant consente di creare uno script di compilazione che genera classi proxy Java facendo riferimento a un WSDL  servizio AEM Forms. È possibile generare file proxy JAX-WS eseguendo i passaggi seguenti:

1. Installate Apache Ant sul computer client. (Vedere [https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi).)

   * Aggiungete la directory bin al percorso della classe.
   * Impostate la variabile di ambiente `ANT_HOME` sulla directory in cui avete installato Ant.

1. Installate JDK 1.6 o versione successiva.

   * Aggiungete la directory bin JDK al percorso della classe.
   * Aggiungete la directory JRE bin al percorso della classe. Questo bin si trova nella directory `[JDK_INSTALL_LOCATION]/jre`.
   * Impostate la variabile di ambiente `JAVA_HOME` sulla directory in cui avete installato il JDK.

   JDK 1.6 include il programma wsimport utilizzato nel file build.xml. JDK 1.5 non include tale programma.

1. Installare JAX-WS sul computer client. (Vedere [Java API for XML Web Services](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html).)
1. Utilizzate JAX-WS e Apache Ant per generare classi proxy Java. Creare uno script di creazione Ant per eseguire questa operazione. Lo script seguente è un esempio di script Ant build denominato build.xml:

   ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    
    <project basedir="." default="compile">
    
    <property name="port" value="8080" />
    <property name="host" value="localhost" />
    <property name="username" value="administrator" />
    <property name="password" value="password" />
    <property name="tests" value="all" />
    
    <target name="clean" >
           <delete dir="classes" />
    </target>
    
    <target name="wsdl" depends="clean">
           <mkdir dir="classes"/>
           <exec executable="wsimport" failifexecutionfails="false" failonerror="true" resultproperty="foundWSIMPORT">
               <arg line="-keep -d classes https://${host}:${port}/soap/services/EncryptionService?wsdl&lc_version=9.0.1"/>
           </exec>
           <fail unless="foundWSIMPORT">
              !!! Failed to execute JDK's wsimport tool. Make sure that JDK 1.6 (or later) is on your PATH !!!
           </fail>
    </target>
    
    <target name="compile" depends="clean, wsdl" >
         <javac destdir="./classes" fork="true" debug="true">
            <src path="./src"/>
         </javac>
    </target>
    
    <target name="run">
         <java classname="Client" fork="yes" failonerror="true" maxmemory="200M">
            <classpath>
              <pathelement location="./classes"/>
            </classpath>
            <arg value="${port}"/>
            <arg value="${host}"/>
            <arg value="${username}"/>
            <arg value="${password}"/>
            <arg value="${tests}"/>
         </java>
    </target>
    </project>
   ```

   All&#39;interno di questo script di creazione Ant, si noti che la proprietà `url` è impostata per fare riferimento al WSDL del servizio di cifratura in esecuzione su localhost. Le proprietà `username` e `password` devono essere impostate su un nome utente e una password validi per i moduli AEM. L&#39;URL contiene l&#39;attributo `lc_version`. Senza specificare l&#39;opzione `lc_version`, non è possibile richiamare nuove operazioni  servizio AEM Forms.

   >[!NOTE]
   >
   >Sostituire `EncryptionService`con il nome  del servizio AEM Forms che si desidera richiamare utilizzando le classi proxy Java. Ad esempio, per creare classi proxy Java per il servizio di Rights Management, specificate:

   ```java
    http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1
   ```

1. Creare un file BAT per eseguire lo script di creazione Ant. È possibile individuare il seguente comando all&#39;interno di un file BAT che è responsabile dell&#39;esecuzione dello script di compilazione Ant:

   ```java
    ant -buildfile "build.xml" wsdl
   ```

   Posizionare lo script di compilazione ANT nella cartella C:\Program Files\Java\jaxws-ri\bin directory. Lo script scrive i file JAVA in ./class. Lo script genera file JAVA in grado di richiamare il servizio.

1. Creare pacchetti di file JAVA in un file JAR. Se state lavorando su Eclipse, effettuate le seguenti operazioni:

   * Create un nuovo progetto Java utilizzato per creare il pacchetto dei file JAVA proxy in un file JAR.
   * Create una cartella sorgente nel progetto.
   * Create un pacchetto `com.adobe.idp.services` nella cartella Source (Origine).
   * Selezionate il pacchetto `com.adobe.idp.services`, quindi importate i file JAVA dalla cartella adobe/idp/services nel pacchetto.
   * Se necessario, create un pacchetto `org/apache/xml/xmlsoap` nella cartella Source.
   * Selezionate la cartella di origine e importate i file JAVA dalla cartella org/apache/xml/xmlsoap.
   * Impostate il livello di conformità del compilatore Java su 5.0 o superiore.
   * Create il progetto.
   * Esportate il progetto come file JAR.
   * Importa questo file JAR nel percorso di classe di un progetto client. Inoltre, importate tutti i file JAR che si trovano in &lt;Directory di installazione>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty.

   >[!NOTE]
   >
   >Tutti i servizi Web Java avviano rapidamente (ad eccezione del servizio Forms) che si trova in Programmazione con moduli AEM creare file proxy Java utilizzando JAX-WS. Inoltre, tutti i servizi Web Java si avviano rapidamente, utilizza SwaRef. (Vedere [Chiamata  AEM Forms tramite SwaRef](#invoking-aem-forms-using-swaref).)

**Consulta anche**

[Creazione di classi proxy Java tramite Apache Axis](#creating-java-proxy-classes-using-apache-axis)

[Richiamo  AEM Forms con codifica Base64](#invoking-aem-forms-using-base64-encoding)

[Richiamo  AEM Forms utilizzando dati BLOB su HTTP](#invoking-aem-forms-using-blob-data-over-http)

[Chiamata  AEM Forms tramite SwaRef](#invoking-aem-forms-using-swaref)

## Creazione di classi proxy Java tramite Apache Axis {#creating-java-proxy-classes-using-apache-axis}

È possibile utilizzare lo strumento Apache Axis WSDL2Java per convertire un servizio Forms in classi proxy Java. Queste classi consentono di richiamare le operazioni del servizio Forms. Utilizzando Apache Ant, potete generare file libreria Axis da un servizio WSDL. Potete scaricare Apache Axis dall&#39;URL [https://ws.apache.org/axis/](https://ws.apache.org/axis/).

>[!NOTE]
>
>Gli avvii rapidi del servizio Web associati al servizio Forms utilizzano le classi proxy Java create utilizzando Apache Axis. Il servizio Web Forms avvia rapidamente l&#39;utilizzo di Base64 come tipo di codifica. (Vedere [Avvio rapido di Forms Service API](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts).)

È possibile generare file libreria Java Axis eseguendo i seguenti passaggi:

1. Installate Apache Ant sul computer client. È disponibile all&#39;indirizzo [https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi).

   * Aggiungete la directory bin al percorso della classe.
   * Impostate la variabile di ambiente `ANT_HOME` sulla directory in cui avete installato Ant.

1. Installate Apache Axis 1.4 nel computer client. È disponibile all&#39;indirizzo [https://ws.apache.org/axis/](https://ws.apache.org/axis/.md).
1. Configurate il percorso della classe per utilizzare i file JAR Axis nel client di servizi Web, come descritto nelle istruzioni di installazione Axis all&#39;indirizzo [https://ws.apache.org/axis/java/install.html](https://ws.apache.org/axis/java/install.html).
1. Utilizzate lo strumento Apache WSDL2Java in Axis per generare classi proxy Java. Creare uno script di creazione Ant per eseguire questa operazione. Lo script seguente è un esempio di script Ant build denominato build.xml:

   ```java
    <?xml version="1.0"?>
    <project name="axis-wsdl2java">
    
    <path id="axis.classpath">
    <fileset dir="C:\axis-1_4\lib" >
        <include name="**/*.jar" />
    </fileset>
    </path>
    
    <taskdef resource="axis-tasks.properties" classpathref="axis.classpath" />
    
    <target name="encryption-wsdl2java-client" description="task">
    <axis-wsdl2java
        output="C:\JavaFiles"
        testcase="false"
        serverside="false"
        verbose="true"
        username="administrator"
        password="password"
        url="http://localhost:8080/soap/services/EncryptionService?wsdl&lc_version=9.0.1" >
    </axis-wsdl2java>
    </target>
    
    </project>
   ```

   All&#39;interno di questo script di creazione Ant, si noti che la proprietà `url` è impostata per fare riferimento al WSDL del servizio di cifratura in esecuzione su localhost. Le proprietà `username` e `password` devono essere impostate su un nome utente e una password validi per i moduli AEM.

1. Creare un file BAT per eseguire lo script di creazione Ant. È possibile individuare il seguente comando all&#39;interno di un file BAT che è responsabile dell&#39;esecuzione dello script di compilazione Ant:

   ```java
    ant -buildfile "build.xml" encryption-wsdl2java-client
   ```

   I file JAVA vengono scritti nella proprietà C:\JavaFiles folder as specified by the `output`. Per richiamare il servizio Forms, importate questi file JAVA nel percorso della classe.

   Per impostazione predefinita, questi file appartengono a un pacchetto Java denominato `com.adobe.idp.services`. È consigliabile inserire questi file JAVA in un file JAR. Quindi importate il file JAR nel percorso di classe dell&#39;applicazione client.

   >[!NOTE]
   >
   >Ci sono diversi modi per inserire i file .JAVA in una JAR. Un modo è utilizzare un IDE Java come Eclipse. Create un progetto Java e create un pacchetto `com.adobe.idp.services`(tutti i file .JAVA appartengono a questo pacchetto). Quindi importate tutti i file .JAVA nel pacchetto. Infine, esportate il progetto come file JAR.

1. Modificate l&#39;URL nella classe `EncryptionServiceLocator` per specificare il tipo di codifica. Ad esempio, per utilizzare base64, specificare `?blob=base64` in modo che l&#39;oggetto `BLOB` restituisca dati binari. Ovvero, nella classe `EncryptionServiceLocator`, individuare la seguente riga di codice:

   ```java
    http://localhost:8080/soap/services/EncryptionService;
   ```

   e cambiarlo in:

   ```java
    http://localhost:8080/soap/services/EncryptionService?blob=base64;
   ```

1. Aggiungete i seguenti file JAR dell&#39;asse al percorso di classe del progetto Java:

   * activation.jar
   * axis.jar
   * commons-codec-1.3.jar
   * commons-collections-3.1.jar
   * commons-discovery.jar
   * commons-logging.jar
   * dom3-xml-apis-2.5.0.jar
   * jai_imageio.jar
   * jaxen-1.1-beta-9.jar
   * jaxrpc.jar
   * log4j.jar
   * mail.jar
   * saaj.jar
   * wsdl4j.jar
   * xalan.jar
   * xbean.jar
   * xercesImpl.jar

   Questi file JAR si trovano nella directory `[install directory]/Adobe/Adobe Experience Manager Forms/sdk/lib/thirdparty`.

**Consulta anche**

[Creazione di classi proxy Java tramite JAX-WS](#creating-java-proxy-classes-using-jax-ws)

[Richiamo  AEM Forms con codifica Base64](#invoking-aem-forms-using-base64-encoding)

[Richiamo  AEM Forms utilizzando dati BLOB su HTTP](#invoking-aem-forms-using-blob-data-over-http)

## Richiamo  AEM Forms con codifica Base64 {#invoking-aem-forms-using-base64-encoding}

È possibile richiamare un servizio AEM Forms  utilizzando la codifica Base64. La codifica Base64 codifica gli allegati inviati con una richiesta di chiamata al servizio Web. Ovvero, i dati `BLOB` sono codificati in Base64, non nell&#39;intero messaggio SOAP.

&quot;Richiamando  AEM Forms con codifica Base64&quot; viene illustrato come richiamare il seguente processo di breve durata di AEM Forms denominato `MyApplication/EncryptDocument` utilizzando la codifica Base64.

>[!NOTE]
>
>Questo processo non è basato su un processo AEM Forms  esistente. Per seguire l&#39;esempio di codice, creare un processo denominato `MyApplication/EncryptDocument` utilizzando Workbench. (Vedere [Uso di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Quando viene richiamato, questo processo esegue le azioni seguenti:

1. Ottiene il documento PDF non protetto passato al processo. Questa azione è basata sull&#39;operazione `SetValue`. Il parametro di input per questo processo è una variabile di processo `document` denominata `inDoc`.
1. Cifra il documento PDF con una password. Questa azione è basata sull&#39;operazione `PasswordEncryptPDF`. Il documento PDF crittografato con password viene restituito in una variabile di processo denominata `outDoc`.

### Creazione di un assembly client .NET che utilizza la codifica Base64 {#creating-a-net-client-assembly-that-uses-base64-encoding}

È possibile creare un assembly client .NET per richiamare un servizio Forms da un progetto Microsoft Visual Studio .NET. Per creare un assembly client .NET che utilizza la codifica base64, effettuare le seguenti operazioni:

1. Create una classe proxy basata su un URL di chiamata  AEM Forms.
1. Creare un progetto Microsoft Visual Studio .NET che produca l&#39;assembly client .NET.

**Creazione di una classe proxy**

È possibile creare una classe proxy utilizzata per creare l&#39;assembly del client .NET utilizzando uno strumento associato a Microsoft Visual Studio. Il nome dello strumento è wsdl.exe e si trova nella cartella di installazione di Microsoft Visual Studio. Per creare una classe proxy, aprite il prompt dei comandi e individuate la cartella che contiene il file wsdl.exe. Per ulteriori informazioni sullo strumento wsdl.exe, vedere la *Guida MSDN*.

Digitare il comando seguente al prompt dei comandi:

```java
 wsdl https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

Per impostazione predefinita, questo strumento crea un file CS nella stessa cartella che si basa sul nome del WSDL. In questa situazione, crea un file CS denominato *EncryptDocumentService.cs*. Questo file CS consente di creare un oggetto proxy che consente di richiamare il servizio specificato nell&#39;URL di chiamata.

Modificate l&#39;URL nella classe proxy in modo da includere `?blob=base64` in modo che l&#39;oggetto `BLOB` restituisca dati binari. Nella classe proxy, individuare la seguente riga di codice:

```java
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument";
```

e cambiarlo in:

```java
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
```

La sezione *Richiamo  AEM Forms utilizzando Base64 Encoding* utilizza `MyApplication/EncryptDocument` come esempio. Se si sta creando un assembly client .NET per un altro servizio Forms, assicurarsi di sostituire `MyApplication/EncryptDocument` con il nome del servizio.

**Sviluppo dell&#39;assembly del client .NET**

Creare un progetto della libreria di classi di Visual Studio che produca un assembly client .NET. Il file CS creato con wsdl.exe può essere importato in questo progetto. Questo progetto genera un file DLL (l&#39;assembly del client .NET) che è possibile utilizzare in altri progetti .NET di Visual Studio per richiamare un servizio.

1. Avviare Microsoft Visual Studio .NET.
1. Creare un progetto della libreria di classi e denominarlo DocumentService.
1. Importate il file CS creato con wsdl.exe.
1. Nel menu **Progetto**, selezionare **Aggiungi riferimento**.
1. Nella finestra di dialogo Aggiungi riferimento, selezionare **System.Web.Services.dll**.
1. Fare clic su **Seleziona**, quindi fare clic su **OK**.
1. Compilate e create il progetto.

>[!NOTE]
>
>Questa procedura crea un assembly client .NET denominato DocumentService.dll che è possibile utilizzare per inviare richieste SOAP al servizio `MyApplication/EncryptDocument`.

>[!NOTE]
>
>Assicurarsi di aver aggiunto `?blob=base64` all&#39;URL nella classe proxy utilizzata per creare l&#39;assembly client .NET. In caso contrario, non è possibile recuperare dati binari dall&#39;oggetto `BLOB`.

**Riferimento all&#39;assembly del client .NET**

Posizionare l&#39;assembly client .NET appena creato sul computer in cui si sta sviluppando l&#39;applicazione client. Dopo aver posizionato l&#39;assembly del client .NET in una directory, è possibile farvi riferimento da un progetto. Fate anche riferimento alla libreria `System.Web.Services` dal progetto. Se non si fa riferimento a questa libreria, non è possibile utilizzare l&#39;assembly client .NET per richiamare un servizio.

1. Nel menu **Progetto**, selezionare **Aggiungi riferimento**.
1. Fare clic sulla scheda **.NET**.
1. Fare clic su **Browse** e individuare il file DocumentService.dll.
1. Fare clic su **Seleziona**, quindi fare clic su **OK**.

**Richiamo di un servizio utilizzando un assembly client .NET che utilizza la codifica Base64**

È possibile richiamare il servizio `MyApplication/EncryptDocument` (creato in Workbench) utilizzando un assembly client .NET che utilizza la codifica Base64. Per richiamare il servizio `MyApplication/EncryptDocument`, effettuare le seguenti operazioni:

1. Creare un assembly client Microsoft .NET che utilizzi il servizio WSDL `MyApplication/EncryptDocument`.
1. Creare un progetto Microsoft .NET client. Fare riferimento all&#39;assembly client Microsoft .NET nel progetto client. Fare riferimento anche a `System.Web.Services`.
1. Utilizzando l&#39;assembly client Microsoft .NET, creare un oggetto `MyApplication_EncryptDocumentService` richiamando il relativo costruttore predefinito.
1. Impostare la proprietà `MyApplication_EncryptDocumentService` dell&#39;oggetto `Credentials` con un oggetto `System.Net.NetworkCredential`. All&#39;interno del costruttore `System.Net.NetworkCredential`, specificare un nome utente per i moduli AEM e la password corrispondente. Impostare i valori di autenticazione per consentire all&#39;applicazione client .NET di scambiare correttamente i messaggi SOAP con  AEM Forms.
1. Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF passato al processo `MyApplication/EncryptDocument`.
1. Creare un oggetto `System.IO.FileStream` richiamandone il costruttore. Passare un valore di stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
1. Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
1. Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `System.IO.FileStream` dell&#39;oggetto `Read`. Passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
1. Compilare l&#39;oggetto `BLOB` assegnandone la proprietà `binaryData` con il contenuto dell&#39;array di byte.
1. Richiamare il processo `MyApplication/EncryptDocument` richiamando il metodo `MyApplication_EncryptDocumentService` dell&#39;oggetto `invoke` e passando l&#39;oggetto `BLOB` che contiene il documento PDF. Questo processo restituisce un documento PDF crittografato all&#39;interno di un oggetto `BLOB`.
1. Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta il percorso del file del documento crittografato con password.
1. Creare un array di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `MyApplicationEncryptDocumentService` dell&#39;oggetto `invoke`. Compilare l&#39;array di byte ottenendo il valore del membro di dati `BLOB` dell&#39;oggetto `binaryData`.
1. Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
1. Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando l&#39;array di byte.

### Chiamata di un servizio mediante classi proxy Java e codifica Base64 {#invoking-a-service-using-java-proxy-classes-and-base64-encoding}

È possibile richiamare un servizio AEM Forms  utilizzando le classi proxy Java e Base64. Per richiamare il servizio `MyApplication/EncryptDocument` utilizzando le classi proxy Java, effettuare le seguenti operazioni:

1. Creare classi proxy Java utilizzando JAX-WS che utilizza il servizio WSDL `MyApplication/EncryptDocument`. Utilizzate il seguente endpoint WSDL:

   `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1`

   >[!NOTE]
   >
   >Sostituire `hiro-xp` *con l&#39;indirizzo IP del server applicazioni J2EE che ospita  AEM Forms.*

1. Creare pacchetti delle classi proxy Java create utilizzando JAX-WS in un file JAR.
1. Includete il file Java proxy JAR e i file JAR che si trovano nel seguente percorso:

   &lt;install Directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   nel percorso di classe del progetto client Java.

1. Creare un oggetto `MyApplicationEncryptDocumentService` utilizzando il relativo costruttore.
1. Creare un oggetto `MyApplicationEncryptDocument` richiamando il metodo `MyApplicationEncryptDocumentService` dell&#39;oggetto `getEncryptDocument`.
1. Impostate i valori di connessione necessari per richiamare  AEM Forms assegnando valori ai seguenti membri di dati:

   * Assegnare l&#39;endpoint WSDL e il tipo di codifica al campo `javax.xml.ws.BindingProvider` dell&#39;oggetto `ENDPOINT_ADDRESS_PROPERTY`. Per richiamare il servizio `MyApplication/EncryptDocument` utilizzando la codifica Base64, specificate il seguente valore URL:

      `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64`

   * Assegnare l&#39;utente dei moduli AEM al campo `javax.xml.ws.BindingProvider` dell&#39;oggetto `USERNAME_PROPERTY`.
   * Assegnare il valore della password corrispondente al campo `javax.xml.ws.BindingProvider` dell&#39;oggetto `PASSWORD_PROPERTY`.

   L&#39;esempio di codice seguente mostra la logica dell&#39;applicazione:

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. Recuperare il documento PDF da inviare al processo `MyApplication/EncryptDocument` creando un oggetto `java.io.FileInputStream` utilizzando il relativo costruttore. Passa un valore di stringa che specifica la posizione del documento PDF.
1. Creare un array di byte e compilarlo con il contenuto dell&#39;oggetto `java.io.FileInputStream`.
1. Creare un oggetto `BLOB` utilizzando il relativo costruttore.
1. Compilare l&#39;oggetto `BLOB` richiamandone il metodo `setBinaryData` e passando l&#39;array di byte. L&#39;oggetto `setBinaryData` `BLOB` è il metodo da chiamare quando si utilizza la codifica Base64. Consultate Fornitura di oggetti BLOB nelle richieste di assistenza.
1. Richiamare il processo `MyApplication/EncryptDocument` richiamando il metodo `MyApplicationEncryptDocument` dell&#39;oggetto `invoke`. Passa l&#39;oggetto `BLOB` che contiene il documento PDF. Il metodo invoke restituisce un oggetto `BLOB` che contiene il documento PDF crittografato.
1. Creare un array di byte contenente il documento PDF crittografato richiamando il metodo `BLOB` dell&#39;oggetto `getBinaryData`.
1. Salvare il documento PDF crittografato come file PDF. Scrivere l&#39;array di byte in un file.

**Consulta anche**

[Avvio rapido: Chiamata di un servizio tramite file proxy Java e codifica Base64](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-java-proxy-files-and-base64-encoding)

[Creazione di un assembly client .NET che utilizza la codifica Base64](#creating-a-net-client-assembly-that-uses-base64-encoding)

## Chiamata  AEM Forms con MTOM {#invoking-aem-forms-using-mtom}

È possibile richiamare  servizi AEM Forms utilizzando l&#39;MTOM standard del servizio Web. Questo standard definisce il modo in cui i dati binari, come un documento PDF, vengono trasmessi via Internet o Intranet. Una caratteristica di MTOM è l&#39;utilizzo dell&#39;elemento `XOP:Include`. Questo elemento è definito nella specifica XML Binary Optimized Packaging (XOP) per fare riferimento agli allegati binari di un messaggio SOAP.

La discussione qui riguarda l&#39;utilizzo di MTOM per invocare il seguente processo di breve durata di AEM Forms denominato `MyApplication/EncryptDocument`.

>[!NOTE]
>
>Questo processo non è basato su un processo AEM Forms  esistente. Per seguire l&#39;esempio di codice, creare un processo denominato `MyApplication/EncryptDocument` utilizzando Workbench. (Vedere [Uso di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Quando viene richiamato, questo processo esegue le azioni seguenti:

1. Ottiene il documento PDF non protetto passato al processo. Questa azione è basata sull&#39;operazione `SetValue`. Il parametro di input per questo processo è una variabile di processo `document` denominata `inDoc`.
1. Cifra il documento PDF con una password. Questa azione è basata sull&#39;operazione `PasswordEncryptPDF`. Il documento PDF crittografato con password viene restituito in una variabile di processo denominata `outDoc`.

>[!NOTE]
>
>Supporto per MTOM aggiunto in  AEM Forms, versione 9.

>[!NOTE]
>
>Le applicazioni basate su JAX WS che utilizzano il protocollo di trasmissione MTOM sono limitate a 25 MB di dati inviati e ricevuti. Questa limitazione è dovuta a un bug in JAX-WS. Se la dimensione combinata dei file inviati e ricevuti supera i 25 MB, utilizzate il protocollo di trasmissione SwaRef invece di quello MTOM. In caso contrario, esiste la possibilità di un&#39;eccezione `OutOfMemory`.

La discussione qui riguarda l&#39;utilizzo di MTOM all&#39;interno di un progetto Microsoft .NET per richiamare  servizi AEM Forms. .NET framework utilizzato è 3.5 e l&#39;ambiente di sviluppo è Visual Studio 2008. Se nel computer di sviluppo è installato Web Service Enhancements (WSE), rimuoverlo. Il framework .NET 3.5 supporta un framework SOAP denominato Windows Communication Foundation (WCF). Quando si esegue  AEM Forms utilizzando MTOM, è supportato solo WCF (non WSE).

### Creazione di un progetto .NET che richiama un servizio utilizzando MTOM {#creating-a-net-project-that-invokes-a-service-using-mtom}

È possibile creare un progetto Microsoft .NET in grado di richiamare un servizio AEM Forms  utilizzando i servizi Web. Creare innanzitutto un progetto Microsoft .NET utilizzando Visual Studio 2008. Per richiamare un servizio AEM Forms , create un riferimento al servizio AEM Forms  che desiderate richiamare all&#39;interno del progetto. Quando create un riferimento a un servizio, specificate un URL per il servizio AEM Forms :

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

Sostituire `localhost` con l&#39;indirizzo IP del server applicazione J2EE che ospita  AEM Forms. Sostituire `MyApplication/EncryptDocument` con il nome del servizio AEM Forms  da richiamare. Ad esempio, per richiamare un&#39;operazione di Rights Management, specificate:

`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`

L&#39;opzione `lc_version` garantisce la disponibilità  funzionalità AEM Forms, come MTOM. Senza specificare l&#39;opzione `lc_version`, non è possibile richiamare  AEM Forms utilizzando MTOM.

Dopo aver creato un riferimento a un servizio, i tipi di dati associati al servizio AEM Forms  sono disponibili per l&#39;utilizzo all&#39;interno del progetto .NET. Per creare un progetto .NET che richiama un servizio AEM Forms , effettuare le seguenti operazioni:

1. Creare un progetto .NET utilizzando Microsoft Visual Studio 2008.
1. Nel menu **Progetto**, selezionare **Aggiungi riferimento servizio**.
1. Nella finestra di dialogo **Address**, specificare il WSDL nel servizio AEM Forms . Esempio,

   ```java
    http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

1. Fare clic su **Vai**, quindi fare clic su **OK**.

### Richiamo di un servizio utilizzando MTOM in un progetto .NET {#invoking-a-service-using-mtom-in-a-net-project}

Prendere in considerazione il processo `MyApplication/EncryptDocument` che accetta un documento PDF non protetto e restituisce un documento PDF crittografato con password. Per richiamare il processo `MyApplication/EncryptDocument` (creato in Workbench) utilizzando MTOM, eseguire i passaggi seguenti:

1. Creare un progetto Microsoft .NET.
1. Creare un oggetto `MyApplication_EncryptDocumentClient` utilizzando il relativo costruttore predefinito.
1. Creare un oggetto `MyApplication_EncryptDocumentClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms  e il tipo di codifica:

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=mtom
   ```

   Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando create un riferimento a un servizio. Tuttavia, accertatevi di specificare `?blob=mtom`.

   >[!NOTE]
   >
   >Sostituire `hiro-xp` *con l&#39;indirizzo IP del server applicazioni J2EE che ospita  AEM Forms.*

1. Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del membro di dati `EncryptDocumentClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
1. Impostare il membro di dati `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
1. Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

   * Assegnare il nome utente del modulo AEM al membro di dati `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.UserName`.
   * Assegnare il valore della password corrispondente al membro di dati `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.Password`.
   * Assegnare il valore costante `HttpClientCredentialType.Basic` al membro di dati `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al membro di dati `BasicHttpBindingSecurity.Security.Mode`.

   L&#39;esempio di codice seguente mostra queste attività.

   ```java
    //Enable BASIC HTTP authentication
    encryptProcess.ClientCredentials.UserName.UserName = "administrator";
    encryptProcess.ClientCredentials.UserName.Password = "password";
    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
    b.MaxReceivedMessageSize = 4000000;
    b.MaxBufferSize = 4000000;
    b.ReaderQuotas.MaxArrayLength = 4000000;
   ```

1. Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF da passare al processo `MyApplication/EncryptDocument`.
1. Creare un oggetto `System.IO.FileStream` richiamandone il costruttore. Passare un valore di stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
1. Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
1. Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `System.IO.FileStream` dell&#39;oggetto `Read`. Passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
1. Compilare l&#39;oggetto `BLOB` assegnando il membro di dati `MTOM` con il contenuto dell&#39;array di byte.
1. Richiamare il processo `MyApplication/EncryptDocument` richiamando il metodo `MyApplication_EncryptDocumentClient` dell&#39;oggetto `invoke`. Passa l&#39;oggetto `BLOB` che contiene il documento PDF. Questo processo restituisce un documento PDF crittografato all&#39;interno di un oggetto `BLOB`.
1. Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF protetto.
1. Creare un array di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `invoke`. Compilare l&#39;array di byte ottenendo il valore del membro di dati `BLOB` dell&#39;oggetto `MTOM`.
1. Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
1. Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando l&#39;array di byte.

>[!NOTE]
>
>La maggior parte  operazioni di servizio AEM Forms hanno un avvio rapido MTOM. Potete visualizzare questi avvii rapidi nella sezione di avvio rapido corrispondente del servizio. Ad esempio, per vedere la sezione Avvio rapido di Output, vedere [Avvio rapido di Output Service API](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap).

**Consulta anche**

[Avvio rapido: Chiamata di un servizio tramite MTOM in un progetto .NET](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-mtom-in-a-net-project)

[Accesso a più servizi tramite i servizi Web](#accessing-multiple-services-using-web-services)

[Creazione di un&#39;applicazione Web ASP.NET che richiama un processo longevo incentrato sull&#39;uomo](/help/forms/developing/invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

## Chiamata  AEM Forms tramite SwaRef {#invoking-aem-forms-using-swaref}

È possibile richiamare  servizi AEM Forms utilizzando SwaRef. Il contenuto dell&#39;elemento XML `wsi:swaRef` viene inviato come allegato all&#39;interno di un corpo SOAP che memorizza il riferimento all&#39;allegato. Quando si richiama un servizio Forms utilizzando SwaRef, creare classi proxy Java utilizzando l&#39;API Java per i servizi Web XML (JAX-WS). (Vedere [Java API for XML Web Services](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html).)

La discussione qui è su come richiamare il seguente processo Forms di breve durata denominato `MyApplication/EncryptDocument` utilizzando SwaRef.

>[!NOTE]
>
>Questo processo non è basato su un processo AEM Forms  esistente. Per seguire l&#39;esempio di codice, creare un processo denominato `MyApplication/EncryptDocument` utilizzando Workbench. (Vedere [Uso di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Quando viene richiamato, questo processo esegue le azioni seguenti:

1. Ottiene il documento PDF non protetto passato al processo. Questa azione è basata sull&#39;operazione `SetValue`. Il parametro di input per questo processo è una variabile di processo `document` denominata `inDoc`.
1. Cifra il documento PDF con una password. Questa azione è basata sull&#39;operazione `PasswordEncryptPDF`. Il documento PDF crittografato con password viene restituito in una variabile di processo denominata `outDoc`.

>[!NOTE]
>
>Supporto SwaRef aggiunto in  AEM Forms

Di seguito viene illustrato come invocare i servizi Forms utilizzando SwaRef in un&#39;applicazione client Java. L&#39;applicazione Java utilizza le classi proxy create utilizzando JAX-WS.

### Richiamare un servizio utilizzando i file di libreria JAX-WS che utilizzano SwaRef {#invoke-a-service-using-jax-ws-library-files-that-use-swaref}

Per richiamare il processo `MyApplication/EncryptDocument` utilizzando i file proxy Java creati utilizzando JAX-WS e SwaRef, eseguire i seguenti passaggi:

1. Creare classi proxy Java utilizzando JAX-WS che utilizza il servizio WSDL `MyApplication/EncryptDocument`. Utilizzate il seguente endpoint WSDL:

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   Per informazioni, vedere [Creazione di classi proxy Java tramite JAX-WS](#creating-java-proxy-classes-using-jax-ws).

   >[!NOTE]
   >
   >Sostituire `hiro-xp` *con l&#39;indirizzo IP del server applicazioni J2EE che ospita  AEM Forms.*

1. Creare pacchetti delle classi proxy Java create utilizzando JAX-WS in un file JAR.
1. Includete il file Java proxy JAR e i file JAR che si trovano nel seguente percorso:

   &lt;install Directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   nel percorso di classe del progetto client Java.

1. Creare un oggetto `MyApplicationEncryptDocumentService` utilizzando il relativo costruttore.
1. Creare un oggetto `MyApplicationEncryptDocument` richiamando il metodo `MyApplicationEncryptDocumentService` dell&#39;oggetto `getEncryptDocument`.
1. Impostate i valori di connessione necessari per richiamare  AEM Forms assegnando valori ai seguenti membri di dati:

   * Assegnare l&#39;endpoint WSDL e il tipo di codifica al campo `javax.xml.ws.BindingProvider` dell&#39;oggetto `ENDPOINT_ADDRESS_PROPERTY`. Per richiamare il servizio `MyApplication/EncryptDocument` utilizzando la codifica SwaRef, specificate il seguente valore URL:

      ` https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref`

   * Assegnare l&#39;utente dei moduli AEM al campo `javax.xml.ws.BindingProvider` dell&#39;oggetto `USERNAME_PROPERTY`.
   * Assegnare il valore della password corrispondente al campo `javax.xml.ws.BindingProvider` dell&#39;oggetto `PASSWORD_PROPERTY`.

   L&#39;esempio di codice seguente mostra la logica dell&#39;applicazione:

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. Recuperare il documento PDF da inviare al processo `MyApplication/EncryptDocument` creando un oggetto `java.io.File` utilizzando il relativo costruttore. Passa un valore di stringa che specifica la posizione del documento PDF.
1. Creare un oggetto `javax.activation.DataSource` utilizzando il costruttore `FileDataSource`. Passa l&#39;oggetto `java.io.File`.
1. Creare un oggetto `javax.activation.DataHandler` utilizzando il relativo costruttore e passando l&#39;oggetto `javax.activation.DataSource`.
1. Creare un oggetto `BLOB` utilizzando il relativo costruttore.
1. Compilare l&#39;oggetto `BLOB` richiamandone il metodo `setSwaRef` e passando l&#39;oggetto `javax.activation.DataHandler`.
1. Richiamare il processo `MyApplication/EncryptDocument` richiamando il metodo `MyApplicationEncryptDocument` dell&#39;oggetto `invoke` e passando l&#39;oggetto `BLOB` che contiene il documento PDF. Il metodo invoke restituisce un oggetto `BLOB` contenente un documento PDF crittografato.
1. Compilare un oggetto `javax.activation.DataHandler` richiamando il metodo `BLOB` dell&#39;oggetto `getSwaRef`.
1. Convertire l&#39;oggetto `javax.activation.DataHandler` in un&#39;istanza `java.io.InputSteam` richiamando il metodo `javax.activation.DataHandler` dell&#39;oggetto `getInputStream`.
1. Scrivere l&#39;istanza `java.io.InputSteam` in un file PDF che rappresenta il documento PDF crittografato.

>[!NOTE]
>
>La maggior parte  operazioni del servizio AEM Forms hanno un avvio rapido SwaRef. Potete visualizzare questi avvii rapidi nella sezione di avvio rapido corrispondente del servizio. Ad esempio, per vedere la sezione Avvio rapido di Output, vedere [Avvio rapido di Output Service API](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap).

**Consulta anche**

[Avvio rapido: Richiamo di un servizio tramite SwaRef in un progetto Java](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-swaref-in-a-java-project)

## Chiamata  AEM Forms con dati BLOB su HTTP {#invoking-aem-forms-using-blob-data-over-http}

È possibile richiamare  servizi AEM Forms utilizzando i servizi Web e inviando dati BLOB via HTTP. La trasmissione di dati BLOB su HTTP è una tecnica alternativa anziché utilizzare la codifica base64, DIME o MIME. Ad esempio, è possibile trasmettere dati via HTTP in un progetto Microsoft .NET che utilizza Web Service Enhancement 3.0, che non supporta DIME o MIME. Quando si utilizzano dati BLOB su HTTP, i dati di input vengono caricati prima che venga richiamato il servizio AEM Forms .

&quot;Richiamando  AEM Forms utilizzando i dati BLOB su HTTP&quot; viene illustrato come richiamare il seguente processo di breve durata di AEM Forms denominato `MyApplication/EncryptDocument` trasmettendo i dati BLOB su HTTP.

>[!NOTE]
>
>Questo processo non è basato su un processo AEM Forms  esistente. Per seguire l&#39;esempio di codice, creare un processo denominato `MyApplication/EncryptDocument` utilizzando Workbench. (Vedere [Uso di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Quando viene richiamato, questo processo esegue le azioni seguenti:

1. Ottiene il documento PDF non protetto passato al processo. Questa azione è basata sull&#39;operazione `SetValue`. Il parametro di input per questo processo è una variabile di processo `document` denominata `inDoc`.
1. Cifra il documento PDF con una password. Questa azione è basata sull&#39;operazione `PasswordEncryptPDF`. Il documento PDF crittografato con password viene restituito in una variabile di processo denominata `outDoc`.

>[!NOTE]
>
>Si consiglia di avere familiarità con l&#39;invocazione  AEM Forms utilizzando SOAP. (Vedere [Chiamata  AEM Forms tramite servizi Web](#invoking-aem-forms-using-web-services).)

### Creazione di un assembly client .NET che utilizza i dati su HTTP {#creating-a-net-client-assembly-that-uses-data-over-http}

Per creare un assembly client che utilizza i dati via HTTP, seguire il processo specificato in [Richiamo  AEM Forms utilizzando la codifica Base64](#invoking-aem-forms-using-base64-encoding). Tuttavia, modificate l&#39;URL nella classe proxy in modo da includere `?blob=http` invece di `?blob=base64`. In questo modo i dati vengono trasferiti su HTTP. Nella classe proxy, individuare la seguente riga di codice:

```java
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument";
```

e cambiarlo in:

```java
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument?blob=http";
```

**Riferimento all&#39;assembly .NET clientMyApplication/EncryptDocumentt**

Posizionare il nuovo assembly client .NET sul computer in cui si sta sviluppando l&#39;applicazione client. Dopo aver posizionato l&#39;assembly del client .NET in una directory, è possibile farvi riferimento da un progetto. Fate riferimento alla libreria `System.Web.Services` dal progetto. Se non si fa riferimento a questa libreria, non è possibile utilizzare l&#39;assembly client .NET per richiamare un servizio.

1. Nel menu **Progetto**, selezionare **Aggiungi riferimento**.
1. Fare clic sulla scheda **.NET**.
1. Fare clic su **Browse** e individuare il file DocumentService.dll.
1. Fare clic su **Seleziona**, quindi fare clic su **OK**.

**Richiamo di un servizio utilizzando un assembly client .NET che utilizza dati BLOB su HTTP**

È possibile richiamare il servizio `MyApplication/EncryptDocument` (creato in Workbench) utilizzando un assembly client .NET che utilizza i dati via HTTP. Per richiamare il servizio `MyApplication/EncryptDocument`, effettuare le seguenti operazioni:

1. Creare l&#39;assembly del client .NET.
1. Fare riferimento all&#39;assembly client Microsoft .NET. Creare un progetto Microsoft .NET client. Fare riferimento all&#39;assembly client Microsoft .NET nel progetto client. Fare riferimento anche a `System.Web.Services`.
1. Utilizzando l&#39;assembly client Microsoft .NET, creare un oggetto `MyApplication_EncryptDocumentService` richiamando il relativo costruttore predefinito.
1. Impostare la proprietà `MyApplication_EncryptDocumentService` dell&#39;oggetto `Credentials` con un oggetto `System.Net.NetworkCredential`. All&#39;interno del costruttore `System.Net.NetworkCredential`, specificare un nome utente per i moduli AEM e la password corrispondente. Impostare i valori di autenticazione per consentire all&#39;applicazione client .NET di scambiare correttamente i messaggi SOAP con  AEM Forms.
1. Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per trasmettere i dati al processo `MyApplication/EncryptDocument`.
1. Assegnare un valore di stringa al membro di dati `remoteURL` dell&#39;oggetto `BLOB` che specifica la posizione URI di un documento PDF da trasmettere al servizio `MyApplication/EncryptDocument`.
1. Richiamare il processo `MyApplication/EncryptDocument` richiamando il metodo `MyApplication_EncryptDocumentService` dell&#39;oggetto `invoke` e passando l&#39;oggetto `BLOB`. Questo processo restituisce un documento PDF crittografato all&#39;interno di un oggetto `BLOB`.
1. Creare un oggetto `System.UriBuilder` utilizzando il relativo costruttore e passando il valore del membro di dati `BLOB` restituito dell&#39;oggetto `remoteURL`.
1. Convertire l&#39;oggetto `System.UriBuilder` in un oggetto `System.IO.Stream`. (L&#39;Avvio rapido C# che segue questo elenco illustra come eseguire questa attività.)
1. Creare un array di byte e compilarlo con i dati che si trovano nell&#39;oggetto `System.IO.Stream`.
1. Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
1. Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando l&#39;array di byte.

### Richiamo di un servizio mediante classi proxy Java e dati BLOB su HTTP {#invoking-a-service-using-java-proxy-classes-and-blob-data-over-http}

Potete richiamare un servizio AEM Forms  utilizzando le classi proxy Java e i dati BLOB su HTTP. Per richiamare il servizio `MyApplication/EncryptDocument` utilizzando le classi proxy Java, effettuare le seguenti operazioni:

1. Creare classi proxy Java utilizzando JAX-WS che utilizza il servizio WSDL `MyApplication/EncryptDocument`. Utilizzate il seguente endpoint WSDL:

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   Per informazioni, vedere [Creazione di classi proxy Java tramite JAX-WS](#creating-java-proxy-classes-using-jax-ws).

   >[!NOTE]
   >
   >Sostituire `hiro-xp` *con l&#39;indirizzo IP del server applicazioni J2EE che ospita  AEM Forms.*

1. Creare pacchetti delle classi proxy Java create utilizzando JAX-WS in un file JAR.
1. Includete il file Java proxy JAR e i file JAR che si trovano nel seguente percorso:

   &lt;install Directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   nel percorso di classe del progetto client Java.

1. Creare un oggetto `MyApplicationEncryptDocumentService` utilizzando il relativo costruttore.
1. Creare un oggetto `MyApplicationEncryptDocument` richiamando il metodo `MyApplicationEncryptDocumentService` dell&#39;oggetto `getEncryptDocument`.
1. Impostate i valori di connessione necessari per richiamare  AEM Forms assegnando valori ai seguenti membri di dati:

   * Assegnare l&#39;endpoint WSDL e il tipo di codifica al campo `javax.xml.ws.BindingProvider` dell&#39;oggetto `ENDPOINT_ADDRESS_PROPERTY`. Per richiamare il servizio `MyApplication/EncryptDocument` utilizzando la codifica BLOB su HTTP, specificate il seguente valore URL:

      `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http`

   * Assegnare l&#39;utente dei moduli AEM al campo `javax.xml.ws.BindingProvider` dell&#39;oggetto `USERNAME_PROPERTY`.
   * Assegnare il valore della password corrispondente al campo `javax.xml.ws.BindingProvider` dell&#39;oggetto `PASSWORD_PROPERTY`.

   L&#39;esempio di codice seguente mostra la logica dell&#39;applicazione:

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. Creare un oggetto `BLOB` utilizzando il relativo costruttore.
1. Compilare l&#39;oggetto `BLOB` richiamandone il metodo `setRemoteURL`. Passa un valore di stringa che specifica la posizione URI di un documento PDF da passare al servizio `MyApplication/EncryptDocument`.
1. Richiamare il processo `MyApplication/EncryptDocument` richiamando il metodo `MyApplicationEncryptDocument` dell&#39;oggetto `invoke` e passando l&#39;oggetto `BLOB` che contiene il documento PDF. Questo processo restituisce un documento PDF crittografato all&#39;interno di un oggetto `BLOB`.
1. Creare un array di byte per memorizzare il flusso di dati che rappresenta il documento PDF crittografato. Richiamare il metodo `BLOB` dell&#39;oggetto `getRemoteURL` (utilizzare l&#39;oggetto `BLOB` restituito dal metodo `invoke`).
1. Creare un oggetto `java.io.File` utilizzando il relativo costruttore. Questo oggetto rappresenta il documento PDF crittografato.
1. Creare un oggetto `java.io.FileOutputStream` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.File`.
1. Richiamare il metodo `java.io.FileOutputStream` dell&#39;oggetto `write`. Trasmettere l&#39;array di byte che contiene il flusso di dati che rappresenta il documento PDF crittografato.

## Richiamo  AEM Forms con DIME {#invoking-aem-forms-using-dime}

È possibile richiamare  servizi AEM Forms utilizzando SOAP con allegati.  AEM Forms supporta sia gli standard dei servizi Web MIME che DIME. DIME consente di inviare allegati binari, come documenti PDF, insieme a richieste di chiamata invece di codificare l&#39;allegato. Nella sezione *Richiamo  AEM Forms utilizzando DIME* viene illustrato come richiamare il seguente processo di breve durata di AEM Forms denominato `MyApplication/EncryptDocument` utilizzando DIME.

Quando viene richiamato, questo processo esegue le azioni seguenti:

1. Ottiene il documento PDF non protetto passato al processo. Questa azione è basata sull&#39;operazione `SetValue`. Il parametro di input per questo processo è una variabile di processo `document` denominata `inDoc`.
1. Cifra il documento PDF con una password. Questa azione è basata sull&#39;operazione `PasswordEncryptPDF`. Il documento PDF crittografato con password viene restituito in una variabile di processo denominata `outDoc`.

Questo processo non è basato su un processo AEM Forms  esistente. Per seguire gli esempi di codice, creare un processo denominato `MyApplication/EncryptDocument` utilizzando Workbench. (Vedere [Uso di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

>[!NOTE]
>
>La chiamata  operazioni di servizio AEM Forms tramite DIME è obsoleta. Si consiglia di utilizzare MTOM. (Vedere [Chiamata  AEM Forms tramite MTOM](#invoking-aem-forms-using-mtom).)

### Creazione di un progetto .NET che utilizza DIME {#creating-a-net-project-that-uses-dime}

Per creare un progetto .NET in grado di richiamare un servizio Forms utilizzando DIME, eseguire le operazioni seguenti:

* Installazione di Web Services Enhancements 2.0 nel computer di sviluppo.
* Dall&#39;interno del progetto .NET, creare un riferimento Web al servizio Forms FormsAEM.

**Installazione dei miglioramenti ai servizi Web 2.0**

Installazione dei miglioramenti ai servizi Web 2.0 nel computer di sviluppo e integrazione con Microsoft Visual Studio .NET. È possibile scaricare Web Services Enhancements 2.0 dal [Centro download Microsoft.](https://www.microsoft.com/downloads/search.aspx)

Da questa pagina Web, cercare Web Services Enhancements 2.0 e scaricarlo sul computer di sviluppo. Questo download inserisce nel computer un file denominato Microsoft WSE 2.0 SPI.msi. Eseguire il programma di installazione e seguire le indicazioni online.

>[!NOTE]
>
>Web Services Enhancements 2.0 supporta DIME. La versione supportata di Microsoft Visual Studio è 2003 quando si utilizzano i miglioramenti ai servizi Web 2.0. Web Services Enhancement 3.0 non supporta DIME; tuttavia, supporta MTOM.

**Creazione di un riferimento Web a un servizio AEM Forms**

Dopo aver installato Web Services Enhancements 2.0 nel computer di sviluppo e creato un progetto Microsoft .NET, creare un riferimento Web al servizio Forms. Ad esempio, per creare un riferimento Web al processo `MyApplication/EncryptDocument` e presupponendo che Forms sia installato sul computer locale, specificate il seguente URL:

```java
     http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL
```

Dopo aver creato un riferimento Web, è possibile utilizzare nel progetto .NET i due tipi di dati proxy seguenti: `EncryptDocumentService` e `EncryptDocumentServiceWse`. Per richiamare il processo `MyApplication/EncryptDocument` utilizzando DIME, utilizzare il tipo `EncryptDocumentServiceWse`.

>[!NOTE]
>
>Prima di creare un riferimento Web al servizio Forms, assicurarsi di fare riferimento a Web Services Enhancements 2.0 nel progetto. (Vedere &quot;Installazione dei miglioramenti ai servizi Web 2.0&quot;.)

**Riferimento alla libreria WSE**

1. Nel menu Progetto, selezionate Aggiungi riferimento.
1. Nella finestra di dialogo Aggiungi riferimento, selezionare Microsoft.Web.Services2.dll.
1. Selezionare System.Web.Services.dll.
1. Fate clic su Seleziona e quindi su OK.

**Creare un riferimento Web a un servizio Forms**

1. Nel menu Progetto, selezionate Aggiungi riferimento Web.
1. Nella finestra di dialogo URL, specificate l&#39;URL del servizio Forms.
1. Fare clic su Vai, quindi su Aggiungi riferimento.

>[!NOTE]
>
>Assicurarsi di abilitare il progetto .NET per l&#39;utilizzo della libreria WSE. In Esplora progetti, fare clic con il pulsante destro del mouse sul nome del progetto e selezionare Abilita WSE 2.0. Verificare che la casella di controllo nella finestra di dialogo visualizzata sia selezionata.

**Richiamo di un servizio mediante DIME in un progetto .NET**

È possibile richiamare un servizio Forms utilizzando DIME. Prendere in considerazione il processo `MyApplication/EncryptDocument` che accetta un documento PDF non protetto e restituisce un documento PDF crittografato con password. Per richiamare il processo `MyApplication/EncryptDocument` utilizzando DIME, eseguire i seguenti passaggi:

1. Creare un progetto Microsoft .NET che consenta di richiamare un servizio Forms utilizzando DIME. Assicurarsi di includere i miglioramenti ai servizi Web 2.0 e creare un riferimento Web al servizio AEM Forms .
1. Dopo aver impostato un riferimento Web al processo `MyApplication/EncryptDocument`, creare un oggetto `EncryptDocumentServiceWse` utilizzando il relativo costruttore predefinito.
1. Impostare il membro di dati `Credentials` dell&#39;oggetto `EncryptDocumentServiceWse` con un valore `System.Net.NetworkCredential` che specifica il nome utente e il valore della password del modulo AEM.
1. Creare un oggetto `Microsoft.Web.Services2.Dime.DimeAttachment` utilizzando il relativo costruttore e passando i seguenti valori:

   * Un valore di stringa che specifica un valore GUID. È possibile ottenere un valore GUID richiamando il metodo `System.Guid.NewGuid.ToString`.
   * Una stringa che specifica il tipo di contenuto. Poiché questo processo richiede un documento PDF, specificare `application/pdf`.
   * Un valore di enumerazione `TypeFormat`. Specifica `TypeFormat.MediaType`.
   * Una stringa che specifica la posizione del documento PDF da passare al processo AEM Forms .

1. Creare un oggetto `BLOB` utilizzando il relativo costruttore.
1. Aggiungere l&#39;allegato DIME all&#39;oggetto `BLOB` assegnando il valore del membro di dati `Microsoft.Web.Services2.Dime.DimeAttachment` dell&#39;oggetto `Id` al membro di dati `BLOB` dell&#39;oggetto `attachmentID`.
1. Richiamare il metodo `EncryptDocumentServiceWse.RequestSoapContext.Attachments.Add` e passare l&#39;oggetto `Microsoft.Web.Services2.Dime.DimeAttachment`.
1. Richiamare il processo `MyApplication/EncryptDocument` richiamando il metodo `EncryptDocumentServiceWse` dell&#39;oggetto `invoke` e passando l&#39;oggetto `BLOB` che contiene l&#39;allegato DIME. Questo processo restituisce un documento PDF crittografato all&#39;interno di un oggetto `BLOB`.
1. Ottenere il valore dell&#39;identificatore allegato ottenendo il valore del membro di dati `BLOB` dell&#39;oggetto `attachmentID` restituito.
1. Per ottenere il documento PDF crittografato, è possibile utilizzare l&#39;identificatore allegato in `EncryptDocumentServiceWse.ResponseSoapContext.Attachments` e spostarsi tra gli allegati presenti in &lt;a0/>.
1. Ottenere un oggetto `System.IO.Stream` ottenendo il valore del membro di dati `Attachment` dell&#39;oggetto `Stream`.
1. Create un array di byte e passate tale array di byte al metodo `System.IO.Stream` dell&#39;oggetto `Read`. Questo metodo popola l&#39;array di byte con un flusso di dati che rappresenta il documento PDF crittografato.
1. Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore di stringa che rappresenta una posizione di file PDF. Questo oggetto rappresenta il documento PDF crittografato.
1. Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
1. Scrivere il contenuto dell&#39;array di byte nel file PDF richiamando il metodo `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando l&#39;array di byte.

### Creazione di classi proxy Java Apache Axis che utilizzano DIME {#creating-apache-axis-java-proxy-classes-that-use-dime}

È possibile utilizzare lo strumento Apache Axis WSDL2Java per convertire un servizio WSDL in classi proxy Java in modo da poter richiamare le operazioni del servizio. Apache Ant consente di generare file libreria Axis da un WSDL  servizio AEM Forms che consente di richiamare il servizio. (Vedere [Creazione di classi proxy Java tramite Apache Axis](#creating-java-proxy-classes-using-apache-axis).)

Lo strumento Apache Axis WSDL2Java genera file JAVA contenenti metodi utilizzati per inviare richieste SOAP a un servizio. Le richieste SOAP ricevute da un servizio vengono decodificate dalle librerie generate da Axis e tornate ai metodi e agli argomenti.

Per richiamare il servizio `MyApplication/EncryptDocument` (incorporato in Workbench) utilizzando i file libreria generati da Axis e DIME, eseguire le operazioni seguenti:

1. Create classi proxy Java che utilizzano il servizio WSDL `MyApplication/EncryptDocument` utilizzando Apache Axis. (Vedere [Creazione di classi proxy Java tramite Apache Axis](#creating-java-proxy-classes-using-apache-axis).)
1. Includete le classi proxy Java nel percorso della classe.
1. Creare un oggetto `MyApplicationEncryptDocumentServiceLocator` utilizzando il relativo costruttore.
1. Creare un oggetto `URL` utilizzando il relativo costruttore e passando un valore di stringa che specifica la definizione WSDL del servizio AEM Forms . Assicurarsi di specificare `?blob=dime` alla fine dell&#39;URL dell&#39;endpoint SOAP. Ad esempio, utilizzate

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=dime.
   ```

1. Creare un oggetto `EncryptDocumentSoapBindingStub` richiamando il relativo costruttore e passando l&#39;oggetto `MyApplicationEncryptDocumentServiceLocator`e l&#39;oggetto `URL`.
1. Impostare il nome utente e il valore della password dei moduli AEM richiamando i metodi `setUsername` e `setPassword` dell&#39;oggetto `EncryptDocumentSoapBindingStub`.

   ```java
    encryptionClientStub.setUsername("administrator");
    encryptionClientStub.setPassword("password");
   ```

1. Recuperare il documento PDF da inviare al servizio `MyApplication/EncryptDocument` creando un oggetto `java.io.File`. Passa un valore di stringa che specifica la posizione del documento PDF.
1. Creare un oggetto `javax.activation.DataHandler` utilizzando il relativo costruttore e passando un oggetto `javax.activation.FileDataSource`. È possibile creare l&#39;oggetto `javax.activation.FileDataSource` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.File` che rappresenta il documento PDF.
1. Creare un oggetto `org.apache.axis.attachments.AttachmentPart` utilizzando il relativo costruttore e passando l&#39;oggetto `javax.activation.DataHandler`.
1. Allegare l&#39;allegato richiamando il metodo `EncryptDocumentSoapBindingStub` dell&#39;oggetto `addAttachment` e passando l&#39;oggetto &lt;a2/>.`org.apache.axis.attachments.AttachmentPart`
1. Creare un oggetto `BLOB` utilizzando il relativo costruttore. Compilare l&#39;oggetto `BLOB` con il valore dell&#39;identificatore allegato richiamando il metodo `BLOB` dell&#39;oggetto `setAttachmentID` e passando il valore dell&#39;identificatore allegato. Questo valore può essere ottenuto richiamando il metodo `org.apache.axis.attachments.AttachmentPart` dell&#39;oggetto `getContentId`.
1. Richiamare il processo `MyApplication/EncryptDocument` richiamando il metodo `EncryptDocumentSoapBindingStub` dell&#39;oggetto `invoke`. Passare l&#39;oggetto `BLOB` che contiene l&#39;allegato DIME. Questo processo restituisce un documento PDF crittografato all&#39;interno di un oggetto `BLOB`.
1. Ottenere il valore dell&#39;identificatore allegato richiamando il metodo `BLOB` dell&#39;oggetto restituito `getAttachmentID`. Questo metodo restituisce un valore di stringa che rappresenta il valore identificatore dell&#39;allegato restituito.
1. Recuperare gli allegati richiamando il metodo `EncryptDocumentSoapBindingStub` dell&#39;oggetto `getAttachments`. Questo metodo restituisce un array di `Objects` che rappresenta gli allegati.
1. Per ottenere il documento PDF crittografato, è necessario utilizzare l&#39;identificatore allegato (l&#39;array `Object`) e utilizzare il valore dell&#39;identificatore allegato. Ciascun elemento è un oggetto `org.apache.axis.attachments.AttachmentPart`.
1. Ottenere l&#39;oggetto `javax.activation.DataHandler` associato all&#39;allegato richiamando il metodo `org.apache.axis.attachments.AttachmentPart` dell&#39;oggetto `getDataHandler`.
1. Ottenere un oggetto `java.io.FileStream` richiamando il metodo `javax.activation.DataHandler` dell&#39;oggetto `getInputStream`.
1. Create un array di byte e passate tale array di byte al metodo `java.io.FileStream` dell&#39;oggetto `read`. Questo metodo popola l&#39;array di byte con un flusso di dati che rappresenta il documento PDF crittografato.
1. Creare un oggetto `java.io.File` utilizzando il relativo costruttore. Questo oggetto rappresenta il documento PDF crittografato.
1. Creare un oggetto `java.io.FileOutputStream` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.File`.
1. Richiamare il metodo `java.io.FileOutputStream` dell&#39;oggetto `write` e passare l&#39;array di byte che contiene il flusso di dati che rappresenta il documento PDF crittografato.

**Consulta anche**

[Avvio rapido: Chiamata di un servizio tramite DIME in un progetto Java](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-dime-in-a-java-project)

## Utilizzo dell&#39;autenticazione basata su SAML {#using-saml-based-authentication}

 AEM Forms supporta diverse modalità di autenticazione del servizio Web quando si richiamano i servizi. Una modalità di autenticazione consiste nel specificare sia il nome utente che il valore della password utilizzando un&#39;intestazione di autorizzazione di base nella chiamata al servizio Web.  AEM Forms supporta anche l&#39;autenticazione basata sull&#39;asserzione SAML. Quando un&#39;applicazione client richiama un servizio AEM Forms  utilizzando un servizio Web, l&#39;applicazione client può fornire informazioni di autenticazione in uno dei modi seguenti:

* Invio delle credenziali nell&#39;ambito dell&#39;autorizzazione di base
* Passaggio del token nome utente come parte dell&#39;intestazione WS-Security
* Passaggio di un&#39;asserzione SAML come parte dell&#39;intestazione WS-Security
* Passaggio del token Kerberos come parte dell&#39;intestazione WS-Security

 AEM Forms non supporta l&#39;autenticazione standard basata sui certificati, ma supporta l&#39;autenticazione basata sui certificati in un modulo diverso.

>[!NOTE]
>
>Il servizio Web avvia rapidamente la programmazione con  AEM Forms specifica i valori di nome utente e password per eseguire l&#39;autorizzazione.

L&#39;identità degli utenti AEM moduli può essere rappresentata tramite un&#39;asserzione SAML firmata utilizzando una chiave segreta. Nel seguente codice XML è riportato un esempio di asserzione SAML.

```xml
 <Assertion xmlns="urn:oasis:names:tc:SAML:1.0:assertion"
     xmlns:saml="urn:oasis:names:tc:SAML:1.0:assertion"
     xmlns:samlp="urn:oasis:names:tc:SAML:1.0:protocol"
     AssertionID="fd4bd0c87302780e0d9bbfa8726d5bc0" IssueInstant="2008-04-17T13:47:00.720Z" Issuer="LiveCycle"
     MajorVersion="1" MinorVersion="1">
     <Conditions NotBefore="2008-04-17T13:47:00.720Z" NotOnOrAfter="2008-04-17T15:47:00.720Z">
     </Conditions>
     <AuthenticationStatement
         AuthenticationInstant="2008-04-17T13:47:00.720Z"
         AuthenticationMethod="urn:oasis:names:tc:SAML:1.0:am:unspecified">
         <Subject>
             <NameIdentifier NameQualifier="DefaultDom">administrator</NameIdentifier>
             <SubjectConfirmation>
                 <ConfirmationMethod>urn:oasis:names:tc:SAML:1.0:cm:sender-vouches</ConfirmationMethod>
             </SubjectConfirmation>
         </Subject>
     </AuthenticationStatement>
     <ds:Signature >
         <ds:SignedInfo>
             <ds:CanonicalizationMethod Algorithm="https://www.w3.org/2001/10/xml-exc-c14n#"></ds:CanonicalizationMethod>
             <ds:SignatureMethod    Algorithm="https://www.w3.org/2000/09/xmldsig#hmac-sha1"></ds:SignatureMethod>
             <ds:Reference URI="#fd4bd0c87302780e0d9bbfa8726d5bc0">
                 <ds:Transforms>
                     <ds:Transform Algorithm="https://www.w3.org/2000/09/xmldsig#enveloped-signature"></ds:Transform>
                     <ds:Transform Algorithm="https://www.w3.org/2001/10/xml-exc-c14n#">
                         <ec:InclusiveNamespaces
                             PrefixList="code ds kind rw saml samlp typens #default">
                         </ec:InclusiveNamespaces>
                     </ds:Transform>
                 </ds:Transforms>
                 <ds:DigestMethod Algorithm="https://www.w3.org/2000/09/xmldsig#sha1"></ds:DigestMethod>
                 <ds:DigestValue>hVrtqjWr+VzaVUIpQx0YI9lIjaY=</ds:DigestValue>
             </ds:Reference>
         </ds:SignedInfo>
         <ds:SignatureValue>UMbBb+cUcPtcWDCIhXes4n4FxfU=</ds:SignatureValue>
     </ds:Signature>
 </Assertion>
```

Questa affermazione di esempio viene rilasciata per un utente amministratore. Questa asserzione contiene i seguenti elementi visibili:

* È valido per una certa durata.
* Viene emesso per un utente specifico.
* È firmato digitalmente. Qualsiasi modifica apportata alla firma potrebbe quindi interrompere la firma.
* Può essere presentato a  AEM Forms come un token dell&#39;identità dell&#39;utente simile al nome utente e alla password.

Un&#39;applicazione client può recuperare l&#39;asserzione da qualsiasi  API AEM Forms AuthenticationManager che restituisce un oggetto `AuthResult`. È possibile ottenere un&#39;istanza `AuthResult` eseguendo uno dei due metodi seguenti:

* Autenticazione dell&#39;utente tramite uno dei metodi di autenticazione esposti dall&#39;API AuthenticationManager. In genere, è possibile utilizzare il nome utente e la password; tuttavia, potete anche utilizzare l&#39;autenticazione basata sui certificati.
* Utilizzo del metodo `AuthenticationManager.getAuthResultOnBehalfOfUser`. Questo metodo consente a un&#39;applicazione client di ottenere un oggetto `AuthResult` per qualsiasi utente AEM moduli.

un utente AEM modulo può essere autenticato utilizzando un token SAML ottenuto. Questa asserzione SAML (frammento xml) può essere inviata come parte dell&#39;intestazione WS-Security con la chiamata del servizio Web per l&#39;autenticazione dell&#39;utente. In genere, un&#39;applicazione client ha autenticato un utente ma non ha memorizzato le credenziali utente. Oppure l’utente ha eseguito l’accesso a tale client tramite un meccanismo diverso dall’uso di un nome utente e una password. In questa situazione, l&#39;applicazione client deve richiamare  AEM Forms e rappresentare un utente specifico che può richiamare  AEM Forms.

Per rappresentare un utente specifico, invocate il metodo `AuthenticationManager.getAuthResultOnBehalfOfUser` utilizzando un servizio Web. Questo metodo restituisce un&#39;istanza `AuthResult` che contiene l&#39;asserzione SAML per tale utente.

Quindi, utilizzate l&#39;asserzione SAML per richiamare qualsiasi servizio che richiede l&#39;autenticazione. Questa azione prevede l&#39;invio dell&#39;asserzione come parte dell&#39;intestazione SOAP. Quando viene effettuata una chiamata a un servizio Web con questa asserzione,  AEM Forms identifica l&#39;utente come rappresentato da tale asserzione. In altre parole, l&#39;utente specificato nell&#39;asserzione è l&#39;utente che sta richiamando il servizio.

### Uso delle classi Apache Axis e autenticazione basata su SAML {#using-apache-axis-classes-and-saml-based-authentication}

È possibile richiamare un servizio AEM Forms  dalle classi proxy Java create utilizzando la libreria Asse. (Vedere [Creazione di classi proxy Java tramite Apache Axis](#creating-java-proxy-classes-using-apache-axis).)

Quando si utilizza AXIS che utilizza l&#39;autenticazione basata su SAML, registrare il gestore di richieste e risposte con Axis. Apache Axis richiama il gestore prima di inviare una richiesta di chiamata a  AEM Forms. Per registrare un gestore, creare una classe Java che si estenda `org.apache.axis.handlers.BasicHandler`.

**Creare un gestore di attività con Axis**

La seguente classe Java, denominata `AssertionHandler.java`, mostra un esempio di classe Java che si estende `org.apache.axis.handlers.BasicHandler`.

```java
 public class AssertionHandler extends BasicHandler {
        public void invoke(MessageContext ctx) throws AxisFault {
            String assertion = (String) ctx.getProperty(LC_ASSERTION);
 
            //no assertion hence nothing to insert
            if(assertion == null) return;
 
            try {
                MessageElement samlElement = new MessageElement(convertToXML(assertion));
                SOAPHeader header = (SOAPHeader) ctx.getRequestMessage().getSOAPHeader();
                //Create the wsse:Security element which would contain the SAML element
                SOAPElement wsseHeader = header.addChildElement("Security", "wsse", WSSE_NS);
                wsseHeader.appendChild(samlElement);
                //remove the actor attribute as in LC we do not specify any actor. This would not remove the actor attribute though
                //it would only remove it from the soapenv namespace
                wsseHeader.getAttributes().removeNamedItem("actor");
            } catch (SOAPException e) {
                throw new AxisFault("Error occured while adding the assertion to the SOAP Header",e);
            }
        }
 }
```

**Registra il gestore**

Per registrare un gestore con Axis, create un file client-config.wsdd. Per impostazione predefinita, Axis cerca un file con questo nome. Il seguente codice XML è un esempio di file client-config.wsdd. Per ulteriori informazioni, consulta la documentazione sull’asse.

```xml
 <deployment xmlns="https://xml.apache.org/axis/wsdd/" xmlns:java="https://xml.apache.org/axis/wsdd/providers/java">
     <transport name="http" pivot="java:org.apache.axis.transport.http.HTTPSender"/>
      <globalConfiguration >
       <requestFlow >
        <handler type="java:com.adobe.idp.um.example.AssertionHandler" />
       </requestFlow >
      </globalConfiguration >
 </deployment>
 
```

**Richiamo di un servizio AEM Forms**

L&#39;esempio di codice seguente richiama un servizio AEM Forms  utilizzando l&#39;autenticazione basata su SAML.

```java
 public class ImpersonationExample {
        . . .
        public void  authenticateOnBehalf(String superUsername,String password,
                String canonicalName,String domainName) throws UMException, RemoteException{
            ((org.apache.axis.client.Stub) authenticationManager).setUsername(superUsername);
            ((org.apache.axis.client.Stub) authenticationManager).setPassword(password);
 
            //Step 1 - Invoke the Auth manager api to get an assertion for the user to be impersonated
            AuthResult ar = authenticationManager.getAuthResultOnBehalfOfUser(canonicalName, domainName, null);
            String assertion = ar.getAssertion();
            //Step 2 - Setting the assertion here to be picked later by the AssertionHandler. Note that stubs are not threadSafe
            //hence should not be reused. For this simple example we have made them instance variable but care should be taken
            //regarding the thread safety
            ((javax.xml.rpc.Stub) authorizationManager)._setProperty(AssertionHandler.LC_ASSERTION, assertion);
        }
 
        public Role findRole(String roleId) throws UMException, RemoteException{
            //This api would be invoked under bob's user rights
            return authorizationManager.findRole(roleId);
        }
 
        public static void main(String[] args) throws Exception {
            ImpersonationExample ie = new ImpersonationExample("http://localhost:5555");
            //Get the SAML assertion for the user to impersonate and store it in stub
            ie.authenticateOnBehalf(
                    "administrator", //The Super user which has the required impersonation permission
                    "password", // Password of the super user as referred above
                    "bob", //Cannonical name of the user to impersonate
                    "testdomain" //Domain of the user to impersonate
                    );
 
            Role r = ie.findRole("BASIC_ROLE_ADMINISTRATOR");
            System.out.println("Role "+r.getName());
        }
 }
```

### Utilizzo di un assembly client .NET e autenticazione basata su SAML {#using-a-net-client-assembly-and-saml-based-authentication}

È possibile richiamare un servizio Forms utilizzando un assembly client .NET e l&#39;autenticazione basata su SAML. A tal fine, è necessario utilizzare il Web Service Enhancements 3.0 (WSE). Per informazioni sulla creazione di un assembly client .NET che utilizza WSE, vedere [Creazione di un progetto .NET che utilizza DIME](#creating-a-net-project-that-uses-dime).

>[!NOTE]
>
>La sezione DIME utilizza WSE 2.0. Per utilizzare l&#39;autenticazione basata su SAML, seguire le stesse istruzioni specificate nell&#39;argomento DIME. Tuttavia, sostituite WSE 2.0 con WSE 3.0. Installazione di Web Services Enhancements 3.0 nel computer di sviluppo e integrazione con Microsoft Visual Studio .NET. È possibile scaricare i miglioramenti apportati ai servizi Web 3.0 dal [Centro download Microsoft](https://www.microsoft.com/downloads/search.aspx).

L&#39;architettura WSE utilizza i tipi di dati Criteri, Asserzioni e SecurityToken. Brevemente, per una chiamata a un servizio Web, specificate un criterio. Un criterio può contenere più asserzioni. Ogni asserzione può contenere filtri. Un filtro viene invocato in determinate fasi di una chiamata a un servizio Web e, in quel momento, può modificare la richiesta SOAP. Per informazioni dettagliate, consultate la documentazione sui miglioramenti dei servizi Web 3.0.

**Creare l&#39;asserzione e il filtro**

Nell&#39;esempio di codice C# vengono create classi di filtri e asserzioni. Questo esempio di codice crea un SamlAssertionOutputFilter. Questo filtro viene richiamato dal framework WSE prima che la richiesta SOAP venga inviata a  AEM Forms.

```java
 class LCSamlPolicyAssertion : Microsoft.Web.ServicES4.Design.PolicyAssertion
 {
        public override Microsoft.Web.ServicES4.SoapFilter CreateClientOutputFilter(FilterCreationContext context)
        {
           return new SamlAssertionOutputFilter();
        }
        . . .
 }
 
 
 class SamlAssertionOutputFilter : SendSecurityFilter
 {
        public override void SecureMessage(SoapEnvelope envelope, Security security)
        {
           // Get the SamlToken from the SessionState
           SamlToken samlToken = envelope.Context.Credentials.UltimateReceiver.GetClientToken<SamlToken>();
           security.Tokens.Add(samlToken);
        }
 }
```

**Creare il token SAML**

Create una classe per rappresentare l&#39;asserzione SAML. L&#39;attività principale eseguita da questa classe è convertire i valori dei dati da stringa a xml e mantenere lo spazio vuoto. Questo xml di asserzione viene importato in seguito nella richiesta SOAP.

```java
 class SamlToken : SecurityToken
 {
        public const string SAMLAssertion = "https://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1";
        private XmlElement _assertionElement;
 
        public SamlToken(string assertion)
             : base(SAMLAssertion)
        {
           XmlDocument xmlDoc = new XmlDocument();
           //The white space has to be preserved else the digital signature would get broken
           xmlDoc.PreserveWhitespace = true;
           xmlDoc.LoadXml(assertion);
           _assertionElement = xmlDoc.DocumentElement;
         }
 
         public override XmlElement GetXml(XmlDocument document)
         {
            return (XmlElement)document.ImportNode(_assertionElement, true);
         }
        . . .
 }
```

**Richiamo di un servizio AEM Forms**

Nell&#39;esempio di codice C# riportato di seguito viene richiamato un servizio Forms utilizzando l&#39;autenticazione basata su SAML.

```java
 public class ImpersonationExample
 {
        . . .
        public void AuthenticateOnBehalf(string superUsername, string password, string canonicalName, string domainName)
        {
            //Create a policy for UsernamePassword Token
            Policy usernamePasswordPolicy = new Policy();
            usernamePasswordPolicy.Assertions.Add(new UsernameOverTransportAssertion());
 
            UsernameToken token = new UsernameToken(superUsername, password, PasswordOption.SendPlainText);
            authenticationManager.SetClientCredential(token);
            authenticationManager.SetPolicy(usernamePasswordPolicy);
 
            //Get the SAML assertion for impersonated user
            AuthClient.AuthenticationManagerService.AuthResult ar
                = authenticationManager.getAuthResultOnBehalfOfUser(canonicalName, domainName, null);
            System.Console.WriteLine("Received assertion " + ar.assertion);
 
            //Create a policy for inserting SAML assertion
            Policy samlPolicy = new Policy();
            samlPolicy.Assertions.Add(new LCSamlPolicyAssertion());
            authorizationManager.SetPolicy(samlPolicy);
            //Set the SAML assertion obtained previously as the token
            authorizationManager.SetClientCredential(new SamlToken(ar.assertion));
        }
 
        public Role findRole(string roleId)
        {
            return authorizationManager.findRole(roleId);
        }
 
        static void Main(string[] args)
        {
            ImpersonationExample ie = new ImpersonationExample("http://localhost:5555");
            ie.AuthenticateOnBehalf(
                 "administrator", //The Super user which has the required impersonation permission
                 "password", // Password of the super user as referred above
                 "bob", //Cannonical name of the user to impersonate
                 "testdomain" //Domain of the user to impersonate
                 );
 
         Role r = ie.findRole("BASIC_ROLE_ADMINISTRATOR");
            System.Console.WriteLine("Role "+r.name);
     }
 }
```

## Considerazioni correlate all&#39;utilizzo dei servizi Web {#related-considerations-when-using-web-services}

A volte si verificano dei problemi quando si richiamano determinate operazioni  servizi AEM Forms utilizzando i servizi Web. L&#39;obiettivo di questa discussione è identificare tali questioni e fornire una soluzione, se disponibile.

### Richiamo delle operazioni del servizio in modo asincrono {#invoking-service-operations-asynchronously}

Se si tenta di richiamare in modo asincrono un&#39;operazione del servizio AEM Forms , come l&#39;operazione di generazione di file PDF `htmlToPDF`, si verifica un evento `SoapFaultException`. Per risolvere questo problema, creare un file XML di binding personalizzato che associa l&#39;elemento `ExportPDF_Result` e altri elementi a classi diverse. Il seguente codice XML rappresenta un file di binding personalizzato.

```xml
 <bindings
        xmlns:xsd="https://www.w3.org/2001/XMLSchema"
        xmlns:jxb="https://java.sun.com/xml/ns/jaxb" jxb:version="1.0"
        xmlns:wsdl="https://schemas.xmlsoap.org/wsdl/"
      wsdlLocation="http://localhost:8080/soap/services/GeneratePDFService?wsdl&async=true&lc_version=9.0.0"
        xmlns="https://java.sun.com/xml/ns/jaxws">
        <enableAsyncMapping>false</enableAsyncMapping>
        <package name="external_customize.client"/>
        <enableWrapperStyle>true</enableWrapperStyle>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='ExportPDF_Result']">
            <jxb:class name="ExportPDFAsyncResult">
            </jxb:class>
        </bindings>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='CreatePDF_Result']">
            <jxb:class name="CreatePDFAsyncResult">
            </jxb:class>
        </bindings>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='HtmlToPDF_Result']">
            <jxb:class name="HtmlToPDFAsyncResult">
            </jxb:class>
        </bindings>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='OptimizePDF_Result']">
            <jxb:class name="OptimizePDFAsyncResult">
            </jxb:class>
        </bindings>
        <!--bindings node="//wsdl:portType[@name='GeneratePDFService']/wsdl:operation[@name='HtmlToPDF_Result']">
            <jxb:class name="HtmlToPDFAsyncResult"/>
        </bindings-->
 </bindings>
```

Utilizzare questo file XML per creare file proxy Java utilizzando JAX-WS. (Vedere [Creazione di classi proxy Java tramite JAX-WS](#creating-java-proxy-classes-using-jax-ws).)

Fare riferimento a questo file XML durante l&#39;esecuzione dello strumento JAX-WS (wsimport.exe) utilizzando l&#39;opzione della riga di comando - `b`. Aggiornare l&#39;elemento `wsdlLocation` nel file XML di binding per specificare l&#39;URL di  AEM Forms.

Per garantire il funzionamento della chiamata asincrona, modificate il valore dell&#39;URL del punto finale e specificate `async=true`. Ad esempio, per i file proxy Java creati con JAX-WS, specificare quanto segue per `BindingProvider.ENDPOINT_ADDRESS_PROPERTY`.

`https://server:port/soap/services/ServiceName?wsdl&async=true&lc_version=9.0.0`

L&#39;elenco seguente specifica altri servizi che richiedono un file di binding personalizzato quando viene richiamato in modo asincrono:

* PDFG3D
* Task Manager
* Application Manager
* Gestione directory
* Distiller
* Rights Management
* Gestione documenti

### Differenze nei server applicazioni J2EE {#differences-in-j2ee-application-servers}

A volte una libreria proxy creata utilizzando uno specifico server applicazione J2EE non richiama correttamente  AEM Forms ospitato su un server applicazione J2EE diverso. Considerare una libreria proxy generata utilizzando  AEM Forms distribuita su WebSphere. Questa libreria proxy non è in grado di richiamare  servizi AEM Forms distribuiti sul server applicazioni JBoss.

Alcuni tipi di dati complessi  AEM Forms, come `PrincipalReference`, vengono definiti in modo diverso quando  AEM Forms viene distribuito su WebSphere rispetto al server applicazioni JBoss. Le differenze nei JDK utilizzati dai diversi servizi applicativi J2EE sono il motivo per cui esistono differenze nelle definizioni WSDL. Di conseguenza, utilizzate le librerie proxy generate dallo stesso server applicazione J2EE.

### Accesso a più servizi tramite servizi Web {#accessing-multiple-services-using-web-services}

A causa di conflitti di spazio nomi, gli oggetti dati non possono essere condivisi tra più WSDL di servizi. Diversi servizi possono condividere tipi di dati e, di conseguenza, i servizi condividono la definizione di questi tipi nei WSDL. Ad esempio, non è possibile aggiungere due assembly client .NET contenenti un tipo di dati `BLOB` allo stesso progetto client .NET. Se tentate di farlo, si verifica un errore di compilazione.

L&#39;elenco seguente specifica i tipi di dati che non possono essere condivisi tra più WSDL di servizi:

* `User`
* `Principals`
* `PrincipalReference`
* `Groups`
* `Roles`
* `BLOB`

Per evitare questo problema, è consigliabile qualificare completamente i tipi di dati. Si consideri ad esempio un&#39;applicazione .NET che fa riferimento sia al servizio Forms che al servizio Signature utilizzando un riferimento al servizio. Entrambi i riferimenti di servizio conterranno una classe `BLOB`. Per utilizzare un&#39;istanza `BLOB`, qualificate completamente l&#39;oggetto `BLOB` quando lo dichiarate. Questo approccio è illustrato nel seguente esempio di codice. Per informazioni su questo esempio di codice, vedere [Firma digitale di Forms interattivo](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-interactive-forms).

Nell&#39;esempio di codice C# riportato di seguito viene firmato un modulo interattivo di cui il servizio Forms esegue il rendering. L&#39;applicazione client ha due riferimenti di servizio. L&#39;istanza `BLOB` associata al servizio Forms appartiene allo spazio dei nomi `SignInteractiveForm.ServiceReference2`. Analogamente, l&#39;istanza `BLOB` associata al servizio Signature appartiene allo spazio dei nomi `SignInteractiveForm.ServiceReference1`. Il modulo interattivo firmato viene salvato come file PDF denominato *LoanXFASigned.pdf*.

```csharp
 ???/**
     * Ensure that you create a .NET project that uses
     * MS Visual Studio 2008 and version 3.5 of the .NET
     * framework. This is required to invoke a
     * AEM Forms service using MTOM.
     *
     * For information, see "Invoking AEM Forms using MTOM" in Programming with AEM forms
     */
 using System;
 using System.Collections.Generic;
 using System.Linq;
 using System.Text;
 using System.ServiceModel;
 using System.IO;
 
 //A reference to the Signature service
 using SignInteractiveForm.ServiceReference1;
 
 //A reference to the Forms service
 using SignInteractiveForm.ServiceReference2;
 
 namespace SignInteractiveForm
 {
        class Program
        {
            static void Main(string[] args)
            {
                try
                {
                    //Because BLOB objects are used in both service references
                    //it is necessary to fully-qualify the BLOB objects
 
                    //Retrieve the form -- invoke the Forms service
                    SignInteractiveForm.ServiceReference2.BLOB formData = GetForm();
 
                    //Create a BLOB object associated with the Signature service
                    SignInteractiveForm.ServiceReference1.BLOB sigData = new SignInteractiveForm.ServiceReference1.BLOB();
 
                    //Transfer the byte stream from one Forms BLOB object to the
                    //Signature BLOB object
                    sigData.MTOM = formData.MTOM;
 
                    //Sign the Form -- invoke the Signature service
                    SignForm(sigData);
                }
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
            }
 
            //Creates an interactive PDF form based on a XFA form - invoke the Forms service
            private static SignInteractiveForm.ServiceReference2.BLOB GetForm()
            {
 
                try
                {
                    //Create a FormsServiceClient object
                    FormsServiceClient formsClient = new FormsServiceClient();
                    formsClient.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/FormsService?blob=mtom");
 
                    //Enable BASIC HTTP authentication
                    BasicHttpBinding b = (BasicHttpBinding)formsClient.Endpoint.Binding;
                    b.MessageEncoding = WSMessageEncoding.Mtom;
                    formsClient.ClientCredentials.UserName.UserName = "administrator";
                    formsClient.ClientCredentials.UserName.Password = "password";
                    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                    b.MaxReceivedMessageSize = 2000000;
                    b.MaxBufferSize = 2000000;
                    b.ReaderQuotas.MaxArrayLength = 2000000;
 
                    //Create a BLOB to store form data
                    SignInteractiveForm.ServiceReference2.BLOB formData = new SignInteractiveForm.ServiceReference2.BLOB();
                    SignInteractiveForm.ServiceReference2.BLOB pdfForm = new SignInteractiveForm.ServiceReference2.BLOB();
 
                    //Specify a XML form data
                    string path = "C:\\Adobe\Loan.xml";
                    FileStream fs = new FileStream(path, FileMode.Open);
 
                    //Get the length of the file stream
                    int len = (int)fs.Length;
                    byte[] ByteArray = new byte[len];
 
                    fs.Read(ByteArray, 0, len);
                    formData.MTOM = ByteArray;
 
                    //Specify a XML form data
                    string path2 = "C:\\Adobe\LoanSigXFA.pdf";
                    FileStream fs2 = new FileStream(path2, FileMode.Open);
 
                    //Get the length of the file stream
                    int len2 = (int)fs2.Length;
                    byte[] ByteArray2 = new byte[len2];
 
                    fs2.Read(ByteArray2, 0, len2);
                    pdfForm.MTOM = ByteArray2;
 
                    PDFFormRenderSpec renderSpec = new PDFFormRenderSpec();
                    renderSpec.generateServerAppearance = true;
 
                    //Set out parameter values
                    long pageCount = 1;
                    String localValue = "en_US";
                    FormsResult result = new FormsResult();
 
                    //Render an interactive PDF form
                    formsClient.renderPDFForm2(
                        pdfForm,
                        formData,
                        renderSpec,
                        null,
                        null,
                        out pageCount,
                        out localValue,
                        out result);
 
                    //Write the data stream to the BLOB object
                    SignInteractiveForm.ServiceReference2.BLOB outForm = result.outputContent;
                    return outForm;
                }
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
                return null;
            }
 
            //Sign the form -- invoke the Signature service
            private static void SignForm(SignInteractiveForm.ServiceReference1.BLOB inDoc)
            {
 
                try
                {
                    //Create a SignatureServiceClient object
                    SignatureServiceClient signatureClient = new SignatureServiceClient();
                    signatureClient.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/SignatureService?blob=mtom");
 
                    //Enable BASIC HTTP authentication
                    BasicHttpBinding b = (BasicHttpBinding)signatureClient.Endpoint.Binding;
                    b.MessageEncoding = WSMessageEncoding.Mtom;
                    signatureClient.ClientCredentials.UserName.UserName = "administrator";
                    signatureClient.ClientCredentials.UserName.Password = "password";
                    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                    b.MaxReceivedMessageSize = 2000000;
                    b.MaxBufferSize = 2000000;
                    b.ReaderQuotas.MaxArrayLength = 2000000;
 
                    //Specify the name of the signature field
                    string fieldName = "form1[0].grantApplication[0].page1[0].SignatureField1[0]";
 
                    //Create a Credential object
                    Credential myCred = new Credential();
                    myCred.alias = "secure";
 
                    //Specify the reason to sign the document
                    string reason = "The document was reviewed";
 
                    //Specify the location of the signer
                    string location = "New York HQ";
 
                    //Specify contact information
                    string contactInfo = "Tony Blue";
 
                    //Create a PDFSignatureAppearanceOptions object
                    //and show date information
                    PDFSignatureAppearanceOptionSpec appear = new PDFSignatureAppearanceOptionSpec();
                    appear.showDate = true;
 
                    //Sign the PDF document
                    SignInteractiveForm.ServiceReference1.BLOB signedDoc = signatureClient.sign(
                        inDoc,
                        fieldName,
                        myCred,
                        HashAlgorithm.SHA1,
                        reason,
                        location,
                        contactInfo,
                        appear,
                        true,
                        null,
                        null,
                        null);
 
                    //Populate a byte array with BLOB data that represents the signed form
                    byte[] outByteArray = signedDoc.MTOM;
 
                    //Save the signed PDF document
                    string fileName = "C:\\Adobe\LoanXFASigned.pdf";
                    FileStream fs2 = new FileStream(fileName, FileMode.OpenOrCreate);
 
                    //Create a BinaryWriter object
                    BinaryWriter w = new BinaryWriter(fs2);
                    w.Write(outByteArray);
                    w.Close();
                    fs2.Close();
                }
 
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
            }
        }
 }
 
 
```

### I servizi che iniziano con la lettera produco file proxy non validi {#services-starting-with-the-letter-i-produce-invalid-proxy-files}

Il nome di alcune classi proxy generate  AEM Forms non è corretto quando si utilizzano Microsoft .Net 3.5 e WCF. Questo problema si verifica quando vengono create classi proxy per IBMFilenetContentRepositoryConnector, IDPSchedulerService o qualsiasi altro servizio il cui nome inizia con la lettera I. Ad esempio, il nome del client generato nel caso di IBMFileNetContentRepositoryConnector è `BMFileNetContentRepositoryConnectorClient`. Lettera I mancante nella classe proxy generata.

