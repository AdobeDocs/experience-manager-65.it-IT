---
title: Condividere risorse tramite un collegamento
description: Condividere risorse, cartelle e raccolte come URL.
contentOwner: AG
role: User
feature: Link Sharing,Asset Management
exl-id: 20370b00-862e-4d04-af2f-7d1c74a842dd
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 6%

---

# Condividere la risorsa come collegamento {#asset-link-sharing}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/share-assets.html?lang=en) |
| AEM 6.5 | Questo articolo |

[!DNL Adobe Experience Manager Assets] consente di condividere risorse, cartelle e raccolte come URL con i membri dell’organizzazione e le entità esterne, inclusi partner e fornitori. La condivisione delle risorse tramite un collegamento rappresenta un modo pratico per rendere le risorse disponibili a terzi senza dover prima accedere a [!DNL Assets].

>[!PREREQUISITES]
>
>* Hai bisogno di `Edit ACL` autorizzazione per la cartella o la risorsa da condividere come collegamento.
>* Per inviare e-mail agli utenti, configura i dettagli del server SMTP in [Day CQ Mail Service](#configmailservice).


## Condividere le risorse {#share-assets}

Per generare l’URL per le risorse da condividere con gli utenti, utilizza [!UICONTROL Condivisione collegamenti] .

* Gli utenti con privilegi di amministratore o con autorizzazioni di lettura all’indirizzo `/var/dam/share` la posizione può visualizzare i collegamenti condivisi con loro.
* Gli utenti che dispongono delle autorizzazioni di lettura in `/var/dam/jobs/download` la posizione può scaricare risorse dal collegamento condiviso.

1. In [!DNL Assets] interfaccia utente, seleziona la risorsa da condividere come collegamento.

1. Dalla barra degli strumenti, fai clic su **[!UICONTROL Condividi collegamento]** ![icona condividi risorse](assets/do-not-localize/assets_share.png). Il collegamento che verrà creato dopo aver fatto clic su **[!UICONTROL Condividi]** viene visualizzato in anticipo in [!UICONTROL Condividi collegamento] campo. Il collegamento non viene creato finché non selezioni **[!UICONTROL Invia]**.

   ![Finestra di dialogo con Condivisione collegamenti](assets/share-assets-as-link.png)

   *Figura: Finestra di dialogo per condividere le risorse come collegamento.*

1. Nella casella dell’indirizzo e-mail della finestra di dialogo **[!UICONTROL Condivisione collegamenti]**, digita l’ID e-mail dell’utente con cui vuoi condividere il collegamento. Puoi aggiungere uno o più utenti.

   >[!NOTE]
   >
   >Se immetti un ID e-mail di un utente che non è membro della tua organizzazione, le parole [!UICONTROL Utente esterno] hanno il prefisso ID e-mail dell’utente.

1. In **[!UICONTROL Oggetto]** immettere un oggetto per la risorsa da condividere.

1. In **[!UICONTROL Messaggio]** immettere un messaggio facoltativo.

1. In **[!UICONTROL Scade]** , specifica una data e un’ora di scadenza per il collegamento in modo che non funzioni più. La scadenza predefinita del collegamento è un giorno.

   ![Imposta data di scadenza del collegamento condiviso](assets/Set-shared-link-expiration.png)

1. Per consentire agli utenti di scaricare la risorsa originale, seleziona **[!UICONTROL Consenti download del file originale]**. Per consentire agli utenti di scaricare solo le rappresentazioni delle risorse condivise, seleziona **[!UICONTROL Consenti download delle rappresentazioni del file]**.

1. Clic **[!UICONTROL Condividi]**. Un messaggio conferma che il collegamento è condiviso con gli utenti tramite e-mail.

1. Per visualizzare la risorsa condivisa, fai clic sul collegamento nell’e-mail inviata all’utente. Per generare un’anteprima della risorsa, fai clic sulla risorsa condivisa. Per chiudere l&#39;anteprima, fare clic su **[!UICONTROL Indietro]**. Se hai condiviso una cartella, fai clic su **[!UICONTROL Cartella padre]** per tornare alla cartella principale.

   ![Anteprima della risorsa condivisa](assets/chlimage_1-546.png)

   >[!NOTE]
   >
   >[!DNL Experience Manager] supporta la generazione dell’anteprima delle risorse di solo [i tipi di file supportati](/help/assets/assets-formats.md). Se sono condivisi altri tipi MIME, puoi scaricare solo le risorse e non visualizzare l’anteprima.

1. Per scaricare la risorsa condivisa, fai clic su **[!UICONTROL Seleziona]** dalla barra degli strumenti, fai clic sulla risorsa, quindi fai clic su **[!UICONTROL Scarica]** dalla barra degli strumenti.

   ![Opzione barra degli strumenti per scaricare la risorsa condivisa](assets/chlimage_1-547.png)

1. Per visualizzare le risorse condivise come collegamenti, vai al [!DNL Assets] e fare clic sul pulsante [!DNL Experience Manager] Logo. Scegli **[!UICONTROL Navigazione]**. Nel riquadro di spostamento scegliere **[!UICONTROL Collegamenti condivisi]** per visualizzare un elenco delle risorse condivise.

1. Per non condividere una risorsa, selezionala e fai clic su **[!UICONTROL Annulla condivisione]** dalla barra degli strumenti. Segue un messaggio di conferma. La voce relativa alla risorsa viene rimossa dall’elenco.

## Configurare il servizio di posta Day CQ {#configure-day-cq-mail-service}

1. Il giorno [!DNL Experience Manager] home page, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console web]**.
1. Dall’elenco dei servizi, individua **[!UICONTROL Day CQ Mail Service]**.
1. Clic **[!UICONTROL Modifica]** accanto al servizio e configura i seguenti parametri per **[!UICONTROL Day CQ Mail Service]** con i dati indicati insieme al loro nome:

   * Nome host server SMTP: nome host server e-mail
   * Porta server SMTP: porta server e-mail
   * Utente SMTP: nome utente del server e-mail
   * Password SMTP: password del server e-mail

   ![chlimage_1-263](assets/chlimage_1-548.png)

1. Fai clic su **[!UICONTROL Salva]**.

## Configurare la dimensione massima dei dati {#configure-maximum-data-size}

Quando scarichi risorse dal collegamento condiviso utilizzando la funzione Condivisione collegamenti, [!DNL Experience Manager] comprime la gerarchia delle risorse dal repository, quindi restituisce la risorsa in un file ZIP. Tuttavia, in assenza di limiti alla quantità di dati che è possibile comprimere in un file ZIP, enormi quantità di dati sono soggette a compressione, che causa errori di memoria esaurita in JVM. Per proteggere il sistema da un potenziale attacco Denial of Service dovuto a questa situazione, configurare la dimensione massima utilizzando **[!UICONTROL Dimensione massima contenuto (non compresso)]** parametro per **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** in Configuration Manager. Se la dimensione non compressa della risorsa supera il valore configurato, le richieste di download della risorsa vengono rifiutate. Il valore predefinito è 100 MB.

1. Fai clic su [!DNL Experience Manager] e quindi vai a **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console web]**.
1. Dalla console Web, individua il **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** configurazione.
1. Apri la configurazione **[!UICONTROL Day CQ DAM Adhoc Asset Share Proxy Servlet]** in modalità di modifica e cambia il valore del parametro in **[!UICONTROL Max Content Size (uncompressed)]**.

   ![chlimage_1-264](assets/chlimage_1-549.png)

1. Salva le modifiche.

## Best practice e risoluzione dei problemi {#best-practices-and-troubleshooting}

* Le cartelle di risorse o le raccolte il cui nome contiene uno spazio vuoto potrebbero non essere condivise.
* Se gli utenti non possono scaricare le risorse condivise, verifica con il tuo [!DNL Experience Manager] amministratore che cosa [limiti di download](#configure-maximum-data-size) sono.
* Se non riesci a inviare e-mail con collegamenti a risorse condivise o se gli altri utenti non possono ricevere il tuo indirizzo e-mail, verifica con il tuo [!DNL Experience Manager] amministratore se [servizio e-mail](#configure-day-cq-mail-service) è configurato o meno.
* Se non riesci a condividere le risorse utilizzando la funzionalità di condivisione dei collegamenti, assicurati di disporre delle autorizzazioni appropriate. Consulta [condividere risorse](#share-assets).
* Se una risorsa condivisa viene spostata in una posizione diversa, il relativo collegamento non funziona più. Ricreare il collegamento e condividerlo nuovamente con gli utenti.

* Se desideri condividere i collegamenti dal tuo [!DNL Experience Manager] Distribuzione dell’authoring ad entità esterne, accertati di esporre solo i seguenti URL utilizzati per la condivisione dei collegamenti, per `GET` solo richieste. Blocca altri URL per motivi di sicurezza.

   * `http://[aem_server]:[port]/linkshare.html`
   * `http://[aem_server]:[port]/linksharepreview.html`
   * `http://[aem_server]:[port]/linkexpired.html`
   In entrata [!DNL Experience Manager] interfaccia, accesso **[!UICONTROL Strumenti]** > **[!UICONTROL Operazioni]** > **[!UICONTROL Console web]**. Apri **[!UICONTROL Day CQ Link Externalizer]** e modificare le seguenti proprietà in **[!UICONTROL Domini]** campo con i valori indicati a fronte `local`, `author`, e `publish`. Per `local` e `author` , forniscono l&#39;URL per le istanze locale e Autore, rispettivamente. Se si esegue un singolo [!DNL Experience Manager] Autore, utilizza lo stesso valore per `local` e `author` proprietà. Per le istanze Publish, fornisci l’URL del [!DNL Experience Manager] Istanza di pubblicazione.
