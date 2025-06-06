---
title: Problemi di connessione con i servizi DoR di output, Forms e (documento di record)
description: Risolvere gli errori di connessione di AEM Forms dopo SP19. Arrestare, installare Microsoft Visual C++, riavviare il server per una soluzione ottimale. Risolvere i problemi relativi ai servizi Output, Forms e DoR.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
role: Admin
exl-id: bd58099c-08cd-4056-afb6-a5935454429a
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 1%

---

# Impossibile utilizzare il servizio di output, il servizio Forms o il servizio Document of Record (DoR) {#unable-to-use-output-service-forms-service-or-document-of-record-service}

## Problema  

Dopo aver installato AEM Forms 6.5 Service Pack 19, il tentativo di utilizzare il servizio di output, il servizio Forms o il servizio Document of Record (DoR) potrebbe causare un errore `Connection to failed service`.

## Soluzione

Per risolvere il problema:

1. Arresta l’istanza Forms di AEM 6.5.
1. Scaricare e installare la versione a [64 bit dei pacchetti ridistribuibili di Microsoft Visual C++ per Visual Studio 2015, 2017, 2019 e 2022](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022) nel computer in cui è installato AEM 6.5 Forms.
1. Riavvia il server AEM Forms.

   >[!NOTE]
   >
   > Per riavviare l&#39;SDK, si consiglia di utilizzare il comando &#39;Ctrl + C&#39;. Il riavvio dell’SDK dell’AEM con metodi alternativi, ad esempio l’arresto dei processi Java, può causare incongruenze nell’ambiente di sviluppo dell’AEM.


>[!NOTE]
>
>
> Assicurati di installare Redistributable anche se è installata una versione precedente.
