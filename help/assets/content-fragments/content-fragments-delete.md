---
title: Frammenti di contenuto - Considerazioni sull’eliminazione
seo-title: Frammenti di contenuto - Considerazioni sull’eliminazione
description: Frammenti di contenuto - Considerazioni sull’eliminazione
seo-description: Frammenti di contenuto - Considerazioni sull’eliminazione
uuid: e7ac1809-159f-4d02-ad30-dc6c246e8a04
contentOwner: aheimoz
topic-tags: content-fragments
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: ec21237f-9186-49b4-8039-99df4db7c14a
docset: aem65
translation-type: tm+mt
source-git-commit: a430c4de89bde3b907d342106465d3b5a7c75cc8
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 12%

---


# Frammenti di contenuto - Considerazioni sull’eliminazione{#content-fragments-delete-considerations}

## Autorizzazioni - Elimina o Non eliminare {#permissions-delete-or-not-delete}

La possibilità di eliminare contenuti è potente, ma potenzialmente sensibile, e molti settori devono limitare e controllare la modalità di distribuzione di tali privilegi.

Per quanto riguarda l’eliminazione delle autorizzazioni, i frammenti di contenuto devono essere considerati a due livelli:

1. **Il frammento di contenuto come entità singola.**

   * **Caso** di utilizzo: Utente che deve modificare/aggiornare un frammento di contenuto  **ed eliminare un intero frammento**.
   * **Autorizzazioni**: L&#39;autorizzazione  [](/help/sites-administering/security.md#actions) Elimina può essere  [assegnata tramite Gestione](/help/sites-administering/security.md#managing-permissions) utente e/o gruppo.

1. **Più sottoentità che costituiscono un frammento di contenuto; ad esempio, varianti, nodi secondari.**

   Il funzionamento di base dell’editor dei frammenti di contenuto richiede che tali sottoelementi transitori possano essere eliminati. Ad esempio, durante la manipolazione delle variazioni; anche durante la modifica dei metadati o la gestione del contenuto associato.

   * **Caso** di utilizzo: Un utente che deve modificare/aggiornare un frammento di contenuto,  **senza la possibilità di eliminare un intero frammento**.
   * **Autorizzazioni**: Consultate  [Autorizzazioni necessarie solo](/help/assets/content-fragments/content-fragments-delete.md#permissions-required-for-editor-functionality-only) per la funzionalità dell’editor.

>[!NOTE]
>
>Se un utente non dispone di autorizzazioni [Elimina](/help/sites-administering/security.md#actions), l&#39;editor dei frammenti di contenuto funziona in modalità *sola lettura*.

>[!NOTE]
>
>Vedere anche [Come controllare le operazioni di gestione utenti in AEM](/help/sites-administering/audit-user-management-operations.md).

## Autorizzazioni necessarie per la sola funzionalità dell&#39;editor {#permissions-required-for-editor-functionality-only}

Dovrai assegnare autorizzazioni specifiche agli utenti che necessitano di modificare/aggiornare un frammento di contenuto, **ma a cui non vuoi consentire di eliminare un intero frammento**, poiché il funzionamento di base dell’Editor frammento di contenuto richiede l’eliminazione di elementi secondari transitori.

Ad esempio, durante la manipolazione delle variazioni; anche durante la modifica dei metadati o la gestione del contenuto associato.

>[!NOTE]
>
>Le autorizzazioni di eliminazione, necessarie per modificare/aggiornare un frammento di contenuto, sono incluse nell&#39;autorizzazione di eliminazione [assegnata tramite Gestione utente e/o gruppo](/help/sites-administering/security.md#managing-permissions).

Le autorizzazioni necessarie per modificare/aggiornare un frammento devono essere applicate al nodo contenente il frammento di contenuto o a un nodo principale appropriato (a qualsiasi livello in `/content/dam`). Quando vengono assegnate a tale nodo padre, le autorizzazioni vengono applicate a tutti i nodi all&#39;interno di tale ramo.

Ad esempio, una cartella contenente tutti i frammenti di contenuto, come:

* `/content/dam/contentfragments`

>[!CAUTION]
>
>È inoltre possibile impostare le autorizzazioni su `/content/dam`, in quanto tutti i frammenti di contenuto sono memorizzati qui.
>
>Tuttavia, questa azione applica le stesse autorizzazioni di eliminazione anche agli altri tipi di risorse *all*.

I prerequisiti per consentire a un utente e/o gruppo specifico di modificare/aggiornare un frammento di contenuto sono:

>[!NOTE]
>
>Questo elenco mostra tutti i privilegi richiesti, non solo quelli di eliminazione.

* Per i nodi o le cartelle dei frammenti di contenuto:

   * `jcr:addChildNodes`, `jcr:modifyProperties`

* Per il nodo `jcr:content`di tutti i frammenti di contenuto:

   * `jcr:addChildNodes`,  `jcr:modifyProperties` e  `jcr:removeChildNodes`

* Per tutti i nodi sotto `jcr:content` di tutti i frammenti di contenuto:

   * `jcr:addChildNodes`,  `jcr:modifyProperties` e  `jcr:removeChildNodes`,  `jcr:removeNode`

Questi privilegi `remove` devono essere [amministrati tramite elenchi di controllo di accesso, all&#39;interno di CRXDE Lite](/help/sites-administering/user-group-ac-admin.md#access-right-management).

I privilegi `add` e `modify` possono essere amministrati anche in CRXDE Lite o mediante la console Gestione utente.

Ad esempio, la definizione dei privilegi `remove` per un gruppo `content-authors-no-delete`:

![cf-delete-03](assets/cf-delete-03.png)

