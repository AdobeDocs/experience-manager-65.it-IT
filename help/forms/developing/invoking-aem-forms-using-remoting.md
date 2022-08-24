---
title: Richiamo di AEM Forms tramite Remoting
seo-title: Invoking AEM Forms using Remoting
description: Utilizzare Remoting per richiamare un processo AEM Forms per richiamare i processi creati in Workbench. Puoi richiamare un processo AEM Forms da un’applicazione client creata con Flex.
seo-description: Use Remoting to invoke an AEM Forms process to invoke processes created in Workbench. You can invoke a AEM Forms process from a client application built with Flex.
uuid: 592d1519-c38b-4b33-8cf3-61e2bff81501
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 3d8bb2d3-b1f8-49e1-a529-b3e7a28da4bb
role: Developer
exl-id: 94a48776-f537-4b4e-8d71-51b08e463cba
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '4628'
ht-degree: 0%

---

# Richiamo di AEM Forms tramite Remoting {#invoking-aem-forms-using-remoting}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

I processi creati in Workbench possono essere richiamati utilizzando Remoting. In altre parole, puoi richiamare un processo AEM Forms da un’applicazione client creata con Flex. Questa funzione si basa sui servizi dati.

>[!NOTE]
>
>Quando si utilizza Remoting, si consiglia di richiamare i processi creati in Workbench anziché i servizi AEM Forms. Tuttavia, è possibile richiamare direttamente i servizi AEM Forms. (Consultare Crittografia dei documenti PDF tramite Remoting situato in AEM Forms Developer Center.)

>[!NOTE]
>
>Se un servizio AEM Forms non è configurato per consentire l’accesso anonimo, le richieste di un client Flex si traducono in una sfida per il browser web. L&#39;utente deve immettere il nome utente e le credenziali della password.

Il seguente processo AEM Forms di breve durata, denominato `MyApplication/EncryptDocument`, può essere richiamato utilizzando Remoting. (Per informazioni su questo processo, ad esempio sui valori di input e output, consulta [Esempio di processo a breve termine](/help/forms/developing/aem-forms-processes.md).)

![iu_iu_encryptdocumentprocess2](assets/iu_iu_encryptdocumentprocess2.png)

>[!NOTE]
>
>Per richiamare un processo AEM Forms utilizzando un&#39;applicazione Flex, assicurati che sia abilitato un endpoint remoto. Per impostazione predefinita, quando si distribuisce un processo viene attivato un endpoint remoto.

Quando si richiama questo processo, vengono eseguite le azioni seguenti:

1. Ottiene il documento PDF non protetto passato come valore di input. Questa azione si basa sul `SetValue` funzionamento. Il nome del parametro di input è `inDoc` e il relativo tipo di dati è `document`. (2) `document` il tipo di dati è un tipo di dati disponibile in Workbench.)
1. Cifra il documento PDF con una password. Questa azione si basa sul `PasswordEncryptPDF` funzionamento. Il nome del valore di output per questo processo è `outDoc` e rappresenta il documento PDF crittografato con password. Il tipo di dati di outDoc è `document`.
1. Salva il documento PDF crittografato con password come file PDF nel file system locale. Questa azione si basa sul `WriteDocument` funzionamento.

>[!NOTE]
>
>La `MyApplication/EncryptDocument` Il processo non è basato su un processo AEM Forms esistente. Per seguire gli esempi di codice, crea un processo denominato `MyApplication/EncryptDocument` utilizzo di Workbench.

>[!NOTE]
>
>Per informazioni sull&#39;utilizzo di Remoting per richiamare un processo longevo, vedere [Richiamo dei processi a lunga durata incentrati sull&#39;uomo](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

**Consulta anche**

[Inclusione del file della libreria AEM Forms Flex](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Gestione dei documenti tramite AEM Forms Remoting (obsoleto per i moduli AEM)](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[Richiamare un processo di breve durata passando un documento non sicuro utilizzando (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Autenticazione di applicazioni client integrate con Flex](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[Trasferimento di documenti protetti per richiamare i processi utilizzando Remoting](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

[Richiamo dei servizi dei componenti personalizzati tramite Remoting](invoking-aem-forms-using-remoting.md#invoking-custom-component-services-using-remoting)

[Creazione di un&#39;applicazione client creata con Flex che richiama un processo longevo incentrato sull&#39;uomo](/help/forms/developing/invoking-human-centric-long-lived.md#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process)

[Creazione di applicazioni di Flash Builder che eseguono l&#39;autenticazione SSO utilizzando i token HTTP](/help/forms/developing/creating-flash-builder-applications-perform.md#creating-flash-builder-applications-that-perform-sso-authentication-using-http-tokens)

Per informazioni su come visualizzare i dati del processo in un controllo grafico Flex, vedi [Visualizzazione dei dati del processo AEM Forms nei grafici Flex](https://www.adobe.com/devnet/livecycle/articles/populating_flexcontrols.html).

>[!NOTE]
>
>*Assicurati di posizionare il file crossdomain.xml nella posizione corretta. Ad esempio, supponendo di aver implementato AEM Forms su JBoss, posiziona questo file nel percorso seguente: &lt;install_directory>\Adobe_Experience_Manager_forms\jboss\server\lc_turnkey\deploy\jboss-web.deployer\ROOT.war.*

## Inclusione del file della libreria AEM Forms Flex {#including-the-aem-forms-flex-library-file}

Per richiamare programmaticamente i processi AEM Forms utilizzando Remoting, aggiungi il file adobe-remoting-provider.swc al percorso di classe del progetto Flex. Questo file SWC si trova nel seguente percorso:

* *&lt;install_directory>\Adobe_Experience_Manager_forms\sdk\misc\DataServices\Client-Libraries*

   dove &lt;*install_directory*> è la directory in cui è installato AEM Forms.

**Consulta anche**

[Richiamo di AEM Forms utilizzando (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Gestione dei documenti tramite AEM Forms Remoting (obsoleto per i moduli AEM)](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[Richiamare un processo di breve durata passando un documento non sicuro utilizzando (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Autenticazione di applicazioni client integrate con Flex](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

## Gestione dei documenti con la rimozione {#handling-documents-with-remoting}

Uno dei tipi Java non primitivi più importanti utilizzati in AEM Forms è il `com.adobe.idp.Document` classe. Un documento viene comunemente richiesto per richiamare un’operazione AEM Forms. Si tratta principalmente di un documento PDF, ma può contenere altri tipi di documenti, ad esempio SWF, HTML, XML o un file DOC. (Vedi [Trasmissione di dati ai servizi AEM Forms tramite l’API Java](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api).)

Un&#39;applicazione client creata con Flex non può richiedere direttamente un documento. Ad esempio, non puoi avviare Adobe Reader per richiedere un URL che produca un file PDF. Le richieste per tipi di documenti, ad esempio documenti PDF e Microsoft Word, restituiscono un risultato che è un URL. È responsabilità del cliente mostrare il contenuto dell’URL. Il servizio Gestione documenti consente di generare l’URL e le informazioni sul tipo di contenuto. Le richieste di documenti XML restituiscono il documento XML completo nel risultato.

### Passaggio di un documento come parametro di input {#passing-a-document-as-an-input-parameter}

Un&#39;applicazione client creata con Flex non può passare un documento direttamente a un processo AEM Forms. Al contrario, l&#39;applicazione client utilizza un&#39;istanza del `mx.rpc.livecycle.DocumentReference` Classe ActionScript per passare parametri di input a un&#39;operazione che prevede un `com.adobe.idp.Document` istanza. Un&#39;applicazione client Flex dispone di diverse opzioni per la configurazione di un `DocumentReference` oggetto:

* Quando il documento si trova sul server e la relativa posizione del file è nota, impostare la proprietà referenceType dell&#39;oggetto DocumentReference su REF_TYPE_FILE. Impostare la proprietà fileRef sulla posizione del file, come illustrato nell&#39;esempio seguente:

```java
 ... var docRef: DocumentReference = new DocumentReference(); 
 docRef.referenceType = DocumentReference.REF_TYPE_FILE; 
 docRef.fileRef = "C:/install/adobe/cs2/How to Uninstall.pdf"; ...
```

* Quando il documento si trova sul server e si conosce il relativo URL, impostare la proprietà referenceType dell&#39;oggetto DocumentReference su REF_TYPE_URL. Imposta la proprietà url sull’URL, come illustrato nell’esempio seguente:

```java
... var docRef: DocumentReference = new DocumentReference(); 
docRef.referenceType = DocumentReference.REF_TYPE_URL; 
docRef.url = "https://companyserver:8080/DocumentManager/116/7855"; ...
```

* Per creare un oggetto DocumentReference da una stringa di testo nell&#39;applicazione client, impostare la proprietà referenceType dell&#39;oggetto DocumentReference su REF_TYPE_INLINE. Impostare la proprietà text sul testo da includere nell&#39;oggetto, come illustrato nell&#39;esempio seguente:

```java
... var docRef: DocumentReference = new DocumentReference(); 
docRef.referenceType = DocumentReference.REF_TYPE_INLINE; 
docRef.text = "Text for my document";  // Optionally, you can override the server’s default character set  // if necessary:  // docRef.charsetName=CharacterSetName  ...
```

* Se il documento non è sul server, utilizza il servlet di caricamento Remoting per caricare un documento in AEM Forms. La novità di AEM Forms è la possibilità di caricare documenti protetti. Quando si carica un documento protetto, è necessario utilizzare un utente che ha *Utente applicazione di caricamento documenti* ruolo. Senza questo ruolo, l&#39;utente non può caricare un documento protetto. È consigliabile utilizzare il single sign on per caricare un documento protetto. (Vedi [Trasferimento di documenti protetti per richiamare i processi utilizzando Remoting](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting).)

>[!NOTE]
se AEM Forms è configurato per consentire il caricamento di documenti non sicuri, puoi utilizzare un utente che non ha il ruolo Utente applicazione di caricamento documenti per caricare un documento. Un utente può anche disporre dell’autorizzazione per il caricamento dei documenti. Tuttavia, se AEM Forms è configurato per consentire solo documenti protetti, assicurati che l’utente disponga del ruolo Utente applicazione di caricamento documenti o dell’autorizzazione Caricamento documenti. (Vedi [Configurazione di AEM Forms per accettare documenti sicuri e non protetti](invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents).

Utilizza le funzionalità di caricamento di Flash standard per l’URL di caricamento designato: `https://SERVER:PORT/remoting/lcfileupload`. È quindi possibile utilizzare la `DocumentReference` ovunque un parametro di input di tipo `Document` previsto
` private function startUpload():void  {  fileRef.addEventListener(Event.SELECT, selectHandler);  fileRef.addEventListener("uploadCompleteData", completeHandler);  try  {   var success:Boolean = fileRef.browse();  }    catch (error:Error)  {   trace("Unable to browse for files.");  }  }      private function selectHandler(event:Event):void {  var request:URLRequest = new  URLRequest("https://SERVER:PORT/remoting/lcfileupload")  try   {   fileRef.upload(request);   }    catch (error:Error)   {   trace("Unable to upload file.");   }  }    private function completeHandler(event:DataEvent):void  {   var params:Object = new Object();   var docRef:DocumentReference = new DocumentReference();   docRef.url = event.data as String;   docRef.referenceType = DocumentReference.REF_TYPE_URL;  }`Per passare un file PDF al servizio di caricamento Remoting, è necessario utilizzare il servlet di caricamento Remoting `MyApplication/EncryptDocument`processo. (Vedi [Richiamare un processo di breve durata passando un documento non sicuro utilizzando (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting).)

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

Per passare un file PDF al servizio di caricamento Remoting, è necessario utilizzare il servlet di caricamento Remoting `MyApplication/EncryptDocument`processo. (Vedi [Richiamare un processo di breve durata passando un documento non sicuro utilizzando (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting).)

### Restituzione di un documento a un&#39;applicazione client {#passing-a-document-back-to-a-client-application}

Un&#39;applicazione client riceve un oggetto di tipo `mx.rpc.livecycle.DocumentReference` per un&#39;operazione di servizio che restituisce un `com.adobe.idp.Document` istanza come parametro di output. Poiché un’applicazione client si occupa di oggetti ActionScript e non di Java, non è possibile restituire un oggetto Document basato su Java a un client Flex. Invece, il server genera un URL per il documento e lo trasmette nuovamente al client. La `DocumentReference` dell’oggetto `referenceType` specifica se il contenuto si trova nel `DocumentReference` o deve essere recuperato da un URL nel `DocumentReference.url` proprietà. La `DocumentReference.contentType` specifica il tipo di documento.

**Consulta anche**

[Richiamo di AEM Forms utilizzando (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Inclusione del file della libreria AEM Forms Flex](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Richiamare un processo di breve durata passando un documento non sicuro utilizzando (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Autenticazione di applicazioni client integrate con Flex](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[Trasferimento di documenti protetti per richiamare i processi utilizzando Remoting](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

## Richiamare un processo di breve durata passando un documento non sicuro utilizzando Remoting {#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting}

Per richiamare un processo AEM Forms da un&#39;applicazione creata con Flex, esegui le seguenti attività:

1. Crea un `mx:RemoteObject` istanza.
1. Crea un `ChannelSet` istanza.
1. Passa i valori di input richiesti.
1. Gestisci i valori restituiti.

>[!NOTE]
Questa sezione illustra come richiamare un processo AEM Forms e caricare un documento quando AEM Forms è configurato per caricare documenti non sicuri. Per informazioni su come richiamare i processi AEM Forms e caricare documenti protetti e su come configurare AEM Forms per accettare documenti protetti e non protetti, consulta [Trasferimento di documenti protetti per richiamare i processi utilizzando Remoting](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting).

**Creazione di un&#39;istanza mx:RemoteObject**

Crea un `mx:RemoteObject` istanza per richiamare un processo AEM Forms creato in Workbench. Per creare una `mx:RemoteObject` , specifica i seguenti valori:

* **id:** Nome della `mx:RemoteObject` istanza che rappresenta il processo da richiamare.
* **destinazione:** Nome del processo AEM Forms da richiamare. Ad esempio, per richiamare `MyApplication/EncryptDocument` processo, specificare `MyApplication/EncryptDocument`.
* **risultato:** Nome del metodo Flex che gestisce il risultato.

All&#39;interno di `mx:RemoteObject` , specifica un `<mx:method>` che specifica il nome del metodo di chiamata del processo. In genere, il nome di un metodo di chiamata Forms è `invoke`.

Nell&#39;esempio di codice seguente viene creato un `mx:RemoteObject` istanza che richiama il `MyApplication/EncryptDocument` processo.

```java
 <mx:RemoteObject id="EncryptDocument" destination="MyApplication/EncryptDocument" result="resultHandler(event);">
          <mx:method name="invoke" result="handleExecuteInvoke(event)"/>
      </mx:RemoteObject>
```

**Creare un canale su AEM Forms**

Un’applicazione client può richiamare AEM Forms specificando un canale in MXML o ActionScript, come illustrato nell’esempio di ActionScript seguente. Il canale deve essere un `AMFChannel`, `SecureAMFChannel`, `HTTPChannel`oppure `SecureHTTPChannel`.

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

Assegna `ChannelSet` l&#39;istanza `mx:RemoteObject` dell’istanza `channelSet` (come mostrato nell’esempio di codice precedente). In genere, si importa la classe di canale in un&#39;istruzione di importazione anziché specificare il nome completo quando si richiama il `ChannelSet.addChannel` metodo .

**Trasferimento dei valori di ingresso**

Un processo creato in Workbench può richiedere zero o più parametri di input e restituire un valore di output. Un&#39;applicazione client trasmette i parametri di input all&#39;interno di un `ActionScript` oggetto con campi corrispondenti a parametri appartenenti al processo AEM Forms. Il processo di breve durata, denominato `MyApplication/EncryptDocument`, richiede un parametro di input denominato `inDoc`. Il nome dell&#39;operazione esposta dal processo è `invoke` (nome predefinito per un processo di breve durata). (Vedi [Richiamo di AEM Forms utilizzando (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

Nell’esempio di codice seguente viene passato un documento PDF al `MyApplication/EncryptDocument` processo:

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

In questo esempio di codice, `pdfDocument` è un `DocumentReference` istanza che contiene un documento PDF non protetto. Per informazioni su un `DocumentReference`, vedi [Gestione dei documenti tramite AEM Forms Remoting (obsoleto per i moduli AEM)](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting).

**Richiamo di una versione specifica di un servizio**

È possibile richiamare una versione specifica di un servizio Forms utilizzando un `_version` nella mappa dei parametri della chiamata. Ad esempio, per richiamare la versione 1.2 del `MyApplication/EncryptDocument` servizio:

```java
 var params:Object = new Object();
 params["inDoc"] = pdfDocument;
 params["_version"] = "1.2"
 var token:AsyncToken = echoService.echoString(params);
```

La `version` Il parametro deve essere una stringa contenente un singolo punto. I valori a sinistra, versione principale e a destra, versione secondaria del periodo devono essere numeri interi. Se questo parametro non viene specificato, viene richiamata la versione attiva dell&#39;intestazione.

**Gestione dei valori restituiti**

I parametri di output del processo AEM Forms vengono deserializzati in oggetti ActionScript da cui l’applicazione client estrae parametri specifici per nome, come illustrato nell’esempio seguente. (Il valore di output del `MyApplication/EncryptDocument` processo denominato `outDoc`.)

```java
     ...
     var res:Object = event.result;
     var docRef:DocumentReference = res["outDoc"] as DocumentReference;
     ...
```

**Richiamo del processo MyApplication/EncryptDocument**

È possibile richiamare `MyApplication/EncryptDocument` esegui le seguenti operazioni:

1. Crea un `mx:RemoteObject` tramite ActionScript o MXML. Consulta Creazione di un&#39;istanza mx:RemoteObject .
1. Imposta un `ChannelSet` istanza per comunicare con AEM Forms e associarla al `mx:RemoteObject` istanza. Consulta Creare un canale su AEM Forms .
1. Chiamare il `login` metodo o del servizio `setCredentials` per specificare il valore dell&#39;identificatore utente e la password. (Vedi [Utilizzo del single sign-on](invoking-aem-forms-using-remoting.md#using-single-sign-on).)
1. Popolare un `mx.rpc.livecycle.DocumentReference` istanza con un documento PDF non protetto da passare a `MyApplication/EncryptDocument` processo. (Vedi [Passaggio di un documento come parametro di input](invoking-aem-forms-using-remoting.md#passing-a-document-as-an-input-parameter).)
1. Cifrare il documento PDF chiamando il `mx:RemoteObject` dell’istanza `invoke` metodo . Passa la `Object` che contiene il parametro di input (che è il documento PDF non protetto). Vedere Trasmissione dei valori di input.
1. Recupera il documento PDF crittografato con password restituito dal processo. Consulta Gestione dei valori restituiti.

[Avvio rapido: Richiamare un processo di breve durata passando un documento non sicuro utilizzando (obsoleto per i moduli AEM) AEM Forms Remoting](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-by-passing-an-unsecure-document-using-deprecated-for-aem-forms-aem-forms-remoting)

## Autenticazione di applicazioni client integrate con Flex {#authenticating-client-applications-built-with-flex}

Sono disponibili diversi modi per AEM Forms User Manager per l’autenticazione di una richiesta Remoting da un’applicazione Flex, tra cui il single sign-on AEM Forms tramite il servizio di accesso centrale, l’autenticazione di base e l’autenticazione personalizzata. Se non è abilitato né l&#39;accesso single sign-on né l&#39;accesso anonimo, una richiesta Remoting restituisce l&#39;autenticazione di base (impostazione predefinita) o l&#39;autenticazione personalizzata.

L’autenticazione di base si basa sull’autenticazione di base J2EE standard dal contenitore dell’applicazione web. Per l’autenticazione di base, un errore HTTP 401 causa una sfida del browser. Ciò significa che quando si tenta di connettersi a un&#39;applicazione Forms utilizzando RemoteObject e non si è ancora effettuato l&#39;accesso dall&#39;applicazione Flex, il browser richiede un nome utente e una password.

Per l&#39;autenticazione personalizzata, il server invia un errore al client per indicare che l&#39;autenticazione è necessaria.

>[!NOTE]
Per informazioni sull’esecuzione dell’autenticazione tramite token HTTP, vedi [Creazione di applicazioni di Flash Builder che eseguono l&#39;autenticazione SSO utilizzando i token HTTP](/help/forms/developing/creating-flash-builder-applications-perform.md#creating-flash-builder-applications-that-perform-sso-authentication-using-http-tokens).

### Utilizzo dell’autenticazione personalizzata {#using-custom-authentication}

Per abilitare l’autenticazione personalizzata nella console di amministrazione, cambia il metodo di autenticazione da Base a Personalizzato sull’endpoint remoto. Se utilizzi l’autenticazione personalizzata, l’applicazione client chiama il `ChannelSet.login` metodo di accesso e `ChannelSet.logout` metodo di disconnessione.

>[!NOTE]
Nella versione precedente di AEM Forms, hai inviato le credenziali a una destinazione chiamando il `RemoteObject.setCredentials` metodo . La `setCredentials` non ha passato effettivamente le credenziali al server fino al primo tentativo del componente di connettersi al server. Pertanto, se il componente ha emesso un evento di errore, non è possibile essere certi se l&#39;errore si è verificato a causa di un errore di autenticazione o per un altro motivo. La `ChannelSet.login` il metodo si connette al server quando lo si chiama in modo da poter gestire immediatamente un problema di autenticazione. Anche se puoi continuare a utilizzare il `setCredentials` è consigliabile utilizzare il metodo `ChannelSet.login` metodo .

Poiché più destinazioni possono utilizzare gli stessi canali e l&#39;oggetto ChannelSet corrispondente, l&#39;accesso a una destinazione consente all&#39;utente di accedere a qualsiasi altra destinazione che utilizzi lo stesso canale o gli stessi canali. Se due componenti applicano credenziali diverse allo stesso oggetto ChannelSet, vengono utilizzate le ultime credenziali applicate. Se più componenti utilizzano lo stesso oggetto ChannelSet autenticato, la chiamata al `logout` registra tutti i componenti fuori dalle destinazioni.

Nell&#39;esempio seguente viene utilizzato il `ChannelSet.login` e `ChannelSet.logout` metodi con un controllo RemoteObject. Questa applicazione esegue le azioni seguenti:

* Crea un `ChannelSet` nell&#39;oggetto `creationComplete` che rappresenta i canali utilizzati dal `RemoteObject` component
* Trasmette le credenziali al server chiamando il `ROLogin` in risposta a un evento clic pulsante
* Utilizza il componente RemoteObject per inviare una stringa al server in risposta a un evento di clic Button. Il server restituisce lo stesso valore String al componente RemoteObject
* Utilizza l&#39;evento risultato del componente RemoteObject per visualizzare la stringa in un controllo TextArea
* Si disconnette dal server chiamando il `ROLogout` in risposta a un evento clic pulsante

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

La `login` e `logout` restituiscono un oggetto AsyncToken. Assegna i gestori eventi all&#39;oggetto AsyncToken affinché l&#39;evento risultato possa gestire una chiamata riuscita e che l&#39;evento di errore possa gestire un errore.

### Utilizzo del single sign-on {#using-single-sign-on}

AEM gli utenti dei moduli possono connettersi a più applicazioni Web AEM Forms per eseguire un’attività. Poiché gli utenti passano da un&#39;applicazione Web all&#39;altra, non è efficiente richiedere loro di accedere separatamente a ogni applicazione web. Il meccanismo di single sign-on AEM Forms consente agli utenti di accedere una volta e quindi di accedere a qualsiasi applicazione web AEM Forms. Poiché gli sviluppatori AEM Forms possono creare applicazioni client da utilizzare con AEM Forms, devono anche poter sfruttare il meccanismo di single sign-on.

Ogni applicazione web AEM Forms viene assemblata nel proprio file WAR (Web Archive), che viene quindi compilato come parte di un file Enterprise Archive (EAR). Poiché un server applicazioni non consente la condivisione di dati di sessione tra diverse applicazioni web, AEM Forms utilizza cookie HTTP per memorizzare le informazioni di autenticazione. I cookie di autenticazione consentono a un utente di accedere a un&#39;applicazione Forms e quindi di connettersi ad altre applicazioni web AEM Forms. Questa tecnica è nota come single sign-on.

Gli sviluppatori AEM Forms scrivono applicazioni client per estendere le funzionalità delle guide dei moduli (obsolete) e personalizzare Workspace. Ad esempio, un’applicazione Workspace può avviare un processo. L&#39;applicazione client utilizza quindi un endpoint remoto per recuperare i dati dal servizio Forms.

Quando un servizio AEM Forms viene richiamato utilizzando (obsoleto per AEM moduli) AEM Forms Remoting, l’applicazione client trasmette il cookie di autenticazione come parte della richiesta. Poiché l’utente ha già eseguito l’autenticazione, non è necessario alcun accesso aggiuntivo per effettuare una connessione dall’applicazione client al servizio AEM Forms.

>[!NOTE]
Se un cookie non è valido o manca, non esiste un reindirizzamento implicito a una pagina di accesso. Pertanto, puoi ancora chiamare un servizio anonimo.

È possibile bypassare il meccanismo di single sign-on di AEM Forms scrivendo un&#39;applicazione client che esegue l&#39;accesso e la disconnessione da sola. Se si bypassa il meccanismo di single sign-on, è possibile utilizzare l&#39;autenticazione di base o personalizzata con l&#39;applicazione.

Poiché questo meccanismo non utilizza il meccanismo di single sign-on di AEM Forms, nessun cookie di autenticazione viene scritto sul client. Le credenziali di accesso sono memorizzate in `ChannelSet` oggetto per il canale remoto. Di conseguenza, `RemoteObject` effettua le stesse chiamate `ChannelSet` nel contesto di tali credenziali.

### Configurazione del single sign-on in AEM Forms {#setting-up-single-sign-on-in-aem-forms}

Per utilizzare il single sign-on in AEM Forms, installa il componente del flusso di lavoro dei moduli, che include il servizio di accesso centralizzato. Dopo che un utente ha eseguito correttamente l&#39;accesso, il servizio di accesso centralizzato restituisce un cookie di autenticazione all&#39;utente. Ogni richiesta successiva a un&#39;applicazione web Forms contiene il cookie . Se il cookie è valido, l&#39;utente viene considerato autenticato e non deve effettuare di nuovo l&#39;accesso.

### Scrittura di un&#39;applicazione client che utilizza il single sign-on {#writing-a-client-application-that-uses-single-sign-on}

Quando si utilizza il meccanismo di accesso singolo, gli utenti dovranno effettuare l&#39;accesso utilizzando il servizio di accesso centralizzato prima di avviare un&#39;applicazione client. In altre parole, un&#39;applicazione client non effettua l&#39;accesso tramite il browser o chiamando il `ChannelSet.login` metodo .

Se utilizzi il meccanismo di single sign-on di AEM Forms, configura l&#39;endpoint Remoting per l&#39;utilizzo dell&#39;autenticazione personalizzata, non di base. In caso contrario, quando si utilizza l&#39;autenticazione di base, un errore di autenticazione causa una sfida del browser, che non si desidera che l&#39;utente veda. Al contrario, l&#39;applicazione rileva l&#39;errore di autenticazione e visualizza un messaggio che indica all&#39;utente di effettuare l&#39;accesso utilizzando il servizio di accesso centralizzato.

Un&#39;applicazione client accede ad AEM Forms tramite un endpoint remoto utilizzando `RemoteObject` , come illustrato nell’esempio seguente.

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

Un’applicazione creata con Flex include il cookie di autenticazione a ogni richiesta a un servizio AEM Forms. Per motivi di prestazioni, AEM Forms non convalida il cookie su ogni richiesta. Tuttavia, AEM Forms rileva quando un cookie di autenticazione viene sostituito da un altro cookie di autenticazione.

Ad esempio, si avvia un&#39;applicazione client e, mentre l&#39;applicazione è attiva, si utilizza il servizio di accesso centralizzato per disconnettersi. Successivamente, puoi accedere come un altro utente. L’accesso come utente diverso sostituisce il cookie di autenticazione esistente con un cookie di autenticazione per il nuovo utente.

Nella richiesta successiva dell’applicazione client, AEM Forms rileva che il cookie è stato modificato e disconnette l’utente. Pertanto, la prima richiesta dopo una modifica del cookie non riesce. Tutte le richieste successive vengono effettuate nel contesto del nuovo cookie e hanno esito positivo.

**Disconnessione**

Per uscire da AEM Forms e annullare la validità di una sessione, il cookie di autenticazione deve essere eliminato dal computer del client. Poiché lo scopo del single sign-on è quello di consentire a un utente di effettuare l&#39;accesso una volta, non si desidera che un&#39;applicazione client elimini il cookie. Questa azione disconnette efficacemente l’utente.

Pertanto, la `RemoteObject.logout` in un&#39;applicazione client genera un messaggio di errore sul client specificando che la sessione non è disconnessa. Al contrario, l’utente può utilizzare il servizio di accesso centralizzato per disconnettersi ed eliminare il cookie di autenticazione.

**Disconnessione mentre l&#39;applicazione Flex è ancora in esecuzione**

Puoi avviare un&#39;applicazione client creata con Flex e utilizzare il servizio di accesso centralizzato per disconnettersi. Come parte del processo di logout, il cookie di autenticazione viene eliminato. Se una richiesta remota viene effettuata senza un cookie o con un cookie non valido, la sessione utente viene invalidata. Questa azione è in effetti un logout. Al successivo tentativo di connessione dell’applicazione client a un servizio AEM Forms, l’utente viene invitato ad effettuare l’accesso.

**Consulta anche**

[Richiamo di AEM Forms utilizzando (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Gestione dei documenti tramite AEM Forms Remoting (obsoleto per i moduli AEM)](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[Inclusione del file della libreria AEM Forms Flex](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Richiamare un processo di breve durata passando un documento non sicuro utilizzando (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Trasferimento di documenti protetti per richiamare i processi utilizzando Remoting](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)

## Trasferimento di documenti protetti per richiamare i processi utilizzando Remoting {#passing-secure-documents-to-invoke-processes-using-remoting}

È possibile passare documenti protetti ad AEM Forms quando si richiama un processo che richiede uno o più documenti. Approvando un documento sicuro, proteggi le informazioni commerciali e i documenti confidenziali. In questa situazione, un documento può fare riferimento a un documento PDF, a un documento XML, a un documento Word e così via. Quando AEM Forms è configurato per consentire documenti sicuri, è necessario passare un documento protetto ad AEM Forms da un’applicazione client scritta in Flex. (Vedi [Configurazione di AEM Forms per accettare documenti sicuri e non protetti](invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents).)

Quando si passa un documento protetto, utilizzare il single sign-on e specificare un utente AEM forms con il tag *Utente applicazione di caricamento documenti* ruolo. Senza questo ruolo, l&#39;utente non può caricare un documento protetto. Puoi assegnare un ruolo a un utente a livello di programmazione. (Vedi [Gestione di ruoli e autorizzazioni](/help/forms/developing/users.md#managing-roles-and-permissions).)

>[!NOTE]
Quando crei un nuovo ruolo e desideri che i membri di tale ruolo caricino documenti protetti, assicurati di specificare l’autorizzazione per il caricamento dei documenti.

AEM Forms supporta un’operazione denominata `getFileUploadToken` che restituisce un token passato al servlet di caricamento. La `DocumentReference.constructRequestForUpload` richiede un URL ad AEM Forms insieme al token restituito da `LC.FileUploadAuthenticator.getFileUploadToken` metodo . Questo metodo restituisce un `URLRequest` oggetto utilizzato nella chiamata al servlet di caricamento. Il codice seguente illustra questa logica di applicazione.

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

### Configurazione di AEM Forms per accettare documenti sicuri e non protetti {#configuring-aem-forms-to-accept-secure-and-unsecure-documents}

È possibile utilizzare la console di amministrazione per specificare se i documenti sono protetti quando si passa un documento da un&#39;applicazione client Flex a un processo AEM Forms. Per impostazione predefinita, AEM Forms è configurato per accettare documenti protetti. Puoi configurare AEM Forms per accettare documenti protetti eseguendo le operazioni seguenti:

1. Accedi alla console di amministrazione.
1. Fai clic su **Impostazioni**.
1. Fai clic su **Impostazioni di sistema di base.**
1. Fai clic su Configurazioni.
1. Assicurati che l&#39;opzione Consenti caricamento di documenti non protetti da applicazioni Flex sia deselezionata.

>[!NOTE]
Per configurare AEM Forms per l’accettazione di documenti non sicuri, selezionare l’opzione Consenti caricamento di documenti non protetti dalle applicazioni Flex. Quindi riavvia un&#39;applicazione o un servizio per assicurarsi che l&#39;impostazione abbia effetto.

### Avvio rapido: Richiamare un processo di breve durata passando un documento sicuro utilizzando Remoting {#quick-start-invoking-a-short-lived-process-by-passing-a-secure-document-using-remoting}

L&#39;esempio di codice seguente richiama il `MyApplication/EncryptDocument.`Un utente deve effettuare l’accesso per fare clic sul pulsante Seleziona file utilizzato per caricare un file PDF e richiamare il processo. In altre parole, una volta che l’utente è autenticato, il pulsante Seleziona file è attivato. L&#39;illustrazione seguente mostra l&#39;applicazione client Flex dopo l&#39;autenticazione di un utente. Tenere presente che la casella di controllo Autenticata è abilitata.

![iu_iu_security_emoemoelogin](assets/iu_iu_secureremotelogin.png)

se AEM Forms è configurato per consentire solo il caricamento di documenti sicuri e l&#39;utente non ha *Utente applicazione di caricamento documenti* allora viene lanciata un&#39;eccezione. Se l’utente ha questo ruolo, il file viene caricato e il processo viene richiamato.

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
 
        // Set the docRef’s url and referenceType parameters
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

[Richiamo di AEM Forms utilizzando (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Gestione dei documenti tramite AEM Forms Remoting (obsoleto per i moduli AEM)](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[Inclusione del file della libreria AEM Forms Flex](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Richiamare un processo di breve durata passando un documento non sicuro utilizzando (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Autenticazione di applicazioni client integrate con Flex](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

## Richiamo dei servizi dei componenti personalizzati tramite Remoting {#invoking-custom-component-services-using-remoting}

È possibile richiamare servizi situati in un componente personalizzato utilizzando Remoting. Ad esempio, considera il componente Banca che contiene il servizio clienti. Puoi richiamare le operazioni che appartengono al servizio clienti utilizzando un&#39;applicazione client scritta in Flex. Prima di eseguire l’avvio rapido associato a questa sezione, è necessario creare il componente personalizzato Banca.

Il servizio clienti espone un&#39;operazione denominata `createCustomer`. Questa discussione descrive come creare un&#39;applicazione client Flex che richiama il servizio clienti e crea un cliente. Questa operazione richiede un oggetto complesso di tipo `com.adobe.livecycle.sample.customer.Customer` che rappresenta il nuovo cliente. L&#39;illustrazione seguente mostra l&#39;applicazione client che richiama il servizio clienti e crea un nuovo cliente. La `createCustomer` restituisce un valore di identificatore del cliente. Il valore dell’identificatore viene visualizzato nella casella di testo Identificatore cliente .

![iu_iu_flexnewcust](assets/iu_iu_flexnewcust.png)

Nella tabella seguente sono elencati i controlli che fanno parte di questa applicazione client.

<table>
 <thead>
  <tr>
   <th><p>Nome del controllo</p></th>
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
   <td><p>Specifica il nome della strada del cliente.</p></td>
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
   <td><p>Specifica il valore dell'identificatore del cliente a cui appartiene il nuovo account. Questa casella di testo è compilata dal valore restituito dal servizio del cliente <code>createCustomer</code> funzionamento. </p></td>
  </tr>
 </tbody>
</table>

### Mappatura di tipi di dati complessi AEM Forms {#mapping-aem-forms-complex-data-types}

Alcune operazioni di AEM Forms richiedono tipi di dati complessi come valori di input. Questi tipi di dati complessi definiscono i valori di runtime utilizzati dall’operazione. Ad esempio, il `createCustomer` l&#39;operazione richiede un `Customer` istanza che contiene i valori di runtime richiesti dal servizio. Senza il tipo complesso, il servizio Clienti genera un&#39;eccezione e non esegue l&#39;operazione.

Quando si richiama un servizio AEM Forms, creare oggetti ActionScript da associare ai tipi complessi AEM Forms richiesti. Per ogni tipo di dati complesso richiesto da un&#39;operazione, creare un oggetto ActionScript separato.

Nella classe ActionScript, utilizza il `RemoteClass` tag metadati da mappare al tipo complesso di AEM Forms. Ad esempio, quando si richiama il servizio del cliente `createCustomer` creare una classe ActionScript mappata su `com.adobe.livecycle.sample.customer.Customer` tipo di dati.

La seguente classe ActionScript denominata Customer illustra come eseguire il mapping al tipo di dati AEM Forms `com.adobe.livecycle.sample.customer.Customer`.

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

Il tipo di dati completo del tipo complesso di AEM Forms viene assegnato al tag alias.

I campi della classe ActionScript corrispondono ai campi che appartengono al tipo complesso di AEM Forms. I sei campi situati nella classe Customer ActionScript corrispondono ai campi che appartengono a `com.adobe.livecycle.sample.customer.Customer`.

>[!NOTE]
Per determinare i nomi di campo appartenenti a un tipo complesso di Forms, è consigliabile visualizzare il WSDL di un servizio in un browser Web. Una WSDL specifica i tipi complessi di un servizio e i relativi membri dati. Per il servizio clienti viene utilizzata la seguente WSDL: `https://[yourServer]:[yourPort]/soap/services/CustomerService?wsdl.`

La classe Customer ActionScript appartiene a un pacchetto denominato cliente. È consigliabile inserire nel proprio pacchetto tutte le classi ActionScript associate a tipi di dati AEM Forms complessi. Crea una cartella nella cartella src del progetto Flex e inserisci il file ActionScript nella cartella , come illustrato di seguito.

![iu_iu_customeras](assets/iu_iu_customeras.png)

### Avvio rapido: Richiamo del servizio personalizzato Cliente tramite Remoting {#quick-start-invoking-the-customer-custom-service-using-remoting}

Nell&#39;esempio di codice seguente viene richiamato il servizio clienti e viene creato un nuovo cliente. Quando esegui questo esempio di codice, assicurati di compilare tutte le caselle di testo. Inoltre, assicurati di creare il file Customer.as associato a `com.adobe.livecycle.sample.customer.Customer`.

>[!NOTE]
Prima di eseguire questo avvio rapido, è necessario creare e distribuire il componente personalizzato Banca.

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

[Richiamo di AEM Forms utilizzando (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Gestione dei documenti tramite AEM Forms Remoting (obsoleto per i moduli AEM)](invoking-aem-forms-using-remoting.md#handling-documents-with-remoting)

[Inclusione del file della libreria AEM Forms Flex](invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)

[Richiamare un processo di breve durata passando un documento non sicuro utilizzando (obsoleto per i moduli AEM) AEM Forms Remoting](invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting)

[Autenticazione di applicazioni client integrate con Flex](invoking-aem-forms-using-remoting.md#authenticating-client-applications-built-with-flex)

[Trasferimento di documenti protetti per richiamare i processi utilizzando Remoting](invoking-aem-forms-using-remoting.md#passing-secure-documents-to-invoke-processes-using-remoting)
