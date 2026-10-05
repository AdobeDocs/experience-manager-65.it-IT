---
title: Abilita conversioni di file multithread
description: Scopri come abilitare le conversioni di file a più thread.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: 402c1fd4-c6c8-494e-b452-b56a91c4a397
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 4a55f87d3b8aa9944f0b32760aa645c42efd93e8
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 2%
---
# Abilita conversioni di file multithread {#enabling-multi-threaded-file-conversions}

PDF Generator può eseguire più conversioni di file contemporaneamente per migliorare la velocità effettiva di conversione. Scegli la modalità di conversione applicabile:

| Modalità di conversione | Applicazioni che supportano le conversioni simultanee | Modello account utente |
|---|---|---|
| Modalità multiutente | OpenOffice | Un account utente separato esegue ogni istanza di OpenOffice. |
| Modalità utente singolo | Microsoft® Word e Microsoft® Excel | Un account utente esegue più istanze di Word ed Excel. Le conversioni di PowerPoint rimangono serializzate. |

Prima di abilitare entrambe le modalità, completare la [configurazione di preinstallazione di PDF Generator](/help/forms/using/install-configure-document-services.md#preinstallationconfigurations) per le applicazioni e il sistema operativo utilizzati. Per le versioni di applicazioni supportate, vedere [Supporto software per PDF Generator](/help/forms/using/aem-forms-jee-supported-platforms.md#software-support-for-pdf-generator).

## Modalità multiutente {#multi-user-mode}

In modalità multiutente, PDF Generator avvia ogni istanza di OpenOffice con un account utente separato. Configurare un numero sufficiente di account utente amministrativi validi per il numero di conversioni simultanee necessarie. In un cluster, configura gli stessi account su ogni nodo.

In Windows, assicurati che gli utenti di PDF Generator dispongano del privilegio [Sostituisci un token a livello di processo](/help/forms/using/install-configure-document-services.md#grant-the-replace-a-process-level-token-privilege) e completa la configurazione del controllo dell&#39;account utente applicabile descritta in [Configura servizi documentali](/help/forms/using/install-configure-document-services.md#disable-user-account-control-uac).

### Conversioni OpenOffice {#openoffice-conversions}

Configurare un account utente di PDF Generator per ogni istanza di OpenOffice che può essere eseguita contemporaneamente. Installare OpenOffice in un percorso accessibile a tutti gli utenti configurati e chiudere le finestre di dialogo iniziali di attivazione di OpenOffice per ogni utente.

Per i sistemi basati su UNIX, completare l&#39;installazione di OpenOffice e i requisiti delle autorizzazioni utente in [Configure Document Services](/help/forms/using/install-configure-document-services.md#preinstallationconfigurations).

## Modalità utente singolo in Windows {#single-user-mode-on-windows}

La modalità utente singolo consente a PDF Generator di eseguire conversioni simultanee con un unico account utente configurato.

In questa modalità, più istanze di Microsoft® Word (DOC e DOCX) ed Excel (XLS e XLSX) vengono eseguite con lo stesso utente. Microsoft® PowerPoint (PPT e PPTX) non supporta la modalità utente singolo. PDF Generator avvia una sola istanza di PowerPoint alla volta, pertanto le conversioni di PowerPoint vengono serializzate.

Per attivare la modalità utente singolo per le conversioni di Word ed Excel:

1. Nella console di amministrazione, passare a **Home > Servizi > Applicazioni e servizi > Gestione servizi**.
1. Filtra per **PDF Generator** e seleziona **GeneratePDFService**.
1. Nella scheda **Configurazione** configurare le opzioni seguenti:

   * Impostare **Abilita modalità utente singolo per PDFMaker** su **true**.
   * Impostare **Dimensione pool PDFMaker** sul numero massimo di istanze di Word che possono eseguire conversioni simultaneamente.
   * Imposta **Abilita modalità utente singolo per Native2PDF** su **true**.
   * Imposta **Dimensione pool nativo2PDF** sul numero massimo di istanze di Excel che possono eseguire conversioni simultaneamente.

1. Riavvia il server AEM Forms.
