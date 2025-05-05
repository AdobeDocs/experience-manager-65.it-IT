---
title: Condividere risorse tramite un collegamento
description: Condividere risorse, cartelle e raccolte come URL.
contentOwner: AG
role: User
feature: Link Sharing,Asset Management
exl-id: 20370b00-862e-4d04-af2f-7d1c74a842dd
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 7%

---

# Condividere la risorsa come collegamento {#asset-link-sharing}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/share-assets.html?lang=it) |
| AEM 6.5 | Questo articolo |

[!DNL Adobe Experience Manager Assets] consente di condividere risorse, cartelle e raccolte come URL con i membri dell&#39;organizzazione ed entità esterne, inclusi partner e fornitori. La condivisione delle risorse tramite un collegamento è un modo pratico per rendere le risorse disponibili alle parti esterne senza dover prima accedere a [!DNL Assets].

>[!PREREQUISITES]
>
>* È necessaria l&#39;autorizzazione `Edit ACL` per la cartella o la risorsa da condividere come collegamento.
>* Per inviare le e-mail agli utenti, configura i dettagli del server SMTP in [Day CQ Mail Service](#configmailservice).

## Condividere le risorse {#share-assets}

Per generare l&#39;URL per le risorse da condividere con gli utenti, utilizza la finestra di dialogo [!UICONTROL Condivisione collegamenti].

* Gli utenti con privilegi di amministratore o con autorizzazioni di lettura nel percorso `/var/dam/share` possono visualizzare i collegamenti condivisi con loro.
* Gli utenti con autorizzazioni di lettura nel percorso `/var/dam/jobs/download` possono scaricare risorse dal collegamento condiviso.

1. Nell&#39;interfaccia utente [!DNL Assets], seleziona la risorsa da condividere come collegamento.

1. Dalla barra degli strumenti, fai clic sull&#39;icona **[!UICONTROL Condividi collegamento]** ![condividi risorse](assets/do-not-localize/assets_share.png). Il collegamento creato dopo aver fatto clic su **[!UICONTROL Condividi]** viene visualizzato in anticipo nel campo [!UICONTROL Condividi collegamento]. Il collegamento non viene creato finché non si seleziona **[!UICONTROL Invia]**.

   ![Finestra di dialogo con condivisione collegamenti](assets/share-assets-as-link.png)

   *Figura: finestra di dialogo per condividere le risorse come collegamento.*

1. Nella casella dell’indirizzo e-mail della finestra di dialogo **[!UICONTROL Condivisione collegamenti]**, digita l’ID e-mail dell’utente con cui vuoi condividere il collegamento. Puoi aggiungere uno o più utenti.

   >[!NOTE]
   >
   >Se immetti un ID e-mail di un utente che non è membro della tua organizzazione, le parole [!UICONTROL Utente esterno] avranno il prefisso ID e-mail dell&#39;utente.

1. Nella casella **[!UICONTROL Oggetto]** immettere un oggetto per la risorsa da condividere.

1. Nella casella **[!UICONTROL Messaggio]** immettere un messaggio facoltativo.

1. Nel campo **[!UICONTROL Scadenza]**, specifica una data e un&#39;ora di scadenza per il collegamento in modo che non funzioni più. La scadenza predefinita del collegamento è un giorno.

   ![Imposta la data di scadenza del collegamento condiviso](assets/Set-shared-link-expiration.png)

1. Per consentire agli utenti di scaricare la risorsa originale, selezionare **[!UICONTROL Consenti download del file originale]**. Per consentire agli utenti di scaricare solo i rendering delle risorse condivise, selezionare **[!UICONTROL Consenti download dei rendering del file]**.

1. Fai clic su **[!UICONTROL Condividi]**. Un messaggio conferma che il collegamento è condiviso con gli utenti tramite e-mail.

1. Per visualizzare la risorsa condivisa, fai clic sul collegamento nell’e-mail inviata all’utente. Per generare un’anteprima della risorsa, fai clic sulla risorsa condivisa. Per chiudere l&#39;anteprima, fare clic su **[!UICONTROL Indietro]**. Se hai condiviso una cartella, fai clic su **[!UICONTROL Cartella principale]** per tornare alla cartella principale.

   ![Anteprima della risorsa condivisa](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager] supporta la generazione dell&#39;anteprima delle risorse solo di [tipi di file supportati](/help/assets/assets-formats.md). Se sono condivisi altri tipi MIME, puoi scaricare solo le risorse e non visualizzare l’anteprima.

1. Per scaricare la risorsa condivisa, fai clic su **[!UICONTROL Seleziona]** nella barra degli strumenti, fai clic sulla risorsa e quindi su **[!UICONTROL Scarica]** nella barra degli strumenti.

   ![Opzione barra degli strumenti per scaricare la risorsa condivisa](assets/chlimage_1-547.png)

1. Per visualizzare le risorse condivise come collegamenti, passa all&#39;interfaccia utente [!DNL Assets] e fai clic sul logo [!DNL Experience Manager]. Scegliere **[!UICONTROL Navigazione]**. Nel riquadro di spostamento scegliere **[!UICONTROL Collegamenti condivisi]** per visualizzare un elenco di risorse condivise.

1. Per non condividere una risorsa, selezionala e fai clic su **[!UICONTROL Annulla condivisione]** nella barra degli strumenti. Segue un messaggio di conferma. La voce relativa alla risorsa viene rimossa dall’elenco.

## Configurare il servizio di posta Day CQ {#configure-day-cq-mail-service}

1. Nella home page di [!DNL Experience Manager], passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console Web]**.
1. Dall&#39;elenco dei servizi, individuare **[!UICONTROL Day CQ Mail Service]**.
1. Fai clic su **[!UICONTROL Modifica]** accanto al servizio e configura i seguenti parametri per **[!UICONTROL Day CQ Mail Service]** con i dettagli indicati insieme ai relativi nomi:

   * Nome host server SMTP: nome host server e-mail
   * Porta server SMTP: porta server e-mail
   * Utente SMTP: nome utente del server e-mail
   * Password SMTP: password del server e-mail

   ![chlimage_1-263](assets/chlimage_1-548.png)

1. Fai clic su **[!UICONTROL Salva]**.

## Configurare la dimensione massima dei dati {#configure-maximum-data-size}

Quando si scaricano risorse dal collegamento condiviso utilizzando la funzione Condivisione collegamenti, [!DNL Experience Manager] comprime la gerarchia delle risorse dall&#39;archivio e quindi restituisce la risorsa in un file ZIP. Tuttavia, in assenza di limiti alla quantità di dati che è possibile comprimere in un file ZIP, enormi quantità di dati sono soggette a compressione, che causa errori di memoria esaurita in JVM. Per proteggere il sistema da un potenziale attacco Denial of Service dovuto a questa situazione, configurare la dimensione massima utilizzando il parametro **[!UICONTROL Max Content Size (uncompressed)]** per **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** in Configuration Manager. Se la dimensione non compressa della risorsa supera il valore configurato, le richieste di download della risorsa vengono rifiutate. Il valore predefinito è 100 MB.

1. Fai clic sul logo [!DNL Experience Manager] e passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console Web]**.
1. Dalla console Web, individua la configurazione **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]**.
1. Apri la configurazione **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** in modalità di modifica e cambia il valore del parametro in **[!UICONTROL Max Content Size (uncompressed)]**.

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. Salva le modifiche.

## Best practice e risoluzione dei problemi {#best-practices-and-troubleshooting}

* Le cartelle di risorse o le raccolte il cui nome contiene uno spazio vuoto potrebbero non essere condivise.
* Se gli utenti non riescono a scaricare le risorse condivise, verifica con l&#39;amministratore [!DNL Experience Manager] i [limiti di download](#configure-maximum-data-size).
* Se non riesci a inviare messaggi di posta elettronica con collegamenti a risorse condivise o se gli altri utenti non possono ricevere i tuoi messaggi di posta elettronica, rivolgiti al tuo amministratore [!DNL Experience Manager] per sapere se il servizio di posta elettronica [è configurato o meno.](#configure-day-cq-mail-service)
* Se non riesci a condividere le risorse utilizzando la funzionalità di condivisione dei collegamenti, assicurati di disporre delle autorizzazioni appropriate. Consulta [condividere risorse](#share-assets).
* Se una risorsa condivisa viene spostata in una posizione diversa, il relativo collegamento non funziona più. Ricreare il collegamento e condividerlo nuovamente con gli utenti.

* Se si desidera condividere collegamenti dalla distribuzione Autore [!DNL Experience Manager] ad entità esterne, assicurarsi di esporre solo i seguenti URL utilizzati per la condivisione dei collegamenti, solo per le richieste `GET`. Blocca altri URL per motivi di sicurezza.

   * `http://[aem_server]:[port]/linkshare.html`
   * `http://[aem_server]:[port]/linksharepreview.html`
   * `http://[aem_server]:[port]/linkexpired.html`

  Nell&#39;interfaccia [!DNL Experience Manager], accedere a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console Web]**. Apri la configurazione di **[!UICONTROL Day CQ Link Externalizer]** e modifica le seguenti proprietà nel campo **[!UICONTROL Domains]** con i valori indicati rispetto a `local`, `author` e `publish`. Per le proprietà `local` e `author`, fornisci l&#39;URL rispettivamente per le istanze Local e Author. Se si esegue una singola istanza Autore [!DNL Experience Manager], utilizzare lo stesso valore per le proprietà `local` e `author`. Per le istanze Publish, fornire l&#39;URL dell&#39;istanza Publish [!DNL Experience Manager].
