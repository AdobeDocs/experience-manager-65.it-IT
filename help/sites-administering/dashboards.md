---
title: Dashboard
seo-title: Dashboards
description: Scopri come creare, configurare e sviluppare nuove dashboard per l’AEM.
seo-description: Learn how to create, configure and develop new AEM dashboards.
uuid: 3eadbba2-0ce1-41be-a9f8-e6cafa109893
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 40560e06-2508-45a4-a648-39629ed54f28
exl-id: 5b934e3a-f554-46ec-a913-8d570abb1503
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 4%

---

# Dashboard{#dashboards}

Con l’AEM puoi gestire molti contenuti di tipi diversi (ad esempio pagine, risorse). I dashboard dell’AEM offrono un modo semplice e personalizzabile di definire le pagine che visualizzano i dati consolidati.

>[!NOTE]
>
>I dashboard di AEM vengono creati in base all’utente, in modo che un utente possa accedere solo al proprio dashboard.
>
>Tuttavia, [Modelli dashboard](#creating-a-dashboard-template) può essere utilizzato per condividere la configurazione e il layout del dashboard comuni.

![chlimage_1-22](assets/chlimage_1-22.jpeg)

## Amministrazione delle dashboard {#administering-dashboards}

### Creazione Di Un Dashboard {#creating-a-dashboard}

1. In **Strumenti** , fare clic su **Console di configurazione**.
1. Nell&#39;albero, fare doppio clic su **Dashboard**.
1. Clic **Nuovo dashboard**.
1. Digita il **Titolo** (ad esempio, My Dashboard) e **Nome**.
1. Fai clic su **Crea**.

### Clonazione Di Un Dashboard {#cloning-a-dashboard}

Potrebbe essere necessario disporre di più dashboard per visualizzare rapidamente le informazioni sul contenuto da diverse visualizzazioni. Per facilitare la creazione di un nuovo dashboard, AEM fornisce una funzione di duplicazione che è possibile utilizzare per duplicare un dashboard esistente. Per clonare un dashboard, procedere come segue:

1. In **Strumenti** , fare clic su **Console di configurazione**.

1. Nella struttura, fai clic su **Dashboard**.
1. Fare clic sul dashboard che si desidera clonare.

1. Clic **Clona**.

1. Digita il **Nome** della nuova dashboard.

### Rimozione Di Un Dashboard {#removing-a-dashboard}

1. In **Strumenti** , fare clic su **Console di configurazione**.

1. Nella struttura, fai clic su **Dashboard**.
1. Fai clic sul dashboard da eliminare.

1. Fai clic su **Rimuovi**.

1. Fai clic su **Sì** per confermare.

## Componenti del dashboard {#dashboard-components}

### Panoramica {#overview}

I componenti del dashboard non sono altro che normali [Componenti AEM](/help/sites-developing/developing-components-samples.md). Questa sezione descrive i componenti di reporting forniti con AEM.

### Componenti di reporting di Web Analytics {#web-analytics-reporting-components}

L’AEM viene fornito con un set di componenti che restituiscono più metriche delle [SiteCatalyst](/help/sites-administering/adobeanalytics.md) dati. Tali componenti sono elencati nel Sidekick sotto **Dashboard** sezione.

Ogni componente di reporting fornisce almeno tre schede:

* **Base**: contiene la configurazione principale.

* **Rapporto:** contiene la configurazione specifica di ciascun rapporto.
* **Stile**: contiene una configurazione di stile come dimensione e margine del grafico.

I componenti di reporting vengono inizializzati con una configurazione predefinita che consente di configurare rapidamente il dashboard.

#### Configurazione di base {#basic-configuration}

Il **Base** La scheda consente di accedere alle seguenti voci di configurazione:

**Titolo** Titolo visualizzato nel dashboard.

**Tipo di richiesta** Il modo in cui vengono richiesti i dati.

**Configurazione SiteCatalyst (opzionale)** Configurazione che si desidera utilizzare per connettersi al SiteCatalyst. Se non specificato, la configurazione viene considerata configurata nella pagina Dashboard (tramite le proprietà della pagina).

**ID suite di rapporti (facoltativo)** La suite di rapporti di SiteCatalyst che desideri utilizzare per generare il grafico.

#### Configurazione del rapporto {#report-configuration}

Per visualizzare le statistiche web, è necessario definire l’intervallo di date dei dati da recuperare. Il **Report** fornisce due campi per definire tale intervallo.

>[!NOTE]
>
>Impostando un intervallo di date ampio si può ridurre la reattività del dashboard.

**Data da** Data assoluta o relativa da cui vengono recuperati i dati.

**Data - A** Data assoluta o relativa di recupero dei dati.

Ogni componente definisce anche impostazioni specifiche.

#### Report tempo eccessivo {#overtime-report}

![chlimage_1-26](assets/chlimage_1-26a.png)

**Granularità data** Unità di tempo dell’asse X (ad esempio, giorno, ora).

**Metriche** L’elenco degli eventi che desideri visualizzare.

**Elementi** L’elenco degli elementi che suddividono i dati delle metriche nel grafico.

#### Report elenco classifica {#ranked-list-report}

![chlimage_1-27](assets/chlimage_1-27a.png)

**Elementi** L’elemento che suddivide i dati delle metriche nel grafico.

**Metriche** L’evento che desideri visualizzare.

**No. di elementi principali** Numero di elementi visualizzati dal rapporto.

#### Report classifica {#ranked-report}

![chlimage_1-28](assets/chlimage_1-28a.png)

**Metriche** L’evento che desideri visualizzare.

**Elementi** L’elemento che suddivide i dati delle metriche nel grafico.

#### Report sezione del sito principale {#top-site-section-report}

Questo componente visualizza un grafico che mostra la sezione più visitata di un sito web in base alla seguente configurazione.

![chlimage_1-29](assets/chlimage_1-29a.png)

**No. di elementi principali** Numero di sezioni visualizzate da nel rapporto.

#### Report con tendenze {#trended-report}

![chlimage_1-30](assets/chlimage_1-30a.png)

**Granularità data** Unità di tempo dell’asse X (ad esempio, giorno, ora).

**Metriche** L’evento che desideri visualizzare.

**Elementi** L’elemento che suddivide i dati delle metriche nel grafico.

## Estensione del dashboard {#extending-dashboard}

### Panoramica {#overview-1}

I dashboard sono pagine normali ( `cq:Page`), pertanto tutti i componenti possono essere utilizzati per assemblare le dashboard.

È presente un gruppo di componenti predefinito `Dashboard` contenente i componenti di reporting di analytics abilitati per impostazione predefinita sul modello.

### Creazione Di Un Modello Di Dashboard {#creating-a-dashboard-template}

Un modello definisce il contenuto predefinito di un nuovo dashboard. Puoi utilizzare diversi modelli per creare diversi tipi di dashboard.

I modelli di dashboard vengono creati come altri modelli di pagina, con la differenza che sono memorizzati in `/libs/cq/dashboards/templates/`. Consulta la [Creazione del modello Contentpage](/help/sites-developing/website.md#creating-the-contentpage-template) sezione.

>[!NOTE]
>
>I modelli di dashboard sono condivisi tra gli utenti.

### Sviluppo di un componente Dashboard {#developing-a-dashboard-component}

Lo sviluppo di un componente Dashboard consiste nella creazione di un componente AEM regolare. Questa sezione descrive un esempio di un componente che visualizza i primi 10 collaboratori.

![chlimage_1-31](assets/chlimage_1-31a.png)

I componenti Autore principali vengono memorizzati nell’archivio in `/apps/geometrixx-outdoors/components/reporting` ed è composto da:

1. a `jsp` file che legge i dati jcr e definisce `html` segnaposto.

1. una libreria lato client contenente una `js` file che recupera e ordina i dati, quindi compila `html` segnaposto.

![chlimage_1-32](assets/chlimage_1-32a.png)

Il seguente file JavaScript è definito nel `geout.reporting.topauthors` [Libreria client](/help/sites-developing/clientlibs.md) come elemento figlio del componente stesso.

Il [QueryBuilder](/help/sites-developing/querybuilder-api.md) viene utilizzato per eseguire una query sull’archivio da leggere `cq:AuditEvent` nodi. Il risultato della query è un oggetto JSON dal quale vengono estratti i contributi dell’autore.

#### top_authors.js {#top-authors-js}

```
$.ajax({
  url: "/bin/querybuilder.json",
  cache: false,
  data: {
       "orderby": "cq:time",
       "orderby.sort": "desc",
       "p.hits": "full",
       "p.limit": 100,
       "path": "/var/audit/com.day.cq.wcm.core.page/",
       "type": "cq:AuditEvent"
   },
  dataType: "json"
}).done(function( res ) {
    var authors = {};
    // from JSON to Object
    for(var r in res.hits) {
        var userId = res.hits[r].userId;
        if(userId == undefined) {
            continue;
        }
        var auth = authors[userId] || {userId : userId};
        auth.contrib = (auth.contrib || 0) +1;

        authors[userId] = auth;
    }

    // order by contribution
    var orderedByContrib = [];
    for(var a in authors) {
        orderedByContrib.push(authors[a]);
    }
    orderedByContrib.sort(function(a,b){return b.contrib - a.contrib});

    // produce the list
    for (var i=0, tot=orderedByContrib.length; i < tot; i++) {
        var current = orderedByContrib[i];
        $("<div> #" + (i + 1) +" "+ current.userId + " (" + current.contrib +" contrib.)</div>").appendTo("#authors-list");

    }
});
```

Il `JSP` include entrambi `global.jsp` e `clientlib`.

#### top_authors.jsp {#top-authors-jsp}

```java
<%@page session="false" contentType="text/html; charset=utf-8" %><%
%><%
%><%@include file="/libs/foundation/global.jsp" %><%
%>
<ui:includeClientLib categories="geout.reporting.topauthors" />
<%
String reportletTitle = properties.get("title", "Top Authors");
%>
<html>
     <h3><%=xssAPI.encodeForHTML(reportletTitle) %></h3>
     <div id="authors-list"></div>
</html>
```
