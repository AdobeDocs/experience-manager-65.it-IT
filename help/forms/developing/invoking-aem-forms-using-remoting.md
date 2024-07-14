---
title: Richiamare AEM Forms tramite la comunicazione remota
description: Utilizzare la funzione di comunicazione remota per richiamare un processo AEM Forms per richiamare i processi creati in Workbench. Puoi richiamare un processo AEM Forms da un’applicazione client creata con Flex.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
role: Developer
exl-id: 94a48776-f537-4b4e-8d71-51b08e463cba
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations,Workbench
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '4604'
ht-degree: 0%

---

# Richiamare AEM Forms tramite la comunicazione remota {#invoking-aem-forms-using-remoting}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

I processi creati in Workbench possono essere richiamati utilizzando la funzione di comunicazione remota. In altre parole, è possibile richiamare un processo AEM Forms da un’applicazione client creata con Flex. Questa funzione si basa su Data Services.

>[!NOTE]
>
>Quando si utilizza la comunicazione remota, è consigliabile richiamare i processi creati in Workbench anziché i servizi di AEM Forms. Tuttavia, è possibile invocare direttamente i servizi di AEM Forms. Consulta Crittografia dei documenti di PDF tramite la comunicazione remota disponibile in AEM Forms Developer Center.

>[!NOTE]
>
>Se un servizio AEM Forms non è configurato per consentire l’accesso anonimo, le richieste provenienti da un client Flex generano un problema con il browser web. L&#39;utente deve immettere il nome utente e la password.

È possibile richiamare il seguente processo di breve durata di AEM Forms, denominato `MyApplication/EncryptDocument`, utilizzando la funzionalità di comunicazione remota. (Per informazioni sul processo, ad esempio i valori di input e output, vedere [Esempio di processo di breve durata](/help/forms/developing/aem-forms-processes.md).)

![ui_iu_encryptdocumentprocess2](assets/iu_iu_encryptdocumentprocess2.png)

>[!NOTE]
>
>Per richiamare un processo AEM Forms utilizzando un’applicazione Flex, accertati che sia abilitato un endpoint remoto. Per impostazione predefinita, quando si distribuisce un processo viene abilitato un endpoint remoto.

Quando viene richiamato, il processo esegue le azioni seguenti:

1. Ottiene il documento PDF non protetto passato come valore di input. Questa azione è basata sull&#39;operazione `SetValue`. Il nome del parametro di input è `inDoc` e il relativo tipo di dati è `document`. Il tipo di dati `document` è un tipo di dati disponibile all&#39;interno di Workbench.
1. Crittografa il documento PDF con una password. Questa azione è basata sull&#39;operazione `PasswordEncryptPDF`. Il nome del valore di output per questo processo è `outDoc` e rappresenta il documento PDF crittografato con password. Il tipo di dati di outDoc è `document`.
1. Salva il documento PDF crittografato con password come file PDF nel file system locale. Questa azione è basata sull&#39;operazione `WriteDocument`.

>[!NOTE]
>
>Il processo `MyApplication/EncryptDocument` non è basato su un processo AEM Forms esistente. Per seguire insieme agli esempi di codice, creare un processo denominato `MyApplication/EncryptDocument` utilizzando Workbench.

>[!NOTE]
>
>Per informazioni sull&#39;utilizzo della funzionalità di comunicazione remota per richiamare un processo di lunga durata, vedere [Richiamare processi di lunga durata incentrati sull&#39;uomo](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

**Consulta anche**

[Inclusione del file della libreria Flex di AEM Forms](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Gestione dei documenti con (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[Richiamare un processo di breve durata passando un documento non sicuro utilizzando (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Autenticazione delle applicazioni client create con Flex](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[Passaggio di documenti protetti per richiamare i processi tramite la comunicazione remota](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

[Richiamare servizi di componenti personalizzati tramite la comunicazione remota](invoking-aem-forms-using-remoting.md#invoking-custom-component-services-using-remoting)

[Creazione di un&#39;applicazione client creata con Flex che richiama un processo di lunga durata incentrato sull&#39;uomo](/help/forms/developing/invoking-human-centric-long-lived.md#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process)

[Creazione di applicazioni di Flash Builder che eseguono l&#39;autenticazione SSO tramite token HTTP](/help/forms/developing/creating-flash-builder-applications-perform.md#creating-flash-builder-applications-that-perform-sso-authentication-using-http-tokens)

<!-- For information on how to display process data in a Flex graph control, see [Displaying AEM Forms process data in Flex graphs](https://www.adobe.com/devnet/livecycle/articles/populating_flexcontrols.html). This URL is 404. No suitable replacement URL was found after a search. Do not make this link live if it is dead! -->

>[!NOTE]
>
>*Assicurarsi di posizionare il file crossdomain.xml nella posizione corretta. Ad esempio, supponendo che AEM Forms sia stato distribuito su JBoss, posizionare il file nel percorso seguente: &lt;directory_installazione>\Adobe_Experience_Manager_forms\jboss\server\lc_turnkey\deploy\jboss-web.deployer\ROOT.war.*

## Inclusione del file della libreria Flex di AEM Forms {#including-the-aem-forms-flex-library-file}

Per richiamare in modo programmatico i processi di AEM Forms utilizzando la funzione di comunicazione remota, aggiungi il file adobe-remoting-provider.swc al percorso della classe del progetto Flex. Il file SWC si trova nel percorso seguente:

* *&lt;directory_di_installazione>\Adobe_Experience_Manager_forms\sdk\misc\DataServices\Client-Libraries*

  dove &lt;*install_directory*> è la directory in cui è installato AEM Forms.

**Consulta anche**

[Richiamare AEM Forms tramite (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Gestione dei documenti con (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[Richiamare un processo di breve durata passando un documento non sicuro utilizzando (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Autenticazione delle applicazioni client create con Flex](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

## Gestione di documenti con la comunicazione remota {#handling-documents-with-remoting}

Uno dei più importanti tipi Java™ non primitivi utilizzati in AEM Forms è la classe `com.adobe.idp.Document`. Un documento è comunemente richiesto per richiamare un’operazione AEM Forms. Si tratta principalmente di un documento PDF, ma può contenere altri tipi di documenti, ad esempio SWF, HTML, XML o un file DOC. (Vedi [Trasmissione di dati ai servizi AEM Forms tramite l&#39;API Java](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api).)

Un&#39;applicazione client creata con Flex non può richiedere direttamente un documento. Ad esempio, non è possibile avviare Adobe Reader per richiedere un URL che generi un file PDF. Le richieste di tipi di documenti, ad esempio documenti PDF e Microsoft® Word, restituiscono un risultato che corrisponde a un URL. È responsabilità del cliente visualizzare il contenuto dell’URL. Il servizio Document Management consente di generare informazioni sull’URL e sul tipo di contenuto. Le richieste di documenti XML restituiscono il documento XML completo nel risultato.

### Trasmissione di un documento come parametro di input {#passing-a-document-as-an-input-parameter}

Un’applicazione client creata con Flex non può trasmettere un documento direttamente a un processo AEM Forms. L&#39;applicazione client utilizza invece un&#39;istanza della classe ActionScript `mx.rpc.livecycle.DocumentReference` per passare i parametri di input a un&#39;operazione che prevede un&#39;istanza `com.adobe.idp.Document`. Un&#39;applicazione client Flex dispone di diverse opzioni per la configurazione di un oggetto `DocumentReference`:

* Quando il documento si trova sul server e la posizione del file è nota, impostare la proprietà referenceType dell&#39;oggetto DocumentReference su REF_TYPE_FILE. Impostare la proprietà fileRef sulla posizione del file, come illustrato nell&#39;esempio seguente:

```java
 ... var docRef: DocumentReference = new DocumentReference(); 
 docRef.referenceType = DocumentReference.REF_TYPE_FILE; 
 docRef.fileRef = "C:/install/adobe/cs2/How to Uninstall.pdf"; ...
```

* Quando il documento si trova sul server e se ne conosce l&#39;URL, impostare la proprietà referenceType dell&#39;oggetto DocumentReference su REF_TYPE_URL. Imposta la proprietà url sull’URL, come illustrato nell’esempio seguente:

```java
... var docRef: DocumentReference = new DocumentReference(); 
docRef.referenceType = DocumentReference.REF_TYPE_URL; 
docRef.url = "https://companyserver:8080/DocumentManager/116/7855"; ...
```

* Per creare un oggetto DocumentReference da una stringa di testo nell&#39;applicazione client, impostare la proprietà referenceType dell&#39;oggetto DocumentReference su REF_TYPE_INLINE. Impostare la proprietà text sul testo da includere nell&#39;oggetto, come illustrato nell&#39;esempio seguente:

```java
... var docRef: DocumentReference = new DocumentReference(); 
docRef.referenceType = DocumentReference.REF_TYPE_INLINE; 
docRef.text = "Text for my document";  // Optionally, you can override the server's default character set  // if necessary:  // docRef.charsetName=CharacterSetName  ...
```

* Quando il documento non si trova sul server, utilizza il servlet di caricamento remoto per caricare un documento in AEM Forms. Una novità di AEM Forms è la possibilità di caricare documenti protetti. Quando si carica un documento protetto, è necessario utilizzare un utente con il ruolo *Utente applicazione di caricamento documento*. Senza questo ruolo, l’utente non può caricare un documento protetto. È consigliabile utilizzare il Single Sign-On per caricare un documento protetto. (Vedi [Passaggio di documenti protetti per richiamare i processi tramite la comunicazione remota](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting).)

>[!NOTE]
>
se AEM Forms è configurato per consentire il caricamento di documenti non sicuri, puoi utilizzare un utente che non dispone del ruolo di utente dell’applicazione di caricamento documento per caricare un documento. Un utente può anche disporre dell’autorizzazione Caricamento documento. Tuttavia, se AEM Forms è configurato per consentire solo documenti protetti, accertati che l’utente disponga del ruolo di utente dell’applicazione di caricamento del documento o dell’autorizzazione di caricamento del documento. (Vedi [Configurazione di AEM Forms per accettare documenti protetti e non protetti](invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents).

Si utilizzano le funzionalità di caricamento standard del Flash per l&#39;URL di caricamento designato: `https://SERVER:PORT/remoting/lcfileupload`. È quindi possibile utilizzare l&#39;oggetto `DocumentReference` nei casi in cui è previsto un parametro di input di tipo `Document`
` private function startUpload():void  {  fileRef.addEventListener(Event.SELECT, selectHandler);  fileRef.addEventListener("uploadCompleteData", completeHandler);  try  {   var success:Boolean = fileRef.browse();  }    catch (error:Error)  {   trace("Unable to browse for files.");  }  }      private function selectHandler(event:Event):void {  var request:URLRequest = new  URLRequest("https://SERVER:PORT/remoting/lcfileupload")  try   {   fileRef.upload(request);   }    catch (error:Error)   {   trace("Unable to upload file.");   }  }    private function completeHandler(event:DataEvent):void  {   var params:Object = new Object();   var docRef:DocumentReference = new DocumentReference();   docRef.url = event.data as String;   docRef.referenceType = DocumentReference.REF_TYPE_URL;  }`Il servizio di caricamento remoto utilizza il servlet di caricamento remoto per passare un file PDF al processo `MyApplication/EncryptDocument`. (Vedi [Richiamare un processo di breve durata passando un documento non sicuro utilizzando (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting).)

```java
 
private
function startUpload(): void  { 
 fileRef.addEventListener(Event.SELECT, selectHandler); 
 fileRef.addEventListener("uploadCompleteData", completeHandler); 
 try  { 
  var success: Boolean = fileRef.browse(); 
 }  
 catch (error: Error)  { 
  trace("Unable to browse for files."); 
 } 
}   
private
function selectHandler(event: Event): void { 
 var request: URLRequest = new  URLRequest("https://SERVER:PORT/remoting/lcfileupload")  try  { 
  fileRef.upload(request); 
 }  
 catch (error: Error)  { 
  trace("Unable to upload file."); 
 } 
}  
private
function completeHandler(event: DataEvent): void  { 
 var params: Object = new Object(); 
 var docRef: DocumentReference = new DocumentReference(); 
 docRef.url = event.data as String; 
 docRef.referenceType = DocumentReference.REF_TYPE_URL; 
}
```

La Guida rapida alla comunicazione remota utilizza il servlet di caricamento della comunicazione remota per trasmettere un file PDF al processo `MyApplication/EncryptDocument`. (Vedi [Richiamare un processo di breve durata passando un documento non sicuro utilizzando (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting).)

### Trasmissione di un documento a un&#39;applicazione client {#passing-a-document-back-to-a-client-application}

Un&#39;applicazione client riceve un oggetto di tipo `mx.rpc.livecycle.DocumentReference` per un&#39;operazione di servizio che restituisce un&#39;istanza `com.adobe.idp.Document` come parametro di output. Poiché un’applicazione client si occupa di oggetti ActionScript e non di Java, non è possibile restituire un oggetto Document basato su Java a un client Flex. Il server genera invece un URL per il documento e lo restituisce al client. La proprietà `referenceType` dell&#39;oggetto `DocumentReference` specifica se il contenuto si trova nell&#39;oggetto `DocumentReference` o deve essere recuperato da un URL nella proprietà `DocumentReference.url`. La proprietà `DocumentReference.contentType` specifica il tipo di documento.

**Consulta anche**

[Richiamare AEM Forms tramite (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Inclusione del file della libreria Flex di AEM Forms](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Richiamare un processo di breve durata passando un documento non sicuro utilizzando (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Autenticazione delle applicazioni client create con Flex](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[Passaggio di documenti protetti per richiamare i processi tramite la comunicazione remota](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

## Richiamare un processo di breve durata passando un documento non sicuro tramite la comunicazione remota {#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting}

Per richiamare un processo AEM Forms da un’applicazione creata con Flex, esegui le seguenti attività:

1. Crea un&#39;istanza `mx:RemoteObject`.
1. Crea un&#39;istanza `ChannelSet`.
1. Passa i valori di input richiesti.
1. Gestisce i valori restituiti.

>[!NOTE]
>
Questa sezione illustra come richiamare un processo AEM Forms e caricare un documento quando AEM Forms è configurato per caricare documenti non sicuri. Per informazioni su come richiamare i processi AEM Forms e caricare documenti protetti e su come configurare AEM Forms per accettare documenti protetti e non protetti, vedere [Passaggio di documenti protetti per richiamare i processi tramite la comunicazione remota](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting).

**Creazione di un&#39;istanza mx:RemoteObject**

Si crea un&#39;istanza `mx:RemoteObject` per richiamare un processo AEM Forms creato in Workbench. Per creare un&#39;istanza di `mx:RemoteObject`, specificare i valori seguenti:

* **id:** Il nome dell&#39;istanza `mx:RemoteObject` che rappresenta il processo da richiamare.
* **destinazione:** il nome del processo AEM Forms da richiamare. Ad esempio, per richiamare il processo `MyApplication/EncryptDocument`, specificare `MyApplication/EncryptDocument`.
* **risultato:** il nome del metodo Flex che gestisce il risultato.

All&#39;interno del tag `mx:RemoteObject`, specificare un tag `<mx:method>` che specifichi il nome del metodo di chiamata del processo. In genere, il nome di un metodo di chiamata Forms è `invoke`.

Esempio Nell&#39;esempio di codice seguente viene creata un&#39;istanza `mx:RemoteObject` che richiama il processo `MyApplication/EncryptDocument`.

```java
 <mx:RemoteObject id="EncryptDocument" destination="MyApplication/EncryptDocument" result="resultHandler(event);">
          <mx:method name="invoke" result="handleExecuteInvoke(event)"/>
      </mx:RemoteObject>
```

**Crea un canale per AEM Forms**

Un’applicazione client può richiamare AEM Forms specificando un canale in MXML o ActionScript, come mostra l’ActionScript seguente. Il canale deve essere un `AMFChannel`, `SecureAMFChannel`, `HTTPChannel` o `SecureHTTPChannel`.

```java
     ...
     private function refresh():void{
         var cs:ChannelSet= new ChannelSet();
         cs.addChannel(new AMFChannel("my-amf",
             "https://yourlcserver:8080/remoting/messagebroker/amf"));
         EncryptDocument.setCredentials("administrator", "password");
         EncryptDocument.channelSet = cs;
     }
     ...
```

Assegnare l&#39;istanza `ChannelSet` al campo `channelSet` dell&#39;istanza `mx:RemoteObject` (come mostrato nell&#39;esempio di codice precedente). In genere, la classe channel viene importata in un&#39;istruzione import anziché specificare il nome completo quando si richiama il metodo `ChannelSet.addChannel`.

**Trasmissione dei valori di input**

Un processo creato in Workbench può accettare zero o più parametri di input e restituire un valore di output. Un&#39;applicazione client trasmette i parametri di input all&#39;interno di un oggetto `ActionScript` con campi corrispondenti ai parametri appartenenti al processo AEM Forms. Il processo di breve durata denominato `MyApplication/EncryptDocument` richiede un parametro di input denominato `inDoc`. Il nome dell&#39;operazione esposta dal processo è `invoke` (il nome predefinito per un processo di breve durata). (Vedi [Chiamata di AEM Forms tramite (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

Esempio Nell&#39;esempio di codice riportato di seguito viene passato un documento PDF al processo `MyApplication/EncryptDocument`:

```java
     ...
     var params:Object = new Object();
 
     //Document is an instance of DocumentReference
     //that store an unsecured PDF document
     params["inDoc"] = pdfDocument;
 
     // Invoke an operation synchronously:
     EncryptDocument.invoke(params);
     ...
```

In questo esempio di codice, `pdfDocument` è un&#39;istanza `DocumentReference` che contiene un documento PDF non protetto. Per informazioni su `DocumentReference`, vedere [Gestione dei documenti con (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting).

**Richiamo di una versione specifica di un servizio**

È possibile richiamare una versione specifica di un servizio Forms utilizzando un parametro `_version` nella mappa dei parametri della chiamata. Ad esempio, per richiamare la versione 1.2 del servizio `MyApplication/EncryptDocument`:

```java
 var params:Object = new Object();
 params["inDoc"] = pdfDocument;
 params["_version"] = "1.2"
 var token:AsyncToken = echoService.echoString(params);
```

Il parametro `version` deve essere una stringa contenente un singolo punto. I valori a sinistra, versione principale e a destra, versione secondaria, del periodo devono essere numeri interi. Se questo parametro non viene specificato, viene richiamata la versione head attiva.

**Gestione dei valori restituiti**

I parametri di output dei processi di AEM Forms vengono deserializzati in oggetti ActionScript dai quali l&#39;applicazione client estrae parametri specifici per nome, come illustrato nell&#39;esempio seguente. Il valore di output del processo `MyApplication/EncryptDocument` è denominato `outDoc`.

```java
     ...
     var res:Object = event.result;
     var docRef:DocumentReference = res["outDoc"] as DocumentReference;
     ...
```

**Richiamo del processo MyApplication/EncryptDocument**

È possibile richiamare il processo `MyApplication/EncryptDocument` eseguendo i passaggi seguenti:

1. Creare un&#39;istanza `mx:RemoteObject` tramite ActionScript o MXML. Vedere Creazione di un&#39;istanza mx:RemoteObject.
1. Configura un&#39;istanza `ChannelSet` per comunicare con AEM Forms e associala all&#39;istanza `mx:RemoteObject`. Consulta Creazione di un canale per AEM Forms.
1. Chiamare il metodo `login` di ChannelSet o il metodo `setCredentials` del servizio per specificare il valore e la password dell&#39;identificatore utente. (Vedere [Utilizzo del Single Sign-On](invoking-aem-forms-using-remoting.md#using-single-sign-on).)
1. Compilare un&#39;istanza `mx.rpc.livecycle.DocumentReference` con un documento PDF non protetto da passare al processo `MyApplication/EncryptDocument`. (Vedi [Trasmissione di un documento come parametro di input](invoking-aem-forms-using-remoting.md#passing-a-document-as-an-input-parameter).)
1. Crittografare il documento PDF chiamando il metodo `invoke` dell&#39;istanza `mx:RemoteObject`. Passa `Object` che contiene il parametro di input (che è il documento di PDF non protetto). Consulta Trasmissione dei valori di input.
1. Recuperare il documento PDF crittografato con password restituito dal processo. Consulta Gestione dei valori restituiti.

[Guida introduttiva: richiamare un processo di breve durata passando un documento non sicuro utilizzando (obsoleto per i moduli AEM) AEM Forms Remoting](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-by-passing-an-unsecure-document-using-deprecated-for-aem-forms-aem-forms-remoting)

## Autenticazione delle applicazioni client create con Flex {#authenticating-client-applications-built-with-flex}

Sono disponibili diversi modi in cui AEM Forms User Manager può autenticare una richiesta remota da un’applicazione Flex, tra cui AEM Forms single sign-on tramite il servizio di accesso centrale, l’autenticazione di base e l’autenticazione personalizzata. Se non è abilitato né il Single Sign-On né l&#39;accesso anonimo, una richiesta di comunicazione remota determina l&#39;autenticazione di base (impostazione predefinita) o personalizzata.

L’autenticazione di base si basa sull’autenticazione di base standard J2EE dal contenitore dell’applicazione web. Per l’autenticazione di base, un errore HTTP 401 causa un problema del browser. Ciò significa che quando si tenta di connettersi a un&#39;applicazione Forms utilizzando RemoteObject e non si è ancora effettuato l&#39;accesso dall&#39;applicazione Flex, il browser richiede un nome utente e una password.

Per l&#39;autenticazione personalizzata, il server invia un errore al client per indicare che è necessaria l&#39;autenticazione.

>[!NOTE]
>
Per informazioni sull&#39;esecuzione dell&#39;autenticazione tramite token HTTP, vedere [Creazione di applicazioni di Flash Builder che eseguono l&#39;autenticazione SSO tramite token HTTP](/help/forms/developing/creating-flash-builder-applications-perform.md#creating-flash-builder-applications-that-perform-sso-authentication-using-http-tokens).

### Utilizzo dell’autenticazione personalizzata {#using-custom-authentication}

Per abilitare l’autenticazione personalizzata nella console di amministrazione, devi modificare il metodo di autenticazione da Basic a Custom sull’endpoint remoto. Se si utilizza l&#39;autenticazione personalizzata, l&#39;applicazione client chiama il metodo `ChannelSet.login` per accedere e il metodo `ChannelSet.logout` per disconnettersi.

>[!NOTE]
>
Nella versione precedente di AEM Forms, hai inviato le credenziali a una destinazione chiamando il metodo `RemoteObject.setCredentials`. Il metodo `setCredentials` non ha passato le credenziali al server fino al primo tentativo del componente di connettersi al server. Pertanto, se il componente ha generato un evento di errore, non è possibile stabilire con certezza se l&#39;errore è stato causato da un errore di autenticazione o da un altro motivo. Il metodo `ChannelSet.login` si connette al server quando viene chiamato in modo da poter gestire immediatamente un problema di autenticazione. Sebbene sia possibile continuare a utilizzare il metodo `setCredentials`, si consiglia di utilizzare il metodo `ChannelSet.login`.

Poiché più destinazioni possono utilizzare gli stessi canali e l&#39;oggetto ChannelSet corrispondente, l&#39;accesso a una destinazione comporta l&#39;accesso dell&#39;utente a qualsiasi altra destinazione che utilizza lo stesso canale o gli stessi canali. Se due componenti applicano credenziali diverse allo stesso oggetto ChannelSet, vengono utilizzate le ultime credenziali applicate. Se più componenti utilizzano lo stesso oggetto ChannelSet autenticato, la chiamata al metodo `logout` registra tutti i componenti fuori dalle destinazioni.

Nell&#39;esempio seguente vengono utilizzati i metodi `ChannelSet.login` e `ChannelSet.logout` con un controllo RemoteObject. Questa applicazione esegue le azioni seguenti:

* Crea un oggetto `ChannelSet` nel gestore `creationComplete` che rappresenta i canali utilizzati dal componente `RemoteObject`
* Passa le credenziali al server chiamando la funzione `ROLogin` in risposta a un evento di clic Button
* Utilizza il componente RemoteObject per inviare una stringa al server in risposta a un evento di clic Button. Il server restituisce la stessa stringa al componente RemoteObject
* Utilizza l&#39;evento result del componente RemoteObject per visualizzare la stringa in un controllo TextArea
* Esci dal server chiamando la funzione `ROLogout` in risposta a un evento di clic su pulsante

```java
 <?xml version="1.0"?>
 <!-- security/SecurityConstraintCustom.mxml -->
 <mx:Application xmlns:mx="https://www.adobe.com/2006/mxml" width="100%"
     height="100%" creationComplete="creationCompleteHandler();">
 
     <mx:Script>
         <![CDATA[
             import mx.controls.Alert;
             import mx.messaging.config.ServerConfig;
             import mx.rpc.AsyncToken;
             import mx.rpc.AsyncResponder;
             import mx.rpc.events.FaultEvent;
             import mx.rpc.events.ResultEvent;
             import mx.messaging.ChannelSet;
 
             // Define a ChannelSet object.
             public var cs:ChannelSet;
 
             // Define an AsyncToken object.
             public var token:AsyncToken;
 
             // Initialize ChannelSet object based on the
             // destination of the RemoteObject component.
             private function creationCompleteHandler():void {
                 if (cs == null)
                 cs = ServerConfig.getChannelSet(remoteObject.destination);
             }
 
             // Login and handle authentication success or failure.
             private function ROLogin():void {
                 // Make sure that the user is not already logged in.
                 if (cs.authenticated == false) {
                     token = cs.login("sampleuser", "samplepassword");
                     // Add result and fault handlers.
                     token.addResponder(new AsyncResponder(LoginResultEvent,
                     LoginFaultEvent));
                 }
             }
 
             // Handle successful login.
             private function LoginResultEvent(event:ResultEvent,
                 token:Object=null):void  {
                     switch(event.result) {
                         case "success":
                             authenticatedCB.selected = true;
                             break;
                             default:
                     }
                 }
 
                 // Handle login failure.
                 private function LoginFaultEvent(event:FaultEvent,
                     token:Object=null):void {
                         switch(event.fault.faultCode) {
                             case "Client.Authentication":
                                 default:
                                 authenticatedCB.selected = false;
                                 Alert.show("Login failure: " + event.fault.faultString);
                     }
                 }
 
                 // Logout and handle success or failure.
                 private function ROLogout():void {
                     // Add result and fault handlers.
                     token = cs.logout();
                     token.addResponder(new
                         AsyncResponder(LogoutResultEvent,LogoutFaultEvent));
                 }
 
                 // Handle successful logout.
                 private function LogoutResultEvent(event:ResultEvent,
                     token:Object=null):void {
                         switch (event.result) {
                             case "success":
                                 authenticatedCB.selected = false;
                                 break;
                                 default:
                     }
                 }
 
                 // Handle logout failure.
                 private function LogoutFaultEvent(event:FaultEvent,
                     token:Object=null):void {
                         Alert.show("Logout failure: " + event.fault.faultString);
                 }
                 // Handle message recevied by RemoteObject component.
                 private function resultHandler(event:ResultEvent):void {
                     ta.text += "Server responded: "+ event.result + "\n";
                 }
 
                 // Handle fault from RemoteObject component.
                 private function faultHandler(event:FaultEvent):void {
                     ta.text += "Received fault: " + event.fault + "\n";
                 }
             ]]>
     </mx:Script>
     <mx:HBox>
         <mx:Label text="Enter a text for the server to echo"/>
         <mx:TextInput id="ti" text="Hello World!"/>
         <mx:Button label="Login"
             click="ROLogin();"/>
         <mx:Button label="Echo"
             enabled="{authenticatedCB.selected}"
             click="remoteObject.echo(ti.text);"/>
         <mx:Button label="Logout"
             click="ROLogout();"/>
         <mx:CheckBox id="authenticatedCB"
             label="Authenticated?"
             enabled="false"/>
     </mx:HBox>
     <mx:TextArea id="ta" width="100%" height="100%"/>
 
     <mx:RemoteObject id="remoteObject"
         destination="myDest"
         result="resultHandler(event);"
         fault="faultHandler(event);"/>
 </mx:Application>
```

I metodi `login` e `logout` restituiscono un oggetto AsyncToken. Assegnare gestori eventi all&#39;oggetto AsyncToken affinché l&#39;evento risultante gestisca una chiamata riuscita e l&#39;evento di errore gestisca un errore.

### Utilizzo del Single Sign-On {#using-single-sign-on}

Gli utenti di moduli AEM possono connettersi a più applicazioni web AEM Forms per eseguire un’attività. Quando gli utenti passano da un’applicazione web a un’altra, non è efficiente richiedere loro di accedere separatamente a ogni applicazione web. Il meccanismo single sign-on di AEM Forms consente agli utenti di accedere una sola volta e quindi a qualsiasi applicazione web AEM Forms. Poiché gli sviluppatori di AEM Forms possono creare applicazioni client da utilizzare con AEM Forms, devono anche poter sfruttare il meccanismo di single sign-on.

Ogni applicazione web AEM Forms viene inserita in un proprio file di archivio web (WAR), che viene quindi inserito in un pacchetto come parte di un file di archivio aziendale (EAR). Poiché un server applicazioni non consente la condivisione dei dati di sessione tra diverse applicazioni web, AEM Forms utilizza i cookie HTTP per memorizzare le informazioni di autenticazione. I cookie di autenticazione consentono a un utente di accedere a un’applicazione Forms e quindi di connettersi ad altre applicazioni web AEM Forms. Questa tecnica è nota come single sign-on.

Gli sviluppatori di AEM Forms scrivono applicazioni client per estendere le funzionalità delle guide dei moduli (obsolete) e personalizzare Workspace. Un&#39;applicazione Workspace, ad esempio, può avviare un processo. L&#39;applicazione client utilizza quindi un endpoint remoto per recuperare i dati dal servizio Forms.

Quando un servizio AEM Forms viene richiamato utilizzando (obsoleto per i moduli AEM) AEM Forms Remoting, l’applicazione client trasmette il cookie di autenticazione come parte della richiesta. Poiché l’utente ha già eseguito l’autenticazione, non è necessario alcun accesso aggiuntivo per effettuare una connessione dall’applicazione client al servizio AEM Forms.

>[!NOTE]
>
Se un cookie non è valido o è mancante, non esiste alcun reindirizzamento implicito a una pagina di accesso. Pertanto, è ancora possibile chiamare un servizio anonimo.

È possibile evitare il meccanismo Single Sign-On di AEM Forms scrivendo un&#39;applicazione client che esegue l&#39;accesso e la disconnessione autonomamente. Se si ignora il meccanismo Single Sign-On, è possibile utilizzare l&#39;autenticazione di base o personalizzata con l&#39;applicazione.

Poiché questo meccanismo non utilizza il meccanismo Single Sign-On di AEM Forms, nel client non viene scritto alcun cookie di autenticazione. Le credenziali di accesso sono archiviate nell&#39;oggetto `ChannelSet` per il canale remoto. Pertanto, qualsiasi chiamata `RemoteObject` effettuata sullo stesso `ChannelSet` viene effettuata nel contesto di tali credenziali.

### Configurazione del single sign-on in AEM Forms {#setting-up-single-sign-on-in-aem-forms}

Per utilizzare il single sign-on in AEM Forms, installa il componente del flusso di lavoro moduli, che include il servizio di accesso centralizzato. Dopo che un utente ha effettuato l’accesso, il servizio di accesso centralizzato restituisce all’utente un cookie di autenticazione. Ogni richiesta successiva a un’applicazione web Forms contiene il cookie. Se il cookie è valido, l’utente viene considerato autenticato e non deve effettuare di nuovo l’accesso.

### Scrittura di un&#39;applicazione client che utilizza il Single Sign-On {#writing-a-client-application-that-uses-single-sign-on}

Quando si utilizza il meccanismo di accesso singolo, è possibile che gli utenti accedano utilizzando il servizio di accesso centralizzato prima di avviare un&#39;applicazione client. In altre parole, un&#39;applicazione client non effettua l&#39;accesso tramite il browser o chiamando il metodo `ChannelSet.login`.

Se utilizzi il meccanismo Single Sign-On di AEM Forms, configura l’endpoint remoto in modo che utilizzi l’autenticazione personalizzata, non di base. In caso contrario, quando si utilizza l’autenticazione di base, un errore di autenticazione causa un problema del browser che non deve essere visualizzato dall’utente. Al contrario, l’applicazione rileva l’errore di autenticazione e quindi visualizza un messaggio per istruire l’utente ad accedere utilizzando il servizio di accesso centralizzato.

Un&#39;applicazione client accede ad AEM Forms tramite un endpoint remoto utilizzando il componente `RemoteObject`, come illustrato nell&#39;esempio seguente.

```java
 <?xml version="1.0"?>
 <mx:Application
        backgroundColor="#FFFFFF">
 
       <mx:Script>
          <![CDATA[
 
            import mx.controls.Alert;
            import mx.rpc.events.FaultEvent;
 
            // Prompt user to login on a fault.
            private function faultHandler(event:FaultEvent):void
            {
             if(event.fault.faultCode=="Client.Authentication")
             {
                 Alert.show(
                     event.fault.faultString + "\n" +
                     event.fault.faultCode + "\n" +
                     "Please login to continue.");
             }
         }
          ]]>
       </mx:Script>
 
       <mx:RemoteObject id="srv"
           destination="product"
           fault="faultHandler(event);"/>
 
       <mx:DataGrid
           width="100%" height="100%"
           dataProvider="{srv.getProducts.lastResult}"/>
 
       <mx:Button label="Get Data"
           click="srv.getProducts();"/>
 
 </mx:Application>
```

**Accesso come nuovo utente mentre l&#39;applicazione Flex è ancora in esecuzione**

Un’applicazione creata con Flex include il cookie di autenticazione con ogni richiesta a un servizio AEM Forms. Per motivi di prestazioni, AEM Forms non convalida il cookie su ogni richiesta. Tuttavia, AEM Forms rileva quando un cookie di autenticazione viene sostituito da un altro cookie di autenticazione.

Ad esempio, si avvia un&#39;applicazione client e mentre l&#39;applicazione è attiva, si utilizza il servizio di accesso centralizzato per disconnettersi. Quindi, puoi accedere come un altro utente. L’accesso come utente diverso sostituisce il cookie di autenticazione esistente con un cookie di autenticazione per il nuovo utente.

Alla successiva richiesta dell’applicazione client, AEM Forms rileva che il cookie è stato modificato e disconnette l’utente. Pertanto, la prima richiesta dopo una modifica del cookie non riesce. Tutte le richieste successive vengono effettuate nel contesto del nuovo cookie e hanno esito positivo.

**Disconnessione**

Per disconnettersi da AEM Forms e annullare la validità di una sessione, il cookie di autenticazione deve essere eliminato dal computer del client. Poiché lo scopo del Single Sign-On è consentire a un utente di effettuare l&#39;accesso una sola volta, non si desidera che un&#39;applicazione client elimini il cookie. Questa azione comporta la disconnessione dell’utente.

La chiamata al metodo `RemoteObject.logout` in un&#39;applicazione client genera quindi un messaggio di errore nel client che specifica che la sessione non è disconnessa. L’utente può utilizzare il servizio di accesso centralizzato per disconnettersi ed eliminare il cookie di autenticazione.

**Disconnessione mentre l&#39;applicazione Flex è ancora in esecuzione**

Puoi avviare un’applicazione client creata con Flex e utilizzare il servizio di accesso centralizzato per disconnettersi. Durante il processo di disconnessione, il cookie di autenticazione viene eliminato. Se viene effettuata una richiesta remota senza un cookie o con un cookie non valido, la sessione utente viene invalidata. Questa azione corrisponde a una disconnessione. Alla successiva connessione dell’applicazione client a un servizio AEM Forms, viene richiesto all’utente di effettuare l’accesso.

**Consulta anche**

[Richiamare AEM Forms tramite (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Gestione dei documenti con (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[Inclusione del file della libreria Flex di AEM Forms](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Richiamare un processo di breve durata passando un documento non sicuro utilizzando (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Passaggio di documenti protetti per richiamare i processi tramite la comunicazione remota](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

## Passaggio di documenti protetti per richiamare i processi tramite la comunicazione remota {#passing-secure-documents-to-invoke-processes-using-remoting}

È possibile passare documenti protetti ad AEM Forms quando si richiama un processo che richiede uno o più documenti. Trasmettendo un documento sicuro si proteggono le informazioni commerciali e i documenti riservati. In questa situazione, un documento può fare riferimento a un documento PDF, a un documento XML, a un documento Word e così via. Il passaggio di un documento protetto ad AEM Forms da un’applicazione client scritta in Flex è necessario quando AEM Forms è configurato per consentire l’utilizzo di documenti protetti. (Vedi [Configurazione di AEM Forms per accettare documenti protetti e non protetti](invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents).)

Quando si passa un documento protetto, utilizzare il Single Sign-On e specificare un utente di AEM Forms con il ruolo *Utente applicazione di caricamento documento*. Senza questo ruolo, l’utente non può caricare un documento protetto. È possibile assegnare un ruolo a un utente a livello di programmazione. (Vedi [Gestione di ruoli e autorizzazioni](/help/forms/developing/users.md#managing-roles-and-permissions).)

>[!NOTE]
>
Quando crei un ruolo e desideri che i membri di tale ruolo caricino documenti protetti, accertati di specificare l’autorizzazione Caricamento documento.

AEM Forms supporta un&#39;operazione denominata `getFileUploadToken` che restituisce un token passato al servlet di caricamento. Il metodo `DocumentReference.constructRequestForUpload` richiede un URL ad AEM Forms insieme al token restituito dal metodo `LC.FileUploadAuthenticator.getFileUploadToken`. Questo metodo restituisce un oggetto `URLRequest` utilizzato nella chiamata al servlet di caricamento. Il codice seguente illustra questa logica dell&#39;applicazione.

```java
     ...
         private function startUpload():void
         {
             fileRef.addEventListener(Event.SELECT, selectHandler);
             fileRef.addEventListener("uploadCompleteData", completeHandler);
             try
             {
         var success:Boolean = fileRef.browse();
             }
             catch (error:Error)
             {
                 trace("Unable to browse for files.");
             }
 
         }
 
          private function selectHandler(event:Event):void
             {
             var authTokenService:RemoteObject = new RemoteObject("LC.FileUploadAuthenticator");
             authTokenService.addEventListener("result", authTokenReceived);
             authTokenService.channelSet = cs;
             authTokenService.getFileUploadToken();
             }
 
         private function authTokenReceived(event:ResultEvent):void
             {
             var token:String = event.result as String;
             var request:URLRequest = DocumentReference.constructRequestForUpload("http://localhost:8080", token);
 
             try
             {
           fileRef.upload(request);
             }
             catch (error:Error)
             {
             trace("Unable to upload file.");
             }
             }
 
         private function completeHandler(event:DataEvent):void
         {
 
             var params:Object = new Object();
             var docRef:DocumentReference = new DocumentReference();
             docRef.url = event.data as String;
             docRef.referenceType = DocumentReference.REF_TYPE_URL;
         }
         ...
```

)

### Configurazione di AEM Forms per accettare documenti protetti e non protetti {#configuring-aem-forms-to-accept-secure-and-unsecure-documents}

È possibile utilizzare la console di amministrazione per specificare se i documenti sono protetti quando si passa un documento da un&#39;applicazione client Flex a un processo AEM Forms. Per impostazione predefinita, AEM Forms è configurato per accettare documenti protetti. Per configurare AEM Forms per l’accettazione di documenti protetti, effettua le seguenti operazioni:

1. Accedere alla console di amministrazione.
1. Fare clic su **Impostazioni**.
1. Fare clic su **Impostazioni di sistema principali.**
1. Fai clic su Configurazioni.
1. Verificare che l&#39;opzione Consenti caricamento di documenti non protetti da applicazioni Flex non sia selezionata.

>[!NOTE]
>
* Per configurare AEM Forms per l’accettazione di documenti non protetti, seleziona l’opzione Consenti caricamento di documenti non protetti dalle applicazioni Flex. Riavviare quindi un&#39;applicazione o un servizio per assicurarsi che l&#39;impostazione abbia effetto.
* Per riavviare l&#39;SDK, si consiglia di utilizzare il comando &#39;Ctrl + C&#39;. Il riavvio dell’SDK dell’AEM con metodi alternativi, ad esempio l’arresto dei processi Java, può causare incongruenze nell’ambiente di sviluppo dell’AEM.


### Guida introduttiva: richiamare un processo di breve durata passando un documento protetto tramite la funzionalità di comunicazione remota {#quick-start-invoking-a-short-lived-process-by-passing-a-secure-document-using-remoting}

Nell&#39;esempio di codice seguente viene richiamato `MyApplication/EncryptDocument.`Un utente deve effettuare l&#39;accesso per fare clic sul pulsante Seleziona file utilizzato per caricare un file PDF e richiamare la procedura. In altre parole, una volta che l’utente è autenticato, il pulsante Seleziona file è abilitato. La figura seguente mostra l’applicazione client Flex dopo l’autenticazione di un utente. La casella di controllo Autenticato è attivata.

![ui_iu_secureremotelogin](assets/iu_iu_secureremotelogin.png)

se AEM Forms è configurato per consentire solo il caricamento di documenti protetti e l&#39;utente non ha il ruolo *Utente applicazione di caricamento documento*, viene generata un&#39;eccezione. Se l’utente dispone di questo ruolo, il file viene caricato e il processo viene richiamato.

```java
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Application  xmlns="*"
      creationComplete="initializeChannelSet();">
        <mx:Script>
        <![CDATA[
      import mx.rpc.livecycle.DocumentReference;
      import flash.net.FileReference;
      import flash.net.URLRequest;
      import flash.events.Event;
      import flash.events.DataEvent;
      import mx.messaging.ChannelSet;
      import mx.messaging.channels.AMFChannel;
      import mx.rpc.events.ResultEvent;
      import mx.collections.ArrayCollection;
      import mx.rpc.AsyncToken;
      import mx.controls.Alert;
      import mx.rpc.events.FaultEvent;
      import mx.rpc.AsyncResponder;
 
      // Classes used in file retrieval
      private var fileRef:FileReference = new FileReference();
      private var docRef:DocumentReference = new DocumentReference();
      private var parentResourcePath:String = "/";
      private var now1:Date;
      private var serverPort:String = "hiro-xp:8080";
 
      // Define a ChannelSet object.
      public var cs:ChannelSet;
 
      // Define an AsyncToken object.
      public var token:AsyncToken;
 
       // Holds information returned from AEM Forms
      [Bindable]
      public var progressList:ArrayCollection = new ArrayCollection();
 
 
      // Handles a successful login
     private function LoginResultEvent(event:ResultEvent,
         token:Object=null):void  {
             switch(event.result) {
                 case "success":
                     authenticatedCB.selected = true;
                     btnFile.enabled = true;
                     btnLogout.enabled = true;
                     btnLogin.enabled = false;
                         break;
                     default:
                 }
             }
 
 
 // Handle login failure.
 private function LoginFaultEvent(event:FaultEvent,
     token:Object=null):void {
     switch(event.fault.faultCode) {
                 case "Client.Authentication":
                         default:
                         authenticatedCB.selected = false;
                         Alert.show("Login failure: " + event.fault.faultString);
                 }
             }
 
 
      // Set up channel set to invoke AEM Forms
      private function initializeChannelSet():void {
        cs = new ChannelSet();
        cs.addChannel(new AMFChannel("remoting-amf", "https://" + serverPort + "/remoting/messagebroker/amf"));
        EncryptDocument2.channelSet = cs;
      }
 
     // Call this method to upload the file.
      // This creates a file picker and lets the user select a PDF file to pass to the EncryptDocument process.
      private function uploadFile():void {
        fileRef.addEventListener(Event.SELECT, selectHandler);
        fileRef.addEventListener(DataEvent.UPLOAD_COMPLETE_DATA,completeHandler);
        fileRef.browse();
      }
 
      // Gets called for selected file. Does the actual upload via the file upload servlet.
      private function selectHandler(event:Event):void {
              var authTokenService:RemoteObject = new RemoteObject("LC.FileUploadAuthenticator");
         authTokenService.addEventListener("result", authTokenReceived);
         authTokenService.channelSet = cs;
         authTokenService.getFileUploadToken();
      }
 
     private function authTokenReceived(event:ResultEvent):void
     {
     var token:String = event.result as String;
     var request:URLRequest = DocumentReference.constructRequestForUpload("https://hiro-xp:8080", token);
 
     try
     {
           fileRef.upload(request);
     }
     catch (error:Error)
     {
         trace("Unable to upload file.");
     }
 }
 
      // Called once the file is completely uploaded.
      private function completeHandler(event:DataEvent):void {
 
        // Set the docRef's url and referenceType parameters
        docRef.url = event.data as String;
        docRef.referenceType=DocumentReference.REF_TYPE_URL;
        executeInvokeProcess();
      }
 
     //This method invokes the EncryptDocument process
      public function executeInvokeProcess():void {
         //Create an Object to store the input value for the EncryptDocument process
           now1 = new Date();
 
         var params:Object = new Object();
         params["inDoc"]=docRef;
 
         // Invoke the EncryptDocument process
         var token:AsyncToken;
         token = EncryptDocument2.invoke(params);
         token.name = name;
      }
 
      // AEM Forms  login method
      private function ROLogin():void {
         // Make sure that the user is not already logged in.
 
         //Get the User and Password
         var userName:String = txtUser.text;
         var pass:String = txtPassword.text;
 
        if (cs.authenticated == false) {
             token = cs.login(userName, pass);
 
         // Add result and fault handlers.
         token.addResponder(new AsyncResponder(LoginResultEvent,    LoginFaultEvent));
                 }
             }
 
      // This method handles a successful process invocation
      public function handleResult(event:ResultEvent):void
      {
            //Retrieve information returned from the service invocation
          var token:AsyncToken = event.token;
          var res:Object = event.result;
          var dr:DocumentReference = res["outDoc"] as DocumentReference;
          var now2:Date = new Date();
 
           // These fields map to columns in the DataGrid
          var progObject:Object = new Object();
          progObject.filename = token.name;
          progObject.timing = (now2.time - now1.time).toString();
          progObject.state = "Success";
          progObject.link = "<a href='" + dr.url + "'> open </a>";
          progressList.addItem(progObject);
      }
 
      // Prompt user to login on a fault.
       private function faultHandler(event:FaultEvent):void
            {
             if(event.fault.faultCode=="Client.Authentication")
             {
                 Alert.show(
                     event.fault.faultString + "\n" +
                     event.fault.faultCode + "\n" +
                     "Please login to continue.");
             }
            }
 
       // AEM Forms  logout method
     private function ROLogout():void {
         // Add result and fault handlers.
         token = cs.logout();
         token.addResponder(new AsyncResponder(LogoutResultEvent,LogoutFaultEvent));
     }
 
     // Handle successful logout.
     private function LogoutResultEvent(event:ResultEvent,
         token:Object=null):void {
         switch (event.result) {
         case "success":
                 authenticatedCB.selected = false;
                 btnFile.enabled = false;
                 btnLogout.enabled = false;
                 btnLogin.enabled = true;
                 break;
                 default:
             }
     }
 
     // Handle logout failure.
     private function LogoutFaultEvent(event:FaultEvent,
             token:Object=null):void {
             Alert.show("Logout failure: " + event.fault.faultString);
     }
 
          private function resultHandler(event:ResultEvent):void {
          // Do anything else here.
          }
        ]]>
 
      </mx:Script>
      <mx:RemoteObject id="EncryptDocument" destination="MyApplication/EncryptDocument" result="resultHandler(event);">
          <mx:method name="invoke" result="handleResult(event)"/>
      </mx:RemoteObject>
 
       <!--//This consists of what is displayed on the webpage-->
      <mx:Panel id="lcPanel" title="EncryptDocument  (Deprecated for AEM forms) AEM Forms Remoting Example"
           height="25%" width="25%" paddingTop="10" paddingLeft="10" paddingRight="10"
           paddingBottom="10">
         <mx:Label width="100%" color="blue"
                text="Select a PDF file to pass to the EncryptDocument process"/>
        <mx:DataGrid x="10" y="0" width="500" id="idProgress" editable="false"
           dataProvider="{progressList}" height="231" selectable="false" >
          <mx:columns>
            <mx:DataGridColumn headerText="Filename" width="200" dataField="filename" editable="false"/>
            <mx:DataGridColumn headerText="State" width="75" dataField="state" editable="false"/>
            <mx:DataGridColumn headerText="Timing" width="75" dataField="timing" editable="false"/>
            <mx:DataGridColumn headerText="Click to Open" dataField="link" editable="false" >
             <mx:itemRenderer>
                <mx:Component>
                   <mx:Text x="0" y="0" width="100%" htmlText="{data.link}"/>
                </mx:Component>
             </mx:itemRenderer>
            </mx:DataGridColumn>
          </mx:columns>
        </mx:DataGrid>
        <mx:Button label="Select File" click="uploadFile()"  id="btnFile" enabled="false"/>
        <mx:Button label="Login" click="ROLogin();" id="btnLogin"/>
        <mx:Button label="LogOut" click="ROLogout();" enabled="false" id="btnLogout"/>
        <mx:HBox>
         <mx:Label text="User:"/>
         <mx:TextInput id="txtUser" text=""/>
         <mx:Label text="Password:"/>
         <mx:TextInput id="txtPassword" text="" displayAsPassword="true"/>
         <mx:CheckBox id="authenticatedCB"
             label="Authenticated?"
             enabled="false"/>
     </mx:HBox>
      </mx:Panel>
 </mx:Application>
```

**Consulta anche**

[Richiamare AEM Forms tramite (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Gestione dei documenti con (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[Inclusione del file della libreria Flex di AEM Forms](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Richiamare un processo di breve durata passando un documento non sicuro utilizzando (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Autenticazione delle applicazioni client create con Flex](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

## Richiamare servizi di componenti personalizzati tramite la comunicazione remota {#invoking-custom-component-services-using-remoting}

È possibile richiamare i servizi in un componente personalizzato utilizzando la funzione di comunicazione remota. Si consideri, ad esempio, il componente Banca che contiene il servizio clienti. È possibile richiamare le operazioni che appartengono al servizio clienti utilizzando un&#39;applicazione client scritta in Flex. Prima di poter eseguire l’avvio rapido associato a questa sezione, è necessario creare il componente personalizzato Banca.

Il servizio clienti espone un&#39;operazione denominata `createCustomer`. In questa discussione viene descritto come creare un&#39;applicazione client Flex che richiami il servizio clienti e crei un cliente. Questa operazione richiede un oggetto complesso di tipo `com.adobe.livecycle.sample.customer.Customer` che rappresenta il nuovo cliente. Nell&#39;illustrazione seguente viene illustrata l&#39;applicazione client che richiama l&#39;assistenza clienti e crea un nuovo cliente. L&#39;operazione `createCustomer` restituisce un valore dell&#39;identificatore del cliente. Il valore dell&#39;identificatore viene visualizzato nella casella di testo Identificatore cliente.

![ui_iu_flexnewcust](assets/iu_iu_flexnewcust.png)

Nella tabella seguente sono elencati i controlli che fanno parte di questa applicazione client.

<table>
 <thead>
  <tr>
   <th><p>Nome controllo</p></th>
   <th><p>Descrizione</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>txtFirst</p></td>
   <td><p>Specifica il nome del cliente. </p></td>
  </tr>
  <tr>
   <td><p>txtLast</p></td>
   <td><p>Specifica il cognome del cliente. </p></td>
  </tr>
  <tr>
   <td><p>txtPhone</p></td>
   <td><p>Specifica il numero di telefono del cliente.</p></td>
  </tr>
  <tr>
   <td><p>txtStreet</p></td>
   <td><p>Specifica il nome della via del cliente.</p></td>
  </tr>
  <tr>
   <td><p>txtState</p></td>
   <td><p>Specifica lo stato del cliente. </p></td>
  </tr>
  <tr>
   <td><p>txtZIP</p></td>
   <td><p>Specifica il codice postale del cliente. </p></td>
  </tr>
  <tr>
   <td><p>txtCity</p></td>
   <td><p>Specifica la città del cliente.</p></td>
  </tr>
  <tr>
   <td><p>txtCustId</p></td>
   <td><p>Specifica il valore dell'identificatore cliente a cui appartiene il nuovo account. Questa casella di testo viene compilata dal valore restituito dall'operazione <code>createCustomer</code> del servizio clienti. </p></td>
  </tr>
 </tbody>
</table>

### Mappatura di tipi di dati complessi di AEM Forms {#mapping-aem-forms-complex-data-types}

Alcune operazioni di AEM Forms richiedono tipi di dati complessi come valori di input. Questi tipi di dati complessi definiscono i valori di runtime utilizzati dall&#39;operazione. Ad esempio, l&#39;operazione `createCustomer` del servizio clienti richiede un&#39;istanza `Customer` contenente i valori di runtime richiesti dal servizio. Senza il tipo complesso, il servizio clienti genera un’eccezione e non esegue l’operazione.

Quando richiami un servizio AEM Forms, crea oggetti ActionScript mappati sui tipi complessi AEM Forms richiesti. Per ogni tipo di dati complesso richiesto da un&#39;operazione, creare un oggetto ActionScript separato.

Nella classe ActionScript, utilizzare il tag di metadati `RemoteClass` per eseguire il mapping al tipo complesso AEM Forms. Quando si richiama l&#39;operazione `createCustomer` del servizio clienti, ad esempio, creare una classe ActionScript mappata al tipo di dati `com.adobe.livecycle.sample.customer.Customer`.

La seguente classe ActionScript denominata Customer mostra come eseguire il mapping al tipo di dati di AEM Forms `com.adobe.livecycle.sample.customer.Customer`.

```java
 package customer
 
 {
     [RemoteClass(alias="com.adobe.livecycle.sample.customer.Customer")]
     public class Customer
     {
            public var name:String;
            public var street:String;
            public var city:String;
            public var state:String;
            public var phone:String;
            public var zip:int;
        }
 }
```

Il tipo di dati completo del tipo complesso AEM Forms viene assegnato al tag alias.

I campi della classe ActionScript corrispondono ai campi che appartengono al tipo complesso AEM Forms. I sei campi nella classe ActionScript cliente corrispondono ai campi che appartengono a `com.adobe.livecycle.sample.customer.Customer`.

>[!NOTE]
>
Un buon modo per determinare i nomi di campo che appartengono a un tipo complesso di Forms consiste nel visualizzare il WSDL di un servizio in un browser web. Un WSDL specifica i tipi complessi di un servizio e i membri dati corrispondenti. Il seguente WSDL è utilizzato per il servizio clienti: `https://[yourServer]:[yourPort]/soap/services/CustomerService?wsdl.`

La classe ActionScript cliente appartiene a un pacchetto denominato cliente. È consigliabile inserire nel proprio pacchetto tutte le classi ActionScript mappate a tipi di dati AEM Forms complessi. Creare una cartella nella cartella src del progetto Flex e inserire il file ActionScript nella cartella, come illustrato nella figura seguente.

![ui_iu_customeras](assets/iu_iu_customeras.png)

### Guida introduttiva: Richiamare il servizio personalizzato del cliente tramite la comunicazione remota {#quick-start-invoking-the-customer-custom-service-using-remoting}

Esempio Nell&#39;esempio di codice riportato di seguito viene richiamato il Servizio clienti e viene creato un cliente. Quando si esegue questo esempio di codice, assicurarsi di compilare tutte le caselle di testo. Assicurarsi inoltre di creare il file Customer.as associato a `com.adobe.livecycle.sample.customer.Customer`.

>[!NOTE]
>
Prima di poter eseguire questo avvio rapido, è necessario creare e distribuire il componente personalizzato Banca.

```java
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Application  layout="absolute" backgroundColor="#B1ABAB">
 
 <mx:Script>
            <![CDATA[
 
      import flash.net.FileReference;
      import flash.net.URLRequest;
      import flash.events.Event;
      import flash.events.DataEvent;
      import mx.messaging.ChannelSet;
      import mx.messaging.channels.AMFChannel;
      import mx.rpc.events.ResultEvent;
      import mx.collections.ArrayCollection;
      import mx.rpc.AsyncToken;
      import mx.managers.CursorManager;
      import mx.rpc.remoting.mxml.RemoteObject;
 
 
      // Custom class that corresponds to an input to the
      // AEM Forms encryption method
      import customer.Customer;
 
      // Classes used in file retrieval
      private var fileRef:FileReference = new FileReference();
      private var parentResourcePath:String = "/";
      private var serverPort:String = "hiro-xp:8080";
      private var now1:Date;
      private var fileName:String;
 
      // Prepares parameters for encryptPDFUsingPassword method call
      public function executeCreateCustomer():void
      {
 
        var cs:ChannelSet= new ChannelSet();
     cs.addChannel(new AMFChannel("remoting-amf", "https://" + serverPort + "/remoting/messagebroker/amf"));
 
     customerService.setCredentials("administrator", "password");
     customerService.channelSet = cs;
 
     //Create a Customer object required to invoke the Customer service's
     //createCustomer operation
     var myCust:Customer = new Customer();
 
     //Get values from the user of the Flex application
     var fullName:String = txtFirst.text +" "+txtLast.text ;
     var Phone:String = txtPhone.text;
     var Street:String = txtStreet.text;
     var State:String = txtState.text;
     var Zip:int = parseInt(txtZIP.text);
     var City:String = txtCity.text;
 
     //Populate Customer fields
     myCust.name = fullName;
     myCust.phone = Phone;
     myCust.street= Street;
     myCust.state= State;
     myCust.zip = Zip;
     myCust.city = City;
 
     //Invoke the Customer service's createCustomer operation
     var params:Object = new Object();
        params["inCustomer"]=myCust;
     var token:AsyncToken;
        token = customerService.createCustomer(params);
        token.name = name;
      }
 
      private function handleResult(event:ResultEvent):void
      {
          // Retrieve the information returned from the service invocation
          var token:AsyncToken = event.token;
          var res:Object = event.result;
          var custId:String = res["CustomerId"] as String;
 
          //Assign to the custId to the text box
          txtCustId.text = custId;
      }
 
 
      private function resultHandler(event:ResultEvent):void
      {
 
      }
            ]]>
 </mx:Script>
 <mx:RemoteObject id="customerService" destination="CustomerService" result="resultHandler(event);">
 <mx:method name="createCustomer" result="handleResult(event)"/>
 </mx:RemoteObject>
 
 
 <mx:Style source="../bank.css"/>
     <mx:Grid>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="New Customer" fontSize="16" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="First Name:" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtFirst"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:Button label="Create Customer" id="btnCreateCustomer" click="executeCreateCustomer()"/>
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="Last Name" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtLast"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="Phone" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtPhone"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="Street" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtStreet"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="State" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtState"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="ZIP" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtZIP"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                     <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="City" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtCity"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                             <mx:GridRow width="100%" height="100%">
                         <mx:GridItem width="100%" height="100%">
                             <mx:Label text="Customer Identifier" fontSize="12" fontWeight="bold"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                             <mx:TextInput styleName="textField" id="txtCustId" editable="false"/>
                         </mx:GridItem>
                         <mx:GridItem width="100%" height="100%">
                         </mx:GridItem>
                     </mx:GridRow>
                 </mx:Grid>
 </mx:Application>
 
```

**Foglio di stile**

Questo avvio rapido contiene un foglio di stile denominato *bank.css*. Il codice seguente rappresenta il foglio di stile utilizzato.

```css
 /* CSS file */
 global
 {
          backgroundGradientAlphas: 1.0, 1.0;
          backgroundGradientColors: #525152,#525152;
          borderColor: #424444;
          verticalAlign: middle;
          color: #FFFFFF;
          font-size:12;
          font-weight:normal;
 }
 
 ApplicationControlBar
 {
          fillAlphas: 1.0, 1.0;
          fillColors: #393839, #393839;
 }
 
 .textField
 {
          backgroundColor: #393839;
          background-disabled-color: #636563;
 }
 
 
 .button
 {
          fillColors: #636563, #424242;
 }
 
 .dropdownMenu
 {
          backgroundColor: #DDDDDD;
          fillColors: #636563, #393839;
          alternatingItemColors: #888888, #999999;
 }
 
 .questionLabel
 {
 
 }
 
 ToolTip
 {
        backgroundColor: black;
        backgroundAlpha: 1.0;
        cornerRadius: 0;
        color: white;
 }
 
 DateChooser
 {
        cornerRadius: 0; /* pixels */
        headerColors: black, black;
        borderColor: black;
        themeColor: black;
        todayColor: red;
        todayStyleName: myTodayStyleName;
        headerStyleName: myHeaderStyleName;
        weekDayStyleName: myWeekDayStyleName;
        dropShadowEnabled: true;
 }
 
 .myTodayStyleName
 {
        color: white;
 }
 
 .myWeekDayStyleName
 {
        fontWeight: normal;
 }
 
 .myHeaderStyleName
 {
        color: red;
        fontSize: 16;
        fontWeight: bold;
 }
```

**Consulta anche**

[Richiamare AEM Forms tramite (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Gestione dei documenti con (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[Inclusione del file della libreria Flex di AEM Forms](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Richiamare un processo di breve durata passando un documento non sicuro utilizzando (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Autenticazione delle applicazioni client create con Flex](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[Passaggio di documenti protetti per richiamare i processi tramite la comunicazione remota](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)
