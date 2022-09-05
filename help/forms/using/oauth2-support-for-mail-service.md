---
title: Supporto OAuth2 per il servizio di posta
description: 'Supporto Oauth2 per il servizio di posta  '
source-git-commit: 081b0c70ceca0502cb84d7e1b68b0b12dc45a4e7
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 47%

---

# Supporto OAuth2 per il servizio di posta {#oauth2-support-for-the-mail-service}

AEM as a Cloud Service offre il supporto OAuth2 per il servizio di posta integrato, al fine di consentire alle organizzazioni di rispettare i requisiti e-mail sicuri.

Puoi configurare OAuth per più provider di posta elettronica. Di seguito sono riportate le istruzioni dettagliate per configurare il servizio di posta AEM per l’autenticazione tramite OAuth2 con Microsoft Office 365 Outlook. Altri fornitori possono essere configurati in modo simile.

## Microsoft Outlook {#microsoft-outlook}

1. Vai a [https://portal.azure.com/](https://portal.azure.com/) e accedi.
1. Cerca **Azure Active Directory** nella barra di ricerca e fai clic sul risultato. In alternativa, è possibile navigare direttamente in [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. Fai clic su **Registrazione app** - **Nuova registrazione**

   ![](/help/forms/using/assets/outh_outlook.PNG)

1. Compila le informazioni in base alle tue esigenze, quindi fai clic su **Registra**
1. Vai alla nuova app creata e seleziona **Autorizzazioni API**
1. Vai a **Aggiungi autorizzazione** - **Autorizzazione grafico** - **Autorizzazioni delegate**
1. Seleziona le seguenti autorizzazioni per la tua app, quindi fai clic su **Aggiungi autorizzazione**:
   * `SMTP.Send`
   * `Mail.Read`
   * `Mail.Send`
   * `openid`
   * `offline_access`
1. Vai a **Autenticazione** - **Aggiungi una piattaforma** - **Web** e nella sezione **URL di reindirizzamento** aggiungi i seguenti URL - uno con e uno senza una barra:
   * `http://localhost/`
   * `http://localhost`
1. Premi **Configura** dopo aver aggiunto ogni URL e configurato le impostazioni in base alle tue esigenze
1. Quindi, vai a **Certificati e segreti**, fai clic su **Nuovo segreto client** e segui i passaggi sullo schermo per creare un segreto. Assicurati di prendere nota di questo segreto per un uso successivo
1. Press **Panoramica** nel riquadro a sinistra e copia i valori per **ID applicazione (client)** per un uso successivo.

Per ricapitolare, è necessario disporre delle seguenti informazioni per configurare OAuth2 per il servizio di posta sul lato AEM:

* L’URL di autenticazione nel modulo: `https://login.microsoftonline.com/<ID>/oauth2/v2.0/authorize`
* L’URL del token nel modulo: `https://login.microsoftonline.com/<ID>/oauth2/v2.0/token`
* L’URL di aggiornamento nel modulo: `https://login.microsoftonline.com/<ID>/oauth2/v2.0/token`
* ID client
* Segreto client

### Generazione del token di aggiornamento {#generating-the-refresh-token}

Successivamente, devi generare il token di aggiornamento, come illustrato in un passaggio successivo.

Puoi eseguire questa operazione seguendo questi passaggi:

1. Apri il seguente URL nel browser dopo la sostituzione `clientID` con i valori specifici del tuo account:

   ```https://login.microsoftonline.com/common/oauth2/v2/authorize?client_id=<client_id>&scope=IMAP.AccessAsUser.A;;%20POP.AccessAsUser.All%20SMTP.Send%20User.Read&response_type=code&redirect-uri=http://loginmicrosoftonline.com/common/outh2/nativeclient&prompt=login```

1. Consentire l&#39;autorizzazione, laddove necessario.
1. L’URL verrà reindirizzato a una nuova posizione, costruita in questo formato: `http://localhost/?code=<code>&state=12345&session_state=4f984c6b-cc1f-47b9-81b2-66522ea83f81#`
1. Copia il valore di `<code>` nell’esempio precedente
1. Usa il seguente comando cURL per ottenere il refreshToken. Sostituisci clientID, clientSecret con i valori per il tuo account e il valore per `<code>`:

   ```
   curl -H “ContentType application/x-www-form-urlencoded” -d 
   "client_id=<client-id>
   &scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All&code=M.R3_BAY.1bf609bf-25b3-2fcd-d910-02e02c53bc
   &grant_type=authorization_code
   &redirect_uri= https://login.microsoftonline.com/common/oauth2/nativeclient
   &client_secret=~1E8Q~cz-m6vgOb9m~SI.eF9jSVTbFUiP5f0” -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token
   ```

1. Prendi nota di refreshToken e accessToken.

### Convalida dei token {#validating-the-tokens}

Prima di procedere alla configurazione di OAuth sul lato AEM, assicurati di convalidare sia accessToken che refreshToken con la procedura seguente:

1. Genera l’accessToken utilizzando il refreshToken prodotto nella procedura precedente. Puoi ottenere questo risultato con il seguente curl e sostituendo i valori per `<client_id>`,`<client_secret>` insieme al `<refreshToken>`:

   ```
   curl -H “ContentType application/x-www-form-urlencoded” -d 
   "client_id=<client_id>
   &scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All&code=<code>
   &grant_type=authorization_code
   &redirect_uri= https://login.microsoftonline.com/common/oauth2/nativeclient
   &client_secret=<client_secret>
   &refresh_token=<refresh_token” 
   -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token
   ```

1. Invia un messaggio di posta utilizzando accessToken per verificare se funziona correttamente.

>[!NOTE]
>
> Puoi ottenere la raccolta API Postman da [questa posizione](https://docs.microsoft.com/it-it/azure/active-directory/develop/v2-oauth2-auth-code-flow).

### Configurare il servizio e-mail con il supporto di Auth2.0 {#configureemailservice}

Ora devi configurare il servizio e-mail al server JEE più recente tramite l’accesso in Interfaccia utente amministratore:

1. Vai a **Pagina principale** - **Servizio** - **Applicazione e servizi** - **Gestione dei servizi** - **Servizio e-mail**
1. **Servizio e-mail di configurazione** viene visualizzata la finestra, configura **SMPT** e **IMP** server per l’autenticazione di base.
1. Per abilitare il servizio di autenticazione della posta di Outlook, selezionare **Impostazioni di autenticazione di Auth 2.0** casella di controllo.
1. Copia i valori di **ID client** e **Segreto client** dal portale di Azure.
1. Copia il valore di generato **Aggiorna token**.
1. Fai clic su **Salva** per salvare i dettagli.
1. Accedi a Workbench e cerca **Email 1.0** da **Selettore attività**.
1. In E-mail 1.0 sono disponibili tre opzioni:
   * **Invia con documento**: Invia e-mail con singoli allegati.
   * **Invia con mappa degli allegati**: Invia e-mail con più allegati.
   * **Ricezione**: Riceve un’e-mail da POP3 o IMAP.
1. Test dell&#39;applicazione selezionando **Invia con documento**
1. Fornire **A** e **Da** indirizzi.
1. Richiama l’applicazione e l’e-mail viene inviata utilizzando l’autenticazione oAuth2.0.

>[!NOTE]
>
> Se desideri modificare l’impostazione di autenticazione di Auth 2.0 in autenticazione di base per un particolare processo in un workbench, puoi deselezionare l’opzione **Autenticazione oAuth2.0** spunta sotto **Usa impostazioni globali** in **Impostazioni connessione** scheda .

### Risoluzione dei problemi {#troubleshooting}

Se il servizio di posta non funziona correttamente, rigenerare il `refreshToken` come descritto sopra. L’implementazione del nuovo valore richiede alcuni minuti.


