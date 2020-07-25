---
cloud: experience-cloud
product: adobe experience manager
audience: end-user
user-guide-title: Guida alla distribuzione di AEM 6.5
user-guide-description: Learn more about installing, deploying, and the architecture of Adobe Experience Manager 6.5, including our Adobe Managed Services cloud deployment.
translation-type: tm+mt
source-git-commit: 73fbf9c4f631e87132fbd9ef5cf769b4f8ce7a17
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 11%

---


# AEM 6.5 Deploying User Guide {#deploying}

+ [Guida utente alla distribuzione](home.md)
+ Introduzione ad AEM Platform {#introduction}
   + [Introduzione ad AEM Platform](platform.md)
   + [Requisiti tecnici](technical-requirements.md)
   + [Elementi di archiviazione in AEM 6.5](storage-elements-in-aem-6.md)
   + [AEM con MongoDB](aem-with-mongodb.md)
+ Implementazione di AEM {#deploying}
   + [Implementazione e manutenzione](deploy.md)
   + [Implementazioni consigliate](recommended-deploys.md)
   + [Installazione dell’applicazione da server](application-server-install.md)
   + [Installazione personalizzata indipendente](custom-standalone-install.md)
   + [Avvio e interruzione da riga di comando](command-line-start-and-stop.md)
   + [Configurazione degli archivi di nodi e degli archivi di dati in AEM 6](data-store-config.md)
   + [Pulizia revisioni](revision-cleanup.md)
   + [Query e indicizzazione Oak](queries-and-indexing.md)
   + [Come eseguire AEM con TarMK Cold Standby](tarmk-cold-standby.md)
   + [Supporto RDBMS in AEM 6.5](rdbms-support-in-aem.md)
   + [Indicizzazione tramite il Jar di esecuzione Oak](indexing-via-the-oak-run-jar.md)
   + [Indicizzazione Oak-run.jar - Casi di utilizzo](oak-run-indexing-usecases.md)
   + [Risoluzione dei problemi relativi agli indici Oak](troubleshooting-oak-indexes.md)
   + [Passaggio All&#39;Insieme Di Statistiche Di Utilizzo Aggregato](opt-in-aggregated-usage-statistics.md)
   + [Aggiorna definizioni veicolo di rilascio](update-release-vehicle-definitions.md)
   + [Risoluzione dei problemi](troubleshooting.md)
+ Configurazione di AEM {#configuring}
   + [Concetti di configurazione di base](configuring.md)
   + [Registrazione](configure-logging.md)
   + [Configurazione di OSGi](configuring-osgi.md)
   + [Impostazioni di configurazione OSGi](osgi-configuration-settings.md)
   + [Modalità di esecuzione](configure-runmodes.md)
   + [Console Web](web-console.md)
   + [Replica](replication.md)
   + [Replica mediante SSL reciproco](mssl-replication.md)
   + [Risoluzione dei problemi di replica](troubleshoot-rep.md)
   + [Scadenza degli oggetti statici](expiration-static-objects.md)
   + [Rimozione delle versioni](version-purging.md)
   + [Monitoraggio e manutenzione dell’istanza AEM](monitoring-and-maintaining.md)
   + [Scaricamento dei processi](offloading.md)
   + [Single Sign On](single-sign-on.md)
   + [Mapping delle risorse](resource-mapping.md)
   + [Abilitazione di HTTP su SSL](/help/sites-administering/ssl-by-default.md)
   + [Controlli di coerenza e di transito](consistency-check.md)
   + [Linee guida sulle prestazioni](performance-guidelines.md)
   + [Ottimizzazione delle prestazioni](configuring-performance.md)
   + [Guida alle prestazioni di Risorse](assets-performance-sizing.md)
   + [Articoli guida alla configurazione](ht-deploy.md)
   + [Configurazione della console Web](configuring-web-console.md)
+ Upgrading to AEM 6.5 {#upgrading}
   + [Aggiornamento ad AEM 6.5](upgrade.md)
   + [Pianificazione dell&#39;aggiornamento](upgrade-planning.md)
   + [Valutazione della complessità dell&#39;aggiornamento con il rilevamento dei pattern](pattern-detector.md)
   + [Compatibilità con le versioni precedenti in AEM 6.5](backward-compatibility.md)
   + [Procedura di aggiornamento](upgrade-procedure.md)
   + [Esecuzione di un aggiornamento locale](in-place-upgrade.md)
   + [Lazy Content Migration](lazy-content-migration.md)
   + [Utilizzo dello strumento di migrazione CRX2Oak](using-crx2oak.md)
   + [Attività di manutenzione pre-aggiornamento](pre-upgrade-maintenance-tasks.md)
   + [Post Upgrade Checks e risoluzione dei problemi](post-upgrade-checks-and-troubleshooting.md)
   + [Aggiornamento di moduli di ricerca personalizzati](upgrading-custom-search-forms.md)
   + [Aggiornamenti sostenibili](sustainable-upgrades.md)
   + [Aggiornamento di codice e personalizzazioni](upgrading-code-and-customizations.md)
   + [Passaggi di aggiornamento per le installazioni di Application Server](app-server-upgrade.md)
   + [Elenco dei pacchetti obsoleti disinstallati dopo l&#39;aggiornamento](obsolete-bundles.md)
+ Ristrutturazione repository {#restructuring}
   + [Ristrutturazione repository in AEM 6.5](repository-restructuring.md)
   + [Ristrutturazione del repository comune in AEM 6.5](all-repository-restructuring-in-aem-6-5.md)
   + [Ristrutturazione del repository dei siti in AEM 6.5](sites-repository-restructuring-in-aem-6-5.md)
   + [Ristrutturazione dell&#39;archivio risorse in AEM 6.5](assets-repository-restructuring-in-aem-6-5.md)
   + [Ristrutturazione dell&#39;archivio Dynamic Media in AEM 6.5](dynamicmedia-repository-restructuring-in-aem-6-5.md)
   + [Ristrutturazione dell&#39;archivio moduli in AEM 6.5](forms-repository-restructuring-in-aem-6-5.md)
   + [Ristrutturazione del repository di e-commerce in AEM 6.5](ecommerce-repository-restructuring-in-aem-6-5.md)
   + [Ristrutturazione del repository per AEM Communities in 6.5](communities-repository-restructuring-in-aem-6-5.md)
+ eCommerce {#ecommerce}
   + [Panoramica di eCommerce](ecommerce.md)
   + [SAP Commerce Cloud](sap-commerce-cloud.md)
   + [Salesforce Commerce Cloud](https://github.com/adobe/commerce-salesforce)
   + [Magento](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/integrations.html#!AdobeDocs/commerce-cif-documentation/master/integrations/02-AEM-Magento.md)
+ Best practice  {#practices}
   + [Best practice di distribuzione](best-practices.md)
   + [Struttura delle prestazioni](performance-tree.md)
   + [Best practice per il test delle prestazioni](best-practices-for-performance-testing.md)
   + [Best practice per query e indicizzazione](best-practices-for-queries-and-indexing.md)
   + [Raccomandazioni in merito all&#39;interfaccia utente per i clienti](ui-recommendations.md)
   + [Prestazioni e scalabilità](performance.md)
