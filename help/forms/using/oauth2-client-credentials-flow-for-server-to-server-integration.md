---
title: Integrazione di Salesforce con AEM Forms tramite il flusso delle credenziali client OAuth 2.0
description: Passaggi per integrare l’integrazione di Salesforce con AEM Forms utilizzando il flusso delle credenziali del client OAuth 2.0
exl-id: 4c356aa6-ebd4-40b9-89e3-bc4519e4a7c5
solution: Experience Manager, Experience Manager Forms
feature: Form Data Model
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 4%

---

# Integrazione di Salesforce tramite il flusso di credenziali client OAuth 2.0 {#configure-salesforce-with-ouath-2.0-client-credential}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/oauth2-client-credentials-flow-for-server-to-server-integration.html?lang=it) |
| AEM 6.5 | Questo articolo |

Puoi utilizzare le credenziali client OAuth 2.0 per integrare AEM Forms con l’applicazione Salesforce. Le credenziali client OAuth 2.0 sono un metodo standard e sicuro per la comunicazione diretta senza il coinvolgimento dell’utente.

![Flusso di lavoro durante l&#39;impostazione della comunicazione tra l&#39;applicazione AEM Forms e Salesforce](/help/forms/using/assets/salesforce-workflow.png)

AEM Forms scambia le credenziali del client (chiave consumer e segreto consumer), definite nell’applicazione connessa Salesforce, per ottenere un token di accesso.

L’utilizzo delle credenziali del client OAuth 2.0 per l’autenticazione rispetto all’autenticazione del flusso del codice di autorizzazione offre diversi vantaggi:

* L&#39;autenticazione delle credenziali client OAuth 2.0 consente più di cinque connessioni per utente.
* La configurazione dell’origine dati dell’AEM continua a funzionare su disattivazione, modifiche di accesso, aggiornamento della password per un utente AEM.

## Prerequisiti {#prerequisites}

Prima di impostare la comunicazione tra un’applicazione Salesforce e un ambiente AEM:

* Crea un&#39;app connessa a [Salesforce con flusso di credenziali client OAuth 2.0](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&amp;type=5) e un utente solo API per la tua organizzazione e ottieni la chiave consumer e il segreto consumer per l&#39;app.

* Assicurati che il file Swagger sia configurato in modo appropriato per corrispondere alle API della tua organizzazione. In alternativa, puoi scegliere di [creare un file Swagger](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api.html?lang=it) da zero, adatto all&#39;utilizzo nell&#39;ambiente AEM.
>[!NOTE]
>
> AEM 6.5 supporta solo le specifiche dei file Swagger 2.0.

+++

## Passaggi per configurare Salesforce con il flusso delle credenziali del client {#steps-to-create-aem-datasource-configuration}

1. Accedi all’istanza di authoring.
1. Vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Origini dati]**.
1. Seleziona la cartella di configurazione.
1. Fai clic su **[!UICONTROL Crea]** per visualizzare **[!UICONTROL Crea configurazione Data Source]**.
1. Specifica il **[!UICONTROL Titolo]** e seleziona il **[!UICONTROL Tipo di servizio]** come **[!UICONTROL Servizio RESTful]**.
1. Fai clic su **[!UICONTROL Avanti]**.
1. Seleziona **[!UICONTROL Swagger Source]** come **[!UICONTROL File].**
   >[!NOTE]
   >
   > Non appena il file Swagger viene selezionato, lo Schema, il nome host e il percorso di base vengono popolati automaticamente.

1. Carica il file Swagger creato dal computer locale facendo clic su **[!UICONTROL Sfoglia]**.
1. Selezionare **[!UICONTROL Tipo di autenticazione]** come **[!UICONTROL OAuth 2.0]** e viene visualizzato il pannello **[!UICONTROL Impostazioni autenticazione]**.
1. Selezionare **[!UICONTROL Tipo di concessione]** come **[!UICONTROL Credenziali client]**.
1. Specifica l&#39;**[!UICONTROL ID client]** e il **[!UICONTROL Segreto client]** ottenuti dall&#39;app connessa Salesforce.
1. Specifica l&#39;**[!UICONTROL URL token di accesso]** in formato
   `https://[MyDomainName].my.salesforce.com/services/oauth2/token`.

   >[!NOTE]
   >
   > Ogni organizzazione ha il proprio nome di dominio specifico.

1. Fare clic su **[!UICONTROL Verifica connessione]**.
1. Se la connessione riesce, fare clic sul pulsante **[!UICONTROL Crea]**.

Ora puoi [creare il modello dati del modulo](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html?lang=it) per integrare l&#39;origine dati configurata con il Forms adattivo.
