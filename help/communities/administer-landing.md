---
title: Siti community
description: Scopri le nozioni di base delle community Adobe Experience Manager (AEM) per amministratori che hanno già familiarità con le sue funzioni di base.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: e3ffc73e-2bc5-492d-b64b-750cc7d8ab9b
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 4%

---

# Siti community {#communities-sites}

Questa sezione è destinata agli amministratori di AEM Communities e presuppone la conoscenza delle funzioni di AEM Communities.

## Panoramica {#overview}

Per una panoramica e tutorial introduttivi, visita:

* [Panoramica di AEM Communities](overview.md)
* [Guida introduttiva ad AEM Communities](getting-started.md)

## Argomenti relativi all&#39;amministrazione e alla configurazione {#administration-and-configuration-topics}

### Creazione e gestione di siti community {#communities-site-creation-and-management}

* [console](consoles.md) community

   * [Sites](sites-console.md)

      * [Gruppi (sottocomunità)](groups.md)

   * [Moderazione](moderation.md)
   * [Gestione di membri e gruppi](members.md)
   * [Rapporti](reports.md)

* [*strumenti*](tools.md) per community:

   * [Modelli per siti](sites.md)
   * [Modelli per gruppi](tools-groups.md)
   * [Funzioni community](functions.md)
   * [Configurazione di archiviazione](srp-config.md)
   * [Guida dei componenti](components-guide.md)
   * [Badge](badges.md)


### Contenuto generato dall&#39;utente {#user-generated-content}

Una funzione importante di AEM Communities è la generazione di contenuti generati dagli utenti (UGC, User Generated Content) da parte dei visitatori del sito (membri) che hanno effettuato l’accesso. Per ulteriori informazioni sull’utilizzo di UGC, visita:

* [Archivio UGC comune](working-with-srp.md): scelta dell&#39;SRP per l&#39;archiviazione condivisa di UGC
* [Moderazione UGC](moderate-ugc.md): i membri attendibili possono moderare UGC in blocco o nel contesto
* [Assegnazione tag UGC](tag-ugc.md): le funzionalità possono essere configurate per consentire ai membri di assegnare tag al contenuto
* [Traduzione UGC](translate-ugc.md): le funzionalità possono essere configurate per tradurre tutti i UGC o consentire ai membri di tradurre i post selezionati
* [Configurazione di Analytics](analytics.md): abilitazione di Adobe Analytics per creare rapporti su varie metriche relative all&#39;attività dei membri

### Membri community {#community-members}

* [Gestione di utenti e gruppi di utenti](users.md): dettagli dei membri della community e dei gruppi di membri, inclusi i membri con privilegi.
* [Limiti contributi](limits.md): possibilità di vincolare la pubblicazione da parte di nuovi membri.
* [Servizio tunnel](deploy-communities.md#tunnel-service-on-author): consente l&#39;accesso ai membri e ai gruppi membri lato pubblicazione dall&#39;ambiente di authoring.
* [Console membri e gruppi](members.md): consente la creazione e la gestione di membri e gruppi lato pubblicazione dall&#39;ambiente di authoring.
* [Sincronizzazione utente](sync.md): per sincronizzare membri e gruppi di membri in più istanze di pubblicazione.
* [Accesso social network tramite Facebook e Twitter](social-login.md): possibilità per i visitatori del sito di diventare membri della community utilizzando le credenziali Facebook o di Twitter.
* [Punteggio e distintivi](implementing-scoring.md): possibilità per i distintivi di essere assegnati per identificare i ruoli di un membro e per i membri di guadagnare distintivi tramite la loro partecipazione alla community.
* [Notifiche](notifications.md): possibilità per i membri di ricevere una notifica dell&#39;attività che seguono.
* [Iscrizioni](subscriptions.md): possibilità per i membri di interagire con la community tramite e-mail esterna.
* [Messaggistica](messaging.md): possibilità per i membri di interagire con la community utilizzando messaggi interni.

### Distribuzione {#deployment}

La sezione distribuzione contiene informazioni specifiche di AEM Communities.

La natura dell’utilizzo dei contenuti della community influenza la struttura della distribuzione:

* [Topologie consigliate per le community](topologies.md)

È importante installare l’ultima versione di Communities sulla piattaforma AEM:

* [Pacchetto di funzioni per community più recenti](deploy-communities.md#latestfeaturepack)

Consulta la pagina della distribuzione per altre informazioni specifiche della community, ad esempio [Aggiornamento](upgrade.md), [Dispatcher](dispatcher.md) e [Replica](deploy-communities.md#replication-agents-on-author).

## Documentazione delle community correlate {#related-communities-documentation}

* Visita [Distribuzione di Communities](deploy-communities.md) per scoprire le distribuzioni consigliate.

* Visita [Sviluppo di community](communities.md) per scoprire il framework dei componenti social network (SCF) e personalizzare i componenti e le funzionalità di Communities.

* Visita [Authoring dei componenti delle community](author-communities.md) per scoprire come creare e configurare i componenti delle community.
