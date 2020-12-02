---
title: Servizio di output
seo-title: Servizio di output
description: Descrive Output Service, che fa parte di AEM Document Services
seo-description: Descrive Output Service, che fa parte di AEM Document Services
uuid: edddef59-b43c-486f-8734-3f97961ecf4d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 51ab91ff-c0c0-4165-ae02-f306e45eea03
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---


# Servizio di output{#output-service}

## Panoramica {#overview}

Il servizio di output è un servizio OSGi che fa parte di AEM Document Services. Il servizio Output supporta vari formati di output e le funzionalità di progettazione dell&#39;output di  AEM Forms Designer. Il servizio di output può convertire i modelli XFA e i dati XML per generare documenti di stampa in vari formati.

Il servizio di output consente di creare applicazioni che consentono di:

* Generare documenti modulo finali compilando i file modello con dati XML.
* Generazione di moduli di output in vari formati, inclusi flussi di stampa PDF non interattivi, PostScript, PCL e ZPL.
* Generazione di PDF per la stampa dai PDF dei moduli XFA.
* Generate documenti PDF, PostScript, PCL e ZPL in blocco unendo più set di dati ai modelli forniti.

>[!NOTE]
>
>Il servizio di output è un&#39;applicazione a 32 bit. In Microsoft Windows, un&#39;applicazione a 32 bit può utilizzare un massimo di 2 GB di memoria. Il limite si applica anche al servizio di output.

## Creazione di documenti modulo non interattivi {#creating-non-interactive-form-documents}

![usingoutput_modified](assets/usingoutput_modified.png)

In genere, i modelli vengono creati utilizzando  AEM Forms Designer. Le `generatePDFOutput` e `generatePrintedOutput` API del servizio Output consentono di convertire direttamente questi modelli in vari formati, inclusi PDF, PostScript, ZPL e PCL.

L&#39;operazione `generatePDFOutput` genera PDF, mentre l&#39;operazione `generatePrintedOutput` genera formati PostScript, ZPL e PCL. Il primo parametro di entrambe le operazioni accetta il nome del file modello (ad esempio `ExpenseClaim.xdp`) o un oggetto Document che contiene il modello. Quando specificate il nome del file modello, specificate anche la directory principale del contenuto come percorso della cartella che contiene il modello. È possibile specificare la radice del contenuto utilizzando il parametro `PDFOutputOptions` o `PrintedOutputOptions`. Per informazioni dettagliate sulle altre opzioni che potete specificare utilizzando questi parametri, consultate Javadoc.

Il secondo parametro accetta un documento XML unito al modello durante la generazione del documento di output.

L&#39;operazione `generatePDFOutput` può inoltre accettare come input un modulo PDF basato su XFA e restituire una versione non interattiva del modulo PDF come output.

## Generazione di documenti modulo non interattivi {#generating-non-interactive-form-documents}

Considerare uno scenario in cui sono disponibili uno o più modelli e più record di dati XML per ciascun modello.

Utilizzare le operazioni `generatePDFOutputBatch` e `generatePrintedOutputBatch` del servizio Output per generare un documento di stampa per ciascun record.

È inoltre possibile combinare i record in un singolo documento. Entrambe le operazioni richiedono quattro parametri.

Il primo parametro è una mappa che contiene una stringa arbitraria come chiave e il nome del file modello come valore.

Il secondo parametro è una mappa diversa il cui valore è un oggetto Document che contiene dati XML. La chiave è la stessa specificata per il primo parametro.

Il terzo parametro per `generatePDFOutputBatch` o `generatePrintedOutputBatch` è di tipo `PDFOutputOptions` o `PrintedOutputOptions` rispettivamente.

I tipi di parametri sono gli stessi tipi dei parametri per le operazioni `generatePDFOutput` e `generatePrintedOutput` e hanno lo stesso effetto.

Il quarto parametro è di tipo `BatchOptions`, che consente di specificare se è possibile generare un file separato per ciascun record. Il valore predefinito di questo parametro è false.

Sia `generatePrintedOutputBatch` che `generatePDFOutputBatch` restituiscono un valore di tipo `BatchResult`. Il valore contiene un elenco di documenti generati. Contiene inoltre un documento di metadati in formato XML che contiene informazioni relative a ciascun documento generato.
