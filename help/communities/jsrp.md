---
title: JSRP - Provider risorsa di archiviazione JCR
seo-title: JSRP - Provider risorsa di archiviazione JCR
description: JSRP è generalmente più adatto per gli ambienti di dimostrazione o sviluppo di un’istanza di pubblicazione e di un’istanza di authoring
seo-description: JSRP è generalmente più adatto per gli ambienti di dimostrazione o sviluppo di un’istanza di pubblicazione e di un’istanza di authoring
uuid: 358a43c1-4137-4300-8443-c0d7166968ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: f5316a73-84e2-4a18-98c1-a384eeaa77cf
role: Admin
exl-id: 873e013c-a2da-4b37-b0e3-56bdf240004a
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---

# JSRP - Provider risorsa di archiviazione JCR {#jsrp-jcr-storage-resource-provider}

## Informazioni su JSRP {#about-jsrp}

Quando AEM Communities utilizza JSRP come opzione di archiviazione (opzione predefinita), il contenuto della community viene memorizzato in JCR e il contenuto generato dall’utente (UGC) è accessibile solo dall’istanza di authoring o pubblicazione a cui è stato pubblicato.

A causa della semplicità di implementazione, JSRP è generalmente più adatto per gli ambienti di dimostrazione o sviluppo di un’istanza di pubblicazione e di un’istanza di authoring.

Vedere anche [Caratteristiche delle opzioni SRP](working-with-srp.md#characteristics-of-srp-options) e [Topologie consigliate](topologies.md).

## Configurazione {#configuration}

### Seleziona JSRP {#select-jsrp}

Per impostazione predefinita, JSRP è l’opzione di archiviazione per UGC.

La [console di configurazione dello storage](srp-config.md) consente di selezionare la configurazione di archiviazione predefinita, che identifica l&#39;implementazione dell&#39;SRP da utilizzare.

Nell’ambiente di authoring, per raggiungere la console di configurazione dello storage

* Dalla navigazione globale: **[!UICONTROL Strumenti]** > **[!UICONTROL Community]** > **[!UICONTROL Configurazione dell&#39;archiviazione]**

* Selezionare **[!UICONTROL JCR Storage Resource Provider (JSRP)]**

* Seleziona **[!UICONTROL Invia]**

![jsrp-configuration](assets/jsrp-configuration.png)

### Pubblicazione della configurazione {#publishing-the-configuration}

Mentre JSRP è la configurazione predefinita, per assicurarsi che la configurazione identica sia impostata nell&#39;ambiente di pubblicazione:

* Dalla navigazione globale: **[!UICONTROL Strumenti]** > **[!UICONTROL Implementazione]** > **[!UICONTROL Replica]**
* Seleziona **[!UICONTROL Attiva albero]** > **[!UICONTROL Percorso iniziale]**:

   * Vai a `/conf/global/settings/community/srpc/`

* Seleziona **[!UICONTROL Attiva]**

## Gestione dei dati utente {#managing-user-data}

Per informazioni sugli *utenti*, *profili utente* e *gruppi di utenti*, spesso inseriti nell&#39;ambiente di pubblicazione, visita:

* [Sincronizzazione utente](sync.md)
* [Gestione di utenti e gruppi di utenti](users.md)

## Risoluzione dei problemi {#troubleshooting}

### UGC non visibile in JCR {#ugc-not-visible-in-jcr}

Assicurati che JSRP sia stato configurato come provider predefinito controllando la configurazione dell&#39;opzione di archiviazione. Per impostazione predefinita, il provider delle risorse di archiviazione è JSRP.

Su tutte le istanze di authoring e pubblicazione AEM, rivedi la console di configurazione dello storage o controlla l’archivio AEM:

* In JCR, se [/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * Non contiene un nodo [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc), significa che il provider di archiviazione è JSRP.
   * Se il nodo srpc esiste e contiene il nodo [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration), le proprietà della configurazione predefinita devono definire JSRP come provider predefinito.

### UGC non visibile nell’istanza di authoring {#ugc-not-visible-on-author-instance}

Questo non è un bug. Una caratteristica di JSRP è che il contenuto della community inserito nell’ambiente di pubblicazione sarà visibile solo nell’ambiente di pubblicazione.

### UGC non visibile sull&#39;istanza di pubblicazione {#ugc-not-visible-on-publish-instance}

Se una singola istanza di pubblicazione o se è implementato un cluster di pubblicazione, segui le istruzioni per [UGC Non visibile in JCR](#ugc-not-visible-in-jcr).

Se viene implementata una farm di pubblicazione, una caratteristica di JSRP è che il contenuto della community sarà visibile solo sull’istanza di pubblicazione in cui è stato pubblicato.

Affinché UGC sia visibile da qualsiasi istanza di pubblicazione, è necessario un cluster di pubblicazione.
