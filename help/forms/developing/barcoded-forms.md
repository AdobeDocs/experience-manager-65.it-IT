---
title: Uso dei moduli con codice a barre
seo-title: Uso dei moduli con codice a barre
description: Decodificare i dati da un modulo PDF o da un’immagine che contiene un codice a barre utilizzando l’API Java e l’API Web Service.
seo-description: Decodificare i dati da un modulo PDF o da un’immagine che contiene un codice a barre utilizzando l’API Java e l’API Web Service.
uuid: e56c3c94-384d-401f-b418-dd34cdc57eda
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: eb28ac30-265c-4611-8247-1f4bc826f254
role: Developer (Sviluppatore)
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1946'
ht-degree: 0%

---


# Uso dei moduli con codice a barre {#working-with-barcoded-forms}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

## Informazioni sul servizio moduli con codice a barre {#about-the-barcoded-forms-service}

Il servizio moduli con codice a barre automatizza l’acquisizione di dati dai moduli di compilazione e stampa e integra le informazioni acquisite nei sistemi IT di base di un’organizzazione.

Il servizio moduli con codice a barre consente di aggiungere codici a barre monodimensionali e bidimensionali ai PDF forms interattivi. È quindi possibile pubblicare i moduli con codice a barre in un sito web o distribuirli per e-mail o CD. Quando un utente compila un modulo con codice a barre utilizzando Adobe Reader, Acrobat Professional o Acrobat Standard, il codice a barre viene aggiornato automaticamente per codificare i dati del modulo forniti dall’utente. L’utente può inviare il modulo elettronicamente o stamparlo su carta e inviarlo per posta, fax o a mano. In seguito è possibile estrarre i dati forniti dall’utente come parte di un flusso di lavoro automatizzato, indirizzandoli tra i processi di approvazione e i sistemi aziendali.

Per ulteriori informazioni sul servizio dei moduli con codice a barre, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Decodifica dei dati dei moduli codificati a barre {#decoding-barcoded-form-data}

È possibile utilizzare l’API del servizio moduli con codice a barre per decodificare i dati da un modulo PDF o da un’immagine contenente un codice a barre. Per decodifica dei dati modulo si intende l’estrazione dei dati contenuti nei codici a barre. Prima che i dati possano essere decodificati da un modulo PDF (o da un’immagine), è necessario che l’utente compili il modulo con i dati.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio dei moduli con codice a barre, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per decodificare i dati da un modulo PDF, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un oggetto API client formscon codice a barre.
1. Ottenere un modulo PDF contenente dati codificati a barre.
1. Decodificare i dati dal modulo PDF.
1. Convertire i dati in un’origine dati XML.
1. Elabora i dati decodificati.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-barcodedforms-client.jar
* adobe-utilities.jar (obbligatorio se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)
* xercesImpl.jar (che si trova in &lt;directory di installazione>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs\thirdparty)

Se AEM Forms è implementato su un server applicazioni J2EE supportato che non è JBOSS, sarà necessario sostituire adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE in cui viene distribuito AEM Forms. Per informazioni sulla posizione di tutti i file JAR di AEM Forms, consulta [Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Creare un oggetto API client per moduli con codice a barre**

Prima di poter eseguire programmaticamente un’operazione del servizio di moduli con codice a barre, è necessario creare un client di servizio Forms con codice a barre. Se utilizzi l’API Java, crea un oggetto `BarcodedFormsServiceClient`. Se utilizzi l’API del servizio Web per moduli con codice a barre, crea un oggetto `BarcodedFormsServiceService` .

**Ottenere un modulo PDF contenente dati con codice a barre**

È necessario ottenere un modulo PDF contenente un codice a barre compilato con i dati utente.

**Decodificare i dati dal modulo PDF**

Dopo aver ottenuto un modulo PDF (o un’immagine) contenente un codice a barre, è possibile decodificare i dati. Il servizio Forms con codice a barre supporta i seguenti tipi di codici a barre:

* Codici a barre PDF417.
* Codici a barre della matrice dati.
* Codici a barre QR.
* Codici a barre Codabar.
* Codici a barre Codice 128.
* Codici a barre Codice 39.
* Codici a barre EAN-13.
* Codici a barre EAN-8.

L’input del set di caratteri come esadecimale nell’API di decodifica implica che il contenuto del codice a barre è codificato come stringa esadecimale. Ad esempio, se UTF-8 è specificato come codifica Carattere nel modulo e Hex è specificato nell’operazione di decodifica, il contenuto del codice a barre viene codificato come stringa esadecimale nell’elemento &lt; `xb:content`> nell’output decodificato. Puoi convertire questo valore esadecimale per ottenere il contenuto originale creando logica applicativa nella tua applicazione client.

**Convertire i dati in un’origine dati XML**

Dopo aver decodificato i dati del modulo, è possibile convertirli in dati XDP o XFDF. Ad esempio, si supponga di voler importare i dati in un altro modulo. Per importare i dati in un modulo XFA, è necessario convertirli in dati XDP. Per informazioni, consultare [Importazione di dati modulo](/help/forms/developing/importing-exporting-data.md#importing-form-data).

**Elaborazione dei dati decodificati**

Puoi elaborare i dati convertiti per soddisfare le tue esigenze aziendali. Ad esempio, dopo aver decodificato e convertito i dati, è possibile salvarli in un file, archiviarli in un database aziendale, compilare un altro modulo e così via. Questa sezione illustra come salvare i dati convertiti come file XML.

>[!NOTE]
>
>Il servizio moduli con codice a barre non è in grado di decodificare i dati del codice a barre quando il delimitatore di riga e i parametri del delimitatore di campo hanno lo stesso valore

**Consulta anche**

[Decodifica dei dati dei moduli con codice a barre tramite l’API Java](barcoded-forms.md#decode-barcoded-form-data-using-the-java-api)

[Decodifica dei dati dei moduli con codice a barre tramite l’API del servizio Web](barcoded-forms.md#decode-barcoded-form-data-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Decodifica dei dati dei moduli con codice a barre utilizzando l’API Java {#decode-barcoded-form-data-using-the-java-api}

Decodifica dei dati del modulo utilizzando l’API dei moduli a barre (Java):

1. Includi file di progetto

   Includi file JAR client nel percorso di classe del progetto Java.

1. Creare un oggetto API client per moduli con codice a barre

   Creare un oggetto `BarcodedFormsServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` contenente proprietà di connessione.

1. Ottenere un modulo PDF contenente dati con codice a barre

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il modulo PDF contenente dati codificati a barre utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Decodificare i dati dal modulo PDF

   Decodificare i dati del modulo richiamando il metodo `decode` dell’oggetto `BarcodedFormsServiceClient` e passando i seguenti valori:

   * L’oggetto `com.adobe.idp.Document` che contiene il modulo PDF.
   * Un oggetto `java.lang.Boolean` che specifica se decodificare un codice a barre PDF417.
   * Un oggetto `java.lang.Boolean` che specifica se decodificare un codice a barre della matrice di dati.
   * Un oggetto `java.lang.Boolean` che specifica se decodificare un codice a barre del codice QR.
   * Un oggetto `java.lang.Boolean` che specifica se decodificare un codice a barre codabar.
   * Un oggetto `java.lang.Boolean` che specifica se decodificare un codice a barre 128.
   * Un oggetto `java.lang.Boolean` che specifica se decodificare un codice a barre 39.
   * Oggetto `java.lang.Boolean` che specifica se decodificare un codice a barre EAN-13.
   * Oggetto `java.lang.Boolean` che specifica se decodificare un codice a barre EAN-8.
   * Valore di enumerazione `com.adobe.livecycle.barcodedforms.CharSet` che specifica il valore di codifica del set di caratteri utilizzato nel codice a barre.

   Il metodo `decode` restituisce un oggetto `org.w3c.dom.Document` contenente dati del modulo decodificati.

1. Convertire i dati in un’origine dati XML

   Converti i dati decodificati in dati XDP o XFDF richiamando il metodo `BarcodedFormsServiceClient` dell’oggetto `extractToXML` e passando i seguenti valori:

   * L&#39;oggetto `org.w3c.dom.Document` che contiene dati decodificati (assicurati di utilizzare il valore restituito del metodo `decode`).
   * Un valore di enumerazione `com.adobe.livecycle.barcodedforms.Delimiter` che specifica il delimitatore di riga. È consigliabile specificare `Delimiter.Carriage_Return`.
   * Un valore di enumerazione `com.adobe.livecycle.barcodedforms.Delimiter` che specifica il delimitatore di campo. Ad esempio, specifica `Delimiter.Tab`.
   * Valore di enumerazione `com.adobe.livecycle.barcodedforms.XMLFormat` che specifica se convertire i dati del codice a barre in dati XML XDP o XFDF. Ad esempio, specificare `XMLFormat.XDP` per convertire i dati in dati XDP.

   >[!NOTE]
   >
   >Non specificare gli stessi valori per i parametri del delimitatore di riga e del delimitatore di campo.

   Il metodo `extractToXML` restituisce un oggetto `java.util.List` in cui ogni elemento è un oggetto `org.w3c.dom.Document`. È disponibile un elemento separato per ciascun codice a barre posizionato sul modulo. In altre parole, se sul modulo sono presenti quattro codici a barre, l&#39;oggetto `java.util.List` restituito contiene quattro elementi.

1. Elaborazione dei dati decodificati

   * Itera attraverso l&#39;oggetto `java.util.List` per ottenere ogni oggetto `org.w3c.dom.Document` presente nell&#39;elenco.
   * Per ogni elemento dell’elenco, convertire l’oggetto `org.w3c.dom.Document` in un oggetto `com.adobe.idp.Document`. (La logica dell&#39;applicazione che converte un oggetto `org.w3c.dom.Document` in un oggetto `com.adobe.idp.Document` viene mostrata nei dati del modulo con codice a barre Decoding utilizzando l&#39;esempio API Java).
   * Salvare i dati XML come file XML richiamando il `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` e passando un oggetto File che rappresenta il file XML.

**Consulta anche**

[Avvio rapido (modalità SOAP): Decodifica di dati modulo codificati a barre tramite API Java](/help/forms/developing/barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Decodifica dei dati dei moduli con codice a barre utilizzando l’API del servizio Web {#decode-barcoded-form-data-using-the-web-service-api}

Decodificare i dati del modulo utilizzando l’API dei moduli a barre (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il servizio WSDL per moduli con codice a barre. Per informazioni, vedere [Richiamo di AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).
   * Fare riferimento all&#39;assembly client Microsoft .NET. Per informazioni, vedere &quot;Riferimento all&#39;assembly client .NET&quot; in [Richiamo di AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).

1. Creare un oggetto API client per moduli con codice a barre

   Utilizzando l’assembly client Microsoft .NET che utilizza il servizio WSDL per i moduli con codice a barre, creare un oggetto `BarcodedFormsServiceService` richiamando il relativo costruttore predefinito.

1. Ottenere un modulo PDF contenente dati con codice a barre

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF contenente un codice a barre.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream` e passando l’array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando la relativa proprietà `binaryData` con il contenuto dell&#39;array di byte.

1. Decodificare i dati dal modulo PDF

   Decodificare i dati del modulo richiamando il metodo `decode` dell’oggetto `BarcodedFormsServiceService` e passando i seguenti valori:

   * L’oggetto `BLOB` che contiene il modulo PDF.
   * Un oggetto `Boolean` che specifica se decodificare un codice a barre PDF417.
   * Un oggetto `Boolean` che specifica se decodificare un codice a barre della matrice di dati.
   * Un oggetto `Boolean` che specifica se decodificare un codice a barre del codice QR.
   * Un oggetto `Boolean` che specifica se decodificare un codice a barre codabar.
   * Un oggetto `Boolean` che specifica se decodificare un codice a barre 128.
   * Un oggetto `Bolean` che specifica se decodificare un codice a barre 39.
   * Oggetto `Boolean` che specifica se decodificare un codice a barre EAN-13.
   * Oggetto `Boolean` che specifica se decodificare un codice a barre EAN-8.
   * Valore di enumerazione `CharSet` che specifica il valore di codifica del set di caratteri utilizzato nel codice a barre.

   Il metodo `decode` restituisce un valore stringa contenente dati del modulo decodificati.

1. Convertire i dati in un’origine dati XML

   Converti i dati decodificati in dati XDP o XFDF richiamando il metodo `BarcodedFormsServiceService` dell’oggetto `extractToXML` e passando i seguenti valori:

   * Una stringa contenente dati decodificati (assicurati di utilizzare il valore restituito del metodo `decode`).
   * Un valore di enumerazione `Delimiter` che specifica il delimitatore di riga. È consigliabile specificare `Delimiter.Carriage_Return`.
   * Un valore di enumerazione `Delimiter` che specifica il delimitatore di campo. Ad esempio, specifica `Delimiter.Tab`.
   * Valore di enumerazione `XMLFormat` che specifica se convertire i dati del codice a barre in dati XML XDP o XFDF. Ad esempio, specificare `XMLFormat.XDP` per convertire i dati in dati XDP.

   >[!NOTE]
   >
   >Non specificare gli stessi valori per i parametri del delimitatore di riga e del delimitatore di campo.

   Il metodo `extractToXML` restituisce un array `Object` in cui ogni elemento è un&#39;istanza `BLOB`. È disponibile un elemento separato per ciascun codice a barre posizionato sul modulo. In altre parole, se sul modulo sono presenti quattro codici a barre, nella matrice `Object` restituita sono presenti quattro elementi.

1. Elaborazione dei dati decodificati

   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF protetto.
   * Creare una matrice di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `encryptPDFUsingPassword`. Compilare l&#39;array di byte ottenendo il valore del membro dati `BLOB` dell&#39;oggetto `binaryData`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivi il contenuto dell’array di byte in un file PDF richiamando il metodo `Write` dell’oggetto `System.IO.BinaryWriter` e passando l’array di byte.

**Consulta anche**

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
