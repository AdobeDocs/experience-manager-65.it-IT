---
title: Configurare le impostazioni Fuori sede
seo-title: Configurare le impostazioni Fuori sede
description: Configurazione delle impostazioni Fuori sede
seo-description: Configurare le impostazioni Fuori sede
translation-type: tm+mt
source-git-commit: 7ed5c2d0121029811d8ddeca3b1121912bc761f4

---



# Configurare l&#39;impostazione Fuori sede {#configure-out-of-office-settings}

Se prevedete di uscire dall&#39;ufficio, potete specificare cosa accade agli elementi assegnati a quel periodo.

È possibile specificare una data e un&#39;ora di inizio e una data e un&#39;ora di fine affinché le impostazioni fuori sede siano attive. Se vi trovate in un fuso orario diverso dal server, il fuso orario utilizzato è quello del client.

Potete impostare una persona predefinita alla quale vengono inviati tutti gli elementi. È inoltre possibile specificare eccezioni per gli elementi provenienti da processi specifici da inviare a un altro utente o da rimanere nella Posta in arrivo fino al ritorno. Se anche la persona designata è fuori ufficio, l&#39;elemento va all&#39;utente che ha designato. Se l’elemento non può essere assegnato a un utente che non è fuori ufficio, l’elemento rimane nella Casella in entrata.

Potete separare la delega degli elementi in base ai modelli di workflow. Ad esempio, puoi assegnare all&#39;utente A un elemento correlato al Flusso di lavoro A e a un elemento correlato al Flusso di lavoro B è assegnato all&#39;utente B.


>[!NOTE]
>
> * Quando si attiva l&#39;impostazione Fuori sede, tutti gli elementi disponibili nella casella in entrata, prima di attivare l&#39;impostazione, rimangono nella inbox. Vengono delegati solo gli elementi ricevuti dopo l&#39;attivazione dell&#39;impostazione.
> * Quando disattivate l&#39;impostazione Fuori sede, gli elementi delegati non vengono automaticamente assegnati. È possibile utilizzare la funzionalità di attestazione per assegnare elementi.
> * Quando l&#39;utente A delega gli elementi all&#39;utente B e l&#39;utente B delega ulteriormente all&#39;utente C, gli elementi vengono assegnati solo all&#39;utente C e non all&#39;utente B.
> * In presenza di un ciclo di assegnazione, le attività restano associate all&#39;utente originale. Ad esempio, quando l&#39;utente A delega gli elementi all&#39;utente B l&#39;utente B delega all&#39;utente C, l&#39;utente C delega all&#39;utente D e l&#39;utente D delega all&#39;utente B, viene creato un ciclo. In questa situazione, l’elemento rimane unito all’utente originale. L&#39;utente A è l&#39;utente originale nell&#39;esempio precedente.


## Attiva l’impostazione Fuori sede per l’account {#enable-out-of-office}

Effettuate le seguenti operazioni per abilitare l&#39;impostazione Fuori sede per il vostro account e delegare gli elementi in entrata a un altro utente:

1. Accedi alla tua istanza di AEM. Toccate l’icona ![Inbox](assets/bell.svg) e toccate **[!UICONTROL Visualizza tutto]**. Viene visualizzato un elenco degli elementi della inbox.
1. Toccate l’icona ![Visualizza selettore](assets/viewlist.svg) o Selettore ![](assets/calendar.svg) vista accanto al pulsante **[!UICONTROL Crea]** e toccate **[!UICONTROL Impostazioni]**. Viene visualizzata la finestra di dialogo delle impostazioni.
1. Aprite la scheda **[!UICONTROL Fuori sede]** nella finestra di dialogo delle impostazioni.
1. Toccate il pulsante **[!UICONTROL Attiva/Disattiva]** per attivare l’impostazione Fuori sede.
1. Specificate l’ora **[!UICONTROL di]** inizio e l’ora **[!UICONTROL di]** fine per l’impostazione. Gli elementi sono delegati solo durante il periodo specificato. Lasciate vuoto il campo Ora **** fine per delegare gli elementi per un periodo di tempo indefinito.
1. Selezionare la casella di controllo **[!UICONTROL Inoltra gli elementi durante questo periodo]** . Se non selezionate l&#39;opzione e non specificate un assegnatario, gli elementi non verranno inoltrati ad alcun utente. Anche se siete lontani e l’impostazione è attivata, gli elementi rimangono nella Posta in arrivo.
1. Toccate **[!UICONTROL Aggiungi assegnatario]**. Specificate un utente nel campo **[!UICONTROL Assegnatario]** a cui delegare gli elementi. Specificate il modello **[!UICONTROL di]** flusso di lavoro da delegare all’utente specificato. Potete selezionare più modelli di workflow.

   Inoltre, per assegnare tutti gli elementi, indipendentemente dal modello di workflow, a un particolare utente, selezionare **[!UICONTROL Tutti i flussi]** di lavoro dall&#39;elenco a discesa Modello flusso di lavoro. <br>

   Per assegnare elementi a un utente specifico per tutti i modelli di workflow, ad eccezione di alcuni, selezionare **[!UICONTROL Tutti i flussi]** di lavoro dall&#39;elenco a discesa Modello flusso di lavoro, toccare **[!UICONTROL + Aggiungi eccezioni]**e specificare i modelli di workflow da escludere.
   <br>

   Ripetere il passaggio per aggiungere altri assegnatari. <br>

   >[!NOTE]
   >L&#39;ordine degli assegnatari è importante. Quando un elemento viene assegnato a un utente che ha attivato l&#39;impostazione fuori sede, l&#39;elemento viene valutato rispetto all&#39;elenco assegnatari specificato nell&#39;ordine in cui vengono aggiunti gli assegnatari. Quando un elemento soddisfa i criteri, viene assegnato all&#39;assegnatario e l&#39;assegnatario successivo non viene selezionato.

1. Toccate **[!UICONTROL Salva]**. L&#39;impostazione ha effetto alla data e all&#39;ora di inizio specificate. Se accedete mentre siete fuori dall&#39;ufficio, non sarete considerati in ufficio finché non cambiate le impostazioni.

Ora, gli elementi assegnati durante il periodo di tempo Fuori sede vengono automaticamente assegnati al cessionario specificato.\
![Fuori sede](assets/out-of-office.png)

>[!NOTE]
>(Solo per gli elementi del flusso di lavoro incentrati su Forms) Abilitare l&#39;opzione **Consenti all&#39;assegnatario di delegare utilizzando l&#39;opzione** &quot;Fuori sede&quot; del passaggio dell&#39;attività **** Assegna nel flusso di lavoro. Solo gli elementi con la suddetta opzione abilitata sono delegati ad altri utenti.

## Limiti {#limitations}

* L&#39;assegnazione di elementi a un gruppo non è supportata.
* Al momento l&#39;abilitazione di Out of Office per le attività di progetto non è supportata.
