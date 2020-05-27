---
title: Procedure ottimali per la conversione delle risorse
description: Procedure ottimali per una gestione efficiente delle risorse, per sincronizzare le diverse versioni tradotte e semplificare i flussi di lavoro di traduzione.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 1%

---


# Procedure ottimali per la conversione delle risorse {#best-practices-for-translating-assets-efficiently}

Risorse Adobe Experience Manager supporta flussi di lavoro multilingue per tradurre file binari, metadati e tag per risorse digitali in più lingue e gestire le risorse tradotte. Per informazioni dettagliate, consultate Risorse [](multilingual-assets.md)multilingue.

Per una gestione efficiente delle risorse, al fine di garantire che le diverse versioni tradotte rimangano sincronizzate, create copie [in](preparing-assets-for-translation.md) lingua delle risorse prima di eseguire i flussi di lavoro di traduzione.

Una copia in lingua di una risorsa o di un gruppo di risorse è un linguaggio di pari livello (o una versione delle risorse in un linguaggio cognato) con una gerarchia di contenuti simile.

Ogni copia della lingua è una risorsa indipendente. Pertanto, la conversione di risorse in più lingue può notevolmente aumentare le dimensioni del repository CRX. Ad esempio, tradurre le risorse con una dimensione combinata di 10 GB in due lingue può aumentare la dimensione del repository di circa 20 GB (10 GB per ciascuna lingua).

I file binari delle risorse occupano uno spazio di archiviazione molto più ampio rispetto ai metadati e ai tag. Pertanto, se tradurre metadati e tag serve solo al vostro scopo, omettete di tradurre i file binari. È possibile conservare la copia originale dei file binari nella directory archivio per associarli ai metadati e ai tag tradotti in lingue diverse. Mantenendo una singola copia dei file binari, anziché più versioni tradotte, si riduce al minimo l&#39;impatto sulle dimensioni del repository.

File Data Store e Amazon S3 Data Store forniscono un&#39;infrastruttura di storage più adatta a questi scenari. Questi repository di archiviazione memorizzano una singola copia dei file binari di risorse (comprese le rappresentazioni) che possono essere condivisi da metadati e tag in più lingue. Pertanto, la creazione di copie della lingua delle risorse e la traduzione di metadati e tag non influisce sulle dimensioni dell’archivio.

Potete inoltre apportare alcune modifiche alla configurazione di un paio di flussi di lavoro e al framework di integrazione della traduzione per semplificare ulteriormente il processo.

1. Effettua una delle operazioni seguenti:

   * [Imposta archivio dati file](/help/sites-deploying/data-store-config.md)
   * [Imposta archivio dati Amazon S3](/help/sites-deploying/data-store-config.md)

1. Disattiva il flusso di lavoro [di riscrittura](/help/sites-administering/workflow-offloader.md#disable-offloading) metadati DAM.

   Come suggerisce il nome, il flusso di lavoro [!UICONTROL DAM Metadata Writeback] riscrive i metadati nel file binario. Poiché i metadati cambiano dopo la traduzione, la riscrittura nel file binario genera un binario diverso per una copia della lingua.

   >[!NOTE]
   >
   >La disattivazione del flusso di lavoro [!UICONTROL DAM MetaData Write] consente di disattivare la riscrittura dei metadati XMP sui file binari delle risorse. Di conseguenza, le modifiche future ai metadati non saranno più salvate nelle risorse. Valutare le conseguenze prima di disattivare questo flusso di lavoro.

1. Attiva il flusso di lavoro [!UICONTROL Imposta data] ultima modifica.

   Il flusso di lavoro [!UICONTROL DAM MetaData Writeback] configura l’ultima data modificata per una risorsa. Poiché questo flusso di lavoro viene disattivato al passaggio 2, Risorse non è più in grado di aggiornare l’ultima data di modifica delle risorse. Pertanto, abilitate il flusso di lavoro *Imposta data* ultima modifica per fare in modo che le ultime date di modifica delle risorse siano aggiornate. Le risorse con date dell’ultima modifica non aggiornate possono causare errori.

1. [Configurate il framework](/help/sites-administering/tc-tic.md) di integrazione della conversione per interrompere la traduzione dei file binari delle risorse. Deselezionate l’opzione **[!UICONTROL Traduci risorse]** nella scheda Risorse per interrompere la conversione dei file binari delle risorse.
1. Traducete i metadati/i tag delle risorse utilizzando flussi di lavoro [di risorse](multilingual-assets.md)multilingue.
