---
title: Funzionalità di messaggistica
seo-title: Messaging Feature
description: Configurazione dei componenti di messaggistica
seo-description: Configuring Messaging components
uuid: 8b99ded1-aec2-40c9-82d5-e2e404f614ca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9d952604-f9ef-498f-937b-871817c80226
docset: aem65
exl-id: d121dc05-7d15-44ba-8d2d-b59d6c6480c8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 4%

---

# Funzionalità di messaggistica {#messaging-feature}

Oltre alle interazioni visibili al pubblico che si verificano nei forum e nei commenti, la funzione di messaggistica di AEM Communities consente ai membri della community di interagire più privatamente tra di loro.

Questa funzione può essere inclusa quando [sito della community](/help/communities/overview.md#communitiessites) viene creato.

La funzione di messaggistica consente di:

**A** - inviare un messaggio a uno o più membri della community

**B** - inviare messaggi diretti in [in blocco a gruppi membri della comunità](/help/communities/messaging.md#group-messaging)

**C** - inviare un messaggio con allegati

**D** - inoltro di un messaggio

**E** - risposta a un messaggio

**F** - Eliminare un messaggio

**G** - ripristinare un messaggio eliminato

![sezione messaggistica](assets/messaging-section.png)

![messaggio di ripristino](assets/restore-message.png)

Per abilitare e modificare la funzione di messaggistica, vedi:

* [Configurare la messaggistica](/help/communities/messaging.md) per amministratori
* [Nozioni di base sulla messaggistica](/help/communities/essentials-messaging.md) per sviluppatori

>[!NOTE]
>
>Non è supportato per aggiungere `Compose Message, Message, or Message List` componenti (disponibili in `Communities`gruppo di componenti) in una pagina in modalità di modifica dell’autore.

## Configurare i componenti di messaggistica {#configure-messaging-components}

Quando la messaggistica è abilitata per un sito community, non è necessaria alcuna ulteriore configurazione. Le informazioni vengono fornite se è necessario modificare la configurazione predefinita.

### Configura elenco messaggi (finestra messaggio) {#configure-message-list-message-box}

Per modificare la configurazione dell’elenco di messaggi per **Inbox**, **Elementi inviati** e **Cestino** pagine della funzione di messaggistica, apri il sito in [modalità modifica autore](/help/communities/sites-console.md#authoring-site-content).

1. In `Preview` seleziona la modalità **Messaggi** per aprire la pagina di messaggistica principale. Quindi seleziona uno **Inbox**, **Elementi inviati** o **Cestino** per configurare il componente per l’elenco dei messaggi.

1. In `Edit` , seleziona il componente nella pagina.
1. Per accedere alla finestra di dialogo di configurazione, annulla ereditarietà selezionando la `link` icona.
Una volta annullata l’ereditarietà, è possibile selezionare l’icona di configurazione per aprire la finestra di dialogo di configurazione.

1. Una volta completata la configurazione, è necessario ripristinare l’ereditarietà selezionando la `broken link` icona.

![configure-message-list](assets/configure-message-list.png)

#### Scheda Base {#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **Selezione servizio**

   (*Obbligatorio*) Impostalo sul valore della proprietà **`serviceSelector.name`** dal [Servizio AEM Communities Messaging Operations](/help/communities/messaging.md#messaging-operations-service).

* **Pagina Componi**

   (*Obbligatorio*) La pagina da aprire quando un membro fa clic sul pulsante **`Reply`** pulsante . La pagina di destinazione deve contenere **Componi messaggio** modulo.

* **Rispondi/visualizza come risorsa**

   Se questa opzione è selezionata, l’URL di risposta e l’URL di visualizzazione faranno riferimento a una risorsa; in caso contrario i dati vengono passati come parametri di query nell’URL.

* **Modulo di visualizzazione del profilo**

   Il modulo del profilo da utilizzare per visualizzare il profilo dei mittenti.

* **Cartella Cestino**

   Se questa opzione è selezionata, in questo componente Elenco messaggi vengono visualizzati solo i messaggi contrassegnati come eliminati (cestino).

* **Percorsi cartella**

   (*Obbligatorio*) Riferimento ai valori impostati per **inbox.path.name** e **sentitems.path.name** in [Servizio AEM Communities Messaging Operations](/help/communities/messaging.md#messaging-operations-service). Durante la configurazione di un `Inbox`, aggiungi una voce utilizzando il valore di **inbox.path.name**. Durante la configurazione di un `Outbox`, aggiungi una voce utilizzando il valore di **sentitems.path.name**. Per la configurazione di `Trash`, aggiungi due voci con entrambi i valori.

#### Scheda Visualizzazione {#display-tab}

![display-tab-message-list](assets/display-tab-message-list.png)

* **Contrassegna pulsante di lettura**

   Se questa opzione è selezionata, viene visualizzata una `Read`che consente di contrassegnare un messaggio come letto.

* **Pulsante Segna non letto**

   Se questa opzione è selezionata, viene visualizzata una `Mark Unread` che consente di contrassegnare un messaggio come letto.

* **Pulsante Elimina**

   Se questa opzione è selezionata, viene visualizzata una `Delete` che consente di contrassegnare un messaggio come letto. Duplica la funzionalità di eliminazione se **`Message Options`** è anche controllato.

* **Opzioni messaggio**

   Se questa opzione è selezionata, viene visualizzato **`Reply`**, **`Reply All`**, **`Forward`** e **`Delete`** pulsanti che consentono di inviare o eliminare un messaggio. Duplica la funzionalità di eliminazione se **`Delete Button`** è anche controllato.

* **Messaggi per pagina**

   Il numero specificato è il numero massimo di messaggi visualizzati per pagina in uno schema di impaginazione. Se non viene specificato alcun numero (lasciato vuoto), vengono visualizzati tutti i messaggi e non è presente alcuna impaginazione.

* **Pattern per marca temporale**

   Fornisci pattern di marca temporale per una o più lingue. Il valore predefinito è en, de, fr, it, es, ja, zh_CN, ko_KR.

* **Visualizza utente**

   Scegli una **`Sender`** o **`Recipients`** per determinare se visualizzare il mittente o i destinatari.

### Configura messaggio di composizione {#configure-compose-message}

Per modificare la configurazione della pagina del messaggio di composizione, apri il sito in [modalità modifica autore](/help/communities/sites-console.md#authoring-site-content).

* In `Preview` seleziona la modalità **Messaggi** per aprire la pagina di messaggistica principale. Quindi seleziona il pulsante Nuovo messaggio per aprire il `Compose Message` pagina.

* In `Edit` in , seleziona il componente principale nella pagina contenente il corpo del messaggio.
* Per accedere alla finestra di dialogo di configurazione, annulla ereditarietà selezionando la `link` icona.
Una volta annullata l’ereditarietà, è possibile selezionare l’icona di configurazione per aprire la finestra di dialogo di configurazione.

* Una volta completata la configurazione, è necessario ripristinare l’ereditarietà selezionando la `broken link` icona.

![config-compose-message](assets/config-compose-message.png)

#### Scheda Base {#basic-tab-1}

![basic-tab-compose](assets/basic-tab-compose.png)

* **URL di reindirizzamento**

   Immetti l’URL della pagina visualizzata dopo l’invio del messaggio. Esempio: `../messaging.html`.

* **Annulla URL**

   Immetti l’URL della pagina visualizzata se il mittente annulla il messaggio. Esempio: `../messaging.html`.

* **Lunghezza massima per l&#39;oggetto del messaggio**

   Numero massimo di caratteri consentiti nel campo Oggetto. Ad esempio, 500. Il valore predefinito non è un limite.

* **Lunghezza massima del corpo del messaggio**

   Il numero massimo di caratteri consentiti nel campo Contenuto. Ad esempio, 10000. Il valore predefinito non è un limite.

* **Selezione servizio**

   (*Obbligatorio*) Impostalo sul valore della proprietà **`serviceSelector.name`** dal [Servizio AEM Communities Messaging Operations](/help/communities/messaging.md#messaging-operations-service).

#### Scheda Visualizzazione {#display-tab-1}

![display-tab-compose](assets/display-tab-compose.png)

* **Mostra campo oggetto**

   Se questa opzione è selezionata, mostra la `Subject` e abilita l’aggiunta di un oggetto al messaggio. Il valore predefinito non è selezionato.

* **Etichetta oggetto**

   Immetti il testo da visualizzare accanto al `Subject` campo . Il valore predefinito è `Subject`.

* **Mostra campo Allega file**

   Se questa opzione è selezionata, mostra la `Attachment` e abilitare l&#39;aggiunta di allegati al messaggio. Il valore predefinito non è selezionato.

* **Etichetta Allega file**

   Immetti il testo da visualizzare accanto al `Attachment` campo . Il valore predefinito è **`Attach File`**.

* **Mostra campo contenuto**

   Se questa opzione è selezionata, mostra la `Content` e abilita l’aggiunta di un corpo del messaggio. Il valore predefinito non è selezionato.

* **Etichetta contenuto**

   Immetti il testo da visualizzare accanto al `Content` campo . Il valore predefinito è **`Body`**.

* **Con editor Rich Text**

   Se questa opzione è selezionata, indica l’utilizzo di una casella di testo Contenuto personalizzato con il proprio editor di testo RTF. Il valore predefinito non è selezionato.

* **Pattern per marca temporale**

   Fornisci pattern di marca temporale per una o più lingue. Il valore predefinito è en, de, fr, it, es, ja, zh_CN, ko_KR.
