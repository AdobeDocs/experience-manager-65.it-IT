---
title: Creazione di componenti di layout personalizzati per i moduli adattivi
seo-title: Creating custom layout components for adaptive forms
description: Procedura per creare componenti di layout personalizzati per i moduli adattivi.
seo-description: Procedure to create custom layout components for adaptive forms.
uuid: f0bb5fcd-3938-4804-ad0c-d96d3083fd01
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: d4ae432d-557d-4e89-92b8-dca5f37cb6f8
docset: aem65
exl-id: 544b06f9-2456-4c05-88c2-b5349947742d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 1%

---

# Creazione di componenti di layout personalizzati per i moduli adattivi{#creating-custom-layout-components-for-adaptive-forms}

## Prerequisito {#prerequisite}

Conoscenza dei layout, che consente di creare/utilizzare un layout personalizzato. Vedi [Modifica del layout del pannello](../../forms/using/layout-capabilities-adaptive-forms.md).

## Componente Layout del pannello dei moduli adattivo {#adaptive-form-panel-layout-component}

Il componente Layout del pannello dei moduli adattivi controlla il modo in cui i componenti dei moduli adattivi vengono disposti in un pannello relativo all’interfaccia utente.

## Creazione di un layout di pannello personalizzato {#creating-a-custom-panel-layout}

1. Passa alla posizione `/crx/de`.
1. Copiare un layout di un pannello dalla posizione `/libs/fd/af/layouts/panel` (ad esempio, `tabbedPanelLayout`) a `/apps` (ad esempio, `/apps/af-custom-layout`).
1. Rinomina il layout copiato in `customPanelLayout`. Modificare le proprietà dei nodi `qtip` e `jcr:description`. Ad esempio, modificali in `Custom layout - Toggle tabs`.

suggerimento

![Snapshot CRX DE layout del pannello personalizzato](assets/custom_layout_new.png)

>[!NOTE]
>
>Impostazione della proprietà `guideComponentType`al valore `fd/af/layouts/panel` determina che il layout è un layout a pannello.

1. Rinomina il file `tabbedPanelLayout.jsp` sotto il nuovo layout a customPanelLayout.jsp.
1. Per introdurre nuovi stili e comportamenti, crea una libreria client nella sezione `etc` nodo. Ad esempio, nel percorso /etc/af-custom-layout-clientlib, crea il nodo client-library. Consenti al nodo di avere la proprietà categories af.panel.custom. Contiene i seguenti file .css e .js:

   ```css
   /** CSS defining new styles used by custom layout **/
   
   .menu-nav {
       background-color: rgb(198, 38, 76);
       height: 30px;
    width: 30px;
    font-size: 2em;
    color: white;
       -webkit-transition: -webkit-transform 1s;  /* For Safari 3.1 to 6.0 */
    transition: transform 1s;
   }
   
   .tab-content {
    border: 1px solid #08b1cf;
   }
   
   .custom-navigation {
       -webkit-transition: width 1s, height 1s, -webkit-transform 1s;  /* For Safari 3.1 to 6.0 */
    transition: width 1s, height 1s, transform 1s;
   }
   
   .panel-name {
       padding-left: 30px;
       font-size: 20px;
   }
   
   @media (min-width: 992px) {
    .nav-close {
     width: 0px;
       }
   }
   
   @media (min-width: 768px) and (max-width: 991px) {
    .nav-close {
     height: 0px;
       }
   }
   
   @media (max-width: 767px) {
    .menu-nav, .custom-navigation {
        display: none;
       }
   }
   ```

   ```javascript
   /** function for toggling the navigators **/
   var toggleNav = function () {
   
       var nav = $('.custom-navigation');
       if (nav) {
           nav.toggleClass('nav-close');
       }
   }
   
   /** function to populate the panel title **/
   $(window).on('load', function() {
       if (window.guideBridge) {
           window.guideBridge.on("elementNavigationChanged",
           function (evntName, evnt) {
                       var activePanelSom = evnt.newText,
                           activePanel = window.guideBridge._guideView.getView(activePanelSom);
                       $('.panel-name').html(activePanel.$itemNav.find('a').html());
                   }
           );
       }
   });
   ```

1. Per migliorare l’aspetto e il comportamento, puoi includere `client library`.

   Inoltre, aggiorna i percorsi degli script inclusi nei file .jsp. Ad esempio, aggiorna il `customPanelLayout.jsp` file come segue:

   ```html
   <%-- jsp encapsulating navigator container and panel container divs --%>
   
   <%@include file="/libs/fd/af/components/guidesglobal.jsp"%>
   <cq:includeClientLib categories="af.panel.custom"/>
   <div>
       <div class="row">
           <div class="col-md-2 col-sm-2 hidden-xs menu-nav glyphicon glyphicon-align-justify" onclick="toggleNav();"></div>
           <div class="col-md-10 col-sm-10 hidden-xs panel-name"></div>
       </div>
       <div class="row">
           <div class="col-md-2 hidden-xs guide-tab-stamp-list custom-navigation">
               <cq:include script = "/apps/af-custom-layout/customPanelLayout/defaultNavigatorLayout.jsp" />
           </div>
           <div  class="col-md-10">
               <c:if test="${fn:length(guidePanel.description) > 0}">
                   <div class="<%=GuideConstants.GUIDE_PANEL_DESCRIPTION%>">
                       ${guide:encodeForHtml(guidePanel.description,xssAPI)}
                           <cq:include script="/libs/fd/af/components/panel/longDescription.jsp"/>
                   </div>
               </c:if>
               <cq:include script = "/apps/af-custom-layout/customPanelLayout/panelContainer.jsp"/>
           </div>
       </div>
   </div>
   ```

   La `/apps/af-custom-layout/customPanelLayout/defaultNavigatorLayout.jsp` file:

   ```html
   <%-- jsp governing the navigation part --%>
   
   <%@include file="/libs/fd/af/components/guidesglobal.jsp"%>
   <%@ page import="com.adobe.aemds.guide.utils.StyleUtils" %>
   <%-- navigation tabs --%>
   <ul id="${guidePanel.id}_guide-item-nav-container" class="tab-navigators tab-navigators-vertical in"
       data-guide-panel-edit="reorderItems" role="tablist">
       <c:forEach items="${guidePanel.items}" var="panelItem">
           <c:set var="isNestedLayout" value="${guide:hasNestablePanelLayout(guidePanel,panelItem)}"/>
           <li id="${panelItem.id}_guide-item-nav" title="${guide:encodeForHtmlAttr(panelItem.navTitle,xssAPI)}" data-path="${panelItem.path}" role="tab" aria-controls="${panelItem.id}_guide-item">
               <c:set var="panelItemCss" value="${panelItem.cssClassName}"/>
               <% String panelItemCss = (String) pageContext.getAttribute("panelItemCss");%>
               <a data-guide-toggle="tab" class="<%= StyleUtils.addPostfixToClasses(panelItemCss, "_nav") %> guideNavIcon nested_${isNestedLayout}">${guide:encodeForHtml(panelItem.navTitle,xssAPI)}</a>
               <c:if test="${isNestedLayout}">
                   <guide:initializeBean name="guidePanel" className="com.adobe.aemds.guide.common.GuidePanel"
                       resourcePath="${panelItem.path}" restoreOnExit="true">
                       <sling:include path="${panelItem.path}"
                                      resourceType="/apps/af-custom-layout/customPanelLayout/defaultNavigatorLayout.jsp"/>
                   </guide:initializeBean>
               </c:if>
               <em></em>
           </li>
       </c:forEach>
   </ul>
   ```

   Il `/apps/af-custom-layout/customPanelLayout/panelContainer.jsp`:

   ```html
   <%-- jsp governing the panel content --%>
   
   <%@include file="/libs/fd/af/components/guidesglobal.jsp"%>
   
   <div id="${guidePanel.id}_guide-item-container" class="tab-content">
       <c:if test="${guidePanel.hasToolbar && (guidePanel.toolbarPosition == 'Top') }">
           <sling:include path="${guidePanel.toolbar.path}"/>
       </c:if>
   
   <c:forEach items="${guidePanel.items}" var="panelItem">
       <div class="tab-pane" id="${panelItem.id}_guide-item" role="tabpanel">
           <c:set var="isNestedLayout" value="${guide:hasNestablePanelLayout(guidePanel,panelItem)}"/>
           <c:if test="${isNestedLayout}">
               <c:set var="guidePanelResourceType" value="/apps/af-custom-layout/customPanelLayout/panelContainer.jsp" scope="request"/>
           </c:if>
           <sling:include path="${panelItem.path}" resourceType="${panelItem.resourceType}"/>
       </div>
   </c:forEach>
   <c:if test="${guidePanel.hasToolbar && (guidePanel.toolbarPosition == 'Bottom')}">
       <sling:include path="${guidePanel.toolbar.path}"/>
   </c:if>
   </div>
   ```

1. Apri un modulo adattivo in modalità Creazione. Il layout del pannello definito viene aggiunto all’elenco per la configurazione dei layout dei pannelli.

   ![Il layout del pannello personalizzato viene visualizzato nell’elenco del layout del pannello](assets/auth-layt.png) ![Schermata del modulo adattivo, con layout personalizzato del pannello](assets/s1.png) ![Schermata che mostra la funzionalità di attivazione/disattivazione del layout personalizzato](assets/s2.png)

ZIP di esempio per un layout di pannello personalizzato e un modulo adattivo che lo utilizza.

[Ottieni file](assets/af-custom-layout.zip)
