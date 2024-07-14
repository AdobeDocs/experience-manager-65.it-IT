---
title: Creazione di un'azione personalizzata sulla barra degli strumenti
description: Gli sviluppatori di moduli possono creare azioni della barra degli strumenti personalizzate per i moduli adattivi in AEM Forms. L’utilizzo di azioni personalizzate da parte degli autori di moduli può fornire più flussi di lavoro e opzioni ai loro utenti finali.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
exl-id: 17f7f0e1-09d8-45cd-a4f6-0846bdb079b6
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Foundation Components
source-git-commit: 8a77756e8ba771c8de9950c2323bef8f23cc59b4
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---

# Creazione di un&#39;azione personalizzata sulla barra degli strumenti{#creating-a-custom-toolbar-action}

## Prerequisiti {#prerequisite}

Prima di creare un&#39;azione personalizzata della barra degli strumenti, è necessario conoscere [Utilizzo delle librerie lato client](/help/sites-developing/clientlibs.md) e [Sviluppo con CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

## Che cos’è un’azione {#what-is-an-action-br}

Un modulo adattivo fornisce una barra degli strumenti che consente all’autore del modulo di configurare un set di opzioni. Queste opzioni sono definite come azioni per il modulo adattivo. Fai clic sul pulsante Modifica nella barra degli strumenti del pannello per impostare le azioni supportate dai moduli adattivi.

![Azioni barra degli strumenti predefinite](assets/default_toolbar_actions.png)

Oltre al set di azioni fornito per impostazione predefinita, nella barra degli strumenti puoi creare azioni personalizzate. Ad esempio, puoi aggiungere un’azione per consentire all’utente di rivedere tutti i campi del modulo adattivo prima dell’invio di un modulo.

## Passaggi per creare un’azione personalizzata in un modulo adattivo {#steps}

Per illustrare la creazione di un’azione personalizzata nella barra degli strumenti, i passaggi seguenti ti guidano a creare un pulsante che consenta agli utenti finali di esaminare tutti i campi del modulo adattivo prima di inviare un modulo compilato.

1. Tutte le azioni predefinite supportate dai moduli adattivi sono presenti nella cartella `/libs/fd/af/components/actions`. In CRXDE, copiare il nodo `fileattachmentlisting` da `/libs/fd/af/components/actions/fileattachmentlisting` a `/apps/customaction`.

1. Dopo aver copiato il nodo nella cartella `apps/customaction`, rinominare il nome del nodo in `reviewbeforesubmit`. Inoltre, modificare le proprietà `jcr:title` e `jcr:description` del nodo.

   La proprietà `jcr:title` contiene il nome dell&#39;azione visualizzata nella finestra di dialogo della barra degli strumenti. La proprietà `jcr:description` contiene ulteriori informazioni visualizzate quando un utente passa il puntatore del mouse sull&#39;azione.

   ![Gerarchia di nodi per la personalizzazione della barra degli strumenti](assets/action3.png)

1. Selezionare il nodo `cq:template` nel nodo `reviewbeforesubmit`. Verificare che il valore della proprietà `guideNodeClass` sia `guideButton` e modificare di conseguenza la proprietà `jcr:title`.
1. Modificare la proprietà del tipo nel nodo `cq:Template`. Nell&#39;esempio corrente, modificare la proprietà type in button.

   Il valore del tipo viene aggiunto come classe CSS nel HTML generato per il componente. Gli utenti possono utilizzare tale classe CSS per assegnare uno stile alle proprie azioni. Lo stile predefinito per i dispositivi mobili e desktop viene fornito per i valori dei tipi di pulsante, invio, reimpostazione e salvataggio.

1. Seleziona l’azione personalizzata dalla finestra di dialogo della barra degli strumenti di modifica del modulo adattivo. Nella barra degli strumenti del pannello viene visualizzato un pulsante Rivedi.

   ![L&#39;azione personalizzata è disponibile nella barra degli strumenti](assets/custom_action_available_in_toolbar.png) ![Visualizzazione dell&#39;azione della barra degli strumenti creata dall&#39;utente](assets/action7.png)

1. Per fornire funzionalità al pulsante Review, aggiungere codice JavaScript e CSS e codice lato server nel file init.jsp, presente nel nodo `reviewbeforesubmit`.

   Aggiungere il codice seguente in `init.jsp`.

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

   Aggiungere il codice seguente nel file `ReviewBeforeSubmit.js`.

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

   Aggiungere il codice seguente al file `ReviewBeforeSubmit.css`.

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

1. Per verificare la funzionalità dell’azione personalizzata, apri il modulo adattivo in modalità Anteprima e fai clic su Revisione nella barra degli strumenti.

   >[!NOTE]
   >
   >La libreria `GuideBridge` non è caricata in modalità di creazione. Pertanto, questa azione personalizzata non funziona nella modalità di authoring.

   ![Dimostrazione dell&#39;azione del pulsante di revisione personalizzato](assets/action9.png)

## Esempi {#samples}

Il seguente archivio contiene un pacchetto di contenuti. Il pacchetto include un modulo adattivo relativo alla demo di cui sopra per l’azione personalizzata della barra degli strumenti.

[Ottieni file](assets/customtoolbaractiondemo.zip)
