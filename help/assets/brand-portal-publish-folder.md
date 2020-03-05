---
title: Pubblicare le cartelle su Brand Portal
seo-title: Pubblicare le cartelle su Brand Portal
description: Scoprite come pubblicare e annullare la pubblicazione delle cartelle in Brand Portal.
seo-description: Scoprite come pubblicare e annullare la pubblicazione delle cartelle in Brand Portal.
uuid: 350beb85-c0fb-4a1c-8597-c03592c02d3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 39b8cf9b-afec-4c9a-8a5d-7fc87e643f26
docset: aem65
translation-type: tm+mt
source-git-commit: 9f923782d3d0a7bdf45b18e8025bd2d083acf77c

---


# Publish folders to Brand Portal{#publish-folders-to-brand-portal}

In qualità di amministratore Risorse Adobe Experience Manager (AEM), puoi pubblicare risorse e cartelle nell’istanza del Portale del marchio di AEM Assets (o pianificare il flusso di lavoro di pubblicazione in una data/ora successiva) per la tua organizzazione. Tuttavia, devi prima integrare AEM Assets con il Brand Portal. Per informazioni dettagliate, consultate [Configurare AEM Assets con il Portale](/help/assets/configure-aem-assets-with-brand-portal.md)marchio.

Dopo aver pubblicato una risorsa o una cartella, questa è disponibile per gli utenti in Brand Portal.

Se apportate modifiche successive alla risorsa o alla cartella originale in Risorse AEM, le modifiche non vengono riportate nel Portale marchio fino a quando non ripubblicate la risorsa o la cartella. Questa funzione garantisce che le modifiche in corso non siano disponibili in Brand Portal. Solo le modifiche approvate pubblicate da un amministratore sono disponibili in Brand Portal.

## Publish folders to Brand Portal {#publish-folders-to-brand-portal-1}

1. Dall’interfaccia di Risorse AEM, passa il mouse sulla cartella desiderata e seleziona l’opzione **Pubblica** dalle azioni rapide.

   In alternativa, selezionate la cartella desiderata e seguite i passaggi successivi.

   ![publish2bp](assets/publish2bp.png)

1. **Pubblica le cartelle ora**

   Per pubblicare le cartelle selezionate in Brand Portal, effettuate una delle seguenti operazioni:

   * Dalla barra degli strumenti, selezionate Pubblicazione **** rapida. Dal menu, selezionate **Pubblica su Brand Portal**.

   * Dalla barra degli strumenti, selezionate **Gestisci pubblicazione**.
   1. In **Azione** , selezionate **Pubblica su Portale** marchio, in **Pianificazione** selezionate **Ora** e fate clic su **Avanti.**
   1. Conferma la selezione nell’ **ambito** e fai clic su **Pubblica sul portale** del marchio.
   Viene visualizzato un messaggio che informa che la cartella è stata messa in coda per la pubblicazione sul Brand Portal. Accedete all’interfaccia Brand Portal per visualizzare la cartella pubblicata.

   **Pubblicare le cartelle in un secondo momento**

   Per pianificare il flusso di lavoro di pubblicazione in Brand Portal delle cartelle di risorse in una data o ora successiva:

   1. Dopo aver selezionato le risorse o le cartelle da pubblicare, selezionate **Gestisci pubblicazione** dalla barra degli strumenti nella parte superiore.
   1. In **Azione** , selezionate **Pubblica su Portale** marchio, in **Pianificazione** selezionate **Più tardi**.

      ![publishlaterbp](assets/publishlaterbp.png)

   1. Selezionate una data **di** attivazione e specificate l&#39;ora. Fai clic su **Avanti**.
   1. Conferma la selezione nell’ **ambito**. Fai clic su **Avanti**.
   1. Specificate un titolo del flusso di lavoro in **Flussi di lavoro**. Fate clic su **Pubblica più tardi**.

      ![manageschedulepub](assets/manageschedulepub.png)



## Unpublish folders from Brand Portal {#unpublish-folders-from-brand-portal}

Potete rimuovere qualsiasi cartella di risorse pubblicata nel Portale marchio annullandone la pubblicazione dall’istanza di AEM Author. Dopo l’annullamento della pubblicazione della cartella originale, la relativa copia non sarà più disponibile per gli utenti di Brand Portal.

Potete annullare la pubblicazione delle cartelle da Brand Portal in modo rapido oppure pianificarle in un secondo momento. Per annullare la pubblicazione delle cartelle di risorse da Brand Portal:

1. Dall’interfaccia di AEM Assets nell’istanza di AEM Author, selezionate la cartella da annullare la pubblicazione.

   ![publish2bp-1](assets/publish2bp.png)

1. Dalla barra degli strumenti, fate clic su **Gestisci pubblicazione**.

1. **Annulla pubblicazione da Brand Portal**

   Per annullare rapidamente la pubblicazione della cartella desiderata da Brand Portal:

   1. Dalla barra degli strumenti, selezionate **Gestisci pubblicazione**.
   1. In **Azione** , selezionate **Annulla pubblicazione da Brand Portal**; in **Pianificazione** , selezionate **Ora** e fate clic su **Avanti.**
   1. Confermate la selezione nell&#39; **ambito** e fate clic su **Annulla pubblicazione dal portale** marchio.
   ![confirm-unpublish](assets/confirm-unpublish.png)

   **Annulla pubblicazione da Brand Portal in un secondo momento**

   Per pianificare la pubblicazione di una cartella da Brand Portal a una data e un’ora successive:

   1. Dalla barra degli strumenti, selezionate **Gestisci pubblicazione**.
   1. In **Azione** , selezionate **Annulla pubblicazione da Brand Portal** e, in **Pianificazione** , selezionate **Più tardi**.
   1. Selezionate una data **di** attivazione e specificate l’ora. Fai clic su **Avanti**.
   1. Conferma la selezione nell’ **ambito** e fai clic su **Avanti**.
   1. Specificate un titolo **** Flusso di lavoro in **Flussi di lavoro**. Fate clic su **Annulla pubblicazione più tardi.**

      ![flussi di lavoro non pubblicati](assets/unpublishworkflows.png)


>[!NOTE]
>
>La procedura per pubblicare/annullare la pubblicazione di una risorsa in/da Brand Portal è simile alla procedura corrispondente per una cartella.

