---
title: Creazione di un’app AEM Forms sicura per iOS
description: Scopri come creare un’app AEM Forms sicura per iOS archiviando il progetto Xcode. In questo modo vengono creati il file di installazione (file con estensione ipa) e l'elenco delle proprietà (file con estensione plist).
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 12cc2027-ae94-40c3-a7d1-553469426114
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---

# Creazione di un’app AEM Forms sicura per iOS {#building-a-secure-aem-forms-app-for-ios}

Devi archiviare il progetto Xcode per l’app AEM Forms per creare il file di installazione (un file .ipa) e l’elenco delle proprietà (un file .plist). Il file dell’elenco delle proprietà contiene informazioni di configurazione dell’app ospitata all’interno, ad esempio il nome e il percorso di hosting dell’app. Per ulteriori informazioni sul file dell&#39;elenco proprietà, vedere [Informazioni sui file dell&#39;elenco proprietà](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html).

1. Accedi al seguente sito Web:

   [https://developer.apple.com/account/ios/identifier/bundle](https://developer.apple.com/account/ios/identifier/bundle)

1. Crea un App ID. Per i passaggi dettagliati per la creazione di un ID app, vedi [Creazione e configurazione degli ID app](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html).
1. Per configurare l&#39;identificatore del bundle per l&#39;applicazione iOS per l&#39;app, fare clic su **[!UICONTROL Configura ID app]**.
1. Nella parte inferiore della pagina Web, selezionare **[!UICONTROL Abilita per la protezione dei dati]**. Specificare le opzioni di protezione dei dati.

   Fai clic su **[!UICONTROL Fine]**.

1. Passa a Provisioning>Distribuzione e crea un nuovo profilo utilizzando l’ID app configurato nel passaggio 3.
1. Scarica e aggiungi il profilo di provisioning a Xcode e iPad.
1. Accedi al tuo computer Mac con Xcode e iOS SDK installato e configurato.
1. Apri il progetto `AEM Forms.xcodeproj` in Xcode.
1. Fai clic su **[!UICONTROL AEM Forms]**, in **[!UICONTROL TARGET]**, seleziona **[!UICONTROL AEM Forms]**. Seleziona la scheda **[!UICONTROL Impostazioni build]**, individua la sezione **[!UICONTROL Diritto alla firma del codice]** e, nel menu a discesa Diritti, seleziona l&#39;opzione **[!UICONTROL LC Enterprise]**.
1. Individua e apri il file `LC Enterprise.entitlements` nel codice Xcode per la modifica. In **Diritti Xcode**, aggiungi la stessa coppia chiave-valore presente nel profilo di provisioning.
1. Nella scheda **[!UICONTROL Impostazioni build]**, fai clic su **[!UICONTROL Tutti]**, quindi su **[!UICONTROL Combinati]**.
1. Nell&#39;elenco **[!UICONTROL Impostazioni]** espandere **[!UICONTROL Firma codice]**.
1. Per **[!UICONTROL Identità firma codice]**, selezionare la firma appropriata. Assicurati che la stessa firma sia selezionata per **[!UICONTROL Debug]**, **[!UICONTROL Versione]** e **[!UICONTROL Qualsiasi SDK iOS]**.
1. In **[!UICONTROL PROGETTO]**, seleziona **[!UICONTROL AEM Forms]** e assicurati che sia selezionata la firma appropriata per **[!UICONTROL Identità firma codice]**, **[!UICONTROL Debug]**, **[!UICONTROL Versione]** e **[!UICONTROL Qualsiasi SDK iOS]**.
1. Crea e distribuisci l’app AEM Forms. Per istruzioni dettagliate su come generare e distribuire l&#39;app AEM Forms, vedi [Creare il programma di installazione per l&#39;app AEM Forms](setup-xcode-project-build-installer.md#build-the-installer-for-the-mobile-workspace-app).
