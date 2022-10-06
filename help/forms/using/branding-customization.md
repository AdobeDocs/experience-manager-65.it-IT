---
title: Personalizzazione branding
seo-title: Branding Customization
description: Personalizza l’icona dell’applicazione, il nome dell’applicazione, le immagini di lancio e la pagina di accesso per fornire un aspetto e un aspetto distinti dell’organizzazione all’app AEM Forms.
seo-description: Customize the application icon, application name, launch images, and login page to provide a distinct organization-specific look and feel to AEM Forms app.
uuid: fece0fa8-c417-45eb-93f1-a91b49835fa0
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: f6440a36-719a-4f89-b7db-1af918a3469a
exl-id: 9333705b-9944-4a74-a30f-7d9ec85fd824
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 2%

---

# Personalizzazione branding {#branding-customization}

Puoi personalizzare l’icona dell’applicazione, il nome dell’applicazione, le immagini di avvio e la pagina di accesso per fornire all’app AEM Forms un aspetto specifico per l’organizzazione. Ad esempio, puoi modificare le immagini per utilizzare i loghi della tua organizzazione. L’app AEM Forms supporta le seguenti personalizzazioni:

* Personalizzazione dell’icona dell’applicazione e delle immagini di lancio
* Personalizzazione del nome dell’app
* Personalizzazione delle immagini nella pagina di accesso
* Personalizzazione del logo nel menu dell’app

## Personalizzazione delle immagini icona e lancio {#customizing-icon-and-launch-images}

Per personalizzare l’icona dell’app predefinita e l’immagine di avvio dell’app AEM Forms, effettua le seguenti operazioni:

>[!NOTE]
>
>Per tutte le icone e le immagini, utilizza il formato PNG non interlacciato.

### Personalizzazione delle immagini icona e lancio {#to-customize-icon-and-launch-images}

#### Per iOS {#for-ios}

1. Apri `Capture.xcodeproj` progetto in Xcode.
1. (***Icona per personalizzare***) Nella visualizzazione Navigatore di Capture, passare a **[!UICONTROL Cattura > Cattura > File di supporto > Capture-info.plist]**. Fai clic sull’elenco a discesa accanto ai file Icona . Specifica il nome del file di icona (.png) e carica il file in **[!UICONTROL Cattura > Cattura > Risorse > icone]**. Le dimensioni attualmente supportate sono: 29x29, 50x50, 58x58, 72x72, 100x100 e 144x144.
1. (***Per personalizzare le immagini di lancio***) Assicurati che i nomi dei file delle immagini siano:

   * Per verticale: `Default-Portrait~ipad.png` e `Default-Portrait@2x~ipad.png`
   * Per orizzontale: `Default-Landscape~ipad.png` e `Default-Landscape@2x~ipad.png`

   Caricali nel progetto Capture per sostituire i file esistenti nel progetto.

   >[!NOTE]
   >
   >Assicurati che il nome e la risoluzione dell&#39;immagine corrispondano all&#39;immagine sostituita nel progetto.

1. Crea ed esegui l’app AEM Forms sul dispositivo iOS o sul simulatore iOS.

#### Per Android {#for-android}

1. Denomina i file delle icone dell&#39;applicazione come:

   `ic_launcher.png`

1. Posiziona i file di icona corrispondenti nelle seguenti directory:

   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-hdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-mdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxxhdpi`

   >[!NOTE]
   >
   >Assicurati che il nome e la risoluzione dell&#39;immagine corrispondano all&#39;immagine sostituita nel progetto.

1. Rigenera l’app AEM Forms.

### Per Windows {#for-windows}

1. Sostituisci le icone nel percorso:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\icons\windows`

1. Sostituisci l’immagine del modulo di avvio nel percorso:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\screens\windows`

   >[!NOTE]
   >
   >Assicurati che il nome e la risoluzione dell&#39;immagine corrispondano all&#39;immagine sostituita nel progetto.

1. Rigenera l’app AEM Forms.

## Personalizzare il nome dell’app {#customize-the-app-name}

### Per iOS {#for-ios-1}

1. Apri `Capture.xcodeproj` progetto in Xcode.
1. Nella visualizzazione Navigatore di Capture, passare a **[!UICONTROL Cattura > Cattura > File di supporto > InfoPlist.strings]**.

   Aggiorna il valore per `CFBundleDisplayName` Attributo a un nome che desideri visualizzare per l&#39;app.

1. Crea ed esegui l’app AEM Forms sul dispositivo iOS o sul simulatore iOS.

   Per informazioni dettagliate sulla creazione dell’app per iOS, vedi [Configurare il progetto Xcode e creare l&#39;app iOS](/help/forms/using/setup-xcode-project-build-installer.md).

### Per Android {#for-android-1}

1. Apri il seguente file XML in qualsiasi editor di testo o XML:

   `[User_Home]/Projects/[your-project]/src/android/res/values/strings.xml and android/res/values-en/strings.xml`

1. Aggiorna il valore della chiave `app_name`.
1. Rigenera l’app AEM Forms.

   Per i dettagli sulla creazione dell&#39;app per Android, vedi [Configurare il progetto Eclipse e creare l’app Android](/help/forms/using/setup-eclipse-project-build-installer.md).

### Per Windows {#for-windows-1}

1. Apri il seguente file XML in qualsiasi editor di testo:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\config.xml`

1. Aggiorna il valore in `<name>...</name>` tag .
1. Rigenera l’app AEM Forms.

   Per informazioni dettagliate sulla creazione dell&#39;app per Windows, vedi [Configurare il progetto Visual Studio e creare l&#39;app Windows](/help/forms/using/setup-visual-studio-project-build-installer.md).

## Personalizzazione delle immagini nella pagina di accesso {#customizing-images-on-the-login-page}

La pagina di accesso dell’app AEM Forms dispone di logo e immagini di sfondo. Il logo si trova sopra la finestra di dialogo di accesso e l’immagine di sfondo si trova sotto la finestra di dialogo di accesso. Esegui i seguenti passaggi per personalizzare l’immagine predefinita nella pagina di accesso:

**Prima di iniziare**

Assicurati di avere le seguenti immagini:

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

**Per personalizzare le immagini nella pagina di accesso utilizzando Xcode**

1. Apri `Capture.xcodeproj` progetto in Xcode.

1. Passa a `www/wsmobile/images`cartella.
1. Per modificare il logo, sostituisci il predefinito `LC-logo.png` con il file personalizzato `LC-logo.png` file.
1. Per modificare lo sfondo, sostituisci il valore predefinito `Landing_bg.jpeg` con il file personalizzato `Landing_bg.jpeg`file.
1. Crea ed esegui l’app AEM Forms sul dispositivo iOS o sul simulatore iOS.

### Per personalizzare le immagini nelle pagine di login utilizzando Eclipse {#to-customize-images-on-the-login-pages-using-eclipse}

1. Apri il progetto Android in Eclipse.

1. Passa a `assets/www/wsmobile/images`cartella.
1. Per modificare il logo, sostituisci il predefinito `LC-logo.png` con il file personalizzato `LC-logo.png` file.
1. Per modificare lo sfondo, sostituisci il valore predefinito `Landing_bg.jpeg` con il file personalizzato `Landing_bg.jpeg`file.
1. Crea ed esegui l’app AEM Forms sul dispositivo Android.

### Personalizzazione di immagini nelle pagine di accesso tramite Visual Studio {#to-customize-images-on-the-login-pages-using-visual-studio}

1. Apri `MWSWindows.sln` progetto in Visual Studio.

1. Passa a `MWSWindows\www\wsmobile\images`cartella.
1. Per modificare il logo, sostituisci il predefinito `LC-logo.png` con il file personalizzato `LC-logo.png` file.
1. Per modificare lo sfondo, sostituisci il valore predefinito `Landing_bg.jpeg` con il file personalizzato `Landing_bg.jpeg`file.
1. Crea ed esegui l’app AEM Forms sul dispositivo Windows.

## Personalizzazione del logo nel menu dell’app {#customizing_images_on_the_login_page-1}

Dopo aver effettuato l’accesso all’app AEM Forms e aver toccato il pulsante del menu , puoi vedere il logo sopra il menu. Per personalizzare il logo predefinito, effettua le seguenti operazioni:

**Prima di iniziare**

Assicurati di avere la seguente immagine:

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

**Per personalizzare le immagini nella pagina di accesso utilizzando Xcode**

1. Apri `Capture.xcodeproj` progetto in Xcode.

1. Passa a `www/wsmobile/images`cartella.
1. Per modificare il logo, sostituisci l’impostazione predefinita `aem_icon.png` con il file personalizzato `aem_icon.png` file.
1. Crea ed esegui l’app AEM Forms sul dispositivo iOS o sul simulatore iOS.

### Per personalizzare le immagini nelle pagine di login utilizzando Eclipse {#to-customize-images-on-the-login-pages-using-eclipse-1}

1. Apri il progetto Android in Eclipse.

1. Passa a `assets/www/wsmobile/images`cartella.
1. Per modificare il logo, sostituisci l’impostazione predefinita `aem_icon.png` con il file personalizzato `aem_icon.png` file.
1. Crea ed esegui l’app AEM Forms sul dispositivo Android.

### Personalizzazione di immagini nelle pagine di accesso tramite Visual Studio {#to-customize-images-on-the-login-pages-using-visual-studio-1}

1. Apri `MWSWindows.sln` progetto in Visual Studio.

1. Passa a `MWSWindows\www\wsmobile\images`cartella.
1. Per modificare il logo, sostituisci l’impostazione predefinita `aem_icon.png` con il file personalizzato `aem_icon.png` file.
1. Crea ed esegui l’app AEM Forms sul dispositivo Windows.
