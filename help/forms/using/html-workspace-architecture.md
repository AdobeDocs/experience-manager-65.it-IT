---
title: ' AEM Forms Workspace Architecture'
seo-title: ' AEM Forms Workspace Architecture'
description: Informazioni concettuali e panoramica dell'architettura dell'area di lavoro di LiveCycle  AEM Forms.
seo-description: Informazioni concettuali e panoramica dell'architettura dell'area di lavoro di LiveCycle  AEM Forms.
uuid: e1a48452-ed44-4ea7-ba38-d961c8faafa5
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c3a312fb-f684-477d-916d-2d3c99aa7607
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---


#  Architettura di AEM Forms Workspace {#aem-forms-workspace-architecture}

&#39;area di lavoro AEM Forms è un&#39;applicazione Web ospitata su CRX™. Quando l&#39;area di lavoro viene aperta in un browser, si accede a una risorsa CRX e l&#39;applicazione viene rappresentata come pagina HTML nel browser.

L&#39;applicazione accede  server AEM Forms sugli endpoint REST per eseguire le operazioni seguenti:

* Recupero di attività utente, punti di avvio del processo, cronologia del processo e informazioni utente
* Esecuzione di azioni sulle attività
* Attività di query nel database
* Aggiornare le preferenze utente e altro

Il server AEM Forms  accede  database AEM Forms tramite JDBC. Il database persiste nelle attività, nei processi e nelle relative istanze, negli utenti e nelle relative informazioni.

L&#39;area di lavoro di  AEM Forms è progettata per componenti JavaScript™ modulari che possono essere personalizzati e riutilizzati in altre applicazioni Web. I componenti sono basati su BackBone, una libreria JavaScript che fornisce struttura alle applicazioni Web. Un articolo dettagliato che descrive l&#39;interazione dei componenti con BackBone è [qui](/help/forms/using/backbone-interaction.md). L&#39;organizzazione dei componenti nella struttura di cartelle CRX è descritta nell&#39;articolo [this](/help/forms/using/folder-structure.md).

Pacchetti consegnati per &#39;area di lavoro AEM Forms:

* `adobe-lc-workspace-pkg-<version>.zip`: È un pacchetto CRX, ovvero può essere distribuito in CRX utilizzando Package Manager.
* `adobe-lc-workspace-<version>-src.zip`: Si tratta di un archivio che contiene il codice completo dell&#39;area di lavoro  AEM Forms e degli script per creare i pacchetti di distribuzione: Spedizione, Debug e Sviluppo.
