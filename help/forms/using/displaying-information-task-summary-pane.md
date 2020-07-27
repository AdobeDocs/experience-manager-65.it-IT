---
title: Visualizzazione delle informazioni nel riquadro Riepilogo attività
seo-title: Visualizzazione delle informazioni nel riquadro Riepilogo attività
description: Nell'area di lavoro AEM Forms, è possibile configurare un riquadro Riepilogo attività per riepilogare l'attività o visualizzare qualsiasi altra pagina Web.
seo-description: Nell'area di lavoro AEM Forms, è possibile configurare un riquadro Riepilogo attività per riepilogare l'attività o visualizzare qualsiasi altra pagina Web.
uuid: 2fcc3d9f-0ec2-4250-8dc1-9746fd72ea60
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 90d0f584-b598-4b21-85d7-31da5f13d404
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---


# Visualizzazione delle informazioni nel riquadro Riepilogo attività {#displaying-information-in-the-task-summary-pane}

Quando si apre un&#39;attività nell&#39;area di lavoro AEM Forms, un riquadro Riepilogo attività può visualizzare un riepilogo dell&#39;attività. Queste informazioni aggiuntive e rilevanti per un’attività aggiungono maggiore valore all’utente finale dell’area di lavoro AEM Forms.

L’area di lavoro AEM Forms consente di visualizzare una pagina Web di propria scelta nel riquadro Riepilogo attività. È possibile creare un processo per visualizzare un riquadro Riepilogo attività utilizzando Workbench.

1. Creare un processo Assegna attività in Workbench. Per ulteriori dettagli sull&#39;operazione Assegna task, vedere l&#39;argomento Riferimento servizio nella Guida [di](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/)Workbench.

   >[!NOTE]
   >
   >Se esiste un URL TaskSummary, per impostazione predefinita viene visualizzata la visualizzazione Riepilogo attività al posto della visualizzazione Modulo. In questo caso, anche quando un utente abilita l&#39;opzione &quot;Apri il modulo in modalità ingrandita&quot; in Assegna attività, il modulo non si apre in modalità ingrandita.

1. Configurare il campo URL riepilogo attività. È possibile specificare un valore letterale, un modello, una variabile o un&#39;espressione XPath.
1. Di seguito è riportato un esempio di visualizzazione delle informazioni nella pagina Riepilogo attività.

   * Accedete all&#39;ambiente CRXDE Lite all&#39;indirizzo `https://'[server]:[port]'/lc/crx/de`.
   * `Create a node`**SampleSummary **` under `/` with type `content:`. In the properties of this node, add `unstructuredsling:` of type String and value ``. In the Access Control List of this node, add an entry for `resourceTypeSampleSummaryPERM_WORKSPACE_` allowing `USERjcr:read` privileges.`
   * `Create a folder`**SampleSummary **in`/apps`. Nell’elenco di controllo degli accessi di`/apps/SampleSummary`, aggiungere una voce per l’`PERM_WORKSPACE_USER`autorizzazione`jcr:readprivileges`.
   * `Create a file `html.esp` at `/apps/`. For example, add the following lines in `SampleSummaryhtml.esp`.`

   ```html
   <html>
       <body>
           <h1>Sample Summary</h1>
           <br/>
           <p>Hello Sir!
               <br/>
               This is sample summary page for this task.
           </p>
       </body>
   </html>
   ```

   * Impostate il valore dell&#39;URL di riepilogo attività come `/lc/content/SampleSummary.html` nel passaggio Assegna attività.
   * Quando l&#39;attività associata a questo passaggio Assegna attività viene aperta nell&#39;area di lavoro AEM Forms, viene eseguito il rendering `html.esp` in `/apps/SampleSummary` nel riquadro di riepilogo delle attività.
