---
title: Rendering di PDF forms interattivi
seo-title: Rendering di PDF forms interattivi
description: Utilizzate il servizio Forms per eseguire il rendering dei PDF forms interattivi sui dispositivi client, in genere sui browser Web, per raccogliere informazioni dagli utenti. È possibile utilizzare il servizio Forms per eseguire il rendering dei moduli interattivi utilizzando l'API Java e l'API del servizio Web.
seo-description: Utilizzate il servizio Forms per eseguire il rendering dei PDF forms interattivi sui dispositivi client, in genere sui browser Web, per raccogliere informazioni dagli utenti. È possibile utilizzare il servizio Forms per eseguire il rendering dei moduli interattivi utilizzando l'API Java e l'API del servizio Web.
uuid: df2a4dc8-f19e-49de-850f-85a204102631
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3cb307ec-9b7b-4f03-b860-48553ccee746
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '2514'
ht-degree: 0%

---


# Rendering PDF forms interattivi {#rendering-interactive-pdf-forms}

Il servizio Forms esegue il rendering dei PDF forms interattivi sui dispositivi client, in genere sui browser Web, per raccogliere informazioni dagli utenti. Dopo aver eseguito il rendering di un modulo interattivo, l&#39;utente può immettere i dati nei campi del modulo e fare clic su un pulsante di invio situato sul modulo per inviare le informazioni al servizio Forms.  Adobe Reader o  Acrobat deve essere installato sul computer in cui è installato il browser Web client per rendere visibile un modulo PDF interattivo.

>[!NOTE]
>
>Prima di eseguire il rendering di un modulo con il servizio Forms, creare una struttura del modulo. In genere, una struttura del modulo viene creata in Designer e salvata come file XDP. Per informazioni sulla creazione di una struttura del modulo, vedere [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

**Esempio di domanda di prestito**

È stata introdotta un&#39;applicazione di prestito di esempio per illustrare in che modo il servizio Forms utilizza i moduli interattivi per raccogliere informazioni dagli utenti. Questa applicazione consente a un utente di compilare un modulo con i dati necessari per ottenere un prestito e quindi inviare i dati al servizio Forms. Il diagramma seguente mostra il flusso logico dell&#39;applicazione del prestito.

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
   <td><p>Il servlet <code>GetLoanForm</code> Java utilizza l'API client del servizio Forms per eseguire il rendering del modulo di prestito nel browser Web del client. (Vedere <a href="#render-an-interactive-pdf-form-using-the-java-api">Eseguire il rendering di un modulo PDF interattivo utilizzando l'API Java</a>.)</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Dopo che l'utente ha compilato il modulo di prestito e fatto clic sul pulsante di invio, i dati vengono inviati al <code>HandleData</code> Servlet Java. (Vedere <i>"Loan form"</i>.)</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Il servlet <code>HandleData</code> Java utilizza l'API client del servizio Forms per elaborare l'invio del modulo e recuperare i dati del modulo. I dati vengono quindi memorizzati in un database aziendale. (Vedere <a href="/help/forms/developing/handling-submitted-forms.md#handling-submitted-forms">Gestione di Forms</a> inviato.)</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>Viene eseguito il rendering di un modulo di conferma nel browser Web. I dati, come il nome e il cognome dell'utente, vengono uniti al modulo prima del rendering. (Vedere <a href="/help/forms/developing/prepopulating-forms-flowable-layouts.md">Precompilazione di Forms con layout scorrevoli</a>.)</p></td>
  </tr>
 </tbody>
</table>

**Modulo di prestito**

Questo modulo di prestito interattivo viene rappresentato dal servlet Java `GetLoanForm` dell&#39;applicazione di prestito di esempio.

![ri_ri_loanform](assets/ri_ri_loanform.png)

**Modulo di conferma**

Questo modulo viene rappresentato dal servlet Java dell&#39;applicazione di prestito di esempio `HandleData`.

![ri_ri_confirm](assets/ri_ri_confirm.png)

Il Servlet Java `HandleData` precompila il modulo con il nome e il cognome dell&#39;utente e con l&#39;importo. Una volta precompilato, il modulo viene inviato al browser Web del client. (Vedere [Precompilazione di Forms con layout scorrevoli](/help/forms/developing/prepopulating-forms-flowable-layouts.md))

**Servlet Java**

L&#39;applicazione di prestito di esempio è un esempio di applicazione di servizio Forms esistente come servlet Java. Un servlet Java è un programma Java in esecuzione su un server applicazione J2EE, come WebSphere, e contiene il codice API client del servizio Forms.

Il codice seguente mostra la sintassi di un Servlet Java denominato GetLoanForm:

```java
     public class GetLoanForm extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

             }
```

Normalmente, non si inserisce il codice API client del servizio Forms all&#39;interno di un metodo `doGet` o `doPost` di un Servlet Java. È consigliabile posizionare il codice all&#39;interno di una classe separata, creare un&#39;istanza della classe dall&#39;interno del metodo `doPost` (o `doGet`) e chiamare i metodi appropriati. Tuttavia, per la brevità del codice, gli esempi di codice riportati in questa sezione sono limitati al minimo e gli esempi di codice vengono inseriti nel metodo `doPost`.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

**Riepilogo dei passaggi**

Per eseguire il rendering di un modulo PDF interattivo, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto Forms Client API.
1. Specificate i valori URI.
1. Allegare file al modulo (facoltativo).
1. Eseguire il rendering di un modulo PDF interattivo.
1. Scrivere il flusso di dati del modulo nel browser Web del client.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto Forms Client API**

Prima di eseguire un&#39;operazione API client di Forms Service a livello di programmazione, è necessario creare un oggetto API client Forms. Se utilizzate l&#39;API Java, create un oggetto `FormsServiceClient`. Se utilizzate l&#39;API del servizio Web di Forms, create un oggetto `FormsService`.

**Specificare i valori URI**

È possibile specificare i valori URI richiesti dal servizio Forms per eseguire il rendering di un modulo. Per fare riferimento a una struttura del modulo salvata come parte di un&#39;applicazione Forms, utilizzare il valore URI radice del contenuto `repository:///`. Ad esempio, tenere in considerazione la seguente struttura del modulo denominata *Loan.xdp* all&#39;interno di un&#39;applicazione Forms denominata *FormsApplication*:

![ri_ri_formrepository](assets/ri_ri_formrepository.png)

Per accedere a questa struttura del modulo, specificare `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp` come nome del modulo (il primo parametro passato al metodo `renderPDFForm`) e `repository:///` come valore URI della directory principale del contenuto.

>[!NOTE]
>
>Per informazioni sulla creazione di un&#39;applicazione Forms utilizzando Workbench, vedere la Guida di Workbench [Guida](https://www.adobe.com/go/learn_aemforms_workbench_63).

Il percorso di una risorsa che si trova in un&#39;applicazione Forms è:

`Applications/Application-name/Application-version/Folder.../Filename`

I seguenti valori mostrano alcuni esempi di valori URI:

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

Quando si esegue il rendering di un modulo interattivo, è possibile definire valori URI quali l&#39;URL di destinazione in cui vengono inviati i dati del modulo. L’URL di destinazione può essere definito in uno dei modi seguenti:

* Sul pulsante Invia durante la progettazione della struttura del modulo in Designer
* Utilizzando l&#39;API client del servizio Forms

Se l&#39;URL di destinazione è definito all&#39;interno della struttura del modulo, non ignorarlo con l&#39;API client del servizio Forms. In altre parole, l&#39;impostazione dell&#39;URL di destinazione tramite l&#39;API di Forms reimposta l&#39;URL specificato nella struttura del modulo a quello specificato tramite l&#39;API. Se si desidera inviare il modulo PDF all&#39;URL di destinazione specificato nella struttura del modulo, impostare l&#39;URL di destinazione a livello di programmazione su una stringa vuota.

Se si dispone di un modulo contenente un pulsante di invio e un pulsante di calcolo (con uno script corrispondente eseguito sul server), è possibile definire a livello di programmazione l&#39;URL al quale viene inviato il modulo per eseguire lo script. Utilizzare il pulsante di invio nella struttura del modulo per specificare l&#39;URL in cui vengono inviati i dati del modulo. (Vedere [Calcolo dei dati del modulo](/help/forms/developing/calculating-form-data.md).)

>[!NOTE]
>
>Invece di specificare un valore URL per fare riferimento a un file XDP, potete anche passare un&#39;istanza `com.adobe.idp.Document` al servizio Forms. L&#39;istanza `com.adobe.idp.Document` contiene una struttura del modulo. (Vedere [Trasmissione di documenti al servizio Forms](/help/forms/developing/passing-documents-forms-service.md).)

**Allega file al modulo**

È possibile allegare file a un modulo. Quando si esegue il rendering di un modulo PDF con file allegati, gli utenti possono recuperare i file allegati in  Acrobat utilizzando il riquadro dell&#39;allegato. È possibile allegare tipi di file diversi a un modulo, ad esempio un file di testo, o a un file binario come un file JPG.

>[!NOTE]
>
>L&#39;associazione di file allegati a un modulo è facoltativa.

**Rendering di un modulo PDF interattivo**

Per eseguire il rendering di un modulo, utilizzare una struttura del modulo creata in Designer e salvata come file XDP o PDF. È inoltre possibile eseguire il rendering di un modulo creato con  Acrobat e salvato come file PDF. Per eseguire il rendering di un modulo PDF interattivo, richiamare il metodo `FormsServiceClient` dell&#39;oggetto `renderPDFForm` o il metodo &lt;a2/>.`renderPDFForm2`

L&#39;oggetto `renderPDFForm` utilizza un oggetto `URLSpec`. Il livello principale del contenuto del file XDP viene passato al servizio Forms utilizzando il metodo `URLSpec` dell&#39;oggetto `setContentRootURI`. Il nome della struttura del modulo ( `formQuery`) viene passato come valore di parametro separato. I due valori vengono concatenati per ottenere il riferimento assoluto alla struttura del modulo.

Il metodo `renderPDFForm2` accetta un&#39;istanza `com.adobe.idp.Document` che contiene il documento XDP o PDF per il rendering.

>[!NOTE]
>
>L&#39;opzione PDF con tag non può essere impostata se il documento di input è un documento PDF. Se il file di input è un file XDP, è possibile impostare l&#39;opzione PDF con tag.

## Eseguire il rendering di un modulo PDF interattivo utilizzando l&#39;API Java {#render-an-interactive-pdf-form-using-the-java-api}

Eseguire il rendering di un modulo PDF interattivo utilizzando l&#39;API di Forms (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto Forms Client API

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `FormsServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Specificare i valori URI

   * Creare un oggetto `URLSpec` che memorizza i valori URI utilizzando il relativo costruttore.
   * Richiamare il metodo `URLSpec` dell&#39;oggetto `setApplicationWebRoot` e passare un valore di stringa che rappresenta la radice Web dell&#39;applicazione.
   * Richiamare il metodo `URLSpec` dell&#39;oggetto `setContentRootURI` e passare un valore di stringa che specifica il valore URI radice del contenuto. Verificare che la struttura del modulo si trovi nell&#39;URI della directory principale del contenuto. In caso contrario, il servizio Forms genera un&#39;eccezione. Per fare riferimento alla directory archivio, specificare `repository:///`.
   * Richiamare il metodo `URLSpec` dell&#39;oggetto `setTargetURL` e passare un valore di stringa che specifica il valore dell&#39;URL di destinazione in cui vengono inviati i dati del modulo. Se si definisce l&#39;URL di destinazione nella struttura del modulo, è possibile passare una stringa vuota. È inoltre possibile specificare l&#39;URL al quale viene inviato il modulo per eseguire i calcoli.

1. Allega file al modulo

   * Creare un oggetto `java.util.HashMap` per memorizzare gli allegati utilizzando il relativo costruttore.
   * Richiamare il metodo `java.util.HashMap` dell&#39;oggetto `put` affinché ciascun file venga allegato al modulo di cui è stato effettuato il rendering. Passa i seguenti valori a questo metodo:

      * Una stringa che specifica il nome dell&#39;allegato del file, inclusa l&#39;estensione del nome del file.
   * Un oggetto `com.adobe.idp.Document` che contiene l&#39;allegato del file.

   >[!NOTE]
   >
   >Ripetere questo passaggio per ogni file da allegare al modulo. Questo passaggio è facoltativo ed è possibile passare `null` se non si desidera inviare allegati di file.

1. Rendering di un modulo PDF interattivo

   Richiamare il metodo `FormsServiceClient` dell&#39;oggetto `renderPDFForm` e trasmettere i seguenti valori:

   * Una stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, è necessario specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un oggetto `com.adobe.idp.Document` che contiene i dati da unire al modulo. Se non si desidera unire i dati, passare un oggetto `com.adobe.idp.Document` vuoto.
   * Un oggetto `PDFFormRenderSpec` che memorizza le opzioni di esecuzione. Si tratta di un parametro facoltativo e potete specificare `null` se non desiderate specificare le opzioni di esecuzione.
   * Un oggetto `URLSpec` che contiene valori URI richiesti dal servizio Forms.
   * Un oggetto `java.util.HashMap` che memorizza gli allegati. Si tratta di un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.

   Il metodo `renderPDFForm` restituisce un oggetto `FormsResult` contenente un flusso di dati del modulo che deve essere scritto nel browser Web del client.

1. Scrivere il flusso di dati del modulo nel browser Web del client

   * Creare un oggetto `com.adobe.idp.Document` richiamando il metodo `FormsResult` object ‘s `getOutputContent`.
   * Ottenere il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document` richiamandone il metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamandone il metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web del client richiamando il metodo `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream`.
   * Creare un oggetto `java.io.InputStream` richiamando il metodo `com.adobe.idp.Document` dell&#39;oggetto `getInputStream`.
   * Creare un array di byte e compilarlo con il flusso di dati del modulo richiamando il metodo `InputStream` dell&#39;oggetto `read` e passando l&#39;array di byte come argomento.
   * Richiamare il metodo `javax.servlet.ServletOutputStream` dell&#39;oggetto `write` per inviare il flusso di dati del modulo al browser Web del client. Passate l&#39;array di byte al metodo `write`.

## Eseguire il rendering di un modulo PDF interattivo utilizzando l&#39;API del servizio Web {#render-an-interactive-pdf-form-using-the-web-service-api}

Eseguire il rendering di un modulo PDF interattivo utilizzando l&#39;API di Forms (servizio Web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio WSDL di Forms.
   * Includete le classi proxy Java nel percorso della classe.

1. Creare un oggetto Forms Client API

   Creare un oggetto `FormsService` e impostare i valori di autenticazione.

1. Specificare i valori URI

   * Creare un oggetto `URLSpec` che memorizza i valori URI utilizzando il relativo costruttore.
   * Richiamare il metodo `URLSpec` dell&#39;oggetto `setApplicationWebRoot` e passare un valore di stringa che rappresenta la radice Web dell&#39;applicazione.
   * Richiamare il metodo `URLSpec` dell&#39;oggetto `setContentRootURI` e passare un valore di stringa che specifica il valore URI radice del contenuto. Verificare che la struttura del modulo si trovi nell&#39;URI della directory principale del contenuto. In caso contrario, il servizio Forms genera un&#39;eccezione. Per fare riferimento alla directory archivio, specificare `repository:///`.
   * Richiamare il metodo `URLSpec` dell&#39;oggetto `setTargetURL` e passare un valore di stringa che specifica il valore dell&#39;URL di destinazione in cui vengono inviati i dati del modulo. Se si definisce l&#39;URL di destinazione nella struttura del modulo, è possibile passare una stringa vuota. È inoltre possibile specificare l&#39;URL al quale viene inviato il modulo per eseguire i calcoli.

1. Allega file al modulo

   * Creare un oggetto `java.util.HashMap` per memorizzare gli allegati utilizzando il relativo costruttore.
   * Richiamare il metodo `java.util.HashMap` dell&#39;oggetto `put` affinché ciascun file venga allegato al modulo di cui è stato effettuato il rendering. Passa i seguenti valori a questo metodo:

      * Una stringa che specifica il nome dell&#39;allegato del file, inclusa l&#39;estensione del nome file
   * Un oggetto `BLOB` che contiene l&#39;allegato del file

   >[!NOTE]
   >
   >Ripetere questo passaggio per ogni file da allegare al modulo.

1. Rendering di un modulo PDF interattivo

   Richiamare il metodo `FormsService` dell&#39;oggetto `renderPDFForm` e trasmettere i seguenti valori:

   * Una stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, è necessario specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un oggetto `BLOB` che contiene i dati da unire al modulo. Se non si desidera unire i dati, passare `null`.
   * Un oggetto `PDFFormRenderSpec` che memorizza le opzioni di esecuzione. Si tratta di un parametro facoltativo e potete specificare `null` se non desiderate specificare le opzioni di esecuzione.
   * Un oggetto `URLSpec` che contiene valori URI richiesti dal servizio Forms.
   * Un oggetto `java.util.HashMap` che memorizza gli allegati. Si tratta di un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.
   * Un oggetto `com.adobe.idp.services.holders.BLOBHolder` vuoto compilato dal metodo. Viene utilizzato per memorizzare il modulo PDF di cui è stato effettuato il rendering.
   * Un oggetto `javax.xml.rpc.holders.LongHolder` vuoto compilato dal metodo. Questo argomento consente di memorizzare il numero di pagine nel modulo.
   * Un oggetto `javax.xml.rpc.holders.StringHolder` vuoto compilato dal metodo. (Questo argomento memorizza il valore delle impostazioni internazionali.)
   * Un oggetto `com.adobe.idp.services.holders.FormsResultHolder` vuoto che conterrà i risultati dell&#39;operazione.

   Il metodo `renderPDFForm` compila l&#39;oggetto `com.adobe.idp.services.holders.FormsResultHolder` passato come ultimo valore argomento con un flusso di dati del modulo che deve essere scritto nel browser Web del client.

1. Scrivere il flusso di dati del modulo nel browser Web del client

   * Creare un oggetto `FormResult` ottenendo il valore del membro di dati `com.adobe.idp.services.holders.FormsResultHolder` dell&#39;oggetto `value`.
   * Creare un oggetto `BLOB` contenente dati del modulo richiamando il metodo `FormsResult` dell&#39;oggetto `getOutputContent`.
   * Ottenere il tipo di contenuto dell&#39;oggetto `BLOB` richiamandone il metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamandone il metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `BLOB`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web del client richiamando il metodo `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream`.
   * Creare un array di byte e compilarlo richiamando il metodo `BLOB` dell&#39;oggetto `getBinaryData`. Questa attività assegna il contenuto dell&#39;oggetto `FormsResult` all&#39;array di byte.
   * Richiamare il metodo `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `write` per inviare il flusso di dati del modulo al browser Web del client. Passate l&#39;array di byte al metodo `write`.

**Scrivere il flusso di dati del modulo nel browser Web del client**

Quando il servizio Forms esegue il rendering di un modulo, restituisce un flusso di dati del modulo che è necessario scrivere nel browser Web del client. Una volta scritto nel browser Web del client, il modulo è visibile all&#39;utente.
