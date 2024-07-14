---
title: Sovrapposizioni
description: Adobe Experience Manager utilizza il principio delle sovrapposizioni per estendere e personalizzare le console e altre funzionalità.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: e57a6971-6a6f-427b-a8cd-a2f2e8cdf9e2
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 0%

---

# Sovrapposizioni{#overlays}

Adobe Experience Manager (AEM), e prima ancora CQ, ha a lungo utilizzato il principio delle sovrapposizioni per consentire di estendere e personalizzare le [console](/help/sites-developing/customizing-consoles-touch.md) e altre funzionalità (ad esempio, [authoring delle pagine](/help/sites-developing/customizing-page-authoring-touch.md)).

Sovrapposizione è un termine utilizzato in molti contesti. In questo contesto (estensione dell’AEM), una sovrapposizione significa accettare la funzionalità predefinita e imporre le tue definizioni al riguardo (per personalizzare la funzionalità standard).

In un&#39;istanza standard, la funzionalità predefinita si trova in `/libs` e si consiglia di definire la sovrapposizione (personalizzazioni) nel ramo `/apps`. AEM utilizza un percorso di ricerca per trovare una risorsa, eseguendo prima la ricerca nel ramo `/apps` e poi nel ramo `/libs` (è possibile configurare il percorso di ricerca [](#configuring-the-search-paths)). Questo meccanismo indica che la sovrapposizione (e le personalizzazioni ivi definite) ha la priorità.

A partire dalla versione 6.0 dell’AEM, sono state apportate modifiche alle modalità di implementazione e utilizzo delle sovrapposizioni:

* AEM 6.0 e attivato: per sovrapposizioni relative a [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) (ovvero l&#39;interfaccia utente touch)

   * Metodo

      * Ricostruire la struttura `/libs` appropriata in `/apps`.

        Questa operazione non richiede una copia 1:1, [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) viene utilizzato per fare un riferimento incrociato alle definizioni originali richieste. Sling Resource Merger fornisce servizi per l’accesso e l’unione di risorse con meccanismi di differenze.

      * In `/apps`, apportare le modifiche desiderate.

   * Vantaggi

      * Più affidabile per le modifiche in `/libs`.
      * Ridefinisci solo ciò che è richiesto.

* Sovrapposizioni e sovrapposizioni non-Granite prima di AEM 6.0

   * Metodo

      * Copia il contenuto da `/libs` a `/apps`

        Copia l’intero sottoramo, comprese le proprietà.

      * In `/apps`, apportare le modifiche desiderate.

   * Svantaggi

      * Anche se le modifiche non andranno perse quando qualcosa cambia in `/libs`, potrebbe essere necessario ricreare alcune modifiche che si verificano nella sovrapposizione in `/apps`.

>[!CAUTION]
>
>[Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) e i metodi correlati possono essere utilizzati solo con [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html). Ciò significa che la creazione di una sovrapposizione con una struttura di ossatura è appropriata solo per l’interfaccia utente standard touch.
>
>Le sovrapposizioni per altre aree (inclusa l’interfaccia classica) implicano la copia del nodo e dell’intera sottostruttura appropriati, quindi l’apporto delle modifiche necessarie.

Le sovrapposizioni sono il metodo consigliato per molte modifiche, ad esempio [configurazione delle console](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) o [creazione della categoria di selezione nel browser risorse nel pannello laterale](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) (utilizzato durante la creazione delle pagine). Sono necessari in quanto:

* ***Non* apportare modifiche nel ramo `/libs`**Qualsiasi modifica apportata potrebbe andare persa, poiché questo ramo potrebbe subire modifiche ogni volta che:

   * aggiorna nell’istanza
   * applicare un hotfix
   * installare un feature pack

* Concentrano le modifiche in un&#39;unica posizione, semplificando il monitoraggio, la migrazione, il backup o il debug delle modifiche, in base alle esigenze.

## Configurazione dei percorsi di ricerca {#configuring-the-search-paths}

Per le sovrapposizioni, la risorsa consegnata è un aggregato delle risorse e delle proprietà recuperate, a seconda dei percorsi di ricerca che possono essere definiti:

* La risorsa **Percorso di ricerca del Risolutore** come definito nella [configurazione OSGi](/help/sites-deploying/configuring-osgi.md) per **Apache Sling Resource Resolver Factory**.

   * L’ordine discendente dei percorsi di ricerca indica le rispettive priorità.
   * In un&#39;installazione standard, i valori predefiniti principali sono `/apps`, `/libs`, pertanto il contenuto di `/apps` ha una priorità maggiore rispetto a quello di `/libs` (ovvero *sovrapposizioni*).

* Due utenti del servizio hanno bisogno dell&#39;accesso JCR:READ alla posizione in cui sono memorizzati gli script. Tali utenti sono: components-search-service (utilizzato dai componenti com.day.cq.wcm.coreto access/cache ) e sling-scripting (utilizzato da org.apache.sling.servlets.resolver per trovare i servlet).
* La seguente configurazione deve essere configurata anche in base alla posizione in cui inserisci gli script (in questo esempio in /etc, /libs o /apps).

  ```
  PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
  resource.resolver.searchpath=["/etc","/apps","/libs"]
  resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
  ```

* Infine, è necessario configurare anche il Servlet Resolver (in questo esempio, per aggiungere anche /etc)

  ```
  PID = org.apache.sling.servlets.resolver.SlingServletResolver
  servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
  ```

## Esempio di utilizzo {#example-of-usage}

Alcuni esempi sono trattati quando:

* [Personalizzazione delle console](/help/sites-developing/customizing-consoles-touch.md)
* [Personalizzazione dell’authoring delle pagine](/help/sites-developing/customizing-page-authoring-touch.md)
