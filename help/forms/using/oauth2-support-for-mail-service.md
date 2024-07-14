---
title: Configurare l’autenticazione basata su OAuth2 per Microsoft&reg (Forms JEE OAuth); protocolli del server di posta Office 365
description: Configurare l’autenticazione basata su OAuth2 per Microsoft&reg (Forms JEE OAuth); protocolli del server di posta Office 365
exl-id: cd3da71f-892c-4fde-905f-71a64fb5d4e4
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 5%

---

# Integrare AEM Forms con i protocolli del server di posta Microsoft® Office 365 {#oauth2-support-for-the-microsoft-mail-server-protocols}

Per consentire alle organizzazioni di rispettare i requisiti e-mail sicuri, AEM Forms offre il supporto OAuth 2.0 per l’integrazione con i protocolli del server di posta Microsoft® Office 365. È possibile utilizzare il servizio di autenticazione di Azure Active Directory (Azure AD) OAuth 2.0 per connettersi con vari protocolli quali IMAP, POP o SMTP e accedere ai dati e-mail per gli utenti di Office 365. Di seguito sono riportate le istruzioni dettagliate per configurare i protocolli del server di posta Microsoft® Office 365 per l’autenticazione tramite il servizio OAuth 2.0:

1. Accedi a [https://portal.azure.com/](https://portal.azure.com/) e cerca **Azure Active Directory** nella barra di ricerca, quindi fai clic sul risultato.
In alternativa, è possibile passare direttamente a [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. Fai clic su **Aggiungi** > **Registrazione app** > **Nuova registrazione**.

   ![Registrazione app](/help/forms/using/assets/outh_outlook_microsoft_azure.png)

1. Compila le informazioni in base alle tue esigenze, quindi fai clic su **Registra**.
   ![Account supportato](/help/forms/using/assets/azure_suuportedaccountype.png)
Nel caso precedente, viene selezionata l&#39;opzione **Account in qualsiasi directory organizzativa (qualsiasi directory di Azure AD - Multitenant) e account Microsoft® personali (ad esempio, Skype, Xbox)**.

   >[!NOTE]
   >
   > * Per gli account **in qualsiasi directory organizzativa (qualsiasi directory di Azure AD - Multitenant)**, l&#39;Adobe consiglia di utilizzare un account di lavoro anziché un account di posta elettronica personale.
   > * **Solo account Microsoft® personali** applicazione non supportata.
   > * L&#39;Adobe consiglia di utilizzare l&#39;applicazione **Multi-tenant and personal Microsoft® account**.

1. Quindi, passa a **Certificati e segreti**, fai clic su **Nuovo segreto client** e segui i passaggi sullo schermo per creare un segreto. Assicurati di prendere nota di questo valore di segreto per un uso successivo.

   ![Chiave segreta](/help/forms/using/assets/azure_secretkey.png)

1. Per aggiungere le autorizzazioni, accedi all&#39;app appena creata e seleziona **Autorizzazioni API** > **Aggiungi un&#39;autorizzazione** > **Microsoft® Graph** > **Autorizzazioni delegate**.
1. Seleziona le caselle di controllo per le seguenti autorizzazioni per l&#39;app e fai clic su **Aggiungi autorizzazione**:

   * `IMAP.AccessUser.All`
   * `Mail.Read`
   * `offline_access`
   * `POP.AccessAsUser.All`
   * `SMTP.Send`
   * `User.Read`

   ![Autorizzazione API](/help/forms/using/assets/azure_apipermission.png)

1. Seleziona **Autenticazione** > **Aggiungi una piattaforma** > **Web** e nella sezione **Url di reindirizzamento** aggiungi uno dei seguenti URI (Universal Resource Identifier) come:
   * `https://login.microsoftonline.com/common/oauth2/nativeclient`
   * `http://localhost`

   In questo caso, `https://login.microsoftonline.com/common/oauth2/nativeclient` viene utilizzato come URI di reindirizzamento.

1. Fai clic su **Configura** dopo aver aggiunto ogni URL e configurato le impostazioni in base alle tue esigenze.
   ![URI reindirizzamento](/help/forms/using/assets/azure_redirecturi.png)

   >[!NOTE]
   >
   > È obbligatorio selezionare le caselle di controllo **Token di accesso** e **Token ID**.

1. Fare clic su **Panoramica** nel riquadro di sinistra e copiare i valori per **ID applicazione (client)**, **ID directory (tenant)** e **Segreto client** per un utilizzo successivo.

   ![Panoramica](/help/forms/using/assets/azure_overview.png)

## Generazione del codice di autorizzazione {#generating-the-authorization-code}

Successivamente, devi generare il codice di autorizzazione, descritto nei passaggi seguenti:

1. Apri il seguente URL nel browser dopo aver sostituito `clientID` con `<client_id>` e `redirect_uri` con l&#39;URI di reindirizzamento dell&#39;applicazione:

   ```https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=[clientid]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login```

   >[!NOTE]
   >
   > Se è presente la singola applicazione tenant, sostituire `common` con `[tenantid]` nell&#39;URL seguente per generare il codice di autorizzazione: `https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/authorize?client_id=[[clientid]]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20openid%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login`

1. Quando digiti l’URL indicato sopra, vieni reindirizzato alla schermata di accesso:
   ![Schermata di accesso](/help/forms/using/assets/azure_loginscreen.png)

1. Immetti l&#39;e-mail, fai clic su **Avanti** e viene visualizzata la schermata delle autorizzazioni dell&#39;app:

   ![Consenti autorizzazione](/help/forms/using/assets/azure_permission.png)

1. Quando consenti l&#39;autorizzazione, vieni reindirizzato a un nuovo URL come: `https://login.microsoftonline.com/common/oauth2/nativeclient?code=<code>&session_state=[session_id]`

1. Copiare il valore di `<code>` dall&#39;URL sopra indicato da `0.ASY...` a `&session_state` nell&#39;URL sopra indicato.

## Generazione del token di aggiornamento {#generating-the-refresh-token}

Successivamente, devi generare il token di aggiornamento, come descritto nei passaggi seguenti:

1. Apri il prompt dei comandi e utilizza il seguente comando cURL per ottenere refreshToken.

1. Sostituisci `clientID`, `client_secret` e `redirect_uri` con i valori per l&#39;applicazione insieme al valore di `<code>`:

   `curl -H "ContentType application/x-www-form-urlencoded" -d "client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]" -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token`

   >[!NOTE]
   >
   > Nell&#39;applicazione tenant singola, per generare il token di aggiornamento utilizzare il seguente comando cURL e sostituire `common` con `[tenantid]` in:
   >`curl -H "ContentType application/x-www-form-urlencoded" -d "client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]" -X POST https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/token`

1. Prendi nota del token di aggiornamento.

## Configurazione del servizio di posta elettronica con supporto OAuth 2.0 {#configureemailservice}

Ora configura il servizio e-mail al più recente server JEE accedendo all’interfaccia utente di amministrazione:

1. Vai a **Home** > **Servizio** > **Applicazione e servizi** > **Gestione servizi** > **Servizio e-mail**. Viene visualizzata la finestra **Servizio e-mail di configurazione**, configurata per l&#39;autenticazione di base.

   >[!NOTE]
   >
   > Per abilitare il servizio di autenticazione oAuth 2.0, è necessario selezionare **Se il server SMTP richiede l&#39;autenticazione (autenticazione SMTP)**.

1. Impostare **oAuth 2.0 Authentication Settings** come `True`.
1. Copia i valori di **ID client** e **Segreto client** dal portale di Azure.
1. Copia il valore del **Token di aggiornamento** generato.
1. Accedi a **Workbench** e cerca in **E-mail 1.0** da **Selezione attività**.
1. In E-mail 1.0 sono disponibili tre opzioni:
   * **Invia con documento**: invia e-mail con allegati singoli.
   * **Invia con mappa degli allegati**: invia e-mail con più allegati.
   * **Ricezione**: riceve un&#39;e-mail da IMAP.

   >[!NOTE]
   >
   >* Il protocollo Transport Security ha i seguenti valori validi: &#39;blank&#39;, &#39;SSL&#39; o &#39;TLS&#39;. Impostare i valori di **Sicurezza trasporto SMTP** e **Sicurezza trasporto ricezione** su **TLS** per abilitare il servizio di autenticazione oAuth.
   >* Il protocollo **POP3** non è supportato per OAuth durante l&#39;utilizzo degli endpoint di posta elettronica.

   ![Impostazioni connessione](/help/forms/using/assets/oauth_connectionsettings.png)

1. Verificare l&#39;applicazione selezionando **Invia con documento**.
1. Fornisci gli indirizzi **TO** e **From**.
1. Richiama l’applicazione e viene inviata un’e-mail utilizzando l’autenticazione 0Auth 2.0.

   >[!NOTE]
   >
   >Se lo desideri, puoi impostare l’autenticazione Auth 2.0 su autenticazione di base per un particolare processo in un workbench. Per eseguire questa operazione, impostare il valore **Autenticazione OAuth 2.0** su &#39;False&#39; in **Usa impostazioni globali** nella scheda **Impostazioni connessione**.

## Per abilitare le notifiche delle attività OAuth {#enable_oauth_task}

1. Vai a **Home** > **Servizi** > **Flusso di lavoro modulo** > **Impostazioni server** > **Impostazioni e-mail**
1. Per abilitare le notifiche delle attività OAuth, selezionare la casella di controllo **Abilita OAuth**.
1. Copia i valori di **ID client** e **Segreto client** dal portale di Azure.
1. Copia il valore del **Token di aggiornamento** generato.
1. Fai clic su **Salva** per salvare i dettagli.

   ![Notifica attività](/help/forms/using/assets/task_notification.png)

   >[!NOTE]
   >
   > Per ulteriori informazioni relative alle notifiche delle attività, [fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/content/forms/administrator-help/configuring-email-endpoints.html#create-an-email-endpoint-for-the-complete-task-service).

## Per configurare l’endpoint e-mail {#configure_email_endpoint}

1. Vai alla **Home** > **Servizi** > **Applicazione e servizi** > **Gestione endpoint**
1. Per configurare l&#39;endpoint e-mail, impostare **oAuth 2.0 Authentication Settings** come `True`.
1. Copia i valori di **ID client** e **Segreto client** dal portale di Azure.
1. Copia il valore del **Token di aggiornamento** generato.
1. Fai clic su **Salva** per salvare i dettagli.

   ![Impostazioni connessione](/help/forms/using/assets/oauth_emailendpoint.png)

   >[!NOTE]
   >
   > Per ulteriori informazioni sulla configurazione degli endpoint e-mail, fare clic su [Configura un endpoint e-mail](https://experienceleague.adobe.com/docs/experience-manager-65/content/forms/administrator-help/configuring-email-endpoints.html).

## Risoluzione dei problemi {#troubleshooting}

* Se il servizio di posta elettronica non funziona correttamente, provare a rigenerare `Refresh Token` come descritto in precedenza. L’implementazione del nuovo valore richiede alcuni minuti.

* Errore durante la configurazione dei dettagli del server di posta elettronica nell’endpoint e-mail tramite Workbench. Prova a configurare l’endpoint tramite l’interfaccia utente di amministrazione anziché Workbench.
