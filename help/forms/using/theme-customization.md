---
title: Personalizzazione tema
seo-title: Personalizzazione tema
description: Come personalizzare il tema dell'app AEM Forms.
seo-description: Come personalizzare il tema dell'app AEM Forms.
uuid: 36632e67-1cc6-416d-ae80-d84bbabab4bd
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: c72f608e-052a-4bf9-b7bc-ddf57483af35
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Personalizzazione tema {#theme-customization}

Potete personalizzare il codice HTML e il file CSS per fornire un aspetto e un aspetto distinti specifici dell&#39;organizzazione all&#39;app AEM Forms. Ad esempio, è possibile modificare il colore e l&#39;altezza di sfondo delle attività o dei punti di inizio. L&#39;esempio seguente fornisce le istruzioni per la modifica:

* visualizzare le istruzioni al posto della descrizione
* numero di percorsi di visualizzazione
* colore sfumatura sfondo

## Passaggi {#steps}

1. Apri il progetto.

   * Per iOS, aprite `Capture.xcodeproj` in Xcode
   * Per Android, aprite il progetto Android in Eclipse.
   * Per Windows, aprire `MWSWindows.sln` in Visual Studio.

1. Passate alla cartella dei modelli.

   * In Xcode, andate alla cartella **Capture > www > wsmobile > js > runtime > templates** .
   * In Eclipse, passa alla cartella **assets > www > wsmobile > js > runtime > templates** .
   * In Visual Studio, passare alla cartella **MWSWindows > www > wsmobile > js > runtime > templates** .

1. Open the `template.html` file for editing.
1. Individuate la stringa seguente:

   ```
   <%if ( (task.description !== "") && (task.description !== null) && (typeof task.description !== null) && (typeof task.description !== 'undefined') ) {%>
                  <div class="description_details">
                    <%= task.description %>
                  </div>
                 <%} else
   ```

   Sostituiscilo con `<%`.

1. Individuate il codice seguente nel `template.html` file:

   ```
   <ul id="task_menu_list">
                                   <li class="approve" title="<%= task.availableCommands.directCommands[0]%>" data-routename="<%= task.availableCommands.directCommands[0]%>">
                                       <%= task.availableCommands.directCommands[0]%>
                                   </li>
                                   <li class="reject last" title="<%= task.availableCommands.directCommands[1]%>" data-routename="<%= task.availableCommands.directCommands[1]%>">
                                       <%= task.availableCommands.directCommands[1]%>
                                   </li>
   ```

1. Commenta la riga seguente e salva il file.

   ```
   task.availableCommands.directCommands[1]%>">
   <%= task.availableCommands.directCommands[1]%>
   </li>
   ```

1. Passate alla cartella css.

   * In Xcode, passa a **Capture > www > wsmobile > css**.
   * In Eclipse, passa a **risorse > www > wsmobile > css**.
   * In Visual Studio, passare a **MWSWindows > www > wsmobile > css**.

1. Open the `_style.css` file for editing.
1. Per Immagine di sfondo, passate `#323232` a `#fff`.
1. Salvare le modifiche e chiudere il `_style.css` file.
1. Aprite l&#39;app AEM Forms.

   L&#39;app AEM Forms ora visualizza istruzioni invece della descrizione.
