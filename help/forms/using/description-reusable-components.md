---
title: Descrizione dei componenti riutilizzabili
seo-title: Descrizione dei componenti riutilizzabili
description: Un elenco completo di componenti riutilizzabili con nomi di file e dipendenze per integrare  componente area di lavoro AEM Forms nelle applicazioni Web.
seo-description: Un elenco completo di componenti riutilizzabili con nomi di file e dipendenze per integrare  componente area di lavoro AEM Forms nelle applicazioni Web.
uuid: 8e6accc7-0935-4d7b-b838-d23676df5cda
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: d3facd17-ceb0-4799-8cd9-ff9e81e09793
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '1257'
ht-degree: 9%

---


# Descrizione dei componenti riutilizzabili {#description-of-reusable-components}

&#39;area di lavoro AEM Forms è composta da [componenti riutilizzabili](/help/forms/using/integrating-html-ws-components-web.md) organizzati in una struttura [di cartelle ](/help/forms/using/folder-structure.md) specifica in CRX™. Ciascun componente dispone di un modello, una vista e un file di modello nella posizione specificata nella struttura delle cartelle, dipendenze JavaScript™ da altri file componenti, eventi ascoltati dagli oggetti componenti e JavaScript che attivano tali eventi &#39;area di lavoro di AEM Forms. L&#39;elenco completo dei componenti riutilizzabili con nomi file e dipendenze dei componenti è riportato qui.

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
     <li><p>UserSearch</p></li>
     <li><p>Attività</p></li>
     <li><p>Teamtask</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td>
    <ul>
     <li><p>task model</p></li>
     <li><p>modello di gruppo</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (nome evento - Trigger)</p></td>
   <td>
    <ul>
     <li><p>filterSelected - modello elenco di task</p></li>
     <li><p>remove - modello elenco attività</p></li>
     <li><p>updateQueue - modello elenco di task</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Questo componente può essere utilizzato indipendentemente ’area di lavoro di AEM Forms, a condizione che sia attivato un evento filterSelezionato per questo componente dall’applicazione personalizzata.

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
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td>
    <ul>
     <li><p>modello lista di task</p></li>
     <li><p>utility task</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (nome evento - Trigger)</p></td>
   <td>
    <ul>
     <li><p>submitComplete - modello task</p></li>
     <li><p>Rifiuta - modello task</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>L&#39;area di lavoro chiama la funzione fetchTasks del modello TaskList per creare modelli di task per questo componente.

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
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (nome evento - Trigger)</p></td>
   <td>
    <ul>
     <li><p>fetching - modello elenco attività </p></li>
     <li><p>remove - modello elenco attività </p></li>
     <li><p>updateQueue - modello elenco di task </p></li>
     <li><p>refreshQueue - modello elenco di task </p></li>
     <li><p>filterSelected - modello elenco di task</p></li>
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
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p> </td>
   <td>
    <ul>
     <li><p>Campo: coda: { name, qid, isDefault, type}</p> </li>
     <li><p>Campo: query: string</p> </li>
     <li><p>Campo: parentView: visualizzazione elenco filtri</p> </li>
     <li><p>Campo: parentModel: modello lista di task</p> </li>
     <li><p>Campo: utility</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati</p> </td>
   <td><p>NA</p> </td>
  </tr>
 </tbody>
</table>

## TeamCode {#teamqueues}

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
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (nome evento - Trigger)</p></td>
   <td>
    <ul>
     <li><p>fetching - modello elenco attività </p></li>
     <li><p>remove - modello elenco attività </p></li>
     <li><p>updateQueue - modello elenco di task </p></li>
     <li><p>teamQueuesFetched - modello elenco di task </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## TeamFilter {#teamfilter}

<table>
 <tbody>
  <tr>
   <td><p>Modello</p> </td>
   <td><p>NA</p> </td>
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
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p> </td>
   <td>
    <ul>
     <li><p>Estende : visualizzazione filtro</p> </li>
     <li><p>Campo : queue :{ nome, qid, isDefault, type }</p> </li>
     <li><p>Campo : query: string</p> </li>
     <li><p>Campo : parentView : visualizzazione elenco filtri</p> </li>
     <li><p>Campo : parentModel : modello lista di task</p> </li>
     <li><p>Campo : utility</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati</p> </td>
   <td><p>NA</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>TeamFilter riceve l&#39;evento che indica quale attività è stata selezionata dal componente TaskList. Sebbene questi componenti condividano la classe del modello, non esiste altra dipendenza.

## TaskDetails {#taskdetails}

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
     <li><p>formrendering, utilità</p> </li>
     <li><p>notes utility</p> </li>
     <li><p>utility allegati</p> </li>
     <li><p>utility task</p> </li>
     <li><p>utility di cronologia</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (nome evento - Trigger)</p> </td>
   <td>
    <ul>
     <li><p>inoltrato - modello di task</p> </li>
     <li><p>shared - task model</p> </li>
     <li><p>Consultato - modello dei compiti</p> </li>
     <li><p>rifiutato - modello task</p> </li>
     <li><p>abbandonato - modello</p> </li>
     <li><p>sbloccato - modello task</p> </li>
     <li><p>bloccato - modello task</p> </li>
     <li><p>reclamato - modello task</p> </li>
     <li><p>modifica:task selezionato - modello elenco task</p> </li>
     <li><p>change:formUrl - modello di task</p> </li>
     <li>attachmentURLFetched - modello attività</li>
    </ul>
    <ul>
     <li>newAttachment - modello di task</li>
     <li><p>taskHistoryFetched - modello di task</p> </li>
     <li>readyForSubmitComplete - modello di task</li>
     <li><p>submitComplete - modello task</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## CategoryList {#categorylist}

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
     <li><p>favoritecategoryfactory</p></li>
     <li><p>allcategoryfactory, modello</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (nome evento - Trigger)</p></td>
   <td>
    <ul>
     <li><p>allInitipointsFetched - categorylist model </p></li>
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
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td>
    <ul>
     <li><p>categorylist, modello</p></li>
     <li><p>startpointlist, modello</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (nome evento - Trigger)</p></td>
   <td>
    <ul>
     <li><p>changed - category model </p></li>
     <li><p>childFetched - modello di categoria </p></li>
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
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td>
    <ul>
     <li><p>category model</p></li>
     <li><p>favoritecategoryfactory</p></li>
     <li><p>allcategoryfactory, modello</p></li>
     <li><p>startpoint view</p></li>
     <li><p>startpointlist, modello</p></li>
     <li><p>startpoint, modello</p></li>
     <li><p>task model</p></li>
     <li><p>task model</p></li>
     <li><p>modello lista di task</p></li>
     <li><p>modello di gruppo</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (nome evento - Trigger)</p></td>
   <td>
    <ul>
     <li><p>categoria:selezionata - modello elenco categorie </p></li>
     <li><p>allInitipointsFetched - categorylist model </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>I componenti StartPointList e CategoryList condividono la classe del modello, pertanto il primo dipende dal secondo. CategoryList accede alle informazioni sui punti iniziali della categoria visualizzati. Per utilizzare StartPointList in modo indipendente, simulare l&#39;attivatore dell&#39;evento da CategoryList.

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
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td><p>task model</p></td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (nome evento - Trigger)</p></td>
   <td><p>change - startpoint model </p></td>
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
     <li><p>UserSearch</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p> </td>
   <td>
    <ul>
     <li><p>category model</p> </li>
     <li><p>favoritecategoryfactory</p> </li>
     <li><p>allcategoryfactory, modello</p> </li>
     <li><p>formrendering, utilità</p> </li>
     <li><p>notes utility</p> </li>
     <li><p>utility allegati</p> </li>
     <li><p>utility task</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (nome evento - Trigger)</p> </td>
   <td>
    <ul>
     <li><p>categoria:selezionata - modello elenco categorie</p> </li>
     <li><p>change:invogliateTask - startpointlist, modello</p> </li>
     <li><p>change:formUrl - modello di task</p> </li>
     <li><p>startpoint:selected - startpointlist, modello</p> </li>
     <li><p>inoltrato - modello di task</p> </li>
     <li><p>abbandonato - modello</p> </li>
     <li><p>sbloccato - modello task</p> </li>
     <li><p>bloccato - modello task</p> </li>
     <li>attachmentURLFetched - modello attività</li>
     <li>newAttachment - modello di task</li>
     <li>readyForSubmitComplete - modello di task </li>
     <li><p>submitComplete - modello task</p> </li>
     <li><p>allInitipointsFetched - categorylist model</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>I componenti StartProcess e StartPointList condividono la classe del modello. Questo componente diventa rilevante e si seleziona un punto di inizio da StartPointList.

## ProcessNameList {#processnamelist}

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
   <td><p>tracking.html (nella cartella route)</p></td>
  </tr>
  <tr>
   <td><p>Richiede componenti</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td><p>processname, modello</p></td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (nome evento - Trigger)</p></td>
   <td>
    <ul>
     <li><p>add - processnamelist model </p></li>
     <li><p>fetching:processnames - processnamelist model </p></li>
     <li><p>change - processnamelist model </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessNameList non dipende da altri componenti. Tuttavia, internamente dipende dalla classe del modello ProcessInstanceList che a sua volta dipende da altri componenti. Quindi, ProcessNameList utilizza molte classi di modelli come ProcessInstanceList, ProcessInstance, TaskList, Teamtask e Task. Oltre a queste dipendenze, ProcessNameList può essere utilizzato in modo indipendente.

## ProcessName {#processname}

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
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td><p>processinstancelist, modello</p></td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (nome evento - Trigger)</p></td>
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
   <td><p>tracking.html (nella cartella route)</p></td>
  </tr>
  <tr>
   <td><p>Richiede componenti</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td><p>processname, modello</p></td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (nome evento - Trigger)</p></td>
   <td>
    <ul>
     <li><p>nomeprocesso:selected - modello di elenco di processi </p></li>
     <li><p>processname:instancesfetched - processnamelist model </p></li>
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
   <td><p>processname inside processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>Modello</p></td>
   <td><p>processinstance.html</p></td>
  </tr>
  <tr>
   <td><p>Richiede componenti</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td><p>modello lista di task</p></td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (nome evento - Trigger)</p></td>
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
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td>
    <ul>
     <li><p>processname, modello</p></li>
     <li><p>utility di cronologia</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (nome evento - Trigger)</p></td>
   <td>
    <ul>
     <li><p>nomeprocesso:selected - modello di elenco di processi </p></li>
     <li><p>processinstance:selected - processinstancelist model </p></li>
     <li><p>TasksFetched - Process instance model </p></li>
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
   <td><p>UserSearch</p> </td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p> </td>
   <td><p>visualizzazione ricerca utente</p> </td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (nome evento - Trigger)</p> </td>
   <td>
    <ul>
     <li><p>outOfOfficeSettingsFetched - Modello outofoffice</p> </li>
     <li><p>outOfOfficeSettingsSaved - outOfOfficeSettingsSaved</p> </li>
     <li><p>processFetched - Modello outofoffice</p> </li>
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
   <td><p>UserSearch</p> </td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p> </td>
   <td><p>visualizzazione ricerca utente</p> </td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (nome evento - Trigger)</p> </td>
   <td>
    <ul>
     <li><p>queueAccessGranted - sharequeue, modello</p> </li>
     <li><p>queueAccessRequired - sharequeue, modello</p> </li>
     <li><p>givenUsersFetched - sharequeue, modello</p> </li>
     <li>accessUsersFetched - sharequeue, modello</li>
     <li><p>queueAccessRevked - modello di nitidezza</p> </li>
     <li><p>queueAccessRemoved - sharequeue, modello</p> </li>
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
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (nome evento - Trigger)</p></td>
   <td>
    <ul>
     <li><p>preferencesFetched - modello di impostazioni </p></li>
     <li><p>settingUpdated - uisettings model </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>UISettings può essere utilizzato in modo indipendente.

## AppNavigation {#appnavigation}

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
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati</p></td>
   <td><p>NA</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AppNavigation può essere utilizzato in modo indipendente.

## UserInfo {#userinfo}

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
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (nome evento - Trigger)</p> </td>
   <td>
    <ul>
     <li>userImageUrlFetched - modello userinfo</li>
     <li>sessionRinnovato - modello userinfo <br /> </li>
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
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td><p>NA</p></td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (nome evento - Trigger)</p></td>
   <td><p>newWsError - modello di errore </p></td>
  </tr>
 </tbody>
</table>

## Ricerca utente {#usersearch}

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
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (nome evento - Trigger)</p> </td>
   <td>
    <ul>
     <li>principalSearched - modello di ricerca principale</li>
     <li>outOfOfficeInfoFetched - modello di ricerca utente</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## SearchTemplate {#searchtemplate}

<table>
 <tbody>
  <tr>
   <td><p>Modello</p> </td>
   <td><p>searchtemplate.js</p> </td>
  </tr>
  <tr>
   <td><p>Visualizzazione</p> </td>
   <td><p>search template (in search templatelist.js) </p> </td>
  </tr>
  <tr>
   <td><p>Modello</p> </td>
   <td><p>searchtemplate.html</p> </td>
  </tr>
  <tr>
   <td><p>Richiede componenti</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (nome evento - Trigger)</p> </td>
   <td><p>templateFetched - modello di ricerca</p> </td>
  </tr>
 </tbody>
</table>

## SearchTemplateList {#searchtemplatelist}

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
   <td><p>tracking.html (nella cartella route)</p> </td>
  </tr>
  <tr>
   <td><p>Richiede componenti</p> </td>
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p> </td>
   <td><p>search template, modello</p> </td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (nome evento - Trigger)</p> </td>
   <td><p>change - ricertemplatelist model</p> </td>
  </tr>
 </tbody>
</table>

## SearchTemplateDetails {#searchtemplatedetails}

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
   <td><p>NA</p> </td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p> </td>
   <td>NA<br /> </td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati (nome evento - Trigger)</p> </td>
   <td><p>searchTemplate:selected - modello di ricerca</p> </td>
  </tr>
 </tbody>
</table>
