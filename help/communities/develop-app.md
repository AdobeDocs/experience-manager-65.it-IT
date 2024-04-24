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

In questa sezione, ora che il modello è configurato nel [applicazione iniziale](initial-app.md) e le pagine iniziali definite nella sezione [contenuto iniziale](initial-content.md) sezione, puoi sviluppare l’applicazione. A tale scopo, puoi utilizzare script di base che includono la possibilità di abilitare l’authoring con i componenti di Communities. Alla fine di questa sezione, il sito Web è completamente funzionante.

## Utilizzo degli script di pagina di Foundation {#using-foundation-page-scripts}

Lo script predefinito, creato quando è stato aggiunto il componente che esegue il rendering del modello di pagina playlist, viene modificato per includere il file head.jsp della pagina di base e un body.jsp locale.

### Tipo di risorsa super {#super-resource-type}

Il primo passaggio consiste nell’aggiungere una proprietà di super tipo della risorsa al `/apps/an-scf-sandbox/components/playpage` in modo che erediti gli script e le proprietà del super-tipo.

Utilizzo di CRXDE Liti:

1. Seleziona nodo `/apps/an-scf-sandbox/components/playpage`.
1. Nella scheda delle proprietà, immetti una nuova proprietà con i seguenti valori:

   Nome: `sling:resourceSuperType`

   Tipo: `String`

   Valore: `foundation/components/page`

1. Fai clic sul pulsante verde **[!UICONTROL +Aggiungi]** pulsante.
1. Clic **[!UICONTROL Salva tutto]**.

   ![page-script](assets/page-script.png)

### Script per la testa e il corpo {#head-and-body-scripts}

1. In entrata **CRXDE Liti** riquadro di esplorazione, passare a `/apps/an-scf-sandbox/components/playpage` e fare doppio clic sul file `playpage.jsp` per aprirlo nel riquadro di modifica.

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

1. Tenendo conto dei tag script aperti/chiusi, sostituisci &quot; // TODO ...&quot; con `includes` di script per le parti della testa e del corpo di &lt;html>.

   Con un super tipo di `foundation/components/page`, qualsiasi script non definito nella stessa cartella viene risolto in uno script in `/apps/foundation/components/page` cartella (se esiste), oppure a uno script in `/libs/foundation/components/page` cartella.

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

1. Sovrapposizione dello script di base `head.jsp` non è necessario, ma lo script di foundation `body.jsp` è vuoto.

   Per impostare per l’authoring, sovrapponi `body.jsp` con uno script locale e includere un sistema paragrafo (parsys) nel corpo:

   1. Accedi a `/apps/an-scf-sandbox/components`.
   1. Seleziona la `playpage` nodo.
   1. Fai clic con il pulsante destro del mouse e seleziona (Copia negli Appunti) `Create > Create File...`

      * Nome: **body.jsp**

   1. Clic **[!UICONTROL Salva tutto]**.

   Apri `/apps/an-scf-sandbox/components/playpage/body.jsp` e incolla il testo seguente:

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

1. Clic **[!UICONTROL Salva tutto]**.

**Visualizza la pagina in un browser in modalità di modifica:**

* Interfaccia utente standard: `http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.html`

Non dovresti vedere solo l’intestazione **Community Play**, ma anche l’interfaccia utente per la modifica del contenuto della pagina.

Il pannello laterale Risorse/Componenti viene visualizzato quando entrambi i pannelli laterali sono aperti e la finestra è sufficientemente ampia da consentire la visualizzazione sia del contenuto laterale che del contenuto della pagina.

![view-page](assets/view-page.png)

* Interfaccia classica: `http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html`

Di seguito è riportato l’aspetto della pagina di riproduzione nell’interfaccia classica, incluso con content finder (cf):

![play-page-view](assets/play-page-view.png)

## Componenti community {#communities-components}

Per abilitare i componenti Community per l’authoring, inizia seguendo queste istruzioni:

* [Accesso ai componenti delle community](basics.md#accessing-communities-components)

Ai fini di questa sandbox, inizia con questi **Community** componenti (abilitare selezionando la casella):

* Commenti
* Forum
* Valutazione
* Recensioni
* Riepilogo recensioni (visualizzazione)
* Votazione

Inoltre, scegli **[!UICONTROL Generale]** componenti, come

* Immagine
* Tabella
* Testo
* Titolo (fondazione)

>[!NOTE]
>
>I componenti abilitati per la parte page vengono memorizzati nell’archivio come valore della proprietà `components` proprietà del
>
>Nodo `/etc/designs/an-scf-sandbox/jcr:content/playpage/par`.

## Pagina di destinazione {#landing-page}

In un ambiente multilingue, la pagina principale includerebbe uno script che analizzerebbe la richiesta del client per determinare la lingua preferita.

In questo esempio, la pagina principale viene impostata in modo statico per il reindirizzamento alla pagina inglese, che potrebbe essere sviluppata in futuro come pagina di destinazione principale con un collegamento alla pagina di riproduzione.

Modifica l’URL del browser con la pagina root: `http://localhost:4502/editor.html/content/an-scf-sandbox.html`

* Seleziona l’icona Informazioni pagina
* Seleziona **[!UICONTROL Apri proprietà]**
* Nella scheda AVANZATE

   * Per la voce Reindirizza, selezionare **[!UICONTROL Siti Web]** > **[!UICONTROL Sito sandbox SCF]** > **[!UICONTROL Sandbox SCF]**
   * Clic **[!UICONTROL OK]**

* Clic **[!UICONTROL OK]**

Dopo la pubblicazione del sito, l’accesso alla pagina principale di un’istanza Publish viene reindirizzato alla pagina inglese.

L’ultimo passaggio prima di riprodurlo con i componenti SCF di Communities è aggiungere una .... Cartella libreria client (clientlibs) [Aggiungi Clientlibs](add-clientlibs.md)
