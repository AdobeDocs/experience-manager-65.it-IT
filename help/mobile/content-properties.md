---
title: Proprietà e nodi di contenuto
description: Segui questa pagina per scoprire di più sulle proprietà e sui nodi del contenuto.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 05c8c846-69cc-4075-9149-33890b3d1e08
solution: Experience Manager
feature: Mobile
role: User
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 19%
---
# Proprietà e nodi di contenuto {#content-properties-and-nodes}

{{ue-over-mobile}}

Articoli, banner e raccolte sono rappresentati come cq:Pages in AEM.

Condividono le stesse proprietà comuni presenti in qualsiasi cq:Page, oltre a diverse altre mostrate di seguito che rappresentano i metadati di Adobe Experience Manager (AEM) Mobile On-Demand Services e le proprietà di supporto dell&#39;integrazione.

Le tabelle seguenti descrivono le proprietà e i nodi del contenuto.

## Proprietà di integrazione comuni {#common-integration-properties}

| **Nome proprietà** | **Tipo** | **Valori predefiniti o previsti** | **Descrizione** |
|---|---|---|---|
| dps-id | Stringa |  | assegnati da AEM Mobile e memorizzati da AEM dopo essere stati caricati su AEM Mobile o importati da AEM Mobile |
| dps-resourceType | Stringa | dps:Article | `dps:Banner` \| `dps:Collection` \| `entity type property` |
| dps-version | Stringa |  | versione dell’entità AEM Mobile (contenuta anche nell’aemm-id completo) |
| dps-lastSynced | Data |  | data dell’ultima sincronizzazione/importazione da AEM Mobile ad AEM |
| dps-lastUploaded | Data |  | data dell’ultimo caricamento da AEM ad AEM Mobile |
| dps-lastUploadedBy | Stringa:userid |  | utente id che ha eseguito l’ultima richiesta di caricamento da AEM ad AEM Mobile |

## Proprietà metadati core {#core-metadata-properties}

| Nome proprietà | Tipo | Valori predefiniti o previsti |
|--- |--- |--- |
| dps-title | Stringa |  |
| dps-shortTitle | Stringa |  |
| dps-abstract | Stringa |  |
| dps-shortAbstract | Stringa |  |
| dps-reparto | Stringa |  |
| dps-category | Stringa |  |
| parole chiave dps | Stringa[] |  |
| dps-internalKeywords | Stringa[] |  |
| dps-importance | Stringa[] | Importanza da {&quot;low&quot;, &quot;normal&quot;, &quot;high&quot;} |

### Articoli {#articles}

| **Nome proprietà** | **Tipo** | **Valori predefiniti o previsti** |
|---|---|---|
| dps-author | Stringa |  |
| dps-authorURL | Stringa |  |
| dps-hideFromBrowsePage | Booleano |  |
| accesso a dps | Stringa | ProtectedAccess da {&quot;protected&quot;, &quot;metered&quot;, &quot;free&quot;} |
| **Social** |  |  |
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
| dps-readingPosition | Stringa | da {&quot;reset&quot;,&quot;keep&quot;} |
| dps-horizontalSwipe | Booleano |  |
| dps-allowDownload | Booleano |  |
| dps-openDefault | Stringa | da {&quot;browsePage&quot;,&quot;contentView&quot;} |
| dps-layout | Stringa |  |

## Nodi di contenuto {#content-nodes}

### Nodi comuni {#common-nodes}

| Nome nodo | Tipo | Valori predefiniti o previsti | Descrizione |
|--- |--- |--- |--- |
| immagine | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |

### Entità {#entities}

#### Articoli {#articles-1}

| Nome nodo | Tipo | Valori predefiniti dei valori previsti | Descrizione |
|--- |--- |--- |--- |
| social-share-image |  | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |

#### Banner {#banners-1}

| Nome nodo | Tipo | Valori predefiniti dei valori previsti | Descrizione |
|---|---|---|---|
| ND |  |  |  |

#### Raccolte {#collections-1}

| Nome nodo | Tipo | Valori predefiniti dei valori previsti | Descrizione |
|--- |--- |--- |--- |
| background-image | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |
