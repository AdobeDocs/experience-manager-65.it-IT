---
title: Attività di manutenzione pre-aggiornamento
description: Scopri le attività di pre-aggiornamento consigliate per l’AEM.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
docset: aem65
feature: Upgrading
exl-id: 37d4aee4-15eb-41ab-ad71-dfbd5c7910f8
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '2014'
ht-degree: 0%

---

# Attività di manutenzione pre-aggiornamento{#pre-upgrade-maintenance-tasks}

Prima di iniziare l’aggiornamento, è importante seguire queste attività di manutenzione per garantire che il sistema sia pronto e possa essere ripristinato nel caso in cui si verifichino dei problemi:

* [Garantire spazio su disco sufficiente](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#ensure-sufficient-disk-space)
* [Backup completo dell&#39;AEM](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#fully-back-up-aem)
* [Backup delle modifiche in /etc](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#backup-changes-etc)
* [Genera il file quickstart.properties](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#generate-quickstart-properties)
* [Configurare il flusso di lavoro e la rimozione del registro di controllo](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#configure-wf-audit-purging)
* [Installare, configurare ed eseguire le attività di pre-aggiornamento](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#install-configure-run-pre-upgrade-tasks)
* [Disabilita moduli di accesso personalizzati](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-login-modules)
* [Rimuovi aggiornamenti dalla directory /install](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#remove-updates-install-directory)
* [Arresta tutte le istanze di standby a freddo](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#stop-tarmk-coldstandby-instance)
* [Disabilita processi pianificati personalizzati](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-scheduled-jobs)
* [Esegui pulizia revisioni offline](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-offline-revision-cleanup)
* [Esegui raccolta oggetti inattivi archivio dati](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-datastore-garbage-collection)
* [Aggiorna lo schema del database se necessario](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#upgradethedatabaseschemaifneeded)
* [Elimina utenti che potrebbero impedire l&#39;aggiornamento](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#delete-users-that-might-hinder-the-upgrade)

* [Ruota file di registro](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#rotate-log-files)

## Garantire spazio su disco sufficiente {#ensure-sufficient-disk-space}

Durante l’esecuzione dell’aggiornamento, oltre alle attività di aggiornamento del contenuto e del codice, è necessario eseguire una migrazione dell’archivio. La migrazione crea una copia dell’archivio nel nuovo formato Tar segmento. Di conseguenza, è necessario spazio su disco sufficiente per conservare una seconda versione, potenzialmente più grande, dell’archivio.

## Backup completo dell&#39;AEM {#fully-back-up-aem}

Prima di iniziare l’aggiornamento è necessario eseguire il backup completo dell’AEM. Assicurati di eseguire il backup dell’archivio, dell’installazione dell’applicazione, dell’archivio dati e delle istanze Mongo, se applicabile. Per ulteriori informazioni sul backup e il ripristino di un&#39;istanza AEM, vedere [Backup e ripristino](/help/sites-administering/backup-and-restore.md).

## Backup delle modifiche in /etc {#backup-changes-etc}

Il processo di aggiornamento consente di mantenere e unire i contenuti e le configurazioni esistenti da sotto `/apps` e `/libs` percorsi nell’archivio. Per le modifiche apportate al `/etc` , incluse le configurazioni di Context Hub, spesso è necessario riapplicare queste modifiche dopo l’aggiornamento. Durante l’aggiornamento viene creata una copia di backup di tutte le modifiche in cui non è possibile unire `/var`, Adobe consiglia di eseguire manualmente il backup di queste modifiche prima di iniziare l’aggiornamento.

## Genera il file quickstart.properties {#generate-quickstart-properties}

Quando si avvia AEM dal file jar, un `quickstart.properties` file generato in `crx-quickstart/conf`. Se AEM è stato avviato solo in passato con lo script di avvio, il file non è presente e l’aggiornamento non riesce. Verifica l’esistenza di questo file e, se non è presente, riavvia AEM dal file jar.

## Configurare il flusso di lavoro e la rimozione del registro di controllo {#configure-wf-audit-purging}

Il `WorkflowPurgeTask` e `com.day.cq.audit.impl.AuditLogMaintenanceTask` Le attività richiedono configurazioni OSGi separate e non possono funzionare senza di esse. In caso di errore durante l’esecuzione delle attività di pre-aggiornamento, la causa più probabile è la mancanza di configurazioni. Di conseguenza, se non desideri eseguirle, accertati di aggiungere configurazioni OSGi per queste attività o rimuoverle completamente dall’elenco delle attività di ottimizzazione pre-aggiornamento. La documentazione relativa alla configurazione delle attività di eliminazione del flusso di lavoro è disponibile all’indirizzo [Amministrazione delle istanze dei flussi di lavoro](/help/sites-administering/workflows-administering.md) e la configurazione dell’attività di manutenzione del registro di controllo sono disponibili all’indirizzo [Manutenzione del registro di controllo dell’AEM 6](/help/sites-administering/operations-audit-log.md).

Per la rimozione del flusso di lavoro e del registro di controllo in CQ 5.6 e la rimozione del registro di controllo in AEM 6.0, consulta [Eliminare i nodi del flusso di lavoro e del controllo](https://helpx.adobe.com/experience-manager/kb/howtopurgewf.html).

## Installare, configurare ed eseguire le attività di pre-aggiornamento {#install-configure-run-pre-upgrade-tasks}

A causa del livello di personalizzazione consentito da AEM, gli ambienti di solito non si attengono a un modo uniforme di eseguire gli aggiornamenti. In quanto tale, la creazione di una procedura standardizzata per gli aggiornamenti è un processo difficile.

Nelle versioni precedenti, era difficile anche per gli aggiornamenti AEM interrotti o che non erano riusciti a riprendere in modo sicuro. Questo problema causava situazioni in cui era necessario riavviare la procedura di aggiornamento completa o in cui venivano eseguiti aggiornamenti difettosi senza attivare alcun avviso.

Per risolvere questi problemi, Adobe ha aggiunto diversi miglioramenti al processo di aggiornamento, rendendolo più resiliente e di facile utilizzo. Le attività di manutenzione pre-aggiornamento che prima dovevano essere eseguite manualmente vengono ottimizzate e automatizzate. Inoltre, sono stati aggiunti report di post-aggiornamento in modo da poter esaminare completamente il processo nella speranza che eventuali problemi vengano rilevati più facilmente.

Le attività di manutenzione pre-aggiornamento sono attualmente distribuite su varie interfacce che vengono parzialmente o completamente eseguite manualmente. L’ottimizzazione della manutenzione pre-aggiornamento introdotta in AEM 6.3 consente di attivare in modo unificato queste attività e di verificarne i risultati su richiesta.

Tutte le attività incluse nel passaggio di ottimizzazione pre-aggiornamento sono compatibili con tutte le versioni a partire da AEM 6.0.

### Come impostarla {#how-to-set-it-up}

In AEM 6.3 e versioni successive, le attività di ottimizzazione della manutenzione pre-aggiornamento sono incluse nel file jar quickstart.

<!-- URLs below are all 404s. This content should probably be removed because it is entirely obsolete.

If you are upgrading from an older version of AEM 6, they are made available through separate packages that you can download from the Package Manager.

You can find the packages at these locations:

* [For upgrading from AEM 6.0](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq600/product/pre-upgrade-tasks-content-cq60)

* [For upgrading from AEM 6.1](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq610/product/pre-upgrade-tasks-content-cq61)

* [For upgrading from AEM 6.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq620/product/pre-upgrade-tasks-content-cq62) -->

### Come usarlo {#how-to-use-it}

Il `PreUpgradeTasksMBean` Il componente OSGI viene fornito preconfigurato con un elenco di attività di manutenzione pre-aggiornamento che possono essere eseguite tutte contemporaneamente. Puoi configurare le attività seguendo la procedura seguente:

1. Passa alla console Web navigando in *https://serveraddress:serverport/system/console/configMgr*

1. Cerca &quot;**pre-aggiornamento attività**&quot;, quindi fai clic sul primo componente corrispondente. Il nome completo del componente è `com.adobe.aem.upgrade.prechecks.mbean.impl.PreUpgradeTasksMBeanImpl`

1. Modificare l&#39;elenco delle attività di manutenzione che devono essere eseguite come illustrato di seguito:

   ![1487758925984](assets/1487758925984.png)

L’elenco delle attività varia a seconda della modalità di esecuzione utilizzata per avviare l’istanza. Di seguito è riportata una descrizione della modalità di esecuzione per cui ogni attività di manutenzione è progettata.

<table>
 <tbody>
  <tr>
   <td><strong>Attività</strong></td>
   <td><strong>Modalità esecuzione</strong></td>
   <td><strong>Note</strong></td>
  </tr>
  <tr>
   <td><code>TarIndexMergeTask</code></td>
   <td>crx2</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>DataStoreGarbageCollectionTask</code></td>
   <td>crx2</td>
   <td>Esegue il contrassegno e lo sweep. Per gli archivi dati condivisi, rimuovi questo passaggio ed esegui<br /> prepara le istanze manualmente o correttamente prima dell’esecuzione.</td>
  </tr>
  <tr>
   <td><code>ConsistencyCheckTask</code></td>
   <td>crx2</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>WorkflowPurgeTask</code></td>
   <td>crx2/crx3</td>
   <td>Prima di eseguire, è necessario configurare l’OSGi Adobe Granite Workflow Purge Configuration.</td>
  </tr>
  <tr>
   <td><code>GenerateBundlesListFileTask</code></td>
   <td>crx2/crx3</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>RevisionCleanupTask</code></td>
   <td>crx3</td>
   <td>Per le istanze TarMK su AEM da 6.0 a 6.2, esegui manualmente Offline Revision Cleanup (Pulizia revisioni offline).</td>
  </tr>
  <tr>
   <td><code>com.day.cq.audit.impl.AuditLogMaintenanceTask</code></td>
   <td>crx3</td>
   <td>Prima di eseguire, è necessario configurare la configurazione OSGi dell’utilità di pianificazione per la rimozione del registro di controllo.</td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>Il `DataStoreGarbageCollectionTask` chiama un’operazione di raccolta oggetti inattivi del datastore con la fase di contrassegno e sweep, se utilizzate. Per le distribuzioni che utilizzano un archivio dati condiviso, assicurati di riconfigurarlo correttamente o di preparare l’istanza per evitare l’eliminazione degli elementi a cui fa riferimento un’altra istanza. Questo processo potrebbe richiedere l’esecuzione manuale della fase di contrassegno su tutte le istanze prima di attivare questa attività di pre-aggiornamento.

### Configurazione predefinita dei controlli di integrità pre-aggiornamento {#default-configuration-of-the-pre-upgrade-health-checks}

Il `PreUpgradeTasksMBeanImpl` Il componente OSGI è preconfigurato con un elenco di tag di verifica dello stato pre-aggiornamento da eseguire quando `runAllPreUpgradeHealthChecks` viene chiamato il metodo:

* **sistema** - il tag utilizzato dai controlli di integrità della manutenzione granite

* **pre-aggiornamento** - un tag personalizzato che può essere aggiunto a tutti i controlli di integrità che puoi impostare per l’esecuzione prima di un aggiornamento

L’elenco è modificabile. È possibile utilizzare il segno più **(+)** e meno **(-)** oltre ai tag per aggiungere altri tag personalizzati o rimuovere quelli predefiniti.

**Metodi MBean**

È possibile accedere alla funzionalità dei bean gestiti utilizzando [Console JMX](/help/sites-administering/jmx-console.md).

Per accedere a MBean:

1. Andare alla console JMX all’indirizzo *https://serveraddress:serverport/system/console/jmx*
1. Cerca **PreUpgradeTasks** e fai clic sul risultato

1. Seleziona un metodo dalla **Operazioni** sezione e seleziona **Richiama** nella finestra seguente.

Di seguito sono elencati tutti i metodi disponibili che `PreUpgradeTasksMBeanImpl` espone:

<table>
 <tbody>
  <tr>
   <td><strong>Nome metodo</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td><code>getAvailablePreUpgradeTasksNames()</code></td>
   <td>INFO</td>
   <td>Visualizza l'elenco dei nomi delle attività di manutenzione pre-aggiornamento disponibili.</td>
  </tr>
  <tr>
   <td><code>getAvailablePreUpgradeHealthChecksTagNames()</code></td>
   <td>INFO</td>
   <td>Visualizza l'elenco dei nomi dei tag dei controlli di integrità pre-aggiornamento.</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeTasks()</code></td>
   <td>AZIONE</td>
   <td>Esegue tutte le attività di manutenzione pre-aggiornamento nell’elenco.</td>
  </tr>
  <tr>
   <td><code>runPreUpgradeTask(preUpgradeTaskName)</code></td>
   <td>AZIONE</td>
   <td>Esegue l'attività di manutenzione pre-aggiornamento con il nome specificato come parametro.</td>
  </tr>
  <tr>
   <td><code>isRunAllPreUpgradeTaskRunning()</code></td>
   <td>INFORMAZIONI_AZIONE</td>
   <td>Controlla se <code>runAllPreUpgradeTasksmaintenance</code> l'attività è in esecuzione.</td>
  </tr>
  <tr>
   <td><code>getAnyPreUpgradeTaskRunning()</code></td>
   <td>INFORMAZIONI_AZIONE</td>
   <td>Controlla se è in esecuzione un’attività di manutenzione pre-aggiornamento e<br /> restituisce un array contenente i nomi delle attività attualmente in esecuzione.</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunTime(preUpgradeTaskName)</code></td>
   <td>AZIONE</td>
   <td>Visualizza il tempo di esecuzione esatto dell'attività di manutenzione pre-aggiornamento con il nome specificato come parametro.</td>
  </tr>
  <tr>
   <td><code>getPreUpgradeTaskLastRunState(preUpgradeTaskName)</code></td>
   <td>AZIONE</td>
   <td>Visualizza l'ultimo stato di esecuzione dell'attività di manutenzione pre-aggiornamento con il nome specificato come parametro.</td>
  </tr>
  <tr>
   <td><code>runAllPreUpgradeHealthChecks(shutDownOnSuccess)</code></td>
   <td>AZIONE</td>
   <td><p>Esegue tutti i controlli di integrità pre-aggiornamento e ne salva lo stato in un file denominato <code>preUpgradeHCStatus.properties</code> si trova nel percorso principale di sling. Se il <code>shutDownOnSuccess</code> il parametro è impostato su <code>true</code>, l’istanza AEM viene chiusa, ma solo se tutti i controlli di integrità precedenti all’aggiornamento hanno uno stato OK.</p> <p>Il file delle proprietà viene utilizzato come precondizione per qualsiasi aggiornamento futuro<br /> e il processo di aggiornamento viene interrotto se il controllo di integrità pre-aggiornamento<br /> esecuzione non riuscita. Se si desidera ignorare il risultato del pre-aggiornamento<br /> verifica stato e avvia l'aggiornamento in ogni caso, puoi eliminare il file.</p> </td>
  </tr>
  <tr>
   <td><code>detectUsageOfUnavailableAPI(aemVersion)</code></td>
   <td>AZIONE</td>
   <td>Elenca tutti i pacchetti importati non più soddisfatti quando<br /> aggiornamento alla versione AEM specificata. La versione AEM di destinazione deve essere<br /> dato come parametro.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>I metodi MBean possono essere richiamati tramite:
>
>* Console JMX
>* Qualsiasi applicazione esterna che si connette a JMX
>* cURL
>

## Disabilita moduli di accesso personalizzati {#disable-custom-login-modules}

>[!NOTE]
>
>Questo passaggio è necessario solo se si esegue l&#39;aggiornamento da una versione di AEM 5. Può essere ignorato completamente per gli aggiornamenti dalle versioni precedenti di AEM 6.

Il modo personalizzato `LoginModules` sono configurati per l’autenticazione a livello di archivio, ma sono fondamentalmente cambiati in Apache Oak.

Nelle versioni AEM che utilizzavano la configurazione CRX2, veniva inserito nel `repository.xml` mentre a partire da AEM 6 in poi viene eseguito nel servizio Apache Felix JAAS Configuration Factory tramite la console web.

Pertanto, eventuali configurazioni esistenti dovranno essere disattivate e ricreate per Apache Oak dopo l’aggiornamento.

Per disattivare i moduli personalizzati definiti nella configurazione JAAS di `repository.xml`, è necessario modificare la configurazione per utilizzare il valore predefinito `LoginModule`, come nell’esempio seguente:

```xml
<Security >
             ....
          <!--
                 Use LoginModule authenticating against repository itself
                 -->
                 <LoginModule class = "com.day.crx.core.CRXLoginModule" >
                     <param name = "anonymousId" value = "anonymous" />
                     <param name = "adminId" value ="admin" />
                     <param name = "disableNTLMAuth" value = "true" />
                     <param name = "tokenExpiration" value = "43200000" />
                     <!-- param name="trust_credentials_attribute" value="d5b9167e95dad6e7d3b5d6fa8df48af8"/
                -->
                 </LoginModule >
         </ Security>
```

>[!NOTE]
>
>Per ulteriori informazioni, consulta [Autenticazione con il modulo di accesso esterno](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html).
>
>Per un esempio di `LoginModule` configurazione in AEM 6, vedi [Configurazione di LDAP con AEM 6](/help/sites-administering/ldap-config.md).

## Rimuovi aggiornamenti dalla directory /install {#remove-updates-install-directory}

>[!NOTE]
>
>Rimuovere solo i pacchetti dalla directory crx-quickstart/install DOPO aver chiuso l&#39;istanza AEM. Questo passaggio è uno degli ultimi prima di avviare la procedura di aggiornamento sul posto.

Rimuovi i Service Pack, i Feature Pack o gli hotfix distribuiti tramite `crx-quickstart/install` sul file system locale. In questo modo si evita l’installazione involontaria di vecchi hotfix e service pack in aggiunta alla nuova versione dell’AEM al termine dell’aggiornamento.

## Arresta tutte le istanze di standby a freddo {#stop-tarmk-coldstandby-instance}

Se si utilizza lo standby a freddo TarMK, interrompere le istanze di standby a freddo. In questo modo è possibile tornare online in caso di problemi durante l&#39;aggiornamento. Al termine dell’aggiornamento, è necessario ricompilare le istanze in standby a freddo dalle istanze primarie aggiornate.

## Disabilita processi pianificati personalizzati {#disable-custom-scheduled-jobs}

Disattiva tutti i processi pianificati OSGi inclusi nel codice dell’applicazione.

## Esegui pulizia revisioni offline {#execute-offline-revision-cleanup}

>[!NOTE]
>
>Questo passaggio è necessario solo per le installazioni TarMK

Se utilizzi TarMK, esegui Offline Revision Cleanup prima dell’aggiornamento. In questo modo il passaggio di migrazione dell’archivio e le successive attività di aggiornamento vengono eseguiti molto più rapidamente e si garantisce che la pulizia delle revisioni online possa essere eseguita correttamente al termine dell’aggiornamento. Per informazioni sull&#39;esecuzione di Offline Revision Cleanup, vedere [Esecuzione della pulizia delle revisioni offline](/help/sites-deploying/storage-elements-in-aem-6.md#performing-offline-revision-cleanup).

## Esegui raccolta oggetti inattivi archivio dati {#execute-datastore-garbage-collection}

>[!NOTE]
>
>Questo passaggio è necessario solo per le istanze che eseguono crx3

Dopo aver eseguito la pulizia delle revisioni sulle istanze CRX3, è necessario eseguire la raccolta oggetti inattivi del datastore per rimuovere eventuali BLOB senza riferimenti nell’archivio dati. Per istruzioni, consulta la documentazione su [Raccolta oggetti inattivi dell’archivio dati](/help/sites-administering/data-store-garbage-collection.md).

## Aggiorna lo schema del database se necessario {#upgrade-the-database-schema-if-needed}

Di solito, lo stack Apache Oak sottostante utilizzato dall’AEM per la persistenza si occupa dell’aggiornamento dello schema del database, se necessario.

Tuttavia, potrebbero verificarsi dei casi in cui non è possibile aggiornare automaticamente lo schema. Si tratta per lo più di ambienti ad alta sicurezza in cui il database viene eseguito da un utente con privilegi limitati. Se si verifica una situazione di questo tipo, l’AEM continua a utilizzare il vecchio schema.

Per evitare che si verifichi uno scenario di questo tipo, aggiorna lo schema effettuando le seguenti operazioni:

1. Arrestare l&#39;istanza AEM che deve essere aggiornata.
1. Aggiornare lo schema del database. Consultare la documentazione relativa al tipo di database in uso per verificare gli strumenti necessari per ottenere il risultato.

   Per ulteriori informazioni su come Oak gestisce gli aggiornamenti dello schema, consulta [questa pagina del sito web Apache](https://jackrabbit.apache.org/oak/docs/nodestore/document/rdb-document-store.html#upgrade).

1. Procedere con l&#39;aggiornamento dell&#39;AEM.

## Elimina utenti che potrebbero impedire l&#39;aggiornamento {#delete-users-that-might-hinder-the-upgrade}

>[!NOTE]
>
>Questa attività di manutenzione pre-aggiornamento è necessaria solo se:
>
>* Stai effettuando l’aggiornamento da versioni AEM precedenti alla 6.3 di AEM
>* Durante l’aggiornamento si verifica uno degli errori indicati di seguito.
>

Ci sono casi eccezionali in cui gli utenti del servizio potrebbero finire con una versione precedente dell’AEM impropriamente taggata come utenti normali.

In questo caso, l’aggiornamento non riesce e viene visualizzato un messaggio simile al seguente:

```
ERROR [Apache Sling Repository Startup Thread] com.adobe.granite.repository.impl.SlingRepositoryManager Exception in a SlingRepositoryInitializer, SlingRepository service registration aborted
java.lang.RuntimeException: Unable to create service user [communities-utility-reader]:java.lang.RuntimeException: Existing user communities-utility-reader is not a service user.
```

Per risolvere il problema, eseguire le operazioni seguenti:

1. Scollega l’istanza dal traffico di produzione
1. Crea un backup di uno o più utenti che causano il problema. Puoi eseguire questa operazione tramite Gestione pacchetti. Per ulteriori informazioni, consulta [Come utilizzare i pacchetti.](/help/sites-administering/package-manager.md)
1. Eliminare uno o più utenti che causano il problema. Di seguito è riportato un elenco di utenti che potrebbero rientrare in questa categoria:

   1. `dynamic-media-replication`
   1. `communities-ugc-writer`
   1. `communities-utility-reader`
   1. `communities-user-admin`
   1. `oauthservice`
   1. `sling-scripting`

## Ruota file di registro {#rotate-log-files}

L&#39;Adobe consiglia di archiviare i file di registro correnti prima di iniziare l&#39;aggiornamento. In questo modo è più facile monitorare e analizzare i file di registro durante e dopo l’aggiornamento per identificare e risolvere eventuali problemi.
