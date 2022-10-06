---
title: Configurazione del connettore per Microsoft SharePoint
seo-title: Configuring Connector for Microsoft SharePoint
description: Configura il connettore per Microsoft SharePoint per abilitare la comunicazione tra AEM moduli e Microsoft SharePoint.
seo-description: Configure Connector for Microsoft SharePoint to enable communication between AEM forms and Microsoft SharePoint.
uuid: f1561b41-da20-4220-b13a-e78472a9449f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0ec881c9-8dcc-4847-9edf-24d9e6c4a7ea
exl-id: a8be58f1-1961-4bf5-aaad-feb4489fb389
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 1%

---

# Configurazione del connettore per Microsoft SharePoint {#configuring-connector-for-microsoft-sharepoint}

Il connettore per Microsoft SharePoint consente la comunicazione tra AEM moduli e Microsoft SharePoint. Per ulteriori informazioni di base, consulta &quot;Connettori per ECM&quot; in [Riferimento servizi](https://www.adobe.com/go/learn_aemforms_services_63).

1. Nella console di amministrazione, fai clic su Servizi > Connettore per Microsoft SharePoint.
1. Specifica le seguenti impostazioni per il server SharePoint:

   **Nome host server SharePoint:** Il numero di porta del nome host dell&#39;applicazione Web sul server SharePoint, nel formato `[hostname]:'port'`.

   **Nome utente:** Account utente utilizzato per la connessione al server SharePoint.

   **Password:** Password per l&#39;account utente utilizzato per la connessione al server SharePoint

   **Nome di dominio:** Dominio in cui si trova il server SharePoint.

1. Fai clic su Salva.

## Servizio di configurazione Microsoft SharePoint {#microsoft-sharepoint-configuration-service}

Servizio di configurazione Microsoft SharePoint `(MSSharePointConfigService)` consente di specificare le credenziali per l’utente dei moduli AEM che dispone delle autorizzazioni di rappresentazione. Per informazioni sulle autorizzazioni di rappresentazione, vedi [Configurazione del connettore per Microsoft SharePoint](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html). Segui questi passaggi per specificare le impostazioni per `MSSharePointConfigService`:

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione dei servizi.
1. Passa all’elenco dei servizi e fai clic su `MSSharePointConfigService`.
1. Nella pagina Configurazione , specifica le seguenti impostazioni:

   * Nome Utente Per Un Utente Con Autorizzazioni Di Rappresentazione
   * Password Per L&#39;Utente Sopra Indicato

1. Fai clic su Salva.
