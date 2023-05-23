---
title: Utilizzo di moduli con codice a barre
seo-title: Working with barcoded forms
description: Decodificare dati da un modulo PDF o da un’immagine che contiene un codice a barre utilizzando l’API Java e l’API del servizio Web.
seo-description: Decode data from a PDF form or an image that contains a barcode using the Java API and Web Service API.
uuid: e56c3c94-384d-401f-b418-dd34cdc57eda
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: eb28ac30-265c-4611-8247-1f4bc826f254
role: Developer
exl-id: dd32808e-b773-48a2-90e1-7a277d349493
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '1920'
ht-degree: 0%

---

# Utilizzo di moduli con codice a barre {#working-with-barcoded-forms}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

## Informazioni sul servizio Forms con codice a barre {#about-the-barcoded-forms-service}

Il servizio di moduli con codice a barre automatizza l&#39;acquisizione dei dati dai moduli di compilazione e stampa e integra le informazioni acquisite nei principali sistemi IT di un&#39;organizzazione.

Utilizzando il servizio Forms con codice a barre, è possibile aggiungere codici a barre unidimensionali e bidimensionali ai PDF forms interattivi. Puoi quindi pubblicare i moduli con codice a barre su un sito web o distribuirli tramite e-mail o CD. Quando un utente compila un modulo codificato a barre utilizzando Adobe Reader, Acrobat Professional o Acrobat Standard, il codice a barre viene aggiornato automaticamente per codificare i dati del modulo forniti dall’utente. L’utente può inviare il modulo elettronicamente o stamparlo su carta e inviarlo per posta, fax o mano. In seguito sarà possibile estrarre i dati forniti dall&#39;utente come parte di un flusso di lavoro automatizzato, indirizzando i dati tra i processi di approvazione e i sistemi aziendali.

Per ulteriori informazioni sul servizio Forms con codice a barre, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Decodifica dei dati del modulo con codice a barre {#decoding-barcoded-form-data}

Puoi utilizzare l’API del servizio Forms con codice a barre per decodificare dati da un modulo PDF o da un’immagine che contiene un codice a barre. Per decodificare i dati del modulo si intendono i dati che si trovano nel codice a barre. Prima di poter decodificare i dati da un modulo (o un’immagine) di PDF, l’utente deve inserire nel modulo i dati necessari.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms con codice a barre, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per decodificare dati da un modulo PDF, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Crea un oggetto API formsClient con codice a barre.
1. Ottieni un modulo PDF contenente dati con codice a barre.
1. Decodifica i dati dal modulo PDF.
1. Convertire i dati in un&#39;origine dati XML.
1. Elabora i dati decodificati.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-barcodedforms-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)
* xercesImpl.jar (che si trova in &lt;install directory=&quot;&quot;>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs\thirdparty)

Se AEM Forms viene distribuito su un server applicazioni J2EE supportato che non è JBOSS, sarà necessario sostituire adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE in cui viene distribuito AEM Forms. Per informazioni sulla posizione di tutti i file JAR di AEM Forms, vedi [Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto API client Forms con codice a barre**

Prima di poter eseguire a livello di programmazione un&#39;operazione del servizio Forms codificata a barre, è necessario creare un client del servizio Forms codificato a barre. Se utilizzi l’API Java, crea un’ `BarcodedFormsServiceClient` oggetto. Se utilizzi l’API del servizio web Forms con codice a barre, crea un’ `BarcodedFormsServiceService` oggetto.

**Ottieni un modulo PDF contenente dati con codice a barre**

È necessario ottenere un modulo PDF contenente un codice a barre che è stato compilato con i dati utente.

**Decodificare i dati dal modulo PDF**

Dopo aver ottenuto un modulo PDF (o un&#39;immagine) contenente un codice a barre, è possibile decodificare i dati. Il servizio Barcoded Forms supporta i seguenti tipi di codici a barre:

* Codici a barre PDF417.
* Codici a barre della matrice dati.
* Codici a barre del codice QR.
* Codici a barre Codabar.
* Codice 128 codici a barre.
* Codice 39 codici a barre.
* Codice a barre EAN-13.
* Codice a barre EAN-8.

L’input del set di caratteri come esadecimale nell’API di decodifica implica che il contenuto del codice a barre sia codificato come stringa esadecimale. Ad esempio, se UTF-8 è specificato come codifica Character nel modulo e Hex è specificato nell&#39;operazione di decodifica, il contenuto del codice a barre viene codificato come stringa Hex nel tag &lt; `xb:content`> nell&#39;output decodificato. Puoi convertire questo valore esadecimale per ottenere il contenuto originale creando la logica dell’applicazione nell’applicazione client.

**Convertire i dati in un&#39;origine dati XML**

Dopo aver decodificato i dati del modulo, è possibile convertirli in dati XDP o XFDF. Si supponga, ad esempio, di voler importare i dati in un altro modulo. Per importare i dati in un modulo XFA, è necessario convertire i dati in dati XDP. Per informazioni, consulta [Importazione dati modulo](/help/forms/developing/importing-exporting-data.md#importing-form-data).

**Elabora i dati decodificati**

È possibile elaborare i dati convertiti per soddisfare i requisiti aziendali. Ad esempio, dopo aver decodificato e convertito i dati, è possibile salvarli in un file, memorizzarli in un database aziendale, compilare un altro modulo e così via. Questa sezione illustra come salvare i dati convertiti come file XML.

>[!NOTE]
>
>Il servizio Forms con codice a barre non riesce a decodificare i dati del codice a barre quando i parametri del delimitatore di riga e del delimitatore di campo hanno lo stesso valore

**Consulta anche**

[Decodificare i dati dei moduli con codice a barre utilizzando l’API Java](barcoded-forms.md#decode-barcoded-form-data-using-the-java-api)

[Decodificare i dati dei moduli con codice a barre utilizzando l’API del servizio web](barcoded-forms.md#decode-barcoded-form-data-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Decodificare i dati dei moduli con codice a barre utilizzando l’API Java {#decode-barcoded-form-data-using-the-java-api}

Decodificare i dati del modulo utilizzando l’API (Java) dei moduli codificati a barre:

1. Includi file di progetto

   Includi i file JAR client nel percorso della classe del progetto Java.

1. Creare un oggetto API client Forms con codice a barre

   Creare un `BarcodedFormsServiceClient` oggetto utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto che contiene proprietà di connessione.

1. Ottieni un modulo PDF contenente dati con codice a barre

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il modulo PDF contenente dati con codice a barre tramite il relativo costruttore e che trasmette un valore stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` mediante il costruttore e passando il `java.io.FileInputStream` oggetto.

1. Decodificare i dati dal modulo PDF

   Decodificare i dati del modulo richiamando `BarcodedFormsServiceClient` dell&#39;oggetto `decode` e fornendo i seguenti valori:

   * Il `com.adobe.idp.Document` oggetto che contiene il modulo PDF.
   * A `java.lang.Boolean` oggetto che specifica se decodificare un codice a barre PDF417.
   * A `java.lang.Boolean` oggetto che specifica se decodificare un codice a barre della matrice dati.
   * A `java.lang.Boolean` oggetto che specifica se decodificare un codice a barre del codice QR.
   * A `java.lang.Boolean` oggetto che specifica se decodificare un codice a barre codabar.
   * A `java.lang.Boolean` oggetto che specifica se decodificare un codice a barre 128.
   * A `java.lang.Boolean` oggetto che specifica se decodificare un codice a barre 39.
   * A `java.lang.Boolean` oggetto che specifica se decodificare un codice a barre EAN-13.
   * A `java.lang.Boolean` oggetto che specifica se decodificare un codice a barre EAN-8.
   * A `com.adobe.livecycle.barcodedforms.CharSet` valore di enumerazione che specifica il valore di codifica del set di caratteri utilizzato nel codice a barre.

   Il `decode` il metodo restituisce un `org.w3c.dom.Document` oggetto contenente dati modulo decodificati.

1. Convertire i dati in un&#39;origine dati XML

   Converti i dati decodificati in dati XDP o XFDF richiamando il `BarcodedFormsServiceClient` dell&#39;oggetto `extractToXML` e fornendo i seguenti valori:

   * Il `org.w3c.dom.Document` oggetto contenente dati decodificati (assicurarsi di utilizzare `decode` valore restituito dal metodo).
   * A `com.adobe.livecycle.barcodedforms.Delimiter` valore di enumerazione che specifica il delimitatore di riga. È consigliabile specificare `Delimiter.Carriage_Return`.
   * A `com.adobe.livecycle.barcodedforms.Delimiter` valore di enumerazione che specifica il delimitatore di campo. Ad esempio, specifica `Delimiter.Tab`.
   * A `com.adobe.livecycle.barcodedforms.XMLFormat` valore di enumerazione che specifica se convertire i dati del codice a barre in dati XML XDP o XFDF. Ad esempio, specifica `XMLFormat.XDP` per convertire i dati in dati XDP.

   >[!NOTE]
   >
   >Non specificare gli stessi valori per i parametri delimitatore di riga e delimitatore di campo.

   Il `extractToXML` il metodo restituisce un `java.util.List` oggetto in cui ogni elemento è un `org.w3c.dom.Document` oggetto. Nel modulo è presente un elemento separato per ogni codice a barre. In altre parole, se nel modulo sono presenti quattro codici a barre, sono presenti quattro elementi nel modulo restituito `java.util.List` oggetto.

1. Elabora i dati decodificati

   * Effettua iterazione attraverso `java.util.List` oggetto per ottenere ciascun `org.w3c.dom.Document` oggetto presente nell&#39;elenco.
   * Per ogni elemento dell’elenco, converti `org.w3c.dom.Document` oggetto a un `com.adobe.idp.Document` oggetto. (La logica dell’applicazione che converte un `org.w3c.dom.Document` oggetto in un `com.adobe.idp.Document` L&#39;oggetto viene visualizzato nella decodifica dei dati del modulo codificati a barre utilizzando l&#39;esempio dell&#39;API Java).
   * Salvare i dati XML come file XML richiamando `com.adobe.idp.Document` dell&#39;oggetto `copyToFile`e il passaggio di un oggetto File che rappresenta il file XML.

**Consulta anche**

[Quick Start (modalità SOAP): decodifica dei dati dei moduli con codice a barre tramite l’API Java](/help/forms/developing/barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Decodificare i dati dei moduli con codice a barre utilizzando l’API del servizio web {#decode-barcoded-form-data-using-the-web-service-api}

Decodificare i dati del modulo utilizzando l’API (servizio web) dei moduli codificati a barre:

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il WSDL del servizio Forms codificato a barre. Per informazioni, consulta [Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).
   * Fare riferimento all&#39;assembly client Microsoft .NET. Per informazioni, vedere &quot;Riferimento all&#39;assembly client .NET&quot; in [Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).

1. Creare un oggetto API client Forms con codice a barre

   Utilizzando l&#39;assembly client Microsoft .NET che utilizza il servizio WSDL dei moduli codificati a barre, creare un `BarcodedFormsServiceService` richiamando il relativo costruttore predefinito.

1. Ottieni un modulo PDF contenente dati con codice a barre

   * Creare un `BLOB` mediante il costruttore. Il `BLOB` L&#39;oggetto viene utilizzato per memorizzare un documento PDF contenente un codice a barre.
   * Creare un `System.IO.FileStream` dell&#39;oggetto richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto della `System.IO.FileStream` oggetto. È possibile determinare le dimensioni della matrice di byte ottenendo `System.IO.FileStream` dell&#39;oggetto `Length` proprietà.
   * Compilare la matrice di byte con i dati di flusso richiamando `System.IO.FileStream` dell&#39;oggetto `Read` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare il `BLOB` oggetto assegnando il relativo `binaryData` con il contenuto della matrice di byte.

1. Decodificare i dati dal modulo PDF

   Decodificare i dati del modulo richiamando `BarcodedFormsServiceService` dell&#39;oggetto `decode` e fornendo i seguenti valori:

   * Il `BLOB` oggetto che contiene il modulo PDF.
   * A `Boolean` oggetto che specifica se decodificare un codice a barre PDF417.
   * A `Boolean` oggetto che specifica se decodificare un codice a barre della matrice dati.
   * A `Boolean` oggetto che specifica se decodificare un codice a barre del codice QR.
   * A `Boolean` oggetto che specifica se decodificare un codice a barre codabar.
   * A `Boolean` oggetto che specifica se decodificare un codice a barre 128.
   * A `Bolean` oggetto che specifica se decodificare un codice a barre 39.
   * A `Boolean` oggetto che specifica se decodificare un codice a barre EAN-13.
   * A `Boolean` oggetto che specifica se decodificare un codice a barre EAN-8.
   * A `CharSet` valore di enumerazione che specifica il valore di codifica del set di caratteri utilizzato nel codice a barre.

   Il `decode` il metodo restituisce un valore stringa contenente dati del modulo decodificati.

1. Convertire i dati in un&#39;origine dati XML

   Converti i dati decodificati in dati XDP o XFDF richiamando il `BarcodedFormsServiceService` dell&#39;oggetto `extractToXML` e fornendo i seguenti valori:

   * Un valore stringa che contiene dati decodificati (assicurati di utilizzare il `decode` valore restituito dal metodo).
   * A `Delimiter` valore di enumerazione che specifica il delimitatore di riga. È consigliabile specificare `Delimiter.Carriage_Return`.
   * A `Delimiter` valore di enumerazione che specifica il delimitatore di campo. Ad esempio, specifica `Delimiter.Tab`.
   * A `XMLFormat` valore di enumerazione che specifica se convertire i dati del codice a barre in dati XML XDP o XFDF. Ad esempio, specifica `XMLFormat.XDP` per convertire i dati in dati XDP.

   >[!NOTE]
   >
   >Non specificare gli stessi valori per i parametri delimitatore di riga e delimitatore di campo.

   Il `extractToXML` il metodo restituisce un `Object` in cui ogni elemento è un `BLOB` dell&#39;istanza. Nel modulo è presente un elemento separato per ogni codice a barre. In altre parole, se nel modulo sono presenti quattro codici a barre, sono presenti quattro elementi nel modulo restituito `Object` array.

1. Elabora i dati decodificati

   * Creare un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF protetto.
   * Creare una matrice di byte che memorizza il contenuto dei dati `BLOB` oggetto restituito da `encryptPDFUsingPassword` metodo. Popolare la matrice di byte ottenendo il valore della `BLOB` dell&#39;oggetto `binaryData` membro dati.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando il `System.IO.FileStream` oggetto.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando `System.IO.BinaryWriter` dell&#39;oggetto `Write` e passando la matrice di byte.

**Consulta anche**

[Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
