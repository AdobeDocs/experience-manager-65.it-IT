---
title: Dashboard
description: Scopri come creare, configurare e sviluppare nuove dashboard per l’AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 5b934e3a-f554-46ec-a913-8d570abb1503
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 4%

---

# Dashboard{#dashboards}

Quando si utilizza l’AEM, è possibile gestire numerosi contenuti di tipi diversi (ad esempio pagine, risorse). I dashboard dell’AEM offrono un modo semplice e personalizzabile di definire le pagine che visualizzano i dati consolidati.

>[!NOTE]
>
>I dashboard di AEM vengono creati in base all’utente, in modo che un utente possa accedere solo al proprio dashboard.
>
>Tuttavia, è possibile utilizzare [modelli di dashboard](#creating-a-dashboard-template) per condividere la configurazione e il layout del dashboard comuni.

![chlimage_1-22](assets/chlimage_1-22.jpeg)

## Amministrazione delle dashboard {#administering-dashboards}

### Creazione Di Un Dashboard {#creating-a-dashboard}

1. Nella sezione **Strumenti** fare clic su **Console di configurazione**.
1. Nella struttura fare doppio clic su **Dashboard**.
1. Fai clic su **Nuovo dashboard**.
1. Digita il **Titolo** (ad esempio, Dashboard personale) e il **Nome**.
1. Fai clic su **Crea**.

### Clonazione Di Un Dashboard {#cloning-a-dashboard}

Potrebbe essere necessario disporre di più dashboard per visualizzare rapidamente le informazioni sul contenuto da diverse visualizzazioni. Per facilitare la creazione di un nuovo dashboard, AEM fornisce una funzione di duplicazione che è possibile utilizzare per duplicare un dashboard esistente. Per clonare un dashboard, procedere come segue:

1. Nella sezione **Strumenti** fare clic su **Console di configurazione**.

1. Nella struttura fare clic su **Dashboard**.
1. Fare clic sul dashboard che si desidera clonare.

1. Fare clic su **Clona**.

1. Digita il **Nome** del nuovo dashboard.

### Rimozione Di Un Dashboard {#removing-a-dashboard}

1. Nella sezione **Strumenti** fare clic su **Console di configurazione**.

1. Nella struttura fare clic su **Dashboard**.
1. Fai clic sul dashboard da eliminare.

1. Fai clic su **Rimuovi**.

1. Fai clic su **Sì** per confermare.

## Componenti del dashboard {#dashboard-components}

### Panoramica {#overview}

I componenti del dashboard non sono altro che [componenti AEM regolari](/help/sites-developing/developing-components-samples.md). Questa sezione descrive i componenti di reporting forniti con AEM.

### Componenti di reporting di Web Analytics {#web-analytics-reporting-components}

AEM viene fornito con un set di componenti che eseguono il rendering di più metriche dei dati del [SiteCatalyst](/help/sites-administering/adobeanalytics.md). Tali componenti sono elencati nel Sidekick nella sezione **Dashboard**.

Ogni componente di reporting fornisce almeno tre schede:

* **Base**: contiene la configurazione principale.

* **Report:** contiene la configurazione specifica di ogni report.
* **Stile**: contiene una configurazione di stile come dimensione e margine del grafico.

I componenti di reporting vengono inizializzati con una configurazione predefinita che consente di configurare rapidamente il dashboard.

#### Configurazione di base {#basic-configuration}

La scheda **Base** consente di accedere alle seguenti voci di configurazione:

**Titolo** Il titolo visualizzato nel dashboard.

**Tipo di richiesta** Modalità di richiesta dei dati.

**Configurazione SiteCatalyst (facoltativa)** Configurazione che si desidera utilizzare per connettersi al SiteCatalyst. Se non specificato, la configurazione viene considerata configurata nella pagina Dashboard (tramite le proprietà della pagina).

**ID suite di rapporti (facoltativo)** la suite di rapporti di SiteCatalyst che desideri utilizzare per generare il grafico.

#### Configurazione del rapporto {#report-configuration}

Per visualizzare le statistiche web, è necessario definire l’intervallo di date dei dati da recuperare. La scheda **Report** fornisce due campi per definire tale intervallo.

>[!NOTE]
>
>Impostando un intervallo di date ampio si può ridurre la reattività del dashboard.

**Data da** Data assoluta o relativa da cui vengono recuperati i dati.

**Data - A** Data assoluta o relativa di recupero dei dati.

Ogni componente definisce anche impostazioni specifiche.

#### Report tempo eccessivo {#overtime-report}

![chlimage_1-26](assets/chlimage_1-26a.png)

**Granularità data** Unità di tempo dell&#39;asse X (ad esempio, giorno, ora).

**Metriche** l&#39;elenco degli eventi da visualizzare.

**Elementi** L&#39;elenco di elementi che suddivide i dati delle metriche nel grafico.

#### Report elenco classifica {#ranked-list-report}

![chlimage_1-27](assets/chlimage_1-27a.png)

**Elementi** L&#39;elemento che suddivide i dati delle metriche nel grafico.

**Metriche** l&#39;evento che desideri visualizzare.

**No. di elementi principali** Numero di elementi visualizzati dal report.

#### Report classifica {#ranked-report}

![chlimage_1-28](assets/chlimage_1-28a.png)

**Metriche** l&#39;evento che desideri visualizzare.

**Elementi** L&#39;elemento che suddivide i dati delle metriche nel grafico.

#### Report sezione del sito principale {#top-site-section-report}

Questo componente visualizza un grafico che mostra la sezione più visitata di un sito web in base alla seguente configurazione.

![chlimage_1-29](assets/chlimage_1-29a.png)

**No. di elementi principali** Numero di sezioni visualizzate da nel report.

#### Report con tendenze {#trended-report}

![chlimage_1-30](assets/chlimage_1-30a.png)

**Granularità data** Unità di tempo dell&#39;asse X (ad esempio, giorno, ora).

**Metriche** l&#39;evento che desideri visualizzare.

**Elementi** L&#39;elemento che suddivide i dati delle metriche nel grafico.

## Estensione del dashboard {#extending-dashboard}

### Panoramica {#overview-1}

I dashboard sono pagine normali ( `cq:Page`), pertanto tutti i componenti possono essere utilizzati per assemblare i dashboard.

Esiste un gruppo di componenti predefinito `Dashboard` contenente componenti di reporting di Analytics abilitati per impostazione predefinita nel modello.

### Creazione Di Un Modello Di Dashboard {#creating-a-dashboard-template}

Un modello definisce il contenuto predefinito di un nuovo dashboard. Puoi utilizzare diversi modelli per creare diversi tipi di dashboard.

I modelli del dashboard vengono creati come gli altri modelli di pagina, tranne per il fatto che sono memorizzati in `/libs/cq/dashboards/templates/`. Consulta la sezione [Creazione del modello Contentpage](/help/sites-developing/website.md#creating-the-contentpage-template).

>[!NOTE]
>
>I modelli di dashboard sono condivisi tra gli utenti.

### Sviluppo di un componente Dashboard {#developing-a-dashboard-component}

Lo sviluppo di un componente Dashboard consiste nella creazione di un componente AEM regolare. Questa sezione descrive un esempio di un componente che visualizza i primi 10 collaboratori.

![chlimage_1-31](assets/chlimage_1-31a.png)

I componenti Autore principali sono archiviati nell&#39;archivio in `/apps/geometrixx-outdoors/components/reporting` e sono composti da:

1. un file `jsp` che legge i dati jcr e definisce il segnaposto `html`.

1. una libreria lato client contenente un file `js` che recupera e ordina i dati, quindi compila il segnaposto `html`.

![chlimage_1-32](assets/chlimage_1-32a.png)

Il seguente file JavaScript è definito nella `geout.reporting.topauthors` [Libreria client](/help/sites-developing/clientlibs.md) come elemento figlio del componente stesso.

[QueryBuilder](/help/sites-developing/querybuilder-api.md) viene utilizzato per eseguire query nell&#39;archivio per leggere `cq:AuditEvent` nodi. Il risultato della query è un oggetto JSON dal quale vengono estratti i contributi dell’autore.

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

`JSP` include sia `global.jsp` che `clientlib`.

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
