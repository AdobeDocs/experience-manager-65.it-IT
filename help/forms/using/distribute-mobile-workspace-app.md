---
title: Distribuire l’app AEM Forms
description: Utilizza Mobile Device Management (MDM) per l’implementazione su larga scala di app su dispositivi mobili.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 375cfa95-ac6f-44c4-a736-f5dd55d24195
source-git-commit: 474a726058b141985f52a0faec6161a34be1e9dc
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# Distribuire l’app AEM Forms {#distribute-aem-forms-app}

Mobile Device Management (MDM) consente la distribuzione su larga scala di app su dispositivi mobili.

>[!NOTE]
>
>Questa distribuzione è applicabile solo ai dispositivi iOS e Android™.

## Funzioni principali fornite dalle soluzioni MDM: {#main-features-generally-provided-by-mdm-solutions}

* Abilitare la registrazione dei dispositivi nell&#39;ambiente aziendale
* Consenti la configurazione e l&#39;aggiornamento delle impostazioni del dispositivo
* Applicazione della conformità in materia di sicurezza.
* Accesso mobile sicuro alle risorse aziendali

Una soluzione MDM insieme alla gestione delle applicazioni mobili, consente di gestire le app interne, pubbliche e acquistate tra i dispositivi mobili dell’azienda.

L&#39;amministratore MDM può caricare sia i file ipa che i file apk sul server MDM e controllare gli utenti che possono accedere ai file ipa o apk. L’amministratore può anche controllare le impostazioni di profilo corrispondenti a ciascuna applicazione.

## Impostazioni del profilo che interessano l’app AEM Forms {#profile-settings-affecting-the-aem-forms-app-br}

Le seguenti impostazioni di profilo sul dispositivo influiscono sul funzionamento dell’app AEM Forms sul dispositivo:

* **Consenti l&#39;uso della fotocamera** nel **Funzionalità del dispositivo** sezione

Se disattivi **Consenti l&#39;uso della fotocamera**, la funzionalità della fotocamera del [Annotazione fotografia](/help/forms/using/add-attachments.md) non funziona. Abilita questa opzione per utilizzare la fotocamera nell’app.

* **Richiedi passcode sul dispositivo** nella sezione Criteri passcode

Per abilitare **crittografia dei dati dell&#39;applicazione**, si consiglia di abilitare **passcode** sul dispositivo. Se il passcode non è impostato sul dispositivo, i dati dell&#39;applicazione memorizzati sul dispositivo non vengono crittografati.
