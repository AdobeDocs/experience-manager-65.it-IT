---
title: Assemblare Più Frammenti XDP
seo-title: Assemblare Più Frammenti XDP
description: 'null'
seo-description: 'null'
uuid: 0e35ff85-ff40-4878-ae31-aa8da75bd3ec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c4706632-02e5-4510-ad9c-4f732d5fbdad
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1876'
ht-degree: 0%

---


# Assemblare Più Frammenti XDP{#assembling-multiple-xdp-fragments}

È possibile assemblare più frammenti XDP in un unico documento XDP. Si consideri ad esempio i frammenti XDP in cui ogni file XDP contiene uno o più sottomoduli utilizzati per creare un modulo di integrità. L&#39;illustrazione seguente mostra la visualizzazione struttura (rappresenta il file tuc018_template_flowed.xdp utilizzato nell&#39;avvio rapido per l&#39; *assemblaggio di più frammenti* XDP):

![am_am_forma](assets/am_am_forma.png)

L&#39;illustrazione seguente mostra la sezione paziente (rappresenta il file tuc018_contact.xdp utilizzato nell&#39;avvio rapido per l&#39; *assemblaggio di più frammenti* XDP):

![am_am_formb](assets/am_am_formb.png)

L&#39;illustrazione seguente mostra la sezione relativa allo stato del paziente (rappresenta il file tuc018_paziente.xdp utilizzato nell&#39;avvio rapido *Assembling multiple XDP fragments* ):

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

Il documento DDX contiene un `result` tag XDP che specifica il nome del risultato. In questa situazione, il valore è `tuc018result.xdp`. A questo valore viene fatto riferimento nella logica dell&#39;applicazione utilizzata per recuperare il documento XDP dopo che il servizio Assembler restituisce il risultato. Si consideri, ad esempio, la seguente logica di applicazione Java utilizzata per recuperare il documento XDP assemblato (notare che il valore è bloccato):

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

Il `XDP source` tag specifica il file XDP che rappresenta un documento XDP completo che può essere utilizzato come contenitore per l&#39;aggiunta di frammenti XDP o come uno dei numerosi documenti che vengono uniti in ordine. In questa situazione, il documento XDP viene utilizzato solo come contenitore (la prima illustrazione mostrata in *Assemblaggio di più frammenti* XDP). Gli altri file XDP vengono quindi inseriti all&#39;interno del contenitore XDP.

Per ciascun sottomodulo, è possibile aggiungere un `XDPContent` elemento (questo elemento è facoltativo). Nell&#39;esempio precedente, si noti che esistono tre sottomoduli: `subPatientContact`, `subPatientPhysical`e `subPatientHealth`. Sia il `subPatientPhysical` sottomodulo che il `subPatientHealth` sottomodulo si trovano nello stesso file XDP, tuc018_paziente.xdp. L&#39;elemento frammento specifica il nome del sottomodulo, come definito in Designer.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere Riferimento [servizi per i AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere Servizio [Assembler e Riferimento](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

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
* adobe-utilities.jar (richiesto se i AEM Forms sono distribuiti su JBoss)
* jbossall-client.jar (richiesto se i AEM Forms sono distribuiti su JBoss)

**Creare un client Assembler PDF**

Prima di eseguire un&#39;operazione Assembler a livello di programmazione, create un client di servizio Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare più documenti XDP è necessario fare riferimento a un documento DDX. Questo documento DDX deve contenere `XDP result`, `XDP source`e `XDPContent` elementi.

**Riferimento ai documenti XDP**

Per assemblare più documenti XDP, fate riferimento a tutti i file XDP utilizzati per assemblare il documento XDP risultante. Assicurarsi che il nome del sottomodulo contenuto nel documento XDP a cui fa riferimento l&#39; `source` attributo sia specificato nell&#39; `fragment` attributo. Un sottomodulo è definito in Designer. Ad esempio, prendere in considerazione il seguente XML.

```xml
 <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
```

Il sottomodulo *subPatientContact* deve trovarsi nel file XDP denominato *tuc018_contact.xdp*.

**Impostazione delle opzioni di esecuzione**

È possibile impostare opzioni di esecuzione che controllano il comportamento del servizio Assembler mentre esegue un processo. Ad esempio, potete impostare un&#39;opzione che indichi al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore.

**Assemblare più documenti XDP**

Per assemblare più file XDP, chiamate l&#39; `invokeDDX` operazione. Il servizio Assembler restituisce il documento XDP assemblato all&#39;interno di un oggetto di raccolta.

**Recuperare il documento XDP assemblato**

Un documento XDP assemblato viene restituito all&#39;interno di un oggetto raccolta. Iterare l&#39;oggetto della raccolta e salvare il documento XDP come file XDP. È inoltre possibile trasmettere il documento XDP a un altro servizio AEM Forms, ad esempio Output.

**Consulta anche**

[Assemblare più frammenti XDP utilizzando l&#39;API Java](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-java-api)

[Assemblare più frammenti XDP utilizzando l&#39;API del servizio Web](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)

[Creazione di documenti PDF tramite frammenti](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)

## Assemblare più frammenti XDP utilizzando l&#39;API Java {#assemble-multiple-xdp-fragments-using-the-java-api}

Assemblate più frammenti XDP utilizzando l&#39;API di Assembler Service (Java):

1. Includere i file di progetto.

   Includete file JAR client, ad esempio adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Assembler PDF.

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `AssemblerServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Fare riferimento a un documento DDX esistente.

   * Creare un `java.io.FileInputStream` oggetto che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file DDX.
   * Creare un `com.adobe.idp.Document` oggetto utilizzando il relativo costruttore e passando l&#39; `java.io.FileInputStream` oggetto.

1. Fare riferimento ai documenti XDP.

   * Creare un oggetto `java.util.Map` utilizzato per memorizzare i documenti XDP in input utilizzando un `HashMap` costruttore.
   * Creare un `com.adobe.idp.Document` oggetto e passare l&#39; `java.io.FileInputStream` oggetto che contiene il file XDP di input (ripetere l&#39;attività per ciascun file XDP).
   * Aggiungere una voce all&#39; `java.util.Map` oggetto richiamandone il `put` metodo e passando gli argomenti seguenti:

      * Un valore di stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore `source` dell&#39;elemento specificato nel documento DDX (ripetere l&#39;attività per ciascun file XDP).
      * Un `com.adobe.idp.Document` oggetto che contiene il documento XDP che corrisponde all&#39; `source` elemento (ripetere l&#39;attività per ciascun file XDP).

1. Impostare le opzioni di esecuzione.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostate le opzioni di runtime per soddisfare i requisiti aziendali richiamando un metodo che appartiene all&#39; `AssemblerOptionSpec` oggetto. Ad esempio, per indicare al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiamare il metodo dell&#39; `AssemblerOptionSpec` oggetto `setFailOnError` e passare `false`.

1. Assemblate più documenti XDP.

   Richiamare il metodo dell&#39; `AssemblerServiceClient` oggetto `invokeDDX` e trasmettere i seguenti valori obbligatori:

   * Un `com.adobe.idp.Document` oggetto che rappresenta il documento DDX da utilizzare
   * Un `java.util.Map` oggetto che contiene i file XDP di input
   * Un `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione, incluso il font predefinito e il livello di registro del processo

   Il `invokeDDX` metodo restituisce un `com.adobe.livecycle.assembler.client.AssemblerResult` oggetto che contiene il documento XDP assemblato.

1. Recuperare il documento XDP assemblato.

   Per ottenere il documento XDP assemblato, eseguire le operazioni seguenti:

   * Richiama il metodo dell’ `AssemblerResult` oggetto `getDocuments` . Questo metodo restituisce un `java.util.Map` oggetto.
   * Eseguire un&#39;iterazione sull&#39; `java.util.Map` oggetto fino a individuare l&#39; `com.adobe.idp.Document` oggetto risultante.
   * Richiamare il metodo dell&#39; `com.adobe.idp.Document` oggetto `copyToFile` per estrarre il documento XDP assemblato.

**Consulta anche**

[Assemblaggio di più frammenti](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)XDP Avvio[rapido (modalità SOAP): Assemblare più frammenti XDP utilizzando l&#39;API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api)Java[Inclusi i file](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)libreria Java AEM Forms[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblare più frammenti XDP utilizzando l&#39;API del servizio Web {#assemble-multiple-xdp-fragments-using-the-web-service-api}

Assemblate più frammenti XDP utilizzando l&#39;API di Assembler Service (servizio Web):

1. Includere i file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Quando imposti un riferimento a un servizio, accertatevi di utilizzare la seguente definizione WSDL:

   ```java
    https://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   >[!NOTE]
   >
   >Sostituire `localhost` con l&#39;indirizzo IP del server host AEM Forms.

1. Creare un client Assembler PDF.

   * Creare un `AssemblerServiceClient` oggetto utilizzando il relativo costruttore predefinito.
   * Creare un `AssemblerServiceClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms, ad esempio `https://localhost:8080/soap/services/AssemblerService?blob=mtom`). Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio.
   * Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del `AssemblerServiceClient.Endpoint.Binding` campo. Inserite il valore restituito in `BasicHttpBinding`.
   * Impostare il campo `System.ServiceModel.BasicHttpBinding` dell&#39; `MessageEncoding` oggetto su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

      * Assegnare il nome utente dei moduli AEM al `AssemblerServiceClient.ClientCredentials.UserName.UserName` campo.
      * Assegnare il valore della password corrispondente al `AssemblerServiceClient.ClientCredentials.UserName.Password`campo.
      * Assegnare il valore `HttpClientCredentialType.Basic` costante al `BasicHttpBindingSecurity.Transport.ClientCredentialType`campo.
      * Assegnare il valore `BasicHttpSecurityMode.TransportCredentialOnly` costante al `BasicHttpBindingSecurity.Security.Mode`campo.

1. Fare riferimento a un documento DDX esistente.

   * Creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare il documento DDX.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento DDX e la modalità in cui aprire il file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo dell&#39; `System.IO.FileStream` oggetto `Read` . Trasmettere l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` la proprietà con il contenuto dell&#39;array di byte.

1. Fare riferimento ai documenti XDP.

   * Per ciascun file XDP di input, creare un `BLOB` oggetto utilizzando il relativo costruttore. L&#39; `BLOB` oggetto viene utilizzato per memorizzare il file di input.
   * Creare un `System.IO.FileStream` oggetto richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file di input e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto dell&#39; `System.IO.FileStream` oggetto. È possibile determinare la dimensione dell&#39;array di byte ottenendo la proprietà dell&#39; `System.IO.FileStream` oggetto `Length` .
   * Compilare l&#39;array di byte con i dati del flusso richiamando il metodo dell&#39; `System.IO.FileStream` oggetto `Read` . Trasmettere l&#39;array di byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39; `BLOB` oggetto assegnandone `MTOM` il campo con il contenuto dell&#39;array di byte.
   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. Questo oggetto raccolta viene utilizzato per memorizzare i file di input necessari per creare un documento XDP assemblato.
   * Per ciascun file di input, creare un `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto.
   * Assegnare un valore di stringa che rappresenta il nome chiave al campo dell&#39; `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto `key` . Questo valore deve corrispondere al valore dell&#39;elemento specificato nel documento DDX. (Eseguire questa operazione per ciascun file XDP di input.)
   * Assegnare l&#39; `BLOB` oggetto che memorizza il file di input al `MyMapOf_xsd_string_To_xsd_anyType_Item` campo dell&#39; `value` oggetto. (Eseguire questa operazione per ciascun file XDP di input.)
   * Aggiungere l&#39; `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto all&#39; `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Richiamare il `MyMapOf_xsd_string_To_xsd_anyType` metodo dell&#39;oggetto `Add` e passare l&#39; `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Eseguire questa operazione per ciascun documento XDP di input.

1. Impostare le opzioni di esecuzione.

   * Creare un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali assegnando un valore a un membro di dati che appartiene all&#39; `AssemblerOptionSpec` oggetto. Ad esempio, per indicare al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore, assegnare `false` al membro `AssemblerOptionSpec` dati dell&#39; `failOnError` oggetto.

1. Assemblate più documenti XDP.

   Richiama il metodo dell’ `AssemblerServiceClient` oggetto `invokeDDX` e passa i seguenti valori:

   * Un `BLOB` oggetto che rappresenta il documento DDX
   * L&#39; `MyMapOf_xsd_string_To_xsd_anyType` oggetto che contiene i file richiesti
   * Un oggetto `AssemblerOptionSpec` che specifica le opzioni di esecuzione

   Il `invokeDDX` metodo restituisce un `AssemblerResult` oggetto che contiene i risultati del processo ed eventuali eccezioni.

1. Recuperare il documento XDP assemblato.

   Per ottenere il documento XDP appena creato, effettuare le seguenti operazioni:

   * Accedere al campo `AssemblerResult` dell&#39; `documents` oggetto, ovvero un `Map` oggetto che contiene i documenti PDF risultanti.
   * Eseguire un&#39;iterazione sull&#39; `Map` oggetto per ottenere ogni documento risultante. Quindi, inserite il membro dell&#39;array `value` in un `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo alla `BLOB` proprietà dell&#39; `MTOM` oggetto. Questo restituisce un array di byte che è possibile scrivere in un file XDP.

**Consulta anche**

[Assemblaggio di più frammenti](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)[di chiamata XDP mediante MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)