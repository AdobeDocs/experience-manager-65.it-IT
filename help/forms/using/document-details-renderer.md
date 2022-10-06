---
title: Dettagli del documento per il renderer
seo-title: Document details for renderer
description: Informazioni concettuali sul funzionamento dei rendering nell’area di lavoro di AEM Forms per eseguire il rendering dei vari tipi di modulo e file supportati.
seo-description: Conceptual information on how renders work in AEM Forms workspace to render the various supported form and file types.
uuid: ae3f0585-9105-4ca7-a490-ffdefd3ac8cd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: b6e88080-6ffc-4796-98c7-d7462bca454e
exl-id: 946f0f6d-86af-41c1-98ef-98c8f5566e95
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 0%

---

# Dettagli del documento per il renderer {#document-details-for-renderer}

## Introduzione {#introduction}

Nell’area di lavoro di AEM Forms, sono supportati più tipi di moduli senza soluzione di continuità. Comprendono:

* PDF forms (XDP/Acroform/Flat PDF)
* Nuovi moduli HTML
* Immagini
* Applicazioni di terze parti (ad esempio, Gestione della corrispondenza)

Questo documento spiega il funzionamento di questi moduli di rendering dal punto di vista della personalizzazione semantica / riutilizzo dei componenti, in modo che i requisiti del cliente siano soddisfatti senza interrompere il rendering. Sebbene lo spazio di lavoro di AEM Forms consenta qualsiasi modifica dell’interfaccia utente/semantica, si consiglia di non modificare la logica di rendering di diversi tipi di modulo, altrimenti i risultati potrebbero essere imprevedibili. Questo documento fornisce indicazioni/conoscenze per supportare il rendering dello stesso modulo, l’utilizzo degli stessi componenti Workspace in portali diversi e non per modificare la logica di rendering stessa.

## PDF forms {#pdf-forms}

Viene eseguito il rendering dei PDF forms da `PdfTaskForm View`.

Quando si esegue il rendering di un modulo XDP come PDF, viene eseguito un `FormBridge` JavaScript™ viene aggiunto dal servizio FormsAugmenter. Questo JavaScript™ (all’interno del modulo PDF) consente di eseguire azioni quali l’invio, il salvataggio di moduli o l’utilizzo offline del modulo.

Nell’area di lavoro di AEM Forms, la visualizzazione PDFTaskForm comunica con `FormBridge`javascript, tramite un HTML intermediario presente a `/lc/libs/ws/libs/ws/pdf.html`. Il flusso è:

**Visualizzazione PDFTaskForm - pdf.html**

Comunica utilizzando `window.postMessage` / `window.attachEvent('message')`

Questo metodo è il modo standard di comunicazione tra un frame principale e un iframe. I listener di eventi esistenti dai PDF forms aperti in precedenza vengono rimossi prima di aggiungerne uno nuovo. Questa eliminazione considera anche il passaggio tra la scheda del modulo e la scheda della cronologia nella visualizzazione dei dettagli delle attività.

**pdf.html - `FormBridge`javascript all’interno del PDF renderizzato**

Comunica utilizzando `pdfObject.postMessage` / `pdfObject.messageHandler`

Questo metodo è il metodo standard di comunicazione con un PDFJavaScript di un HTML. La visualizzazione PdfTaskForm si occupa anche di flat PDF e lo rende semplice.

>[!NOTE]
>
>Non è consigliabile modificare il contenuto pdf.html / della visualizzazione PdfTaskForm.

## Nuovo HTML Forms {#new-html-forms}

Il rendering dei nuovi moduli HTML viene eseguito tramite la visualizzazione NewHTMLTaskForm.

Quando viene eseguito il rendering di un modulo XDP come HTML utilizzando il pacchetto di moduli mobili distribuito su CRX, viene aggiunto anche `FormBridge`JavaScript al modulo, che espone diversi metodi di salvataggio e invio dei dati del modulo.

Questo JavaScript è diverso da quello indicato nei PDF forms precedenti, ma ha uno scopo simile.

>[!NOTE]
>
>Non è consigliabile modificare il contenuto della visualizzazione NewHTMLTaskForm.

## Forms e guide di Flex {#flex-forms-and-guides}

Il rendering di Flex Forms viene eseguito da SwfTaskForm e il rendering delle guide viene eseguito rispettivamente da HtmlTaskForm Views.

Nell’area di lavoro di AEM Forms, queste visualizzazioni comunicano con l’effettivo SWF che costituisce la forma/guida flex utilizzando un SWF intermedio presente in `/lc/libs/ws/libs/ws/WSNextAdapter.swf`

La comunicazione avviene utilizzando `swfObject.postMessage` / `window.flexMessageHandler`.

Questo protocollo è definito dalla `WsNextAdapter.swf`. L&#39;esistente `flexMessageHandlers`su un oggetto finestra, i moduli di SWF aperti in precedenza vengono rimossi prima di aggiungerne uno nuovo. La logica considera anche il passaggio tra la scheda del modulo e la scheda della cronologia nella visualizzazione dei dettagli dell’attività. `WsNextAdapter.swf` viene utilizzato per eseguire varie azioni del modulo, come salvataggio o invio.

>[!NOTE]
>
>Si sconsiglia di modificare `WSNextAdapter.swf` o il contenuto della visualizzazione SwfTaskForm / HtmlTaskForm.

## Applicazioni di terze parti (ad esempio, Gestione della corrispondenza) {#third-party-applications-for-example-correspondence-management}

Viene eseguito il rendering di applicazioni di terze parti utilizzando la visualizzazione ExtAppTaskForm.

**Comunicazione dell’applicazione di terze parti all’area di lavoro di AEM Forms**

L’area di lavoro di AEM Forms ascolta `window.global.postMessage([Message],[Payload])`

[Messaggio] può essere una stringa specificata come `SubmitMessage`| `CancelMessage`| `ErrorMessage`| `actionEnabledMessage`in `runtimeMap`. Le applicazioni di terze parti devono utilizzare questa interfaccia per notificare l’area di lavoro di AEM Forms in base alle esigenze. L’utilizzo di questa interfaccia è obbligatorio, perché l’area di lavoro di AEM Forms deve sapere che quando l’attività viene inviata in modo da poter ripulire la finestra dell’attività.

**Comunicazione tra l’area di lavoro di AEM Forms e applicazioni di terze parti**

Se i pulsanti di azione diretta dell’area di lavoro AEM Forms sono visibili, effettua una chiamata `window.[External-App-Name].getMessage([Action])`, dove `[Action]` viene letto dal `routeActionMap`. L’applicazione di terze parti deve ascoltare questa interfaccia e quindi inviare una notifica all’area di lavoro di AEM Forms tramite l’ `postMessage ()` API.

Ad esempio, un&#39;applicazione Flex può definire `ExternalInterface.addCallback('getMessage', listener)` a sostegno della presente comunicazione. Se l’applicazione di terze parti desidera gestire l’invio del modulo tramite i propri pulsanti, è necessario specificare `hideDirectActions = true() in the runtimeMap` e puoi saltare questo ascoltatore. Pertanto, questo costrutto è facoltativo.

Per ulteriori informazioni sull’integrazione di applicazioni di terze parti per quanto riguarda la gestione della corrispondenza, consulta [Integrazione della gestione della corrispondenza nell’area di lavoro di AEM Forms](/help/forms/using/integrating-correspondence-management-html-workspace.md).
