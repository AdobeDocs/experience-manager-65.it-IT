---
title: Integrazione di Salesforce con AEM Forms tramite il flusso delle credenziali client OAuth 2.0
description: Passaggi per integrare l’integrazione di Salesforce con AEM Forms utilizzando il flusso delle credenziali del client OAuth 2.0
exl-id: 4c356aa6-ebd4-40b9-89e3-bc4519e4a7c5
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 4%

---

# Integrazione di Salesforce tramite il flusso delle credenziali client OAuth 2.0  {#configure-salesforce-with-ouath-2.0-client-credential}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/oauth2-client-credentials-flow-for-server-to-server-integration.html?lang=it) |
| AEM 6.5 | Questo articolo |

Puoi utilizzare le credenziali client OAuth 2.0 per integrare AEM Forms con l’applicazione Salesforce. Le credenziali client OAuth 2.0 sono un metodo standard e sicuro per la comunicazione diretta senza il coinvolgimento dell’utente.

![Flusso di lavoro durante l’impostazione della comunicazione tra l’applicazione AEM Forms e Salesforce](/help/forms/using/assets/salesforce-workflow.png)

AEM Forms scambia le credenziali del client (chiave consumer e segreto consumer), definite nell’applicazione connessa Salesforce, per ottenere un token di accesso.

L’utilizzo delle credenziali del client OAuth 2.0 per l’autenticazione rispetto all’autenticazione del flusso del codice di autorizzazione offre diversi vantaggi:

* L&#39;autenticazione delle credenziali client OAuth 2.0 consente più di cinque connessioni per utente.
* La configurazione dell’origine dati dell’AEM continua a funzionare su disattivazione, modifiche di accesso, aggiornamento della password per un utente AEM.

## Prerequisiti {#prerequisites}

Prima di impostare la comunicazione tra un’applicazione Salesforce e un ambiente AEM:

* Creare un [App connessa Salesforce con flusso di credenziali client OAuth 2.0](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&amp;type=5) e un utente solo API per la tua organizzazione e ottenere la chiave del consumatore e il segreto del consumatore per l’app.

* Assicurati che il file Swagger sia configurato in modo appropriato per corrispondere alle API della tua organizzazione. In alternativa, puoi scegliere di [creare un file Swagger](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api.html) da zero, personalizzato per l’utilizzo nell’ambiente AEM.
>[!NOTE]
>
> AEM 6.5 supporta solo le specifiche dei file Swagger 2.0.

+++

## Passaggi per configurare Salesforce con il flusso delle credenziali del client {#steps-to-create-aem-datasource-configuration}

1. Accedi all’istanza di authoring.
1. Vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Origini dati]**.
1. Seleziona la cartella di configurazione.
1. Clic **[!UICONTROL Crea]** e **[!UICONTROL Crea configurazione origine dati]** viene visualizzato.
1. Specifica la **[!UICONTROL Titolo]** e seleziona la **[!UICONTROL Tipo di servizio]** as **[!UICONTROL Servizio RESTful]**.
1. Fai clic su **[!UICONTROL Avanti]**.
1. Seleziona la **[!UICONTROL Sorgente Swagger]** as **[!UICONTROL File].**
   >[!NOTE]
   >
   > Non appena il file Swagger viene selezionato, lo Schema, il nome host e il percorso di base vengono popolati automaticamente.

1. Carica il file Swagger creato dal computer locale facendo clic su **[!UICONTROL Sfoglia]**.
1. Seleziona la **[!UICONTROL Tipo di autenticazione]** as **[!UICONTROL OAuth 2.0]** e **[!UICONTROL Impostazioni di autenticazione]** viene visualizzato il pannello.
1. Seleziona la **[!UICONTROL Tipo di concessione]** as **[!UICONTROL Credenziali client]**.
1. Specifica la **[!UICONTROL ID client]** e **[!UICONTROL Segreto client]** ottenuti dall’app connessa Salesforce.
1. Specifica la **[!UICONTROL URL token di accesso]** in formato
   `https://[MyDomainName].my.salesforce.com/services/oauth2/token`.

   >[!NOTE]
   >
   > Ogni organizzazione ha il proprio nome di dominio specifico.

1. Clic **[!UICONTROL Verifica connessione]**.
1. Se la connessione ha esito positivo, fare clic sul pulsante **[!UICONTROL Crea]** pulsante.

Ora puoi [creare il modello dati del modulo](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html?lang=en) per integrare l’origine dati configurata con Adaptive Forms.
