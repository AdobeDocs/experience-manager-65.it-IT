---
title: Descrizione oggetto JSON dell'area di lavoro di AEM Forms
seo-title: Descrizione oggetto JSON dell'area di lavoro di AEM Forms
description: Informazioni concettuali sugli oggetti JavaScript JSON utilizzati nell'area di lavoro di LiveCycle  AEM Forms per la personalizzazione, l'estensione, la modifica e il riutilizzo.
seo-description: Informazioni concettuali sugli oggetti JavaScript JSON utilizzati nell'area di lavoro di LiveCycle  AEM Forms per la personalizzazione, l'estensione, la modifica e il riutilizzo.
uuid: 91c923c8-144a-4453-ba91-6a5193f1c4c4
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 61b7246d-ed28-4470-a0a2-a4aaf1a061a4
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '2134'
ht-degree: 9%

---


#  descrizione dell&#39;oggetto JSON dell&#39;area di lavoro AEM Forms {#aem-forms-workspace-json-object-description}

Gli oggetti JSON utilizzati &#39;area di lavoro di AEM Forms sono descritti di seguito.

1. Categoria

   Le categorie sono presenti nella scheda del processo iniziale dell&#39;area di lavoro. Queste categorie vengono utilizzate per classificare i punti di avvio.

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Solo client</strong></td>
   <td><strong>Commenti</strong></td>
  </tr>
  <tr>
   <td>name</td>
   <td>F</td>
   <td>Nome categoria</td>
  </tr>
  <tr>
   <td>id</td>
   <td>F</td>
   <td>ID categoria<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>descrizione<br type="_moz" /> </td>
   <td>F</td>
   <td>Descrizione categoria<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>parentOid<br type="_moz" /> </td>
   <td>F</td>
   <td>Contiene un ID della categoria padre<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>startPointsList<br type="_moz" /> </td>
   <td>T</td>
   <td>Contiene l'elenco di tutti i punti di avvio presenti in una categoria</td>
  </tr>
  <tr>
   <td>categoryList</td>
   <td>T</td>
   <td>Contiene l'elenco delle categorie figlio dirette di una categoria<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Tutti i punti di partenza e i preferiti sono categorie definite sul lato client. La categoria Preferiti contiene tutti i punti di inizio contrassegnati dall&#39;utente come preferiti. La categoria Punti di partenza contiene tutti i punti di partenza.

1. Punto di partenza

   Il punto di partenza viene utilizzato per avviare un processo dall’area di lavoro quando viene richiamato.

   | **Proprietà** | **Solo client** | **Commenti** |
   |---|---|---|
   | categoryId | F | Contiene l&#39;ID della categoria a cui il punto di avvio appartiene. |
   | descrizione | F | Contiene la descrizione di un punto iniziale. |
   | name | F | Contiene il nome del punto di partenza. |
   | serializedImageTicket | F | Contiene un biglietto immagine corrispondente al punto di partenza. Questo ticket immagine viene utilizzato nel campo imageUrl di startpoint, per ottenere l&#39;immagine per startpoint dal server. |
   | serviceName | F | Contiene il nome del servizio per startpoint. |
   | startpointId | F | Contiene id of startpoint. |
   | isFavorite | T | Indica se il punto di avvio è il preferito o meno. True se startpoint è il preferito altrimenti false. |
   | isDefaultImage | T | Indica se esiste un&#39;immagine specificata per il processo o meno. True se non è associata alcuna immagine a process else false. |
   | task | T | Contiene l&#39;attività creata quando viene richiamato il punto di avvio. |
   | imageUrl | T | Contiene l’url dell’immagine corrispondente al punto di avvio. |

1. Attività

   Le attività vengono assegnate a utenti/gruppi e includono un&#39;interfaccia utente, un modulo o una Guida (obsoleta), che può essere compilata con i dati. Quando gli utenti ricevono un’attività, vengono forniti il modulo o la Guida da compilare e inviare.

<table>
 <tbody>
  <tr>
   <td>Proprietà<br /> </td>
   <td>Solo client<br /> </td>
   <td>Commenti<br /> </td>
  </tr>
  <tr>
   <td>classOfTask</td>
   <td>F</td>
   <td>La classe di attività è 'LC8' quando l'attività è lc8 task else 'Standard'.<br /> </td>
  </tr>
  <tr>
   <td>completeTime<br /> </td>
   <td>F</td>
   <td>Contiene la marca temporale al termine dell'attività.<br /> </td>
  </tr>
  <tr>
   <td>consultareGroupId<br /> </td>
   <td>F</td>
   <td>Contiene l'ID di un gruppo al quale è possibile consultare l'attività. È impostato durante la progettazione del processo.<br /> </td>
  </tr>
  <tr>
   <td>createTime<br /> </td>
   <td>F</td>
   <td>Contiene la marca temporale alla creazione dell'attività.<br /> </td>
  </tr>
  <tr>
   <td>creatingId<br /> </td>
   <td>F</td>
   <td>Contiene l'ID dell'utente che ha creato l'attività.<br /> </td>
  </tr>
  <tr>
   <td>currentAssignment<br /> </td>
   <td>F</td>
   <td>Contiene dettagli sull'assegnazione corrente dell'attività.<br /> </td>
  </tr>
  <tr>
   <td>scadenza<br /> </td>
   <td>F</td>
   <td>Contiene la marca temporale in cui un'attività raggiungerà la scadenza.<br /> </td>
  </tr>
  <tr>
   <td>descrizione<br /> </td>
   <td>F</td>
   <td>Contiene la descrizione dell'attività.<br /> </td>
  </tr>
  <tr>
   <td>displayName<br /> </td>
   <td>F</td>
   <td>Contiene il nome visualizzato dell'attività.<br /> </td>
  </tr>
  <tr>
   <td>forwardGroupId<br /> </td>
   <td>F</td>
   <td>Contiene l’ID di un gruppo al quale è possibile inoltrare l’attività. È impostato durante la progettazione del processo.<br /> </td>
  </tr>
  <tr>
   <td>istruzioni<br /> </td>
   <td>F</td>
   <td>Contiene istruzioni per un'attività.<br /> </td>
  </tr>
  <tr>
   <td>isLocked<br /> </td>
   <td>F</td>
   <td>True se l'attività è bloccata.<br /> </td>
  </tr>
  <tr>
   <td>isMustOpenToComplete<br /> </td>
   <td>F</td>
   <td>True se è necessario aprire il modulo attività per completare l'attività.<br /> </td>
  </tr>
  <tr>
   <td>isOpenFullScreen<br /> </td>
   <td>F</td>
   <td>Se true, all'apertura dell'attività il modulo viene visualizzato per la prima volta.<br /> </td>
  </tr>
  <tr>
   <td>isRouteSelectionRequired<br /> </td>
   <td>F</td>
   <td>Se true, è necessario selezionare la route per completare l'attività.<br /> </td>
  </tr>
  <tr>
   <td>isShowAttachments<br /> </td>
   <td>F</td>
   <td>Gli allegati sono visualizzati se è vero.<br /> </td>
  </tr>
  <tr>
   <td>isStartTask<br /> </td>
   <td>F</td>
   <td>Se true, l'attività viene creata dal punto iniziale.<br /> </td>
  </tr>
  <tr>
   <td>isVisible<br /> </td>
   <td>F</td>
   <td>True se l'attività è visibile nell'area di lavoro.<br /> </td>
  </tr>
  <tr>
   <td>nextPromemoria<br /> </td>
   <td>F</td>
   <td>Timestamp per il promemoria successivo.<br /> </td>
  </tr>
  <tr>
   <td>priority<br /> </td>
   <td>F</td>
   <td>Contiene la priorità dell'attività.<br /> 1 = Priorità<br /> 2 più alta = Priorità<br /> 3 alta = Priorità<br />  normale 4 = Priorità<br /> 5 bassa = Prioritàpiù bassa<br /> </td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>F</td>
   <td>ID dell'istanza di processo di cui fa parte l'attività.<br /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br /> </td>
   <td>F</td>
   <td>Stato dell'istanza di processo dell'attività.<br /> </td>
  </tr>
  <tr>
   <td>promemoriaCount<br /> </td>
   <td>F</td>
   <td>Contiene il conteggio dei promemoria per l'attività.<br /> </td>
  </tr>
  <tr>
   <td>routeList<br /> </td>
   <td>F</td>
   <td>Contiene l'elenco di route associati all'attività. L'utente può completare l'attività selezionando una qualsiasi delle route dall'elenco di route.<br /> </td>
  </tr>
  <tr>
   <td>selectedRoute<br /> </td>
   <td>F</td>
   <td>Contiene il nome della route selezionata al completamento dell'attività.<br /> </td>
  </tr>
  <tr>
   <td>serializedImageTicket<br /> </td>
   <td>F</td>
   <td>Contiene un ticket immagine corrispondente all'attività. Questo ticket immagine viene utilizzato nel campo imageUrl dell'attività, per ottenere l'immagine per l'attività dal server.<br /> <br /> </td>
  </tr>
  <tr>
   <td>serviceName<br /> </td>
   <td>F</td>
   <td>Contiene il nome del servizio per l'attività.<br /> </td>
  </tr>
  <tr>
   <td>serviceTitle<br /> </td>
   <td>F</td>
   <td>Contiene il titolo del servizio per l'attività.<br /> </td>
  </tr>
  <tr>
   <td>stato<br /> </td>
   <td>F</td>
   <td>1 = Creato (l'attività viene creata dal punto iniziale).<br /> 2 = Creato e salvato (l'attività viene creata dal punto iniziale e salvata).<br /> 3 = Assegnato (l'attività viene assegnata all'utente dopo l'avvio del processo).<br /> 4 = Assegnato e Salvato (l'attività viene assegnata e salvata).<br /> 100 = Completato (l'attività è completata).<br /> 101 = Terminato (l'attività ha raggiunto la scadenza).<br /> 102 = Terminato<br /> </td>
  </tr>
  <tr>
   <td>stepName<br /> </td>
   <td>F</td>
   <td>Contiene il nome del set di attività durante la progettazione del processo.<br /> </td>
  </tr>
  <tr>
   <td>summaryUrl<br /> </td>
   <td>F</td>
   <td>Contiene l'URL di riepilogo attività.<br /> </td>
  </tr>
  <tr>
   <td>taskACL<br /> </td>
   <td>F</td>
   <td>È l'elenco di controllo di accesso per un'attività.<br /> </td>
  </tr>
  <tr>
   <td>taskId<br /> </td>
   <td>F</td>
   <td>ID di un'attività.<br /> </td>
  </tr>
  <tr>
   <td>updateTime<br /> </td>
   <td>F</td>
   <td>Timestamp dell'ultimo aggiornamento dell'attività.<br /> </td>
  </tr>
  <tr>
   <td>formUrl<br /> </td>
   <td>T</td>
   <td>Contiene l'URL del modulo per un'attività.<br /> </td>
  </tr>
  <tr>
   <td>taskFormType<br /> </td>
   <td>T</td>
   <td>Contiene il tipo di modulo attività. Utilizzando questo campo, il rendering dell'attività viene eseguito sul client come pdf per, modulo SWF e così via.<br /> </td>
  </tr>
  <tr>
   <td>showDirectActions<br /> </td>
   <td>T</td>
   <td>Se true, le azioni di route sono visibili nell'area di lavoro.<br /> </td>
  </tr>
  <tr>
   <td>showACLActions<br /> </td>
   <td>T</td>
   <td>Se true, azioni quali forward, consultare, condividere sono visibili nell'area di lavoro.<br /> </td>
  </tr>
  <tr>
   <td>supportedOffline<br /> </td>
   <td>T</td>
   <td>Se true, il modulo può essere portato offline. Solo per i moduli PDF.<br /> </td>
  </tr>
  <tr>
   <td>supportedSave<br /> </td>
   <td>T</td>
   <td>Se true, l'utente può salvare l'attività.<br /> </td>
  </tr>
  <tr>
   <td>readerSubmitOptions<br /> </td>
   <td>T</td>
   <td>Questo oggetto contiene opzioni che vengono utilizzate per inviare moduli PDF tramite lettore nel caso in cui il modulo pdf non contenga alcun pulsante di invio.<br /> </td>
  </tr>
  <tr>
   <td>isDefaultImage<br /> </td>
   <td>T</td>
   <td>Indica se esiste un'immagine specificata per il processo o meno. True se non esiste un'immagine associata a process else false.<br /> </td>
  </tr>
  <tr>
   <td>historyTaskList<br /> </td>
   <td>T</td>
   <td>Contiene l'elenco delle attività utilizzate nella scheda Cronologia dei dettagli delle attività.<br /> </td>
  </tr>
  <tr>
   <td>isOwner<br /> </td>
   <td>T</td>
   <td>True se l'utente connesso è proprietario dell'attività.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands<br /> </td>
   <td>T</td>
   <td>Contiene tutte le azioni che è possibile eseguire sull'attività.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.directCommands<br /> </td>
   <td>T</td>
   <td>Contiene tutte le azioni di route disponibili per un'attività.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.taskACLCommands<br /> </td>
   <td>T</td>
   <td>Contiene comandi come avanti, condivisione e consulta se disponibili per un'attività.<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.otherCommands<br /> </td>
   <td>T</td>
   <td>Contiene comandi quali blocco, sblocco, abbandono, restituzione, attestazione e così via, come disponibili.<br /> </td>
  </tr>
  <tr>
   <td>processInstanceInfo<br /> </td>
   <td>T</td>
   <td>Contiene informazioni sull'istanza di processo dell'attività.<br /> </td>
  </tr>
  <tr>
   <td>processVariables<br /> </td>
   <td>T<br /> </td>
   <td>Contiene un array di oggetti di variabili di processo, se presenti.<br /> </td>
  </tr>
  <tr>
   <td>pendingTasks<br /> </td>
   <td>T</td>
   <td>Contiene l'elenco delle attività in sospeso per l'istanza di processo dell'attività.<br /> </td>
  </tr>
  <tr>
   <td>userActions<br /> </td>
   <td>T</td>
   <td>È una matrice di oggetti. Ogni oggetto contiene dettagli sulla route e il messaggio di conferma corrispondente, se presente.<br /> </td>
  </tr>
  <tr>
   <td>dataUrl<br /> </td>
   <td>T</td>
   <td>È url per i dati del modulo di un'attività.<br /> </td>
  </tr>
  <tr>
   <td>externalAppConfig<br /> </td>
   <td>T</td>
   <td>Configurazione per i moduli di applicazione di terze parti.<br /> </td>
  </tr>
  <tr>
   <td>submit<br /> </td>
   <td>T</td>
   <td>True se l'attività viene inviata.<br /> </td>
  </tr>
  <tr>
   <td>attachments<br /> </td>
   <td>T</td>
   <td>Elenco degli allegati per un'attività.<br /> </td>
  </tr>
  <tr>
   <td>assegnazioni<br /> </td>
   <td>T</td>
   <td>Elenco delle assegnazioni di un'attività.<br /> </td>
  </tr>
 </tbody>
</table>

1. Filtro

   Il filtro è sostanzialmente una coda di utente o gruppo. Quando un&#39;attività viene assegnata a un utente/gruppo, l&#39;attività viene aggiunta nella coda corrispondente.

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Solo client</strong></td>
   <td><strong>Commenti</strong></td>
  </tr>
  <tr>
   <td>isDefault <br type="_moz" /> </td>
   <td>F</td>
   <td>True se la coda è la coda predefinita dell'utente connesso, altrimenti false.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>name<br type="_moz" /> </td>
   <td>F</td>
   <td>Nome del proprietario della coda.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>qid</td>
   <td>F</td>
   <td>ID della coda.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>tipo</td>
   <td>F</td>
   <td>Contiene il tipo di coda.<br /> 0 - Coda utente.<br /> 1. Coda condivisa.<br /> 2. Coda gruppo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>query</td>
   <td>T</td>
   <td>Contiene query associate a un filtro. Questa query viene utilizzata per cercare attività dall'elenco di task completo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>task</td>
   <td>T</td>
   <td>Contiene l'elenco di tutte le attività appartenenti a un filtro.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Fuori sede

   È possibile gestire la pianificazione fuori sede e controllare il flusso delle attività assegnate in assenza.

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong><br type="_moz" /> </td>
   <td><strong>Solo client</strong><br type="_moz" /> </td>
   <td><strong>Commenti</strong><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>dateRanges<br type="_moz" /> </td>
   <td>F</td>
   <td>Contiene oggetti array di pianificazioni fuori sede di un utente. In ciascun oggetto di pianificazione, il campo startDate contiene la data di inizio della pianificazione e il campo endDate contiene la data di fine della programmazione. Se endDate è null nella pianificazione, significa che l'utente non ha pianificato la data di fine della pianificazione fuori ufficio.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isNoPrimaryDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>True se non è presente un predefinito principale nel caso in cui l'utente sia fuori ufficio.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>F</td>
   <td>True se l'utente è fuori ufficio.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>Contiene i dettagli dell'utente assegnato come designato principale dall'utente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processSpecificDesignates<br type="_moz" /> </td>
   <td>F</td>
   <td>Contiene un array di oggetti per la definizione fuori sede specifica per il processo. In ciascun oggetto designato specifico per il processo, processName contiene il nome del processo, isNotDesignated è true se nessun utente è assegnato per il processo corrispondente, e userDesignated è null se nessun utente ha assegnato altri dettagli dell'utente assegnato per il processo corrispondente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>process<br type="_moz" /> </td>
   <td>T</td>
   <td>Contiene un elenco di tutti i processi disponibili per l'utente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initialOutOfOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>Contiene le impostazioni iniziali dell'utente fuori ufficio recuperate inizialmente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>Contiene impostazioni esterne all'ufficio modificate.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userSearchHistory<br type="_moz" /> </td>
   <td>T</td>
   <td>Contiene un elenco di utenti per i quali l'utente ha effettuato l'accesso fino alla data.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Istanza di processo

   Un&#39;istanza di processo viene creata quando un processo viene richiamato tramite un&#39;area di lavoro o un workbench.

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Solo client</strong></td>
   <td><strong>Commenti</strong></td>
  </tr>
  <tr>
   <td>descrizione<br type="_moz" /> </td>
   <td>F</td>
   <td>Descrizione dell'istanza di processo<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>iniziatore</td>
   <td>F</td>
   <td>Nome dell'iniziatore di un'istanza di processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>iniziatorId</td>
   <td>F</td>
   <td>ID dell'iniziatore dell'istanza di processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processCompleteTime<br type="_moz" /> </td>
   <td>F</td>
   <td>Timestamp al termine del processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceId<br type="_moz" /> </td>
   <td>F</td>
   <td>ID dell'istanza di processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br type="_moz" /> </td>
   <td>F</td>
   <td>0 = Iniziato<br /> 1 = In esecuzione<br /> 2 = Completato<br /> 3 = Completato<br /> 4 = Terminato<br /> 5 = Terminante<br /> 6 = Sospeso<br /> 7 = Sospeso<br /> 8 = Non sospeso<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nome del processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processStartTime<br type="_moz" /> </td>
   <td>F</td>
   <td>Timestamp all'avvio del processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processVariables<br type="_moz" /> </td>
   <td>F</td>
   <td>Array di oggetti di variabili di processo. Ogni oggetto variabile di processo contiene il nome che è il nome della variabile di processo, il valore che è il valore della variabile di processo e il tipo che è il tipo di variabile di processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>elenco attività<br type="_moz" /> </td>
   <td>T</td>
   <td>Attività generate da questa istanza di processo.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Nome processo

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Solo client</strong></td>
   <td><strong>Commenti</strong></td>
  </tr>
  <tr>
   <td>processMajorVersion<br type="_moz" /> </td>
   <td>F</td>
   <td>Versione principale di un processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processMinorVersion<br type="_moz" /> </td>
   <td>F</td>
   <td>Versione secondaria di un processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nome del processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processTitle<br type="_moz" /> </td>
   <td>F</td>
   <td>Titolo del processo.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceList<br type="_moz" /> </td>
   <td>T</td>
   <td>Elenco di istanze del processo per questo processo.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Oggetto assegnazione attività

   L&#39;oggetto assegnazione attività contiene informazioni sull&#39;assegnazione dell&#39;attività. Di seguito sono riportate le proprietà dell&#39;assegnazione dell&#39;attività.

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Solo client</strong></td>
   <td><strong>Commenti</strong></td>
  </tr>
  <tr>
   <td>assignCreateTime<br type="_moz" /> </td>
   <td>F</td>
   <td>Timestamp della creazione dell'assegnazione di un'attività.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignType<br type="_moz" /> </td>
   <td>F</td>
   <td>0 = Assegnazione iniziale<br /> 1 = Inoltro (l'attività è stata inoltrata al proprietario corrente dell'attività).<br /> 2 = Restituito (l'attività è stata restituita al proprietario corrente dell'attività dal proprietario precedente dell'attività.)<br /> 3 = Richiesto (l'attività è stata reclamata dal proprietario corrente dell'attività).<br /> 4 = Inoltro (l'attività è stata assegnata al proprietario corrente dell'attività dopo l'inoltro.)<br /> 5 = Amministratore assegnato (l'attività è stata assegnata dall'amministratore al proprietario corrente dell'attività.)<br /> 6 = Consultato (l'attività è stata consultata al proprietario corrente dell'attività).<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignUpdateTime<br type="_moz" /> </td>
   <td>F</td>
   <td>Timestamp dell'aggiornamento dell'assegnazione di un'attività.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueId<br type="_moz" /> </td>
   <td>F</td>
   <td>ID della coda del proprietario corrente dell'attività.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwner<br type="_moz" /> </td>
   <td>F</td>
   <td>Nome del proprietario corrente dell'attività.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwnerId<br type="_moz" /> </td>
   <td>F</td>
   <td>ID del proprietario corrente dell'attività.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Oggetto ACL attività

   L&#39;oggetto ACL dell&#39;attività contiene informazioni sulle autorizzazioni come inoltro, condivisione, consultazione ecc. di un&#39;attività. Di seguito sono riportate le proprietà dell&#39;ACL dell&#39;attività.

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Solo client</strong></td>
   <td><strong>Commenti</strong></td>
  </tr>
  <tr>
   <td>canAddAttachments<br type="_moz" /> </td>
   <td>F</td>
   <td>Se true, gli allegati possono essere aggiunti all'attività.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canAddNotes<br type="_moz" /> </td>
   <td>F</td>
   <td>Se true, è possibile aggiungere note all'attività.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canClaim<br type="_moz" /> </td>
   <td>F</td>
   <td>Se true, è possibile richiedere l'attività.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canConsult<br type="_moz" /> </td>
   <td>F</td>
   <td>Se true, l'attività può essere consultata.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canForward<br type="_moz" /> </td>
   <td>F</td>
   <td>Se true, l'attività può essere inoltrata.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canShare<br type="_moz" /> </td>
   <td>F</td>
   <td>Se true, l'attività può essere condivisa.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. Allegato attività

   Gli allegati possono essere aggiunti a un&#39;attività. L&#39;allegato può essere di tipo allegato e nota. Di seguito sono riportate le proprietà dell&#39;oggetto attachment.

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Solo client</strong></td>
   <td><strong>Commenti</strong></td>
  </tr>
  <tr>
   <td>creatingDate<br type="_moz" /> </td>
   <td>F</td>
   <td>Timestamp della creazione dell'allegato.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>creatorId<br type="_moz" /> </td>
   <td>F</td>
   <td>ID dell'utente che ha aggiunto l'allegato.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>creatorName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nome dell'utente che ha aggiunto l'allegato.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>descrizione<br type="_moz" /> </td>
   <td>F</td>
   <td>Descrizione dell'allegato.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>fileName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nome dell'allegato.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>id<br type="_moz" /> </td>
   <td>F</td>
   <td>ID dell'allegato.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lastModifiedDate<br type="_moz" /> </td>
   <td>F</td>
   <td>Timestamp dell'ultima modifica apportata all'allegato.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>noteExtended<br type="_moz" /> </td>
   <td>F</td>
   <td>Se true, la nota è una nota estesa (lunga).<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>permissions<br type="_moz" /> </td>
   <td>F</td>
   <td>Autorizzazioni associate a un allegato. allowRead campo is for read permissions. allowWrite è per l'autorizzazione di scrittura. allowDelete è per l'autorizzazione di eliminazione.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>size<br type="_moz" /> </td>
   <td>F</td>
   <td>Dimensione dell'allegato in byte.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>taskId<br type="_moz" /> </td>
   <td>F</td>
   <td>ID dell'attività a cui viene aggiunto l'allegato.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>tipo<br type="_moz" /> </td>
   <td>F</td>
   <td>Il tipo è allegato per i file e il tipo è nota per le note.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedCreationDate<br type="_moz" /> </td>
   <td>T</td>
   <td>Contiene la data di creazione dell'allegato in base alle impostazioni dell'interfaccia utente dell'utente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedDescription<br type="_moz" /> </td>
   <td>T</td>
   <td>Descrizione allegato formattato. Utilizzato per visualizzare i caratteri speciali presenti nella descrizione dell'allegato nell'area di lavoro  AEM Forms.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedFileName<br type="_moz" /> </td>
   <td>T</td>
   <td>Nome allegato formattato. Utilizzato per visualizzare i caratteri speciali presenti nel nome dell'allegato nell'area di lavoro  AEM Forms. Solo per note.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. User

   Di seguito sono riportate le proprietà dell&#39;oggetto utente.

<table>
 <tbody>
  <tr>
   <td><strong>Proprietà</strong></td>
   <td><strong>Solo client</strong></td>
   <td><strong>Commenti</strong></td>
  </tr>
  <tr>
   <td>address<br type="_moz" /> </td>
   <td>F</td>
   <td>Indirizzo dell'utente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>commonName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nome comune dell'utente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>descrizione<br type="_moz" /> </td>
   <td>F</td>
   <td>Descrizione dell'utente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>directGroupMemberships<br type="_moz" /> </td>
   <td>F</td>
   <td>Elenco del gruppo di utenti.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>displayName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nome visualizzato dell'utente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>email<br type="_moz" /> </td>
   <td>F</td>
   <td>ID e-mail dell'utente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>F</td>
   <td>True se l'utente è fuori ufficio.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lastName<br type="_moz" /> </td>
   <td>F</td>
   <td>Cognome dell'utente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>firstName<br type="_moz" /> </td>
   <td>F</td>
   <td>Nome dell'utente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>oid<br type="_moz" /> </td>
   <td>F</td>
   <td>ID dell'utente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>org<br type="_moz" /> </td>
   <td>F</td>
   <td>Nome dell'organizzazione dell'utente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>postalAddress<br type="_moz" /> </td>
   <td>F</td>
   <td>Indirizzo postale dell'utente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>phone<br type="_moz" /> </td>
   <td>F</td>
   <td>Numero di contatto dell'utente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>phoneNumber<br type="_moz" /> </td>
   <td>F</td>
   <td>Numero di contatto dell'utente.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userid<br type="_moz" /> </td>
   <td>F</td>
   <td>ID di accesso dell'utente.<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>
