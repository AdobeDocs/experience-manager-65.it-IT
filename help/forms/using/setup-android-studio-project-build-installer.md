---
title: Configurare il progetto Android Studio e creare l'app Android
seo-title: Set up the Android studio project and build the Android app
description: Passaggi per configurare il progetto Android Studio e creare il programma di installazione per l’app AEM Forms
seo-description: Steps to set up the Android Studio project and build the installer for the AEM Forms app
uuid: 4c966cdc-d0f5-4b5b-b21f-f11e8a35ec8a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: forms-app
discoiquuid: fabc981e-0c9e-4157-b0a1-0c13717fb6cd
exl-id: 47d6af00-34d8-4e5d-8117-86fc1b6f58cb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 7%

---

# Configurare il progetto Android Studio e creare l&#39;app Android {#set-up-the-android-studio-project-and-build-the-android-app}

Questo articolo è per la creazione di AEM Forms App 6.3.1.1 e versioni successive. Per la creazione di un&#39;app dal codice sorgente del codice sorgente dell&#39;app AEM Forms 6.3, vedi [Configurare il progetto Eclipse e creare l&#39;app Android™](/help/forms/using/setup-eclipse-project-build-installer.md).

AEM Forms fornisce il codice sorgente completo dell’app AEM Forms. La sorgente contiene tutti i componenti per creare un’app AEM Forms personalizzata. archivio del codice sorgente, `adobe-lc-mobileworkspace-src-<version>.zip` fa parte del `adobe-aemfd-forms-app-src-pkg-<version>.zip` pacchetto sulla distribuzione software.

Per ottenere la sorgente dell’app AEM Forms, esegui i seguenti passaggi:

1. Apri [Software Distribution](https://experience.adobe.com/downloads). Per accedere a Software Distribution è necessario disporre di un Adobe ID.
1. Tocca **[!UICONTROL Adobe Experience Manager]** che si trova nel menu di intestazione.
1. In **[!UICONTROL Filtri]** sezione:
   1. Seleziona **[!UICONTROL Forms]** dal **[!UICONTROL Soluzione]** elenco a discesa.
   2. Seleziona la versione e digita il pacchetto. È inoltre possibile utilizzare **[!UICONTROL Download di ricerca]** per filtrare i risultati.
1. Toccare il nome del pacchetto applicabile al sistema operativo in uso, selezionare **[!UICONTROL Accettare i termini dell&#39;EULA]**, e tocca **[!UICONTROL Scarica]**.
1. Apri [Gestione pacchetti](https://docs.adobe.com/content/help/it/experience-manager-65/administering/contentmanagement/package-manager.html) e fai clic su **[!UICONTROL Carica pacchetto]** per caricarlo.
1. Seleziona il pacchetto e fai clic su **[!UICONTROL Installa]**.

L’immagine seguente visualizza il contenuto estratto del `adobe-lc-mobileworkspace-src-<version>.zip`.

![Contenuto estratto della sorgente Android™ zippata](assets/mws-content-1.png)

Nell&#39;immagine seguente viene visualizzata la struttura di directory del `android`nella cartella `src`cartella.

![Struttura della directory della cartella android in src](assets/android-folder.png)

## Creare un’app AEM Forms standard {#set-up-the-xcode-project}

1. Esegui i seguenti passaggi per configurare un progetto in Android™ Studio e fornire un’identità di firma:

   Accedi a un computer con Android™ Studio installato e configurato.

1. Copia il download `adobe-lc-mobileworkspace-src-<version>.zip` archiviare in:

   **Per gli utenti MAC**: `[User_Home]/Projects`

   **Per utenti Windows®**: `%HOMEPATH%\Projects`

   >[!NOTE]
   >
   >Per Windows®, si consiglia di mantenere il progetto android nell&#39;unità di sistema.

1. Estrai l’archivio nella seguente directory:

   **Per gli utenti MAC**: `[User_Home]/Projects/[your-project]`

   **Per utenti Windows®**: `%HOMEPATH%\Projects\[your-project]`

   >[!NOTE]
   >
   >Si consiglia di mantenere il progetto android estratto nell’unità di sistema prima di importare il progetto in Android Studio.

1. Avvia Android™ Studio.

   **Per gli utenti MAC**: Aggiorna `local.properties` file presente nel `[User_Home]/Projects/[your-project]/android` la cartella e il punto `sdk.dir` variabile a `SDK` sul desktop.

   **Per utenti Windows®**: Aggiorna `local.properties` file presente nel `%HOMEPATH%\Projects\[your-project]\android` la cartella e il punto `sdk.dir` variabile a `SDK` sul desktop.

1. Fai clic su **[!UICONTROL Fine]** per creare il progetto.

   Il progetto è disponibile in ADT Project Explorer.

   ![progetto eclipse dopo la creazione dell&#39;app](assets/eclipsebuildmws.png)

1. In Android™ Studio, seleziona **[!UICONTROL Progetto Di Importazione (Eclipse ADT, Gradle, Ecc.)]**.
1. Nell’explorer del progetto, seleziona la directory principale del progetto che desideri creare nel **Directory principale** casella di testo:

   **Per gli utenti Mac:** [Utente_Home]/Projects/MobileWorkspace/src/android

   **Per gli utenti Windows®:** %HOMEPATH%\Projects\MobileWorkspace\src\android

1. Dopo l&#39;importazione del progetto, viene visualizzato un pop-up con l&#39;opzione per aggiornare il livello del plug-in Android™. Fai clic sul pulsante appropriato a seconda delle tue esigenze.

   ![dontremindmeagainotisproject](assets/dontremindmeagainforthisproject.png)

1. Dopo la generazione gradle corretta, viene visualizzata la seguente schermata. Collegare il dispositivo o l&#39;emulatore appropriato al sistema e fare clic su **[!UICONTROL Esegui Android™]**.

   ![gradleconsole](assets/gradleconsole.png)

1. Android™ Studio visualizza i dispositivi collegati e gli emulatori disponibili. Selezionare il dispositivo sul quale si desidera eseguire l&#39;applicazione, quindi fare clic su **OK**.

   ![connecteddevice](assets/connecteddevice.png)

Dopo aver creato il progetto, puoi scegliere di installare l’app utilizzando Android™ Debug Bridge o Android™ Studio.

### Utilizzo di Android™ Debug Bridge {#andriod-debug-bridge}

È possibile installare l&#39;applicazione su un dispositivo Android™ tramite [Bridge di debug Android™](https://developer.android.com/tools/help/adb.html) con il comando seguente:

**Per gli utenti MAC**: `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`

**Per utenti Windows®**: `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`
