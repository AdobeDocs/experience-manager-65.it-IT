---
title: Linee guida per la risoluzione dei problemi per l'area di lavoro Moduli AEM
seo-title: Linee guida per la risoluzione dei problemi per l'area di lavoro Moduli AEM
description: Abilita registri e usa il debugger nel browser per risolvere eventuali problemi nell’area di lavoro di AEM Forms.
seo-description: Abilita registri e usa il debugger nel browser per risolvere eventuali problemi nell’area di lavoro di AEM Forms.
uuid: 07b8c8ed-f1ff-4be5-8005-251ff7b2ac85
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 5dae9ed9-77a3-44f5-a94d-ca5c355c8730
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Linee guida per la risoluzione dei problemi per l&#39;area di lavoro Moduli AEM {#troubleshooting-guidelines-for-aem-forms-workspace}

In questo articolo viene illustrato come eseguire il debug dell&#39;area di lavoro Moduli AEM abilitando la registrazione e utilizzando debugger in un browser. Vengono inoltre illustrati alcuni problemi comuni che è possibile incontrare quando si utilizza l&#39;area di lavoro di AEM Forms e le relative soluzioni.

## Impossibile installare il pacchetto dell&#39;area di lavoro AEM Forms {#unable-to-install-aem-forms-workspace-package}

Dopo aver installato la patch, aprite l&#39;area di lavoro AEM Forms. Se si verifica l&#39;errore Nessuna risorsa trovata, aprite Gestione pacchetti CRX e reinstallate il `adobe-lc-workspace-pkg-<version>.zip` pacchetto.

Durante l&#39;installazione del pacchetto, in caso di errore, `javax.jcr.nodetype.ConstraintViolationException: OakConstraint0025: Authorizable property rep:authorizableId may not be removed`eseguite i seguenti passaggi:

1. Accedete a CRX DE lite. L&#39;URL predefinito è `https://[localhost]:'port'/lc/crx/de/index.jsp`
1. Elimina il seguente nodo:

   `/home/groups/P/PERM_WORKSPACE_USER`

1. Andate a Gestione pacchetti. L’URL predefinito è `https://[localhost]:'port'/lc/crx/packmgr/index.jsp.`
1. Cercate e installate il `adobe-lc-workspace-pkg-[version].zip` pacchetto.
1. Riavviate il server applicazione.

## Registrazione dell&#39;area di lavoro di AEM Forms {#aem-forms-workspace-nbsp-logging}

Potete generare file di registro a vari livelli per consentire la risoluzione ottimale degli errori. Ad esempio, in un’applicazione complessa, l’accesso a livello di componente facilita il debug e la risoluzione dei problemi relativi a componenti specifici.

Nell’area di lavoro AEM Forms:

* Per ottenere le informazioni di registrazione su un file componente specifico, aggiungete `/log/<ComponentFile>/<LogLevel>` l’URL e premete `Enter`. Tutte le informazioni di registrazione per il file componente al livello di registro specificato vengono stampate nella console.

* Per ottenere informazioni di registrazione su tutti i file dei componenti, aggiungete `/log/all/trace` l’URL e premete `Enter`.

* Formato registro: `<Component file> <Date>:<Time>: <Log Level> : <Log Message>`

>[!NOTE]
>
>Per impostazione predefinita, il livello di registro di tutti i componenti è impostato su INFO.

* Il livello di registro impostato dall&#39;utente viene mantenuto solo per la sessione del browser in questione. Quando l’utente aggiorna la pagina, il livello di registro viene impostato sul valore iniziale per tutti i componenti.

### Elenco dei file di componenti nell’area di lavoro Moduli AEM {#list-of-component-files-in-nbsp-aem-forms-workspace}

<table>
 <tbody>
  <tr>
   <td><p>allcategoryModel</p> </td>
   <td><p>processinstanceModel</p> </td>
   <td><p>taskListModel</p> </td>
  </tr>
  <tr>
   <td><p>appnavigationModel</p> </td>
   <td><p>processInstanceView</p> </td>
   <td><p>taskListView</p> </td>
  </tr>
  <tr>
   <td><p>appnavigationView</p> </td>
   <td><p>processnamelistModel</p> </td>
   <td><p>taskModel</p> </td>
  </tr>
  <tr>
   <td><p>categoryListModel</p> </td>
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
   <td><p>taskDetails</p> </td>
   <td><p>wsmessageView</p> </td>
  </tr>
 </tbody>
</table>

### Livelli di registro disponibili nell&#39;area di lavoro Moduli AEM {#log-levels-available-in-nbsp-aem-forms-workspace}

* FATTILE
* ERRORE
* AVVISO
* INFO
* DEBUG
* TRACE
* DISATTIVATO

## Informazioni sul debug per i browser {#debugging-information-for-browsers}

È possibile eseguire il debug di script e stili in diversi browser.

* **Debug in IE**: Per eseguire il debug dell&#39;area di lavoro Moduli AEM in IE, vedi: [https://msdn.microsoft.com/en-us/library/hh772704(v=vs.85).aspx](https://msdn.microsoft.com/en-us/library/hh772704(v=vs.85).aspx).

* **Debug in Chrome**: Per aprire il debugger in Chrome, utilizzate la scelta rapida: Ctrl+Maiusc+I. Per ulteriori informazioni, vedi: [https://developer.chrome.com/extensions/tut_debugging.html](https://developer.chrome.com/extensions/tut_debugging.html).

* **Debug in Firefox**: Diversi componenti aggiuntivi sono disponibili per il debug di script e stili in Firefox. Ad esempio, Firebug è una di queste utilità di debug ([https://getfirebug.com](https://getfirebug.com)).

## Domande frequenti {#faqs}

1. Il modulo PDF non viene sottoposto a rendering o inviato in Google Chrome.

   1. Installate il plug-in Adobe® Reader®.
   1. In Chrome, aprite chrome://plugins per visualizzare i plug-in disponibili.
   1. Disattivate il plug-in per visualizzatori PDF Chrome e attivate il plug-in Adobe Reader.

1. Il rendering del modulo o della guida SWF non viene eseguito in Google Chrome.

   1. In Chrome, aprite chrome://plugins per visualizzare i plug-in disponibili.
   1. Consultate i dettagli per il plug-in di Adobe Flash® Player.
   1. Disattivate PepperFlash nel plug-in di Adobe Flash Player.

1. L’area di lavoro Moduli AEM è stata personalizzata ma non è possibile visualizzare le modifiche.

   Cancella la cache del browser e accedi all&#39;area di lavoro Moduli AEM.

1. Cosa deve essere fatto dall&#39;utente per consentire il rendering del modulo in HTML quando viene aperto sul desktop?

   Selezionare il pulsante di scelta HTML per il profilo predefinito nella fase di assegnazione dell&#39;attività durante l&#39;utilizzo di Workbench.

1. L&#39;allegato non viene visualizzato quando si fa clic su di esso.

   Per visualizzare gli allegati, abilita i pop-up nel browser.

1. Un utente ha eseguito il login a un&#39;applicazione dei moduli. Se l’utente tenta di accedere all’area di lavoro, potrebbe non essere caricato se non dispone delle autorizzazioni per l’area di lavoro.

   Disconnettersi dall&#39;applicazione altri moduli, quindi accedere all&#39;area di lavoro.

1. Nei moduli HTML, che utilizzano le proprietà di processo nella relativa struttura, quando viene eseguito il rendering nell&#39;area di lavoro Moduli AEM, viene visualizzato il pulsante Invia all&#39;interno del modulo.

   Durante la progettazione dei moduli, quando si utilizza Proprietà processo, all&#39;interno del modulo viene aggiunto un pulsante Invia. Durante il rendering come PDF nell’area di lavoro Moduli AEM, il pulsante Invia non è visibile all’utente finale. Tuttavia, quando si esegue il rendering come modulo HTML nell&#39;area di lavoro Moduli AEM, all&#39;utente finale è visibile il pulsante Invia. Se si fa clic sul pulsante Invia all&#39;interno del modulo, non viene avviata alcuna azione. Fai clic sul pulsante Invia nella parte inferiore dell’area di lavoro Moduli AEM, all’esterno del modulo, per completare l’attività.

[Contattare il supporto](https://www.adobe.com/account/sign-in.supportportal.html)
