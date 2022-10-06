---
title: Distribuire l’app AEM Forms
seo-title: Distribute AEM Forms app
description: Utilizza Mobile Device Management (MDM) per la distribuzione su larga scala di app su dispositivi mobili.
seo-description: Use Mobile Device Management (MDM) for the large-scale deployment of apps on mobile devices.
uuid: 8a2ce42b-5e9b-42c1-a945-c069f6152f6e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 5756cb52-dd47-4277-981c-fd0af9a20638
exl-id: 375cfa95-ac6f-44c4-a736-f5dd55d24195
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# Distribuire l’app AEM Forms {#distribute-aem-forms-app}

Mobile Device Management (MDM) consente la distribuzione su larga scala di app su dispositivi mobili.

>[!NOTE]
>
>Questa distribuzione è applicabile solo per i dispositivi iOS e Android.

## Caratteristiche principali generalmente fornite dalle soluzioni MDM: {#main-features-generally-provided-by-mdm-solutions}

* Abilitare la registrazione dei dispositivi nell&#39;ambiente aziendale
* Consenti configurazione e aggiornamento delle impostazioni del dispositivo
* Applica la conformità in materia di sicurezza.
* Accesso mobile sicuro alle risorse aziendali

Una soluzione MDM, insieme a Mobile Application Management, consente di gestire app interne, pubbliche e acquistate sui dispositivi mobili della tua azienda.

L’amministratore MDM può caricare sia file ipa che apk sul server MDM e controllare gli utenti che possono accedere ai file ipa o apk. L’amministratore può inoltre controllare l’impostazione del profilo corrispondente a ciascuna applicazione.

## Impostazioni del profilo che interessano l’app AEM Forms {#profile-settings-affecting-the-aem-forms-app-br}

Le seguenti impostazioni del profilo sul tuo dispositivo influiranno sul funzionamento dell’app AEM Forms sul tuo dispositivo:

* **Consenti uso della fotocamera** in **Funzionalità del dispositivo** sezione

Se si disattiva **Consenti uso della fotocamera**, la funzione della telecamera [Annotazione foto](/help/forms/using/add-attachments.md) non funzionerà. Abilita questa opzione per usare la fotocamera nell’app.

* **Richiedi passcode sul dispositivo** nella sezione Criteri passcode

Per abilitare **crittografia dei dati delle applicazioni**, si consiglia di abilitare **passcode** sul dispositivo. Se il passcode non è impostato sul dispositivo, i dati dell&#39;applicazione memorizzati sul dispositivo non sono crittografati.
