---
title: Configurazione dell'autenticazione basata su OAuth2 per i protocolli del server di posta di Microsoft® Office 365
description: Configurazione dell'autenticazione basata su OAuth2 per i protocolli del server di posta di Microsoft® Office 365
exl-id: cd3da71f-892c-4fde-905f-71a64fb5d4e4
source-git-commit: d19de2955adef56570378a6d62ec0015718f9039
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 3%

---

# Integrazione con i protocolli del server di posta Microsoft® Office 365 {#oauth2-support-for-the-microsoft-mail-server-protocols}

Per consentire alle organizzazioni di rispettare i requisiti e-mail sicuri, AEM Forms offre il supporto OAuth 2.0 per l’integrazione con i protocolli del server di posta Microsoft® Office 365. È possibile utilizzare il servizio di autenticazione di Azure Active Directory (Azure AD) OAuth 2.0 per connettersi con vari protocolli quali IMAP, POP o SMTP e accedere ai dati e-mail per gli utenti di Office 365. Di seguito sono riportate le istruzioni dettagliate per configurare i protocolli del server di posta Microsoft® Office 365 per l&#39;autenticazione tramite il servizio OAuth 2.0:

1. Login [https://portal.azure.com/](https://portal.azure.com/) e cerca **Azure Active Directory** nella barra di ricerca e fai clic sul risultato.
In alternativa, è possibile navigare direttamente in [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. Clic **Aggiungi** > **Registrazione app** > **Nuova registrazione**

   ![Registrazione app](/help/forms/using/assets/outh_outlook_microsoft_azure.png)

1. Inserisci le informazioni in base alle tue esigenze, quindi fai clic su **Registrati**.
   ![Account supportato](/help/forms/using/assets/azure_suuportedaccountype.png)
Nel caso di cui sopra, 
**Account in qualsiasi directory organizzativa (qualsiasi directory di Azure AD - Multitenant) e account Microsoft® personali (ad esempio, Skype, Xbox)** è selezionata.

   >[!NOTE]
   >
   > * Per **Account in qualsiasi directory organizzativa (qualsiasi directory di Azure AD - Multitenant)** dell&#39;applicazione, si consiglia di utilizzare l&#39;account aziendale anziché l&#39;account di posta elettronica personale.
   > * **Solo account Microsoft® personali** applicazione non supportata.
   > * Si consiglia di utilizzare **Account Microsoft® multi-tenant e personale** applicazione.


1. Quindi, vai a **Certificati e segreti**, fai clic su **Nuovo segreto client** e segui i passaggi sullo schermo per creare un segreto. Assicurati di prendere nota di questo valore di segreto per un uso successivo.

   ![Chiave segreta](/help/forms/using/assets/azure_secretkey.png)

1. Per aggiungere le autorizzazioni, vai alla nuova app creata e seleziona **Autorizzazioni API** > **Aggiungi un&#39;autorizzazione** > **Grafico Microsoft®** > **Autorizzazioni delegate**
1. Seleziona le caselle di controllo per le seguenti autorizzazioni per l’app e fai clic su **Aggiungi autorizzazione**:

   * `IMAP.AccessUser.All`
   * `Mail.Read`
   * `offline_access`
   * `POP.AccessAsUser.All`
   * `SMTP.Send`
   * `User.Read`

   ![Autorizzazione API](/help/forms/using/assets/azure_apipermission.png)

1. Seleziona **Autenticazione** > **Aggiungi una piattaforma** > **Web**, e nella **Url di reindirizzamento** , aggiungi uno dei seguenti URI (Universal Resource Identifier) come:
   * `https://login.microsoftonline.com/common/oauth2/nativeclient`
   * `http://localhost`

   In questo caso, `https://login.microsoftonline.com/common/oauth2/nativeclient` viene utilizzato come URI di reindirizzamento.

1. Clic **Configura** dopo aver aggiunto ogni URL e configurato le impostazioni in base alle tue esigenze.
   ![URI di reindirizzamento](/help/forms/using/assets/azure_redirecturi.png)

   >[!NOTE]
   >
   > È obbligatorio selezionare **Token di accesso** e **Token ID** caselle di controllo.

1. Clic **Panoramica** nel riquadro a sinistra e copiare i valori per **ID applicazione (client)**, **ID directory (tenant)**, e **Segreto client** per un uso successivo.

   ![Panoramica](/help/forms/using/assets/azure_overview.png)

## Generazione del codice di autorizzazione {#generating-the-authorization-code}

Successivamente, devi generare il codice di autorizzazione, descritto nei passaggi seguenti:

1. Apri il seguente URL nel browser dopo la sostituzione `clientID` con `<client_id>` e `redirect_uri` con l’URI di reindirizzamento dell’applicazione:

   ```https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=[clientid]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login```

   >[!NOTE]
   >
   > Nel caso della domanda unica del tenant, sostituire `common` con il `[tenantid]` nell’URL seguente per generare il codice di autorizzazione: `https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/authorize?client_id=[[clientid]]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20openid%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login`

1. Quando, immetti l’URL precedente, vieni reindirizzato alla schermata di accesso:
   ![Schermata di accesso](/help/forms/using/assets/azure_loginscreen.png)

1. Inserisci l’e-mail, fai clic su **Successivo** Viene visualizzata la schermata delle autorizzazioni di e app:

   ![Consenti autorizzazione](/help/forms/using/assets/azure_permission.png)

1. Dopo aver concesso l’autorizzazione, vieni reindirizzato a un nuovo URL come: `https://login.microsoftonline.com/common/oauth2/nativeclient?code=<code>&session_state=[session_id]`

1. Copia il valore di `<code>` dall’URL precedente da `0.ASY...` a `&session_state` nell’URL indicato sopra.

## Generazione del token di aggiornamento {#generating-the-refresh-token}

Successivamente, devi generare il token di aggiornamento, come descritto nei passaggi seguenti:

1. Apri il prompt dei comandi e utilizza il seguente comando cURL per ottenere refreshToken.

1. Sostituisci il `clientID`, `client_secret` e `redirect_uri` con i valori per l&#39;applicazione insieme al valore di `<code>`:

   `curl -H “ContentType application/x-www-form-urlencoded” -d “client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]” -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token`

   >[!NOTE]
   >
   > Nell’applicazione con un singolo tenant, per generare il token di aggiornamento utilizza il seguente comando cURL e sostituiscilo `common` con `[tenantid]` in:
   >`curl -H “ContentType application/x-www-form-urlencoded” -d “client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]” -X POST https://login.microsoftonline.com/[tenantid]/oauth2/v2.0/token`

1. Prendi nota del token di aggiornamento.

## Configurazione del servizio di posta elettronica con supporto OAuth 2.0 {#configureemailservice}

Ora è necessario configurare il servizio di posta elettronica al più tardi per il server JEE accedendo all’interfaccia utente di amministrazione:

1. Vai a **Home** > **Servizio** > **Applicazione e servizi** > **Gestione dei servizi** > **Servizio e-mail**, il **Servizio e-mail di configurazione** viene visualizzata la finestra, configurata per l&#39;autenticazione di base.

   >[!NOTE]
   >
   > Per abilitare il servizio di autenticazione oAuth 2.0, è necessario selezionare **Se il server SMTP richiede l&#39;autenticazione (autenticazione SMTP)** casella di controllo.

1. Imposta **Impostazioni autenticazione OAuth 2.0** as `True`.
1. Copia i valori di **ID client** e **Segreto client** dal portale di Azure.
1. Copia il valore di generato **Aggiorna token**.
1. Accedi a **Workbench** e ricerca **E-mail 1.0** da **Selettore attività**.
1. In E-mail 1.0 sono disponibili tre opzioni:
   * **Invia con documento**: invia e-mail con singoli allegati.
   * **Invia con mappa degli allegati**: invia e-mail con più allegati.
   * **Ricezione**: riceve un’e-mail da IMAP.

   >[!NOTE]
   >
   >* Il protocollo Transport Security ha valori validi come: &#39;blank&#39;, &#39;SSL&#39; o &#39;TLS&#39;. È necessario impostare i valori di **Sicurezza trasporto SMTP** e **Ricezione della sicurezza del trasporto** a **TLS** per abilitare il servizio di autenticazione OAuth.
   >* **Protocollo POP3** non è supportato per OAuth durante l’utilizzo di endpoint e-mail.


   ![Impostazioni di connessione](/help/forms/using/assets/oauth_connectionsettings.png)

1. Verificare l&#39;applicazione selezionando **Invia con documento**.
1. Fornire **A** e **Da** indirizzi.
1. Richiama l’applicazione e l’e-mail viene inviata utilizzando l’autenticazione 0Auth 2.0.

   >[!NOTE]
   >
   >Se si desidera modificare l&#39;impostazione Autenticazione 2.0 in Autenticazione di base per un particolare processo di un workbench, è possibile impostare **Autenticazione OAuth 2.0** valore come &#39;False&#39; in **Usa impostazioni globali** nel **Impostazioni di connessione** scheda.

## Per abilitare le notifiche delle attività OAuth {#enable_oauth_task}

1. Vai a **Home** > **Servizi** > **Flusso di lavoro modulo** > **Impostazioni server** > **Impostazioni e-mail**
1. Per abilitare le notifiche delle attività OAuth, seleziona la **Abilita OAuth** casella di controllo.
1. Copia i valori di **ID client** e **Segreto client** dal portale di Azure.
1. Copia il valore di generato **Aggiorna token**.
1. Clic **Salva** per salvare i dettagli.

   ![Notifica attività](/help/forms/using/assets/task_notification.png)

   >[!NOTE]
   >
   > Per ulteriori informazioni relative alle notifiche di attività, [fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/manage-endpoints/configuring-email-endpoints.html#create-an-email-endpoint-for-the-complete-task-service).

## Per configurare l’endpoint e-mail {#configure_email_endpoint}

1. Vai a **Home** > **Servizi** > **Applicazione e servizi** > **Gestione degli endpoint**
1. Per configurare l’endpoint e-mail, imposta **Impostazioni autenticazione OAuth 2.0** as `True`.
1. Copia i valori di **ID client** e **Segreto client** dal portale di Azure.
1. Copia il valore di generato **Aggiorna token**.
1. Clic **Salva** per salvare i dettagli.

   ![Impostazioni di connessione](/help/forms/using/assets/oauth_emailendpoint.png)

   >[!NOTE]
   >
   > Per ulteriori informazioni sulla configurazione degli endpoint e-mail, fai clic su [Configurare un endpoint e-mail](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/manage-endpoints/configuring-email-endpoints.html).

## Risoluzione dei problemi {#troubleshooting}

* Se il servizio di posta elettronica non funziona correttamente. Prova a rigenerare il `Refresh Token` come descritto in precedenza. L’implementazione del nuovo valore richiede alcuni minuti.

* Errore durante la configurazione dei dettagli del server di posta elettronica nell’endpoint e-mail utilizzando Workbench. Prova a configurare l’endpoint tramite l’interfaccia utente amministratore anziché Workbench.
