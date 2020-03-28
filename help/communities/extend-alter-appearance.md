---
title: Modifica dell'aspetto (HBS)
seo-title: Modifica dell'aspetto
description: Modificare gli script HBS
seo-description: Modificare gli script HBS
uuid: cff24505-dbb3-4312-9b1b-c1693b8d1c98
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e0da09b3-725d-4ed1-9273-2532132f6918
docset: aem65
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# Modifica dell&#39;aspetto (HBS) {#alter-the-appearance-hbs}

Ora che i componenti per il sistema di commenti personalizzati nella directory dell&#39;applicazione (/apps) sono già presenti, con un resourceSuperType che fa riferimento al sistema di commenti predefinito e il modello/vista personalizzato registrato, è possibile modificare l&#39;implementazione.

Per una semplice dimostrazione, viene rimossa una funzione visiva, l’avatar mostrato dall’utente che ha effettuato l’accesso e che ha pubblicato un commento.

>[!NOTE]
>
>Per utilizzare l’estensione, l’istanza del sistema di commenti in un sito Web da influenzare (/content) deve impostare resourceType come sistema di commenti personalizzato.

## Modificare gli script HBS {#modify-the-hbs-scripts}

Utilizzo di [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* Apri [/app/custom/components/comments/comment/**comment.hbs **](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment/comment.hbs)

   * commentare il tag che include l&#39;avatar per un post di commento (~ riga 21):

      ```
      <!--
       <<img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
       -->
      ```

* Apri [/app/custom/components/comments/**comments.hbs **](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comments.hbs)

   * commentare il tag che include l&#39;avatar per la voce di commento successiva (~ riga 44):

      ```
      <!--
       <img class="scf-composer-avatar" src="{{loggedInUser.avatarUrl}}"></img>
       -->
      ```

* Seleziona **Salva tutto**

### Replica app personalizzata {#replicate-custom-app}

Dopo che l’applicazione è stata modificata, è necessario replicare nuovamente il componente personalizzato.

Un modo per farlo è

* Dal menu principale

   * selezionare **Strumenti > Operazioni > Replica**
   * select `Activate Tree`
   * set `Start Path`: to `/apps/custom`
   * deselect `Only Modified`
   * pulsante `Activate`di selezione

### Visualizza commento modificato sulla pagina di esempio pubblicata {#view-modified-comment-on-published-sample-page}

[Continuando l’esperienza](/help/communities/extend-sample-page.md#publish-sample-page) nell’istanza di pubblicazione, ancora con accesso come lo stesso utente, è ora possibile aggiornare la pagina nell’ambiente di pubblicazione per visualizzare la modifica per rimuovere l’avatar:

![chlimage_1-136](assets/chlimage_1-136.png)

### Esempio di pacchetto di estensione dei commenti {#sample-comment-extension-package}

Allegato è un pacchetto dell&#39;applicazione di commenti personalizzata creata in questa esercitazione.

[Ottieni file](assets/sample-comment-extension-6-1-fp3.zip)
