---
title: Best practice per tradurre le risorse
description: Best practice per una gestione efficiente delle risorse al fine di sincronizzare varie versioni tradotte e semplificare i flussi di lavoro di traduzione.
contentOwner: AG
role: Admin
feature: Asset Management
exl-id: e632dcdb-b2b9-45bc-89e7-337b44b6fc61
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 1%

---

# Best practice per tradurre le risorse {#best-practices-for-translating-assets-efficiently}

[!DNL Adobe Experience Manager Assets] supporta flussi di lavoro multilingue per la traduzione di file binari, metadati e tag per risorse digitali in più lingue e per la gestione delle risorse tradotte. Per informazioni dettagliate, vedere [Assets multilingue](multilingual-assets.md).

Per una gestione efficiente delle risorse e per garantire che diverse versioni tradotte rimangano sincronizzate, crea [copie in lingua](preparing-assets-for-translation.md) delle risorse prima di eseguire i flussi di lavoro di traduzione.

Una copia in lingua di una risorsa o di un gruppo di risorse è un elemento di pari livello (o una versione delle risorse in un linguaggio simile) con una gerarchia di contenuti simile.

Ogni copia per lingua è una risorsa indipendente. Pertanto, la traduzione delle risorse in più lingue può aumentare drasticamente le dimensioni dell’archivio CRX. Ad esempio, la traduzione di risorse con una dimensione combinata di 10 GB in due lingue può aumentare le dimensioni dell’archivio di circa 20 GB (10 GB per ogni lingua).

I file binari delle risorse occupano uno spazio di archiviazione molto più ampio rispetto ai metadati e ai tag. Pertanto, se la traduzione di metadati e tag serve solo al tuo scopo, ometti di tradurre i binari. Puoi conservare la copia originale dei binari nell’archivio per l’associazione con metadati e tag tradotti in diverse lingue. Mantenere una singola copia di file binari, invece di più versioni tradotte, riduce al minimo l’impatto sulla dimensione dell’archivio.

File Data Store e Amazon S3 Data Store forniscono un&#39;infrastruttura di storage più adatta a questi scenari. Questi archivi di archiviazione memorizzano una singola copia dei file binari delle risorse (incluse le rappresentazioni) che possono essere condivisi da metadati e tag in più lingue. Pertanto, la creazione di copie in lingua delle risorse e la traduzione di metadati e tag non influiscono sulle dimensioni dell’archivio.

Puoi anche apportare alcune modifiche alla configurazione di un paio di flussi di lavoro e al framework di integrazione della traduzione per semplificare ulteriormente il processo.

1. Effettua una delle operazioni seguenti:

   * [Configura archivio dati file](/help/sites-deploying/data-store-config.md)
   * [Configurare Amazon S3 Data Store](/help/sites-deploying/data-store-config.md)

<!--
1. Disable the [DAM MetaData Write-back](/help/sites-administering/workflow-offloader.md#disable-offloading) workflow.

   As the name suggests, the [!UICONTROL DAM Metadata Writeback] workflow rewrites the metadata to the binary file. Because the metadata changes after translation, writing it back to the binary file generates a different binary for a language copy.

   >[!NOTE]
   >
   >Disabling the [!UICONTROL DAM MetaData Writeback] workflow turns off XMP metadata write-back on asset binaries. Consequently, future metadata changes are no longer be saved within the assets. Evaluate the consequences before disabling this workflow.
-->

1. Abilita il flusso di lavoro [!UICONTROL Imposta data ultima modifica].

   Il flusso di lavoro [!UICONTROL Writeback di metadati DAM] configura la data dell&#39;ultima modifica per una risorsa. Poiché hai disattivato questo flusso di lavoro nel passaggio 2, [!DNL Assets] non è più in grado di mantenere aggiornata la data dell&#39;ultima modifica delle risorse. Abilita pertanto il flusso di lavoro *Imposta data ultima modifica* per garantire che le date dell&#39;ultima modifica delle risorse siano aggiornate. Assets con le date dell’ultima modifica non aggiornate può causare errori.

1. [Configura il framework di integrazione della traduzione](/help/sites-administering/tc-tic.md) per interrompere la traduzione dei file binari delle risorse. Deseleziona l&#39;opzione **[!UICONTROL Traduci Assets]** nella scheda [!UICONTROL Assets] per interrompere la traduzione dei file binari delle risorse.
1. Traduci metadati/tag risorse utilizzando [Flussi di lavoro risorse multilingue](multilingual-assets.md).
