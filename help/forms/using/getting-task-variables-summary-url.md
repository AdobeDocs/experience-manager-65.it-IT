---
title: Ottenimento delle variabili attività nell'URL di riepilogo
seo-title: Ottenimento delle variabili attività nell'URL di riepilogo
description: Procedura per riutilizzare le informazioni su un’attività e generare un URL di riepilogo per riepilogare o descrivere un’attività.
seo-description: Procedura per riutilizzare le informazioni su un’attività e generare un URL di riepilogo per riepilogare o descrivere un’attività.
uuid: 9eab3a6a-a99a-40ae-b483-33ec7d21c5b6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6dc31bec-b02d-47db-a4f4-be8c14c5619e
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---


# Ottenimento delle variabili attività nell&#39;URL di riepilogo {#getting-task-variables-in-summary-url}

Nella pagina di riepilogo sono visualizzate le informazioni relative all’attività. Questo articolo descrive come riutilizzare le informazioni relative alle attività nella pagina di riepilogo.

In questa orchestrazione di esempio, un dipendente invia un modulo di richiesta di congedo. Il modulo di richiesta va quindi al responsabile del dipendente per l&#39;approvazione.

1. Create un renderer HTML di esempio (html.esp) per il tipo di risorse **Dipendenti/PtoApplication**.

   Il renderer presuppone l&#39;impostazione delle seguenti proprietà sul nodo:

   * ename
   * empid
   * reason
   * duration

   >[!NOTE]
   >
   >Questo renderer è il modello di pagina di riepilogo.

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

1. Modificare l&#39;orchestrazione per estrarre le quattro proprietà dai dati del modulo inviato. Dopo questo, creare un nodo in CRX di tipo **Dipendenti/PtoApplication**, con le proprietà popolate.

   1. Creare un processo **creare un riepilogo** PTO e utilizzarlo come sottoprocesso prima dell&#39;operazione **Assegna attività** nell&#39;orchestrazione.
   1. Definisci **dipendenteName**, **dipendenteID**, **ptoReason**, **totalDays** e **nodeName** come variabili di input nel nuovo processo. Queste variabili verranno trasmesse come dati del modulo inviato.

      Definite anche una variabile di output **ptoNodePath** che verrà utilizzata per impostare l’URL di riepilogo.

   1. Nel processo di **creazione del riepilogo** PTO, utilizzate il componente **set value** per impostare i dettagli di input in una mappa **nodeProperty**(**nodeProps**).

      Le chiavi in questa mappa devono corrispondere alle chiavi definite nel renderer HTML nel passaggio precedente.

      Inoltre, aggiungete una chiave **sling:resourceType** con il valore **Dipendenti/PtoApplication** nella mappa.

   1. Utilizzate il sottoprocesso **storeContent** dal servizio **ContentRepositoryConnector** nel processo di **creazione del riepilogo** PTO. Questo sottoprocesso crea un nodo CRX.

      Sono necessarie tre variabili di input:

      * **Percorso** cartella: Percorso in cui viene creato il nuovo nodo CRX. Impostate il percorso come **/content**.
      * **Nome** nodo: Assegnare la variabile di input nodeName a questo campo. Si tratta di una stringa nome di nodo univoca.
      * **Tipo** nodo: Definire il tipo come **nt:unstructure**. L&#39;output di questo processo è nodePath. nodePath è il percorso CRX del nodo appena creato. Il percorso ndoePath è l’output finale del processo di **creazione del riepilogo PTO** .
   1. Passa i dati del modulo inviati (**dipendenteName**, **dipendenteID**, **ptoReason** e **totalDays**) come input al nuovo processo di **creazione del riepilogo** PTO. Assumere l’output come **ptoSummaryNodePath**.


1. Definire l&#39;URL di riepilogo come espressione XPath contenente i dettagli del server insieme a **ptoSummaryNodePath**.

   XPath: `concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`.

Nell’area di lavoro AEM Forms, quando si apre un’attività, l’URL di riepilogo accede al nodo CRX, mentre il renderer HTML visualizza il riepilogo.

Il layout di riepilogo può essere modificato senza modificare il processo. Il renderer HTML visualizza il riepilogo in modo appropriato.
