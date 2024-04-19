---
title: Rendering di Forms
description: Utilizzare il servizio Forms per creare applicazioni client di acquisizione dati interattive che convalidano, elaborano, trasformano e distribuiscono moduli generalmente creati in Designer. Gli autori di moduli possono sviluppare un singolo design di moduli eseguito dal servizio Forms in PDF, SWF o HTML in vari ambienti del browser.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/performing_service_operations_using_apis
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
role: Developer
exl-id: ec9ccf04-7cec-493a-91ab-0e399a905338
solution: Experience Manager, Experience Manager Forms
source-git-commit: a28883778c5e8fb90cbbd0291ded17059ab2ba7e
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---

# Rendering di Forms {#rendering-forms}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

**Informazioni sul servizio Forms**

Il servizio Forms consente di creare applicazioni client di acquisizione dati interattive per la convalida, l&#39;elaborazione, la trasformazione e la distribuzione di moduli generalmente creati in Designer. Gli autori di moduli possono sviluppare un singolo design di moduli eseguito dal servizio Forms in PDF, SWF o HTML in vari ambienti del browser.

Quando un utente finale richiede un modulo, un’applicazione client invia la richiesta al servizio Forms, che restituisce il modulo in un formato appropriato. Non appena il servizio Forms riceve una richiesta, unisce i dati con una struttura di modulo e quindi distribuisce il modulo nel formato desiderato. L’output del servizio Modulo è un modulo interattivo, in genere un documento PDF. Un modulo interattivo consente agli utenti di compilare i campi presenti nel modulo.

A seconda del tipo di applicazione client, è possibile scrivere il modulo in un browser Web client o salvarlo come file PDF. Un&#39;applicazione basata sul Web può scrivere il modulo nel browser Web. Un&#39;applicazione desktop può salvare il modulo come file PDF. Per dimostrare come scrivere in un browser Web e in un file PDF, la procedura rapida inizia in *Rendering di Forms* sono organizzate nel modo seguente:

* Gli esempi di API Java fortemente tipizzati (modalità SOAP) sono un servlet Java.
* Gli esempi di servizio web (Java Base64) sono un servlet Java.
* Gli esempi di servizio web (MTOM) sono un’applicazione console (non tutti gli avvii rapidi hanno un esempio MTOM).

>[!NOTE]
>
>Per informazioni sulla creazione di un’applicazione web che utilizza servlet Java per richiamare il servizio Forms, consulta [Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md).

È possibile passare una progettazione di modulo (un file XDP) o un documento PDF al servizio Forms utilizzando uno dei due modi seguenti:

* Puoi fare riferimento alla progettazione del modulo utilizzando un valore URL. Questo approccio comporta l’utilizzo di un `URLSpec` oggetto. La directory principale del contenuto viene passata al servizio Forms utilizzando `URLSpec` dell&#39;oggetto `setContentRootURI` metodo. Il nome della struttura del modulo ( `formQuery`) viene passato come parametro separato. I due valori vengono concatenati per ottenere il riferimento assoluto alla progettazione del modulo. (La maggior parte delle operazioni rapide inizia in *Rendering di Forms* in questa sezione viene utilizzato questo approccio.)
* È possibile passare un `com.adobe.idp.Document` che contiene la struttura del modulo per il servizio Forms. Due nuovi metodi: `renderPDFForm2` e `renderHTMLForm2` accetta un `com.adobe.idp.Document` oggetto che contiene una struttura di modulo. (vedere [Trasmissione di documenti al servizio Forms](/help/forms/developing/passing-documents-forms-service.md)

Puoi eseguire queste attività utilizzando il servizio Forms:

* Eseguire il rendering dei PDF forms interattivi. (vedere [Rendering dei PDF forms interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md).)
* Eseguire il rendering dei moduli nel client. (vedere [Rendering di Forms nel client](/help/forms/developing/rendering-forms-client.md).)
* Eseguire il rendering dei moduli basati su frammenti. (vedere [Rendering di Forms basato su frammenti](/help/forms/developing/rendering-forms-based-fragments.md).)
* Eseguire il rendering dei moduli abilitati per i diritti. (vedere [Forms con diritti di rendering](/help/forms/developing/rendering-rights-enabled-forms.md).)
* Rendering dei moduli come HTML. (vedere [Rendering di Forms come HTML](/help/forms/developing/rendering-forms-html.md).)
* Rendering di HTML Forms tramite file CSS personalizzati ([Rendering di HTML Forms tramite file CSS personalizzati](/help/forms/developing/rendering-html-forms-using-custom.md).)
* Gestisce i moduli inviati. (vedere [Gestione dei Forms inviati](/help/forms/developing/handling-submitted-forms.md).)
* Creazione di documenti PDF con i dati XML inviati. (vedere [Creazione di documenti PDF con i dati XML inviati](/help/forms/developing/creating-pdf-documents-submitted-xml.md).)
* Precompilare i moduli. (vedere [Precompilazione di Forms con layout fluibili](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
* Passaggio di documenti. (vedere [Trasmissione di documenti al servizio Forms](/help/forms/developing/passing-documents-forms-service.md)
* Calcola i dati del modulo. (vedere [Calcolo dati modulo](/help/forms/developing/calculating-form-data.md).)
* Ottimizzare un’applicazione. (vedere [Ottimizzazione delle prestazioni del servizio Forms](/help/forms/developing/optimizing-performance-forms-service.md).)
