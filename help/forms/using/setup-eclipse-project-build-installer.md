---
title: Creare l’app Android di AEM Forms
description: Passaggi per configurare il progetto Android Studio e creare il file .apk per l’app AEM Forms per Android
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 3fb069cf-d3ed-47b0-b6bf-82e110b3b059
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 2%

---

# Creare l’app Android di AEM Forms {#build-the-aem-forms-android-app}

Per creare l’app Android per AEM Forms, effettua le seguenti operazioni nella sequenza consigliata.

1. [Scarica il pacchetto del codice sorgente dell’app AEM Forms](#download-android-zip)
1. [Impostare le variabili di ambiente](#set-environment-variable-android)
1. [Creare un’app AEM Forms standard](#set-up-the-xcode-project)

## Scarica il pacchetto del codice sorgente dell’app AEM Forms {#download-android-zip}

Il pacchetto del codice sorgente dell’app AEM Forms fa riferimento al `adobe-lc-mobileworkspace-src-<version>.zip` archivio. Questo archivio include il codice sorgente necessario per creare un’app AEM Forms personalizzata. L&#39;archivio è incluso nel `adobe-aemfd-forms-app-src-pkg-<version>.zip`disponibile nella pagina Distribuzione di software.

Per scaricare `adobe-aemfd-forms-app-src-pkg-<version>.zip` file, effettuare le seguenti operazioni:

1. Apri [Software Distribution](https://experience.adobe.com/downloads). Per accedere a Software Distribution è necessario disporre di un Adobe ID.
1. Seleziona **[!UICONTROL Adobe Experience Manager]** disponibile nel menu di intestazione.
1. In **[!UICONTROL Filtri]** sezione:
   1. Seleziona **[!UICONTROL Forms]** dal **[!UICONTROL Soluzione]** elenco a discesa.
   2. Seleziona la versione e digita per il pacchetto. È inoltre possibile utilizzare **[!UICONTROL Cerca download]** per filtrare i risultati.
1. Selezionare il nome del pacchetto applicabile al sistema operativo in uso, quindi selezionare **[!UICONTROL Accetta termini EULA]**, e seleziona **[!UICONTROL Scarica]**.
1. Apri [Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)  e fai clic su **[!UICONTROL Carica pacchetto]** per caricare il pacchetto.
1. Seleziona il pacchetto e fai clic su **[!UICONTROL Installa]**.
1. Per scaricare l’archivio del codice sorgente, apri **https://&lt;server>:&lt;port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-&lt;version>.zip** nel browser. Il file .zip dell’app Android viene scaricato sul dispositivo.
1. Estrarre il contenuto del file .zip in una cartella del file system locale. Ad esempio: *C:\&lt;folder structure=&quot;&quot;>\adobe-lc-mobileworkspace-src-2.4.20*

L&#39;immagine seguente mostra la struttura del `adobe-lc-mobileworkspace-src-<version>.zip\android`cartella.

![zip_android_folder_structure](assets/zip_android_folder_structure.png)

## Impostare le variabili di ambiente {#set-environment-variable-android}

Imposta le seguenti variabili di ambiente prima di avviare il processo di build per l’app AEM Forms:

* Impostare la variabile di ambiente JAVA_HOME sulla posizione del software JDK nel file system locale. Ad esempio, C:\Program Files\Java\jdk1.8.0_181
* Imposta il `ANDROID_SDK_ROOT` variabile di ambiente di sistema alla posizione SDK per Android. Ad esempio, C:\Users\&amp;lt;username>\AppData\Local\Android\Sdk
* Imposta il `Path` variabile di ambiente di sistema per includere i percorsi delle cartelle degli strumenti e degli strumenti di Platform per Android. Ad esempio, C:\Users\&amp;lt;nomeutente>\AppData\Local\Android\Sdk\platform-tools e C:\Users\&amp;lt;nomeutente>\AppData\Local\Android\Sdk\tools.

## Creare un’app AEM Forms standard {#set-up-the-xcode-project}

Dopo aver salvato adobe-lc-mobileworkspace-src-&lt;version>.zip sul file system locale e di impostare le variabili di ambiente, crea un’app AEM Forms Android standard utilizzando una delle seguenti opzioni:

* [Creare un’app AEM Forms con Android Studio](#using-android-studio)
* [Generare il file .apk con Android Studio](#generate-apk-android-studio)

### Creare un’app AEM Forms con Android Studio {#using-android-studio}

Per creare un’app AEM Forms con Android Studio, effettua le seguenti operazioni:

1. Avvia l&#39;applicazione Android Studio sul computer.
1. Clic **Apri un progetto Android Studio esistente**. Se la finestra di dialogo per aprire un progetto esistente non viene visualizzata automaticamente, selezionare **File** > **Apri**.
1. Accedi a *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* nel file system locale e fare clic su **OK**.

   Il **androide** nel riquadro a sinistra.

   ![android_folder_studio](assets/android_folder_studio.png)

1. Seleziona **androide** dal riquadro di sinistra e fare clic su **Esegui** > **Esegui &quot;android&quot;**.
1. Seleziona il dispositivo Android dalla sezione Dispositivi collegati della finestra di dialogo Seleziona destinazione di distribuzione e fai clic su OK.

   Una volta creato correttamente l’ambiente di sviluppo, puoi applicare le personalizzazioni all’app. Utilizza i seguenti articoli per personalizzare l’app:

   * [Personalizzazione branding](/help/forms/using/branding-customization.md)
   * [Personalizzazione tema](/help/forms/using/theme-customization.md)
   * [Personalizzazione movimento](/help/forms/using/gesture-customization.md)

   Dopo aver applicato le personalizzazioni appropriate all’app, puoi generare il file .apk per la distribuzione.

### Generare il file .apk con Android Studio {#generate-apk-android-studio}

Per generare il file .apk con Android Studio, effettuate le seguenti operazioni:

1. Avvia l&#39;applicazione Android Studio sul computer.
1. Seleziona **Apri un progetto Android Studio esistente**. Se la finestra di dialogo per aprire un progetto esistente non viene visualizzata automaticamente, selezionare **File** > **Apri**.
1. Accedi a *adobe-lc-mobileworkspace-src-&lt;version>.zip/android* nel file system locale e fare clic su **OK**.

   L’opzione Android viene visualizzata nel riquadro a sinistra.

1. Per generare il file apk, selezionare **Genera** > **Genera APK**.

   Facoltativamente, seleziona **Genera** > **Genera APK firmato** per generare un [versione firmata](https://developer.android.com/studio/publish/app-signing) del file .apk.

## Usa Bridge di debug Android {#build-android-debug-bridge}

Una volta generato il file .apk, esegui il seguente comando per installare l’applicazione su un dispositivo Android utilizzando [Bridge di debug Android](https://developer.android.com/tools/adb).

**Utenti Windows:** `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`

**Utenti Mac:** `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`
