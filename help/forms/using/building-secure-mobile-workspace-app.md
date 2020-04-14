---
title: Creazione di un'app AEM Forms protetta per iOS
seo-title: Creazione di un'app AEM Forms protetta per iOS
description: Passaggi per creare un'app AEM Forms protetta.
seo-description: Passaggi per creare un'app AEM Forms protetta.
uuid: 6c4b160f-4d0c-4976-9609-9196795b6c8e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 90cd8ba5-4f47-4074-bc54-6a7bb8afe256
translation-type: tm+mt
source-git-commit: 49da3dbe590f70b98185a6bc330db6077dc864c0

---


# Creazione di un&#39;app AEM Forms protetta per iOS {#building-a-secure-aem-forms-app-for-ios}

È necessario archiviare il progetto Xcode per l&#39;app AEM Forms per creare il programma di installazione (un file .ipa) e un file elenco di proprietà (un file .plist). Il file dell&#39;elenco delle proprietà contiene le informazioni di configurazione dell&#39;app in hosting, ad esempio il nome e il percorso di hosting dell&#39;app. Per ulteriori informazioni sul file dell&#39;elenco delle proprietà, vedere [Informazioni sui file](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html)dell&#39;elenco delle proprietà.

1. Accedete al seguente sito Web:

   [https://developer.apple.com/account/ios/identifier/bundle](https://developer.apple.com/account/ios/identifier/bundle)

1. Create un ID app. Per i passaggi dettagliati per creare un ID app, consultate [Creazione e configurazione di ID](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html)app.
1. Per configurare l&#39;identificatore pacchetto per l&#39;applicazione iOS per la vostra app, fate clic su **[!UICONTROL Configura ID]** app.
1. Nella parte inferiore della pagina Web, selezionare **[!UICONTROL Abilita per protezione]** dati. Specificare le opzioni di protezione dei dati.

   Fate clic su **[!UICONTROL Fine]**.

1. Passa a Provisioning->Distribuzione e crea un nuovo profilo utilizzando l&#39;ID app configurato nel passaggio 3.
1. Scaricate e aggiungete il profilo di provisioning a Xcode e iPad.
1. Accedete al computer Mac in cui è installato e configurato Xcode e l’SDK per iOS.
1. Apri il `AEM Forms.xcodeproj` progetto in Xcode.
1. Fate clic su **[!UICONTROL AEM Forms]**, in **[!UICONTROL TARGET]**, selezionate **[!UICONTROL AEM Forms]**. Selezionate la scheda Impostazioni **** build, individuate la sezione Adesione **[!UICONTROL firma]** codice e, nel menu a discesa Adesione, selezionate l&#39;opzione **[!UICONTROL LC Enterprise]** .
1. Individuate e aprite il `LC Enterprise.entitlements` file in Xcode per la modifica. In **XCode**, aggiungete la stessa coppia chiave-valore presente nel profilo di provisioning.
1. Nella scheda **[!UICONTROL Impostazioni]** build, fai clic su **[!UICONTROL Tutto]** , quindi su **[!UICONTROL Combinato]**.
1. Dall&#39;elenco **[!UICONTROL Impostazioni]** , espandere Firma **[!UICONTROL codice]**.
1. Per Identità **[!UICONTROL firma]** codice, selezionare la firma appropriata. Verifica che la stessa firma sia selezionata per **[!UICONTROL Debug]**, **[!UICONTROL Release]** e **[!UICONTROL Qualsiasi SDK]** iOS.
1. In **[!UICONTROL PROJECT]**, seleziona **[!UICONTROL AEM Forms]** e accertati che sia selezionata la firma appropriata per Identità **[!UICONTROL di firma del]** codice, **[!UICONTROL Debug]**, **[!UICONTROL Rilascio]** **** e Qualsiasi SDK iOS.
1. Creazione e distribuzione di app AEM Forms. Per istruzioni dettagliate sulla creazione e distribuzione di app AEM Forms, consultate [Creazione del programma di installazione per l&#39;app](setup-xcode-project-build-installer.md#build-the-installer-for-the-mobile-workspace-app)AEM Forms.
