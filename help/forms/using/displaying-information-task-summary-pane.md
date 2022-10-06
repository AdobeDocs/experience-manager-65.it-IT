---
title: Visualizzazione delle informazioni nel riquadro Riepilogo attività
seo-title: Displaying information in the Task Summary pane
description: Nell’area di lavoro di AEM Forms, è possibile configurare un riquadro Riepilogo attività per riepilogare l’attività o visualizzare qualsiasi altra pagina Web.
seo-description: In AEM Forms workspace, a Task Summary pane can be configured to summarize the task or display any other web page.
uuid: 2fcc3d9f-0ec2-4250-8dc1-9746fd72ea60
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 90d0f584-b598-4b21-85d7-31da5f13d404
exl-id: 0b3087fe-a3fb-4eac-ad4b-c123526e8195
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Visualizzazione delle informazioni nel riquadro Riepilogo attività {#displaying-information-in-the-task-summary-pane}

Quando si apre un’attività nell’area di lavoro di AEM Forms, in un riquadro Riepilogo attività è possibile visualizzare un riepilogo dell’attività. Queste informazioni aggiuntive e rilevanti per un’attività aggiungono più valore all’utente finale di AEM Forms workspace.

L’area di lavoro di AEM Forms consente di visualizzare una pagina Web a scelta nel riquadro Riepilogo attività. È possibile creare un processo per visualizzare un riquadro Riepilogo attività utilizzando Workbench.

1. Crea un processo di assegnazione attività in Workbench. Per ulteriori dettagli sull&#39;operazione Assegna attività, vedere l&#39;argomento Riferimento servizio in [Guida di Workbench](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/).

   >[!NOTE]
   >
   >Se esiste un URL di riepilogo attività, la visualizzazione Riepilogo attività viene visualizzata per impostazione predefinita al posto della visualizzazione Maschera. In questo caso, anche quando un utente abilita l’opzione &quot;Apri il modulo in modalità ingrandita&quot; in Assegna attività, il modulo non si apre in modalità ingrandita.

1. Configura il campo URL di riepilogo attività. È possibile specificare un valore letterale, un modello, una variabile o un&#39;espressione XPath.
1. Di seguito è riportato un esempio di visualizzazione delle informazioni nella pagina Riepilogo attività.

   * Accedi all’ambiente CRXDE Lite in `https://'[server]:[port]'/lc/crx/de`.
   * `Create a node`**RiepilogoEsempio** ` under `/content` with type `nt:unstructured`. In the properties of this node, add `sling:resourceType` of type String and value `RiepilogoEsempio`. In the Access Control List of this node, add an entry for `PERM_WORKSPACE_USER` allowing `jcr:read` privileges.`
   * `Create a folder`**RiepilogoEsempio** sotto `/apps`. Nell&#39;elenco di controllo accessi di `/apps/SampleSummary`, aggiungi una voce per `PERM_WORKSPACE_USER` permettere `jcr:readprivileges`.
   * `Create a file `html.esp` at `/apps/SampleSummary`. For example, add the following lines in `html.esp`.`

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

   * Imposta il valore dell&#39;url di riepilogo attività come `/lc/content/SampleSummary.html` nel passaggio Assegna attività .
   * Quando l’attività associata a questo passaggio Assegna attività viene aperta nell’area di lavoro di AEM Forms, la `html.esp` a `/apps/SampleSummary` viene eseguito il rendering nel riquadro di riepilogo delle attività.
