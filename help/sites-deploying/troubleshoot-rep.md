---
title: Risoluzione dei problemi di replica
seo-title: Troubleshooting Replication
description: Questo articolo fornisce informazioni su come risolvere i problemi di replica.
seo-description: This article provides information on how to troubleshoot replication issues.
uuid: 1662bf60-b000-4eb2-8834-c6da607128fe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 0d055be7-7189-4587-8c7c-2ce34e22a6ad
docset: aem65
feature: Configuring
exl-id: cfa822c8-f9a9-4122-9eac-0293d525f6b5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1243'
ht-degree: 0%

---

# Risoluzione dei problemi di replica{#troubleshooting-replication}

Questa pagina fornisce informazioni su come risolvere i problemi di replica.

## Problema {#problem}

La replica (replica non inversa) non riesce per qualche motivo.

## Risoluzione {#resolution}

Ci sono varie ragioni per cui la replica non riesce. Questo articolo spiega l&#39;approccio che si potrebbe adottare quando si analizzano questi problemi.

**Le replicazioni vengono attivate quando si fa clic sul pulsante Attiva? In caso contrario, procedere come segue:**

1. Vai a /crx/explorer e accedi come amministratore.
1. Apri &quot;Esplora contenuti&quot;
1. Vedi se esiste un nodo /bin/replicate o /bin/replicate.json. Se il nodo esiste, eliminalo e salva.

**Le replicazioni vengono messe in coda nelle code degli agenti di replica?**

Controlla questo andando a /etc/replication/agents.author.html, quindi fai clic sugli agenti di replica da controllare.

**Se una coda dell&#39;agente o alcune code dell&#39;agente sono bloccate:**

1. Visualizza la coda **bloccato** stato? In caso affermativo, l’istanza di pubblicazione non è in esecuzione o non risponde completamente? Controlla l&#39;istanza di pubblicazione per vedere cosa c&#39;è che non va (ad es. controlla i log, e vedi se c&#39;è un errore OutOfMemory o qualche altro problema. Poi se è solo generalmente lento allora prendere i dump di thread e analizzarli.
1. Viene visualizzato lo stato della coda? **La coda è attiva - # in sospeso**? In sostanza, il processo di replica potrebbe essere bloccato in una lettura del socket in attesa della risposta dell&#39;istanza o del dispatcher di pubblicazione. Ciò potrebbe significare che l’istanza o il dispatcher di pubblicazione è sotto carico elevato o bloccato in un blocco. Prendi i dump di thread dall&#39;autore e pubblica in questo caso.

   * Apri i dump di thread dall&#39;autore in un analizzatore di dump di thread, controlla se mostra che il processo di sling eventing dell&#39;agente di replica è bloccato in un socketRead.
   * Apri i dump di thread da publish in un analizzatore di dump di thread, analizza cosa potrebbe causare la mancata risposta dell&#39;istanza di pubblicazione. Dovresti visualizzare un thread con POST /bin/receive nel suo nome, ovvero il thread che riceve la replica dall&#39;autore.

**Se tutte le code dell&#39;agente sono bloccate**

1. È possibile che un certo contenuto non possa essere serializzato sotto /var/replication/data a causa di corruzione dell&#39;archivio o di qualche altro problema. Controlla logs/error.log per un errore correlato. Per eliminare l&#39;elemento di replica non valido, procedi come segue:

   1. Vai su https://&lt;host>:&lt;port>/crx/de e accedi come utente amministratore.
   1. Fai clic su &quot;Strumenti&quot; dal menu principale.
   1. Fare clic sul pulsante della lente d&#39;ingrandimento.
   1. Selezionare &quot;XPath&quot; come Tipo.
   1. Nella casella &quot;Query&quot; inserisci questa query /jcr:root/var/eventing/jobs//element(&#42;,slingevent:Job) ordine di @slingevent:created
   1. Fai clic su &quot;Cerca&quot;
   1. Nei risultati gli elementi principali sono gli ultimi lavori di eventing sling. Fai clic su ciascuna e trova le repliche bloccate che corrispondono a ciò che viene visualizzato nella parte superiore della coda.

1. Ci potrebbe essere qualcosa di sbagliato nell&#39;alleggerire le code di lavoro del framework degli eventi. Prova a riavviare il bundle org.apache.sling.event in/system/console.
1. Potrebbe essere che l&#39;elaborazione dei processi sia completamente disattivata. Puoi controllarlo sotto la console Felix nella scheda Sling Eventing. Controlla se viene visualizzato - Evento Sling Apache (L&#39;ELABORAZIONE DEL PROCESSO È DISATTIVATA!)

   * Se sì, allora controlla Apache Sling Job Event Handler sotto la scheda Configuration in Felix Console. Potrebbe essere che la casella di controllo &quot;Elaborazione processo abilitata&quot; sia deselezionata. Se è selezionato e visualizza ancora che &#39;l&#39;elaborazione del processo è disabilitata&#39;, quindi controlla se c&#39;è una sovrapposizione sotto /apps/system/config che sta disabilitando l&#39;elaborazione del processo. Prova a creare un nodo osgi:config per jobmanager.enabled con un valore booleano su true e controlla nuovamente se l&#39;attivazione è iniziata e non ci sono più processi in coda.

1. È anche possibile che la configurazione di DefaultJobManager si trovi in uno stato incoerente. Questo può accadere quando qualcuno modifica manualmente la configurazione di &#39;Apache Sling Job Event Handler&#39; tramite l&#39;OSGiconsole (ad esempio, disattiva e riattiva la proprietà &#39;Job Processing Enabled&#39; e salva la configurazione).

   * A questo punto la configurazione DefaultJobManager memorizzata in crx-quickstart/launchpad/config/org/apache/sling/event/impl/jobs/DefaultJobManager.config si trova in uno stato incoerente. E anche se la proprietà &#39;Apache Sling Job Event Handler&#39; mostra che &#39;Job Processing Enabled&#39; è in stato selezionato, quando si passa alla scheda Sling Eventing, mostra il messaggio - JOB PROCESSING IS DISABLED e la replica non funziona.
   * Per risolvere questo problema, è necessario passare alla pagina Configurazione della console OSGi ed eliminare la configurazione &quot;Apache Sling Job Event Handler&quot;. Quindi riavvia il nodo principale del cluster per riportare la configurazione in uno stato coerente. Questo dovrebbe risolvere il problema e la replica inizierà a funzionare di nuovo.

**Creare un file replication.log**

A volte può essere molto utile impostare tutte le registrazioni di replica da aggiungere in un file di log separato a livello di DEBUG. Per effettuare questo collegamento:

1. Vai su https://host:port/system/console/configMgr e accedi come amministratore.
1. Trova la fabbrica del logger di registrazione Apache Sling e crea un’istanza facendo clic sul pulsante **+** a destra della configurazione di fabbrica. Verrà creato un nuovo logger di registrazione.
1. Imposta la configurazione come segue:

   * Livello di log: DEBUG
   * Percorso file di registro: logs/replication.log
   * Categorie: com.day.cq.replication

1. Se sospetti che il problema sia correlato all&#39;evento o ai lavori di sling in qualsiasi modo, puoi anche aggiungere questo pacchetto java in categories:org.apache.sling.event

## Sospensione della coda dell&#39;agente di replica  {#pausing-replication-agent-queue}

A volte potrebbe essere opportuno mettere in pausa la coda di replica per ridurre il carico sul sistema di authoring, senza disattivarlo. Attualmente questo è possibile solo tramite un hack di configurazione temporanea di una porta non valida. A partire da 5.4 è possibile vedere il pulsante di pausa nella coda dell&#39;agente di replica ha alcune limitazioni

1. Lo stato non viene mantenuto, il che significa che se si riavvia un server o un bundle di replica viene riciclato, ritorna allo stato di esecuzione.
1. La pausa è inattiva per un periodo più breve (OOB 1 ora dopo nessuna attività con replica da parte di altri thread) e non per un periodo di tempo più lungo. Perché c&#39;è una funzione in sling che evita i thread inattivi. In pratica, controlla se un thread della coda di lavoro è stato inutilizzato per un periodo di tempo più lungo, se così facendo si innesca i cicli di pulizia. A causa del ciclo di pulizia arresta il thread e quindi l&#39;impostazione sospesa viene persa. Dal momento che i processi sono persistenti, avvia un nuovo thread per elaborare la coda che non ha dettagli della configurazione sospesa. A causa di questa coda si trasforma in stato di esecuzione.

## Le autorizzazioni di pagina non vengono replicate all&#39;attivazione dell&#39;utente {#page-permissions-are-not-replicated-on-user-activation}

Le autorizzazioni di pagina non vengono replicate perché sono memorizzate sotto i nodi a cui è concesso l&#39;accesso, non con l&#39;utente.

In generale, le autorizzazioni della pagina non devono essere replicate dall&#39;autore per la pubblicazione e non sono per impostazione predefinita. Questo perché i diritti di accesso devono essere diversi in questi due ambienti. Pertanto si consiglia di configurare le ACL al momento della pubblicazione separatamente dall&#39;autore.

## Coda di replica bloccata durante la replica delle informazioni sullo spazio dei nomi da Author a Publish {#replication-queue-blocked-when-replicating-namespace-information-from-author-to-publish}

In alcuni casi la coda di replica viene bloccata quando si tenta di replicare le informazioni sullo spazio dei nomi dall&#39;istanza dell&#39;autore all&#39;istanza di pubblicazione. Questo accade perché l&#39;utente di replica non ha `jcr:namespaceManagement` privilegio. Per evitare questo problema, assicurati che:

* L&#39;utente di replica (come configurato in [Trasporti](/help/sites-deploying/replication.md#replication-agents-configuration-parameters) tab>User) esiste anche nell&#39;istanza Publish.
* L&#39;utente dispone dei privilegi di lettura e scrittura nel percorso in cui è installato il contenuto.
* L&#39;utente ha `jcr:namespaceManagement` a livello di archivio. Puoi concedere il privilegio come segue:

1. Accedi a CRX/DE ( `https://localhost:4502/crx/de/index.jsp`) come amministratore.
1. Fai clic sul pulsante **Controllo degli accessi** scheda .
1. Seleziona **Archivio**.
1. Fai clic su **Aggiungi voce** (l’icona più).
1. Immettere il nome dell&#39;utente.
1. Seleziona `jcr:namespaceManagement` dall&#39;elenco dei privilegi.
1. Fai clic su OK.
