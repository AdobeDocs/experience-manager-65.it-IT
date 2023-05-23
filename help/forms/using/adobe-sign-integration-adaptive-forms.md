---
title: Integrare Adobe Sign con AEM Forms
seo-title: Integrate Adobe Sign with AEM Forms
description: Scopri come configurare Adobe Sign per AEM Forms
seo-description: Learn how to configure Adobe Sign for AEM Forms
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
feature: Adaptive Forms, Acrobat Sign
exl-id: 52146038-1582-41b8-aee0-215d04bb91d7
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 1%

---

# Integrare [!DNL Adobe Sign] con AEM [!DNL Forms]{#integrate-adobe-sign-with-aem-forms}

[!DNL Adobe Sign] abilita i flussi di lavoro di firma elettronica per i moduli adattivi. Le firme elettroniche consentono di migliorare i flussi di lavoro per l&#39;elaborazione di documenti relativi a questioni legali, vendite, retribuzioni, gestione delle risorse umane e molte altre aree.

In un tipico [!DNL Adobe Sign] e di moduli adattivi, un utente compila un modulo adattivo in **richiedere un servizio**. Ad esempio, la richiesta di una carta di credito e il modulo relativo ai benefit per i cittadini. Quando un utente compila, invia e firma il modulo di richiesta, questo viene inviato al fornitore di servizi per ulteriori azioni. Il provider di servizi esamina l&#39;applicazione e utilizza [!DNL Adobe Sign] per contrassegnare la domanda approvata. Per abilitare flussi di lavoro di firma elettronica simili, puoi integrare [!DNL Adobe Sign] con AEM [!DNL Forms].

Da utilizzare [!DNL Adobe Sign] con AEM [!DNL Forms], configura [!DNL Adobe Sign] in AEM Cloud Services:

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
1. Il giorno **[!UICONTROL Browser configurazioni]** pagina, tocca **[!UICONTROL Crea]**.
   * Consulta la [Browser configurazioni](/help/sites-administering/configurations.md) per ulteriori informazioni.
1. In **[!UICONTROL Crea configurazione]** , specifica un **[!UICONTROL Titolo]** per la configurazione, abilita **[!UICONTROL Configurazioni cloud]**, e tocca **[!UICONTROL Crea]**. Crea un contenitore di configurazione per i servizi cloud.
1. Accedi a **Strumenti** ![martello](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]** e seleziona il contenitore di configurazione creato nel passaggio precedente.

   >[!NOTE]
   >
   >Puoi eseguire i passaggi 1-4 per creare un nuovo contenitore di configurazione e un [!DNL Adobe Sign] nel contenitore o utilizza il file esistente `global` cartella in **Strumenti** ![martello](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. Se crei la configurazione nel nuovo contenitore di configurazione, assicurati di specificare il nome del contenitore nel **[!UICONTROL Contenitore configurazione]** quando crei un modulo adattivo.

   >[!NOTE]
   Assicurati che l’URL della pagina di configurazione dei servizi cloud inizi con **HTTPS**. In caso contrario, [abilita SSL](/help/sites-administering/ssl-by-default.md) per AEM [!DNL Forms] server.

1. Nella pagina di configurazione, tocca **[!UICONTROL Crea]** per creare [!DNL Adobe Sign] configurazione in AEM [!DNL Forms].
1. In **[!UICONTROL Generale]** scheda di **[!UICONTROL Crea configurazione Adobe Sign]** , specificare un **[!UICONTROL Nome]** per la configurazione e tocca **[!UICONTROL Successivo]**. Facoltativamente, puoi specificare un titolo e cercare la miniatura da configurare.

1. Copiare l&#39;URL nella finestra del browser corrente in un blocco note. È necessario per configurare [!DNL Adobe Sign] applicazione con AEM[!DNL Forms].

1. In **[!UICONTROL Impostazioni]** , la scheda **[!UICONTROL URL OAuth]** contiene l’URL predefinito. Il formato dell’URL è:

   `https://<shard>/public/oAuth/v2`

   Ad esempio:
   `https://secure.na1.echosign.com/public/oauth/v2`

   Dove:

   **na1** fa riferimento alla partizione di database predefinita. È possibile modificare il valore della partizione del database. Assicurati che [!DNL  Adobe Sign] Le configurazioni cloud puntano al [partitura corretta](https://helpx.adobe.com/sign/using/identify-account-shard.html).

   Se ne crei un altro [!DNL Adobe Sign] per una funzione o un componente di Adobe Experience Manager, assicurati che tutte le [!DNL Adobe Sign] Le configurazioni cloud puntano alla stessa partizione.

   >[!NOTE]
   Mantieni **Crea configurazione Adobe Sign** pagina aperta. Non chiuderlo. Puoi recuperare **ID client** e **Segreto client** dopo aver configurato le impostazioni OAuth per [!DNL Adobe Sign] come descritto nei passaggi successivi.


1. Configurare le impostazioni OAuth per [!DNL Adobe Sign] applicazione:

   1. Apri una finestra del browser e accedi al [!DNL Adobe Sign] account sviluppatore.
   1. Seleziona l’applicazione configurata per AEM [!DNL Forms], e tocca **[!UICONTROL Configurare OAuth per l’applicazione]**.
   1. Copia il **[!UICONTROL ID client]** e **[!UICONTROL Segreto client]** in un blocco note.
   1. In **[!UICONTROL URL di reindirizzamento]** , aggiungi l’URL HTTPS copiato nel passaggio precedente.
   1. Abilita le seguenti impostazioni OAuth per [!DNL Adobe Sign] e fare clic su **[!UICONTROL Salva]**.
   * accordo_lettura
   * accordo_scrittura
   * accord_send
   * widget_write
   * workflow_read

   Per informazioni dettagliate su come configurare le impostazioni OAuth per un [!DNL Adobe Sign] e ottenere le chiavi, consulta [Configurare le impostazioni OAuth per l&#39;applicazione](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md) documentazione per gli sviluppatori.

   ![Configurazione OAuth](assets/oauthconfig_new.png)

1. Torna a **[!UICONTROL Crea configurazione Adobe Sign]** pagina. In **[!UICONTROL Impostazioni]** , la scheda **[!UICONTROL URL OAuth]** nel campo è indicato l’URL predefinito. Il formato dell’URL è:

   `https://<shard>/public/oAuth/v2`

   Ad esempio:
   `https://secure.na1.echosign.com/public/oauth/v2`

   Dove:

   **na1** fa riferimento alla partizione di database predefinita.

   È possibile modificare il valore della partizione del database. Riavviare il server per poter utilizzare il nuovo valore per la partizione del database.

   >[!NOTE]
   Assicurati che le configurazioni dell’istanza di authoring e pubblicazione puntino alla stessa partizione. Se crei più configurazioni di Adobe Sign per un’organizzazione, assicurati che tutte le configurazioni utilizzino la stessa condivisione.

1. Torna a **[!UICONTROL Crea configurazione Adobe Sign]** pagina. In **[!UICONTROL Impostazioni]** , specificare **ID client** (indicato anche come ID applicazione) e **Segreto client**. Utilizza il [ID client e segreto client dell’applicazione Adobe Sign](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) creato per AEM Forms.

1. Seleziona la **[!UICONTROL Abilita Adobe Sign anche per gli allegati]** opzione per aggiungere i file allegati a un modulo adattivo al [!DNL Adobe Sign] documento inviato per la firma.

1. Tocca **[!UICONTROL Connettersi ad Adobe Sign]**. Quando vengono richieste le credenziali, specifica il nome utente e la password dell’account utilizzato durante la creazione [!DNL Adobe Sign] applicazione.

1. Tocca **[!UICONTROL Crea]** per creare [!DNL Adobe Sign] configurazione.

1. Apri la console web AEM. L’URL è `https://'[server]:[port]'/system/console/configMgr`
1. Apri **[!UICONTROL Servizio di configurazione comune di Forms].**
1. In **[!UICONTROL Consenti]** campo, **seleziona** Tutti gli utenti: tutti gli utenti, anonimi o connessi, possono visualizzare in anteprima gli allegati, verificare e firmare i moduli e fare clic su **[!UICONTROL Salva].** L’istanza di authoring è configurata per utilizzare [!DNL Adobe Sign].
1. Pubblica la configurazione.
1. Utilizzare [replica](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html?lang=it) per creare una configurazione identica sulle istanze di pubblicazione corrispondenti.

Ora, [!DNL Adobe Sign] è integrato con l’AEM [!DNL Forms] e pronti per essere utilizzati nei moduli adattivi. A [utilizzare il servizio Adobe Sign in un modulo adattivo](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form), specifica il contenitore di configurazione creato in precedenza nelle proprietà dei moduli adattivi.



## Configura [!DNL Adobe Sign] per sincronizzare lo stato della firma {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Un [!DNL Adobe Sign] il modulo adattivo abilitato viene inviato solo dopo che tutti i firmatari hanno completato il processo di firma. Per impostazione predefinita, il [!DNL Adobe Sign] È pianificato che i servizi di pianificazione controllino la risposta del firmatario (polling) ogni 24 ore. È possibile modificare l’intervallo predefinito per l’ambiente. Per modificare l’intervallo predefinito, effettua le seguenti operazioni:

1. Accedere a AEM [!DNL Forms] server con credenziali di amministratore e passa a **Strumenti** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console web]**.

   Puoi anche aprire il seguente URL in una finestra del browser:
   `https://[localhost]:'port'/system/console/configMgr`

1. Individuare e aprire **[!UICONTROL Servizio di configurazione Adobe Sign]** opzione. Specifica un [espressione cron](https://en.wikipedia.org/wiki/Cron#CRON_expression) nel **[!UICONTROL Espressione modulo di pianificazione aggiornamento stato]** e fai clic su **[!UICONTROL Salva]**. Ad esempio, per eseguire il servizio di configurazione ogni giorno alle 00:00, specifica `0 0 0 1/1 * ? *` nel **[!UICONTROL Espressione modulo di pianificazione aggiornamento stato]** campo.

Intervallo predefinito per lo stato di sincronizzazione di [!DNL Adobe Sign] è stato modificato.

## Articoli correlati {#related-articles}

* [Utilizzo di Adobe Sign in un modulo adattivo](../../forms/using/working-with-adobe-sign.md)
* [Utilizzo di Adobe Sign con AEM Forms (video)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
