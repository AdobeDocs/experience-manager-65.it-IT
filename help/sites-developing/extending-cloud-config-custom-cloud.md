---
title: Creazione di un Cloud Service personalizzato
seo-title: Creating a Custom Cloud Service
description: Il set predefinito di Cloud Services può essere esteso con tipi di Cloud Service personalizzati
seo-description: The default set of Cloud Services can be extended with custom Cloud Service types
uuid: b105a0c1-b68c-4f57-8e3b-561c8051a08e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e48e87c6-43ca-45ba-bd6b-d74c969757cd
exl-id: 9414c77a-b180-4440-8386-e6eb4426e475
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 15%

---

# Creazione di un Cloud Service personalizzato{#creating-a-custom-cloud-service}

Il set di Cloud Services predefinito può essere esteso con tipi di Cloud Service personalizzati. Ciò ti consente di inserire markup personalizzati nella pagina in modo strutturato. Questo verrà utilizzato principalmente per provider di analisi di terze parti, ad esempio Google Analytics, Chartbeat, ecc. I Cloud Services vengono ereditati dalle pagine padre alle pagine figlie, con la possibilità di interrompere l’ereditarietà a qualsiasi livello.

>[!NOTE]
>
>Questa guida dettagliata per la creazione di un nuovo Cloud Service è un esempio che utilizza Google Analytics. Tutto potrebbe non essere applicabile al tuo caso d’uso.

1. In CRXDE Lite, crea un nuovo nodo sotto `/apps`:

   * **Nome**: `acs`
   * **Tipo**: `nt:folder`

1. Crea un nuovo nodo sotto `/apps/acs`:

   * **Nome**: `analytics`
   * **Tipo**: `sling:Folder`

1. Crea 2 nuovi nodi sotto `/apps/acs/analytics`:

   * **Nome**: componenti
   * **Tipo**: `sling:Folder`

   e

   * **Nome**: modelli
   * **Tipo**: `sling:Folder`


1. Fai clic con il pulsante destro del mouse `/apps/acs/analytics/components`. Seleziona **Crea...** seguito da **Crea componente...** La finestra di dialogo visualizzata consente di specificare:

   * **Etichetta**: `googleanalyticspage`
   * **Titolo**: `Google Analytics Page`
   * **Super Type**: `cq/cloudserviceconfigs/components/configpage`
   * **Gruppo**: `.hidden`

1. Fai clic su **Successivo** due volte e specifica:

   * **Elementi padre consentiti:** `acs/analytics/templates/googleanalytics`

   Fai clic su **Successivo** due volte e fai clic su **OK**.

1. Aggiungi una proprietà a `googleanalyticspage`:

   * **Nome:** `cq:defaultView`
   * **Valore:** `html`

1. Crea un nuovo file denominato `content.jsp` sotto `/apps/acs/analytics/components/googleanalyticspage`, con il seguente contenuto:

   ```xml
   <%@page contentType="text/html"
               pageEncoding="utf-8"%><%
   %><%@include file="/libs/foundation/global.jsp"%><div>
   
   <div>
       <h3>Google Analytics Settings</h3>
       <ul>
           <li><div class="li-bullet"><strong>accountID: </strong><br><%= xssAPI.encodeForHTML(properties.get("accountID", "")) %></div></li>
       </ul>
   </div>
   ```

1. Crea un nuovo nodo sotto `/apps/acs/analytics/components/googleanalyticspage/`:

   * **Nome**: `dialog`
   * **Tipo**: `cq:Dialog`
   * **Proprietà**:

      * **Nome**: `title`
      * **Tipo**: `String`
      * **Valore**: `Google Analytics Config`
      * **Nome**: `xtype`
      * **Tipo**: `String`
      * **Valore**: `dialog`

1. Crea un nuovo nodo sotto `/apps/acs/analytics/components/googleanalyticspage/dialog`:

   * **Nome**: `items`
   * **Tipo**: `cq:Widget`
   * **Proprietà**:

      * **Nome**: `xtype`
      * **Tipo**: `String`
      * **Valore**: `tabpanel`

1. Crea un nuovo nodo sotto `/apps/acs/analytics/components/googleanalyticspage/dialog/items`:

   * **Nome**: `items`
   * **Tipo**: `cq:WidgetCollection`

1. Crea un nuovo nodo sotto `/apps/acs/analytics/components/googleanalyticspage/dialog/items/items`:

   * **Nome**: scheda1
   * **Tipo**: `cq:Panel`
   * **Proprietà**:

      * **Nome**: `title`
      * **Tipo**: `String`
      * **Valore**: `Config`

1. Crea un nuovo nodo sotto `/apps/acs/analytics/components/googleanalyticspage/dialog/items/items/tab1`:

   * **Nome**: items
   * **Tipo**: `nt:unstructured`
   * **Proprietà**:

      * **Nome**: `fieldLabel`
      * **Tipo**: Stringa
      * **Valore**: ID account

      * **Nome**: `fieldDescription`
      * **Tipo**: `String`
      * **Valore**: `The account ID assigned by Google. Usually in the form UA-NNNNNN-N`

      * **Nome**: `name`
      * **Tipo**: `String`
      * **Valore**: `./accountID`
      * **Nome**: `validateOnBlur`
      * **Tipo**: `String`
      * **Valore**: `true`
      * **Nome**: `xtype`
      * **Tipo**: `String`
      * **Valore**: `textfield`

1. Copia `/libs/cq/cloudserviceconfigs/components/configpage/body.jsp` a `/apps/acs/analytics/components/googleanalyticspage/body.jsp` e cambiare `libs` a `apps` alla riga 34 e rendere il riferimento script alla riga 79 un percorso completo.
1. Crea un nuovo modello in `/apps/acs/analytics/templates/`:

   * con **Tipo di risorsa** = `acs/analytics/components/googleanalyticspage`
   * con **Etichetta** = `googleanalytics`
   * con **Titolo**= `Google Analytics Configuration`
   * con **allowedPath** = `/etc/cloudservices/googleanalytics(/.*)?`
   * con **allowedChildren** = `/apps/acs/analytics/templates/googleanalytics`
   * con **sling:resourceSuperType** = `cq/cloudserviceconfigs/templates/configpage` (sul nodo modello, non sul nodo jcr:content)
   * con **cq:designPath** = `/etc/designs/cloudservices/googleanalytics` (su jcr:content)

1. Crea un nuovo componente: `/apps/acs/analytics/components/googleanalytics`.

   Aggiungi il contenuto seguente a `googleanalytics.jsp`:

   ```xml
   <%@page import="org.apache.sling.api.resource.Resource,
                   org.apache.sling.api.resource.ValueMap,
                   org.apache.sling.api.resource.ResourceUtil,
                   com.day.cq.wcm.webservicesupport.Configuration,
                   com.day.cq.wcm.webservicesupport.ConfigurationManager" %>
   <%@include file="/libs/foundation/global.jsp" %><%
   
   String[] services = pageProperties.getInherited("cq:cloudserviceconfigs", new String[]{});
   ConfigurationManager cfgMgr = resource.getResourceResolver().adaptTo(ConfigurationManager.class);
   if(cfgMgr != null) {
       String accountID = null;
       Configuration cfg = cfgMgr.getConfiguration("googleanalytics", services);
       if(cfg != null) {
           accountID = cfg.get("accountID", null);
       }
   
       if(accountID != null) {
       %>
   <script type="text/javascript">
   
     var _gaq = _gaq || [];
     _gaq.push(['_setAccount', '<%= accountID %>']);
     _gaq.push(['_trackPageview']);
   
     (function() {
       var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
       ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'https://www') + '.google-analytics.com/ga.js';
       var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
     })();
   
   </script><%
       }
   }
   %>
   ```

   Questo dovrebbe generare il markup personalizzato in base alle proprietà di configurazione.

1. Passa a `http://localhost:4502/miscadmin#/etc/cloudservices` e crea una nuova pagina:

   * **Titolo**: `Google Analytics`
   * **Nome**: `googleanalytics`

   Torna in CRXDE Lite e sotto `/etc/cloudservices/googleanalytics`, aggiungi la seguente proprietà a `jcr:content`:

   * **Nome**: `componentReference`
   * **Tipo**: `String`
   * **Valore**: `acs/analytics/components/googleanalytics`


1. Passa alla nuova pagina Servizio ( `http://localhost:4502/etc/cloudservices/googleanalytics.html`) e fai clic su **+** per creare una nuova configurazione:

   * **Configurazione elemento padre**: `/etc/cloudservices/googleanalytics`
   * **Titolo:**  `My First GA Config`

   Scegli **Configurazione Google Analytics** e fai clic su **Crea**.

1. Inserisci un **ID account**, ad esempio `AA-11111111-1`. Fai clic su **OK**.
1. Passa a una pagina e aggiungi la configurazione appena creata nelle proprietà della pagina, nella sezione **Cloud Services** scheda .
1. Alla pagina verrà aggiunto il markup personalizzato.
