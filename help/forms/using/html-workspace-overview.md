---
title: Utilizzo dell’area di lavoro  AEM Forms
seo-title: Utilizzo dell’area di lavoro  AEM Forms
description: Scopri 'area di lavoro AEM Forms con questa panoramica rapida dei flussi di lavoro dei processi.
seo-description: Scopri 'area di lavoro AEM Forms con questa panoramica rapida dei flussi di lavoro dei processi.
uuid: 36381e7b-1533-459c-80de-92e806a49cd5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 866cd9cb-6661-4b0f-a3af-e39453e6e51b
docset: aem65
translation-type: tm+mt
source-git-commit: 21efe30c6a69d04c737bc523aeaab504db8f605b
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 0%

---


# Utilizzo dell&#39;area di lavoro  AEM Forms{#working-with-aem-forms-workspace}

## Introduzione {#introduction}

&#39;area di lavoro di AEM Forms fa parte di  AEM Forms. Workspace facilita la rappresentazione di Forms HTML oltre ai PDF forms. Ora puoi partecipare ai processi aziendali dalle interfacce mobili e dalle applicazioni Web.

Inoltre, &#39;area di lavoro AEM Forms è altamente personalizzabile utilizzando le metodologie di sviluppo standard HTML e JavaScript™. È un software basato su componenti che si integra facilmente con le altre applicazioni Web.

Per ulteriori informazioni, vedere [Introduzione a  area di lavoro AEM Forms](/help/forms/using/introduction-html-workspace.md).

## Acquisizione familiare {#getting-familiar}

Per acquisire familiarità con il processo end-to-end di creazione di un&#39;applicazione di moduli per automatizzare un processo aziendale, seguire la procedura dettagliata. È possibile creare, gestire e testare un&#39;applicazione utilizzando Workbench, Designer e &#39;area di lavoro AEM Forms dopo aver completato la procedura dettagliata. Per informazioni dettagliate sull&#39;implementazione, vedere [Creazione della prima applicazione AEM Forms ](https://help.adobe.com/en_US/livecycle/11.0/CreateFirstApp/index.html).

## Panoramica funzionale {#functional-overview}

È possibile utilizzare  area di lavoro AEM Forms per eseguire le seguenti operazioni:

**Avvio di un processo aziendale:** &#39;area di lavoro AEM Forms identifica i processi come progettati e configurati dall&#39;organizzazione. Potete preferire le categorie utilizzate di frequente per accedere rapidamente alle categorie. Quando si avvia un processo, in genere si compila un modulo per avviare un processo aziendale che controlla il flusso di lavoro dei moduli. Per ulteriori informazioni, vedere [Avvio dei processi](/help/forms/using/starting-processes.md).

**Visualizzare e agire sulle attività:** Quando si visualizzano gli elenchi A-do, vengono visualizzate le attività da un processo aziendale assegnato all&#39;utente, a qualsiasi gruppo a cui appartenete o che sono le attività condivise di altri utenti. È possibile aprire, lavorare e completare le attività come necessario. In genere, completare un&#39;attività comporta fornire informazioni, approvare un modulo o rifiutare un modulo. Per ulteriori informazioni, vedere [Uso degli elenchi delle operazioni da eseguire](/help/forms/using/todo-lists.md).

**Tenere traccia delle attività**: Per tenere traccia delle attività, è possibile utilizzare la scheda Tracciamento &#39;area di lavoro AEM Forms. Potete cercare i processi attivi o completati avviati o ai quali avete partecipato. È possibile visualizzare le attività, le assegnazioni e i moduli che facevano parte del processo. È inoltre possibile avviare nuovi processi utilizzando i dati del modulo provenienti da un processo avviato in precedenza. Per ulteriori informazioni, vedere [Processi di tracciamento](/help/forms/using/tracking-processes.md).

## Nuova offerta  area di lavoro AEM Forms {#new-offering-of-aem-forms-workspace}

**Supporto per l&#39;approvazione in blocco delle attività**:

È possibile approvare più attività dello stesso tipo. Dopo aver selezionato un&#39;attività per l&#39;approvazione, rimangono abilitate solo le attività con lo stesso processo, con gli stessi nomi di attività e le stesse opzioni di route. Per informazioni dettagliate sull&#39;implementazione, vedere [Utilizzo degli elenchi delle attività da eseguire](/help/forms/using/todo-lists.md).

## Migrazione da Flex Workspace a  area di lavoro AEM Forms {#migrating-from-flex-workspace-to-aem-forms-workspace}

Flex Workspace non è supportato per  clienti AEM Forms. Tutti i clienti che utilizzano Flex Workspace devono passare a  AEM Forms Workspace.

Nell&#39;area di lavoro  AEM Forms, i servizi di rendering e invio predefiniti, nel profilo azione predefinito, associati ai moduli XDP, sono stati modificati e sono stati introdotti nuovi servizi. Per informazioni dettagliate, consultate [Nuovo servizio di rendering e invio](/help/forms/using/new-render-submit-service.md). Per migrare i processi esistenti, che utilizzano i moduli XDP, è possibile seguire [i passaggi indicati di seguito](new-render-submit-service.md).

**Mappatura delle personalizzazioni di Flex Workspace con  area di lavoro AEM Forms**

La mappatura tra i vari tipi di personalizzazioni in entrambe le aree di lavoro è la seguente.

<table>
 <tbody>
  <tr>
   <td><strong>Tipo di personalizzazione </strong></td>
   <td><strong>Personalizzazioni coperte </strong></td>
   <td><strong>Corrispondente scenario di personalizzazione 'area di lavoro AEM Forms</strong></td>
  </tr>
  <tr>
   <td>Personalizzazione della localizzazione</td>
   <td>
    <ol>
     <li>Modifica delle impostazioni internazionali di Workspace</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/changing-locale-user-interface.md">Modifica  impostazioni internazionali area di lavoro AEM Forms</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Personalizzazione tema</td>
   <td>
    <ol>
     <li>Sostituzione delle immagini</li>
     <li>Modifica dei colori</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/changing-organization-logo-branding.md">Modifica del logo dell'organizzazione</a> </li>
     <li><a href="/help/forms/using/changing-color-scheme-interface.md">Modifica combinazione di colori</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Personalizzazione del layout</td>
   <td>
    <ol>
     <li>Semplificazione dell'interfaccia utente di Workspace<br /> </li>
     <li>Creazione di una nuova schermata di login</li>
     <li>Creazione di un contenitore di approvazione personalizzato</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/description-reusable-components.md">Utilizzo di componenti riutilizzabili</a></li>
     <li><a href="/help/forms/using/creating-new-login-screen.md">Creazione di una nuova schermata di login</a></li>
     <li>Il contenitore di approvazione è obsoleto.</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

Alcune delle funzioni di Flex Workspace non disponibili &#39;area di lavoro di AEM Forms includono: messaggi e notifiche, pagina di benvenuto, contenitore di approvazione e opzione per gestire le intestazioni di colonna. Per un elenco completo, vedere [Funzioni di Flex Workspace non disponibili &#39;area di lavoro di AEM Forms](/help/forms/using/features-flex-workspace-available-html.md).

## Sviluppo con  area di lavoro AEM Forms {#developing-with-aem-forms-workspace}

### Architettura {#architecture}

&#39;area di lavoro AEM Forms è un&#39;applicazione Web basata su HTML e JavaScript™ ospitata su CRX™. Quando l&#39;URL Workspace viene aperto in un browser, si accede a una risorsa CRX™ e l&#39;applicazione viene rappresentata come una pagina HTML nel browser. Le librerie JavaScript e il codice JavaScript personalizzato gestiscono il comportamento interno ed esterno dell&#39;applicazione, ad esempio l&#39;interfaccia utente, l&#39;interazione con l&#39;utente e la comunicazione con  server AEM Forms. Per ulteriori dettagli, vedere  area di lavoro AEM Forms [Architecture](/help/forms/using/html-workspace-architecture.md).

### Personalizzazione  area di lavoro AEM Forms {#aem-forms-workspace-customization}

&#39;area di lavoro di AEM Forms supporta un&#39;ampia gamma di personalizzazioni per aggiornare il layout dell&#39;interfaccia utente, il suo aspetto, le sue funzionalità e molto altro ancora. Le personalizzazioni richiedono l&#39;aggiornamento di uno o più dei seguenti elementi:

* Aspetto dell’interfaccia utente
* Funzionalità mediante personalizzazioni semantiche
* Riutilizzo di componenti HTML in altre applicazioni Web

L&#39;articolo [customization](introduction-customizing-html-workspace.md#types-of-customizations) spiega i tipi di tali personalizzazioni.

### Configurare l&#39;ambiente sviluppatore {#set-up-the-developer-environment}

 risultati finali dell&#39;area di lavoro di AEM Forms includono un pacchetto CRX distribuito su CRX, un archivio SDK contenente il codice sorgente completo, librerie JavaScript di terze parti e script di creazione &#39;area di lavoro di AEM Forms. Utilizzate queste opzioni per configurare l&#39;ambiente di sviluppo per eseguire le personalizzazioni di cui sopra. Per ulteriori dettagli, vedere [Creazione  codice dell&#39;area di lavoro AEM Forms](introduction-customizing-html-workspace.md#building-html-workspace-code).

È possibile personalizzare una parte importante dell&#39;interfaccia e delle funzionalità di base come font, combinazione di colori, logo, schermata di login, finestre di dialogo degli errori, integrazione con applicazioni di terze parti e riutilizzo di componenti in applicazioni di terze parti. È inoltre possibile migliorare il contenuto visualizzato nella pagina Riepilogo attività, visualizzare immagini per le azioni di route delle attività e persino modificare i modelli e le viste di livello inferiore che creano l&#39;applicazione dell&#39;area di lavoro di AEM Forms .

### Rendering HTML di Forms XDP {#html-rendering-of-xdp-forms}

Per impostazione predefinita, per un nuovo processo, viene eseguito il rendering di un modulo XDP in formato PDF su computer desktop e in formato HTML su un tablet. È possibile eseguire sempre il rendering di un modulo XDP in formato HTML. Per informazioni dettagliate, vedere [New Render and Submit Services](/help/forms/using/new-render-submit-service.md).

[La funzione ](https://helpx.adobe.com/livecycle/help/mobile-forms/introduction.html) Moduli mobili, che funziona con  [i profili](https://helpx.adobe.com/livecycle/help/mobile-forms/creating-profile.html), consente la rappresentazione HTML dei moduli XDP. Per impostazione predefinita, l&#39;opzione &quot;Rendering nuovo modulo HTML&quot; utilizza il profilo `default.html` che è possibile modificare. È inoltre possibile aggiungere modifiche personalizzate prima del rendering di un modulo XDP in formato HTML.

##  app area di lavoro AEM Forms {#aem-forms-workspace-app}

Per lavorare sui processi aziendali su un dispositivo mobile, potete utilizzare l&#39;app dell&#39;area di lavoro AEM Forms  offerta di  AEM Forms. Per ulteriori informazioni, consultate la [ panoramica dell&#39;app dell&#39;area di lavoro AEM Forms](https://helpx.adobe.com/livecycle/help/mobile-workspace/mobile-workspace-overview.html).
