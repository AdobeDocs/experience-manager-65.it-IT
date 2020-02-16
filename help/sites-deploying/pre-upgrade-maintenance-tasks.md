---
title: Attività di manutenzione pre-aggiornamento
seo-title: Attività di manutenzione pre-aggiornamento
description: Scopri le attività di pre-aggiornamento in AEM.
seo-description: Scopri le attività di pre-aggiornamento in AEM.
uuid: 5da1cfc7-8a10-47b1-aafb-2cd112e3f818
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: 291c91e5-65ff-473d-ac11-3da480239e76
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Attività di manutenzione pre-aggiornamento{#pre-upgrade-maintenance-tasks}

Prima di iniziare l&#39;aggiornamento, è importante seguire queste attività di manutenzione per assicurarsi che il sistema sia pronto e possa essere ripristinato in caso di problemi:

* [Spazio su disco sufficiente](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#ensure-sufficient-disk-space)
* [Backup completo di AEM](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#fully-back-up-aem)
* [Backup delle modifiche a /etc](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#backup-changes-etc)
* [Genera il file quickstart.properties](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#generate-quickstart-properties)
* [Configurare lo scorrimento del flusso di lavoro e del registro di controllo](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#configure-wf-audit-purging)
* [Installare, configurare ed eseguire le attività di pre-aggiornamento](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#install-configure-run-pre-upgrade-tasks)
* [Disattiva moduli di login personalizzati](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-login-modules)
* [Rimuovere Gli Aggiornamenti Dalla Directory /install](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#remove-updates-install-directory)
* [Interrompi eventuali istanze in standby a freddo](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#stop-tarmk-coldstandby-instance)
* [Disattiva processi pianificati personalizzati](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-scheduled-jobs)
* [Esegui pulizia revisione offline](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-offline-revision-cleanup)
* [Esegui raccolta dati Garbage](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-datastore-garbage-collection)
* [Se necessario, aggiorna lo schema del database](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#upgradethedatabaseschemaifneeded)
* [Eliminare gli utenti che potrebbero ostacolare l&#39;aggiornamento](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#delete-users-that-might-hinder-the-upgrade)

* [Ruota file di registro](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#rotate-log-files)

## Spazio su disco sufficiente {#ensure-sufficient-disk-space}

Quando si esegue l&#39;aggiornamento, oltre alle attività di aggiornamento del contenuto e del codice, sarà necessario eseguire una migrazione dell&#39;archivio. La migrazione creerà una copia del repository nel nuovo formato Segment Tar. Di conseguenza, sarà necessario spazio su disco sufficiente per mantenere una seconda versione, potenzialmente più grande, del repository.

## Backup completo di AEM {#fully-back-up-aem}

Prima di avviare l&#39;aggiornamento, deve essere eseguito il backup completo di AEM. Accertatevi di eseguire il backup dell&#39;archivio, dell&#39;installazione dell&#39;applicazione, del datastore e delle istanze Mongo, se applicabili. Per ulteriori informazioni sul backup e il ripristino di un’istanza di AEM, consultate [Backup e ripristino](/help/sites-administering/backup-and-restore.md).

## Backup delle modifiche a /etc {#backup-changes-etc}

Il processo di aggiornamento consente di mantenere e unire i contenuti e le configurazioni esistenti sotto i percorsi `/apps` e `/libs` nella directory archivio. Per le modifiche apportate al `/etc` percorso, comprese le configurazioni Context Hub, spesso è necessario riapplicare queste modifiche dopo l&#39;aggiornamento. Anche se l&#39;aggiornamento effettuerà una copia di backup di tutte le modifiche che non possono essere unite in `/var`, è consigliabile eseguire il backup manuale di tali modifiche prima di avviare l&#39;aggiornamento.

## Genera il file quickstart.properties {#generate-quickstart-properties}

Quando si avvia AEM dal file JAR, viene generato un `quickstart.properties` file in `crx-quickstart/conf`. Se AEM è stato avviato solo con lo script start in passato, questo file non sarà presente e l&#39;aggiornamento non riuscirà. Accertatevi di verificare l’esistenza di questo file e riavviate AEM dal file JAR se non è presente.

## Configurare lo scorrimento del flusso di lavoro e del registro di controllo {#configure-wf-audit-purging}

Le `WorkflowPurgeTask` operazioni e `com.day.cq.audit.impl.AuditLogMaintenanceTask` le configurazioni OSGi sono specifiche e non funzionano senza di esse. Se durante l&#39;esecuzione di un&#39;attività precedente all&#39;aggiornamento non riesce, è probabile che la causa principale sia la mancanza di configurazioni. Di conseguenza, se non desiderate eseguirle, accertatevi di aggiungere configurazioni OSGi per queste attività o di rimuoverle completamente dall&#39;elenco delle attività di ottimizzazione pre-aggiornamento. La documentazione relativa alla configurazione delle attività di eliminazione del flusso di lavoro è disponibile in [Amministrazione delle istanze](/help/sites-administering/workflows-administering.md) del flusso di lavoro e nella configurazione delle attività di manutenzione del registro di controllo, disponibile in Gestione [registro di controllo in AEM 6](/help/sites-administering/operations-audit-log.md).

Per l’eliminazione del flusso di lavoro e del registro di controllo in CQ 5.6 e per l’eliminazione del registro di controllo in AEM 6.0, consultate [Eliminare il flusso di lavoro e i nodi](https://helpx.adobe.com/experience-manager/kb/howtopurgewf.html)di controllo.

## Installare, configurare ed eseguire le attività di pre-aggiornamento {#install-configure-run-pre-upgrade-tasks}

A causa del livello di personalizzazione consentito da AEM, gli ambienti generalmente non soddisfano un metodo uniforme per eseguire gli aggiornamenti. Ciò rende difficile la creazione di una procedura standardizzata per gli aggiornamenti.

Nelle versioni precedenti, era anche difficile per gli aggiornamenti di AEM interrotti o che non erano stati ripristinati in modo sicuro. Ciò causava situazioni in cui era necessario riavviare la procedura di aggiornamento completo o in cui venivano eseguiti aggiornamenti difettosi senza attivare alcun avviso.

Per risolvere questi problemi, Adobe ha aggiunto diversi miglioramenti al processo di aggiornamento, rendendolo più flessibile e semplice da usare. Le attività di manutenzione pre-aggiornamento che prima dovevano essere eseguite manualmente vengono ottimizzate e automatizzate. Inoltre, sono stati aggiunti rapporti post-aggiornamento in modo che il processo possa essere esaminato completamente nella speranza che tutti i problemi siano trovati più facilmente.

Le attività di manutenzione pre-aggiornamento sono attualmente distribuite su varie interfacce, che vengono eseguite manualmente o parzialmente. L’ottimizzazione per la manutenzione pre-aggiornamento introdotta in AEM 6.3 consente di attivare in modo unificato queste attività e di controllarne i risultati su richiesta.

Tutte le attività incluse nel passaggio di ottimizzazione pre-aggiornamento sono compatibili con tutte le versioni a partire da AEM 6.0.

### Come impostare {#how-to-set-it-up}

In AEM 6.3 e versioni successive, le attività di ottimizzazione per la manutenzione pre-aggiornamento sono incluse nel Jar di avvio rapido. Se state effettuando l’aggiornamento da una versione precedente di AEM 6, questi vengono resi disponibili tramite pacchetti separati che potete scaricare da Gestione pacchetti.

Potete trovare i pacchetti nelle seguenti posizioni:

* [Per l&#39;aggiornamento da AEM 6.0](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq600/product/pre-upgrade-tasks-content-cq60)

* [Per l&#39;aggiornamento da AEM 6.1](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq610/product/pre-upgrade-tasks-content-cq61)

* [Per l&#39;aggiornamento da AEM 6.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq620/product/pre-upgrade-tasks-content-cq62)

### How to Use It {#how-to-use-it}

Il componente `PreUpgradeTasksMBean` OSGI è preconfigurato con un elenco di attività di manutenzione pre-aggiornamento che possono essere eseguite tutte contemporaneamente. È possibile configurare le attività seguendo la procedura seguente:

1. Passate alla console Web accedendo a *https://serveraddress:serverport/system/console/configMgr*

1. Cercate &quot;**preupgradetask**&quot;, quindi fate clic sul primo componente corrispondente. Il nome completo del componente è `com.adobe.aem.upgrade.prechecks.mbean.impl.PreUpgradeTasksMBeanImpl`

1. Modificate l&#39;elenco delle attività di manutenzione da eseguire come illustrato di seguito:

   ![1487758925984](assets/1487758925984.png)

L&#39;elenco delle attività varia a seconda della modalità di esecuzione utilizzata per avviare l&#39;istanza. Di seguito è riportata una descrizione della modalità di esecuzione per cui ogni attività di manutenzione è progettata.

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
   <td>Viene eseguito mark and sweep. Per gli archivi dati condivisi, rimuovete questo passaggio ed eseguite<br /> manualmente o in modo corretto le istanze prima dell'esecuzione.</td>
  </tr>
  <tr>
   <td><code>ConsistencyCheckTask</code></td>
   <td>crx2</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>WorkflowPurgeTask</code></td>
   <td>crx2/crx3</td>
   <td>È necessario configurare l’OSGi per la configurazione della rimozione dei flussi di lavoro di Adobe Granite prima di eseguire.</td>
  </tr>
  <tr>
   <td><code>GenerateBundlesListFileTask</code></td>
   <td>crx2/crx3</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>RevisionCleanupTask</code></td>
   <td>crx3</td>
   <td>Per le istanze TarMK su AEM da 6.0 a 6.2, eseguite manualmente la pulizia delle revisioni offline.</td>
  </tr>
  <tr>
   <td><code>com.day.cq.audit.impl.AuditLogMaintenanceTask</code></td>
   <td>crx3</td>
   <td>È necessario configurare la configurazione OSGi dell'utilità di pianificazione della rimozione del registro di controllo prima di eseguire.</td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>`DataStoreGarbageCollectionTask` sta chiamando un&#39;operazione di Garbage Collection di datastore con la fase mark e sweep, se utilizzata. Per le distribuzioni che utilizzano un datastore condiviso, assicurarsi di riconfigurarlo o di preparare l&#39;istanza in modo da evitare l&#39;eliminazione degli elementi a cui fa riferimento un&#39;altra istanza. Questa operazione potrebbe richiedere l&#39;esecuzione manuale della fase di contrassegno su tutte le istanze prima di attivare l&#39;attività di pre-aggiornamento.

### Configurazione predefinita dei controlli di stato pre-aggiornamento {#default-configuration-of-the-pre-upgrade-health-checks}

Il componente `PreUpgradeTasksMBeanImpl` OSGI è preconfigurato con un elenco di tag di controllo dello stato pre-aggiornamento da eseguire quando viene chiamato il `runAllPreUpgradeHealthChecks` metodo:

* **system** - il tag utilizzato dai controlli di integrità della manutenzione granitica

* **pre-aggiornamento** : si tratta di un tag personalizzato che può essere aggiunto a tutti i controlli di integrità che è possibile impostare per l&#39;esecuzione prima di un aggiornamento

L&#39;elenco è modificabile. È possibile utilizzare i pulsanti più **(+)** e meno **(-)** oltre ai tag per aggiungere altri tag personalizzati o rimuovere quelli predefiniti.

**Metodi MBean**

È possibile accedere alla funzionalità dei fagioli gestiti tramite la console [](/help/sites-administering/jmx-console.md)JMX.

Per accedere agli MBeans:

1. Passate alla console JMX all&#39;indirizzo *https://serveraddress:serverport/system/console/jmx*
1. Cercare **PreUpgradeTasks** e fare clic sul risultato

1. Selezionare un metodo dalla sezione **Operazioni** e selezionare **Richiama** nella finestra seguente.

Di seguito è riportato un elenco di tutti i metodi disponibili `PreUpgradeTasksMBeanImpl` esposti:

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
   <td>Esegue tutte le attività di manutenzione pre-aggiornamento elencate.</td>
  </tr>
  <tr>
   <td><code>runPreUpgradeTask(preUpgradeTaskName)</code></td>
   <td>AZIONE</td>
   <td>Esegue l'attività di manutenzione pre-aggiornamento con il nome specificato come parametro.</td>
  </tr>
  <tr>
   <td><code>isRunAllPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>Controlla se l' <code>runAllPreUpgradeTasksmaintenance</code> attività è in esecuzione.</td>
  </tr>
  <tr>
   <td><code>getAnyPreUpgradeTaskRunning()</code></td>
   <td>ACTION_INFO</td>
   <td>Controlla se sono in esecuzione attività di manutenzione pre-aggiornamento e restituisce<br /> un array contenente i nomi delle attività in esecuzione.</td>
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
   <td><p>Esegue tutti i controlli di integrità pre-aggiornamento e ne salva lo stato in un file denominato <code>preUpgradeHCStatus.properties</code> che si trova nel percorso principale di sling. Se il <code>shutDownOnSuccess</code> parametro è impostato su <code>true</code>, l’istanza di AEM verrà chiusa, ma solo se tutti i controlli di integrità pre-aggiornamento hanno uno stato OK.</p> <p>Il file delle proprietà verrà utilizzato come prerequisito per qualsiasi aggiornamento<br /> futuro e il processo di aggiornamento verrà interrotto se l'esecuzione del controllo<br /> dello stato di pre-aggiornamento non riesce. Se si desidera ignorare il risultato dei controlli di stato pre-aggiornamento<br /> e avviare comunque l'aggiornamento, è possibile eliminare il file.</p> </td>
  </tr>
  <tr>
   <td><code>detectUsageOfUnavailableAPI(aemVersion)</code></td>
   <td>AZIONE</td>
   <td>Elenca tutti i pacchetti importati che non saranno più soddisfatti quando<br /> si esegue l'aggiornamento alla versione specificata di AEM. La versione AEM di destinazione deve essere<br /> specificata come parametro.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>I metodi MBean possono essere invocati tramite:
>
>* Console JMX
>* Qualsiasi applicazione esterna che si connette a JMX
>* cURL
>



## Disattiva moduli di login personalizzati {#disable-custom-login-modules}

>[!NOTE]
>
>Questo passaggio è richiesto solo se state effettuando l&#39;aggiornamento da una versione di AEM 5. Può essere ignorato completamente per gli aggiornamenti da versioni precedenti di AEM 6.

Il modo in cui `LoginModules` vengono configurate le impostazioni personalizzate per l&#39;autenticazione a livello di repository è sostanzialmente cambiato in Apache Oak.

Nelle versioni di AEM che utilizzavano la configurazione CRX2, il file veniva inserito nel `repository.xml` file, mentre da AEM 6 in poi viene eseguito nel servizio Apache Felix JAAS Configuration Factory tramite la console Web.

Pertanto, tutte le configurazioni esistenti dovranno essere disattivate e ricreate per Apache Oak dopo l&#39;aggiornamento.

Per disabilitare i moduli personalizzati definiti nella configurazione JAAS di `repository.xml`, è necessario modificare la configurazione per utilizzare i moduli predefiniti `LoginModule`, come in questo esempio:

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
>Per ulteriori informazioni, consultate [Autenticazione con il modulo](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html)di login esterno.
>
>Per un esempio di configurazione in AEM 6, consultate `LoginModule` Configurazione di LDAP con AEM 6 [](/help/sites-administering/ldap-config.md).

## Rimuovere Gli Aggiornamenti Dalla Directory /install {#remove-updates-install-directory}

>[!NOTE]
>
>Rimuovere i pacchetti dalla directory crx-quickstart/install solo dopo che l&#39;istanza AEM è stata chiusa. Questo sarà uno degli ultimi passi prima di avviare la procedura di aggiornamento locale.

Rimuovere tutti i Service Pack, i feature pack o gli hotfix distribuiti tramite la `crx-quickstart/install` directory del file system locale. Questo impedirà l&#39;installazione involontaria di hotfix e Service Pack precedenti sulla nuova versione di AEM dopo il completamento dell&#39;aggiornamento.

## Interrompi eventuali istanze in standby a freddo {#stop-tarmk-coldstandby-instance}

Se si utilizza TarMK in standby a freddo, arrestare eventuali istanze in standby a freddo. Questi garantiranno un modo efficiente per tornare online in caso di problemi nell&#39;aggiornamento. Una volta completato l&#39;aggiornamento, le istanze in standby freddo dovranno essere ricreate dalle istanze primarie aggiornate.

## Disattiva processi pianificati personalizzati {#disable-custom-scheduled-jobs}

Disattiva tutti i processi pianificati OSGi inclusi nel codice dell’applicazione.

## Esegui pulizia revisione offline {#execute-offline-revision-cleanup}

>[!NOTE]
>
>Questo passaggio è necessario solo per le installazioni TarMK

Se si utilizza TarMK, è necessario eseguire la pulizia revisioni offline prima di eseguire l&#39;aggiornamento. In questo modo la fase di migrazione dell&#39;archivio e le successive attività di aggiornamento verranno eseguite molto più rapidamente e sarà possibile garantire la corretta esecuzione della funzione di pulizia delle revisioni online al termine dell&#39;aggiornamento. Per informazioni sull&#39;esecuzione della pulizia revisioni offline, vedere [Esecuzione della pulizia](/help/sites-deploying/storage-elements-in-aem-6.md#performing-offline-revision-cleanup)revisioni offline.

## Esegui raccolta dati Garbage {#execute-datastore-garbage-collection}

>[!NOTE]
>
>Questo passaggio è necessario solo per le istanze che eseguono crx3

Dopo aver eseguito la pulizia revisioni sulle istanze CRX3, è necessario eseguire la raccolta dei dati per rimuovere eventuali blob senza riferimenti nell&#39;archivio dati. Per istruzioni, consultate la documentazione sulla raccolta [di oggetti inattivi nell&#39;archivio](/help/sites-administering/data-store-garbage-collection.md)dati.

## Se necessario, aggiorna lo schema del database {#upgrade-the-database-schema-if-needed}

Solitamente, lo stack Apache Oak sottostante utilizzato da AEM per la persistenza si occuperà di aggiornare lo schema del database, se necessario.

Tuttavia, potrebbero verificarsi casi in cui lo schema non può essere aggiornato automaticamente. Si tratta per lo più di ambienti ad alta protezione in cui il database viene eseguito sotto un utente con privilegi molto limitati. In questo caso, AEM continuerà a utilizzare lo schema precedente.

Per evitare che ciò si verifichi, è necessario aggiornare lo schema seguendo la procedura seguente:

1. Arrestate l’istanza di AEM da aggiornare.
1. Aggiornare lo schema del database. Consulta la documentazione relativa al tipo di database in uso per vedere quali sono gli strumenti necessari per ottenere questo risultato.

   Per ulteriori informazioni su come Oak gestisce gli aggiornamenti dello schema, consultate [questa pagina sul sito Web](https://jackrabbit.apache.org/oak/docs/nodestore/document/rdb-document-store.html#upgrade)Apache.

1. Procedete con l’aggiornamento di AEM.

## Eliminare gli utenti che potrebbero ostacolare l&#39;aggiornamento {#delete-users-that-might-hinder-the-upgrade}

>[!NOTE]
>
>Questa attività di manutenzione pre-aggiornamento è necessaria solo se:
>
>* Stai effettuando l&#39;aggiornamento dalle versioni di AEM precedenti a AEM 6.3
>* Durante l&#39;aggiornamento si verificano i seguenti errori.
>



In alcuni casi eccezionali, gli utenti del servizio potrebbero finire in una versione precedente di AEM con tag non corretti come utenti normali.

In questo caso, l&#39;aggiornamento non riuscirà con un messaggio come questo:

```
ERROR [Apache Sling Repository Startup Thread] com.adobe.granite.repository.impl.SlingRepositoryManager Exception in a SlingRepositoryInitializer, SlingRepository service registration aborted
java.lang.RuntimeException: Unable to create service user [communities-utility-reader]:java.lang.RuntimeException: Existing user communities-utility-reader is not a service user.
```

Per risolvere questo problema, accertatevi di effettuare le seguenti operazioni:

1. Scollegare l&#39;istanza dal traffico di produzione
1. Create un backup degli utenti che causano il problema. Puoi farlo tramite Gestione pacchetti. Per ulteriori informazioni, vedere [Come utilizzare i pacchetti.](/help/sites-administering/package-manager.md)
1. Eliminare gli utenti che causano il problema. Di seguito è riportato un elenco di utenti che potrebbero rientrare in questa categoria:

   1. `dynamic-media-replication`
   1. `communities-ugc-writer`
   1. `communities-utility-reader`
   1. `communities-user-admin`
   1. `oauthservice`
   1. `sling-scripting`

## Ruota file di registro {#rotate-log-files}

È consigliabile archiviare i file di registro correnti prima di avviare l&#39;aggiornamento. In questo modo sarà più semplice monitorare e analizzare i file di registro durante e dopo l&#39;aggiornamento per identificare e risolvere eventuali problemi che possono verificarsi.
