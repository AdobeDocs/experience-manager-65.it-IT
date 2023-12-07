---
title: Panoramica di Health Monitor
description: Questo documento fornisce una panoramica di Health Monitor e informazioni dettagliate su come accedervi.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 05f8b430-141e-4921-98b1-a0d8f636e478
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# Panoramica di Health Monitor {#overview-of-health-monitor}

Health Monitor fornisce informazioni critiche sul sistema dei moduli AEM, come informazioni sui server, l&#39;utilizzo della memoria e l&#39;utilizzo del processore. Sono inoltre disponibili le statistiche di Work Manager, ad esempio il numero di elementi di lavoro o processi in coda e i relativi stati. È possibile eseguire le seguenti attività utilizzando Health Monitor:

* Verificare che il sistema funzioni correttamente
* Visualizza informazioni per la diagnosi dei problemi di sistema quando si verificano
* Eseguire operazioni su elementi di lavoro o processi che presentano problemi
* Eliminare i record obsoleti dal database di Gestione processi

La pagina Health Monitor nella console di amministrazione dispone di tre schede:

* Nella scheda Sistema vengono visualizzati i grafici di monitoraggio delle risorse e le informazioni sul server Forms (o sul nodo in un ambiente cluster). (vedere [Visualizza informazioni di sistema](/help/forms/using/admin-help/view-system-information.md#view-system-information).)
* Nella scheda Gestione lavoro vengono visualizzati i dati correlati a Gestione lavoro, ad esempio il numero di elementi di lavoro nella coda di Gestione lavoro. È possibile filtrare le informazioni utilizzando vari criteri o gestire singoli elementi di lavoro utilizzando gli strumenti operativi. (vedere [Visualizzare le statistiche relative a Work Manager](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager).)
* La scheda Utilità di pianificazione eliminazione job consente di rimuovere i record obsoleti dal database di Gestione job. (vedere [Eliminare i record dal database di Gestione processi](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)

La pagina Web Health Monitor è compilata con statistiche raccolte tramite un&#39;API Gemfire. Questa API rileva automaticamente tutti i nodi in un cluster. Risolve inoltre i problemi di sicurezza che si verificano durante la raccolta di statistiche da dietro server proxy o load balancer. Sono disponibili opzioni Java per ottimizzare Health Monitor, riducendo l’impatto sulle prestazioni dell’ambiente dei moduli AEM. (vedere [Ottimizzazione delle prestazioni di Health Monitor](/help/forms/using/admin-help/fine-tuning-health-monitor-performance.md#fine-tuning-health-monitor-performance).)

**Accedi a Health Monitor**

1. Nella console di amministrazione, fare clic su Health Monitor nell&#39;angolo superiore destro della pagina.
