---
title: Utilizzo delle attività
seo-title: Working with tasks
description: Utilizzare la pagina Ricerca attività per cercare le attività in base al nome utente o all’ID attività. Ulteriori informazioni sull'utilizzo delle attività.
seo-description: Use the Task Search page to search for tasks by user name or task ID. Learn more about working with tasks.
uuid: 630372d5-255f-4ea8-974d-d4f923108673
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9161c8ca-ef33-4ec9-affc-94b5b3e48a4c
exl-id: 375376d1-60b3-49a4-8893-ba9336e6bf7b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---

# Utilizzo delle attività {#working-with-tasks}

Utilizzare la pagina Ricerca attività per cercare le attività in base al nome utente o all’ID attività. I risultati della ricerca vengono visualizzati nella pagina Elenco attività, in cui è possibile accedere alla cronologia di un’attività. È inoltre possibile riassegnare un&#39;attività se un utente ha troppe attività o se un utente ha ricevuto un&#39;assegnazione di un&#39;attività per errore.

>[!NOTE]
>
>L&#39;esecuzione delle ricerche delle attività non restituisce alcun risultato per i nomi utente che iniziano con un simbolo numerico (#). Se possibile, evitare di creare nomi utente che iniziano con un simbolo numerico.

## Cercare le attività associate a un utente {#search-for-tasks-associated-with-a-user}

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro moduli > Ricerca attività.
1. In Cerca per, selezionare Nome utente. Se si conosce una parte del nome utente che si sta cercando, digitarla nella casella. Fare clic su Trova utente.
1. Viene visualizzata la pagina Trova utente. Puoi perfezionare ulteriormente la ricerca ricercando per nome utente o e-mail. Quando si individua l&#39;utente desiderato, selezionare il pulsante di scelta accanto al nome e fare clic su OK.
1. Per impostazione predefinita, la ricerca attività cerca le attività attualmente assegnate all’utente. Per cercare anche le attività precedentemente assegnate all&#39;utente, selezionare Mostra attività non assegnata. Per cercare anche le attività completate dall&#39;utente, selezionare Mostra attività completata.
1. Fare clic su Cerca. Viene visualizzata la pagina Elenco attività, in cui sono elencati i risultati della ricerca.

## Ricerca di un’attività quando si conosce il relativo ID attività {#search-for-a-task-when-you-know-its-task-id}

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro moduli > Ricerca attività.
1. In Cerca per, selezionare ID attività e digitare l&#39;ID attività nella casella.
1. Fare clic su Cerca. Viene visualizzata la pagina Elenco attività, in cui sono elencati i risultati della ricerca.

## Utilizzo dell’elenco delle attività {#working-with-the-task-list}

I risultati di una ricerca di attività vengono visualizzati nella pagina Elenco attività. È possibile selezionare un&#39;attività per aprire la pagina Cronologia attività. Da qui è possibile assegnare l’attività a un altro utente.

Le attività vengono visualizzate con le seguenti informazioni:

**ID attività:** Numero intero positivo assegnato dal flusso di lavoro del modulo quando viene creata un&#39;istanza dell&#39;attività (avviata da un utente). È possibile utilizzare questo identificatore per tenere traccia dell&#39;attività nel corso del relativo ciclo di vita. Fare clic su un ID attività per visualizzare i dettagli della cronologia delle attività o per riassegnare l&#39;attività a un altro utente.

**Stato:** Assegnato significa che l’attività è attualmente assegnata all’utente. Non assegnato indica che l’attività è stata precedentemente assegnata all’utente. È inoltre possibile completare lo stato.

**Attività:** Visualizza il modulo e il nome di un&#39;operazione iniziale o dell&#39;operazione di processo che ha generato l&#39;attività.

**ID processo:** Questo numero intero positivo assegnato dal flusso di lavoro dei moduli quando viene creata un&#39;istanza del processo (ovvero quando un utente o un passaggio automatizzato avvia un processo). Puoi utilizzare questo identificatore per tenere traccia dell’istanza di processo nel corso del suo ciclo di vita.

**Nome processo - Versione:** Nome del processo, come definito in Workbench.

**Applicazione:** Nome dell&#39;applicazione a cui appartiene il processo, come definito in Workbench.

**Data creazione:** Data e ora di creazione dell&#39;attività.

## Visualizzazione della cronologia delle attività e riassegnazione delle attività {#viewing-task-history-and-reassigning-tasks}

Nella pagina Cronologia attività viene visualizzato un elenco degli utenti e dei gruppi assegnati a una particolare attività.

Per ogni assegnazione di attività, l&#39;elenco mostra le seguenti informazioni:

**Nome:** Nome dell&#39;utente.

**Stato:** Assegnato indica che l’attività è attualmente assegnata all’utente. Non assegnato indica che l’attività è stata precedentemente assegnata all’utente.

**ID elenco di lavoro:** Identificatore numerico della coda utente a cui appartiene l&#39;attività. Un processo può essere condiviso tra più utenti.

**Tipo:** Indica come è stata assegnata l&#39;attività:

**Iniziale:** All&#39;utente è stata originariamente assegnata l&#39;attività.

**Avanti:** Il proprietario dell&#39;attività originale ha assegnato l&#39;attività a un altro utente.

**Rifiuta:** Un&#39;attività inoltrata è stata rifiutata o un&#39;attività è stata restituita a un elenco di lavoro senza essere stata completata.

**Domanda:** L&#39;utente ha richiesto l&#39;attività in un elenco di lavoro condiviso.

**Inoltro:** Tempo trascorso (come impostato nell’azione Utente in Workbench) senza interazione con l’utente; l’attività è stata assegnata a un altro utente.

**Consulta:** Il proprietario dell&#39;attività ha inoltrato l&#39;attività a un altro utente per la consultazione, che può aprire il modulo, salvare i dati, modificare gli allegati e le note, ma non può completare il passaggio. L&#39;utente deve restituire l&#39;attività al proprietario dell&#39;attività che ha consultato l&#39;utente.

**Riassegnazione amministratore:** L&#39;attività è stata riassegnata da un amministratore.

**Data assegnazione:** Data e ora in cui l’attività è stata assegnata all’utente.

### Assegnazione di un nuovo utente a un&#39;attività {#assigning-a-new-user-to-a-task}

Nella pagina Assegna utente sono elencati gli utenti che possono essere assegnati a un’attività. Per accedere alla pagina Assegna utente, fare clic su Assegna nuovo utente nella pagina Cronologia attività.

1. Nella casella Cerca della pagina Assegna utente digitare parte o tutto il nome utente o l&#39;indirizzo e-mail richiesto.
1. In Utilizzo selezionare Nome o Indirizzo e-mail, quindi fare clic su Trova. Vengono visualizzati gli utenti che corrispondono alla ricerca.
1. Selezionare l’utente dall’elenco e fare clic su OK. Viene visualizzata la pagina Cronologia attività con la nuova assegnazione utente.
