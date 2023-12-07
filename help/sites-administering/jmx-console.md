---
title: Monitoraggio delle risorse del server tramite la console JMX
description: Scopri come monitorare le risorse del server utilizzando la console JMX.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: eabd8335-6140-4c15-8cff-21608719aa5f
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '4830'
ht-degree: 0%

---

# Monitoraggio delle risorse del server tramite la console JMX{#monitoring-server-resources-using-the-jmx-console}

La console JMX consente di monitorare e gestire i servizi sul server CRX. Le sezioni che seguono riepilogano gli attributi e le operazioni esposte tramite il framework JMX.

Per informazioni sull&#39;utilizzo dei controlli della console, vedere [Utilizzo della console JMX](#using-the-jmx-console). Per informazioni di base su JMX, vedi [Tecnologia Java Management Extensions (JMX)](https://www.oracle.com/technetwork/java/javase/tech/javamanagement-140525.html) sul sito web dell’Oracle.

Per informazioni sulla creazione di MBean per gestire i servizi tramite la console JMX, consulta [Integrazione dei servizi con la console JMX](/help/sites-developing/jmx-integration.md).

## Manutenzione del flusso di lavoro {#workflow-maintenance}

Operazioni per l’amministrazione di istanze di flusso di lavoro in esecuzione, completate, non aggiornate e non riuscite.

* Dominio: com.adobe.granite.workflow
* Tipo: manutenzione

>[!NOTE]
>
>Consulta la [console flusso di lavoro](/help/sites-administering/workflows-administering.md) per ulteriori strumenti di amministrazione del flusso di lavoro e descrizioni dei possibili stati delle istanze del flusso di lavoro.

### Operazioni {#operations}

**listRunningWorkflowsPerModel** Elenca il numero di istanze del flusso di lavoro in esecuzione per ciascun modello di flusso di lavoro.

* Argomenti: nessuno
* Valore restituito: dati tabulari contenenti le colonne Count e ModelId.

**listCompletedWorkflowsPerModel** Elenca il numero di istanze di flusso di lavoro completate per ciascun modello di flusso di lavoro.

* Argomenti: nessuno
* Valore restituito: dati tabulari contenenti le colonne Count e ModelId.

**returnWorkflowQueueInfo** Elenca le informazioni sugli elementi del flusso di lavoro che sono stati elaborati e che sono in coda per l&#39;elaborazione.

* Argomenti: nessuno
* Valore restituito: dati tabulari contenenti le colonne seguenti:

   * Jobs
   * Nome coda
   * Lavori attivi
   * Tempo medio di elaborazione
   * Tempo medio di attesa
   * Lavori annullati
   * Lavori con errori
   * Processi completati
   * Processi elaborati
   * Processi in coda

**returnWorkflowJobTopicInfo** Elenca le informazioni di elaborazione per i processi del flusso di lavoro, organizzate per argomento.

* Argomenti: nessuno
* Valore restituito: dati tabulari contenenti le colonne seguenti:

   * Nome argomento
   * Tempo medio di elaborazione
   * Tempo medio di attesa
   * Lavori annullati
   * Lavori con errori
   * Processi completati
   * Processi elaborati

**returnFailedWorkflowCount** Mostra il numero di istanze del flusso di lavoro non riuscite. È possibile specificare un modello di flusso di lavoro per eseguire query o recuperare informazioni per tutti i modelli di flusso di lavoro.

* Argomenti:

   * model: ID del modello da interrogare. Per visualizzare un conteggio delle istanze del flusso di lavoro non riuscite per tutti i modelli di flusso di lavoro, non specificare alcun valore. L’ID è il percorso del nodo del modello, ad esempio:

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valore restituito: numero di istanze del flusso di lavoro non riuscite.

**returnFailedWorkflowCountPerModel** Mostra il numero di istanze del flusso di lavoro non riuscite per ciascun modello di flusso di lavoro.

* Argomenti: nessuno.
* Valore restituito: dati tabulari contenenti le colonne Count e Model ID.

**terminateFailedInstances** Termina le istanze del flusso di lavoro non riuscite. È possibile terminare tutte le istanze non riuscite o solo le istanze non riuscite per un modello specifico. Facoltativamente, puoi riavviare le istanze dopo che sono state terminate. È inoltre possibile eseguire il test dell&#39;operazione per visualizzare i risultati senza eseguire l&#39;operazione.

* Argomenti:

   * Riavvia l’istanza: (facoltativo) specifica un valore di `true` per riavviare le istanze dopo che sono state terminate. Il valore predefinito di `false` non riavvia le istanze del flusso di lavoro terminate.
   * Dry run: (facoltativo) specifica un valore di `true` per visualizzare i risultati dell&#39;operazione senza eseguirla effettivamente. Il valore predefinito di `false` causa l&#39;esecuzione dell&#39;operazione.
   * Modello: (facoltativo) l’ID del modello a cui viene applicata l’operazione. Non specificate alcun modello per applicare l&#39;operazione alle istanze non riuscite di tutti i modelli di flusso di lavoro. L’ID è il percorso del nodo del modello, ad esempio:

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valore restituito: dati tabulari relativi alle istanze terminate, contenenti le colonne seguenti:

   * Iniziatore
   * InstanceId
   * ID modello
   * Payload
   * StartComment
   * WorkflowTitle

**retryFailedWorkItems** Tentativi non riusciti di eseguire i passaggi dell&#39;elemento di lavoro. È possibile riprovare tutti gli elementi di lavoro non riusciti o solo gli elementi di lavoro non riusciti per un modello di flusso di lavoro specifico. È possibile eseguire il test dell&#39;operazione per visualizzare i risultati senza eseguire effettivamente l&#39;operazione.

* Argomenti:

   * Dry run: (facoltativo) specifica un valore di `true` per visualizzare i risultati dell&#39;operazione senza eseguirla effettivamente. Il valore predefinito di `false` causa l&#39;esecuzione dell&#39;operazione.
   * Modello: (facoltativo) l’ID del modello a cui viene applicata l’operazione. Non specificare alcun modello per applicare l&#39;operazione agli elementi di lavoro non riusciti di tutti i modelli di flusso di lavoro. L’ID è il percorso del nodo del modello, ad esempio:

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valore restituito: dati tabulari relativi agli elementi di lavoro non riusciti che vengono ritentati, incluse le colonne seguenti:

   * Iniziatore
   * InstanceId
   * ID modello
   * Payload
   * StartComment
   * WorkflowTitle

**PurgeActive** Rimuove le istanze di flusso di lavoro attive di una pagina specifica. Potete eliminare le varianti attive per tutti i modelli o solo le varianti per un modello specifico. Se lo si desidera, è possibile eseguire il test dell&#39;operazione per visualizzare i risultati senza eseguirla effettivamente.

* Argomenti:

   * Modello: (facoltativo) l’ID del modello a cui viene applicata l’operazione. Non specificate alcun modello per applicare l&#39;operazione alle istanze del flusso di lavoro di tutti i modelli del flusso di lavoro. L’ID è il percorso del nodo del modello, ad esempio:

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * Numero di giorni dall’avvio del flusso di lavoro: età in giorni delle istanze del flusso di lavoro da eliminare.
   * Dry run: (facoltativo) specifica un valore di `true` per visualizzare i risultati dell&#39;operazione senza eseguirla effettivamente. Il valore predefinito di `false` causa l&#39;esecuzione dell&#39;operazione.

* Valore restituito: dati tabulari relativi alle istanze del flusso di lavoro attive eliminate, incluse le colonne seguenti:

   * Iniziatore
   * InstanceId
   * ID modello
   * Payload
   * StartComment
   * WorkflowTitle

**countStaleWorkflows** Restituisce il numero di istanze del flusso di lavoro non aggiornate. Puoi recuperare il numero di istanze non aggiornate per tutti i modelli di flusso di lavoro o per un modello specifico.

* Argomenti:

   * Modello: (facoltativo) l’ID del modello a cui viene applicata l’operazione. Non specificate alcun modello per applicare l&#39;operazione alle istanze del flusso di lavoro di tutti i modelli del flusso di lavoro. L’ID è il percorso del nodo del modello, ad esempio:

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valore restituito: numero di istanze di flusso di lavoro non aggiornate.

**restartStaleWorkflows** Riavvia le istanze di flusso di lavoro obsolete. È possibile riavviare tutte le istanze non aggiornate o solo le istanze non aggiornate per un modello specifico. È inoltre possibile eseguire il test dell&#39;operazione per visualizzare i risultati senza eseguire l&#39;operazione.

* Argomenti:

   * Modello: (facoltativo) l’ID del modello a cui viene applicata l’operazione. Non specificate alcun modello per applicare l&#39;operazione alle istanze non aggiornate di tutti i modelli di flusso di lavoro. L’ID è il percorso del nodo del modello, ad esempio:

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * Dry run: (facoltativo) specifica un valore di `true` per visualizzare i risultati dell&#39;operazione senza eseguirla effettivamente. Il valore predefinito di `false` causa l&#39;esecuzione dell&#39;operazione.

* Valore restituito: elenco di istanze del flusso di lavoro riavviate.

**fetchModelList** Elenca tutti i modelli di workflow.

* Argomenti: nessuno
* Valore restituito: dati tabulari che identificano i modelli di flusso di lavoro, incluse le colonne ModelId e ModelName.

**countRunningWorkflows** Restituisce il numero di istanze del flusso di lavoro in esecuzione. Puoi recuperare il numero di istanze in esecuzione per tutti i modelli di flusso di lavoro o per un modello specifico.

* Argomenti:

   * Modello: (facoltativo) l’ID del modello per il quale viene restituito il numero di istanze in esecuzione. Non specificare alcun modello per restituire il numero di istanze in esecuzione di tutti i modelli di flusso di lavoro. L’ID è il percorso del nodo del modello, ad esempio:

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valore restituito: numero di istanze del flusso di lavoro in esecuzione.

**countCompletedWorkflows** Restituisce il numero di istanze del flusso di lavoro completate. Puoi recuperare il numero di istanze completate per tutti i modelli di flusso di lavoro o per un modello specifico.

* Argomenti:

   * Modello: (facoltativo) l’ID del modello per il quale viene restituito il numero di istanze completate. Non specificare alcun modello per restituire il numero di istanze completate di tutti i modelli di flusso di lavoro. L’ID è il percorso del nodo del modello, ad esempio:

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valore restituito: numero di istanze del flusso di lavoro completate.

**purgeCompleted** Rimuove i record dei flussi di lavoro completati di una data specifica dall’archivio. Utilizza questa operazione periodicamente per ridurre al minimo le dimensioni dell’archivio quando utilizzi in modo massiccio i flussi di lavoro. Potete eliminare le varianti completate per tutti i modelli o solo le varianti per un modello specifico. Se lo si desidera, è possibile eseguire il test dell&#39;operazione per visualizzare i risultati senza eseguirla effettivamente.

* Argomenti:

   * Modello: (facoltativo) l’ID del modello a cui viene applicata l’operazione. Non specificate alcun modello per applicare l&#39;operazione alle istanze del flusso di lavoro di tutti i modelli del flusso di lavoro. L’ID è il percorso del nodo del modello, ad esempio:

     `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * Numero di giorni dal completamento del flusso di lavoro: il numero di giorni in cui le istanze del flusso di lavoro sono state completate.
   * Dry run: (facoltativo) specifica un valore di `true` per visualizzare i risultati dell&#39;operazione senza eseguirla effettivamente. Il valore predefinito di `false` causa l&#39;esecuzione dell&#39;operazione.

* Valore restituito: dati tabulari relativi alle istanze del flusso di lavoro completate che vengono eliminate, incluse le colonne seguenti:

   * Iniziatore
   * InstanceId
   * ID modello
   * Payload
   * StartComment
   * WorkflowTitle

## Archivio {#repository}

Informazioni sull’archivio CRX

* Dominio: com.adobe.granite
* Tipo: archivio

### Attributi {#attributes}

**Nome** Nome dell’implementazione dell’archivio JCR. Sola lettura.

**Versione** Versione di implementazione dell’archivio. Sola lettura.

**DirHome** La directory in cui si trova l’archivio. La posizione predefinita è &lt;quickstart_jar_location>/crx-quickstart/repository. Sola lettura.

**NomeCliente** Il nome del cliente a cui viene rilasciata la licenza software. Sola lettura.

**LicenseKey** Chiave di licenza univoca per questa installazione dell’archivio. Sola lettura.

**AvailableDiskSpace** Spazio su disco disponibile per questa istanza del repository, in Mbyte. Sola lettura.

**MaximumNumberOfOpenFiles** Il numero di file che è possibile aprire contemporaneamente. Sola lettura.

**SessionTracker** Il valore della variabile di sistema crx.debug.essions. true indica una sessione di debug. false indica una sessione normale. Lettura/scrittura.

**Descrittori** Un insieme di coppie chiave-valore che rappresentano le proprietà dell’archivio. Tutte le proprietà sono di sola lettura.

<table>
 <tbody>
  <tr>
   <th>Chiave</th>
   <th>Valore</th>
  </tr>
  <tr>
   <td>option.node.and.property.with.same.name.supported</td>
   <td>Indica se un nodo e una proprietà del nodo possono avere lo stesso nome. true indica che sono supportati gli stessi nomi, false indica che non sono supportati. </td>
  </tr>
  <tr>
   <td>identifier.stability</td>
   <td>Indica la stabilità degli identificatori di nodo non referenziabili. Sono possibili i seguenti valori:
    <ul>
     <li>identifier.stability.indefined.duration: gli identificatori non cambiano.</li>
     <li>identifier.stability.method.duration: gli identificatori possono cambiare tra le chiamate al metodo.</li>
     <li>identifier.stability.save.duration: gli identificatori non cambiano durante un ciclo di salvataggio/aggiornamento.</li>
     <li>identifier.stability.session.duration: gli identificatori non cambiano durante una sessione.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>query.xpath.pos.index</td>
   <td>Indica se il linguaggio di query JCR 1.0 XPath è supportato. true indica il supporto e false indica l'assenza di supporto.</td>
  </tr>
  <tr>
   <td>crx.repository.systemid</td>
   <td>Identificatore di sistema trovato nel file system.id.</td>
  </tr>
  <tr>
   <td>option.query.sql.supported</td>
   <td>Indica se il linguaggio di query JCR 1.0 XPath è supportato. true indica il supporto e false indica l'assenza di supporto.</td>
  </tr>
  <tr>
   <td>jcr.repository.version</td>
   <td>Versione dell’implementazione dell’archivio.</td>
  </tr>
  <tr>
   <td>option.update.primary.node.type.supported</td>
   <td>Indica se il tipo di nodo principale di un nodo può essere modificato. true indica che è possibile modificare il tipo di nodo principale e false indica che la modifica non è supportata.</td>
  </tr>
  <tr>
   <td>option.node.type.management.supported</td>
   <td>Indica se la gestione del tipo di nodo è supportata. true indica che è supportato, mentre false indica che non è supportato.</td>
  </tr>
  <tr>
   <td>node.type.management.overrides.supported</td>
   <td>Indica se è possibile ignorare la proprietà ereditata o la definizione di nodo figlio di un tipo di nodo. true indica che le sostituzioni sono supportate e false indica che non sono supportate.</td>
  </tr>
  <tr>
   <td>option.observation.supported</td>
   <td>true indica che è supportata l’osservazione asincrona delle modifiche dell’archivio. Il supporto dell’osservazione asincrona consente alle applicazioni di ricevere e rispondere alle notifiche di ogni modifica nel momento in cui si verifica.</td>
  </tr>
  <tr>
   <td>query.jcrscore</td>
   <td><p>true indica che la pseudo-proprietà jcr:score è disponibile nelle query XPath e SQL che includono una funzione jcrfn:contains (in XPath) o CONTAINS (in SQL) per eseguire una ricerca full-text.</p> </td>
  </tr>
  <tr>
   <td>option.simple.versioning.supported</td>
   <td>true indica che l'archivio supporta il controllo delle versioni semplice. Con un semplice controllo delle versioni, l’archivio mantiene una serie sequenziale di versioni di un nodo.</td>
  </tr>
  <tr>
   <td>option.workspace.management.supported</td>
   <td>true indica che l’archivio supporta la creazione e l’eliminazione delle aree di lavoro tramite API.</td>
  </tr>
  <tr>
   <td>option.update.mixin.node.types.supported</td>
   <td>true indica che l'archivio supporta l'aggiunta e la rimozione di tipi di nodo mixin di un nodo esistente.</td>
  </tr>
  <tr>
   <td>node.type.management.primary.item.name.supported</td>
   <td>true indica che il repository consente alle definizioni dei nodi di contenere un elemento primario come elemento secondario. Un elemento primario è accessibile utilizzando l’API senza conoscere il nome dell’elemento.</td>
  </tr>
  <tr>
   <td>level.2.supported</td>
   <td>true indica che LEVEL_1_SUPPORTED e OPTION_XML_IMPORT_SUPPORTED sono entrambi true.</td>
  </tr>
  <tr>
   <td>write.supported</td>
   <td>true indica che l’archivio fornisce accesso in scrittura utilizzando l’API. false indica l'accesso in sola lettura.</td>
  </tr>
  <tr>
   <td>node.type.management.update.in.use.supported</td>
   <td>true indica che è possibile modificare le definizioni dei nodi utilizzate dai nodi esistenti.</td>
  </tr>
  <tr>
   <td>jcr.specification.version</td>
   <td>Versione della specifica JCR implementata dall’archivio.</td>
  </tr>
  <tr>
   <td>option.journaled.observation.supported</td>
   <td>true indica che le applicazioni possono eseguire l'osservazione dell'archivio registrata. con l'osservazione nel diario, è possibile ottenere una serie di notifiche di modifica per un periodo di tempo specifico. </td>
  </tr>
  <tr>
   <td>query.languages</td>
   <td>I linguaggi di query supportati dall’archivio. Nessun valore indica che non è supportata alcuna query.</td>
  </tr>
  <tr>
   <td>option.xml.export.supported</td>
   <td>true indica che il repository supporta l'esportazione di nodi come codice XML.</td>
  </tr>
  <tr>
   <td>node.type.management.multiple.binary.properties.supported</td>
   <td>true indica che l'archivio supporta la registrazione di tipi di nodo con più proprietà binarie. false indica che è supportata una singola proprietà binaria per un tipo di nodo.</td>
  </tr>
  <tr>
   <td>option.access.control.supported</td>
   <td>true indica che il repository supporta il controllo degli accessi per l'impostazione e la determinazione dei privilegi utente per l'accesso ai nodi.</td>
  </tr>
  <tr>
   <td>option.baselines.supported</td>
   <td>true indica che l'archivio supporta sia le configurazioni che le linee di base.</td>
  </tr>
  <tr>
   <td>option.shareable.nodes.supported</td>
   <td>true indica che l'archivio supporta la creazione di nodi condivisibili.</td>
  </tr>
  <tr>
   <td>crx.cluster.id</td>
   <td>Identificatore del cluster di repository.</td>
  </tr>
  <tr>
   <td>query.stored.queries.supported</td>
   <td>true indica che l'archivio supporta le query archiviate.</td>
  </tr>
  <tr>
   <td>query.full.text.search.supported</td>
   <td>true indica che l'archivio supporta la ricerca full-text.</td>
  </tr>
  <tr>
   <td>node.type.management.inheritance</td>
   <td><p>Indica il livello di supporto dell’archivio per l’ereditarietà del tipo di nodo. Sono possibili i seguenti valori:</p> <p>node.type.management.inheritance.minimal: la registrazione dei tipi di nodo primario è limitata a quelli che hanno solo nt:base come supertipo. La registrazione dei tipi di nodo mixin è limitata a quelli senza supertipo.</p> <p>node.type.management.inheritance.single: la registrazione dei tipi di nodo primario è limitata a quelli con un supertipo. La registrazione dei tipi di nodo mixin è limitata a quelli con al massimo un supertipo.</p> <p><br /> node.type.management.inheritance.multiple: i tipi di nodo primari possono essere registrati con uno o più supertipi. I tipi di nodo mixin possono essere registrati con zero o più supertipi.</p> </td>
  </tr>
  <tr>
   <td>crx.cluster.preferredMaster</td>
   <td>true indica che questo nodo cluster è il master preferito del cluster.</td>
  </tr>
  <tr>
   <td>option.transactions.supported</td>
   <td>true indica che il repository supporta le transazioni.</td>
  </tr>
  <tr>
   <td>jcr.repository.vendor.url</td>
   <td>URL del fornitore del repository.</td>
  </tr>
  <tr>
   <td>node.type.management.value.constraints.supported</td>
   <td>true indica che l'archivio supporta vincoli di valore per le proprietà dei nodi.</td>
  </tr>
  <tr>
   <td>node.type.management.property.types</td>
   <td>matrice di costanti javax.jcr.PropertyType che rappresentano i tipi di proprietà che un tipo di nodo registrato può specificare. Una matrice di lunghezza zero indica che i tipi di nodo registrati non possono specificare definizioni di proprietà. I tipi di proprietà sono STRING, URI, BOOLEAN, LONG, DOUBLE, DECIMAL, BINARY, DATE, NAME, PATH, WEAKREFERENCE, REFERENCE e UNDEFINED (se supportato)</td>
  </tr>
  <tr>
   <td>node.type.management.orderable.child.nodes.supported</td>
   <td>true indica che l'archivio supporta il mantenimento dell'ordine dei nodi figlio.</td>
  </tr>
  <tr>
   <td>jcr.repository.vendor</td>
   <td>Nome del fornitore del repository.</td>
  </tr>
  <tr>
   <td>query.joins</td>
   <td><p>Livello di supporto per i join nelle query. Sono possibili i seguenti valori:</p>
    <ul>
     <li>query.joins.none: nessun supporto per i join. Nelle query è possibile utilizzare un solo selettore.</li>
     <li>query.joins.inner: supporto per inner join.</li>
     <li>query.joins.inner.outer: supporto per join interni ed esterni.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>org.apache.jackrabbit.spi.commons.AdditionalEventInfo</td>
   <td> </td>
  </tr>
  <tr>
   <td>query.xpath.doc.order</td>
   <td>true indica che l'archivio supporta il linguaggio di query XPath 1.0.</td>
  </tr>
  <tr>
   <td>query.jcrpath</td>
   <td> </td>
  </tr>
  <tr>
   <td>option.xml.import.supported</td>
   <td>true indica che il repository supporta l'importazione di codice XML come contenuto.</td>
  </tr>
  <tr>
   <td>node.type.management.same.name.siblings.supported</td>
   <td>true indica che l'archivio supporta nodi di pari livello (nodi con lo stesso elemento padre) con gli stessi nomi.</td>
  </tr>
  <tr>
   <td>node.type.management.residual.definitions.supported</td>
   <td>true indica che l'archivio supporta le proprietà dei nomi con definizioni residue. Se supportato, l'attributo name di una definizione di elemento può essere un asterisco ("*").</td>
  </tr>
  <tr>
   <td>node.type.management.autocreated.definitions.supported</td>
   <td>true indica che l'archivio supporta la creazione automatica di elementi secondari (nodi o proprietà) di un nodo al momento della creazione del nodo.</td>
  </tr>
  <tr>
   <td>crx.cluster.master</td>
   <td>true indica che questo nodo di repository è il nodo principale del cluster.</td>
  </tr>
  <tr>
   <td>level.1.supported</td>
   <td>true indica che option.xml.export.support è true e query.Languages è di lunghezza diversa da zero.</td>
  </tr>
  <tr>
   <td>option.unfiled.content.supported</td>
   <td>true indica che l'archivio supporta il contenuto non archiviato. I nodi non archiviati non fanno parte della gerarchia dell’archivio.</td>
  </tr>
  <tr>
   <td>jcr.specification.name</td>
   <td>Nome della specifica JCR implementata dall’archivio.</td>
  </tr>
  <tr>
   <td>option.versioning.supported</td>
   <td>true indica che l'archivio supporta il controllo delle versioni complete.</td>
  </tr>
  <tr>
   <td>jcr.repository.name</td>
   <td>Nome dell’archivio.</td>
  </tr>
  <tr>
   <td>option.locking.supported</td>
   <td>true indica che l'archivio supporta il blocco dei nodi. Il blocco consente a un utente di impedire temporaneamente ad altri utenti di apportare modifiche.</td>
  </tr>
  <tr>
   <td>jcr.repository.version.display</td>
   <td> </td>
  </tr>
  <tr>
   <td>option.activities.supported</td>
   <td>true indica che l'archivio supporta le attività. Le attività sono un insieme di modifiche eseguite in un’area di lavoro e unite a un’altra area di lavoro.</td>
  </tr>
  <tr>
   <td>node.type.management.multivalued.properties.supported</td>
   <td>true indica che l'archivio supporta proprietà del nodo che possono avere zero o più valori.</td>
  </tr>
  <tr>
   <td>option.retention.supported</td>
   <td>true indica che l'archivio supporta l'utilizzo di applicazioni di gestione della conservazione esterne per applicare i criteri di conservazione ai contenuti e supporta il blocco e il rilascio.</td>
  </tr>
  <tr>
   <td>option.lifecycle.supported</td>
   <td>true indica che l'archivio supporta la gestione del ciclo di vita.</td>
  </tr>
 </tbody>
</table>

**WorkspaceNames** Nomi delle aree di lavoro nel repository. Sola lettura.

**DataStoreGarbageCollectionDelay** Quantità di tempo, in millisecondi, in cui la raccolta di oggetti inattivi sospende la scansione ogni decimo nodo. Lettura/scrittura.

**RitardoBackup** Tempo, in millisecondi, di sospensione del processo di backup tra ogni passaggio del backup. Lettura/scrittura.

**Backup in corso** Il valore true indica che è in esecuzione un processo di backup. Sola lettura.

**AvanzamentoBackup** Per il backup corrente, la percentuale di tutti i file di cui è stato eseguito il backup. Sola lettura.

**CurrentBackupTarget** Per il backup corrente, il file ZIP in cui vengono archiviati i file di backup. Quando non è in corso un backup, non viene visualizzato alcun valore. Sola lettura.

**BackupWasSuccessful** Il valore true indica che non si sono verificati errori durante il backup corrente o che non è in corso alcun backup. false indica che si è verificato un errore durante il backup corrente. Sola lettura.

**BackupResult** Stato del backup corrente. Sono possibili i seguenti valori:

* Backup in corso: è in corso un backup.
* Backup annullato: backup annullato.
* Backup completato con errore: si è verificato un errore durante il backup. Il messaggio di errore fornisce informazioni sulla causa.
* Backup completato: backup completato.
* Nessun backup eseguito finora: nessun backup in corso.

Sola lettura.

**TarOptimizationRunningSince** Ora di inizio del processo di ottimizzazione del file TAR corrente. Sola lettura.

**TarOptimizationDelay** Il tempo, in millisecondi, di sospensione del processo di ottimizzazione TAR tra ogni fase del processo. Lettura/scrittura.

**ProprietàCluster** Un insieme di coppie chiave-valore che rappresentano proprietà e valori del cluster. Ogni riga della tabella rappresenta una proprietà cluster. Sola lettura.

**ClusterNodes** Membri del cluster di repository.

**ClusterId** Identificatore di questo cluster di repository. Sola lettura.

**ClusterMasterId** Identificatore del nodo principale di questo cluster di repository. Sola lettura.

**ClusterNodeId** Identificatore di questo nodo del cluster di repository. Sola lettura.

### Operazioni {#operations-1}

**createWorkspace** Crea un&#39;area di lavoro in questo repository.

* Argomenti:

   * name (nome): valore String che rappresenta il nome della nuova area di lavoro.

* Valore restituito: nessuno

**runDataStoreGarbageCollection** Esegue la Garbage Collection sui nodi dell&#39;archivio.

* Argomenti:

   * delete: Valore booleano che indica se eliminare gli elementi del repository non utilizzati. Il valore true determina l&#39;eliminazione dei nodi e delle proprietà non utilizzati. Se si imposta il valore false, tutti i nodi vengono analizzati ma nessuno viene eliminato.

* Valore restituito: nessuno

**stopDataStoreGarbageCollection** Arresta una raccolta di oggetti inattivi dell&#39;archivio dati in esecuzione.

* Argomenti: nessuno
* Valore restituito: rappresentazione stringa dello stato corrente

**startBackup** Esegue il backup dei dati del repository in un file ZIP.

* Argomenti:

   * `target`: (Facoltativo) A `String` valore che rappresenta il nome del file ZIP o della directory in cui archiviare i dati del repository. Per utilizzare un file ZIP, Includi l’estensione del nome del file ZIP. Per utilizzare una directory, non includere alcuna estensione di file.

     Per eseguire un backup incrementale, specificare la directory utilizzata in precedenza per il backup.

     È possibile specificare un percorso assoluto o relativo. I percorsi relativi sono relativi alla directory principale della directory crx-quickstart.

     Se non specificate alcun valore, il valore predefinito è `backup-currentdate.zip` viene utilizzato, dove `currentdate` è nel formato `yyyyMMdd-HHmm`.

* Valore restituito: nessuno

**cancelBackup** Arresta il processo di backup corrente ed elimina l&#39;archivio temporaneo creato dal processo per l&#39;archiviazione dei dati.

* Argomenti: nessuno
* Valore restituito: nessuno

**blockRepositoryWrites** Blocca le modifiche ai dati del repository. Il blocco viene notificato a tutti i listener di backup dell’archivio.

* Argomenti: nessuno
* Valore restituito: nessuno

**unblockRepositoryWrites** Rimuove il blocco dal repository. Tutti i listener di backup dell’archivio ricevono una notifica della rimozione del blocco.

* Argomenti: nessuno
* Valore restituito: nessuno

**startTarOptimization** Avvia il processo di ottimizzazione del file TAR utilizzando il valore predefinito per tarOptimizationDelay.

* Argomenti: nessuno
* Valore restituito: nessuno

**stopTarOptimization** Interrompe l&#39;ottimizzazione del file TAR.

* Argomenti: nessuno
* Valore restituito: nessuno

**tarIndexMerge** Unisce i file di indice principali di tutti i set TAR. I file di indice principali sono file con versioni principali diverse. Ad esempio, i seguenti file vengono uniti nel file index_3_1.tar: index_1_1.tar, index_2_0.tar, index_3_0.tar. I file che sono stati uniti vengono eliminati (nell&#39;esempio precedente, index_1_1.tar, index_2_0.tar e index_3_0.tar vengono eliminati).

* Argomenti:

   * `background`: valore booleano che indica se eseguire l’operazione in background in modo che la console web sia utilizzabile durante l’esecuzione. Il valore true esegue l&#39;operazione in background.

* Valore restituito: nessuno

**transformClusterMaster** Imposta questo nodo del repository come nodo principale del cluster. Se non è già master, questo comando arresta il listener dell&#39;istanza master corrente e avvia un listener master sul nodo corrente. Questo nodo viene quindi impostato come nodo principale e riavviato, causando la connessione a questa istanza di tutti gli altri nodi del cluster, ovvero quelli controllati dal nodo principale.

* Argomenti: nessuno
* Valore restituito: nessuno

**joinCluster** Aggiunge questo repository a un cluster come nodo controllato dal cluster master. Fornisci un nome utente e una password per scopi di autenticazione. La connessione utilizza l’autenticazione di base. Le credenziali di sicurezza sono codificate in base 64 prima di essere inviate al server.

* Argomenti:

   * `master`: valore stringa che rappresenta l’indirizzo IP o il nome del computer che esegue il nodo dell’archivio master.
   * `username`: nome da utilizzare per l&#39;autenticazione con il cluster.
   * `password`: password da utilizzare per l’autenticazione.

* Valore restituito: nessuno

**traversalCheck** Attraversa e, facoltativamente, corregge le incoerenze in una sottostruttura che inizia in un nodo specifico. Questo è trattato in modo dettagliato nella documentazione su Persistence Manager.

**consistencyCheck** Controlla e, facoltativamente, corregge la coerenza nell’archivio dati. Questo è trattato in modo dettagliato nella documentazione sull’archivio dati.

## Statistiche archivio (TimeSeries) {#repository-statistics-timeseries}

Il valore del campo TimeSeries per ogni tipo di statistica che `org.apache.jackrabbit.api.stats.RepositoryStatistics` definisce.

* Dominio: `com.adobe.granite`
* Tipo: `TimeSeries`
* Name (Nome): uno dei seguenti valori del `org.apache.jackrabbit.api.stats.RepositoryStatistics.Type` Classe enum:

   * BUNDLE_CACHE_ACCESS_COUNTER
   * BUNDLE_CACHE_MISS_AVERAGE
   * BUNDLE_CACHE_MISS_COUNTER
   * BUNDLE_CACHE_MISS_DURATION
   * BUNDLE_CACHE_SIZE_COUNTER
   * BUNDLE_COUNTER
   * BUNDLE_READ_COUNTER
   * BUNDLE_WRITE_AVERAGE
   * CONTATORE_SCRITTURA_BUNDLE
   * BUNDLE_WRITE_DURATION
   * CONTATORE_DIMENSIONI_BUNDLE
   * MEDIA_QUERY
   * CONTEGGIO_QUERY
   * QUERY_DURATION
   * SESSION_COUNT
   * SESSION_LOGIN_COUNTER
   * SESSION_READ_AVERAGE
   * SESSION_READ_COUNTER
   * SESSION_READ_DURATION
   * SESSION_WRITE_AVERAGE
   * SESSION_WRITE_COUNTER
   * SESSION_WRITE_DURATION

### Attributi {#attributes-1}

Per ogni tipo di statistica segnalato sono forniti i seguenti attributi:

* ValuePerSecond: valore misurato al secondo nell&#39;ultimo minuto. Sola lettura.
* ValuePerMinute: valore al minuto misurato nell&#39;ultima ora. Sola lettura.
* ValuePerHour: valore misurato per ora nell&#39;ultima settimana. Sola lettura.
* ValuePerWeek: valore misurato per settimana negli ultimi tre anni. Sola lettura.

## Statistiche query archivio {#repository-query-stats}

Informazioni statistiche sulle query dell’archivio.

* Dominio: com.adobe.granite
* Tipo: QueryStat

### Attributi {#attributes-2}

**SlowQueries** Informazioni sulle query dell’archivio che hanno richiesto più tempo per essere completate. Sola lettura.

**SlowQueriesQueueSize** Numero massimo di query da includere nell&#39;elenco SlowQueries. Lettura/scrittura.

**PopularQuery** Informazioni sulle query dell’archivio più frequenti. Sola lettura.

**PopularQueriesQueueSize** Numero massimo di query nell&#39;elenco PopularQueries. Lettura/scrittura.

### Operazioni {#operations-2}

**clearSlowQueriesQueue** Rimuove tutte le query dall&#39;elenco SlowQueries.

* Argomenti: nessuno
* Valore restituito: nessuno

**clearPopularQueriesQueue** Rimuove tutte le query dall&#39;elenco PopularQueries.

* Argomenti: nessuno
* Valore restituito: nessuno

## Agenti di replica {#replication-agents}

Monitora i servizi per ogni agente di replica. Quando crei un agente di replica, il servizio viene visualizzato automaticamente nella console JMX.

* **Dominio:** com.adobe.granite.replication
* **Tipo:** agente
* **Nome:** nessun valore
* **Proprietà:** {id=&quot;*Nome*&quot;}, dove *Nome* è il valore della proprietà Nome agente.

### Attributi {#attributes-3}

**ID** Valore String che rappresenta l&#39;identificatore della configurazione dell&#39;agente di replica. Più agenti possono utilizzare la stessa configurazione. Sola lettura.

**Valido** Valore booleano che indica se l’agente è configurato correttamente:

* `true`: configurazione valida.
* `false` : la configurazione contiene errori.

Sola lettura.

**Abilitato** Valore booleano che indica se l’agente è abilitato:

* `true`: abilitato.
* `false`: disattivato.

**QueueBlocked** Valore booleano che indica se la coda esiste ed è bloccata:

* `true`: bloccato. Un nuovo tentativo automatico è in sospeso.
* `false`: non bloccato o inesistente.

Sola lettura.

**QueuePaused** Valore booleano che indica se la coda dei processi è in pausa:

* `true`: in pausa (sospeso)
* `false`: non in pausa o inesistente.

Lettura/scrittura.

**QueueNumEntries** Valore int che rappresenta il numero di processi nella coda dell&#39;agente. Sola lettura.

**OraStatoCoda** Un valore di data che indica l&#39;ora sul server in cui sono stati ottenuti i valori di stato visualizzati. Il valore corrisponde all’ora in cui è stata caricata la pagina. Sola lettura.

**QueueNextRetryTime** Per le code bloccate, un valore Date che indica quando si verifica il nuovo tentativo automatico successivo. Quando non viene visualizzato alcun orario, la coda non viene bloccata. Sola lettura.

**QueueProcessingSince** Valore di tipo Date che indica quando è iniziata l&#39;elaborazione per il processo corrente. Quando non viene visualizzato alcun orario, la coda è bloccata o inattiva. Sola lettura.

**QueueLastProcessTime** Valore data che indica quando è stato completato il processo precedente. Sola lettura.

### Operazioni {#operations-3}

**queueForceRetry** Per le code bloccate, invia alla coda il comando Riprova.

* Argomenti: nessuno
* Valore restituito: nessuno

**queueClear** Rimuove tutti i processi dalla coda.

* Argomenti: nessuno
* Valore restituito: nessuno

## Motore Sling {#sling-engine}

Fornisce statistiche sulle richieste HTTP in modo da poter monitorare le prestazioni del servizio SlingRequestProcessor.

* Dominio: org.apache.sling
* Tipo: motore
* Proprietà: {service=RequestProcessor}

### Attributi {#attributes-4}

**RequestsCount** Il numero di richieste che si sono verificate dall’ultima reimpostazione delle statistiche.

**MinRequestDurationMsec** Il tempo più breve (in millisecondi) necessario per elaborare una richiesta dall’ultima reimpostazione delle statistiche.

**MaxRequestDurationMsec** Il tempo più lungo (in millisecondi) necessario per elaborare una richiesta dall&#39;ultima reimpostazione delle statistiche.

**StandardDeviationDurationMsec** Deviazione standard della quantità di tempo necessaria per elaborare le richieste. La deviazione standard viene calcolata utilizzando tutte le richieste dall’ultima reimpostazione delle statistiche.

**MediaRequestDurationMsec** Il tempo medio necessario per elaborare una richiesta. La media viene calcolata utilizzando tutte le richieste dall’ultima reimpostazione delle statistiche

### Operazioni {#operations-4}

**resetStatistics** Imposta tutte le statistiche su zero. Reimposta le statistiche quando devi analizzare le prestazioni di elaborazione delle richieste durante un intervallo di tempo specifico.

* Argomenti: nessuno
* Valore restituito: nessuno

**id** Rappresentazione stringa dell&#39;ID pacchetto.

**installato** Valore booleano che indica se il pacchetto è installato:

* `true`: installato.
* `false`: non installato.

**installBy** ID dell’ultimo utente che ha installato il pacchetto.

**installedDate** Data dell&#39;ultima installazione del pacchetto.

**dimensione** Valore lungo che contiene le dimensioni del pacchetto in byte.


## Avvio rapido {#quickstart-launcher}

Informazioni sul processo di avvio e sul modulo di avvio Quickstart.

* Dominio: com.adobe.granite.quickstart
* Tipo: modulo di avvio

### Operazioni {#operations-5}

**log**

Visualizza un messaggio nella finestra QuickStart.

Argomenti:

* p1: A `String` valore che rappresenta il messaggio da visualizzare.
* Valore restituito: nessuno

**startupFinished**

Chiama il metodo startupFinished del modulo di avvio del server. Il metodo tenta di aprire la pagina di benvenuto in un browser Web.

* Argomenti: nessuno
* Valore restituito: nessuno

**startupProgress**

Imposta il valore di completamento del processo di avvio del server. La barra di avanzamento nella finestra QuickStart rappresenta il valore di completamento.

* Argomenti:
   * p1: Valore float che rappresenta la frazione di completamento del processo di avvio. Il valore deve essere compreso tra zero e uno. Ad esempio, 0,3 indica 30% completato.
* Valore restituito: nessuno.

## Servizi di terze parti {#third-party-services}

Diverse risorse server di terze parti installano MBean che espongono attributi e operazioni alla console JMX. Nella tabella seguente sono elencate le risorse di terze parti e sono disponibili collegamenti a ulteriori informazioni.

<table>
 <tbody>
  <tr>
   <th>Dominio</th>
   <th>Tipo</th>
   <th>Classe MBean</th>
  </tr>
  <tr>
   <td>Implementazione JMI</td>
   <td>MBeanServerDelegate</td>
   <td><a href="https://docs.oracle.com/javase/8/docs/api/javax/management/MBeanServerDelegate.html">javax.management.MBeanServerDelegate</a></td>
  </tr>
  <tr>
   <td>com.sun.management</td>
   <td>HotSpotDiagnostic</td>
   <td><a href="https://docs.oracle.com/javase/8/docs/jre/api/management/extension/com/sun/management/HotSpotDiagnosticMXBean.html">com.sun.management.HotSpotDiagnosticMXBean</a></td>
  </tr>
  <tr>
   <td>java.lang</td>
   <td>
    <ul>
     <li>ClassLoading</li>
     <li>Compilazione</li>
     <li>GarbageCollector</li>
     <li>Memoria</li>
     <li>MemoryManager</li>
     <li>MemoryPool</li>
     <li>OperatingSystem</li>
     <li>Runtime</li>
     <li>Threading</li>
    </ul> </td>
   <td><a href="https://docs.oracle.com/javase/8/docs/api/javax/management/package-summary.html">javax.management</a> pacchetto</td>
  </tr>
  <tr>
   <td>java.util.logging</td>
   <td> </td>
   <td><a href="https://docs.oracle.com/javase/8/docs/api/java/util/logging/LoggingMXBean.html">java.util.logging.LoggingMXBean</a></td>
  </tr>
  <tr>
   <td>osgi.core</td>
   <td>
    <ul>
     <li>bundleState</li>
     <li>framework</li>
     <li>packageState</li>
     <li>serviceState</li>
    </ul> </td>
   <td><a href="https://osgi.org/specification/osgi.enterprise/7.0.0/service.jmx.html#d0e42567">org.osgi.jmx.framework</a> pacchetto</td>
  </tr>
 </tbody>
</table>

## Utilizzo della console JMX {#using-the-jmx-console}

La console JMX visualizza informazioni su diversi servizi in esecuzione sul server:

* Attributi: proprietà del servizio come configurazioni o dati di runtime. Gli attributi possono essere di sola lettura o di lettura/scrittura.
* Operazioni: comandi che è possibile richiamare sul servizio.

Gli MBean distribuiti con un servizio OSGi espongono gli attributi e le operazioni del servizio alla console. MBean determina gli attributi e le operazioni esposte e se gli attributi sono di sola lettura o di lettura/scrittura.

La pagina principale della console JMX include una tabella di servizi. Ogni riga della tabella rappresenta un servizio esposto da un MBean.

1. Apri la console Web e fai clic sulla scheda JMX. ([http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
2. Fare clic su un valore di cella per un servizio per visualizzare gli attributi e le operazioni del servizio.
3. Per modificare il valore di un attributo, fare clic sul valore, specificarlo nella finestra di dialogo visualizzata e fare clic su Salva.
4. Per richiamare un&#39;operazione di servizio, fare clic sul nome dell&#39;operazione, specificare i valori degli argomenti nella finestra di dialogo visualizzata e fare clic su Richiama.

## Utilizzo di applicazioni JMX esterne per il monitoraggio {#using-external-jmx-applications-for-monitoring}

CRX consente alle applicazioni esterne di interagire con Managed Beans (MBean) tramite [Estensioni di gestione Java (JMX)](https://docs.oracle.com/javase/6/docs/technotes/guides/management/overview.html). Utilizzo di console generiche come [JConsole](https://java.sun.com/developer/technicalArticles/J2SE/jconsole.html) o applicazioni di monitoraggio specifiche per il dominio, consente di ottenere e impostare configurazioni e proprietà CRX e il monitoraggio delle prestazioni e dell’utilizzo delle risorse.

### Utilizzo di JConsole per la connessione a CRX {#using-jconsole-to-connect-to-crx}

Per connettersi a CRX utilizzando JConsole, effettuare le seguenti operazioni:

1. Apri una finestra del terminale.
1. Immetti il comando seguente:

   `jconsole`

Verrà avviata la console JConsole e verrà visualizzata la finestra JConsole.

### Connessione a un processo CRX locale {#connecting-to-a-local-crx-process}

In JConsole verrà visualizzato un elenco di processi di Java Virtual Machine locali. L’elenco conterrà due processi di avvio rapido. Selezionare il processo quickstart &quot;CHILD&quot; dall&#39;elenco dei processi locali (in genere quello con il PID più alto).

![screen_shot_2012-03-26at114557am](assets/screen_shot_2012-03-26at114557am.png)

### Connessione a un processo CRX remoto {#connecting-to-a-remote-crx-process}

Per connettersi a un processo CRX remoto, la JVM che ospita il processo CRX remoto deve essere abilitata per accettare connessioni JMX remote.

Per abilitare le connessioni JMX remote, è necessario impostare la seguente proprietà di sistema all&#39;avvio della JVM:

`com.sun.management.jmxremote.port=portNum`

Nella proprietà precedente, `portNum` è il numero di porta attraverso il quale si desidera abilitare le connessioni RMI JMX. Assicurarsi di specificare un numero di porta non utilizzato. Oltre a pubblicare un connettore RMI per l&#39;accesso locale, l&#39;impostazione di questa proprietà consente di pubblicare un connettore RMI aggiuntivo in un registro privato di sola lettura sulla porta specificata utilizzando un nome noto, &quot;jmxrmi&quot;.

Per impostazione predefinita, quando si abilita l&#39;agente JMX per il monitoraggio remoto, viene utilizzata l&#39;autenticazione tramite password basata su un file di password che deve essere specificato utilizzando la seguente proprietà di sistema all&#39;avvio della VM Java:

`com.sun.management.jmxremote.password.file=pwFilePath`

Consulta la [documentazione JMX rilevante](https://docs.oracle.com/javase/6/docs/technotes/guides/management/agent.html) per istruzioni dettagliate sulla configurazione di un file di password.

Esempio:

```shell
$ java
  -Dcom.sun.management.jmxremote.password.file=pwFilePath
  -Dcom.sun.management.jmxremote.port=8463
  -jar ./cq-quickstart.jar
```

### Utilizzo degli MBean forniti da CRX {#using-the-mbeans-provided-by-crx}

Dopo la connessione al processo quickstart, JConsole fornisce una serie di strumenti generali di monitoraggio per la JVM in cui CRX è in esecuzione.

![screen_shot_2012-03-26at115056am](assets/screen_shot_2012-03-26at115056am.png)

Per accedere alle opzioni di monitoraggio e configurazione interne di CRX, vai alla scheda MBean e, dalla struttura gerarchica del contenuto a sinistra, seleziona la sezione Attributi o operazioni a cui sei interessato. Ad esempio, la sezione com.adobe.granite/Repository/Operations.

All’interno di tale sezione, seleziona l’attributo o l’operazione desiderata nel riquadro a sinistra.

![screen_shot_2012-03-26at115728am](assets/screen_shot_2012-03-26at115728am.png)
