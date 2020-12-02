---
title: Applicazione dei flussi di lavoro alle pagine
seo-title: Applicazione dei flussi di lavoro alle pagine
description: I flussi di lavoro possono essere avviati dalla console Siti web o, durante la modifica di una pagina, dalla barra laterale.
seo-description: I flussi di lavoro possono essere avviati dalla console Siti web o, durante la modifica di una pagina, dalla barra laterale.
uuid: 55f6f1d7-da54-4732-b9ff-b7479622db51
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 22712b73-90f2-4329-b32f-dbb7ce802d1d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 86%

---


# Applicazione dei flussi di lavoro alle pagine{#applying-workflows-to-pages}

Quando si applica il flusso di lavoro, è necessario specificare le seguenti informazioni:

* Flusso di lavoro da applicare.

   Puoi utilizzare qualsiasi flusso di lavoro a cui hai accesso, secondo quanto assegnato dall’amministratore AEM.
* Facoltativamente:

   * Un commento che fornisce informazioni sul motivo per cui è stato avviato il flusso di lavoro.
   * Un titolo che aiuta a identificare l&#39;istanza del flusso di lavoro nella casella in entrata di un utente.

>[!NOTE]
>
>Gli amministratori AEM possono avviare i flussi di lavoro attraverso [molti altri metodi](/help/sites-administering/workflows-starting.md).

## Applicazione dei flussi di lavoro {#applying-workflows}

I flussi di lavoro possono essere avviati dalla console Siti web o, durante la modifica di una pagina, dalla barra laterale.

La colonna **Stato** nella console **Siti Web** indica se un flusso di lavoro è stato applicato a una pagina:

![workflowstatus](assets/workflowstatus.png)

### Avvio di un flusso di lavoro dalla console Siti web {#starting-a-workflow-from-the-websites-console}

1. Apri la console Siti web. ([http://localhost:4502/siteadmin](http://localhost:4502/siteadmin))
1. Nella struttura ad albero dei siti web, seleziona il padre della pagina a cui applicare il flusso di lavoro.
1. Nell&#39;elenco delle pagine, seleziona la pagina, quindi fai clic su Flusso di lavoro.
1. Nella finestra di dialogo Avvia flusso di lavoro, seleziona il flusso di lavoro da applicare. In alternativa, inserisci un commento e un titolo. Quindi fai clic su Avvia.

### Avvio di un flusso di lavoro con la barra laterale  {#starting-a-workflow-using-sidekick}

1. Apri la console Siti web. 
1. Apri la pagina desiderata.
1. Seleziona la scheda Flusso di lavoro dalla barra laterale.
1. Espandete la finestra di dialogo **Workflow** per selezionare il **Workflow** e, facoltativamente, immettete **Workflow Title** e **Comment**.

   ![workflowstartsidekick](assets/workflowstartsidekick.png)

1. Fai clic su **Inizia un nuovo flusso di lavoro** per avviare un&#39;istanza di flusso di lavoro con le proprietà configurate e la pagina corrente come payload. Ora il flusso di lavoro è in esecuzione.

