---
title: Gestione dell’accesso ai flussi di lavoro
description: Scopri come configurare gli elenchi di controllo di accesso in base agli account utente per consentire (o disabilitare) l’avvio e la partecipazione ai flussi di lavoro.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: cc54d637-d66c-49d2-99ee-00d96f1a74e0
solution: Experience Manager, Experience Manager Sites
feature: Operations
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 2%

---

# Gestione dell’accesso ai flussi di lavoro{#managing-access-to-workflows}

Configura gli ACL in base agli account utente per consentire (o disabilitare) l’avvio e la partecipazione ai flussi di lavoro.

## Autorizzazioni utente richieste per i flussi di lavoro {#required-user-permissions-for-workflows}

È possibile intraprendere azioni sui flussi di lavoro se:

* si sta utilizzando l&#39;account `admin`
* l&#39;account è stato assegnato al gruppo predefinito `workflow-users`:

   * questo gruppo dispone di tutti i privilegi necessari agli utenti per eseguire azioni del flusso di lavoro.
   * quando l’account si trova in questo gruppo, può accedere solo ai flussi di lavoro avviati dall’account.

* l&#39;account è stato assegnato al gruppo predefinito `workflow-administrators`:

   * questo gruppo dispone di tutti i privilegi necessari affinché gli utenti con privilegi possano monitorare e amministrare i flussi di lavoro.
   * quando l’account si trova in questo gruppo, ha accesso a tutti i flussi di lavoro.

>[!NOTE]
>
>Questi sono i requisiti minimi. Il tuo account deve essere anche il partecipante assegnato o un membro del gruppo assegnato per intraprendere passi specifici.

## Configurazione dell’accesso ai flussi di lavoro {#configuring-access-to-workflows}

I modelli di flusso di lavoro ereditano un elenco di controllo di accesso (ACL, Access Control List) predefinito per controllare il modo in cui gli utenti possono interagire con i flussi di lavoro. Per personalizzare l&#39;accesso utente per un flusso di lavoro, modificare l&#39;elenco di controllo di accesso (ACL) nel repository per la cartella contenente il nodo del modello di flusso di lavoro:

* [Applica un ACL per il modello di flusso di lavoro specifico a /var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models)
* [Crea una sottocartella in /var/workflow/models e applica a essa l’ACL](/help/sites-administering/workflows-managing.md#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that)

>[!NOTE]
>
>Per informazioni sull&#39;utilizzo di CRXDE Lite per configurare gli ACL, vedere [Gestione dei diritti di accesso](/help/sites-administering/user-group-ac-admin.md#access-right-management).

### Applica un ACL per il modello di flusso di lavoro specifico a /var/workflow/models {#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models}

Se il modello di flusso di lavoro è memorizzato in `/var/workflow/models`, è possibile assegnare un ACL specifico, relativo solo a tale flusso di lavoro, nella cartella:

1. Apri CRXDE Lite nel browser Web (ad esempio, [http://localhost:4502/crx/de](http://localhost:4502/crx/de)).
1. Nella struttura ad albero dei nodi, seleziona il nodo per la cartella dei modelli di flusso di lavoro:

   `/var/workflow/models`

1. Fare clic sulla scheda **Controllo di accesso**.
1. Nella tabella **Criteri di controllo di accesso locali** (**Elenco di controllo di accesso**) fare clic sull&#39;icona più (+) per **Aggiungere voce**.
1. Nella finestra di dialogo **Aggiungi nuova voce**, aggiungi un ACE con le seguenti proprietà:

   * **Entità**: `content-authors`
   * **Tipo**: `Deny`
   * **Privilegi**: `jcr:read`
   * **rep:glob**: riferimento al flusso di lavoro specifico

   ![wf-108](assets/wf-108.png)

   La tabella **Elenco di controllo di accesso** ora include la restrizione per `content-authors` nel modello di flusso di lavoro `prototype-wfm-01`.

   ![wf-109](assets/wf-109.png)

1. Fare clic su **Salva tutto**.

   Il flusso di lavoro `prototype-wfm-01` non è più disponibile per i membri del gruppo `content-authors`.

### Crea una sottocartella in /var/workflow/models e applica a essa l’ACL {#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that}

Il tuo team di sviluppo [&#x200B; può creare i flussi di lavoro in una sottocartella](/help/sites-developing/workflows-models.md#creating-a-new-workflow) di

`/var/workflow/models`

Paragonabile ai flussi di lavoro DAM memorizzati in

`/var/workflow/models/dam/`

È quindi possibile aggiungere un ACL alla cartella stessa.

1. Apri CRXDE Lite nel browser Web (ad esempio, [http://localhost:4502/crx/de](http://localhost:4502/crx/de)).
1. Nella struttura ad albero del nodo, seleziona il nodo per la singola cartella nella cartella dei modelli di flusso di lavoro; ad esempio:

   `/var/workflow/models/prototypes`

1. Fare clic sulla scheda **Controllo di accesso**.
1. Nella tabella **Criteri di controllo di accesso applicabili**, fare clic sull&#39;icona più (+) per **aggiungere** una voce.
1. Nella tabella **Criteri di controllo di accesso locali** (**Elenco di controllo di accesso**) fare clic sull&#39;icona più (+) per **Aggiungere voce**.
1. Nella finestra di dialogo **Aggiungi nuova voce**, aggiungi un ACE con le seguenti proprietà:

   * **Entità**: `content-authors`
   * **Tipo**: `Deny`
   * **Privilegi**: `jcr:read`

   >[!NOTE]
   >
   >Come con [Applica un ACL per il modello di flusso di lavoro specifico a /var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models) puoi includere un rep:glob per limitare l&#39;accesso a un flusso di lavoro specifico.

   ![wf-110](assets/wf-110.png)

   La tabella **Elenco di controllo di accesso** include ora la restrizione per `content-authors` nella cartella `prototypes`.

   ![wf-111](assets/wf-111.png)

1. Fare clic su **Salva tutto**.

   I modelli nella cartella `prototypes` non sono più disponibili per i membri del gruppo `content-authors`.
