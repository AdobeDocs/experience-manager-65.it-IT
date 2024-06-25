---
title: Risoluzione dei problemi Articolo per risolvere il problema quando il servizio PaperCapture non esegue operazioni OCR (riconoscimento ottico dei caratteri) sui PDF.
description: Scopri i passaggi per risolvere il problema in cui il servizio PaperCapture non esegue operazioni OCR (riconoscimento ottico dei caratteri) sui PDF.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 64e120ee-5f16-4cd3-9ae9-95b165169e47
source-git-commit: f9e98d7de24d516eab163d42f6c1c3155915856e
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 2%

---


# Il servizio PaperCature non riesce a eseguire l&#39;operazione OCR sui PDF

## Problema  

Dopo l&#39;aggiornamento ad AEM Forms Service Pack 6.5.21.0, il `PaperCapture` Il servizio non riesce a eseguire operazioni OCR (Optical Character Recognition) sui PDF. Il servizio non genera output sotto forma di PDF o file di registro.

## Applicabile a

Questa soluzione si applica a:
* AEM Forms su tutti i server JEE (JBoss, Weblogic, Websphere)
* AEM Forms sui server OSGi

## Soluzione

1. Scarica il file [hotfix](https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0) dal portale di distribuzione software.
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
1. Arrestare il server applicazioni AEM.
1. Sostituisci il contenuto esistente del `PaperCaptureSvc` cartella con il contenuto copiato.
1. Riavviare il server applicazioni AEM.

   >[!NOTE]
   >
   > Per riavviare l&#39;SDK, si consiglia di utilizzare il comando &#39;Ctrl + C&#39;. Il riavvio dell’SDK dell’AEM con metodi alternativi, ad esempio l’arresto dei processi Java, può causare incongruenze nell’ambiente di sviluppo dell’AEM.
