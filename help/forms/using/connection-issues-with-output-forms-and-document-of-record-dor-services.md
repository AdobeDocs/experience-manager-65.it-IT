---
title: Problemi di connessione con i servizi DoR di output, Forms e (documento di record)
description: Risolvere gli errori di connessione di AEM Forms dopo SP19. Arrestare, installare Microsoft Visual C++, riavviare il server per una soluzione ottimale. Risolvere i problemi relativi ai servizi Output, Forms e DoR.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
role: Admin
source-git-commit: cf5da092fabbc7834108dc54d65eb97e160984ce
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 1%

---


# Impossibile utilizzare il servizio di output, il servizio Forms o il servizio Document of Record (DoR) {#unable-to-use-output-service-forms-service-or-document-of-record-service}

## Problema  

Dopo aver installato AEM Forms 6.5 Service Pack 19, il tentativo di utilizzare il servizio di output, il servizio Forms o il servizio Document of Record (DoR) potrebbe causare un `Connection to failed service` errore.

## Soluzione

Per risolvere il problema:

1. Arresta l’istanza Forms di AEM 6.5.
1. Scarica e installa [Versione a 64 bit di Microsoft Visual C++ Redistributable per Visual Studio 2015, 2017, 2019 e 2022](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022) sul computer in cui è installato AEM 6.5 Forms.
1. Riavvia il server AEM Forms.


>[!NOTE]
>
>
> Assicurati di installare Redistributable anche se è installata una versione precedente.