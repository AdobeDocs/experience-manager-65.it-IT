---
title: Configurare le impostazioni di blocco dell’account
description: Utilizza l’opzione Abilita blocco account per bloccare gli account utente dopo un numero specifico di errori di autenticazione consecutivi.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: eb8c748d-51d9-4684-97c5-e982ad84ba9f
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
source-wordcount: '210'
ht-degree: 100%
---
# Configurare le impostazioni di blocco dell’account {#configure-account-locking-settings}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Quando aggiungi un dominio, specifica se abilitare il blocco dell’account. Quando l’opzione Abilita blocco account è selezionata, gli account utente vengono bloccati dopo un numero specificato di errori di autenticazione consecutivi. Dopo un periodo di tempo specificato, l’utente può tentare di eseguire nuovamente l’autenticazione. Questa funzione impedisce agli utenti di provare diverse combinazioni di credenziali per accedere al sistema.

Utilizza le impostazioni nella pagina Gestione dominio per specificare il numero massimo di errori di autenticazione e il periodo di tempo di blocco degli account. Queste impostazioni si applicano a tutti i domini in cui è abilitato il blocco account.

1. Nella console di amministrazione, fai clic su **[!UICONTROL Impostazioni > Gestione utente > Gestione dominio]**.
1. Nella casella Numero massimo di errori di autenticazione consecutivi immetti il numero massimo di tentativi di accesso non riusciti di un utente prima che l’account venga bloccato. Il valore predefinito è 20.
1. Nella casella Sblocca account dopo (minuti) immetti il numero di minuti di blocco dell’account utente. Dopo il numero di minuti specificato, l’utente può tentare di accedere di nuovo. Il valore predefinito è 30.
1. Fai clic su **[!UICONTROL Salva]**.
