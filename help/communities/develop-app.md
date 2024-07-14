---
title: Sviluppa applicazione sandbox
description: Scopri come sviluppare un’applicazione Sandbox che utilizza script di base e include la possibilità di abilitare l’authoring con i componenti di Communities.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 7ac0056c-a742-49f4-8312-2cf90ab9f23a
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 2%

---

# Sviluppa applicazione sandbox  {#develop-sandbox-application}

In questa sezione, ora che il modello è configurato nella sezione [applicazione iniziale](initial-app.md) e che le pagine iniziali sono state stabilite nella sezione [contenuto iniziale](initial-content.md), è possibile sviluppare l&#39;applicazione. A tale scopo, puoi utilizzare script di base che includono la possibilità di abilitare l’authoring con i componenti di Communities. Alla fine di questa sezione, il sito Web è completamente funzionante.

## Utilizzo degli script di pagina di Foundation {#using-foundation-page-scripts}

Lo script predefinito, creato quando è stato aggiunto il componente che esegue il rendering del modello di pagina playlist, viene modificato per includere il file head.jsp della pagina di base e un body.jsp locale.

### Tipo di risorsa super {#super-resource-type}

Il primo passaggio consiste nell&#39;aggiungere una proprietà del super tipo di risorsa al nodo `/apps/an-scf-sandbox/components/playpage` in modo che erediti gli script e le proprietà del super tipo.

Utilizzo di CRXDE Lite:

1. Selezionare il nodo `/apps/an-scf-sandbox/components/playpage`.
1. Nella scheda delle proprietà, immetti una nuova proprietà con i seguenti valori:

   Nome: `sling:resourceSuperType`

   Tipo: `String`

   Valore: `foundation/components/page`

1. Fai clic sul pulsante verde **[!UICONTROL +Aggiungi]**.
1. Fare clic su **[!UICONTROL Salva tutto]**.

   ![script-pagina](assets/page-script.png)

### Script per la testa e il corpo {#head-and-body-scripts}

1. Nel riquadro Esplora risorse **CRXDE Liti** passare a `/apps/an-scf-sandbox/components/playpage` e fare doppio clic sul file `playpage.jsp` per aprirlo nel riquadro di modifica.

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

1. Tenendo conto dei tag script aperti/chiusi, sostituire &quot; // TODO ...&quot; con `includes` di script per le parti head e body di &lt;html>.

   Con un super tipo di `foundation/components/page`, qualsiasi script non definito nella stessa cartella viene risolto in uno script nella cartella `/apps/foundation/components/page` (se esiste) o in uno script nella cartella `/libs/foundation/components/page`.

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

1. La sovrapposizione dello script di Foundation `head.jsp` non è necessaria, ma lo script di Foundation `body.jsp` è vuoto.

   Per configurare per l&#39;authoring, sovrapporre `body.jsp` con uno script locale e includere un sistema paragrafo (parsys) nel corpo:

   1. Accedi a `/apps/an-scf-sandbox/components`.
   1. Selezionare il nodo `playpage`.
   1. Fare clic con il pulsante destro del mouse e selezionare `Create > Create File...`

      * Nome: **body.jsp**

   1. Fare clic su **[!UICONTROL Salva tutto]**.

   Apri `/apps/an-scf-sandbox/components/playpage/body.jsp` e incolla il seguente testo:

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

**Visualizza la pagina in un browser in modalità di modifica:**

* Interfaccia utente standard: `http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.html`

Dovresti visualizzare non solo l&#39;intestazione **Riproduzione community**, ma anche l&#39;interfaccia utente per la modifica del contenuto della pagina.

Il pannello laterale Assets/Componente viene visualizzato quando entrambi i pannelli laterali sono aperti e la finestra è sufficientemente ampia da consentire la visualizzazione sia del contenuto laterale che del contenuto della pagina.

![visualizza-pagina](assets/view-page.png)

* Interfaccia classica: `http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html`

Di seguito è riportato l’aspetto della pagina di riproduzione nell’interfaccia classica, incluso con content finder (cf):

![visualizzazione pagina di riproduzione](assets/play-page-view.png)

## Componenti community {#communities-components}

Per abilitare i componenti Community per l’authoring, inizia seguendo queste istruzioni:

* [Accesso ai componenti delle community](basics.md#accessing-communities-components)

Ai fini di questa sandbox, inizia con questi **componenti Communities** (attivali selezionando la casella):

* Commenti
* Forum
* Valutazione
* Recensioni
* Riepilogo recensioni (visualizzazione)
* Votazione

Inoltre, scegli **[!UICONTROL Componenti generali]**, ad esempio

* Immagine
* Tabella
* Testo
* Titolo (fondazione)

>[!NOTE]
>
>I componenti abilitati per la parte page vengono memorizzati nell&#39;archivio come valore della proprietà `components` della proprietà
>
>Nodo `/etc/designs/an-scf-sandbox/jcr:content/playpage/par`.

## Pagina di destinazione {#landing-page}

In un ambiente multilingue, la pagina principale includerebbe uno script che analizzerebbe la richiesta del client per determinare la lingua preferita.

In questo esempio, la pagina principale viene impostata in modo statico per il reindirizzamento alla pagina inglese, che potrebbe essere sviluppata in futuro come pagina di destinazione principale con un collegamento alla pagina di riproduzione.

Cambia l&#39;URL del browser nella pagina principale: `http://localhost:4502/editor.html/content/an-scf-sandbox.html`

* Seleziona l’icona Informazioni pagina
* Seleziona **[!UICONTROL Apri proprietà]**
* Nella scheda AVANZATE

   * Per la voce di reindirizzamento, passa a **[!UICONTROL Siti Web]** > **[!UICONTROL Sito Sandbox SCF]** > **[!UICONTROL Sandbox SCF]**
   * Fai clic su **[!UICONTROL OK]**

* Fai clic su **[!UICONTROL OK]**

Dopo la pubblicazione del sito, l’accesso alla pagina principale di un’istanza Publish viene reindirizzato alla pagina inglese.

L’ultimo passaggio prima di riprodurlo con i componenti SCF di Communities è aggiungere una .... Cartella libreria client (clientlibs) [Aggiungi Clientlibs](add-clientlibs.md)
