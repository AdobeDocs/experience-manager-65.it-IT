---
title: Nozioni di base sulla ricerca
seo-title: Search Essentials
description: Cerca in Communities
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
ht-degree: 5%

---

# Nozioni di base sulla ricerca {#search-essentials}

## Panoramica {#overview}

La funzione di ricerca è una funzione essenziale di AEM Communities. Oltre al [Ricerca su piattaforma AEM](../../help/sites-deploying/queries-and-indexing.md) AEM Communities fornisce [API di ricerca UGC](#ugc-search-api) allo scopo di cercare contenuti generati dall’utente (UGC). UGC ha proprietà univoche in quanto viene immesso e memorizzato separatamente dagli altri contenuti AEM e dati utente.

Per Communities, i due elementi generalmente ricercati sono:

* Contenuto pubblicato da membri della community

   * Utilizza l’API di ricerca UGC di AEM Communities.

* Utenti e gruppi di utenti (dati utente)

   * Utilizza le funzionalità di ricerca della piattaforma AEM.

Questa sezione della documentazione è di interesse per gli sviluppatori che creano componenti personalizzati che creano o gestiscono UGC.

## Nodi di sicurezza e ombreggiatura {#security-and-shadow-nodes}

Per un componente personalizzato, è necessario utilizzare il [SocialResourceUtilities](socialutils.md#socialresourceutilities-package) metodi. I metodi di utilità che creano e cercano UGC stabiliranno i requisiti richiesti [nodi ombra](srp.md#about-shadow-nodes-in-jcr) e assicurati che il membro disponga delle autorizzazioni corrette per la richiesta.

Ciò che non viene gestito tramite le utility SRP sono proprietà correlate alla moderazione.

Vedi [Essenze SRP e UGC](srp-and-ugc.md) per informazioni sui metodi di utilità utilizzati per accedere ai nodi shadow UGC e ACL.

## API di ricerca UGC {#ugc-search-api}

La [Archivio comune UGC](working-with-srp.md) è fornito da uno dei vari provider di risorse di archiviazione (SRP), ognuno dei quali può avere un linguaggio di query nativo diverso. Pertanto, indipendentemente dall’SRP scelto, il codice personalizzato deve utilizzare i metodi della [Pacchetto API UGC](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) (*com.adobe.cq.social.ugc.api*) che richiamerà il linguaggio di query appropriato per l’SRP scelto.

### Ricerche ASRP {#asrp-searches}

Per [ASRP](asrp.md), UGC viene memorizzato in Adobe cloud. Mentre UGC non è visibile in CRX, [moderazione](moderate-ugc.md) è disponibile sia negli ambienti di authoring che di pubblicazione. L&#39;uso del [API di ricerca UGC](#ugc-search-api) funziona per ASRP come per altri SRP.

Al momento non esistono strumenti per la gestione delle ricerche ASRP.

Quando si creano proprietà personalizzate ricercabili, è necessario aderire al [requisiti di denominazione](#naming-of-custom-properties).

### Ricerche MSRP {#msrp-searches}

Per [MSRP](msrp.md), UGC viene memorizzato in MongoDB configurato per utilizzare Solr per la ricerca. UGC non sarà visibile in CRX, ma [moderazione](moderate-ugc.md) è disponibile sia negli ambienti di authoring che di pubblicazione.

Per quanto riguarda MSRP e Solr:

* Il Solr incorporato per la piattaforma AEM non viene utilizzato per MSRP.
* Se si utilizza un Solr remoto per la piattaforma AEM, può essere condiviso con MSRP, ma deve utilizzare raccolte diverse.
* Solr può essere configurato per la ricerca standard o per la ricerca multilingue (MLS).
* Per informazioni dettagliate sulla configurazione, consulta [Configurazione Solr](msrp.md#solr-configuration) per MSRP.

Le funzioni di ricerca personalizzate devono utilizzare [API di ricerca UGC](#ugc-search-api).

Quando si creano proprietà personalizzate ricercabili, è necessario aderire al [requisiti di denominazione](#naming-of-custom-properties).

### Ricerche JSRP {#jsrp-searches}

Per [JSRP](jsrp.md)UGC è memorizzato in [Oak](../../help/sites-deploying/platform.md) ed è visibile solo nell’archivio dell’istanza di authoring o pubblicazione AEM in cui è stato inserito.

Poiché l’UGC viene generalmente immesso nell’ambiente di pubblicazione per i sistemi di produzione con più editori, è necessario configurare un [pubblicare un cluster](topologies.md), non una farm di pubblicazione, in modo che il contenuto immesso sia visibile da tutti gli editori.

Per JSRP, l’UGC immesso nell’ambiente di pubblicazione non sarà mai visibile nell’ambiente di authoring. Così tutti [moderazione](moderate-ugc.md) le attività vengono eseguite nell’ambiente di pubblicazione.

Le funzioni di ricerca personalizzate devono utilizzare [API di ricerca UGC](#ugc-search-api).

#### Indicizzazione Oak {#oak-indexing}

Sebbene gli indici Oak non vengano creati automaticamente per la ricerca della piattaforma AEM, a partire dalla AEM 6.2 sono stati aggiunti per AEM Communities per migliorare le prestazioni e fornire il supporto per l’impaginazione durante la presentazione dei risultati della ricerca UGC.

Se le proprietà personalizzate sono in uso e le ricerche sono lente, è necessario creare indici aggiuntivi affinché le proprietà personalizzate siano più performanti. Per mantenere la portabilità, fai riferimento al [requisiti di denominazione](#naming-of-custom-properties) durante la creazione di proprietà personalizzate ricercabili.

Per modificare gli indici esistenti o creare indici personalizzati, consulta [Query e indicizzazione Oak](../../help/sites-deploying/queries-and-indexing.md).

La [Gestione indici Oak](https://adobe-consulting-services.github.io/acs-aem-commons/features/oak-index-manager.html) è disponibile da ACS AEM Commons. Fornisce:

* Visualizzazione degli indici esistenti.
* La capacità di avviare la reindicizzazione.

Per visualizzare gli indici Oak esistenti in [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md), la posizione è:

* `/oak:index/socialLucene`

![social-lucene](assets/social-lucene.png)

## Proprietà di ricerca indicizzate {#indexed-search-properties}

### Proprietà di ricerca predefinite {#default-search-properties}

Di seguito sono riportate alcune delle proprietà ricercabili utilizzate per varie funzioni di Communities:

| **Proprietà** | **Tipo di dati** |
|---|---|
| isFlagged | *Booleano* |
| isSpam | *Booleano* |
| read | *Booleano* |
| influenza | *Booleano* |
| allegati | *Booleano* |
| sentimento | *Lungo* |
| contrassegnato | *Booleano* |
| aggiunto | *Data* |
| modifiedDate | *Data* |
| stadio | *Stringa* |
| userIdentifier | *Stringa* |
| risposte | *Lungo* |
| jcr:title | *Stringa* |
| jcr:description | *Stringa* |
| sling:resourceType | *Stringa* |
| allowThreadedReply | *Booleano* |
| isDraft | *Booleano* |
| publishDate | *Data* |
| publishJobId | *Stringa* |
| ha risposto | *Booleano* |
| scettico | *Booleano* |
| tag | *Stringa* |
| cq:Tag | *Stringa* |
| author_display_name | *Stringa* |
| location_t | *Stringa* |
| parentPath | *Stringa* |
| parentTitle | *Stringa* |

### Denominazione delle proprietà personalizzate {#naming-of-custom-properties}

Quando si aggiungono proprietà personalizzate, affinché tali proprietà siano visibili agli ordini e alle ricerche creati con [API di ricerca UGC](#ugc-search-api), *obbligatorio* per aggiungere un suffisso al nome della proprietà.

Il suffisso è destinato ai linguaggi di query che utilizzano uno schema:

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

* *Testo* è una stringa token, *Stringa* non lo è. Utilizzo *Testo* cerca fuzzy (più così) ricerche.

* Per i tipi con più valori, aggiungi &quot;s&quot; al suffisso, ad esempio:

   * `viewDate_dt`: proprietà data singola
   * `viewDates_dts`: list date, proprietà

## Filtri {#filters}

Componenti che includono [sistema di commento](essentials-comments.md) supporta l’aggiunta del parametro del filtro ai relativi endpoint.

La sintassi del filtro per la logica AND e OR viene espressa come segue (mostrato prima di essere codificato nell’URL):

* Per specificare OR utilizzare un parametro di filtro con valori separati da virgole:

   * `filter=name eq 'Jennifer',name eq 'Jen'`

* Per specificare e utilizzare più parametri di filtro:

   * `filter = name eq 'Jackson'&filter=message eq 'testing'`

Implementazione predefinita del [Componente di ricerca](search.md) utilizza questa sintassi come è possibile vedere nell’URL che apre la pagina Risultati ricerca nel [Guida ai componenti della community](components-guide.md). Per sperimentare, sfoglia fino a [http://localhost:4503/content/community-components/en/search.html](http://localhost:4503/content/community-components/en/search.html).

Gli operatori di filtro sono:

| EQ | è uguale a |
|---|---|
| NE | non è uguale a |
| LT | inferiore a |
| LTE | minore o uguale a |
| GE | maggiore di |
| GTE | maggiore o uguale a |
| LIKE | abbinamento sfuocato |

È importante che l’URL faccia riferimento al componente Community (risorsa) e non alla pagina in cui è posizionato il componente:

* Corretto: componente forum
   * `/content/community-components/en/forum/jcr:content/content/forum.social.json`
* Errato: pagina forum
   * `/content/community-components/en/forum.social.json`

## Strumenti SRP {#srp-tools}

Esiste un progetto GitHub Adobe Marketing Cloud che contiene:

[Strumenti AEM Communities SRP](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

Questo archivio contiene strumenti per la gestione dei dati nell’SRP.

Attualmente, esiste un servlet che offre la possibilità di eliminare tutti gli UGC da qualsiasi SRP.

Ad esempio, per eliminare tutti gli UGC nell’ASRP:

```shell
curl -X POST http://localhost:4502/services/social/srp/cleanup?path=/content/usergenerated/asi/cloud -uadmin:admin
```

## Risoluzione dei problemi {#troubleshooting}

### Query Solr {#solr-query}

Per risolvere i problemi relativi a una query Solr, abilita la registrazione DEBUG per

`com.adobe.cq.social.srp.impl.SocialSolrConnector`.

La query Solr effettiva verrà visualizzata con URL codificato nel registro di debug:

La query da solr è: `sort=timestamp+desc&bl=en&pl=en&start=0&rows=10 &q=%2Btitle_t:(hello)+%2Bprovider_id:\/content/usergenerated/asi/mongo/content/+%2Bresource_type_s:&df=provider_id&trf=verbatim&fq={!cost%3D100}report_suite:mongo`

Il valore del `q` è la query. Una volta decodificata la codifica URL, la query può essere passata allo strumento Solr Admin Query per un ulteriore debug.

## Risorse correlate {#related-resources}

* [Archiviazione dei contenuti della community](working-with-srp.md) - Descrive le scelte SRP disponibili per un archivio comune UGC.
* [Panoramica del provider di risorse di storage](srp.md) - Introduzione e panoramica sull’utilizzo dell’archivio.
* [Accesso a UGC con SRP](accessing-ugc-with-srp.md) - Linee guida per la codifica.
* [Refactoring di SocialUtils](socialutils.md) - Metodi di utilità per SRP che sostituiscono SocialUtils.
* [Componenti per risultati di ricerca](search.md) - Aggiunta di una funzione di ricerca UGC a un modello.
