---
title: Sviluppo di community
seo-title: Sviluppo di community
description: Creazione e personalizzazione di funzioni per community quali forum, gruppi di utenti e altro
seo-description: Creazione e personalizzazione di funzioni per community quali forum, gruppi di utenti e altro
uuid: 51dc54da-9090-4d36-adf9-72d5479062a5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: fbfe8097-3c3f-4a05-97ad-1ce526362a26
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 6%

---


# Sviluppo di community {#developing-communities}

## Panoramica {#overview}

 AEM Communities semplifica la creazione e la personalizzazione di funzionalità della community quali forum, gruppi di utenti, blog, D e R, calendari, commenti, revisioni, voti, valutazioni e assegnazioni. Queste funzioni consentono di inserire nell’ambiente di pubblicazione il contenuto generato dall’utente (UGC).

La base di un [sito community](overview.md#communitiessites) è il [social component framework](scf.md) (SCF). La creazione di un sito community inizia con la selezione di un [modello di sito community](sites-console.md) composto da [funzioni community](functions.md).

Per una panoramica ed esercitazioni introduttive, visitate:

* [ Panoramica di AEM Communities](overview.md)
* [Guida introduttiva di AEM Communities](getting-started.md)
* [Guida introduttiva  AEM Communities per l’abilitazione](getting-started-enablement.md)

>[!NOTE]
> 
>Si consiglia vivamente di essere aggiornati sulle [ultime versioni](deploy-communities.md#latest-releases).

## Implementazioni consigliate {#recommended-deployments}

* [Archiviazione](working-with-srp.md) contenuto community: illustra le opzioni SRP disponibili per uno store comune UGC
* [Topologie consigliate per community](topologies.md): illustra le topologie in base al caso di utilizzo e alla scelta SRP

## Framework componente sociale {#social-component-framework}

* [Quadro](scf.md) dei componenti sociali: panoramica del framework e delle API.
* [Helper](handlebars-helpers.md) manubrio SCF: helper predefiniti e come scrivere gli helper personalizzati.
* [Personalizzazione](client-customize.md) lato client: personalizzazione del codice in esecuzione nel browser.
* [Personalizzazione](server-customize.md) lato server: personalizzazione del codice in esecuzione sul server.
* [Provider di risorse di storage (SRP)](srp.md): panoramica dello storage dei contenuti della community.
* [Linee guida](code-guide.md) sulla codifica: linee guida, suggerimenti e trucchi.
* [Guida](components-guide.md) ai componenti community: strumento di sviluppo interattivo.

## Componenti, funzioni e funzioni essenziali {#component-function-and-feature-essentials}

 componenti, funzioni e funzionalità di AEM Communities costituiscono gli elementi di base per [siti della community](sites-console.md).

* [Componenti, funzioni e funzioni di base](essentials.md)
* [Clientlibs per componenti Community](clientlibs.md)
* [Funzioni per community](functions.md)
* [Modelli per gruppi community](tools-groups.md)
* [Modelli per sito community](sites.md)

## Membri community {#community-members}

* [Gestione di utenti e gruppi di utenti](users.md)
* [Login tramite social network con Facebook e Twitter](social-login.md)

## Gruppi community {#community-groups}

[I ](overview.md#communitygroups) raggruppamenti comunitari prevedono la possibilità di consentire ai membri della comunità di formare delle sub-comunità all&#39;interno del sito comunitario. La creazione di un gruppo di community può avvenire nell’ambiente di pubblicazione o di authoring.

* [Community Group Essentials](essentials-groups.md)
* [Funzione Groups](functions.md#groups-function)
* [Modelli per gruppi community](tools-groups.md)
* [Gestione di utenti e gruppi di utenti](users.md)
* [Gruppi community per gli autori](creating-groups.md)

## Gestione dei dati {#managing-data}

* [Funzioni di base SRP e UGC](srp-and-ugc.md)  - Metodi e esempi di utilità API SRP
* [Tag Essentials](tag.md) : possibilità per i membri della community di assegnare tag UGC e/o risorse di abilitazione catalogate

## Esercitazioni {#tutorials}

* [Esercitazioni lato client](tutorials.md#client-side-customization)
* [Esercitazioni lato server](tutorials.md#server-side-customization)
* [Istruzioni pratiche](tutorials.md#how-to-instructions)

## Risoluzione dei problemi {#troubleshooting}

* [Risoluzione dei problemi](troubleshooting.md)
* [Problemi noti](/help/release-notes/known-issues.md)

## Documentazione sulle community correlate {#related-communities-documentation}

* Per informazioni sulle distribuzioni consigliate e sulla configurazione del dispatcher, visitare [Implementazione di Communities](deploy-communities.md).

* Per informazioni su come creare un sito community, configurare modelli di sito community, moderare i contenuti della community, gestire i membri e configurare i messaggi, visitate [Amministrazione siti community](administer-landing.md).

* Per informazioni su come creare e configurare i componenti di Communities, visita [Componenti di authoring](author-communities.md).

