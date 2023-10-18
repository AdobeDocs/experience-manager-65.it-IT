---
title: Configurare la messaggistica
description: Scopri la funzione di messaggistica di AEM Communities che consente ai visitatori del sito (membri) che hanno effettuato l’accesso di inviarsi messaggi reciprocamente.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: ee94f093-fd14-49f2-9990-fbe853d924b1
source-git-commit: 00b6f2f03470aca7f87717818d0dfcd17ac16bed
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 1%

---

# Configurare la messaggistica {#configure-messaging}

## Panoramica {#overview}

La funzione di messaggistica di AEM Communities consente ai visitatori del sito (membri) che hanno effettuato l&#39;accesso di inviare messaggi reciprocamente accessibili quando hanno effettuato l&#39;accesso al sito.

La messaggistica è abilitata per un sito community selezionando una casella durante [creazione di siti community](/help/communities/sites-console.md).

Questa pagina contiene informazioni sulla configurazione predefinita e sulle possibili regolazioni.

Per ulteriori informazioni per gli sviluppatori, vedi [Nozioni di base sulla messaggistica](/help/communities/essentials-messaging.md).

## Servizio operazioni di messaggistica {#messaging-operations-service}

La configurazione [Servizio operazioni di messaggistica di AEM Communities](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl) identifica l’endpoint che gestisce le richieste relative alla messaggistica, le cartelle che il servizio deve utilizzare per archiviare i messaggi e, se i messaggi possono includere allegati, quali tipi di file sono consentiti.

Per i siti community creati utilizzando `Communities Sites console`, esiste un’istanza del servizio, con la casella in entrata impostata su `/mail/inbox`.

### Servizio operazioni di messaggistica per community {#community-messaging-operations-service}

Come mostrato di seguito, esiste una configurazione del servizio per i siti creati con [creazione guidata sito](/help/communities/sites-console.md). Per visualizzare o modificare la configurazione, seleziona l’icona a forma di matita accanto alla configurazione.

![messaggistica-operazioni](assets/messaging-operations.png)

### Aggiungi nuova configurazione {#add-new-configuration}

Per aggiungere una configurazione, seleziona il segno più &quot;**+** Icona &#39; accanto al nome del servizio:

* **Inserire nell&#39;elenco Consentiti Campi messaggio in fase di**

  Specifica le proprietà del componente Componi messaggio che gli utenti possono modificare e mantenere. Se vengono aggiunti nuovi elementi modulo, è necessario aggiungere l’ID elemento se si desidera memorizzarlo in SRP. Il valore predefinito è due voci: *oggetto* e *contenuto*.

* **Limite dimensioni casella messaggi**

  Numero massimo di byte nella finestra di messaggio di ogni utente. Il valore predefinito è *1073741824* (1 GB)

* **Limite di conteggio messaggi**

  Numero totale di messaggi consentiti per utente. Il valore -1 indica che è consentito un numero illimitato di messaggi, soggetto al limite di dimensioni della finestra di messaggio. Il valore predefinito è *10000* (10 duodecies)

* **Notifica consegna non riuscita**

  Se questa opzione è selezionata, avvisa il mittente se la consegna del messaggio non riesce ad alcuni destinatari. Il valore predefinito è *selezionato*.

* **ID mittente consegna non riuscita**

  Nome del mittente visualizzato nel messaggio di consegna non riuscita. Il valore predefinito è *failureNotifier*.

* **Percorso modello messaggio di errore**

  Percorso assoluto della directory principale del modello del messaggio di consegna non riuscita. Il valore predefinito è */etc/notification/messaging/default*.

* **N. di nuovi tentativi**

  Numero di tentativi di reinvio di un messaggio non recapitato. Il valore predefinito è *3*.

* **Attesa tra nuovi tentativi**

  Numero di secondi di attesa tra i tentativi di reinvio del messaggio in caso di errore di invio. Il valore predefinito è *100* (secondi).

* **Conta dimensioni pool di aggiornamento**

  Numero di thread simultanei utilizzati per l’aggiornamento del conteggio. Il valore predefinito è *10*.

* **Percorso casella in entrata**

  (*Obbligatorio*) Il percorso, relativo al nodo dell&#39;utente (/home/users/*nome utente*), da utilizzare per `inbox` cartella. Il percorso NON deve terminare con una barra finale &#39;/&#39;. Il valore predefinito è */mail/inbox*.

* **Percorso elementi inviati**

  (*Obbligatorio*) Il percorso, relativo al nodo dell&#39;utente (/home/users/*nome utente*), da utilizzare per `sent items` cartella. Il percorso NON deve terminare con una barra finale &#39;/&#39;. Il valore predefinito è */mail/sentitems* .

* **Allegati di supporto**

  Se questa opzione è selezionata, gli utenti possono aggiungere allegati ai loro messaggi. Il valore predefinito è *selezionato*.

* **Abilita messaggi di gruppo**

  Se questa opzione è selezionata, gli utenti registrati possono inviare messaggi in blocco a un gruppo di membri. Il valore predefinito è *deselezionato*.

* **N. massimo del totale dei destinatari**

  Se la messaggistica di gruppo è abilitata, specifica il numero massimo di destinatari a cui è possibile inviare un messaggio di gruppo alla volta. Il valore predefinito è *100*.

* **Dimensione batch**

  Numero di messaggi da raggruppare per un invio quando l’invio viene effettuato a un ampio gruppo di destinatari. Il valore predefinito è *100*.

* **Dimensione totale allegato**

  Se supportAttachments è selezionato, questo valore specifica la dimensione totale massima consentita (in byte) di tutti gli allegati. Il valore predefinito è *104857600* (100 MB)

* **Inserisco nell&#39;elenco Bloccati di tipo di allegato**

  Una inserisce nell&#39;elenco Bloccati di estensione di nome file con il prefisso &#39;.**.**&quot;, rifiutato dal sistema. Se non è inserita nell&#39;elenco Bloccati, allora l’estensione è consentita. Le estensioni possono essere aggiunte o rimosse utilizzando &quot;**+**&#39; e &#39;**-**&quot;.

* **Tipi di allegati consentiti**

  **(*Azione richiesta*)** Una inserisce nell&#39;elenco Consentiti di estensione di nome file di, opposta a quella del inserisco nell&#39;elenco Bloccati. Inserire nell&#39;elenco Bloccati Per consentire tutte le estensioni del nome file, ad eccezione di quelle, utilizzare il tasto &#39;**-**&#39; per rimuovere la singola voce vuota.

* **Selezione servizio**

  (*Obbligatorio*) Percorso assoluto (endpoint) attraverso il quale viene chiamato il servizio (risorsa virtuale). La directory principale del percorso scelto deve essere inclusa in *Percorsi di esecuzione* configurazione della configurazione OSGi [`Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver), ad esempio `/bin/`, `/apps/`, e `/services/`. Per selezionare questa configurazione per la funzione di messaggistica di un sito, questo endpoint viene fornito come **`Service selector`** valore per `Message List and Compose Message components` (vedere [Funzione Messaggio](/help/communities/configure-messaging.md)).

  Il valore predefinito è */bin/messaging* .

* **Inserire nell&#39;elenco Consentiti Campo**

  Utilizzare **Inserire nell&#39;elenco Consentiti Campi messaggio in fase di**.

>[!CAUTION]
>
>Ogni volta che un `Messaging Operations Service` la configurazione viene aperta per la modifica, se `allowedAttachmentTypes.name` è stata rimossa, viene letta una voce vuota per rendere configurabile la proprietà. Una singola voce vuota disattiva efficacemente gli allegati.
>
>Inserire nell&#39;elenco Bloccati Per consentire tutte le estensioni del nome file, ad eccezione di quelle, utilizzare il tasto &#39;**-**&#39; per rimuovere (di nuovo) la singola voce vuota prima di fare clic su **Salva**.

## Messaggistica di gruppo {#group-messaging}

Per consentire agli utenti registrati di inviare messaggi diretti in blocco a gruppi di utenti, assicurati di: **Abilita messaggi di gruppo** nelle seguenti due istanze di **Servizi operazioni di messaggistica** configurazione:

* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console`
* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-messaging`

**Servizio operazioni di messaggistica: console social**

![social-console-op-service](assets/social-console-op-service.png)

**Servizio operazioni di messaggistica: messaggistica social**

![social-message-op-service](assets/social-message-op-service.png)

## Risoluzione dei problemi {#troubleshooting}

Un modo per risolvere i problemi consiste nell&#39;abilitare [debug dei messaggi nel registro.](/help/sites-administering/troubleshooting.md)

Vedi anche [Logger e writer per singoli servizi](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services).

Il pacchetto da monitorare è `com.adobe.cq.social.messaging`.
