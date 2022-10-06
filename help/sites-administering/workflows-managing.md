---
title: Gestione dell’accesso ai flussi di lavoro
seo-title: Managing Access to Workflows
description: Scopri come gestire l’accesso ai flussi di lavoro.
seo-description: Learn how to manage access to Workflows.
uuid: 58f79b89-fe56-4565-a869-8179c1ac68de
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 5150867a-02a9-45c9-b2fd-e536b60ffa8c
exl-id: cc54d637-d66c-49d2-99ee-00d96f1a74e0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 3%

---

# Gestione dell’accesso ai flussi di lavoro{#managing-access-to-workflows}

Configura le ACL in base agli account utente per consentire (o disabilitare) l&#39;avvio e la partecipazione ai flussi di lavoro.

## Autorizzazioni utente necessarie per i flussi di lavoro {#required-user-permissions-for-workflows}

È possibile intraprendere azioni sui flussi di lavoro se:

* stai lavorando con `admin` account
* l&#39;account è stato assegnato al gruppo predefinito `workflow-users`:

   * questo gruppo contiene tutti i privilegi necessari agli utenti per eseguire le azioni del flusso di lavoro.
   * quando l’account si trova in questo gruppo, dispone solo dell’accesso ai flussi di lavoro avviati.

* l&#39;account è stato assegnato al gruppo predefinito `workflow-administrators`:

   * questo gruppo dispone di tutti i privilegi necessari per consentire agli utenti privilegiati di monitorare e amministrare i flussi di lavoro.
   * quando l’account si trova in questo gruppo ha accesso a tutti i flussi di lavoro.

>[!NOTE]
>
>Questi sono i requisiti minimi. Il tuo account deve anche essere il partecipante assegnato o un membro del gruppo assegnato per compiere passi specifici.

## Configurazione dell’accesso ai flussi di lavoro {#configuring-access-to-workflows}

I modelli di flusso di lavoro ereditano un elenco di controllo accessi predefinito (ACL) per controllare come gli utenti possono interagire con i flussi di lavoro. Per personalizzare l&#39;accesso utente per un flusso di lavoro, modifica l&#39;elenco di controllo accessi (ACL) nel repository per la cartella contenente il nodo del modello di flusso di lavoro:

* [Applica un ACL per il modello di flusso di lavoro specifico a /var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models)
* [Crea una sottocartella in /var/workflow/models e applica l&#39;ACL a quello](/help/sites-administering/workflows-managing.md#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that)

>[!NOTE]
>
>Per informazioni sull&#39;utilizzo di CRXDE Lite per configurare le ACL, vedi [Accesso alla gestione dei diritti](/help/sites-administering/user-group-ac-admin.md#access-right-management).

### Applica un ACL per il modello di flusso di lavoro specifico a /var/workflow/models {#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models}

Se il modello di flusso di lavoro è memorizzato in `/var/workflow/models` quindi puoi assegnare un ACL specifico, rilevante solo per quel flusso di lavoro, sulla cartella:

1. Apri CRXDE Lite nel browser Web (ad esempio, [http://localhost:4502/crx/de](http://localhost:4502/crx/de)).
1. Nella struttura ad albero dei nodi, seleziona il nodo per la cartella dei modelli di flusso di lavoro:

   `/var/workflow/models`

1. Fai clic sul pulsante **Controllo degli accessi** scheda .
1. In **Criteri di controllo accessi locali** (**Elenco di controllo di accesso**), fai clic sull’icona più (+) per **Aggiungi voce**.
1. In **Aggiungi nuova voce** aggiungi un nuovo ACE con le seguenti proprietà:

   * **Principale**: `content-authors`
   * **Tipo**: `Deny`
   * **Privilegi**: `jcr:read`
   * **rep:glob**: riferimento al flusso di lavoro specifico

   ![wf-108](assets/wf-108.png)

   La **Elenco di controllo di accesso** la tabella ora include il limite per `content-authors` sulla `prototype-wfm-01` modello di flusso di lavoro.

   ![wf-109](assets/wf-109.png)

1. Fai clic su **Salva tutto**.

   La `prototype-wfm-01` il flusso di lavoro non è più disponibile per i membri del `content-authors` gruppo.

### Crea una sottocartella in /var/workflow/models e applica l&#39;ACL a quello {#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that}

Le [il team di sviluppo può creare i flussi di lavoro in una sottocartella](/help/sites-developing/workflows-models.md#creating-a-new-workflow) di

`/var/workflow/models`

Comparabile ai flussi di lavoro DAM memorizzati in

`/var/workflow/models/dam/`

Puoi quindi aggiungere un ACL alla cartella stessa.

1. Apri CRXDE Lite nel browser Web (ad esempio, [http://localhost:4502/crx/de](http://localhost:4502/crx/de)).
1. Nella struttura ad albero dei nodi, seleziona il nodo per la singola cartella nella cartella dei modelli di flusso di lavoro; ad esempio:

   `/var/workflow/models/prototypes`

1. Fai clic sul pulsante **Controllo degli accessi** scheda .
1. In **Criteri applicabili per il controllo degli accessi** tabella, fai clic sull’icona più (+) per **Aggiungi** una voce.
1. In **Criteri di controllo accessi locali** (**Elenco di controllo di accesso**), fai clic sull’icona più (+) per **Aggiungi voce**.
1. In **Aggiungi nuova voce** aggiungi un nuovo ACE con le seguenti proprietà:

   * **Principale**: `content-authors`
   * **Tipo**: `Deny`
   * **Privilegi**: `jcr:read`

   >[!NOTE]
   >
   >Come con [Applica un ACL per il modello di flusso di lavoro specifico a /var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models) puoi includere un rep:glob per limitare l’accesso a un flusso di lavoro specifico.

   ![wf-110](assets/wf-110.png)

   La **Elenco di controllo di accesso** la tabella ora include il limite per `content-authors` sulla `prototypes` cartella.

   ![wf-111](assets/wf-111.png)

1. Fai clic su **Salva tutto**.

   I modelli nel `prototypes` la cartella non è più disponibile per i membri della `content-authors` gruppo.
