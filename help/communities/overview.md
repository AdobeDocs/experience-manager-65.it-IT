---
title: Panoramica di AEM Communities
description: Scopri le nozioni di base sulle funzioni e sulla configurazione di Adobe Experience Manager Communities.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
exl-id: d6243dff-a067-455c-a326-5f451f225efd
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1204'
ht-degree: 2%

---

# Panoramica di AEM Communities {#aem-communities-overview}

Le community Adobe Experience Manager (AEM) consentono di creare rapidamente un sito community on-premise con prestazioni migliori, una migliore gestione del sito e la promozione della conversione dei visitatori del sito in membri di valore della community.

## Funzioni community {#communities-features}

AEM Communities consente di sviluppare una relazione con i visitatori del sito, che:

* **Informa** tramite blog, domande e risposte e calendari eventi,
* Mentre **acquisiscono informazioni** tramite forum, commenti e altri contenuti della community, spesso denominati contenuti generati dagli utenti (UGC, User-Generated Content).
* Consente la **moderazione** da parte di membri attendibili nell&#39;ambiente Publish,
* **Accesso social** con Twitter e Facebook,
* **Traduzione in linea** del contenuto community,
* **Creazione di gruppi community** dal sito community pubblicato,
* **Punteggio** per assegnare i distintivi,
* **Condivisione file**,
* **Notifiche** e **flussi attività**,
* Consente a **tagging** (@mention) altri membri registrati in Contenuti generati dagli utenti di richiamare la loro attenzione.

Le funzionalità delle community possono essere dimostrate utilizzando la [macchina dimostrativa AEM](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki) disponibile pubblicamente su GitHub.com o con la nuova implementazione di riferimento `We.Retail`.

## Siti community {#community-sites}

Un sito community è un sito AEM creato tramite una semplice procedura guidata che consente di creare un sito web con molte funzioni comuni collegate al sito.

La [procedura guidata per la creazione del sito](/help/communities/sites-console.md):

* Assembla le funzionalità del sito in base al [modello di sito community](/help/communities/sites.md) selezionato:

   * creato da [funzioni community](#community-functions)
   * funzionalità facoltativa [gruppi community](#communitygroups)

* Utilizza le impostazioni per configurare:

   * moderazione
   * accesso
   * traduzione

* Offre funzioni essenziali:

   * Progettazione reattiva: utilizza [temi Bootstrap Twitter](https://getbootstrap.com)

   * Accesso: registrazione autonoma, [accesso social](/help/communities/social-login.md), profili utente

      * Notifiche:
i membri visualizzano eventi rilevanti per loro e contenuti generati dall&#39;utente in cui sono [@mentioned](/help/communities/overview.md#mentionssupport).

      * Messaggistica: i membri possono inviare o ricevere messaggi all&#39;interno del sito community.
      * Ricerca: possibilità di eseguire ricerche all’interno del sito community.
      * Cambio di lingua: possibilità di selezionare una lingua per un [sito multilingue](/help/sites-administering/translation.md).

      * Amministrazione: consente ai membri autorizzati di moderare e gestire gli utenti all&#39;interno del sito community.

* Elimina molti passaggi di authoring a livello di pagina:

   * Branding: caricamento opzionale di un&#39;immagine del banner da visualizzare su tutte le pagine del sito community
   * Menu di navigazione: i collegamenti di navigazione sono disponibili per le funzioni incluse nel modello di sito community.

Per provare la semplicità della creazione rapida di un sito community, visita [Guida introduttiva ad AEM Communities](/help/communities/getting-started.md).

## Persistenza dei contenuti community {#community-content-persistence}

Per migliorare le prestazioni e la sincronizzazione dei contenuti della community, AEM Communities richiede un archivio comune specifico per i contenuti generati dagli utenti (UGC) condivisi tra tutte le istanze AEM (di authoring e pubblicazione).

Il contenuto della community è facilmente accessibile tramite il provider di risorse di archiviazione (SRP), che fornisce un livello per separare l’accesso dalla topologia sottostante e supporta un archivio comune per UGC.

Per ulteriori informazioni sulla persistenza dei contenuti della community e sulle distribuzioni consigliate, consulta:

* [Archiviazione contenuto community](/help/communities/working-with-srp.md): illustra le opzioni di archiviazione SRP disponibili per UGC.
* [Topologie consigliate](/help/communities/topologies.md): illustra le topologie in base al caso d&#39;uso e alla scelta SRP.
* [Aggiornamento alle community AEM 6.5](/help/communities/upgrade.md): fornisce informazioni utili sulle UGC durante il passaggio all&#39;AEM 6.5.

## Console community {#communities-consoles}

Nell&#39;ambiente di authoring, la console di navigazione globale fornisce l&#39;accesso alla console [Communities](/help/communities/consoles.md), che contiene:

* La console [Sites](/help/communities/sites-console.md)

   * Creazione di siti
   * Modifica del sito
   * Gestione del sito
   * Console [Gruppi community](/help/communities/groups.md)

* Console [Moderazione](/help/communities/moderation.md)

   * Interfaccia utente comune per la moderazione in blocco per gli ambienti Author e Publish.
   * Nuovi criteri di filtro.

* [Membri e gruppi](/help/communities/members.md) console di gestione

   * Consente di creare e gestire utenti lato pubblicazione (membri) dall’ambiente di authoring.
   * Consente di vietare i membri.
   * Consente di creare e gestire gruppi di utenti lato pubblicazione (gruppi di membri) dall’ambiente di authoring.

* Console [Rapporti](/help/communities/reports.md)

   * Consente di generare rapporti su assegnazioni, post e visualizzazioni.

La console Strumenti globale consente di accedere ai seguenti strumenti di Communities:

* [Modelli del sito](/help/communities/tools.md#sitetemplatesconsole) console

   * Creazione e gestione di modelli di sito community.

* Console [Modelli di gruppo](/help/communities/tools.md#grouptemplatesconsole)

   * Creare e gestire modelli per gruppi community.

* Console [Funzioni community](/help/communities/tools.md#communityfunctionsconsole)

   * Creare e gestire funzioni community.

* [Configurazione archiviazione](/help/communities/tools.md#storageconfiguratonconsole) console

   * Seleziona e configura l&#39;[archivio comune](/help/communities/working-with-srp.md) per il sito.

* [Guida dei componenti](/help/communities/components-guide.md)

   * In un sito di esempio, [Componenti community](https://localhost:4502/editor.html/content/community-components/en.html) è incluso un esempio di tutti i componenti community con la relativa configurazione predefinita e la possibilità di utilizzarli in modo sperimentale.

## Modelli per sito community {#community-site-templates}

La creazione di siti community si basa sulla selezione di un modello di sito community per impostare rapidamente un sito community indipendente da qualsiasi sito di esempio.

Un modello di sito per community, composto da funzioni per community e modelli per gruppi di community, fornisce la struttura di un sito per community. Include le funzioni di accesso, profili utente, messaggistica, menu del sito, ricerca, temi e branding.

Consulta la [console Modelli sito](/help/communities/sites.md).

## Funzioni community {#community-functions}

Le funzioni previste da un’esperienza community sono ben note. Con AEM Communities, queste funzioni sono disponibili come blocchi predefiniti, noti come funzioni community.

Le funzioni community sono normali pagine AEM e includono componenti collegati tra loro in una funzione che può essere facilmente incorporata in un modello di sito community.

Consulta la [console Funzioni community](/help/communities/functions.md).

## Gruppi community e modelli di gruppi {#community-groups-and-group-templates}

La funzione Gruppi community consente la creazione dinamica di una sottocommunity all’interno di un sito community da parte di utenti e membri autorizzati degli ambienti di authoring e pubblicazione.

Nell&#39;ambiente di authoring è possibile creare gruppi community (sottocomunità) all&#39;interno di un sito community esistente o nidificati all&#39;interno di un gruppo esistente, quando la struttura del modello contiene la funzione [Gruppi](/help/communities/functions.md#groups-function).

La creazione di un gruppo community richiede la selezione di un modello di gruppo community che fornisca la struttura delle pagine del gruppo community. Quando una funzione Gruppi viene aggiunta a una struttura di modelli, viene configurata per specificare un modello di gruppo o per fornire una scelta di modelli al momento della creazione di un nuovo gruppo community.

Consulta anche:

* [Console Gruppi del sito](/help/communities/groups.md) per la creazione di comunità secondarie nell&#39;ambiente di authoring.
* [Console Modelli di gruppo](/help/communities/tools-groups.md) per la creazione di strutture del sito per i gruppi.
* [Guida introduttiva di AEM Communities](/help/communities/getting-started.md) per l&#39;esercitazione per la creazione rapida di un sito community con gruppi nidificati.

## Componenti community {#community-components}

I [componenti community](/help/communities/author-communities.md) da cui viene creato un sito community possono essere utilizzati per aggiungere le funzionalità delle community a qualsiasi sito AEM.

La [guida ai componenti della community](/help/communities/components-guide.md) è disponibile per l&#39;esplorazione interattiva dei componenti.

## Community di coinvolgimento {#engagement-community}

Una community di engagement è un sito della community che coinvolge i clienti per informarli, richiederne il feedback e farli interagire come membri della community.

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

Per scoprire la semplicità della creazione rapida di una community di coinvolgimento, visita [Guida introduttiva ad AEM Communities](/help/communities/getting-started.md).

## Dispositivo dimostrativo AEM {#aem-demo-machine}

La [macchina dimostrativa AEM](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) gestisce ed esegue demo per AEM [Sites](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites), [Assets](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets), [Communities](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities), [Apps](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps) e [Forms](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms), che spesso richiedono una configurazione maggiore rispetto al semplice avvio di un&#39;istanza QuickStart. Il Demo Machine dell&#39;AEM configura ulteriori [infrastrutture](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) quali MongoDB, Solr, MySQL, FFmpeg e server di posta elettronica.

Il Demo Machine per AEM include:

* [interfaccia utente grafica](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface).
* Script Apache ANT con [proprietà](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) e [destinazioni](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line) configurabili.

* Pacchetti da installare.

Il Demo Machine per AEM è stato testato con successo con CQ 5.5, CQ 5.6.1, AEM 6.0, AEM 6.1, AEM 6.2, AEM 6.3 e AEM 6.4 su Windows, macOS e Linux®.

Il Demo Machine per AEM richiede una licenza AEM valida.

>[!NOTE]
>
>Visualizza un [video introduttivo](https://www.youtube.com/watch?v=zEE_zkR9fVQ&feature=youtu.be) sul dispositivo dimostrativo AEM (13:26).

## Documentazione di AEM Communities {#aem-communities-documentation}

* Visita [Distribuzione di Communities](deploy-communities.md) per scoprire le distribuzioni consigliate.
* Visita [Amministrazione di siti community](administer-landing.md) per scoprire come creare un sito community, aggiungere gruppi community, configurare modelli di sito community, moderare il contenuto della community, gestire i membri, assegnare tag, notifiche, punteggi e badge.
* Visita [Sviluppo di community](communities.md) per scoprire il framework dei componenti social network (SCF) e personalizzare i componenti e le funzionalità di Communities.
* Visita [Authoring dei componenti delle community](author-communities.md) per scoprire come creare e configurare i componenti delle community.
