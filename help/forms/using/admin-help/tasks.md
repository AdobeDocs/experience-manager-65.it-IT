---
title: Operazioni con le attività
seo-title: Operazioni con le attività
description: Utilizzare la pagina Ricerca attività per cercare le attività in base al nome utente o all'ID dell'attività. Ulteriori informazioni sull'utilizzo delle attività.
seo-description: Utilizzare la pagina Ricerca attività per cercare le attività in base al nome utente o all'ID dell'attività. Ulteriori informazioni sull'utilizzo delle attività.
uuid: 630372d5-255f-4ea8-974d-d4f923108673
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9161c8ca-ef33-4ec9-affc-94b5b3e48a4c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 0%

---


# Operazioni con le attività {#working-with-tasks}

Utilizzare la pagina Ricerca attività per cercare le attività in base al nome utente o all&#39;ID dell&#39;attività. I risultati della ricerca vengono visualizzati nella pagina Elenco attività, in cui è possibile accedere alla cronologia di un&#39;attività. È inoltre possibile riassegnare un&#39;attività se un utente ha troppe attività o se un utente ha ricevuto un&#39;assegnazione di attività per errore.

>[!NOTE]
>
>L&#39;esecuzione delle ricerche di attività non restituisce alcun risultato per i nomi utente che iniziano con un simbolo cancelletto (#). Se possibile, evitare di creare nomi utente che iniziano con un simbolo cancelletto.

## Cerca attività associate a un utente {#search-for-tasks-associated-with-a-user}

1. Nella console di amministrazione, fare clic su Servizi > Flusso di lavoro moduli > Ricerca attività.
1. In Cerca per, selezionate Nome utente. Se si conosce parte del nome utente che si sta cercando, digitarlo nella casella. Fate clic su Trova utente.
1. Viene visualizzata la pagina Trova utente. Per perfezionare ulteriormente la ricerca, effettuate una ricerca in base al nome utente o all’e-mail. Quando individuate l’utente che state cercando, selezionate il pulsante di scelta accanto al nome e fate clic su OK.
1. Per impostazione predefinita, la ricerca delle attività cerca le attività attualmente assegnate all&#39;utente. Per cercare anche le attività precedentemente assegnate all&#39;utente, selezionare Mostra attività non assegnata. Per cercare anche le attività completate dall&#39;utente, selezionare Mostra attività completata.
1. Fate clic su Cerca. Viene visualizzata la pagina Elenco attività, in cui sono elencati i risultati della ricerca.

## Ricerca di un&#39;attività quando si conosce il relativo ID attività {#search-for-a-task-when-you-know-its-task-id}

1. Nella console di amministrazione, fare clic su Servizi > Flusso di lavoro moduli > Ricerca attività.
1. In Cerca per, selezionare ID attività e digitare l&#39;ID attività nella casella.
1. Fate clic su Cerca. Viene visualizzata la pagina Elenco attività, in cui sono elencati i risultati della ricerca.

## Utilizzo dell&#39;elenco delle attività {#working-with-the-task-list}

I risultati di una ricerca di attività vengono visualizzati nella pagina Elenco attività. È possibile selezionare un&#39;attività per aprire la pagina Cronologia attività. Da qui è possibile assegnare l’attività a un altro utente.

Le attività vengono visualizzate con le informazioni seguenti:

**ID attività:** il numero intero positivo assegnato dal flusso di lavoro del modulo quando viene creata un&#39;istanza dell&#39;attività (avviata da un utente). È possibile utilizzare questo identificatore per tenere traccia dell&#39;attività nel corso del suo ciclo di vita. Fare clic su un ID attività per visualizzare i dettagli relativi alla cronologia delle attività o per riassegnare l&#39;attività a un altro utente.

**Stato:** assegnato indica che l&#39;attività è attualmente assegnata all&#39;utente. Non assegnato indica che l&#39;attività era stata precedentemente assegnata all&#39;utente. È inoltre possibile completare lo stato.

**Attività:** mostra il modulo e il nome di un&#39;operazione iniziale o dell&#39;operazione di processo che ha generato l&#39;attività.

**ID processo:** questo numero intero positivo assegnato dal flusso di lavoro dei moduli quando viene creata un&#39;istanza del processo (ovvero quando un utente o un passaggio automatico avvia un processo). Potete utilizzare questo identificatore per tenere traccia dell’istanza di processo nel corso del suo ciclo di vita.

**Nome processo - Versione:** nome del processo, come definito in Workbench.

**Applicazione:** il nome dell&#39;applicazione a cui appartiene il processo, come definito in Workbench.

**Data creazione:** data e ora di creazione dell&#39;attività.

## Visualizzazione della cronologia delle attività e riassegnazione delle attività {#viewing-task-history-and-reassigning-tasks}

Nella pagina Cronologia attività viene visualizzato un elenco degli utenti e dei gruppi assegnati a una particolare attività.

Per ogni assegnazione di task, l&#39;elenco mostra le informazioni seguenti:

**Nome:** il nome dell’utente.

**Stato:** assegnato indica che l&#39;attività è attualmente assegnata all&#39;utente. Non assegnato indica che l’attività è stata precedentemente assegnata all’utente.

**ID elenco di lavoro:** Identificatore numerico della coda di utenti a cui appartiene l&#39;attività. Un processo può essere condiviso tra più utenti.

**Tipo:** Indica l&#39;assegnazione dell&#39;attività:

**Iniziale:** all’utente è stata originariamente assegnata l’attività.

**Avanti:** il proprietario dell&#39;attività originale ha assegnato l&#39;attività a un altro utente.

**Rifiuta:** Un&#39;attività inoltrata è stata rifiutata o un&#39;attività è stata restituita a un elenco di lavoro senza essere stata completata.

**Dichiarazione:** L&#39;utente ha richiesto l&#39;attività in un elenco di lavoro condiviso.

**Inoltro:** tempo trascorso (come impostato nell&#39;azione Utente in Workbench) predeterminato senza interazione con l&#39;utente; a un altro utente è stata assegnata l&#39;attività.

**Consulta:** Il proprietario dell&#39;attività ha inoltrato l&#39;attività a un altro utente per la consultazione, che può aprire il modulo, salvare i dati, modificare gli allegati e le note, ma non può completare il passaggio. L&#39;utente deve restituire l&#39;attività al proprietario dell&#39;attività che ha consultato l&#39;utente.

**Riassegnazione amministratore:** l&#39;attività è stata riassegnata da un amministratore.

**Data assegnazione:** la data e l&#39;ora in cui l&#39;attività è stata assegnata all&#39;utente.

### Assegnazione di un nuovo utente a un&#39;attività {#assigning-a-new-user-to-a-task}

Nella pagina Assegna utente sono elencati gli utenti che possono essere assegnati a un’attività. Per accedere alla pagina Assegna utente, fai clic su Assegna nuovo utente nella pagina Cronologia attività.

1. Nella casella Cerca della pagina Assegna utente, digitate parte o tutto il nome utente o l’indirizzo e-mail richiesto.
1. In Utilizzo, selezionare Nome o Indirizzo e-mail, quindi fare clic su Trova. Vengono visualizzati gli utenti che corrispondono alla ricerca.
1. Selezionate l’utente dall’elenco e fate clic su OK. Viene visualizzata la pagina Cronologia attività con la nuova assegnazione utente.

