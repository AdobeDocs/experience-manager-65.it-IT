---
title: Configurazione del connettore per Microsoft SharePoint
description: Configura il connettore per Microsoft SharePoint per abilitare la comunicazione tra AEM Forms e Microsoft SharePoint.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: a8be58f1-1961-4bf5-aaad-feb4489fb389
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
source-git-commit: 98cbaaf64c0268be1afe7196a7bbbf5c93f02148
workflow-type: ht
source-wordcount: '214'
ht-degree: 100%

---


# Configurazione del connettore per Microsoft SharePoint

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

Il connettore per Microsoft SharePoint abilita la comunicazione tra AEM Forms e Microsoft SharePoint. Per ulteriori informazioni di base, consulta “Connettori per ECM” in [Riferimento servizi](https://www.adobe.com/go/learn_aemforms_services_63).

1. Nella console di amministrazione, fai clic su Servizi > Connettore per Microsoft SharePoint.
2. Specifica le impostazioni seguenti per il server SharePoint:

   **Nome host SharePoint Server:** il numero di porta del nome host dell’applicazione Web nel server SharePoint, nel formato `[hostname]:'port'`.

   **Nome utente:** l’account utente utilizzato per connettersi al server SharePoint.

   **Password:** password per l’account utente utilizzato la connessione al server SharePoint

   **Nome dominio:** dominio in cui si trova il server SharePoint.

3. Fai clic su Salva.

## Servizio di configurazione di Microsoft SharePoint {#microsoft-sharepoint-configuration-service}

Il servizio di configurazione di Microsoft SharePoint `(MSSharePointConfigService)` consente di specificare le credenziali per l’utente di AEM Forms che dispone delle autorizzazioni di rappresentazione. Per informazioni sulle autorizzazioni di rappresentazione, consulta [Configurazione del connettore per Microsoft SharePoint](https://help.adobe.com/en_US/AEMForms/6.1/SharePointConfig/index.html). Per specificare le impostazioni per `MSSharePointConfigService`, seguire la procedura seguente:

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione servizi.
1. Passa all’elenco dei servizi e fai clic su `MSSharePointConfigService`.
1. Nella pagina Configurazione, specifica le impostazioni seguenti:

   * Nome utente per un utente con autorizzazioni di rappresentazione
   * Password per l’utente sopra indicato

1. Fai clic su Salva.
