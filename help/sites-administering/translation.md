---
title: Traduzione di contenuti per siti multilingue
description: Scopri come tradurre i contenuti per siti multilingue.
contentOwner: Guillaume Carlino
feature: Language Copy
exl-id: 6ccfe612-8cfd-4ca2-ad01-8e4af36d44fa
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 74%

---

# Traduzione di contenuti per siti multilingue {#translating-content-for-multilingual-sites}

Automatizza la traduzione di contenuti di pagina, risorse e contenuti generati dall&#39;utente per creare e gestire siti web multilingue. Per automatizzare i flussi di lavoro di traduzione, puoi integrare fornitori di servizi di traduzione con AEM e creare progetti per la traduzione dei contenuti in più lingue. AEM supporta flussi di lavoro di traduzione umana e automatica.

* Traduzione umana: il contenuto viene inviato al tuo provider di traduzioni e tradotto da traduttori professionisti. Una volta completato, il contenuto tradotto viene rinviato e importato in AEM. Quando il provider di traduzione è integrato con AEM, il contenuto viene inviato automaticamente tra AEM e il provider di traduzione.
* Traduzione automatica: il servizio di traduzione automatica traduce immediatamente il contenuto.

La traduzione del contenuto prevede i seguenti passaggi:

1. [Connetti AEM con il provider di servizi di traduzione](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider) e [crea configurazioni del Translation Integration Framework](/help/sites-administering/tc-tic.md).
1. [Associa le pagine della lingua master](/help/sites-administering/tc-tic.md#configuring-pages-for-translation) con il servizio di traduzione e le configurazioni del framework.
1. [Identifica il tipo di contenuto](/help/sites-administering/tc-rules.md) da tradurre.
1. [Prepara il contenuto per la traduzione](/help/sites-administering/tc-prep.md) creando la lingua master e le pagine root delle copie in lingua.
1. [Crea progetti di traduzione](/help/sites-administering/tc-manage.md) per raccogliere il contenuto da tradurre e preparare il processo di traduzione.
1. Utilizza i progetti di traduzione per [gestire il processo di traduzione dei contenuti](/help/sites-administering/tc-manage.md).

Se il provider di servizi di traduzione non fornisce un connettore per l’integrazione con AEM, AEM supporta l’estrazione e il reinserimento manuali del contenuto di traduzione in formato XML.

>[!NOTE]
>
>Per utilizzare le funzioni Copia in lingua, l’utente deve essere membro del gruppo amministratori dei progetti.

## Best practice   {#best-practices}

La pagina [Best practice per la traduzione](/help/sites-administering/tc-bp.md) contiene informazioni importanti sull’implementazione.
