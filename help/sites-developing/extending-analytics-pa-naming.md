---
title: Implementazione della denominazione delle pagine lato server per Analytics
seo-title: Implementazione della denominazione delle pagine lato server per Analytics
description: ' Adobe Analytics utilizza la proprietà s.pageName per identificare in modo univoco le pagine e per associare i dati raccolti per le pagine'
seo-description: ' Adobe Analytics utilizza la proprietà s.pageName per identificare in modo univoco le pagine e per associare i dati raccolti per le pagine'
uuid: 37b92099-0cce-4b2d-b55c-928f636dbd7e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: be2aa297-5b78-4b1d-8ff1-e6a585a177dd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 0%

---


# Implementazione della denominazione delle pagine lato server per Analytics{#implementing-server-side-page-naming-for-analytics}

 Adobe Analytics utilizza la proprietà `s.pageName` per identificare in modo univoco le pagine e per associare i dati raccolti per le pagine. In genere, per assegnare un valore a questa proprietà che AEM inviata ad Analytics, vengono eseguite le seguenti operazioni in AEM:

* Utilizzate il framework del servizio cloud di Analytics per mappare una variabile CQ alla proprietà Analytics `s.pageName`. (Vedere [Mappatura dei dati dei componenti con  proprietà Adobe Analytics](/help/sites-administering/adobeanalytics-mapping.md).)

* Progettare il componente pagina in modo che includa la variabile CQ mappata sulla proprietà `s.pageName`. (Vedere [Implementazione  tracciamento Adobe Analytics per componenti personalizzati](/help/sites-developing/extending-analytics-components.md).)

Per esporre i dati dei report di Analytics nella console Siti e in Content Insight, AEM richiede il valore della proprietà `s.pageName` per ogni pagina. L&#39;API Java AEM Analytics definisce l&#39;interfaccia `AnalyticsPageNameProvider` implementata per fornire alla console Siti e a Content Insights il valore della proprietà `s.pageName`. Il servizio `AnaltyicsPageNameProvider` risolve la proprietà pageName sul server a scopo di reporting, in quanto può essere impostata in modo dinamico utilizzando Javascript sul client a scopo di tracciamento.

## Servizio provider nome pagina Analytics predefinito {#the-default-analytics-page-name-provider-service}

Il servizio `DefaultPageNameProvider` è il servizio predefinito che determina il valore della proprietà `s.pageName` da utilizzare per il recupero dei dati di Analytics per una pagina. Il servizio funziona insieme al componente AEM pagina di base ( `/libs/foundation/components/page`). Questo componente di pagina definisce le seguenti variabili CQ che devono essere mappate sulla proprietà `s.pageName`:

* `pagedata.path`: Il valore è impostato sul percorso della pagina.
* `pagedata.title`: Il valore è impostato sul titolo della pagina.
* `pagedata.navTitle`: Il valore è impostato sul titolo di navigazione della pagina.

Il servizio `DefaultPageNameProvider` determina quale di queste variabili CQ viene mappata alla proprietà `s.pageName` nel framework del servizio cloud di Analytics. Il servizio determina quindi la proprietà pagina appropriata da utilizzare per il recupero dei dati dei report di analisi:

* `pagedata.path`: Il servizio utilizza  `page.getPath()`

* `pagedata.title`: Il servizio utilizza  `page.getTitle()`

* `pagedata.navTitle`: Il servizio utilizza  `page.getNavigationTitle()`

L&#39;oggetto `page` è l&#39;oggetto Java [ `com.day.cq.wcm.api.Page`](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/com/day/cq/wcm/api/Page.html) della pagina.

Se non mappate una variabile CQ sulla proprietà `s.pageName` nel framework, il valore per `s.pageName` viene generato dal percorso della pagina. Ad esempio, la pagina con il percorso `/content/geometrixx/en` utilizza il valore `content:geometrixx:en` per `s.pageName`.

>[!NOTE]
>
>Il servizio DefaultPageNameProvider utilizza una classificazione del servizio pari a 100.

## Mantenimento della continuità nei report di Analytics {#maintaining-continuity-in-analytics-reporting}

Per mantenere una cronologia completa dei dati di analisi per una pagina è necessario che il valore della proprietà s.pageName utilizzata per una pagina non cambi mai. Tuttavia, le proprietà di analisi definite dal componente pagina di base possono essere facilmente modificate. Ad esempio, spostando una pagina si modifica il valore di `pagedata.path` e si interrompe la continuità della cronologia del reporting:

* I dati raccolti per il percorso precedente non sono più associati alla pagina.
* Se una pagina diversa utilizza il percorso utilizzato da un&#39;altra pagina, la pagina diversa eredita i dati per tale percorso.

Per garantire la continuità della segnalazione, il valore di `s.pageName` deve avere le seguenti caratteristiche:

* Univoco.
* Stabile.
* Leggibile dall&#39;uomo.

Ad esempio, un componente pagina personalizzato può includere una proprietà pagina che gli autori utilizzano per specificare un ID univoco per la pagina che viene utilizzata come valore per la proprietà `s.pageProperties`:

* La pagina include una variabile di analisi impostata sul valore dell&#39;ID univoco memorizzato nella proprietà page.
* La variabile di analisi viene mappata sulla proprietà `s.pageProperties` nel framework Analytics.
* L&#39;implementazione dell&#39;interfaccia AnalyticsPageNameProvider recupera il valore della proprietà page da utilizzare per eseguire query sui dati Analytics della pagina.

>[!NOTE]
>
>Chiedi aiuto al tuo consulente Analytics per sviluppare una strategia efficace per il tuo `s.pageName` valore.

### Implementazione di un servizio provider di nomi pagina di Analytics {#implementing-an-analytics-page-name-provider-service}

Implementate l&#39;interfaccia `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider` come servizio OSGi per personalizzare la logica che recupera il valore della proprietà `s.pageName`. L&#39;analisi delle pagine Siti e Content Insight utilizzano il servizio per recuperare i dati dei report da Analytics.

L&#39;interfaccia AnalyticsPageNameProvider definisce due metodi da implementare:

* `getPageName`: Restituisce un  `String` valore che rappresenta il valore da utilizzare come  `s.pageName` proprietà.

* `getResource`: Restituisce un  `org.apache.sling.api.resource.Resource` oggetto che rappresenta la pagina associata alla  `s.pageName` proprietà.

Entrambi i metodi utilizzano un oggetto `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext` come parametro. La classe `AnalyticsPageNameContext` fornisce informazioni sul contesto delle chiamate di analisi:

* Percorso di base della risorsa di pagina.
* L&#39;oggetto `Framework` per la configurazione del servizio cloud di Analytics.
* L&#39;oggetto `Resource` per la pagina.
* L&#39;oggetto `ResourceResolver` per la pagina.

La classe fornisce inoltre un setter per il nome della pagina.

### Esempio di implementazione di AnalyticsPageNameProvider {#example-analyticspagenameprovider-implementation}

L&#39;implementazione di esempio seguente `AnalyticsPageNameProvider` supporta un componente pagina personalizzato:

* Il componente estende il componente della pagina di base.
* La finestra di dialogo include un campo che viene utilizzato dagli autori per specificare il valore della proprietà `s.pageName`.
* Il valore della proprietà è memorizzato nella proprietà pageName del nodo `jcr:content`delle istanze di pagina.
* La proprietà analytics che memorizza la proprietà `s.pageName` è denominata `pagedata.pagename`. Questa proprietà viene mappata sulla proprietà `s.pageName` nel framework Analytics.

La seguente implementazione del metodo `getPageName` restituisce il valore della proprietà node pageName se la mappatura framework è configurata correttamente:

```java
public String getPageName(AnalyticsPageNameContext context) {
        String pageName = null;

        Framework framework = context.getFramework();
        Resource resource = context.getResource();

        if (resource != null && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            Page page = resource.adaptTo(Page.class);
            if (cqVar.equals("pagedata.pagename")) {
                pageName = page.getProperties().get("pageName",null);
            }
        }
        return pageName;
    }
```

La seguente implementazione del metodo getResource restituisce l&#39;oggetto Resource per la pagina:

```java
     public Resource getResource(AnalyticsPageNameContext context) {
        Resource res = null;

        Framework framework = context.getFramework();
        ResourceResolver resolver = context.getResourceResolver();
        String pageName = context.getPageName();
        String basePath = context.getBasePath();

        if (pageName != null && basePath != null && resolver != null
                && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            if (cqVar.equals("pagedata.pagename")) {
             Iterator<Resource>
             hits = resolver.findResources(createQuery(pageName, basePath, "pagename"), Query.JCR_SQL2);
             if (hits.hasNext()) {
              res = hits.next();
              res = res.getParent();
             }
            }
        }
        return res;
    }

    private String createQuery(String pageName, String basePath, String propName) {
        return "SELECT * FROM [cq:PageContent] WHERE ISDESCENDANTNODE(["
                + basePath + "]) and [" + propName + "] = \"" + pageName + "\"";
    }
```

Il codice seguente rappresenta l&#39;intera classe, incluse le annotazioni SCR che configurano il servizio. La classifica del servizio è 200 e sostituisce il servizio predefinito.

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2019 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and may be covered by U.S. and Foreign Patents,
 * patents in process, and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.day.cq.analytics.sitecatalyst;

import java.util.Iterator;

import javax.jcr.query.Query;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ResourceResolver;
import org.osgi.framework.Constants;
import org.osgi.service.component.annotations.Component;

import com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext;
import com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider;
import com.day.cq.analytics.sitecatalyst.Framework;
import com.day.cq.wcm.api.Page;

import static com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext.S_PAGE_NAME;

/**
 * Default implementation of {@link AnalyticsPageNameProvider} that resolves
 * page title, path or navTitle if mapped in {@link Framework}.
 */
@Component(
    service = { AnalyticsPageNameProvider.class },
    property = {
        Constants.SERVICE_DESCRIPTION + "=Example Page Name Resolver implementation",
        Constants.SERVICE_RANKING + ":Integer=200"
    }
)
public class ExamplePageNameProvider implements AnalyticsPageNameProvider {
    public String getPageName(AnalyticsPageNameContext context) {
        String pageName = null;

        Framework framework = context.getFramework();
        Resource resource = context.getResource();

        if (resource != null && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            Page page = resource.adaptTo(Page.class);
            if (cqVar.equals("pagedata.path")) {
                pageName = page.getProperties().get("pageName",null);
            }
        }
        return pageName;
    }

    public Resource getResource(AnalyticsPageNameContext context) {
        Resource res = null;

        Framework framework = context.getFramework();
        ResourceResolver resolver = context.getResourceResolver();
        String pageName = context.getPageName();
        String basePath = context.getBasePath();

        if (pageName != null && basePath != null && resolver != null
                && framework != null && framework.mapsSCVariable(S_PAGE_NAME)) {
            String cqVar = framework.getMapping(S_PAGE_NAME);
            if (cqVar.equals("pagedata.pagename")) {
                Iterator<Resource>
                hits = resolver.findResources(createQuery(pageName, basePath, "pagename"), Query.JCR_SQL2);
                if (hits.hasNext()) {
                    res = hits.next();
                    res = res.getParent();
                }
            }
        }
        return res;
    }

    private String createQuery(String pageName, String basePath, String propName) {
        return "SELECT * FROM [cq:PageContent] WHERE ISDESCENDANTNODE(["
                + basePath + "]) and [" + propName + "] = \"" + pageName + "\"";
    }
}
```

