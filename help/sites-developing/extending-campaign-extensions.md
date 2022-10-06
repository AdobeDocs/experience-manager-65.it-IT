---
title: Creazione di estensioni personalizzate
seo-title: Creating Custom Extensions
description: Puoi chiamare il tuo codice personalizzato in Adobe Campaign da AEM o da AEM ad Adobe Campaign
seo-description: You can call your custom code in Adobe Campaign from AEM or from AEM to Adobe Campaign
uuid: 8392aa0d-06cd-4b37-bb20-f67e6a0550b1
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: f536bcc1-7744-4f05-ac6a-4cec94a1ffb6
exl-id: 0702858e-5e46-451f-9ac3-40a4fec68ca0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 2%

---

# Creazione di estensioni personalizzate{#creating-custom-extensions}

In genere, quando implementi un progetto, il codice personalizzato è presente sia in AEM che in Adobe Campaign. Utilizzando l’API esistente, puoi chiamare il codice personalizzato in Adobe Campaign da AEM o da AEM ad Adobe Campaign. Questo documento descrive come farlo.

## Prerequisiti {#prerequisites}

Devi aver installato quanto segue:

* Adobe Experience Manager
* Adobe Campaign 6.1

Vedi [Integrazione di AEM con Adobe Campaign 6.1](/help/sites-administering/campaignonpremise.md) per ulteriori informazioni.

## Esempio 1: AEM ad Adobe Campaign {#example-aem-to-adobe-campaign}

L’integrazione standard tra AEM e Campaign è basata su JSON e JSSP (pagina server JavaScript). Questi file JSSP si trovano nella console Campaign e iniziano tutti con **amc** (Adobe Marketing Cloud).

![chlimage_1-15](assets/chlimage_1-15a.png)

>[!NOTE]
>
>[Per questo esempio, vedi Geometrixx](/help/sites-developing/we-retail.md), disponibile da Condivisione pacchetti.

In questo esempio, creiamo un nuovo file JSSP personalizzato e lo chiamiamo dal lato AEM per recuperare il risultato. Può essere utilizzato, ad esempio, per recuperare dati da Adobe Campaign o per salvare dati in Adobe Campaign.

1. In Adobe Campaign, per creare un nuovo file JSSP, fai clic sul pulsante **Nuovo** icona.

   ![](do-not-localize/chlimage_1-4a.png)

1. Immetti il nome del file JSSP. In questo esempio, utilizziamo **cus:custom.jssp** (cioè sarà nel **muco** namespace).

   ![chlimage_1-16](assets/chlimage_1-16a.png)

1. Inserisci il seguente codice nel file jssp:

   ```
   <%
   var origin = request.getParameter("origin");
   document.write("Hello from Adobe Campaign, origin : " + origin);
   %>
   ```

1. Salva il tuo lavoro. Il lavoro rimanente è in AEM.
1. Crea un semplice servlet sul lato AEM per chiamare questo JSSP. In questo esempio, si assume quanto segue:

   * La connessione funziona tra AEM e Campaign
   * Il servizio cloud della campagna è configurato in **/content/geometrixx-outdoors**

   L&#39;oggetto più importante in questo esempio è il **GenericCampaignConnector**, che ti consente di chiamare (get e pubblicare) file jssp sul lato Adobe Campaign.

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

1. Come vedi in questo esempio, devi immettere le credenziali nella chiamata . Puoi ottenerlo tramite il metodo getCredentials() , dove passi una pagina con il servizio cloud Campaign configurato.

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

## Esempio 2: Adobe Campaign per AEM {#example-adobe-campaign-to-aem}

AEM offre API predefinite per recuperare gli oggetti disponibili in qualsiasi punto della visualizzazione di siteadmin explorer.

![chlimage_1-17](assets/chlimage_1-17a.png)

>[!NOTE]
>
>[Per questo esempio, vedi Geometrixx](/help/sites-developing/we-retail.md), disponibile da Condivisione pacchetti.

Per ogni nodo nell&#39;explorer è presente un&#39;API collegata ad essa. Ad esempio per il nodo :

* [http://localhost:4502/siteadmin#/content/campaigns/geometrixx/scott-recommends](http://localhost:4502/siteadmin#/content/campaigns/geometrixx/scott-recommends)

l’API è:

* [http://localhost:4502/content/campaigns/geometrixx/scott-recommends.1.json](http://localhost:4502/content/campaigns/geometrixx/scott-recommends.2.json)

Fine dell’URL **.1.json** può essere sostituito da **.2.json**, **.3.json**, in base al numero di livelli secondari che si desidera ottenere Per ottenere tutti loro la parola chiave **infinito** possono essere utilizzati:

* [http://localhost:4502/content/campaigns/geometrixx/scott-recommends.infinity.json](http://localhost:4502/content/campaigns/geometrixx/scott-recommends.2.json)

Ora per utilizzare l’API è necessario sapere che AEM, per impostazione predefinita, utilizza l’autenticazione di base.

Una libreria JS denominata **amcIntegration.js** è disponibile nella versione 6.1.1 (build 8624 e versioni successive) che implementa tale logica tra diverse altre.

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
