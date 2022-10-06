---
title: Descrizione dei componenti riutilizzabili
seo-title: Description of reusable components
description: Un elenco completo dei componenti riutilizzabili con nomi di file e dipendenze, per facilitare l’integrazione del componente Workspace di AEM Forms nelle applicazioni web.
seo-description: A complete list of reusable components with filenames and dependencies, to help you integrate AEM Forms workspace component in your web applications.
uuid: 8e6accc7-0935-4d7b-b838-d23676df5cda
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: d3facd17-ceb0-4799-8cd9-ff9e81e09793
exl-id: b8cb7233-3d9e-41d4-85c5-8e8c2481f89c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1231'
ht-degree: 9%

---

# Descrizione dei componenti riutilizzabili {#description-of-reusable-components}

L’area di lavoro di AEM Forms è composta da [riutilizzabile](/help/forms/using/integrating-html-ws-components-web.md) componenti organizzati in un [struttura a cartelle](/help/forms/using/folder-structure.md) in CRX™. Ogni componente dispone di un file modello, vista e modello nel percorso specificato nella struttura delle cartelle, dipendenze JavaScript™ da altri file di componenti, eventi ascoltati dal componente e oggetti JavaScript che attivano tali eventi nell’area di lavoro di AEM Forms. L&#39;elenco completo dei componenti riutilizzabili con nomi di file e dipendenze costituenti è riportato qui.

## Elenco attività {#tasklist}

<table>
 <tbody>
  <tr>
   <td><p>Modello</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>Visualizzazione</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>Modello</p></td>
   <td><p>tasklist.html</p></td>
  </tr>
  <tr>
   <td><p>Richiede componenti</p></td>
   <td>
    <ul>
     <li><p>RicercaUtente</p></li>
     <li><p>Attività</p></li>
     <li><p>Gruppo</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td>
    <ul>
     <li><p>modello task</p></li>
     <li><p>modello a mano</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (Nome evento - Trigger)</p></td>
   <td>
    <ul>
     <li><p>filterSelected - modello elenco task</p></li>
     <li><p>remove - tasklist, modello</p></li>
     <li><p>updateQueue - modello elenco task</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Questo componente può essere utilizzato indipendentemente dall’area di lavoro di AEM Forms, a condizione che si attivi l’evento filterSelected per questo componente dall’applicazione personalizzata.

## Attività {#task}

<table>
 <tbody>
  <tr>
   <td><p>Modello</p></td>
   <td><p>task.js</p></td>
  </tr>
  <tr>
   <td><p>Visualizzazione</p></td>
   <td><p>task.js</p></td>
  </tr>
  <tr>
   <td><p>Modello</p></td>
   <td><p>task.html</p></td>
  </tr>
  <tr>
   <td><p>Richiede componenti</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td>
    <ul>
     <li><p>modello a elenco delle applicazioni</p></li>
     <li><p>utility taskazioni</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (Nome evento - Trigger)</p></td>
   <td>
    <ul>
     <li><p>submitComplete - modello task</p></li>
     <li><p>Rifiuto: modello task</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Workspace chiama la funzione fetchTasks del modello TaskList per creare modelli Task per questo componente.

## FilterList {#filterlist}

<table>
 <tbody>
  <tr>
   <td><p>Modello</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>Visualizzazione</p></td>
   <td><p>filterlist.js</p></td>
  </tr>
  <tr>
   <td><p>Modello</p></td>
   <td><p>filterlist.html</p></td>
  </tr>
  <tr>
   <td><p>Richiede componenti</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (Nome evento - Trigger)</p></td>
   <td>
    <ul>
     <li><p>recuperato - modello elenco task </p></li>
     <li><p>remove - tasklist, modello </p></li>
     <li><p>updateQueue - modello elenco task </p></li>
     <li><p>refreshQueue - modello elenco task </p></li>
     <li><p>filterSelected - modello elenco task</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## Filtro {#filter}

<table>
 <tbody>
  <tr>
   <td><p>Visualizzazione</p> </td>
   <td><p>filter.js</p> </td>
  </tr>
  <tr>
   <td><p>Modello</p> </td>
   <td><p>filter.html</p> </td>
  </tr>
  <tr>
   <td><p>Richiede componenti</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p> </td>
   <td>
    <ul>
     <li><p>Campo: coda: { nome, qid, isDefault, type}</p> </li>
     <li><p>Campo: query: string</p> </li>
     <li><p>Campo: parentView: visualizzazione elenco filtri</p> </li>
     <li><p>Campo: parentModel: modello a elenco delle applicazioni</p> </li>
     <li><p>Campo: utilità</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati</p> </td>
   <td><p>ND</p> </td>
  </tr>
 </tbody>
</table>

## CodeTeam {#teamqueues}

<table>
 <tbody>
  <tr>
   <td><p>Modello</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>Visualizzazione</p></td>
   <td><p>teamqueues.js</p></td>
  </tr>
  <tr>
   <td><p>Modello</p></td>
   <td><p>teamqueues.html</p></td>
  </tr>
  <tr>
   <td><p>Richiede componenti</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (Nome evento - Trigger)</p></td>
   <td>
    <ul>
     <li><p>recuperato - modello elenco task </p></li>
     <li><p>remove - tasklist, modello </p></li>
     <li><p>updateQueue - modello elenco task </p></li>
     <li><p>teamQueuesFetched - modello elenco task </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## TeamFilter {#teamfilter}

<table>
 <tbody>
  <tr>
   <td><p>Modello</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Visualizzazione</p> </td>
   <td><p>teamfilter.js</p> </td>
  </tr>
  <tr>
   <td><p>Modello</p> </td>
   <td><p>teamfilter.html</p> </td>
  </tr>
  <tr>
   <td><p>Richiede componenti</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p> </td>
   <td>
    <ul>
     <li><p>Estende : vista a filtri</p> </li>
     <li><p>Campo : coda :{ nome, qid, isDefault, type }</p> </li>
     <li><p>Campo : query : string</p> </li>
     <li><p>Campo : parentView : visualizzazione elenco filtri</p> </li>
     <li><p>Campo : parentModel : modello a elenco delle applicazioni</p> </li>
     <li><p>Campo : utilità</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati</p> </td>
   <td><p>ND</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>TeamFilter ottiene l&#39;evento che indica quale attività è stata selezionata dal componente TaskList. Sebbene questi componenti condividano la classe del modello, non vi sono altre dipendenze.

## DettagliAttività {#taskdetails}

<table>
 <tbody>
  <tr>
   <td><p>Modello</p> </td>
   <td><p>tasklist.js</p> </td>
  </tr>
  <tr>
   <td><p>Visualizzazione</p> </td>
   <td><p>taskdetails.js</p> </td>
  </tr>
  <tr>
   <td><p>Modello</p> </td>
   <td><p>taskdetails.html</p> </td>
  </tr>
  <tr>
   <td><p>Richiede componenti</p> </td>
   <td><p>La maggior parte delle classi Utility</p> </td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p> </td>
   <td>
    <ul>
     <li><p>processinstancehistory.html</p> </li>
     <li><p>utility di rendering dei moduli</p> </li>
     <li><p>utilità note</p> </li>
     <li><p>utilità allegati</p> </li>
     <li><p>utility taskazioni</p> </li>
     <li><p>utilità di cronologia</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (Nome evento - Trigger)</p> </td>
   <td>
    <ul>
     <li><p>inoltrato - modello di task</p> </li>
     <li><p>condiviso - modello task</p> </li>
     <li><p>consultato - modello dei compiti</p> </li>
     <li><p>rifiutato - modello task</p> </li>
     <li><p>abbandonato - modello di task</p> </li>
     <li><p>sbloccato - modello task</p> </li>
     <li><p>bloccato - modello task</p> </li>
     <li><p>rivendicato - modello task</p> </li>
     <li><p>modifica:task selezionato - modello elenco task</p> </li>
     <li><p>change:formUrl - modello di task</p> </li>
     <li>attachmentURLFetched - modello di task</li>
    </ul>
    <ul>
     <li>newAttachment - modello di task</li>
     <li><p>taskHistoryFetched - modello task</p> </li>
     <li>PrepareForSubmitComplete - modello di task</li>
     <li><p>submitComplete - modello task</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Elenco categorie {#categorylist}

<table>
 <tbody>
  <tr>
   <td><p>Modello</p></td>
   <td><p>categorylist.js</p></td>
  </tr>
  <tr>
   <td><p>Visualizzazione</p></td>
   <td><p>categorylist.js</p></td>
  </tr>
  <tr>
   <td><p>Modello</p></td>
   <td><p>startprocess.html (nella cartella route)</p></td>
  </tr>
  <tr>
   <td><p>Richiede componenti</p></td>
   <td><p>Categoria</p></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td>
    <ul>
     <li><p>modello favoritecategoryfactory</p></li>
     <li><p>modello allcategoryfactory</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (Nome evento - Trigger)</p></td>
   <td>
    <ul>
     <li><p>allStartpointsFetched - categorylist model </p></li>
     <li><p>add - categorylist, modello </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Questo componente utilizza le classi di modelli di altri componenti come StartPointList, StartPoint e Task. Oltre a questa dipendenza, CategoryList può essere utilizzato in modo indipendente.

## Categoria {#category}

<table>
 <tbody>
  <tr>
   <td><p>Modello</p></td>
   <td><p>category.js</p></td>
  </tr>
  <tr>
   <td><p>Visualizzazione</p></td>
   <td><p>category.js</p></td>
  </tr>
  <tr>
   <td><p>Modello</p></td>
   <td><p>category.html</p></td>
  </tr>
  <tr>
   <td><p>Richiede componenti</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td>
    <ul>
     <li><p>modello a elenco categorie</p></li>
     <li><p>modello startpointlist</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (Nome evento - Trigger)</p></td>
   <td>
    <ul>
     <li><p>modificato - modello di categoria </p></li>
     <li><p>childrenFetched - modello di categoria </p></li>
     <li><p>categoria:selezionata - modello elenco categorie </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## StartPointList {#startpointlist}

<table>
 <tbody>
  <tr>
   <td><p>Modello</p></td>
   <td><p>categorylist.js</p></td>
  </tr>
  <tr>
   <td><p>Visualizzazione</p></td>
   <td><p>startpointlist.js</p></td>
  </tr>
  <tr>
   <td><p>Modello</p></td>
   <td><p>startprocess.html (nella cartella route)</p></td>
  </tr>
  <tr>
   <td><p>Richiede componenti</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td>
    <ul>
     <li><p>modello di categoria</p></li>
     <li><p>modello favoritecategoryfactory</p></li>
     <li><p>modello allcategoryfactory</p></li>
     <li><p>vista iniziale</p></li>
     <li><p>modello startpointlist</p></li>
     <li><p>modello startpoint</p></li>
     <li><p>modello task</p></li>
     <li><p>modello task</p></li>
     <li><p>modello a elenco delle applicazioni</p></li>
     <li><p>modello a mano</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (Nome evento - Trigger)</p></td>
   <td>
    <ul>
     <li><p>categoria:selezionata - modello elenco categorie </p></li>
     <li><p>allStartpointsFetched - categorylist model </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>I componenti StartPointList e CategoryList condividono la classe del modello, quindi il primo dipende da quest&#39;ultimo. CategoryList accede alle informazioni sui punti iniziali della categoria visualizzati. Per utilizzare StartPointList in modo indipendente, simulare il trigger dell&#39;evento da CategoryList.

## StartPoint {#startpoint}

<table>
 <tbody>
  <tr>
   <td><p>Modello</p></td>
   <td><p>startpoint.js</p></td>
  </tr>
  <tr>
   <td><p>Visualizzazione</p></td>
   <td><p>startpoint.js</p></td>
  </tr>
  <tr>
   <td><p>Modello</p></td>
   <td><p>startpoint.html</p></td>
  </tr>
  <tr>
   <td><p>Richiede componenti</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td><p>modello task</p></td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (Nome evento - Trigger)</p></td>
   <td><p>change - modello startpoint </p></td>
  </tr>
 </tbody>
</table>

## StartProcess {#startprocess}

<table>
 <tbody>
  <tr>
   <td><p>Modello</p> </td>
   <td><p>categorylist.js</p> </td>
  </tr>
  <tr>
   <td><p>Visualizzazione</p> </td>
   <td><p>startprocess.js</p> </td>
  </tr>
  <tr>
   <td><p>Modello</p> </td>
   <td><p>startprocess.html</p> </td>
  </tr>
  <tr>
   <td><p>Richiede componenti</p> </td>
   <td>
    <ul>
     <li><p>La maggior parte delle classi Utility</p> </li>
     <li><p>RicercaUtente</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p> </td>
   <td>
    <ul>
     <li><p>modello di categoria</p> </li>
     <li><p>modello favoritecategoryfactory</p> </li>
     <li><p>modello allcategoryfactory</p> </li>
     <li><p>utility di rendering dei moduli</p> </li>
     <li><p>utilità note</p> </li>
     <li><p>utilità allegati</p> </li>
     <li><p>utility taskazioni</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (Nome evento - Trigger)</p> </td>
   <td>
    <ul>
     <li><p>categoria:selezionata - modello elenco categorie</p> </li>
     <li><p>change:invogliatoTask - modello startpointlist</p> </li>
     <li><p>change:formUrl - modello di task</p> </li>
     <li><p>startpoint:selected - modello startpointlist</p> </li>
     <li><p>inoltrato - modello di task</p> </li>
     <li><p>abbandonato - modello di task</p> </li>
     <li><p>sbloccato - modello task</p> </li>
     <li><p>bloccato - modello task</p> </li>
     <li>attachmentURLFetched - modello di task</li>
     <li>newAttachment - modello di task</li>
     <li>PrepareForSubmitComplete - modello di task </li>
     <li><p>submitComplete - modello task</p> </li>
     <li><p>allStartpointsFetched - categorylist model</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>I componenti StartProcess e StartPointList condividono la classe del modello. Questo componente diventa rilevante quando si seleziona un punto iniziale da StartPointList.

## ElencoNomeProcesso {#processnamelist}

<table>
 <tbody>
  <tr>
   <td><p>Modello</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>Visualizzazione</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>Modello</p></td>
   <td><p>tracking.html (nella cartella del percorso)</p></td>
  </tr>
  <tr>
   <td><p>Richiede componenti</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td><p>modello nome processo</p></td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (Nome evento - Trigger)</p></td>
   <td>
    <ul>
     <li><p>add - processnamelist, modello </p></li>
     <li><p>fetched:processnames - modello processnamelist </p></li>
     <li><p>change - modello processnamelist </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessNameList non dipende da altri componenti. Tuttavia, internamente dipende dalla classe del modello ProcessInstanceList che a sua volta dipende da altri componenti. Quindi, ProcessNameList utilizza molte classi di modelli come ProcessInstanceList, ProcessInstance, TaskList, Teamtask e Task. Oltre a queste dipendenze, ProcessNameList può essere utilizzato in modo indipendente.

## NomeProcesso {#processname}

<table>
 <tbody>
  <tr>
   <td><p>Modello</p></td>
   <td><p>processname.js</p></td>
  </tr>
  <tr>
   <td><p>Visualizzazione</p></td>
   <td><p>processname (in processnamelist.js)</p></td>
  </tr>
  <tr>
   <td><p>Modello</p></td>
   <td><p>processname.html</p></td>
  </tr>
  <tr>
   <td><p>Richiede componenti</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td><p>modello processinstancelist</p></td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (Nome evento - Trigger)</p></td>
   <td><p>change - processname model </p></td>
  </tr>
 </tbody>
</table>

## ProcessInstanceList {#processinstancelist}

<table>
 <tbody>
  <tr>
   <td><p>Modello</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>Visualizzazione</p></td>
   <td><p>processinstancelist.js</p></td>
  </tr>
  <tr>
   <td><p>Modello</p></td>
   <td><p>tracking.html (nella cartella del percorso)</p></td>
  </tr>
  <tr>
   <td><p>Richiede componenti</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td><p>modello nome processo</p></td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (Nome evento - Trigger)</p></td>
   <td>
    <ul>
     <li><p>nome processo:selected - modello di elenchi di processi </p></li>
     <li><p>nomeprocesso:instancesfetched - modello processnamelist </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceList prevede un evento da ProcessNameList che indica il nome del processo per il recupero e la visualizzazione delle istanze. Per utilizzare ProcessInstanceList in modo indipendente, simulare l&#39;attivazione dell&#39;evento separatamente.

## ProcessInstance {#processinstance}

<table>
 <tbody>
  <tr>
   <td><p>Modello</p></td>
   <td><p>processinstance.js</p></td>
  </tr>
  <tr>
   <td><p>Visualizzazione</p></td>
   <td><p>processname all'interno di processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>Modello</p></td>
   <td><p>processinstance.html</p></td>
  </tr>
  <tr>
   <td><p>Richiede componenti</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td><p>modello a elenco delle applicazioni</p></td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (Nome evento - Trigger)</p></td>
   <td><p>change - process instance model </p></td>
  </tr>
 </tbody>
</table>

## ProcessInstanceHistory {#processinstancehistory}

<table>
 <tbody>
  <tr>
   <td><p>Modello</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>Visualizzazione</p></td>
   <td><p>processinstancehistory.js</p></td>
  </tr>
  <tr>
   <td><p>Modello</p></td>
   <td><p>processinstancehistory.html</p></td>
  </tr>
  <tr>
   <td><p>Richiede componenti</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td>
    <ul>
     <li><p>modello nome processo</p></li>
     <li><p>utilità di cronologia</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (Nome evento - Trigger)</p></td>
   <td>
    <ul>
     <li><p>nome processo:selected - modello di elenchi di processi </p></li>
     <li><p>processinstance:selected - processinstancelist model </p></li>
     <li><p>TasksFetched - process instance model </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceHistory prevede un evento da ProcessInstanceList che indica la cronologia dell&#39;istanza di processo da visualizzare. Oltre a questa dipendenza, il componente può essere utilizzato in modo indipendente.

## OutofOffice {#outofoffice}

<table>
 <tbody>
  <tr>
   <td><p>Modello</p> </td>
   <td><p>outofoffice.js</p> </td>
  </tr>
  <tr>
   <td><p>Visualizzazione</p> </td>
   <td><p>outofoffice.js</p> </td>
  </tr>
  <tr>
   <td><p>Modello</p> </td>
   <td><p>outofoffice.html</p> </td>
  </tr>
  <tr>
   <td><p>Richiede componenti</p> </td>
   <td><p>RicercaUtente</p> </td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p> </td>
   <td><p>visualizzazione ricerca utente</p> </td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (Nome evento - Trigger)</p> </td>
   <td>
    <ul>
     <li><p>outOfOfficeSettingsFetched - modello outofoffice</p> </li>
     <li><p>outOfOfficeSettingsSaved - modello di spazio</p> </li>
     <li><p>processFetched - modello outofoffice</p> </li>
     <li><p>principalSelected - visualizzazione ricerca principale</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>OutofOffice può essere utilizzato in modo indipendente.

## ShareQueue {#sharequeue}

<table>
 <tbody>
  <tr>
   <td><p>Modello</p> </td>
   <td><p>sharequeue.js</p> </td>
  </tr>
  <tr>
   <td><p>Visualizzazione</p> </td>
   <td><p>sharequeue.js</p> </td>
  </tr>
  <tr>
   <td><p>Modello</p> </td>
   <td><p>sharequeue.html</p> </td>
  </tr>
  <tr>
   <td><p>Richiede componenti</p> </td>
   <td><p>RicercaUtente</p> </td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p> </td>
   <td><p>visualizzazione ricerca utente</p> </td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (Nome evento - Trigger)</p> </td>
   <td>
    <ul>
     <li><p>queueAccessGranted - modello di condivisione</p> </li>
     <li><p>queueAccessRequested - modello di condivisione</p> </li>
     <li><p>allowUsersFetched - modello di condivisione</p> </li>
     <li>accessibleUsersFetched - modello di condivisione</li>
     <li><p>queueAccessRevked - modello di condivisione</p> </li>
     <li><p>queueAccessRemoved - modello di condivisione</p> </li>
     <li><p>principalSelected - visualizzazione ricerca principale</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ShareQueue può essere utilizzato in modo indipendente.

## UISettings {#uisettings}

<table>
 <tbody>
  <tr>
   <td><p>Modello</p></td>
   <td><p>uisettings.js</p></td>
  </tr>
  <tr>
   <td><p>Visualizzazione</p></td>
   <td><p>uisettings.js</p></td>
  </tr>
  <tr>
   <td><p>Modello</p></td>
   <td><p>uisettings.html</p></td>
  </tr>
  <tr>
   <td><p>Richiede componenti</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (Nome evento - Trigger)</p></td>
   <td>
    <ul>
     <li><p>preferencesFetched - modello di utenze </p></li>
     <li><p>settingUpdated - modello di utilizzo </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>UISettings può essere utilizzato indipendentemente.

## NavigazioneApp {#appnavigation}

<table>
 <tbody>
  <tr>
   <td><p>Modello</p></td>
   <td><p>appnavigation.js</p></td>
  </tr>
  <tr>
   <td><p>Visualizzazione</p></td>
   <td><p>appnavigation.js</p></td>
  </tr>
  <tr>
   <td><p>Modello</p></td>
   <td><p>appnavigation.html</p></td>
  </tr>
  <tr>
   <td><p>Richiede componenti</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati</p></td>
   <td><p>ND</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AppNavigation può essere utilizzato indipendentemente.

## InformazioniUtente {#userinfo}

<table>
 <tbody>
  <tr>
   <td><p>Modello</p> </td>
   <td><p>userinfo.js</p> </td>
  </tr>
  <tr>
   <td><p>Visualizzazione</p> </td>
   <td><p>userinfo.js</p> </td>
  </tr>
  <tr>
   <td><p>Modello</p> </td>
   <td><p>userinfo.html</p> </td>
  </tr>
  <tr>
   <td><p>Richiede componenti</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (Nome evento - Trigger)</p> </td>
   <td>
    <ul>
     <li>userImageUrlFetched - modello userinfo</li>
     <li>sessionRenewed - modello userinfo <br /> </li>
     <li>sessionExpired - modello userinfo </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>UserInfo può essere utilizzato in modo indipendente.

## WSError {#wserror}

<table>
 <tbody>
  <tr>
   <td><p>Modello</p></td>
   <td><p>wserror.js</p></td>
  </tr>
  <tr>
   <td><p>Visualizzazione</p></td>
   <td><p>wserror.js</p></td>
  </tr>
  <tr>
   <td><p>Modello</p></td>
   <td><p>wserror.html</p></td>
  </tr>
  <tr>
   <td><p>Richiede componenti</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (Nome evento - Trigger)</p></td>
   <td><p>newWsError - modello wserror </p></td>
  </tr>
 </tbody>
</table>

## RicercaUtente {#usersearch}

<table>
 <tbody>
  <tr>
   <td><p>Modello</p> </td>
   <td><p>usersearch.js</p> </td>
  </tr>
  <tr>
   <td><p>Visualizzazione</p> </td>
   <td><p>usersearch.js</p> </td>
  </tr>
  <tr>
   <td><p>Modello</p> </td>
   <td><p>usersearch.html</p> </td>
  </tr>
  <tr>
   <td><p>Richiede componenti</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (Nome evento - Trigger)</p> </td>
   <td>
    <ul>
     <li>principalSearched - modello di ricerca principale</li>
     <li>outOfOfficeInfoFetched - modello di ricerca utente</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Modello di ricerca {#searchtemplate}

<table>
 <tbody>
  <tr>
   <td><p>Modello</p> </td>
   <td><p>searchtemplate.js</p> </td>
  </tr>
  <tr>
   <td><p>Visualizzazione</p> </td>
   <td><p>searchtemplate (in searchtemplatelist.js) </p> </td>
  </tr>
  <tr>
   <td><p>Modello</p> </td>
   <td><p>searchtemplate.html</p> </td>
  </tr>
  <tr>
   <td><p>Richiede componenti</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (Nome evento - Trigger)</p> </td>
   <td><p>templateFetched- modello di ricerca</p> </td>
  </tr>
 </tbody>
</table>

## ElencoModelliRicerca {#searchtemplatelist}

<table>
 <tbody>
  <tr>
   <td><p>Modello</p> </td>
   <td><p>searchtemplatelist.js</p> </td>
  </tr>
  <tr>
   <td><p>Visualizzazione</p> </td>
   <td><p>searchtemplatelist.js</p> </td>
  </tr>
  <tr>
   <td><p>Modello</p> </td>
   <td><p>tracking.html (nella cartella del percorso)</p> </td>
  </tr>
  <tr>
   <td><p>Richiede componenti</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p> </td>
   <td><p>modello di ricerca</p> </td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (Nome evento - Trigger)</p> </td>
   <td><p>change - modello searchtemplatelist</p> </td>
  </tr>
 </tbody>
</table>

## DettagliModelloRicerca {#searchtemplatedetails}

<table>
 <tbody>
  <tr>
   <td><p>Modello</p> </td>
   <td><p>searchtemplatelist.js</p> </td>
  </tr>
  <tr>
   <td><p>Visualizzazione</p> </td>
   <td><p>searchtemplatedetails.js</p> </td>
  </tr>
  <tr>
   <td><p>Modello</p> </td>
   <td><p>searchtemplatedetails.html</p> </td>
  </tr>
  <tr>
   <td><p>Richiede componenti</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p> </td>
   <td>ND<br /> </td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (Nome evento - Trigger)</p> </td>
   <td><p>searchTemplate:selected - modello di ricerca</p> </td>
  </tr>
 </tbody>
</table>
