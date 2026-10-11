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
source-wordcount: '652'
ht-degree: 100%
---
# Configurare le code condivise{#configuring-shared-queues}

Le code condivise ti consentono di configurare e gestire in modo efficace le code utente. Una coda utente è costituita semplicemente da tutte le attività assegnate a un utente. Per ulteriori informazioni, consulta [Elenchi attività](https://help.adobe.com/it_IT/livecycle/11.0/WorkspaceHelp/WS92d06802c76abadb-2b6ab502126beb6ba2f-7ffc.2.html). Puoi assegnare, annullare l’assegnazione e riassegnare le code utente in base alle tue esigenze organizzative. Puoi gestire le code condivise in due modi:

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
