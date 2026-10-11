---
title: Personalizzazione del gesto
description: Scopri come personalizzare i movimenti nell’app AEM Forms. Puoi personalizzare i movimenti per fornire un metodo distinto di interazione con l’applicazione.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 6debb1a7-7889-4fdd-87c7-ecb87cc0b1f5
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
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 1%
---
# Personalizzazione del gesto {#gesture-customization}

>[!NOTE]
>
>L’app AEM Forms è attualmente obsoleta. Per domande o assistenza, contattare [aemformsapp-android@adobe.com](mailto:aemformsapp-android@adobe.com).

Puoi personalizzare i movimenti dell’app AEM Forms in modo da fornire un metodo distinto per interagire con l’app. È ad esempio possibile aggiungere nuovi movimenti per aprire o chiudere un&#39;attività o un punto d&#39;inizio.

## Per personalizzare i movimenti nell’app AEM Forms {#to-customize-gestures-in-aem-forms-app}

Nell’app AEM Forms, con il pulsante sinistro del mouse viene aperta una nuova attività o un punto d’inizio, mentre con il pulsante destro del mouse non viene eseguita alcuna operazione. L’esempio seguente illustra la procedura per aprire una nuova attività o un punto d’inizio durante l’esecuzione dei movimenti di scorrimento con il pulsante destro del mouse nell’app AEM Forms.

1. Apri il progetto.

   * Per iOS, apri `Capture.xcodeproj` in Xcode.
   * Per Android, apri il progetto Android in Eclipse.
   * Per Windows, aprire `MWSWindows.sln` in Visual Studio.

1. Passare alla cartella delle visualizzazioni e aprire il file `task.js` per la modifica.

   * In Xcode, passa alla cartella **Capture > www > wsmobile > js > runtime > views**.
   * In Eclipse, passa alla cartella **assets > www > wsmobile > js > runtime > views**.
   * In Visual Studio, passare alla cartella **MWSWwindows > www > wsmobile > js > runtime > views**.

   >[!NOTE]
   >
   >Il file task.js contiene la vista backbone associata a ogni attività o punto d&#39;inizio elencato negli elenchi di attività o punto d&#39;inizio.

1. Nel file `task.js`, cercare la proprietà degli eventi della visualizzazione.

   La proprietà events è una mappa con ogni voce nel formato:

   `"EventName Selector": "Function"`

   Quando si attiva un evento JavaScript denominato `EventName` su un elemento HTML specificato da `Selector`, viene chiamato `Function`.

1. Trova

   * &quot;select .taskContentArea&quot; : &quot;onTaskClick&quot;,

     &quot;select .taskOpenArea&quot; : &quot;onTaskClick&quot;,

     &quot;select .task-content&quot; : &quot;onTaskClick&quot;,

     &quot;select .last_empty_div&quot; : &quot;onTaskClick&quot;,

   e sostituisci con

   * &quot;swipe .taskContentArea&quot; : &quot;onTaskClick&quot;,

     &quot;swipe .taskOpenArea&quot; : &quot;onTaskClick&quot;,

     &quot;swipe .task-content&quot; : &quot;onTaskClick&quot;,

     &quot;swipe .last_empty_div&quot; : &quot;onTaskClick&quot;,

1. Salvare e chiudere il file `task.js`.
1. Crea ed esegui l’app AEM Forms. Ora è possibile aprire un utilizzando con le opzioni scorri a sinistra e scorri a destra.

Allo stesso modo, è possibile apportare modifiche in altre viste per varie combinazioni di movimenti, elementi HTML e funzioni.
