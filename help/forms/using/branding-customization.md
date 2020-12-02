---
title: Personalizzazione branding
seo-title: Personalizzazione branding
description: Personalizzate l'icona dell'applicazione, il nome dell'applicazione, le immagini di avvio e la pagina di login per fornire un aspetto e un aspetto distinti dell'organizzazione 'app AEM Forms.
seo-description: Personalizzate l'icona dell'applicazione, il nome dell'applicazione, le immagini di avvio e la pagina di login per fornire un aspetto e un aspetto distinti dell'organizzazione 'app AEM Forms.
uuid: fece0fa8-c417-45eb-93f1-a91b49835fa0
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: f6440a36-719a-4f89-b7db-1af918a3469a
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 2%

---


# Personalizzazione branding {#branding-customization}

Potete personalizzare l&#39;icona dell&#39;applicazione, il nome dell&#39;applicazione, le immagini di avvio e la pagina di login per fornire un aspetto specifico dell&#39;organizzazione a &#39;app AEM Forms. Ad esempio, potete modificare le immagini per utilizzare i logo aziendali. L&#39;app AEM Forms  supporta le seguenti personalizzazioni:

* Personalizzazione delle immagini dell’icona e dell’avvio dell’applicazione
* Personalizzazione del nome dell&#39;app
* Personalizzazione delle immagini nella pagina di login
* Personalizzazione del logo nel menu dell&#39;app

## Personalizzazione delle immagini di icona e lancio {#customizing-icon-and-launch-images}

Per personalizzare l&#39;icona dell&#39;app predefinita e l&#39;immagine di avvio dell&#39;app  AEM Forms, effettuate le seguenti operazioni:

>[!NOTE]
>
>Per tutte le icone e immagini, usate il formato PNG non interlacciato.

### Personalizzazione delle immagini di icona e lancio {#to-customize-icon-and-launch-images}

#### Per iOS {#for-ios}

1. Apri il progetto `Capture.xcodeproj` in Xcode.
1. (***Per personalizzare l&#39;icona***) Nella visualizzazione del Navigator di Capture, passare a **[!UICONTROL Capture > Capture > Supporting Files > Capture-info.plist]**. Fare clic sul menu a discesa accanto ai file Icona. Specificate il nome del file di icona (.png) e caricate il file in **[!UICONTROL Capture > Capture > Resources > icons]**. Le dimensioni attualmente supportate sono: 29x29, 50x50, 58x58, 72x72, 100x100 e 144x144.
1. (***Per personalizzare le immagini del lancio***) Accertatevi che i nomi file delle immagini siano:

   * Per verticale: `Default-Portrait~ipad.png` e `Default-Portrait@2x~ipad.png`
   * Per orizzontale: `Default-Landscape~ipad.png` e `Default-Landscape@2x~ipad.png`

   Caricateli nel progetto Capture per sostituire i file esistenti nel progetto.

   >[!NOTE]
   >
   >Accertatevi che il nome e la risoluzione dell’immagine corrispondano all’immagine sostituita nel progetto.

1. Create ed eseguite &#39;app AEM Forms sul dispositivo iOS o sul simulatore iOS.

#### Per Android {#for-android}

1. Denominate i file di icona dell’applicazione come:

   `ic_launcher.png`

1. Inserite i file di icona corrispondenti nelle seguenti directory:

   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-hdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-mdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxxhdpi`

   >[!NOTE]
   >
   >Accertatevi che il nome e la risoluzione dell’immagine corrispondano all’immagine sostituita nel progetto.

1. Rigenerate l&#39;app  AEM Forms.

### Per Windows {#for-windows}

1. Sostituisce le icone nel percorso:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\icons\windows`

1. Sostituisce l’immagine di avvio nel percorso:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\screens\windows`

   >[!NOTE]
   >
   >Accertatevi che il nome e la risoluzione dell’immagine corrispondano all’immagine sostituita nel progetto.

1. Rigenerate l&#39;app  AEM Forms.

## Personalizzare il nome dell&#39;app {#customize-the-app-name}

### Per iOS {#for-ios-1}

1. Apri il progetto `Capture.xcodeproj` in Xcode.
1. Nella visualizzazione del Navigator di Capture, passare a **[!UICONTROL Capture > Capture > Supporting Files > InfoPlist.strings]**.

   Aggiornate il valore dell&#39;attributo `CFBundleDisplayName` in un nome che desiderate visualizzare per l&#39;app.

1. Create ed eseguite &#39;app AEM Forms sul dispositivo iOS o sul simulatore iOS.

   Per informazioni dettagliate sulla creazione dell&#39;app per iOS, consultate [Configurare il progetto Xcode e creare l&#39;app iOS](/help/forms/using/setup-xcode-project-build-installer.md).

### Per Android {#for-android-1}

1. Aprite il seguente file XML in qualsiasi editor di testo o XML:

   `[User_Home]/Projects/[your-project]/src/android/res/values/strings.xml and android/res/values-en/strings.xml`

1. Aggiornare il valore della chiave `app_name`.
1. Rigenerate l&#39;app  AEM Forms.

   Per informazioni dettagliate sulla creazione dell&#39;app per Android, consultate [Configurare il progetto Eclipse e creare l&#39;app Android](/help/forms/using/setup-eclipse-project-build-installer.md).

### Per Windows {#for-windows-1}

1. Aprite il seguente file XML in qualsiasi editor di testo:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\config.xml`

1. Aggiornate il valore nel tag `<name>...</name>`.
1. Rigenerate l&#39;app  AEM Forms.

   Per informazioni dettagliate sulla creazione dell&#39;app per Windows, consultate [Configurare il progetto di Visual Studio e creare l&#39;app per Windows](/help/forms/using/setup-visual-studio-project-build-installer.md).

## Personalizzazione delle immagini nella pagina di login {#customizing-images-on-the-login-page}

La pagina di accesso dell&#39;app AEM Forms  ha logo e immagini di sfondo. Il logo si trova sopra la finestra di dialogo di login e l’immagine di sfondo si trova sotto la finestra di dialogo di login. Per personalizzare l’immagine predefinita nella pagina di login, effettuate le seguenti operazioni:

**Prima di iniziare**

Assicuratevi di disporre delle immagini seguenti:

<table>
 <tbody>
  <tr>
   <th><p>Descrizione</p> </th>
   <th><p>Dimensione</p> </th>
   <th><p>Nome file</p> </th>
  </tr>
  <tr>
   <td><p>Logo</p> </td>
   <td><p>72 x 72 pixel</p> </td>
   <td><p>LC-logo.png</p> </td>
  </tr>
  <tr>
   <td><p>Immagine di sfondo (verticale)</p> </td>
   <td><p>1280 x 989 pixel</p> </td>
   <td><p>Landing_bg.jpeg</p> </td>
  </tr>
 </tbody>
</table>

**Per personalizzare le immagini nella pagina di login utilizzando Xcode**

1. Apri il progetto `Capture.xcodeproj` in Xcode.

1. Individuate la cartella `www/wsmobile/images`.
1. Per modificare il logo, sostituire il file `LC-logo.png` predefinito con il file `LC-logo.png` personalizzato.
1. Per modificare lo sfondo, sostituire il file `Landing_bg.jpeg` predefinito con il file `Landing_bg.jpeg`personalizzato.
1. Create ed eseguite &#39;app AEM Forms sul dispositivo iOS o sul simulatore iOS.

### Per personalizzare le immagini nelle pagine di login utilizzando Eclipse {#to-customize-images-on-the-login-pages-using-eclipse}

1. Apri il progetto Android in Eclipse.

1. Individuate la cartella `assets/www/wsmobile/images`.
1. Per modificare il logo, sostituire il file `LC-logo.png` predefinito con il file `LC-logo.png` personalizzato.
1. Per modificare lo sfondo, sostituire il file `Landing_bg.jpeg` predefinito con il file `Landing_bg.jpeg`personalizzato.
1. Creare ed eseguire &#39;app AEM Forms sul dispositivo Android.

### Per personalizzare le immagini nelle pagine di login utilizzando Visual Studio {#to-customize-images-on-the-login-pages-using-visual-studio}

1. Aprire il progetto `MWSWindows.sln` in Visual Studio.

1. Individuate la cartella `MWSWindows\www\wsmobile\images`.
1. Per modificare il logo, sostituire il file `LC-logo.png` predefinito con il file `LC-logo.png` personalizzato.
1. Per modificare lo sfondo, sostituire il file `Landing_bg.jpeg` predefinito con il file `Landing_bg.jpeg`personalizzato.
1. Creare ed eseguire  app AEM Forms sul dispositivo Windows.

## Personalizzazione del logo nel menu dell&#39;app {#customizing_images_on_the_login_page-1}

Dopo aver effettuato l&#39;accesso all&#39;app AEM Forms  e aver toccato il pulsante del menu, il logo è visibile sopra il menu. Per personalizzare il logo predefinito, effettuate le seguenti operazioni:

**Prima di iniziare**

Accertatevi di disporre della seguente immagine:

<table>
 <tbody>
  <tr>
   <th><p>Descrizione</p> </th>
   <th><p>Dimensione</p> </th>
   <th><p>Nome file</p> </th>
  </tr>
  <tr>
   <td><p>Logo</p> </td>
   <td><p>72 x 72 pixel</p> </td>
   <td><p>aem_icon.png</p> </td>
  </tr>
 </tbody>
</table>

**Per personalizzare le immagini nella pagina di login utilizzando Xcode**

1. Apri il progetto `Capture.xcodeproj` in Xcode.

1. Individuate la cartella `www/wsmobile/images`.
1. Per modificare il logo, sostituire il file `aem_icon.png` predefinito con il file `aem_icon.png` personalizzato.
1. Create ed eseguite &#39;app AEM Forms sul dispositivo iOS o sul simulatore iOS.

### Per personalizzare le immagini nelle pagine di login utilizzando Eclipse {#to-customize-images-on-the-login-pages-using-eclipse-1}

1. Apri il progetto Android in Eclipse.

1. Individuate la cartella `assets/www/wsmobile/images`.
1. Per modificare il logo, sostituire il file `aem_icon.png` predefinito con il file `aem_icon.png` personalizzato.
1. Creare ed eseguire &#39;app AEM Forms sul dispositivo Android.

### Per personalizzare le immagini nelle pagine di login utilizzando Visual Studio {#to-customize-images-on-the-login-pages-using-visual-studio-1}

1. Aprire il progetto `MWSWindows.sln` in Visual Studio.

1. Individuate la cartella `MWSWindows\www\wsmobile\images`.
1. Per modificare il logo, sostituire il file `aem_icon.png` predefinito con il file `aem_icon.png` personalizzato.
1. Creare ed eseguire  app AEM Forms sul dispositivo Windows.
