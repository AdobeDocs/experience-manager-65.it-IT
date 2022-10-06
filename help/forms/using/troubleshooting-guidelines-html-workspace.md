---
title: Linee guida per la risoluzione dei problemi relativi all’area di lavoro di AEM Forms
seo-title: Troubleshooting guidelines for AEM Forms workspace
description: Abilita i registri e utilizza il debugger nel browser per risolvere i problemi relativi all’area di lavoro di AEM Forms.
seo-description: Enable logs and use debugger in browser to troubleshoot AEM Forms workspace.
uuid: 07b8c8ed-f1ff-4be5-8005-251ff7b2ac85
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 5dae9ed9-77a3-44f5-a94d-ca5c355c8730
exl-id: a054b60a-5e89-4c98-87bc-35669988d160
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 0%

---

# Linee guida per la risoluzione dei problemi relativi all’area di lavoro di AEM Forms {#troubleshooting-guidelines-for-aem-forms-workspace}

Questo articolo illustra come eseguire il debug dell’area di lavoro AEM Forms abilitando la registrazione e utilizzando il debugger in un browser. Vengono inoltre illustrati alcuni problemi comuni che è possibile incontrare quando si utilizza l’area di lavoro di AEM Forms e le relative soluzioni alternative.

## Impossibile installare il pacchetto dell&#39;area di lavoro AEM Forms {#unable-to-install-aem-forms-workspace-package}

Dopo aver installato la patch, apri l’area di lavoro AEM Forms. Se incontri l&#39;errore No Resource Found (Nessuna risorsa trovata), apri la Gestione pacchetti CRX e reinstalla la `adobe-lc-workspace-pkg-<version>.zip` pacchetto.

Durante l&#39;installazione del pacchetto, in caso di errore `javax.jcr.nodetype.ConstraintViolationException: OakConstraint0025: Authorizable property rep:authorizableId may not be removed`, esegui le seguenti operazioni:

1. Accedi a CRX DE lite. L’URL predefinito è `https://[localhost]:'port'/lc/crx/de/index.jsp`
1. Elimina il seguente nodo:

   `/home/groups/P/PERM_WORKSPACE_USER`

1. Vai a Gestione pacchetti. L’URL predefinito è `https://[localhost]:'port'/lc/crx/packmgr/index.jsp.`
1. Cerca e installa il `adobe-lc-workspace-pkg-[version].zip` pacchetto.
1. Riavvia il server applicazioni.

## Registrazione nell’area di lavoro di AEM Forms {#aem-forms-workspace-nbsp-logging}

È possibile generare registri a vari livelli per consentire una risoluzione ottimale degli errori. Ad esempio, in un’applicazione complessa, la registrazione a livello di componente consente di eseguire il debug e risolvere problemi relativi a componenti specifici.

Nell’area di lavoro di AEM Forms:

* Per ottenere le informazioni di registrazione su un file di componente specifico, aggiungi `/log/<ComponentFile>/<LogLevel>` nell’URL, quindi premi `Enter`. Tutte le informazioni di registrazione per il file componente a livello di registro specificato vengono stampate sulla console.

* Per ottenere le informazioni di registrazione di tutti i file dei componenti, aggiungi `/log/all/trace` nell’URL, quindi premi `Enter`.

* Formato registro: `<Component file> <Date>:<Time>: <Log Level> : <Log Message>`

>[!NOTE]
>
>Per impostazione predefinita, il livello di registro di tutti i componenti è impostato su INFO.

* Il livello di log impostato dall&#39;utente viene mantenuto solo per la sessione del browser. Quando l’utente aggiorna la pagina, il livello di registro viene impostato sul valore iniziale per tutti i componenti.

### Elenco dei file di componenti nell’area di lavoro di AEM Forms {#list-of-component-files-in-nbsp-aem-forms-workspace}

<table>
 <tbody>
  <tr>
   <td><p>allcategoryModel</p> </td>
   <td><p>processinstanceModel</p> </td>
   <td><p>tasklistModel</p> </td>
  </tr>
  <tr>
   <td><p>appnavigationModel</p> </td>
   <td><p>processInstanceView</p> </td>
   <td><p>tasklistView</p> </td>
  </tr>
  <tr>
   <td><p>appnavigationView</p> </td>
   <td><p>processnamelistModel</p> </td>
   <td><p>taskModel</p> </td>
  </tr>
  <tr>
   <td><p>categorylistModel</p> </td>
   <td><p>processnamelistView</p> </td>
   <td><p>taskView</p> </td>
  </tr>
  <tr>
   <td><p>categorylistView</p> </td>
   <td><p>processnameModel</p> </td>
   <td><p>teamqueuesView</p> </td>
  </tr>
  <tr>
   <td><p>categoryModel</p> </td>
   <td><p>processnameView</p> </td>
   <td><p>todoView</p> </td>
  </tr>
  <tr>
   <td><p>categoryView</p> </td>
   <td><p>searchtemplatedetailsView</p> </td>
   <td><p>trackingView</p> </td>
  </tr>
  <tr>
   <td><p>favoritecategoryModel</p> </td>
   <td><p>sharequeueModel</p> </td>
   <td><p>uisettingsModel</p> </td>
  </tr>
  <tr>
   <td><p>filterlistView</p> </td>
   <td><p>sharequeueView</p> </td>
   <td><p>uisettingsView</p> </td>
  </tr>
  <tr>
   <td><p>filterView</p> </td>
   <td><p>startpointlistModel</p> </td>
   <td><p>userinfoModel</p> </td>
  </tr>
  <tr>
   <td><p>outofofficeModel</p> </td>
   <td><p>startpointlistView</p> </td>
   <td><p>userinfoView</p> </td>
  </tr>
  <tr>
   <td><p>outofofficeView</p> </td>
   <td><p>startpointModel</p> </td>
   <td><p>usersearchModel</p> </td>
  </tr>
  <tr>
   <td><p>preferencesView</p> </td>
   <td><p>startpointView</p> </td>
   <td><p>usersearchView</p> </td>
  </tr>
  <tr>
   <td><p>processinstancehistoryView</p> </td>
   <td><p>startProcessView</p> </td>
   <td><p>wserrorModel</p> </td>
  </tr>
  <tr>
   <td><p>processinstancelistModel</p> </td>
   <td><p>startprocessView</p> </td>
   <td><p>wserrorView</p> </td>
  </tr>
  <tr>
   <td><p>processinstancelistView</p> </td>
   <td><p>taskdetailsView</p> </td>
   <td><p>wsmessageView</p> </td>
  </tr>
 </tbody>
</table>

### Livelli di registro disponibili nell’area di lavoro di AEM Forms {#log-levels-available-in-nbsp-aem-forms-workspace}

* GRASSETTO
* ERRORE
* AVVISO
* INFO
* DEBUG
* TRACE
* DISATTIVATO

## Informazioni di debug per i browser {#debugging-information-for-browsers}

È possibile eseguire il debug di script e stili in diversi browser.

* **Debug in IE**: Per eseguire il debug dell&#39;area di lavoro AEM Forms in IE, vedi: [https://msdn.microsoft.com/en-us/library/hh772704(v=vs.85).aspx](https://msdn.microsoft.com/en-us/library/hh772704(v=vs.85).aspx).

* **Debug in Chrome**: Per aprire debugger in Chrome, utilizza il collegamento: Ctrl+Maiusc+I. Per ulteriori informazioni, consulta: [https://developer.chrome.com/extensions/tut_debugging.html](https://developer.chrome.com/extensions/tut_debugging.html).

* **Debug in Firefox**: Diversi componenti aggiuntivi sono disponibili per eseguire il debug di script e stili in Firefox. Ad esempio, Firebug è una di tali utility di debug ([https://getfirebug.com](https://getfirebug.com)).

## Domande frequenti {#faqs}

1. Il rendering o l’invio del modulo PDF in Google Chrome non viene eseguito.

   1. Installare il plug-in Adobe® Reader®.
   1. In Chrome, apri chrome://plugins per visualizzare i plug-in disponibili.
   1. Disattiva il plug-in Visualizzatore di Chrome PDF e abilita il plug-in Adobe Reader.

1. Il rendering del modulo o della Guida di SWF non viene eseguito in Google Chrome.

   1. In Chrome, apri chrome://plugins per visualizzare i plug-in disponibili.
   1. Vedi i dettagli del plug-in Adobe Flash® Player.
   1. Disattiva PepperFlash sotto il plug-in Flash Player Adobe.

1. Ho personalizzato l&#39;area di lavoro di AEM Forms ma non riesco a vedere le modifiche.

   Elimina la cache del browser e accedi all’area di lavoro AEM Forms.

1. Cosa deve essere fatto dall’utente per consentire il rendering del modulo in HTML quando viene aperto sul desktop?

   Selezionare il pulsante di scelta HTML per il profilo predefinito nel passaggio assegnazione attività durante l’utilizzo di Workbench.

1. L&#39;allegato non viene visualizzato quando si fa clic su di esso.

   Per visualizzare gli allegati, abilita i popup nel browser.

1. Un utente ha effettuato l’accesso a un’applicazione forms. Se l&#39;utente tenta di accedere all&#39;area di lavoro, potrebbe non essere caricato, se l&#39;utente non dispone di autorizzazioni dell&#39;area di lavoro.

   Disconnettiti dall’applicazione altri moduli e accedi a workspace.

1. Nei moduli di HTML, utilizzando le proprietà del processo nella relativa progettazione, quando viene eseguito il rendering nell’area di lavoro di AEM Forms, viene visualizzato il pulsante Invia all’interno del modulo.

   Durante la progettazione dei moduli, quando si utilizza Proprietà processo, all’interno del modulo viene aggiunto un pulsante Invia. Durante il rendering come PDF nell’area di lavoro di AEM Forms, il pulsante Invia non è visibile all’utente finale. Tuttavia, durante il rendering come modulo HTML nell’area di lavoro di AEM Forms, il pulsante Invia è visibile all’utente finale. Se si fa clic sul pulsante Invia all’interno del modulo, non viene avviata alcuna azione. L’attività viene completata facendo clic sul pulsante Invia nella parte inferiore dell’area di lavoro di AEM Forms, all’esterno del modulo.
