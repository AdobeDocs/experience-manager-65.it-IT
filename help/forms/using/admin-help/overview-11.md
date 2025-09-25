---
title: Panoramica sul monitoraggio dello stato
description: Questo documento fornisce una panoramica sul monitoraggio dello stato e informazioni dettagliate sulle modalità di accesso.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 05f8b430-141e-4921-98b1-a0d8f636e478
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '296'
ht-degree: 100%

---

# Panoramica sul monitoraggio dello stato {#overview-of-health-monitor}

Il monitoraggio dello stato fornisce informazioni critiche sul sistema AEM Forms, ad esempio informazioni sul server, sull’utilizzo della memoria e sull’utilizzo del processore. Sono inoltre disponibili le statistiche di Work Manager, ad esempio il numero di elementi di lavoro o processi in coda e i relativi stati. È possibile eseguire le seguenti attività utilizzando Health Monitor:

* Verificare che il sistema funzioni correttamente
* Visualizzare informazioni per la diagnosi dei problemi di sistema quando si verificano
* Eseguire operazioni su elementi di lavoro o processi che presentano problemi
* Eliminare i record obsoleti dal database di Gestione processo

La pagina Health Monitor nella console di amministrazione dispone di tre schede:

* Nella scheda Sistema vengono visualizzati i grafici di monitoraggio delle risorse e le informazioni sul server Forms (o sul nodo in un ambiente cluster). (Consulta [Visualizza informazioni di sistema](/help/forms/using/admin-help/view-system-information.md#view-system-information).)
* Nella scheda Work manager vengono visualizzati i dati correlati a Work manager, ad esempio il numero di elementi di lavoro nella coda di Work manager. È possibile filtrare le informazioni utilizzando vari criteri o gestire singoli elementi di lavoro utilizzando gli strumenti operativi. (Consulta [Visualizza statistiche relative a Work Manager](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager).)
* La scheda Pianificazione eliminazione lavori consente di eliminare i record obsoleti dal database di Gestione processo. (Consulta [Eliminare i record dal database di Gestione processo](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)

La pagina web Health Monitor presenta le statistiche raccolte tramite un’API Gemfire. Questa API rileva automaticamente tutti i nodi in un cluster. Risolve inoltre i problemi di sicurezza che si verificano durante la raccolta di statistiche da dietro server proxy o load balancer. Sono disponibili opzioni Java per ottimizzare Health Monitor, riducendo l’impatto sulle prestazioni dell’ambiente AEM Forms. (Consulta [Ottimizzazione delle prestazioni di Health Monitor](/help/forms/using/admin-help/fine-tuning-health-monitor-performance.md#fine-tuning-health-monitor-performance).)

**Accesso a Health Monitor**

1. Nella console di amministrazione, fai clic su Health Monitor nell’angolo superiore destro della pagina.
