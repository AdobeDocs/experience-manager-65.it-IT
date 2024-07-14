---
title: Assemblaggio di più frammenti XDP
description: Assembla più frammenti XDP in un singolo documento XDP utilizzando l’API Java e l’API del servizio web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
docset: aem65
role: Developer
exl-id: 54d98c69-2b2e-46cb-9f6a-7e9bdbe5c378
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1859'
ht-degree: 0%

---

# Assemblaggio di più frammenti XDP{#assembling-multiple-xdp-fragments}

È possibile assemblare più frammenti XDP in un unico documento XDP. Ad esempio, considera i frammenti XDP in cui ogni file XDP contiene uno o più sottomoduli utilizzati per creare un modulo di integrità. La figura seguente mostra la visualizzazione struttura (rappresenta il file tuc018_template_flowed.xdp utilizzato in *Assemblaggio di più frammenti XDP* con avvio rapido):

![am_am_forma](assets/am_am_forma.png)

La figura seguente mostra la sezione paziente (rappresenta il file tuc018_contact.xdp utilizzato in *Assemblaggio di più frammenti XDP* con avvio rapido):

![am_formb](assets/am_am_formb.png)

La figura seguente mostra la sezione relativa allo stato di salute del paziente (rappresenta il file tuc018_patient.xdp utilizzato nella *Guida introduttiva all&#39;assemblaggio di più frammenti XDP*):

![am_formc](assets/am_am_formc.png)

Questo frammento contiene due sottomaschere denominate *subPatientPhysical* e *subPatientHealth*. Entrambi i moduli secondari sono indicati nel documento DDX passato al servizio Assembler. Utilizzando il servizio Assembler, è possibile combinare tutti questi frammenti XDP in un unico documento XDP, come illustrato nella figura seguente.

![am_formd](assets/am_am_formd.png)

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

Il documento DDX contiene un tag XDP `result` che specifica il nome del risultato. In questa situazione, il valore è `tuc018result.xdp`. Questo valore è indicato nella logica dell&#39;applicazione utilizzata per recuperare il documento XDP dopo che il servizio Assembler ha restituito il risultato. Ad esempio, considera la seguente logica dell’applicazione Java utilizzata per recuperare il documento XDP assemblato (nota che il valore è in grassetto):

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

Il tag `XDP source` specifica il file XDP che rappresenta un documento XDP completo che può essere utilizzato come contenitore per l&#39;aggiunta di frammenti XDP o come uno dei numerosi documenti accodati nell&#39;ordine. In questa situazione, il documento XDP viene utilizzato solo come contenitore (la prima illustrazione mostrata in *Assemblaggio di più frammenti XDP*). In altre parole, gli altri file XDP vengono posizionati all’interno del contenitore XDP.

Per ogni modulo secondario, è possibile aggiungere un elemento `XDPContent` (questo elemento è facoltativo). Nell&#39;esempio precedente si noti che sono disponibili tre sottomoduli: `subPatientContact`, `subPatientPhysical` e `subPatientHealth`. Sia il sottomodulo `subPatientPhysical` che il sottomodulo `subPatientHealth` si trovano nello stesso file XDP, tuc018_patient.xdp. L’elemento frammento specifica il nome del modulo secondario, come definito in Designer.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Assembler, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Per ulteriori informazioni su un documento DDX, vedere [Servizio assemblatore e riferimento DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per assemblare più frammenti XDP, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Creare un client PDF Assembler.
1. Fare riferimento a un documento DDX esistente.
1. Fai riferimento ai documenti XDP.
1. Impostare le opzioni di runtime.
1. Assemblare più documenti XDP.
1. Recuperate il documento XDP assemblato.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

I seguenti file JAR devono essere aggiunti al percorso della classe del progetto:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (richiesto se AEM Forms è implementato su JBoss)
* jbossall-client.jar (obbligatorio se AEM Forms è distribuito su JBoss)

**Creare un client Assembler PDF**

Prima di eseguire un&#39;operazione Assembler a livello di programmazione, creare un client del servizio Assembler.

**Riferimento a un documento DDX esistente**

Per assemblare più documenti XDP, è necessario fare riferimento a un documento DDX. Questo documento DDX deve contenere `XDP result`, `XDP source` e `XDPContent` elementi.

**Riferimento ai documenti XDP**

Per assemblare più documenti XDP, fare riferimento a tutti i file XDP utilizzati per assemblare il documento XDP risultante. Verificare che il nome del modulo secondario contenuto nel documento XDP a cui fa riferimento l&#39;attributo `source` sia specificato nell&#39;attributo `fragment`. Un modulo secondario è definito in Designer. Consideriamo ad esempio il seguente codice XML.

```xml
 <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
```

Il modulo secondario denominato *subPatientContact* deve trovarsi nel file XDP denominato *tuc018_contact.xdp*.

**Impostare le opzioni di runtime**

È possibile impostare le opzioni di runtime che controllano il comportamento del servizio Assembler durante l&#39;esecuzione di un processo. È ad esempio possibile impostare un&#39;opzione che indichi al servizio Assembler di continuare l&#39;elaborazione di un processo in caso di errore.

**Assemblare più documenti XDP**

Per assemblare più file XDP, chiamare l&#39;operazione `invokeDDX`. Il servizio Assembler restituisce il documento XDP assemblato all&#39;interno di un oggetto insieme.

**Recupera il documento XDP assemblato**

Un documento XDP assemblato viene restituito all&#39;interno di un oggetto insieme. Scorrere l&#39;oggetto insieme e salvare il documento XDP come file XDP. Puoi anche passare il documento XDP a un altro servizio AEM Forms, ad esempio Output.

**Consulta anche**

[Assemblare più frammenti XDP utilizzando l’API Java](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-java-api)

[Assemblare più frammenti XDP utilizzando l’API del servizio web](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblaggio di documenti PDF a livello di programmazione](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)

[Creazione di documenti PDF tramite frammenti](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)

## Assemblare più frammenti XDP utilizzando l’API Java {#assemble-multiple-xdp-fragments-using-the-java-api}

Assembla più frammenti XDP utilizzando l’API del servizio Assembler (Java):

1. Includi file di progetto.

   Includi i file JAR client, come adobe-assembler-client.jar, nel percorso di classe del progetto Java.

1. Creare un client PDF Assembler.

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Fare riferimento a un documento DDX esistente.

   * Creare un oggetto `java.io.FileInputStream` che rappresenta il documento DDX utilizzando il relativo costruttore e passando un valore stringa che specifica la posizione del file DDX.
   * Creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e passando l&#39;oggetto `java.io.FileInputStream`.

1. Fai riferimento ai documenti XDP.

   * Creare un oggetto `java.util.Map` utilizzato per memorizzare i documenti XDP di input utilizzando un costruttore `HashMap`.
   * Creare un oggetto `com.adobe.idp.Document` e passare l&#39;oggetto `java.io.FileInputStream` che contiene il file XDP di input (ripetere questa attività per ogni file XDP).
   * Aggiungere una voce all&#39;oggetto `java.util.Map` richiamando il relativo metodo `put` e passando i seguenti argomenti:

      * Valore stringa che rappresenta il nome della chiave. Questo valore deve corrispondere al valore dell&#39;elemento `source` specificato nel documento DDX (ripetere questa attività per ogni file XDP).
      * Oggetto `com.adobe.idp.Document` contenente il documento XDP corrispondente all&#39;elemento `source` (ripetere questa attività per ogni file XDP).

1. Impostare le opzioni di runtime.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di runtime utilizzando il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali richiamando un metodo che appartiene all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per indicare al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, richiamare il metodo `setFailOnError` dell&#39;oggetto `AssemblerOptionSpec` e passare `false`.

1. Assemblare più documenti XDP.

   Richiama il metodo `invokeDDX` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori richiesti:

   * Oggetto `com.adobe.idp.Document` che rappresenta il documento DDX da utilizzare
   * Oggetto `java.util.Map` contenente i file XDP di input
   * Oggetto `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` che specifica le opzioni di runtime, inclusi il tipo di carattere predefinito e il livello del log del processo

   Il metodo `invokeDDX` restituisce un oggetto `com.adobe.livecycle.assembler.client.AssemblerResult` che contiene il documento XDP assemblato.

1. Recuperate il documento XDP assemblato.

   Per ottenere il documento XDP assemblato, effettuare le seguenti operazioni:

   * Richiama il metodo `getDocuments` dell&#39;oggetto `AssemblerResult`. Questo metodo restituisce un oggetto `java.util.Map`.
   * Scorrere l&#39;oggetto `java.util.Map` fino a trovare l&#39;oggetto `com.adobe.idp.Document` risultante.
   * Richiama il metodo `copyToFile` dell&#39;oggetto `com.adobe.idp.Document` per estrarre il documento XDP assemblato.

**Consulta anche**

[Assemblaggio di più frammenti XDP](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[Guida rapida (modalità SOAP): assemblaggio di più frammenti XDP tramite l&#39;API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api)
[Inclusi i file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblare più frammenti XDP utilizzando l’API del servizio web {#assemble-multiple-xdp-fragments-using-the-web-service-api}

Assembla più frammenti XDP utilizzando l’API del servizio Assembler (servizio web):

1. Includi file di progetto.

   Creare un progetto Microsoft .NET che utilizza MTOM. Assicurarsi di utilizzare la seguente definizione WSDL durante l&#39;impostazione di un riferimento al servizio:

   ```java
    https://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   >[!NOTE]
   >
   >Sostituisci `localhost` con l&#39;indirizzo IP del server che ospita AEM Forms.

1. Creare un client PDF Assembler.

   * Creare un oggetto `AssemblerServiceClient` utilizzando il relativo costruttore predefinito.
   * Creare un oggetto `AssemblerServiceClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il WSDL al servizio AEM Forms, ad esempio `https://localhost:8080/soap/services/AssemblerService?blob=mtom`). Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio.
   * Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del campo `AssemblerServiceClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
   * Impostare il campo `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
   * Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

      * Assegnare il nome utente dei moduli AEM al campo `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Assegnare il valore della password corrispondente al campo `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Assegnare il valore costante `HttpClientCredentialType.Basic` al campo `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al campo `BasicHttpBindingSecurity.Security.Mode`.

1. Fare riferimento a un documento DDX esistente.

   * Creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per archiviare il documento DDX.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file del documento DDX e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream`. Passare la matrice di byte, la posizione iniziale e la lunghezza del flusso per la lettura.
   * Compilare l&#39;oggetto `BLOB` assegnando la relativa proprietà `MTOM` al contenuto della matrice di byte.

1. Fai riferimento ai documenti XDP.

   * Per ogni file XDP di input, creare un oggetto `BLOB` utilizzando il relativo costruttore. L&#39;oggetto `BLOB` viene utilizzato per memorizzare il file di input.
   * Creare un oggetto `System.IO.FileStream` richiamandone il costruttore e passando un valore stringa che rappresenta la posizione del file di input e la modalità di apertura del file.
   * Creare una matrice di byte che memorizza il contenuto dell&#39;oggetto `System.IO.FileStream`. È possibile determinare le dimensioni della matrice di byte ottenendo la proprietà `Length` dell&#39;oggetto `System.IO.FileStream`.
   * Compilare la matrice di byte con i dati di flusso richiamando il metodo `Read` dell&#39;oggetto `System.IO.FileStream`. Passare la matrice di byte, la posizione iniziale e la lunghezza del flusso per la lettura.
   * Compilare l&#39;oggetto `BLOB` assegnando il relativo campo `MTOM` al contenuto della matrice di byte.
   * Creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Questo oggetto insieme viene utilizzato per memorizzare i file di input necessari per creare un documento XDP assemblato.
   * Per ogni file di input, creare un oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Assegnare un valore stringa che rappresenta il nome chiave al campo `key` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`. Questo valore deve corrispondere al valore dell&#39;elemento specificato nel documento DDX. (Esegui questa operazione per ogni file XDP di input).
   * Assegnare l&#39;oggetto `BLOB` che memorizza il file di input al campo `value` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item`. (Esegui questa operazione per ogni file XDP di input).
   * Aggiungere l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType_Item` all&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType`. Richiama il metodo `Add` dell&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType` e passa l&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType`. (Esegui questa operazione per ogni documento XDP di input.)

1. Impostare le opzioni di runtime.

   * Creare un oggetto `AssemblerOptionSpec` che memorizza le opzioni di runtime utilizzando il relativo costruttore.
   * Impostare le opzioni di runtime per soddisfare i requisiti aziendali assegnando un valore a un membro dati che appartiene all&#39;oggetto `AssemblerOptionSpec`. Ad esempio, per indicare al servizio Assembler di continuare a elaborare un processo quando si verifica un errore, assegnare `false` al membro dati `failOnError` dell&#39;oggetto `AssemblerOptionSpec`.

1. Assemblare più documenti XDP.

   Richiama il metodo `invokeDDX` dell&#39;oggetto `AssemblerServiceClient` e passa i seguenti valori:

   * Oggetto `BLOB` che rappresenta il documento DDX
   * L&#39;oggetto `MyMapOf_xsd_string_To_xsd_anyType` che contiene i file richiesti
   * Oggetto `AssemblerOptionSpec` che specifica le opzioni di runtime

   Il metodo `invokeDDX` restituisce un oggetto `AssemblerResult` contenente i risultati del processo ed eventuali eccezioni.

1. Recuperate il documento XDP assemblato.

   Per ottenere il documento XDP appena creato, effettuare le seguenti operazioni:

   * Accedere al campo `documents` dell&#39;oggetto `AssemblerResult`, che è un oggetto `Map` contenente i documenti PDF risultanti.
   * Scorrere l&#39;oggetto `Map` per ottenere ogni documento risultante. Quindi, esegui il cast di `value` del membro dell&#39;array in un `BLOB`.
   * Estrarre i dati binari che rappresentano il documento PDF accedendo alla proprietà `MTOM` dell&#39;oggetto `BLOB`. Restituisce una matrice di byte che è possibile scrivere in un file XDP.

**Consulta anche**

[Assemblaggio di più frammenti XDP](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
