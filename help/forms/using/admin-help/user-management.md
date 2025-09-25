---
title: Gestione utenti
description: La Gestione utenti consente di abilitare l’SSO tra i moduli di AEM Forms e le applicazioni protette da Netegrity SiteMinder utilizzando SAML. Questo documento fornisce ulteriori informazioni sulla gestione degli utenti.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1da1f6de-ac0d-4e0d-b8bb-956420e42699
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '484'
ht-degree: 100%

---

# Gestione utenti {#user-management}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Gestione utenti consente di abilitare il Single Sign-On (SSO) tra i moduli di AEM Forms e le applicazioni protette da Netegrity SiteMinder utilizzando il linguaggio SAML (Security Assertion Markup Language). Quando l’SSO viene implementato, le pagine di accesso dell’utente di AEM Forms non sono obbligatorie e non vengono visualizzate se l’utente è già autenticato tramite il portale aziendale.

Per informazioni sul miglioramento delle prestazioni di sincronizzazione di database e directory per DB2, vedere [Database IBM DB2: esecuzione di comandi per la manutenzione regolare](/help/forms/using/admin-help/ibm-db2-database-running-commands.md#ibm-db2-database-running-commands-for-regular-maintenance).

## Configurazione della gestione degli utenti per un server LDAP abilitato per SSL {#configuring-user-management-for-an-ssl-enabled-ldap-server}

Se disponi di un server LDAP abilitato per SSL, configura la gestione utenti per utilizzarlo. (Consulta [Configurare la gestione degli utenti per un server LDAP abilitato per SSL](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server).)

## Impostazione dei privilegi utente per l’utilizzo con Protezione documenti {#setting-user-privileges-for-use-with-document-security}

Crea un utente amministratore con i privilegi appropriati per la creazione di utenti e gruppi. Se l’ambiente AEM Forms include Protezione documenti, concedi a un utente l’accesso necessario per gestire gli utenti invitati e locali per i quali fungerà da amministratore. Assegna inoltre il ruolo Utente alla Console di amministrazione per far sì che l’utente vi possa accedere. Consulta [Creazione e configurazione dei gruppi](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).

Per visualizzare gli utenti e i gruppi nei domini selezionati durante le ricerche degli utenti dei criteri, un amministratore privilegiato o un amministratore di set di criteri deve selezionare e aggiungere i domini (creati in Gestione utente) all’elenco visibile di utenti e gruppi per ogni set di criteri creato.

L’elenco visibile di utenti e gruppi è visibile al coordinatore del set di criteri e viene utilizzato per limitare i domini che l’utente finale può sfogliare quando sceglie utenti o gruppi da aggiungere ai criteri. Se questa attività non viene eseguita, il coordinatore del set di criteri non troverà alcun utente o gruppo da aggiungere al criterio. Per ogni set di criteri può essere presente più di un coordinatore.

>[!NOTE]
>
>La creazione di domini deve essere eseguita prima di poter creare qualsiasi criterio.

### Impostare utenti e gruppi come visibili {#set-visible-users-and-groups}

Dopo aver installato e configurato l’ambiente AEM Forms con Protezione documenti, imposta tutti i domini appropriati in Gestione utente.

1. In Console di amministrazione, fai clic su Servizi > Protezione documenti > Criteri, quindi fai clic sulla scheda Set di criteri.
1. Seleziona Set di criteri globale, quindi fai clic sulla scheda Utenti e gruppi visibili.
1. Fai clic su Aggiungi domini e aggiungi i domini esistenti come richiesto.
1. Passa a Servizi > Protezione documenti > Configurazione > I miei criteri e fai clic sulla scheda Utenti e gruppi visibili.
1. Fai clic su Aggiungi domini e aggiungi i domini esistenti come richiesto.

## Limitazioni per gli utenti amministratori {#administrator-user-restrictions}

Per motivi di sicurezza gli utenti con determinati tipi di privilegi di amministratore non possono accedere alle pagine web degli utenti finali dell’area di lavoro. Poiché queste pagine web possono esistere all’esterno di un firewall, consentire attività a livello di amministrazione potrebbe rappresentare un rischio per la sicurezza. Solo gli utenti che dispongono dei privilegi di amministratore o di utente di Workspace possono accedere alle pagine web degli utenti finali.

>[!NOTE]
>
>Flex Workspace è obsoleto per la versione di AEM Forms.
