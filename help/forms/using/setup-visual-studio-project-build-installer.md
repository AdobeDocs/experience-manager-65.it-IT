---
title: Configurare il progetto Visual Studio e creare l'app Windows
seo-title: Configurare il progetto Visual Studio e creare l'app Windows
description: Scoprite come impostare un progetto di Visual Studio per creare l'app dispositivo mobile AEM Forms Windows.
seo-description: Scoprite come impostare un progetto di Visual Studio per creare l'app dispositivo mobile AEM Forms Windows.
uuid: 9559e584-2a40-4740-a29a-d7ad66220224
topic-tags: forms-app
discoiquuid: c71c2a17-54f9-4c95-a90a-3c89d6d45721
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Configurare il progetto Visual Studio e creare l&#39;app Windows{#set-up-the-visual-studio-project-and-build-the-windows-app}

AEM Forms fornisce il codice sorgente completo dell&#39;app AEM Forms. L&#39;origine contiene tutti i componenti per creare un&#39;applicazione area di lavoro personalizzata. L&#39;archivio del codice sorgente `adobe-lc-mobileworkspace-src-<version>.zip`fa parte del `adobe-aemfd-forms-app-src-pkg-<version>.zip` pacchetto sulla condivisione del pacchetto.

Per ottenere l&#39;origine dell&#39;app AEM Forms, effettua i seguenti passaggi:

1. Passa alla condivisione del pacchetto\
   URL: `https://<server>:<port>/crx/packageshare`.

1. Scaricate il pacchetto sorgente. Quando scaricate il pacchetto, questo viene aggiunto nel gestore pacchetti di AEM Forms.
1. Dopo il download, passa a: `https://<server>:<port>/crx/packmgr/index.jsp`e installare `adobe-aemfd-forms-app-src-pkg-<version>.zip`.

1. Per scaricare l&#39;archivio del codice sorgente, aprite `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` nel browser.\
   Il pacchetto di origine viene scaricato sul dispositivo.

Nell’immagine seguente sono visualizzati i contenuti estratti dell’ `adobe-lc-mobileworkspace-src-<version>.zip`.

![mws-content-1](assets/mws-content-1.png)

L’immagine seguente mostra la struttura di directory della `windows` cartella nella `src` cartella.

![win-dir](assets/win-dir.png)

## Impostazione dell&#39;ambiente {#setting-up-the-environment}

Per i dispositivi Windows, è necessario:

* Microsoft Windows 8.1 o Windows 10
* Microsoft Visual Studio 2015
* Microsoft Visual Studio Tools per Apache Cordova

## Impostazione dell&#39;app Visual Studio Project per AEM Forms {#setting-up-visual-studio-project-for-aem-forms-app}

Per impostare il progetto dell&#39;app AEM Forms in Visual Studio, effettua i seguenti passaggi.

1. Copiare l&#39; `adobe-lc-mobileworkspace-src-<version>.zip` archivio nella `%HOMEPATH%\Projects` cartella del dispositivo Windows 8.1 o Windows 10 con Visual Studio 2015 installato e configurato.
1. Estrarre l&#39;archivio nella `%HOMEPATH%\Projects\MobileWorkspace` directory.
1. Andate alla `%HOMEPATH%\Projects\MobileWorkspace\adobe-lc-mobileworkspace-src-[versionsrc]\windows` directory.
1. Aprite il `CordovaApp.sln` file utilizzando Visual Studio 2015 e procedete alla creazione dell&#39;app AEM Forms.

## Creare app AEM Forms {#build-aem-forms-app}

Per creare e distribuire l&#39;app AEM Forms, effettuate i seguenti passaggi.

>[!NOTE]
>
>I dati memorizzati nel file system Windows per l&#39;app AEM Forms non sono crittografati. È consigliabile utilizzare uno strumento di terze parti come Crittografia unità BitLocker di Windows per crittografare i dati del disco.

1. Nella barra degli strumenti di Visual Studio Standard, selezionare **Rilascia** dall&#39;elenco a discesa per la modalità di creazione.

1. Seleziona Windows-AnyCPU, Windows-x64 o Windows-x86 in base alla piattaforma in uso. Si consiglia Windows-AnyCPU.
1. In Esplora soluzioni di Visual Studio fare clic con il pulsante destro del mouse sul progetto **CordovaApp.Windows** e selezionare **Store > Crea pacchetti** app.

   ![create_apppackages](assets/createapppackages.png)

   Viene visualizzata la procedura guidata Crea pacchetti app.

   Il file del programma di installazione CordovaApp.Windows_3.0.2.0_anycpu.appx viene creato nella directory platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test.

   Se si verifica l&#39;errore `Retarget to windows 8.1 required`fare clic con il pulsante destro del mouse sull&#39;errore e scegliere **Riporta a Windows 8.1** dal menu a comparsa.

   ![retarget-solution](assets/retarget-solution.png)

1. Nella procedura guidata Crea pacchetti app, seleziona il tempo meteorologico o non vuoi caricare l&#39;app nello store Windows, quindi fai clic su **Avanti**.

   ![createapppackageswizard1](assets/createapppackageswizard1.png)

1. Apportate le modifiche necessarie ai parametri, ad esempio la versione e il percorso di output della build dell&#39;app.

   ![createapppackageswizard2](assets/createapppackageswizard2.png)

1. Dopo aver creato il progetto, potete installare l&#39;app utilizzando:

   * Windows PowerShell
   * Visual Studio
   Il `.appx` pacchetto richiede la corretta installazione dei seguenti elementi:

   1. Libreria WinJS
   1. Verificate che il pacchetto sia dotato di un certificato autofirmato o di un&#39;autorità affidabile firmata come VeriSign.
   1. Licenza sviluppatore
   La directory Platforms\windows\AppPackages\CordovaApp.Windows_3.0.2.0_anycpu_Test contiene i quattro componenti principali:

   1. `.appx` file
   1. Certificato (attualmente è un certificato autofirmato di Apache Cordova)
   1. Cartella dipendenze
   1. File PowerShell (.ps1 extension)



## Distribuzione di un&#39;app tramite Windows PowerShell {#deploying-an-app-using-windows-powershell}

Esistono due modi per installare l&#39;applicazione su un dispositivo Windows.

### Acquisendo la licenza sviluppatore {#by-acquiring-the-developer-license}

1. Fare clic con il pulsante destro del mouse sul file PowerShell ( `Add-AppDevPackage.ps1)`e scegliere **Esegui con PowerShell**.

1. La configurazione richiede di ottenere una licenza sviluppatore. Utilizzate le credenziali dell&#39;account Microsoft per ottenere la licenza per lo sviluppatore.\
   Questa licenza è valida per 30 giorni e può essere rinnovata gratuitamente.
1. Quando acquistate la licenza di sviluppatore, la configurazione installa il certificato autofirmato sul sistema e l&#39;applicazione viene installata correttamente.

### Utilizzando dispositivi di proprietà aziendale {#by-using-enterprise-owned-devices}

Per i dispositivi di proprietà dell&#39;azienda che fanno parte del dominio dell&#39;azienda, non è necessario acquisire una licenza sviluppatore.

I dispositivi di proprietà Enterprise utilizzano le edizioni Professional ed Enterprise di Windows.

Microsoft consiglia di installare un certificato pubblico emesso da un&#39;autorità affidabile, ad esempio VeriSign.

Per distribuire l&#39;app:

* Assicurarsi che il dispositivo sia unito al dominio dell&#39;organizzazione.
* Abilitare l&#39;impostazione dei criteri di gruppo.

**Per abilitare l&#39;impostazione dei criteri di gruppo:**

1. Nel dispositivo, eseguire `gpedit.msc`.
1. Andate a Configurazione **computer > Modelli amministrativi > Componente Windows > Distribuzione** pacchetto app.
1. Fate clic con il pulsante destro del mouse su **Consenti l&#39;installazione** di tutte le app attendibili.
1. Fate clic su **Modifica** e selezionate **Abilitato**.

1. Fai clic su **OK**. 

Modificare lo script PowerShell generato da Visual Studio per impedirne l&#39;acquisizione da parte dello sviluppatore.

Nello script PowerShell, impostare la variabile: `$NeedDeveloperLicense = $false`.

Per i dispositivi che non fanno parte del dominio, è necessario caricare il codice di attivazione del prodotto. È possibile acquistarlo da un rivenditore Windows.

Per Windows 8.1 Home Edition non è disponibile alcun criterio di gruppo, il caricamento laterale dell&#39;organizzazione non è consentito e non è possibile unirsi a esso con il dominio Enterprise. Distribuite l&#39;app su un dispositivo Windows 8.1 Home Edition utilizzando la licenza per sviluppatori.

Per ulteriori informazioni, fai clic [qui](https://blogs.msdn.com/b/mvpawardprogram/archive/2014/03/24/side-loading-deployment-of-windows-store-apps-in-enterprises-step-by-step.aspx).

## Distribuzione di un&#39;app tramite Visual Studio {#deploying-an-app-using-visual-studio}

Per installare l&#39;app in Windows utilizzando Visual Studio:

1. Collegare il dispositivo mediante il debugger remoto.\
   Per ulteriori informazioni, consultate [Eseguire app Windows Store su un computer](https://docs.microsoft.com/en-us/visualstudio/debugger/run-windows-store-apps-on-a-remote-machine)remoto.

1. Con l&#39;app aperta in Visual Studio, scegliere Windows-x64, Windows-x86 o Windows-AnyCPU dall&#39;elenco Piattaforme soluzione, quindi selezionare **Computer** remoto.
1. L&#39;app è distribuita sul computer remoto.

