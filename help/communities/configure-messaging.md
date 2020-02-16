---
title: Funzionalità di messaggistica
seo-title: Funzionalità di messaggistica
description: Configurazione dei componenti di messaggistica
seo-description: Configurazione dei componenti di messaggistica
uuid: 8b99ded1-aec2-40c9-82d5-e2e404f614ca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9d952604-f9ef-498f-937b-871817c80226
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Funzionalità di messaggistica{#messaging-feature}

Oltre alle interazioni visibili al pubblico che si verificano nei forum e nei commenti, la funzione di messaggistica di** **AEM Communities consente ai membri della community di interagire più privatamente.

Questa funzione può essere inclusa quando si crea un sito [](/help/communities/overview.md#communitiessites) community.

La funzione di messaggistica consente di:

**A** - inviare un messaggio a uno o più membri **B** della community - inviare messaggi diretti in [massa a gruppi](/help/communities/messaging.md#group-messaging)**C** di membri della community - inviare un messaggio con allegati **D** - inoltrare un messaggio**E - **risponde a un messaggio **** F - cancellare un messaggio**G **- ripristinare un messaggio eliminato

![messaging-section](assets/messaging-section.png) ![restore-message](assets/restore-message.png)

Per attivare e modificare la funzione di messaggistica, vedi:

* [Configurare i messaggi](/help/communities/messaging.md) per gli amministratori
* [Messaging Essentials](/help/communities/essentials-messaging.md) for developer

>[!NOTE]
>
>Non è supportato aggiungere `Compose Message, Message, or Message List` componenti (nel gruppo di `Communities`componenti) a una pagina in modalità di modifica dell’autore.

## Configurare i componenti per la messaggistica {#configure-messaging-components}

Quando la messaggistica è abilitata per un sito community, viene configurata senza bisogno di ulteriori configurazioni. Le informazioni vengono fornite se è necessario modificare la configurazione predefinita.

### Configura elenco messaggi (finestra di messaggio) {#configure-message-list-message-box}

Per modificare la configurazione dell&#39;elenco dei messaggi per le pagine **Posta in arrivo**, **Inviati** e **Cestino **pagine della funzione di messaggistica, aprire il sito in modalità [di modifica](/help/communities/sites-console.md#authoring-site-content)dell&#39;autore.

1. In `Preview`modalità, selezionare il collegamento **Messages **link per aprire la pagina di messaggistica principale. Selezionare quindi **Inbox**, **Sent Items **o **Cestino **per configurare il componente per l&#39;elenco dei messaggi.

1. In `Edit` modalità, selezionate il componente sulla pagina.
1. Per accedere alla finestra di dialogo di configurazione, annullare l’ereditarietà selezionando l’ `link`icona .
Una volta annullata l&#39;ereditarietà, è possibile selezionare l&#39;icona di configurazione per aprire la finestra di dialogo di configurazione.

1. Una volta completata la configurazione, è necessario ripristinare l&#39;ereditarietà selezionando l&#39; `broken link` icona.

![configure-message-list](assets/configure-message-list.png)

#### Basic tab {#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **Selettore** del servizio (*obbligatorio*) Impostare questo valore sulla proprietà**`serviceSelector.name`** dal servizio [Operazioni messaggistica](/help/communities/messaging.md#messaging-operations-service)AEM Communities.

* **Componi pagina**(*richiesta*) La pagina da aprire quando un membro fa clic sul pulsante **`Reply`**. La pagina di destinazione deve contenere il modulo **Componi messaggio** .

* **Rispondi/Visualizza come risorsa** Se questa opzione è selezionata, l&#39;URL di risposta e l&#39;URL di visualizzazione faranno riferimento a una risorsa. In caso contrario, i dati vengono passati come parametri di query nell&#39;URL.

* **Modulo** di visualizzazione profilo Modulo di profilo da utilizzare per visualizzare il profilo di mittenti.

* **Cartella** Cestino Se questa opzione è selezionata, questo componente Elenco messaggi visualizza solo i messaggi contrassegnati come eliminati (cestino).

* **Percorsi** cartella (*obbligatorio*) Con riferimento ai valori impostati per **inbox.path.name** e **sentitems.path.name **nel servizio [Operazioni messaggistica](/help/communities/messaging.md#messaging-operations-service)AEM Communities. Quando si configura per un `Inbox`, aggiungere una voce utilizzando il valore di **inbox.path.name**. Quando si configura per un `Outbox`, aggiungere una voce utilizzando il valore di **sentitems.path.name**. Durante la configurazione per `Trash`, aggiungere due voci con entrambi i valori.

#### Scheda Visualizzazione {#display-tab}

![display-tab-message-list](assets/display-tab-message-list.png)

* **Contrassegna pulsante** di lettura Se questa opzione è selezionata, visualizza un `Read`pulsante che consente di contrassegnare un messaggio come letto.

* **Contrassegna pulsante** non letto Se questa opzione è selezionata, visualizza un `Mark Unread` pulsante che consente di contrassegnare un messaggio come letto.

* **Pulsante** Elimina Se questa opzione è selezionata, visualizza un `Delete`pulsante che consente di contrassegnare un messaggio come letto. Duplica la funzionalità di eliminazione se **`Message Options`** è selezionata.

* **Opzioni** messaggio Se questa opzione è selezionata, vengono visualizzati **`Reply`**, **`Reply All`**, **`Forward`**e **`Delete`***i pulsanti che consentono di inviare o eliminare un messaggio. Duplica la funzionalità di eliminazione se **`Delete Button`** è selezionata.

* **Messaggi per pagina** Il numero specificato corrisponde al numero massimo di messaggi visualizzati per pagina in uno schema di impaginazione. Se non viene specificato alcun numero (lasciato vuoto), vengono visualizzati tutti i messaggi e non è prevista alcuna impaginazione.

* **Pattern** di marca temporale Fornisci pattern di marca temporale per una o più lingue. Il valore predefinito è en, de, fr, it, es, ja, zh_CN, ko_KR.

* **Visualizza utente** Scegliere **`Sender`**o **`Recipients`**per determinare se visualizzare il mittente o i destinatari.

### Configura messaggio di composizione {#configure-compose-message}

Per modificare la configurazione della pagina di composizione del messaggio, aprite il sito in modalità [di modifica](/help/communities/sites-console.md#authoring-site-content)dell’autore.

* In `Preview`modalità, selezionare il collegamento **Messages **link per aprire la pagina di messaggistica principale. Quindi fate clic sul pulsante Nuovo messaggio per aprire la `Compose Message` pagina.

* In `Edit` modalità, selezionate il componente principale nella pagina contenente il corpo del messaggio.
* Per accedere alla finestra di dialogo di configurazione, annullare l’ereditarietà selezionando l’ `link`icona .
Una volta annullata l&#39;ereditarietà, è possibile selezionare l&#39;icona di configurazione per aprire la finestra di dialogo di configurazione.

* Una volta completata la configurazione, è necessario ripristinare l&#39;ereditarietà selezionando l&#39; `broken link`icona.

![config-compose-message](assets/config-compose-message.png)

#### Basic tab {#basic-tab-1}

![basic-tab-compose](assets/basic-tab-compose.png)

* **URL** di reindirizzamento Immettere l&#39;URL della pagina visualizzata dopo l&#39;invio del messaggio. Esempio, `../messaging.html`.

* **Annulla URL** Immettere l&#39;URL della pagina visualizzata se il mittente annulla il messaggio. Esempio, `../messaging.html`.

* **Lunghezza massima oggetto** messaggio Il numero massimo di caratteri consentiti nel campo Oggetto. Ad esempio, 500. Il valore predefinito non è alcun limite.

* **Lunghezza massima del corpo** del messaggio Il numero massimo di caratteri consentiti nel campo Contenuto. Ad esempio, 10000. Il valore predefinito non è alcun limite.

* **Selettore** del servizio (*obbligatorio*) Impostare questo valore sulla proprietà**`serviceSelector.name`** dal servizio [Operazioni messaggistica](/help/communities/messaging.md#messaging-operations-service)AEM Communities.

#### Scheda Visualizzazione {#display-tab-1}

![display-tab-compose](assets/display-tab-compose.png)

* **Mostra campo** oggetto Se questa opzione è selezionata, mostra il `Subject` campo e abilita l’aggiunta di un oggetto al messaggio. Il valore predefinito non è selezionato.

* **Etichetta** oggetto Immettere il testo da visualizzare accanto al `Subject` campo. Default is `Subject`.

* **Mostra campo** file allegato Se questa opzione è selezionata, mostrare il `Attachment` campo e abilitare l&#39;aggiunta di allegati al messaggio. Il valore predefinito non è selezionato.

* **Etichetta** file allegato Immettere il testo da visualizzare accanto al `Attachment` campo. Default is **`Attach File`**.

* **Mostra campo** contenuto Se questa opzione è selezionata, mostra il `Content` campo e abilita l&#39;aggiunta di un corpo del messaggio. Il valore predefinito non è selezionato.

* **Etichetta** contenuto Immettere il testo da visualizzare accanto al `Content` campo. Default is **`Body`**.

* **Se questa opzione è selezionata, l&#39;Editor** Rich Text indica l&#39;utilizzo di una casella di testo Contenuto personalizzata con un proprio editor Rich Text. Il valore predefinito non è selezionato.

* **Pattern** di marca temporale Fornisci pattern di marca temporale per una o più lingue. Il valore predefinito è en, de, fr, it, es, ja, zh_CN, ko_KR.

