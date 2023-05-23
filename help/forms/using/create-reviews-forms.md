---
title: Creazione e gestione delle revisioni delle risorse nei moduli
seo-title: Creating and managing reviews for assets in forms
description: Una revisione è un meccanismo che consente a uno o più revisori di aggiungere commenti su una risorsa disponibile in un modulo.
seo-description: A Review is a mechanism that allows one or more reviewers to comment on an asset that is available in a form.
uuid: 45c7ff56-3fa8-4a0f-8597-05404e547282
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: d8c1c507-a6c4-44f5-be01-ee902bc28410
docset: aem65
feature: Adaptive Forms
exl-id: 9ca4fcd6-3eb0-4fc1-a09c-e4ad532bbed0
source-git-commit: 4edfc51227607b4fb3ee4b97443d2040015b6a65
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# Creazione e gestione delle revisioni delle risorse nei moduli{#creating-and-managing-reviews-for-assets-in-forms}

## Recensione {#review}

Una revisione è un meccanismo che consente a uno o più revisori di aggiungere commenti su una risorsa disponibile in un modulo.

## Impostazione di una revisione {#setting-up-a-review}

1. Passa alla scheda Forms e seleziona un modulo.
1. Se per la risorsa non è in corso una revisione, viene avviata una revisione ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) nella barra delle azioni. Fai clic su Avvia revisione ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) icona.
1. Immettere le seguenti informazioni:

   * Nome revisione: obbligatorio, può contenere caratteri alfanumerici, trattini o trattini bassi.
   * Descrizione revisione: facoltativo, descrizione dello scopo/contenuto da rivedere.
   * Scadenza revisione: facoltativo, la data in cui termina la revisione. Se la scadenza è stata superata, l’attività viene visualizzata come &quot;Scaduto&quot;.
   * Revisori: almeno uno è obbligatorio. Utilizza la casella combinata per aggiungere revisori. Se si digita un nome, vengono elencati tutti i nomi corrispondenti; selezionare un nome e fare clic su Aggiungi.

1. Immettere tutti i dettagli rimanenti e quindi fare clic su Avvia.

### Azioni che si verificano quando viene impostata una revisione {#actions-that-occur-when-a-review-is-set-up}

Questa sezione descrive cosa accade quando si crea o si configura una revisione.

1. Viene creata una nuova attività di revisione assegnata all&#39;iniziatore della revisione.
1. A tutti i revisori viene assegnata un&#39;attività di revisione. L’attività viene visualizzata nella sezione Notifiche. Un revisore può fare clic su una notifica o passare alla casella in entrata per visualizzare l&#39;attività. Un revisore può fare clic per aprire l&#39;attività di revisione, visualizzare il modulo e iniziare ad aggiungere commenti.

   ![Avviso di notifica revisore](assets/noti.png)

   Avviso di notifica revisore

1. La casella dei commenti è disponibile per l’iniziatore e i revisori della risorsa. Altri possono visualizzare i commenti, ma non possono scriverli.

## Gestione di una revisione {#managing-a-review}

>[!NOTE]
>
>È possibile modificare solo le revisioni in corso. Le recensioni completate non possono essere modificate.

1. Passa alla scheda Forms e seleziona un modulo.

1. Se per una risorsa è in corso una revisione e l’utente è l’iniziatore della revisione, viene visualizzata l’opzione Gestisci revisione ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) nella barra delle azioni. Solo l&#39;iniziatore di revisione può gestire (aggiornare/terminare) la revisione.

   Fai clic sul pulsante Gestisci revisione ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png)icona.

   Per gli utenti diversi dall&#39;iniziatore, l&#39;icona Gestisci revisione è disabilitata.

1. Viene visualizzata una schermata con le seguenti informazioni:

   * **Nome revisione**: impossibile modificarlo.

   * **Descrizione revisione**: disponibile per la modifica.

   * **Scadenza revisione**: disponibile per la modifica. È possibile modificare la scadenza in qualsiasi data e ora oltre la data e l&#39;ora correnti.

   * **Revisori**: disponibile per la modifica. È possibile aggiungere o rimuovere revisori. Se un&#39;attività è scaduta, è possibile aggiungere revisori solo dopo aver esteso la scadenza oltre la data corrente.

1. Per terminare la revisione, fare clic su Fine.

### Azioni che si verificano quando viene modificata una revisione {#actions-that-occur-when-a-review-is-modified}

Questa sezione descrive cosa accade alla fine della revisione o alla modifica:

1. Se la descrizione Revisione viene modificata, l&#39;attività corrispondente dei revisori e dell&#39;iniziatore viene aggiornata.
1. Se la scadenza della revisione viene modificata, l&#39;attività corrispondente per i revisori viene aggiornata con la nuova data.

1. Se un revisore viene rimosso:

   ![Rimozione di un revisore](assets/removeduser.png)

   Rimozione di un revisore

   1. Se incompleta, l&#39;attività assegnata viene terminata.
   1. Il revisore non può più aggiungere commenti alla risorsa.

1. Se viene aggiunto un revisore:

   ![Aggiunta di un revisore](assets/addedreviewer.png)

   Aggiunta di un revisore

   1. Viene creata un&#39;attività di revisione assegnata al revisore appena aggiunto.
   1. Il revisore appena aggiunto può aggiungere commenti per la risorsa.

1. Al termine di una revisione:

   1. **Revisori**: per ogni revisore, l’attività incompleta correlata alla revisione viene terminata. L’attività non viene più visualizzata come &quot;In sospeso&quot; nella sezione Notifiche del revisore.
   1. **Iniziatore**: l&#39;attività assegnata all&#39;iniziatore di revisione è contrassegnata come completata. L&#39;attività viene rimossa dalla sezione Notifica dell&#39;iniziatore di revisione.
   1. **Tutti**: la revisione viene visualizzata nella sezione Revisioni precedenti. Non è possibile aggiungere altri commenti.
