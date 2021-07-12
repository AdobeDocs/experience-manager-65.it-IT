---
title: SRP - Archiviazione dei contenuti della community
seo-title: SRP - Archiviazione dei contenuti della community
description: A partire da AEM Communities 6.1, il contenuto generato dall’utente (UGC) viene memorizzato in un singolo archivio comune fornito da un provider di risorse di archiviazione (SRP)
seo-description: A partire da AEM Communities 6.1, il contenuto generato dall’utente (UGC) viene memorizzato in un singolo archivio comune fornito da un provider di risorse di archiviazione (SRP)
uuid: d45e03c4-378b-4510-a6a0-d48c8cb879d9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 6f13b21a-f4ef-4889-9b8e-4da3f846fa35
docset: aem65
role: Admin
exl-id: e29aae44-67be-43d2-8004-c986412d9e63
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 0%

---

# SRP - Archiviazione dei contenuti della community {#srp-community-content-storage}

## Introduzione {#introduction}

A partire da AEM Communities 6.1, il contenuto generato dall’utente (UGC) viene memorizzato in un singolo archivio comune fornito da un provider di risorse di archiviazione (SRP). Ci sono diverse opzioni SRP da scegliere, come ASRP, MSRP e JSRP.

A differenza delle versioni precedenti, non esiste una replica inversa/forward di UGC tra le istanze AEM. Al contrario, l’SRP rende l’UGC direttamente accessibile per le operazioni di creazione, lettura, aggiornamento ed eliminazione (CRUD) da tutte le istanze di authoring e pubblicazione, con un’eccezione per JSRP.

Di seguito sono riportate le [caratteristiche di ogni opzione SRP](#characteristics-of-srp-options), che sono informazioni cruciali per il processo decisionale quando si sceglie l&#39;SRP appropriato e la [distribuzione sottostante](/help/communities/topologies.md).

Per informazioni dettagliate sull&#39;utilizzo dell&#39;SRP per UGC, vedere [Panoramica del provider di risorse di storage](/help/communities/srp.md).

>[!NOTE]
>
>L’SRP si applica solo ai contenuti della community. Non influisce sulla posizione in cui viene memorizzato il contenuto del sito ([node store](/help/sites-deploying/data-store-config.md)) e non sulla gestione sicura della registrazione utente, dei profili utente e dei gruppi di utenti tra le istanze AEM (vedi anche [Gestione dei dati utente](#managing-user-data)).

>[!CAUTION]
>
>A partire da AEM 6.1, [UGC non viene mai replicato](#ugc-never-replicated).
>
>Quando la distribuzione non include un archivio comune, ad esempio la topologia predefinita [JSRP](/help/communities/topologies.md#jsrp), UGC sarà visibile solo sull&#39;istanza di pubblicazione o authoring AEM in cui è stato immesso. Solo se la topologia include un cluster di pubblicazione, l&#39;UGC sarà visibile su qualsiasi istanza di pubblicazione.

## Caratteristiche delle opzioni SRP {#characteristics-of-srp-options}

[ASRP - Provider risorsa di archiviazione Adobe](/help/communities/asrp.md)

Con questa opzione, l’UGC viene mantenuto in remoto in un servizio cloud ospitato e gestito da Adobe. Richiede una licenza aggiuntiva e collabora con un rappresentante commerciale per fornire l&#39;account per quella licenza specifica. L’ASRP richiede:

* Un servizio cloud associato fornito e supportato da Adobe per memorizzare i contenuti della community.
* Scelta di un centro dati in una specifica area geografica (Stati Uniti, EMEA, APAC).

* L’accesso programmatico a UGC può essere effettuato tramite l’API SRP.

ASRP è adatto:

* Per la farm di pubblicazione TarMK.
* Quando non si intende investire nello storage locale.

>[!NOTE]
>
>C&#39;è un limite per caricare gli allegati ai post (o commenti) in ASRP, che è di 50 MB.

[MSRP - Provider risorsa di archiviazione MongoDB](/help/communities/msrp.md)

Con questa opzione, l’UGC viene mantenuto direttamente in un’istanza MongoDB locale.

MSRP richiede:

* Installazione locale con licenza di MongoDB per memorizzare i contenuti della community.
* Installazione locale di Apache Solr.
* L’accesso programmatico a UGC può essere effettuato tramite l’API SRP.

ASRP è adatto:

* Per una farm di pubblicazione TarMK esistente.
* Per un cluster MongoMK o RdbMK.
* Quando ci si aspetta grandi quantità di contenuti della community.

[DSRP - Provider risorsa di archiviazione database relazionale](/help/communities/dsrp.md)

Con questa opzione, l&#39;UGC viene mantenuto direttamente in un&#39;istanza di database MySQL locale.

DSRP richiede:

* Installazione locale di MySQL per memorizzare il contenuto della community.
* Installazione locale di Apache Solr.
* L’accesso programmatico a UGC può essere effettuato tramite l’API SRP.

DSRP è adatto:

* Per una farm di pubblicazione TarMK esistente.
* Per un cluster MongoMK o RdbMK.
* Quando ci si aspetta grandi quantità di contenuti della community.

[JSRP - Provider risorsa di archiviazione JCR](/help/communities/jsrp.md)

Con l&#39;opzione predefinita, non esiste un archivio comune. L’UGC viene mantenuto solo nello stesso archivio JCR dell’istanza AEM in cui è stato inserito.

JSRP:

* Memorizza il contenuto della community nell’archivio JCR dell’istanza di authoring o pubblicazione AEM a cui è stato pubblicato.
* Richiede l’accesso programmatico a UGC tramite l’API SRP.
* Richiede un cluster di pubblicazione se vengono distribuite più istanze di pubblicazione (non esiste un meccanismo di replica tra le istanze di pubblicazione in una farm TarMK).
* la moderazione viene eseguita solo nell’ambiente di pubblicazione (non esiste un meccanismo di replica inversa/forward tra l’autore e la pubblicazione).
* È il migliore per lo sviluppo, le dimostrazioni e la formazione.

## Configurazione dell’SRP {#configuring-srp}

La specificazione dell&#39;opzione di archiviazione predefinita, basata sulla distribuzione sottostante, viene eseguita tramite la [console di configurazione dello storage](/help/communities/srp-config.md).

Per i dettagli di configurazione di ciascuna opzione, vedi:

* [ASRP - Provider risorsa di archiviazione Adobe](/help/communities/asrp.md)
* [MSRP - Provider risorsa di archiviazione MongoDB](/help/communities/msrp.md)
* [DSRP - Provider risorsa di archiviazione database relazionale](/help/communities/dsrp.md)
* [JSRP - Provider risorsa di archiviazione JCR](/help/communities/jsrp.md)

Se non è selezionata alcuna opzione di archiviazione attiva, per impostazione predefinita JSRP è abilitato.

## Informazioni aggiuntive {#additional-information}

### UGC non replicato {#ugc-never-replicated}

Nell’ambiente di authoring, un autore crea il contenuto della pagina e lo replica nell’ambiente di pubblicazione. Quando una pagina include una funzione di AEM Communities interattiva, ad esempio commenti, revisioni, forum, blog o QnA, l’interazione dei membri (connessi ai visitatori del sito) su un’istanza di pubblicazione si traduce in contenuti generati dagli utenti (UGC) inseriti nell’ambiente di pubblicazione.

In precedenza, il contenuto della community veniva replicato inverso nelle istanze dell’autore e dall’autore replicato alle istanze di pubblicazione. È stato problematico mantenere la coerenza tra le istanze AEM con la replica inversa e successiva.

A partire da AEM Communities 6.1, la necessità di replica di UGC è stata eliminata utilizzando lo storage condiviso per UGC, come descritto in precedenza.

Mentre il contenuto del sito viene replicato, UGC non viene mai replicato.

### Gestione dei dati utente {#managing-user-data}

Anche i siti CommunitIes sono [*utenti*, *gruppi di utenti* e *profili utente*](/help/communities/users.md). Questi dati relativi all’utente, quando creati e aggiornati nell’ambiente di pubblicazione, devono essere resi disponibili ad altre istanze di pubblicazione quando la topologia è una [farm di pubblicazione](/help/sites-deploying/recommended-deploys.md#tarmk-farm).

A partire da AEM Communities 6.1, i dati relativi all’utente vengono sincronizzati utilizzando la distribuzione Sling invece della replica. Per ulteriori informazioni, visita [Sincronizzazione utente](/help/communities/sync.md).

### Aggiornamento ad AEM Communities 6.5 {#upgrading-to-aem-communities}

Quando si esegue l’aggiornamento a AEM 6.5 Communities, se è necessario mantenere gli UGC preesistenti, è necessario adottare misure a seconda che la comunità AEM 5.6.1 o AEM 6.0 utilizzasse lo storage Adobe on-demand o on-premise di UGC.

Per ulteriori informazioni, visita [Aggiornamento ad AEM Communities 6.5](/help/communities/upgrade.md).
