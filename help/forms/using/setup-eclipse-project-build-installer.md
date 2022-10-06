---
title: Creare l’app AEM Forms Android
seo-title: Build the AEM Forms Android app
description: Passaggi per configurare il progetto Android Studio e generare il file .apk per l’app AEM Forms per Android
seo-description: Steps to set up the Android Studio project and build the .apk file for the AEM Forms app for Android
uuid: 2e140aaf-5be5-4d5d-9941-9d1f4bf2debd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: f5d6d9bd-4f36-4a4f-8008-15fb853a9219
exl-id: 3fb069cf-d3ed-47b0-b6bf-82e110b3b059
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 6%

---

# Creare l’app AEM Forms Android {#build-the-aem-forms-android-app}

Esegui i seguenti passaggi nella sequenza consigliata per creare l’app Android per AEM Forms.

1. [Scarica il pacchetto del codice sorgente dell’app AEM Forms](#download-android-zip)
1. [Impostare le variabili di ambiente](#set-environment-variable-android)
1. [Creare un’app AEM Forms standard](#set-up-the-xcode-project)

## Scarica il pacchetto del codice sorgente dell’app AEM Forms {#download-android-zip}

Il pacchetto del codice sorgente dell&#39;app di AEM Forms si riferisce al `adobe-lc-mobileworkspace-src-<version>.zip` archivio. Questo archivio include il codice sorgente necessario per creare un’app AEM Forms personalizzata. L&#39;archivio è incluso nel `adobe-aemfd-forms-app-src-pkg-<version>.zip`disponibile nella Distribuzione di software.

Esegui i seguenti passaggi per scaricare il `adobe-aemfd-forms-app-src-pkg-<version>.zip` file:

1. Apri [Software Distribution](https://experience.adobe.com/downloads). Per accedere a Software Distribution è necessario disporre di un Adobe ID.
1. Tocca **[!UICONTROL Adobe Experience Manager]** che si trova nel menu di intestazione.
1. In **[!UICONTROL Filtri]** sezione:
   1. Seleziona **[!UICONTROL Forms]** dal **[!UICONTROL Soluzione]** elenco a discesa.
   2. Seleziona la versione e digita il pacchetto. È inoltre possibile utilizzare **[!UICONTROL Download di ricerca]** per filtrare i risultati.
1. Toccare il nome del pacchetto applicabile al sistema operativo in uso, selezionare **[!UICONTROL Accettare i termini dell&#39;EULA]**, e tocca **[!UICONTROL Scarica]**.
1. Apri [Gestione pacchetti](https://docs.adobe.com/content/help/it/experience-manager-65/administering/contentmanagement/package-manager.html) e fai clic su **[!UICONTROL Carica pacchetto]** per caricarlo.
1. Seleziona il pacchetto e fai clic su **[!UICONTROL Installa]**.
1. Per scaricare l&#39;archivio del codice sorgente, apri **https://&lt;server>:&lt;port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-&lt;version>.zip** nel browser. Il file .zip dell&#39;app Android viene scaricato sul tuo dispositivo.
1. Estrai il contenuto del file .zip in una cartella del file system locale. Ad esempio: *C:\&lt;folder structure=&quot;&quot;>\adobe-lc-mobileworkspace-src-2.4.20*

Nell&#39;immagine seguente viene visualizzata la struttura della `adobe-lc-mobileworkspace-src-<version>.zip\android`cartella.

![zip_android_folder_structure](assets/zip_android_folder_structure.png)

## Impostare le variabili di ambiente {#set-environment-variable-android}

Imposta le seguenti variabili d&#39;ambiente prima di avviare il processo di creazione per l&#39;app AEM Forms:

* Impostare la variabile di ambiente JAVA_HOME sul percorso del software JDK sul file system locale. Ad esempio, C:\Program Files\Java\jdk1.8.0_181
* Imposta la `ANDROID_SDK_ROOT` variabile di ambiente di sistema nella posizione SDK per Android. Ad esempio, C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk
* Imposta la `Path` variabile di ambiente del sistema per includere le posizioni della cartella platform-tools e tools per Android. Ad esempio, C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\platform-tools and C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk\tools.

## Creare un’app AEM Forms standard {#set-up-the-xcode-project}

Dopo aver salvato adobe-lc-mobileworkspace-src-&lt;version>.zip sul file system locale e imposta le variabili di ambiente, genera l&#39;app standard AEM Forms Android utilizzando una delle seguenti opzioni:

* [Creare un’app AEM Forms con Android Studio](#using-android-studio)
* [Genera file .apk utilizzando Android Studio](#generate-apk-android-studio)

### Creare un’app AEM Forms con Android Studio {#using-android-studio}

Esegui i seguenti passaggi per creare l’app AEM Forms utilizzando Android Studio:

1. Avvia l&#39;applicazione Android Studio sul computer.
1. Fai clic su **Apri un progetto Android Studio esistente**. Se la finestra di dialogo per aprire un progetto esistente non viene visualizzata automaticamente, seleziona **File** > **Apri**.
1. Passa a *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* sul file system locale e fare clic su **OK**.

   La **androide** nel riquadro a sinistra viene visualizzata l’opzione .

   ![android_folder_studio](assets/android_folder_studio.png)

1. Seleziona **androide** dal riquadro a sinistra e fai clic su **Esegui** > **Esegui &#39;android&#39;**.
1. Seleziona il dispositivo Android dalla sezione Dispositivi collegati della finestra di dialogo Seleziona destinazione distribuzione e fai clic su OK.

   Dopo aver creato correttamente l’ambiente di sviluppo, ora puoi applicare le personalizzazioni sull’app. Usa i seguenti articoli per personalizzare l’app:

   * [Personalizzazione branding](/help/forms/using/branding-customization.md)
   * [Personalizzazione del tema](/help/forms/using/theme-customization.md)
   * [Personalizzazione dei movimenti](/help/forms/using/gesture-customization.md)

   Dopo aver applicato le personalizzazioni appropriate alla tua app, puoi generare il file .apk da distribuire.

### Genera file .apk utilizzando Android Studio {#generate-apk-android-studio}

Esegui i seguenti passaggi per generare il file .apk utilizzando Android Studio:

1. Avvia l&#39;applicazione Android Studio sul computer.
1. Seleziona **Apri un progetto Android Studio esistente**. Se la finestra di dialogo per aprire un progetto esistente non viene visualizzata automaticamente, seleziona **File** > **Apri**.
1. Passa a *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* sul file system locale e fare clic su **OK**.

   L’opzione android viene visualizzata nel riquadro a sinistra.

1. Seleziona **Crea** > **Creare APK** per generare il file .apk.

   Facoltativamente, seleziona **Crea** > **Genera APK firmato** per generare un [versione firmata](https://developer.android.com/studio/publish/app-signing) del file .apk.

## Usa Bridge di debug Android {#build-android-debug-bridge}

Una volta generato il file .apk, esegui il seguente comando per installare l&#39;applicazione su un dispositivo Android utilizzando [Bridge di debug Android](https://developer.android.com/tools/help/adb.html).

**Utenti Windows:** `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`

**Utenti Mac:** `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`
