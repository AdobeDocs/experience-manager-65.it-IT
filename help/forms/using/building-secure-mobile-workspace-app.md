---
title: Creazione di un’app AEM Forms sicura per iOS
description: Scopri come creare un’app AEM Forms sicura per iOS archiviando il progetto Xcode. In questo modo vengono creati il file di installazione (file con estensione ipa) e l'elenco delle proprietà (file con estensione plist).
uuid: 6c4b160f-4d0c-4976-9609-9196795b6c8e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 90cd8ba5-4f47-4074-bc54-6a7bb8afe256
exl-id: 12cc2027-ae94-40c3-a7d1-553469426114
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---

# Creazione di un’app AEM Forms sicura per iOS {#building-a-secure-aem-forms-app-for-ios}

Devi archiviare il progetto Xcode per l’app AEM Forms per creare il file di installazione (un file .ipa) e l’elenco delle proprietà (un file .plist). Il file dell’elenco delle proprietà contiene informazioni di configurazione dell’app ospitata all’interno, ad esempio il nome e il percorso di hosting dell’app. Per ulteriori informazioni sul file dell&#39;elenco delle proprietà, vedere [Informazioni sui file di elenco delle proprietà delle informazioni](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html).

1. Accedi al seguente sito Web:

   [https://developer.apple.com/account/ios/identifier/bundle](https://developer.apple.com/account/ios/identifier/bundle)

1. Crea un App ID. Per i passaggi dettagliati della creazione di un App ID, vedi [Creazione e configurazione degli ID app](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html).
1. Per configurare l’identificatore del bundle per l’applicazione iOS per la tua app, fai clic su **[!UICONTROL Configurare l’ID app]**.
1. Nella parte inferiore della pagina Web, seleziona **[!UICONTROL Attiva per protezione dei dati]**. Specificare le opzioni di protezione dei dati.

   Clic **[!UICONTROL Fine]**.

1. Passa a Provisioning>Distribuzione e crea un nuovo profilo utilizzando l’ID app configurato nel passaggio 3.
1. Scarica e aggiungi il profilo di provisioning a Xcode e iPad.
1. Accedi al tuo computer Mac con Xcode e iOS SDK installato e configurato.
1. Apri `AEM Forms.xcodeproj` progetto in Xcode.
1. Clic **[!UICONTROL AEM Forms]**, in **[!UICONTROL TARGET]**, seleziona **[!UICONTROL AEM Forms]**. Seleziona la **[!UICONTROL Impostazioni build]** , individua la scheda **[!UICONTROL Diritto alla firma del codice]** e nel menu a discesa Diritti, seleziona la **[!UICONTROL LC Enterprise]** opzione.
1. Individuare e aprire `LC Enterprise.entitlements` Xcode per la modifica. Sotto **Diritti Xcode**, aggiungi la stessa coppia chiave-valore presente nel profilo di provisioning.
1. In **[!UICONTROL Impostazioni build]** , fare clic su **[!UICONTROL Tutti]** e quindi fare clic su **[!UICONTROL Combinato]**.
1. Dalla sezione **[!UICONTROL Impostazioni]** list, expand **[!UICONTROL Firma codice]**.
1. Per **[!UICONTROL Identità firma codice]**, selezionare la firma appropriata. Assicurati che la stessa firma sia selezionata per **[!UICONTROL Debug]**, **[!UICONTROL Versione]**, e **[!UICONTROL Qualsiasi SDK di iOS]**.
1. Sotto **[!UICONTROL PROGETTO]**, seleziona **[!UICONTROL AEM Forms]** e accertarsi che sia selezionata la firma appropriata per **[!UICONTROL Identità firma codice]**, **[!UICONTROL Debug]**, **[!UICONTROL Versione]** e **[!UICONTROL Qualsiasi SDK di iOS]**.
1. Crea e distribuisci l’app AEM Forms. Per istruzioni dettagliate su come creare e distribuire l’app AEM Forms, consulta [Creare il programma di installazione per l’app AEM Forms](setup-xcode-project-build-installer.md#build-the-installer-for-the-mobile-workspace-app).
