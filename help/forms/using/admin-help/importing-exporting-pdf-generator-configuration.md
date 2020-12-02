---
title: Importazione ed esportazione di file di configurazione PDF Generator
seo-title: Importazione ed esportazione di file di configurazione PDF Generator
description: Informazioni su come importare ed esportare i file di configurazione PDF Generator.
seo-description: Informazioni su come importare ed esportare i file di configurazione PDF Generator.
uuid: 3367253b-d222-4c5f-9455-a1810d96112e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e25c1b35-73eb-4353-8e39-a2d4cdccd101
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---


# Importazione ed esportazione di file di configurazione PDF Generator {#importing-and-exporting-pdf-generator-configuration-files}

Il file di configurazione contiene le informazioni di conversione di PDF Generator, tra cui il PDF, il tipo di file e le impostazioni di protezione.

>[!NOTE]
>
>Non è possibile modificare l&#39;impostazione del timeout per PDF Generator importando un file nativo2pdfconfig.xml personalizzato. L&#39;impostazione del timeout in tale file è solo a scopo informativo e visualizza l&#39;impostazione corrente in PDF Generator. Per modificare l&#39;impostazione del timeout, vedere &quot;Impostazione dei parametri di prestazioni di PDF Generator&quot; in [Installazione e distribuzione di moduli AEM](https://www.adobe.com/go/learn_aemforms_installJBoss_63).

## Esporta il file di configurazione corrente {#export-your-current-configuration-file}

1. Nella console di amministrazione, fare clic su Servizi > PDF Generator > File di configurazione > Esporta configurazione.
1. Per esportare le impostazioni, selezionate l’opzione appropriata:

   * Per esportare tutte le impostazioni denominate, selezionate Scarica intera configurazione.
   * Per esportare solo un&#39;impostazione Adobe PDF , un&#39;impostazione di protezione o un tipo di file, selezionate Scarica configurazione minima.

      Se state esportando una configurazione minima, selezionate le  impostazioni Adobe PDF, protezione e tipo di file da esportare.

1. Fate clic su Scarica e salvate il file XML nella posizione appropriata.

## Importa un file di configurazione {#import-a-configuration-file}

>[!NOTE]
>
>Il sistema verrà riconfigurato in base alle informazioni presenti nel file importato.

1. Nella console di amministrazione, fare clic su Servizi > PDF Generator > File di configurazione > Importa configurazione.
1. Selezionare Importa un file di configurazione esistente.
1. Per specificare il percorso del file nella casella File di configurazione, fare clic su Sfoglia per individuare e selezionare il file, quindi fare clic su **Importa**.

## Convertire tutti i livelli all&#39;interno di file AutoCAD {#convert-all-layers-within-autocad-files}

Per impostazione predefinita, PDF Generator converte in PDF solo il livello predefinito dei file AutoCAD anziché tutti i livelli contenuti nel file. Per convertire tutti i livelli, seguite questa procedura.

1. Nella console di amministrazione, fare clic su Servizi > PDF Generator > File di configurazione > Esporta configurazione.
1. Selezionate Scarica intera configurazione e fate clic su Scarica.
1. In un editor di testo, aprite il file scaricato e, sotto il tag `AutoCAD` all&#39;interno del tag `PDFMaker`, aggiungete il testo `convertAllPages="true"`.
1. Nella console di amministrazione, fare clic su Servizi > PDF Generator > File di configurazione > Importa configurazione.
1. Selezionate Importa un file di configurazione esistente, specificate il file aggiornato e fate clic su Importa.

   Tutti i file AutoCAD convertiti utilizzando il file di configurazione modificato verranno convertiti.

## Ripristinare le impostazioni originali installate con PDF Generator {#reset-your-configuration-to-the-original-settings-installed-with-pdf-generator}

1. Nella console di amministrazione, fare clic su Servizi > PDF Generator > File di configurazione > Importa configurazione.
1. Selezionate Reimposta configurazione su impostazioni predefinite e fate clic su Importa.

