---
title: Aggiornamento di moduli di ricerca personalizzati
seo-title: Aggiornamento di moduli di ricerca personalizzati
description: In questo articolo vengono descritte le regolazioni necessarie dopo un aggiornamento per il funzionamento dei moduli di ricerca personalizzati.
seo-description: In questo articolo vengono descritte le regolazioni necessarie dopo un aggiornamento per il funzionamento dei moduli di ricerca personalizzati.
uuid: 35b8fbb9-5951-4e1c-bf04-4471a55b9cb0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: a08cee9c-e981-4483-8bdc-e6353977f854
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Aggiornamento di moduli di ricerca personalizzati{#upgrading-custom-search-forms}

In AEM 6.2, è stato modificato il percorso in cui sono memorizzati i moduli di ricerca personalizzati nell’archivio. Al momento dell&#39;aggiornamento, vengono spostati dalla loro posizione in 6.1 a:

* /apps/cq/gui/content/facet

in una nuova posizione in:

* /conf/global/settings/cq/search/facet

Di conseguenza, dopo un aggiornamento sono necessarie regolazioni manuali per consentire il funzionamento dei moduli.

Questo vale sia per i nuovi moduli di ricerca che per i moduli predefiniti personalizzati.

Per ulteriori informazioni, consultate la documentazione sui facet di [ricerca](/help/assets/search-facets.md).

## Modifica della proprietà resourceType {#changing-the-resourcetype-property}

Se non diversamente specificato, la maggior parte delle regolazioni da eseguire dopo l&#39;aggiornamento richiede la modifica della `sling:resourceType` proprietà per i moduli di ricerca personalizzati configurati. È necessaria in modo che la proprietà punti alla posizione corretta dello script di rendering.

È possibile modificare la proprietà effettuando le seguenti operazioni:

1. Aprire CRXDE Lite andando `https://server:port/crx/de/index.jsp`
1. Individuare la posizione del nodo da modificare, come specificato nell&#39;elenco dei moduli [di ricerca](/help/sites-deploying/upgrading-custom-search-forms.md#list-of-custom-search-forms) personalizzati riportato di seguito.
1. Fare clic sul nodo. Nel riquadro delle proprietà a destra, fare clic sulla proprietà **sling:resourceType** e modificarla.
1. Infine, salvare le modifiche premendo il pulsante **Salva tutto** .

## Elenco di moduli di ricerca personalizzati {#list-of-custom-search-forms}

Di seguito è riportato un elenco di tutti i moduli di ricerca personalizzati e le modifiche necessarie dopo l’aggiornamento. Si riferiscono ai nomi in `/conf/global/settings/cq/search/facets/sites/items`.

### Predicato full-text con nome nodo &quot;fulltext&quot; {#fulltext-predicate-with-node-name-fulltext}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1</td>
   <td>fulltext</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/search predicates/fulltextpredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td>n/d</td>
  </tr>
 </tbody>
</table>

In AEM 6.1, il predicato full-text standard faceva parte del modulo di ricerca. In 6.2, il campo full text è stato sostituito da OmniSearch. Questo predicato viene ignorato a livello di programmazione e può essere rimosso.

**** Azione: Rimuovere completamente il nodo.

### Altri predefiniti full-text {#other-fulltext-predicates}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nella ricerca predefinita da in 6.1</td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/search predicates/fulltextpredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/search predicates/fulltextpredicate</p> </td>
  </tr>
 </tbody>
</table>

**** Azione: Regolare la `resourceType` proprietà (aggiungere &quot;**/corallo**&quot; come nella posizione 6.2 sopra indicata).

### Predicati browser percorso {#path-browser-predicates}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /><br /> </td>
   <td>path</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/search predicates/pathpredicates</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/Searchpredicates/pathpredicate</p> </td>
  </tr>
 </tbody>
</table>

**** Azione: Regolare la `resourceType` proprietà (aggiungere &quot;**/corallo**&quot; come nella posizione 6.2 sopra indicata).

### Predicati tag {#tags-predicates}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /><br /> </td>
   <td>tag</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/search predicates/tagspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/search predicates/tagspredicate</p> </td>
  </tr>
 </tbody>
</table>

**** Azione: Regolare la proprietà **resourceType** (aggiungere &quot;**/coral**&quot; come nella posizione 6.2 sopra indicata).

### Predicato di stato pagina {#page-status-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /><br /> </td>
   <td>pagestatuspredicate</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/search-predicates/pagestatuspredicato</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td>n/d</td>
  </tr>
 </tbody>
</table>

Lo stato della pagina è stato sostituito da due predefiniti di proprietà Opzioni, uno per la pubblicazione e uno per lo stato LiveCopy.

**Azioni:**

* Rimuovi il `pagestatuspredicate` nodo
* Copia nodo

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/publishstatuspredicate`
   * a `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* Copia nodo

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/livecopystatuspredicate`
   * a `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* Assicurarsi di impostare `listOrder` la proprietà per il `analyticspredicate` nodo su &quot;**8**&quot;. Ciò è necessario per evitare conflitti.

### Predicati intervallo date {#date-range-predicates}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /><br /> </td>
   <td>daterangepredicate</td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.1</td>
   <td>cq/gui/components/common/admin/customsearch/search predicates/daterangepredicate</td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/Searchpredicates/daterangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**** Azione: Regolare la `resourceType` proprietà (aggiungere &quot;**/corallo**&quot; come nella posizione 6.2 sopra indicata).

### Filtro nascosto {#hidden-filter}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /><br /> </td>
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

**** Azione: Niente da regolare.

### Predicato di analisi {#analytics-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /><br /> </td>
   <td>analyticspredicate</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/search-predicates/analyticspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchPanel/searchpredicates/analyticspredicate</p> </td>
  </tr>
 </tbody>
</table>

**** Azione: Regolare la `resourceType` proprietà (aggiungere &quot;**/corallo**&quot; come nella posizione 6.2 sopra indicata).

### Predicato intervallo {#range-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /><br /> </td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/search-predicates/rangepredicates</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchPanel/searchpredicates/rangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**** Azione: Regolare la `resourceType` proprietà (aggiungere &quot;**/corallo**&quot; come nella posizione 6.2 sopra indicata).

>[!NOTE]
>
>Nota: In opposizione alla versione 6.1, il predicato Range non esegue più il rendering di un tag nella barra di ricerca.

### Predicato proprietà opzioni {#options-property-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /><br /> </td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/search-predicates/optionspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchPanel/searchpredicates/optionspredicate</p> </td>
  </tr>
 </tbody>
</table>

**** Azione: Regolare la `resourceType` proprietà (aggiungere &quot;**/corallo**&quot; come nella posizione 6.2 sopra indicata).

### Predicato intervallo del cursore {#slider-range-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /><br /> </td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/search-predicates/sliderrangepredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchPanel/searchpredicates/sliderrangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**** Azione: Regolare la `resourceType` proprietà (aggiungere &quot;**/corallo**&quot; come nella posizione 6.2 sopra indicata).

### Predicato componenti {#components-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /><br /> </td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/search-predicates/componentspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchPanel/searchpredicates/componentsspredicate</p> </td>
  </tr>
 </tbody>
</table>

**** Azione: Regolare la `resourceType` proprietà (aggiungere &quot;**/corallo**&quot; come nella posizione 6.2 sopra indicata).

### Predicato autore {#author-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /><br /> </td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/Searchpanel/browpredicates/userpredicates</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchPanel/searchpredicates/userpredicate</p> </td>
  </tr>
 </tbody>
</table>

**** Azione: Regolare la `resourceType` proprietà (aggiungere &quot;**/corallo**&quot; come nella posizione 6.2 sopra indicata).

### Predicato modelli {#templates-predicate}

<table>
 <tbody>
  <tr>
   <td>Nodo/i nel modulo di ricerca predefinito in 6.1<br /><br /> </td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo di risorsa in 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/search-predicates/templatespredicato</p> </td>
  </tr>
  <tr>
   <td>Tipo di risorsa in 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchPanel/searchpredicates/templatespredicato</p> </td>
  </tr>
 </tbody>
</table>

**** Azione: Regolare la `resourceType` proprietà (aggiungere &quot;**/corallo**&quot; come nella posizione 6.2 sopra indicata).

## Barra di ricerca amministrazione risorse {#assets-admin-search-rail}

I nodi seguenti fanno riferimento ai nomi in `/conf/global/settings/dam/search/facets/assets/items`

### Predicato full-text con nome nodo &quot;fulltext&quot; {#fulltext-predicate-with-node-name-fulltext-1}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | fulltext |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/browpredicates/fulltextpredicate |
| Tipo di risorsa in 6.2 | n/d |

In 6.1 il predicato full text standard faceva parte del modulo di ricerca. In 6.2 il campo full text è stato sostituito da OmniSearch. Questo predicato viene ignorato a livello di programmazione e può essere rimosso.

**** Azione: Rimuovere il nodo sopra indicato.

### Predicati browser percorso {#path-browser-predicates-1}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | pathbrowser |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/Searchpredicates/pathbrowserpredicate |
| Tipo di risorsa in 6.2 | dam/gui/coral/components/admin/customsearch/browserpredicates/pathbrowserpredicate |

**** Azione: Regolare la `resourceType` proprietà (aggiungere &quot;**/corallo**&quot; come nella posizione 6.2 sopra indicata).

### Predicati tipo mime {#mime-type-predicates}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | mimetype |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/browpredicates/optionspredicate |
| Tipo di risorsa in 6.2 | dam/gui/coral/components/admin/customsearch/browpredicates/optionspredicate |

**** Azione: Regolare la `resourceType` proprietà (aggiungere &quot;**/corallo**&quot; come nella posizione 6.2 sopra indicata).

### Predicati dimensione file {#file-size-predicates}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | filesize |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/browpredicates/filesizepredicate |
| Tipo di risorsa in 6.2 | dam/gui/coral/components/admin/customsearch/browpredicates/sliderangepredicate |

**** Azione: Regolate `resourceType` come mostrato nella precedente posizione 6.2.

### Predicati Ultima modifica risorsa {#asset-last-modified-predicates}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | assetlastmodifiedpredicate |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/browpredicates/assetlastmodifiedpredicato |
| Tipo di risorsa in 6.2 | dam/gui/coral/components/admin/customsearch/browpredicates/assetlastmodifiedpredicato |

Azione: Regolare la proprietà resourceType (aggiungere &quot;/coral&quot; come nella posizione 6.2 indicata sopra).

### Predicato pubblicazione {#publish-predicate}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | pubblicazione |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/browpredicates/publishpredicate |
| Tipo di risorsa in 6.2 | dam/gui/coral/components/admin/customsearch/browpredicates/publishpredicato |

**Azioni:**

*  Regolare la `resourceType` proprietà (aggiungere &quot;**/corallo**&quot; come nella posizione 6.2 sopra indicata)

* Aggiungere una proprietà `optionPaths` (di tipo String) con il valore: `/libs/dam/options/predicates/publish`

* Aggiungi `singleSelect` proprietà con valore booleano `true`.

### Predicati di stato {#status-predicates}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | stato |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/browpredicates/optionspredicate |
| Tipo di risorsa in 6.2 | dam/gui/coral/components/admin/customsearch/browpredicates/optionspredicate |

**** Azione: Regolare la `resourceType` proprietà (aggiungere &quot;**/corallo**&quot; come nella posizione 6.2 sopra indicata)

### Predicati stato scadenza {#expiry-status-predicates}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | stato di scadenza |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/Searchpredicates/esesredassetpredicate |
| Tipo di risorsa in 6.2 | dam/gui/coral/components/admin/customsearch/search predicates/esesredassetpredicato |

**** Azione: Regolare la `resourceType` proprietà (aggiungere &quot;**/corallo**&quot; come nella posizione 6.2 sopra indicata)

### Predicati validità metadati {#metadata-validity-predicates}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | metadata |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/browpredicates/optionspredicate |
| Tipo di risorsa in 6.2 | dam/gui/coral/components/admin/customsearch/browpredicates/optionspredicate |

**** Azione: Regolare la `resourceType` proprietà (aggiungere &quot;**/corallo**&quot; come nella posizione 6.2 sopra indicata)

### Predicati di valutazione {#rating-predicates}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | valutazione |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/browpredicates/ratingpredicate |
| Tipo di risorsa in 6.2 | dam/gui/coral/components/admin/customsearch/browpredicates/sliderangepredicate |

**** Azione: Regolare la `resourceType` proprietà (aggiungere &quot;**/corallo**&quot; come nella posizione 6.2 sopra indicata)

### Predicato orientamento {#orientation-predicate}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | orientation |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/Searchpredicates/tagsfilterpredicate |
| Tipo di risorsa in 6.2 | cq/gui/components/coral/common/admin/customsearch/search predicates/tagspredicate |

**Azioni:**

*  Regolare la `resourceType` proprietà (aggiungere &quot;**/corallo**&quot; come nella posizione 6.2 sopra indicata)

* Aggiungere una `fieldLabel` proprietà con lo stesso valore della `text` proprietà sullo stesso nodo.

* Aggiungere una `emptyText` proprietà con lo stesso valore della `text` proprietà sullo stesso nodo.

* Aggiungere una `rootPath` proprietà con lo stesso valore della `optionPaths` proprietà sullo stesso nodo.

### Predicato stile {#style-predicate}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | stile |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/Searchpredicates/tagsfilterpredicate |
| Tipo di risorsa in 6.2 | cq/gui/components/coral/common/admin/customsearch/search predicates/tagspredicate |

**Azioni:**

*  Regolare la `resourceType` proprietà (aggiungere &quot;**/corallo**&quot; come nella posizione 6.2 sopra indicata)

* Aggiungere una `fieldLabel` proprietà con lo stesso valore della `text` proprietà sullo stesso nodo.

* Aggiungere una `emptyText` proprietà con lo stesso valore della `text` proprietà sullo stesso nodo.

* Aggiungere una `rootPath` proprietà con lo stesso valore della `optionPaths` proprietà sullo stesso nodo.

### Predicati formato video {#video-format-predicates}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | videoFormat |
|---|---|
| Tipo di risorsa in 6.1 | dam/gui/components/admin/customsearch/browpredicates/optionspredicate |
| Tipo di risorsa in 6.2 | dam/gui/coral/components/admin/customsearch/browpredicates/optionspredicate |

**** Azione: Regolare la `resourceType` proprietà (aggiungere &quot;**/corallo**&quot; come nella posizione 6.2 sopra indicata)

### Predicato risorsa principale {#mainasset-predicate}

| Nodo/i nel modulo di ricerca predefinito in 6.1 | principale |
|---|---|
| Tipo di risorsa in 6.1 | granite/ui/components/foundation/form/hidden |
| Tipo di risorsa in 6.2 | granite/ui/components/corallo/foundation/form/hidden |

**** Azione: Regolare la `resourceType` proprietà (aggiungere &quot;**/corallo**&quot; come nella posizione 6.2 sopra indicata)
