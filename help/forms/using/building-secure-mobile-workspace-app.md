---
title: Creazione di un'app  AEM Forms protetta per iOS
seo-title: Creazione di un'app  AEM Forms protetta per iOS
description: Passaggi per creare un'app AEM Forms  protetta.
seo-description: Passaggi per creare un'app AEM Forms  protetta.
uuid: 6c4b160f-4d0c-4976-9609-9196795b6c8e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 90cd8ba5-4f47-4074-bc54-6a7bb8afe256
translation-type: tm+mt
source-git-commit: 49da3dbe590f70b98185a6bc330db6077dc864c0
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---


# Creazione di un&#39;app AEM Forms  protetta per iOS {#building-a-secure-aem-forms-app-for-ios}

È necessario archiviare il progetto Xcode per  app AEM Forms per creare il programma di installazione (un file .ipa) e un file elenco di proprietà (un file .plist). Il file dell&#39;elenco delle proprietà contiene le informazioni di configurazione dell&#39;app in hosting, ad esempio il nome e il percorso di hosting dell&#39;app. Per ulteriori informazioni sul file dell&#39;elenco delle proprietà, vedere [Informazioni sui file dell&#39;elenco delle proprietà](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html).

1. Accedete al seguente sito Web:

   [https://developer.apple.com/account/ios/identifier/bundle](https://developer.apple.com/account/ios/identifier/bundle)

1. Create un ID app. Per i passaggi dettagliati per creare un ID app, consultate [Creazione e configurazione di ID app](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html).
1. Per configurare l&#39;identificatore pacchetto per l&#39;applicazione iOS per la tua app, fai clic su **[!UICONTROL Configura ID app]**.
1. Nella parte inferiore della pagina Web, selezionare **[!UICONTROL Abilita per la protezione dei dati]**. Specificare le opzioni di protezione dei dati.

   Fare clic su **[!UICONTROL Fine]**.

1. Passa a Provisioning->Distribuzione e crea un nuovo profilo utilizzando l&#39;ID app configurato nel passaggio 3.
1. Scaricate e aggiungete il profilo di provisioning a Xcode e iPad.
1. Accedete al computer Mac in cui è installato e configurato Xcode e l’SDK per iOS.
1. Apri il progetto `AEM Forms.xcodeproj` in Xcode.
1. Fare clic su **[!UICONTROL AEM Forms]**, in **[!UICONTROL TARGETS]** selezionare **[!UICONTROL AEM Forms]**. Selezionate la scheda **[!UICONTROL Impostazioni build]**, individuate la sezione **[!UICONTROL Adesione firma codice]** e, nel menu a discesa Adesione, selezionate l&#39;opzione **[!UICONTROL LC Enterprise]**.
1. Individuate e aprite il file `LC Enterprise.entitlements` in Xcode per la modifica. In **XCode entitlement**, aggiungete la stessa coppia chiave-valore presente nel profilo di provisioning.
1. Nella scheda **[!UICONTROL Impostazioni build]** fare clic su **[!UICONTROL All]**, quindi fare clic su **[!UICONTROL Combinato]**.
1. Dall&#39;elenco **[!UICONTROL Impostazioni]**, espandere **[!UICONTROL Firma codice]**.
1. Per **[!UICONTROL Identità di firma del codice]**, selezionare la firma appropriata. Assicurarsi che la stessa firma sia selezionata per **[!UICONTROL Debug]**, **[!UICONTROL Release]** e **[!UICONTROL Qualsiasi SDK iOS]**.
1. In **[!UICONTROL PROJECT]**, selezionare **[!UICONTROL AEM Forms]** e assicurarsi che la firma appropriata sia selezionata per **[!UICONTROL Identità di firma del codice]**, **[!UICONTROL Debug]**, **[!UICONTROL Rilascio]** e **[!UICONTROL Qualsiasi SDK iOS]**.
1. Creare e distribuire  app AEM Forms. Per istruzioni dettagliate sulla creazione e distribuzione  app AEM Forms, consultate [Creare il programma di installazione per  app AEM Forms](setup-xcode-project-build-installer.md#build-the-installer-for-the-mobile-workspace-app).
