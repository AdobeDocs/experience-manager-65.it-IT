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
feature: Adaptive Forms,APIs & Integrations,AEM Forms on JEE
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2481'
ht-degree: 0%

---

# Richiamare AEM Forms tramite richieste REST {#invoking-aem-forms-using-rest-requests}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

I processi creati in Workbench possono essere configurati in modo da poterli richiamare tramite richieste REST (Managational State Transfer). Le richieste REST vengono inviate dalle pagine di HTML. In altre parole, è possibile richiamare un processo Forms direttamente da una pagina web utilizzando una richiesta REST. Ad esempio, puoi aprire una nuova istanza di una pagina web. È quindi possibile richiamare un processo Forms e caricare un documento PDF di cui è stato eseguito il rendering con i dati inviati in una richiesta HTTP POST.

Esistono due tipi di client HTML. Il primo client HTML è un client AJAX scritto in JavaScript. Il secondo client è un modulo HTML che contiene un pulsante di invio. Un&#39;applicazione client basata su HTML non è l&#39;unico client REST possibile. Qualsiasi applicazione client che supporta le richieste HTTP può richiamare un servizio utilizzando una chiamata REST. È ad esempio possibile richiamare un servizio utilizzando una chiamata REST da un modulo PDF. (Vedi [Richiamo del processo MyApplication/EncryptDocument da Acrobat](#rest-invocation-examples).)

Quando si utilizzano richieste REST, si consiglia di non richiamare direttamente i servizi Forms. Richiama invece i processi creati in Workbench. Quando crei un processo destinato alla chiamata REST, utilizza un punto iniziale programmatico. In questa situazione, l’endpoint REST viene aggiunto automaticamente. Per informazioni sulla creazione di processi in Workbench, vedere [Utilizzo di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

Quando si richiama un servizio utilizzando REST, viene richiesto di immettere un nome utente e una password per il modulo AEM. Tuttavia, se non si desidera specificare un nome utente e una password, è possibile disattivare la protezione del servizio.

Per richiamare un servizio Forms (un processo diventa servizio quando viene attivato) utilizzando REST, configura un endpoint REST. (Vedi &quot;Gestione degli endpoint&quot; nella [guida per l&#39;amministrazione](https://www.adobe.com/go/learn_aemforms_admin_63).)

Dopo aver configurato un endpoint REST, è possibile richiamare un servizio Forms utilizzando un metodo HTTP GET o POST.

```java
 action="https://hiro-xp:8080/rest/services/[ServiceName]/[OperationName]:[ServiceVersion]" method="post" enctype="multipart/form-data"
```

Il valore obbligatorio `ServiceName` è il nome del servizio Forms da richiamare. Il valore facoltativo `OperationName` è il nome dell&#39;operazione del servizio. Se questo valore non viene specificato, il nome predefinito sarà `invoke`, ovvero il nome dell&#39;operazione che avvia il processo. Il valore facoltativo `ServiceVersion` è la versione codificata nel formato X.Y. Se questo valore non viene specificato, viene utilizzata la versione più recente. Il valore `enctype` può anche essere `application/x-www-form-urlencoded`.

## Tipi di dati supportati {#supported-data-types}

I seguenti tipi di dati sono supportati quando si richiamano i servizi AEM Forms utilizzando le richieste REST:

* Tipi di dati primitivi Java, ad esempio Stringhe e interi
* Tipo di dati `com.adobe.idp.Document`
* Tipi di dati XML come `org.w3c.Document` e `org.w3c.Element`
* Oggetti raccolta come `java.util.List` e `java.util.Map`

  Questi tipi di dati vengono comunemente accettati come valori di input per i processi creati in Workbench.

  Se viene richiamato un servizio Forms con il metodo HTTP POST, gli argomenti vengono passati nel corpo della richiesta HTTP. Se la firma del servizio AEM Forms contiene un parametro di input di tipo stringa, il corpo della richiesta può contenere il valore di testo del parametro di input. Se la firma del servizio definisce più parametri stringa, la richiesta può seguire la notazione HTTP `application/x-www-form-urlencoded` con i nomi dei parametri utilizzati come nomi dei campi del modulo.

  Se un servizio Forms restituisce un parametro di stringa, il risultato è una rappresentazione testuale del parametro di output. Se un servizio restituisce più parametri stringa, il risultato è un documento XML che codifica i parametri di output nel formato seguente:
  ` <result> <output-paramater1>output-parameter-value-as-string</output-paramater1> . . . <output-paramaterN>output-parameter-value-as-string</output-paramaterN> </result>`

  >[!NOTE]
  >
  >Il valore `output-paramater1` rappresenta il nome del parametro di output.

  Se un servizio Forms richiede un parametro `com.adobe.idp.Document`, il servizio può essere richiamato solo utilizzando il metodo HTTP POST. Se il servizio richiede un parametro `com.adobe.idp.Document`, il corpo della richiesta HTTP diventa il contenuto dell&#39;oggetto documento di input.

  Se un servizio AEM Forms richiede più parametri di input, il corpo della richiesta HTTP deve essere un messaggio MIME multiparte come definito dalla RFC 1867. (RFC 1867 è uno standard utilizzato dai browser web per caricare file sui siti web.) Ogni parametro di input deve essere inviato come parte separata del messaggio multipart e codificato nel formato `multipart/form-data`. Il nome di ogni parte deve corrispondere al nome del parametro.

  Gli elenchi e le mappe vengono utilizzati anche come valori di input per i processi di AEM Forms creati in Workbench. Di conseguenza, puoi utilizzare questi tipi di dati quando utilizzi una richiesta REST. Gli array Java non sono supportati perché non vengono utilizzati come valore di input in un processo AEM Forms.

  Se un parametro di input è un elenco, un client REST può inviarlo specificando il parametro più volte (una volta per ogni elemento dell’elenco). Ad esempio, se A è un elenco di documenti, l&#39;input deve essere un messaggio in più parti costituito da più parti denominate A. In questo caso, ogni parte denominata A diventa un elemento nell&#39;elenco di input. Se B è un elenco di stringhe, l&#39;input può essere un messaggio `application/x-www-form-urlencoded` costituito da più campi denominati B. In questo caso, ogni campo modulo denominato B diventa un elemento nell&#39;elenco di input.

  Se un parametro di input è una mappa e si tratta del parametro di input solo dei servizi, ogni parte/campo del messaggio di input diventa un record chiave/valore nella mappa. Il nome di ogni parte/campo diventa la chiave del record. Il contenuto di ogni parte/campo diventa il valore del record.

  Se una mappa di input non è il solo parametro di input dei servizi, ogni record chiave/valore che appartiene alla mappa può essere inviato utilizzando un parametro denominato come concatenazione del nome del parametro e della chiave del record. Ad esempio, è possibile inviare una mappa di input denominata `attributes` con un elenco delle coppie chiave/valori seguenti:

  `attributesColor=red`

  `attributesShape=box`

  `attributesWidth=5`

  Ciò si traduce in una mappa di tre record: `Color=red`, `Shape=box` e `Width=5`.

  I parametri di output dei tipi di elenco e mappa diventano parte del messaggio XML risultante. L&#39;elenco di output è rappresentato in XML come una serie di elementi XML con un elemento per ogni elemento dell&#39;elenco. A ogni elemento viene assegnato lo stesso nome del parametro dell’elenco di output. Il valore di ogni elemento XML è uno dei due elementi seguenti:

* Rappresentazione testuale dell&#39;elemento nell&#39;elenco (se l&#39;elenco è costituito da tipi di stringa)
* URL che punta al contenuto del documento (se l&#39;elenco è costituito da `com.adobe.idp.Document` oggetti)

  L&#39;esempio seguente è un messaggio XML restituito da un servizio con un singolo parametro di output denominato *list*, ovvero un elenco di numeri interi.
  ` <result>   <list>12345</list>   . . .   <list>67890</list>  </result>`Un parametro di mapping di output è rappresentato nel messaggio XML risultante come una serie di elementi XML con un elemento per ogni record del mapping. A ogni elemento viene assegnato lo stesso nome della chiave del record mappa. Il valore di ciascun elemento è una rappresentazione testuale del valore del record mappa (se la mappa è costituita da record con un valore stringa) o un URL che punta al contenuto del documento (se la mappa è costituita da record con il valore `com.adobe.idp.Document`). Di seguito è riportato un esempio di messaggio XML restituito da un servizio che dispone di un singolo parametro di output denominato `map`. Questo valore di parametro è una mappa costituita da record che associano lettere a oggetti `com.adobe.idp.Document`.
  ` <result>   http://localhost:8080/DocumentManager/docm123/4567   . . .   <Z>http://localhost:8080/DocumentManager/docm987/6543</Z>  </result>  `

## Chiamate asincrone {#asynchronous-invocations}

Alcuni servizi di AEM Forms, come i processi a lunga durata incentrati sull’uomo, richiedono molto tempo per essere completati. Questi servizi possono essere richiamati in modo asincrono senza blocchi. (Vedi [Richiamare Processi A Lunga Durata Incentrati Sull&#39;Uomo](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).)

È possibile richiamare un servizio AEM Forms in modo asincrono sostituendo `services` con `async_invoke` nell&#39;URL di chiamata, come illustrato nell&#39;esempio seguente.

```java
 http://localhost:8080/rest/async_invoke/SomeService. SomeOperation?integer_input_variable=123&string_input_variable=abc
```

Questo URL restituisce il valore dell’identificatore (in formato &quot;text/plain&quot;) del processo responsabile di questa chiamata.

È possibile recuperare lo stato della chiamata asincrona utilizzando un URL di chiamata con `services` sostituito da `async_status`. L&#39;URL deve contenere un parametro `job_id` che specifica il valore dell&#39;identificatore del processo associato a questa chiamata. Ad esempio:

```java
 http://localhost:8080/rest/async_status/SomeService.SomeOperation?job_id=2345353443366564
```

Questo URL restituisce un valore intero (in formato &quot;text/plain&quot;) che codifica lo stato del processo in base alle specifiche del Manager processo (ad esempio, 2 significa in esecuzione, 3 significa completato, 4 significa non riuscito e così via).

Se il processo è completato, l’URL restituisce lo stesso risultato di se il servizio è stato richiamato in modo sincrono.

Una volta completato il processo e recuperato il risultato, il processo può essere eliminato utilizzando un URL di chiamata con `services` sostituito con `async_dispose`. L&#39;URL deve inoltre contenere un parametro `job_id` che specifica il valore dell&#39;identificatore del processo. Ad esempio:

```java
 http://localhost:8080/rest/async_dispose/SomeService.SomeOperation?job_id=2345353443366564
```

Se il processo viene eliminato correttamente, questo URL restituisce un messaggio vuoto.

## Segnalazione di errori {#error-reporting}

Se non è possibile completare una richiesta di chiamata sincrona o asincrona a causa di un&#39;eccezione generata sul server, l&#39;eccezione viene segnalata come parte del messaggio di risposta HTTP. Se l&#39;URL di chiamata (o l&#39;URL `async_result` in caso di chiamata asincrona) non ha un suffisso .xml, il provider REST restituisce il codice HTTP `500 Internal Server Error` seguito da un messaggio di eccezione.

Se l&#39;URL di chiamata (o l&#39;URL `async_result` se è presente una chiamata asincrona) ha un suffisso .xml, il provider REST restituisce il codice HTTP `200 OK` seguito da un documento XML che descrive l&#39;eccezione nel formato seguente.

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

L&#39;elemento `DSCError` è facoltativo e presente solo se l&#39;eccezione è un&#39;istanza di `com.adobe.idp.dsc.DSCException`.

## Sicurezza e autenticazione {#security-and-authentication}

Per fornire chiamate REST con un trasporto sicuro, un amministratore dei moduli AEM può abilitare il protocollo HTTPS sul server applicazioni J2EE che ospita AEM Forms. Questa configurazione è specifica del server applicazioni J2EE e non fa parte della configurazione del server Forms.

>[!NOTE]
>
>In qualità di sviluppatore di Workbench che desidera esporre i processi tramite un endpoint REST, tieni presente il problema di vulnerabilità XSS. Le vulnerabilità XSS possono essere utilizzate per rubare o manipolare i cookie, modificare la presentazione dei contenuti e compromettere le informazioni riservate. Se si riscontra un problema di vulnerabilità XSS, si consiglia di estendere la logica di processo con le regole di convalida dei dati di input e output aggiuntive.

## Servizi AEM Forms che supportano la chiamata REST {#aem-forms-services-that-support-rest-invocation}

Sebbene sia consigliabile richiamare i processi creati utilizzando Workbench anziché direttamente i servizi, alcuni servizi di AEM Forms supportano la chiamata REST. Il motivo per cui si consiglia di richiamare direttamente un processo anziché un servizio è che è più efficiente richiamare un processo. Considera lo scenario seguente. Si supponga di voler creare un criterio da un client REST. In altre parole, si desidera che il client REST definisca valori quali il nome del criterio e il periodo di lease offline.

Per creare un criterio, è necessario definire tipi di dati complessi, ad esempio un oggetto `PolicyEntry`. Un oggetto `PolicyEntry` definisce attributi quali le autorizzazioni associate al criterio. (Vedi [Creazione di criteri](/help/forms/developing/protecting-documents-policies.md#creating-policies).)

Invece di inviare una richiesta REST per creare un criterio (che includerebbe la definizione di tipi di dati complessi come un oggetto `PolicyEntry`), creare un processo che crei un criterio utilizzando Workbench. Definisci il processo per accettare variabili di input primitive, ad esempio un valore stringa che definisce il nome del processo o un numero intero che definisce il periodo di lease offline.

In questo modo, non è necessario creare una richiesta di chiamata REST che includa i tipi di dati complessi richiesti dall&#39;operazione. Il processo definisce i tipi di dati complessi e tutte le operazioni eseguite dal client REST vengono richiamate e passate ai tipi di dati primitivi. Per informazioni sulla chiamata di un processo tramite REST, vedere [Richiamo del processo MyApplication/EncryptDocument tramite REST](#rest-invocation-examples).

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

Nell&#39;esempio di HTML seguente vengono passati due valori `Boolean` a un processo AEM Forms denominato `RestTest2`. Il nome del metodo di chiamata è `invoke` e la versione è 1.0. Si noti che viene utilizzato il metodo HTML Post.

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

**Trasmissione di valori di data a un processo**

Nell&#39;esempio di HTML seguente viene passato un valore di data a un processo AEM Forms denominato `SOAPEchoService`. Il nome del metodo di chiamata è `echoCalendar`. Si noti che viene utilizzato il metodo HTML `Post`.

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

Nell&#39;esempio di HTML seguente viene richiamato un processo AEM Forms denominato `MyApplication/EncryptDocument` che richiede un documento PDF. Per informazioni su questo processo, vedere [Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom).

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

Nell&#39;esempio di HTML seguente viene richiamato un processo AEM Forms denominato `RestTest3` che richiede un documento e due valori di testo. Si noti che viene utilizzato il metodo HTML Post.

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

**Trasferimento dei valori di enumerazione a un processo**

Nell&#39;esempio di HTML seguente viene richiamato un processo AEM Forms denominato `SOAPEchoService` che richiede un valore di enumerazione. Si noti che viene utilizzato il metodo HTML Post.

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

**Richiamo del processo MyApplication/EncryptDocument tramite REST**

È possibile richiamare un processo AEM Forms di breve durata denominato *MyApplication/EncryptDocument* utilizzando REST.

>[!NOTE]
>
>Questo processo non è basato su un processo AEM Forms esistente. Per seguire l&#39;esempio di codice, creare un processo denominato `MyApplication/EncryptDocument` utilizzando Workbench. (Vedi [Utilizzo di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Quando viene richiamato, il processo esegue le azioni seguenti:

1. Ottiene il documento PDF non protetto passato al processo. Questa azione è basata sull&#39;operazione `SetValue`. Il parametro di input per questo processo è una variabile di processo `document` denominata `inDoc`.
1. Crittografa il documento PDF con una password. Questa azione è basata sull&#39;operazione `PasswordEncryptPDF`. Il documento PDF crittografato con password è stato restituito in una variabile di processo denominata `outDoc`.

   Quando questo processo viene richiamato utilizzando una richiesta REST, il documento PDF crittografato viene visualizzato nel browser web. Prima di visualizzare il documento PDF, specificare la password (a meno che la protezione non sia disattivata). Il codice HTML seguente rappresenta una richiesta di chiamata REST al processo `MyApplication/EncryptDocument`.

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

**Richiamo del processo MyApplication/EncryptDocument da Acrobat** {#invoke-process-acrobat}

È possibile richiamare un processo Forms da Acrobat utilizzando una richiesta REST. È ad esempio possibile richiamare il processo *MyApplication/EncryptDocument*. Per richiamare un processo Forms da Acrobat, posiziona un pulsante di invio su un file XDP all’interno di Designer. (Vedi [Guida di Designer](https://www.adobe.com/go/learn_aemforms_designer_63).)

Specifica l&#39;URL per richiamare il processo nel campo *Invia all&#39;URL* del pulsante, come illustrato nella figura seguente.

L’URL completo per richiamare il processo è https://hiro-xp:8080/rest/services/MyApplication/EncryptDocument.

Se il processo richiede un documento PDF come valore di input, assicurarsi di inviare il modulo come PDF, come illustrato nella figura precedente. Inoltre, per richiamare correttamente un processo, il processo deve restituire un documento PDF. In caso contrario, Acrobat non può gestire il valore restituito e si verifica un errore. Non è necessario specificare il nome della variabile di processo di input. Ad esempio, il processo *MyApplication/EncryptDocument* ha una variabile di input denominata `inDoc`. Non è necessario specificare inDoc, purché il modulo venga inviato come PDF.

È inoltre possibile inviare i dati del modulo come XML a un processo di Forms. Per inviare i dati XML, verificare che l&#39;elenco a discesa `Submit As` specifichi XML. Poiché il valore restituito dalla procedura deve essere un documento PDF, il documento PDF viene visualizzato in Acrobat.
