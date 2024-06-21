---
title: Risoluzione dei problemi Articolo per risolvere il problema quando il servizio PaperCapture non esegue operazioni OCR (riconoscimento ottico dei caratteri) sui PDF.
description: Scopri i passaggi per risolvere il problema in cui il servizio PaperCapture non esegue operazioni OCR (riconoscimento ottico dei caratteri) sui PDF.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 18005ba060954151df126789496c81f7238e32f6
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 1%

---


# Il servizio PaperCature non esegue il riconoscimento sui PDF

## Problema  

Dopo l&#39;aggiornamento ad AEM Forms Service Pack 6.5.21.0, il `PaperCapture` Il servizio non riesce a eseguire operazioni OCR (Optical Character Recognition) sui PDF. Il servizio non genera output sotto forma di PDF o file di registro.

## Soluzione

1. Scarica il file [hotfix](https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Ca285aedf27094c9e8d9b08dc91e26aa7%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545648843177070%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=uWk0PsSSDjLRxqEMGMW%2BbD%2Fv4egR4vWL%2B0mfKpXdrKQ%3D&amp;reserved=0) dal portale di distribuzione software.
1. Estrarre e copiare il contenuto della cartella scaricata.
1. Passare ai percorsi seguenti per i server applicazioni corrispondenti:
   * **jboss**:
     `..\Adobe\Adobe_Experience_Manager_Forms\jboss\standalone\svcnative\PaperCaptureSvc`
   * **weblogic**:
     `..\Adobe\Adobe_Experience_Manager_Forms\crx-repository\bedrock\svcnative\PaperCaptureSvc`
   * **websphere**:\
     `..\Adobe\Adobe_Experience_Manager_Forms\crx-repository\bedrock\svcnative\PaperCaptureSvc`
   * **Configurazione OSGi**:\
     `..\quickstart\crx-quickstart\bedrock\svcnative\PaperCaptureSvc`
1. Sostituisci il contenuto esistente del `PaperCaptureSvc` cartella con il contenuto copiato.
1. [Riavvia l’istanza AEM](/help/forms/using/restart-aem-sdk.md).


