---
title: Configurazioni URL avanzate
description: Scopri come personalizzare gli URL per le pagine di prodotti e categorie. Questo consente alle implementazioni di ottimizzare gli URL per i motori di ricerca e promuovere l’individuazione.
sub-product: Commerce
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
exl-id: 0125021a-1c00-4ea3-b7fb-1533b7b9f4f2
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 29%

---

# Configurazioni URL avanzate {#url}

>[!NOTE]
>
>L’ottimizzazione SEO (Search Engine Optimization) è diventato un aspetto cruciale per molti esperti marketing. Di conseguenza, le preoccupazioni in materia di SEO devono essere affrontate in molti progetti AEM. Consulta [Best practice per la gestione di SEO e URL](https://experienceleague.adobe.com/docs/experience-manager-65/managing/managing-further-reference/seo-and-url-management.html) per ulteriori informazioni.

I [componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components) forniscono configurazioni avanzate per personalizzare gli URL per le pagine di prodotti e categorie. Molte implementazioni personalizzano questi URL a scopo di SEO (Search Engine Optimization). Nei seguenti video viene descritto come configurare il servizio `UrlProvider` e le funzioni di [mappatura Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) per personalizzare gli URL delle pagine di prodotti e categorie.

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## Configurazione {#configuration}

Per configurare `UrlProvider` secondo i requisiti e le esigenze SEO (Search Engine Optimization), un progetto deve fornire una configurazione OSGI per la &quot;configurazione provider URL CIF&quot;.

>[!NOTE]
>
>A partire dalla versione 2.0.0 dei Componenti core CIF dell’AEM, la configurazione del provider URL fornisce solo formati URL predefiniti, invece dei formati configurabili a testo libero noti dalle versioni 1.x. Inoltre, l’utilizzo dei selettori per trasmettere i dati negli URL è stato sostituito dai suffissi.

### Formato URL pagina prodotto {#product}

Questo configura gli URL delle pagine dei prodotti e supporta le seguenti opzioni:

* `{{page}}.html/{{sku}}.html#{{variant_sku}}` (impostazione predefinita)
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`

Se è presente [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` è sostituito da `/content/venia/us/en/products/product-page`
* `{{sku}}` è sostituito dalla SKU del prodotto, ad esempio `VP09`
* `{{url_key}}` è sostituito da `url_key` proprietà, ad esempio `lenora-crochet-shorts`
* `{{url_path}}` è sostituito da `url_path`ad esempio: `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` viene sostituito dalla variante attualmente selezionata, ad esempio, `VP09-KH-S`

Poiché il `url_path` diventati obsoleti, i formati URL di prodotto predefiniti utilizzano i `url_rewrites` e scegliete quello con il maggior numero di segmenti di tracciato come alternativa se `url_path` non è disponibile.

Con i dati dell’esempio precedente, l’URL di una variante di prodotto formattato con il formato URL predefinito ha l’aspetto di `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`.

### Formato URL pagina categoria {#product-list}

In questo modo vengono configurati gli URL delle pagine delle categorie o degli elenchi di prodotti e sono supportate le seguenti opzioni:

* `{{page}}.html/{{url_path}}.html` (impostazione predefinita)
* `{{page}}.html/{{url_key}}.html`

Se è presente [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` è sostituito da `/content/venia/us/en/products/category-page`
* `{{url_key}}` è sostituito da quello della categoria `url_key` proprietà
* `{{url_path}}` è sostituito da quello della categoria `url_path`

Con i dati dell’esempio precedente, l’URL di una pagina categoria formattato con il formato URL predefinito ha l’aspetto di `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`.

>[!NOTE]
> 
>Il `url_path` è una concatenazione del `url_keys` dei predecessori di un prodotto o di una categoria e del prodotto o della categoria `url_key` separato da `/` barra.

### Categorie/pagine di prodotti specifiche {#specific-pages}

È possibile creare [più pagine di prodotti e categorie](multi-template-usage.md) solo per un sottoinsieme specifico di categorie o prodotti di un catalogo.

Il `UrlProvider` è preconfigurato per generare collegamenti profondi a tali pagine sulle istanze del livello di authoring. Questa funzione è utile per gli editor che navigano in un sito utilizzando la modalità Anteprima, per passare a una pagina di prodotto o categoria specifica e tornare alla modalità Modifica per modificare la pagina.

Nelle istanze del livello di pubblicazione, invece, gli URL delle pagine del catalogo devono essere mantenuti stabili per non perdere i guadagni, ad esempio, nella classificazione dei motori di ricerca. Per questo motivo, per impostazione predefinita, le istanze del livello di pubblicazione non eseguiranno il rendering dei collegamenti profondi a pagine di catalogo specifiche. Per modificare questo comportamento, _Strategia pagina specifica per il provider URL CIF_ può essere configurato in modo da generare sempre url di pagina specifici.

## Formati URL personalizzati {#custom-url-format}

Per fornire un formato URL personalizzato che un progetto possa implementare [`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html) o [`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html) e registra l’implementazione come servizio OSGI. Queste implementazioni, se disponibili, sostituiscono il formato configurato e predefinito. Se sono registrate più implementazioni, quella con la classificazione di servizio più alta sostituisce quelle con la classificazione di servizio più bassa.

Le implementazioni del formato URL personalizzato devono implementare una coppia di metodi per generare un URL dai parametri forniti e per analizzare un URL rispettivamente per restituire gli stessi parametri.

## Combinare con mappature Sling {#sling-mapping}

Oltre al `UrlProvider`, è anche possibile configurare [Mappature Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) per riscrivere ed elaborare gli URL. Il progetto Archetipo AEM fornisce anche [un esempio di configurazione](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) per configurare alcune mappature Sling per le porte 4503 (pubblicazione) e 80 (Dispatcher).

## Combinare con AEM Dispatcher {#dispatcher}

Le riscritture URL possono essere ottenute anche utilizzando il server HTTP di Dispatcher dell’AEM con `mod_rewrite` modulo. [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) fornisce una configurazione di AEM Dispatcher di riferimento che include [regole di riscrittura](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) di base per la dimensione generata.

## Esempio

Il progetto [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) include configurazioni esemplificative che mostrano come usare URL personalizzati per le pagine di prodotti e categorie. Questo consente a ciascun progetto di impostare pattern di URL individuali per le pagine di prodotti e categorie in base alle proprie esigenze SEO (Search Engine Optimization). Si utilizza una combinazione di `UrlProvider` CIF e di mappature Sling, come descritto sopra.

>[!NOTE]
>
>Questa configurazione deve essere regolata con il dominio esterno utilizzato dal progetto. Le mappature Sling funzionano in base al nome host e al dominio. Pertanto questa configurazione è disabilitata per impostazione predefinita e deve essere abilitata prima della distribuzione. Per eseguire questa operazione, rinomina la cartella delle mappature Sling da `hostname.adobeaemcloud.com` a `ui.content/src/main/content/jcr_root/etc/map.publish/https` in base al nome di dominio utilizzato e abilita questa configurazione aggiungendo `resource.resolver.map.location="/etc/map.publish"` alla configurazione `JcrResourceResolver` del progetto.

## Risorse aggiuntive

* [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
* [Mappature delle risorse di AEM](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Mappature Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
