---
title: Integrare  Adobe Sign con  AEM Forms
seo-title: Integrare  Adobe Sign con  AEM Forms
description: Scoprite come configurare  Adobe Sign per  AEM Forms
seo-description: Scoprite come configurare  Adobe Sign per  AEM Forms
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
translation-type: tm+mt
source-git-commit: c451948c43004d084bc3fce7a2c6ad99381f1ea8
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 0%

---


# Integrare [!DNL Adobe Sign] con AEM [!DNL Forms]{#integrate-adobe-sign-with-aem-forms}

[!DNL Adobe Sign] abilita flussi di lavoro di firma elettronica per i moduli adattivi. Le firme elettroniche migliorano i flussi di lavoro per l&#39;elaborazione di documenti per scopi legali, di vendita, di retribuzione, di gestione delle risorse umane e per molte altre aree.

In uno scenario di moduli [!DNL Adobe Sign] e adattivi tipico, un utente compila un modulo adattivo per **richiedere un servizio**. Ad esempio, un&#39;applicazione con carta di credito e un benefit per i cittadini vengono modulo. Quando un utente compila, invia e firma il modulo di domanda, il modulo viene inviato al provider di servizi per ulteriori azioni. Il provider di servizi controlla l&#39;applicazione e utilizza [!DNL Adobe Sign] per contrassegnare l&#39;applicazione approvata. Per abilitare flussi di lavoro di firma elettronica simili, è possibile integrare [!DNL Adobe Sign] con AEM [!DNL Forms].

Per utilizzare [!DNL Adobe Sign] con AEM [!DNL Forms], configura [!DNL Adobe Sign] nei servizi di AEM Cloud:

## Prerequisiti {#prerequisites}

Per integrare [!DNL Adobe Sign] con AEM [!DNL Forms] è necessario disporre di quanto segue:

* Un account sviluppatore [ Adobe Sign attivo.](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* Un server [SSL abilitato](/help/sites-administering/ssl-by-default.md) AEM [!DNL Forms].
* Un&#39;applicazione [ Adobe Sign API](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* Credenziali (ID client e Segreto cliente) dell&#39;applicazione [!DNL Adobe Sign] API.
* Durante la riconfigurazione, rimuovete la configurazione [!DNL Adobe Sign] esistente dalle istanze di creazione e pubblicazione.
* Utilizzate la chiave di crittografia [identica](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) per le istanze di creazione e pubblicazione.

## Configurare [!DNL Adobe Sign] con AEM [!DNL Forms] {#configure-adobe-sign-with-aem-forms}

Dopo aver creato i prerequisiti, eseguite i seguenti passaggi per configurare [!DNL Adobe Sign] con AEM [!DNL Forms] nell&#39;istanza Author:

1. Nell&#39;istanza di creazione AEM [!DNL Forms], andate a **Strumenti** ![martello](assets/hammer.png) > **[!UICONTROL Generale]** > **[!UICONTROL Browser di configurazione]**.
1. Nella pagina **[!UICONTROL Configuration Browser]**, toccare **[!UICONTROL Create]**.
   * Per ulteriori informazioni, consulta la documentazione del [browser di configurazione](/help/sites-administering/configurations.md).
1. Nella finestra di dialogo **[!UICONTROL Crea configurazione]**, specificate un **[!UICONTROL Titolo]** per la configurazione, abilitate **[!UICONTROL Configurazioni cloud]** e toccate **[!UICONTROL Crea]**. Crea un contenitore di configurazione per i servizi cloud.
1. Andate su **Strumenti** ![martello](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]** e selezionate il contenitore di configurazione creato nel passaggio precedente.

   >[!NOTE]
   >
   >È possibile eseguire i passaggi da 1 a 4 per creare un nuovo contenitore di configurazione e creare una configurazione [!DNL Adobe Sign] nel contenitore oppure utilizzare la cartella `global` esistente in **Strumenti** ![martello](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. Se si crea la configurazione nel nuovo contenitore di configurazione, assicurarsi di specificare il nome del contenitore nel campo **[!UICONTROL Contenitore di configurazione]** al momento della creazione di un modulo adattivo.

   >[!NOTE]
   Assicurati che l&#39;URL della pagina di configurazione dei servizi cloud inizi con **HTTPS**. In caso contrario, [abilitare SSL](/help/sites-administering/ssl-by-default.md) per AEM server [!DNL Forms].

1. Nella pagina di configurazione, toccare **[!UICONTROL Crea]** per creare la configurazione [!DNL Adobe Sign] in AEM [!DNL Forms].
1. Nella scheda **[!UICONTROL Generale]** della pagina **[!UICONTROL Crea  configurazione Adobe Sign]**, specificare un **[!UICONTROL Nome]** per la configurazione e toccare **[!UICONTROL Avanti]**. Facoltativamente potete specificare un titolo e cercare per selezionare una miniatura per la configurazione.

1. Copiate l’URL nella finestra del browser corrente su un blocco note. È necessario configurare l&#39;applicazione [!DNL Adobe Sign] con AEM[!DNL Forms].

1. Configurare le impostazioni OAuth per l&#39;applicazione [!DNL Adobe Sign]:

   1. Aprite una finestra del browser ed effettuate l&#39;accesso all&#39;account sviluppatore [!DNL Adobe Sign].
   1. Selezionare l&#39;applicazione configurata per AEM [!DNL Forms] e toccare **[!UICONTROL Configura OAuth per applicazione]**.
   1. Copiare l&#39; **[!UICONTROL ID client]** e **[!UICONTROL Segreto cliente]** su un blocco note.
   1. Nella casella **[!UICONTROL URL di reindirizzamento]**, aggiungere l&#39;URL HTTPS copiato nel passaggio precedente.
   1. Abilitare le seguenti impostazioni OAuth per l&#39;applicazione [!DNL Adobe Sign] e fare clic su **[!UICONTROL Salva]**.
   * aggrement_read
   * aggrement_write
   * aggrement_send
   * widget_write
   * workflow_read

   Per informazioni dettagliate su come configurare le impostazioni OAuth per un&#39;applicazione [!DNL Adobe Sign] e ottenere le chiavi, vedere [Configurare le impostazioni di autenticazione per la documentazione per gli sviluppatori dell&#39;applicazione](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md).

   ![Configurazione OAuth](assets/oauthconfig_new.png)

1. Torna alla pagina **[!UICONTROL Crea  configurazione Adobe Sign]**. Nella scheda **[!UICONTROL Impostazioni]**, il campo **[!UICONTROL URL OAuth]** indica il seguente URL predefinito:

   https://secure.na1.echosign.com/public/oauth

   dove:

   **na1** fa riferimento alla condivisione di database predefinita.

   È possibile modificare il valore per la condivisione del database. Riavviate il server per poter utilizzare il nuovo valore per la condivisione del database.

   >[!NOTE]
   Verificate che le configurazioni dell’istanza di creazione e pubblicazione puntino alla stessa condivisione. Se create più configurazioni Adobe Sign  per un&#39;organizzazione, accertatevi che tutte le configurazioni utilizzino la stessa condivisione.

1. Specificate l&#39; **ID client** (altrimenti denominato ID applicazione) e il **Segreto client** copiato al punto 8. Selezionare l&#39;opzione **[!UICONTROL Abilita  Adobe Sign per gli allegati anche]** per aggiungere i file allegati a un modulo adattivo al documento [!DNL Adobe Sign] corrispondente inviato per la firma.

   Toccate **[!UICONTROL Connetti a  Adobe Sign]**. Quando viene richiesto di specificare le credenziali, specificare il nome utente e la password dell&#39;account utilizzato durante la creazione dell&#39;applicazione [!DNL Adobe Sign].

   Toccate **[!UICONTROL Crea]** per creare la configurazione [!DNL Adobe Sign].

1. Apri AEM console Web. L&#39;URL è `https://'[server]:[port]'/system/console/configMgr`
1. Aprire **[!UICONTROL Forms Common Configuration Service].**
1. Nel campo **[!UICONTROL Consenti]**, **selezionare** Tutti gli utenti - Tutti gli utenti, anonimi o connessi, possono visualizzare in anteprima gli allegati, verificare e firmare i moduli, quindi fare clic su **[!UICONTROL Salva].** L&#39;istanza Author è configurata per l&#39;utilizzo  [!DNL Adobe Sign].
1. Pubblicate la configurazione.
1. Utilizzate [replica](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/replication.html) per creare una configurazione identica sulle istanze di pubblicazione corrispondenti.

Ora, [!DNL Adobe Sign] è integrato con AEM [!DNL Forms] ed è pronto per essere utilizzato nei moduli adattivi. Per [utilizzare  servizio Adobe Sign in un modulo adattivo](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form), specificare il contenitore di configurazione creato sopra nelle proprietà del modulo adattivo.



## Configurare l&#39;utilità di pianificazione [!DNL Adobe Sign] per sincronizzare lo stato di firma {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Un modulo adattivo abilitato per [!DNL Adobe Sign] viene inviato solo dopo che tutti i firmatari avranno completato il processo di firma. Per impostazione predefinita, i servizi di pianificazione [!DNL Adobe Sign] sono programmati per controllare (sondaggio) la risposta del firmatario dopo ogni 24 ore. È possibile modificare l&#39;intervallo predefinito per l&#39;ambiente. Per modificare l’intervallo predefinito, effettuate le seguenti operazioni:

1. Accedete al AEM [!DNL Forms] server con credenziali di amministratore e andate a **Strumenti** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console Web]**.

   Potete anche aprire il seguente URL in una finestra del browser:
   `https://[localhost]:'port'/system/console/configMgr`

1. Individuate e aprite l&#39;opzione **[!UICONTROL Adobe Sign Configuration Service]**. Specificate un&#39;espressione [cron](https://en.wikipedia.org/wiki/Cron#CRON_expression) nel campo **[!UICONTROL Status Update Scheduler Expression]** e fate clic su **[!UICONTROL Save]**. Ad esempio, per eseguire il servizio di configurazione ogni giorno alle 00:00, specificare `0 0 0 1/1 * ? *` nel campo **[!UICONTROL Espressione pianificazione aggiornamento stato]**.

L&#39;intervallo predefinito per la sincronizzazione dello stato di [!DNL Adobe Sign] ora viene modificato.

## Articoli correlati {#related-articles}

* [Utilizzo di  Adobe Sign in un modulo adattivo](../../forms/using/working-with-adobe-sign.md)
* [Utilizzo  Adobe Sign con  AEM Forms (video)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
* [Integrare  Adobe Sign con  AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)

