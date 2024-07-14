---
title: Topologie consigliate per le community
description: Come affrontare la gestione dei contenuti generati dagli utenti (UGC, User-Generated Content)
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
exl-id: b6658330-d862-44e3-aac0-824fb91cd087
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 1%

---

# Topologie consigliate per le community {#recommended-topologies-for-communities}

A partire da AEM Communities 6.1, è stato adottato un approccio univoco per la gestione dei contenuti generati dagli utenti (UGC) inviati dai visitatori del sito (membri) dall’ambiente di pubblicazione.

Questo approccio è fondamentalmente diverso dal modo in cui la piattaforma AEM gestisce i contenuti del sito che sono generalmente gestiti dall’ambiente di authoring.

La piattaforma AEM utilizza un archivio nodi che replica il contenuto del sito dall’ambiente di authoring a quello di pubblicazione, mentre AEM Communities utilizza un singolo archivio comune per i contenuti generati dagli utenti che non vengono mai replicati.

Per l&#39;archivio UGC comune, è necessario scegliere un provider di risorse di archiviazione [SRP](working-with-srp.md). Le scelte consigliate sono:

* [DSRP - Provider risorsa di archiviazione database relazionale](dsrp.md)
* [MSRP - Provider risorsa di archiviazione MongoDB](msrp.md)
* [ASRP - Provider risorsa di archiviazione Adobe](asrp.md)

Un&#39;altra opzione SRP, [JSRP - Provider risorsa di archiviazione JCR](jsrp.md), non supporta un archivio UGC comune per gli ambienti di authoring e pubblicazione per accedere a entrambi.

La richiesta di un archivio comune determina le seguenti topologie consigliate.

>[!NOTE]
>
>Per AEM Communities, [UGC non viene mai replicato](working-with-srp.md#ugc-never-replicated).
>
>Se la distribuzione non include un [archivio comune](working-with-srp.md), UGC sarà visibile solo nell&#39;istanza di pubblicazione o di authoring dell&#39;AEM in cui è stato immesso.
>

>[!NOTE]
>
>Per ulteriori informazioni sulla piattaforma AEM, vedere [Distribuzioni consigliate](../../help/sites-deploying/recommended-deploys.md) e [Introduzione alla piattaforma AEM](../../help/sites-deploying/data-store-config.md).

## Per la produzione {#for-production}

La creazione di un archivio comune per i contenuti generati dagli utenti (UGC, Common Store) è essenziale, pertanto la distribuzione sottostante dipende dalla sua capacità di supportare un archivio comune.

Due esempi:

1. Se il volume previsto di UGC è elevato ed è possibile un&#39;istanza MongoDB locale, la scelta sarà [MSRP](msrp.md).

1. Per prestazioni ottimali per il contenuto della pagina, la scelta di una [farm di pubblicazione](../../help/sites-deploying/recommended-deploys.md#tarmk-farm) e [ASRP](asrp.md) fornirebbe una scalabilità ottimale di UGC con operazioni relativamente semplici.

Per entrambi, la distribuzione può essere basata su qualsiasi microkernel OAK.

Per scegliere l&#39;archivio comune appropriato, considerare attentamente le [caratteristiche](working-with-srp.md#characteristics-of-srp-options) univoche di ciascuna.

Per ulteriori dettagli sui microkernel di Oak, visita [Distribuzioni consigliate](../../help/sites-deploying/recommended-deploys.md).

### Farm Publish TarMK {#tarmk-publish-farm}

Quando la topologia è una farm di pubblicazione, gli argomenti rilevanti sono:

* [Sincronizzazione utente](sync.md)
* [Gestione di utenti e gruppi di utenti](users.md)

### Consigliato: DSRP, MSRP o ASRP {#recommended-dsrp-msrp-or-asrp}

| MicroKernel | ARCHIVIO CONTENUTO SITO | ARCHIVIO CONTENUTI GENERATO DALL&#39;UTENTE | PROVIDER RISORSA DI ARCHIVIAZIONE | ARCHIVIO COMUNE |
|-------------|------------------------|----------------------------------|---------------------------|---------------|
| qualsiasi | JCR | MySQL | DSRP | Sì |
| qualsiasi | JCR | MongoDB | MSRP | Sì |
| qualsiasi | JCR | Adobe di storage on-demand | ASRP | Sì |

### JSRP {#jsrp}


| Distribuzione | ARCHIVIO CONTENUTO SITO | ARCHIVIO CONTENUTI GENERATO DALL&#39;UTENTE | PROVIDER RISORSA DI ARCHIVIAZIONE | ARCHIVIO COMUNE |
|----------------------|------------------------|----------------------------------|---------------------------|---------------------------------|
| Farm TarMK (impostazione predefinita) | JCR | JCR | JSRP | No |
| Cluster Oak | JCR | JCR | JSRP | Sì solo per l’ambiente di pubblicazione |

## Per lo sviluppo {#for-development}

Per gli ambienti non di produzione, [JSRP](jsrp.md) fornisce semplicità nella configurazione di un ambiente di sviluppo con un&#39;istanza di authoring e un&#39;istanza di pubblicazione.

Se si sceglie [ASRP](asrp.md), [DSRP](dsrp.md) o [MSRP](msrp.md) per la produzione, è anche possibile impostare un ambiente di sviluppo simile utilizzando l&#39;archiviazione Adobe on-demand o MongoDB. Per un esempio, vedere [Come configurare MongoDB per Demo](demo-mongo.md).

## Riferimenti {#references}

* [Sincronizzazione utente](sync.md)

  Descrive la sincronizzazione dei dati utente tra le istanze della farm di pubblicazione.

* [Gestione di utenti e gruppi di utenti](users.md)

  Descrive i ruoli degli utenti e dei gruppi di utenti negli ambienti di authoring e pubblicazione.

* [archivio comune](working-with-srp.md) UGC

  Descrive l&#39;archiviazione del contenuto della community separata dal contenuto del sito.

* [Archivi nodi e archivi dati](../../help/sites-deploying/data-store-config.md)

  In pratica, il contenuto del sito viene memorizzato in un archivio nodi. Per Assets, è possibile configurare un archivio dati per l’archiviazione di dati binari. Per le community, è necessario configurare un archivio comune per selezionare l&#39;SRP.

* [Elementi di archiviazione](../../help/sites-deploying/storage-elements-in-aem-6.md)

  Descrive le implementazioni di archiviazione a due nodi: Tar e MongoDB.
