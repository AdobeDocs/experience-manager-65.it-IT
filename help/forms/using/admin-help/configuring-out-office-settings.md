---
title: Configurazione delle impostazioni Fuori sede
description: La funzione Fuori sede consente di specificare quando un utente sarà fuori sede e non sarà in grado di completare le attività assegnate da AEM Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1c8ad09b-d44a-4d90-86d5-d4c66cf5c57c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '671'
ht-degree: 100%

---

# Configurazione delle impostazioni Fuori sede {#configuring-out-of-office-settings}

La funzione Fuori sede consente agli utenti o agli amministratori di specificare quando un utente sarà fuori sede e non potrà completare le attività assegnate da AEM Forms. Quando un utente è impostato su Fuori sede, le relative attività vengono assegnate a uno o più utenti designati. Gli utenti possono modificare le impostazioni Fuori sede nell’area di lavoro, oppure gli amministratori possono modificare le impostazioni per conto di un utente in Forms Workflow.

Durante la creazione di un processo, l’utente di Workbench può specificare se un’attività può essere reindirizzata a causa di impostazioni Fuori sede.

## Visualizzare le informazioni Fuori sede di un utente {#view-a-user-s-out-of-office-information}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

1. Nella console di amministrazione, fai clic su Servizi > Forms Workflow > Fuori sede.
1. Nella casella nella parte superiore della pagina Fuori sede puoi effettuare una delle seguenti operazioni:

   **Ricerca per nome**

   Seleziona l’opzione Ricerca per nome. Digita tutto o parte del nome utente e fai clic su Trova. Se lasci vuoto il campo, Forms Workflow restituisce un elenco di tutti gli utenti.

   **Ricerca per intervallo di date**

   Seleziona l’opzione Ricerca per intervallo di date. Specifica le date di inizio e di fine con le marche temporali che desideri per limitare il risultato della ricerca. Fai clic su Trova.

1. Fai clic su un nome utente per visualizzare le informazioni Fuori sede dell’utente sotto l’elenco degli utenti.

## Modificare lo stato fuori sede di un utente {#change-a-user-s-out-of-office-status}

1. Trova l’utente come descritto in [Visualizzare le informazioni Fuori sede dell’utente](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
1. Fai clic sul nome dell’utente da modificare.
1. Dall’elenco *nome utente* attualmente visualizzato, seleziona In ufficio o Fuori ufficio.
1. Fai clic su Salva.

## Aggiungere un intervallo di date fuori sede per un utente {#add-an-out-of-office-date-range-for-a-user}

1. Trova l’utente come descritto in [Visualizzare le informazioni Fuori sede dell’utente](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
1. Fai clic sul nome dell’utente da modificare.
1. Fai clic su Aggiungi intervallo di date.
1. Immetti un’ora di inizio e un’ora di fine. Puoi fare clic sull’icona Calendario per selezionare una data. Se non specifichi un’ora di fine, l’utente verrà impostato come fuori sede a tempo indefinito.
1. Fai clic su Salva.

## Assegnare un utente per le attività fuori sede {#assign-a-user-for-out-of-office-tasks}

Quando un utente è fuori sede, puoi assegnare uno o più utenti per eseguire nuove attività per l’utente. Puoi impostare le seguenti configurazioni:

* Assegna tutte le nuove attività a un utente predefinito designato.
* Non riassegnare alcuna attività. Le nuove attività rimangono assegnate all’utente fuori sede.
* Assegna un utente predefinito che riceverà la maggior parte delle attività dell’utente, ma specifica che le attività di alcuni processi vengono riassegnate ad altri utenti o rimangono assegnate all’utente fuori sede.
* Non assegnare un utente predefinito, ma assegna determinate attività da determinati processi a utenti specifici.

   1. Trova l’utente come descritto in [Visualizzare le informazioni Fuori sede dell’utente](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
   1. Fai clic sul nome dell’utente da modificare.
   1. Nell’elenco Utente predefinito per attività fuori sede, seleziona un utente dall’elenco. Se non desideri designare un utente predefinito per la ricezione di elementi riassegnati, seleziona Non assegnare.

      Se il nome utente appropriato non viene visualizzato nell’elenco, fai clic su Trova utente e utilizza la finestra di dialogo Trova utente per ricercare l’utente. Seleziona l’utente appropriato dall’elenco e fai clic su Seleziona utente. Puoi inoltre fare clic su Visualizza pianificazione utente nella finestra di dialogo Trova utente per visualizzare la pianificazione fuori sede dell’utente selezionato.

   1. Se esistono processi che non devono essere inviati all’utente predefinito, fai clic su Aggiungi un’eccezione, quindi seleziona il processo e seleziona un altro utente dall’elenco. Puoi inoltre selezionare Non assegnare per fare in modo che l’attività rimanga assegnata all’utente fuori sede.
   1. Fai clic su Salva.
