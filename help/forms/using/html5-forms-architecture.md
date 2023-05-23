---
title: Architettura dei moduli di HTML5
seo-title: Architecture of HTML5 forms
description: I moduli HTML5 vengono distribuiti come pacchetto all’interno dell’istanza AEM incorporata e espongono la funzionalità come endpoint REST su HTTP/S utilizzando l’architettura RESTful Apache Sling.
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
source-git-commit: 4fa868f3ae4778d3a637e90b91f7c5909fe5f8aa
workflow-type: tm+mt
source-wordcount: '2011'
ht-degree: 1%

---

# Architettura dei moduli di HTML5{#architecture-of-html-forms}

## Architettura {#architecture}

La funzionalità dei moduli di HTML5 viene distribuita come pacchetto all’interno dell’istanza AEM incorporata ed è esposta come endpoint REST su HTTP/S utilizzando RESTful [Architettura Apache Sling](https://sling.apache.org/).

![02-aem-forms-architecture_large](assets/02-aem-forms-architecture_large.jpg)

### Utilizzo di Sling Framework {#using-sling-framework}

[Apache Sling](https://sling.apache.org/) è incentrato sulle risorse. Utilizza un URL di richiesta per risolvere prima la risorsa. Ogni risorsa ha un **sling:resourceType** (o **sling:resourceSuperType**). In base a questa proprietà, al metodo di richiesta e alle proprietà dell’URL della richiesta, viene quindi selezionato uno script sling per gestire la richiesta. Questo script sling può essere un JSP o un servlet. Per i moduli HTML5: **Profilo** i nodi fungono da risorse sling e **Rendering profilo** agisce da script sling che gestisce la richiesta di rendering del modulo mobile con un particolare profilo. A **Rendering profilo** è una JSP che legge i parametri da una richiesta e chiama il servizio OSGi di Forms.

Per informazioni dettagliate sull’endpoint REST e sui parametri di richiesta supportati, consulta [Rendering modello modulo](/help/forms/using/rendering-form-template.md).

Quando un utente effettua una richiesta da un dispositivo client come un browser iOS o Android™, Sling risolve prima il nodo del profilo in base all’URL della richiesta. Da questo nodo profilo, legge **sling:resourceSuperType** e **sling:resourceType** per determinare tutti gli script disponibili che possono gestire questa richiesta di rendering del modulo. Quindi utilizza i selettori di richieste Sling insieme al metodo di richiesta per identificare lo script più adatto per la gestione di questa richiesta. Una volta che la richiesta raggiunge una JSP di rendering del profilo, JSP chiama il servizio OSGi di Forms.

Per ulteriori dettagli sulla risoluzione dello script Sling, consulta [Scheda di riferimento rapido di AEM Sling](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=it) o [Scomposizione URL Apache Sling](https://sling.apache.org/documentation/the-sling-engine/url-decomposition.html).

#### Flusso di chiamata di elaborazione modulo tipico {#typical-form-processing-call-flow}

I moduli HTML5 memorizzano nella cache tutti gli oggetti intermedi necessari per elaborare (rendering o invio) un modulo alla prima richiesta. Non memorizza in cache gli oggetti dipendenti dai dati, in quanto tali oggetti potrebbero cambiare.

Mobile Form mantiene due diversi livelli di cache, PreRender cache e Render cache. La cache di preRender contiene tutti i frammenti e le immagini di un modello risolto, mentre la cache di rendering contiene contenuto renderizzato come HTML.

![Flusso di lavoro per moduli di HTML5](assets/cacheworkflow.png)

Flusso di lavoro per moduli di HTML5

I moduli HTML5 non memorizzano in cache i modelli con riferimenti mancanti di frammenti e immagini. Se i moduli di HTML5 richiedono più tempo del normale, controlla i registri del server per individuare eventuali riferimenti e avvisi mancanti. Verificare inoltre che non venga raggiunta la dimensione massima dell&#39;oggetto.

Il servizio OSGi di Forms elabora una richiesta in due passaggi:

* **Layout e generazione iniziale dello stato del modulo**: il servizio di rendering OSGi di Forms chiama il componente Cache di Forms per determinare se il modulo è già stato memorizzato in cache e non è stato invalidato. Se il modulo è memorizzato nella cache ed è valido, viene distribuito dalla cache al HTML generato. Se il modulo viene invalidato, il servizio di rendering Forms OSGi genera il layout modulo iniziale e lo stato del modulo in formato XML. Questo XML viene trasformato in layout HTML e stato iniziale del modulo JSON dal servizio Forms OSGi e quindi memorizzato nella cache per le richieste successive.
* **Forms precompilato**: durante il rendering, se un utente richiede moduli con dati precompilati, il servizio di rendering OSGi di Forms chiama il contenitore del servizio Forms e genera un nuovo stato del modulo con dati uniti. Tuttavia, poiché il layout è già generato nel passaggio precedente, questa chiamata è più veloce della prima chiamata. Questa chiamata esegue solo l’unione dei dati ed esegue gli script sui dati.

Se nel modulo sono presenti aggiornamenti o risorse utilizzate all’interno del modulo, il componente Cache modulo lo rileva e la cache per quel particolare modulo viene invalidata. Una volta completata l’elaborazione da parte del servizio OSGi di Forms, JSP aggiunge al modulo i riferimenti e lo stile della libreria JavaScript e restituisce la risposta al client. Un tipico server web come [Apache](https://httpd.apache.org/) può essere utilizzato qui con la compressione HTML attivata. Un server web ridurrebbe in modo significativo le dimensioni della risposta, il traffico di rete e il tempo necessario per lo streaming dei dati tra server e computer client.

Quando un utente invia il modulo, il browser invia lo stato del modulo in formato JSON al [invia proxy servizio](../../forms/using/service-proxy.md); quindi il proxy del servizio di invio genera un XML dati utilizzando i dati JSON e invia tale XML dati all’endpoint di invio.

## Componenti {#components}

Per abilitare HTML Forms è necessario il pacchetto del componente aggiuntivo AEM Forms. Per informazioni sull’installazione del pacchetto del componente aggiuntivo AEM Forms, consulta [Installazione e configurazione di AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md).

### Componenti OSGi (adobe-lc-forms-core.jar) {#osgi-components-adobe-lc-forms-core-jar}

**Adobe di XFA Forms Renderer (com.adobe.livecycle.adobe-lc-forms-core)** è il nome visualizzato del bundle OSGi dei moduli HTML5 visualizzato dalla vista Bundle di Felix Admin Console (https://[host]:[porta]/system/console/bundles).

Questo componente contiene componenti OSGi per le impostazioni di rendering, gestione della cache e configurazione.

#### Servizio Forms OSGi {#forms-osgi-service}

Questo servizio OSGi contiene la logica per il rendering di un XDP come HTML e gestisce l’invio di un modulo per generare l’XML dei dati. Questo servizio utilizza il contenitore del servizio Forms. Il contenitore del servizio Forms chiama internamente il componente nativo `XMLFormService.exe` che esegue l’elaborazione.

Se viene ricevuta una richiesta di rendering, questo componente chiama il contenitore del servizio Forms per generare informazioni su layout e stato che vengono ulteriormente elaborate per generare gli stati DOM dei moduli HTML e JSON.

Questo componente è anche responsabile della generazione di dati XML da JSON dello stato del modulo inviato.

#### Componente cache {#cache-component}

HTML5 forms utilizza la memorizzazione nella cache per ottimizzare la velocità effettiva e i tempi di risposta. Puoi configurare il livello del servizio cache per ottimizzare il compromesso tra prestazioni e utilizzo dello spazio.

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
   <td>Conservatore</td>
   <td>Memorizza nella cache solo gli artefatti intermedi generati prima del rendering del modulo, ad esempio il modello contenente frammenti e immagini in linea</td>
  </tr>
  <tr>
   <td>Aggressivo</td>
   <td>Memorizza contenuto HTML con rendering della cache<br /> Memorizza nella cache tutti gli artefatti memorizzati nella cache a livello conservativo.<br /> <strong>Nota</strong>: questa strategia offre prestazioni migliori, ma consuma più memoria per l’archiviazione degli artefatti memorizzati nella cache.</td>
  </tr>
 </tbody>
</table>

I moduli HTML5 eseguono il caching in memoria utilizzando la strategia LRU. Se la strategia della cache è impostata su Nessuno, la cache non verrà creata e i dati esistenti, se presenti, verranno cancellati. Oltre alla strategia di caching, puoi anche configurare la dimensione totale della cache in memoria, che può essere utile per avere la dimensione massima associata alla cache e, se va oltre, utilizzerà la modalità LRU per liberare le risorse della cache.

>[!NOTE]
>
>La cache in memoria non è condivisa tra i nodi del cluster.

#### Servizio di configurazione {#configuration-service}

Configuration Service consente di ottimizzare i parametri di configurazione e le impostazioni della cache per i moduli HTML5.

Per aggiornare queste impostazioni, vai all’Admin Console CQ Felix (disponibile all’indirizzo https://&lt;’[server]:[porta]&#39;/system/console/configMgr), cerca e seleziona Mobile Forms Configuration.

Puoi configurare la dimensione della cache o disabilitarla utilizzando il servizio di configurazione. È inoltre possibile abilitare il debug utilizzando il parametro Opzioni di debug. Ulteriori informazioni sul debug dei moduli sono disponibili all’indirizzo [Debug dei moduli di HTML5](/help/forms/using/debug.md).

### Componenti runtime (adobe-lc-forms-runtime-pkg.zip) {#runtime-components-adobe-lc-forms-runtime-pkg-zip}

Il pacchetto runtime contiene le librerie lato client utilizzate per eseguire il rendering dei moduli HTML.

**Componenti importanti disponibili come parte del pacchetto Runtime:**

#### Motore di script {#scripting-engine}

L’implementazione XFA di Adobe supporta due tipi di linguaggi di script per abilitare l’esecuzione logica definita dall’utente nei moduli: JavaScript e FormCalc.

Il motore di script di HTML Forms è scritto in JavaScript per supportare l’API di script XFA in entrambi questi linguaggi.

Al momento del rendering, lo script FormCalc viene tradotto (e memorizzato nella cache) in JavaScript sul server trasparente per l’utente o il designer.

Questo motore di script utilizza alcune funzionalità di ECMAScript5 come Object.defineProperty. Il motore o la libreria viene distribuito come libreria client CQ con il nome della categoria **xfaforms.profile**. Fornisce inoltre **API FormBridge** per abilitare i portali o le app esterni per l&#39;interazione con il modulo. Utilizzando FormBridge, un&#39;app esterna può nascondere alcuni elementi a livello di programmazione, ottenerne o impostarne i valori o modificarne gli attributi.

Per ulteriori dettagli, vedi [Bridge modulo](/help/forms/using/form-bridge-apis.md) articolo.

#### Motore di layout {#layout-engine}

Il layout e l’aspetto visivo dei moduli HTML5 si basano sulle funzioni SVG 1.1, jQuery, BackBone e CSS3. L’aspetto iniziale di un modulo viene generato e memorizzato nella cache del server. La modifica del layout iniziale e le ulteriori modifiche incrementali al layout del modulo vengono gestite sul client. Per ottenere questo risultato, il pacchetto Runtime contiene un motore di layout scritto in JavaScript e basato su jQuery/Backbone. Questo motore gestisce tutti i comportamenti dinamici, ad esempio Aggiungi/Rimuovi istanze ripetibili, layout di oggetti di crescita. Questo motore di layout esegue il rendering di un modulo una pagina alla volta. Inizialmente, un utente visualizza solo una pagina e la barra di scorrimento orizzontale tiene conto solo della prima pagina. Tuttavia, quando un utente scorre verso il basso, inizia il rendering della pagina successiva. Questa rappresentazione pagina per pagina riduce il tempo necessario per il rendering della prima pagina in un browser e migliora le prestazioni percepite del modulo. Questo motore/libreria fa parte di CQ Client Lib con il nome della categoria **xfaforms.profile**.

Il motore di layout contiene anche un set di widget utilizzati per acquisire il valore dei campi modulo da un utente. Questi widget sono modellati come [Widget interfaccia utente jQuery](https://api.jqueryui.com/jQuery.widget/) che implementano alcuni contratti aggiuntivi per funzionare senza problemi con il motore di layout.

Per maggiori dettagli sui widget e i contratti corrispondenti, vedi [Widget personalizzati per moduli HTML5](/help/forms/using/introduction-widgets.md).

#### Attribuzione stile {#styling}

Lo stile associato agli elementi HTML viene aggiunto in linea o in base al blocco CSS incorporato. Alcuni stili comuni che non dipendono dalla forma sono parte della libreria client CQ con il nome di categoria xfaforms.profile.

Oltre alle proprietà di stile predefinite, ogni elemento modulo contiene alcune classi CSS basate su tipo di elemento, nome e altre proprietà. Utilizzando queste classi, è possibile ridefinire gli elementi specificando il proprio CSS.

Per ulteriori dettagli sugli stili e le classi predefiniti, consulta [Introduzione agli stili](/help/forms/using/css-styles.md).

#### Script lato server e servizi Web {#server-side-script-and-web-services}

Tutti gli script contrassegnati per l&#39;esecuzione sul server o per la chiamata a un servizio Web (indipendentemente dalla posizione in cui è contrassegnato per l&#39;esecuzione) vengono sempre eseguiti sul server.

Il motore di script client:

1. Effettua una chiamata sincrona al server passando lo stato corrente del modulo sotto forma di JSON
1. Esegue lo script o il servizio Web sul server
1. Genera un nuovo stato JSON
1. Unisce il nuovo stato JSON sul client quando viene restituita la risposta.

#### Bundle risorse di localizzazione {#localization-resource-bundles}

I moduli HTML5 supportano la lingua italiana (it), spagnola (es), portoghese brasiliano (pt_BR), cinese semplificato (zh_CN), cinese tradizionale (solo supporto limitato) (zh_TW), coreana (ko_KR), inglese (en_US), francese (fr_FR), tedesca (de_DE) e giapponese (ja). In base alle impostazioni locali ricevute nell’intestazione della richiesta, il Bundle di risorse corrispondente viene inviato al client. Questo bundle di risorse viene aggiunto a JSP profilo come libreria client CQ con nome categoria **xfaforms.I18N**. È possibile ignorare la logica di prelievo del pacchetto delle impostazioni internazionali nel profilo.

### Componenti Sling (adobe-lc-forms-content-pkg.zip) {#sling-components-adobe-lc-forms-content-pkg-zip}

Il pacchetto Sling contiene contenuti relativi a Profili e Profile Renderer.

#### Profili {#profiles}

I profili sono i nodi Resource in Sling che rappresentano un modulo o una famiglia di Forms. A livello CQ, questi profili sono nodi JCR. I nodi si trovano sotto **/content** nell’archivio JCR e può trovarsi in qualsiasi sottocartella sotto il **/content** cartella.

#### Rendering profilo {#profile-renderers}

Il nodo Profilo ha una proprietà **sling:resourceSuperType** con valore **xfaforms/profile**. Questa proprietà invia internamente le richieste di inoltro allo script sling per i nodi di profilo che si trovano in **/libs/xfaforms/profile** cartella. Si tratta di pagine JSP, che sono contenitori per la creazione di moduli HTML e di artefatti JS/CSS richiesti. Le pagine includono riferimenti a:

* **xfaforms.I18N.&lt;locale>**: questa libreria contiene dati localizzati.
* **xfaforms.profile**: questa libreria contiene l’implementazione per il motore di script e layout XFA.

Queste librerie sono modellate come librerie client CQ e sfruttano i vantaggi della concatenazione automatica, della minimizzazione e della compressione delle librerie JavaScript del framework CQ.
Per ulteriori informazioni sulle librerie client CQ, consulta [Documentazione di CQ Clientlib](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=it).

Come descritto in precedenza, il modulo di rendering del profilo JSP chiama il servizio Forms tramite un’inclusione sling. Questa JSP imposta anche varie opzioni di debug in base alla configurazione amministratore o ai parametri di richiesta.

I moduli di HTML5 consentono agli sviluppatori di creare un profilo e un modulo di rendering dei profili per personalizzare l’aspetto dei moduli. I moduli HTML, ad esempio, consentono agli sviluppatori di integrare i moduli in un pannello o &lt;div> di un portale HTML esistente.
Per ulteriori dettagli sulla creazione di profili personalizzati, consulta [Creazione di un profilo personalizzato](/help/forms/using/custom-profile.md).
