---
title: Configurazione di archiviazione
description: Scopri la console Configurazione di archiviazione come mezzo per identificare lo storage scelto per il contenuto della community, noto anche come contenuto generato dall’utente.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 67de7e26-3f93-4034-9e3a-5c127f7447bc
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 4%

---

# Configurazione di archiviazione {#storage-configuration}

La configurazione dello storage è il mezzo per identificare lo storage scelto per il contenuto della community, noto anche come UGC (User-generated Content).

Questa impostazione informa il codice AEM Communities sull’implementazione del provider di risorse di archiviazione (SRP) utilizzata durante l’accesso a UGC. Deve riflettere la topologia stabilita quando è stato distribuito Adobe Experience Manager (AEM).

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

   * Visualizza dettagli per [selezione di MSRP](msrp.md#select-msrp)
   * Vedi dettagli per [selezione DSRP](dsrp.md#select-dsrp)
   * Vedi i dettagli per [selezionare ASRP](asrp.md#select-asrp)

* Seleziona **[!UICONTROL Invia]**.

### Informazioni sull’archiviazione JCR {#about-jcr-storage}

Se non viene effettuata alcuna selezione, l’impostazione predefinita è l’archivio AEM, JCR.

JCR è *non* un archivio comune condiviso dagli ambienti Author e Publish. Il contenuto della community è visibile solo dall’ambiente di authoring o Publish in cui è stato creato.

Visita [Archivio JCR](jsrp.md) per ulteriori informazioni.

>[!NOTE]
>
>L&#39;assenza del nodo `srpc` in `/etc/socialconfig` indica l&#39;archivio predefinito [JCR](jsrp.md).
