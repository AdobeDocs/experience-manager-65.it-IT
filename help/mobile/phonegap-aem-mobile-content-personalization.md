---
title: Personalizzazione dei contenuti AEM Mobile
seo-title: AEM Mobile content personalization
description: Segui questa pagina per scoprire la funzione di personalizzazione dei contenuti di AEM Mobile che consente AEM autori di personalizzare i contenuti delle app mobili sfruttando Adobe Target.
seo-description: Follow this page to learn about AEM Mobile content personalization feature that allows AEM authors to personalize mobile app content by leveraging Adobe Target.
uuid: 9078edd1-8399-485f-8a63-a07e766f7ef9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: c9c818dc-c5c4-4a96-94fe-9dc9fe75705b
exl-id: 70d7ee0d-2f6d-4f97-a6e2-b02d84a0ca42
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '2673'
ht-degree: 1%

---

# Personalizzazione dei contenuti AEM Mobile{#aem-mobile-content-personalization}

>[!NOTE]
>
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio, React). [Per saperne di più](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Questo documento fa parte del [Guida introduttiva ad AEM Mobile](/help/mobile/getting-started-aem-mobile.md) Guida, un punto di partenza consigliato per riferimento AEM Mobile.

La funzione di personalizzazione dei contenuti di AEM Mobile consente [Autori AEM](#author) personalizzare il contenuto delle app mobili sfruttando [Adobe Target](https://www.adobe.com/ca/marketing-cloud/testing-targeting.html). Ciò consente la consegna di offerte mirate agli utenti di applicazioni mobili. Adobe Experience Manager Mobile offre la possibilità di creare, eseguire il targeting e distribuire contenuti che forniranno all’utente contenuti specifici per i propri gusti individuali.

Come spesso accade in AEM, affinché gli autori inizino a creare questo contenuto, gli amministratori e gli sviluppatori devono prima preparare l’ambiente.

[Amministratori AEM](#administrator) sono necessarie per stabilire una connessione tra AEM Mobile e l’Cloud Service Adobe Target.

Nel frattempo, AEM Mobile [sviluppatori](#developer) devono modificare gli script esistenti per facilitare l’authoring di contenuti mirati.

## Per gli amministratori {#for-administrators}

È necessario procedere in diversi modi per collaborare prima che gli autori dei contenuti possano iniziare a generare contenuti mirati per le app per dispositivi mobili: Ottieni il set di autorizzazioni corretto per utenti e gruppi, creazione di servizi cloud, configurazione dell’applicazione per l’attività e infine generazione del contenuto.

Questo articolo ti guiderà attraverso il processo utilizzato per configurare il [Applicazione di riferimento ibrida AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) per il targeting.

Si presume che l’applicazione di riferimento ibrida di AEM Mobile sia stata implementata correttamente e accessibile tramite il dashboard di AEM Mobile.

Prima che gli autori possano generare contenuti mirati all’interno di un’applicazione, l’istanza AEM deve essere [configurato con l’Cloud Service Adobe Target.](/help/mobile/aem-mobile-configuring-cloud-service.md)

### Autorizzazioni {#permissions}

Gli utenti che devono accedere alla console di personalizzazione devono far parte del gruppo `target-activity-authors` gruppo.

È consigliabile che, come parte della configurazione degli utenti e del gruppo, il gruppo target-activity venga aggiunto al gruppo apps-admins . Aggiungendo il gruppo target-activity-authors , gli utenti potranno vedere la voce di menu di navigazione Personalizzazione.

>[!NOTE]
>
>Se dimentichi di aggiungere al gruppo target-activity-authors gli utenti o i gruppi a cui desideri accedere da admin console di personalizzazione, gli utenti non potranno più visualizzare la console di personalizzazione.

### Cloud Services {#cloud-services}

Per il funzionamento del contenuto di destinazione per le applicazioni mobili sono necessari due servizi: Adobe Target Service e Adobe Mobile Services. Il servizio Adobe Target fornisce il motore per l’elaborazione delle richieste dei clienti e la restituzione del contenuto personalizzato. Il servizio Adobe Mobile Services fornisce la connessione tra Adobe Services e l’app mobile tramite il file ADBMobileConfig.json, utilizzato dal plug-in AMS Cordova. Dalla dashboard di AEM Mobile è possibile configurare l&#39;applicazione aggiungendo i due servizi.

Dalla dashboard di AEM Mobile individua i Cloud Services di gestione e fai clic sul pulsante + .

![chlimage_1-38](assets/chlimage_1-38.png)

Dalla procedura guidata Aggiungi Cloud Service selezionare la scheda del servizio cloud &quot;Adobe Target&quot; e fare clic su Avanti.

![chlimage_1-39](assets/chlimage_1-39.png)

Dal menu a discesa Seleziona una configurazione puoi creare una nuova configurazione o selezionarla da una esistente. Per creare una nuova configurazione, seleziona &quot;Crea configurazione&quot; dal menu a discesa. Immetti un titolo per la configurazione di Target. Immetti il codice cliente, l&#39;e-mail e la password associati al tuo account Target. Se non conosci i valori per questi campi, contatta il supporto Adobe Target. Fai clic sul pulsante &quot;Verifica&quot; per convalidare le credenziali. Una volta verificato, fai clic sul pulsante Invia per creare il servizio cloud.

>[!NOTE]
>
>Il servizio cloud che viene creato viene associato automaticamente all’app mobile tramite la procedura guidata. Il valore della proprietà cq:cloudserviceconfigs viene impostato sul nodo jcr:content del nodo del gruppo di app. Per l&#39;esempio di app ibrida viene impostato su /content/mobileapps/ibrido-reference-app/jcr:content con il valore che punta al nodo del framework generato automaticamente, che si trova in /etc/cloudservices/testandtarget/adobe-target—aem-apps/framework. Il nodo del framework ha due proprietà impostate per impostazione predefinita, genere ed età. Il framework viene utilizzato solo AEM visualizzazione in anteprima e non ha alcun impatto sul dispositivo.

Dopo il completamento della procedura guidata, il riquadro Gestione Cloud Service conterrà il servizio cloud di Target, tuttavia contiene un avviso relativo a un account Adobe Mobile Service mancante.

![chlimage_1-40](assets/chlimage_1-40.png)

### Adobe Mobile Services {#adobe-mobile-services}

È necessario collegare un account Adobe Mobile Services (AMS) anche all’applicazione, il servizio AMS fornisce il file ADBMobileConfig.json richiesto che contiene le informazioni sul codice client di Target. Prima di creare un’associazione con l’account AMS, l’account AMS deve essere modificato da un utente che dispone delle autorizzazioni per AMS.

### Codice cliente {#client-code}

Per accedere ai servizi AMS visita [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/), seleziona l’app mobile e fai clic sulle impostazioni . Individua il campo Opzioni SDK Target e inserisci il codice client nel campo , quindi fai clic su Salva.

![chlimage_1-41](assets/chlimage_1-41.png)

Ora che il codice client è stato associato all’app mobile, quando il servizio cloud AMS è configurato tramite la dashboard di Adobe Mobile, le impostazioni per le impostazioni del servizio verranno distribuite tramite il file ADBMobileConfig.json .

### Cloud Service Adobe Mobile Services {#adobe-mobile-service-cloud-service}

Ora che AMS è stato configurato, è il momento di associare l’app mobile nel dashboard di Adobe Mobile. Dalla dashboard di AEM Mobile individua i Cloud Services di gestione e fai clic sul pulsante + .

![chlimage_1-42](assets/chlimage_1-42.png)

Seleziona la scheda Adobe Mobile Services e fai clic su Avanti.

![chlimage_1-43](assets/chlimage_1-43.png)

Dal passaggio Crea o Seleziona procedura guidata , seleziona il menu a discesa Mobile Services e seleziona la voce Crea configurazione . Fornisci un titolo, una società, un nome utente e una password e seleziona il centro dati appropriato. Se non conosci questi valori, contatta l’amministratore di Adobe Mobile Services per ottenerli. Dopo aver compilato tutti i campi, fai clic sul pulsante Verifica . Il processo di verifica va ad AMS e verifica le credenziali per l’account. Una volta eseguita la convalida, un elenco di applicazioni mobili verrà compilato nel punto in cui si seleziona l’applicazione mobile associata dal menu a discesa. Fare clic sul pulsante Invia per completare la procedura guidata. Il processo potrebbe richiedere un po&#39; di tempo per ottenere i dati di configurazione e qualsiasi analisi associata all&#39;applicazione. Una volta completato il processo, fai clic sul pulsante Fine dal modale per tornare alla dashboard mobile di Adobe.

Tornando alla Dashboard mobile, la sezione Gestione Cloud Services conterrà il servizio cloud AMS. Noterai inoltre che la sezione Analizza metriche sarà compilata con rapporti sul ciclo di vita.

![chlimage_1-44](assets/chlimage_1-44.png)

## Per gli autori {#for-authors}

**Prerequisito:** Come indicato in precedenza, gli amministratori devono configurare la connessione al servizio Adobe Target prima che gli autori possano generare nuovi contenuti mirati.

Dopo che l’amministratore ha configurato i due servizi cloud e lo sviluppatore ha configurato il gestore di dispositivi mobili, gli autori dei contenuti possono ora iniziare a generare esperienze mirate.

La procedura per creare contenuti mirati all’interno di un’app AEM Mobile è simile a quella per l’authoring di AEM Sites:

Vedi qui per una panoramica completa su [Creazione di contenuti mirati in AEM](/help/sites-authoring/personalization.md)

## Per sviluppatori {#for-developers}

AEM gli sviluppatori che creano applicazioni mobili devono continuare a seguire i pattern comunemente utilizzati in AEM durante lo sviluppo dei componenti. Di seguito sono riportati i passaggi necessari per consentire agli autori di contenuti di creare contenuti mirati:

### Gestori di Adobe Target ContentSync {#adobe-target-contentsync-handlers}

Per distribuire contenuti al contenuto del dispositivo dell’utente, viene generato il rendering delle offerte create dagli autori AEM contenuti. Per gestire il rendering delle offerte target, è disponibile un nuovo gestore di sincronizzazione dei contenuti che elabora le offerte. Utilizzando come esempio l’applicazione di riferimento ibrida, il pacchetto di contenuto en (inglese) contiene la configurazione ContentSyncConfig con un [telefonatori](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) handler. Il passaggio successivo è fondamentale per il rendering delle offerte sul dispositivo. Il gestore mobileappoffer ha una proprietà path che identifica il percorso dell&#39;attività di personalizzazione da utilizzare per l&#39;applicazione.

Ad esempio, se esiste un’attività che si trova in */content/campagne/hybridref* copia questo percorso e incollalo come valore nel *path* proprietà del gestore mobileappoffers.

>[!NOTE]
>
>Per l&#39;applicazione di riferimento ibrida sono disponibili due gestori di dispositivi mobili, uno per lo sviluppo e uno per le produzioni.

Una volta impostato il percorso delle attività nella proprietà del percorso del gestore mobileappoffer, salva il gestore. Il gestore sarà ora pronto per avviare il rendering delle offerte per i nostri dispositivi mobili.

### Modalità rendering {#render-mode}

Il gestore mobileappoffer è configurato in modo diverso per le impostazioni di pubblicazione e di sviluppo. Per le impostazioni di pubblicazione è presente una proprietà denominata *renderMode* con un valore di *pubblicare* impostato sul nodo cq:ContentSyncConfig . Il gestore mobileappoffers fa riferimento a renderMode e, se impostato su publish, modificherà l&#39;id mbox che viene creato. Per impostazione predefinita, alle mbox create da AEM è stato aggiunto un valore —author all&#39;id mbox. Questo identifica che l’attività non è stata pubblicata e dovrebbe utilizzare la campagna non pubblicata per le risoluzioni delle offerte.

Quando il contenuto viene messo in staging tramite la dashboard di Adobe Mobile, il contenuto in staging viene considerato contenuto pronto per la produzione e sottoposto a rendering tramite la configurazione di sincronizzazione dei contenuti non per sviluppo. Il rendering in questo modo causerà la rimozione dell’autore —da tutti gli ID mbox e prevede che un’attività pubblicata sia disponibile sul server Target. Prima di testare il contenuto in staging, accertati che l’attività sia stata pubblicata.

### Sviluppo di app per la personalizzazione {#personalization-app-development}

#### Componenti {#components}

Il fondamento di qualsiasi contenuto è in genere un componente di pagina che estende uno dei componenti di base AEM pagina wcm/foundation/components/page o foundation/components/page a seconda che si utilizzi HTL o JSP. La durata di questi passaggi sarà incentrata sull’utilizzo del componente wcm/foundation/components/page . La struttura di base del componente pagina è suddivisa in più script, ciascuno dei quali fornisce lo scopo specifico di consentire allo sviluppatore di organizzare e sovrascrivere il codice, se necessario. I due script di interesse per la personalizzazione sono head.html e body.html. Questi due script forniscono un’area in cui è possibile inserire codice per supportare Context Hub, i Cloud Services e l’authoring mobile.

Ecco una panoramica dei due script principali utilizzati per abilitare il targeting dei contenuti.

#### head.html {#head-html}

Per consentire all’autore di eseguire il targeting del contenuto, è necessario aggiungere alla pagina il menu di destinazione in modo che l’autore possa cambiare contesto passando dalla modalità di modifica alla modalità di targeting. Per abilitare questa funzione, lo sviluppatore deve modificare lo script head.html in modo da includere il seguente frammento di codice vicino alla parte superiore del file head.html o vicino al &lt;title>&lt;/title> il più possibile.

```xml
<meta data-sly-test="${!wcmmode.disabled}">
    <div data-sly-call="${clientLib.all @ categories='personalization.kernel'}" data-sly-unwrap></div>
    <div data-sly-resource="${'config' @ resourceType='cq/personalization/components/clientcontext_optimized/config'}" data-sly-unwrap></div>
    <div data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}" data-sly-unwrap></div>
</meta>
```

>[!NOTE]
>
>Tieni presente che lo script deve essere incluso solo quando la modalità WCM non è stata disattivata in modo tale che quando la modalità WCM è disabilitata (consulta la sezione del gestore ContentSync per i dettagli) lo script non verrà incluso nel codice dell’applicazione finale.

Per consentire agli autori di visualizzare in anteprima il contenuto di destinazione, l’editor deve essere in grado di individuare la configurazione del servizio cloud Adobe Target. Il blocco di codice seguente aggiunge due script importanti. La prima aggiunta della possibilità per la pagina di individuare il servizio cloud Target associato e di effettuare le chiamate ad Adobe Target. Il secondo è l&#39;aggiunta della categoria cq.apps.targeting .

La **cq.apps.targeting** Questa categoria sostituisce il componente predefinito cq/personalization/component/target e utilizza il componente mobileapps/components/target che esegue il rendering delle offerte specificamente per il consumo di applicazioni mobili. Ulteriori dettagli su questo argomento saranno discussi nella sezione del componente Target .

Il codice deve essere aggiunto in head.html e posizionato immediatamente prima della fine del &lt;/head> elemento.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-include="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" data-sly-unwrap></div>
    <meta data-sly-call="${clientLib.all @ categories='cq.apps.targeting'}" data-sly-unwrap></meta>
</div>
```

>[!NOTE]
>
>Il blocco di codice viene racchiuso all’interno di una modalità WCM e non viene disattivato, pertanto viene riprodotto solo mentre l’autore del contenuto sta lavorando alla creazione del contenuto. Gli script del servizio cloud non verranno aggiunti al codice di runtime mobile generato.

#### body.html {#body-html}

Per consentire all’autore del contenuto di testare utenti tipo diversi, lo script body.html deve includere il seguente blocco di codice come primo elemento figlio dell’elemento body.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'clientcontext' @ resourceType='cq/personalization/components/clientcontext_optimized'}" data-sly-unwrap></div>
</div>
```

L&#39;ultimo bit di codice richiesto si trova nella parte inferiore del file body.html . Questo bit di codice cerca il servizio cloud associato e inserisce il codice appropriato del motore di destinazione.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'cloudservices' @ resourceType='cq/cloudserviceconfigs/components/servicecomponents'}" data-sly-unwrap></div>
</div>
```

### Applicazione di riferimento {#reference-application}

Esempi di head.html e body.html sono disponibili nella sezione [Applicazione di riferimento ibrida AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) mostrare allo sviluppatore dove posizionare i blocchi di script all’interno dei due script.

### Gestori di sincronizzazione dei contenuti {#content-sync-handlers}

Al termine della creazione del contenuto per l’app mobile, l’autore del contenuto deve scaricare l’origine e generare l’applicazione, oppure creare un’area di visualizzazione del contenuto da pubblicare. Per eseguire questa operazione, lo sviluppatore deve effettuare una serie di passaggi. Per facilitare il rendering del contenuto, AEM Mobile utilizza gestori di sincronizzazione dei contenuti per eseguire il rendering e creare pacchetti del contenuto. È stato introdotto un nuovo gestore di sincronizzazione dei contenuti per il caso d’uso Personalizzazione per eseguire il rendering del contenuto di destinazione. Il gestore &quot;mobileappoffers&quot; sa come eseguire il rendering delle offerte target associate create dall’autore del contenuto. Il gestore mobileappoffers estende il gestore di aggiornamenti delle pagine astratte, quindi molte delle proprietà sono simili. I dettagli del gestore mobileappoffer hanno le seguenti proprietà.

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Valore</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>riscrittura</td>
   <td>+ relativoParentPath<p> - "/"</p> </td>
   <td>La proprietà rewrite identifica il modo in cui i percorsi all'interno del contenuto devono essere riscritti.</td>
  </tr>
  <tr>
   <td>includedPageTypes</td>
   <td><p>"cq/personalization/components/teaserpage",</p> <p>"cq/personalization/components/offerproxy"</p> </td>
   <td>La proprietà includePageTypes è facoltativa, per impostazione predefinita nelle pagine che hanno tipi di risorse di cq/personalization/components/teaserpage e cq/personalization/components/offerproxy. Questi due tipi di risorse sono i tipi di risorse predefiniti utilizzati per il targeting del contenuto. Se è necessario supportare altri tipi di risorse, è necessario aggiungerli all’elenco di includePageTypes.</td>
  </tr>
  <tr>
   <td>locationRoot</td>
   <td>/content/mobileapps/&lt;app&gt;</td>
   <td>Posizione dell’app.</td>
  </tr>
  <tr>
   <td>tipo</td>
   <td>telefonatori</td>
   <td>Il nome del gestore che si trova in mobileappoffer.</td>
  </tr>
  <tr>
   <td>selettore</td>
   <td>candela</td>
   <td>Il selettore di tag viene utilizzato per eseguire il rendering del contenuto di destinazione. </td>
  </tr>
  <tr>
   <td>targetRootDirectory</td>
   <td>www</td>
   <td>Directory principale in cui persistere il contenuto di cui è stato effettuato il rendering.</td>
  </tr>
  <tr>
   <td>includeImages</td>
   <td>true | false</td>
   <td>Se true, viene eseguito il rendering di tutte le immagini incluse nell’offerta. Se false immagini verranno saltate.</td>
  </tr>
  <tr>
   <td>includeVideo</td>
   <td>true | false</td>
   <td>Se true , verrà eseguito il rendering di qualsiasi video incluso nell’offerta. Se i video falsi vengono ignorati.</td>
  </tr>
  <tr>
   <td>path</td>
   <td>/content/campagne/&lt;brand&gt;</td>
   <td>Indica il marchio della campagna a cui partecipano le offerte. Attualmente tutte le offerte devono provenire dalla stessa campagna.</td>
  </tr>
  <tr>
   <td>profondo</td>
   <td>true | false</td>
   <td>Se true esegue in modo ricorsivo il rendering di tutte le pagine figlie, se false non ricorre. </td>
  </tr>
  <tr>
   <td>estensione</td>
   <td>viene</td>
   <td>Imposta l'estensione per la risorsa di cui si sta eseguendo il rendering. Imposta su html in modo che le pagine abbiano un'estensione .html .</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>La [App di riferimento ibrida di AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) dispone della configurazione predefinita del gestore di telefonia mobile. La proprietà del percorso nell&#39;esempio è vuota in quanto dipende dalla posizione della campagna. Dopo che un autore di Campaign ha creato una campagna, l’amministratore delle app deve associare la campagna al gestore specificando la proprietà del percorso in cui puntare alla campagna.

### Componente Target {#target-component}

Per facilitare il rendering del contenuto in modo specifico per le applicazioni mobili, AEM Mobile utilizza il componente mobileapps/components/target . Il componente target mobile estende il componente cq/personalization/components/target e sostituisce lo script engine_tnt.jsp. Ignorando engine_tnt.jsp questo consente ad AEM Mobile di controllare il HTML generato per il caso d’uso delle app per dispositivi mobili. Per ogni componente di destinazione di un autore di contenuti, una mbox associata viene creata da engine_tnt.jsp.

Per ogni mbox un attributo di **cq-targeting** è stato aggiunto per consentire agli sviluppatori di applicazioni di scrivere codice personalizzato da utilizzare e utilizzare in qualsiasi momento. La [App di riferimento ibrida di AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) ha un esempio di direttiva di Angular che utilizza l&#39;attributo cq-targeting. Il concetto di sostituzione dei contenuti quando e come viene fatto dipende in larga misura dallo sviluppatore di applicazioni mobili. È disponibile un SDK mobile fornito tramite AEM /etc/clientlibs/mobileapps/js/mobileapps.js che fornisce un’API per chiamare il servizio di targeting di Adobe. Spetta allo sviluppatore dell’applicazione specificare quando effettuare la chiamata in base alla progettazione della propria applicazione.

## Novità? {#what-s-next}

1. [Avvia la mia esperienza con l’app AEM Mobile](/help/mobile/starting-aem-phonegap-app.md)
1. [Gestire il contenuto dell’app](/help/mobile/phonegap-manage-app-content.md)
1. [Creare l&#39;applicazione](/help/mobile/building-app-mobile-phonegap.md)
1. [Monitora le prestazioni della mia app con Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Fornire un’esperienza di app personalizzata con Adobe Target](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [Inviare messaggi importanti ai miei utenti](/help/mobile/phonegap-push-notifications.md)
