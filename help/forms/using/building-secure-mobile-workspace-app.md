---
title: Creazione di un’app AEM Forms sicura per iOS
seo-title: Building a secure AEM Forms app for iOS
description: Passaggi per creare un’app AEM Forms sicura.
seo-description: Steps to build a secure AEM Forms app.
uuid: 6c4b160f-4d0c-4976-9609-9196795b6c8e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 90cd8ba5-4f47-4074-bc54-6a7bb8afe256
exl-id: 12cc2027-ae94-40c3-a7d1-553469426114
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# Creazione di un’app AEM Forms sicura per iOS {#building-a-secure-aem-forms-app-for-ios}

Devi archiviare il progetto Xcode per l’app AEM Forms per creare il file di installazione (un file .ipa) e un file di elenco delle proprietà (un file .plist). Il file di elenco delle proprietà contiene informazioni di configurazione dell’app in hosting, ad esempio il nome e il percorso di hosting dell’app. Per ulteriori informazioni sul file dell&#39;elenco delle proprietà, vedere [Informazioni sui file di elenco delle proprietà](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html).

1. Accedi al seguente sito web:

   [https://developer.apple.com/account/ios/identifier/bundle](https://developer.apple.com/account/ios/identifier/bundle)

1. Crea un App ID. Per i passaggi dettagliati per la creazione di un ID app, vedi [Creazione e configurazione degli ID app](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html).
1. Per configurare l&#39;identificatore del bundle per l&#39;applicazione iOS per la tua app, fai clic su **[!UICONTROL Configurare l’ID app]**.
1. Nella parte inferiore della pagina web, seleziona **[!UICONTROL Abilita per la protezione dei dati]**. Specifica le opzioni di protezione dei dati.

   Fai clic su **[!UICONTROL Fine]**.

1. Passa a Provisioning->Distribuzione e crea un nuovo profilo utilizzando l&#39;App ID configurato nel passaggio 3.
1. Scarica e aggiungi il profilo di provisioning a Xcode e iPad.
1. Accedi al computer Mac con Xcode e iOS SDK installato e configurato.
1. Apri `AEM Forms.xcodeproj` progetto in Xcode.
1. Fai clic su **[!UICONTROL AEM Forms]**, **[!UICONTROL TARGET]**, seleziona **[!UICONTROL AEM Forms]**. Seleziona la **[!UICONTROL Impostazioni build]** , individua la **[!UICONTROL Diritto di firma del codice]** e nel menu a discesa Autorizzazioni , seleziona la **[!UICONTROL LC Enterprise]** opzione .
1. Individua e apri la `LC Enterprise.entitlements` in Xcode per la modifica. Sotto la **Adeguamenti XCode**, aggiungi la stessa coppia chiave-valore presente nel profilo di provisioning.
1. In **[!UICONTROL Impostazioni build]** scheda , fai clic su **[!UICONTROL Tutto]** quindi fai clic su **[!UICONTROL Combinato]**.
1. Da **[!UICONTROL Impostazioni]** elenco, espandi **[!UICONTROL Firma del codice]**.
1. Per **[!UICONTROL Identità di firma del codice]**, selezionare la firma appropriata. Verificare che sia selezionata la stessa firma per **[!UICONTROL Debug]**, **[!UICONTROL Versione]** e **[!UICONTROL Qualsiasi SDK iOS]**.
1. Sotto **[!UICONTROL PROGETTO]**, seleziona **[!UICONTROL AEM Forms]** e assicurarsi che la firma appropriata sia selezionata per **[!UICONTROL Identità di firma del codice]**, **[!UICONTROL Debug]**, **[!UICONTROL Versione]** e **[!UICONTROL Qualsiasi SDK iOS]**.
1. Crea e distribuisci app AEM Forms. Per istruzioni dettagliate su come creare e distribuire l’app AEM Forms, vedi [Creare il programma di installazione per l’app AEM Forms](setup-xcode-project-build-installer.md#build-the-installer-for-the-mobile-workspace-app).
