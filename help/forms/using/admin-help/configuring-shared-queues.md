---
title: Configurazione delle code condivise
seo-title: Configurazione delle code condivise
description: Le code condivise consentono di configurare e gestire le code degli utenti in modo efficace. Scoprite come configurare le code condivise.
seo-description: Le code condivise consentono di configurare e gestire le code degli utenti in modo efficace. Scoprite come configurare le code condivise.
uuid: 69ab611d-334b-40a5-bd2d-533d4cb25eda
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fc403a60-b635-4334-9bf8-2f3d2036b2f3
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---


# Configurazione delle code condivise{#configuring-shared-queues}

Le code condivise consentono di configurare e gestire le code degli utenti in modo efficace. Una coda di utenti è semplicemente tutte le attività assegnate a un utente. Per ulteriori informazioni, vedere [To Do Lists](https://help.adobe.com/en_US/livecycle/11.0/WorkspaceHelp/WS92d06802c76abadb-2b6ab502126beb6ba2f-7ffc.2.html). Potete assegnare, annullare l’assegnazione e riassegnare le code utente in base alle esigenze aziendali. Potete gestire le code condivise in due modi:

**Gestire L&#39;Accesso A Un Utente**

Questa opzione consente di gestire l&#39;accesso a una coda di utenti selezionata.

**Gestire L&#39;Accesso Da Un Utente**

Questa opzione consente di gestire le code condivise assegnate a un utente selezionato.

## Gestione dell&#39;accesso a una coda utente selezionata {#managing-access-to-a-selected-user-queue}

Gestione dell&#39;accesso a un utente consente di gestire l&#39;accesso a una coda di utenti selezionata. Potete concedere o revocare l’accesso a una coda di utenti selezionata ad altri utenti nell’organizzazione. Per esempio, Kara Bowman è fuori ufficio. Utilizzando la funzionalità Gestisci accesso a un utente, la sua coda può essere condivisa con Akira Tanaka e John Jacobs per il completamento. A un punto successivo, quando Kara Bowman ritorna in ufficio, puoi revocare l&#39;accesso alla sua coda da Akira Tanaka e John Jacobs.

Una volta condivise, queste attività possono essere completate dall&#39;utente, con accesso alla coda, tramite Workspace.

>[!NOTE]
>
>Flex Workspace è obsoleto per AEM rilascio di moduli.

### Configurazione dell&#39;accesso a una coda utente selezionata {#configuring-access-to-a-selected-user-queue}

1. Accedete alla console di amministrazione utilizzando un account amministratore.
1. Selezionare **Servizi** > **flusso di lavoro moduli** > **Coda condivisa**.

1. Nella scheda Gestisci accesso a un utente, individua e seleziona l’utente di cui desideri condividere la coda. In qualsiasi momento, il riquadro in basso a destra visualizza l&#39;elenco degli utenti con accesso alla coda di utenti selezionata.
1. Nel riquadro in basso a sinistra, individuate e selezionate l’utente. Fate clic su Condividi.
1. Fai clic su Salva per completare l&#39;operazione.

### Revoca dell&#39;accesso a una coda utente selezionata {#revoking-access-to-a-selected-user-queue}

1. Accedete alla console di amministrazione utilizzando un account amministratore.
1. Selezionare **Servizi** > **flusso di lavoro moduli** > **Coda condivisa**.

1. Nella scheda Gestisci accesso a un utente, individua e seleziona l’utente di cui desideri gestire la coda.
1. Nel riquadro in basso a destra viene visualizzato l’elenco degli utenti con accesso alla coda di utenti selezionata. Selezionate l’utente e fate clic su Revoca.
1. Fai clic su Salva per completare l&#39;operazione.

## Gestione delle code assegnate a un utente {#managing-queues-assigned-to-a-user}

La funzionalità Gestisci accesso per utente consente di gestire le code assegnate a un utente selezionato. Potete concedere o revocare l&#39;accesso alle code utente a un utente selezionato singolarmente. Ad esempio, potete assegnare le code utente Akira Tanaka e John Jacobs a Kara Bowman. Utilizzando la funzionalità Gestisci accesso per utente, potete cercare Kara Bowman e concedere l&#39;accesso alle attività assegnate ad Akira Tanaka e John Jacobs. In un secondo momento, potete revocare l&#39;accesso di Kara Bowman a queste code di utenti.

Una volta assegnati, questi task possono essere completati dall&#39;utente tramite Workspace.

>[!NOTE]
>
>Flex Workspace è obsoleto per AEM rilascio di moduli.

### Concessione dell&#39;accesso a una coda utente selezionata {#granting-access-to-a-selected-user-queue}

1. Accedete alla console di amministrazione utilizzando un account amministratore.
1. Selezionare **Servizi** > **flusso di lavoro moduli** > **Coda condivisa**.

1. Nella scheda Gestisci accesso a un utente, individua e seleziona l&#39;utente di cui desideri condividere la coda. In qualsiasi momento, il riquadro in basso a destra visualizza l&#39;elenco degli utenti con accesso alla coda di utenti selezionata.
1. Nel riquadro in basso a sinistra, individuate e selezionate le code utente da condividere con l’utente selezionato. Fate clic su Condividi.
1. Fai clic su Salva per completare l&#39;operazione.

### Revoca dell&#39;accesso a una coda utente selezionata {#revoking_access_to_a_selected_user_queue-1}

1. Accedete alla console di amministrazione utilizzando un account amministratore.
1. Selezionare **Servizi** > **flusso di lavoro moduli** > **Coda condivisa**.

1. Nella scheda Gestisci accesso per utente, individua e seleziona l’utente di cui desideri gestire la coda.
1. Nel riquadro in basso a destra viene visualizzato l’elenco delle code utente assegnate all’utente selezionato. Selezionate la coda di utenti e fate clic su Revoca.
1. Fai clic su Salva per completare l&#39;operazione.

