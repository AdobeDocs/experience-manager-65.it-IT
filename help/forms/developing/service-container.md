---
title: Contenitore di servizi
seo-title: Contenitore di servizi
description: 'null'
seo-description: 'null'
uuid: 89f2fd3d-63d7-4b70-b335-47314441f3ec
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding, development-tools
discoiquuid: dd9c0ec4-a195-4b78-8992-81d0efcc0a7e
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 0%

---


# Service container {#service-container}

 servizi AEM Forms situati nel contenitore di servizi (compresi i servizi standard quali il servizio di cifratura, i processi di lunga durata e di breve durata) possono essere invocati tramite diversi fornitori, ad esempio un provider EJB. Un provider EJB consente di richiamare  servizi AEM Forms attraverso RMI/IIOP. Un provider di servizi Web espone i servizi come servizi Web (generazione WSDL) utilizzando standard quali SOAP/HTTP e SOAP/JMS.

Nella tabella seguente sono descritti i diversi modi in cui è possibile invocare  servizi AEM Forms a livello di programmazione.

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
   <td><p>L'integrazione remota consente ai client Flex di richiamare le operazioni del servizio. (Vedere <a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting">Chiamata  AEM Forms utilizzando (obsoleto per AEM moduli)  AEM Forms Remoting</a>.)</p></td>
  </tr>
  <tr>
   <td><p>API Java</p></td>
   <td><p>Un'API Java può richiamare un servizio AEM Forms . L'API Java è organizzata nelle librerie client e nell'API Java Invocation. (Vedete <a href="/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api">Chiamata  AEM Forms tramite l'API</a>Java.)</p></td>
  </tr>
  <tr>
   <td><p>Servizi Web</p></td>
   <td><p> AEM Forms supporta gli standard dei servizi Web come SOAP/HTTP. Un servizio può essere esposto come servizio Web, con il WSDL conforme agli standard di servizio Web definiti da W3C.</p><p>È possibile richiamare un servizio da qualsiasi stack di servizi Web, incluso .NET Framework e Sun™ Web Services SDK. (Vedere <a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services">Chiamata  AEM Forms tramite i servizi</a>Web.)</p></td>
  </tr>
  <tr>
   <td><p>Richieste REST</p></td>
   <td><p> AEM Forms supporta le richieste REST. Un servizio può essere richiamato direttamente da una pagina HTML. (Vedete <a href="/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests">Chiamata  AEM Forms mediante richieste</a>REST.)</p></td>
  </tr>
 </tbody>
</table>

L&#39;illustrazione seguente fornisce una rappresentazione visiva dei diversi modi in cui  servizi AEM Forms possono essere invocati a livello di programmazione.

>[!NOTE]
>
>Oltre a usare l’SDK per AEM Forms  per creare applicazioni client che possono richiamare  servizi AEM Forms, potete anche creare componenti che possono essere distribuiti nel contenitore dei servizi. Ad esempio, è possibile creare un componente Banca che contiene tipi di dati personalizzati utilizzabili nei processi. In altre parole, è possibile creare un tipo di dati come `com.adobe.idp.BankAccount`. Potete quindi creare `com.adobe.idp.BankAccount` istanze nelle applicazioni client.

Il contenitore del servizio fornisce le seguenti funzionalità:

* Consente di richiamare  servizi AEM Forms utilizzando metodi diversi. Puoi configurare un servizio impostando gli endpoint in modo che possa essere invocato utilizzando tutti i metodi: Remoto, API Java, servizi Web e REST. (Vedere Gestione [programmatica degli endpoint](/help/forms/developing/programmatically-endpoints.md#programmatically-managing-endpoints).)
* Converte un messaggio in un formato normalizzato denominato richiesta di chiamata. Una richiesta di chiamata viene inviata da un&#39;applicazione client (o da un altro servizio) a un servizio che si trova nel contenitore del servizio. Una richiesta di chiamata contiene informazioni quali il nome del servizio da richiamare e i valori dei dati necessari per eseguire l&#39;operazione. Molti servizi richiedono un documento per eseguire un&#39;operazione. Di conseguenza, una richiesta di chiamata in genere contiene un documento, che può essere dati PDF, dati XDP, dati XML e così via.
* Invia le richieste di chiamata ai servizi appropriati (il nome del servizio da richiamare fa parte della richiesta di chiamata).
* Esegue attività quali determinare se il chiamante dispone dell&#39;autorizzazione per richiamare l&#39;operazione del servizio specificata. La richiesta di chiamata deve contenere un nome utente e una password validi per i moduli AEM.

   Esistono diversi modi per inviare una richiesta di chiamata a un servizio. Inoltre, esistono diversi modi per inviare i valori di input richiesti al servizio. Ad esempio, si supponga di utilizzare l&#39;API Java per richiamare un servizio che richiede un documento PDF. Il metodo Java corrispondente contiene un parametro che accetta un documento PDF. In questa situazione, il tipo di dati del parametro è `com.adobe.idp.Document`. (vedere [Trasmissione di dati a  servizi AEM Forms tramite l&#39;API](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)Java).

   Se richiamate un servizio utilizzando le cartelle esaminate, quando inserite un file in una cartella esaminata configurata viene inviata una richiesta di chiamata. Se richiamate un servizio tramite e-mail, una richiesta di chiamata viene inviata a un servizio quando un messaggio e-mail arriva in una inbox configurata.

   Il contenitore del servizio invia una risposta di chiamata una volta eseguita l&#39;operazione. Una risposta di chiamata contiene informazioni quali i risultati dell&#39;operazione. Ad esempio, se l&#39;operazione modifica un documento PDF, la risposta di chiamata contiene il documento PDF modificato. Se l&#39;operazione non ha avuto esito positivo, la risposta di chiamata contiene un messaggio di errore.

   Una risposta di chiamata può essere recuperata nello stesso modo in cui viene inviata una richiesta di chiamata. In altre parole, se la richiesta di chiamata viene inviata utilizzando l&#39;API Java, è possibile recuperare una risposta di chiamata utilizzando l&#39;API Java. Si supponga, ad esempio, che un&#39;operazione modifichi un documento PDF. È possibile recuperare il documento PDF modificato ottenendo il valore restituito dal metodo Java che ha richiamato il servizio.

   Quando viene richiamato un processo di lunga durata, una risposta di chiamata contiene un valore di identificatore associato alla richiesta di chiamata. Utilizzando questo valore di identificatore, potete controllare lo stato del processo in un secondo momento. Ad esempio, si consideri il servizio di lunga durata di mutuo ipotecario. Utilizzando il valore dell&#39;identificatore, potete verificare se il processo è stato completato correttamente. (Vedete [Richiamo Di Processi](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)Lunghi Orientati All’Umano.)

   Il diagramma seguente mostra un&#39;applicazione client (che utilizza l&#39;API Java) che richiama un servizio.

   Quando un&#39;applicazione client richiama un servizio, si verificano tre eventi:

   1. Un&#39;applicazione client invia una richiesta di chiamata a un servizio.
   1. Il servizio esegue l&#39;operazione specificata nella richiesta di chiamata.
   1. Il contenitore del servizio restituisce una risposta di chiamata all&#39;applicazione client.

**Consulta anche**

[Informazioni  processi AEM Forms](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)

[Richiamo  AEM Forms utilizzando (obsoleto per AEM moduli)  AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Chiamata  AEM Forms tramite l&#39;API Java](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Chiamata  AEM Forms tramite servizi Web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)

[Richiamo di processi a lunga durata basati sull&#39;uomo](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Chiamata  AEM Forms tramite richieste REST](/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests)
