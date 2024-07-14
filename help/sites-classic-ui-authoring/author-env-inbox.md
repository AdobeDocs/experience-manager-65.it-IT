---
title: Casella in entrata
description: Puoi ricevere notifiche da varie aree dell’AEM, ad esempio notifiche su elementi di lavoro o attività che rappresentano azioni da eseguire sul contenuto della pagina.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 52ea2ca2-eb1c-4bed-b52d-feef37c6afd6
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: a28883778c5e8fb90cbbd0291ded17059ab2ba7e
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 1%

---

# Casella in entrata{#your-inbox}

Puoi ricevere notifiche da varie aree dell’AEM, ad esempio notifiche su elementi di lavoro o attività che rappresentano azioni da eseguire sul contenuto della pagina.

Queste notifiche vengono ricevute in due caselle in entrata, separate dal tipo di notifica:

* Nella sezione seguente viene descritta una casella in entrata in cui è possibile visualizzare le notifiche ricevute come risultato degli abbonamenti.
* Nel documento [Partecipazione ai flussi di lavoro](/help/sites-classic-ui-authoring/classic-workflows-participating.md) è descritta una casella in entrata specializzata per gli elementi del flusso di lavoro.

## Visualizzazione delle notifiche {#viewing-your-notifications}

Per visualizzare le notifiche:

1. Apri la casella in entrata delle notifiche: nella console **Siti Web**, fai clic sul pulsante utente in alto a destra e seleziona **Casella in entrata delle notifiche**.

   ![schermata_shot_2012-02-08at105226am](assets/screen_shot_2012-02-08at105226am.png)

   >[!NOTE]
   >
   >Puoi anche accedere alla console direttamente nel browser, ad esempio:
   >
   >
   >` https://<host>:<port>/libs/wcm/core/content/inbox.html`

1. Le notifiche sono elencate. Puoi intraprendere le azioni necessarie:

   * [Iscrizione alle notifiche](#subscribing-to-notifications)
   * [Elaborazione delle notifiche](#processing-your-notifications)

   ![chlimage_1-4](assets/chlimage_1-4.jpeg)

## Iscrizione alle notifiche {#subscribing-to-notifications}

Per iscriverti alle notifiche:

1. Apri la casella in entrata delle notifiche: nella console **Siti Web**, fai clic sul pulsante utente in alto a destra e seleziona **Casella in entrata delle notifiche**.

   ![schermata_shot_2012-02-08at105226am-1](assets/screen_shot_2012-02-08at105226am-1.png)

   >[!NOTE]
   >
   >Puoi anche accedere alla console direttamente nel browser, ad esempio:
   >
   >
   >`https://<host>:<port>/libs/wcm/core/content/inbox.html`

1. Fare clic su **Configura...** nell&#39;angolo superiore sinistro per aprire la finestra di dialogo di configurazione.

   ![schermata_shot_2012-02-08at111056am](assets/screen_shot_2012-02-08at111056am.png)

1. Seleziona il canale di notifica:

   * **Posta in arrivo**: le notifiche vengono visualizzate nella Posta in arrivo AEM.
   * **E-mail**: le notifiche vengono inviate tramite e-mail all&#39;indirizzo e-mail definito nel profilo utente.

   >[!NOTE]
   >
   >È necessario configurare alcune impostazioni per ricevere una notifica tramite e-mail. È inoltre possibile personalizzare il modello e-mail o aggiungere un modello e-mail per una nuova lingua. Consulta [Configurazione della notifica e-mail](/help/sites-administering/notification.md#configuringemailnotification) per configurare le notifiche e-mail in AEM.

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

   * Fai clic su **Aggiungi** per aggiungere una nuova riga alla tabella.
   * Fare clic sulla cella della tabella **Percorso** e immettere il percorso, ad esempio `/content/docs`.

   * Per ricevere una notifica per tutte le pagine appartenenti alla sottostruttura, impostare **Esatto?Da** a **No**.
Per ricevere una notifica solo per le azioni sulla pagina definita dal percorso, impostare **Exact?Da** a **Sì**.

   * Per consentire la regola, impostare **Rule** su **Allow**. Se impostato su **Nega**, la regola viene negata ma non rimossa e può essere consentita in un secondo momento.

   Per rimuovere una definizione, selezionare la riga facendo clic su una cella di tabella e fare clic su **Elimina**.

1. Fare clic su **OK** per salvare la configurazione.

## Elaborazione delle notifiche {#processing-your-notifications}

Se si è scelto di ricevere notifiche nella cartella Posta in arrivo AEM, la cartella Posta in arrivo viene riempita con le notifiche. Puoi [visualizzare le notifiche](#viewing-your-notifications), quindi selezionare le notifiche necessarie per:

* Accettarlo facendo clic su **Approve**: il valore nella colonna **Read** è impostato su **true**.

* Eliminarla facendo clic su **Elimina**.

![chlimage_1-5](assets/chlimage_1-5.jpeg)
