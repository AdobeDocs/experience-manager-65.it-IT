---
title: Integrazione di Form Bridge con il portale personalizzato per i moduli HTML5
seo-title: Integrazione di Form Bridge con il portale personalizzato per i moduli HTML5
description: È possibile utilizzare l’API FormBridge per ottenere o impostare i valori dei campi del modulo dalla pagina HTML e inviare il modulo.
seo-description: È possibile utilizzare l’API FormBridge per ottenere o impostare i valori dei campi del modulo dalla pagina HTML e inviare il modulo.
uuid: c8911f82-1a25-47a5-9a06-19b5dce74a2c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bd9bf095-d74d-458c-afe7-fab04050849d
docset: aem65
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---


# Integrazione di Form Bridge con il portale personalizzato per i moduli HTML5{#integrating-form-bridge-with-custom-portal-for-html-forms}

FormBridge è un’API di bridge per moduli HTML5 che consente di interagire con un modulo. Per il riferimento API FormBridge, vedere [Riferimento API FormBridge](/help/forms/using/form-bridge-apis.md).

È possibile utilizzare l’API FormBridge per ottenere o impostare i valori dei campi del modulo dalla pagina HTML e inviare il modulo. Ad esempio, puoi utilizzare l’API per creare un’esperienza simile alla procedura guidata.

Un’applicazione HTML esistente può utilizzare l’API FormBridge per interagire con un modulo e incorporarlo nella pagina HTML. Per impostare il valore di un campo utilizzando l’API Form Bridge, è possibile effettuare le seguenti operazioni.

## Integrazione dei moduli HTML5 in una pagina web {#integrating-html-forms-to-a-web-page}

1. **Scegli un profilo o crea un profilo**

   1. Nell&#39;interfaccia CRX DE, passa a: `https://'[server]:[port]'/crx/de`.
   1. Accedi con le credenziali di amministratore.
   1. Crea un profilo o scegli un profilo esistente.

      Per informazioni dettagliate su come creare un profilo, consulta [Creazione di un nuovo profilo](/help/forms/using/custom-profile.md).

1. **Modificare il profilo HTML**

   Includi runtime XFA, libreria locale XFA e snippet HTML del modulo XFA nel modulo di rendering del profilo, progetta la pagina web e inserisci il modulo nella pagina web.

   Ad esempio, utilizza il seguente frammento di codice per creare un’app con due campi di input e un modulo per illustrare l’interazione tra il modulo e un’app esterna.

   ```xml
   <%@ page session="false"
                  contentType="text/html; charset=utf-8"%><%
   %><%@ taglib prefix="cq" uri="https://www.day.com/taglibs/cq/1.0" %><%
   %><!DOCTYPE html>
   <html manifest="${param.offlineSpec}">
       <head>
          <cq:include script="formRuntime.jsp"/>
           <!-- Portal Scripts and Styles -->
          <cq:include script="portalheader.jsp"/>
       </head>
       <body>
           <div id="leftdiv" >
               <div id="leftdivcontentarea">
                   <!-- Portal Body -->
                 <cq:include script="portalbody.jsp"/>
               </div>
           </div>
           <div id="rightdiv">
               <div id="formBody">
               <cq:include script="config.jsp"/>
               <!-- Form body -->
               <cq:include script="formBody.jsp"/>
               <!  --To assist in page transitions -- add navigation, based on scrolling -->
               <cq:include  script="../nav/scroll/nav_footer.jsp"/>
               <cq:include script="footer.jsp"/>
               </div>
           </div>
       </body>
   </html>
   ```

   >[!NOTE]
   >
   >La **riga 9** contiene riferimenti JSP aggiuntivi per gli stili CSS e i file JavaScript per la progettazione della pagina.
   >
   >
   >Il tag &lt;div id=&quot;rightdiv&quot;> sulla riga 18 **contiene lo snippet HTML del modulo XFA.**
   La pagina è formattata in due contenitori: **sinistra** e **destra**. Il contenitore di destra contiene il modulo. Il contenitore sinistro ha due campi di input e parte della pagina HTML esterna.
   La seguente schermata mostra come viene visualizzato il modulo in un browser.

   ![portale](assets/portal.jpg)

   Il lato sinistro fa parte della **pagina HTML**. Il lato destro contenente i campi è il **modulo xfa**.

1. **Accesso ai campi del modulo dalla pagina**

   Di seguito è riportato uno script di esempio che è possibile aggiungere per impostare valori in un campo modulo.

   Ad esempio, se desideri impostare il **NomeDipendente** utilizzando i valori nei campi **Nome** e **Cognome**, chiama la funzione **window.formBridge.setFieldValue** .

   Allo stesso modo, è possibile leggere il valore chiamando l&#39;API **window.formBridge.getFieldValue** .

   ```javascript
   $(function() {
               $(".input").blur(function() {
                   window.formBridge.setFieldValue(
                               'xfa.form.form1.#subform[0].EmployeeName',
                                $("#lname").val()+' '+$("#fname").val()
                              )
                   });
           });
   ```
