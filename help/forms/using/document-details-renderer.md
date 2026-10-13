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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 1%
---
# Dettagli documento per renderer {#document-details-for-renderer}

## Introduzione {#introduction}

Nell’area di lavoro di AEM Forms, sono supportati senza problemi più tipi di modulo. Comprendono:

* PDF forms (XDP/Acroform/PDF piatti)
* Nuovi moduli HTML
* Immagini
* Applicazioni di terze parti (ad esempio, Gestione della corrispondenza)

Questo documento spiega il funzionamento di questi renderer dal punto di vista della personalizzazione semantica e del riutilizzo dei componenti, in modo da soddisfare i requisiti dei clienti senza interrompere alcuna rappresentazione. Sebbene l’area di lavoro di AEM Forms consenta qualsiasi modifica semantica o all’interfaccia utente, si consiglia di non modificare la logica di rendering dei diversi tipi di modulo, altrimenti i risultati potrebbero essere imprevedibili. Questo documento offre indicazioni e supporto per il rendering dello stesso modulo, l’utilizzo degli stessi componenti dell’area di lavoro in portali diversi e non per la modifica della logica di rendering.

## PDF forms {#pdf-forms}

Il rendering di PDF forms viene eseguito da `PdfTaskForm View`.

Quando un modulo XDP viene renderizzato come PDF, il servizio FormsAugmenter aggiunge un JavaScript™ `FormBridge`. Questo JavaScript™ (all’interno del modulo PDF) consente di eseguire azioni quali l’invio di un modulo, il salvataggio di un modulo o la disconnessione del modulo.

Nell&#39;area di lavoro di AEM Forms, la vista PDFTaskForm comunica con `FormBridge`JavaScript tramite un HTML intermedio presente in `/lc/libs/ws/libs/ws/pdf.html`. Il flusso è:

**Vista PDFTaskForm - pdf.html**

Comunica utilizzando `window.postMessage` / `window.attachEvent('message')`

Questo metodo è il metodo standard di comunicazione tra un frame principale e un iframe. I listener di eventi esistenti da PDF forms aperti in precedenza vengono rimossi prima di aggiungerne uno nuovo. Questa rimozione considera anche il passaggio tra la scheda del modulo e la scheda della cronologia nella visualizzazione dei dettagli dell’attività.

**pdf.html - `FormBridge`JavaScript all&#39;interno del PDF sottoposto a rendering**

Comunica utilizzando `pdfObject.postMessage` / `pdfObject.messageHandler`

Questo metodo è il metodo standard di comunicazione con un PDFJavaScript di un HTML. La visualizzazione PdfTaskForm si occupa anche di un PDF piatto e lo rende semplice.

>[!NOTE]
>
>Si sconsiglia di modificare il contenuto pdf.html/della visualizzazione PdfTaskForm.

## Nuovo Forms HTML {#new-html-forms}

Il rendering dei nuovi moduli di HTML viene eseguito tramite la visualizzazione NewHTMLTaskForm.

Quando si esegue il rendering di un modulo XDP come HTML utilizzando il pacchetto di moduli per dispositivi mobili distribuito su CRX, al modulo viene aggiunto anche `FormBridge`JavaScript aggiuntivo, che espone diversi metodi per il salvataggio e l’invio dei dati del modulo.

Questo JavaScript è diverso da quello a cui si fa riferimento in PDF forms in precedenza, ma ha uno scopo simile.

>[!NOTE]
>
>Adobe consiglia di non modificare il contenuto della visualizzazione NewHTMLTaskForm.

## Flex Forms e guide {#flex-forms-and-guides}

Il rendering dei Forms di Flex viene eseguito da SwfTaskForm e il rendering delle guide viene eseguito rispettivamente da HtmlTaskForm Views.

Nell&#39;area di lavoro di AEM Forms, queste visualizzazioni comunicano con il SWF effettivo che costituisce il modulo/guida di Flex® utilizzando un SWF intermedio presente in `/lc/libs/ws/libs/ws/WSNextAdapter.swf`

La comunicazione viene eseguita utilizzando `swfObject.postMessage` / `window.flexMessageHandler`.

Protocollo definito da `WsNextAdapter.swf`. L&#39;oggetto `flexMessageHandlers` esistente nella finestra, da SWF Form aperti in precedenza, viene rimosso prima di aggiungerne uno nuovo. La logica considera anche il passaggio tra la scheda del modulo e la scheda della cronologia nella visualizzazione dei dettagli dell’attività. `WsNextAdapter.swf` viene utilizzato per eseguire varie azioni del modulo, ad esempio Salva o Invia.

>[!NOTE]
>
>Non è consigliabile modificare `WSNextAdapter.swf` o il contenuto della visualizzazione SwfTaskForm/HtmlTaskForm.

## Applicazioni di terze parti (ad esempio, Gestione della corrispondenza) {#third-party-applications-for-example-correspondence-management}

Il rendering delle applicazioni di terze parti viene eseguito utilizzando la vista ExtAppTaskForm.

**Applicazione di terze parti per la comunicazione nell&#39;area di lavoro di AEM Forms**

L&#39;area di lavoro di AEM Forms è in ascolto su `window.global.postMessage([Message],[Payload])`

[Messaggio] può essere una stringa specificata come `SubmitMessage`| `CancelMessage`| `ErrorMessage`| `actionEnabledMessage`in `runtimeMap`. Le applicazioni di terze parti devono utilizzare questa interfaccia per inviare le notifiche necessarie all’area di lavoro di AEM Forms. L’utilizzo di questa interfaccia è obbligatorio perché l’area di lavoro di AEM Forms deve sapere quando l’attività viene inviata in modo da poter pulire la finestra dell’attività.

**Area di lavoro AEM Forms per comunicazioni applicazioni di terze parti**

Se i pulsanti di azione diretta dell&#39;area di lavoro AEM Forms sono visibili, chiama `window.[External-App-Name].getMessage([Action])`, dove `[Action]` viene letto da `routeActionMap`. L&#39;applicazione di terze parti deve essere in ascolto su questa interfaccia e quindi inviare una notifica all&#39;area di lavoro di AEM Forms tramite l&#39;API `postMessage ()`.

Ad esempio, un&#39;applicazione Flex può definire `ExternalInterface.addCallback('getMessage', listener)` per supportare questa comunicazione. Se l&#39;applicazione di terze parti desidera gestire l&#39;invio del modulo tramite i propri pulsanti, è necessario specificare `hideDirectActions = true() in the runtimeMap`. È possibile ignorare questo listener. Pertanto, questo costrutto è facoltativo.

Per ulteriori informazioni sull&#39;integrazione di applicazioni di terze parti relative alla gestione della corrispondenza, consulta [Integrazione della gestione della corrispondenza nell&#39;area di lavoro di AEM Forms](/help/forms/using/integrating-correspondence-management-html-workspace.md).
