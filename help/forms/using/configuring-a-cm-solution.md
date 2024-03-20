---
title: Configurazione di una soluzione di gestione della corrispondenza
description: Scopri come configurare una soluzione di gestione della corrispondenza in un ambiente AEM Forms.
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
feature: Correspondence Management
exl-id: f7f5eb0d-a283-45ea-84d3-d6375d2bb95b
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 1%

---

# Configurazione di una soluzione di gestione della corrispondenza {#configuring-a-correspondence-management-solution}

## Definizione dell’URL dell’istanza di authoring per VersionRestoreManagerImpl {#defining-author-instance-url-for-versionrestoremanagerimpl}

Per definire l’URL di un’istanza di authoring per il ripristino della versione dell’istanza di authoring, effettua le seguenti operazioni:

1. Vai a *https://:&lt;publishhost>:&lt;publishport>/lc/system/console/configMgr*. Accedi con le credenziali utente di OSGi Management Console. Le credenziali predefinite sono amministratore/amministratore.
1. Trova e fai clic su **[!UICONTROL Modifica]** accanto al simbolo **[!UICONTROL com.adobe.livecycle.content.activate.impl.VersionRestoreManagerImpl.name]** impostazione.
1. In **[!UICONTROL URL autore VersionRestoreManager]** , specificare l&#39;URL dell&#39;istanza Author di VersionRestoreManager.

   **Stringa URL**:

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >Se sono presenti più istanze di authoring (cluster) gestite da un load balancer, specifica l’URL del load balancer in **[!UICONTROL URL autore VersionRestoreManager]** campo.

1. Fai clic su **[!UICONTROL Salva]**.

## Definizione dell’URL dell’istanza Publish per ActivationManagerImpl (public instance activation manager) {#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

Segui questi passaggi per definire l’URL dell’istanza Publish per la gestione dell’attivazione di un’istanza pubblica:

1. Vai a *https://:&lt;authorhost>:&lt;authorport>/lc/system/console/configMgr*. Accedi con le credenziali utente di OSGi Management Console. Le credenziali predefinite sono amministratore/amministratore.
1. Trova e fai clic su **[!UICONTROL Modifica]** accanto al simbolo **[!UICONTROL com.adobe.livecycle.content.activate.impl.ActivationManagerImpl.name]** impostazione.
1. In **[!UICONTROL URL di pubblicazione di ActivationManager]** , specificare l&#39;URL per accedere all&#39;istanza Publish ActivationManager. Puoi fornire i seguenti URL.

   * **URL del load balancer (consigliato)**: specifica l’URL del load balancer, se davanti alla farm di pubblicazione (più istanze di pubblicazione non cluster) hai un server web che funge da load balancer.
   * **URL istanza di pubblicazione**: specifica un URL per l’istanza di pubblicazione . Se disponi di una singola istanza di pubblicazione o il server web che precede la farm di pubblicazione non è accessibile dall’ambiente di authoring a causa di eventuali restrizioni. Se l’istanza Publish specificata non è disponibile, è disponibile un meccanismo di fallback da gestire dal lato dell’autore.
   * **Stringa URL**:

     `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. Fai clic su **[!UICONTROL Salva]**.

Per ulteriori informazioni sulla configurazione di Gestione della corrispondenza, consulta [Proprietà di configurazione di Gestione corrispondenza](https://helpx.adobe.com/aem-forms/6-2/cm-configuration-properties.html).
