---
title: Personalizzazione dei gesti
seo-title: Personalizzazione dei gesti
description: Personalizzare i gesti nell'app AEM Forms
seo-description: Personalizzare i gesti nell'app AEM Forms
uuid: 117e0e21-66bd-42f1-879c-6c1443991974
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 747d13d3-e7cc-4aa1-bcc8-4b57157e71ed
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Personalizzazione dei gesti {#gesture-customization}

Potete personalizzare i gesti dell&#39;app AEM Forms per fornire un metodo distinto di interazione con l&#39;app. Ad esempio, è possibile aggiungere nuovi gesti per aprire o chiudere un&#39;attività o un punto iniziale.

## Personalizzazione dei gesti nell&#39;app AEM Forms {#to-customize-gestures-in-aem-forms-app}

Nell&#39;app AEM Forms, lo scorrimento a sinistra apre una nuova attività o un punto iniziale mentre lo scorrimento a destra non esegue alcuna operazione. L&#39;esempio seguente illustra i passaggi necessari per aprire una nuova attività o un punto iniziale durante l&#39;esecuzione dei gesti di scorrimento destro nell&#39;app AEM Forms.

1. Apri il progetto.

   * Per iOS, aprite `Capture.xcodeproj` in Xcode
   * Per Android, aprite il progetto Android in Eclipse.
   * Per Windows, aprire `MWSWindows.sln` in Visual Studio.

1. Andate alla cartella delle viste e aprite il `task.js` file per la modifica.

   * In Xcode, andate alla cartella **Capture > www > wsmobile > js > runtime > views** .
   * In Eclipse, passa alla cartella **assets > www > wsmobile > js > runtime > views** .
   * In Visual Studio, passare alla cartella **MWSWindows > www > wsmobile > js > runtime > views** .
   >[!NOTE]
   >
   >Il file task.js contiene la visualizzazione della colonna vertebrale associata a ogni attività o punto di inizio elencato negli elenchi task o punto di inizio.

1. Nel `task.js` file, cercare la proprietà events della visualizzazione.

   La proprietà events è una mappa con ciascuna voce nel formato seguente:

   `"EventName Selector": "Function"`

   Quando si attiva un evento Javascript denominato `EventName`su un elemento HTML specificato da `Selector`, `Function`viene chiamato.

1. Trova

   * &quot;tap.taskContentArea&quot;: &quot;onTaskClick&quot;,

      &quot;tap .taskOpenArea&quot;: &quot;onTaskClick&quot;,

      &quot;tap .task-content&quot;: &quot;onTaskClick&quot;,

      &quot;tap .last_empty_div&quot;: &quot;onTaskClick&quot;,
   e sostituire con

   * &quot;swipe.taskContentArea&quot;: &quot;onTaskClick&quot;,

      &quot;swipe.taskOpenArea&quot;: &quot;onTaskClick&quot;,

      &quot;swipe.task-content&quot;: &quot;onTaskClick&quot;,

      &quot;swipe.last_empty_div&quot;: &quot;onTaskClick&quot;,


1. Salvate e chiudete il `task.js` file.
1. Create ed eseguite l&#39;app AEM Forms. Ora è possibile aprire un&#39;applicazione con il dito sinistro e il passaggio del dito destro.

Allo stesso modo, potete apportare modifiche in altre viste per diverse combinazioni di gesti, elementi HTML e funzioni.

**[Contattare il supporto](https://www.adobe.com/account/sign-in.supportportal.html)**
