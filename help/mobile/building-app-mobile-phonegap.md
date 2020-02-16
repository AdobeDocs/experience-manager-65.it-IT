---
title: Creazione di applicazioni mobili
seo-title: Creazione di applicazioni mobili
description: Questa pagina fornisce un articolo completo passo passo su come creare un'applicazione mobile utilizzando il codice disponibile da GitHub è disponibile qui. Create l'applicazione da installare su un dispositivo o simulatore per il test o per la pubblicazione negli app store. Potete creare applicazioni localmente utilizzando l'interfaccia della riga di comando PhoneGap o nel cloud utilizzando PhoneGap Build.
seo-description: Questa pagina fornisce un articolo completo passo passo su come creare un'applicazione mobile utilizzando il codice disponibile da GitHub è disponibile qui. Create l'applicazione da installare su un dispositivo o simulatore per il test o per la pubblicazione negli app store. Potete creare applicazioni localmente utilizzando l'interfaccia della riga di comando PhoneGap o nel cloud utilizzando PhoneGap Build.
uuid: 1ff6fe1a-24cc-4973-a2cd-8d356bc649b0
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: b2778086-8280-4306-bf3a-f6ec2a0e04df
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Creazione di applicazioni mobili{#building-mobile-applications}

>[!NOTE]
>
>Adobe consiglia di utilizzare SPA Editor per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Create l&#39;applicazione da installare su un dispositivo o un simulatore per il test o la pubblicazione negli app store. Potete creare applicazioni localmente utilizzando l&#39;interfaccia della riga di comando PhoneGap o nel cloud utilizzando PhoneGap Build.

Un articolo completo e dettagliato su come creare un’applicazione mobile utilizzando il codice disponibile da GitHub è disponibile [qui](https://helpx.adobe.com/experience-manager/using/aem62_mobile.html).

## Spostamento dell’applicazione nell’istanza Pubblica {#moving-the-application-to-the-publish-instance}

Spostate i file dell&#39;applicazione nell&#39;istanza di pubblicazione in modo da fornire gli aggiornamenti di contenuto alle istanze installate dell&#39;applicazione mobile e per creare l&#39;applicazione utilizzando il contenuto pubblicato. Le applicazioni sono composte da due rami nodo nella directory archivio:

* `/content/phonegap/apps/<application name>`: Pagine Web create e attivate dagli autori.
* `/content/phonegap/content/<application name>`: File di configurazione dell&#39;applicazione e configurazioni di Content Sync.

>[!NOTE]
>
>Se non spostate i file dell’applicazione nell’istanza di pubblicazione, gli autori del contenuto non possono aggiornare la cache di sincronizzazione dei contenuti.

È sufficiente spostare i file del `/content/phonegap/content/<application name>` ramo nell’istanza di pubblicazione. I file nel `/content/phonegap/apps/<application name>` ramo vengono spostati quando l&#39;autore attiva le pagine.

In AEM sono disponibili due metodi per spostare contenuti in blocco nell’istanza di pubblicazione:

* [Utilizzare il comando](/help/sites-authoring/publishing-pages.md) Attiva albero nella console di replica.
* [Create un pacchetto](/help/sites-administering/package-manager.md) che contenga il contenuto e replicate il pacchetto.

Ad esempio, viene creata un&#39;applicazione mobile denominata phonegapapp. Il seguente nodo deve essere spostato nell’istanza di pubblicazione: /content/phonegap/content/phonegapapp.

**** Suggerimento: Per spostare un pacchetto dall’istanza di creazione all’istanza di pubblicazione, usate il comando Replica del pacchetto.

![chlimage_1-16](assets/chlimage_1-16.png)

## Creazione utilizzando l&#39;interfaccia della riga di comando PhoneGap {#building-using-the-phonegap-command-line-interface}

Compilare l&#39;applicazione PhoneGap sul computer utilizzando l&#39;interfaccia CLI (Command-Line Interface) di PhoneGap. Per includere il contenuto AEM nell’applicazione, AEM crea un file ZIP che contiene il contenuto dell’applicazione mobile, le configurazioni di sincronizzazione dei contenuti e altre risorse necessarie. Scaricate il file ZIP e includetelo nella build.

### Preparazione dell’ambiente di creazione {#preparing-your-build-environment}

Per creare utilizzando l&#39;interfaccia CLI di PhoneGap, è necessario installare Node.js e l&#39;utility client PhoneGap. È necessaria una connessione Internet per eseguire la procedura seguente.

1. Scarica e installa [Node.js](https://nodejs.org/).
1. Aprite un terminale o un prompt dei comandi e immettete il comando seguente per installare l&#39;utility PhoneGap:

   ```shell
   npm install -g phonegap
   ```

   Su un sistema Unix o Linux, potrebbe essere necessario preimpostare il comando con `sudo`.

   Il terminale mostra i risultati di una serie di comandi HTTP GET. Quando l&#39;installazione ha esito positivo, il terminale mostra dove sono installate le librerie, in modo simile al seguente esempio:

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

1. (Facoltativo) Ottenete l’SDK per la piattaforma mobile di destinazione:

   * Per creare app per la piattaforma iOS, installate la versione più recente di [Xcode](https://developer.apple.com/xcode/).
   * Per creare app Android, installate l&#39;SDK [](https://developer.android.com/)Android.

### Download del file ZIP del contenuto {#downloading-the-content-zip-file}

Sposta il contenuto dell’applicazione mobile nel file system.

1. Nella pagina Applicazioni mobili, seleziona l’applicazione.
1. (Facoltativo) Per creare l&#39;applicazione per installazioni complete, sulla barra degli strumenti, fate clic o toccate l&#39;icona Cancella cache.

   ![](do-not-localize/chlimage_1.png)

   >[!NOTE]
   >
   >La cache contiene gli aggiornamenti di contenuto per le applicazioni installate. La cancellazione della cache annulla tutti gli aggiornamenti memorizzati nella cache.

1. Sulla barra degli strumenti, fai clic o tocca l&#39;icona Scarica risorse CLI.

   ![](do-not-localize/chlimage_1-1.png)

1. Dopo aver salvato il file ZIP, fate clic su Chiudi nella finestra di dialogo Successo.
1. Estrarre il contenuto del file ZIP.

### Utilizzo della CLI PhoneGap per la creazione {#using-the-phonegap-cli-to-build}

Utilizzare l&#39;interfaccia CLI di PhoneGap per compilare e installare l&#39;applicazione. Per informazioni sull&#39;utilizzo dell&#39;interfaccia CLI di PhoneGap, consulta la documentazione dell&#39;interfaccia [della riga di](https://docs.phonegap.com/en/3.0.0/guide_cli_index.md.html) comando di PhoneGap.

1. Aprite un terminale o un prompt dei comandi e modificate la directory corrente nel file ZIP dell&#39;applicazione scaricato. Ad esempio, quanto segue modifica la directory nel file ng-app-cli.1392137825303.zip:

   ```shell
   cd ~/Downloads/ng-app-cli.1392137825303
   ```

1. Immettete il comando phonegap per la piattaforma di destinazione. Ad esempio, il seguente comando crea l&#39;app per Android:

   ```shell
   phonegap build android
   ```

## Creazione tramite PhoneGap Build {#building-using-phonegap-build}

Utilizzate il servizio cloud PhoneGap per creare la vostra app. Per eseguire questa procedura, è innanzitutto necessario creare una configurazione PhoneGap Build.

### Connessione a PhoneGap Build {#connecting-to-phonegap-build}

Create una configurazione PhoneGap Build in modo da poter utilizzare i servizi PhoneGap Build da AEM. Specifica il nome utente e la password dell&#39;account PhoneGap Build che utilizzerai per creare le tue applicazioni mobili.

1. Aprite la pagina Strumenti. ([http://localhost:4502/tools.html](http://localhost:4502/tools.html)).
1. Nell’area Operazioni CQ, fate clic su Servizi cloud.
1. Fate clic sul collegamento Configura ora per PhoneGap Build.

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. Nella finestra di dialogo Crea configurazione, digitate un valore per la proprietà Titolo. Per impostazione predefinita, il valore della proprietà Name viene derivato dal titolo, tuttavia è possibile immettere un nome. Fate clic su Crea.
1. Nella finestra di dialogo Configurazione PhoneGap Build, digitate il nome utente e la password di PhoneGap Build, quindi fate clic su OK.

### Utilizzo di PhoneGap Build {#using-phonegap-build}

Inviate le risorse dell&#39;applicazione a PhoneGap Build per la compilazione per le varie piattaforme mobili.

1. Nella pagina Applicazioni mobili, apri l’applicazione mobile. ([http://localhost:4502/mobile.html/content/phonegap](http://localhost:4502/mobile.html/content/phonegap))
1. (Facoltativo) Per creare l&#39;applicazione per installazioni complete, selezionate l&#39;applicazione e fate clic sull&#39;icona Cancella cache.

   ![](do-not-localize/chlimage_1-2.png)

   >[!NOTE]
   >
   >La cache contiene gli aggiornamenti di contenuto per le applicazioni installate. La cancellazione della cache annulla tutti gli aggiornamenti memorizzati nella cache.

1. Selezionate la pagina iniziale, quindi fate clic sull&#39;icona Genera remoto.

   ![](do-not-localize/chlimage_1-3.png)

   **** Nota: La versione beta di AEM Beta non crea una notifica Inbox al termine della creazione.

1. Nella finestra di dialogo di successo, fate clic su PhoneGap Build per aprire la pagina Adobe PhoneGap Build all&#39;indirizzo [https://build.phonegap.com/apps](https://build.phonegap.com/apps). Se siete in attesa della visualizzazione dell&#39;app, potete controllare la pagina Stato [](https://status.build.phonegap.com/) di PhoneGap Build.

   Per informazioni sull&#39;installazione della build, consulta la Documentazione [di](https://docs.build.phonegap.com/en_US/3.1.0/#googtrans%28en%29)PhoneGap Build.

   >[!NOTE]
   >
   >Gli account PhoneGap Build gratuiti sono autorizzati per un&#39;applicazione privata. Le build PhoneGap non riescono se si sta creando un&#39;applicazione privata aggiuntiva.

### Passaggi successivi {#the-next-steps}

Il passaggio successivo al processo di creazione consiste nel conoscere la [struttura di un&#39;app](/help/mobile/phonegap-structure-an-app.md).
