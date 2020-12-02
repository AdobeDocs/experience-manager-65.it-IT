---
title: Panoramica del provider di risorse di storage
seo-title: Panoramica del provider di risorse di storage
description: Archiviazione comune per Community
seo-description: Archiviazione comune per Community
uuid: abdf4e5a-767b-428f-9aa4-0dc06819a26e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 63abeda4-6ea1-4b45-b188-f9c6b44ca0cd
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 0%

---


# Panoramica del provider di risorse di storage {#storage-resource-provider-overview}

## Introduzione {#introduction}

A partire  AEM Communities 6.1, il contenuto della community, comunemente denominato contenuto generato dall&#39;utente (UGC), viene memorizzato in un unico store comune fornito da un [provider di risorse di storage](working-with-srp.md) (SRP).

Esistono diverse opzioni SRP, tutte con accesso a UGC tramite una nuova interfaccia AEM Communities , l&#39;API [SocialResourceProvider](srp-and-ugc.md) (API SRP), che include tutte le operazioni di creazione, lettura, aggiornamento ed eliminazione (CRUD).

Tutti i componenti SCF sono implementati utilizzando l&#39;API SRP, consentendo lo sviluppo del codice senza conoscere la [topologia sottostante](topologies.md) o la posizione dell&#39;UGC.

***L&#39;API SocialResourceProvider è disponibile solo per i clienti autorizzati di  AEM Communities.***

>[!NOTE]
>
>**Componenti** personalizzati: Per i clienti con licenza di  AEM Communities, l&#39;API SRP è disponibile per gli sviluppatori di componenti personalizzati allo scopo di accedere a UGC senza riguardo alla topologia sottostante. Vedere [SRP e UGC Essentials](srp-and-ugc.md).

Consulta anche:

* [SRP e UGC Essentials](srp-and-ugc.md)  - Metodi e esempi di utilità SRP.
* [Accesso a UGC con linee guida SRP](accessing-ugc-with-srp.md) - Codifica.
* [Refactoring](socialutils.md)  SocialUtils - Mappatura di metodi di utilità obsoleti ai metodi di utilità SRP correnti.

## Informazioni sul repository {#about-the-repository}

Per comprendere meglio SRP, è utile comprendere il ruolo del repository AEM (OAK) in un sito AEM community.

**Java Content Repository (JCR)**
Questo standard definisce un modello dati e un&#39;interfaccia di programmazione applicazione (API[ ](https://jackrabbit.apache.org/jcr/jcr-api.html)JCR) per i repository dei contenuti. Unisce le caratteristiche dei file system convenzionali a quelle dei database relazionali e aggiunge una serie di funzioni aggiuntive spesso necessarie per le applicazioni di contenuto.

Un&#39;implementazione di JCR è il repository AEM, OAK.

**Apache Jackrabbit Oak (OAK)**
[](../../help/sites-deploying/platform.md) OAK è un&#39;implementazione di JCR 2.0 che è un sistema di storage dei dati appositamente progettato per applicazioni incentrate sui contenuti. È un tipo di database gerarchico progettato per dati non strutturati e semi-strutturati. L&#39;archivio memorizza non solo il contenuto rivolto all&#39;utente, ma anche tutto il codice, i modelli e i dati interni utilizzati dall&#39;applicazione. L&#39;interfaccia utente per accedere ai contenuti è [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md).

Sia JCR che OAK sono generalmente utilizzati per fare riferimento al repository AEM.

Dopo aver sviluppato il contenuto del sito nell’ambiente di authoring privato, questo deve essere copiato nell’ambiente di pubblicazione pubblica. Questa operazione viene spesso eseguita tramite un&#39;operazione denominata *[replica](deploy-communities.md#replication-agents-on-author)*. Ciò avviene sotto il controllo dell&#39;autore/sviluppatore/amministratore.

Per UGC, il contenuto è immesso dai visitatori registrati del sito (membri della community) nell&#39;ambiente di pubblicazione pubblica. Questo succede in modo casuale.

Ai fini della gestione e del reporting, è utile avere accesso a UGC dall’ambiente di authoring privato. Con SRP, l’accesso a UGC dall’autore è più coerente e performante, in quanto non è necessaria la replica inversa dalla pubblicazione all’autore.

## Informazioni su SRP {#about-srp}

Quando UGC viene salvato nello storage condiviso, esiste un&#39;unica istanza di contenuto membro a cui, nella maggior parte delle distribuzioni, è possibile accedere sia dall&#39;ambiente di creazione che da quello di pubblicazione. Indipendentemente dalla scelta SRP (MSRP, ASRP, JSRP), l&#39;accesso a tutti deve essere programmaticamente effettuato con l&#39;API SRP.

>[!NOTE]
>
>Vedere [SRP e UGC Essentials](srp-and-ugc.md) per il codice di esempio e ulteriori dettagli.
>
>Per le procedure ottimali per la codifica, vedere [Accesso a UGC con SRP](accessing-ugc-with-srp.md).

### ASRP {#asrp}

Nel caso di ASRP, UGC non è memorizzato in JCR, è memorizzato in un servizio cloud ospitato e gestito da  Adobe. L&#39;UGC memorizzato in ASRP non può essere visualizzato né con CRXDE Lite né accessibile tramite l&#39;API JCR.

Vedere [ASRP -  provider di risorse di storage di Adobe](asrp.md).

Gli sviluppatori non possono accedere direttamente all&#39;UGC.

ASRP utilizza  Adobe cloud per le query.

### MSRP {#msrp}

Nel caso di MSRP, UGC non è memorizzato in JCR, è memorizzato in MongoDB. L&#39;UGC memorizzato in MSRP non può essere visualizzato né con CRXDE Lite né accessibile tramite l&#39;API JCR.

Vedere [MSRP - Provider di risorse di storage MongoDB](msrp.md).

Sebbene MSRP sia paragonabile ad ASRP, poiché tutte AEM istanze server accedono allo stesso UGC, è possibile utilizzare strumenti comuni per accedere direttamente all&#39;UGC memorizzato in MongoDB.

MSRP utilizza Solr per le query.

### JSRP {#jsrp}

JSRP è il provider predefinito per l&#39;accesso a tutti gli UGC su una singola istanza AEM. Fornisce la possibilità di sperimentare rapidamente  AEM Communities 6.1 senza la necessità di configurare MSRP o ASRP.

Vedere [JSRP - Provider di risorse di storage JCR](jsrp.md).

Nel caso di JSRP, mentre UGC è memorizzato in JCR, e accessibile tramite API CRXDE Lite e JCR, è fortemente consigliato che l&#39;API JCR non venga mai utilizzata per farlo, altrimenti le modifiche future potrebbero influenzare il codice personalizzato.

Inoltre, l’archivio per gli ambienti di creazione e pubblicazione non è condiviso. Mentre un cluster di istanze di pubblicazione genera un archivio condiviso di pubblicazione, gli UGC immessi al momento della pubblicazione non saranno visibili all’autore, per cui non è possibile gestire UGC dall’autore. UGC è persistente solo nell&#39;archivio AEM (JCR) dell&#39;istanza in cui è stato immesso.

JSRP utilizza gli indici Oak per le query.

## Informazioni sui nodi ombra in JCR {#about-shadow-nodes-in-jcr}

I nodi shadow, che imitano il percorso dell&#39;UGC, esistono nell&#39;archivio locale per due scopi:

1. [Controllo degli accessi (ACL)](#for-access-control-acls)
1. [Risorse non esistenti (NER)](#for-non-existing-resources-ners)

Indipendentemente dall&#39;implementazione SRP, l&#39;UGC effettivo *non sarà visibile nella stessa posizione del nodo ombra.

### Per il controllo degli accessi (ACL) {#for-access-control-acls}

Alcune implementazioni SRP, come ASRP e MSRP, memorizzano il contenuto della community in database che non forniscono alcuna verifica ACL. I nodi shadow forniscono una posizione nell&#39;archivio locale in cui è possibile applicare gli ACL.

Utilizzando l&#39;API SRP, tutte le opzioni SRP eseguono lo stesso controllo della posizione dell&#39;ombra prima di tutte le operazioni CRUD.

Il controllo ACL utilizza un metodo di utilità che restituisce un percorso adatto per verificare le autorizzazioni applicate all&#39;UGC della risorsa.

Per un esempio di codice, vedere [SRP e UGC Essentials](srp-and-ugc.md).

### Per risorse non esistenti (NER) {#for-non-existing-resources-ners}

Alcuni componenti Community sono inclusi in uno script e richiedono quindi un nodo indirizzabile Sling per supportare le funzioni Community. [I ](scf.md#add-or-include-a-communities-component) componenti inclusi sono denominati risorse non esistenti (NER).

I nodi shadow forniscono una posizione indirizzabile Sling nella directory archivio.

>[!CAUTION]
>
>Poiché il nodo ombra ha più usi, la presenza di un nodo ombra *non* implica che il componente sia un NER.

### Percorso di archiviazione {#storage-location}

Di seguito è riportato un esempio di un nodo ombra, utilizzando il [componente Commenti](http://localhost:4502/content/community-components/en/comments.html) nella [Guida ai componenti della community](components-guide.md):

* Il componente esiste nell’archivio locale in:

   `/content/community-components/en/comments/jcr:content/content/includable/comments`

* Il nodo shadow corrispondente esiste nel repository locale in:

   `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

Non verrà trovato alcun UGC sotto il nodo shadow.

Il comportamento predefinito consiste nell’impostare i nodi ombra su un’istanza di pubblicazione ogni volta che viene fatto riferimento alla relativa sottostruttura ad albero per una lettura o una scrittura.

Ad esempio, supponiamo che la distribuzione sia [MSRP](msrp.md) con una farm di pubblicazione TarMK.

Quando un [membro](users.md) inserisce UGC su pub1 (memorizzato in MongoDB), i nodi ombra vengono creati in JCR su pub1.

La prima volta che l’UGC viene letto su pub2, se non è impostato nulla, il comportamento predefinito consiste nel creare i nodi ombra.

Se si desidera un comportamento diverso da quello predefinito, è necessario impostarlo sull’istanza di creazione e inoltrarlo a tutte le istanze di pubblicazione, che in genere è un processo manuale.
