---
title: Utilizzo dell’area di lavoro di AEM Forms
seo-title: Working with AEM Forms workspace
description: Inizia a usare l’area di lavoro di AEM Forms con questa rapida panoramica dei flussi di lavoro del processo.
seo-description: Get started with AEM Forms workspace with this quick overview of the process workflows.
uuid: 36381e7b-1533-459c-80de-92e806a49cd5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 866cd9cb-6661-4b0f-a3af-e39453e6e51b
docset: aem65
exl-id: 0bedcbd9-2cf8-47da-9440-c773982e550c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 0%

---

# Utilizzo dell’area di lavoro di AEM Forms{#working-with-aem-forms-workspace}

## Introduzione {#introduction}

L’area di lavoro di AEM Forms fa parte di AEM Forms. Workspace facilita il rendering di HTML Forms oltre ai PDF forms. Ora puoi interagire con i processi aziendali dalle interfacce mobili e dalle applicazioni web.

Inoltre, lo spazio di lavoro AEM Forms è altamente personalizzabile utilizzando le metodologie di sviluppo standard HTML e JavaScript™. Si tratta di un software basato su componenti che si integra facilmente con le altre applicazioni web.

Per ulteriori informazioni, consulta [Introduzione all’area di lavoro di AEM Forms](/help/forms/using/introduction-html-workspace.md).

## Acquisire familiarità {#getting-familiar}

Per acquisire familiarità con il processo end-to-end di creazione di un&#39;applicazione forms per automatizzare un processo aziendale, seguire la procedura dettagliata. È possibile creare, gestire e testare un&#39;applicazione utilizzando Workbench, Designer e l&#39;area di lavoro di AEM Forms dopo aver seguito la procedura dettagliata. Per informazioni dettagliate sull’implementazione, consulta [Creazione della prima applicazione AEM Forms](https://help.adobe.com/en_US/livecycle/11.0/CreateFirstApp/index.html).

## Panoramica funzionale {#functional-overview}

È possibile utilizzare l’area di lavoro di AEM Forms per eseguire le seguenti attività:

**Avviare un processo aziendale:** L’area di lavoro di AEM Forms categorie i processi come progettati e configurati dalla tua organizzazione. È possibile preferire le categorie utilizzate di frequente per accedere rapidamente alle categorie. Quando si avvia un processo, in genere si compila un modulo per avviare un processo aziendale che controlla il flusso di lavoro dei moduli. Per ulteriori informazioni, consulta [Avvio dei processi](/help/forms/using/starting-processes.md).

**Visualizza ed agisce in base alle attività:** Quando si visualizzano gli elenchi A-do, vengono visualizzate le attività di un processo aziendale assegnato all&#39;utente o a qualsiasi gruppo a cui l&#39;utente appartiene o che sono le attività condivise di altri utenti. È possibile aprire, lavorare e completare le attività in base alle esigenze. In genere, per completare un’attività è necessario fornire informazioni, approvare un modulo o rifiutare un modulo. Per ulteriori informazioni, consulta [Utilizzo degli elenchi A-do](/help/forms/using/todo-lists.md).

**Tracciare le attività**: Per tenere traccia delle attività, utilizza la scheda Tracking dell’area di lavoro di AEM Forms. Puoi cercare i processi attivi o completati avviati o a cui hai partecipato. È possibile visualizzare le attività, le assegnazioni e i moduli inclusi nel processo. È inoltre possibile avviare nuovi processi utilizzando i dati del modulo da un processo avviato in precedenza. Per ulteriori informazioni, consulta [Tracciamento dei processi](/help/forms/using/tracking-processes.md).

## Nuova offerta di AEM Forms Workspace {#new-offering-of-aem-forms-workspace}

**Sostegno all&#39;approvazione in blocco delle attività**:

È possibile approvare più attività dello stesso tipo. Dopo aver selezionato un&#39;attività per l&#39;approvazione, rimangono abilitate solo le attività con lo stesso processo, con gli stessi nomi di attività e le stesse opzioni di route. Vedi [Utilizzo degli elenchi Da fare](/help/forms/using/todo-lists.md) per i dettagli di implementazione.

## Migrazione da Flex Workspace all’area di lavoro AEM Forms {#migrating-from-flex-workspace-to-aem-forms-workspace}

Flex Workspace non è supportato dai clienti AEM Forms. Tutti i clienti che utilizzano Flex Workspace devono passare ad AEM Forms Workspace.

Nell’area di lavoro di AEM Forms, i servizi di rendering e invio predefiniti, nel profilo di azione predefinito, associati ai moduli XDP, sono stati modificati e sono stati introdotti nuovi servizi. Per maggiori dettagli, vedi [Nuovo servizio di rendering e invio](/help/forms/using/new-render-submit-service.md). Per migrare i processi esistenti che funzionano con i moduli XDP, per utilizzare questi servizi, puoi seguire [questi passaggi](new-render-submit-service.md).

**Mappatura delle personalizzazioni di Flex Workspace con l’area di lavoro di AEM Forms**

La mappatura tra i vari tipi di personalizzazioni in entrambe le aree di lavoro è la seguente.

<table>
 <tbody>
  <tr>
   <td><strong>Tipo di personalizzazione </strong></td>
   <td><strong>Personalizzazioni coperte </strong></td>
   <td><strong>Scenario di personalizzazione dell’area di lavoro AEM Forms corrispondente</strong></td>
  </tr>
  <tr>
   <td>Personalizzazione della localizzazione</td>
   <td>
    <ol>
     <li>Modifica delle impostazioni internazionali di Workspace</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/changing-locale-user-interface.md">Modifica delle impostazioni internazionali dell’area di lavoro di AEM Forms</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Personalizzazione del tema</td>
   <td>
    <ol>
     <li>Sostituzione delle immagini</li>
     <li>Modifica dei colori</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/changing-organization-logo-branding.md">Modifica del logo dell'organizzazione</a> </li>
     <li><a href="/help/forms/using/changing-color-scheme-interface.md">Modifica della combinazione di colori</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>Personalizzazione del layout</td>
   <td>
    <ol>
     <li>Semplificazione dell’interfaccia utente di Workspace<br /> </li>
     <li>Creazione di una nuova schermata di accesso</li>
     <li>Creazione di un contenitore di approvazione personalizzato</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/description-reusable-components.md">Utilizzo dei componenti riutilizzabili</a></li>
     <li><a href="/help/forms/using/creating-new-login-screen.md">Creazione di una nuova schermata di accesso</a></li>
     <li>Il contenitore di approvazione è obsoleto.</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

Alcune delle funzioni di Flex Workspace non disponibili nell’area di lavoro di AEM Forms includono: messaggi e notifiche, pagina di benvenuto, contenitore di approvazione e opzione per gestire le intestazioni di colonna. Per un elenco completo, vedi [Funzioni di Flex Workspace non disponibili nell’area di lavoro di AEM Forms](/help/forms/using/features-flex-workspace-available-html.md).

## Sviluppo con l’area di lavoro AEM Forms {#developing-with-aem-forms-workspace}

### Architettura {#architecture}

AEM Forms workspace è un&#39;applicazione web basata su HTML e JavaScript™ ospitata su CRX™. Quando l&#39;URL Workspace viene aperto in un browser, si accede a una risorsa CRX™ e l&#39;applicazione viene riprodotta come pagina HTML nel browser. Le librerie JavaScript e il codice JavaScript personalizzato gestiscono il comportamento interno ed esterno dell&#39;applicazione, ad esempio l&#39;interfaccia utente, l&#39;interazione dell&#39;utente e la comunicazione con il server AEM Forms. Per ulteriori dettagli, consulta Area di lavoro di AEM Forms [architettura](/help/forms/using/html-workspace-architecture.md).

### Personalizzazione dell’area di lavoro AEM Forms {#aem-forms-workspace-customization}

L’area di lavoro di AEM Forms supporta un’ampia varietà di personalizzazioni per aggiornare il layout dell’interfaccia utente, il suo aspetto, le sue funzionalità e molto altro. Le personalizzazioni comportano l’aggiornamento di uno o più dei seguenti elementi:

* Aspetto dell’interfaccia utente
* Funzionalità tramite personalizzazioni semantiche
* Riutilizzo dei componenti di HTML in altre applicazioni web

La [personalizzazione](introduction-customizing-html-workspace.md#types-of-customizations) articolo spiega i tipi di tali personalizzazioni.

### Configurare l’ambiente di sviluppo {#set-up-the-developer-environment}

I risultati finali dell&#39;area di lavoro di AEM Forms includono un pacchetto CRX distribuito su CRX, un archivio SDK contenente il codice sorgente completo, le librerie JavaScript di terze parti e gli script di creazione dell&#39;area di lavoro di AEM Forms. Utilizzali per configurare l’ambiente di sviluppo per eseguire le personalizzazioni di cui sopra. Per ulteriori dettagli, consulta [Creazione del codice dell’area di lavoro di AEM Forms](introduction-customizing-html-workspace.md#building-html-workspace-code).

È possibile personalizzare una parte principale dell’interfaccia e delle funzionalità di base, ad esempio font, combinazione di colori, logo, schermata di accesso, finestre di dialogo degli errori, integrazione con applicazioni di terze parti e riutilizzo di componenti in applicazioni di terze parti. È inoltre possibile migliorare il contenuto visualizzato nella pagina Riepilogo attività, mostrare le immagini per le azioni di route delle attività e persino modificare i modelli e le visualizzazioni di livello inferiore che creano l&#39;applicazione dell&#39;area di lavoro AEM Forms.

### Rendering HTML di XDP Forms {#html-rendering-of-xdp-forms}

Per impostazione predefinita, per un nuovo processo, viene eseguito il rendering di un modulo XDP in formato PDF su un computer desktop e in formato HTML su un tablet. È sempre possibile eseguire il rendering di un modulo XDP in formato HTML. Per maggiori dettagli, vedi [Nuovi servizi di rendering e invio](/help/forms/using/new-render-submit-service.md).

[Forms mobile](https://helpx.adobe.com/livecycle/help/mobile-forms/introduction.html) funzionalità, compatibile con [profiles](https://helpx.adobe.com/livecycle/help/mobile-forms/creating-profile.html), abilita il rendering HTML dei moduli XDP. Per impostazione predefinita, l’opzione &quot;Rendering nuovo modulo HTML&quot; utilizza `default.html` profilo, che puoi modificare. È inoltre possibile aggiungere modifiche personalizzate prima di eseguire il rendering di un modulo XDP in formato HTML.

## App Workspace AEM Forms {#aem-forms-workspace-app}

Per lavorare sui processi aziendali su un dispositivo mobile, puoi utilizzare l’offerta dell’app Workspace AEM Forms di AEM Forms. Per ulteriori informazioni, consulta la sezione [Panoramica dell’app nell’area di lavoro AEM Forms](https://helpx.adobe.com/livecycle/help/mobile-workspace/mobile-workspace-overview.html).
