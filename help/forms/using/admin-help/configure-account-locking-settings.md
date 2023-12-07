---
title: Configurare le impostazioni di blocco account
description: Utilizzare l'opzione Abilita blocco account per bloccare gli account utente dopo un numero specificato di errori di autenticazione consecutivi.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: eb8c748d-51d9-4684-97c5-e982ad84ba9f
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 6%

---

# Configurare le impostazioni di blocco account {#configure-account-locking-settings}

Quando aggiungi un dominio, specifica se abilitare il blocco dell’account. Quando l&#39;opzione Abilita blocco account è selezionata, gli account utente vengono bloccati dopo un numero specificato di errori di autenticazione consecutivi. Dopo un periodo di tempo specificato, l’utente può tentare di eseguire nuovamente l’autenticazione. Questa funzione impedisce agli utenti di provare diverse combinazioni di credenziali per accedere al sistema.

Utilizzare le impostazioni nella pagina Gestione dominio per specificare il numero massimo di errori di autenticazione e il periodo di tempo di blocco degli account. Queste impostazioni si applicano a tutti i domini in cui è abilitato il blocco account.

1. Nella console di amministrazione, fai clic su **[!UICONTROL Impostazioni > Gestione utente > Gestione dominio]**.
1. Nella casella Numero massimo di errori di autenticazione consecutivi immettere il numero di tentativi di accesso non riusciti di un utente prima che l&#39;account venga bloccato. Il valore predefinito è 20.
1. Nella casella Sblocca account dopo (minuti) immettere il numero di minuti di blocco dell&#39;account utente. Dopo il numero di minuti specificato, l&#39;utente può tentare di accedere di nuovo. Il valore predefinito è 30.
1. Fai clic su **[!UICONTROL Salva]**.
