---
title: Configurazione delle impostazioni Fuori sede
seo-title: Configuring Out of Office Settings
description: La funzione Fuori sede consente di specificare quando un utente sarà fuori sede e non sarà in grado di completare le attività assegnate dai moduli AEM.
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

# Configurazione delle impostazioni Fuori sede {#configuring-out-of-office-settings}

La funzione Fuori sede consente agli utenti o agli amministratori di specificare quando un utente sarà fuori sede e non sarà in grado di completare le attività assegnate dai moduli AEM. Quando un utente è impostato su Fuori sede, le sue attività vengono assegnate a uno o più utenti designati. Gli utenti possono modificare le impostazioni Fuori sede in Workspace oppure gli amministratori possono modificare le impostazioni per conto di un utente nel flusso di lavoro dei moduli.

Durante la creazione di un processo, l’utente di Workbench può specificare se un’attività può essere reindirizzata a causa di impostazioni Fuori sede.

## Visualizzare le informazioni Fuori sede di un utente {#view-a-user-s-out-of-office-information}

1. Nella console di amministrazione, fai clic su Servizi > Flusso di lavoro moduli > Fuori sede.
1. Nella casella nella parte superiore della pagina Fuori sede è possibile effettuare una delle operazioni seguenti:

   **Cerca per nome**

   Selezionare l&#39;opzione Cerca per nome. Digitare tutto o parte del nome utente e fare clic su Trova. Se si lascia vuoto il campo, Forms workflow restituisce un elenco di tutti gli utenti

   **Cerca per intervallo di date**

   Selezionare l&#39;opzione Cerca per intervallo di date. Specifica le date di inizio e di fine con le marche temporali desiderate per limitare il risultato della ricerca. Fai clic su Trova.

1. Fare clic su un nome utente per visualizzare le informazioni Fuori sede dell&#39;utente sotto l&#39;elenco degli utenti.

## Modificare lo stato di Fuori sede di un utente {#change-a-user-s-out-of-office-status}

1. Trovare l&#39;utente come descritto in [Visualizzare le informazioni Fuori sede di un utente](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
1. Fare clic sul nome dell&#39;utente che si desidera modificare.
1. Dalla sezione *Nome utente* è attualmente nell&#39;elenco, selezionare In Office o Out of the Office.
1. Fai clic su Salva.

## Aggiungere un intervallo di date Fuori sede per un utente {#add-an-out-of-office-date-range-for-a-user}

1. Trovare l&#39;utente come descritto in [Visualizzare le informazioni Fuori sede di un utente](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
1. Fare clic sul nome dell&#39;utente che si desidera modificare.
1. Fai clic su Aggiungi intervallo di date.
1. Immettere un&#39;ora di inizio e un&#39;ora di fine. Puoi fare clic sull’icona Calendario per selezionare una data. Se non si specifica un&#39;ora di fine, l&#39;utente verrà impostato come fuori sede a tempo indefinito.
1. Fai clic su Salva.

## Assegnare un utente per le attività Fuori sede {#assign-a-user-for-out-of-office-tasks}

Quando un utente è fuori sede, puoi assegnare uno o più utenti per eseguire nuove attività per l’utente. Puoi impostare le seguenti configurazioni:

* Assegna tutte le nuove attività a un utente predefinito designato.
* Non riassegnare alcuna attività. Le nuove attività rimangono assegnate all&#39;utente fuori sede.
* Assegna un utente predefinito che riceverà la maggior parte delle attività dell’utente, ma specifica che le attività di alcuni processi vengono riassegnate ad altri utenti o rimangono assegnate all’utente che è fuori sede.
* Non assegnare un utente predefinito, ma assegnare determinate attività da determinati processi a utenti specifici.

   1. Trovare l&#39;utente come descritto in [Visualizzare le informazioni Fuori sede di un utente](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
   1. Fare clic sul nome dell&#39;utente che si desidera modificare.
   1. Nell&#39;elenco Utente predefinito per attività fuori sede selezionare un utente dall&#39;elenco. Se non si desidera designare un utente predefinito per la ricezione di elementi riassegnati, selezionare Non assegnare.

      Se il nome utente appropriato non viene visualizzato nell&#39;elenco, fare clic su Trova utente e utilizzare la finestra di dialogo Trova utente per cercare l&#39;utente. Selezionare l&#39;utente appropriato dall&#39;elenco e fare clic su Seleziona utente. È inoltre possibile fare clic su Visualizza pianificazione utente nella finestra di dialogo Trova utente per visualizzare la pianificazione fuori sede dell&#39;utente selezionato.

   1. Se esistono processi che non devono essere inviati all&#39;utente predefinito, fare clic su Aggiungi un&#39;eccezione, quindi selezionare il processo e selezionare un altro utente dall&#39;elenco. È inoltre possibile selezionare Non assegnare per fare in modo che l&#39;attività rimanga assegnata all&#39;utente fuori sede.
   1. Fai clic su Salva.
