---
title: Linee guida sulle prestazioni
seo-title: Linee guida sulle prestazioni
description: Questo articolo fornisce linee guida generali su come ottimizzare le prestazioni della distribuzione AEM.
seo-description: Questo articolo fornisce linee guida generali su come ottimizzare le prestazioni della distribuzione AEM.
uuid: 38cf8044-9ff9-48df-a843-43f74b0c0133
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 9ccbc39e-aea7-455e-8639-9193abc1552f
translation-type: tm+mt
source-git-commit: a678716e2c0520891e4228bc49b075f070ea45b7
workflow-type: tm+mt
source-wordcount: '2993'
ht-degree: 6%

---


# Linee guida sulle prestazioni{#performance-guidelines}

Questa pagina contiene linee guida generali su come ottimizzare le prestazioni della distribuzione AEM. Se non avete mai AEM, passate le pagine seguenti prima di iniziare a leggere le linee guida sulle prestazioni:

* [AEM Concetti di base](/help/sites-deploying/deploy.md#basic-concepts)
* [Panoramica dello storage in AEM](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [Implementazioni consigliate](/help/sites-deploying/recommended-deploys.md)
* [Requisiti tecnici](/help/sites-deploying/technical-requirements.md)

Di seguito sono illustrate le opzioni di distribuzione disponibili per AEM (scorrete per visualizzare tutte le opzioni):

<table>
 <tbody>
  <tr>
   <td><p><strong>AEM</strong></p> <p><strong>Prodotto</strong></p> </td>
   <td><p><strong>Topologia</strong></p> </td>
   <td><p><strong>Sistema operativo</strong></p> </td>
   <td><p><strong>Application Server</strong></p> </td>
   <td><p><strong>JRE</strong></p> </td>
   <td><p><strong>Sicurezza</strong></p> </td>
   <td><p><strong>Micro Kernel</strong></p> </td>
   <td><p><strong>Datastore</strong></p> </td>
   <td><p><strong>Indicizzazione</strong></p> </td>
   <td><p><strong>Server web</strong></p> </td>
   <td><p><strong>Browser</strong></p> </td>
   <td><p><strong>Marketing Cloud</strong></p> </td>
  </tr>
  <tr>
   <td><p>Sites</p> </td>
   <td><p>Non HA</p> </td>
   <td><p>Windows</p> </td>
   <td><p>CQSE</p> </td>
   <td><p> Oracle</p> </td>
   <td><p>LDAP</p> </td>
   <td><p>Tar</p> </td>
   <td><p>Segmento</p> </td>
   <td><p>Proprietà</p> </td>
   <td><p>Apache</p> </td>
   <td><p>Edge</p> </td>
   <td><p>Destinazione</p> </td>
  </tr>
  <tr>
   <td><p>Assets</p> </td>
   <td><p>Publish-HA</p> </td>
   <td><p>Solaris</p> </td>
   <td><p>WebLogic</p> </td>
   <td><p>IBM</p> </td>
   <td><p>SAML</p> </td>
   <td><p>MongoDB</p> </td>
   <td><p>File</p> </td>
   <td><p>Lucene</p> </td>
   <td><p>IIS</p> </td>
   <td><p>IE</p> </td>
   <td><p>Analisi</p> </td>
  </tr>
  <tr>
   <td><p>Communities</p> </td>
   <td><p>Author-CS</p> </td>
   <td><p>Cappello rosso</p> </td>
   <td><p>WebSphere</p> </td>
   <td><p>HP</p> </td>
   <td><p>Oauth</p> </td>
   <td><p>RDB/ Oracle</p> </td>
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
   <td><p>Effetto cromatura</p> </td>
   <td><p>Social network</p> </td>
  </tr>
  <tr>
   <td><p>Mobile</p> </td>
   <td><p>Author-Cluster</p> </td>
   <td><p>IBM AIX</p> </td>
   <td><p>JBoss</p> </td>
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
   <td><p>Più siti</p> </td>
   <td><p>ASRP</p> </td>
   <td><p>SUSE</p> </td>
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
   <td><p>Doc Security</p> </td>
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
   <td><p>Mgt di processo</p> </td>
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
   <td><p>app desktop</p> </td>
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
>Le linee guida sulle prestazioni si applicano principalmente a  AEM Sites.

## Quando utilizzare le linee guida sulle prestazioni {#when-to-use-the-performance-guidelines}

Le linee guida sulle prestazioni devono essere utilizzate nelle situazioni seguenti:

* **Prima distribuzione**: Quando pianificate di distribuire  AEM Sites o Assets per la prima volta, è importante comprendere le opzioni disponibili per la configurazione del kernel Micro, dell’archivio nodi e dell’archivio dati (rispetto alle impostazioni predefinite). Ad esempio, modifica delle impostazioni predefinite di Data Store per TarMK in File Data Store.
* **Aggiornamento a una nuova versione**: Quando si esegue l&#39;aggiornamento a una nuova versione, è importante comprendere le differenze di prestazioni rispetto all&#39;ambiente in esecuzione. Ad esempio, l&#39;aggiornamento da AEM 6.1 a 6.2 o da AEM 6.0 CRX2 a 6.2 OAK.
* **Il tempo di risposta è lento**: Se l&#39;architettura del Nodestore selezionata non soddisfa i requisiti dell&#39;utente, è importante comprendere le differenze di prestazioni rispetto ad altre opzioni di topologia. Ad esempio, è possibile distribuire TarMK invece di MongoMK oppure utilizzare un archivio dati file invece di un archivio dati  Amazon S3 o Microsoft Azure.
* **Aggiunta di altri autori**: Quando la topologia TarMK consigliata non soddisfa i requisiti di prestazioni e il ridimensionamento del nodo Author ha raggiunto la capacità massima disponibile, è importante comprendere le differenze di prestazioni rispetto all&#39;utilizzo di MongoMK con tre o più nodi Author. Ad esempio, distribuzione di MongoMK invece di TarMK.
* **Aggiunta di altro contenuto**: Se l&#39;architettura dell&#39;archivio dati consigliata non soddisfa i requisiti dell&#39;utente, è importante comprendere le differenze di prestazioni rispetto alle altre opzioni dell&#39;archivio dati. Esempio: utilizzo  archivio dati di Amazon S3 o Microsoft Azure invece di un archivio dati file.

## Introduzione {#introduction}

Questo capitolo offre una panoramica generale dell&#39;architettura AEM e dei suoi componenti più importanti. Fornisce inoltre linee guida di sviluppo e descrive gli scenari di test utilizzati nei test di benchmark TarMK e MongoMK.

### La piattaforma AEM {#the-aem-platform}

La piattaforma AEM è costituita dai seguenti componenti:

![chlimage_1](assets/chlimage_1a.png)

Per ulteriori informazioni sulla piattaforma AEM, vedere [AEM](/help/sites-deploying/deploy.md#what-is-aem).

### Architettura AEM {#the-aem-architecture}

Esistono tre importanti elementi di base per una distribuzione AEM. La **Istanza autore** utilizzata da autori, editor e approvatori di contenuti per creare e rivedere i contenuti. Quando il contenuto viene approvato, viene pubblicato in un secondo tipo di istanza denominato **Istanza di pubblicazione** da cui gli utenti finali accedono. Il terzo blocco predefinito è il **Dispatcher**, un modulo che gestisce la memorizzazione nella cache e il filtraggio degli URL e che viene installato sul server Web. Per ulteriori informazioni sull&#39;architettura AEM, vedere [Scenari di distribuzione tipici](/help/sites-deploying/deploy.md#typical-deployment-scenarios).

![chlimage_1-1](assets/chlimage_1-1a.png)

### Micro kernel {#micro-kernels}

I micro kernel agiscono come persistence manager in AEM. Esistono tre tipi di microkernel utilizzati con AEM: TarMK, MongoDB e Database relazionale (con supporto limitato). La scelta di un MicroKernel adatto alle tue esigenze dipende dallo scopo della tua istanza e dal tipo di implementazione che prevedi di effettuare. Per ulteriori informazioni sui microkernel, vedere la pagina [Deployments](/help/sites-deploying/recommended-deploys.md) consigliati.

![chlimage_1-2](assets/chlimage_1-2a.png)

### Nodestore {#nodestore}

In AEM, i dati binari possono essere memorizzati indipendentemente dai nodi di contenuto. La posizione in cui sono memorizzati i dati binari è denominata **Data Store**, mentre la posizione dei nodi e delle proprietà di contenuto è denominata **Node Store**.

>[!NOTE]
>
> Adobe consiglia a TarMK di essere la tecnologia di persistenza predefinita utilizzata dai clienti sia per le istanze AEM Author che per quelle Publish.

>[!CAUTION]
>
>Supporto limitato per il Micro Kernel del database relazionale. Contattare l&#39;Assistenza clienti [ Adobe](https://helpx.adobe.com/it/marketing-cloud/contact-support.html) prima di utilizzare questo tipo di kernel Micro.

![chlimage_1-3](assets/chlimage_1-3a.png)

### Archivio dati {#data-store}

Per gestire un numero elevato di file binari, si consiglia di utilizzare un archivio dati esterno al posto degli archivi di nodi predefiniti, al fine di massimizzare le prestazioni. Ad esempio, se il progetto richiede un numero elevato di risorse multimediali, la loro memorizzazione nel file o nell&#39;archivio dati di Azure/S3 consente di accedervi più rapidamente che archiviarle direttamente all&#39;interno di un MongoDB.

Per ulteriori dettagli sulle opzioni di configurazione disponibili, vedere [Configurazione dei nodi e dei Data Store](/help/sites-deploying/data-store-config.md).

>[!NOTE]
>
> Adobe consiglia di scegliere l&#39;opzione di distribuire AEM su Azure o  Amazon Web Services (AWS) utilizzando Adobe Managed Services, dove i clienti potranno beneficiare di un team che possiede l&#39;esperienza e le capacità di implementazione e funzionamento AEM in questi ambienti cloud computing. Consultare la [documentazione aggiuntiva su Adobe Managed Services](https://www.adobe.com/marketing-cloud/enterprise-content-management/managed-services-cloud-platform.html?aemClk=t).
>
>Per consigli su come distribuire AEM su Azure o AWS, al di fuori di Adobe Managed Services, si consiglia vivamente di lavorare direttamente con il provider cloud o con uno dei nostri partner che supporta la distribuzione di AEM nell&#39;ambiente cloud di vostra scelta. Il fornitore o il partner cloud selezionato è responsabile delle specifiche di dimensionamento, della progettazione e dell&#39;implementazione dell&#39;architettura che offriranno per soddisfare i requisiti specifici di prestazioni, carico, scalabilità e sicurezza.
>
>Per ulteriori dettagli, vedere anche la pagina [Technical requirements](/help/sites-deploying/technical-requirements.md#supported-platforms).

### Ricerca {#search-features}

In questa sezione sono elencati i provider di indice personalizzati utilizzati con AEM. Per ulteriori informazioni sull&#39;indicizzazione, vedere [Query Oak e Indicizzazione](/help/sites-deploying/queries-and-indexing.md).

>[!NOTE]
>
>Per la maggior parte delle distribuzioni,  Adobe consiglia di utilizzare l&#39;indice Lucene. È consigliabile utilizzare Solr solo per la scalabilità in installazioni specializzate e complesse.

![chlimage_1-4](assets/chlimage_1-4a.png)

### Linee guida per lo sviluppo {#development-guidelines}

È necessario sviluppare per AEM mirare a **prestazioni e scalabilità**. Di seguito sono riportate una serie di best practice che potete seguire:

**ANNULLA**

* Applicare la separazione tra presentazione, logica e contenuto
* Usa le API AEM esistenti (ad esempio: Sling) e utensili (ad esempio: Replica
* Sviluppare nel contesto dei contenuti effettivi
* Sviluppare una capacità ottimale
* Riduci al minimo il numero di salvataggi (ad es.: utilizzando flussi di lavoro transitori)
* Verificate che tutti i punti finali HTTP siano RESTful
* Limitare il campo di applicazione dell&#39;osservazione JCR
* Attenzione al thread asincrono

**NON**

* Non utilizzate direttamente le API JCR, se potete
* Non modificate /libs, ma utilizzate invece le sovrapposizioni
* Non utilizzate le query quando possibile
* Non utilizzate i binding Sling per ottenere i servizi OSGi nel codice Java, ma utilizzate:

   * @Reference in a DS component
   * @Inject in a Sling Model
   * sling.getService() in una classe Sightly Use
   * sling.getService() in una JSP
   * a ServiceTracker
   * accesso diretto al registro dei servizi OSGi

Per ulteriori informazioni sullo sviluppo in AEM, leggere [Developing - The Basics](/help/sites-developing/the-basics.md) (Sviluppo - Nozioni di base). Per ulteriori best practice, vedere [Tecniche consigliate per lo sviluppo](/help/sites-developing/best-practices.md).

### Scenari di riferimento {#benchmark-scenarios}

>[!NOTE]
>
>Tutti i test di benchmark visualizzati in questa pagina sono stati eseguiti in laboratorio.

Gli scenari di test descritti di seguito sono utilizzati per le sezioni di riferimento dei capitoli TarMK, MongoMk e TarMK rispetto a MongoMk. Per vedere quale scenario è stato utilizzato per un particolare test di benchmark, leggere il campo Scenario dalla tabella [Specifiche tecniche](/help/sites-deploying/performance-guidelines.md#tarmk-performance-benchmark).

**Scenario di prodotto singolo**

AEM Assets:

* Interazioni utente: Sfoglia risorse / Cerca risorse / Scarica risorsa / Leggi metadati risorsa / Aggiorna metadati risorsa / Carica risorsa / Esegui flusso di lavoro Carica risorsa
* Modalità di esecuzione: utenti simultanei, interazione singola per utente

**Scenario prodotti misti**

 AEM Sites + Risorse:

* Interazioni utente sui siti: Pagina Leggi Articolo / Pagina Leggi / Crea paragrafo / Modifica paragrafo / Crea pagina contenuto / Attiva pagina contenuto / Ricerca autore
* Interazioni utente risorse: Sfoglia risorse / Cerca risorse / Scarica risorsa / Leggi metadati risorsa / Aggiorna metadati risorsa / Carica risorsa / Esegui flusso di lavoro Carica risorsa
* Modalità di esecuzione: utenti simultanei, interazioni miste per utente

**Scenario di utilizzo verticale**

File multimediali:

* Pagina Leggi Articolo (27,4%), Pagina Di Lettura (10,9%), Crea Sessione (2,6%), Attiva Pagina Contenuto (1,7%), Crea Pagina Contenuto (0,4%), Crea Paragrafo (4,3%), Modifica Paragrafo (0,9%), Componente Immagine (0,9%), Sfoglia Risorse (20%), Leggi Metadati Risorse (8,5%), Scarica (4,2%), Ricerca risorsa (0,2%), Aggiornamento metadati risorsa (2,4%), Caricamento risorsa (1,2%), Sfoglia progetto (4,9%), Lettura progetto (6,6%), Project Add Asset (1,2%), Project Add Site (1,2%), Creazione progetto (0,1%), Ricerca autore (0,4%)
* Modalità di esecuzione: utenti simultanei, interazioni miste per utente

## TarMK {#tarmk}

In questo capitolo vengono fornite le linee guida generali sulle prestazioni per TarMK che specificano i requisiti minimi di architettura e la configurazione delle impostazioni. Sono inoltre previsti test di riferimento per ulteriori chiarimenti.

 Adobe consiglia a TarMK di essere la tecnologia di persistenza predefinita utilizzata dai clienti in tutti gli scenari di distribuzione, sia per le istanze AEM Author che Publish.

Per ulteriori informazioni su TarMK, vedere [Scenari di distribuzione](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) e [Tar Storage](/help/sites-deploying/storage-elements-in-aem-6.md#tar-storage).

### Linee guida sull&#39;architettura minima TarMK {#tarmk-minimum-architecture-guidelines}

>[!NOTE]
>
>Le linee guida di architettura minima presentate di seguito riguardano gli ambienti di produzione e i siti a traffico elevato. Si tratta di **not** le [specifiche minime](/help/sites-deploying/technical-requirements.md#prerequisites) necessarie per eseguire AEM.

Per ottenere buone prestazioni quando si utilizza TarMK, è necessario partire dalla seguente architettura:

* Un&#39;istanza Author
* Due istanze di pubblicazione
* Due dispatcher

Di seguito sono illustrate le linee guida dell&#39;architettura per AEM siti e  AEM Assets.

>[!NOTE]
>
>La replica senza binario deve essere attivata **ON** se il datastore del file è condiviso.

**Linee guida per l&#39;architettura  AEM Sites**

![chlimage_1-5](assets/chlimage_1-5a.png)

**Linee guida per l&#39;architettura  AEM Assets**

![chlimage_1-6](assets/chlimage_1-6a.png)

### Linee guida per le impostazioni TarMK {#tarmk-settings-guideline}

Per ottenere buone prestazioni, seguite le linee guida delle impostazioni riportate di seguito. Per istruzioni su come modificare le impostazioni, vedere questa pagina[.](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)

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
   <td>Impostate il valore su metà del numero di core CPU. </td>
   <td>Per impostazione predefinita, il numero di thread simultanei per coda di processi è uguale al numero di core CPU.</td>
  </tr>
  <tr>
   <td>Coda flusso di lavoro transitorio Granite</td>
   <td><code>Max Parallel</code></td>
   <td>Impostare il valore a metà del numero di core CPU</td>
   <td> </td>
  </tr>
  <tr>
   <td>Parametri JVM</td>
   <td><p><code>Doak.queryLimitInMemory</code></p> <p><code>Doak.queryLimitReads</code></p> <p><code>Dupdate.limit</code></p> <p><code>Doak.fastQuerySize</code></p> </td>
   <td><p>500000</p> <p>100000</p> <p>250000</p> <p>Vero</p> </td>
   <td>Aggiungere questi parametri JVM nello script di avvio AEM per evitare che query estese sovraccarichino i sistemi.</td>
  </tr>
  <tr>
   <td>Configurazione indice Lucene</td>
   <td><p><code>CopyOnRead</code></p> <p><code>CopyOnWrite</code></p> <p><code>Prefetch Index Files</code></p> </td>
   <td><p>Abilitato</p> <p>Abilitato</p> <p>Abilitato</p> </td>
   <td>Per ulteriori dettagli sui parametri disponibili, vedere <a href="https://jackrabbit.apache.org/oak/docs/query/lucene.html">questa pagina</a>.</td>
  </tr>
  <tr>
   <td>Archivio dati = archivio dati S3</td>
   <td><p><code>maxCachedBinarySize</code></p> <p><code>cacheSizeInMB</code></p> </td>
   <td><p>1048576 (1 MB) o inferiore</p> <p>2-10% della dimensione massima dell'heap</p> </td>
   <td>Vedere anche <a href="/help/sites-deploying/data-store-config.md#data-store-configurations">Configurazioni archivio dati</a>.</td>
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
   <td>Questo flusso di lavoro gestisce XMP riscrittura nel binario originale e imposta l'ultima data modificata in JCR.</td>
  </tr>
 </tbody>
</table>

### Benchmark delle prestazioni TarMK {#tarmk-performance-benchmark}

#### Specifiche tecniche {#technical-specifications}

Le prove di benchmark sono state eseguite sulle seguenti specifiche:

|  | **Nodo autore** |
|---|---|
| Server | Hardware Bare metal (HP) |
| Sistema operativo | RedHat Linux |
| CPU/core | Intel(R) Xeon(R) CPU E5-2407 @2,40 GHz, 8 core |
| RAM | 32 GB |
| Disco | Magnetico |
| Java |  Oracle JRE versione 8 |
| Heap JVM | 16 GB |
| Prodotto | AEM 6.2 |
| Nodestore | TarMK |
| Datastore | File DS |
| Scenario | Prodotto singolo: Risorse / 30 thread simultanei |

#### Risultati benchmark prestazioni {#performance-benchmark-results}

>[!NOTE]
>
>I numeri riportati di seguito sono stati normalizzati a 1 come linea di base e non sono i numeri effettivi di throughput.

![chlimage_1-7 ](assets/chlimage_1-7a.png) ![chlimage_1-8](assets/chlimage_1-8a.png)

## MongoMK {#mongomk}

Il motivo principale per cui si sceglie la persistenza MongoMK al di sopra di TarMK è quello di ridimensionare le istanze orizzontalmente. Ciò significa che due o più istanze di autori attive sono sempre in esecuzione e che utilizzano MongoDB come sistema di storage persistente. La necessità di eseguire più di un&#39;istanza di autore deriva generalmente dal fatto che la CPU e la capacità di memoria di un singolo server, che supportano tutte le attività di authoring simultanee, non sono più sostenibili.

Per ulteriori informazioni su TarMK, vedere [Scenari di distribuzione](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) e [Mongo Storage](/help/sites-deploying/storage-elements-in-aem-6.md#mongo-storage).

### Linee guida sull&#39;architettura minima di MongoMK {#mongomk-minimum-architecture-guidelines}

Per ottenere buone prestazioni quando si utilizza MongoMK, è necessario partire dalla seguente architettura:

* Tre istanze Author
* Due istanze di pubblicazione
* Tre istanze MongoDB
* Due dispatcher

>[!NOTE]
>
>Negli ambienti di produzione, MongoDB sarà sempre utilizzato come set di repliche con due secondari e primario. Le letture e le scritture vanno al primo e le letture possono passare ai secondi. Se l&#39;archiviazione non è disponibile, uno dei secondari può essere sostituito con un arbitro, ma i set di repliche MongoDB devono sempre essere composti da un numero dispari di istanze.

>[!NOTE]
>
>La replica senza binario deve essere attivata **ON** se il datastore del file è condiviso.

![chlimage_1-9](assets/chlimage_1-9a.png)

### Linee guida sulle impostazioni MongoMK {#mongomk-settings-guidelines}

Per ottenere buone prestazioni, seguite le linee guida delle impostazioni riportate di seguito. Per istruzioni su come modificare le impostazioni, vedere questa pagina[.](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)

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
   <td>Impostate il valore su metà del numero di core CPU. </td>
   <td>Per impostazione predefinita, il numero di thread simultanei per coda di processi è uguale al numero di core CPU.</td>
  </tr>
  <tr>
   <td>Coda flusso di lavoro transitorio Granite</td>
   <td><code>Max Parallel</code></td>
   <td>Impostate il valore su metà del numero di core CPU.</td>
   <td> </td>
  </tr>
  <tr>
   <td>Parametri JVM</td>
   <td><p><code>Doak.queryLimitInMemory</code></p> <p><code>Doak.queryLimitReads</code></p> <p><code>Dupdate.limit</code></p> <p><code>Doak.fastQuerySize</code></p> <p><code>Doak.mongo.maxQueryTimeMS</code></p> </td>
   <td><p>500000</p> <p>100000</p> <p>250000</p> <p>Vero</p> <p>60000</p> </td>
   <td>Aggiungere questi parametri JVM nello script di avvio AEM per evitare che query estese sovraccarichino i sistemi.</td>
  </tr>
  <tr>
   <td>Configurazione indice Lucene</td>
   <td><p><code>CopyOnRead</code></p> <p><code>CopyOnWrite</code></p> <p><code>Prefetch Index Files</code></p> </td>
   <td><p>Abilitato</p> <p>Abilitato</p> <p>Abilitato</p> </td>
   <td>Per ulteriori dettagli sui parametri disponibili, vedere <a href="https://jackrabbit.apache.org/oak/docs/query/lucene.html">questa pagina</a>.</td>
  </tr>
  <tr>
   <td>Archivio dati = archivio dati S3</td>
   <td><p><code>maxCachedBinarySize</code></p> <p><code>cacheSizeInMB</code></p> </td>
   <td><p>1048576 (1 MB) o inferiore</p> <p>2-10% della dimensione massima dell'heap</p> </td>
   <td>Vedere anche <a href="/help/sites-deploying/data-store-config.md#data-store-configurations">Configurazioni archivio dati</a>.</td>
  </tr>
  <tr>
   <td>DocumentNodeStoreService</td>
   <td><p><code>cache</code></p> <p><code>nodeCachePercentage</code></p> <p><code>childrenCachePercentage</code></p> <p><code>diffCachePercentage</code></p> <p><code>docChildrenCachePercentage</code></p> <p><code>prevDocCachePercentage</code></p> <p><code>persistentCache</code></p> </td>
   <td><p>2048</p> <p>35 (25)</p> <p>20 (10)</p> <p>30 (5)</p> <p>10 (3)</p> <p>4 (4)</p> <p>./cache,size=2048,binary=0,-compact,-compress</p> </td>
   <td><p>La dimensione predefinita della cache è impostata su 256 MB.</p> <p>Ha un impatto sul tempo necessario per eseguire l'annullamento della validità della cache.</p> </td>
  </tr>
  <tr>
   <td>osservazione della quercia</td>
   <td><p><code>thread pool</code></p> <p><code>length</code></p> </td>
   <td><p>min &amp; max = 20</p> <p>50000</p> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Benchmark delle prestazioni di MongoMK {#mongomk-performance-benchmark}

### Specifiche tecniche {#technical-specifications-1}

Le prove di benchmark sono state eseguite sulle seguenti specifiche:

|  | **Nodo autore** | **Nodo MongoDB** |
|---|---|---|
| Server | Hardware Bare metal (HP) | Hardware Bare metal (HP) |
| Sistema operativo | RedHat Linux | RedHat Linux |
| CPU/core | Intel(R) Xeon(R) CPU E5-2407 @2,40 GHz, 8 core | Intel(R) Xeon(R) CPU E5-2407 @2,40 GHz, 8 core |
| RAM | 32 GB | 32 GB |
| Disco | Magnetico - >1 k IOPS | Magnetico - >1 k IOPS |
| Java |  Oracle JRE versione 8 | N/D |
| Heap JVM | 16 GB | N/D |
| Prodotto | AEM 6.2 | MongoDB 3.2 WiredTiger |
| Nodestore | MongoMK | N/D |
| Datastore | File DS | N/D |
| Scenario | Prodotto singolo: Risorse / 30 thread simultanei | Prodotto singolo: Risorse / 30 thread simultanei |

### Risultati benchmark prestazioni {#performance-benchmark-results-1}

>[!NOTE]
>
>I numeri riportati di seguito sono stati normalizzati a 1 come linea di base e non sono i numeri effettivi di throughput.

![chlimage_1-10](assets/chlimage_1-10a.png) ![chlimage_1-11](assets/chlimage_1-11a.png)

## TarMK vs MongoMK {#tarmk-vs-mongomk}

La regola di base che deve essere presa in considerazione nella scelta tra i due è che TarMK è progettato per le prestazioni, mentre MongoMK è utilizzato per la scalabilità.  Adobe consiglia a TarMK di essere la tecnologia di persistenza predefinita utilizzata dai clienti in tutti gli scenari di distribuzione, sia per le istanze AEM Author che Publish.

Il motivo principale per cui si sceglie la persistenza MongoMK al di sopra di TarMK è quello di ridimensionare le istanze orizzontalmente. Ciò significa che due o più istanze di autori attive sono sempre in esecuzione e che utilizzano MongoDB come sistema di storage persistenza. La necessità di eseguire più di un&#39;istanza di autore in genere deriva dal fatto che la CPU e la capacità di memoria di un singolo server, che supportano tutte le attività di authoring simultanee, non sono più sostenibili.

Per ulteriori dettagli su TarMK e MongoMK, vedere [Implementazioni consigliate](/help/sites-deploying/recommended-deploys.md#microkernels-which-one-to-use).

### Linee guida TarMK e MongoMk {#tarmk-vs-mongomk-guidelines}

**Vantaggi di TarMK**

* Progettato appositamente per le applicazioni di gestione dei contenuti
* I file sono sempre coerenti e possono essere sottoposti a backup utilizzando qualsiasi strumento di backup basato su file
* Offre un meccanismo di failover. Per ulteriori informazioni, vedere [Cold Standby](/help/sites-deploying/tarmk-cold-standby.md)
* Offre storage dei dati affidabile e ad alte prestazioni con costi operativi minimi
* TCO inferiore (costo totale di proprietà)

**Criteri per la scelta di MongoMK**

* Numero di utenti denominati connessi in un giorno: in migliaia o più
* Numero di utenti simultanei: a centinaia o più
* Volume di invii di risorse al giorno: in centinaia di migliaia o più
* Volume di modifiche alla pagina al giorno: in centinaia di migliaia o più
* Volume di ricerche al giorno: in decine di migliaia o più

### TarMK vs MongoMK Benchmark {#tarmk-vs-mongomk-benchmarks}

>[!NOTE]
>
>I numeri riportati di seguito sono stati normalizzati a 1 come linea di base e non sono numeri di throughput effettivi.

### Scenario 1 Specifiche tecniche {#scenario-technical-specifications}

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>Crea nodo OAK</strong></td>
   <td><strong>Nodo MongoDB</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td>Server</td>
   <td>Hardware Bare metal (HP)</td>
   <td>Hardware Bare metal (HP)</td>
   <td> </td>
  </tr>
  <tr>
   <td>Sistema operativo</td>
   <td>RedHat Linux</td>
   <td>RedHat Linux</td>
   <td> </td>
  </tr>
  <tr>
   <td>CPU/core</td>
   <td>Intel(R) Xeon(R) CPU E5-2407 @2,40 GHz, 8 core</td>
   <td>Intel(R) Xeon(R) CPU E5-2407 @2,40 GHz, 8 core</td>
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
   <td>Magnetico - &gt;1 k IOPS</td>
   <td>Magnetico - &gt;1 k IOPS</td>
   <td> </td>
  </tr>
  <tr>
   <td>Java</td>
   <td> Oracle JRE versione 8</td>
   <td>N/D</td>
   <td> </td>
  </tr>
  <tr>
   <td>Heap JVM 16 GB</td>
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

### Risultati Benchmark Prestazioni Scenario 1 {#scenario-performance-benchmark-results}

![chlimage_1-12](assets/chlimage_1-12a.png)

### Scenario 2 Specifiche tecniche {#scenario-technical-specifications-1}

>[!NOTE]
>
>Per abilitare lo stesso numero di autori con MongoDB come con un sistema TarMK, è necessario un cluster con due nodi AEM. Un cluster MongoDB a quattro nodi può gestire 1,8 volte il numero di autori rispetto a un&#39;istanza TarMK. Un cluster MongoDB a otto nodi può gestire 2,3 volte il numero di autori rispetto a un&#39;istanza TarMK.

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>Crea nodo TarMK</strong></td>
   <td><strong>Crea nodo MongoMK</strong></td>
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
   <td>RedHat Linux</td>
   <td>RedHat Linux</td>
   <td>RedHat Linux</td>
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
   <td>SSD - 10 k IOPS</td>
   <td>SSD - 10 k IOPS</td>
   <td>SSD - 10 k IOPS</td>
  </tr>
  <tr>
   <td>Java</td>
   <td> Oracle JRE versione 8</td>
   <td><br />  Oracle JRE versione 8</td>
   <td>N/D</td>
  </tr>
  <tr>
   <td>Heap JVM 16 GB</td>
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
   <td><p><br /> <br /> Caso di utilizzo verticale: Media / 2000 thread simultanei</p> </td>
   <td></td>
   <td></td>
  </tr>
 </tbody>
</table>

### Risultati Benchmark Prestazioni Scenario 2 {#scenario-performance-benchmark-results-1}

![chlimage_1-13](assets/chlimage_1-13a.png)

### Linee guida sulla scalabilità dell&#39;architettura per  AEM Sites e risorse {#architecture-scalability-guidelines-for-aem-sites-and-assets}

![chlimage_1-14](assets/chlimage_1-14a.png)

## Riepilogo delle linee guida sulle prestazioni {#summary-of-performance-guidelines}

Le linee guida presentate in questa pagina possono essere riassunte come segue:

* **TarMK con file** Datastoreè l&#39;architettura consigliata per la maggior parte dei clienti:

   * Topologia minima: un&#39;istanza Author, due istanze Publish, due Dispatcher
   * Replica senza binario attivata se il datastore file è condiviso

* **MongoMK con File** Datastoreè l&#39;architettura consigliata per la scalabilità orizzontale del livello Author:

   * Topologia minima: tre istanze Author, tre istanze MongoDB, due istanze Publish, due Dispatcher
   * Replica senza binario attivata se il datastore file è condiviso

* **I** nodi devono essere memorizzati sul disco locale, non su uno storage NAS (Network Attached Storage)
* Quando si utilizza **Amazon S3**:

   * Il datastore  Amazon S3 è condiviso tra il livello Autore e Pubblica
   * La replica senza binario deve essere attivata
   * La raccolta di dati per oggetti inattivi richiede una prima esecuzione su tutti i nodi Autore e Pubblica, quindi una seconda esecuzione su Autore

* **L&#39;indice personalizzato deve essere creato in aggiunta all&#39;indice out of the box** basato sulla maggior parte delle ricerche comuni

   * Per gli indici personalizzati è necessario utilizzare gli indici Lucene

* **La personalizzazione del flusso di lavoro può migliorare notevolmente le prestazioni**, ad esempio rimuovendo il passaggio video nel flusso di lavoro &quot;Aggiorna risorsa&quot;, disattivando i listener non utilizzati, ecc.

Per ulteriori dettagli, consultare anche la pagina [Implementazioni consigliate](/help/sites-deploying/recommended-deploys.md).
