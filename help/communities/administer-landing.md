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
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 5%

---


# Siti community {#communities-sites}

Questa sezione è destinata a coloro che amministrano AEM Communities e acquisiscono familiarità con le funzioni di AEM Communities.

## Panoramica {#overview}

Per una panoramica e le esercitazioni introduttive, visita:

* [Panoramica di AEM Communities](overview.md)
* [Guida introduttiva di AEM Communities](getting-started.md)
* [Guida introduttiva ad AEM Communities per l&#39;abilitazione](getting-started-enablement.md)

## Argomenti di amministrazione e configurazione {#administration-and-configuration-topics}

### Creazione e gestione di siti di Communities {#communities-site-creation-and-management}

* Community [console](consoles.md)

   * [Sites](sites-console.md)

      * [Gruppi (sottocomunità)](groups.md)
   * [Moderazione](moderation.md)
   * [Gestione dei membri e dei gruppi](members.md)
   * [Risorse di abilitazione](resources.md)
   * [Rapporti](reports.md)


* Community [*strumenti*](tools.md):

   * [Modelli per siti](sites.md)
   * [Modelli per gruppi](tools-groups.md)
   * [Funzioni per community](functions.md)
   * [Configurazione dell’archiviazione](srp-config.md)
   * [Guida dei componenti](components-guide.md)
   * [Badge](badges.md)


### Contenuto generato dall&#39;utente {#user-generated-content}

Una caratteristica principale di AEM Communities è la generazione di contenuti generati dagli utenti (UGC) mediante l’accesso ai visitatori del sito (membri). Per ulteriori informazioni sull’utilizzo di UGC, visita:

* [Archivio](working-with-srp.md) UGC comune: scelta dell&#39;SRP per lo stoccaggio condiviso dell&#39;UGC
* [Moderazione UGC](moderate-ugc.md): i membri affidabili possono moderare UGC in massa o nel contesto
* [Assegnazione tag UGC](tag-ugc.md): le funzioni possono essere configurate per consentire ai membri di assegnare tag al contenuto
* [Traduzione di UGC](translate-ugc.md): le funzionalità possono essere configurate per tradurre tutti gli UGC o consentire ai membri di tradurre i post selezionati
* [Configurazione](analytics.md) di Analytics: che consente ad Adobe Analytics di generare rapporti su varie metriche relative all’attività dei membri

### Membri community {#community-members}

* [Gestione di utenti e gruppi](users.md) di utenti: i dettagli dei membri della comunità e dei gruppi di membri, compresi i membri privilegiati.
* [Limiti](limits.md) di contributo: capacità di limitare la pubblicazione da parte di nuovi membri.
* [Servizio](deploy-communities.md#tunnel-service-on-author) tunnel: consente di accedere ai membri e ai gruppi di membri lato pubblicazione dall’ambiente di authoring.
* [Console](members.md) Membri e gruppi: consente di creare e gestire membri e gruppi di membri lato pubblicazione dall’ambiente di authoring.
* [Sincronizzazione](sync.md) utente: per la sincronizzazione di membri e gruppi di membri in più istanze di pubblicazione.
* [Accesso social con Facebook e Twitter](social-login.md): possibilità per i visitatori del sito di diventare membri della community utilizzando le proprie credenziali Facebook o Twitter.
* [Punteggio e badge](implementing-scoring.md): la possibilità di assegnare distintivi per identificare i ruoli di un membro e di ottenere distintivi attraverso la loro partecipazione alla comunità.
* [Notifiche](notifications.md): la possibilità per i membri di essere informati dell&#39;attività che seguono.
* [Abbonamenti](subscriptions.md): possibilità per i membri di interagire con la community utilizzando e-mail esterne.
* [Messaggistica](messaging.md): capacità dei membri di interagire con la comunità utilizzando messaggi interni.

### Funzioni di abilitazione {#enablement-features}

* [Configurazione di Enablement](enablement.md): informazioni necessarie per configurare correttamente le funzioni di abilitazione.
* [Configurazione](analytics.md) di Analytics: informazioni necessarie per abilitare le funzionalità di Adobe Analytics for Communities.
* [Risorse](tag-resources.md) di abilitazione assegnazione tag: necessari per creare cataloghi di abilitazione.

### Implementazione {#deployment}

La sezione Distribuzione contiene informazioni specifiche di AEM Communities.

La natura dell&#39;utilizzo dei contenuti della community influenza la struttura dell&#39;implementazione:

* [Topologie consigliate per community](topologies.md)

È importante installare la versione più recente di Communities sulla piattaforma AEM:

* [Feature Pack per le community più recenti](deploy-communities.md#latestfeaturepack)

Consulta la pagina di distribuzione per altre informazioni specifiche di Communities, ad esempio per [Aggiornamento](upgrade.md), [Dispatcher](dispatcher.md) e [Replica](deploy-communities.md#replication-agents-on-author).

## Documentazione relativa a Communities {#related-communities-documentation}

* Per informazioni sulle distribuzioni consigliate, visita [Implementazione di Communities](deploy-communities.md) .

* Visita [Sviluppo di community](communities.md) per informazioni sul framework dei componenti social (SCF) e sulla personalizzazione dei componenti e delle funzionalità di Communities.

* Per informazioni su come eseguire l’authoring con e configurare i componenti di Communities, visita [Authoring Communities Components](author-communities.md) .
