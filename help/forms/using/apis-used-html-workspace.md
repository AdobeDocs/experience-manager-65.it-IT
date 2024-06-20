---
title: API utilizzate nell’area di lavoro di AEM Forms
description: Java&trade pubblico; API JavaScript e metodi di LiveCycle AEM Forms Workspace, esposti per la personalizzazione e l’automazione.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 9034f73a-83f3-498e-b6a6-ad6577aa1a3a
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms, Adaptive Forms
role: Admin, User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 1%

---

# API utilizzate nell’area di lavoro di AEM Forms {#apis-used-in-aem-forms-workspace}

Le seguenti API vengono utilizzate nell’area di lavoro di AEM Forms.

<table>
 <tbody>
  <tr>
   <td><strong>Metodo JavaScript</strong></td>
   <td><strong>Nome servizio</strong></td>
   <td><strong>Nome API</strong></td>
   <td><strong>Commenti</strong></td>
  </tr>
  <tr>
   <td>getGroups</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getGroups</td>
   <td>Cerca nei gruppi. restituisce un elenco di tutti i gruppi se non viene specificato nulla, altrimenti restituisce gruppi con il nome specificato.</td>
  </tr>
  <tr>
   <td>getUsersAndGroups</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsersAndGroups</td>
   <td>Cerca utenti e gruppi. Restituisce un elenco di tutti gli utenti e i gruppi se non viene specificato nulla, altrimenti restituisce gli utenti e i gruppi con il nome specificato.</td>
  </tr>
  <tr>
   <td>prepareForSubmit</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>prepareForSubmit</td>
   <td>Viene richiamato prima dell’invio di un modulo tramite DocumentSubmitServlet. Imposta l’ID attività in una variabile di sessione (insieme all’ora di scadenza) che viene recuperata durante l’invio effettivo.</td>
  </tr>
  <tr>
   <td>submitTask</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>invia</td>
   <td>Invia l’oggetto documento associato a un’attività (e il processo di invio a sua volta).</td>
  </tr>
  <tr>
   <td>getRootEndpointCategories</td>
   <td>ProcessManagementStartpointService</td>
   <td>getRootEndpointCategories</td>
   <td>Recupera tutte le categorie principali presenti sul server.</td>
  </tr>
  <tr>
   <td>getDirectChildCategories</td>
   <td>ProcessManagementStartpointService</td>
   <td>getDirectChildCategories2</td>
   <td>Recupera tutti i figli diretti per una categoria.</td>
  </tr>
  <tr>
   <td>getAllStartpoints</td>
   <td>ProcessManagementStartpointService</td>
   <td>getAllStartpoints</td>
   <td>Recupera tutti i punti iniziali presenti sul server in tutte le categorie.</td>
  </tr>
  <tr>
   <td>invokeStartpoint</td>
   <td>ProcessManagementStartpointService</td>
   <td>invokeStartpoint</td>
   <td>Viene richiamato un punto d'inizio e viene creata un'attività corrispondente a un punto d'inizio</td>
  </tr>
  <tr>
   <td>getAllTasks</td>
   <td>ServizioAttivitàGestioneProcessi</td>
   <td>getAllActionableTasks</td>
   <td>Recupera tutte le attività create e inoltrate o consultate, salvate, assegnate, assegnate e salvate per l’utente connesso.</td>
  </tr>
  <tr>
   <td>getTask</td>
   <td>ServizioAttivitàGestioneProcessi</td>
   <td>getTask</td>
   <td>Recupera un’attività specifica.</td>
  </tr>
  <tr>
   <td>renderTask</td>
   <td>ServizioAttivitàGestioneProcessi</td>
   <td>rendering</td>
   <td>Se necessario, restituisce un’attività e le informazioni necessarie per eseguire il rendering del modulo come URL del modulo, tipo di modulo, URL di dati.</td>
  </tr>
  <tr>
   <td>submitWithPriorData</td>
   <td>ServizioAttivitàGestioneProcessi</td>
   <td>submitWithPriorData</td>
   <td>Restituisce il risultato dell'API di invio di TaskManager utilizzando la chiave di risultato.</td>
  </tr>
  <tr>
   <td>submitWithData</td>
   <td>ServizioAttivitàGestioneProcessi</td>
   <td>submitWithData</td>
   <td>Invia i dati del modulo (passati come stringa) associati all’attività utilizzando l’API submit di TaskManager. Viene utilizzato per i Flex Form che non chiamano l’API di invio di TaskManager.</td>
  </tr>
  <tr>
   <td>salva</td>
   <td>ServizioAttivitàGestioneProcessi</td>
   <td>salva</td>
   <td>Consente di salvare un'attività sul server.</td>
  </tr>
  <tr>
   <td>completo</td>
   <td>ServizioAttivitàGestioneProcessi</td>
   <td>completo</td>
   <td>L'attività viene completata e passata al passaggio successivo in base alla progettazione del processo.</td>
  </tr>
  <tr>
   <td>getAttachment</td>
   <td>ServizioAttivitàGestioneProcessi</td>
   <td>getAttachment</td>
   <td>Restituisce l’URL di un allegato in cui l’allegato è disponibile.</td>
  </tr>
  <tr>
   <td>getAllAttachments</td>
   <td>ServizioAttivitàGestioneProcessi</td>
   <td>getAllActionableAttachments</td>
   <td>Recupera tutti gli allegati e le note di un’attività.</td>
  </tr>
  <tr>
   <td>condividere</td>
   <td>ServizioAttivitàGestioneProcessi</td>
   <td>condividere</td>
   <td>Condivide un’attività con un altro utente. Un altro utente può richiedere l’attività e diventarne il proprietario.</td>
  </tr>
  <tr>
   <td>inoltra</td>
   <td>ServizioAttivitàGestioneProcessi</td>
   <td>inoltra</td>
   <td>Inoltra un’attività a un altro utente.</td>
  </tr>
  <tr>
   <td>consulta</td>
   <td>ServizioAttivitàGestioneProcessi</td>
   <td>consulta</td>
   <td>Consulta un’attività con un altro utente.</td>
  </tr>
  <tr>
   <td>reclamo</td>
   <td>ServizioAttivitàGestioneProcessi</td>
   <td>reclamo</td>
   <td>Richiede un'operazione disponibile in una coda condivisa.</td>
  </tr>
  <tr>
   <td>sblocca</td>
   <td>ServizioAttivitàGestioneProcessi</td>
   <td>sblocca</td>
   <td>Sblocca un’attività.</td>
  </tr>
  <tr>
   <td>blocca</td>
   <td>ServizioAttivitàGestioneProcessi</td>
   <td>blocca</td>
   <td>Blocca un’attività e l’attività non può essere rivendicata da un altro utente se condivisa.</td>
  </tr>
  <tr>
   <td>rifiuta</td>
   <td>ServizioAttivitàGestioneProcessi</td>
   <td>rifiuta</td>
   <td>Restituisce un'attività al proprietario precedente dell'attività.</td>
  </tr>
  <tr>
   <td>abbandonare</td>
   <td>ServizioAttivitàGestioneProcessi</td>
   <td>abbandonare</td>
   <td>Elimina un'attività.</td>
  </tr>
  <tr>
   <td>setVisibility</td>
   <td>ServizioAttivitàGestioneProcessi</td>
   <td>setVisibility</td>
   <td>Imposta la visibilità di un'attività. Se la visibilità è impostata su false, l’attività non sarà più visibile all’utente.</td>
  </tr>
  <tr>
   <td>getUsers</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsers</td>
   <td>Viene utilizzato per la ricerca degli utenti. Restituisce tutti gli utenti se non viene specificato alcun nome oppure restituisce gli utenti con un nome specificato.</td>
  </tr>
  <tr>
   <td>getUsersInGroup</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsersInGroupByName</td>
   <td>Restituisce tutti gli utenti di un gruppo.</td>
  </tr>
  <tr>
   <td>grantQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>grantQueueAccess</td>
   <td>Consente l'accesso della coda dell'utente connesso a un utente specificato. In pratica stai condividendo la tua coda con un altro utente.</td>
  </tr>
  <tr>
   <td>requestQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>requestQueueAccess</td>
   <td>Effettua la richiesta di accesso di una coda di un utente specificato per l’utente connesso. Se l’utente approva la richiesta, la coda dell’utente viene condivisa con l’utente connesso.</td>
  </tr>
  <tr>
   <td>getGrantedUsers</td>
   <td>ProcessManagementQueueService</td>
   <td>getGrantedUsers</td>
   <td>Restituisce tutti gli utenti che hanno accesso alla coda dell'utente connesso.</td>
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
   <td>Rimuove un utente dall’elenco degli utenti che hanno accesso alla coda dell’utente connesso.</td>
  </tr>
  <tr>
   <td>removeQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>removeQueueAccess</td>
   <td>Rimuove un utente dall’elenco degli utenti la cui coda è accessibile all’utente connesso.</td>
  </tr>
  <tr>
   <td>getAllQueues<br /> </td>
   <td>ProcessManagementQueueService<br /> </td>
   <td>getAllQueues<br /> </td>
   <td>Ottiene tutte le code (proprie, condivise e di gruppo) accessibili all'utente connesso.<br /> </td>
  </tr>
  <tr>
   <td>getOutOfOfficeSettings</td>
   <td>ProcessManagementOutOfOfficeService</td>
   <td>getOutOfOfficeSettings</td>
   <td>Ottiene le impostazioni fuori sede di un utente.</td>
  </tr>
  <tr>
   <td>saveOutOfOfficeSettingsJson</td>
   <td>ProcessManagementOutOfOfficeService</td>
   <td>saveOutOfOfficeSettingsJson</td>
   <td>Consente di salvare le impostazioni fuori sede di un utente.</td>
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
   <td>Restituisce un elenco di tutti i nomi di processo a cui partecipa l'utente connesso.</td>
  </tr>
  <tr>
   <td>getProcessInstance<br /> </td>
   <td>ProcessManagementProcessService<br /> </td>
   <td>getProcessInstance<br /> </td>
   <td>Recupera i dettagli di un’istanza del processo.<br /> </td>
  </tr>
  <tr>
   <td>getProcessInstances</td>
   <td>ProcessManagementQueryService</td>
   <td>getProcessInstances</td>
   <td>Recupera tutte le istanze del processo.</td>
  </tr>
  <tr>
   <td>getPendingTasksForProcessInstance</td>
   <td>ProcessManagementQueryService</td>
   <td>getPendingTasksForProcessInstance</td>
   <td>Ottiene le attività in sospeso per un'istanza del processo.</td>
  </tr>
  <tr>
   <td>getTasksForProcessInstance</td>
   <td>ProcessManagementQueryService</td>
   <td>getTasksForProcessInstance</td>
   <td>Ottiene tutte le attività per un’istanza del processo.</td>
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
   <td>ServizioAttivitàGestioneProcessi</td>
   <td>getAssignmentsForTask</td>
   <td>Ottiene tutte le assegnazioni per un'attività. Ad esempio, se un utente inoltra o consulta un’attività con un altro utente, si tratta di un’assegnazione per un’attività.</td>
  </tr>
  <tr>
   <td>deleteAttachment </td>
   <td>ServizioGestioneAttività</td>
   <td>deleteAttachment</td>
   <td>Elimina un allegato.</td>
  </tr>
  <tr>
   <td>inizializzare</td>
   <td>ProcessManagementClientSessionService</td>
   <td>inizializzare</td>
   <td>Se necessario, rinnova l’asserzione. Autentica l’utente. Imposta i parametri di sessione per le informazioni su server/client. Restituisce informazioni utente e intervallo di polling.</td>
  </tr>
  <tr>
   <td>getTasksForDirectReports</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getTasksForDirectReports</td>
   <td>Restituisce tutte le attività dei referenti diretti del manager connesso.</td>
  </tr>
  <tr>
   <td>getTaskOfDirectReport<br /> </td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getDirectReportTask</td>
   <td>Restituisce un'attività di un referente diretto specificato del manager connesso.</td>
  </tr>
  <tr>
   <td>forwardTaskOfDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>forwardTaskOfDirectReport</td>
   <td>Inoltra un’attività di referente diretto a un altro utente.</td>
  </tr>
  <tr>
   <td>rejectedTaskOfDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>rejectedTaskOfDirectReport</td>
   <td>Restituisce un’attività di un referente diretto all’utente precedente.</td>
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
   <td>elimina</td>
   <td>Rimuove una proprietà Workspace per un utente.</td>
  </tr>
  <tr>
   <td>getProperties</td>
   <td>WorkspacePropertyService</td>
   <td>getPropertiesAsMap</td>
   <td>Restituisce tutte le proprietà di Workspace di un utente.</td>
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
   <td>Ottiene l’URL dell’immagine dell’utente connesso.</td>
  </tr>
  <tr>
   <td>getUserImageUrl</td>
   <td>ProcessManagementClientSessionService</td>
   <td>getUserImageUrl</td>
   <td>Ottiene l’URL dell’immagine dell’utente per l’utente specificato.</td>
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
   <td>Carica un allegato sul server per un’attività.</td>
  </tr>
  <tr>
   <td>getImageURL (chiamato anche direttamente dal modello HTML)</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>getImage</td>
   <td>Ottiene l’immagine per un processo.</td>
  </tr>
 </tbody>
</table>
