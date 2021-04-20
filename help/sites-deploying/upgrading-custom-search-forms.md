---
title: Aggiornamento di Custom Search Forms
seo-title: Aggiornamento di Custom Search Forms
description: Questo articolo descrive le regolazioni necessarie dopo un aggiornamento per il funzionamento dei moduli di ricerca personalizzati.
seo-description: Questo articolo descrive le regolazioni necessarie dopo un aggiornamento per il funzionamento dei moduli di ricerca personalizzati.
uuid: 35b8fbb9-5951-4e1c-bf04-4471a55b9cb0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: a08cee9c-e981-4483-8bdc-e6353977f854
feature: Upgrading
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1710'
ht-degree: 3%

---


# Aggiornamento della funzione Ricerca personalizzata Forms{#upgrading-custom-search-forms}

Nella AEM 6.2, è stato modificato il percorso in cui sono memorizzati nell’archivio i Forms di ricerca personalizzati. Al momento dell’aggiornamento, vengono spostati dalla loro posizione in 6.1 in:

* /apps/cq/gui/content/facet

in una nuova posizione in:

* /conf/global/settings/cq/search/facet

Per questo motivo, dopo un aggiornamento sono necessarie regolazioni manuali affinché i moduli continuino a funzionare.

Questo vale sia per la nuova Forms di ricerca che per la Forms predefinita personalizzata.

Per ulteriori informazioni, consulta la documentazione su [Facet di ricerca](/help/assets/search-facets.md).

## Modifica della proprietà resourceType {#changing-the-resourcetype-property}

Se non diversamente specificato, la maggior parte delle regolazioni che devono essere eseguite dopo l’aggiornamento richiede la modifica della proprietà `sling:resourceType` per il Forms di ricerca personalizzato configurato. È necessario in modo che la proprietà punti alla posizione corretta dello script di rendering.

È possibile modificare la proprietà facendo quanto segue:

1. Apri CRXDE Lite andando su `https://server:port/crx/de/index.jsp`
1. Individua la posizione del nodo da regolare, come specificato nell&#39;elenco di [Ricerca personalizzata Forms](/help/sites-deploying/upgrading-custom-search-forms.md#list-of-custom-search-forms) qui sotto.
1. Fai clic sul nodo . Nel riquadro delle proprietà di destra, fai clic su e modifica la proprietà **sling:resourceType** .
1. Infine, salvare le modifiche premendo il pulsante **Salva tutto**.

## Elenco di Forms di ricerca personalizzata {#list-of-custom-search-forms}

Di seguito trovi un elenco di tutti i Forms di ricerca personalizzati e le modifiche necessarie dopo l’aggiornamento. Si riferiscono ai nomi in `/conf/global/settings/cq/search/facets/sites/items`.

### Predicato full-text con nome nodo &quot;fulltext&quot; {#fulltext-predicate-with-node-name-fulltext}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1</td>
   <td>fulltext</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/fulltextpredicato</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td>n/d</td>
  </tr>
 </tbody>
</table>

Nella AEM 6.1, il predicato full-text standard faceva parte del modulo di ricerca. Nella versione 6.2, il campo di testo completo è stato sostituito da OmniSearch. Questo predicato viene ignorato a livello di programmazione e può essere rimosso.

**Azione:** rimuovi completamente il nodo.

### Altri predicati full-text {#other-fulltext-predicates}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nella ricerca predefinita da in 6.1</td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/fulltextpredicato</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/fulltextpredicato</p> </td>
  </tr>
 </tbody>
</table>

**Azione:** regola la  `resourceType` proprietà (aggiungi &quot;**/coral**&quot; come nella posizione 6.2 indicata sopra).

### Predicati browser del percorso {#path-browser-predicates}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /> <br /> </td>
   <td>path</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/pathpredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/pathpredicate</p> </td>
  </tr>
 </tbody>
</table>

**Azione:** regola la  `resourceType` proprietà (aggiungi &quot;**/coral**&quot; come nella posizione 6.2 indicata sopra).

### Predicati tag {#tags-predicates}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /> <br /> </td>
   <td>tag</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/tagspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/tagspredicate</p> </td>
  </tr>
 </tbody>
</table>

**Azione:** regola la proprietà  **** resourceType (aggiungi &quot;**/coral**&quot; come nella posizione 6.2 indicata sopra).

### Predicato di stato pagina {#page-status-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /> <br /> </td>
   <td>pagestatuspredicato</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/pagestatuspredicato</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td>n/d</td>
  </tr>
 </tbody>
</table>

Lo stato della pagina è stato sostituito da due predicati di proprietà Opzioni, uno per la pubblicazione e uno per lo stato LiveCopy.

**Azioni:**

* Rimuovi il nodo `pagestatuspredicate`
* Copia nodo

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/publishstatuspredicate`
   * a `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* Copia nodo

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/livecopystatuspredicate`
   * a `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* Assicurati di impostare la proprietà `listOrder` per il nodo `analyticspredicate` su &quot;**8**&quot;. Ciò è necessario per evitare conflitti.

### Predicati intervallo di date {#date-range-predicates}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /> <br /> </td>
   <td>daterangepredicato</td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.1</td>
   <td>cq/gui/components/common/admin/customsearch/searchpredicates/daterangepredicate</td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/daterangepredicato</p> </td>
  </tr>
 </tbody>
</table>

**Azione:** regola la  `resourceType` proprietà (aggiungi &quot;**/coral**&quot; come nella posizione 6.2 indicata sopra).

### Filtro nascosto {#hidden-filter}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /> <br /> </td>
   <td>tipo</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>granite/ui/components/foundation/form/hidden</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>granite/ui/components/foundation/form/hidden</p> </td>
  </tr>
 </tbody>
</table>

**Azione:** nessuna regolazione.

### Predicato di analisi {#analytics-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /> <br /> </td>
   <td>analyticspredicate</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/analyticspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/analyticspredicate</p> </td>
  </tr>
 </tbody>
</table>

**Azione:** regola la  `resourceType` proprietà (aggiungi &quot;**/coral**&quot; come nella posizione 6.2 indicata sopra).

### Predicato intervallo {#range-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /> <br /> </td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/rangepredicato</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/rangepredicato</p> </td>
  </tr>
 </tbody>
</table>

**Azione:** regola la  `resourceType` proprietà (aggiungi &quot;**/coral**&quot; come nella posizione 6.2 indicata sopra).

>[!NOTE]
>
>Nota: In opposizione alla versione 6.1, il predicato Intervallo non esegue più il rendering di un tag nella barra di ricerca.

### Predicato proprietà opzioni {#options-property-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /> <br /> </td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/optionspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/optionspredicate</p> </td>
  </tr>
 </tbody>
</table>

**Azione:** regola la  `resourceType` proprietà (aggiungi &quot;**/coral**&quot; come nella posizione 6.2 indicata sopra).

### Predicato intervallo del cursore {#slider-range-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /> <br /> </td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/sliderrangepredicato</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/sliderrangepredicato</p> </td>
  </tr>
 </tbody>
</table>

**Azione:** regola la  `resourceType` proprietà (aggiungi &quot;**/coral**&quot; come nella posizione 6.2 indicata sopra).

### Predicato componenti {#components-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /> <br /> </td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/componentspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/componentspredicate</p> </td>
  </tr>
 </tbody>
</table>

**Azione:** regola la  `resourceType` proprietà (aggiungi &quot;**/coral**&quot; come nella posizione 6.2 indicata sopra).

### Predicato autore {#author-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /> <br /> </td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/userpredicates</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/userpredicato</p> </td>
  </tr>
 </tbody>
</table>

**Azione:** regola la  `resourceType` proprietà (aggiungi &quot;**/coral**&quot; come nella posizione 6.2 indicata sopra).

### Predicato modelli {#templates-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /> <br /> </td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/templatespredicato</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/templatespredicato</p> </td>
  </tr>
 </tbody>
</table>

**Azione:** regola la  `resourceType` proprietà (aggiungi &quot;**/coral**&quot; come nella posizione 6.2 indicata sopra).

## Barra di ricerca amministrazione risorse {#assets-admin-search-rail}

I nodi sotto riportati si riferiscono ai nomi in `/conf/global/settings/dam/search/facets/assets/items`

### Predicato full-text con nome nodo &quot;fulltext&quot; {#fulltext-predicate-with-node-name-fulltext-1}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | fulltext |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/searchpredicates/fulltextpredicate |
| Tipo di risorsa in 6.2 | n/d |

Nella versione 6.1, il predicato full-text standard faceva parte del modulo di ricerca. Nella versione 6.2, il campo di testo completo è stato sostituito da OmniSearch. Questo predicato viene ignorato a livello di programmazione e può essere rimosso.

**Azione:** rimuovi il nodo sopra menzionato.

### Predicati browser del percorso {#path-browser-predicates-1}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | pathbrowser |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/searchpredicates/pathbrowserpredicate |
| Tipo di risorsa in 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/pathbrowserpredicate |

**Azione:** regola la  `resourceType` proprietà (aggiungi &quot;**/coral**&quot; come nella posizione 6.2 indicata sopra).

### Predicati tipo MIME {#mime-type-predicates}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | mimetype |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| Tipo di risorsa in 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**Azione:** regola la  `resourceType` proprietà (aggiungi &quot;**/coral**&quot; come nella posizione 6.2 indicata sopra).

### Predicati dimensioni file {#file-size-predicates}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | filesize |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/searchpredicates/filesizepredicate |
| Tipo di risorsa in 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/sliderangepredicato |

**Azione:** regola  `resourceType` come mostrato nella posizione 6.2 precedente.

### Predicati per l’ultima modifica della risorsa {#asset-last-modified-predicates}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | assetlastmodifiedpredicato |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/searchpredicates/assetlastmodifiedpredicato |
| Tipo di risorsa in 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/assetlastmodifiedpredicato |

Azione: Regola la proprietà resourceType (aggiungi &quot;/coral&quot; come nella posizione 6.2 indicata sopra).

### Predicato di pubblicazione {#publish-predicate}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | pubblicazione |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/searchpredicates/publishpredicato |
| Tipo di risorsa in 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/publishpredicato |

**Azioni:**

* Regola la proprietà `resourceType` (aggiungi &quot;**/coral**&quot; come nella posizione 6.2 sopra indicata)

* Aggiungi una proprietà `optionPaths` (di tipo String) con il valore: `/libs/dam/options/predicates/publish`

* Aggiungi la proprietà `singleSelect` con il valore booleano `true`.

### Predicati di stato {#status-predicates}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | stato |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| Tipo di risorsa in 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**Azione:** regola la  `resourceType` proprietà (aggiungi &quot;**/coral**&quot; come nella posizione 6.2 sopra indicata)

### Predicati di stato di scadenza {#expiry-status-predicates}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | stato di scadenza |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/searchpredicates/esredassetpredicato |
| Tipo di risorsa in 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/esredassetpredicato |

**Azione:** regola la  `resourceType` proprietà (aggiungi &quot;**/coral**&quot; come nella posizione 6.2 sopra indicata)

### Predicati di validità dei metadati {#metadata-validity-predicates}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | metadatavalidità |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| Tipo di risorsa in 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**Azione:** regola la  `resourceType` proprietà (aggiungi &quot;**/coral**&quot; come nella posizione 6.2 sopra indicata)

### Predicati di valutazione {#rating-predicates}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | valutazione |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/searchpredicates/ratingpredicate |
| Tipo di risorsa in 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/sliderangepredicato |

**Azione:** regola la  `resourceType` proprietà (aggiungi &quot;**/coral**&quot; come nella posizione 6.2 sopra indicata)

### Predicato di orientamento {#orientation-predicate}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | orientation |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/searchpredicates/tagsfilterpredicate |
| Tipo di risorsa in 6.2 | cq/gui/components/coral/common/admin/customsearch/searchpredicates/tagspredicate |

**Azioni:**

* Regola la proprietà `resourceType` (aggiungi &quot;**/coral**&quot; come nella posizione 6.2 sopra indicata)

* Aggiungi una proprietà `fieldLabel` con lo stesso valore della proprietà `text` sullo stesso nodo.

* Aggiungi una proprietà `emptyText` con lo stesso valore della proprietà `text` sullo stesso nodo.

* Aggiungi una proprietà `rootPath` con lo stesso valore della proprietà `optionPaths` sullo stesso nodo.

### Predicato di stile {#style-predicate}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | stile |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/searchpredicates/tagsfilterpredicate |
| Tipo di risorsa in 6.2 | cq/gui/components/coral/common/admin/customsearch/searchpredicates/tagspredicate |

**Azioni:**

* Regola la proprietà `resourceType` (aggiungi &quot;**/coral**&quot; come nella posizione 6.2 sopra indicata)

* Aggiungi una proprietà `fieldLabel` con lo stesso valore della proprietà `text` sullo stesso nodo.

* Aggiungi una proprietà `emptyText` con lo stesso valore della proprietà `text` sullo stesso nodo.

* Aggiungi una proprietà `rootPath` con lo stesso valore della proprietà `optionPaths` sullo stesso nodo.

### Predicati formato video {#video-format-predicates}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | videoFormat |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| Tipo di risorsa in 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**Azione:** regola la  `resourceType` proprietà (aggiungi &quot;**/coral**&quot; come nella posizione 6.2 sopra indicata)

### Predicato risorsa principale {#mainasset-predicate}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | principale |
|---|---|
| Tipo di risorsa in 6.1 | granite/ui/components/foundation/form/hidden |
| Tipo di risorsa in 6.2 | granite/ui/components/coral/foundation/form/hidden |

**Azione:** regola la  `resourceType` proprietà (aggiungi &quot;**/coral**&quot; come nella posizione 6.2 sopra indicata)
