---
title: Panoramica di AEM Communities
seo-title: AEM Communities Overview
description: Panoramica delle funzioni e della configurazione di AEM Communities
seo-description: An overview of AEM Communities features and setup
uuid: 14405847-36ae-4958-bdc6-d799ecd05f06
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 44374006-f711-4af8-a1fe-f89164f79581
docset: aem65
exl-id: d6243dff-a067-455c-a326-5f451f225efd
source-git-commit: 9f9f80eb4cb74b687c7fadd41d0f8ea4ee967865
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 1%

---

# Panoramica di AEM Communities {#aem-communities-overview}

Adobe Experience Manager (AEM) Communities consente di creare rapidamente un sito di community on-premise con prestazioni migliorate, una migliore gestione del sito e la possibilità di convertire i visitatori del sito in membri di valore della community.

## Funzioni di Communities {#communities-features}

AEM Communities consente lo sviluppo di una relazione con i visitatori del sito, che:

* **Informazioni** tramite blog, domande e risposte e calendari di eventi,
* Quando **acquisire informazioni** attraverso forum, commenti e altri contenuti della community, spesso denominati contenuti generati dagli utenti (UGC).
* Permette **moderazione** da membri affidabili nell’ambiente di pubblicazione,
* **Accesso social** con Twitter e Facebook,
* **Traduzione in linea** del contenuto comunitario,
* **Creazione di gruppi comunitari** dal sito della comunità pubblicato,
* **Punteggio** assegnare i distintivi,
* **Condivisione file**,
* **Notifiche** e **flussi di attività**,
* Permette **assegnazione tag** (@menzione) altri membri registrati in Contenuto generato dagli utenti, per attirare la loro attenzione.

Le funzioni di Communities possono essere dimostrate utilizzando [AEM Demo](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki) disponibile pubblicamente su GitHub.com o con la nuova implementazione di riferimento We.Retail.

## Siti community {#community-sites}

Un sito community è un sito AEM creato utilizzando una semplice procedura guidata che consente di creare un sito web con numerose funzioni comuni precollegate al sito.

La [creazione guidata sito](/help/communities/sites-console.md):

* Assembla le caratteristiche del sito, in base alla [modello di sito community](/help/communities/sites.md) che è:

   * costruito da [funzioni della community](#community-functions)
   * facoltativo [gruppi comunitari](#communitygroups) caratteristica

* Utilizza le impostazioni per configurare:

   * moderazione
   * login
   * traduzione

* Fornisce funzioni essenziali:

   * Design dinamico: utilizza [Temi di Bootstrap twitter](https://getbootstrap.com)

   * Accesso : autoregistrazione, [accesso social](/help/communities/social-login.md), profili utente

      * Notifiche: i membri visualizzano eventi rilevanti per loro e contenuti generati dagli utenti laddove [@mention](/help/communities/overview.md#mentionssupport).

      * Messaggi: i membri possono inviare o ricevere messaggi all&#39;interno del sito della community.
      * Ricerca: possibilità di effettuare ricerche all&#39;interno del sito community.
      * Passaggio alla lingua: possibilità di selezionare una lingua per un [sito multilingue](/help/sites-administering/translation.md).

      * Amministrazione: accesso per i membri autorizzati a moderare e gestire gli utenti all&#39;interno del sito community.

* Elimina molti passaggi di authoring a livello di pagina:

   * Branding: caricamento facoltativo di un&#39;immagine banner per la visualizzazione su tutte le pagine del sito community
   * Menu di navigazione: i collegamenti di navigazione sono forniti per le funzioni incluse nel modello di sito community.

Per scoprire la facilità di creazione rapida di un nuovo sito community, visita [Guida introduttiva ad AEM Communities](/help/communities/getting-started.md).

## Persistenza dei contenuti della community {#community-content-persistence}

Per migliorare le prestazioni e la sincronizzazione dei contenuti della community, AEM Communities richiede un archivio comune specifico per i contenuti generati dagli utenti (UGC) condivisi tra tutte le istanze di AEM (authoring e pubblicazione).

Il contenuto della community è facilmente accessibile tramite l’SRP (Storage Resource Provider), che fornisce un livello per separare l’accesso dalla topologia sottostante e supporta un archivio comune per UGC.

Per ulteriori informazioni sulla persistenza dei contenuti della community e sulle distribuzioni consigliate, consulta:

* [Archiviazione dei contenuti della community](/help/communities/working-with-srp.md), che illustra le opzioni di storage SRP disponibili per UGC.
* [Topologie consigliate](/help/communities/topologies.md), che esamina le topologie in base al caso d’uso e alla scelta dell’SRP.
* [Aggiornamento a AEM 6.5 Communities](/help/communities/upgrade.md), che fornisce informazioni utili relative agli UGC quando si passa a AEM 6.5.

## Console di Communities {#communities-consoles}

Nell’ambiente di authoring, la console di navigazione globale consente di accedere alle [Console di Communities](/help/communities/consoles.md), che contiene:

* [Sites](/help/communities/sites-console.md) console

   * Creazione di siti
   * Modifica del sito
   * Gestione del sito
   * [Gruppi community](/help/communities/groups.md) console

* [Moderazione](/help/communities/moderation.md) console

   * Interfaccia utente comune per la moderazione in massa per gli ambienti di authoring e pubblicazione.
   * Nuovi criteri di filtro.

* [Membri e gruppi](/help/communities/members.md) console di gestione

   * Consente di creare e gestire utenti (membri) lato pubblicazione dall’ambiente di authoring.
   * Consente di vietare i membri.
   * Consente di creare e gestire gruppi di utenti lato pubblicazione (gruppi di membri) dall’ambiente di authoring.

* [Rapporti](/help/communities/reports.md) console

   * Consente di generare rapporti su assegnazioni, post e viste.

La console strumenti globali consente di accedere ai seguenti strumenti di Communities:

* [Modelli di sito](/help/communities/tools.md#sitetemplatesconsole) console

   * Creare e gestire modelli di sito community.

* [Modelli per gruppi](/help/communities/tools.md#grouptemplatesconsole) console

   * Creare e gestire modelli di gruppi di community.

* [Funzioni della community](/help/communities/tools.md#communityfunctionsconsole) console

   * Crea e gestisci funzioni della community.

* [Configurazione dell&#39;archiviazione](/help/communities/tools.md#storageconfiguratonconsole) console

   * Seleziona e configura il [negozio comune](/help/communities/working-with-srp.md) per il sito.

* [Guida dei componenti](/help/communities/components-guide.md)

   * un sito campione, [Componenti della community](https://localhost:4502/editor.html/content/community-components/en.html), che fornisce un esempio di tutti i componenti di Communities con la loro configurazione predefinita e la possibilità di sperimentare con essi.

## Modelli per sito community {#community-site-templates}

La creazione di siti community si basa sulla selezione di un modello di sito community per configurare rapidamente un sito community indipendente da qualsiasi sito di esempio.

Un modello di sito community, composto da funzioni community e modelli di gruppo community, fornisce la struttura di un sito community che include login, profili utente, messaggistica, menu del sito, ricerca, temi e funzioni di branding.

Consulta la sezione [Console Modelli per siti](/help/communities/sites.md).

## Funzioni community {#community-functions}

Le funzioni previste per un’esperienza comunitaria sono ben note. Con AEM Communities, queste funzioni sono disponibili come blocchi predefiniti, noti come funzioni per community.

Le funzioni della community sono normali pagine AEM includono componenti collegati tra loro in una funzione facilmente incorporata in un modello di sito della community.

Consulta la sezione [Console Funzioni community](/help/communities/functions.md).

## Gruppi e modelli di gruppi della community {#community-groups-and-group-templates}

La funzione gruppi community consente a una sottocommunity di creare in modo dinamico all’interno di un sito community da parte di utenti autorizzati e membri della community sia dagli ambienti di authoring che di pubblicazione.

Dall’ambiente di authoring, i gruppi di community (sub-community) possono essere creati all’interno di un sito community esistente o nidificati all’interno di un gruppo esistente, quando la struttura del modello contiene il [Funzione Groups](/help/communities/functions.md#groups-function).

La creazione di un gruppo community richiede la selezione di un modello di gruppo community che fornisce la progettazione delle pagine del gruppo community. Quando una funzione Groups viene aggiunta a una struttura di modelli, viene configurata per specificare un modello di gruppo o per fornire una scelta di modelli al momento della creazione di un nuovo gruppo community.

Consulta anche:

* [Console dei gruppi del sito](/help/communities/groups.md) per creare sottocommunity nell’ambiente di authoring.
* [Console Modelli di gruppo](/help/communities/tools-groups.md) per la creazione della struttura del sito per i gruppi.
* [Guida introduttiva ad AEM Communities](/help/communities/getting-started.md) per un tutorial per creare rapidamente un sito community con gruppi nidificati.

## Componenti della community {#community-components}

La [componenti della community](/help/communities/author-communities.md) può essere utilizzato per aggiungere funzionalità di Communities a qualsiasi sito AEM.

La [guida ai componenti della community](/help/communities/components-guide.md) è disponibile per l’esplorazione interattiva dei componenti.

## Community di coinvolgimento {#engagement-community}

Una community di coinvolgimento è un sito della community incentrato sul coinvolgimento dei clienti per informare, richiedere un feedback e consentire ai clienti di interagire come membri della community.

Le caratteristiche di una community di coinvolgimento possono includere:

* Accesso
* Messaggi
* Forum
* Commenti
* Recensioni
* Valutazioni
* Votazione
* Blog
* Gruppi
* Calendari
* Traduzione
* Moderazione
* Notifiche
* Punteggio e badge
* Reporting di Analytics

Per scoprire la facilità di creare rapidamente una nuova community di coinvolgimento, visita [Guida introduttiva ad AEM Communities](/help/communities/getting-started.md).

## AEM Demo {#aem-demo-machine}

La [AEM Demo](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) gestisce ed esegue demo per AEM [Sites](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites), [Risorse](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets), [Community](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities), [App](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps) e [Forms](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms), che spesso richiede una configurazione maggiore rispetto al semplice avvio di un&#39;istanza QuickStart. Il AEM Demo Machine configurerà ulteriori [infrastruttura](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) come i server MongoDB, Solr, MySQL, FFmpeg e email.

La AEM Demo Machine include:

* A [interfaccia utente grafica](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface).
* Script Apache ANT con configurabile [proprietà](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) e [target](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line).

* Pacchetti da installare.

La AEM Demo Machine è stata testata con successo con CQ 5.5, CQ 5.6.1, AEM 6.0, AEM 6.1, AEM 6.2, AEM 6.3 e AEM 6.4 su Windows, MacOS e Linux.

Il Demo Machine AEM richiede una licenza AEM valida.

>[!NOTE]
>
>Visualizzare un [introduzione video](https://www.youtube.com/watch?v=zEE_zkR9fVQ&amp;feature=youtu.be) alla AEM Demo Machine (13:26).

## Documentazione di AEM Communities {#aem-communities-documentation}

* Visita [Distribuzione di Communities](deploy-communities.md) per informazioni sulle distribuzioni consigliate.
* Visita [Amministrazione di siti di Communities](administer-landing.md) per ulteriori informazioni su come creare un sito community, aggiungere gruppi community, configurare modelli di sito community, moderare contenuti community, gestire membri, assegnare tag, notifiche, valutazione e badge,
* Visita [Sviluppo di Communities](communities.md) per informazioni sul framework dei componenti sociali (SCF) e sulla personalizzazione dei componenti e delle funzionalità di Communities.
* Visita [Authoring dei componenti di Communities](author-communities.md) per scoprire come creare e configurare i componenti di Communities.
