---
title: Gestione dell'accesso ai flussi di lavoro
seo-title: Gestione dell'accesso ai flussi di lavoro
description: Scopri come gestire l’accesso ai flussi di lavoro.
seo-description: Scopri come gestire l’accesso ai flussi di lavoro.
uuid: 58f79b89-fe56-4565-a869-8179c1ac68de
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 5150867a-02a9-45c9-b2fd-e536b60ffa8c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 1%

---


# Gestione dell&#39;accesso ai flussi di lavoro{#managing-access-to-workflows}

Configurare gli ACL in base agli account utente per consentire (o disabilitare) l&#39;avvio e la partecipazione ai flussi di lavoro.

## Autorizzazioni utente necessarie per i flussi di lavoro {#required-user-permissions-for-workflows}

Le azioni sui flussi di lavoro possono essere intraprese se:

* state lavorando con l&#39;account `admin`
* l&#39;account è stato assegnato al gruppo predefinito `workflow-users`:

   * questo gruppo contiene tutti i privilegi necessari agli utenti per eseguire azioni sul flusso di lavoro.
   * quando l&#39;account si trova in questo gruppo, può accedere solo ai flussi di lavoro che ha avviato.

* l&#39;account è stato assegnato al gruppo predefinito `workflow-administrators`:

   * questo gruppo offre tutti i privilegi necessari agli utenti privilegiati per monitorare e amministrare i flussi di lavoro.
   * quando l&#39;account si trova in questo gruppo, può accedere a tutti i flussi di lavoro.

>[!NOTE]
>
>Questi sono i requisiti minimi. Il tuo account deve essere anche il partecipante assegnato o un membro del gruppo assegnato per eseguire passi specifici.

## Configurazione dell&#39;accesso ai flussi di lavoro {#configuring-access-to-workflows}

I modelli di workflow ereditano un elenco di controllo di accesso predefinito (ACL, Access Control List) per controllare in che modo gli utenti possono interagire con i flussi di lavoro. Per personalizzare l’accesso dell’utente per un flusso di lavoro, modificate l’elenco di controllo degli accessi (ACL) nell’archivio della cartella contenente il nodo del modello di workflow:

* [Applicare un ACL per il modello di flusso di lavoro specifico a /var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models)
* [Creare una sottocartella in /var/workflow/models e applicare l’ACL a tale cartella](/help/sites-administering/workflows-managing.md#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that)

>[!NOTE]
>
>Per informazioni sull&#39;utilizzo dei CRXDE Lite per configurare gli ACL, vedere [Accesso a Right Management](/help/sites-administering/user-group-ac-admin.md#access-right-management).

### Applicare un ACL per il modello di flusso di lavoro specifico a /var/workflow/models {#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models}

Se il modello di workflow è memorizzato in `/var/workflow/models`, è possibile assegnare un ACL specifico, relativo solo a tale flusso di lavoro, alla cartella:

1. Aprite il CRXDE Lite nel browser Web (ad esempio, [http://localhost:4502/crx/de](http://localhost:4502/crx/de)).
1. Nell&#39;albero dei nodi, selezionare il nodo per la cartella dei modelli di workflow:

   `/var/workflow/models`

1. Fare clic sulla scheda **Controllo accesso**.
1. Nella tabella **Criteri per il controllo dell&#39;accesso locale** (**elenco di controllo dell&#39;accesso**), fare clic sull&#39;icona più per **Aggiungi voce**.
1. Nella finestra di dialogo **Aggiungi nuova voce** aggiungere un nuovo elemento ACE con le seguenti proprietà:

   * **Principal**:  `content-authors`
   * **Tipo**: `Deny`
   * **Privilegi**:  `jcr:read`
   * **rep:DSM**: riferimento al flusso di lavoro specifico

   ![wf-108](assets/wf-108.png)

   La tabella **Access Control List** ora include il limite per `content-authors` nel modello di flusso di lavoro `prototype-wfm-01`.

   ![wf-109](assets/wf-109.png)

1. Fare clic su **Salva tutto**.

   Il flusso di lavoro `prototype-wfm-01` non è più disponibile per i membri del gruppo `content-authors`.

### Creare una sottocartella in /var/workflow/models e applicare l&#39;ACL a tale {#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that}

Il team di sviluppo [può creare i flussi di lavoro in una sottocartella](/help/sites-developing/workflows-models.md#creating-a-new-workflow) di

`/var/workflow/models`

Confronto con i flussi di lavoro DAM memorizzati in

`/var/workflow/models/dam/`

È quindi possibile aggiungere un ACL alla cartella stessa.

1. Aprite il CRXDE Lite nel browser Web (ad esempio, [http://localhost:4502/crx/de](http://localhost:4502/crx/de)).
1. Nell&#39;albero dei nodi, selezionare il nodo per la singola cartella nella cartella dei modelli di workflow; ad esempio:

   `/var/workflow/models/prototypes`

1. Fare clic sulla scheda **Controllo accesso**.
1. Nella tabella **Criteri di controllo di accesso applicabili**, fare clic sull&#39;icona più per **Aggiungere** una voce.
1. Nella tabella **Criteri per il controllo dell&#39;accesso locale** (**elenco di controllo dell&#39;accesso**), fare clic sull&#39;icona più per **Aggiungi voce**.
1. Nella finestra di dialogo **Aggiungi nuova voce** aggiungere un nuovo elemento ACE con le seguenti proprietà:

   * **Principal**:  `content-authors`
   * **Tipo**: `Deny`
   * **Privilegi**:  `jcr:read`

   >[!NOTE]
   >
   >Come per [Applicare un ACL per il modello di flusso di lavoro specifico a /var/workflow/models](/help/sites-administering/workflows-managing.md#apply-an-acl-for-the-specific-workflow-model-to-var-workflow-models), potete includere un rep:idspnList per limitare l&#39;accesso a un flusso di lavoro specifico.

   ![wf-110](assets/wf-110.png)

   La tabella **Access Control List** ora include il limite per `content-authors` nella cartella `prototypes`.

   ![wf-111](assets/wf-111.png)

1. Fare clic su **Salva tutto**.

   I modelli nella cartella `prototypes` non sono più disponibili per i membri del gruppo `content-authors`.

