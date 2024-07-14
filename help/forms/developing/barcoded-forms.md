---
title: Utilizzo di moduli con codice a barre
description: Decodificare dati da un modulo PDF o da un’immagine che contiene un codice a barre utilizzando l’API Java e l’API del servizio Web.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: dd32808e-b773-48a2-90e1-7a277d349493
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations,Barcoded Forms
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1911'
ht-degree: 0%

---

# Utilizzo di moduli con codice a barre {#working-with-barcoded-forms}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

## Informazioni sul servizio Forms con codice a barre {#about-the-barcoded-forms-service}

Il servizio di moduli con codice a barre automatizza l&#39;acquisizione dei dati dai moduli di compilazione e stampa e integra le informazioni acquisite nei principali sistemi IT di un&#39;organizzazione.

Utilizzando il servizio Forms con codice a barre, è possibile aggiungere codici a barre unidimensionali e bidimensionali ai PDF forms interattivi. Puoi quindi pubblicare i moduli con codice a barre su un sito web o distribuirli tramite e-mail o CD. Quando un utente compila un modulo codificato a barre utilizzando Adobe Reader, Acrobat Professional o Acrobat Standard, il codice a barre viene aggiornato automaticamente per codificare i dati del modulo forniti dall’utente. L’utente può inviare il modulo elettronicamente o stamparlo su carta e inviarlo per posta, fax o mano. In seguito sarà possibile estrarre i dati forniti dall&#39;utente come parte di un flusso di lavoro automatizzato, indirizzando i dati tra i processi di approvazione e i sistemi aziendali.

Per ulteriori informazioni sul servizio Forms con codice a barre, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Decodifica dei dati del modulo con codice a barre {#decoding-barcoded-form-data}

Puoi utilizzare l’API del servizio Forms con codice a barre per decodificare dati da un modulo PDF o da un’immagine che contiene un codice a barre. Per decodificare i dati del modulo si intende l&#39;estrazione dei dati contenuti nel codice a barre. Prima di poter decodificare i dati da un modulo (o un’immagine) di PDF, l’utente deve inserire nel modulo i dati necessari.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms con codice a barre, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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
* xercesImpl.jar (in &lt;directory di installazione>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs\thirdparty)

Se AEM Forms viene distribuito su un server applicazioni J2EE supportato che non è JBOSS, è necessario sostituire adobe-utilities.jar e jbossall-client.jar con file JAR specifici per il server applicazioni J2EE in cui viene distribuito AEM Forms. Per informazioni sulla posizione di tutti i file JAR di AEM Forms, vedi [Inclusi i file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Crea un oggetto API client per moduli con codice a barre**

Prima di poter eseguire a livello di programmazione un&#39;operazione del servizio Forms codificata a barre, è necessario creare un client del servizio Forms codificato a barre. Se si utilizza l&#39;API Java, creare un oggetto `BarcodedFormsServiceClient`. Se si utilizza l&#39;API del servizio Web Forms con codice a barre, creare un oggetto `BarcodedFormsServiceService`.

**Ottieni un modulo PDF contenente dati con codice a barre**

Ottenere un modulo PDF contenente un codice a barre che è stato compilato con dati utente.

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

L’input del set di caratteri come esadecimale nell’API di decodifica implica che il contenuto del codice a barre sia codificato come stringa esadecimale. Ad esempio, se si specifica UTF-8 come codifica Character nel modulo e Hex nell&#39;operazione di decodifica, il contenuto del codice a barre viene codificato come stringa Hex nell&#39;elemento &lt; `xb:content`> nell&#39;output decodificato. Puoi convertire questo valore esadecimale per ottenere il contenuto originale creando la logica dell’applicazione nell’applicazione client.

**Convertire i dati in un&#39;origine dati XML**

Dopo aver decodificato i dati del modulo, è possibile convertirli in dati XDP o XFDF. Si supponga, ad esempio, di voler importare i dati in un altro modulo. Per importare i dati in un modulo XFA, è necessario convertire i dati in dati XDP. Per informazioni, vedere [Importazione dati modulo](/help/forms/developing/importing-exporting-data.md#importing-form-data).

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

   Creare un oggetto `BarcodedFormsServiceClient` utilizzando il relativo costruttore e passando un oggetto `ServiceClientFactory` che contiene proprietà di connessione.

1. Ottieni un modulo PDF contenente dati con codice a barre

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il modulo PDF contenente dati con codice a barre utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del documento PDF.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Decodificare i dati dal modulo PDF

   Decodificare i dati del modulo richiamando il metodo `decode` dell&#39;oggetto `BarcodedFormsServiceClient` e passando i valori seguenti:

   * L&#39;oggetto `com.adobe.idp.Document` che contiene il modulo PDF.
   * Oggetto `java.lang.Boolean` che specifica se decodificare un codice a barre PDF417.
   * Oggetto `java.lang.Boolean` che specifica se decodificare un codice a barre della matrice dati.
   * Oggetto `java.lang.Boolean` che specifica se decodificare un codice a barre del codice QR.
   * Oggetto `java.lang.Boolean` che specifica se decodificare un codice a barre codabar.
   * Oggetto `java.lang.Boolean` che specifica se decodificare un codice a barre 128.
   * Oggetto `java.lang.Boolean` che specifica se decodificare un codice a barre 39.
   * Oggetto `java.lang.Boolean` che specifica se decodificare un codice a barre EAN-13.
   * Oggetto `java.lang.Boolean` che specifica se decodificare un codice a barre EAN-8.
   * Valore di enumerazione `com.adobe.livecycle.barcodedforms.CharSet` che specifica il valore di codifica del set di caratteri utilizzato nel codice a barre.

   Il metodo `decode` restituisce un oggetto `org.w3c.dom.Document` contenente dati del modulo decodificati.

1. Convertire i dati in un&#39;origine dati XML

   Convertire i dati decodificati in dati XDP o XFDF richiamando il metodo `extractToXML` dell&#39;oggetto `BarcodedFormsServiceClient` e passando i valori seguenti:

   * Oggetto `org.w3c.dom.Document` contenente dati decodificati (assicurarsi di utilizzare il valore restituito dal metodo `decode`).
   * Valore di enumerazione `com.adobe.livecycle.barcodedforms.Delimiter` che specifica il delimitatore di riga. È consigliabile specificare `Delimiter.Carriage_Return`.
   * Valore di enumerazione `com.adobe.livecycle.barcodedforms.Delimiter` che specifica il delimitatore di campo. Specificare ad esempio `Delimiter.Tab`.
   * Valore di enumerazione `com.adobe.livecycle.barcodedforms.XMLFormat` che specifica se convertire i dati del codice a barre in dati XML XDP o XFDF. Specificare ad esempio `XMLFormat.XDP` per convertire i dati in dati XDP.

   >[!NOTE]
   >
   >Non specificare gli stessi valori per i parametri delimitatore di riga e delimitatore di campo.

   Il metodo `extractToXML` restituisce un oggetto `java.util.List` in cui ogni elemento è un oggetto `org.w3c.dom.Document`. Nel modulo è presente un elemento separato per ogni codice a barre. In altre parole, se nel modulo sono presenti quattro codici a barre, nell&#39;oggetto `java.util.List` restituito sono presenti quattro elementi.

1. Elabora i dati decodificati

   * Scorrere l&#39;oggetto `java.util.List` per ottenere ogni oggetto `org.w3c.dom.Document` presente nell&#39;elenco.
   * Per ogni elemento dell&#39;elenco, convertire l&#39;oggetto `org.w3c.dom.Document` in un oggetto `com.adobe.idp.Document`. (La logica dell&#39;applicazione che converte un oggetto `org.w3c.dom.Document` in un oggetto `com.adobe.idp.Document` viene visualizzata nella decodifica dei dati del modulo codificati a barre tramite l&#39;esempio dell&#39;API Java).
   * Salvare i dati XML come file XML richiamando `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` e passando un oggetto File che rappresenta il file XML.

**Consulta anche**

[Quick Start (modalità SOAP): decodifica dei dati dei moduli codificati a barre tramite l’API Java](/help/forms/developing/barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Decodificare i dati dei moduli con codice a barre utilizzando l’API del servizio web {#decode-barcoded-form-data-using-the-web-service-api}

Decodificare i dati del modulo utilizzando l’API (servizio web) dei moduli codificati a barre:

1. Includi file di progetto

   * Creare un assembly client Microsoft .NET che utilizzi il WSDL del servizio Forms codificato a barre. Per informazioni, vedere [Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).
   * Fare riferimento all&#39;assembly client Microsoft .NET. Per informazioni, vedere &quot;Riferimento all&#39;assembly client .NET&quot; in [Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).

1. Creare un oggetto API client Forms con codice a barre

   Utilizzando l&#39;assembly client Microsoft .NET che utilizza il servizio WSDL dei moduli codificati a barre, creare un oggetto `BarcodedFormsServiceService` richiamando il relativo costruttore predefinito.

1. Ottieni un modulo PDF contenente dati con codice a barre

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare un documento PDF contenente un codice a barre.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream` e passando la matrice di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando la relativa proprietà `binaryData` al contenuto della matrice di byte.

1. Decodificare i dati dal modulo PDF

   Decodificare i dati del modulo richiamando il metodo `decode` dell&#39;oggetto `BarcodedFormsServiceService` e passando i valori seguenti:

   * L&#39;oggetto `BLOB` che contiene il modulo PDF.
   * Oggetto `Boolean` che specifica se decodificare un codice a barre PDF417.
   * Oggetto `Boolean` che specifica se decodificare un codice a barre della matrice dati.
   * Oggetto `Boolean` che specifica se decodificare un codice a barre del codice QR.
   * Oggetto `Boolean` che specifica se decodificare un codice a barre codabar.
   * Oggetto `Boolean` che specifica se decodificare un codice a barre 128.
   * Oggetto `Bolean` che specifica se decodificare un codice a barre 39.
   * Oggetto `Boolean` che specifica se decodificare un codice a barre EAN-13.
   * Oggetto `Boolean` che specifica se decodificare un codice a barre EAN-8.
   * Valore di enumerazione `CharSet` che specifica il valore di codifica del set di caratteri utilizzato nel codice a barre.

   Il metodo `decode` restituisce un valore stringa contenente dati del modulo decodificati.

1. Convertire i dati in un&#39;origine dati XML

   Convertire i dati decodificati in dati XDP o XFDF richiamando il metodo `extractToXML` dell&#39;oggetto `BarcodedFormsServiceService` e passando i valori seguenti:

   * Valore stringa che contiene dati decodificati (assicurarsi di utilizzare il valore restituito dal metodo `decode`).
   * Valore di enumerazione `Delimiter` che specifica il delimitatore di riga. È consigliabile specificare `Delimiter.Carriage_Return`.
   * Valore di enumerazione `Delimiter` che specifica il delimitatore di campo. Specificare ad esempio `Delimiter.Tab`.
   * Valore di enumerazione `XMLFormat` che specifica se convertire i dati del codice a barre in dati XML XDP o XFDF. Specificare ad esempio `XMLFormat.XDP` per convertire i dati in dati XDP.

   >[!NOTE]
   >
   >Non specificare gli stessi valori per i parametri delimitatore di riga e delimitatore di campo.

   Il metodo `extractToXML` restituisce un array `Object` in cui ogni elemento è un&#39;istanza `BLOB`. Nel modulo è presente un elemento separato per ogni codice a barre. In altre parole, se nel modulo sono presenti quattro codici a barre, nell&#39;array `Object` restituito sono presenti quattro elementi.

1. Elabora i dati decodificati

   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento PDF protetto.
   * Creare una matrice di byte che memorizza il contenuto dei dati dell&#39;oggetto `BLOB` restituito dal metodo `encryptPDFUsingPassword`. Popolare la matrice di byte ottenendo il valore del membro dati `binaryData` dell&#39;oggetto `BLOB`.
   * Creare un oggetto `System.IO.BinaryWriter` richiamandone il costruttore e passando l&#39;oggetto `System.IO.FileStream`.
   * Scrivere il contenuto della matrice di byte in un file PDF richiamando il metodo `Write` dell&#39;oggetto `System.IO.BinaryWriter` e passando la matrice di byte.

**Consulta anche**

[Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
