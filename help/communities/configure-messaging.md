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
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 4%

---


# Funzione di messaggistica {#messaging-feature}

Oltre alle interazioni pubblicamente visibili che si verificano nei forum e nei commenti, la funzione di messaggistica di  AEM Communities consente ai membri della community di interagire più privatamente tra di loro.

Questa funzione può essere inclusa quando si crea un [sito community](/help/communities/overview.md#communitiessites).

La funzione di messaggistica consente di:

**A** - inviare un messaggio a uno o più membri della community

**B** - inviare messaggi diretti in  [massa a gruppi di membri della community](/help/communities/messaging.md#group-messaging)

**C** - inviare un messaggio con gli allegati

**D** - inoltrare un messaggio

**E** - risposta a un messaggio

**F** - eliminare un messaggio

**G** - ripristinare un messaggio eliminato

![messaging-section](assets/messaging-section.png)

![restore-message](assets/restore-message.png)

Per attivare e modificare la funzione di messaggistica, vedi:

* [Configurare i ](/help/communities/messaging.md) messaggi per gli amministratori
* [Messaging ](/help/communities/essentials-messaging.md) Essentials for developer

>[!NOTE]
>
>Non è supportato l&#39;aggiunta di componenti `Compose Message, Message, or Message List` (nel gruppo di componenti `Communities`) a una pagina in modalità di modifica dell&#39;autore.

## Configurare i componenti di messaggistica {#configure-messaging-components}

Quando la messaggistica è abilitata per un sito community, viene configurata senza bisogno di ulteriori configurazioni. Le informazioni vengono fornite se è necessario modificare la configurazione predefinita.

### Configura elenco messaggi (finestra di messaggio) {#configure-message-list-message-box}

Per modificare la configurazione dell&#39;elenco dei messaggi per le pagine **Inbox**, **Posta inviata** e **Cestino** della funzione di messaggistica, aprire il sito in [modalità di modifica dell&#39;autore](/help/communities/sites-console.md#authoring-site-content).

1. In modalità `Preview`, selezionare il collegamento **Messages** per aprire la pagina di messaggi principale. Selezionare quindi **Inbox**, **Posta inviata** o **Cestino** per configurare il componente per l&#39;elenco dei messaggi.

1. In modalità `Edit`, selezionate il componente sulla pagina.
1. Per accedere alla finestra di dialogo di configurazione, annullare l&#39;ereditarietà selezionando l&#39;icona `link`.
Una volta annullata l&#39;ereditarietà, è possibile selezionare l&#39;icona di configurazione per aprire la finestra di dialogo di configurazione.

1. Una volta completata la configurazione, è necessario ripristinare l&#39;ereditarietà selezionando l&#39;icona `broken link`.

![configure-message-list](assets/configure-message-list.png)

#### Scheda di base {#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **Selezione servizio**

   (*Obbligatorio*) Impostare questo valore sulla proprietà **`serviceSelector.name`** dal [ AEM Communities Messaging Operations Service](/help/communities/messaging.md#messaging-operations-service).

* **Componi pagina**

   (*Obbligatorio*) La pagina da aprire quando un membro fa clic sul pulsante **`Reply`**. La pagina di destinazione deve contenere il modulo **Componi messaggio**.

* **Rispondi/Visualizza come risorsa**

   Se questa opzione è attivata, l&#39;URL di risposta e l&#39;URL di visualizzazione faranno riferimento a una risorsa. In caso contrario, i dati vengono passati come parametri di query nell&#39;URL.

* **Modulo di visualizzazione profilo**

   Il modulo del profilo da utilizzare per visualizzare il profilo dei mittenti.

* **Cartella Cestino**

   Se questa opzione è selezionata, questo componente Elenco messaggi visualizza solo i messaggi contrassegnati come eliminati (cestino).

* **Percorsi cartella**

   (*Obbligatorio*) Riferimento ai valori impostati per **inbox.path.name** e **sentitems.path.name** in [ AEM Communities Messaging Operations Service](/help/communities/messaging.md#messaging-operations-service). Durante la configurazione di un `Inbox`, aggiungere una voce utilizzando il valore di **inbox.path.name**. Durante la configurazione per un `Outbox`, aggiungere una voce utilizzando il valore di **sentitems.path.name**. Durante la configurazione per `Trash`, aggiungere due voci con entrambi i valori.

#### Scheda Visualizza {#display-tab}

![display-tab-message-list](assets/display-tab-message-list.png)

* **Contrassegna pulsante Lettura**

   Se questa opzione è selezionata, visualizza un pulsante `Read`che consente di contrassegnare un messaggio come letto.

* **Contrassegna pulsante Non letto**

   Se questa opzione è selezionata, visualizza un pulsante `Mark Unread` che consente di contrassegnare un messaggio come letto.

* **Pulsante Elimina**

   Se questa opzione è selezionata, visualizza un pulsante `Delete` che consente di contrassegnare un messaggio come letto. Duplica la funzionalità di eliminazione se è selezionata anche **`Message Options`**.

* **Opzioni messaggio**

   Se questa opzione è selezionata, visualizza i pulsanti **`Reply`**, **`Reply All`**, **`Forward`** e **`Delete`** che consentono di inviare o eliminare un messaggio. Duplica la funzionalità di eliminazione se è selezionata anche **`Delete Button`**.

* **Messaggi per pagina**

   Il numero specificato corrisponde al numero massimo di messaggi visualizzati per pagina in uno schema di impaginazione. Se non viene specificato alcun numero (lasciato vuoto), vengono visualizzati tutti i messaggi e non è prevista alcuna impaginazione.

* **Pattern per marca temporale**

   Specifica i pattern delle marche temporali per una o più lingue. Il valore predefinito è en, de, fr, it, es, ja, zh_CN, ko_KR.

* **Visualizza utente**

   Scegliere **`Sender`** o **`Recipients`** per determinare se visualizzare il mittente o i destinatari.

### Configura messaggio di composizione {#configure-compose-message}

Per modificare la configurazione della pagina dei messaggi di composizione, aprire il sito in [modalità di modifica dell&#39;autore](/help/communities/sites-console.md#authoring-site-content).

* In modalità `Preview`, selezionare il collegamento **Messages** per aprire la pagina di messaggi principale. Quindi fate clic sul pulsante Nuovo messaggio per aprire la pagina `Compose Message`.

* In modalità `Edit`, selezionate il componente principale nella pagina contenente il corpo del messaggio.
* Per accedere alla finestra di dialogo di configurazione, annullare l&#39;ereditarietà selezionando l&#39;icona `link`.
Una volta annullata l&#39;ereditarietà, è possibile selezionare l&#39;icona di configurazione per aprire la finestra di dialogo di configurazione.

* Una volta completata la configurazione, è necessario ripristinare l&#39;ereditarietà selezionando l&#39;icona `broken link`.

![config-compose-message](assets/config-compose-message.png)

#### Scheda di base {#basic-tab-1}

![basic-tab-compose](assets/basic-tab-compose.png)

* **URL di reindirizzamento**

   Inserite l’URL della pagina visualizzata dopo l’invio del messaggio. Esempio, `../messaging.html`.

* **Annulla URL**

   Inserite l&#39;URL della pagina visualizzata se il mittente annulla il messaggio. Esempio, `../messaging.html`.

* **Lunghezza massima per l&#39;oggetto del messaggio**

   Il numero massimo di caratteri consentiti nel campo Oggetto. Ad esempio, 500. Il valore predefinito non è alcun limite.

* **Lunghezza massima del corpo del messaggio**

   Il numero massimo di caratteri consentiti nel campo Contenuto. Ad esempio, 10000. Il valore predefinito non è alcun limite.

* **Selezione servizio**

   (*Obbligatorio*) Impostare questo valore sulla proprietà **`serviceSelector.name`** dal [ AEM Communities Messaging Operations Service](/help/communities/messaging.md#messaging-operations-service).

#### Scheda Visualizza {#display-tab-1}

![display-tab-compose](assets/display-tab-compose.png)

* **Mostra campo oggetto**

   Se questa opzione è selezionata, mostrare il campo `Subject` e abilitare l&#39;aggiunta di un oggetto al messaggio. Il valore predefinito non è selezionato.

* **Etichetta oggetto**

   Immettere il testo da visualizzare accanto al campo `Subject`. Il valore predefinito è `Subject`.

* **Mostra campo Allega file**

   Se questa opzione è selezionata, mostrare il campo `Attachment` e abilitare l&#39;aggiunta di allegati al messaggio. Il valore predefinito non è selezionato.

* **Etichetta Allega file**

   Immettere il testo da visualizzare accanto al campo `Attachment`. Il valore predefinito è **`Attach File`**.

* **Mostra campo contenuto**

   Se questa opzione è selezionata, mostrare il campo `Content` e abilitare l&#39;aggiunta di un corpo del messaggio. Il valore predefinito non è selezionato.

* **Etichetta contenuto**

   Immettere il testo da visualizzare accanto al campo `Content`. Il valore predefinito è **`Body`**.

* **Con editor Rich Text**

   Se questa opzione è selezionata, indica l&#39;utilizzo di una casella di testo Contenuto personalizzata con un proprio editor Rich Text. Il valore predefinito non è selezionato.

* **Pattern per marca temporale**

   Specifica i pattern delle marche temporali per una o più lingue. Il valore predefinito è en, de, fr, it, es, ja, zh_CN, ko_KR.

