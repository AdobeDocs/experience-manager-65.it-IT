---
title: Creare i componenti
description: Scopri come estendere i componenti utilizzando il sistema di commenti composto dai componenti Commenti e Commenti.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 2e02db9f-294d-4d4a-92da-3ab1d38416ab
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 0%

---

# Creare i componenti  {#create-the-components}

Nell’esempio di estensione dei componenti viene utilizzato il sistema di commenti, composto da due componenti.

* Commenti: il sistema di commenti globale, ovvero il componente inserito in una pagina.
* Commento: componente che acquisisce un’istanza di un commento pubblicato.

Entrambi i componenti devono essere implementati, soprattutto se si personalizza l’aspetto di un commento pubblicato.

>[!NOTE]
>
>È consentito un solo sistema di commenti per pagina del sito.
>
>Molte funzioni di Communities includono già un sistema di commenti il cui resourceType può essere modificato per fare riferimento al sistema di commenti esteso.

## Creare il componente Commenti {#create-the-comments-component}

Queste indicazioni specificano un valore **Group** diverso da `.hidden` in modo che il componente possa essere reso disponibile dal browser componenti (barra laterale).

L’eliminazione del file JSP creato automaticamente è dovuta al fatto che viene utilizzato il file HBS predefinito.

1. Passa a **CRXDE|Lite** ([http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp))

1. Creare una posizione per le applicazioni personalizzate:

   * Seleziona il nodo `/apps`

      * **Crea cartella** denominata **[!UICONTROL personalizzata]**

   * Seleziona il nodo `/apps/custom`

      * **Crea cartella** denominata **[!UICONTROL componenti]**

1. Seleziona il nodo `/apps/custom/components`

   * **[!UICONTROL Crea > Componente...]**

      * **Etichetta**: *commenti*
      * **Titolo**: *Commenti Alt*
      * **Descrizione**: *Stile commenti alternativo*
      * **Super Type**: *social/commons/components/hbs/comments*
      * **Gruppo**: *Personalizzato*

   * Seleziona **[!UICONTROL Avanti]**
   * Seleziona **[!UICONTROL Avanti]**
   * Seleziona **[!UICONTROL Avanti]**
   * Seleziona **[!UICONTROL OK]**

1. Espandere il nodo creato: `/apps/custom/components/comments`
1. Seleziona **[!UICONTROL Salva tutto]**
1. Fare clic con il pulsante destro del mouse su `comments.jsp`
1. Seleziona **[!UICONTROL Elimina]**
1. Seleziona **[!UICONTROL Salva tutto]**

![create-component](assets/create-component.png)

### Creare il componente Commento figlio {#create-the-child-comment-component}

Queste indicazioni impostano **Group** su `.hidden` in quanto solo il componente padre deve essere incluso in una pagina.

L’eliminazione del file JSP creato automaticamente è dovuta al fatto che viene utilizzato il file HBS predefinito.

1. Passa al nodo `/apps/custom/components/comments`
1. Fare clic con il pulsante destro del mouse sul nodo

   * Seleziona **[!UICONTROL Crea]** > **[!UICONTROL Componente...]**

      * **Etichetta**: *commento*
      * **Titolo**: *Commento alternativo*
      * **Descrizione**: *Stile commento alternativo*
      * **Super Type**: *social/commons/components/hbs/comments/comment*
      * **Gruppo**: `*.hidden*`

   * Seleziona **[!UICONTROL Avanti]**
   * Seleziona **[!UICONTROL Avanti]**
   * Seleziona **[!UICONTROL Avanti]**
   * Seleziona **[!UICONTROL OK]**

1. Espandere il nodo creato: `/apps/custom/components/comments/comment`
1. Seleziona **[!UICONTROL Salva tutto]**
1. Fare clic con il pulsante destro del mouse su `comment.jsp`
1. Seleziona **[!UICONTROL Elimina]**
1. Seleziona **[!UICONTROL Salva tutto]**

![create-child-component](assets/create-child-component.png)

![create-component-crxde](assets/create-component-crxde.png)

### Copiare e modificare gli script HBS predefiniti {#copy-and-modify-the-default-hbs-scripts}

Utilizzo di [CRXDE Liti](../../help/sites-developing/developing-with-crxde-lite.md):

* Copia `comments.hbs`

   * Da [/libs/social/commons/components/hbs/comments](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments)
   * A [/apps/custom/components/comments](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments)

* Modifica `comments.hbs` in:

   * Modifica il valore dell&#39;attributo `data-scf-component` (~riga 20):

      * Da `social/commons/components/hbs/comments`
      * A `/apps/custom/components/comments`

   * Modifica per includere il componente commento personalizzato (~riga 75):

      * Sostituisci `{{include this resourceType='social/commons/components/hbs/comments/comment'}}`
      * Con `{{include this resourceType='/apps/custom/components/comments/comment'}}`

* Copia `comment.hbs`

   * Da [/libs/social/commons/components/hbs/comments/comment](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments/comment)
   * A [/apps/custom/components/comments/comment](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment)

* Modifica `comment.hbs` in:

   * Modifica il valore dell’attributo data-scf-component (~ riga 19)

      * Da `social/commons/components/hbs/comments/comment`
      * A `/apps/custom/components/comments/comment`

* Seleziona nodo `/apps/custom`
* Seleziona **[!UICONTROL Salva tutto]**

## Creare una cartella della libreria client {#create-a-client-library-folder}

Per evitare di dover includere questa libreria client, è possibile utilizzare il valore delle categorie per la libreria client del sistema di commenti predefinito ( `cq.social.author.hbs.comments`). Tuttavia, questa libreria client dovrebbe quindi essere inclusa anche per tutte le istanze del componente predefinito.

Utilizzo di [CRXDE Liti](../../help/sites-developing/developing-with-crxde-lite.md):

* Seleziona nodo `/apps/custom/components/comments`
* Seleziona **[!UICONTROL Crea nodo]**

   * **Nome**: `clientlibs`
   * **Tipo**: `cq:ClientLibraryFolder`
   * Aggiungi alla scheda **[!UICONTROL Proprietà]**:

      * **Nome** `categories` **Tipo** `String` **Valore** `cq.social.author.hbs.comments` `Multi`
      * **Nome** `dependencies` **Tipo** `String` **Valore** `cq.social.scf` `Multi`

* Seleziona **[!UICONTROL Salva tutto]**
* Con il nodo `/apps/custom/components/comments/clientlib` selezionato, crea tre file:

   * **Nome**: `css.txt`
   * **Nome**: `js.txt`
   * **Nome**: customcommentsystem.js

* Immettere &#39;customcommentsystem.js&#39; come contenuto di `js.txt`
* Seleziona **[!UICONTROL Salva tutto]**

![commenti-clientlibs](assets/comments-clientlibs.png)

## Registra il modello e la vista SCF {#register-the-scf-model-view}

Quando si estende (esegue l&#39;override) un componente SCF, resourceType è diverso (la sovrapposizione utilizza il meccanismo di ricerca relativo che esegue la ricerca in `/apps` prima di `/libs` in modo che resourceType rimanga invariato). Per questo motivo è necessario scrivere JavaScript (nella libreria client) per registrare il modello JS SCF e visualizzare per il resourceType personalizzato.

Immettere il testo seguente come contenuto di `customcommentsystem.js`:

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

## Publish l’app {#publish-the-app}

Per avere un’idea del componente esteso nell’ambiente di pubblicazione, è necessario replicare il componente personalizzato.

Un modo per farlo è:

* Dalla navigazione globale,

   * Seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Distribuzione]** > **[!UICONTROL Replica]**
   * Seleziona **[!UICONTROL Attiva albero]**
   * Imposta `Start Path` su `/apps/custom`
   * Deseleziona **[!UICONTROL Solo Modificato]**
   * Seleziona pulsante **[!UICONTROL Attiva]**
