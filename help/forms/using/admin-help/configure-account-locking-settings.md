---
title: Configurare le impostazioni di blocco degli account
seo-title: Configurare le impostazioni di blocco degli account
description: Utilizzate l'opzione Attiva blocco account per bloccare gli account utente dopo un numero specificato di errori di autenticazione consecutivi.
seo-description: Utilizzate l'opzione Attiva blocco account per bloccare gli account utente dopo un numero specificato di errori di autenticazione consecutivi.
uuid: 5ff3fb76-8b11-4818-9a75-40ed8e121da5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d4409c6b-f4ef-499c-8daa-e93a163ff8ab
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 4%

---


# Configurare le impostazioni di blocco dell&#39;account {#configure-account-locking-settings}

Quando aggiungete un dominio, specificate se abilitare il blocco dell&#39;account. Quando l&#39;opzione Attiva blocco account è selezionata, gli account utente vengono bloccati dopo un numero specificato di errori di autenticazione consecutivi. Dopo un periodo di tempo specificato, l&#39;utente può tentare di eseguire nuovamente l&#39;autenticazione. Questa funzione impedisce agli utenti di provare diverse combinazioni di credenziali per accedere al sistema.

Utilizzare le impostazioni della pagina Gestione dominio per specificare il numero massimo di errori di autenticazione e la durata del blocco degli account. Queste impostazioni si applicano a tutti i domini in cui è attivato il blocco dell&#39;account.

1. Nella console di amministrazione, fate clic su **[!UICONTROL Impostazioni > Gestione utente > Gestione dominio]**.
1. Nella casella Massimo errori di autenticazione consecutivi, immettere il numero di tentativi consecutivi in cui un utente può tentare di eseguire il login prima che il proprio account sia bloccato. Il valore predefinito è 20.
1. Nella casella Sblocca l’account dopo (minuti), inserite il numero di minuti in cui l’account utente è bloccato. Dopo il numero specificato di minuti, l&#39;utente può tentare di nuovo l&#39;accesso. Il valore predefinito è 30.
1. Fai clic su **[!UICONTROL Salva]**.

