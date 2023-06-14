---
title: Modificare l'aspetto
description: Modificare lo script
uuid: 30555b9f-da29-4115-9ed5-25f80a247bd6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: c9d31ed8-c105-453b-bd3c-4660dfd81272
docset: aem65
exl-id: cb8f6967-216c-46d3-a7ba-068b0f5e3b94
source-git-commit: 78c584db8c35ea809048580fe5b440a0b73c8eea
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# Modificare l&#39;aspetto {#alter-the-appearance}

## Modificare lo script {#modify-the-script}

Lo script comment.hbs è responsabile della creazione del HTML complessivo di ogni commento.

Per non mostrare l&#39;avatar accanto a ogni commento pubblicato:

1. Copia `comment.hbs`da `libs`a `apps`

   1. Seleziona `/libs/social/commons/components/hbs/comments/comment/comment.hbs`
   1. Seleziona **[!UICONTROL Copia]**
   1. Seleziona `/apps/social/commons/components/hbs/comments/comment`
   1. Seleziona **[!UICONTROL Incolla]**

1. Apri la sovrapposizione `comment.hbs`

   * Doppio clic sul nodo `comment.hbs` in `/apps/social/commons/components/hbs/comments/comment folder`

1. Trova le seguenti righe ed eliminale o aggiungendovi un commento:

```xml
  <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

Eliminare le linee o circondarle con `<!--` e `-->` quindi li commenta. Inoltre, i caratteri &quot;xxx&quot; vengono aggiunti come indicatore visivo di dove sarebbe stato l’avatar.

```xml
   xxx
   <!-- do not display avatar with comment
    <aside class="scf-comment-author">
        <img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
```

### Replica la sovrapposizione {#replicate-the-overlay}

Invia il componente dei commenti sovrapposti all’istanza di pubblicazione utilizzando lo strumento di replica.

>[!NOTE]
>
>Una forma più solida di replica consiste nel creare un pacchetto in Gestione pacchetti e [attivare](/help/sites-administering/package-manager.md#replicating-packages) ... Un pacchetto può essere esportato e archiviato.

Dalla navigazione globale, seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Distribuzione]** > **[!UICONTROL Replica]** e fai clic su **[!UICONTROL Attiva albero]**.

Per il percorso iniziale, immetti `/apps/social/commons` e seleziona **[!UICONTROL Attiva]**.

![verify-content-template](assets/verify-content-template.png)

### Visualizza risultati {#view-results}

Se accedi all’istanza Publish come amministratore, ad esempio https://localhost:4503/crx/de come amministratore/amministratore, puoi verificare che i componenti sovrapposti siano presenti.

Se ci si disconnette e si accede come `aaron.mcdonald@mailinator.com/password` e aggiorna la pagina, osserva che un avatar non viene visualizzato con il commento pubblicato. Viene invece visualizzato un semplice &quot;xxx&quot;.

![create-template-component](assets/create-template-component.png)
