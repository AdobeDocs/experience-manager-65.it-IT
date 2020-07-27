---
title: Configurare il progetto Xcode e creare l'app iOS
seo-title: Configurare il progetto Xcode e creare l'app iOS
description: Spiega come creare app AEM Forms standard per iOS.
seo-description: Spiega come creare app AEM Forms standard per iOS.
uuid: 29779bbb-06b4-4ece-9f29-786afab59eaf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 88555db2-712f-4ef9-bf47-76c7ba83d964
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---


# Configurare il progetto Xcode e creare l&#39;app iOS{#set-up-the-xcode-project-and-build-the-ios-app}

AEM Forms fornisce il codice sorgente completo dell&#39;app AEM Forms. L&#39;origine contiene tutti i componenti per creare un&#39;app AEM Forms personalizzata. L&#39;archivio del codice sorgente `adobe-lc-mobileworkspace-src-<version>.zip` è una parte del `adobe-aemfd-forms-app-src-pkg-<version>.zip` pacchetto sulla distribuzione del software.

Per ottenere l&#39;origine dell&#39;app AEM Forms, effettua le seguenti operazioni:

1. Apri distribuzione [](https://experience.adobe.com/downloads)software. È necessario un Adobe ID  per accedere a Distribuzione software.
1. Toccate **[!UICONTROL Adobe Experience Manager]** disponibile nel menu dell&#39;intestazione.
1. Nella sezione **[!UICONTROL Filtri]** :
   1. Selezionare **[!UICONTROL Forms]** dall&#39;elenco a discesa **[!UICONTROL Soluzione]** .
   2. Selezionate la versione e digitate il tipo di pacchetto. Potete anche utilizzare l&#39;opzione Download **[!UICONTROL di]** ricerca per filtrare i risultati.
1. Toccate il nome del pacchetto applicabile al sistema operativo in uso, selezionate **[!UICONTROL Accetta termini]** EULA e toccate **[!UICONTROL Scarica]**.
1. Aprite [Package Manager](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) e fate clic su **[!UICONTROL Carica pacchetto]** per caricare il pacchetto.
1. Select the package and click **[!UICONTROL Install]**.

1. Per scaricare l&#39;archivio del codice sorgente, aprite `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` nel browser.
Il pacchetto di origine viene scaricato sul dispositivo.

Nell’immagine seguente sono visualizzati i contenuti estratti dell’ `adobe-lc-mobileworkspace-src-<version>.zip`.

![mws-content](assets/mws-content.png)

La tabella seguente riassume il contenuto della `adobe-lc-mobileworkspace-src-[version]/ios` cartella.

<table>
 <tbody>
  <tr>
   <th><p>Directory</p> </th>
   <th><p>Contenuto</p> </th>
  </tr>
  <tr>
   <td><p><code>CordovaLib</code></p> </td>
   <td><p>PhoneGap SDK 6.4.0</p> </td>
  </tr>
  <tr>
   <td><p><code>AEM Forms</code></p> </td>
   <td><p>Risorse, plug-in PhoneGap e modulo principale dell'applicazione</p> </td>
  </tr>
  <tr>
   <td><p><code>AEM Forms.xcodeproj</code></p> </td>
   <td><p>Progetto Xcode per l'app AEM Forms</p> </td>
  </tr>
  <tr>
   <td><p><code>www</code></p> </td>
   <td><p>File HTML, CSS, immagini e JavaScript per il progetto dell'app AEM Forms</p> </td>
  </tr>
 </tbody>
</table>

Per informazioni dettagliate sulla firma del codice e l&#39;aggiunta di dispositivi al portale di provisioning iOS, consultate Configurazione, elaborazione e risoluzione dei problemi della firma del codice [iOS](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html).

## Creare app AEM Forms standard {#set-up-the-xcode-project}

1. Per impostare un progetto in Xcode e fornire un&#39;identità di firma, procedere come segue:

   Accedete al computer Mac in cui è installato e configurato Xcode e iOS SDK.

1. Copiate l&#39; `adobe-lc-mobileworkspace-src-<version>.zip` archivio dalla cartella dei download a `[User_Home]/Projects/`.
1. Estrarre l&#39;archivio nella `[User_Home]/Projects/[your-project]`directory.
1. Andate alla directory del ` [User_Home]/Projects/ `[vostro progetto]`/adobe-lc-mobileworkspace-src-[version]/ios` .
1. Apri il `AEM Forms.xcodeproj` progetto in Xcode.
1. Fate clic su **AEM Forms**, in **TARGET**, selezionate **AEM Forms**. Selezionate la scheda Impostazioni **** build, individuate la sezione Adesione firma **** codice, quindi nei campi Debug e Rilascio effettuate una delle seguenti operazioni:

   * Non specificare i campi per creare un&#39;app Mobile Workspace standard
   * Specificate i campi in base a quanto spiegato in [Creazione di un&#39;app per AEM Forms protetti per iOS](/help/forms/using/building-secure-mobile-workspace-app.md) per creare un&#39;app per AEM Forms protetti.

1. Nella scheda **Impostazioni** build, fai clic su **Tutto** , quindi su **Combinato**.
1. Dall&#39;elenco **Impostazioni** , espandere Firma **codice**.
1. Per Identità **firma** codice, selezionare la firma appropriata. Per informazioni dettagliate sulla creazione di nuove firme, vedere [Creazione e scaricamento di profili](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)di provisioning di sviluppo.
1. Verifica che la stessa firma sia selezionata per **Debug**, **Release** e **Qualsiasi SDK** iOS.
1. Sostituire il seguente codice nel `AEM Forms-info.plist` file:

   ```xml
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSAllowsArbitraryLoads</key>
   <true/>
   </dict>
   ```

   con il seguente nome durante la sostituzione `yourserver.com` con un nome host appropriato per il server.

   ```xml
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSExceptionDomains</key>
   <dict>
   <key>yourserver.com</key>
   <dict>
   <!-Include to allow subdomains->
   <key>NSIncludesSubdomains</key>
   <true/>
   <!-Include to allow HTTP requests->
   <key>NSTemporaryExceptionAllowsInsecureHTTPLoads</key>
   <true/>
   <!-Include to support forward secrecy->
   <key>NSExceptionRequiresForwardSecrecy</key>
   <false/>
   <!-Include to specify minimum TLS version->
   <key>NSTemporaryExceptionMinimumTLSVersion</key>
   <string>TLSv1.1</string>
   </dict>
   </dict>
   </dict>
   ```

   >[!NOTE]
   >
   >Questo passaggio è richiesto solo se l&#39;app AEM Forms deve connettersi a un server che non soddisfa i requisiti di sicurezza di Trasporto app.

1. In **PROJECT**, selezionare **AEM Forms** e assicurarsi che la firma appropriata sia selezionata per Identità **firma** codice, **Debug**, **Rilascio** **** e Qualsiasi SDK iOS.
1. Collegate un iPad in provisioning a un computer Mac.
1. Selezionate il dispositivo di provisioning per il progetto **AEM Forms** .

   ![ipad](assets/ipad.png)

   È selezionato un dispositivo con provisioning, iPad Air 2.

1. Selezionare **Prodotto** > **Pulisci**.
1. Selezionate **Prodotto** > **Genera**.

## Creare il programma di installazione per l&#39;app AEM Forms {#build-the-installer-for-the-mobile-workspace-app}

È necessario archiviare il progetto Xcode per creare il programma di installazione (un file .ipa) e un file elenco di proprietà (un file .plist). Il file dell&#39;elenco delle proprietà contiene le informazioni di configurazione dell&#39;app in hosting, ad esempio il nome e il percorso di hosting dell&#39;app. Per ulteriori informazioni sul file dell&#39;elenco delle proprietà, vedere [Informazioni sui file](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html)dell&#39;elenco delle proprietà.

1. Collegate un iPad in provisioning a un computer Mac. Per informazioni dettagliate sul provisioning di un iPad, consultate [Creazione e scaricamento di profili di provisioning di sviluppo](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)
1. Selezionate il dispositivo di provisioning per il progetto **AEM Forms** .

   ![ipad-1](assets/ipad-1.png)

   È selezionato un dispositivo con provisioning, iPad Air 2.

1. Selezionare **Prodotto** > **Pulisci**.
1. Selezionate **Prodotto** > **Genera**.
1. Selezionate **Prodotto** > **Archivio**.
1. In Organizer - Archivi, seleziona l’archivio più recente del progetto e fai clic su **Distribuisci**.
1. Selezionate **Salva per distribuzione** Enterprise o Ad Hoc come metodo di distribuzione e fate clic su **Avanti**.
1. Selezionare l&#39;identità **di firma del** codice appropriata e fare clic su **Avanti**. Fare clic su **Consenti** di applicare la firma.
1. Immettete il nome dell&#39;app e selezionate **Salva per distribuzione** Enterprise.
1. Fornite l&#39;URL **** applicazione per l&#39;app. Ad esempio, per ospitare l&#39;app su un server CRX, immetti l&#39;URL `https://[LC_host]:'port'/lc/content/distribution/mobileworkspace/APP_NAME.ipa`.
1. Nel campo **Titolo** , specificate i AEM Forms.
1. Click **Save** and close Xcode.

   Nel percorso specificato vengono creati un file del programma di installazione `AEM Forms.ipa`e un file dell&#39;elenco delle proprietà `AEM Forms-info.plist`.

1. Aprite il `AEM Forms-info.plist` file in un editor.
1. Sostituite tutti gli spazi nell’URL del file .ipa con %20.
1. Salvate e chiudete il `AEM Forms-info.plist` file.