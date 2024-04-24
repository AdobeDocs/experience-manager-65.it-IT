---
title: Comunità in via di sviluppo
description: Crea e personalizza funzioni community come forum, gruppi di utenti e altro ancora.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 3ed3768a-1b3c-45a1-a34c-61694cd407d9
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 5%

---

# Comunità in via di sviluppo  {#developing-communities}

## Panoramica {#overview}

Le community Adobe Experience Manager (AEM) semplificano la creazione e la personalizzazione di funzioni quali forum, gruppi di utenti, blog, domande e risposte, calendari, commenti, recensioni, votazioni, valutazioni e assegnazioni. Queste funzioni consentono di immettere nell’ambiente di pubblicazione i contenuti generati dagli utenti (UGC, User-Generated Content).

La base di un [sito community](overview.md#communitiessites) è il [framework della componente social](scf.md) (SCF). La creazione di un sito community inizia con la selezione di un [modello per sito community](sites-console.md) composto da [funzioni community](functions.md).

Per una panoramica e tutorial introduttivi, visita:

* [Panoramica di AEM Communities](overview.md)
* [Guida introduttiva ad AEM Communities](getting-started.md)

>[!NOTE]
> 
>Si consiglia vivamente di essere sempre aggiornati con [ultime versioni](deploy-communities.md#latest-releases).

## Distribuzioni consigliate {#recommended-deployments}

* [Archiviazione contenuti community](working-with-srp.md): illustra le scelte del provider di risorse social network (SRP) disponibili per un archivio comune UGC
* [Topologie consigliate per le community](topologies.md): descrive le topologie in base al caso d’uso e alla scelta SRP

## Framework componenti social {#social-component-framework}

* [Framework componenti social](scf.md): panoramica del framework e delle API.
* [Helper Handlebars SCF](handlebars-helpers.md): helper predefiniti e come scrivere helper personalizzati.
* [Personalizzazione lato client](client-customize.md): personalizzazione del codice eseguito nel browser.
* [Personalizzazione lato server](server-customize.md): personalizzazione del codice in esecuzione sul server.
* [Provider risorsa di archiviazione (SRP)](srp.md): panoramica dell’archiviazione dei contenuti della community.
* [Linee guida per la codifica](code-guide.md): linee guida, suggerimenti.
* [Guida ai componenti della community](components-guide.md): strumento di sviluppo interattivo.

## Nozioni di base su componenti, funzioni e funzioni {#component-function-and-feature-essentials}

I componenti, le funzioni e le funzioni di AEM Communities forniscono i blocchi predefiniti per [siti community](sites-console.md).

* [Nozioni di base su componenti, funzioni e funzioni](essentials.md)
* [Clientlibs per i componenti Communities](clientlibs.md)
* [Funzioni community](functions.md)
* [Modelli per gruppi community](tools-groups.md)
* [Modelli per sito community](sites.md)

## Membri community {#community-members}

* [Gestione di utenti e gruppi di utenti](users.md)
* [Accesso social network con Facebook e Twitter](social-login.md)

## Gruppi community {#community-groups}

[Gruppi community](overview.md#communitygroups) si tratta del concetto di consentire ai membri della community di creare sottocomunità all’interno del sito community. La creazione di un gruppo community può verificarsi nell’ambiente di pubblicazione o di authoring.

* [Nozioni di base sul gruppo community](essentials-groups.md)
* [Funzione Gruppi](functions.md#groups-function)
* [Modelli per gruppi community](tools-groups.md)
* [Gestione di utenti e gruppi di utenti](users.md)
* [Gruppi community per autori](creating-groups.md)

## Gestione dei dati {#managing-data}

* [Nozioni di base su SRP e UGC](srp-and-ugc.md) - Metodi ed esempi di utilità API SRP
* [Nozioni di base sui tag](tag.md) - possibilità per i membri della community di assegnare tag alle risorse di abilitazione UGC e/o catalogate

## Tutorial {#tutorials}

* [Tutorial lato client](tutorials.md#client-side-customization)
* [Tutorial lato server](tutorials.md#server-side-customization)
* [Istruzioni pratiche](tutorials.md#how-to-instructions)

## Risoluzione dei problemi {#troubleshooting}

* [Risoluzione dei problemi](troubleshooting.md)
* [Problemi noti](/help/release-notes/release-notes.md)

## Documentazione delle community correlate {#related-communities-documentation}

* Visita [Distribuzione delle community](deploy-communities.md) per informazioni sulle distribuzioni consigliate e sulla configurazione di Dispatcher.

* Visita [Amministrazione di siti community](administer-landing.md) per informazioni sulla creazione di un sito community, sulla configurazione di modelli di sito community, sulla moderazione del contenuto della community, sulla gestione dei membri e sulla configurazione dei messaggi.

* Visita [Authoring dei componenti delle community](author-communities.md) per scoprire come effettuare l’authoring con e configurare i componenti di Communities.
