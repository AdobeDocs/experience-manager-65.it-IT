---
title: Servizio Forms
seo-title: Servizio Forms
description: L'articolo descrive il servizio Forms e le attività relative ai moduli che è possibile eseguire utilizzando il servizio Forms.
seo-description: L'articolo descrive il servizio Forms e le attività relative ai moduli che è possibile eseguire utilizzando il servizio Forms.
uuid: 3258d3c2-8755-4815-8c97-b2cfb9a9dfd4
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: a9695d10-43ec-40eb-942f-7720abaa0973
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 9%

---


# Servizio Forms {#forms-service}

## Panoramica {#overview}

Il servizio Forms consente di creare applicazioni client interattive per l&#39;acquisizione dei dati che convalidano, elaborano, trasformano e distribuiscono i moduli generalmente creati in Designer. Il servizio Forms esegue il rendering come documenti PDF di qualsiasi struttura del modulo sviluppata dall&#39;utente.

Il servizio Forms consente inoltre alle organizzazioni di sviluppare le procedure avanzate di acquisizione dei dati in uso mediante la distribuzione di moduli elettronici  file PDF di Adobe. È inoltre possibile utilizzare il servizio per importare ed esportare i dati rispettivamente da e verso PDF forms esistenti.

Utilizzate il servizio Forms per effettuare le seguenti operazioni:

* Eseguire il rendering dei PDF forms in base ai dati XML e ai modelli.
* Abilitare l&#39;integrazione dei dati del modulo per importare ed estrarre dati dai PDF forms.
* Eseguire il rendering dei moduli in base ai frammenti.

## Creazione di PDF forms  {#creating-pdf-forms-nbsp}

Utilizzare il servizio Modulo per creare PDF forms per l&#39;acquisizione dei dati. In genere si inizia con un modello  AEM Forms Designer. Per convertire il modello in un modulo PDF, utilizzare l&#39;operazione `renderPDFForm` (collegamento a Javadoc) del servizio Forms.

Il primo parametro dell&#39;operazione `renderPDFForm` è il nome del file modello (ad esempio, `ExpenseClaim.xdp`). È possibile archiviare il file modello in un file system locale, nell&#39;archivio CRX o in un percorso HTTP o FTP. Potete specificare la posizione del file modello impostando la directory principale del contenuto nel parametro `PDFFormRenderOptions` dell&#39;operazione `renderPDFForm`. Per informazioni dettagliate sulle altre opzioni che è possibile specificare per il parametro `PDFFormRenderOptions`, consultate Javadoc.

L&#39;operazione `renderPDFForm` può inoltre accettare dati XML. Durante la creazione di un modulo PDF, i dati XML vengono uniti al modello in modo che il modulo PDF generato contenga i dati specificati. Il secondo parametro per l&#39;operazione `renderPDFForm` può accettare un oggetto Document (Javadoc) che contiene dati XML.

## Estrazione di dati dai PDF forms  {#extracting-data-from-pdf-forms-nbsp}

Utilizzare l&#39;operazione `exportData` (Javadoc) del servizio Forms per estrarre dati XML da un modulo PDF. Questa operazione accetta un documento come primo parametro. È possibile esportare i dati come documento XDP o file XML. Se esportate i dati come file XML, i dati esportati rimuovono la busta XDP e restituiscono un file XML semplice. Potete specificare questa disposizione utilizzando il secondo parametro.

## Importazione di dati in PDF forms {#importing-data-into-pdf-forms}

Il servizio Forms consente inoltre di unire un modulo PDF creato utilizzando  AEM Forms Designer o l&#39;operazione `renderPDFForm` con dati XML. L&#39;operazione `importData` (Javadoc) del servizio Forms accetta il modulo PDF e i dati XML e restituisce un modulo PDF con dati XML.

## Rendering di moduli basati su frammenti {#rendering-forms-based-on-fragments}

Il servizio Forms è in grado di eseguire il rendering dei moduli in base ai frammenti creati con  AEM Forms Designer. Un frammento è una parte riutilizzabile di un modulo. Viene salvato come file XDP separato che può essere inserito in più strutture del modulo. Ad esempio, un frammento può contenere un blocco indirizzo o note legali.

L&#39;utilizzo dei frammenti semplifica e velocizza la creazione e la manutenzione di un elevato numero di moduli. Durante la creazione di un modulo, inserire un riferimento al frammento richiesto per consentirne la visualizzazione nel modulo. Il riferimento al frammento contiene un sottomodulo che punta al file XDP fisico.

Di seguito sono riportati i vantaggi offerti dall’uso dei frammenti:

* **Riuso** del contenuto: È possibile riutilizzare il contenuto in più strutture del modulo. Per riutilizzare rapidamente parti dello stesso contenuto in più moduli, creare un frammento. Copiare o ricreare il contenuto richiede più tempo. I frammenti garantiscono inoltre che le parti di un modello di modulo usate di frequente siano uniformi, per aspetto e contenuto, in tutti i moduli che vi fanno riferimento.
* **Aggiornamenti** globali: È possibile apportare modifiche globali a più moduli una sola volta in un file. È possibile modificare contenuto, oggetti script, binding dei dati, layout o stili di un frammento. Tutti i moduli XDP che fanno riferimento al frammento riflettono le modifiche.
* **Creazione** di moduli condivisi: È possibile condividere la creazione di moduli tra diverse risorse. Gli sviluppatori di moduli che dispongono di competenze specifiche in materia di script o in altre funzioni avanzate di  AEM Forms Designer possono sviluppare e condividere frammenti che utilizzano proprietà dinamiche e script. I progettisti di moduli possono utilizzare i frammenti per progettare i moduli. Inoltre, possono utilizzare i frammenti per garantire che tutte le parti del modulo abbiano aspetto e funzionalità uniformi in più moduli.

