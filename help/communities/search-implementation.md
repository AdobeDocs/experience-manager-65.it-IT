---
title: Search Essentials
seo-title: Search Essentials
description: Cerca nelle community
seo-description: Search in Communities
uuid: 5f35a033-2069-499e-9cdb-db25781312f0
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 300aa9f3-596f-42bc-8d46-e535f2bc4379
exl-id: 8af5ee58-19d7-47b6-b45d-e88006703a5d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1184'
ht-degree: 4%

---

# Search Essentials {#search-essentials}

## Panoramica {#overview}

La funzione di ricerca è una funzione essenziale di AEM Communities. Oltre al [Ricerca per piattaforma AEM](../../help/sites-deploying/queries-and-indexing.md) funzionalità, AEM Communities fornisce [API di ricerca UGC](#ugc-search-api) ai fini della ricerca di contenuti generati dagli utenti (UGC, User Generated Content). UGC ha proprietà univoche in quanto viene immesso e memorizzato separatamente dagli altri contenuti e dati utente dell’AEM.

Per le comunità, le due cose generalmente cercate sono:

* Contenuto pubblicato dai membri della community

   * Utilizza l’API di ricerca UGC di AEM Communities.

* Utenti e gruppi di utenti (dati utente)

   * Utilizza le funzionalità di ricerca della piattaforma AEM.

Questa sezione della documentazione è interessante per gli sviluppatori che creano componenti personalizzati per la creazione o la gestione di contenuti generati dagli utenti (UGC, User-Generated Content).

## Sicurezza e nodi ombra {#security-and-shadow-nodes}

Per un componente personalizzato, è necessario utilizzare [UtilitàRisorseSocial](socialutils.md#socialresourceutilities-package) metodi. I metodi di utilità che creano e cercano UGC stabiliranno il [nodi shadow](srp.md#about-shadow-nodes-in-jcr) e accertarsi che il membro disponga delle autorizzazioni corrette per la richiesta.

Ciò che non viene gestito tramite le utility SRP sono proprietà relative alla moderazione.

Consulta [Nozioni di base su SRP e UGC](srp-and-ugc.md) per informazioni sui metodi di utilità utilizzati per accedere ai nodi ombra UGC e ACL.

## API di ricerca UGC {#ugc-search-api}

Il [Archivio comune UGC](working-with-srp.md) viene fornito da uno dei diversi provider di risorse di archiviazione (SRP), ciascuno dei quali può disporre di una lingua di query nativa diversa. Pertanto, indipendentemente dall&#39;SRP scelto, il codice personalizzato deve utilizzare i metodi dell&#39; [Pacchetto API UGC](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) (*com.adobe.cq.social.ugc.api*) che richiamerà il linguaggio di query appropriato per l&#39;SRP scelto.

### Ricerche ASRP {#asrp-searches}

Per [ASRP](asrp.md), UGC è memorizzato nel cloud di Adobe. Mentre UGC non è visibile in CRX, [moderazione](moderate-ugc.md) è disponibile sia dall’ambiente di authoring che da quello di pubblicazione. L&#39;uso del [API di ricerca UGC](#ugc-search-api) funziona per ASRP allo stesso modo degli altri SRP.

Al momento non esistono strumenti per la gestione delle ricerche ASRP.

Quando si creano proprietà personalizzate ricercabili, è necessario aderire al [requisiti di denominazione](#naming-of-custom-properties).

### Ricerche MSRP {#msrp-searches}

Per [MSRP](msrp.md), UGC viene memorizzato in MongoDB configurato per l’utilizzo di Solr per la ricerca. UGC non sarà visibile in CRX, ma [moderazione](moderate-ugc.md) è disponibile sia dall’ambiente di authoring che da quello di pubblicazione.

Per quanto riguarda MSRP e Solr:

* La Solr incorporata per la piattaforma AEM non viene utilizzata per la MSRP.
* Se si utilizza una Solr remota per la piattaforma AEM, questa può essere condivisa con MSRP, ma è necessario che utilizzino raccolte diverse.
* Solr può essere configurato per la ricerca standard o per la ricerca multilingue (MLS).
* Per informazioni dettagliate sulla configurazione, consulta [Configurazione Solr](msrp.md#solr-configuration) per MSRP.

Le funzioni di ricerca personalizzate devono utilizzare [API di ricerca UGC](#ugc-search-api).

Quando si creano proprietà personalizzate ricercabili, è necessario aderire al [requisiti di denominazione](#naming-of-custom-properties).

### Ricerche JSRP {#jsrp-searches}

Per [JSRP](jsrp.md), UGC è memorizzato in [Oak](../../help/sites-deploying/platform.md) ed è visibile solo nell’archivio dell’istanza di authoring o pubblicazione AEM in cui è stata immessa.

Poiché UGC viene in genere immesso nell’ambiente di pubblicazione, per i sistemi di produzione con più editori è necessario configurare un [cluster di pubblicazione](topologies.md), non una farm di pubblicazione, in modo che il contenuto immesso sia visibile da tutti gli editori.

Per JSRP, le UGC immesse nell’ambiente di pubblicazione non saranno mai visibili nell’ambiente di authoring. Così tutto [moderazione](moderate-ugc.md) Le attività di vengono eseguite nell’ambiente di pubblicazione.

Le funzioni di ricerca personalizzate devono utilizzare [API di ricerca UGC](#ugc-search-api).

#### Indicizzazione Oak {#oak-indexing}

Gli indici Oak non vengono creati automaticamente per la ricerca della piattaforma AEM, ma a partire da AEM 6.2 sono stati aggiunti per consentire ad AEM Communities di migliorare le prestazioni e fornire supporto per l’impaginazione durante la presentazione dei risultati della ricerca UGC.

Se le proprietà personalizzate sono in uso e le ricerche sono lente, è necessario creare indici aggiuntivi per le proprietà personalizzate per renderle più performanti. Per mantenere la portabilità, attieniti alla [requisiti di denominazione](#naming-of-custom-properties) durante la creazione di proprietà personalizzate ricercabili.

Per modificare gli indici esistenti o creare indici personalizzati, fare riferimento a [Query e indicizzazione Oak](../../help/sites-deploying/queries-and-indexing.md).

Il [Gestore indice Oak](https://adobe-consulting-services.github.io/acs-aem-commons/features/oak-index-manager.html) è disponibile da ACS AEM Commons. Esso prevede:

* Una visualizzazione degli indici esistenti.
* Possibilità di avviare la reindicizzazione.

Per visualizzare gli indici Oak esistenti in [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md), il percorso è:

* `/oak:index/socialLucene`

![social-lucene](assets/social-lucene.png)

## Proprietà ricerca indicizzata {#indexed-search-properties}

### Proprietà di ricerca predefinite {#default-search-properties}

Di seguito sono riportate alcune delle proprietà ricercabili utilizzate per varie funzioni di Communities:

| **Proprietà** | **Tipo di dati** |
|---|---|
| isFlagged | *Booleano* |
| isSpam | *Booleano* |
| letto | *Booleano* |
| influenza | *Booleano* |
| allegati | *Booleano* |
| sentiment | *Lungo* |
| contrassegnato | *Booleano* |
| aggiunto | *Data* |
| modifiedDate | *Data* |
| stadio | *Stringa* |
| userIdentifier | *Stringa* |
| risposte | *Lungo* |
| jcr:title | *Stringa* |
| jcr:descrizione | *Stringa* |
| sling:resourceType | *Stringa* |
| allowThreadedReply | *Booleano* |
| isDraft | *Booleano* |
| publishDate | *Data* |
| publishJobId | *Stringa* |
| ha risposto | *Booleano* |
| chosenanswer | *Booleano* |
| tag | *Stringa* |
| cq:Tag | *Stringa* |
| author_display_name | *Stringa* |
| location_t | *Stringa* |
| parentPath | *Stringa* |
| parentTitle | *Stringa* |

### Denominazione delle proprietà personalizzate {#naming-of-custom-properties}

Quando si aggiungono proprietà personalizzate, affinché siano visibili agli ordinamenti e alle ricerche creati con [API di ricerca UGC](#ugc-search-api), è *obbligatorio* per aggiungere un suffisso al nome della proprietà.

Il suffisso è per i linguaggi di query che utilizzano uno schema:

* Identifica la proprietà come ricercabile.
* Identifica il tipo di dati.

Solr è un esempio di linguaggio di query che utilizza uno schema.

| **Suffisso** | **Tipo di dati** |
|---|---|
| _b | *Booleano* |
| _dt | *Calendario* |
| _d | *Doppio* |
| _tl | *Lungo* |
| _s | *Stringa* |
| _t | *Testo* |

**Note:**

* *Testo* è una stringa tokenizzata, *Stringa* non lo è. Utilizzare *Testo* per ricerche fuzzy (più simili).

* Per i tipi con più valori, aggiungi &quot;s&quot; al suffisso, ad esempio:

   * `viewDate_dt`: proprietà data singola
   * `viewDates_dts`: proprietà list of dates

## Filtri {#filters}

Componenti che includono [sistema di commenti](essentials-comments.md) supporta l’aggiunta del parametro di filtro ai relativi endpoint.

La sintassi del filtro per la logica AND e OR è espressa come segue (visualizzata prima dell’URL codificato):

* Per specificare OR, utilizza un parametro di filtro con valori separati da virgola:

   * `filter=name eq 'Jennifer',name eq 'Jen'`

* Per specificare E utilizzare più parametri di filtro:

   * `filter = name eq 'Jackson'&filter=message eq 'testing'`

L&#39;implementazione predefinita del [Componente di ricerca](search.md) utilizza questa sintassi come mostrato nell’URL che apre la pagina Risultati ricerca in [Guida ai componenti della community](components-guide.md). Per fare delle prove, passa a [http://localhost:4503/content/community-components/en/search.html](http://localhost:4503/content/community-components/en/search.html).

Gli operatori filtro sono:

| EQ | è uguale a |
|---|---|
| NE | diverso da |
| LT | minore di |
| LTE | minore o uguale a |
| GE | maggiore di |
| GTE | maggiore o uguale a |
| MI PIACE | corrispondenza sfocata |

È importante che l’URL faccia riferimento al componente Communities (risorsa) e non alla pagina in cui il componente viene inserito:

* Corretto: componente forum
   * `/content/community-components/en/forum/jcr:content/content/forum.social.json`
* Pagina forum errata
   * `/content/community-components/en/forum.social.json`

## Strumenti SRP {#srp-tools}

Esiste un progetto GitHub Adobe Marketing Cloud che contiene:

[Strumenti AEM Communities SRP](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

Questo archivio contiene strumenti per la gestione dei dati in SRP.

Attualmente, esiste un servlet che consente di eliminare tutti i contenuti UGC da qualsiasi SRP.

Ad esempio, per eliminare tutti i contenuti generati dagli utenti (UGC) in ASRP:

```shell
curl -X POST http://localhost:4502/services/social/srp/cleanup?path=/content/usergenerated/asi/cloud -uadmin:admin
```

## Risoluzione dei problemi {#troubleshooting}

### Query Solr {#solr-query}

Per facilitare la risoluzione dei problemi relativi a una query Solr, abilitare la registrazione DEBUG per

`com.adobe.cq.social.srp.impl.SocialSolrConnector`.

La query Solr effettiva verrà visualizzata con l’URL codificato nel registro di debug:

Query da avviare: `sort=timestamp+desc&bl=en&pl=en&start=0&rows=10 &q=%2Btitle_t:(hello)+%2Bprovider_id:\/content/usergenerated/asi/mongo/content/+%2Bresource_type_s:&df=provider_id&trf=verbatim&fq={!cost%3D100}report_suite:mongo`

Il valore della proprietà `q` Il parametro è la query. Una volta decodificata la codifica URL, la query può essere passata allo strumento Solr Admin Query per ulteriori operazioni di debug.

## Risorse correlate {#related-resources}

* [Archiviazione contenuti community](working-with-srp.md) - Descrive le scelte SRP disponibili per un archivio comune UGC.
* [Panoramica del provider di risorse di archiviazione](srp.md) - Introduzione e panoramica sull’utilizzo dell’archivio.
* [Accesso a UGC con SRP](accessing-ugc-with-srp.md) - Linee guida per la codifica.
* [Refactoring SocialUtils](socialutils.md) - Metodi di utilità per SRP che sostituiscono SocialUtils.
* [Componenti Risultati di ricerca e ricerca](search.md) - Aggiunta della funzione di ricerca UGC a un modello.
