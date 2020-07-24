---
title: Configurate i tag delle risorse mediante Smart Content Service.
description: Scoprite come configurare i tag avanzati e i tag avanzati in [!DNL Adobe Experience Manager]mediante Smart Content Service.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 29cf202b2522b4e624960e8b911f77ec7f291e24
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 61%

---


# Configurare i tag delle risorse tramite Smart Content Service {#configure-asset-tagging-using-the-smart-content-service}

È possibile effettuare l&#39;integrazione [!DNL Adobe Experience Manager] con Smart Content Service tramite Adobe Developer Console. Utilizzate questa configurazione per accedere a Smart Content Service dall&#39;interno [!DNL Experience Manager].

L’articolo descrive le seguenti attività chiave necessarie per configurare il Servizio di contenuti avanzati. At the back end, the [!DNL Experience Manager] server authenticates your service credentials with the Adobe Developer Console gateway before forwarding your request to the Smart Content Service.

1. Crea una configurazione del Servizio di contenuti avanzati in [!DNL Experience Manager] per generare una chiave pubblica. [Ottieni un certificato pubblico](#obtain-public-certificate) per l’integrazione di OAuth.
1. [Crea un’integrazione in Adobe Developer Console](#create-adobe-i-o-integration) e carica la chiave pubblica generata.
1. [Configurate la distribuzione](#configure-smart-content-service) utilizzando la chiave API e altre credenziali da Adobe Developer Console.
1. [Verifica la configurazione](#validate-the-configuration).
1. Optionally, [enable auto-tagging on asset upload](#enable-smart-tagging-in-the-update-asset-workflow-optional).

## Prerequisiti {#prerequisites}

Prima di poter utilizzare Smart Content Service, accertatevi quanto segue per creare un&#39;integrazione in Adobe Developer Console:

* Disponi di un account Adobe ID con privilegi di amministratore dell’organizzazione.
* Il Servizio di contenuti avanzati è abilitato per la tua organizzazione.

Per abilitare i tag avanzati avanzati avanzati, oltre a quanto indicato sopra, installa anche il service pack [](https://helpx.adobe.com/it/experience-manager/aem-releases-updates.html)AEM più recente.

## Recuperare il certificato pubblico {#obtain-public-certificate}

Un certificato pubblico ti consente di autenticare il profilo su Adobe Developer Console.

1. Nell’interfaccia di [!DNL Experience Manager], accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Servizi cloud precedenti]**.

1. In the Cloud Services page, click **[!UICONTROL Configure Now]** under **[!UICONTROL Assets Smart Tags]**.
1. Nella finestra di dialogo **[!UICONTROL Crea configurazione]**, specifica un titolo e un nome per la configurazione di tag avanzati. Fai clic su **[!UICONTROL Crea]**.
1. Nella finestra di dialogo **[!UICONTROL Servizio di contenuti avanzati AEM]**, usa i seguenti valori:

   **[!UICONTROL URL servizio]**: `https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL Server autorizzazioni]**: `https://ims-na1.adobelogin.com`

   Lascia vuoti gli altri campi per il momento (dovranno essere riempiti successivamente). Fai clic su **[!UICONTROL OK]**.

   ![Finestra di dialogo Servizio di contenuti avanzati di Experience Manager per fornire l’URL del servizio di contenuti](assets/aem_scs.png)

   >[!NOTE]
   >
   >L&#39;URL fornito come URL  del servizio non è accessibile tramite browser e genera un errore 404. La configurazione funziona correttamente con lo stesso valore del parametro URL  servizio. Per informazioni sullo stato generale del servizio e sulla pianificazione della manutenzione, vedete [https://status.adobe.com](https://status.adobe.com).

1. Fai clic su **[!UICONTROL Scarica certificato pubblico per integrazione OAuth]** e scarica il file del certificato pubblico `AEM-SmartTags.crt`.

   ![Una rappresentazione delle impostazioni create per il servizio assegnazione tag avanzati](assets/smart-tags-download-public-cert.png)

### Reconfigure when a certificate expires {#certrenew}

Una volta scaduto, il certificato non è più affidabile. Non è possibile rinnovare un certificato scaduto. Per aggiungere un nuovo certificato, effettua le seguenti operazioni.

1. Accedi alla tua implementazione di [!DNL Experience Manager] come amministratore. Fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Protezione]** > **[!UICONTROL Utenti]**.

1. Individua e fai clic sull’utente **[!UICONTROL dam-update-service]**. Fai clic sulla scheda **[!UICONTROL Registro chiavi]**.
1. Elimina il registro chiavi esistente **[!UICONTROL similaritysearch]** con il certificato scaduto. Fai clic su **[!UICONTROL Salva e chiudi]**.

   ![Per aggiungere un nuovo certificato di protezione, eliminate la voce di ricerca per similarità esistente in Keystore](assets/smarttags_delete_similaritysearch_keystore.png)

   *Figura: per aggiungere un nuovo certificato di sicurezza, elimina la voce esistente`similaritysearch`in Registro chiavi*

1. Vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Servizi cloud precedenti]**. Fai clic su **[!UICONTROL Tag avanzati risorse]** > **[!UICONTROL Mostra configurazioni]** > **[!UICONTROL Configurazioni disponibili]**. Seleziona la configurazione richiesta.

1. Per scaricare un certificato pubblico, fai clic su **[!UICONTROL Scarica certificato pubblico per integrazione OAuth]**.
1. Accedi a [https://console.adobe.io](https://console.adobe.io) e passa ai Servizi di contenuti avanzati esistenti nella pagina **[!UICONTROL Integrazioni]**. Carica il nuovo certificato. For more information, see the instructions in [Create Adobe Developer Console integration](#create-adobe-i-o-integration).

## Creare un’integrazione con Adobe Developer Console {#create-adobe-i-o-integration}

Per utilizzare le API Smart Content Service, create un&#39;integrazione in Adobe Developer Console per generare la chiave API, l&#39;ID account tecnico, l&#39;ID organizzazione e il Segreto cliente.

1. Accedi a [https://console.adobe.io](https://console.adobe.io/) in un browser. Seleziona l’account appropriato e verifica che il ruolo aziendale associato sia quello di amministratore di sistema.
1. Crea un progetto con il nome desiderato. Fai clic su **[!UICONTROL Aggiungi API]**.
1. Nella pagina **[!UICONTROL Aggiungi un’API]**, seleziona **[!UICONTROL Experience Cloud]** e **[!UICONTROL Contenuti avanzati]**. Fai clic su **[!UICONTROL Avanti]**.
1. Seleziona **[!UICONTROL Carica la chiave pubblica]**. Fornisci il file del certificato scaricato da [!DNL Experience Manager]. Viene visualizzato il messaggio [!UICONTROL Chiavi pubbliche caricate correttamente]. Fai clic su **[!UICONTROL Avanti]**.
1. Nella pagina per la [!UICONTROL creazione di una nuova credenziale dell’account di servizio (JWT)] viene visualizzata la chiave pubblica per l’account di servizio appena configurato. Fai clic su **[!UICONTROL Avanti]**.
1. Nella pagina per la **[!UICONTROL selezione dei profili di prodotto]**, seleziona **[!UICONTROL Servizi di contenuti avanzati]**. Fai clic su **[!UICONTROL Salva API configurata]**. In una pagina vengono visualizzate ulteriori informazioni sulla configurazione. Tieni aperta questa pagina per copiare e aggiungere questi valori in Experience Manager durante l’ulteriore configurazione di Tag avanzati in [!DNL Experience Manager].

   ![Nella scheda Panoramica, puoi esaminare le informazioni fornite sull’integrazione.](assets/integration_details.png)

## Configurare il Servizio di contenuti avanzati {#configure-smart-content-service}

Per configurare l&#39;integrazione, utilizzate i valori dei campi ID account tecnico, ID organizzazione, Segreto cliente, Server di autorizzazione e chiave API dall&#39;integrazione di Adobe Developer Console. Creating a Smart Tags cloud configuration allows authentication of API requests from the [!DNL Experience Manager] deployment.

1. In [!DNL Experience Manager], navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Legacy Cloud Services]** to open the [!UICONTROL Cloud Services] console.
1. In **[!UICONTROL Tag avanzati risorse]**, apri la configurazione creata in precedenza. Nella pagina delle impostazioni del servizio, fai clic su **[!UICONTROL Modifica]**.
1. Nella finestra di dialogo **[!UICONTROL Servizio di contenuti avanzati AEM]**, utilizza i valori precompilati per i campi **[!UICONTROL URL servizio]** e **[!UICONTROL Server autorizzazioni]**.
1. Per i campi **[!UICONTROL Chiave API]**, **[!UICONTROL ID account tecnico]**, **[!UICONTROL ID organizzazione]** e **[!UICONTROL Segreto client]**, utilizza i valori generati sopra.

## Convalidare la configurazione {#validate-the-configuration}

Dopo aver completato la configurazione, puoi usare un MBean JMX per convalidare la configurazione. Per eseguire la convalida, effettua le seguenti operazioni.

1. Accedi al server di [!DNL Experience Manager] all’indirizzo `https://[aem_server]:[port]`.
1. Go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]** to open the OSGi console. Click **[!UICONTROL Main]>[!UICONTROL JMX]**.
1. Clic `com.day.cq.dam.similaritysearch.internal.impl`. It opens **[!UICONTROL SimilaritySearch Miscellaneous Tasks]**.
1. Clic `validateConfigs()`. Nella finestra di dialogo **[!UICONTROL Validate Configurations]** (Convalida configurazioni), fai clic su **[!UICONTROL Invoke]** (Richiama). I risultati della convalida vengono visualizzati nella stessa finestra di dialogo.

## Abilitare i tag avanzati nel flusso di lavoro [!UICONTROL DAM Update Asset] (facoltativo) {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. In [!DNL Experience Manager], go to **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Models]**.
1. Nella pagina **[!UICONTROL Modelli flusso di lavoro]**, seleziona il modello del flusso di lavoro **[!UICONTROL Risorsa di aggiornamento DAM]**.
1. Fai clic su **[!UICONTROL Modifica]** nella barra degli strumenti.
1. Per visualizzare i passaggi, espandi il pannello laterale. Trascina il passaggio **[!UICONTROL Risorsa di tag avanzati]** della sezione Flusso di lavoro DAM e inseriscilo dopo il passaggio **[!UICONTROL Elabora miniature]**.

   ![Aggiungi il passaggio Risorsa di tag avanzati dopo il passaggio Elabora miniature nel flusso di lavoro Aggiorna risorsa DAM](assets/smart-tag-in-dam-update-asset-workflow.png)

   *Figura: Aggiungi il passaggio Risorsa di tag avanzati dopo il passaggio Elabora miniature nel flusso di lavoro Aggiorna risorsa DAM.*

1. Apri il passaggio in modalità di modifica. In **[!UICONTROL Impostazioni avanzate]**, accertati che sia selezionata l’opzione **[!UICONTROL Avanzamento gestore]**.

   ![Configurare il flusso di lavoro Aggiorna risorsa DAM e aggiungere il passaggio smart tag](assets/smart-tag-step-properties-workflow1.png)

1. Nella scheda **[!UICONTROL Argomenti]**, seleziona **[!UICONTROL Ignora errori]** se vuoi che il flusso di lavoro venga completato anche con esito negativo del passaggio di assegnazione tag automatica.

   Per assegnare i tag alle risorse quando vengono caricate, a prescindere dal fatto che l’assegnazione tag avanzati sia abilitata o meno per le cartelle, seleziona **[!UICONTROL Ignora flag di tag avanzati]**.

   ![Configurare il flusso di lavoro Aggiorna risorsa DAM per aggiungere il passo smart tag e selezionare Ignora flag Smart Tag](assets/smart-tag-step-properties-workflow2.png)

1. Fai clic su **[!UICONTROL OK]** per chiudere il passaggio del processo, quindi salva il flusso di lavoro.

>[!MORELIKETHIS]
>
>* [Gestire i tag avanzati](managing-smart-tags.md)
>* [Panoramica e come formare i tag avanzati](enhanced-smart-tags.md)
>* [Linee guida e regole per la formazione di Smart Content Service](smart-tags-training-guidelines.md)
>* [Esercitazione video sulla configurazione degli smart tag](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-technical-video-setup.html)

