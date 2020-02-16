---
title: Uso dei moduli con codice a barre
seo-title: Uso dei moduli con codice a barre
description: 'null'
seo-description: 'null'
uuid: e56c3c94-384d-401f-b418-dd34cdc57eda
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: eb28ac30-265c-4611-8247-1f4bc826f254
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7

---


# Uso dei moduli con codice a barre {#working-with-barcoded-forms}

## Informazioni sul servizio moduli con codice a barre {#about-the-barcoded-forms-service}

Il servizio moduli con codice a barre automatizza l&#39;acquisizione dei dati dai moduli di compilazione e stampa e integra le informazioni acquisite nei sistemi IT di base dell&#39;azienda.

Il servizio moduli con codice a barre consente di aggiungere codici a barre monodimensionali e bidimensionali ai moduli PDF interattivi. È quindi possibile pubblicare i moduli codici a barre in un sito Web o distribuirli per e-mail o CD. Quando un utente compila un modulo con codice a barre utilizzando Adobe Reader, Acrobat Professional o Acrobat Standard, i codici a barre vengono aggiornati automaticamente per codificare i dati del modulo forniti dall&#39;utente. L&#39;utente può inviare il modulo elettronicamente oppure stamparlo e inviarlo per posta, fax o a mano. In un secondo momento potete estrarre i dati forniti dall’utente come parte di un flusso di lavoro automatizzato, indirizzandoli tra i processi di approvazione e i sistemi aziendali.

Per ulteriori informazioni sul servizio dei moduli con codice a barre, consultate Guida di riferimento [ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Decodifica dei dati del modulo con codice a barre {#decoding-barcoded-form-data}

È possibile utilizzare l&#39;API del servizio moduli codici a barre per decodificare i dati da un modulo PDF o da un&#39;immagine che contiene un codice a barre. Per decodifica dei dati del modulo si intende l&#39;estrazione dei dati contenuti nel codice a barre. Prima che i dati possano essere decodificati da un modulo PDF (o da un&#39;immagine), è necessario compilare il modulo con i dati.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio dei moduli con codice a barre, consultate Guida di riferimento [ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per decodificare i dati da un modulo PDF, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto API formClient con codice a barre.
1. Ottenere un modulo PDF contenente dati con codice a barre.
1. Decodificare i dati dal modulo PDF.
1. Conversione dei dati in un&#39;origine dati XML.
1. Elaborare i dati decodificati.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se state creando un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-barcodedforms-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss)
* xercesImpl.jar (nella directory &lt;directory di installazione>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs\thirdparty)

Se AEM Forms è distribuito su un server applicazione J2EE supportato che non è JBOSS, dovrai sostituire adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazione J2EE su cui è distribuito AEM Forms. Per informazioni sulla posizione di tutti i file AEM Forms JAR, consultate [Inclusione dei file](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)di libreria Java AEM Forms.

**Creare un oggetto API client per moduli con codice a barre**

Prima di poter eseguire un&#39;operazione del servizio moduli codici a barre a livello di programmazione, è necessario creare un client di servizi Forms con codice a barre. Se utilizzate l&#39;API Java, create un `BarcodedFormsServiceClient` oggetto. Se si utilizza l&#39;API del servizio Web dei moduli con codice a barre, creare un `BarcodedFormsServiceService` oggetto.

**Ottenere un modulo PDF contenente dati con codice a barre**

È necessario ottenere un modulo PDF contenente un codice a barre compilato con i dati utente.

**Decodifica dei dati dal modulo PDF**

Dopo aver ottenuto un modulo PDF (o un&#39;immagine) contenente un codice a barre, è possibile decodificare i dati. Il servizio Barcoded Forms supporta i seguenti tipi di codici a barre:

* codici a barre PDF417.
* Codici a barre della matrice dati.
* Codici a barre QR.
* Codici a barre codabar.
* Codici a barre Codice 128.
* Codici a barre Codice 39.
* Codici a barre EAN-13.
* Codici a barre EAN-8.

L&#39;input del set di caratteri come esadecimale nell&#39;API di decodifica implica che il contenuto del codice a barre è codificato come una stringa esadecimale. Ad esempio, se UTF-8 è specificato come codifica caratteri nel modulo e Hex è specificato nell&#39;operazione di decodifica, il contenuto del codice a barre è codificato come stringa esadecimale nell&#39;elemento &lt; `xb:content`> nell&#39;output decodificato. Potete convertire questo valore esadecimale per ottenere il contenuto originale creando la logica dell&#39;applicazione nell&#39;applicazione client.

**Conversione dei dati in un&#39;origine dati XML**

Dopo aver decodificato i dati del modulo, è possibile convertirli in dati XDP o XFDF. Ad esempio, si supponga di voler importare i dati in un altro modulo. Per importare i dati in un modulo XFA, è necessario convertire i dati in dati XDP. Per ulteriori informazioni, vedere [Importazione di dati](/help/forms/developing/importing-exporting-data.md#importing-form-data)del modulo.

**Elaborazione dei dati decodificati**

Puoi elaborare i dati convertiti per soddisfare le tue esigenze aziendali. Ad esempio, dopo aver decodificato e convertito i dati, è possibile salvarli in un file, memorizzarli in un database aziendale, compilare un altro modulo e così via. In questa sezione viene illustrato come salvare i dati convertiti come file XML.

>[!NOTE]
>
>Il servizio moduli con codice a barre non è in grado di decodificare i dati del codice a barre se i parametri del delimitatore di riga e del delimitatore di campo hanno lo stesso valore

**Consulta anche**

[Decodifica dei dati del modulo codici a barre tramite l&#39;API Java](barcoded-forms.md#decode-barcoded-form-data-using-the-java-api)

[Decodifica dei dati del modulo codici a barre tramite l&#39;API del servizio Web](barcoded-forms.md#decode-barcoded-form-data-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Decodifica dei dati del modulo codici a barre tramite l&#39;API Java {#decode-barcoded-form-data-using-the-java-api}

Decodificare i dati del modulo utilizzando l&#39;API dei moduli con codice a barre (Java):

1. Includi file di progetto

   Includete i file JAR client nel percorso di classe del progetto Java.

1. Creare un oggetto API client per moduli con codice a barre

   Creare un `BarcodedFormsServiceClient` oggetto utilizzando il relativo costruttore e passando un `ServiceClientFactory` oggetto che contiene le proprietà di connessione.

1. Ottenere un modulo PDF contenente dati con codice a barre

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il modulo PDF contenente dati con codice a barre utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del documento PDF.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Decodifica dei dati dal modulo PDF

   Decodificare i dati del modulo richiamando il `BarcodedFormsServiceClient` metodo dell&#39; `decode` oggetto e passando i seguenti valori:

   * L&#39; `com.adobe.idp.Document` oggetto che contiene il modulo PDF.
   * Un `java.lang.Boolean` oggetto che specifica se decodificare un codice a barre PDF417.
   * Un `java.lang.Boolean` oggetto che specifica se decodificare o meno un codice a barre matrice dati.
   * Un `java.lang.Boolean` oggetto che specifica se decodificare o meno un codice a barre del codice QR.
   * Un `java.lang.Boolean` oggetto che specifica se decodificare un codice a barre codabar.
   * Un `java.lang.Boolean` oggetto che specifica se decodificare un codice a barre 128.
   * Un `java.lang.Boolean` oggetto che specifica se decodificare un codice a barre 39.
   * Un `java.lang.Boolean` oggetto che specifica se decodificare un codice a barre EAN-13.
   * Un `java.lang.Boolean` oggetto che specifica se decodificare un codice a barre EAN-8.
   * Un valore di `com.adobe.livecycle.barcodedforms.CharSet` enumerazione che specifica il valore di codifica del set di caratteri utilizzato nel codice a barre.
   Il `decode` metodo restituisce un `org.w3c.dom.Document` oggetto contenente dati del modulo decodificati.

1. Conversione dei dati in un&#39;origine dati XML

   Convertire i dati decodificati in dati XDP o XFDF richiamando il metodo dell&#39; `BarcodedFormsServiceClient` oggetto `extractToXML` e passando i seguenti valori:

   * L&#39; `org.w3c.dom.Document` oggetto che contiene dati decodificati (assicurarsi di utilizzare il valore restituito dal `decode` metodo).
   * Un valore di `com.adobe.livecycle.barcodedforms.Delimiter` enumerazione che specifica il delimitatore di riga. È consigliabile specificare `Delimiter.Carriage_Return`.
   * Un valore di `com.adobe.livecycle.barcodedforms.Delimiter` enumerazione che specifica il delimitatore di campo. Ad esempio, specificate `Delimiter.Tab`.
   * Un valore di `com.adobe.livecycle.barcodedforms.XMLFormat` enumerazione che specifica se convertire i dati del codice a barre in dati XML XDP o XFDF. Ad esempio, specificare `XMLFormat.XDP` per convertire i dati in dati XDP.
   >[!NOTE]
   >
   >Non specificare gli stessi valori per i parametri del delimitatore di riga e del delimitatore di campo.

   Il `extractToXML` metodo restituisce un `java.util.List` oggetto in cui ogni elemento è un `org.w3c.dom.Document` oggetto. Esiste un elemento separato per ciascun codice a barre che si trova sul modulo. Se il modulo contiene quattro codici a barre, l&#39; `java.util.List` oggetto restituito contiene quattro elementi.

1. Elaborazione dei dati decodificati

   * Scorrere l&#39; `java.util.List` oggetto per ottenere ogni `org.w3c.dom.Document` oggetto che si trova nell&#39;elenco.
   * Per ciascun elemento dell&#39;elenco, convertire l&#39; `org.w3c.dom.Document` oggetto in un `com.adobe.idp.Document` oggetto. (La logica dell&#39;applicazione che converte un `org.w3c.dom.Document` &#39;oggetto in un `com.adobe.idp.Document` oggetto è mostrata nei dati del modulo con codice a barre decodifica, utilizzando l&#39;esempio di API Java).
   * Salvare i dati XML come file XML richiamando l&#39; `com.adobe.idp.Document` oggetto `copyToFile`e passando un oggetto File che rappresenta il file XML.

**Consulta anche**

[Avvio rapido (modalità SOAP): Decodifica dei dati del modulo con codice a barre tramite l&#39;API Java](/help/forms/developing/barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Decodifica dei dati del modulo codici a barre tramite l&#39;API del servizio Web {#decode-barcoded-form-data-using-the-web-service-api}

Decodificare i dati del modulo utilizzando l&#39;API dei moduli codici a barre (servizio Web):

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il servizio WSDL per moduli con codice a barre. Per informazioni, consultate [Richiamo di moduli AEM con codifica](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)Base64.
   * Fare riferimento all&#39;assembly client Microsoft .NET. Per informazioni, vedere &quot;Riferimento all&#39;assembly del client .NET&quot; in [Attivazione di moduli AEM con codifica](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)Base64.

1. Creare un oggetto API client per moduli con codice a barre

   Utilizzando l&#39;assembly client Microsoft .NET che utilizza il servizio WSDL del servizio moduli con codice a barre, creare un `BarcodedFormsServiceService` oggetto richiamando il relativo costruttore predefinito.

1. Ottenere un modulo PDF contenente dati con codice a barre

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare un documento PDF contenente un codice a barre.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` `Read` metodo dell&#39;oggetto e passando l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `binaryData` la proprietà con il contenuto dell&#39;array di byte.

1. Decodifica dei dati dal modulo PDF

   Decodificare i dati del modulo richiamando il `BarcodedFormsServiceService` metodo dell&#39; `decode` oggetto e passando i seguenti valori:

   * L&#39; `BLOB` oggetto che contiene il modulo PDF.
   * Un `Boolean` oggetto che specifica se decodificare un codice a barre PDF417.
   * Un `Boolean` oggetto che specifica se decodificare o meno un codice a barre matrice dati.
   * Un `Boolean` oggetto che specifica se decodificare o meno un codice a barre del codice QR.
   * Un `Boolean` oggetto che specifica se decodificare un codice a barre codabar.
   * Un `Boolean` oggetto che specifica se decodificare un codice a barre 128.
   * Un `Bolean` oggetto che specifica se decodificare un codice a barre 39.
   * Un `Boolean` oggetto che specifica se decodificare un codice a barre EAN-13.
   * Un `Boolean` oggetto che specifica se decodificare un codice a barre EAN-8.
   * Un valore di `CharSet` enumerazione che specifica il valore di codifica del set di caratteri utilizzato nel codice a barre.
   Il `decode` metodo restituisce un valore di stringa contenente dati del modulo decodificati.

1. Conversione dei dati in un&#39;origine dati XML

   Convertire i dati decodificati in dati XDP o XFDF richiamando il metodo dell&#39; `BarcodedFormsServiceService` oggetto `extractToXML` e passando i seguenti valori:

   * Un valore di stringa che contiene dati decodificati (assicurarsi di utilizzare il valore restituito dal `decode` metodo).
   * Un valore di `Delimiter` enumerazione che specifica il delimitatore di riga. È consigliabile specificare `Delimiter.Carriage_Return`.
   * Un valore di `Delimiter` enumerazione che specifica il delimitatore di campo. Ad esempio, specificate `Delimiter.Tab`.
   * Un valore di `XMLFormat` enumerazione che specifica se convertire i dati del codice a barre in dati XML XDP o XFDF. Ad esempio, specificare `XMLFormat.XDP` per convertire i dati in dati XDP.
   >[!NOTE]
   >
   >Non specificare gli stessi valori per i parametri del delimitatore di riga e del delimitatore di campo.

   Il `extractToXML` metodo restituisce un `Object` array in cui ogni elemento è un&#39; `BLOB` istanza. Esiste un elemento separato per ciascun codice a barre che si trova sul modulo. Se il modulo contiene quattro codici a barre, nell&#39; `Object` array restituito sono presenti quattro elementi.

1. Elaborazione dei dati decodificati

   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento PDF protetto.
   * Creare un array di byte che memorizza il contenuto dei dati dell&#39; `BLOB` oggetto restituito dal `encryptPDFUsingPassword` metodo. Compilare l&#39;array di byte ottenendo il valore del membro `BLOB` dati dell&#39; `binaryData` oggetto.
   * Creare un `System.IO.BinaryWriter` oggetto richiamando il relativo costruttore e passando l&#39; `System.IO.FileStream` oggetto.
   * Scrivere il contenuto dell&#39;array di byte in un file PDF richiamando il metodo dell&#39; `System.IO.BinaryWriter` oggetto `Write` e passando l&#39;array di byte.

**Consulta anche**

[Richiamo di moduli AEM con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
