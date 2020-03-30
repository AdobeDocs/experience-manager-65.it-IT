---
title: Configurazione del connettore per Microsoft SharePoint
seo-title: Configurazione del connettore per Microsoft SharePoint
description: Configurare il connettore per Microsoft SharePoint per abilitare la comunicazione tra i moduli AEM e Microsoft SharePoint.
seo-description: Configurare il connettore per Microsoft SharePoint per abilitare la comunicazione tra i moduli AEM e Microsoft SharePoint.
uuid: f1561b41-da20-4220-b13a-e78472a9449f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0ec881c9-8dcc-4847-9edf-24d9e6c4a7ea
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Configurazione del connettore per Microsoft SharePoint {#configuring-connector-for-microsoft-sharepoint}

Il connettore per Microsoft SharePoint consente la comunicazione tra i moduli AEM e Microsoft SharePoint. Per ulteriori informazioni di base, vedere &quot;Connettori per l&#39;ECM&quot; nella Guida di riferimento dei [servizi](https://www.adobe.com/go/learn_aemforms_services_63).

1. Nella console di amministrazione, fare clic su Servizi > Connettore per Microsoft SharePoint.
1. Specificate le seguenti impostazioni per SharePoint Server:

   **Nome host di SharePoint Server:** Il numero della porta del nome host dell&#39;applicazione Web nel server SharePoint, nel formato `[hostname]:'port'`.

   **Nome utente:** L&#39;account utente utilizzato per connettersi al server SharePoint.

   **Password:** Password per l&#39;account utente utilizzato per connettersi al server SharePoint

   **Nome dominio:** Dominio in cui si trova il server SharePoint.

1. Fate clic su Salva.

## Servizio di configurazione di Microsoft SharePoint {#microsoft-sharepoint-configuration-service}

Il servizio di configurazione di Microsoft SharePoint `(MSSharePointConfigService)` consente di specificare le credenziali per l&#39;utente di moduli AEM che dispone di autorizzazioni di rappresentazione. Per informazioni sulle autorizzazioni di rappresentazione, vedere [Configurazione del connettore per Microsoft SharePoint](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html). Per specificare le impostazioni per `MSSharePointConfigService`:

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione dei servizi.
1. Spostatevi nell’elenco dei servizi e fate clic su `MSSharePointConfigService`.
1. Specificate le seguenti impostazioni nella pagina Configurazione:

   * Nome Utente Per Un Utente Con Autorizzazioni Di Rappresentazione
   * Password Per L&#39;Utente Sopra

1. Fate clic su Salva.

