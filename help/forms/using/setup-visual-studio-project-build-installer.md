---
title: Configurare il progetto Visual Studio e creare l'app Windows
description: Informazioni su come configurare un progetto Visual Studio per creare l'app per dispositivi mobili AEM Forms Windows.
topic-tags: forms-app
docset: aem65
exl-id: ae7340c8-38cc-4b2b-ba17-22011471fd7d
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 2%

---

# Configurare il progetto Visual Studio e creare l&#39;app Windows{#set-up-the-visual-studio-project-and-build-the-windows-app}

AEM Forms fornisce il codice sorgente completo dell’app AEM Forms. L’origine contiene tutti i componenti per creare un’applicazione Workspace personalizzata. L&#39;archivio del codice sorgente `adobe-lc-mobileworkspace-src-<version>.zip` fa parte del pacchetto `adobe-aemfd-forms-app-src-pkg-<version>.zip` in Distribuzione software.

Per ottenere l’origine dell’app AEM Forms, effettua le seguenti operazioni:

1. Apri [Software Distribution](https://experience.adobe.com/downloads). Per accedere a Software Distribution è necessario disporre di un Adobe ID.
1. Seleziona **[!UICONTROL Adobe Experience Manager]** disponibile nel menu intestazione.
1. Nella sezione **[!UICONTROL Filtri]**:
   1. Selezionare **[!UICONTROL Forms]** dall&#39;elenco a discesa **[!UICONTROL Soluzione]**.
   2. Seleziona la versione e digita per il pacchetto. Puoi anche utilizzare l&#39;opzione **[!UICONTROL Cerca download]** per filtrare i risultati.
1. Selezionare il nome del pacchetto applicabile al sistema operativo in uso, selezionare **[!UICONTROL Accetta termini EULA]** e selezionare **[!UICONTROL Scarica]**.
1. Apri [Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=it) e fai clic su **[!UICONTROL Carica pacchetto]** per caricare il pacchetto.
1. Selezionare il pacchetto e fare clic su **[!UICONTROL Installa]**.

1. Per scaricare l&#39;archivio del codice sorgente, apri `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` nel browser.\
   Il pacchetto sorgente viene scaricato sul dispositivo.

Nell&#39;immagine seguente viene visualizzato il contenuto estratto di `adobe-lc-mobileworkspace-src-<version>.zip`.

![mws-content-1](assets/mws-content-1.png)

Nell&#39;immagine seguente viene visualizzata la struttura di directory della cartella `windows` nella cartella `src`.

![win-dir](assets/win-dir.png)

## Configurazione dell’ambiente {#setting-up-the-environment}

Per i dispositivi Windows, è necessario:

* Microsoft Windows 8.1 o Windows 10
* Microsoft Visual Studio 2015
* Strumenti Microsoft Visual Studio per Apache Cordova

## Configurazione del progetto Visual Studio per l&#39;app AEM Forms {#setting-up-visual-studio-project-for-aem-forms-app}

Per configurare il progetto di app AEM Forms in Visual Studio, eseguire la procedura seguente.

1. Copiare l&#39;archivio `adobe-lc-mobileworkspace-src-<version>.zip` nella cartella `%HOMEPATH%\Projects` nel dispositivo Windows 8.1 o Windows 10 con Visual Studio 2015 installato e configurato.
1. Estrarre l&#39;archivio nella directory `%HOMEPATH%\Projects\MobileWorkspace`.
1. Passare alla directory `%HOMEPATH%\Projects\MobileWorkspace\adobe-lc-mobileworkspace-src-[versionsrc]\windows`.
1. Aprire il file `CordovaApp.sln` con Visual Studio 2015 e procedere con la creazione dell&#39;app AEM Forms.

## Creare un’app AEM Forms {#build-aem-forms-app}

Per generare e distribuire l’app AEM Forms, effettua le seguenti operazioni.

>[!NOTE]
>
>I dati memorizzati nel file system di Windows per l’app AEM Forms non sono crittografati. È consigliabile utilizzare uno strumento di terze parti come Crittografia unità BitLocker di Windows per crittografare i dati del disco.

1. Nella barra degli strumenti di Visual Studio Standard, selezionare **Release** dal menu a discesa per la modalità di compilazione.

1. Seleziona Windows-AnyCPU, Windows-x64 o Windows-x86 in base alla tua piattaforma. Si consiglia Windows-AnyCPU.
1. In Esplora soluzioni di Visual Studio, fare clic con il pulsante destro del mouse sul progetto **CordovaApp.Windows** e selezionare **Store > Crea pacchetti app**.

   ![createapppackages](assets/createapppackages.png)

   Viene visualizzata la procedura guidata Crea pacchetti app.

   Il file di installazione di CordovaApp.Windows_3.0.2.0_anycpu.appx viene creato nella directory platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test.

   Se si verifica l&#39;errore `Retarget to windows 8.1 required`, fare clic con il pulsante destro del mouse sull&#39;errore e nel menu di scelta rapida selezionare **Ridestinare a Windows 8.1**.

   ![soluzione di retargeting](assets/retarget-solution.png)

1. Nella procedura guidata Crea pacchetti app, seleziona il meteo o non vuoi caricare l&#39;app in Windows Store, quindi fai clic su **Avanti**.

   ![createapppackageswizard1](assets/createapppackageswizard1.png)

1. Apporta le modifiche necessarie nei parametri, ad esempio la versione e il percorso di output della build dell’app.

   ![createapppackageswizard2](assets/createapppackageswizard2.png)

1. Dopo aver generato il progetto, puoi installare l’app utilizzando:

   * Windows PowerShell
   * Visual Studio

   Il pacchetto `.appx` richiede i seguenti elementi per essere installato correttamente:

   1. Libreria WinJS
   1. Verificare che il pacchetto sia dotato di un certificato autofirmato o di un certificato pubblico firmato da un&#39;autorità attendibile, ad esempio VeriSign.
   1. Licenza sviluppatore

   La directory Platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test contiene i quattro componenti principali:

   1. `.appx` file
   1. Certificato (attualmente è un certificato autofirmato da Apache Cordova)
   1. Cartella dipendenze
   1. File di PowerShell (estensione ps1)

## Distribuzione di un&#39;app tramite Windows PowerShell {#deploying-an-app-using-windows-powershell}

Esistono due modi per installare l&#39;applicazione su un dispositivo Windows.

### Acquisendo la licenza per sviluppatori {#by-acquiring-the-developer-license}

1. Fare clic con il pulsante destro del mouse sul file di PowerShell ( `Add-AppDevPackage.ps1)` e scegliere **Esegui con PowerShell**.

1. Viene richiesto di ottenere una licenza per sviluppatori. Utilizza le credenziali dell’account Microsoft per acquisire la licenza di sviluppatore.\
   Questa licenza è valida per 30 giorni ed è possibile rinnovarla gratuitamente.
1. Quando si acquisisce la licenza per sviluppatori, il certificato autofirmato viene installato nel sistema e l&#39;applicazione viene installata correttamente.

### Utilizzando dispositivi di proprietà dell&#39;azienda {#by-using-enterprise-owned-devices}

Per i dispositivi di proprietà dell’azienda che fanno parte del dominio dell’azienda, l’acquisizione di una licenza per sviluppatori non è richiesta.

I dispositivi di proprietà aziendale utilizzano le edizioni Professional ed Enterprise di Windows.

Microsoft consiglia di installare un certificato pubblico emesso da un’autorità attendibile, ad esempio VeriSign.

Per distribuire l’app:

* Verificare che il dispositivo sia aggiunto al dominio dell&#39;organizzazione.
* Abilitare l&#39;impostazione di Criteri di gruppo.

**Per abilitare l&#39;impostazione dei criteri di gruppo:**

1. Nel dispositivo, eseguire `gpedit.msc`.
1. Passa a **Configurazione computer > Modelli amministrativi > Componente Windows > Distribuzione pacchetto app**.
1. Fare clic con il pulsante destro del mouse su **Consenti l&#39;installazione di tutte le app attendibili**.
1. Fai clic su **Modifica** e seleziona **Abilitato**.

1. Fai clic su **OK**.

Modificare lo script di PowerShell generato da Visual Studio per impedirgli di acquisire la licenza per sviluppatori.

Nello script di PowerShell impostare la variabile: `$NeedDeveloperLicense = $false`.

Per i dispositivi che non fanno parte di un dominio, è necessario il codice di attivazione del prodotto con caricamento laterale. Puoi acquistarlo da un rivenditore Windows.

Per Windows 8.1 Home Edition non esistono criteri di gruppo, il caricamento laterale dell&#39;organizzazione non è consentito e non è possibile aggiungerlo al dominio enterprise. Distribuisci l’app su un dispositivo Windows 8.1 Home Edition con una licenza per sviluppatori.

Per ulteriori informazioni, fare clic [qui](https://blogs.msdn.com/b/mvpawardprogram/archive/2014/03/24/side-loading-deployment-of-windows-store-apps-in-enterprises-step-by-step.aspx).

## Distribuzione di un&#39;app tramite Visual Studio {#deploying-an-app-using-visual-studio}

Per installare l&#39;app in Windows utilizzando Visual Studio:

1. Connetti il dispositivo utilizzando il debugger remoto.\
   Per ulteriori informazioni, vedere [Eseguire applicazioni Windows Store in un computer remoto](https://docs.microsoft.com/en-us/visualstudio/debugger/run-windows-store-apps-on-a-remote-machine).

1. Con l&#39;app aperta in Visual Studio, scegliere Windows-x64, Windows-x86 o Windows-AnyCPU dall&#39;elenco Piattaforme soluzione e selezionare **Computer remoto**.
1. L&#39;app viene distribuita nel computer remoto.
