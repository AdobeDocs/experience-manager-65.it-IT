---
title: Azioni e funzionalità dei flussi di lavoro AEM incentrati sui moduli nei flussi di lavoro OSGi e  AEM Forms JEE
description: Azioni e funzionalità dei flussi di lavoro AEM incentrati sui moduli nei flussi di lavoro OSGi e  AEM Forms JEE
contentOwner: khsingh
translation-type: tm+mt
source-git-commit: dfa5a0dbfdd2c63ea0ec66d805e8b452baa3d0ac
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 22%

---


# Azioni e funzionalità dei flussi di lavoro AEM incentrati sui moduli nei flussi di lavoro OSGi e  AEM Forms JEE {#actions-and-capabilities-of-form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

## AEM Inbox e area di lavoro HTML {#aem-inbox-and-html-workspace}

È possibile utilizzare AEM Posta in arrivo per eseguire e monitorare i flussi di lavoro AEM basati su Forms in OSGi. HTML Workspace consente invece di eseguire e monitorare  flussi di lavoro AEM Forms JEE. La tabella seguente illustra le varie azioni importanti disponibili in AEM Inbox per i flussi di lavoro AEM basati su Forms su OSGi e in HTML Workspace per  flussi di lavoro AEM Forms JEE.

<table>
 <tbody>
  <tr>
   <td>Azioni</td>
   <td>Casella in entrata AEM</td>
   <td>Area di lavoro HTML</td>
  </tr>
  <tr>
   <td>Avvio di un processo, un'attività o un'applicazione modulo<br /> </td>
   <td>Supportato<br /> </td>
   <td>Supportato<br /> </td>
  </tr>
  <tr>
   <td>Invio delle attività</td>
   <td>Supportato<br /> </td>
   <td>Supportato<br /> </td>
  </tr>
  <tr>
   <td>Assegnazione di un'attività a un gruppo</td>
   <td>Supportato<br /> </td>
   <td>Supportato<br /> </td>
  </tr>
  <tr>
   <td>Invio a più route</td>
   <td>Supportato<br /> </td>
   <td>Supportato<br /> </td>
  </tr>
  <tr>
   <td>Cronologia delle attività e riepilogo delle attività</td>
   <td>Supportato<br /> </td>
   <td>Supportato<br /> </td>
  </tr>
  <tr>
   <td>Notifiche e-mail</td>
   <td>Supportato<br /> </td>
   <td>Supportato<br /> </td>
  </tr>
  <tr>
   <td>Riassegnazione delle attività</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Allegati a livello di campo per moduli adattivi</td>
   <td>Supportato</td>
   <td>Non supportato</td>
  </tr>
  <tr>
   <td>Vista calendario</td>
   <td>Supportato</td>
   <td>Non supportato</td>
  </tr>
  <tr>
   <td>Commenti a livello di attività</td>
   <td>Supportato</td>
   <td>Non supportato</td>
  </tr>
  <tr>
   <td>Code (coda personale condivisa, attività di richiesta di rimborso dalla coda)</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Notifica fuori ufficio</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
    <tr>
   <td>Personalizzazione degli elementi dell'interfaccia</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Assegnazione di un'attività a più utenti</td>
   <td>Non supportato</td>
   <td>Supportato</td>
  </tr>
 </tbody>
</table>

## Flussi di lavoro AEM incentrati sui moduli nei flussi di lavoro OSGi e  AEM Forms JEE {#form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

I flussi di lavoro AEM incentrati sui moduli su OSGi e  flussi di lavoro AEM Forms JEE ( AEM Forms su JEE Process Management) dispongono di un set di funzionalità diverso. La tabella seguente illustra le importanti funzionalità disponibili nei flussi di lavoro AEM basati su moduli su OSGi e  AEM Forms sui flussi di lavoro JEE:

<table>
 <tbody>
  <tr>
   <td>Funzionalità</td>
   <td>Flussi di lavoro AEM incentrati sui moduli in OSGi<br /> </td>
   <td>Flussi di lavoro AEM Forms JEE</td>
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
   <td>Definizione priorità attività</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Timeout di un'attività dopo la data di scadenza</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Cicli nel flusso di lavoro</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Selezione dinamica di un assegnatario </td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Utilizzo di metadati personalizzati</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Firma elettronica ( Adobe Sign)</td>
   <td>Supported <sup>[1]</sup></td>
   <td>Supported <sup>[5]</sup></td>
  </tr>
  <tr>
   <td>Gestione di applicazioni di modulo e attività</td>
   <td>Supported <sup>[2]</sup><br /> </td>
   <td>Supported <sup>[2]</sup></td>
  </tr>
  <tr>
   <td>Servizi basati su documenti</td>
   <td>Supported <sup>[3]</sup></td>
   <td>Supported <sup>[3]</sup></td>
  </tr>
  <tr>
   <td>Rendering dell'attività completata come modulo adattivo o documento PDF</td>
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
   <td>Supported <sup>[7]</sup></td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Chiamare un servizio Web da un flusso di lavoro</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Firma digitale</td>
   <td>Supportato<br /> </td>
   <td>Supportato<br /> </td>
  </tr>
  <tr>
   <td>Pulsante Ripristina</td>
   <td>Supportato</td>
   <td>Non supportato</td>
  </tr>
  <tr>
   <td>Fasi del flusso di lavoro</td>
   <td>Supportato</td>
   <td>Non supportato</td>
  </tr>
  <tr>
   <td>Moduli adattivi di sola lettura</td>
   <td>Supportato</td>
   <td>Non supportato</td>
  </tr>
  <tr>
   <td>Nascondere il pulsante Salva predefinito</td>
   <td>Supportato</td>
   <td>Non supportato</td>
  </tr>
  <tr>
   <td>Controllo granulare sulla sezione dei dettagli del flusso di lavoro</td>
   <td>Supportato</td>
   <td>Non supportato</td>
  </tr>
  <tr>
   <td>Servizio Polling/Scheduling</td>
   <td>Disponibile fuori dalla scatola</td>
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
   <td>PDF Generator Service</td>
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
   <td>FORMS HTML5, PDF forms interattivi, set di moduli</td>
   <td>Non supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Reporting processi</td>
   <td>Non supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Firma digitale</td>
   <td>Supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Categorie di punti di partenza</td>
   <td>Non supportato </td>
   <td>Supportato </td>
  </tr>
  <tr>
   <td>Approvazione di massa attività </td>
   <td>Non supportato </td>
   <td>Supportato </td>
  </tr>
  <tr>
   <td>Salva bozza con nome personalizzato</td>
   <td>Non supportato </td>
   <td>Supportato </td>
  </tr>
  <tr>
   <td>Avviare un processo con i dati del processo esistenti<br /> </td>
   <td>Non supportato</td>
   <td>Supportato </td>
  </tr>
  <tr>
   <td>Salvataggio di un punto iniziale come bozza</td>
   <td>Non supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Vista manager</td>
   <td>Non supportato</td>
   <td>Supportato<br /> </td>
  </tr>
  <tr>
   <td>Modelli di ricerca</td>
   <td>Non supportato</td>
   <td>Supportato<br /> </td>
  </tr>
  <tr>
   <td>Integrazione con applicazioni di terze parti</td>
   <td>Not Supported <sup>[6]</sup></td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Allegati a livello di attività per l’applicazione del flusso di lavoro o il punto di avvio</td>
   <td>Non supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>E-mail promemoria</td>
   <td>Non supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Modifica del titolo in caso di timeout dell'attività</td>
   <td>Non supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>E-mail su delega attività e richiesta attività</td>
   <td>Non supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Delega tra gruppi disgiunti</td>
   <td>Non supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Trasformazione XSLT</td>
   <td>Non supportato</td>
   <td>Supportato</td>
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

1. È possibile utilizzare i flussi di lavoro AEM basati su moduli in OSGi per firmare un modulo adattivo compilato. Flussi di lavoro AEM incentrati sui moduli in OSGi supporta la firma fuori dal modulo. L&#39;esperienza di firma [](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience) in-form non è supportata.

1. È necessario accedere AEM Posta in arrivo per eseguire e monitorare i flussi di lavoro basati su moduli  AEM Forms OSGi e HTML Workspace per eseguire e monitorare  flussi di lavoro AEM Forms JEE.
1. I servizi AEM Forms Document Services nativi  sono disponibili sia per i flussi di lavoro AEM basati su moduli su OSGi che per  AEM Forms su flussi di lavoro JEE. AEM Flusso di lavoro utilizza servizi di documenti nativi per i flussi di lavoro AEM basati su moduli in OSGi e  AEM Forms JEE (Process Management).
1.  flussi di lavoro AEM Forms JEE può eseguire il rendering solo di un modulo adattivo. Non supporta il rendering di un modulo adattivo come documento PDF.
1. AEM moduli i flussi di lavoro JEE non dispongono di un passaggio separato per  Adobe Sign. È necessario un  modulo adattivo abilitato per Adobe Sign per AEM moduli Flussi di lavoro JEE. Per ulteriori dettagli, consultate [documentazione](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component)Adobe Sign.
1. È possibile utilizzare il passaggio [Richiama servizio](../../forms/using/aem-forms-workflow-step-reference.md#p-invoke-form-data-model-service-step-p) modello dati modulo per richiamare un servizio Web e inviare o recuperare dati da un&#39;applicazione di terze parti.
1. Potete utilizzare il passaggio [Invia e-mail](../../forms/using/aem-forms-workflow-step-reference.md#send-email-step) per inviare e-mail.

## Differenze tra AEM Posta in arrivo e  funzionalità dell&#39;app AEM Forms {#differences-between-aem-inbox-and-aem-forms-app-features}

Due dei modi principali per avviare un flusso di lavoro incentrato su Forms sono utilizzare [AEM Posta in arrivo](../../forms/using/manage-applications-inbox.md) e  app AEM Forms. Le funzionalità dell&#39;app AEM Posta in arrivo e  AEM Forms, tuttavia, differiscono. AEM Inbox funziona solo con flussi di lavoro [basati su](../../forms/using/aem-forms-workflow.md) Forms, mentre l&#39;app AEM Forms  funziona sia con flussi di lavoro incentrati su Forms che con la gestione dei processi.

Nella tabella seguente sono elencate le funzionalità AEM Posta in arrivo e  app AEM Forms:

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
   <td><p>Invio delle attività</p> </td>
   <td><p>Supportato</p> </td>
   <td><p>Supportato</p> </td>
  </tr>
  <tr>
   <td><p>Delega di attività</p> </td>
   <td><p>Supportato</p> </td>
   <td><p>Non supportato</p> </td>
  </tr>
  <tr>
   <td><p>Cronologia delle attività e riepilogo delle attività</p> </td>
   <td><p>Supportato</p> </td>
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
   <td><p>Supportato</p> </td>
   <td><p>Non supportato</p> </td>
  </tr>
  <tr>
   <td><p>Aggiunta di commenti</p> </td>
   <td><p>Supportato</p> </td>
   <td><p>Supportato</p> </td>
  </tr>
 </tbody>
</table>

