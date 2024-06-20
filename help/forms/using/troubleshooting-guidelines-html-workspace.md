---
title: Linee guida per la risoluzione dei problemi per AEM Forms Workspace
description: Abilita i registri e utilizza il debugger nel browser per la risoluzione dei problemi di AEM Forms Workspace.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: a054b60a-5e89-4c98-87bc-35669988d160
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 0%

---

# Linee guida per la risoluzione dei problemi per AEM Forms Workspace {#troubleshooting-guidelines-for-aem-forms-workspace}

Questo articolo illustra come eseguire il debug dell’area di lavoro di AEM Forms abilitando la registrazione e utilizzando il debugger in un browser. Vengono inoltre illustrati alcuni problemi comuni che è possibile incontrare durante l’utilizzo di AEM Forms Workspace e delle relative soluzioni.

## Impossibile installare il pacchetto dell’area di lavoro di AEM Forms {#unable-to-install-aem-forms-workspace-package}

Dopo aver installato la patch, apri l’area di lavoro di AEM Forms. Se riscontri l’errore Nessuna risorsa trovata, apri Gestione pacchetti CRX e reinstalla `adobe-lc-workspace-pkg-<version>.zip` pacchetto.

Se durante l’installazione del pacchetto si verifica un errore `javax.jcr.nodetype.ConstraintViolationException: OakConstraint0025: Authorizable property rep:authorizableId may not be removed`, effettua le seguenti operazioni:

1. Accedi a CRXDE Liti. L’URL predefinito è `https://[localhost]:'port'/lc/crx/de/index.jsp`
1. Elimina il seguente nodo:

   `/home/groups/P/PERM_WORKSPACE_USER`

1. Passa a Gestione pacchetti. L’URL predefinito è `https://[localhost]:'port'/lc/crx/packmgr/index.jsp.`
1. Cerca e installa `adobe-lc-workspace-pkg-[version].zip` pacchetto.
1. Riavviare il server applicazioni.

>[!NOTE]
>
> Per riavviare l&#39;SDK, si consiglia di utilizzare il comando &#39;Ctrl + C&#39;. Il riavvio dell’SDK dell’AEM con metodi alternativi, ad esempio l’arresto dei processi Java, può causare incongruenze nell’ambiente di sviluppo dell’AEM.

## Registrazione nell’area di lavoro di AEM Forms {#aem-forms-workspace-nbsp-logging}

Puoi generare i registri a vari livelli per consentire una risoluzione ottimale degli errori. Ad esempio, in un’applicazione complessa, la registrazione a livello di componente aiuta a eseguire il debug e a risolvere i problemi di componenti specifici.

Nell’area di lavoro AEM Forms:

* Per ottenere le informazioni di registrazione relative a un file di componente specifico, aggiungere `/log/<ComponentFile>/<LogLevel>` nell’URL, quindi premi `Enter`. Tutte le informazioni di registrazione per il file componente al livello di registro specificato vengono stampate sulla console.

* Per ottenere le informazioni di registrazione di tutti i file dei componenti, aggiungi `/log/all/trace` nell’URL, quindi premi `Enter`.

* Formato registro: `<Component file> <Date>:<Time>: <Log Level> : <Log Message>`

>[!NOTE]
>
>Per impostazione predefinita, il livello di registro di tutti i componenti è impostato su INFO.

* Il livello di registro impostato dall&#39;utente viene mantenuto solo per quella sessione del browser. Quando l’utente aggiorna la pagina, il livello di registro viene impostato sul valore iniziale per tutti i componenti.

### Elenco dei file dei componenti nell’area di lavoro di AEM Forms {#list-of-component-files-in-nbsp-aem-forms-workspace}

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

* FATALE
* ERRORE 
* AVVISO
* INFO
* DEBUG
* TRACE
* OFF

## Informazioni di debug per i browser {#debugging-information-for-browsers}

È possibile eseguire il debug di script e stili in browser diversi.

* **Debug in IE**: per eseguire il debug dell’area di lavoro di AEM Forms in IE, consulta: [https://learn.microsoft.com/en-us/office/dev/add-ins/testing/debug-add-ins-using-f12-tools-ie](https://learn.microsoft.com/en-us/office/dev/add-ins/testing/debug-add-ins-using-f12-tools-ie).

* **Debug in Chrome**: per aprire il debugger in Chrome, utilizza la scelta rapida: Ctrl+Maiusc+I. Per ulteriori informazioni, consulta: [https://developer.chrome.com/docs/extensions/mv3/tut_debugging/](https://developer.chrome.com/docs/extensions/mv3/tut_debugging/).

* **Debug in Firefox**: sono disponibili diversi componenti aggiuntivi per il debug di script e stili in Firefox. Firebug, ad esempio, è una di queste utility di debug ([https://getfirebug.com](https://getfirebug.com)).

## Domande frequenti {#faqs}

1. Il modulo PDF non viene renderizzato o inviato in Google Chrome.

   1. Installare il plug-in Adobe® Reader®.
   1. In Chrome, apri chrome://plugins per visualizzare i plug-in disponibili.
   1. Disattiva il plug-in Chrome PDF Viewer e abilita il plug-in Adobe Reader.

1. Il rendering del modulo o della Guida SWF non viene eseguito in Google Chrome.

   1. In Chrome, apri chrome://plugins per visualizzare i plug-in disponibili.
   1. Vedi i dettagli per Adobe plug-in Flash® Player.
   1. Disattivare PepperFlash sotto il plug-in Flash Player Adobe.

1. Ho personalizzato l’area di lavoro di AEM Forms, ma non riesco a vedere le modifiche.

   Cancella la cache del browser, quindi accedi all’area di lavoro di AEM Forms.

1. Cosa deve fare l’utente per abilitare il rendering del modulo in HTML quando viene aperto sul desktop?

   Selezionare il pulsante di scelta HTML per il profilo predefinito nel passaggio Assegna attività quando si utilizza Workbench.

1. L&#39;allegato non viene visualizzato quando si fa clic su di esso.

   Per visualizzare gli allegati, abilita i popup nel browser.

1. Un utente ha eseguito l&#39;accesso a un&#39;applicazione Forms. Se l’utente tenta di accedere all’area di lavoro, è possibile che non venga caricato, se non dispone delle autorizzazioni per l’area di lavoro.

   Disconnettersi dall&#39;altra applicazione Forms, quindi accedere all&#39;area di lavoro.

1. I moduli HTML, utilizzando le Proprietà processo nella progettazione, quando vengono sottoposti a rendering nell’area di lavoro di AEM Forms, visualizzano il pulsante Invia all’interno del modulo.

   Durante la progettazione dei moduli, quando si utilizzano le proprietà del processo, viene aggiunto un pulsante Invia all&#39;interno del modulo. Quando viene eseguito il rendering come PDF nell’area di lavoro di AEM Forms, il pulsante Invia non è visibile all’utente finale. Tuttavia, quando si esegue il rendering come modulo HTML nell’area di lavoro di AEM Forms, il pulsante Invia è visibile all’utente finale. Se si fa clic sul pulsante Invia all&#39;interno del modulo, non viene avviata alcuna azione. Per completare l’attività, fai clic sul pulsante Invia nella parte inferiore dell’area di lavoro di AEM Forms, all’esterno del modulo.
