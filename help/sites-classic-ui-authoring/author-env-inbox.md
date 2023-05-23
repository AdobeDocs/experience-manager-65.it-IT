---
title: Casella in entrata
description: Puoi ricevere notifiche da varie aree dell’AEM, ad esempio notifiche su elementi di lavoro o attività che rappresentano azioni da eseguire sul contenuto della pagina.
uuid: e7ba9150-957d-4f84-a570-2f3d83792472
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: ce2a1475-49cf-43e6-bfb9-006884ce3881
docset: aem65
exl-id: 52ea2ca2-eb1c-4bed-b52d-feef37c6afd6
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 1%

---

# Casella in entrata{#your-inbox}

Puoi ricevere notifiche da varie aree dell’AEM, ad esempio notifiche su elementi di lavoro o attività che rappresentano azioni da eseguire sul contenuto della pagina.

Queste notifiche vengono ricevute in due caselle in entrata, separate dal tipo di notifica:

* Nella sezione seguente viene descritta una casella in entrata in cui è possibile visualizzare le notifiche ricevute come risultato degli abbonamenti.
* Una casella in entrata specializzata per gli elementi del flusso di lavoro è descritta in [Partecipazione ai flussi di lavoro](/help/sites-classic-ui-authoring/classic-workflows-participating.md) documento.

## Visualizzazione delle notifiche {#viewing-your-notifications}

Per visualizzare le notifiche:

1. Apri la casella in entrata delle notifiche: in **Siti Web** , fai clic sul pulsante utente nell’angolo in alto a destra e seleziona **Casella in entrata notifica**.

   ![screen_shot_2012-02-08at105226am](assets/screen_shot_2012-02-08at105226am.png)

   >[!NOTE]
   >
   >Puoi anche accedere alla console direttamente nel browser, ad esempio:
   >
   >
   >` https://<host>:<port>/libs/wcm/core/content/inbox.html`

1. Le notifiche verranno elencate. Puoi intraprendere le azioni necessarie:

   * [Iscrizione alle notifiche](#subscribing-to-notifications)
   * [Elaborazione delle notifiche](#processing-your-notifications)

   ![chlimage_1-4](assets/chlimage_1-4.jpeg)

## Iscrizione alle notifiche {#subscribing-to-notifications}

Per iscriverti alle notifiche:

1. Apri la casella in entrata delle notifiche: in **Siti Web** , fai clic sul pulsante utente nell’angolo in alto a destra e seleziona **Casella in entrata notifica**.

   ![screen_shot_2012-02-08at105226am-1](assets/screen_shot_2012-02-08at105226am-1.png)

   >[!NOTE]
   >
   >Puoi anche accedere alla console direttamente nel browser, ad esempio:
   >
   >
   >`https://<host>:<port>/libs/wcm/core/content/inbox.html`

1. Clic **Configura...** nell’angolo in alto a sinistra per aprire la finestra di dialogo di configurazione.

   ![screen_shot_2012-02-08at111056am](assets/screen_shot_2012-02-08at111056am.png)

1. Seleziona il canale di notifica:

   * **Casella in entrata**: le notifiche vengono visualizzate nella casella in entrata AEM.
   * **E-mail**: le notifiche verranno inviate tramite e-mail all’indirizzo e-mail definito nel profilo utente.

   >[!NOTE]
   >
   >È necessario configurare alcune impostazioni per ricevere una notifica tramite e-mail. È inoltre possibile personalizzare il modello e-mail o aggiungere un modello e-mail per una nuova lingua. Fare riferimento a [Configurazione delle notifiche e-mail](/help/sites-administering/notification.md#configuringemailnotification) per configurare le notifiche e-mail in AEM.

1. Seleziona le azioni di pagina per le quali inviare la notifica:

   * Attivato: quando una pagina è stata attivata.
   * Disattivato: quando una pagina è stata disattivata.
   * Eliminata (sindacazione): quando una pagina è stata eliminata-replicata, ovvero quando viene replicata un’azione di eliminazione eseguita su una pagina.
Quando una pagina viene eliminata o spostata, viene replicata automaticamente un’azione di eliminazione: la pagina viene eliminata nell’istanza di origine in cui è stata eseguita l’azione di eliminazione e nell’istanza di destinazione definita dagli agenti di replica.

   * Modificato: quando una pagina è stata modificata.
   * Creato: quando viene creata una pagina.
   * Eliminata: quando una pagina è stata eliminata tramite l’azione di eliminazione della pagina.
   * Rollout: quando viene eseguito il rollout di una pagina.

1. Definisci i percorsi delle pagine per le quali riceverai una notifica:

   * Clic **Aggiungi** per aggiungere una nuova riga alla tabella.
   * Fai clic su **Percorso** e immettere il percorso, ad esempio `/content/docs`.

   * Da notificare per tutte le pagine appartenenti alla sottostruttura, imposta **Esatto?** a **No**.
Per ricevere una notifica solo per le azioni sulla pagina definita dal percorso, imposta **Esatto?** a **Sì**.

   * Per consentire la regola, imposta **Regola** a **Consenti**. Se impostato su **Rifiuta**, la regola viene negata ma non rimossa e può essere consentita in un secondo momento.

   Per rimuovere una definizione, selezionare la riga facendo clic su una cella di tabella e fare clic su **Elimina**.

1. Clic **OK** per salvare la configurazione.

## Elaborazione delle notifiche {#processing-your-notifications}

Se hai scelto di ricevere le notifiche nella casella in entrata dell’AEM, questa si riempirà di notifiche. È possibile [visualizzare le notifiche](#viewing-your-notifications) quindi seleziona le notifiche richieste per:

* Approva facendo clic su **Approva**: il valore in **Letto** è impostata su **true**.

* Per eliminarlo, fai clic su **Elimina**.

![chlimage_1-5](assets/chlimage_1-5.jpeg)
