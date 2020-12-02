---
title: Configurare i tag delle risorse tramite Smart Content Service
description: Scoprite come configurare i tag avanzati e i tag avanzati in [!DNL Adobe Experience Manager] utilizzando Smart Content Service.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '2179'
ht-degree: 35%

---


# Preparare [!DNL Assets] per l&#39;assegnazione di tag avanzati {#configure-asset-tagging-using-the-smart-content-service}

Prima di poter iniziare a assegnare tag alle risorse tramite Smart Content Services, è necessario integrare [!DNL Experience ManageR Assets] con  Adobe Developer Console per sfruttare il servizio avanzato [!DNL Adobe Sensei]. Una volta configurato, il servizio viene addestrato utilizzando alcune immagini e un tag.

Prima di utilizzare Smart Content Service, accertatevi quanto segue:

* [Integrare con Adobe Developer Console](#integrate-adobe-io).
* [Formazione del servizio](#training-the-smart-content-service) Smart Content.

   <!-- TBD: This link will update soon after the new articles goes live on docs.adobe.com. Change it when new URL is available.
  -->

* Installare il service pack di Experience Manager [ più recente](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html).

## Integrare con Adobe Developer Console {#integrate-adobe-io}

Quando si esegue l&#39;integrazione con  Adobe Developer Console, il server [!DNL Experience Manager] esegue l&#39;autenticazione delle credenziali del servizio con il gateway  Adobe Developer Console prima di inoltrare la richiesta a Smart Content Service. Per poter essere integrato, è necessario un account Adobe ID  che disponga dei privilegi di amministratore per l&#39;organizzazione e della licenza di Smart Content Service acquistati e abilitati per l&#39;organizzazione.

Per configurare Smart Content Service, attenetevi alla seguente procedura di livello principale:

1. [](#obtain-public-certificate)Crea una configurazione del Servizio di contenuti avanzati in [!DNL Experience Manager] per generare una chiave pubblica. [Ottieni un certificato pubblico](#obtain-public-certificate) per l’integrazione di OAuth.

1. [Crea un’integrazione in Adobe Developer Console](#create-adobe-i-o-integration) e carica la chiave pubblica generata.

1. [Configurate la ](#configure-smart-content-service) distribuzione utilizzando la chiave API e altre credenziali da  Adobe Developer Console.

1. [Verifica la configurazione](#validate-the-configuration).

1. Facoltativamente, [abilita l&#39;assegnazione di tag automatica al caricamento delle risorse](#enable-smart-tagging-in-the-update-asset-workflow-optional).

### Creare la configurazione di Smart Content Service per ottenere il certificato pubblico {#obtain-public-certificate}

Un certificato pubblico ti consente di autenticare il profilo su Adobe Developer Console.

1. Nell’interfaccia di [!DNL Experience Manager], accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Servizi cloud precedenti]**.

1. Nella pagina Cloud Services, fare clic su **[!UICONTROL Configura ora]** in **[!UICONTROL Risorse Smart Tags]**.

1. Nella finestra di dialogo **[!UICONTROL Crea configurazione]**, specifica un titolo e un nome per la configurazione di tag avanzati. Fai clic su **[!UICONTROL Crea]**.

1. Nella finestra di dialogo **[!UICONTROL Servizio di contenuti avanzati AEM]**, usa i seguenti valori:

   **[!UICONTROL URL servizio]**: `https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL Server autorizzazioni]**: `https://ims-na1.adobelogin.com`

   Lascia vuoti gli altri campi per il momento (dovranno essere riempiti successivamente). Fai clic su **[!UICONTROL OK]**.

   ![Finestra di dialogo Servizio di contenuti avanzati di Experience Manager per fornire l’URL del servizio di contenuti](assets/aem_scs.png)


   *Figura: Finestra di dialogo Smart Content Service per fornire l&#39;URL del servizio di contenuto*

   >[!NOTE]
   >
   >L&#39;URL fornito come [!UICONTROL URL servizio] non è accessibile tramite browser e genera un errore 404. La configurazione funziona correttamente con lo stesso valore del parametro [!UICONTROL URL del servizio]. Per informazioni sullo stato generale del servizio e sul programma di manutenzione, vedere [https://status.adobe.com](https://status.adobe.com).

1. Fai clic su **[!UICONTROL Scarica certificato pubblico per integrazione OAuth]** e scarica il file del certificato pubblico `AEM-SmartTags.crt`.

   ![Una rappresentazione delle impostazioni create per il servizio assegnazione tag avanzati](assets/smart-tags-download-public-cert.png)


   *Figura: Impostazioni per il servizio di smart tag*

#### Riconfigura alla scadenza del certificato {#certrenew}

Una volta scaduto, il certificato non è più affidabile. Non è possibile rinnovare un certificato scaduto. Per aggiungere un nuovo certificato, effettua le seguenti operazioni.

1. Accedi alla tua implementazione di [!DNL Experience Manager] come amministratore. Fai clic su **[!UICONTROL Strumenti]** > **[!UICONTROL Protezione]** > **[!UICONTROL Utenti]**.

1. Individua e fai clic sull’utente **[!UICONTROL dam-update-service]**. Fare clic sulla scheda **[!UICONTROL Keystore]**.

1. Elimina il registro chiavi esistente **[!UICONTROL similaritysearch]** con il certificato scaduto. Fai clic su **[!UICONTROL Salva e chiudi]**.

   ![Per aggiungere un nuovo certificato di protezione, eliminate la voce di ricerca per similarità esistente in Keystore](assets/smarttags_delete_similaritysearch_keystore.png)


   *Figura: per aggiungere un nuovo certificato di sicurezza, elimina la voce esistente `similaritysearch` in Registro chiavi*

1. Vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Servizi cloud precedenti]**. Fai clic su **[!UICONTROL Tag avanzati risorse]** > **[!UICONTROL Mostra configurazioni]** > **[!UICONTROL Configurazioni disponibili]**. Seleziona la configurazione richiesta.

1. Per scaricare un certificato pubblico, fai clic su **[!UICONTROL Scarica certificato pubblico per integrazione OAuth]**.

1. Accedi a [https://console.adobe.io](https://console.adobe.io) e passa ai Servizi di contenuti avanzati esistenti nella pagina **[!UICONTROL Integrazioni]**. Carica il nuovo certificato. Per ulteriori informazioni, consultare le istruzioni riportate in [Creare &#39;integrazione della console per sviluppatori di Adobi](#create-adobe-i-o-integration).

### Crea &#39;integrazione con Developer Console di Adobe {#create-adobe-i-o-integration}

Per utilizzare le API di Smart Content Service, create un&#39;integrazione in  Adobe Developer Console per ottenere [!UICONTROL Chiave API] (generata nel campo [!UICONTROL ID CLIENT] dell&#39;integrazione  Adobe Developer Console), [!UICONTROL ID ACCOUNT TECNICO], [!UICONTROL ID ORGANIZZAZIONE] e [!UICONTROL ID CLIENT SECRET] per [!UICONTROL Assets Smart Tagging Service Settings] della configurazione cloud in [!DNL Experience Manager].

1. Accedi a [https://console.adobe.io](https://console.adobe.io/) in un browser. Seleziona l’account appropriato e verifica che il ruolo aziendale associato sia quello di amministratore di sistema.

1. Crea un progetto con il nome desiderato. Fai clic su **[!UICONTROL Aggiungi API]**.

1. Nella pagina **[!UICONTROL Aggiungi un’API]**, seleziona **[!UICONTROL Experience Cloud]** e **[!UICONTROL Contenuti avanzati]**. Fai clic su **[!UICONTROL Avanti]**.

1. Seleziona **[!UICONTROL Carica la chiave pubblica]**. Fornisci il file del certificato scaricato da [!DNL Experience Manager]. Viene visualizzato il messaggio [!UICONTROL Chiavi pubbliche caricate correttamente]. Fai clic su **[!UICONTROL Avanti]**.

   Nella pagina per la [!UICONTROL creazione di una nuova credenziale dell’account di servizio (JWT)] viene visualizzata la chiave pubblica per l’account di servizio appena configurato.

1. Fai clic su **[!UICONTROL Avanti]**.

1. Nella pagina per la **[!UICONTROL selezione dei profili di prodotto]**, seleziona **[!UICONTROL Servizi di contenuti avanzati]**. Fai clic su **[!UICONTROL Salva API configurata]**.

   In una pagina vengono visualizzate ulteriori informazioni sulla configurazione. Tenete aperta questa pagina per copiare e aggiungere questi valori in [!UICONTROL Impostazioni servizio Smart Tagging Assets] della configurazione cloud in [!DNL Experience Manager] per configurare gli smart tag.

   ![Nella scheda Panoramica, puoi esaminare le informazioni fornite sull’integrazione.](assets/integration_details.png)


   *Figura: Dettagli dell&#39;integrazione in  Adobe Developer Console*

### Configurare il Servizio di contenuti avanzati {#configure-smart-content-service}

Per configurare l&#39;integrazione, utilizzate i valori dei campi [!UICONTROL ID ACCOUNT TECNICO], [!UICONTROL ID ORGANIZZAZIONE], [!UICONTROL CLIENT SECRET] e [!UICONTROL ID CLIENT] dall&#39;integrazione  Developer Console. La creazione di una configurazione cloud di Smart Tags consente l&#39;autenticazione delle richieste API dalla distribuzione [!DNL Experience Manager].

1. In [!DNL Experience Manager], passare a **[!UICONTROL Strumenti]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Cloud Services precedenti]** per aprire la console [!UICONTROL Cloud Services].

1. In **[!UICONTROL Tag avanzati risorse]**, apri la configurazione creata in precedenza. Nella pagina delle impostazioni del servizio, fai clic su **[!UICONTROL Modifica]**.

1. Nella finestra di dialogo **[!UICONTROL Servizio di contenuti avanzati AEM]**, utilizza i valori precompilati per i campi **[!UICONTROL URL servizio]** e **[!UICONTROL Server autorizzazioni]**.

1. Per i campi [!UICONTROL Chiave API], [!UICONTROL ID account tecnico], [!UICONTROL ID organizzazione] e [!UICONTROL Segreto cliente], copiate e utilizzate i seguenti valori generati in [ Integrazione con Developer Console di Adobe](#create-adobe-i-o-integration).

   | [!UICONTROL Impostazioni servizio tag avanzati di Assets] | [!DNL Adobe Developer Console] campi di integrazione |
   |--- |--- |
   | [!UICONTROL Chiave API] | [!UICONTROL ID CLIENT] |
   | [!UICONTROL ID account tecnico] | [!UICONTROL ID ACCOUNT TECNICO] |
   | [!UICONTROL ID organizzazione] | [!UICONTROL ID ORGANIZZAZIONE] |
   | [!UICONTROL Segreto client] | [!UICONTROL SEGRETO CLIENT] |

### Convalidare la configurazione {#validate-the-configuration}

Dopo aver completato la configurazione, puoi usare un MBean JMX per convalidare la configurazione. Per eseguire la convalida, effettua le seguenti operazioni.

1. Accedi al server di [!DNL Experience Manager] all’indirizzo `https://[aem_server]:[port]`.

1. Accedete a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console Web]** per aprire la console OSGi. Fare clic su **[!UICONTROL Principale] > [!UICONTROL JMX]**.

1. Clic `com.day.cq.dam.similaritysearch.internal.impl`. Si apre **[!UICONTROL SimilaritySearch Miscellaneous Tasks]**.

1. Clic `validateConfigs()`. Nella finestra di dialogo **[!UICONTROL Validate Configurations]** (Convalida configurazioni), fai clic su **[!UICONTROL Invoke]** (Richiama).

I risultati della convalida vengono visualizzati nella stessa finestra di dialogo.

### Abilitare i tag avanzati nel flusso di lavoro [!UICONTROL Aggiornamento DAM Asset] (facoltativo) {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. In [!DNL Experience Manager], passare a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.

1. Nella pagina **[!UICONTROL Modelli flusso di lavoro]**, seleziona il modello del flusso di lavoro **[!UICONTROL Risorsa di aggiornamento DAM]**.

1. Fai clic su **[!UICONTROL Modifica]** nella barra degli strumenti.

1. Per visualizzare i passaggi, espandi il pannello laterale. Trascina il passaggio **[!UICONTROL Risorsa di tag avanzati]** della sezione Flusso di lavoro DAM e inseriscilo dopo il passaggio **[!UICONTROL Elabora miniature]**.

   ![Aggiungi il passaggio Risorsa di tag avanzati dopo il passaggio Elabora miniature nel flusso di lavoro Aggiorna risorsa DAM](assets/smart-tag-in-dam-update-asset-workflow.png)

   *Figura: Aggiungi il passaggio Risorsa di tag avanzati dopo il passaggio Elabora miniature nel flusso di lavoro Aggiorna risorsa DAM.*

1. Apri il passaggio in modalità di modifica. In **[!UICONTROL Impostazioni avanzate]**, accertati che sia selezionata l’opzione **[!UICONTROL Avanzamento gestore]**.

   ![Configurare il flusso di lavoro Aggiorna risorsa DAM e aggiungere il passaggio smart tag](assets/smart-tag-step-properties-workflow1.png)


   *Figura: Configurare il flusso di lavoro Aggiorna risorsa DAM e aggiungere il passaggio smart tag*

1. Nella scheda **[!UICONTROL Argomenti]**, seleziona **[!UICONTROL Ignora errori]** se vuoi che il flusso di lavoro venga completato anche con esito negativo del passaggio di assegnazione tag automatica.

   ![Configurare il flusso di lavoro Aggiorna risorsa DAM per aggiungere il passaggio smart tag e selezionare l&#39;avanzamento del gestore](assets/smart-tag-step-properties-workflow2.png)


   *Figura: Configurare il flusso di lavoro Aggiorna risorsa DAM per aggiungere il passaggio smart tag e selezionare l&#39;avanzamento del gestore*

   Per assegnare i tag alle risorse quando vengono caricate, a prescindere dal fatto che l’assegnazione tag avanzati sia abilitata o meno per le cartelle, seleziona **[!UICONTROL Ignora flag di tag avanzati]**.

   ![Configurare il flusso di lavoro Aggiorna risorsa DAM per aggiungere il passo smart tag e selezionare Ignora flag Smart Tag](assets/smart-tag-step-properties-workflow3.png)


   *Figura: Configurare il flusso di lavoro Aggiorna risorsa DAM per aggiungere il passo smart tag e selezionare Ignora flag Smart Tag*

1. Fai clic su **[!UICONTROL OK]** per chiudere il passaggio del processo, quindi salva il flusso di lavoro.

## Train the Smart Content Service {#training-the-smart-content-service}

Affinché Smart Content Service riconosca la tassonomia aziendale, eseguitela su un set di risorse che già includono tag rilevanti per la vostra attività. Per assegnare tag efficaci alle immagini del tuo marchio, Smart Content Service richiede che le immagini di formazione siano conformi a determinate linee guida. Dopo la formazione, il servizio può applicare la stessa tassonomia a un set di risorse simile.

È possibile formare il servizio più volte per migliorarne la capacità di applicare tag rilevanti. Dopo ogni ciclo di formazione, eseguite un flusso di lavoro con tag e verificate che le risorse dispongano dei tag appropriati.

Potete addestrare Smart Content Service periodicamente o su richiesta.

>[!NOTE]
>
>Il flusso di lavoro di formazione viene eseguito solo sulle cartelle.

### Linee guida per la formazione {#guidelines-for-training}

Per risultati ottimali, le immagini del set di formazione devono essere conformi alle seguenti linee guida:

**Quantity and size (Quantità e dimensioni)**: almeno 30 immagini per tag. Almeno 500 pixel sul lato più lungo.

**Coerenza**: Le immagini di un tag devono essere visivamente simili.

Ad esempio, non è consigliabile assegnare a tutte queste immagini il tag `my-party` (per la formazione) perché non sono visivamente simili.

![Immagini illustrative per esemplificare le linee guida per la formazione](/help/assets/assets/do-not-localize/coherence.png)

**Copertura**: Dovrebbe esserci una varietà sufficiente nelle immagini della formazione. L&#39;idea è quella di fornire alcuni esempi, ma abbastanza diversi, in modo che  Experience Manager impari a concentrarsi sulle cose giuste. Se applicate lo stesso tag a immagini visivamente diverse, includete almeno cinque esempi di ciascun tipo.

Ad esempio, per il tag *model-down-pose*, includete più immagini di formazione simili all&#39;immagine evidenziata di seguito per il servizio, in modo da identificare le immagini simili con maggiore precisione durante l&#39;assegnazione dei tag.

![Immagini illustrative per esemplificare le linee guida per la formazione](/help/assets/assets/do-not-localize/coverage_1.png)

**Distrazione/ostruzione**: Il servizio si allena meglio sulle immagini con meno distrazioni (sfondi visibili, accompagnamento indipendenti, come oggetti/persone con il soggetto principale).

Ad esempio, per il tag *casual-shoe*, la seconda immagine non è un buon candidato alla formazione.

![Immagini illustrative per esemplificare le linee guida per la formazione](/help/assets/assets/do-not-localize/distraction.png)

**Completeness (Completezza):** se un’immagine è idonea per più tag, aggiungi tutti i tag applicabili prima di includere l’immagine nella formazione. Ad esempio, per tag quali `raincoat` e `model-side-view`, aggiungi entrambi i tag alla risorsa idonea prima di includerla nella formazione.

![Immagini illustrative per esemplificare le linee guida per la formazione](/help/assets/assets/do-not-localize/completeness.png)

>[!NOTE]
>
>La capacità di Smart Content Service di formare i tag e applicarli ad altre immagini dipende dalla qualità delle immagini utilizzate per la formazione. Per risultati ottimali,  Adobe consiglia di usare immagini visivamente simili per formare il servizio per ciascun tag.

### Formazione periodica {#periodic-training}

Potete abilitare Smart Content Service per l&#39;addestramento periodico delle risorse e dei tag associati all&#39;interno di una cartella. Aprite la pagina [!UICONTROL Proprietà] della cartella di risorse, selezionate **[!UICONTROL Abilita tag avanzati]** nella scheda **[!UICONTROL Dettagli]** e salvate le modifiche.

![enable_smart_tags](assets/enable_smart_tags.png)

Quando questa opzione è selezionata per una cartella, [!DNL Experience Manager] esegue automaticamente un flusso di lavoro di formazione per formare Smart Content Service sulle risorse delle cartelle e i relativi tag. Per impostazione predefinita, il flusso di lavoro della formazione viene eseguito settimanalmente alle 12:30 del sabato.

### Formazione su richiesta {#on-demand-training}

Potete addestrare Smart Content Service quando necessario dalla console Flusso di lavoro.

1. Nell&#39;interfaccia [!DNL Experience Manager], passare a **[!UICONTROL Strumenti]** > **[!UICONTROL Workflow]** > **[!UICONTROL Modelli]**.
1. Dalla pagina **[!UICONTROL Modelli di workflow]**, selezionare il flusso di lavoro **[!UICONTROL Formazione tag avanzati]**, quindi fare clic su **[!UICONTROL Avvia flusso di lavoro]** dalla barra degli strumenti.
1. Nella finestra di dialogo **[!UICONTROL Esegui flusso di lavoro]**, individuate la cartella payload che include le risorse con tag per la formazione del servizio.
1. Specificate un titolo per il flusso di lavoro e un commento. Quindi, fare clic su **[!UICONTROL Esegui]**. Le risorse e i tag vengono inviati per la formazione.

   ![workflow_dialog](assets/workflow_dialog.png)

>[!NOTE]
>
>Una volta che le risorse di una cartella vengono elaborate per la formazione, solo le risorse modificate vengono elaborate nei cicli di formazione successivi.

### Visualizzare i rapporti sulla formazione {#viewing-training-reports}

Per verificare se Smart Content Service è addestrato sui tag presenti nel set di risorse di formazione, controllate il rapporto sul flusso di lavoro di formazione dalla console Rapporti.

1. Nell&#39;interfaccia [!DNL Experience Manager], passare a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Rapporti]**.
1. Nella pagina **[!UICONTROL Report risorse]**, fate clic su **[!UICONTROL Crea]**.
1. Selezionare il report **[!UICONTROL Smart Tags Training]**, quindi fare clic su **[!UICONTROL Next]** dalla barra degli strumenti.
1. Specifica un titolo e una descrizione per il rapporto. In **[!UICONTROL Pianifica rapporto]**, lascia selezionata l’opzione **[!UICONTROL Now (Ora)]**. Se vuoi pianificare il rapporto per un momento successivo, seleziona **[!UICONTROL Later (Più tardi)]** e specifica una data e un’ora. Quindi, fare clic su **[!UICONTROL Crea]** dalla barra degli strumenti.
1. Nella pagina **[!UICONTROL Rapporti su risorse]**, seleziona il rapporto generato. Per visualizzare il rapporto, fare clic su **[!UICONTROL Visualizza]** nella barra degli strumenti.
1. Rivedete i dettagli del rapporto.

   Il rapporto mostra lo stato di formazione per i tag che hai appreso. La presenza del colore verde nella colonna **[!UICONTROL Training Status (Stato formazione)]** indica che per il tag è stato eseguito il training del servizio di contenuti avanzati. Se invece del verde è presente il colore giallo, il training del servizio di contenuti avanzati non è stato completato per un tag specifico. In questo caso, aggiungi altre immagini che contengono il tag in questione ed esegui il flusso di lavoro di formazione per completare il training del servizio per quel tag.

   Se non visualizzate i tag nel rapporto, eseguite nuovamente il flusso di lavoro di formazione per questi tag.

1. Per scaricare il rapporto, selezionatelo dall&#39;elenco e fate clic su **[!UICONTROL Scarica]** dalla barra degli strumenti. Il rapporto viene scaricato come foglio di calcolo di Microsoft Excel.

## Limitazioni  {#limitations}

* Gli smart tag avanzati si basano su modelli di apprendimento delle immagini e dei relativi tag. Questi modelli non sempre sono perfetti per identificare i tag. La versione corrente di Smart Content Service presenta i seguenti limiti:

   * Incapacità di riconoscere sottili differenze nelle immagini. Ad esempio, camicie sottili o regolari.
   * Impossibile identificare i tag in base a piccoli pattern/parti di un’immagine. Ad esempio, i logo delle T-shirt.
   * I tag sono supportati nelle impostazioni internazionali in cui [!DNL Experience Manager] è supportato. Per un elenco delle lingue, vedere [Note sulla versione di Smart Content Services](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/smart-content-service-release-notes.html).

* Per cercare risorse con smart tag (regolari o migliorati), utilizzate la ricerca Omnisearch (ricerca full-text). [!DNL Assets] Non esiste un predicato di ricerca separato per gli smart tag.

>[!MORELIKETHIS]
>
>* [Panoramica e come formare i tag avanzati](enhanced-smart-tags.md)
>* [Esercitazione video sugli smart tag](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html)

