---
title: Configurazione delle impostazioni di Fuori sede
seo-title: Configuring Out of Office Settings
description: La funzione Fuori sede consente di specificare quando un utente sarà fuori ufficio e non sarà in grado di completare le attività assegnate dai moduli AEM.
seo-description: The Out of Office feature enables you to specify when a user will be out of the office and unable to complete tasks assigned by AEM forms.
uuid: 0d01df0a-aa6a-40e5-bf24-423ed1c932cc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 30312159-58a5-4781-b554-29dcbce696cb
exl-id: 1c8ad09b-d44a-4d90-86d5-d4c66cf5c57c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---

# Configurazione delle impostazioni di Fuori sede {#configuring-out-of-office-settings}

La funzione Fuori sede consente agli utenti o agli amministratori di specificare quando un utente sarà fuori ufficio e non sarà in grado di completare le attività assegnate dai moduli AEM. Quando un utente è impostato su Fuori sede, le relative attività vengono assegnate a uno o più utenti designati. Gli utenti possono modificare le impostazioni Fuori sede in Workspace oppure gli amministratori possono modificare le impostazioni per conto di un utente nel flusso di lavoro dei moduli.

Durante la creazione di un processo, l&#39;utente di Workbench può specificare se un&#39;attività può essere reindirizzata a causa delle impostazioni Fuori sede.

## Visualizzazione delle informazioni fuori sede di un utente {#view-a-user-s-out-of-office-information}

1. Nella console di amministrazione, fai clic su Servizi > flusso di lavoro moduli > Fuori sede.
1. Nella casella accanto alla parte superiore della pagina Fuori sede è possibile effettuare una delle seguenti operazioni:

   **Ricerca per nome**

   Selezionare l’opzione Cerca per nome. Digitare tutto o parte del nome utente e fare clic su Trova. Se lasci il campo vuoto, il flusso di lavoro Forms restituisce un elenco di tutti gli utenti

   **Ricerca per intervallo di date**

   Selezionare l’opzione Cerca per intervallo di date. Specifica le date da e a insieme alle marche temporali desiderate per limitare il risultato della ricerca. Fare clic su Trova.

1. Fare clic su un nome utente per visualizzare le informazioni fuori sede dell&#39;utente sotto l&#39;elenco degli utenti.

## Modificare lo stato fuori sede di un utente {#change-a-user-s-out-of-office-status}

1. Trova l’utente, come descritto in [Visualizzazione delle informazioni fuori sede di un utente](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
1. Fare clic sul nome dell&#39;utente che si desidera modificare.
1. Da *Nome utente* è attualmente in elenco, selezionare In Office o Fuori dall&#39;Ufficio.
1. Fai clic su Salva.

## Aggiungere un intervallo di date fuori sede per un utente {#add-an-out-of-office-date-range-for-a-user}

1. Trova l’utente, come descritto in [Visualizzazione delle informazioni fuori sede di un utente](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
1. Fare clic sul nome dell&#39;utente che si desidera modificare.
1. Fai clic su Aggiungi intervallo di date.
1. Immettere l&#39;ora di inizio e l&#39;ora di fine. Puoi fare clic sull’icona Calendario per selezionare una data. Se non si specifica un&#39;ora di fine, l&#39;utente verrà impostato come fuori sede a tempo indeterminato.
1. Fai clic su Salva.

## Assegnare un utente per le attività fuori sede {#assign-a-user-for-out-of-office-tasks}

Quando un utente è fuori ufficio, è possibile assegnare uno o più utenti per eseguire eventuali nuove attività per l&#39;utente. Puoi impostare le seguenti configurazioni:

* Assegnare tutte le nuove attività a un utente predefinito designato.
* Non riassegnare attività. Le nuove attività rimangono assegnate all&#39;utente fuori sede.
* Assegna un utente predefinito che riceverà la maggior parte delle attività dell’utente, ma specifica che le attività di determinati processi vengono riassegnate ad altri utenti o rimangono assegnate all’utente fuori sede.
* Non assegnare un utente predefinito, ma assegnare determinate attività da determinati processi a utenti specifici.

   1. Trova l’utente, come descritto in [Visualizzazione delle informazioni fuori sede di un utente](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
   1. Fare clic sul nome dell&#39;utente che si desidera modificare.
   1. Nell&#39;elenco Attività predefinite utente per fuori sede selezionare un utente dall&#39;elenco. Se non si desidera designare un utente predefinito per ricevere gli elementi riassegnati, selezionare Non assegnare.

      Se il nome utente appropriato non viene visualizzato nell&#39;elenco, fare clic su Trova utente e utilizzare la finestra di dialogo Trova utente per cercare l&#39;utente. Seleziona dall’elenco l’utente appropriato e fai clic su Seleziona utente . È inoltre possibile fare clic su Visualizza pianificazione utente nella finestra di dialogo Trova utente per visualizzare la pianificazione fuori sede dell’utente selezionato.

   1. Se sono presenti processi che non devono essere inviati all&#39;utente predefinito, fare clic su Aggiungi un&#39;eccezione, quindi selezionare il processo e selezionare un altro utente dall&#39;elenco. È inoltre possibile selezionare Non assegnare per assegnare l&#39;attività all&#39;utente fuori sede.
   1. Fai clic su Salva.
