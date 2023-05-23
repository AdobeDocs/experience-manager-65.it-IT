---
title: Configurazione archiviazione
seo-title: Storage Configuration
description: Come accedere alla console di configurazione dell'archiviazione
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

# Configurazione archiviazione {#storage-configuration}

La configurazione dello storage è il mezzo per identificare lo storage scelto per il contenuto della community, noto anche come UGC (User Generated Content).

Questa impostazione informa il codice AEM Communities sull’implementazione del provider di risorse di archiviazione (SRP) da utilizzare per l’accesso a UGC e deve riflettere la topologia stabilita al momento della distribuzione dell’AEM.

Per informazioni sulle opzioni di storage e sulle topologie di distribuzione, visitare il sito Web all&#39;indirizzo:

* [Archivio contenuti community](working-with-srp.md)
* [Topologie consigliate](topologies.md)

## Console di configurazione archiviazione {#storage-configuration-console}

![jsrp-configuration](assets/jsrp-configuration.png)

Nell&#39;ambiente di authoring, per raggiungere la console di configurazione dello storage.

* Dalla navigazione globale, seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Community]** > **[!UICONTROL Configurazione archiviazione]**

Per selezionare un&#39;opzione di archiviazione diversa da JCR predefinita:

* Seleziona un’opzione
* Configurare in modo appropriato

   * Vedi i dettagli per [selezione di MSRP](msrp.md#select-msrp)
   * Vedi i dettagli per [selezione DSRP](dsrp.md#select-dsrp)
   * Vedi i dettagli per [selezione di ASRP](asrp.md#select-asrp)

* Seleziona **[!UICONTROL Invia]**.

### Informazioni sull’archiviazione JCR {#about-jcr-storage}

Tieni presente che se non viene effettuata alcuna selezione, l’impostazione predefinita è l’archivio AEM, JCR.

JCR è *non* un archivio comune condiviso dagli ambienti di authoring e pubblicazione. Il contenuto della community sarà visibile solo dall’ambiente di authoring o pubblicazione in cui è stato creato.

Visita [Archivio JCR](jsrp.md) per ulteriori informazioni.

>[!NOTE]
>
>Assenza del nodo `srpc` in `/etc/socialconfig` indica il valore predefinito [Store JCR](jsrp.md).
