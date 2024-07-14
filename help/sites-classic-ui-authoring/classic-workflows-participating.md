---
title: Partecipazione ai flussi di lavoro
description: In genere i flussi di lavoro includono passaggi che richiedono di eseguire un’attività su una pagina o una risorsa. Il flusso di lavoro seleziona un utente o un gruppo per eseguire l’attività e assegna un elemento di lavoro a tale persona o gruppo.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: 2f1a3a73-7a20-48c7-8f3e-54252f5fb71c
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: a28883778c5e8fb90cbbd0291ded17059ab2ba7e
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 39%

---

# Partecipazione ai flussi di lavoro{#participating-in-workflows}

In genere i flussi di lavoro includono passaggi che richiedono di eseguire un’attività su una pagina o una risorsa. Il flusso di lavoro seleziona un utente o un gruppo per eseguire l’attività e assegna un elemento di lavoro a tale persona o gruppo.

## Elaborazione degli elementi di lavoro {#processing-your-work-items}

Per elaborare un elemento di lavoro è possibile eseguire le azioni seguenti:

* **Completa**

  Quando si completa un elemento di lavoro, il flusso di lavoro procede al passaggio successivo.

* **Delega**

  Se ti è stato assegnato un passaggio, ma per qualche motivo non ti è possibile intervenire, puoi delegarlo a un altro utente o gruppo.

  Gli utenti disponibili per la delega dipendono dal tipo di assegnatario dell’elemento di lavoro:

   * Se l’elemento di lavoro è stato assegnato a un gruppo, sono disponibili i membri del gruppo.
   * Se l’elemento di lavoro è stato assegnato a un gruppo e poi è stato delegato a un utente, sono disponibili i membri del gruppo e il gruppo.
   * Se l’elemento di lavoro è stato assegnato a un singolo utente, l’elemento di lavoro non può essere delegato.

* **Indietro**

  Se scopri che un passaggio, o una serie di passaggi, deve essere ripetuto, puoi fare un passo indietro. Questo consente di selezionare un passaggio precedente nel flusso di lavoro, per la rielaborazione. Il flusso di lavoro ritorna al passaggio specificato, quindi procede da lì.

## Partecipazione a un flusso di lavoro {#participating-in-a-workflow}

### Notifiche delle azioni del flusso di lavoro assegnate {#notifications-of-assigned-workflow-actions}

Quando ti viene assegnato un elemento di lavoro (ad esempio, **Approva contenuto**) vengono visualizzati diversi avvisi e/o notifiche:

* La colonna **Stato** della console Siti Web indica quando una pagina si trova in un flusso di lavoro:

  ![workflowstatus-1](assets/workflowstatus-1.png)

* Quando a te o a un gruppo a cui appartieni viene assegnato un elemento di lavoro come parte di un flusso di lavoro, l’elemento di lavoro viene visualizzato nella casella in entrata del flusso di lavoro AEM.

  ![workflowinbox](assets/workflowinbox.png)

### Completamento di un passaggio partecipante {#completing-a-participant-step}

Dopo aver eseguito l’azione indicata, puoi completare l’elemento di lavoro, consentendo in tal modo la continuazione del flusso di lavoro. Per completare l&#39;elemento di lavoro, attenersi alla procedura descritta di seguito.

1. Seleziona il passaggio del flusso di lavoro e fai clic sul pulsante **Completa** nella barra di navigazione superiore.
1. Nella finestra di dialogo risultante, seleziona il **Passaggio successivo**, ovvero il passaggio da eseguire successivamente. Un elenco a discesa mostra tutte le destinazioni appropriate. È inoltre possibile immettere **Commento**.

   ![workflowcomplete](assets/workflowcomplete.png)

   Il numero di passaggi elencati dipende dalla progettazione del modello di flusso di lavoro.

1. Fai clic su **OK** per confermare l&#39;azione.

### Delega di un passaggio partecipante {#delegating-a-participant-step}

Per delegare un elemento di lavoro, attenersi alla procedura descritta di seguito.

1. Fai clic sul pulsante **Delega** nella barra di navigazione superiore.
1. Nella finestra di dialogo, utilizza l&#39;elenco a discesa per selezionare l&#39;**utente** a cui delegare l&#39;elemento di lavoro. Puoi anche aggiungere un **Commento**.

   ![workflowdelegate](assets/workflowdelegate.png)

1. Fai clic su **OK** per confermare l&#39;azione.

### Esecuzione di un passo indietro su un Passaggio Partecipante {#performing-step-back-on-a-participant-step}

Per tornare indietro, attenersi alla procedura descritta di seguito.

1. Fai clic sul pulsante Indietro nella barra di navigazione superiore.
1. Nella finestra di dialogo risultante, seleziona il passaggio precedente, ovvero il passaggio da eseguire successivamente, anche se si tratta di un passaggio precedente nel flusso di lavoro. Un elenco a discesa mostra tutte le destinazioni appropriate.

   ![schermata_shot_2018-08-10at155325](assets/screen_shot_2018-08-10at155325.jpg)

1. Fai clic su OK per confermare l’azione.
