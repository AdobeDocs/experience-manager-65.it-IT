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

AEM (e prima di questo, CQ) utilizza da tempo il principio delle sovrapposizioni per consentire di estendere e personalizzare la [console](/help/sites-developing/customizing-consoles-touch.md) e altre funzionalità (ad esempio, [authoring delle pagine](/help/sites-developing/customizing-page-authoring-touch.md)).

La sovrapposizione è un termine che può essere utilizzato in molti contesti. In questo contesto (estensione AEM) una sovrapposizione implica l’utilizzo delle funzionalità predefinite e l’imposizione di definizioni personalizzate (per personalizzare la funzionalità standard).

In un&#39;istanza standard, la funzionalità predefinita è mantenuta in `/libs` e si consiglia di definire la sovrapposizione (personalizzazioni) in `/apps` ramo. AEM utilizza un percorso di ricerca per trovare una risorsa, eseguendo prima la ricerca `/apps` e quindi `/libs` la [è possibile configurare il percorso di ricerca](#configuring-the-search-paths)). Questo meccanismo significa che la sovrapposizione (e le personalizzazioni qui definite) avrà priorità.

A partire dalla versione 6.0 AEM sono state apportate modifiche alle modalità di implementazione e utilizzo delle sovrapposizioni:

* AEM 6.0 in avanti - per [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)Sovrapposizioni correlate (cioè l’interfaccia touch)

   * Metodo

      * Ricostruire l&#39;appropriato `/libs` struttura `/apps`.

         Questa operazione non richiede una copia 1:1, [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) viene utilizzato per fare riferimento incrociato alle definizioni originali richieste. Sling Resource Merger fornisce servizi per l’accesso e l’unione delle risorse tramite meccanismi di differenziazione (differenze).

      * Apporta le modifiche in `/apps`.
   * Vantaggi

      * Più robusto per le modifiche in `/libs`.
      * Ridefinisci solo ciò che è effettivamente richiesto.


* Sovrapposizioni e sovrapposizioni non granite prima di AEM 6.0

   * Metodo

      * Copia il contenuto da `/libs` a `/apps`

         È necessario copiare l’intero ramo secondario, incluse le proprietà.

      * Apporta le modifiche in `/apps`.
   * Svantaggi

      * Anche se le modifiche non andranno perse quando qualcosa cambia in `/libs`, potrebbe essere necessario ricreare alcune modifiche che si verificano nella sovrapposizione in `/apps`.


>[!CAUTION]
>
>La [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) e i relativi metodi possono essere utilizzati solo con [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html). Ciò significa che la creazione di una sovrapposizione con una struttura dell’ossatura è appropriata solo per l’interfaccia utente standard abilitata per il tocco.
>
>Le sovrapposizioni per altre aree (inclusa l’interfaccia classica) richiedono di copiare il nodo appropriato e l’intera sottostruttura, quindi di apportare le modifiche necessarie.

Le sovrapposizioni sono il metodo consigliato per molte modifiche, ad esempio [configurazione delle console](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) o [creazione della categoria di selezione nel browser risorse nel pannello laterale](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) (utilizzato per l’authoring delle pagine). Sono richiesti come:

* You ***non deve* apporta modifiche nel `/libs` filiale **Eventuali modifiche apportate potrebbero andare perse, in quanto questo ramo è soggetto a modifiche ogni volta che:

   * aggiornamento dell&#39;istanza
   * applica un hotfix
   * installare un feature pack

* Concentrano le modifiche in un&#39;unica posizione; semplificando il monitoraggio, la migrazione, il backup e/o il debug delle modifiche, a seconda delle necessità.

## Configurazione dei percorsi di ricerca {#configuring-the-search-paths}

Per le sovrapposizioni la risorsa consegnata è un aggregato delle risorse e delle proprietà recuperate, a seconda dei percorsi di ricerca che possono essere definiti:

* La risorsa **Percorso di ricerca del risolutore** come definito nel [Configurazione OSGi](/help/sites-deploying/configuring-osgi.md) per **Factory di Apache Sling Resource Resolver**.

   * L’ordine dall’alto verso il basso dei percorsi di ricerca indica le rispettive priorità.
   * In un&#39;installazione standard, i valori predefiniti principali sono `/apps`, `/libs` - il contenuto `/apps` ha una priorità più alta di quella di `/libs` (cioè *sovrapposizioni* it).

* Due utenti di servizi necessitano dell’accesso JCR:READ al percorso in cui sono memorizzati gli script. Gli utenti sono: components-search-service (utilizzato da com.day.cq.wcm.coreto access/cache components) e sling-scripting (utilizzato da org.apache.sling.servlets.resolver per trovare i servlet).
* La seguente configurazione deve anche essere configurata in base al punto in cui hai inserito i tuoi script (in questo esempio sotto /etc, /libs o /apps).

   ```
   PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
   resource.resolver.searchpath=["/etc","/apps","/libs"]
   resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
   ```

* Infine, anche il Risolutore Servlet deve essere configurato (in questo esempio per aggiungere anche /etc)

   ```
   PID = org.apache.sling.servlets.resolver.SlingServletResolver
   servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
   ```

## Esempio di utilizzo {#example-of-usage}

Alcuni esempi sono trattati quando:

* [Personalizzazione delle console](/help/sites-developing/customizing-consoles-touch.md)
* [Personalizzazione dell’authoring delle pagine](/help/sites-developing/customizing-page-authoring-touch.md)
