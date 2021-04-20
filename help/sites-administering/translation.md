---
title: Traduzione di contenuti per siti multilingue
seo-title: Traduzione di contenuti per siti multilingue
description: Scopri come tradurre i contenuti per siti multilingue.
seo-description: Scopri come tradurre i contenuti per siti multilingue.
uuid: 69b3e3a9-6773-4759-8178-aaa612e4c170
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 1e0a68c5-1583-4103-9dbb-7a53faa03c06
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/third-party-services/machine-translation
feature: Language Copy
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 1%

---


# Traduzione di contenuti per siti multilingue {#translating-content-for-multilingual-sites}

Automatizza la traduzione di contenuti, risorse e contenuti generati dagli utenti per creare e gestire siti web multilingue. Per automatizzare i flussi di lavoro di traduzione, è possibile integrare fornitori di servizi di traduzione con AEM e creare progetti per la traduzione dei contenuti in più lingue. AEM supporta flussi di lavoro di traduzione umana e automatica.

* Traduzione umana: Il contenuto viene inviato al tuo provider di traduzioni e tradotto da traduttori professionisti. Una volta completato, il contenuto tradotto viene restituito e importato in AEM. Quando il provider di traduzione è integrato con AEM, il contenuto viene inviato automaticamente tra AEM e il provider di traduzione.
* Traduzione automatica: Il servizio di traduzione automatica traduce immediatamente il contenuto.

La conversione del contenuto prevede i seguenti passaggi:

1. [Collega AEM al tuo ](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider) provider di servizi di traduzione e  [crea configurazioni](/help/sites-administering/tc-tic.md) del framework di integrazione della traduzione.
1. [Associa le pagine del tuo ](/help/sites-administering/tc-tic.md#configuring-pages-for-translation) masterizzatore di linguaggio alle configurazioni del servizio di traduzione e del framework.
1. [Identifica il tipo di ](/help/sites-administering/tc-rules.md) contenuto da tradurre.
1. [Prepara il contenuto per la ](/help/sites-administering/tc-prep.md) traduzione creando il master lingua e le pagine principali delle copie della lingua.
1. [Crea progetti di traduzione per ](/help/sites-administering/tc-manage.md) raccogliere i contenuti da tradurre e preparare il processo di traduzione.
1. Utilizza i progetti di traduzione per [gestire il processo di traduzione dei contenuti](/help/sites-administering/tc-manage.md).

Se il provider di servizi di traduzione non fornisce un connettore per l’integrazione con AEM, AEM supporta l’estrazione e il reinserimento manuali del contenuto di traduzione in formato XML.

>[!NOTE]
>
>Per utilizzare le funzioni Copia lingua, l’utente deve essere membro del gruppo amministratori di progetto.

## Best practice   {#best-practices}

La pagina [Best practice per la traduzione](/help/sites-administering/tc-bp.md) contiene informazioni importanti sull’implementazione.
