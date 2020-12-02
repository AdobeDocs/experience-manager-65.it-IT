---
title: Configurare i messaggi
seo-title: Configurazione dei messaggi
description: Messaggi community
seo-description: Messaggi community
uuid: 159dcf9d-7948-4a3d-9f51-a5b4d03e172b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 232a0ec1-8dfc-41ec-84cc-69f9db494ea0
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 1%

---


# Configurare i messaggi {#configure-messaging}

## Panoramica {#overview}

La funzione di messaggistica di  AEM Communities consente ai visitatori del sito che hanno effettuato l’accesso (membri) di inviare messaggi a un altro utente accessibili una volta effettuato l’accesso al sito.

La messaggistica è abilitata per un sito community selezionando una casella durante la creazione del sito community [](/help/communities/sites-console.md).

Questa pagina contiene informazioni sulla configurazione predefinita e sulle possibili regolazioni.

Per ulteriori informazioni per gli sviluppatori, vedere [Messaging Essentials](/help/communities/essentials-messaging.md).

## Servizio operazioni di messaggistica {#messaging-operations-service}

La configurazione [ AEM Communities Messaging Operations Service](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl) identifica l&#39;endpoint che gestisce le richieste correlate ai messaggi, le cartelle che il servizio deve utilizzare per memorizzare i messaggi e, se i messaggi possono includere allegati, quali tipi di file sono consentiti.

Per i siti della community creati utilizzando `Communities Sites console`, esiste già un&#39;istanza del servizio, con la inbox impostata su `/mail/inbox`.

### Servizio Operazioni messaggistica community {#community-messaging-operations-service}

Come mostrato di seguito, esiste una configurazione del servizio per i siti creati con la [creazione guidata sito](/help/communities/sites-console.md). Per visualizzare o modificare la configurazione, fai clic sull’icona matita accanto alla configurazione.

![messaggistica-operazioni](assets/messaging-operations.png)

### Aggiungi nuova configurazione {#add-new-configuration}

Per aggiungere una nuova configurazione, selezionate l&#39;icona più &quot;**+**&quot; accanto al nome del servizio:

* **Campi  messaggio Inserì nell&#39;elenco Consentiti**

   Specifica le proprietà del componente Componi messaggio che gli utenti possono modificare e mantenere. Se vengono aggiunti nuovi elementi modulo, l&#39;ID elemento dovrà essere aggiunto se lo si desidera per essere memorizzato nell&#39;SRP. Il valore predefinito è due voci: *subject* e *content*.

* **Limite dimensione casella messaggio**

   Il numero massimo di byte nella finestra di messaggio di ogni utente. Il valore predefinito è *1073741824* (1 GB).

* **Limite conteggio messaggi**

   Numero totale di messaggi consentiti per utente. Un valore pari a -1 indica che è consentito un numero illimitato di messaggi, in base al limite delle dimensioni delle finestre di messaggio. Il valore predefinito è *10000* (10k).

* **Notifica errore di consegna**

   Se questa opzione è selezionata, avvisa il mittente se la consegna del messaggio non riesce ad alcuni destinatari. Il valore predefinito è *selezionato*.

* **ID mittente consegna non riuscita**

   Nome del mittente visualizzato nel messaggio di consegna non riuscita. Il valore predefinito è *failureNotifier*.

* **Percorso modello messaggio di errore**

   Percorso assoluto della directory principale del modello di messaggio di consegna non riuscita. Il valore predefinito è */etc/notification/messaging/default*.

* **Numero di tentativi**

   Numero di volte per cui provare a inviare nuovamente il messaggio che non viene recapitato. Il valore predefinito è *3*.

* **Attendi tra i tentativi**

   Numero di secondi di attesa tra i tentativi di reinvio del messaggio in caso di mancata invio. Il valore predefinito è *100* (secondi).

* **Conteggio dimensioni pool di aggiornamento**

   Numero di thread simultanei utilizzati per l&#39;aggiornamento del conteggio. Il valore predefinito è *10*.

* **Percorso Inbox**

   (*Obbligatorio*) Il percorso, relativo al nodo dell&#39;utente (/home/users/*username*), da utilizzare per la cartella `inbox`. Il percorso NON deve terminare con una barra finale &#39;/&#39;. Il valore predefinito è */mail/inbox*.

* **Percorso elementi inviati**

   (*Obbligatorio*) Il percorso, relativo al nodo dell&#39;utente (/home/users/*username*), da utilizzare per la cartella `sent items`. Il percorso NON deve terminare con una barra finale &#39;/&#39;. Il valore predefinito è */mail/sentitems*.

* **Allegati di supporto**

   Se questa opzione è selezionata, gli utenti possono aggiungere allegati ai messaggi. Il valore predefinito è *selezionato*.

* **Abilitare i messaggi di gruppo**

   Se selezionato, gli utenti registrati possono inviare un messaggio in blocco a un gruppo di membri. Il valore predefinito è *deselezionato*.

* **N. massimo dei destinatari totali**

   Se la messaggistica del gruppo è abilitata, specifica il numero massimo di destinatari ai quali è possibile inviare il messaggio del gruppo alla volta. Il valore predefinito è *100*.

* **Dimensione batch**

   Numero di messaggi da raggruppare in batch per un&#39;invio a un gruppo esteso di destinatari. Il valore predefinito è *100*.

* **Dimensione totale attacco**

   Se supportAttachments è selezionato, questo valore specifica la dimensione totale massima consentita (in byte) di tutti gli allegati. Il valore predefinito è *104857600* (100 MB).

* **Tipo di allegato  inserii nell&#39;elenco Bloccati**

   Un  inserire nell&#39;elenco Bloccati di estensioni del nome file, con il prefisso &quot;**.**&quot;, che verrà rifiutato dal sistema. Se non  inserire nell&#39;elenco Bloccati, l&#39;estensione è consentita. Le estensioni possono essere aggiunte o rimosse utilizzando le icone &#39;**+**&#39; e &#39;**-**&#39;.

* **Tipi di allegati consentiti**

   **(*Azione richiesta*)** Un  inserì nell&#39;elenco Consentiti di estensioni di nomi file, l&#39;opposto del inserire nell&#39;elenco Bloccati . Per consentire tutte le estensioni del nome file, ad eccezione di quelle  inserire nell&#39;elenco Bloccati, utilizzate l&#39;icona &quot;**-**&quot; per rimuovere la singola voce vuota.

* **Selezione servizio**

   (*Obbligatorio*) Un percorso assoluto (endpoint) attraverso il quale viene chiamato il servizio (una risorsa virtuale). La radice del percorso scelto deve essere inclusa nell&#39;impostazione di configurazione *Percorsi di esecuzione* della configurazione OSGi [ `Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver), ad esempio `/bin/`, `/apps/` e `/services/`. Per selezionare questa configurazione per la funzione di messaggistica di un sito, questo endpoint viene fornito come il valore **`Service selector`** per la `Message List and Compose Message components` (vedere [Funzione messaggio](/help/communities/configure-messaging.md)).

   Il valore predefinito è */bin/messaging* .

* **campo Inserì nell&#39;elenco Consentiti**

   Utilizzare i campi messaggio **Inserì nell&#39;elenco Consentiti**.

>[!CAUTION]
>
>Ogni volta che si apre una configurazione `Messaging Operations Service` per la modifica, se `allowedAttachmentTypes.name` è stato rimosso, viene aggiunta una voce vuota per rendere la proprietà configurabile. Una singola voce vuota disattiva efficacemente gli allegati.
>
>Per consentire tutte le estensioni del nome file, ad eccezione di quelle  inserire nell&#39;elenco Bloccati, utilizzare l&#39;icona &quot;**-**&quot; per (di nuovo) rimuovere la singola voce vuota prima di fare clic su **Salva**.

## Messaggi di gruppo {#group-messaging}

Per consentire agli utenti registrati di inviare messaggi diretti in massa a gruppi di utenti, assicurarsi di **Abilitare i messaggi di gruppo** nelle due seguenti istanze della configurazione **Messaging Operation Services**:

* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console`
* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-messaging`

**Servizio Operazioni di messaggistica: console sociale**

![social-console-op-service](assets/social-console-op-service.png)

**Servizio Operazioni di messaggistica: messaggio social**

![social-message-op-service](assets/social-message-op-service.png)

## Risoluzione dei problemi {#troubleshooting}

Un modo per risolvere i problemi consiste nell&#39;abilitare [il debug dei messaggi nel registro.](/help/sites-administering/troubleshooting.md)

Vedere anche [Registratori e scrittori per servizi individuali](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services).

Il pacchetto da monitorare è `com.adobe.cq.social.messaging`.
