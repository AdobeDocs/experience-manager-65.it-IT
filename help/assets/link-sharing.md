---
title: Condivisione di risorse tramite un collegamento
description: Condividete risorse, cartelle e raccolte come URL.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 1f6da1c69ea3b3c3f07e8ac10fd8e1e9c7208158
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 6%

---


# Condivisione di risorse tramite un collegamento {#asset-link-sharing}

[!DNL Adobe Experience Manager Assets] consente di condividere risorse, cartelle e raccolte come URL con i membri dell&#39;organizzazione e le entità esterne, inclusi partner e fornitori. La condivisione delle risorse tramite un collegamento è un modo pratico per rendere disponibili le risorse a soggetti esterni senza dover prima effettuare il login a [!DNL Assets].

>[!PREREQUISITES]
>
>* È necessaria l’autorizzazione Modifica ACL per la cartella o la risorsa da condividere come collegamento.
>* Per inviare e-mail agli utenti, configurate i dettagli del server SMTP in [Day CQ Mail Service](#configmailservice).


## Condividere le risorse {#sharelink}

Per generare l’URL delle risorse da condividere con gli utenti, usate la finestra di dialogo Condivisione collegamenti. Gli utenti con privilegi di amministratore o con autorizzazioni di lettura sul `/var/dam/share` posto possono visualizzare i collegamenti condivisi con tali utenti.

1. Nell’interfaccia [!DNL Assets] utente, seleziona la risorsa da condividere come collegamento.
1. Dalla barra degli strumenti, fate clic sull’icona **[!UICONTROL Condividi collegamento]** per ![condividere le risorse](assets/do-not-localize/assets_share.png).

   Il collegamento che verrà creato dopo aver fatto clic su [!UICONTROL Condividi] viene visualizzato in anticipo nel campo [!UICONTROL Condividi collegamento] . Il tempo di scadenza predefinito per il collegamento è un giorno.

   ![Finestra di dialogo con la condivisione dei collegamenti](assets/Link-sharing-dialog-box.png)

   *Figura: Finestra di dialogo per condividere le risorse come collegamento.*

   >[!NOTE]
   >
   >Se desiderate condividere i collegamenti dalla distribuzione di [!DNL Experience Manager] Author a entità esterne, accertatevi di esporre solo i seguenti URL (utilizzati per la condivisione dei collegamenti) per `GET` le richieste. Bloccate altri URL per motivi di sicurezza.
   >
   >* `http://[aem_server]:[port]/linkshare.html`
   >* `http://[aem_server]:[port]/linksharepreview.html`
   >* `http://[aem_server]:[port]/linkexpired.html`


1. Nell&#39; [!DNL Experience Manager] interfaccia, accedere a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > Console **** Web.

1. Open the **[!UICONTROL Day CQ Link Externalizer]** configuration and modify the following properties in the **[!UICONTROL Domains]** field with the values mentioned against `local`, `author`, and `publish`. Per le proprietà `local` e `author` , fornite l’URL rispettivamente per l’istanza locale e per l’istanza di creazione. Sia `local` che `author` le proprietà hanno lo stesso valore se si esegue una singola istanza di [!DNL Experience Manager] creazione. Per le istanze Pubblica, fornite l’URL per l’istanza [!DNL Experience Manager] Pubblica.

1. Nella casella dell’indirizzo e-mail della finestra di dialogo **[!UICONTROL Condivisione collegamenti]**, digita l’ID e-mail dell’utente con cui vuoi condividere il collegamento. Potete aggiungere uno o più utenti.

   ![Condivisione di collegamenti alle risorse direttamente dalla finestra di dialogo Condivisione collegamenti](assets/Asset-Sharing-LinkShareDialog.png)

   *Figura: Condividi i collegamenti alle risorse direttamente dalla finestra di dialogo [!UICONTROL Condivisione] collegamenti.*

   >[!NOTE]
   >
   >Se immettete un ID e-mail di un utente che non è membro dell’organizzazione, le parole Utente  esterno hanno il prefisso con l’ID e-mail dell’utente.

1. Nel campo **[!UICONTROL Oggetto]** , inserire un oggetto.

1. Nel campo **[!UICONTROL Messaggio]** , inserite un messaggio facoltativo.

1. Nel campo **[!UICONTROL Scadenza]** , specificate una data e un&#39;ora di scadenza affinché il collegamento smetta di funzionare. Per impostazione predefinita, la data di scadenza è impostata per una settimana dalla data di condivisione del collegamento.

   ![Imposta data di scadenza del collegamento condiviso](assets/Set-shared-link-expiration.png)

1. Per consentire agli utenti di scaricare la risorsa originale insieme alle rappresentazioni, selezionate **[!UICONTROL Consenti download del file]** originale. Per impostazione predefinita, gli utenti possono scaricare solo le rappresentazioni della risorsa condivisa come collegamento.

1. Fate clic su **[!UICONTROL Condividi]**. Un messaggio conferma la condivisione del collegamento con gli utenti tramite e-mail.

1. Per visualizzare la risorsa condivisa, fate clic sul collegamento contenuto nell&#39;e-mail inviata all&#39;utente. La risorsa condivisa viene visualizzata nella pagina **[!UICONTROL Adobe Marketing Cloud]** .

   ![chlimage_1-260](assets/chlimage_1-545.png)

1. Per generare un’anteprima della risorsa, fate clic sulla risorsa condivisa. To close the preview and return to the **[!UICONTROL Marketing Cloud]** page, click **[!UICONTROL Back]** in the toolbar. If you have shared a folder, click **[!UICONTROL Parent Folder]** to return to the parent folder.

   ![chlimage_1-261](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager] supporta la generazione dell&#39;anteprima delle risorse solo per [i tipi](/help/assets/assets-formats.md)di file supportati. Se altri tipi MIME sono condivisi, potete solo scaricare le risorse e non visualizzare l&#39;anteprima.

1. Per scaricare la risorsa condivisa, fate clic su **[!UICONTROL Seleziona]** nella barra degli strumenti, fate clic sulla risorsa, quindi su **[!UICONTROL Scarica]** dalla barra degli strumenti.

   ![chlimage_1-262](assets/chlimage_1-547.png)

1. Per visualizzare le risorse condivise come collegamenti, passate all’interfaccia [!DNL Assets] utente e fate clic sul [!DNL Experience Manager] logo. Scegliete **[!UICONTROL Navigazione]**. In the Navigation pane, choose **[!UICONTROL Shared Links]** to display a list of shared assets.

1. Per annullare la condivisione di una risorsa, selezionatela e fate clic su **[!UICONTROL Annulla condivisione]** nella barra degli strumenti. Segue un messaggio di conferma. La voce relativa alla risorsa viene rimossa dall’elenco.

## Configura servizio di posta CQ Day {#configmailservice}

1. Nella pagina [!DNL Experience Manager] principale, accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > Console **** Web.
1. Dall&#39;elenco dei servizi, individuare il servizio **[!UICONTROL di posta]** Day CQ.
1. Click **[!UICONTROL Edit]** beside the service, and configure the following parameters for **[!UICONTROL Day CQ Mail Service]** with the details mentioned against their names:

   * Nome host del server SMTP: nome host del server di posta elettronica
   * Porta server SMTP: porta del server di posta elettronica
   * Utente SMTP: nome utente del server di posta elettronica
   * Password SMTP: password del server di posta elettronica

   ![chlimage_1-263](assets/chlimage_1-548.png)

1. Fai clic su **[!UICONTROL Salva]**.

## Configurare la dimensione massima dei dati {#maxdatasize}

Quando scaricate le risorse dal collegamento condiviso mediante la funzione Condivisione collegamenti, comprime [!DNL Experience Manager] la gerarchia delle risorse dall’archivio e quindi restituisce la risorsa in un file ZIP. Tuttavia, in assenza di limiti alla quantità di dati che possono essere compressi in un file ZIP, enormi quantità di dati sono soggetti a compressione, il che causa errori di memoria insufficiente in JVM. Per proteggere il sistema da un potenziale attacco di negazione di servizio a causa di questa situazione, configurate la dimensione massima utilizzando il parametro **[!UICONTROL Max Content Size (non compresso)]** per il servlet [!UICONTROL proxy di condivisione di risorse Adhoc] Day CQ DAM in Configuration Manager. Se le dimensioni non compresse della risorsa superano il valore configurato, le richieste di download delle risorse vengono rifiutate. Il valore predefinito è 100 MB.

1. Click the [!DNL Experience Manager] logo and then go to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Dalla console Web, individua la configurazione **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** .
1. Apri la configurazione **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** in modalità di modifica e cambia il valore del parametro in **[!UICONTROL Max Content Size (uncompressed)]**.

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. Salva le modifiche.

## Best practices and troubleshooting {#bestpractices}

* Le cartelle di risorse o le raccolte che contengono uno spazio vuoto nel loro nome potrebbero non essere condivise.
* Se gli utenti non possono scaricare le risorse condivise, verificate con [!DNL Experience Manager] l’amministratore quali siano i limiti [di](#maxdatasize) download.
* Se non potete inviare e-mail con collegamenti a risorse condivise o se gli altri utenti non possono ricevere l’e-mail, verificate con l’ [!DNL Experience Manager] amministratore se il servizio [e-](#configmailservice) mail è configurato o meno.
* Se non potete condividere le risorse utilizzando la funzionalità di condivisione dei collegamenti, accertatevi di disporre delle autorizzazioni appropriate. Consultate [Condividere le risorse](#sharelink).
* Se una risorsa condivisa viene spostata in un percorso diverso, il collegamento non funziona più. Crea di nuovo il collegamento e condividi nuovamente con gli utenti.
