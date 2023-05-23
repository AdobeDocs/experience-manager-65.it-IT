---
title: proxy del servizio HTML5 forms
seo-title: HTML5 forms service proxy
description: Il proxy del servizio HTML5 forms è una configurazione che consente di registrare un proxy per il servizio di invio. Per configurare Service Proxy, specifica l’URL del servizio di invio tramite il parametro di richiesta submitServiceProxy.
seo-description: HTML5 forms Service Proxy is a configuration to register a proxy for the submission service. To configure Service Proxy, specify the URL of submission service through request parameter submissionServiceProxy.
uuid: 42d6c1da-3945-469d-b429-c33e563ed70c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 081f7c17-4e5d-4c7e-a5c3-5541a29b9d55
docset: aem65
feature: Mobile Forms
exl-id: 8f9b10ae-1600-49c2-a061-153a2a89c67e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 1%

---

# proxy del servizio HTML5 forms{#html-forms-service-proxy}

Il proxy del servizio HTML5 forms è una configurazione che consente di registrare un proxy per il servizio di invio. Per configurare Service Proxy, specifica l’URL del servizio di invio tramite il parametro della richiesta *submitServiceProxy*.

## Vantaggi del proxy di servizio {#benefits-of-service-proxy-br}

Il proxy del servizio elimina i seguenti elementi:

* Il flusso di lavoro di HTML5 Forms richiede l’apertura del servizio di invio &quot;/content/xfaforms/submit/default&quot; per gli utenti di HTML5 forms. Espone i server dell’AEM a un pubblico non intenzionale più ampio.
* L’URL del servizio è incorporato nel modello di runtime del modulo. Impossibile modificare il percorso dell&#39;URL del servizio.
* L’invio è un processo in due fasi. Per inviare i dati del modulo, sono necessari almeno due percorsi al server. Di conseguenza, aumenta il carico sul server.
* I moduli HTML5 inviano dati nella richiesta POST anziché nella richiesta PDF. Per i flussi di lavoro che coinvolgono moduli PDF e HTML5, sono necessari due diversi metodi di elaborazione degli invii.

### Topologie {#topologies-br}

I moduli HTML5 possono utilizzare le seguenti topologie per connettersi ai server AEM.

* Una topologia in cui i moduli AEM Server o HTML5 inviano dati al server tramite POST.
* Topologia in cui il server proxy invia i dati POST al server.

![Topologie proxy del servizio HTML5 forms](assets/topology.png)

Topologie proxy del servizio HTML5 forms

I moduli HTML5 si connettono ai server AEM per eseguire script lato server, servizi Web e invii. Il runtime XFA dei moduli HTML5 utilizza chiamate Ajax sull’endpoint &quot;/bin/xfaforms/submitaction&quot; con vari parametri per la connessione ai server AEM. I moduli HTML5 consentono di connettere i server AEM per eseguire le operazioni seguenti:

#### Esecuzione di script lato server e servizi Web {#execute-server-sided-scripts-and-web-services}

Gli script contrassegnati per l&#39;esecuzione sul server sono noti come script lato server. Nella tabella seguente sono elencati tutti i parametri utilizzati negli script lato server e nei servizi Web.

<table>
 <tbody>
  <tr>
   <td><p><strong>Parametro</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p>attività</p> </td>
   <td><p>L’attività contiene gli eventi che attivano la richiesta. Ad esempio clic, uscita o modifica</p> </td>
  </tr>
  <tr>
   <td><p>contextSom</p> </td>
   <td><p>contextSom contiene l'espressione SOM dell'oggetto in cui vengono eseguiti gli eventi.</p> </td>
  </tr>
  <tr>
   <td><p>Modello</p> </td>
   <td><p>Il modello contiene il modello utilizzato per il rendering del modulo.</p> </td>
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
   <td><p>formDom contiene DOM del modulo HTML5 in formato JSON.</p> </td>
  </tr>
  <tr>
   <td><p>pacchetto</p> </td>
   <td><p>pacchetto specificato come modulo.</p> </td>
  </tr>
  <tr>
   <td><p>debugDir</p> </td>
   <td><p>debugDir contiene la directory di debug utilizzata per il rendering del modulo.</p> </td>
  </tr>
 </tbody>
</table>

#### Inviare dati {#submit-data}

Facendo clic sul pulsante di invio, i moduli HTML5 inviano dati al server. Nella tabella seguente sono elencati tutti i parametri inviati dai moduli HTML5 al server.

<table>
 <tbody>
  <tr>
   <td><p><strong>Parametro</strong></p> </td>
   <td><p><strong>Descrizione</strong></p> </td>
  </tr>
  <tr>
   <td><p>Modello</p> </td>
   <td><p>Modello utilizzato per il rendering del modulo.</p> </td>
  </tr>
  <tr>
   <td><p>contentRoot</p> </td>
   <td><p>directory principale del modello utilizzata per il rendering del modulo.</p> </td>
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
   <td><p>URL in cui viene pubblicato l'XML dati.</p> </td>
  </tr>
  <tr>
   <td><p>debugDir</p> </td>
   <td><p>Directory di debug utilizzata per il rendering del modulo.</p> </td>
  </tr>
 </tbody>
</table>

#### Funzionamento del proxy di invio {#how-nbsp-the-nbsp-submit-proxy-works}

Il proxy del servizio di invio funge da pass-through se il submiturl non è presente nel parametro della richiesta. Funge da pass-through. Invia la richiesta all’endpoint /bin/xfaforms/submitaction e invia la risposta al runtime XFA.

Il proxy del servizio di invio seleziona una topologia se submiturl è presente nel parametro della richiesta.

* Se i server AEM pubblicano i dati, il servizio proxy funge da pass-through. Invia la richiesta all’endpoint /bin/xfaforms/submitaction e invia la risposta al runtime XFA.
* Se il proxy pubblica i dati, il servizio proxy trasmette tutti i parametri ad eccezione di submitUrl al */bin/xfaforms/submitaction* end point e riceve i byte xml nel flusso di risposta. Successivamente, il servizio proxy invia i byte XML dei dati all&#39;elemento submitUrl per l&#39;elaborazione.

* Prima di inviare i dati (richiesta POST) a un server, i moduli HTML5 verificano la connettività e la disponibilità del server. Per verificare la connettività e la disponibilità, i moduli HTML inviano una richiesta head vuota al server. Se il server è disponibile, il modulo HTML5 invia i dati (richiesta POST) al server. Se il server non è disponibile, viene visualizzato un messaggio di errore, *Impossibile connettersi al server,* viene visualizzato. Il rilevamento avanzato impedisce agli utenti di riempire nuovamente il modulo. Il servlet proxy gestisce la richiesta head e non genera un’eccezione.
