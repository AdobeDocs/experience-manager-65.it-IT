---
title: Creare l'app  AEM Forms Android
seo-title: Creare l'app  AEM Forms Android
description: Passaggi per configurare il progetto Android Studio e creare il file .apk per l'app AEM Forms  per Android
seo-description: Passaggi per configurare il progetto Android Studio e creare il file .apk per l'app AEM Forms  per Android
uuid: 2e140aaf-5be5-4d5d-9941-9d1f4bf2debd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: f5d6d9bd-4f36-4a4f-8008-15fb853a9219
translation-type: tm+mt
source-git-commit: 1dfc8fa91d3e5ae8ca49cf1f3cb739b59feb18cf
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 0%

---


# Creare l&#39;app AEM Forms Android  {#build-the-aem-forms-android-app}

Effettuate i seguenti passaggi nella sequenza consigliata per creare l&#39;app Android per  AEM Forms.

1. [Scarica il pacchetto  codice sorgente dell&#39;app AEM Forms](#download-android-zip)
1. [Impostare le variabili di ambiente](#set-environment-variable-android)
1. [Creare app standard  AEM Forms](#set-up-the-xcode-project)

## Scarica il pacchetto  codice sorgente dell&#39;app AEM Forms {#download-android-zip}

 pacchetto codice sorgente app AEM Forms fa riferimento all&#39;archivio `adobe-lc-mobileworkspace-src-<version>.zip`. Questo archivio include il codice sorgente richiesto per creare un&#39;app AEM Forms  personalizzata. L&#39;archivio è incluso nel `adobe-aemfd-forms-app-src-pkg-<version>.zip`pacchetto disponibile sul Software Distribution.

Per scaricare il file `adobe-aemfd-forms-app-src-pkg-<version>.zip`, effettuate le seguenti operazioni:

1. Aprire [Distribuzione software](https://experience.adobe.com/downloads). È necessario un Adobe ID  per accedere a Distribuzione software.
1. Toccate **[!UICONTROL Adobe Experience Manager]** disponibile nel menu di intestazione.
1. Nella sezione **[!UICONTROL Filtri]**:
   1. Selezionare **[!UICONTROL Forms]** dall&#39;elenco a discesa **[!UICONTROL Soluzione]**.
   2. Selezionate la versione e digitate il tipo di pacchetto. Potete anche utilizzare l&#39;opzione **[!UICONTROL Download di ricerca]** per filtrare i risultati.
1. Toccate il nome del pacchetto applicabile al sistema operativo in uso, selezionate **[!UICONTROL Accetta termini EULA]**, quindi toccate **[!UICONTROL Scarica]**.
1. Aprite [Gestione pacchetti](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) e fate clic su **[!UICONTROL Carica pacchetto]** per caricare il pacchetto.
1. Selezionate il pacchetto e fate clic su **[!UICONTROL Installa]**.
1. Per scaricare l&#39;archivio del codice sorgente, aprite **https://&lt;server>:&lt;porta>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-&lt;versione>.zip** nel browser. Il file .zip dell&#39;app Android viene scaricato sul dispositivo.
1. Estrarre il contenuto del file .zip in una cartella del file system locale. Ad esempio, *C:\&lt;Struttura cartella>\adobe-lc-mobileworkspace-src-2.4.20*

Nell&#39;immagine seguente viene visualizzata la struttura della cartella `adobe-lc-mobileworkspace-src-<version>.zip\android`.

![zip_android_folder_structure](assets/zip_android_folder_structure.png)

## Impostare le variabili di ambiente {#set-environment-variable-android}

Impostate le seguenti variabili di ambiente prima di avviare il processo di creazione per l&#39;app AEM Forms :

* Impostare la variabile di ambiente JAVA_HOME sul percorso del software JDK nel file system locale. Ad esempio, C:\Program Files\Java\jdk1.8.0_181
* Impostate la variabile di ambiente di sistema `ANDROID_SDK_ROOT` sul percorso SDK per Android. Ad esempio, C:\Users\&amp;lt;nomeutente>\AppData\Local\Android\Sdk
* Impostate la variabile di ambiente di sistema `Path` in modo da includere le posizioni delle cartelle platform-tools e tools per Android. Ad esempio, C:\Users\&amp;lt;nomeutente>\AppData\Local\Android\Sdk\platform-tools and C:\Users\&amp;lt;nomeutente>\AppData\Local\Android\Sdk\tools.

## Creare app standard  AEM Forms {#set-up-the-xcode-project}

Dopo aver salvato il file adobe-lc-mobileworkspace-src-&lt;versione>.zip nel file system locale e aver impostato le variabili di ambiente, create l&#39;app standard  AEM Forms Android utilizzando una delle seguenti opzioni:

* [Creare  app AEM Forms con Android Studio](#using-android-studio)
* [Genera file .apk con Android Studio](#generate-apk-android-studio)

### Creare  app AEM Forms utilizzando Android Studio {#using-android-studio}

Per creare &#39;app AEM Forms utilizzando Android Studio, effettuate le seguenti operazioni:

1. Avviate l&#39;applicazione Android Studio sul computer.
1. Fare clic su **Apri un progetto Android Studio esistente**. Se la finestra di dialogo per l&#39;apertura di un progetto esistente non viene visualizzata automaticamente, selezionare **File** > **Apri**.
1. Accedete a *adobe-lc-mobileworkspace-src-&lt;versione>.zip/android* nel file system locale e fate clic su **OK**.

   L&#39;opzione **android** viene visualizzata nel riquadro a sinistra.

   ![android_folder_studio](assets/android_folder_studio.png)

1. Selezionare **android** dal riquadro a sinistra e fare clic su **Esegui** > **Esegui &#39;android&#39;**.
1. Selezionate il dispositivo Android dalla sezione Dispositivi collegati della finestra di dialogo Seleziona destinazione di distribuzione, quindi fate clic su OK.

   Dopo aver creato con successo l&#39;ambiente di sviluppo, ora puoi applicare le personalizzazioni sull&#39;app. Utilizzate i seguenti articoli per personalizzare l&#39;app:

   * [Personalizzazione branding](/help/forms/using/branding-customization.md)
   * [Personalizzazione tema](/help/forms/using/theme-customization.md)
   * [Personalizzazione Gesti](/help/forms/using/gesture-customization.md)

   Dopo aver applicato le personalizzazioni appropriate all&#39;app, potete generare il file .apk per la distribuzione.

### Genera file .apk con Android Studio {#generate-apk-android-studio}

Per generare il file .apk utilizzando Android Studio, eseguite i seguenti passaggi:

1. Avviate l&#39;applicazione Android Studio sul computer.
1. Selezionare **Apri un progetto Android Studio esistente**. Se la finestra di dialogo per l&#39;apertura di un progetto esistente non viene visualizzata automaticamente, selezionare **File** > **Apri**.
1. Accedete a *adobe-lc-mobileworkspace-src-&lt;versione>.zip/android* nel file system locale e fate clic su **OK**.

   L’opzione android viene visualizzata nel riquadro a sinistra.

1. Selezionare **Build** > **Genera APK** per generare il file .apk.

   Facoltativamente, selezionare **Build** > **Genera APK con firma** per generare una [versione firmata](https://developer.android.com/studio/publish/app-signing) del file .apk.

## Utilizzare Android Debug Bridge {#build-android-debug-bridge}

Una volta generato il file .apk, eseguite il comando seguente per installare l&#39;applicazione su un dispositivo Android utilizzando [Android Debug Bridge](https://developer.android.com/tools/help/adb.html).

**Utenti Windows:** `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`

**Utenti MAC:** `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`
