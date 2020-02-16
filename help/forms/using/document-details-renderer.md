---
title: Dettagli del documento per il renderer
seo-title: Dettagli del documento per il renderer
description: Informazioni concettuali sul funzionamento dei rendering nell’area di lavoro Moduli AEM per eseguire il rendering dei vari moduli e tipi di file supportati.
seo-description: Informazioni concettuali sul funzionamento dei rendering nell’area di lavoro Moduli AEM per eseguire il rendering dei vari moduli e tipi di file supportati.
uuid: ae3f0585-9105-4ca7-a490-ffdefd3ac8cd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: b6e88080-6ffc-4796-98c7-d7462bca454e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Dettagli del documento per il renderer {#document-details-for-renderer}

## Introduzione {#introduction}

Nell&#39;area di lavoro Moduli AEM, sono supportati più tipi di moduli senza problemi. Comprendono:

* Moduli PDF (XDP/Acroform/PDF semplici)
* Nuovi moduli HTML
* Immagini
* Applicazioni di terze parti (ad esempio, Gestione della corrispondenza)

In questo documento viene illustrato il funzionamento di questi renderer dal punto di vista della personalizzazione semantica e del riutilizzo dei componenti, in modo da soddisfare le esigenze dei clienti senza interrompere alcuna rappresentazione. L&#39;area di lavoro Moduli AEM consente di apportare qualsiasi modifica all&#39;interfaccia utente o alla logica di rendering dei diversi tipi di modulo, ma in caso contrario i risultati potrebbero essere imprevedibili. Questo documento è destinato alle linee guida/conoscenze per supportare il rendering dello stesso modulo, l’utilizzo degli stessi componenti dell’area di lavoro in portali diversi e non la modifica della logica di rendering stessa.

## Moduli PDF {#pdf-forms}

Il rendering dei moduli PDF viene eseguito da `PdfTaskForm View`.

Quando si esegue il rendering di un modulo XDP come PDF, il servizio FormsAugmenter aggiunge un `FormBridge` JavaScript™. Questo JavaScript™ (all&#39;interno del modulo PDF) consente di eseguire azioni quali l&#39;invio, il salvataggio dei moduli o la messa in modalità offline dei moduli.

Nell’area di lavoro AEM Forms, la visualizzazione PDFTaskForm comunica con il `FormBridge`javascript tramite un HTML intermedio presente in `/lc/libs/ws/libs/ws/pdf.html`. Il flusso è:

**Visualizzazione PDFTaskForm - pdf.html**

Comunica utilizzando `window.postMessage` / `window.attachEvent('message')`

Questo metodo è il metodo standard di comunicazione tra un fotogramma principale e un iframe. I listener di eventi esistenti dai moduli PDF aperti in precedenza vengono rimossi prima di aggiungerne uno nuovo. Questa eliminazione considera anche il passaggio tra la scheda del modulo e la scheda della cronologia nella visualizzazione dei dettagli dell&#39;attività.

**pdf.html -`FormBridge`javascript nel PDF di cui è stato effettuato il rendering**

Comunica utilizzando `pdfObject.postMessage` / `pdfObject.messageHandler`

Questo metodo è il metodo standard di comunicazione con un javascript PDF da un HTML. La visualizzazione PdfTaskForm si occupa anche di PDF semplice e lo riproduce in modo semplice.

>[!NOTE]
>
>Non è consigliabile modificare il contenuto pdf.html / della visualizzazione PdfTaskForm.

## Nuovi moduli HTML {#new-html-forms}

Il rendering dei nuovi moduli HTML viene eseguito dalla visualizzazione NewHTMLTaskForm.

Quando si esegue il rendering in HTML di un modulo XDP utilizzando il pacchetto di moduli mobili distribuito in CRX, viene aggiunto al modulo anche `FormBridge` javascript aggiuntivo, che espone metodi diversi per salvare e inviare i dati del modulo.

Questo javascript è diverso da quello indicato nei moduli PDF sopra, ma ha uno scopo simile.

>[!NOTE]
>
>Non è consigliabile modificare il contenuto della visualizzazione NewHTMLTaskForm.

## Moduli e guide Flex {#flex-forms-and-guides}

Per i moduli Flex viene eseguito il rendering da SwfTaskForm e le guide vengono rappresentate rispettivamente da HtmlTaskForm Views.

Nell&#39;area di lavoro di AEM Forms, queste viste comunicano con il file SWF effettivo che costituisce la forma/guida flessibile tramite un file SWF intermedio presente in `/lc/libs/ws/libs/ws/WSNextAdapter.swf`

La comunicazione avviene utilizzando `swfObject.postMessage` / `window.flexMessageHandler`.

Questo protocollo è definito dall&#39; `WsNextAdapter.swf`. L&#39;oggetto `flexMessageHandlers`presente nella finestra, dai moduli SWF aperti in precedenza, viene rimosso prima di aggiungerne uno nuovo. La logica considera anche il passaggio tra la scheda del modulo e la scheda della cronologia nella visualizzazione dei dettagli dell&#39;attività. `WsNextAdapter.swf` viene utilizzato per eseguire varie azioni modulo, ad esempio salvare o inviare.

>[!NOTE]
>
>Non è consigliabile modificare `WSNextAdapter.swf` o il contenuto della visualizzazione SwfTaskForm/HtmlTaskForm.

## Applicazioni di terze parti (ad esempio, Gestione della corrispondenza) {#third-party-applications-for-example-correspondence-management}

Il rendering delle applicazioni di terze parti viene eseguito utilizzando la visualizzazione ExtAppTaskForm.

**Comunicazione di applicazioni di terze parti all’area di lavoro AEM Forms**

L&#39;area di lavoro Moduli AEM ascolta `window.global.postMessage([Message],[Payload])`

[]`SubmitMessage``CancelMessage`Il messaggio`ErrorMessage` può essere una stringa specificata come||| `actionEnabledMessage`nel `runtimeMap`. Le applicazioni di terze parti devono utilizzare questa interfaccia per inviare le notifiche all&#39;area di lavoro di AEM Forms, in base alle esigenze. L&#39;utilizzo di questa interfaccia è obbligatorio perché l&#39;area di lavoro Moduli AEM deve sapere che all&#39;invio dell&#39;attività in modo da poter ripulire la finestra dell&#39;attività.

**Area di lavoro AEM Forms per comunicare con applicazioni di terze parti**

Se i pulsanti di azione diretta dell&#39;area di lavoro AEM Forms sono visibili, richiama `window.[External-App-Name].getMessage([Action])`, dove [ `Action]` viene letto dall&#39;area di lavoro `routeActionMap`. L&#39;applicazione di terze parti deve ascoltare questa interfaccia, quindi inviare una notifica all&#39;area di lavoro di AEM Forms tramite l&#39; `postMessage ()` API.

Ad esempio, un&#39;applicazione Flex può definire `ExternalInterface.addCallback('getMessage', listener)` per supportare questa comunicazione. Se l&#39;applicazione di terze parti desidera gestire l&#39;invio del modulo tramite i propri pulsanti, è necessario specificare `hideDirectActions = true() in the runtimeMap` e ignorare il listener. Quindi, questo costrutto è facoltativo.

Per ulteriori informazioni sull’integrazione di applicazioni di terze parti con la gestione della corrispondenza, consulta [Integrazione della gestione della corrispondenza nell’area di lavoro](/help/forms/using/integrating-correspondence-management-html-workspace.md)Moduli AEM.


[Contattare il supporto](https://www.adobe.com/account/sign-in.supportportal.html)
