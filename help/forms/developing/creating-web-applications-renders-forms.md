---
title: Creazione di applicazioni Web per il rendering di Forms
description: Creare un’applicazione basata sul web che utilizza servlet Java per richiamare il servizio Forms ed eseguire il rendering dei moduli. Il servlet Java funge da collegamento tra il servizio Forms che restituisce un modulo e un browser web client.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 85e00003-8c8b-463a-b728-66af174be295
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Workbench,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1832'
ht-degree: 0%

---

# Creazione di applicazioni Web per il rendering di Forms {#creating-web-applications-thatrenders-forms}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

## Creazione di applicazioni Web per il rendering di Forms {#creating-web-applications-that-renders-forms}

Puoi creare un’applicazione basata sul web che utilizza servlet Java per richiamare il servizio Forms ed eseguire il rendering dei moduli. Un vantaggio dell’utilizzo di un servlet Java™ è la possibilità di scrivere il valore restituito dal processo in un browser web client. In altre parole, un servlet Java può essere utilizzato come collegamento tra il servizio Forms che restituisce un modulo e un browser web client.

>[!NOTE]
>
>Questa sezione descrive come creare un’applicazione basata sul web che utilizza un servlet Java che richiama il servizio Forms ed esegue il rendering dei moduli basati su frammenti. (vedere [Rendering di Forms basato su frammenti](/help/forms/developing/rendering-forms-based-fragments.md).)

Utilizzando un servlet Java, è possibile scrivere un modulo in un browser Web client in modo che un cliente possa visualizzare e immettere dati nel modulo. Dopo aver inserito i dati nel modulo, l’utente web fa clic su un pulsante di invio nel modulo per inviare nuovamente le informazioni al servlet Java, dove è possibile recuperare ed elaborare i dati. Ad esempio, i dati possono essere inviati a un altro processo.

Questa sezione illustra come creare un&#39;applicazione basata sul Web che consenta all&#39;utente di selezionare i dati di un modulo basato su moduli americani o su moduli basati su canadesi, come illustrato nella figura seguente.

![cw_cw_fragmentwebclient](assets/cw_cw_fragmentwebclient.png)

Il modulo di cui viene eseguito il rendering è un modulo basato su frammenti. In altre parole, se l’utente seleziona dati americani, il modulo restituito utilizza frammenti basati su dati americani. Ad esempio, il piè di pagina del modulo contiene un indirizzo americano, come illustrato nella figura seguente.

![cw_cw_fragementformfooter](assets/cw_cw_fragementformfooter.png)

Analogamente, se l&#39;utente seleziona dati canadesi, il modulo restituito contiene un indirizzo canadese, come illustrato nella figura seguente.

![cw_cw_fragementformfootercnd](assets/cw_cw_fragementformfootercnd.png)

>[!NOTE]
>
>Per informazioni sulla creazione di strutture di moduli basate su frammenti, vedere [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

**File di esempio**

In questa sezione vengono utilizzati file di esempio che possono trovarsi nel percorso seguente:

&lt;*Directory di installazione di Forms Designer*>/Samples/Forms/Purchase Order/Form Fragments (Frammenti di ordini di acquisto/moduli)

dove &lt;*directory di installazione*> è il percorso di installazione. Ai fini dell’applicazione client, il file Purchase Order Dynamic.xdp è stato copiato da questa posizione di installazione e distribuito in un’applicazione Forms denominata *Applicazioni/FormsApplication*. Il file Dynamic.xdp dell’ordine di acquisto viene inserito in una cartella denominata FormsFolder. Analogamente, i frammenti vengono inseriti nella cartella Frammenti, come illustrato nella figura seguente.

![cw_cw_fragmentsrepository](assets/cw_cw_fragmentsrepository.png)

Per accedere alla progettazione del modulo Dynamic.xdp dell’ordine di acquisto, specifica `Applications/FormsApplication/1.0/FormsFolder/Purchase Order Dynamic.xdp` come nome del modulo (il primo parametro trasmesso al `renderPDFForm` metodo) e `repository:///` come valore URI della directory principale del contenuto.

I file di dati XML utilizzati dall&#39;applicazione Web sono stati spostati dalla cartella Dati a `C:\Adobe`(il file system che appartiene al server applicazioni J2EE che ospita AEM Forms). I nomi dei file sono Ordine di acquisto *Canada.xml* e ordine di acquisto *US.xml*.

>[!NOTE]
>
>Per informazioni sulla creazione di un’applicazione Forms tramite Workbench, consulta [Guida di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per creare un’applicazione basata sul web che esegua il rendering dei moduli basati su frammenti, effettua le seguenti operazioni:

1. Crea un progetto web.
1. Creare la logica dell’applicazione Java che rappresenta il servlet Java.
1. Crea la pagina web per l’applicazione web.
1. Creare un pacchetto dell’applicazione web in un file WAR.
1. Distribuire il file WAR sul server applicazioni J2EE.
1. Verifica l’applicazione web.

>[!NOTE]
>
>Alcuni di questi passaggi dipendono dall’applicazione J2EE su cui viene distribuito AEM Forms. Ad esempio, il metodo utilizzato per distribuire un file WAR dipende dal server applicazioni J2EE in uso. Questa sezione presuppone che AEM Forms sia implementato su JBoss®.

### Creazione di un progetto web {#creating-a-web-project}

Il primo passaggio per creare un’applicazione web che contiene un servlet Java in grado di richiamare il servizio Forms consiste nella creazione di un progetto web. L’IDE Java su cui si basa questo documento è Eclipse 3.3. Utilizzando l’IDE Eclipse, crea un progetto web e aggiungi al progetto i file JAR richiesti. Infine, aggiungi una pagina HTML denominata *index.html* e un servlet Java per il progetto.

L’elenco seguente specifica i file JAR da aggiungere al progetto web:

* adobe-forms-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar

Per il percorso di questi file JAR, vedi [Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Per creare un progetto Web:**

1. Avvia Eclipse e fai clic su **File** >  **Nuovo progetto**.
1. In **Nuovo progetto** finestra di dialogo, seleziona **Web** > **Progetto Web dinamico**.
1. Tipo `FragmentsWebApplication` per il nome del progetto, quindi fai clic su **Fine**.

**Per aggiungere al progetto i file JAR richiesti:**

1. Nella finestra Esplora progetti, fare clic con il pulsante destro del mouse sulla `FragmentsWebApplication` progetto e selezione **Proprietà**.
1. Clic **Percorso build Java** e quindi fare clic su **Librerie** scheda.
1. Fai clic su **Aggiungi JAR esterni** e individuare i file JAR da includere.

**Per aggiungere un servlet Java al progetto:**

1. Nella finestra Esplora progetti, fare clic con il pulsante destro del mouse sulla `FragmentsWebApplication` progetto e selezione **Nuovo** >  **Altro**.
1. Espandi **Web** cartella, seleziona **Servlet** e quindi fare clic su **Successivo**.
1. Nella finestra di dialogo Crea servlet digitare `RenderFormFragment` per il nome del servlet, quindi fai clic su **Fine**.

**Per aggiungere una pagina HTML al progetto:**

1. Nella finestra Esplora progetti, fare clic con il pulsante destro del mouse sulla `FragmentsWebApplication` progetto e selezione **Nuovo** > **Altro**.
1. Espandi **Web** cartella, seleziona **HTML** e fai clic su **Successivo**.
1. Nella finestra di dialogo Nuovo HTML digitare `index.html` per il nome del file, quindi fare clic su **Fine**.

>[!NOTE]
>
>Per informazioni sulla creazione della pagina HTML che richiama `RenderFormFragment` Servlet Java, vedi [Creazione della pagina web](/help/forms/developing/rendering-forms.md#creating-the-web-page).

### Creazione della logica dell’applicazione Java per il servlet {#creating-java-application-logic-for-the-servlet}

Puoi creare una logica dell’applicazione Java che richiama il servizio Forms dall’interno del servlet Java. Il codice seguente mostra la sintassi del `RenderFormFragment` Servlet Java:

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

Normalmente, non inserisci il codice client all’interno di un servlet Java `doGet` o `doPost` metodo. Una migliore pratica di programmazione consiste nel posizionare questo codice all&#39;interno di una classe separata, creare un&#39;istanza della classe dall&#39;interno di `doPost` metodo (o `doGet` e chiamare i metodi appropriati. Tuttavia, per brevità del codice, gli esempi di codice in questa sezione sono limitati al minimo e gli esempi di codice vengono inseriti nel `doPost` metodo.

Per eseguire il rendering di un modulo basato su frammenti utilizzando l’API di servizio Forms, esegui le seguenti attività:

1. Includi i file JAR client, ad esempio adobe-forms-client.jar, nel percorso di classe del progetto Java. Per informazioni sulla posizione di questi file, vedere [Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).
1. Recupera il valore del pulsante di opzione inviato dal modulo HTML e specifica se utilizzare i dati americani o canadesi. Se viene inviato American, crea un `com.adobe.idp.Document` che memorizza i dati in *Ordine di acquisto US.xml*. Allo stesso modo, se canadese, crea un `com.adobe.idp.Document` che memorizza i dati in *Ordine di acquisto Canada.xml* file.
1. Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione. (vedere [Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
1. Creare un `FormsServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.
1. Creare un `URLSpec` oggetto che memorizza i valori URI utilizzando il relativo costruttore.
1. Richiama `URLSpec` dell&#39;oggetto `setApplicationWebRoot` e passa un valore stringa che rappresenta la directory principale del web dell’applicazione.
1. Richiama `URLSpec` dell&#39;oggetto `setContentRootURI` e passa un valore stringa che specifica il valore URI della directory principale del contenuto. Assicurati che la progettazione del modulo e i frammenti siano nell’URI della directory principale del contenuto. In caso contrario, il servizio Forms genera un&#39;eccezione. Per fare riferimento all’archivio AEM Forms, specifica `repository://`.
1. Richiama `URLSpec` dell&#39;oggetto `setTargetURL` e passa un valore stringa che specifica il valore dell&#39;URL di destinazione in cui vengono pubblicati i dati del modulo. Se definisci l’URL di destinazione nella progettazione del modulo, puoi trasmettere una stringa vuota. È inoltre possibile specificare l&#39;URL a cui viene inviato un modulo per eseguire i calcoli.
1. Richiama `FormsServiceClient` dell&#39;oggetto `renderPDFForm` e trasmettere i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file.
   * A `com.adobe.idp.Document` oggetto contenente i dati da unire con il modulo (creato nel passaggio 2).
   * A `PDFFormRenderSpec` oggetto che memorizza le opzioni di runtime. Per ulteriori informazioni, consulta [Riferimento API di AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * A `URLSpec` oggetto contenente valori URI richiesti dal servizio Forms per eseguire il rendering di un modulo basato su frammenti.
   * A `java.util.HashMap` oggetto che memorizza gli allegati. Questo è un parametro facoltativo e puoi specificare `null` se non si desidera allegare file al modulo.

   Il `renderPDFForm` il metodo restituisce un `FormsResult` oggetto contenente un flusso di dati modulo che deve essere scritto nel browser web client.

1. Creare un `com.adobe.idp.Document` oggetto richiamando il `FormsResult` oggetto &quot;s `getOutputContent` metodo.
1. Ottieni il tipo di contenuto del `com.adobe.idp.Document` oggetto richiamando il relativo `getContentType` metodo.
1. Imposta il `javax.servlet.http.HttpServletResponse` tipo di contenuto dell&#39;oggetto richiamando il relativo `setContentType` e passando il tipo di contenuto del `com.adobe.idp.Document` oggetto.
1. Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser web client richiamando `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream` metodo.
1. Creare un `java.io.InputStream` oggetto richiamando il `com.adobe.idp.Document` dell&#39;oggetto `getInputStream` metodo.
1. Creare una matrice di byte compilarla con il flusso di dati del modulo richiamando `InputStream` dell&#39;oggetto `read`e passando la matrice di byte come argomento.
1. Richiama `javax.servlet.ServletOutputStream` dell&#39;oggetto `write` metodo per inviare il flusso di dati del modulo al browser web client. Passare la matrice di byte al `write` metodo.

Esempio Nell&#39;esempio di codice riportato di seguito viene rappresentato il servlet Java che richiama il servizio Forms ed esegue il rendering di un modulo basato su frammenti.

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
     * These JAR files are in the following path:
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

### Creazione della pagina web {#creating-the-web-page}

La pagina web index.html fornisce un punto di ingresso al servlet Java e richiama il servizio Forms. Questa pagina Web è un modulo HTML di base che contiene due pulsanti di scelta e un pulsante di invio. Il nome dei pulsanti di scelta è radio. Quando l’utente fa clic sul pulsante di invio, i dati del modulo vengono inviati al `RenderFormFragment` Servlet Java.

Il servlet Java acquisisce i dati pubblicati dalla pagina HTML utilizzando il seguente codice Java:

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

Il seguente codice HTML si trova nel file index.html creato durante la configurazione dell’ambiente di sviluppo. (vedere [Creazione di un progetto web](/help/forms/developing/rendering-forms.md#creating-a-web-project).)

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

### Creazione di pacchetti dell’applicazione web {#packaging-the-web-application}

Per distribuire il servlet Java che richiama il servizio Forms, crea un pacchetto dell’applicazione web in un file WAR. Assicurati che nel file WAR siano inclusi anche i file JAR esterni da cui dipende la logica di business del componente, come adobe-livecycle-client.jar e adobe-forms-client.jar.

**Per creare un pacchetto di un&#39;applicazione Web in un file WAR:**

1. Dalla sezione **Gestione progetti** fare clic con il pulsante destro del mouse sulla `FragmentsWebApplication` progetto e selezione **Esporta** > **File WAR**.
1. In **Modulo web** casella di testo, digitare `FragmentsWebApplication` per il nome del progetto Java.
1. In **Destinazione** casella di testo, digitare `FragmentsWebApplication.war`**per** nome file, specificare il percorso del file WAR e quindi fare clic su Fine.

### Distribuzione del file WAR sul server applicazioni J2EE {#deploying-the-war-file-to-the-j2ee-application-server}

È possibile distribuire il file WAR sul server applicazioni J2EE sul quale viene distribuito AEM Forms. Dopo aver distribuito il file WAR, puoi accedere alla pagina web HTML utilizzando un browser web.

**Per distribuire il file WAR sul server applicazioni J2EE:**

* Copiare il file WAR dal percorso di esportazione in `[Forms Install]\Adobe\Adobe Experience Manager Forms\jboss\server\all\deploy`.

### Verifica dell’applicazione web {#testing-your-web-application}

Dopo aver distribuito l’applicazione web, puoi testarla utilizzando un browser web. Se utilizzi lo stesso computer che ospita AEM Forms, puoi specificare il seguente URL:

* http://localhost:8080/FragmentsWebApplication/index.html

  Selezionare un pulsante di opzione e fare clic sul pulsante Invia. Un modulo basato su frammenti verrà visualizzato nel browser Web. Se si verificano problemi, vedere il file di registro del server applicazioni J2EE.
