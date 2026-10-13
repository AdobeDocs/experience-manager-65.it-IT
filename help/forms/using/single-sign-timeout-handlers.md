---
title: Gestori del Single Sign On e del timeout
description: Come impostare il valore di timeout della sessione per l’area di lavoro di AEM Forms.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 4f824d80-f3f8-4010-9583-5a9ab1151a7b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 6%
---
# Gestori del Single Sign On e del timeout {#single-sign-on-and-timeout-handlers}

L’area di lavoro di AEM Forms è abilitata per l’SSO. Se un utente ha effettuato l’accesso a un’applicazione AEM Forms come Forms Manager o l’interfaccia utente di PDF Generator e accede all’area di lavoro di AEM Forms nella stessa sessione del browser, l’utente ha effettuato l’accesso all’area di lavoro di AEM Forms e viceversa.

## Gestione del timeout del server nell’area di lavoro di AEM Forms {#handling-server-timeout-in-nbsp-aem-forms-workspace}

Il timeout della sessione di un utente può essere configurato nella console di amministrazione.

Per impostare il timeout, accedere a `https://'[server]:[port]'/adminui`, passare a **Impostazioni > Gestione utente > Configurazione > Configura attributi di sistema avanzati** e impostare le impostazioni desiderate.

In AEM Forms il timeout nell’area di lavoro viene gestito come:

* La durata della sessione per un utente è disponibile in risposta alla chiamata `initialize` che inizializza la sessione utente.
* Una finestra di dialogo a comparsa notifica all&#39;utente che la sessione sta per scadere, 15 secondi prima della scadenza.

In questa finestra di dialogo a comparsa:

* Fare clic su OK per terminare la sessione utente.
* Fare clic su Annulla per reinizializzare la sessione utente.

>[!NOTE]
>
>Se non viene eseguita alcuna azione, l’utente viene automaticamente disconnesso dall’area di lavoro di AEM Forms tre secondi prima della scadenza della sessione.
