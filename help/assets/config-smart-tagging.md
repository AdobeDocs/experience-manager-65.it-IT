---
title: Configurare l’assegnazione tag delle risorse tramite Smart Content Service
description: Scopri come configurare l'assegnazione tag avanzati e l'assegnazione tag avanzati migliorati in [!DNL Adobe Experience Manager], utilizzando il Servizio di contenuti avanzati.
contentOwner: AG
role: Admin
feature: Tagging,Smart Tags
exl-id: 9f68804f-ba15-4f83-ab1b-c249424b1396
solution: Experience Manager, Experience Manager Assets
source-git-commit: 5aff321eb52c97e076c225b67c35e9c6d3371154
workflow-type: tm+mt
source-wordcount: '2415'
ht-degree: 26%

---

# Prepara [!DNL Assets] per assegnazione tag avanzati {#configure-asset-tagging-using-the-smart-content-service}

Prima di iniziare a assegnare tag alle risorse utilizzando Smart Content Services, è necessario integrare [!DNL Experience Manager Assets] con Adobe Developer Console per utilizzare Smart Service di [!DNL Adobe Sensei]. Una volta configurato, il servizio viene addestrato utilizzando alcune immagini e un tag.

>[!NOTE]
>
>* Smart Content Services non è più disponibile per i nuovi clienti locali di [!DNL Experience Manager Assets]. I clienti on-premise esistenti che dispongono già di questa funzionalità possono continuare a utilizzare Smart Content Services.
>* Smart Content Services è disponibile per i clienti esistenti di [!DNL Experience Manager Assets] Managed Services che dispongono già di questa funzionalità abilitata.
>* I nuovi clienti di [!DNL Experience Manager Assets] Managed Services possono seguire le istruzioni riportate in questo articolo per configurare Smart Content Services.

Prima di utilizzare il Servizio di contenuti avanzati, verifica quanto segue:

* [Integrare con Adobe Developer Console](#integrate-adobe-io).
* [Formazione del Servizio di contenuti avanzati](#training-the-smart-content-service).

* Installa il [[!DNL Experience Manager] Service Pack](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=it) più recente.

## Integrare con Adobe Developer Console {#integrate-adobe-io}

Quando si esegue l&#39;integrazione con Adobe Developer Console, il server [!DNL Experience Manager] autentica le credenziali del servizio con il gateway di Adobe Developer Console prima di inoltrare la richiesta al Servizio di contenuti avanzati. Per l’integrazione, è necessario un account Adobe ID con privilegi di amministratore per l’organizzazione e una licenza del Servizio di contenuti avanzati acquistata e abilitata per la tua organizzazione.

Per configurare il Servizio di contenuti avanzati, segui questi passaggi di livello principale:

1. Per generare una chiave pubblica, [Crea una configurazione del Servizio di contenuti avanzati](#obtain-public-certificate) in [!DNL Experience Manager]. [Ottieni un certificato pubblico](#obtain-public-certificate) per l’integrazione di OAuth.

1. [Crea un’integrazione in Adobe Developer Console](#create-adobe-i-o-integration) e carica la chiave pubblica generata.

1. [Configura la distribuzione](#configure-smart-content-service) utilizzando la chiave API e altre credenziali di Adobe Developer Console.

1. [Verifica la configurazione](#validate-the-configuration).

1. Facoltativamente, [abilita assegnazione tag automatica al caricamento delle risorse](#enable-smart-tagging-in-the-update-asset-workflow-optional).

### Ottenere un certificato pubblico creando la configurazione del Servizio di contenuti avanzati {#obtain-public-certificate}

Un certificato pubblico consente di autenticare il profilo su Adobe Developer Console.

1. Nell’interfaccia di [!DNL Experience Manager], accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Servizi cloud precedenti]**.

1. Nella pagina Cloud Service, fai clic su **[!UICONTROL Configura ora]** in **[!UICONTROL Tag avanzati di Assets]**.

1. Nella finestra di dialogo **[!UICONTROL Crea configurazione]**, specifica un titolo e un nome per la configurazione di tag avanzati. Fai clic su **[!UICONTROL Crea]**.

1. Nella finestra di dialogo **[!UICONTROL Servizio di contenuti avanzati AEM]**, usa i seguenti valori:

   **[!UICONTROL URL servizio]**: `https://smartcontent.adobe.io/<region where your Experience Manager author instance is hosted>`

   Ad esempio, `https://smartcontent.adobe.io/apac`. È possibile specificare `na`, `emea` o `apac` come aree in cui è ospitata l&#39;istanza Autore Experience Manager.

   >[!NOTE]
   >
   >Se il provisioning di Experience Manager Managed Service è stato eseguito prima del 1° settembre 2022, utilizza il seguente URL del servizio:
   >`https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL Server autorizzazioni]**: `https://ims-na1.adobelogin.com`

   Lascia vuoti gli altri campi per il momento (dovranno essere riempiti successivamente). Fai clic su **[!UICONTROL OK]**.

   ![Finestra di dialogo Servizio di contenuti avanzati di Experience Manager per fornire l’URL del servizio di contenuti](assets/aem_scs.png)


   *Figura: finestra di dialogo Servizio di contenuti avanzati per fornire l&#39;URL del servizio di contenuti*

   >[!NOTE]
   >
   >L&#39;URL fornito come [!UICONTROL URL servizio] non è accessibile tramite browser e genera un errore 404. La configurazione funziona correttamente con lo stesso valore del parametro [!UICONTROL URL servizio]. Per informazioni sullo stato generale del servizio e sulla pianificazione della manutenzione, vedere [https://status.adobe.com](https://status.adobe.com).

1. Fai clic su **[!UICONTROL Scarica certificato pubblico per integrazione OAuth]** e scarica il file del certificato pubblico `AEM-SmartTags.crt`.

   ![Una rappresentazione delle impostazioni create per il servizio assegnazione tag avanzati](assets/smart-tags-download-public-cert.png)


   *Figura: impostazioni per il servizio di assegnazione tag avanzati.*

#### Riconfigura alla scadenza di un certificato {#certrenew}

Dopo la scadenza, il certificato non è più attendibile. Impossibile rinnovare un certificato scaduto. Per aggiungere un certificato, segui la procedura riportata di seguito.

1. Accedi alla tua implementazione di [!DNL Experience Manager] come amministratore. Fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Protezione]** > **[!UICONTROL Utenti]**.

1. Individua e fai clic sull’utente **[!UICONTROL dam-update-service]**. Fare clic sulla scheda **[!UICONTROL Registro chiavi]**.

1. Elimina il registro chiavi esistente **[!UICONTROL similaritysearch]** con il certificato scaduto. Fai clic su **[!UICONTROL Salva e chiudi]**.

   ![Per aggiungere un certificato di sicurezza, elimina la voce esistente per la ricerca per affinità in Registro chiavi](assets/smarttags_delete_similaritysearch_keystore.png)


   *Figura: per aggiungere un certificato di sicurezza, eliminare la voce `similaritysearch` esistente in Registro chiavi.*

1. Vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Servizi cloud precedenti]**. Fai clic su **[!UICONTROL Tag avanzati risorse]** > **[!UICONTROL Mostra configurazioni]** > **[!UICONTROL Configurazioni disponibili]**. Seleziona la configurazione richiesta.

1. Per scaricare un certificato pubblico, fai clic su **[!UICONTROL Scarica certificato pubblico per integrazione OAuth]**.

1. Accedi a [https://console.adobe.io](https://console.adobe.io) e passa ai Servizi di contenuti avanzati esistenti nella pagina **[!UICONTROL Integrazioni]**. Carica il nuovo certificato. Per ulteriori informazioni, vedere le istruzioni in [Creare l&#39;integrazione di Adobe Developer Console](#create-adobe-i-o-integration).

### Creare l’integrazione con Adobe Developer Console {#create-adobe-i-o-integration}

Per utilizzare le API del Servizio di contenuti avanzati, creare un&#39;integrazione in Adobe Developer Console per ottenere [!UICONTROL la chiave API] (generata nel campo [!UICONTROL ID CLIENT] dell&#39;integrazione Adobe Developer Console), [!UICONTROL ID ACCOUNT TECNICO], [!UICONTROL ID ORGANIZZAZIONE] e [!UICONTROL SEGRETO CLIENT] per [!UICONTROL Impostazioni del Servizio di tag avanzati Assets] della configurazione cloud in [!DNL Experience Manager].

1. Accedi a [https://console.adobe.io](https://console.adobe.io/) in un browser. Seleziona l’account appropriato e verifica che il ruolo aziendale associato sia quello di amministratore di sistema.

1. Crea un progetto con il nome desiderato. Fai clic su **[!UICONTROL Aggiungi API]**.

1. Nella pagina **[!UICONTROL Aggiungi un’API]**, seleziona **[!UICONTROL Experience Cloud]** e **[!UICONTROL Contenuti avanzati]**. Fai clic su **[!UICONTROL Avanti]**.

1. Seleziona **[!UICONTROL Carica la chiave pubblica]**. Fornisci il file del certificato scaricato da [!DNL Experience Manager]. Viene visualizzato il messaggio [!UICONTROL Chiavi pubbliche caricate correttamente]. Fai clic su **[!UICONTROL Avanti]**.

   Nella pagina [!UICONTROL Crea una nuova credenziale dell&#39;account di servizio (JWT)] viene visualizzata la chiave pubblica per l&#39;account di servizio.

1. Fai clic su **[!UICONTROL Avanti]**.

1. Nella pagina per la **[!UICONTROL selezione dei profili di prodotto]**, seleziona **[!UICONTROL Servizi di contenuti avanzati]**. Fai clic su **[!UICONTROL Salva API configurata]**.

   In una pagina vengono visualizzate ulteriori informazioni sulla configurazione. Tieni aperta questa pagina per copiare e aggiungere questi valori nelle [!UICONTROL Impostazioni del servizio di assegnazione tag avanzati di Assets] della configurazione cloud in [!DNL Experience Manager] per configurare gli smart tag.

   ![Nella scheda Panoramica, puoi esaminare le informazioni fornite sull’integrazione.](assets/integration_details.png)


   *Figura: dettagli dell&#39;integrazione in Adobe Developer Console*

### Configurare il Servizio di contenuti avanzati {#configure-smart-content-service}

>[!CAUTION]
>
>In precedenza, le configurazioni create con credenziali JWT ora sono diventate obsolete in Adobe Developer Console. Non puoi creare nuove credenziali JWT dopo il 3 giugno 2024. Tali configurazioni non possono più essere create o aggiornate, ma è possibile eseguirne la migrazione alle configurazioni OAuth.
> Vedi [Configurazione delle integrazioni IMS per AEM](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service)
>Consulta [Passaggi per configurare OAuth per gli utenti on-premise](#config-oauth-onprem)
> Consulta [Risoluzione dei problemi dei tag avanzati per le credenziali OAuth](#config-smart-tagging.md)

Per configurare l&#39;integrazione, utilizzare i valori dei campi [!UICONTROL ID ACCOUNT TECNICO], [!UICONTROL ID ORGANIZZAZIONE], [!UICONTROL SEGRETO CLIENT] e [!UICONTROL ID CLIENT] dell&#39;integrazione Adobe Developer Console. La creazione di una configurazione cloud di tag avanzati consente l&#39;autenticazione delle richieste API dalla distribuzione [!DNL Experience Manager].

1. In [!DNL Experience Manager], passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Cloud Services precedenti]** per aprire la console [!UICONTROL Cloud Services].

1. In **[!UICONTROL Tag avanzati risorse]**, apri la configurazione creata in precedenza. Nella pagina delle impostazioni del servizio, fai clic su **[!UICONTROL Modifica]**.

1. Nella finestra di dialogo **[!UICONTROL Servizio di contenuti avanzati AEM]**, utilizza i valori precompilati per i campi **[!UICONTROL URL servizio]** e **[!UICONTROL Server autorizzazioni]**.

1. Per i campi [!UICONTROL Chiave API], [!UICONTROL ID account tecnico], [!UICONTROL ID organizzazione] e [!UICONTROL Segreto client], copia e utilizza i seguenti valori generati nell&#39;[integrazione Adobe Developer Console](#create-adobe-i-o-integration).

   | [!UICONTROL Impostazioni del servizio di assegnazione tag avanzati di Assets] | [!DNL Adobe Developer Console] campi di integrazione |
   |--- |--- |
   | [!UICONTROL Chiave Api] | [!UICONTROL ID CLIENT] |
   | [!UICONTROL ID account tecnico] | [!UICONTROL ID ACCOUNT TECNICO] |
   | [!UICONTROL ID organizzazione] | [!UICONTROL ID ORGANIZZAZIONE] |
   | [!UICONTROL Segreto client] | [!UICONTROL SEGRETO CLIENT] |

### Configurare OAuth per gli utenti locali {#config-oauth-onprem}

#### Prerequisiti {#prereqs-config-oauth-onprem}

Un ambito di autorizzazione è una stringa OAuth che contiene i seguenti prerequisiti:

* Crea una nuova integrazione OAuth in [Developer Console](https://developer.adobe.com/console/user/servicesandapis) utilizzando `ClientID`, `ClientSecretID` e `OrgID`.
* Aggiungere i seguenti file nel percorso `/apps/system/config in crx/de`:
   * `com.adobe.granite.auth.oauth.accesstoken.provider.<randomnumbers>.config`
   * `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl.<randomnumber>.config`

#### Configurare OAuth per gli utenti locali {#steps-config-oauth-onprem}

1. Aggiungi o aggiorna le seguenti proprietà in `com.adobe.granite.auth.oauth.accesstoken.provider.<randomnumbers>.config`:

   * `auth.token.provider.authorization.grants="client_credentials"`
   * `auth.token.provider.orgId="<OrgID>"`
   * `auth.token.provider.default.claims=("\"iss\"\ :\ \"<OrgID>\"")`
   * `auth.token.provider.scope="read_pc.dma_smart_content,\ openid,\ AdobeID,\ additional_info.projectedProductContext"`
     `auth.token.validator.type="adobe-ims-similaritysearch"`
   * Aggiorna `auth.token.provider.client.id` con l&#39;ID client della nuova configurazione OAuth.
   * Aggiorna `auth.access.token.request` a `"https://ims-na1.adobelogin.com/ims/token/v3"`
2. Rinominare il file in `com.adobe.granite.auth.oauth.accesstoken.provider-<randomnumber>.config`.
3. Eseguire i passaggi seguenti in `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl.<randomnumber>.config`:
   * Aggiorna la proprietà auth.ims.client.secret con il segreto client dalla nuova integrazione OAuth.
   * Rinomina il file in `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl-<randomnumber>.config`
4. Salva tutte le modifiche nella console di sviluppo dell’archivio dei contenuti, ad esempio CRXDE.
5. Passa a `/system/console/configMgr` e sostituisci la configurazione OSGi da `.<randomnumber>` a `-<randomnumber>`.
6. Elimina la configurazione precedente per `"Access Token provider name: adobe-ims-similaritysearch"` in `/system/console/configMgr`.
7. Riavvia la console.

### Convalidare la configurazione {#validate-the-configuration}

Dopo aver completato la configurazione, puoi utilizzare un MBean JMX per convalidarla. Per eseguire la convalida, effettua le seguenti operazioni.

1. Accedi al server di [!DNL Experience Manager] all’indirizzo `https://[aem_server]:[port]`.

1. Vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console Web]** per aprire la console OSGi. Fai clic su **[!UICONTROL Principale] > [!UICONTROL JMX]**.

1. Fai clic su `com.day.cq.dam.similaritysearch.internal.impl`. Apre **[!UICONTROL Attività varie di SimilaritySearch]**.

1. Fai clic su `validateConfigs()`. Nella finestra di dialogo **[!UICONTROL Validate Configurations]** (Convalida configurazioni), fai clic su **[!UICONTROL Invoke]** (Richiama).

I risultati della convalida vengono visualizzati nella stessa finestra di dialogo.

### Abilitare l&#39;assegnazione tag avanzati nel flusso di lavoro [!UICONTROL Risorsa di aggiornamento DAM] (facoltativo) {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. In [!DNL Experience Manager], vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.

1. Nella pagina **[!UICONTROL Modelli flusso di lavoro]**, seleziona il modello del flusso di lavoro **[!UICONTROL Risorsa di aggiornamento DAM]**.

1. Fai clic su **[!UICONTROL Modifica]** nella barra degli strumenti.

1. Per visualizzare i passaggi, espandi il pannello laterale. Trascina il passaggio **[!UICONTROL Risorsa di tag avanzati]** della sezione Flusso di lavoro DAM e inseriscilo dopo il passaggio **[!UICONTROL Elabora miniature]**.

   ![Aggiungi il passaggio Risorsa di tag avanzati dopo il passaggio Elabora miniature nel flusso di lavoro Aggiorna risorsa DAM](assets/smart-tag-in-dam-update-asset-workflow.png)

   *Figura: aggiungi il passaggio Risorsa di tag avanzati dopo il passaggio Elabora miniature nel flusso di lavoro [!UICONTROL Risorsa di aggiornamento DAM].*

1. Apri il passaggio in modalità di modifica. In **[!UICONTROL Impostazioni avanzate]**, accertati che sia selezionata l’opzione **[!UICONTROL Avanzamento gestore]**.

   ![Configurare il flusso di lavoro Aggiorna risorsa DAM e aggiungere il passaggio smart tag](assets/smart-tag-step-properties-workflow1.png)


   *Figura: configurare il flusso di lavoro Aggiorna risorsa DAM e aggiungere il passaggio smart tag*

1. Nella scheda **[!UICONTROL Argomenti]**, seleziona **[!UICONTROL Ignora errori]** se vuoi che il flusso di lavoro venga completato anche con esito negativo del passaggio di assegnazione tag automatica.

   ![Configura il flusso di lavoro Risorsa di aggiornamento DAM per aggiungere il passaggio smart tag e selezionare l&#39;handler avanzato](assets/smart-tag-step-properties-workflow2.png)


   *Figura: configura il flusso di lavoro Risorsa di aggiornamento DAM per aggiungere il passaggio smart tag e selezionare l&#39;avanzamento del gestore*

   Per assegnare i tag alle risorse quando vengono caricate, a prescindere dal fatto che l’assegnazione tag avanzati sia abilitata o meno per le cartelle, seleziona **[!UICONTROL Ignora flag di tag avanzati]**.

   ![Configura il flusso di lavoro Risorsa di aggiornamento DAM per aggiungere il passaggio smart tag e selezionare Ignora flag di smart tag](assets/smart-tag-step-properties-workflow3.png)


   *Figura: Configura il flusso di lavoro Risorsa di aggiornamento DAM per aggiungere il passaggio smart tag e selezionare Ignora flag di smart tag.*

1. Fare clic su **[!UICONTROL OK]** per chiudere il passaggio del processo, quindi salvare il flusso di lavoro.

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
>La capacità del Servizio di contenuti avanzati di addestrarsi sui tag e di applicarli ad altre immagini dipende dalla qualità delle immagini utilizzate per la formazione. Per ottenere i migliori risultati, l’Adobe consiglia di utilizzare immagini visivamente simili per addestrare il servizio per ogni tag.

### Formazione periodica {#periodic-training}

Puoi abilitare il Servizio di contenuti avanzati per la formazione periodica sulle risorse e sui tag associati all’interno di una cartella. Apri la pagina [!UICONTROL Proprietà] della cartella di risorse, seleziona **[!UICONTROL Abilita tag avanzati]** nella scheda **[!UICONTROL Dettagli]** e salva le modifiche.

![enable_smart_tags](assets/enable_smart_tags.png)

Una volta selezionata questa opzione per una cartella, [!DNL Experience Manager] esegue automaticamente un flusso di lavoro di formazione per addestrare il Servizio di contenuti avanzati sulle risorse della cartella e sui relativi tag. Per impostazione predefinita, il flusso di lavoro di formazione viene eseguito settimanalmente alle 00:30 del sabato.

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
>* [Esercitazione video sugli smart tag](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html)
