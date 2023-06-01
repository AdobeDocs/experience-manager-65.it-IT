---
title: Integrazione di Salesforce con AEM Forms tramite il flusso delle credenziali client OAuth 2.0
seo-title: Salesforce integration with AEM Forms using OAuth 2.0 client credentials flow
description: Passaggi per integrare l’integrazione di Salesforce con AEM Forms utilizzando il flusso delle credenziali del client OAuth 2.0
seo-description: Steps to integrate Salesforce integration with AEM Forms using OAuth 2.0 client credentials flow
source-git-commit: f03513c98455e00beef37819a5a47ba56dfa5028
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 0%

---


# Integrazione di Salesforce tramite il flusso delle credenziali client OAuth 2.0  {#configure-salesforce-with-ouath-2.0-client-credential}

Per integrare AEM Forms con l’applicazione Salesforce, viene utilizzato il flusso delle credenziali client OAuth 2.0. Si tratta di un metodo standardizzato e sicuro per la comunicazione diretta senza il coinvolgimento degli utenti. In questo flusso, l’applicazione client (Modulo AEM) scambia le credenziali client, definite nell’applicazione connessa Salesforce, per ottenere un token di accesso. Le credenziali client richieste includono la chiave consumer e il segreto consumer.

## Vantaggi dell’integrazione di Salesforce con AEM Forms tramite il flusso delle credenziali client OAuth 2.0 {#advantages-of-integrating-saleforce-aemforms}

AEM Forms supporta l’integrazione di Salesforce con il flusso del codice di autorizzazione, oltre al flusso delle credenziali del client OAuth 2.0. Nel flusso Codice di autorizzazione OAuth 2.0, l’applicazione client (AEM Forms) ottiene l’accesso alle risorse per conto di un utente Salesforce, con alcune limitazioni:

* Sono consentite al massimo cinque connessioni per utente. Ulteriori connessioni revocano automaticamente le connessioni meno recenti.
* Se un utente viene disattivato, perde l’accesso o aggiorna una password, la configurazione dell’origine dati AEM non funziona più.

## Prerequisiti {#prerequisites}

Per recuperare e recuperare i dati tra gli ambienti Salesforce e AEM è necessario soddisfare alcuni prerequisiti prima di procedere ulteriormente:

+++ **Configurare un’applicazione connessa Saleforce con un flusso di credenziali client e un utente solo API**

È obbligatorio creare un’app Salesforce connessa con un flusso di credenziali client OAuth 2.0 e un utente solo API per la tua organizzazione. Per i passaggi dettagliati, consulta l’articolo [Flusso delle credenziali client OAuth 2.0 per l&#39;integrazione server-to-server](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&amp;type=5). Questi passaggi ti aiutano a ottenere la chiave del consumatore e il segreto del consumatore.

>[!NOTE]
>
> Assicurati di annotare la chiave del consumatore e il segreto del consumatore in quanto sono necessari durante la creazione di una configurazione di origine dati AEM.

+++

+++ **Creare un file Swagger**

Swagger è un set open-source di regole, specifiche e strumenti per sviluppare e descrivere le API RESTful. [Creare un file Swagger](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api.html) prima di integrare Salesforce con AEM Forms.

    >[!NOTA]
    >
    > AEM 6.5 supporta solo le specifiche dei file Swagger 2.0.

+++

## Passaggi per configurare Salesforce con il flusso delle credenziali del client {#steps-to-create-aem-datasource-configuration}

1. Accedi all’istanza di authoring.
1. Vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Origini dati]**.
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

Ora puoi [creare il modello dati del modulo](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html?lang=en) per integrare l’origine dati configurata con il modulo adattivo.


