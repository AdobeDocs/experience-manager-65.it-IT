---
title: JSRP - Provider risorsa di archiviazione JCR
description: JSRP è ideale per ambienti di dimostrazione o sviluppo di un’istanza Publish e di un’istanza Author
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 873e013c-a2da-4b37-b0e3-56bdf240004a
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# JSRP - Provider risorsa di archiviazione JCR {#jsrp-jcr-storage-resource-provider}

## JSRP {#about-jsrp}

Quando AEM Communities utilizza JSRP come opzione di archiviazione (impostazione predefinita), il contenuto della community viene memorizzato in JCR e il contenuto generato dall’utente (UGC) è accessibile solo dall’istanza di authoring o pubblicazione in cui è stato pubblicato.

Data la semplicità di implementazione, JSRP è ideale per ambienti di dimostrazione o sviluppo di un’istanza Publish e di un’istanza Author.

Vedi anche [Caratteristiche delle opzioni SRP](working-with-srp.md#characteristics-of-srp-options) e [topologie consigliate](topologies.md).

## Configurazione {#configuration}

### Seleziona JSRP {#select-jsrp}

Per impostazione predefinita, JSRP è l&#39;opzione di archiviazione per UGC.

La [console Configurazione archiviazione](srp-config.md) consente di selezionare la configurazione di archiviazione predefinita, che identifica l&#39;implementazione di SRP da utilizzare.

Nell’ambiente di authoring, per raggiungere la console Configurazione di archiviazione

* Dalla navigazione globale: **[!UICONTROL Strumenti]** > **[!UICONTROL Community]** > **[!UICONTROL Configurazione archiviazione]**

* Seleziona **[!UICONTROL Provider risorsa di archiviazione JCR (JSRP)]**

* Seleziona **[!UICONTROL Invia]**

![jsrp-configuration](assets/jsrp-configuration.png)

### Pubblicazione della configurazione {#publishing-the-configuration}

Mentre JSRP è la configurazione predefinita, per garantire che la configurazione identica sia impostata nell’ambiente di pubblicazione:

* Dalla navigazione globale: **[!UICONTROL Strumenti]** > **[!UICONTROL Distribuzione]** > **[!UICONTROL Replica]**
* Seleziona **[!UICONTROL Attiva albero]** > **[!UICONTROL Percorso iniziale]**:

   * Passa a `/conf/global/settings/community/srpc/`

* Seleziona **[!UICONTROL Attiva]**

## Gestione dei dati utente {#managing-user-data}

Per informazioni relative a *utenti*, *profili utente* e *gruppi di utenti*, spesso immessi nell&#39;ambiente di pubblicazione, visitare:

* [Sincronizzazione utente](sync.md)
* [Gestione di utenti e gruppi di utenti](users.md)

## Risoluzione dei problemi {#troubleshooting}

### UGC non visibile in JCR {#ugc-not-visible-in-jcr}

Verificare che JSRP sia stato configurato come provider predefinito controllando la configurazione dell&#39;opzione di archiviazione. Per impostazione predefinita, il provider di risorse di archiviazione è JSRP.

Su tutte le istanze di AEM di Author e Publish, visita nuovamente la console Configurazione di archiviazione o controlla l’archivio AEM:

* In JCR, se [/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * Non contiene un nodo [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc). Il provider di archiviazione è JSRP.
   * Se il nodo srpc esiste e contiene il nodo [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration), le proprietà della configurazione predefinita devono definire JSRP come provider predefinito.

### UGC non visibile nell’istanza di authoring {#ugc-not-visible-on-author-instance}

Questo non è un bug. Una caratteristica di JSRP è che il contenuto della community inserito nell’ambiente di pubblicazione è visibile solo nell’ambiente Publish.

### UGC non visibile nell’istanza di Publish {#ugc-not-visible-on-publish-instance}

Se è distribuita una singola istanza di Publish o un cluster di pubblicazione, segui le istruzioni per [UGC Not Visible in JCR](#ugc-not-visible-in-jcr).

Se viene distribuita una farm di pubblicazione, una caratteristica di JSRP è che il contenuto della community è visibile solo sull’istanza Publish in cui è stato pubblicato.

Affinché UGC sia visibile da qualsiasi istanza di Publish, è necessario un cluster di pubblicazione.
