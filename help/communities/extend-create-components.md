---
title: Creare i componenti
seo-title: Create the Components
description: Creare il componente Commenti
seo-description: Create the Comments component
uuid: ea6e00d4-1db7-40ef-ae49-9ec55df58adf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 83c4f18a-d7d6-4090-88c7-41a9075153b5
exl-id: 2e02db9f-294d-4d4a-92da-3ab1d38416ab
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 4%

---

# Creare i componenti  {#create-the-components}

L’esempio di estensione dei componenti utilizza il sistema di commento, che in realtà è composto da due componenti

* Commenti : il sistema di commenti che comprende il componente inserito in una pagina.
* Commento : il componente che acquisisce un’istanza di un commento pubblicato.

Entrambi i componenti devono essere implementati, specialmente se si personalizzano l’aspetto di un commento pubblicato.

>[!NOTE]
>
>È consentito un solo sistema di commenti per pagina del sito.
>
>Molte funzionalità di Communities includono già un sistema di commenti il cui resourceType può essere modificato per fare riferimento al sistema di commenti esteso.

## Creare il componente Commenti {#create-the-comments-component}

Queste direzioni specificano **Gruppo** valore diverso da `.hidden` il componente può quindi essere reso disponibile dal browser componenti (barra laterale).

L&#39;eliminazione del file JSP creato automaticamente è perché verrà utilizzato il file HBS predefinito.

1. Sfoglia per **CRXDE|Lite** ([http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp))

1. Crea un percorso per le applicazioni personalizzate:

   * Seleziona la `/apps` nodo

      * **Crea cartella** denominato **[!UICONTROL personalizzato]**
   * Seleziona la `/apps/custom` nodo

      * **Crea cartella** denominato **[!UICONTROL componenti]**


1. Seleziona la `/apps/custom/components` nodo

   * **[!UICONTROL Crea > Componente..]**

      * **Etichetta**: *commenti*
      * **Titolo**: *Commenti Alt*
      * **Descrizione**: *Stile commenti alternativi*
      * **Super Type**: *social/commons/components/hbs/comments*
      * **Gruppo**: *Personalizzato*
   * Seleziona **[!UICONTROL Avanti]**
   * Seleziona **[!UICONTROL Avanti]**
   * Seleziona **[!UICONTROL Avanti]**
   * Seleziona **[!UICONTROL OK]**


1. Espandi il nodo appena creato: `/apps/custom/components/comments`
1. Seleziona **[!UICONTROL Salva tutto]**
1. Fai clic con il pulsante destro del mouse `comments.jsp`
1. Seleziona **[!UICONTROL Elimina]**
1. Seleziona **[!UICONTROL Salva tutto]**

![create-component](assets/create-component.png)

### Creare il componente Commento figlio {#create-the-child-comment-component}

Queste direzioni **Gruppo** a `.hidden` poiché solo il componente principale deve essere incluso all’interno di una pagina.

L&#39;eliminazione del file JSP creato automaticamente è perché verrà utilizzato il file HBS predefinito.

1. Passa a `/apps/custom/components/comments` nodo
1. Fai clic con il pulsante destro del mouse sul nodo

   * Seleziona **[!UICONTROL Crea]** > **[!UICONTROL Componente...]**

      * **Etichetta**: *commento*
      * **Titolo**: *Commento Alt*
      * **Descrizione**: *Stile commento alternativo*
      * **Super Type**: *social/commons/components/hbs/comments/comment*
      * **Gruppo**: `*.hidden*`
   * Seleziona **[!UICONTROL Avanti]**
   * Seleziona **[!UICONTROL Avanti]**
   * Seleziona **[!UICONTROL Avanti]**
   * Seleziona **[!UICONTROL OK]**


1. Espandi il nodo appena creato: `/apps/custom/components/comments/comment`
1. Seleziona **[!UICONTROL Salva tutto]**
1. Fai clic con il pulsante destro del mouse `comment.jsp`
1. Seleziona **[!UICONTROL Elimina]**
1. Seleziona **[!UICONTROL Salva tutto]**

![create-child-component](assets/create-child-component.png)

![create-component-crxde](assets/create-component-crxde.png)

### Copia e modifica degli script HBS predefiniti {#copy-and-modify-the-default-hbs-scripts}

Utilizzo [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* Copia `comments.hbs`

   * Da [/libs/social/commons/components/hbs/comments](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments)
   * A [/apps/custom/components/comments](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments)

* Modifica `comments.hbs` a:

   * Modificare il valore del `data-scf-component` attributo (~riga 20):

      * Da `social/commons/components/hbs/comments`
      * A `/apps/custom/components/comments`
   * Modifica per includere il componente commento personalizzato (~riga 75):

      * Sostituisci `{{include this resourceType='social/commons/components/hbs/comments/comment'}}`
      * Con `{{include this resourceType='/apps/custom/components/comments/comment'}}`


* Copia `comment.hbs`

   * Da [/libs/social/commons/components/hbs/comments/comment](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments/comment)
   * A [/apps/custom/components/comments/comment](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment)

* Modifica `comment.hbs` a:

   * Modifica il valore dell’attributo data-scf-component (~ riga 19)

      * Da `social/commons/components/hbs/comments/comment`
      * A `/apps/custom/components/comments/comment`

* Seleziona `/apps/custom` nodo
* Seleziona **[!UICONTROL Salva tutto]**

## Creare una cartella della libreria client {#create-a-client-library-folder}

Per evitare di dover includere esplicitamente questa libreria client, è possibile utilizzare il valore delle categorie per la clientlib del sistema di commenti predefinita ( `cq.social.author.hbs.comments`), ma questo clientlib verrebbe incluso anche per tutte le istanze del componente predefinito.

Utilizzo [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* Seleziona `/apps/custom/components/comments` nodo
* Seleziona **[!UICONTROL Crea nodo]**

   * **Nome**: `clientlibs`
   * **Tipo**: `cq:ClientLibraryFolder`
   * Aggiungi a **[!UICONTROL Proprietà]** scheda:

      * **Nome** `categories` **Tipo** `String` **Valore** `cq.social.author.hbs.comments` `Multi`
      * **Nome** `dependencies` **Tipo** `String` **Valore** `cq.social.scf` `Multi`

* Seleziona **[!UICONTROL Salva tutto]**
* Con `/apps/custom/components/comments/clientlib`come nodo selezionato, crea 3 file:

   * **Nome**: `css.txt`
   * **Nome**: `js.txt`
   * **Nome**: customcommentsystem.js

* Inserisci &#39;customcommentsystem.js&#39; come contenuto di `js.txt`
* Seleziona **[!UICONTROL Salva tutto]**

![comments-clientlibs](assets/comments-clientlibs.png)

## Registrare il modello e la vista SCF {#register-the-scf-model-view}

Quando estendi (sovrascrivi) un componente SCF, resourceType è diverso (la sovrapposizione fa uso del meccanismo di ricerca relativo che esegue la ricerca attraverso `/apps` prima `/libs` in modo che resourceType rimanga lo stesso). Per questo motivo è necessario scrivere JavaScript (nella libreria client) per registrare il modello SCF JS e visualizzare il resourceType personalizzato.

Inserisci il seguente testo come contenuto di `customcommentsystem.js`:

### customcommentsystem.js {#customcommentsystem-js}

```xml
(function($CQ, _, Backbone, SCF) {
    "use strict";

    var CustomComment = SCF.Components["social/commons/components/hbs/comments/comment"].Model;
    var CustomCommentView = SCF.Components["social/commons/components/hbs/comments/comment"].View;

    var CustomCommentSystem = SCF.Components["social/commons/components/hbs/comments"].Model;
    var CustomCommentSystemView = SCF.Components["social/commons/components/hbs/comments"].View;

    SCF.registerComponent('/apps/custom/components/comments/comment', CustomComment, CustomCommentView);
    SCF.registerComponent('/apps/custom/components/comments', CustomCommentSystem, CustomCommentSystemView);

})($CQ, _, Backbone, SCF);
```

* Seleziona **[!UICONTROL Salva tutto]**

## Pubblicare l’app {#publish-the-app}

Per provare l’esperienza del componente esteso nell’ambiente di pubblicazione, è necessario replicare il componente personalizzato.

Un modo per farlo è:

* Dalla navigazione globale,

   * Seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Distribuzione]** > **[!UICONTROL Replica]**
   * Seleziona **[!UICONTROL Attiva albero]**
   * Imposta `Start Path` a `/apps/custom`
   * Deseleziona **[!UICONTROL Modificato solo]**
   * Seleziona **[!UICONTROL Attiva]** pulsante
