---
title: Sviluppo di applicazioni sandbox
seo-title: Sviluppo di applicazioni sandbox
description: Sviluppo di applicazioni mediante script di base
seo-description: Sviluppo di applicazioni mediante script di base
uuid: 572f68cd-9ecb-4b43-a7f8-4aa8feb6c64e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 910229a3-38b1-44f1-9c09-55f8fd6cbb1d
translation-type: tm+mt
source-git-commit: e5c2385c29e2d20d453e2d1496f7d459d1c55876
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 4%

---


# Sviluppo di applicazioni sandbox  {#develop-sandbox-application}

In questa sezione, ora che il modello è stato impostato nella sezione [iniziale dell&#39;applicazione](initial-app.md) e nelle pagine iniziali stabilite nella sezione del contenuto [](initial-content.md) iniziale, l&#39;applicazione può essere sviluppata utilizzando script di base, inclusa la possibilità di abilitare l&#39;authoring con i componenti Community. Alla fine di questa sezione, il sito Web sarà funzionale.

## Utilizzo di script di pagina Foundation {#using-foundation-page-scripts}

Lo script predefinito, creato al momento dell&#39;aggiunta del componente che esegue il rendering del modello della pagina di riproduzione, viene modificato in modo da includere il file head.jsp della pagina di base e il file body.jsp locale.

### Super Resource Type {#super-resource-type}

Il primo passaggio consiste nell&#39;aggiungere al `/apps/an-scf-sandbox/components/playpage` nodo una proprietà super type di risorsa in modo che erediti gli script e le proprietà del super type.

Utilizzo del CRXDE Lite:

1. Selezionare il nodo `/apps/an-scf-sandbox/components/playpage`.
1. Nella scheda Proprietà, immettere una nuova proprietà con i seguenti valori:

   Nome: `sling:resourceSuperType`

   Tipo: `String`

   Valore: `foundation/components/page`

1. Fate clic sul pulsante verde **[!UICONTROL +Aggiungi]** .
1. Fate clic su **[!UICONTROL Salva tutto]**.

   ![chlimage_1-231](assets/chlimage_1-231.png)

### Script head e body {#head-and-body-scripts}

1. Nel riquadro di **CRXDE Lite** Explorer, individuate `/apps/an-scf-sandbox/components/playpage` e fate doppio clic sul file `playpage.jsp` per aprirlo nel riquadro di modifica.

   `/apps/an-scf-sandbox/components/playpage/playpage.jsp`

   ```xml
   <%--
   
     An SCF Sandbox Play Component component.
   
     This is the component which renders content for An SCF Sandbox page.
   
   --%><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" %><%
   %><%
    // TODO add your code here
   %>
   ```

1. Essendo a conoscenza dei tag script aperti/chiusi, sostituire &quot; // TODO ...&quot; con include gli script per le parti head e body di &lt;html>.

   Con un super tipo di `foundation/components/page`, qualsiasi script non definito nella stessa cartella verrà risolto in uno script nella `/apps/foundation/components/page` cartella (se presente), in un altro script nella `/libs/foundation/components/page` cartella.

   `/apps/an-scf-sandbox/components/playpage/playpage.jsp`

   ```xml
   <%--
   
       An SCF Sandbox Play Component component: playpage.jsp
   
     This is the component which renders content for An SCF Sandbox page.
   
   --%><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" %>
   <html>
     <cq:include script="head.jsp"/>
     <cq:include script="body.jsp"/>
   </html>
   ```

1. Lo script foundation non `head.jsp` deve essere sovrapposto, ma lo script foundation `body.jsp` è vuoto.

   Per impostare l’authoring, sovrapponete `body.jsp` con uno script locale e includete nel corpo un sistema paragrafo (parsys):

   1. Accedi a `/apps/an-scf-sandbox/components`.
   1. Select the `playpage` node.
   1. Fare clic con il pulsante destro del mouse e selezionare `Create > Create File...`

      * Nome: **body.jsp**
   1. Fate clic su **[!UICONTROL Salva tutto]**.

   Aprite `/apps/an-scf-sandbox/components/playpage/body.jsp` e incollate il testo seguente:

   ```xml
   <%--
   
       An SCF Sandbox Play Component component: body.jsp
   
     This is the component which renders content for An SCF Sandbox page.
   
   --%><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" %>
   <body>
       <h2>Community Play</h2>
       <cq:include path="par" resourceType="foundation/components/parsys" />
   </body>
   ```

1. Fate clic su **[!UICONTROL Salva tutto]**.

**Visualizzare la pagina in un browser in modalità di modifica:**

* Interfaccia standard: [http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.html](http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.md)

Per modificare il contenuto della pagina è necessario non solo visualizzare l’intestazione **Community Play**, ma anche l’interfaccia utente.

Il pannello laterale Risorse/Componente viene visualizzato quando il pannello laterale è aperto e la finestra è sufficientemente ampia da consentire la visualizzazione del contenuto laterale e del contenuto della pagina.

![chlimage_1-232](assets/chlimage_1-232.png)

* Interfaccia classica: [http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html](http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html)

Di seguito viene illustrata l’aspetto della pagina di riproduzione nell’interfaccia classica, incluso con Content Finder (cf):

![chlimage_1-233](assets/chlimage_1-233.png)

## Componenti di Communities {#communities-components}

Per abilitare i componenti di Communities per la creazione, attenetevi alle istruzioni seguenti:

* [Accesso ai componenti Community](basics.md#accessing-communities-components)

Ai fini di questa sandbox, iniziate con i seguenti componenti **Community** (attivabili selezionando la casella):

* Commenti
* Forum
* Valutazione
* Recensioni
* Riepilogo recensioni (visualizzazione)
* Votazione

Inoltre, scegliete i componenti **[!UICONTROL Generali]** , ad esempio

* Immagine
* Tabella
* Testo
* Titolo (Foundation)

>[!NOTE]
>
>I componenti abilitati per la pagina par vengono memorizzati nell’archivio come valore della `components` proprietà della proprietà
>`/etc/designs/an-scf-sandbox/jcr:content/playpage/par` node.


## Pagina di destinazione {#landing-page}

In un ambiente multilingue, la pagina principale includerebbe uno script che analizzerebbe la richiesta del client per determinare la lingua preferita.

In questo semplice esempio, la pagina principale viene impostata statisticamente per reindirizzare alla pagina inglese, che in futuro potrebbe essere la pagina di destinazione principale con un collegamento alla pagina di riproduzione.

Modificate l’URL del browser nella pagina principale: [http://localhost:4502/editor.html/content/an-scf-sandbox.html](https://locahost:4502/editor.html/content/an-scf-sandbox.html)

* Selezionate l’icona Informazioni pagina
* Seleziona proprietà **[!UICONTROL di apertura]**
* Nella scheda AVANZATE

   * Per la voce Reindirizza, accedete a Siti **[!UICONTROL Web]** > Sito sandbox **[!UICONTROL SCF]** > Sandbox **[!UICONTROL SCF]**
   * Fai clic su **[!UICONTROL OK]**

* Fai clic su **[!UICONTROL OK]**

Una volta pubblicato il sito, quando si passa alla pagina principale di un’istanza di pubblicazione si passa alla pagina inglese.

L&#39;ultimo passaggio prima di giocare con i componenti SCF delle community è aggiungere una cartella libreria client (clientlibs) .... [Aggiungi Clienlibs](add-clientlibs.md)