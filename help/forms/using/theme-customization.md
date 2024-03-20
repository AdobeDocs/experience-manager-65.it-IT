---
title: Personalizzazione tema
description: Scopri come personalizzare il tema dell’applicazione AEM Forms. Puoi personalizzare il codice HTML e il file CSS per dare un aspetto specifico all’organizzazione.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 9b8c5933-b783-48f9-b463-15a01e06ee98
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# Personalizzazione tema {#theme-customization}

Puoi personalizzare il codice HTML e il file CSS per fornire all’app AEM Forms un aspetto specifico per l’organizzazione. È ad esempio possibile modificare il colore e l&#39;altezza dello sfondo delle attività o dei punti iniziali. Nell&#39;esempio seguente vengono fornite istruzioni per la modifica:

* visualizza le istruzioni al posto della descrizione
* numero di route di visualizzazione
* colore sfumatura sfondo

## Passaggi {#steps}

1. Apri il progetto.

   * Per iOS, apri `Capture.xcodeproj` in Xcode
   * Per Android, apri il progetto Android in Eclipse.
   * Per Windows, apri `MWSWindows.sln` in Visual Studio.

1. Passa alla cartella dei modelli.

   * In Xcode, passa a **Acquisizione > www > wsmobile > js > runtime > modelli** cartella.
   * In Eclipse, accedi al **assets > www > wsmobile > js > runtime > template** cartella.
   * In Visual Studio, passare al **MWSWwindows > www > wsmobile > js > runtime > modelli** cartella.

1. Apri `template.html` file per la modifica.
1. Individua la seguente stringa:

   ```jsp
   <%if ( (task.description !== "") && (task.description !== null) && (typeof task.description !== null) && (typeof task.description !== 'undefined') ) {%>
                  <div class="description_details">
                    <%= task.description %>
                  </div>
                 <%} else
   ```

   Sostituiscilo con `<%`.

1. Individua il seguente codice in `template.html` file:

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

1. Passa alla cartella css.

   * In Xcode, passa a **Acquisizione > www > wsmobile > css**.
   * In Eclipse, passa a **assets > www > wsmobile > css**.
   * In Visual Studio passare a **MWSWwindows > www > wsmobile > css**.

1. Apri `_style.css` file per la modifica.
1. Per l&#39;immagine di sfondo, modificare `#323232` a `#fff`.
1. Salva le modifiche e chiudi `_style.css` file.
1. Apri l’app AEM Forms.

   L’app AEM Forms ora visualizza istruzioni invece della descrizione.
