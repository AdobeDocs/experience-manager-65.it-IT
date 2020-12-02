---
title: Configurazione delle funzioni di abilitazione
seo-title: Configurazione delle funzioni di abilitazione
description: Configurare le funzioni di abilitazione in Communities
seo-description: Configurare le funzioni di abilitazione in Communities
uuid: 27be3128-1a7d-412e-99a9-6e3b3b0aec1c
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 765a3d9b-4552-403e-872c-fdf684ac271d
translation-type: tm+mt
source-git-commit: ce21755263a2e8a3f0e97acb7f586e32cedde83a
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---


# Configurazione delle funzioni di abilitazione {#configuring-enablement-features}

## Panoramica {#overview}

Le funzioni di abilitazione consentono di creare [community di abilitazione](overview.md#enablement-community).

* Questa funzione richiede licenze aggiuntive per l&#39;utilizzo in un ambiente di produzione.

L&#39;utilizzo delle funzioni di abilitazione richiede quanto segue:

Installazione di:

* **SCORM**

   SCORM (Shared Content Object Reference Model) è una raccolta di standard e specifiche per l&#39;e-learning. SCORM definisce anche come il contenuto può essere incluso in un file ZIP trasferibile.

* **MySQL**

   MySQL è un database relazionale utilizzato principalmente per il tracciamento SCORM e i dati di reporting per l&#39;abilitazione, nonché tabelle per il monitoraggio dell&#39;avanzamento video. Il pacchetto di funzioni SCORM per l&#39;abilitazione richiede il driver JDBC MySQL.

* **FFmpeg**

   FFmpeg è una soluzione per la conversione e lo streaming audio e video e, se installato, viene utilizzato per la corretta transcodifica di [Video Assets](../../help/sites-authoring/default-components-foundation.md#video). Per le comunità di abilitazione, viene utilizzata nell’ambiente di authoring per ottenere i metadati per le risorse caricate e generare una miniatura da visualizzare quando si elenca le risorse.

Configurazione di:

* **Manager community**

   Per le comunità di abilitazione, solo ai membri del gruppo di utenti `Community Enablement Managers` può essere assegnato il ruolo di `Community Site Enablement Manager`, le cui autorizzazioni possono includere la creazione di contenuto, le assegnazioni e la gestione di membri nell&#39;ambiente di pubblicazione.

Configurazione opzionale di:

* **Adobe Analytics**

   L&#39;integrazione con  Adobe Analytics aggiunge funzionalità di reporting complete e supporta l&#39;aggiunta di heartbeat video ad Analytics.

* **Dispatcher**

## Passaggi di configurazione {#configuration-steps}

Di seguito sono riportati i passaggi necessari per abilitare le community.

Ogni passaggio fa riferimento alla documentazione che fornisce i dettagli necessari.

**Per tutte le istanze di creazione/pubblicazione:**

1. **[Installare il driver JDBC per MySQL](deploy-communities.md#jdbc-driver-for-mysql)**

   Usa console Web (bundle): *http://localhost:4502/system/console/bundles*

   Installare *prima* l&#39;installazione del pacchetto SCORM

1. **[Installare il pacchetto SCORM](deploy-communities.md#scorm-package)**


   Usa Gestione pacchetti: *http://localhost:4502/crx/packmgr/*

**Su qualsiasi server:**

1. **[Installazione di MySQL, MySQL Workbench](mysql.md)**

1. **[Installare i database MySQL](mysql.md#database-setup)**

   Esecuzione di script SQL scaricati dall&#39;istanza di creazione

   Utilizzare Workbench MySQL

**Sulla stessa istanza di creazione del server host:**

1. **[Installare FFmpeg](ffmpeg.md)**

**Per tutte le istanze di creazione/pubblicazione:**

1. **[Configurare il pool di connessioni JDBC](mysql.md#configure-jdbc-connections)**

   Usa console Web (configMgr): *http://localhost:4502/system/console/configMgr*

1. **[Configurare il servizio motore SCORM](mysql.md#aem-communities-scormengine-service)**

   Usa console Web (configMgr): *http://localhost:4502/system/console/configMgr*

1. **[Configurare i filtri CSRF](mysql.md#adobe-granite-csrf-filter)**

   Usa console Web (configMgr): *http://localhost:4502/system/console/configMgr*

**Nell’istanza di creazione:**

1. (*Facoltativo*) **[Configura servizio Analytics](analytics.md)**

   Usa console Strumenti, Implementazione, Cloud Services: *http://localhost:4502/etc/cloudservices/sitecatalyst.html*

1. **[Configurare FFmpeg](ffmpeg.md#configure-ffmpeg-transcoding-service)**

   Usa console Flusso di lavoro/Modelli

1. **[Abilita servizio tunnel](deploy-communities.md#tunnel-service-on-author)**

   Usa console Web (configMgr): *http://localhost:4502/system/console/configMgr*

1. **[Creazione di amministratori community](users.md#creating-community-members)**

   Per l’ambiente di authoring utilizzate la console di sicurezza dell’interfaccia classica: *http://localhost:4502/useradmin*

   Creare utenti con percorso = /home/users/community

   * Aggiungi membri ai seguenti gruppi:

      * Manager abilitazione community
      * Amministratori community

## Dispatcher {#dispatcher}

Se la distribuzione include [AEM Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html), affinché le funzioni di abilitazione funzionino correttamente, è necessario modificare le sezioni `clientheader` e `filter`. Vedere [Configurazione del dispatcher per Communities](dispatcher.md#enablement).
