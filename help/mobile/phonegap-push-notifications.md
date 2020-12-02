---
title: Notifiche push
seo-title: Notifiche push
description: Segui questa pagina per scoprire come utilizzare le notifiche push in un'app  AEM Mobile.
seo-description: Segui questa pagina per scoprire come utilizzare le notifiche push in un'app  AEM Mobile.
uuid: 0ed8b183-ef81-487f-8f35-934d74ec82af
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: ed8c51d2-5aac-4fe8-89e8-c175d4ea1374
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d
workflow-type: tm+mt
source-wordcount: '3291'
ht-degree: 1%

---


# Notifiche push{#push-notifications}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

La possibilità di avvisare immediatamente gli utenti  app AEM Mobile con notifiche importanti è fondamentale per il valore di un&#39;app mobile e delle sue campagne di marketing. Qui descriviamo i passaggi da effettuare per consentire alla tua app di ricevere le notifiche push e come configurare e inviare i messaggi push da  AEM Mobile all&#39;app installata sul telefono. Inoltre, questa sezione descrive come configurare la funzione [Collegamento profondo](#deeplinking) alle notifiche push.

>[!NOTE]
>
>*Le notifiche push non sono garantite; sono più come annunci. Si fa il massimo sforzo per assicurarsi che tutti li ricevano ma non sono un meccanismo di consegna garantito. Inoltre, il tempo necessario per distribuire un push può variare da meno di un secondo a meno di mezz&#39;ora.*

L&#39;utilizzo delle notifiche push con AEM richiede diverse tecnologie. Innanzitutto, un provider di servizi di notifica push deve essere utilizzato per gestire le notifiche e i dispositivi (AEM non lo fa ancora). Due provider sono configurati out-of-the-box con AEM: [ Amazon Simple Notification Service](https://aws.amazon.com/sns/) (o SNS) e [Pushwoosh](https://www.pushwoosh.com/). In secondo luogo, la tecnologia push per il sistema operativo mobile specificato deve passare attraverso il servizio appropriato — Apple Push Notification Service (o APNS) per dispositivi iOS; e Google Cloud Messaging (o GCM) per dispositivi Android. Sebbene AEM non comunichi direttamente con questi servizi specifici della piattaforma, alcune informazioni di configurazione correlate devono essere fornite da AEM insieme alle notifiche affinché questi servizi eseguano il push.

Una volta installato e configurato (come spiegato di seguito) funziona come segue:

1. Una notifica push viene creata in AEM e inviata al provider di servizi ( Amazon SNS o Pushwoosh).
1. Il provider di servizi lo riceve e lo invia al provider di base (APNS o GCM).
1. Il provider di base invia la notifica a tutti i dispositivi registrati per tale push. Per ogni dispositivo utilizza la rete dati cellulare o il WiFi, a seconda di quale sia attualmente disponibile sul dispositivo.
1. La notifica viene visualizzata sul dispositivo se l&#39;app per cui è registrata non è in esecuzione. Toccando la notifica l&#39;utente avvia l&#39;app e visualizza la notifica all&#39;interno dell&#39;app. Nel caso in cui l&#39;applicazione sia già in esecuzione, viene visualizzata solo la notifica in-app.

Questa versione di AEM supporta i dispositivi mobili iOS e Android.

## Panoramica e procedura {#overview-and-procedure}

Per utilizzare le notifiche push in un&#39;app AEM Mobile , è necessario effettuare i seguenti passaggi di alto livello.

In genere, uno sviluppatore AEM:

1. Registrati con i servizi di messaggistica Apple e Google
1. Registrati con un servizio di messaggistica push e configuralo
1. Aggiunta del supporto push all&#39;app
1. Preparare un telefono per il test

Mentre un amministratore AEM:

1. Configurare il push su AEM app
1. Creare e distribuire l&#39;app
1. Invia una notifica push
1. Configurare il collegamento profondo *(facoltativo)*

### Passaggio 1: Registrati con i servizi di messaggistica Apple e Google {#step-register-with-apple-and-google-messaging-services}

#### Utilizzo di Apple Push Notification Service (APNS) {#using-the-apple-push-notification-service-apns}

Andate alla pagina Apple [qui](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html) per acquisire familiarità con Apple Push Notification Service.

Per utilizzare APNS è necessario un file **Certificate** (un file .cer), una **Chiave privata** (un file .p12) e una **Password chiave privata** da Apple. Le istruzioni su come farlo sono reperibili [qui](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ProvisioningDevelopment.html).

#### Utilizzo del servizio Google Cloud Messaging (GCM) {#using-the-google-cloud-messaging-gcm-service}

>[!NOTE]
>
>Google sta sostituendo GCM con un servizio simile denominato Firebase Cloud Messaging (FCM). Per ulteriori informazioni su FCM, fare clic su [qui](https://developers.google.com/cloud-messaging/faq).

Andate alla pagina Google [qui](https://developer.android.com/google/gcm/index.html) per acquisire familiarità con Google Cloud Messaging per Android.

Sarà necessario seguire i passaggi da [qui](https://developer.android.com/google/gcm/gs.html) a **Crea un progetto API Google**, **Abilita il servizio GCM** e **Ottieni una chiave API**. Per inviare le notifiche push ai dispositivi Android sarà necessario **Chiave API**. Inoltre, registrare il numero **Project Number**, talvolta denominato anche **GCM Sender Id**.

La procedura seguente illustra un metodo diverso per la creazione di chiavi API GCM:

1. Accedete a Google e andate alla [pagina Sviluppatore di Google](https://developers.google.com/mobile/add?platform=android&amp;cntapi=gcm).
1. Scegliete l&#39;app dall&#39;elenco (o createne una nuova).
1. In Nome pacchetto Android, immettete il vostro ID app, ossia `com.adobe.cq.mobile.weretail.outdoorsapp`. Se questo non funziona, riprovate con &quot;test.test&quot;.
1. Fare clic su **Continua per scegliere e configurare i servizi**
1. Selezionate Cloud Messaging, quindi fate clic su **Abilita Google Cloud Messaging**.
1. Verrà visualizzata la nuova chiave API server e l&#39;ID mittente (nuovo o esistente).

>[!NOTE]
>
>Registra la chiave API del server. Questo valore viene immesso nel sito del provider push.

### Passaggio 2: Registrazione e configurazione di un servizio di messaggistica push {#step-register-and-configure-a-push-messaging-service}

AEM configurato per utilizzare uno dei tre servizi per le notifiche push:

* Amazon SNS
* Pushwoosh
* Adobe Mobile Services

*configurazioni Amazon* SNSe  ** Pushwooshsaranno in grado di inviare i messaggi push dall&#39;interno AEM schermi.

*Adobe Mobile* Services la configurazione consente di configurare e inviare le notifiche push dall&#39;interno  Adobe Mobile Services utilizzando un account Adobe Analytics  (ma l&#39;app deve essere creata con questo set di configurazione per abilitare le notifiche push AMS).

#### Utilizzo del servizio di messaggistica  Amazon SNS {#using-the-amazon-sns-messaging-service}

>[!NOTE]
>
>*Informazioni su  Amazon SNS e un collegamento per la creazione di un nuovo account AWS sono disponibili  [qui](https://aws.amazon.com/sns/). È possibile ottenere un account gratuito per un anno.*

Se non si desidera utilizzare  Amazon SNS, è possibile saltare questi passaggi.

Per impostare  Amazon SNS per le notifiche push, effettuate le seguenti operazioni:

1. **Registrazione con  Amazon SNS**

   1. Registra il tuo ID account. Il formato deve essere composto da dodici cifre senza spazi o trattini, ovvero &quot;123456789012&quot;.
   1. Assicurarsi di essere nell&#39;area &quot;us-east&quot; o &quot;eu&quot;, come un passo successivo (Creazione del pool di identità) richiede uno di questi.
   1. Dopo la registrazione, accedete alla console di gestione e selezionate [SNS](https://console.aws.amazon.com/sns/) (Push Notification Service). Fare clic su &quot;Get Started&quot; se viene visualizzato.

1. **Crea chiave di accesso e ID**

   1. Fate clic sul nome di accesso in alto a destra della schermata e scegliete Credenziali di protezione dal menu.
   1. Fare clic su Tasti di accesso e nello spazio sottostante fare clic su **Crea nuova chiave di accesso**.
   1. Fare clic su **Mostra chiave di accesso**, quindi copiare e salvare l&#39;ID chiave di accesso e la chiave di accesso segreta mostrati. Se scegliete l&#39;opzione per scaricare le chiavi, otterrete un file CSV che contiene gli stessi valori.
   1. In questa pagina è possibile gestire altri certificati relativi alla sicurezza e altri.

   >[!NOTE]
   >
   >Una chiave di accesso può essere utilizzata per più app.

   Per le organizzazioni che utilizzano un account &quot;AWS Sandbox&quot;, i passaggi sono molto simili e descritti di seguito:

   1. Fate clic sul nome di accesso in alto a destra della schermata e scegliete Credenziali di protezione personale dal menu.
   1. Fate clic su Utenti nell’elenco a sinistra delle azioni e scegliete il nome utente.
   1. Fare clic sulla scheda Credenziali di protezione.
   1. Da qui si vedono le chiavi e si creano nuove chiavi. Salvate le chiavi per un utilizzo successivo.


1. **Creare un argomento**

   1. Fate clic su **Crea argomento** e scegliete un nome per l&#39;argomento. Registra tutti i campi come ARN argomento, Proprietario argomento, Regione, Nome visualizzato.
   1. Fare clic su **Altre azioni argomento** > **Modifica criterio argomento**. In **Consenti a questi utenti di iscriversi a questo argomento**, selezionare **Tutti.**
   1. Fare clic su **Aggiorna criterio**.

   >[!NOTE]
   >
   >Potete creare più argomenti per diversi scenari, ad esempio dev, test, demo e così via. Il resto della configurazione SNS può rimanere invariato. Create l&#39;app con il diverso argomento; le notifiche push inviate a tale argomento verranno ricevute solo dall&#39;app creata con tale argomento.

1. **Creare applicazioni per la piattaforma**

   1. Fate clic su Applicazioni, quindi su Crea applicazione piattaforma. Scegliete un nome e selezionate una piattaforma (APNS for iOS, GCM for Android). A seconda della piattaforma, dovranno essere compilati altri campi:

      1. Per APNS, è necessario immettere un file P12, una password, un certificato e una chiave privata. Questi sono stati ottenuti nel passaggio *Utilizzo del servizio APNS (Apple Push Notification Service)* precedente.
      1. Per GCM, è necessario inserire una chiave API. Ciò dovrebbe essere ottenuto nel passaggio *Utilizzo del servizio Google Cloud Messaging (GCM)* precedente.
   1. Ripetete il passaggio riportato sopra una volta per ogni piattaforma da supportare. Per poter effettuare il push sia a iOS che ad Android, è necessario creare due applicazioni piattaforma.


1. **Creare un pool di identità**

   1. Utilizzate [Cognito](https://console.aws.amazon.com/cognito) per creare un pool di identità, che archivierà i dati di base degli utenti non autenticati. In questa fase, solo le regioni &quot;us-east&quot; e &quot;eu&quot; sono supportate da  Amazon Cognito.
   1. Assegna un nome e seleziona la casella &quot;Abilita accesso alle identità non autenticate&quot;.
   1. Nella pagina successiva (&quot;*Le identità Cognito richiedono l&#39;accesso alle risorse*&quot;) fare clic su Consenti.
   1. Nella parte superiore destra della pagina, fare clic sul collegamento &quot;*Modifica pool di identità&quot;*. Viene visualizzato l&#39;ID del pool di identità. Salvate il testo per un secondo tempo.
   1. Nella stessa pagina, scegliere il menu a discesa accanto a &quot;Ruolo non autenticato&quot; e assicurarsi che sia selezionato il ruolo Cognito_&lt;nome pool>UnauthRole. Salvare le modifiche.

1. **Configura accesso**

   1. Accedi a [Gestione identità e accesso](https://console.aws.amazon.com/iam/home) (IAM)
   1. Seleziona ruoli
   1. Fate clic sul ruolo creato nel passaggio precedente, denominato Cognito_&lt;yourIdentityPoolName>Unauth_Role. Registrare la voce &quot;Role ARN&quot; visualizzata.
   1. Apri &quot;Criteri in linea&quot; se non è già aperto. Dovresti visualizzare qui un criterio con un nome come oneClick_Cognito_&lt;yourIdentityPoolName>Unauth_Role_1234567890123.
   1. Fare clic su &quot;Edit Policy&quot;. Sostituisci il contenuto del documento criteri con questo frammento di JSON:

   <table>
    <tbody>
     <tr>
     <td><p> </p> <p>{</p> <p> "Versione": "2012-10-17",</p> <p> "Dichiarazione": [</p> <p> {</p> <p> "Azione": [</p> <p> "mobileanalytics:PutEvents",</p> <p> "cognito-sync:*",</p> <p> "SNS:CreatePlatformEndpoint",</p> <p> "SNS:Subscribe"</p> <p> ],</p> <p> "Effetto": "Allow",</p> <p> "Risorsa": [</p> <p> "*"</p> <p> ]</p> <p> }</p> <p> ]</p> <p>}</p> <p> </p> </td>
     </tr>
    </tbody>
    </table>

   1. Fare clic su **Applica criterio**


#### Utilizzo del servizio di messaggistica Pushwoosh {#using-the-pushwoosh-messaging-service}

Se non si desidera utilizzare Pushwoosh, è possibile saltare questo passaggio.

Per utilizzare Pushwoosh:

1. **Registrati con Pushwoosh**

   1. Passate a passeggwoosh.com e create un nuovo account.

1. **Creare un token di accesso API**

   1. Nel sito Pushwoosh, andate alla voce di menu Accesso API per generare un token di accesso API. Sarà necessario registrare in modo sicuro questo.

1. **Create una nuova app**

   1. Per il supporto di Android, dovete fornire la vostra chiave API GCM.
   1. Quando configurate l&#39;app, scegliete Cordova come framework.
   1. Per il supporto iOS, dovete fornire il file del certificato (.cer), il certificato push (.p12) e la password della chiave privata; questi avrebbero dovuto essere ottenuti dal sito APNS di Apple. Per Framework, scegliete Cordova.
   1. Pushwoosh genererà un App Id per quell&#39;app, nel modulo &quot;XXXXX-XXXXX&quot;, dove ogni X è un valore esadecimale (da 0 a F).

>[!NOTE]
>
>*Se una seconda app è configurata in AEM con lo stesso ID app (e altri valori correlati): Token di accesso API e ID GCM), tutte le notifiche push inviate tramite la seconda app in AEM andranno a qualsiasi altra app con tale ID app.*

### Passaggio 3: Aggiunta del supporto push all&#39;app {#step-add-push-support-to-the-app}

#### Aggiungi configurazione ContentSync {#add-contentsync-configuration}

Create due nodi di contenuto (uno in app-config e uno in app-config-dev) denominati notificationsConfig:

* /content/`<your app>`/shell/jcr:content/page-app/app-config-dev/notificationsConfig
* /content/`<your app>`/shell/jcr:content/page-app/app-config/notificationsConfig

Con queste proprietà (file .content.xml):
&lt;jcr:root xmlns:jcr=&quot; [https://www.jcp.org/jcr/1.0](https://www.jcp.org/jcr/1.0)&quot; xmlns:nt=&quot; [https://www.jcp.org/jcr/nt/1.0](https://www.jcp.org/jcr/nt/1.0)&quot;
jcr:PrimaryType=&quot;nt:unstructure&quot;
excludeProperties=&quot;[appAPIAccessToken]&quot;
path=&quot;../../../../..&quot;
targetRootDirectory=&quot;www&quot;
type=&quot;notifications sconfig&quot;/>

>[!NOTE]
>
>Il gestore di sincronizzazione dei contenuti cerca tali nodi e, se non sono presenti, non scrive il file page-notifications-config.json.

#### Aggiungi librerie client {#add-client-libraries}

Le librerie client di notifica push devono essere aggiunte all&#39;app attenendosi alla seguente procedura:

In CRXDE Lite:

1. Andate su */etc/designs/phonegap/&lt;nome app>/clientlibsall.*
1. Fare doppio clic sulla sezione Incorpora nel riquadro delle proprietà.
1. Nella finestra di dialogo visualizzata, aggiungere una nuova libreria client facendo clic sul pulsante +.
1. Nel nuovo campo di testo, aggiungete &quot;cq.mobile.push&quot; e fate clic su OK.
1. Aggiungete un’altra voce denominata cq.mobile.push.amazon e fate clic su OK.
1. Salva le modifiche.

>[!NOTE]
>
>Se le notifiche push vengono rimosse o non vengono utilizzate per considerazioni relative allo spazio nell&#39;app e per evitare messaggi di errore della console, rimuovete questi clientlibs dall&#39;app.

### Passaggio 4: Preparare un telefono per la verifica di {#step-prepare-a-phone-for-testing}

>[!NOTE]
>
>*Per le notifiche push, è necessario eseguire il test su un dispositivo effettivo, in quanto gli emulatori non sono in grado di ricevere le notifiche push.*

#### IOS {#ios}

Per iOS, è necessario utilizzare un computer Mac OS e partecipare al [iOS Developer Program](https://developer.apple.com/programs/ios/). Alcune società dispongono di licenze aziendali che possono essere disponibili a tutti gli sviluppatori.

Con XCode 8.1, prima di utilizzare le notifiche push è necessario passare alla scheda Capacità del progetto e attivare l&#39;opzione Notifiche push.

#### Android {#android}

Per installare l&#39;app su un telefono Android utilizzando CLI (vedi sotto): **Passaggio 6 - Creare e distribuire l&#39;app**), è innanzitutto necessario inserire il telefono in &quot;modalità sviluppatore&quot;. Per ulteriori informazioni, vedere [Abilitazione delle opzioni per gli sviluppatori sul dispositivo](https://developer.android.com/tools/device.html#developer-device-options).

### Passaggio 5: Configurare il push AEM app {#step-configure-push-on-aem-apps}

Prima di creare e distribuire il contenuto al dispositivo mobile configurato, dovete configurare le impostazioni di notifica per il servizio di messaggistica che avete deciso di utilizzare.

1. Create i gruppi di autorizzazione appropriati per le notifiche push.
1. Accedi a AEM come utente appropriato, fai clic sulla scheda App.
1. Fai clic sull&#39;app.
1. Trova la sezione Gestione Cloud Services e fai clic sulla matita per modificare le configurazioni cloud.
1. Selezionate  connessione Amazon SNS, connessione Pushwoosh o  Adobe Mobile Services come configurazione di notifica.
1. Immettete le proprietà del provider e fate clic su Invia per salvarle, quindi su Fine. In questa fase non sono verificati a distanza, salvo nel caso di AMS.
1. Ora dovresti vedere la configurazione appena inserita nella sezione Gestisci Cloud Services.

### Passaggio 6: Creazione e implementazione dell&#39;app {#step-build-and-deploy-the-app}

**Nota:** fare riferimento anche alle nostre istruzioni  [](/help/mobile/building-app-mobile-phonegap.md) qui sulla creazione di applicazioni PhoneGap.

Esistono due modi per creare e distribuire l&#39;app utilizzando PhoneGap.

**Nota:** per il test delle notifiche push, gli emulatori non saranno sufficienti perché le notifiche push utilizzano un protocollo distinto tra il provider push (Apple o Google) e il dispositivo. L&#39;hardware e gli emulatori Mac/PC correnti non supportano questa funzionalità.

1. *PhoneGap* Crea un servizio offerto da PhoneGap che creerà la vostra app per voi sui loro server e vi permetterà di scaricarla direttamente sul vostro dispositivo. Per informazioni su come impostare e utilizzare le PhoneGap Build, fare riferimento alla [documentazione sulle PhoneGap Build](https://build.phonegap.com/).

1. *L&#39;interfaccia*  CLI (Command Line Interface) di PhoneGap consente di utilizzare un set completo di comandi PhoneGap sulla riga di comando per creare, eseguire il debug e distribuire l&#39;app. Per informazioni su come impostare e utilizzare l&#39;interfaccia CLI di PhoneGap, fare riferimento alla [documentazione per gli sviluppatori di PhoneGap](https://docs.phonegap.com/en/edge/guide_cli_index.md.html#The%20Command-Line%20Interface).

### Passaggio 7: Invia una notifica push {#step-send-a-push-notification}

Per creare una nuova notifica e inviarla, effettuate le seguenti operazioni.

1. Creare una nuova notifica

   * Nel dashboard dell&#39;app  AEM Mobile, trova la sezione Notifiche push.
   * Nel menu in alto a destra, scegliete &quot;Crea&quot;. Questo pulsante sarà disponibile solo dopo che sarà stata impostata la configurazione cloud.
   * In Creazione guidata notifiche, inserire un titolo e un messaggio, quindi fare clic sul pulsante &quot;Crea&quot;. La notifica è ora pronta per l&#39;invio immediato o successivo. Può essere modificato e il messaggio e/o il titolo possono essere modificati e salvati.

1. Inviare la notifica

   * Nel dashboard App, trova la sezione Notifiche push.
   * Selezionate la notifica o fate clic sul pulsante dei dettagli in basso a destra (. . .), per visualizzare l&#39;elenco delle notifiche. Questo elenco indica anche se una notifica è pronta per essere inviata, se è già stata inviata o se si è verificato un errore durante l&#39;invio.
   * Selezionate la casella di controllo per una notifica (solo) e fate clic sul pulsante &quot;Invia notifica&quot; sopra l’elenco. Avrete una possibilità di annullare o inviare la notifica nella finestra di dialogo visualizzata.

1. Gestione dei risultati

   * Se il servizio di notifica push ( Amazon SNS o Pushwoosh) riceve la richiesta Invia, la conferma come valida e la invia correttamente ai provider nativi (APNS e GCM), la finestra di dialogo Invia si chiuderà senza messaggio. Nell&#39;elenco delle notifiche, lo stato di tale notifica è indicato come Inviato.
   * Se l&#39;invio push non riesce, nella finestra di dialogo viene visualizzato un messaggio che indica il problema. Nell&#39;elenco delle notifiche, lo stato di tale notifica viene elencato come Errore, ma se il problema viene risolto, la notifica può essere inviata di nuovo. In caso di errore, nel registro errori del server dovrebbero essere visualizzate informazioni aggiuntive sull&#39;errore.
   * Notate che ci sono alcune differenze di piattaforma tra le notifiche push di iOS e Android. Tra questi:

      * La creazione con CLI avvierà l&#39;app dopo che sarà stata distribuita su Android. Su iOS, è necessario avviarlo manualmente. Dal momento che il passaggio di registrazione push viene eseguito all&#39;avvio, le app Android possono ricevere notifiche push subito (perché saranno state avviate e registrate) mentre le app iOS no.
      * Su Android, il testo del pulsante OK si trova in tutte le didascalie (e in qualsiasi altro pulsante aggiunto alla notifica in-app), mentre in iOS non lo è.

Per le notifiche push AMS, le notifiche devono essere composte e inviate dal server AMS. AMS fornisce funzionalità aggiuntive di notifica push oltre a quelle fornite dalle notifiche AEM con AWS e Pushwoosh.

>[!NOTE]
>
>*Le notifiche push non sono garantite; sono più come annunci. Si fa il massimo sforzo per far sì che tutti lo sentano, ma non sono un meccanismo di consegna garantito. Inoltre, il tempo necessario per distribuire un push può variare da meno di un secondo a meno di mezz&#39;ora.*

### Configurazione dei collegamenti profondi con le notifiche push {#configuring-deep-linking-with-push-notifications}

Cos&#39;è il collegamento profondo? Nel contesto di una notifica push, si tratta di un mezzo per consentire l&#39;apertura o il reindirizzamento di un&#39;app (se aperta) a una posizione specifica all&#39;interno dell&#39;app.

Come funziona? L&#39;autore di una notifica push aggiunge facoltativamente un&#39;etichetta di pulsante (ad es. &quot;Mostrami!&quot;) alla notifica e sceglie la pagina che desiderano collegare nella notifica, tramite un browser del percorso visivo. Quando viene inviata, la notifica push viene eseguita come normale, tranne per il fatto che nel messaggio in-app, il pulsante OK viene sostituito da un pulsante &quot;Dismiss&quot; e il nuovo pulsante specificato (&quot;Show me!&quot;) appare anche. Facendo clic sul nuovo pulsante l&#39;app passerà alla pagina specificata all&#39;interno dell&#39;app. Fai clic su Ignora per chiudere il messaggio.

Se l&#39;app non è aperta, l&#39;ombreggiatura verrà visualizzata come normale. Intervenendo sulla notifica all’ombra, l’app viene aperta e gli vengono quindi presentati i pulsanti di collegamento profondo in base alla configurazione della notifica push.

Crea la notifica, aggiungi il testo di un pulsante e il percorso di collegamento per il collegamento profondo facoltativo:

>[!CAUTION]
>
>.Per accedere al riquadro delle notifiche push nel dashboard, segui i passaggi descritti di seguito.

1. Fate clic sulla modifica nell&#39;angolo superiore destro della sezione **Gestisci Cloud Services**.

   ![chlimage_1-108](assets/chlimage_1-108.png)

1. Selezionare la **Connessione Pushwoosh**. Fai clic su **Avanti**.

   ![chlimage_1-109](assets/chlimage_1-109.png)

1. Immettete i dettagli delle proprietà e fate clic su **Invia**.

   ![chlimage_1-110](assets/chlimage_1-110.png)

   Una volta inviata la configurazione, la sezione **Notifiche push** viene visualizzata nel dashboard.

   ![chlimage_1-111](assets/chlimage_1-111.png)

### Creazione guidata notifica {#create-notification-wizard}

Quando la sezione **Notifiche push** viene visualizzata nel dashboard, utilizzate la procedura guidata di creazione delle notifiche per aggiungere il contenuto:

1. Fare clic sul simbolo di aggiunta nell&#39;angolo superiore destro della sezione **Notifiche push** per aprire la **Creazione guidata notifiche**.

   ![chlimage_1-112](assets/chlimage_1-112.png)

1. Facendo clic sull&#39;icona Sfoglia nel percorso del collegamento, l&#39;utente viene presentato con la struttura del contenuto dell&#39;app.

   Dopo aver selezionato il percorso, fate clic sull’icona di controllo.

   ![chlimage_1-113](assets/chlimage_1-113.png)

   >[!NOTE]
   >
   >Il testo del pulsante di collegamento è limitato a 20 caratteri.
   >
   >Se l&#39;utente finale non dispone della versione più recente dell&#39;applicazione e il percorso collegato non è disponibile, la conferma dell&#39;azione del collegamento profondo porterà l&#39;utente nella pagina principale dell&#39;app.

1. Immettere i **Dettagli testo** nella **Creazione guidata notifica** e fare clic su **Crea**.

   ![chlimage_1-114](assets/chlimage_1-114.png)

   Aprite i dettagli facendo clic sulla notifica push creata dalla sezione **Notifiche push**.

   Potete modificare le proprietà, inviare notifiche o eliminare la notifica.

   ![chlimage_1-115](assets/chlimage_1-115.png)

>[!NOTE]
>
>**Informazioni aggiuntive**:
>
>Pushwoosh e  Amazon SNS non saranno supportati dopo la versione 6.4 e saranno disponibili come componente aggiuntivo dalla condivisione del pacchetto.

### Passaggi successivi {#the-next-steps}

Una volta inclusi i dettagli sulle notifiche push per la tua app, vedi [ AEM Mobile Content Personalization](/help/mobile/phonegap-aem-mobile-content-personalization.md).

