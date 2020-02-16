---
title: Lazy Content Migration
seo-title: Lazy Content Migration
description: Scopri ulteriori informazioni sulla migrazione dei contenuti Lazy in AEM 6.4.
seo-description: Scopri ulteriori informazioni sulla migrazione dei contenuti Lazy in AEM 6.4.
uuid: f5b0aa84-5638-4708-9da2-89964d394632
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: d72b8844-d782-4b5b-8999-338217dbefb9
docset: aem65
translation-type: tm+mt
source-git-commit: 7d93df515bf98f0a947428b8093e059d63b21a34

---


# Lazy Content Migration {#lazy-content-migration}

Per motivi di compatibilità con le versioni precedenti, il contenuto e la configurazione in **/etc** e **/content** a partire da AEM 6.3 non saranno toccati o trasformati immediatamente con l’aggiornamento. Ciò è fatto per garantire che le dipendenze delle applicazioni dei clienti su tali strutture rimangano intatte. La funzionalità relativa a queste strutture di contenuto è ancora la stessa anche se il contenuto in un&#39;applicazione AEM 6.5 out-of-box sarebbe ospitato in un&#39;altra posizione.

Anche se non tutte queste posizioni possono essere trasformate automaticamente, ci sono alcuni ritardi `CodeUpgradeTasks` anche denominati Lazy Content Migration. Questo consente ai clienti di attivare tali trasformazioni automatiche riavviando l&#39;istanza con la seguente proprietà di sistema:

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

Questo causerà l&#39;esecuzione `CodeUpgradeTasks` dell&#39;evento durante la migrazione.

L&#39;obiettivo è un&#39;esecuzione efficiente, ma questo processo di aggiornamento è sincrono e comporta un tempo di inattività in base alla quantità di contenuto da elaborare. Si consiglia di valutare i tempi di esecuzione in un ambiente di fase prima di un sistema di produzione per pianificare una finestra di manutenzione in base.

Poiché in genere questo richiede anche la regolazione dell&#39;applicazione, questa attività deve essere eseguita insieme alla distribuzione dell&#39;applicazione corrispondente.

Di seguito è riportato l&#39;elenco completo delle `CodeUpgradeTasks` modifiche introdotte al punto 6.5:

| **Nome** | **Pertinente** **per le versioni di AEM precedenti a** | **Migrazione** **tipo** | **Dettagli** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5.6.1 | Immediato |  |
| `Cq60MSMContentUpgrade` | &lt; 6.0 | Immediato | Rileva tutti `LiveRelationShips` quelli `VersionStorage` che sono stati eliminati e aggiunge la proprietà di esclusione all&#39;elemento padre |
| `Cq61CloudServicesContentUpgrade` | &lt; 6.1 | Immediato | Ristrutturazione dei servizi cloud per impostazione predefinita sicura |
| `Cq62ConfContentUpgrade` | &lt; 6.2 | Immediato | Rimuove il collegamento basato su proprietà da **/content** a **/conf** (sostituito dal meccanismo OSGi), genera la configurazione OSGi corrispondente |
| `Cq62FormsContentUpgrade` | &lt; 6.2 | Immediato | A causa di merge_preserve la gestione sicura per impostazione predefinita delle sostituzioni delle regole di negazione in base alle autorizzazioni che determinano la necessità di riordinare l&#39;aggiornamento |
| `CQ62Html5SmartFileUpgrade` | &lt; 6.2 | Immediato | Rileva i componenti che utilizzano il widget Html5SmartFile, cerca gli usi del componente nel contenuto e ristruttura la persistenza, spostando efficacemente il binario verso il basso e non lo archivia a livello di componente. |
| `Cq62ProjectsCodeUpgrade` | &lt; 6.2 | Immediato | Sposta i vecchi progetti di stile da **/etc/projects** a **/content/projects** |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6.2 | Immediato | Introduce un livello contenitore in una gerarchia (Aree) e regola i riferimenti. |
| `Cq62TargetContentUpgrade` | &lt; 6.2 | Immediato | Imposta i nomi delle posizioni fisse sui componenti di destinazione. |
| `Cq62WorkflowContentUpgrade` | &lt; 6.2 | Immediato | Complessa trasformazione di modelli di workflow che precedono le strutture, le istanze, le notifiche della versione 6.2 e quindi l&#39;unione dal percorso di backup da **/var/backup** |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6.3 | Immediato | Sposta risorse, schemi di metadati personalizzati e profili di elaborazione da **/app** a **/conf** e traduce lo schema di metadati e i profili di metadati nei moduli dal corallo2 al coral3. |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6.3 | Immediato | Sposta risorse e facet di ricerca personalizzati da **/app** a **/conf** e traduce lo schema di metadati e i profili di metadati nei moduli dal corallo2 al corallo3. |
| `CQ63InboxItemsUpgrade` | &lt; 6.3 | Immediato | Aggiorna InboxItems per ordinare gli elementi della inbox (regolazione dei metadati per un ordinamento efficiente) |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6.3 | Immediato | Regola la proprietà metadataSchema nella cartella sostituendo i percorsi relativi a **/conf** al posto di **/apps** |
| `CQ63MobileAppsNavUpgrade` | &lt; 6.3 | Immediato | Regolazione della struttura di navigazione |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6.3 | Immediato | Sposta le configurazioni personalizzate per i dashboard di monitoraggio da **/libs** e **/apps** |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6.3 | Immediato | Converte la proprietà processingProfile (utilizzata fino alla versione 6.1) in Assets in modo che corrisponda alla struttura 6.3 e successiva. Regola inoltre i percorsi relativi del profilo in **/conf** al posto di **/apps**. |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6.3 | Immediato | Attività di aggiornamento che rimuove le voci di menu CRXDE Lite e Console Web obsolete in caso di aggiornamento. |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6.3 | Ritardato | Spostare le configurazioni cloud SRP, le configurazioni di orologi community, pulire **/etc/social** e **/etc/enablement** (eventuali riferimenti e dati devono essere regolati quando viene eseguita la migrazione pigra - nessuna parte dell&#39;applicazione dovrebbe più dipendere da questa struttura). |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6.4 | Ritardato | Elimina le impostazioni **del cloud** /ecc. (contenente la configurazione ContextHub). La configurazione viene migrata automaticamente al primo accesso. Se la migrazione dei contenuti Lazy viene avviata insieme all&#39;aggiornamento di questo contenuto in **/etc/cloud settings** deve essere mantenuto tramite pacchetto prima dell&#39;aggiornamento e reinstallato per l&#39;avvio della trasformazione implicita, insieme a una successiva disinstallazione del pacchetto dopo il completamento. |
| `CQ64UsersTitleFixTask` | &lt; 6.4 | Ritardato | Regola la struttura del titolo legacy in base al titolo nel nodo del profilo utente. |
| `CQ64CommerceMigrationTask` | &lt; 6.4 | Ritardato | Migrare il contenuto del commercio da **/etc/commerce** a **/var/commerce**. Durante la migrazione il contenuto viene spostato e i riferimenti al contenuto spostato vengono aggiornati per riflettere la nuova posizione. |
| `CQ65DMMigrationTask` | &lt; 6.5 | Ritardato | Migrazione delle impostazioni del catalogo legacy e delle impostazioni dei servizi cloud per contenuti multimediali dinamici da **/etc** a **/conf** |
| `CQ65LegacyClientlibsCleanupTask` | &lt; 6.5 | Ritardato | Pulizia di clientlibs legacy esistenti in **/etc/clientlibs** |
