---
title: Configurare le code condivise
description: Le code condivise ti consentono di configurare e gestire in modo efficace le code utente. Scopri come configurare le code condivise.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 5f4467c1-0f3f-4dc6-9bd5-98259f327295
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '636'
ht-degree: 100%

---

# Configurare le code condivise{#configuring-shared-queues}

Le code condivise ti consentono di configurare e gestire in modo efficace le code utente. Una coda utente è costituita semplicemente da tutte le attività assegnate a un utente. Per ulteriori informazioni, consulta [Elenchi attività](https://help.adobe.com/en_US/livecycle/11.0/WorkspaceHelp/WS92d06802c76abadb-2b6ab502126beb6ba2f-7ffc.2.html). Puoi assegnare, annullare l’assegnazione e riassegnare le code utente in base alle tue esigenze organizzative. Puoi gestire le code condivise in due modi:

**Gestire l’accesso a un utente**

Con questa opzione puoi gestire l’accesso a una coda utente selezionata.

**Gestire l’accesso di un utente**

Con questa opzione puoi gestire le code condivise assegnate a un utente selezionato.

## Gestire l’accesso a una coda utente selezionata {#managing-access-to-a-selected-user-queue}

La funzionalità Gestisci accesso a un utente consente di gestire l’accesso a una coda utente selezionata. Puoi concedere o revocare l’accesso a una coda utente selezionata ad altri utenti dell’organizzazione. Ad esempio, Kara Bowman è fuori sede. Utilizzando la funzionalità Gestisci accesso a un utente, la coda di Kara può essere condivisa con Akira Tanaka e John Jacobs per il completamento. In un secondo momento, quando Kara ritorna in ufficio, potrai revocare l’accesso alla sua coda ad Akira Tanaka e John Jacobs.

Una volta condivise, queste attività possono essere completate dall’utente, con accesso alla coda, utilizzando Workspace.

>[!NOTE]
>
>Per la versione di AEM Forms, l’area di lavoro flessibile è obsoleta.

### Configurazione dell’accesso a una coda utente selezionata {#configuring-access-to-a-selected-user-queue}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

1. Accedi alla console di amministrazione utilizzando un account Amministratore.
1. Seleziona **Servizi** > **Forms Workflow** > **Coda condivisa**.

1. Nella scheda Gestisci accesso a un utente, individua e seleziona l’utente di cui desideri condividere la coda. In qualsiasi punto, nel riquadro in basso a destra viene visualizzato l’elenco degli utenti con accesso alla coda utente selezionata.
1. Nel riquadro in basso a sinistra, individua e seleziona l’utente. Fai clic su Condividi.
1. Fai clic su Salva per completare.

### Revoca dell’accesso a una coda utente selezionata {#revoking-access-to-a-selected-user-queue}

1. Accedi alla console di amministrazione utilizzando un account Amministratore.
1. Seleziona **Servizi** > **Forms Workflow** > **Coda condivisa**.

1. Nella scheda Gestisci accesso a un utente individua e seleziona l’utente di cui desideri gestire la coda.
1. Nel riquadro in basso a destra viene visualizzato l’elenco degli utenti con accesso alla coda utente selezionata. Seleziona l’utente e fai clic su Revoca.
1. Fai clic su Salva per completare.

## Gestione delle code assegnate a un utente {#managing-queues-assigned-to-a-user}

La funzionalità Gestisci accesso per singolo utente consente di gestire le code assegnate a un utente selezionato. È possibile concedere o revocare l’accesso alle code utente per un utente selezionato singolarmente. Ad esempio, desideri assegnare le code utente di Akira Tanaka e John Jacobs a Kara Bowman. Utilizzando la funzionalità Gestisci accesso per singolo utente, puoi cercare Kara Bowman e concedere l’accesso alle attività assegnate ad Akira Tanaka e John Jacobs. In un secondo momento, puoi revocare l’accesso di Kara Bowman a queste code utente.

Una volta assegnate, queste attività possono essere completate dall’utente utilizzando Workspace.

>[!NOTE]
>
>Per la versione di AEM Forms, l’area di lavoro flessibile è obsoleta.

### Concessione dell’accesso a una coda utente selezionata {#granting-access-to-a-selected-user-queue}

1. Accedi alla console di amministrazione utilizzando un account Amministratore.
1. Seleziona **Servizi** > **Forms Workflow** > **Coda condivisa**.

1. Nella scheda Gestisci accesso a un utente, individua e seleziona l’utente di cui desideri condividere la coda. In qualsiasi punto, nel riquadro in basso a destra viene visualizzato l’elenco degli utenti con accesso alla coda utente selezionata.
1. Nel riquadro in basso a sinistra, individua e seleziona le code utente che desideri condividere con l’utente selezionato. Fai clic su Condividi.
1. Fai clic su Salva per completare.

### Revoca dell’accesso a una coda utente selezionata {#revoking_access_to_a_selected_user_queue-1}

1. Accedi alla console di amministrazione utilizzando un account Amministratore.
1. Seleziona **Servizi** > **Forms Workflow** > **Coda condivisa**.

1. Nella scheda Gestisci accesso per singolo utente individua e seleziona l’utente di cui desideri gestire la coda.
1. Nel riquadro inferiore a destra viene visualizzato l’elenco delle code utente assegnate all’utente selezionato. Seleziona la coda utente e fai clic su Revoca.
1. Fai clic su Salva per completare.
