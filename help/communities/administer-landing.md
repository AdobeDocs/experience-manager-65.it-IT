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

* Community [console](consoles.md)

   * [Sites](sites-console.md)

      * [Gruppi (sottocomunità)](groups.md)

   * [Moderazione](moderation.md)
   * [Gestione di membri e gruppi](members.md)
   * [Rapporti](reports.md)

* Community [*strumenti*](tools.md):

   * [Modelli per siti](sites.md)
   * [Modelli per gruppi](tools-groups.md)
   * [Funzioni community](functions.md)
   * [Configurazione di archiviazione](srp-config.md)
   * [Guida dei componenti](components-guide.md)
   * [Badge](badges.md)


### Contenuto generato dall&#39;utente {#user-generated-content}

Una funzione importante di AEM Communities è la generazione di contenuti generati dagli utenti (UGC, User Generated Content) da parte dei visitatori del sito (membri) che hanno effettuato l’accesso. Per ulteriori informazioni sull’utilizzo di UGC, visita:

* [Archivio UGC comune](working-with-srp.md): scelta di SRP per lo storage condiviso di UGC
* [Moderazione UGC](moderate-ugc.md): i membri attendibili possono moderare UGC in blocco o nel contesto
* [Assegnazione tag UGC](tag-ugc.md): le funzionalità possono essere configurate per consentire ai membri di assegnare tag al contenuto
* [Traduzione UGC](translate-ugc.md): le funzioni possono essere configurate per tradurre tutti i contenuti generati dagli utenti (UGC) o consentire ai membri di tradurre i post selezionati
* [Configurazione analisi](analytics.md): consentendo ad Adobe Analytics di generare rapporti su varie metriche relative all’attività dei membri

### Membri community {#community-members}

* [Gestione di utenti e gruppi di utenti](users.md): dettagli dei membri della community e dei gruppi di membri, inclusi i membri con privilegi.
* [Limiti contributi](limits.md): possibilità di vincolare la pubblicazione da parte di nuovi membri.
* [Servizio tunnel](deploy-communities.md#tunnel-service-on-author): consente di accedere ai membri lato pubblicazione e ai gruppi di membri dall’ambiente di authoring.
* [Console membri e gruppi](members.md): consente la creazione e la gestione di membri lato pubblicazione e gruppi di membri dall’ambiente di authoring.
* [Sincronizzazione utente](sync.md): per sincronizzare membri e gruppi di membri tra più istanze di pubblicazione.
* [Accesso social network con Facebook e Twitter](social-login.md): possibilità per i visitatori del sito di diventare membri della community utilizzando le credenziali Facebook o di Twitter.
* [Punteggio e distintivi](implementing-scoring.md): possibilità di assegnare i distintivi per identificare i ruoli di un membro e di assegnare i distintivi ai membri tramite la loro partecipazione alla community.
* [Notifiche](notifications.md): possibilità per i membri di essere informati delle attività che seguono.
* [Iscrizioni](subscriptions.md): possibilità per i membri di interagire con la community tramite e-mail esterna.
* [Messaggistica](messaging.md): possibilità per i membri di interagire con la community utilizzando messaggi interni.

### Distribuzione {#deployment}

La sezione distribuzione contiene informazioni specifiche di AEM Communities.

La natura dell’utilizzo dei contenuti della community influenza la struttura della distribuzione:

* [Topologie consigliate per le community](topologies.md)

È importante installare l’ultima versione di Communities sulla piattaforma AEM:

* [Pacchetto di funzioni per community più recenti](deploy-communities.md#latestfeaturepack)

Consulta la pagina della distribuzione per altre informazioni specifiche per la community, ad esempio per [Aggiornamento](upgrade.md), [Dispatcher](dispatcher.md), e [Replica](deploy-communities.md#replication-agents-on-author).

## Documentazione delle community correlate {#related-communities-documentation}

* Visita [Distribuzione delle community](deploy-communities.md) dove puoi scoprire le distribuzioni consigliate.

* Visita [Comunità in via di sviluppo](communities.md) dove puoi scoprire il framework dei componenti social (SCF) e personalizzare i componenti e le funzioni di Communities.

* Visita [Authoring dei componenti delle community](author-communities.md) dove puoi scoprire come effettuare l’authoring con e configurare i componenti di Communities.
