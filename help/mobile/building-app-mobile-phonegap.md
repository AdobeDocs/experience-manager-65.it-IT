---
title: Creazione di applicazioni mobili
description: Questa pagina fornisce un articolo completo e dettagliato su come creare un’app mobile utilizzando il codice disponibile su GitHub. Crea l’applicazione da installare su un dispositivo o simulatore per test o per la pubblicazione in app store. Puoi creare applicazioni localmente utilizzando l'interfaccia della riga di comando di PhoneGap o nel cloud utilizzando PhoneGap Build.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 7c2e5ed8-9f8e-4a81-b736-589ef4089f29
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 0%

---

# Creazione di applicazioni mobili{#building-mobile-applications}

>[!NOTE]
>
>L’Adobe consiglia di utilizzare l’Editor SPA per i progetti che richiedono il rendering lato client basato su framework di applicazione a pagina singola (ad esempio, React). [Ulteriori informazioni](/help/sites-developing/spa-overview.md).

Crea l’applicazione da installare su un dispositivo o simulatore per test o per la pubblicazione in app store. Puoi creare applicazioni localmente utilizzando l&#39;interfaccia della riga di comando di PhoneGap o nel cloud utilizzando PhoneGap Build.

Un articolo completo e dettagliato su come creare un&#39;app mobile utilizzando il codice disponibile da GitHub è disponibile [qui](https://helpx.adobe.com/experience-manager/using/aem62_mobile.html).

## Spostamento dell’applicazione nell’istanza di Publish {#moving-the-application-to-the-publish-instance}

Sposta i file dell’applicazione nell’istanza di pubblicazione in modo da poter fornire aggiornamenti del contenuto alle istanze installate dell’app mobile e da generare l’applicazione utilizzando il contenuto pubblicato. Le applicazioni sono costituite da due rami di nodo nell’archivio:

* `/content/phonegap/apps/<application name>`: pagine Web create e attivate dagli autori.
* `/content/phonegap/content/<application name>`: file di configurazione dell&#39;applicazione e configurazioni di sincronizzazione dei contenuti.

>[!NOTE]
>
>Se non sposti i file dell’applicazione nell’istanza di pubblicazione, gli autori di contenuto non possono aggiornare la cache di sincronizzazione contenuti.

È sufficiente spostare i file nel ramo `/content/phonegap/content/<application name>` nell&#39;istanza Publish. I file nel ramo `/content/phonegap/apps/<application name>` vengono spostati quando l&#39;autore attiva le pagine.

L’AEM fornisce due metodi per spostare contenuti in blocco nell’istanza Publish:

* [Utilizzare il comando Attiva struttura](/help/sites-authoring/publishing-pages.md) nella console di replica.
* [Creare un pacchetto](/help/sites-administering/package-manager.md) contenente il contenuto e replicare il pacchetto.

Ad esempio, viene creata un’app mobile denominata phonegapapp. Il seguente nodo deve essere spostato nell’istanza di pubblicazione: /content/phonegap/content/phonegapapp.

**Suggerimento:** Per spostare un pacchetto dall&#39;istanza di authoring all&#39;istanza di pubblicazione, utilizzare il comando Replica del pacchetto.

![chlimage_1-16](assets/chlimage_1-16.png)

## Generazione tramite l&#39;interfaccia della riga di comando PhoneGap {#building-using-the-phonegap-command-line-interface}

Compilare l&#39;applicazione PhoneGap sul computer utilizzando l&#39;interfaccia della riga di comando (CLI) di PhoneGap. Per includere il contenuto dell’AEM nell’applicazione, AEM crea un file ZIP contenente il contenuto dell’app mobile, le configurazioni di sincronizzazione dei contenuti e altre risorse richieste. Scarica il file ZIP e includilo nella build.

### Preparazione dell’ambiente di build {#preparing-your-build-environment}

Per generare utilizzando PhoneGap CLI, è necessario installare Node.js e l’utility client PhoneGap. Per eseguire la procedura seguente è necessaria una connessione Internet.

1. Scarica e installa [Node.js](https://nodejs.org/en).
1. Apri un terminale o un prompt dei comandi e immetti il seguente comando del nodo per installare l&#39;utility PhoneGap:

   ```shell
   npm install -g phonegap
   ```

   In un sistema UNIX® o Linux®, potrebbe essere necessario anteporre al comando il prefisso `sudo`.

   Il terminale mostra i risultati di una serie di comandi HTTP GET. Quando l’installazione ha esito positivo, il terminale mostra dove vengono installate le librerie in modo simile all’esempio seguente:

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

1. (Facoltativo) Ottieni l’SDK per la piattaforma mobile di destinazione:

   * Per creare app per la piattaforma iOS, installa la versione più recente di [Xcode](https://developer.apple.com/xcode/).
   * Per creare app Android™, installa l&#39;[SDK Android™](https://developer.android.com/).

### Download del file ZIP del contenuto {#downloading-the-content-zip-file}

Sposta il contenuto dell’app mobile nel file system.

1. Nella pagina Applicazioni mobili, seleziona l’applicazione.
1. (Facoltativo) Per creare l&#39;applicazione per installazioni complete, fare clic sull&#39;icona Cancella cache sulla barra degli strumenti.

   ![Icona Cancella cache indicata da un simbolo di collegamento interrotto.](do-not-localize/chlimage_1.png)

   >[!NOTE]
   >
   >La cache contiene gli aggiornamenti del contenuto per le applicazioni installate. La cancellazione della cache annulla tutti gli aggiornamenti memorizzati nella cache.

1. Sulla barra degli strumenti fare clic sull&#39;icona Scarica CLI Assets.

   ![Icona Download CLI Assets indicata dal simbolo del Tablet PC sovrapposto.](do-not-localize/chlimage_1-1.png)

1. Dopo aver salvato il file ZIP, fai clic su Chiudi nella finestra di dialogo Corretto.
1. Estrai il contenuto del file ZIP.

### Utilizzo di PhoneGap CLI per la generazione {#using-the-phonegap-cli-to-build}

Utilizza PhoneGap CLI per compilare e installare l’applicazione. Per informazioni sull&#39;utilizzo di PhoneGap CLI, vedere la documentazione relativa all&#39;interfaccia della riga di comando PhoneGap (`https://docs.phonegap.com/en/3.0.0/guide_cli_index.md.html`).

1. Apri un terminale o un prompt dei comandi e cambia la directory corrente con il file ZIP dell’applicazione scaricato. Ad esempio, la seguente modifica la directory nel file ng-app-cli.1392137825303.zip:

   ```shell
   cd ~/Downloads/ng-app-cli.1392137825303
   ```

1. Immetti il comando phonegap per la piattaforma di destinazione. Ad esempio, il comando seguente crea l’app per Android™:

   ```shell
   phonegap build android
   ```

## Edificio Con PhoneGap Build {#building-using-phonegap-build}

Usa il servizio cloud PhoneGap per creare la tua app. Per eseguire questa procedura, è necessario innanzitutto creare una configurazione di PhoneGap Build.

### Connessione a PhoneGap Build {#connecting-to-phonegap-build}

Creare una configurazione di PhoneGap Build in modo da poter utilizzare i servizi PhoneGap Build dall&#39;AEM. Fornisci il nome utente e la password dell’account PhoneGap Build che utilizzerai per creare le tue app mobili.

1. Apri la pagina Strumenti. ([http://localhost:4502/tools.html](http://localhost:4502/tools.html)).
1. Nell&#39;area Operazioni CQ fare clic su Cloud Service.
1. Fare clic sul collegamento Configura ora per la PhoneGap Build.

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. Nella finestra di dialogo Crea configurazione digitare un valore per la proprietà Titolo. Per impostazione predefinita, il valore della proprietà Name è derivato dal titolo, tuttavia è possibile immettere un nome. Fai clic su Crea.
1. Nella finestra di dialogo Configurazione PhoneGap Build digitare il nome utente e la password della PhoneGap Build e quindi fare clic su OK.

### Utilizzo delle PhoneGap Build {#using-phonegap-build}

Invia le risorse della tua applicazione a PhoneGap Build per la compilazione per le varie piattaforme mobili.

1. Nella pagina Mobile Applications (Applicazioni mobili), apri l’app mobile. ([http://localhost:4502/mobile.html/content/phonegap](http://localhost:4502/mobile.html/content/phonegap))
1. (Facoltativo) Per creare l&#39;applicazione per installazioni complete, selezionarla e fare clic sull&#39;icona Cancella cache.

   ![Icona Cancella cache indicata da un simbolo di collegamento interrotto.](do-not-localize/chlimage_1-2.png)

   >[!NOTE]
   >
   >La cache contiene gli aggiornamenti del contenuto per le applicazioni installate. La cancellazione della cache annulla tutti gli aggiornamenti memorizzati nella cache.

1. Selezionare la pagina iniziale, quindi fare clic sull&#39;icona Genera remoto.

   ![Icona Genera remoto indicata da due ingranaggi di arrotondamento.](do-not-localize/chlimage_1-3.png)

   **Nota:** la versione Beta di AEM Beta non crea una notifica casella in entrata al completamento della compilazione.

1. Nella finestra di dialogo Operazione completata, fare clic su PhoneGap Build per aprire la pagina Adobe PhoneGap Build in `https://build.phonegap.com/apps`. Se stai aspettando che l&#39;app venga visualizzata, puoi controllare lo stato della PhoneGap Build in `https://status.build.phonegap.com/`.

   Per informazioni sull&#39;installazione della build, vedere la [documentazione della PhoneGap Build](https://github.com/phonegap/phonegap-docs/tree/master/docs/4-phonegap-build).

   >[!NOTE]
   >
   >Gli account di PhoneGap Build gratuiti sono consentiti in un&#39;applicazione privata. Le build di PhoneGap non riescono se si sta creando un&#39;ulteriore applicazione privata.

### Passaggi successivi {#the-next-steps}

Il passaggio successivo dopo il processo di compilazione è la conoscenza della [struttura di un&#39;app](/help/mobile/phonegap-structure-an-app.md).
