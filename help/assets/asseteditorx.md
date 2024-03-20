---
title: Estendi editor risorse
description: Scopri come estendere le funzionalità dell’Editor risorse utilizzando componenti personalizzati.
contentOwner: AG
role: User, Admin
feature: Developer Tools
exl-id: de1c63c1-a0e5-470b-8d83-b594513a5dbd
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 12%

---

# Estendi editor risorse {#extending-asset-editor}

L’Editor risorse è la pagina che si apre quando si fa clic su una risorsa trovata tramite Condivisione risorse, consentendo all’utente di modificare aspetti della risorsa come metadati, miniature, titolo e tag.

La configurazione dell’editor utilizzando i componenti di modifica predefiniti è descritta in [Creazione e configurazione di una pagina Editor risorse](assets-finder-editor.md#creating-and-configuring-an-asset-editor-page).

Oltre a utilizzare componenti editor preesistenti, [!DNL Adobe Experience Manager] gli sviluppatori possono anche creare i propri componenti.

## Creare un modello di Editor risorse {#creating-an-asset-editor-template}

Le pagine di esempio seguenti sono incluse in Geometrixx:

* Pagina di esempio Geometrixx: `/content/geometrixx/en/press/asseteditor.html`
* Modello di esempio: `/apps/geometrixx/templates/asseteditor`
* Componente pagina di esempio: `/apps/geometrixx/components/asseteditor`

### Configurare Clientlib {#configuring-clientlib}

[!DNL Assets] I componenti utilizzano un’estensione della libreria client di modifica WCM. Le clientlibs vengono generalmente caricate in `init.jsp`.

Rispetto al caricamento clientlib predefinito (in core `init.jsp`), un [!DNL Assets] il modello deve presentare le seguenti caratteristiche:

* Il modello deve includere `cq.dam.edit` clientlib (anziché `cq.wcm.edit`).

* Per poter eseguire il rendering di predicati, azioni e obiettivi, clientlib deve essere incluso anche in modalità WCM disabilitata (ad esempio, caricata **al momento della pubblicazione**).

Nella maggior parte dei casi, la copia del campione esistente `init.jsp` (`/apps/geometrixx/components/asseteditor/init.jsp`) deve soddisfare queste esigenze.

### Configurare azioni JS {#configuring-js-actions}

Alcune delle [!DNL Assets] I componenti richiedono le funzioni JS definite in `component.js`. Copia il file nella directory dei componenti e collegalo.

```javascript
<script type="text/javascript" src="<%= component.getPath() %>/component.js"></script>
```

L’esempio carica questa origine JavaScript in `head.jsp`(`/apps/geometrixx/components/asseteditor/head.jsp`).

### Fogli di stile aggiuntivi {#additional-style-sheets}

Alcune delle [!DNL Assets] i componenti utilizzano la libreria widget. Per eseguire correttamente il rendering nel contesto del contenuto, è necessario caricare un foglio di stile aggiuntivo. Il componente Azione tag ne richiede un altro.

```css
<link href="/etc/designs/geometrixx/ui.widgets.css" rel="stylesheet" type="text/css">
```

### Foglio di stile Geometrixx {#geometrixx-style-sheet}

I componenti della pagina di esempio richiedono che tutti i selettori inizino con `.asseteditor` di `static.css` (`/etc/designs/geometrixx/static.css`). Best practice: copia tutto `.asseteditor` selettori nel foglio di stile e regola le regole come desiderato.

### FormChooser: regolazioni per le risorse caricate {#formchooser-adjustments-for-eventually-loaded-resources}

L’Editor risorse utilizza il Selettore moduli, che consente di modificare le risorse, in questo caso le risorse, nella stessa pagina del modulo semplicemente aggiungendo un selettore di moduli e il percorso del modulo all’URL della risorsa.

Ad esempio:

* Pagina modulo normale: [http://localhost:4502/content/geometrixx/en/press/asseteditor.html](http://localhost:4502/content/geometrixx/en/press/asseteditor.html)
* Risorsa caricata nella pagina del modulo: [http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/en/press/asseteditor.html](http://localhost:4502/content/dam/geometrixx/icons/diamond.png.form.html/content/geometrixx/en/press/asseteditor.html)

Gli handle di esempio in `head.jsp` (`/apps/geometrixx/components/asseteditor/head.jsp`) effettuare le seguenti operazioni:

* Rilevano se una risorsa è caricata o se è necessario visualizzare il modulo normale.
* Se viene caricata una risorsa, viene disabilitata la modalità WCM, in quanto è possibile modificare i dati parsys solo su una pagina modulo normale.
* Se viene caricata una risorsa, ne viene utilizzato il titolo invece di quello presente nella pagina del modulo.

```javascript
 List<Resource> resources = FormsHelper.getFormEditResources(slingRequest);
    if (resources != null) {
        if (resources.size() == 1) {
            // single resource
            FormsHelper.setFormLoadResource(slingRequest, resources.get(0));
        } else if (resources.size() > 1) {
            // multiple resources
            // not supported by CQ 5.3
        }
    }
    Resource loadResource = (Resource) request.getAttribute("cq.form.loadresource");
    String title;
    if (loadResource != null) {
        // an asset is loaded: disable WCM
        WCMMode.DISABLED.toRequest(request);

        String path = loadResource.getPath();
        Asset asset = loadResource.adaptTo(Asset.class);
        try {
            // it might happen that the adobe xmp lib creates an array
            Object titleObj = asset.getMetadata("dc:title");
            if (titleObj instanceof Object[]) {
                Object[] titleArray = (Object[]) titleObj;
                title = (titleArray.length > 0) ? titleArray[0].toString() : "";
            } else {
                title = titleObj.toString();
            }
        }
        catch (NullPointerException e) {
            title = path.substring(path.lastIndexOf("/") + 1);
        }
    }
    else {
        title = currentPage.getTitle() == null ? currentPage.getName() : currentPage.getTitle();
    }
```

Nella parte HTML, utilizza il set di titoli precedente (titolo della risorsa o della pagina):

```html
<title><%= title %></title>
```

## Creare un componente campo modulo semplice {#creating-a-simple-form-field-component}

Questo esempio descrive come creare un componente che mostra e visualizza i metadati di una risorsa caricata.

1. Crea una cartella di componenti nella directory dei progetti, ad esempio: `/apps/geometrixx/components/samplemeta`.
1. Aggiungi `content.xml` con il seguente frammento:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Dimension"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Asset Editor"/>
   ```

1. Aggiungi `samplemeta.jsp` con il seguente frammento:

   ```javascript
   <%--
   
     Sample metadata field component
   
   --%><%@ page import="com.day.cq.dam.api.Asset,
                    java.security.AccessControlException" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       String value = "";
       String name = "dam:sampleMetadata";
       boolean readOnly = false;
   
       // If the form page is requested for an asset loadResource is the asset.
       Resource loadResource = (Resource) request.getAttribute("cq.form.loadresource");
   
       if (loadResource != null) {
   
           // Determine if the loaded asset is read only.
           Session session = slingRequest.getResourceResolver().adaptTo(Session.class);
           try {
               session.checkPermission(loadResource.getPath(), "set_property");
               readOnly = false;
           }
           catch (AccessControlException ace) {
               // checkPermission throws exception if asset is read only
               readOnly = true;
           }
           catch (RepositoryException re) {}
   
           // Get the value of the metadata.
           Asset asset = loadResource.adaptTo(Asset.class);
           try {
               value = asset.getMetadata(name).toString();
           }
           catch (NullPointerException npe) {
               // no metadata dc:description available
           }
       }
   %>
   <div class="form_row">
       <div class="form_leftcol">
           <div class="form_leftcollabel">Sample Metadata</div>
       </div>
       <div class="form_rightcol">
           <%
           if (readOnly) {
               %><c:out value="<%= value %>"/><%
           }
           else {
               %><input class="text" type="text" name="./jcr:content/metadata/<%= name %>" value="<c:out value="<%= value %>" />"><%
           }%>
       </div>
   </div>
   ```

1. Per rendere disponibile il componente, devi essere in grado di modificarlo. Per rendere modificabile un componente, in CRXDE Liti aggiungi un nodo `cq:editConfig` di tipo primario `cq:EditConfig`. Per rimuovere i paragrafi, aggiungi una proprietà con più valori `cq:actions` con un singolo valore di `DELETE`.

1. Passa al browser e nella pagina di esempio (ad esempio, `asseteditor.html`) passa alla modalità progettazione e attiva il nuovo componente per il sistema paragrafo.

1. Nella modalità **Modifica**, il nuovo componente, ad esempio, **Metadati campione**, è ora disponibile nella barra laterale (gruppo **Editor risorse**). Inserisci il componente. Per memorizzare i metadati, è necessario aggiungerli al modulo relativo.

## Modifica opzioni metadati {#modifying-metadata-options}

È possibile modificare gli spazi dei nomi disponibili nel [modulo metadati](assets-finder-editor.md#metadata-form-and-text-field-configuring-the-view-metadata-component).

I metadati attualmente disponibili sono definiti in `/libs/dam/options/metadata`:

* Il primo livello all&#39;interno di questa directory contiene gli spazi dei nomi.
* Gli elementi all&#39;interno di ogni spazio dei nomi rappresentano metadati, ad esempio il risultato in un elemento di parte locale.
* Il contenuto dei metadati contiene le informazioni per il tipo e le opzioni con più valori.

Le opzioni possono essere sovrascritte in `/apps/dam/options/metadata`:

1. Copia la directory da `/libs` a `/apps`.

1. Rimuovere, modificare o aggiungere elementi.

>[!NOTE]
>
>Se aggiungi nuovi spazi dei nomi, questi devono essere registrati nel tuo archivio/CRX. In caso contrario, l’invio del modulo di metadati genererà un errore.
