---
title: Topologie consigliate per community
seo-title: Recommended Topologies for Communities
description: Come approcciare la gestione dei contenuti generati dall’utente (UGC)
seo-description: How to approach the handling of user-generated content (UGC)
uuid: 4bc1c423-0ba9-4f2e-b11c-4d6824f45641
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: 46f135de-a0bf-451d-bdcc-fb29188250aa
exl-id: b6658330-d862-44e3-aac0-824fb91cd087
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 1%

---

# Topologie consigliate per community {#recommended-topologies-for-communities}

A partire da AEM Communities 6.1, è stato adottato un approccio univoco per la gestione dei contenuti generati dagli utenti (UGC) inviati dai visitatori del sito (membri) dall’ambiente di pubblicazione.

Questo approccio è fondamentalmente diverso dal modo in cui la piattaforma AEM gestisce il contenuto del sito generalmente gestito dall’ambiente di authoring.

La piattaforma AEM utilizza un archivio nodi che replica il contenuto del sito dall’autore alla pubblicazione, mentre AEM Communities utilizza un singolo archivio comune per UGC che non viene mai replicato.

Per l&#39;archivio UGC comune, è necessario scegliere un [provider di risorse di archiviazione (SRP)](working-with-srp.md). Le scelte consigliate sono:

* [DSRP - Provider risorsa di archiviazione database relazionale](dsrp.md)
* [MSRP - Provider risorsa di archiviazione MongoDB](msrp.md)
* [ASRP - Provider risorsa di archiviazione Adobe](asrp.md)

Un&#39;altra opzione SRP, [JSRP - Provider risorsa di archiviazione JCR](jsrp.md), non supporta un archivio UGC comune per gli ambienti di authoring e pubblicazione per entrambi gli accessi.

Se si richiede un archivio comune, si ottengono le seguenti topologie consigliate.

>[!NOTE]
>
>Per AEM Communities, [UGC non viene mai replicato](working-with-srp.md#ugc-never-replicated).
>
>Quando la distribuzione non include un [negozio comune](working-with-srp.md), UGC sarà visibile solo sull’istanza di pubblicazione o authoring AEM in cui è stato inserito.

>[!NOTE]
>
>Per ulteriori informazioni sulla piattaforma AEM, consulta [Implementazioni consigliate](../../help/sites-deploying/recommended-deploys.md) e [Introduzione alla piattaforma AEM](../../help/sites-deploying/data-store-config.md).

## Per la produzione {#for-production}

La creazione di un archivio comune per UGC è essenziale, e quindi la distribuzione sottostante dipende dalla sua capacità di supportare un negozio comune.

Due esempi:

1. Se il volume previsto dell&#39;UGC è alto e un&#39;istanza MongoDB locale è possibile, allora la scelta sarebbe [MSRP](msrp.md).

1. Per prestazioni ottimali per il contenuto della pagina, è possibile scegliere un [pubblica azienda](../../help/sites-deploying/recommended-deploys.md#tarmk-farm) e [ASRP](asrp.md) fornirebbe una scala ottimale di UGC con operazioni relativamente semplici.

Per entrambi, la distribuzione può essere basata su qualsiasi microkernel OAK.

Per scegliere il negozio comune appropriato, considerare attentamente l&#39;unico [caratteristiche](working-with-srp.md#characteristics-of-srp-options) di ciascuno.

Per maggiori dettagli sui microkernals Oak, visita [Implementazioni consigliate](../../help/sites-deploying/recommended-deploys.md).

### TarMK Publish Farm {#tarmk-publish-farm}

Quando la topologia è un’azienda di pubblicazione, gli argomenti rilevanti sono:

* [Sincronizzazione utente](sync.md)
* [Gestione di utenti e gruppi di utenti](users.md)

### Consigliato: DSRP, MSRP o ASRP {#recommended-dsrp-msrp-or-asrp}

| MicroKernel | CONTENUTO DEL SITO | CONTENUTO GENERATO DALL&#39;UTENTE | FORNITORE DI RISORSE DI STORAGE | NEGOZIO COMUNE |
|-------------|------------------------|----------------------------------|---------------------------|---------------|
| qualsiasi | JCR | MySQL | DSRP | Sì |
| qualsiasi | JCR | MongoDB | MSRP | Sì |
| qualsiasi | JCR | Adobe di archiviazione su richiesta | ASRP | Sì |

### JSRP {#jsrp}


| Distribuzione | CONTENUTO DEL SITO | CONTENUTO GENERATO DALL&#39;UTENTE | FORNITORE DI RISORSE DI STORAGE | NEGOZIO COMUNE |
|----------------------|------------------------|----------------------------------|---------------------------|---------------------------------|
| Farm TarMK (predefinito) | JCR | JCR | JSRP | No |
| Cluster Oak | JCR | JCR | JSRP | Sì solo per ambiente di pubblicazione |

## Per lo sviluppo {#for-development}

Per ambienti non di produzione, [JSRP](jsrp.md) fornisce semplicità nella configurazione di un ambiente di sviluppo con un’istanza di authoring e un’istanza di pubblicazione.

Se si sceglie [ASRP](asrp.md), [DSRP](dsrp.md) o [MSRP](msrp.md) per la produzione, è anche possibile impostare un ambiente di sviluppo simile utilizzando Adobe on-demand storage o MongoDB. Ad esempio, vedi [Come impostare MongoDB per la demo](demo-mongo.md).

## Riferimenti {#references}

* [Sincronizzazione utente](sync.md)

   Descrive la sincronizzazione dei dati utente tra le istanze farm di pubblicazione.

* [Gestione di utenti e gruppi di utenti](users.md)

   Illustra i ruoli degli utenti e dei gruppi di utenti negli ambienti di creazione e pubblicazione.

* UGC [negozio comune](working-with-srp.md)

   Descrive l&#39;archiviazione dei contenuti della community separati dal contenuto del sito.

* [Archivi di nodi e archivi di dati](../../help/sites-deploying/data-store-config.md)

   In sostanza, il contenuto del sito viene memorizzato in un archivio nodi. Per Assets, è possibile configurare un archivio dati per memorizzare dati binari. Per Communities, è necessario configurare un archivio comune per selezionare l’SRP.

* [Elementi di storage](../../help/sites-deploying/storage-elements-in-aem-6.md)

   Descrive le implementazioni di archiviazione a due nodi: Tar e MongoDB.
