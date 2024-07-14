---
title: Personalizzazione branding
description: Personalizza l’icona dell’applicazione, il nome dell’applicazione, le immagini di avvio e la pagina di accesso per conferire all’app AEM Forms un aspetto distinto e specifico per l’organizzazione.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 9333705b-9944-4a74-a30f-7d9ec85fd824
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
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

1. Apri il progetto `Capture.xcodeproj` in Xcode.
1. (***Per personalizzare l&#39;icona***) Nella visualizzazione del navigatore di Acquisizione, passare a **[!UICONTROL Acquisizione > Acquisizione > File di supporto > Acquisizione-info.plist]**. Fai clic sul menu a discesa accanto ai file icona. Specifica il nome del file di icona (.png) e carica il file in **[!UICONTROL Acquisisci > Acquisisci > Risorse > icone]**. Le dimensioni attualmente supportate sono: 29x29, 50x50, 58x58, 72x72, 100x100 e 144x144.
1. (***Per personalizzare le immagini di lancio***) Verifica che i nomi dei file delle immagini siano:

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

1. Apri il progetto `Capture.xcodeproj` in Xcode.
1. Nella visualizzazione del Navigator di Acquisizione, passare a **[!UICONTROL Acquisizione > Acquisizione > File di supporto > InfoPlist.strings]**.

   Aggiornare il valore dell&#39;attributo `CFBundleDisplayName` a un nome che si desidera visualizzare per l&#39;app.

1. Crea ed esegui l’app AEM Forms sul dispositivo iOS o sul simulatore iOS.

   Per informazioni dettagliate sulla creazione dell&#39;app per iOS, consulta [Configurare il progetto Xcode e creare l&#39;app iOS](/help/forms/using/setup-xcode-project-build-installer.md).

### Per Android {#for-android-1}

1. Apri il seguente XML in qualsiasi editor di testo o Xml:

   `[User_Home]/Projects/[your-project]/src/android/res/values/strings.xml and android/res/values-en/strings.xml`

1. Aggiornare il valore per la chiave `app_name`.
1. Rigenera l’app AEM Forms.

   Per informazioni dettagliate sulla creazione dell&#39;app per Android, consulta [Configurare il progetto Eclipse e creare l&#39;app Android](/help/forms/using/setup-eclipse-project-build-installer.md).

### Per Windows {#for-windows-1}

1. Apri il seguente XML in qualsiasi editor di testo:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\config.xml`

1. Aggiorna il valore nel tag `<name>...</name>`.
1. Rigenera l’app AEM Forms.

   Per informazioni dettagliate sulla creazione dell&#39;app per Windows, vedere [Configurare il progetto Visual Studio e creare l&#39;app Windows](/help/forms/using/setup-visual-studio-project-build-installer.md).

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

1. Apri il progetto `Capture.xcodeproj` in Xcode.

1. Passare alla cartella `www/wsmobile/images`.
1. Per modificare il logo, sostituire il file `LC-logo.png` predefinito con il file `LC-logo.png` personalizzato.
1. Per cambiare lo sfondo, sostituire il file `Landing_bg.jpeg` predefinito con il file `Landing_bg.jpeg` personalizzato.
1. Crea ed esegui l’app AEM Forms sul dispositivo iOS o sul simulatore iOS.

### Per personalizzare le immagini nelle pagine di accesso tramite Eclipse {#to-customize-images-on-the-login-pages-using-eclipse}

1. Apri il progetto Android in Eclipse.

1. Passare alla cartella `assets/www/wsmobile/images`.
1. Per modificare il logo, sostituire il file `LC-logo.png` predefinito con il file `LC-logo.png` personalizzato.
1. Per cambiare lo sfondo, sostituire il file `Landing_bg.jpeg` predefinito con il file `Landing_bg.jpeg` personalizzato.
1. Crea ed esegui l’app AEM Forms sul dispositivo Android.

### Per personalizzare le immagini nelle pagine di accesso tramite Visual Studio {#to-customize-images-on-the-login-pages-using-visual-studio}

1. Aprire il progetto `MWSWindows.sln` in Visual Studio.

1. Passare alla cartella `MWSWindows\www\wsmobile\images`.
1. Per modificare il logo, sostituire il file `LC-logo.png` predefinito con il file `LC-logo.png` personalizzato.
1. Per cambiare lo sfondo, sostituire il file `Landing_bg.jpeg` predefinito con il file `Landing_bg.jpeg` personalizzato.
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

1. Apri il progetto `Capture.xcodeproj` in Xcode.

1. Passare alla cartella `www/wsmobile/images`.
1. Per modificare il logo, sostituire il file `aem_icon.png` predefinito con il file `aem_icon.png` personalizzato.
1. Crea ed esegui l’app AEM Forms sul dispositivo iOS o sul simulatore iOS.

### Per personalizzare le immagini nelle pagine di accesso tramite Eclipse {#to-customize-images-on-the-login-pages-using-eclipse-1}

1. Apri il progetto Android in Eclipse.

1. Passare alla cartella `assets/www/wsmobile/images`.
1. Per modificare il logo, sostituire il file `aem_icon.png` predefinito con il file `aem_icon.png` personalizzato.
1. Crea ed esegui l’app AEM Forms sul dispositivo Android.

### Per personalizzare le immagini nelle pagine di accesso tramite Visual Studio {#to-customize-images-on-the-login-pages-using-visual-studio-1}

1. Aprire il progetto `MWSWindows.sln` in Visual Studio.

1. Passare alla cartella `MWSWindows\www\wsmobile\images`.
1. Per modificare il logo, sostituire il file `aem_icon.png` predefinito con il file `aem_icon.png` personalizzato.
1. Crea ed esegui l’app AEM Forms su un dispositivo Windows.
