---
title: Search Essentials
description: Scopri la funzione di ricerca, una funzionalità essenziale di AEM Communities. Le community forniscono anche l’API di ricerca per contenuti generati dall’utente.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8af5ee58-19d7-47b6-b45d-e88006703a5d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 3%

---

# Search Essentials {#search-essentials}

## Panoramica {#overview}

La funzione di ricerca è una caratteristica essenziale delle community Adobe Experience Manager (AEM). Oltre alle funzionalità di [ricerca per piattaforma AEM](../../help/sites-deploying/queries-and-indexing.md), AEM Communities fornisce [API di ricerca UGC](#ugc-search-api) per la ricerca di contenuti generati dagli utenti (UGC, User-Generated Content). UGC ha proprietà univoche in quanto viene immesso e memorizzato separatamente dagli altri contenuti e dati utente dell’AEM.

Per le comunità, le due cose generalmente cercate sono:

* Contenuto pubblicato dai membri della community

   * Utilizza l’API di ricerca UGC di AEM Communities.

* Utenti e gruppi di utenti (dati utente)

   * Utilizza le funzionalità di ricerca della piattaforma AEM.

Questa sezione della documentazione è interessante per gli sviluppatori che creano componenti personalizzati per la creazione o la gestione di contenuti generati dagli utenti (UGC, User-Generated Content).

## Sicurezza e nodi ombra {#security-and-shadow-nodes}

Per un componente personalizzato, è necessario utilizzare i metodi [SocialResourceUtilities](socialutils.md#socialresourceutilities-package). I metodi di utilità che creano e cercano UGC stabiliscono i [nodi shadow](srp.md#about-shadow-nodes-in-jcr) richiesti e garantiscono che il membro disponga delle autorizzazioni corrette per la richiesta.

Ciò che non viene gestito tramite le utility SRP sono proprietà relative alla moderazione.

Per informazioni sui metodi di utilità utilizzati per accedere ai nodi shadow UGC e ACL, vedere [SRP e UGC Essentials](srp-and-ugc.md).

## API di ricerca UGC {#ugc-search-api}

L&#39;archivio comune [UGC](working-with-srp.md) è fornito da uno dei vari provider di risorse di archiviazione (SRP), ciascuno con un linguaggio di query nativo diverso. Pertanto, indipendentemente dall&#39;SRP scelto, il codice personalizzato deve utilizzare i metodi del pacchetto API [UGC](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) (*com.adobe.cq.social.ugc.api*) che richiama il linguaggio di query appropriato per l&#39;SRP scelto.

### Ricerche ASRP {#asrp-searches}

Per [ASRP](asrp.md), UGC è archiviato nel cloud Adobe. Anche se UGC non è visibile in CRX, [moderation](moderate-ugc.md) è disponibile sia dall&#39;ambiente di authoring che da quello di Publish. L&#39;utilizzo dell&#39;[API di ricerca UGC](#ugc-search-api) funziona per ASRP allo stesso modo degli altri SRP.

Al momento non esistono strumenti per la gestione delle ricerche ASRP.

Durante la creazione di proprietà personalizzate ricercabili, è necessario rispettare i [requisiti di denominazione](#naming-of-custom-properties).

### Ricerche MSRP {#msrp-searches}

Per [MSRP](msrp.md), UGC è archiviato in MongoDB configurato per l&#39;utilizzo di Solr per la ricerca. UGC non è visibile in CRX, ma [moderation](moderate-ugc.md) è disponibile sia dall&#39;ambiente di authoring che da quello di Publish.

Per quanto riguarda MSRP e Solr:

* La Solr incorporata per la piattaforma AEM non viene utilizzata per la MSRP.
* Se si utilizza una Solr remota per la piattaforma AEM, questa può essere condivisa con MSRP, ma è necessario che utilizzino raccolte diverse.
* Solr può essere configurato per la ricerca standard o per la ricerca multilingue (MLS).
* Per informazioni dettagliate sulla configurazione, vedere [Configurazione Solr](msrp.md#solr-configuration) per MSRP.

Le funzionalità di ricerca personalizzate devono utilizzare l&#39;[API di ricerca UGC](#ugc-search-api).

Durante la creazione di proprietà personalizzate ricercabili, è necessario rispettare i [requisiti di denominazione](#naming-of-custom-properties).

### Ricerche JSRP {#jsrp-searches}

Per [JSRP](jsrp.md), UGC è archiviato in [Oak](../../help/sites-deploying/platform.md) ed è visibile solo nell&#39;archivio dell&#39;istanza di Publish o di creazione AEM in cui è stato immesso.

Poiché UGC viene in genere immesso nell&#39;ambiente Publish, per i sistemi di produzione con più editori è necessario configurare un cluster di pubblicazione [](topologies.md), non una farm di pubblicazione, in modo che il contenuto immesso sia visibile da tutti gli editori.

Per JSRP, le voci UGC immesse nell’ambiente Publish non sono mai visibili nell’ambiente di authoring. Pertanto, tutte le [attività di moderazione](moderate-ugc.md) si svolgono nell&#39;ambiente Publish.

Le funzionalità di ricerca personalizzate devono utilizzare l&#39;[API di ricerca UGC](#ugc-search-api).

#### Indicizzazione Oak {#oak-indexing}

Sebbene gli indici Oak non vengano creati automaticamente per la ricerca della piattaforma AEM, a partire dalla versione 6.2 dell’AEM sono stati aggiunti per consentire ad AEM Communities di migliorare le prestazioni e supportare l’impaginazione durante la presentazione dei risultati della ricerca UGC.

Se le proprietà personalizzate sono in uso e le ricerche sono lente, è necessario creare indici aggiuntivi per le proprietà personalizzate per renderle più performanti. Per mantenere la portabilità, attieniti ai [requisiti di denominazione](#naming-of-custom-properties) durante la creazione di proprietà personalizzate ricercabili.

Per modificare gli indici esistenti o creare indici personalizzati, vedere [Query e indicizzazione di Oak](../../help/sites-deploying/queries-and-indexing.md).

[Gestione indice Oak](https://adobe-consulting-services.github.io/acs-aem-commons/features/oak-index-manager.html) è disponibile da ACS AEM Commons. Esso prevede:

* Una visualizzazione degli indici esistenti.
* La capacità di avviare la reindicizzazione.

Per visualizzare gli indici Oak esistenti in [CRXDE Liti](../../help/sites-developing/developing-with-crxde-lite.md), il percorso è:

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
| stato | *Stringa* |
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

Quando si aggiungono proprietà personalizzate, affinché siano visibili agli ordinamenti e alle ricerche creati con [UGC search API](#ugc-search-api), è *obbligatorio* aggiungere un suffisso al nome della proprietà.

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

* *Il testo* è una stringa tokenizzata, *La stringa* non lo è. Utilizza *Testo* per ricerche fuzzy (come questa).

* Per i tipi con più valori, aggiungi &quot;s&quot; al suffisso, ad esempio:

   * `viewDate_dt`: proprietà data singola
   * `viewDates_dts`: proprietà list of dates

## Filtri {#filters}

I componenti, che includono il [sistema di commenti](essentials-comments.md), supportano il parametro di filtro oltre ai relativi endpoint.

La sintassi del filtro per la logica AND e OR è espressa come segue (visualizzata prima dell’URL codificato):

* Per specificare OR, utilizza un parametro di filtro con valori separati da virgola:

   * `filter=name eq 'Jennifer',name eq 'Jen'`

* Per specificare E utilizzare più parametri di filtro:

   * `filter = name eq 'Jackson'&filter=message eq 'testing'`

L&#39;implementazione predefinita del [componente Ricerca](search.md) utilizza questa sintassi, come riportato nell&#39;URL che apre la pagina Risultati ricerca nella [guida dei componenti community](components-guide.md). Per fare delle prove, passa a [http://localhost:4503/content/community-components/en/search.html](http://localhost:4503/content/community-components/en/search.html).

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

Esiste un progetto GitHub Adobe Experience Cloud che contiene:

[Strumenti AEM Communities SRP](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

Questo archivio contiene strumenti per la gestione dei dati in SRP.

Attualmente, esiste un servlet che può eliminare tutti i contenuti UGC da qualsiasi SRP.

Ad esempio, per eliminare tutti i contenuti generati dagli utenti (UGC) in ASRP:

```shell
curl -X POST http://localhost:4502/services/social/srp/cleanup?path=/content/usergenerated/asi/cloud -uadmin:admin
```

## Risoluzione dei problemi {#troubleshooting}

### Query Solr {#solr-query}

Per facilitare la risoluzione dei problemi relativi a una query Solr, abilitare la registrazione DEBUG per

`com.adobe.cq.social.srp.impl.SocialSolrConnector`.

La query Solr effettiva viene visualizzata con l’URL codificato nel registro di debug:

Query da solr: `sort=timestamp+desc&bl=en&pl=en&start=0&rows=10 &q=%2Btitle_t:(hello)+%2Bprovider_id:\/content/usergenerated/asi/mongo/content/+%2Bresource_type_s:&df=provider_id&trf=verbatim&fq={!cost%3D100}report_suite:mongo`

Il valore del parametro `q` è la query. Una volta decodificata la codifica URL, la query può essere passata allo strumento Solr Admin Query per ulteriori operazioni di debug.

## Risorse correlate {#related-resources}

* [Archiviazione contenuto community](working-with-srp.md): illustra le scelte SRP disponibili per un archivio comune UGC.
* [Panoramica del provider di risorse di archiviazione](srp.md) - Introduzione e panoramica sull&#39;utilizzo dell&#39;archivio.
* [Accesso a UGC con SRP](accessing-ugc-with-srp.md) - Linee guida per la codifica.
* [Refactoring SocialUtils](socialutils.md) - Metodi di utilità per SRP che sostituiscono SocialUtils.
* [Componenti risultati ricerca e ricerca](search.md) - Aggiunta della funzionalità di ricerca UGC a un modello.
