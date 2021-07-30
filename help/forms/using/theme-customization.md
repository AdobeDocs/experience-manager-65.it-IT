---
title: Personalizzazione del tema
seo-title: Personalizzazione del tema
description: Come personalizzare il tema della tua app AEM Forms.
seo-description: Come personalizzare il tema della tua app AEM Forms.
uuid: 36632e67-1cc6-416d-ae80-d84bbabab4bd
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: c72f608e-052a-4bf9-b7bc-ddf57483af35
exl-id: 9b8c5933-b783-48f9-b463-15a01e06ee98
source-git-commit: 6bc228866aca785ec768daefb73970fc24568ef0
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# Personalizzazione del tema {#theme-customization}

Puoi personalizzare il codice HTML e il file CSS per fornire all’app AEM Forms un aspetto e un aspetto distinti per l’organizzazione. Ad esempio, è possibile modificare il colore e l&#39;altezza dello sfondo delle attività o dei punti iniziali. L&#39;esempio seguente fornisce istruzioni per la modifica:

* visualizza le istruzioni al posto della descrizione
* numero di percorsi di visualizzazione
* colore sfumatura sfondo

## Passaggi {#steps}

1. Apri il progetto.

   * Per iOS, apri `Capture.xcodeproj` in Xcode.
   * Per Android, apri il progetto Android in Eclipse.
   * Per Windows, aprire `MWSWindows.sln` in Visual Studio.

1. Passa alla cartella dei modelli.

   * In Xcode, passa alla cartella **Capture > www > wsmobile > js > runtime > templates** .
   * In Eclipse, passa alla cartella **risorse > www > wsmobile > js > runtime > templates** .
   * In Visual Studio, passare alla cartella **MWSWindows > www > wsmobile > js > runtime > templates** .

1. Apri il file `template.html` per la modifica.
1. Individua la stringa seguente:

   ```jsp
   <%if ( (task.description !== "") && (task.description !== null) && (typeof task.description !== null) && (typeof task.description !== 'undefined') ) {%>
                  <div class="description_details">
                    <%= task.description %>
                  </div>
                 <%} else
   ```

   Sostituiscilo con `<%`.

1. Individua il seguente codice nel file `template.html` :

   ```jsp
   <ul id="task_menu_list">
                                   <li class="approve" title="<%= task.availableCommands.directCommands[0]%>" data-routename="<%= task.availableCommands.directCommands[0]%>">
                                       <%= task.availableCommands.directCommands[0]%>
                                   </li>
                                   <li class="reject last" title="<%= task.availableCommands.directCommands[1]%>" data-routename="<%= task.availableCommands.directCommands[1]%>">
                                       <%= task.availableCommands.directCommands[1]%>
                                   </li>
   ```

1. Commenta la riga seguente e salva il file.

   ```jsp
   task.availableCommands.directCommands[1]%>">
   <%= task.availableCommands.directCommands[1]%>
   </li>
   ```

1. Passa alla cartella css .

   * In Xcode, passa a **Cattura > www > wsmobile > css**.
   * In Eclipse, passa a **risorse > www > wsmobile > css**.
   * In Visual Studio, passare a **MWSWindows > www > wsmobile > css**.

1. Apri il file `_style.css` per la modifica.
1. Per Immagine di sfondo, modifica `#323232` in `#fff`.
1. Salva le modifiche e chiudi il file `_style.css`.
1. Apri l’app AEM Forms.

   L’app AEM Forms ora visualizza le istruzioni anziché la descrizione.
