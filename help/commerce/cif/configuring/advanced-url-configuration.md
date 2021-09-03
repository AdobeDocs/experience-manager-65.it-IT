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
source-git-commit: fd973cb3693872e4850f860a625cab70553d2754
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 41%

---

# Configurazioni URL avanzate {#url}

>[!NOTE]
>
> L’ottimizzazione SEO (Search Engine Optimization) è diventato un aspetto cruciale per molti esperti marketing. Di conseguenza, è necessario affrontare le questioni relative all’ottimizzazione SEO (Search Engine Optimization) in numerosi progetti AEM. Per ulteriori informazioni, leggi [Best practice relative alla gestione di SEO e URL](https://experienceleague.adobe.com/docs/experience-manager-65/managing/managing-further-reference/seo-and-url-management.html) .

I [componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components) forniscono configurazioni avanzate per personalizzare gli URL per le pagine di prodotti e categorie. Per molte implementazioni questi URL devono essere personalizzati a scopo di SEO (Search Engine Optimization). Nei seguenti video viene descritto come configurare il servizio `UrlProvider` e le funzioni di [mappatura Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) per personalizzare gli URL delle pagine di prodotti e categorie.

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## Configurazione {#configuration}

Per configurare il servizio `UrlProvider` in base ai requisiti e alle esigenze SEO (Search Engine Optimization), un progetto deve fornire una configurazione OSGI per la &quot;configurazione di provider URL CIF&quot;.

>[!NOTE]
>
> A partire dalla versione 2.0.0 dei componenti core CIF di AEM, la configurazione del provider URL fornisce solo formati url predefiniti, invece dei formati configurabili in formato testo libero noti a partire dalle versioni 1.x. Inoltre, l’uso dei selettori per trasmettere dati negli URL è stato sostituito con suffissi.

### Formato URL pagina di prodotto {#product}

Consente di configurare gli URL delle pagine dei prodotti e supporta le seguenti opzioni:

* `{{page}}.html/{{sku}}.html#{{variant_sku}}` (impostazione predefinita)
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`

Nel caso del [negozio di riferimento Venia](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` è sostituito da  `/content/venia/us/en/products/product-page`
* `{{sku}}` saranno sostituiti dalla SKU del prodotto, ad esempio  `VP09`
* `{{url_key}}` viene sostituito dalla  `url_key` proprietà del prodotto, ad esempio  `lenora-crochet-shorts`
* `{{url_path}}` saranno sostituiti dal prodotto  `url_path`, ad esempio  `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` viene sostituito dalla variante attualmente selezionata, ad esempio  `VP09-KH-S`

Con i dati di esempio di cui sopra, un URL di variante del prodotto formattato utilizzando il formato URL predefinito sarà simile a `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`.

### Formato URL pagina categoria {#product-list}

Consente di configurare gli URL delle pagine di elenchi di prodotti o categorie e supporta le seguenti opzioni:

* `{{page}}.html/{{url_path}}.html` (impostazione predefinita)
* `{{page}}.html/{{url_key}}.html`

Nel caso del [negozio di riferimento Venia](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` è sostituito da  `/content/venia/us/en/products/category-page`
* `{{url_key}}` viene sostituito dalla  `url_key` proprietà della categoria
* `{{url_path}}` sarà sostituito dal  `url_path`

Con i dati di esempio di cui sopra, un URL di pagina di categoria formattato utilizzando il formato URL predefinito sarà simile a `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`.

>[!NOTE]
> 
> Il `url_path` è una concatenazione dei `url_keys` predecessori di un prodotto o di una categoria e del prodotto o della categoria `url_key` separato da `/` slash.

## Formati URL personalizzati {#custom-url-format}

Per fornire un formato URL personalizzato, un progetto può implementare l&#39; [`UrlFormat` interface](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/UrlFormat.html) e registrare l&#39;implementazione come servizio OSGI, utilizzandola come pagina di categoria o come formato URL di pagina di prodotto. La proprietà del servizio `UrlFormat#PROP_USE_AS` indica quale dei formati predefiniti configurati per sostituire:

* `useAs=productPageUrlFormat`sostituirà il formato url della pagina di prodotto configurato
* `useAs=categoryPageUrlFormat`sostituirà il formato URL della pagina della categoria configurato

Se sono presenti più implementazioni di `UrlFormat` registrate come servizi OSGI, quella con la classificazione di servizio superiore sostituisce quella con la classificazione di servizio inferiore.

Il `UrlFormat` deve implementare una coppia di metodi per creare un URL da una data Mappa di parametri e per analizzare un URL per restituire la stessa Mappa di parametri. I parametri sono gli stessi descritti in precedenza, solo per le categorie viene fornito un parametro aggiuntivo `{{uid}}` al `UrlFormat`.

## Combinare con mappature Sling {#sling-mapping}

Oltre a `UrlProvider`, è anche possibile configurare [mappature Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) per riscrivere ed elaborare gli URL. Il progetto AEM Archetype fornisce anche una [configurazione esemplificativa](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) per configurare mappature Sling per le porte 4503 (pubblicazione) e 80 (dispatcher).

## Combinare con AEM Dispatcher {#dispatcher}

Le riscritture URL possono essere ottenute anche utilizzando il server HTTP di AEM Dispatcher con il modulo `mod_rewrite`. [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) fornisce una configurazione di AEM Dispatcher di riferimento che include [regole di riscrittura](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) di base per la dimensione generata.

## Esempio

Il progetto [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) include configurazioni esemplificative che mostrano come usare URL personalizzati per le pagine di prodotti e categorie. Questo consente a ogni progetto di impostare singoli pattern URL per le pagine di prodotti e categorie in base alle proprie esigenze SEO (Search Engine Optimization). Si utilizza una combinazione di `UrlProvider` CIF e di mappature Sling, come descritto sopra.

>[!NOTE]
>
>Questa configurazione deve essere regolata con il dominio esterno utilizzato dal progetto. Le mappature Sling funzionano in base al nome host e al dominio. Pertanto questa configurazione è disabilitata per impostazione predefinita e deve essere abilitata prima della distribuzione. Per eseguire questa operazione, rinomina la cartella delle mappature Sling da `hostname.adobeaemcloud.com` a `ui.content/src/main/content/jcr_root/etc/map.publish/https` in base al nome di dominio utilizzato e abilita questa configurazione aggiungendo `resource.resolver.map.location="/etc/map.publish"` alla configurazione `JcrResourceResolver` del progetto.

## Risorse aggiuntive

* [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
* [Mappature delle risorse di AEM](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Mappature Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
