---
title: Distribuisci  app AEM Forms
seo-title: Distribuisci  app AEM Forms
description: Utilizzate Mobile Device Management (MDM) per la distribuzione su larga scala di app sui dispositivi mobili.
seo-description: Utilizzate Mobile Device Management (MDM) per la distribuzione su larga scala di app sui dispositivi mobili.
uuid: 8a2ce42b-5e9b-42c1-a945-c069f6152f6e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 5756cb52-dd47-4277-981c-fd0af9a20638
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---


# Distribuisci  app AEM Forms {#distribute-aem-forms-app}

Mobile Device Management (MDM) consente la distribuzione su larga scala delle app sui dispositivi mobili.

>[!NOTE]
>
>Questa distribuzione è applicabile solo per i dispositivi iOS e Android.

## Caratteristiche principali generalmente fornite dalle soluzioni MDM: {#main-features-generally-provided-by-mdm-solutions}

* Abilitare l&#39;iscrizione ai dispositivi nell&#39;ambiente aziendale
* Consenti configurazione e aggiornamento delle impostazioni del dispositivo
* Applica la conformità alla sicurezza.
* Protezione dell&#39;accesso mobile alle risorse aziendali

Una soluzione MDM insieme a Mobile Application Management consente di gestire le app interne, pubbliche e acquistate sui dispositivi mobili dell&#39;azienda.

L&#39;amministratore MDM può caricare sia file ipa che apk nel server MDM e controllare gli utenti che possono accedere ai file ipa o apk. L&#39;amministratore può anche controllare l&#39;impostazione del profilo corrispondente a ciascuna applicazione.

## Impostazioni di profilo che interessano l&#39;app  AEM Forms {#profile-settings-affecting-the-aem-forms-app-br}

Le seguenti impostazioni di profilo sul dispositivo influiranno sul funzionamento dell&#39;app AEM Forms  sul dispositivo:

* **Consenti utilizzo della** videocamera nella sezione  **Funzionalità** dispositivo

Se si disabilita **Consenti l&#39;uso della fotocamera**, la funzionalità della fotocamera dell&#39; [annotazione foto](/help/forms/using/add-attachments.md) non funzionerà. È necessario abilitare questa opzione per utilizzare la fotocamera nell&#39;app.

* **Richiedi passcode sul** dispositivo nella sezione Criteri passcode

Per abilitare la crittografia **dei dati dell&#39;applicazione**, si consiglia di abilitare la **passcode** sul dispositivo. Se passcode non è impostato sul dispositivo, i dati dell&#39;applicazione memorizzati sul dispositivo non sono crittografati.
