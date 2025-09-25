---
title: Utilizzo delle attività
description: Utilizza la pagina Ricerca attività per cercare le attività in base al nome utente o all’ID attività. Scopri di più sull’utilizzo delle attività.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 375376d1-60b3-49a4-8893-ba9336e6bf7b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '852'
ht-degree: 100%

---

# Utilizzo delle attività {#working-with-tasks}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Utilizza la pagina Ricerca attività per cercare le attività in base al nome utente o all’ID attività. I risultati della ricerca vengono visualizzati nella pagina Elenco attività, in cui è possibile accedere alla cronologia di un’attività. È inoltre possibile riassegnare un’attività se un utente ne ha troppe o se ha ricevuto un’assegnazione di attività per errore.

>[!NOTE]
>
>L’esecuzione di ricerche di attività non restituisce alcun risultato per i nomi utente che iniziano con un cancelletto (#). Se possibile, evita di creare nomi utente che iniziano con un simbolo numerico.

## Cerca le attività associate a un utente {#search-for-tasks-associated-with-a-user}

1. Nella console di amministrazione, fai clic su Servizi > Forms Workflow > Ricerca attività.
1. In Cerca per, seleziona Nome utente. Se conosci parte del nome utente che stai cercando, digitalo nella casella. Fai clic su Trova utente.
1. Viene visualizzata la pagina Trova utente. Puoi perfezionare la ricerca per nome utente o e-mail. Quando individui l’utente desiderato, seleziona il pulsante di opzione accanto al nome e fai clic su OK.
1. Per impostazione predefinita, la ricerca delle attività cerca quelle attualmente assegnate all’utente. Per cercare anche le attività precedentemente assegnate all’utente, seleziona Mostra attività non assegnate. Per cercare anche le attività completate dall’utente, seleziona Mostra attività completate.
1. Fai clic su Ricerca. Viene visualizzata la pagina Elenco task, in cui sono elencati i risultati della ricerca.

## Cerca un’attività quando ne conosci l’ID {#search-for-a-task-when-you-know-its-task-id}

1. Nella console di amministrazione, fai clic su Servizi > Forms Workflow > Ricerca attività.
1. In Cerca per, seleziona ID attività e digita l’ID attività nella casella.
1. Fai clic su Ricerca. Viene visualizzata la pagina Elenco task, in cui sono elencati i risultati della ricerca.

## Utilizzo dell’elenco delle attività {#working-with-the-task-list}

I risultati della ricerca di un’attività vengono visualizzati nella pagina Elenco attività. Puoi selezionare un’attività per aprire la pagina Cronologia attività. A questo punto, puoi assegnare l’attività a un altro utente.

Le attività vengono visualizzate con le seguenti informazioni:

**ID attività:** il numero intero positivo assegnato da Forms Workflow quando viene creata un’istanza dell’attività (avviata da un utente). Puoi utilizzare questo identificatore per tenere traccia dell’attività durante il relativo ciclo di vita. Fai clic su un ID attività per visualizzare i dettagli sulla cronologia dell’attività o per riassegnare l’attività a un altro utente.

**Stato:** se è Assegnato significa che l’attività è attualmente assegnata all’utente. Non assegnato indica che l’attività era assegnata all’utente in precedenza. Lo stato può anche essere Completato.

**Attività:** mostra il modulo e il nome per un’operazione iniziale o l’operazione di processo che ha generato l’attività.

**ID processo:** si tratta di un numero intero positivo assegnato da Forms Workflow quando viene creata un’istanza del processo, ovvero quando un utente o un passaggio automatico avvia un processo. Puoi utilizzare questo identificatore per tenere traccia dell’istanza di processo durante il relativo ciclo di vita.

**Nome processo - Versione:** il nome del processo definito in Workbench.

**Applicazione:** il nome dell’applicazione a cui appartiene il processo, come definito in Workbench.

**Data di creazione:** la data e l’ora di creazione dell’attività.

## Visualizzazione della cronologia delle attività e riassegnazione delle attività {#viewing-task-history-and-reassigning-tasks}

Nella pagina Cronologia attività viene visualizzato un elenco degli utenti e dei gruppi assegnati a una determinata attività.

Per ogni assegnazione di attività, l’elenco mostra le informazioni seguenti:

**Nome:** il nome dell’utente.

**Stato:** se è Assegnato significa che l’attività è attualmente assegnata all’utente. Non assegnata significa che l’attività è stata precedentemente assegnata all’utente.

**ID elenco di lavoro:** l’identificatore numerico della coda utente a cui appartiene l’attività. Un processo non può essere condiviso tra più utenti.

**Tipo:** indica come è stata assegnata l’attività:

**Iniziale:** l’attività è stata originariamente assegnata all’utente.

**Inoltro:** il proprietario attività originale ha assegnato l’attività a un altro utente.

**Rifiuto:** un’attività inoltrata è stata rifiutata oppure un’attività è stata restituita a un elenco di lavoro senza essere stata completata.

**Reclamo:** l’utente ha reclamato l’attività in un elenco di lavoro condiviso.

**Escalation:** è trascorso un tempo predeterminato (come impostato nell’azione utente in Workbench) senza interazione da parte dell’utente e l’attività è stata assegnata a un altro utente.

**Consulto:** il proprietario attività ha inoltrato l’attività a un altro utente per consultazione, che può aprire il modulo, salvare i dati, modificare gli allegati e le note, ma non può completare il passaggio. L’utente deve restituire l’attività al proprietario attività che ha consultato l’utente.

**Riassegnazione amministratore:** l’attività è stata riassegnata da un amministratore.

**Data assegnazione:** la data e l’ora in cui l’attività è stata assegnata all’utente.

### Assegnazione di un nuovo utente a un’attività {#assigning-a-new-user-to-a-task}

Nella pagina Assegna utente sono elencati gli utenti che possono essere assegnati a un’attività. Per accedere alla pagina Assegna utente, fai clic su Assegna nuovo utente nella pagina Cronologia attività.

1. Nella casella Cerca della pagina Assegna utente, digita parte o tutto il nome utente o l’indirizzo e-mail richiesto.
1. In Utilizzo, seleziona Nome o Indirizzo e-mail, quindi fai clic su Trova. Vengono visualizzati gli utenti corrispondenti alla ricerca.
1. Seleziona un utente dall’elenco e fai clic su OK. Viene visualizzata la pagina Cronologia attività con la nuova assegnazione utente.
