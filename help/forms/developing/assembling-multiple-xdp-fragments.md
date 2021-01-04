---
title: Assemblare Più Frammenti XDP
seo-title: Assemblare Più Frammenti XDP
description: Assemblate più frammenti XDP in un singolo documento XDP utilizzando l'API Java e l'API del servizio Web.
seo-description: Assemblate più frammenti XDP in un singolo documento XDP utilizzando l'API Java e l'API del servizio Web.
uuid: 0e35ff85-ff40-4878-ae31-aa8da75bd3ec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c4706632-02e5-4510-ad9c-4f732d5fbdad
docset: aem65
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '1908'
ht-degree: 0%

---


# Assemblaggio di più frammenti XDP{#assembling-multiple-xdp-fragments}

È possibile assemblare più frammenti XDP in un unico documento XDP. Si consideri ad esempio i frammenti XDP in cui ogni file XDP contiene uno o più sottomoduli utilizzati per creare un modulo di integrità. L&#39;illustrazione seguente mostra la visualizzazione struttura (rappresenta il file tuc018_template_flowed.xdp utilizzato in *Assembling multiple XDP fragments* quick start):

![am_am_forma](assets/am_am_forma.png)

L&#39;illustrazione seguente mostra la sezione paziente (rappresenta il file tuc018_contact.xdp utilizzato nell&#39; *assemblaggio di più frammenti XDP* avvio rapido):

![am_am_formb](assets/am_am_formb.png)

L&#39;illustrazione seguente mostra la sezione relativa allo stato del paziente (rappresenta il file tuc018_paziente.xdp utilizzato nell&#39; *Assembling multiple XDP fragments* quick start):

![am_am_formc](assets/am_am_formc.png)

Questo frammento contiene due sottomoduli denominati *subPatientPhysical* e *subPatientHealth*. Entrambi i sottomoduli sono citati nel documento DDX passato al servizio Assembler. Il servizio Assembler consente di combinare tutti questi frammenti XDP in un unico documento XDP, come illustrato nella figura riportata di seguito.

![am_am_formd](assets/am_am_formd.png)

Nel seguente documento DDX vengono assemblati più frammenti XDP in un documento XDP.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <XDP result="tuc018result.xdp">
            <XDP source="tuc018_template_flowed.xdp">
             <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
               <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientPhysical" required="false"/>
               <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientHealth" required="false"/>
            </XDP>
         </XDP>
 </DDX>
```

Il documento DDX contiene un tag XDP `result` che specifica il nome del risultato. In questa situazione, il valore è `tuc018result.xdp`. A questo valore viene fatto riferimento nella logica dell&#39;applicazione utilizzata per recuperare il documento XDP dopo che il servizio Assembler restituisce il risultato. Si consideri, ad esempio, la seguente logica di applicazione Java utilizzata per recuperare il documento XDP assemblato (notare che il valore è bloccato):

```java
 //Iterate through the map object to retrieve the result XDP document
 for (Iterator i = allDocs.entrySet().iterator(); i.hasNext();) {
     // Retrieve the Map object’s value
     Map.Entry e = (Map.Entry)i.next();
     //Get the key name as specified in the
     //DDX document
     String keyName = (String)e.getKey();
     if (keyName.equalsIgnoreCase("tuc018result.xdp"))
                 {
         Object o = e.getValue();
         outDoc = (Document)o;
         //Save the result PDF file
         File myOutFile = new File("C:\\AssemblerResultXDP.xdp");
         outDoc.copyToFile(myOutFile);
     }
 }
```

Il tag `XDP source` specifica il file XDP che rappresenta un documento XDP completo che può essere utilizzato come contenitore per l&#39;aggiunta di frammenti XDP o come uno dei numerosi documenti che vengono uniti in ordine. In questa situazione, il documento XDP viene utilizzato solo come contenitore (la prima illustrazione mostrata in *Assembling Multiple XDP Fragments*). Gli altri file XDP vengono quindi inseriti all&#39;interno del contenitore XDP.

Per ciascun sottomodulo, è possibile aggiungere un elemento `XDPContent` (questo elemento è facoltativo). Nell&#39;esempio precedente, si noti che esistono tre sottomoduli: `subPatientContact`, `subPatientPhysical` e `subPatientHealth`. Sia il sottomodulo `subPatientPhysical` che il sottomodulo `subPatientHealth` si trovano nello stesso file XDP, tuc018_paziente.xdp. L&#39;elemento frammento specifica il nome del sottomodulo, come definito in Designer.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere [Servizio Assembler e Riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per assemblare più frammenti XDP, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un client Assembler PDF.
1. Fare riferimento a un documento DDX esistente.
1. Fare riferimento ai documenti XDP.
1. Impostare le opzioni di esecuzione.
1. Assemblate più documenti XDP.
1. Recuperare il documento XDP assemblato.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso di classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (richiesto se  AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se  AEM Forms è distribuito su JBoss)

**Creare un client Assembler PDF**

Prima di eseguire un&#39;operazione Assembler a livello di programmazione, create un client di servizio Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare più documenti XDP è necessario fare riferimento a un documento DDX. Il documento DDX deve contenere elementi `XDP result`, `XDP source` e `XDPContent`.

**Riferimento ai documenti XDP**

Per assemblare più documenti XDP, fate riferimento a tutti i file XDP utilizzati per assemblare il documento XDP risultante. Assicurarsi che il nome del sottomodulo contenuto nel documento XDP a cui fa riferimento l&#39;attributo `source` sia specificato nell&#39;attributo `fragment`. Un sottomodulo è definito in Designer. Ad esempio, prendere in considerazione il seguente XML.

```xml
 <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
```

Il sottomodulo *subPatientContact* deve trovarsi nel file XDP denominato *tuc018_contact.xdp*.

**Impostazione delle opzioni di esecuzione**

È possibile impostare opzioni di esecuzione che controllano il comportamento del servizio Assembler mentre esegue un processo. Ad esempio, potete impostare un&#39;opzione che indichi al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore.

**Assemblare più documenti XDP**

Per assemblare più file XDP, chiamare l&#39;operazione `invokeDDX`. Il servizio Assembler restituisce il documento XDP assemblato all&#39;interno di un oggetto di raccolta.

**Recuperare il documento XDP assemblato**

Un documento XDP assemblato viene restituito all&#39;interno di un oggetto raccolta. Iterare l&#39;oggetto della raccolta e salvare il documento XDP come file XDP. È inoltre possibile trasmettere il documento XDP a un altro servizio AEM Forms , ad esempio Output.

**Consulta anche**

[Assemblare più frammenti XDP utilizzando l&#39;API Java](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-java-api)

[Assemblare più frammenti XDP utilizzando l&#39;API del servizio Web](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)

[Creazione di documenti PDF tramite frammenti](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)

## Assemblare più frammenti XDP utilizzando l&#39;API Java {#assemble-multiple-xdp-fragments-using-the-java-api}

Assemblate più frammenti XDP utilizzando l&#39;API di Assembler Service (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Assembler PDF.

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Fare riferimento a un documento DDX esistente.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file DDX.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Fare riferimento ai documenti XDP.

   * Creare un oggetto `java.util.Map` utilizzato per memorizzare i documenti XDP in input utilizzando un costruttore `HashMap`.
   * Creare un oggetto `com.adobe.idp.Document` e passare l&#39;oggetto `java.io.FileInputStream` che contiene il file XDP di input (ripetere l&#39;attività per ciascun file XDP).
   * Aggiungere una voce all&#39;oggetto `java.util.Map` richiamandone il metodo `put` e trasmettendo gli argomenti seguenti:

      * Un valore di stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento `source` specificato nel documento DDX (ripetere l&#39;attività per ciascun file XDP).
      * Un oggetto `com.adobe.idp.Document` che contiene il documento XDP che corrisponde all&#39;elemento `source` (ripetere l&#39;attività per ciascun file XDP).

1. Impostare le opzioni di esecuzione.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostate le opzioni di runtime per soddisfare i requisiti aziendali richiamando un metodo che appartiene all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per indicare al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiamare il metodo `AssemblerOptionSpec` dell&#39;oggetto `setFailOnError` e passare `false`.

1. Assemblate più documenti XDP.

   Richiamare il metodo `AssemblerServiceClient` dell&#39;oggetto `invokeDDX` e trasmettere i seguenti valori obbligatori:

   * Un oggetto `com.adobe.idp.Document` che rappresenta il documento DDX da utilizzare
   * Un oggetto `java.util.Map` che contiene i file XDP di input
   * Un oggetto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` che specifica le opzioni di esecuzione, incluso il font predefinito e il livello di registro del processo

   Il metodo `invokeDDX` restituisce un oggetto `com.adobe.livecycle.assembler.client.AssemblerResult` che contiene il documento XDP assemblato.

1. Recuperare il documento XDP assemblato.

   Per ottenere il documento XDP assemblato, eseguire le operazioni seguenti:

   * Richiamare il metodo `AssemblerResult` dell&#39;oggetto `getDocuments`. Questo metodo restituisce un oggetto `java.util.Map`.
   * Iterate l&#39;oggetto `java.util.Map` fino a individuare l&#39;oggetto `com.adobe.idp.Document` risultante.
   * Richiamare il metodo `com.adobe.idp.Document` dell&#39;oggetto `copyToFile` per estrarre il documento XDP assemblato.

**Consulta anche**

[Assemblaggio di più ](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[frammenti XDP Avvio rapido (modalità SOAP): Assemblare più frammenti XDP utilizzando Java ](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api)
[APIIncluso  ](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[file di libreria Java AEM FormsImpostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblare più frammenti XDP utilizzando l&#39;API del servizio Web {#assemble-multiple-xdp-fragments-using-the-web-service-api}

Assemblate più frammenti XDP utilizzando l&#39;API di Assembler Service (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Quando imposti un riferimento a un servizio, accertatevi di utilizzare la seguente definizione WSDL:

   ```java
    https://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server che ospita  AEM Forms.

1. Creare un client Assembler PDF.

   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `AssemblerServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passate un valore di stringa che specifica il WSDL al servizio AEM Forms , ad esempio `https://localhost:8080/soap/services/AssemblerService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `AssemblerServiceClient.Endpoint.Binding`. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39;oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente del modulo AEM al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un documento DDX esistente.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento DDX.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento DDX e la modalità in cui aprire il file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `System.IO.FileStream` dell&#39;oggetto `Read`. Passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso per la lettura.
   * Compilare l&#39;oggetto `BLOB` assegnandone la proprietà `MTOM` con il contenuto dell&#39;array di byte.

1. Fare riferimento ai documenti XDP.

   * Per ciascun file XDP di input, create un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il file di input.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file di input e la modalità in cui aprire il file.
   * Creare un array di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà `System.IO.FileStream` dell&#39;oggetto `Length`.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo `System.IO.FileStream` dell&#39;oggetto `Read`. Passare l&#39;array di byte, la posizione iniziale e la lunghezza del flusso per la lettura.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.
   * Creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Questo oggetto raccolta viene utilizzato per memorizzare i file di input necessari per creare un documento XDP assemblato.
   * Per ciascun file di input, create un oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Assegnare un valore di stringa che rappresenta il nome chiave al campo `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `key`. Questo valore deve corrispondere al valore dell&#39;elemento specificato nel documento DDX. (Eseguire questa operazione per ciascun file XDP di input.)
   * Assegnare l&#39;oggetto `BLOB` che memorizza il file di input nel campo `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `value`. (Eseguire questa operazione per ciascun file XDP di input.)
   * Aggiungere l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item` all&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Richiamare il metodo `MyMapOf_xsd_string_To_xsd_anyType` dell&#39;oggetto `Add` e passare l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Eseguire questa operazione per ciascun documento XDP di input.

1. Impostare le opzioni di esecuzione.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali assegnando un valore a un membro di dati che appartiene all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per indicare al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore, assegnare `false` al membro di dati `AssemblerOptionSpec` dell&#39;oggetto `failOnError`.

1. Assemblate più documenti XDP.

   Richiamare il metodo `AssemblerServiceClient` dell&#39;oggetto `invokeDDX` e trasmettere i seguenti valori:

   * Un oggetto `BLOB` che rappresenta il documento DDX
   * L&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType` che contiene i file richiesti
   * Un oggetto `AssemblerOptionSpec` che specifica le opzioni di esecuzione

   Il metodo `invokeDDX` restituisce un oggetto `AssemblerResult` che contiene i risultati del processo ed eventuali eccezioni.

1. Recuperare il documento XDP assemblato.

   Per ottenere il documento XDP appena creato, effettuare le seguenti operazioni:

   * Accedere al campo `documents` dell&#39;oggetto `AssemblerResult`, che è un oggetto `Map` contenente i documenti PDF risultanti.
   * Iterate l&#39;oggetto `Map` per ottenere ogni documento risultante. Quindi, proiettare l&#39;elemento `value` del membro della matrice su un elemento `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo alla proprietà `BLOB` dell&#39;oggetto `MTOM`. Questo restituisce un array di byte che è possibile scrivere in un file XDP.

**Consulta anche**

[Assemblaggio di più ](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[frammenti XDPrichiamo  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)