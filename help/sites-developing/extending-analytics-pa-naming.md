---
title: Implementazione della denominazione delle pagine lato server per Analytics
seo-title: Implementing Server-Side Page Naming for Analytics
description: Adobe Analytics utilizza la proprietà s.pageName per identificare in modo univoco le pagine e associare i dati raccolti per le pagine
seo-description: Adobe Analytics uses the s.pageName property to uniquely identify pages and to associate the data that is collected for the pages
uuid: 37b92099-0cce-4b2d-b55c-928f636dbd7e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: be2aa297-5b78-4b1d-8ff1-e6a585a177dd
exl-id: 17a4e4dc-804e-44a9-9942-c37dbfc8016f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 0%

---

# Implementazione della denominazione delle pagine lato server per Analytics{#implementing-server-side-page-naming-for-analytics}

Adobe Analytics utilizza `s.pageName` per identificare in modo univoco le pagine e associare i dati raccolti per le pagine. In genere, in AEM si eseguono le seguenti attività per assegnare un valore a questa proprietà che AEM inviata ad Analytics:

* Utilizza il framework del servizio cloud di Analytics per mappare una variabile CQ su Analytics `s.pageName` proprietà. (Vedi [Mappatura dei dati dei componenti con le proprietà di Adobe Analytics](/help/sites-administering/adobeanalytics-mapping.md).)

* Progetta il componente pagina in modo che includa la variabile CQ mappata sul `s.pageName` proprietà. (Vedi [Implementazione del tracciamento di Adobe Analytics per i componenti personalizzati](/help/sites-developing/extending-analytics-components.md).)

Per esporre i dati dei rapporti di Analytics nella console Sites e in Approfondimenti contenuto, AEM richiede il valore della `s.pageName` per ogni pagina. L’API Java di AEM Analytics definisce il `AnalyticsPageNameProvider` Interfaccia implementata per fornire alla console Sites e a Approfondimenti contenuto il valore di `s.pageName` proprietà. Le `AnaltyicsPageNameProvider` il servizio risolve la proprietà pageName sul server a scopo di reporting, in quanto può essere impostata dinamicamente utilizzando Javascript sul client a scopo di tracciamento.

## Servizio provider di nomi di pagina predefinito di Analytics {#the-default-analytics-page-name-provider-service}

La `DefaultPageNameProvider` è il servizio predefinito che determina il valore del `s.pageName` da utilizzare per recuperare i dati di Analytics per una pagina. Il servizio funziona in combinazione con il componente pagina di base AEM ( `/libs/foundation/components/page`). Questo componente pagina definisce le seguenti variabili CQ che devono essere mappate su `s.pageName` proprietà:

* `pagedata.path`: Il valore è impostato sul percorso della pagina.
* `pagedata.title`: Il valore è impostato sul titolo della pagina.
* `pagedata.navTitle`: Il valore è impostato sul titolo di navigazione della pagina.

La `DefaultPageNameProvider` il servizio determina quale di queste variabili CQ è mappata a `s.pageName` nel framework dei servizi cloud di Analytics. Il servizio determina quindi la proprietà pagina appropriata da utilizzare per il recupero dei dati dei rapporti di analytics:

* `pagedata.path`: Il servizio utilizza `page.getPath()`

* `pagedata.title`: Il servizio utilizza `page.getTitle()`

* `pagedata.navTitle`: Il servizio utilizza `page.getNavigationTitle()`

La `page` l&#39;oggetto è [ `com.day.cq.wcm.api.Page`](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/com/day/cq/wcm/api/Page.html) Oggetto Java per la pagina.

Se non mappi una variabile CQ sul `s.pageName` proprietà nel framework, il valore per `s.pageName` viene generato dal percorso della pagina. Ad esempio, la pagina con il percorso `/content/geometrixx/en` utilizza il valore `content:geometrixx:en` per `s.pageName`.

>[!NOTE]
>
>Il servizio DefaultPageNameProvider utilizza una classificazione del servizio pari a 100.

## Mantenimento della continuità nei rapporti di Analytics {#maintaining-continuity-in-analytics-reporting}

Per mantenere una cronologia completa dei dati di analisi per una pagina è necessario che il valore della proprietà s.pageName utilizzata per una pagina non cambi mai. Tuttavia, le proprietà di analisi definite dal componente della pagina di base possono essere facilmente modificate. Ad esempio, lo spostamento di una pagina modifica il valore di `pagedata.path` e interrompe la continuità dello storico dei rapporti:

* I dati raccolti per il percorso precedente non sono più associati alla pagina.
* Se una pagina diversa utilizza il percorso utilizzato da un’altra pagina, la pagina diversa eredita i dati di tale percorso.

Per garantire la continuità delle segnalazioni, `s.pageName` devono avere le seguenti caratteristiche:

* Univoco.
* Stabile.
* Leggibile per l&#39;uomo.

Ad esempio, un componente pagina personalizzato può includere una proprietà di pagina che gli autori utilizzano per specificare un ID univoco per la pagina utilizzata come valore per il `s.pageProperties` proprietà:

* La pagina include una variabile di analisi impostata sul valore dell&#39;ID univoco memorizzato nella proprietà page.
* La variabile di analisi è mappata alla variabile `s.pageProperties` nel framework di Analytics.
* L&#39;implementazione dell&#39;interfaccia AnalyticsPageNameProvider recupera il valore della proprietà page da utilizzare per eseguire query sui dati di Analytics della pagina.

>[!NOTE]
>
>Chiedi aiuto al tuo consulente Analytics per sviluppare una strategia efficace per il tuo `s.pageName` valore.

### Implementazione di un servizio provider di nomi di pagina di Analytics {#implementing-an-analytics-page-name-provider-service}

Implementare `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider` come servizio OSGi per personalizzare la logica che recupera il `s.pageName` valore della proprietà. L’analisi delle pagine Sites e l’analisi dei contenuti utilizzano il servizio per recuperare i dati dei rapporti da Analytics.

L’interfaccia AnalyticsPageNameProvider definisce due metodi da implementare:

* `getPageName`: Restituisce un valore `String` che rappresenta il valore da utilizzare come `s.pageName` proprietà.

* `getResource`: Restituisce un valore `org.apache.sling.api.resource.Resource` che rappresenta la pagina associata alla `s.pageName` proprietà.

Entrambi i metodi richiedono un `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext` come parametro. La `AnalyticsPageNameContext` class fornisce informazioni sul contesto delle chiamate di analytics:

* Percorso base della risorsa pagina.
* La `Framework` oggetto per la configurazione del servizio cloud di Analytics.
* La `Resource` oggetto per la pagina.
* La `ResourceResolver` oggetto per la pagina.

La classe fornisce anche un setter per il nome della pagina.

### Implementazione di esempio di AnalyticsPageNameProvider {#example-analyticspagenameprovider-implementation}

Esempio `AnalyticsPageNameProvider` l&#39;implementazione supporta un componente pagina personalizzato:

* Il componente estende il componente della pagina di base.
* La finestra di dialogo include un campo che viene utilizzato dagli autori per specificare il valore del `s.pageName` proprietà.
* Il valore della proprietà viene memorizzato nella proprietà pageName della proprietà `jcr:content`nodo delle istanze della pagina.
* La proprietà analytics che memorizza il `s.pageName` viene chiamata `pagedata.pagename`. Questa proprietà è mappata al `s.pageName` nel framework di Analytics.

La seguente attuazione `getPageName` restituisce il valore della proprietà node pageName se il mapping del framework è configurato correttamente:

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

Il codice seguente rappresenta l’intera classe, incluse le annotazioni SCR che configurano il servizio. Tieni presente che la classificazione del servizio è 200 e sostituisce il servizio predefinito.

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
