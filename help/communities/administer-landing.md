---
title: Siti community
seo-title: Siti community
description: Panoramica della documentazione di AEM Communities
seo-description: Panoramica della documentazione di AEM Communities
uuid: 9842ce6c-1af8-4b27-b199-07410e797ab2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 8799386a-c3b8-43cf-9f71-580ff2a81abc
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Communities Sites {#communities-sites}

Questa sezione è destinata agli amministratori di AEM Communities e acquisisce familiarità con le funzioni di AEM Communities.

## Panoramica {#overview}

Per una panoramica ed esercitazioni introduttive, visitate:

* [Panoramica di AEM Communities](overview.md)
* [Guida introduttiva di AEM Communities](getting-started.md)
* [Guida introduttiva ad AEM Communities per l&#39;abilitazione](getting-started-enablement.md)

## Argomenti di amministrazione e configurazione {#administration-and-configuration-topics}

### Creazione e gestione di siti community {#communities-site-creation-and-management}

* Console [Community](consoles.md)

   * [Sites](sites-console.md)

      * [Gruppi (sub community)](groups.md)
   * [Moderazione](moderation.md)
   * [Gestione di membri e gruppi](members.md)
   * [Risorse di abilitazione](resources.md)
   * [Rapporti](reports.md)


* Strumenti [**](tools.md)Community:

   * [Modelli per siti](sites.md)
   * [Modelli per gruppi](tools-groups.md)
   * [Funzioni per community](functions.md)
   * [Configurazione dell’archiviazione](srp-config.md)
   * [Guida dei componenti](components-guide.md)
   * [Badge](badges.md)


### Contenuto generato dall&#39;utente {#user-generated-content}

Una delle caratteristiche principali di AEM Communities è la generazione di contenuti generati dagli utenti (UGC, user generated content) tramite visitatori del sito (membri). Per saperne di più sull’utilizzo di UGC visita:

* [Archivio](working-with-srp.md)UGC comune: scelta dell&#39;SRP per la memorizzazione condivisa dell&#39;UGC
* [Moderazione UGC](moderate-ugc.md): i membri attendibili possono moderare l&#39;UGC in massa o nel contesto
* [Assegnazione tag UGC](tag-ugc.md): possono essere configurate per consentire ai membri di assegnare tag al contenuto
* [Traduzione UGC](translate-ugc.md): le funzioni possono essere configurate per tradurre tutti gli UGC o consentire ai membri di tradurre i post selezionati
* [Configurazione](analytics.md)Analytics: abilitazione di Adobe Analytics per report su diverse metriche relative all&#39;attività dei membri

### Membri community {#community-members}

* [Gestione di utenti e gruppi](users.md)di utenti: i dettagli dei membri della comunità e dei gruppi di membri, compresi i membri privilegiati
* [Limiti](limits.md)contributi: possibilità di limitare l&#39;invio da parte di nuovi membri
* [Servizio](deploy-communities.md#tunnel-service-on-author)tunnel: consente l’accesso ai membri e ai gruppi di membri lato pubblicazione dall’ambiente di authoring
* [Console](members.md)Membri e Gruppi: consente ai membri e ai gruppi di membri lato pubblicazione di essere creati e gestiti dall’ambiente di authoring
* [Sincronizzazione](sync.md)utente: per la sincronizzazione di membri e gruppi di membri tra più istanze di pubblicazione
* [Login tramite social network con Facebook e Twitter](social-login.md): possibilità per i visitatori del sito di diventare membri della comunità utilizzando le proprie credenziali Facebook o Twitter
* [Punteggio e Badge](implementing-scoring.md): la possibilità di assegnare distintivi per identificare i ruoli di un membro e per consentire ai membri di ottenere distinzioni attraverso la loro partecipazione alla comunità
* [Notifiche](notifications.md): possibilità per i membri di essere informati dell&#39;attività che seguono
* [Iscrizioni](subscriptions.md): possibilità per i membri di interagire con la community utilizzando e-mail esterne
* [Messaggi](messaging.md): possibilità per i membri di interagire con la comunità utilizzando messaggi interni

### Funzioni di abilitazione {#enablement-features}

* [Configurazione di Enablement](enablement.md): informazioni necessarie per configurare correttamente le funzioni di abilitazione
* [Configurazione](analytics.md)Analytics: informazioni necessarie per abilitare le funzionalità di Adobe Analytics for Communities
* [Risorse](tag-resources.md)di abilitazione tag: necessari per creare cataloghi di abilitazione

### Distribuzione {#deployment}

La sezione di distribuzione contiene informazioni specifiche per AEM Communities.

La natura dell&#39;utilizzo dei contenuti della community influenza la struttura dell&#39;implementazione:

* [Topologie consigliate per community](topologies.md)

È importante installare la versione più recente di Communities sulla piattaforma AEM:

* [Pacchetto di funzioni per le ultime community](deploy-communities.md#latestfeaturepack)

Vedi la pagina di distribuzione per altre informazioni specifiche di Communities, ad esempio per [Aggiornamento](upgrade.md), [Dispatcher](dispatcher.md) e [Replica](deploy-communities.md#replication-agents-on-author).

## Documentazione di Community correlate {#related-communities-documentation}

* Per informazioni sulle distribuzioni consigliate, visitate [Implementazione delle community](deploy-communities.md) .

* Visitate [Developing Communities](communities.md) per informazioni sul framework dei componenti sociali (SCF) e sulla personalizzazione dei componenti e delle funzionalità di Communities.

* Per informazioni su come creare e configurare i componenti di Community, consulta [Authoring dei componenti](author-communities.md) di Communities.
