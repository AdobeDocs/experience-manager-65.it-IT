---
title: Richiamare processi a lunga durata incentrati sull'uomo
description: Richiama in modo programmatico i processi a lunga durata incentrati sull'uomo creati in Workbench utilizzando un'applicazione client Java basata sul Web che utilizza l'API Invocation, un'applicazione ASP.NET che utilizza i servizi Web e un'applicazione client creata con Flex che utilizza la comunicazione remota.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
role: Developer
exl-id: c9ebad8b-b631-492d-99a3-094e892b2ddb
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations,AEM Forms on JEE
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '3674'
ht-degree: 0%

---

# Richiamare processi a lunga durata incentrati sull&#39;uomo {#invoking-human-centric-long-lived-processes}

Puoi richiamare in modo programmatico i processi a vita lunga incentrati sull’uomo creati in Workbench utilizzando le seguenti applicazioni client:

* Applicazione client Java basata sul Web che utilizza l&#39;API di richiamo. (Vedi [Richiamare AEM Forms utilizzando l&#39;API Java](/help/forms/developing/invoking-aem-forms-using-java.md)(/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api).)
* Applicazione ASP.NET che utilizza servizi Web. (Vedi [Chiamata di AEM Forms tramite servizi Web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)
* Applicazione client creata con Flex che utilizza la funzionalità di comunicazione remota. (Vedi [Chiamata di AEM Forms tramite (obsoleto per i moduli AEM) AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

Il processo di lunga durata richiamato è denominato *FirstAppSolution/PreLoanProcess*. Puoi creare questo processo seguendo l&#39;esercitazione specificata in [Creazione della prima applicazione AEM Forms](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63).

Un processo incentrato sull’uomo implica un’attività alla quale un utente può rispondere utilizzando Workspace. Ad esempio, utilizzando Workbench, è possibile creare un processo che consenta a un manager bancario di approvare o rifiutare una richiesta di prestito. Nella figura seguente viene illustrato il processo *FirstAppSolution/PreLoanProcess*.

Il processo *FirstAppSolution/PreLoanProcess* accetta un parametro di input denominato *formData* il cui tipo di dati è XML. I dati XML vengono uniti a una struttura di modulo denominata *PreLoanForm.xdp*. Nella figura seguente viene illustrato un modulo che rappresenta un task assegnato a un utente per approvare o rifiutare una richiesta di prestito. L’utente approva o nega l’applicazione utilizzando Workspace. L’utente di Workspace può approvare la richiesta di prestito facendo clic sul pulsante Approve (Approva) illustrato nella figura seguente. Analogamente, l’utente può rifiutare la richiesta di prestito facendo clic sul pulsante Nega.

Un processo di lunga durata viene richiamato in modo asincrono e non può essere richiamato in modo sincrono a causa dei seguenti fattori:

* Un processo può richiedere molto tempo.
* Un processo può estendersi oltre i confini dell’organizzazione.
* Per completare un processo è necessario un input esterno. Si consideri ad esempio una situazione in cui un modulo viene inviato a un manager fuori sede. In questa situazione, il processo non viene completato fino a quando il manager non restituisce e compila il modulo.

Quando viene richiamato un processo di lunga durata, AEM Forms crea un valore di identificativo di chiamata come parte della creazione di un record. Il record tiene traccia dello stato del processo di lunga durata e viene memorizzato nel database di AEM Forms. Utilizzando il valore dell&#39;identificatore di chiamata, è possibile tenere traccia dello stato del processo di lunga durata. È inoltre possibile utilizzare il valore dell&#39;identificatore di chiamata del processo per eseguire operazioni di Gestione processi, ad esempio la chiusura di un&#39;istanza del processo in esecuzione.

>[!NOTE]
>
>AEM Forms non crea un valore di identificatore di chiamata o un record quando viene richiamato un processo di breve durata.

Il processo `FirstAppSolution/PreLoanProcess` viene richiamato quando un richiedente invia un&#39;applicazione, rappresentata come dati XML. Il nome della variabile del processo di input è `formData` e il relativo tipo di dati è XML. Ai fini della presente discussione, si supponga che i seguenti dati XML vengano utilizzati come input per il processo `FirstAppSolution/PreLoanProcess`.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <LoanApp>
 <Name>Sam White</Name>
 <LoanAmount>250000</LoanAmount>
 <PhoneOrEmail>(555)555-5555</PhoneOrEmail>
 <ApprovalStatus>PENDING APPROVAL</ApprovalStatus>
 </LoanApp>
```

I dati XML passati a un processo devono corrispondere ai campi nel modulo utilizzato nel processo. In caso contrario, i dati non verranno visualizzati all&#39;interno del modulo. Tutte le applicazioni che richiamano il processo `FirstAppSolution/PreLoanProcess` devono passare questa origine dati XML. Le applicazioni create in *Richiamo di processi a lunga durata incentrati sull&#39;uomo* creano in modo dinamico l&#39;origine dati XML dai valori immessi da un utente in un client Web.

Utilizzando un&#39;applicazione client, puoi inviare *FirstAppSolution/PreLoanProcess* a elaborare i dati XML richiesti. Un processo di lunga durata restituisce un valore dell&#39;identificatore di chiamata come valore restituito. L’illustrazione seguente mostra le applicazioni client che richiamano il processo di lunga durata*FirstAppSolution/PreLoanProcess. Le applicazioni client inviano dati XML e restituiscono un valore stringa che rappresenta il valore dell&#39;identificatore di chiamata.

**Consulta anche**

[Creazione di un’applicazione web Java che richiama un processo di lunga durata incentrato sull’uomo](invoking-human-centric-long-lived.md#creating-a-java-web-application-that-invokes-a-human-centric-long-lived-process)

[Creazione di un&#39;applicazione Web ASP.NET che richiama un processo di lunga durata incentrato sull&#39;uomo](invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

[Creazione di un&#39;applicazione client creata con Flex che richiama un processo di lunga durata incentrato sull&#39;uomo](invoking-human-centric-long-lived.md#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process)

## Creazione di un’applicazione web Java che richiama un processo di lunga durata incentrato sull’uomo {#creating-a-java-web-application-that-invokes-a-human-centric-long-lived-process}

È possibile creare un&#39;applicazione basata sul Web che utilizza un servlet Java per richiamare il processo `FirstAppSolution/PreLoanProcess`. Per richiamare questo processo da un servlet Java, utilizza l’API di chiamata all’interno del servlet Java. (Vedi [Richiamare AEM Forms utilizzando l&#39;API Java](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api).)

La figura seguente mostra un&#39;applicazione client basata sul Web che pubblica i valori di nome, telefono (o e-mail) e importo. Questi valori vengono inviati al servlet Java quando l’utente fa clic sul pulsante Invia applicazione.

Il servlet Java esegue le seguenti attività:

* Recupera i valori pubblicati dalla pagina HTML nel servlet Java.
* Crea in modo dinamico un&#39;origine dati XML da passare al processo *FirstAppSolution/PreLoanProcess*. I valori di nome, telefono (o e-mail) e quantità sono specificati nell&#39;origine dati XML.
* Richiama il processo *FirstAppSolution/PreLoanProcess* utilizzando l&#39;API di chiamata di AEM Forms.
* Restituisce il valore dell&#39;identificatore di chiamata al browser Web client.

### Riepilogo dei passaggi {#summary-of-steps}

Per creare un&#39;applicazione Java basata sul Web che richiama il processo `FirstAppSolution/PreLoanProcess`, effettuare le seguenti operazioni:

1. [Crea un progetto Web](invoking-human-centric-long-lived.md#create-a-web-project).
1. [Creare la logica dell&#39;applicazione Java per il servlet](invoking-human-centric-long-lived.md#create-java-application-logic-for-the-servlet).
1. [Creare la pagina web per l’applicazione web](invoking-human-centric-long-lived.md#create-the-web-page-for-the-web-application)
1. [Creare un pacchetto dell&#39;applicazione Web in un file WAR](invoking-human-centric-long-lived.md#package-the-web-application-to-a-war-file).
1. [Distribuire il file WAR nel server applicazioni J2EE che ospita AEM Forms](invoking-human-centric-long-lived.md#deploy-the-war-file-to-the-j2ee-application-server-hosting-aem-forms).
1. [Verifica l&#39;applicazione Web](invoking-human-centric-long-lived.md#test-your-web-application).

>[!NOTE]
>
>Alcuni di questi passaggi dipendono dall’applicazione J2EE su cui viene distribuito AEM Forms. Ad esempio, il metodo utilizzato per distribuire un file WAR dipende dal server applicazioni J2EE in uso. Si presume che AEM Forms sia implementato su JBoss®.

### Creare un progetto web {#create-a-web-project}

Il primo passaggio per creare un’applicazione web consiste nel creare un progetto web. L’IDE Java su cui si basa questo documento è Eclipse 3.3. Utilizzando l’IDE Eclipse, crea un progetto web e aggiungi al progetto i file JAR richiesti. Aggiungi al progetto una pagina HTML denominata *index.html* e un servlet Java.

L’elenco seguente specifica i file JAR da includere nel progetto web:

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* J2EE.jar

Per il percorso di questi file JAR, vedi [Inclusi i file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

>[!NOTE]
>
>Il file J2EE.jar definisce i tipi di dati utilizzati da un servlet Java. Puoi ottenere questo file JAR dal server applicazioni J2EE in cui viene distribuito AEM Forms.

**Crea un progetto Web**

1. Avvia Eclipse e fai clic su **File** > **Nuovo progetto**.
1. Nella finestra di dialogo **Nuovo progetto** selezionare **Web** > **Progetto Web dinamico**.
1. Digitare `InvokePreLoanProcess` per il nome del progetto, quindi fare clic su **Fine**.

**Aggiungi i file JAR richiesti al progetto**

1. Nella finestra Esplora progetti fare clic con il pulsante destro del mouse sul progetto `InvokePreLoanProcess` e selezionare **Proprietà**.
1. Fare clic su **Percorso build Java** e quindi sulla scheda **Libraries**.
1. Fai clic sul pulsante **Aggiungi JAR esterni** e individua i file JAR da includere.

**Aggiungi un servlet Java al progetto**

1. Nella finestra Esplora progetti fare clic con il pulsante destro del mouse sul progetto `InvokePreLoanProcess` e selezionare **Nuovo** > **Altro**.
1. Espandere la cartella **Web**, selezionare **Servlet**, quindi fare clic su **Avanti**.
1. Nella finestra di dialogo Crea servlet digitare `SubmitXML` per il nome del servlet e quindi fare clic su **Fine**.

**Aggiungi una pagina HTML al progetto**

1. Nella finestra Esplora progetti fare clic con il pulsante destro del mouse sul progetto `InvokePreLoanProcess` e selezionare **Nuovo** > **Altro**.
1. Espandi la cartella **Web**, seleziona **HTML**, quindi fai clic su **Avanti**.
1. Nella finestra di dialogo Nuovo HTML digitare `index.html` per il nome del file e quindi fare clic su **Fine**.

>[!NOTE]
>
>Per informazioni sulla creazione di contenuto HTML che richiama il servlet Java SubmitXML, vedere [Creare la pagina Web per l&#39;applicazione Web](invoking-human-centric-long-lived.md#create-the-web-page-for-the-web-application).

### Creare la logica dell’applicazione Java per il servlet {#create-java-application-logic-for-the-servlet}

Creare la logica dell&#39;applicazione Java che richiama il processo `FirstAppSolution/PreLoanProcess` dall&#39;interno del servlet Java. Il codice seguente mostra la sintassi del servlet Java `SubmitXML`:

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

In genere, il codice client non viene inserito nel metodo `doGet` o `doPost` di un servlet Java. Una migliore pratica di programmazione consiste nel posizionare questo codice all&#39;interno di una classe separata. Creare quindi un&#39;istanza della classe all&#39;interno del metodo `doPost` (o del metodo `doGet`) e chiamare i metodi appropriati. Tuttavia, per la brevità del codice, gli esempi di codice sono limitati al minimo e sono inseriti nel metodo `doPost`.

Per richiamare il processo `FirstAppSolution/PreLoanProcess` utilizzando l&#39;API di chiamata, eseguire le attività seguenti:

1. Includi i file JAR dei client, ad esempio adobe-livecycle-client.jar, nel percorso di classe del progetto Java. Per informazioni sul percorso di questi file, vedere [Inclusi i file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).
1. Recupera i valori di nome, telefono e importo inviati dalla pagina HTML. Utilizzare questi valori per creare in modo dinamico un&#39;origine dati XML inviata al processo `FirstAppSolution/PreLoanProcess`. È possibile utilizzare `org.w3c.dom` classi per creare l&#39;origine dati XML (questa logica dell&#39;applicazione è illustrata nell&#39;esempio di codice seguente).
1. Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione. (Vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
1. Creare un oggetto `ServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`. Un oggetto `ServiceClient` consente di richiamare un&#39;operazione di servizio. Gestisce attività quali l’individuazione, l’invio e l’instradamento delle richieste di chiamata.
1. Creare un oggetto `java.util.HashMap` utilizzando il relativo costruttore.
1. Richiama il metodo `put` dell&#39;oggetto `java.util.HashMap` per ogni parametro di input da passare al processo di lunga durata. Assicurarsi di specificare il nome dei parametri di input del processo. Poiché il processo `FirstAppSolution/PreLoanProcess` richiede un parametro di input di tipo `XML` (denominato `formData`), è necessario richiamare il metodo `put` una sola volta.

   ```java
    //Get the XML to pass to the FirstAppSolution/PreLoanProcess process
    org.w3c.dom.Document inXML = GetDataSource(name,phone,amount);
    
    //Create a Map object to store the parameter value
    Map params = new HashMap();
    params.put("formData", inXML);
   ```

1. Creare un oggetto `InvocationRequest` richiamando il metodo `createInvocationRequest` dell&#39;oggetto `ServiceClientFactory` e passando i valori seguenti:

   * Valore stringa che specifica il nome del processo di lunga durata da richiamare. Per richiamare il processo `FirstAppSolution/PreLoanProcess`, specificare `FirstAppSolution/PreLoanProcess`.
   * Valore stringa che rappresenta il nome dell&#39;operazione di processo. Il nome dell&#39;operazione del processo di lunga durata è `invoke`.
   * L&#39;oggetto `java.util.HashMap` che contiene i valori dei parametri richiesti dall&#39;operazione del servizio.
   * Valore booleano che specifica `false`, che crea una richiesta asincrona. Questo valore è applicabile per richiamare un processo di lunga durata.

   >[!NOTE]
   >
   >*Un processo di breve durata può essere richiamato passando il valore true come quarto parametro del metodo createInvocationRequest. Se si passa il valore true, viene creata una richiesta sincrona.*

1. Inviare la richiesta di chiamata ad AEM Forms richiamando il metodo `invoke` dell&#39;oggetto `ServiceClient` e passando l&#39;oggetto `InvocationRequest`. Il metodo `invoke` restituisce un oggetto `InvocationReponse`.
1. Un processo di lunga durata restituisce un valore stringa che rappresenta un valore di identificazione di chiamata. Recuperare questo valore richiamando il metodo `getInvocationId` dell&#39;oggetto `InvocationReponse`.

   ```java
    //Send the invocation request to the long-lived process and
    //get back an invocation response object
    InvocationResponse lcResponse = myServiceClient.invoke(lcRequest);
    String invocationId = lcResponse.getInvocationId();
   ```

1. Scrivere il valore di identificazione della chiamata nel browser Web client. È possibile utilizzare un&#39;istanza `java.io.PrintWriter` per scrivere questo valore nel browser Web client.

### Guida introduttiva: richiamare un processo di lunga durata utilizzando l’API di chiamata {#quick-start-invoking-a-long-lived-process-using-the-invocation-api}

L&#39;esempio di codice Java seguente rappresenta il servlet Java che richiama il processo `FirstAppSolution/PreLoanProcess`.

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
     * These JAR files are in the following path:
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
 
                 //Create a Document object
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

### Creare la pagina web per l’applicazione web {#create-the-web-page-for-the-web-application}

La pagina Web *index.html* fornisce un punto di ingresso al servlet Java che richiama il processo `FirstAppSolution/PreLoanProcess`. Questa pagina Web è un modulo HTML di base che contiene un modulo HTML e un pulsante di invio. Quando l&#39;utente fa clic sul pulsante di invio, i dati del modulo vengono inviati al servlet Java `SubmitXML`.

Il servlet Java acquisisce i dati pubblicati dalla pagina HTML utilizzando il seguente codice Java:

```java
 //Get the values that are passed from the Loan HTML page
 String name = request.getParameter("name");
 String phone = request.getParameter("phone");
 String amount = request.getParameter("amount");
```

Il codice HTML seguente rappresenta il file index.html creato durante l’installazione dell’ambiente di sviluppo. (Vedi [Creare un progetto Web](invoking-human-centric-long-lived.md#create-a-web-project).)

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

### Creare un pacchetto dell’applicazione web in un file WAR {#package-the-web-application-to-a-war-file}

Per distribuire il servlet Java che richiama il processo `FirstAppSolution/PreLoanProcess`, creare un pacchetto dell&#39;applicazione Web in un file WAR. Assicurati che nel file WAR siano inclusi anche i file JAR esterni da cui dipende la logica di business del componente, come adobe-livecycle-client.jar e adobe-usermanager-client.jar.

L’illustrazione seguente mostra il contenuto del progetto Eclipse, inserito in un pacchetto in un file WAR.

>[!NOTE]
>
>Nell’illustrazione precedente, il file JPG può essere sostituito da qualsiasi file di immagine JPG.

**Creare il pacchetto di un&#39;applicazione Web in un file WAR:**

1. Dalla finestra **Esplora progetti**, fare clic con il pulsante destro del mouse sul progetto `InvokePreLoanProcess` e selezionare **Esporta** > **File WAR**.
1. Nella casella di testo **Modulo Web** digitare `InvokePreLoanProcess` per il nome del progetto Java.
1. Nella casella di testo **Destinazione** digitare `PreLoanProcess.war`**per il nome del file**, specificare il percorso del file WAR e quindi fare clic su Fine.

### Distribuire il file WAR nel server applicazioni J2EE che ospita AEM Forms {#deploy-the-war-file-to-the-j2ee-application-server-hosting-aem-forms}

Distribuire il file WAR sul server applicazioni J2EE sul quale viene distribuito AEM Forms. Per distribuire il file WAR nel server applicazioni J2EE, copiare il file WAR dal percorso di esportazione in `[AEM Forms Install]\Adobe\Adobe Experience Manager Forms\jboss\server\lc_turnkey\deploy`.

>[!NOTE]
>
>se AEM Forms non è distribuito su JBoss, è necessario distribuire il file WAR in conformità con il server applicazioni J2EE che ospita AEM Forms.

### Testare l’applicazione web {#test-your-web-application}

Dopo aver distribuito l’applicazione web, puoi testarla utilizzando un browser web. Se utilizzi lo stesso computer che ospita AEM Forms, puoi specificare il seguente URL:

* http://localhost:8080/PreLoanProcess/index.html

  Immettere i valori nei campi del modulo HTML e fare clic sul pulsante Sottometti applicazione. Se si verificano problemi, vedere il file di registro del server applicazioni J2EE.

>[!NOTE]
>
>Per confermare che l’applicazione Java ha richiamato il processo, avvia Workspace e accetta il prestito.

## Creazione di un&#39;applicazione Web ASP.NET che richiama un processo di lunga durata incentrato sull&#39;uomo {#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process}

È possibile creare un&#39;applicazione ASP.NET che richiami il processo `FirstAppSolution/PreLoanProcess`. Per richiamare questo processo da un&#39;applicazione ASP.NET, utilizzare i servizi Web. (Vedi [Chiamata di AEM Forms tramite servizi Web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)

La figura seguente mostra un&#39;applicazione client ASP.NET che ottiene dati da un utente finale. I dati vengono inseriti in un&#39;origine dati XML e inviati al processo `FirstAppSolution/PreLoanProcess` quando l&#39;utente fa clic sul pulsante Invia applicazione.

Avviso dopo che il processo è stato richiamato, viene visualizzato un valore dell&#39;identificatore di chiamata. Un valore dell&#39;identificatore di chiamata viene creato come parte di un record che tiene traccia dello stato del processo di lunga durata.

L&#39;applicazione ASP.NET esegue le seguenti attività:

* Recupera i valori immessi dall’utente nella pagina web.
* Crea in modo dinamico un&#39;origine dati XML che viene passata al processo* FirstAppSolution/PreLoanProcess *. I tre valori sono specificati nell&#39;origine dati XML.
* Richiama il processo* FirstAppSolution/PreLoanProcess *utilizzando i servizi web.
* Restituisce il valore dell&#39;identificatore di chiamata e lo stato dell&#39;operazione di lunga durata al browser Web client.

### Riepilogo dei passaggi {#summary_of_steps-1}

Per creare un&#39;applicazione ASP.NET in grado di richiamare il processo FirstAppSolution/PreLoanProcess, effettuare le seguenti operazioni:

1. [Creare un&#39;applicazione Web ASP.NET](invoking-human-centric-long-lived.md#create-an-asp-net-web-application).
1. [Creare una pagina ASP che richiami FirstAppSolution/PreLoanProcess](invoking-human-centric-long-lived.md#create-an-asp-page-that-invokes-firstappsolution-preloanprocess).
1. [Esegui l&#39;applicazione ASP.NET](invoking-human-centric-long-lived.md#run-the-asp-net-application).

### Creare un’applicazione web ASP.NET {#create-an-asp-net-web-application}

Creare un&#39;applicazione Web Microsoft .NET C# ASP.NET. Nella figura seguente viene illustrato il contenuto del progetto ASP.NET denominato *InvokePreLoanProcess*.

Avviso in Riferimenti servizio sono disponibili due elementi. Il primo elemento è denominato* JobManager*. Questo riferimento consente all&#39;applicazione ASP.NET di richiamare il servizio Gestione processi. Questo servizio restituisce informazioni sullo stato di un processo di lunga durata. Se ad esempio il processo è in esecuzione, il servizio restituisce un valore numerico che specifica che il processo è in esecuzione. Il secondo riferimento è denominato *PreLoanProcess*. Questo riferimento al servizio rappresenta il riferimento al processo* FirstAppSolution/PreLoanProcess *. Dopo aver creato un riferimento al servizio, i tipi di dati associati al servizio AEM Forms sono disponibili per l&#39;utilizzo all&#39;interno del progetto .NET.

**Crea un progetto ASP.NET:**

1. Avviare Microsoft Visual Studio 2008.
1. Dal menu **File**, selezionare **Nuovo**, **Sito Web**.
1. Nell&#39;elenco **Modelli** selezionare **ASP.NET sito Web**.
1. Nella casella **Posizione** selezionare una posizione per il progetto. Denomina il progetto *InvokePreLoanProcess*.
1. Nella casella **Lingua** selezionare Visual C#
1. Fare clic su OK.

**Aggiungi riferimenti al servizio:**

1. Nel menu Progetto, selezionare **Aggiungi riferimento servizio**.
1. Nella finestra di dialogo **Indirizzo** specificare il file WSDL per il servizio Gestione processi.

   ```java
    https://hiro-xp:8080/soap/services/JobManager?WSDL&lc_version=9.0.1
   ```

1. Nel campo Namespace, digitare `JobManager`.
1. Fai clic su **Vai a** e quindi su **OK**.
1. Nel menu **Progetto**, seleziona **Aggiungi riferimento servizio**.
1. Nella finestra di dialogo **Indirizzo** specificare il WSDL per il processo FirstAppSolution/PreLoanProcess.

   ```java
    https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?WSDL&lc_version=9.0.1
   ```

1. Nel campo Namespace, digitare `PreLoanProcess`.
1. Fai clic su **Vai a** e quindi su **OK**.

>[!NOTE]
>
>Sostituire `hiro-xp` con l&#39;indirizzo IP del server applicazioni J2EE che ospita AEM Forms. L&#39;opzione `lc_version` garantisce la disponibilità delle funzionalità di AEM Forms, ad esempio MTOM. Senza specificare l&#39;opzione `lc_version`, non è possibile richiamare AEM Forms utilizzando MTOM. (Vedi [Chiamata di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom).)

### Creare una pagina ASP che richiami FirstAppSolution/PreLoanProcess {#create-an-asp-page-that-invokes-firstappsolution-preloanprocess}

All’interno del progetto ASP.NET, aggiungi un modulo web (un file ASPX) responsabile della visualizzazione di una pagina HTML al richiedente del prestito. Il modulo Web è basato su una classe derivata da `System.Web.UI.Page`. La logica dell&#39;applicazione C# che richiama `FirstAppSolution/PreLoanProcess` si trova nel metodo `Button1_Click` (questo pulsante rappresenta il pulsante Invia applicazione).

La figura seguente mostra l&#39;applicazione ASP.NET

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
   <td><p>Specifica nome e cognome del cliente. </p></td>
  </tr>
  <tr>
   <td><p>TextBoxPhone</p></td>
   <td><p>Specifica l’indirizzo di telefono o e-mail del cliente. </p></td>
  </tr>
  <tr>
   <td><p>Valore TextBoxAmount</p></td>
   <td><p>Specifica l’importo del prestito.</p></td>
  </tr>
  <tr>
   <td><p>Pulsante1</p></td>
   <td><p>Rappresenta il pulsante Invia applicazione.</p></td>
  </tr>
  <tr>
   <td><p>LabelJobID</p></td>
   <td><p>Controllo Label che specifica il valore dell'identificatore di chiamata.</p></td>
  </tr>
  <tr>
   <td><p>LabelStatus</p></td>
   <td><p>Controllo Label che specifica il valore dello stato del processo. Questo valore viene recuperato richiamando il servizio Gestione processi. </p></td>
  </tr>
 </tbody>
</table>

La logica dell&#39;applicazione che fa parte dell&#39;applicazione ASP.NET deve creare in modo dinamico un&#39;origine dati XML da passare al processo `FirstAppSolution/PreLoanProcess`. I valori immessi dal richiedente nella pagina HTML devono essere specificati nell&#39;origine dati XML. Questi valori di dati vengono uniti nel modulo quando questo viene visualizzato in Workspace. Le classi nello spazio dei nomi `System.Xml` vengono utilizzate per creare l&#39;origine dati XML.

Quando si richiama un processo che richiede dati XML da un&#39;applicazione ASP.NET, è disponibile un tipo di dati XML da utilizzare. Non è quindi possibile passare un&#39;istanza `System.Xml.XmlDocument` al processo. Il nome completo dell&#39;istanza XML da passare al processo è `InvokePreLoanProcess.PreLoanProcess.XML`. Convertire l&#39;istanza `System.Xml.XmlDocument` in `InvokePreLoanProcess.PreLoanProcess.XML`. È possibile eseguire questa operazione utilizzando il codice seguente.

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

Per creare una pagina ASP che richiami il processo `FirstAppSolution/PreLoanProcess`, eseguire le attività seguenti nel metodo `Button1_Click`:

1. Creare un oggetto `FirstAppSolution_PreLoanProcessClient` utilizzando il relativo costruttore predefinito.
1. Creare un oggetto `FirstAppSolution_PreLoanProcessClient.Endpoint.Address` utilizzando il costruttore `System.ServiceModel.EndpointAddress`. Passa un valore stringa che specifica il file WSDL al servizio AEM Forms e il tipo di codifica:

   ```java
    https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?blob=mtom
   ```

   Non è necessario utilizzare l&#39;attributo `lc_version`. Questo attributo viene utilizzato quando si crea un riferimento a un servizio. Tuttavia, assicurarsi di specificare `?blob=mtom`.

   >[!NOTE]
   >
   >Sostituire `hiro-xp`* con l&#39;indirizzo IP del server applicazioni J2EE che ospita AEM Forms. *

1. Creare un oggetto `System.ServiceModel.BasicHttpBinding` ottenendo il valore del membro dati `FirstAppSolution_PreLoanProcessClient.Endpoint.Binding`. Eseguire il cast del valore restituito in `BasicHttpBinding`.
1. Impostare il membro dati `MessageEncoding` dell&#39;oggetto `System.ServiceModel.BasicHttpBinding` su `WSMessageEncoding.Mtom`. Questo valore assicura che venga utilizzato MTOM.
1. Abilita l’autenticazione HTTP di base eseguendo le seguenti attività:

   * Assegnare il nome utente dei moduli AEM al membro dati `FirstAppSolution_PreLoanProcessClient.ClientCredentials.UserName.UserName`.
   * Assegnare il valore della password corrispondente al membro dati `FirstAppSolution_PreLoanProcessClient.ClientCredentials.UserName.Password`.
   * Assegnare il valore costante `HttpClientCredentialType.Basic` al membro dati `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Assegnare il valore costante `BasicHttpSecurityMode.TransportCredentialOnly` al membro dati `BasicHttpBindingSecurity.Security.Mode`.

   Nell&#39;esempio di codice riportato di seguito vengono illustrate queste attività.

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

1. Recupera i valori di nome, telefono e importo immessi dall’utente nella pagina web. Utilizzare questi valori per creare in modo dinamico un&#39;origine dati XML inviata al processo `FirstAppSolution/PreLoanProcess`. Creare un elemento `System.Xml.XmlDocument` che rappresenta l&#39;origine dati XML da passare al processo (questa logica di applicazione è illustrata nell&#39;esempio di codice seguente).
1. Convertire l&#39;istanza `System.Xml.XmlDocument` in `InvokePreLoanProcess.PreLoanProcess.XML` (questa logica dell&#39;applicazione è illustrata nell&#39;esempio di codice seguente).
1. Richiama il processo `FirstAppSolution/PreLoanProcess` richiamando il metodo `invoke_Async` dell&#39;oggetto `FirstAppSolution_PreLoanProcessClient`. Questo metodo restituisce un valore stringa che rappresenta il valore dell&#39;identificatore di chiamata del processo di lunga durata.
1. Creare `JobManagerClient` utilizzando il costruttore is. Verificare di aver impostato un riferimento al servizio Gestione processo.
1. Ripetere i passaggi da 1 a 5. Specificare l&#39;URL seguente per il passaggio 2: `https://hiro-xp:8080/soap/services/JobManager?blob=mtom`.
1. Creare un oggetto `JobId` utilizzando il relativo costruttore.
1. Impostare il membro dati `id` dell&#39;oggetto `JobId` con il valore restituito del metodo `invoke_Async` dell&#39;oggetto `FirstAppSolution_PreLoanProcessClient`.
1. Assegnare `value` true al membro dati `persistent` dell&#39;oggetto `JobId`.
1. Creare un oggetto `JobStatus` richiamando il metodo `getStatus` dell&#39;oggetto `JobManagerService` e passando l&#39;oggetto `JobId`.
1. Ottenere il valore dello stato recuperando il valore del membro dati `statusCode` dell&#39;oggetto `JobStatus`.
1. Assegnare il valore dell&#39;identificatore di chiamata al campo `LabelJobID.Text`.
1. Assegnare il valore dello stato al campo `LabelStatus.Text`.

### Guida introduttiva: richiamare un processo di lunga durata utilizzando l’API del servizio web {#quick-start-invoking-a-long-lived-process-using-the-web-service-api}

Nell&#39;esempio di codice C# seguente viene richiamato il processo `FirstAppSolution/PreLoanProcess`.

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
>I valori nel metodo definito dall&#39;utente getJobDescription corrispondono ai valori restituiti dal servizio Gestione processo.

### Eseguire l&#39;applicazione ASP.NET {#run-the-asp-net-application}

Dopo aver compilato e distribuito l&#39;applicazione ASP.NET, è possibile eseguirla utilizzando un browser Web. Supponendo che il nome del progetto ASP.NET sia *InvokePreLoanProcess*, specifica il seguente URL in un browser Web:

*http://localhost:1629/InvokePreLoanProcess/*Default.aspx

dove localhost è il nome del server web che ospita il progetto ASP.NET e 1629 è il numero di porta. Quando si compila e si genera l&#39;applicazione ASP.NET, Microsoft Visual Studio, la distribuisce automaticamente.

>[!NOTE]
>
>Per confermare che l&#39;applicazione ASP.NET ha richiamato il processo, avviare Workspace e accettare il prestito.

## Creazione di un&#39;applicazione client creata con Flex che richiama un processo di lunga durata incentrato sull&#39;uomo {#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process}

È possibile creare un&#39;applicazione client creata con Flex per richiamare il processo *FirstAppSolution/PreLoanProcess*. Questa applicazione utilizza la funzionalità di comunicazione remota per richiamare il processo *FirstAppSolution/PreLoanProcess*. (Vedi [Chiamata di AEM Forms tramite (obsoleto per i moduli AEM) AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

L’illustrazione seguente mostra un’applicazione client creata con Flex che raccoglie dati da un utente finale. I dati vengono inseriti in un&#39;origine dati XML e inviati al processo.

Avviso dopo che il processo è stato richiamato, viene visualizzato un valore dell&#39;identificatore di chiamata. Un valore dell&#39;identificatore di chiamata viene creato come parte di un record che tiene traccia dello stato del processo di lunga durata.

L’applicazione client generata con Flex esegue le seguenti attività:

* Recupera i valori immessi dall’utente nella pagina web.
* Crea in modo dinamico un&#39;origine dati XML passata al processo *FirstAppSolution/PreLoanProcess*. I tre valori sono specificati nell&#39;origine dati XML.
* Richiama il processo *FirstAppSolution/PreLoanProcess* utilizzando la funzionalità di comunicazione remota.
* Restituisce il valore dell&#39;identificatore di chiamata del processo di lunga durata.

### Riepilogo dei passaggi {#summary_of_steps-2}

Per creare un&#39;applicazione client generata con Flex in grado di richiamare il processo FirstAppSolution/PreLoanProcess, effettuare le seguenti operazioni:

1. Avvia un nuovo progetto Flex.
1. Includi il file adobe-remoting-provider.swc nel percorso della classe del progetto. (Vedi [Inclusione del file della libreria Flex di AEM Forms](/help/forms/developing/invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file).)
1. Creare un&#39;istanza `mx:RemoteObject` tramite ActionScript o MXML. (Vedi [Creazione di un&#39;istanza mx:RemoteObject](/help/forms/developing/invoking-aem-forms-using-remoting.md))
1. Configura un&#39;istanza `ChannelSet` per comunicare con AEM Forms e associala all&#39;istanza `mx:RemoteObject`. (Vedi [Creare un canale per AEM Forms](/help/forms/developing/invoking-aem-forms-using-remoting.md).)
1. Chiamare il metodo `login` di ChannelSet o il metodo `setCredentials` del servizio per specificare il valore e la password dell&#39;identificatore utente. (Vedere [Utilizzo del Single Sign-On](/help/forms/developing/invoking-aem-forms-using-remoting.md#using-single-sign-on).)
1. Creare l&#39;origine dati XML da passare al processo `FirstAppSolution/PreLoanProcess` creando un&#39;istanza XML. Questa logica di applicazione è illustrata nell&#39;esempio di codice seguente.
1. Creare un oggetto di tipo Object utilizzando il relativo costruttore. Assegnare il codice XML all&#39;oggetto specificando il nome del parametro di input del processo, come illustrato nel codice seguente:

   ```csharp
    //Get the XML data to pass to the AEM Forms process
    var xml:XML = createXML();
    var params:Object = new Object();
    params["formData"]=xml;
   ```

1. Richiama il processo `FirstAppSolution/PreLoanProcess` chiamando il metodo `invoke_Async` dell&#39;istanza `mx:RemoteObject`. Passa `Object` che contiene il parametro di input. (Vedi [Trasmissione dei valori di input](/help/forms/developing/invoking-aem-forms-using-remoting.md).)
1. Recuperare il valore di identificazione della chiamata restituito da un processo di lunga durata, come illustrato nel codice seguente:

   ```csharp
    // Handles async call that invokes the long-lived process
    private function resultHandler(event:ResultEvent):void
    {
    ji = event.result as JobId;
    jobStatusDisplay.text = "Job Status ID: " + ji.jobId as String;
    }
   ```

### Richiamare un processo di lunga durata tramite la comunicazione remota {#invoking-a-long-lived-process-using-remoting}

Nell&#39;esempio di codice di Flex seguente viene richiamato il processo `FirstAppSolution/PreLoanProcess`.

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
