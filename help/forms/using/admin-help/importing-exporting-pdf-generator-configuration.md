---
title: Importazione ed esportazione dei file di configurazione di PDF Generator
seo-title: Importing and exporting PDF Generator configuration files
description: Scopri come importare ed esportare i file di configurazione di PDF Generator.
seo-description: Learn how to import and export PDF Generator configuration files.
uuid: 3367253b-d222-4c5f-9455-a1810d96112e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e25c1b35-73eb-4353-8e39-a2d4cdccd101
feature: PDF Generator
exl-id: b363b23a-29bb-4ea4-a8f2-5ba9fe3c7b27
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# Importazione ed esportazione dei file di configurazione di PDF Generator {#importing-and-exporting-pdf-generator-configuration-files}

Il file di configurazione contiene le informazioni sulla conversione di PDF Generator, inclusi PDF, tipo di file e impostazioni di protezione.

>[!NOTE]
>
>Non è possibile modificare l&#39;impostazione di timeout per PDF Generator importando un file nativo2pdfconfig.xml personalizzato. L&#39;impostazione di timeout in tale file ha solo scopo informativo e visualizza l&#39;impostazione corrente in PDF Generator. Per modificare l&#39;impostazione del timeout, vedere &quot;Impostazione dei parametri delle prestazioni del generatore di PDF&quot; in [Installazione e distribuzione di moduli AEM](https://www.adobe.com/go/learn_aemforms_installJBoss_63).

## Esporta il file di configurazione corrente {#export-your-current-configuration-file}

1. Nella console di amministrazione, fai clic su Servizi > Generatore di PDF > File di configurazione > Esporta configurazione.
1. Per esportare le impostazioni, selezionare l&#39;opzione appropriata:

   * Per esportare tutte le impostazioni denominate, selezionare Scarica configurazione completa.
   * Per esportare solo un&#39;impostazione di Adobe PDF, un&#39;impostazione di protezione o un&#39;impostazione del tipo di file, selezionare Scarica configurazione minima.

      Se stai esportando una configurazione minima, seleziona le impostazioni Adobe PDF, sicurezza e tipo di file da esportare.

1. Fare clic su Scarica e salvare il file XML nella posizione appropriata.

## Importare un file di configurazione {#import-a-configuration-file}

>[!NOTE]
>
>Il sistema verrà riconfigurato in base alle informazioni contenute nel file importato.

1. Nella console di amministrazione, fai clic su Servizi > Generatore di PDF > File di configurazione > Importa configurazione.
1. Seleziona Importa Un File Di Configurazione Esistente.
1. Per specificare il percorso del file nella casella File di configurazione, fare clic su Sfoglia per trovare e selezionare il file, quindi fare clic su **Importa**.

## Convertire tutti i livelli all&#39;interno di file AutoCAD {#convert-all-layers-within-autocad-files}

Per default, il Generatore di PDF converte solo il livello di default dei file AutoCAD in PDF anziché tutti i livelli all&#39;interno del file. Per convertire tutti i livelli, seguite questa procedura.

1. Nella console di amministrazione, fai clic su Servizi > Generatore di PDF > File di configurazione > Esporta configurazione.
1. Seleziona Scarica configurazione completa e fai clic su Scarica.
1. In un editor di testo, apri il file scaricato e, nella sezione `AutoCAD` tag all&#39;interno di `PDFMaker` , aggiungi il testo `convertAllPages="true"`.
1. Nella console di amministrazione, fai clic su Servizi > Generatore di PDF > File di configurazione > Importa configurazione.
1. Selezionate Importa file di configurazione esistente (Import An Existing Configuration File), specificate il file aggiornato e fate clic su Importa (Import).

   Tutti i file AutoCAD convertiti utilizzando il file di configurazione modificato avranno tutti i livelli convertiti.

## Ripristina le impostazioni originali installate con PDF Generator {#reset-your-configuration-to-the-original-settings-installed-with-pdf-generator}

1. Nella console di amministrazione, fai clic su Servizi > Generatore di PDF > File di configurazione > Importa configurazione.
1. Seleziona Ripristina configurazione predefinita e fai clic su Importa.
