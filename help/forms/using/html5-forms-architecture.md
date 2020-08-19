---
title: Architettura dei moduli HTML5
seo-title: Architettura dei moduli HTML5
description: I moduli HTML5 vengono distribuiti come pacchetto all’interno dell’istanza di AEM incorporata ed espone la funzionalità come punto finale REST su HTTP/S utilizzando l’architettura RESTful Apache Sling.
seo-description: I moduli HTML5 vengono distribuiti come pacchetto all’interno dell’istanza di AEM incorporata ed espone la funzionalità come punto finale REST su HTTP/S utilizzando l’architettura RESTful Apache Sling.
uuid: 7f515cea-1447-4fc7-82ba-17f2e3f9f80c
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: a644978e-5736-4771-918a-dfefe350a4a1
docset: aem65
translation-type: tm+mt
source-git-commit: 84dd0d551431169239f63cff62a015e15f998e7d
workflow-type: tm+mt
source-wordcount: '2043'
ht-degree: 0%

---


# Architettura dei moduli HTML5{#architecture-of-html-forms}

## Architettura {#architecture}

La funzionalità dei moduli HTML5 è distribuita come pacchetto all’interno dell’istanza AEM incorporata ed è esposta come punto finale REST su HTTP/S utilizzando RESTful [Apache Sling Architecture](https://sling.apache.org/).

![02-aem-forms-architecture_large](assets/02-aem-forms-architecture_large.jpg)

### Utilizzo di Sling Framework {#using-sling-framework}

[Apache Sling](https://sling.apache.org/) è incentrato sulle risorse. Utilizza un URL di richiesta per risolvere la risorsa. Ciascuna risorsa dispone di una proprietà **sling:resourceType** (o **sling:resourceSuperType**). In base a questa proprietà, al metodo di richiesta e alle proprietà dell’URL della richiesta, viene quindi selezionato uno script sling per gestire la richiesta. Questo script sling può essere un JSP o un servlet. Per i moduli HTML5, i nodi **Profilo** fungono da risorse sling e il modulo di rendering dei **profili** funge da script sling che gestisce la richiesta di rendering del modulo mobile con un profilo particolare. Un renderer di **profilo** è un JSP che legge i parametri da una richiesta e chiama il servizio Forms OSGi.

Per informazioni dettagliate sull&#39;endpoint REST e sui parametri di richiesta supportati, consultate Modello [per moduli di](/help/forms/using/rendering-form-template.md)rendering.

Quando un utente effettua una richiesta da un dispositivo client come un browser iOS o Android, Sling risolve prima il nodo del profilo in base all&#39;URL della richiesta. Da questo nodo di profilo si legge **sling:resourceSuperType** e **sling:resourceType** per determinare tutti gli script disponibili che possono gestire questa richiesta di rendering del modulo. Quindi utilizza i selettori di richieste Sling insieme al metodo di richiesta per identificare lo script più adatto per gestire questa richiesta. Quando la richiesta raggiunge un JSP di rendering profilo, il JSP chiama il servizio Forms OSGi.

Per ulteriori dettagli sulla risoluzione dello script Sling, vedere [AEM Sling Cheat Sheet](https://docs.adobe.com/content/docs/en/cq/current/developing/sling_cheatsheet.html) o [Apache Sling Url decomposizione](https://sling.apache.org/site/url-decomposition.html).

#### Flusso di chiamate di elaborazione dei moduli tipico {#typical-form-processing-call-flow}

I moduli HTML5 memorizzano nella cache tutti gli oggetti intermedi necessari per elaborare (rendering o invio) un modulo alla prima richiesta. Non memorizza nella cache gli oggetti dipendenti dai dati in quanto tali oggetti potrebbero essere modificati.

Mobile Form mantiene due diversi livelli di cache, cache PreRender e cache di rendering. La cache preRender contiene tutti i frammenti e le immagini di un modello risolto e la cache di rendering contiene il contenuto di cui è stato effettuato il rendering, ad esempio HTML.

![Flusso di lavoro per moduli HTML5](assets/cacheworkflow.png)

Flusso di lavoro per moduli HTML5

I moduli HTML5 non memorizzano nella cache i modelli con riferimenti di frammenti e immagini mancanti. Se i moduli HTML5 richiedono più tempo del normale, controllate che nei registri del server siano presenti riferimenti e avvisi mancanti. Inoltre, verificare che la dimensione massima dell&#39;oggetto non sia raggiunta.

Il servizio Forms OSGi elabora una richiesta in due passaggi:

* **Generazione** di layout e stato modulo iniziale: Il servizio di rendering Forms OSGi chiama il componente Forms Cache per determinare se il modulo è già stato memorizzato nella cache e non è stato invalidato. Se il modulo è memorizzato nella cache e valido, viene distribuito l&#39;HTML generato dalla cache. Se il modulo viene invalidato, il servizio di rendering Forms OSGi genera il layout iniziale del modulo e lo stato del modulo in formato XML. Il codice XML viene trasformato in layout HTML e stato iniziale del modulo JSON dal servizio Forms OSGi, quindi memorizzato nella cache per richieste successive.
* **Forms** prepopolato: Durante il rendering, se un utente richiede moduli con dati precompilati, il servizio di rendering Forms OSGi chiama il contenitore del servizio Forms e genera un nuovo stato Modulo con dati uniti. Tuttavia, poiché il layout è già generato nel passaggio precedente, questa chiamata è più veloce della prima. Questa chiamata esegue solo l&#39;unione dei dati ed esegue gli script sui dati.

Se è presente un aggiornamento del modulo o di risorse utilizzate all’interno del modulo, il componente cache del modulo lo rileva e la cache del modulo specifico viene invalidata. Una volta completata l&#39;elaborazione del servizio Forms OSGi, il modulo di rendering dei profili jsp aggiunge riferimenti e stili di libreria JavaScript al modulo e restituisce la risposta al client. Un server Web tipico come [Apache](https://httpd.apache.org/) può essere utilizzato qui con la compressione HTML attivata. Un server Web ridurrebbe notevolmente le dimensioni di risposta, il traffico di rete e il tempo necessario per lo streaming dei dati tra il server e il computer client.

Quando un utente invia il modulo, il browser invia lo stato del modulo in formato JSON al proxy [del servizio di](../../forms/using/service-proxy.md)invio; quindi il proxy del servizio di invio genera un XML di dati utilizzando i dati JSON e invia l&#39;XML di dati per inviare l&#39;endpoint.

## Componenti {#components}

Per abilitare i moduli HTML5 è necessario  pacchetto aggiuntivo AEM Forms. Per informazioni sull&#39;installazione  pacchetto aggiuntivo AEM Forms, consultate [Installazione e configurazione  AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md).

### Componenti OSGi (adobe-lc-forms-core.jar) {#osgi-components-adobe-lc-forms-core-jar}

**Adobe XFA Forms Renderer (com.adobe.livecycle.adobe-lc-forms-core)** è il nome visualizzato del bundle OSGi moduli HTML5 visualizzato da Bundle View of Felix admin console (https://[host]:[port]/system/console/bundle).

Questo componente contiene componenti OSGi per le impostazioni di rendering, gestione cache e configurazione.

#### Forms OSGi Service {#forms-osgi-service}

Questo servizio OSGi contiene la logica per eseguire il rendering di un XDP come HTML e gestisce l&#39;invio di un modulo per generare dati XML. Questo servizio utilizza il contenitore del servizio Forms. Il contenitore del servizio Forms chiama internamente il componente nativo `XMLFormService.exe` che esegue l’elaborazione.

Se viene ricevuta una richiesta di rendering, questo componente chiama il contenitore del servizio Forms per generare informazioni di layout e stato ulteriormente elaborate per generare stati DOM modulo HTML e JSON.

Questo componente è inoltre responsabile della generazione di dati XML da JSON (stato modulo inviato).

#### Componente cache {#cache-component}

I moduli HTML5 utilizzano la cache per ottimizzare il throughput e il tempo di risposta. Potete configurare il livello del servizio cache per ottimizzare il bilanciamento tra prestazioni e utilizzo dello spazio.

<table>
 <tbody>
  <tr>
   <th>Strategia cache</th>
   <th>Descrizione</th>
  </tr>
  <tr>
   <td>Nessuno</td>
   <td>Non memorizzare gli artefatti nella cache<br /> </td>
  </tr>
  <tr>
   <td>Conservatore</td>
   <td>Memorizza nella cache solo gli artefatti intermedi generati prima del rendering del modulo come il modello contenente frammenti e immagini in linea</td>
  </tr>
  <tr>
   <td>Aggressivo</td>
   <td>Memorizza nella cache tutti gli artefatti memorizzati nella cache a livello di conservatore.<br /><br /> <strong>Nota</strong>: Questa strategia offre prestazioni ottimali, ma consuma più memoria per memorizzare gli artefatti memorizzati nella cache.</td>
  </tr>
 </tbody>
</table>

I moduli HTML5 eseguono il caching in memoria utilizzando la strategia LRU. Se la strategia della cache è impostata su Nessuna cache non verrà creata e gli eventuali dati della cache esistenti verranno cancellati. Oltre alla strategia di caching, è anche possibile configurare la dimensione totale della cache in memoria che può aiutare ad avere il limite massimo sulla dimensione della cache e se va oltre, utilizzerà la modalità LRU per liberare le risorse della cache.

>[!NOTE]
>
>La cache in memoria non è condivisa tra i nodi del cluster.

#### Servizio di configurazione {#configuration-service}

Il servizio di configurazione consente di sintonizzare i parametri di configurazione e le impostazioni della cache per i moduli HTML5.

Per aggiornare queste impostazioni, andate all&#39;Admin Console di CQ Felix  (disponibile all&#39;indirizzo https://&lt;&#39;[server]:[port]&#39;/system/console/configMgr), cercate e selezionate Configurazione Forms mobile.

È possibile configurare la dimensione della cache o disabilitare la cache utilizzando il servizio di configurazione. Potete inoltre abilitare il debug utilizzando il parametro Opzioni di debug. Per ulteriori informazioni sul debug dei moduli, vedere [Debug di moduli](/help/forms/using/debug.md)HTML5.

### Componenti runtime (adobe-lc-forms-runtime-pkg.zip) {#runtime-components-adobe-lc-forms-runtime-pkg-zip}

Il pacchetto Runtime contiene le librerie lato client utilizzate per il rendering dei moduli HTML.

**Componenti importanti disponibili come parte del pacchetto Runtime:**

#### Motore di scripting {#scripting-engine}

&#39;implementazione XFA di Adobe supporta due tipi di linguaggi di script per consentire l&#39;esecuzione logica definita dall&#39;utente nei moduli: JavaScript e FormCalc.

Il motore di script di HTML Forms è scritto in JavaScript per supportare l&#39;API di script XFA in entrambi i linguaggi.

Al momento del rendering, lo script FormCalc viene convertito (e memorizzato nella cache) in JavaScript sul server e reso trasparente per l&#39;utente o il progettista.

Questo motore di scripting utilizza alcune delle funzioni di ECMAScript5 come Object.defineProperty. Il motore/libreria viene distribuito come CQ Client Lib con il nome della categoria **xfaforms.profile**. Fornisce inoltre l&#39;API **** FormBridge per consentire l&#39;interazione con i moduli da parte di portali o app esterne. Con FormBridge, un&#39;app esterna può nascondere in modo programmatico alcuni elementi, ottenerne o impostarne i valori o modificarne gli attributi.

Per ulteriori dettagli, vedere l&#39;articolo [Form Bridge](/help/forms/using/form-bridge-apis.md) .

#### Motore di layout {#layout-engine}

Il layout e l’aspetto visivo dei moduli HTML5 si basano sulle funzioni SVG 1.1, jQuery, BackBone e CSS3. L&#39;aspetto iniziale di un modulo viene generato e memorizzato nella cache del server. Il tweaking di tale layout iniziale e di eventuali ulteriori modifiche incrementali al layout del modulo vengono gestiti sul client. A tal fine, il pacchetto Runtime contiene un motore di layout scritto in JavaScript e basato su jQuery/Backbone. Questo motore gestisce tutti i comportamenti dinamici, come Aggiungi/Rimuovi istanze ripetibili, layout oggetto espandibile. Questo modulo di gestione del layout esegue il rendering di un modulo una pagina alla volta. Inizialmente un utente visualizza solo una pagina e la barra di scorrimento orizzontale rappresenta solo la prima pagina. Tuttavia, quando un utente scorre verso il basso, la pagina successiva avvia il rendering. Questa rappresentazione pagina per pagina riduce il tempo necessario per eseguire il rendering della prima pagina in un browser e migliora le prestazioni percepite del modulo. Questo motore/libreria fa parte di CQ Client Lib con il nome della categoria **xfaforms.profile**.

Il motore di layout contiene anche un set di widget utilizzati per acquisire il valore dei campi del modulo da un utente. Questi widget sono modellati come Widget [interfaccia utente](https://api.jqueryui.com/jQuery.widget/) jQuery che implementano alcuni contratti aggiuntivi per lavorare senza problemi con il motore di layout.

Per ulteriori dettagli sui widget e i contratti corrispondenti, vedere Widget [personalizzati per i moduli](/help/forms/using/introduction-widgets.md)HTML5.

#### Attribuzione stile {#styling}

Lo stile associato agli elementi HTML viene aggiunto in linea o basato su un blocco CSS incorporato. Alcuni stili comuni che non dipendono dal modulo fanno parte di CQ Client Lib con nome categoria xfaforms.profile.

Oltre alle proprietà di stile predefinite, ogni elemento del modulo contiene anche alcune classi CSS basate su tipo di elemento, nome e altre proprietà. Utilizzando queste classi, è possibile ridefinire gli elementi specificando il proprio CSS.

Per ulteriori dettagli sullo stile e sulle classi predefinite, vedere [Introduzione agli stili](/help/forms/using/css-styles.md).

#### Script lato server e servizi Web {#server-side-script-and-web-services}

Tutti gli script contrassegnati per l&#39;esecuzione sul server o contrassegnati per chiamare un servizio Web (indipendentemente da dove è contrassegnato per l&#39;esecuzione) vengono sempre eseguiti sul server.

Il motore di script client:

1. Effettua una chiamata sincrona al server passando lo stato del modulo corrente sotto forma di JSON
1. Esegue lo script o il servizio Web sul server
1. Genera un nuovo stato JSON
1. Unisce il nuovo stato JSON sul client quando viene restituita la risposta.

#### Bundle risorse di localizzazione {#localization-resource-bundles}

I moduli HTML5 supportano italiano (it), spagnolo (es), portoghese brasiliano (pt_BR), cinese semplificato (zh_CN), cinese tradizionale (solo supporto limitato) (zh_TW), coreano (ko_KR), inglese (en_US), francese (fr_FR), tedesco (de_DE) e giapponese (ja). In base alle impostazioni internazionali ricevute nell’intestazione della richiesta, il pacchetto di risorse corrispondente viene inviato al client. Questo pacchetto di risorse viene aggiunto a Profile JSP come CQ Client Lib con nome categoria **xfaforms.I18N**. Potete ignorare la logica di prelievo del pacchetto di impostazioni internazionali nel profilo.

### Componenti Sling (adobe-lc-forms-content-pkg.zip) {#sling-components-adobe-lc-forms-content-pkg-zip}

Il pacchetto Sling contiene il contenuto correlato a Profili e Modulo di rendering profilo.

#### Profili {#profiles}

I profili sono i nodi delle risorse in sling che rappresentano una maschera o una famiglia di Forms. A livello di CQ, questi profili sono nodi JCR. I nodi risiedono nella cartella **/content** dell’archivio JCR e possono trovarsi all’interno di qualsiasi sottocartella all’interno della cartella **/content** .

#### Modulo di rendering profili {#profile-renderers}

Il nodo Profile ha una proprietà **sling:resourceSuperType** con valori **xfaforms/profile**. Questa proprietà invia internamente richieste allo script sling per i nodi Profilo che si trovano nella cartella **/libs/xfaforms/profile** . Questi script sono pagine JSP, che sono contenitori per l&#39;assemblaggio dei moduli HTML e degli artefatti JS/CSS richiesti. Le pagine contengono riferimenti a:

* **xfaforms.I18N.&lt;locale>**: Questa libreria contiene dati localizzati.
* **xfaforms.profile**: Questa libreria contiene l&#39;implementazione per il motore XFA Scripting e Layout.

Queste librerie sono modellate come CQ Client Libraries e sono caratterizzate dalle funzionalità di concatenazione, riduzione e compressione automatiche delle librerie JavaScript del framework CQ.
Per ulteriori informazioni sulle librerie client CQ, consulta la documentazione [](https://docs.adobe.com/docs/en/cq/current/developing/components/clientlibs.html)CQ Clientlib.

Come descritto in precedenza, il renderer di profili JSP chiama Forms Service tramite una sling include. Questa JSP imposta anche diverse opzioni di debug in base alla configurazione dell&#39;amministratore o ai parametri di richiesta.

I moduli HTML5 consentono agli sviluppatori di creare il modulo di rendering dei profili e di personalizzarne l&#39;aspetto. Ad esempio, i moduli HTML consentono agli sviluppatori di integrare moduli in un pannello o nella sezione &lt;div> di un portale HTML esistente.
Per ulteriori dettagli sulla creazione di profili personalizzati, consultate [Creazione di un profilo](/help/forms/using/custom-profile.md)personalizzato.
