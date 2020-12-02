---
title: Sovrapposizioni
seo-title: Sovrapposizioni
description: AEM utilizza il principio delle sovrapposizioni per estendere e personalizzare le console e altre funzionalità
seo-description: AEM utilizza il principio delle sovrapposizioni per estendere e personalizzare le console e altre funzionalità
uuid: d14c08fe-04c0-4925-8c99-c6644357919d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0470b74c-2c34-4327-afed-b95eefb1d521
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---


# Overlays{#overlays}

AEM (e prima ancora, CQ) ha utilizzato da tempo il principio delle sovrapposizioni per consentire di estendere e personalizzare le [console](/help/sites-developing/customizing-consoles-touch.md) e altre funzionalità (ad esempio, [authoring delle pagine](/help/sites-developing/customizing-page-authoring-touch.md)).

Sovrapposizione è un termine che può essere utilizzato in molti contesti. In questo contesto (estensione AEM) una sovrapposizione significa acquisire le funzionalità predefinite e imporre le proprie definizioni su di essa (per personalizzare la funzionalità standard).

In un&#39;istanza standard, la funzionalità predefinita è mantenuta in `/libs` ed è consigliabile definire la sovrapposizione (personalizzazioni) sotto il ramo `/apps`. AEM utilizza un percorso di ricerca per trovare una risorsa, eseguendo prima la ricerca del ramo `/apps` e quindi del ramo `/libs` (il percorso di ricerca [può essere configurato](#configuring-the-search-paths)). Questo meccanismo significa che la sovrapposizione (e le personalizzazioni qui definite) avranno priorità.

A partire dal AEM 6.0, sono state apportate modifiche alle modalità di implementazione e utilizzo delle sovrapposizioni:

* A partire da AEM 6.0 - per le sovrapposizioni relative a [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) (ad es. l&#39;interfaccia touch)

   * Metodo

      * Ricostruire la struttura `/libs` appropriata in `/apps`.

         Questa operazione non richiede una copia 1:1. La [Fusione risorse Sling](/help/sites-developing/sling-resource-merger.md) viene utilizzata per fare riferimento incrociato alle definizioni originali richieste. Sling Resource Merger fornisce servizi per l&#39;accesso e l&#39;unione delle risorse mediante meccanismi diversi (differenziazione).

      * Apportate eventuali modifiche in `/apps`.
   * Vantaggi

      * Più robusto alle modifiche in `/libs`.
      * Ridefinisci solo ciò che è effettivamente richiesto.


* Sovrapposizioni e sovrapposizioni non granite prima di AEM 6.0

   * Metodo

      * Copiare il contenuto da `/libs` a `/apps`

         È necessario copiare l’intero ramo secondario, incluse le proprietà.

      * Apportate eventuali modifiche in `/apps`.
   * Svantaggi

      * Sebbene le modifiche non vadano perdute in caso di modifiche in `/libs`, potrebbe essere necessario ricreare alcune modifiche che si verificano nella sovrapposizione in `/apps`.


>[!CAUTION]
>
>La [Fusione risorse Sling](/help/sites-developing/sling-resource-merger.md) e i metodi correlati possono essere utilizzati solo con [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). Ciò significa che la creazione di una sovrapposizione con una struttura di ossatura è appropriata solo per l’interfaccia touch standard.
>
>Le sovrapposizioni per altre aree (inclusa l’interfaccia classica) comportano la copia del nodo appropriato e dell’intera sottostruttura, quindi l’esecuzione delle modifiche richieste.

Le sovrapposizioni sono il metodo consigliato per molte modifiche, ad esempio [configurazione delle console](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) o [creazione della categoria di selezione nel browser delle risorse nel pannello laterale](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) (utilizzato per l’authoring delle pagine). Sono richiesti come:

* ***non è necessario* apportare modifiche al ramo `/libs`**Eventuali modifiche apportate potrebbero andare perse, in quanto il ramo potrebbe essere modificato ogni volta che:

   * aggiornare l&#39;istanza
   * applica un hotfix
   * installare un pacchetto di funzioni

* Consentono di concentrare le modifiche in un&#39;unica posizione; facilitando il monitoraggio, la migrazione, il backup e/o il debug delle modifiche, se necessario.

## Configurazione dei percorsi di ricerca {#configuring-the-search-paths}

Per le sovrapposizioni, la risorsa consegnata è un insieme di risorse e proprietà recuperate, a seconda dei percorsi di ricerca che è possibile definire:

* La risorsa **Risolutore Search Path** come definito nella [configurazione OSGi](/help/sites-deploying/configuring-osgi.md) per **Apache Sling Resource Resolver Factory**.

   * L&#39;ordine superiore dei percorsi di ricerca indica le rispettive priorità.
   * In un&#39;installazione standard i valori predefiniti principali sono `/apps`, `/libs`, pertanto il contenuto di `/apps` ha una priorità maggiore rispetto a quello di `/libs` (ovvero *overlays*).

* Due utenti di servizi necessitano dell&#39;accesso JCR:READ alla posizione in cui sono memorizzati gli script. Tali utenti sono: components-search-service (utilizzato dai com.day.cq.wcm.coreto access/cache components) e sling-scripting (utilizzato da org.apache.sling.servlets.resolver per trovare servlet).
* È inoltre necessario configurare la seguente configurazione in base al punto in cui vengono inseriti gli script (in questo esempio in /etc, /libs o /apps).

   ```
   PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
   resource.resolver.searchpath=["/etc","/apps","/libs"]
   resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
   ```

* Infine, deve essere configurato anche Servlet Resolver (in questo esempio per aggiungere anche /etc)

   ```
   PID = org.apache.sling.servlets.resolver.SlingServletResolver
   servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
   ```

## Esempio di utilizzo {#example-of-usage}

Alcuni esempi riguardano:

* [Personalizzazione delle console](/help/sites-developing/customizing-consoles-touch.md)
* [Personalizzazione dell’authoring delle pagine](/help/sites-developing/customizing-page-authoring-touch.md)

