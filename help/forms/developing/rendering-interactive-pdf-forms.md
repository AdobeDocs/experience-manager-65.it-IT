---
title: Rendering di PDF forms interattivi
seo-title: Rendering di PDF forms interattivi
description: 'null'
seo-description: 'null'
uuid: df2a4dc8-f19e-49de-850f-85a204102631
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3cb307ec-9b7b-4f03-b860-48553ccee746
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2442'
ht-degree: 0%

---


# Rendering di PDF forms interattivi {#rendering-interactive-pdf-forms}

Il servizio Forms esegue il rendering dei PDF forms interattivi sui dispositivi client, in genere sui browser Web, per raccogliere informazioni dagli utenti. Dopo aver eseguito il rendering di un modulo interattivo, l&#39;utente può immettere i dati nei campi del modulo e fare clic su un pulsante di invio situato nel modulo per inviare le informazioni al servizio Forms. Per rendere visibile un modulo PDF interattivo, è necessario installare Adobe Reader o Acrobat nel computer in cui è installato il browser Web del client.

>[!NOTE]
>
>Prima di eseguire il rendering di un modulo con il servizio Forms, creare una struttura del modulo. In genere, una struttura del modulo viene creata in Designer e salvata come file XDP. Per informazioni sulla creazione di una struttura del modulo, vedere [Designer](https://www.adobe.com/go/learn_aemforms_designer_63)di moduli.

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
   <td><p>Il servlet <code>GetLoanForm</code> Java viene richiamato da una pagina HTML. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Il servlet <code>GetLoanForm</code> Java utilizza l'API client del servizio Forms per eseguire il rendering del modulo di prestito nel browser Web del client. (Vedere <a href="#render-an-interactive-pdf-form-using-the-java-api">Rendering di un modulo PDF interattivo mediante l'API</a>Java.)</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>Dopo che l'utente ha compilato il modulo di prestito e fatto clic sul pulsante di invio, i dati vengono inviati a <code>HandleData</code> Java Servlet. (Vedere <i>"Modulo di prestito"</i>.)</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Il servlet <code>HandleData</code> Java utilizza l'API client del servizio Forms per elaborare l'invio e il recupero dei dati del modulo. I dati vengono quindi memorizzati in un database aziendale. (Vedere <a href="/help/forms/developing/handling-submitted-forms.md#handling-submitted-forms">Gestione Dei Moduli</a>Inviati.)</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>Viene eseguito il rendering di un modulo di conferma nel browser Web. I dati, come il nome e il cognome dell'utente, vengono uniti al modulo prima del rendering. (Vedere <a href="/help/forms/developing/prepopulating-forms-flowable-layouts.md">Precompilazione dei moduli con layout</a>scorrevoli.)</p></td>
  </tr>
 </tbody>
</table>

**Modulo di prestito**

Questo modulo di prestito interattivo viene rappresentato dal servlet `GetLoanForm` Java dell&#39;applicazione di prestito di esempio.

![ri_ri_loanform](assets/ri_ri_loanform.png)

**Modulo di conferma**

Questo modulo viene rappresentato dal servlet `HandleData` Java dell&#39;applicazione di prestito di esempio.

![ri_ri_confirm](assets/ri_ri_confirm.png)

Il Servlet `HandleData` Java precompila il modulo con il nome e il cognome dell&#39;utente e con l&#39;importo. Una volta precompilato, il modulo viene inviato al browser Web del client. (Vedere [Precompilazione dei moduli con layout](/help/forms/developing/prepopulating-forms-flowable-layouts.md)scorrevoli)

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

Normalmente, non posizionare il codice API client del servizio Forms all&#39;interno di un `doGet` `doPost` metodo o di un servlet Java. È consigliabile posizionare il codice all&#39;interno di una classe separata, creare un&#39;istanza della classe dall&#39;interno del `doPost` metodo (o `doGet` metodo) e chiamare i metodi appropriati. Tuttavia, per la brevità del codice, gli esempi di codice riportati in questa sezione sono limitati al minimo e gli esempi di codice sono inseriti nel `doPost` metodo.

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, vedere Riferimento [servizi per gli AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

**Riepilogo dei passaggi**

Per eseguire il rendering di un modulo PDF interattivo, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto API client Forms.
1. Specificate i valori URI.
1. Allegare file al modulo (facoltativo).
1. Eseguire il rendering di un modulo PDF interattivo.
1. Scrivere il flusso di dati del modulo nel browser Web del client.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto API client Forms**

Prima di eseguire un&#39;operazione API client del servizio Forms a livello di programmazione, è necessario creare un oggetto API client Forms. Se utilizzate l&#39;API Java, create un `FormsServiceClient` oggetto. Se si utilizza l&#39;API del servizio Web Forms, creare un `FormsService` oggetto.

**Specificare i valori URI**

È possibile specificare i valori URI richiesti dal servizio Forms per eseguire il rendering di un modulo. Una struttura del modulo salvata come parte di un&#39;applicazione Forms può essere utilizzata come riferimento utilizzando il valore URI della directory principale del contenuto `repository:///`. Ad esempio, tenere in considerazione la seguente struttura del modulo denominata *Loan.xdp* , che si trova all&#39;interno di un&#39;applicazione Forms denominata *FormsApplication*:

![ri_ri_formrepository](assets/ri_ri_formrepository.png)

Per accedere a questa struttura del modulo, specificare `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp` come nome del modulo (il primo parametro passato al `renderPDFForm` metodo) e `repository:///` come valore URI radice del contenuto.

>[!NOTE]
>
>Per informazioni sulla creazione di un&#39;applicazione Forms utilizzando Workbench, vedere la Guida [di](https://www.adobe.com/go/learn_aemforms_workbench_63)Workbench.

Il percorso di una risorsa situata in un&#39;applicazione Forms è:

`Applications/Application-name/Application-version/Folder.../Filename`

I seguenti valori mostrano alcuni esempi di valori URI:

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

Quando si esegue il rendering di un modulo interattivo, è possibile definire valori URI quali l&#39;URL di destinazione in cui vengono inviati i dati del modulo. L’URL di destinazione può essere definito in uno dei modi seguenti:

* Sul pulsante Invia durante la progettazione della struttura del modulo in Designer
* Utilizzando l&#39;API client del servizio Forms

Se l&#39;URL di destinazione è definito all&#39;interno della struttura del modulo, non ignorarlo con l&#39;API client del servizio Forms. In altre parole, l&#39;impostazione dell&#39;URL di destinazione tramite l&#39;API Forms consente di ripristinare l&#39;URL specificato nella struttura del modulo a quello specificato tramite l&#39;API. Se si desidera inviare il modulo PDF all&#39;URL di destinazione specificato nella struttura del modulo, impostare l&#39;URL di destinazione a livello di programmazione su una stringa vuota.

Se si dispone di un modulo contenente un pulsante di invio e un pulsante di calcolo (con uno script corrispondente eseguito sul server), è possibile definire a livello di programmazione l&#39;URL al quale viene inviato il modulo per eseguire lo script. Utilizzare il pulsante di invio nella struttura del modulo per specificare l&#39;URL in cui vengono inviati i dati del modulo. (Vedere [Calcolo dei dati](/help/forms/developing/calculating-form-data.md)del modulo.)

>[!NOTE]
>
>Anziché specificare un valore URL per fare riferimento a un file XDP, è anche possibile trasmettere un&#39; `com.adobe.idp.Document` istanza al servizio Forms. L&#39; `com.adobe.idp.Document` istanza contiene una struttura del modulo. (vedere [Trasmissione di documenti al servizio](/help/forms/developing/passing-documents-forms-service.md)Forms).

**Allega file al modulo**

È possibile allegare file a un modulo. Quando si esegue il rendering di un modulo PDF con file allegati, gli utenti possono recuperare i file allegati in Acrobat utilizzando il riquadro degli allegati. È possibile allegare tipi di file diversi a un modulo, ad esempio un file di testo, o a un file binario come un file JPG.

>[!NOTE]
>
>L&#39;associazione di file allegati a un modulo è facoltativa.

**Rendering di un modulo PDF interattivo**

Per eseguire il rendering di un modulo, utilizzare una struttura del modulo creata in Designer e salvata come file XDP o PDF. È inoltre possibile eseguire il rendering di un modulo creato con Acrobat e salvato come file PDF. Per eseguire il rendering di un modulo PDF interattivo, richiamare il metodo `FormsServiceClient` o `renderPDFForm` il `renderPDFForm2` metodo dell&#39;oggetto.

L&#39;oggetto `renderPDFForm` utilizza un `URLSpec` oggetto. Il livello principale del contenuto del file XDP viene passato al servizio Forms utilizzando il metodo `URLSpec` dell&#39;oggetto `setContentRootURI` . Il nome della struttura del modulo ( `formQuery`) viene passato come valore di parametro separato. I due valori vengono concatenati per ottenere il riferimento assoluto alla struttura del modulo.

Il `renderPDFForm2` metodo accetta un&#39; `com.adobe.idp.Document` istanza che contiene il documento XDP o PDF da sottoporre a rendering.

>[!NOTE]
>
>L&#39;opzione PDF con tag non può essere impostata se il documento di input è un documento PDF. Se il file di input è un file XDP, è possibile impostare l&#39;opzione PDF con tag.

## Eseguire il rendering di un modulo PDF interattivo utilizzando l&#39;API Java {#render-an-interactive-pdf-form-using-the-java-api}

Eseguire il rendering di un modulo PDF interattivo utilizzando l&#39;API Forms (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API client Forms

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `FormsServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Specificare i valori URI

   * Creare un `URLSpec` oggetto che memorizza i valori URI utilizzando il relativo costruttore.
   * Richiamate il metodo dell&#39; `URLSpec` oggetto `setApplicationWebRoot` e passate un valore di stringa che rappresenta la radice Web dell&#39;applicazione.
   * Richiamate il metodo dell&#39; `URLSpec` oggetto `setContentRootURI` e passate un valore di stringa che specifica il valore URI della radice del contenuto. Verificare che la struttura del modulo si trovi nell&#39;URI della directory principale del contenuto. In caso contrario, il servizio Forms genera un&#39;eccezione. Per fare riferimento alla directory archivio, specificare `repository:///`.
   * Richiamare il metodo dell&#39; `URLSpec` oggetto `setTargetURL` e passare un valore di stringa che specifica il valore dell&#39;URL di destinazione in cui vengono inviati i dati del modulo. Se si definisce l&#39;URL di destinazione nella struttura del modulo, è possibile passare una stringa vuota. È inoltre possibile specificare l&#39;URL al quale viene inviato il modulo per eseguire i calcoli.

1. Allega file al modulo

   * Creare un `java.util.HashMap` oggetto per memorizzare gli allegati utilizzando il relativo costruttore.
   * Richiamare il metodo dell&#39; `java.util.HashMap` oggetto `put` affinché ciascun file venga allegato al modulo di cui è stato effettuato il rendering. Passa i seguenti valori a questo metodo:

      * Una stringa che specifica il nome dell&#39;allegato del file, inclusa l&#39;estensione del nome del file.
   * Un `com.adobe.idp.Document` oggetto che contiene l&#39;allegato del file.

   >[!NOTE]
   >
   >Ripetere questo passaggio per ogni file da allegare al modulo. Questo passaggio è facoltativo e puoi passare `null` se non desideri inviare allegati.

1. Rendering di un modulo PDF interattivo

   Richiama il metodo dell’ `FormsServiceClient` oggetto `renderPDFForm` e passa i seguenti valori:

   * Una stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, è necessario specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un `com.adobe.idp.Document` oggetto che contiene i dati da unire al modulo. Se non si desidera unire i dati, passare un `com.adobe.idp.Document` oggetto vuoto.
   * Un `PDFFormRenderSpec` oggetto che memorizza le opzioni di esecuzione. Si tratta di un parametro facoltativo e potete specificare `null` se non desiderate specificare le opzioni di esecuzione.
   * Un `URLSpec` oggetto che contiene valori URI richiesti dal servizio Forms.
   * Un `java.util.HashMap` oggetto che memorizza gli allegati. Si tratta di un parametro facoltativo e potete specificare `null` se non desiderate allegare file al modulo.

   Il `renderPDFForm` metodo restituisce un `FormsResult` oggetto che contiene un flusso di dati del modulo che deve essere scritto nel browser Web del client.

1. Scrivere il flusso di dati del modulo nel browser Web del client

   * Creare un `com.adobe.idp.Document` oggetto richiamando il `FormsResult` metodo ‘s `getOutputContent` .
   * Ottenere il tipo di contenuto dell&#39; `com.adobe.idp.Document` oggetto richiamandone il `getContentType` metodo.
   * Impostare il tipo di contenuto dell&#39; `javax.servlet.http.HttpServletResponse` oggetto richiamandone `setContentType` il metodo e passando il tipo di contenuto dell&#39; `com.adobe.idp.Document` oggetto.
   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser Web del client richiamando il `javax.servlet.http.HttpServletResponse` metodo dell&#39; `getOutputStream` oggetto.
   * Creare un `java.io.InputStream` oggetto richiamando il `com.adobe.idp.Document` metodo dell&#39; `getInputStream` oggetto.
   * Creare un array di byte e compilarlo con il flusso di dati del modulo richiamando il metodo dell&#39; `InputStream` oggetto `read` e passando l&#39;array di byte come argomento.
   * Richiamare il metodo dell&#39; `javax.servlet.ServletOutputStream` oggetto `write` per inviare il flusso di dati del modulo al browser Web del client. Passa l&#39;array di byte al `write` metodo.

## Eseguire il rendering di un modulo PDF interattivo utilizzando l&#39;API del servizio Web {#render-an-interactive-pdf-form-using-the-web-service-api}

Eseguire il rendering di un modulo PDF interattivo utilizzando l&#39;API Forms (servizio Web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il WSDL del servizio Forms.
   * Includete le classi proxy Java nel percorso della classe.

1. Creare un oggetto API client Forms

   Creare un `FormsService` oggetto e impostare i valori di autenticazione.

1. Specificare i valori URI

   * Creare un `URLSpec` oggetto che memorizza i valori URI utilizzando il relativo costruttore.
   * Richiamate il metodo dell&#39; `URLSpec` oggetto `setApplicationWebRoot` e passate un valore di stringa che rappresenta la radice Web dell&#39;applicazione.
   * Richiamate il metodo dell&#39; `URLSpec` oggetto `setContentRootURI` e passate un valore di stringa che specifica il valore URI della radice del contenuto. Verificare che la struttura del modulo si trovi nell&#39;URI della directory principale del contenuto. In caso contrario, il servizio Forms genera un&#39;eccezione. Per fare riferimento alla directory archivio, specificare `repository:///`.
   * Richiamare il metodo dell&#39; `URLSpec` oggetto `setTargetURL` e passare un valore di stringa che specifica il valore dell&#39;URL di destinazione in cui vengono inviati i dati del modulo. Se si definisce l&#39;URL di destinazione nella struttura del modulo, è possibile passare una stringa vuota. È inoltre possibile specificare l&#39;URL al quale viene inviato il modulo per eseguire i calcoli.

1. Allega file al modulo

   * Creare un `java.util.HashMap` oggetto per memorizzare gli allegati utilizzando il relativo costruttore.
   * Richiamare il metodo dell&#39; `java.util.HashMap` oggetto `put` affinché ciascun file venga allegato al modulo di cui è stato effettuato il rendering. Passa i seguenti valori a questo metodo:

      * Una stringa che specifica il nome dell&#39;allegato del file, inclusa l&#39;estensione del nome file
   * Un `BLOB` oggetto che contiene l&#39;allegato del file

   >[!NOTE]
   >
   >Ripetere questo passaggio per ogni file da allegare al modulo.

1. Rendering di un modulo PDF interattivo

   Richiama il metodo dell’ `FormsService` oggetto `renderPDFForm` e passa i seguenti valori:

   * Una stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, è necessario specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un `BLOB` oggetto che contiene i dati da unire al modulo. Se non si desidera unire i dati, passare `null`.
   * Un `PDFFormRenderSpec` oggetto che memorizza le opzioni di esecuzione. Si tratta di un parametro facoltativo e potete specificare `null` se non desiderate specificare le opzioni di esecuzione.
   * Un `URLSpec` oggetto che contiene valori URI richiesti dal servizio Forms.
   * Un `java.util.HashMap` oggetto che memorizza gli allegati. Si tratta di un parametro facoltativo e potete specificare `null` se non desiderate allegare file al modulo.
   * Un oggetto vuoto `com.adobe.idp.services.holders.BLOBHolder` compilato dal metodo. Viene utilizzato per memorizzare il modulo PDF di cui è stato effettuato il rendering.
   * Un oggetto vuoto `javax.xml.rpc.holders.LongHolder` compilato dal metodo. Questo argomento consente di memorizzare il numero di pagine nel modulo.
   * Un oggetto vuoto `javax.xml.rpc.holders.StringHolder` compilato dal metodo. (Questo argomento memorizza il valore delle impostazioni internazionali.)
   * Un oggetto vuoto `com.adobe.idp.services.holders.FormsResultHolder` che conterrà i risultati dell&#39;operazione.

   Il `renderPDFForm` metodo compila l&#39; `com.adobe.idp.services.holders.FormsResultHolder` oggetto passato come valore dell&#39;ultimo argomento con un flusso di dati del modulo che deve essere scritto nel browser Web del client.

1. Scrivere il flusso di dati del modulo nel browser Web del client

   * Creare un `FormResult` oggetto ottenendo il valore del membro `com.adobe.idp.services.holders.FormsResultHolder` dati dell&#39; `value` oggetto.
   * Creare un `BLOB` oggetto che contenga dati del modulo richiamando il `FormsResult` metodo dell&#39; `getOutputContent` oggetto.
   * Ottenere il tipo di contenuto dell&#39; `BLOB` oggetto richiamandone il `getContentType` metodo.
   * Impostare il tipo di contenuto dell&#39; `javax.servlet.http.HttpServletResponse` oggetto richiamandone `setContentType` il metodo e passando il tipo di contenuto dell&#39; `BLOB` oggetto.
   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser Web del client richiamando il `javax.servlet.http.HttpServletResponse` metodo dell&#39; `getOutputStream` oggetto.
   * Creare un array di byte e compilarlo richiamando il metodo dell&#39; `BLOB` oggetto `getBinaryData` . Questa attività assegna il contenuto dell&#39; `FormsResult` oggetto all&#39;array di byte.
   * Richiamare il metodo dell&#39; `javax.servlet.http.HttpServletResponse` oggetto `write` per inviare il flusso di dati del modulo al browser Web del client. Passa l&#39;array di byte al `write` metodo.

**Scrivere il flusso di dati del modulo nel browser Web del client**

Quando il servizio Forms esegue il rendering di un modulo, restituisce un flusso di dati del modulo che è necessario scrivere nel browser Web del client. Una volta scritto nel browser Web del client, il modulo è visibile all&#39;utente.
