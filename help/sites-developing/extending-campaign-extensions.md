---
title: Creazione di estensioni personalizzate
description: Puoi richiamare il codice personalizzato in Adobe Campaign dall’AEM o dall’AEM ad Adobe Campaign.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 0702858e-5e46-451f-9ac3-40a4fec68ca0
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 2%

---

# Creazione di estensioni personalizzate{#creating-custom-extensions}

In genere, quando implementi un progetto, hai un codice personalizzato sia in AEM che in Adobe Campaign. Con l’utilizzo dell’API esistente, puoi richiamare il codice personalizzato in Adobe Campaign dall’AEM o dall’AEM ad Adobe Campaign. Questo documento descrive come farlo.

## Prerequisiti {#prerequisites}

Devi avere installato quanto segue:

* Adobe Experience Manager
* Adobe Campaign 6.1

Consulta [Integrazione dell’AEM con Adobe Campaign 6.1](/help/sites-administering/campaignonpremise.md) per ulteriori informazioni.

## Esempio 1: da AEM ad Adobe Campaign {#example-aem-to-adobe-campaign}

L’integrazione standard tra AEM e Campaign si basa su JSON e JSSP (JavaScript Server Page). Questi file JSSP si trovano nella console Campaign e iniziano tutti con **aec** (Adobe Experience Cloud)

![chlimage_1-15](assets/chlimage_1-15a.png)

>[!NOTE]
>
>[Per questo esempio, vedi Geometrixx](/help/sites-developing/we-retail.md), disponibile in Condivisione pacchetti.

In questo esempio, è stato creato un nuovo file JSSP personalizzato e lo chiama dal lato AEM per recuperare il risultato. Può essere utilizzato, ad esempio, per recuperare dati da Adobe Campaign o per salvarli in Adobe Campaign.

1. In Adobe Campaign, per creare un file JSSP, fai clic su **Nuovo** icona.

   ![L’icona Nuovo è indicata da una pagina con una stella nell’angolo in alto a sinistra.](do-not-localize/chlimage_1-4a.png)

1. Immetti il nome di questo file JSSP. In questo esempio, **cus:custom.jssp** viene utilizzato (nel senso che si trova nella **cus** namespace).

   ![chlimage_1-16](assets/chlimage_1-16a.png)

1. Inserisci il seguente codice nel file jssp:

   ```
   <%
   var origin = request.getParameter("origin");
   document.write("Hello from Adobe Campaign, origin : " + origin);
   %>
   ```

1. Salvare i dati. Il lavoro rimanente è svolto dall&#39;AEM.
1. Crea un semplice servlet sul lato AEM che puoi chiamare JSSP. In questo esempio, puoi assumere quanto segue:

   * È attiva la connessione tra AEM e Campaign
   * Il servizio cloud di Campaign è configurato su **/content/geometrixx-outdoors**

   L’oggetto più importante di questo esempio è **GenericCampaignConnector**, che consente di chiamare (ottenere e pubblicare) i file jssp sul lato Adobe Campaign.

   Ecco un piccolo frammento di codice:

   ```
   @Reference
   private GenericCampaignConnector campaignConnector;
   ...
   Map<String, String> params = new HashMap<String, String>();
   params.put("origin", "AEM");
   CallResults results = campaignConnector.callGeneric("/jssp/cus/custom.jssp", params, credentials);
   return results.bodyAsString();
   ```

1. In questo esempio, devi passare le credenziali nella chiamata di. Puoi ottenerli tramite il metodo getCredentials() in cui passi in una pagina in cui è configurato il servizio cloud Campaign.

   ```xml
   // page containing the cloudservice for Adobe Campaign
   Configuration config = campaignConnector.getWebserviceConfig(page.getContentResource().getParent());
   CampaignCredentials credentials = campaignConnector.retrieveCredentials(config);
   ```

Il codice completo è il seguente:

```java
import java.io.IOException;
import java.io.PrintWriter;
import java.util.HashMap;
import java.util.Map;

import javax.servlet.ServletException;

import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.sling.SlingServlet;
import org.apache.sling.api.SlingHttpServletRequest;
import org.apache.sling.api.SlingHttpServletResponse;
import org.apache.sling.api.servlets.SlingSafeMethodsServlet;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.day.cq.mcm.campaign.CallResults;
import com.day.cq.mcm.campaign.CampaignCredentials;
import com.day.cq.mcm.campaign.GenericCampaignConnector;
import com.day.cq.wcm.api.Page;
import com.day.cq.wcm.api.PageManager;
import com.day.cq.wcm.api.PageManagerFactory;
import com.day.cq.wcm.webservicesupport.Configuration;

@SlingServlet(paths="/bin/campaign", methods="GET")
public class CustomServlet extends SlingSafeMethodsServlet {

 private final Logger log = LoggerFactory.getLogger(this.getClass());

 @Reference
 private GenericCampaignConnector campaignConnector;

 @Reference
 private PageManagerFactory pageManagerFactory;

 @Override
 protected void doGet(SlingHttpServletRequest request,
   SlingHttpServletResponse response) throws ServletException,
   IOException {

  PageManager pm = pageManagerFactory.getPageManager(request.getResourceResolver());

  Page page = pm.getPage("/content/geometrixx-outdoors");

  String result = null;
  if ( page != null) {
   result = callCustomFunction(page);
  }
  if ( result != null ) {
   PrintWriter pw = response.getWriter();
   pw.print(result);
  }
 }

 private String callCustomFunction(Page page ) {
  try {
   Configuration config = campaignConnector.getWebserviceConfig(page.getContentResource().getParent());
   CampaignCredentials credentials = campaignConnector.retrieveCredentials(config);

   Map<String, String> params = new HashMap<String, String>();
   params.put("origin", "AEM");
   CallResults results = campaignConnector.callGeneric("/jssp/cus/custom.jssp", params, credentials);
   return results.bodyAsString();
  } catch (Exception e ) {
   log.error("Something went wrong during the connection", e);
  }
  return null;

 }

}
```

## Esempio 2: da Adobe Campaign a AEM {#example-adobe-campaign-to-aem}

AEM offre API pronte all’uso per recuperare gli oggetti disponibili in qualsiasi punto della vista di SiteAdmin Explorer.

![chlimage_1-17](assets/chlimage_1-17a.png)

>[!NOTE]
>
>[Per questo esempio, vedi Geometrixx](/help/sites-developing/we-retail.md), disponibile in Condivisione pacchetti.

Per ogni nodo dell’Explorer è presente un’API ad esso collegata. Ad esempio, per il nodo:

* [http://localhost:4502/siteadmin#/content/campaigns/geometrixx/scott-recommends](http://localhost:4502/siteadmin#/content/campaigns/geometrixx/scott-recommends)

L’API è:

* [http://localhost:4502/content/campaigns/geometrixx/scott-recommends.1.json](http://localhost:4502/content/campaigns/geometrixx/scott-recommends.2.json)

Fine dell’URL **.1.json** può essere sostituito da **.2.json**, **.3.json**, in base al numero di sottolivelli che sei interessato a ottenere. Per ottenere tutte le parole chiave, **infinito** può essere utilizzato:

* [http://localhost:4502/content/campaigns/geometrixx/scott-recommends.infinity.json](http://localhost:4502/content/campaigns/geometrixx/scott-recommends.2.json)

Per utilizzare l’API, l’AEM utilizza per impostazione predefinita l’autenticazione di base.

Una libreria JS denominata **amcIntegration.js** è disponibile in 6.1.1 (build 8624 e successive) che implementa tale logica tra diverse altre.

### Chiamata API AEM {#aem-api-call}

```java
loadLibrary("nms:amcIntegration.js");

var cmsAccountId = sqlGetInt("select iExtAccountId from NmsExtAccount where sName=$(sz)","aemInstance")
var cmsAccount = nms.extAccount.load(String(cmsAccountId));
var cmsServer = cmsAccount.server;

var request = new HttpClientRequest(cmsServer+"/content/campaigns/geometrixx.infinity.json")
aemAddBasicAuthentication(cmsAccount, request);
request.method = "GET"
request.header["Content-Type"] = "application/json; charset=UTF-8";
request.execute();
var response = request.response;
```
