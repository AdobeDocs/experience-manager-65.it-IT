---
title: Richiamo di AEM Forms utilizzando le richieste REST
seo-title: Richiamo di AEM Forms utilizzando le richieste REST
description: Richiamare i processi creati in Workbench utilizzando le richieste REST.
seo-description: Richiamare i processi creati in Workbench utilizzando le richieste REST.
uuid: 3a19a296-f3fe-4e50-9143-b68aed37f9ef
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: df7b60bb-4897-479e-a05e-1b1e9429ed87
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2521'
ht-degree: 0%

---


# Richiamo di AEM Forms utilizzando le richieste REST {#invoking-aem-forms-using-rest-requests}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

I processi creati in Workbench possono essere configurati in modo da poterli richiamare tramite le richieste di trasferimento dello stato di rappresentanza (REST). Le richieste REST vengono inviate dalle pagine HTML. In altre parole, puoi richiamare un processo Forms direttamente da una pagina web utilizzando una richiesta REST. Ad esempio, puoi aprire una nuova istanza di una pagina web. È quindi possibile richiamare un processo Forms e caricare un documento PDF di cui è stato eseguito il rendering con i dati inviati in una richiesta HTTP POST.

Esistono due tipi di client HTML. Il primo client HTML è un client AJAX scritto in JavaScript. Il secondo client è un modulo HTML contenente un pulsante di invio. Un’applicazione client basata su HTML non è l’unico client REST possibile. Qualsiasi applicazione client che supporta le richieste HTTP può richiamare un servizio utilizzando una chiamata REST. Ad esempio, è possibile richiamare un servizio utilizzando una chiamata REST da un modulo PDF. (Vedere [Richiamo del processo MyApplication/EncryptDocument da Acrobat](#rest-invocation-examples).)

Quando utilizzi le richieste REST, ti consigliamo di non invocare direttamente i servizi Forms. Richiama invece i processi creati in Workbench. Quando crei un processo destinato alla chiamata REST, utilizza un punto iniziale programmatico. In questa situazione, l’endpoint REST viene aggiunto automaticamente. Per informazioni sulla creazione di processi in Workbench, vedere [Uso di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

Quando si richiama un servizio utilizzando REST, viene richiesto di specificare il nome utente e la password del modulo di AEM. Tuttavia, se non si desidera specificare un nome utente e una password, è possibile disabilitare la sicurezza del servizio.

Per richiamare un servizio Forms (un processo diventa un servizio quando il processo viene attivato) utilizzando REST, configura un endpoint REST. (Consultare &quot;Gestione degli endpoint&quot; nella [guida di amministrazione](https://www.adobe.com/go/learn_aemforms_admin_63).)

Dopo aver configurato un endpoint REST, è possibile richiamare un servizio Forms utilizzando un metodo HTTP GET o un metodo POST.

```java
 action="https://hiro-xp:8080/rest/services/[ServiceName]/[OperationName]:[ServiceVersion]" method="post" enctype="multipart/form-data"
```

Il valore obbligatorio `ServiceName` è il nome del servizio Forms da richiamare. Il valore facoltativo `OperationName` è il nome dell&#39;operazione del servizio. Se questo valore non viene specificato, il nome viene impostato automaticamente su `invoke`, che è il nome dell&#39;operazione che avvia il processo. Il valore facoltativo `ServiceVersion` è la versione codificata in formato X.Y. Se questo valore non viene specificato, viene utilizzata la versione più recente. Il valore `enctype` può anche essere `application/x-www-form-urlencoded`.

## Tipi di dati supportati {#supported-data-types}

I seguenti tipi di dati sono supportati quando si richiamano i servizi AEM Forms utilizzando le richieste REST:

* Tipi di dati primitivi Java, ad esempio stringhe e numeri interi
* `com.adobe.idp.Document` tipo di dati
* Tipi di dati XML quali `org.w3c.Document` e `org.w3c.Element`
* Oggetti di raccolta come `java.util.List` e `java.util.Map`

   Questi tipi di dati vengono comunemente accettati come valori di input per i processi creati in Workbench.

   Se si richiama un servizio Forms con il metodo HTTP POST, gli argomenti vengono trasmessi all’interno del corpo della richiesta HTTP. Se la firma del servizio AEM Forms dispone di un parametro di input della stringa, il corpo della richiesta può contenere il valore di testo del parametro di input. Se la firma del servizio definisce più parametri di stringa, la richiesta può seguire la notazione HTTP `application/x-www-form-urlencoded` con i nomi del parametro utilizzati come nomi di campo del modulo.

   Se un servizio Forms restituisce un parametro stringa, il risultato è una rappresentazione testuale del parametro di output. Se un servizio restituisce più parametri di stringa, il risultato è un documento XML che codifica i parametri di output nel formato seguente:
   ` <result> <output-paramater1>output-parameter-value-as-string</output-paramater1> . . . <output-paramaterN>output-parameter-value-as-string</output-paramaterN> </result>`

   >[!NOTE]
   >
   >Il valore `output-paramater1` rappresenta il nome del parametro di output.

   Se un servizio Forms richiede un parametro `com.adobe.idp.Document` , può essere richiamato solo utilizzando il metodo HTTP POST. Se il servizio richiede un parametro `com.adobe.idp.Document`, il corpo della richiesta HTTP diventa il contenuto dell&#39;oggetto Document di input.

   Se un servizio AEM Forms richiede più parametri di input, il corpo della richiesta HTTP deve essere un messaggio MIME multiparte come definito dalla RFC 1867. (RFC 1867 è uno standard utilizzato dai browser web per caricare i file sui siti web.) Ogni parametro di input deve essere inviato come parte separata del messaggio multiparte e codificato nel formato `multipart/form-data` . Il nome di ciascuna parte deve corrispondere al nome del parametro.

   Gli elenchi e le mappe vengono inoltre utilizzati come valori di input per i processi AEM Forms creati in Workbench. Di conseguenza, è possibile utilizzare questi tipi di dati quando si utilizza una richiesta REST. Gli array Java non sono supportati perché non vengono utilizzati come valore di input per un processo AEM Forms.

   Se un parametro di input è un elenco, un client REST può inviarlo specificando il parametro più volte (una volta per ogni elemento dell’elenco). Ad esempio, se A è un elenco di documenti, l&#39;input deve essere un messaggio multiparte costituito da più parti denominate A. In questo caso, ogni parte denominata A diventa un elemento dell&#39;elenco di input. Se B è un elenco di stringhe, l’input può essere un messaggio `application/x-www-form-urlencoded` composto da più campi denominati B. In questo caso, ogni campo modulo denominato B diventa una voce dell’elenco di input.

   Se un parametro di input è una mappa ed è l’unico parametro di input dei servizi, ogni parte/campo del messaggio di input diventa un record chiave/valore nella mappa. Il nome di ogni parte/campo diventa la chiave del record. Il contenuto di ogni parte/campo diventa il valore del record.

   Se una mappa di input non è l’unico parametro di input dei servizi, ogni record chiave/valore appartenente alla mappa può essere inviato utilizzando un parametro denominato come concatenazione del nome del parametro e della chiave del record. Ad esempio, una mappa di input denominata `attributes` può essere inviata con un elenco delle seguenti coppie chiave/valori:

   `attributesColor=red`

   `attributesShape=box`

   `attributesWidth=5`

   Questo si traduce in una mappa di tre record: `Color=red`, `Shape=box` e `Width=5`.

   I parametri di output dei tipi di elenco e mappa diventano parte del messaggio XML risultante. L&#39;elenco di output è rappresentato in XML come una serie di elementi XML con un elemento per ogni elemento dell&#39;elenco. A ogni elemento viene assegnato lo stesso nome del parametro dell’elenco di output. Il valore di ogni elemento XML è uno dei due elementi seguenti:

* Una rappresentazione testuale dell’elemento nell’elenco (se l’elenco è costituito da tipi di stringa)
* Un URL che punta al contenuto del documento (se l’elenco è costituito da `com.adobe.idp.Document` oggetti)

   L&#39;esempio seguente è un messaggio XML restituito da un servizio con un singolo parametro di output denominato *list*, che è un elenco di numeri interi.
   ` <result>   <list>12345</list>   . . .   <list>67890</list>  </result>`Un parametro di mappa di output è rappresentato nel messaggio XML risultante come una serie di elementi XML con un elemento per ogni record della mappa. A ogni elemento viene assegnato lo stesso nome della chiave del record mappa. Il valore di ciascun elemento è una rappresentazione testuale del valore del record della mappa (se la mappa è costituita da record con un valore stringa) o un URL che punta al contenuto del documento (se la mappa è costituita da record con il valore `com.adobe.idp.Document` ). Di seguito è riportato un esempio di messaggio XML restituito da un servizio con un singolo parametro di output denominato `map`. Questo valore del parametro è una mappa costituita da record che associano lettere agli oggetti `com.adobe.idp.Document`.
   ` <result>   http://localhost:8080/DocumentManager/docm123/4567   . . .   <Z>http://localhost:8080/DocumentManager/docm987/6543</Z>  </result>  `

## Chiamate asincrone {#asynchronous-invocations}

Alcuni servizi AEM Forms, come i processi a lunga vita incentrati sull’uomo, richiedono molto tempo per essere completati. Questi servizi possono essere richiamati in modo asincrono senza blocchi. (Vedere [Richiamo di processi a lunga durata incentrati sull&#39;uomo](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).)

Un servizio AEM Forms può essere richiamato in modo asincrono sostituendo `services` con `async_invoke` nell&#39;URL di chiamata, come illustrato nell&#39;esempio seguente.

```java
 http://localhost:8080/rest/async_invoke/SomeService. SomeOperation?integer_input_variable=123&string_input_variable=abc
```

Questo URL restituisce il valore dell&#39;identificatore (in formato &quot;text/plain&quot;) del processo responsabile di questa chiamata.

Lo stato della chiamata asincrona può essere recuperato utilizzando un URL di chiamata con `services` sostituito con `async_status`. L&#39;URL deve contenere un parametro `job_id` che specifica il valore dell&#39;identificatore del processo associato a questa chiamata. Esempio:

```java
 http://localhost:8080/rest/async_status/SomeService.SomeOperation?job_id=2345353443366564
```

Questo URL restituisce un valore intero (in formato &quot;text/plain&quot;) che codifica lo stato del processo in base alle specifiche del Job Manager (ad esempio, 2 significa in esecuzione, 3 significa completato, 4 significa non riuscito e così via).

Se il processo è completato, l’URL restituisce lo stesso risultato di come se il servizio fosse stato richiamato in modo sincrono.

Una volta completato il processo e recuperato il risultato, il processo può essere eliminato utilizzando un URL di chiamata con `services` viene sostituito con `async_dispose`. L’URL deve inoltre contenere un parametro `job_id` che specifica il valore dell’identificatore del processo. Esempio:

```java
 http://localhost:8080/rest/async_dispose/SomeService.SomeOperation?job_id=2345353443366564
```

Se il processo viene eliminato correttamente, questo URL restituisce un messaggio vuoto.

## Segnalazione errori {#error-reporting}

Se non è possibile completare una richiesta di chiamata sincrona o asincrona a causa di un&#39;eccezione lanciata sul server, l&#39;eccezione viene segnalata come parte del messaggio di risposta HTTP. Se l&#39;URL di chiamata (o l&#39; `async_result` URL nel caso di una chiamata asincrona) non ha un suffisso .xml, il provider REST restituisce il codice HTTP `500 Internal Server Error` seguito da un messaggio di eccezione.

Se l&#39;URL di chiamata (o l&#39; `async_result` URL nel caso di una chiamata asincrona) ha un suffisso .xml, il provider REST restituisce il codice HTTP `200 OK`seguito da un documento XML che descrive l&#39;eccezione nel seguente formato.

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

Per fornire chiamate REST con un trasporto sicuro, un amministratore di moduli AEM può abilitare il protocollo HTTPS sul server dell’applicazione J2EE che ospita AEM Forms. Questa configurazione è specifica per il server applicativo J2EE; non fa parte della configurazione del server dei moduli.

>[!NOTE]
>
>In qualità di sviluppatore di Workbench che desidera esporre i processi tramite un endpoint REST, ricorda il problema di vulnerabilità XSS. Le vulnerabilità XSS possono essere utilizzate per rubare o manipolare i cookie, modificare la presentazione dei contenuti e compromettere le informazioni confidenziali. Se la vulnerabilità XSS è un problema, è consigliabile estendere la logica del processo con le regole di convalida dei dati di input e output aggiuntive.

## Servizi AEM Forms che supportano la chiamata REST {#aem-forms-services-that-support-rest-invocation}

Sebbene sia consigliato richiamare direttamente i processi creati utilizzando Workbench anziché i servizi, alcuni servizi AEM Forms supportano la chiamata REST. Il motivo per cui si consiglia di richiamare direttamente un processo anziché un servizio è perché è più efficiente richiamare un processo. Considera lo scenario seguente. Supponi di voler creare un criterio da un client REST. In altre parole, desideri che il client REST definisca valori come il nome del criterio e il periodo di lease offline.

Per creare un criterio, è necessario definire tipi di dati complessi, ad esempio un oggetto `PolicyEntry`. Un oggetto `PolicyEntry` definisce attributi quali le autorizzazioni associate al criterio. (Consulta [Creazione di criteri](/help/forms/developing/protecting-documents-policies.md#creating-policies).)

Invece di inviare una richiesta REST per creare un criterio (che include la definizione di tipi di dati complessi come un oggetto `PolicyEntry` ), crea un processo che crea un criterio utilizzando Workbench. Definisci il processo per accettare variabili di input primitive, ad esempio un valore stringa che definisce il nome del processo o un numero intero che definisce il periodo di lease offline.

In questo modo, non è necessario creare una richiesta di chiamata REST che includa tipi di dati complessi richiesti dall’operazione. Il processo definisce i tipi di dati complessi e tutto ciò che si fa dal client REST è richiamare il processo e passare i tipi di dati primitivi. Per informazioni su come richiamare un processo utilizzando REST, vedere [Richiamare il processo MyApplication/EncryptDocument utilizzando REST](#rest-invocation-examples).

Gli elenchi seguenti specificano i servizi AEM Forms che supportano la chiamata REST diretta.

* Servizio Distiller
* servizio Rights Management
* Servizio GeneratePDF
* Servizio Generate3dPDF
* IntegrazioneDatiModulo

## Esempi di chiamata REST {#rest-invocation-examples}

Vengono forniti i seguenti esempi di chiamata REST:

* Trasferimento di valori booleani a un processo AEM Forms
* Trasmissione dei valori di data a un processo AEM Forms
* Trasmissione di documenti a un processo AEM Forms
* Trasferimento dei valori di documento e testo a un processo AEM Forms
* Trasferimento dei valori di enumerazione a un processo AEM Forms
* Richiamo del processo MyApplication/EncryptDocument tramite REST
* Richiamo del processo MyApplication/EncryptDocument da Acrobat

   Ogni esempio mostra come passare diversi tipi di dati a un processo AEM Forms

**Trasferimento di valori booleani a un processo**

L’esempio HTML seguente passa due valori `Boolean` a un processo AEM Forms denominato `RestTest2`. Il nome del metodo di chiamata è `invoke` e la versione è 1.0. Si noti che viene utilizzato il metodo HTML Post.

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

**Trasferimento dei valori di data a un processo**

Nell’esempio HTML seguente viene passato un valore di data a un processo AEM Forms denominato `SOAPEchoService`. Il nome del metodo di chiamata è `echoCalendar`. Si noti che viene utilizzato il metodo HTML `Post` .

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

**Trasferimento di documenti a un processo**

L’esempio HTML seguente richiama un processo AEM Forms denominato `MyApplication/EncryptDocument` che richiede un documento PDF. Per informazioni su questo processo, consulta [Richiamo di AEM Forms utilizzando MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom).

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

**Trasferimento dei valori di documento e testo a un processo**

L&#39;esempio HTML seguente richiama un processo AEM Forms denominato `RestTest3` che richiede un documento e due valori di testo. Si noti che viene utilizzato il metodo HTML Post.

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

L&#39;esempio HTML seguente richiama un processo AEM Forms denominato `SOAPEchoService` che richiede un valore di enumerazione. Si noti che viene utilizzato il metodo HTML Post.

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
>Questo processo non è basato su un processo AEM Forms esistente. Per seguire l’esempio di codice, crea un processo denominato `MyApplication/EncryptDocument` utilizzando workbench. (Vedere [Uso di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Quando si richiama questo processo, vengono eseguite le azioni seguenti:

1. Ottiene il documento PDF non protetto passato al processo. Questa azione è basata sull&#39;operazione `SetValue` . Il parametro di input per questo processo è una variabile di processo `document` denominata `inDoc`.
1. Cifra il documento PDF con una password. Questa azione è basata sull&#39;operazione `PasswordEncryptPDF` . Il documento PDF crittografato con password viene restituito in una variabile di processo denominata `outDoc`.

   Quando questo processo viene richiamato utilizzando una richiesta REST, il documento PDF crittografato viene visualizzato nel browser Web. Prima di visualizzare il documento PDF, specificare la password (a meno che la protezione non sia disabilitata). Il seguente codice HTML rappresenta una richiesta di chiamata REST al processo `MyApplication/EncryptDocument`.

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

Puoi richiamare un processo Forms da Acrobat utilizzando una richiesta REST. Ad esempio, è possibile richiamare il processo *MyApplication/EncryptDocument* . Per richiamare un processo Forms da Acrobat, posizionare un pulsante di invio su un file XDP all’interno di Designer. (Consultare [Guida di Designer](https://www.adobe.com/go/learn_aemforms_designer_63).)

Specifica l’URL per richiamare il processo all’interno del campo *Invia a URL* del pulsante, come illustrato nella figura seguente.

L’URL completo per richiamare il processo è https://hiro-xp:8080/rest/services/MyApplication/EncryptDocument.

Se il processo richiede un documento PDF come valore di input, assicurarsi di inviare il modulo come PDF, come illustrato nell’illustrazione precedente. Inoltre, per richiamare correttamente un processo, il processo deve restituire un documento PDF. In caso contrario, Acrobat non può gestire il valore restituito e si verifica un errore. Non è necessario specificare il nome della variabile del processo di input. Ad esempio, il processo *MyApplication/EncryptDocument* ha una variabile di input denominata `inDoc`. Non è necessario specificare inDoc, purché il modulo venga inviato come PDF.

È inoltre possibile inviare i dati del modulo come XML a un processo Forms. Per inviare i dati XML, assicurarsi che il menu a discesa `Submit As` specifichi XML. Poiché il valore restituito dal processo deve essere un documento PDF, il documento PDF viene visualizzato in Acrobat.
