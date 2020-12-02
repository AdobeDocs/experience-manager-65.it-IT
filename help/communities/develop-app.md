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
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 4%

---


# Sviluppo di applicazioni sandbox {#develop-sandbox-application}

In questa sezione, ora che il modello è stato impostato nella sezione [applicazione iniziale](initial-app.md) e nelle pagine iniziali stabilite nella sezione [contenuto iniziale](initial-content.md), l&#39;applicazione può essere sviluppata utilizzando script di base, inclusa la possibilità di abilitare l&#39;authoring con i componenti Community. Alla fine di questa sezione, il sito Web sarà funzionale.

## Utilizzo degli script di pagina di Foundation {#using-foundation-page-scripts}

Lo script predefinito, creato al momento dell&#39;aggiunta del componente che esegue il rendering del modello della pagina di riproduzione, viene modificato in modo da includere il file head.jsp della pagina di base e il file body.jsp locale.

### Super Resource Type {#super-resource-type}

Il primo passaggio consiste nell&#39;aggiungere una proprietà super type della risorsa al nodo `/apps/an-scf-sandbox/components/playpage` in modo che erediti gli script e le proprietà del super type.

Utilizzo del CRXDE Lite:

1. Selezionare il nodo `/apps/an-scf-sandbox/components/playpage`.
1. Nella scheda Proprietà, immettere una nuova proprietà con i seguenti valori:

   Nome: `sling:resourceSuperType`

   Tipo: `String`

   Valore: `foundation/components/page`

1. Fare clic sul pulsante verde **[!UICONTROL +Aggiungi]**.
1. Fare clic su **[!UICONTROL Salva tutto]**.

   ![pageScript](assets/page-script.png)

### Script head e body {#head-and-body-scripts}

1. Nel riquadro **CRXDE Lite** dell&#39;elenco delle cartelle, passare a `/apps/an-scf-sandbox/components/playpage` e fare doppio clic sul file `playpage.jsp` per aprirlo nel riquadro di modifica.

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

   Con un super tipo di `foundation/components/page`, qualsiasi script non definito nella stessa cartella verrà risolto in uno script nella cartella `/apps/foundation/components/page` (se presente), in uno script nella cartella `/libs/foundation/components/page`.

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

1. Lo script di base `head.jsp` non deve essere sovrapposto, ma lo script di base `body.jsp` è vuoto.

   Per impostare l’authoring, sovrapponete `body.jsp` con uno script locale e includete un sistema paragrafo (parsys) nel corpo:

   1. Accedi a `/apps/an-scf-sandbox/components`.
   1. Selezionare il nodo `playpage`.
   1. Fare clic con il pulsante destro del mouse e selezionare `Create > Create File...`

      * Nome: **body.jsp**
   1. Fare clic su **[!UICONTROL Salva tutto]**.

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

1. Fare clic su **[!UICONTROL Salva tutto]**.

**Visualizzare la pagina in un browser in modalità di modifica:**

* Interfaccia standard: [http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.html](http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.md)

È consigliabile non solo visualizzare l&#39;intestazione **Riproduzione community**, ma anche l&#39;interfaccia utente per la modifica del contenuto della pagina.

Il pannello laterale Risorse/Componente viene visualizzato quando il pannello laterale è aperto e la finestra è sufficientemente ampia da consentire la visualizzazione del contenuto laterale e del contenuto della pagina.

![view-page](assets/view-page.png)

* Interfaccia classica: [http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html](http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html)

Di seguito viene illustrata l’aspetto della pagina di riproduzione nell’interfaccia classica, incluso con Content Finder (cf):

![play-page-view](assets/play-page-view.png)

## Componenti di Communities {#communities-components}

Per abilitare i componenti di Communities per la creazione, attenetevi alle istruzioni seguenti:

* [Accesso ai componenti Community](basics.md#accessing-communities-components)

Ai fini di questa sandbox, iniziate con i seguenti componenti **Communities** (attivabili selezionando la casella):

* Commenti
* Forum
* Valutazione
* Recensioni
* Riepilogo recensioni (visualizzazione)
* Votazione

Inoltre, scegliete i componenti **[!UICONTROL Generale]**, ad esempio

* Immagine
* Tabella
* Testo
* Titolo (Foundation)

>[!NOTE]
>
>I componenti abilitati per la pari pagina vengono memorizzati nella directory archivio come valore della proprietà `components` della variabile
>
>`/etc/designs/an-scf-sandbox/jcr:content/playpage/par` node.

## Pagina di destinazione {#landing-page}

In un ambiente multilingue, la pagina principale includerebbe uno script che analizzerebbe la richiesta del client per determinare la lingua preferita.

In questo semplice esempio, la pagina principale viene impostata statisticamente per reindirizzare alla pagina inglese, che in futuro potrebbe essere la pagina di destinazione principale con un collegamento alla pagina di riproduzione.

Modificate l’URL del browser nella pagina principale: [http://localhost:4502/editor.html/content/an-scf-sandbox.html](https://locahost:4502/editor.html/content/an-scf-sandbox.html)

* Selezionate l’icona Informazioni pagina
* Selezionare **[!UICONTROL Apri proprietà]**
* Nella scheda AVANZATE

   * Per la voce Redirect, individuare **[!UICONTROL Siti Web]** > **[!UICONTROL Siti sandbox SCF]** > **[!UICONTROL SCF Sandbox]**
   * Fai clic su **[!UICONTROL OK]**

* Fai clic su **[!UICONTROL OK]**

Una volta pubblicato il sito, quando si passa alla pagina principale di un’istanza di pubblicazione si passa alla pagina inglese.

L&#39;ultimo passaggio prima di giocare con i componenti SCF delle community è aggiungere una cartella libreria client (clientlibs) .... [Aggiungi Clienlibs](add-clientlibs.md)