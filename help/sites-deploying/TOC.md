---
cloud: Experience Cloud
product: adobe experience manager
solution: Experience Manager, Experience Manager Sites
audience: end-user
user-guide-title: Guida alla distribuzione di AEM 6.5
breadcrumb-title: Guida alla distribuzione
user-guide-description: Informazioni sull’installazione, la distribuzione e l’architettura di Adobe Experience Manager 6.5, inclusa la distribuzione cloud di Adobe Managed Services.
feature: Deploying
role: Architect
source-git-commit: f29612ee633d2a62144b770f3c225fc82b9174f8
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 12%

---


# Guida utente alla distribuzione di AEM 6.5 {#deploying}

+ [Guida utente alla distribuzione](home.md)
+ Introduzione alla piattaforma AEM {#introduction}
   + [Introduzione alla piattaforma AEM](platform.md)
   + [Requisiti tecnici](technical-requirements.md)
   + [Elementi di conservazione in AEM 6.5](storage-elements-in-aem-6.md)
   + [AEM con MongoDB](aem-with-mongodb.md)
+ Distribuzione dell’AEM {#deploying}
   + [Distribuzione e manutenzione](deploy.md)
   + [Distribuzioni consigliate](recommended-deploys.md)
   + [Installazione server applicazioni](application-server-install.md)
   + [Installazione autonoma personalizzata](custom-standalone-install.md)
   + [Avvio e arresto riga di comando](command-line-start-and-stop.md)
   + [Configurazione degli archivi dei nodi e dei dati in AEM 6](data-store-config.md)
   + [Pulizia revisioni](revision-cleanup.md)
   + [Query e indicizzazione Oak](queries-and-indexing.md)
   + [Come eseguire l’AEM con TarMK Cold Standby](tarmk-cold-standby.md)
   + [Supporto RDBMS nell’AEM 6.5](rdbms-support-in-aem.md)
   + [Indicizzazione tramite Oak-run Jar](indexing-via-the-oak-run-jar.md)
   + [Casi di utilizzo dell’indicizzazione Oak-run.jar](oak-run-indexing-usecases.md)
   + [Risoluzione dei problemi degli indici Oak](troubleshooting-oak-indexes.md)
   + [Accesso alla raccolta di statistiche di utilizzo aggregate](opt-in-aggregated-usage-statistics.md)
   + [Risoluzione dei problemi](troubleshooting.md)
+ Configurazione dell’AEM {#configuring}
   + [Concetti di base sulla configurazione](configuring.md)
   + [Registrazione](configure-logging.md)
   + [Configurazione di OSGi](configuring-osgi.md)
   + [Impostazioni configurazione OSGi](osgi-configuration-settings.md)
   + [Modalità di esecuzione](configure-runmodes.md)
   + [Console Web](web-console.md)
   + [Replica](replication.md)
   + [Replica tramite SSL reciproco](mssl-replication.md)
   + [Risoluzione dei problemi di replica](troubleshoot-rep.md)
   + [Scadenza degli oggetti statici](expiration-static-objects.md)
   + [Rimozione versione](version-purging.md)
   + [Monitoraggio e manutenzione dell’istanza AEM](monitoring-and-maintaining.md)
   + [Offload dei processi](offloading.md)
   + [Single Sign-On](single-sign-on.md)
   + [Mappatura delle risorse](resource-mapping.md)
   + [Abilitazione di HTTP su SSL](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/ssl-by-default.html)
   + [Controlli di coerenza e di attraversamento](consistency-check.md)
   + [Linee guida sulle prestazioni](performance-guidelines.md)
   + [Ottimizzazione delle prestazioni](configuring-performance.md)
   + [Guida alle prestazioni di Assets](assets-performance-sizing.md)
   + [Articoli pratici sulla configurazione](ht-deploy.md)
   + [Configurazione della console web](configuring-web-console.md)
+ Aggiornamento a AEM 6.5 {#upgrading}
   + [Aggiornamento a AEM 6.5](upgrade.md)
   + [Pianificazione dell&#39;aggiornamento](upgrade-planning.md)
   + [Valutazione della complessità dell’aggiornamento con il rilevatore pattern](pattern-detector.md)
   + [Compatibilità con le versioni precedenti in AEM 6.5](backward-compatibility.md)
   + [Procedura di aggiornamento](upgrade-procedure.md)
   + [Esecuzione di un aggiornamento sul posto](in-place-upgrade.md)
   + [Utilizzo della reindicizzazione offline per ridurre i tempi di inattività durante un aggiornamento](upgrade-offline-reindexing.md)
   + [Migrazione dei contenuti differita](lazy-content-migration.md)
   + [Utilizzo dello strumento di migrazione CRX2Oak](using-crx2oak.md)
   + [Attività di manutenzione pre-aggiornamento](pre-upgrade-maintenance-tasks.md)
   + [Controlli post-aggiornamento e risoluzione dei problemi](post-upgrade-checks-and-troubleshooting.md)
   + [Aggiornamento del Forms di ricerca personalizzato](upgrading-custom-search-forms.md)
   + [Aggiornamenti sostenibili](sustainable-upgrades.md)
   + [Aggiornamento del codice e delle personalizzazioni](upgrading-code-and-customizations.md)
   + [Passaggi per l&#39;aggiornamento delle installazioni di Application Server](app-server-upgrade.md)
   + [Elenco dei bundle obsoleti disinstallati dopo l&#39;aggiornamento](obsolete-bundles.md)
+ Ristrutturazione dell’archivio {#restructuring}
   + [Ristrutturazione dell’archivio in AEM 6.5](repository-restructuring.md)
   + [Ristrutturazione dell’archivio comune in AEM 6.5](all-repository-restructuring-in-aem-6-5.md)
   + [Ristrutturazione dell’archivio Sites in AEM 6.5](sites-repository-restructuring-in-aem-6-5.md)
   + [Ristrutturazione dell&#39;archivio di asset in AEM 6.5](assets-repository-restructuring-in-aem-6-5.md)
   + [Ristrutturazione dell’archivio Dynamic Media nell’AEM 6.5](dynamicmedia-repository-restructuring-in-aem-6-5.md)
   + [Ristrutturazione dell’archivio Forms nell’AEM 6.5](forms-repository-restructuring-in-aem-6-5.md)
   + [Ristrutturazione dell’archivio di e-commerce in AEM 6.5](ecommerce-repository-restructuring-in-aem-6-5.md)
   + [Ristrutturazione dell’archivio per AEM Communities nella versione 6.5](communities-repository-restructuring-in-aem-6-5.md)
+ Best practice   {#practices}
   + [Implementazione delle best practice](best-practices.md)
   + [Albero prestazioni](performance-tree.md)
   + [Best practice per i test delle prestazioni](best-practices-for-performance-testing.md)
   + [Best practice per query e indicizzazione](best-practices-for-queries-and-indexing.md)
   + [Interfaccia utente di Recommendations per i clienti](ui-recommendations.md)
   + [Prestazioni e scalabilità](performance.md)
