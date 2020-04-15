---
title: Configurare i tag delle risorse tramite Smart Content Service
description: Scoprite come configurare i tag avanzati e i tag avanzati in AEM, utilizzando Smart Content Service.
contentOwner: AG
translation-type: tm+mt
source-git-commit: c7d0bcbf39adfc7dfd01742651589efb72959603

---


# Configurare i tag delle risorse tramite Smart Content Service {#configure-asset-tagging-using-the-smart-content-service}

Puoi integrare Adobe Experience Manager (AEM) con Smart Content Service tramite Adobe I/O. Utilizzate questa configurazione per accedere a Smart Content Service da AEM.

L&#39;articolo descrive le seguenti attività chiave necessarie per configurare Smart Content Service. Sul lato posteriore, il server AEM autentica le credenziali del servizio con il gateway Adobe IO prima di inoltrare la richiesta a Smart Content Service.

* Create una configurazione di Smart Content Service in AEM per generare una chiave pubblica. Ottenete un certificato pubblico per l&#39;integrazione OAuth.
* Create un&#39;integrazione in Adobe I/O e caricate la chiave pubblica generata.
* Configurate l&#39;istanza AEM utilizzando la chiave API e altre credenziali dall&#39;I/O di Adobe.
* Se necessario, abilitate l’assegnazione automatica di tag al caricamento delle risorse.

## Prerequisiti {#prerequisites}

Prima di poter utilizzare Smart Content Service, accertatevi quanto segue per creare un&#39;integrazione su Adobe I/O:

* Un account Adobe ID con privilegi di amministratore per l’organizzazione.
* Il servizio Smart Content Service è abilitato per la vostra azienda.

## Recuperare il certificato pubblico {#obtain-public-certificate}

Un certificato pubblico consente di autenticare il profilo sull&#39;I/O di Adobe.

1. From the AEM user interface, click the AEM logo, and go to **[!UICONTROL Tools > Cloud Services]**> **[!UICONTROL Legacy Cloud Services]**.

1. In the Cloud Services page, click **[!UICONTROL Configure Now]** under **[!UICONTROL Assets Smart Tags]**.
1. Nella finestra di dialogo **[!UICONTROL Crea configurazione]** , specificate un titolo e un nome per la configurazione Smart Tags. Fai clic su **[!UICONTROL Crea]**.
1. Nella finestra di dialogo **[!UICONTROL AEM Smart Content Service]** , usate i seguenti valori:

   **[!UICONTROL URL servizio]**: `https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL Server autorizzazioni]**: `https://ims-na1.adobelogin.com`

   Lasciate vuoti gli altri campi per ora (da fornire successivamente). Fai clic su **[!UICONTROL OK]**. 

   ![Finestra di dialogo di AEM Smart Content Service per fornire l&#39;URL del servizio di contenuto](assets/aem_scs.png)

1. Fate clic su **[!UICONTROL Scarica certificato pubblico per l&#39;integrazione]** OAuth e scaricate il file del certificato pubblico `AEM-SmartTags.crt`.

   ![Una rappresentazione delle impostazioni create per il servizio di smart tag](assets/download_link.png)

### Riconfigura alla scadenza di un certificato {#certrenew}

Alla scadenza del certificato non è più attendibile. Per aggiungere un nuovo certificato, attenetevi alla procedura seguente. Non è possibile rinnovare un certificato scaduto.

1. Accedi alla tua distribuzione AEM come amministratore. Fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Protezione]** > **[!UICONTROL Utenti]**.

1. Individuate e fate clic su **[!UICONTROL dam-update-service]** user. Fate clic sulla scheda **[!UICONTROL Keystore]** .
1. Eliminate l&#39;archivio di chiavi di ricerca **[!UICONTROL per]** similarità esistente con il certificato scaduto. Click **[!UICONTROL Save &amp; Close]**.

   ![Per aggiungere un nuovo certificato di protezione, eliminate una voce di ricerca per similarità in Keystore](assets/smarttags_delete_similaritysearch_keystore.png)

   Per aggiungere un nuovo certificato di protezione, eliminate una voce di ricerca per similarità in Keystore

1. Vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Servizi cloud precedenti]**. Fai clic su **[!UICONTROL Tag avanzati risorse]** > **[!UICONTROL Mostra configurazioni]** > **[!UICONTROL Configurazioni disponibili]**. Seleziona la configurazione richiesta.

1. Per scaricare un certificato pubblico, fate clic su **[!UICONTROL Scarica certificato pubblico per l&#39;integrazione]** OAuth.
1. Accedete a [https://console.adobe.io](https://console.adobe.io) e andate a Smart Content Services nella pagina **[!UICONTROL Integrazioni]** . Caricate il nuovo certificato. Per ulteriori informazioni, consultate le istruzioni in [Creazione dell&#39;integrazione](#create-adobe-i-o-integration)I/O Adobe.

## Creare l’integrazione di Adobe I/O {#create-adobe-i-o-integration}

Per utilizzare le API Smart Content Service, create un&#39;integrazione in Adobe I/O per generare la chiave API, l&#39;ID account tecnico, l&#39;ID organizzazione e il Segreto cliente.

1. Accedete a [https://console.adobe.io](https://console.adobe.io/).
1. Nella pagina **[!UICONTROL Integrazioni]** , selezionate l&#39;account appropriato e verificate che il ruolo organizzazione associato sia amministratore di sistema.
1. Fate clic su **[!UICONTROL Nuova integrazione]**.
1. Nella pagina **[!UICONTROL Crea nuova integrazione]** , selezionate **[!UICONTROL Accedi a un&#39;API]**. Fate clic su **[!UICONTROL Continua]**.
1. In **[!UICONTROL Experience Cloud]**, seleziona **[!UICONTROL Smart Content]**. Fate clic su **[!UICONTROL Continua]**.

   ![Quando crei una nuova integrazione, seleziona Smart Content in Experience Cloud dalle opzioni disponibili](assets/smart_content.png)

1. Nella pagina successiva, selezionate **[!UICONTROL Nuova integrazione]**. Fate clic su **[!UICONTROL Continua]**.
1. Nella pagina **[!UICONTROL Dettagli]** integrazione, specificate un nome per il gateway di integrazione e aggiungete una descrizione.
1. Nei certificati delle chiavi **[!UICONTROL pubbliche]**, caricate il `AEM-SmartTags.crt` file scaricato in precedenza.
1. Fai clic su **[!UICONTROL Create Integration]** (Crea integrazione).
1. Per visualizzare le informazioni sull&#39;integrazione, fate clic su **[!UICONTROL Continua con i dettagli]** sull&#39;integrazione.

   ![Nella scheda Panoramica è possibile esaminare le informazioni fornite per l&#39;integrazione.](assets/integration_details.png)

## Configurare Smart Content Service {#configure-smart-content-service}

Per configurare l&#39;integrazione, utilizzate i valori dei campi ID account tecnico, ID organizzazione, Segreto cliente, Server autorizzazioni e chiave API dall&#39;integrazione I/O di Adobe. La creazione di una configurazione cloud di Smart Tags consente l’autenticazione delle richieste API dall’istanza AEM.

1. In Experience Manager, passa a **[!UICONTROL Strumenti > Servizio Cloud > Servizi]** cloud legacy per aprire la console Servizi  Cloud.
1. In Tag **[!UICONTROL avanzati]** risorse, apri la configurazione creata sopra. Nella pagina delle impostazioni del servizio, fate clic su **[!UICONTROL Modifica]**.
1. Nella finestra di dialogo **[!UICONTROL Servizio di contenuti avanzati AEM]**, utilizza i valori precompilati per i campi **[!UICONTROL URL servizio]** e **[!UICONTROL Server autorizzazioni]**.
1. Per i campi **[!UICONTROL Chiave API]**, **[!UICONTROL ID account tecnico]**, **[!UICONTROL ID organizzazione]** e **[!UICONTROL Segreto client]**, utilizza i valori generati sopra.

## Convalida della configurazione {#validate-the-configuration}

Dopo aver completato la configurazione, puoi usare un MBean JMX per convalidare la configurazione. Per eseguire la convalida, effettuare le seguenti operazioni.

1. Accedi al server AEM all&#39;indirizzo `https://[server]:[port]`.

1. Passate a **[!UICONTROL Strumenti > Operazioni > Console]** Web per aprire la console OSGi. Fate clic su **[!UICONTROL Principale > JMX]**.
1. Fate clic su **[!UICONTROL com.day.cq.dam.similaritysearch.internal.impl]**. Si apre **[!UICONTROL SimilaritySearch Attività varie.]**
1. Fare clic su **[!UICONTROL validateConfigs()]**. Nella finestra di dialogo **[!UICONTROL Convalida configurazioni]** , fare clic su **[!UICONTROL Richiama]**.

   Il risultato della convalida viene visualizzato nella stessa finestra di dialogo.

## Abilitare i tag avanzati nel flusso di lavoro Aggiorna risorsa (facoltativo) {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. In Experience Manager, accedi a **[!UICONTROL Strumenti > Flusso di lavoro > Modelli]**.
1. Nella pagina **[!UICONTROL Modelli flusso di lavoro]**, seleziona il modello del flusso di lavoro **[!UICONTROL Risorsa di aggiornamento DAM]**.
1. Fare clic su **[!UICONTROL Modifica]** nella barra degli strumenti.
1. Per visualizzare i passaggi, espandi il pannello laterale. Trascina il passaggio **[!UICONTROL Risorsa di tag avanzati]** della sezione Flusso di lavoro DAM e inseriscilo dopo il passaggio **[!UICONTROL Elabora miniature]**.

   ![Aggiungere un passaggio di risorsa smart tag dopo la miniatura del processo nel flusso di lavoro [!UICONTROL DAM Update Asset]](assets/chlimage_1-105.png)

   *Figura: Aggiungere un passaggio di risorsa smart tag dopo la miniatura del processo nel flusso di lavoro[!UICONTROL DAM Update Asset]*

1. Apri il passaggio in modalità di modifica. In **[!UICONTROL Impostazioni avanzate]**, accertati che sia selezionata l’opzione **[!UICONTROL Avanzamento gestore]**.

   ![chlimage_1-3](assets/chlimage_1-106.png)

1. Nella scheda **[!UICONTROL Argomenti]**, seleziona **[!UICONTROL Ignora errori]** se vuoi che il flusso di lavoro venga completato anche con esito negativo del passaggio di assegnazione tag automatica.

   ![chlimage_1-4](assets/chlimage_1-107.png)

   Per assegnare tag alle risorse quando vengono caricate, a prescindere dal fatto che l’assegnazione di tag avanzati sia abilitata o meno nelle cartelle, selezionate **[!UICONTROL Ignora contrassegno]** smart tag.

   ![chlimage_1-5](assets/chlimage_1-108.png)

1. Fate clic su **[!UICONTROL OK]** per chiudere il passaggio del processo, quindi salvate il flusso di lavoro.

>[!MORELIKETHIS]
>
>* [Gestire i tag avanzati](managing-smart-tags.md)
>* [Panoramica e come formare i tag avanzati](enhanced-smart-tags.md)
>* [Linee guida e regole per la formazione di Smart Content Service](smart-tags-training-guidelines.md)
>* [Esercitazione video sulla configurazione degli smart tag](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-technical-video-setup.html)

