---
title: Sovrapposizioni
seo-title: Overlays
description: AEM utilizza il principio delle sovrapposizioni per estendere e personalizzare le console e altre funzionalità
seo-description: AEM uses the principle of overlays to allow you to extend and customize the consoles and other functionality
uuid: d14c08fe-04c0-4925-8c99-c6644357919d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0470b74c-2c34-4327-afed-b95eefb1d521
exl-id: e57a6971-6a6f-427b-a8cd-a2f2e8cdf9e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 0%

---

# Sovrapposizioni{#overlays}

L’AEM (e prima di questo, CQ) ha a lungo utilizzato il principio delle sovrapposizioni per consentire di estendere e personalizzare il [console](/help/sites-developing/customizing-consoles-touch.md) e altre funzionalità (ad esempio [authoring delle pagine](/help/sites-developing/customizing-page-authoring-touch.md)).

Sovrapposizione è un termine che può essere utilizzato in molti contesti. In questo contesto (estensione dell’AEM), per sovrapposizione si intende l’assunzione delle funzionalità predefinite e l’imposizione di definizioni personalizzate (per personalizzare la funzionalità standard).

In un’istanza standard la funzionalità predefinita è mantenuta in `/libs` e si consiglia di definire la sovrapposizione (personalizzazioni) in `/apps` filiale. L’AEM utilizza un percorso di ricerca per trovare una risorsa, eseguendo prima la ricerca nel `/apps` e quindi il `/libs` filiale (il [il percorso di ricerca può essere configurato](#configuring-the-search-paths)). Questo meccanismo significa che la sovrapposizione (e le personalizzazioni qui definite) avranno la priorità.

A partire dalla versione 6.0 dell’AEM, sono state apportate modifiche alle modalità di implementazione e utilizzo delle sovrapposizioni:

* AEM 6.0 e versioni successive - favorevoli [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)Sovrapposizioni relative a (ad es. interfaccia touch)

   * Metodo

      * Ricostruire l’appropriato `/libs` struttura in `/apps`.

         Questo non richiede una copia 1:1, il [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) viene utilizzato per fare riferimento incrociato alle definizioni originali richieste. Sling Resource Merger fornisce servizi per l’accesso e l’unione delle risorse mediante meccanismi di differenze.

      * Apporta le modifiche in `/apps`.
   * Vantaggi

      * Più robusto per le modifiche in `/libs`.
      * Ridefinisci solo ciò che è effettivamente necessario.


* Sovrapposizioni e sovrapposizioni diverse da Granite prima di AEM 6.0

   * Metodo

      * Copia il contenuto da `/libs` a `/apps`

         È necessario copiare l’intero ramo secondario, comprese le proprietà.

      * Apporta le modifiche in `/apps`.
   * Svantaggi

      * Anche se le modifiche non andranno perse quando qualcosa cambia in `/libs`, potrebbe essere necessario ricreare alcune modifiche che si verificano nella sovrapposizione in `/apps`.


>[!CAUTION]
>
>Il [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) e i metodi correlati possono essere utilizzati solo con [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). Ciò significa che la creazione di una sovrapposizione con una struttura di ossatura è appropriata solo per l’interfaccia utente standard touch.
>
>Le sovrapposizioni per altre aree (inclusa l’interfaccia classica) implicano la copia del nodo appropriato e dell’intera sottostruttura, quindi l’apporto delle modifiche necessarie.

Le sovrapposizioni sono il metodo consigliato per molte modifiche, ad esempio [configurazione delle console](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) o [creazione della categoria di selezione nel browser risorse nel pannello laterale](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) (utilizzato per l’authoring delle pagine). Sono necessari in quanto:

* Tu ***non deve* apportare modifiche in `/libs` filiale **Qualsiasi modifica apportata potrebbe andare persa, poiché questo ramo potrebbe subire modifiche ogni volta che:

   * aggiorna nell’istanza
   * applicare un hotfix
   * installare un feature pack

* Concentrano le modifiche in un&#39;unica posizione, semplificando il monitoraggio, la migrazione, il backup e/o il debug delle modifiche in base alle esigenze.

## Configurazione dei percorsi di ricerca {#configuring-the-search-paths}

Per le sovrapposizioni, la risorsa consegnata è un aggregato delle risorse e delle proprietà recuperate, a seconda dei percorsi di ricerca che possono essere definiti:

* La risorsa **Percorso di ricerca del Risolutore** come definito nella [Configurazione OSGi](/help/sites-deploying/configuring-osgi.md) per **Apache Sling Resource Resolver Factory**.

   * L’ordine discendente dei percorsi di ricerca indica le rispettive priorità.
   * In un&#39;installazione standard i valori predefiniti principali sono `/apps`, `/libs` - in modo che il contenuto `/apps` ha una priorità più alta di quella di `/libs` (ad es. *sovrapposizioni* it).

* Due utenti del servizio hanno bisogno dell&#39;accesso JCR:READ alla posizione in cui sono memorizzati gli script. Tali utenti sono: components-search-service (utilizzato dai componenti com.day.cq.wcm.coreto access/cache ) e sling-scripting (utilizzato da org.apache.sling.servlets.resolver per trovare i servlet).
* La seguente configurazione deve essere configurata anche in base alla posizione in cui inserisci gli script (in questo esempio in /etc, /libs o /apps).

   ```
   PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
   resource.resolver.searchpath=["/etc","/apps","/libs"]
   resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
   ```

* Infine, è necessario configurare anche il Servlet Resolver (in questo esempio per aggiungere anche /etc)

   ```
   PID = org.apache.sling.servlets.resolver.SlingServletResolver
   servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
   ```

## Esempio di utilizzo {#example-of-usage}

Alcuni esempi sono trattati quando:

* [Personalizzazione delle console](/help/sites-developing/customizing-consoles-touch.md)
* [Personalizzazione dell’authoring delle pagine](/help/sites-developing/customizing-page-authoring-touch.md)
