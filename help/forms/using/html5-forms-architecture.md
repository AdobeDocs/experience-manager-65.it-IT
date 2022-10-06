---
title: Architettura dei moduli di HTML5
seo-title: Architecture of HTML5 forms
description: HTML5 forms viene distribuito come pacchetto all’interno dell’istanza AEM incorporata ed espone la funzionalità come punto finale REST su HTTP/S utilizzando l’architettura RESTful Apache Sling.
seo-description: HTML5 forms is deployed as a package within the embedded AEM instance and exposes the functionality as REST end point over HTTP/S using RESTful Apache Sling architecture.
uuid: 7f515cea-1447-4fc7-82ba-17f2e3f9f80c
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: a644978e-5736-4771-918a-dfefe350a4a1
docset: aem65
feature: Mobile Forms
exl-id: ed8349a1-f761-483f-9186-bf435899df7d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2011'
ht-degree: 0%

---

# Architettura dei moduli di HTML5{#architecture-of-html-forms}

## Architettura {#architecture}

La funzionalità HTML5 forms viene distribuita come pacchetto all’interno dell’istanza AEM incorporata e viene esposta come punto finale REST su HTTP/S utilizzando RESTful [Architettura Apache Sling](https://sling.apache.org/).

![02-aem-forms-architecture_large](assets/02-aem-forms-architecture_large.jpg)

### Utilizzo del framework Sling {#using-sling-framework}

[Sling Apache](https://sling.apache.org/) è incentrato sulle risorse. Utilizza un URL di richiesta per risolvere prima la risorsa. Ogni risorsa ha un **sling:resourceType** o **sling:resourceSuperType**). In base a questa proprietà, al metodo di richiesta e alle proprietà dell’URL della richiesta, viene quindi selezionato uno script sling per gestire la richiesta. Questo script sling può essere un JSP o un servlet. Per i moduli HTML5, **Profilo** nodi fungono da risorse sling e **Renderer del profilo** agisce come script sling che gestisce la richiesta di rendering del modulo mobile con un particolare profilo. A **Renderer del profilo** è un JSP che legge i parametri da una richiesta e chiama il servizio Forms OSGi.

Per informazioni dettagliate sull’endpoint REST e sui parametri di richiesta supportati, consulta [Modello di modulo di rendering](/help/forms/using/rendering-form-template.md).

Quando un utente effettua una richiesta da un dispositivo client come un browser iOS o Android, Sling risolve prima il Nodo profilo in base all&#39;URL della richiesta. Da questo nodo di profilo si legge **sling:resourceSuperType** e **sling:resourceType** per determinare tutti gli script disponibili in grado di gestire questa richiesta di rendering del modulo. Utilizza quindi selettori di richieste Sling insieme al metodo di richiesta per identificare lo script più adatto per gestire questa richiesta. Una volta che la richiesta raggiunge un Profile Renderer JSP, il JSP chiama il servizio Forms OSGi.

Per ulteriori dettagli sulla risoluzione degli script sling, vedi [AEM Sling Chat Sheet](https://docs.adobe.com/content/docs/en/cq/current/developing/sling_cheatsheet.html) o [Decomposizione URL Sling Apache](https://sling.apache.org/site/url-decomposition.html).

#### Flusso di chiamate di elaborazione dei moduli tipico {#typical-form-processing-call-flow}

HTML5 forms memorizza nella cache tutti gli oggetti intermedi necessari per elaborare (rendering o invio) un modulo sulla prima richiesta. Non memorizza in cache gli oggetti dipendenti dai dati in quanto tali oggetti potrebbero cambiare.

Il modulo mobile mantiene due diversi livelli di cache, cache di preRender e cache di rendering. La cache di preRender contiene tutti i frammenti e le immagini di un modello risolto e la cache di rendering contiene il contenuto di cui è stato eseguito il rendering, ad esempio HTML.

![Flusso di lavoro di HTML5 forms](assets/cacheworkflow.png)

Flusso di lavoro di HTML5 forms

I moduli di HTML5 non memorizzano nella cache modelli con riferimenti mancanti di frammenti e immagini. Se i moduli di HTML5 richiedono più del tempo normale, controllare i registri del server per verificare la presenza di riferimenti e avvisi mancanti. Inoltre, assicurati che le dimensioni massime dell’oggetto non siano raggiunte.

Il servizio Forms OSGi elabora una richiesta in due passaggi:

* **Generazione di layout e stato modulo iniziale**: Il servizio di rendering OSGi di Forms chiama il componente Forms Cache per determinare se il modulo è già stato memorizzato nella cache e non è stato invalidato. Se il modulo è memorizzato nella cache e valido, distribuisce il HTML generato dalla cache. Se il modulo viene invalidato, il servizio di rendering Forms OSGi genera il layout del modulo iniziale e lo stato del modulo in formato XML. Questo XML viene trasformato in layout HTML e in stato iniziale del modulo JSON dal servizio Forms OSGi e quindi memorizzato nella cache per le richieste successive.
* **Forms prepopolato**: Durante il rendering, se un utente richiede moduli con dati precompilati, il servizio di rendering Forms OSGi chiama il contenitore del servizio Forms e genera un nuovo stato del modulo con i dati uniti. Tuttavia, poiché il layout è già generato nel passaggio precedente, questa chiamata è più veloce della prima chiamata . Questa chiamata esegue solo l&#39;unione dati ed esegue gli script sui dati.

Se è presente un aggiornamento nel modulo o una delle risorse utilizzate all’interno del modulo, il componente cache del modulo lo rileva e la cache per quel particolare modulo viene invalidata. Una volta completata l’elaborazione del servizio Forms OSGi, il modulo di rendering del profilo jsp aggiunge riferimenti e stili della libreria JavaScript a questo modulo e restituisce la risposta al client. Un tipico server web come [Apache](https://httpd.apache.org/) può essere utilizzato qui con la compressione HTML attiva. Un server web ridurrebbe in modo significativo le dimensioni di risposta, il traffico di rete e il tempo necessario per lo streaming dei dati tra server e computer client.

Quando un utente invia il modulo, il browser invia lo stato del modulo in formato JSON al [invia proxy di servizio](../../forms/using/service-proxy.md); il proxy del servizio di invio genera un codice XML di dati utilizzando i dati JSON e invia tale dato XML per inviare l’endpoint.

## Componenti {#components}

È necessario un pacchetto aggiuntivo di AEM Forms per abilitare HTML5 forms. Per informazioni sull&#39;installazione del pacchetto aggiuntivo di AEM Forms, vedi [Installazione e configurazione di AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md).

### Componenti OSGi (adobe-lc-forms-core.jar) {#osgi-components-adobe-lc-forms-core-jar}

**Adobe Forms Renderer (com.adobe.livecycle.adobe-lc-forms-core)** è il nome visualizzato del bundle OSGi di HTML5 forms quando visualizzato da Bundle View of Felix admin console (https://[host]:[porta]/system/console/bundles).

Questo componente contiene componenti OSGi per le impostazioni di rendering, gestione della cache e configurazione.

#### Servizio Forms OSGi {#forms-osgi-service}

Questo servizio OSGi contiene la logica necessaria per eseguire il rendering di un file XDP come HTML e gestisce l’invio di un modulo per generare dati XML. Questo servizio utilizza il contenitore del servizio Forms. Il contenitore di servizi Forms effettua chiamate interne al componente nativo `XMLFormService.exe` che esegue l’elaborazione.

Se viene ricevuta una richiesta di rendering, questo componente chiama il contenitore del servizio Forms per generare informazioni di layout e stato ulteriormente elaborate per generare stati DOM di moduli HTML e JSON.

Questo componente è anche responsabile della generazione di dati XML dallo stato del modulo JSON inviato.

#### Componente cache {#cache-component}

I moduli di HTML5 utilizzano la memorizzazione in cache per ottimizzare il throughput e i tempi di risposta. Puoi configurare il livello del servizio cache per ottimizzare il compromesso tra prestazioni e utilizzo dello spazio.

<table>
 <tbody>
  <tr>
   <th>Strategia cache</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>Nessuno</td>
   <td>Non memorizzare in cache gli artefatti<br /> </td>
  </tr>
  <tr>
   <td>conservatore</td>
   <td>Memorizza in cache solo gli artefatti intermedi generati prima del rendering del modulo, come un modello contenente frammenti e immagini in linea</td>
  </tr>
  <tr>
   <td>Aggressivo</td>
   <td>Contenuto HTML di cui è stato effettuato il rendering nella cache<br /> Memorizza in cache tutti gli artefatti memorizzati nella cache a livello di Conservative.<br /> <strong>Nota</strong>: Questa strategia offre prestazioni migliori ma consuma più memoria per memorizzare gli artefatti memorizzati nella cache.</td>
  </tr>
 </tbody>
</table>

I moduli HTML5 eseguono il caching in memoria utilizzando la strategia LRU. Se la strategia della cache è impostata su Nessuna cache non verrà creata e i dati esistenti della cache, se presenti, verranno cancellati. Oltre alla strategia di caching, è anche possibile configurare la dimensione totale della cache in memoria che può aiutare ad avere il limite massimo sulla dimensione della cache e se va oltre che utilizzare la modalità LRU per liberare le risorse della cache.

>[!NOTE]
>
>La cache in-memory non è condivisa tra i nodi del cluster.

#### Servizio di configurazione {#configuration-service}

Il servizio di configurazione consente di ottimizzare i parametri di configurazione e le impostazioni della cache per i moduli HTML5.

Per aggiornare queste impostazioni, vai all&#39;Admin Console CQ Felix (disponibile all&#39;indirizzo https://&lt;&#39;[server]:[porta]&#39;/system/console/configMgr), cerca e seleziona Configurazione Forms mobile.

Puoi configurare la dimensione della cache o disabilitare la cache utilizzando il servizio di configurazione. È inoltre possibile abilitare il debug utilizzando il parametro Opzioni di debug. Ulteriori informazioni sul debug dei moduli sono disponibili all’indirizzo [Debug dei moduli di HTML5](/help/forms/using/debug.md).

### Componenti runtime (adobe-lc-forms-runtime-pkg.zip) {#runtime-components-adobe-lc-forms-runtime-pkg-zip}

Il pacchetto runtime contiene le librerie lato client utilizzate per il rendering dei moduli HTML.

**Componenti importanti disponibili come parte del pacchetto Runtime:**

#### Motore di scripting {#scripting-engine}

Ad Adobe, l’implementazione XFA supporta due tipi di linguaggi di script per consentire l’esecuzione logica definita dall’utente nei moduli: JavaScript e FormCalc.

Il motore di script di HTML Forms è scritto in JavaScript per supportare l’API di script XFA in entrambi i linguaggi.

Al momento del rendering, lo script FormCalc viene convertito (e memorizzato in cache) in JavaScript sul server trasparente per l&#39;utente o il designer.

Questo motore di scripting utilizza alcune delle funzioni di ECMAScript5 come Object.defineProperty. Il motore/libreria viene consegnato come CQ Client Lib con il nome della categoria **xfaforms.profile**. Fornisce inoltre **API FormBridge** per consentire l’interazione di portali o app esterni con il modulo. Utilizzando FormBridge, un’app esterna può nascondere a livello di programmazione determinati elementi, ottenere o impostare i relativi valori o modificarne gli attributi.

Per ulteriori dettagli, consulta la sezione [Form Bridge](/help/forms/using/form-bridge-apis.md) articolo.

#### Motore di layout {#layout-engine}

Il layout e l’aspetto visivo dei moduli di HTML5 si basano sulle funzioni di SVG 1.1, jQuery, BackBone e CSS3. L’aspetto iniziale di un modulo viene generato e memorizzato nella cache del server. Il cambiamento del layout iniziale e le eventuali ulteriori modifiche incrementali al layout del modulo vengono gestiti dal client. A questo scopo, il pacchetto Runtime contiene un motore di layout scritto in JavaScript e basato su jQuery/Backbone. Questo motore gestisce tutti i comportamenti dinamici, come Aggiungi/Rimuovi istanze ripetibili, layout di oggetti espandibili. Questo motore di layout esegue il rendering di un modulo una pagina alla volta. Inizialmente un utente visualizza una sola pagina e la barra di scorrimento orizzontale rappresenta solo la prima pagina. Tuttavia, quando un utente scorre verso il basso, inizia il rendering della pagina successiva. Questo rendering pagina per pagina riduce il tempo necessario per eseguire il rendering della prima pagina in un browser e migliora le prestazioni percepite del modulo. Questo motore/libreria fa parte della libreria client CQ con il nome della categoria **xfaforms.profile**.

Il motore di layout contiene anche un set di widget utilizzati per acquisire il valore dei campi del modulo da un utente. Questi widget sono modellati come [Widget interfaccia utente jQuery](https://api.jqueryui.com/jQuery.widget/) che implementano alcuni contratti aggiuntivi per lavorare senza problemi con il motore Layout.

Per maggiori dettagli sui widget e i contratti corrispondenti, vedi [Widget personalizzati per moduli HTML5](/help/forms/using/introduction-widgets.md).

#### Attribuzione stile {#styling}

Lo stile associato agli elementi HTML viene aggiunto in linea o in base al blocco CSS incorporato. Alcuni stili comuni che non dipendono dalla forma fanno parte di CQ Client Lib con nome di categoria xfaforms.profile.

Oltre alle proprietà di stile predefinite, ogni elemento del modulo contiene anche alcune classi CSS basate sul tipo di elemento, il nome e altre proprietà. Utilizzando queste classi, è possibile ridefinire gli elementi specificando il proprio CSS.

Per ulteriori dettagli sullo stile e sulle classi predefinite, consulta [Introduzione agli stili](/help/forms/using/css-styles.md).

#### Script lato server e servizi Web {#server-side-script-and-web-services}

Tutti gli script contrassegnati per l&#39;esecuzione su server o contrassegnati per la chiamata a un servizio Web (indipendentemente da dove è contrassegnato per l&#39;esecuzione) vengono sempre eseguiti sul server.

Il motore di script client:

1. Effettua una chiamata sincrona al server passando lo stato del modulo corrente sotto forma di JSON
1. Esegue lo script o il servizio Web sul server
1. Genera un nuovo stato JSON
1. Unisce il nuovo stato JSON sul client quando viene restituita la risposta.

#### Bundle risorse di localizzazione {#localization-resource-bundles}

I moduli HTML5 supportano italiano (it), spagnolo (es), portoghese brasiliano (pt_BR), cinese semplificato (zh_CN), cinese tradizionale (supporto limitato) (zh_TW), coreano (ko_KR), inglese (en_US), francese (fr_FR), tedesco (de_DE) e giapponese (ja). In base alle impostazioni internazionali ricevute nell’intestazione della richiesta, al client viene inviato il bundle risorse corrispondente. Questo bundle di risorse viene aggiunto a Profile JSP as a CQ Client Lib con nome categoria **xfaforms.I18N**. È possibile ignorare la logica di prelievo del pacchetto locale nel profilo.

### Componenti Sling (adobe-lc-forms-content-pkg.zip) {#sling-components-adobe-lc-forms-content-pkg-zip}

Il pacchetto Sling contiene il contenuto relativo a Profili e Profile Renderer.

#### Profili {#profiles}

I profili sono i nodi Resource in sling che rappresentano una forma o una famiglia di Forms. A livello di CQ, questi profili sono nodi JCR. I nodi risiedono sotto il **/content** nell’archivio JCR e può trovarsi all’interno di qualsiasi sottocartella **/content** cartella.

#### Renderer di profili {#profile-renderers}

Il nodo Profilo ha una proprietà **sling:resourceSuperType** con valore **xfaforms/profile**. Questa proprietà invia internamente richieste allo script sling per i nodi di profilo che si trovano nella **/libs/xfaforms/profile** cartella. Questi script sono pagine JSP, che sono contenitori per la compilazione dei moduli HTML e gli artefatti JS/CSS richiesti. Le pagine includono riferimenti a:

* **xfaforms.I18N.&lt;locale>**: Questa libreria contiene dati localizzati.
* **xfaforms.profile**: Questa libreria contiene l&#39;implementazione per il motore di script e layout XFA.

Queste librerie sono modellate come librerie client CQ e sfruttano le funzionalità di concatenazione, minimizzazione e compressione automatiche delle librerie JavaScript del framework CQ.
Per ulteriori informazioni sulle librerie client CQ, vedi [Documentazione di CQ Clientlib](https://docs.adobe.com/docs/en/cq/current/developing/components/clientlibs.html).

Come descritto in precedenza, il modulo di rendering del profilo JSP chiama Forms Service tramite un include sling. Questo JSP imposta anche varie opzioni di debug in base alla configurazione dell&#39;amministratore o ai parametri di richiesta.

I moduli di HTML5 consentono agli sviluppatori di creare un modulo di rendering di profili e profili per personalizzare l’aspetto dei moduli. Ad esempio, i moduli di HTML consentono agli sviluppatori di integrare i moduli in un pannello o &lt;div> di un portale HTML esistente.
Per ulteriori dettagli sulla creazione di profili personalizzati, consulta [Creazione di un profilo personalizzato](/help/forms/using/custom-profile.md).
