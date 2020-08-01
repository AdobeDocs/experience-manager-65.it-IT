---
title: Generare un URL per le risorse condivise
description: Questo articolo descrive come condividere risorse, cartelle e raccolte [!DNL Experience Manager Assets] all’interno di un URL per parti esterne.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '1196'
ht-degree: 7%

---


# Condivisione di risorse tramite un collegamento {#asset-link-sharing}

[!DNL Adobe Experience Manager Assets] consente di condividere risorse, cartelle e raccolte come URL con i membri dell&#39;organizzazione e le entità esterne, inclusi partner e fornitori. La condivisione delle risorse tramite un collegamento è un modo pratico per rendere disponibili le risorse a soggetti esterni senza dover prima effettuare il login a [!DNL Assets].

>[!NOTE]
>
>È necessaria l’autorizzazione Modifica ACL per la cartella o la risorsa da condividere come collegamento.

## Condividere le risorse {#sharelink}

Per generare l’URL delle risorse da condividere con gli utenti, usate la finestra di dialogo Condivisione collegamenti. Gli utenti con privilegi di amministratore o con autorizzazioni di lettura sul `/var/dam/share` posto possono visualizzare i collegamenti condivisi con tali utenti.

>[!NOTE]
>
>Prima di condividere un collegamento con gli utenti, assicurarsi che Day CQ Mail Service sia configurato. Si verifica un errore se si tenta di condividere un collegamento senza prima [configurare Day CQ Mail Service](/help/assets/link-sharing.md#configmailservice).

1. Nell’interfaccia [!DNL Assets] utente, seleziona la risorsa da condividere come collegamento.
1. Dalla barra degli strumenti, fate clic sull’icona **[!UICONTROL Condividi collegamento]** per ![condividere le risorse](assets/do-not-localize/assets_share.png).

   Nel campo **[!UICONTROL Condividi collegamento]** viene creato automaticamente un collegamento a una risorsa. Copiate questo collegamento e condividetelo con gli utenti. Il tempo di scadenza predefinito per il collegamento è un giorno.

   ![Finestra di dialogo con la condivisione dei collegamenti](assets/Link-sharing-dialog-box.png)

   *Figura: Finestra di dialogo per condividere le risorse come collegamento.*

   In alternativa, esegui i passaggi 3-7 di questa procedura per aggiungere i destinatari e-mail, configurare l’ora di scadenza del collegamento e inviarlo dalla finestra di dialogo.

   >[!NOTE]
   >
   >Se desiderate condividere i collegamenti dalla distribuzione di [!DNL Experience Manager] Author a entità esterne, accertatevi di esporre solo i seguenti URL (utilizzati per la condivisione dei collegamenti) per `GET` le richieste. Bloccate altri URL per garantire la sicurezza di [!DNL Experience Manager] Author.
   >
   >* http://[aem_server]:[porta]/linkshare.html
   >* http://[aem_server]:[porta]/linksharepreview.html
   >* http://[aem_server]:[porta]/linkexpired.html


   >[!NOTE]
   >
   >Se una risorsa condivisa viene spostata in un percorso diverso, il collegamento non funziona più. Crea di nuovo il collegamento e condividi nuovamente con gli utenti.

1. Nell&#39; [!DNL Experience Manager] interfaccia, accedere a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > Console **** Web.

1. Open the **[!UICONTROL Day CQ Link Externalizer]** configuration and modify the following properties in the **[!UICONTROL Domains]** field with the values mentioned against `local`, `author`, and `publish`. Per le proprietà `local` e `author` , fornite l’URL rispettivamente per l’istanza locale e per l’istanza di creazione. Sia `local` che `author` le proprietà hanno lo stesso valore se si esegue una singola istanza di [!DNL Experience Manager] Author. Ad `publish`esempio, fornite l’URL per l’istanza di [!DNL Experience Manager] pubblicazione.

1. Nella casella dell’indirizzo e-mail della finestra di dialogo **[!UICONTROL Condivisione collegamenti]**, digita l’ID e-mail dell’utente con cui vuoi condividere il collegamento. Puoi anche condividere il collegamento con più utenti.

   Se l’utente è membro dell’organizzazione, selezionate l’ID e-mail dell’utente dagli ID e-mail suggeriti che vengono visualizzati nell’elenco al di sotto dell’area di digitazione. Per un utente esterno, digitate l’ID e-mail completo e selezionatelo dall’elenco.

   Per abilitare l&#39;invio di e-mail agli utenti, configurate i dettagli del server SMTP in [Day CQ Mail Service](#configmailservice).

   ![Condivisione di collegamenti alle risorse direttamente dalla finestra di dialogo Condivisione collegamenti](assets/Asset-Sharing-LinkShareDialog.png)

   *Figura: Condividi i collegamenti alle risorse direttamente dalla finestra di dialogo[!UICONTROL Condivisione]collegamenti.*

   >[!NOTE]
   >
   >Se immettete un ID e-mail di un utente che non è membro dell’organizzazione, le parole Utente  esterno hanno il prefisso con l’ID e-mail dell’utente.

1. Nel campo **[!UICONTROL Oggetto]** , inserite un oggetto per la risorsa da condividere.

1. Nel campo **[!UICONTROL Messaggio]** , inserite un messaggio facoltativo.

1. Nel campo **[!UICONTROL Scadenza]** , specifica una data e un&#39;ora di scadenza per il collegamento utilizzando il selettore data. Per impostazione predefinita, la data di scadenza è impostata per una settimana dalla data di condivisione del collegamento.

   ![Imposta data di scadenza del collegamento condiviso](assets/Set-shared-link-expiration.png)

1. Per consentire agli utenti di scaricare l&#39;immagine originale insieme alle rappresentazioni, selezionate **[!UICONTROL Consenti download del file]** originale.

   >[!NOTE]
   >
   >Per impostazione predefinita, gli utenti possono scaricare solo le rappresentazioni della risorsa condivisa come collegamento.

1. Fate clic su **[!UICONTROL Condividi]**. Un messaggio conferma la condivisione del collegamento con gli utenti tramite e-mail.
1. Per visualizzare la risorsa condivisa, fate clic sul collegamento contenuto nell&#39;e-mail inviata all&#39;utente. La risorsa condivisa viene visualizzata nella pagina **[!UICONTROL Adobe Marketing Cloud]** .

   ![chlimage_1-260](assets/chlimage_1-545.png)

   Per passare alla vista a elenco, fate clic sull’opzione di layout nella barra degli strumenti.

1. Per generare un’anteprima della risorsa, fate clic sulla risorsa condivisa. To close the preview and return to the **[!UICONTROL Marketing Cloud]** page, click **[!UICONTROL Back]** in the toolbar. If you have shared a folder, click **[!UICONTROL Parent Folder]** to return to the parent folder.

   ![chlimage_1-261](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager] supporta la generazione dell&#39;anteprima delle risorse di questi tipi MIME: JPG, PNG, GIF, BMP, INDD, PDF e PPT. Potete scaricare solo le risorse degli altri tipi MIME.

1. Per scaricare la risorsa condivisa, fate clic su **[!UICONTROL Seleziona]** nella barra degli strumenti, fate clic sulla risorsa, quindi su **[!UICONTROL Scarica]** dalla barra degli strumenti.

   ![chlimage_1-262](assets/chlimage_1-547.png)

1. Per visualizzare le risorse condivise come collegamenti, passate all’interfaccia [!DNL Assets] utente e fate clic sul [!DNL Experience Manager] logo. Scegliere **[!UICONTROL Navigazione]** dall&#39;elenco per visualizzare il riquadro di navigazione.
1. Per visualizzare un elenco delle risorse condivise, scegli **[!UICONTROL Collegamenti condivisi]** nel riquadro di navigazione.
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
