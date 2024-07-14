---
title: Implementazione della denominazione delle pagine lato server per Analytics
description: Adobe Analytics utilizza la proprietà s.pageName per identificare in modo univoco le pagine e associare i dati raccolti per le pagine
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 17a4e4dc-804e-44a9-9942-c37dbfc8016f
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 0%

---

# Implementazione della denominazione delle pagine lato server per Analytics{#implementing-server-side-page-naming-for-analytics}

Adobe Analytics utilizza la proprietà `s.pageName` per identificare in modo univoco le pagine e associare i dati raccolti per le pagine. In genere, per assegnare un valore a questa proprietà che l’AEM invia ad Analytics, esegui le seguenti attività in AEM:

* Utilizzare il framework del servizio cloud Analytics per mappare una variabile CQ alla proprietà Analytics `s.pageName`. (Vedi [Mappatura dei dati dei componenti con le proprietà di Adobe Analytics](/help/sites-administering/adobeanalytics-mapping.md).)

* Progettare il componente page in modo che includa la variabile CQ mappata alla proprietà `s.pageName`. (Vedi [Implementazione del tracciamento di Adobe Analytics per i componenti personalizzati](/help/sites-developing/extending-analytics-components.md).)

Per esporre i dati dei rapporti di Analytics nella console Sites e in Content Insight, AEM richiede il valore della proprietà `s.pageName` per ogni pagina. L&#39;API Java di AEM Analytics definisce l&#39;interfaccia `AnalyticsPageNameProvider` implementata per fornire alla console Sites e a Content Insights il valore della proprietà `s.pageName`. Il servizio `AnaltyicsPageNameProvider` risolve la proprietà pageName sul server a scopo di reporting, in quanto può essere impostata dinamicamente utilizzando JavaScript sul client a scopo di tracciamento.

## Servizio provider nome pagina di Analytics predefinito {#the-default-analytics-page-name-provider-service}

Il servizio `DefaultPageNameProvider` è il servizio predefinito che determina il valore della proprietà `s.pageName` da utilizzare per recuperare i dati di Analytics per una pagina. Il servizio funziona insieme al componente pagina di base AEM ( `/libs/foundation/components/page`). Questo componente page definisce le seguenti variabili CQ da mappare alla proprietà `s.pageName`:

* `pagedata.path`: valore impostato sul percorso della pagina.
* `pagedata.title`: valore impostato sul titolo della pagina.
* `pagedata.navTitle`: valore impostato sul titolo di navigazione della pagina.

Il servizio `DefaultPageNameProvider` determina quali di queste variabili CQ sono mappate alla proprietà `s.pageName` nel framework del servizio cloud Analytics. Il servizio determina quindi la proprietà di pagina appropriata da utilizzare per recuperare i dati del rapporto di analisi:

* `pagedata.path`: il servizio utilizza `page.getPath()`

* `pagedata.title`: il servizio utilizza `page.getTitle()`

* `pagedata.navTitle`: il servizio utilizza `page.getNavigationTitle()`

L&#39;oggetto `page` è l&#39;oggetto Java [`com.day.cq.wcm.api.Page`](https://helpx.adobe.com/experience-manager/6-3/sites-developing/reference-materials/javadoc/com/day/cq/wcm/api/Page.html) per la pagina.

Se non mappi una variabile CQ alla proprietà `s.pageName` nel framework, il valore per `s.pageName` viene generato dal percorso della pagina. Ad esempio, la pagina con il percorso `/content/geometrixx/en` utilizza il valore `content:geometrixx:en` per `s.pageName`.

>[!NOTE]
>
>Il servizio DefaultPageNameProvider utilizza una classificazione del servizio di 100.

## Mantenimento della continuità nel reporting di Analytics {#maintaining-continuity-in-analytics-reporting}

Per mantenere una cronologia completa dei dati di analisi per una pagina, è necessario che il valore della proprietà s.pageName utilizzata per una pagina non cambi mai. Tuttavia, le proprietà di analisi definite dal componente della pagina di base possono essere facilmente modificate. Ad esempio, lo spostamento di una pagina modifica il valore di `pagedata.path` e interrompe la continuità della cronologia di reporting:

* I dati raccolti per il percorso precedente non sono più associati alla pagina.
* Se una pagina diversa utilizza il percorso utilizzato un’altra pagina, tale pagina eredita i dati per tale percorso.

Per garantire la continuità del reporting, il valore di `s.pageName` deve avere le seguenti caratteristiche:

* Univoco.
* Stabile.
* Leggibile.

Ad esempio, un componente pagina personalizzato può includere una proprietà di pagina utilizzata dagli autori per specificare un ID univoco per la pagina da utilizzare come valore per la proprietà `s.pageProperties`:

* La pagina include una variabile di analisi impostata sul valore dell’ID univoco memorizzato nella proprietà della pagina.
* La variabile di analisi è mappata alla proprietà `s.pageProperties` nel framework di Analytics.
* L’implementazione dell’interfaccia AnalyticsPageNameProvider recupera il valore della proprietà della pagina da utilizzare per l’esecuzione di query sui dati di Analytics della pagina.

>[!NOTE]
>
>Chiedi al tuo consulente Analytics di aiutarti a sviluppare una strategia efficace per il tuo valore `s.pageName`.

### Implementazione di un servizio provider del nome della pagina di Analytics {#implementing-an-analytics-page-name-provider-service}

Implementa l&#39;interfaccia `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameProvider` come servizio OSGi per personalizzare la logica che recupera il valore della proprietà `s.pageName`. Le funzioni di analisi della pagina Sites e Insight sui contenuti utilizzano il servizio per recuperare i dati dei rapporti da Analytics.

L&#39;interfaccia AnalyticsPageNameProvider definisce due metodi che è necessario implementare:

* `getPageName`: restituisce un valore `String` che rappresenta il valore da utilizzare come proprietà `s.pageName`.

* `getResource`: restituisce un oggetto `org.apache.sling.api.resource.Resource` che rappresenta la pagina associata alla proprietà `s.pageName`.

Entrambi i metodi accettano un oggetto `com.day.cq.analytics.sitecatalyst.AnalyticsPageNameContext` come parametro. La classe `AnalyticsPageNameContext` fornisce informazioni sul contesto delle chiamate di analisi:

* Percorso di base della risorsa della pagina.
* Oggetto `Framework` per la configurazione del servizio cloud Analytics.
* Oggetto `Resource` per la pagina.
* Oggetto `ResourceResolver` per la pagina.

La classe fornisce anche un setter per il nome della pagina.

### Esempio di implementazione di AnalyticsPageNameProvider {#example-analyticspagenameprovider-implementation}

L&#39;implementazione `AnalyticsPageNameProvider` dell&#39;esempio seguente supporta un componente pagina personalizzato:

* Il componente estende il componente pagina di base.
* La finestra di dialogo include un campo utilizzato dagli autori per specificare il valore della proprietà `s.pageName`.
* Il valore della proprietà viene memorizzato nella proprietà pageName del nodo `jcr:content` delle istanze della pagina.
* La proprietà di analisi che memorizza la proprietà `s.pageName` è denominata `pagedata.pagename`. Questa proprietà è mappata alla proprietà `s.pageName` nel framework Analytics.

La seguente implementazione del metodo `getPageName` restituisce il valore della proprietà del nodo pageName se il mapping del framework è configurato correttamente:

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

Il codice seguente rappresenta l’intera classe, incluse le annotazioni SCR che configurano il servizio. La classificazione del servizio è 200 e sostituisce il servizio predefinito.

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
