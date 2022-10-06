---
title: Panoramica di Health Monitor
seo-title: Overview of Health Monitor
description: Questo documento fornisce la panoramica del monitoraggio dello stato e i dettagli su come accedervi.
seo-description: This document provides the overview of the Health monitor, and details about how you can access it.
uuid: 5934fd2d-80a5-4c6d-b3ee-882c2865705b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c303e967-944d-40b0-96ca-f91e2f42a0d0
exl-id: 05f8b430-141e-4921-98b1-a0d8f636e478
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# Panoramica di Health Monitor {#overview-of-health-monitor}

Health Monitor fornisce informazioni critiche sul sistema dei moduli AEM, ad esempio informazioni sul server, sull&#39;utilizzo della memoria e del processore. Sono inoltre disponibili le statistiche di Work Manager, ad esempio il numero di elementi di lavoro o processi in coda e i relativi stati. È possibile eseguire le seguenti attività utilizzando Monitoraggio integrità:

* Verifica che il sistema funzioni correttamente
* Visualizzazione delle informazioni per diagnosticare i problemi del sistema nel momento in cui si verificano
* Eseguire operazioni su elementi di lavoro o processi che presentano problemi
* Eliminare i record obsoleti dal database di Job Manager

La pagina Monitoraggio integrità nella console di amministrazione dispone di tre schede:

* Nella scheda Sistema sono visualizzati i grafici di monitoraggio delle risorse e le informazioni sul server dei moduli (o sul nodo in un ambiente cluster). (Vedi [Visualizza informazioni sul sistema](/help/forms/using/admin-help/view-system-information.md#view-system-information).)
* Nella scheda Work Manager sono visualizzati i dati relativi a Work Manager, ad esempio il numero di elementi di lavoro nella coda di Work Manager. È possibile filtrare le informazioni utilizzando vari criteri o gestire singoli elementi di lavoro utilizzando gli strumenti operativi. (Vedi [Visualizza le statistiche relative a Work Manager](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager).)
* La scheda Utilità di pianificazione eliminazione processi consente di eliminare i record obsoleti dal database di Gestione processi. (Vedi [Eliminare i record dal database di Job Manager](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)

La pagina web di Monitoraggio integrità è compilata con le statistiche raccolte tramite un’API Gemfire. Questa API rileva automaticamente tutti i nodi in un cluster. Risolve anche i problemi di sicurezza che si verificano durante la raccolta di statistiche da server proxy o load balancer. Sono disponibili opzioni Java per regolare con precisione Monitor integrità, riducendo l’impatto sulle prestazioni dell’ambiente dei moduli AEM. (Vedi [Ottimizzazione delle prestazioni di Health Monitor](/help/forms/using/admin-help/fine-tuning-health-monitor-performance.md#fine-tuning-health-monitor-performance).)

**Accedere a Health Monitor**

1. Nella console di amministrazione, fai clic su Monitoraggio integrità nell’angolo in alto a destra della pagina.
