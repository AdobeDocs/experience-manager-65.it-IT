---
title: Personalizzazione del gesto
description: Scopri come personalizzare i movimenti nell’app AEM Forms. Puoi personalizzare i movimenti per fornire un metodo distinto di interazione con l’applicazione.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 6debb1a7-7889-4fdd-87c7-ecb87cc0b1f5
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '309'
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

   * &quot;select .taskContentArea&quot; : &quot;onTaskClick&quot;,

     &quot;select .taskOpenArea&quot; : &quot;onTaskClick&quot;,

     &quot;select .task-content&quot; : &quot;onTaskClick&quot;,

     &quot;select .last_empty_div&quot; : &quot;onTaskClick&quot;,

   e sostituisci con

   * &quot;swipe .taskContentArea&quot; : &quot;onTaskClick&quot;,

     &quot;swipe .taskOpenArea&quot; : &quot;onTaskClick&quot;,

     &quot;swipe .task-content&quot; : &quot;onTaskClick&quot;,

     &quot;swipe .last_empty_div&quot; : &quot;onTaskClick&quot;,

1. Salva e chiudi `task.js` file.
1. Crea ed esegui l’app AEM Forms. Ora è possibile aprire un utilizzando con le opzioni scorri a sinistra e scorri a destra.

Analogamente, è possibile apportare modifiche in altre viste per varie combinazioni di movimenti, elementi HTML e funzioni.
