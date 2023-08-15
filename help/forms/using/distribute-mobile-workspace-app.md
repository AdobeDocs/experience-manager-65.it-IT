---
title: Distribuire l’app AEM Forms
seo-title: Distribute AEM Forms app
description: Utilizza Mobile Device Management (MDM) per l’implementazione su larga scala di app su dispositivi mobili.
seo-description: Use Mobile Device Management (MDM) for the large-scale deployment of apps on mobile devices.
uuid: 8a2ce42b-5e9b-42c1-a945-c069f6152f6e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 5756cb52-dd47-4277-981c-fd0af9a20638
exl-id: 375cfa95-ac6f-44c4-a736-f5dd55d24195
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# Distribuire l’app AEM Forms {#distribute-aem-forms-app}

Mobile Device Management (MDM) consente la distribuzione su larga scala di app su dispositivi mobili.

>[!NOTE]
>
>Questa distribuzione è applicabile solo ai dispositivi iOS e Android.

## Caratteristiche principali generalmente fornite dalle soluzioni MDM: {#main-features-generally-provided-by-mdm-solutions}

* Abilitare la registrazione dei dispositivi nell&#39;ambiente aziendale
* Consenti la configurazione e l&#39;aggiornamento delle impostazioni del dispositivo
* Applicazione della conformità in materia di sicurezza.
* Accesso mobile sicuro alle risorse aziendali

Una soluzione MDM insieme alla gestione delle applicazioni mobili, consente di gestire le app interne, pubbliche e acquistate tra i dispositivi mobili dell’azienda.

L&#39;amministratore MDM può caricare sia i file ipa che i file apk sul server MDM e controllare gli utenti che possono accedere ai file ipa o apk. L’amministratore può anche controllare l’impostazione del profilo corrispondente a ciascuna applicazione.

## Impostazioni del profilo che interessano l’app AEM Forms {#profile-settings-affecting-the-aem-forms-app-br}

Le seguenti impostazioni di profilo sul dispositivo influiranno sul funzionamento dell’app AEM Forms sul dispositivo:

* **Consenti l&#39;uso della fotocamera** nel **Funzionalità del dispositivo** sezione

Se disattivi **Consenti l&#39;uso della fotocamera**, la funzionalità della fotocamera del [Annotazione fotografia](/help/forms/using/add-attachments.md) non funzionerà. Devi abilitare questa opzione per usare la fotocamera nell’app.

* **Richiedi passcode sul dispositivo** nella sezione Criteri passcode

Per abilitare **crittografia dei dati dell&#39;applicazione**, si consiglia di abilitare **passcode** sul dispositivo. Se il passcode non è impostato sul dispositivo, i dati dell&#39;applicazione memorizzati sul dispositivo non vengono crittografati.
