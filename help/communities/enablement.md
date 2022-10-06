---
title: Configurazione delle funzionalità di abilitazione
seo-title: Configuring Enablement Features
description: Configurare le funzioni di abilitazione in Communities
seo-description: Configure enablement features in Communities
uuid: 27be3128-1a7d-412e-99a9-6e3b3b0aec1c
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 765a3d9b-4552-403e-872c-fdf684ac271d
role: Admin
exl-id: b635e2ed-4637-4b2f-a746-ec8dc7541bab
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 1%

---

# Configurazione delle funzionalità di abilitazione {#configuring-enablement-features}

## Panoramica {#overview}

Le funzioni di abilitazione consentono di creare [comunità di abilitazione](overview.md#enablement-community).

* Questa funzione richiede licenze aggiuntive per l’utilizzo in un ambiente di produzione.

L’utilizzo delle funzioni di abilitazione richiede quanto segue:

Installazione di:

* **SCORM**

   SCORM (Sharable Content Object Reference Model) è una raccolta di standard e specifiche per l&#39;e-learning. SCORM definisce anche come il contenuto può essere confezionato in un file ZIP trasferibile.

* **MySQL**

   MySQL è un database relazionale utilizzato principalmente per il tracciamento SCORM e i dati di reporting per l&#39;abilitazione, nonché tabelle per il tracciamento dell&#39;avanzamento video. Il feature pack SCORM per l&#39;abilitazione richiede il driver JDBC MySQL.

* **FFmpeg**

   FFmpeg è una soluzione per la conversione e lo streaming audio e video e, quando installato, viene utilizzato per la corretta transcodifica di [Risorse video](../../help/sites-authoring/default-components-foundation.md#video). Per le community di abilitazione, viene utilizzato nell’ambiente di authoring per ottenere i metadati per le risorse caricate e generare una miniatura da visualizzare durante l’elenco della risorsa.

Configurazione di:

* **Manager community**

   Per le comunità di abilitazione, solo i membri del `Community Enablement Managers` al gruppo di utenti può essere assegnato il ruolo di `Community Site Enablement Manager`, le cui autorizzazioni possono includere la creazione di contenuti, le assegnazioni e la gestione dei membri nell’ambiente di pubblicazione.

Configurazione opzionale di:

* **Adobe Analytics**

   L’integrazione con Adobe Analytics aggiunge funzioni di reporting complete e supporta l’aggiunta di Video Heartbeat ad Analytics.

* **Dispatcher**

## Passaggi di configurazione {#configuration-steps}

Di seguito sono riportati i passaggi necessari per abilitare le comunità.

Ogni passaggio è collegato alla documentazione che fornisce i dettagli necessari.

**Su tutte le istanze di authoring/pubblicazione:**

1. **[Installare il driver JDBC per MySQL](deploy-communities.md#jdbc-driver-for-mysql)**

   Utilizzare la console Web (bundle): *http://localhost:4502/system/console/bundles*

   Installa *prima* installazione del pacchetto SCORM

1. **[Installa il pacchetto SCORM](deploy-communities.md#scorm-package)**


   Utilizza Gestione pacchetti: *http://localhost:4502/crx/packmgr/*

**Su qualsiasi server:**

1. **[Installazione di MySQL, Workbench MySQL](mysql.md)**

1. **[Installare i database MySQL](mysql.md#database-setup)**

   Esegui script SQL scaricati dall&#39;istanza autore

   Utilizzare Workbench MySQL

**Nella stessa istanza di authoring del server di hosting:**

1. **[Installa FFmpeg](ffmpeg.md)**

**Su tutte le istanze di authoring/pubblicazione:**

1. **[Configurare il pool di connessioni JDBC](mysql.md#configure-jdbc-connections)**

   Utilizzare la console Web (configMgr): *http://localhost:4502/system/console/configMgr*

1. **[Configura il servizio del motore SCORM](mysql.md#aem-communities-scormengine-service)**

   Utilizzare la console Web (configMgr): *http://localhost:4502/system/console/configMgr*

1. **[Configurare i filtri CSRF](mysql.md#adobe-granite-csrf-filter)**

   Utilizzare la console Web (configMgr): *http://localhost:4502/system/console/configMgr*

**Nell’istanza dell’autore:**

1. (*Facoltativo*) **[Configurare il servizio Analytics](analytics.md)**

   Usa la console Strumenti, Implementazione, Cloud Services: *http://localhost:4502/etc/cloudservices/sitecatalyst.html*

1. **[Configura FFmpeg](ffmpeg.md#configure-ffmpeg-transcoding-service)**

   Usa console Flusso di lavoro/Modelli

1. **[Attiva servizio tunnel](deploy-communities.md#tunnel-service-on-author)**

   Utilizzare la console Web (configMgr): *http://localhost:4502/system/console/configMgr*

1. **[Creare amministratori della community](users.md#creating-community-members)**

   Per l’ambiente di authoring utilizza la console di sicurezza classica-interfaccia utente: *http://localhost:4502/useradmin*

   Crea utenti con percorso = /home/users/community

   * Aggiungi membri ai gruppi seguenti:

      * Responsabili dell&#39;abilitazione della community
      * Amministratori community

## Dispatcher {#dispatcher}

Quando la distribuzione include [Dispatcher AEM](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html), affinché le funzioni di abilitazione funzionino correttamente, il `clientheader` e `filter` le sezioni devono essere modificate. Vedi [Configurazione di Dispatcher per Communities](dispatcher.md#enablement).
