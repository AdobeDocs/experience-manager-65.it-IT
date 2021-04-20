---
title: Configurazione di una soluzione di gestione della corrispondenza
seo-title: Configurazione di una soluzione di gestione della corrispondenza
description: Configurazione di una soluzione di gestione della corrispondenza
uuid: 76b25004-fe47-44d7-9bed-7c0fd963306b
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 186ca75c-638b-4057-826e-cd5d56aa0397
feature: Correspondence Management
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 2%

---


# Configurazione di una soluzione di gestione della corrispondenza {#configuring-a-correspondence-management-solution}

## Definizione dell&#39;URL dell&#39;istanza dell&#39;autore per VersionRestoreManagerImpl {#defining-author-instance-url-for-versionrestoremanagerimpl}

Utilizza i seguenti passaggi per definire l’URL di un’istanza di authoring per il ripristino della versione dell’istanza di authoring:

1. Vai a *https://:&lt;PublishHost>:&lt;PublishPort>/lc/system/console/configMgr*. Accedi con le credenziali utente della console di gestione OSGi. Le credenziali predefinite sono amministratore/amministratore.
1. Trova e fai clic sull&#39;icona **[!UICONTROL Modifica]** accanto all&#39;impostazione **[!UICONTROL com.adobe.livecycle.content.activate.impl.VersionRestoreManagerImpl.name]** .
1. Nel campo **[!UICONTROL URL autore VersionRestoreManager]** , specifica l&#39;URL dell&#39;istanza Autore di VersionRestoreManager.

   **Stringa** URL:

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >Se sono presenti più istanze dell&#39;autore (in cluster) davanti a un load balancer, specifica l&#39;URL del load balancer nel campo **[!UICONTROL VersionRestoreManager Author URL]** .

1. Fai clic su **[!UICONTROL Salva]**.

## Definizione dell’URL dell’istanza di pubblicazione per ActivationManagerImpl (public instance activation manager) {#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

Segui questi passaggi per definire l’URL dell’istanza di pubblicazione per l’attivazione di un’istanza pubblica:

1. Vai a *https://:&lt;authorHost>:&lt;authorPort>/lc/system/console/configMgr*. Accedi con le credenziali utente della console di gestione OSGi. Le credenziali predefinite sono amministratore/amministratore.
1. Trova e fai clic sull&#39;icona **[!UICONTROL Modifica]** accanto all&#39;impostazione **[!UICONTROL com.adobe.livecycle.content.activate.impl.ActivationManagerImpl.name]** .
1. Nel campo **[!UICONTROL URL pubblicazione di ActivationManager]** , specifica l’URL per accedere all’istanza Publish ActivationManager. Puoi fornire i seguenti URL.

   * **URL di bilanciamento del carico (consigliato)**: Fornisci l&#39;URL del load balancer, se disponi di un server web che agisce come load balancer davanti alla farm di pubblicazione (più istanze di pubblicazione non in cluster).
   * **URL** dell’istanza di pubblicazione: Fornisci qualsiasi URL di istanza di pubblicazione, Se disponi di un’unica istanza di pubblicazione o il server web che precede la farm di pubblicazione non è accessibile dall’ambiente di authoring a causa di eventuali restrizioni. Nel caso in cui l’istanza di pubblicazione specificata sia inattiva, è presente un meccanismo di fallback da gestire dal lato dell’autore.
   * **Stringa** URL:

      `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. Fai clic su **[!UICONTROL Salva]**.

Per ulteriori informazioni sulla configurazione di Gestione Corrispondenza, consulta [Proprietà di configurazione Gestione Corrispondenza](https://helpx.adobe.com/aem-forms/6-2/cm-configuration-properties.html).
