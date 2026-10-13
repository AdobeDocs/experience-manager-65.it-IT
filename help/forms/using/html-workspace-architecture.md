---
title: Architettura dell’area di lavoro di AEM Forms
description: Informazioni concettuali e panoramica dell’architettura dell’area di lavoro di AEM Forms LiveCycle.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: c6f216d4-781c-4356-b9f0-3324903a28e7
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 3%
---
# Architettura dell’area di lavoro di AEM Forms {#aem-forms-workspace-architecture}

AEM Forms Workspace è un’applicazione web ospitata su CRX™. Quando l’area di lavoro viene aperta in un browser, si accede a una risorsa CRX e l’applicazione viene riprodotta come pagina HTML nel browser.

L’applicazione accede al server AEM Forms sugli endpoint REST per eseguire le seguenti operazioni:

* Recupera le attività utente, i punti d&#39;inizio processo, la cronologia processo e le informazioni utente
* Eseguire azioni sulle attività
* Eseguire query sulle attività nel database
* Aggiornare le preferenze utente e altro ancora

Il server AEM Forms accede al database di AEM Forms tramite JDBC. Il database consente di salvare in modo permanente le attività, i processi e le relative istanze, gli utenti e le informazioni correlate.

L’area di lavoro di AEM Forms è progettata in componenti modulari JavaScript™ che possono essere personalizzati individualmente e riutilizzati in altre applicazioni web. I componenti sono basati su BackBone, una libreria JavaScript che dà struttura alle applicazioni web. Un articolo dettagliato che descrive l&#39;interazione dei componenti con BackBone è [qui](/help/forms/using/backbone-interaction.md). L&#39;organizzazione dei componenti nella struttura di cartelle di CRX è descritta in [questo](/help/forms/using/folder-structure.md) articolo.

Pacchetti consegnati per l’area di lavoro di AEM Forms:

* `adobe-lc-workspace-pkg-<version>.zip`: è un pacchetto CRX, ovvero può essere distribuito in CRX utilizzando Gestione pacchetti.
* `adobe-lc-workspace-<version>-src.zip`: è un archivio che contiene il codice completo dell&#39;area di lavoro AEM Forms e gli script per la creazione dei pacchetti di distribuzione: spedizione, debug e sviluppo.
