---
title: Personalizzazione dei modelli di ricerca
seo-title: Personalizzazione dei modelli di ricerca
description: È possibile creare modelli di ricerca da utilizzare in Workspace per cercare le istanze di processi dalle pagine Attività e Tracciamento. Potete inoltre modificare o eliminare i modelli di ricerca esistenti.
seo-description: È possibile creare modelli di ricerca da utilizzare in Workspace per cercare le istanze di processi dalle pagine Attività e Tracciamento. Potete inoltre modificare o eliminare i modelli di ricerca esistenti.
uuid: 2043ba8a-07f0-4054-af3c-f3a14c2183ab
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6e4b4dfa-3af5-4c21-a2a1-b90ef02d8514
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 0%

---


# Personalizzazione dei modelli di ricerca {#customizing-search-templates}

È possibile creare modelli di ricerca da utilizzare in Workspace per cercare le istanze di processi dalle pagine Attività e Tracciamento. Potete inoltre modificare o eliminare i modelli di ricerca esistenti.

Quando create o modificate un modello di ricerca, potete specificare il layout e l’ordine dei risultati della ricerca. Tuttavia, gli utenti possono modificare queste impostazioni in Workspace dopo la visualizzazione dei risultati della ricerca.

Potete creare tutti i modelli di ricerca richiesti.

>[!NOTE]
>
>Quando salvate un modello di ricerca, dovete assegnargli un nome univoco. In caso contrario, un modello esistente può essere sovrascritto senza ricevere un messaggio di avviso.

## Creare un modello di ricerca semplice {#create-a-simple-search-template}

1. Nella console di amministrazione, fai clic su Servizi > Area di lavoro > Cerca modelli.
1. Nella scheda Identificazione, nella casella Descrizione modello di ricerca, specificare lo scopo del modello.
1. (Facoltativo) Fate clic sulla scheda Criteri e specificate i criteri di ricerca per il modello.
1. Fate clic sulla scheda Salva, immettete un nome univoco per il modello, quindi fate clic su Salva.

## Creare o modificare un modello di ricerca {#create-or-edit-a-search-template}

1. Nella console di amministrazione, fai clic su Servizi > Area di lavoro > Cerca modelli.
1. (Facoltativo) Se state modificando un modello esistente o utilizzando un modello esistente come base per un nuovo modello, selezionate il modello dall&#39;elenco Nome modello di ricerca.
1. Nella casella Descrizione modello di ricerca, specificare lo scopo del modello.
1. (Facoltativo) Nella casella Istruzioni utente, fornite tutte le istruzioni utili per l’utilizzo del modello. Queste istruzioni vengono visualizzate in Workspace quando un utente seleziona il modello di ricerca.
1. Fare clic sulla scheda Criteri. Qui si definiscono uno o più criteri di ricerca. Per aggiungere un criterio di ricerca:

   * Nella parte superiore della scheda Criteri, selezionare un elemento di processo o un elemento di attività.

      **Suggerimento**:  *Se in precedenza è stato selezionato l&#39;elemento Nome processo e specificato un processo, tutte le variabili di processo definite in tale processo sono disponibili anche per la selezione.*

      **Suggerimento**:  *Se si seleziona l&#39;elemento Visibile attività, gli utenti potranno rimuovere i task completati dai risultati della ricerca.*

      I campi dei criteri di ricerca per l&#39;elemento selezionato vengono visualizzati nella parte inferiore della scheda Criteri.

   * Per ogni elemento di processo, elemento task e variabile di processo selezionato, compilare i campi di ricerca corrispondenti nella parte inferiore della scheda Criteri:

      * Selezionare un operatore relazionale (ad esempio &quot;essere uguale a&quot;) dall&#39;elenco fornito e specificare il valore dell&#39;operando nella casella accanto ad esso.
      * (Facoltativo) Per consentire agli utenti di modificare il valore dell&#39;operando in Workspace, selezionare Consenti all&#39;utente di modificare l&#39;operando.
      * (Facoltativo) Per consentire agli utenti di modificare l&#39;operatore relazionale, selezionare Consenti all&#39;utente di selezionare un altro operatore relazionale. Nell&#39;elenco visualizzato, selezionate gli operatori che saranno disponibili per l&#39;utente.

      **Suggerimento**:  *Se come elemento è stato selezionato Nome processo, è possibile fare clic sull&#39;icona accanto al campo operando per visualizzare un elenco in cui è possibile selezionare un processo in esecuzione sul server dei moduli. Dopo aver selezionato un processo, tutte le variabili di processo definite in tale processo sono disponibili per la selezione in Variabili di processo nella sezione superiore della scheda Criteri.*

      **Suggerimento**:  *Per eliminare un elemento dal modello di ricerca, fate clic sull&#39;icona Elimina accanto ai criteri di ricerca dell&#39;elemento.*


1. (Facoltativo) Per ogni intestazione di colonna da visualizzare nei risultati della ricerca, fare clic sulla scheda Layout ed eseguire le operazioni seguenti:

   * Selezionate un processo o un elemento attività e fate clic sulla freccia destra per spostarlo nell’elenco Colonne in cui visualizzare il rapporto.
   * Nell&#39;elenco Colonne su rapporto, selezionare il processo o l&#39;elemento attività e fare clic sulla freccia su o sulla freccia giù per portarlo nella posizione desiderata nell&#39;ordine delle colonne. Le intestazioni di colonna nei risultati della ricerca vengono visualizzate nell’ordine in cui sono elencate qui.
   * (Facoltativo) Per modificare il nome dell&#39;elemento per l&#39;intestazione della colonna, selezionate l&#39;elemento dall&#39;elenco Colonne in rapporto e fornite il nuovo nome.

   >[!NOTE]
   >
   >Il layout specificato nel modello di ricerca ha la priorità sulle preferenze dell&#39;utente specificate per le intestazioni di colonna in Workspace.

1. (Facoltativo) Per ogni colonna da ordinare nei risultati della ricerca, fate clic sulla scheda Ordina ed eseguite i seguenti passaggi:

   * Selezionare un processo o un elemento attività e fare clic sulla freccia destra per spostarlo nell&#39;elenco Ordinamento.
   * Nell&#39;elenco Ordina, selezionare il processo o l&#39;elemento attività e fare clic sulla freccia su o giù per portarlo nella posizione desiderata nell&#39;ordine di ordinamento. Le colonne nei risultati della ricerca verranno ordinate in base all&#39;ordine in cui sono elencate.
   * (Facoltativo) Per ordinare una colonna in ordine decrescente, selezionate la casella di controllo accanto al nome dell&#39;elemento. Se la casella di controllo non è selezionata, la colonna viene ordinata in ordine crescente.

1. Fate clic sulla scheda Salva.
1. (Facoltativo) Se create un nuovo modello di ricerca, assegnategli un nome univoco. Se non specificate un nome univoco, potete sovrascrivere un modello esistente.
1. Fate clic sul pulsante Salva.

## Eliminare un modello di ricerca {#delete-a-search-template}

1. Nella scheda Identificazione, selezionate un nome dall’elenco Nome modello di ricerca.
1. Fate clic su Elimina questo modello e su OK.

