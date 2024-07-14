---
title: Funzione di messaggistica
description: Scopri come configurare la funzione Messaggistica di AEM Communities per consentire ai membri della community di interagire tra loro in modo più privato.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: d121dc05-7d15-44ba-8d2d-b59d6c6480c8
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 0%

---

# Funzione di messaggistica {#messaging-feature}

Oltre alle interazioni pubblicamente visibili che si verificano nei forum e nei commenti, la funzione di messaggistica di AEM Communities consente ai membri della community di interagire tra loro in modo più privato.

Questa funzionalità può essere inclusa durante la creazione di un [sito community](/help/communities/overview.md#communitiessites).

La funzione di messaggistica consente di effettuare le seguenti operazioni:

**A** - invia un messaggio a uno o più membri della community

**B** - invia messaggi diretti in [blocco ai gruppi membri della community](/help/communities/messaging.md#group-messaging)

**C** - invia un messaggio con allegati

**D** - inoltra un messaggio

**E** - risponde a un messaggio

**F** - elimina un messaggio

**G** - ripristina un messaggio eliminato

![sezione di messaggistica](assets/messaging-section.png)

![messaggio-ripristino](assets/restore-message.png)

Per abilitare e modificare la funzione di messaggistica, consulta:

* [Configurare la messaggistica](/help/communities/messaging.md) per gli amministratori
* [Messaging Essentials](/help/communities/essentials-messaging.md) per sviluppatori

>[!NOTE]
>
>Non è supportato aggiungere `Compose Message, Message, or Message List` componenti (presenti nel gruppo di componenti `Communities`) a una pagina in modalità di modifica dell&#39;autore.

## Configurare i componenti di messaggistica {#configure-messaging-components}

Quando la messaggistica è abilitata per un sito community, non è necessario configurarla ulteriormente. Le informazioni vengono fornite se è necessario modificare la configurazione predefinita.

### Configura elenco messaggi (finestra di messaggio) {#configure-message-list-message-box}

Per modificare la configurazione dell&#39;elenco dei messaggi per **Posta in arrivo**, **Elementi inviati** e **Cestino** pagine della funzionalità di messaggistica, aprire il sito in [modalità modifica autore](/help/communities/sites-console.md#authoring-site-content).

1. In modalità `Preview`, seleziona il collegamento **Messaggi** per aprire la pagina di messaggistica principale. Quindi seleziona **Posta in arrivo**, **Elementi inviati** o **Cestino** per configurare il componente per l&#39;elenco dei messaggi.

1. In modalità `Edit`, selezionare il componente nella pagina.
1. Per accedere alla finestra di dialogo di configurazione, annullare l&#39;ereditarietà selezionando l&#39;icona `link`.
Una volta annullata l’ereditarietà, è possibile selezionare l’icona di configurazione per aprire la finestra di dialogo di configurazione.

1. Una volta completata la configurazione, è necessario ripristinare l&#39;ereditarietà selezionando l&#39;icona `broken link`.

![configure-message-list](assets/configure-message-list.png)

#### Scheda Base {#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **Selettore servizio**

  (*Obbligatorio*) Impostare questo valore sul valore della proprietà **`serviceSelector.name`** del [Servizio operazioni di messaggistica di AEM Communities](/help/communities/messaging.md#messaging-operations-service).

* **Componi pagina**

  (*Obbligatorio*) Pagina da aprire quando un membro fa clic sul pulsante **`Reply`**. La pagina di destinazione deve contenere il modulo **Componi messaggio**.

* **Rispondi/Visualizza come risorsa**

  Se questa opzione è selezionata, l’URL di risposta e l’URL di visualizzazione fanno riferimento a una risorsa, altrimenti i dati vengono trasmessi come parametri di query nell’URL.

* **Modulo visualizzazione profilo**

  Modulo di profilo da utilizzare per visualizzare il profilo mittenti.

* **Cartella cestino**

  Se questa opzione è selezionata, in questo componente Elenco messaggi vengono visualizzati solo i messaggi contrassegnati come eliminati (cestino).

* **Percorsi cartella**

  (*Obbligatorio*) Riferimento ai valori impostati per **inbox.path.name** e **sentitems.path.name** nel [Servizio operazioni di messaggistica AEM Communities](/help/communities/messaging.md#messaging-operations-service). Durante la configurazione per un `Inbox`, aggiungi una voce utilizzando il valore di **inbox.path.name**. Durante la configurazione per un `Outbox`, aggiungi una voce utilizzando il valore di **sentitems.path.name**. Durante la configurazione per `Trash`, aggiungere due voci con entrambi i valori.

#### Scheda Visualizzazione {#display-tab}

![display-tab-message-list](assets/display-tab-message-list.png)

* **Contrassegna pulsante di lettura**

  Se questa opzione è selezionata, visualizza un pulsante `Read` che consente di contrassegnare un messaggio come letto.

* **Pulsante Contrassegna come da leggere**

  Se questa opzione è selezionata, visualizza un pulsante `Mark Unread` che consente di contrassegnare un messaggio come letto.

* **Pulsante Elimina**

  Se questa opzione è selezionata, visualizza un pulsante `Delete` che consente di contrassegnare un messaggio come letto. Duplica la funzionalità di eliminazione se è selezionato anche **`Message Options`**.

* **Opzioni messaggio**

  Se questa opzione è selezionata, vengono visualizzati i pulsanti **`Reply`**, **`Reply All`**, **`Forward`** e **`Delete`** che consentono di inviare o eliminare nuovamente un messaggio. Duplica la funzionalità di eliminazione se è selezionato anche **`Delete Button`**.

* **Messaggi Per Pagina**

  Il numero specificato è il numero massimo di messaggi visualizzati per pagina in uno schema di impaginazione. Se non viene specificato alcun numero (lasciato vuoto), vengono visualizzati tutti i messaggi e non è presente alcuna impaginazione.

* **Modelli di marca temporale**

  Fornisci modelli di marca temporale per una o più lingue. Il valore predefinito è en, de, fr, it, es, ja, zh_CN, ko_KR.

* **Utente visualizzato**

  Scegliere **`Sender`** o **`Recipients`** per determinare se visualizzare il mittente o i destinatari.

### Configura messaggio di composizione {#configure-compose-message}

Per modificare la configurazione della pagina del messaggio di composizione, aprire il sito in [modalità modifica autore](/help/communities/sites-console.md#authoring-site-content).

* In modalità `Preview`, seleziona il collegamento **Messaggi** per aprire la pagina di messaggistica principale. Quindi selezionare il pulsante Nuovo messaggio per aprire la pagina `Compose Message`.

* In modalità `Edit`, selezionare il componente principale nella pagina contenente il corpo del messaggio.
* Per accedere alla finestra di dialogo di configurazione, annullare l&#39;ereditarietà selezionando l&#39;icona `link`.
Una volta annullata l’ereditarietà, è possibile selezionare l’icona di configurazione per aprire la finestra di dialogo di configurazione.

* Una volta completata la configurazione, è necessario ripristinare l&#39;ereditarietà selezionando l&#39;icona `broken link`.

![config-compose-message](assets/config-compose-message.png)

#### Scheda Base {#basic-tab-1}

![base-scheda-composizione](assets/basic-tab-compose.png)

* **URL di reindirizzamento**

  Immetti l’URL della pagina visualizzata dopo l’invio del messaggio. Esempio: `../messaging.html`.

* **Annulla URL**

  Inserisci l’URL della pagina visualizzata se il mittente annulla il messaggio. Esempio: `../messaging.html`.

* **Lunghezza massima dell&#39;oggetto del messaggio**

  Numero massimo di caratteri consentito nel campo Oggetto. Ad esempio, 500. Il valore predefinito non è un limite.

* **Lunghezza massima del corpo del messaggio**

  Numero massimo di caratteri consentito nel campo Contenuto. Ad esempio, 10000. Il valore predefinito non è un limite.

* **Selettore servizio**

  (*Obbligatorio*) Impostare questo valore sul valore della proprietà **`serviceSelector.name`** del [Servizio operazioni di messaggistica di AEM Communities](/help/communities/messaging.md#messaging-operations-service).

#### Scheda Visualizzazione {#display-tab-1}

![display-tab-compose](assets/display-tab-compose.png)

* **Mostra campo soggetto**

  Se questa opzione è selezionata, mostra il campo `Subject` e abilita l&#39;aggiunta di un oggetto al messaggio. Il valore predefinito non è selezionato.

* **Etichetta oggetto**

  Immettere il testo da visualizzare accanto al campo `Subject`. Il valore predefinito è `Subject`.

* **Mostra campo Allega file**

  Se questa opzione è selezionata, mostrare il campo `Attachment` e abilitare l&#39;aggiunta di allegati al messaggio. Il valore predefinito non è selezionato.

* **Allega etichetta file**

  Immettere il testo da visualizzare accanto al campo `Attachment`. Il valore predefinito è **`Attach File`**.

* **Mostra campo contenuto**

  Se questa opzione è selezionata, mostra il campo `Content` e abilita l&#39;aggiunta del corpo di un messaggio. Il valore predefinito non è selezionato.

* **Etichetta contenuto**

  Immettere il testo da visualizzare accanto al campo `Content`. Il valore predefinito è **`Body`**.

* **Con Editor Rich Text**

  Se questa opzione è selezionata, indica l&#39;utilizzo di una casella di testo Contenuto personalizzata con il relativo editor Rich Text. Il valore predefinito non è selezionato.

* **Modelli di marca temporale**

  Fornisci modelli di marca temporale per una o più lingue. Il valore predefinito è en, de, fr, it, es, ja, zh_CN, ko_KR.
