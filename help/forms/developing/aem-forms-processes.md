---
title: Informazioni sui processi AEM Forms
seo-title: Understanding AEM Forms Processes
description: Informazioni sui processi AEM Forms
uuid: 7cbebe7d-f222-42fa-8eb6-d2443458a791
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: development-tools, coding
discoiquuid: ac9fe461-63e7-442b-bd1c-eb9576ef55aa
role: Developer
exl-id: 434ac316-8a01-43a6-844b-1b792f60fa21
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 0%

---

# Informazioni sui processi AEM Forms {#understanding-aem-forms-processes}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

Un caso d’uso comune è quello di un set di servizi AEM Forms che operano su un singolo documento. Puoi inviare una richiesta al contenitore del servizio creando un processo utilizzando Workbench. Un processo rappresenta un processo aziendale automatizzato. Per informazioni sulla creazione dei processi, consulta [Utilizzo di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

Quando un processo viene attivato, diventa un servizio e può essere richiamato come altri servizi. Una differenza tra un servizio standard, ad esempio il servizio di cifratura e un servizio originato da un processo, è che quest&#39;ultimo dispone di un&#39;operazione che esegue molte azioni. Al contrario, un servizio standard ha molte operazioni. In genere, ogni operazione esegue una sola azione, ad esempio l&#39;applicazione di un criterio a un documento o la cifratura di un documento.

I processi possono essere di breve durata o di lunga durata. Un processo di breve durata è un’operazione eseguita in modo sincrono e sullo stesso thread di esecuzione da cui è stata richiamata. Le operazioni di breve durata sono paragonabili al comportamento standard rilevato nella maggior parte dei linguaggi di programmazione, in cui un&#39;applicazione client chiama un metodo e attende un valore di ritorno.

Tuttavia, in alcune situazioni un processo non può essere completato in modo sincrono a causa di fattori come questi:

* Un processo può avere un periodo di tempo significativo.
* Un processo può superare i limiti organizzativi.
* Per completare un processo, è necessario un input esterno. Ad esempio, si consideri una situazione in cui un modulo viene inviato a un responsabile che non è in ufficio. In questa situazione, il processo non viene completato finché il responsabile non restituisce e compila il modulo.

   Questi tipi di processi sono noti come processi longevi. Un processo di lunga durata viene eseguito in modo asincrono, consentendo ai sistemi di interagire come le risorse lo consentono e consentendo il tracciamento e il monitoraggio dell&#39;operazione. Quando si richiama un processo di lunga durata, AEM Forms crea un valore di identificatore di chiamata come parte di un record che tiene traccia dello stato del processo di lunga durata. Il record viene memorizzato nel database AEM Forms. È possibile eliminare i record di processo di lunga durata quando non sono più necessari.

>[!NOTE]
>
>AEM Forms non crea un record quando si richiama un processo di breve durata.

Utilizzando il valore dell&#39;identificatore di chiamata, puoi tenere traccia dello stato del processo di lunga durata. Ad esempio, è possibile utilizzare il valore dell&#39;identificatore di chiamata del processo per eseguire operazioni di Process Manager, ad esempio la terminazione di un&#39;istanza di processo in esecuzione.

**Esempio di processo a breve termine**

L’illustrazione seguente è un esempio di processo di breve durata denominato *MyApplication/EncryptDocument*.

>[!NOTE]
>
>Questo processo non è basato su un processo AEM Forms esistente. Per seguire gli esempi di codice che illustrano come richiamare questo processo, crea un processo denominato `MyApplication/EncryptDocument` utilizzo di Workbench. (Vedi [Utilizzo di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Quando si richiama questo processo di breve durata, vengono eseguite le azioni seguenti:

1. Ottiene il documento PDF non protetto passato al processo come valore di input.
1. Cifra il documento PDF con una password. Il nome del parametro di input per questo processo è `inDoc` e il tipo di dati è document.
1. Salva il documento PDF crittografato con password come file PDF nel file system locale. Questo processo restituisce il documento PDF crittografato come valore di output. Il nome del parametro di output per questo processo è `outDoc` e il tipo di dati è document.

   Questo processo viene completato in modo sincrono sullo stesso thread di esecuzione da cui è stato richiamato. Il nome di questo processo di breve durata è `MyApplication/EncryptDocument`e il suo funzionamento `invoke`.

   >[!NOTE]
   >
   >In genere, un processo di breve durata consiste in più di tre azioni. È possibile creare un processo utilizzando Workbench. (Vedi [Utilizzo di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

   *Programmazione con moduli AEM* descrive i seguenti modi in cui è possibile richiamare questo processo di breve durata a livello di programmazione:

   * [Richiamare un processo di breve durata passando un documento non sicuro utilizzando AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting) (Utilizzo di un&#39;applicazione Flex)
   * [Richiamare un processo di breve durata utilizzando l’API di richiamo](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-short-lived-process-using-the-invocation-api) (API Java Invocation)
   * [Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding) (esempio di servizio Web)
   * [Richiamo di AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom) (esempio di servizio Web)
   * [Richiamo di AEM Forms tramite SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref) (esempio di servizio Web)
   * [Richiamo di dati AEM Forms tramite BLOB su HTTP](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http) (esempio di servizio Web)
   * [Richiamo di AEM Forms tramite DIME](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-dime) (esempio di servizio Web)
   * [Richiamo del processo MyApplication/EncryptDocument tramite REST](/help/forms/developing/invoking-aem-forms-using-rest.md)

**Esempio di processo a lungo termine**

L&#39;illustrazione seguente è un esempio di processo di lunga durata.

Questo processo viene invocato quando un richiedente presenta un modulo di prestito. Il processo non è completo finché un funzionario responsabile del prestito non approva o rifiuta la richiesta di prestito. Il nome di questo processo di lunga vita è *FirstAppSolution/PreLoanProcess* e il suo funzionamento `invoke_Async`. Questo processo deve essere richiamato in modo asincrono. Per informazioni su come richiamare questo processo a lungo termine a livello di programmazione, vedi [Richiamo dei processi a lunga durata incentrati sull&#39;uomo](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

>[!NOTE]
>
>Puoi creare questo processo seguendo l’esercitazione specificata in [Creazione della prima applicazione AEM Forms](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63).
