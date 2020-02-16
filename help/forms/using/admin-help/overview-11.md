---
title: Panoramica di Health Monitor
seo-title: Panoramica di Health Monitor
description: Questo documento fornisce una panoramica del monitoraggio dello stato e informazioni su come accedervi.
seo-description: Questo documento fornisce una panoramica del monitoraggio dello stato e informazioni su come accedervi.
uuid: 5934fd2d-80a5-4c6d-b3ee-882c2865705b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c303e967-944d-40b0-96ca-f91e2f42a0d0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Panoramica di Health Monitor {#overview-of-health-monitor}

Health Monitor fornisce informazioni critiche sul sistema di moduli AEM, come informazioni sul server, sull&#39;utilizzo della memoria e sul processore. Sono inoltre disponibili le statistiche di Work Manager, ad esempio il numero di elementi di lavoro o processi in coda e i relativi stati. Con il Monitor integrità potete eseguire le seguenti operazioni:

* Verificare che il sistema sia in esecuzione correttamente
* Visualizzazione delle informazioni per diagnosticare i problemi del sistema man mano che si verificano
* Eseguire operazioni su elementi di lavoro o processi che presentano problemi
* Rimozione di record obsoleti dal database di Gestione processi

La pagina Monitoraggio stato nella console di amministrazione presenta tre schede:

* Nella scheda Sistema sono visualizzati i grafici di monitoraggio delle risorse e le informazioni sul server o sul nodo dei moduli in un ambiente cluster. Consultate [Visualizzare le informazioni](/help/forms/using/admin-help/view-system-information.md#view-system-information)di sistema.
* La scheda Work Manager visualizza i dati relativi a Work Manager, ad esempio il numero di elementi di lavoro nella coda di Work Manager. Potete filtrare le informazioni utilizzando vari criteri o gestire singoli elementi di lavoro utilizzando gli strumenti operativi. (Vedere [Visualizzare le statistiche relative a Work Manager](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager).)
* La scheda Utilità di pianificazione rimozione processo consente di eliminare i record obsoleti dal database di Gestione processi. (vedere [Eliminare i record dal database](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database)di Gestione processi.)

La pagina Web Health Monitor è composta da statistiche raccolte tramite un&#39;API Gemfire. Questa API rileva automaticamente tutti i nodi di un cluster. Risolve inoltre i problemi di sicurezza che si verificano durante la raccolta di statistiche da server proxy o dai sistemi di bilanciamento del carico. Sono disponibili opzioni Java per configurare il Monitor integrità in modo da ridurre l&#39;impatto sulle prestazioni dell&#39;ambiente dei moduli AEM. (vedere [Ottimizzazione delle prestazioni](/help/forms/using/admin-help/fine-tuning-health-monitor-performance.md#fine-tuning-health-monitor-performance)del monitor di stato).

**Monitoraggio integrità accesso**

1. Nella console di amministrazione, fate clic su Monitoraggio stato nell’angolo superiore destro della pagina.

