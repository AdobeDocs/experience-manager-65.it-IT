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
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2455'
ht-degree: 0%

---

# Rendering dei PDF forms interattivi {#rendering-interactive-pdf-forms}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

Il servizio Forms esegue il rendering dei PDF forms interattivi sui dispositivi client, in genere i browser web, per raccogliere informazioni dagli utenti. Dopo aver eseguito il rendering di un modulo interattivo, un utente può immettere i dati nei campi del modulo e fare clic su un pulsante di invio presente nel modulo per inviare nuovamente le informazioni al servizio Forms. Adobe Reader o Acrobat devono essere installati nel computer che ospita il browser web client per rendere visibile un modulo interattivo di PDF.

>[!NOTE]
>
>Prima di poter eseguire il rendering di un modulo utilizzando il servizio Forms, crea una progettazione del modulo. In genere, la progettazione di un modulo viene creata in Designer e salvata come file XDP. Per informazioni sulla creazione di una struttura di modulo, vedere [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

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
   <td><p>Il servlet Java <code>GetLoanForm</code> viene richiamato da una pagina HTML. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Il servlet Java <code>GetLoanForm</code> utilizza l'API client del servizio Forms per eseguire il rendering del modulo di prestito al browser Web client. (Vedi <a href="#render-an-interactive-pdf-form-using-the-java-api">Eseguire il rendering di un modulo PDF interattivo utilizzando l'API Java</a>.)</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Dopo che l'utente compila il modulo del prestito e fa clic sul pulsante di invio, i dati vengono inviati al servlet Java <code>HandleData</code>. (Vedere <i>"Modulo prestito"</i>.)</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Il servlet Java <code>HandleData</code> utilizza l'API client del servizio Forms per elaborare l'invio del modulo e recuperare i dati del modulo. I dati vengono quindi memorizzati in un database aziendale. (Vedi <a href="/help/forms/developing/handling-submitted-forms.md#handling-submitted-forms">Gestione di Forms inviato</a>.)</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>Viene eseguito il rendering di un modulo di conferma sul browser web. Dati quali il nome e il cognome dell'utente vengono uniti al modulo prima che questo venga sottoposto a rendering. (Vedi <a href="/help/forms/developing/prepopulating-forms-flowable-layouts.md">Precompilazione di Forms con layout percorribili</a>.)</p></td>
  </tr>
 </tbody>
</table>

**Modulo prestito**

Questo modulo di prestito interattivo viene visualizzato dal servlet Java `GetLoanForm` dell&#39;applicazione di prestito di esempio.

![ri_ri_loanform](assets/ri_ri_loanform.png)

**Modulo di conferma**

Questo modulo viene visualizzato dal servlet Java `HandleData` dell&#39;applicazione di prestito di esempio.

![ri_ri_confirm](assets/ri_ri_confirm.png)

Il servlet Java `HandleData` precompila questo modulo con il nome e il cognome dell&#39;utente e l&#39;importo. Una volta precompilato, il modulo viene inviato al browser Web client. (Vedi [Precompilazione di Forms con layout flessibili](/help/forms/developing/prepopulating-forms-flowable-layouts.md))

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

In genere, il codice API client del servizio Forms non viene inserito nel metodo `doGet` o `doPost` di un servlet Java. È consigliabile programmare il codice all&#39;interno di una classe separata, creare un&#39;istanza della classe all&#39;interno del metodo `doPost` (o del metodo `doGet`) e chiamare i metodi appropriati. Tuttavia, per la brevità del codice, gli esempi di codice in questa sezione sono limitati al minimo e gli esempi di codice sono inseriti nel metodo `doPost`.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Prima di poter eseguire un&#39;operazione API client di un servizio Forms a livello di programmazione, è necessario creare un oggetto API client Forms. Se si utilizza l&#39;API Java, creare un oggetto `FormsServiceClient`. Se si utilizza l&#39;API del servizio Web Forms, creare un oggetto `FormsService`.

**Specificare valori URI**

È possibile specificare i valori URI richiesti dal servizio Forms per il rendering di un modulo. È possibile fare riferimento a una struttura di modulo salvata come parte di un&#39;applicazione Forms utilizzando il valore URI radice contenuto `repository:///`. Si consideri ad esempio il seguente design di modulo denominato *Loan.xdp* che si trova all&#39;interno di un&#39;applicazione Forms denominata *FormsApplication*:

![ri_ri_formrepository](assets/ri_ri_formrepository.png)

Per accedere alla struttura del modulo, specificare `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp` come nome del modulo (il primo parametro passato al metodo `renderPDFForm`) e `repository:///` come valore URI della radice del contenuto.

>[!NOTE]
>
>Per informazioni sulla creazione di un&#39;applicazione Forms tramite Workbench, vedere la [Guida di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

Il percorso di una risorsa in un’applicazione Forms è:

`Applications/Application-name/Application-version/Folder.../Filename`

I seguenti valori mostrano alcuni esempi di valori URI:

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

Quando esegui il rendering di un modulo interattivo, puoi definire valori URI come l’URL di destinazione in cui vengono pubblicati i dati del modulo. L’URL di destinazione può essere definito in uno dei seguenti modi:

* Sul pulsante Invia durante la progettazione della struttura del modulo in Designer
* Utilizzando l’API client del servizio Forms

Se l’URL di destinazione è definito nella progettazione del modulo, non eseguirne l’override con l’API client del servizio Forms. In altre parole, impostando l’URL di destinazione utilizzando l’API di Forms, l’URL specificato nella progettazione del modulo viene reimpostato su quello specificato utilizzando l’API. Se desideri inviare il modulo PDF all’URL di destinazione specificato nella progettazione del modulo, imposta a livello di programmazione l’URL di destinazione su una stringa vuota.

Se si dispone di un modulo contenente un pulsante di invio e un pulsante di calcolo (con uno script corrispondente in esecuzione sul server), è possibile definire a livello di programmazione l&#39;URL a cui inviare il modulo per eseguire lo script. Utilizza il pulsante Invia nella struttura del modulo per specificare l’URL in cui vengono pubblicati i dati del modulo. (Vedi [Calcolo dei dati del modulo](/help/forms/developing/calculating-form-data.md).)

>[!NOTE]
>
>Anziché specificare un valore URL per fare riferimento a un file XDP, è possibile passare un&#39;istanza `com.adobe.idp.Document` al servizio Forms. L&#39;istanza `com.adobe.idp.Document` contiene una struttura di modulo. (Vedi [Trasmissione di documenti al servizio Forms](/help/forms/developing/passing-documents-forms-service.md).)

**Allega file al modulo**

È possibile allegare file a un modulo. Quando si esegue il rendering di un modulo PDF con file allegati, gli utenti possono recuperare i file allegati in Acrobat utilizzando il riquadro dei file allegati. È possibile allegare tipi di file diversi a un modulo, ad esempio un file di testo, oppure a un file binario, ad esempio un file JPG.

>[!NOTE]
>
>L&#39;aggiunta di allegati a un modulo è facoltativa.

**Eseguire il rendering di un modulo PDF interattivo**

Per eseguire il rendering di un modulo, utilizza una struttura di modulo creata in Designer e salvata come file XDP o PDF. È inoltre possibile eseguire il rendering di un modulo creato con Acrobat e salvato come file PDF. Per eseguire il rendering di un modulo PDF interattivo, richiamare il metodo `renderPDFForm` o `renderPDFForm2` dell&#39;oggetto `FormsServiceClient`.

`renderPDFForm` utilizza un oggetto `URLSpec`. La radice del contenuto del file XDP viene passata al servizio Forms utilizzando il metodo `setContentRootURI` dell&#39;oggetto `URLSpec`. Il nome della struttura del modulo ( `formQuery`) viene passato come valore di parametro separato. I due valori vengono concatenati per ottenere il riferimento assoluto alla progettazione del modulo.

Il metodo `renderPDFForm2` accetta un&#39;istanza `com.adobe.idp.Document` che contiene il documento XDP o PDF da riprodurre.

>[!NOTE]
>
>Impossibile impostare l&#39;opzione di runtime PDF con tag se il documento di input è un documento PDF. Se il file di input è un file XDP, è possibile impostare l&#39;opzione PDF con tag.

## Eseguire il rendering di un modulo PDF interattivo tramite l’API Java {#render-an-interactive-pdf-form-using-the-java-api}

Esegui il rendering di un modulo PDF interattivo utilizzando l’API Forms (Java):

1. Includi file di progetto

   Includi i file JAR client, ad esempio adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client di Forms

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `FormsServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Specificare i valori URI

   * Creare un oggetto `URLSpec` che memorizza i valori URI utilizzando il relativo costruttore.
   * Richiama il metodo `setApplicationWebRoot` dell&#39;oggetto `URLSpec` e passa un valore stringa che rappresenta la radice web dell&#39;applicazione.
   * Richiama il metodo `setContentRootURI` dell&#39;oggetto `URLSpec` e passa un valore stringa che specifica il valore URI della radice del contenuto. Assicurati che la progettazione del modulo sia nell’URI della directory principale del contenuto. In caso contrario, il servizio Forms genera un&#39;eccezione. Per fare riferimento all&#39;archivio, specificare `repository:///`.
   * Richiama il metodo `setTargetURL` dell&#39;oggetto `URLSpec` e passa un valore stringa che specifica il valore dell&#39;URL di destinazione in cui vengono inviati i dati del modulo. Se definisci l’URL di destinazione nella progettazione del modulo, puoi trasmettere una stringa vuota. È inoltre possibile specificare l&#39;URL a cui viene inviato un modulo per eseguire i calcoli.

1. Allega file al modulo

   * Creare un oggetto `java.util.HashMap` per archiviare gli allegati utilizzando il relativo costruttore.
   * Richiama il metodo `put` dell&#39;oggetto `java.util.HashMap` per ogni file da allegare al modulo di cui è stato eseguito il rendering. Passa i seguenti valori a questo metodo:

      * Valore stringa che specifica il nome del file allegato, inclusa l&#39;estensione.

   * Oggetto `com.adobe.idp.Document` contenente il file allegato.

   >[!NOTE]
   >
   >Ripetere questo passaggio per ogni file da allegare al modulo. Questo passaggio è facoltativo ed è possibile passare `null` se non si desidera inviare file allegati.

1. Rendering di un modulo PDF interattivo

   Richiama il metodo `renderPDFForm` dell&#39;oggetto `FormsServiceClient` e passa i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura di modulo che fa parte di un&#39;applicazione Forms, assicurarsi di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Oggetto `com.adobe.idp.Document` contenente dati da unire al modulo. Se non si desidera unire i dati, passare un oggetto `com.adobe.idp.Document` vuoto.
   * Un oggetto `PDFFormRenderSpec` che memorizza le opzioni di runtime. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera specificare le opzioni di runtime.
   * Oggetto `URLSpec` contenente i valori URI richiesti dal servizio Forms.
   * Oggetto `java.util.HashMap` che memorizza gli allegati. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.

   Il metodo `renderPDFForm` restituisce un oggetto `FormsResult` che contiene un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo nel browser Web client

   * Creare un oggetto `com.adobe.idp.Document` richiamando il metodo `getOutputContent` dell&#39;oggetto `FormsResult`.
   * Ottenere il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document` richiamando il relativo metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamando il relativo metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il metodo `getOutputStream` dell&#39;oggetto `javax.servlet.http.HttpServletResponse`.
   * Creare un oggetto `java.io.InputStream` richiamando il metodo `getInputStream` dell&#39;oggetto `com.adobe.idp.Document`.
   * Creare una matrice di byte e popolarla con il flusso di dati del modulo richiamando il metodo `read` dell&#39;oggetto `InputStream` e passando la matrice di byte come argomento.
   * Richiama il metodo `write` dell&#39;oggetto `javax.servlet.ServletOutputStream` per inviare il flusso di dati del modulo al browser Web client. Passare la matrice di byte al metodo `write`.

## Eseguire il rendering di un modulo PDF interattivo utilizzando l’API del servizio web {#render-an-interactive-pdf-form-using-the-web-service-api}

Esegui il rendering di un modulo PDF interattivo utilizzando l’API Forms (servizio web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio Forms WSDL.
   * Includi le classi proxy Java nel percorso della classe.

1. Creare un oggetto API client di Forms

   Creare un oggetto `FormsService` e impostare i valori di autenticazione.

1. Specificare i valori URI

   * Creare un oggetto `URLSpec` che memorizza i valori URI utilizzando il relativo costruttore.
   * Richiama il metodo `setApplicationWebRoot` dell&#39;oggetto `URLSpec` e passa un valore stringa che rappresenta la radice web dell&#39;applicazione.
   * Richiama il metodo `setContentRootURI` dell&#39;oggetto `URLSpec` e passa un valore stringa che specifica il valore URI della radice del contenuto. Assicurati che la progettazione del modulo sia nell’URI della directory principale del contenuto. In caso contrario, il servizio Forms genera un&#39;eccezione. Per fare riferimento all&#39;archivio, specificare `repository:///`.
   * Richiama il metodo `setTargetURL` dell&#39;oggetto `URLSpec` e passa un valore stringa che specifica il valore dell&#39;URL di destinazione in cui vengono inviati i dati del modulo. Se definisci l’URL di destinazione nella progettazione del modulo, puoi trasmettere una stringa vuota. È inoltre possibile specificare l&#39;URL a cui viene inviato un modulo per eseguire i calcoli.

1. Allega file al modulo

   * Creare un oggetto `java.util.HashMap` per archiviare gli allegati utilizzando il relativo costruttore.
   * Richiama il metodo `put` dell&#39;oggetto `java.util.HashMap` per ogni file da allegare al modulo di cui è stato eseguito il rendering. Passa i seguenti valori a questo metodo:

      * Valore stringa che specifica il nome dell&#39;allegato, inclusa l&#39;estensione del nome file

   * Oggetto `BLOB` contenente il file allegato

   >[!NOTE]
   >
   >Ripetere questo passaggio per ogni file da allegare al modulo.

1. Rendering di un modulo PDF interattivo

   Richiama il metodo `renderPDFForm` dell&#39;oggetto `FormsService` e passa i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura di modulo che fa parte di un&#39;applicazione Forms, assicurarsi di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Oggetto `BLOB` contenente dati da unire al modulo. Se non si desidera unire i dati, passare `null`.
   * Un oggetto `PDFFormRenderSpec` che memorizza le opzioni di runtime. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera specificare le opzioni di runtime.
   * Oggetto `URLSpec` contenente i valori URI richiesti dal servizio Forms.
   * Oggetto `java.util.HashMap` che memorizza gli allegati. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.
   * Oggetto `com.adobe.idp.services.holders.BLOBHolder` vuoto popolato dal metodo. Viene utilizzato per memorizzare il modulo PDF di cui è stato eseguito il rendering.
   * Oggetto `javax.xml.rpc.holders.LongHolder` vuoto popolato dal metodo. Questo argomento consente di memorizzare il numero di pagine nel modulo.
   * Oggetto `javax.xml.rpc.holders.StringHolder` vuoto popolato dal metodo. Questo argomento consente di memorizzare il valore delle impostazioni locali.
   * Oggetto `com.adobe.idp.services.holders.FormsResultHolder` vuoto che conterrà i risultati dell&#39;operazione.

   Il metodo `renderPDFForm` popola l&#39;oggetto `com.adobe.idp.services.holders.FormsResultHolder` passato come ultimo valore di argomento con un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo nel browser Web client

   * Creare un oggetto `FormResult` ottenendo il valore del membro dati `value` dell&#39;oggetto `com.adobe.idp.services.holders.FormsResultHolder`.
   * Creare un oggetto `BLOB` contenente dati del modulo richiamando il metodo `getOutputContent` dell&#39;oggetto `FormsResult`.
   * Ottenere il tipo di contenuto dell&#39;oggetto `BLOB` richiamando il relativo metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamando il relativo metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `BLOB`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il metodo `getOutputStream` dell&#39;oggetto `javax.servlet.http.HttpServletResponse`.
   * Creare una matrice di byte e popolarla richiamando il metodo `getBinaryData` dell&#39;oggetto `BLOB`. Questa attività assegna il contenuto dell&#39;oggetto `FormsResult` alla matrice di byte.
   * Richiama il metodo `write` dell&#39;oggetto `javax.servlet.http.HttpServletResponse` per inviare il flusso di dati del modulo al browser Web client. Passare la matrice di byte al metodo `write`.

**Scrivere il flusso di dati del modulo nel browser Web client**

Quando il servizio Forms esegue il rendering di un modulo, restituisce un flusso di dati del modulo che è necessario scrivere nel browser Web client. Quando viene scritto nel browser Web client, il modulo è visibile all&#39;utente.
