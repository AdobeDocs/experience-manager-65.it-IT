---
title: Linee guida sulle prestazioni
seo-title: Performance Guidelines
description: Questo articolo fornisce linee guida generali su come ottimizzare le prestazioni della distribuzione di AEM.
seo-description: This article provides general guidelines on how to optimize the performance of your AEM deployment.
uuid: 38cf8044-9ff9-48df-a843-43f74b0c0133
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 9ccbc39e-aea7-455e-8639-9193abc1552f
feature: Configuring
exl-id: 5a305a5b-0c3d-413b-88c1-1f5abf7e1579
source-git-commit: 9defa6d1843007e9375d839f72f6993c691a37c0
workflow-type: tm+mt
source-wordcount: '2913'
ht-degree: 6%

---

# Linee guida sulle prestazioni{#performance-guidelines}

Questa pagina fornisce linee guida generali su come ottimizzare le prestazioni della distribuzione di AEM. Se non hai ancora AEM, controlla le pagine seguenti prima di iniziare a leggere le linee guida sulle prestazioni:

* [AEM Concetti di base](/help/sites-deploying/deploy.md#basic-concepts)
* [Panoramica dello storage in AEM](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [Implementazioni consigliate](/help/sites-deploying/recommended-deploys.md)
* [Requisiti tecnici](/help/sites-deploying/technical-requirements.md)

Di seguito sono illustrate le opzioni di distribuzione disponibili per AEM (scorri per visualizzare tutte le opzioni):

<table>
 <tbody>
  <tr>
   <td><p><strong>AEM</strong></p> <p><strong>Prodotto</strong></p> </td>
   <td><p><strong>Topologia</strong></p> </td>
   <td><p><strong>Sistema operativo</strong></p> </td>
   <td><p><strong>Server applicazioni</strong></p> </td>
   <td><p><strong>JRE</strong></p> </td>
   <td><p><strong>Sicurezza</strong></p> </td>
   <td><p><strong>Micro Kernel</strong></p> </td>
   <td><p><strong>Datastore</strong></p> </td>
   <td><p><strong>Indicizzazione</strong></p> </td>
   <td><p><strong>Server web</strong></p> </td>
   <td><p><strong>Browser</strong></p> </td>
   <td><p><strong>Experience Cloud</strong></p> </td>
  </tr>
  <tr>
   <td><p>Sites</p> </td>
   <td><p>Non HA</p> </td>
   <td><p>Windows</p> </td>
   <td><p>CQSE</p> </td>
   <td><p>Oracle</p> </td>
   <td><p>LDAP</p> </td>
   <td><p>Tar</p> </td>
   <td><p>Segmento</p> </td>
   <td><p>Proprietà</p> </td>
   <td><p>Apache</p> </td>
   <td><p>Bordo</p> </td>
   <td><p>Destinazione</p> </td>
  </tr>
  <tr>
   <td><p>Risorse</p> </td>
   <td><p>Publish-HA</p> </td>
   <td><p>Solaris™</p> </td>
   <td><p>WebLogic</p> </td>
   <td><p>IBM®</p> </td>
   <td><p>SAML</p> </td>
   <td><p>MongoDB</p> </td>
   <td><p>File</p> </td>
   <td><p>Lucene</p> </td>
   <td><p>IIS</p> </td>
   <td><p>IE</p> </td>
   <td><p>Analytics</p> </td>
  </tr>
  <tr>
   <td><p>Communities</p> </td>
   <td><p>Autore-CS</p> </td>
   <td><p>Red Hat®</p> </td>
   <td><p>WebSphere®</p> </td>
   <td><p>HP</p> </td>
   <td><p>Oauth</p> </td>
   <td><p>RDB/Oracle</p> </td>
   <td><p>S3/Azure</p> </td>
   <td><p>Solr</p> </td>
   <td><p>iPlanet</p> </td>
   <td><p>FireFox</p> </td>
   <td><p>Campaign</p> </td>
  </tr>
  <tr>
   <td><p>Forms</p> </td>
   <td><p>Author-Offload</p> </td>
   <td><p>HP-UX</p> </td>
   <td><p>Tomcat</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>RDB/DB2</p> </td>
   <td><p>MongoDB</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Chrome</p> </td>
   <td><p>Social network</p> </td>
  </tr>
  <tr>
   <td><p>Mobile</p> </td>
   <td><p>Autore-cluster</p> </td>
   <td><p>IBM® AIX®</p> </td>
   <td><p>JBoss®</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>RDB/MySQL</p> </td>
   <td><p>RDBMS</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Safari</p> </td>
   <td><p>Pubblico</p> </td>
  </tr>
  <tr>
   <td><p>Sito multiplo</p> </td>
   <td><p>ASRP</p> </td>
   <td><p>SUSE®</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>RDB/SQLServer</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Risorse</p> </td>
  </tr>
  <tr>
   <td><p>Commerce</p> </td>
   <td><p>MSRP</p> </td>
   <td><p>Apple OS</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Attivazione</p> </td>
  </tr>
  <tr>
   <td><p>Dynamic Media</p> </td>
   <td><p>JSRP</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Mobile</p> </td>
  </tr>
  <tr>
   <td><p>Brand Portal</p> </td>
   <td><p>J2E</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>AoD</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>LiveFyre</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>Screens</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>Sicurezza dei documenti</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>Mgt del processo</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>App desktop</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Le linee guida sulle prestazioni si applicano principalmente ad AEM Sites.

## Quando utilizzare le linee guida sulle prestazioni {#when-to-use-the-performance-guidelines}

Utilizza le linee guida sulle prestazioni nelle situazioni seguenti:

* **Distribuzione iniziale**: Quando prevedi di distribuire AEM Sites o Assets per la prima volta, è importante comprendere le opzioni disponibili. Soprattutto per la configurazione del Micro Kernel, del Node Store e del Data Store (rispetto alle impostazioni predefinite). Ad esempio, la modifica delle impostazioni predefinite di Data Store per TarMK in File Data Store.
* **Aggiornamento a una nuova versione**: Quando esegui l’aggiornamento a una nuova versione, è importante comprendere le differenze di prestazioni rispetto all’ambiente in esecuzione. Ad esempio, l&#39;aggiornamento da AEM 6.1 a 6.2 o da AEM 6.0 CRX2 a 6.2 OAK.
* **Il tempo di risposta è lento**: Quando l’architettura del nodestore selezionato non soddisfa le tue esigenze, è importante comprendere le differenze di prestazioni rispetto ad altre opzioni di topologia. Ad esempio, distribuire TarMK invece di MongoMK o utilizzare un archivio dati file invece di un archivio dati Amazon S3 o Microsoft® Azure.
* **Aggiunta di altri autori**: Quando la topologia TarMK consigliata non soddisfa i requisiti di prestazioni e l’upsize del nodo Autore ha raggiunto la capacità massima disponibile, comprendere le differenze di prestazioni. Confronta con l&#39;utilizzo di MongoMK con tre o più nodi Author. Ad esempio, distribuisci MongoMK invece di TarMK.
* **Aggiunta di altro contenuto**: Quando l’architettura consigliata dell’archivio dati non soddisfa le tue esigenze, è importante comprendere le differenze di prestazioni rispetto ad altre opzioni dell’archivio dati. Esempio: utilizzo dell’archivio dati di Amazon S3 o Microsoft® Azure invece di un archivio dati file.

## Introduzione {#introduction}

Questo capitolo offre una panoramica generale dell&#39;architettura AEM e dei suoi componenti più importanti. Fornisce inoltre linee guida di sviluppo e descrive gli scenari di test utilizzati nei test di benchmark TarMK e MongoMK.

### Piattaforma AEM {#the-aem-platform}

La piattaforma AEM è costituita dai seguenti componenti:

![chlimage_1](assets/chlimage_1a.png)

Per ulteriori informazioni sulla piattaforma AEM, consulta [AEM](/help/sites-deploying/deploy.md#what-is-aem).

### Architettura AEM {#the-aem-architecture}

Sono disponibili tre importanti elementi di base per una distribuzione AEM. La **Istanza autore** utilizzato da autori di contenuti, editor e approvatori per creare e rivedere contenuti. Quando il contenuto viene approvato, viene pubblicato in un secondo tipo di istanza denominato **Pubblica istanza** da dove è accessibile agli utenti finali. Il terzo elemento costitutivo è il **Dispatcher** che è un modulo che gestisce la memorizzazione in cache e il filtro URL e viene installato sul server web. Per ulteriori informazioni sull’architettura AEM, consulta [Scenari di implementazione tipici](/help/sites-deploying/deploy.md#typical-deployment-scenarios).

![chlimage_1-1](assets/chlimage_1-1a.png)

### Micro Kernel {#micro-kernels}

I micro kernel agiscono come gestori di persistenza in AEM. Esistono tre tipi di Micro Kernel utilizzati con AEM: TarMK, MongoDB e database relazionale (con supporto limitato). La scelta di uno per soddisfare le tue esigenze dipende dallo scopo della tua istanza e dal tipo di distribuzione che stai considerando. Per ulteriori informazioni sui Micro Kernel, consulta la sezione [Implementazioni consigliate](/help/sites-deploying/recommended-deploys.md) pagina.

![chlimage_1-2](assets/chlimage_1-2a.png)

### Nodestore {#nodestore}

In AEM, i dati binari possono essere memorizzati indipendentemente dai nodi di contenuto. La posizione in cui vengono memorizzati i dati binari è indicata come **Archiviazione dati**, mentre la posizione dei nodi e delle proprietà del contenuto è denominata **Archiviazione dei nodi**.

>[!NOTE]
>
>Adobe consiglia a TarMK di essere la tecnologia di persistenza predefinita utilizzata dai clienti sia per le istanze di authoring AEM che per quelle di pubblicazione.

>[!CAUTION]
>
>Supporto limitato per il Micro Kernel del database relazionale. Contatto [Adobe Customer Care](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=homehome?lang=it#support) prima di utilizzare questo tipo di Micro Kernel.

![chlimage_1-3](assets/chlimage_1-3a.png)

### Archiviazione dati {#data-store}

Quando si gestisce un numero elevato di binari, è consigliabile utilizzare un archivio dati esterno invece degli archivi nodi predefiniti per massimizzare le prestazioni. Ad esempio, se il progetto richiede molte risorse multimediali, memorizzarle nell’archivio dati File o Azure/S3 consente di accedervi più rapidamente che archiviarle direttamente all’interno di un MongoDB.

Per ulteriori dettagli sulle opzioni di configurazione disponibili, vedi [Configurazione di nodi e archivi dati](/help/sites-deploying/data-store-config.md).

>[!NOTE]
>
>Adobe consiglia di scegliere l’opzione di distribuzione di AEM su Azure o Amazon Web Services (AWS) tramite Adobe Managed Services. I clienti beneficiano di un team che dispone dell&#39;esperienza e delle competenze necessarie per implementare e operare AEM in questi ambienti di cloud computing. Vedi [documentazione aggiuntiva su Adobe Managed Services](https://business.adobe.com/products/experience-manager/managed-services.html?aemClk=t).
>
>Per raccomandazioni su come distribuire AEM su Azure o AWS, al di fuori di Adobe Managed Services, Adobe consiglia di lavorare direttamente con il provider cloud. Oppure, collabora con uno dei partner di Adobe che supporta l’implementazione di AEM nell’ambiente cloud desiderato. Il fornitore o partner cloud selezionato è responsabile delle specifiche di dimensionamento, della progettazione e dell&#39;implementazione dell&#39;architettura che supporta per soddisfare i requisiti specifici di prestazioni, carico, scalabilità e sicurezza.
>Vedi anche [requisiti tecnici](/help/sites-deploying/technical-requirements.md#supported-platforms) pagina.
>
>
>
### Ricerca {#search-features}

In questa sezione sono elencati i provider di indice personalizzati utilizzati con AEM. Per ulteriori informazioni sull&#39;indicizzazione, vedi [Query e indicizzazione Oak](/help/sites-deploying/queries-and-indexing.md).

>[!NOTE]
Per la maggior parte delle distribuzioni, Adobe consiglia di utilizzare l&#39;Indice Lucene. Utilizza Solr solo per la scalabilità in implementazioni specializzate e complesse.

![chlimage_1-4](assets/chlimage_1-4a.png)

### Linee guida per lo sviluppo {#development-guidelines}

Sviluppare AEM **prestazioni e scalabilità**. Di seguito sono riportate le best practice che puoi seguire:

**ANNULLA**

* Applicare la separazione di presentazione, logica e contenuto
* Utilizza le API AEM esistenti (ad esempio: Sling) e utensili (ad esempio: Replica)
* Sviluppare nel contesto dei contenuti effettivi
* Sviluppare una capacità di memorizzazione ottimale
* Riduci al minimo il numero di salvataggi (ad esempio: utilizzando flussi di lavoro transitori)
* Assicurati che tutti i punti finali HTTP siano RESTful
* Limitare il campo di applicazione dell&#39;osservazione JCR
* Presta attenzione al thread asincrono

**NON**

* Non utilizzare direttamente le API JCR, se puoi
* Non modificare /libs, ma piuttosto utilizzare le sovrapposizioni
* Non utilizzare le query dove possibile
* Non utilizzare i binding Sling per ottenere i servizi OSGi nel codice Java™, ma utilizza piuttosto:

   * @Riferimento in un componente DS
   * @Inserisci in un modello Sling
   * sling.getService() in una classe Sightly Use
   * sling.getService() in un JSP
   * a ServiceTracker
   * accesso diretto al registro del servizio OSGi

Per ulteriori dettagli sullo sviluppo su AEM, leggi [Sviluppo - Nozioni di base](/help/sites-developing/the-basics.md). Per ulteriori best practice, consulta [Tecniche consigliate per lo sviluppo](/help/sites-developing/best-practices.md).

### Scenari di benchmark {#benchmark-scenarios}

>[!NOTE]
Tutti i test di riferimento visualizzati in questa pagina sono stati eseguiti in un ambiente di laboratorio.

Gli scenari di test descritti di seguito sono utilizzati per le sezioni di riferimento dei capitoli TarMK, MongoMk e TarMK rispetto a MongoMk. Per vedere quale scenario è stato utilizzato per un particolare test di benchmark, leggi il campo Scenario dal [Specifiche tecniche](/help/sites-deploying/performance-guidelines.md#tarmk-performance-benchmark) tabella.

**Scenario di prodotto singolo**

AEM Assets:

* Interazioni utente: Sfoglia risorse / Cerca risorse / Scarica risorsa / Leggi metadati risorsa / Aggiorna metadati risorsa / Carica risorsa / Esegui flusso di lavoro di caricamento risorsa
* Modalità di esecuzione: utenti simultanei, interazione singola per utente

**Scenario di prodotti misti**

AEM Sites + Risorse:

* Interazioni utente su Sites: Pagina Leggi Articolo / Pagina Leggi / Crea Paragrafo / Modifica Paragrafo / Crea Pagina Contenuto / Attiva Pagina Contenuto / Ricerca Autore
* Interazioni utente delle risorse: Sfoglia risorse / Cerca risorse / Scarica risorsa / Leggi metadati risorsa / Aggiorna metadati risorsa / Carica risorsa / Esegui flusso di lavoro di caricamento risorsa
* Modalità di esecuzione: utenti simultanei, interazioni miste per utente

**Scenario d&#39;uso verticale**

File multimediali:

* `Read Article Page (27.4%), Read Page (10.9%), Create Session (2.6%), Activate Content Page (1.7%), Create Content Page (0.4%), Create Paragraph (4.3%), Edit Paragraph (0.9%), Image Component (0.9%), Browse Assets (20%), Read Asset Metadata (8.5%), Download Asset (4.2%), Search Asset (0.2%), Update Asset Metadata (2.4%), Upload Asset (1.2%), Browse Project (4.9%), Read Project (6.6%), Project Add Asset (1.2%), Project Add Site (1.2%), Create Project (0.1%), Author Search (0.4%)`
* Modalità di esecuzione: utenti simultanei, interazioni miste per utente

## TarMK {#tarmk}

Questo capitolo fornisce linee guida generali sulle prestazioni per TarMK che specificano i requisiti minimi di architettura e la configurazione delle impostazioni. Sono inoltre previste prove di riferimento per ulteriori chiarimenti.

Adobe consiglia a TarMK di essere la tecnologia di persistenza predefinita utilizzata dai clienti in tutti gli scenari di implementazione, sia per le istanze di authoring AEM che per quelle di pubblicazione.

Per ulteriori informazioni su TarMK, vedi [Scenari di distribuzione](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) e [Archiviazione Tar](/help/sites-deploying/storage-elements-in-aem-6.md#tar-storage).

### Linee guida sull’architettura minima TarMK {#tarmk-minimum-architecture-guidelines}

>[!NOTE]
Le linee guida dell’architettura minima illustrate di seguito sono per gli ambienti di produzione e i siti a traffico elevato. Tali orientamenti **not** la [specifiche minime](/help/sites-deploying/technical-requirements.md#prerequisites) per eseguire AEM.

Per stabilire buone prestazioni quando si utilizza TarMK, è necessario partire dalla seguente architettura:

* Un’istanza Author
* Due istanze di pubblicazione
* Due dispatcher

Di seguito sono illustrate le linee guida dell’architettura per AEM siti e AEM Assets.

>[!NOTE]
La replica senza binario deve essere attivata **ON** se File Datastore è condiviso.

**Linee guida sull’architettura Tar per AEM Sites**

![chlimage_1-5](assets/chlimage_1-5a.png)

**Linee guida sull’architettura Tar per AEM Assets**

![chlimage_1-6](assets/chlimage_1-6a.png)

### Linee guida sulle impostazioni TarMK {#tarmk-settings-guideline}

Per ottenere prestazioni ottimali, segui le linee guida sulle impostazioni illustrate di seguito. Per istruzioni su come modificare le impostazioni, [vedere questa pagina](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=en).

<table>
 <tbody>
  <tr>
   <td><strong>Impostazione</strong></td>
   <td><strong>Parametro</strong></td>
   <td><strong>Valore</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>Code di lavoro Sling</td>
   <td><code>queue.maxparallel</code></td>
   <td>Imposta il valore a metà del numero di core della CPU. </td>
   <td>Per impostazione predefinita, il numero di thread simultanei per coda di lavoro è uguale al numero di core della CPU.</td>
  </tr>
  <tr>
   <td>Coda flusso di lavoro transitorio di Granite</td>
   <td><code>Max Parallel</code></td>
   <td>Imposta il valore a metà del numero di core della CPU</td>
   <td> </td>
  </tr>
  <tr>
   <td>Parametri JVM</td>
   <td><p><code>Doak.queryLimitInMemory</code></p> <p><code>Doak.queryLimitReads</code></p> <p><code>Dupdate.limit</code></p> <p><code>Doak.fastQuerySize</code></p> </td>
   <td><p>500000</p> <p>100000</p> <p>250000</p> <p>Vero</p> </td>
   <td>Per evitare che le query espansive sovraccarichino i sistemi, aggiungi questi parametri JVM nello script di avvio AEM.</td>
  </tr>
  <tr>
   <td>Configurazione dell'indice Lucene</td>
   <td><p><code>CopyOnRead</code></p> <p><code>CopyOnWrite</code></p> <p><code>Prefetch Index Files</code></p> </td>
   <td><p>Abilitato</p> <p>Abilitato</p> <p>Abilitato</p> </td>
   <td>Per maggiori dettagli sui parametri disponibili, vedi <a href="https://jackrabbit.apache.org/oak/docs/query/lucene.html">questa pagina</a>.</td>
  </tr>
  <tr>
   <td>Archivio dati = Datastore S3</td>
   <td><p><code>maxCachedBinarySize</code></p> <p><code>cacheSizeInMB</code></p> </td>
   <td><p>1048576 (1 MB) o inferiore</p> <p>2-10% della dimensione massima dell'heap</p> </td>
   <td>Vedi anche <a href="/help/sites-deploying/data-store-config.md#data-store-configurations">Configurazioni dell'archivio dati</a>.</td>
  </tr>
  <tr>
   <td>Flusso di lavoro Aggiorna risorsa DAM</td>
   <td><code>Transient Workflow</code></td>
   <td>spuntato</td>
   <td>Questo flusso di lavoro gestisce l'aggiornamento delle risorse.</td>
  </tr>
  <tr>
   <td>Writeback di metadati DAM</td>
   <td><code>Transient Workflow</code></td>
   <td>spuntato</td>
   <td>Questo flusso di lavoro gestisce XMP write-back del binario originale e imposta l'ultima data modificata in JCR.</td>
  </tr>
 </tbody>
</table>

### Benchmark delle prestazioni di TarMK {#tarmk-performance-benchmark}

#### Specifiche tecniche {#technical-specifications}

Le prove di riferimento sono state eseguite sulle seguenti specifiche:

|  | **Nodo autore** |
|---|---|
| Server | Hardware a metallo nudo (HP) |
| Sistema operativo | Red Hat® Linux® |
| CPU/core | CPU Intel(R) Xeon(R) E5-2407 @2,40 GHz, 8 core |
| RAM | 32 GB |
| Disco | Magnetico |
| Java™ | Oracle JRE versione 8 |
| Heap JVM | 16 GB |
| Prodotto | AEM 6.2 |
| Nodestore | TarMK |
| Datastore | File DS |
| Scenario | Prodotto singolo: Risorse / 30 thread simultanei |

#### Risultati del benchmark delle prestazioni {#performance-benchmark-results}

>[!NOTE]
I numeri riportati di seguito sono stati normalizzati a 1 come linea di base e non sono i numeri effettivi della velocità effettiva.

![chlimage_1-7](assets/chlimage_1-7a.png) ![chlimage_1-8](assets/chlimage_1-8a.png)

## MongoMK {#mongomk}

La ragione principale per scegliere il backend di persistenza MongoMK su TarMK è la scalabilità orizzontale delle istanze. Questa capacità significa che due o più istanze di authoring attive sono sempre in esecuzione e utilizzano MongoDB come sistema di storage di persistenza. La necessità di eseguire più di un&#39;istanza dell&#39;autore deriva generalmente dal fatto che la CPU e la capacità di memoria di un singolo server, che supportano tutte le attività di authoring simultanee, non sono più sostenibili.

Per ulteriori informazioni su TarMK, vedi [Scenari di distribuzione](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) e [Archiviazione Mongo](/help/sites-deploying/storage-elements-in-aem-6.md#mongo-storage).

### Linee guida sull’architettura minima MongoMK {#mongomk-minimum-architecture-guidelines}

Per stabilire buone prestazioni quando si utilizza MongoMK, è necessario partire dalla seguente architettura:

* Tre istanze di authoring
* Due istanze di pubblicazione
* Tre istanze MongoDB
* Due dispatcher

>[!NOTE]
Negli ambienti di produzione MongoDB viene sempre utilizzato come set di repliche con un database primario e due secondari. Le letture e le scritture vanno al primo e le letture possono andare ai secondi. Se lo spazio di archiviazione non è disponibile, è possibile sostituire uno dei secondari con un arbitro, ma i set di repliche MongoDB devono sempre essere composti da un numero dispari di istanze.

>[!NOTE]
La replica senza binario deve essere attivata **ON** se File Datastore è condiviso.

![chlimage_1-9](assets/chlimage_1-9a.png)

### Linee guida sulle impostazioni MongoMK {#mongomk-settings-guidelines}

Per ottenere prestazioni ottimali, segui le linee guida sulle impostazioni illustrate di seguito. Per istruzioni su come modificare le impostazioni, [vedere questa pagina](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=en).

<table>
 <tbody>
  <tr>
   <td><strong>Impostazione</strong></td>
   <td><strong>Parametro</strong></td>
   <td><strong>Valore (predefinito)</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>Code di lavoro Sling</td>
   <td><code>queue.maxparallel</code></td>
   <td>Imposta il valore a metà del numero di core della CPU. </td>
   <td>Per impostazione predefinita, il numero di thread simultanei per coda di lavoro è uguale al numero di core della CPU.</td>
  </tr>
  <tr>
   <td>Coda flusso di lavoro transitorio di Granite</td>
   <td><code>Max Parallel</code></td>
   <td>Imposta il valore a metà del numero di core della CPU.</td>
   <td> </td>
  </tr>
  <tr>
   <td>Parametri JVM</td>
   <td><p><code>Doak.queryLimitInMemory</code></p> <p><code>Doak.queryLimitReads</code></p> <p><code>Dupdate.limit</code></p> <p><code>Doak.fastQuerySize</code></p> <p><code>Doak.mongo.maxQueryTimeMS</code></p> </td>
   <td><p>500000</p> <p>100000</p> <p>250000</p> <p>Vero</p> <p>60000</p> </td>
   <td>Per evitare che le query espansive sovraccarichino i sistemi, aggiungi questi parametri JVM nello script di avvio AEM.</td>
  </tr>
  <tr>
   <td>Configurazione dell'indice Lucene</td>
   <td><p><code>CopyOnRead</code></p> <p><code>CopyOnWrite</code></p> <p><code>Prefetch Index Files</code></p> </td>
   <td><p>Abilitato</p> <p>Abilitato</p> <p>Abilitato</p> </td>
   <td>Per ulteriori dettagli sui parametri disponibili, vedi <a href="https://jackrabbit.apache.org/oak/docs/query/lucene.html">questa pagina</a>.</td>
  </tr>
  <tr>
   <td>Archivio dati = Datastore S3</td>
   <td><p><code>maxCachedBinarySize</code></p> <p><code>cacheSizeInMB</code></p> </td>
   <td><p>1048576 (1 MB) o inferiore</p> <p>2-10% della dimensione massima dell'heap</p> </td>
   <td>Vedi anche <a href="/help/sites-deploying/data-store-config.md#data-store-configurations">Configurazioni dell'archivio dati</a>.</td>
  </tr>
  <tr>
   <td>DocumentNodeStoreService</td>
   <td><p><code>cache</code></p> <p><code>nodeCachePercentage</code></p> <p><code>childrenCachePercentage</code></p> <p><code>diffCachePercentage</code></p> <p><code>docChildrenCachePercentage</code></p> <p><code>prevDocCachePercentage</code></p> <p><code>persistentCache</code></p> </td>
   <td><p>2048</p> <p>35 (25)</p> <p>20 (10)</p> <p>30 (5)</p> <p>10 (3)</p> <p>4 (4)</p> <p>./cache,size=2048,binary=0,-compact,-compress</p> </td>
   <td><p>La dimensione predefinita della cache è impostata su 256 MB.</p> <p>Ha un impatto sul tempo necessario per eseguire l’annullamento della validità della cache.</p> </td>
  </tr>
  <tr>
   <td>osservazione della quercia</td>
   <td><p><code>thread pool</code></p> <p><code>length</code></p> </td>
   <td><p>min &amp; max = 20</p> <p>50000</p> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Benchmark delle prestazioni MongoMK {#mongomk-performance-benchmark}

### Specifiche tecniche {#technical-specifications-1}

Le prove di riferimento sono state eseguite sulle seguenti specifiche:

|  | **Nodo autore** | **Nodo MongoDB** |
|---|---|---|
| Server | Hardware a metallo nudo (HP) | Hardware a metallo nudo (HP) |
| Sistema operativo | Red Hat® Linux® | Red Hat® Linux® |
| CPU/core | CPU Intel(R) Xeon(R) E5-2407 @2,40 GHz, 8 core | CPU Intel(R) Xeon(R) E5-2407 @2,40 GHz, 8 core |
| RAM | 32 GB | 32 GB |
| Disco | Magnetico - >1k IOPS | Magnetico - >1k IOPS |
| Java™ | Oracle JRE versione 8 | N/D |
| Heap JVM | 16 GB | N/D |
| Prodotto | AEM 6.2 | MongoDB 3.2 WiredTiger |
| Nodestore | MongoMK | N/D |
| Datastore | File DS | N/D |
| Scenario | Prodotto singolo: Risorse / 30 thread simultanei | Prodotto singolo: Risorse / 30 thread simultanei |

### Risultati del benchmark delle prestazioni {#performance-benchmark-results-1}

>[!NOTE]
I numeri riportati di seguito sono stati normalizzati a 1 come linea di base e non sono i numeri effettivi della velocità effettiva.

![chlimage_1-10](assets/chlimage_1-10a.png) ![chlimage_1-11](assets/chlimage_1-11a.png)

## TarMK vs MongoMK {#tarmk-vs-mongomk}

La regola di base di cui tenere conto quando si sceglie tra i due è che TarMK è progettato per le prestazioni, mentre MongoMK è utilizzato per la scalabilità. Adobe consiglia a TarMK di essere la tecnologia di persistenza predefinita utilizzata dai clienti in tutti gli scenari di implementazione, sia per le istanze di authoring AEM che per quelle di pubblicazione.

La ragione principale per scegliere il backend di persistenza MongoMK su TarMK è la scalabilità orizzontale delle istanze. Questa funzionalità significa che due o più istanze di authoring attive sono sempre in esecuzione e utilizzano MongoDB come sistema di storage di persistenza. La necessità di eseguire più di un’istanza di authoring generalmente deriva dal fatto che la CPU e la capacità di memoria di un singolo server, che supportano tutte le attività di authoring simultanee, non sono più sostenibili.

Per maggiori dettagli su TarMK vs MongoMK, vedi [Implementazioni consigliate](/help/sites-deploying/recommended-deploys.md#microkernels-which-one-to-use).

### Linee guida per TarMK e MongoMk {#tarmk-vs-mongomk-guidelines}

**Vantaggi di TarMK**

* Progettato appositamente per le applicazioni di gestione dei contenuti
* I file sono sempre coerenti e possono essere sottoposti a backup utilizzando qualsiasi strumento di backup basato su file
* Fornisce un meccanismo di failover - vedi [Standby a freddo](/help/sites-deploying/tarmk-cold-standby.md) per ulteriori dettagli
* Offre prestazioni elevate e un&#39;archiviazione affidabile dei dati con costi operativi minimi
* TCO ridotto (costo totale di proprietà)

**Criteri per la scelta di MongoMK**

* Numero di utenti denominati connessi in un giorno: in migliaia o più
* Numero di utenti simultanei: a centinaia o più
* Volume di ingestioni di risorse al giorno: a centinaia di migliaia o più
* Volume di modifiche alla pagina al giorno: a centinaia di migliaia o più
* Volume di ricerche al giorno: a decine di migliaia o più

### Benchmark TarMK vs MongoMK {#tarmk-vs-mongomk-benchmarks}

>[!NOTE]
I numeri riportati di seguito sono stati normalizzati a 1 come linea di base e non sono numeri effettivi del throughput.

### Scenario 1 Specifiche tecniche {#scenario-technical-specifications}

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>Nodo OAK autore</strong></td>
   <td><strong>Nodo MongoDB</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td>Server</td>
   <td>Hardware a metallo nudo (HP)</td>
   <td>Hardware a metallo nudo (HP)</td>
   <td> </td>
  </tr>
  <tr>
   <td>Sistema operativo</td>
   <td>Red Hat® Linux®</td>
   <td>Red Hat® Linux®</td>
   <td> </td>
  </tr>
  <tr>
   <td>CPU/core</td>
   <td>CPU Intel(R) Xeon(R) E5-2407 @2,40 GHz, 8 core</td>
   <td>CPU Intel(R) Xeon(R) E5-2407 @2,40 GHz, 8 core</td>
   <td> </td>
  </tr>
  <tr>
   <td>RAM</td>
   <td>32 GB</td>
   <td>32 GB</td>
   <td> </td>
  </tr>
  <tr>
   <td>Disco</td>
   <td>Magnetico - &gt;1k IOPS</td>
   <td>Magnetico - &gt;1k IOPS</td>
   <td> </td>
  </tr>
  <tr>
   <td>Java™</td>
   <td>Oracle JRE versione 8</td>
   <td>N/D</td>
   <td> </td>
  </tr>
  <tr>
   <td>Heap JVM da 16 GB</td>
   <td>16 GB</td>
   <td>N/D</td>
   <td> </td>
  </tr>
  <tr>
   <td>Prodotto </td>
   <td>AEM 6.2</td>
   <td>MongoDB 3.2 WiredTiger</td>
   <td> </td>
  </tr>
  <tr>
   <td>Nodestore</td>
   <td>TarMK o MongoMK</td>
   <td>N/D</td>
   <td> </td>
  </tr>
  <tr>
   <td>Datastore</td>
   <td>File DS </td>
   <td>N/D</td>
   <td> </td>
  </tr>
  <tr>
   <td>Scenario</td>
   <td><p><br /> Prodotto singolo: Risorse / 30 thread simultanei per esecuzione</p> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Risultati del benchmark delle prestazioni dello scenario 1 {#scenario-performance-benchmark-results}

![chlimage_1-12](assets/chlimage_1-12a.png)

### Scenario 2 Specifiche tecniche {#scenario-technical-specifications-1}

>[!NOTE]
Per abilitare lo stesso numero di autori con MongoDB come con un sistema TarMK, è necessario un cluster con due nodi AEM. Un cluster MongoDB a quattro nodi può gestire 1,8 volte il numero di autori rispetto a un&#39;istanza TarMK. Un cluster MongoDB a otto nodi può gestire 2,3 volte il numero di autori rispetto a un&#39;istanza TarMK.

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>Nodo TarMK autore</strong></td>
   <td><strong>Nodo MongoMK autore</strong></td>
   <td><strong>Nodo MongoDB</strong></td>
  </tr>
  <tr>
   <td>Server</td>
   <td>AWS c3.8xlarge</td>
   <td>AWS c3.8xlarge</td>
   <td>AWS c3.8xlarge</td>
  </tr>
  <tr>
   <td>Sistema operativo</td>
   <td>Red Hat® Linux®</td>
   <td>Red Hat® Linux®</td>
   <td>Red Hat® Linux®</td>
  </tr>
  <tr>
   <td>CPU/core</td>
   <td>32</td>
   <td>32</td>
   <td>32</td>
  </tr>
  <tr>
   <td>RAM</td>
   <td>60 GB</td>
   <td>60 GB</td>
   <td>60 GB</td>
  </tr>
  <tr>
   <td>Disco</td>
   <td>SSD - 10.000 IOPS</td>
   <td>SSD - 10.000 IOPS</td>
   <td>SSD - 10.000 IOPS</td>
  </tr>
  <tr>
   <td>Java™</td>
   <td>Oracle JRE versione 8</td>
   <td><br /> Oracle JRE versione 8</td>
   <td>N/D</td>
  </tr>
  <tr>
   <td>Heap JVM da 16 GB</td>
   <td>30 GB</td>
   <td>30 GB</td>
   <td>N/D</td>
  </tr>
  <tr>
   <td>Prodotto </td>
   <td>AEM 6.2</td>
   <td>AEM 6.2</td>
   <td><br /> MongoDB 3.2 WiredTiger</td>
  </tr>
  <tr>
   <td>Nodestore</td>
   <td>TarMK </td>
   <td>MongoMK</td>
   <td><br /> N/D</td>
  </tr>
  <tr>
   <td>Datastore</td>
   <td>File DS </td>
   <td><br /> File DS</td>
   <td><br /> N/D</td>
  </tr>
  <tr>
   <td>Scenario</td>
   <td><p><br /> <br /> Caso di utilizzo verticale: Thread simultanei di Media / 2000</p> </td>
   <td></td>
   <td></td>
  </tr>
 </tbody>
</table>

### Risultati di benchmark delle prestazioni dello scenario 2 {#scenario-performance-benchmark-results-1}

![chlimage_1-13](assets/chlimage_1-13a.png)

### Linee guida per la scalabilità dell’architettura per AEM Sites e Assets {#architecture-scalability-guidelines-for-aem-sites-and-assets}

![chlimage_1-14](assets/chlimage_1-14a.png)

## Riepilogo delle linee guida sulle prestazioni  {#summary-of-performance-guidelines}

Le linee guida presentate in questa pagina possono essere riassunte come segue:

* **TarMK con archivio dati file** - Architettura consigliata per la maggior parte dei clienti:

   * Topologia minima: un’istanza Author, due istanze Publish, due istanze Dispatcher
   * Replica senza binario attivata se File Datastore è condiviso

* **MongoMK con archivio dati file** - Architettura consigliata per la scalabilità orizzontale del livello di authoring:

   * Topologia minima: tre istanze Autore, tre istanze MongoDB, due istanze Publish, due istanze Dispatcher
   * Replica senza binario attivata se File Datastore è condiviso

* **Nodestore** - Archiviato sul disco locale, non su un sistema NAS (Network Attached Storage)
* Quando utilizzi **Amazon S3**:

   * Il datastore Amazon S3 è condiviso tra il livello Author e Publish
   * La replica senza binario deve essere attivata
   * La raccolta oggetti inattivi del datastore richiede una prima esecuzione su tutti i nodi Author e Publish, quindi una seconda esecuzione su Author

* **L&#39;indice personalizzato deve essere creato in aggiunta all&#39;indice preconfigurato** - In base alle ricerche più comuni

   * Gli indici Lucene devono essere utilizzati per gli indici personalizzati

* **La personalizzazione del flusso di lavoro può migliorare notevolmente le prestazioni** - Rimuovi il passaggio video nel flusso di lavoro &quot;Aggiorna risorsa&quot;, disabilitando gli ascoltatori non utilizzati e così via.

Per ulteriori dettagli, consulta anche il [Implementazioni consigliate](/help/sites-deploying/recommended-deploys.md) pagina.
