---
title: Condivisione di risorse tramite un collegamento
description: Condividete risorse, cartelle e raccolte come URL.
contentOwner: AG
translation-type: tm+mt
source-git-commit: e36d08c9ea89e840aecde79ffdd911372c0c54ee
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 5%

---


# Condivisione di risorse tramite un collegamento {#asset-link-sharing}

[!DNL Adobe Experience Manager Assets] consente di condividere risorse, cartelle e raccolte come URL con i membri dell&#39;organizzazione e le entità esterne, inclusi partner e fornitori. La condivisione delle risorse tramite un collegamento è un modo pratico per rendere disponibili le risorse a soggetti esterni senza dover prima accedere a [!DNL Assets].

>[!PREREQUISITES]
>
>* È necessaria l’autorizzazione Modifica ACL per la cartella o la risorsa da condividere come collegamento.
>* Per inviare e-mail agli utenti, configurare i dettagli del server SMTP in [Day CQ Mail Service](#configmailservice).


## Condividere le risorse {#sharelink}

Per generare l’URL delle risorse da condividere con gli utenti, usate la finestra di dialogo Condivisione collegamenti. Gli utenti con privilegi di amministratore o con autorizzazioni di lettura nel percorso `/var/dam/share` possono visualizzare i collegamenti condivisi con loro.

1. Nell&#39;interfaccia utente [!DNL Assets], seleziona la risorsa da condividere come collegamento.
1. Dalla barra degli strumenti, fate clic sull&#39;icona **[!UICONTROL Condividi collegamento]** ![Condividi risorse](assets/do-not-localize/assets_share.png).

   Il collegamento che verrà creato dopo aver fatto clic su [!UICONTROL Condividi] viene visualizzato in anticipo nel campo [!UICONTROL Condividi collegamento]. Il tempo di scadenza predefinito per il collegamento è un giorno.

   ![Finestra di dialogo con la condivisione dei collegamenti](assets/Link-sharing-dialog-box.png)

   *Figura: Finestra di dialogo per condividere le risorse come collegamento.*

   >[!NOTE]
   >
   >Se desiderate condividere i collegamenti dalla distribuzione [!DNL Experience Manager] Autore a entità esterne, accertatevi di esporre solo i seguenti URL (utilizzati per la condivisione dei collegamenti) per le sole richieste `GET`. Bloccate altri URL per motivi di sicurezza.
   >
   >* `http://[aem_server]:[port]/linkshare.html`
   >* `http://[aem_server]:[port]/linksharepreview.html`
   >* `http://[aem_server]:[port]/linkexpired.html`


1. Nell&#39;interfaccia [!DNL Experience Manager], accedere a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console Web]**.

1. Aprire la configurazione **[!UICONTROL Day CQ Link Externalizer]** e modificare le seguenti proprietà nel campo **[!UICONTROL Domains]** con i valori indicati rispetto a `local`, `author` e `publish`. Per le proprietà `local` e `author`, fornite l&#39;URL rispettivamente per l&#39;istanza locale e per l&#39;istanza di creazione. Sia le proprietà `local` che `author` hanno lo stesso valore se si esegue una singola istanza di creazione [!DNL Experience Manager]. Per le istanze Pubblica, fornite l&#39;URL per l&#39;istanza di pubblicazione [!DNL Experience Manager].

1. Nella casella dell’indirizzo e-mail della finestra di dialogo **[!UICONTROL Condivisione collegamenti]**, digita l’ID e-mail dell’utente con cui vuoi condividere il collegamento. Potete aggiungere uno o più utenti.

   ![Condivisione di collegamenti alle risorse direttamente dalla finestra di dialogo Condivisione collegamenti](assets/Asset-Sharing-LinkShareDialog.png)

   *Figura: Condividi i collegamenti alle risorse direttamente dalla finestra di dialogo  [!UICONTROL Collega ] condivisione.*

   >[!NOTE]
   >
   >Se immettete un ID e-mail di un utente che non è membro dell&#39;organizzazione, le parole [!UICONTROL Utente esterno] hanno il prefisso dell&#39;ID e-mail dell&#39;utente.

1. Nella casella **[!UICONTROL Oggetto]**, inserite l’oggetto della risorsa da condividere.

1. Nella casella **[!UICONTROL Messaggio]**, immettere un messaggio facoltativo.

1. Nel campo **[!UICONTROL Scadenza]**, specificare una data e un&#39;ora di scadenza affinché il collegamento smetta di funzionare. Per impostazione predefinita, la data di scadenza è impostata per una settimana dalla data di condivisione del collegamento.

   ![Imposta data di scadenza del collegamento condiviso](assets/Set-shared-link-expiration.png)

1. Per consentire agli utenti di scaricare la risorsa originale insieme alle rappresentazioni, selezionate **[!UICONTROL Consenti download del file originale]**. Per impostazione predefinita, gli utenti possono scaricare solo le rappresentazioni della risorsa condivisa come collegamento.

1. Fate clic su **[!UICONTROL Condividi]**. Un messaggio conferma la condivisione del collegamento con gli utenti tramite e-mail.

1. Per visualizzare la risorsa condivisa, fate clic sul collegamento contenuto nell&#39;e-mail inviata all&#39;utente. La risorsa condivisa viene visualizzata nella pagina [!UICONTROL Adobe Marketing Cloud].

   ![Le risorse condivise sono disponibili in Adobe Marketing Cloud](assets/chlimage_1-545.png)

1. Per generare un’anteprima della risorsa, fate clic sulla risorsa condivisa. Per chiudere l&#39;anteprima e tornare alla pagina **[!UICONTROL Marketing Cloud]**, fare clic su **[!UICONTROL Indietro]** nella barra degli strumenti. Se avete condiviso una cartella, fate clic su **[!UICONTROL Cartella principale]** per tornare alla cartella principale.

   ![chlimage_1-261](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager] supporta la generazione dell&#39;anteprima delle risorse solo per  [i tipi](/help/assets/assets-formats.md) di file supportati. Se altri tipi MIME sono condivisi, potete solo scaricare le risorse e non visualizzare l&#39;anteprima.

1. Per scaricare la risorsa condivisa, fate clic su **[!UICONTROL Seleziona]** nella barra degli strumenti, fate clic sulla risorsa, quindi su **[!UICONTROL Scarica]** dalla barra degli strumenti.

   ![Opzione della barra degli strumenti per scaricare la risorsa condivisa](assets/chlimage_1-547.png)

1. Per visualizzare le risorse condivise come collegamenti, passate all&#39;interfaccia utente [!DNL Assets] e fate clic sul logo [!DNL Experience Manager]. Scegliere **[!UICONTROL Navigazione]**. Nel riquadro di navigazione, scegliete **[!UICONTROL Collegamenti condivisi]** per visualizzare un elenco delle risorse condivise.

1. Per annullare la condivisione di una risorsa, selezionatela e fate clic su **[!UICONTROL Annulla condivisione]** nella barra degli strumenti. Segue un messaggio di conferma. La voce relativa alla risorsa viene rimossa dall’elenco.

## Configurare il servizio di posta di CQ Day {#configmailservice}

1. Nella home page di [!DNL Experience Manager], passare a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console Web]**.
1. Dall&#39;elenco dei servizi, individuare **[!UICONTROL Day CQ Mail Service]**.
1. Fare clic su **[!UICONTROL Modifica]** accanto al servizio e configurare i seguenti parametri per **[!UICONTROL Day CQ Mail Service]** con i dettagli indicati con i relativi nomi:

   * Nome host del server SMTP: nome host del server di posta elettronica
   * Porta server SMTP: porta del server di posta elettronica
   * Utente SMTP: nome utente del server di posta elettronica
   * Password SMTP: password del server di posta elettronica

   ![chlimage_1-263](assets/chlimage_1-548.png)

1. Fai clic su **[!UICONTROL Salva]**.

## Configurare la dimensione massima dei dati {#maxdatasize}

Quando scaricate le risorse dal collegamento condiviso utilizzando la funzione Condivisione collegamenti, [!DNL Experience Manager] comprime la gerarchia di risorse dall&#39;archivio e quindi restituisce la risorsa in un file ZIP. Tuttavia, in assenza di limiti alla quantità di dati che possono essere compressi in un file ZIP, enormi quantità di dati sono soggetti a compressione, il che causa errori di memoria insufficiente in JVM. Per proteggere il sistema da un potenziale attacco di negazione del servizio a causa di questa situazione, configurare la dimensione massima utilizzando il parametro **[!UICONTROL Max Content Size (non compresso)]** per [!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet] in Configuration Manager. Se le dimensioni non compresse della risorsa superano il valore configurato, le richieste di download delle risorse vengono rifiutate. Il valore predefinito è 100 MB.

1. Fare clic sul logo [!DNL Experience Manager], quindi passare a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console Web]**.
1. Dalla console Web, individua la configurazione **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]**.
1. Apri la configurazione **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** in modalità di modifica e cambia il valore del parametro in **[!UICONTROL Max Content Size (uncompressed)]**.

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. Salva le modifiche.

## Procedure ottimali e risoluzione dei problemi {#bestpractices}

* Le cartelle di risorse o le raccolte che contengono uno spazio vuoto nel loro nome potrebbero non essere condivise.
* Se gli utenti non possono scaricare le risorse condivise, verificate con il vostro [!DNL Experience Manager] amministratore quali siano i [limiti di download](#maxdatasize).
* Se non potete inviare e-mail con collegamenti a risorse condivise o se gli altri utenti non possono ricevere l&#39;e-mail, verificate con l&#39;amministratore [!DNL Experience Manager]se il &lt;a1/>servizio e-mail[ è configurato o meno.](#configmailservice)
* Se non potete condividere le risorse utilizzando la funzionalità di condivisione dei collegamenti, accertatevi di disporre delle autorizzazioni appropriate. Consultate [condividere risorse](#sharelink).
* Se una risorsa condivisa viene spostata in un percorso diverso, il collegamento non funziona più. Crea di nuovo il collegamento e condividi nuovamente con gli utenti.
