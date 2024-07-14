---
title: Utilizzo dei flussi di lavoro per i progetti
description: Sono disponibili diversi flussi di lavoro per progetti già pronti all’uso.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
exl-id: 407fc164-291d-42f6-8c46-c1df9ba3d454
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Workflow
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 40%

---


# Utilizzo dei flussi di lavoro per i progetti {#working-with-project-workflows}

I flussi di lavoro per progetti disponibili includono:

* **Flusso di lavoro di approvazione progetto** - Questo flusso di lavoro consente di assegnare contenuti a un utente, rivederli e approvarli.
* **Richiedi lancio**: flusso di lavoro per richiedere un lancio.
* **Richiedi pagina di destinazione**: flusso di lavoro per richiedere una pagina di destinazione.
* **Richiedi e-mail**: flusso di lavoro per la richiesta di un’e-mail.
* **Servizio fotografico per prodotto e servizio fotografico per prodotto (Commerce)** - Associa le risorse ai prodotti
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

1. In un progetto multimediale, fai clic sulla freccia rivolta verso il basso in alto a destra nella sezione **Flussi di lavoro** e seleziona **Avvia flusso di lavoro**.
1. Nella procedura guidata del flusso di lavoro, seleziona **Richiedi copia** e fai clic su **Avanti**.
1. Inserisci un titolo del manoscritto e un breve riepilogo delle richieste. Se applicabile, immettere un conteggio delle parole di destinazione, una priorità dell&#39;attività e una data di scadenza.

   ![Flusso di lavoro per copia richiesta](assets/project-request-copy-workflow.png)

1. Fai clic su **Invia**.

Il flusso di lavoro viene avviato. L&#39;attività viene visualizzata nella scheda **Attività**.

## Flusso di lavoro per servizio fotografico per prodotto {#product-photo-shoot-workflow}

I flussi di lavoro **Servizio fotografico per prodotto** (sia commerce che senza commerce) sono descritti in dettaglio nel documento [Progetti creativi](/help/sites-authoring/managing-product-information.md)

## Flusso di lavoro di approvazione progetto {#project-approval-workflow}

Nel flusso di lavoro **Approvazione progetto** è possibile assegnare il contenuto a un utente, rivederlo e quindi approvarlo.

1. In un semplice progetto, fai clic sulla freccia rivolta verso il basso in alto a destra del riquadro **Flussi di lavoro** e seleziona **Avvia flusso di lavoro**.
1. Nella procedura guidata del flusso di lavoro, seleziona **Flusso di lavoro di approvazione progetto** e fai clic su **Avanti**.
1. Inserisci un titolo e seleziona a chi assegnarlo. Se necessario, puoi aggiungere una descrizione e il percorso del contenuto e impostare la priorità e la scadenza.

   ![Flusso di lavoro di approvazione progetto](assets/project-approval-workflow.png)

1. Fai clic su **Invia**.

Il flusso di lavoro viene avviato. L&#39;attività viene visualizzata nella scheda **Attività**.

## Richiedi flusso di lavoro di avvio {#request-launch-workflow}

Questo flusso di lavoro consente di richiedere un lancio.

1. In un semplice progetto, fai clic sulla freccia rivolta verso il basso in alto a destra del riquadro **Flussi di lavoro** e seleziona **Avvia flusso di lavoro**.
1. Nella procedura guidata del flusso di lavoro, seleziona **Richiedi flusso di lavoro di avvio** e fai clic su **Avanti**.
1. Inserisci un titolo per il lancio e specifica il percorso di origine del lancio. Se necessario, puoi anche aggiungere una descrizione e una data di pubblicazione. Seleziona Eredita i dati live della pagina sorgente o escludi le sottopagine a seconda di come desideri che si comporti il lancio.

   ![Richiedi flusso di lavoro lancio](assets/project-request-launch-workflow.png)

1. Fai clic su **Invia**.

Il flusso di lavoro viene avviato. Il flusso di lavoro viene visualizzato nell&#39;elenco **Flussi di lavoro**.

## Richiedi flusso di lavoro per pagina di destinazione {#request-landing-page-workflow}

Questo flusso di lavoro ti consente di richiedere una pagina di destinazione.

1. In un semplice progetto, fai clic sulla freccia rivolta verso il basso in alto a destra del riquadro **Flussi di lavoro** e seleziona **Avvia flusso di lavoro**.
1. Nella procedura guidata del flusso di lavoro, seleziona **Richiedi pagina di destinazione** e fai clic su **Avanti**.
1. Inserisci un titolo per la pagina di destinazione e il percorso principale. Se applicabile, inserisci una data di attivazione o scegli un file per la pagina di destinazione.

   ![Richiedi flusso di lavoro per la pagina di destinazione](assets/project-request-landing-page-workflow.png)

1. Fai clic su **Invia**.

Il flusso di lavoro viene avviato. L&#39;attività viene visualizzata nella scheda **Attività**.

## Flusso di lavoro Richiedi e-mail {#request-email-workflow}

Questo flusso di lavoro ti consente di richiedere un’e-mail. Si tratta dello stesso flusso di lavoro visualizzato nel riquadro **E-mail**.

1. In un semplice progetto, fai clic sulla freccia rivolta verso il basso in alto a destra del riquadro **Flussi di lavoro** e seleziona **Avvia flusso di lavoro**.
1. Nella procedura guidata del flusso di lavoro, seleziona **Richiedi e-mail** e fai clic su **Avanti**.
1. Immetti un titolo e-mail e i percorsi della campagna e del modello. Inoltre puoi fornire un nome, una descrizione e una data di attivazione.

   ![Richiedi flusso di lavoro e-mail](assets/project-request-email-workflow.png)

1. Fai clic su **Invia**.

Il flusso di lavoro viene avviato. L&#39;attività viene visualizzata nella scheda **Attività**.

## Flusso di lavoro Crea (e traduci) copia per lingua per le risorse {#create-and-translate-language-copy-workflow-for-assets}

I flussi di lavoro **Crea copia per lingua** e **Crea e traduci copia per lingua** sono descritti in dettaglio nel documento [Creazione di copie per lingua per Assets.](/help/assets/translation-projects.md)
