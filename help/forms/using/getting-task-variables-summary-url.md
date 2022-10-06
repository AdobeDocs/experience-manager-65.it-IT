---
title: Ottenimento di variabili di attività nell’URL di riepilogo
seo-title: Getting Task Variables in Summary URL
description: Come riutilizzare le informazioni su un'attività e generare un URL di riepilogo per riepilogare o descrivere un'attività.
seo-description: How-to reuse the information about a task and generate a Summary URL to summarize or describe a task.
uuid: 9eab3a6a-a99a-40ae-b483-33ec7d21c5b6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6dc31bec-b02d-47db-a4f4-be8c14c5619e
exl-id: b5e27b54-d141-48dd-a4ed-dd0a691319a5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# Ottenimento di variabili di attività nell’URL di riepilogo {#getting-task-variables-in-summary-url}

Nella pagina di riepilogo sono visualizzate le informazioni relative all’attività. Questo articolo descrive come riutilizzare le informazioni relative alle attività nella pagina di riepilogo.

In questa orchestrazione di esempio, un dipendente invia un modulo di richiesta di congedo. Il modulo di richiesta va quindi al responsabile del dipendente per l&#39;approvazione.

1. Crea un modulo di rendering HTML di esempio (html.esp) per resourseType **Dipendenti/PtoApplication**.

   Il renderer presuppone che le seguenti proprietà siano impostate sul nodo:

   * Nome
   * empid
   * reason
   * duration

   >[!NOTE]
   >
   >Questo modulo di rendering è il modello di pagina di riepilogo.

   Il seguente codice di esempio per questo renderer è contenuto in:

   `apps/Employees/PtoApplication/html.esp`

   ```html
   <html>
     <body>
       <table>
       <tbody>
       <tr>
           <td>
               <h3>Employee Name: <%= currentNode.ename %></h3>
               <h3>Employee ID: <%= currentNode.eid %></h3>
               <h3>Leave duration: <%= currentNode.duration %> days</h3>
               <h3>Reason: <%= currentNode.reason %></h3>
           </td>
       </tr>
       </tbody>
       </table>
     </body>
   </html>
   ```

1. Modificare l’orchestrazione per estrarre le quattro proprietà dai dati del modulo inviati. Dopo questo crea un nodo in CRX di tipo **Dipendenti/PtoApplication**, con le proprietà popolate.

   1. Creare un processo **crea riepilogo PTO** e utilizzarlo come sottoprocesso prima della **Assegna attività** nell&#39;orchestrazione.
   1. Definisci **dipendenteName**, **IDdipendente**, **ptoReason**, **totalDays** e **nodeName** come variabili di input nel nuovo processo. Queste variabili verranno trasmesse come dati del modulo inviato.

      Definire anche una variabile di output **ptoNodePath** che verrà utilizzato durante l&#39;impostazione dell&#39;URL di riepilogo.

   1. In **crea riepilogo PTO** , utilizza **imposta valore** per impostare i dettagli di input in un **nodeProperty**(**nodeProps**) mappa.

      Le chiavi in questa mappa devono corrispondere alle chiavi definite nel renderer di HTML nel passaggio precedente.

      Inoltre, aggiungi un **sling:resourceType** chiave con valore **Dipendenti/PtoApplication** nella mappa.

   1. Utilizzare il sottoprocesso **storeContent** dal **ContentRepositoryConnector** nel **crea riepilogo PTO** processo. Questo sottoprocesso crea un nodo CRX.

      Sono necessarie tre variabili di input:

      * **Percorso cartella**: Il percorso in cui viene creato il nuovo nodo CRX. Imposta il percorso come **/content**.
      * **Nome nodo**: Assegna la variabile di input nodeName a questo campo. Questa è una stringa di nome di nodo univoco.
      * **Tipo di nodo**: Definisci il tipo come **nt:unstructured**. L&#39;output di questo processo è nodePath. Il nodePath è il percorso CRX del nodo appena creato. Il percorso ndoePath sarà l&#39;output finale del **crea PTO** processo di riepilogo.
   1. Passa i dati del modulo inviati (**dipendenteName**, **IDdipendente**, **ptoReason** e **totalDays**) come contributo al nuovo processo **crea riepilogo PTO**. Prendi l&#39;output come **ptoSummaryNodePath**.


1. Definisci l&#39;URL di riepilogo come espressione XPath contenente i dettagli del server insieme a **ptoSummaryNodePath**.

   XPath: `concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`.

Nell’area di lavoro di AEM Forms, quando apri un’attività, l’URL di riepilogo accede al nodo CRX e il modulo di rendering di HTML visualizza il riepilogo.

Il layout di riepilogo può essere modificato senza modificare il processo. Il modulo di rendering di HTML visualizza il riepilogo in modo appropriato.
