---
title: Personalizzazione branding
description: Personalizza l’icona dell’applicazione, il nome dell’applicazione, le immagini di avvio e la pagina di accesso per conferire all’app AEM Forms un aspetto distinto e specifico per l’organizzazione.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 9333705b-9944-4a74-a30f-7d9ec85fd824
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 1%

---

# Personalizzazione branding {#branding-customization}

Puoi personalizzare l’icona dell’applicazione, il nome dell’applicazione, le immagini di avvio e la pagina di accesso per fornire all’app AEM Forms un aspetto specifico per l’organizzazione. Ad esempio, puoi modificare le immagini per utilizzare i logo della tua organizzazione. L’app AEM Forms supporta le seguenti personalizzazioni:

* Personalizzazione dell’icona dell’applicazione e delle immagini di avvio
* Personalizzazione del nome dell’app
* Personalizzazione delle immagini nella pagina di accesso
* Personalizzazione del logo nel menu dell’app

## Personalizzazione delle immagini di icone e lanci {#customizing-icon-and-launch-images}

Per personalizzare l’icona predefinita dell’app e l’immagine di avvio dell’app AEM Forms, effettua le seguenti operazioni:

>[!NOTE]
>
>Per tutte le icone e le immagini, utilizzate il formato PNG non interlacciato.

### Per personalizzare le immagini delle icone e dei lanci {#to-customize-icon-and-launch-images}

#### Per iOS {#for-ios}

1. Apri `Capture.xcodeproj` progetto in Xcode.
1. (***Icona per la personalizzazione***) Nella vista Navigatore di Acquisizione, passare a **[!UICONTROL Capture > Capture > Supporting Files > Capture-info.plist]**. Fai clic sul menu a discesa accanto ai file icona. Specifica il nome del file di icona (.png) e carica il file in **[!UICONTROL Acquisizione > Acquisizione > Risorse > icone]**. Le dimensioni attualmente supportate sono: 29x29, 50x50, 58x58, 72x72, 100x100 e 144x144.
1. (***Per personalizzare le immagini di lancio***) Accertatevi che i nomi dei file delle immagini siano:

   * Per ritratto: `Default-Portrait~ipad.png` e `Default-Portrait@2x~ipad.png`
   * Per orizzontale: `Default-Landscape~ipad.png` e `Default-Landscape@2x~ipad.png`

   Caricali nel progetto Acquisizione per sostituire i file esistenti nel progetto.

   >[!NOTE]
   >
   >Assicurati che il nome e la risoluzione dell’immagine corrispondano a quelli sostituiti nel progetto.

1. Crea ed esegui l’app AEM Forms sul dispositivo iOS o sul simulatore iOS.

#### Per Android {#for-android}

1. Denomina i file dell&#39;icona dell&#39;applicazione come:

   `ic_launcher.png`

1. Posizionare i file di icona corrispondenti nelle directory seguenti:

   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-hdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-mdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxxhdpi`

   >[!NOTE]
   >
   >Assicurati che il nome e la risoluzione dell’immagine corrispondano a quelli sostituiti nel progetto.

1. Rigenera l’app AEM Forms.

### Per Windows {#for-windows}

1. Sostituisci le icone nel percorso:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\icons\windows`

1. Sostituisci l’immagine di avvio nel percorso:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\screens\windows`

   >[!NOTE]
   >
   >Assicurati che il nome e la risoluzione dell’immagine corrispondano a quelli sostituiti nel progetto.

1. Rigenera l’app AEM Forms.

## Personalizzare il nome dell’app {#customize-the-app-name}

### Per iOS {#for-ios-1}

1. Apri `Capture.xcodeproj` progetto in Xcode.
1. Nella vista navigatore di Acquisizione, passare a **[!UICONTROL Cattura > Cattura > File di supporto > InfoPlist.strings]**.

   Aggiorna il valore per `CFBundleDisplayName` attributo a un nome che desideri visualizzare per l’app.

1. Crea ed esegui l’app AEM Forms sul dispositivo iOS o sul simulatore iOS.

   Per informazioni dettagliate sulla creazione dell’app per iOS, consulta [Configurare il progetto Xcode e creare l’app iOS](/help/forms/using/setup-xcode-project-build-installer.md).

### Per Android {#for-android-1}

1. Apri il seguente XML in qualsiasi editor di testo o Xml:

   `[User_Home]/Projects/[your-project]/src/android/res/values/strings.xml and android/res/values-en/strings.xml`

1. Aggiorna il valore della chiave `app_name`.
1. Rigenera l’app AEM Forms.

   Per informazioni dettagliate sulla creazione dell’app per Android, consulta [Configurare il progetto Eclipse e creare l’app Android](/help/forms/using/setup-eclipse-project-build-installer.md).

### Per Windows {#for-windows-1}

1. Apri il seguente XML in qualsiasi editor di testo:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\config.xml`

1. Aggiornare il valore in `<name>...</name>` tag.
1. Rigenera l’app AEM Forms.

   Per informazioni dettagliate sulla creazione dell’app per Windows, consulta [Configurare il progetto Visual Studio e creare l&#39;app Windows](/help/forms/using/setup-visual-studio-project-build-installer.md).

## Personalizzazione delle immagini nella pagina di accesso {#customizing-images-on-the-login-page}

La pagina di accesso dell’app AEM Forms contiene il logo e le immagini di sfondo. Il logo si trova sopra la finestra di dialogo di accesso e l&#39;immagine di sfondo si trova sotto la finestra di dialogo di accesso. Per personalizzare l&#39;immagine predefinita nella pagina di accesso, effettua le seguenti operazioni:

**Prima di iniziare**

Verifica di disporre delle seguenti immagini:

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

**Per personalizzare le immagini nella pagina di accesso tramite Xcode**

1. Apri `Capture.xcodeproj` progetto in Xcode.

1. Accedi a `www/wsmobile/images`cartella.
1. Per modificare il logo, sostituisci quello predefinito `LC-logo.png` file con il file personalizzato `LC-logo.png` file.
1. Per cambiare lo sfondo, sostituisci il predefinito `Landing_bg.jpeg` file con il file personalizzato `Landing_bg.jpeg`file.
1. Crea ed esegui l’app AEM Forms sul dispositivo iOS o sul simulatore iOS.

### Per personalizzare le immagini nelle pagine di accesso tramite Eclipse {#to-customize-images-on-the-login-pages-using-eclipse}

1. Apri il progetto Android in Eclipse.

1. Accedi a `assets/www/wsmobile/images`cartella.
1. Per modificare il logo, sostituisci quello predefinito `LC-logo.png` file con il file personalizzato `LC-logo.png` file.
1. Per cambiare lo sfondo, sostituisci il predefinito `Landing_bg.jpeg` file con il file personalizzato `Landing_bg.jpeg`file.
1. Crea ed esegui l’app AEM Forms su un dispositivo Android.

### Per personalizzare le immagini nelle pagine di accesso tramite Visual Studio {#to-customize-images-on-the-login-pages-using-visual-studio}

1. Apri `MWSWindows.sln` progetto in Visual Studio.

1. Accedi a `MWSWindows\www\wsmobile\images`cartella.
1. Per modificare il logo, sostituisci quello predefinito `LC-logo.png` file con il file personalizzato `LC-logo.png` file.
1. Per cambiare lo sfondo, sostituisci il predefinito `Landing_bg.jpeg` file con il file personalizzato `Landing_bg.jpeg`file.
1. Crea ed esegui l’app AEM Forms su un dispositivo Windows.

## Personalizzazione del logo nel menu dell’app {#customizing_images_on_the_login_page-1}

Dopo aver effettuato l’accesso all’app AEM Forms e aver selezionato il pulsante del menu, puoi visualizzare il logo sopra il menu. Per personalizzare il logo predefinito, effettua le seguenti operazioni:

**Prima di iniziare**

Verifica di disporre della seguente immagine:

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

**Per personalizzare le immagini nella pagina di accesso tramite Xcode**

1. Apri `Capture.xcodeproj` progetto in Xcode.

1. Accedi a `www/wsmobile/images`cartella.
1. Per modificare il logo, sostituisci quello predefinito `aem_icon.png` file con il file personalizzato `aem_icon.png` file.
1. Crea ed esegui l’app AEM Forms sul dispositivo iOS o sul simulatore iOS.

### Per personalizzare le immagini nelle pagine di accesso tramite Eclipse {#to-customize-images-on-the-login-pages-using-eclipse-1}

1. Apri il progetto Android in Eclipse.

1. Accedi a `assets/www/wsmobile/images`cartella.
1. Per modificare il logo, sostituisci quello predefinito `aem_icon.png` file con il file personalizzato `aem_icon.png` file.
1. Crea ed esegui l’app AEM Forms su un dispositivo Android.

### Per personalizzare le immagini nelle pagine di accesso tramite Visual Studio {#to-customize-images-on-the-login-pages-using-visual-studio-1}

1. Apri `MWSWindows.sln` progetto in Visual Studio.

1. Accedi a `MWSWindows\www\wsmobile\images`cartella.
1. Per modificare il logo, sostituisci quello predefinito `aem_icon.png` file con il file personalizzato `aem_icon.png` file.
1. Crea ed esegui l’app AEM Forms su un dispositivo Windows.
