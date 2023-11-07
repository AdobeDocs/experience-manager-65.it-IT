---
title: Contenitore servizio
seo-title: Service container
description: Servizi AEM Forms nel contenitore di servizi
uuid: 89f2fd3d-63d7-4b70-b335-47314441f3ec
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding, development-tools
discoiquuid: dd9c0ec4-a195-4b78-8992-81d0efcc0a7e
role: Developer
exl-id: 6abf2401-5a87-4f72-9028-74580df5b9de
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 0%

---

# Contenitore servizio {#service-container}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

I servizi AEM Forms nel contenitore di servizi (inclusi i servizi standard come il servizio di crittografia, i processi di lunga durata e quelli di breve durata) possono essere richiamati utilizzando vari provider, ad esempio un provider EJB. Un provider EJB consente di richiamare i servizi AEM Forms tramite RMI/IIOP. Un provider di servizi Web espone i servizi come servizi Web (generazione WSDL) utilizzando standard quali SOAP/HTTP e SOAP/JMS.

La tabella seguente descrive i diversi modi in cui è possibile richiamare a livello di programmazione i servizi di AEM Forms.

<table>
 <thead>
  <tr>
   <th><p>Metodo di chiamata</p></th>
   <th><p>Descrizione</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Integrazione remota</p></td>
   <td><p>L'integrazione remota consente ai client Flex di richiamare le operazioni del servizio. (vedere <a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting">Richiamare AEM Forms tramite (obsoleto per i moduli AEM) AEM Forms Remoting</a>.)</p></td>
  </tr>
  <tr>
   <td><p>API Java</p></td>
   <td><p>Un’API Java può richiamare un servizio AEM Forms. L’API Java è organizzata in librerie client e API Java Invocation. (vedere <a href="/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api">Richiamare AEM Forms tramite l’API Java</a>.)</p></td>
  </tr>
  <tr>
   <td><p>Servizi web</p></td>
   <td><p>AEM Forms supporta gli standard dei servizi web come SOAP/HTTP. Un servizio può essere esposto come servizio web, con il WSDL conforme agli standard di servizio web definiti dal W3C.</p><p>Un servizio può essere richiamato da qualsiasi stack di servizi Web, inclusi .NET Framework e Sun™ Web Services SDK. (vedere <a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services">Richiamare AEM Forms tramite servizi Web</a>.)</p></td>
  </tr>
  <tr>
   <td><p>Richieste REST</p></td>
   <td><p>AEM Forms supporta le richieste REST. Un servizio può essere richiamato direttamente da una pagina HTML. (vedere <a href="/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests">Richiamare AEM Forms tramite richieste REST</a>.)</p></td>
  </tr>
 </tbody>
</table>

L’illustrazione seguente fornisce una rappresentazione visiva dei diversi modi in cui i servizi AEM Forms possono essere richiamati a livello di programmazione.

>[!NOTE]
>
>Oltre a utilizzare l’SDK di AEM Forms per creare applicazioni client che possono richiamare i servizi AEM Forms, puoi anche creare componenti che possono essere distribuiti nel contenitore di servizi. È ad esempio possibile creare un componente Banca contenente tipi di dati personalizzati che possono essere utilizzati nei processi. In altre parole, puoi creare un tipo di dati come `com.adobe.idp.BankAccount`. A questo punto puoi creare `com.adobe.idp.BankAccount` nelle applicazioni client.

Il contenitore di servizi fornisce le funzionalità seguenti:

* Consente di richiamare i servizi AEM Forms utilizzando metodi diversi. Puoi configurare un servizio impostando gli endpoint in modo che possano essere richiamati utilizzando tutti i metodi: Remoting, API Java, servizi web e REST. (vedere [Gestione programmatica degli endpoint](/help/forms/developing/programmatically-endpoints.md#programmatically-managing-endpoints).)
* Converte un messaggio in un formato normalizzato denominato richiesta di chiamata. Viene inviata una richiesta di chiamata da un&#39;applicazione client (o da un altro servizio) a un servizio nel contenitore del servizio. Una richiesta di chiamata contiene informazioni quali il nome del servizio da richiamare e i valori dei dati necessari per eseguire l&#39;operazione. Molti servizi richiedono un documento per eseguire un&#39;operazione. Pertanto, una richiesta di chiamata contiene in genere un documento, che può essere costituito da dati PDF, dati XDP, dati XML e così via.
* Indirizza le richieste di chiamata ai servizi appropriati (il nome del servizio da richiamare fa parte della richiesta di chiamata).
* Esegue attività quali determinare se il chiamante dispone dell&#39;autorizzazione per richiamare l&#39;operazione di servizio specificata. La richiesta di chiamata deve contenere un nome utente e una password validi per i moduli AEM.

  Esistono diversi modi per inviare una richiesta di chiamata a un servizio. Inoltre, esistono diversi modi per inviare i valori di input richiesti al servizio. Si supponga, ad esempio, di utilizzare l&#39;API Java per richiamare un servizio che richiede un documento PDF. Il metodo Java corrispondente contiene un parametro che accetta un documento PDF. In questa situazione, il tipo di dati del parametro è `com.adobe.idp.Document`. (vedere [Passaggio dei dati ai servizi AEM Forms tramite API Java](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api).)

  Se richiami un servizio utilizzando cartelle controllate, viene inviata una richiesta di chiamata quando inserisci un file in una cartella controllata configurata. Se si richiama un servizio tramite posta elettronica, viene inviata una richiesta di chiamata a un servizio quando un messaggio di posta elettronica arriva in una casella in entrata configurata.

  Il contenitore del servizio invia una risposta di chiamata una volta eseguita l&#39;operazione. Una risposta alla chiamata contiene informazioni quali i risultati dell&#39;operazione. Se, ad esempio, l&#39;operazione modifica un documento PDF, la risposta alla chiamata contiene il documento PDF modificato. Se l&#39;operazione non è riuscita, la risposta alla chiamata contiene un messaggio di errore.

  È possibile recuperare una risposta di chiamata nello stesso modo in cui viene inviata una richiesta di chiamata. In altre parole, se la richiesta di chiamata viene inviata utilizzando l’API Java, è possibile recuperare una risposta di chiamata utilizzando l’API Java. Si supponga, ad esempio, che un&#39;operazione modifichi un documento PDF. È possibile recuperare il documento PDF modificato ottenendo il valore restituito dal metodo Java che ha richiamato il servizio.

  Quando si richiama un processo di lunga durata, una risposta di chiamata contiene un valore di identificatore associato alla richiesta di chiamata. Utilizzando questo valore di identificatore, puoi controllare lo stato del processo in un secondo momento. Ad esempio, si consideri il servizio di lunga durata di MortgageLoan. Utilizzando il valore dell’identificatore, puoi verificare se il processo è stato completato correttamente. (vedere [Richiamare processi a lunga durata incentrati sull&#39;uomo](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).)

  Il diagramma seguente mostra un’applicazione client (che utilizza l’API Java) che richiama un servizio.

  Quando un&#39;applicazione client richiama un servizio, si verificano tre eventi:

   1. Un&#39;applicazione client invia una richiesta di chiamata a un servizio.
   1. Il servizio esegue l&#39;operazione specificata nella richiesta di chiamata.
   1. Il contenitore del servizio restituisce una risposta di chiamata all&#39;applicazione client.

**Consulta anche**

[Informazioni sui processi di AEM Forms](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes)

[Richiamare AEM Forms tramite (obsoleto per i moduli AEM) AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)

[Richiamare AEM Forms tramite l’API Java](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Richiamare AEM Forms tramite servizi Web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)

[Richiamare processi a lunga durata incentrati sull&#39;uomo](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Richiamare AEM Forms tramite richieste REST](/help/forms/developing/invoking-aem-forms-using-rest.md#invoking-aem-forms-using-rest-requests)
