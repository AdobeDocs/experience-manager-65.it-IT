---
title: Utilizzo dei flussi di lavoro per i progetti
seo-title: Working with Project Workflows
description: Sono disponibili diversi flussi di lavoro per progetti già pronti all’uso.
seo-description: A variety of project workflows are available out of the box.
uuid: 376922ca-e09e-4ac8-88c8-23dac2b49dbe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: 9d2bf30c-5190-4924-82cd-bcdfde24eb39
exl-id: 407fc164-291d-42f6-8c46-c1df9ba3d454
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 42%

---


# Utilizzo dei flussi di lavoro per i progetti {#working-with-project-workflows}

I flussi di lavoro per progetti disponibili includono:

* **Flusso di lavoro di approvazione progetto** - Questo flusso di lavoro consente di assegnare il contenuto a un utente, rivederlo e approvarlo.
* **Richiedi lancio**: flusso di lavoro per richiedere un lancio.
* **Richiedi pagina di destinazione**: flusso di lavoro per richiedere una pagina di destinazione.
* **Richiedi e-mail**: flusso di lavoro per la richiesta di un’e-mail.
* **Servizio fotografico per prodotto e servizio fotografico per prodotto (Commerce)** - Mappatura di risorse con prodotti
* **DAM - Crea e traduci copia lingua e DAM - Crea copia per lingua**: vengono creati file binari tradotti, metadati e tag per risorse e cartelle.

A seconda del modello di progetto selezionato, sono disponibili alcuni flussi di lavoro:

|   | **Progetto semplice** | **Progetto multimediale** | **Progetto servizio fotografico per prodotto** | **Progetto di traduzione** |
|---|:-:|:-:|:-:|:-:|
| Richiedi copia |  | x |  |  |
| Servizio fotografico per prodotto |  | x | x |  |
| Servizio fotografico per prodotto (Commerce) |  |  | x |  |
| Approvazione progetto | x |  |  |  |
| Richiedi lancio | x |  |  |  |
| Richiedi pagina di destinazione | x |  |  |  |
| Richiedi e-mail | x |  |  |  |
| Creazione DAM copia in lingua &amp;ast; |  |  |  | x |
| Creazione DAM e traduzione copia in lingua &amp;ast; |  |  |  | x |

>[!NOTE]
>
>&amp;ast Questi flussi di lavoro non si trovano nella sezione **Flusso di lavoro** in Progetti. Consulta [Creazione di copie per lingua per Assets.](/help/sites-administering/tc-manage.md)

I passaggi per avviare e completare i flussi di lavoro sono gli stessi, indipendentemente dal flusso di lavoro scelto. Cambiano solo i passaggi.

Avvia un flusso di lavoro direttamente in Progetti (ad eccezione di DAM - Crea copia per lingua o DAM - Crea e traduci copia per lingua). Le informazioni su eventuali attività in sospeso in un progetto sono elencate nel riquadro **Attività**. Le notifiche per le attività da completare vengono visualizzate accanto all’icona utente.

Per ulteriori informazioni sull’utilizzo dei flussi di lavoro in AEM, consulta i seguenti documenti:

* [Partecipare ai flussi di lavoro](/help/sites-authoring/workflows-participating.md)
* [Applicazione dei flussi di lavoro alle pagine](/help/sites-authoring/workflows-applying.md)
* [Configurare i flussi di lavoro](/help/sites-administering/workflows.md)

Questa sezione descrive i flussi di lavoro disponibili per Progetti.

## Richiedi copia flusso di lavoro {#request-copy-workflow}

Questo flusso di lavoro consente di richiedere un manoscritto a un utente e quindi approvarlo. Per avviare il flusso di lavoro di copia delle richieste:

1. In un progetto multimediale, tocca o fai clic sulla freccia verso il basso in alto a destra del **Flussi di lavoro** affiancare e selezionare **Avvia flusso di lavoro**.
1. Nella procedura guidata del flusso di lavoro seleziona **Richiedi copia** e fai clic su **Successivo**.
1. Inserisci un titolo del manoscritto e un breve riepilogo delle richieste. Se applicabile, immettere un conteggio delle parole di destinazione, una priorità dell&#39;attività e una data di scadenza.

   ![Flusso di lavoro Richiedi copia](assets/project-request-copy-workflow.png)

1. Fai clic su **Invia**.

Il flusso di lavoro viene avviato. L&#39;attività viene visualizzata nella **Attività** Card.

## Flusso di lavoro per servizio fotografico per prodotto {#product-photo-shoot-workflow}

Il **Servizio fotografico per prodotto** i flussi di lavoro (sia di commerce che senza commerce) sono descritti in dettaglio nel documento [Progetti creativi](/help/sites-authoring/managing-product-information.md)

## Flusso di lavoro di approvazione progetto {#project-approval-workflow}

In **Approvazione progetto** flusso di lavoro, puoi assegnare il contenuto a un utente, rivederlo e quindi approvarlo.

1. In un progetto semplice, tocca o fai clic sulla freccia verso il basso in alto a destra del **Flussi di lavoro** affiancare e selezionare **Avvia flusso di lavoro**.
1. Nella procedura guidata del flusso di lavoro seleziona **Flusso di lavoro di approvazione progetto** e fai clic su **Successivo**.
1. Inserisci un titolo e seleziona a chi assegnarlo. Se necessario, puoi aggiungere una descrizione e il percorso del contenuto e impostare la priorità e la scadenza.

   ![Flusso di lavoro di approvazione progetto](assets/project-approval-workflow.png)

1. Fai clic su **Invia**.

Il flusso di lavoro viene avviato. L&#39;attività viene visualizzata nella **Attività** Card.

## Richiedi flusso di lavoro di avvio {#request-launch-workflow}

Questo flusso di lavoro consente di richiedere un lancio.

1. In un progetto semplice, tocca o fai clic sulla freccia verso il basso in alto a destra del **Flussi di lavoro** affiancare e selezionare **Avvia flusso di lavoro**.
1. Nella procedura guidata del flusso di lavoro seleziona **Richiedi flusso di lavoro di avvio** e fai clic su **Successivo**.
1. Inserisci un titolo per il lancio e specifica il percorso di origine del lancio. Se necessario, puoi anche aggiungere una descrizione e una data di pubblicazione. Seleziona Eredita i dati live della pagina sorgente o escludi le sottopagine a seconda di come desideri che si comporti il lancio.

   ![Richiedi flusso di lavoro di lancio](assets/project-request-launch-workflow.png)

1. Fai clic su **Invia**.

Il flusso di lavoro viene avviato. Il flusso di lavoro viene visualizzato nel **Flussi di lavoro** elenco.

## Richiedi flusso di lavoro per pagina di destinazione {#request-landing-page-workflow}

Questo flusso di lavoro ti consente di richiedere una pagina di destinazione.

1. In un progetto semplice, tocca o fai clic sulla freccia verso il basso in alto a destra del **Flussi di lavoro** affiancare e selezionare **Avvia flusso di lavoro**.
1. Nella procedura guidata del flusso di lavoro seleziona **Richiedi pagina di destinazione** e fai clic su **Successivo**.
1. Inserisci un titolo per la pagina di destinazione e il percorso principale. Se applicabile, inserisci una data di attivazione o scegli un file per la pagina di destinazione.

   ![Richiedi flusso di lavoro per pagina di destinazione](assets/project-request-landing-page-workflow.png)

1. Fai clic su **Invia**.

Il flusso di lavoro viene avviato. L&#39;attività viene visualizzata nella **Attività** Card.

## Flusso di lavoro Richiedi e-mail {#request-email-workflow}

Questo flusso di lavoro ti consente di richiedere un’e-mail. Si tratta dello stesso flusso di lavoro visualizzato nel **E-mail** affiancare.

1. In un progetto semplice, tocca o fai clic sulla freccia verso il basso in alto a destra del **Flussi di lavoro** affiancare e selezionare **Avvia flusso di lavoro**.
1. Nella procedura guidata del flusso di lavoro seleziona **Richiedi e-mail** e fai clic su **Successivo**.
1. Immetti un titolo e-mail e i percorsi della campagna e del modello. Inoltre puoi fornire un nome, una descrizione e una data di attivazione.

   ![Richiedi flusso di lavoro e-mail](assets/project-request-email-workflow.png)

1. Fai clic su **Invia**.

Il flusso di lavoro viene avviato. L&#39;attività viene visualizzata nella **Attività** Card.

## Flusso di lavoro Crea (e traduci) copia per lingua per le risorse {#create-and-translate-language-copy-workflow-for-assets}

Il **Crea copia per lingua** e **Crea e traduci copia per lingua** I flussi di lavoro sono descritti in dettaglio nel documento [Creazione di copie per lingua per Assets.](/help/assets/translation-projects.md)
