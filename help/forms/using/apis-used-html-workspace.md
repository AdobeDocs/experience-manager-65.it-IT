---
title: API utilizzate nell'area di lavoro  AEM Forms
seo-title: API utilizzate nell'area di lavoro  AEM Forms
description: API Java e JavaScript pubblici e metodi dell'area di lavoro di LiveCycle  AEM Forms, esposti per la personalizzazione e l'automazione.
seo-description: API Java e JavaScript pubblici e metodi dell'area di lavoro di LiveCycle  AEM Forms, esposti per la personalizzazione e l'automazione.
uuid: 9602990e-8ac7-42eb-b507-50b3594055ba
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 4a73a973-fccf-466b-b4a0-47652a14a080
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 1%

---


# API utilizzate nell&#39;area di lavoro  AEM Forms {#apis-used-in-aem-forms-workspace}

Le seguenti API vengono utilizzate nell&#39;area di lavoro  AEM Forms.

<table>
 <tbody>
  <tr>
   <td><strong>Metodo Javascript</strong></td>
   <td><strong>Nome servizio</strong></td>
   <td><strong>Nome API</strong></td>
   <td><strong>Commenti</strong></td>
  </tr>
  <tr>
   <td>getGroups</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getGroups</td>
   <td>Cerca nei gruppi. restituisce un elenco di tutti i gruppi se non viene specificato nulla, altrimenti restituisce i gruppi con il nome specificato.</td>
  </tr>
  <tr>
   <td>getUsersAndGroups</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsersAndGroups</td>
   <td>Esegue la ricerca di utenti e gruppi. Restituisce un elenco di tutti gli utenti e i gruppi se non è stato specificato nulla, altrimenti restituisce utenti e gruppi con nome specificato.</td>
  </tr>
  <tr>
   <td>PreparaPerInvia</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>PreparaPerInvia</td>
   <td>Viene chiamato prima dell'invio del modulo tramite DocumentSubmitServlet. Imposta l’ID dell’attività in una variabile di sessione (insieme all’ora di scadenza) recuperata durante l’invio effettivo.</td>
  </tr>
  <tr>
   <td>submitTask</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>submit</td>
   <td>Invia l'oggetto documento associato a un'attività (e a sua volta invia il processo).</td>
  </tr>
  <tr>
   <td>getRootEndpointCategories</td>
   <td>ProcessManagementInitipointService</td>
   <td>getRootEndpointCategories</td>
   <td>Recupera tutte le categorie principali presenti sul server.</td>
  </tr>
  <tr>
   <td>getDirectChildCategories</td>
   <td>ProcessManagementInitipointService</td>
   <td>getDirectChildCategories2</td>
   <td>Recupera tutti gli elementi figlio diretti per una categoria.</td>
  </tr>
  <tr>
   <td>getAllInitipoints</td>
   <td>ProcessManagementInitipointService</td>
   <td>getAllInitipoints</td>
   <td>Recupera tutti i punti di avvio presenti sul server in tutte le categorie.</td>
  </tr>
  <tr>
   <td>invokeStartPoint</td>
   <td>ProcessManagementInitipointService</td>
   <td>invokeStartPoint</td>
   <td>Viene richiamato un punto di inizio e viene creata una nuova attività corrispondente a un punto di partenza</td>
  </tr>
  <tr>
   <td>getAllTasks</td>
   <td>ProcessManagementTaskService</td>
   <td>getAllActionableTasks</td>
   <td>Recupera tutte le attività che vengono create e inoltrate o consultate, salvate, assegnate, assegnate e salvate per l'utente connesso.</td>
  </tr>
  <tr>
   <td>getTask</td>
   <td>ProcessManagementTaskService</td>
   <td>getTask</td>
   <td>Recupera un'attività specifica.</td>
  </tr>
  <tr>
   <td>renderTask</td>
   <td>ProcessManagementTaskService</td>
   <td>rendering</td>
   <td>Rendering di un'attività e restituzione delle informazioni necessarie per eseguire il rendering del modulo come URL del modulo, tipo di modulo, URL dati, se necessario e così via.</td>
  </tr>
  <tr>
   <td>submitWithPreData</td>
   <td>ProcessManagementTaskService</td>
   <td>submitWithPreData</td>
   <td>Restituisce il risultato dell'API submit di TaskManager utilizzando la chiave result.</td>
  </tr>
  <tr>
   <td>submitWithData</td>
   <td>ProcessManagementTaskService</td>
   <td>submitWithData</td>
   <td>Invia i dati del modulo (passati come stringa) associati all'attività utilizzando l'API submit di TaskManager. Viene utilizzato per i moduli Flex che non inviano l'API submit di callTaskManager.</td>
  </tr>
  <tr>
   <td>save</td>
   <td>ProcessManagementTaskService</td>
   <td>save</td>
   <td>Consente di salvare un'attività sul server.</td>
  </tr>
  <tr>
   <td>complete</td>
   <td>ProcessManagementTaskService</td>
   <td>complete</td>
   <td>Completa un'attività e l'attività viene passata al passaggio successivo come previsto dalla progettazione del processo.</td>
  </tr>
  <tr>
   <td>getAttachment</td>
   <td>ProcessManagementTaskService</td>
   <td>getAttachment</td>
   <td>Restituisce l'URL di un allegato in cui è disponibile l'allegato.</td>
  </tr>
  <tr>
   <td>getAllAttachments</td>
   <td>ProcessManagementTaskService</td>
   <td>getAllActionableAttachments</td>
   <td>Recupera tutti gli allegati e le note di un'attività.</td>
  </tr>
  <tr>
   <td>share</td>
   <td>ProcessManagementTaskService</td>
   <td>share</td>
   <td>Condivide un'attività con un altro utente. Un altro utente può reclamare l’attività e diventarne proprietario.</td>
  </tr>
  <tr>
   <td>inoltra</td>
   <td>ProcessManagementTaskService</td>
   <td>inoltra</td>
   <td>Invia un'attività a un altro utente.</td>
  </tr>
  <tr>
   <td>consultare</td>
   <td>ProcessManagementTaskService</td>
   <td>consultare</td>
   <td>Consulta un'attività con un altro utente.</td>
  </tr>
  <tr>
   <td>reclamo</td>
   <td>ProcessManagementTaskService</td>
   <td>reclamo</td>
   <td>Richiede un'attività disponibile nella coda condivisa.</td>
  </tr>
  <tr>
   <td>sbloccare</td>
   <td>ProcessManagementTaskService</td>
   <td>sbloccare</td>
   <td>Sblocca un'attività.</td>
  </tr>
  <tr>
   <td>lock</td>
   <td>ProcessManagementTaskService</td>
   <td>lock</td>
   <td>Blocca un'attività e non può essere richiesta da un altro utente se condivisa.</td>
  </tr>
  <tr>
   <td>rifiutare</td>
   <td>ProcessManagementTaskService</td>
   <td>rifiutare</td>
   <td>Restituisce l'attività al proprietario precedente dell'attività.</td>
  </tr>
  <tr>
   <td>abbandono</td>
   <td>ProcessManagementTaskService</td>
   <td>abbandono</td>
   <td>Elimina un'attività.</td>
  </tr>
  <tr>
   <td>setVisibility</td>
   <td>ProcessManagementTaskService</td>
   <td>setVisibility</td>
   <td>Imposta la visibilità di un’attività. Se la visibilità è impostata su false, l'attività non sarà più visibile per l'utente.</td>
  </tr>
  <tr>
   <td>getUsers</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsers</td>
   <td>Viene utilizzato per la ricerca degli utenti. Se non viene specificato alcun nome, restituisce tutti gli utenti con un nome specificato.</td>
  </tr>
  <tr>
   <td>getUsersInGroup</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsersInGroupByName</td>
   <td>Restituisce tutti gli utenti di un gruppo.</td>
  </tr>
  <tr>
   <td>GrantQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>GrantQueueAccess</td>
   <td>Consente l'accesso alla coda dell'utente connesso a un utente specificato. Si tratta sostanzialmente di condividere una propria coda con un altro utente.</td>
  </tr>
  <tr>
   <td>requestQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>requestQueueAccess</td>
   <td>Esegue la richiesta di accesso alla coda dell'utente specificato per l'utente connesso. Se l'utente approva la richiesta, la coda dell'utente viene condivisa con l'utente che ha effettuato l'accesso.</td>
  </tr>
  <tr>
   <td>getGrantedUsers</td>
   <td>ProcessManagementQueueService</td>
   <td>getGrantedUsers</td>
   <td>Restituisce tutti gli utenti che hanno accesso alla coda degli utenti connessi.</td>
  </tr>
  <tr>
   <td>getUsersForAccessibleQueues</td>
   <td>ProcessManagementQueueService</td>
   <td>getUsersForAccessibleQueues</td>
   <td>Restituisce tutti gli utenti la cui coda è accessibile a un utente.</td>
  </tr>
  <tr>
   <td>revokeQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>revokeQueueAccess</td>
   <td>Rimuove un utente dall'elenco di utenti che hanno accesso alla coda di utenti connessi.</td>
  </tr>
  <tr>
   <td>removeQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>removeQueueAccess</td>
   <td>Rimuove un utente dall'elenco di utenti la cui coda è accessibile all'utente connesso.</td>
  </tr>
  <tr>
   <td>getAllQueues<br /> </td>
   <td>ProcessManagementQueueService<br /> </td>
   <td>getAllQueues<br /> </td>
   <td>Ottiene tutte le code (code proprie, condivise e di gruppo) accessibili all'utente che ha effettuato l'accesso.<br /> </td>
  </tr>
  <tr>
   <td>getOutOfOfficeSettings</td>
   <td>ProcessManagementOutOfOfficeService</td>
   <td>getOutOfOfficeSettings</td>
   <td>Esce dalle impostazioni di ufficio di un utente.</td>
  </tr>
  <tr>
   <td>saveOutOfOfficeSettingsJson</td>
   <td>ProcessManagementOutOfOfficeService</td>
   <td>saveOutOfOfficeSettingsJson</td>
   <td>Consente di risparmiare le impostazioni di un utente fuori sede.</td>
  </tr>
  <tr>
   <td>getAllProcesses</td>
   <td>ProcessManagementProcessService</td>
   <td>getAllProcesses</td>
   <td>Restituisce un elenco di tutti i processi.</td>
  </tr>
  <tr>
   <td>getParticipatedProcesses</td>
   <td>ProcessManagementProcessService</td>
   <td>getParticipatedProcesses</td>
   <td>Restituisce l'elenco di tutti i nomi di processo partecipanti dall'utente connesso.</td>
  </tr>
  <tr>
   <td>getProcessInstance<br /> </td>
   <td>ProcessManagementProcessService<br /> </td>
   <td>getProcessInstance<br /> </td>
   <td>Recupera i dettagli di un'istanza di processo.<br /> </td>
  </tr>
  <tr>
   <td>getProcessInstances</td>
   <td>ProcessManagementQueryService</td>
   <td>getProcessInstances</td>
   <td>Recupera tutte le istanze di processo per un processo.</td>
  </tr>
  <tr>
   <td>getPendingTasksForProcessInstance</td>
   <td>ProcessManagementQueryService</td>
   <td>getPendingTasksForProcessInstance</td>
   <td>Ottiene le attività in sospeso per un'istanza di processo.</td>
  </tr>
  <tr>
   <td>getTasksForProcessInstance</td>
   <td>ProcessManagementQueryService</td>
   <td>getTasksForProcessInstance</td>
   <td>Ottiene tutte le attività per un'istanza di processo.</td>
  </tr>
  <tr>
   <td>getAllSearchTemplates</td>
   <td>ProcessManagementQueryService</td>
   <td>getAllSearchTemplates</td>
   <td>Restituisce un elenco di tutti i modelli di ricerca.</td>
  </tr>
  <tr>
   <td>getTemplate</td>
   <td>ProcessManagementQueryService</td>
   <td>getTemplate</td>
   <td>Restituisce il contenuto per un modello di ricerca.</td>
  </tr>
  <tr>
   <td>findTasksJson<br /> </td>
   <td>ProcessManagementQueryService</td>
   <td>findTasksJson</td>
   <td>Cerca e restituisce tutte le attività che soddisfano tutte le condizioni di un modello di ricerca.</td>
  </tr>
  <tr>
   <td>getAssignmentsForTask</td>
   <td>ProcessManagementTaskService</td>
   <td>getAssignmentsForTask</td>
   <td>Riceve tutte le assegnazioni per un'attività. Ad esempio :- Se l'utente inoltra o consulta un'attività con un altro utente, si tratta di un'assegnazione per un'attività.</td>
  </tr>
  <tr>
   <td>deleteAttachment </td>
   <td>TaskManagerService</td>
   <td>deleteAttachment</td>
   <td>Consente di eliminare un allegato.</td>
  </tr>
  <tr>
   <td>initialize</td>
   <td>ProcessManagementClientSessionService</td>
   <td>initialize</td>
   <td>Rinnova asserzione se necessario. Esegue l'autenticazione dell'utente. Imposta i parametri di sessione per le informazioni server/client. Restituisce le informazioni utente e l’intervallo di polling.</td>
  </tr>
  <tr>
   <td>getTasksForDirectReports</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getTasksForDirectReports</td>
   <td>Restituisce tutte le attività dei rapporti diretti del gestore di accesso.</td>
  </tr>
  <tr>
   <td>getTaskOfDirectReport<br /> </td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getDirectReportTask</td>
   <td>Restituisce l'attività del report diretto specificato del gestore di accesso.</td>
  </tr>
  <tr>
   <td>forwardTaskOfDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>forwardTaskOfDirectReport</td>
   <td>Invia a un altro utente un’attività di rapporto diretto.</td>
  </tr>
  <tr>
   <td>rifiutareTaskOfDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>rifiutareTaskOfDirectReport</td>
   <td>Restituisce un'attività di un rapporto diretto all'utente precedente.</td>
  </tr>
  <tr>
   <td>getProperty</td>
   <td>WorkspacePropertyService</td>
   <td>getProperty</td>
   <td>Ottiene una proprietà Workspace per un utente.</td>
  </tr>
  <tr>
   <td>removeProperty</td>
   <td>WorkspacePropertyService</td>
   <td>delete</td>
   <td>Rimuove una proprietà Workspace per un utente.</td>
  </tr>
  <tr>
   <td>getProperties</td>
   <td>WorkspacePropertyService</td>
   <td>getPropertiesAsMap</td>
   <td>Restituisce tutte le proprietà Workspace di un utente.</td>
  </tr>
  <tr>
   <td>setProperty</td>
   <td>WorkspacePropertyService</td>
   <td>setProperty</td>
   <td>Imposta una proprietà Workspace per un utente.</td>
  </tr>
  <tr>
   <td>getCurrentUserImageUrl</td>
   <td>ProcessManagementClientSessionService</td>
   <td>getCurrentUserImageUrl</td>
   <td>Ottiene l'URL dell'immagine dell'utente per l'utente che ha effettuato l'accesso.</td>
  </tr>
  <tr>
   <td>getUserImageUrl</td>
   <td>ProcessManagementClientSessionService</td>
   <td>getUserImageUrl</td>
   <td>Ottiene l'URL dell'immagine dell'utente per l'utente specificato.</td>
  </tr>
  <tr>
   <td>uploadNote</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>uploadNote</td>
   <td>Carica una nota sul server per un’attività.</td>
  </tr>
  <tr>
   <td>uploadRMAToServer (viene chiamato anche direttamente dal modello html)<br /> </td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>uploadAttachment</td>
   <td>Carica un allegato sul server per un'attività.</td>
  </tr>
  <tr>
   <td>getImageURL (viene chiamato anche direttamente dal modello html)</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>getImage</td>
   <td>Riceve immagini per un processo.</td>
  </tr>
 </tbody>
</table>
