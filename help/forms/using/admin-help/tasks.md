---
title: Utilizzo delle attività
description: Utilizzare la pagina Ricerca task per cercare i task in base al nome utente o all'ID task. Ulteriori informazioni sull'utilizzo delle attività.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 375376d1-60b3-49a4-8893-ba9336e6bf7b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 0%

---

# Utilizzo delle attività {#working-with-tasks}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Utilizzare la pagina Ricerca task per cercare i task in base al nome utente o all&#39;ID task. I risultati della ricerca vengono visualizzati nella pagina Elenco task, in cui è possibile accedere alla cronologia di un task. È inoltre possibile riassegnare un&#39;attività se un utente ha troppe attività o se un utente ha ricevuto un&#39;assegnazione di attività per errore.

>[!NOTE]
>
>L&#39;esecuzione di ricerche di attività non restituisce alcun risultato per i nomi utente che iniziano con un cancelletto (#). Se possibile, evita di creare nomi utente che iniziano con un simbolo numerico.

## Cerca le attività associate a un utente {#search-for-tasks-associated-with-a-user}

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro moduli > Ricerca attività.
1. In Cerca per selezionare Nome utente. Se si conosce parte del nome utente che si sta cercando, digitarlo nella casella. Fare clic su Trova utente.
1. Viene visualizzata la pagina Trova utente. Puoi perfezionare la ricerca per nome utente o e-mail. Quando si individua l&#39;utente desiderato, selezionare il pulsante di opzione accanto al nome e fare clic su OK.
1. Per impostazione predefinita, la ricerca delle attività cerca le attività attualmente assegnate all&#39;utente. Per cercare anche le attività precedentemente assegnate all&#39;utente, selezionare Mostra attività non assegnate. Per cercare anche le attività completate dall&#39;utente, selezionare Mostra attività completate.
1. Fai clic su Cerca. Viene visualizzata la pagina Elenco task, in cui sono elencati i risultati della ricerca.

## Cerca un&#39;attività quando ne conosci l&#39;ID {#search-for-a-task-when-you-know-its-task-id}

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro moduli > Ricerca attività.
1. In Cerca per selezionare ID attività e digitare l&#39;ID attività nella casella.
1. Fai clic su Cerca. Viene visualizzata la pagina Elenco task, in cui sono elencati i risultati della ricerca.

## Utilizzo dell’elenco delle attività {#working-with-the-task-list}

I risultati della ricerca di un&#39;attività vengono visualizzati nella pagina Elenco attività. È possibile selezionare un task per aprire la pagina Cronologia task. A questo punto è possibile assegnare l&#39;attività a un altro utente.

Le attività vengono visualizzate con le seguenti informazioni:

**ID attività:** Il numero intero positivo assegnato dal flusso di lavoro dei moduli quando viene creata un&#39;istanza dell&#39;attività (avviata da un utente). È possibile utilizzare questo identificatore per tenere traccia dell&#39;attività durante il relativo ciclo di vita. Fare clic su un ID attività per visualizzare i dettagli sulla cronologia dell&#39;attività o per riassegnare l&#39;attività a un altro utente.

**Stato:** assegnato indica che l&#39;attività è attualmente assegnata all&#39;utente. Non assegnato significa che l’attività è stata precedentemente assegnata all’utente. Lo stato può anche essere Completato.

**Attività:** mostra il modulo e il nome per un&#39;operazione iniziale o l&#39;operazione di processo che ha generato l&#39;attività.

**ID processo:** Questo numero intero positivo assegnato dal flusso di lavoro dei moduli quando viene creata un&#39;istanza del processo, ovvero quando un utente o un passaggio automatico avvia un processo. È possibile utilizzare questo identificatore per tenere traccia dell&#39;istanza di processo durante il relativo ciclo di vita.

**Nome processo - Versione:** Il nome del processo definito in Workbench.

**Applicazione:** il nome dell&#39;applicazione a cui appartiene il processo, come definito in Workbench.

**Data di creazione:** La data e l&#39;ora di creazione dell&#39;attività.

## Visualizzazione della cronologia delle attività e riassegnazione delle attività {#viewing-task-history-and-reassigning-tasks}

Nella pagina Cronologia attività viene visualizzato un elenco degli utenti e dei gruppi assegnati a una determinata attività.

Per ogni assegnazione di attività, l&#39;elenco mostra le informazioni seguenti:

**Nome:** il nome dell&#39;utente.

**Stato:** assegnato indica che l&#39;attività è attualmente assegnata all&#39;utente. Non assegnato significa che l’attività è stata precedentemente assegnata all’utente.

**ID Worklist:** l&#39;identificatore numerico della coda utente a cui appartiene l&#39;attività. Un processo può essere condiviso tra più utenti.

**Tipo:** Indica come è stata assegnata l&#39;attività:

**Iniziale:** all&#39;utente è stata originariamente assegnata l&#39;attività.

**Inoltra:** Il proprietario dell&#39;attività originale ha assegnato l&#39;attività a un altro utente.

**Rifiuto:** un&#39;attività inoltrata è stata rifiutata oppure un&#39;attività è stata restituita a un elenco lavori senza essere stata completata.

**Attestazione:** l&#39;utente ha richiesto l&#39;attività in un elenco lavori condiviso.

**Riassegnazione:** È trascorso un tempo predeterminato (come impostato nell&#39;azione utente in Workbench) senza interazione da parte dell&#39;utente e l&#39;attività è stata assegnata a un altro utente.

**Consultare:** Il proprietario dell&#39;attività ha inoltrato l&#39;attività a un altro utente per consultazione, che può aprire il modulo, salvare i dati, modificare gli allegati e le note, ma non può completare il passaggio. L&#39;utente deve restituire l&#39;attività al proprietario dell&#39;attività che ha consultato l&#39;utente.

**Riassegnazione amministratore:** l&#39;attività è stata riassegnata da un amministratore.

**Data assegnazione:** La data e l&#39;ora in cui l&#39;attività è stata assegnata all&#39;utente.

### Assegnazione di un nuovo utente a un&#39;attività {#assigning-a-new-user-to-a-task}

Nella pagina Assegna utente sono elencati gli utenti che possono essere assegnati a un&#39;attività. Per accedere alla pagina Assegna utente, fare clic su Assegna nuovo utente nella pagina Cronologia attività.

1. Nella casella Cerca della pagina Assegna utente, digita parte o tutto il nome utente o l’indirizzo e-mail richiesto.
1. In Utilizzo, seleziona Nome o Indirizzo e-mail, quindi fai clic su Trova. Vengono visualizzati gli utenti corrispondenti alla ricerca.
1. Selezionare l&#39;utente dall&#39;elenco e fare clic su OK. Viene visualizzata la pagina Cronologia attività con la nuova assegnazione utente.
