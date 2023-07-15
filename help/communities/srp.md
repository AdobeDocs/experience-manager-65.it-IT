---
title: Panoramica del provider di risorse di archiviazione
description: Archiviazione comune per community
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 5f313274-1a2a-4e83-9289-60a4729b99b4
source-git-commit: e161c37544c3391607cbe495644f3353b9f77fe3
workflow-type: tm+mt
source-wordcount: '1125'
ht-degree: 0%

---

# Panoramica del provider di risorse di archiviazione {#storage-resource-provider-overview}

## Introduzione {#introduction}

A partire da Adobe Experience Manager (AEM) Communities 6.1, i contenuti community, comunemente denominati contenuti generati dagli utenti (UGC, User-Generated Content), sono memorizzati in un unico archivio comune fornito da un [provider di risorse di archiviazione](working-with-srp.md) (SRP)

Esistono diverse opzioni SRP, tutte accessibili da UGC tramite una nuova interfaccia AEM Communities, la [API SocialResourceProvider](srp-and-ugc.md) (API SRP), che include tutte le operazioni di creazione, lettura, aggiornamento ed eliminazione (CRUD).

Tutti i componenti SCF vengono implementati utilizzando l’API SRP, consentendo lo sviluppo del codice senza la conoscenza di [topologia sottostante](topologies.md) o la posizione dell&#39;UGC.

***L’API SocialResourceProvider è disponibile solo per i clienti con licenza di AEM Communities.***

>[!NOTE]
>
>**Componenti personalizzati**: per i clienti con licenza di AEM Communities, l’API SRP è disponibile per gli sviluppatori di componenti personalizzati per l’accesso a UGC, indipendentemente dalla topologia sottostante. Consulta [Nozioni di base su SRP e UGC](srp-and-ugc.md).

Consulta anche:

* [Nozioni di base su SRP e UGC](srp-and-ugc.md) - Metodi ed esempi di utilità SRP.
* [Accesso a UGC con SRP](accessing-ugc-with-srp.md) - Linee guida per la codifica.
* [Refactoring SocialUtils](socialutils.md) - Mappatura dei metodi di utilità obsoleti sui metodi di utilità SRP correnti.

## Informazioni sull’archivio {#about-the-repository}

Per comprendere la SRP, è utile comprendere il ruolo dell’archivio dell’AEM (Oak) in un sito della community dell’AEM.

**Java™ Content Repository (JCR)**
Questo standard definisce un modello dati e un&#39;interfaccia di programmazione dell&#39;applicazione ([API JCR](https://jackrabbit.apache.org/jcr/jcr-api.html)) per gli archivi di contenuti. Combina le caratteristiche dei file system convenzionali con quelle dei database relazionali e aggiunge diverse funzioni aggiuntive di cui le applicazioni di contenuti hanno spesso bisogno.

Un’implementazione del JCR è l’archivio dell’AEM, Oak.

**Apache Jackrabbit Oak**
[Oak](../../help/sites-deploying/platform.md) è un’implementazione di JCR 2.0, un sistema di storage dei dati progettato per applicazioni incentrate sui contenuti. Si tratta di un tipo di database gerarchico progettato per i dati non strutturati e semistrutturati. L’archivio memorizza non solo il contenuto rivolto all’utente, ma anche tutto il codice, i modelli e i dati interni utilizzati dall’applicazione. L’interfaccia utente per l’accesso al contenuto è [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md).

Sia JCR che Oak vengono in genere utilizzati per fare riferimento all’archivio AEM.

Dopo aver sviluppato il contenuto del sito nell’ambiente di authoring privato, deve essere copiato nell’ambiente di pubblicazione pubblico. Questo viene spesso fatto attraverso un&#39;operazione chiamata *[replica](deploy-communities.md#replication-agents-on-author)*. Questo accade sotto il controllo dell’autore/sviluppatore/amministratore.

Per UGC, il contenuto viene immesso dai visitatori del sito registrati (membri della community) nell’ambiente di pubblicazione pubblico. Questo succede in modo casuale.

A scopo di gestione e reporting, è utile avere accesso a UGC dall’ambiente di authoring privato. Con SRP, l’accesso a UGC da Author è più coerente ed efficiente, in quanto non è necessaria la replica inversa da Publish a Author.

## Informazioni su SRP {#about-srp}

Quando UGC viene salvato nello storage condiviso, esiste una singola istanza di contenuto membro a cui è possibile accedere, nella maggior parte delle implementazioni, sia dagli ambienti di authoring che da quelli di pubblicazione. Indipendentemente dalla scelta SRP (MSRP, ASRP, JSRP), tutto deve essere accessibile a livello di programmazione con l’API SRP.

>[!NOTE]
>
>Consulta [Nozioni di base su SRP e UGC](srp-and-ugc.md) per il codice di esempio e ulteriori dettagli.
>
>Consulta [Accesso a UGC con SRP](accessing-ugc-with-srp.md) per best practice durante la codifica.

### ASRP {#asrp}

Se è presente ASRP, UGC non viene memorizzato in JCR, ma in un servizio cloud ospitato e gestito da Adobe. Le UGC memorizzate in ASRP potrebbero non essere visualizzate con CRXDE Lite o non essere accessibili utilizzando l’API JCR.

Consulta [ASRP - Provider risorsa di archiviazione Adobe](asrp.md).

Non è possibile per gli sviluppatori accedere direttamente all’UGC.

ASRP utilizza Adobe Cloud per le query.

### MSRP {#msrp}

Se è presente, MSRP, UGC non è memorizzato in JCR, ma in MongoDB. Le UGC memorizzate in MSRP potrebbero non essere visualizzate con CRXDE Lite o non essere accessibili utilizzando l’API JCR.

Consulta [MSRP - Provider risorsa di archiviazione MongoDB](msrp.md).

Anche se MSRP è paragonabile ad ASRP, poiché tutte le istanze del server AEM accedono allo stesso UGC, è possibile utilizzare strumenti comuni per accedere direttamente al UGC memorizzato in MongoDB.

MSRP utilizza Solr per le query.

### JSRP {#jsrp}

JSRP è il provider predefinito per l’accesso a tutti i contenuti generati dagli utenti su una singola istanza AEM. Consente di utilizzare rapidamente AEM Communities 6.1 senza la necessità di configurare MSRP o ASRP.

Consulta [JSRP - Provider risorsa di archiviazione JCR](jsrp.md).

Se è presente JSRP, mentre UGC è memorizzato in JCR e accessibile tramite l’API CRXDE Lite e JCR, si consiglia di non utilizzare mai l’API JCR per farlo, altrimenti le modifiche future potrebbero influenzare il codice personalizzato.

Inoltre, l’archivio per gli ambienti di authoring e pubblicazione non è condiviso. Anche se un cluster di istanze di pubblicazione genera un archivio di pubblicazione condiviso, l’UGC immesso al momento della pubblicazione non sarà visibile nell’autore, pertanto non sarà possibile gestire l’UGC dall’autore. L’UGC viene mantenuto solo nell’archivio AEM (JCR) dell’istanza in cui è stato inserito.

JSRP utilizza gli indici Oak per le query.

## Informazioni sui nodi ombra in JCR {#about-shadow-nodes-in-jcr}

I nodi shadow, che imitano il percorso di UGC, esistono nell’archivio locale per due scopi:

1. [Controllo degli accessi (ACL)](#for-access-control-acls)
1. [Risorse non esistenti (NER)](#for-non-existing-resources-ners)

Indipendentemente dall’implementazione SRP, l’UGC effettivo *non *sarà visibile nella stessa posizione del nodo ombra.

### Per il controllo degli accessi (ACL) {#for-access-control-acls}

Alcune implementazioni SRP, come ASRP e MSRP, memorizzano il contenuto della community in database che non forniscono alcuna verifica ACL. I nodi shadow forniscono una posizione nell’archivio locale a cui possono essere applicati gli ACL.

Utilizzando l&#39;API SRP, tutte le opzioni SRP eseguono lo stesso controllo della posizione ombra prima di tutte le operazioni CRUD.

Il controllo ACL utilizza un metodo di utilità che restituisce un percorso adatto per la verifica delle autorizzazioni applicate all’UGC della risorsa.

Consulta [Nozioni di base su SRP e UGC](srp-and-ugc.md) per il codice di esempio.

### Per le risorse non esistenti (NER) {#for-non-existing-resources-ners}

Alcuni componenti di Communities sono inclusi in uno script e quindi richiedono un nodo indirizzabile Sling per supportare le funzioni di Communities. [Componenti inclusi](scf.md#add-or-include-a-communities-component) sono denominate risorse non esistenti (NER).

I nodi shadow forniscono una posizione indirizzabile Sling nell’archivio.

>[!CAUTION]
>
>Poiché il nodo ombra ha più utilizzi, la presenza di un nodo ombra *non* implica che il componente è un NER.

### Percorso di archiviazione {#storage-location}

Di seguito è riportato un esempio di nodo ombra che utilizza [Componente Commenti](http://localhost:4502/content/community-components/en/comments.html) nel [Guida ai componenti della community](components-guide.md):

* Il componente esiste nell’archivio locale in:

  `/content/community-components/en/comments/jcr:content/content/includable/comments`

* Il nodo shadow corrispondente esiste nell’archivio locale in:

  `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

Nessun UGC trovato nel nodo shadow.

Il comportamento predefinito consiste nell’impostare nodi shadow in un’istanza Publish ogni volta che si fa riferimento alla sottostruttura pertinente per una lettura o una scrittura.

Ad esempio, supponiamo che la distribuzione sia [MSRP](msrp.md) con una farm di pubblicazione TarMK.

Quando un [membro](users.md) post UGC su pub1 (memorizzato in MongoDB), i nodi ombra vengono creati in JCR su pub1.

La prima volta che l&#39;UGC viene letto su pub2, se non viene configurato nulla, il comportamento predefinito consiste nel creare i nodi ombra.

Per un comportamento diverso da quello predefinito, è necessario impostarlo sull’istanza di authoring e riportarlo a tutte le istanze di pubblicazione, solitamente un processo manuale.
