---
title: Contenitore di servizio
seo-title: Contenitore di servizio
description: Servizi AEM Forms situati nel contenitore di servizi
uuid: 89f2fd3d-63d7-4b70-b335-47314441f3ec
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding, development-tools
discoiquuid: dd9c0ec4-a195-4b78-8992-81d0efcc0a7e
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 0%

---


# Contenitore di servizi {#service-container}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

I servizi AEM Forms situati nel contenitore di servizi (inclusi i servizi standard come il servizio di crittografia, i processi a lunga durata e quelli a breve durata) possono essere richiamati utilizzando vari provider, ad esempio un provider EJB. Un provider EJB consente di richiamare i servizi AEM Forms tramite RMI/IIOP. Un provider di servizi web espone i servizi come servizi web (generazione WSDL) utilizzando standard quali SOAP/HTTP e SOAP/JMS.

Nella tabella seguente sono descritti i diversi modi in cui è possibile richiamare i servizi AEM Forms a livello di programmazione.

<table>
 <thead>
  <tr>
   <th><p>Metodo di incitamento</p></th>
   <th><p>Descrizione</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Integrazione remota</p></td>
   <td><p>L'integrazione remota consente ai client Flex di richiamare le operazioni del servizio. (Vedere <a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting">Richiamo di AEM Forms utilizzando (obsoleto per i moduli AEM) AEM Forms Remoting</a>.)</p></td>
  </tr>
  <tr>
   <td><p>API Java</p></td>
   <td><p>Un’API Java può richiamare un servizio AEM Forms. L’API Java è organizzata in librerie client e nell’API Java Invocation. (Consulta <a href="/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api">Richiamo di AEM Forms tramite l'API Java</a>.)</p></td>
  </tr>
  <tr>
   <td><p>Servizi web</p></td>
   <td><p>AEM Forms supporta gli standard dei servizi web come SOAP/HTTP. Un servizio può essere esposto come servizio Web, con il WSDL conforme agli standard di servizio Web definiti da W3C.</p><p>È possibile richiamare un servizio da qualsiasi stack di servizi Web, inclusi .NET Framework e Sun™ Web Services SDK. (Vedere <a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services">Richiamo di AEM Forms tramite Web Services</a>.)</p></td>
  </tr>
  <tr>
   <td><p>Richieste REST</p></td>
   <td><p>AEM Forms supporta le richieste REST. Un servizio può essere richiamato direttamente da una pagina HTML. (Consulta <a href="/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests">Richiamo di AEM Forms utilizzando le richieste REST</a>.)</p></td>
  </tr>
 </tbody>
</table>

L’illustrazione seguente fornisce una rappresentazione visiva dei diversi modi in cui i servizi AEM Forms possono essere richiamati a livello di programmazione.

>[!NOTE]
>
>Oltre a utilizzare l’SDK per AEM Forms per creare applicazioni client che possono richiamare i servizi AEM Forms, puoi anche creare componenti che possono essere distribuiti nel contenitore di servizi. Ad esempio, puoi creare un componente Banca contenente tipi di dati personalizzati che possono essere utilizzati nei processi. In altre parole, puoi creare un tipo di dati come `com.adobe.idp.BankAccount`. Puoi quindi creare istanze `com.adobe.idp.BankAccount` nelle applicazioni client.

Il contenitore di servizi fornisce le seguenti funzionalità:

* Consente di richiamare i servizi AEM Forms con metodi diversi. Puoi configurare un servizio impostando gli endpoint in modo che possa essere richiamato utilizzando tutti i metodi: Remoto, API Java, servizi web e REST. (Vedere [Gestione programmatica degli endpoint](/help/forms/developing/programmatically-endpoints.md#programmatically-managing-endpoints).)
* Converte un messaggio in un formato normalizzato denominato richiesta di chiamata. Una richiesta di chiamata viene inviata da un&#39;applicazione client (o da un altro servizio) a un servizio situato nel contenitore del servizio. Una richiesta di chiamata contiene informazioni quali il nome del servizio da richiamare e i valori dei dati necessari per eseguire l&#39;operazione. Molti servizi richiedono un documento per eseguire un&#39;operazione. Pertanto, una richiesta di chiamata di solito contiene un documento, che può essere dati PDF, dati XDP, dati XML e così via.
* Esegue le richieste di chiamata ai servizi appropriati (il nome del servizio da richiamare fa parte della richiesta di chiamata).
* Esegue attività quali determinare se il chiamante dispone dell&#39;autorizzazione per richiamare l&#39;operazione di servizio specificata. La richiesta di chiamata deve contenere un nome utente e una password validi AEM forms.

   Esistono diversi modi per inviare una richiesta di chiamata a un servizio. Inoltre, esistono diversi modi per inviare i valori di input richiesti al servizio. Ad esempio, si supponga di utilizzare l’API Java per richiamare un servizio che richiede un documento PDF. Il metodo Java corrispondente contiene un parametro che accetta un documento PDF. In questa situazione, il tipo di dati del parametro è `com.adobe.idp.Document`. (Consulta [Trasmissione di dati ai servizi AEM Forms tramite l&#39;API Java](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api).)

   Se invochi un servizio utilizzando cartelle controllate, viene inviata una richiesta di chiamata quando inserisci un file in una cartella controllata configurata. Se invochi un servizio tramite e-mail, una richiesta di chiamata viene inviata a un servizio quando un messaggio di posta elettronica arriva in una casella in entrata configurata.

   Il contenitore di servizi invia una risposta di chiamata dopo l&#39;esecuzione dell&#39;operazione. Una risposta di chiamata contiene informazioni quali i risultati dell&#39;operazione. Ad esempio, se l’operazione modifica un documento PDF, la risposta di chiamata contiene il documento PDF modificato. Se l&#39;operazione non è riuscita, la risposta alla chiamata contiene un messaggio di errore.

   Una risposta di chiamata può essere recuperata nello stesso modo in cui viene inviata una richiesta di chiamata. In altre parole, se la richiesta di chiamata viene inviata utilizzando l&#39;API Java, è possibile recuperare una risposta di chiamata utilizzando l&#39;API Java. Si supponga, ad esempio, che un’operazione modifichi un documento PDF. È possibile recuperare il documento PDF modificato ottenendo il valore restituito dal metodo Java che ha richiamato il servizio.

   Quando si richiama un processo di lunga durata, una risposta di chiamata contiene un valore di identificatore associato alla richiesta di chiamata. Utilizzando questo valore di identificatore, puoi controllare lo stato del processo in un secondo momento. Ad esempio, consideriamo il servizio a lungo termine mutuo ipotecario. Utilizzando il valore dell&#39;identificatore, puoi verificare se il processo è stato completato correttamente. (Vedere [Richiamo di processi a lunga durata incentrati sull&#39;uomo](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).)

   Il diagramma seguente mostra un’applicazione client (che utilizza l’API Java) che richiama un servizio.

   Quando un&#39;applicazione client richiama un servizio, si verificano tre eventi:

   1. Un&#39;applicazione client invia una richiesta di chiamata a un servizio.
   1. Il servizio esegue l&#39;operazione specificata nella richiesta di chiamata.
   1. Il contenitore di servizi restituisce una risposta di chiamata all&#39;applicazione client.

**Consulta anche**

[Informazioni sui processi AEM Forms](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)

[Richiamo di AEM Forms utilizzando (obsoleto per i moduli AEM) AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Richiamo di AEM Forms tramite l’API Java](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Richiamo di AEM Forms tramite i servizi web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)

[Richiamo dei processi a lunga durata incentrati sull&#39;uomo](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Richiamo di AEM Forms utilizzando le richieste REST](/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests)
