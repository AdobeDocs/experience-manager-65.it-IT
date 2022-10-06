---
title: Modificare l’aspetto
seo-title: Alter the Appearance
description: Modificare lo script
seo-description: Modify the script
uuid: 30555b9f-da29-4115-9ed5-25f80a247bd6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: c9d31ed8-c105-453b-bd3c-4660dfd81272
docset: aem65
exl-id: cb8f6967-216c-46d3-a7ba-068b0f5e3b94
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%

---

# Modificare l’aspetto {#alter-the-appearance}

## Modificare lo script {#modify-the-script}

Lo script comment.hbs è responsabile della creazione del HTML generale per ogni commento.

Per non visualizzare l&#39;avatar accanto a ciascun commento pubblicato:

1. Copia `comment.hbs`da `libs`a `apps`

   1. Seleziona `/libs/social/commons/components/hbs/comments/comment/comment.hbs`
   1. Seleziona **[!UICONTROL Copia]**
   1. Seleziona `/apps/social/commons/components/hbs/comments/comment`
   1. Seleziona **[!UICONTROL Incolla]**

1. Apri la sovrapposizione `comment.hbs`

   * Fare doppio clic sul nodo `comment.hbs` in `/apps/social/commons/components/hbs/comments/comment folder`

1. Trova le seguenti righe ed eliminale o commenta:

```xml
  <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

Eliminare le linee o circondarle con `<!--` e `-->` per commentarli. Inoltre, i caratteri &#39;xxx&#39; vengono aggiunti come indicatore visivo di dove sarebbe stato l&#39;avatar.

```xml
   xxx
   <!-- do not display avatar with comment
    <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

### Replicare la sovrapposizione {#replicate-the-overlay}

Invia il componente commenti sovrapposti all’istanza di pubblicazione utilizzando lo strumento di replica.

>[!NOTE]
>
>Una forma di replica più solida sarebbe quella di creare un pacchetto in Gestione pacchetti e [attivare](/help/sites-administering/package-manager.md#replicating-packages) . Un pacchetto può essere esportato e archiviato.

Dalla navigazione globale, seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Distribuzione]** > **[!UICONTROL Replica]** e fai clic su **[!UICONTROL Attiva albero]**.

Per Percorso iniziale immetti `/apps/social/commons` e seleziona **[!UICONTROL Attiva]**.

![verify-content-template](assets/verify-content-template.png)

### Visualizza risultati {#view-results}

Se accedi all’istanza di pubblicazione come amministratore, ad esempio https://localhost:4503/crx/de come amministratore/amministratore, puoi verificare che i componenti sovrapposti siano presenti.

Se disconnetti e riaccedi come `aaron.mcdonald@mailinator.com/password` e aggiorna la pagina, noterai che il commento pubblicato non viene più visualizzato con un avatar, ma viene visualizzato un semplice &#39;xxx&#39;.

![create-template-component](assets/create-template-component.png)
