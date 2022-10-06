---
title: Servizio di output
seo-title: Output Service
description: Descrive il servizio di output, che fa parte di AEM Document Services
seo-description: Describes Output Service, which is part of AEM Document Services
uuid: edddef59-b43c-486f-8734-3f97961ecf4d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 51ab91ff-c0c0-4165-ae02-f306e45eea03
docset: aem65
exl-id: 1b62e1c1-428d-4c0f-98a8-486f319fa581
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 2%

---

# Servizio di output{#output-service}

## Panoramica {#overview}

Il servizio di output è un servizio OSGi che fa parte di AEM Document Services. Il servizio di output supporta vari formati di output e funzioni di progettazione dell’output di AEM Forms Designer. Il servizio di output può convertire modelli XFA e dati XML per generare documenti di stampa in vari formati.

Il servizio di output consente di creare applicazioni che consentono di:

* Generare documenti modulo finali compilando i file modello con dati XML.
* Genera moduli di output in vari formati, inclusi flussi di stampa non interattivi PDF, PostScript, PCL e ZPL.
* Genera PDF di stampa da PDF modulo XFA.
* Genera in blocco documenti PDF, PostScript, PCL e ZPL unendo più set di dati con i modelli forniti.

>[!NOTE]
>
>Il servizio di output è un&#39;applicazione a 32 bit. Su Microsoft Windows, un&#39;applicazione a 32 bit può utilizzare un massimo di 2 GB di memoria. Il limite si applica anche al servizio di output.

## Creazione di documenti modulo non interattivi {#creating-non-interactive-form-documents}

![usingoutput_modified](assets/usingoutput_modified.png)

In genere si creano modelli con AEM Forms Designer. La `generatePDFOutput` e `generatePrintedOutput` Le API del servizio Output consentono di convertire direttamente questi modelli in vari formati, tra cui PDF, PostScript, ZPL e PCL.

La `generatePDFOutput` l&#39;operazione genera PDF mentre il `generatePrintedOutput` Questa operazione genera i formati PostScript, ZPL e PCL. Il primo parametro di entrambe le operazioni accetta il nome del file modello (ad esempio `ExpenseClaim.xdp`) o un oggetto Document contenente il modello. Quando specifichi il nome del file modello, specifica anche la directory principale del contenuto come percorso della cartella che contiene il modello. È possibile specificare la directory principale del contenuto utilizzando `PDFOutputOptions` o `PrintedOutputOptions` parametro . Consulta Javadoc per i dettagli di altre opzioni che puoi specificare utilizzando questi parametri.

Il secondo parametro accetta un documento XML unito al modello durante la generazione del documento di output.

La `generatePDFOutput` può inoltre accettare un modulo PDF basato su XFA come input e restituire una versione non interattiva del modulo PDF come output.

## Generazione di documenti modulo non interattivi {#generating-non-interactive-form-documents}

Considerare uno scenario in cui si dispone di uno o più modelli e più record di dati XML per ciascun modello.

Utilizza la `generatePDFOutputBatch` e `generatePrintedOutputBatch` operazioni del servizio Output per generare un documento di stampa per ogni record.

È inoltre possibile combinare i record in un unico documento. Entrambe le operazioni richiedono quattro parametri.

Il primo parametro è una mappa che contiene una stringa arbitraria come chiave e il nome del file modello come valore.

Il secondo parametro è una mappa diversa il cui valore è un oggetto Document che contiene dati XML. La chiave è la stessa specificata per il primo parametro.

Il terzo parametro per `generatePDFOutputBatch` o `generatePrintedOutputBatch` è di tipo `PDFOutputOptions` o `PrintedOutputOptions` rispettivamente.

I tipi di parametri sono gli stessi dei tipi dei parametri per `generatePDFOutput` e `generatePrintedOutput` e hanno lo stesso effetto.

Il quarto parametro è di tipo `BatchOptions`, che consente di specificare se è possibile generare un file separato per ogni record. Il valore predefinito di questo parametro è false.

Entrambi `generatePrintedOutputBatch` e `generatePDFOutputBatch` restituisce un valore di tipo `BatchResult`. Il valore contiene un elenco di documenti generati. Contiene inoltre un documento con metadati in formato XML contenente informazioni relative a ciascun documento generato.
