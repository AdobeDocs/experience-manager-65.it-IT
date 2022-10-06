---
title: Servizio Forms
seo-title: Forms Service
description: L’articolo descrive il servizio Forms e le attività relative ai moduli che è possibile eseguire utilizzando il servizio Forms.
seo-description: The article describes Forms service and the form-related tasks you can perform using Forms service.
uuid: 3258d3c2-8755-4815-8c97-b2cfb9a9dfd4
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: a9695d10-43ec-40eb-942f-7720abaa0973
exl-id: bd1216e4-2248-484b-a3c1-c209da4ff94f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 9%

---

# Servizio Forms {#forms-service}

## Panoramica {#overview}

Il servizio Forms consente di creare applicazioni client interattive per l’acquisizione di dati che consentono di convalidare, elaborare, trasformare e distribuire i moduli generalmente creati in Designer. Il servizio Forms esegue il rendering come documento PDF di qualsiasi struttura del modulo sviluppato dall’utente.

Il servizio Forms consente inoltre alle organizzazioni di estendere i processi intelligenti di acquisizione dei dati mediante la distribuzione di moduli elettronici come PDF Adobi. Puoi inoltre utilizzare il servizio per importare ed esportare i dati rispettivamente da e verso PDF forms esistenti.

Utilizza il servizio Forms per effettuare le seguenti operazioni:

* Esegui il rendering dei PDF forms in base ai dati XML e ai modelli.
* Abilita l’integrazione dei dati del modulo per importare ed estrarre dati dai PDF forms.
* Eseguire il rendering dei moduli in base ai frammenti.

## Creazione di PDF forms  {#creating-pdf-forms-nbsp}

Utilizza il servizio Form per creare PDF forms per l’acquisizione dei dati. In genere si inizia con un modello di AEM Forms Designer. Utilizza la `renderPDFForm` (collegamento a Javadoc) operazione del servizio Forms per convertire questo modello in un modulo PDF.

Il primo parametro della `renderPDFForm` operation è il nome del file modello (ad esempio, `ExpenseClaim.xdp`). Puoi archiviare il file modello in un file system locale, in un archivio CRX o in una posizione HTTP o FTP. È possibile specificare la posizione del file modello impostando la directory principale del contenuto nel `PDFFormRenderOptions` del `renderPDFForm` funzionamento. Vedi Javadoc per i dettagli di altre opzioni che puoi specificare per `PDFFormRenderOptions` parametro .

La `renderPDFForm` può anche accettare dati XML. I dati XML vengono uniti al modello durante la creazione di un modulo PDF in modo che il modulo PDF generato contenga i dati specificati. Il secondo parametro per `renderPDFForm` può accettare un oggetto Document (Javadoc) contenente dati XML.

## Estrazione di dati dai PDF forms  {#extracting-data-from-pdf-forms-nbsp}

Utilizza la `exportData` (Javadoc) operazione del servizio Forms per estrarre dati XML da un modulo PDF. Questa operazione accetta un documento come primo parametro. È possibile esportare i dati come un documento XDP o un file XML. Se si esportano i dati come file XML, i dati esportati rimuovono la busta XDP e restituiscono un file XML semplice. Potete specificare questa disposizione utilizzando il secondo parametro.

## Importazione di dati in PDF forms {#importing-data-into-pdf-forms}

Il servizio Forms consente inoltre di unire un modulo PDF creato con AEM Forms Designer o con `renderPDFForm` con dati XML. La `importData` (Javadoc) il funzionamento del servizio Forms accetta il modulo PDF e i dati XML e restituisce un modulo PDF con dati XML.

## Rendering di moduli basati su frammenti {#rendering-forms-based-on-fragments}

Il servizio Forms può eseguire il rendering dei moduli in base ai frammenti creati con AEM Forms Designer. Un frammento è una parte riutilizzabile di un modulo. Viene salvato come file XDP separato che può essere inserito in più strutture del modulo. Ad esempio, un frammento può contenere un blocco indirizzo o note legali.

L’utilizzo dei frammenti semplifica e velocizza la creazione e la manutenzione di un numero elevato di moduli. Durante la creazione di un modulo, inserire un riferimento al frammento richiesto per consentirne la visualizzazione nel modulo. Il riferimento al frammento contiene un sottomodulo che punta al file XDP fisico.

Di seguito sono riportati i vantaggi dell’utilizzo dei frammenti:

* **Riutilizzo dei contenuti**: È possibile riutilizzare il contenuto in più strutture del modulo. Per riutilizzare rapidamente parti dello stesso contenuto in più moduli, creare un frammento. Copiare o ricreare il contenuto richiede più tempo. I frammenti garantiscono inoltre che le parti di un modello di modulo usate di frequente siano uniformi, per aspetto e contenuto, in tutti i moduli che vi fanno riferimento.
* **Aggiornamenti globali**: È possibile apportare modifiche globali a più moduli una sola volta in un file. È possibile modificare il contenuto, gli oggetti script, i binding dei dati, il layout o gli stili di un frammento. Tutti i moduli XDP che fanno riferimento al frammento riflettono le modifiche apportate.
* **Creazione di moduli condivisi**: Puoi condividere la creazione di moduli tra diverse risorse. Gli sviluppatori di moduli che dispongono di conoscenze in materia di script o di altre funzioni avanzate di AEM Forms Designer possono sviluppare e condividere frammenti che utilizzano proprietà dinamiche e script. I progettisti di moduli possono utilizzare i frammenti per progettare i moduli. Inoltre, è possibile utilizzare i frammenti per garantire che tutte le parti di un modulo abbiano aspetto e funzionalità uniformi in più moduli.
