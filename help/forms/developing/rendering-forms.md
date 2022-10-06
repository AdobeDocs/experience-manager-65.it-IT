---
title: Rendering di Forms
seo-title: Rendering Forms
description: Utilizzare il servizio Forms per creare applicazioni client di acquisizione dati interattive per convalidare, elaborare, trasformare e distribuire i moduli generalmente creati in Designer. Gli autori dei moduli possono sviluppare una singola struttura del modulo che il servizio Forms esegue in PDF, SWF o HTML in diversi ambienti del browser.
seo-description: Use the Forms service to create interactive data capture client applications that validate, process, transform, and deliver forms typically created in Designer. Form authors can develop a single form design that the Forms service renders in PDF, SWF, or HTML in various browser environments.
uuid: 68d7b7bc-7730-4a83-b7b9-ebe2a29d6c51
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/performing_service_operations_using_apis
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: f8749793-e53f-4812-a093-8278f480e6a8
role: Developer
exl-id: ec9ccf04-7cec-493a-91ab-0e399a905338
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---

# Rendering di Forms {#rendering-forms}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

**Informazioni sul servizio Forms**

Il servizio Forms consente di creare applicazioni client interattive per l’acquisizione di dati che consentono di convalidare, elaborare, trasformare e distribuire i moduli generalmente creati in Designer. Gli autori dei moduli possono sviluppare una singola struttura del modulo che il servizio Forms esegue in PDF, SWF o HTML in diversi ambienti del browser.

Quando un utente finale richiede un modulo, un&#39;applicazione client invia la richiesta al servizio Forms, che restituisce il modulo in un formato appropriato. Non appena il servizio Forms riceve una richiesta, unisce i dati a una struttura del modulo e quindi distribuisce il modulo nel formato desiderato. L’output del servizio Form è un modulo interattivo, in genere un documento PDF. Un modulo interattivo consente agli utenti di compilare i campi presenti nel modulo.

A seconda del tipo di applicazione client, è possibile scrivere il modulo in un browser Web client o salvarlo come file PDF. Un’applicazione basata sul web può scrivere il modulo nel browser web. Un’applicazione desktop può salvare il modulo come file PDF. Per illustrare come eseguire la scrittura in un browser Web e in un file PDF, l’avvio rapido si trova nella *Rendering di Forms* sono organizzate nel modo seguente:

* Gli esempi di API Java fortemente tipizzati (modalità SOAP) sono un servlet Java.
* Gli esempi di servizi web (Java Base64) sono un servlet Java.
* Gli esempi di servizio Web (MTOM) sono un’applicazione console (non tutti gli avvii rapidi hanno un esempio MTOM).

>[!NOTE]
>
>Per informazioni sulla creazione di un&#39;applicazione web che utilizza servlet java per richiamare il servizio Forms, vedi [Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md).

È possibile passare una struttura del modulo (un file XDP) o un documento PDF al servizio Forms in uno dei due modi seguenti:

* È possibile fare riferimento alla struttura del modulo utilizzando un valore URL. Questo approccio comporta l’utilizzo di un `URLSpec` oggetto. La directory principale del contenuto viene trasmessa al servizio Forms utilizzando `URLSpec` dell’oggetto `setContentRootURI` metodo . Nome della struttura del modulo ( `formQuery`) viene passato come parametro separato. I due valori vengono concatenati per ottenere il riferimento assoluto alla struttura del modulo. (La maggior parte degli avvii rapidi si trova nella *Rendering di Forms* utilizza questo approccio.)
* Puoi trasmettere un `com.adobe.idp.Document` che contiene la struttura del modulo al servizio Forms. Due nuovi metodi denominati `renderPDFForm2` e `renderHTMLForm2` accettare `com.adobe.idp.Document` oggetto contenente una struttura del modulo. (Vedi [Trasmissione di documenti al servizio Forms](/help/forms/developing/passing-documents-forms-service.md)

Puoi eseguire queste attività utilizzando il servizio Forms:

* Esegui il rendering dei PDF forms interattivi. (Vedi [Rendering di PDF forms interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md).)
* Eseguire il rendering dei moduli sul client. (Vedi [Rendering di Forms sul client](/help/forms/developing/rendering-forms-client.md).)
* Eseguire il rendering dei moduli in base ai frammenti. (Vedi [Rendering di Forms basato su frammenti](/help/forms/developing/rendering-forms-based-fragments.md).)
* Eseguire il rendering dei moduli abilitati per i diritti. (Vedi [Forms con diritti di rendering](/help/forms/developing/rendering-rights-enabled-forms.md).)
* Eseguire il rendering dei moduli come HTML. (Vedi [Rendering di Forms as HTML](/help/forms/developing/rendering-forms-html.md).)
* Rendering di HTML Forms utilizzando file CSS personalizzati ([Rendering di HTML Forms utilizzando file CSS personalizzati](/help/forms/developing/rendering-html-forms-using-custom.md).)
* Gestire i moduli inviati. (Vedi [Gestione di Forms inviati](/help/forms/developing/handling-submitted-forms.md).)
* Creazione di documenti PDF con dati XML inviati. (Vedi [Creazione di documenti PDF con dati XML inviati](/help/forms/developing/creating-pdf-documents-submitted-xml.md).)
* Precompilare i moduli. (Vedi [Precompilazione di Forms con layout fluidi](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
* Invio di documenti. (Vedi [Trasmissione di documenti al servizio Forms](/help/forms/developing/passing-documents-forms-service.md)
* Calcolare i dati del modulo. (Vedi [Calcolo dei dati del modulo](/help/forms/developing/calculating-form-data.md).)
* Ottimizzare un&#39;applicazione. (Vedi [Ottimizzazione delle prestazioni del servizio Forms](/help/forms/developing/optimizing-performance-forms-service.md).)
