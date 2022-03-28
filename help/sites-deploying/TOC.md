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
ht-degree: 18%

---


# Guida utente alla distribuzione di AEM 6.5 {#deploying}

+ [Guida utente alla distribuzione](home.md)
+ Introduzione alla piattaforma AEM {#introduction}
   + [Introduzione alla piattaforma AEM](platform.md)
   + [Requisiti tecnici](technical-requirements.md)
   + [Elementi di storage in AEM 6.5](storage-elements-in-aem-6.md)
   + [AEM con MongoDB](aem-with-mongodb.md)
+ Implementazione di AEM {#deploying}
   + [Implementazione e manutenzione](deploy.md)
   + [Implementazioni consigliate](recommended-deploys.md)
   + [Installazione dell’applicazione da server](application-server-install.md)
   + [Installazione personalizzata indipendente](custom-standalone-install.md)
   + [Avvio e interruzione da riga di comando](command-line-start-and-stop.md)
   + [Configurazione degli archivi di nodi e degli archivi di dati nel AEM 6](data-store-config.md)
   + [Pulizia revisioni](revision-cleanup.md)
   + [Query e indicizzazione Oak](queries-and-indexing.md)
   + [Come eseguire AEM con lo standby a freddo TarMK](tarmk-cold-standby.md)
   + [Supporto RDBMS in AEM 6.5](rdbms-support-in-aem.md)
   + [Indicizzazione tramite Oak-run Jar](indexing-via-the-oak-run-jar.md)
   + [Casi d&#39;uso dell&#39;indicizzazione Oak-run.jar](oak-run-indexing-usecases.md)
   + [Risoluzione dei problemi degli indici Oak](troubleshooting-oak-indexes.md)
   + [Consenso alla raccolta di statistiche di utilizzo aggregate](opt-in-aggregated-usage-statistics.md)
   + [Risoluzione dei problemi](troubleshooting.md)
+ Configurazione di AEM {#configuring}
   + [Concetti di configurazione di base](configuring.md)
   + [Registrazione](configure-logging.md)
   + [Configurazione di OSGi](configuring-osgi.md)
   + [Impostazioni di configurazione OSGi](osgi-configuration-settings.md)
   + [Modalità di esecuzione](configure-runmodes.md)
   + [Console Web](web-console.md)
   + [Replica](replication.md)
   + [Replicazione con SSL reciproco](mssl-replication.md)
   + [Risoluzione dei problemi di replica](troubleshoot-rep.md)
   + [Scadenza degli oggetti statici](expiration-static-objects.md)
   + [Rimozione delle versioni](version-purging.md)
   + [Monitoraggio e manutenzione dell’istanza AEM](monitoring-and-maintaining.md)
   + [Offload dei processi](offloading.md)
   + [Single Sign On](single-sign-on.md)
   + [Mappatura delle risorse](resource-mapping.md)
   + [Abilitazione di HTTP su SSL](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/ssl-by-default.html)
   + [Controlli di coerenza e di transito](consistency-check.md)
   + [Linee guida sulle prestazioni](performance-guidelines.md)
   + [Ottimizzazione delle prestazioni](configuring-performance.md)
   + [Guida alle prestazioni di Assets](assets-performance-sizing.md)
   + [Articoli dimostrativi sulla configurazione](ht-deploy.md)
   + [Configurazione della console Web](configuring-web-console.md)
+ Aggiornamento a AEM 6.5 {#upgrading}
   + [Aggiornamento a AEM 6.5](upgrade.md)
   + [Pianificazione dell&#39;aggiornamento](upgrade-planning.md)
   + [Valutazione della complessità dell’aggiornamento con il rilevatore pattern](pattern-detector.md)
   + [Compatibilità con le versioni precedenti in AEM 6.5](backward-compatibility.md)
   + [Procedura di aggiornamento](upgrade-procedure.md)
   + [Esecuzione di un aggiornamento sul posto](in-place-upgrade.md)
   + [Utilizzo della reindicizzazione offline per ridurre i tempi di inattività durante un aggiornamento](upgrade-offline-reindexing.md)
   + [Migrazione dei contenuti Lazy](lazy-content-migration.md)
   + [Utilizzo dello strumento di migrazione CRX2Oak](using-crx2oak.md)
   + [Attività di manutenzione pre-aggiornamento](pre-upgrade-maintenance-tasks.md)
   + [Controlli e risoluzione dei problemi post-aggiornamento](post-upgrade-checks-and-troubleshooting.md)
   + [Aggiornamento di Custom Search Forms](upgrading-custom-search-forms.md)
   + [Aggiornamenti sostenibili](sustainable-upgrades.md)
   + [Aggiornamento di codice e personalizzazioni](upgrading-code-and-customizations.md)
   + [Passaggi di aggiornamento per le installazioni di Application Server](app-server-upgrade.md)
   + [Elenco dei bundle obsoleti disinstallati dopo l&#39;aggiornamento](obsolete-bundles.md)
+ Ristrutturazione dell’archivio {#restructuring}
   + [Ristrutturazione dell’archivio in AEM 6.5](repository-restructuring.md)
   + [Ristrutturazione dell’archivio comune in AEM 6.5](all-repository-restructuring-in-aem-6-5.md)
   + [Ristrutturazione dell’archivio siti in AEM 6.5](sites-repository-restructuring-in-aem-6-5.md)
   + [Ristrutturazione dell’archivio risorse in AEM 6.5](assets-repository-restructuring-in-aem-6-5.md)
   + [Ristrutturazione dell&#39;archivio Dynamic Media in AEM 6.5](dynamicmedia-repository-restructuring-in-aem-6-5.md)
   + [Ristrutturazione dell&#39;archivio Forms in AEM 6.5](forms-repository-restructuring-in-aem-6-5.md)
   + [Ristrutturazione dell’archivio di e-commerce in AEM 6.5](ecommerce-repository-restructuring-in-aem-6-5.md)
   + [Ristrutturazione dell’archivio per AEM Communities nella versione 6.5](communities-repository-restructuring-in-aem-6-5.md)
+ Best practice   {#practices}
   + [Best practice di distribuzione](best-practices.md)
   + [Struttura delle prestazioni](performance-tree.md)
   + [Tecniche consigliate per il test delle prestazioni](best-practices-for-performance-testing.md)
   + [Tecniche consigliate per query e indicizzazione](best-practices-for-queries-and-indexing.md)
   + [Interfaccia utente Recommendations per clienti](ui-recommendations.md)
   + [Prestazioni e scalabilità](performance.md)
