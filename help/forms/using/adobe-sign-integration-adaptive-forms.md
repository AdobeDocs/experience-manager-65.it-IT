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
source-git-commit: 6eb6ea86c5544329be5cb28500c59c632ccc9639
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 0%

---


# Integrare  Adobe Sign con  AEM Forms{#integrate-adobe-sign-with-aem-forms}

 Adobe Sign consente flussi di lavoro di firma elettronica per i moduli adattivi. Le firme elettroniche migliorano i flussi di lavoro per l&#39;elaborazione di documenti per scopi legali, di vendita, di retribuzione, di gestione delle risorse umane e per molte altre aree.

In uno scenario di moduli Adobe Sign  e adattivi tipico, un utente compila un modulo adattivo da **richiedere per un servizio**. Ad esempio, un&#39;applicazione con carta di credito e un benefit per i cittadini vengono modulo. Quando un utente compila, invia e firma il modulo di domanda, il modulo viene inviato al provider di servizi per ulteriori azioni. Il provider di servizi controlla l&#39;applicazione e utilizza  Adobe Sign per contrassegnare l&#39;applicazione approvata. Per abilitare flussi di lavoro di firma elettronica simili, è possibile integrare  Adobe Sign con  AEM Forms.

Per utilizzare  Adobe Sign con  AEM Forms, configura  Adobe Sign nei servizi AEM Cloud:

## Prerequisiti {#prerequisites}

Per integrare  Adobe Sign con  AEM Forms è necessario disporre dei seguenti requisiti:

* Un account sviluppatore [Adobe Sign attivo.](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* Un server [SSL abilitato](/help/sites-administering/ssl-by-default.md)  AEM Forms.
* Un&#39;applicazione [API](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md)Adobe Sign.
* Credenziali (ID client e Segreto cliente) &#39;applicazione API Adobe Sign.
* Durante la riconfigurazione, rimuovete la configurazione Adobe Sign esistente  dalle istanze di creazione e pubblicazione.
* Utilizzate una chiave [di crittografia](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) identica per le istanze di creazione e pubblicazione.

## Configurare  Adobe Sign con  AEM Forms {#configure-adobe-sign-with-aem-forms}

Dopo aver creato i prerequisiti, eseguite i seguenti passaggi per configurare  Adobe Sign con  AEM Forms nell’istanza Author:

1. ’istanza di creazione di AEM Forms, selezionate **Strumenti** ![martello](assets/hammer.png) > **Generale** > **Browser** di configurazione.
1. Nella pagina del browser **[!UICONTROL di]** configurazione, toccate **[!UICONTROL Crea]**.
1. Nella finestra di dialogo **[!UICONTROL Crea configurazione]** , specificate un **[!UICONTROL titolo]** per la configurazione, abilitate le configurazioni **** Cloud e toccate **[!UICONTROL Crea]**. Crea un contenitore di configurazione per i servizi cloud.
1. Accedete a **Strumenti** ![martello](assets/hammer.png) > **Cloud Services** > **Adobe Sign** e selezionate il contenitore di configurazione creato nel passaggio precedente.

   >[!NOTE]
   >
   >Assicurati che l&#39;URL della pagina di configurazione dei servizi cloud inizi con **HTTPS**. In caso contrario, [abilitate SSL](/help/sites-administering/ssl-by-default.md) per  server AEM Forms.

1. Nella pagina di configurazione, toccate **[!UICONTROL Crea]** per creare  configurazione Adobe Sign in  AEM Forms.
1. Nella scheda **[!UICONTROL Generale]** della pagina **[!UICONTROL Crea configurazione]** Adobe Sign, specificate un **Nome** per la configurazione e toccate **Avanti**. Facoltativamente potete specificare un titolo e cercare per selezionare una miniatura per la configurazione.

1. Copiate l’URL nella finestra del browser corrente su un blocco note. È necessario configurare &#39;applicazione Adobe Sign con  AEM Forms.

1. Configurare le impostazioni OAuth per l&#39;applicazione Adobe Sign :

   1. Aprite una finestra del browser ed effettuate l&#39;accesso all&#39;account sviluppatore Adobe Sign .
   1. Selezionate l&#39;applicazione configurata per  AEM Forms e toccate Configura OAuth per applicazione.
   1. Nella casella URL **di** reindirizzamento, aggiungete l’URL HTTPS copiato nel passaggio precedente e fate clic su **Salva**.
   1. Attivate le seguenti impostazioni OAuth per l&#39;applicazione Adobe Sign  e fate clic su **Salva**.
   * aggrement_read
   * aggrement_write
   * aggrement_send
   * widget_write
   * workflow_read

   Per informazioni dettagliate su come configurare le impostazioni OAuth per un&#39;applicazione Adobe Sign  e ottenere le chiavi, consultate [Configurare le impostazioni di autenticazione per la documentazione per lo sviluppatore dell&#39;applicazione](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md) .

   ![Configurazione OAuth](assets/oauthconfig_new.png)

1. Tornate alla pagina **Crea configurazione** Adobe Sign . Nella scheda **[!UICONTROL Impostazioni]** , il campo URL **** OAuth fa riferimento al seguente URL predefinito:

   https://secure.na1.echosign.com/public/oauth

   dove:

   **na1** fa riferimento alla condivisione di database predefinita.

   È possibile modificare il valore per la condivisione del database. Riavviate il server per poter utilizzare il nuovo valore per la condivisione del database.

1. Specificate l&#39;ID **** client (altrimenti denominato ID applicazione) e il segreto **** client. Selezionare l&#39;opzione **Abilita  Adobe Sign per gli allegati anche** per aggiungere i file allegati a un modulo adattivo al documento Adobe Sign  corrispondente inviato per la firma.

   Tap **[!UICONTROL Connect to Adobe Sign]**. Quando viene richiesto di fornire le credenziali, fornite il nome utente e la password dell&#39;account utilizzato durante la creazione &#39;applicazione Adobe Sign.

   Toccate **[!UICONTROL Crea]** per creare la configurazione Adobe Sign .

1. Apri AEM console Web. L&#39;URL è `https://'[server]:[port]'/system/console/configMgr`
1. Aprite il servizio di configurazione comune **Forms.**
1. Nel campo **Consenti** , **selezionare** Tutti gli utenti - Tutti gli utenti, anonimi o connessi, possono visualizzare in anteprima gli allegati, verificare e firmare i moduli e fare clic su **Salva.** L&#39;istanza Author è configurata per l&#39;utilizzo  Adobe Sign.
1. Utilizzate [la replica](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/replication.html) per creare una configurazione identica sulle istanze di pubblicazione corrispondenti.

 Adobe Sign è ora integrato con  AEM Forms ed è pronto per essere utilizzato nei moduli adattivi. Per [utilizzare  servizio Adobe Sign in un modulo](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form)adattivo, specificare il contenitore di configurazione creato sopra nelle proprietà del modulo adattivo.



## Configurare  pianificazione Adobe Sign per sincronizzare lo stato di firma {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Un  modulo adattivo abilitato per Adobe Sign viene inviato solo dopo che tutti i firmatari avranno completato il processo di firma. Per impostazione predefinita, i servizi di pianificazione di Adobe Sign  sono programmati per controllare (sondaggio) la risposta del firmatario dopo ogni 24 ore. È possibile modificare l&#39;intervallo predefinito per l&#39;ambiente. Per modificare l’intervallo predefinito, effettuate le seguenti operazioni:

1. Accedete a  server AEM Forms con credenziali di amministratore e andate a **Strumenti** > **Operazioni** > Console **** Web.

   Potete anche aprire il seguente URL in una finestra del browser:
   `https://[localhost]:'port'/system/console/configMgr`

1. Individuate e aprite l&#39;opzione **Adobe Sign Configuration Service** . Specificate un&#39;espressione [cron nel campo Espressione](https://en.wikipedia.org/wiki/Cron#CRON_expression) Utilità di pianificazione **Aggiornamento stato e fate clic su** Salva ****. Ad esempio, per eseguire il servizio di configurazione ogni giorno alle 00:00, specificate `0 0 0 1/1 * ? *` nel campo Espressione **Utilità di pianificazione aggiornamento** stato.

L&#39;intervallo predefinito per la sincronizzazione dello stato di  Adobe Sign ora viene modificato.

## Related Articles {#related-articles}

* [Utilizzo di  Adobe Sign in un modulo adattivo](../../forms/using/working-with-adobe-sign.md)
* [Utilizzo  Adobe Sign con  AEM Forms (video)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
* [Integrare  Adobe Sign con  AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md)

