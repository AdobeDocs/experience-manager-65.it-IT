---
title: Risoluzione dei problemi di replica
description: Questo articolo fornisce informazioni su come risolvere i problemi di replica.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
docset: aem65
feature: Configuring
exl-id: cfa822c8-f9a9-4122-9eac-0293d525f6b5
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 0%

---

# Risoluzione dei problemi di replica{#troubleshooting-replication}

Questa pagina fornisce informazioni su come risolvere i problemi di replica.

## Problema {#problem}

La replica (replica non inversa) non riesce per qualche motivo.

## Risoluzione {#resolution}

Esistono diversi motivi per cui la replica non riesce. Questo articolo spiega l’approccio che si potrebbe adottare quando si analizzano questi problemi.

**Le repliche vengono attivate quando si fa clic sul pulsante Attiva? Se NON lo è, procedere come segue:**

1. Vai a /crx/explorer e accedi come amministratore.
1. Apri &quot;Esplora contenuti&quot;
1. Verifica se esiste un nodo /bin/replicate o /bin/replicate.json. Se il nodo esiste, eliminalo e salvalo.

**Le repliche vengono messe in coda nelle code dell&#39;agente di replica?**

Seleziona questa opzione andando su /etc/replication/agents.author.html, quindi fai clic sugli agenti di replica da controllare.

**Se una o più code di agenti sono bloccate:**

1. La coda viene visualizzata **bloccato** stato? In caso affermativo, l’istanza Publish non è in esecuzione o non risponde? Controlla l’istanza Publish per vedere cosa c’è di sbagliato. In altre parole, controlla i registri e verifica se è presente un errore OutOfMemory o un altro problema. Se è semplicemente lento, prendi le immagini thread e analizzale.
1. Lo stato della coda è visibile **La coda è attiva - n. in sospeso**? In pratica, il processo di replica potrebbe essere bloccato in un socket letto in attesa della risposta dell’istanza Publish o di Dispatcher. Ciò potrebbe significare che l’istanza Publish o Dispatcher è sotto un carico elevato o è bloccata in un blocco. In questo caso, prendi le immagini thread da authoring e pubblica.

   * Apri le immagini thread dall’autore in un analizzatore di immagini thread, verifica se il processo di eventi sling dell’agente di replica è bloccato in un socketRead.
   * Apri le immagini thread da Publish in un analizzatore di immagini thread e analizza cosa potrebbe causare la mancata risposta dell’istanza Publish. Dovresti trovare un thread con il nome POST /bin/receive che corrisponde al thread che riceve la replica dall’autore.

**Se tutte le code dell&#39;agente sono bloccate**

1. È possibile che un determinato contenuto non possa essere serializzato in /var/replication/data a causa di un danneggiamento dell’archivio o per altri problemi. Controlla logs/error.log per un errore correlato. Per cancellare l’elemento di replica non valido, effettua le seguenti operazioni:

   1. Vai a https://&lt;host>:&lt;port>/crx/de e accedi come utente amministratore.
   1. Fare clic su Strumenti nel menu principale.
   1. Fare clic sul pulsante della lente di ingrandimento.
   1. Selezionare &quot;XPath&quot; come Tipo.
   1. Nella casella &quot;Query&quot; immettere questa query /jcr:root/var/eventing/jobs//element(&#42;,slingevent:Job) ordina per @slingevent:creato
   1. Fare clic su &quot;Search&quot; (Cerca).
   1. Nei risultati, gli elementi principali sono gli ultimi sette processi con eventi. Fai clic su ciascuna replica e trova le repliche bloccate corrispondenti a quelle visualizzate nella parte superiore della coda.

1. Potrebbe essersi verificato un errore con le code dei processi del framework eventi Sling. Prova a riavviare il bundle org.apache.sling.event in/system/console.
1. È possibile che l’elaborazione del processo sia disattivata. Puoi verificarlo in Felix Console nella scheda Evento di Sling. Controlla se viene visualizzato - Evento Apache Sling (L’ELABORAZIONE DEL PROCESSO È DISABILITATA!)

   * In caso affermativo, controlla Apache Sling Job Event Handler nella scheda Configuration della console Felix. È possibile che la casella di controllo Elaborazione processo abilitata sia deselezionata. Se questa opzione è selezionata e viene comunque visualizzato che &quot;l’elaborazione del processo è disabilitata&quot;, verifica se è presente una sovrapposizione in /apps/system/config che disabilita l’elaborazione del processo. Prova a creare un nodo osgi:config per jobmanager.enabled con un valore booleano impostato su true e verifica di nuovo se l’attivazione è iniziata e non sono presenti altri processi in coda.

1. È inoltre possibile che la configurazione di DefaultJobManager entri in uno stato incoerente. Questo può accadere quando qualcuno modifica manualmente la configurazione di &quot;Apache Sling Job Event Handler&quot; tramite OSGiconsole (ad esempio, disabilita e riabilita la proprietà &quot;Job Processing Enabled&quot; e salva la configurazione).

   * A questo punto la configurazione DefaultJobManager memorizzata in crx-quickstart/launchpad/config/org/apache/sling/event/impl/jobs/DefaultJobManager.config diventa incoerente. E anche se la proprietà &quot;Apache Sling Job Event Handler&quot; mostra che &quot;Elaborazione del processo abilitata&quot; è in stato selezionato, quando si passa alla scheda Evento Sling, viene visualizzato il messaggio - ELABORAZIONE DEL PROCESSO DISABILITATA e la replica non funziona.
   * Per risolvere questo problema, accedi alla pagina Configurazione della console OSGi ed elimina la configurazione &quot;Apache Sling Job Event Handler&quot;. Riavviare quindi il nodo Master del cluster per riportare la configurazione in uno stato coerente. Questo dovrebbe risolvere il problema e la replica ricomincia a funzionare.

**Creare un replication.log**

A volte è utile impostare tutte le registrazioni di replica da aggiungere in un file di registro separato a livello di DEBUG. Per effettuare questo collegamento:

1. Vai a https://host:port/system/console/configMgr e accedi come amministratore.
1. Trova la factory del logger di registrazione Apache Sling e crea un’istanza facendo clic sul pulsante **+** sulla destra della configurazione di fabbrica. Verrà creato un nuovo logger di registrazione.
1. Imposta la configurazione come segue:

   * Livello registro: DEBUG
   * Percorso file di registro: logs/replication.log
   * Categorie: com.day.cq.replication

1. Se pensi che il problema sia correlato in qualche modo a sling eventing/jobs, puoi anche aggiungere questo pacchetto Java™ nelle categorie:org.apache.sling.event

## Sospensione coda agente di replica  {#pausing-replication-agent-queue}

A volte può essere opportuno mettere in pausa la coda di replica per ridurre il carico sul sistema di authoring, senza disabilitarla. Attualmente, ciò è possibile solo tramite un hack di configurazione temporanea di una porta non valida. Dalla versione 5.4 in poi, il pulsante Pausa nella coda dell’agente di replica presenta alcune limitazioni

1. Lo stato non è persistente, il che significa che se si riavvia un server o se il bundle di replica viene riciclato, viene ripristinato lo stato di esecuzione.
1. La pausa è inattiva per un periodo più breve (OOB 1 ora dopo nessuna attività con replica da parte di altri thread) e non per un periodo più lungo. Perché c’è una funzione in sling che evita i thread inattivi. In pratica, verifica se un thread della coda processi è stato inutilizzato per un periodo di tempo più lungo. In tal caso, avvia i cicli di pulizia. A causa del ciclo di pulizia, il thread viene arrestato e l&#39;impostazione di pausa viene quindi persa. Poiché i processi sono persistenti, viene avviato un nuovo thread per elaborare la coda che non contiene dettagli sulla configurazione in pausa. A causa di questa coda si trasforma in stato di esecuzione.

## Le autorizzazioni pagina non vengono replicate al momento dell’attivazione dell’utente {#page-permissions-are-not-replicated-on-user-activation}

Le autorizzazioni di pagina non vengono replicate perché sono memorizzate nei nodi a cui è concesso l’accesso, non con l’utente.

In generale, le autorizzazioni di pagina non devono essere replicate dall’autore alla pubblicazione e non sono per impostazione predefinita. Questo perché i diritti di accesso dovrebbero essere diversi in questi due ambienti. Pertanto, l’Adobe consiglia di configurare gli ACL in fase di pubblicazione, separatamente dall’istanza di authoring.

## Coda di replica bloccata durante la replica delle informazioni sullo spazio dei nomi da Author a Publish {#replication-queue-blocked-when-replicating-namespace-information-from-author-to-publish}

A volte la coda di replica viene bloccata quando si tenta di replicare le informazioni sullo spazio dei nomi dall’istanza di authoring all’istanza di pubblicazione. Ciò si verifica perché l’utente di replica non dispone di `jcr:namespaceManagement` privilegio. Per evitare questo problema, assicurati che:

* L&#39;utente di replica (come configurato in [Trasporto](/help/sites-deploying/replication.md#replication-agents-configuration-parameters) tab>User) esiste anche nell’istanza Publish.
* L’utente dispone dei privilegi di lettura e scrittura nel percorso in cui viene installato il contenuto.
* L’utente ha `jcr:namespaceManagement` privilegio a livello di repository. È possibile concedere il privilegio nel modo seguente:

1. Accedi a CRX/DE ( `https://localhost:4502/crx/de/index.jsp`) come amministratore.
1. Fai clic su **Controllo dell’accesso** scheda.
1. Seleziona **Archivio**.
1. Clic **Aggiungi voce** (icona più ).
1. Immettere il nome dell&#39;utente.
1. Seleziona `jcr:namespaceManagement` dall&#39;elenco dei privilegi.
1. Fai clic su **OK**.
