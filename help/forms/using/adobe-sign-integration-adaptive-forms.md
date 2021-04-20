---
title: Integrare Adobe Sign con AEM Forms
seo-title: Integrare Adobe Sign con AEM Forms
description: Scopri come configurare Adobe Sign per AEM Forms
seo-description: Scopri come configurare Adobe Sign per AEM Forms
uuid: e5049775-fb6c-4228-9823-e6a2811460da
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 1f28b257-5419-4a21-a54a-b20bf35530ac
docset: aem65
feature: Adaptive Forms, Adobe Sign
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 0%

---


# Integrare [!DNL Adobe Sign] con AEM [!DNL Forms]{#integrate-adobe-sign-with-aem-forms}

[!DNL Adobe Sign] abilita i flussi di lavoro di firma elettronica per i moduli adattivi. Le firme elettroniche migliorano i flussi di lavoro per elaborare documenti per scopi legali, di vendita, di retribuzione, di gestione delle risorse umane e molte altre aree.

In uno scenario tipico [!DNL Adobe Sign] e con moduli adattivi, un utente compila un modulo adattivo per **richiedere un servizio**. Ad esempio, un&#39;applicazione con carta di credito e un modulo di benefit per i cittadini. Quando un utente compila, invia e firma il modulo di applicazione, il modulo viene inviato al provider di servizi per ulteriori azioni. Il fornitore di servizi controlla l&#39;applicazione e utilizza [!DNL Adobe Sign] per contrassegnare l&#39;applicazione approvata. Per abilitare flussi di lavoro con firma elettronica simili, è possibile integrare [!DNL Adobe Sign] con AEM [!DNL Forms].

Per utilizzare [!DNL Adobe Sign] con AEM [!DNL Forms], configura [!DNL Adobe Sign] in AEM Cloud Services:

## Prerequisiti {#prerequisites}

Per integrare [!DNL Adobe Sign] con AEM [!DNL Forms] è necessario quanto segue:

* Un account sviluppatore [Adobe Sign attivo.](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* Un server [SSL abilitato](/help/sites-administering/ssl-by-default.md) AEM [!DNL Forms].
* Applicazione API Adobe Sign [](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* Credenziali (ID client e segreto client) dell&#39;applicazione API [!DNL Adobe Sign].
* Durante la riconfigurazione, rimuovi la configurazione [!DNL Adobe Sign] esistente sia dalle istanze di authoring che di pubblicazione.
* Utilizza [la chiave di crittografia identica](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) per le istanze di authoring e pubblicazione.

## Configura [!DNL Adobe Sign] con AEM [!DNL Forms] {#configure-adobe-sign-with-aem-forms}

Dopo aver impostato i prerequisiti, esegui i seguenti passaggi per configurare [!DNL Adobe Sign] con AEM [!DNL Forms] sull’istanza di authoring:

1. AEM [!DNL Forms] istanza autore, accedi a **Strumenti** ![martello](assets/hammer.png) > **[!UICONTROL Generale]** > **[!UICONTROL Browser configurazioni]**.
1. Nella pagina **[!UICONTROL Browser configurazione]**, tocca **[!UICONTROL Crea]**.
   * Per ulteriori informazioni, consulta la documentazione [Browser configurazioni](/help/sites-administering/configurations.md) .
1. Nella finestra di dialogo **[!UICONTROL Crea configurazione]**, specifica un **[!UICONTROL Titolo]** per la configurazione, abilita **[!UICONTROL Configurazioni cloud]** e tocca **[!UICONTROL Crea]**. Crea un contenitore di configurazione per Cloud Services.
1. Passa a **Strumenti** ![martello](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]** e seleziona il contenitore di configurazione creato nel passaggio precedente.

   >[!NOTE]
   >
   >Puoi eseguire i passaggi 1-4 per creare un nuovo contenitore di configurazione e creare una configurazione [!DNL Adobe Sign] nel contenitore oppure utilizzare la cartella `global` esistente in **Strumenti** ![martello](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. Se crei la configurazione nel nuovo contenitore di configurazione, assicurati di specificare il nome del contenitore nel campo **[!UICONTROL Contenitore di configurazione]** quando crei un modulo adattivo.

   >[!NOTE]
   Assicurati che l&#39;URL della pagina di configurazione dei servizi cloud inizi con **HTTPS**. In caso contrario, [abilita SSL](/help/sites-administering/ssl-by-default.md) per AEM server [!DNL Forms].

1. Nella pagina di configurazione, tocca **[!UICONTROL Crea]** per creare la configurazione [!DNL Adobe Sign] in AEM [!DNL Forms].
1. Nella scheda **[!UICONTROL Generale]** della pagina **[!UICONTROL Crea configurazione Adobe Sign]** , specifica un **[!UICONTROL Nome]** per la configurazione e tocca **[!UICONTROL Avanti]**. Facoltativamente, puoi specificare un titolo e cercare per selezionare una miniatura per la configurazione.

1. Copia l&#39;URL nella finestra del browser corrente su un blocco note. È necessario configurare l&#39;applicazione [!DNL Adobe Sign] con AEM[!DNL Forms].

1. Configura le impostazioni OAuth per l&#39;applicazione [!DNL Adobe Sign]:

   1. Apri una finestra del browser e accedi all’ account sviluppatore [!DNL Adobe Sign] .
   1. Seleziona l’applicazione configurata per AEM [!DNL Forms] e tocca **[!UICONTROL Configura OAuth per l’applicazione]**.
   1. Copia l&#39; **[!UICONTROL ID client]** e **[!UICONTROL Segreto client]** in un blocco note.
   1. Nella casella **[!UICONTROL URL di reindirizzamento]** , aggiungi l’URL HTTPS copiato nel passaggio precedente.
   1. Abilita le seguenti impostazioni OAuth per l’applicazione [!DNL Adobe Sign] e fai clic su **[!UICONTROL Salva]**.
   * aggrement_read
   * aggeggio_scrittura
   * annuncio_invio
   * widget_write
   * workflow_read

   Per informazioni dettagliate su come configurare le impostazioni OAuth per un’applicazione [!DNL Adobe Sign] e ottenere le chiavi, consulta [Configurare le impostazioni oAuth per la documentazione per gli sviluppatori dell’applicazione](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md).

   ![Configurazione OAuth](assets/oauthconfig_new.png)

1. Torna alla pagina **[!UICONTROL Crea configurazione Adobe Sign]** . Nella scheda **[!UICONTROL Impostazioni]** , il campo **[!UICONTROL URL OAuth]** cita il seguente URL predefinito:

   https://secure.na1.echosign.com/public/oauth

   dove:

   **na1** fa riferimento alla condivisione di database predefinita.

   È possibile modificare il valore della condivisione del database. Riavvia il server per poter utilizzare il nuovo valore per la condivisione del database.

   >[!NOTE]
   Assicurati che le configurazioni dell&#39;istanza di authoring e pubblicazione puntino alla stessa condivisione. Se crei più configurazioni Adobe Sign per un&#39;organizzazione, assicurati che tutte le configurazioni utilizzino la stessa condivisione.

1. Specifica l&#39; **ID client** (noto anche come ID applicazione) e **Segreto client** nel passaggio 8. Selezionare l&#39;opzione **[!UICONTROL Abilita Adobe Sign per gli allegati anche]** per aggiungere i file allegati a un modulo adattivo al documento [!DNL Adobe Sign] corrispondente inviato per la firma.

   Tocca **[!UICONTROL Connetti ad Adobe Sign]**. Quando viene richiesto di specificare le credenziali, specificare il nome utente e la password dell&#39;account utilizzato durante la creazione dell&#39;applicazione [!DNL Adobe Sign].

   Tocca **[!UICONTROL Crea]** per creare la configurazione [!DNL Adobe Sign].

1. Apri AEM console Web. L&#39;URL è `https://'[server]:[port]'/system/console/configMgr`
1. Apri **[!UICONTROL Forms Common Configuration Service].**
1. Nel campo **[!UICONTROL Consenti]**, **seleziona** Tutti gli utenti - Tutti gli utenti, anonimi o connessi, possono visualizzare in anteprima gli allegati, verificare e firmare i moduli e fare clic su **[!UICONTROL Salva].** L’istanza di authoring è configurata per l’utilizzo di  [!DNL Adobe Sign].
1. Pubblica la configurazione.
1. Utilizza [replica](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/configuring/replication.html) per creare una configurazione identica sulle istanze di pubblicazione corrispondenti.

Ora [!DNL Adobe Sign] è integrato con AEM [!DNL Forms] ed è pronto per l’uso nei moduli adattivi. Per [utilizzare il servizio Adobe Sign in un modulo adattivo](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form), specifica il contenitore di configurazione creato sopra nelle proprietà del modulo adattivo.



## Configura la pianificazione [!DNL Adobe Sign] per sincronizzare lo stato di firma {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Un modulo adattivo abilitato [!DNL Adobe Sign] viene inviato solo dopo che tutti i firmatari hanno completato il processo di firma. Per impostazione predefinita, i servizi di pianificazione [!DNL Adobe Sign] sono programmati per controllare (polling) la risposta del firmatario dopo ogni 24 ore. È possibile modificare l’intervallo predefinito per l’ambiente. Esegui i seguenti passaggi per modificare l’intervallo predefinito:

1. Accedi al server AEM [!DNL Forms] con credenziali di amministratore e passa a **Strumenti** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console web]**.

   Puoi anche aprire il seguente URL in una finestra del browser:
   `https://[localhost]:'port'/system/console/configMgr`

1. Individua e apri l&#39;opzione **[!UICONTROL Servizio di configurazione Adobe Sign]** . Specifica un&#39;espressione [cron](https://en.wikipedia.org/wiki/Cron#CRON_expression) nel campo **[!UICONTROL Espressione pianificazione aggiornamento stato]** e fai clic su **[!UICONTROL Salva]**. Ad esempio, per eseguire il servizio di configurazione ogni giorno alle 00:00, specifica `0 0 0 1/1 * ? *` nel campo **[!UICONTROL Espressione pianificazione aggiornamento stato]** .

L&#39;intervallo predefinito per la sincronizzazione dello stato di [!DNL Adobe Sign] viene ora modificato.

## Articoli correlati {#related-articles}

* [Utilizzo di Adobe Sign in un modulo adattivo](../../forms/using/working-with-adobe-sign.md)
* [Utilizzo di Adobe Sign con AEM Forms (video)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)


