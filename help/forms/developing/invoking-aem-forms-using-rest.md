---
title: Richiamare AEM Forms tramite richieste REST
description: Richiama i processi creati in Workbench utilizzando le richieste REST.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
role: Developer
exl-id: 991fbc56-f144-4ae6-b010-8d02f780d347
solution: Experience Manager, Experience Manager Forms
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '2481'
ht-degree: 0%

---

# Richiamare AEM Forms tramite richieste REST {#invoking-aem-forms-using-rest-requests}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

I processi creati in Workbench possono essere configurati in modo da poterli richiamare tramite richieste REST (Managational State Transfer). Le richieste REST vengono inviate dalle pagine di HTML. In altre parole, è possibile richiamare un processo Forms direttamente da una pagina web utilizzando una richiesta REST. Ad esempio, puoi aprire una nuova istanza di una pagina web. È quindi possibile richiamare un processo Forms e caricare un documento PDF di cui è stato eseguito il rendering con i dati inviati in una richiesta HTTP POST.

Esistono due tipi di client HTML. Il primo client HTML è un client AJAX scritto in JavaScript. Il secondo client è un modulo HTML che contiene un pulsante di invio. Un&#39;applicazione client basata su HTML non è l&#39;unico client REST possibile. Qualsiasi applicazione client che supporta le richieste HTTP può richiamare un servizio utilizzando una chiamata REST. È ad esempio possibile richiamare un servizio utilizzando una chiamata REST da un modulo PDF. (vedere [Richiamare il processo MyApplication/EncryptDocument da Acrobat](#rest-invocation-examples).)

Quando si utilizzano richieste REST, si consiglia di non richiamare direttamente i servizi Forms. Richiama invece i processi creati in Workbench. Quando crei un processo destinato alla chiamata REST, utilizza un punto iniziale programmatico. In questa situazione, l’endpoint REST viene aggiunto automaticamente. Per informazioni sulla creazione di processi in Workbench, vedi [Utilizzo di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

Quando si richiama un servizio utilizzando REST, viene richiesto di immettere un nome utente e una password per il modulo AEM. Tuttavia, se non si desidera specificare un nome utente e una password, è possibile disattivare la protezione del servizio.

Per richiamare un servizio Forms (un processo diventa servizio quando viene attivato) utilizzando REST, configura un endpoint REST. (Consulta &quot;Gestione degli endpoint&quot; in [aiuto per l&#39;amministrazione](https://www.adobe.com/go/learn_aemforms_admin_63).)

Dopo aver configurato un endpoint REST, è possibile richiamare un servizio Forms utilizzando un metodo HTTP GET o POST.

```java
 action="https://hiro-xp:8080/rest/services/[ServiceName]/[OperationName]:[ServiceVersion]" method="post" enctype="multipart/form-data"
```

L&#39;opzione obbligatoria `ServiceName` value è il nome del servizio Forms da richiamare. L&#39;opzione `OperationName` value è il nome dell’operazione del servizio. Se questo valore non viene specificato, il nome predefinito è `invoke`, nome dell&#39;operazione che avvia il processo. L&#39;opzione `ServiceVersion` value è la versione codificata nel formato X.Y. Se questo valore non viene specificato, viene utilizzata la versione più recente. Il `enctype` valore può essere `application/x-www-form-urlencoded`.

## Tipi di dati supportati {#supported-data-types}

I seguenti tipi di dati sono supportati quando si richiamano i servizi AEM Forms utilizzando le richieste REST:

* Tipi di dati primitivi Java, ad esempio Stringhe e interi
* `com.adobe.idp.Document` tipo di dati
* Tipi di dati XML come `org.w3c.Document` e `org.w3c.Element`
* Oggetti di raccolta come `java.util.List` e `java.util.Map`

  Questi tipi di dati vengono comunemente accettati come valori di input per i processi creati in Workbench.

  Se viene richiamato un servizio Forms con il metodo HTTP POST, gli argomenti vengono passati nel corpo della richiesta HTTP. Se la firma del servizio AEM Forms contiene un parametro di input di tipo stringa, il corpo della richiesta può contenere il valore di testo del parametro di input. Se la firma del servizio definisce più parametri di stringa, la richiesta può seguire i `application/x-www-form-urlencoded` notazione con i nomi del parametro utilizzati come nomi dei campi del modulo.

  Se un servizio Forms restituisce un parametro di stringa, il risultato è una rappresentazione testuale del parametro di output. Se un servizio restituisce più parametri stringa, il risultato è un documento XML che codifica i parametri di output nel formato seguente:
  ` <result> <output-paramater1>output-parameter-value-as-string</output-paramater1> . . . <output-paramaterN>output-parameter-value-as-string</output-paramaterN> </result>`

  >[!NOTE]
  >
  >Il `output-paramater1` value rappresenta il nome del parametro di output.

  Se un servizio Forms richiede un `com.adobe.idp.Document` , il servizio può essere richiamato solo utilizzando il metodo HTTP POST. Se il servizio ne richiede uno `com.adobe.idp.Document` , il corpo della richiesta HTTP diventa il contenuto dell&#39;oggetto Document di input.

  Se un servizio AEM Forms richiede più parametri di input, il corpo della richiesta HTTP deve essere un messaggio MIME multiparte come definito dalla RFC 1867. (RFC 1867 è uno standard utilizzato dai browser web per caricare file sui siti web.) Ogni parametro di input deve essere inviato come parte separata del messaggio multipart e codificato nel `multipart/form-data` formato. Il nome di ogni parte deve corrispondere al nome del parametro.

  Gli elenchi e le mappe vengono utilizzati anche come valori di input per i processi di AEM Forms creati in Workbench. Di conseguenza, puoi utilizzare questi tipi di dati quando utilizzi una richiesta REST. Gli array Java non sono supportati perché non vengono utilizzati come valore di input in un processo AEM Forms.

  Se un parametro di input è un elenco, un client REST può inviarlo specificando il parametro più volte (una volta per ogni elemento dell’elenco). Ad esempio, se A è un elenco di documenti, l&#39;input deve essere un messaggio in più parti costituito da più parti denominate A. In questo caso, ogni parte denominata A diventa un elemento nell&#39;elenco di input. Se B è un elenco di stringhe, l’input può essere un `application/x-www-form-urlencoded` messaggio costituito da più campi denominati B. In questo caso, ogni campo modulo denominato B diventa un elemento nell&#39;elenco di input.

  Se un parametro di input è una mappa e si tratta del parametro di input solo dei servizi, ogni parte/campo del messaggio di input diventa un record chiave/valore nella mappa. Il nome di ogni parte/campo diventa la chiave del record. Il contenuto di ogni parte/campo diventa il valore del record.

  Se una mappa di input non è il solo parametro di input dei servizi, ogni record chiave/valore che appartiene alla mappa può essere inviato utilizzando un parametro denominato come concatenazione del nome del parametro e della chiave del record. Ad esempio, una mappa di input denominata `attributes` può essere inviato con un elenco delle seguenti coppie chiave/valori:

  `attributesColor=red`

  `attributesShape=box`

  `attributesWidth=5`

  Questo si traduce in una mappa di tre record: `Color=red`, `Shape=box`, e `Width=5`.

  I parametri di output dei tipi di elenco e mappa diventano parte del messaggio XML risultante. L&#39;elenco di output è rappresentato in XML come una serie di elementi XML con un elemento per ogni elemento dell&#39;elenco. A ogni elemento viene assegnato lo stesso nome del parametro dell’elenco di output. Il valore di ogni elemento XML è uno dei due elementi seguenti:

* Rappresentazione testuale dell&#39;elemento nell&#39;elenco (se l&#39;elenco è costituito da tipi di stringa)
* Un URL che punta al contenuto del documento (se l’elenco è costituito da `com.adobe.idp.Document` oggetti)

  L&#39;esempio seguente è un messaggio XML restituito da un servizio che dispone di un singolo parametro di output denominato *list*, che è un elenco di interi.
  ` <result>   <list>12345</list>   . . .   <list>67890</list>  </result>`Un parametro di mappa di output è rappresentato nel messaggio XML risultante come una serie di elementi XML con un elemento per ogni record della mappa. A ogni elemento viene assegnato lo stesso nome della chiave del record mappa. Il valore di ciascun elemento è una rappresentazione testuale del valore del record mappa (se la mappa è costituita da record con un valore stringa) o un URL che punta al contenuto del documento (se la mappa è costituita da record con `com.adobe.idp.Document` valore). Di seguito è riportato un esempio di messaggio XML restituito da un servizio con un singolo parametro di output denominato `map`. Questo valore di parametro è una mappa costituita da record a cui vengono associate le lettere `com.adobe.idp.Document` oggetti.
  ` <result>   http://localhost:8080/DocumentManager/docm123/4567   . . .   <Z>http://localhost:8080/DocumentManager/docm987/6543</Z>  </result>  `

## Chiamate asincrone {#asynchronous-invocations}

Alcuni servizi di AEM Forms, come i processi a lunga durata incentrati sull’uomo, richiedono molto tempo per essere completati. Questi servizi possono essere richiamati in modo asincrono senza blocchi. (vedere [Richiamare processi a lunga durata incentrati sull&#39;uomo](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).)

Un servizio AEM Forms può essere richiamato in modo asincrono sostituendo `services` con `async_invoke` nell’URL di chiamata, come illustrato nell’esempio seguente.

```java
 http://localhost:8080/rest/async_invoke/SomeService. SomeOperation?integer_input_variable=123&string_input_variable=abc
```

Questo URL restituisce il valore dell’identificatore (in formato &quot;text/plain&quot;) del processo responsabile di questa chiamata.

Lo stato della chiamata asincrona può essere recuperato utilizzando un URL di chiamata con `services` sostituito con `async_status`. L’URL deve contenere `job_id` parametro che specifica il valore dell&#39;identificatore del processo associato a questa chiamata. Ad esempio:

```java
 http://localhost:8080/rest/async_status/SomeService.SomeOperation?job_id=2345353443366564
```

Questo URL restituisce un valore intero (in formato &quot;text/plain&quot;) che codifica lo stato del processo in base alle specifiche del Manager processo (ad esempio, 2 significa in esecuzione, 3 significa completato, 4 significa non riuscito e così via).

Se il processo è completato, l’URL restituisce lo stesso risultato di se il servizio è stato richiamato in modo sincrono.

Una volta completato il processo e recuperato il risultato, il processo può essere eliminato utilizzando un URL di chiamata con `services` viene sostituito con `async_dispose`. L’URL deve contenere anche `job_id` parametro che specifica il valore dell’identificatore del processo. Ad esempio:

```java
 http://localhost:8080/rest/async_dispose/SomeService.SomeOperation?job_id=2345353443366564
```

Se il processo viene eliminato correttamente, questo URL restituisce un messaggio vuoto.

## Segnalazione di errori {#error-reporting}

Se non è possibile completare una richiesta di chiamata sincrona o asincrona a causa di un&#39;eccezione generata sul server, l&#39;eccezione viene segnalata come parte del messaggio di risposta HTTP. Se l’URL di chiamata (o il `async_result` URL in caso di chiamata asincrona) non dispone di un suffisso .xml, il provider REST restituisce il codice HTTP `500 Internal Server Error` seguito da un messaggio di eccezione.

Se l’URL di chiamata (o il `async_result` URL in caso di chiamata asincrona) non dispone di un suffisso .xml, il provider REST restituisce il codice HTTP `200 OK`seguito da un documento XML che descrive l&#39;eccezione nel formato seguente.

```xml
 <exception>
       <exception_class_name>[
       <DSCError>
          <componentUID>component_UUD</componentUID>
         <errorCode>error_code</errorCode>
         <minorCode>minor_code</minorCode>
         <message>error_message</message>
       </DSCError>
 ]
       <message>exception_message</message>
     <stackTrace>exception_stack_trace</stackTrace>
       </exception_class_name>
     <exception>
       </exception>
 </exception>
```

Il `DSCError` è facoltativo e presente solo se l&#39;eccezione è un&#39;istanza di `com.adobe.idp.dsc.DSCException`.

## Sicurezza e autenticazione {#security-and-authentication}

Per fornire chiamate REST con un trasporto sicuro, un amministratore dei moduli AEM può abilitare il protocollo HTTPS sul server applicazioni J2EE che ospita AEM Forms. Questa configurazione è specifica del server applicazioni J2EE e non fa parte della configurazione del server Forms.

>[!NOTE]
>
>In qualità di sviluppatore di Workbench che desidera esporre i processi tramite un endpoint REST, tieni presente il problema di vulnerabilità XSS. Le vulnerabilità XSS possono essere utilizzate per rubare o manipolare i cookie, modificare la presentazione dei contenuti e compromettere le informazioni riservate. Se si riscontra un problema di vulnerabilità XSS, si consiglia di estendere la logica di processo con le regole di convalida dei dati di input e output aggiuntive.

## Servizi AEM Forms che supportano la chiamata REST {#aem-forms-services-that-support-rest-invocation}

Sebbene sia consigliabile richiamare i processi creati utilizzando Workbench anziché direttamente i servizi, alcuni servizi di AEM Forms supportano la chiamata REST. Il motivo per cui si consiglia di richiamare direttamente un processo anziché un servizio è che è più efficiente richiamare un processo. Considera lo scenario seguente. Si supponga di voler creare un criterio da un client REST. In altre parole, si desidera che il client REST definisca valori quali il nome del criterio e il periodo di lease offline.

Per creare una policy, è necessario definire tipi di dati complessi, ad esempio `PolicyEntry` oggetto. A `PolicyEntry` object definisce attributi quali le autorizzazioni associate al criterio. (vedere [Creazione di criteri](/help/forms/developing/protecting-documents-policies.md#creating-policies).)

Invece di inviare una richiesta REST per creare un criterio (che includerebbe la definizione di tipi di dati complessi come `PolicyEntry` ), crea un processo che crea una policy utilizzando Workbench. Definisci il processo per accettare variabili di input primitive, ad esempio un valore stringa che definisce il nome del processo o un numero intero che definisce il periodo di lease offline.

In questo modo, non è necessario creare una richiesta di chiamata REST che includa i tipi di dati complessi richiesti dall&#39;operazione. Il processo definisce i tipi di dati complessi e tutte le operazioni eseguite dal client REST vengono richiamate e passate ai tipi di dati primitivi. Per informazioni sulla chiamata di un processo tramite REST, vedere [Richiamare il processo MyApplication/EncryptDocument tramite REST](#rest-invocation-examples).

L’elenco seguente specifica i servizi AEM Forms che supportano la chiamata diretta REST.

* servizio Distiller
* servizio Rights Management
* Genera servizio PDF
* Genera servizio3dPDF
* Integrazione FormData

## Esempi di chiamata REST {#rest-invocation-examples}

Vengono forniti i seguenti esempi di chiamata REST:

* Trasmettere valori booleani a un processo AEM Forms
* Trasmettere i valori di data a un processo AEM Forms
* Trasmissione di documenti a un processo AEM Forms
* Trasmissione di valori di documento e testo a un processo AEM Forms
* Trasmissione di valori di enumerazione a un processo AEM Forms
* Richiamare il processo MyApplication/EncryptDocument tramite REST
* Richiamare il processo MyApplication/EncryptDocument da Acrobat

  Ogni esempio illustra come passare diversi tipi di dati a un processo AEM Forms

**Trasmissione di valori booleani a un processo**

Il seguente esempio di HTML passa due `Boolean` valori in un processo AEM Forms denominato `RestTest2`. Il nome del metodo di chiamata è `invoke` e la versione è 1.0. Si noti che viene utilizzato il metodo Post di HTML.

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/RestTest2/invoke/1.0" method="post">
 
 Boolean 1: <input type="text" name="inBooleanList" value="true">
 Boolean 2: <input type="text" name="inBooleanList" value="false">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**Trasmissione dei valori di data a un processo**

Nell&#39;esempio di HTML seguente viene passato un valore di data a un processo AEM Forms denominato `SOAPEchoService`. Il nome del metodo di chiamata è `echoCalendar`. Il HTML `Post` viene utilizzato il metodo.

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/SOAPEchoService/echoCalendar" method="post">
 
 Date: <input type="text" name="value-to-echo" value="2009-01-02T12:15:30Z">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**Trasmissione di documenti a un processo**

Nell&#39;esempio di HTML seguente viene richiamato un processo AEM Forms denominato `MyApplication/EncryptDocument` richiede un documento PDF. Per informazioni su questo processo, consulta [Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom).

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/MyApplication/EncryptDocument/invoke" method="post"
          enctype="multipart/form-data">
 
 File: <input type="file" name="value-to-echo">
 <input type="submit" value="Submit"/>
 
 </form>
 
 </body>
 </html>
```

**Trasmissione di valori di documento e testo a un processo**

Nell&#39;esempio di HTML seguente viene richiamato un processo AEM Forms denominato `RestTest3` che richiede un documento e due valori di testo. Si noti che viene utilizzato il metodo Post di HTML.

```html
 <html>
 <body>
 
 <form name="input" action="http://localhost:9080/rest/services/RestTest3" method="post"
          enctype="multipart/form-data">
 
 Doc: <input type="file" name="inDoc">
 String 1: <input type="text" name="inListOfStrings" value="hello">
 String 2: <input type="text" name="inListOfStrings" value="privet">
 <input type="submit" value="Submit"/>
 
 </form>
 
 </body>
 </html>
```

**Trasmissione dei valori di enumerazione a un processo**

Nell&#39;esempio di HTML seguente viene richiamato un processo AEM Forms denominato `SOAPEchoService` che richiede un valore di enumerazione. Si noti che viene utilizzato il metodo Post di HTML.

```html
 <html>
 <body>
 
 <form name="input" action="https://hiro-xp:8080/rest/services/SOAPEchoService/echoEnum" method="post">
 
 Color Enum Value: <input type="text" name="value-to-echo" value="green">
 <input type="submit" value="Submit">
 
 </form>
 
 </body>
 </html>
```

**Richiamare il processo MyApplication/EncryptDocument tramite REST**

È possibile richiamare un processo AEM Forms di breve durata denominato *MyApplication/EncryptDocument* utilizzando REST.

>[!NOTE]
>
>Questo processo non è basato su un processo AEM Forms esistente. Per seguire insieme all&#39;esempio di codice, creare un processo denominato `MyApplication/EncryptDocument` utilizzo di workbench. (vedere [Utilizzo di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Quando viene richiamato, il processo esegue le azioni seguenti:

1. Ottiene il documento PDF non protetto passato al processo. Questa azione si basa sulla `SetValue` operazione. Il parametro di input per questo processo è un `document` variabile di processo denominata `inDoc`.
1. Crittografa il documento PDF con una password. Questa azione si basa sulla `PasswordEncryptPDF` operazione. Il documento PDF crittografato con password viene restituito in una variabile di processo denominata `outDoc`.

   Quando questo processo viene richiamato utilizzando una richiesta REST, il documento PDF crittografato viene visualizzato nel browser web. Prima di visualizzare il documento PDF, specificare la password (a meno che la protezione non sia disattivata). Il seguente codice HTML rappresenta una richiesta di chiamata REST a `MyApplication/EncryptDocument` processo.

   ```html
    <html>
    <body>
    <form action="https://hiro-xp:8080/rest/services/MyApplication/EncryptDocument" method="post" enctype="multipart/form-data">
         <p>Chose a PDF file (.pdf) to send to the EncryptDocument process.</p>
         <p>file:
           <input type="file" name="inDoc" />
         </p>
         <p>
           <input type="submit"/>
         </p>
    </form>
    </body>
   ```

**Richiamare il processo MyApplication/EncryptDocument da Acrobat** {#invoke-process-acrobat}

È possibile richiamare un processo Forms da Acrobat utilizzando una richiesta REST. Ad esempio, puoi richiamare il *MyApplication/EncryptDocument* processo. Per richiamare un processo Forms da Acrobat, posiziona un pulsante di invio su un file XDP all’interno di Designer. (vedere [Guida di Designer](https://www.adobe.com/go/learn_aemforms_designer_63).)

Specifica l’URL da utilizzare per richiamare il processo nel file del pulsante *Invia a URL* come illustrato nella figura seguente.

L’URL completo per richiamare il processo è https://hiro-xp:8080/rest/services/MyApplication/EncryptDocument.

Se il processo richiede un documento PDF come valore di input, assicurarsi di inviare il modulo come PDF, come illustrato nella figura precedente. Inoltre, per richiamare correttamente un processo, il processo deve restituire un documento PDF. In caso contrario, Acrobat non può gestire il valore restituito e si verifica un errore. Non è necessario specificare il nome della variabile di processo di input. Ad esempio, il *MyApplication/EncryptDocument* il processo ha una variabile di input denominata `inDoc`. Non è necessario specificare inDoc, purché il modulo venga inviato come PDF.

È inoltre possibile inviare i dati del modulo come XML a un processo di Forms. Per inviare i dati XML, assicurarsi che `Submit As` a discesa specifica XML. Poiché il valore restituito dalla procedura deve essere un documento PDF, il documento PDF viene visualizzato in Acrobat.
