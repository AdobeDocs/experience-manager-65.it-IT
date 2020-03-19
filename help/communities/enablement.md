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
source-git-commit: d6c8bbb9aa763a2eb6660b6b6755aba75241e394

---


# Configurazione delle funzioni di abilitazione {#configuring-enablement-features}

## Panoramica {#overview}

Le funzioni di abilitazione consentono di creare comunità di [abilitazione](overview.md#enablement-community).

* Questa funzione richiede licenze aggiuntive per l&#39;utilizzo in un ambiente di produzione.

L&#39;utilizzo delle funzioni di abilitazione richiede quanto segue:

Installazione di:

* **SCORM** Sharable Content Object Reference Model (SCORM) è una raccolta di standard e specifiche per l&#39;e-learning. SCORM definisce anche come il contenuto può essere incluso in un file ZIP trasferibile.

* **MySQL** MySQL è un database relazionale utilizzato principalmente per il tracciamento SCORM e i dati di reporting per l&#39;abilitazione, nonché tabelle per il monitoraggio dell&#39;avanzamento video. Il pacchetto di funzioni SCORM per l&#39;abilitazione richiede il driver JDBC MySQL.

* **FFmpeg** FFmpeg è una soluzione per la conversione e lo streaming audio e video e, se installato, viene utilizzato per la corretta transcodifica di risorse [](../../help/sites-authoring/default-components-foundation.md#video)video. Per le comunità di abilitazione, viene utilizzata nell’ambiente di authoring per ottenere i metadati per le risorse caricate e generare una miniatura da visualizzare quando si elenca le risorse.

Configurazione di:

* **Manager** community Per le comunità di abilitazione, solo ai membri del gruppo di `Community Enablement Managers` utenti può essere assegnato il ruolo di `Community Site Enablement Manager`, le cui autorizzazioni possono includere la creazione di contenuto, le assegnazioni e la gestione di membri nell&#39;ambiente di pubblicazione.

Configurazione opzionale di:

* **L&#39;integrazione di Adobe Analytics** con Adobe Analytics aggiunge funzionalità di reporting complete e supporta l&#39;aggiunta di heartbeat video ad Analytics.

* **Dispatcher**

## Passaggi di configurazione {#configuration-steps}

Di seguito sono riportati i passaggi necessari per abilitare le community.

Ogni passaggio fa riferimento alla documentazione che fornisce i dettagli necessari.

**Per tutte le istanze di creazione/pubblicazione:**

1. **[Installare il driver JDBC per MySQL](deploy-communities.md#jdbc-driver-for-mysql)**Use Web Console (bundle):*http://localhost:4502/system/console/bundles*Installare *prima*di installare il pacchetto SCORM

1. **[Installare il pacchetto](deploy-communities.md#scorm-package)**SCORM Utilizzare Package Manager:*http://localhost:4502/crx/packmgr/*

**Su qualsiasi server:**

1. **[Installazione di MySQL, MySQL Workbench](mysql.md)**

1. **[Installazione database](mysql.md#database-setup)**MySQL Esecuzione di script SQL scaricati dall&#39;istanza di creazioneUtilizzo di MySQL Workbench

**Sulla stessa istanza di creazione del server host:**

1. **[Installare FFmpeg](ffmpeg.md)**

**Per tutte le istanze di creazione/pubblicazione:**

1. **[Configura pool](mysql.md#configure-jdbc-connections)**connessioni JDBC Usa console Web (configMgr):*http://localhost:4502/system/console/configMgr*

1. **[Configurare il servizio](mysql.md#aem-communities-scormengine-service)**motore SCORM Utilizzare la console Web (configMgr):*http://localhost:4502/system/console/configMgr*

1. **[Configurare i filtri](mysql.md#adobe-granite-csrf-filter)**CSRF Utilizzo della console Web (configMgr):*http://localhost:4502/system/console/configMgr*

**Nell’istanza di creazione:**

1. (*Facoltativo*) **[Configurare la console Strumenti di](analytics.md)**utilizzo del servizioAnalytics, Distribuzione, Servizi cloud:*http://localhost:4502/etc/cloudservices/sitecatalyst.html*

1. **[Configurare la console Flusso di lavoro/Modelli](ffmpeg.md#configure-ffmpeg-transcoding-service)**di FFmpeg

1. **[Abilita Tunnel Service](deploy-communities.md#tunnel-service-on-author)**Use Web Console (configMgr):*http://localhost:4502/system/console/configMgr*

1. **[Creazione di amministratori](users.md#creating-community-members)**community Per l’ambiente di authoring, utilizzare la console di protezione classica:*http://localhost:4502/useradmin*creare utenti con percorso = /home/users/community

   * Aggiungi membri ai seguenti gruppi:

      * Manager abilitazione community
      * Amministratori community

## Dispatcher {#dispatcher}

Quando la distribuzione include il dispatcher di [AEM](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html), affinché le funzioni di abilitazione funzionino correttamente, le `clientheader` sezioni e `filter` le sezioni devono essere modificate. Consultate [Configurazione del dispatcher per Communities](dispatcher.md#enablement).
