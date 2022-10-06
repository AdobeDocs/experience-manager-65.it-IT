---
title: Configurazione dell’archiviazione
seo-title: Storage Configuration
description: Accesso alla console di configurazione dell'archiviazione
seo-description: How to access the Storage Configuration Console
uuid: 6a5a71d5-6aaa-4635-8852-4dae33c497a9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 71fac7e9-814a-48b5-b816-9bdcb2a05190
role: Admin
exl-id: 67de7e26-3f93-4034-9e3a-5c127f7447bc
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 4%

---

# Configurazione dell’archiviazione {#storage-configuration}

La configurazione dello storage è il mezzo per identificare lo storage scelto per il contenuto della community, noto anche come contenuto generato dall’utente (UGC).

Questa impostazione informa il codice AEM Communities in merito all&#39;implementazione del provider di risorse di archiviazione (SRP) da utilizzare per l&#39;accesso a UGC e deve riflettere la topologia stabilita al momento della distribuzione di AEM.

Per una discussione sulle opzioni di storage e sulle topologie di distribuzione, visita:

* [Archivio dei contenuti della community](working-with-srp.md)
* [Topologie consigliate](topologies.md)

## Console di configurazione dell&#39;archiviazione {#storage-configuration-console}

![jsrp-configuration](assets/jsrp-configuration.png)

Nell’ambiente di authoring, raggiungere la console di configurazione dello storage.

* Dalla navigazione globale, seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Community]** > **[!UICONTROL Configurazione dell&#39;archiviazione]**

Per selezionare un&#39;opzione di archiviazione diversa dal JCR predefinito:

* Seleziona un’opzione
* Configurare in modo appropriato

   * Vedi i dettagli per [selezione di MSRP](msrp.md#select-msrp)
   * Vedi i dettagli per [selezione di DSRP](dsrp.md#select-dsrp)
   * Vedi i dettagli per [selezione di ASRP](asrp.md#select-asrp)

* Seleziona **[!UICONTROL Invia]**.

### Informazioni sullo storage JCR {#about-jcr-storage}

Se non viene effettuata alcuna selezione, l’impostazione predefinita è l’archivio AEM, JCR.

JCR è *not* un archivio comune condiviso dagli ambienti di authoring e pubblicazione. Il contenuto della community sarà visibile solo dall’ambiente di authoring o pubblicazione in cui è stato creato.

Visita [Store JCR](jsrp.md) per ulteriori informazioni.

>[!NOTE]
>
>L&#39;assenza del nodo `srpc` sotto `/etc/socialconfig` indica il valore predefinito [Store JCR](jsrp.md).
