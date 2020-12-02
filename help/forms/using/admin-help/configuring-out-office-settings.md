---
title: Configurazione delle impostazioni Fuori sede
seo-title: Configurazione delle impostazioni Fuori sede
description: La funzione Fuori sede consente di specificare quando un utente sarà fuori ufficio e non sarà in grado di completare le attività assegnate dai moduli AEM.
seo-description: La funzione Fuori sede consente di specificare quando un utente sarà fuori ufficio e non sarà in grado di completare le attività assegnate dai moduli AEM.
uuid: 0d01df0a-aa6a-40e5-bf24-423ed1c932cc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 30312159-58a5-4781-b554-29dcbce696cb
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 0%

---


# Configurazione delle impostazioni fuori sede {#configuring-out-of-office-settings}

La funzione Fuori sede consente a utenti o amministratori di specificare quando un utente sarà fuori ufficio e non sarà in grado di completare le attività assegnate dai moduli AEM. Quando un utente è impostato su Fuori sede, le sue attività vengono assegnate a uno o più utenti designati. Gli utenti possono modificare le impostazioni Fuori sede in Workspace oppure gli amministratori possono modificare le impostazioni per conto di un utente nel flusso di lavoro dei moduli.

Durante la creazione di un processo, l&#39;utente di Workbench può specificare se è possibile reindirizzare un&#39;attività a causa delle impostazioni Fuori sede.

## Visualizzazione delle informazioni fuori sede di un utente {#view-a-user-s-out-of-office-information}

1. Nella console di amministrazione, fare clic su Servizi > Flusso di lavoro moduli > Fuori sede.
1. Nella casella accanto alla parte superiore della pagina Fuori sede, potete effettuare una delle seguenti operazioni:

   **Ricerca per nome**

   Selezionate l’opzione Cerca per nome. Digitate tutto o parte del nome utente e fate clic su Trova. Se lasciate vuoto il campo, il flusso di lavoro di Forms restituisce un elenco di tutti gli utenti

   **Cerca per intervallo di date**

   Selezionate l’opzione Cerca per intervallo di date. Specificate le date di origine e di destinazione insieme ai timestamp desiderati per limitare il risultato della ricerca. Fate clic su Trova.

1. Fate clic su un nome utente per visualizzare le informazioni fuori sede dell’utente sotto l’elenco degli utenti.

## Modifica dello stato fuori ufficio di un utente {#change-a-user-s-out-of-office-status}

1. Individuate l&#39;utente, come descritto in [Visualizza le informazioni fuori sede di un utente](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
1. Fate clic sul nome dell’utente che desiderate modificare.
1. Nell&#39;elenco *Nome utente*, selezionare In Office o Fuori dall&#39;ufficio.
1. Fate clic su Salva.

## Aggiunta di un intervallo di date fuori sede per un utente {#add-an-out-of-office-date-range-for-a-user}

1. Individuate l&#39;utente, come descritto in [Visualizza le informazioni fuori sede di un utente](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
1. Fate clic sul nome dell’utente che desiderate modificare.
1. Fai clic su Aggiungi intervallo date.
1. Immettete l’ora di inizio e di fine. Potete fare clic sull&#39;icona Calendario per selezionare una data. Se non si specifica un&#39;ora di fine, l&#39;utente verrà impostato come fuori ufficio a tempo indeterminato.
1. Fate clic su Salva.

## Assegnazione di un utente per le attività fuori sede {#assign-a-user-for-out-of-office-tasks}

Mentre un utente è fuori ufficio, potete assegnare uno o più utenti per eseguire qualsiasi nuova attività per l’utente. Potete impostare le seguenti configurazioni:

* Assegnare tutte le nuove attività a un utente predefinito designato.
* Non riassegnare alcuna attività. Le nuove attività restano assegnate all&#39;utente fuori dall&#39;ufficio.
* Assegnate un utente predefinito che riceverà la maggior parte delle attività dell&#39;utente, ma specificate che le attività di determinati processi vengono riassegnate ad altri utenti o restano assegnate all&#39;utente fuori ufficio.
* Non assegnate un utente predefinito, ma assegnate determinate attività da determinati processi a utenti specifici.

   1. Individuate l&#39;utente, come descritto in [Visualizza le informazioni fuori sede di un utente](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
   1. Fate clic sul nome dell’utente che desiderate modificare.
   1. Nell&#39;elenco Attività predefinite utente per fuori ufficio, selezionare un utente dall&#39;elenco. Se non si desidera designare un utente predefinito per ricevere gli elementi riassegnati, selezionare Non assegnare.

      Se il nome utente appropriato non viene visualizzato nell’elenco, fate clic su Trova utente e utilizzate la finestra di dialogo Trova utente per cercare l’utente. Selezionate l’utente appropriato dall’elenco e fate clic su Seleziona utente. Potete anche fare clic su Visualizza pianificazione utente nella finestra di dialogo Trova utente per visualizzare la pianificazione non in ufficio dell’utente selezionato.

   1. Se sono presenti processi che non devono essere inviati all&#39;utente predefinito, fare clic su Aggiungi un&#39;eccezione, quindi selezionare il processo e selezionare un altro utente dall&#39;elenco. È inoltre possibile selezionare Non assegnare per fare in modo che l&#39;attività rimanga assegnata all&#39;utente fuori ufficio.
   1. Fate clic su Salva.

