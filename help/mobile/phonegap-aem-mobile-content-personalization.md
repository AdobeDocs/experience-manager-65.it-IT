---
title: Personalizzazione  dei contenuti AEM Mobile
seo-title: Personalizzazione  dei contenuti AEM Mobile
description: Seguite questa pagina per informazioni  funzione di personalizzazione dei contenuti AEM Mobile che consente agli autori AEM personalizzare i contenuti delle app mobili sfruttando  Adobe Target.
seo-description: Seguite questa pagina per informazioni  funzione di personalizzazione dei contenuti AEM Mobile che consente agli autori AEM personalizzare i contenuti delle app mobili sfruttando  Adobe Target.
uuid: 9078edd1-8399-485f-8a63-a07e766f7ef9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: c9c818dc-c5c4-4a96-94fe-9dc9fe75705b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '2701'
ht-degree: 1%

---


#  personalizzazione dei contenuti AEM Mobile{#aem-mobile-content-personalization}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Questo documento fa parte della [Guida introduttiva  AEM Mobile](/help/mobile/getting-started-aem-mobile.md) Guide, un punto di partenza consigliato per  riferimento AEM Mobile.

La funzione di personalizzazione  dei contenuti AEM Mobile consente agli [autori AEM](#author) di personalizzare i contenuti delle app mobili sfruttando [ Adobe Target](https://www.adobe.com/ca/marketing-cloud/testing-targeting.html). Questo consente di distribuire offerte mirate agli utenti delle applicazioni mobili. Adobe Experience Manager Mobile offre la possibilità di creare, indirizzare e distribuire contenuti che forniranno all&#39;utente contenuti specifici per i propri gusti individuali.

Come spesso accade in AEM, per consentire agli autori di iniziare a creare questo contenuto, gli amministratori e gli sviluppatori devono prima preparare l&#39;ambiente.

[AEM ](#administrator) amministratori sono necessari per stabilire una connessione tra  AEM Mobile e il Cloud Service Adobe Target .

Nel frattempo,  AEM Mobile [sviluppatori](#developer) devono modificare gli script esistenti per facilitare l&#39;authoring dei contenuti mirati.

## Per gli amministratori {#for-administrators}

È necessario procedere in diversi modi per collaborare prima che gli autori dei contenuti possano iniziare a generare contenuto mirato per le app mobili: È disponibile il set di autorizzazioni corretto per utenti e gruppi, creazione di servizi cloud, configurazione dell&#39;applicazione per l&#39;attività e infine generazione del contenuto.

Questo articolo vi guiderà attraverso il processo utilizzato per configurare l&#39; [ applicazione di riferimento ibrida AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) per il targeting.

Si presume che l&#39;applicazione di riferimento ibrido  AEM Mobile sia stata implementata e accessibile tramite  AEM Mobile Dashboard.

Prima che gli autori possano generare contenuto mirato all&#39;interno di un&#39;applicazione, l&#39;istanza AEM deve essere [configurata con l&#39;Cloud Service Adobe Target .](/help/mobile/aem-mobile-configuring-cloud-service.md)

### Autorizzazioni  {#permissions}

Gli utenti che devono accedere alla console di personalizzazione devono far parte del gruppo `target-activity-authors`.

Si consiglia di aggiungere il gruppo target-activity al gruppo apps-admins come parte della configurazione di utenti e gruppi. Aggiungendo il gruppo target-activity-authors, gli utenti potranno vedere la voce di menu di navigazione Personalizzazione.

>[!NOTE]
>
>Se si dimentica di aggiungere gli utenti o i gruppi a cui si desidera accedere alla console di amministrazione della personalizzazione al gruppo target-activity-authors, gli utenti non potranno vedere la console di personalizzazione.

### Cloud Services {#cloud-services}

Per far funzionare il contenuto di destinazione per le applicazioni mobili, sono necessari due servizi: Il  Adobe Target Service e il  Adobe Mobile Services.  Adobe Target Service fornisce il motore per l&#39;elaborazione delle richieste dei clienti e la restituzione dei contenuti personalizzati. Il servizio  Mobile Services fornisce la connessione tra i servizi di Adobe  e l’applicazione mobile tramite il file ADBMobileConfig.json che viene utilizzato dal plug-in AMS Cordova. Dalla  AEM Mobile Dashboard potete configurare l&#39;applicazione aggiungendo i due servizi.

Dal  AEM Mobile Dashboard, individuate i Cloud Services Gestisci e fate clic sul pulsante +.

![chlimage_1-38](assets/chlimage_1-38.png)

Dalla procedura guidata Aggiungi Cloud Service, selezionate la scheda del servizio cloud &quot; Adobe Target&quot; e fate clic su Avanti.

![chlimage_1-39](assets/chlimage_1-39.png)

Dal menu a discesa Selezionate una configurazione potete creare una nuova configurazione oppure selezionarla da una già esistente. Per creare una nuova configurazione, selezionate &quot;Crea configurazione&quot; dal menu a discesa. Immettete un titolo per la configurazione di Target. Immetti il codice cliente, l&#39;e-mail e la password associati al tuo account Target. Se non conosci i valori di questi campi, contatta il supporto Adobe Target . Fare clic sul pulsante &quot;Verifica&quot; per convalidare le credenziali. Una volta verificato, fate clic sul pulsante Invia per creare il servizio cloud.

>[!NOTE]
>
>Il servizio cloud creato viene automaticamente associato all’applicazione mobile tramite la procedura guidata. Il valore della proprietà cq:cloudserviceconfigs viene impostato sul nodo jcr:content del nodo del gruppo delle app. Per l&#39;esempio di app ibrida viene impostato su /content/mobileapps/ibrido-reference-app/jcr:content con il valore che indica il nodo di framework generato automaticamente che si trova in /etc/cloudservices/testandtarget/adobe-target—aem-apps/framework. Per impostazione predefinita, il nodo framework ha due proprietà: genere ed età. Il framework viene utilizzato solo AEM anteprima e non ha alcun impatto sul dispositivo.

Dopo il completamento della procedura guidata, la sezione Gestione Cloud Service conterrà il servizio cloud Target, ma contiene un avviso relativo a un account Mobile Service  Adobe mancante.

![chlimage_1-40](assets/chlimage_1-40.png)

### Adobe Mobile Services {#adobe-mobile-services}

È necessario collegare un account  Mobile Services (AMS) all’applicazione, il servizio AMS fornisce il file ADBMobileConfig.json richiesto che contiene le informazioni sul codice client di Target. Prima di creare un&#39;associazione con l&#39;account AMS, l&#39;account AMS deve essere modificato da un utente che dispone delle autorizzazioni per AMS.

### Codice cliente {#client-code}

Per accedere ai servizi AMS, visita [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/), seleziona l&#39;applicazione mobile e fai clic sulle impostazioni. Individuate il campo Opzioni SDK Target, inserite il codice client nel campo e fate clic su Salva.

![chlimage_1-41](assets/chlimage_1-41.png)

Ora che il codice client è stato associato all’applicazione mobile, quando il servizio cloud AMS viene configurato tramite il dashboard mobile  Adobe, le impostazioni per le impostazioni del servizio verranno distribuite tramite il file ADBMobileConfig.json.

### Cloud Service  Mobile Service {#adobe-mobile-service-cloud-service}

Ora che AMS è stato configurato, è ora di associare l&#39;applicazione mobile nel dashboard Mobile del Adobe . Dal  AEM Mobile Dashboard, individuate i Cloud Services Gestisci e fate clic sul pulsante +.

![chlimage_1-42](assets/chlimage_1-42.png)

Selezionate la scheda  Adobe Mobile Services e fate clic su Avanti.

![chlimage_1-43](assets/chlimage_1-43.png)

Dal passaggio della procedura guidata Crea o Seleziona, selezionate il menu a discesa Mobile Service e la voce Crea configurazione. Fornire un titolo, una società, un nome utente e una password e selezionare il data center appropriato. Se non conosci questi valori, contatta il tuo amministratore  Adobe di Mobile Services per ottenerli. Una volta completati tutti i campi, fate clic sul pulsante Verifica. Il processo di verifica va ad AMS e verifica le credenziali per l&#39;account. Una volta eseguita la convalida, un elenco di Applicazioni mobili verrà popolato nel punto in cui si seleziona l&#39;applicazione mobile associata dal menu a discesa. Fare clic sul pulsante Invia per completare la procedura guidata. Il processo potrebbe richiedere un po&#39; di tempo per ottenere i dati di configurazione e qualsiasi analisi associata all&#39;applicazione. Una volta completato il processo, fate clic sul pulsante Fine dal modale per tornare al dashboard Mobile Adobe .

Tornando alla Mobile Dashboard, la sezione Gestione Cloud Services conterrà il servizio cloud AMS. Inoltre, la sezione Analisi metriche verrà compilata con i rapporti sul ciclo di vita.

![chlimage_1-44](assets/chlimage_1-44.png)

## Per gli autori {#for-authors}

**Prerequisito:** Come già detto, gli amministratori devono configurare la connessione al servizio Adobe Target  prima che gli autori possano generare nuovo contenuto con targeting.

Una volta che l&#39;amministratore ha configurato i due servizi cloud e lo sviluppatore ha configurato il gestore mobileappoffer, gli autori dei contenuti possono ora iniziare a generare esperienze mirate.

La creazione di contenuti mirati all&#39;interno di un&#39;app  AEM Mobile segue una procedura simile a quella per la creazione  AEM Sites:

Per una panoramica completa sull&#39; [Creazione di contenuti mirati in AEM](/help/sites-authoring/personalization.md)

## Per sviluppatori {#for-developers}

AEM gli sviluppatori che creano applicazioni mobili devono continuare a seguire i modelli comunemente utilizzati in AEM durante lo sviluppo di componenti. Di seguito sono descritti i passaggi necessari per consentire agli autori di contenuti di creare contenuti mirati:

###  Adobe Target ContentSync Handlers {#adobe-target-contentsync-handlers}

Per distribuire contenuti al contenuto del dispositivo dell&#39;utente, viene generato il rendering delle offerte create dagli autori AEM contenuto. Per gestire il rendering delle offerte di destinazione, è disponibile un nuovo gestore di sincronizzazione dei contenuti che eseguirà l&#39;elaborazione delle offerte. Utilizzando come esempio l&#39;applicazione di riferimento ibrida, il pacchetto di contenuto en (inglese) contiene ContentSyncConfig con un gestore [mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml). Il passaggio successivo è fondamentale per il rendering delle offerte sul dispositivo. Il gestore mobileappoffer dispone di una proprietà path che identifica il percorso dell&#39;attività di personalizzazione da utilizzare per l&#39;applicazione.

Ad esempio, se esiste un&#39;attività che si trova in */content/campaign/hybridref*, copiate questo percorso e incollatelo come valore nella proprietà *path* del gestore mobileappoffer.

>[!NOTE]
>
>Per l&#39;applicazione di riferimento ibrido ci sono due gestori di mobileNomers uno per il dev e uno per le produzioni.

Una volta che il percorso attività è stato impostato nella proprietà path del gestore mobileappoffer, salvare il gestore. Il gestore sarà ora pronto per avviare le offerte di rendering per i nostri dispositivi mobili.

### Modalità di rendering {#render-mode}

Il gestore mobileappoffer è configurato in modo diverso per le impostazioni di pubblicazione e di sviluppo. Per le impostazioni di pubblicazione, sul nodo cq:ContentSyncConfig è presente una proprietà denominata *renderingMode* con un valore di *publish* impostato. Il gestore mobileappoffers fa riferimento a renderingMode e, se impostato su Pubblica, modifica l&#39;ID mbox che viene creato. Per impostazione predefinita, alle mbox create da AEM viene aggiunto un valore —author. Questo indica che l&#39;attività non è stata pubblicata e che deve utilizzare la campagna non pubblicata per le risoluzioni delle offerte.

Quando il contenuto viene messo in scena tramite il dashboard mobile del  Adobe, il contenuto in fase viene considerato contenuto pronto per la produzione e viene rappresentato tramite la configurazione di sincronizzazione dei contenuti non-dev. Il rendering in questo modo causerà la rimozione di —author da tutti gli ID mbox e prevede la disponibilità di un&#39;attività pubblicata sul server di Target. Prima di testare il contenuto in fase, accertatevi che l&#39;attività sia stata pubblicata.

### Sviluppo app di personalizzazione {#personalization-app-development}

#### Componenti {#components}

Il fondamento di qualsiasi contenuto è in genere un componente di pagina che estende uno dei componenti di base AEM pagina wcm/foundation/components/page o foundation/components/page, a seconda se si utilizza HTL o JSP. La durata di questi passaggi sarà incentrata sull’utilizzo del componente wcm/foundation/components/page. La struttura di base del componente pagina è suddivisa in più script, ciascuno dei quali fornisce lo scopo specifico di consentire allo sviluppatore di organizzare e ignorare il codice, se necessario. I due script che interessano la personalizzazione sono head.html e body.html. Questi due script forniscono un&#39;area in cui è possibile inserire il codice per supportare l&#39;hub di contesto, gli Cloud Services e l&#39;authoring per dispositivi mobili.

Di seguito viene fornita una panoramica dei due script primari utilizzati per abilitare il targeting dei contenuti.

#### head.html {#head-html}

Per consentire all’autore di eseguire il targeting del contenuto, è necessario aggiungere alla pagina il menu di destinazione in modo che l’autore possa cambiare contesto passando dalla modalità di modifica alla modalità di targeting. Per abilitare questa funzione, lo sviluppatore deve modificare lo script head.html in modo da includere il frammento di codice seguente nella parte superiore del file head.html o il più vicino possibile all&#39;elemento &lt;title>&lt;/title>.

```xml
<meta data-sly-test="${!wcmmode.disabled}">
    <div data-sly-call="${clientLib.all @ categories='personalization.kernel'}" data-sly-unwrap></div>
    <div data-sly-resource="${'config' @ resourceType='cq/personalization/components/clientcontext_optimized/config'}" data-sly-unwrap></div>
    <div data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}" data-sly-unwrap></div>
</meta>
```

>[!NOTE]
>
>Tenere presente che lo script deve essere incluso solo quando la modalità WCM non è stata disabilitata, in modo che quando la modalità WCM è disabilitata (per informazioni dettagliate, consultate la sezione del gestore ContentSync) lo script non verrà incluso nel codice dell&#39;applicazione finale.

Per consentire agli autori di visualizzare l&#39;anteprima del contenuto di destinazione, l&#39;editor deve essere in grado di individuare la configurazione del servizio cloud Adobe Target . Il blocco di codice riportato di seguito aggiunge due script importanti. Il primo aggiunge alla pagina la capacità di individuare il servizio cloud Target associato e di effettuare le chiamate a  Adobe Target. Il secondo è l&#39;aggiunta della categoria cq.apps.targeting.

La categoria **cq.apps.targeting** sostituisce il componente predefinito cq/personalization/component/target e utilizza il componente mobileapps/components/target che esegue il rendering delle offerte specifiche per l&#39;uso da parte delle applicazioni mobili. Ulteriori dettagli su questo argomento verranno discussi nella sezione del componente Target.

Il codice deve essere aggiunto in head.html e posizionato appena prima della fine dell&#39;elemento &lt;/head>.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-include="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" data-sly-unwrap></div>
    <meta data-sly-call="${clientLib.all @ categories='cq.apps.targeting'}" data-sly-unwrap></meta>
</div>
```

>[!NOTE]
>
>Il blocco di codice viene racchiuso all’interno di una modalità WCM e non viene disabilitato, pertanto viene riprodotto solo mentre l’autore del contenuto sta lavorando alla creazione di contenuto. Gli script del servizio cloud non verranno aggiunti al codice runtime mobile generato.

#### body.html {#body-html}

Per consentire all&#39;autore del contenuto di testare persone diverse, lo script body.html deve includere il seguente blocco di codice come primo figlio dell&#39;elemento body.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'clientcontext' @ resourceType='cq/personalization/components/clientcontext_optimized'}" data-sly-unwrap></div>
</div>
```

L&#39;ultimo bit di codice richiesto si trova nella parte inferiore del body.html. Questo bit di codice cerca il servizio cloud associato e inserisce il codice appropriato del motore di targeting.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'cloudservices' @ resourceType='cq/cloudserviceconfigs/components/servicecomponents'}" data-sly-unwrap></div>
</div>
```

### Applicazione di riferimento {#reference-application}

Esempi di head.html e body.html si trovano nell&#39;applicazione di riferimento ibrida [ AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) che mostra allo sviluppatore dove inserire i blocchi di script all&#39;interno dei due script.

### Gestori di sincronizzazione dei contenuti {#content-sync-handlers}

Al termine della creazione del contenuto per l’applicazione per dispositivi mobili, il passaggio successivo consiste nel scaricare l’origine e creare l’applicazione, oppure nell’area di visualizzazione del contenuto da pubblicare. Lo sviluppatore deve effettuare una serie di operazioni. Per facilitare il rendering del contenuto  AEM Mobile utilizza gestori di sincronizzazione dei contenuti per eseguire il rendering e creare pacchetti del contenuto. È stato introdotto un nuovo gestore di sincronizzazione dei contenuti per il caso di utilizzo Personalizzazione per eseguire il rendering del contenuto di destinazione. Il gestore &#39;mobileappoffers&#39; è in grado di eseguire il rendering delle offerte di destinazione associate create dall&#39;autore del contenuto. Il gestore mobileappoffers estende il gestore di aggiornamenti delle pagine astratte, pertanto molte delle proprietà sono simili. I dettagli del gestore mobileappoffers hanno le seguenti proprietà.

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Valore</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>riscrittura</td>
   <td>+ relativeParentPath<p> - "/"</p> </td>
   <td>La proprietà rewrite identifica il modo in cui i percorsi all'interno del contenuto devono essere riscritti.</td>
  </tr>
  <tr>
   <td>includePageTypes</td>
   <td><p>"cq/personalization/components/teaserpage",</p> <p>"cq/personalization/components/offerproxy"</p> </td>
   <td>La proprietà includePageTypes è facoltativa, per impostazione predefinita nelle pagine con tipi di risorse cq/personalization/components/teaserpage e cq/personalization/components/offerproxy. Questi due tipi di risorse sono i tipi di risorse predefiniti utilizzati per il targeting del contenuto. Se è necessario supportare altri tipi di risorse, questi devono essere aggiunti all’elenco includePageTypes.</td>
  </tr>
  <tr>
   <td>locationRoot</td>
   <td>/content/mobileapps/&lt;app&gt;</td>
   <td>Il percorso dell'app.</td>
  </tr>
  <tr>
   <td>tipo</td>
   <td>mobileappoffers</td>
   <td>Il nome del gestore che viene chiamato mobileappoffer.</td>
  </tr>
  <tr>
   <td>selettore</td>
   <td>candela</td>
   <td>Il selettore di testo viene utilizzato per eseguire il rendering del contenuto di destinazione. </td>
  </tr>
  <tr>
   <td>targetRootDirectory</td>
   <td>www</td>
   <td>La directory principale in cui persistere il contenuto di cui è stato effettuato il rendering.</td>
  </tr>
  <tr>
   <td>includeImages</td>
   <td>true | false</td>
   <td>Se true, viene eseguito il rendering di tutte le immagini incluse nell'offerta. Se false immagini verranno ignorate.</td>
  </tr>
  <tr>
   <td>includeVideo</td>
   <td>true | false</td>
   <td>Se true, verrà eseguito il rendering dei video inclusi nell'offerta. Se false, i video verranno ignorati.</td>
  </tr>
  <tr>
   <td>path</td>
   <td>/content/campaign/&lt;brand&gt;</td>
   <td>Indica il marchio della campagna a cui partecipano le offerte. Attualmente tutte le offerte devono provenire dalla stessa campagna.</td>
  </tr>
  <tr>
   <td>profondo</td>
   <td>true | false</td>
   <td>Se true esegue il rendering ricorsivo di tutte le pagine figlie, se false non ricorre. </td>
  </tr>
  <tr>
   <td>extension</td>
   <td>viene</td>
   <td>Imposta l'estensione per la risorsa di cui viene eseguito il rendering. Impostate su html in modo che le pagine abbiano l’estensione .html.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>L&#39;[ AEM Mobile Hybrid Reference App](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) dispone della configurazione predefinita del gestore mobileappoffer. La proprietà path nell&#39;esempio è vuota perché dipende dalla posizione della campagna. Dopo che l&#39;autore di una campagna ha creato una campagna, l&#39;amministratore delle app deve associare la campagna al gestore specificando la proprietà path da indirizzare alla campagna.

### Componente di destinazione {#target-component}

Per facilitare il rendering del contenuto specificatamente per le applicazioni mobili,  AEM Mobile utilizza il componente mobileapps/components/target. Il componente destinazione per dispositivi mobili estende il componente cq/personalization/components/target e sostituisce lo script Engine_tnt.jsp. Ignorando il motore_tnt.jsp questo consente  AEM Mobile di controllare l&#39;HTML generato per le applicazioni mobili. Per ogni componente per il quale l&#39;autore del contenuto esegue il targeting, viene creata una mbox associata da Engine_tnt.jsp.

Per ogni mbox viene aggiunto un attributo di **cq-targeting**, che consente agli sviluppatori di applicazioni di scrivere codice personalizzato da utilizzare in qualsiasi momento. L&#39; [ AEM Mobile Hybrid Reference App](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) include un esempio di direttiva Angular che utilizza l&#39;attributo cq-targeting. Il concetto di sostituzione del contenuto quando e come viene fatto dipende in larga misura dallo sviluppatore di applicazioni mobili. Esiste un SDK Mobile che viene distribuito tramite AEM /etc/clientlibs/mobileapps/js/mobileapps.js che fornisce un&#39;API per chiamare il servizio di targeting del Adobe . Spetta allo sviluppatore dell’applicazione specificare quando effettuare la chiamata in base alla progettazione dell’applicazione.

## Cosa succede dopo? {#what-s-next}

1. [Avvia la mia esperienza  app AEM Mobile](/help/mobile/starting-aem-phonegap-app.md)
1. [Gestione del contenuto dell&#39;app](/help/mobile/phonegap-manage-app-content.md)
1. [Creare l&#39;applicazione](/help/mobile/building-app-mobile-phonegap.md)
1. [Monitora le prestazioni dell&#39;app con  Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Esperienza app personalizzata con  Adobe Target](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [Invio di messaggi importanti agli utenti](/help/mobile/phonegap-push-notifications.md)
