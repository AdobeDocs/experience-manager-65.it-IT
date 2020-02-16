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
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Configurare i messaggi{#configure-messaging}

## Panoramica {#overview}

La funzione di messaggistica di AEM Communities consente ai visitatori del sito che hanno effettuato l&#39;accesso (membri) di inviare messaggi a un altro utente che sono accessibili dopo l&#39;accesso al sito.

La messaggistica è abilitata per un sito community selezionando una casella durante la creazione [del sito](/help/communities/sites-console.md)community.

Questa pagina contiene informazioni sulla configurazione predefinita e sulle possibili regolazioni.

Per ulteriori informazioni per gli sviluppatori, consulta [Messaging Essentials](/help/communities/essentials-messaging.md).

## Servizio Operazioni di messaggistica {#messaging-operations-service}

Il servizio [Operazioni messaggistica](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl) AEM Communities di configurazione identifica l&#39;endpoint che gestisce le richieste correlate ai messaggi, le cartelle che il servizio deve utilizzare per la memorizzazione dei messaggi e, se i messaggi possono includere allegati, quali tipi di file sono consentiti.

Per i siti della community creati utilizzando l&#39; `Communities Sites console`, esiste già un&#39;istanza del servizio, con la casella in entrata impostata su `/mail/inbox`.

### Servizio Operazioni di messaggistica community {#community-messaging-operations-service}

Come mostrato di seguito, esiste una configurazione del servizio per i siti creati con la procedura guidata [per la creazione del](/help/communities/sites-console.md)sito. Per visualizzare o modificare la configurazione, fai clic sull’icona matita accanto alla configurazione.

![messaggistica-operazioni](assets/messaging-operations.png)

### Aggiungi nuova configurazione {#add-new-configuration}

Per aggiungere una nuova configurazione, selezionate l&#39;icona più&#x200B;**+** accanto al nome del servizio:

* **Whitelist** Campi messaggio Specifica le proprietà del componente Componi messaggio che gli utenti possono modificare e mantenere. Se vengono aggiunti nuovi elementi modulo, l&#39;ID elemento dovrà essere aggiunto se lo si desidera per essere memorizzato nell&#39;SRP. Il valore predefinito è due voci: *oggetto* e *contenuto*.

* **Limite** dimensione casella messaggio Il numero massimo di byte nella finestra di messaggio di ogni utente. Il valore predefinito è *1073741824 *(1 GB).

* **Limite** conteggio messaggi Il numero totale di messaggi consentiti per utente. Un valore pari a -1 indica che è consentito un numero illimitato di messaggi, in base al limite delle dimensioni delle finestre di messaggio. Il valore predefinito è *10000* (10 k).

* **Notifica un errore** di consegna Se questa opzione è selezionata, avvisa il mittente se la consegna del messaggio non riesce ad alcuni destinatari. Il valore predefinito è *selezionato*.

* **ID** mittente di recapito non riuscito che viene visualizzato nel messaggio di consegna non riuscita. Il valore predefinito è *failureNotifier*.

* **Percorso** del modello di messaggio di errore Percorso assoluto del modello di messaggio di consegna non riuscita radice. Il valore predefinito è */etc/notification/messaging/default*.

* **Numero di tentativi** Numero di tentativi di reinvio del messaggio che non è stato recapitato. Default is *3*.

* **Attesa tra i tentativi** Numero di secondi di attesa tra i tentativi di reinvio del messaggio in caso di mancata invio. Il valore predefinito è *100 *(secondi).

* **Dimensione** pool di aggiornamento conteggio Numero di thread simultanei utilizzati per l&#39;aggiornamento del conteggio. Default is *10*.

* **Percorso** Casella in entrata (*obbligatorio*) Il percorso, relativo al nodo dell&#39;utente (home/users/*username*), da utilizzare per la **`inbox`** cartella. Il percorso NON deve terminare con una barra finale &#39;/&#39;. Il valore predefinito è */mail/inbox.*

* **Percorso** degli elementi inviati (*Obbligatorio*) Il percorso, relativo al nodo dell&#39;utente (home/users/*username*), da utilizzare per la **`send items`** cartella. Il percorso NON deve terminare con una barra finale &#39;/&#39;. Il valore predefinito è */mail/sentitems* .

* **Supporto di allegati** Se questa opzione è selezionata, gli utenti possono aggiungere allegati ai messaggi. Il valore predefinito è *selezionato*.

* **Abilita messaggi** di gruppo Se questa opzione è selezionata, gli utenti registrati possono inviare messaggi in blocco a un gruppo di membri. Il valore predefinito è *deselezionato*.

* **N. massimo dei destinatari** totali Se la messaggistica del gruppo è abilitata, specifica il numero massimo di destinatari ai quali il messaggio del gruppo può essere inviato contemporaneamente. Default is *100*.

* **Dimensione** batch Numero di messaggi da raggruppare in batch per un&#39;invio quando si invia a un gruppo di destinatari di grandi dimensioni. Default is *100*.

* **Dimensione** totale allegato Se supportAttachments è selezionato, questo valore specifica la dimensione totale massima consentita (in byte) di tutti gli allegati. Il valore predefinito è *104857600* (100 MB).

* **Tipo di allegato lista** nera Una lista nera di estensioni di nomi file, con il prefisso &#39;**.**&quot;, che verrà rifiutato dal sistema. Se non è presente in blacklist, l’estensione è consentita. Le estensioni possono essere aggiunte o rimosse utilizzando le icone &#39;**+**&#39; e &#39;**-**&#39;.

* **Tipi di allegati consentiti**
   **(*Action Required*)** Una whitelist di estensioni di nomi file, in corrispondenza dell&#39;opposto della blacklist. Per consentire tutte le estensioni di file, ad eccezione di quelle elencate in blacklist, utilizzate l&#39;icona **-** per rimuovere la singola voce vuota.

* **Selettore** di servizio (*obbligatorio*) Un percorso assoluto (endpoint) attraverso il quale viene chiamato il servizio (una risorsa virtuale). La radice del percorso scelto deve essere inclusa nell&#39;impostazione di configurazione *Percorsi* di esecuzione della configurazione OSGi [ , `Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver)ad esempio `/bin/`, `/apps/`e `/services/`. Per selezionare questa configurazione per la funzione di messaggistica di un sito, questo endpoint viene fornito come **`Service selector`** valore per la funzione `Message List and Compose Message components` (vedere Funzione [](/help/communities/configure-messaging.md)Messaggio).
Il valore predefinito è */bin/messaging* .

* **Whitelist** Use **Message Fields (Usa whitelist** campi messaggio).

>[!CAUTION]
>
>Ogni volta che una `Messaging Operations Service` configurazione viene aperta per la modifica, se `allowedAttachmentTypes.name` è stata rimossa, viene aggiunta una voce vuota per rendere la proprietà configurabile. Una singola voce vuota disattiva efficacemente gli allegati.
>
>Per consentire tutte le estensioni di file, ad eccezione di quelle elencate in blacklist, utilizzate l&#39;icona **-** per rimuovere (di nuovo) la singola voce vuota prima di fare clic su **Salva**.

## Group Messaging {#group-messaging}

Per consentire agli utenti registrati di inviare messaggi diretti in massa a gruppi di utenti, assicurarsi di **Enable group messaging **nelle due seguenti istanze della configurazione **Messaging Operation Services** :

* com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console
* com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~messaggi social

**Servizio Operazioni di messaggistica: console sociale**

![social-console-op-service](assets/social-console-op-service.png)

**Servizio Operazioni di messaggistica: messaggio social**

![social-message-op-service](assets/social-message-op-service.png)

## Risoluzione dei problemi {#troubleshooting}

Un modo per risolvere i problemi è attivare i messaggi di [debug nel registro.](/help/sites-administering/troubleshooting.md)

Vedi anche [Loggers e Scrittori per i Servizi](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services)individuali.

Il pacchetto da monitorare è `com.adobe.cq.social.messaging`.
