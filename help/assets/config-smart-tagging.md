---
title: Configurare l’assegnazione tag delle risorse tramite Smart Content Service
description: Scopri come configurare l'assegnazione tag avanzati e l'assegnazione tag avanzati migliorati in [!DNL Adobe Experience Manager], utilizzando il Servizio di contenuti avanzati.
role: Admin
feature: Tagging,Smart Tags
exl-id: 9f68804f-ba15-4f83-ab1b-c249424b1396
solution: Experience Manager, Experience Manager Assets
source-git-commit: 7c1aeec18f35b019a63d0385ada248b26a0df9de
workflow-type: tm+mt
source-wordcount: '2130'
ht-degree: 14%

---

# Prepara [!DNL Assets] per assegnazione tag avanzati {#configure-asset-tagging-using-the-smart-content-service}

Prima di iniziare a assegnare tag alle risorse tramite Smart Content Services, è necessario integrare [!DNL Experience Manager Assets] con Adobe Developer Console per utilizzare il servizio intelligente di [!DNL Adobe AI]. Una volta configurato, il servizio viene addestrato utilizzando alcune immagini e un tag.

<!--
>[!NOTE]
>
>* Smart Content Services is no longer available to new [!DNL Experience Manager Assets] On-Premise customers. Existing On-Premise customers, who already have this capability enabled, can continue using Smart Content Services.
>* Smart Content Services is available for existing [!DNL Experience Manager Assets] Managed Services customers, who already have this capability enabled.
>* New Experience Manager Assets Managed Services customers can follow the instructions mentioned in this article to set up Smart Content Services.
>* For Service Pack 20 and older, you need to perform the workaround steps for SCS to support Oauth integration. See [Troubleshooting smart tags for OAuth credentials](config-oauth.md).
>* To support the Oauth integration on Service Pack 21, you need to install the [Hotfix for SP 21](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fproduct%2Fassets%2Fcq-6.5.0-hotfix-40772-1.2.zip). 
>* For Existing SCS configuration, the process is the same as setting up a new OAuth integration. Any legacy configuration will be automatically cleaned up.
-->

Prima di utilizzare il Servizio di contenuti avanzati, verifica quanto segue:

* [Integrare con Adobe Developer Console](#integrate-adobe-io).
* [Formazione del Servizio di contenuti avanzati](#training-the-smart-content-service).

* Installa il [[!DNL Experience Manager] Service Pack](https://experienceleague.adobe.com/it/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates) più recente.

## Aggiornamento SCS per supportare Oauth per Adobe Managed Services {#scs-upgrade-oauth-managed-services}

**Nuovi utenti**

Installare Service Pack 22. Per supportare l&#39;integrazione Oauth in Service Pack 22, è necessario installare [Hotfix per Service Pack 22](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fproduct%2Fassets%2Fcq-6.5.0-hotfix-42384-1.2.zip).

Segui le istruzioni riportate in questo articolo per configurare Smart Content Services.

**Utenti esistenti**

Se è stato eseguito l&#39;aggiornamento al Service Pack 21, installare [Hotfix per Service Pack 21](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fproduct%2Fassets%2Fcq-6.5.0-hotfix-40772-1.2.zip) per supportare l&#39;integrazione Oauth. Qualsiasi configurazione esistente viene eliminata automaticamente. Segui le istruzioni riportate in questo articolo per configurare Smart Content Services. Se si esegue l&#39;aggiornamento al Service Pack 22, è necessario installare questo [Hotfix per Service Pack 22](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fproduct%2Fassets%2Fcq-6.5.0-hotfix-42384-1.2.zip).

Per Service Pack 20 e versioni precedenti, è necessario eseguire i passaggi per la soluzione alternativa per il supporto dell’integrazione Oauth da parte di SCS. Consulta [Risoluzione dei problemi relativi agli smart tag per le credenziali OAuth](config-oauth.md).

## Aggiornamento SCS per supportare Oauth per gli utenti on-premise {#scs-upgrade-oauth-on-premise}

**Nuovi utenti**

Smart Content Services non è più disponibile per i nuovi utenti locali di [!DNL Experience Manager Assets].

**Utenti esistenti**

Gli utenti on-premise esistenti che dispongono già di questa funzionalità possono continuare a utilizzare Smart Content Services.

Se è stato eseguito l&#39;aggiornamento al Service Pack 21, installare [Hotfix per Service Pack 21](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fproduct%2Fassets%2Fcq-6.5.0-hotfix-40772-1.2.zip) per supportare l&#39;integrazione Oauth. Qualsiasi configurazione esistente viene eliminata automaticamente. Segui le istruzioni riportate in questo articolo per configurare Smart Content Services. Se si esegue l&#39;aggiornamento al Service Pack 22, è necessario installare questo [Hotfix per Service Pack 22](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fproduct%2Fassets%2Fcq-6.5.0-hotfix-42384-1.2.zip).

Per Service Pack 20 e versioni precedenti, è necessario eseguire i passaggi per la soluzione alternativa per il supporto dell’integrazione Oauth da parte di SCS. Consulta [Risoluzione dei problemi relativi agli smart tag per le credenziali OAuth](config-oauth.md).


## Integrare con Adobe Developer Console {#integrate-adobe-io}

Quando si esegue l&#39;integrazione con Adobe Developer Console, il server [!DNL Experience Manager] autentica le credenziali del servizio con il gateway di Adobe Developer Console prima di inoltrare la richiesta al Servizio di contenuti avanzati. Per l’integrazione, è necessario un account Adobe ID con privilegi di amministratore per l’organizzazione e una licenza del Servizio di contenuti avanzati acquistata e abilitata per la tua organizzazione.

Per configurare il Servizio di contenuti avanzati, segui questi passaggi di livello principale:

1. Crea un&#39;integrazione in [Adobe Developer Console](#create-adobe-io-integration).

1. Crea una configurazione dell&#39;account tecnico IMS [&#128279;](#create-ims-account-config) utilizzando la chiave API e altre credenziali di Adobe Developer Console.

1. [Configura il Servizio di contenuti avanzati](#configure-smart-content-service).

1. [Verifica la configurazione](#validate-the-configuration).

<!--
To configure the Smart Content Service, follow these top-level steps:

1. To generate a public key, [Create a Smart Content Service] (#obtain-public-certificate) configuration in [!DNL Experience Manager]. 

1. Optionally, [enable auto-tagging on asset upload](#enable-smart-tagging-in-the-update-asset-workflow-optional).

   <!--1. [Obtain public certificate](#obtain-public-certificate) for OAuth integration.
   1. [Create an integration in Adobe Developer Console](#create-adobe-i-o-integration) and upload the generated public key.

   1. [Configure your deployment](#configure-smart-content-service) using the API key and other credentials from Adobe Developer Console.

   1. [Test the configuration](#validate-the-configuration).-->

### Creare l’integrazione con Adobe Developer Console {#create-adobe-io-integration}

Per utilizzare le API del Servizio di contenuti avanzati, crea un’integrazione in Adobe Developer Console per ottenere quanto segue:

* [!UICONTROL CHIAVE API] (generata nel campo [!UICONTROL ID CLIENT] dell&#39;integrazione Adobe Developer Console),
* [!UICONTROL ID ORGANIZZAZIONE],
* e [!UICONTROL SEGRETO CLIENT], per [!UICONTROL Impostazioni servizio di assegnazione tag avanzati Assets] della configurazione cloud in [!DNL Experience Manager].

1. Accedi a [https://developer.adobe.com](https://developer.adobe.com/) in un browser. Selezionare l&#39;account appropriato e verificare che il ruolo organizzazione associato sia **amministratore** di sistema.

1. Crea un progetto con il nome desiderato. Fai clic su **[!UICONTROL Aggiungi API]**.

1. Nella pagina **[!UICONTROL Aggiungi un’API]**, seleziona **[!UICONTROL Experience Cloud]** e **[!UICONTROL Contenuti avanzati]**. Fai clic su **[!UICONTROL Avanti]**.

1. Selezionare **[!UICONTROL OAuth Server-to-Server]**. Fai clic su **[!UICONTROL Avanti]**.
Per informazioni dettagliate su come eseguire questa configurazione, consulta la documentazione di Developer Console, a seconda dei requisiti:

   * Per una panoramica, vedere *Autenticazione da server a server* su developer.adobe.com.
   * Per creare una nuova credenziale OAuth, consulta la *Guida all&#39;implementazione delle credenziali server-to-server OAuth* su developer.adobe.com.
   * Per eseguire la migrazione di una credenziale JWT esistente a una credenziale OAuth, vedere *Migrazione delle credenziali dall&#39;account di servizio (JWT) alle credenziali server-to-server OAuth* in developer.adobe.com.


1. Nella pagina **[!UICONTROL Seleziona profili di prodotto]**, seleziona **[!UICONTROL Servizi di contenuti avanzati]**, quindi fai clic sull&#39;opzione **[!UICONTROL Salva API configurata]**.

   In una pagina vengono visualizzate ulteriori informazioni sulla configurazione. Tieni aperta questa pagina per copiare e aggiungere questi valori nelle [!UICONTROL Impostazioni del servizio di assegnazione tag avanzati di Assets] della configurazione cloud in [!DNL Experience Manager] per configurare gli smart tag.

   ![Credenziali OAuth in Developer Console](assets/ims-configuration-developer-console.png)

### Creare la configurazione dell’account tecnico IMS {#create-ims-account-config}

Devi creare una configurazione dell’account tecnico IMS seguendo questi passaggi:

1. Nell’interfaccia utente di [!DNL Experience Manager], accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Sicurezza]** > **[!UICONTROL Configurazioni Adobe IMS]**.

1. Fai clic su **[!UICONTROL Crea]**.

1. Nella finestra di dialogo Configurazione account tecnico IMS, utilizza i seguenti valori:

   ![Finestra di configurazione Adobe IMS](assets/adobe-ims-config.png)

   | Campo | Descrizione |
   | -------- | ---------------------------- |
   | Soluzione cloud | Scegli **[!UICONTROL Tag avanzati]** dal menu a discesa. |
   | Titolo | Aggiungi il titolo della configurazione dell’account IMS. |
   | Server autorizzazioni | Aggiungi `https://ims-na1.adobelogin.com` |
   | ID client | Da fornire tramite la [console Adobe Developer](https://developer.adobe.com/console/). |
   | Segreto client | Da fornire tramite la [console Adobe Developer](https://developer.adobe.com/console/). |
   | Ambito | Da fornire tramite la [console Adobe Developer](https://developer.adobe.com/console/). |
   | ID organizzazione | Da fornire tramite la [console Adobe Developer](https://developer.adobe.com/console/). |

1. Selezionare la configurazione creata e fare clic su **[!UICONTROL Verifica stato]**.

1. Confermare la finestra di dialogo Verifica stato e fare clic su Chiudi una volta che la configurazione è nello stato integro.

### Crea una nuova configurazione {#configure-smart-content-service}

<!--
>[!CAUTION]
>
>Previously, configurations that were made with JWT Credentials are now subject to deprecation in the Adobe Developer Console. You cannot create new JWT credentials after June 3, 2024. Such configurations can no longer be created or updated, but can be migrated to OAuth configurations.
> See [Setting up IMS integrations for AEM](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service)
>See [Steps to configure OAuth for on-premise users](#config-oauth-onprem)
> See [Troubleshooting smart tags for OAuth credentials](#config-smart-tagging.md)
-->

Per configurare l&#39;integrazione, utilizzare i valori dei campi [!UICONTROL ID ACCOUNT TECNICO], [!UICONTROL ID ORGANIZZAZIONE], [!UICONTROL SEGRETO CLIENT] e [!UICONTROL ID CLIENT] dell&#39;integrazione Adobe Developer Console. La creazione di una configurazione cloud di tag avanzati consente l&#39;autenticazione delle richieste API dalla distribuzione [!DNL Experience Manager].

1. In [!DNL Experience Manager], passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Smart Tag]** per aprire le [!UICONTROL Configurazioni smart tag].

1. Fai clic su **[!UICONTROL Crea]** per creare una nuova configurazione. In caso contrario, fare clic su **[!UICONTROL Proprietà]** per aggiornare la configurazione esistente.

1. Compila i campi seguenti:

   ![Configurazione tag avanzati](assets/smart-tags-config.png)

   | Campo | Descrizione |
   | -------- | ---------------------------- |
   | Titolo | Aggiungi il titolo della configurazione dell’account IMS. |
   | Configurazione Adobe IMS associata | Scegli una configurazione dal menu a discesa. |
   | URL del servizio | `https://smartcontent.adobe.io/<region where your Experience Manager author instance is hosted>`. Ad esempio, `https://smartcontent.adobe.io/apac`. È possibile specificare `na`, `emea` o `apac` come aree in cui è ospitata l&#39;istanza di authoring di Experience Manager. |

   >[!NOTE]
   >
   >Se il provisioning del servizio gestito di Experience Manager è stato eseguito prima del 1° settembre 2022, utilizza il seguente URL del servizio:
   >`https://mc.adobe.io/marketingcloud/smartcontent`

1. Fai clic su **[!UICONTROL Salva e chiudi]**.

### Convalidare la configurazione {#validate-the-configuration}

Dopo aver completato la configurazione, puoi utilizzare un MBean JMX per convalidarla. Per eseguire la convalida, effettua le seguenti operazioni.

1. Accedi al server di [!DNL Experience Manager] all’indirizzo `https://[aem_server]:[port]`.

1. Vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console Web]** per aprire la console OSGi. Fai clic su **[!UICONTROL Principale] > [!UICONTROL JMX]**.

<!--
1. Click `com.day.cq.dam.similaritysearch.internal.impl`. It opens **[!UICONTROL SimilaritySearch Miscellaneous Tasks]**.-->

1. Fai clic su `com.day.cq.dam.similaritysearch.internal.impl (SCS)`.

   ![Finestra Mbean](assets/mbean.png)

1. Fai clic su `validateConfigs()`. Nella finestra di dialogo **[!UICONTROL Validate Configurations]** (Convalida configurazioni), fai clic su **[!UICONTROL Invoke]** (Richiama).

I risultati della convalida vengono visualizzati nella stessa finestra di dialogo.

<!--
### Obtain public certificate by creating Smart Content Service configuration {#obtain-public-certificate}

A public certificate lets you authenticate your profile on Adobe Developer Console.

1. In the [!DNL Experience Manager] user interface, access **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Legacy Cloud Services]**.

1. In the Cloud Services page, click **[!UICONTROL Configure Now]** under **[!UICONTROL Assets Smart Tags]**.

1. In the **[!UICONTROL Create Configuration]** dialog, specify a title and name for the Smart Tags configuration. Click **[!UICONTROL Create]**.

1. In the **[!UICONTROL AEM Smart Content Service]** dialog, use the following values:

   **[!UICONTROL Service URL]**: `https://smartcontent.adobe.io/<region where your Experience Manager author instance is hosted>`

   For example, `https://smartcontent.adobe.io/apac`. You can specify `na`, `emea`, or, `apac` as the regions where your Experience Manager author instance is hosted. 

   >[!NOTE]
   >
   >If the Experience Manager Managed Service is provisioned before September 01, 2022, use the following Service URL:
   >`https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL Authorization Server]**: `https://ims-na1.adobelogin.com`

   Leave the other fields blank for now (to be provided later). Click **[!UICONTROL OK]**.

   ![Experience Manager Smart Content Service dialog to provide content service URL](assets/aem_scs.png)


   *Figure: Smart Content Service dialog to provide content service URL*

   >[!NOTE]
   >
   >The URL provided as [!UICONTROL Service URL] is not accessible via browser and generates a 404 error. The configuration works OK with the same value of the [!UICONTROL Service URL] parameter. For the overall service status and maintenance schedule, see [https://status.adobe.com](https://status.adobe.com).

1. Click **[!UICONTROL Download Public Certificate for OAuth Integration]**, and download the public certificate file `AEM-SmartTags.crt`.

   ![A representation of the settings created for the smart tagging service](assets/smart-tags-download-public-cert.png)


   *Figure: Settings for smart tagging service.*

#### Reconfigure when a certificate expires {#certrenew}

After a certificate expires, it is no longer trusted. You cannot renew an expired certificate. To add a certificate, follow these steps.

1. Log in your [!DNL Experience Manager] deployment as an administrator. Click **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**.

1. Locate and click **[!UICONTROL dam-update-service]** user. Click **[!UICONTROL Keystore]** tab.

1. Delete the existing **[!UICONTROL similaritysearch]** keystore with the expired certificate. Click **[!UICONTROL Save & Close]**.

   ![Delete the existing similarity search entry in Keystore to add a security certificate](assets/smarttags_delete_similaritysearch_keystore.png)


   *Figure: Delete the existing `similaritysearch` entry in Keystore to add a security certificate.*

1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Legacy Cloud Services]**. Click **[!UICONTROL Asset Smart Tags]** > **[!UICONTROL Show Configuration]** > **[!UICONTROL Available Configurations]**. Click the required configuration.  

1. To download a public certificate, click **[!UICONTROL Download Public Certificate for OAuth Integration]**.

1. Access [https://console.adobe.io](https://console.adobe.io) and navigate to the existing Smart Content Services on the **[!UICONTROL Integrations]** page. Upload the new certificate. For more information, see the instructions in [Create Adobe Developer Console integration](#create-adobe-i-o-integration).

### Create Adobe Developer Console integration {#create-adobe-i-o-integration}

To use Smart Content Service APIs, create an integration in Adobe Developer Console to obtain [!UICONTROL API Key] (generated in [!UICONTROL CLIENT ID] field of Adobe Developer Console integration), [!UICONTROL TECHNICAL ACCOUNT ID], [!UICONTROL ORGANIZATION ID], and [!UICONTROL CLIENT SECRET] for [!UICONTROL Assets Smart Tagging Service Settings] of cloud configuration in [!DNL Experience Manager].

1. Access [https://console.adobe.io](https://console.adobe.io/) in a browser. Select the appropriate account and verify that the associated organization role is system administrator.

1. Create a project with any desired name. Click **[!UICONTROL Add API]**.

1. On the **[!UICONTROL Add an API]** page, select **[!UICONTROL Experience Cloud]** and select **[!UICONTROL Smart Content]**. Click **[!UICONTROL Next]**.

1. Select **[!UICONTROL Upload your public key]**. Provide the certificate file downloaded from [!DNL Experience Manager]. A message [!UICONTROL Public key(s) uploaded successfully] is displayed. Click **[!UICONTROL Next]**.

   [!UICONTROL Create a new Service Account (JWT) credential] page displays the public key for the service account.

1. Click **[!UICONTROL Next]**.

1. On the **[!UICONTROL Select product profiles]** page, select **[!UICONTROL Smart Content Services]**. Click **[!UICONTROL Save configured API]**.

   A page displays more information about the configuration. Keep this page open to copy and add these values in [!UICONTROL Assets Smart Tagging Service Settings] of cloud configuration in [!DNL Experience Manager] to configure smart tags.

   ![In the Overview tab, you can review the information provided for integration.](assets/integration_details.png)


   *Figure: Details of integration in Adobe Developer Console*

### Configure Smart Content Service {#configure-smart-content-service}

>[!CAUTION]
>
>Previously, configurations that were made with JWT Credentials are now subject to deprecation in the Adobe Developer Console. You cannot create new JWT credentials after June 3, 2024. Such configurations can no longer be created or updated, but can be migrated to OAuth configurations.
> See [Setting up IMS integrations for AEM](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service)
>See [Steps to configure OAuth for on-premise users](#config-oauth-onprem)
> See [Troubleshooting smart tags for OAuth credentials](#config-smart-tagging.md)

To configure the integration, use the values of [!UICONTROL TECHNICAL ACCOUNT ID], [!UICONTROL ORGANIZATION ID], [!UICONTROL CLIENT SECRET], and [!UICONTROL CLIENT ID] fields from the Adobe Developer Console integration. Creating a Smart Tags cloud configuration allows authentication of API requests from the [!DNL Experience Manager] deployment.

1. In [!DNL Experience Manager], navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Legacy Cloud Services]** to open the [!UICONTROL Cloud Services] console.

1. Under the **[!UICONTROL Assets Smart Tags]**, open the configuration created above. On the service settings page, click **[!UICONTROL Edit]**.

1. In the **[!UICONTROL AEM Smart Content Service]** dialog, use the pre-populated values for the **[!UICONTROL Service URL]** and **[!UICONTROL Authorization Server]** fields.

1. For the fields [!UICONTROL Api Key], [!UICONTROL Technical Account ID], [!UICONTROL Organization ID], and [!UICONTROL Client Secret], copy and use the following values generated in [Adobe Developer Console integration](#create-adobe-i-o-integration).

   | [!UICONTROL Assets Smart Tagging Service Settings] | [!DNL Adobe Developer Console] integration fields |
   |--- |--- |
   | [!UICONTROL Api Key] | [!UICONTROL CLIENT ID] |
   | [!UICONTROL Technical Account ID] | [!UICONTROL TECHNICAL ACCOUNT ID] |
   | [!UICONTROL Organization ID] | [!UICONTROL ORGANIZATION ID] |
   | [!UICONTROL Client Secret] | [!UICONTROL CLIENT SECRET] |

### Configure OAuth for on-premise users {#config-oauth-onprem}

#### Prerequisites {#prereqs-config-oauth-onprem}

An authorization scope is an OAuth string that contains the following prerequisites:

* Create a new OAuth integration in the [Developer Console](https://developer.adobe.com/console/user/servicesandapis) using `ClientID`, `ClientSecretID`, and `OrgID`.
* Add the following files at this path `/apps/system/config in crx/de`:
   * `com.adobe.granite.auth.oauth.accesstoken.provider.<randomnumbers>.config`
   * `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl.<randomnumber>.config`

#### Configure OAuth for on-premise users {#steps-config-oauth-onprem}

1. Add or update the below properties in `com.adobe.granite.auth.oauth.accesstoken.provider.<randomnumbers>.config`:

   * `auth.token.provider.authorization.grants="client_credentials"`
   * `auth.token.provider.orgId="<OrgID>"`
   * `auth.token.provider.default.claims=("\"iss\"\ :\ \"<OrgID>\"")`
   * `auth.token.provider.scope="read_pc.dma_smart_content,\ openid,\ AdobeID,\ additional_info.projectedProductContext"`
     `auth.token.validator.type="adobe-ims-similaritysearch"`
   * Update the `auth.token.provider.client.id` with the Client ID of the new OAuth configuration.
   * Update `auth.access.token.request` to `"https://ims-na1.adobelogin.com/ims/token/v3"`
2. Rename the file to `com.adobe.granite.auth.oauth.accesstoken.provider-<randomnumber>.config`.
3. Perform the steps below in `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl.<randomnumber>.config`:
   * Update the property auth.ims.client.secret with the Client Secret from the new OAuth integration.
   * Rename the file to `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl-<randomnumber>.config`
4. Save all the changes in content repository development console, for example, CRXDE.
5. Navigate to `/system/console/configMgr` and replace the OSGi configuration from `.<randomnumber>` to `-<randomnumber>`.
6. Delete the old configuration for `"Access Token provider name: adobe-ims-similaritysearch"` in `/system/console/configMgr`.
7. Restart the console.

### Validate the configuration {#validate-the-configuration}

After you have completed the configuration, you can use a JMX MBean to validate the configuration. To validate, follow these steps.

1. Access your [!DNL Experience Manager] server at `https://[aem_server]:[port]`.

1. Go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]** to open the OSGi console. Click **[!UICONTROL Main] > [!UICONTROL JMX]**.

1. Click `com.day.cq.dam.similaritysearch.internal.impl`. It opens **[!UICONTROL SimilaritySearch Miscellaneous Tasks]**.

1. Click `validateConfigs()`. In the **[!UICONTROL Validate Configurations]** dialog, click **[!UICONTROL Invoke]**.

The validation results are displayed in the same dialog.
-->

### Abilitare l&#39;assegnazione tag avanzati nel flusso di lavoro [!UICONTROL Risorsa di aggiornamento DAM] (facoltativo) {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. In [!DNL Experience Manager], vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.

1. Nella pagina **[!UICONTROL Modelli flusso di lavoro]**, seleziona il modello di flusso di lavoro **[!UICONTROL Risorsa di aggiornamento DAM]**.

1. Fai clic su **[!UICONTROL Modifica]** nella barra degli strumenti.

1. Per visualizzare i passaggi, espandi il pannello laterale. Trascina il passaggio **[!UICONTROL Risorsa di tag avanzati]** disponibile nella sezione Flusso di lavoro DAM e inseriscilo dopo il passaggio **[!UICONTROL Elabora miniature]**.

   ![Aggiungere il passaggio Assegna tag avanzati a risorse dopo il passaggio Elabora miniature nel flusso di lavoro Aggiorna risorsa DAM](assets/smart-tag-in-dam-update-asset-workflow.png)

1. Apri le proprietà del passaggio per modificare i dettagli. In **[!UICONTROL Impostazioni avanzate]**, accertati che sia selezionata l’opzione **[!UICONTROL Avanzamento gestore]**.

   ![Configurare il flusso di lavoro Aggiorna risorsa DAM e aggiungere il passaggio smart tag](assets/smart-tag-step-properties-workflow1.png)

1. Nella scheda **[!UICONTROL Argomenti]**, seleziona **[!UICONTROL Ignora errori]** se vuoi che il flusso di lavoro venga completato anche con esito negativo del passaggio di assegnazione tag automatica.

   Inoltre, per assegnare i tag alle risorse quando vengono caricate, a prescindere dal fatto che l&#39;assegnazione tag avanzati sia abilitata o meno per le cartelle, seleziona **[!UICONTROL Ignora flag di tag avanzati]**.

   ![Configura il flusso di lavoro Risorsa di aggiornamento DAM per aggiungere il passaggio smart tag e selezionare l&#39;handler avanzato](assets/smart-tag-step-properties-workflow2.png)

1. Fai clic sull&#39;icona Fine ![fine](assets/do-not-localize/check-ok-done-icon.png) per chiudere il passaggio del processo.

1. Fai clic su **[!UICONTROL Sincronizza]** per salvare il flusso di lavoro.

## Formazione del Servizio di contenuti avanzati {#training-the-smart-content-service}

Affinché il Servizio di contenuti avanzati riconosca la tassonomia aziendale, eseguilo su una serie di risorse che includono già tag rilevanti per la tua azienda. Per assegnare tag efficaci alle immagini del tuo marchio, il Servizio di contenuti avanzati richiede che le immagini di formazione siano conformi a determinate linee guida. Dopo l’addestramento, il servizio può applicare la stessa tassonomia a un set di risorse simile.

Puoi addestrare il servizio più volte per migliorarne la capacità di applicare tag rilevanti. Dopo ogni ciclo di formazione, esegui un flusso di lavoro sui tag e verifica che alle risorse siano assegnati i tag appropriati.

Puoi addestrare il Servizio di contenuti avanzati periodicamente o in base ai requisiti.

>[!NOTE]
>
>Il flusso di lavoro di formazione viene eseguito solo sulle cartelle.

### Linee guida per la formazione {#guidelines-for-training}

Per ottenere risultati ottimali, le immagini del set di apprendimento sono conformi alle seguenti linee guida:

**Quantity and size (Quantità e dimensioni)**: almeno 30 immagini per tag. Almeno 500 pixel sul lato più lungo.

**Coerenza**: le immagini utilizzate per un tag specifico sono visivamente simili.

Ad esempio, non è consigliabile assegnare a tutte queste immagini il tag `my-party` (per la formazione) perché non sono visivamente simili.

![Immagini illustrative che illustrano le linee guida per la formazione](/help/assets/assets/do-not-localize/coherence.png)

**Copertura**: utilizza una varietà sufficiente di immagini nel corso di formazione. L&#39;idea è quella di fornire alcuni esempi, ma ragionevolmente diversi, in modo che l&#39;Experience Manager apprenda a concentrarsi sulle cose giuste. Se applichi lo stesso tag a immagini visivamente diverse, includi almeno cinque esempi per ogni tipo.

Ad esempio, per il tag *model-down-pose*, includi più immagini di formazione simili all&#39;immagine evidenziata di seguito affinché il servizio identifichi più accuratamente immagini simili durante l&#39;assegnazione dei tag.

![Immagini illustrative che illustrano le linee guida per la formazione](/help/assets/assets/do-not-localize/coverage_1.png)

**Distrazione/ostruzione**: il servizio si addestra meglio alle immagini che hanno meno distrazione (sfondi prominenti, accompagnamenti non correlati, come oggetti/persone con il soggetto principale).

Ad esempio, per il tag *casual-shoe*, la seconda immagine non è un buon candidato per la formazione.

![Immagini illustrative che illustrano le linee guida per la formazione](/help/assets/assets/do-not-localize/distraction.png)

**Completeness (Completezza):** se un’immagine è idonea per più tag, aggiungi tutti i tag applicabili prima di includere l’immagine nella formazione. Ad esempio, per tag come `raincoat` e `model-side-view`, aggiungi entrambi i tag alla risorsa idonea prima di includerla nella formazione.

![Immagini illustrative che illustrano le linee guida per la formazione](/help/assets/assets/do-not-localize/completeness.png)

>[!NOTE]
>
>La capacità del Servizio di contenuti avanzati di addestrarsi sui tag e di applicarli ad altre immagini dipende dalla qualità delle immagini utilizzate per la formazione. Per ottenere i migliori risultati, Adobe consiglia di utilizzare immagini visivamente simili per addestrare il servizio per ogni tag.

### Formazione periodica {#periodic-training}

Puoi abilitare il Servizio di contenuti avanzati per la formazione periodica sulle risorse e sui tag associati all’interno di una cartella. Apri la pagina [!UICONTROL Proprietà] della cartella di risorse, seleziona **[!UICONTROL Abilita tag avanzati]** nella scheda **[!UICONTROL Dettagli]** e salva le modifiche.

![enable_smart_tags](assets/enable_smart_tags.png)

Una volta selezionata questa opzione per una cartella, [!DNL Experience Manager] esegue automaticamente un flusso di lavoro di formazione per addestrare il Servizio di contenuti avanzati sulle risorse della cartella e sui relativi tag. Per impostazione predefinita, il flusso di lavoro di formazione viene eseguito settimanalmente alle ore 00:00 del sabato.:30

### Formazione on-demand {#on-demand-training}

Puoi addestrare il Servizio di contenuti avanzati quando necessario dalla console Flusso di lavoro.

1. Nell&#39;interfaccia [!DNL Experience Manager], vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.
1. Dalla pagina **[!UICONTROL Modelli di flusso di lavoro]**, seleziona il flusso di lavoro **[!UICONTROL Apprendimento dei tag avanzati]**, quindi fai clic su **[!UICONTROL Avvia flusso di lavoro]** nella barra degli strumenti.
1. Nella finestra di dialogo **[!UICONTROL Esegui flusso di lavoro]**, individua la cartella del payload che include le risorse con tag per l&#39;apprendimento del servizio.
1. Specifica un titolo per il flusso di lavoro e aggiungi un commento. Quindi fare clic su **[!UICONTROL Esegui]**. Le risorse e i tag vengono inviati per la formazione.

   ![workflow_dialog](assets/workflow_dialog.png)

>[!NOTE]
>
>Una volta elaborate le risorse di una cartella per l’apprendimento, solo le risorse modificate vengono elaborate nei cicli di apprendimento successivi.

### Visualizzare i rapporti di formazione {#viewing-training-reports}

Per verificare se il Servizio di contenuti avanzati è stato addestrato sui tag nel set di formazione di risorse, controlla il rapporto sul flusso di lavoro di formazione dalla console Rapporti.

1. Nell&#39;interfaccia [!DNL Experience Manager], vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Rapporti]**.
1. Nella pagina **[!UICONTROL Rapporti risorse]**, fai clic su **[!UICONTROL Crea]**.
1. Seleziona il report **[!UICONTROL Apprendimento dei tag avanzati]** e fai clic su **[!UICONTROL Avanti]** nella barra degli strumenti.
1. Specifica un titolo e una descrizione per il rapporto. In **[!UICONTROL Pianifica rapporto]**, lascia selezionata l’opzione **[!UICONTROL Now (Ora)]**. Se vuoi pianificare il rapporto per un momento successivo, seleziona **[!UICONTROL Later (Più tardi)]** e specifica una data e un’ora. Quindi fare clic su **[!UICONTROL Crea]** nella barra degli strumenti.
1. Nella pagina **[!UICONTROL Rapporti su risorse]**, seleziona il rapporto generato. Per visualizzare il report, fare clic su **[!UICONTROL Visualizza]** nella barra degli strumenti.
1. Esamina i dettagli del rapporto.

   Il rapporto mostra lo stato di formazione per i tag che hai appreso. La presenza del colore verde nella colonna **[!UICONTROL Training Status (Stato formazione)]** indica che per il tag è stato eseguito il training del servizio di contenuti avanzati. Se invece del verde è presente il colore giallo, il training del servizio di contenuti avanzati non è stato completato per un tag specifico. In questo caso, aggiungi altre immagini che contengono il tag in questione ed esegui il flusso di lavoro di formazione per completare il training del servizio per quel tag.

   Se non trovi i tuoi tag in questo rapporto, esegui nuovamente il flusso di lavoro di formazione per questi tag.

1. Per scaricare il report, selezionarlo dall&#39;elenco e fare clic su **[!UICONTROL Scarica]** nella barra degli strumenti. Il rapporto viene scaricato come foglio di calcolo di Microsoft Excel.

## Limitazioni {#limitations}

* I tag avanzati migliorati si basano su modelli di apprendimento delle immagini e dei relativi tag. Questi modelli non sono sempre perfetti per identificare i tag. La versione corrente del Servizio di contenuti avanzati presenta le seguenti limitazioni:

   * Incapacità di riconoscere le sottili differenze nelle immagini. Ad esempio, magliette e magliette normali.
   * Impossibilità di identificare i tag in base a modelli/parti minuscole di un’immagine. Ad esempio, i logo sulle magliette.
   * L&#39;assegnazione tag è supportata nelle impostazioni internazionali in cui è supportato [!DNL Experience Manager].

* Per cercare le risorse con tag avanzati (regolari o migliorati), utilizza l&#39;Omnisearch [!DNL Assets] (ricerca full-text). Non esiste un predicato di ricerca separato per i tag avanzati.

>[!MORELIKETHIS]
>
>* [Panoramica e formazione dei tag avanzati](enhanced-smart-tags.md)
>* [Risoluzione dei problemi relativi agli smart tag per le credenziali OAuth](config-oauth.md)
>* [Esercitazione video sugli smart tag](https://experienceleague.adobe.com/it/docs/experience-manager-learn/assets/metadata/image-smart-tags)
