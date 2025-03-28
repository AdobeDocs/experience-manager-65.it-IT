---
title: SRP - Archiviazione di contenuti community
description: A partire da AEM Communities 6.1, i contenuti generati dagli utenti (UGC) vengono memorizzati in un unico archivio comune fornito da un provider di risorse di archiviazione (SRP)
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: e29aae44-67be-43d2-8004-c986412d9e63
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 0%

---

# SRP - Archiviazione di contenuti community {#srp-community-content-storage}

## Introduzione {#introduction}

A partire da AEM Communities 6.1, i contenuti generati dagli utenti (UGC, User-Generated Content) vengono memorizzati in un unico archivio comune fornito da un provider di risorse di archiviazione (SRP, Storage Resource Provider). Sono disponibili diverse opzioni SRP tra cui scegliere, ad esempio ASRP, MSRP e JSRP.

A differenza delle versioni precedenti, non esiste alcuna replica in avanti/indietro di UGC tra le istanze AEM. SRP rende invece direttamente accessibili i contenuti generati dagli utenti (UGC, User-Generated Content) per operazioni di creazione, lettura, aggiornamento ed eliminazione (CRUD, Create, Update, Delete) da tutte le istanze di authoring e pubblicazione, con un&#39;eccezione per JSRP.

Di seguito sono riportate le [caratteristiche di ogni opzione SRP](#characteristics-of-srp-options), che sono informazioni fondamentali per il processo decisionale durante la scelta dell&#39;SRP appropriato e della [distribuzione sottostante](/help/communities/topologies.md).

Per informazioni dettagliate sull&#39;utilizzo di SRP per UGC, vedere [Panoramica provider risorse di archiviazione](/help/communities/srp.md).

>[!NOTE]
>
>SRP si applica solo al contenuto della community. Non influisce sulla posizione in cui è archiviato il contenuto del sito ([archivio nodi](/help/sites-deploying/data-store-config.md)) e non influisce sulla gestione sicura della registrazione degli utenti, dei profili utente e dei gruppi di utenti tra le istanze AEM (vedi anche [Gestione dei dati utente](#managing-user-data)).

>[!CAUTION]
>
>A partire da AEM 6.1, [UGC non viene mai replicato](#ugc-never-replicated).
>
>Se la distribuzione non include un archivio comune, ad esempio la topologia predefinita [JSRP](/help/communities/topologies.md#jsrp), UGC sarà visibile solo nell&#39;istanza di pubblicazione o di authoring dell&#39;AEM in cui è stato immesso. Solo se la topologia include un cluster di pubblicazione, l&#39;UGC sarà visibile in qualsiasi istanza di pubblicazione.

## Caratteristiche delle opzioni SRP {#characteristics-of-srp-options}

[ASRP - Provider risorsa di archiviazione Adobe](/help/communities/asrp.md)

Con questa opzione, l’UGC viene mantenuto in remoto in un servizio cloud ospitato e gestito da Adobe. È necessaria una licenza aggiuntiva e la collaborazione con un rappresentante del conto per effettuare il provisioning del conto per quella specifica licenza. ASRP richiede:

* Servizio cloud associato fornito e supportato da Adobe per archiviare i contenuti della community.
* Scelta di un centro dati in una specifica area geografica (Stati Uniti, EMEA, APAC).

* Tutti gli accessi programmatici a UGC devono essere effettuati tramite l’API SRP.

ASRP è adatto:

* Per farm di pubblicazione TarMK.
* Quando non vi è alcuna intenzione di investire nello storage locale.

>[!NOTE]
>
>In ASRP, il caricamento di allegati ai post (o ai commenti) è limitato a 50 MB.

[MSRP - Provider risorsa di archiviazione MongoDB](/help/communities/msrp.md)

Con questa opzione, l’UGC viene mantenuto direttamente in un’istanza MongoDB locale.

Il piano MSRP richiede:

* Un’installazione locale autorizzata di MongoDB per archiviare i contenuti della community.
* Installazione locale di Apache Solr.
* Tutti gli accessi programmatici a UGC devono essere effettuati tramite l’API SRP.

ASRP è adatto:

* Per una farm di pubblicazione TarMK esistente.
* Per un cluster MongoMK o RdbMK.
* Quando sono previsti volumi elevati di contenuti della community.

[DSRP - Provider risorsa di archiviazione database relazionale](/help/communities/dsrp.md)

Con questa opzione, l&#39;UGC viene mantenuto direttamente in un&#39;istanza di database MySQL locale.

DSRP richiede:

* Installazione locale di MySQL per archiviare il contenuto della community.
* Installazione locale di Apache Solr.
* Tutti gli accessi programmatici a UGC devono essere effettuati tramite l’API SRP.

DSRP è adatto:

* Per una farm di pubblicazione TarMK esistente.
* Per un cluster MongoMK o RdbMK.
* Quando sono previsti volumi elevati di contenuti della community.

[JSRP - Provider risorsa di archiviazione JCR](/help/communities/jsrp.md)

Con l’opzione predefinita, non esiste un archivio comune. L’UGC viene mantenuto solo nello stesso archivio JCR dell’istanza AEM in cui è stato inserito.

JSRP:

* Memorizza il contenuto della community nell’archivio JCR dell’istanza di authoring o pubblicazione AEM in cui è stato pubblicato.
* Richiede l’accesso programmatico a UGC tramite l’API SRP.
* Richiede un cluster di pubblicazione se viene distribuita più di un’istanza di pubblicazione (non esiste alcun meccanismo di replica tra le istanze di pubblicazione in una farm TarMK).
* la moderazione viene eseguita solo nell&#39;ambiente di pubblicazione (non esiste alcun meccanismo di replica inversa/avanti tra authoring e pubblicazione).
* È ideale per lo sviluppo, le dimostrazioni e la formazione.

## Configurazione di SRP {#configuring-srp}

L&#39;opzione di archiviazione predefinita, basata sulla distribuzione sottostante, viene specificata tramite la [console Configurazione archiviazione](/help/communities/srp-config.md).

Per informazioni dettagliate sulla configurazione di ciascuna opzione, consulta:

* [ASRP - Provider risorsa di archiviazione Adobe](/help/communities/asrp.md)
* [MSRP - Provider risorsa di archiviazione MongoDB](/help/communities/msrp.md)
* [DSRP - Provider risorsa di archiviazione database relazionale](/help/communities/dsrp.md)
* [JSRP - Provider risorsa di archiviazione JCR](/help/communities/jsrp.md)

Se non è selezionata alcuna opzione di archiviazione attiva, JSRP è attivato per impostazione predefinita.

## Informazioni aggiuntive {#additional-information}

### UGC mai replicato {#ugc-never-replicated}

Nell’ambiente di authoring, un autore crea il contenuto della pagina e lo replica nell’ambiente di pubblicazione. Quando una pagina include una funzione interattiva di AEM Communities, ad esempio commenti, recensioni, forum, blog o domande e risposte, l’interazione dei membri (visitatori del sito con accesso) su un’istanza Publish genera contenuti generati dagli utenti (UGC, User Generated Content) immessi nell’ambiente di pubblicazione.

In precedenza, questo contenuto della community veniva replicato inverso nelle istanze di authoring e dall’istanza di authoring a quella di pubblicazione. È stato problematico mantenere la coerenza tra le istanze AEM con la replica inversa e successiva.

A partire da AEM Communities 6.1, la necessità di replica di UGC è stata eliminata utilizzando lo storage condiviso per UGC, come descritto in precedenza.

Mentre il contenuto del sito viene replicato, UGC non viene mai replicato.

### Gestione dei dati utente {#managing-user-data}

Sono interessati anche i [*utenti*, *gruppi di utenti* e *profili utente*](/help/communities/users.md). Questi dati relativi all&#39;utente, quando vengono creati e aggiornati nell&#39;ambiente di pubblicazione, devono essere resi disponibili ad altre istanze di pubblicazione quando la topologia è una [farm di pubblicazione](/help/sites-deploying/recommended-deploys.md#tarmk-farm).

A partire da AEM Communities 6.1, i dati relativi all’utente vengono sincronizzati utilizzando la distribuzione Sling anziché la replica. Per ulteriori informazioni, visitare [Sincronizzazione utente](/help/communities/sync.md).

### Aggiornamento ad AEM Communities 6.5 {#upgrading-to-aem-communities}

Quando si esegue l’aggiornamento alle community AEM 6.5, se è necessario mantenere le UGC preesistenti, è necessario adottare misure a seconda che la community AEM 5.6.1 o AEM 6.0 utilizzasse lo storage Adobe on-demand o lo storage on-premise delle UGC.

Per informazioni dettagliate, visita [Aggiornamento ad AEM Communities 6.5](/help/communities/upgrade.md).
