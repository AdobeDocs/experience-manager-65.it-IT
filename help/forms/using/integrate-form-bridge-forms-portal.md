---
title: Integrazione di Form Bridge con il portale personalizzato per i moduli HTML5
description: È possibile utilizzare l’API FormBridge per ottenere o impostare i valori dei campi modulo dalla pagina HTML e inviare il modulo.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 89118bb8-6ec8-4048-b3d6-5c73a9eea33e
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 4%
---
# Integrazione di Form Bridge con il portale personalizzato per i moduli HTML5{#integrating-form-bridge-with-custom-portal-for-html-forms}

FormBridge è un&#39;API bridge per HTML5 Forms che consente di interagire con un modulo. Per il riferimento all&#39;API FormBridge, vedere [Riferimento all&#39;API FormBridge](/help/forms/using/form-bridge-apis.md).

È possibile utilizzare l’API FormBridge per ottenere o impostare i valori dei campi modulo dalla pagina HTML e inviare il modulo. Ad esempio, puoi utilizzare l’API per creare un’esperienza simile a una procedura guidata.

Un’applicazione HTML esistente può utilizzare l’API FormBridge per interagire con un modulo e incorporarlo nella pagina HTML. Puoi utilizzare la procedura seguente per impostare il valore di un campo utilizzando l’API Bridge di Form.

## Integrazione di moduli HTML5 in una pagina web {#integrating-html-forms-to-a-web-page}

1. **Scegli un profilo o creane uno**

   1. Nell&#39;interfaccia di CRX DE, passare a: `https://'[server]:[port]'/crx/de`.
   1. Accedi con le credenziali di amministratore.
   1. Crea un profilo o scegli un profilo esistente.

      Per informazioni dettagliate su come creare un profilo, vedere [Creazione di un profilo](/help/forms/using/custom-profile.md).

1. **Modifica il profilo HTML**

   Includi il runtime XFA, la libreria locale XFA e lo snippet HTML del modulo XFA nel modulo di rendering dei profili, progetta la pagina web e inserisci il modulo all’interno della pagina web.

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
   >La **riga 9** contiene un riferimento JSP aggiuntivo per gli stili CSS e i file JavaScript per progettare la pagina.
   >
   >
   >Il tag &lt;div id=&quot;rightdiv&quot;> della **riga 18** contiene lo snippet HTML del modulo XFA.
   >
   >
   >Lo stile della pagina è in due contenitori: **left** e **right**. Il contenitore corretto contiene il modulo. Il contenitore sinistro dispone di due campi di input e fa parte della pagina HTML esterna.
   >
   >
   >Nella schermata seguente viene illustrato come il modulo viene visualizzato in un browser.

   ![portale](assets/portal.jpg)

   Il lato sinistro fa parte della **pagina HTML**. Il lato destro contenente i campi è il **modulo xfa**.

1. **Accesso ai campi modulo dalla pagina**

   Di seguito è riportato uno script di esempio che è possibile aggiungere per impostare i valori in un campo modulo.

   Ad esempio, se desideri impostare **NomeDipendente** utilizzando i valori dei campi **Nome** e **Cognome**, chiama la funzione **window.formBridge.setFieldValue**.

   Analogamente, è possibile leggere il valore chiamando l&#39;API **window.formBridge.getFieldValue**.

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
