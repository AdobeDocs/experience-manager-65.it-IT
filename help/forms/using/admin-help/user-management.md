---
title: User Management
seo-title: User Management
description: User Management consente di abilitare l'SSO tra moduli AEM e applicazioni protette da Netegrity SiteMinder utilizzando SAML. Questo documento fornisce ulteriori informazioni sulla gestione degli utenti.
seo-description: User Management allows you to enable SSO between AEM forms modules and Netegrity SiteMinder-protected applications by using SAML. This document provides more information about User Management.
uuid: f0c8331a-d995-483d-97b7-259df53b1a1a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 10e6177a-8228-4515-aba9-bbe59bede449
exl-id: 1da1f6de-ac0d-4e0d-b8bb-956420e42699
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# Gestione utente {#user-management}

User Management consente di abilitare l&#39;accesso single sign-on (SSO) tra moduli AEM e applicazioni protette da Netegrity SiteMinder utilizzando Security Assertion Markup Language (SAML). Quando l’SSO è implementato, le pagine di accesso utente dei moduli di AEM non sono necessarie e non vengono visualizzate se l’utente è già autenticato tramite il portale aziendale.

Per informazioni su come migliorare le prestazioni di sincronizzazione del database e delle directory per DB2, vedi [Database IBM DB2: Esecuzione di comandi per la manutenzione regolare](/help/forms/using/admin-help/ibm-db2-database-running-commands.md#ibm-db2-database-running-commands-for-regular-maintenance).

## Configurazione della gestione utente per un server LDAP abilitato per SSL {#configuring-user-management-for-an-ssl-enabled-ldap-server}

Se disponi di un server LDAP abilitato per SSL, configura Gestione utente per utilizzarlo. (Vedi [Configurare la gestione utente per un server LDAP abilitato per SSL](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server).)

## Impostazione dei privilegi utente per l&#39;utilizzo con Document Security {#setting-user-privileges-for-use-with-document-security}

Crea un utente amministratore con i privilegi appropriati per la creazione di utenti e gruppi. Se l’ambiente dei moduli AEM include Document Security, concedere il privilegio di gestire gli utenti invitati e locali a un utente che sarà l’amministratore per questi utenti. Assegna anche il ruolo utente della console di amministrazione per fornire all’utente l’accesso alla console di amministrazione. (Vedi [Creazione e configurazione di ruoli](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)

Per visualizzare gli utenti e i gruppi nei domini selezionati durante le ricerche degli utenti dei criteri, un amministratore privilegiato o un amministratore di set di criteri deve selezionare e aggiungere i domini (creati in Gestione utente) all&#39;elenco di utenti e gruppi visibili per ciascun set di criteri creato.

L&#39;elenco visibile di utenti e gruppi è visibile al coordinatore del set di criteri e viene utilizzato per limitare i domini che l&#39;utente finale può sfogliare quando sceglie utenti o gruppi da aggiungere ai criteri. Se questa attività non viene eseguita, il coordinatore del set di criteri non troverà utenti o gruppi da aggiungere al criterio. Può essere presente più di un coordinatore set di criteri per ogni set di criteri specificato.

>[!NOTE]
>
>È necessario creare i domini prima di creare qualsiasi criterio.

### Imposta utenti e gruppi visibili {#set-visible-users-and-groups}

Dopo aver installato e configurato l’ambiente AEM forms con Document Security, configura tutti i domini appropriati in Gestione utente.

1. Nella console di amministrazione, fare clic su Servizi > Sicurezza documenti> Criteri, quindi fare clic sulla scheda Set di criteri.
1. Seleziona Set di criteri globale, quindi fai clic sulla scheda Utenti e gruppi visibili .
1. Fai clic su Aggiungi domini e aggiungi i domini esistenti come richiesto.
1. Passa a Servizi > Protezione documento > Configurazione > Criteri personali e fai clic sulla scheda Utenti e gruppi visibili .
1. Fai clic su Aggiungi domini e aggiungi i domini esistenti come richiesto.

## Restrizioni per gli utenti amministratori {#administrator-user-restrictions}

Gli utenti con determinati tipi di privilegi di amministratore non possono accedere alle pagine web dell’utente finale di Workspace per motivi di sicurezza. Poiché queste pagine web possono esistere al di fuori di un firewall, l’autorizzazione delle attività a livello di amministrazione potrebbe comportare un rischio per la sicurezza. Solo gli utenti con i privilegi di amministratore di Workspace o utente di Workspace possono accedere alle pagine web dell’utente finale.

>[!NOTE]
>
>Flex Workspace è obsoleto per AEM versione dei moduli.
