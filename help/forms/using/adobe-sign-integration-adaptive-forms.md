---
title: Integrazione di Adobe Sign con i AEM Forms
seo-title: Integrazione di Adobe Sign con i AEM Forms
description: Scopri come configurare Adobe Sign per AEM Forms
seo-description: Scopri come configurare Adobe Sign per AEM Forms
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
translation-type: tm+mt
source-git-commit: bd70508b361ac8b62ebc0344538a18369a075f3e
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---


# Integrazione di Adobe Sign con i AEM Forms{#integrate-adobe-sign-with-aem-forms}

Adobe Sign consente flussi di lavoro di firma elettronica per i moduli adattivi. Le firme elettroniche migliorano i flussi di lavoro per l&#39;elaborazione di documenti per scopi legali, di vendita, di retribuzione, di gestione delle risorse umane e per molte altre aree.

In uno scenario di moduli adattivi e Adobe Sign tipico, l&#39;utente compila un modulo adattivo da **richiedere per un servizio**. Ad esempio, un&#39;applicazione con carta di credito e un benefit per i cittadini vengono modulo. Quando un utente compila, invia e firma il modulo di domanda, il modulo viene inviato al provider di servizi per ulteriori azioni. Il fornitore di servizi controlla l’applicazione e utilizza Adobe Sign per contrassegnare l’applicazione approvata. Per abilitare flussi di lavoro di firma elettronica simili, è possibile integrare Adobe Sign con i AEM Forms.

Per utilizzare Adobe Sign con i AEM Forms, configurare i AEM cloud services di accesso di Adobe Sign:

## Prerequisiti {#prerequisites}

Per integrare Adobe Sign con i AEM Forms, è necessario disporre di quanto segue:

* Un account sviluppatore [Adobe Sign attivo.](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* Un server AEM Forms abilitato [per](/help/sites-administering/ssl-by-default.md) SSL.
* Un&#39;applicazione [API](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md)Adobe Sign.
* Credenziali (ID client e Segreto cliente) dell’applicazione API Adobe Sign.

## Configurare Adobe Sign con i AEM Forms {#configure-adobe-sign-with-aem-forms}

Dopo aver creato i prerequisiti, effettuare le seguenti operazioni per configurare Adobe Sign con AEM Forms nell&#39;istanza Author:

1. Nell’istanza di creazione AEM Forms, andate a **Strumenti** ![a martello](assets/hammer.png) > **Generale** > **Browser** di configurazione.
1. Nella pagina del browser **[!UICONTROL di]** configurazione, toccate **[!UICONTROL Crea]**.
1. Nella finestra di dialogo **[!UICONTROL Crea configurazione]** , specificate un **[!UICONTROL titolo]** per la configurazione, abilitate le configurazioni **** Cloud e toccate **[!UICONTROL Crea]**. Crea un contenitore di configurazione per i servizi cloud.
1. Passa a **Strumenti** ![a martello](assets/hammer.png) > Servizi **** cloud > **Adobe Sign** e seleziona il contenitore di configurazione creato nel passaggio precedente.

   >[!NOTE]
   >
   >Assicurati che l&#39;URL della pagina di configurazione dei servizi cloud inizi con **HTTPS**. In caso contrario, [abilita SSL](/help/sites-administering/ssl-by-default.md) per il server AEM Forms.

1. Nella pagina di configurazione, tocca **[!UICONTROL Crea]** per creare la configurazione di Adobe Sign in AEM Forms.
1. Nella scheda **[!UICONTROL Generale]** della pagina **[!UICONTROL Crea configurazione]** Adobe Sign, specificare un **nome** per la configurazione e toccare **Avanti**. Facoltativamente potete specificare un titolo e cercare per selezionare una miniatura per la configurazione.

   Copiate l’URL nella finestra del browser corrente. È necessario configurare l’applicazione Adobe Sign con AEM Forms.

1. Configurare le impostazioni OAuth per l’applicazione Adobe Sign:

   1. Apri una finestra del browser ed effettua l’accesso all’account sviluppatore Adobe Sign.
   1. Selezionate l&#39;applicazione configurata per i AEM Forms e toccate Configura OAuth per l&#39;applicazione.
   1. Nella casella URL **di** reindirizzamento, aggiungete l’URL HTTPS copiato nel passaggio precedente e fate clic su **Salva**.
   1. Abilita le seguenti impostazioni OAuth per l’applicazione Adobe Sign e fai clic su **Salva**.
   * aggrement_read
   * aggrement_write
   * aggrement_send
   * widget_write
   * workflow_read

   Per informazioni dettagliate su come configurare le impostazioni OAuth per un’applicazione Adobe Sign e ottenere le chiavi, consultare la documentazione [Configurare le impostazioni di autenticazione per lo sviluppatore dell’applicazione](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobeio/adobeio-documentation/master/sign/gstarted/configure_oauth.md) .

   ![Configurazione OAuth](assets/oauthconfig_new.png)

1. Torna alla pagina **Crea configurazione** Adobe Sign. Nella scheda **[!UICONTROL Impostazioni]** , il campo URL **** OAuth fa riferimento al seguente URL predefinito:

   https://secure.na1.echosign.com/public/oauth

   dove:

   **na1** fa riferimento alla condivisione di database predefinita.

   È possibile modificare il valore per la condivisione del database. Riavviate il server per poter utilizzare il nuovo valore per la condivisione del database.

1. Specificate l&#39;ID **** client (altrimenti denominato ID applicazione) e il segreto **** client. Selezionare l&#39;opzione **Abilita Adobe Sign per gli allegati anche** per aggiungere i file allegati a un modulo adattivo al documento Adobe Sign corrispondente inviato per la firma.

   Tap **[!UICONTROL Connect to Adobe Sign]**. Quando viene richiesto di fornire le credenziali, specificare il nome utente e la password dell&#39;account utilizzato durante la creazione dell&#39;applicazione Adobe Sign.

   Tocca **[!UICONTROL Crea]** per creare la configurazione di Adobe Sign.

1. Aprite la console Web di AEM. L&#39;URL è `https://'[server]:[port]'/system/console/configMgr`
1. Aprire **Forms Common Configuration Service.**
1. Nel campo **Consenti** , **selezionare** Tutti gli utenti - Tutti gli utenti, anonimi o connessi, possono visualizzare in anteprima gli allegati, verificare e firmare i moduli e fare clic su **Salva.** L’istanza Author è configurata per l’utilizzo di Adobe Sign.
1. Nell’istanza [Pubblica](/help/sites-deploying/deploy.md) , effettuate l’accesso e aprite il seguente URL:

   `https://<server-name>:<port>/libs/granite/configurations/content/view.html/conf`

1. Ripetere i passaggi da 1 a 12 per configurare Adobe Sign con AEM Forms. Utilizzate lo stesso titolo per la configurazione (come specificato al punto 3) e lo stesso nome (come specificato al punto 6) per replicare le impostazioni configurate nell&#39;istanza Author.

   Adobe Sign è ora integrato con i AEM Forms e può essere utilizzato nei moduli adattivi. Per [utilizzare il servizio Adobe Sign in un modulo](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form)adattivo, specificare il contenitore di configurazione creato sopra nelle proprietà del modulo adattivo.

## Configurare l’utilità di pianificazione di Adobe Sign per sincronizzare lo stato di firma {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Un modulo adattivo abilitato per Adobe Sign viene inviato solo dopo che tutti i firmatari avranno completato il processo di firma. Per impostazione predefinita, i servizi di pianificazione di Adobe Sign sono programmati per controllare (sondaggio) la risposta del firmatario dopo ogni 24 ore. È possibile modificare l&#39;intervallo predefinito per l&#39;ambiente. Per modificare l’intervallo predefinito, effettuate le seguenti operazioni:

1. Accedete al server AEM Forms con le credenziali di amministratore e andate a **Strumenti** > **Operazioni** > Console **** Web.

   Potete anche aprire il seguente URL in una finestra del browser:
   `https://[localhost]:'port'/system/console/configMgr`

1. Individuare e aprire l&#39;opzione **Adobe Sign Configuration Service** . Specificate un&#39;espressione [cron nel campo Espressione](https://en.wikipedia.org/wiki/Cron#CRON_expression) Utilità di pianificazione **Aggiornamento stato e fate clic su** Salva ****. Ad esempio, per eseguire il servizio di configurazione ogni giorno alle 00:00, specificate `0 0 0 1/1 * ? *` nel campo Espressione **Utilità di pianificazione aggiornamento** stato.

L&#39;intervallo predefinito per la sincronizzazione dello stato di Adobe Sign ora viene modificato.

## Related Articles {#related-articles}

* [Utilizzo di Adobe Sign in un modulo adattivo](../../forms/using/working-with-adobe-sign.md)
* [Utilizzo di Adobe Sign con AEM Forms (video)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
* [Integrazione di Adobe Sign con i AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)

