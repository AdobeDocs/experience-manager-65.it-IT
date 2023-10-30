---
title: Informazioni sui processi di AEM Forms
description: I processi di AEM Forms includono la creazione di moduli, l’invio, la gestione dei dati, la convalida, l’integrazione, l’automazione dei flussi di lavoro e la gestione degli output.
uuid: 7cbebe7d-f222-42fa-8eb6-d2443458a791
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: development-tools, coding
discoiquuid: ac9fe461-63e7-442b-bd1c-eb9576ef55aa
role: Developer
exl-id: 434ac316-8a01-43a6-844b-1b792f60fa21
source-git-commit: 20b0d0db54dc30285c056a10032f02ba45f8baca
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 0%

---

# Informazioni sui processi di AEM Forms {#understanding-aem-forms-processes}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

Un caso d’uso comune prevede che un set di servizi AEM Forms funzioni su un singolo documento. Puoi inviare una richiesta al contenitore del servizio creando un processo utilizzando Workbench. Un processo rappresenta un processo aziendale che si sta automatizzando. Per informazioni sulla creazione di processi, consulta [Utilizzo di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).

Una volta attivato, il processo diventa un servizio e può essere richiamato come altri servizi. Una differenza tra un servizio standard, ad esempio Crittografia, e un servizio che ha avuto origine da un processo, è che quest&#39;ultimo ha un&#39;operazione che esegue molte azioni. Al contrario, un servizio standard ha molte operazioni. Ogni operazione in genere esegue un&#39;azione, ad esempio l&#39;applicazione di una policy a un documento o la crittografia di un documento.

I processi possono essere di breve durata o di lunga durata. Un processo di breve durata è un&#39;operazione eseguita in modo sincrono e sullo stesso thread di esecuzione da cui è stato richiamato. Le operazioni di breve durata sono paragonabili al comportamento standard rilevato nella maggior parte dei linguaggi di programmazione, in cui un&#39;applicazione client chiama un metodo e attende un valore restituito.

Tuttavia, in alcune situazioni un processo non può essere completato in modo sincrono a causa di fattori quali:

* Un processo può richiedere molto tempo.
* Un processo può estendersi oltre i confini dell’organizzazione.
* Per completare un processo è necessario un input esterno. Si consideri ad esempio una situazione in cui un modulo viene inviato a un manager fuori sede. In questa situazione, il processo non viene completato fino a quando il manager non restituisce e compila il modulo.

  Questi tipi di processi sono noti come processi di lunga durata. Un processo di lunga durata viene eseguito in modo asincrono, consentendo ai sistemi di interagire quando le risorse lo consentono e consentendo il tracciamento e il monitoraggio dell&#39;operazione. Quando viene richiamato un processo di lunga durata, AEM Forms crea un valore di identificativo di chiamata come parte di un record che tiene traccia dello stato del processo di lunga durata. Il record viene memorizzato nel database di AEM Forms. È possibile eliminare i record di processi di lunga durata quando non sono più necessari.

>[!NOTE]
>
>AEM Forms non crea un record quando viene richiamato un processo di breve durata.

Utilizzando il valore dell&#39;identificatore di chiamata, è possibile tenere traccia dello stato del processo di lunga durata. Ad esempio, è possibile utilizzare il valore dell&#39;identificatore di chiamata del processo per eseguire operazioni di Gestione processi, ad esempio la chiusura di un&#39;istanza del processo in esecuzione.

**Esempio di processo di breve durata**

L’illustrazione seguente è un esempio di processo di breve durata denominato *MyApplication/EncryptDocument*.

>[!NOTE]
>
>Questo processo non è basato su un processo AEM Forms esistente. Per seguire insieme agli esempi di codice che illustrano come richiamare questo processo, creare un processo denominato `MyApplication/EncryptDocument` utilizzando Workbench. (vedere [Utilizzo di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Quando viene richiamato, questo processo di breve durata esegue le azioni seguenti:

1. Ottiene il documento PDF non protetto passato al processo come valore di input.
1. Crittografa il documento PDF con una password. Il nome del parametro di input per questo processo è `inDoc` e il tipo di dati è document.
1. Salva il documento PDF crittografato con password come file PDF nel file system locale. Questo processo restituisce il documento PDF crittografato come valore di output. Il nome del parametro di output per questo processo è `outDoc` e il tipo di dati è document.

   Questo processo viene completato in modo sincrono sullo stesso thread di esecuzione da cui è stato richiamato. Il nome di questo processo di breve durata è `MyApplication/EncryptDocument`e il suo funzionamento è `invoke`.

   >[!NOTE]
   >
   >In genere, un processo di breve durata è costituito da più di tre azioni. È possibile creare un processo utilizzando Workbench. (vedere [Utilizzo di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

   *Programmazione con i moduli AEM* descrive i seguenti modi in cui è possibile richiamare a livello di programmazione questo processo di breve durata:

   * [Richiamare un processo di breve durata passando un documento non sicuro tramite AEM Forms Remoting](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-a-short-lived-process-by-passing-an-unsecure-document-using-remoting) (Utilizzo di un’applicazione Flex)
   * [Richiamare un processo di breve durata utilizzando l’API di richiamo](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-short-lived-process-using-the-invocation-api) (API Java Invocation)
   * [Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding) (esempio di servizio web)
   * [Richiamare AEM Forms tramite MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom) (esempio di servizio web)
   * [Richiamare AEM Forms con SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref) (esempio di servizio web)
   * [Richiamare AEM Forms utilizzando i dati BLOB su HTTP](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http) (esempio di servizio web)
   * [Richiamare AEM Forms utilizzando DIME](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-dime) (esempio di servizio web)
   * [Richiamare il processo MyApplication/EncryptDocument tramite REST](/help/forms/developing/invoking-aem-forms-using-rest.md)

**Esempio di processo di lunga durata**

L’illustrazione seguente è un esempio di processo di lunga durata.

Questo processo viene richiamato quando un richiedente presenta un modulo di prestito. Il processo non è completo finché un responsabile del prestito non approva o rifiuta la richiesta di prestito. Il nome di questo processo di lunga durata è *FirstAppSolution/PreLoanProcess* e il suo funzionamento è `invoke_Async`. Questo processo deve essere richiamato in modo asincrono. Per informazioni sul richiamo programmatico di questo processo di lunga durata, consulta [Richiamare processi a lunga durata incentrati sull&#39;uomo](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

>[!NOTE]
>
>Questo processo può essere creato seguendo l’esercitazione specificata in [Creazione della prima applicazione AEM Forms](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63).
