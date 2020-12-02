---
title: Dettagli del documento per il renderer
seo-title: Dettagli del documento per il renderer
description: Informazioni concettuali sul funzionamento dei rendering nell'area di lavoro  AEM Forms per eseguire il rendering dei vari moduli e tipi di file supportati.
seo-description: Informazioni concettuali sul funzionamento dei rendering nell'area di lavoro  AEM Forms per eseguire il rendering dei vari moduli e tipi di file supportati.
uuid: ae3f0585-9105-4ca7-a490-ffdefd3ac8cd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: b6e88080-6ffc-4796-98c7-d7462bca454e
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---


# Dettagli del documento per il renderer {#document-details-for-renderer}

## Introduzione {#introduction}

Nellarea di lavoro di AEM Forms, sono supportati più tipi di moduli senza problemi. Comprendono:

* PDF forms (XDP/Acroform/PDF flat)
* Nuovi moduli HTML
* Immagini
* Applicazioni di terze parti (ad esempio, Gestione della corrispondenza)

In questo documento viene illustrato il funzionamento di questi renderer dal punto di vista della personalizzazione semantica e del riutilizzo dei componenti, in modo da soddisfare le esigenze dei clienti senza interrompere alcuna rappresentazione. Anche se &#39;area di lavoro di AEM Forms consente qualsiasi interfaccia utente/modifica semantica, si consiglia di non modificare la logica di rendering dei diversi tipi di modulo, altrimenti i risultati potrebbero essere imprevedibili. Questo documento è destinato alle linee guida/conoscenze per supportare il rendering dello stesso modulo, l’utilizzo degli stessi componenti dell’area di lavoro in portali diversi e non la modifica della logica di rendering stessa.

## PDF forms {#pdf-forms}

Il rendering dei PDF forms viene eseguito da `PdfTaskForm View`.

Quando si esegue il rendering di un modulo XDP come PDF, il servizio FormsAugmenter aggiunge un `FormBridge` JavaScript™. Questo JavaScript™ (all&#39;interno del modulo PDF) consente di eseguire azioni quali l&#39;invio, il salvataggio dei moduli o la messa in modalità offline dei moduli.

Nell&#39;area di lavoro  AEM Forms, la visualizzazione PDFTaskForm comunica con il codice `FormBridge`javascript, tramite un codice HTML intermedio presente in `/lc/libs/ws/libs/ws/pdf.html`. Il flusso è:

**Visualizzazione PDFTaskForm - pdf.html**

Comunica utilizzando `window.postMessage` / `window.attachEvent('message')`

Questo metodo è il metodo standard di comunicazione tra un fotogramma principale e un iframe. I listener di eventi esistenti provenienti da PDF forms aperti in precedenza vengono rimossi prima di aggiungerne uno nuovo. Questa eliminazione considera anche il passaggio tra la scheda del modulo e la scheda della cronologia nella visualizzazione dei dettagli dell&#39;attività.

**pdf.html -  `FormBridge`javascript nel PDF di cui è stato effettuato il rendering**

Comunica utilizzando `pdfObject.postMessage` / `pdfObject.messageHandler`

Questo metodo è il metodo standard di comunicazione con un PDF PDFavaScript da un HTML. La visualizzazione PdfTaskForm si occupa anche di PDF semplice e lo riproduce in modo semplice.

>[!NOTE]
>
>Non è consigliabile modificare il contenuto pdf.html / della visualizzazione PdfTaskForm.

## Nuovo Forms HTML {#new-html-forms}

Il rendering dei nuovi moduli HTML viene eseguito dalla visualizzazione NewHTMLTaskForm.

Quando si esegue il rendering di un modulo XDP come HTML utilizzando il pacchetto di moduli mobili distribuito in CRX, viene aggiunto al modulo anche `FormBridge`JavaScript aggiuntivo, che espone metodi diversi per salvare e inviare i dati del modulo.

Questo JavaScript è diverso da quello indicato nei PDF forms precedenti, ma ha uno scopo simile.

>[!NOTE]
>
>Non è consigliabile modificare il contenuto della visualizzazione NewHTMLTaskForm.

## Flex Forms e Guide {#flex-forms-and-guides}

Il rendering di Flex Forms viene eseguito da SwfTaskForm e il rendering delle guide viene eseguito rispettivamente da HtmlTaskForm Views.

Nell&#39;area di lavoro  AEM Forms, queste viste comunicano con il file SWF effettivo che costituisce la forma/guida flessibile utilizzando un file SWF intermedio presente in `/lc/libs/ws/libs/ws/WSNextAdapter.swf`

La comunicazione avviene utilizzando `swfObject.postMessage` / `window.flexMessageHandler`.

Questo protocollo è definito dalla `WsNextAdapter.swf`. L&#39;oggetto `flexMessageHandlers`presente nella finestra, dai moduli SWF aperti in precedenza, viene rimosso prima di aggiungerne uno nuovo. La logica considera anche il passaggio tra la scheda del modulo e la scheda della cronologia nella visualizzazione dei dettagli dell&#39;attività. `WsNextAdapter.swf` viene utilizzato per eseguire varie azioni modulo, ad esempio salvare o inviare.

>[!NOTE]
>
>Non è consigliabile modificare `WSNextAdapter.swf` o il contenuto della visualizzazione SwfTaskForm / HtmlTaskForm.

## Applicazioni di terze parti (ad esempio, Gestione corrispondenza) {#third-party-applications-for-example-correspondence-management}

Il rendering delle applicazioni di terze parti viene eseguito utilizzando la visualizzazione ExtAppTaskForm.

**Applicazione di terze parti per  comunicazione area di lavoro AEM Forms**

&#39;area di lavoro di AEM Forms ascolta `window.global.postMessage([Message],[Payload])`

[Messagecan ] può essere una stringa specificata come  `SubmitMessage`|  `CancelMessage`|  `ErrorMessage`|  `actionEnabledMessage`nel  `runtimeMap`. Le applicazioni di terze parti devono utilizzare questa interfaccia per notificare &#39;area di lavoro di AEM Forms in base alle esigenze. L&#39;utilizzo di questa interfaccia è obbligatorio, perché l&#39;area di lavoro di AEM Forms  deve sapere che quando l&#39;attività viene inviata in modo da poter ripulire la finestra dell&#39;attività.

**area di lavoro AEM Forms alla comunicazione con applicazioni di terze parti**

Se  i pulsanti di azione diretta dell&#39;area di lavoro AEM Forms sono visibili, chiama `window.[External-App-Name].getMessage([Action])`, dove `[Action]` viene letto dal `routeActionMap`. L&#39;applicazione di terze parti deve essere in ascolto su questa interfaccia, quindi inviare una notifica &#39;area di lavoro AEM Forms tramite l&#39;API `postMessage ()`.

Ad esempio, un&#39;applicazione Flex può definire `ExternalInterface.addCallback('getMessage', listener)` per supportare questa comunicazione. Se l&#39;applicazione di terze parti desidera gestire l&#39;invio del modulo tramite i propri pulsanti, è necessario specificare `hideDirectActions = true() in the runtimeMap` e ignorare questo listener. Quindi, questo costrutto è facoltativo.

Per saperne di più sull&#39;integrazione di applicazioni di terze parti con la gestione della corrispondenza, consultate [Integrazione della gestione della corrispondenza nell&#39;area di lavoro  AEM Forms](/help/forms/using/integrating-correspondence-management-html-workspace.md).
