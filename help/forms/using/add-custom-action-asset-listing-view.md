---
title: Aggiungere un’azione personalizzata alla vista Elenco risorse
description: Questo articolo illustra come aggiungere un’azione personalizzata alla visualizzazione Elenco risorse
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: bf6d3edb-6bf7-4d3e-b042-d75cb8e39e3f
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1333'
ht-degree: 2%

---

# Aggiungere un’azione personalizzata alla vista Elenco risorse{#add-custom-action-to-the-asset-listing-view}

## Panoramica {#overview}

La soluzione Gestione della corrispondenza consente di aggiungere azioni personalizzate all’interfaccia utente Gestione risorse.

Puoi aggiungere un’azione personalizzata alla vista Elenco risorse per:

* Uno o più tipi di risorse o lettere
* Esecuzione (azione/comando diventa attivo) quando si selezionano risorse/lettere singole o multiple o senza selezione

Questa personalizzazione viene dimostrata con lo scenario che aggiunge un comando &quot;Scarica Flat PDF&quot; alla visualizzazione Elenco risorse per le lettere. Questo scenario di personalizzazione consente agli utenti di scaricare flat PDF di una singola lettera selezionata.

### Prerequisiti {#prerequisites}

Per completare il seguente scenario o uno simile, è necessario conoscere:

* CRX
* JavaScript
* Java™

## Scenario: aggiungere un comando all&#39;interfaccia utente dell&#39;elenco Lettere per scaricare la versione flat PDF di una lettera {#addcommandtoletters}

I passaggi seguenti aggiungono un comando &quot;Scarica Flat PDF&quot; alla visualizzazione Elenco risorse per Lettere e consentono agli utenti di scaricare Flat PDF della lettera selezionata. Utilizzando questi passaggi con il codice e i parametri appropriati, puoi aggiungere altre funzionalità per una risorsa diversa, ad esempio dizionari di dati o testi.

La procedura seguente illustra come personalizzare Gestione della corrispondenza per consentire agli utenti di scaricare un PDF piatto di lettere:

1. Vai a `https://'[server]:[port]'/[ContextPath]/crx/de` e accedere come amministratore.

1. Nella cartella delle app, crea una cartella denominata items con un percorso/struttura simile a quello della cartella items nella cartella selection (selezione), seguendo la procedura descritta di seguito:

   1. Fare clic con il pulsante destro del mouse **elementi** cartella nel percorso seguente e selezionare **Sovrapponi nodo**:

      `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/body/content/header/items/selection/items`

      >[!NOTE]
      >
      >Questo percorso è specifico per creare un’azione che funziona con la selezione di una o più risorse o lettere. Se desideri creare un&#39;azione che funzioni senza selezione, crea invece un nodo di sovrapposizione per il percorso seguente e completa i passaggi rimanenti di conseguenza:
      >
      >
      >`/libs/fd/cm/ma/gui/content/cmassets/jcr:content/body/content/header/items/default/items`

      ![Crea nodo](assets/1_itemscreatenode.png)

   1. Assicurati che la finestra di dialogo Sovrapponi nodo abbia i seguenti valori:

      **Percorso:** /libs/fd/cm/ma/gui/content/cmassets/jcr:content/body/content/header/items/selection/items

      **Posizione:** /apps/

      **Corrispondenza tipi di nodo:** Selezionato

      ![Sovrapponi nodo](assets/2_createnodedownloadflatpdf.png)

   1. Clic **OK**. La struttura di cartelle viene creata nella cartella delle app.

      Clic **Salva tutto**.

1. Nella cartella degli elementi appena creata, aggiungi un nodo per il pulsante/azione personalizzato in una particolare risorsa (Esempio: downloadFlatPDF) seguendo la procedura riportata di seguito:

   1. Fare clic con il pulsante destro del mouse **elementi** cartella e seleziona **Crea** > **Crea nodo**.

   1. Assicurati che la finestra di dialogo Crea nodo abbia i seguenti valori e fai clic su **OK**:

      **Nome:** downloadFlatPDF (o il nome da assegnare a questa proprietà)

      **Tipo:** nt:unstructured

   1. Fai clic sul nuovo nodo creato (qui downloadFlatPDF). CRX visualizza le proprietà del nodo.

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
        <td><p>{"target": ".cq-manageasset-admin-childpages", "activeSelectionCount": "single","type": "LETTER"}<br /> <br /> <br /> <strong>activeSelectionCount</strong> può essere singolo o multiplo per consentire selezioni di una o più risorse sulle quali viene eseguita l’azione personalizzata.</p> <p><strong>tipo</strong> può essere una o più delle seguenti voci (separa virgole più voci): LETTERA,TESTO,ELENCO,CONDIZIONE,DIZIONARIO DATI</p> </td>
        </tr>
        <tr>
        <td>icon</td>
        <td>Stringa</td>
        <td>icon-download<br /> <br /> Icona visualizzata da Gestione corrispondenza sul lato sinistro del comando o del menu. Per informazioni sulle diverse icone e impostazioni disponibili, vedere <a href="https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=it" target="_blank">Documentazione delle icone di CoralUI</a>.<br /> </td>
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
        <td>text</td>
        <td>Stringa</td>
        <td>Scarica Flat PDF (o qualsiasi altra etichetta)<br /> <br /> Comando visualizzato nell’interfaccia Elenco risorse</td>
        </tr>
        <tr>
        <td>titolo</td>
        <td>Stringa</td>
        <td>Scarica un PDF piatto della lettera selezionata (o qualsiasi altra etichetta/testo alternativo)<br /> <br /> Il titolo è il testo alternativo visualizzato da Gestione corrispondenza quando l’utente passa il puntatore sul comando personalizzato.</td>
        </tr>
        </tbody>
       </table>

1. Nella cartella apps, crea una cartella denominata js con un percorso/struttura simile a quello della cartella items nella cartella admin, seguendo la procedura riportata di seguito:

   1. Fare clic con il pulsante destro del mouse **js** cartella nel percorso seguente e selezionare **Sovrapponi nodo**:

      `/libs/fd/cm/ma/gui/components/admin/clientlibs/admin/js`

   1. Assicurati che la finestra di dialogo Sovrapponi nodo abbia i seguenti valori:

      **Percorso:** /libs/fd/cm/ma/gui/components/admin/clientlibs/admin/js

      **Posizione:** /apps/

      **Corrispondenza tipi di nodo:** Selezionato

   1. Clic **OK**. La struttura di cartelle viene creata nella cartella delle app. Clic **Salva tutto**.

1. Nella cartella js, crea un file denominato formaction.js con il codice per la gestione delle azioni del pulsante, seguendo la procedura riportata di seguito:

   1. Fare clic con il pulsante destro del mouse **js** cartella nel percorso seguente e selezionare **Crea > Crea file**:

      `/apps/fd/cm/ma/gui/components/admin/clientlibs/admin/js`

      Denomina il file come formaction.js.

   1. Fai doppio clic sul file per aprirlo in CRX.
   1. Nel file formaction.js (nel ramo /apps), copia il codice dal file formaction.js nel percorso seguente:

      `/libs/fd/cm/ma/gui/components/admin/clientlibs/admin/js/formaction.js`

      Quindi aggiungi il seguente codice alla fine nel file formaction.js (nel ramo /apps) e fai clic su **Salva tutto**:

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

      Il codice aggiunto in questo passaggio sostituisce il codice nella cartella libs, quindi copia il codice precedente nel file formaction.js nel ramo /apps. Copiare il codice dal ramo /libs al ramo /apps garantisce il funzionamento anche della funzionalità precedente.

      Il codice riportato sopra è per la gestione delle azioni specifiche per le lettere del comando creato in questa procedura. Per la gestione delle azioni relative ad altre risorse, modifica il codice JavaScript.

1. Nella cartella delle app, crea una cartella denominata items con un percorso/struttura simile a quello della cartella items nella cartella actionhandlers, seguendo la procedura riportata di seguito:

   1. Fare clic con il pulsante destro del mouse **elementi** cartella nel percorso seguente e selezionare **Sovrapponi nodo**:

      `/libs/fd/cm/ma/gui/content/commons/actionhandlers/items/`

   1. Assicurati che la finestra di dialogo Sovrapponi nodo abbia i seguenti valori:

      **Percorso:** /libs/fd/cm/ma/gui/content/commons/actionhandlers/items/

      **Posizione:** /apps/

      **Corrispondenza tipi di nodo:** Selezionato

   1. Clic **OK**. La struttura di cartelle viene creata nella cartella delle app.

   1. Clic **Salva tutto**.

1. Nel nodo degli elementi appena creati, aggiungi un nodo per il pulsante/azione personalizzato in una particolare risorsa (Esempio: letterpdfdownloader) seguendo la procedura riportata di seguito:

   1. Fai clic con il pulsante destro del mouse sulla cartella degli elementi e seleziona **Crea > Crea nodo**.

   1. Assicurati che la finestra di dialogo Crea nodo abbia i seguenti valori e fai clic su **OK**:

      **Nome:** letterpdfdownloader (o il nome che si desidera assegnare a questa proprietà) deve essere univoco. Se utilizzi un nome diverso, specifica lo stesso nella variabile ACTION_URL del file formaction.js.

      **Tipo:** nt:unstructured

   1. Fai clic sul nuovo nodo creato (qui downloadFlatPDF). CRX visualizza le proprietà del nodo.

   1. Aggiungi la seguente proprietà al nodo (qui letterpdfdownloader) e fai clic su **Salva tutto**:

      | **Nome** | **Tipo** | **Valore** |
      |---|---|---|
      | sling:resourceType | Stringa | fd/cm/ma/gui/components/admin/clientlibs/admin |

1. Crea un file denominato POST.jsp con il codice per la gestione delle azioni del comando nel percorso seguente:

   /apps/fd/cm/ma/gui/components/admin/clientlibs/admin

   1. Fare clic con il pulsante destro del mouse **admin** cartella nel percorso seguente e selezionare **Crea > Crea file**:

      /apps/fd/cm/ma/gui/components/admin/clientlibs/admin

      Denomina il file come POST.jsp. Il nome del file deve essere solo POST.jsp.

   1. Fai doppio clic su **POST.jsp** per aprirlo in CRX.
   1. Aggiungi il codice seguente al file POST.jsp e fai clic su **Salva tutto**:

      Questo codice è specifico per il servizio di rendering di lettere. Per qualsiasi altra risorsa, aggiungi le librerie Java™ di quella risorsa a questo codice. Per ulteriori informazioni sulle API di AEM Forms, consulta [API AEM FORMS](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=it).

      Per ulteriori informazioni sulle librerie AEM, vedi AEM [Componenti](/help/sites-developing/components.md).

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

## Scaricare il PDF flat di una lettera utilizzando la funzionalità personalizzata {#download-flat-pdf-of-a-letter-using-the-custom-functionality}

Dopo aver aggiunto la funzionalità personalizzata per il download di flat PDF delle lettere, è possibile utilizzare i seguenti passaggi per scaricare la versione flat PDF della lettera selezionata:

1. Vai a `https://'[server]:[port]'/[ContextPath]/projects.html` e accedi.

1. Seleziona **Forms > Lettere**. Gestione della corrispondenza elenca le lettere disponibili nel sistema.
1. Clic **Seleziona** quindi fare clic su una lettera per selezionarla.
1. Seleziona **Altro** > **&lt;download flat=&quot;&quot; pdf=&quot;&quot;>** La funzionalità personalizzata creata seguendo le istruzioni di questo articolo. Viene visualizzata la finestra di dialogo Scarica lettera come PDF.

   Il nome della voce di menu, la funzionalità e il testo alternativo dipendono dalla personalizzazione creata in [Scenario: aggiungere un comando all&#39;interfaccia utente dell&#39;elenco Lettere per scaricare la versione flat PDF di una lettera.](#addcommandtoletters)

   ![Funzionalità personalizzata: scarica Flat PDF](assets/5_downloadflatpdf.png)

1. Nella finestra di dialogo Scarica lettera come PDF, seleziona l’XML appropriato da cui vuoi popolare i dati nel PDF.

   >[!NOTE]
   >
   >Prima di scaricare la lettera come PDF semplice, potete creare il file XML con i dati contenuti nella lettera utilizzando **Crea rapporto** opzione.

   ![Scarica lettera come PDF](assets/6_downloadflatpdf.png)

   La lettera viene scaricata nel computer come PDF semplice.
