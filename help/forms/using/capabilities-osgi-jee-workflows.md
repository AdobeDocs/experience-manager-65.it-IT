---
title: Azioni e funzionalità dei flussi di lavoro AEM incentrati sui moduli nei flussi di lavoro OSGi e AEM Forms JEE
seo-title: Azioni e funzionalità dei flussi di lavoro AEM incentrati sui moduli nei flussi di lavoro OSGi e AEM Forms JEE
description: 'null'
seo-description: 'null'
uuid: 8af9527d-fa5e-4fcb-88e1-49571528fca6
contentOwner: khsingh
topic-tags: publish
discoiquuid: 89bcc76d-122f-4a3f-b857-16e5376e1624
docset: aem65
translation-type: tm+mt
source-git-commit: 48d18de8c982ab3b92cad4df030cb1e4a1a8dfc4
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 20%

---


# Azioni e funzionalità dei flussi di lavoro AEM incentrati sui moduli nei flussi di lavoro OSGi e AEM Forms JEE {#actions-and-capabilities-of-form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

## Casella in entrata AEM e area di lavoro HTML {#aem-inbox-and-html-workspace}

È possibile utilizzare AEM Inbox per eseguire e monitorare i flussi di lavoro AEM incentrati sui moduli in OSGi. HTML Workspace consente invece di eseguire e monitorare i flussi di lavoro AEM Forms JEE. La tabella seguente illustra le varie azioni importanti disponibili in AEM Inbox per i flussi di lavoro AEM incentrati sui moduli su OSGi e in HTML Workspace per i flussi di lavoro AEM Forms JEE.

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

## Flussi di lavoro AEM incentrati sui moduli nei flussi di lavoro OSGi e AEM Forms JEE {#form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

I flussi di lavoro AEM incentrati sui moduli nei flussi di lavoro OSGi e AEM Forms JEE (AEM Forms on JEE Process Management) presentano un set di funzionalità diverso. La tabella seguente illustra le importanti funzionalità disponibili nei flussi di lavoro AEM incentrati sui moduli su OSGi e AEM Forms su flussi di lavoro JEE:

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
   <td>(Obsoleto) Firma scarabocchio</td>
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
   <td>Firma elettronica (Adobe Sign)</td>
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
   <td>Moduli HTML5, moduli PDF interattivi, set di moduli<br /> </td>
   <td>Non supportato<br /> </td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Reporting processi</td>
   <td>Non supportato<br /> </td>
   <td>Supportato<br /> </td>
  </tr>
  <tr>
   <td>Firma digitale</td>
   <td>Supportato<br /> </td>
   <td>Supportato<br /> </td>
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
   <td>Avatar utente</td>
   <td>Supportato</td>
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
   <td>Invia un messaggio e-mail alla fine del flusso di lavoro</td>
   <td>Supported <sup>[7]</sup></td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Delega tra gruppi disgiunti</td>
   <td>Non supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Chiamare un servizio Web da un flusso di lavoro</td>
   <td>Non supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Trasformazione XSLT</td>
   <td>Non supportato</td>
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
   <td>Non supportato</td>
   <td>Supportato</td>
  </tr>
  <tr>
   <td>Priorità attività dinamica</td>
   <td>Non supportato</td>
   <td>Non supportato</td>
  </tr>
 </tbody>
</table>

1. In OSGi potete utilizzare flussi di lavoro AEM incentrati sui moduli per firmare un modulo adattivo compilato. Flussi di lavoro AEM incentrati sui moduli in OSGi supportati dalla firma dei moduli. L&#39;esperienza di firma [](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience) in-form non è supportata.

1. Per eseguire e monitorare i flussi di lavoro AEM Forms JEE, è necessario accedere alla Casella in entrata AEM.
1. AEM Forms Document Services nativo è disponibile per i flussi di lavoro AEM incentrati sui moduli su OSGi e AEM Forms su flussi di lavoro JEE. AEM Workflow utilizza servizi di documenti nativi per i flussi di lavoro AEM incentrati sui moduli su OSGi e AEM Forms JEE (Process Management).
1. I flussi di lavoro AEM Forms JEE possono eseguire solo il rendering di un modulo adattivo. Non supporta il rendering di un modulo adattivo come documento PDF.
1. I flussi di lavoro JEE dei moduli AEM non dispongono di un passaggio separato per Adobe Sign. È necessario un modulo adattivo abilitato per Adobe Sign per i flussi di lavoro JEE dei moduli AEM. Per ulteriori dettagli, consultare la documentazione [di](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component)Adobe Sign.
1. È possibile utilizzare il passaggio [Richiama servizio](../../forms/using/aem-forms-workflow-step-reference.md#p-invoke-form-data-model-service-step-p) modello dati modulo per richiamare un servizio Web e inviare o recuperare dati da un&#39;applicazione di terze parti.
1. Potete utilizzare il passaggio [Invia e-mail](../../forms/using/aem-forms-workflow-step-reference.md#send-email-step) per inviare e-mail.

## Differenze tra le funzioni dell&#39;app AEM Inbox e AEM Forms {#differences-between-aem-inbox-and-aem-forms-app-features}

Due dei modi principali per avviare un flusso di lavoro incentrato sui moduli sono utilizzare l&#39;app [AEM Inbox](../../forms/using/manage-applications-inbox.md) e AEM Forms. Le funzionalità dell&#39;app AEM Inbox e AEM Forms, tuttavia, sono diverse. AEM Inbox funziona solo con flussi di lavoro [incentrati su](../../forms/using/aem-forms-workflow.md) Forms, mentre l&#39;app AEM Forms funziona sia con flussi di lavoro incentrati sui moduli che con la gestione dei processi.

Nella tabella seguente sono elencate le funzionalità dell&#39;app AEM Inbox e AEM Forms:

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

