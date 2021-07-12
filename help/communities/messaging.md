---
title: Configurare la messaggistica
seo-title: Configurazione della messaggistica
description: Messaggistica community
seo-description: Messaggistica community
uuid: 159dcf9d-7948-4a3d-9f51-a5b4d03e172b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 232a0ec1-8dfc-41ec-84cc-69f9db494ea0
docset: aem65
role: Admin
exl-id: ee94f093-fd14-49f2-9990-fbe853d924b1
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 1%

---

# Configurare la messaggistica {#configure-messaging}

## Panoramica {#overview}

La funzione di messaggistica di AEM Communities consente ai visitatori del sito (membri) che hanno effettuato l’accesso di inviare messaggi a un altro visitatore, accessibili al momento dell’accesso al sito.

La messaggistica è abilitata per un sito community selezionando una casella durante la [creazione di siti community](/help/communities/sites-console.md).

Questa pagina contiene informazioni sulla configurazione predefinita e sulle possibili regolazioni.

Per ulteriori informazioni per gli sviluppatori, consulta [Nozioni di base sulla messaggistica](/help/communities/essentials-messaging.md).

## Servizio operazioni di messaggistica {#messaging-operations-service}

La configurazione [AEM Communities Messaging Operations Service](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl) identifica l&#39;endpoint che gestisce le richieste relative alla messaggistica, le cartelle che il servizio deve utilizzare per la memorizzazione dei messaggi e, se i messaggi possono includere allegati di file, quali tipi di file sono consentiti.

Per i siti della community creati utilizzando `Communities Sites console`, esiste già un’istanza del servizio, con la casella in entrata impostata su `/mail/inbox`.

### Servizio per le operazioni di messaggistica comunitaria {#community-messaging-operations-service}

Come mostrato di seguito, esiste una configurazione del servizio per i siti creati con la [creazione guidata sito](/help/communities/sites-console.md). Per visualizzare o modificare la configurazione, seleziona l’icona a forma di matita accanto alla configurazione.

![operazioni di messaggistica](assets/messaging-operations.png)

### Aggiungi nuova configurazione {#add-new-configuration}

Per aggiungere una nuova configurazione, seleziona l’icona più &quot;**+**&quot; accanto al nome del servizio :

* **Inserire nell&#39;elenco Consentiti campi messaggio**

   Specifica le proprietà del componente Componi messaggio che gli utenti possono modificare e mantenere. Se vengono aggiunti nuovi elementi modulo, se lo desideri, devi aggiungere l’ID elemento per essere memorizzato nell’SRP. Il valore predefinito è due voci: *oggetto* e *contenuto*.

* **Limite dimensione casella messaggio**

   Il numero massimo di byte nella finestra di messaggio di ogni utente. Il valore predefinito è *1073741824* (1 GB).

* **Limite del conteggio dei messaggi**

   Numero totale di messaggi consentiti per utente. Il valore -1 indica un numero illimitato di messaggi consentiti, in base al limite di dimensioni della finestra dei messaggi. Il valore predefinito è *10000* (10k).

* **Notifica errore di consegna**

   Se questa opzione è selezionata, invia una notifica al mittente se la consegna del messaggio non riesce ad alcuni destinatari. Il valore predefinito è *selezionato*.

* **ID mittente della consegna non riuscita**

   Nome del mittente visualizzato nel messaggio di consegna non riuscita. Il valore predefinito è *failedNotifier*.

* **Percorso modello messaggio di errore**

   Percorso assoluto della directory principale del modello di messaggio non riuscito di consegna. Il valore predefinito è */etc/notification/messaging/default*.

* **Numero di tentativi**

   Numero di volte in cui è possibile provare a inviare nuovamente il messaggio che non è stato recapitato. Il valore predefinito è *3*.

* **Attendi tra tentativi**

   Numero di secondi di attesa tra i tentativi di reinvio del messaggio in caso di invio non riuscito. Il valore predefinito è *100* (secondi).

* **Conta dimensioni pool di aggiornamenti**

   Numero di thread simultanei utilizzati per l&#39;aggiornamento del conteggio. Il valore predefinito è *10*.

* **Percorso casella in entrata**

   (*Obbligatorio*) Il percorso relativo al nodo dell&#39;utente (/home/users/*username*) da utilizzare per la cartella `inbox`. Il percorso NON deve terminare con una barra finale &#39;/&#39;. Il valore predefinito è */mail/inbox*.

* **Percorso elementi inviati**

   (*Obbligatorio*) Il percorso relativo al nodo dell&#39;utente (/home/users/*username*) da utilizzare per la cartella `sent items`. Il percorso NON deve terminare con una barra finale &#39;/&#39;. Il valore predefinito è */mail/sentitems* .

* **Allegati di supporto**

   Se questa opzione è selezionata, gli utenti possono aggiungere allegati ai messaggi. Il valore predefinito è *selezionato*.

* **Abilitare i messaggi di gruppo**

   Se selezionato, gli utenti registrati possono inviare messaggi in blocco a un gruppo di membri. Il valore predefinito è *deselezionato*.

* **N. massimo dei destinatari totali**

   Se la messaggistica di gruppo è abilitata, specifica il numero massimo di destinatari a cui è possibile inviare il messaggio di gruppo alla volta. Il valore predefinito è *100*.

* **Dimensione batch**

   Numero di messaggi da raggruppare per un invio quando si invia a un gruppo di destinatari di grandi dimensioni. Il valore predefinito è *100*.

* **Dimensione totale attacco**

   Se supportAttachments è selezionato, questo valore specifica la dimensione totale massima consentita (in byte) di tutti gli allegati. Il valore predefinito è *104857600* (100 MB).

* **Tipo di allegato inserii nell&#39;elenco Bloccati**

   Un inserire nell&#39;elenco Bloccati di estensioni del nome file, con prefisso &quot;**.**&quot;, che sarà respinto dal sistema. Se non inserire nell&#39;elenco Bloccati, l&#39;estensione è consentita. Le estensioni possono essere aggiunte o rimosse utilizzando le icone &#39;**+**&#39; e &#39;**-**&#39;.

* **Tipi di allegati consentiti**

   **(*Azione richiesta*)** Un inserì nell&#39;elenco Consentiti di estensioni di nome file, in corrispondenza dell’inserire nell&#39;elenco Bloccati. Per consentire tutte le estensioni del nome file, ad eccezione di quelle inserire nell&#39;elenco Bloccati, utilizza l&#39;icona &quot;**-**&quot; per rimuovere la singola voce vuota.

* **Selezione servizio**

   (*Obbligatorio*) Un percorso assoluto (endpoint) attraverso il quale viene chiamato il servizio (una risorsa virtuale). La radice del percorso scelto deve essere inclusa nell&#39;impostazione di configurazione *Percorsi di esecuzione* della configurazione OSGi [ `Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver), ad esempio `/bin/`, `/apps/` e `/services/`. Per selezionare questa configurazione per la funzione di messaggistica di un sito, questo endpoint viene fornito come valore **`Service selector`** per `Message List and Compose Message components` (consulta [Funzionalità messaggio](/help/communities/configure-messaging.md)).

   Il valore predefinito è */bin/messaging* .

* **Inserire nell&#39;elenco Consentiti campo**

   Utilizza **Inserire nell&#39;elenco Consentiti campi messaggio**.

>[!CAUTION]
>
>Ogni volta che viene aperta una configurazione `Messaging Operations Service` per la modifica, se `allowedAttachmentTypes.name` è stato rimosso, viene aggiunta nuovamente una voce vuota per rendere la proprietà configurabile. Una singola voce vuota disattiva efficacemente gli allegati di file.
>
>Per consentire tutte le estensioni del nome file, ad eccezione di quelle inserire nell&#39;elenco Bloccati, utilizza l&#39;icona &quot;**-**&quot; per (di nuovo) rimuovere la singola voce vuota prima di fare clic su **Salva**.

## Messaggistica di gruppo {#group-messaging}

Per consentire agli utenti registrati di inviare messaggi diretti in blocco a gruppi di utenti, assicurati di **abilitare i messaggi di gruppo** nelle due istanze seguenti della configurazione **Messaging Operation Services**:

* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console`
* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-messaging`

**Servizio operazioni di messaggistica: console social**

![social-console-op-service](assets/social-console-op-service.png)

**Servizio operazioni di messaggistica: messaggi social**

![social-message-op-service](assets/social-message-op-service.png)

## Risoluzione dei problemi {#troubleshooting}

Un modo per risolvere i problemi è quello di abilitare [il debug dei messaggi nel registro.](/help/sites-administering/troubleshooting.md)

Vedi anche [Loggers e Scrittori per servizi individuali](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services).

Il pacchetto da monitorare è `com.adobe.cq.social.messaging`.
