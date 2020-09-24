---
title: Informazioni  processi AEM Forms
seo-title: Informazioni  processi AEM Forms
description: 'null'
seo-description: 'null'
uuid: 7cbebe7d-f222-42fa-8eb6-d2443458a791
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: development-tools, coding
discoiquuid: ac9fe461-63e7-442b-bd1c-eb9576ef55aa
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 0%

---


# Informazioni  processi AEM Forms {#understanding-aem-forms-processes}

Un caso d’uso comune è rappresentato dal fatto che un insieme di servizi AEM Forms  funzionare su un singolo documento. È possibile inviare una richiesta al contenitore dei servizi creando un processo utilizzando Workbench. Un processo rappresenta un processo aziendale automatizzato. Per informazioni sulla creazione di processi, vedere [Uso di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

Una volta attivato, il processo diventa un servizio e può essere invocato come altri servizi. Una differenza tra un servizio standard, come il servizio di cifratura e un servizio originato da un processo, è che quest&#39;ultimo dispone di un&#39;operazione che esegue molte azioni. Al contrario, un servizio standard ha molte operazioni. In genere, ogni operazione esegue un&#39;azione, ad esempio l&#39;applicazione di un criterio a un documento o la cifratura di un documento.

I processi possono essere di breve durata o di lunga durata. Un processo di breve durata è un&#39;operazione eseguita in modo sincrono e sullo stesso thread di esecuzione da cui è stata richiamata. Le operazioni di breve durata sono paragonabili al comportamento standard riscontrato nella maggior parte dei linguaggi di programmazione, in cui un&#39;applicazione client chiama un metodo e attende un valore restituito.

Tuttavia, in alcuni casi non è possibile completare un processo in modo sincrono a causa di fattori quali:

* Un processo può durare un periodo di tempo significativo.
* Un processo può estendersi oltre i limiti organizzativi.
* Per completare un processo, è necessario un input esterno. Si consideri, ad esempio, una situazione in cui un modulo viene inviato a un manager che non è in ufficio. In questa situazione, il processo non è completo finché il manager non restituisce e compila il modulo.

   Questi tipi di processi sono noti come processi longevi. Un processo di lunga durata viene eseguito in modo asincrono, consentendo ai sistemi di interagire come le risorse lo consentono e consentendo il monitoraggio e il monitoraggio dell&#39;operazione. Quando viene richiamato un processo di lunga durata,  AEM Forms crea un valore identificativo di chiamata come parte di un record che tiene traccia dello stato del processo di lunga durata. Il record viene memorizzato nel database AEM Forms . È possibile eliminare i record di processo di lunga durata quando non sono più necessari.

>[!NOTE]
>
> AEM Forms non crea un record quando viene richiamato un processo di breve durata.

Utilizzando il valore dell’identificatore di chiamata, potete tenere traccia dello stato del processo di lunga durata. Ad esempio, è possibile utilizzare il valore dell&#39;identificatore di chiamata del processo per eseguire operazioni di Process Manager, ad esempio la terminazione di un&#39;istanza di processo in esecuzione.

**Esempio di processo di breve durata**

L&#39;illustrazione seguente è un esempio di un processo di breve durata denominato *MyApplication/EncryptDocument*.

>[!NOTE]
>
>Questo processo non è basato su un processo AEM Forms  esistente. Per seguire gli esempi di codice che illustrano come richiamare questo processo, creare un processo denominato `MyApplication/EncryptDocument` utilizzando Workbench. (Vedere [Uso di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Quando viene richiamato questo processo di breve durata, esegue le azioni seguenti:

1. Ottiene il documento PDF non protetto che viene passato al processo come valore di input.
1. Cifra il documento PDF con una password. Il nome del parametro di input per questo processo è `inDoc` e il tipo di dati è document.
1. Salva il documento PDF crittografato con password come file PDF nel file system locale. Questo processo restituisce il documento PDF crittografato come valore di output. Il nome del parametro di output per questo processo è `outDoc` e il tipo di dati è document.

   Questo processo viene completato in modo sincrono sullo stesso thread di esecuzione da cui è stato richiamato. Il nome di questo processo di breve durata è `MyApplication/EncryptDocument`e il suo funzionamento è `invoke`.

   >[!NOTE]
   >
   >In genere, un processo di breve durata consiste di più di tre azioni. È possibile creare un processo utilizzando Workbench. (Vedere [Uso di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

   *La programmazione con AEM* moduli descrive i seguenti modi in cui è possibile invocare questo processo di breve durata a livello di programmazione:

   * [Richiamo di un processo di breve durata passando un documento non sicuro utilizzando  AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting) (utilizzando un&#39;applicazione Flex)
   * [Richiamo di un processo di breve durata tramite l&#39;API](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-short-lived-process-using-the-invocation-api) di incitamento (Java Invocation API)
   * [Richiamo  AEM Forms con codifica](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding) Base64 (esempio di servizio Web)
   * [Chiamata  AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom) (esempio di servizio Web)
   * [Chiamata  AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref) (esempio di servizio Web)
   * [Chiamata  AEM Forms tramite dati BLOB su HTTP](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http) (esempio di servizio Web)
   * [Chiamata  AEM Forms tramite DIME](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-dime) (esempio di servizio Web)
   * [Richiamo del processo MyApplication/EncryptDocument tramite REST](/help/forms/developing/invoking-aem-forms-using-rest.md)

**Esempio di processo longevo**

L&#39;illustrazione seguente è un esempio di processo di lunga durata.

Questa procedura viene invocata quando un richiedente presenta un modulo di prestito. Il processo non è completo finché un funzionario del prestito non approva o rifiuta la richiesta di prestito. Il nome di questo processo longevo è *FirstAppSolution/PreLoanProcess* e il suo funzionamento è `invoke_Async`. Questo processo deve essere richiamato in modo asincrono. Per informazioni su come invocare questo processo a lungo termine a livello di programmazione, vedere [Richiamo di processi](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)a vita lunga incentrati sull’uomo.

>[!NOTE]
>
>Questo processo può essere creato seguendo l&#39;esercitazione specificata in [Creazione della prima applicazione](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63)AEM Forms .