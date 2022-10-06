---
title: Personalizzazione dei modelli di ricerca
seo-title: Customizing search templates
description: È possibile creare modelli di ricerca da utilizzare in Workspace per cercare le istanze dei processi nelle pagine Da fare e Tracking. È inoltre possibile modificare o eliminare i modelli di ricerca esistenti.
seo-description: You can create search templates to be used in Workspace to search for instances of processes from the To Do and Tracking pages. You can also edit or delete existing search templates.
uuid: 2043ba8a-07f0-4054-af3c-f3a14c2183ab
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6e4b4dfa-3af5-4c21-a2a1-b90ef02d8514
exl-id: bf69de86-2ca6-4d21-936c-07c1debacfa0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 0%

---

# Personalizzazione dei modelli di ricerca {#customizing-search-templates}

È possibile creare modelli di ricerca da utilizzare in Workspace per cercare le istanze dei processi nelle pagine Da fare e Tracking. È inoltre possibile modificare o eliminare i modelli di ricerca esistenti.

Quando crei o modifichi un modello di ricerca, puoi specificare il layout e l’ordine dei risultati della ricerca. Tuttavia, gli utenti possono modificare queste impostazioni in Workspace dopo la visualizzazione dei risultati della ricerca.

Puoi creare tutti i modelli di ricerca richiesti.

>[!NOTE]
>
>Quando salvi un modello di ricerca, devi assegnargli un nome univoco. In caso contrario, un modello esistente può essere sovrascritto senza un messaggio di avviso.

## Creare un modello di ricerca semplice {#create-a-simple-search-template}

1. Nella console di amministrazione, fai clic su Servizi > Area di lavoro > Cerca modelli.
1. Nella casella Descrizione modello di ricerca della scheda Identificazione specificare lo scopo del modello.
1. (Facoltativo) Fai clic sulla scheda Criteri e specifica i criteri di ricerca per il modello.
1. Fare clic sulla scheda Salva, immettere un nome univoco per il modello, quindi fare clic su Salva.

## Creare o modificare un modello di ricerca {#create-or-edit-a-search-template}

1. Nella console di amministrazione, fai clic su Servizi > Area di lavoro > Cerca modelli.
1. (Facoltativo) Se stai modificando un modello esistente o utilizzando un modello esistente come base per un nuovo modello, selezionalo dall’elenco Nome modello di ricerca.
1. Nella casella Descrizione modello di ricerca specificare lo scopo del modello.
1. (Facoltativo) Nella casella Istruzioni utente , fornisci tutte le istruzioni utili per l’utilizzo del modello. Queste istruzioni vengono visualizzate in Workspace quando un utente seleziona il modello di ricerca.
1. Fai clic sulla scheda Criteri . In questo punto puoi definire uno o più criteri di ricerca. Per aggiungere un criterio di ricerca:

   * Nella parte superiore della scheda Criteri, seleziona un elemento del processo o un elemento dell’attività.

      **Suggerimento**: *Se in precedenza hai selezionato l&#39;elemento Nome processo e hai specificato un processo, puoi selezionare anche tutte le variabili di processo definite in tale processo.*

      **Suggerimento**: *Se selezioni l’elemento Visualizzazione attività , gli utenti potranno rimuovere i task completati dai risultati della ricerca.*

      I campi dei criteri di ricerca per l’elemento selezionato vengono visualizzati nella parte inferiore della scheda Criteri.

   * Per ogni elemento di processo, elemento task e variabile di processo selezionato, compila i campi di ricerca corrispondenti nella parte inferiore della scheda Criteri:

      * Seleziona un operatore relazionale (ad esempio &quot;essere uguale a&quot;) dall’elenco fornito e specifica il valore dell’operando nella casella accanto a esso.
      * (Facoltativo) Per consentire agli utenti di modificare il valore dell&#39;operando in Workspace, selezionare Consenti all&#39;utente di modificare l&#39;operando.
      * (Facoltativo) Per consentire agli utenti di modificare l&#39;operatore relazionale, selezionare Consenti all&#39;utente di selezionare un altro operatore relazionale. Nell’elenco visualizzato, seleziona gli operatori che saranno disponibili per l’utente.

      **Suggerimento**: *Se come elemento è stato selezionato Nome processo, è possibile fare clic sull’icona accanto al campo operando per visualizzare un elenco in cui selezionare un processo in esecuzione sul server dei moduli. Dopo aver selezionato un processo, tutte le variabili di processo definite in tale processo sono disponibili per la selezione in Variabili di processo nella sezione superiore della scheda Criteri.*

      **Suggerimento**: *Per eliminare un elemento dal modello di ricerca, fai clic sull’icona Elimina accanto ai criteri di ricerca dell’elemento.*


1. (Facoltativo) Per visualizzare l’intestazione di ogni colonna nei risultati della ricerca, fai clic sulla scheda Layout ed esegui le seguenti operazioni:

   * Selezionare un processo o un elemento dell&#39;attività e fare clic sulla freccia destra per spostarlo nell&#39;elenco Colonne da report.
   * Nell’elenco Colonne per report selezionare l’elemento del processo o dell’attività e fare clic sulla freccia su o sulla freccia giù per spostarlo nella posizione desiderata nell’ordine delle colonne. Le intestazioni di colonna nei risultati della ricerca vengono visualizzate nell’ordine in cui sono elencate.
   * (Facoltativo) Per modificare il nome dell’elemento per l’intestazione della colonna, selezionare l’elemento dall’elenco Colonne in cui creare un rapporto e specificare il nuovo nome.

   >[!NOTE]
   >
   >Il layout specificato nel modello di ricerca sostituisce le preferenze dell’utente specificate per le intestazioni di colonna in Workspace.

1. (Facoltativo) Per ogni colonna da ordinare nei risultati della ricerca, fare clic sulla scheda Ordina ed eseguire i seguenti passaggi:

   * Selezionare un elemento di processo o di attività e fare clic sulla freccia destra per spostarlo nell&#39;elenco Ordina ordine.
   * Nell&#39;elenco Ordina selezionare l&#39;elemento del processo o dell&#39;attività e fare clic sulla freccia Su o sulla freccia Giù per spostarlo nella posizione desiderata nell&#39;ordinamento. Le colonne nei risultati della ricerca vengono ordinate in base all’ordine in cui sono elencate.
   * (Facoltativo) Per ordinare una colonna in ordine decrescente, seleziona la casella di controllo accanto al nome dell’elemento. Se la casella di controllo non è selezionata, la colonna viene ordinata in ordine crescente.

1. Fai clic sulla scheda Salva .
1. (Facoltativo) Se crei un nuovo modello di ricerca, assegnagli un nome univoco. Se non si specifica un nome univoco, è possibile sovrascrivere un modello esistente.
1. Fai clic sul pulsante Salva .

## Eliminare un modello di ricerca {#delete-a-search-template}

1. Nella scheda Identificazione , seleziona un nome dall’elenco Nome modello di ricerca.
1. Fare clic su Elimina modello e quindi su OK.
