---
title: Integrazione di Form Bridge con portale personalizzato per HTML5 Forms
description: È possibile utilizzare l’API FormBridge per ottenere o impostare i valori dei campi modulo dalla pagina HTML e inviare il modulo.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms
exl-id: 89118bb8-6ec8-4048-b3d6-5c73a9eea33e
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 0%

---

# Integrazione di Form Bridge con portale personalizzato per HTML5 Forms{#integrating-form-bridge-with-custom-portal-for-html-forms}

FormBridge è un’API bridge di HTML5 forms che consente di interagire con un modulo. Per informazioni di riferimento sull’API di FormBridge, consulta [Riferimento API di FormBridge](/help/forms/using/form-bridge-apis.md).

È possibile utilizzare l’API FormBridge per ottenere o impostare i valori dei campi modulo dalla pagina HTML e inviare il modulo. Ad esempio, puoi utilizzare l’API per creare un’esperienza simile a una procedura guidata.

Un’applicazione HTML esistente può utilizzare l’API FormBridge per interagire con un modulo e incorporarlo nella pagina HTML. Puoi utilizzare i seguenti passaggi per impostare il valore di un campo utilizzando l’API Bridge modulo.

## Integrazione di moduli HTML5 in una pagina web {#integrating-html-forms-to-a-web-page}

1. **Scegli un profilo o creane uno**

   1. Nell’interfaccia CRX DE, passa a: `https://'[server]:[port]'/crx/de`.
   1. Accedi con le credenziali di amministratore.
   1. Crea un profilo o scegli un profilo esistente.

      Per informazioni dettagliate su come creare un profilo, consulta [Creazione di un profilo](/help/forms/using/custom-profile.md).

1. **Modificare il profilo di HTML**

   Include il runtime XFA, la libreria locale XFA e lo snippet di HTML del modulo XFA nel modulo di rendering dei profili, progetta la pagina web e inserisce il modulo all’interno della pagina web.

   Ad esempio, utilizza il seguente frammento di codice, per creare un’app con due campi di input e un modulo per dimostrare l’interazione tra il modulo e un’app esterna.

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
   >Il **riga 9**, contiene un riferimento JSP aggiuntivo per gli stili CSS e i file JavaScript per progettare la pagina.
   >
   >
   >Il &lt;div id=&quot;rightdiv&quot;> tag su **riga 18** contiene il frammento HTML del modulo XFA.
   >
   >
   Lo stile della pagina è suddiviso in due contenitori: **left** e **destra**. Il contenitore corretto contiene il modulo. Il contenitore sinistro dispone di due campi di input e fa parte della pagina HTML esterna.
   >
   >
   Nella schermata seguente viene illustrato come il modulo viene visualizzato in un browser.

   ![portale](assets/portal.jpg)

   Il lato sinistro fa parte del **Pagina HTML**. Il lato destro contenente i campi è il **modulo xfa**.

1. **Accesso ai campi modulo dalla pagina**

   Di seguito è riportato uno script di esempio che è possibile aggiungere per impostare i valori in un campo modulo.

   Ad esempio, se desideri impostare **NomeDipendente** utilizzo dei valori nei campi **Nome** e **Cognome**, chiama il **window.formBridge.setFieldValue** funzione.

   Allo stesso modo, puoi leggere il valore chiamando **window.formBridge.getFieldValue** API.

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
