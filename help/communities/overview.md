---
title: Panoramica di AEM Communities
seo-title: Panoramica di AEM Communities
description: Panoramica delle funzioni e della configurazione di AEM Communities
seo-description: Panoramica delle funzioni e della configurazione di AEM Communities
uuid: 14405847-36ae-4958-bdc6-d799ecd05f06
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 44374006-f711-4af8-a1fe-f89164f79581
docset: aem65
translation-type: tm+mt
source-git-commit: 70e6f2d8366456e5091b7b775dc40914948921ab

---


# Panoramica di AEM Communities{#aem-communities-overview}

Adobe Experience Manager (AEM) Communities permette di creare rapidamente un sito di community on-premise con prestazioni ottimizzate e una migliore gestione del sito, che favorisce la conversione dei visitatori in membri attivi della community.

Contatta il tuo rappresentante commerciale per informazioni sulle licenze di AEM Communities, oltre a licenze aggiuntive per le funzioni di abilitazione e Adobe Analytics.

## Funzioni di Communities {#communities-features}

AEM Communities consente lo sviluppo di una relazione con i visitatori del sito, che:

* **informazioni** tramite blog, domande e risposte e calendari degli eventi,
* **ottenere informazioni **tramite forum, commenti e altri contenuti della community, spesso denominati contenuti generati dall&#39;utente (UGC).
* Consente** moderazione **dai membri attendibili nell&#39;ambiente di pubblicazione,
* **login sociale **con Twitter e Facebook,
* **traduzione** in linea del contenuto comunitario,
* **creazione di gruppi comunitari **dal sito della comunità pubblicato,
* **punteggio **per l&#39;assegnazione di badge,
* **condivisione** dei file,
* **notifiche **e flussi **di attività**,

* consente **di assegnare tag** (@reference) ad altri membri registrati in Contenuto generato dall&#39;utente, per attirare la loro attenzione.
* Supporta la navigazione tramite **tastiera** sui componenti di abilitazione (ad esempio Catalogo e Riproduzione corso, Assegnazioni, Libreria file).

Le funzioni Community possono essere dimostrate utilizzando [AEM Demo Machine](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki) disponibile pubblicamente su GitHub.com o con la nuova implementazione di riferimento We.Retail.

## Siti community {#community-sites}

Un sito community è un sito AEM creato tramite una semplice procedura guidata che consente di creare un sito Web con molte funzioni comuni già collegate al sito.

Creazione guidata [](/help/communities/sites-console.md)sito:

* raccoglie le caratteristiche del sito, in base al modello [di sito](/help/communities/sites.md) community selezionato, che è:

   * basato su funzioni [della community](#community-functions)
   * funzione opzionale per i gruppi [](#communitygroups) della community

* utilizza le impostazioni per configurare:

   * moderazione
   * login
   * traduzione

* offre funzioni essenziali:

   * responsive design:
utilizza i temi [di Bootstrap su Twitter](https://getbootstrap.com)

   * login :
registrazione automatica, login [](/help/communities/social-login.md)social network, profili utente

   * notifiche:
i membri visualizzano gli eventi rilevanti per loro e i contenuti generati dagli utenti in cui sono [@menzionati](/help/communities/overview.md#mentionssupport).

   * messaging:
i membri possono inviare o ricevere messaggi all&#39;interno del sito della comunità
   * search:
capacità di ricerca all&#39;interno del sito della community
   * cambio lingua:
possibilità di selezionare una lingua per un sito [multilingue](/help/sites-administering/translation.md)

   * amministrazione:
accesso per i membri autorizzati a moderare e gestire gli utenti all&#39;interno del sito community

* elimina molti passaggi di authoring a livello di pagina:

   * marchio:
caricamento facoltativo di un&#39;immagine banner da visualizzare su tutte le pagine del sito della community
   * menu di navigazione:
i collegamenti di navigazione sono forniti per le funzioni incluse nel modello di sito community

Per provare la facilità di creare rapidamente un nuovo sito community, visita la [Guida introduttiva ad AEM Communities](/help/communities/getting-started.md).

## Persistenza del contenuto della community {#community-content-persistence}

Per migliorare le prestazioni e la sincronizzazione del contenuto della community, AEM Communities richiede uno store comune specifico per il contenuto generato dall’utente (UGC) condiviso tra tutte le istanze di AEM (creazione e pubblicazione).

Il contenuto della community è facilmente accessibile tramite l&#39;SRP (Storage Resource Provider), che fornisce un livello per l&#39;accesso separato dalla topologia sottostante e supporta un archivio comune per UGC.

Per ulteriori informazioni sulla persistenza del contenuto della community e sulle distribuzioni consigliate, vedi:

* [Archiviazione](/help/communities/working-with-srp.md)dei contenuti della community, che illustra le opzioni di storage SRP disponibili per UGC.
* [Topologie](/help/communities/topologies.md)consigliate, che trattano le topologie in base al caso di utilizzo e alla scelta SRP.
* [Aggiornamento ad AEM 6.5 Communities](/help/communities/upgrade.md), che fornisce informazioni utili sull’UGC quando si passa ad AEM 6.5.

## Console community {#communities-consoles}

Nell’ambiente di authoring, la console di navigazione globale consente di accedere alla console [](/help/communities/consoles.md)Community, che contiene:

* La console [Sites](/help/communities/sites-console.md)

   * creazione di siti
   * modifica del sito
   * gestione del sito
   * [Console Gruppi](/help/communities/groups.md) community

* [Console Moderazione](/help/communities/moderation.md)

   * interfaccia utente di moderazione in blocco comune per gli ambienti di creazione e pubblicazione
   * nuovi criteri di filtro

* [Console di gestione Membri e Gruppi](/help/communities/members.md)

   * consente di creare e gestire utenti (membri) lato pubblicazione dall’ambiente di authoring
   * consente di vietare i membri
   * consente di creare e gestire gruppi di utenti lato pubblicazione (gruppi di membri) dall’ambiente di authoring

* [Console Rapporti](/help/communities/reports.md)

   * consente di generare rapporti su assegnazioni, post e viste

* [Console Risorse](/help/communities/resources.md)

   * consente di creare risorse di abilitazione e percorsi di apprendimento
   * consente di accedere ai rapporti sulle risorse di abilitazione e sui percorsi di apprendimento

La console degli strumenti globali consente di accedere ai seguenti strumenti di Communities:

* [Console Modelli](/help/communities/tools.md#sitetemplatesconsole) per siti

   * creazione e gestione di modelli di sito community

* [Console Modelli](/help/communities/tools.md#grouptemplatesconsole) gruppo

   * creazione e gestione di modelli di gruppi di community

* [Console Funzioni](/help/communities/tools.md#communityfunctionsconsole) community

   * creazione e gestione di funzioni per community

* [Console di configurazione](/help/communities/tools.md#storageconfiguratonconsole) dell&#39;archivio

   * selezionare e configurare lo store [](/help/communities/working-with-srp.md) comune per il sito

* [Guida dei componenti](/help/communities/components-guide.md)

   * un sito di esempio, [Community Components](https://localhost:4502/editor.html/content/community-components/en.html), che fornisce un esempio di tutti i componenti Community con la configurazione predefinita e la possibilità di sperimentare con essi

## Modelli per sito community {#community-site-templates}

La creazione di siti community si basa sulla selezione di un modello di sito community per configurare rapidamente un sito community indipendente da qualsiasi sito campione.

Un modello di sito community, composto da funzioni per la community e modelli per i gruppi di community, fornisce la struttura per un sito community che include login, profili utente, messaggistica, menu del sito, ricerca, temi e funzioni di branding.

Consultate la console [Modelli](/help/communities/sites.md)sito.

## Funzioni per community {#community-functions}

Le caratteristiche previste per un&#39;esperienza comunitaria sono ben note. Con AEM Communities, queste funzioni sono disponibili come elementi costitutivi, note come funzioni per la community.

Le funzioni della community sono normali pagine AEM e includono componenti collegati tra loro in una funzione facilmente incorporata in un modello di sito della community.

Consultate la console Funzioni [community](/help/communities/functions.md).

## Gruppi community e modelli di gruppo {#community-groups-and-group-templates}

La funzione per i gruppi della community è la possibilità che una sub-community venga creata in modo dinamico all&#39;interno di un sito della community da utenti autorizzati e membri della community sia dall&#39;ambiente di creazione che da quello di pubblicazione.

Dall&#39;ambiente di authoring, i gruppi di community (sub-community) possono essere creati all&#39;interno di un sito community esistente o nidificati all&#39;interno di un gruppo esistente, quando la struttura del modello contiene la funzione [](/help/communities/functions.md#groups-function)Gruppi.

La creazione di un gruppo community richiede la selezione di un modello di gruppo community che fornisce la progettazione delle pagine del gruppo community. Quando una funzione Groups viene aggiunta a una struttura di modelli, viene configurata per specificare un modello di gruppo o per fornire una scelta di modelli al momento della creazione di un nuovo gruppo community.

Consulta anche:

* [Console](/help/communities/groups.md) Gruppi del sito per la creazione di sottocomunità nell’ambiente di authoring
* [Console](/help/communities/tools-groups.md) Modelli per gruppi per la creazione della struttura del sito per i gruppi
* [Guida introduttiva ad AEM Communities](/help/communities/getting-started.md) per un&#39;esercitazione per la creazione rapida di un sito community con gruppi nidificati

## Componenti community {#community-components}

I componenti [della](/help/communities/author-communities.md) community da cui viene creato un sito community possono essere utilizzati per aggiungere funzioni Community a qualsiasi sito AEM.

La guida ai componenti [della](/help/communities/components-guide.md) community è disponibile per l&#39;esplorazione interattiva dei componenti.

## Tipi di comunità {#types-of-communities}

### Community di coinvolgimento {#engagement-community}

Una community di coinvolgimento è un sito della community incentrato sul coinvolgimento dei clienti per informare, richiedere feedback e consentire ai clienti di interagire come membri della community.

Le funzioni di una community di partecipazione possono includere:

* login
* messaging
* forum
* commenti
* recensioni
* valutazioni
* votazione
* blog
* gruppi
* calendari
* traduzione
* moderazione
* notifiche
* punteggio e simboli
* reporting delle analisi

Per provare la facilità e la rapidità con cui creare una nuova community di coinvolgimento, visita la [Guida introduttiva ad AEM Communities](/help/communities/getting-started.md).

### Community di abilitazione {#enablement-community}

Una community di abilitazione è un sito della community che include funzionalità per l&#39;apprendimento online.

Le funzioni di una community di abilitazione possono includere:

* tutte le caratteristiche di una community di [coinvolgimento](#engagement-community)
* capacità di assegnare contenuti e risorse di apprendimento a membri e gruppi di membri
* supporta il contenuto SCORM, come quiz e test
* tracciamento del completamento delle assegnazioni
* accesso a reporting e analisi
* la possibilità di parlare di una risorsa di apprendimento attraverso forum, messaggi, commenti e valutazioni

Una community di abilitazione può essere creata quando viene configurato [il componente aggiuntivo](/help/communities/enablement.md)Abilitazione, il che richiede licenze aggiuntive da utilizzare in un ambiente di produzione. Un sito community di abilitazione includerà la funzione [](#community-functions)assegnazioni.

Per provare la facilità di creazione di una nuova community di abilitazione, visita la [Guida introduttiva ad AEM Communities per l&#39;abilitazione](/help/communities/getting-started-enablement.md).

## AEM Demo Machine {#aem-demo-machine}

La Demo Machine [di](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) AEM gestisce ed esegue dimostrazioni per [siti](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites), [risorse](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets), [community](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities), [app](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps) [](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms)e moduli, che spesso richiedono una configurazione maggiore rispetto all&#39;avvio di un&#39;istanza QuickStart. Il Demo Machine di AEM configurerà un&#39; [infrastruttura](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) aggiuntiva come MongoDB, Solr, MySQL, FFmpeg e i server di posta elettronica.

La Demo Machine di AEM include:

* un&#39;interfaccia utente [grafica](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface)
* Script Apache ANT con [proprietà](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) configurabili e [destinazioni](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line)

* pacchetti da installare

La Demo Machine di AEM è stata testata con CQ 5.5, CQ 5.6.1, AEM 6.0, AEM 6.1, AEM 6.2, AEM 6.3 e AEM 6.4 su Windows, MacOS e Linux.

AEM Demo Machine richiede una licenza AEM valida.

>[!NOTE]
>
>Guardate un&#39;introduzione [](https://www.youtube.com/watch?v=zEE_zkR9fVQ&feature=youtu.be) video alla Demo Machine di AEM (13:26).

## Documentazione di AEM Communities {#aem-communities-documentation}

* Per informazioni sulle distribuzioni consigliate, visitate [Implementazione delle community](/help/communities/deploy-communities.md) .
* Visitate [Administering Communities Sites](/help/communities/administer-landing.md) per informazioni su come creare un sito community, aggiungere gruppi community, configurare modelli di sito community, moderare contenuti community, gestire membri, assegnare tag, notifiche, punteggio e simboli.
* Visitate [Developing Communities](/help/communities/communities.md) per informazioni sul framework dei componenti sociali (SCF) e sulla personalizzazione dei componenti e delle funzionalità di Communities.
* Per informazioni su come creare e configurare i componenti di Community, consulta [Authoring dei componenti](/help/communities/author-communities.md) di Communities.

