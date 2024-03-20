---
title: Come si collegano e inviano i dati del modulo adattivo a Microsoft&reg; Power Automate?
description: Guida dettagliata alla connessione e all'invio di dati di moduli adattivi a Microsoft&reg; Power Automate.
keywords: Adaptive Forms Microsoft Power Automate, invia dati Adaptive Forms a Microsoft Power Automate
feature: Adaptive Forms, Foundation Components
exl-id: 3fd26ddb-d247-462f-a0f6-8af6166516c1
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 2%

---

# Collegare e inviare i dati del modulo adattivo a Microsoft® Power Automate {#connect-adaptive-form-with-power-automate}

È possibile configurare un modulo adattivo per eseguire un flusso cloud di Microsoft® Power Automate all’invio. Il modulo adattivo configurato invia i dati acquisiti, gli allegati e il documento di record al flusso cloud Power Automate per l’elaborazione. Consente di creare un’esperienza di acquisizione dati personalizzata sfruttando al contempo la potenza di Microsoft® Power Automate per creare logiche di business basate sui dati acquisiti e automatizzare i flussi di lavoro dei clienti. Di seguito sono riportati alcuni esempi di cosa è possibile fare dopo l’integrazione di un modulo adattivo con Microsoft® Power Automate:

* Utilizzare dati Forms adattivi in processi aziendali Power Automate
* Utilizza Power Automate per inviare i dati acquisiti a più di 500 origini dati o a qualsiasi API disponibile pubblicamente
* Eseguire calcoli complessi sui dati acquisiti
* Salvataggio dei dati Adaptive Forms sui sistemi di storage secondo una pianificazione predefinita

L’editor di Forms adattivo fornisce **Richiama un flusso Microsoft® Power Automate** l’azione di invio per inviare i dati dei moduli adattivi, gli allegati e il documento di record viene inviata a Power Automate Cloud Flow. Per utilizzare l&#39;azione Invia per inviare i dati acquisiti a Microsoft® Power Automate, [Collegare l’istanza di AEM Forms Author con Microsoft® Power Automate](#connect-your-aem-forms-instance-with-microsoft&reg;-power-automate)

## Prerequisiti

Per collegare un modulo adattivo con Microsoft® Power Automate sono necessari i seguenti elementi:

* Licenza Microsoft® Power Automate Premium
* Microsoft® [Flusso di Power Automate](https://docs.microsoft.com/en-us/power-automate/create-flow-solution) con `When an HTTP request is received` trigger per accettare i dati di invio del modulo adattivo
* Un Experience Manager di utente con [Autore Forms](/help/forms/using/forms-groups-privileges-tasks.md) e [Amministratore Forms](/help/forms/using/forms-groups-privileges-tasks.md) privilegi
* L’account utilizzato per connettersi a Microsoft® Power Automate è il proprietario del flusso Power Automate configurato per ricevere i dati dal modulo adattivo


## Collegare l&#39;istanza AEM Forms con Microsoft® Power Automate {#connect-forms-server-with-power-automate}

Per collegare l’istanza AEM Forms Author con Microsoft® Power Automate, effettua le seguenti operazioni:

1. [Creazione di un Microsoft](#ms-power-automate-application)
1. [Crea Microsoft](#microsoft-power-automate-dataverse-cloud-configuration)
1. [Crea Microsoft](#create-microsoft-power-automate-flow-cloud-configuration)
1. [Pubblica Microsoft](#publish-microsoft-power-automate-dataverse-cloud-configuration)

### Crea applicazione Microsoft® Azure Active Directory {#ms-power-automate-application}

1. Accedi a [Portale Azure](https://portal.azure.com/).
1. Seleziona [!UICONTROL Azure Active Directory] dal menu di navigazione a sinistra.
1. Nella pagina Directory predefinita, selezionare [!UICONTROL Registrazioni app] dal pannello a sinistra.
1. Nella pagina Registrazioni app, fai clic su Nuove registrazioni.
1. Specifica il nome, i tipi di account supportati e l’URI di reindirizzamento nella pagina. Nell’URI di reindirizzamento, specifica quanto segue e fai clic su Salva.
   * `https://[AEM Forms Author instance]/libs/fd/powerautomate/content/dataverse/config.html`
   * `https://[AEM Forms Author instance]/libs/fd/powerautomate/content/flowservice/config.html`

   ![Registrare un&#39;applicazione Azure Active Directory](assets/power-automate-application.png)

   >[!NOTE]
   >Se necessario, puoi anche specificare URI di reindirizzamento aggiuntivi dalla pagina Autenticazione.
   > Per i tipi di account supportati, seleziona singolo tenant, più tenant o account Microsoft® personale a seconda del caso d’uso


1. Nella pagina Autenticazione, abilita le opzioni seguenti e fai clic su Salva.


   * Token di accesso (utilizzati per i flussi impliciti)
   * Token ID (utilizzati per flussi impliciti e ibridi)

1. Nella pagina Autorizzazioni API, fai clic su Aggiungi un’autorizzazione.
1. In API di Microsoft®, seleziona il servizio Flusso e le seguenti autorizzazioni.
   * Flows.Manage.All
   * Flows.Read.All

   Fai clic su Aggiungi autorizzazioni per salvare le autorizzazioni.
1. Nella pagina Autorizzazioni API, fai clic su Aggiungi un’autorizzazione. Seleziona le API utilizzate dalla mia organizzazione e cerca `DataVerse`.
1. Abilita user_impersonation e fai clic su Aggiungi autorizzazioni.
1. (Facoltativo) Nella pagina Certificati e segreti, fai clic su Nuovo segreto client. Nella schermata Aggiungi segreto client, fornisci una descrizione e un periodo di tempo per la scadenza del segreto, quindi fai clic su Aggiungi. Viene generata una stringa segreta.
1. Tieni nota delle specifiche della tua organizzazione [URL ambiente Dynamics](https://docs.microsoft.com/en-us/power-automate/web-api#compose-http-requests).

### Crea configurazione cloud Microsoft® Power Automate Dataverse {#microsoft-power-automate-dataverse-cloud-configuration}

1. Nell’istanza di authoring di AEM Forms, passa a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Generale]** > **[!UICONTROL Browser configurazioni]**.
1. Il giorno **[!UICONTROL Browser configurazioni]** pagina, seleziona **[!UICONTROL Crea]**.
1. In **[!UICONTROL Crea configurazione]** , specifica un **[!UICONTROL Titolo]** per la configurazione, abilita **[!UICONTROL Configurazioni cloud]**, e seleziona **[!UICONTROL Crea]**. Crea un contenitore di configurazione per archiviare i Cloud Service. Verificare che il nome della cartella non contenga spazio.
1. Accedi a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Microsoft®® Power Automate Dataverse]** e apri il contenitore di configurazione creato nel passaggio precedente.

   >[!NOTE]
   >
   >Quando crei un modulo adattivo, specifica il nome del contenitore in **[!UICONTROL Contenitore configurazione]** campo.

1. Nella pagina di configurazione, seleziona **[!UICONTROL Crea]** per creare [!DNL Microsoft®® Power Automate Flow Service] in AEM Forms.
1. Il giorno **[!UICONTROL Configurazione del servizio Dataverse per Microsoft®® Power Automate]** , specificare **[!UICONTROL ID client]** (indicato anche come ID applicazione), **[!UICONTROL Segreto client]**, **[!UICONTROL URL OAuth]** e **[!UICONTROL URL ambiente dinamico]**. Utilizza l’ID client, il segreto client, l’URL OAuth e l’URL dell’ambiente dinamico di [Applicazione Microsoft® Azure Active Directory](#ms-power-automate-application) creato nella sezione precedente. Utilizza l’opzione Endpoints nell’interfaccia utente dell’applicazione Microsoft® Azure Active Directory per trovare l’URL OAuth

   ![Utilizza l’opzione Endpoints nell’interfaccia utente dell’applicazione Microsoft Power Automate per trovare l’URL OAuth](assets/endpoints.png)

1. Seleziona **[!UICONTROL Connetti]** . Se richiesto, accedere all&#39;account Microsoft® Azure. Seleziona **[!UICONTROL Salva]**.

### Crea configurazione cloud del servizio Flow di Microsoft® Power Automate {#create-microsoft-power-automate-flow-cloud-configuration}

1. Accedi a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Servizio Flow di Microsoft®® Power Automate]** e apri il contenitore di configurazione creato nella sezione precedente.

   >[!NOTE]
   >
   >Quando crei un modulo adattivo, specifica il nome del contenitore in **[!UICONTROL Contenitore configurazione]** campo.
1. Nella pagina di configurazione, seleziona **[!UICONTROL Crea]** per creare [!DNL Microsoft®® Power Automate Flow Service] in AEM Forms.
1. Il giorno **[!UICONTROL Configurazione di Dataverse per Microsoft®® Power Automate]** , specificare **[!UICONTROL ID client]** (indicato anche come ID applicazione), **[!UICONTROL Segreto client]**, **[!UICONTROL URL OAuth]** e **[!UICONTROL URL ambiente dinamico]**. Utilizza l’ID client, il segreto client, l’URL OAuth e l’ID ambiente Dynamics. Utilizza l’opzione Endpoints nell’interfaccia utente dell’applicazione Microsoft® Azure Active Directory per trovare l’URL OAuth. Apri [I miei flussi](https://us.flow.microsoft.com) e seleziona I miei flussi utilizzano l’ID elencato nell’URL come ID ambiente Dynamics.
1. Seleziona **[!UICONTROL Connetti]**. Se richiesto, accedere all&#39;account Microsoft® Azure. Seleziona **[!UICONTROL Salva]**.

### Pubblicare le configurazioni cloud di Microsoft® Power Automate Dataverse e Microsoft® Power Automate Flow Service {#publish-microsoft-power-automate-dataverse-cloud-configuration}

1. Accedi a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Microsoft®® Power Automate Dataverse]** e apri il contenitore di configurazione creato in [Crea configurazione cloud Microsoft® Power Automate Dataverse](#microsoft-power-automate-dataverse-cloud-configuration) sezione.
1. Seleziona la `dataverse` configurazione e selezione **[!UICONTROL Pubblica]**.
1. Nella pagina Pubblica, seleziona **[!UICONTROL Tutte le configurazioni]** e seleziona **[!UICONTROL Pubblica]**. Pubblicare configurazioni cloud Power Automate Dataverse e Power Automate Flow Service.

L’istanza Autore AEM Forms è ora collegata a Microsoft® Power Automate. È ora possibile inviare dati Adaptive Forms a un flusso Power Automate.

## Utilizzare l&#39;azione di invio Richiama un flusso Microsoft® Power Automate per inviare i dati a un flusso Power Automate {#use-the-invoke-microsoft-power-automate-flow-submit-action}

Dopo di te [Collegare l’istanza di AEM Forms Author con Microsoft® Power Automate](#connect-forms-server-with-power-automate), esegui l’azione seguente per configurare il modulo adattivo per l’invio di dati acquisiti a un flusso Microsoft® al momento dell’invio del modulo.

1. Accedi all’istanza di authoring, seleziona il modulo adattivo e fai clic su **[!UICONTROL Proprietà]**.
1. Nel Contenitore di configurazione, sfoglia e seleziona il contenitore creato nella sezione [Crea configurazione cloud Microsoft® Power Automate Dataverse](#microsoft-power-automate-dataverse-cloud-configuration), e seleziona **[!UICONTROL Salva e chiudi]**.
1. Apri il modulo adattivo per la modifica e passa a **[!UICONTROL Invio]** sezione delle proprietà Contenitore modulo adattivo.
1. Nel contenitore delle proprietà, per **[!UICONTROL Invia azioni]** seleziona la **[!UICONTROL Richiama un flusso Power Automate]** opzione. Un elenco dei flussi di Power Automate disponibili è disponibile sotto **[!UICONTROL Flusso di Power Automate]** opzione. Seleziona il flusso richiesto e i dati di Adaptive Forms vengono inviati al momento dell’invio.

   ![Configura azione di invio](assets/submission.png)

>[!NOTE]
>
> Prima di inviare il modulo adattivo, assicurati che `When an HTTP Request is received` al flusso Power Automate viene aggiunto l’attivatore con lo schema JSON sottostante.

```
        {
            "type": "object",
            "properties": {
                "attachments": {
                    "type": "array",
                    "items": {
                        "type": "object",
                        "properties": {
                            "filename": {
                                "type": "string"
                            },
                            "data": {
                                "type": "string"
                            },
                            "contentType": {
                                "type": "string"
                            },
                            "size": {
                                "type": "integer"
                            }
                        },
                        "required": [
                            "filename",
                            "data",
                            "contentType",
                            "size"
                        ]
                    }
                },
                "templateId": {
                    "type": "string"
                },
                "templateType": {
                    "type": "string"
                },
                "data": {
                    "type": "string"
                },
                "document": {
                    "type": "object",
                    "properties": {
                        "filename": {
                            "type": "string"
                        },
                        "data": {
                            "type": "string"
                        },
                        "contentType": {
                            "type": "string"
                        },
                        "size": {
                            "type": "integer"
                        }
                    }
                }
            }
        }
```

## Vedi anche,

* [Creare un modulo adattivo](create-an-adaptive-form-core-components.md)
* [Configurare un’azione di invio](configuring-submit-actions.md)
* [Connettore Adobe Experience Manager per Microsoft® Power Automate](https://learn.microsoft.com/en-us/connectors/adobeexperiencemanag/)
