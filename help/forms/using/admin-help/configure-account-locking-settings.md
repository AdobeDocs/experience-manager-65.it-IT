---
title: Configurare le impostazioni di blocco account
seo-title: Configure account-locking settings
description: Utilizzare l'opzione Abilita blocco account per bloccare gli account utente dopo un numero specificato di errori di autenticazione consecutivi.
seo-description: Use the Enable Account Locking option to lock user accounts after a specified number of consecutive authentication failures.
uuid: 5ff3fb76-8b11-4818-9a75-40ed8e121da5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d4409c6b-f4ef-499c-8daa-e93a163ff8ab
exl-id: eb8c748d-51d9-4684-97c5-e982ad84ba9f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 5%

---

# Configurare le impostazioni di blocco account {#configure-account-locking-settings}

Quando aggiungi un dominio, specifica se abilitare il blocco dell’account. Quando l&#39;opzione Abilita blocco account è selezionata, gli account utente vengono bloccati dopo un numero specificato di errori di autenticazione consecutivi. Dopo un periodo di tempo specificato, l’utente può tentare di eseguire nuovamente l’autenticazione. Questa funzione impedisce agli utenti di provare diverse combinazioni di credenziali per accedere al sistema.

Utilizzare le impostazioni nella pagina Gestione dominio per specificare il numero massimo di errori di autenticazione e il periodo di tempo di blocco degli account. Queste impostazioni si applicano a tutti i domini in cui è abilitato il blocco account.

1. Nella console di amministrazione, fai clic su **[!UICONTROL Impostazioni > Gestione utente > Gestione dominio]**.
1. Nella casella Numero massimo di errori di autenticazione consecutivi immettere il numero di tentativi di accesso non riusciti di un utente prima che l&#39;account venga bloccato. Il valore predefinito è 20.
1. Nella casella Sblocca account dopo (minuti) immettere il numero di minuti di blocco dell&#39;account utente. Dopo il numero di minuti specificato, l&#39;utente può tentare di accedere di nuovo. Il valore predefinito è 30.
1. Fai clic su **[!UICONTROL Salva]**.
