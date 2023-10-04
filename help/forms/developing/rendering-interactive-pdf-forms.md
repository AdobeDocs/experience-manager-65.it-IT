---
title: Rendering dei PDF forms interattivi
description: Utilizza il servizio Forms per eseguire il rendering dei PDF forms interattivi su dispositivi client, in genere browser web, per raccogliere informazioni dagli utenti. Puoi utilizzare il servizio Forms per eseguire il rendering dei moduli interattivi utilizzando l’API Java e l’API del servizio web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: d9f32939-c2c0-4531-b15e-f63941c289e3
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '2487'
ht-degree: 0%

---

# Rendering dei PDF forms interattivi {#rendering-interactive-pdf-forms}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

Il servizio Forms esegue il rendering dei PDF forms interattivi sui dispositivi client, in genere i browser web, per raccogliere informazioni dagli utenti. Dopo aver eseguito il rendering di un modulo interattivo, un utente può immettere i dati nei campi del modulo e fare clic su un pulsante di invio presente nel modulo per inviare nuovamente le informazioni al servizio Forms. Adobe Reader o Acrobat devono essere installati nel computer che ospita il browser web client per rendere visibile un modulo interattivo di PDF.

>[!NOTE]
>
>Prima di poter eseguire il rendering di un modulo utilizzando il servizio Forms, crea una progettazione del modulo. In genere, la progettazione di un modulo viene creata in Designer e salvata come file XDP. Per informazioni sulla creazione di una struttura di modulo, vedere [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63_it).

**Esempio di richiesta di prestito**

Viene introdotta un&#39;applicazione di prestito di esempio per dimostrare come il servizio Forms utilizza moduli interattivi per raccogliere informazioni dagli utenti. Questa applicazione consente a un utente di compilare un modulo con i dati necessari per ottenere un prestito e quindi di inviare i dati al servizio Forms. Il diagramma seguente mostra il flusso logico della richiesta di prestito.

![ri_ri_finsrv_loanapp_v1](assets/ri_ri_finsrv_loanapp_v1.png)

Nella tabella seguente vengono descritti i passaggi del diagramma.

<table>
 <thead>
  <tr>
   <th><p>Passaggio</p></th>
   <th><p>Descrizione</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>Il <code>GetLoanForm</code> Java Servlet viene richiamato da una pagina HTML. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Il <code>GetLoanForm</code> Java Servlet utilizza l’API client del servizio Forms per eseguire il rendering del modulo di prestito sul browser web client. (vedere <a href="#render-an-interactive-pdf-form-using-the-java-api">Eseguire il rendering di un modulo PDF interattivo tramite l’API Java</a>.)</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Dopo che l’utente compila il modulo del prestito e fa clic sul pulsante di invio, i dati vengono inviati al <code>HandleData</code> Servlet Java. (vedere <i>"Modulo di prestito"</i>.)</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Il <code>HandleData</code> Java Servlet utilizza l’API client del servizio Forms per elaborare l’invio del modulo e recuperare i dati del modulo. I dati vengono quindi memorizzati in un database aziendale. (vedere <a href="/help/forms/developing/handling-submitted-forms.md#handling-submitted-forms">Gestione dei Forms inviati</a>.)</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>Viene eseguito il rendering di un modulo di conferma sul browser web. Dati quali il nome e il cognome dell'utente vengono uniti al modulo prima che questo venga sottoposto a rendering. (vedere <a href="/help/forms/developing/prepopulating-forms-flowable-layouts.md">Precompilazione di Forms con layout fluibili</a>.)</p></td>
  </tr>
 </tbody>
</table>

**Modulo di prestito**

Questo modulo di prestito interattivo è reso dalla richiesta di prestito campione `GetLoanForm` Servlet Java.

![ri_ri_loanform](assets/ri_ri_loanform.png)

**Modulo di conferma**

Il modulo è fornito dalla richiesta di prestito di esempio `HandleData` Servlet Java.

![ri_ri_confirm](assets/ri_ri_confirm.png)

Il `HandleData` Java Servlet precompila questo modulo con il nome e il cognome dell’utente e l’importo. Una volta precompilato, il modulo viene inviato al browser Web client. (vedere [Precompilazione di Forms con layout fluibili](/help/forms/developing/prepopulating-forms-flowable-layouts.md))

**Servlet Java**

L’esempio di applicazione di prestito è un esempio di applicazione di servizio Forms esistente come servlet Java. Un servlet Java è un programma Java in esecuzione su un server applicazioni J2EE, come WebSphere, e contiene il codice API client del servizio Forms.

Il codice seguente mostra la sintassi di un servlet Java denominato GetLoanForm:

```java
     public class GetLoanForm extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

             }
```

Normalmente, non inserisci il codice API client del servizio Forms all’interno di un servlet Java `doGet` o `doPost` metodo. È consigliabile programmare questo codice all&#39;interno di una classe separata, creare un&#39;istanza della classe dall&#39;interno di `doPost` metodo (o `doGet` e chiamare i metodi appropriati. Tuttavia, per brevità del codice, gli esempi di codice in questa sezione sono limitati al minimo e gli esempi di codice vengono inseriti nel `doPost` metodo.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

**Riepilogo dei passaggi**

Per eseguire il rendering di un modulo PDF interattivo, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Crea un oggetto API client di Forms.
1. Specifica i valori URI.
1. Allega file al modulo (facoltativo).
1. Eseguire il rendering di un modulo PDF interattivo.
1. Scrivere il flusso di dati del modulo nel browser Web client.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un oggetto API client di Forms**

Prima di poter eseguire un&#39;operazione API client di un servizio Forms a livello di programmazione, è necessario creare un oggetto API client Forms. Se utilizzi l’API Java, crea un’ `FormsServiceClient` oggetto. Se utilizzi l’API del servizio web Forms, crea un’ `FormsService` oggetto.

**Specificare i valori URI**

È possibile specificare i valori URI richiesti dal servizio Forms per il rendering di un modulo. È possibile fare riferimento a una progettazione di modulo salvata come parte di un’applicazione Forms utilizzando il valore URI della directory principale del contenuto `repository:///`. Si consideri, ad esempio, la struttura di modulo seguente denominata *Loan.xdp* si trova all’interno di un’applicazione Forms denominata *FormsApplication*:

![ri_ri_formrepository](assets/ri_ri_formrepository.png)

Per accedere a questa struttura di modulo, specifica `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp` come nome del modulo (il primo parametro trasmesso al `renderPDFForm` metodo) e `repository:///` come valore URI della directory principale del contenuto.

>[!NOTE]
>
>Per informazioni sulla creazione di un’applicazione Forms tramite Workbench, consulta [Guida di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

Il percorso di una risorsa che si trova in un’applicazione Forms è:

`Applications/Application-name/Application-version/Folder.../Filename`

I seguenti valori mostrano alcuni esempi di valori URI:

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

Quando esegui il rendering di un modulo interattivo, puoi definire valori URI come l’URL di destinazione in cui vengono pubblicati i dati del modulo. L’URL di destinazione può essere definito in uno dei seguenti modi:

* Sul pulsante Invia durante la progettazione della struttura del modulo in Designer
* Utilizzando l’API client del servizio Forms

Se l’URL di destinazione è definito nella progettazione del modulo, non eseguirne l’override con l’API client del servizio Forms. In altre parole, impostando l’URL di destinazione utilizzando l’API di Forms, l’URL specificato nella progettazione del modulo viene reimpostato su quello specificato utilizzando l’API. Se desideri inviare il modulo PDF all’URL di destinazione specificato nella progettazione del modulo, imposta a livello di programmazione l’URL di destinazione su una stringa vuota.

Se si dispone di un modulo contenente un pulsante di invio e un pulsante di calcolo (con uno script corrispondente in esecuzione sul server), è possibile definire a livello di programmazione l&#39;URL a cui inviare il modulo per eseguire lo script. Utilizza il pulsante Invia nella struttura del modulo per specificare l’URL in cui vengono pubblicati i dati del modulo. (vedere [Calcolo dati modulo](/help/forms/developing/calculating-form-data.md).)

>[!NOTE]
>
>Invece di specificare un valore URL per fare riferimento a un file XDP, puoi anche trasmettere un `com.adobe.idp.Document` al servizio Forms. Il `com.adobe.idp.Document` L&#39;istanza contiene una struttura di modulo. (vedere [Trasmissione di documenti al servizio Forms](/help/forms/developing/passing-documents-forms-service.md).)

**Allega file al modulo**

È possibile allegare file a un modulo. Quando si esegue il rendering di un modulo PDF con file allegati, gli utenti possono recuperare i file allegati in Acrobat utilizzando il riquadro dei file allegati. È possibile allegare tipi di file diversi a un modulo, ad esempio un file di testo, oppure a un file binario, ad esempio un file JPG.

>[!NOTE]
>
>L&#39;aggiunta di allegati a un modulo è facoltativa.

**Rendering di un modulo PDF interattivo**

Per eseguire il rendering di un modulo, utilizza una struttura di modulo creata in Designer e salvata come file XDP o PDF. È inoltre possibile eseguire il rendering di un modulo creato con Acrobat e salvato come file PDF. Per eseguire il rendering di un modulo di PDF interattivo, richiama `FormsServiceClient` dell&#39;oggetto `renderPDFForm` metodo o `renderPDFForm2` metodo.

Il `renderPDFForm` utilizza un `URLSpec` oggetto. La directory principale del contenuto del file XDP viene passata al servizio Forms utilizzando `URLSpec` dell&#39;oggetto `setContentRootURI` metodo. Il nome della struttura del modulo ( `formQuery`) viene passato come valore di parametro separato. I due valori vengono concatenati per ottenere il riferimento assoluto alla progettazione del modulo.

Il `renderPDFForm2` il metodo accetta un `com.adobe.idp.Document` istanza che contiene il documento XDP o PDF da riprodurre.

>[!NOTE]
>
>Impossibile impostare l&#39;opzione di runtime PDF con tag se il documento di input è un documento PDF. Se il file di input è un file XDP, è possibile impostare l&#39;opzione PDF con tag.

## Eseguire il rendering di un modulo PDF interattivo tramite l’API Java {#render-an-interactive-pdf-form-using-the-java-api}

Esegui il rendering di un modulo PDF interattivo utilizzando l’API Forms (Java):

1. Includi file di progetto

   Includi i file JAR client, ad esempio adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client di Forms

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `FormsServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Specificare i valori URI

   * Creare un `URLSpec` oggetto che memorizza i valori URI utilizzando il relativo costruttore.
   * Richiama `URLSpec` dell&#39;oggetto `setApplicationWebRoot` e passare un valore string che rappresenta la radice web dell&#39;applicazione.
   * Richiama `URLSpec` dell&#39;oggetto `setContentRootURI` e passa un valore stringa che specifica il valore URI della directory principale del contenuto. Assicurati che la progettazione del modulo si trovi nell’URI della directory principale del contenuto. In caso contrario, il servizio Forms genera un&#39;eccezione. Per fare riferimento all’archivio, specifica `repository:///`.
   * Richiama `URLSpec` dell&#39;oggetto `setTargetURL` e passa un valore stringa che specifica il valore dell&#39;URL di destinazione in cui vengono pubblicati i dati del modulo. Se definisci l’URL di destinazione nella progettazione del modulo, puoi trasmettere una stringa vuota. Per eseguire i calcoli, è inoltre possibile specificare l&#39;URL a cui viene inviato un modulo.

1. Allega file al modulo

   * Creare un `java.util.HashMap` oggetto per memorizzare gli allegati utilizzando il relativo costruttore.
   * Richiama `java.util.HashMap` dell&#39;oggetto `put` metodo per ciascun file da allegare al modulo sottoposto a rendering. Passa i seguenti valori a questo metodo:

      * Valore stringa che specifica il nome del file allegato, inclusa l&#39;estensione.

   * A `com.adobe.idp.Document` oggetto che contiene il file allegato.

   >[!NOTE]
   >
   >Ripetere questo passaggio per ogni file da allegare al modulo. Questo passaggio è facoltativo e puoi trasmettere `null` se non si desidera inviare file allegati.

1. Rendering di un modulo PDF interattivo

   Richiama `FormsServiceClient` dell&#39;oggetto `renderPDFForm` e trasmettere i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura di modulo che fa parte di un&#39;applicazione Forms, assicurarsi di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `com.adobe.idp.Document` oggetto contenente dati da unire con il modulo. Se non desideri unire i dati, passa un campo vuoto `com.adobe.idp.Document` oggetto.
   * A `PDFFormRenderSpec` oggetto che memorizza le opzioni di runtime. Questo è un parametro facoltativo e puoi specificare `null` se non si desidera specificare le opzioni di runtime.
   * A `URLSpec` oggetto contenente valori URI richiesti dal servizio Forms.
   * A `java.util.HashMap` oggetto che memorizza gli allegati. Questo è un parametro facoltativo e puoi specificare `null` se non si desidera allegare file al modulo.

   Il `renderPDFForm` il metodo restituisce un `FormsResult` oggetto contenente un flusso di dati modulo che deve essere scritto nel browser web client.

1. Scrivere il flusso di dati del modulo nel browser Web client

   * Creare un `com.adobe.idp.Document` oggetto richiamando il `FormsResult` dell&#39;oggetto `getOutputContent` metodo.
   * Ottieni il tipo di contenuto del `com.adobe.idp.Document` oggetto richiamando il relativo `getContentType` metodo.
   * Imposta il `javax.servlet.http.HttpServletResponse` tipo di contenuto dell&#39;oggetto richiamando il relativo `setContentType` e passando il tipo di contenuto del `com.adobe.idp.Document` oggetto.
   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser web client richiamando `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream` metodo.
   * Creare un `java.io.InputStream` oggetto richiamando il `com.adobe.idp.Document` dell&#39;oggetto `getInputStream` metodo.
   * Creare una matrice di byte e popolarla con il flusso di dati del modulo richiamando `InputStream` dell&#39;oggetto `read` e passando la matrice di byte come argomento.
   * Richiama `javax.servlet.ServletOutputStream` dell&#39;oggetto `write` metodo per inviare il flusso di dati del modulo al browser web client. Passare la matrice di byte al `write` metodo.

## Eseguire il rendering di un modulo PDF interattivo utilizzando l’API del servizio web {#render-an-interactive-pdf-form-using-the-web-service-api}

Esegui il rendering di un modulo PDF interattivo utilizzando l’API Forms (servizio web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio Forms WSDL.
   * Includi le classi proxy Java nel percorso della classe.

1. Creare un oggetto API client di Forms

   Creare un `FormsService` e impostare i valori di autenticazione.

1. Specificare i valori URI

   * Creare un `URLSpec` oggetto che memorizza i valori URI utilizzando il relativo costruttore.
   * Richiama `URLSpec` dell&#39;oggetto `setApplicationWebRoot` e passare un valore string che rappresenta la radice web dell&#39;applicazione.
   * Richiama `URLSpec` dell&#39;oggetto `setContentRootURI` e passa un valore stringa che specifica il valore URI della directory principale del contenuto. Assicurati che la progettazione del modulo si trovi nell’URI della directory principale del contenuto. In caso contrario, il servizio Forms genera un&#39;eccezione. Per fare riferimento all’archivio, specifica `repository:///`.
   * Richiama `URLSpec` dell&#39;oggetto `setTargetURL` e passa un valore stringa che specifica il valore dell&#39;URL di destinazione in cui vengono pubblicati i dati del modulo. Se definisci l’URL di destinazione nella progettazione del modulo, puoi trasmettere una stringa vuota. Per eseguire i calcoli, è inoltre possibile specificare l&#39;URL a cui viene inviato un modulo.

1. Allega file al modulo

   * Creare un `java.util.HashMap` oggetto per memorizzare gli allegati utilizzando il relativo costruttore.
   * Richiama `java.util.HashMap` dell&#39;oggetto `put` metodo per ciascun file da allegare al modulo sottoposto a rendering. Passa i seguenti valori a questo metodo:

      * Valore stringa che specifica il nome dell&#39;allegato, inclusa l&#39;estensione del nome file

   * A `BLOB` oggetto che contiene il file allegato

   >[!NOTE]
   >
   >Ripetere questo passaggio per ogni file da allegare al modulo.

1. Rendering di un modulo PDF interattivo

   Richiama `FormsService` dell&#39;oggetto `renderPDFForm` e trasmettere i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura di modulo che fa parte di un&#39;applicazione Forms, assicurarsi di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `BLOB` oggetto contenente dati da unire con il modulo. Se non si desidera unire i dati, passare `null`.
   * A `PDFFormRenderSpec` oggetto che memorizza le opzioni di runtime. Questo è un parametro facoltativo e puoi specificare `null` se non si desidera specificare le opzioni di runtime.
   * A `URLSpec` oggetto contenente valori URI richiesti dal servizio Forms.
   * A `java.util.HashMap` oggetto che memorizza gli allegati. Questo è un parametro facoltativo e puoi specificare `null` se non si desidera allegare file al modulo.
   * Un campo vuoto `com.adobe.idp.services.holders.BLOBHolder` oggetto popolato dal metodo. Viene utilizzato per memorizzare il modulo PDF di cui è stato eseguito il rendering.
   * Un campo vuoto `javax.xml.rpc.holders.LongHolder` oggetto popolato dal metodo. Questo argomento consente di memorizzare il numero di pagine nel modulo.
   * Un campo vuoto `javax.xml.rpc.holders.StringHolder` oggetto popolato dal metodo. Questo argomento consente di memorizzare il valore delle impostazioni locali.
   * Un campo vuoto `com.adobe.idp.services.holders.FormsResultHolder` oggetto che conterrà i risultati dell&#39;operazione.

   Il `renderPDFForm` il metodo compila `com.adobe.idp.services.holders.FormsResultHolder` oggetto passato come ultimo valore di argomento con un flusso di dati del modulo che deve essere scritto nel browser web client.

1. Scrivere il flusso di dati del modulo nel browser Web client

   * Creare un `FormResult` dell&#39;oggetto ottenendo il valore del `com.adobe.idp.services.holders.FormsResultHolder` dell&#39;oggetto `value` membro dati.
   * Creare un `BLOB` oggetto che contiene i dati del modulo richiamando `FormsResult` dell&#39;oggetto `getOutputContent` metodo.
   * Ottieni il tipo di contenuto del `BLOB` oggetto richiamando il relativo `getContentType` metodo.
   * Imposta il `javax.servlet.http.HttpServletResponse` tipo di contenuto dell&#39;oggetto richiamando il relativo `setContentType` e passando il tipo di contenuto del `BLOB` oggetto.
   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser web client richiamando `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream` metodo.
   * Creare una matrice di byte e popolarla richiamando il `BLOB` dell&#39;oggetto `getBinaryData` metodo. Questa attività assegna il contenuto del `FormsResult` alla matrice di byte.
   * Richiama `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `write` metodo per inviare il flusso di dati del modulo al browser web client. Passare la matrice di byte al `write` metodo.

**Scrivere il flusso di dati del modulo nel browser Web client**

Quando il servizio Forms esegue il rendering di un modulo, restituisce un flusso di dati del modulo che è necessario scrivere nel browser Web client. Quando viene scritto nel browser Web client, il modulo è visibile all&#39;utente.
