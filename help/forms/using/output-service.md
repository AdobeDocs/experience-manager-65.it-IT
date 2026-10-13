---
title: Servizio di output
description: Descrive il servizio di output, parte di AEM Document Services
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
docset: aem65
feature: Document Services,Output Service
exl-id: 82b0293a-711f-4769-9b11-b4cff4fec021
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 9cc5e18e-2002-58a1-befa-285122cf6653
    internal-label: Output Service
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: f19cff18-c8cc-4a4b-adad-85dd2fa3dbe2
    internal-label: Document Services
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 6%
---
# Servizio di output{#output-service}

## Panoramica {#overview}

Il servizio di output è un servizio OSGi incluso in AEM Document Services. Il servizio di output supporta vari formati di output e funzioni di progettazione dell’output di AEM Forms Designer. Il servizio di output può convertire modelli XFA e dati XML per generare documenti di stampa in vari formati.

Il servizio di output consente di creare applicazioni che permettono di:

* Generare i documenti compilando i file modello con dati XML.
* Genera moduli di output in vari formati, inclusi flussi di stampa non interattivi PDF, PostScript, PCL e ZPL.
* Generare PDF di stampa da PDF modulo XFA.
* Generare in blocco documenti PDF, PostScript, PCL e ZPL unendo più set di dati con i modelli forniti.

>[!NOTE]
>
>Il servizio di output è un&#39;applicazione a 32 bit. In Microsoft Windows, un&#39;applicazione a 32 bit può utilizzare un massimo di 2 GB di memoria. Il limite si applica anche al servizio di output.

## Creazione di documenti modulo non interattivi {#creating-non-interactive-form-documents}

![usingoutput_modified](assets/usingoutput_modified.png)

In genere, si creano modelli utilizzando AEM Forms Designer. Le API `generatePDFOutput` e `generatePrintedOutput` del servizio di output consentono di convertire direttamente questi modelli in vari formati, inclusi PDF, PostScript, ZPL e PCL.

L&#39;operazione `generatePDFOutput` genera PDF, mentre l&#39;operazione `generatePrintedOutput` genera formati PostScript, ZPL e PCL. Il primo parametro di entrambe le operazioni accetta il nome del file modello (ad esempio, `ExpenseClaim.xdp`) o un oggetto Document contenente il modello. Quando si specifica il nome del file modello, specificare anche la directory principale del contenuto come percorso della cartella che contiene il modello. È possibile specificare la directory principale del contenuto utilizzando il parametro `PDFOutputOptions` o `PrintedOutputOptions`. Consulta JavaScript per informazioni dettagliate su altre opzioni che puoi specificare utilizzando questi parametri.

Il secondo parametro accetta un documento XML che viene unito al modello durante la generazione del documento di output.

L&#39;operazione `generatePDFOutput` può inoltre accettare un modulo PDF basato su XFA come input e restituire una versione non interattiva del modulo PDF come output.

## Generazione di documenti modulo non interattivi {#generating-non-interactive-form-documents}

Si consideri uno scenario in cui sono presenti uno o più modelli e più record di dati XML per ciascun modello.

Utilizzare le operazioni `generatePDFOutputBatch` e `generatePrintedOutputBatch` del servizio di output per generare un documento di stampa per ogni record.

È inoltre possibile combinare i record in un unico documento. Entrambe le operazioni richiedono quattro parametri.

Il primo parametro è una mappa che contiene una stringa arbitraria come chiave e il nome del file modello come valore.

Il secondo parametro è un mapping diverso il cui valore è un oggetto Document contenente dati XML. La chiave è la stessa di quella specificata per il primo parametro.

Il terzo parametro per `generatePDFOutputBatch` o `generatePrintedOutputBatch` è rispettivamente di tipo `PDFOutputOptions` o `PrintedOutputOptions`.

I tipi di parametri sono gli stessi dei tipi dei parametri per le operazioni `generatePDFOutput` e `generatePrintedOutput` e hanno lo stesso effetto.

Il quarto parametro è di tipo `BatchOptions`, utilizzato per specificare se è possibile generare un file separato per ogni record. Il valore predefinito di questo parametro è false.

Sia `generatePrintedOutputBatch` che `generatePDFOutputBatch` restituiscono un valore di tipo `BatchResult`. Il valore contiene un elenco di documenti generati. Contiene inoltre un documento di metadati in formato XML che contiene informazioni relative a ciascun documento generato.
