---
title: Configurare il progetto Android Studio e creare l'app Android
seo-title: Configurare il progetto Android Studio e creare l'app Android
description: 'Passaggi per configurare il progetto Android Studio e creare il programma di installazione per l''app AEM Forms '
seo-description: 'Passaggi per configurare il progetto Android Studio e creare il programma di installazione per l''app AEM Forms '
uuid: 4c966cdc-d0f5-4b5b-b21f-f11e8a35ec8a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: forms-app
discoiquuid: fabc981e-0c9e-4157-b0a1-0c13717fb6cd
translation-type: tm+mt
source-git-commit: 1dfc8fa91d3e5ae8ca49cf1f3cb739b59feb18cf
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---


# Configurare il progetto Android Studio e creare l&#39;app Android {#set-up-the-android-studio-project-and-build-the-android-app}

Questo articolo è destinato alla creazione di  AEM Forms App 6.3.1.1 e versioni successive. Per creare un&#39;app dal codice sorgente del codice sorgente dell&#39; AEM Forms App 6.3, vedete [Configurare il progetto Eclipse e creare l&#39;app Android™](/help/forms/using/setup-eclipse-project-build-installer.md).

 AEM Forms fornisce il codice sorgente completo dell&#39;app AEM Forms . L&#39;origine contiene tutti i componenti per creare un&#39;app AEM Forms  personalizzata. L&#39;archivio del codice sorgente, `adobe-lc-mobileworkspace-src-<version>.zip` è una parte del pacchetto `adobe-aemfd-forms-app-src-pkg-<version>.zip` sulla distribuzione del software.

Per ottenere l&#39;origine dell&#39;app AEM Forms , effettuate le seguenti operazioni:

1. Aprire [Distribuzione software](https://experience.adobe.com/downloads). È necessario un Adobe ID  per accedere a Distribuzione software.
1. Toccate **[!UICONTROL Adobe Experience Manager]** disponibile nel menu di intestazione.
1. Nella sezione **[!UICONTROL Filtri]**:
   1. Selezionare **[!UICONTROL Forms]** dall&#39;elenco a discesa **[!UICONTROL Soluzione]**.
   2. Selezionate la versione e digitate il tipo di pacchetto. Potete anche utilizzare l&#39;opzione **[!UICONTROL Download di ricerca]** per filtrare i risultati.
1. Toccate il nome del pacchetto applicabile al sistema operativo in uso, selezionate **[!UICONTROL Accetta termini EULA]**, quindi toccate **[!UICONTROL Scarica]**.
1. Aprite [Gestione pacchetti](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) e fate clic su **[!UICONTROL Carica pacchetto]** per caricare il pacchetto.
1. Selezionate il pacchetto e fate clic su **[!UICONTROL Installa]**.

Nell&#39;immagine seguente sono visualizzati i contenuti estratti della `adobe-lc-mobileworkspace-src-<version>.zip`.

![Contenuto estratto della sorgente Android™ compresso](assets/mws-content-1.png)

Nell&#39;immagine seguente viene visualizzata la struttura di directory della cartella `android`nella cartella `src`.

![Struttura delle directory della cartella android in src](assets/android-folder.png)

## Creare app standard  AEM Forms {#set-up-the-xcode-project}

1. Per configurare un progetto in Android™ Studio e fornire un&#39;identità di firma, effettuate le seguenti operazioni:

   Accedete a un computer in cui sia installato e configurato Android™ Studio.

1. Copiate l&#39;archivio `adobe-lc-mobileworkspace-src-<version>.zip` scaricato in:

   **Per gli utenti** MAC:  `[User_Home]/Projects`

   **Per gli utenti** di Windows®:  `%HOMEPATH%\Projects`

   >[!NOTE]
   >
   >Per Windows®, si consiglia di mantenere il progetto android nell&#39;unità di sistema.

1. Estrarre l&#39;archivio nella seguente directory:

   **Per gli utenti** MAC:  `[User_Home]/Projects/[your-project]`

   **Per gli utenti** di Windows®:  `%HOMEPATH%\Projects\[your-project]`

   >[!NOTE]
   >
   >Si consiglia di mantenere il progetto android estratto nell&#39;unità di sistema prima di importare il progetto in Android Studio.

1. Avviate Android™ Studio.

   **Per gli utenti** MAC: Aggiornate il  `local.properties` file presente nella  `[User_Home]/Projects/[your-project]/android` cartella e puntate la  `sdk.dir` variabile in  `SDK` posizione sul desktop.

   **Per gli utenti** di Windows®: Aggiornate il  `local.properties` file presente nella  `%HOMEPATH%\Projects\[your-project]\android` cartella e puntate la  `sdk.dir` variabile in  `SDK` posizione sul desktop.

1. Fare clic su **[!UICONTROL Fine]** per creare il progetto.

   Il progetto è disponibile in ADT Project Explorer.

   ![progetto eclipse dopo la creazione dell&#39;app](assets/eclipsebuildmws.png)

1. In Android™ Studio, selezionare **[!UICONTROL Importa progetto (Eclipse ADT, Gradle, ecc.)]**.
1. In Project Explorer, selezionate la directory principale del progetto da creare nella casella di testo **Directory principale**:

   **Per utenti Mac:** [User_Home]/Projects/MobileWorkspace/src/android

   **Per gli utenti di Windows®:** %HOMEPATH%\Projects\MobileWorkspace\src\android

1. Dopo l&#39;importazione del progetto, viene visualizzato un pop-up con l&#39;opzione per aggiornare il plug-in Gradle per Android™. Fate clic sul pulsante appropriato in base alle vostre esigenze.

   ![dontremindmeagainputisproject](assets/dontremindmeagainforthisproject.png)

1. Dopo la generazione gradle completata, viene visualizzata la schermata seguente. Collegare il dispositivo o l&#39;emulatore appropriato al sistema e fare clic su **[!UICONTROL Esegui Android™]**.

   ![gradleconsole](assets/gradleconsole.png)

1. Android™ Studio visualizza i dispositivi connessi e gli emulatori disponibili. Selezionare il dispositivo su cui si desidera eseguire l&#39;applicazione, quindi fare clic su **OK**.

   ![connecteddevice](assets/connecteddevice.png)

Dopo aver creato il progetto, potete scegliere di installare l&#39;app utilizzando Android™ Debug Bridge o Android™ Studio.

### Utilizzo di Android™ Debug Bridge {#andriod-debug-bridge}

Potete installare l&#39;applicazione su un dispositivo Android™ tramite il [Android™ Debug Bridge](https://developer.android.com/tools/help/adb.html) con il seguente comando:

**Per gli utenti** MAC:  `adb install [User_Home]/Projects/[your-project]/adobe-lc-mobileworkspace-src-[version]/android/build/outputs/apk/android-debug.apk`

**Per gli utenti** di Windows®:  `adb install %HOMEPATH%\Projects\[your-project]\adobe-lc-mobileworkspace-src-[version]\android\build\outputs\apk\android-debug.apk`
