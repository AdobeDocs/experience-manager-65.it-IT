---
title: Creare l'app AEM Forms Android
seo-title: Creare l'app AEM Forms Android
description: Passaggi per configurare il progetto Android Studio e creare il file .apk per l'app AEM Forms per Android
seo-description: Passaggi per configurare il progetto Android Studio e creare il file .apk per l'app AEM Forms per Android
uuid: 2e140aaf-5be5-4d5d-9941-9d1f4bf2debd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: f5d6d9bd-4f36-4a4f-8008-15fb853a9219
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Creare l&#39;app AEM Forms Android {#build-the-aem-forms-android-app}

Per creare l&#39;app Android per AEM Forms, effettuate i seguenti passaggi nella sequenza consigliata.

1. [Scarica il pacchetto di codice sorgente dell’app AEM Forms](/help/forms/using/setup-eclipse-project-build-installer.md#main-pars-header-277929160)
1. [Impostare le variabili di ambiente](/help/forms/using/setup-eclipse-project-build-installer.md#main-pars-header-111803610)
1. [Creare app AEM Forms standard](/help/forms/using/setup-eclipse-project-build-installer.md#main-pars-heading-0)

## Scarica il pacchetto di codice sorgente dell’app AEM Forms {#download-android-zip}

Il pacchetto del codice sorgente dell’app AEM Forms fa riferimento all’ `adobe-lc-mobileworkspace-src-<version>.zip` archivio. Questo archivio include il codice sorgente richiesto per creare un&#39;app AEM Forms personalizzata. L&#39;archivio è incluso nel `adobe-aemfd-forms-app-src-pkg-<version>.zip`pacchetto disponibile nella condivisione del pacchetto.

Per scaricare il `adobe-aemfd-forms-app-src-pkg-<version>.zip` file, effettuate le seguenti operazioni:

1. Accedete all’istanza di creazione del server [](Http://localhost:4502/) AEM come amministratore e aprite la condivisione [del](http://localhost:4502/crx/packageshare)pacchetto. È necessario un Adobe ID per accedere alla condivisione del pacchetto.
1. In Condivisione [pacchetti](http://localhost:4502/crx/packageshare/login.html)AEM, eseguite una ricerca `adobe-aemfd-forms-app-src-pkg-<version>.zip`, fate clic sul pacchetto applicabile al sistema operativo in uso e fate clic su **Scarica**. Leggere e accettare il contratto di licenza e fare clic su **OK**. Il download viene avviato. Una volta scaricata, accanto al pacchetto viene visualizzata la parola **Download** .
1. Al termine del download, fate clic su **Scaricato**. Viene reindirizzato a Gestione pacchetti. In Gestione pacchetti, eseguite una ricerca nel pacchetto scaricato e fate clic su **Installa**.
1. Per scaricare l’archivio del codice sorgente, aprite **https://&lt;server>:&lt;porta>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-&lt;versione>.zip** nel browser. Il file .zip dell&#39;app Android viene scaricato sul dispositivo.
1. Estrarre il contenuto del file .zip in una cartella del file system locale. Ad esempio, *C:\&amp;lt;Folder Structure>\adobe-lc-mobileworkspace-src-2.4.20*

Nell’immagine seguente viene visualizzata la struttura della `adobe-lc-mobileworkspace-src-<version>.zip\android`cartella.

![zip_android_folder_structure](assets/zip_android_folder_structure.png)

## Impostare le variabili di ambiente {#set-environment-variable-android}

Impostate le seguenti variabili di ambiente prima di avviare il processo di creazione per l&#39;app AEM Forms:

* Impostare la variabile di ambiente JAVA_HOME sul percorso del software JDK nel file system locale. Ad esempio, C:\Program Files\Java\jdk1.8.0_181
* Impostate la variabile di ambiente del `ANDROID_SDK_ROOT` sistema sul percorso SDK per Android. Ad esempio, C:\Users\&amp;lt;nomeutente>\AppData\Local\Android\Sdk
* Impostate la variabile di ambiente del `Path` sistema in modo che includa le posizioni delle cartelle platform-tools e tools per Android. Ad esempio, C:\Users\&amp;lt;nomeutente>\AppData\Local\Android\Sdk\platform-tools and C:\Users\&amp;lt;nomeutente>\AppData\Local\Android\Sdk\tools.

## Creare app AEM Forms standard {#set-up-the-xcode-project}

Dopo aver salvato il file adobe-lc-mobileworkspace-src-&lt;versione>.zip nel file system locale e aver impostato le variabili di ambiente, create l&#39;app standard AEM Forms Android utilizzando una delle seguenti opzioni:

* [Creare un&#39;app AEM Forms utilizzando Android Studio](/help/forms/using/setup-eclipse-project-build-installer.md#main-pars-header-1347434739)
* [Genera file .apk con Android Studio](/help/forms/using/setup-eclipse-project-build-installer.md#main-pars-header-0)

### Creare un&#39;app AEM Forms utilizzando Android Studio {#using-android-studio}

Per creare l&#39;app AEM Forms utilizzando Android Studio, effettuate le seguenti operazioni:

1. Avviate l&#39;applicazione Android Studio sul computer.
1. Fate clic su **Apri un progetto** Android Studio esistente. Se la finestra di dialogo per l&#39;apertura di un progetto esistente non viene visualizzata automaticamente, selezionare **File** > **Apri**.
1. Individuate *adobe-lc-mobileworkspace-src-&lt;versione>.zip/android* nel file system locale e fate clic su **OK**.

   L’opzione **android** viene visualizzata nel riquadro a sinistra.

   ![android_folder_studio](assets/android_folder_studio.png)

1. Selezionate **android** dal riquadro a sinistra e fate clic su **Esegui** > **Esegui &#39;android&#39;**.
1. Selezionate il dispositivo Android dalla sezione Dispositivi collegati della finestra di dialogo Seleziona destinazione di distribuzione, quindi fate clic su OK.

   Dopo aver creato con successo l&#39;ambiente di sviluppo, ora puoi applicare le personalizzazioni sull&#39;app. Utilizzate i seguenti articoli per personalizzare l&#39;app:

   * [Personalizzazione branding](/help/forms/using/branding-customization.md)
   * [Personalizzazione tema](/help/forms/using/theme-customization.md)
   * [Personalizzazione Gesti](/help/forms/using/gesture-customization.md)
   Dopo aver applicato le personalizzazioni appropriate all&#39;app, potete generare il file .apk per la distribuzione.

### Genera file .apk con Android Studio {#generate-apk-android-studio}

Per generare il file .apk utilizzando Android Studio, eseguite i seguenti passaggi:

1. Avviate l&#39;applicazione Android Studio sul computer.
1. Selezionate **Apri un progetto** Android Studio esistente. Se la finestra di dialogo per l&#39;apertura di un progetto esistente non viene visualizzata automaticamente, selezionare **File** > **Apri**.
1. Individuate *adobe-lc-mobileworkspace-src-&lt;versione>.zip/android* nel file system locale e fate clic su **OK**.

   L’opzione android viene visualizzata nel riquadro a sinistra.

1. Selezionate **Genera** > **Genera APK** per generare il file .apk.

   Se necessario, selezionate **Genera** > **Genera APK** con firma per generare una versione [](https://developer.android.com/studio/publish/app-signing) firmata del file .apk.

## Utilizzo di Android Debug Bridge {#build-android-debug-bridge}

Una volta generato il file .apk, eseguite il comando seguente per installare l&#39;applicazione su un dispositivo Android tramite [Android Debug Bridge](https://developer.android.com/tools/help/adb.html).

**Utenti Windows:** `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`

**Utenti MAC:** `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`
