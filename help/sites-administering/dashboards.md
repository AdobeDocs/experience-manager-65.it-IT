---
title: Dashboard
seo-title: Dashboard
description: Scopri come creare, configurare e sviluppare nuove dashboard AEM.
seo-description: Scopri come creare, configurare e sviluppare nuove dashboard AEM.
uuid: 3eadbba2-0ce1-41be-a9f8-e6cafa109893
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 40560e06-2508-45a4-a648-39629ed54f28
translation-type: tm+mt
source-git-commit: 69dfd6b41b32cb9131fd90fd7039a0c224889db5

---


# Dashboard{#dashboards}

Con AEM è possibile gestire numerosi contenuti di tipo diverso (ad esempio pagine e contenuti). AEM Dashboard offre un metodo facile e personalizzabile per definire le pagine in cui sono visualizzati dati consolidati.

>[!NOTE]
>
>I dashboard di AEM vengono creati a livello di utente e ogni utente può quindi accedere solo al proprio dashboard.
>
>However, [Dashboard templates](#creating-a-dashboard-template) can be used to share common configuration and Dashboard layout.

![chlimage_1-22](assets/chlimage_1-22.jpeg)

## Amministrazione dei dashboard {#administering-dashboards}

### Creazione di un dashboard {#creating-a-dashboard}

Per creare un nuovo dashboard, effettuate le seguenti operazioni:

1. Nella sezione **Strumenti**, fate clic su **Console di configurazione**.
1. In the tree, Double-Click **Dashboard**.
1. Fate clic su **Dashboard**.
1. Digitate il **Titolo** (ad esempio Mio dashboard) e **Nome**.
1. Fate clic su **Crea**. 

### Clonazione di un dashboard {#cloning-a-dashboard}

Può essere utile disporre di più dashboard per vedere rapidamente le informazioni sui contenuti sotto forma diversa. Per facilitare la creazione di nuovi dashboard, AEM consente di clonare, o duplicare, un dashboard esistente. Per clonare un dashboard, effettuate le seguenti operazioni:

1. Nella sezione **Strumenti**, fate clic su **Console di configurazione**.

1. Nella struttura ad albero, fate clic su **Dashboard**.
1. Fate clic sul dashboard da clonare.

1. Fate clic su **Clona**.

1. Digitate il **Nome** del nuovo dashboard.

### Rimozione di un dashboard {#removing-a-dashboard}

1. Nella sezione **Strumenti**, fate clic su **Console di configurazione**.

1. Nella struttura ad albero, fate clic su **Dashboard**.
1. Fate clic sul dashboard da eliminare.

1. Fate clic su **Rimuovi**.

1. Fate clic su **Sì** per confermare.

## Componenti per dashboard {#dashboard-components}

### Panoramica {#overview}

I componenti dashboard non sono altro che normali componenti [](/help/sites-developing/developing-components-samples.md)AEM. Questa sezione descrive i componenti per report forniti con AEM.

### Componenti per report per analisi Web {#web-analytics-reporting-components}

AEM viene fornito con un set di componenti che eseguono il rendering di più metriche dei dati [SiteCatalyst](/help/sites-administering/adobeanalytics.md) . Tali componenti sono elencati nella barra laterale sotto la sezione **Dashboard**.

Ciascun componente per report dispone di almeno tre schede:

* **Base**: contiene la configurazione principale.

* **Report:** contiene la configurazione specifica di ciascun report.
* **Stile**: contiene la configurazione di stile, come dimensione del grafico e margini.

I componenti per report vengono inizializzati con una configurazione predefinita che consente di impostare rapidamente il dashboard.

#### Configurazione di base {#basic-configuration}

La scheda **Base** permette di accedere alle seguenti voci di configurazione:

**Titolo** Titolo visualizzato sul dashboard.

**Tipo** di richiesta Modalità di richiesta dei dati.

**Configurazione SiteCatalyst (facoltativo)** Configurazione da usare per la connessione a SiteCatalyst. Se non viene fornita, viene considerata la configurazione sulla pagina Dashboard (tramite le proprietà pagina).

**ID suite di rapporti (facoltativo)** La suite di rapporti SiteCatalyst da usare per generare il grafico.

#### Configurazione del report {#report-configuration}

Per visualizzare le statistiche Web, occorre definire l’intervallo di date che interessano. La scheda **Report** contiene due campi con cui definire tale intervallo.

>[!NOTE]
>
>Se si imposta un intervallo di date ampio, il dashboard potrebbe risultare lento.

**Data Da** data assoluta o relativa dalla quale vengono estratti i dati.

**Data A** data assoluta o relativa alla quale vengono estratti i dati.

Per ciascun componente vengono inoltre definite specifiche impostazioni.

#### Report tempo eccessivo {#overtime-report}

![chlimage_1-26](assets/chlimage_1-26a.png)

**Granularità** data Unità di tempo dell’asse X (ad esempio giorno, ora).

**Metriche** L&#39;elenco degli eventi da visualizzare.

**Elementi** L’elenco degli elementi che compongono i dati delle metriche nel grafico.

#### Report elenco classifica {#ranked-list-report}

![chlimage_1-27](assets/chlimage_1-27a.png)

**Elementi** L’elemento che compone i dati delle metriche nel grafico.

**Metriche** L’evento da visualizzare.

**No. degli elementi** principali Numero di elementi visualizzati dal rapporto.

#### Report classifica {#ranked-report}

![chlimage_1-28](assets/chlimage_1-28a.png)

**Metriche** L’evento da visualizzare.

**Elementi** L’elemento che compone i dati delle metriche nel grafico.

#### Report sezione del sito principale {#top-site-section-report}

Questo componente visualizza un grafico che illustra la sezione più visitata del sito Web in base alla seguente configurazione.

![chlimage_1-29](assets/chlimage_1-29a.png)

**No. degli elementi** principali Numero di sezioni visualizzate dal report.

#### Report con tendenze {#trended-report}

![chlimage_1-30](assets/chlimage_1-30a.png)

**Granularità** data Unità di tempo dell’asse X (ad esempio giorno, ora).

**Metriche** L’evento da visualizzare.

**Elementi** L’elemento che compone i dati delle metriche nel grafico.

## Estensione del dashboard {#extending-dashboard}

### Panoramica {#overview-1}

I dashboard sono normali pagine (`cq:Page`) e possono quindi essere assemblati con qualsiasi componente.

There is a default component group `Dashboard` containing analytics reporting components which are enabled on the template by default.

### Creazione di un modello di dashboard {#creating-a-dashboard-template}

Con un modello si definisce il contenuto predefinito di un nuovo dashboard. È possibile disporre di più modelli, con cui creare diversi tipi di dashboard.

Dashboard templates are created like other page templates, except that they are stored under `/libs/cq/dashboards/templates/`. Consultate la sezione [Creazione di un modello](/help/sites-developing/website.md#creating-the-contentpage-template) per pagina di contenuto.

>[!NOTE]
>
>I modelli di dashboard possono essere condivisi tra più utenti.

### Sviluppo di un componente dashboard {#developing-a-dashboard-component}

Lo sviluppo di un componente dashboard consiste nella creazione di un normale componente AEM. In questa sezione viene descritto un esempio di componente per visualizzare i primi 10 utenti collaboratori.

![chlimage_1-31](assets/chlimage_1-31a.png)

The top author components is stored in the repository at `/apps/geometrixx-outdoors/components/reporting` and is composed of :

1. un file `jsp` che legge i dati jcr e definisce il segnaposto `html`;

1. una libreria lato client contenente un file `js` che raccoglie e ordina i dati, quindi compila il segnaposto `html`.

![chlimage_1-32](assets/chlimage_1-32a.png)

Il seguente file Javascript è definito nella libreria `geout.reporting.topauthors` [](/help/sites-developing/clientlibs.md) client come figlio del componente stesso.

QueryBuilder [viene utilizzato per eseguire query nell&#39;archivio per leggere](/help/sites-developing/querybuilder-api.md) `cq:AuditEvent` i nodi. Il risultato della query genera un oggetto JSON dal quale vengono estratti i contributi degli autori.

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

L&#39; `JSP` opzione include sia `global.jsp` che `clientlib`.

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

