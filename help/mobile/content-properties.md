---
title: Proprietà e nodi contenuto
seo-title: Proprietà e nodi contenuto
description: Seguite questa pagina per informazioni sulle proprietà e i nodi del contenuto.
seo-description: Seguite questa pagina per informazioni sulle proprietà e i nodi del contenuto.
uuid: 2dad52c8-5b6c-4b90-8498-62217a9a27fc
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: f5721ddc-df5c-496c-be61-38d1cab63ad4
translation-type: tm+mt
source-git-commit: 50c0bdfc3203410d392e53536bc7cd00245406e5
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 20%

---


# Proprietà contenuto e nodi {#content-properties-and-nodes}

>[!NOTE]
>
> Adobe consiglia di utilizzare l&#39;editor SPA per i progetti che richiedono il rendering lato client basato sul framework dell&#39;applicazione a pagina singola (ad es. React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Articoli, banner e raccolte sono rappresentati come cq:Pages in AEM.

Condividono le stesse proprietà comuni presenti in qualsiasi cq:Page, oltre a molte altre mostrate di seguito, che rappresentano i metadati dei servizi on-demand di Adobe Experience Manager (AEM) Mobile e le proprietà di supporto dell&#39;integrazione.

Le tabelle seguenti descrivono le proprietà e i nodi del contenuto.

## Proprietà comuni di integrazione {#common-integration-properties}

| **Nome proprietà** | **Tipo** | **Valori predefiniti o previsti** | **Descrizione** |
|---|---|---|---|
| dps-id | Stringa |  | assegnato da  AEM Mobile e memorizzato da AEM una volta caricato  AEM Mobile o importato da  AEM Mobile |
| dps-resourceType | Stringa | dps:Article | dps:Banner | dps:Collection | entity type, proprietà |
| dps-version | Stringa |  | versione di &#39;entità AEM Mobile (anch&#39;essa contenuta nell&#39;aemm-id completo) |
| dps-lastSynced | Data |  | data dell&#39;ultima sincronizzazione/importazione da  AEM Mobile in AEM |
| dps-lastUploaded | Data |  | data dell&#39;ultimo caricamento da AEM a  AEM Mobile |
| dps-lastUploadedBy | String:userid |  | utente ID che ha eseguito l’ultima richiesta di caricamento da AEM a  AEM Mobile |

## Proprietà metadati di base {#core-metadata-properties}

| Nome proprietà | Tipo | Valori predefiniti o previsti |
|--- |--- |--- |
| dps-title | Stringa |  |
| dps-shortTitle | Stringa |  |
| dps-abstract | Stringa |  |
| dps-shortAbstract | Stringa |  |
| dipartimento DPS | Stringa |  |
| dps-category | Stringa |  |
| dps-keywords | Stringa[] |  |
| dps-internalKeywords | Stringa[] |  |
| importanza dps | Stringa[] | Importanza da {&quot;low&quot;, &quot;normal&quot;, &quot;high&quot;} |

### Articoli {#articles}

| **Nome proprietà** | **Tipo** | **Valori predefiniti o previsti** |
|---|---|---|
| dps-author | Stringa |  |
| dps-authorURL | Stringa |  |
| dps-hideFromBrowsePage | Booleano |  |
| dps-access | Stringa | ProtectedAccess da {&quot;protected&quot;, &quot;metered&quot;, &quot;free&quot;} |
| **Social network** |  |  |
| dps-socialShareURL | Stringa |  |
| dps-articleText | Stringa |  |
| dps-url | Stringa |  |

### Banner {#banners}

| **Nome proprietà** | **Tipo** | **Valori predefiniti o previsti** |
|---|---|---|
| dps-tapAction |  | TapAction da {webLink} |
| dps-tapActionUrl |  |  |

### Raccolte {#collections}

| Nome proprietà | Tipo | Valori predefiniti o previsti |
|--- |--- |--- |
| dps-productId | Stringa |  |
| dps-readingPosition | Stringa | da {&quot;reset&quot;,&quot;retain&quot;} |
| dps-horizontalSwipe | Booleano |  |
| dps-allowDownload | Booleano |  |
| dps-openDefault | Stringa | da {&quot;browsePage&quot;,&quot;contentView&quot;} |
| dps-layout | Stringa |  |

## Nodi contenuto {#content-nodes}

### Nodi comuni {#common-nodes}

| Nome nodo | Tipo | Valori predefiniti o previsti | Descrizione |
|--- |--- |--- |--- |
| immagine | jcr:PrimaryType=nt:unstructure <br> sling:resourceType=foundation/components/image |  |  |

### Entità {#entities}

#### Articoli {#articles-1}

| Nome nodo | Tipo | Valori predefiniti per i valori previsti | Descrizione |
|--- |--- |--- |--- |
| social-share-image |  | jcr:PrimaryType=nt:unstructure <br> sling:resourceType=foundation/components/image |  |

#### Banner {#banners-1}

| Nome nodo | Tipo | Valori predefiniti per i valori previsti | Descrizione |
|---|---|---|---|
| NA |  |  |  |

#### Raccolte {#collections-1}

| Nome nodo | Tipo | Valori predefiniti per i valori previsti | Descrizione |
|--- |--- |--- |--- |
| background-image | jcr:PrimaryType=nt:unstructure <br> sling:resourceType=foundation/components/image |  |  |
