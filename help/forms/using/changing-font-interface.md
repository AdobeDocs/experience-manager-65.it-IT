---
title: Modifica del font nell’interfaccia
seo-title: Changing the font on the interface
description: Come modificare selettivamente i font nell’interfaccia utente.
seo-description: How to change the fonts on the user interface selectively.
uuid: 421fdd24-441a-4092-8c52-f3ed3d5d5671
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 9fcb80b4-cbc2-48a5-afd1-4f3bc50bc503
docset: aem65
exl-id: 226f70f0-8eb4-4724-b496-5801dc6b436f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 1%

---

# Modifica del font nell’interfaccia{#changing-the-font-on-the-interface}

È possibile modificare il font visualizzato nell’area di lavoro di AEM Forms. I font utilizzati in una sezione specifica dell’interfaccia utente sono definiti nella sezione corrispondente del foglio di stile. È possibile modificare selettivamente i font nell’interfaccia utente.

Segui [Passaggi generici per la personalizzazione dell’area di lavoro AEM Forms](../../forms/using/generic-steps-html-workspace-customization.md) e, a seconda dei requisiti, segui i passaggi per personalizzare CSS, HTML o entrambi.

1. Modificare o aggiungere la famiglia di font in uno stile esistente.
1. Modifica o aggiungi il font-family in linea per l’elemento HTML.
1. Aggiungi uno stile e utilizzalo per l’elemento HTML.

Ad esempio, per modificare il font del testo di ancoraggio della barra di navigazione superiore in Courier New, effettua le seguenti operazioni:

1. Accedi a CRXDE Lite accedendo a `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Effettua una delle operazioni seguenti:

   1. Per modificare la famiglia di font in uno stile esistente, aggiungi quanto segue nel file newStyle.css in /apps/ws/css.

      ```css
      #topnav a {
         font-family: "Courier New";
      }
      ```

   1. Per aggiungere il font-family in linea per l’elemento HTML, copia il `/libs/ws/js/runtime/templates/appnavigation.html` file a `/apps/ws/js/runtime/templates/appnavigation.html`.

      Aggiorna il file /apps/ws/js/runtime/templates/appnavigation.html come segue:

      ```jsp
      <li class="process"><a href="#" title="<%= $.t('index.header.topnav.startprocess.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.startprocess.name')%></a></li>
      <li class="todo"><a href="#/todo" title="<%= $.t('index.header.topnav.todo.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.todo.name')%></a></li>
      <li class="track"><a href="#/tracking" title="<%= $.t('index.header.topnav.tracking.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.tracking.name')%></a></li>
      <li class="preference"><a href="#/preferences" title="<%= $.t('index.header.topnav.preferences.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.preferences.name')%></a></li>
      ```

      Apri il file /apps/ws/js/registry.js per la modifica e la sostituzione `text!/lc/libs/ws/js/runtime/templates/appnavigation.html` con `text!/lc/apps/ws/js/runtime/templates/appnavigation.html`.

   1. Per aggiungere uno stile che definisca la famiglia di font, aggiungi quanto segue nel file newStyle.css in /apps/ws/css.

      ```css
      .myNewFontStyle a {
         font-family: "Courier New";
      }
      ```

      Per aggiungere il font-family in linea per l’elemento HTML, aggiungi quanto segue nel file appnavigation.html in /apps/ws/js/runtime/templates.

      ```jsp
      <div id="topnav" class="myNewFontStyle">
          <ul>
              <li class="process"><a href="#" title="<%= $.t('index.header.topnav.startprocess.detail')%>" ><%= $.t('index.header.topnav.startprocess.name')%></a></li>
              <li class="todo"><a href="#/todo" title="<%= $.t('index.header.topnav.todo.detail')%>"><%= $.t('index.header.topnav.todo.name')%></a></li>
              <li class="track"><a href="#/tracking" title="<%= $.t('index.header.topnav.tracking.detail')%>" ><%= $.t('index.header.topnav.tracking.name')%></a></li>
              <li class="preference"><a href="#/preferences" title="<%= $.t('index.header.topnav.preferences.detail')%>" ><%= $.t('index.header.topnav.preferences.name')%></a></li>
          </ul>
      </div>
      ```

1. Riavvia l’area di lavoro e cancella la cache del browser per rendere visibili le modifiche.

![change_font_before](assets/change_font_before.png)

Barra di navigazione superiore prima della personalizzazione del font

![change_font_after](assets/change_font_after.png)

Barra di navigazione superiore dopo la personalizzazione del font della prima scheda
