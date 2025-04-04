---
title: Modificare l'aspetto (HBS)
description: Scopri come modificare l’aspetto (HBS) modificando gli script HBS.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 27e1bff3-385e-4ced-87af-54044b7e8812
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# Modificare l&#39;aspetto (HBS) {#alter-the-appearance-hbs}

Ora che i componenti per il sistema di commenti personalizzato nella directory dell’applicazione (/apps) sono presenti, con una risorsa SuperType che fa riferimento al sistema di commenti predefinito e con il modello/vista personalizzato registrato, puoi modificare l’implementazione.

Per una semplice dimostrazione, una funzione visiva, l’avatar mostrato dall’utente connesso che pubblica un commento, viene rimossa.

>[!NOTE]
>
>Per utilizzare l’estensione, l’istanza del sistema di commenti in un sito web interessato (/content) deve impostare resourceType come sistema di commenti personalizzato.

## Modificare gli script HBS {#modify-the-hbs-scripts}

Utilizzo di [CRXDE Liti](/help/sites-developing/developing-with-crxde-lite.md):

* Apri [/apps/custom/components/comments/comment/**comment.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment/comment.hbs)

   * Commenta il tag che include l&#39;avatar per un post di commento (~ riga 21):

     ```
       <!--
        <<img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
        -->
     ```

* Apri [/apps/custom/components/comments/**comments.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comments.hbs)

   * Commenta il tag che include l&#39;avatar per la voce di commento successiva (~ riga 44):

     ```
       <!--
        <img class="scf-composer-avatar" src="{{loggedInUser.avatarUrl}}"></img>
        -->
     ```

* Seleziona **Salva tutto**

### Replica app personalizzata {#replicate-custom-app}

Dopo la modifica dell’applicazione, è necessario replicare nuovamente il componente personalizzato.

Un modo per farlo è:

* Dal menu principale

   * Selezionare **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Replica]**.
   * Selezionare **[!UICONTROL Attiva albero]**.
   * Imposta `Start Path` su `/apps/custom`.
   * Deseleziona **[!UICONTROL Solo Modificato]**.
   * Selezionare il pulsante **[!UICONTROL Attiva]**.

### Visualizza commento modificato nella pagina di esempio pubblicata {#view-modified-comment-on-published-sample-page}

[Continuando l&#39;esperienza](/help/communities/extend-sample-page.md#publish-sample-page) sull&#39;istanza di pubblicazione, ancora connessa con lo stesso utente, ora è possibile aggiornare la pagina nell&#39;ambiente di pubblicazione per visualizzare la modifica per rimuovere l&#39;avatar:

![view-modified-content](assets/view-modified-content.png)

### Pacchetto estensione commento di esempio {#sample-comment-extension-package}

In allegato è presente un pacchetto dell’applicazione per commenti personalizzati creata in questa esercitazione.

[Ottieni file](assets/sample-comment-extension-6-1-fp3.zip)
