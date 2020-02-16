---
title: JSRP - Provider risorse di storage JCR
seo-title: JSRP - Provider risorse di storage JCR
description: JSRP è generalmente ideale per gli ambienti di dimostrazione o sviluppo di un’istanza di pubblicazione e di un’istanza di authoring
seo-description: JSRP è generalmente ideale per gli ambienti di dimostrazione o sviluppo di un’istanza di pubblicazione e di un’istanza di authoring
uuid: 358a43c1-4137-4300-8443-c0d7166968ad
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: f5316a73-84e2-4a18-98c1-a384eeaa77cf
translation-type: tm+mt
source-git-commit: aa2c75e061e00ba74d54843a5f35bb7d82d12a92

---


# JSRP - Provider risorse di storage JCR {#jsrp-jcr-storage-resource-provider}

## Informazioni su JSRP {#about-jsrp}

Quando AEM Communities utilizza JSRP come opzione di archiviazione (impostazione predefinita), il contenuto della community viene memorizzato in JCR e il contenuto generato dall&#39;utente (UGC) è accessibile solo dall&#39;istanza di creazione o pubblicazione a cui è stato pubblicato.

Grazie alla semplicità di implementazione, JSRP è generalmente ideale per gli ambienti di dimostrazione o sviluppo di un’istanza di pubblicazione e di un’istanza di autore.

Vedere anche [Caratteristiche delle opzioni](working-with-srp.md#characteristics-of-srp-options) SRP e topologie [](topologies.md)consigliate.

## Configurazione {#configuration}

### Select JSRP {#select-jsrp}

Per impostazione predefinita, JSRP è l’opzione di memorizzazione per UGC.

La console [Configurazione](srp-config.md) storage consente di selezionare la configurazione di storage predefinita, che identifica quale implementazione di SRP utilizzare.

Nell’ambiente di authoring, per accedere alla console Configurazione archiviazione

* Dalla navigazione globale: **[!UICONTROL Strumenti > Community > Configurazione dello storage]**

![chlimage_1-234](assets/chlimage_1-234.png)

* Select **[!UICONTROL JCR Storage Resource Provider (JSRP)]**
* Seleziona **[!UICONTROL Invia]**

### Pubblicazione della configurazione {#publishing-the-configuration}

JSRP è la configurazione predefinita, ma per assicurarsi che la configurazione identica sia impostata nell’ambiente di pubblicazione:

* Per autore:

   * Dalla navigazione globale: **[!UICONTROL Strumenti > Implementazione > Replica]**
   * Seleziona **[!UICONTROL Attiva albero]**
   * **[!UICONTROL Percorso iniziale]**:

      * Passa a `/conf/global/settings/community/srpc/`
   * Seleziona **[!UICONTROL attiva]**


## Gestione dei dati utente {#managing-user-data}

Per informazioni sugli *utenti*, i profili ** utente e i gruppi *di* utenti, spesso inseriti nell’ambiente di pubblicazione, visita

* [Sincronizzazione utente](sync.md)
* [Gestione di utenti e gruppi di utenti](users.md)

## Risoluzione dei problemi {#troubleshooting}

### UGC non visibile in JCR {#ugc-not-visible-in-jcr}

Verificate che JSRP sia stato configurato come fornitore predefinito, verificando la configurazione dell&#39;opzione di memorizzazione. Per impostazione predefinita, il provider delle risorse di storage è JSRP.

Per creare e pubblicare tutte le istanze di AEM, rivisitate la console Configurazione archiviazione o verificate l’archivio AEM:

* in JCR, se [/conf/global/settings/community](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community)

   * Non contiene un nodo [srpc](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc) , significa che il provider di archiviazione è JSRP
   * Se il nodo srpc esiste e contiene il nodo [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/conf/global/settings/community/srpc/defaultconfiguration), le proprietà della configurazione predefinita devono definire JSRP come provider predefinito

### UGC non visibile nell&#39;istanza Author {#ugc-not-visible-on-author-instance}

Questo non è un bug. Una caratteristica di JSRP è che il contenuto della community inserito nell’ambiente di pubblicazione sarà visibile solo nell’ambiente di pubblicazione.

### UGC non visibile nell&#39;istanza di pubblicazione {#ugc-not-visible-on-publish-instance}

Se viene distribuita una singola istanza di pubblicazione o un cluster di pubblicazione, seguite le istruzioni per [UGC non visibile in JCR](#ugc-not-visible-in-jcr).

Se viene distribuita una farm di pubblicazione, una caratteristica di JSRP è che il contenuto della community sarà visibile solo nell’istanza di pubblicazione in cui è stato pubblicato.

Affinché UGC sia visibile da qualsiasi istanza di pubblicazione, è necessario un cluster di pubblicazione.
