---
title: Creare l’app AEM Forms Android
description: Passaggi per configurare il progetto Android Studio e creare il file .apk per l’app AEM Forms per Android
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 3fb069cf-d3ed-47b0-b6bf-82e110b3b059
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 2%

---

# Creare l’app AEM Forms Android {#build-the-aem-forms-android-app}

Per creare l’app Android per AEM Forms, esegui i seguenti passaggi nella sequenza consigliata.

1. [Scarica il pacchetto di codice Source per app AEM Forms](#download-android-zip)
1. [Impostare le variabili di ambiente](#set-environment-variable-android)
1. [Creare un’app AEM Forms standard](#set-up-the-xcode-project)

## Scarica il pacchetto di codice Source per app AEM Forms {#download-android-zip}

Il pacchetto di codice Source per app AEM Forms fa riferimento all&#39;archivio `adobe-lc-mobileworkspace-src-<version>.zip`. Questo archivio include il codice sorgente necessario per creare un’app AEM Forms personalizzata. L&#39;archivio è incluso nel pacchetto `adobe-aemfd-forms-app-src-pkg-<version>.zip` disponibile in Software Distribution.

Per scaricare il file `adobe-aemfd-forms-app-src-pkg-<version>.zip`, effettuare le seguenti operazioni:

1. Apri [Software Distribution](https://experience.adobe.com/downloads). Per accedere a Software Distribution è necessario disporre di un Adobe ID.
1. Seleziona **[!UICONTROL Adobe Experience Manager]** disponibile nel menu intestazione.
1. Nella sezione **[!UICONTROL Filtri]**:
   1. Selezionare **[!UICONTROL Forms]** dall&#39;elenco a discesa **[!UICONTROL Soluzione]**.
   2. Seleziona la versione e digita per il pacchetto. Puoi anche utilizzare l&#39;opzione **[!UICONTROL Cerca download]** per filtrare i risultati.
1. Selezionare il nome del pacchetto applicabile al sistema operativo in uso, selezionare **[!UICONTROL Accetta termini EULA]** e selezionare **[!UICONTROL Scarica]**.
1. Apri [Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html) e fai clic su **[!UICONTROL Carica pacchetto]** per caricare il pacchetto.
1. Selezionare il pacchetto e fare clic su **[!UICONTROL Installa]**.
1. Per scaricare l&#39;archivio del codice sorgente, apri **https://&lt;server>:&lt;port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-&lt;version>.zip** nel browser. Il file .zip dell’app Android viene scaricato sul tuo dispositivo.
1. Estrarre il contenuto del file .zip in una cartella del file system locale. Ad esempio, *C:\&lt;Struttura cartella>\adobe-lc-mobileworkspace-src-2.4.20*

Nell&#39;immagine seguente viene visualizzata la struttura della cartella `adobe-lc-mobileworkspace-src-<version>.zip\android`.

![zip_android_folder_structure](assets/zip_android_folder_structure.png)

## Impostare le variabili di ambiente {#set-environment-variable-android}

Imposta le seguenti variabili di ambiente prima di avviare il processo di build per l’app AEM Forms:

* Impostare la variabile di ambiente JAVA_HOME sulla posizione del software JDK nel file system locale. Ad esempio, C:\Program Files\Java\jdk1.8.0_181
* Impostare la variabile di ambiente di sistema `ANDROID_SDK_ROOT` sulla posizione SDK per Android. Ad esempio, C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk
* Impostare la variabile di ambiente di sistema `Path` per includere i percorsi delle cartelle degli strumenti e degli strumenti di Platform per Android. Ad esempio, C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\platform-tools e C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\tools.

## Creare un’app AEM Forms standard {#set-up-the-xcode-project}

Dopo aver salvato il file adobe-lc-mobileworkspace-src-&lt;versione>.zip sul file system locale e aver impostato le variabili di ambiente, crea un’app AEM Forms Android standard utilizzando una delle opzioni seguenti:

* [Creare un’app AEM Forms con Android Studio](#using-android-studio)
* [Generare il file .apk con Android Studio](#generate-apk-android-studio)

### Creare un’app AEM Forms con Android Studio {#using-android-studio}

Per creare un’app AEM Forms con Android Studio, effettua le seguenti operazioni:

1. Avvia l&#39;applicazione Android Studio sul computer.
1. Fai clic su **Apri un progetto Android Studio esistente**. Se la finestra di dialogo per aprire un progetto esistente non viene visualizzata automaticamente, selezionare **File** > **Apri**.
1. Passa a *adobe-lc-mobileworkspace-src-&lt;versione>.zip/android* nel file system locale e fai clic su **OK**.

   L&#39;opzione **android** è visualizzata nel riquadro a sinistra.

   ![android_folder_studio](assets/android_folder_studio.png)

1. Seleziona **android** dal riquadro a sinistra e fai clic su **Esegui** > **Esegui &#39;android&#39;**.
1. Seleziona il dispositivo Android dalla sezione Dispositivi collegati della finestra di dialogo Seleziona destinazione di distribuzione e fai clic su OK.

   Una volta creato correttamente l’ambiente di sviluppo, puoi applicare le personalizzazioni all’app. Utilizza i seguenti articoli per personalizzare l’app:

   * [Personalizzazione branding](/help/forms/using/branding-customization.md)
   * [Personalizzazione tema](/help/forms/using/theme-customization.md)
   * [Personalizzazione movimento](/help/forms/using/gesture-customization.md)

   Dopo aver applicato le personalizzazioni appropriate all’app, puoi generare il file .apk per la distribuzione.

### Generare il file .apk con Android Studio {#generate-apk-android-studio}

Per generare il file apk con Android Studio, effettuate le seguenti operazioni:

1. Avvia l&#39;applicazione Android Studio sul computer.
1. Seleziona **Apri un progetto Android Studio esistente**. Se la finestra di dialogo per aprire un progetto esistente non viene visualizzata automaticamente, selezionare **File** > **Apri**.
1. Passa a *adobe-lc-mobileworkspace-src-&lt;versione>.zip/android* nel file system locale e fai clic su **OK**.

   L’opzione Android viene visualizzata nel riquadro a sinistra.

1. Per generare il file apk, selezionare **Build** > **Build APK**.

   Facoltativamente, selezionare **Build** > **Generate Signed APK** per generare una [versione firmata](https://developer.android.com/studio/publish/app-signing) del file .apk.

## Utilizzare Android Debug Bridge {#build-android-debug-bridge}

Una volta generato il file apk, eseguire il comando seguente per installare l&#39;applicazione su un dispositivo Android utilizzando [Android Debug Bridge](https://developer.android.com/tools/adb).

**Utenti Windows:** `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`

**Utenti Mac:** `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`
