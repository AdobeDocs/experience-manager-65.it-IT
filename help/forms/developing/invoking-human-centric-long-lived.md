---
title: Richiamo di processi a lunga durata basati sull'uomo
seo-title: Richiamo di processi a lunga durata basati sull'uomo
description: 'null'
seo-description: 'null'
uuid: 42269d41-a90f-4ea1-aeb9-d61337bcfa54
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 18a320b4-dce6-4c50-8864-644b0b2d6644
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '3669'
ht-degree: 0%

---


# Richiamo di processi a lunga durata basati sull&#39;uomo {#invoking-human-centric-long-lived-processes}

È possibile invocare a livello di programmazione i processi longevi incentrati sull&#39;uomo creati in Workbench utilizzando le seguenti applicazioni client:

* Un&#39;applicazione client Java basata su Web che utilizza l&#39;API Invocation. Consultate [Richiamare AEM Forms mediante l’API](/help/forms/developing/invoking-aem-forms-using-java.md)Java (/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api).
* Applicazione ASP.NET che utilizza i servizi Web. (Vedere [Chiamata di AEM Forms tramite servizi](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)Web.)
* Un&#39;applicazione client integrata con Flex che utilizza Remoting. (consultate [Richiamo di AEM Forms mediante (obsoleto per i moduli AEM) AEM Forms](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)Remoting.)

Il processo di lunga durata richiamato è denominato *FirstAppSolution/PreLoanProcess*. Potete creare questo processo seguendo l&#39;esercitazione specificata in [Creazione dell&#39;applicazione](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63)First AEM Forms.

Un processo incentrato sull’uomo implica un’attività a cui l’utente può rispondere utilizzando Workspace. Ad esempio, utilizzando Workbench è possibile creare un processo che consente a un manager bancario di approvare o rifiutare una richiesta di prestito. L&#39;illustrazione seguente mostra il processo *FirstAppSolution/PreLoanProcess*.

Il processo *FirstAppSolution/PreLoanProcess* accetta un parametro di input denominato *formData* il cui tipo di dati è XML. I dati XML vengono uniti con una struttura del modulo denominata *PreLoanForm.xdp*. Nell&#39;illustrazione seguente è illustrato un modulo che rappresenta un&#39;attività assegnata a un utente per approvare o rifiutare una richiesta di prestito. L’utente approva o nega l’applicazione utilizzando Workspace. L’utente di Workspace può approvare la richiesta di prestito facendo clic sul pulsante Approva illustrato nell’illustrazione seguente. Analogamente, l&#39;utente può negare la richiesta di prestito facendo clic sul pulsante di rifiuto.

Un processo longevo viene richiamato in modo asincrono e non può essere invocato in modo sincrono a causa dei seguenti fattori:

* Un processo può durare un periodo di tempo significativo.
* Un processo può estendersi oltre i limiti organizzativi.
* Per completare un processo, è necessario un input esterno. Si consideri, ad esempio, una situazione in cui un modulo viene inviato a un manager che non è in ufficio. In questa situazione, il processo non è completo finché il manager non restituisce e compila il modulo.

Quando viene richiamato un processo di lunga durata, i AEM Forms creano un valore identificativo di chiamata come parte della creazione di un record. Il record tiene traccia dello stato del processo di lunga durata e viene memorizzato nel database AEM Forms. Utilizzando il valore dell’identificatore di chiamata, potete tenere traccia dello stato del processo di lunga durata. Inoltre, potete utilizzare il valore dell&#39;identificatore di chiamata del processo per eseguire operazioni di Process Manager, ad esempio la terminazione di un&#39;istanza di processo in esecuzione.

>[!NOTE]
>
>I AEM Forms non creano un valore identificativo di chiamata o un record quando viene richiamato un processo di breve durata.

Il `FirstAppSolution/PreLoanProcess` processo viene richiamato quando un richiedente invia un&#39;applicazione, rappresentata come dati XML. Il nome della variabile del processo di input è XML `formData` e il relativo tipo di dati è XML. Ai fini di questa discussione, si supponga che i seguenti dati XML siano utilizzati come input per il `FirstAppSolution/PreLoanProcess` processo.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <LoanApp>
 <Name>Sam White</Name>
 <LoanAmount>250000</LoanAmount>
 <PhoneOrEmail>(555)555-5555</PhoneOrEmail>
 <ApprovalStatus>PENDING APPROVAL</ApprovalStatus>
 </LoanApp>
```

I dati XML passati a un processo devono corrispondere ai campi presenti nel modulo utilizzato nel processo. In caso contrario, i dati non vengono visualizzati all&#39;interno del modulo. Tutte le applicazioni che richiamano il `FirstAppSolution/PreLoanProcess` processo devono trasmettere questa origine dati XML. Le applicazioni create in *Invoking Human-Centric Long-Lived Processes (Richiamo di processi* a vita lunghi incentrati sull&#39;uomo) creano in modo dinamico l&#39;origine dati XML dai valori immessi da un utente in un client Web.

Utilizzando un&#39;applicazione client, è possibile inviare l&#39;elaborazione *FirstAppSolution/PreLoanProcess* dei dati XML richiesti. Un processo di lunga durata restituisce come valore restituito un identificatore di chiamata. L&#39;illustrazione seguente mostra le applicazioni client che richiamano il processo di lunga durata*FirstAppSolution/PreLoanProcess. Le applicazioni client inviano dati XML e restituiscono un valore di stringa che rappresenta il valore dell&#39;identificatore di chiamata.

**Consulta anche**

[Creazione di un&#39;applicazione Web Java che richiama un processo longevo incentrato sull&#39;uomo](invoking-human-centric-long-lived.md#creating-a-java-web-application-that-invokes-a-human-centric-long-lived-process)

[Creazione di un&#39;applicazione Web ASP.NET che richiama un processo longevo incentrato sull&#39;uomo](invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

[Creazione di un&#39;applicazione client integrata con Flex che richiama un processo longevo incentrato sull&#39;uomo](invoking-human-centric-long-lived.md#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process)

## Creazione di un&#39;applicazione Web Java che richiama un processo longevo incentrato sull&#39;uomo {#creating-a-java-web-application-that-invokes-a-human-centric-long-lived-process}

Potete creare un&#39;applicazione basata sul Web che utilizza un servlet Java per richiamare il `FirstAppSolution/PreLoanProcess` processo. Per richiamare questo processo da un servlet Java, utilizzate l&#39;API di vocazione all&#39;interno del servlet Java. (consultate [Chiamata di AEM Forms tramite l&#39;API](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)Java.)

L&#39;illustrazione seguente mostra un&#39;applicazione client basata sul Web che pubblica nome, telefono (o e-mail) e valori di importo. Questi valori vengono inviati al servlet Java quando l&#39;utente fa clic sul pulsante Invia applicazione.

Il servlet Java esegue le seguenti attività:

* Recupera i valori inviati dalla pagina HTML al servlet Java.
* Crea in modo dinamico un&#39;origine dati XML da trasmettere al processo *FirstAppSolution/PreLoanProcess* . I valori di nome, telefono (o e-mail) e importo sono specificati nell&#39;origine dati XML.
* Richiama il processo *FirstAppSolution/PreLoanProcess* utilizzando l&#39;API AEM Forms Invocation.
* Restituisce il valore dell&#39;identificatore di chiamata al browser Web del client.

### Riepilogo dei passaggi {#summary-of-steps}

Per creare un&#39;applicazione Java basata su Web che richiama il `FirstAppSolution/PreLoanProcess` processo, eseguire le operazioni seguenti:

1. [Creare un progetto](invoking-human-centric-long-lived.md#create-a-web-project)Web.
1. [Creare una logica di applicazione Java per il servlet](invoking-human-centric-long-lived.md#create-java-application-logic-for-the-servlet).
1. [Creare la pagina Web per l’applicazione Web](invoking-human-centric-long-lived.md#create-the-web-page-for-the-web-application)
1. [Creare un pacchetto dell&#39;applicazione Web in un file](invoking-human-centric-long-lived.md#package-the-web-application-to-a-war-file)WAR.
1. [Distribuire il file WAR ai AEM Forms](invoking-human-centric-long-lived.md#deploy-the-war-file-to-the-j2ee-application-server-hosting-aem-forms)host del server applicazione J2EE.
1. [Eseguite il test dell&#39;applicazione](invoking-human-centric-long-lived.md#test-your-web-application)Web.

>[!NOTE]
>
>Alcuni di questi passaggi dipendono dall’applicazione J2EE da cui vengono distribuiti i AEM Forms. Ad esempio, il metodo utilizzato per distribuire un file WAR dipende dal server applicazione J2EE in uso. Si presume che i AEM Forms siano distribuiti su JBoss®.

### Creazione di un progetto Web {#create-a-web-project}

Il primo passo per creare un&#39;applicazione Web è creare un progetto Web. L&#39;IDE Java su cui si basa il presente documento è Eclipse 3.3. Utilizzando Eclipse IDE, create un progetto Web e aggiungete i file JAR richiesti al progetto. Aggiungete una pagina HTML denominata *index.html* e un servlet Java al progetto.

Il seguente elenco specifica i file JAR da includere nel progetto Web:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* J2EE.jar

Per la posizione di questi file JAR, vedere [Inclusione di file](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)libreria Java AEM Forms.

>[!NOTE]
>
>Il file J2EE.jar definisce i tipi di dati utilizzati da un servlet Java. È possibile ottenere questo file JAR dal server applicazione J2EE su cui sono distribuiti i AEM Forms.

**Creazione di un progetto Web**

1. Avviate Eclipse e fate clic su **File** > **Nuovo progetto**.
1. Nella finestra di dialogo **Nuovo progetto** , selezionare **Web** > Progetto **Web** dinamico.
1. Digitare `InvokePreLoanProcess` il nome del progetto e fare clic su **Fine**.

**Aggiungere i file JAR richiesti al progetto**

1. Nella finestra Esplora progetti, fare clic con il pulsante destro del mouse sul `InvokePreLoanProcess` progetto e selezionare **Proprietà**.
1. Fate clic sul percorso **di creazione** Java, quindi fate clic sulla scheda **Librerie** .
1. Fate clic sul pulsante **Aggiungi JARs** esterni e individuate i file JAR da includere.

**Aggiungere un servlet Java al progetto**

1. Nella finestra Esplora progetti, fare clic con il pulsante destro del mouse sul `InvokePreLoanProcess` progetto e selezionare **Nuovo** > **Altro**.
1. Espandete la cartella **Web** , selezionate **Servlet** e fate clic su **Avanti**.
1. Nella finestra di dialogo Crea servlet, digitare `SubmitXML` il nome del servlet, quindi fare clic su **Fine**.

**Aggiungere una pagina HTML al progetto**

1. Nella finestra Esplora progetti, fare clic con il pulsante destro del mouse sul `InvokePreLoanProcess` progetto e selezionare **Nuovo** > **Altro**.
1. Espandete la cartella **Web** , selezionate **HTML** e fate clic su **Avanti**.
1. Nella finestra di dialogo Nuovo HTML, digitare `index.html` il nome del file e fare clic su **Fine**.

>[!NOTE]
>
>Per informazioni sulla creazione di contenuto HTML che richiama il servlet Java SubmitXML, consultate [Creare la pagina Web per l&#39;applicazione](invoking-human-centric-long-lived.md#create-the-web-page-for-the-web-application)Web.

### Creare una logica di applicazione Java per il servlet {#create-java-application-logic-for-the-servlet}

Creare una logica di applicazione Java che richiama il `FirstAppSolution/PreLoanProcess` processo dall&#39;interno del servlet Java. Il codice seguente mostra la sintassi del servlet `SubmitXML` Java:

```java
     public class SubmitXML extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {
         doPost(req,resp);
 
         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {
             //Add code here to invoke the FirstAppSolution/PreLoanProcess process
             }
```

Normalmente, il codice client non viene inserito all&#39;interno di un servlet `doGet` o di un `doPost` metodo Java. Una procedura di programmazione migliore consiste nell&#39;inserire questo codice all&#39;interno di una classe separata. Create quindi un&#39;istanza della classe dall&#39;interno del `doPost` metodo (o `doGet` metodo) e richiamate i metodi appropriati. Tuttavia, per la brevità del codice, gli esempi di codice vengono mantenuti al minimo e inseriti nel `doPost` metodo.

Per richiamare il `FirstAppSolution/PreLoanProcess` processo utilizzando l&#39;API di vocazione, eseguire le operazioni seguenti:

1. Includete file JAR client, ad esempio adobe-livecycle-client.jar, nel percorso di classe del progetto Java. Per informazioni sulla posizione di questi file, vedere [Inclusione di file](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)libreria Java AEM Forms.
1. Recuperate i valori di nome, telefono e importo inviati dalla pagina HTML. Utilizzare questi valori per creare in modo dinamico un&#39;origine dati XML inviata al `FirstAppSolution/PreLoanProcess` processo. È possibile utilizzare `org.w3c.dom` le classi per creare l&#39;origine dati XML (questa logica di applicazione è illustrata nell&#39;esempio di codice seguente).
1. Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione. (Vedere [Impostazione delle proprietà](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)di connessione.)
1. Creare un `ServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto. Un `ServiceClient` oggetto consente di richiamare un&#39;operazione del servizio. Gestisce attività quali l&#39;individuazione, l&#39;invio e il routing delle richieste di chiamata.
1. Creare un `java.util.HashMap` oggetto utilizzando il relativo costruttore.
1. Richiama il metodo dell’ `java.util.HashMap` oggetto `put` per ogni parametro di input da passare al processo longevo. Accertatevi di specificare il nome dei parametri di input del processo. Poiché il `FirstAppSolution/PreLoanProcess` processo richiede un parametro di input di tipo `XML` (denominato `formData``put` ), è necessario richiamare il metodo solo una volta.

   ```java
    //Get the XML to pass to the FirstAppSolution/PreLoanProcess process
    org.w3c.dom.Document inXML = GetDataSource(name,phone,amount);
    
    //Create a Map object to store the parameter value
    Map params = new HashMap();
    params.put("formData", inXML);
   ```

1. Creare un `InvocationRequest` oggetto richiamando il metodo dell&#39; `ServiceClientFactory` oggetto `createInvocationRequest` e passando i seguenti valori:

   * Un valore di stringa che specifica il nome del processo longevo da richiamare. Per richiamare il `FirstAppSolution/PreLoanProcess` processo, specificate `FirstAppSolution/PreLoanProcess`.
   * Un valore di stringa che rappresenta il nome dell&#39;operazione di processo. Il nome dell&#39;operazione di processo di lunga durata è `invoke`.
   * L&#39; `java.util.HashMap` oggetto che contiene i valori dei parametri richiesti dall&#39;operazione del servizio.
   * Un valore booleano che specifica `false`, che crea una richiesta asincrona (questo valore è applicabile per richiamare un processo longevo).

   >[!NOTE]
   >
   >*Un processo di breve durata può essere invocato trasmettendo il valore true come quarto parametro del metodo createInvocationRequest. Passando il valore true si crea una richiesta sincrona.*

1. Inviare la richiesta di chiamata agli AEM Forms richiamando il metodo dell&#39; `ServiceClient` oggetto `invoke` e passando l&#39; `InvocationRequest` oggetto. Il `invoke` metodo restituisce un `InvocationReponse` oggetto.
1. Un processo di lunga durata restituisce un valore di stringa che rappresenta un valore identificativo della chiamata. Recuperare questo valore richiamando il metodo dell&#39; `InvocationReponse` oggetto `getInvocationId` .

   ```java
    //Send the invocation request to the long-lived process and
    //get back an invocation response object
    InvocationResponse lcResponse = myServiceClient.invoke(lcRequest);
    String invocationId = lcResponse.getInvocationId();
   ```

1. Scrivete il valore di identificazione della chiamata nel browser Web del client. Potete utilizzare un&#39; `java.io.PrintWriter` istanza per scrivere questo valore nel browser Web del client.

### Avvio rapido: Richiamo di un processo di lunga durata tramite l&#39;API di incitamento {#quick-start-invoking-a-long-lived-process-using-the-invocation-api}

Il seguente esempio di codice Java rappresenta il servlet Java che richiama il `FirstAppSolution/PreLoanProcess` processo.

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-livecycle-client.jar
     * 2. adobe-usermanager-client.jar
     *
     * (Because this  quick start is implemented as a Java servlet, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     * */
 import java.io.ByteArrayOutputStream;
 import java.io.File;
 import java.io.IOException;
 import java.io.PrintWriter;
 
 import javax.servlet.ServletException;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import java.util.*;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import javax.xml.parsers.DocumentBuilder;
 import javax.xml.parsers.DocumentBuilderFactory;
 import javax.xml.transform.Transformer;
 import javax.xml.transform.TransformerFactory;
 import javax.xml.transform.dom.DOMSource;
 import javax.xml.transform.stream.StreamResult;
 
 import com.adobe.idp.dsc.InvocationRequest;
 import com.adobe.idp.dsc.InvocationResponse;
 import com.adobe.idp.dsc.clientsdk.ServiceClient;
 import org.w3c.dom.Element;
 
     public class SubmitXML extends javax.servlet.http.HttpServlet implements javax.servlet.Servlet {
       static final long serialVersionUID = 1L;
 
        public SubmitXML() {
         super();
     }
 
 
     protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
         // TODO Auto-generated method stub
         doPost(request,response);
     }
 
     protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
 
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://localhost:1099");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a ServiceClient object
             ServiceClient myServiceClient = myFactory.getServiceClient();
 
             //Get the values that are passed from the Loan HTML page
             String name = (String)request.getParameter("name");
             String phone = (String)request.getParameter("phone");
             String amount = (String)request.getParameter("amount");
 
             //Create XML to pass to the FirstAppSolution/PreLoanProcess process
             org.w3c.dom.Document inXML = GetDataSource(name,phone,amount);
 
             //Create a Map object to store the XML input parameter value
             Map params = new HashMap();
             params.put("formData", inXML);
 
             //Create an InvocationRequest object
             InvocationRequest lcRequest =  myFactory.createInvocationRequest(
                 "FirstAppSolution/PreLoanProcess", //Specify the long-lived process name
                     "invoke",           //Specify the operation name
                     params,               //Specify input values
                     false);               //Create an asynchronous request
 
             //Send the invocation request to the long-lived process and
             //get back an invocation response object
             InvocationResponse lcResponse = myServiceClient.invoke(lcRequest);
             String invocationId = lcResponse.getInvocationId();
 
             //Create a PrintWriter instance
             PrintWriter pp = response.getWriter();
 
             //Write the invocation identifier value back to the client web browser
             pp.println("The job status identifier value is: " +invocationId);
 
         }catch (Exception e) {
              System.out.println("The following exception occurred: "+e.getMessage());
       }
     }
 
 
      //Create XML data to pass to the long-lived process
      private static org.w3c.dom.Document GetDataSource(String name, String phone, String amount)
      {
             org.w3c.dom.Document document = null;
 
             try
             {
                 //Create DocumentBuilderFactory and DocumentBuilder objects
                 DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
                 DocumentBuilder builder = factory.newDocumentBuilder();
 
                 //Create a new Document object
                 document = builder.newDocument();
 
                 //Create MortgageApp - the root element in the XML
                 Element root = (Element)document.createElement("LoanApp");
                 document.appendChild(root);
 
                 //Create an XML element for Name
                 Element nameElement = (Element)document.createElement("Name");
                 nameElement.appendChild(document.createTextNode(name));
                 root.appendChild(nameElement);
 
                 //Create an XML element for Phone
                 Element phoneElement = (Element)document.createElement("PhoneOrEmail");
                 phoneElement.appendChild(document.createTextNode(phone));
                 root.appendChild(phoneElement);
 
                 //Create an XML element for amount
                 Element loanElement = (Element)document.createElement("LoanAmount");
                 loanElement.appendChild(document.createTextNode(amount));
                 root.appendChild(loanElement);
 
                 //Create an XML element for ApprovalStatus
                 Element approveElement = (Element)document.createElement("ApprovalStatus");
                 approveElement.appendChild(document.createTextNode("PENDING APPROVAL"));
                 root.appendChild(approveElement);
 
               }
          catch (Exception e) {
                   System.out.println("The following exception occurred: "+e.getMessage());
                }
         return document;
          }
         }
```

### Creare la pagina Web per l’applicazione Web {#create-the-web-page-for-the-web-application}

La pagina Web *index.html* fornisce un punto di ingresso al servlet Java che richiama il `FirstAppSolution/PreLoanProcess` processo. Questa pagina Web è un modulo HTML di base che contiene un modulo HTML e un pulsante di invio. Quando l&#39;utente fa clic sul pulsante di invio, i dati del modulo vengono inviati al servlet `SubmitXML` Java.

Il servlet Java acquisisce i dati inviati dalla pagina HTML utilizzando il seguente codice Java:

```java
 //Get the values that are passed from the Loan HTML page
 String name = request.getParameter("name");
 String phone = request.getParameter("phone");
 String amount = request.getParameter("amount");
```

Il seguente codice HTML rappresenta il file index.html creato durante l&#39;impostazione dell&#39;ambiente di sviluppo. Consultate [Creare un progetto](invoking-human-centric-long-lived.md#create-a-web-project)Web.

```xml
 <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "https://www.w3.org/TR/html4/loose.dtd">
 <html>
 <head>
 <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
 <title>Insert title here</title>
 </head>
 <body>
 <table>
     <TBODY>
         <TR>
             <td><img src="financeCorpLogo.jpg" width="172" height="62"></TD>
             <td><FONT size="+2"><strong>Java Loan Application Page</strong></FONT></TD>
             <td> </TD>
             <td> </TD>
         </TR>
 
     </TBODY>
 </TABLE>
     <FORM action="https://hiro-xp:8080/PreLoanProcess/SubmitXML" method="post">
        <table>
          <TBODY>
                <TR>
                      <td><LABEL for="name">Name: </LABEL></TD>
                  <td><INPUT type="text" name="name"></TD>
                  <td><input type="submit" value="Submit Application"></TD>
                  </TR>
            <TR>
                  <td> <LABEL for="phone">Phone/Email: </LABEL></TD>
              <td><INPUT type="text" name="phone"></TD>
                  <td></TD>
              </TR>
 
            <TR>
                  <td><LABEL for="amount">Amount: </LABEL></TD>
              <td><INPUT type="text" name="amount"></TD>
                 <td></TD>
             </TR>
          </TBODY>
 </TABLE>
       </FORM>
 </body>
 </html>
```

### Creare un pacchetto dell&#39;applicazione Web in un file WAR {#package-the-web-application-to-a-war-file}

Per distribuire il servlet Java che richiama il `FirstAppSolution/PreLoanProcess` processo, creare un pacchetto dell&#39;applicazione Web in un file WAR. Assicurati che nel file WAR siano inclusi anche i file JAR esterni da cui dipende la logica aziendale del componente, ad esempio adobe-livecycle-client.jar e adobe-usermanager-client.jar.

L&#39;illustrazione seguente mostra il contenuto del progetto Eclipse, che viene compresso in un file WAR.

>[!NOTE]
>
>Nell&#39;illustrazione precedente, il file JPG può essere sostituito da qualsiasi file immagine JPG.

**Creare un pacchetto di un&#39;applicazione Web in un file WAR:**

1. Nella finestra **Esplora** progetti, fare clic con il pulsante destro del mouse sul `InvokePreLoanProcess` progetto e selezionare **Esporta** > File **** WAR.
1. Nella casella di testo del modulo **** Web, digitare `InvokePreLoanProcess` il nome del progetto Java.
1. Nella casella di testo **Destinazione** , digitare `PreLoanProcess.war`**il nome del **file, specificare il percorso del file WAR, quindi fare clic su Fine.

### Distribuire il file WAR ai AEM Forms host del server applicazione J2EE {#deploy-the-war-file-to-the-j2ee-application-server-hosting-aem-forms}

Distribuire il file WAR sul server applicazione J2EE su cui sono distribuiti i AEM Forms. Per distribuire il file WAR al server applicazione J2EE, copiate il file WAR dal percorso di esportazione a `[AEM Forms Install]\Adobe\Adobe Experience Manager Forms\jboss\server\lc_turnkey\deploy`.

>[!NOTE]
>
>se i AEM Forms non sono distribuiti su JBoss, è necessario distribuire il file WAR in conformità con i AEM Forms host del server applicazione J2EE.

### Verificare l’applicazione Web {#test-your-web-application}

Dopo aver implementato l&#39;applicazione Web, potete verificarla utilizzando un browser Web. Presupponendo di utilizzare lo stesso computer in cui sono installati AEM Forms, potete specificare il seguente URL:

* http://localhost:8080/PreLoanProcess/index.html

   Immettete i valori nei campi del modulo HTML e fate clic sul pulsante Invia applicazione. Se si verificano dei problemi, consultare il file di registro del server applicazione J2EE.

>[!NOTE]
>
>Per confermare che l&#39;applicazione Java ha richiamato il processo, avviare Workspace e accettare il prestito.

## Creazione di un&#39;applicazione Web ASP.NET che richiama un processo longevo incentrato sull&#39;uomo {#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process}

È possibile creare un&#39;applicazione ASP.NET che richiama il `FirstAppSolution/PreLoanProcess` processo. Per richiamare questo processo da un&#39;applicazione ASP.NET, utilizzare i servizi Web. (Vedere [Chiamata di AEM Forms mediante i servizi](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)Web.)

Nell&#39;illustrazione seguente è illustrata un&#39;applicazione client ASP.NET che ottiene dati da un utente finale. I dati vengono inseriti in un&#39;origine dati XML e inviati al `FirstAppSolution/PreLoanProcess` processo quando l&#39;utente fa clic sul pulsante Invia applicazione.

Una volta richiamato il processo, viene visualizzato un valore di identificatore di chiamata. Il valore dell’identificatore di chiamata viene creato come parte di un record che tiene traccia dello stato del processo di lunga durata.

L&#39;applicazione ASP.NET esegue le seguenti attività:

* Recupera i valori immessi dall&#39;utente nella pagina Web.
* Crea in modo dinamico un&#39;origine dati XML passata al processo* FirstAppSolution/PreLoanProcess *process. I tre valori sono specificati nell&#39;origine dati XML.
* Richiama il processo* FirstAppSolution/PreLoanProcess *utilizzando i servizi Web.
* Restituisce il valore dell&#39;identificatore di chiamata e lo stato dell&#39;operazione di lunga durata al browser Web del client.

### Riepilogo dei passaggi {#summary_of_steps-1}

Per creare un&#39;applicazione ASP.NET in grado di richiamare il processo FirstAppSolution/PreLoanProcess, effettuare le seguenti operazioni:

1. [Creare un&#39;applicazione](invoking-human-centric-long-lived.md#create-an-asp-net-web-application)Web ASP.NET.
1. [Creare una pagina ASP che richiama FirstAppSolution/PreLoanProcess](invoking-human-centric-long-lived.md#create-an-asp-page-that-invokes-firstappsolution-preloanprocess).
1. [Eseguire l&#39;applicazione](invoking-human-centric-long-lived.md#run-the-asp-net-application)ASP.NET.

### Creare un&#39;applicazione Web ASP.NET {#create-an-asp-net-web-application}

Creare un&#39;applicazione Web Microsoft .NET C# ASP.NET. L&#39;illustrazione seguente mostra il contenuto del progetto ASP.NET denominato *InvokePreLoanProcess*.

In Riferimenti ai servizi sono disponibili due elementi. Il primo elemento è denominato* JobManager*. Questo riferimento consente all&#39;applicazione ASP.NET di richiamare il servizio Job Manager. Questo servizio restituisce informazioni sullo stato di un processo di lunga durata. Ad esempio, se il processo è in esecuzione, il servizio restituisce un valore numerico che specifica che il processo è in esecuzione. Il secondo riferimento è&#x200B;*denominatoPreLoanProcess*. Questo riferimento al servizio rappresenta il riferimento al processo* FirstAppSolution/PreLoanProcess *. Dopo aver creato un riferimento a un servizio, i tipi di dati associati al servizio AEM Forms sono disponibili per l&#39;utilizzo all&#39;interno del progetto .NET.

**Creare un progetto ASP.NET:**

1. Avviare Microsoft Visual Studio 2008.
1. Dal menu **File** , selezionate **Nuovo** sito **Web**.
1. Nell&#39;elenco **Modelli** , selezionare Sito **Web** ASP.NET.
1. Nella casella **Posizione** , selezionate una posizione per il progetto. Denominate il progetto *InvokePreLoanProcess*.
1. Nella casella **Lingua** selezionare Visual C#
1. Fai clic su OK.

**Aggiungi riferimenti al servizio:**

1. Nel menu Progetto, selezionate **Aggiungi riferimento** servizio.
1. Nella finestra di dialogo **Indirizzo** , specificare il WSDL nel servizio Job Manager.

   ```java
    https://hiro-xp:8080/soap/services/JobManager?WSDL&lc_version=9.0.1
   ```

1. Nel campo Spazio dei nomi, digitare `JobManager`.
1. Click **Go** and then click **OK**.
1. Nel menu **Progetto** , selezionate **Aggiungi riferimento** servizio.
1. Nella finestra di dialogo **Indirizzo** , specificare il WSDL per il processo FirstAppSolution/PreLoanProcess.

   ```java
    https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?WSDL&lc_version=9.0.1
   ```

1. Nel campo Spazio dei nomi, digitare `PreLoanProcess`.
1. Click **Go** and then click **OK**.

>[!NOTE]
>
>Sostituire `hiro-xp` con l&#39;indirizzo IP dei AEM Forms host del server applicazione J2EE. L&#39; `lc_version` opzione garantisce la disponibilità della funzionalità AEM Forms, ad esempio MTOM. Senza specificare l&#39; `lc_version`opzione, non è possibile richiamare AEM Forms utilizzando MTOM. (vedere [Chiamata di AEM Forms utilizzando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)).

### Creare una pagina ASP che richiama FirstAppSolution/PreLoanProcess {#create-an-asp-page-that-invokes-firstappsolution-preloanprocess}

All&#39;interno del progetto ASP.NET, aggiungere un modulo Web (un file ASPX) responsabile per la visualizzazione di una pagina HTML al richiedente del prestito. Il modulo Web si basa su una classe derivata da `System.Web.UI.Page`. La logica dell&#39;applicazione C# richiamata `FirstAppSolution/PreLoanProcess` si trova nel `Button1_Click` metodo (questo pulsante rappresenta il pulsante Invia applicazione).

Nell&#39;illustrazione seguente è illustrata l&#39;applicazione ASP.NET

Nella tabella seguente sono elencati i controlli che fanno parte di questa applicazione ASP.NET.

<table>
 <thead>
  <tr>
   <th><p>Nome controllo</p></th>
   <th><p>Descrizione</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>TextBoxName</p></td>
   <td><p>Specifica il nome e il cognome del cliente. </p></td>
  </tr>
  <tr>
   <td><p>TextBoxPhone</p></td>
   <td><p>Specifica l'indirizzo e-mail del cliente. </p></td>
  </tr>
  <tr>
   <td><p>TextBoxAmount</p></td>
   <td><p>Specifica l'importo del prestito.</p></td>
  </tr>
  <tr>
   <td><p>Button1</p></td>
   <td><p>Rappresenta il pulsante Invia applicazione.</p></td>
  </tr>
  <tr>
   <td><p>LabelJobID</p></td>
   <td><p>Un controllo Label che specifica il valore dell'identificatore di chiamata.</p></td>
  </tr>
  <tr>
   <td><p>LabelStatus</p></td>
   <td><p>Un controllo Label che specifica il valore dello stato del processo. Questo valore viene recuperato richiamando il servizio Job Manager. </p></td>
  </tr>
 </tbody>
</table>

La logica dell&#39;applicazione che fa parte dell&#39;applicazione ASP.NET deve creare in modo dinamico un&#39;origine dati XML da trasmettere al `FirstAppSolution/PreLoanProcess` processo. I valori immessi dal richiedente nella pagina HTML devono essere specificati all&#39;interno dell&#39;origine dati XML. Questi valori dati vengono uniti nel modulo quando il modulo viene visualizzato in Workspace. Le classi situate nello `System.Xml` spazio dei nomi vengono utilizzate per creare l&#39;origine dati XML.

Quando si richiama un processo che richiede dati XML da un&#39;applicazione ASP.NET, è possibile utilizzare un tipo di dati XML. In altre parole, non è possibile passare un&#39; `System.Xml.XmlDocument` istanza al processo. Il nome completo di questa istanza XML da passare al processo è `InvokePreLoanProcess.PreLoanProcess.XML`. Converti l’ `System.Xml.XmlDocument` istanza in `InvokePreLoanProcess.PreLoanProcess.XML`. È possibile eseguire questa operazione utilizzando il seguente codice.

```java
 //Create the XML to pass to the FirstAppSolution/PreLoanProcess process
 XmlDocument myXML = CreateXML(userName, phone, amount);
 
 //Convert the XML to a InvokePreLoanProcess.PreLoanProcess.XML instance
 StringWriter sw = new StringWriter();
 XmlTextWriter xw = new XmlTextWriter(sw);
 myXML.WriteTo(xw);
 
 InvokePreLoanProcess.PreLoanProcess.XML inXML = new XML();
 inXML.document = sw.ToString();
```

Per creare una pagina ASP che richiama il `FirstAppSolution/PreLoanProcess` processo, eseguire le operazioni seguenti nel `Button1_Click` metodo:

1. Creare un `FirstAppSolution_PreLoanProcessClient` oggetto utilizzando il relativo costruttore predefinito.
1. Creare un `FirstAppSolution_PreLoanProcessClient.Endpoint.Address` oggetto utilizzando il `System.ServiceModel.EndpointAddress` costruttore. Passa un valore di stringa che specifica il WSDL al servizio AEM Forms e il tipo di codifica:

   ```java
    https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?blob=mtom
   ```

   Non è necessario utilizzare l&#39; `lc_version` attributo. Questo attributo viene utilizzato quando create un riferimento a un servizio. Tuttavia, accertatevi di specificare `?blob=mtom`.

   >[!NOTE]
   >
   >Sostituire `hiro-xp`* con l&#39;indirizzo IP dei AEM Forms host del server applicazione J2EE. *

1. Creare un `System.ServiceModel.BasicHttpBinding` oggetto ottenendo il valore del membro `FirstAppSolution_PreLoanProcessClient.Endpoint.Binding` dati. Inserite il valore restituito in `BasicHttpBinding`.
1. Impostare il membro dati dell&#39; `System.ServiceModel.BasicHttpBinding` oggetto `MessageEncoding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
1. Abilitate l&#39;autenticazione HTTP di base eseguendo le seguenti operazioni:

   * Assegnare il nome utente dei moduli AEM al membro dati `FirstAppSolution_PreLoanProcessClient.ClientCredentials.UserName.UserName`.
   * Assegnare il valore della password corrispondente al membro dati `FirstAppSolution_PreLoanProcessClient.ClientCredentials.UserName.Password`.
   * Assegnare il valore costante `HttpClientCredentialType.Basic` al membro dati `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al membro dati `BasicHttpBindingSecurity.Security.Mode`.

   L&#39;esempio di codice seguente mostra queste attività.

   ```as3
    //Enable BASIC HTTP authentication
    BasicHttpBinding b = (BasicHttpBinding)mortgageClient.Endpoint.Binding;
    b.MessageEncoding = WSMessageEncoding.Mtom;
    mortgageClient.ClientCredentials.UserName.UserName = "administrator";
    mortgageClient.ClientCredentials.UserName.Password = "password";
    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
    b.MaxReceivedMessageSize = 2000000;
    b.MaxBufferSize = 2000000;
    b.ReaderQuotas.MaxArrayLength = 2000000;
   ```

1. Recuperate i valori di nome, telefono e importo immessi dall’utente nella pagina Web. Utilizzare questi valori per creare in modo dinamico un&#39;origine dati XML inviata al `FirstAppSolution/PreLoanProcess` processo. Creare un oggetto `System.Xml.XmlDocument` che rappresenti l&#39;origine dati XML da trasmettere al processo (la logica dell&#39;applicazione è illustrata nell&#39;esempio di codice seguente).
1. Converti l’ `System.Xml.XmlDocument` istanza in `InvokePreLoanProcess.PreLoanProcess.XML` (questa logica di applicazione è illustrata nell’esempio di codice seguente).
1. Richiamare il `FirstAppSolution/PreLoanProcess` processo richiamando il `FirstAppSolution_PreLoanProcessClient` metodo dell&#39; `invoke_Async` oggetto. Questo metodo restituisce un valore di stringa che rappresenta il valore dell’identificatore di chiamata del processo longevo.
1. Creare un `JobManagerClient` mediante il relativo costruttore. (Assicurarsi di aver impostato un riferimento al servizio Job Manager.)
1. Ripetere i passaggi da 1 a 5. Specificate il seguente URL per il passaggio 2: `https://hiro-xp:8080/soap/services/JobManager?blob=mtom`.
1. Creare un `JobId` oggetto utilizzando il relativo costruttore.
1. Impostare il membro `JobId` dati dell&#39; `id` oggetto con il valore restituito dal `FirstAppSolution_PreLoanProcessClient` metodo dell&#39;oggetto `invoke_Async` .
1. Assegnare il valore `value` true al membro `JobId` dati dell&#39; `persistent` oggetto.
1. Creare un `JobStatus` oggetto richiamando il `JobManagerService` metodo dell&#39;oggetto `getStatus` e passando l&#39; `JobId` oggetto.
1. Ottenere il valore dello stato recuperando il valore del membro `JobStatus` dati dell&#39; `statusCode` oggetto.
1. Assegnare il valore dell’identificatore di chiamata al `LabelJobID.Text` campo.
1. Assegnare il valore di stato al `LabelStatus.Text` campo.

### Avvio rapido: Richiamo di un processo di lunga durata tramite l&#39;API del servizio Web {#quick-start-invoking-a-long-lived-process-using-the-web-service-api}

Il seguente esempio di codice C# richiama il `FirstAppSolution/PreLoanProcess`processo.

```csharp
 ???/**
     * Ensure that you create a .NET project that uses
     * MS Visual Studio 2008 and version 3.5 of the .NET
     * framework. This is required to invoke a
     * AEM Forms service using MTOM.
 
 
 using System;
 using System.Collections;
 using System.Configuration;
 using System.Data;
 using System.Linq;
 using System.Web;
 using System.ServiceModel;
 using System.Web.Security;
 using System.Web.UI;
 using System.Web.UI.HtmlControls;
 using System.Web.UI.WebControls;
 using System.Web.UI.WebControls.WebParts;
 using System.Xml.Linq;
 using System.Xml;
 using System.IO;
 
 //A reference to FirstAppSolution/PreLoanProcess
 using InvokePreLoanProcess.PreLoanProcess;
 
 //A reference to JobManager service
 using InvokePreLoanProcess.JobManager;
 
 
 namespace InvokePreLoanProcess
 {
        public partial class _Default : System.Web.UI.Page
        {
            //This method is called when the Submit Application button is
            //Clicked
            protected void Button1_Click(object sender, EventArgs e)
            {
                //Create a FirstAppSolution_PreLoanProcessClient object
                FirstAppSolution_PreLoanProcessClient mortgageClient = new FirstAppSolution_PreLoanProcessClient();
                mortgageClient.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?blob=mtom");
 
                //Enable BASIC HTTP authentication
                BasicHttpBinding b = (BasicHttpBinding)mortgageClient.Endpoint.Binding;
                b.MessageEncoding = WSMessageEncoding.Mtom;
                mortgageClient.ClientCredentials.UserName.UserName = "administrator";
                mortgageClient.ClientCredentials.UserName.Password = "password";
                b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                b.MaxReceivedMessageSize = 2000000;
                b.MaxBufferSize = 2000000;
                b.ReaderQuotas.MaxArrayLength = 2000000;
 
                //Retrieve values that user entered into the web page
                String userName = TextBoxName.Text;
                String phone = TextBoxPhone.Text;
                String amount = TextBoxAmount.Text;
 
                //Create the XML to pass to the FirstAppSolution/PreLoanProcess process
                XmlDocument myXML = CreateXML(userName, phone, amount);
 
                StringWriter sw = new StringWriter();
                XmlTextWriter xw = new XmlTextWriter(sw);
                myXML.WriteTo(xw);
 
                InvokePreLoanProcess.PreLoanProcess.XML inXML = new XML();
                inXML.document = sw.ToString();
 
                //INvoke the FirstAppSolution/PreLoanProcess process
                String invocationID =  mortgageClient.invoke_Async(inXML);
 
                //Create a JobManagerClient object to obtain the status of the long-lived operation
                JobManagerClient jobManager = new JobManagerClient();
                jobManager.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/JobManager?blob=mtom");
 
                //Enable BASIC HTTP authentication
                BasicHttpBinding b1 = (BasicHttpBinding)jobManager.Endpoint.Binding;
                b1.MessageEncoding = WSMessageEncoding.Mtom;
                jobManager.ClientCredentials.UserName.UserName = "administrator";
                jobManager.ClientCredentials.UserName.Password = "password";
                b1.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                b1.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                b1.MaxReceivedMessageSize = 2000000;
                b1.MaxBufferSize = 2000000;
                b1.ReaderQuotas.MaxArrayLength = 2000000;
 
 
                //Create a JobID object that represents the status of the
                //long-lived operation
                JobId jobId = new JobId();
                jobId.id = invocationID;
                jobId.persistent = true;
                JobStatus jobStatus = jobManager.getStatus(jobId);
                System.Int16 val2 = jobStatus.statusCode;
                LabelJobID.Text = "The job status identifier value is " + invocationID;
                LabelStatus.Text = "The status of the long-lived operation is " + getJobDescription(val2);
 
            }
 
            private static XmlDocument CreateXML(String name, String phone, String amount)
            {
                //This method dynamically creates a DDX document
                //to pass to the FirstAppSolution/PreLoanProcess process
                XmlDocument xmlDoc = new XmlDocument();
 
                //Create the root element and append it to the XML DOM
                System.Xml.XmlElement root = xmlDoc.CreateElement("LoanApp");
                xmlDoc.AppendChild(root);
 
                //Create the Name element
                XmlElement nameElement = xmlDoc.CreateElement("Name");
                nameElement.AppendChild(xmlDoc.CreateTextNode(name));
                root.AppendChild(nameElement);
 
                //Create the LoanAmount element
                XmlElement LoanAmount = xmlDoc.CreateElement("LoanAmount");
                LoanAmount.AppendChild(xmlDoc.CreateTextNode(amount));
                root.AppendChild(LoanAmount);
 
                //Create the PhoneOrEmail element
                XmlElement PhoneOrEmail = xmlDoc.CreateElement("PhoneOrEmail");
                PhoneOrEmail.AppendChild(xmlDoc.CreateTextNode(phone));
                root.AppendChild(PhoneOrEmail);
 
                //Create the ApprovalStatus element
                XmlElement ApprovalStatus = xmlDoc.CreateElement("ApprovalStatus");
                ApprovalStatus.AppendChild(xmlDoc.CreateTextNode("PENDING APPROVAL"));
                root.AppendChild(ApprovalStatus);
 
                //Return the XmlElement instance
                return xmlDoc;
            }
 
 
            //Returns the String value of the Job Manager status code
            private String getJobDescription(int val)
            {
                switch(val)
                {
                    case 0:
                        return "JOB_STATUS_UNKNOWN";
 
                    case 1:
                        return "JOB_STATUS_QUEUED";
 
                    case 2:
                        return "JOB_STATUS_RUNNING";
 
                    case 3:
                        return "JOB_STATUS_COMPLETED";
 
                    case 4:
                        return "JOB_STATUS_FAILED";
 
                     case 5:
                        return "JOB_STATUS_COMPLETED";
 
                    case 6:
                        return "JOB_STATUS_SUSPENDED";
 
                    case 7:
                        return "JOB_STATUS_COMPLETE_REQUESTED";
 
                    case 8:
                        return "JOB_STATUS_TERMINATE_REQUESTED";
 
                     case 9:
                        return "JOB_STATUS_SUSPEND_REQUESTED";
 
                       case 10:
                        return "JOB_STATUS_RESUME_REQUESTED";
                }
 
                return "";
            }
       }
 }
 
```

>[!NOTE]
>
>I valori che si trovano nel metodo getJobDescription definito dall&#39;utente corrispondono ai valori restituiti dal servizio Job Manager.

### Eseguire l&#39;applicazione ASP.NET {#run-the-asp-net-application}

Dopo aver compilato e implementato l&#39;applicazione ASP.NET, è possibile eseguirla utilizzando un browser Web. Presupponendo che il nome del progetto ASP.NET sia *InvokePreLoanProcess*, specificate l&#39;URL seguente all&#39;interno di un browser Web:

*http://localhost:1629/InvokePreLoanProcess/*Default.aspx

dove localhost è il nome del server Web che ospita il progetto ASP.NET e 1629 è il numero di porta. Quando si compila e si crea l&#39;applicazione ASP.NET, Microsoft Visual Studio la distribuisce automaticamente.

>[!NOTE]
>
>Per confermare che l&#39;applicazione ASP.NET ha richiamato il processo, avviare Workspace e accettare il prestito.

## Creazione di un&#39;applicazione client integrata con Flex che richiama un processo longevo incentrato sull&#39;uomo {#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process}

È possibile creare un&#39;applicazione client integrata con Flex per richiamare il processo *FirstAppSolution/PreLoanProcess* . Questa applicazione utilizza Remoting per richiamare il processo *FirstAppSolution/PreLoanProcess* . (consultate [Richiamo di AEM Forms mediante (obsoleto per i moduli AEM) AEM Forms](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)Remoting.)

L&#39;illustrazione seguente mostra un&#39;applicazione client integrata con Flex che raccoglie dati da un utente finale. I dati vengono inseriti in un&#39;origine dati XML e inviati al processo.

Una volta richiamato il processo, viene visualizzato un valore di identificatore di chiamata. Il valore dell’identificatore di chiamata viene creato come parte di un record che tiene traccia dello stato del processo di lunga durata.

L&#39;applicazione client integrata con Flex esegue le seguenti attività:

* Recupera i valori immessi dall&#39;utente nella pagina Web.
* Crea in modo dinamico un&#39;origine dati XML passata al processo *FirstAppSolution/PreLoanProcess* . I tre valori sono specificati nell&#39;origine dati XML.
* Richiama il processo *FirstAppSolution/PreLoanProcess* utilizzando Remoting.
* Restituisce il valore dell&#39;identificatore di chiamata del processo longevo.

### Riepilogo dei passaggi {#summary_of_steps-2}

Per creare un&#39;applicazione client integrata con Flex in grado di richiamare il processo FirstAppSolution/PreLoanProcess, eseguire le operazioni seguenti:

1. Avviate un nuovo progetto Flex.
1. Includete il file adobe-remoting-provider.swc nel percorso di classe del progetto. Consultate [Inclusione del file](/help/forms/developing/invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)libreria Flex AEM Forms.
1. Create un&#39; `mx:RemoteObject` istanza tramite ActionScript o MXML. (Vedere [Creazione di un&#39;istanza](/help/forms/developing/invoking-aem-forms-using-remoting.md)mx:RemoteObject)
1. Configurate un&#39; `ChannelSet` istanza per comunicare con i AEM Forms e associatela all&#39; `mx:RemoteObject` istanza. Consultate [Creare un canale ai AEM Forms](/help/forms/developing/invoking-aem-forms-using-remoting.md).
1. Chiama il metodo ChannelSet o il `login` metodo del `setCredentials` servizio per specificare il valore dell&#39;identificatore utente e la password. Consultate [Utilizzo del single sign-on](/help/forms/developing/invoking-aem-forms-using-remoting.md#using-single-sign-on).
1. Creare l&#39;origine dati XML da trasmettere al `FirstAppSolution/PreLoanProcess` processo creando un&#39;istanza XML. (Questa logica dell&#39;applicazione è illustrata nel seguente esempio di codice.)
1. Creare un oggetto di tipo Object utilizzando il relativo costruttore. Assegnare l&#39;XML all&#39;oggetto specificando il nome del parametro di input del processo, come illustrato nel codice seguente:

   ```csharp
    //Get the XML data to pass to the AEM Forms process
    var xml:XML = createXML();
    var params:Object = new Object();
    params["formData"]=xml;
   ```

1. Richiamate il `FirstAppSolution/PreLoanProcess` processo chiamando il `mx:RemoteObject` metodo dell&#39; `invoke_Async` istanza. Passa il parametro `Object` che contiene il parametro di input. (Vedere [Trasmissione dei valori](/help/forms/developing/invoking-aem-forms-using-remoting.md)di input).
1. Recuperate il valore di identificazione della chiamata restituito da un processo di lunga durata, come illustrato nel codice seguente:

   ```csharp
    // Handles async call that invokes the long-lived process
    private function resultHandler(event:ResultEvent):void
    {
    ji = event.result as JobId;
    jobStatusDisplay.text = "Job Status ID: " + ji.jobId as String;
    }
   ```

### Richiamo di un processo di lunga durata tramite Remoting {#invoking-a-long-lived-process-using-remoting}

Il seguente esempio di codice Flex richiama il `FirstAppSolution/PreLoanProcess` processo.

```java
 <?xml version="1.0" encoding="utf-8"?>
 
 <mx:Application  xmlns="*" backgroundColor="#FFFFFF"
      creationComplete="initializeChannelSet();">
 
 <mx:Script>
          <![CDATA[
 
             import mx.controls.Alert;
             import mx.rpc.events.FaultEvent;
             import mx.rpc.events.ResultEvent;
             import flash.net.navigateToURL;
             import mx.messaging.ChannelSet;
             import mx.messaging.channels.AMFChannel;
             import mx.collections.ArrayCollection;
             import mx.rpc.livecycle.JobId;
             import mx.rpc.livecycle.JobStatus;
             import mx.rpc.livecycle.DocumentReference;
             import mx.formatters.NumberFormatter;
 
             // Holds the job ID returned by LC.JobManager
             private var ji:JobId;
 
             private function initializeChannelSet():void
              {
              var cs:ChannelSet= new ChannelSet();
         cs.addChannel(new AMFChannel("remoting-amf", "https://hiro-xp:8080/remoting/messagebroker/amf"));
         LC_MortgageApp.setCredentials("tblue", "password");
         LC_MortgageApp.channelSet = cs;
              }
 
            private function submitApplication():void
             {
             //Get the XML data to pass to the AEM Forms process
             var xml:XML = createXML();
             var params:Object = new Object();
             params["formData"]=xml;
             LC_MortgageApp.invoke_Async(params);
             }
 
             // Handles async call that invokes the long-lived process
             private function resultHandler(event:ResultEvent):void
             {
                ji = event.result as JobId;
                jobStatusDisplay.text = "Job Status ID: " + ji.jobId as String;
             }
 
             private function createXML():XML
             {
                //Calculate the Mortgage value to place in the XML data
                var propertyPrice:String = txtAmount.text ;
                var name:String = txtName.text ;
                var phone:String = txtPhone.text ;;
 
                var model:XML =
 
                  <LoanApp>
                           <Name>{name}</Name>
                           <LoanAmount>{propertyPrice}</LoanAmount>
                           <PhoneOrEmail>{phone}</PhoneOrEmail>
                           <ApprovalStatus>PENDING APPROVAL</ApprovalStatus>
                  </LoanApp>
 
              return model;
             }
 
 
          ]]>
       </mx:Script>
 
       <!-- Declare the RemoteObject and set its destination to the mortgage-app remoting endpoint defined in AEM Forms. -->
       <mx:RemoteObject id="LC_MortgageApp" destination="FirstAppSolution/PreLoanProcess" result="resultHandler(event);">
          <mx:method name="invoke_Async" result="resultHandler(event)"/>
      </mx:RemoteObject>
 
 
     <mx:Grid x="229" y="186">
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
                 <mx:Image>
                     <mx:source>file:///D|/LiveCycle_9/FirstApp/financeCorpLogo.jpg</mx:source>
                 </mx:Image>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Flex Loan Application Page" fontSize="20"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
         </mx:GridRow>
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Name:" fontSize="12" fontWeight="bold"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:TextInput id="txtName"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:Button label="Submit Application" click="submitApplication()"/>
             </mx:GridItem>
         </mx:GridRow>
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Phone/Email:" fontSize="12" fontWeight="bold"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:TextInput id="txtPhone"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
         </mx:GridRow>
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Amount:" fontSize="12" fontWeight="bold"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:TextInput id="txtAmount"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
         </mx:GridRow>
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Label" id="jobStatusDisplay" enabled="true" fontSize="12" fontWeight="bold"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
         </mx:GridRow>
     </mx:Grid>
 
 </mx:Application>
 
```

