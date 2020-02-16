---
title: Risorse di Monitoring Server tramite la console JMX
seo-title: Risorse di Monitoring Server tramite la console JMX
description: Scoprite come monitorare le risorse del server mediante la console JMX.
seo-description: Scoprite come monitorare le risorse del server mediante la console JMX.
uuid: 0a28aafe-61b2-472b-8f8f-2cd6540cbfee
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 873ce073-0055-4e1b-b3c6-ae7967700894
docset: aem65
translation-type: tm+mt
source-git-commit: a268b7046430cc17c8b59b9306cf3533d73bb4a2

---


# Risorse di Monitoring Server tramite la console JMX{#monitoring-server-resources-using-the-jmx-console}

La console JMX consente di monitorare e gestire i servizi sul server CRX. Le sezioni che seguono riassumono gli attributi e le operazioni esposti attraverso il framework JMX.

Per informazioni sull’utilizzo dei controlli console, consultate [Utilizzo della console](#using-the-jmx-console)JMX. Per informazioni di base su JMX, vedere la pagina Tecnologia [JMX (](https://www.oracle.com/technetwork/java/javase/tech/javamanagement-140525.html) Java Management Extensions) nel sito Web Oracle.

Per informazioni sulla creazione di MBeans per gestire i servizi tramite la console JMX, consulta [Integrazione dei servizi con la console](/help/sites-developing/jmx-integration.md)JMX.

## Manutenzione del flusso di lavoro {#workflow-maintenance}

Operazioni per l’amministrazione di istanze di flussi di lavoro in esecuzione, completate, non aggiornate e non riuscite.

* Dominio: com.adobe.granite.workflow
* Tipo: Manutenzione

>[!NOTE]
>
>Consultate la console [del](/help/sites-administering/workflows-administering.md) flusso di lavoro per ulteriori strumenti di amministrazione del flusso di lavoro e le descrizioni dei possibili stati delle istanze del flusso di lavoro.

### Operazioni {#operations}

**listRunningWorkflowsPerModel** Mostra il numero di istanze del flusso di lavoro in esecuzione per ciascun modello di workflow.

* Argomenti: none
* Valore restituito: Dati tabulari contenenti le colonne Count e ModelId.

**listCompletedWorkflowsPerModel** Elenca il numero di istanze del flusso di lavoro completate per ciascun modello di workflow.

* Argomenti: none
* Valore restituito: Dati tabulari contenenti le colonne Count e ModelId.

**returnWorkflowQueueInfo** Elenca le informazioni sugli elementi del flusso di lavoro elaborati e in coda per l’elaborazione.

* Argomenti: none
* Valore restituito: Dati della tabella contenenti le colonne seguenti:

   * Processi
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

* Argomenti: none
* Valore restituito: Dati tabulari contenenti le colonne seguenti:

   * Nome argomento
   * Tempo medio di elaborazione
   * Tempo medio di attesa
   * Lavori annullati
   * Lavori con errori
   * Processi completati
   * Processi elaborati

**returnFailedWorkflowCount** Mostra il numero di istanze del flusso di lavoro che hanno avuto esito negativo. Potete specificare un modello di workflow per eseguire query o recuperare informazioni per tutti i modelli di workflow.

* Argomenti:

   * modello: ID del modello da interrogare. Per visualizzare un totale di istanze del flusso di lavoro non riuscite per tutti i modelli di workflow, non specificate alcun valore. L&#39;ID è il percorso del nodo del modello, ad esempio:

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valore restituito: Numero di istanze del flusso di lavoro non riuscite.

**returnFailedWorkflowCountPerModel** Mostra il numero di istanze del flusso di lavoro che non sono riuscite per ciascun modello di workflow.

* Argomenti: Nessuno.
* Valore restituito: Dati tabulari contenenti le colonne Count e Model ID.

**terminateFailedInstances** Terminare le istanze del flusso di lavoro che hanno avuto esito negativo. È possibile terminare tutte le istanze con errore o solo quelle con errore per un modello specifico. Se necessario, è possibile riavviare le istanze dopo che sono state interrotte. È inoltre possibile testare l&#39;operazione per visualizzare i risultati senza eseguire l&#39;operazione.

* Argomenti:

   * Riavviate l’istanza: (Facoltativo) Specificare un valore per `true` riavviare le istanze dopo che sono state interrotte. Il valore predefinito di non `false` causa il riavvio delle istanze del flusso di lavoro interrotte.
   * Prova a secco: (Facoltativo) Specificate un valore di `true` per visualizzare i risultati dell&#39;operazione senza eseguire l&#39;operazione. Il valore predefinito di `false` determina l&#39;esecuzione dell&#39;operazione.
   * Modello: (Facoltativo) L&#39;ID del modello a cui viene applicata l&#39;operazione. Non specificare alcun modello per applicare l&#39;operazione alle istanze non riuscite di tutti i modelli di workflow. L&#39;ID è il percorso del nodo del modello, ad esempio:

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valore restituito: Dati della tabella sulle istanze che vengono interrotte, contenenti le colonne seguenti:

   * Iniziatore
   * InstanceId
   * ModelId
   * Payload
   * StartComment
   * WorkflowTitle

**tryFailedWorkItems** Tenta di eseguire i passaggi degli elementi di lavoro che hanno avuto esito negativo. È possibile riprovare con tutti gli elementi di lavoro non riusciti o solo con gli elementi di lavoro non riusciti per un modello di flusso di lavoro specifico. È possibile verificare l&#39;operazione per visualizzare i risultati senza eseguire l&#39;operazione.

* Argomenti:

   * Prova a secco: (Facoltativo) Specificate un valore di `true` per visualizzare i risultati dell&#39;operazione senza eseguire l&#39;operazione. Il valore predefinito di `false` determina l&#39;esecuzione dell&#39;operazione.
   * Modello: (Facoltativo) L&#39;ID del modello a cui viene applicata l&#39;operazione. Non specificare alcun modello per applicare l&#39;operazione agli elementi di lavoro non riusciti di tutti i modelli di workflow. L&#39;ID è il percorso del nodo del modello, ad esempio:

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valore restituito: Dati della tabella relativi agli elementi di lavoro non riusciti che vengono riprovati, comprese le colonne seguenti:

   * Iniziatore
   * InstanceId
   * ModelId
   * Payload
   * StartComment
   * WorkflowTitle

**PurgeActive** Rimuove le istanze attive del flusso di lavoro di una pagina specifica. Potete eliminare le istanze attive per tutti i modelli o solo per le istanze di un modello specifico. Facoltativamente, è possibile testare l&#39;operazione per visualizzare i risultati senza eseguire l&#39;operazione.

* Argomenti:

   * Modello: (Facoltativo) L&#39;ID del modello a cui viene applicata l&#39;operazione. Non specificare alcun modello per applicare l&#39;operazione alle istanze del flusso di lavoro di tutti i modelli di workflow. L&#39;ID è il percorso del nodo del modello, ad esempio:

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * Numero di giorni dall&#39;avvio del flusso di lavoro: Età delle istanze del flusso di lavoro da eliminare, espressa in giorni.
   * Prova a secco: (Facoltativo) Specificate un valore di `true` per visualizzare i risultati dell&#39;operazione senza eseguire l&#39;operazione. Il valore predefinito di `false` determina l&#39;esecuzione dell&#39;operazione.

* Valore restituito: Dati tabulari sulle istanze del flusso di lavoro attive eliminate, comprese le colonne seguenti:

   * Iniziatore
   * InstanceId
   * ModelId
   * Payload
   * StartComment
   * WorkflowTitle

**countStaleWorkflows** Restituisce il numero di istanze del flusso di lavoro non aggiornate. Potete recuperare il numero di istanze non aggiornate per tutti i modelli di workflow o per un modello specifico.

* Argomenti:

   * Modello: (Facoltativo) L&#39;ID del modello a cui viene applicata l&#39;operazione. Non specificare alcun modello per applicare l&#39;operazione alle istanze del flusso di lavoro di tutti i modelli di workflow. L&#39;ID è il percorso del nodo del modello, ad esempio:

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valore restituito: Il numero di istanze del flusso di lavoro non aggiornate.

**RestartStaleWorkflows** Riavvia le istanze del flusso di lavoro non aggiornate. È possibile riavviare tutte le istanze obsolete o solo quelle per un modello specifico. È inoltre possibile testare l&#39;operazione per visualizzare i risultati senza eseguire l&#39;operazione.

* Argomenti:

   * Modello: (Facoltativo) L&#39;ID del modello a cui viene applicata l&#39;operazione. Non specificate alcun modello per applicare l&#39;operazione alle istanze di tutti i modelli di workflow non aggiornati. L&#39;ID è il percorso del nodo del modello, ad esempio:

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * Prova a secco: (Facoltativo) Specificate un valore di `true` per visualizzare i risultati dell&#39;operazione senza eseguire l&#39;operazione. Il valore predefinito di `false` determina l&#39;esecuzione dell&#39;operazione.

* Valore restituito: Elenco di istanze del flusso di lavoro che vengono riavviate.

**fetchModelList** Elenca tutti i modelli di workflow.

* Argomenti: none
* Valore restituito: Dati della tabella che identificano i modelli di workflow, incluse le colonne ModelId e ModelName.

**countRunningWorkflows** Restituisce il numero di istanze del flusso di lavoro in esecuzione. Potete recuperare il numero di istanze in esecuzione per tutti i modelli di workflow o per un modello specifico.

* Argomenti:

   * Modello: (Facoltativo) L&#39;ID del modello per il quale viene restituito il numero di istanze in esecuzione. Non specificate alcun modello per restituire il numero di istanze in esecuzione di tutti i modelli di workflow. L&#39;ID è il percorso del nodo del modello, ad esempio:

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valore restituito: Numero di istanze del flusso di lavoro in esecuzione.

**countCompletedWorkflows** Restituisce il numero di istanze del flusso di lavoro completate. È possibile recuperare il numero di istanze completate per tutti i modelli di workflow o per un modello specifico.

* Argomenti:

   * Modello: (Facoltativo) L&#39;ID del modello per il quale viene restituito il numero di istanze completate. Non specificare alcun modello per restituire il numero di istanze completate di tutti i modelli di workflow. L&#39;ID è il percorso del nodo del modello, ad esempio:

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`

* Valore restituito: Numero di istanze del flusso di lavoro completate.

**purgeCompleted** Rimuove dall&#39;archivio i record dei flussi di lavoro completati di una specifica età. Utilizzate questa operazione periodicamente per ridurre al minimo le dimensioni del repository quando si utilizzano intensamente i flussi di lavoro. È possibile eliminare le istanze completate per tutti i modelli o solo per le istanze di un modello specifico. Facoltativamente, è possibile testare l&#39;operazione per visualizzare i risultati senza eseguire l&#39;operazione.

* Argomenti:

   * Modello: (Facoltativo) L&#39;ID del modello a cui viene applicata l&#39;operazione. Non specificare alcun modello per applicare l&#39;operazione alle istanze del flusso di lavoro di tutti i modelli di workflow. L&#39;ID è il percorso del nodo del modello, ad esempio:

      `/conf/global/settings/workflow/models/dam/update_asset/jcr:content/model`
   * Numero di giorni dal completamento del flusso di lavoro: Numero di giorni in cui le istanze del flusso di lavoro sono state completate.
   * Prova a secco: (Facoltativo) Specificate un valore di `true` per visualizzare i risultati dell&#39;operazione senza eseguire l&#39;operazione. Il valore predefinito di `false` determina l&#39;esecuzione dell&#39;operazione.

* Valore restituito: Dati tabulari sulle istanze del flusso di lavoro completate eliminate, comprese le colonne seguenti:

   * Iniziatore
   * InstanceId
   * ModelId
   * Payload
   * StartComment
   * WorkflowTitle

## Archivio {#repository}

Informazioni sul repository CRX

* Dominio: com.adobe.granite
* Tipo: Repository

### Attributi {#attributes}

**Nome** Il nome dell&#39;implementazione dell&#39;archivio JCR. Sola lettura.

**Versione** La versione di implementazione del repository. Sola lettura.

**HomeDir** La directory in cui si trova il repository. Il percorso predefinito è &lt;QuickStart_Jar_Location>/crx-quickstart/repository. Sola lettura.

**NomeCliente** Il nome del cliente a cui viene rilasciata la licenza software. Sola lettura.

**LicenseKey** Il codice di licenza univoco per l&#39;installazione dell&#39;archivio. Sola lettura.

**AvailableDiskSpace** Lo spazio su disco disponibile per questa istanza dell&#39;archivio, in Mbyte. Sola lettura.

**MaximumNumberOfOpenFiles** Il numero di file che è possibile aprire contemporaneamente. Sola lettura.

**SessionTracker** Il valore della variabile di sistema crx.debug.session. true indica una sessione di debug. false indica una sessione normale. Lettura/scrittura.

**Descrittori** Un insieme di coppie chiave-valore che rappresentano le proprietà del repository. Tutte le proprietà sono di sola lettura.

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
   <td>Indica la stabilità degli identificatori di nodo non di riferimento. I seguenti valori sono possibili:
    <ul>
     <li>identifier.stability.indefined.term: Gli identificatori non vengono modificati.</li>
     <li>identifier.stability.method.durata: Gli identificatori possono cambiare tra le chiamate dei metodi.</li>
     <li>identifier.stability.save.Duration: Gli identificatori non vengono modificati in un ciclo di salvataggio/aggiornamento.</li>
     <li>identifier.stability.session.durata: Gli identificatori non vengono modificati durante una sessione.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>query.xpath.pos.index</td>
   <td>Indica se il linguaggio di query XPath JCR 1.0 è supportato. true indica il supporto e false indica l'assenza di supporto.</td>
  </tr>
  <tr>
   <td>crx.repository.systemid</td>
   <td>L'identificatore di sistema trovato nel file system.id.</td>
  </tr>
  <tr>
   <td>option.query.sql.supported</td>
   <td>Indica se il linguaggio di query XPath JCR 1.0 è supportato. true indica il supporto e false indica l'assenza di supporto.</td>
  </tr>
  <tr>
   <td>jcr.repository.version</td>
   <td>Versione dell’implementazione del repository.</td>
  </tr>
  <tr>
   <td>option.update.Primary.node.type.supported</td>
   <td>Indica se il tipo di nodo primario di un nodo può essere modificato. true indica che è possibile modificare il tipo di nodo principale, false indica che la modifica non è supportata.</td>
  </tr>
  <tr>
   <td>option.node.type.management.supported</td>
   <td>Indica se la gestione del tipo di nodo è supportata. true indica che è supportato e false indica che non è supportato.</td>
  </tr>
  <tr>
   <td>node.type.management.overrides.supported</td>
   <td>Indica se è possibile ignorare la definizione di un nodo figlio o di proprietà ereditata di un tipo di nodo. true indica che sono supportate le sostituzioni e false indica che non sono supportate.</td>
  </tr>
  <tr>
   <td>option.Observ.supported</td>
   <td>true indica che è supportata l'osservazione asincrona delle modifiche apportate al repository. Il supporto dell'osservazione asincrona consente alle applicazioni di ricevere e rispondere alle notifiche su ogni modifica man mano che si verificano.</td>
  </tr>
  <tr>
   <td>query.jcrscore</td>
   <td><p>true indica che la pseudo-proprietà jcr:score è disponibile nelle query XPath e SQL che includono una funzione jcrfn:contains (in XPath) o CONTAINS (in SQL) per eseguire una ricerca full-text.</p> </td>
  </tr>
  <tr>
   <td>option.simple.versioning.supported</td>
   <td>true indica che il repository supporta il controllo delle versioni semplice. Con il semplice controllo delle versioni, il repository mantiene una serie sequenziale di versioni di un nodo.</td>
  </tr>
  <tr>
   <td>option.workspace.management.supported</td>
   <td>true indica che l'archivio supporta la creazione e l'eliminazione di aree di lavoro tramite API.</td>
  </tr>
  <tr>
   <td>option.update.mixin.node.types.supported</td>
   <td>true indica che l'archivio supporta l'aggiunta e la rimozione di tipi di nodi mixin di un nodo esistente.</td>
  </tr>
  <tr>
   <td>node.type.management.main.item.name.supported</td>
   <td>true indica che l'archivio consente alle definizioni dei nodi di contenere un elemento primario come figlio. Un elemento primario è accessibile tramite l'API senza conoscere il nome dell'elemento.</td>
  </tr>
  <tr>
   <td>level.2.supported</td>
   <td>true indica che LEVEL_1_SUPPORTED e OPTION_XML_IMPORT_SUPPORTED sono entrambi true.</td>
  </tr>
  <tr>
   <td>write.supported</td>
   <td>true indica che l'archivio consente l'accesso in scrittura tramite l'API. false indica l'accesso in sola lettura.</td>
  </tr>
  <tr>
   <td>node.type.management.update.in.use.supported</td>
   <td>true indica che è possibile modificare le definizioni dei nodi in uso nei nodi esistenti.</td>
  </tr>
  <tr>
   <td>jcr.Specification.version</td>
   <td>Versione della specifica JCR implementata dalla directory archivio.</td>
  </tr>
  <tr>
   <td>option.journaling.Observ.supported</td>
   <td>true indica che le applicazioni possono eseguire l'osservazione registrata del repository. con l'osservazione registrata, è possibile ottenere una serie di notifiche di modifica per un periodo di tempo specifico. </td>
  </tr>
  <tr>
   <td>query.language</td>
   <td>I linguaggi di query supportati dalla directory archivio. Nessun valore indica il supporto della query.</td>
  </tr>
  <tr>
   <td>option.xml.export.supported</td>
   <td>true indica che l'archivio supporta l'esportazione di nodi come codice XML.</td>
  </tr>
  <tr>
   <td>node.type.management.multiple.binary.properties.supported</td>
   <td>true indica che l'archivio supporta la registrazione di tipi di nodi con più proprietà binarie. false indica che per un tipo di nodo è supportata una singola proprietà binaria.</td>
  </tr>
  <tr>
   <td>option.access.control.supported</td>
   <td>true indica che l'archivio supporta il controllo di accesso, per l'impostazione e la determinazione dei privilegi utente per l'accesso ai nodi.</td>
  </tr>
  <tr>
   <td>option.baseline.supported</td>
   <td>true indica che il repository supporta sia le configurazioni che le linee di base.</td>
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
   <td>query.stored.query.supported</td>
   <td>true indica che il repository supporta le query memorizzate.</td>
  </tr>
  <tr>
   <td>query.full.text.search.supported</td>
   <td>true indica che l'archivio supporta la ricerca full-text.</td>
  </tr>
  <tr>
   <td>node.type.management.inheritance</td>
   <td><p>Indica il livello di supporto del repository per l'ereditarietà dei tipi di nodo. I seguenti valori sono possibili:</p> <p>node.type.management.inheritance.Minimum: La registrazione dei tipi di nodo primario è limitata a quelli che hanno solo nt:base come supertipo. La registrazione dei tipi di nodo del mixin è limitata a quelli senza supertipo.</p> <p>node.type.management.inheritance.single: La registrazione dei tipi di nodi primari è limitata a quelli con un solo tipo di superentità. La registrazione dei tipi di nodo del mixin è limitata a quelli con al massimo un supertipo.</p> <p><br /> node.type.management.inheritance.multiple: I tipi di nodo principale possono essere registrati con uno o più supertipi. I tipi di nodi misti possono essere registrati con zero o più supertipi.</p> </td>
  </tr>
  <tr>
   <td>crx.cluster.favoriteMaster</td>
   <td>true indica che questo nodo del cluster è il master preferito del cluster.</td>
  </tr>
  <tr>
   <td>option.transaction.supported</td>
   <td>true indica che il repository supporta le transazioni.</td>
  </tr>
  <tr>
   <td>jcr.repository.vendor.url</td>
   <td>URL del fornitore del repository.</td>
  </tr>
  <tr>
   <td>node.type.management.value.limits.supported</td>
   <td>true indica che l'archivio supporta i vincoli di valore per le proprietà dei nodi.</td>
  </tr>
  <tr>
   <td>node.type.management.property.types</td>
   <td>un array di costanti javax.jcr.PropertyType che rappresentano i tipi di proprietà che un tipo di nodo registrato può specificare. Un array di lunghezza zero indica che i tipi di nodi registrati non possono specificare le definizioni delle proprietà. I tipi di proprietà sono STRING, URI, BOOLEAN, LONG, DOPPIO, DECIMAL, BINARY, DATE, NAME, PATH, WEAKREFERENCE, REFERENCE e UNDEFINED (se supportato)</td>
  </tr>
  <tr>
   <td>node.type.management.orderable.child.nodes.supported</td>
   <td>true indica che l'archivio supporta la conservazione dell'ordine dei nodi figlio.</td>
  </tr>
  <tr>
   <td>jcr.repository.vendor</td>
   <td>Nome del fornitore del repository.</td>
  </tr>
  <tr>
   <td>query.joins</td>
   <td><p>Livello di supporto per i join nelle query. I seguenti valori sono possibili:</p>
    <ul>
     <li>query.joins.none: Nessun supporto per i join. Le query possono utilizzare un selettore.</li>
     <li>query.joins.inner: Supporto per join interni.</li>
     <li>query.joins.inner.external: Supporto per giunti interni ed esterni.</li>
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
   <td>true indica che l'archivio supporta il codice XML importato come contenuto.</td>
  </tr>
  <tr>
   <td>node.type.management.same.name.siblings.supported</td>
   <td>true indica che l'archivio supporta nodi di pari livello (nodi con lo stesso elemento padre) con gli stessi nomi.</td>
  </tr>
  <tr>
   <td>node.type.management.residue.definition.supported</td>
   <td>true indica che l'archivio supporta le proprietà del nome con definizioni residue. Se supportato, l'attributo name di una definizione di elemento può essere un asterisco ("*").</td>
  </tr>
  <tr>
   <td>node.type.management.autocreated.definition.supported</td>
   <td>true indica che l'archivio supporta la creazione automatica di elementi secondari (nodi o proprietà) di un nodo al momento della creazione del nodo.</td>
  </tr>
  <tr>
   <td>crx.cluster.master</td>
   <td>true indica che il nodo del repository è il nodo master del cluster.</td>
  </tr>
  <tr>
   <td>level.1.supported</td>
   <td>true indica che option.xml.export.support è true e che query.language ha una lunghezza diversa da zero.</td>
  </tr>
  <tr>
   <td>option.unfield.content.supported</td>
   <td>true indica che l'archivio supporta il contenuto non archiviato. I nodi non archiviati non fanno parte della gerarchia del repository.</td>
  </tr>
  <tr>
   <td>jcr.Specification.name</td>
   <td>Nome della specifica JCR implementata dalla directory archivio.</td>
  </tr>
  <tr>
   <td>option.versioning.supported</td>
   <td>true indica che il repository supporta il controllo completo delle versioni.</td>
  </tr>
  <tr>
   <td>jcr.repository.name</td>
   <td>Nome della directory archivio.</td>
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
   <td>option.activity.supported</td>
   <td>true indica che il repository supporta le attività. Le attività sono un insieme di modifiche che vengono eseguite in un’area di lavoro unita a un’altra area di lavoro.</td>
  </tr>
  <tr>
   <td>node.type.management.multivalued.properties.supported</td>
   <td>true indica che l'archivio supporta le proprietà dei nodi che possono avere zero o più valori.</td>
  </tr>
  <tr>
   <td>option.retention.supported</td>
   <td>true indica che l'archivio supporta l'utilizzo di applicazioni esterne per la gestione della conservazione per applicare criteri di conservazione ai contenuti e supporta il blocco e il rilascio.</td>
  </tr>
  <tr>
   <td>option.lifecycle.supported</td>
   <td>true indica che il repository supporta la gestione del ciclo di vita.</td>
  </tr>
 </tbody>
</table>

**WorkspaceNames** I nomi delle aree di lavoro nella directory archivio. Sola lettura.

**DataStoreGarbageCollectionDelay** Il tempo in millisecondi che la raccolta di oggetti inattivi dorme dopo la scansione ogni decimo nodo. Lettura/scrittura.

**BackupDelay** Il tempo in millisecondi impiegato dal processo di backup tra ogni fase del backup. Lettura/scrittura.

**BackupInProgress** Un valore true indica che è in esecuzione un processo di backup. Sola lettura.

**BackupProgress** Per il backup corrente, la percentuale di tutti i file di cui è stato eseguito il backup. Sola lettura.

**CurrentBackupTarget** Per il backup corrente, il file ZIP in cui vengono memorizzati i file di backup. Se il backup non è in corso, non viene visualizzato alcun valore. Sola lettura.

**BackupIsSuccful** Il valore true indica che non si sono verificati errori durante il backup corrente o che non è in corso alcun backup. false indica che si è verificato un errore durante il backup corrente. Sola lettura.

**BackupResult** Lo stato del backup corrente. I seguenti valori sono possibili:

* Backup in corso: È in esecuzione un backup.
* Backup annullato: Il backup è stato annullato.
* Backup completato con errore: Errore durante il backup. Il messaggio di errore fornisce informazioni sulla causa.
* Backup completato: Backup riuscito.
* Nessun backup eseguito finora: Nessun backup in corso.

Sola lettura.

**TarOptimizationRunningSince** Data di inizio del processo di ottimizzazione file TAR corrente. Sola lettura.

**TarOptimizationDelay** Il tempo in millisecondi impiegato dal processo di ottimizzazione TAR tra ogni fase del processo. Lettura/scrittura.

**ClusterProperties** Un insieme di coppie chiave-valore che rappresentano proprietà e valori del cluster. Ogni riga della tabella rappresenta una proprietà cluster. Sola lettura.

**ClusterNodes** I membri del cluster di repository.

**ClusterId** L&#39;identificatore del cluster di repository. Sola lettura.

**ClusterMasterId** L&#39;identificatore del nodo master del cluster di repository. Sola lettura.

**ClusterNodeId** L&#39;identificatore di questo nodo del cluster di repository. Sola lettura.

### Operazioni {#operations-1}

**createWorkspace** Consente di creare un’area di lavoro nell’archivio.

* Argomenti:

   * name: Valore String che rappresenta il nome della nuova area di lavoro.

* Valore restituito: none

**runDataStoreGarbageCollection** Esegue la raccolta dei rifiuti sui nodi del repository.

* Argomenti:

   * delete: Un valore booleano che indica se eliminare gli elementi del repository non utilizzati. Un valore true causa l&#39;eliminazione di nodi e proprietà inutilizzati. Se si imposta il valore false, tutti i nodi vengono sottoposti a scansione ma non vengono eliminati.

* Valore restituito: none

**stopDataStoreGarbageCollection** Arresta una raccolta di oggetti inattivi nell&#39;archivio dati in esecuzione.

* Argomenti: none
* Valore restituito: rappresentazione in formato stringa dello stato corrente

**startBackup** Esegue il backup dei dati del repository in un file ZIP.

* Argomenti:

   * `target`: (Facoltativo) Un `String` valore che rappresenta il nome del file ZIP o della directory in cui archiviare i dati del repository. Per utilizzare un file ZIP, includete l’estensione del nome del file ZIP. Per utilizzare una directory, non includete alcuna estensione di nome file.

      Per eseguire un backup incrementale, specificate la directory precedentemente utilizzata per il backup.

      Potete specificare un percorso assoluto o relativo. I percorsi relativi sono relativi all&#39;elemento padre della directory crx-quickstart.

      Se non si specifica alcun valore, `backup-currentdate.zip` viene utilizzato il valore predefinito di dove `currentdate` si trova nel formato `yyyyMMdd-HHmm`.

* Valore restituito: none

**cancelBackup** Interrompe il processo di backup corrente ed elimina l&#39;archivio temporaneo creato per l&#39;archiviazione dei dati.

* Argomenti: none
* Valore restituito: none

**blockRepositoryWrites** Blocca le modifiche ai dati del repository. Il blocco viene notificato a tutti i listener di backup del repository.

* Argomenti: none
* Valore restituito: none

**unblockRepositoryWrites** Rimuove il blocco dall&#39;archivio. Tutti i listener di backup del repository ricevono una notifica della rimozione del blocco.

* Argomenti: none
* Valore restituito: none

**startTarOptimization** Avvia il processo di ottimizzazione dei file TAR utilizzando il valore predefinito per tarOptimizationDelay.

* Argomenti: none
* Valore restituito: none

**stopTarOptimization** interrompe l&#39;ottimizzazione dei file TAR.

* Argomenti: none
* Valore restituito: none

**tarIndexMerge** Unisce i file di indice principali di tutti i set TAR. I file indice principali sono file con diverse versioni principali. Ad esempio, i file seguenti vengono uniti nel file index_3_1.tar: index_1_1.tar, index_2_0.tar, index_3_0.tar. I file che sono stati uniti vengono eliminati (nell’esempio precedente, index_1_1.tar, index_2_0.tar e index_3_0.tar vengono eliminati).

* Argomenti:

   * `background`: Un valore booleano che indica se eseguire l&#39;operazione in background in modo che la console Web sia utilizzabile durante l&#39;esecuzione. Il valore true esegue l&#39;operazione in background.

* Valore restituito: none

**diventaClusterMaster** Imposta il nodo del repository come nodo master del cluster. Se non è già master, questo comando arresta il listener dell&#39;istanza master corrente e avvia un listener master sul nodo corrente. Questo nodo viene quindi impostato come nodo master e si riavvia, causando la connessione di tutti i nodi slave a questa istanza.

* Argomenti: none
* Valore restituito: none

**joinCluster** Aggiunge l&#39;archivio a un cluster come nodo slave. È necessario fornire un nome utente e una password a scopo di autenticazione. La connessione utilizza l&#39;autenticazione di base. Le credenziali di protezione sono codificate in base 64 prima di essere inviate al server.

* Argomenti:

   * `master`: Un valore di stringa che rappresenta l&#39;indirizzo IP o il nome del computer che esegue il nodo del repository principale.
   * `username`: Nome da utilizzare per l&#39;autenticazione con il cluster.
   * `password`: La password da utilizzare per l&#39;autenticazione.

* Valore restituito: none

**traversalCheck** Traverse e, facoltativamente, risolve le incongruenze in una sottostruttura che inizia da un nodo specifico. Questo è descritto dettagliatamente nella documentazione sui Manager di persistenza.

**coerenzaControlla** controlli e, facoltativamente, risolve la coerenza nel datastore. Questo è descritto dettagliatamente nella documentazione del datastore.

## Statistiche archivio (TimeSeries) {#repository-statistics-timeseries}

Il valore del campo TimeSeries per ciascun tipo di statistica `org.apache.jackrabbit.api.stats.RepositoryStatistics` definito.

* Dominio: `com.adobe.granite`
* Tipo: `TimeSeries`
* Nome: Uno dei seguenti valori della classe `org.apache.jackrabbit.api.stats.RepositoryStatistics.Type` Enum:

   * BUNDLE_CACHE_ACCESS_COUNTER
   * BUNDLE_CACHE_MISS_AVERAGE
   * BUNDLE_CACHE_MISS_COUNTER
   * BUNDLE_CACHE_MISS_DURATION
   * BUNDLE_CACHE_SIZE_COUNTER
   * BUNDLE_COUNTER
   * BUNDLE_READ_COUNTER
   * BUNDLE_WRITE_AVERAGE
   * BUNDLE_WRITE_COUNTER
   * BUNDLE_WRITE_DURATION
   * BUNDLE_WS_SIZE_COUNTER
   * QUERY_AVERAGE
   * QUERY_COUNT
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

* ValorePerSecondo: Il valore misurato al secondo nell’ultimo minuto. Sola lettura.
* ValuePerMinute: Il valore misurato al minuto nell’ultima ora. Sola lettura.
* ValorePerOra: Il valore misurato per ora nell&#39;ultima settimana. Sola lettura.
* ValuePerWeek: Valore misurato per settimana negli ultimi tre anni. Sola lettura.

## Statistiche query repository {#repository-query-stats}

Informazioni statistiche sulle query del repository.

* Dominio: com.adobe.granite
* Tipo: QueryStat

### Attributi {#attributes-2}

**Query lente** Informazioni sulle query del repository che hanno richiesto il tempo di completamento più lungo. Sola lettura.

**SlowQueriesQueueSize** Il numero massimo di query da includere nell&#39;elenco SlowQueries. Lettura/scrittura.

**Query** popolari Informazioni sulle query del repository che si sono verificate di più. Sola lettura.

**PopularQueriesQueueSize** Il numero massimo di query nell&#39;elenco PopularQueries. Lettura/scrittura.

### Operazioni {#operations-2}

**clearSlowQueriesQueue** Rimuove tutte le query dall&#39;elenco SlowQueries.

* Argomenti: none
* Valore restituito: none

**clearPopularQueries** Rimuove tutte le query dall&#39;elenco PopularQueries.

* Argomenti: none
* Valore restituito: none

## Agenti di replica {#replication-agents}

Monitorare i servizi per ogni agente di replica. Quando create un agente di replica, il servizio viene visualizzato automaticamente nella console JMX.

* **** Dominio: com.adobe.granite.replica
* **** Tipo: agent
* **** Nome: nessun valore
* **** Proprietà: {id=&quot;*Name*&quot;}, dove *Name* è il valore della proprietà Nome agente.

### Attributi {#attributes-3}

**Id** Un valore String che rappresenta l&#39;identificatore della configurazione dell&#39;agente di replica. Più agenti possono utilizzare la stessa configurazione. Sola lettura.

**Valido** Un valore booleano che indica se l&#39;agente è configurato correttamente:

* `true`: Configurazione valida.
* `false` : La configurazione contiene errori.

Sola lettura.

**Enabled** Un valore booleano che indica se l&#39;agente è abilitato:

* `true`: Abilitato.
* `false`: Disattivato.

**QueueBlock** Un valore booleano che indica se la coda esiste ed è bloccata:

* `true`: Bloccato. È in sospeso un tentativo automatico.
* `false`: Non bloccato o non esistente.

Sola lettura.

**QueuePaused** Un valore booleano che indica se la coda di processo è in pausa:

* `true`: Sospeso (sospeso)
* `false`: Non in pausa o non esiste.

Lettura/scrittura.

**QueueNumEntries** Un valore int che rappresenta il numero di processi nella coda agente. Sola lettura.

**QueueStatusTime** Un valore Date che indica l&#39;ora sul server in cui sono stati ottenuti i valori di stato visualizzati. Il valore corrisponde all’ora in cui è stata caricata la pagina. Sola lettura.

**QueueNextRetryTime** Per le code bloccate, un valore Date che indica quando si verifica il successivo tentativo automatico. Se non viene visualizzato alcun tempo, la coda non viene bloccata. Sola lettura.

**QueueProcessingSince** Un valore Date che indica l&#39;inizio dell&#39;elaborazione per il processo corrente. Se non viene visualizzato il tempo, la coda viene bloccata o inattiva. Sola lettura.

**QueueLastProcessTime** Un valore Date che indica quando è stato completato il processo precedente. Sola lettura.

### Operazioni {#operations-3}

**queueForceRetry** Per le code bloccate, invia il comando try alla coda.

* Argomenti: none
* Valore restituito: none

**queueClear** Rimuove tutti i processi dalla coda.

* Argomenti: none
* Valore restituito: none

## Motore Sling {#sling-engine}

Fornisce statistiche sulle richieste HTTP in modo da poter monitorare le prestazioni del servizio SlingRequestProcessor.

* Dominio: org.apache.sling
* Tipo: Engine
* Proprietà: {service=RequestProcessor}

### Attributi {#attributes-4}

**RequestsCount** Il numero di richieste che si sono verificate dopo l&#39;ultima reimpostazione delle statistiche.

**MinRequestDurationMsec** Il tempo più breve (in millisecondi) necessario per elaborare una richiesta dall&#39;ultima reimpostazione delle statistiche.

**MaxRequestDuratioMsec** Il tempo più lungo (in millisecondi) necessario per elaborare una richiesta dall&#39;ultima reimpostazione delle statistiche.

**StandardDeviationDurationMsec** La deviazione standard della quantità di tempo necessaria per elaborare le richieste. La deviazione standard viene calcolata utilizzando tutte le richieste dall&#39;ultima reimpostazione delle statistiche.

**MediaRequestDurationMsec** Il tempo medio richiesto per elaborare una richiesta. La media viene calcolata utilizzando tutte le richieste dall&#39;ultima reimpostazione delle statistiche

### Operazioni {#operations-4}

**resetStatistics** Imposta tutte le statistiche su zero. Reimpostare le statistiche quando è necessario analizzare le prestazioni di elaborazione delle richieste in un intervallo di tempo specifico.

* Argomenti: none
* Valore restituito: none

**id** La rappresentazione in formato stringa dell&#39;ID pacchetto.

**install** Un valore booleano che indica se il pacchetto è installato:

* `true`: Installato.
* `false`: Non installato.

**installedBy** L’ID dell’ultimo utente che ha installato il pacchetto.

**installedDate** La data dell&#39;ultima installazione del pacchetto.

**size** Un valore lungo che contiene la dimensione del pacchetto in byte.


## Avvio rapido {#quickstart-launcher}

Informazioni sul processo di avvio e sull’avvio rapido.

* Dominio: com.adobe.granite.quickstart
* Tipo: Launcher

### Operazioni {#operations-5}

**log**

Visualizza un messaggio nella finestra Avvio rapido.

Argomenti:

* p1: Un `String` valore che rappresenta il messaggio da visualizzare. L&#39;illustrazione seguente mostra il risultato di una chiamata `log` con un valore p1 di `this is a log message`.

![launcheruilog](assets/launcheruilog.png)

* Valore restituito: none

**startupFinished**

Chiama il metodo startupFinished dell&#39;avvio del server. Il metodo tenta di aprire la pagina di benvenuto in un browser Web.

* Argomenti: none
* Valore restituito: none

**startupProgress**

Imposta il valore di completamento del processo di avvio del server. La barra di avanzamento nella finestra Avvio rapido rappresenta il valore di completamento.

* Argomenti:

   * p1: Un valore Mobile che rappresenta la quantità di completamento del processo di avvio, espressa in frazione. Il valore deve essere compreso tra zero e uno. Ad esempio, 0,3 indica che il 30% è completato.

* Valore restituito: Nessuno.

![launcherprogress](assets/launcherprogress.png)

## Servizi di terze parti {#third-party-services}

Diverse risorse server di terze parti installano MBeans che espongono attributi e operazioni alla console JMX. Nella tabella seguente sono elencate le risorse di terze parti e sono disponibili collegamenti verso ulteriori informazioni.

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
     <li>Sistema operativo</li>
     <li>Runtime</li>
     <li>Threading</li>
    </ul> </td>
   <td><a href="https://docs.oracle.com/javase/8/docs/api/javax/management/package-summary.html">pacchetto javax.management</a></td>
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
   <td><a href="https://osgi.org/specification/osgi.enterprise/7.0.0/service.jmx.html#d0e42567">org.osgi.jmx.framework</a> , pacchetto</td>
  </tr>
 </tbody>
</table>

## Utilizzo della console JMX {#using-the-jmx-console}

La console JMX visualizza informazioni su diversi servizi in esecuzione sul server:

* Attributi: Proprietà del servizio quali configurazioni o dati di runtime. Gli attributi possono essere di sola lettura o di lettura/scrittura.
* Operazioni: Comandi che è possibile richiamare sul servizio.

MBeans distribuiti con un servizio OSGi espone gli attributi e le operazioni del servizio alla console. MBean determina gli attributi e le operazioni esposti e se gli attributi sono di sola lettura o di lettura/scrittura.

La pagina principale della console JMX include un sommario di servizi. Ogni riga della tabella rappresenta un servizio esposto da un MBean.

1. Aprite la console Web e fate clic sulla scheda JMX. ([http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx))
2. Fate clic sul valore di una cella per un servizio per visualizzare gli attributi e le operazioni del servizio.
3. Per modificare il valore di un attributo, fate clic su di esso, specificate il valore nella finestra di dialogo visualizzata e fate clic su Salva.
4. Per richiamare un&#39;operazione di servizio, fate clic sul nome dell&#39;operazione, specificate i valori degli argomenti nella finestra di dialogo visualizzata e fate clic su Richiama.

## Utilizzo di applicazioni JMX esterne per il monitoraggio {#using-external-jmx-applications-for-monitoring}

CRX consente alle applicazioni esterne di interagire con i Fagioli gestiti (MBeans) tramite le estensioni [Java Management (JMX)](https://docs.oracle.com/javase/6/docs/technotes/guides/management/overview.html). Utilizzando console generiche come [JConsole](https://java.sun.com/developer/technicalArticles/J2SE/jconsole.html) o applicazioni di monitoraggio specifiche per il dominio, è possibile ottenere e impostare configurazioni e proprietà CRX, nonché monitorare le prestazioni e l&#39;utilizzo delle risorse.

### Utilizzo di JConsole per il collegamento a CRX {#using-jconsole-to-connect-to-crx}

Per collegarsi a CRX utilizzando JConsole, procedere come segue:

1. Aprite una finestra terminale.
1. Digitate il comando seguente:

   `jconsole`

Viene avviata la console JConsole e viene visualizzata la finestra JConsole.

### Collegamento a un processo CRX locale {#connecting-to-a-local-crx-process}

JConsole visualizzerà un elenco dei processi Java Virtual Machine locali. L&#39;elenco conterrà due processi di avvio rapido. Selezionare il processo &quot;FIGLIO&quot; dall&#39;elenco dei processi locali (in genere quello con il PID più alto).

![screen_shot_2012-03-26at114557am](assets/screen_shot_2012-03-26at114557am.png)

### Collegamento a un processo CRX remoto {#connecting-to-a-remote-crx-process}

Per collegarsi a un processo CRX remoto, la JVM che ospita il processo CRX remoto dovrà essere abilitata per accettare connessioni JMX remote.

Per abilitare le connessioni JMX remote, è necessario impostare la seguente proprietà di sistema all&#39;avvio della JVM:

`com.sun.management.jmxremote.port=portNum`

Nella proprietà sopra, `portNum` è il numero di porta attraverso il quale si desidera abilitare le connessioni JMX RMI. Accertatevi di specificare un numero di porta non utilizzato. Oltre a pubblicare un connettore RMI per l&#39;accesso locale, l&#39;impostazione di questa proprietà consente di pubblicare un connettore RMI aggiuntivo in un registro di sola lettura privato nella porta specificata utilizzando un nome noto, &quot;jmxrmi&quot;.

Per impostazione predefinita, quando si abilita l&#39;agente JMX per il monitoraggio remoto, utilizza l&#39;autenticazione tramite password basata su un file password che deve essere specificato utilizzando la seguente proprietà di sistema quando si avvia la VM Java:

`com.sun.management.jmxremote.password.file=pwFilePath`

Per istruzioni dettagliate sulla configurazione di un file password, consultate la documentazione [JMX](https://docs.oracle.com/javase/6/docs/technotes/guides/management/agent.html) pertinente.

Esempio:

```shell
$ java
  -Dcom.sun.management.jmxremote.password.file=pwFilePath
  -Dcom.sun.management.jmxremote.port=8463
  -jar ./cq-quickstart.jar
```

### Utilizzo dei MBeans forniti da CRX {#using-the-mbeans-provided-by-crx}

Dopo il collegamento al processo di avvio rapido, JConsole fornisce una serie di strumenti di monitoraggio generali per la JVM in cui è in esecuzione CRX.

![screen_shot_2012-03-26at115056am](assets/screen_shot_2012-03-26at115056am.png)

Per accedere alle opzioni di monitoraggio e configurazione interne di CRX, passare alla scheda MBeans e, dalla struttura dei contenuti gerarchica a sinistra, selezionare la sezione Attributi o Operazioni a cui si è interessati. Ad esempio, la sezione com.adobe.granite/Repository/Operations.

In tale sezione, selezionare l&#39;attributo o l&#39;operazione desiderati nel riquadro a sinistra.

![screen_shot_2012-03-26at115728am](assets/screen_shot_2012-03-26at115728am.png)

