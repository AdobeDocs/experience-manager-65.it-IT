---
title: Partecipare ai Flussi di lavoro
seo-title: Partecipare ai Flussi di lavoro
description: I flussi di lavoro generalmente includono passaggi che richiedono di eseguire un’attività in una pagina o una risorsa. Il flusso di lavoro seleziona un utente o un gruppo che esegua l’attività e assegna loro un elemento di lavoro.
seo-description: I flussi di lavoro generalmente includono passaggi che richiedono di eseguire un’attività in una pagina o una risorsa. Il flusso di lavoro seleziona un utente o un gruppo che esegua l’attività e assegna loro un elemento di lavoro.
uuid: 04dcc8f2-dc11-430f-b0ae-47ef2cb069a2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 1d7a4889-82c5-4096-8567-8f66215a8458
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 98%

---


# Partecipare ai Flussi di lavoro{#participating-in-workflows}

I flussi di lavoro generalmente includono passaggi che richiedono di eseguire un’attività in una pagina o una risorsa. Il flusso di lavoro seleziona un utente o un gruppo che esegua l’attività e assegna loro un elemento di lavoro.

## Elaborazione degli elementi di lavoro {#processing-your-work-items}

Puoi effettuare le seguenti azioni per elaborare un elemento di lavoro:

* **Completa**

   Quando si completa un elemento di lavoro, il flusso di lavoro procede al passaggio successivo.

* **Delega**

   Se ti è stato assegnato un passaggio, ma per qualche motivo non ti è possibile procedere, puoi delegarlo a un altro utente o gruppo.

   Gli utenti disponibili per la delega dipendono dal tipo di assegnatario:

   * Se l’elemento di lavoro è stato assegnato a un gruppo, sono disponibili i membri del gruppo.
   * Se l’elemento di lavoro è stato assegnato a un gruppo e poi è stato delegato a un utente, sono disponibili i membri del gruppo e il gruppo.
   * Se l&#39;elemento di lavoro è stato assegnato a un singolo utente, l’elemento di lavoro non può essere delegato.

* **Indietro**

   Se devi ripetere un passaggio o una serie di passaggi, puoi tornare indietro. Puoi quindi selezionare un passaggio precedente nel flusso di lavoro, per rielaborarlo. Il flusso di lavoro torna al passaggio specificato e procede da tale punto.

## Partecipare a un flusso di lavoro {#participating-in-a-workflow}

### Notifiche di azioni di flusso di lavoro assegnate {#notifications-of-assigned-workflow-actions}

Quando ti viene assegnato un elemento di lavoro (ad esempio, **Approva contenuto**) vengono visualizzati diversi avvisi e/o notifiche:

* La colonna **Stato** della console Siti web indica quando una pagina è in un flusso di lavoro:

   ![workflowstatus-1](assets/workflowstatus-1.png)

* Quando a te o a un gruppo di lavoro viene assegnato un elemento di lavoro come parte di un flusso di lavoro, l&#39;elemento di lavoro viene visualizzato nella Casella in entrata flusso di lavoro AEM.

   ![workflowinbox](assets/workflowinbox.png)

### Completamento di un passaggio partecipante {#completing-a-participant-step}

Dopo aver eseguito l&#39;azione indicata è possibile completare l&#39;elemento di lavoro, consentendo al flusso di lavoro di continuare. Segui la procedura riportata di seguito per completare l&#39;elemento di lavoro.

1. Seleziona il passaggio del flusso di lavoro e fai clic sul pulsante **Completa** nella barra di navigazione superiore.
1. Nella finestra di dialogo risultante, seleziona **Passaggio successivo**, vale a dire il passaggio successivo da eseguire. Un elenco a discesa mostra tutte le destinazioni appropriate. Puoi anche inserire un **Commento**.

   ![workflowcomplete](assets/workflowcomplete.png)

   Il numero di passaggi elencati dipende dalla progettazione del modello di flusso di lavoro.

1. Fai clic su **OK** per confermare l’azione.

### Delega di un passaggio partecipante  {#delegating-a-participant-step}

Segui la procedura riportata di seguito per delegare l&#39;elemento di lavoro.

1. Fai clic sul pulsante **Delega** nella barra di navigazione superiore.
1. Nella finestra di dialogo, usa l&#39;elenco a discesa per specificare l&#39;**Utente** a cui delegare l&#39;elemento di lavoro. Puoi anche aggiungere un **Commento**.

   ![workflowdelegate](assets/workflowdelegate.png)

1. Fai clic su **OK** per confermare l’azione.

### Tornare indietro di un passaggio  {#performing-step-back-on-a-participant-step}

Segui la procedura riportata di seguito per tornare a un passaggio precedente.

1. Fai clic sul pulsante Indietro nella barra di navigazione superiore.
1. Nella finestra di dialogo risultante, seleziona il Passaggio precedente; in altre parole, il passaggio da eseguire successivamente, anche se si tratta di un passaggio precedente del flusso di lavoro. Un elenco a discesa mostra tutte le destinazioni appropriate. 

   ![screen_shot_2018-08-10at155325](assets/screen_shot_2018-08-10at155325.jpg)

1. Fai clic su OK per confermare l&#39;azione.

