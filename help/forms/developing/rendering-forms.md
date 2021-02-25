---
title: Rendering di Forms
seo-title: Rendering di Forms
description: Il servizio Forms consente di creare applicazioni client di acquisizione dei dati interattive per convalidare, elaborare, trasformare e distribuire i moduli generalmente creati in Designer. Gli autori dei moduli possono sviluppare una singola struttura del modulo che il servizio Forms esegue in PDF, SWF o HTML in vari ambienti del browser.
seo-description: Il servizio Forms consente di creare applicazioni client di acquisizione dei dati interattive per convalidare, elaborare, trasformare e distribuire i moduli generalmente creati in Designer. Gli autori dei moduli possono sviluppare una singola struttura del modulo che il servizio Forms esegue in PDF, SWF o HTML in vari ambienti del browser.
uuid: 68d7b7bc-7730-4a83-b7b9-ebe2a29d6c51
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/performing_service_operations_using_apis
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: f8749793-e53f-4812-a093-8278f480e6a8
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---


# Rendering Forms {#rendering-forms}

**Esempi ed esempi in questo documento sono disponibili solo per  AEM Forms nell&#39;ambiente JEE.**

**Informazioni sul servizio Forms**

Il servizio Forms consente di creare applicazioni client interattive per l&#39;acquisizione dei dati che convalidano, elaborano, trasformano e distribuiscono i moduli generalmente creati in Designer. Gli autori dei moduli possono sviluppare una singola struttura del modulo che il servizio Forms esegue in PDF, SWF o HTML in vari ambienti del browser.

Quando un utente finale richiede un modulo, un&#39;applicazione client invia la richiesta al servizio Forms, che restituisce il modulo nel formato appropriato. Non appena il servizio Forms riceve una richiesta, unisce i dati a una struttura del modulo e quindi invia il modulo nel formato desiderato. L&#39;output del servizio Modulo è un modulo interattivo, in genere un documento PDF. Un modulo interattivo consente agli utenti di compilare i campi presenti nel modulo.

A seconda del tipo di applicazione client, è possibile scrivere il modulo in un browser Web client o salvarlo come file PDF. Un&#39;applicazione basata sul Web può scrivere il modulo nel browser Web. Un&#39;applicazione desktop può salvare il modulo come file PDF. Per dimostrare come eseguire la scrittura in un browser Web e in un file PDF, gli avvii rapidi disponibili nella sezione *Rendering Forms* sono organizzati nel modo seguente:

* Gli esempi Java API fortemente tipizzati (modalità SOAP) sono un servlet Java.
* Gli esempi di servizi Web (Java Base64) sono un servlet Java.
* Gli esempi di servizi Web (MTOM) sono un&#39;applicazione console (non tutti gli avvii rapidi hanno un esempio MTOM).

>[!NOTE]
>
>Per informazioni sulla creazione di un&#39;applicazione Web che utilizza servlet Java per richiamare il servizio Forms, vedere [Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md).

È possibile trasmettere una struttura del modulo (un file XDP) o un documento PDF al servizio Forms in uno dei due modi seguenti:

* È possibile fare riferimento alla struttura del modulo utilizzando un valore URL. Questo approccio prevede l&#39;utilizzo di un oggetto `URLSpec`. Il livello principale del contenuto viene passato al servizio Forms utilizzando il metodo `URLSpec` dell&#39;oggetto `setContentRootURI`. Il nome della struttura del modulo ( `formQuery`) viene passato come parametro separato. I due valori vengono concatenati per ottenere il riferimento assoluto alla struttura del modulo. (La maggior parte degli avvii rapidi che si trovano nella sezione *Rendering Forms* utilizza questo approccio.)
* È possibile passare al servizio Forms un `com.adobe.idp.Document` contenente la struttura del modulo. Due nuovi metodi denominati `renderPDFForm2` e `renderHTMLForm2` accettano un oggetto `com.adobe.idp.Document` contenente una struttura del modulo. (Vedere [Trasmissione di documenti al servizio Forms](/help/forms/developing/passing-documents-forms-service.md)

Potete eseguire le seguenti attività utilizzando il servizio Forms:

* Rendering di PDF forms interattivi. (Vedere [Rendering di PDF forms interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md).)
* Eseguire il rendering dei moduli sul client. (Vedere [Rendering di Forms in Client](/help/forms/developing/rendering-forms-client.md).)
* Eseguire il rendering dei moduli in base ai frammenti. (Vedere [Rendering di Forms basato su frammenti](/help/forms/developing/rendering-forms-based-fragments.md).)
* Eseguire il rendering dei moduli abilitati per i diritti. (Vedere [Forms](/help/forms/developing/rendering-rights-enabled-forms.md) con diritti di rendering.)
* Eseguire il rendering dei moduli come HTML. (Vedere [Rendering di Forms come HTML](/help/forms/developing/rendering-forms-html.md).)
* Rendering di Forms HTML con file CSS personalizzati ([Rendering di Forms HTML con file CSS personalizzati](/help/forms/developing/rendering-html-forms-using-custom.md)).
* Gestire i moduli inviati. (Vedere [Gestione di Forms](/help/forms/developing/handling-submitted-forms.md) inviato.)
* Creazione di documenti PDF con dati XML inviati. (Vedere [Creazione di documenti PDF con dati XML inviati](/help/forms/developing/creating-pdf-documents-submitted-xml.md).)
* Precompilare i moduli. (Vedere [Precompilazione di Forms con layout scorrevoli](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
* Invio di documenti. (Vedere [Trasmissione di documenti al servizio Forms](/help/forms/developing/passing-documents-forms-service.md)
* Calcola i dati del modulo. (Vedere [Calcolo dei dati del modulo](/help/forms/developing/calculating-form-data.md).)
* Ottimizzate un&#39;applicazione. (Vedere [Ottimizzazione delle prestazioni del servizio Forms](/help/forms/developing/optimizing-performance-forms-service.md).)

   ***Suggerimento **: Il sito Web  Adobe Developer contiene l&#39;articolo seguente che illustra come creare un&#39;applicazione ASP.NET che esegue il richiamo del servizio Forms ed esegue il rendering dei moduli. Vedere [Creazione di applicazioni ASP.NET per il rendering dei moduli](https://www.adobe.com/devnet/livecycle/articles/asp_net.html).*

