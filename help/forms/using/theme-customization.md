---
title: Personalizzazione del tema
description: Scopri come personalizzare il tema dell’applicazione AEM Forms. Puoi personalizzare il codice HTML e il file CSS per dare un aspetto specifico all’organizzazione.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 9b8c5933-b783-48f9-b463-15a01e06ee98
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 5%
---
# Personalizzazione del tema {#theme-customization}

>[!NOTE]
>
>L’app AEM Forms è attualmente obsoleta. Per domande o assistenza, contattare [aemformsapp-android@adobe.com](mailto:aemformsapp-android@adobe.com).

Puoi personalizzare il codice HTML e il file CSS per fornire all’app AEM Forms un aspetto specifico per l’organizzazione. È ad esempio possibile modificare il colore e l&#39;altezza dello sfondo delle attività o dei punti iniziali. Nell&#39;esempio seguente vengono fornite istruzioni per la modifica:

* visualizza le istruzioni al posto della descrizione
* numero di route di visualizzazione
* colore sfumatura sfondo

## Passaggi {#steps}

1. Apri il progetto.

   * Per iOS, apri `Capture.xcodeproj` in Xcode.
   * Per Android, apri il progetto Android in Eclipse.
   * Per Windows, aprire `MWSWindows.sln` in Visual Studio.

1. Passa alla cartella dei modelli.

   * In Xcode, passa alla cartella **Acquisizione > www > wsmobile > js > runtime > template**.
   * In Eclipse, passa alla cartella **assets > www > wsmobile > js > runtime > templates**.
   * In Visual Studio, passare alla cartella **MWSWwindows > www > wsmobile > js > runtime > template**.

1. Apri il file `template.html` per la modifica.
1. Individua la seguente stringa:

   ```jsp
   <%if ( (task.description !== "") && (task.description !== null) && (typeof task.description !== null) && (typeof task.description !== 'undefined') ) {%>
                  <div class="description_details">
                    <%= task.description %>
                  </div>
                 <%} else
   ```

   Sostituiscilo con `<%`.

1. Individuare il codice seguente nel file `template.html`:

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
   * In Eclipse, passa a **risorse > www > wsmobile > css**.
   * In Visual Studio passare a **MWSWwindows > www > wsmobile > css**.

1. Apri il file `_style.css` per la modifica.
1. Per l&#39;immagine di sfondo, modificare `#323232` in `#fff`.
1. Salvare le modifiche e chiudere il file `_style.css`.
1. Apri l’app AEM Forms.

   L’app AEM Forms ora visualizza istruzioni invece della descrizione.
