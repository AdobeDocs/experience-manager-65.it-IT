---
title: Creazione e gestione di revisioni per le risorse nei moduli
seo-title: Creating and managing reviews for assets in forms
description: La funzione Revisione è un meccanismo che consente a uno o più revisori di commentare una risorsa disponibile in un modulo.
seo-description: A Review is a mechanism that allows one or more reviewers to comment on an asset that is available in a form.
uuid: 45c7ff56-3fa8-4a0f-8597-05404e547282
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: d8c1c507-a6c4-44f5-be01-ee902bc28410
docset: aem65
feature: Adaptive Forms
exl-id: 9ca4fcd6-3eb0-4fc1-a09c-e4ad532bbed0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 0%

---

# Creazione e gestione di revisioni per le risorse nei moduli{#creating-and-managing-reviews-for-assets-in-forms}

## Recensione {#review}

La funzione Revisione è un meccanismo che consente a uno o più revisori di commentare una risorsa disponibile in un modulo.

## Impostazione di una revisione {#setting-up-a-review}

1. Passare alla scheda Forms e selezionare un modulo.
1. Se la risorsa non dispone di una revisione in corso, avvia una revisione ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) nella barra delle azioni. Fai clic su Avvia revisione ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) icona.
1. Inserite le seguenti informazioni:

   * Nome revisione: Obbligatorio, può contenere caratteri alfanumerici, trattini o caratteri di sottolineatura.
   * Descrizione della revisione: Facoltativo, descrizione dello scopo/contenuto da rivedere.
   * Termine di revisione: Facoltativo, la data in cui termina la revisione. Al termine della scadenza l&#39;attività viene visualizzata come &quot;Scaduto&quot;.
   * Revisori: Un minimo di uno è obbligatorio. Utilizzare la casella combinata per aggiungere revisori. La digitazione di un nome elenca tutti i nomi corrispondenti; selezionare un nome e fare clic su Aggiungi.

1. Compila tutti i dettagli rimanenti, quindi fai clic su Avvia.

### Azioni che si verificano quando viene impostata una revisione {#actions-that-occur-when-a-review-is-set-up}

Questa sezione descrive cosa accade quando viene creata o impostata una revisione.

1. Viene creata e assegnata una nuova attività di revisione all&#39;iniziatore della revisione.
1. A tutti i revisori viene assegnata un&#39;attività di revisione. L’attività viene visualizzata nella relativa sezione Notifiche. Un revisore può fare clic su una notifica oppure passare alla casella in entrata per visualizzare l’attività. Un revisore può fare clic per aprire l&#39;attività di revisione, visualizzare il modulo e iniziare ad aggiungere commenti.

   ![Avviso notifica revisore](assets/noti.png)

   Avviso notifica revisore

1. La casella dei commenti è disponibile per l’iniziatore e i revisori della risorsa. Altri possono visualizzare i commenti, ma non possono scrivere commenti.

## Gestione di una revisione {#managing-a-review}

>[!NOTE]
>
>È possibile modificare solo le revisioni in corso. Impossibile modificare le revisioni completate.

1. Passare alla scheda Forms e selezionare un modulo.

1. Se una risorsa è in corso di revisione e sei l’iniziatore della revisione, consulta Gestisci revisione ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png) nella barra delle azioni vengono visualizzate le icone. Solo l’iniziatore della revisione può gestire (aggiornare/terminare) la revisione.

   Fai clic su Gestisci revisione ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png)icona.

   Per gli utenti diversi dall&#39;iniziatore, l&#39;icona Gestisci revisione è disabilitata.

1. Viene visualizzata una schermata con le informazioni seguenti:

   * **Nome della revisione**: Impossibile modificare.

   * **Descrizione della revisione**: Disponibile per la modifica.

   * **Termine di revisione**: Disponibile per la modifica. È possibile modificare la scadenza in qualsiasi data e ora successive alla data e all’ora correnti.

   * **Revisori**: Disponibile per la modifica. È possibile aggiungere o rimuovere revisori. Se un&#39;attività è scaduta, è possibile aggiungere revisori solo dopo aver esteso la scadenza oltre la data corrente.

1. Modificare i campi necessari, quindi fare clic su Aggiorna.

   ![Rivedere lo stato aggiornato in Gestione attività](assets/tskmgr.png)

   Rivedere lo stato aggiornato in Gestione attività

1. Per terminare la revisione, fare clic su Fine.

### Azioni che si verificano quando una revisione viene modificata {#actions-that-occur-when-a-review-is-modified}

Questa sezione descrive cosa succede al termine della revisione / modifica:

1. Se la descrizione Revisione viene modificata, viene aggiornata l&#39;attività corrispondente dei revisori e dell&#39;iniziatore.
1. Se la scadenza di revisione viene modificata, l&#39;attività corrispondente per i revisori viene aggiornata con la nuova data.

1. Se un revisore viene rimosso:

   ![Rimozione di un revisore](assets/removeduser.png)

   Rimozione di un revisore

   1. Se incompleta, l&#39;attività assegnata viene terminata.
   1. Il revisore non può più commentare la risorsa.

1. Se viene aggiunto un revisore:

   ![Aggiunta di un revisore](assets/addedreviewer.png)

   Aggiunta di un revisore

   1. Viene creata e assegnata un&#39;attività di revisione al revisore appena aggiunto.
   1. Il revisore appena aggiunto può aggiungere commenti per la risorsa.

1. Al termine di una revisione:

   1. **Revisori**: Per ogni revisore, l&#39;attività incompleta relativa alla revisione viene terminata. L&#39;attività non viene più visualizzata come &quot;In sospeso&quot; nella sezione Notifiche del revisore.
   1. **Iniziatore**: L&#39;attività assegnata all&#39;iniziatore Revisione è contrassegnata come completata. L&#39;attività viene rimossa dalla sezione Notifica dell&#39;iniziatore della revisione.
   1. **Tutto**: La revisione viene visualizzata nella sezione Recensioni precedenti . Non è possibile aggiungere ulteriori osservazioni.
