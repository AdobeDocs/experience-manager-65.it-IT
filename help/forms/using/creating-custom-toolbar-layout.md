---
title: Creazione del layout personalizzato della barra degli strumenti
description: È possibile specificare un layout di barra degli strumenti per il modulo. Il layout della barra degli strumenti definisce i comandi e il layout della barra degli strumenti nel modulo.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
exl-id: 44516956-00aa-41d5-a7e9-746c7618e5db
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---

# Creazione del layout personalizzato della barra degli strumenti{#creating-custom-toolbar-layout}

## Layout della barra degli strumenti {#layout}

Quando si crea un modulo adattivo, è possibile specificare un layout della barra degli strumenti per il modulo. Il layout della barra degli strumenti definisce i comandi e il layout della barra degli strumenti nel modulo.

Il layout della barra degli strumenti utilizza in larga misura l’elaborazione lato client guidata da codice JavaScript e CSS complesso. L’organizzazione e l’ottimizzazione della trasmissione di questo codice possono essere un problema complesso. Per risolvere questo problema, AEM fornisce Cartelle libreria lato client, che consentono di memorizzare il codice lato client nell’archivio, organizzarlo in categorie e definire quando e come ogni categoria di codice deve essere trasmessa al client. Il sistema di librerie lato client si occupa quindi di generare i collegamenti corretti nella pagina web finale per caricare il codice corretto. Per informazioni dettagliate, consulta [Funzionamento delle librerie lato client nell’AEM.](/help/sites-developing/clientlibs.md)

![Layout di esempio della barra degli strumenti](assets/default_toolbar_layout.png)

Layout di esempio della barra degli strumenti

I moduli adattivi forniscono una serie di layout predefiniti:

![Layout della barra degli strumenti disponibili ](assets/toolbar1.png)

Layout della barra degli strumenti disponibili

È inoltre possibile creare un layout personalizzato per le barre degli strumenti.

Nella procedura seguente vengono descritti i passaggi necessari per creare una barra degli strumenti personalizzata che visualizzi tre azioni nella barra degli strumenti e le altre azioni in un elenco a discesa nella barra degli strumenti.

Il pacchetto di contenuti allegato contiene l’intero codice descritto di seguito. Dopo aver installato il pacchetto di contenuti, apri `/content/forms/af/CustomLayoutDemo.html` per visualizzare la demo del layout personalizzato della barra degli strumenti.

CustomToolbarLayoutDemo.zip

[Ottieni file](assets/customtoolbarlayoutdemo.zip)
Layout della barra degli strumenti personalizzata demo

## Per creare un layout personalizzato per le barre degli strumenti {#layout-1}

1. Crea una cartella per mantenere i layout personalizzati della barra degli strumenti. Ad esempio:

   `/apps/customlayout/toolbar`.

   Per creare un layout personalizzato, puoi utilizzare (e personalizzare) uno dei layout predefiniti della barra degli strumenti disponibili nella cartella seguente:

   `/libs/fd/af/layouts/toolbar`

   Ad esempio, copia il `mobileFixedToolbarLayout` nodo da `/libs/fd/af/layouts/toolbar` cartella al `/apps/customlayout/toolbar` cartella.

   Inoltre, copia toolbarCommon.jsp in `/apps/customlayout/toolbar` cartella.

   >[!NOTE]
   >
   >La cartella creata per mantenere i layout personalizzati può essere creata con `apps` cartella.

1. Rinomina il nodo copiato, `mobileFixedToolbarLayout`, a `customToolbarLayout.`

   Inoltre, fornisci una descrizione rilevante per il nodo. Ad esempio, modificare jcr:description del nodo in **Layout personalizzato per la barra degli strumenti**.

   Il `guideComponentType` del nodo determina il tipo di layout. In questo caso, il tipo di layout è barra degli strumenti e viene quindi visualizzato nel menu a discesa per la selezione del layout della barra degli strumenti.

   ![Un nodo con descrizione pertinente](assets/toolbar3.png)

   Un nodo con descrizione pertinente

   Il nuovo layout personalizzato della barra degli strumenti viene visualizzato nel **Barra degli strumenti del modulo adattivo** configurazione della finestra di dialogo.

   ![Elenco dei layout di barra degli strumenti disponibili](assets/toolbar4.png)

   Elenco dei layout di barra degli strumenti disponibili

   >[!NOTE]
   >
   >La descrizione aggiornata nel passaggio precedente viene visualizzata nell’elenco a discesa Layout.

1. Selezionare il layout personalizzato della barra degli strumenti e fare clic su OK.

   Aggiungere clientlib (javascript e css) nel `/etc/customlayout` e include il riferimento della libreria client nel `customToolbarLayout.jsp`.

   ![Percorso del file customToolbarLayout.css](assets/toolbar_3.png)

   Percorso del file customToolbarLayout.css

   Esempio `customToolbarLayout.jsp`:

   ```jsp
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <cq:includeClientLib categories="customtoolbarlayout" />
   <c:if test="${isEditMode}">
           <cq:includeClientLib categories="customtoolbarlayoutauthor" />
   </c:if>
   <div class="guidetoolbar mobileToolbar mobilecustomToolbar" data-guide-position-class="guide-element-hide">
       <div data-guide-scroll-indicator="true"></div>
       <%@include file="../toolbarCommon.jsp" %>
   </div>
   ```

   >[!NOTE]
   >
   >Aggiungere la classe guidetoolbar per il layout. Lo stile predefinito della barra degli strumenti è definito rispetto alla classe guidetoolbar.

   Esempio `toolBarCommon.jsp`:

   ```jsp
   <%@taglib prefix="fn" uri="https://java.sun.com/jsp/jstl/functions"%>
   <%--------------------
   This code iterates over all the tool bar items using the guideToolbar bean.
   If the number of toolbar items are more than 3, then we create a dropdown menu using bootstrap for other actions present in the toolbar.
   In both desktop and mobile devices, the layout is different.
   ---------------------------------%>
   
   <c:forEach items="${guideToolbar.items}" var="toolbarItem" varStatus="loop">
       <c:choose>
         <c:when test="${loop.index gt 2}">
      <c:choose>
       <c:when test="${loop.index eq 3}">
                     <div class="btn-group dropdown">
                       <button type="button" class="btn btn-primary dropdown-toggle label" data-toggle="dropdown">Actions <span class="caret"></code></button>
                       <button type="button" class="btn btn-primary dropdown-toggle icon" data-toggle="dropdown"><span class="glyphicon glyphicon-th-list"></code></button>
             <ul class="dropdown-menu" role="menu">
                           <li>
                               <div id="${toolbarItem.id}_guide-item">
                                 <sling:include path="${toolbarItem.path}" resourceType="${toolbarItem.resourceType}"/>
                              </div>
                           </li>
                           <c:if test="${loop.index eq (fn:length(guideToolbar.items)-1)}">
                                </ul>
                                </div>
                           </c:if>
       </c:when>
       <c:when test="${loop.index eq (fn:length(guideToolbar.items)-1)}">
                          <li>
                                     <div id="${toolbarItem.id}_guide-item">
                                         <sling:include path="${toolbarItem.path}" resourceType="${toolbarItem.resourceType}"/>
                                     </div>
                           </li>
                       </ul>
                     </div>
   
       </c:when>
       <c:otherwise>
         <li>
          <div id="${toolbarItem.id}_guide-item">
           <sling:include path="${toolbarItem.path}" resourceType="${toolbarItem.resourceType}"/>
          </div>
         </li>
       </c:otherwise>
      </c:choose>
         </c:when>
         <c:otherwise>
     <div id="${toolbarItem.id}_guide-item">
           <sling:include path="${toolbarItem.path}" resourceType="${toolbarItem.resourceType}"/>
        </div>
         </c:otherwise>
    </c:choose>
   </c:forEach>
   ```

   Il CSS presente all’interno del nodo clientlib:

   ```css
   .mobilecustomToolbar .dropdown {
       display: inline-block;
   }
   
   .mobilecustomToolbar .dropdown {
       float: right;
   }
   
   .mobilecustomToolbar .dropdown > button {
      padding: 6px 12px;
   }
   
   .mobilecustomToolbar .dropdown .guideFieldWidget, .mobilecustomToolbar .dropdown .guideFieldWidget button {
       width: 100%;
   }
   
   .mobilecustomToolbar .dropdown .caret{
       border-bottom: 6px solid;
       border-right: 6px solid transparent;
       border-left: 6px solid transparent;
    border-top: transparent;
   }
   
   .mobilecustomToolbar .dropdown-menu{
    top: auto;
    bottom: 100%;
   }
   
   .mobilecustomToolbar .btn-group {
    vertical-align: super;
   }
   
   .mobilecustomToolbar .glyphicon {
    font-size: 24px;
   }
   
   @media (max-width: 767px){
   
    .mobilecustomToolbar .dropdown .guideButton .iconButton-icon {
      display: none;
       }
   
       .mobilecustomToolbar .dropdown .guideButton .iconButton-label {
      display: inline-block;
       }
   
       .mobilecustomToolbar .dropdown .guideButton button {
      background-color: #013853;
       }
   
    .mobilecustomToolbar .btn-group {
     vertical-align: top;
    }
   
   }
   ```

>[!NOTE]
>
>La descrizione aggiornata nel passaggio precedente viene visualizzata nell’elenco a discesa Layout.

![Vista desktop della barra degli strumenti di layout personalizzato](assets/toolbar_1.png)

Vista desktop della barra degli strumenti di layout personalizzato
