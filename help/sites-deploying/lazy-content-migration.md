---
title: Migrazione dei contenuti Lazy
seo-title: Lazy Content Migration
description: Scopri la Migrazione dei contenuti Lazy in AEM 6.4.
seo-description: Learn about Lazy Content Migration in AEM 6.4.
uuid: f5b0aa84-5638-4708-9da2-89964d394632
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: d72b8844-d782-4b5b-8999-338217dbefb9
docset: aem65
feature: Upgrading
exl-id: 946c7c2a-806b-4461-a38b-9c2e5ef1e958
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 6%

---

# Migrazione dei contenuti Lazy {#lazy-content-migration}

Per motivi di compatibilità con le versioni precedenti, contenuti e configurazione in **/etc** e **/content** a partire da AEM 6.3 non sarà toccato o trasformato immediatamente con l&#39;aggiornamento. Ciò viene fatto per garantire che le dipendenze delle applicazioni dei clienti su tali strutture rimangano intatte. La funzionalità relativa a queste strutture di contenuto è ancora la stessa anche se il contenuto in una versione standard AEM 6.5 sarebbe ospitato in un’altra posizione.

Anche se non tutte queste posizioni possono essere trasformate automaticamente, ci sono alcuni ritardi `CodeUpgradeTasks` è anche noto come Migrazione dei contenuti Lazy. Questo consente ai clienti di attivare tali trasformazioni automatiche riavviando l&#39;istanza con questa proprietà del sistema:

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

Questo causerà il `CodeUpgradeTasks` da eseguire durante la migrazione.

Sebbene l&#39;obiettivo sia un&#39;esecuzione efficiente, questo processo di aggiornamento è sincrono e comporta pertanto un downtime a seconda della quantità di contenuto da elaborare. Si consiglia di valutare i tempi di esecuzione in un ambiente di stage prima di un sistema di produzione per pianificare un intervallo di manutenzione in base.

Poiché in genere è necessario regolare l’applicazione, questa attività deve essere eseguita insieme alla distribuzione dell’applicazione corrispondente.

Di seguito è riportato l&#39;elenco completo di `CodeUpgradeTasks` al punto 6.5:

| **Nome** | **Pertinente** **per AEM versioni precedenti a** | **Migrazione** **Tipo** | **Dettagli** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5.6.1 | Immediato |  |
| `Cq60MSMContentUpgrade` | &lt; 6.0 | Immediato | Rileva tutti `LiveRelationShips` da `VersionStorage` che sono stati eliminati e aggiungono proprietà di esclusione all&#39;elemento padre |
| `Cq61CloudServicesContentUpgrade` | &lt; 6.1 | Immediato | Ristruttura i servizi cloud per la configurazione sicura per impostazione predefinita |
| `Cq62ConfContentUpgrade` | &lt; 6.2 | Immediato | Rimuove il collegamento basato su proprietà da **/content** a **/conf** (sostituito dal meccanismo OSGi), genera la configurazione OSGi corrispondente |
| `Cq62FormsContentUpgrade` | &lt; 6.2 | Immediato | A causa della gestione merge_preserve della regola di negazione sicura per impostazione predefinita, le sostituzioni a causa di autorizzazioni specifiche che comportano la necessità di riordinare l&#39;aggiornamento |
| `CQ62Html5SmartFileUpgrade` | &lt; 6.2 | Immediato | Rileva i componenti che utilizzano il widget Html5SmartFile, cerca gli utilizzi del componente nel contenuto e ristruttura la persistenza, spostando efficacemente il binario verso il basso e non archiviarlo a livello di componente. |
| `Cq62ProjectsCodeUpgrade` | &lt; 6.2 | Immediato | Sposta i progetti in stile precedente da **/etc/projects** a **/content/projects** |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6.2 | Immediato | Introduce un livello contenitore alla gerarchia (Aree) e regola i riferimenti. |
| `Cq62TargetContentUpgrade` | &lt; 6.2 | Immediato | Imposta i nomi della posizione fissa sui componenti di destinazione. |
| `Cq62WorkflowContentUpgrade` | &lt; 6.2 | Immediato | Trasformazione complessa dei modelli di flusso di lavoro precedente a strutture, istanze, notifiche 6.2 e unione dal percorso di backup **/var/backup** |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6.3 | Immediato | Sposta risorse, schemi di metadati personalizzati e profili di elaborazione da **/apps** a **/conf** e traduce lo schema metadati e i profili metadati dei moduli da coral2 a coral3. |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6,3 | Immediato | Sposta le risorse e i facet di ricerca personalizzati da **/apps** a **/conf** e traduce lo schema metadati e i profili metadati dei moduli da coral2 a coral3. |
| `CQ63InboxItemsUpgrade` | &lt; 6,3 | Immediato | Aggiorna InboxItems per ordinare gli elementi della casella in entrata (regolazione dei metadati per un ordinamento efficiente) |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6,3 | Immediato | Regola la proprietà metadataSchema nella cartella sostituendo i percorsi relativi in **/conf** al posto di **/apps** |
| `CQ63MobileAppsNavUpgrade` | &lt; 6,3 | Immediato | Regolazione della struttura di navigazione |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6,3 | Immediato | Sposta le configurazioni personalizzate per le dashboard di monitoraggio da **/libs** e **/apps** |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6,3 | Immediato | Traduce la proprietà processingProfile (utilizzata fino alla versione 6.1) in Assets in modo che corrisponda alla struttura 6.3 e versioni successive. Regola anche i percorsi relativi del profilo in **/conf** al posto di **/apps**. |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6,3 | Immediato | Attività di aggiornamento che rimuove le voci di menu obsolete di CRXDE Lite e della console Web in caso di aggiornamento. |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6,3 | Ritardato | Spostamento delle configurazioni cloud SRP, configurazioni di parole d&#39;ordine community, pulizia **/etc/social** e **/etc/enablement** (tutti i riferimenti e i dati devono essere regolati quando si esegue la migrazione pigra - nessuna parte dell&#39;applicazione deve più dipendere da questa struttura). |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6.4 | Ritardato | Pulizia **/etc/cloudsettings** (contenente la configurazione ContextHub). La configurazione viene migrata automaticamente al primo accesso. Nel caso in cui venga avviata la migrazione dei contenuti Lazy insieme all’aggiornamento di questo contenuto in **/etc/cloudsettings** deve essere mantenuto tramite pacchetto prima dell&#39;aggiornamento e reinstallato per la trasformazione implicita da avviare, insieme a una successiva disinstallazione del pacchetto dopo il completamento. |
| `CQ64UsersTitleFixTask` | &lt; 6.4 | Ritardato | Regola la struttura del titolo legacy in base al titolo nel nodo del profilo utente. |
| `CQ64CommerceMigrationTask` | &lt; 6.4 | Ritardato | Eseguire la migrazione dei contenuti di e-commerce da **/etc/commerce** a **/var/commerce**. Durante la migrazione il contenuto viene spostato e i riferimenti al contenuto spostato vengono aggiornati per riflettere la nuova posizione. |
| `CQ65DMMigrationTask` | &lt; 6.5 | Ritardato | Migrazione delle impostazioni catalogo legacy e delle impostazioni dei Cloud Services Dynamic Media da **/etc** a **/conf** |
| `CQ65LegacyClientlibsCleanupTask` | &lt; 6,5 | Ritardato | Pulizia delle clientlib legacy esistenti in **/etc/clientlibs** |
