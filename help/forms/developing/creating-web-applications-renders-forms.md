---
title: Creazione di applicazioni Web per il rendering di Forms
seo-title: Creazione di applicazioni Web per il rendering di Forms
description: 'null'
seo-description: 'null'
uuid: 00de10c5-79bd-4d8a-ae18-32f1fd2623bf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f29b089e-8902-4744-81c5-15ee41ba8069
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1831'
ht-degree: 0%

---


# Creazione di applicazioni Web per il rendering di Forms {#creating-web-applications-thatrenders-forms}

## Creazione di applicazioni Web per il rendering di Forms {#creating-web-applications-that-renders-forms}

È possibile creare un&#39;applicazione basata sul Web che utilizza servlet Java per richiamare il servizio Forms ed eseguire il rendering dei moduli. Un vantaggio derivante dall&#39;utilizzo di un servlet Java™ è rappresentato dal fatto che è possibile scrivere il valore restituito dal processo in un browser Web client. In altre parole, un servlet Java può essere utilizzato come collegamento tra il servizio Forms che restituisce un modulo e un browser Web client.

>[!NOTE]
>
>Questa sezione descrive come creare un&#39;applicazione basata sul Web che utilizza un servlet Java che richiama il servizio Forms ed esegue il rendering di moduli basati sui frammenti. (Vedere [Rendering di Forms basato su frammenti](/help/forms/developing/rendering-forms-based-fragments.md).)

Utilizzando un servlet Java, è possibile scrivere un modulo in un browser Web client in modo che il cliente possa visualizzare e immettere i dati nel modulo. Dopo aver compilato il modulo con i dati, l&#39;utente Web fa clic su un pulsante di invio situato nel modulo per inviare le informazioni al servlet Java, dove è possibile recuperare ed elaborare i dati. Ad esempio, i dati possono essere inviati a un altro processo.

In questa sezione viene illustrato come creare un&#39;applicazione basata sul Web che consenta all&#39;utente di selezionare dati del modulo basati su Stati Uniti o dati del modulo basati su Canada, come illustrato nell&#39;illustrazione seguente.

![cw_cw_fragmentwebclient](assets/cw_cw_fragmentwebclient.png)

Il modulo di cui si esegue il rendering è un modulo basato sui frammenti. Se l&#39;utente seleziona dati americani, il modulo restituito utilizza quindi frammenti basati su dati americani. Ad esempio, il piè di pagina del modulo contiene un indirizzo americano, come illustrato nell&#39;illustrazione seguente.

![cw_cw_fragementformfooter](assets/cw_cw_fragementformfooter.png)

Analogamente, se l&#39;utente seleziona dati canadesi, il modulo restituito contiene un indirizzo canadese, come illustrato nell&#39;illustrazione seguente.

![cw_cw_fragementformfootercnd](assets/cw_cw_fragementformfootercnd.png)

>[!NOTE]
>
>Per informazioni sulla creazione di strutture del modulo basate sui frammenti, vedere [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

**File di esempio**

In questa sezione vengono utilizzati file di esempio che possono essere memorizzati nel seguente percorso:

&lt;directory *di installazione di* Forms Designer>/Samples/Forms/Purchase Order/Form Fragments

dove &lt;directory *di* installazione> è il percorso di installazione. Ai fini dell&#39;applicazione client, il file Purchase Order Dynamic.xdp è stato copiato da questo percorso di installazione e distribuito in un&#39;applicazione Forms denominata *Applications/FormsApplication*. Il file Purchase Order Dynamic.xdp viene memorizzato in una cartella denominata FormsFolder. Analogamente, i frammenti vengono inseriti in una cartella denominata Frammenti, come illustrato nell&#39;illustrazione seguente.

![cw_cw_fragmentsrepository](assets/cw_cw_fragmentsrepository.png)

Per accedere alla struttura del modulo Purchase Order Dynamic.xdp, specificare `Applications/FormsApplication/1.0/FormsFolder/Purchase Order Dynamic.xdp` come nome del modulo (il primo parametro passato al `renderPDFForm` metodo) e `repository:///` come valore URI della directory principale del contenuto.

I file di dati XML utilizzati dall&#39;applicazione Web sono stati spostati dalla cartella Data a `C:\Adobe`(il file system che appartiene al server applicazione J2EE che ospita  AEM Forms). I nomi dei file sono Purchase Order *Canada.xml* e Purchase Order *US.xml*.

>[!NOTE]
>
>Per informazioni sulla creazione di un&#39;applicazione Forms tramite Workbench, vedere la Guida [](https://www.adobe.com/go/learn_aemforms_workbench_63)di Workbench.

### Riepilogo dei passaggi {#summary-of-steps}

Per creare un&#39;applicazione basata sul Web che esegue il rendering di moduli basati sui frammenti, procedere come segue:

1. Crea un nuovo progetto Web.
1. Creare una logica di applicazione Java che rappresenta il servlet Java.
1. Creare la pagina Web per l’applicazione Web.
1. Creare un pacchetto dell&#39;applicazione Web in un file WAR.
1. Distribuire il file WAR sul server applicazioni J2EE.
1. Eseguite il test dell&#39;applicazione Web.

>[!NOTE]
>
>Alcuni di questi passaggi dipendono dall’applicazione J2EE da cui  AEM Forms è distribuito. Ad esempio, il metodo utilizzato per distribuire un file WAR dipende dal server applicazione J2EE in uso. Questa sezione presuppone che  AEM Forms sia distribuito su JBoss®.

### Creazione di un progetto Web {#creating-a-web-project}

Il primo passo per creare un&#39;applicazione Web che contenga un servlet Java che possa richiamare il servizio Forms è creare un nuovo progetto Web. L&#39;IDE Java su cui si basa il presente documento è Eclipse 3.3. Utilizzando Eclipse IDE, create un progetto Web e aggiungete i file JAR richiesti al progetto. Infine, aggiungete una pagina HTML denominata *index.html* e un servlet Java al progetto.

L&#39;elenco seguente specifica i file JAR da aggiungere al progetto Web:

* adobe-forms-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar

Per la posizione di questi file JAR, consultate [Inclusione  file](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)libreria Java AEM Forms.

**Per creare un progetto Web:**

1. Avviate Eclipse e fate clic su **File** > **Nuovo progetto**.
1. Nella finestra di dialogo **Nuovo progetto** , selezionare **Web** > Progetto **Web** dinamico.
1. Digitare `FragmentsWebApplication` il nome del progetto e fare clic su **Fine**.

**Per aggiungere al progetto i file JAR richiesti:**

1. Nella finestra Esplora progetti, fare clic con il pulsante destro del mouse sul `FragmentsWebApplication` progetto e selezionare **Proprietà**.
1. Fate clic sul percorso **di creazione** Java, quindi fate clic sulla scheda **Librerie** .
1. Fate clic sul pulsante **Aggiungi JARs** esterni e individuate i file JAR da includere.

**Per aggiungere un servlet Java al progetto:**

1. Nella finestra Esplora progetti, fare clic con il pulsante destro del mouse sul `FragmentsWebApplication` progetto e selezionare **Nuovo** > **Altro**.
1. Espandete la cartella **Web** , selezionate **Servlet** e fate clic su **Avanti**.
1. Nella finestra di dialogo Crea servlet, digitare `RenderFormFragment` il nome del servlet, quindi fare clic su **Fine**.

**Per aggiungere una pagina HTML al progetto:**

1. Nella finestra Esplora progetti, fare clic con il pulsante destro del mouse sul `FragmentsWebApplication` progetto e selezionare **Nuovo** > **Altro**.
1. Espandete la cartella **Web** , selezionate **HTML** e fate clic su **Avanti**.
1. Nella finestra di dialogo Nuovo HTML, digitare `index.html` il nome del file, quindi fare clic su **Fine**.

>[!NOTE]
>
>Per informazioni sulla creazione di una pagina HTML che richiama il servlet `RenderFormFragment` Java, consultate [Creazione di una pagina](/help/forms/developing/rendering-forms.md#creating-the-web-page)Web.

### Creazione di una logica di applicazione Java per il servlet {#creating-java-application-logic-for-the-servlet}

È possibile creare una logica di applicazione Java che richiama il servizio Forms dall&#39;interno del servlet Java. Il codice seguente mostra la sintassi del servlet `RenderFormFragment` Java:

```java
     public class RenderFormFragment extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {
         doPost(req,resp);
 
         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {
             //Add code here to invoke the Forms service
             }
```

Normalmente, il codice client non viene inserito all&#39;interno di un servlet `doGet` o di un `doPost` metodo Java. Una procedura di programmazione migliore consiste nel posizionare il codice all&#39;interno di una classe separata, creare un&#39;istanza della classe all&#39;interno del `doPost` metodo (o `doGet` metodo) e chiamare i metodi appropriati. Tuttavia, per la brevità del codice, gli esempi di codice riportati in questa sezione sono limitati al minimo e gli esempi di codice sono inseriti nel `doPost` metodo.

Per eseguire il rendering di un modulo basato su frammenti utilizzando l&#39;API del servizio Forms, effettuare le seguenti operazioni:

1. Includete file JAR client, ad esempio adobe-forms-client.jar, nel percorso di classe del progetto Java. Per informazioni sulla posizione di questi file, consultate [Inclusione  file](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)libreria AEM Forms Java.
1. Recuperare il valore del pulsante di scelta inviato dal modulo HTML e specificare se utilizzare dati americani o canadesi. Se viene inviato American, creare un `com.adobe.idp.Document` oggetto che memorizza i dati presenti nel file *Purchase Order US.xml*. Analogamente, se canadese, creare un `com.adobe.idp.Document` che memorizza i dati presenti nel file *Purchase Order Canada.xml* .
1. Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione. (Vedere [Impostazione delle proprietà](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)di connessione.)
1. Creare un `FormsServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.
1. Creare un `URLSpec` oggetto che memorizza i valori URI utilizzando il relativo costruttore.
1. Richiamate il metodo dell&#39; `URLSpec` oggetto `setApplicationWebRoot` e passate un valore di stringa che rappresenta la radice Web dell&#39;applicazione.
1. Richiamate il metodo dell&#39; `URLSpec` oggetto `setContentRootURI` e passate un valore di stringa che specifica il valore URI della radice del contenuto. Verificare che la struttura del modulo e i frammenti si trovino nell&#39;URI principale del contenuto. In caso contrario, il servizio Forms genera un&#39;eccezione. Per fare riferimento all&#39;archivio AEM Forms , specificare `repository://`.
1. Richiamare il metodo dell&#39; `URLSpec` oggetto `setTargetURL` e passare un valore di stringa che specifica il valore dell&#39;URL di destinazione in cui vengono inviati i dati del modulo. Se si definisce l&#39;URL di destinazione nella struttura del modulo, è possibile passare una stringa vuota. È inoltre possibile specificare l&#39;URL al quale viene inviato il modulo per eseguire i calcoli.
1. Richiama il metodo dell’ `FormsServiceClient` oggetto `renderPDFForm` e passa i seguenti valori:

   * Una stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file.
   * Un `com.adobe.idp.Document` oggetto che contiene i dati da unire al modulo (creato nel passaggio 2).
   * Un `PDFFormRenderSpec` oggetto che memorizza le opzioni di esecuzione. Per ulteriori informazioni, consultate [Guida di riferimento](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)delle API di AEM Forms.
   * Un `URLSpec` oggetto che contiene valori URI richiesti dal servizio Forms per eseguire il rendering di un modulo basato su frammenti.
   * Un `java.util.HashMap` oggetto che memorizza gli allegati. Si tratta di un parametro facoltativo e potete specificare `null` se non desiderate allegare file al modulo.

   Il `renderPDFForm` metodo restituisce un `FormsResult` oggetto che contiene un flusso di dati del modulo che deve essere scritto nel browser Web del client.

1. Creare un `com.adobe.idp.Document` oggetto richiamando il `FormsResult` metodo ‘s `getOutputContent` .
1. Ottenere il tipo di contenuto dell&#39; `com.adobe.idp.Document` oggetto richiamandone il `getContentType` metodo.
1. Impostare il tipo di contenuto dell&#39; `javax.servlet.http.HttpServletResponse` oggetto richiamandone `setContentType` il metodo e passando il tipo di contenuto dell&#39; `com.adobe.idp.Document` oggetto.
1. Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser Web del client richiamando il `javax.servlet.http.HttpServletResponse` metodo dell&#39; `getOutputStream` oggetto.
1. Creare un `java.io.InputStream` oggetto richiamando il `com.adobe.idp.Document` metodo dell&#39; `getInputStream` oggetto.
1. Per creare un array di byte, è necessario inserirlo nel flusso di dati del modulo richiamando il `InputStream` `read`metodo dell&#39;oggetto e passando l&#39;array di byte come argomento.
1. Richiamare il metodo dell&#39; `javax.servlet.ServletOutputStream` oggetto `write` per inviare il flusso di dati del modulo al browser Web del client. Passa l&#39;array di byte al `write` metodo.

L&#39;esempio di codice seguente rappresenta il servlet Java che richiama il servizio Forms ed esegue il rendering di un modulo basato sui frammenti.

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.File;
 import java.io.FileInputStream;
 import java.io.IOException;
 import java.io.PrintWriter;
 
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.InputStream;
 import java.net.URL;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RenderFormFragment extends HttpServlet implements Servlet {
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
             doPost(req,resp);
 
     }
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
     throws ServletException, IOException {
 
 
 
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Get the value of selected radio button
             String radioValue = req.getParameter("radio");
 
             //Create an Document object to store form data
             Document oInputData = null;
 
             //The value of the radio button determines the form data to use
             //which determines which fragments used in the form
             if (radioValue.compareTo("AMERICAN") == 0)            {
                 FileInputStream myData = new FileInputStream("C:\\Adobe\Purchase Order US.xml");
                 oInputData = new Document(myData);
             }
             else if (radioValue.compareTo("CANADIAN") == 0)            {
                 FileInputStream myData = new FileInputStream("C:\\Adobe\Purchase Order Canada.xml");
                 oInputData = new Document(myData);
             }
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Set the parameter values for the renderPDFForm method
             String formName = "Applications/FormsApplication/1.0/FormsFolder/Purchase Order Dynamic.xdp";
 
             //Cache the PDF form
             PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec();
             pdfFormRenderSpec.setCacheEnabled(new Boolean(true));
 
             //Specify URI values that are required to render a form
             //design based on fragments
             URLSpec uriValues = new URLSpec();
             uriValues.setApplicationWebRoot("https://'[server]:[port]'/RenderFormFragment");
             uriValues.setContentRootURI("repository:///");
             uriValues.setTargetURL("https://'[server]:[port]'/FormsServiceClientApp/HandleData");
 
             //Invoke the renderPDFForm method and write the
             //results to a client web browser
             FormsResult formOut = formsClient.renderPDFForm(
                         formName,               //formQuery
                         oInputData,             //inDataDoc
                         pdfFormRenderSpec,      //PDFFormRenderSpec
                         uriValues,                //urlSpec
                         null                    //attachments
                         );
 
             //Create a Document object that stores form data
             Document myData = formOut.getOutputContent();
 
             //Get the content type of the response and
             //set the HttpServletResponse object’s content type
             String contentType = myData.getContentType();
             resp.setContentType(contentType);
 
             //Create a ServletOutputStream object
             ServletOutputStream oOutput = resp.getOutputStream();
 
             //Create an InputStream object
             InputStream inputStream = myData.getInputStream();
 
             //Write the data stream to the web browser
             byte[] data = new byte[4096];
             int bytesRead = 0;
             while ((bytesRead = inputStream.read(data)) > 0)
             {
                 oOutput.write(data, 0, bytesRead);
             }
 
         }catch (Exception e) {
              System.out.println("The following exception occurred: "+e.getMessage());
       }
     }
 }
```

### Creazione di una pagina Web {#creating-the-web-page}

La pagina Web index.html fornisce un punto di ingresso al servlet Java e richiama il servizio Forms. Questa pagina Web è un modulo HTML di base che contiene due pulsanti di scelta e un pulsante di invio. Il nome dei pulsanti di scelta è una scelta. Quando l&#39;utente fa clic sul pulsante di invio, i dati del modulo vengono inviati al servlet `RenderFormFragment` Java.

Il servlet Java acquisisce i dati inviati dalla pagina HTML utilizzando il seguente codice Java:

```java
             Document oInputData = null;
 
             //Get the value of selected radio button
             String radioValue = req.getParameter("radio");
 
             //The value of the radio button determines the form data to use
             //which determines which fragments used in the form
             if (radioValue.compareTo("AMERICAN") == 0)            {
                 FileInputStream myData = new FileInputStream("C:\\Adobe\Purchase Order US.xml");
                 oInputData = new Document(myData);
             }
             else if (radioValue.compareTo("CANADIAN") == 0)            {
                 FileInputStream myData = new FileInputStream("C:\\Adobe\Purchase Order Canada.xml");
                 oInputData = new Document(myData);
             }
```

Il seguente codice HTML si trova nel file index.html creato durante l&#39;impostazione dell&#39;ambiente di sviluppo. Consultate [Creazione di un progetto](/help/forms/developing/rendering-forms.md#creating-a-web-project)Web.

```xml
 <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
 <html xmlns="https://www.w3.org/1999/xhtml">
 <head>
 <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
 <title>Untitled Document</title>
 </head>
 
 <body>
 <form name="myform" action="https://'[server]:[port]'/FragmentsWebApplication/RenderFormFragment" method="post">
      <table>
      <tr>
        <th>Forms Fragment Web Client</th>
      </tr>
      <tr>
        <td>
          <label>
          <input type="radio" name="radio" id="radio_Data" value="CANADIAN" />
          Canadian data<br />
          </label>
          <p>
            <label>
            <input type="radio" name="radio" id="radio_Data" value="AMERICAN" checked/>
            American data</label>
          </p>
        </td>
      </tr>
      <tr>
      <td>
        <label>
          <input type="submit" name="button_Submit" id="button_Submit" value="Submit" />
            </label>
            </td>
         </tr>
        </table>
      </form>
 </body>
 </html>
```

### Creazione del pacchetto dell&#39;applicazione Web {#packaging-the-web-application}

Per distribuire il servlet Java che richiama il servizio Forms, creare un pacchetto dell&#39;applicazione Web in un file WAR. Assicurati che nel file WAR siano inclusi anche i file JAR esterni da cui dipende la logica aziendale del componente, come adobe-livecycle-client.jar e adobe-forms-client.jar.

**Per creare un pacchetto di un&#39;applicazione Web in un file WAR:**

1. Nella finestra **Esplora** progetti, fare clic con il pulsante destro del mouse sul `FragmentsWebApplication` progetto e selezionare **Esporta** > File **** WAR.
1. Nella casella di testo del modulo **** Web, digitare `FragmentsWebApplication` il nome del progetto Java.
1. Nella casella di testo **Destinazione** , digitare `FragmentsWebApplication.war`**il nome del** file, specificare il percorso del file WAR, quindi fare clic su Fine.

### Distribuzione del file WAR nel server applicazioni J2EE {#deploying-the-war-file-to-the-j2ee-application-server}

È possibile distribuire il file WAR al server applicazione J2EE su cui è distribuito  AEM Forms. Dopo la distribuzione del file WAR, è possibile accedere alla pagina Web HTML utilizzando un browser Web.

**Per distribuire il file WAR al server applicazione J2EE:**

* Copiare il file WAR dal percorso di esportazione a `[Forms Install]\Adobe\Adobe Experience Manager Forms\jboss\server\all\deploy`.

### Verifica dell’applicazione Web {#testing-your-web-application}

Dopo aver implementato l&#39;applicazione Web, potete verificarla utilizzando un browser Web. Presupponendo di utilizzare lo stesso computer in cui è installato  AEM Forms, potete specificare il seguente URL:

* http://localhost:8080/FragmentsWebApplication/index.html

   Selezionare un pulsante di scelta e fare clic sul pulsante Invia. Nel browser Web viene visualizzato un modulo basato sui frammenti. Se si verificano dei problemi, consultare il file di registro del server applicazione J2EE.

