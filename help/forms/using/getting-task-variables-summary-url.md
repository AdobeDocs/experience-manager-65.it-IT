---
title: Recupero variabili attività nell’URL di riepilogo
seo-title: Getting Task Variables in Summary URL
description: Riutilizzare le informazioni su un'attività e generare un URL di riepilogo per riepilogare o descrivere un'attività.
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

# Recupero variabili attività nell’URL di riepilogo {#getting-task-variables-in-summary-url}

Nella pagina di riepilogo vengono visualizzate le informazioni relative all&#39;attività. Questo articolo descrive come riutilizzare le informazioni relative alle attività nella pagina di riepilogo.

In questa orchestrazione di esempio, un dipendente invia un modulo di richiesta di congedo. Il modulo di domanda viene quindi inviato al responsabile del dipendente per l&#39;approvazione.

1. Crea un modulo di rendering HTML di esempio (html.esp) per resourseType **Dipendenti/PtoApplication**.

   Il renderer presuppone che le seguenti proprietà siano impostate sul nodo:

   * ename
   * empid
   * motivo
   * durata

   >[!NOTE]
   >
   >Questo renderer è il modello della pagina di riepilogo.

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

1. Modifica l’orchestrazione per estrare le quattro proprietà dai dati del modulo inviati. In seguito, crea un nodo in CRX di tipo **Dipendenti/PtoApplication**, con le proprietà popolate.

   1. Creare un processo **crea riepilogo PTO** e utilizzalo come processo secondario prima del **Assegna attività** nell&#39;orchestrazione.
   1. Definisci **employeeName**, **employeeID**, **ptoReason**, **totalDays**, e **nodeName** come variabili di input nel nuovo processo. Queste variabili verranno trasmesse come dati del modulo inviati.

      Definisci anche una variabile di output **ptoNodePath** che verrà utilizzato durante l’impostazione dell’URL di riepilogo.

   1. In **crea riepilogo PTO** processo, utilizza **imposta valore** per impostare i dettagli di input in una **nodeProperty**(**nodeProps**) mappa.

      Le chiavi in questa mappa devono essere identiche a quelle definite nel renderer HTML nel passaggio precedente.

      Inoltre, aggiungi **sling:resourceType** chiave con valore **Dipendenti/PtoApplication** nella mappa.

   1. Utilizzare il processo secondario **storeContent** dal **ConnettoreArchivioContenuti** servizio in **crea riepilogo PTO** processo. Questo processo secondario crea un nodo CRX.

      Sono necessarie tre variabili di input:

      * **Percorso cartella**: percorso in cui viene creato il nuovo nodo CRX. Imposta il percorso come **/content**.
      * **Nome nodo**: assegna la variabile di input nodeName a questo campo. Questa è una stringa con nome di nodo univoco.
      * **Tipo di nodo**: definisci il tipo come **nt:unstructured**. L&#39;output di questo processo è nodePath. Il percorso nodePath è il percorso CRX del nodo appena creato. Il ndoePath è l’output finale del **crea PTO** processo di riepilogo.
   1. Trasmettere i dati modulo inviati (**employeeName**, **employeeID**, **ptoReason**, e **totalDays**) come input per il nuovo processo **crea riepilogo PTO**. Considera l’output come **ptoSummaryNodePath**.


1. Definisci l’URL di riepilogo come espressione XPath contenente i dettagli del server e **ptoSummaryNodePath**.

   XPath: `concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`.

Nell’area di lavoro di AEM Forms, quando apri un’attività, l’URL di riepilogo accede al nodo CRX e il renderer HTML visualizza il riepilogo.

Il layout del riepilogo può essere modificato senza modificare il processo. Il renderer HTML visualizza il riepilogo in modo appropriato.
