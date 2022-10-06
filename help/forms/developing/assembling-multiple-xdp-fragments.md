---
title: Assemblaggio di più frammenti XDP
seo-title: Assembling Multiple XDP Fragments
description: Assembla più frammenti XDP in un singolo documento XDP utilizzando l’API Java e l’API del servizio Web.
seo-description: Assemble multiple XDP fragments into a single XDP document using the Java API and Web Service API.
uuid: 0e35ff85-ff40-4878-ae31-aa8da75bd3ec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c4706632-02e5-4510-ad9c-4f732d5fbdad
docset: aem65
role: Developer
exl-id: 54d98c69-2b2e-46cb-9f6a-7e9bdbe5c378
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1887'
ht-degree: 0%

---

# Assemblaggio di più frammenti XDP{#assembling-multiple-xdp-fragments}

È possibile assemblare più frammenti XDP in un unico documento XDP. Ad esempio, si considerino frammenti XDP in cui ogni file XDP contiene uno o più sottomoduli utilizzati per creare un modulo di integrità. La figura seguente mostra la vista struttura (rappresenta il file tuc018_template_flowed.xdp utilizzato nel *Assemblaggio di più frammenti XDP* avvio rapido):

![am_am_forma](assets/am_am_forma.png)

La figura seguente mostra la sezione paziente (rappresenta il file tuc018_contact.xdp utilizzato nel *Assemblaggio di più frammenti XDP* avvio rapido):

![am_am_formb](assets/am_am_formb.png)

La figura seguente mostra la sezione salute paziente (rappresenta il file tuc018_paziente.xdp utilizzato nel *Assemblaggio di più frammenti XDP* avvio rapido):

![am_am_formc](assets/am_am_formc.png)

Questo frammento contiene due sottomoduli denominati *subPatientPhysical* e *subPatientHealth*. Entrambi i sottomoduli sono indicati nel documento DDX passato al servizio Assembler. Utilizzando il servizio Assembler, è possibile combinare tutti questi frammenti XDP in un unico documento XDP, come illustrato nella figura seguente.

![am_am_formd](assets/am_am_formd.png)

Il seguente documento DDX assembla più frammenti XDP in un documento XDP.

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

Il documento DDX contiene un file XDP `result` che specifica il nome del risultato. In questa situazione, il valore è `tuc018result.xdp`. Questo valore è riportato nella logica dell&#39;applicazione utilizzata per recuperare il documento XDP dopo che il servizio Assembler restituisce il risultato. Ad esempio, considera la seguente logica di applicazione Java utilizzata per recuperare il documento XDP assemblato (notare che il valore è bloccato):

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

La `XDP source` tag specifica il file XDP che rappresenta un documento XDP completo che può essere utilizzato come contenitore per aggiungere frammenti XDP o come uno dei vari documenti che vengono aggiunti insieme in ordine. In questa situazione, il documento XDP viene utilizzato solo come contenitore (la prima illustrazione mostrata in *Assemblaggio di più frammenti XDP*). In altre parole, gli altri file XDP vengono inseriti all’interno del contenitore XDP.

Per ciascun sottomodulo è possibile aggiungere un `XDPContent` (questo elemento è facoltativo). Nell’esempio precedente, si noti che sono presenti tre sottomoduli: `subPatientContact`, `subPatientPhysical`e `subPatientHealth`. Entrambi i `subPatientPhysical` sottomodulo e `subPatientHealth` i sottomoduli si trovano nello stesso file XDP, tuc018_paziente.xdp. L’elemento frammento specifica il nome del sottomodulo, come definito in Designer.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, consulta [Servizio di assemblaggio e riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per assemblare più frammenti XDP, esegui le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client PDF Assembler.
1. Fai riferimento a un documento DDX esistente.
1. Fai riferimento ai documenti XDP.
1. Impostare le opzioni di esecuzione.
1. Assembla i documenti XDP multipli.
1. Recupera il documento XDP assemblato.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è distribuito su JBoss)
* jbossall-client.jar (richiesto se AEM Forms è distribuito su JBoss)

**Creare un client PDF Assembler**

Prima di eseguire un&#39;operazione Assembler a livello di programmazione, creare un client di servizio Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare più documenti XDP è necessario fare riferimento a un documento DDX. Il documento DDX deve contenere `XDP result`, `XDP source`e `XDPContent` elementi.

**Riferimento ai documenti XDP**

Per assemblare più documenti XDP, fare riferimento a tutti i file XDP utilizzati per assemblare il documento XDP risultante. Assicurarsi che il nome del sottomodulo contenuto nel documento XDP a cui fa riferimento il `source` è specificato nel `fragment` attributo. Un sottomodulo è definito in Designer. Ad esempio, considerare il seguente XML.

```xml
 <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
```

Il sottomodulo denominato *subPatientContact* deve trovarsi nel file XDP denominato *tuc018_contact.xdp*.

**Impostare le opzioni di esecuzione**

È possibile impostare le opzioni di esecuzione che controllano il comportamento del servizio Assembler mentre esegue un processo. Ad esempio, è possibile impostare un&#39;opzione che indica al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore.

**Assemblare i più documenti XDP**

Per assemblare più file XDP, chiama il `invokeDDX` funzionamento. Il servizio Assembler restituisce il documento XDP assemblato all&#39;interno di un oggetto raccolta.

**Recupera il documento XDP assemblato**

All&#39;interno di un oggetto raccolta viene restituito un documento XDP assemblato. Itera attraverso l&#39;oggetto di raccolta e salva il documento XDP come file XDP. È inoltre possibile passare il documento XDP a un altro servizio AEM Forms, ad esempio Output.

**Consulta anche**

[Assemblare più frammenti XDP utilizzando l’API Java](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-java-api)

[Assemblare più frammenti XDP utilizzando l’API del servizio Web](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)

[Creazione di documenti PDF tramite frammenti](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)

## Assemblare più frammenti XDP utilizzando l’API Java {#assemble-multiple-xdp-fragments-using-the-java-api}

Assemblare più frammenti XDP utilizzando l&#39;API del servizio Assembler (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDF Assembler.

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `AssemblerServiceClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Fai riferimento a un documento DDX esistente.

   * Crea un `java.io.FileInputStream` oggetto che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file DDX.
   * Crea un `com.adobe.idp.Document` utilizzando il relativo costruttore e passando `java.io.FileInputStream` oggetto.

1. Fai riferimento ai documenti XDP.

   * Crea un `java.util.Map` oggetto utilizzato per memorizzare i documenti XDP di input utilizzando un `HashMap` costruttore.
   * Crea un `com.adobe.idp.Document` e passare `java.io.FileInputStream` oggetto che contiene il file XDP di input (ripetere questa attività per ogni file XDP).
   * Aggiungi una voce al `java.util.Map` richiamandone l&#39;oggetto `put` e passare gli argomenti seguenti:

      * Valore stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al `source` valore dell&#39;elemento specificato nel documento DDX (ripetere questa attività per ogni file XDP).
      * A `com.adobe.idp.Document` oggetto contenente il documento XDP corrispondente al `source` (ripeti questa attività per ogni file XDP).

1. Impostare le opzioni di esecuzione.

   * Crea un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di esecuzione per soddisfare i requisiti aziendali richiamando un metodo che appartiene al `AssemblerOptionSpec` oggetto. Ad esempio, per dare istruzioni al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiama il `AssemblerOptionSpec` dell’oggetto `setFailOnError` metodo e passaggio `false`.

1. Assembla i documenti XDP multipli.

   Richiama il `AssemblerServiceClient` dell’oggetto `invokeDDX` e trasmettere i seguenti valori richiesti:

   * A `com.adobe.idp.Document` oggetto che rappresenta il documento DDX da utilizzare
   * A `java.util.Map` oggetto che contiene i file XDP di input
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione, incluso il carattere predefinito e il livello del registro di lavoro

   La `invokeDDX` restituisce un `com.adobe.livecycle.assembler.client.AssemblerResult` oggetto contenente il documento XDP assemblato.

1. Recupera il documento XDP assemblato.

   Per ottenere il documento XDP assemblato, eseguire le operazioni seguenti:

   * Richiama il `AssemblerResult` dell’oggetto `getDocuments` metodo . Questo metodo restituisce un `java.util.Map` oggetto.
   * Itera attraverso il `java.util.Map` finché non trovi il risultato `com.adobe.idp.Document` oggetto.
   * Richiama il `com.adobe.idp.Document` dell’oggetto `copyToFile` metodo per estrarre il documento XDP assemblato.

**Consulta anche**

[Assemblaggio di più frammenti XDP](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[Avvio rapido (modalità SOAP): Assemblaggio di più frammenti XDP utilizzando l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api)
[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblare più frammenti XDP utilizzando l’API del servizio Web {#assemble-multiple-xdp-fragments-using-the-web-service-api}

Assemblare più frammenti XDP utilizzando l&#39;API del servizio Assembler (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Quando imposti un riferimento a un servizio, assicurati di utilizzare la seguente definizione WSDL:

   ```java
    https://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   >[!NOTE]
   >
   >Sostituisci `localhost` con l’indirizzo IP del server che ospita AEM Forms.

1. Creare un client PDF Assembler.

   * Crea un `AssemblerServiceClient` utilizzando il relativo costruttore predefinito.
   * Crea un `AssemblerServiceClient.Endpoint.Address` utilizzando `System.ServiceModel.EndpointAddress` costruttore. Passa un valore stringa che specifica il WSDL al servizio AEM Forms, ad esempio `https://localhost:8080/soap/services/AssemblerService?blob=mtom`). Non è necessario utilizzare il `lc_version` attributo. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.
   * Crea un `System.ServiceModel.BasicHttpBinding` ottenendo il valore del `AssemblerServiceClient.Endpoint.Binding` campo . Imposta il valore restituito su `BasicHttpBinding`.
   * Imposta la `System.ServiceModel.BasicHttpBinding` dell’oggetto `MessageEncoding` campo a `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli di AEM al `AssemblerServiceClient.ClientCredentials.UserName.UserName` campo .
      * Assegna il valore della password corrispondente al `AssemblerServiceClient.ClientCredentials.UserName.Password`campo .
      * Assegna `HttpClientCredentialType.Basic` valore costante nel `BasicHttpBindingSecurity.Transport.ClientCredentialType`campo .
      * Assegna `BasicHttpSecurityMode.TransportCredentialOnly` valore costante nel `BasicHttpBindingSecurity.Security.Mode`campo .

1. Fai riferimento a un documento DDX esistente.

   * Crea un `BLOB` utilizzando il relativo costruttore. La `BLOB` viene utilizzato per memorizzare il documento DDX.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento DDX e la modalità in cui aprire il file.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` metodo . Passa la matrice byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto dell&#39;array di byte.

1. Fai riferimento ai documenti XDP.

   * Per ogni file XDP di input, crea un `BLOB` utilizzando il relativo costruttore. La `BLOB` viene utilizzato per memorizzare il file di input.
   * Crea un `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file di input e la modalità di apertura del file.
   * Creare un array di byte che memorizza il contenuto del `System.IO.FileStream` oggetto. È possibile determinare le dimensioni dell&#39;array di byte ottenendo il `System.IO.FileStream` dell’oggetto `Length` proprietà.
   * Compilare l&#39;array di byte con i dati del flusso richiamando il `System.IO.FileStream` dell’oggetto `Read` metodo . Passa la matrice byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Popolare `BLOB` oggetto assegnando il relativo `MTOM` con il contenuto dell&#39;array di byte.
   * Crea un `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Questo oggetto raccolta viene utilizzato per memorizzare i file di input necessari per creare un documento XDP assemblato.
   * Per ogni file di input, crea un `MyMapOf_xsd_string_To_xsd_anyType_Item` oggetto.
   * Assegna un valore stringa che rappresenta il nome della chiave al `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `key` campo . Questo valore deve corrispondere al valore dell&#39;elemento specificato nel documento DDX. (Esegui questa operazione per ogni file XDP di input.)
   * Assegna `BLOB` oggetto che memorizza il file di input nel `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `value` campo . (Esegui questa operazione per ogni file XDP di input.)
   * Aggiungi il `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType` oggetto. Richiama il `MyMapOf_xsd_string_To_xsd_anyType` dell&#39;oggetto `Add` e passare il `MyMapOf_xsd_string_To_xsd_anyType` oggetto. (Esegui questa operazione per ogni documento XDP di input.)

1. Impostare le opzioni di esecuzione.

   * Crea un `AssemblerOptionSpec` oggetto che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di esecuzione per soddisfare i requisiti aziendali assegnando un valore a un membro dati che appartiene al `AssemblerOptionSpec` oggetto. Ad esempio, per dare istruzioni al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, assegnare `false` al `AssemblerOptionSpec` dell’oggetto `failOnError` membro dati.

1. Assembla i documenti XDP multipli.

   Richiama il `AssemblerServiceClient` dell’oggetto `invokeDDX` e passare i seguenti valori:

   * A `BLOB` oggetto che rappresenta il documento DDX
   * La `MyMapOf_xsd_string_To_xsd_anyType` oggetto contenente i file richiesti
   * Un `AssemblerOptionSpec` oggetto che specifica le opzioni di esecuzione

   La `invokeDDX` restituisce un `AssemblerResult` oggetto contenente i risultati del processo ed eventuali eccezioni.

1. Recupera il documento XDP assemblato.

   Per ottenere il documento XDP appena creato, esegui le seguenti operazioni:

   * Accedere al `AssemblerResult` dell’oggetto `documents` un campo `Map` oggetto contenente i documenti PDF risultanti.
   * Itera attraverso il `Map` per ottenere ogni documento risultante. Quindi, eseguire il cast del membro dell&#39;array `value` a `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo ai relativi `BLOB` dell’oggetto `MTOM` proprietà. Restituisce una matrice di byte che è possibile scrivere in un file XDP.

**Consulta anche**

[Assemblaggio di più frammenti XDP](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
