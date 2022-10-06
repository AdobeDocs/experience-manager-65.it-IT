---
title: Configurare il progetto Xcode e creare l'app iOS
seo-title: Set up the Xcode project and build the iOS app
description: Spiega come creare un’app AEM Forms standard per iOS.
seo-description: Explains how to build standard AEM Forms app for iOS.
uuid: 29779bbb-06b4-4ece-9f29-786afab59eaf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 88555db2-712f-4ef9-bf47-76c7ba83d964
docset: aem65
exl-id: 78ce6107-8821-47d6-86ab-7ab968945e7c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '813'
ht-degree: 6%

---

# Configurare il progetto Xcode e creare l&#39;app iOS{#set-up-the-xcode-project-and-build-the-ios-app}

AEM Forms fornisce il codice sorgente completo dell’app AEM Forms. La sorgente contiene tutti i componenti per creare un’app AEM Forms personalizzata. archivio del codice sorgente, `adobe-lc-mobileworkspace-src-<version>.zip` fa parte del `adobe-aemfd-forms-app-src-pkg-<version>.zip` pacchetto sulla distribuzione software.

Per ottenere la sorgente dell’app AEM Forms, esegui i seguenti passaggi:

1. Apri [Software Distribution](https://experience.adobe.com/downloads). Per accedere a Software Distribution è necessario disporre di un Adobe ID.
1. Tocca **[!UICONTROL Adobe Experience Manager]** che si trova nel menu di intestazione.
1. In **[!UICONTROL Filtri]** sezione:
   1. Seleziona **[!UICONTROL Forms]** dal **[!UICONTROL Soluzione]** elenco a discesa.
   2. Seleziona la versione e digita il pacchetto. È inoltre possibile utilizzare **[!UICONTROL Download di ricerca]** per filtrare i risultati.
1. Toccare il nome del pacchetto applicabile al sistema operativo in uso, selezionare **[!UICONTROL Accettare i termini dell&#39;EULA]**, e tocca **[!UICONTROL Scarica]**.
1. Apri [Gestione pacchetti](https://docs.adobe.com/content/help/it/experience-manager-65/administering/contentmanagement/package-manager.html) e fai clic su **[!UICONTROL Carica pacchetto]** per caricarlo.
1. Seleziona il pacchetto e fai clic su **[!UICONTROL Installa]**.

1. Per scaricare l&#39;archivio del codice sorgente, apri `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` nel browser.
Il pacchetto sorgente viene scaricato sul dispositivo.

L’immagine seguente visualizza il contenuto estratto del `adobe-lc-mobileworkspace-src-<version>.zip`.

![mws-content](assets/mws-content.png)

La tabella seguente descrive il contenuto `adobe-lc-mobileworkspace-src-[version]/ios` cartella.

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
   <td><p>Progetto Xcode per l’app AEM Forms</p> </td>
  </tr>
  <tr>
   <td><p><code>www</code></p> </td>
   <td><p>File HTML, CSS, immagini e JavaScript per il progetto dell’app AEM Forms</p> </td>
  </tr>
 </tbody>
</table>

Per informazioni dettagliate sulla firma del codice e sull&#39;aggiunta di dispositivi al portale di provisioning iOS, vedi [Configurazione, elaborazione e risoluzione dei problemi della firma del codice iOS](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html).

## Creare un’app AEM Forms standard {#set-up-the-xcode-project}

1. Esegui i seguenti passaggi per configurare un progetto in Xcode e fornire un’identità di firma:

   Accedi al computer Mac con Xcode e iOS SDK installato e configurato.

1. Copia il `adobe-lc-mobileworkspace-src-<version>.zip` dalla cartella dei download a `[User_Home]/Projects/`.
1. Estrai l’archivio nel `[User_Home]/Projects/[your-project]`directory.
1. Passa a ` [User_Home]/Projects/ `[progetto personale]`/adobe-lc-mobileworkspace-src-[version]/ios` directory.
1. Apri `AEM Forms.xcodeproj` progetto in Xcode.
1. Fai clic su **AEM Forms**, **TARGET**, seleziona **AEM Forms**. Seleziona la **Impostazioni build** , individua la **Diritto di firma del codice** e nei campi Debug e Rilascio eseguire una delle operazioni seguenti:

   * Lascia i campi non specificati per creare un’app Workspace standard
   * Specifica i campi da specificare in [Creazione di un’app AEM Forms sicura per iOS](/help/forms/using/building-secure-mobile-workspace-app.md) per creare un’app AEM Forms sicura.

1. In **Impostazioni build** scheda , fai clic su **Tutto** quindi fai clic su **Combinato**.
1. Da **Impostazioni** elenco, espandi **Firma del codice**.
1. Per **Identità di firma del codice**, selezionare la firma appropriata. Per informazioni dettagliate sulla creazione di nuove firme, vedere [Creazione e download di profili di provisioning dello sviluppo](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html).
1. Verificare che sia selezionata la stessa firma per **Debug**, **Versione** e **Qualsiasi SDK iOS**.
1. Sostituisci il seguente codice nel `AEM Forms-info.plist` file:

   ```xml
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSAllowsArbitraryLoads</key>
   <true/>
   </dict>
   ```

   con quanto segue durante la sostituzione di `yourserver.com` con un nome host appropriato per il server.

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
   >Questo passaggio è necessario solo se l’app AEM Forms deve connettersi a un server che non soddisfa i requisiti di App Transport Security.

1. Sotto **PROGETTO**, seleziona **AEM Forms** e assicurarsi che la firma appropriata sia selezionata per **Identità di firma del codice**, **Debug**, **Versione** e **Qualsiasi SDK iOS**.
1. Collega un iPad fornito a un computer Mac.
1. Seleziona il dispositivo di cui è stato effettuato il provisioning per il **AEM Forms** progetto.

   ![ipad](assets/ipad.png)

   È selezionato un dispositivo predisposto, iPad Air 2.

1. Seleziona **Prodotto** > **Pulisci**.
1. Seleziona **Prodotto** > **Crea**.

## Genera il programma di installazione per l’app AEM Forms {#build-the-installer-for-the-mobile-workspace-app}

Devi archiviare il progetto Xcode per creare il file di installazione (un file .ipa) e un file di elenco delle proprietà (un file .plist). Il file di elenco delle proprietà contiene informazioni di configurazione dell’app in hosting, ad esempio il nome e il percorso di hosting dell’app. Per ulteriori informazioni sul file dell&#39;elenco delle proprietà, vedere [Informazioni sui file di elenco delle proprietà](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html).

1. Collega un iPad fornito a un computer Mac. Per informazioni dettagliate sul provisioning di un iPad, consulta [Creazione e download di profili di provisioning dello sviluppo](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)
1. Seleziona il dispositivo di cui è stato effettuato il provisioning per il **AEM Forms** progetto.

   ![ipad-1](assets/ipad-1.png)

   È selezionato un dispositivo predisposto, iPad Air 2.

1. Seleziona **Prodotto** > **Pulisci**.
1. Seleziona **Prodotto** > **Crea**.
1. Seleziona **Prodotto** > **Archivia**.
1. In Organizer - Archivi, seleziona l’archivio più recente del progetto e fai clic su **Distribuisci**.
1. Seleziona **Salva per implementazione Enterprise o Ad Hoc** come metodo di distribuzione e fai clic su **Successivo**.
1. Selezionare il **Identità di firma del codice** e fai clic su **Successivo**. Fai clic su **Consenti** per applicare la firma.
1. Immetti il nome dell&#39;app e seleziona **Salva per distribuzione Enterprise**.
1. Fornisci **URL applicazione** per l’app. Ad esempio, per ospitare l’app su un server CRX, specifica l’URL `https://[LC_host]:'port'/lc/content/distribution/mobileworkspace/APP_NAME.ipa`.
1. In **Titolo** Specifica AEM Forms.
1. Fai clic su **Salva** e chiudi Xcode.

   Un file di installazione, `AEM Forms.ipa`e file elenco proprietà, `AEM Forms-info.plist`, vengono creati nella posizione specificata.

1. Apri `AEM Forms-info.plist` in un editor.
1. Sostituisci tutti gli spazi nell&#39;URL del file .ipa con %20.
1. Salva e chiudi il `AEM Forms-info.plist` file.
