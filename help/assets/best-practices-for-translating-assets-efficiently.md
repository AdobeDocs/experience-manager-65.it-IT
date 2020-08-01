---
title: Procedure ottimali per la conversione delle risorse
description: Procedure ottimali per una gestione efficiente delle risorse, per sincronizzare le diverse versioni tradotte e semplificare i flussi di lavoro di traduzione.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 1%

---


# Procedure ottimali per la conversione delle risorse {#best-practices-for-translating-assets-efficiently}

[!DNL Adobe Experience Manager Assets] supporta flussi di lavoro multilingue per tradurre file binari, metadati e tag per risorse digitali in più lingue e gestire le risorse tradotte. Per informazioni dettagliate, consultate Risorse [](multilingual-assets.md)multilingue.

Per una gestione efficiente delle risorse, al fine di garantire che le diverse versioni tradotte rimangano sincronizzate, create copie [in](preparing-assets-for-translation.md) lingua delle risorse prima di eseguire i flussi di lavoro di traduzione.

Una copia in lingua di una risorsa o di un gruppo di risorse è un linguaggio di pari livello (o una versione delle risorse in un linguaggio cognato) con una gerarchia di contenuti simile.

Ogni copia della lingua è una risorsa indipendente. Pertanto, la conversione di risorse in più lingue può notevolmente aumentare le dimensioni del repository CRX. Ad esempio, tradurre le risorse con una dimensione combinata di 10 GB in due lingue può aumentare la dimensione del repository di circa 20 GB (10 GB per ciascuna lingua).

I file binari delle risorse occupano uno spazio di archiviazione molto più ampio rispetto ai metadati e ai tag. Pertanto, se tradurre metadati e tag serve solo al vostro scopo, omettete di tradurre i file binari. È possibile conservare la copia originale dei file binari nella directory archivio per associarli ai metadati e ai tag tradotti in lingue diverse. Mantenendo una singola copia dei file binari, anziché più versioni tradotte, si riduce al minimo l&#39;impatto sulle dimensioni del repository.

Archivio dati file e  archivio dati Amazon S3 forniscono un&#39;infrastruttura di storage più adatta a questi scenari. Questi repository di archiviazione memorizzano una singola copia dei file binari di risorse (comprese le rappresentazioni) che possono essere condivisi da metadati e tag in più lingue. Pertanto, la creazione di copie della lingua delle risorse e la traduzione di metadati e tag non influisce sulle dimensioni dell’archivio.

Potete inoltre apportare alcune modifiche alla configurazione di un paio di flussi di lavoro e al framework di integrazione della traduzione per semplificare ulteriormente il processo.

1. Effettua una delle operazioni seguenti:

   * [Imposta archivio dati file](/help/sites-deploying/data-store-config.md)
   * [Configurare  archivio dati Amazon S3](/help/sites-deploying/data-store-config.md)

<!--
1. Disable the [DAM MetaData Write-back](/help/sites-administering/workflow-offloader.md#disable-offloading) workflow.

   As the name suggests, the [!UICONTROL DAM Metadata Writeback] workflow rewrites the metadata to the binary file. Because the metadata changes after translation, writing it back to the binary file generates a different binary for a language copy.

   >[!NOTE]
   >
   >Disabling the [!UICONTROL DAM MetaData Writeback] workflow turns off XMP metadata write-back on asset binaries. Consequently, future metadata changes are no longer be saved within the assets. Evaluate the consequences before disabling this workflow.
-->

1. Attiva il flusso di lavoro [!UICONTROL Imposta data] ultima modifica.

   Il flusso di lavoro [!UICONTROL DAM MetaData Writeback] configura l’ultima data modificata per una risorsa. Poiché nel passaggio 2 avete disattivato questo flusso di lavoro, non [!DNL Assets] è più possibile aggiornare l’ultima data di modifica delle risorse. Pertanto, abilitate il flusso di lavoro *Imposta data* ultima modifica per fare in modo che le ultime date di modifica delle risorse siano aggiornate. Le risorse con date dell’ultima modifica non aggiornate possono causare errori.

1. [Configurate il framework](/help/sites-administering/tc-tic.md) di integrazione della conversione per interrompere la traduzione dei file binari delle risorse. Per arrestare la conversione dei file binari delle risorse, deselezionate l’opzione **[!UICONTROL Traduci risorse]** nella scheda [!UICONTROL Risorse] .
1. Traducete i metadati/i tag delle risorse utilizzando flussi di lavoro [di risorse](multilingual-assets.md)multilingue.
