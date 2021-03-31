---
title: Best practice per tradurre le risorse
description: Procedure consigliate per una gestione efficiente delle risorse, al fine di sincronizzare diverse versioni tradotte e semplificare i flussi di lavoro di traduzione.
contentOwner: AG
role: Administrator
feature: Gestione risorse
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 1%

---


# Best practice per tradurre le risorse {#best-practices-for-translating-assets-efficiently}

[!DNL Adobe Experience Manager Assets] supporta flussi di lavoro multilingue per tradurre file binari, metadati e tag per le risorse digitali in più lingue e gestire le risorse tradotte. Per informazioni dettagliate, consulta [Risorse multilingue](multilingual-assets.md).

Per una gestione efficiente delle risorse, affinché le diverse versioni tradotte rimangano sincronizzate, crea [copie in lingua](preparing-assets-for-translation.md) delle risorse prima di eseguire i flussi di lavoro di traduzione.

Una copia in lingua di una risorsa o di un gruppo di risorse è di pari livello (o una versione delle risorse in un linguaggio cognato) con una gerarchia dei contenuti simile.

Ogni copia in lingua è una risorsa indipendente. Pertanto, tradurre le risorse in più impostazioni internazionali può aumentare drasticamente le dimensioni dell’archivio CRX. Ad esempio, la traduzione di risorse con una dimensione combinata di 10 GB in due lingue può aumentare la dimensione dell’archivio di circa 20 GB (10 GB per ogni lingua).

I file binari delle risorse occupano uno spazio di archiviazione molto più ampio rispetto ai metadati e ai tag. Pertanto, se tradurre metadati e tag serve solo al tuo scopo, ometti di tradurre i binari. È possibile conservare la copia originale dei file binari nell’archivio per associarli ai metadati e ai tag tradotti in lingue diverse. Mantenere una sola copia dei file binari, invece di più versioni tradotte, riduce al minimo l&#39;impatto sulle dimensioni dell&#39;archivio.

File Data Store e Amazon S3 Data Store forniscono un&#39;infrastruttura di storage più adatta a questi scenari. Questi archivi di archiviazione memorizzano una singola copia dei file binari delle risorse (incluse le rappresentazioni) che possono essere condivisi da metadati e tag in più impostazioni internazionali. Pertanto, la creazione di copie della lingua delle risorse e la traduzione di metadati e tag non influisce sulle dimensioni dell’archivio.

Puoi anche apportare alcune modifiche alla configurazione di un paio di flussi di lavoro e del framework di integrazione della traduzione per semplificare ulteriormente il processo.

1. Effettua una delle operazioni seguenti:

   * [Imposta archivio dati file](/help/sites-deploying/data-store-config.md)
   * [Configurazione archivio dati Amazon S3](/help/sites-deploying/data-store-config.md)

<!--
1. Disable the [DAM MetaData Write-back](/help/sites-administering/workflow-offloader.md#disable-offloading) workflow.

   As the name suggests, the [!UICONTROL DAM Metadata Writeback] workflow rewrites the metadata to the binary file. Because the metadata changes after translation, writing it back to the binary file generates a different binary for a language copy.

   >[!NOTE]
   >
   >Disabling the [!UICONTROL DAM MetaData Writeback] workflow turns off XMP metadata write-back on asset binaries. Consequently, future metadata changes are no longer be saved within the assets. Evaluate the consequences before disabling this workflow.
-->

1. Attiva il flusso di lavoro [!UICONTROL Imposta data ultima modifica] .

   Il flusso di lavoro [!UICONTROL DAM MetaData Writeback] configura l’ultima data di modifica per una risorsa. Poiché disattivi questo flusso di lavoro nel passaggio 2, [!DNL Assets] non è più in grado di mantenere aggiornata l’ultima data di modifica delle risorse. Abilita quindi il flusso di lavoro *Imposta data ultima modifica* per garantire che le ultime date di modifica delle risorse siano aggiornate. Le risorse con date dell’ultima modifica non aggiornate possono causare errori.

1. [Configura il ](/help/sites-administering/tc-tic.md) framework di integrazione della traduzione per interrompere la traduzione dei binari delle risorse. Deseleziona l’opzione **[!UICONTROL Traduci risorse]** nella scheda [!UICONTROL Risorse] per interrompere la traduzione dei file binari delle risorse.
1. Traduci metadati/tag delle risorse utilizzando [Flussi di lavoro per risorse multilingue](multilingual-assets.md).
