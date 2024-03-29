---
title: Architettura di AEM Forms Workspace
description: Informazioni concettuali e panoramica dell’architettura di LiveCycle AEM Forms Workspace.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: c6f216d4-781c-4356-b9f0-3324903a28e7
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Architettura di AEM Forms Workspace {#aem-forms-workspace-architecture}

L’area di lavoro AEM Forms è un’applicazione web ospitata su CRX™. Quando l’area di lavoro viene aperta in un browser, si accede a una risorsa CRX e l’applicazione viene riprodotta come pagina HTML nel browser.

L’applicazione accede al server AEM Forms sugli endpoint REST per eseguire le seguenti operazioni:

* Recupera le attività utente, i punti d&#39;inizio processo, la cronologia processo e le informazioni utente
* Eseguire azioni sulle attività
* Eseguire query sulle attività nel database
* Aggiornare le preferenze utente e altro ancora

Il server AEM Forms accede al database di AEM Forms tramite JDBC. Il database consente di salvare in modo permanente le attività, i processi e le relative istanze, gli utenti e le informazioni correlate.

L’area di lavoro di AEM Forms è progettata in componenti modulari JavaScript™ che possono essere personalizzati individualmente e riutilizzati in altre applicazioni web. I componenti sono basati su BackBone, una libreria JavaScript che dà struttura alle applicazioni web. Un articolo dettagliato che descrive l’interazione dei componenti con BackBone è [qui](/help/forms/using/backbone-interaction.md). L’organizzazione dei componenti nella struttura delle cartelle CRX è discussa in [questo](/help/forms/using/folder-structure.md) articolo.

Pacchetti consegnati per l’area di lavoro di AEM Forms:

* `adobe-lc-workspace-pkg-<version>.zip`: si tratta di un pacchetto CRX, ovvero può essere distribuito in CRX utilizzando Gestione pacchetti.
* `adobe-lc-workspace-<version>-src.zip`: è un archivio che contiene il codice completo dell’area di lavoro di AEM Forms e gli script per creare i pacchetti di distribuzione: spedizione, debug e sviluppo.
