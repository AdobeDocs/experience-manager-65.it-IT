---
title: Integrare Adobe Sign con AEM Forms
description: Scopri come configurare Adobe Sign per il Forms adattivo AEM. Adobe Sign migliora il flusso di lavoro e l’elaborazione dei documenti per questioni legali, vendite, retribuzioni, gestione delle risorse umane e molte altre aree.
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms,Foundation Components,Acrobat Sign
exl-id: 52146038-1582-41b8-aee0-215d04bb91d7
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2071'
ht-degree: 1%

---

# Integrare [!DNL Adobe Sign] con AEM [!DNL Forms]{#integrate-adobe-sign-with-aem-forms}

<span class="preview"> Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/adobe-sign-integration-adaptive-forms.html?lang=it#adobe-acrobat-sign-for-government) |
| AEM 6.5 | Questo articolo |

[!DNL Adobe Sign] abilita i flussi di lavoro di firma elettronica per i moduli adattivi. Le firme elettroniche consentono di migliorare i flussi di lavoro per l&#39;elaborazione di documenti relativi a questioni legali, vendite, retribuzioni, gestione delle risorse umane e molte altre aree.

In uno scenario tipico di [!DNL Adobe Acrobat Sign] e Forms adattivo, un utente compila un modulo adattivo da applicare a un servizio. Ad esempio, la richiesta di una carta di credito e il modulo relativo ai benefit per i cittadini. Quando un utente compila, invia e firma il modulo di richiesta, questo viene inviato al fornitore di servizi per ulteriori azioni. Il provider di servizi esamina l&#39;applicazione e utilizza [!DNL Adobe Acrobat Sign] per contrassegnarla come approvata. AEM Forms supporta sia Adobe Acrobat Sign che Adobe Acrobat Sign Solutions for Government. A seconda della licenza e dei requisiti, puoi integrare o collegare AEM Forms con una delle seguenti soluzioni:

* [Collegare AEM Forms a Adobe Acrobat Sign](#adobe-sign)
* [Collegare AEM Forms ad Adobe Acrobat Sign Solutions for Government](#adobe-acrobat-sign-for-government)

## Collegare AEM Forms a Adobe Acrobat Sign {#adobe-sign}

Per connettere **[!DNL AEM Forms]** a **[!DNL Adobe Acrobat Sign]**, configura il software e gli account elencati nella sezione dei prerequisiti e connetti Adobe Sign a tutte le istanze di AEM Forms Author e Publish:

## Prerequisiti {#prerequisites}

Per integrare [!DNL Adobe Sign] con AEM [!DNL Forms] è necessario quanto segue:

* Un account sviluppatore [Adobe Sign attivo.](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* Un server [SSL abilitato](/help/sites-administering/ssl-by-default.md) AEM [!DNL Forms].
* Applicazione API [Adobe Sign](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* Credenziali (ID client e segreto client) dell&#39;applicazione API [!DNL Adobe Sign].
* Durante la riconfigurazione, rimuovere la configurazione [!DNL Adobe Sign] esistente sia dall&#39;istanza di authoring che da quella di pubblicazione.
* Utilizza [chiave di crittografia identica](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) per le istanze di authoring e pubblicazione.

## Configura [!DNL Adobe Sign] con AEM [!DNL Forms] {#configure-adobe-sign-with-aem-forms}

Dopo aver impostato i prerequisiti, eseguire la procedura seguente per configurare [!DNL Adobe Sign] con AEM [!DNL Forms] nell&#39;istanza di authoring:

1. Nell&#39;istanza dell&#39;autore [!DNL Forms] dell&#39;AEM, passare a **Strumenti** ![martello](assets/hammer.png) > **[!UICONTROL Generale]** > **[!UICONTROL Browser configurazioni]**.
1. Nella pagina **[!UICONTROL Browser configurazioni]**, selezionare **[!UICONTROL Crea]**.
   * Per ulteriori informazioni, vedere la documentazione del [browser di configurazione](/help/sites-administering/configurations.md).
1. Nella finestra di dialogo **[!UICONTROL Crea configurazione]**, specifica un **[!UICONTROL Titolo]** per la configurazione, abilita **[!UICONTROL Configurazioni cloud]** e seleziona **[!UICONTROL Crea]**. Crea un contenitore di configurazione.
1. Passa a **Strumenti** ![martello](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Sign]** e seleziona il contenitore di configurazione creato nel passaggio precedente.

   >[!NOTE]
   >
   >È possibile eseguire i passaggi da 1 a 4 per creare un contenitore di configurazione e creare una configurazione [!DNL Adobe Sign] nel contenitore oppure utilizzare la cartella `global` esistente in **Strumenti** ![martello](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Sign]**. Se crei la configurazione nel nuovo contenitore di configurazione, assicurati di specificare il nome del contenitore nel campo **[!UICONTROL Contenitore configurazione]** al momento della creazione di un modulo adattivo.

   >[!NOTE]
   >
   >Verificare che l&#39;URL della pagina Configurazione Cloud Service inizi con **HTTPS**. In caso contrario, [abilita SSL](/help/sites-administering/ssl-by-default.md) per il server AEM [!DNL Forms].


1. Nella pagina di configurazione, toccare **[!UICONTROL Crea]** per creare la configurazione [!DNL Adobe Sign] nell&#39;AEM [!DNL Forms].
1. Nella scheda **[!UICONTROL Generale]** della pagina **[!UICONTROL Crea configurazione Adobe Sign]**, specifica **[!UICONTROL Nome]** per la configurazione e tocca **[!UICONTROL Avanti]**. Facoltativamente, puoi specificare un titolo e cercare la miniatura da configurare.
1. Ora puoi **[!UICONTROL Selezionare la soluzione]** per selezionare [!DNL Adobe Acrobat Sign].

   ![Adobe Acrobat Sign Solutions](/help/forms/using/assets/adobe-sign-solution.png)

1. Copiare l&#39;URL nella finestra del browser corrente in un blocco note e rimuovere la parte /`ui#/aem` dall&#39;URL. L&#39;URL modificato è quindi necessario per configurare l&#39;applicazione [!DNL Adobe Acrobat Sign] con [!DNL AEM Forms], in un passaggio successivo. Tocca [!UICONTROL Avanti].

1. Nella scheda **[!UICONTROL Impostazioni]**,
   * il campo **[!UICONTROL URL OAuth]** contiene l&#39;URL predefinito che include la partizione del database di Adobe Sign. Il formato dell’URL è:

     `https://<shard>/public/oauth/v2`

     Ad esempio:
     `https://secure.na1.echosign.com/public/oauth/v2`

   * il campo **[!UICONTROL URL token di accesso]** contiene l&#39;URL predefinito che include la partizione del database di Adobe Sign. Il formato dell’URL è:

     `https://<shard>/oauth/v2/token`

     Ad esempio:
     `https://api.na1.echosign.com/oauth/v2/token`

   Dove:

   **na1** fa riferimento alla partizione di database predefinita. È possibile modificare il valore della partizione del database. Verificare che le [!DNL &#x200B; Adobe Acrobat Sign] configurazioni cloud puntino alla [partizione corretta](https://helpx.adobe.com/it/sign/using/identify-account-shard.html).

   >[!NOTE]
   >
   >* Mantieni aperta la pagina **Crea configurazione Adobe Acrobat Sign**. Non chiuderlo. È possibile recuperare **ID client** e **Segreto client** dopo aver configurato le impostazioni OAuth per l&#39;applicazione [!DNL Adobe Acrobat Sign] come descritto nei passaggi successivi.
   >* Dopo aver effettuato l&#39;accesso all&#39;account Adobe Sign, passa a **[!UICONTROL API Acrobat Sign]** > **[!UICONTROL Informazioni API]** > **[!UICONTROL Documentazione dei metodi REST API]** > **[!UICONTROL Token di accesso OAuth]** per accedere alle informazioni relative all&#39;URL OAuth di Adobe Sign e all&#39;URL del token di accesso.

1. Configurare le impostazioni OAuth per l&#39;applicazione [!DNL Adobe Sign]:

   1. Apri una finestra del browser e accedi all&#39;account sviluppatore [!DNL Adobe Sign].
   1. Selezionare l&#39;applicazione configurata per l&#39;AEM [!DNL Forms] e selezionare **[!UICONTROL Configura OAuth per l&#39;applicazione]**.
   1. Copia l&#39;**[!UICONTROL ID client]** e il **[!UICONTROL Segreto client]** in un blocco note.
   1. Nella casella **[!UICONTROL URL di reindirizzamento]**, aggiungi l&#39;URL HTTPS copiato nel passaggio precedente.
   1. Abilitare le seguenti impostazioni OAuth per l&#39;applicazione [!DNL Adobe Sign] e fare clic su **[!UICONTROL Salva]**.

   * agreement_read
   * agreement_write
   * agreement_send
   * widget_write
   * workflow_read

   Per informazioni dettagliate su come configurare le impostazioni OAuth per un&#39;applicazione [!DNL Adobe Sign] e ottenere le chiavi, vedere [Configurare le impostazioni OAuth per la documentazione per gli sviluppatori dell&#39;applicazione](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md).

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

1. Torna alla pagina **[!UICONTROL Crea configurazione Adobe Sign]**. Nella scheda **[!UICONTROL Impostazioni]**, specifica l&#39;**ID client** (noto anche come ID applicazione) e il **Segreto client**. Utilizza l&#39;[ID client e segreto client dell&#39;applicazione Adobe Sign](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) creata per AEM Forms.

1. Seleziona l&#39;opzione **[!UICONTROL Abilita Adobe Sign per gli allegati anche]** per aggiungere i file allegati a un modulo adattivo al documento [!DNL Adobe Sign] corrispondente inviato per la firma.

1. Seleziona **[!UICONTROL Connetti ad Adobe Sign]**. Quando vengono richieste le credenziali, specificare il nome utente e la password dell&#39;account utilizzato durante la creazione dell&#39;applicazione [!DNL Adobe Sign].

   ![Configurazione cloud Adobe Acrobat Sign completata](assets/adobe-sign-cloud-configuration-success.png)

1. Tocca **[!UICONTROL Crea]** per creare la configurazione di [!DNL Adobe Sign].
1. Apri la console web AEM. URL: `https://'[server]:[port]'/system/console/configMgr`
1. Apri **[!UICONTROL Servizio di configurazione comune di Forms].**
1. Nel campo **[!UICONTROL Consenti]**, **seleziona** Tutti gli utenti - Tutti gli utenti, anonimi o connessi, possono visualizzare in anteprima gli allegati, verificare e firmare i moduli e fare clic su **[!UICONTROL Salva].L&#39;istanza Autore** è configurata per l&#39;utilizzo di [!DNL Adobe Sign].
1. Publish la configurazione.
1. Utilizza [replica](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html?lang=it) per creare una configurazione identica nelle istanze di pubblicazione corrispondenti.

Ora [!DNL Adobe Sign] è integrato con AEM [!DNL Forms] ed è pronto per essere utilizzato nei moduli adattivi. Per [utilizzare il servizio Adobe Sign in un modulo adattivo](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form), specifica il contenitore di configurazione creato in precedenza nelle proprietà del modulo adattivo.

>[!NOTE]
>
>Per configurare la sandbox di Adobe Sign, puoi seguire gli stessi passaggi di configurazione descritti in [Adobe Sign](#adobe-sign).

## Collegare AEM Forms ad Adobe Acrobat Sign Solutions for Government {#adobe-acrobat-sign-for-government}

La connessione di AEM Forms ad Adobe Acrobat Sign Solutions for Government è un processo in più fasi. Comporta:

* Creazione di un URL di reindirizzamento per le istanze AEM
* Condivisione dell’URL di reindirizzamento e degli ambiti con il team Adobe Sign Solutions for Government
* Ricezione delle credenziali dal team di Adobe Sign
* Utilizzo delle credenziali ricevute per collegare AEM Forms ad Adobe Acrobat Sign Solutions for Government

![adobe-acrobat-sign-govt-workflow](/help/forms/using/assets/adobe-acrobat-sign-govt-workflow.png)

### Prima di iniziare {#prerequisites-for-adobe-sign-for-acrobat-sign-for-government}

Prima di iniziare a collegare AEM Forms alla soluzione Adobe Acrobat Sign,

* Assicurati che sia stato eseguito il provisioning del tuo account [Adobe Acrobat Sign Solutions for Government](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#account-provisioning).
* I server AEM [!DNL Forms] sono [SSL abilitati](/help/sites-administering/ssl-by-default.md) .
* I server [!DNL Forms] dell&#39;AEM utilizzano [una chiave di crittografia identica](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) per le istanze di authoring e pubblicazione.

### Connettere AEM Forms ad Adobe Acrobat Sign Solutions for Government {#connect-adobe-acrobat-sign-for-government}

#### Creare un URL di reindirizzamento per l’istanza AEM

1. Nell&#39;istanza di AEM Forms, passa a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Generale]** > **[!UICONTROL Browser configurazioni]**.
1. Nella pagina **[!UICONTROL Browser configurazioni]**, selezionare **[!UICONTROL Crea]**.
1. Nella finestra di dialogo **[!UICONTROL Crea configurazione]**, specifica un **[!UICONTROL Titolo]** per la configurazione, abilita **[!UICONTROL Configurazioni cloud]** e seleziona **[!UICONTROL Crea]**. Crea un contenitore di configurazione. Assicurati che il nome del contenitore/cartella non contenga spazio.

1. Passa a **[!UICONTROL Strumenti]** ![martello](assets/hammer.png) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Acrobat Sign]** e apri il contenitore di configurazione creato nel passaggio precedente. Quando crei un modulo adattivo, specifica il nome del contenitore nel campo **[!UICONTROL Contenitore configurazione]**.
1. Nella pagina di configurazione, seleziona **[!UICONTROL Crea]** per creare la configurazione [!DNL Adobe Acrobat Sign] in AEM Forms.
1. Copia l’URL della finestra del browser corrente in un blocco note dall’URL. Questo URL è denominato `re-direct URL`. Nella sezione successiva, condividi `re-direct URL` e `Scopes` con il team di Adobe Sign e richiedi le credenziali (ID client e Segreto client).

>[!NOTE]
>
>
>* Un dominio `re-direct URL` deve contenere un dominio [di primo livello](https://en.wikipedia.org/wiki/Top-level_domain). Ad esempio `https://adobe.com/libs/adobesign/cloudservices/adobesign/createcloudconfigwizard/cloudservices.html/conf/global`
>* Non utilizzare un URL locale come `re-direct URL`. Esempio: `https://localhost:4502/libs/adobesign/cloudservices/adobesign/createcloudconfigwizard/cloudservices.html/conf/global`.


#### Condividi l’URL di reindirizzamento e gli ambiti con il team di Adobe Sign e ricevi le credenziali

Il team Adobe Acrobat Sign for Government Solutions richiede che `re-direct URL` e gli ambiti specifici siano abilitati per l&#39;applicazione Adobe Acrobat Sign (elencata di seguito) per generare le credenziali (ID client e segreto client) che consentono di collegare AEM Forms ad Adobe Acrobat Sign Solutions for Government.

Condividi `scopes` (elencato di seguito) e `re-direct URL` creati e annotati nell&#39;ultimo passaggio della sezione precedente con il rappresentante di Adobe Acrobat Sign for Government Solution [membro del team Adobe Professional Services](https://opensource.adobe.com/acrobat-sign/signgov/gstarted.html#password).

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

1. Apri `re-direct URL` nel browser. Hai creato e annotato `re-direct URL` nell&#39;ultimo passaggio della sezione [Creare un URL di reindirizzamento nell&#39;istanza AEM](#create-redirect-url).

1. Nella scheda **[!UICONTROL Generale]** della pagina **[!UICONTROL Crea configurazione Adobe Sign]**, specifica un **[!UICONTROL Nome]** per la configurazione e seleziona **[!UICONTROL Avanti]**. Facoltativamente, puoi specificare un **[!UICONTROL Titolo]** e cercare di selezionare una **[!UICONTROL Miniatura]** per la configurazione. Fai clic su **[!UICONTROL Avanti]**.

1. Nella scheda **[!UICONTROL Impostazioni]** della pagina **[!UICONTROL Crea configurazione Adobe Sign]**, per l&#39;opzione **[!UICONTROL Seleziona soluzione]**, selezionare [!DNL Adobe Acrobat Sign Solutions for Government].

   ![Adobe Acrobat Sign Solutions per enti pubblici](/help/forms/using/assets/adobe-sign-for-govt.png)

1. Nel campo **[!UICONTROL E-mail]**, specifica l&#39;indirizzo e-mail associato al tuo account Adobe Acrobat Sign Solutions for Government.

1. Nella scheda **[!UICONTROL Impostazioni]**,
   * il campo **[!UICONTROL URL OAuth]** contiene l&#39;URL predefinito che include la partizione del database di Adobe Sign. Il formato dell’URL è:

     `https://<shard>/api/gateway/adobesignauthservice/api/v1/authorize`

     Ad esempio:
     `https://secure.na1.adobesign.us/api/gateway/adobesignauthservice/api/v1/authorize`

   * il campo **[!UICONTROL URL token di accesso]** contiene l&#39;URL predefinito che include la partizione del database di Adobe Sign. Il formato dell’URL è:

     `https://<shard>/api/gateway/adobesignauthservice/api/v1/token`

     Ad esempio:
     `https://secure.na1.adobesign.us/api/gateway/adobesignauthservice/api/v1/token`

   Dove:

   **na1** fa riferimento alla partizione di database predefinita. È possibile modificare il valore della partizione del database. Verificare che le [!DNL &#x200B; Adobe Acrobat Sign] configurazioni cloud puntino alla [partizione corretta](https://helpx.adobe.com/it/sign/using/identify-account-shard.html).

   >[!NOTE]
   >
   >* Dopo aver effettuato l&#39;accesso al tuo account Adobe Sign, passa a **[!UICONTROL API Acrobat Sign]** > **[!UICONTROL Informazioni API]** > **[!UICONTROL Documentazione dei metodi REST API]** > **[!UICONTROL Token di accesso OAuth]** per accedere alle informazioni relative all&#39;URL Adobe Sign oAuth e all&#39;URL del token di accesso.

1. Utilizza le credenziali condivise da Adobe Acrobat Sign per il rappresentante di soluzioni governative ([membro del team Adobe Professional Services]) nella sezione precedente come [**[!UICONTROL ID client]** e **[!UICONTROL Segreto client]**].

1. Selezionare l&#39;opzione **[!UICONTROL Abilita Adobe Acrobat Sign per gli allegati]** per aggiungere i file allegati a un modulo adattivo al documento [!DNL Adobe Acrobat Sign] corrispondente inviato per la firma.

1. Seleziona **[!UICONTROL Connetti ad Adobe Sign]**. Quando vengono richieste le credenziali, specificare il nome utente e la password dell&#39;account utilizzato durante la creazione dell&#39;applicazione [!DNL Adobe Acrobat Sign]. Quando viene richiesto di confermare l&#39;accesso per `Adobe Acrobat Sign for Government Solutions` e , fare clic su **[!UICONTROL Consenti accesso]**. Se le credenziali sono corrette e si consente a [!DNL AEM Forms] di accedere all&#39;account sviluppatore [!DNL Adobe Acrobat Sign], verrà visualizzato un messaggio di operazione riuscita simile al seguente.

   ![Configurazione cloud Adobe Acrobat Sign completata](/help/forms/using/assets/adobe-sign-cloud-configuration-success.png)

   Quando vengono richieste le credenziali, specificare il nome utente e la password dell&#39;account utilizzato durante la creazione dell&#39;applicazione [!DNL Adobe Acrobat Sign]. Quando viene richiesto di confermare l&#39;accesso per `your account` e fare clic su **[!UICONTROL Consenti accesso]**.

1. Seleziona **[!UICONTROL Crea]** per creare la configurazione.
1. Apri la console web AEM. URL: `https://'[server]:[port]'/system/console/configMgr`
1. Apri **[!UICONTROL Servizio di configurazione comune di Forms].**
1. Nel campo **[!UICONTROL Consenti]**, **seleziona** Tutti gli utenti - Tutti gli utenti, anonimi o connessi, possono visualizzare in anteprima gli allegati, verificare e firmare i moduli e fare clic su **[!UICONTROL Salva].L&#39;istanza Autore** è configurata per l&#39;utilizzo di [!DNL Adobe Sign].

1. Publish la configurazione.
1. Utilizza [replica](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html?lang=it) per creare una configurazione identica nelle istanze di pubblicazione corrispondenti.

Ora puoi [utilizzare Aggiungi campi Adobe Acrobat Sign in un modulo adattivo](working-with-adobe-sign.md) o [flusso di lavoro AEM](/help/forms/using/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step). Assicurarsi di aggiungere il contenitore di configurazione utilizzato per la configurazione del Cloud Service a tutto il Forms adattivo abilitato per [!DNL Adobe Acrobat Sign]. È possibile specificare un contenitore di configurazione dalle proprietà di un modulo adattivo.


## Configura l&#39;utilità di pianificazione [!DNL Adobe Sign] per sincronizzare lo stato di firma {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Un modulo adattivo abilitato per [!DNL Adobe Sign] viene inviato solo dopo che tutti i firmatari hanno completato il processo di firma. Per impostazione predefinita, i servizi di pianificazione [!DNL Adobe Sign] controllano la risposta del firmatario (polling) ogni 24 ore. È possibile modificare l’intervallo predefinito per l’ambiente. Per modificare l’intervallo predefinito, effettua le seguenti operazioni:

1. Accedi al server AEM [!DNL Forms] con le credenziali di amministratore e passa a **Strumenti** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console Web]**.

   Puoi anche aprire il seguente URL in una finestra del browser:
   `https://[localhost]:'port'/system/console/configMgr`

1. Individua e apri l&#39;opzione **[!UICONTROL Servizio di configurazione Adobe Sign]**. Specifica un&#39;espressione [cron](https://en.wikipedia.org/wiki/Cron#CRON_expression) nel campo **[!UICONTROL Espressione modulo di pianificazione aggiornamento stato]** e fai clic su **[!UICONTROL Salva]**. Ad esempio, per eseguire il servizio di configurazione ogni giorno alle 00:00, specificare `0 0 0 1/1 * ? *` nel campo **[!UICONTROL Espressione modulo di pianificazione aggiornamenti stato]**.

L&#39;intervallo predefinito per sincronizzare lo stato di [!DNL Adobe Sign] è ora modificato.

## Articoli correlati {#related-articles}

* [Utilizzo di Adobe Sign in un modulo adattivo](../../forms/using/working-with-adobe-sign.md)
* [Adobe Sign con flussi di lavoro incentrati su moduli](/help/forms/using/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)
* [Utilizzo di Adobe Sign con AEM Forms (video)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
