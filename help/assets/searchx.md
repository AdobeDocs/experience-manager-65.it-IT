---
title: Estende la funzionalità di ricerca.
description: Estendete le funzionalità di ricerca di  [!DNL Adobe Experience Manager Assets] oltre i valori predefiniti.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 19%

---


# Estendi ricerca risorse {#extending-assets-search}

È possibile estendere le funzionalità di ricerca [!DNL Adobe Experience Manager Assets]. [!DNL Experience Manager Assets] consente di cercare le risorse in base alle stringhe.

La ricerca viene eseguita tramite l&#39;interfaccia QueryBuilder, in modo da personalizzare la ricerca con diversi predicati. Potete sovrapporre il set predefinito di predicati nella seguente directory: `/apps/dam/content/search/searchpanel/facets`.

Potete anche aggiungere ulteriori schede al pannello di amministrazione [!DNL Assets].

>[!CAUTION]
>
>A partire da [!DNL Experience Manager] 6.4, l&#39;interfaccia classica è obsoleta. Per l&#39;annuncio, vedere [funzioni obsolete e rimosse](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/deprecated-removed-features.html).  Adobe consiglia di utilizzare l&#39;interfaccia touch. Per la personalizzazione, vedere [facet di ricerca](/help/assets/search-facets.md).

## Sovrapposizione {#overlaying}

Per sovrapporre i predicati preconfigurati, copiate il nodo `facets` da `/libs/dam/content/search/searchpanel` a `/apps/dam/content/search/searchpanel/` o specificate un&#39;altra proprietà `facetURL` nella configurazione `searchpanel` (l&#39;impostazione predefinita è `/libs/dam/content/search/searchpanel/facets.overlay.infinity.json`).

![screen_shot_2012-06-05at113619am](assets/screen_shot_2012-06-05at113619am.png)

>[!NOTE]
>
>Per impostazione predefinita, la struttura di directory in `/apps` non esiste, pertanto creala. Assicurarsi che i tipi di nodo corrispondano a quelli in `/libs`.

## Aggiungi schede {#adding-tabs}

È possibile aggiungere ulteriori schede di ricerca configurandole nell&#39;interfaccia di amministrazione [!DNL Assets]. Per creare schede aggiuntive:

1. Create la struttura di cartelle `/apps/wcm/core/content/damadmin/tabs,`se non esiste già, quindi copiate il nodo `tabs` da `/libs/wcm/core/content/damadmin` e incollatelo.
1. Create e configurate la seconda scheda, come desiderato.

   >[!NOTE]
   >
   >Quando si crea una seconda `siteadminsearchpanel`, assicurarsi di impostare una proprietà `id` per evitare conflitti tra i moduli.

## Creare predicati personalizzati {#creating-custom-predicates}

[!DNL Assets] viene fornito con un set di predicati predefiniti che possono essere utilizzati per personalizzare una pagina Condivisione risorse. La personalizzazione di una condivisione di risorse in questo modo è descritta in [creazione e configurazione di una pagina di condivisione di risorse](/help/assets/assets-finder-editor.md#creating-and-configuring-an-asset-share-page).

Oltre a utilizzare i predicati preesistenti, [!DNL Experience Manager] gli sviluppatori possono anche creare i propri predicati utilizzando l&#39;API [Query Builder](/help/sites-developing/querybuilder-api.md).

La creazione di predicati personalizzati richiede conoscenze di base sul [framework dei widget](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html).

La procedura ottimale consiste nel copiare e regolare un predicato esistente. I predicati di esempio si trovano in **/libs/cq/search/components/predicates**.

### Esempio: Creare un predicato di proprietà semplice {#example-build-a-simple-property-predicate}

Per creare un predicato di proprietà:

1. Create una cartella di componenti nella directory dei progetti, ad esempio **/apps/geometrixx/components/titlepredicate**.
1. Aggiungi **content.xml**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Title Predicate"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. Aggiungi `titlepredicate.jsp`.

   ```java
   <%--
   
     Sample title predicate component
   
   --%><%@ page import="java.util.Calendar" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       // A unique id is necessary in case this predicate is inserted multiple times on the same page
       String elemId = "cq-predicate-" +  Long.toString(Calendar.getInstance().getTimeInMillis());
   
   %><div class="predicatebox">
   
       <div class="title">Title</div>
   
       <%-- The wrapper for the form elements. All items will be append to this wrapper. --%>
       <div id="<%= elemId %>" class="content"></div>
   
   </div><script type="text/javascript">
   
       CQ.Ext.onLoad(function() {
   
           var predicateName = "property";
           var propertyName = "jcr:content/metadata/dc:title";
           var elemId = "<%= elemId %>";
   
           // Get the page wide available QueryBuilder.
           var qb = CQ.search.Util.getQueryBuilder();
   
           // createId adds a counter to the predicate name - useful in case this predicate
           // is inserted multiple times on the same page.
           var id = qb.createId(predicateName);
   
           // Hidden field that defines the property to search for; in our case this
           // is the "dc:title" metadata. The name "property" (or "1_property", "2_property" etc.)
           // indicates the server to use the property predicate
           // (com.day.cq.search.eval.JcrPropertyPredicateEvaluator).
           qb.addField({
               "xtype": "hidden",
               "renderTo": elemId,
               "name": id,
               "value": propertyName
           });
   
           // The visible text field. The name has to be like the one of the hidden field above
           // plus the ".value" suffix.
           qb.addField({
               "xtype": "textfield",
               "renderTo": elemId,
               "name": id + ".value"
           });
   
           // Depending on the predicate additional parameters allow to configure the
           // predicate. Here we add an operation parameter to create a "like" query.
           // Again note the name set to the id and a suffix.
           qb.addField({
               "xtype": "hidden",
               "renderTo": elemId,
               "name": id + ".operation",
               "value": "like"
           });
       });
   </script>
   ```

1. Per rendere disponibile il componente, devi essere in grado di modificarlo. Per rendere modificabile un componente, in CRXDE aggiungi un nodo **cq:editConfig** di tipo principale **cq:EditConfig**. Per rimuovere i paragrafi, aggiungi una proprietà con più valori **cq:actions** che presenta un singolo valore **DELETE**.
1. Passate al browser e nella pagina di esempio (ad esempio, **press.html**) passate alla modalità di progettazione e abilitate il nuovo componente per il sistema paragrafo predicato (ad esempio, **left**).

1. In modalità **Edit**, il nuovo componente è ora disponibile nella barra laterale (nel gruppo **Search**). Inserite il componente nella colonna **Predicati** e digitate una parola di ricerca, ad esempio **Diamond**, quindi fate clic sulla lente di ingrandimento per avviare la ricerca.

   >[!NOTE]
   >
   >Durante la ricerca, accertarsi di digitare esattamente il termine, compreso il caso corretto.

### Esempio: Creare un predicato di gruppo semplice {#example-build-a-simple-group-predicate}

Per creare un predicato di gruppo:

1. Create una cartella di componenti nella directory dei progetti, ad esempio **/apps/geometrixx/components/picspredicate.**
1. Aggiungi **content.xml**:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Formats"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. Aggiungi **titlepredicate.jsp**:

   ```java
   <%--
   
     Sample group predicate component
   
   --%><%@ page import="java.util.Calendar" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       // A unique id is necessary in case this predicate is inserted multiple times on the same page.
       String elemId = "cq-predicate-" +  Long.toString(Calendar.getInstance().getTimeInMillis());
   
   %><div class="predicatebox">
   
       <div class="title">Image Formats</div>
   
       <%-- The wrapper for the form elements. All items will be append to this wrapper. --%>
       <div id="<%= elemId %>" class="content"></div>
   
   </div><script type="text/javascript">
   
       CQ.Ext.onLoad(function() {
   
           var predicateName = "property";
           var propertyName = "jcr:content/metadata/dc:format";
           var elemId = "<%= elemId %>";
   
           // Get the page wide available QueryBuilder.
           var qb = CQ.search.Util.getQueryBuilder();
   
           // Create a unique group ID; will return e.g. "1_group".
           var groupId = qb.createGroupId();
   
           // Hidden field that defines the property to search for  - in our case "dc:format" -
           // and declares the group of predicates. "property" in the name ("1_group.property")
           // indicates to the server to use the "property predicate"
           // (com.day.cq.search.eval.JcrPropertyPredicateEvaluator).
           qb.addField({
               "xtype": "hidden",
               "renderTo": "<%= elemId %>",
               "name": groupId + "." + predicateName, // 1_group.property
               "value": propertyName
           });
   
           // Declare to combine the multiple values using OR.
           qb.add(new CQ.Ext.form.Hidden({
               "name": groupId + ".p.or",  // 1_group.p.or
               "value": "true"
           }));
   
           // The options
           var options = [
               { "label":"JPEG", "value":"image/jpeg"},
               { "label":"PNG",  "value":"image/png" },
               { "label":"GIF",  "value":"image/gif" }
           ];
   
           // Build a checkbox for each option.
           for (var i = 0; i < options.length; i++) {
               qb.addField({
                   "xtype": "checkbox",
                   "renderTo": "<%= elemId %>",
                   // 1_group.property.0_value, 1_group.property.1_value etc.
                   "name": groupId + "." +  predicateName + "." + i + "_value",
                   "inputValue": options[i].value,
                   "boxLabel": options[i].label,
                   "listeners": {
                       "check": function() {
                           // Submit the search form when checking/unchecking a checkbox.
                           qb.submit();
                       }
                   }
               });
           }
       });
   ```

1. Per rendere disponibile il componente, devi essere in grado di modificarlo. Per rendere modificabile un componente, in CRXDE aggiungi un nodo **cq:editConfig** di tipo principale **cq:EditConfig**. Per rimuovere i paragrafi, aggiungi una proprietà con più valori **cq:actions** che presenta un singolo valore **DELETE**.
1. Passate al browser e nella pagina di esempio (ad esempio, **press.html**) passate alla modalità di progettazione e abilitate il nuovo componente per il sistema paragrafo predicato (ad esempio, **left**).
1. In modalità **Edit**, il nuovo componente è ora disponibile nella barra laterale (nel gruppo **Search**). Inserire il componente nella colonna **Predicati**.

## Widget predicato installati {#installed-predicate-widgets}

I seguenti predicati sono disponibili come widget ExtJS preconfigurati.

### FulltextPredicate {#fulltextpredicate}

| Proprietà | Tipo | Descrizione |
|---|---|---|
| predicateName | Stringa | Nome del predicato. Impostazione predefinita `fulltext` |
| searchCallback | Funzione | Callback per attivare la ricerca sull&#39;evento `keyup`. Impostazione predefinita `CQ.wcm.SiteAdmin.doSearch` |

### PropertyPredicate {#propertypredicate}

| Proprietà | Tipo | Descrizione |
|---|---|---|
| predicateName | Stringa | Nome del predicato. Impostazione predefinita `property` |
| propertyName | Stringa | Nome della proprietà JCR. Impostazione predefinita `jcr:title` |
| defaultValue | Stringa | Valore predefinito precompilato. |

### PathPredicate {#pathpredicate}

| Proprietà | Tipo | Descrizione |
|---|---|---|
| predicateName | Stringa | Nome del predicato. Impostazione predefinita `path` |
| rootPath | Stringa | Percorso principale del predicato. Impostazione predefinita `/content/dam` |
| pathFieldPredicateName | Stringa | Impostazione predefinita `folder` |
| showFlatOption | Booleano | Flag per visualizzare la casella di controllo `search in subfolders`. Valori predefiniti per true. |

### DatePredicate {#datepredicate}

| Proprietà | Tipo | Descrizione |
|---|---|---|
| predicateName | Stringa | Nome del predicato. Impostazione predefinita `daterange` |
| propertyName | Stringa | Nome della proprietà JCR. Impostazione predefinita `jcr:content/jcr:lastModified` |
| defaultValue | Stringa | Valore predefinito precompilato |

### OptionsPredicate {#optionspredicate}

| Proprietà | Tipo | Descrizione |
|---|---|---|
| titolo | Stringa | Aggiunge un altro titolo superiore |
| predicateName | Stringa | Nome del predicato. Impostazione predefinita `daterange` |
| propertyName | Stringa | Nome della proprietà JCR. Impostazione predefinita `jcr:content/metadata/cq:tags` |
| collassare | Stringa | Comprimi livello. Impostazione predefinita `level1` |
| triggerSearch | Booleano | Flag per l’attivazione della ricerca al momento della verifica. Il valore predefinito è false |
| searchCallback | Funzione | Callback per attivare la ricerca. Impostazione predefinita `CQ.wcm.SiteAdmin.doSearch` |
| searchTimeoutTime | Numero | Timeout prima che searchCallback venga attivato. Il valore predefinito è 800 ms |

## Personalizzare i risultati della ricerca {#customizing-search-results}

La presentazione dei risultati della ricerca in una pagina Condivisione risorse è regolata dall’obiettivo selezionato. [!DNL Experience Manager Assets] viene fornito con una serie di obiettivi predefiniti che possono essere utilizzati per personalizzare una pagina Condivisione risorse. La personalizzazione di una condivisione di risorse in questo modo è descritta in [Creazione e configurazione di una pagina di condivisione di risorse](/help/assets/assets-finder-editor.md#creating-and-configuring-an-asset-share-page).

Oltre a utilizzare ottiche preesistenti, gli sviluppatori [!DNL Experience Manager] possono anche creare ottiche proprie.
