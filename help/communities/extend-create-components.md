---
title: Creare i componenti
seo-title: Creare i componenti
description: Creare il componente Commenti
seo-description: Creare il componente Commenti
uuid: ea6e00d4-1db7-40ef-ae49-9ec55df58adf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 83c4f18a-d7d6-4090-88c7-41a9075153b5
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 5%

---


# Creare i componenti  {#create-the-components}

Nell’esempio di estensione dei componenti viene utilizzato il sistema di commenti, che in realtà è composto da due componenti

* Commenti - Il sistema di commenti che include il componente inserito in una pagina.
* Commento - Il componente che acquisisce un’istanza di un commento pubblicato.

Entrambi i componenti devono essere implementati, soprattutto se si personalizzano l’aspetto di un commento pubblicato.

>[!NOTE]
>
>È consentito un solo sistema di commenti per pagina del sito.
>
>Molte funzioni Community includono già un sistema di commenti il cui resourceType può essere modificato per fare riferimento al sistema di commenti esteso.

## Creare il componente Commenti {#create-the-comments-component}

Queste indicazioni specificano un valore **Group** diverso da `.hidden` questo per rendere il componente disponibile dal browser Componenti (barra laterale).

L&#39;eliminazione del file JSP creato automaticamente è perché verrà utilizzato il file HBS predefinito.

1. Passa a **CRXDE|Lite** ([http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp))

1. Create un percorso per le applicazioni personalizzate:

   * Selezionare il `/apps` nodo

      * **Crea cartella** denominata **[!UICONTROL custom]**
   * Selezionare il `/apps/custom` nodo

      * **Creare** componenti con nome cartella ****


1. Selezionare il `/apps/custom/components` nodo

   * **[!UICONTROL Crea > Componente...]**

      * **Etichetta**: *commenti*
      * **Titolo**: *Commenti Alt*
      * **Descrizione**: *Stile commento alternativo*
      * **Super Type**: *social/commons/components/hbs/comments*
      * **Gruppo**: *Personalizzato*
   * Seleziona **[!UICONTROL Avanti]**
   * Seleziona **[!UICONTROL Avanti]**
   * Seleziona **[!UICONTROL Avanti]**
   * Selezionare **[!UICONTROL OK]**


1. Espandi il nodo appena creato: `/apps/custom/components/comments`
1. Seleziona **[!UICONTROL Salva tutto]**
1. Clic con il pulsante destro del mouse `comments.jsp`
1. Seleziona **[!UICONTROL Elimina]**
1. Seleziona **[!UICONTROL Salva tutto]**

![chlimage_1-70](assets/chlimage_1-70.png)

### Creare il componente Commento secondario {#create-the-child-comment-component}

Queste direzioni impostano **Gruppo** su `.hidden` come solo il componente principale deve essere incluso all’interno di una pagina.

L&#39;eliminazione del file JSP creato automaticamente è perché verrà utilizzato il file HBS predefinito.

1. Passa al `/apps/custom/components/comments` nodo
1. Fare clic con il pulsante destro del mouse sul nodo

   * Selezionare **[!UICONTROL Crea] > **[!UICONTROL Componente...]**

      * **Etichetta**: *commento*
      * **Titolo**: *Commento Alt*
      * **Descrizione**: *Stile commento alternativo*
      * **Super Type**: *social/commons/components/hbs/comments/comment*
      * **Gruppo**: `*.hidden*`
   * Seleziona **[!UICONTROL Avanti]**
   * Seleziona **[!UICONTROL Avanti]**
   * Seleziona **[!UICONTROL Avanti]**
   * Selezionare **[!UICONTROL OK]**


1. Espandi il nodo appena creato: `/apps/custom/components/comments/comment`
1. Seleziona **[!UICONTROL Salva tutto]**
1. Clic con il pulsante destro del mouse `comment.jsp`
1. Seleziona **[!UICONTROL Elimina]**
1. Seleziona **[!UICONTROL Salva tutto]**

![chlimage_1-71](assets/chlimage_1-71.png)

![chlimage_1-72](assets/chlimage_1-72.png)

### Copiare e modificare gli script HBS predefiniti {#copy-and-modify-the-default-hbs-scripts}

Utilizzo di [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* Copia `comments.hbs`

   * Da [/libs/social/commons/components/hbs/comments](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments)
   * A/ [apps/custom/components/comments](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments)

* Modifica `comments.hbs` in:

   * Modificate il valore dell&#39; `data-scf-component` attributo (~line 20):

      * Da `social/commons/components/hbs/comments`
      * A `/apps/custom/components/comments`
   * Modificate per includere il componente commento personalizzato (~riga 75):

      * Sostituisci `{{include this resourceType='social/commons/components/hbs/comments/comment'}}`
      * Con `{{include this resourceType='/apps/custom/components/comments/comment'}}`


* Copia `comment.hbs`

   * Da [/libs/social/commons/components/hbs/comments/comment](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments/comment)
   * A/ [apps/custom/components/comments/comment](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment)

* Modifica `comment.hbs` in:

   * Modificare il valore dell’attributo data-scf-component (~ riga 19)

      * Da `social/commons/components/hbs/comments/comment`
      * A `/apps/custom/components/comments/comment`

* Seleziona `/apps/custom` nodo
* Seleziona **[!UICONTROL Salva tutto]**

## Creare una cartella libreria client {#create-a-client-library-folder}

Per evitare di dover includere esplicitamente questa libreria client, è possibile utilizzare il valore delle categorie per la clientlib del sistema di commenti predefinito ( `cq.social.author.hbs.comments`), ma tale clientlib verrà incluso anche per tutte le istanze del componente predefinito.

Utilizzo di [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* Seleziona `/apps/custom/components/comments` nodo
* Seleziona **[!UICONTROL Crea nodo]**

   * **Nome**: `clientlibs`
   * **Tipo**: `cq:ClientLibraryFolder`
   * Aggiungi alla scheda **[!UICONTROL Proprietà]** :

      * **Nome** `categories` Tipo **** Valore `String` **Valore** `cq.social.author.hbs.comments` `Multi`
      * **Nome** `dependencies` Tipo **** Valore `String` **Valore** `cq.social.scf` `Multi`

* Seleziona **[!UICONTROL Salva tutto]**
* Con `/apps/custom/components/comments/clientlib`il nodo s selezionato, create 3 file:

   * **Nome**: `css.txt`
   * **Nome**: `js.txt`
   * **Nome**: customcommentsystem.js

* Immettete &#39;customcommentsystem.js&#39; come contenuto di `js.txt`
* Seleziona **[!UICONTROL Salva tutto]**

![chlimage_1-73](assets/chlimage_1-73.png)

## Registrazione del modello e della vista SCF {#register-the-scf-model-view}

Quando si estende (ignora) un componente SCF, resourceType è diverso (la sovrapposizione utilizza il meccanismo di ricerca relativa che esegue la ricerca `/apps` prima di `/libs` fare in modo che resourceType rimanga lo stesso). Per questo motivo è necessario scrivere JavaScript (nella libreria client) per registrare il modello SCF JS e visualizzarlo per il resourceType personalizzato.

Inserite il testo seguente come contenuto di `customcommentsystem.js`:

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

## Pubblicare l&#39;app {#publish-the-app}

Per provare il componente esteso nell’ambiente di pubblicazione, è necessario replicare il componente personalizzato.

Un modo per farlo è

* Dalla navigazione globale

   * Select **[!UICONTROL Tools]** > **[!UICONTROL Deployment]** > **[!UICONTROL Replication]**
   * Seleziona **[!UICONTROL Attiva albero]**
   * Imposta `Start Path` su `/apps/custom`
   * Deseleziona **[!UICONTROL solo modifica]**
   * Pulsante Seleziona **[!UICONTROL Attiva]**

