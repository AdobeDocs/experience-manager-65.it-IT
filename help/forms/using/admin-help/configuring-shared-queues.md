---
title: Configurazione delle code condivise
description: Le code condivise consentono di configurare e gestire in modo efficace le code utente. Scopri come configurare le code condivise.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 5f4467c1-0f3f-4dc6-9bd5-98259f327295
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 0%

---

# Configurazione delle code condivise{#configuring-shared-queues}

Le code condivise consentono di configurare e gestire in modo efficace le code utente. Una coda di utenti è costituita semplicemente da tutte le operazioni assegnate a un utente. Vedere [Elenchi attività](https://help.adobe.com/en_US/livecycle/11.0/WorkspaceHelp/WS92d06802c76abadb-2b6ab502126beb6ba2f-7ffc.2.html) per ulteriori informazioni. Puoi assegnare, annullare l’assegnazione e riassegnare le code degli utenti in base alle tue esigenze organizzative. È possibile gestire le code condivise in due modi:

**Gestire L’Accesso A Un Utente**

Con questa opzione è possibile gestire l’accesso a una coda di utenti selezionata.

**Gestire L’Accesso Di Un Utente**

Questa opzione consente di gestire le code condivise assegnate a un utente selezionato.

## Gestione dell’accesso a una coda di utenti selezionata {#managing-access-to-a-selected-user-queue}

La funzionalità Gestisci accesso a un utente consente di gestire l&#39;accesso a una coda di utenti selezionata. Puoi concedere o revocare l’accesso a una coda di utenti selezionata ad altri utenti dell’organizzazione. Ad esempio, Kara Bowman è fuori sede. Utilizzando la funzionalità di gestione dell’accesso a un utente, la coda di Kara può essere condivisa con Akira Tanaka e John Jacobs per il completamento. In un secondo momento, quando Kara ritorna in ufficio, puoi revocare l&#39;accesso alla sua coda da Akira Tanaka e John Jacobs.

Una volta condivise, queste attività possono essere completate dall’utente, con accesso alla coda, utilizzando Workspace.

>[!NOTE]
>
>Flex Workspace è obsoleto per la versione con moduli AEM.

### Configurazione dell’accesso a una coda di utenti selezionata {#configuring-access-to-a-selected-user-queue}

1. Accedere alla console di amministrazione utilizzando un account Administrator.
1. Seleziona **Servizi** > **Forms Workflow** > **Coda condivisa**.

1. Nella scheda Gestisci accesso a un utente individuare e selezionare l&#39;utente di cui si desidera condividere la coda. In qualsiasi punto, nel riquadro in basso a destra viene visualizzato l’elenco degli utenti con accesso alla coda di utenti selezionata.
1. Nel riquadro in basso a sinistra, individua e seleziona l’utente. Fai clic su Condividi.
1. Fai clic su Salva per completare l’operazione.

### Revoca dell&#39;accesso a una coda di utenti selezionata {#revoking-access-to-a-selected-user-queue}

1. Accedere alla console di amministrazione utilizzando un account Administrator.
1. Seleziona **Servizi** > **Forms Workflow** > **Coda condivisa**.

1. Nella scheda Gestione accesso a un utente individuare e selezionare l&#39;utente di cui si desidera gestire la coda.
1. Nel riquadro in basso a destra viene visualizzato l’elenco degli utenti con accesso alla coda di utenti selezionata. Seleziona l’utente e fai clic su Revoca.
1. Fai clic su Salva per completare l’operazione.

## Gestione delle code assegnate a un utente {#managing-queues-assigned-to-a-user}

La funzionalità Gestisci accesso tramite utente consente di gestire le code assegnate a un utente selezionato. È possibile concedere o revocare l&#39;accesso alle code utente singolarmente a un utente selezionato. Ad esempio, si desidera assegnare le code utente di Akira Tanaka e John Jacobs a Kara Bowman. Utilizzando la funzionalità Gestisci accesso da parte di un utente, puoi cercare Kara Bowman e concedere l’accesso alle attività assegnate ad Akira Tanaka e John Jacobs. In un secondo momento, puoi revocare l’accesso di Kara Bowman a queste code di utenti.

Una volta assegnate, queste attività possono essere completate dall’utente utilizzando Workspace.

>[!NOTE]
>
>Flex Workspace è obsoleto per la versione con moduli AEM.

### Concessione dell’accesso a una coda di utenti selezionata {#granting-access-to-a-selected-user-queue}

1. Accedere alla console di amministrazione utilizzando un account Administrator.
1. Seleziona **Servizi** > **Forms Workflow** > **Coda condivisa**.

1. Nella scheda Gestisci accesso a un utente, individua e seleziona l’utente di cui desideri condividere la coda. In qualsiasi punto, nel riquadro in basso a destra viene visualizzato l’elenco degli utenti con accesso alla coda di utenti selezionata.
1. Nel riquadro in basso a sinistra, individuare e selezionare le code utente da condividere con l&#39;utente selezionato. Fai clic su Condividi.
1. Fai clic su Salva per completare l’operazione.

### Revoca dell&#39;accesso a una coda di utenti selezionata {#revoking_access_to_a_selected_user_queue-1}

1. Accedere alla console di amministrazione utilizzando un account Administrator.
1. Seleziona **Servizi** > **Forms Workflow** > **Coda condivisa**.

1. Nella scheda Gestisci l&#39;accesso di un utente individuare e selezionare l&#39;utente di cui si desidera gestire la coda.
1. Nel riquadro inferiore destro viene visualizzato l&#39;elenco delle code utente assegnate all&#39;utente selezionato. Seleziona la coda utente e fai clic su Revoca.
1. Fai clic su Salva per completare l’operazione.
