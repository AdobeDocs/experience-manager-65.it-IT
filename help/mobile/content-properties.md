---
title: Proprietà e nodi contenuto
seo-title: Content Properties and Nodes
description: Segui questa pagina per informazioni sulle proprietà del contenuto e sui nodi.
seo-description: Follow this page to learn about content properties and nodes.
uuid: 2dad52c8-5b6c-4b90-8498-62217a9a27fc
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: f5721ddc-df5c-496c-be61-38d1cab63ad4
exl-id: 05c8c846-69cc-4075-9149-33890b3d1e08
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 21%

---

# Proprietà e nodi contenuto {#content-properties-and-nodes}

>[!NOTE]
>
>Adobe consiglia di utilizzare l’editor di SPA per i progetti che richiedono il rendering lato client basato sul framework di un’applicazione a pagina singola (ad esempio, React). [Per saperne di più](/help/sites-developing/spa-overview.md).

Gli articoli, i banner e le raccolte sono rappresentati come cq:Pages in AEM.

Condividono le stesse proprietà comuni presenti in qualsiasi cq:Page oltre a diverse altre mostrate di seguito che rappresentano i metadati dei servizi Adobe Experience Manager (AEM) Mobile On-Demand e le proprietà di supporto dell&#39;integrazione.

Le tabelle seguenti descrivono le proprietà e i nodi del contenuto.

## Proprietà di integrazione comuni {#common-integration-properties}

| **Nome proprietà** | **Tipo** | **Valori predefiniti o previsti** | **Descrizione** |
|---|---|---|---|
| dps-id | Stringa |  | assegnato da AEM Mobile e memorizzato da AEM una volta caricato su AEM Mobile o importato da AEM Mobile |
| dps-resourceType | Stringa | dps:Article | dps:Banner | dps:Collection | proprietà tipo di entità |
| versione dps | Stringa |  | versione dell’entità AEM Mobile (contenuta anche nell’intero aemm-id) |
| dps-lastSynced | Data |  | data dell’ultima sincronizzazione/importazione da AEM Mobile in AEM |
| dps-lastUploaded | Data |  | data dell’ultimo caricamento da AEM ad AEM Mobile |
| dps-lastUploadedBy | Stringa:userid |  | utente id che ha eseguito l’ultima richiesta di caricamento da AEM ad AEM Mobile |

## Proprietà metadati core {#core-metadata-properties}

| Nome proprietà | Tipo | Valori predefiniti o previsti |
|--- |--- |--- |
| dps-title | Stringa |  |
| dps-shortTitle | Stringa |  |
| dps-abstract | Stringa |  |
| dps-shortAbstract | Stringa |  |
| dipartimento del dps | Stringa |  |
| dps-category | Stringa |  |
| parole chiave dps | Stringa[] |  |
| dps-internalKeywords | Stringa[] |  |
| importanza dps | Stringa[] | Importanza da {&quot;low&quot;, &quot;Normal&quot;, &quot;high&quot;} |

### Articoli {#articles}

| **Nome proprietà** | **Tipo** | **Valori predefiniti o previsti** |
|---|---|---|
| autore di dps | Stringa |  |
| dps-authorURL | Stringa |  |
| dps-hideFromBrowsePage | Booleano |  |
| accesso dps | Stringa | ProtectedAccess da {&quot;protected&quot;, &quot;metered&quot;, &quot;free&quot;} |
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
| dps-readingPosition | Stringa | da {&quot;reset&quot;,&quot;keep&quot;} |
| dps-HorizontalSwipe | Booleano |  |
| dps-allowDownload | Booleano |  |
| dps-openDefault | Stringa | da {&quot;browsePage&quot;,&quot;contentView&quot;} |
| dps-layout | Stringa |  |

## Nodi contenuto {#content-nodes}

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
| immagine di sfondo | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |
