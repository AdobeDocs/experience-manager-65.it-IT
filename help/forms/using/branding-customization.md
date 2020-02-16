---
title: Personalizzazione branding
seo-title: Personalizzazione branding
description: Personalizzate l'icona dell'applicazione, il nome dell'applicazione, le immagini di avvio e la pagina di login per fornire un aspetto e un aspetto specifici dell'organizzazione all'app AEM Forms.
seo-description: Personalizzate l'icona dell'applicazione, il nome dell'applicazione, le immagini di avvio e la pagina di login per fornire un aspetto e un aspetto specifici dell'organizzazione all'app AEM Forms.
uuid: fece0fa8-c417-45eb-93f1-a91b49835fa0
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: f6440a36-719a-4f89-b7db-1af918a3469a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Personalizzazione branding {#branding-customization}

Potete personalizzare l&#39;icona dell&#39;applicazione, il nome dell&#39;applicazione, le immagini di avvio e la pagina di login per fornire un aspetto specifico dell&#39;organizzazione all&#39;app AEM Forms. Ad esempio, potete modificare le immagini per utilizzare i logo aziendali. L&#39;app AEM Forms supporta le seguenti personalizzazioni:

* Personalizzazione delle immagini dell’icona e dell’avvio dell’applicazione
* Personalizzazione del nome dell&#39;app
* Personalizzazione delle immagini nella pagina di login
* Personalizzazione del logo nel menu dell&#39;app

## Personalizzazione delle immagini di icona e lancio {#customizing-icon-and-launch-images}

Per personalizzare l’icona dell’app predefinita e l’immagine di avvio dell’app AEM Forms, effettuate le seguenti operazioni:

>[!NOTE]
>
>Per tutte le icone e immagini, usate il formato PNG non interlacciato.

### Per personalizzare le immagini delle icone e del lancio {#to-customize-icon-and-launch-images}

#### Per iOS {#for-ios}

1. Apri il `Capture.xcodeproj` progetto in Xcode.
1. (***Per personalizzare l’icona***) Nella vista Navigatore di Capture, passare a **[!UICONTROL Capture > Capture > Supporting Files (Cattura > File di supporto) > Capture-info.plist]**. Fare clic sul menu a discesa accanto ai file Icona. Specificate il nome del file di icona (.png) e caricate il file in **[!UICONTROL Capture > Capture > Resources > icons (Cattura > Risorse > icone]**). Le dimensioni attualmente supportate sono: 29x29, 50x50, 58x58, 72x72, 100x100 e 144x144.
1. (***Per personalizzare le immagini*** del lancio) Accertatevi che i nomi file delle immagini siano:

   * Per verticale: `Default-Portrait~ipad.png` e `Default-Portrait@2x~ipad.png`
   * Per orizzontale: `Default-Landscape~ipad.png` e `Default-Landscape@2x~ipad.png`
   Caricateli nel progetto Capture per sostituire i file esistenti nel progetto.

   >[!NOTE]
   >
   >Accertatevi che il nome e la risoluzione dell’immagine corrispondano all’immagine sostituita nel progetto.

1. Creare ed eseguire l&#39;app AEM Forms su un dispositivo iOS o su un simulatore iOS.

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

1. Generate di nuovo l&#39;app AEM Forms.

### Per Windows {#for-windows}

1. Sostituisce le icone nel percorso:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\icons\windows`

1. Sostituisce l’immagine di avvio nel percorso:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\screens\windows`

   >[!NOTE]
   >
   >Accertatevi che il nome e la risoluzione dell’immagine corrispondano all’immagine sostituita nel progetto.

1. Generate di nuovo l&#39;app AEM Forms.

## Personalizzare il nome dell&#39;app {#customize-the-app-name}

### Per iOS {#for-ios-1}

1. Apri il `Capture.xcodeproj` progetto in Xcode.
1. Nella visualizzazione del Navigator di Capture, passa a **[!UICONTROL Capture > Capture > Supporting Files > InfoPlist.strings]**.

   Aggiornate il valore dell&#39; `CFBundleDisplayName` attributo al nome che desiderate visualizzare per l&#39;app.

1. Creare ed eseguire l&#39;app AEM Forms su un dispositivo iOS o su un simulatore iOS.

   Per informazioni dettagliate sulla creazione dell&#39;app per iOS, consultate [Configurare il progetto Xcode e creare l&#39;app](/help/forms/using/setup-xcode-project-build-installer.md)iOS.

### Per Android {#for-android-1}

1. Aprite il seguente file XML in qualsiasi editor di testo o XML:

   `[User_Home]/Projects/[your-project]/src/android/res/values/strings.xml and android/res/values-en/strings.xml`

1. Aggiorna il valore della chiave `app_name`.
1. Generate di nuovo l&#39;app AEM Forms.

   Per informazioni dettagliate sulla creazione dell&#39;app per Android, consultate [Configurare il progetto Eclipse e creare l&#39;app](/help/forms/using/setup-eclipse-project-build-installer.md)Android.

### Per Windows {#for-windows-1}

1. Aprite il seguente file XML in qualsiasi editor di testo:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\config.xml`

1. Aggiornate il valore nel `<name>...</name>` tag .
1. Generate di nuovo l&#39;app AEM Forms.

   Per informazioni dettagliate sulla creazione dell&#39;app per Windows, consultate [Configurare il progetto Visual Studio e creare l&#39;app](/help/forms/using/setup-visual-studio-project-build-installer.md)Windows.

## Personalizzazione delle immagini nella pagina di login {#customizing-images-on-the-login-page}

La pagina di accesso dell&#39;app AEM Forms contiene immagini di logo e sfondo. Il logo si trova sopra la finestra di dialogo di login e l’immagine di sfondo si trova sotto la finestra di dialogo di login. Per personalizzare l’immagine predefinita nella pagina di login, effettuate le seguenti operazioni:

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

1. Apri il `Capture.xcodeproj` progetto in Xcode.

1. Passate alla `www/wsmobile/images`cartella.
1. Per modificare il logo, sostituite il `LC-logo.png` file predefinito con il `LC-logo.png` file personalizzato.
1. Per cambiare lo sfondo, sostituite il `Landing_bg.jpeg` file predefinito con il `Landing_bg.jpeg`file personalizzato.
1. Creare ed eseguire l&#39;app AEM Forms su un dispositivo iOS o su un simulatore iOS.

### Per personalizzare le immagini nelle pagine di login utilizzando Eclipse {#to-customize-images-on-the-login-pages-using-eclipse}

1. Apri il progetto Android in Eclipse.

1. Passate alla `assets/www/wsmobile/images`cartella.
1. Per modificare il logo, sostituite il `LC-logo.png` file predefinito con il `LC-logo.png` file personalizzato.
1. Per cambiare lo sfondo, sostituite il `Landing_bg.jpeg` file predefinito con il `Landing_bg.jpeg`file personalizzato.
1. Creare ed eseguire l&#39;app AEM Forms sul dispositivo Android.

### Personalizzazione di immagini nelle pagine di login mediante Visual Studio {#to-customize-images-on-the-login-pages-using-visual-studio}

1. Aprire il `MWSWindows.sln` progetto in Visual Studio.

1. Passate alla `MWSWindows\www\wsmobile\images`cartella.
1. Per modificare il logo, sostituite il `LC-logo.png` file predefinito con il `LC-logo.png` file personalizzato.
1. Per cambiare lo sfondo, sostituite il `Landing_bg.jpeg` file predefinito con il `Landing_bg.jpeg`file personalizzato.
1. Creare ed eseguire l&#39;app AEM Forms su un dispositivo Windows.

## Personalizzazione del logo nel menu dell&#39;app {#customizing_images_on_the_login_page-1}

Dopo aver effettuato l&#39;accesso all&#39;app AEM Forms e aver toccato il pulsante del menu, il logo è visibile sopra il menu. Per personalizzare il logo predefinito, effettuate le seguenti operazioni:

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

1. Apri il `Capture.xcodeproj` progetto in Xcode.

1. Passate alla `www/wsmobile/images`cartella.
1. Per modificare il logo, sostituite il `aem_icon.png` file predefinito con il `aem_icon.png` file personalizzato.
1. Creare ed eseguire l&#39;app AEM Forms su un dispositivo iOS o su un simulatore iOS.

### Per personalizzare le immagini nelle pagine di login utilizzando Eclipse {#to-customize-images-on-the-login-pages-using-eclipse-1}

1. Apri il progetto Android in Eclipse.

1. Passate alla `assets/www/wsmobile/images`cartella.
1. Per modificare il logo, sostituite il `aem_icon.png` file predefinito con il `aem_icon.png` file personalizzato.
1. Creare ed eseguire l&#39;app AEM Forms sul dispositivo Android.

### Personalizzazione di immagini nelle pagine di login mediante Visual Studio {#to-customize-images-on-the-login-pages-using-visual-studio-1}

1. Aprire il `MWSWindows.sln` progetto in Visual Studio.

1. Passate alla `MWSWindows\www\wsmobile\images`cartella.
1. Per modificare il logo, sostituite il `aem_icon.png` file predefinito con il `aem_icon.png` file personalizzato.
1. Creare ed eseguire l&#39;app AEM Forms su un dispositivo Windows.

[Contattare il supporto](https://www.adobe.com/account/sign-in.supportportal.html)
