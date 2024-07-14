---
title: Creazione e gestione delle revisioni nei moduli
description: Una revisione è un meccanismo che consente a uno o più revisori di aggiungere commenti a un modulo.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
docset: aem65
feature: Foundation Components
exl-id: 9ca4fcd6-3eb0-4fc1-a09c-e4ad532bbed0
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 8a77756e8ba771c8de9950c2323bef8f23cc59b4
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 2%

---

# Creazione e gestione delle revisioni ai moduli{#creating-and-managing-reviews-to-forms}

<span class="preview"> Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-reviews-forms.html?lang=it) |
| AEM 6.5 | Questo articolo |

## Rivedi {#review}

Una revisione è un meccanismo che consente a uno o più revisori di aggiungere commenti ai moduli.

## Impostazione di una revisione {#setting-up-a-review}

1. Passare al browser Moduli e selezionare un modulo da rivedere.
1. Se per il modulo non è in corso una revisione, nella barra delle azioni verrà visualizzata l&#39;icona **Avvia revisione** ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png). Fai clic sull&#39;icona **Avvia revisione** ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png).
1. Immettere le seguenti informazioni:

   * **Titolo**: obbligatorio, può contenere caratteri alfanumerici, trattini e trattini bassi.
   * **Descrizione**: facoltativo, descrizione dello scopo/contenuto da rivedere.
   * **Scadenza**: facoltativo, la data in cui termina la revisione. Se la scadenza è stata superata, l’attività viene visualizzata come &quot;Scaduto&quot;.
   * **Nome revisore**: almeno uno è obbligatorio. utilizzare la casella combinata per aggiungere revisori, digitando un elenco dei nomi di tutti i nomi corrispondenti; selezionare un nome e fare clic su **Aggiungi**. Nella sezione successiva della scheda **Revisori** viene visualizzato il nome di tutti i revisori.

1. Fai clic su **Inizio** per avviare una revisione.

   >[!NOTE]
   >
   >* L’amministratore può accedere a tutti i gruppi associati agli utenti del modulo.
   >* Il gruppo Utenti del servizio non è disponibile per la selezione per la revisione.

### Azioni che si verificano quando viene impostata una revisione {#actions-that-occur-when-a-review-is-set-up}

Questa sezione descrive cosa accade quando si crea o si configura una revisione.

1. Viene creata una nuova attività di revisione assegnata al revisore selezionato.
1. A tutti i revisori viene assegnata un&#39;attività di revisione. L’attività viene visualizzata nella sezione Notifiche. Un revisore può fare clic su una notifica o passare alla casella in entrata per visualizzare l&#39;attività. Un revisore può fare clic per aprire l&#39;attività di revisione, visualizzare il modulo e iniziare ad aggiungere commenti.

   ![Avviso di notifica revisore](assets/review-notification-img.png)

   Avviso di notifica revisore

1. La casella dei commenti è disponibile per i revisori del modulo. Altri possono leggere i commenti ma non aggiungerne altri.

## Gestione di una revisione {#managing-a-review}

>[!NOTE]
>
>* È possibile modificare solo le revisioni in corso.
>* Le recensioni completate non possono essere modificate.

1. Passare alla scheda Moduli e selezionare un modulo.

1. Se per un modulo è in corso una revisione e l&#39;utente è l&#39;iniziatore della revisione, nella barra delle azioni verrà visualizzata l&#39;icona **Gestisci revisione** ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png). Solo l&#39;iniziatore di revisione può gestire (aggiornare/terminare) la revisione.

   Fai clic sull&#39;icona **Gestisci revisione** ![aem6forms_review_chat_comment](assets/aem6forms_review_chat_comment.png).

   Per gli utenti diversi dall&#39;iniziatore, l&#39;icona Gestisci revisione è disabilitata.

1. Ora viene visualizzata una schermata con le seguenti informazioni:

   * **Nome revisione**: impossibile modificarlo.

   * **Descrizione revisione**: disponibile per la modifica.

   * **Scadenza revisione**: disponibile per la modifica. È possibile modificare la scadenza in qualsiasi data e ora oltre la data e l&#39;ora correnti.

   * **Revisori**: disponibile per la modifica. È possibile aggiungere o rimuovere revisori. Se un&#39;attività è scaduta, è possibile aggiungere revisori solo dopo aver esteso la scadenza oltre la data corrente.

1. Per terminare la revisione, fare clic su **Fine**.

### Azioni che si verificano quando viene modificata una revisione {#actions-that-occur-when-a-review-is-modified}

Questa sezione descrive cosa accade il **aggiornamento/fine revisione**:

1. Se la descrizione della revisione viene modificata, l&#39;attività corrispondente dei revisori e dell&#39;iniziatore viene aggiornata.
1. Se la scadenza della revisione viene modificata, l&#39;attività corrispondente per i revisori viene aggiornata con la nuova data.

1. Se un revisore viene rimosso:

   ![Rimozione di un revisore](assets/removeduser.png)

   Rimozione di un revisore

   1. Se incompleta, l&#39;attività assegnata viene terminata.
   1. Il revisore non può più aggiungere commenti al modulo.

1. Se viene aggiunto un revisore:

   ![Aggiunta di un revisore](assets/addedreviewer.png)

   Aggiunta di un revisore

   1. Viene creata un&#39;attività di revisione assegnata al revisore appena aggiunto.
   1. Il revisore appena aggiunto può aggiungere commenti sul modulo.

1. Al termine di una revisione:

   1. **Revisori**: per ogni revisore, l&#39;attività incompleta correlata alla revisione viene terminata. L’attività non viene più visualizzata come &quot;In sospeso&quot; nella sezione Notifiche del revisore.
   1. **Iniziatore**: l&#39;attività assegnata all&#39;iniziatore di revisione è contrassegnata come completata. L&#39;attività viene rimossa dalla sezione Notifica dell&#39;iniziatore di revisione.
   1. **Tutti**: la revisione viene visualizzata nella sezione Revisioni precedenti. Non è possibile aggiungere altri commenti.

   ![revisione completata](assets/review-complete-imgg.png)
