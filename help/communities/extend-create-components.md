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
source-git-commit: 418e7fad2d990f1a7cb3b69ab4c290ca1b7075ba
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 4%

---


# Creare i componenti {#create-the-components}

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

Queste indicazioni specificano un valore **Group** diverso da `.hidden` in modo che il componente possa essere reso disponibile dal browser Componenti (barra laterale).

L&#39;eliminazione del file JSP creato automaticamente è perché verrà utilizzato il file HBS predefinito.

1. Passare a **CRXDE|Lite** ([http://localhost:4502/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp))

1. Create un percorso per le applicazioni personalizzate:

   * Selezionare il nodo `/apps`

      * **Crea** cartella  **[!UICONTROL personalizzata]**
   * Selezionare il nodo `/apps/custom`

      * **Creare** componenti  **[!UICONTROL con nome cartella]**


1. Selezionare il nodo `/apps/custom/components`

   * **[!UICONTROL Crea > Componente...]**

      * **Etichetta**:  *commenti*
      * **Titolo**:  *Commenti Alt*
      * **Descrizione**:  *Stile commento alternativo*
      * **Super Type**:  *social/commons/components/hbs/comments*
      * **Gruppo**:  *Personalizzato*
   * Seleziona **[!UICONTROL Avanti]**
   * Seleziona **[!UICONTROL Avanti]**
   * Seleziona **[!UICONTROL Avanti]**
   * Selezionare **[!UICONTROL OK]**


1. Espandi il nodo appena creato: `/apps/custom/components/comments`
1. Selezionare **[!UICONTROL Salva tutto]**
1. Fare clic con il pulsante destro del mouse su `comments.jsp`
1. Selezionare **[!UICONTROL Elimina]**
1. Selezionare **[!UICONTROL Salva tutto]**

![create-component](assets/create-component.png)

### Creare il componente Commento secondario {#create-the-child-comment-component}

Queste indicazioni impostano **Group** su `.hidden`, in quanto solo il componente principale deve essere incluso all&#39;interno di una pagina.

L&#39;eliminazione del file JSP creato automaticamente è perché verrà utilizzato il file HBS predefinito.

1. Passa al nodo `/apps/custom/components/comments`
1. Fare clic con il pulsante destro del mouse sul nodo

   * Selezionare **[!UICONTROL Crea]** > **[!UICONTROL Componente...]**

      * **Etichetta**:  *commento*
      * **Titolo**:  *Commento Alt*
      * **Descrizione**:  *Stile commento alternativo*
      * **Super Type**:  *social/commons/components/hbs/comments/comment*
      * **Gruppo**: `*.hidden*`
   * Seleziona **[!UICONTROL Avanti]**
   * Seleziona **[!UICONTROL Avanti]**
   * Seleziona **[!UICONTROL Avanti]**
   * Selezionare **[!UICONTROL OK]**


1. Espandi il nodo appena creato: `/apps/custom/components/comments/comment`
1. Selezionare **[!UICONTROL Salva tutto]**
1. Fare clic con il pulsante destro del mouse su `comment.jsp`
1. Selezionare **[!UICONTROL Elimina]**
1. Selezionare **[!UICONTROL Salva tutto]**

![create-child-component](assets/create-child-component.png)

![create-component-crxde](assets/create-component-crxde.png)

### Copia e modifica degli script HBS predefiniti {#copy-and-modify-the-default-hbs-scripts}

Utilizzando [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* Copia `comments.hbs`

   * Da [/libs/social/commons/components/hbs/comments](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments)
   * A [/apps/custom/components/comments](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments)

* Modifica `comments.hbs` in:

   * Modificate il valore dell&#39;attributo `data-scf-component` (~line 20):

      * Da `social/commons/components/hbs/comments`
      * A `/apps/custom/components/comments`
   * Modificate per includere il componente commento personalizzato (~riga 75):

      * Sostituisci `{{include this resourceType='social/commons/components/hbs/comments/comment'}}`
      * Con `{{include this resourceType='/apps/custom/components/comments/comment'}}`


* Copia `comment.hbs`

   * Da [/libs/social/commons/components/hbs/comments/comment](http://localhost:4502/crx/de/index.jsp#/libs/social/commons/components/hbs/comments/comment)
   * A [/apps/custom/components/comments/comment](http://localhost:4502/crx/de/index.jsp#/apps/custom/components/comments/comment)

* Modifica `comment.hbs` in:

   * Modificare il valore dell’attributo data-scf-component (~ riga 19)

      * Da `social/commons/components/hbs/comments/comment`
      * A `/apps/custom/components/comments/comment`

* Selezionare il nodo `/apps/custom`
* Selezionare **[!UICONTROL Salva tutto]**

## Creare una cartella libreria client {#create-a-client-library-folder}

Per evitare di dover includere in modo esplicito questa libreria client, è possibile utilizzare il valore delle categorie per la clientlib del sistema di commenti predefinito ( `cq.social.author.hbs.comments`), ma anche questa clientlib verrà inclusa per tutte le istanze del componente predefinito.

Utilizzando [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md):

* Selezionare il nodo `/apps/custom/components/comments`
* Selezionare **[!UICONTROL Crea nodo]**

   * **Nome**: `clientlibs`
   * **Tipo**: `cq:ClientLibraryFolder`
   * Aggiungi alla scheda **[!UICONTROL Proprietà]**:

      * **** `categories` **** `String` **NameTypeValue** `cq.social.author.hbs.comments` `Multi`
      * **** `dependencies` **** `String` **NameTypeValue** `cq.social.scf` `Multi`

* Selezionare **[!UICONTROL Salva tutto]**
* Con il nodo `/apps/custom/components/comments/clientlib`s selezionato, create 3 file:

   * **Nome**: `css.txt`
   * **Nome**: `js.txt`
   * **Nome**: customcommentsystem.js

* Immettete &#39;customcommentsystem.js&#39; come contenuto di `js.txt`
* Selezionare **[!UICONTROL Salva tutto]**

![comments-clientlibs](assets/comments-clientlibs.png)

## Registra modello SCF &amp; vista {#register-the-scf-model-view}

Quando si estende (si sovrascrive) un componente SCF, resourceType è diverso (la sovrapposizione utilizza il meccanismo di ricerca relativa che esegue la ricerca in `/apps` prima di `/libs` in modo che resourceType rimanga lo stesso). Per questo motivo è necessario scrivere JavaScript (nella libreria client) per registrare il modello SCF JS e visualizzarlo per il resourceType personalizzato.

Immettete il testo seguente come contenuto di `customcommentsystem.js`:

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

* Selezionare **[!UICONTROL Salva tutto]**

## Pubblicare l&#39;app {#publish-the-app}

Per provare il componente esteso nell’ambiente di pubblicazione, è necessario replicare il componente personalizzato.

Un modo per farlo è:

* Dalla navigazione globale,

   * Selezionare **[!UICONTROL Strumenti]** > **[!UICONTROL Distribuzione]** > **[!UICONTROL Replica]**
   * Selezionare **[!UICONTROL Attiva albero]**
   * Impostare `Start Path` su `/apps/custom`
   * Deselezionare **[!UICONTROL Solo modificate]**
   * Selezionare il pulsante **[!UICONTROL Attiva]**

