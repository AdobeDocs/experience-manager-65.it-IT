---
title: Configurazione di una soluzione di gestione della corrispondenza
seo-title: Configuring a Correspondence Management solution
description: Configurazione di una soluzione di gestione della corrispondenza
uuid: 76b25004-fe47-44d7-9bed-7c0fd963306b
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 186ca75c-638b-4057-826e-cd5d56aa0397
feature: Correspondence Management
exl-id: f7f5eb0d-a283-45ea-84d3-d6375d2bb95b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 1%

---

# Configurazione di una soluzione di gestione della corrispondenza {#configuring-a-correspondence-management-solution}

## Definizione dell’URL dell’istanza dell’autore per VersionRestoreManagerImpl {#defining-author-instance-url-for-versionrestoremanagerimpl}

Utilizza i seguenti passaggi per definire l’URL di un’istanza di authoring per il ripristino della versione dell’istanza di authoring:

1. Vai a *https://&lt;publishhost>:&lt;publishport>/lc/system/console/configMgr*. Accedi con le credenziali utente della console di gestione OSGi. Le credenziali predefinite sono amministratore/amministratore.
1. Trova e fai clic sul pulsante **[!UICONTROL Modifica]** accanto all’icona **[!UICONTROL com.adobe.livecycle.content.activate.impl.VersionRestoreManagerImpl.name]** impostazione.
1. In **[!UICONTROL URL autore VersionRestoreManager]** Specifica l&#39;URL dell&#39;istanza Author di VersionRestoreManager.

   **stringa URL**:

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >Se esistono più istanze dell&#39;autore (in cluster) davanti a un load balancer, specifica l&#39;URL del load balancer in **[!UICONTROL URL autore VersionRestoreManager]** campo .

1. Fai clic su **[!UICONTROL Salva]**.

## Definizione dell’URL dell’istanza di pubblicazione per ActivationManagerImpl (public instance activation manager) {#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

Segui questi passaggi per definire l’URL dell’istanza di pubblicazione per l’attivazione di un’istanza pubblica:

1. Vai a *https://&lt;authorhost>:&lt;authorport>/lc/system/console/configMgr*. Accedi con le credenziali utente della console di gestione OSGi. Le credenziali predefinite sono amministratore/amministratore.
1. Trova e fai clic sul pulsante **[!UICONTROL Modifica]** accanto all’icona **[!UICONTROL com.adobe.livecycle.content.activate.impl.ActivationManagerImpl.name]** impostazione.
1. In **[!UICONTROL URL pubblicazione di ActivationManager]** specifica l’URL per l’accesso all’istanza Publish ActivationManager. Puoi fornire i seguenti URL.

   * **URL di bilanciamento del carico (consigliato)**: Fornisci l&#39;URL del load balancer, se disponi di un server web che agisce come load balancer davanti alla farm di pubblicazione (più istanze di pubblicazione non in cluster).
   * **URL dell’istanza di pubblicazione**: Fornisci qualsiasi URL di istanza di pubblicazione, Se disponi di un’unica istanza di pubblicazione o il server web che precede la farm di pubblicazione non è accessibile dall’ambiente di authoring a causa di eventuali restrizioni. Nel caso in cui l’istanza di pubblicazione specificata sia inattiva, è presente un meccanismo di fallback da gestire dal lato dell’autore.
   * **stringa URL**:

      `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. Fai clic su **[!UICONTROL Salva]**.

Per ulteriori informazioni sulla configurazione della gestione della corrispondenza, consulta [Proprietà di configurazione della gestione della corrispondenza](https://helpx.adobe.com/aem-forms/6-2/cm-configuration-properties.html).
