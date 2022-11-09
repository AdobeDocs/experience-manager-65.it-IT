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

[!DNL Adobe Sign] abilita i flussi di lavoro di firma elettronica per i moduli adattivi. Le firme elettroniche migliorano i flussi di lavoro per elaborare documenti per scopi legali, di vendita, di retribuzione, di gestione delle risorse umane e molte altre aree.

In un tipico [!DNL Adobe Sign] e lo scenario relativo ai moduli adattivi, un utente compila un modulo adattivo per **richiedere un servizio**. Ad esempio, un&#39;applicazione con carta di credito e un modulo di benefit per i cittadini. Quando un utente compila, invia e firma il modulo di applicazione, il modulo viene inviato al provider di servizi per ulteriori azioni. Il fornitore di servizi esamina l&#39;applicazione e utilizza [!DNL Adobe Sign] per contrassegnare la domanda approvata. Per abilitare flussi di lavoro con firma elettronica simili, è possibile integrare [!DNL Adobe Sign] con AEM [!DNL Forms].

Per utilizzare [!DNL Adobe Sign] con AEM [!DNL Forms], configura [!DNL Adobe Sign] in AEM Cloud Services:

## Prerequisiti {#prerequisites}

Per integrare è necessario quanto segue [!DNL Adobe Sign] con AEM [!DNL Forms]:

* Attivo [Account sviluppatore Adobe Sign.](https://acrobat.adobe.com/us/en/why-adobe/developer-form.html)
* Un [SSL abilitato](/help/sites-administering/ssl-by-default.md) AEM [!DNL Forms] server.
* Un [Applicazione API Adobe Sign](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* Credenziali (ID client e segreto client) di [!DNL Adobe Sign] Applicazione API.
* Durante la riconfigurazione, rimuovere l&#39;esistente [!DNL Adobe Sign] configurazione da istanze di creazione e pubblicazione.
* Utilizzo [chiave crittografica identica](/help/sites-administering/security-checklist.md#make-sure-you-properly-replicate-encryption-keys-when-needed) per le istanze di authoring e pubblicazione.

## Configura [!DNL Adobe Sign] con AEM [!DNL Forms] {#configure-adobe-sign-with-aem-forms}

Dopo aver impostato i prerequisiti, esegui i seguenti passaggi per configurare [!DNL Adobe Sign] con AEM [!DNL Forms] sull’istanza Author:

1. Su AEM [!DNL Forms] istanza autore, passa a **Strumenti** ![martello](assets/hammer.png) > **[!UICONTROL Generale]** > **[!UICONTROL Browser di configurazione]**.
1. Sulla **[!UICONTROL Browser di configurazione]** pagina, tocca **[!UICONTROL Crea]**.
   * Consulta la sezione [Browser di configurazione](/help/sites-administering/configurations.md) documentazione per ulteriori informazioni.
1. In **[!UICONTROL Crea configurazione]** specifica una finestra di dialogo **[!UICONTROL Titolo]** per la configurazione, abilita **[!UICONTROL Configurazioni cloud]**, e tocca **[!UICONTROL Crea]**. Crea un contenitore di configurazione per Cloud Services.
1. Passa a **Strumenti** ![martello](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]** e seleziona il contenitore di configurazione creato nel passaggio precedente.

   >[!NOTE]
   >
   >Puoi eseguire i passaggi 1-4 per creare un nuovo contenitore di configurazione e creare un [!DNL Adobe Sign] configurazione nel contenitore o utilizza l&#39;esistente `global` cartella in **Strumenti** ![martello](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**. Se crei la configurazione nel nuovo contenitore di configurazione, assicurati di specificare il nome del contenitore nel **[!UICONTROL Contenitore di configurazione]** quando si crea un modulo adattivo.

   >[!NOTE]
   Assicurati che l’URL della pagina di configurazione dei servizi cloud inizi con **HTTPS**. In caso contrario, [abilitare SSL](/help/sites-administering/ssl-by-default.md) per AEM [!DNL Forms] server.

1. Nella pagina di configurazione, tocca **[!UICONTROL Crea]** per creare [!DNL Adobe Sign] configurazione in AEM [!DNL Forms].
1. In **[!UICONTROL Generale]** della scheda **[!UICONTROL Creare la configurazione di Adobe Sign]** pagina, specifica un **[!UICONTROL Nome]** per la configurazione e tocca **[!UICONTROL Successivo]**. Facoltativamente, puoi specificare un titolo e cercare per selezionare una miniatura per la configurazione.

1. Copia l&#39;URL nella finestra del browser corrente su un blocco note. È necessario configurare [!DNL Adobe Sign] applicazione con AEM[!DNL Forms].

1. In **[!UICONTROL Impostazioni]** scheda **[!UICONTROL URL OAuth]** contiene l’URL predefinito. Il formato dell’URL è:

   `https://<shard>/public/oAuth/v2`

   Esempio:
   `https://secure.na1.echosign.com/public/oauth/v2`

   Dove:

   **na1** fa riferimento alla condivisione di database predefinita. È possibile modificare il valore della condivisione del database. Assicurati che [!DNL  Adobe Sign] Le configurazioni cloud puntano al [Shard corretto](https://helpx.adobe.com/sign/using/identify-account-shard.html).

   Se ne crea un altro [!DNL Adobe Sign] per una funzione o un componente Adobe Experience Manager, assicurati che tutte le [!DNL Adobe Sign] Le configurazioni cloud puntano alla stessa condivisione.

   >[!NOTE]
   Mantieni la **Creare la configurazione di Adobe Sign** pagina aperta. Non chiudetelo. È possibile recuperare **ID client** e **Segreto client** dopo aver configurato le impostazioni di OAuth per il [!DNL Adobe Sign] come descritto nei passaggi successivi.


1. Configura le impostazioni OAuth per la [!DNL Adobe Sign] domanda:

   1. Apri una finestra del browser e accedi a [!DNL Adobe Sign] account sviluppatore.
   1. Seleziona l’applicazione configurata per AEM [!DNL Forms], e tocca **[!UICONTROL Configurare OAuth per l’applicazione]**.
   1. Copia il **[!UICONTROL ID client]** e **[!UICONTROL Segreto client]** su un blocco note.
   1. In **[!UICONTROL URL di reindirizzamento]** aggiungi l’URL HTTPS copiato nel passaggio precedente.
   1. Abilita le seguenti impostazioni OAuth per [!DNL Adobe Sign] e fai clic su **[!UICONTROL Salva]**.
   * aggrement_read
   * aggeggio_scrittura
   * annuncio_invio
   * widget_write
   * workflow_read

   Per informazioni dettagliate su come configurare le impostazioni OAuth per un [!DNL Adobe Sign] applicazione e ottenere le chiavi, vedi [Configurare le impostazioni di oAuth per l&#39;applicazione](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md) documentazione per gli sviluppatori.

   ![Configurazione OAuth](assets/oauthconfig_new.png)

1. Torna alla pagina **[!UICONTROL Creare la configurazione di Adobe Sign]** pagina. In **[!UICONTROL Impostazioni]** scheda **[!UICONTROL URL OAuth]** fa riferimento all’URL predefinito. Il formato dell’URL è:

   `https://<shard>/public/oAuth/v2`

   Esempio:
   `https://secure.na1.echosign.com/public/oauth/v2`

   Dove:

   **na1** fa riferimento alla condivisione di database predefinita.

   È possibile modificare il valore della condivisione del database. Riavvia il server per poter utilizzare il nuovo valore per la condivisione del database.

   >[!NOTE]
   Assicurati che le configurazioni dell&#39;istanza di authoring e pubblicazione puntino alla stessa condivisione. Se crei più configurazioni Adobe Sign per un&#39;organizzazione, assicurati che tutte le configurazioni utilizzino la stessa condivisione.

1. Torna alla pagina **[!UICONTROL Creare la configurazione di Adobe Sign]** pagina. In **[!UICONTROL Impostazioni]** specifica la scheda **ID client** (noto anche come ID applicazione) e **Segreto client**. Utilizza la [ID client e segreto client dell’applicazione Adobe Sign](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) creato per AEM Forms.

1. Seleziona la **[!UICONTROL Abilita anche Adobe Sign per gli allegati]** opzione per aggiungere file allegati a un modulo adattivo al corrispondente [!DNL Adobe Sign] documento inviato per la firma.

1. Tocca **[!UICONTROL Connettersi ad Adobe Sign]**. Quando viene richiesto di specificare le credenziali, specificare il nome utente e la password dell’account utilizzato durante la creazione [!DNL Adobe Sign] applicazione.

1. Tocca **[!UICONTROL Crea]** per creare [!DNL Adobe Sign] configurazione.

1. Apri AEM console Web. L’URL è `https://'[server]:[port]'/system/console/configMgr`
1. Apri **[!UICONTROL Servizio di configurazione comune Forms].**
1. In **[!UICONTROL Consenti]** campo, **select** Tutti gli utenti - Tutti gli utenti, anonimi o connessi, possono visualizzare in anteprima gli allegati, verificare e firmare i moduli e fare clic su **[!UICONTROL Salva].** L’istanza dell’autore è configurata per l’utilizzo [!DNL Adobe Sign].
1. Pubblica la configurazione.
1. Utilizzo [replica](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/replication.html?lang=it) per creare una configurazione identica sulle istanze di pubblicazione corrispondenti.

Ora, [!DNL Adobe Sign] è integrato con AEM [!DNL Forms] pronto per l’uso nei moduli adattivi. A [utilizzare il servizio Adobe Sign in un modulo adattivo](../../forms/using/working-with-adobe-sign.md#configure-adobe-sign-for-an-adaptive-form), specifica il contenitore di configurazione creato sopra nelle proprietà del modulo adattivo.



## Configura [!DNL Adobe Sign] scheduler per sincronizzare lo stato della firma {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Un [!DNL Adobe Sign] il modulo adattivo abilitato viene inviato solo dopo che tutti i firmatari hanno completato il processo di firma. Per impostazione predefinita, la [!DNL Adobe Sign] I servizi di pianificazione sono pianificati per controllare (sondaggio) la risposta del firmatario dopo ogni 24 ore. È possibile modificare l’intervallo predefinito per l’ambiente. Esegui i seguenti passaggi per modificare l’intervallo predefinito:

1. Accedi a AEM [!DNL Forms] server con credenziali di amministratore e accedi a **Strumenti** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console web]**.

   Puoi anche aprire il seguente URL in una finestra del browser:
   `https://[localhost]:'port'/system/console/configMgr`

1. Individua e apri la **[!UICONTROL Servizio di configurazione di Adobe Sign]** opzione . Specifica una [espressione cron](https://en.wikipedia.org/wiki/Cron#CRON_expression) in **[!UICONTROL Espressione di pianificazione dell&#39;aggiornamento dello stato]** campo e fai clic su **[!UICONTROL Salva]**. Ad esempio, per eseguire il servizio di configurazione ogni giorno alle 00:00, specifica `0 0 0 1/1 * ? *` in **[!UICONTROL Espressione di pianificazione dell&#39;aggiornamento dello stato]** campo .

Intervallo predefinito per la sincronizzazione dello stato di [!DNL Adobe Sign] ora viene modificato.

## Articoli correlati {#related-articles}

* [Utilizzo di Adobe Sign in un modulo adattivo](../../forms/using/working-with-adobe-sign.md)
* [Utilizzo di Adobe Sign con AEM Forms (video)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
