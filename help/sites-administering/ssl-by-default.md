---
title: SSL/TLS per impostazione predefinita
seo-title: SSL/TLS By Default
description: Scopri come utilizzare SSL per impostazione predefinita in AEM.
seo-description: Learn how to use SSL by Default in AEM.
uuid: 2fbfd020-1d33-4b22-b963-c698e62f5bf6
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
discoiquuid: 68077369-0549-4c0f-901b-952e323013ea
docset: aem65
exl-id: 574e2fc2-6ebf-49b6-9b65-928237a8a34d
source-git-commit: 252924afb70dd311a27d04278fbe363db15e9519
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 0%

---

# SSL/TLS per impostazione predefinita{#ssl-tls-by-default}

Nel tentativo di migliorare continuamente la sicurezza di AEM, Adobe ha introdotto una funzione chiamata SSL By Default. Lo scopo è incoraggiare l’uso di HTTPS per connettersi alle istanze AEM.

## Abilitazione di SSL/TLS per impostazione predefinita {#enabling-ssl-tls-by-default}

Per impostazione predefinita, puoi iniziare a configurare SSL/TLS facendo clic sul messaggio corrispondente in entrata nella schermata iniziale AEM. Per raggiungere la casella in entrata, premere l&#39;icona della campana nell&#39;angolo superiore destro dello schermo. Quindi, fai clic su **Visualizza tutto**. Verrà visualizzato un elenco di tutti gli avvisi ordinati in una vista a elenco.

Nell’elenco, seleziona e apri le **Configura HTTPS** avviso:

![chlimage_1-103](assets/chlimage_1-103.png)

>[!NOTE]
>
>Se la **Configura HTTPS** L&#39;avviso non è presente nella casella in entrata, è possibile passare direttamente alla procedura guidata HTTPS andando a *<http://serveraddress:serverport/libs/granite/security/content/sslConfig.html?item=configuration%2fconfiguressl&_charset_=utf-8>*

Utente di un servizio denominato **servizio ssl** è stato creato per questa funzione. Una volta aperto l’avviso, verrà visualizzata la seguente procedura guidata di configurazione:

1. Impostare innanzitutto le credenziali dell&#39;archivio. Queste sono le credenziali per **servizio ssl** archivio chiavi dell&#39;utente del sistema che conterrà la chiave privata e l&#39;archivio di attendibilità per il listener HTTPS.

   ![chlimage_1-104](assets/chlimage_1-104.png)

1. Una volta immesse le credenziali, fai clic su **Successivo** nell’angolo superiore destro della pagina. Quindi, carica la chiave privata e il certificato associati per la connessione SSL.

   ![chlimage_1-105](assets/chlimage_1-105.png)

   >[!NOTE]
   >
   >Per informazioni su come generare una chiave privata e un certificato da utilizzare con la procedura guidata, consulta [presente procedura](/help/sites-administering/ssl-by-default.md#generating-a-private-key-certificate-pair-to-use-with-the-wizard) sotto.

1. Infine, specifica il nome host HTTPS e la porta TCP per il listener HTTPS.

   ![screen_shot_2018-07-25at31658pm](assets/screen_shot_2018-07-25at31658pm.png)

## Automazione di SSL/TLS per impostazione predefinita {#automating-ssl-tls-by-default}

Esistono tre modi per automatizzare SSL/TLS per impostazione predefinita.

### Tramite HTTP POST {#via-http-post}

Il primo metodo prevede la pubblicazione sul server SSLSetup utilizzato dalla configurazione guidata:

```shell
POST /libs/granite/security/post/sslSetup.html
```

Puoi utilizzare il seguente payload in POST per automatizzare la configurazione:

```xml
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="keystorePassword"

test
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="keystorePasswordConfirm"
test
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="truststorePassword"
test
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="truststorePasswordConfirm"
test
------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="privatekeyFile"; filename="server.der"
Content-Type: application/x-x509-ca-cert

------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="certificateFile"; filename="server.crt"
Content-Type: application/x-x509-ca-cert

------WebKitFormBoundaryyBO4ArmGlcfdGDbs
Content-Disposition: form-data; name="httpsPort"
8443
```

Il servlet, come qualsiasi servlet sling POST, risponderà con 200 OK o con un codice di stato HTTP di errore. Puoi trovare i dettagli sullo stato nel corpo HTML della risposta.

Di seguito sono riportati alcuni esempi di risposta corretta e di errore.

**ESEMPIO DI SUCCESSO** (stato = 200):

```xml
<!DOCTYPE html>
<html lang='en'>
<head>
<title>OK</title>
</head>
<body>
<h1>OK</h1>
<dl>
<dt class='foundation-form-response-status-code'>Status</dt>
<dd>200</dd>
<dt class='foundation-form-response-status-message'>Message</dt>
<dd>SSL successfully configured</dd>
<dt class='foundation-form-response-title'>Title</dt>
<dd>OK</dd>
<dt class='foundation-form-response-description'>Description</dt>
<dd>HTTPS has been configured on port 8443. The private key and
certificate were stored in the key store of the user ssl-service.
Please take note of the key store password you provided. You will need
it for any subsequent updating of the private key or certificate.</dd>
</dl>
<h2>Links</h2>
<ul class='foundation-form-response-links'>
<li><a class='foundation-form-response-redirect' href='/'>Done</a></li>
</ul>
</body>
</html>
```

**ESEMPIO DI ERRORE** (stato = 500):

```xml
<!DOCTYPE html>
<html lang='en'>
<head>
<title>Error</title>
</head>
<body>
<h1>Error</h1>
<dl>
<dt class='foundation-form-response-status-code'>Status</dt>
<dd>500</dd>
<dt class='foundation-form-response-status-message'>Message</dt>
<dd>The provided file is not a valid key, DER format expected</dd>
<dt class='foundation-form-response-title'>Title</dt>
<dd>Error</dd>
</dl>
</body>
</html>
```

### Tramite pacchetto {#via-package}

In alternativa, puoi automatizzare la configurazione SSL caricando un pacchetto che contiene già questi elementi richiesti:

* L&#39;archivio chiavi dell&#39;utente del servizio ssl. Si trova in */home/users/system/security/ssl-service/keystore* nel repository.
* La `GraniteSslConnectorFactory` configurazione

### Generazione di una coppia chiave/certificato privata da utilizzare con la procedura guidata {#generating-a-private-key-certificate-pair-to-use-with-the-wizard}

Di seguito è riportato un esempio per la creazione di un certificato autofirmato in formato DER utilizzabile dalla procedura guidata SSL/TLS. Installa OpenSSL basato sul sistema operativo, apri il prompt dei comandi OpenSSL e modifica la directory nella cartella in cui desideri generare la chiave privata/certificato.

>[!NOTE]
>
>L’uso di un certificato autofirmato è ad esempio limitato e non deve essere utilizzato in produzione.

1. Innanzitutto, crea la chiave privata:

   ```shell
   openssl genrsa -aes256 -out localhostprivate.key 4096
   openssl rsa -in localhostprivate.key -out localhostprivate.key
   ```

1. Quindi, genera una richiesta di firma del certificato (CSR, Certificate Signing Request) utilizzando una chiave privata:

   ```shell
   openssl req -sha256 -new -key localhostprivate.key -out localhost.csr -subj "/CN=localhost"
   ```

1. Genera il certificato SSL e firma con la chiave privata. In questo esempio, scadrà tra un anno:

   ```shell
   openssl x509 -req -days 365 -in localhost.csr -signkey localhostprivate.key -out localhost.crt
   ```

Converti la chiave privata in formato DER. Questo perché la procedura guidata SSL richiede che la chiave sia in formato DER:

```shell
openssl pkcs8 -topk8 -inform PEM -outform DER -in localhostprivate.key -out localhostprivate.der -nocrypt
```

Infine, carica il **localhostprivate.der** come chiave privata e **localhost.crt** come certificato SSL/TLS al passaggio 2 della procedura guidata grafica SSL/TLS descritta all’inizio di questa pagina.

### Aggiornamento della configurazione SSL/TLS tramite cURL {#updating-the-ssl-tls-configuration-via-curl}

>[!NOTE]
>
>Vedi [Utilizzo di cURL con AEM](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/curl.html) per un elenco centralizzato di comandi cURL utili in AEM.

Puoi anche automatizzare la configurazione SSL/TLS utilizzando lo strumento cURL. Per farlo, pubblica i parametri di configurazione in questo URL:

*https://&lt;serveraddress>:&lt;serverport>/libs/granite/security/post/sslSetup.html*

Di seguito sono riportati i parametri che è possibile utilizzare per modificare le varie impostazioni della procedura guidata di configurazione:

* `-F "keystorePassword=password"` - la password del keystore;

* `-F "keystorePasswordConfirm=password"` - confermare la password del keystore;

* `-F "truststorePassword=password"` - la password del truststore;

* `-F "truststorePasswordConfirm=password"` - confermare la password del truststore;

* `-F "privatekeyFile=@localhostprivate.der"` - specificare la chiave privata;

* `-F "certificateFile=@localhost.crt"` - specificare il certificato;

* `-F "httpsHostname=host.example.com"`- specificare il nome host;
* `-F "httpsPort=8443"` - la porta su cui funzionerà il listener HTTPS.

>[!NOTE]
>
>Il modo più veloce per eseguire cURL per automatizzare la configurazione SSL/TLS è dalla cartella in cui si trovano i file DER e CRT. In alternativa, è possibile specificare il percorso completo nel `privatekeyFile` e gli argomenti certificateFile.
>
>È inoltre necessario essere autenticati per eseguire l&#39;aggiornamento, quindi assicurati di aggiungere il comando cURL con il comando `-u user:passeword` parametro .
>
>Un comando post cURL corretto dovrebbe essere simile al seguente:

```shell
curl -u user:password -F "keystorePassword=password" -F "keystorePasswordConfirm=password" -F "truststorePassword=password" -F "truststorePasswordConfirm=password" -F "privatekeyFile=@localhostprivate.der" -F "certificateFile=@localhost.crt" -F "httpsHostname=host.example.com" -F "httpsPort=8443" https://host:port/libs/granite/security/post/sslSetup.html
```

#### Più certificati utilizzando cURL {#multiple-certificates-using-curl}

Puoi inviare al servlet una catena di certificati ripetendo il parametro certificateFile come riportato di seguito:

`-F "certificateFile=@root.crt" -F "certificateFile=@localhost.crt"..`

Dopo aver eseguito il comando, verifica che tutti i certificati siano stati inviati all&#39;archivio chiavi. Controlla il keystore da:
[http://localhost:4502/libs/granite/security/content/userEditor.html/home/users/system/security/ssl-service](http://localhost:4502/libs/granite/security/content/userEditor.html/home/users/system/security/ssl-service)

### Abilitazione di una connessione TLS 1.3 {#enabling-tls-connection}

1. Passa alla console Web
1. Quindi, passa a **OSGi** - **Configurazione** - **Adobe Granite SSL Connector Factory**
1. Vai a **Suite di cifratura incluse** e aggiungere le seguenti voci. È possibile confermare ogni aggiunta premendo il tasto &quot;**+**&quot; pulsante a sinistra del campo, dopo averli aggiunti in:

   * `TLS_AES_256_GCM_SHA384`
   * `TLS_AES_128_GCM_SHA256`
   * `TLS_CHACHA20_POLY1305_SHA256`
   * `TLS_AES_128_CCM_SHA256`
   * `TLS_AES_128_CCM_8_SHA256`