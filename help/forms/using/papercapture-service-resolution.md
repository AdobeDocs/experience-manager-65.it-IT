---
title: Articolo sulla risoluzione dei problemi per risolvere il problema quando il servizio PaperCapture non esegue operazioni OCR (riconoscimento ottico dei caratteri) sui PDF.
description: Scopri i passaggi per risolvere il problema in cui il servizio PaperCapture non riesce a eseguire operazioni OCR (Optical Character Recognition) sui PDF.
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 64e120ee-5f16-4cd3-9ae9-95b165169e47
source-git-commit: e030a71a0f52e22a803597122369cb111774f49b
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 2%

---


# Il servizio PaperCature non riesce a eseguire l&#39;operazione OCR sui PDF

## Problema  

Dopo l&#39;aggiornamento ad AEM Forms Service Pack 6.5.21.0 o AEM Forms Service Pack 6.5.22.0, il servizio `PaperCapture` non è in grado di eseguire operazioni OCR (riconoscimento ottico dei caratteri) sui PDF. Il servizio non genera output sotto forma di PDF o file di registro.

## Applicabile a

Questa soluzione si applica a:

* AEM Forms su tutti i server JEE (JBoss, Weblogic, Websphere)
* AEM Forms sui server OSGi

## Soluzione

1. Scarica [hotfix](https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&reserved=0) dal portale di distribuzione software.
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
1. Arresta il server applicazioni AEM.
1. Sostituire il contenuto esistente della cartella `PaperCaptureSvc` con il contenuto copiato.
1. Riavvia il server applicazioni AEM.

   >[!NOTE]
   >
   > Si consiglia di utilizzare il comando &#39;Ctrl + C&#39; per riavviare SDK. Il riavvio di AEM SDK utilizzando metodi alternativi, ad esempio l’arresto dei processi Java, può causare incoerenze nell’ambiente di sviluppo AEM.
