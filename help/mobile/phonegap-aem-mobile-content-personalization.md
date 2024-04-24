---
title: Personalizzazione dei contenuti Adobe Experience Manager Mobili
description: Segui questa pagina per scoprire Adobe della funzione di personalizzazione dei contenuti per dispositivi mobili Experience Manager (AEM) che consente agli autori dell’AEM di personalizzare i contenuti delle app mobili utilizzando Adobe Target.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 70d7ee0d-2f6d-4f97-a6e2-b02d84a0ca42
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2571'
ht-degree: 1%

---

# Personalizzazione dei contenuti AEM Mobile{#aem-mobile-content-personalization}

>[!NOTE]
>
>L’Adobe consiglia di utilizzare l’Editor SPA per i progetti che richiedono il rendering lato client basato su framework di applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Questo documento fa parte del [Guida introduttiva ad AEM Mobile](/help/mobile/getting-started-aem-mobile.md) Guida di, punto di partenza consigliato per AEM Mobile.

La funzione di personalizzazione dei contenuti di AEM Mobile consente [Autori AEM](#author) per personalizzare il contenuto delle app mobili utilizzando [Adobe Target](https://business.adobe.com/it/products/target/adobe-target.html). Ciò consente di fornire offerte mirate agli utenti delle app mobili. Adobe Experience Manager Mobili consente di creare, indirizzare e distribuire contenuti specifici per i singoli gusti.

In AEM, affinché gli autori possano iniziare a creare questo contenuto, gli amministratori e gli sviluppatori devono prima preparare l’ambiente.

[Amministratori AEM](#administrator) sono necessarie per stabilire una connessione tra AEM Mobile e il Cloud Service Adobe Target.

Nel frattempo, AEM Mobile [sviluppatori](#developer) devono modificare gli script esistenti per facilitare l’authoring mirato dei contenuti.

## Per gli amministratori {#for-administrators}

Ci sono diversi passaggi che devono essere messi insieme prima che gli autori dei contenuti possano iniziare a generare contenuti mirati per le app mobili: è possibile ottenere il set giusto di autorizzazioni per utenti e gruppi, creare servizi cloud, configurare l’applicazione per l’attività e infine generare il contenuto.

Questo articolo ti guida attraverso il processo utilizzato per configurare [Applicazione di riferimento ibrida AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) per il targeting.

Si presume che l’applicazione di riferimento ibrida AEM Mobile sia stata distribuita correttamente e sia accessibile tramite il dashboard di AEM Mobile.

Prima che gli autori possano generare contenuti mirati all’interno di un’applicazione, l’istanza AEM deve essere [configurato con il Cloud Service Adobe Target.](/help/mobile/aem-mobile-configuring-cloud-service.md)

### Autorizzazioni {#permissions}

Gli utenti che hanno bisogno di accedere alla console di personalizzazione devono far parte della `target-activity-authors` gruppo.

Nell’ambito della configurazione di utenti e gruppi, si consiglia di aggiungere il gruppo target-attività-group al gruppo apps-admins. Aggiungendo il gruppo target-activity-authors, gli utenti potranno visualizzare la voce del menu di navigazione Personalizzazione.

>[!NOTE]
>
>Se si dimentica di aggiungere gli utenti o i gruppi ai quali si desidera concedere l’accesso all’Admin Console di personalizzazione, il gruppo target-activity-authors non sarà in grado di visualizzare la console di personalizzazione.

### Servizi cloud {#cloud-services}

Per ottenere contenuti mirati che funzionano per le app mobili, è necessario configurare due servizi: il servizio Adobe Target e il servizio Adobe Mobile Services. Il servizio Adobe Target fornisce il motore per elaborare le richieste dei client e restituire il contenuto personalizzato. Il servizio Adobe Mobile Services fornisce la connessione tra i servizi Adobe e l’app mobile tramite il file ADBMobileConfig.json, utilizzato dal plug-in Cordova di AMS. Dal dashboard di AEM Mobile, puoi configurare l’applicazione aggiungendo i due servizi.

Dal dashboard di AEM Mobile, individua il Cloud Service Gestisci e fai clic sul pulsante +.

![chlimage_1-38](assets/chlimage_1-38.png)

Dalla procedura guidata Aggiungi Cloud Service, seleziona la scheda del servizio cloud &quot;Adobe Target&quot; e fai clic su Avanti.

![chlimage_1-39](assets/chlimage_1-39.png)

Dal menu a discesa Seleziona una configurazione, puoi creare una configurazione o selezionarne una esistente. Per creare una configurazione, seleziona &quot;Crea configurazione&quot; dal menu a discesa. Immetti un titolo per la configurazione Target. Immetti il codice cliente, l&#39;e-mail e la password associati al tuo account Target. Se non conosci i valori per questi campi, contatta il supporto Adobe Target. Fai clic sul pulsante &quot;Verifica&quot; per convalidare le credenziali. Una volta verificato, fai clic sul pulsante Invia per creare il servizio cloud.

>[!NOTE]
>
>Il servizio cloud creato viene associato automaticamente all’app mobile tramite la procedura guidata. Il valore della proprietà cq:cloudserviceconfigs viene impostato sul nodo jcr:content del nodo del gruppo apps. Per l’esempio di app ibrida, viene impostato su /content/mobileapps/hybrid-reference-app/jcr:content con il valore che punta al nodo del framework generato automaticamente in /etc/cloudservices/testandtarget/adobe-target—aem-apps/framework. Il nodo del framework ha due proprietà impostate per impostazione predefinita: genere ed età. Il framework viene utilizzato solo dall’anteprima AEM e non ha alcun impatto sul dispositivo.

Al termine della procedura guidata, il riquadro Gestisci Cloud Service contiene il servizio cloud Target. Tuttavia, contiene un avviso relativo a un account Adobe Mobile Services mancante.

![chlimage_1-40](assets/chlimage_1-40.png)

### Adobe Mobile Services {#adobe-mobile-services}

È necessario collegare un account Adobe Mobile Services (AMS) anche all’applicazione, il servizio AMS fornisce il file ADBMobileConfig.json richiesto che contiene le informazioni sul codice client di Target. Prima di creare un&#39;associazione con l&#39;account AMS, l&#39;account AMS deve essere modificato da un utente che dispone di autorizzazioni per AMS.

### Codice cliente {#client-code}

Per accedere ai servizi AMS, visita [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/), seleziona l’app mobile e fai clic sulle impostazioni. Individua il campo Opzioni SDK Target, inserisci il codice client nel campo e fai clic su Salva.

![chlimage_1-41](assets/chlimage_1-41.png)

Ora che il codice client è stato associato all’app mobile, quando il servizio cloud AMS è configurato tramite l’Adobe Dashboard per dispositivi mobili, le impostazioni del servizio verranno distribuite tramite il file ADBMobileConfig.json.

### Cloud Service Adobe Mobile Services {#adobe-mobile-service-cloud-service}

Ora che AMS è configurato, è necessario associare l’applicazione mobile all’Adobe Dashboard di Mobile. Dal dashboard di AEM Mobile, individua il Cloud Service Gestisci e fai clic sul pulsante +.

![chlimage_1-42](assets/chlimage_1-42.png)

Seleziona la scheda Adobe Mobile Services e fai clic su Avanti.

![chlimage_1-43](assets/chlimage_1-43.png)

Dal passaggio della procedura guidata Crea o seleziona, seleziona il menu a discesa Mobile Service, quindi seleziona la voce Create Configuration (Crea configurazione). Fornisci titolo, società, nome utente, password e seleziona il centro dati appropriato. Se non conosci questi valori, contatta l’amministratore di Adobe Mobile Services per ottenerli. Dopo aver compilato tutti i campi, fai clic su **Verifica**. Il processo di verifica passa ad AMS e verifica le credenziali per l’account. Una volta completata la convalida, viene popolato un elenco di applicazioni mobili in cui si seleziona l’app mobile associata dal menu a discesa. Clic **Invia** per completare la procedura guidata. Il processo può richiedere un po’ di tempo per ottenere i dati di configurazione ed eventuali analisi associate all’applicazione. Al termine del processo, fai clic su **Fine** per tornare alla dashboard di Adobe Mobile.

Tornando al dashboard di Mobile, la sezione Gestione Cloud Service contiene il servizio cloud AMS. Inoltre, il riquadro Analizza metriche è compilato con i rapporti sul ciclo di vita.

![chlimage_1-44](assets/chlimage_1-44.png)

## Per autori {#for-authors}

**Prerequisito:** Come accennato in precedenza, gli amministratori devono configurare la connessione al servizio Adobe Target prima che gli autori possano generare nuovi contenuti mirati.

Dopo che l’amministratore ha configurato i due servizi cloud e lo sviluppatore ha configurato il gestore mobileapffers, gli autori di contenuto possono ora iniziare a generare esperienze mirate.

L’authoring di contenuti di destinazione all’interno di un’app AEM Mobile segue una procedura simile all’authoring di AEM Sites:

Consulta qui per una panoramica completa su [Creazione di contenuti mirati nell’AEM](/help/sites-authoring/personalization.md)

## Per sviluppatori {#for-developers}

Gli sviluppatori AEM che creano applicazioni mobili devono continuare a seguire i pattern comunemente utilizzati nell’AEM per lo sviluppo di componenti. In questo Adobe vengono descritti i passaggi necessari per consentire agli autori di contenuto di creare contenuti mirati:

### Gestori ContentSync di Adobe Target {#adobe-target-contentsync-handlers}

Per distribuire contenuti al dispositivo dell’utente, il contenuto viene generato eseguendo il rendering delle offerte create dagli autori di contenuti AEM. Per gestire il rendering delle offerte target, è disponibile un nuovo gestore di sincronizzazione dei contenuti che elabora le offerte. Utilizzando come esempio l’applicazione di riferimento ibrida, il pacchetto di contenuti en (inglese) contiene ContentSyncConfig con un [mobileapffffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) handler. Il passaggio successivo è fondamentale per il rendering delle offerte al dispositivo. Il gestore mobileapffers dispone di una proprietà path che identifica il percorso dell&#39;attività di personalizzazione da utilizzare per l&#39;applicazione.

Ad esempio, se è presente un’attività in */content/campaigns/hybridref*, copia questo percorso e incollalo come valore in *percorso* proprietà del gestore mobileapffers.

>[!NOTE]
>
>Per l’applicazione di riferimento ibrida, sono disponibili due gestori di offerte mobili, uno per lo sviluppo e uno per le produzioni.

Dopo aver impostato il percorso delle attività nella proprietà path del gestore mobileapffers, salva il gestore. Il gestore è ora pronto per iniziare a eseguire il rendering delle offerte per dispositivi mobili.

### Modalità rendering {#render-mode}

Il gestore mobileapffers è configurato in modo diverso per le impostazioni di pubblicazione e sviluppo. Per le impostazioni di pubblicazione è disponibile una proprietà denominata *renderMode* con un valore di *pubblicare* impostata sul nodo cq:ContentSyncConfig. Il gestore mobileapffers fa riferimento al renderMode e, se impostato su publish, modifica l’ID mbox creato. Per impostazione predefinita, alle mbox create dall’AEM viene aggiunto un valore —author all’ID mbox. Questo identifica che l’attività non è stata pubblicata e deve utilizzare la campagna non pubblicata per le risoluzioni delle offerte.

Quando il contenuto viene gestito tramite l’Adobe Mobile Dashboard, il contenuto gestito viene considerato pronto per la produzione e ne viene eseguito il rendering tramite la configurazione di sincronizzazione contenuti non di sviluppo. Se si esegue il rendering in questo modo, l’autore —author verrà rimosso da tutti gli ID mbox e si prevede che un’attività pubblicata sia disponibile sul server Target. Prima di testare il contenuto con staging, assicurati che l’attività sia già pubblicata.

### Sviluppo di app di personalizzazione {#personalization-app-development}

#### Componenti {#components}

La base per qualsiasi contenuto è in genere un componente pagina che estende uno dei componenti di base della pagina AEM wcm/foundation/components/page o foundation/components/page a seconda che si utilizzino HTL o JSP. La durata di questi passaggi si concentra sull’utilizzo del componente wcm/foundation/components/page. La struttura di base del componente Pagina è suddivisa in più script e ogni script fornisce lo scopo specifico di consentire allo sviluppatore di organizzare e sovrascrivere il codice, se necessario. I due script di interesse per la personalizzazione sono head.html e body.html. Questi due script forniscono un’area in cui è possibile inserire il codice per supportare l’hub di contesto, i Cloud Service e l’authoring mobile.

Ecco una panoramica dei due script principali utilizzati per abilitare il targeting dei contenuti.

#### head.html {#head-html}

Per consentire all’autore di eseguire il targeting del proprio contenuto, è necessario aggiungere alla pagina il menu di destinazione in modo che l’autore possa passare dalla modalità di modifica alla modalità di targeting. Per abilitare questa funzione, lo sviluppatore deve modificare lo script head.html in modo da includere il seguente frammento di codice nella parte superiore di head.html o in prossimità della &lt;title>&lt;/title> possibile.

```xml
<meta data-sly-test="${!wcmmode.disabled}">
    <div data-sly-call="${clientLib.all @ categories='personalization.kernel'}" data-sly-unwrap></div>
    <div data-sly-resource="${'config' @ resourceType='cq/personalization/components/clientcontext_optimized/config'}" data-sly-unwrap></div>
    <div data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}" data-sly-unwrap></div>
</meta>
```

>[!NOTE]
>
>Includi lo script solo quando la modalità WCM è disabilitata in modo che, quando la modalità WCM è disabilitata (per informazioni dettagliate, consulta la sezione del gestore ContentSync), lo script non viene incluso nel codice finale dell’applicazione.

Per consentire agli autori di visualizzare in anteprima il contenuto di destinazione, l’editor deve essere in grado di individuare la configurazione del servizio cloud Adobe Target. Il blocco di codice seguente aggiunge due script importanti. La prima aggiunta della possibilità per la pagina di individuare il servizio cloud Target associato ed effettuare le chiamate ad Adobe Target. La seconda è l’aggiunta della categoria cq.apps.targeting.

Il **cq.apps.targeting** la categoria sostituisce il componente predefinito cq/personalization/component/target e utilizza il componente mobileapps/components/target che esegue il rendering delle offerte specifico per il consumo di applicazioni mobili. Maggiori dettagli al riguardo saranno discussi nella sezione Componente Target.

Il codice deve essere aggiunto nel file head.html e posizionato immediatamente prima della fine del file &lt;/head> elemento.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-include="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" data-sly-unwrap></div>
    <meta data-sly-call="${clientLib.all @ categories='cq.apps.targeting'}" data-sly-unwrap></meta>
</div>
```

>[!NOTE]
>
>Il blocco di codice viene racchiuso all’interno di una modalità WCM che non viene disabilitata, pertanto viene riprodotto solo mentre l’autore di contenuto sta lavorando alla creazione di contenuto. Gli script del servizio cloud non vengono aggiunti al codice runtime mobile generato.

#### body.html {#body-html}

Per consentire all’autore del contenuto di testare utenti tipo diversi, lo script body.html deve includere il seguente blocco di codice come primo elemento secondario dell’elemento body.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'clientcontext' @ resourceType='cq/personalization/components/clientcontext_optimized'}" data-sly-unwrap></div>
</div>
```

L&#39;ultimo bit di codice richiesto si trova nella parte inferiore di body.html. Questo bit di codice cerca il servizio cloud associato e inserisce il codice del motore di targeting appropriato.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'cloudservices' @ resourceType='cq/cloudserviceconfigs/components/servicecomponents'}" data-sly-unwrap></div>
</div>
```

### Applicazione di riferimento {#reference-application}

Esempi di head.html e body.html sono disponibili nella [Applicazione di riferimento ibrida AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) mostrare allo sviluppatore dove inserire i blocchi di script all’interno dei due script.

### Gestori di sincronizzazione contenuti {#content-sync-handlers}

Una volta completata la creazione del contenuto per l’app mobile, il passaggio successivo consiste nel scaricare l’origine e creare l’applicazione oppure pubblicare il contenuto nell’area intermedia. Ci sono diversi passaggi con cui lo sviluppatore è coinvolto per rendere questo accade. Per facilitare il rendering del contenuto, AEM Mobile utilizza gestori di sincronizzazione dei contenuti per eseguire il rendering e creare pacchetti del contenuto. È stato introdotto un nuovo gestore di sincronizzazione dei contenuti per il caso di utilizzo Personalizzazione per eseguire il rendering di contenuti di destinazione. Il gestore &quot;mobileapffers&quot; è in grado di eseguire il rendering delle offerte target associate create dall’autore di contenuto. Il gestore mobileapffers estende il gestore di aggiornamento delle pagine astratte pertanto, molte delle proprietà sono simili. I dettagli del gestore mobileappoffers hanno le seguenti proprietà.

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Valore</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>riscrivere</td>
   <td>+ relativeParentPath<p> - "/"</p> </td>
   <td>La proprietà rewrite identifica il modo in cui i percorsi all’interno del contenuto devono essere riscritti.</td>
  </tr>
  <tr>
   <td>includedPageTypes</td>
   <td><p>"cq/personalization/components/teaserpage",</p> <p>"cq/personalization/components/offerproxy"</p> </td>
   <td>La proprietà includePageTypes è facoltativa e utilizza per impostazione predefinita le pagine con tipi di risorse cq/personalization/components/teaserpage e cq/personalization/components/offerproxy. Questi due tipi di risorse sono i tipi di risorse predefiniti utilizzati per il targeting del contenuto. Se è necessario supportare tipi di risorse aggiuntivi, aggiungili all’elenco di includePageTypes.</td>
  </tr>
  <tr>
   <td>locationRoot</td>
   <td>/content/mobileapps/&lt;app&gt;</td>
   <td>Posizione dell’app.</td>
  </tr>
  <tr>
   <td>tipo</td>
   <td>mobileapffffers</td>
   <td>Il nome del gestore mobileapffers.</td>
  </tr>
  <tr>
   <td>selettore</td>
   <td>tandt</td>
   <td>Il selettore del colore viene utilizzato per eseguire il rendering del contenuto di destinazione. </td>
  </tr>
  <tr>
   <td>targetRootDirectory</td>
   <td>www</td>
   <td>La directory principale in cui rendere persistente il contenuto sottoposto a rendering.</td>
  </tr>
  <tr>
   <td>includeImages</td>
   <td>true | false</td>
   <td>Se true, verrà eseguito il rendering di qualsiasi immagine inclusa nell’offerta. Se false, le immagini vengono ignorate.</td>
  </tr>
  <tr>
   <td>includeVideos</td>
   <td>true | false</td>
   <td>Se true, verrà eseguito il rendering di tutti i video inclusi nell’offerta. Se false, i video vengono ignorati.</td>
  </tr>
  <tr>
   <td>percorso</td>
   <td>/content/campaigns/&lt;brand&gt;</td>
   <td>Indica il marchio della campagna a cui partecipano le offerte. Attualmente tutte le offerte devono provenire dalla stessa campagna.</td>
  </tr>
  <tr>
   <td>profondo</td>
   <td>true | false</td>
   <td>Se true esegue il rendering ricorsivo di tutte le pagine figlie, se false non viene ripetuto. </td>
  </tr>
  <tr>
   <td>estensione</td>
   <td>html</td>
   <td>Imposta l'estensione per la risorsa di cui viene eseguito il rendering. Imposta su html in modo che le pagine abbiano estensione .html.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Il [App di riferimento ibrida AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) ha la configurazione predefinita del gestore mobileappoffer. La proprietà percorso nell’esempio è vuota in quanto dipende dalla posizione della campagna. Dopo che un autore di Campaign ha creato una campagna, l’amministratore delle app deve associare la campagna al gestore specificando la proprietà path per puntare alla campagna.

### Componente di destinazione {#target-component}

Per facilitare il rendering dei contenuti specifici per le app mobili, AEM Mobile utilizza il componente mobileapps/components/target. Il componente mobile di destinazione estende il componente cq/personalization/components/target e sostituisce lo script engine_tnt.jsp. Eseguendo l’override di engine_tnt.jsp, AEM Mobile può controllare le HTML generate per il caso d’uso delle app mobili. Per ogni componente di destinazione di un autore di contenuti, viene creata una mbox associata da engine_tnt.jsp.

Per ogni mbox, un attributo di **cq-targeting** è stato aggiunto per consentire agli sviluppatori di applicazioni di scrivere codice personalizzato da utilizzare e utilizzare come preferiscono. Il [App di riferimento ibrida AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) Esempio di Angular di direttiva che utilizza l&#39;attributo cq-targeting. Il concetto di sostituzione dei contenuti, quando e come viene effettuato, dipende dallo sviluppatore dell’app mobile. L’SDK di Mobile viene fornito tramite AEM /etc/clientlibs/mobileapps/js/mobileapps.js, che fornisce un’API per chiamare il servizio di targeting degli Adobi. Spetta allo sviluppatore dell’applicazione specificare quando tale chiamata deve essere effettuata in base alla progettazione dell’applicazione.

## Quali sono le prossime novità? {#what-s-next}

1. [Avvia la mia esperienza con l’app AEM Mobile](/help/mobile/starting-aem-phonegap-app.md)
1. [Gestire il contenuto dell’app](/help/mobile/phonegap-manage-app-content.md)
1. [Genera la mia applicazione](/help/mobile/building-app-mobile-phonegap.md)
1. [Monitora le prestazioni dell’app con Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Distribuire un’esperienza app personalizzata con Adobe Target](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [Invia messaggi importanti agli utenti](/help/mobile/phonegap-push-notifications.md)
