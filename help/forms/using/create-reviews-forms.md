---
title: Creazione e gestione di revisioni per le risorse nei moduli
seo-title: Creazione e gestione di revisioni per le risorse nei moduli
description: 'Una revisione è un meccanismo che consente a uno o più revisori di inserire commenti su una risorsa disponibile in un modulo. '
seo-description: 'Una revisione è un meccanismo che consente a uno o più revisori di inserire commenti su una risorsa disponibile in un modulo. '
uuid: 45c7ff56-3fa8-4a0f-8597-05404e547282
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: d8c1c507-a6c4-44f5-be01-ee902bc28410
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 0%

---


# Creazione e gestione di revisioni per le risorse nei moduli{#creating-and-managing-reviews-for-assets-in-forms}

## Recensione {#review}

Una revisione è un meccanismo che consente a uno o più revisori di inserire commenti su una risorsa disponibile in un modulo.

## Impostazione di una revisione {#setting-up-a-review}

1. Passare alla scheda Forms e selezionare un modulo.
1. Se la risorsa non dispone di una revisione in corso, nella barra delle azioni viene visualizzata l&#39;icona Avvia revisione ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png). Fare clic sull&#39;icona Avvia revisione ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png).
1. Inserite le seguenti informazioni:

   * Nome revisione: Obbligatorio, può contenere caratteri alfanumerici, trattini o caratteri di sottolineatura.
   * Descrizione revisione: Facoltativo, descrizione dello scopo/contenuto da rivedere.
   * Termine di revisione: Facoltativo, la data in cui termina la revisione. Una volta trascorsa la scadenza, l&#39;attività viene visualizzata come &quot;scaduta&quot;.
   * Revisori: Almeno uno è obbligatorio. Utilizzate la casella combinata per aggiungere dei revisori. La digitazione di un nome elenca tutti i nomi corrispondenti; selezionate un nome e fate clic su Aggiungi.

1. Compilate tutti i dettagli rimanenti, quindi fate clic su Avvia.

### Azioni che si verificano quando viene impostata una revisione {#actions-that-occur-when-a-review-is-set-up}

Questa sezione descrive cosa accade quando viene creata o impostata una revisione.

1. Viene creata una nuova attività di revisione che viene assegnata all&#39;iniziatore della revisione.
1. A tutti i revisori viene assegnata un&#39;attività di revisione. L&#39;attività viene visualizzata nella sezione Notifiche. Un revisore può fare clic su una notifica oppure passare alla casella in entrata per visualizzare l&#39;attività. Un revisore può fare clic per aprire l&#39;attività di revisione, visualizzare il modulo e iniziare ad aggiungere commenti.

   ![Avviso notifica revisore](assets/noti.png)

   Avviso notifica revisore

1. La casella dei commenti è disponibile per gli iniziatori e i revisori della risorsa. Altri possono visualizzare i commenti, ma non scrivere commenti.

## Gestione di una revisione {#managing-a-review}

>[!NOTE]
>
>È possibile modificare solo le revisioni in corso. Le revisioni complete non possono essere modificate.

1. Passare alla scheda Forms e selezionare un modulo.

1. Se una risorsa dispone di una revisione in corso e l&#39;utente è l&#39;iniziatore della revisione, nella barra delle azioni viene visualizzata l&#39;icona Gestisci revisione ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png). Solo l&#39;iniziatore della revisione può gestire (aggiornare/terminare) la revisione.

   Fare clic sull&#39;icona Gestisci revisione ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png).

   Per gli utenti diversi dall&#39;iniziatore, l&#39;icona Gestisci revisione è disabilitata.

1. Viene visualizzata una schermata con le informazioni seguenti:

   * **Nome** revisione: Impossibile modificare.

   * **Descrizione** revisione: Disponibile per la modifica.

   * **Termine** revisione: Disponibile per la modifica. È possibile modificare la scadenza in qualsiasi data e ora oltre la data e l&#39;ora correnti.

   * **Revisori**: Disponibile per la modifica. Potete aggiungere o rimuovere i revisori. Se un&#39;attività è scaduta, potete aggiungere i revisori solo dopo aver prorogato la scadenza oltre la data corrente.

1. Modificate i campi necessari, quindi fate clic su Aggiorna.

   ![Rivedere lo stato aggiornato in Task Manager](assets/tskmgr.png)

   Rivedere lo stato aggiornato in Task Manager

1. Per terminare la revisione, fare clic su Fine.

### Azioni che si verificano quando una revisione viene modificata {#actions-that-occur-when-a-review-is-modified}

Questa sezione descrive cosa accade in Rivedi fine / modifica:

1. Se la descrizione Review viene modificata, viene aggiornata l&#39;attività corrispondente dei revisori e dell&#39;iniziatore.
1. Se la scadenza Rivedi viene modificata, l&#39;attività corrispondente per i revisori viene aggiornata con la nuova data.

1. Se un revisore viene rimosso:

   ![Rimozione di un revisore](assets/removeduser.png)

   Rimozione di un revisore

   1. Se incompleto, l&#39;attività assegnata viene terminata.
   1. Il revisore non può più commentare la risorsa.

1. Se viene aggiunto un revisore:

   ![Aggiunta di un revisore](assets/addedreviewer.png)

   Aggiunta di un revisore

   1. Un&#39;attività di revisione viene creata e assegnata al nuovo revisore aggiunto.
   1. Il revisore aggiunto di recente può aggiungere commenti alla risorsa.

1. Al termine della revisione:

   1. **Revisori**: Per ciascun revisore, l&#39;attività incompleta relativa alla revisione viene terminata. L&#39;attività non viene più visualizzata come &quot;In sospeso&quot; nella sezione Notifiche del revisore.
   1. **Iniziatore**: L&#39;attività assegnata all&#39;iniziatore revisione è contrassegnata come completata. L&#39;attività viene rimossa dalla sezione Notifica dell&#39;iniziatore della revisione.
   1. **Tutti**: La revisione viene visualizzata nella sezione Recensioni precedenti. Non è possibile aggiungere ulteriori commenti.

