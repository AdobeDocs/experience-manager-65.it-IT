---
title: Migrazione dei contenuti Lazy
seo-title: Migrazione dei contenuti Lazy
description: Scopri la Migrazione dei contenuti Lazy in AEM 6.4.
seo-description: Scopri la Migrazione dei contenuti Lazy in AEM 6.4.
uuid: f5b0aa84-5638-4708-9da2-89964d394632
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: d72b8844-d782-4b5b-8999-338217dbefb9
docset: aem65
feature: Upgrading
translation-type: tm+mt
source-git-commit: ebe7042b931869c3b4b7204e3ce7afa52d56f0ef
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 6%

---


# Migrazione dei contenuti pigri {#lazy-content-migration}

Per motivi di compatibilità con le versioni precedenti, i contenuti e la configurazione in **/etc** e **/content** a partire da AEM 6.3 non verranno toccati o trasformati immediatamente con l’aggiornamento. Ciò viene fatto per garantire che le dipendenze delle applicazioni dei clienti su tali strutture rimangano intatte. La funzionalità relativa a queste strutture di contenuto è ancora la stessa anche se il contenuto in una versione standard AEM 6.5 sarebbe ospitato in un’altra posizione.

Anche se non tutte queste posizioni possono essere trasformate automaticamente, ci sono alcuni ritardi `CodeUpgradeTasks` denominati anche Migrazione dei contenuti pigri. Questo consente ai clienti di attivare tali trasformazioni automatiche riavviando l&#39;istanza con questa proprietà del sistema:

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

Questo causerà l’esecuzione del `CodeUpgradeTasks` durante la migrazione.

Sebbene l&#39;obiettivo sia un&#39;esecuzione efficiente, questo processo di aggiornamento è sincrono e comporta pertanto un downtime a seconda della quantità di contenuto da elaborare. Si consiglia di valutare i tempi di esecuzione in un ambiente di stage prima di un sistema di produzione per pianificare un intervallo di manutenzione in base.

Poiché in genere è necessario regolare l’applicazione, questa attività deve essere eseguita insieme alla distribuzione dell’applicazione corrispondente.

Di seguito è riportato l&#39;elenco completo di `CodeUpgradeTasks` introdotto nella versione 6.5:

| **Nome** | **** **Pertinente per le versioni AEM precedenti a** | **** **MigrationType** | **Dettagli** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5=&quot;&quot;> | Immediato |  |
| `Cq60MSMContentUpgrade` | &lt; 6.0 | Immediato | Rileva tutti i valori `LiveRelationShips` da `VersionStorage` che sono stati eliminati e aggiunge la proprietà di esclusione all&#39;elemento padre |
| `Cq61CloudServicesContentUpgrade` | &lt; 6=&quot;&quot;> | Immediato | Ristruttura i servizi cloud per la configurazione sicura per impostazione predefinita |
| `Cq62ConfContentUpgrade` | &lt; 6.2 | Immediato | Rimuove il collegamento basato su proprietà da **/content** a **/conf** (sostituito dal meccanismo OSGi), genera la configurazione OSGi corrispondente |
| `Cq62FormsContentUpgrade` | &lt; 6=&quot;&quot;> | Immediato | A causa della gestione merge_preserve della regola di negazione sicura per impostazione predefinita, le sostituzioni a causa di autorizzazioni specifiche che comportano la necessità di riordinare l&#39;aggiornamento |
| `CQ62Html5SmartFileUpgrade` | &lt; 6=&quot;&quot;> | Immediato | Rileva i componenti che utilizzano il widget Html5SmartFile, cerca gli utilizzi del componente nel contenuto e ristruttura la persistenza, spostando efficacemente il binario verso il basso e non archiviarlo a livello di componente. |
| `Cq62ProjectsCodeUpgrade` | &lt; 6=&quot;&quot;> | Immediato | Sposta i progetti in stile precedente da **/etc/projects** a **/content/projects** |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6=&quot;&quot;> | Immediato | Introduce un livello contenitore alla gerarchia (Aree) e regola i riferimenti. |
| `Cq62TargetContentUpgrade` | &lt; 6=&quot;&quot;> | Immediato | Imposta i nomi della posizione fissa sui componenti di destinazione. |
| `Cq62WorkflowContentUpgrade` | &lt; 6=&quot;&quot;> | Immediato | Trasformazione complessa dei modelli di flusso di lavoro che precede le strutture, le istanze, le notifiche 6.2, quindi unione dal percorso di backup da **/var/backup** |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6.3 | Immediato | Sposta le risorse, gli schemi di metadati personalizzati e i profili di elaborazione da **/apps** a **/conf** e traduce lo schema di metadati e i profili di metadati nei moduli da coral2 a coral3. |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6=&quot;&quot;> | Immediato | Sposta le risorse e i facet di ricerca personalizzati da **/apps** a **/conf** e traduce lo schema di metadati e i profili di metadati nei moduli da coral2 a coral3. |
| `CQ63InboxItemsUpgrade` | &lt; 6=&quot;&quot;> | Immediato | Aggiorna InboxItems per ordinare gli elementi della casella in entrata (regolazione dei metadati per un ordinamento efficiente) |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6=&quot;&quot;> | Immediato | Regola la proprietà metadataSchema nella cartella sostituendo i percorsi relativi a **/conf** al posto di **/apps** |
| `CQ63MobileAppsNavUpgrade` | &lt; 6=&quot;&quot;> | Immediato | Regolazione della struttura di navigazione |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6=&quot;&quot;> | Immediato | Sposta le configurazioni personalizzate per le dashboard di monitoraggio da **/libs** e **/apps** |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6=&quot;&quot;> | Immediato | Traduce la proprietà processingProfile (utilizzata fino alla versione 6.1) in Assets in modo che corrisponda alla struttura 6.3 e versioni successive. Regola anche i percorsi relativi del profilo in **/conf** al posto di **/apps**. |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6=&quot;&quot;> | Immediato | Attività di aggiornamento che rimuove le voci di menu obsolete di CRXDE Lite e della console Web in caso di aggiornamento. |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6=&quot;&quot;> | Ritardato | Lo spostamento delle configurazioni cloud SRP, delle configurazioni delle parole d&#39;ordine community, la pulizia di **/etc/social** e **/etc/enablement** (tutti i riferimenti e i dati devono essere regolati quando viene eseguita la migrazione lenta - nessuna parte dell&#39;applicazione deve più dipendere da questa struttura). |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6.4 | Ritardato | Pulisce **/etc/cloudsettings** (contenente la configurazione ContextHub). La configurazione viene migrata automaticamente al primo accesso. Nel caso in cui sia avviata la migrazione dei contenuti Lazy insieme all&#39;aggiornamento di questo contenuto in **/etc/cloudsettings** deve essere mantenuto tramite pacchetto prima dell&#39;aggiornamento e reinstallato per la trasformazione implicita da avviare, insieme a una successiva disinstallazione del pacchetto dopo il completamento. |
| `CQ64UsersTitleFixTask` | &lt; 6=&quot;&quot;> | Ritardato | Regola la struttura del titolo legacy in base al titolo nel nodo del profilo utente. |
| `CQ64CommerceMigrationTask` | &lt; 6=&quot;&quot;> | Ritardato | Esegui la migrazione del contenuto di e-commerce da **/etc/commerce** a **/var/commerce**. Durante la migrazione il contenuto viene spostato e i riferimenti al contenuto spostato vengono aggiornati per riflettere la nuova posizione. |
| `CQ65DMMigrationTask` | &lt; 6.5 | Ritardato | Migrare le impostazioni del catalogo legacy e le impostazioni dei Cloud Services Dynamic Media da **/etc** a **/conf** |
| `CQ65LegacyClientlibsCleanupTask` | &lt; 6=&quot;&quot;> | Ritardato | Pulizia delle librerie client legacy esistenti in **/etc/clientlibs** |
