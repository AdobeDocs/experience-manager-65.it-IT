---
title: Configurazione dell’archiviazione
seo-title: Configurazione dell’archiviazione
description: Come accedere alla console di configurazione dell'archivio
seo-description: Come accedere alla console di configurazione dell'archivio
uuid: 6a5a71d5-6aaa-4635-8852-4dae33c497a9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 71fac7e9-814a-48b5-b816-9bdcb2a05190
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configurazione dell’archiviazione {#storage-configuration}

La configurazione dello storage è il mezzo per identificare lo storage scelto per il contenuto della community, noto anche come contenuto generato dall&#39;utente (UGC).

Questa impostazione informa il codice di AEM Communities in merito all&#39;implementazione del provider di risorse di storage (SRP) da utilizzare per l&#39;accesso a UGC e deve riflettere la topologia stabilita al momento della distribuzione di AEM.

Per una discussione sulle opzioni di storage e sulle topologie di distribuzione, visita

* [Archivio contenuti community](working-with-srp.md)
* [Topologie consigliate](topologies.md)

## Console di configurazione dell&#39;archiviazione {#storage-configuration-console}

![chlimage_1-188](assets/chlimage_1-188.png)

Nell’ambiente di authoring, per accedere alla console di configurazione dell’archivio

* Dalla navigazione globale: **[!UICONTROL Strumenti > Community > Configurazione dello storage]**

Per selezionare un&#39;opzione di archiviazione diversa dal JCR predefinito:

* selezionare un&#39;opzione
* Configurare in modo appropriato

   * Vedere i dettagli per la [selezione di MSRP](msrp.md#select-msrp)
   * Vedere i dettagli per [selezionare DSRP](dsrp.md#select-dsrp)
   * Vedere i dettagli per [selezionare ASRP](asrp.md#select-asrp)

* Seleziona **[!UICONTROL Invia]**

### Lo storage JCR {#about-jcr-storage}

Se non viene effettuata alcuna selezione, il valore predefinito è l’archivio AEM, JCR.

JCR *non* è uno store comune condiviso dagli ambienti di creazione e pubblicazione. Il contenuto della community sarà visibile solo dall’ambiente di creazione e pubblicazione in cui è stato creato.

Per ulteriori informazioni, visita [JCR Store](jsrp.md) .

>[!NOTE]
>
>L&#39;assenza del nodo `srpc`sotto `/etc/socialconfig` indica l&#39;archivio [JCR](jsrp.md)predefinito.

