---
title: Azioni e funzionalità dei flussi di lavoro AEM incentrati sui moduli sui flussi di lavoro OSGi e JEE per AEM Forms
description: Azioni e funzionalità dei flussi di lavoro AEM incentrati sui moduli sui flussi di lavoro OSGi e JEE per AEM Forms
contentOwner: khsingh
exl-id: 505b8988-b2b3-4222-b3cb-9b3c6259fdd2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 23%

---

# Azioni e funzionalità dei flussi di lavoro AEM incentrati sui moduli sui flussi di lavoro OSGi e JEE per AEM Forms {#actions-and-capabilities-of-form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

## Casella in entrata AEM e HTML Workspace {#aem-inbox-and-html-workspace}

È possibile utilizzare AEM casella in entrata per eseguire e monitorare i flussi di lavoro AEM incentrati su Forms su OSGi. HTML Workspace consente invece di eseguire e monitorare i flussi di lavoro JEE di AEM Forms. La tabella seguente ti aiuta a comprendere varie azioni importanti disponibili nella AEM casella in entrata per flussi di lavoro AEM basati su Forms su OSGi e in HTML Workspace per flussi di lavoro JEE AEM Forms.

<table>
 <tbody>
  <tr>
   <td>Azioni</td>
   <td>Casella in entrata AEM</td>
   <td>HTML Workspace</td>
  </tr>
  <tr>
   <td>Avvio di un processo, un'attività o un'applicazione del modulo<br /> </td>
   <td>Funzione supportata<br /> </td>
   <td>Funzione supportata<br /> </td>
  </tr>
  <tr>
   <td>Invio di attività</td>
   <td>Funzione supportata<br /> </td>
   <td>Funzione supportata<br /> </td>
  </tr>
  <tr>
   <td>Assegnazione di un'attività a un gruppo</td>
   <td>Funzione supportata<br /> </td>
   <td>Funzione supportata<br /> </td>
  </tr>
  <tr>
   <td>Invio a più route</td>
   <td>Funzione supportata<br /> </td>
   <td>Funzione supportata<br /> </td>
  </tr>
  <tr>
   <td>Cronologia delle attività e riepilogo delle attività</td>
   <td>Funzione supportata<br /> </td>
   <td>Funzione supportata<br /> </td>
  </tr>
  <tr>
   <td>Notifiche e-mail</td>
   <td>Funzione supportata<br /> </td>
   <td>Funzione supportata<br /> </td>
  </tr>
  <tr>
   <td>Riassegnazione delle attività</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Allegati a livello di campo per i moduli adattivi</td>
   <td>Funzione supportata</td>
   <td>Non supportato</td>
  </tr>
  <tr>
   <td>Vista calendario</td>
   <td>Funzione supportata</td>
   <td>Non supportato</td>
  </tr>
  <tr>
   <td>Commenti a livello di attività</td>
   <td>Funzione supportata</td>
   <td>Non supportato</td>
  </tr>
  <tr>
   <td>Code (coda personale condivisa, attività di richiesta di rimborso dalla coda)</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Notifica fuori sede</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
    <tr>
   <td>Personalizzazione degli elementi dell’interfaccia utente</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Assegnazione di un’attività a più utenti</td>
   <td>Non supportato</td>
   <td>Funzione supportata</td>
  </tr>
 </tbody>
</table>

## Flussi di lavoro AEM incentrati sui moduli sui flussi di lavoro OSGi e AEM Forms JEE {#form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

I flussi di lavoro AEM incentrati sui moduli sui flussi di lavoro OSGi e AEM Forms JEE (AEM Forms on JEE Process Management) hanno un set di funzionalità diverso. La tabella seguente ti aiuta a comprendere le funzionalità importanti disponibili nei flussi di lavoro AEM incentrati sui moduli su OSGi e AEM Forms sui flussi di lavoro JEE:

<table>
 <tbody>
  <tr>
   <td>Funzionalità</td>
   <td>Flussi di lavoro AEM incentrati sui moduli su OSGi<br /> </td>
   <td>Flussi di lavoro JEE per AEM Forms</td>
  </tr>
  <tr>
   <td>Moduli adattivi</td>
   <td>Supportato</td>
   <td>Supportato<br /> </td>
  </tr>
  <tr>
   <td>Integrazione con altre soluzioni AEM</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Firma a mano</td>
   <td>Supportato</td>
   <td>Supportato<br /> </td>
  </tr>
  <tr>
   <td>Modelli e-mail personalizzati</td>
   <td>Supportato</td>
   <td>Supportato<br /> </td>
  </tr>
  <tr>
   <td>Definizione della priorità dell’attività</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Timeout di un'attività dopo la data di scadenza</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Cicli all’interno del flusso di lavoro</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Selezione dinamica di un assegnatario </td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Utilizzo dei metadati personalizzati</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Firma elettronica (Adobe Sign)</td>
   <td>Supportato <sup>[1]</sup></td>
   <td>Supportato <sup>[5]</sup></td>
  </tr>
  <tr>
   <td>Gestione di applicazioni per task e moduli</td>
   <td>Supportato <sup>[2]</sup><br /> </td>
   <td>Supportato <sup>[2]</sup></td>
  </tr>
  <tr>
   <td>Document Services</td>
   <td>Supportato <sup>[3]</sup></td>
   <td>Supportato <sup>[3]</sup></td>
  </tr>
  <tr>
   <td>Rendering dell’attività completata come modulo adattivo o documento PDF</td>
   <td>Supportato</td>
   <td>Supportato [4]</td>
  </tr>
  <tr>
   <td>Integrazione con la gestione della corrispondenza</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
   <tr>
   <td>Gateway , NO WAIT </td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
   <tr>
   <td>Variabili per memorizzare i dati </td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>OR, AND Split</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Avatar utente</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Invia un messaggio e-mail alla fine del flusso di lavoro</td>
   <td>Supportato <sup>[7]</sup></td>
   <td>Funzione supportata</td>
  </tr>
  <tr>
   <td>Chiamare un servizio Web da un flusso di lavoro</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Firma digitale</td>
   <td>Funzione supportata<br /> </td>
   <td>Funzione supportata<br /> </td>
  </tr>
  <tr>
   <td>Pulsante Ripristina</td>
   <td>Funzione supportata</td>
   <td>Non supportato</td>
  </tr>
  <tr>
   <td>Fasi del flusso di lavoro</td>
   <td>Funzione supportata</td>
   <td>Non supportato</td>
  </tr>
  <tr>
   <td>Moduli adattivi di sola lettura</td>
   <td>Funzione supportata</td>
   <td>Non supportato</td>
  </tr>
  <tr>
   <td>Nascondere il pulsante di salvataggio predefinito</td>
   <td>Funzione supportata</td>
   <td>Non supportato</td>
  </tr>
  <tr>
   <td>Sezione Controllo granulare sui dettagli del flusso di lavoro</td>
   <td>Funzione supportata</td>
   <td>Non supportato</td>
  </tr>
  <tr>
   <td>Servizio polling/Scheduling</td>
   <td>Disponibile preconfigurato</td>
   <td>Implementazione personalizzata richiesta</td>
  </tr>
  <tr>
   <td>App Forms adattiva</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Servizio assemblatore</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Servizio PDF Generator</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Servizio Forms</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Servizio di output</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Document Assurance</td>
   <td>Supportato</td>
   <td>Supportato </td>
  </tr>
  <tr>
   <td>Esegui script</td>
   <td>Supporta ECMAScript</td>
   <td>Supporta snippet di codice Java</td>
  </tr>
  <tr>
   <td>Assemblatore</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>  
  <tr>
   <td>HTML5 Forms, PDF forms interattivi, set di moduli</td>
   <td>Non supportato</td>
   <td>Funzione supportata</td>
  </tr>
  <tr>
   <td>Reporting processi</td>
   <td>Non supportato</td>
   <td>Funzione supportata</td>
  </tr>
  <tr>
   <td>Firma digitale</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Categorie di punti iniziali</td>
   <td>Non supportato </td>
   <td>Funzione supportata </td>
  </tr>
  <tr>
   <td>Approvazione di attività in blocco </td>
   <td>Non supportato </td>
   <td>Funzione supportata </td>
  </tr>
  <tr>
   <td>Salva bozza con nome personalizzato</td>
   <td>Non supportato </td>
   <td>Funzione supportata </td>
  </tr>
  <tr>
   <td>Avviare un processo con i dati del processo esistenti<br /> </td>
   <td>Non supportato</td>
   <td>Funzione supportata </td>
  </tr>
  <tr>
   <td>Salvataggio di un punto iniziale come bozza</td>
   <td>Non supportato</td>
   <td>Funzione supportata</td>
  </tr>
  <tr>
   <td>Vista Manager</td>
   <td>Non supportato</td>
   <td>Funzione supportata<br /> </td>
  </tr>
  <tr>
   <td>Cerca modelli</td>
   <td>Non supportato</td>
   <td>Funzione supportata<br /> </td>
  </tr>
  <tr>
   <td>Integrazione con applicazioni di terze parti</td>
   <td>Non supportato <sup>[6]</sup></td>
   <td>Funzione supportata</td>
  </tr>
  <tr>
   <td>Allegati a livello di task per l'applicazione del flusso di lavoro o punto iniziale</td>
   <td>Non supportato</td>
   <td>Funzione supportata</td>
  </tr>
  <tr>
   <td>E-mail di promemoria</td>
   <td>Non supportato</td>
   <td>Funzione supportata</td>
  </tr>
  <tr>
   <td>Modifica titolo in timeout attività</td>
   <td>Non supportato</td>
   <td>Funzione supportata</td>
  </tr>
  <tr>
   <td>E-mail su delega attività e attestazione attività</td>
   <td>Non supportato</td>
   <td>Funzione supportata</td>
  </tr>
  <tr>
   <td>Delega tra gruppi disgiunti</td>
   <td>Non supportato</td>
   <td>Funzione supportata</td>
  </tr>
  <tr>
   <td>Trasformazione XSLT</td>
   <td>Non supportato</td>
   <td>Funzione supportata</td>
  </tr>
  <tr>
   <td>Priorità attività dinamica</td>
   <td>Non supportato</td>
   <td>Non supportato</td>
  </tr>
  <tr>
   <td>Titolo dinamico</td>
   <td>Non supportato</td>
   <td>Non supportato</td>
  </tr>
    <tr>
   <td>Descrizione dinamica</td>
   <td>Non supportato</td>
   <td>Non supportato</td>
  </tr>
 </tbody>
</table>

1. È possibile utilizzare flussi di lavoro AEM incentrati sul modulo su OSGi per firmare un modulo adattivo compilato. I flussi di lavoro AEM incentrati sui moduli su OSGi supportano la firma fuori dal modulo. La [firma in-form](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience) esperienza non supportata.

1. Per eseguire e monitorare i flussi di lavoro JEE di AEM Forms, è necessario accedere AEM casella in entrata per eseguire e monitorare i flussi di lavoro incentrati sui moduli su AEM Forms OSGi e HTML Workspace.
1. I servizi nativi per i documenti AEM Forms sono disponibili sia per i flussi di lavoro AEM incentrati sui moduli su OSGi che per AEM Forms sui flussi di lavoro JEE. AEM Workflow utilizza servizi di documenti nativi per flussi di lavoro AEM incentrati sui moduli su OSGi e AEM Forms JEE (Process Management).
1. I flussi di lavoro JEE di AEM Forms possono eseguire il rendering solo di un modulo adattivo. Non supporta il rendering di un modulo adattivo come documento PDF.
1. I flussi di lavoro JEE per i moduli AEM non dispongono di un passaggio separato per Adobe Sign. È necessario un modulo adattivo abilitato per Adobe Sign per i flussi di lavoro JEE per AEM moduli. Per ulteriori dettagli, consulta [Documentazione di Adobe Sign](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component).
1. È possibile utilizzare [Richiama servizio modello dati modulo](../../forms/using/aem-forms-workflow-step-reference.md#p-invoke-form-data-model-service-step-p) passaggio per richiamare un servizio Web-service e pubblicare o recuperare dati da un&#39;applicazione di terze parti.
1. È possibile utilizzare [Invia e-mail](../../forms/using/aem-forms-workflow-step-reference.md#send-email-step) passaggio per inviare e-mail.

## Differenze tra AEM casella in entrata e funzioni dell’app AEM Forms {#differences-between-aem-inbox-and-aem-forms-app-features}

Due dei principali modi per avviare un flusso di lavoro incentrato su Forms sono quelli utilizzati [Casella in entrata AEM](../../forms/using/manage-applications-inbox.md) e l&#39;app AEM Forms. Le funzionalità della casella in entrata AEM e dell’app AEM Forms, tuttavia, differiscono. AEM casella in entrata funziona solo con [Flussi di lavoro incentrati su Forms](../../forms/using/aem-forms-workflow.md) mentre l’app AEM Forms funziona sia con flussi di lavoro incentrati su Forms che con la gestione dei processi.

La tabella seguente elenca le funzionalità di AEM Posta in arrivo e dell’app AEM Forms:

<table>
 <tbody>
  <tr>
   <td><p><strong>Azioni</strong></p> </td>
   <td><p><strong>Casella in entrata AEM</strong></p> </td>
   <td><p><strong>App AEM Forms</strong></p> </td>
  </tr>
  <tr>
   <td><p>Avvio di un’applicazione modulo</p> </td>
   <td><p>Supportato</p> </td>
   <td><p>Supportato</p> </td>
  </tr>
  <tr>
   <td><p>Invio di attività</p> </td>
   <td><p>Supportato</p> </td>
   <td><p>Supportato</p> </td>
  </tr>
  <tr>
   <td><p>Delega delle attività</p> </td>
   <td><p>Funzione supportata</p> </td>
   <td><p>Non supportato</p> </td>
  </tr>
  <tr>
   <td><p>Cronologia delle attività e riepilogo delle attività</p> </td>
   <td><p>Funzione supportata</p> </td>
   <td><p>Non supportato</p> </td>
  </tr>
  <tr>
   <td><p>Aggiunta di allegati a livello di attività</p> </td>
   <td><p>Supportato</p> </td>
   <td><p>Supportato</p> </td>
  </tr>
  <tr>
   <td><p>Visualizzazione degli allegati a livello di attività</p> </td>
   <td><p>Supportato</p> </td>
   <td><p>Supportato</p> </td>
  </tr>
  <tr>
   <td><p>Aggiunta di allegati a livello di campo</p> </td>
   <td><p>Supportato</p> </td>
   <td><p>Supportato</p> </td>
  </tr>
  <tr>
   <td><p>Visualizzazione della vista Calendario</p> </td>
   <td><p>Funzione supportata</p> </td>
   <td><p>Non supportato</p> </td>
  </tr>
  <tr>
   <td><p>Aggiunta di commenti</p> </td>
   <td><p>Supportato</p> </td>
   <td><p>Supportato</p> </td>
  </tr>
 </tbody>
</table>
