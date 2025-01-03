---
title: Configurazione del connettore per Microsoft SharePoint
description: Configura il connettore per Microsoft SharePoint per abilitare la comunicazione tra i moduli AEM e Microsoft SharePoint.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: a8be58f1-1961-4bf5-aaad-feb4489fb389
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
source-git-commit: 98cbaaf64c0268be1afe7196a7bbbf5c93f02148
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 1%

---


# Configurazione del connettore per Microsoft SharePoint

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Il connettore per Microsoft SharePoint consente la comunicazione tra i moduli AEM e Microsoft SharePoint. Per ulteriori informazioni di base, vedere &quot;Connettori per ECM&quot; in [Riferimento servizi](https://www.adobe.com/go/learn_aemforms_services_63).

1. Nella console di amministrazione, fai clic su Servizi > Connettore per Microsoft SharePoint.
2. Specificare le impostazioni seguenti per il server SharePoint:

   **Nome host SharePoint Server:** Il numero di porta del nome host dell&#39;applicazione Web nel server SharePoint, nel formato `[hostname]:'port'`.

   **Nome utente:** l&#39;account utente utilizzato per connettersi al server SharePoint.

   **Password:** Password per l&#39;account utente utilizzato per connettersi al server SharePoint

   **Nome dominio:** Dominio in cui si trova il server SharePoint.

3. Fai clic su Salva.

## Servizio di configurazione di Microsoft SharePoint {#microsoft-sharepoint-configuration-service}

Il servizio di configurazione di Microsoft SharePoint `(MSSharePointConfigService)` consente di specificare le credenziali per l&#39;utente dei moduli AEM che dispone di autorizzazioni di rappresentazione. Per informazioni sulle autorizzazioni di rappresentazione, vedere [Configurazione del connettore per Microsoft SharePoint](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html). Per specificare le impostazioni per `MSSharePointConfigService`, eseguire la procedura seguente:

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione servizi.
1. Spostarsi nell&#39;elenco dei servizi e fare clic su `MSSharePointConfigService`.
1. Nella pagina Configurazione, specifica le impostazioni seguenti:

   * Nome Utente Per Un Utente Con Autorizzazioni Di Rappresentazione
   * Password Per L&#39;Utente Precedente

1. Fai clic su Salva.
