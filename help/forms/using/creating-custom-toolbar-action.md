---
title: Creazione di un’azione personalizzata per la barra degli strumenti
seo-title: Creazione di un’azione personalizzata per la barra degli strumenti
description: Gli sviluppatori di moduli possono creare azioni personalizzate sulla barra degli strumenti per i moduli adattivi in AEM Forms. L'utilizzo di azioni personalizzate da parte degli autori di moduli consente agli utenti finali di disporre di più flussi di lavoro e opzioni.
seo-description: Gli sviluppatori di moduli possono creare azioni personalizzate sulla barra degli strumenti per i moduli adattivi in AEM Forms. L'utilizzo di azioni personalizzate da parte degli autori di moduli consente agli utenti finali di disporre di più flussi di lavoro e opzioni.
uuid: cd785cfb-e1bb-4158-be9b-d99e04eccc02
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 4beca23f-dbb0-4e56-8047-93e4f1775418
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---


# Creazione di un’azione personalizzata per la barra degli strumenti{#creating-a-custom-toolbar-action}

## Prerequisiti {#prerequisite}

Prima di creare un&#39;azione personalizzata per la barra degli strumenti, acquisire familiarità con [l&#39;utilizzo delle librerie](/help/sites-developing/clientlibs.md) lato client e lo [sviluppo con CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

## Azione {#what-is-an-action-br}

Un modulo adattivo fornisce una barra degli strumenti che consente all&#39;autore del modulo di configurare un set di opzioni. Queste opzioni sono definite come azioni per il modulo adattivo. Fare clic sul pulsante Modifica nella barra degli strumenti del pannello per impostare le azioni supportate dai moduli adattivi.

![Azioni predefinite della barra degli strumenti](assets/default_toolbar_actions.png)

Oltre al set di azioni fornito per impostazione predefinita, nella barra degli strumenti è possibile creare azioni personalizzate. Ad esempio, è possibile aggiungere un&#39;azione per consentire all&#39;utente di visualizzare tutti i campi modulo adattivo prima dell&#39;invio di un modulo.

## Passaggi per creare un&#39;azione personalizzata in un modulo adattivo {#steps}

Per illustrare la creazione di un&#39;azione personalizzata per la barra degli strumenti, la seguente procedura consente di creare un pulsante che consenta agli utenti finali di visualizzare tutti i campi modulo adattivi prima di inviare un modulo compilato.

1. Tutte le azioni predefinite supportate dai moduli adattivi sono presenti nella `/libs/fd/af/components/actions` cartella. In CRXDE, copiare il `fileattachmentlisting` nodo da `/libs/fd/af/components/actions/fileattachmentlisting` a `/apps/customaction`.

1. Dopo aver copiato il nodo nella `apps/customaction` cartella, rinominate il nome del nodo in `reviewbeforesubmit`. Inoltre, modificare le `jcr:title` proprietà e `jcr:description` le proprietà del nodo.

   La `jcr:title` proprietà contiene il nome dell&#39;azione visualizzata nella finestra di dialogo della barra degli strumenti. La `jcr:description` proprietà contiene ulteriori informazioni che vengono visualizzate quando un utente passa il puntatore sull&#39;azione.

   ![Gerarchia dei nodi per la personalizzazione della barra degli strumenti](assets/action3.png)

1. Selezionare `cq:template` il nodo nel `reviewbeforesubmit` nodo. Assicurarsi che il valore della `guideNodeClass` proprietà sia `guideButton` e modificare di conseguenza la `jcr:title` proprietà.
1. Modificare la proprietà type nel `cq:Template` nodo. Per l&#39;esempio corrente, modificare la proprietà type in button.

   Il valore type viene aggiunto come classe CSS nel codice HTML generato per il componente. Gli utenti possono utilizzare la classe CSS per definire lo stile delle proprie azioni. Lo stile predefinito per i dispositivi mobili e desktop è disponibile per i valori di pulsante, invio, ripristino e salvataggio.

1. Selezionare l&#39;azione personalizzata dalla finestra di dialogo della barra degli strumenti per la modifica di moduli adattivi. Nella barra degli strumenti del pannello viene visualizzato il pulsante Revisione.

   ![L&#39;azione personalizzata è disponibile nella barra degli strumenti](assets/custom_action_available_in_toolbar.png) ![Visualizza l&#39;azione personalizzata della barra degli strumenti](assets/action7.png)

1. Per fornire funzionalità al pulsante Review, aggiungete codice JavaScript e CSS e codice lato server nel file init.jsp, presente all&#39;interno del `reviewbeforesubmit` nodo.

   Aggiungi il seguente codice in `init.jsp`.

   ```jsp
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <guide:initializeBean name="guideField" className="com.adobe.aemds.guide.common.GuideButton"/>
   
   <c:if test="${not isEditMode}">
           <cq:includeClientLib categories="reviewsubmitclientlibruntime" />
   </c:if>
   
   <%--- BootStrap Modal Dialog  --------------%>
   <div class="modal fade" id="reviewSubmit" tabindex="-1">
       <div class="modal-dialog">
           <div class="modal-content">
               <div class="modal-header">
                   <h3>Review the Form Fields</h3>
               </div>
               <div class="modal-body">
                   <div class="modal-list">
                       <table class="table table-bordered">
                           <tr class="name">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Name is: </label>
                               </td>
                           </tr>
                           <tr class="pan">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Pan Number is: </label>
                               </td>
                           </tr>
                           <tr class="dob">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Date Of Birth is: </label>
                               </td>
                           </tr>
                           <tr class="80cdeclaration">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Total 80C Declaration Amount is: </label>
                               </td>
                           </tr>
                           <tr class="rentpaid">
                               <td class="reviewlabel col-md-3 active">
                                   <label>Your Total HRA Amount is: </label>
                               </td>
                           </tr>
                       </table>
                   </div>
               </div><!-- /.modal-body -->
               <div class="modal-footer">
                   <div class="fileAttachmentListingCloseButton col-md-2 col-xs-2 col-sm-2">
                       <button data-dismiss="modal">Close</button>
                   </div>
               </div>
           </div><!-- /.modal-content -->
       </div><!-- /.modal-dialog -->
   </div><!-- /.modal -->
   ```

   Aggiungi il codice seguente nel `ReviewBeforeSubmit.js` file.

   ```javascript
   /*anonymous function to handle show of review before submit view */
   $(function () {
       if($("div.reviewbeforesubmit button[id*=reviewbeforesubmit]").length > 0) {
           $("div.reviewbeforesubmit button[id*=reviewbeforesubmit]").click(function(){
               // Create the options object to be passed to the getElementProperty API
               var options = {},
                   result = [];
               options.somExpressions = [];
               options.propertyName = "value";
               guideBridge.visit(function(model){
                   if(model.name === "name" || model.name === "pan" || model.name === "dateofbirth" || model.name === "total" || model.name === "totalmonthlyrent"){
                           options.somExpressions.push(model.somExpression);
                   }
               }, this);
               result = guideBridge.getElementProperty(options);
   
               $('#reviewSubmit .reviewlabel').each(function(index, item){
                   var data = ((result.data[index] == null) ? "No Data Filled" : result.data[index]);
                   if($(this).next().hasClass("reviewlabelvalue")){
                       $(this).next().html(data);
                   } else {
                       $(this).after($("<td></td>").addClass("reviewlabelvalue col-md-6 active").html(data));
                   }
               });
               // added because in mobile devices it was causing problem of backdrop
               $("#reviewSubmit").appendTo('body');
               $("#reviewSubmit").modal("show");
           });
       }
   });
   ```

   Aggiungi il codice seguente al `ReviewBeforeSubmit.css` file.

   ```css
   .modal-list .reviewlabel {
       white-space: normal;
       text-align: right;
       padding:2px;
   }
   
   .modal-list .reviewlabelvalue {
       border: #cde0ec 1px solid;
       padding:2px;
   }
   
   /* Adding icon for this action in mobile devices */
   /* This is the glyphicon provided by bootstrap eye-open */
   /* .<type> .iconButton-icon */
   .reviewbeforesubmit .iconButton-icon {
       position: relative;
       top: -8px;
       font-family: 'Glyphicons Halflings';
       font-style: normal;
   }
   
   .reviewbeforesubmit .iconButton-icon:before {
       content: "\e105"
   }
   ```

1. Per verificare la funzionalità dell’azione personalizzata, aprire il modulo adattivo in modalità Anteprima e fare clic su Rivedi nella barra degli strumenti.

   >[!NOTE]
   >
   >La `GuideBridge` libreria non viene caricata in modalità di creazione. Questa azione personalizzata non funziona quindi in modalità di authoring.

   ![Dimostrazione dell&#39;azione del pulsante di revisione personalizzato](assets/action9.png)

## Esempi {#samples}

Il seguente archivio contiene un pacchetto di contenuti. Il pacchetto include un modulo adattivo correlato alla dimostrazione sopra riportata dell’azione personalizzata per la barra degli strumenti.

[Ottieni file](assets/customtoolbaractiondemo.zip)
