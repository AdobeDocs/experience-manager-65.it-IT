---
title: Ricerca Essentials
seo-title: Ricerca Essentials
description: Cerca in Communities
seo-description: Cerca in Communities
uuid: 5f35a033-2069-499e-9cdb-db25781312f0
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 300aa9f3-596f-42bc-8d46-e535f2bc4379
translation-type: tm+mt
source-git-commit: 9a4ae73c08657195da2741cccdb196bd7f7142c9
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 5%

---


# Ricerca Essentials {#search-essentials}

## Panoramica {#overview}

La funzione di ricerca è una caratteristica essenziale di  AEM Communities. Oltre alle funzionalità di [AEM piattaforma di ricerca](../../help/sites-deploying/queries-and-indexing.md),  AEM Communities fornisce l&#39;API di ricerca [UGC](#ugc-search-api) allo scopo di ricercare contenuti generati dall&#39;utente (UGC). UGC ha proprietà univoche in quanto viene immesso e memorizzato separatamente da altri contenuti AEM e dati utente.

Per Community, le due operazioni generalmente ricercate sono:

* Contenuto pubblicato dai membri della community

   * Utilizza l&#39;API di ricerca UGC di AEM Communities.

* Utenti e gruppi di utenti (dati utente)

   * Utilizza le funzionalità di ricerca della piattaforma AEM.

Questa sezione della documentazione interessa gli sviluppatori che creano componenti personalizzati per la creazione o la gestione di UGC.

## Nodi di sicurezza e ombreggiatura {#security-and-shadow-nodes}

Per un componente personalizzato, è necessario utilizzare i metodi [SocialResourceUtilities](socialutils.md#socialresourceutilities-package). I metodi di utilità che creano e ricercano UGC stabiliranno i [nodi shadow](srp.md#about-shadow-nodes-in-jcr) richiesti e si assicureranno che il membro disponga delle autorizzazioni corrette per la richiesta.

Ciò che non viene gestito tramite le utility SRP sono proprietà correlate alla moderazione.

Per informazioni sui metodi di utilità utilizzati per accedere ai nodi ombra UGC e ACL, vedere [SRP e UGC Essentials](srp-and-ugc.md).

## API di ricerca UGC {#ugc-search-api}

L&#39; [archivio comune UGC](working-with-srp.md) è fornito da uno dei vari provider di risorse di storage (SRP), ognuno dei quali può avere una lingua di query nativa diversa. Pertanto, indipendentemente dall&#39;SRP scelto, il codice personalizzato deve utilizzare i metodi del [pacchetto API UGC](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) (*com.adobe.cq.social.ugc.api*) che richiameranno il linguaggio di query appropriato per l&#39;SRP scelto.

### Ricerche ASRP {#asrp-searches}

Per [ASRP](asrp.md), UGC è memorizzato nel cloud di Adobi . Sebbene l&#39;UGC non sia visibile in CRX, [moderazione](moderate-ugc.md) è disponibile sia dall&#39;ambiente di creazione che da quello di pubblicazione. L&#39;utilizzo dell&#39;API di ricerca [UGC](#ugc-search-api) funziona per ASRP come per altri SRP.

Al momento non esistono strumenti per gestire le ricerche ASRP.

Quando si creano proprietà personalizzate ricercabili, è necessario aderire ai [requisiti di denominazione](#naming-of-custom-properties).

### Ricerche MSRP {#msrp-searches}

Per [MSRP](msrp.md), UGC viene memorizzato in MongoDB configurato per utilizzare Solr per la ricerca. UGC non sarà visibile in CRX, ma [moderation](moderate-ugc.md) è disponibile sia dall&#39;ambiente di creazione che da quello di pubblicazione.

Per quanto riguarda MSRP e Solr:

* Il Solr incorporato per la piattaforma AEM non viene utilizzato per MSRP.
* Se utilizzate un Solr remoto per la piattaforma AEM, potrebbe essere condiviso con MSRP, ma dovrebbero utilizzare raccolte diverse.
* Solr può essere configurato per la ricerca standard o per la ricerca multilingue (MLS).
* Per informazioni dettagliate sulla configurazione, consultate [Configurazione solr](msrp.md#solr-configuration) per MSRP.

Le funzionalità di ricerca personalizzate devono utilizzare l&#39;API di ricerca [UGC](#ugc-search-api).

Quando si creano proprietà personalizzate ricercabili, è necessario aderire ai [requisiti di denominazione](#naming-of-custom-properties).

### Ricerche JSRP {#jsrp-searches}

Per [JSRP](jsrp.md), UGC è memorizzato in [Oak](../../help/sites-deploying/platform.md) ed è visibile solo nella directory archivio dell&#39;istanza di creazione o di pubblicazione AEM in cui è stato immesso.

Poiché UGC viene generalmente immesso nell&#39;ambiente di pubblicazione, per i sistemi di produzione con più editori è necessario configurare un [cluster di pubblicazione](topologies.md), non una farm di pubblicazione, in modo che il contenuto immesso sia visibile da tutti gli editori.

Per JSRP, l’UGC immesso nell’ambiente di pubblicazione non sarà mai visibile nell’ambiente di authoring. Di conseguenza, tutte le attività [moderazione](moderate-ugc.md) vengono eseguite nell&#39;ambiente di pubblicazione.

Le funzionalità di ricerca personalizzate devono utilizzare l&#39;API di ricerca [UGC](#ugc-search-api).

#### Indicizzazione quercia {#oak-indexing}

Sebbene gli indici Oak non vengano creati automaticamente per la ricerca della piattaforma AEM, a partire da AEM 6.2 sono stati aggiunti per  AEM Communities per migliorare le prestazioni e fornire supporto per l’impaginazione quando si presentano i risultati di ricerca UGC.

Se le proprietà personalizzate sono in uso e le ricerche sono lente, è necessario creare ulteriori indici per rendere più efficaci le proprietà personalizzate. Per mantenere la portabilità, rispettare i [requisiti di denominazione](#naming-of-custom-properties) durante la creazione di proprietà personalizzate ricercabili.

Per modificare gli indici esistenti o creare indici personalizzati, fare riferimento a [Query e indicizzazione Oak](../../help/sites-deploying/queries-and-indexing.md).

La [Oak Index Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/oak-index-manager.html) è disponibile da ACS AEM Commons. Fornisce:

* Una visualizzazione degli indici esistenti.
* Possibilità di avviare un reindicizzazione.

Per visualizzare gli indici Oak esistenti in [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md), il percorso è:

* `/oak:index/socialLucene`

![social-lucene](assets/social-lucene.png)

## Proprietà ricerca indicizzata {#indexed-search-properties}

### Proprietà di ricerca predefinite {#default-search-properties}

Di seguito sono riportate alcune delle proprietà ricercabili utilizzate per le varie funzioni di Communities:

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
| response | *Lungo* |
| jcr:title | *Stringa* |
| jcr:description | *Stringa* |
| sling:resourceType | *Stringa* |
| allowThreadedReply | *Booleano* |
| isDraft | *Booleano* |
| publishDate | *Data* |
| publishJobId | *Stringa* |
| ha risposto | *Booleano* |
| discordante | *Booleano* |
| tag | *Stringa* |
| cq:Tag | *Stringa* |
| author_display_name | *Stringa* |
| location_t | *Stringa* |
| parentPath | *Stringa* |
| parentTitle | *Stringa* |

### Denominazione delle proprietà personalizzate {#naming-of-custom-properties}

Quando si aggiungono proprietà personalizzate, affinché tali proprietà siano visibili per l&#39;ordinamento e le ricerche create con l&#39;API di ricerca [UGC](#ugc-search-api), è *richiesto* aggiungere un suffisso al nome della proprietà.

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

* *Text* è una stringa token,  ** Stringis no. Utilizzate *Text* per eseguire ricerche sfocate (più simili).

* Per i tipi con più valori, aggiungete ‘s’ al suffisso, ad esempio:

   * `viewDate_dt`: single date, proprietà
   * `viewDates_dts`: list date, proprietà

## Filtri {#filters}

I componenti che includono il [sistema di commenti](essentials-comments.md) supportano il parametro del filtro oltre ai relativi endpoint.

La sintassi del filtro per la logica AND e OR è espressa come segue (visualizzata prima della codifica URL):

* Per specificare O utilizzare un param di filtro con valori separati da virgola:

   * `filter=name eq 'Jennifer',name eq 'Jen'`

* Per specificare e utilizzare più parametri di filtro:

   * `filter = name eq 'Jackson'&filter=message eq 'testing'`

L&#39;implementazione predefinita del [componente di ricerca](search.md) utilizza questa sintassi, come illustrato nell&#39;URL che apre la pagina Risultati ricerca nella [Guida dei componenti della community](components-guide.md). Per provare, individuare [http://localhost:4503/content/community-components/en/search.html](http://localhost:4503/content/community-components/en/search.html).

Gli operatori filtro sono:

| EQ | è uguale a |
|---|---|
| NE | not equals |
| LT | minore di |
| LTE | minore o uguale a |
| GE | maggiore di |
| GTE | maggiore o uguale a |
| SIMILE | sfocato |

È importante che l’URL faccia riferimento al componente Community (risorsa) e non alla pagina in cui il componente è posizionato:

* Corretto: componente forum
   * `/content/community-components/en/forum/jcr:content/content/forum.social.json`
* Scorretto: pagina forum
   * `/content/community-components/en/forum.social.json`

## Strumenti SRP {#srp-tools}

Esiste un progetto Adobe Marketing Cloud GitHub che contiene:

[ AEM Communities SRP Tools](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

Questo archivio contiene strumenti per la gestione dei dati in SRP.

Attualmente, esiste un servlet che consente di eliminare tutti gli UGC da qualsiasi SRP.

Ad esempio, per eliminare tutti gli UGC nell’ASRP:

```shell
curl -X POST http://localhost:4502/services/social/srp/cleanup?path=/content/usergenerated/asi/cloud -uadmin:admin
```

## Risoluzione dei problemi {#troubleshooting}

### Query solr {#solr-query}

Per risolvere i problemi relativi a una query Solr, abilita la registrazione DEBUG per

`com.adobe.cq.social.srp.impl.SocialSolrConnector`.

La query Solr effettiva verrà visualizzata URL codificati nel registro di debug:

La query su solr è: `sort=timestamp+desc&bl=en&pl=en&start=0&rows=10 &q=%2Btitle_t:(hello)+%2Bprovider_id:\/content/usergenerated/asi/mongo/content/+%2Bresource_type_s:&df=provider_id&trf=verbatim&fq={!cost%3D100}report_suite:mongo`

Il valore del parametro `q` è la query. Una volta decodificata la codifica URL, la query può essere passata allo strumento Solr Admin Query per ulteriori attività di debug.

## Risorse correlate {#related-resources}

* [Archiviazione](working-with-srp.md)  dei contenuti della community - Vengono elencate le opzioni SRP disponibili per uno store comune UGC.
* [Panoramica](srp.md)  del provider delle risorse di storage - Introduzione e panoramica sull&#39;utilizzo dell&#39;archivio.
* [Accesso a UGC con linee guida SRP](accessing-ugc-with-srp.md) - Codifica.
* [SocialUtils Refactoring](socialutils.md) - Metodi di utilità per SRP che sostituiscono SocialUtils.
* [Componenti](search.md)  Risultati ricerca e risultati di ricerca - Aggiunta di funzionalità di ricerca UGC a un modello.

