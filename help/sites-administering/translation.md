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

---


# Traduzione di contenuti per siti multilingue {#translating-content-for-multilingual-sites}

Automatizzate la traduzione di contenuti di pagina, risorse e contenuti generati dagli utenti per creare e gestire siti Web multilingue. Per automatizzare i flussi di lavoro di traduzione, integrate i fornitori di servizi di traduzione con AEM e create progetti per la traduzione di contenuti in più lingue. AEM supporta flussi di lavoro di traduzione umana e automatica.

* Traduzione umana: Il contenuto viene inviato al provider di traduzioni e tradotto da traduttori professionisti. Al termine, il contenuto convertito viene restituito e importato in AEM. Quando il fornitore di traduzione è integrato con AEM, il contenuto viene inviato automaticamente tra AEM e il fornitore di traduzione.
* Traduzione automatica: Il servizio di traduzione automatica traduce immediatamente il contenuto.

La conversione dei contenuti comporta i seguenti passaggi:

1. [Connetti AEM con il tuo provider](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider) di servizi di traduzione e [crea configurazioni](/help/sites-administering/tc-tic.md)del framework di integrazione della traduzione.
1. [Associate le pagine del vostro master](/help/sites-administering/tc-tic.md#configuring-pages-for-translation) lingua alle configurazioni del servizio e del framework di traduzione.
1. [Identificare il tipo di contenuto](/help/sites-administering/tc-rules.md) da tradurre.
1. [Preparate il contenuto per la traduzione](/help/sites-administering/tc-prep.md) creando il master della lingua e le pagine principali delle copie della lingua.
1. [Create progetti](/help/sites-administering/tc-manage.md) di traduzione per raccogliere il contenuto da tradurre e preparare il processo di traduzione.
1. Utilizzate i progetti di traduzione per [gestire il processo](/help/sites-administering/tc-manage.md)di traduzione del contenuto.

Se il provider di servizi di traduzione non fornisce un connettore per l’integrazione con AEM, AEM supporta l’estrazione e il reinserimento manuali del contenuto di traduzione in formato XML.

>[!NOTE]
>
>Per utilizzare le funzioni Copia lingua, l’utente deve essere membro del gruppo di amministratori del progetto.

## Best practice {#best-practices}

La pagina [Tecniche consigliate](/help/sites-administering/tc-bp.md) per la traduzione contiene informazioni importanti sulla vostra implementazione.
