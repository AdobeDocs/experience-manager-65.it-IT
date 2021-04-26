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
translation-type: tm+mt
source-git-commit: d92a635d41cf1b14e109c316bd7264cf7d45a9fe
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 95%

---

# Configurazioni URL avanzate {#url}

I [componenti core CIF di AEM](https://github.com/adobe/aem-core-cif-components) forniscono configurazioni avanzate per personalizzare gli URL per le pagine di prodotti e categorie. Per molte implementazioni questi URL devono essere personalizzati a scopo di SEO (Search Engine Optimization). Nei seguenti video viene descritto come configurare il servizio `UrlProvider` e le funzioni di [mappatura Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) per personalizzare gli URL delle pagine di prodotti e categorie.

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## Configurazione {#configuration}

Per configurare il servizio `UrlProvider` in base ai requisiti e alle esigenze SEO (Search Engine Optimization), un progetto deve fornire una configurazione OSGI per la “configurazione di provider URL CIF” e configurare il servizio come descritto di seguito.

>[!NOTE]
>
> Il progetto [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia), riportato di seguito, include configurazioni esemplificative che mostrano come usare URL personalizzati per le pagine di prodotti e categorie.

### Modello URL per pagina di prodotto {#product}

Consente di configurare gli URL delle pagine di prodotti con le seguenti proprietà:

* **Modello URL di prodotto**: definisce il formato degli URL con un set di segnaposto. Il valore predefinito è `{{page}}.{{url_key}}.html#{{variant_sku}}`, che ad esempio genera URL di tipo `/content/venia/us/en/products/product-page.chaz-kangeroo-hoodie.html#MH01-M-Orange`, in cui
   * `{{page}}` è stato sostituito da `/content/venia/us/en/products/product-page`
   * `{{url_key}}` è stato sostituito dalla proprietà `url_key` del prodotto di Magento, in questo caso `chaz-kangeroo-hoodie`
   * `{{variant_sku}}` è stato sostituito dalla variante attualmente selezionata, in questo caso `MH01-M-Orange`
* **Posizione dell’identificatore del prodotto**: definisce la posizione dell’identificatore che verrà utilizzato per recuperare i dati del prodotto. Il valore predefinito è `SELECTOR`; l’altro valore possibile è `SUFFIX`. Per l’URL dell’esempio precedente, ciò significa che l’identificatore `chaz-kangeroo-hoodie` verrà utilizzato per recuperare i dati del prodotto.
* **Tipo di identificatore del prodotto**: definisce il tipo di identificatore da utilizzare per recuperare i dati del prodotto. Il valore predefinito è `URL_KEY`; l’altro valore possibile è `SKU`. Per l’URL dell’esempio precedente, ciò significa che i dati del prodotto verranno recuperati con un filtro GraphQL di Magento come `filter:{url_key:{eq:"chaz-kangeroo-hoodie"}}`.

### Modello URL per pagina elenco prodotti {#product-list}

Consente di configurare gli URL per le pagine contenenti gli elenchi delle categorie o dei prodotti con le seguenti proprietà:

* **Modello URL di categoria**: definisce il formato degli URL con un set di segnaposto. Il valore predefinito è `{{page}}.{{id}}.html`, che ad esempio genera URL di tipo `/content/venia/us/en/products/category-page.3.html`, in cui
   * `{{page}}` è stato sostituito da `/content/venia/us/en/products/category-page`
   * `{{id}}` è stato sostituito dalla proprietà `id` della categoria di Magento, in questo caso `3`
* **Posizione dell’identificatore della categoria**: definisce la posizione dell’identificatore che verrà utilizzato per recuperare i dati del prodotto. Il valore predefinito è `SELECTOR`; l’altro valore possibile è `SUFFIX`. Per l’URL dell’esempio precedente, ciò significa che l’identificatore `3` verrà utilizzato per recuperare i dati del prodotto.
* **Tipo di identificatore della categoria**: definisce il tipo di identificatore da utilizzare per recuperare i dati del prodotto. Il valore predefinito e al momento l’unico valore supportato è `ID`. Per l’URL dell’esempio precedente, ciò significa che i dati della categoria verranno recuperati con un filtro GraphQL di Magento come `category(id:3)`.

È possibile aggiungere proprietà personalizzate per ciascun modello, purché i dati corrispondenti vengano impostati dai componenti mediante `UrlProvider`. Per un esempio di implementazione, dai un’occhiata al codice della classe `ProductListItemImpl`.

È inoltre possibile sostituire il servizio `UrlProvider` con un servizio OSGi completamente personalizzato. In questo caso, per sostituire l’implementazione predefinita, è necessario implementare l’interfaccia `UrlProvider` e registrarla con una classificazione di servizio superiore.

## Combinare con mappature Sling {#sling-mapping}

Oltre a `UrlProvider`, è anche possibile configurare [mappature Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) per riscrivere ed elaborare gli URL. Il progetto AEM Archetype fornisce anche una [configurazione esemplificativa](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) per configurare mappature Sling per le porte 4503 (pubblicazione) e 80 (dispatcher).

## Combinare con AEM Dispatcher {#dispatcher}

Le riscritture URL possono essere ottenute anche utilizzando il server HTTP di AEM Dispatcher con il modulo `mod_rewrite`. [AEM Project Archetype](https://github.com/adobe/aem-project-archetype) fornisce una configurazione di AEM Dispatcher di riferimento che include [regole di riscrittura](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) di base per la dimensione generata.

## Esempio

Il progetto [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia) include configurazioni esemplificative che mostrano come usare URL personalizzati per le pagine di prodotti e categorie. Questi consentono di impostare per ciascun progetto specifici pattern di URL per le pagine di prodotti e categorie, in base alle esigenze SEO (Search Engine Optimization). Si utilizza una combinazione di `UrlProvider` CIF e di mappature Sling, come descritto sopra.

>[!NOTE]
>
>Questa configurazione deve essere regolata con il dominio esterno utilizzato dal progetto. Le mappature Sling funzionano in base al nome host e al dominio. Pertanto questa configurazione è disabilitata per impostazione predefinita e deve essere abilitata prima della distribuzione. Per eseguire questa operazione, rinomina la cartella delle mappature Sling da `hostname.adobeaemcloud.com` a `ui.content/src/main/content/jcr_root/etc/map.publish/https` in base al nome di dominio utilizzato e abilita questa configurazione aggiungendo `resource.resolver.map.location="/etc/map.publish"` alla configurazione `JcrResourceResolver` del progetto.

## Risorse aggiuntive

* [Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
* [Mappature delle risorse di AEM](https://docs.adobe.com/content/help/it-IT/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Mappature Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
