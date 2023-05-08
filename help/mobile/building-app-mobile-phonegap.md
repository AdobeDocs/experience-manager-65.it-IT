---
title: Creazione di applicazioni mobili
seo-title: Building Mobile Applications
description: Questa pagina fornisce un articolo completo passo passo su come creare un’app mobile utilizzando il codice disponibile da GitHub è disponibile qui. Crea la tua applicazione da installare su un dispositivo o simulatore per il test o per la pubblicazione negli app store. È possibile creare applicazioni localmente utilizzando l'interfaccia della riga di comando PhoneGap o nel cloud utilizzando la PhoneGap Build.
seo-description: This page provides a complete step-by-step article on how to build a mobile application using code available from GitHub is available here.Build your application to install to a device or simulator for testing or for publishing to app stores. You can build applications locally using the PhoneGap Command Line Interface, or in the cloud using PhoneGap Build.
uuid: 1ff6fe1a-24cc-4973-a2cd-8d356bc649b0
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: b2778086-8280-4306-bf3a-f6ec2a0e04df
exl-id: 7c2e5ed8-9f8e-4a81-b736-589ef4089f29
source-git-commit: 85d39e59b82fdfdcd310be61787a315668aebe38
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 1%

---

# Creazione di applicazioni mobili{#building-mobile-applications}

>[!NOTE]
>
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

Crea l&#39;applicazione da installare su un dispositivo o simulatore per il test o la pubblicazione negli app store. È possibile creare applicazioni localmente utilizzando l&#39;interfaccia della riga di comando PhoneGap o nel cloud utilizzando la PhoneGap Build.

È disponibile un articolo completo e dettagliato su come creare un’app mobile utilizzando il codice disponibile da GitHub. [qui](https://helpx.adobe.com/experience-manager/using/aem62_mobile.html).

## Spostamento dell’applicazione nell’istanza di pubblicazione {#moving-the-application-to-the-publish-instance}

Sposta i file dell’applicazione nell’istanza di pubblicazione in modo da poter fornire aggiornamenti di contenuto alle istanze installate dell’app mobile e da creare l’applicazione utilizzando il contenuto pubblicato. Le applicazioni sono costituite da due rami nodo nel repository:

* `/content/phonegap/apps/<application name>`: Le pagine web create e attivate dagli autori.
* `/content/phonegap/content/<application name>`: File di configurazione dell&#39;applicazione e configurazioni di Content Sync.

>[!NOTE]
>
>Se i file dell’applicazione non vengono spostati nell’istanza di pubblicazione, gli autori dei contenuti non possono aggiornare la cache di sincronizzazione dei contenuti.

Devi solo spostare i file nella `/content/phonegap/content/<application name>` nell’istanza di pubblicazione. I file nel `/content/phonegap/apps/<application name>` vengono spostati quando l’autore attiva le pagine.

AEM fornisce due metodi per spostare contenuti in blocco nell’istanza di pubblicazione:

* [Utilizzare il comando Attiva albero](/help/sites-authoring/publishing-pages.md) nella console di replica.
* [Creare un pacchetto](/help/sites-administering/package-manager.md) che contiene il contenuto e replica il pacchetto.

Ad esempio, viene creata un’app mobile denominata phonegapapp . Il seguente nodo deve essere spostato nell&#39;istanza di pubblicazione: /content/phonegap/content/phonegapapp.

**Suggerimento:** Per spostare un pacchetto dall’istanza di authoring all’istanza di pubblicazione, utilizza il comando Replica nel pacchetto.

![chlimage_1-16](assets/chlimage_1-16.png)

## Creazione tramite l’interfaccia della riga di comando PhoneGap {#building-using-the-phonegap-command-line-interface}

Compilare l’applicazione PhoneGap sul computer utilizzando l’interfaccia CLI (Command-Line Interface) di PhoneGap. Per includere il contenuto AEM nell’applicazione, AEM crea un file ZIP contenente il contenuto dell’app mobile, le configurazioni di sincronizzazione dei contenuti e altre risorse richieste. Scarica il file ZIP e includilo nella build.

### Preparazione dell’ambiente di creazione {#preparing-your-build-environment}

Per generare utilizzando PhoneGap CLI, è necessario installare Node.js e l&#39;utility client PhoneGap. È necessaria una connessione a Internet per eseguire la procedura seguente.

1. Scarica e installa [Node.js](https://nodejs.org/).
1. Apri un terminale o un prompt dei comandi e immetti il seguente comando del nodo per installare l&#39;utility PhoneGap:

   ```shell
   npm install -g phonegap
   ```

   Su un sistema Unix o Linux, potrebbe essere necessario impostare il prefisso del comando con `sudo`.

   Il terminale mostra i risultati di una serie di comandi HTTP GET. Quando l&#39;installazione è riuscita, il terminale mostra dove le librerie sono installate in modo simile al seguente esempio:

   ```xml
   /usr/local/bin/phonegap -> /usr/local/lib/node_modules/phonegap/bin/phonegap.js
   phonegap@3.3.0-0.19.6 /usr/local/lib/node_modules/phonegap
   ├── pluralize@0.0.4
   ├── colors@0.6.0-1
   ├── semver@1.1.0
   ├── qrcode-terminal@0.9.4
   ├── shelljs@0.1.4
   ├── optimist@0.6.0 (...)
   ├── prompt@0.2.11 (...)
   ├── phonegap-build@0.8.4 (...)
   ├── connect-phonegap@0.8.1 (...)
   └── cordova@3.3.0-0.1.1 (...)
   ```

1. (Facoltativo) Ottieni l&#39;SDK per la piattaforma mobile di destinazione:

   * Per creare app per la piattaforma iOS, installa la versione più recente di [Xcode](https://developer.apple.com/xcode/).
   * Per creare le app Android, installa la [SDK per Android](https://developer.android.com/).

### Download del file ZIP del contenuto {#downloading-the-content-zip-file}

Sposta il contenuto dell’app mobile nel file system.

1. Nella pagina Applicazioni mobili , seleziona l’applicazione.
1. (Facoltativo) Per creare l&#39;applicazione per installazioni complete, sulla barra degli strumenti tocca o fai clic sull&#39;icona Cancella cache .

   ![](do-not-localize/chlimage_1.png)

   >[!NOTE]
   >
   >La cache contiene gli aggiornamenti di contenuto per le applicazioni installate. La cancellazione della cache annulla tutti gli aggiornamenti memorizzati nella cache.

1. Sulla barra degli strumenti, tocca o fai clic sull’icona Scarica risorse CLI .

   ![](do-not-localize/chlimage_1-1.png)

1. Dopo aver salvato il file ZIP, fai clic su Chiudi nella finestra di dialogo Riuscito.
1. Estrai il contenuto del file ZIP.

### Utilizzo della CLI di PhoneGap per generare {#using-the-phonegap-cli-to-build}

Utilizza la CLI di PhoneGap per compilare e installare l&#39;applicazione. Per informazioni su come utilizzare PhoneGap CLI, consulta PhoneGap [Interfaccia a riga di comando](https://docs.phonegap.com/en/3.0.0/guide_cli_index.md.html) documentazione.

1. Apri un terminale o un prompt dei comandi e modifica la directory corrente nel file ZIP dell&#39;applicazione scaricato. Ad esempio, la directory seguente viene modificata nel file ng-app-cli.1392137825303.zip:

   ```shell
   cd ~/Downloads/ng-app-cli.1392137825303
   ```

1. Immetti il comando phonegap per la piattaforma di destinazione. Ad esempio, il seguente comando crea l&#39;app per Android:

   ```shell
   phonegap build android
   ```

## Costruzione con PhoneGap Build {#building-using-phonegap-build}

Utilizza il servizio cloud PhoneGap per creare la tua app. Per eseguire questa procedura, è innanzitutto necessario creare una configurazione di PhoneGap Build.

### Connessione a PhoneGap Build {#connecting-to-phonegap-build}

Crea una configurazione di PhoneGap Build in modo da poter utilizzare i servizi PhoneGap Build da AEM. Immetti il nome utente e la password dell&#39;account PhoneGap Build che utilizzerai per creare le tue applicazioni mobili.

1. Apri la pagina Strumenti . ([http://localhost:4502/tools.html](http://localhost:4502/tools.html)).
1. Nell’area Operazioni CQ, fare clic su Cloud Services.
1. Fare clic sul collegamento Configura ora per la PhoneGap Build.

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. Nella finestra di dialogo Crea configurazione, digita un valore per la proprietà Titolo . Per impostazione predefinita, il valore della proprietà Name viene derivato dal titolo, tuttavia è possibile immettere un nome. Fai clic su Crea.
1. Nella finestra di dialogo Configurazione PhoneGap Build digitare il nome utente e la password della PhoneGap Build e quindi fare clic su OK.

### Utilizzo delle PhoneGap Build {#using-phonegap-build}

Invia le risorse dell&#39;applicazione a PhoneGap Build per la compilazione per le varie piattaforme mobili.

1. Nella pagina Applicazioni mobili , apri l’app mobile. ([http://localhost:4502/mobile.html/content/phonegap](http://localhost:4502/mobile.html/content/phonegap))
1. (Facoltativo) Per creare l&#39;applicazione per installazioni complete, seleziona l&#39;applicazione e fai clic sull&#39;icona Cancella cache.

   ![](do-not-localize/chlimage_1-2.png)

   >[!NOTE]
   >
   >La cache contiene gli aggiornamenti di contenuto per le applicazioni installate. La cancellazione della cache annulla tutti gli aggiornamenti memorizzati nella cache.

1. Selezionare la pagina iniziale, quindi fare clic sull&#39;icona Genera remoto.

   ![](do-not-localize/chlimage_1-3.png)

   **Nota:** La versione beta di AEM Beta non crea una notifica in entrata al completamento della build.

1. Nella finestra di dialogo Completato fare clic su PhoneGap Build per aprire la pagina Adobe PhoneGap Build in [https://build.phonegap.com/apps](https://build.phonegap.com/apps). Se sei in attesa che appaia l’app, puoi controllare la [Stato PhoneGap Build](https://status.build.phonegap.com/) pagina.

   Per informazioni sull’installazione della build, consulta la sezione [Documentazione PhoneGap Build](https://github.com/phonegap/phonegap-docs/tree/master/docs/4-phonegap-build).

   >[!NOTE]
   >
   >Gli account di PhoneGap Build gratuiti sono consentiti un&#39;applicazione privata. Le build di PhoneGap non riescono se si sta creando un&#39;applicazione privata aggiuntiva.

### Passaggi successivi {#the-next-steps}

Il passo successivo al processo di costruzione è imparare [Struttura di un’app](/help/mobile/phonegap-structure-an-app.md).
