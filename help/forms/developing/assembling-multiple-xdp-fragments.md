---
title: Assemblaggio di più frammenti XDP
seo-title: Assemblaggio di più frammenti XDP
description: Assembla più frammenti XDP in un singolo documento XDP utilizzando l’API Java e l’API del servizio Web.
seo-description: Assembla più frammenti XDP in un singolo documento XDP utilizzando l’API Java e l’API del servizio Web.
uuid: 0e35ff85-ff40-4878-ae31-aa8da75bd3ec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c4706632-02e5-4510-ad9c-4f732d5fbdad
docset: aem65
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1909'
ht-degree: 0%

---


# Assemblaggio di più frammenti XDP{#assembling-multiple-xdp-fragments}

È possibile assemblare più frammenti XDP in un unico documento XDP. Ad esempio, si considerino frammenti XDP in cui ogni file XDP contiene uno o più sottomoduli utilizzati per creare un modulo di integrità. L&#39;illustrazione seguente mostra la vista struttura (rappresenta il file tuc018_template_flowed.xdp utilizzato in *Assembling multiple XDP fragments* quick start):

![am_am_forma](assets/am_am_forma.png)

La figura seguente mostra la sezione paziente (rappresenta il file tuc018_contact.xdp utilizzato nel *assemblaggio di più frammenti XDP* avvio rapido):

![am_am_formb](assets/am_am_formb.png)

L&#39;illustrazione seguente mostra la sezione salute paziente (rappresenta il file tuc018_paziente.xdp utilizzato nel *assemblaggio di più frammenti XDP* avvio rapido):

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

Il documento DDX contiene un tag XDP `result` che specifica il nome del risultato. In questa situazione, il valore è `tuc018result.xdp`. Questo valore è riportato nella logica dell&#39;applicazione utilizzata per recuperare il documento XDP dopo che il servizio Assembler restituisce il risultato. Ad esempio, considera la seguente logica di applicazione Java utilizzata per recuperare il documento XDP assemblato (notare che il valore è bloccato):

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

Il tag `XDP source` specifica il file XDP che rappresenta un documento XDP completo che può essere utilizzato come contenitore per aggiungere frammenti XDP o come uno dei vari documenti che vengono aggiunti insieme in ordine. In questa situazione, il documento XDP viene utilizzato solo come contenitore (la prima illustrazione mostrata in *Assembling Multiple XDP Fragments*). In altre parole, gli altri file XDP vengono inseriti all’interno del contenitore XDP.

Per ciascun sottomodulo, è possibile aggiungere un elemento `XDPContent` (questo elemento è facoltativo). Nell’esempio precedente, si noti che sono presenti tre sottomoduli: `subPatientContact`, `subPatientPhysical` e `subPatientHealth`. Sia il sottomodulo `subPatientPhysical` che il sottomodulo `subPatientHealth` si trovano nello stesso file XDP, tuc018_paziente.xdp. L’elemento frammento specifica il nome del sottomodulo, come definito in Designer.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere [Servizio Assembler e Riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per assemblare più frammenti XDP, esegui le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client Assembler PDF.
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

**Creare un client Assembler PDF**

Prima di eseguire un&#39;operazione Assembler a livello di programmazione, creare un client di servizio Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare più documenti XDP è necessario fare riferimento a un documento DDX. Il documento DDX deve contenere elementi `XDP result`, `XDP source` e `XDPContent`.

**Riferimento ai documenti XDP**

Per assemblare più documenti XDP, fare riferimento a tutti i file XDP utilizzati per assemblare il documento XDP risultante. Assicurarsi che il nome del sottomodulo contenuto nel documento XDP a cui fa riferimento l&#39;attributo `source` sia specificato nell&#39;attributo `fragment`. Un sottomodulo è definito in Designer. Ad esempio, considerare il seguente XML.

```xml
 <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
```

Il sottomodulo *subPatientContact* deve trovarsi nel file XDP denominato *tuc018_contact.xdp*.

**Impostare le opzioni di esecuzione**

È possibile impostare le opzioni di esecuzione che controllano il comportamento del servizio Assembler mentre esegue un processo. Ad esempio, è possibile impostare un&#39;opzione che indica al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore.

**Assemblare i più documenti XDP**

Per assemblare più file XDP, chiama l&#39;operazione `invokeDDX`. Il servizio Assembler restituisce il documento XDP assemblato all&#39;interno di un oggetto raccolta.

**Recupera il documento XDP assemblato**

All&#39;interno di un oggetto raccolta viene restituito un documento XDP assemblato. Itera attraverso l&#39;oggetto di raccolta e salva il documento XDP come file XDP. È inoltre possibile passare il documento XDP a un altro servizio AEM Forms, ad esempio Output.

**Consulta anche**

[Assemblare più frammenti XDP utilizzando l’API Java](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-java-api)

[Assemblare più frammenti XDP utilizzando l’API del servizio Web](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio programmatico di documenti PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)

[Creazione di documenti PDF tramite frammenti](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)

## Assemblare più frammenti XDP utilizzando l&#39;API Java {#assemble-multiple-xdp-fragments-using-the-java-api}

Assemblare più frammenti XDP utilizzando l&#39;API del servizio Assembler (Java):

1. Includi file di progetto.

   Includi file JAR client, come adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client Assembler PDF.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Fai riferimento a un documento DDX esistente.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore di stringa che specifica la posizione del file DDX.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Fai riferimento ai documenti XDP.

   * Creare un oggetto `java.util.Map` utilizzato per memorizzare i documenti XDP di input utilizzando un costruttore `HashMap`.
   * Crea un oggetto `com.adobe.idp.Document` e passa l&#39;oggetto `java.io.FileInputStream` che contiene il file XDP di input (ripeti questa attività per ogni file XDP).
   * Aggiungere una voce all&#39;oggetto `java.util.Map` richiamando il relativo metodo `put` e passando i seguenti argomenti:

      * Valore stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento `source` specificato nel documento DDX (ripeti questa attività per ogni file XDP).
      * Un oggetto `com.adobe.idp.Document` contenente il documento XDP che corrisponde all&#39;elemento `source` (ripeti questa attività per ogni file XDP).

1. Impostare le opzioni di esecuzione.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di esecuzione per soddisfare i requisiti aziendali richiamando un metodo appartenente all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per dare istruzioni al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiamare il metodo `setFailOnError` dell&#39;oggetto `AssemblerOptionSpec` e passare `false`.

1. Assembla i documenti XDP multipli.

   Richiama il metodo `invokeDDX` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori obbligatori:

   * Un oggetto `com.adobe.idp.Document` che rappresenta il documento DDX da utilizzare
   * Un oggetto `java.util.Map` che contiene i file XDP di input
   * Un oggetto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` che specifica le opzioni di esecuzione, incluso il font predefinito e il livello di log del processo

   Il metodo `invokeDDX` restituisce un oggetto `com.adobe.livecycle.assembler.client.AssemblerResult` contenente il documento XDP assemblato.

1. Recupera il documento XDP assemblato.

   Per ottenere il documento XDP assemblato, eseguire le operazioni seguenti:

   * Richiama il metodo `getDocuments` dell&#39;oggetto `AssemblerResult`. Questo metodo restituisce un oggetto `java.util.Map`.
   * Iterare l&#39;oggetto `java.util.Map` fino a trovare l&#39;oggetto `com.adobe.idp.Document` risultante.
   * Richiamare il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per estrarre il documento XDP assemblato.

**Consulta anche**

[Assemblaggio di più ](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[frammenti XDP Avvio rapido (modalità SOAP): Assemblaggio di più frammenti XDP utilizzando Java ](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api)
[APIInclusi ](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[file libreria Java AEM FormsImpostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblare più frammenti XDP utilizzando l&#39;API del servizio Web {#assemble-multiple-xdp-fragments-using-the-web-service-api}

Assemblare più frammenti XDP utilizzando l&#39;API del servizio Assembler (servizio Web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Quando imposti un riferimento a un servizio, assicurati di utilizzare la seguente definizione WSDL:

   ```java
    https://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client Assembler PDF.

   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `AssemblerServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms, ad esempio `https://localhost:8080/soap/services/AssemblerService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version` . Questo attributo viene utilizzato quando si crea un riferimento a un servizio.
   * Crea un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `AssemblerServiceClient.Endpoint.Binding` . Imposta il valore restituito su `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegna il nome utente del modulo di AEM al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName` .
      * Assegna il valore della password corrispondente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Assegna il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegna il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fai riferimento a un documento DDX esistente.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il documento DDX.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file del documento DDX e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream`. Passa la matrice byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando la relativa proprietà `MTOM` con il contenuto dell&#39;array di byte.

1. Fai riferimento ai documenti XDP.

   * Per ogni file XDP di input, creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il file di input.
   * Creare un oggetto `System.IO.FileStream` richiamando il relativo costruttore e passando un valore di stringa che rappresenta la posizione del file di input e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni dell&#39;array di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare l’array di byte con i dati del flusso richiamando il metodo `Read` dell’oggetto `System.IO.FileStream`. Passa la matrice byte, la posizione iniziale e la lunghezza del flusso da leggere.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` con il contenuto dell&#39;array di byte.
   * Creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Questo oggetto raccolta viene utilizzato per memorizzare i file di input necessari per creare un documento XDP assemblato.
   * Per ciascun file di input, creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Assegna un valore stringa che rappresenta il nome della chiave al campo `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `key`. Questo valore deve corrispondere al valore dell&#39;elemento specificato nel documento DDX. (Esegui questa operazione per ogni file XDP di input.)
   * Assegna l&#39;oggetto `BLOB` che memorizza il file di input nel campo `MyMapOf_xsd_string_To_xsd_anyType_Item` dell&#39;oggetto `value`. (Esegui questa operazione per ogni file XDP di input.)
   * Aggiungere l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item` all&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Richiama il metodo `Add` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType` e passa l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType`. (Esegui questa operazione per ogni documento XDP di input.)

1. Impostare le opzioni di esecuzione.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di esecuzione utilizzando il relativo costruttore.
   * Impostare le opzioni di esecuzione per soddisfare i requisiti aziendali assegnando un valore a un membro dati appartenente all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per dare istruzioni al servizio Assembler di continuare a elaborare un processo in caso di errore, assegna `false` al membro dati `AssemblerOptionSpec` dell&#39;oggetto `failOnError`.

1. Assembla i documenti XDP multipli.

   Richiama il metodo `invokeDDX` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori:

   * Un oggetto `BLOB` che rappresenta il documento DDX
   * L&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType` che contiene i file richiesti
   * Un oggetto `AssemblerOptionSpec` che specifica le opzioni di esecuzione

   Il metodo `invokeDDX` restituisce un oggetto `AssemblerResult` contenente i risultati del processo ed eventuali eccezioni.

1. Recupera il documento XDP assemblato.

   Per ottenere il documento XDP appena creato, esegui le seguenti operazioni:

   * Accedere al campo `documents` dell&#39;oggetto `AssemblerResult`, che è un oggetto `Map` che contiene i documenti PDF risultanti.
   * Iterare attraverso l&#39;oggetto `Map` per ottenere ogni documento risultante. Quindi, eseguire il cast di `value` del membro della matrice su un `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo alla proprietà `MTOM` dell’oggetto `BLOB` corrispondente. Restituisce una matrice di byte che è possibile scrivere in un file XDP.

**Consulta anche**

[Assemblaggio di più ](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[frammenti XDPrichiamo di AEM Forms utilizzando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)