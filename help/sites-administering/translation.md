---
title: Traduzione di contenuti per siti multilingue
seo-title: Traduzione di contenuti per siti multilingue
description: Scoprite come tradurre i contenuti per siti multilingue.
seo-description: Scoprite come tradurre i contenuti per siti multilingue.
uuid: 69b3e3a9-6773-4759-8178-aaa612e4c170
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 1e0a68c5-1583-4103-9dbb-7a53faa03c06
docset: aem65
legacypath: /content/docs/en/aem/6-0/administer/integration/third-party-services/machine-translation
translation-type: tm+mt
source-git-commit: 8b53e79e3a88f58423e99477db930a4912a1ba09
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---


# Traduzione di contenuti per siti multilingue {#translating-content-for-multilingual-sites}

Automatizzate la traduzione di contenuti di pagina, risorse e contenuti generati dagli utenti per creare e gestire siti Web multilingue. Per automatizzare i flussi di lavoro di traduzione, potete integrare i fornitori di servizi di traduzione con AEM e creare progetti per la traduzione dei contenuti in più lingue. AEM supporta flussi di lavoro di traduzione umana e automatica.

* Traduzione umana: Il contenuto viene inviato al provider di traduzioni e tradotto da traduttori professionisti. Al termine, il contenuto convertito viene restituito e importato in AEM. Quando il provider di traduzione è integrato con AEM, il contenuto viene inviato automaticamente tra AEM e il provider di traduzione.
* Traduzione automatica: Il servizio di traduzione automatica traduce immediatamente il contenuto.

La conversione dei contenuti comporta i seguenti passaggi:

1. [Collega AEM al ](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider) provider del servizio di traduzione e  [crea configurazioni](/help/sites-administering/tc-tic.md) del framework di integrazione delle traduzioni.
1. [Associate le pagine del vostro ](/help/sites-administering/tc-tic.md#configuring-pages-for-translation) maestro di lingua alle configurazioni del servizio di traduzione e del framework.
1. [Identificare il tipo di ](/help/sites-administering/tc-rules.md) contenuto da tradurre.
1. [Preparate il contenuto per la ](/help/sites-administering/tc-prep.md) traduzione creando il master della lingua e le pagine principali delle copie della lingua.
1. [Create ](/help/sites-administering/tc-manage.md) progetti di traduzione per raccogliere il contenuto da tradurre e preparare il processo di traduzione.
1. Utilizzate i progetti di traduzione per [gestire il processo di traduzione del contenuto](/help/sites-administering/tc-manage.md).

Se il provider di servizi di traduzione non fornisce un connettore per l&#39;integrazione con AEM, AEM supporta l&#39;estrazione manuale e il reinserimento del contenuto di traduzione in formato XML.

>[!NOTE]
>
>Per utilizzare le funzioni Copia lingua, l’utente deve essere membro del gruppo di amministratori del progetto.

## Best practice   {#best-practices}

La pagina [Best practice di traduzione](/help/sites-administering/tc-bp.md) contiene informazioni importanti sull&#39;implementazione.
