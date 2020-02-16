---
title: Creazione di un layout della barra degli strumenti personalizzato
seo-title: Creazione di un layout della barra degli strumenti personalizzato
description: È possibile specificare un layout della barra degli strumenti per il modulo. Il layout della barra degli strumenti definisce i comandi e il layout della barra degli strumenti sul modulo.
seo-description: È possibile specificare un layout della barra degli strumenti per il modulo. Il layout della barra degli strumenti definisce i comandi e il layout della barra degli strumenti sul modulo.
uuid: 389a715a-4c91-4a63-895d-bb2d0f1054eb
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 0d817a7e-2758-4308-abda-6194716c2d97
docset: aem65
translation-type: tm+mt
source-git-commit: 76908a565bf9e6916db39d7db23c04d2d40b3247

---


# Creazione di un layout della barra degli strumenti personalizzato{#creating-custom-toolbar-layout}

## Layout della barra degli strumenti {#layout}

Quando si crea un modulo adattivo, è possibile specificare il layout di una barra degli strumenti per il modulo. Il layout della barra degli strumenti definisce i comandi e il layout della barra degli strumenti sul modulo.

Gli utilizzi del layout della barra degli strumenti dipendono in larga misura dall&#39;elaborazione sul lato client basata su codice JavaScript e CSS complessi. L&#39;organizzazione e l&#39;ottimizzazione della gestione di questo codice può essere un problema complicato. Per risolvere questo problema, AEM offre cartelle libreria lato client che consentono di archiviare il codice lato client nell’archivio, organizzarlo in categorie e definire quando e come ciascuna categoria di codice deve essere distribuita al client. Il sistema di libreria lato client si occupa quindi di generare i collegamenti corretti nella pagina Web finale per caricare il codice corretto. Per informazioni dettagliate, consultate [Funzionamento delle librerie lato client in AEM.](/help/sites-developing/clientlibs.md)

![Esempio di layout della barra degli strumenti](assets/default_toolbar_layout.png)

Esempio di layout della barra degli strumenti

I moduli adattivi forniscono una serie di layout predefiniti:

![Layout della barra degli strumenti disponibili ](assets/toolbar1.png)

Layout della barra degli strumenti disponibili

È inoltre possibile creare un layout personalizzato per la barra degli strumenti.

La procedura seguente illustra i passaggi necessari per creare una barra degli strumenti personalizzata in cui sono visualizzate tre azioni nella barra degli strumenti e le altre in un elenco a discesa nella barra degli strumenti.

Il pacchetto di contenuti allegato contiene l’intero codice descritto di seguito. Dopo aver installato il pacchetto di contenuti, aprite `/content/forms/af/CustomLayoutDemo.html` per visualizzare la demo del layout della barra degli strumenti personalizzata.

CustomToolbarLayoutDemo.zip

[Ottieni layout barra degli strumenti personalizzato](assets/customtoolbarlayoutdemo.zip)Demo

## Per creare un layout personalizzato della barra degli strumenti {#layout-1}

1. Create una cartella per mantenere i layout personalizzati della barra degli strumenti. Esempio:

   `/apps/customlayout/toolbar`.

   Per creare un layout personalizzato, potete utilizzare (e personalizzare) uno dei layout predefiniti della barra degli strumenti disponibili nella cartella seguente:

   `/libs/fd/af/layouts/toolbar`

   Ad esempio, copiate il `mobileFixedToolbarLayout` nodo dalla `/libs/fd/af/layouts/toolbar` cartella alla `/apps/customlayout/toolbar` cartella.

   Inoltre, copiate toolbarCommon.jsp nella `/apps/customlayout/toolbar` cartella.

   >[!NOTE]
   >
   >La cartella creata per mantenere i layout personalizzati molto da creare con la `apps` cartella.

1. Rinominare il nodo copiato in `mobileFixedToolbarLayout``customToolbarLayout.`

   Fornire inoltre una descrizione pertinente per il nodo. Ad esempio, modificare jcr:description del nodo in Layout **personalizzato per la barra degli strumenti**.

   Il tipo di layout è determinato dalla `guideComponentType` proprietà del nodo. In questo caso, il tipo di layout è barra degli strumenti, per cui viene visualizzato nel menu a discesa di selezione del layout della barra degli strumenti.

   ![Un nodo con la relativa descrizione](assets/toolbar3.png)

   Un nodo con la relativa descrizione

   Il nuovo layout della barra degli strumenti personalizzata viene visualizzato nella configurazione della finestra di dialogo della barra degli strumenti **modulo** adattiva.

   ![Elenco dei layout disponibili per le barre degli strumenti](assets/toolbar4.png)

   Elenco dei layout disponibili per le barre degli strumenti

   >[!NOTE]
   >
   >La descrizione aggiornata nel passaggio precedente viene visualizzata nell&#39;elenco a discesa Layout.

1. Selezionare il layout personalizzato della barra degli strumenti e fare clic su OK.

   Aggiungi clientlib (javascript e css) nel `/etc/customlayout` nodo e include il riferimento della clientlib nel `customToolbarLayout.jsp`.

   ![Percorso del file customToolbarLayout.css](assets/toolbar_3.png)

   Percorso del file customToolbarLayout.css

   Esempio `customToolbarLayout.jsp`:

   ```php
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
   >Aggiungete la classe guidetoolbar per il layout. Lo stile predefinito per la barra degli strumenti è definito in relazione alla classe guidetoolbar.

   Esempio `toolBarCommon.jsp`:

   ```php
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

   Il CSS presente nel nodo clientlib:

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
>La descrizione aggiornata nel passaggio precedente viene visualizzata nell&#39;elenco a discesa Layout.

![Vista desktop della barra degli strumenti del layout personalizzato](assets/toolbar_1.png)

Vista desktop della barra degli strumenti del layout personalizzato

