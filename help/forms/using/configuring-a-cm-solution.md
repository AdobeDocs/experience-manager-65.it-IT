---
title: Configurazione di una soluzione di gestione della corrispondenza
seo-title: Configurazione di una soluzione di gestione della corrispondenza
description: Configurazione di una soluzione di gestione della corrispondenza
uuid: 76b25004-fe47-44d7-9bed-7c0fd963306b
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 186ca75c-638b-4057-826e-cd5d56aa0397
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 1%

---


# Configurazione di una soluzione di gestione della corrispondenza {#configuring-a-correspondence-management-solution}

## Definizione dell’URL dell’istanza di creazione per VersionRestoreManagerImpl {#defining-author-instance-url-for-versionrestoremanagerimpl}

Per definire l’URL di un’istanza di creazione per il ripristino della versione dell’istanza di creazione, effettuate le seguenti operazioni:

1. Andate a *https://:&lt;HostPubblicazione>:&lt;PortaPubblicazione>/lc/system/console/configMgr*. Accedi con le credenziali utente della console di gestione OSGi. Le credenziali predefinite sono admin/admin.
1. Trova e fai clic sull’icona **[!UICONTROL Modifica]** accanto all’impostazione **[!UICONTROL com.adobe.livecycle.content.activate.impl.VersionRestoreManagerImpl.name]** .
1. Nel campo URL **[!UICONTROL autore]** VersionRestoreManager, specificate l&#39;URL dell&#39;istanza Author di VersionRestoreManager.

   **Stringa** URL:

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >Se esistono più istanze di creazione (cluster) fronte a un sistema di bilanciamento del carico, specificate l&#39;URL del sistema di bilanciamento del carico nel campo URL **[!UICONTROL autore]** VersionRestoreManager.

1. Fai clic su **[!UICONTROL Salva]**.

## Definizione dell’URL dell’istanza Pubblica per ActivationManagerImpl (Gestione attivazione istanza pubblica) {#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

Effettuate le seguenti operazioni per definire l’URL dell’istanza Pubblica per Gestione attivazione dell’istanza pubblica:

1. Andate a *https://:&lt;authorHost>:&lt;authorPort>/lc/system/console/configMgr*. Accedi con le credenziali utente della console di gestione OSGi. Le credenziali predefinite sono admin/admin.
1. Trova e fai clic sull’icona **[!UICONTROL Modifica]** accanto all’impostazione **[!UICONTROL com.adobe.livecycle.content.activate.impl.ActivationManagerImpl.name]** .
1. Nel campo URL **[!UICONTROL pubblicazione di]** ActivationManager, specificate l’URL per l’accesso all’istanza Publish ActivationManager. Potete fornire i seguenti URL.

   * **URL bilanciamento del carico (consigliato)**: Fornite l’URL di bilanciamento del carico se un server Web agisce come sistema di bilanciamento del carico davanti alla farm di pubblicazione (più istanze di pubblicazione non in cluster).
   * **URL** istanza di pubblicazione: Specificate un URL per l’istanza di pubblicazione. Se disponete di un’unica istanza di pubblicazione o se il server Web che accede alla farm di pubblicazione non è accessibile dall’ambiente di authoring a causa di eventuali restrizioni. Se l’istanza di pubblicazione specificata non è attiva, è disponibile un meccanismo di fallback con cui gestire l’authoring dal lato dell’autore.
   * **Stringa** URL:

      `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. Fai clic su **[!UICONTROL Salva]**.

Per ulteriori informazioni sulla configurazione della gestione della corrispondenza, consultate Proprietà [di configurazione della gestione della](https://helpx.adobe.com/aem-forms/6-2/cm-configuration-properties.html)corrispondenza.
