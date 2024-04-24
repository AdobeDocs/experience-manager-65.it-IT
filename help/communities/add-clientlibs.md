---
title: Aggiungi Clientlibs
description: Scopri come aggiungere una ClientLibraryFolder (clientlibs) utilizzata per contenere i fogli di stile JavaScript e Cascading utilizzati per eseguire il rendering delle pagine del sito.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 569f2052-b4fe-4f7f-aec9-657217cba091
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 0%

---

# Aggiungi Clientlibs {#add-clientlibs}

## Aggiungere una ClientLibraryFolder (clientlibs) {#add-a-clientlibraryfolder-clientlibs}

Creare una ClientLibraryFolder denominata `clientlibs` che contiene JavaScript (JS) e Cascading Styles Sheets (CSS) utilizzati per eseguire il rendering delle pagine del sito.

Il `categories` il valore della proprietà assegnato a questa libreria client è l’identificatore utilizzato per includere direttamente questa libreria client da una pagina di contenuto o per incorporarla in altre librerie client.

1. Utilizzo di **CRXDE Liti**, espandi `/etc/designs`

1. Clic con il pulsante destro `an-scf-sandbox` e seleziona `Create Node`

   * Nome : `clientlibs`
   * Tipo : `cq:ClientLibraryFolder`

1. Clic **OK**

![add-client-library](assets/add-client-library.png)

In **Proprietà** scheda per il nuovo `clientlibs` , immetti il **categorie** proprietà:

* Nome : **categorie**
* Tipo : **Stringa**
* Valore : **apps.an-scf-sandbox**
* Clic **Aggiungi**
* Clic **Salva tutto**

Nota: anteprima del valore delle categorie con &quot;apps&quot;. è una convenzione per identificare l’applicazione proprietaria come presente nella cartella /apps, non in /libs. IMPORTANTE: aggiungere un segnaposto `js.tx`t e **`css.txt`** file. (Non è ufficialmente un cq:ClientLibraryFolder senza di loro).

1. Clic con il pulsante destro **`/etc/designs/an-scf-sandbox/clientlibs`**
1. Seleziona **Crea file...**
1. Invio **Nome:** `css.txt`
1. Seleziona **Crea file...**
1. Invio **Nome:** `js.txt`
1. Clic **Salva tutto**

![clientlibs-css](assets/clientlibs-css.png)

La prima riga dei file css.txt e js.txt identifica la posizione di base da cui si trovano i seguenti elenchi di file.

Prova a impostare il contenuto di css.txt su

```
#base=.
 style.css
```

Quindi crea un file in clientlibs denominato style.css e imposta il contenuto su

`body {`

`background-color: #b0c4de;`

`}`

### Incorpora librerie client SCF {#embed-scf-clientlibs}

In **Proprietà** scheda per `clientlibs` , immettere la proprietà String con più valori **incorporare**. Ciò incorpora le [librerie lato client (clientlibs) per i componenti SCF](/help/communities/client-customize.md#clientlibs-for-scf). Per questa esercitazione, vengono aggiunte molte delle clientlibs necessarie per i componenti Community.

Questo potrebbe essere o meno l&#39;approccio desiderato da utilizzare per un sito di produzione, in quanto ci sono considerazioni di convenienza rispetto alle dimensioni/velocità delle clientlibs scaricate per ogni pagina.

Se utilizzi una sola funzione su una pagina, puoi includere la libreria client completa della funzione direttamente sulla pagina, ad esempio,

`% ui:includeClientLib categories=cq.social.hbs.forum" %`

In questo caso, includendoli tutti e quindi si preferiscono le clientlibs SCF di base che sono le clientlibs dell’autore:

* Nome : **`embed`**
* Tipo : **`String`**
* Clic **`Multi`**
* Valore: **`cq.social.scf`**

   * Apparirà una finestra di dialogo, fai clic su **`+`** dopo ogni voce per aggiungere le seguenti categorie clientlib:

      * **`cq.ckeditor`**
      * **`cq.social.author.hbs.comments`**
      * **`cq.social.author.hbs.forum`**
      * **`cq.social.author.hbs.rating`**
      * **`cq.social.author.hbs.reviews`**
      * **`cq.social.author.hbs.voting`**
      * Clic **OK**

* Clic **Salva tutto**

![scf-clientlibs](assets/scf-clientlibs.png)

Ecco come `/etc/designs/an-scf-sandbox/clientlibs` dovrebbe ora essere visualizzato nell’archivio :

![scf-clientlibs-view](assets/scf-clientlibs1.png)

### Includi clientlibs nel modello PlayPage {#include-clientlibs-in-playpage-template}

Senza includere `apps.an-scf-sandbox` Categoria ClientLibraryFolder sulla pagina, i componenti SCF non sono funzionali né formattati in quanto gli stili JavaScript e CSS necessari non sono disponibili.

Ad esempio, senza includere clientlibs, il componente SCF comments (commenti SCF) non viene formattato:

![clientlibs-comment](assets/clientlibs-comment.png)

Una volta incluse le clientlibs apps.an-scf-sandbox, il componente commenti SCF appare con lo stile:

![clientlibs-comment-styled](assets/clientlibs-comment1.png)

L&#39;istruzione &quot;include&quot; appartiene al `head` sezione del `html` script. Il valore predefinito **`foundation head.jsp`** include uno script che può essere sovrapposto: **`headlibs.jsp`**.

**Copia headlibs.jsp e includi clientlibs:**

1. Utilizzo di **CRXDE Liti**, seleziona **`/libs/foundation/components/page/headlibs.jsp`**

1. Fai clic con il pulsante destro del mouse e seleziona (Copia negli Appunti) **Copia** (oppure seleziona Copia dalla barra degli strumenti).
1. Seleziona **`/apps/an-scf-sandbox/components/playpage`**
1. Fai clic con il pulsante destro del mouse e seleziona (Copia negli Appunti) **Incolla** (oppure seleziona Incolla dalla barra degli strumenti).
1. Doppio clic **`headlibs.jsp`** in modo da poterlo aprire
1. Aggiungi la riga seguente alla fine del file
   **`<ui:includeClientLib categories="apps.an-scf-sandbox"/>`**

1. Clic **Salva tutto**

```xml
<%@ page session="false" %><%
%><%@include file="/libs/foundation/global.jsp" %><%
%><ui:includeClientLib categories="cq.foundation-main"/><%
%>
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
<% currentDesign.writeCssIncludes(pageContext); %>
<ui:includeClientLib categories="apps.an-scf-sandbox"/>
```

Carica il tuo sito web nel browser e osserva se lo sfondo non è una tonalità di blu.

[https://localhost:4502/content/an-scf-sandbox/en/play.html](https://localhost:4502/content/an-scf-sandbox/en/play.html)

![community-play](assets/community-play.png)

### Salvataggio del lavoro {#saving-your-work-so-far}

A questo punto, esiste una sandbox minimalista. Potrebbe essere utile salvarlo come pacchetto in modo che, durante la riproduzione, se l’archivio diventa danneggiato e desideri ricominciare, puoi spegnere il server. Quindi rinomina o elimina la cartella crx-quickstart/, accendi il server, carica e installa questo pacchetto salvato e non devi ripetere questi passaggi più semplici.

Questo pacchetto esiste in [Crea una pagina di esempio](/help/communities/create-sample-page.md) tutorial per coloro che non vedono l’ora di entrare e iniziare a giocare.

Per creare un pacchetto:

* Da CRXDE Liti, fai clic su [Icona pacchetto](https://localhost:4502/crx/packmgr/)
* Clic **Crea pacchetto**

   * Nome pacchetto: an-scf-sandbox-minimal-pkg
   * Versione: 0.1
   * Gruppo: `leave as default`
   * Clic **OK**

* Clic **Modifica**

   * Seleziona **Filtri** scheda

      * Clic **Aggiungi filtro**
      * Percorso principale: vai a `/apps/an-scf-sandbox`
      * Clic **Fine**
      * Clic **Aggiungi filtro**
      * Percorso principale: vai a `/etc/designs/an-scf-sandbox`
      * Clic **Fine**
      * Clic **Aggiungi filtro**
      * Percorso principale: vai a `/content/an-scf-sandbox**`
      * Clic **Fine**

   * Clic **Salva**

* Clic **Genera**

Ora puoi selezionare **Scarica** per salvarlo su disco e **Carica pacchetto** altrove e seleziona **Altro > Replica** per inviare la sandbox a un’istanza di pubblicazione localhost per espandere il realm della sandbox.
