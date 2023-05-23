---
title: Descrizione dei componenti riutilizzabili
seo-title: Description of reusable components
description: Un elenco completo dei componenti riutilizzabili con nomi di file e dipendenze, per aiutarti a integrare il componente Workspace di AEM Forms nelle applicazioni web.
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

L’area di lavoro di AEM Forms è composta da [riutilizzabile](/help/forms/using/integrating-html-ws-components-web.md) componenti organizzati in uno specifico [struttura di cartelle](/help/forms/using/folder-structure.md) in CRX™. Ogni componente dispone di un file di modello, di visualizzazione e di modello nella posizione specificata nella struttura della cartella, di dipendenze JavaScript™ da altri file di componenti, di eventi in ascolto dal componente e di oggetti JavaScript che attivano questi eventi nell’area di lavoro di AEM Forms. L’elenco completo dei componenti riutilizzabili con i nomi dei file e le dipendenze dei componenti è disponibile qui.

## ElencoAttività {#tasklist}

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
     <li><p>Attività team</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td>
    <ul>
     <li><p>modello di attività</p></li>
     <li><p>modello teamtask</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventi in ascolto (nome evento - Attivatore)</p></td>
   <td>
    <ul>
     <li><p>filterSelected - modello elenco attività</p></li>
     <li><p>rimuovi - modello elenco attività</p></li>
     <li><p>updateQueue - modello elenco attività</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Questo componente può essere utilizzato indipendentemente dall’area di lavoro di AEM Forms, purché si attivi l’evento filterSelected per questo componente dall’applicazione personalizzata.

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
     <li><p>modello elenco attività</p></li>
     <li><p>utilità taskactions</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventi in ascolto (nome evento - Attivatore)</p></td>
   <td>
    <ul>
     <li><p>submitComplete - modello di attività</p></li>
     <li><p>Rifiuta - Modello attività</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Workspace richiama la funzione fetchTasks del modello TaskList per creare modelli di attività per questo componente.

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
   <td><p>Eventi in ascolto (nome evento - Attivatore)</p></td>
   <td>
    <ul>
     <li><p>recuperato - modello elenco attività </p></li>
     <li><p>rimuovi - modello elenco attività </p></li>
     <li><p>updateQueue - modello elenco attività </p></li>
     <li><p>refreshedQueue - modello elenco attività </p></li>
     <li><p>filterSelected - modello elenco attività</p></li>
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
     <li><p>Campo: queue: { name, qid, isDefault, type}</p> </li>
     <li><p>Campo: query: string</p> </li>
     <li><p>Campo: parentView: visualizzazione elenco filtri</p> </li>
     <li><p>Campo: parentModel: modello elenco attività</p> </li>
     <li><p>Campo: utility</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Eventi ascoltati</p> </td>
   <td><p>ND</p> </td>
  </tr>
 </tbody>
</table>

## TeamQueues {#teamqueues}

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
   <td><p>Eventi in ascolto (nome evento - Attivatore)</p></td>
   <td>
    <ul>
     <li><p>recuperato - modello elenco attività </p></li>
     <li><p>rimuovi - modello elenco attività </p></li>
     <li><p>updateQueue - modello elenco attività </p></li>
     <li><p>teamQueuesFetched - modello di elenco attività </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## FiltroTeam {#teamfilter}

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
     <li><p>Estende : visualizzazione filtro</p> </li>
     <li><p>Campo : queue :{ name, qid, isDefault, type }</p> </li>
     <li><p>Campo : query : string</p> </li>
     <li><p>Campo : parentView : visualizzazione elenco filtri</p> </li>
     <li><p>Campo : parentModel : modello di elenco attività</p> </li>
     <li><p>Campo : utility</p> </li>
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
>TeamFilter ottiene l&#39;evento che indica quale attività è stata selezionata dal componente TaskList. Anche se questi componenti condividono la classe del modello, non c&#39;è altra dipendenza.

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
   <td><p>La maggior parte delle classi di utilità</p> </td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p> </td>
   <td>
    <ul>
     <li><p>processinstancehistory.html</p> </li>
     <li><p>utilità formrendering</p> </li>
     <li><p>utilità notes</p> </li>
     <li><p>utilità allegati</p> </li>
     <li><p>utilità taskactions</p> </li>
     <li><p>utilità cronologia</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Eventi in ascolto (nome evento - Attivatore)</p> </td>
   <td>
    <ul>
     <li><p>inoltrato - modello di attività</p> </li>
     <li><p>condiviso - modello di attività</p> </li>
     <li><p>consultato - modello di attività</p> </li>
     <li><p>rifiutato - modello attività</p> </li>
     <li><p>abbandonato - modello attività</p> </li>
     <li><p>sbloccato - modello attività</p> </li>
     <li><p>bloccato - modello attività</p> </li>
     <li><p>reclamato - modello attività</p> </li>
     <li><p>modifica:selezione task - modello elenco task</p> </li>
     <li><p>change:formUrl - modello di attività</p> </li>
     <li>attachmentURLFetched - modello di attività</li>
    </ul>
    <ul>
     <li>newAttachment - modello di attività</li>
     <li><p>taskHistoryFetched - modello di attività</p> </li>
     <li>preparationForSubmitComplete - modello di attività</li>
     <li><p>submitComplete - modello di attività</p> </li>
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
     <li><p>favoritecategoryfactory model</p></li>
     <li><p>allcategoryfactory model</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventi in ascolto (nome evento - Attivatore)</p></td>
   <td>
    <ul>
     <li><p>allStartpointsFetched - modello categorylist </p></li>
     <li><p>aggiungi - modello categorylist </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Questo componente utilizza classi modello di altri componenti come StartPointList, StartPoint e Task. Oltre a questa dipendenza, CategoryList può essere utilizzato in modo indipendente.

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
     <li><p>modello categorylist</p></li>
     <li><p>modello startpointlist</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventi in ascolto (nome evento - Attivatore)</p></td>
   <td>
    <ul>
     <li><p>modificato - modello categoria </p></li>
     <li><p>childrenFetched - modello di categoria </p></li>
     <li><p>categoria:selezionata - modello elenco categorie </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## ElencoPuntiInizio {#startpointlist}

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
     <li><p>favoritecategoryfactory model</p></li>
     <li><p>allcategoryfactory model</p></li>
     <li><p>vista punto d'inizio</p></li>
     <li><p>modello startpointlist</p></li>
     <li><p>modello punto d'inizio</p></li>
     <li><p>modello di attività</p></li>
     <li><p>modello di attività</p></li>
     <li><p>modello elenco attività</p></li>
     <li><p>modello teamtask</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventi in ascolto (nome evento - Attivatore)</p></td>
   <td>
    <ul>
     <li><p>categoria:selezionata - modello elenco categorie </p></li>
     <li><p>allStartpointsFetched - modello categorylist </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>I componenti StartPointList e CategoryList condividono la classe del modello, pertanto il primo dipende dal secondo. CategoryList consente di accedere alle informazioni sui punti iniziali della categoria visualizzati. Per utilizzare StartPointList in modo indipendente, simulare il trigger di evento da CategoryList.

## PuntoInizio {#startpoint}

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
   <td><p>modello di attività</p></td>
  </tr>
  <tr>
   <td><p>Eventi in ascolto (nome evento - Attivatore)</p></td>
   <td><p>modifica - modello punto d'inizio </p></td>
  </tr>
 </tbody>
</table>

## AvviaProcesso {#startprocess}

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
     <li><p>La maggior parte delle classi di utilità</p> </li>
     <li><p>UserSearch</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p> </td>
   <td>
    <ul>
     <li><p>modello di categoria</p> </li>
     <li><p>favoritecategoryfactory model</p> </li>
     <li><p>allcategoryfactory model</p> </li>
     <li><p>utilità formrendering</p> </li>
     <li><p>utilità notes</p> </li>
     <li><p>utilità allegati</p> </li>
     <li><p>utilità taskactions</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Eventi in ascolto (nome evento - Attivatore)</p> </td>
   <td>
    <ul>
     <li><p>categoria:selezionata - modello elenco categorie</p> </li>
     <li><p>modifica:invokedTask - modello startpointlist</p> </li>
     <li><p>change:formUrl - modello di attività</p> </li>
     <li><p>punto d'inizio:selezionato - modello startpointlist</p> </li>
     <li><p>inoltrato - modello di attività</p> </li>
     <li><p>abbandonato - modello attività</p> </li>
     <li><p>sbloccato - modello attività</p> </li>
     <li><p>bloccato - modello attività</p> </li>
     <li>attachmentURLFetched - modello di attività</li>
     <li>newAttachment - modello di attività</li>
     <li>preparationForSubmitComplete - modello di attività </li>
     <li><p>submitComplete - modello di attività</p> </li>
     <li><p>allStartpointsFetched - modello categorylist</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>I componenti StartProcess e StartPointList condividono la classe del modello. Questo componente diventa rilevante quando si seleziona un punto iniziale da StartPointList.

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
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td><p>modello nomeprocesso</p></td>
  </tr>
  <tr>
   <td><p>Eventi in ascolto (nome evento - Attivatore)</p></td>
   <td>
    <ul>
     <li><p>add - modello processnamelist </p></li>
     <li><p>recuperato:nomi di processo - modello processnamelist </p></li>
     <li><p>change - modello processnamelist </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessNameList non dipende da altri componenti. Tuttavia, internamente dipende dalla classe di modello ProcessInstanceList che a sua volta dipende da altri componenti. ProcessNameList utilizza pertanto molte classi di modelli quali ProcessInstanceList, ProcessInstance, TaskList, Teamtask e Task. Oltre a queste dipendenze, ProcessNameList può essere utilizzato in modo indipendente.

## NomeProcesso {#processname}

<table>
 <tbody>
  <tr>
   <td><p>Modello</p></td>
   <td><p>processname.js</p></td>
  </tr>
  <tr>
   <td><p>Visualizzazione</p></td>
   <td><p>nomeprocesso (in processnamelist.js)</p></td>
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
   <td><p>Eventi in ascolto (nome evento - Attivatore)</p></td>
   <td><p>change - modello nomeprocesso </p></td>
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
   <td><p>ND</p></td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p></td>
   <td><p>modello nomeprocesso</p></td>
  </tr>
  <tr>
   <td><p>Eventi in ascolto (nome evento - Attivatore)</p></td>
   <td>
    <ul>
     <li><p>nomeprocesso:selezionato - modello di elenco dei nomi di processo </p></li>
     <li><p>nomeprocesso:istanze recuperate - modello processnamelist </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceList prevede un evento da ProcessNameList che indica il nome del processo per il recupero e la visualizzazione delle istanze. Per utilizzare ProcessInstanceList in modo indipendente, simulare separatamente l&#39;attivazione dell&#39;evento.

## ProcessInstance {#processinstance}

<table>
 <tbody>
  <tr>
   <td><p>Modello</p></td>
   <td><p>processinstance.js</p></td>
  </tr>
  <tr>
   <td><p>Visualizzazione</p></td>
   <td><p>nomeprocesso in processnamelist.js</p></td>
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
   <td><p>modello elenco attività</p></td>
  </tr>
  <tr>
   <td><p>Eventi in ascolto (nome evento - Attivatore)</p></td>
   <td><p>change - modello processinstance </p></td>
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
     <li><p>modello nomeprocesso</p></li>
     <li><p>utilità cronologia</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>Eventi in ascolto (nome evento - Attivatore)</p></td>
   <td>
    <ul>
     <li><p>nomeprocesso:selezionato - modello di elenco dei nomi di processo </p></li>
     <li><p>processinstance:selezionata - modello processinstancelist </p></li>
     <li><p>tasksFetched - processinstance model </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceHistory prevede un evento da ProcessInstanceList che indica la cronologia dell&#39;istanza di processo da visualizzare. Oltre a questa dipendenza, il componente può essere utilizzato in modo indipendente.

## Fuori sede {#outofoffice}

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
   <td><p>vista usersearch</p> </td>
  </tr>
  <tr>
   <td><p>Eventi in ascolto (nome evento - Attivatore)</p> </td>
   <td>
    <ul>
     <li><p>outOfOfficeSettingsFetched - modello fuori sede</p> </li>
     <li><p>outOfOfficeSettingsSaved - modello fuori sede</p> </li>
     <li><p>processFetched - modello fuori sede</p> </li>
     <li><p>principalSelected - vista principalsearch</p> </li>
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
   <td><p>vista usersearch</p> </td>
  </tr>
  <tr>
   <td><p>Eventi in ascolto (nome evento - Attivatore)</p> </td>
   <td>
    <ul>
     <li><p>queueAccessGranted - modello di coda</p> </li>
     <li><p>queueAccessRequested - modello di coda</p> </li>
     <li><p>grantUsersFetched - modello sharequeue</p> </li>
     <li>accessibleUsersFetched - modello sharequeue</li>
     <li><p>queueAccessRevoked - modello di coda</p> </li>
     <li><p>queueAccessRemoved - modello di coda</p> </li>
     <li><p>principalSelected - vista principalsearch</p> </li>
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
   <td><p>Eventi in ascolto (nome evento - Attivatore)</p></td>
   <td>
    <ul>
     <li><p>preferencesFetched - modello uisettings </p></li>
     <li><p>settingUpdated: modello di impostazioni uisettings </p></li>
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
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p> </td>
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Eventi in ascolto (nome evento - Attivatore)</p> </td>
   <td>
    <ul>
     <li>userImageUrlFetched - modello userinfo</li>
     <li>sessionRenewed - userinfo model <br /> </li>
     <li>sessionExpired: modello userinfo </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>UserInfo può essere utilizzato in modo indipendente.

## Errore {#wserror}

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
   <td><p>Eventi in ascolto (nome evento - Attivatore)</p></td>
   <td><p>newWsError - modello wserror </p></td>
  </tr>
 </tbody>
</table>

## UserSearch {#usersearch}

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
   <td><p>Eventi in ascolto (nome evento - Attivatore)</p> </td>
   <td>
    <ul>
     <li>principalSearched - modello principalsearch</li>
     <li>outOfOfficeInfoFetched - modello usersearch</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## CercaModello {#searchtemplate}

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
   <td><p>Eventi in ascolto (nome evento - Attivatore)</p> </td>
   <td><p>templateFetched- modello searchtemplate</p> </td>
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
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p> </td>
   <td><p>modello searchtemplate</p> </td>
  </tr>
  <tr>
   <td><p>Eventi in ascolto (nome evento - Attivatore)</p> </td>
   <td><p>modifica - modello searchtemplatelist</p> </td>
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
   <td><p>ND</p> </td>
  </tr>
  <tr>
   <td><p>Dipendenze JS</p> </td>
   <td>ND<br /> </td>
  </tr>
  <tr>
   <td><p>Eventi in ascolto (nome evento - Attivatore)</p> </td>
   <td><p>searchTemplate:selezionato - modello di modello di ricerca</p> </td>
  </tr>
 </tbody>
</table>
