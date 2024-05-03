---
title: Configurare il progetto Xcode e creare l’app iOS
description: Come creare un’app AEM Forms standard per iOS.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 78ce6107-8821-47d6-86ab-7ab968945e7c
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 2%

---

# Configurare il progetto Xcode e creare l’app iOS{#set-up-the-xcode-project-and-build-the-ios-app}

AEM Forms fornisce il codice sorgente completo dell’app AEM Forms. L’origine contiene tutti i componenti per la creazione di un’app AEM Forms personalizzata. L’archivio del codice sorgente, `adobe-lc-mobileworkspace-src-<version>.zip` fa parte di `adobe-aemfd-forms-app-src-pkg-<version>.zip` pacchetto sulla Distribuzione di software.

Per ottenere l’origine dell’app AEM Forms, effettua le seguenti operazioni:

1. Apri [Software Distribution](https://experience.adobe.com/downloads). Per accedere a Software Distribution è necessario disporre di un Adobe ID.
1. Seleziona **[!UICONTROL Adobe Experience Manager]** disponibile nel menu di intestazione.
1. In **[!UICONTROL Filtri]** sezione:
   1. Seleziona **[!UICONTROL Forms]** dal **[!UICONTROL Soluzione]** elenco a discesa.
   2. Seleziona la versione e digita per il pacchetto. È inoltre possibile utilizzare **[!UICONTROL Cerca download]** per filtrare i risultati.
1. Selezionare il nome del pacchetto applicabile al sistema operativo in uso, quindi selezionare **[!UICONTROL Accetta termini EULA]**, e seleziona **[!UICONTROL Scarica]**.
1. Apri [Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)  e fai clic su **[!UICONTROL Carica pacchetto]** per caricare il pacchetto.
1. Seleziona il pacchetto e fai clic su **[!UICONTROL Installa]**.

1. Per scaricare l’archivio del codice sorgente, apri `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` nel browser.
Il pacchetto sorgente viene scaricato sul dispositivo.

Nell&#39;immagine seguente viene visualizzato il contenuto estratto del `adobe-lc-mobileworkspace-src-<version>.zip`.

![mws-content](assets/mws-content.png)

La tabella seguente descrive il contenuto di `adobe-lc-mobileworkspace-src-[version]/ios` cartella.

<table>
 <tbody>
  <tr>
   <th><p>Directory</p> </th>
   <th><p>Contenuto</p> </th>
  </tr>
  <tr>
   <td><p><code>CordovaLib</code></p> </td>
   <td><p>SDK di PhoneGap 6.4.0</p> </td>
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
   <td><p>File HTML, CSS, immagini e JavaScript per il progetto di app AEM Forms</p> </td>
  </tr>
 </tbody>
</table>

Per informazioni dettagliate sulla firma del codice e sull&#39;aggiunta di dispositivi al portale di provisioning di iOS, vedere [Configurazione, processo e risoluzione dei problemi di iOS Code Signing](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html).

## Creare un’app AEM Forms standard {#set-up-the-xcode-project}

1. Per configurare un progetto in Xcode e fornire un’identità di firma, effettua le seguenti operazioni:

   Accedi al computer Mac in cui sono installati e configurati Xcode e iOS SDK.

1. Copia il `adobe-lc-mobileworkspace-src-<version>.zip` archiviare dalla cartella dei download in `[User_Home]/Projects/`.
1. Estrarre l’archivio in `[User_Home]/Projects/[your-project]`directory.
1. Accedi a ` [User_Home]/Projects/ `[il tuo progetto]`/adobe-lc-mobileworkspace-src-[version]/ios` directory.
1. Apri `AEM Forms.xcodeproj` progetto in Xcode.
1. Clic **AEM Forms**, in **TARGET**, seleziona **AEM Forms**. Seleziona la **Impostazioni build** , individua la scheda **Diritto alla firma del codice** e nei campi Debug e Release eseguire una delle operazioni seguenti:

   * Lascia i campi non specificati per creare un’app standard per Mobile Workspace
   * Specifica i campi da visualizzare come descritto in [Creazione di un’app Secure AEM Forms per iOS](/help/forms/using/building-secure-mobile-workspace-app.md) per creare un’app AEM Forms sicura.

1. In **Impostazioni build** , fare clic su **Tutti** e quindi fare clic su **Combinato**.
1. Dalla sezione **Impostazioni** list, expand **Firma codice**.
1. Per **Identità firma codice**, selezionare la firma appropriata. Per informazioni dettagliate sulla creazione di nuove firme, vedere [Creazione e download di profili di provisioning di sviluppo](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html).
1. Assicurati che la stessa firma sia selezionata per **Debug**, **Versione**, e **Qualsiasi SDK di iOS**.
1. Sostituisci il seguente codice in `AEM Forms-info.plist` file:

   ```xml
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSAllowsArbitraryLoads</key>
   <true/>
   </dict>
   ```

   con quanto segue durante la sostituzione `yourserver.com` con un nome host appropriato per il server.

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
   >Questo passaggio è necessario solo se l’app AEM Forms deve connettersi a un server che non rispetta i requisiti di sicurezza del trasporto dell’app.

1. Sotto **PROGETTO**, seleziona **AEM Forms** e accertarsi che sia selezionata la firma appropriata per **Identità firma codice**, **Debug**, **Versione** e **Qualsiasi SDK di iOS**.
1. Connetti un’iPad con provisioning a un computer Mac.
1. Seleziona il dispositivo per il quale è stato eseguito il provisioning **AEM Forms** progetto.

   ![ipad](assets/ipad.png)

   Viene selezionato un dispositivo con provisioning, iPad Air 2.

1. Seleziona **Prodotto** > **Pulisci**.
1. Seleziona **Prodotto** > **Genera**.

## Creare il programma di installazione per l’app AEM Forms {#build-the-installer-for-the-mobile-workspace-app}

È necessario archiviare il progetto Xcode per generare il file di installazione (file con estensione ipa) e un elenco di proprietà (file con estensione plist). Il file dell’elenco delle proprietà contiene informazioni di configurazione dell’app ospitata all’interno, ad esempio il nome e il percorso di hosting dell’app. Per ulteriori informazioni sul file dell&#39;elenco delle proprietà, vedere [Informazioni sui file di elenco delle proprietà delle informazioni](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html).

1. Connetti un’iPad con provisioning a un computer Mac. Per informazioni dettagliate sul provisioning di un iPad, consulta [Creazione e download di profili di provisioning di sviluppo](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)
1. Seleziona il dispositivo per il quale è stato eseguito il provisioning **AEM Forms** progetto.

   ![ipad-1](assets/ipad-1.png)

   Viene selezionato un dispositivo con provisioning, iPad Air 2.

1. Seleziona **Prodotto** > **Pulisci**.
1. Seleziona **Prodotto** > **Genera**.
1. Seleziona **Prodotto** > **Archivia**.
1. In Organizer - Archives, seleziona l’archivio più recente del progetto e fai clic su **Distribuisci**.
1. Seleziona **Salva per implementazione Enterprise o Ad Hoc** come metodo di distribuzione e fare clic su **Successivo**.
1. Seleziona la scheda appropriata **Identità firma codice** e fai clic su **Successivo**. Clic **Consenti** per applicare la firma.
1. Immetti il nome dell’app e seleziona **Salva per distribuzione Enterprise**.
1. Fornisci **URL applicazione** per l’app. Ad esempio, per ospitare l’app su un server CRX, specifica l’URL `https://[LC_host]:'port'/lc/content/distribution/mobileworkspace/APP_NAME.ipa`.
1. In **Titolo** , specifica AEM Forms.
1. Clic **Salva** e chiudere Xcode.

   Un file di installazione, `AEM Forms.ipa`, e file di elenco delle proprietà, `AEM Forms-info.plist`, vengono create nella posizione specificata.

1. Apri `AEM Forms-info.plist` in un editor.
1. Sostituisci tutti gli spazi nell&#39;URL del file .ipa con %20.
1. Salva e chiudi `AEM Forms-info.plist` file.
