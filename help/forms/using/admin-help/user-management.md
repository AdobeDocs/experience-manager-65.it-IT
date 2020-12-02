---
title: User Management
seo-title: Gestione utenti
description: Gestione utente consente di abilitare SSO tra moduli AEM e applicazioni protette da Netegrity SiteMinder utilizzando SAML. Questo documento fornisce ulteriori informazioni sulla gestione degli utenti.
seo-description: Gestione utente consente di abilitare SSO tra moduli AEM e applicazioni protette da Netegrity SiteMinder utilizzando SAML. Questo documento fornisce ulteriori informazioni sulla gestione degli utenti.
uuid: f0c8331a-d995-483d-97b7-259df53b1a1a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 10e6177a-8228-4515-aba9-bbe59bede449
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 1%

---


# User Management {#user-management}

Gestione utente consente di abilitare SSO (Single Sign-On) tra moduli AEM e applicazioni protette da Netegrity SiteMinder utilizzando SAML (Security Assertion Markup Language). Quando si implementa SSO, le pagine di login utente dei moduli AEM non sono obbligatorie e non vengono visualizzate se l&#39;utente è già autenticato tramite il portale aziendale.

Per informazioni su come migliorare le prestazioni di sincronizzazione di database e directory per DB2, vedere [database IBM DB2: Esecuzione di comandi per la manutenzione regolare](/help/forms/using/admin-help/ibm-db2-database-running-commands.md#ibm-db2-database-running-commands-for-regular-maintenance).

## Configurazione della gestione utente per un server LDAP abilitato per SSL {#configuring-user-management-for-an-ssl-enabled-ldap-server}

Se disponete di un server LDAP abilitato per SSL, configurate Gestione utente per utilizzarlo. Consultate [Configurare la gestione utente per un server LDAP abilitato per SSL](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server).

## Impostazione dei privilegi utente per l&#39;uso con Document Security {#setting-user-privileges-for-use-with-document-security}

Create un utente amministratore che disponga dei privilegi appropriati per la creazione di utenti e gruppi. Se l&#39;ambiente AEM moduli include Document Security, concedere il privilegio di gestire gli utenti invitati e locali a un utente che sarà l&#39;amministratore di tali utenti. Assegnate inoltre il ruolo utente della console di amministrazione per fornire all’utente l’accesso alla console di amministrazione. (Vedere [Creazione e configurazione di ruoli](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)

Per visualizzare gli utenti e i gruppi nei domini selezionati durante le ricerche degli utenti tramite criterio, un amministratore superiore o un amministratore di set di criteri deve selezionare e aggiungere i domini (creati in Gestione utente) all&#39;elenco di utenti e gruppi visibile per ciascun set di criteri creato.

L&#39;elenco di utenti e gruppi visibile è visibile al coordinatore del set di criteri e viene utilizzato per limitare i domini che l&#39;utente finale può esplorare quando sceglie utenti o gruppi da aggiungere ai criteri. Se questa attività non viene eseguita, il coordinatore del set di criteri non troverà utenti o gruppi da aggiungere al criterio. Per ciascun set di criteri può essere presente più di un coordinatore set di criteri.

>[!NOTE]
>
>È necessario creare i domini prima di poter creare qualsiasi criterio.

### Impostazione di utenti e gruppi visibili {#set-visible-users-and-groups}

Dopo aver installato e configurato l&#39;ambiente dei moduli AEM con Document Security, configurare tutti i domini appropriati in Gestione utente.

1. Nella console di amministrazione, fate clic su Servizi > Document Security > Criteri, quindi fate clic sulla scheda Set criteri.
1. Selezionate Set di criteri globale, quindi fate clic sulla scheda Utenti e gruppi visibili.
1. Fai clic su Aggiungi domini e aggiungi i domini esistenti come necessario.
1. Passa a Servizi > Protezione documento > Configurazione > Criteri personali e fai clic sulla scheda Utenti e gruppi visibili.
1. Fai clic su Aggiungi domini e aggiungi i domini esistenti come necessario.

## Limitazioni per gli utenti amministratori {#administrator-user-restrictions}

Gli utenti con determinati tipi di privilegi di amministratore non possono accedere alle pagine Web degli utenti finali di Workspace per motivi di sicurezza. Poiché queste pagine Web possono esistere all&#39;esterno di un firewall, l&#39;autorizzazione delle attività a livello di amministrazione potrebbe rappresentare un rischio per la sicurezza. Solo gli utenti che dispongono dei privilegi di amministratore Workspace o utente Workspace possono accedere alle pagine Web dell’utente finale.

>[!NOTE]
>
>Flex Workspace è obsoleto per AEM rilascio di moduli.

