---
title: Implementazioni consigliate
seo-title: Implementazioni consigliate
description: Questo articolo descrive le topologie consigliate per AEM.
seo-description: Questo articolo descrive le topologie consigliate per AEM.
uuid: bc638121-c531-43eb-9ec6-3283a33519f8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 66d351e1-87f1-4006-bf8a-3cbbd33db9ed
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Implementazioni consigliate{#recommended-deployments}

>[!NOTE]
>
>Questa pagina fa riferimento alle topologie consigliate per AEM. Per ulteriori informazioni sulle funzionalità di clustering e su come configurarle, consulta la documentazione [di](https://sling.apache.org/documentation/bundles/discovery-api-and-impl.html)Apache Sling Discovery API.

I microkernel agiscono come persistence manager a partire da AEM 6.2. La scelta di uno per soddisfare le esigenze dipende dallo scopo dell&#39;istanza e dal tipo di distribuzione che si sta considerando.

Gli esempi seguenti rappresentano un&#39;indicazione degli usi consigliati nelle impostazioni AEM più comuni.

## Scenari di distribuzione {#deployment-scenarios}

### Istanza TarMK singola {#single-tarmk-instance}

In questo scenario, una singola istanza TarMK viene eseguita su un singolo server.

**Si tratta della distribuzione predefinita per le istanze di creazione.**

![chlimage_1-15](assets/chlimage_1-15.png)

I vantaggi:

* Semplici
* Manutenzione semplice
* Buona prestazione

Gli svantaggi:

* Non scalabile oltre i limiti di capacità del server
* Nessuna capacità di failover

### TarMK Cold Standby {#tarmk-cold-standby}

Un&#39;istanza TarMK agisce come istanza principale. L&#39;archivio dal primario viene replicato in un sistema di failover in standby.

Il meccanismo di standby a freddo può essere utilizzato anche come backup perché il repository completo viene costantemente replicato nel server di failover. Il server di failover è in esecuzione in modalità standby a freddo, il che significa che è in esecuzione solo l&#39;HttpReceiver dell&#39;istanza.

![chlimage_1-16](assets/chlimage_1-16.png)

I vantaggi:

* Semplicità
* Manutenzione
* Spettacolo
* Failover

Gli svantaggi:

* Non scalabile oltre i limiti della capacità del server
* Un server è inattivo nella maggior parte dei casi
* Il failover non è automatico. Deve essere rilevato esternamente prima che il sistema di failover possa avviare la trasmissione delle richieste.

>[!NOTE]
>
>Per ulteriori informazioni su come configurare AEM con TarMK Cold Standby, consulta [questo](/help/sites-deploying/tarmk-cold-standby.md) articolo.

>[!NOTE]
>
>La distribuzione di Cold Standby in questo esempio TarMK richiede che sia le istanze primarie che quelle in standby siano autorizzate separatamente, in quanto è presente una replica costante del server di failover. Per ulteriori informazioni sulle licenze, consultare i Termini [generali di licenza di](https://www.adobe.com/legal/terms/enterprise-licensing.html)Adobe.

### Agriturismo TarMK {#tarmk-farm}

Più istanze Oak vengono eseguite ciascuna con un&#39;istanza TarMK. I repository TarMK sono indipendenti e devono essere mantenuti sincronizzati.

La sincronizzazione dei repository viene fornita con il fatto che il server di creazione pubblica lo stesso contenuto per ogni membro della farm. For more information, see [Replication](/help/sites-deploying/replication.md).

Per AEM Communities, il contenuto generato dall&#39;utente (UGC) non viene mai replicato. Per il supporto di UGC su una farm TarMK, consultate [Considerazioni per AEM Communities](#considerations-for-aem-communities).

**Questa è la distribuzione predefinita per gli ambienti di pubblicazione.**

![chlimage_1-17](assets/chlimage_1-17.png)

I vantaggi:

* Spettacolo
* Scalabilità per accesso in lettura
* Failover

### Cluster Oak con failover MongoMK per un&#39;elevata disponibilità in un singolo datacenter {#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter}

Questo approccio implica l&#39;accesso di più istanze Oak a un set di repliche MongoDB all&#39;interno di un singolo centro dati, in effetti la creazione di un cluster attivo per l&#39;ambiente di creazione AEM. I set di replica in MongoDB vengono utilizzati per fornire elevata disponibilità e ridondanza in caso di guasto dell&#39;hardware o della rete.

![chlimage_1-18](assets/chlimage_1-18.png)

I vantaggi:

* Scalabilità orizzontale con le nuove istanze di creazione di AEM
* Elevata disponibilità, ridondanza e failover automatizzato del livello dati

Gli svantaggi:

* Le prestazioni possono essere inferiori a quelle con TarMK per alcuni scenari

### Cluster Oak con failover MongoMK tra più datacenter {#oak-cluster-with-mongomk-failover-across-multiple-datacenters}

Questo approccio implica l&#39;accesso di più istanze Oak a un set di repliche MongoDB attraverso più centri dati, in effetti creando un cluster attivo per l&#39;ambiente di creazione AEM. Con più data center, la replica MongoDB offre la stessa elevata disponibilità e ridondanza, ma ora include la capacità di gestire un&#39;interruzione del data center.

![oakclustermongofailover2datacenters](assets/oakclustermongofailover2datacenters.png)

I vantaggi:

* Scalabilità orizzontale con le nuove istanze di creazione di AEM
* Elevata disponibilità, ridondanza e failover automatizzato del livello dati (incluse le interruzioni del data center)

>[!NOTE]
>
>Nel diagramma precedente, a AEM Server 3 e AEM Server 4 viene assegnato uno stato inattivo che presuppone una latenza di rete tra i server AEM in Data Center 2 e il nodo principale MongoDB in Data Center 1 superiore ai requisiti [qui](/help/sites-deploying/aem-with-mongodb.md#checklists)documentati. Se la latenza massima è compatibile con i requisiti, ad esempio mediante l’uso di aree di disponibilità, i server AEM in Data Center 2 possono essere attivi anche, creando un cluster AEM attivo su più datacenter.

>[!NOTE]
>
>Per ulteriori informazioni sui concetti architettonici MongoDB descritti in questa sezione, vedere Replica [](https://docs.mongodb.org/manual/replication/)MongoDB.

## Microkernel: quale utilizzare {#microkernels-which-one-to-use}

La regola di base che deve essere presa in considerazione nella scelta tra i due micro kernel disponibili è che TarMK è progettato per le prestazioni, mentre MongoMK è utilizzato per la scalabilità.

Potete utilizzare queste matrici decisionali per stabilire quale sia il tipo di distribuzione migliore adatto ai vostri requisiti.

Adobe consiglia vivamente a TarMK di essere la tecnologia di persistenza predefinita utilizzata dai clienti in tutti gli scenari di distribuzione, sia per le istanze di AEM Author che di AEM Publish, fatta eccezione per i casi di utilizzo indicati di seguito.

### Eccezioni per la scelta di AEM MongoMK su TarMK sulle istanze di authoring {#exceptions-for-choosing-aem-mongomk-over-tarmk-on-author-instances}

Il motivo principale per cui si sceglie la persistenza MongoMK al di sopra di TarMK è quello di ridimensionare le istanze orizzontalmente. Ciò significa che due o più istanze di autori attive sono sempre in esecuzione e che utilizzano MongoDB come sistema di storage persistente. La necessità di eseguire più di un&#39;istanza di autore deriva generalmente dal fatto che la CPU e la capacità di memoria di un singolo server, che supportano tutte le attività di authoring simultanee, non sono più sostenibili.

È quasi impossibile prevedere quale sarà il modello di concorrenza esatto dopo che un nuovo sito sarà attivo. Adobe consiglia pertanto di considerare i seguenti criteri per valutare se utilizzare MongoMK e due o più nodi attivi Autore:

1. Numero di utenti denominati connessi in un giorno: in migliaia o più.
1. Numero di utenti simultanei: nelle centinaia o più.
1. Volume di invii di risorse al giorno: a centinaia di migliaia o più.
1. Volume di modifiche alla pagina al giorno: in centinaia di migliaia o più (inclusi gli aggiornamenti automatizzati tramite Multi Site Manager o news feed, ad esempio).
1. Volume di ricerche al giorno: in decine di migliaia o più.

>[!NOTE]
>
>Il giorno duro può essere utilizzato per valutare le prestazioni dell&#39;applicazione del cliente nel contesto della configurazione hardware implementata. Ulteriori informazioni su questo strumento sono disponibili [qui](/help/sites-developing/tough-day.md).

Una distribuzione minima con MongoDB includerà in genere la seguente topologia:

* Un set di repliche MongoDB composto da un nodo primario, due nodi secondari con ciascuna delle istanze MongoDB in esecuzione in una zona di disponibilità con una latenza inferiore a 15 millisecondi su ciascun nodo;
* Un cluster di istanze di autori con un nodo leader, un nodo non leader e entrambi attivi in ogni momento, con ciascuna istanza di autore in esecuzione in ciascuno dei centri dati, in cui sono in esecuzione le istanze principali e secondarie di MongoDB.

Inoltre, si consiglia vivamente di configurare il datastore su un file system condiviso o su Amazon S3, in modo che le risorse o i file binari non vengano memorizzati in MongoDB. Ciò garantirà prestazioni ottimali all&#39;interno della distribuzione.

Uno dei vantaggi aggiuntivi dell&#39;implementazione di un set di repliche MongoDB con un cluster di due o più istanze di autori è la presenza di uno scenario di ripristino automatico con tempi di inattività minimi in caso di istanze di autore, replica MongoDB o errore completo del datacenter. Tuttavia, la scelta di MongoMK su TarMK non dovrebbe essere guidata esclusivamente dal requisito del ripristino, in quanto TarMK può anche fornire una soluzione di inattività minima con un meccanismo di failover controllato.

Se non è previsto che i criteri di cui sopra siano soddisfatti durante i primi diciotto mesi di implementazione, si consiglia di distribuire AEM utilizzando TarMK, quindi di rivalutare la configurazione in una data successiva quando si applicano i criteri di cui sopra, e infine di stabilire se rimanere su TarMK o effettuare la migrazione a MongoMK.

### Eccezioni per la scelta di AEM MongoMK su TarMK sulle istanze di pubblicazione {#exceptions-for-choosing-aem-mongomk-over-tarmk-on-publish-instances}

Non è consigliabile distribuire le istanze MongoMK per la pubblicazione. Il livello di pubblicazione della distribuzione viene quasi sempre distribuito come farm di istanze di pubblicazione completamente indipendenti con TarMK, che vengono mantenute sincronizzate replicando il contenuto dalle istanze dell’autore. Questa architettura &quot;shared no&quot; (nulla condiviso), propria delle istanze di pubblicazione, consente la distribuzione del livello di pubblicazione in scala orizzontale in modo lineare. La topologia della farm offre inoltre il vantaggio di applicare qualsiasi aggiornamento o aggiornamento alle istanze pubblicate su base continuativa, in modo che qualsiasi modifica al livello di pubblicazione non richieda tempi di inattività.

Ciò non vale per AEM Communities che utilizzano cluster MongoMK nel livello di pubblicazione ogni volta che sono presenti più autori. Se si sceglie JSRP (vedere Archiviazione [dei contenuti](/help/communities/working-with-srp.md)community), sarà appropriato un cluster MongoMK, come qualsiasi altro cluster lato pubblicazione a prescindere dalla MK scelta, ad esempio MongoDB o RDB.

### Prerequisiti e raccomandazioni per la distribuzione di AEM con MongoMK {#prerequisites-and-recommendations-when-deploying-aem-with-mongomk}

È disponibile un set di prerequisiti e raccomandazioni se state valutando una distribuzione MongoMK per AEM:

**Prerequisiti obbligatori per le distribuzioni MongoDB:**

1. L&#39;architettura e il dimensionamento della distribuzione MongoDB devono essere parte dell&#39;implementazione del progetto con l&#39;aiuto di Adobe Consulting o di MongoDB Architects che hanno familiarità con AEM;
1. Le competenze MongoDB devono essere presenti all&#39;interno del partner o del team di clienti per poter mantenere e mantenere un ambiente MongoDB esistente o nuovo;
1. È possibile scegliere di distribuire la versione commerciale o open source di MongoDB (AEM supporta entrambi), ma è necessario acquistare un contratto di manutenzione e supporto MongoDB direttamente da MongoDB Inc.
1. Le architetture e le infrastrutture di AEM e MongoDB dovrebbero essere definite e convalidate da un architetto Adobe AEM;
1. È necessario esaminare il modello di supporto per le distribuzioni AEM che includono MongoDB.

**Consigli forti per le distribuzioni MongoDB:**

* Consultate l&#39; [articolo](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)MongoDB per Adobe Experience Manager;
* Esaminare la [checklist](https://docs.mongodb.org/manual/administration/production-checklist/)di produzione MongoDB;
* Partecipa a un corso di certificazione su MongoDB disponibile [qui](https://university.mongodb.com/).

>[!NOTE]
>
>Per tutte le domande aggiuntive su queste linee guida, prerequisiti e raccomandazioni, contatta l&#39;Assistenza [clienti](https://helpx.adobe.com/marketing-cloud/contact-support.html)Adobe.

### Considerazioni per AEM Communities {#considerations-for-aem-communities}

Per i siti che intendono implementare [AEM Communities](/help/communities/overview.md), si consiglia di [scegliere una distribuzione](/help/communities/working-with-srp.md#characteristicsofstorageoptions) ottimizzata per la gestione di UGC pubblicate dai membri della community dall&#39;ambiente di pubblicazione.

Utilizzando uno store [](/help/communities/working-with-srp.md)comune, non è necessario replicare UGC tra l’autore e altre istanze di pubblicazione per ottenere una visualizzazione coerente dell’UGC.

Di seguito è riportato un set di matrici decisionali che possono aiutarti a scegliere il tipo di persistenza migliore per la distribuzione:

#### Scelta del tipo di distribuzione per le istanze di creazione {#choosing-the-deployment-type-for-author-instances}

![chlimage_1-19](assets/chlimage_1-19.png)

#### Scelta del tipo di distribuzione per le istanze di pubblicazione {#choosing-the-deployment-type-for-publish-instances}

![chlimage_1-20](assets/chlimage_1-20.png)

>[!NOTE]
>
>MongoDB è un software di terze parti e non è incluso nel pacchetto di licenze di AEM. Per ulteriori informazioni, vedere la pagina relativa ai criteri [di licenza](https://www.mongodb.org/about/licensing/) MongoDB.
>
>Per ottenere il massimo dalla distribuzione AEM, Adobe consiglia di concedere in licenza la versione Enterprise di MongoDB per poter usufruire del supporto professionale.
>
>La licenza include un set di repliche standard, composto da una delle istanze primarie e due secondarie che possono essere utilizzate per le distribuzioni di creazione e pubblicazione.
>
>Se si desidera eseguire sia l&#39;autore che la pubblicazione su MongoDB, è necessario acquistare due licenze separate.
>
>Per ulteriori informazioni, consultate la pagina [MongoDB per Adobe Experience Manager](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).

