---
title: Compilazione dinamica di elenchi a discesa
seo-title: Dynamically populating drop-down lists
description: Procedura per compilare dinamicamente gli elenchi a discesa in base ad alcune logiche
seo-description: Procedure to dynamically populate drop-down lists based on some logic
uuid: b3408aee-ac24-43af-a380-a5892abf0248
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: ad6db3fd-0d26-4241-bf73-be74b7f6e509
docset: aem65
exl-id: 64b88423-aaae-4258-bf48-73df5c9353ea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---

# Compilazione dinamica di elenchi a discesa {#dynamically-populating-drop-down-lists}

## Prerequisiti {#prerequisites}

* [Creazione di bundle OSGI](https://helpx.adobe.com/experience-manager/using/creating-osgi-bundles-digital-marketing.html)
* [Sviluppo di componenti AEM](/help/sites-developing/components.md)
* [Creazione di un modulo adattivo](../../forms/using/creating-adaptive-form.md)
* [Creazione di moduli adattivi](../../forms/using/introduction-forms-authoring.md)

## Procedura per la compilazione dinamica degli elenchi a discesa {#procedure-to-dynamically-populate-drop-down-lists}

Considera uno scenario in cui desideri compilare il **Stato** elenco a discesa basato su un valore selezionato nella **Paese** elenco a discesa. Se si seleziona Australia nel **Paese** elenco a discesa, **Stato** nell’elenco a discesa vengono visualizzati gli stati in Australia. La procedura seguente descrive come eseguire questa attività.

1. Crea un progetto con i seguenti moduli:

   * Il bundle che contiene la logica per compilare il menu a discesa, che in questo caso è un servlet.
   * Il contenuto, che incorpora il file .jar e dispone di una risorsa a discesa. Il servlet punta a questa risorsa.

1. Scrivere un servlet basato sul parametro di richiesta Country, che restituisce un array contenente i nomi degli stati all&#39;interno del paese.

   ```java
   @Component(metatype = false)
   @Service(value = Servlet.class)
   @Properties({
           @Property(name = "sling.servlet.resourceTypes", value = "/apps/populatedropdown"),
           @Property(name = "sling.servlet.methods", value = {"GET", "POST"}),
           @Property(name = "service.description", value = "Populate states dropdown based on country value")
   })
   public class DropDownPopulator extends SlingAllMethodsServlet {
       private Logger logger = LoggerFactory.getLogger(DropDownPopulator.class);
   
       protected void doPost(SlingHttpServletRequest request,
                             final SlingHttpServletResponse response)
               throws ServletException, IOException {
           response.setHeader("Access-Control-Allow-Origin", "*");
           response.setContentType("application/json");
           response.setCharacterEncoding("UTF-8");
           try {
               String US_STATES[] = {"0=Alabama",
                       "1=Alaska",
                       "2=Arizona",
                       "3=Arkansas",
                       "4=California",
                       "5=Colorado",
                       "6=Connecticut",
                       "7=Delaware",
                       "8=Florida",
                       "9=Georgia",
                       "10=Hawaii",
                       "11=Idaho",
                       "12=Illinois",
                       "13=Indiana",
                       "14=Iowa",
                       "15=Kansas",
                       "16=Kentucky",
                       "17=Louisiana",
                       "18=Maine",
                       "19=Maryland",
                       "20=Massachusetts",
                       "21=Michigan",
                       "22=Minnesota",
                       "23=Mississippi",
                       "24=Missouri",
                       "25=Montana",
                       "26=Nebraska",
                       "27=Nevada",
                       "28=New Hampshire",
                       "29=New Jersey",
                       "30=New Mexico",
                       "31=New York",
                       "32=North Carolina",
                       "33=North Dakota",
                       "34=Ohio",
                       "35=Oklahoma",
                       "36=Oregon",
                       "37=Pennsylvania",
                       "38=Rhode Island",
                       "39=South Carolina",
                       "40=South Dakota",
                       "41=Tennessee",
                       "42=Texas",
                       "43=Utah",
                       "44=Vermont",
                       "45=Virginia",
                       "46=Washington",
                       "47=West Virginia",
                       "48=Wisconsin",
                       "49=Wyoming"};
               String AUSTRALIAN_STATES[] = {"0=Ashmore and Cartier Islands",
                       "1=Australian Antarctic Territory",
                       "2=Australian Capital Territory",
                       "3=Christmas Island",
                       "4=Cocos (Keeling) Islands",
                       "5=Coral Sea Islands",
                       "6=Heard Island and McDonald Islands",
                       "7=Jervis Bay Territory",
                       "8=New South Wales",
                       "9=Norfolk Island",
                       "10=Northern Territory",
                       "11=Queensland",
                       "12=South Australia",
                       "13=Tasmania",
                       "14=Victoria",
                       "15=Western Australia"};
               String country = request.getParameter("country");
               JSONArray stateJsonArray = new JSONArray();
               if (country.length() > 0) {
                   if ("australia".equalsIgnoreCase(country)) {
                       stateJsonArray = new JSONArray();
                       for (String state : AUSTRALIAN_STATES) {
                           stateJsonArray.put(state);
                       }
                   } else if ("unitedstates".equalsIgnoreCase(country)) {
                       stateJsonArray = new JSONArray();
                       for (String state : US_STATES) {
                           stateJsonArray.put(state);
                       }
                   }
                   response.setContentType("application/json");
                   response.getWriter().write(stateJsonArray.toString());
               }
   
           } catch ( Exception e) {
               logger.error(e.getMessage(), e);
           }
       }
   }
   ```

1. Crea un nodo a discesa sotto una particolare gerarchia di cartelle nelle app (per esempio, crea un nodo sotto /apps/myfolder/demo). Assicurati che `sling:resourceType` Il parametro per il nodo è lo stesso a cui il servlet punta (/apps/popolatedropdown).

   ![Creare un nodo a discesa](assets/dropdown-node.png)

1. Crea un pacchetto con il nodo del contenuto e incorpora il file .jar in una posizione particolare (ad esempio /apps/myfolder/demo/install/). Distribuisci lo stesso file sul server.
1. Crea un modulo adattivo e aggiungi due elenchi a discesa, Paese e Stato . L&#39;elenco Paese può includere i nomi dei paesi. L’elenco Stato può comporre in modo dinamico i nomi degli stati per il paese selezionato nel primo elenco.

   Aggiungere i nomi dei paesi da visualizzare nell&#39;elenco Paese. Nell’elenco Stato, aggiungere uno script per compilarlo in base al nome del paese nell’elenco Paese.

   ![Aggiunta di nomi di paese](assets/country-dropdown.png) ![Aggiunta di script per la compilazione dei nomi degli stati](assets/state-dropdown.png) ![Elenco a discesa Paese e Stato](assets/2dropdowns.png)

   ```javascript
   JSON.parse(
       $.ajax({
           url: "/apps/myfolder/demo/dropdown",
           type: "POST",
           async: false,
           data: {"country": country.value},
            success: function(res){},
            error : function (message) {
                 guideBridge._guide.logger().log(message);
                 successFlag = false;
                 }
              })
   .responseText);
   ```

Il pacchetto Contenuto che contiene un esempio di modulo adattivo (demo/AFdemo) con il codice implementato sopra.

[Ottieni file](assets/dropdown-demo-content-1.0.1-snapshot.zip)
