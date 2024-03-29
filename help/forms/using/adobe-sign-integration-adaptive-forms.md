---
title: Integrare Adobe Sign con AEM Forms
description: Scopri come configurare Adobe Sign per il Forms adattivo AEM. Adobe Sign migliora il flusso di lavoro e l’elaborazione dei documenti per questioni legali, vendite, retribuzioni, gestione delle risorse umane e molte altre aree.
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms, Foundation Components, Acrobat Sign
exl-id: 52146038-1582-41b8-aee0-215d04bb91d7
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2071'
ht-degree: 1%

---

# Integrare [!DNL Adobe Sign] con AEM [!DNL Forms]{#integrate-adobe-sign-with-aem-forms}

<span class="preview"> L’Adobe consiglia di utilizzare l’acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/adobe-sign-integration-adaptive-forms.html?lang=en#adobe-acrobat-sign-for-government) |
| AEM 6.5 | Questo articolo |

[!DNL Adobe Sign] abilita i flussi di lavoro di firma elettronica per i moduli adattivi. Le firme elettroniche consentono di migliorare i flussi di lavoro per l&#39;elaborazione di documenti relativi a questioni legali, vendite, retribuzioni, gestione delle risorse umane e molte altre aree.

In un tipico [!DNL Adobe Acrobat Sign] e nello scenario Forms adattivo, un utente compila un modulo adattivo da applicare a un servizio. Ad esempio, la richiesta di una carta di credito e il modulo relativo ai benefit per i cittadini. Quando un utente compila, invia e firma il modulo di richiesta, questo viene inviato al fornitore di servizi per ulteriori azioni. Il provider di servizi esamina l&#39;applicazione e utilizza [!DNL Adobe Acrobat Sign] per contrassegnare la domanda approvata. AEM Forms supporta sia Adobe Acrobat Sign che Adobe Acrobat Sign Solutions for Government. A seconda della licenza e dei requisiti, puoi integrare o collegare AEM Forms con una delle seguenti soluzioni:

* [Collegare AEM Forms a Adobe Acrobat Sign](#adobe-sign)
* [Collegare AEM Forms ad Adobe Acrobat Sign Solutions for Government](#adobe-acrobat-sign-for-government)

## Collegare AEM Forms a Adobe Acrobat Sign {#adobe-sign}

Per connettersi **[!DNL AEM Forms]** con **[!DNL Adobe Acrobat Sign]**, configura il software e gli account elencati nella sezione prerequisiti e connetti Adobe Sign a tutte le istanze AEM Forms Author e Publish:

## Prerequisiti {#prerequisites}

Per integrare è necessario quanto segue [!DNL Adobe Sign] con AEM [!DNL Forms]:

* Un elemento attivo [Account sviluppatore Adobe Sign.](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* Un [SSL abilitato](/help/sites-administering/ssl-by-default.md) AEM [!DNL Forms] server.
* Un [Applicazione API Adobe Sign](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* Credenziali (ID client e segreto client) di [!DNL Adobe Sign] applicazione API.
* Durante la riconfigurazione, rimuovi il [!DNL Adobe Sign] configurazione sia dalle istanze di authoring che da quelle di pubblicazione.
* Utilizzare [chiave di crittografia identica](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) per le istanze di authoring e pubblicazione.

## Configura [!DNL Adobe Sign] con AEM [!DNL Forms] {#configure-adobe-sign-with-aem-forms}

Dopo aver impostato i prerequisiti, effettua le seguenti operazioni per configurare [!DNL Adobe Sign] con AEM [!DNL Forms] sull’istanza Autore:

1. Sull’AEM [!DNL Forms] istanza di authoring, passa a **Strumenti** ![martello](assets/hammer.png) > **[!UICONTROL Generale]** > **[!UICONTROL Browser configurazioni]**.
1. Il giorno **[!UICONTROL Browser configurazioni]** pagina, seleziona **[!UICONTROL Crea]**.
   * Consulta la [Browser configurazioni](/help/sites-administering/configurations.md) per ulteriori informazioni.
1. In **[!UICONTROL Crea configurazione]** , specifica un **[!UICONTROL Titolo]** per la configurazione, abilita **[!UICONTROL Configurazioni cloud]**, e seleziona **[!UICONTROL Crea]**. Crea un contenitore di configurazione.
1. Accedi a **Strumenti** ![martello](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Sign]** e seleziona il contenitore di configurazione creato nel passaggio precedente.

   >[!NOTE]
   >
   >Puoi eseguire i passaggi 1-4 per creare un contenitore di configurazione e un [!DNL Adobe Sign] nel contenitore o utilizza il file esistente `global` cartella in **Strumenti** ![martello](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Sign]**. Se crei la configurazione nel nuovo contenitore di configurazione, assicurati di specificare il nome del contenitore nel **[!UICONTROL Contenitore configurazione]** quando crei un modulo adattivo.

   >[!NOTE]
   >
   Assicurati che l’URL della pagina di configurazione dei Cloud Service inizi con **HTTPS**. In caso contrario, [abilita SSL](/help/sites-administering/ssl-by-default.md) per AEM [!DNL Forms] server.


1. Nella pagina di configurazione, tocca **[!UICONTROL Crea]** per creare [!DNL Adobe Sign] configurazione in AEM [!DNL Forms].
1. In **[!UICONTROL Generale]** scheda di **[!UICONTROL Crea configurazione Adobe Sign]** , specificare un **[!UICONTROL Nome]** per la configurazione e tocca **[!UICONTROL Successivo]**. Facoltativamente, puoi specificare un titolo e cercare la miniatura da configurare.
1. Ora puoi **[!UICONTROL Seleziona soluzione]** per selezionare [!DNL Adobe Acrobat Sign].

   ![Adobe Acrobat Sign Solutions](/help/forms/using/assets/adobe-sign-solution.png)

1. Copiare l&#39;URL nella finestra del browser corrente in un blocco note e rimuovere la parte /`ui#/aem` dall’URL. L’URL modificato è quindi necessario per configurare [!DNL Adobe Acrobat Sign] applicazione con [!DNL AEM Forms], in un passaggio successivo. Tocca [!UICONTROL Successivo].

1. In **[!UICONTROL Impostazioni]** scheda,
   * il **[!UICONTROL URL OAuth]** contiene l’URL predefinito che include la partizione di database Adobe Sign. Il formato dell’URL è:

     `https://<shard>/public/oauth/v2`

     Ad esempio:
     `https://secure.na1.echosign.com/public/oauth/v2`

   * il **[!UICONTROL URL token di accesso]** contiene l’URL predefinito che include la partizione di database Adobe Sign. Il formato dell’URL è:

     `https://<shard>/oauth/v2/token`

     Ad esempio:
     `https://api.na1.echosign.com/oauth/v2/token`

   Dove:

   **na1** fa riferimento alla partizione di database predefinita. È possibile modificare il valore della partizione del database. Assicurati che [!DNL  Adobe Acrobat Sign] Le configurazioni cloud puntano al [partitura corretta](https://helpx.adobe.com/sign/using/identify-account-shard.html).

   >[!NOTE]
   >
   * Mantieni **Crea configurazione Adobe Acrobat Sign** pagina aperta. Non chiuderlo. Puoi recuperare **ID client** e **Segreto client** dopo aver configurato le impostazioni OAuth per [!DNL Adobe Acrobat Sign] come descritto nei passaggi successivi.
   * Dopo aver effettuato l’accesso al tuo account Adobe Sign, passa a **[!UICONTROL API ACROBAT SIGN]** > **[!UICONTROL Informazioni API]** > **[!UICONTROL Documentazione sui metodi API REST]** > **[!UICONTROL Token di accesso OAuth]** per accedere alle informazioni relative all’URL di Adobe Sign OAuth e all’URL del token di accesso.

1. Configurare le impostazioni OAuth per [!DNL Adobe Sign] applicazione:

   1. Apri una finestra del browser e accedi al [!DNL Adobe Sign] account sviluppatore.
   1. Seleziona l’applicazione configurata per AEM [!DNL Forms], e seleziona **[!UICONTROL Configurare OAuth per l’applicazione]**.
   1. Copia il **[!UICONTROL ID client]** e **[!UICONTROL Segreto client]** in un blocco note.
   1. In **[!UICONTROL URL di reindirizzamento]** , aggiungi l’URL HTTPS copiato nel passaggio precedente.
   1. Abilita le seguenti impostazioni OAuth per [!DNL Adobe Sign] e fare clic su **[!UICONTROL Salva]**.

   * agreement_read
   * agreement_write
   * agreement_send
   * widget_write
   * workflow_read

   Per informazioni dettagliate su come configurare le impostazioni OAuth per un [!DNL Adobe Sign] e ottenere le chiavi, consulta [Configurare le impostazioni OAuth per l&#39;applicazione](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md) documentazione per gli sviluppatori.

   ![Configurazione OAuth](assets/oauthconfig_new.png)

<!--
1. Go back to the **[!UICONTROL Create Adobe Sign Configuration]** page. In the **[!UICONTROL Settings]** tab, the **[!UICONTROL OAuth URL]** field mentions the  default URL. The format of the URL is:

   `https://<shard>/public/oAuth/v2`

   For example: 
   `https://secure.na1.echosign.com/public/oauth/v2`

   where:

   **na1** refers to the default database shard.

   You can modify the value for the database shard. Restart the server to be able to use the new value for the database shard.

   >[!NOTE]
   >
   >Ensure that your author and publish instance configurations point to the same shard. If you create multiple Adobe Sign configurations for an organization, ensure all the configurations utilize the same shard. -->

1. Torna a **[!UICONTROL Crea configurazione Adobe Sign]** pagina. In **[!UICONTROL Impostazioni]** , specificare **ID client** (indicato anche come ID applicazione) e **Segreto client**. Utilizza il [ID client e segreto client dell’applicazione Adobe Sign](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) creato per AEM Forms.

1. Seleziona la **[!UICONTROL Abilita Adobe Sign anche per gli allegati]** opzione per aggiungere i file allegati a un modulo adattivo al [!DNL Adobe Sign] documento inviato per la firma.

1. Seleziona **[!UICONTROL Connettersi ad Adobe Sign]**. Quando vengono richieste le credenziali, specifica il nome utente e la password dell’account utilizzato durante la creazione [!DNL Adobe Sign] applicazione.

   ![Configurazione cloud Adobe Acrobat Sign completata](assets/adobe-sign-cloud-configuration-success.png)

1. Tocca **[!UICONTROL Crea]** per creare [!DNL Adobe Sign] configurazione.
1. Apri la console web AEM. L’URL è `https://'[server]:[port]'/system/console/configMgr`
1. Apri **[!UICONTROL Servizio di configurazione comune di Forms].**
1. In **[!UICONTROL Consenti]** campo, **seleziona** Tutti gli utenti: tutti gli utenti, anonimi o connessi, possono visualizzare in anteprima gli allegati, verificare e firmare i moduli e fare clic su **[!UICONTROL Salva].** L’istanza di authoring è configurata per utilizzare [!DNL Adobe Sign].
1. Pubblica la configurazione.
1. Utilizzare [replica](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html) per creare una configurazione identica sulle istanze di pubblicazione corrispondenti.

Ora, [!DNL Adobe Sign] è integrato con l’AEM [!DNL Forms] e pronti per essere utilizzati nei moduli adattivi. A [utilizzare il servizio Adobe Sign in un modulo adattivo](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form), specifica il contenitore di configurazione creato in precedenza nelle proprietà dei moduli adattivi.

>[!NOTE]
>
Per configurare la sandbox di Adobe Sign, puoi seguire gli stessi passaggi di configurazione descritti in [Adobe Sign](#adobe-sign).

## Collegare AEM Forms ad Adobe Acrobat Sign Solutions for Government {#adobe-acrobat-sign-for-government}

La connessione di AEM Forms ad Adobe Acrobat Sign Solutions for Government è un processo in più fasi. Comporta:

* Creazione di un URL di reindirizzamento per le istanze AEM
* Condivisione dell’URL di reindirizzamento e degli ambiti con il team Adobe Sign Solutions for Government
* Ricezione delle credenziali dal team di Adobe Sign
* Utilizzo delle credenziali ricevute per collegare AEM Forms ad Adobe Acrobat Sign Solutions for Government

![adobe-acrobat-sign-govt-workflow](/help/forms/using/assets/adobe-acrobat-sign-govt-workflow.png)

### Prima di iniziare {#prerequisites-for-adobe-sign-for-acrobat-sign-for-government}

Prima di iniziare a collegare AEM Forms alla soluzione Adobe Acrobat Sign,

* Assicurati che il tuo [Adobe Acrobat Sign Solutions for Government](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#account-provisioning) è stato eseguito il provisioning dell’account.
* Il tuo AEM [!DNL Forms] i server sono [SSL abilitato](/help/sites-administering/ssl-by-default.md) .
* Il tuo AEM [!DNL Forms] i server utilizzano [chiave di crittografia identica](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) per le istanze di authoring e pubblicazione.

### Connettere AEM Forms ad Adobe Acrobat Sign Solutions for Government {#connect-adobe-acrobat-sign-for-government}

#### Creare un URL di reindirizzamento per l’istanza AEM

1. Nell’istanza di AEM Forms, passa a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Generale]** > **[!UICONTROL Browser configurazioni]**.
1. Il giorno **[!UICONTROL Browser configurazioni]** pagina, seleziona **[!UICONTROL Crea]**.
1. In **[!UICONTROL Crea configurazione]** , specifica un **[!UICONTROL Titolo]** per la configurazione, abilita **[!UICONTROL Configurazioni cloud]**, e seleziona **[!UICONTROL Crea]**. Crea un contenitore di configurazione. Assicurati che il nome del contenitore/cartella non contenga spazio.

1. Accedi a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Acrobat Sign]** e apri il contenitore di configurazione creato nel passaggio precedente. Quando crei un modulo adattivo, specifica il nome del contenitore in **[!UICONTROL Contenitore configurazione]** campo.
1. Nella pagina di configurazione, seleziona **[!UICONTROL Crea]** per creare [!DNL Adobe Acrobat Sign] in AEM Forms.
1. Copia l’URL della finestra del browser corrente in un blocco note dall’URL. Questo URL è denominato `re-direct URL`. Nella sezione successiva, condividi `re-direct URL` e `Scopes` con il team di Adobe Sign e le credenziali di richiesta (ID client e Segreto client).

>[!NOTE]
>
>
* A `re-direct URL` deve contenere [Livello superiore](https://en.wikipedia.org/wiki/Top-level_domain) dominio. Ad esempio `https://adobe.com/libs/adobesign/cloudservices/adobesign/createcloudconfigwizard/cloudservices.html/conf/global`
* Non utilizzare un URL locale come `re-direct URL`. Esempio: `https://localhost:4502/libs/adobesign/cloudservices/adobesign/createcloudconfigwizard/cloudservices.html/conf/global`.


#### Condividi l’URL di reindirizzamento e gli ambiti con il team di Adobe Sign e ricevi le credenziali

Il team Adobe Acrobat Sign for Government Solutions richiede `re-direct URL` e determinati ambiti da abilitare per l’applicazione Adobe Acrobat Sign (elencati di seguito) per la generazione di credenziali (ID client e segreto client) che consentono di collegare AEM Forms ad Adobe Acrobat Sign Solutions per la pubblica amministrazione.

Condividi `scopes` (elencati di seguito) e `re-direct URL` creato e annotato l&#39;ultimo passaggio della sezione precedente con il rappresentante Adobe Acrobat Sign for Government Solution [membro del team Adobe Professional Services](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#password).

**_Ambiti_**

* [!DNL agreement_read]
* [!DNL agreement_write]
* [!DNL agreement_send]
* [!DNL widget_read]
* [!DNL widget_write]
* [!DNL workflow_read]
* [!DNL offline_access]

Il rappresentante genera e condivide le credenziali con te. Nella sezione successiva utilizzi le credenziali (ID client e Segreto client) per collegare AEM Forms ad Adobe Acrobat Sign Solutions for Government.

#### Utilizza le credenziali ricevute per collegare AEM Forms ad Adobe Acrobat Sign Solutions for Government

1. Apri `re-direct URL` nel browser. Hai creato e annotato il `re-direct URL` nell&#39;ultimo passaggio della [creare un URL di reindirizzamento nell’istanza AEM](#create-redirect-url) sezione.

1. In **[!UICONTROL Generale]** scheda di **[!UICONTROL Crea configurazione Adobe Sign]** , specificare un **[!UICONTROL Nome]** per la configurazione, quindi seleziona **[!UICONTROL Successivo]**. Facoltativamente, puoi specificare un valore **[!UICONTROL Titolo]** e sfoglia per selezionare un **[!UICONTROL Miniatura]** per la configurazione. Fai clic su **[!UICONTROL Avanti]**.

1. In **[!UICONTROL Impostazioni]** scheda di **[!UICONTROL Crea configurazione Adobe Sign]** pagina, per **[!UICONTROL Seleziona soluzione]** , seleziona [!DNL Adobe Acrobat Sign Solutions for Government].

   ![Adobe Acrobat Sign Solutions for Government](/help/forms/using/assets/adobe-sign-for-govt.png)

1. In **[!UICONTROL E-mail]** , specifica l’indirizzo e-mail associato al tuo account Adobe Acrobat Sign Solutions for Government.

1. In **[!UICONTROL Impostazioni]** scheda,
   * il **[!UICONTROL URL OAuth]** contiene l’URL predefinito che include la partizione di database Adobe Sign. Il formato dell’URL è:

     `https://<shard>/api/gateway/adobesignauthservice/api/v1/authorize`

     Ad esempio:
     `https://secure.na1.adobesign.us/api/gateway/adobesignauthservice/api/v1/authorize`

   * il **[!UICONTROL URL token di accesso]** contiene l’URL predefinito che include la partizione di database Adobe Sign. Il formato dell’URL è:

     `https://<shard>/api/gateway/adobesignauthservice/api/v1/token`

     Ad esempio:
     `https://secure.na1.adobesign.us/api/gateway/adobesignauthservice/api/v1/token`

   Dove:

   **na1** fa riferimento alla partizione di database predefinita. È possibile modificare il valore della partizione del database. Assicurati che [!DNL  Adobe Acrobat Sign] Le configurazioni cloud puntano al [partitura corretta](https://helpx.adobe.com/sign/using/identify-account-shard.html).

   >[!NOTE]
   >
   * Dopo aver effettuato l’accesso al tuo account Adobe Sign, passa a **[!UICONTROL API ACROBAT SIGN]** > **[!UICONTROL Informazioni API]** > **[!UICONTROL Documentazione sui metodi API REST]** > **[!UICONTROL Token di accesso OAuth]** per accedere alle informazioni relative all’URL Adobe Sign OAuth e all’URL del token di accesso.

1. Utilizza le credenziali condivise da Adobe Acrobat Sign per il rappresentante della soluzione governativa ([membro del team Adobe Professional Services]) nella sezione precedente come [**[!UICONTROL ID client]** e **[!UICONTROL Segreto client]**].

1. Seleziona la **[!UICONTROL Abilita Adobe Acrobat Sign per allegati]** opzione per aggiungere i file allegati a un modulo adattivo al [!DNL Adobe Acrobat Sign] documento inviato per la firma.

1. Seleziona **[!UICONTROL Connettersi ad Adobe Sign]**. Quando vengono richieste le credenziali, specifica il nome utente e la password dell’account utilizzato durante la creazione [!DNL Adobe Acrobat Sign] applicazione. Quando ti viene richiesto di confermare l’accesso per `Adobe Acrobat Sign for Government Solutions` e , fai clic su **[!UICONTROL Consenti accesso]**. Se le credenziali sono corrette e si consente [!DNL AEM Forms] per accedere al [!DNL Adobe Acrobat Sign] per gli sviluppatori, viene visualizzato un messaggio di successo simile al seguente.

   ![Configurazione cloud Adobe Acrobat Sign completata](/help/forms/using/assets/adobe-sign-cloud-configuration-success.png)

   Quando vengono richieste le credenziali, specifica il nome utente e la password dell’account utilizzato durante la creazione [!DNL Adobe Acrobat Sign] applicazione. Quando ti viene richiesto di confermare l’accesso per `your account`e fai clic su **[!UICONTROL Consenti accesso]**.

1. Seleziona **[!UICONTROL Crea]** per creare la configurazione.
1. Apri la console web AEM. L’URL è `https://'[server]:[port]'/system/console/configMgr`
1. Apri **[!UICONTROL Servizio di configurazione comune di Forms].**
1. In **[!UICONTROL Consenti]** campo, **seleziona** Tutti gli utenti: tutti gli utenti, anonimi o connessi, possono visualizzare in anteprima gli allegati, verificare e firmare i moduli e fare clic su **[!UICONTROL Salva].** L’istanza di authoring è configurata per utilizzare [!DNL Adobe Sign].

1. Pubblica la configurazione.
1. Utilizzare [replica](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html) per creare una configurazione identica sulle istanze di pubblicazione corrispondenti.

Ora puoi [utilizzare aggiungere campi Adobe Acrobat Sign in un modulo adattivo](working-with-adobe-sign.md) o [Flusso di lavoro AEM](/help/forms/using/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step). Accertati di aggiungere il contenitore di configurazione utilizzato per la configurazione del Cloud Service a tutto il Forms adattivo abilitato per [!DNL Adobe Acrobat Sign]. È possibile specificare un contenitore di configurazione dalle proprietà di un modulo adattivo.


## Configura [!DNL Adobe Sign] per sincronizzare lo stato della firma {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Un [!DNL Adobe Sign] il modulo adattivo abilitato viene inviato solo dopo che tutti i firmatari hanno completato il processo di firma. Per impostazione predefinita, il [!DNL Adobe Sign] È pianificato che i servizi di pianificazione controllino la risposta del firmatario (polling) ogni 24 ore. È possibile modificare l’intervallo predefinito per l’ambiente. Per modificare l’intervallo predefinito, effettua le seguenti operazioni:

1. Accedere a AEM [!DNL Forms] server con credenziali di amministratore e passa a **Strumenti** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console web]**.

   Puoi anche aprire il seguente URL in una finestra del browser:
   `https://[localhost]:'port'/system/console/configMgr`

1. Individuare e aprire **[!UICONTROL Servizio di configurazione Adobe Sign]** opzione. Specifica un [espressione cron](https://en.wikipedia.org/wiki/Cron#CRON_expression) nel **[!UICONTROL Espressione modulo di pianificazione aggiornamento stato]** e fai clic su **[!UICONTROL Salva]**. Ad esempio, per eseguire il servizio di configurazione ogni giorno alle 00:00, specifica `0 0 0 1/1 * ? *` nel **[!UICONTROL Espressione modulo di pianificazione aggiornamento stato]** campo.

Intervallo predefinito per lo stato di sincronizzazione di [!DNL Adobe Sign] è stato modificato.

## Articoli correlati {#related-articles}

* [Utilizzo di Adobe Sign in un modulo adattivo](../../forms/using/working-with-adobe-sign.md)
* [Adobe Sign con flussi di lavoro incentrati su moduli](/help/forms/using/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)
* [Utilizzo di Adobe Sign con AEM Forms (video)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
