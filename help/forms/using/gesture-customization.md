---
title: Personalizzazione dei gesti
seo-title: Personalizzazione dei gesti
description: Personalizzare i gesti sull'app  AEM Forms
seo-description: Personalizzare i gesti sull'app  AEM Forms
uuid: 117e0e21-66bd-42f1-879c-6c1443991974
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 747d13d3-e7cc-4aa1-bcc8-4b57157e71ed
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---


# Personalizzazione dei gesti {#gesture-customization}

Potete personalizzare i gesti di &#39;app AEM Forms per fornire un metodo distinto di interazione con l&#39;app. Ad esempio, è possibile aggiungere nuovi gesti per aprire o chiudere un&#39;attività o un punto iniziale.

## Personalizzazione dei gesti nell&#39;app  AEM Forms {#to-customize-gestures-in-aem-forms-app}

Nell&#39;app AEM Forms , lo scorrimento a sinistra apre una nuova attività o un punto iniziale mentre lo scorrimento a destra non esegue alcuna operazione. L&#39;esempio seguente illustra i passaggi per aprire una nuova attività o un punto iniziale durante l&#39;esecuzione dei gesti di scorrimento destro nell&#39;app AEM Forms .

1. Apri il progetto.

   * Per iOS, apri `Capture.xcodeproj` in Xcode
   * Per Android, aprite il progetto Android in Eclipse.
   * Per Windows, aprire `MWSWindows.sln` in Visual Studio.

1. Andate alla cartella delle viste e aprite il file `task.js` per la modifica.

   * In Xcode, andate alla cartella **Capture > www > wsmobile > js > runtime > views**.
   * In Eclipse, andate alla cartella **assets > www > wsmobile > js > runtime > views**.
   * In Visual Studio, passare alla cartella **MWSWindows > www > wsmobile > js > runtime > views**.

   >[!NOTE]
   >
   >Il file task.js contiene la visualizzazione della colonna vertebrale associata a ogni attività o punto di inizio elencato negli elenchi task o punto di inizio.

1. Nel file `task.js`, cercare la proprietà events della vista.

   La proprietà events è una mappa con ciascuna voce nel formato seguente:

   `"EventName Selector": "Function"`

   Quando si attiva un evento Javascript denominato `EventName`su un elemento HTML specificato da `Selector`, viene chiamato il simbolo `Function`.

1. Trova

   * &quot;tap.taskContentArea&quot;: &quot;onTaskClick&quot;,

      &quot;tap.taskOpenArea&quot;: &quot;onTaskClick&quot;,

      &quot;tap .task-content&quot;: &quot;onTaskClick&quot;,

      &quot;tap .last_empty_div&quot;: &quot;onTaskClick&quot;,
   e sostituire con

   * &quot;swipe.taskContentArea&quot;: &quot;onTaskClick&quot;,

      &quot;swipe.taskOpenArea&quot;: &quot;onTaskClick&quot;,

      &quot;swipe.task-content&quot;: &quot;onTaskClick&quot;,

      &quot;swipe.last_empty_div&quot;: &quot;onTaskClick&quot;,


1. Salvate e chiudete il file `task.js`.
1. Create ed eseguite l&#39;app AEM Forms . Ora è possibile aprire un’interfaccia con il passaggio del dito verso sinistra e il passaggio del dito verso destra.

Allo stesso modo, potete apportare modifiche in altre viste per diverse combinazioni di gesti, elementi HTML e funzioni.
