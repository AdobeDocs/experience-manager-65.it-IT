---
title: Configurare le impostazioni di Fuori sede
seo-title: Configure Out of Office settings
description: Configurare le impostazioni Fuori sede
seo-description: Configure Out of Office settings
exl-id: e4c9d74c-e08d-4675-91f2-4f9fc2f1bcea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 0%

---

# Configurare l&#39;impostazione Fuori sede {#configure-out-of-office-settings}

Se si prevede di uscire dall&#39;ufficio, è possibile specificare cosa accade agli articoli che vi vengono assegnati per quel periodo.

Puoi specificare una data e un’ora di inizio e una data e un’ora di fine per rendere effettive le impostazioni fuori sede. Se ti trovi in un fuso orario diverso dal server, il fuso orario utilizzato è quello del client.

Puoi impostare una persona predefinita a cui vengono inviati tutti gli elementi. È inoltre possibile specificare eccezioni per gli elementi di processi specifici da inviare a un utente diverso o da rimanere nella casella in entrata fino a quando non si ritorna. Se la persona designata è anche fuori dall&#39;ufficio, l&#39;articolo va all&#39;utente che ha designato. Se l&#39;elemento non può essere assegnato a un utente che non è fuori ufficio, l&#39;elemento rimane nella Posta in arrivo.

Puoi separare la delega degli elementi in base ai modelli di flusso di lavoro. Ad esempio, puoi assegnare un elemento correlato al Flusso di lavoro A all’utente A e un elemento relativo al Flusso di lavoro B viene assegnato all’utente B.


>[!NOTE]
>
>* Quando si attiva l’impostazione Fuori sede, tutti gli elementi disponibili nella casella in entrata prima di attivare l’impostazione rimangono nella casella in entrata. Vengono delegati solo gli elementi ricevuti dopo l’abilitazione dell’impostazione.
>* Quando si disattiva l&#39;impostazione Fuori sede, gli elementi delegati non vengono assegnati automaticamente. È possibile utilizzare la funzionalità di attestazione per assegnare gli elementi.
>* Quando l&#39;utente A delega gli elementi all&#39;utente B e l&#39;utente B delega ulteriormente l&#39;utente C, gli elementi vengono assegnati solo all&#39;utente C e non all&#39;utente B.
>* Quando si verifica un ciclo nell&#39;assegnazione, le attività rimangono con l&#39;utente originale. Ad esempio, quando l&#39;utente A delega gli elementi all&#39;utente B l&#39;utente B delega all&#39;utente C, l&#39;utente C delega all&#39;utente D e l&#39;utente D delega all&#39;utente B, viene creato un ciclo. In tale situazione, l&#39;elemento rimane con l&#39;utente originale. L&#39;utente A è l&#39;utente originale nell&#39;esempio precedente.


## Abilita l&#39;impostazione Fuori sede per il tuo account {#enable-out-of-office}

Esegui i seguenti passaggi per abilitare l’impostazione Fuori sede per il tuo account e delegare gli elementi della Posta in arrivo a un altro utente:

1. Accedi alla tua istanza AEM. Tocca ![Inbox](assets/bell.svg) icona e tocco **[!UICONTROL Visualizza tutto]**. Viene visualizzato un elenco degli elementi della casella in entrata.
1. Tocca ![Selettore vista](assets/viewlist.svg) o ![Selettore vista](assets/calendar.svg) accanto all’icona **[!UICONTROL Crea]** pulsante e tocco **[!UICONTROL Impostazioni]**. Viene visualizzata la finestra di dialogo delle impostazioni.
1. Apri **[!UICONTROL Fuori sede]** nella finestra di dialogo impostazioni.
1. Tocca **[!UICONTROL Attiva/Disattiva]** per abilitare l&#39;impostazione Fuori sede.
1. Specifica la **[!UICONTROL Ora di inizio]**  e **[!UICONTROL Ora di fine]** per l&#39;impostazione. Gli elementi sono delegati solo durante il periodo specificato. Lascia la **[!UICONTROL Ora di fine]** campo vuoto per delegare gli elementi per un periodo di tempo indefinito.
1. Seleziona la **[!UICONTROL Inoltra gli oggetti durante questo periodo]** casella di controllo. Se non selezioni l’opzione e non specifichi un assegnatario, gli elementi non verranno inoltrati ad alcun utente. Anche se sei via e l’impostazione è attivata, gli elementi rimangono nella Posta in arrivo.
1. Tocca **[!UICONTROL Aggiungi assegnatario]**. Specifica un utente nella **[!UICONTROL Assegnatario]** campo a cui delegare gli elementi. Specifica la **[!UICONTROL Modello di flusso di lavoro]** per delegare all&#39;utente specificato. Puoi selezionare più di un modello di flusso di lavoro.

   Inoltre, per assegnare tutti gli elementi, indipendentemente dal modello di flusso di lavoro, a un particolare utente, seleziona **[!UICONTROL Tutti i flussi di lavoro]** dall’elenco a discesa Modello flusso di lavoro . <br>

   Per assegnare gli elementi a un utente specifico per tutti i modelli di flusso di lavoro, ad eccezione di alcuni, seleziona **[!UICONTROL Tutti i flussi di lavoro]** dall’elenco a discesa Modello flusso di lavoro , tocca **[!UICONTROL + Aggiungi eccezioni]**e specifica i modelli di flusso di lavoro da escludere.
   <br>

   Ripeti il passaggio per aggiungere altri assegnatari. <br>

   >[!NOTE]
   >
   >L&#39;ordine degli assegnatari è importante. Quando un elemento viene assegnato a un utente che ha abilitato l&#39;impostazione fuori sede, l&#39;elemento viene valutato rispetto all&#39;elenco assegnatari specificato nell&#39;ordine in cui vengono aggiunti gli assegnatari. Quando un elemento corrisponde ai criteri, viene assegnato all’assegnatario e l’assegnatario successivo non viene selezionato.

1. Tocca **[!UICONTROL Salva]**. L&#39;impostazione ha effetto alla data e all&#39;ora di inizio specificate. Se effettui l&#39;accesso quando sei fuori ufficio, non sei considerato in ufficio fino a quando non cambi le impostazioni.

Ora, gli elementi assegnati durante il periodo di tempo Fuori sede vengono assegnati automaticamente all&#39;assegnatario specificato.
![Fuori sede](assets/out-of-office.png)

>[!NOTE]
>
>(Solo per gli elementi del flusso di lavoro incentrati su Forms) Attiva la **Consenti agli assegnatari di delegare utilizzando le impostazioni &quot;Fuori sede&quot;** opzione **Assegna attività** nel flusso di lavoro. Solo gli elementi che hanno abilitato la suddetta opzione sono delegati ad altri utenti.

## Limitazioni {#limitations}

* L&#39;assegnazione di elementi a un gruppo non è supportata.
* L&#39;abilitazione di Out of Office per le attività di progetto non è attualmente supportata.
