---
title: Modificare l’aspetto (HBS)
seo-title: Alter the Appearance
description: Modificare gli script HBS
seo-description: Modify the HBS scripts
uuid: cff24505-dbb3-4312-9b1b-c1693b8d1c98
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e0da09b3-725d-4ed1-9273-2532132f6918
docset: aem65
exl-id: 27e1bff3-385e-4ced-87af-54044b7e8812
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# Modificare l’aspetto (HBS) {#alter-the-appearance-hbs}

Ora che i componenti per il sistema di commento personalizzato nella directory dell&#39;applicazione (/apps) sono in posizione, con una risorsaSuperType che fa riferimento al sistema di commento predefinito e il modello/vista personalizzato registrato, è possibile modificare l&#39;implementazione.

Per una semplice dimostrazione, viene rimosso l’avatar visualizzato dall’utente che ha effettuato l’accesso e che ha pubblicato un commento.

>[!NOTE]
>
>Per utilizzare l’estensione, l’istanza del sistema di commenti in un sito web da modificare (/content) deve impostare il relativo resourceType come sistema di commenti personalizzato.

## Modificare gli script HBS {#modify-the-hbs-scripts}

Utilizzo [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* Apri [/apps/custom/components/comments/comment/**comment.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment/comment.hbs)

   * Aggiungi un commento al tag che include l&#39;avatar per un commento (~ riga 21):

      ```
        <!--
         <<img class="scf-comment-avatar {{#if topLevel}}withTopLevel{{/if}}" src="{{author.avatarUrl}}"></img>
         -->
      ```

* Apri [/apps/custom/components/comments/**comments.hbs**](https://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comments.hbs)

   * Aggiungi un commento al tag che include l&#39;avatar per la voce di commento successiva (~ riga 44):

      ```
        <!--
         <img class="scf-composer-avatar" src="{{loggedInUser.avatarUrl}}"></img>
         -->
      ```

* Seleziona **Salva tutto**

### Replicare l&#39;app personalizzata {#replicate-custom-app}

Dopo che l’applicazione è stata modificata, è necessario replicare nuovamente il componente personalizzato.

Un modo per farlo è:

* Dal menu principale

   * Seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Replica]**.
   * Seleziona **[!UICONTROL Attiva albero]**.
   * Imposta `Start Path` a `/apps/custom`.
   * Deseleziona **[!UICONTROL Modificato solo]**.
   * Seleziona **[!UICONTROL Attiva]** pulsante .

### Visualizza commento modificato sulla pagina di esempio pubblicata {#view-modified-comment-on-published-sample-page}

[Continuazione dell’esperienza](/help/communities/extend-sample-page.md#publish-sample-page) nell’istanza di pubblicazione, ancora connesso come lo stesso utente, è ora possibile aggiornare la pagina nell’ambiente di pubblicazione per visualizzare la modifica per rimuovere l’avatar:

![view-modified-content](assets/view-modified-content.png)

### Pacchetto di estensione dei commenti di esempio {#sample-comment-extension-package}

In allegato è presente un pacchetto dell’applicazione di commenti personalizzati creata in questa esercitazione.

[Ottieni file](assets/sample-comment-extension-6-1-fp3.zip)
