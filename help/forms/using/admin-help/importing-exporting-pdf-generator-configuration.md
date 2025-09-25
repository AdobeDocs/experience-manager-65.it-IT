---
title: Importazione ed esportazione dei file di configurazione di PDF Generator
description: Scopri come importare ed esportare i file di configurazione di PDF Generator.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: b363b23a-29bb-4ea4-a8f2-5ba9fe3c7b27
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '384'
ht-degree: 100%

---

# Importazione ed esportazione dei file di configurazione di PDF Generator {#importing-and-exporting-pdf-generator-configuration-files}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Il file di configurazione contiene le informazioni sulla conversione di PDF Generator, inclusi PDF, tipo di file e impostazioni di protezione.

>[!NOTE]
>
>Non puoi modificare l’impostazione di timeout per PDF Generator importando un file native2pdfconfig.xml personalizzato. L’impostazione di timeout in tale file è solo a scopo informativo e mostra l’impostazione corrente in PDF Generator. Per modificare l’impostazione di timeout, consulta “Impostazione dei parametri delle prestazioni di PDF Generator” in [Installazione e distribuzione di AEM Forms](https://www.adobe.com/go/learn_aemforms_installJBoss_63).

## Esportare il file di configurazione corrente {#export-your-current-configuration-file}

1. Nella console di amministrazione, fai clic su Servizi > PDF Generator > File di configurazione > Esporta configurazione.
1. Per esportare le impostazioni, seleziona l’opzione appropriata:

   * Per esportare tutte le impostazioni denominate, seleziona Scarica configurazione completa.
   * Per esportare solo un’impostazione di Adobe PDF, di protezione o del tipo di file, seleziona Scarica configurazione minima.

     Se stai esportando una configurazione minima, seleziona le impostazioni Adobe PDF, protezione e tipo di file da esportare.

1. Fai clic su Scarica e salva il file XML nella posizione appropriata.

## Importare un file di configurazione {#import-a-configuration-file}

>[!NOTE]
>
>Il sistema verrà riconfigurato in base alle informazioni nel file importato.

1. Nella console di amministrazione, fai clic su Servizi > PDF Generator > File di configurazione > Importa configurazione.
1. Seleziona Importa un file di configurazione esistente.
1. Per specificare la posizione del file nella casella File di configurazione, fai clic su Sfoglia per trovare e selezionare il file, quindi fai clic su **Importa**.

## Convertire tutti i livelli all’interno dei file AutoCAD {#convert-all-layers-within-autocad-files}

Per impostazione predefinita, PDF Generator converte in PDF solo il livello predefinito dei file AutoCAD, anziché tutti i livelli all’interno del file. Per convertire tutti i livelli, segui questa procedura.

1. Nella console di amministrazione, fai clic su Servizi > PDF Generator > File di configurazione > Esporta configurazione.
1. Seleziona Scarica configurazione completa e fai clic su Scarica.
1. In un editor di testo, apri il file scaricato e aggiungi il testo `convertAllPages="true"` sotto il tag `AutoCAD` all’interno del tag `PDFMaker`.
1. Nella console di amministrazione, fai clic su Servizi > PDF Generator > File di configurazione > Importa configurazione.
1. Seleziona Importa file di configurazione esistente, specifica il file aggiornato e fai clic su Importa.

   Tutti i file AutoCAD convertiti utilizzando il file di configurazione modificato avranno tutti i livelli convertiti.

## Ripristinare le impostazioni originali della configurazione installate con PDF Generator {#reset-your-configuration-to-the-original-settings-installed-with-pdf-generator}

1. Nella console di amministrazione, fai clic su Servizi > PDF Generator > File di configurazione > Importa configurazione.
1. Seleziona Ripristina le impostazioni predefinite della configurazione e fai clic su Importa.
