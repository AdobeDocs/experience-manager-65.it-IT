---
title: Dettagli documento per renderer
description: Informazioni concettuali sul funzionamento dei rendering nell’area di lavoro di AEM Forms per eseguire il rendering dei vari tipi di file e moduli supportati.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 946f0f6d-86af-41c1-98ef-98c8f5566e95
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---

# Dettagli documento per renderer {#document-details-for-renderer}

## Introduzione {#introduction}

Nell’area di lavoro di AEM Forms, sono supportati senza problemi più tipi di modulo. Comprendono:

* PDF forms (XDP/Acroform/Flat PDF)
* Nuovi moduli HTML
* Immagini
* Applicazioni di terze parti (ad esempio, Gestione della corrispondenza)

Questo documento spiega il funzionamento di questi renderer dal punto di vista della personalizzazione semantica e del riutilizzo dei componenti, in modo da soddisfare i requisiti dei clienti senza interrompere alcuna rappresentazione. Sebbene l’area di lavoro di AEM Forms consenta qualsiasi modifica semantica o all’interfaccia utente, si consiglia di non modificare la logica di rendering dei diversi tipi di modulo, altrimenti i risultati potrebbero essere imprevedibili. Questo documento offre indicazioni e supporto per il rendering dello stesso modulo, l’utilizzo degli stessi componenti dell’area di lavoro in portali diversi e non per la modifica della logica di rendering.

## PDF forms {#pdf-forms}

Il rendering dei PDF forms è eseguito da `PdfTaskForm View`.

Quando viene eseguito il rendering di un modulo XDP come PDF, il servizio FormsAugmenter aggiunge un JavaScript™ `FormBridge`. Questo JavaScript™ (all’interno del modulo PDF) consente di eseguire azioni quali l’invio di un modulo, il salvataggio di un modulo o la disconnessione del modulo.

Nell&#39;area di lavoro di AEM Forms, la vista PDFTaskForm comunica con `FormBridge`JavaScript tramite un HTML intermedio presente in `/lc/libs/ws/libs/ws/pdf.html`. Il flusso è:

**Vista PDFTaskForm - pdf.html**

Comunica utilizzando `window.postMessage` / `window.attachEvent('message')`

Questo metodo è il metodo standard di comunicazione tra un frame principale e un iframe. I listener di eventi esistenti dai PDF forms aperti in precedenza vengono rimossi prima di aggiungerne uno nuovo. Questa rimozione considera anche il passaggio tra la scheda del modulo e la scheda della cronologia nella visualizzazione dei dettagli dell’attività.

**pdf.html - `FormBridge`JavaScript all&#39;interno del PDF sottoposto a rendering**

Comunica utilizzando `pdfObject.postMessage` / `pdfObject.messageHandler`

Questo metodo è il metodo standard di comunicazione con un PDFJavaScript di un HTML. La visualizzazione PdfTaskForm si occupa anche di un PDF piatto e lo rende semplice.

>[!NOTE]
>
>Si sconsiglia di modificare il contenuto pdf.html/della visualizzazione PdfTaskForm.

## Nuovo HTML Forms {#new-html-forms}

Il rendering dei nuovi moduli HTML viene eseguito dalla vista NewHTMLTaskForm.

Quando si esegue il rendering di un modulo XDP come HTML utilizzando il pacchetto di moduli per dispositivi mobili distribuito su CRX, al modulo viene aggiunto anche `FormBridge`JavaScript aggiuntivo, che espone diversi metodi per il salvataggio e l’invio dei dati del modulo.

Questo JavaScript è diverso da quello a cui si fa riferimento nei PDF forms precedenti, ma ha uno scopo simile.

>[!NOTE]
>
>L&#39;Adobe non consiglia di modificare il contenuto della visualizzazione NewHTMLTaskForm.

## Flex Forms e guide {#flex-forms-and-guides}

Il rendering dei Forms di Flex viene eseguito da SwfTaskForm e il rendering delle guide viene eseguito rispettivamente da HtmlTaskForm Views.

Nell&#39;area di lavoro di AEM Forms, queste visualizzazioni comunicano con il SWF effettivo che costituisce il modulo/guida di Flex® utilizzando un SWF intermedio presente in `/lc/libs/ws/libs/ws/WSNextAdapter.swf`

La comunicazione viene eseguita utilizzando `swfObject.postMessage` / `window.flexMessageHandler`.

Protocollo definito da `WsNextAdapter.swf`. L&#39;oggetto `flexMessageHandlers` esistente nella finestra, da moduli SWF aperti in precedenza, viene rimosso prima di aggiungerne uno nuovo. La logica considera anche il passaggio tra la scheda del modulo e la scheda della cronologia nella visualizzazione dei dettagli dell’attività. `WsNextAdapter.swf` viene utilizzato per eseguire varie azioni del modulo, ad esempio Salva o Invia.

>[!NOTE]
>
>Non è consigliabile modificare `WSNextAdapter.swf` o il contenuto della visualizzazione SwfTaskForm/HtmlTaskForm.

## Applicazioni di terze parti (ad esempio, Gestione della corrispondenza) {#third-party-applications-for-example-correspondence-management}

Il rendering delle applicazioni di terze parti viene eseguito utilizzando la vista ExtAppTaskForm.

**Applicazione di terze parti per la comunicazione nell&#39;area di lavoro di AEM Forms**

L&#39;area di lavoro di AEM Forms è in ascolto su `window.global.postMessage([Message],[Payload])`

[Messaggio] può essere una stringa specificata come `SubmitMessage`| `CancelMessage`| `ErrorMessage`| `actionEnabledMessage` in `runtimeMap`. Le applicazioni di terze parti devono utilizzare questa interfaccia per inviare le notifiche necessarie all’area di lavoro di AEM Forms. L’utilizzo di questa interfaccia è obbligatorio perché l’area di lavoro di AEM Forms deve sapere quando l’attività viene inviata in modo da poter pulire la finestra dell’attività.

**Area di lavoro AEM Forms per comunicazioni applicazioni di terze parti**

Se i pulsanti di azione diretta dell&#39;area di lavoro AEM Forms sono visibili, chiama `window.[External-App-Name].getMessage([Action])`, dove `[Action]` viene letto da `routeActionMap`. L&#39;applicazione di terze parti deve essere in ascolto su questa interfaccia e quindi inviare una notifica all&#39;area di lavoro di AEM Forms tramite l&#39;API `postMessage ()`.

Ad esempio, un&#39;applicazione Flex può definire `ExternalInterface.addCallback('getMessage', listener)` per supportare questa comunicazione. Se l&#39;applicazione di terze parti desidera gestire l&#39;invio del modulo tramite i propri pulsanti, è necessario specificare `hideDirectActions = true() in the runtimeMap`. È possibile ignorare questo listener. Pertanto, questo costrutto è facoltativo.

Per ulteriori informazioni sull&#39;integrazione di applicazioni di terze parti relative alla gestione della corrispondenza, consulta [Integrazione della gestione della corrispondenza nell&#39;area di lavoro di AEM Forms](/help/forms/using/integrating-correspondence-management-html-workspace.md).
