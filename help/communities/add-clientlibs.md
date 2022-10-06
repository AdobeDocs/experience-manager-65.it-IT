---
title: Aggiungi clientlibs
seo-title: Add Clientlibs
description: Aggiungi una ClientLibraryFolder
seo-description: Add a ClientLibraryFolder
uuid: 2944923d-caca-4607-81a4-4122a2ce8e41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 46f81c3f-6512-43f1-8ec1-cc717ab6f6ff
docset: aem65
exl-id: 569f2052-b4fe-4f7f-aec9-657217cba091
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 2%

---

# Aggiungi clientlibs {#add-clientlibs}

## Aggiungi una ClientLibraryFolder (clientlibs) {#add-a-clientlibraryfolder-clientlibs}

Crea una ClientLibraryFolder denominata `clientlibs` che conterrà i JS e CSS utilizzati per il rendering delle pagine del sito.

La `categories` il valore della proprietà dato a questa libreria client è l&#39;identificatore utilizzato per includere direttamente questa clientlib da una pagina di contenuto o per incorporarla in altre clientlibs.

1. Utilizzo **CRXDE Lite**, espandi `/etc/designs`

1. Fai clic con il pulsante destro del mouse `an-scf-sandbox` e seleziona `Create Node`

   * Nome : `clientlibs`
   * Tipo : `cq:ClientLibraryFolder`

1. Fai clic su **OK**

![add-client-library](assets/add-client-library.png)

In **Proprietà** scheda per il nuovo `clientlibs` , immetti **categorie** proprietà:

* Nome : **categorie**
* Tipo : **Stringa**
* Valore : **apps.an-scf-sandbox**
* Fate clic su **Aggiungi**
* Fai clic su **Salva tutto**

Nota : aggiunta in anteprima del valore delle categorie con &#39;apps&#39;. è una convenzione per identificare l&#39;applicazione proprietaria come presente nella cartella /apps, non /libs.  IMPORTANTE : Aggiungi segnaposto `js.tx`t e **`css.txt`** file. (Non è ufficialmente un cq:ClientLibraryFolder senza di loro.)

1. Fai clic con il pulsante destro del mouse **`/etc/designs/an-scf-sandbox/clientlibs`**
1. Seleziona **Crea file...**
1. Invio **Nome:** `css.txt`
1. Seleziona **Crea file...**
1. Invio **Nome:** `js.txt`
1. Fai clic su **Salva tutto**

![clientlibs-css](assets/clientlibs-css.png)

La prima riga di css.txt e js.txt identifica la posizione di base da cui devono essere trovati i seguenti elenchi di file.

Prova a impostare il contenuto di css.txt su

```
#base=.
 style.css
```

Quindi crea un file sotto clientlibs denominato style.css e imposta il contenuto su

`body {`

`background-color: #b0c4de;`

`}`

### Incorpora Clientlibs SCF {#embed-scf-clientlibs}

In **Proprietà** scheda per `clientlibs` node, immettere la proprietà String con più valori **incorporare**. Questo incorpora il necessario [librerie lato client (clientlibs) per componenti SCF](/help/communities/client-customize.md#clientlibs-for-scf). Per questa esercitazione vengono aggiunte molte delle clientlib necessarie per i componenti di Communities.

**Nota** che questo potrebbe essere o meno l&#39;approccio desiderato da utilizzare per un sito di produzione in quanto ci sono considerazioni di convenienza rispetto a dimensione/velocità dei clientlibs scaricati per ogni pagina.

Se utilizzi una sola funzione su una pagina, puoi includere la clientlib completa di quella funzione direttamente sulla pagina, ad esempio,

`% ui:includeClientLib categories=cq.social.hbs.forum" %`

In questo caso, includendoli tutti e così le clientlibs SCF più basilari che sono gli autori clientlibs sono preferite:

* Nome : **`embed`**
* Tipo : **`String`**
* Clic **`Multi`**
* Valore: **`cq.social.scf`**

   * Viene visualizzata una finestra di dialogo, fai clic su **`+`** dopo ogni voce per aggiungere le seguenti categorie clientlib:

      * **`cq.ckeditor`**
      * **`cq.social.author.hbs.comments`**
      * **`cq.social.author.hbs.forum`**
      * **`cq.social.author.hbs.rating`**
      * **`cq.social.author.hbs.reviews`**
      * **`cq.social.author.hbs.voting`**
      * Fai clic su **OK**

* Fai clic su **Salva tutto**

![scf-clientlibs](assets/scf-clientlibs.png)

Questo è come `/etc/designs/an-scf-sandbox/clientlibs` dovrebbe ora essere visualizzato nell’archivio :

![scf-clientlibs-view](assets/scf-clientlibs1.png)

### Includi clientlibs nel modello PlayPage {#include-clientlibs-in-playpage-template}

Senza includere `apps.an-scf-sandbox` Categoria ClientLibraryFolder nella pagina, i componenti SCF non saranno funzionali né formattati in quanto i JavaScript e gli stili necessari non saranno disponibili.

Ad esempio, senza includere le clientlibs, il componente commenti SCF viene visualizzato senza stile :

![clientlibs-comment](assets/clientlibs-comment.png)

Una volta incluse le clientlibs di apps.an-scf-sandbox, il componente dei commenti SCF appare formattato :

![clientlibs-comment-style](assets/clientlibs-comment1.png)

L’istruzione &quot;include&quot; appartiene alla `head` della sezione `html` script. Il valore predefinito **`foundation head.jsp`** include uno script che può essere sovrapposto : **`headlibs.jsp`**.

**Copia headlibs.jsp e includi clientlibs:**

1. Utilizzo **CRXDE Lite**, seleziona **`/libs/foundation/components/page/headlibs.jsp`**

1. Fai clic con il pulsante destro del mouse e seleziona **Copia** (o seleziona Copia dalla barra degli strumenti)
1. Seleziona **`/apps/an-scf-sandbox/components/playpage`**
1. Fai clic con il pulsante destro del mouse e seleziona **Incolla** (oppure seleziona Incolla dalla barra degli strumenti)
1. Fare doppio clic **`headlibs.jsp`** per aprirlo
1. Aggiungi la riga seguente alla fine del file
   **`<ui:includeClientLib categories="apps.an-scf-sandbox"/>`**

1. Fai clic su **Salva tutto**

```xml
<%@ page session="false" %><%
%><%@include file="/libs/foundation/global.jsp" %><%
%><ui:includeClientLib categories="cq.foundation-main"/><%
%>
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
<% currentDesign.writeCssIncludes(pageContext); %>
<ui:includeClientLib categories="apps.an-scf-sandbox"/>
```

Carica il tuo sito web nel browser e controlla se lo sfondo non è un&#39;ombra di blu.

[https://localhost:4502/content/an-scf-sandbox/en/play.html](https://localhost:4502/content/an-scf-sandbox/en/play.html)

![gioco di comunità](assets/community-play.png)

### Salvataggio del lavoro finora eseguito {#saving-your-work-so-far}

A questo punto, esiste una sandbox minimalista e potrebbe essere utile salvarla come pacchetto in modo che, durante la riproduzione, se il tuo archivio diventa danneggiato e desideri ricominciare da capo, puoi spegnere il server, rinominare o eliminare la cartella crx-quickstart/, accendere il server, caricare e installare questo pacchetto salvato, e non dover ripetere questi passaggi più fondamentali.

Questo pacchetto esiste nel [Creare una pagina di esempio](/help/communities/create-sample-page.md) tutorial per coloro che non vedono l&#39;ora di saltare e iniziare a giocare!..

Per creare un pacchetto:

* Da CRXDE Lite, fai clic su [Icona del pacchetto](https://localhost:4502/crx/packmgr/)
* Fai clic su **Crea pacchetto**

   * Nome pacchetto: an-scf-sandbox-minimal-pkg
   * Versione: 0,1
   * Gruppo: `leave as default`
   * Fai clic su **OK**

* Fai clic su **Modifica**

   * Seleziona **Filtri** scheda

      * Fai clic su **Aggiungi filtro**
      * Percorso principale: naviga a `/apps/an-scf-sandbox`
      * Fai clic su **Fine**
      * Fai clic su **Aggiungi filtro**
      * Percorso principale: naviga a `/etc/designs/an-scf-sandbox`
      * Fai clic su **Fine**
      * Fai clic su **Aggiungi filtro**
      * Percorso principale: naviga a `/content/an-scf-sandbox**`
      * Fai clic su **Fine**
   * Fai clic su **Salva**


* Fai clic su **Crea**

Ora è possibile selezionare **Scarica** per salvarlo su disco e **Carica pacchetto** altrove, e selezionare **Altro > Replica** per spingere la sandbox a un&#39;istanza di pubblicazione localhost per espandere il regno della sandbox.
