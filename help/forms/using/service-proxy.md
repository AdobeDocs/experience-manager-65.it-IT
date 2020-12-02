---
title: Proxy del servizio moduli HTML5
seo-title: Proxy del servizio moduli HTML5
description: Il proxy di servizio moduli HTML5 è una configurazione per registrare un proxy per il servizio di invio. Per configurare il proxy di servizio, specificate l'URL del servizio di invio tramite il parametro request submitServiceProxy.
seo-description: Il proxy di servizio moduli HTML5 è una configurazione per registrare un proxy per il servizio di invio. Per configurare il proxy di servizio, specificate l'URL del servizio di invio tramite il parametro request submitServiceProxy.
uuid: 42d6c1da-3945-469d-b429-c33e563ed70c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 081f7c17-4e5d-4c7e-a5c3-5541a29b9d55
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 1%

---


# Proxy servizio moduli HTML5{#html-forms-service-proxy}

Il proxy di servizio moduli HTML5 è una configurazione per registrare un proxy per il servizio di invio. Per configurare il proxy di servizio, specificate l&#39;URL del servizio di invio tramite il parametro di richiesta *submitServiceProxy*.

## Vantaggi del proxy di servizio {#benefits-of-service-proxy-br}

Il proxy di servizio elimina quanto segue:

* Il flusso di lavoro dei moduli HTML5 richiede l’apertura del servizio di invio &quot;/content/xfaforms/submit/default&quot; per gli utenti dei moduli HTML5. Espone AEM server a un pubblico più vasto e non intenzionale.
* L&#39;URL del servizio è incorporato nel modello runtime del modulo. Non è possibile modificare il percorso dell&#39;URL del servizio.
* L&#39;invio è un processo in due fasi. Per inviare i dati del modulo, l&#39;invio richiede almeno due viaggi al server. Aumenta quindi il carico sul server.
* I moduli HTML5 inviano dati nella richiesta POST invece che nella richiesta PDF. Per i flussi di lavoro che coinvolgono moduli PDF e HTML5, sono necessari due metodi diversi per elaborare gli invii.

### Topologie {#topologies-br}

I moduli HTML5 possono utilizzare le seguenti topologie per connettersi ai server AEM.

* Topologia in cui AEM moduli Server o HTML5 inviano dati al server tramite POST.
* Topologia in cui il server proxy invia dati POST al server.

![Topologie proxy del servizio moduli HTML5](assets/topology.png)

Topologie proxy del servizio moduli HTML5

I moduli HTML5 si connettono ai server AEM per eseguire script, servizi Web e invii sul lato server. Il runtime XFA dei moduli HTML5 utilizza chiamate Ajax al punto finale &quot;/bin/xfaforms/submitaction&quot; con vari parametri per connettersi ai server AEM. I moduli HTML5 collegano AEM server per eseguire le operazioni seguenti:

#### Esegui script sul lato server e servizi Web {#execute-server-sided-scripts-and-web-services}

Gli script contrassegnati per l&#39;esecuzione sul server sono noti come script sul lato server. Nella tabella seguente sono elencati tutti i parametri utilizzati negli script sul lato server e nei servizi Web.

<table>
 <tbody>
  <tr>
   <td><p><strong>Parametro</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p>activity</p> </td>
   <td><p>L'attività contiene gli eventi che attivano la richiesta. Ad esempio clic, uscita o modifica</p> </td>
  </tr>
  <tr>
   <td><p>contextSom</p> </td>
   <td><p>contextSom contiene l'espressione SOM dell'oggetto in cui vengono eseguiti gli eventi.</p> </td>
  </tr>
  <tr>
   <td><p>Modello</p> </td>
   <td><p>Il modello contiene il modello utilizzato per eseguire il rendering del modulo.</p> </td>
  </tr>
  <tr>
   <td><p>contentRoot</p> </td>
   <td><p>contentRoot contiene la directory principale del modello utilizzata per eseguire il rendering del modulo.</p> </td>
  </tr>
  <tr>
   <td><p>Dati</p> </td>
   <td><p>I dati contengono byte di dati utilizzati per il rendering del modulo.</p> </td>
  </tr>
  <tr>
   <td><p>formDom</p> </td>
   <td><p>formDom contiene il DOM del modulo HTML5 in formato JSON.</p> </td>
  </tr>
  <tr>
   <td><p>packet</p> </td>
   <td><p>è specificato come modulo.</p> </td>
  </tr>
  <tr>
   <td><p>debugDir</p> </td>
   <td><p>debugDir contiene la directory di debug utilizzata per eseguire il rendering del modulo.</p> </td>
  </tr>
 </tbody>
</table>

#### Invia dati {#submit-data}

Facendo clic sul pulsante di invio, i moduli HTML5 inviano i dati al server. Nella tabella seguente sono elencati tutti i parametri che i moduli HTML5 inviano al server.

<table>
 <tbody>
  <tr>
   <td><p><strong>Parametro</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p>Modello</p> </td>
   <td><p>Modello utilizzato per eseguire il rendering del modulo.</p> </td>
  </tr>
  <tr>
   <td><p>contentRoot</p> </td>
   <td><p>directory principale del modello utilizzata per eseguire il rendering del modulo.</p> </td>
  </tr>
  <tr>
   <td><p>Dati</p> </td>
   <td><p>byte di dati utilizzati per il rendering del modulo.</p> </td>
  </tr>
  <tr>
   <td><p>formDom</p> </td>
   <td><p>DOM del modulo HTML5 in formato JSON.</p> </td>
  </tr>
  <tr>
   <td><p>submiturl</p> </td>
   <td><p>L'URL in cui viene inviato l'XML dei dati.</p> </td>
  </tr>
  <tr>
   <td><p>debugDir</p> </td>
   <td><p>La directory di debug utilizzata per eseguire il rendering del modulo.</p> </td>
  </tr>
 </tbody>
</table>

#### Come funziona il proxy di invio? {#how-nbsp-the-nbsp-submit-proxy-works}

Il proxy del servizio di invio funge da pass-through se l’URL di invio non è presente nel parametro della richiesta. Agisce come un passaggio. Invia la richiesta al punto finale /bin/xfaforms/submitaction e invia la risposta al runtime XFA.

Il proxy del servizio di invio seleziona una topologia se l’URL di invio è presente nel parametro della richiesta.

* Se AEM server inviano i dati, il servizio proxy agisce come un pass-through. Invia la richiesta al punto finale /bin/xfaforms/submitaction e invia la risposta al runtime XFA.
* Se il proxy pubblica i dati, il servizio proxy passa tutti i parametri eccetto submitUrl al punto finale */bin/xfaforms/submitaction* e riceve i byte xml nel flusso di risposta. Quindi, il servizio proxy invia i byte del codice xml dei dati a submitUrl per l&#39;elaborazione.

* Prima di inviare dati (richiesta POST) a un server, i moduli HTML5 verificano la connettività e la disponibilità del server. Per verificare la connettività e la disponibilità, i moduli HTML inviano al server una richiesta head vuota. Se il server è disponibile, il modulo HTML5 invia dati (richiesta POST) al server. Se il server non è disponibile, viene visualizzato un messaggio di errore *Impossibile connettersi al server,*. Il rilevamento anticipato impedisce agli utenti di compilare il modulo in modo semplice. Il servlet proxy gestisce la richiesta dell&#39;intestazione e non genera eccezioni.
