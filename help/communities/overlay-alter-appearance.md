---
title: Modifica dell'aspetto
seo-title: Modifica dell'aspetto
description: Modificare lo script
seo-description: Modificare lo script
uuid: 30555b9f-da29-4115-9ed5-25f80a247bd6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: c9d31ed8-c105-453b-bd3c-4660dfd81272
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# Modifica dell&#39;aspetto {#alter-the-appearance}

## Modificare lo script {#modify-the-script}

Lo script comment.hbs è responsabile della creazione dell&#39;HTML complessivo per ciascun commento.

Per non visualizzare l&#39;avatar accanto a ciascun commento pubblicato:

1. Copiare `comment.hbs`da `libs`a `apps`

   1. Seleziona `/libs/social/commons/components/hbs/comments/comment/comment.hbs`
   1. Selezionare **[!UICONTROL Copia]**
   1. Seleziona `/apps/social/commons/components/hbs/comments/comment`
   1. Selezionare **[!UICONTROL Incolla]**

1. Aprire la sovrapposizione `comment.hbs`

   * Fare doppio clic sul nodo `comment.hbs` in `/apps/social/commons/components/hbs/comments/comment folder`

1. Trovate le righe seguenti ed eliminatele o aggiungetele un commento:

```xml
  <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

Eliminare le righe o circondarle con `<!--` e `-->` per escluderle. Inoltre, i caratteri &#39;xxx&#39; vengono aggiunti come indicatore visivo del punto in cui l&#39;avatar sarebbe stato.

```xml
   xxx
   <!-- do not display avatar with comment
    <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

### Replicare la sovrapposizione {#replicate-the-overlay}

Inviate il componente dei commenti sovrapposti all’istanza di pubblicazione utilizzando lo strumento di replica.

>[!NOTE]
>
>Una replica più affidabile sarebbe quella di creare un pacchetto in Gestione pacchetti e [attivarlo](/help/sites-administering/package-manager.md#replicating-packages). Un pacchetto può essere esportato e archiviato.

Dalla navigazione globale, selezionare **[!UICONTROL Strumenti]** > **[!UICONTROL Distribuzione]** > **[!UICONTROL Replica]** e fare clic su **[!UICONTROL Attiva albero]**.

Per Percorso iniziale, immettere `/apps/social/commons` e selezionare **[!UICONTROL Attiva]**.

![verify-content-template](assets/verify-content-template.png)

### Visualizza risultati {#view-results}

Se accedete all’istanza di pubblicazione come amministratore, ad esempio https://localhost:4503/crx/de come amministratore/amministratore, potete verificare che i componenti sovrapposti siano presenti.

Se effettuate il logout e accedete nuovamente come `aaron.mcdonald@mailinator.com/password` e aggiornate la pagina, il commento pubblicato non viene più visualizzato con un avatar, ma viene visualizzato un semplice &#39;xxx&#39;.

![create-template-component](assets/create-template-component.png)

