---
title: Aggiungere un’azione personalizzata alla visualizzazione Elenco risorse
seo-title: Aggiungere un’azione personalizzata alla visualizzazione Elenco risorse
description: In questo articolo viene illustrato come aggiungere un’azione personalizzata alla visualizzazione Elenco risorse
seo-description: In questo articolo viene illustrato come aggiungere un’azione personalizzata alla visualizzazione Elenco risorse
uuid: 45f25cfb-f08f-42c6-99c5-01900dd8cdee
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 6378ae30-a351-49f7-8e9a-f0bd4287b9d3
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1381'
ht-degree: 2%

---


# Aggiungere un&#39;azione personalizzata alla visualizzazione Elenco risorse{#add-custom-action-to-the-asset-listing-view}

## Panoramica {#overview}

La soluzione Gestione della corrispondenza consente di aggiungere azioni personalizzate all’interfaccia utente Gestisci risorse.

Potete aggiungere un’azione personalizzata alla visualizzazione Elenco risorse per:

* Uno o più tipi di risorse o lettere
* Esecuzione (azione/comando diventa attivo) in caso di selezione di risorse/lettere singole o multiple o senza selezione

Questa personalizzazione viene illustrata con lo scenario in cui viene aggiunto il comando &quot;Scarica PDF semplice&quot; alla visualizzazione Elenco risorse per lettere. Questo scenario di personalizzazione consente agli utenti di scaricare un PDF semplice di una singola lettera selezionata.

### Prerequisiti {#prerequisites}

Per completare il seguente scenario o uno scenario simile, è necessario conoscere:

* CRX
* JavaScript
* Java

## Scenario: Aggiungere un comando all&#39;interfaccia utente dell&#39;elenco Lettere per scaricare la versione PDF semplice di una lettera {#addcommandtoletters}

La procedura seguente aggiunge un comando &quot;Scarica PDF semplice&quot; alla visualizzazione Elenco risorse per lettere e consente agli utenti di scaricare un PDF semplice della lettera selezionata. Utilizzando questi passaggi con il codice e i parametri appropriati, potete aggiungere altre funzionalità a una risorsa diversa, come dizionari di dati o testi.

Per personalizzare la gestione della corrispondenza per consentire agli utenti di scaricare un PDF semplice di lettere, procedere come segue:

1. Andate a `https://'[server]:[port]'/[ContextPath]/crx/de` e accedete come amministratore.

1. Nella cartella delle app, create una cartella denominata items con percorso/struttura simile alla cartella degli elementi che si trova nella cartella di selezione mediante la procedura seguente:

   1. Fare clic con il pulsante destro del mouse sulla cartella **items** nel percorso seguente e selezionare **Overlay Node**:

      `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/body/content/header/items/selection/items`

      >[!NOTE]
      >
      >Questo percorso è specifico per la creazione di un’azione che funziona con la selezione di una o più risorse/lettere. Se desiderate creare un’azione che funzioni senza selezione, dovete creare un nodo di sovrapposizione per il percorso seguente e completare di conseguenza i passaggi rimanenti:
      >
      >
      >`/libs/fd/cm/ma/gui/content/cmassets/jcr:content/body/content/header/items/default/items`

      ![Crea nodo](assets/1_itemscreatenode.png)

   1. Verificate che la finestra di dialogo Nodo sovrapposizione contenga i seguenti valori:

      **Percorso:** /libs/fd/cm/ma/gui/content/cmassets/jcr:content/body/content/header/items/selection/items

      **Posizione:** /app/

      **Corrispondenza tipi di nodo:** Selezionati

      ![Sovrapposizione, nodo](assets/2_createnodedownloadflatpdf.png)

   1. Fai clic su **OK**. La struttura delle cartelle viene creata nella cartella delle app.

      Fare clic su **Salva tutto**.

1. Nella cartella degli elementi appena creati, aggiungete un nodo per il pulsante o l’azione personalizzati in una risorsa specifica (esempio: downloadFlatPDF) utilizzando la procedura seguente:

   1. Fare clic con il pulsante destro del mouse sulla cartella **items** e selezionare **Crea** > **Crea nodo**.

   1. Assicurarsi che la finestra di dialogo Crea nodo contenga i valori seguenti e fare clic su **OK**:

      **Nome:** downloadFlatPDF (o il nome che si desidera assegnare a questa proprietà)

      **Tipo:** nt:unstructure

   1. Fare clic sul nuovo nodo creato (qui downloadFlatPDF). CRX visualizza le proprietà del nodo.

   1. Aggiungi le seguenti proprietà al nodo (qui downloadFlatPDF) e fai clic su **Salva tutto**:

      <table>
        <tbody>
        <tr>
        <td><strong>Nome</strong></td>
        <td><strong>Tipo</strong></td>
        <td><strong>Valore e descrizione</strong></td>
        </tr>
        <tr>
        <td>classe</td>
        <td>Stringa</td>
        <td>foundation-collection-action</td>
        </tr>
        <tr>
        <td>foundation-collection-action</td>
        <td>Stringa</td>
        <td><p>{"target": ".cq-management-asset-admin-child-pages", "activeSelectionCount": "single","type": "LETTER"}<br /> <br /> <br /> <strong>activeSelectionCount</strong> può essere uno o più elementi, per consentire la selezione di una o più risorse su cui viene eseguita l'azione personalizzata.</p> <p><strong>può </strong> essere una o più voci (voci multiple separate da virgola) tra le seguenti: LETTERA,TESTO,ELENCO,CONDIZIONE,DATADICTIONARIO</p> </td>
        </tr>
        <tr>
        <td>icon</td>
        <td>Stringa</td>
        <td>icon-download<br /> <br /> L'icona che Gestione corrispondenza viene visualizzata a sinistra del comando/menu. Per le diverse icone e impostazioni disponibili, consultate la <a href="https://docs.adobe.com/docs/en/aem/6-3/develop/ref/coral-ui/coralui3/Coral.Icon.html" target="_blank">documentazione delle icone CoralUI</a>.<br /> </td>
        </tr>
        <tr>
        <td>jcr:primaryType</td>
        <td>Nome</td>
        <td>nt:unstructured</td>
        </tr>
        <tr>
        <td>rel</td>
        <td>Stringa</td>
        <td>download-flat-pdf-button</td>
        </tr>
        <tr>
        <td>sling:resourceType</td>
        <td>Stringa</td>
        <td>granite/ui/components/endor/actionbar/button</td>
        </tr>
        <tr>
        <td>testo</td>
        <td>Stringa</td>
        <td>Scarica PDF semplice (o qualsiasi altra etichetta)<br /> <br /> Il comando che viene visualizzato nell'interfaccia Elenco risorse</td>
        </tr>
        <tr>
        <td>titolo</td>
        <td>Stringa</td>
        <td>Scaricate un PDF semplice della lettera selezionata (o di qualsiasi altro testo etichetta/Alt)<br /> <br /> Il titolo è il testo alternativo visualizzato quando l'utente passa il puntatore del mouse sul comando personalizzato.</td>
        </tr>
        </tbody>
       </table>

1. Nella cartella delle app, create una cartella denominata js con percorso/struttura simile alla cartella degli elementi che si trova nella cartella di amministrazione tramite la procedura seguente:

   1. Fare clic con il pulsante destro del mouse sulla cartella **js** nel percorso seguente e selezionare **Overlay Node**:

      `/libs/fd/cm/ma/gui/components/admin/clientlibs/admin/js`

   1. Verificate che la finestra di dialogo Nodo sovrapposizione contenga i seguenti valori:

      **Percorso:** /libs/fd/cm/ma/gui/components/admin/clientlibs/admin/js

      **Posizione:** /app/

      **Corrispondenza tipi di nodo:** Selezionati

   1. Fai clic su **OK**. La struttura delle cartelle viene creata nella cartella delle app. Fare clic su **Salva tutto**.

1. Nella cartella js, creare un file denominato formaction.js con il codice per la gestione dell&#39;azione del pulsante utilizzando la procedura seguente:

   1. Fare clic con il pulsante destro del mouse sulla cartella **js** nel percorso seguente e selezionare **Crea > Crea file**:

      `/apps/fd/cm/ma/gui/components/admin/clientlibs/admin/js`

      Denominate il file come formaction.js.

   1. Fate doppio clic sul file per aprirlo in CRX.
   1. Nel file formaction.js (sotto il ramo /apps), copiate il codice dal file formaction.js nel percorso seguente:

      `/libs/fd/cm/ma/gui/components/admin/clientlibs/admin/js/formaction.js`

      Quindi aggiungete il codice seguente alla fine del file formaction.js (sotto il ramo /apps) e fate clic su **Salva tutto**:

      ```javascript
      /* Action url for xml file to be added.*/
      var ACTION_URL = "/apps/fd/cm/ma/gui/content/commons/actionhandlers/items/letterpdfdownloader.html";
      
      /* File upload handling*/
      var fileSelectedHandler = function(e){
          if(e && e.target && e.target.value)
              $(".downloadLetterPDFBtn").removeAttr('disabled');
          else
              $(".downloadLetterPDFBtn").attr('disabled','disabled');
      }
      
      /*Handing of Download button in pop up.*/
      var downloadClickHandler = function(){
          $('#downloadLetterPDFDilaog').modal("hide");
          var element = $('.foundation-selections-item');
          var path = $(element).data("path");
          $("#fileUploadForm").attr('action', ACTION_URL + "?letterId="+path).submit();
      }
      
      /*Click handling on action button.*/
      $(document).on("click",'.download-flat-pdf-button',function(e){
          $("#uploadSamepledata").val("");
           if($('#downloadLetterPDFDilaog').length == 0){
              $(document).on("click",".downloadLetterPDFBtn",downloadClickHandler);
              $(document).on("change","#uploadSamepledata",fileSelectedHandler);
              $("body").append(downloadLetterPDFDilaog);
          }
            $('#downloadLetterPDFDilaog').modal("show");
      });
      
      /*Download popup.*/
      var downloadLetterPDFDilaog = '<div id="downloadLetterPDFDilaog" class="coral-Modal notice " role="dialog"  aria-hidden="true">'+
          '<form id="fileUploadForm" method="POST" enctype="multipart/form-data">'+
              '<div class="coral-Modal-header">'+
                  '<h2 class="coral-Modal-title coral-Heading coral-Heading--2" id="modal-header1443020790107-label" tabindex="0">Download Letter as PDF.</h2>'+
                  '<button type="button" class="coral-MinimalButton coral-Modal-closeButton" data-dismiss="modal">×</button>'+
              '</div>'+
              '<div class="coral-Modal-body" id="modal-header1443020790107-message" role="document" tabindex="0">'+
                  '<div class="coral-Modal-message">'+
                      '<p></p>'+
                  '</div>'+
                  '<div class="coral-Modal-uploader">'+
                      '<p>Select sample data for letter.</p>'+
                      '<input type="file" id="uploadSamepledata" name="file" accept=".xml" size="70px">'+
                  '</div>'+
              '</div>'+
           '</form>'+
              '<div class="coral-Modal-footer">'+
                  '<button type="button" class="coral-Button" data-dismiss="modal">Cancel</button>'+
                  '<button type="button" class="coral-Button coral-Button--primary downloadLetterPDFBtn" disabled="disabled">Download</button>'+
              '</div>'+
      '</div>';
      ```

      Il codice aggiunto in questo passaggio ha la priorità sul codice presente nella cartella libs, quindi copiate il codice precedente nel file formaction.js nel ramo /apps. Copiando il codice dal ramo /libs al ramo /apps si garantisce che funzioni anche la funzionalità precedente.

      Il codice riportato sopra è relativo alla gestione dell&#39;azione specifica delle lettere del comando creato in questa procedura. Per la gestione delle azioni di altre risorse, modificate il codice JavaScript.

1. Nella cartella delle app, create una cartella denominata items con percorso/struttura simile alla cartella degli elementi che si trova nella cartella dei gestori di azioni, eseguendo la procedura seguente:

   1. Fare clic con il pulsante destro del mouse sulla cartella **items** nel percorso seguente e selezionare **Overlay Node**:

      `/libs/fd/cm/ma/gui/content/commons/actionhandlers/items/`

   1. Verificate che la finestra di dialogo Nodo sovrapposizione contenga i seguenti valori:

      **Percorso:** /libs/fd/cm/ma/gui/content/commons/actionhandlers/items/

      **Posizione:** /app/

      **Corrispondenza tipi di nodo:** Selezionati

   1. Fai clic su **OK**. La struttura delle cartelle viene creata nella cartella delle app.

   1. Fare clic su **Salva tutto**.

1. Sotto il nodo di elementi appena creati, aggiungete un nodo per il pulsante/azione personalizzato in una risorsa particolare (esempio: letterpdfdownloader) utilizzando i seguenti passaggi:

   1. Fare clic con il pulsante destro del mouse sulla cartella degli elementi e selezionare **Crea > Crea nodo**.

   1. Assicurarsi che la finestra di dialogo Crea nodo contenga i valori seguenti e fare clic su **OK**:

      **Nome:** letterpdfdownloader (oppure il nome che si desidera assegnare a questa proprietà) deve essere univoco. Se utilizzate un nome diverso, specificate lo stesso nella variabile ACTION_URL del file formaction.js.)

      **Tipo:** nt:unstructure

   1. Fare clic sul nuovo nodo creato (qui downloadFlatPDF). CRX visualizza le proprietà del nodo.

   1. Aggiungete la seguente proprietà al nodo (qui letterpdfdownloader) e fate clic su **Salva tutto**:

      | **Nome** | **Tipo** | **Valore** |
      |---|---|---|
      | sling:resourceType | Stringa | fd/cm/ma/gui/components/admin/clientlibs/admin |

1. Create un file denominato POST.jsp con il codice per la gestione dell&#39;azione del comando nella posizione seguente:

   /apps/fd/cm/ma/gui/components/admin/clientlibs/admin

   1. Fare clic con il pulsante destro del mouse sulla cartella **admin** nel percorso seguente e selezionare **Crea > Crea file**:

      /apps/fd/cm/ma/gui/components/admin/clientlibs/admin

      Denominate il file come POST.jsp. (il nome del file deve essere solo POST.jsp.)

   1. Fare doppio clic sul file **POST.jsp** per aprirlo in CRX.
   1. Aggiungi il codice seguente al file POST.jsp e fai clic su **Salva tutto**:

      Questo codice è specifico per il servizio di rendering della lettera. Per qualsiasi altra risorsa, aggiungi le librerie Java della risorsa al codice. Per ulteriori informazioni sulle  API AEM Forms, consultate [ API AEM Forms](https://adobe.com/go/learn_aemforms_javadocs_63_en).

      Per ulteriori informazioni sulle librerie AEM, vedere AEM [Componenti](/help/sites-developing/components.md).

      ```xml
      /*Import libraries. Here we are downloading letter flat pdf with input xml data so we require letterRender Api. For any other Module functionality we need to first import that library. */
      <%@include file="/libs/foundation/global.jsp"%>
      <!DOCTYPE html lang="en" PUBLIC "-//W3C//DTD XHTML 1.1//EN" "https://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">
      <%@page import="com.adobe.icc.ddg.api.*"%>
      <%@page import="com.adobe.icc.dbforms.obj.*"%>
      <%@page import="com.adobe.icc.render.obj.*" %>
      <%@page import="com.adobe.icc.services.api.*" %>
      <%@page import="org.apache.sling.api.resource.*" %>
      <%@page import="java.io.File" %>
      <%@page import="java.util.*" %>
      <%@page import="com.adobe.livecycle.content.appcontext.AppContextManager"%>
      <%@page import=" com.adobe.icc.dbforms.exceptions.ICCException"%>
      <%@page import="java.io.InputStream" %>
      <%@page import="java.io.FileInputStream" %>
      <%@page import="org.apache.commons.io.IOUtils" %>
      <%@page session="false" contentType="text/html; charset=utf-8"%>
      <%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0"%>
      <%@taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %>
       <%@page session="false" contentType="text/html; charset=utf-8"%>
      <%
         AppContextManager.setCurrentAppContext("/content/apps/cm");
         /*Get letter id sent in js file.*/
          String letterId = request.getParameter("letterId");
          if(letterId.lastIndexOf("?") != -1)
              letterId = letterId.substring(0, letterId.indexOf("?"));
          String fileName = null;
          String letterName = null;
          InputStream inputStream = null;
          /*Get xml file data*/
          if (slingRequest.getRequestParameter("file") != null)
              inputStream = slingRequest.getRequestParameter("file").getInputStream();
          if(letterId != null){
              String xmlData = null;
              try{
                  xmlData = IOUtils.toString(inputStream, "UTF-8");
              }
              catch (Exception e) {
                  log.error("Xml data does not exists.");
              }
              /*letter Name from letter letter id.*/
              letterName = letterId.substring(letterId.lastIndexOf("/")+1);
              /*Invoking letter render services API.*/
              LetterRenderService letterRenderService = sling.getService(LetterRenderService.class);
              /*using CM renderLetter api to get pdfbytes.*/
              PDFResponseType  pdfResponseType= letterRenderService.renderLetter(letterId,xmlData,true,false,false,false);
              byte[] bytes = null;
              /*Downloading pdf bytes as pdf.*/
              if(pdfResponseType != null && pdfResponseType.getFile() != null){
                  bytes = pdfResponseType.getFile().getDocument();
                  /*set the response header to enable download*/
                  response.setContentType("application/OCTET-STREAM");
                  response.setHeader("Content-Disposition", "attachment;filename=\"" + letterName + ".pdf\"");
                  response.setHeader("Pragma", "cache");
                  response.setHeader("Cache-Control", "private");
                  out.clear();
                  response.getOutputStream().write(bytes);
              }
          }
          else{
              log.error("Letter id does not exists.");
          }
      %>
      ```

## Scarica il PDF semplice di una lettera utilizzando la funzionalità personalizzata {#download-flat-pdf-of-a-letter-using-the-custom-functionality}

Dopo aver aggiunto funzionalità personalizzate per scaricare il PDF piatto delle lettere, è possibile utilizzare la procedura seguente per scaricare la versione PDF semplice della lettera selezionata:

1. Vai a `https://'[server]:[port]'/[ContextPath]/projects.html` ed effettua l&#39;accesso.

1. Selezionare **Forms > Lettere**. Gestione corrispondenza elenca le lettere disponibili nel sistema.
1. Fare clic su **Seleziona**, quindi fare clic su una lettera per selezionarla.
1. Selezionare **More** > **&lt;Download Flat PDF>** (la funzionalità personalizzata creata utilizzando le istruzioni di questo articolo). Viene visualizzata la finestra di dialogo Scarica lettera come PDF.

   Il nome, la funzionalità e il testo alt della voce di menu si basano sulla personalizzazione creata in [Scenario: Aggiungere un comando all&#39;interfaccia utente dell&#39;elenco Lettere per scaricare la versione PDF semplice di una lettera.](#addcommandtoletters)

   ![Funzionalità personalizzata: Scarica PDF semplice](assets/5_downloadflatpdf.png)

1. Nella finestra di dialogo Scarica lettera come PDF, selezionare il codice XML appropriato dal quale si desidera compilare i dati nel PDF.

   >[!NOTE]
   >
   >Prima di scaricare la lettera come PDF semplice, è possibile creare il file XML con i dati nella lettera utilizzando l&#39;opzione **Crea rapporto**.

   ![Scarica la lettera come PDF](assets/6_downloadflatpdf.png)

   La lettera viene scaricata nel computer come PDF semplice.

