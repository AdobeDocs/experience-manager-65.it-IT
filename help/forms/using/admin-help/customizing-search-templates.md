---
title: Personalizzazione dei modelli di ricerca
description: Puoi creare modelli di ricerca da utilizzare in Workspace per cercare istanze di processi dalle pagine Da fare e Tracciamento. È inoltre possibile modificare o eliminare i modelli di ricerca esistenti.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: bf69de86-2ca6-4d21-936c-07c1debacfa0
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 0%

---

# Personalizzazione dei modelli di ricerca {#customizing-search-templates}

Puoi creare modelli di ricerca da utilizzare in Workspace per cercare istanze di processi dalle pagine Da fare e Tracciamento. È inoltre possibile modificare o eliminare i modelli di ricerca esistenti.

Durante la creazione o la modifica di un modello di ricerca, è possibile specificare il layout e l&#39;ordinamento dei risultati della ricerca. Tuttavia, gli utenti possono modificare queste impostazioni in Workspace dopo la visualizzazione dei risultati della ricerca.

Puoi creare tutti i modelli di ricerca necessari.

>[!NOTE]
>
>Quando si salva un modello di ricerca, è necessario assegnargli un nome univoco. In caso contrario, un modello esistente può essere sovrascritto senza un messaggio di avviso.

## Creare un modello di ricerca semplice {#create-a-simple-search-template}

1. Nella console di amministrazione, fai clic su Servizi > Workspace > Cerca modelli.
1. Nella casella Descrizione modello di ricerca della scheda Identificazione specificare lo scopo del modello.
1. (Facoltativo) Fai clic sulla scheda Criteri e specifica i criteri di ricerca per il modello.
1. Fare clic sulla scheda Salva, immettere un nome univoco per il modello e quindi fare clic su Salva.

## Creare o modificare un modello di ricerca {#create-or-edit-a-search-template}

1. Nella console di amministrazione, fai clic su Servizi > Workspace > Cerca modelli.
1. (Facoltativo) Se si sta modificando un modello esistente o si utilizza un modello esistente come base per un nuovo modello, selezionare il modello dall&#39;elenco Nome modello di ricerca.
1. Nella casella Descrizione modello di ricerca specificare lo scopo del modello.
1. (Facoltativo) Nella casella Istruzioni utente, fornisci tutte le istruzioni utili per l’utilizzo del modello. Queste istruzioni vengono visualizzate in Workspace quando un utente seleziona il modello di ricerca.
1. Fai clic sulla scheda Criteri. In questo punto è possibile definire uno o più criteri di ricerca. Per aggiungere un criterio di ricerca:

   * Nella parte superiore della scheda Criteri, selezionare un elemento processo o un elemento task.

     **Suggerimento**: *Se in precedenza è stato selezionato l&#39;elemento Nome processo e è stato specificato un processo, sono disponibili per la selezione anche le eventuali variabili di processo definite in tale processo.*

     **Suggerimento**: *Se si seleziona l&#39;elemento Visibile attività, gli utenti potranno rimuovere le attività completate dai risultati della ricerca.*

     I campi dei criteri di ricerca per l’elemento selezionato vengono visualizzati nella parte inferiore della scheda Criteri.

   * Per ogni elemento processo, elemento attività e variabile processo selezionati, compilare i campi di ricerca corrispondenti nella parte inferiore della scheda Criteri:

      * Seleziona un operatore relazionale (ad esempio &quot;sia uguale a&quot;) dall’elenco fornito e specifica il valore dell’operando nella casella accanto a esso.
      * (Facoltativo) Per consentire agli utenti di modificare il valore dell&#39;operando in Workspace, selezionare Consenti all&#39;utente di modificare l&#39;operando.
      * (Facoltativo) Per consentire agli utenti di modificare l&#39;operatore relazionale, selezionare Consenti all&#39;utente di selezionare un altro operatore relazionale. Nell&#39;elenco visualizzato selezionare gli operatori che saranno disponibili per l&#39;utente.

     **Suggerimento**: *Se è stato selezionato Nome processo come elemento, è possibile fare clic sull&#39;icona accanto al campo dell&#39;operando per visualizzare un elenco in cui è possibile selezionare un processo in esecuzione sul server Forms. Dopo aver selezionato un processo, tutte le variabili di processo definite in tale processo sono disponibili per la selezione in Variabili di processo nella sezione superiore della scheda Criteri.*

     **Suggerimento**: *È possibile eliminare un elemento dal modello di ricerca facendo clic sull&#39;icona Elimina accanto ai criteri di ricerca dell&#39;elemento.*

1. (Facoltativo) Per ogni intestazione di colonna da visualizzare nei risultati della ricerca, fare clic sulla scheda Layout ed eseguire i passaggi seguenti:

   * Selezionare un processo o un elemento attività e fare clic sulla freccia destra per spostarlo nell&#39;elenco Colonne da segnalare.
   * Nell&#39;elenco Colonne da segnalare selezionare l&#39;elemento del processo o dell&#39;attività e fare clic sulla freccia su o sulla freccia giù per spostarlo nella posizione desiderata nell&#39;ordine delle colonne. Le intestazioni di colonna nei risultati della ricerca verranno visualizzate nell&#39;ordine in cui sono elencate qui.
   * (Facoltativo) Per modificare il nome dell&#39;elemento per l&#39;intestazione di colonna, selezionare l&#39;elemento dall&#39;elenco Colonne da segnalare e specificare il nuovo nome.

   >[!NOTE]
   >
   >Il layout specificato nel modello di ricerca sostituisce le preferenze dell’utente specificate per le intestazioni di colonna in Workspace.

1. (Facoltativo) Per ordinare le colonne nei risultati della ricerca, fare clic sulla scheda Ordina ed eseguire i passaggi seguenti:

   * Selezionare un processo o un elemento task e fare clic sulla freccia destra per spostarlo nell&#39;elenco Ordinamento.
   * Nell&#39;elenco Ordinamento selezionare l&#39;elemento del processo o dell&#39;attività e fare clic sulla freccia su o sulla freccia giù per spostarlo nella posizione desiderata nell&#39;ordinamento. Le colonne nei risultati della ricerca verranno ordinate in base all&#39;ordine in cui sono elencate qui.
   * (Facoltativo) Per ordinare una colonna in ordine decrescente, seleziona la casella di controllo accanto al nome dell’elemento. Se la casella di controllo non è selezionata, la colonna viene ordinata in ordine crescente.

1. Fare clic sulla scheda Salva.
1. (Facoltativo) Se crei un modello di ricerca, assegnagli un nome univoco. Se non si specifica un nome univoco, è possibile sovrascrivere un modello esistente.
1. Fare clic sul pulsante Salva.

## Eliminare un modello di ricerca {#delete-a-search-template}

1. Nella scheda Identificazione, selezionare un nome dall&#39;elenco Nome modello di ricerca.
1. Fare clic su Elimina modello e quindi su OK.
