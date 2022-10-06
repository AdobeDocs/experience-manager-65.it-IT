---
title: Configurazione delle code condivise
seo-title: Configuring Shared Queues
description: Le code condivise consentono di configurare e gestire le code utente in modo efficace. Scopri come configurare le code condivise.
seo-description: Shared Queues allow you to configure and manage user queues effectively. Learn how to configure shared queues.
uuid: 69ab611d-334b-40a5-bd2d-533d4cb25eda
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fc403a60-b635-4334-9bf8-2f3d2036b2f3
exl-id: 5f4467c1-0f3f-4dc6-9bd5-98259f327295
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 0%

---

# Configurazione delle code condivise{#configuring-shared-queues}

Le code condivise consentono di configurare e gestire le code utente in modo efficace. Una coda utente è semplicemente tutte le attività assegnate a un utente, vedi [Per fare elenchi](https://help.adobe.com/en_US/livecycle/11.0/WorkspaceHelp/WS92d06802c76abadb-2b6ab502126beb6ba2f-7ffc.2.html) per ulteriori informazioni. Puoi assegnare, annullare l’assegnazione e riassegnare le code utente in base alle tue esigenze organizzative. Puoi gestire le code condivise in due modi:

**Gestire L’Accesso A Un Utente**

Puoi gestire l’accesso a una coda utente selezionata utilizzando questa opzione.

**Gestire L&#39;Accesso Da Un Utente**

Puoi gestire le code condivise assegnate a un utente selezionato utilizzando questa opzione.

## Gestione dell’accesso a una coda utente selezionata {#managing-access-to-a-selected-user-queue}

La funzionalità Gestisci accesso a un utente consente di gestire l&#39;accesso a una coda utente selezionata. Puoi concedere o revocare l’accesso a una coda utente selezionata ad altri utenti dell’organizzazione. Per esempio, Kara Bowman è fuori carica. Utilizzando la funzionalità Gestisci accesso a un utente, la sua coda può essere condivisa con Akira Tanaka e John Jacobs per il completamento. Ad un punto successivo, quando Kara Bowman ritorna in ufficio, puoi revocare l&#39;accesso alla sua coda da Akira Tanaka e John Jacobs.

Una volta condivise, queste attività possono essere completate dall’utente con accesso alla coda tramite Workspace.

>[!NOTE]
>
>Flex Workspace è obsoleto per AEM versione dei moduli.

### Configurazione dell’accesso a una coda utente selezionata {#configuring-access-to-a-selected-user-queue}

1. Accedi alla console di amministrazione utilizzando un account Amministratore.
1. Seleziona **Servizi** > **flusso di lavoro dei moduli** > **Coda condivisa**.

1. Nella scheda Gestisci accesso a un utente individuare e selezionare l&#39;utente di cui si desidera condividere la coda. In qualsiasi punto, nel riquadro in basso a destra viene visualizzato l’elenco degli utenti con accesso alla coda utente selezionata.
1. Nel riquadro in basso a sinistra, trova e seleziona l’utente. Fate clic su Condividi.
1. Fai clic su Salva per completare l’operazione.

### Revoca dell’accesso a una coda utente selezionata {#revoking-access-to-a-selected-user-queue}

1. Accedi alla console di amministrazione utilizzando un account Amministratore.
1. Seleziona **Servizi** > **flusso di lavoro dei moduli** > **Coda condivisa**.

1. Nella scheda Gestisci accesso a un utente , individua e seleziona l’utente di cui desideri gestire la coda.
1. Nel riquadro in basso a destra viene visualizzato l’elenco degli utenti con accesso alla coda utente selezionata. Selezionare l&#39;utente e fare clic su Revoca.
1. Fai clic su Salva per completare l’operazione.

## Gestione delle code assegnate a un utente {#managing-queues-assigned-to-a-user}

La funzionalità Gestisci accesso per utente consente di gestire le code assegnate a un utente selezionato. Puoi concedere o revocare l’accesso alle code utente a un utente selezionato singolarmente. Ad esempio, si desidera assegnare le code utente Akira Tanaka e John Jacobs a Kara Bowman. Utilizzando la funzionalità Gestisci accesso per un utente, puoi cercare Kara Bowman e concedere l&#39;accesso alle attività assegnate ad Akira Tanaka e John Jacobs. In un secondo momento, puoi revocare l’accesso di Kara Bowman a queste code di utenti.

Una volta assegnate, queste attività possono essere completate dall’utente tramite Workspace.

>[!NOTE]
>
>Flex Workspace è obsoleto per AEM versione dei moduli.

### Concessione dell&#39;accesso a una coda utente selezionata {#granting-access-to-a-selected-user-queue}

1. Accedi alla console di amministrazione utilizzando un account Amministratore.
1. Seleziona **Servizi** > **flusso di lavoro dei moduli** > **Coda condivisa**.

1. Nella scheda Gestisci accesso a un utente individuare e selezionare l&#39;utente di cui si desidera condividere la coda. In qualsiasi punto, nel riquadro in basso a destra viene visualizzato l’elenco degli utenti con accesso alla coda utente selezionata.
1. Nel riquadro in basso a sinistra, trova e seleziona le code utente che desideri condividere con l’utente selezionato. Fate clic su Condividi.
1. Fai clic su Salva per completare l’operazione.

### Revoca dell’accesso a una coda utente selezionata {#revoking_access_to_a_selected_user_queue-1}

1. Accedi alla console di amministrazione utilizzando un account Amministratore.
1. Seleziona **Servizi** > **flusso di lavoro dei moduli** > **Coda condivisa**.

1. Nella scheda Gestisci accesso per utente individuare e selezionare l&#39;utente di cui si desidera gestire la coda.
1. Nel riquadro in basso a destra viene visualizzato l’elenco delle code utente assegnate all’utente selezionato. Seleziona la coda utente e fai clic su Revoca.
1. Fai clic su Salva per completare l’operazione.
