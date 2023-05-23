---
title: Personalizzazione del gesto
seo-title: Gesture customization
description: Personalizzare i movimenti nell’app AEM Forms
seo-description: Customize the gestures on your AEM Forms app
uuid: 117e0e21-66bd-42f1-879c-6c1443991974
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 747d13d3-e7cc-4aa1-bcc8-4b57157e71ed
exl-id: 6debb1a7-7889-4fdd-87c7-ecb87cc0b1f5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# Personalizzazione del gesto {#gesture-customization}

Puoi personalizzare i movimenti dell’app AEM Forms in modo da fornire un metodo distinto per interagire con l’app. È ad esempio possibile aggiungere nuovi movimenti per aprire o chiudere un&#39;attività o un punto d&#39;inizio.

## Per personalizzare i movimenti nell’app AEM Forms {#to-customize-gestures-in-aem-forms-app}

Nell’app AEM Forms, con il pulsante sinistro del mouse viene aperta una nuova attività o un punto d’inizio, mentre con il pulsante destro del mouse non viene eseguita alcuna operazione. L’esempio seguente illustra la procedura per aprire una nuova attività o un punto d’inizio durante l’esecuzione dei movimenti di scorrimento con il pulsante destro del mouse nell’app AEM Forms.

1. Apri il progetto.

   * Per iOS, apri `Capture.xcodeproj` in Xcode
   * Per Android, apri il progetto Android in Eclipse.
   * Per Windows, apri `MWSWindows.sln` in Visual Studio.

1. Passa alla cartella delle viste e apri `task.js` file per la modifica.

   * In Xcode, passa a **Acquisizione > www > wsmobile > js > runtime > visualizzazioni** cartella.
   * In Eclipse, accedi al **assets > www > wsmobile > js > runtime > views** cartella.
   * In Visual Studio, passare al **MWSWwindows > www > wsmobile > js > runtime > visualizzazioni** cartella.

   >[!NOTE]
   >
   >Il file task.js contiene la vista backbone associata a ogni attività o punto d&#39;inizio elencato negli elenchi di attività o punto d&#39;inizio.

1. In `task.js` , cercare la proprietà events della visualizzazione.

   La proprietà events è una mappa con ogni voce nel formato:

   `"EventName Selector": "Function"`

   Quando si attiva un evento JavaScript denominato `EventName`su un elemento HTML specificato da `Selector`, il `Function`viene chiamato.

1. Trova

   * &quot;toccare .taskContentArea&quot; : &quot;onTaskClick&quot;,

      &quot;toccare .taskOpenArea&quot; : &quot;onTaskClick&quot;,

      &quot;toccare .task-content&quot; : &quot;onTaskClick&quot;,

      &quot;toccare .last_empty_div&quot; : &quot;onTaskClick&quot;,
   e sostituisci con

   * &quot;swipe .taskContentArea&quot; : &quot;onTaskClick&quot;,

      &quot;swipe .taskOpenArea&quot; : &quot;onTaskClick&quot;,

      &quot;swipe .task-content&quot; : &quot;onTaskClick&quot;,

      &quot;swipe .last_empty_div&quot; : &quot;onTaskClick&quot;,


1. Salva e chiudi `task.js` file.
1. Crea ed esegui l’app AEM Forms. Ora è possibile aprire un utilizzando con le opzioni scorri a sinistra e scorri a destra.

Analogamente, è possibile apportare modifiche in altre viste per varie combinazioni di movimenti, elementi HTML e funzioni.
