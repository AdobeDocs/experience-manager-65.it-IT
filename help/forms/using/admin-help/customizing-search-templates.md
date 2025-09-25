---
title: Personalizzazione dei modelli di ricerca
description: Puoi creare modelli di ricerca da utilizzare nell’area di lavoro per cercare istanze di processi dalle pagine delle Attività da svolgere e Tracciamento. È inoltre possibile modificare o eliminare i modelli di ricerca esistenti.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: bf69de86-2ca6-4d21-936c-07c1debacfa0
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '867'
ht-degree: 100%

---

# Personalizzazione dei modelli di ricerca {#customizing-search-templates}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Puoi creare modelli di ricerca da utilizzare nell’area di lavoro per cercare istanze di processi dalle pagine delle Attività da svolgere e Tracciamento. È inoltre possibile modificare o eliminare i modelli di ricerca esistenti.

Durante la creazione o la modifica di un modello di ricerca, è possibile specificare il layout e l’ordinamento dei risultati della ricerca. Tuttavia, gli utenti possono modificare queste impostazioni nell’area di lavoro dopo la visualizzazione dei risultati della ricerca.

Puoi creare tutti i modelli di ricerca necessari.

>[!NOTE]
>
>Quando salvi un modello di ricerca, è necessario assegnargli un nome univoco. In caso contrario, un modello esistente può essere sovrascritto senza un messaggio di avviso.

## Creare un modello di ricerca semplice {#create-a-simple-search-template}

1. Nella console di amministrazione, fai clic su Servizi > Area di lavoro > Ricerca modelli.
1. Nella casella Descrizione modello di ricerca della scheda Identificazione, specifica lo scopo del modello.
1. (Facoltativo) Fai clic sulla scheda Criteri e specifica i criteri di ricerca per il modello.
1. Fai clic sulla scheda Salva, immetti un nome univoco per il modello e quindi fai clic su Salva.

## Creare o modificare un modello di ricerca {#create-or-edit-a-search-template}

1. Nella console di amministrazione, fai clic su Servizi > Area di lavoro > Ricerca modelli.
1. (Facoltativo) Se stai modificando un modello esistente o utilizzi un modello esistente come base per un nuovo modello, seleziona il modello dall’elenco Nome modello di ricerca.
1. Nella casella Descrizione modello di ricerca specifica lo scopo del modello.
1. (Facoltativo) Nella casella Istruzioni utente, fornisci tutte le istruzioni utili per l’utilizzo del modello. Queste istruzioni vengono visualizzate nell’area di lavoro quando un utente seleziona il modello di ricerca.
1. Fai clic sulla scheda Criteri. Qui è possibile definire uno o più criteri di ricerca. Per aggiungere un criterio di ricerca:

   * Nella parte superiore della scheda Criteri, seleziona un elemento Processo o un elemento Attività.

     **Suggerimento**: *se in precedenza hai selezionato l’elemento Nome processo e è stato specificato un processo, è possibile selezionare anche le eventuali variabili di processo definite in tale processo.*

     **Suggerimento**: *se selezioni l’elemento Attività visibile, gli utenti potranno rimuovere le attività completate dai risultati della ricerca.*

     I campi dei criteri di ricerca per l’elemento selezionato vengono visualizzati nella parte inferiore della scheda Criteri.

   * Per ciascun elemento Processo, elemento Attività e Variabile processo selezionati, compila i campi di ricerca corrispondenti nella parte inferiore della scheda Criteri:

      * Seleziona un operatore relazionale (ad esempio “è uguale a”) dall’elenco fornito e specifica il valore dell’operando nella casella accanto a esso.
      * (Facoltativo) Per consentire agli utenti di modificare il valore dell’operando nell’area di lavoro, seleziona Consenti all’utente di modificare l’operando.
      * (Facoltativo) Per consentire agli utenti di modificare l’operatore relazionale, seleziona Consenti all’utente di selezionare un altro operatore relazionale. Nell’elenco visualizzato, seleziona gli operatori che saranno disponibili per l’utente.

     **Suggerimento**: *se hai selezionato Nome processo come elemento, è possibile fare clic sull’icona accanto al campo dell’operando per visualizzare un elenco in cui è possibile selezionare un processo in esecuzione sul server Forms. Dopo aver selezionato un processo, tutte le variabili di processo definite in tale processo sono disponibili per la selezione in Variabili di processo nella sezione superiore della scheda Criteri.*

     **Suggerimento**: *è possibile eliminare un elemento dal modello di ricerca facendo clic sull’icona Elimina accanto ai criteri di ricerca dell’elemento.*

1. (Facoltativo) Per ogni intestazione di colonna da visualizzare nei risultati della ricerca, fai clic sulla scheda Layout ed esegui i passaggi seguenti:

   * Seleziona un processo o un elemento Attività e fai clic sulla freccia destra per spostarlo nell’elenco Colonne da segnalare.
   * Nell’elenco Colonne da segnalare, seleziona l’elemento del processo o dell’attività e fai clic sulla freccia su o sulla freccia giù per spostarlo nella posizione desiderata nell’ordine delle colonne. Le intestazioni di colonna nei risultati della ricerca verranno visualizzate nell’ordine in cui sono elencate qui.
   * (Facoltativo) Per modificare il nome dell’elemento per l’intestazione di colonna, seleziona l’elemento dall’elenco Colonne da segnalare e specifica il nuovo nome.

   >[!NOTE]
   >
   >Il layout specificato nel modello di ricerca sostituisce le preferenze dell’utente specificate per le intestazioni di colonna nell’area di lavoro.

1. (Facoltativo) Per ordinare le colonne nei risultati della ricerca, fai clic sulla scheda Ordina ed esegui i passaggi seguenti:

   * Seleziona un processo o un elemento Attività e fai clic sulla freccia destra per spostarlo nell’elenco Ordinamento.
   * Nell’elenco Ordinamento, seleziona l’elemento del processo o dell’attività e fai clic sulla freccia su o sulla freccia giù per spostarlo nella posizione desiderata nell’ordinamento. Le colonne nei risultati della ricerca verranno ordinate in base all’ordine in cui sono elencate qui.
   * (Facoltativo) Per ordinare una colonna in ordine decrescente, seleziona la casella di controllo accanto al nome dell’elemento. Se la casella di controllo non è selezionata, la colonna viene ordinata in ordine crescente.

1. Fai clic sulla scheda Salva.
1. (Facoltativo) Se crei un modello di ricerca, assegnagli un nome univoco. Se non specifici un nome univoco, è possibile sovrascrivere un modello esistente.
1. Fai clic sul pulsante Salva.

## Eliminare un modello di ricerca {#delete-a-search-template}

1. Nella scheda Identificazione, seleziona un nome dall’elenco Nome modello di ricerca.
1. Fai clic su Elimina questo modello e quindi su OK.
