---
title: Panoramica del provider di risorse di storage
seo-title: Storage Resource Provider Overview
description: Archiviazione comune per Communities
seo-description: Common storage for Communities
uuid: abdf4e5a-767b-428f-9aa4-0dc06819a26e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 63abeda4-6ea1-4b45-b188-f9c6b44ca0cd
exl-id: 5f313274-1a2a-4e83-9289-60a4729b99b4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 0%

---

# Panoramica del provider di risorse di storage {#storage-resource-provider-overview}

## Introduzione {#introduction}

A partire da AEM Communities 6.1, il contenuto della community, comunemente denominato contenuto generato dall’utente (UGC), viene memorizzato in un singolo archivio comune fornito da un [provider di risorse di archiviazione](working-with-srp.md) (SRP).

Sono disponibili diverse opzioni SRP, tutte con accesso a UGC tramite una nuova interfaccia AEM Communities, la [API SocialResourceProvider](srp-and-ugc.md) (API SRP), che include tutte le operazioni di creazione, lettura, aggiornamento ed eliminazione (CRUD).

Tutti i componenti SCF sono implementati utilizzando l’API SRP, consentendo lo sviluppo del codice senza conoscere né l’API [topologia sottostante](topologies.md) o la posizione dell&#39;UGC.

***L&#39;API SocialResourceProvider è disponibile solo per i clienti con licenza di AEM Communities.***

>[!NOTE]
>
>**Componenti personalizzati**: Per i clienti con licenza di AEM Communities, l’API SRP è disponibile per gli sviluppatori di componenti personalizzati allo scopo di accedere a UGC senza tenere conto della topologia sottostante. Vedi [Essenze SRP e UGC](srp-and-ugc.md).

Consulta anche:

* [Essenze SRP e UGC](srp-and-ugc.md) - Metodi ed esempi di utilità SRP.
* [Accesso a UGC con SRP](accessing-ugc-with-srp.md) - Linee guida per la codifica.
* [Refactoring di SocialUtils](socialutils.md) - Mappatura di metodi di utilità obsoleti ai metodi di utilità SRP correnti.

## Informazioni sull’archivio {#about-the-repository}

Per comprendere l’SRP, è utile comprendere il ruolo dell’archivio AEM (OAK) in un sito della community AEM.

**Java Content Repository (JCR)**
Questo standard definisce un modello dati e un&#39;interfaccia di programmazione dell&#39;applicazione ([API JCR](https://jackrabbit.apache.org/jcr/jcr-api.html)) per gli archivi di contenuti. Combina le caratteristiche dei file system convenzionali con quelle dei database relazionali e aggiunge una serie di funzioni aggiuntive di cui spesso le applicazioni di contenuti hanno bisogno.

Un’implementazione di JCR è l’archivio AEM, OAK.

**Apache Jackrabbit Oak (OAK)**
[OAK](../../help/sites-deploying/platform.md) è un’implementazione di JCR 2.0 che è un sistema di storage dei dati appositamente progettato per applicazioni incentrate sui contenuti. È un tipo di database gerarchico progettato per dati non strutturati e semi-strutturati. Il repository memorizza non solo il contenuto rivolto all&#39;utente, ma anche tutto il codice, i modelli e i dati interni utilizzati dall&#39;applicazione. L’interfaccia utente per accedere ai contenuti è [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md).

Sia JCR che OAK sono generalmente utilizzati per fare riferimento all’archivio AEM.

Dopo aver sviluppato il contenuto del sito nell’ambiente di authoring privato, deve essere copiato nell’ambiente di pubblicazione pubblico. Questa operazione viene spesso eseguita tramite un’operazione denominata *[replica](deploy-communities.md#replication-agents-on-author)*. Questo accade sotto il controllo dell&#39;autore/sviluppatore/amministratore.

Per UGC, il contenuto è inserito dai visitatori registrati del sito (membri della community) nell’ambiente di pubblicazione pubblico. Questo succede in modo casuale.

Ai fini della gestione e del reporting, è utile avere accesso a UGC dall’ambiente di authoring privato. Con l’SRP, l’accesso a UGC dall’autore è più coerente e performante, in quanto la replica inversa da pubblicazione all’autore non è necessaria.

## Informazioni sull’SRP {#about-srp}

Quando UGC viene salvato nello storage condiviso, esiste una singola istanza di contenuto membro a cui è possibile accedere, nella maggior parte delle distribuzioni, sia dagli ambienti di authoring che di pubblicazione. Indipendentemente dalla scelta dell’SRP (MSRP, ASRP, JSRP), è necessario accedere a tutti a livello di programmazione con l’API SRP.

>[!NOTE]
>
>Vedi [Essenze SRP e UGC](srp-and-ugc.md) per codice di esempio e ulteriori dettagli.
>
>Vedi [Accesso a UGC con SRP](accessing-ugc-with-srp.md) per le best practice relative alla codifica.

### ASRP {#asrp}

Nel caso di ASRP, UGC non è memorizzato in JCR, viene memorizzato in un servizio cloud ospitato e gestito da Adobe. Gli UGC memorizzati in ASRP non possono essere visualizzati con CRXDE Lite né utilizzati con l’API JCR.

Vedi [ASRP - Provider risorsa di archiviazione Adobe](asrp.md).

Non è possibile per gli sviluppatori accedere direttamente all’UGC.

ASRP utilizza Adobe cloud per le query.

### MSRP {#msrp}

Nel caso di MSRP, UGC non è memorizzato in JCR, è memorizzato in MongoDB. Gli UGC memorizzati in MSRP non possono essere visualizzati con CRXDE Lite né utilizzati con l’API JCR.

Vedi [MSRP - Provider risorsa di archiviazione MongoDB](msrp.md).

Mentre MSRP è paragonabile ad ASRP, poiché tutte le istanze AEM server stanno accedendo allo stesso UGC, è possibile utilizzare strumenti comuni per accedere direttamente all&#39;UGC memorizzato in MongoDB.

MSRP utilizza Solr per le query.

### JSRP {#jsrp}

JSRP è il provider predefinito per accedere a tutti gli UGC su una singola istanza AEM. Fornisce la possibilità di sperimentare rapidamente AEM Communities 6.1 senza la necessità di configurare MSRP o ASRP.

Vedi [JSRP - Provider risorsa di archiviazione JCR](jsrp.md).

Nel caso di JSRP, mentre UGC è memorizzato in JCR e accessibile tramite sia CRXDE Lite che JCR API, si consiglia vivamente di non utilizzare mai l’API JCR per farlo, altrimenti le modifiche future potrebbero influenzare il codice personalizzato.

Inoltre, l’archivio per gli ambienti di authoring e pubblicazione non è condiviso. Mentre un cluster di istanze di pubblicazione genera un archivio di pubblicazione condiviso, l&#39;UGC immesso al momento della pubblicazione non sarà visibile sull&#39;autore, quindi non è possibile gestire l&#39;UGC dall&#39;autore. UGC viene mantenuto solo nell’archivio AEM (JCR) dell’istanza in cui è stato inserito.

JSRP utilizza gli indici Oak per le query.

## Informazioni sui nodi ombra in JCR {#about-shadow-nodes-in-jcr}

I nodi shadow, che imitano il percorso dell&#39;UGC, esistono nell&#39;archivio locale per due scopi:

1. [Controllo degli accessi (ACL)](#for-access-control-acls)
1. [Risorse non esistenti (NER)](#for-non-existing-resources-ners)

Indipendentemente dall&#39;implementazione SRP, l&#39;UGC effettivo *non *sarà visibile nella stessa posizione del nodo ombra.

### Per controllo accessi (ACL) {#for-access-control-acls}

Alcune implementazioni SRP, come ASRP e MSRP, memorizzano il contenuto della community nei database che non forniscono alcuna verifica ACL. I nodi shadow forniscono una posizione nell&#39;archivio locale a cui possono essere applicate le ACL.

Utilizzando l’API SRP, tutte le opzioni SRP eseguono lo stesso controllo della posizione shadow prima di tutte le operazioni CRUD.

Il controllo ACL utilizza un metodo di utilità che restituisce un percorso adatto per controllare le autorizzazioni applicate all&#39;UGC della risorsa.

Vedi [Essenze SRP e UGC](srp-and-ugc.md) per codice di esempio.

### Per risorse non esistenti (NER) {#for-non-existing-resources-ners}

Alcuni componenti di Communities sono inclusi all&#39;interno di uno script e quindi richiedono un nodo indirizzabile Sling per supportare le funzioni di Communities. [Componenti inclusi](scf.md#add-or-include-a-communities-component) sono definite risorse non esistenti (NER).

I nodi shadow forniscono una posizione indirizzabile Sling nell&#39;archivio.

>[!CAUTION]
>
>Poiché il nodo di ombreggiatura ha più utilizzi, la presenza di un nodo di ombreggiatura *not* implicare che il componente è un NER.

### Percorso di archiviazione {#storage-location}

Di seguito è riportato un esempio di nodo shadow, utilizzando [Componente Commenti](http://localhost:4502/content/community-components/en/comments.html) in [Guida ai componenti della community](components-guide.md):

* Il componente esiste nell’archivio locale in:

   `/content/community-components/en/comments/jcr:content/content/includable/comments`

* Il nodo shadow corrispondente esiste nell&#39;archivio locale in:

   `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

Non verrà trovato alcun UGC sotto il nodo ombra.

Il comportamento predefinito consiste nell’impostare i nodi shadow in un’istanza di pubblicazione ogni volta che si fa riferimento alla relativa sottostruttura per una lettura o scrittura.

Ad esempio, supponiamo che la distribuzione sia [MSRP](msrp.md) con una farm di pubblicazione TarMK.

Quando un [membro](users.md) post UGC su pub1 (memorizzato in MongoDB), i nodi shadow vengono creati in JCR su pub1.

La prima volta che l&#39;UGC viene letto su pub2, se non è impostato nulla, il comportamento predefinito è quello di creare i nodi shadow.

Se desideri un comportamento diverso da quello predefinito, devi configurarlo nell’istanza di authoring e inoltrarlo a tutte le istanze di pubblicazione, che in genere è un processo manuale.
