---
title: Risoluzione dei problemi di replica
seo-title: Risoluzione dei problemi di replica
description: Questo articolo fornisce informazioni su come risolvere i problemi di replica.
seo-description: Questo articolo fornisce informazioni su come risolvere i problemi di replica.
uuid: 1662bf60-b000-4eb2-8834-c6da607128fe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 0d055be7-7189-4587-8c7c-2ce34e22a6ad
docset: aem65
translation-type: tm+mt
source-git-commit: 38ef8fc8d80009c8ca79aca9e45cf10bd70e1f1e
workflow-type: tm+mt
source-wordcount: '1255'
ht-degree: 0%

---


# Risoluzione dei problemi relativi alla replica{#troubleshooting-replication}

Questa pagina fornisce informazioni su come risolvere i problemi di replica.

## Problema {#problem}

Replica (replica non inversa) non riuscita per qualche motivo.

## Risoluzione {#resolution}

Esistono diversi motivi per cui la replica non riesce. Questo articolo spiega l&#39;approccio che si potrebbe adottare nell&#39;analisi di questi problemi.

**Le repliche vengono attivate quando si fa clic sul pulsante Attiva? Se NON è necessario eseguire le operazioni seguenti:**

1. Andate a /crx/explorer e accedete come amministratore.
1. Apri &quot;Content Explorer&quot;
1. Verificare se esiste un nodo /bin/replication o /bin/replicate.json. Se il nodo esiste, eliminatelo e salvatelo.

**Le repliche vengono messe in coda nelle code dell&#39;agente di replica?**

Per verificare il problema, visitate /etc/replication/agents.author.html e fate clic sugli agenti di replica da controllare.

**Se una coda agente o alcune code agente si bloccano:**

1. La coda mostra lo stato **bloccato**? In caso affermativo, l’istanza di pubblicazione non è in esecuzione o non risponde completamente? Controllate l’istanza di pubblicazione per verificare i problemi riscontrati (ad esempio, controllate i registri e verificate se si è verificato un errore OutOfMemory o un altro problema). Poi se è solo in generale lento poi prendere i cespugli di fili e analizzarli.
1. Lo stato della coda mostra **La coda è attiva - # pending**? Il processo di replica potrebbe essere bloccato in una lettura socket in attesa della risposta dell&#39;istanza pubblica o del dispatcher. Ciò potrebbe significare che l’istanza di pubblicazione o il dispatcher sono sotto carico elevato o sono bloccati in un blocco. Eseguite la creazione di thread dumps dall’autore e la pubblicazione in questo caso.

   * Aprire i thread dumps dall&#39;autore in un analizzatore di dump del thread, verificare che il processo di sling dell&#39;agente di replica sia bloccato in un socketRead.
   * Aprite i thread dumps dalla pubblicazione in un analizzatore di dump del thread, analizzate cosa potrebbe causare la mancata risposta dell&#39;istanza di pubblicazione. Dovrebbe essere visualizzato un thread con il nome dell&#39;POST /bin/receive, ovvero il thread che riceve la replica dall&#39;autore.

**Se tutte le code dell&#39;agente sono bloccate**

1. È possibile che una determinata parte del contenuto non possa essere serializzata in /var/replica/data a causa di un problema di corruzione del repository o di un altro problema. Verificate la presenza di un errore correlato nella logs/error.log. Per eliminare l&#39;elemento di replica non valido, effettuate le seguenti operazioni:

   1. Andate a https://&lt;host>:&lt;porta>/crx/de e accedete come utente amministratore.
   1. Fare clic su &quot;Strumenti&quot; dal menu principale.
   1. Fare clic sul pulsante della lente di ingrandimento.
   1. Selezionare &quot;XPath&quot; come Tipo.
   1. Nella casella &quot;Query&quot; immettere l&#39;ordine di query /jcr:root/var/eventing/jobs//element(*,slingevent:Job) di @slingevent:created
   1. Fare clic su &quot;Search&quot;
   1. Nei risultati, gli elementi principali sono gli ultimi processi di sling eventing. Clicca su ciascuno e trova le repliche bloccate che corrispondono a ciò che appare nella parte superiore della coda.

1. Potrebbe esserci qualcosa di sbagliato nel tagliare le code di lavoro del framework di eventi. Provare a riavviare il bundle org.apache.sling.event nella console/system/console.
1. Potrebbe darsi che l&#39;elaborazione dei processi sia completamente disattivata. Potete controllarlo nella console Felix nella scheda Sling Eventing (Evento Sling). Controlla se viene visualizzato - Apache Sling Eventing (L&#39;ELABORAZIONE DEL PROCESSO È DISATTIVATA!)

   * Se sì, selezionate il gestore eventi processo Apache Sling nella scheda Configurazione nella console Felix. Potrebbe essere che la casella di controllo &#39;Elaborazione processo abilitata&#39; sia deselezionata. Se questa opzione è selezionata e continua a visualizzare che l&#39;elaborazione del processo è disabilitata, verificate che in /apps/system/config sia presente una sovrapposizione che disattiva l&#39;elaborazione del processo. Provate a creare un nodo osgi:config per jobmanager.enabled con un valore booleano su true e verificate nuovamente se l&#39;attivazione è iniziata e non ci sono più processi in coda.

1. Potrebbe anche verificarsi il caso in cui la configurazione DefaultJobManager si trovi in uno stato incoerente. Ciò può accadere quando qualcuno modifica manualmente la configurazione &#39;Apache Sling Job Event Handler&#39; tramite OSGiconsole (ad esempio, disabilita e riabilita la proprietà &#39;Job Processing Enabled&#39; e salva la configurazione).

   * A questo punto, la configurazione DefaultJobManager memorizzata in crx-quickstart/launchpad/config/org/apache/sling/event/impl/jobs/DefaultJobManager.config si trova in uno stato incoerente. E anche se la proprietà &#39;Apache Sling Job Event Handler&#39; mostra &#39;Job Processing Enabled&#39; come stato controllato, quando si passa alla scheda Sling Eventing, viene visualizzato il messaggio - JOB PROCESSING IS DISABLED e la replica non funziona.
   * Per risolvere questo problema, è necessario passare alla pagina Configurazione della console OSGi ed eliminare la configurazione &#39;Apache Sling Job Event Handler&#39;. Riavviate quindi il nodo master del cluster per ripristinare la configurazione in uno stato coerente. In questo modo si dovrebbe risolvere il problema e la replica riprenderà a funzionare.

**Creare un file Replication.log**

A volte può essere molto utile impostare tutte le registrazioni di replica da aggiungere in un file di registro separato a livello DEBUG. Per effettuare ciò:

1. Andate a https://host:port/system/console/configMgr e accedete come amministratore.
1. Trovate la fabbrica Apache Sling Logging e create un&#39;istanza facendo clic sul pulsante **+** a destra della configurazione di fabbrica. Questo creerà un nuovo logger.
1. Impostate la configurazione come segue:

   * Livello registro: DEBUG
   * Percorso file di registro: logs/replication.log
   * Categorie: com.day.cq.replication

1. Se sospettate che il problema sia correlato alla vendita di eventi/processi in qualsiasi modo, potete anche aggiungere questo pacchetto Java in categorie:org.apache.sling.event

## Sospensione della coda dell&#39;agente di replica {#pausing-replication-agent-queue}

In alcuni casi potrebbe essere opportuno mettere in pausa la coda di replica per ridurre il carico sul sistema di authoring, senza disattivarla. Attualmente questo è possibile solo tramite un hack di configurazione temporanea di una porta non valida. A partire da 5.4 è possibile visualizzare il pulsante Pausa nella coda dell&#39;agente di replica che presenta alcuni limiti

1. Lo stato non è persistente, ovvero se si riavvia un server o si ricicla un bundle di replica, si torna allo stato di esecuzione.
1. La pausa è inattiva per un periodo più breve (OOB 1 ora dopo l’assenza di attività con replica da parte di altri thread) e non per un periodo più lungo. Perché c&#39;è una caratteristica nella fionda che evita i filetti inattivi. In sostanza, verificate se un thread della coda di lavoro non è stato utilizzato per un periodo di tempo più lungo, se necessario, avvia cicli di pulizia. A causa del ciclo di pulizia, il thread si arresta e quindi l&#39;impostazione messa in pausa si perde. Poiché i processi sono persistenti, avvia un nuovo thread per elaborare la coda che non contiene dettagli sulla configurazione in pausa. A causa di questa coda si trasforma in stato di esecuzione.

## Le autorizzazioni pagina non vengono replicate in attivazione utente {#page-permissions-are-not-replicated-on-user-activation}

Le autorizzazioni di pagina non vengono replicate perché sono memorizzate nei nodi a cui è concesso l&#39;accesso, non con l&#39;utente.

In generale, le autorizzazioni della pagina non devono essere replicate dall’autore alla pubblicazione e non sono per impostazione predefinita. Questo perché i diritti di accesso dovrebbero essere diversi in questi due ambienti. Si consiglia pertanto di configurare gli ACL al momento della pubblicazione separatamente dall&#39;autore.

## Coda di replica bloccata durante la replica delle informazioni dello spazio nomi da Author a Publish {#replication-queue-blocked-when-replicating-namespace-information-from-author-to-publish}

In alcuni casi, la coda di replica viene bloccata quando si tenta di replicare le informazioni dello spazio nomi dall’istanza di creazione all’istanza di pubblicazione. Ciò si verifica perché l&#39;utente di replica non dispone di privilegi `jcr:namespaceManagement`. Per evitare questo problema, accertatevi che:

* L&#39;utente di replica (configurato nella scheda [Trasporto](/help/sites-deploying/replication.md#replication-agents-configuration-parameters)>Utente) esiste anche nell&#39;istanza Pubblica.
* L&#39;utente dispone dei privilegi di lettura e scrittura nel percorso in cui è installato il contenuto.
* L&#39;utente ha il privilegio `jcr:namespaceManagement` a livello di repository. Potete concedere il privilegio come segue:

1. Accedete a CRX/DE ( `https://localhost:4502/crx/de/index.jsp`) come amministratore.
1. Fare clic sulla scheda **Controllo accesso**.
1. Selezionare **Repository**.
1. Fare clic su **Aggiungi voce** (icona più).
1. Immettete il nome dell’utente.
1. Selezionare `jcr:namespaceManagement` dall&#39;elenco dei privilegi.
1. Fai clic su OK.

