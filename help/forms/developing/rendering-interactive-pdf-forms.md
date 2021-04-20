---
title: Rendering di PDF forms interattivi
seo-title: Rendering di PDF forms interattivi
description: Utilizza il servizio Forms per eseguire il rendering dei PDF forms interattivi sui dispositivi client, in genere i browser web, per raccogliere informazioni dagli utenti. È possibile utilizzare il servizio Forms per eseguire il rendering dei moduli interattivi utilizzando l’API Java e l’API del servizio Web.
seo-description: Utilizza il servizio Forms per eseguire il rendering dei PDF forms interattivi sui dispositivi client, in genere i browser web, per raccogliere informazioni dagli utenti. È possibile utilizzare il servizio Forms per eseguire il rendering dei moduli interattivi utilizzando l’API Java e l’API del servizio Web.
uuid: df2a4dc8-f19e-49de-850f-85a204102631
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3cb307ec-9b7b-4f03-b860-48553ccee746
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2529'
ht-degree: 0%

---


# Rendering di PDF forms interattivi {#rendering-interactive-pdf-forms}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

Il servizio Forms esegue il rendering dei PDF forms interattivi su dispositivi client, in genere browser web, per raccogliere informazioni dagli utenti. Una volta eseguito il rendering di un modulo interattivo, l’utente può immettere i dati nei campi del modulo e fare clic su un pulsante di invio situato nel modulo per inviare le informazioni al servizio Forms. Affinché sia visibile un modulo PDF interattivo, è necessario installare Adobe Reader o Acrobat nel computer che ospita il browser Web client.

>[!NOTE]
>
>Prima di eseguire il rendering di un modulo utilizzando il servizio Forms, creare una struttura del modulo. In genere, una struttura del modulo viene creata in Designer e salvata come file XDP. Per informazioni sulla creazione di una struttura del modulo, vedere [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

**Domanda di prestito di esempio**

Viene introdotta un’applicazione di prestito di esempio per dimostrare come il servizio Forms utilizza moduli interattivi per raccogliere informazioni dagli utenti. Questa applicazione consente a un utente di compilare un modulo con i dati necessari per garantire un prestito e quindi di inviare i dati al servizio Forms. Il diagramma seguente illustra il flusso logico dell&#39;applicazione di prestito.

![ri_ri_finsrv_loanapp_v1](assets/ri_ri_finsrv_loanapp_v1.png)

La tabella seguente descrive i passaggi descritti in questo diagramma.

<table>
 <thead>
  <tr>
   <th><p>Incremento</p></th>
   <th><p>Descrizione</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>Il servlet Java <code>GetLoanForm</code> viene richiamato da una pagina HTML. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Il <code>GetLoanForm</code> Java Servlet utilizza l’API client del servizio Forms per eseguire il rendering del modulo di prestito sul browser web del client. (Vedere <a href="#render-an-interactive-pdf-form-using-the-java-api">Rendering di un modulo PDF interattivo utilizzando l'API Java</a>.)</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Dopo che l'utente compila il modulo di prestito e fa clic sul pulsante di invio, i dati vengono inviati al <code>HandleData</code> Java Servlet. (Vedere <i>"Modulo di prestito"</i>.)</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Il <code>HandleData</code> Java Servlet utilizza l’API client del servizio Forms per elaborare l’invio del modulo e recuperare i dati del modulo. I dati vengono quindi memorizzati in un database aziendale. (Consulta <a href="/help/forms/developing/handling-submitted-forms.md#handling-submitted-forms">Gestione dei Forms inviati</a>.)</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>Viene eseguito il rendering di un modulo di conferma nel browser web. I dati, come il nome e il cognome dell’utente, vengono uniti al modulo prima di eseguirne il rendering. (Consultare <a href="/help/forms/developing/prepopulating-forms-flowable-layouts.md">Precompilazione di Forms con layout fluidi</a>.)</p></td>
  </tr>
 </tbody>
</table>

**Modulo di prestito**

Questo modulo di prestito interattivo è reso dal `GetLoanForm` Java Servlet dell&#39;applicazione di prestito di esempio.

![ri_ri_loanform](assets/ri_ri_loanform.png)

**Modulo di conferma**

Questo modulo viene reso dal servlet Java `HandleData` dell&#39;applicazione di prestito di esempio.

![ri_ri_confirm](assets/ri_ri_confirm.png)

Il `HandleData` Java Servlet precompila questo modulo con il nome e il cognome dell’utente e la quantità. Dopo la precompilazione, il modulo viene inviato al browser Web client. (Consulta [Precompilazione di Forms con layout fluidi](/help/forms/developing/prepopulating-forms-flowable-layouts.md))

**Servlet Java**

L&#39;applicazione di prestito di esempio è un esempio di un&#39;applicazione di servizio Forms che esiste come servlet Java. Un servlet Java è un programma Java in esecuzione su un server applicativo J2EE, ad esempio WebSphere, e contiene il codice API client del servizio Forms.

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

Normalmente, non inserisci il codice API client del servizio Forms all&#39;interno del metodo `doGet` o `doPost` di un servlet Java. È consigliabile posizionare il codice all&#39;interno di una classe separata, creare un&#39;istanza della classe all&#39;interno del metodo `doPost` (o del metodo `doGet`) e chiamare i metodi appropriati. Tuttavia, per la brevità del codice, gli esempi di codice contenuti in questa sezione sono ridotti al minimo e gli esempi di codice vengono inseriti nel metodo `doPost` .

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, consulta [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

**Riepilogo dei passaggi**

Per eseguire il rendering di un modulo PDF interattivo, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Creare un oggetto API client Forms.
1. Specificare i valori URI.
1. Allegare file al modulo (facoltativo).
1. Eseguire il rendering di un modulo PDF interattivo.
1. Scrivere il flusso di dati del modulo sul browser Web client.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, assicurati di includere i file proxy.

**Creare un oggetto API client Forms**

Prima di poter eseguire un’operazione API client di Forms Service a livello di programmazione, è necessario creare un oggetto API client Forms. Se utilizzi l’API Java, crea un oggetto `FormsServiceClient`. Se utilizzi l’API del servizio Web Forms, crea un oggetto `FormsService`.

**Specificare i valori URI**

È possibile specificare i valori URI richiesti dal servizio Forms per il rendering di un modulo. Per fare riferimento a una struttura del modulo salvata come parte di un&#39;applicazione Forms, utilizzare il valore URI della directory principale contenuto `repository:///`. Ad esempio, considerare la seguente struttura del modulo denominata *Loan.xdp* situata all&#39;interno di un&#39;applicazione Forms denominata *FormsApplication*:

![ri_ri_formrepository](assets/ri_ri_formrepository.png)

Per accedere a questa struttura del modulo, specificare `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp` come nome del modulo (il primo parametro passato al metodo `renderPDFForm`) e `repository:///` come valore URI della directory principale del contenuto.

>[!NOTE]
>
>Per informazioni sulla creazione di un&#39;applicazione Forms tramite Workbench, vedere la [Guida di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

Il percorso di una risorsa situata in un&#39;applicazione Forms è:

`Applications/Application-name/Application-version/Folder.../Filename`

I seguenti valori mostrano alcuni esempi di valori URI:

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

Quando si esegue il rendering di un modulo interattivo, è possibile definire valori URI, ad esempio l’URL di destinazione in cui vengono inviati i dati del modulo. L’URL di destinazione può essere definito in uno dei seguenti modi:

* Pulsante Invia durante la progettazione della struttura del modulo in Designer
* Utilizzando l’API client del servizio Forms

Se l’URL di destinazione è definito all’interno della struttura del modulo, non sostituirlo con l’API client del servizio Forms. In altre parole, l’impostazione dell’URL di destinazione tramite l’API Forms reimposta l’URL specificato nella struttura del modulo su quello specificato utilizzando l’API. Se si desidera inviare il modulo PDF all’URL di destinazione specificato nella struttura del modulo, impostare programmaticamente l’URL di destinazione su una stringa vuota.

Se si dispone di un modulo che contiene un pulsante di invio e un pulsante di calcolo (con uno script corrispondente eseguito sul server), è possibile definire a livello di programmazione l’URL al quale viene inviato il modulo per eseguire lo script. Utilizzare il pulsante di invio nella struttura del modulo per specificare l’URL a cui vengono inviati i dati del modulo. (Vedere [Calcolo dei dati del modulo](/help/forms/developing/calculating-form-data.md).)

>[!NOTE]
>
>Invece di specificare un valore URL per fare riferimento a un file XDP, puoi anche passare un&#39;istanza `com.adobe.idp.Document` al servizio Forms. L’istanza `com.adobe.idp.Document` contiene una struttura del modulo. (Vedere [Trasmissione di documenti al servizio Forms](/help/forms/developing/passing-documents-forms-service.md).)

**Allegare file al modulo**

È possibile allegare file a un modulo. Quando si esegue il rendering di un modulo PDF con allegati ai file, gli utenti possono recuperare gli allegati in Acrobat utilizzando il riquadro allegato. È possibile allegare diversi tipi di file a un modulo, ad esempio un file di testo, o a un file binario come un file JPG.

>[!NOTE]
>
>L’allegato a un modulo di file è facoltativo.

**Rendering di un modulo PDF interattivo**

Per eseguire il rendering di un modulo, utilizzare una struttura del modulo creata in Designer e salvata come file XDP o PDF. È inoltre possibile eseguire il rendering di un modulo creato con Acrobat e salvato come file PDF. Per eseguire il rendering di un modulo PDF interattivo, richiamare il metodo `renderPDFForm` dell’oggetto `FormsServiceClient` o il metodo `renderPDFForm2`.

L&#39; `renderPDFForm` utilizza un oggetto `URLSpec`. La directory principale del contenuto del file XDP viene passata al servizio Forms utilizzando il metodo `URLSpec` dell&#39;oggetto `setContentRootURI` . Il nome della struttura del modulo ( `formQuery`) viene passato come valore di parametro separato. I due valori vengono concatenati per ottenere il riferimento assoluto alla struttura del modulo.

Il metodo `renderPDFForm2` accetta un&#39;istanza `com.adobe.idp.Document` che contiene il documento XDP o PDF da sottoporre a rendering.

>[!NOTE]
>
>Impossibile impostare l’opzione di esecuzione PDF con tag se il documento di input è un documento PDF. Se il file di input è un file XDP, è possibile impostare l’opzione PDF con tag.

## Eseguire il rendering di un modulo PDF interattivo utilizzando l’API Java {#render-an-interactive-pdf-form-using-the-java-api}

Eseguire il rendering di un modulo PDF interattivo utilizzando l’API Forms (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client Forms

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `FormsServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Specificare i valori URI

   * Creare un oggetto `URLSpec` che memorizza i valori URI utilizzando il relativo costruttore.
   * Richiama il metodo `setApplicationWebRoot` dell&#39;oggetto `URLSpec` e passa un valore stringa che rappresenta la radice Web dell&#39;applicazione.
   * Richiama il metodo `setContentRootURI` dell&#39;oggetto `URLSpec` e passa un valore stringa che specifica il valore URI della directory principale del contenuto. Verificare che la struttura del modulo si trovi nell’URI della directory principale del contenuto. In caso contrario, il servizio Forms genera un&#39;eccezione. Per fare riferimento al repository, specifica `repository:///`.
   * Richiama il metodo `setTargetURL` dell&#39;oggetto `URLSpec` e passa un valore stringa che specifica il valore dell&#39;URL di destinazione in cui vengono inviati i dati del modulo. Se si definisce l’URL di destinazione nella struttura del modulo, è possibile passare una stringa vuota. È inoltre possibile specificare l’URL a cui viene inviato un modulo per eseguire i calcoli.

1. Allegare file al modulo

   * Creare un oggetto `java.util.HashMap` per memorizzare gli allegati di file utilizzando il relativo costruttore.
   * Richiama il metodo `put` dell&#39;oggetto `java.util.HashMap` per ciascun file da allegare al modulo di cui è stato eseguito il rendering. Passa i seguenti valori a questo metodo:

      * Valore stringa che specifica il nome dell&#39;allegato del file, inclusa l&#39;estensione del nome file.
   * Un oggetto `com.adobe.idp.Document` che contiene l&#39;allegato del file.

   >[!NOTE]
   >
   >Ripetere questo passaggio per ogni file da allegare al modulo. Questo passaggio è facoltativo ed è possibile passare `null` se non si desidera inviare allegati di file.

1. Rendering di un modulo PDF interattivo

   Richiama il metodo `renderPDFForm` dell&#39;oggetto `FormsServiceClient` e passa i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, assicurarsi di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un oggetto `com.adobe.idp.Document` contenente i dati da unire al modulo. Se non si desidera unire i dati, passare un oggetto `com.adobe.idp.Document` vuoto.
   * Un oggetto `PDFFormRenderSpec` che memorizza le opzioni di esecuzione. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera specificare le opzioni di esecuzione.
   * Un oggetto `URLSpec` contenente valori URI richiesti dal servizio Forms.
   * Un oggetto `java.util.HashMap` che memorizza gli allegati di file. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.

   Il metodo `renderPDFForm` restituisce un oggetto `FormsResult` contenente un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo sul browser Web client

   * Creare un oggetto `com.adobe.idp.Document` richiamando il metodo `FormsResult` object ‘s `getOutputContent` .
   * Ottenere il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document` richiamandone il metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamandone il metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il metodo `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream`.
   * Creare un oggetto `java.io.InputStream` richiamando il metodo `com.adobe.idp.Document` dell&#39;oggetto `getInputStream`.
   * Creare una matrice di byte e compilarla con il flusso di dati del modulo richiamando il metodo `InputStream` dell&#39;oggetto `read` e passando la matrice di byte come argomento.
   * Richiamare il metodo `write` dell’oggetto `javax.servlet.ServletOutputStream` per inviare il flusso di dati del modulo al browser Web client. Passa l&#39;array di byte al metodo `write` .

## Eseguire il rendering di un modulo PDF interattivo utilizzando l’API del servizio Web {#render-an-interactive-pdf-form-using-the-web-service-api}

Eseguire il rendering di un modulo PDF interattivo utilizzando l’API Forms (servizio Web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio WSDL di Forms.
   * Includi le classi proxy Java nel percorso della classe.

1. Creare un oggetto API client Forms

   Creare un oggetto `FormsService` e impostare i valori di autenticazione.

1. Specificare i valori URI

   * Creare un oggetto `URLSpec` che memorizza i valori URI utilizzando il relativo costruttore.
   * Richiama il metodo `setApplicationWebRoot` dell&#39;oggetto `URLSpec` e passa un valore stringa che rappresenta la radice Web dell&#39;applicazione.
   * Richiama il metodo `setContentRootURI` dell&#39;oggetto `URLSpec` e passa un valore stringa che specifica il valore URI della directory principale del contenuto. Verificare che la struttura del modulo si trovi nell’URI della directory principale del contenuto. In caso contrario, il servizio Forms genera un&#39;eccezione. Per fare riferimento al repository, specifica `repository:///`.
   * Richiama il metodo `setTargetURL` dell&#39;oggetto `URLSpec` e passa un valore stringa che specifica il valore dell&#39;URL di destinazione in cui vengono inviati i dati del modulo. Se si definisce l’URL di destinazione nella struttura del modulo, è possibile passare una stringa vuota. È inoltre possibile specificare l’URL a cui viene inviato un modulo per eseguire i calcoli.

1. Allegare file al modulo

   * Creare un oggetto `java.util.HashMap` per memorizzare gli allegati di file utilizzando il relativo costruttore.
   * Richiama il metodo `put` dell&#39;oggetto `java.util.HashMap` per ciascun file da allegare al modulo di cui è stato eseguito il rendering. Passa i seguenti valori a questo metodo:

      * Valore stringa che specifica il nome dell&#39;allegato del file, inclusa l&#39;estensione del nome file
   * Un oggetto `BLOB` contenente l&#39;allegato del file

   >[!NOTE]
   >
   >Ripetere questo passaggio per ogni file da allegare al modulo.

1. Rendering di un modulo PDF interattivo

   Richiama il metodo `renderPDFForm` dell&#39;oggetto `FormsService` e passa i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, assicurarsi di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un oggetto `BLOB` contenente i dati da unire al modulo. Se non desideri unire i dati, passa `null`.
   * Un oggetto `PDFFormRenderSpec` che memorizza le opzioni di esecuzione. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera specificare le opzioni di esecuzione.
   * Un oggetto `URLSpec` contenente valori URI richiesti dal servizio Forms.
   * Un oggetto `java.util.HashMap` che memorizza gli allegati di file. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.
   * Un oggetto `com.adobe.idp.services.holders.BLOBHolder` vuoto compilato dal metodo . Viene utilizzato per memorizzare il modulo PDF di cui è stato effettuato il rendering.
   * Un oggetto `javax.xml.rpc.holders.LongHolder` vuoto compilato dal metodo . Questo argomento memorizza il numero di pagine nel modulo.
   * Un oggetto `javax.xml.rpc.holders.StringHolder` vuoto compilato dal metodo . Questo argomento memorizza il valore delle impostazioni internazionali.
   * Un oggetto `com.adobe.idp.services.holders.FormsResultHolder` vuoto che conterrà i risultati dell&#39;operazione.

   Il metodo `renderPDFForm` popola l&#39;oggetto `com.adobe.idp.services.holders.FormsResultHolder` passato come ultimo valore dell&#39;argomento con un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo sul browser Web client

   * Creare un oggetto `FormResult` ottenendo il valore del membro dati `com.adobe.idp.services.holders.FormsResultHolder` dell&#39;oggetto `value`.
   * Creare un oggetto `BLOB` che contiene dati del modulo richiamando il metodo `FormsResult` dell&#39;oggetto `getOutputContent`.
   * Ottenere il tipo di contenuto dell&#39;oggetto `BLOB` richiamandone il metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamandone il metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `BLOB`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il metodo `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream`.
   * Creare una matrice di byte e compilarla richiamando il metodo `getBinaryData` dell&#39;oggetto `BLOB`. Questa attività assegna il contenuto dell&#39;oggetto `FormsResult` all&#39;array di byte.
   * Richiamare il metodo `write` dell’oggetto `javax.servlet.http.HttpServletResponse` per inviare il flusso di dati del modulo al browser Web client. Passa l&#39;array di byte al metodo `write` .

**Scrivere il flusso di dati del modulo sul browser Web client**

Quando il servizio Forms esegue il rendering di un modulo, restituisce un flusso di dati del modulo che è necessario scrivere nel browser Web client. Una volta scritto nel browser Web client, il modulo è visibile all’utente.
