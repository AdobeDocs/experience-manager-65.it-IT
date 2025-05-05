---
title: SSL/TLS per impostazione predefinita
description: Scopri come utilizzare SSL come funzione predefinita in AEM 6.5.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
docset: aem65
exl-id: 574e2fc2-6ebf-49b6-9b65-928237a8a34d
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 9b766fe6e253782be3bc47849b4857216274ae20
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%

---

# SSL/TLS per impostazione predefinita{#ssl-tls-by-default}

Nel tentativo di migliorare continuamente la sicurezza dell&#39;AEM, Adobe ha introdotto una funzione chiamata SSL Per impostazione predefinita. L’obiettivo è incoraggiare l’utilizzo del protocollo HTTPS per connettersi alle istanze dell’AEM.

## Abilitazione di SSL/TLS per impostazione predefinita {#enabling-ssl-tls-by-default}

Puoi iniziare a configurare SSL/TLS per impostazione predefinita facendo clic sul messaggio della casella in entrata corrispondente nella schermata iniziale dell’AEM. Per raggiungere la Casella in entrata, premi l’icona a forma di campana nell’angolo superiore destro dello schermo. Quindi fare clic su **Visualizza tutto**. Viene visualizzato un elenco di tutti gli avvisi ordinati in una vista a elenco.

Nell&#39;elenco, selezionare e aprire l&#39;avviso **Configura HTTPS**:

![chlimage_1-103](assets/chlimage_1-103.png)

>[!NOTE]
>
>Se l&#39;avviso **Configura HTTPS** non è presente nella cartella Posta in arrivo, è possibile passare direttamente alla procedura guidata HTTPS da *<http://serveraddress:serverport/libs/granite/security/content/sslConfig.html?item=configuration%2fconfiguressl&_charset_=utf-8>*

Per questa funzionalità è stato creato un utente del servizio denominato **ssl-service**. Dopo aver aperto l’avviso, segui la procedura guidata di configurazione seguente:

1. Impostare innanzitutto le credenziali dell&#39;archivio. Queste sono le credenziali per l&#39;archivio chiavi del servizio **ssl** del sistema dell&#39;utente che conterrà la chiave privata e l&#39;archivio fonti attendibili per il listener HTTPS.

   ![chlimage_1-104](assets/chlimage_1-104.png)

1. Dopo aver immesso le credenziali, fai clic su **Avanti** nell&#39;angolo superiore destro della pagina. Quindi, carica la chiave privata e il certificato associati per la connessione SSL/TLS.

   ![chlimage_1-105](assets/chlimage_1-105.png)

   >[!NOTE]
   >
   >Per informazioni su come generare una chiave privata e un certificato da utilizzare con la procedura guidata, vedi [questa procedura](/help/sites-administering/ssl-by-default.md#generating-a-private-key-certificate-pair-to-use-with-the-wizard) di seguito.

1. Infine, specifica il nome host HTTPS e la porta TCP per il listener HTTPS.

   ![schermata_shot_2018-07-25at31658pm](assets/screen_shot_2018-07-25at31658pm.png)

## Automatizzazione di SSL/TLS per impostazione predefinita {#automating-ssl-tls-by-default}

Esistono tre modi per automatizzare SSL/TLS per impostazione predefinita.

### Tramite HTTP POST {#via-http-post}

Il primo metodo prevede la pubblicazione nel server SSLSetup utilizzato dalla procedura guidata di configurazione:

```shell
POST /libs/granite/security/post/sslSetup.html
```

Per automatizzare la configurazione, puoi utilizzare il seguente payload nel POST:

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

Il servlet, come qualsiasi servlet POST di Sling, risponderà con 200 OK o un codice di stato HTTP di errore. Puoi trovare i dettagli sullo stato nel corpo HTML della risposta.

Di seguito sono riportati alcuni esempi sia di risposta corretta che di errore.

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
Take note of the key store password you provided. You need
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

In alternativa, puoi automatizzare la configurazione SSL/TLS caricando un pacchetto che contiene già gli elementi richiesti:

* Il keystore dell’utente ssl-service. Si trova in */home/users/system/security/ssl-service/keystore* nell&#39;archivio.
* Configurazione di `GraniteSslConnectorFactory`

### Generazione di una coppia chiave privata/certificato da utilizzare con la procedura guidata {#generating-a-private-key-certificate-pair-to-use-with-the-wizard}

Di seguito è riportato un esempio per la creazione di un certificato autofirmato in formato DER che può essere utilizzato dalla procedura guidata SSL/TLS. Installa OpenSSL in base al sistema operativo, apri il prompt dei comandi OpenSSL e cambia la directory con la cartella in cui desideri generare la chiave privata o il certificato.

>[!NOTE]
>
>L’utilizzo di un certificato autofirmato ha solo scopo esemplificativo. Non utilizzare in produzione.

1. Innanzitutto, crea la chiave privata:

   ```shell
   openssl genrsa -aes256 -out localhostprivate.key 4096
   openssl rsa -in localhostprivate.key -out localhostprivate.key
   ```

1. Quindi, genera una richiesta di firma del certificato (CSR, Certificate Signing Request) utilizzando una chiave privata:

   ```shell
   openssl req -sha256 -new -key localhostprivate.key -out localhost.csr -subj "/CN=localhost"
   ```

1. Genera il certificato SSL/TLS e firmalo con la chiave privata. In questo esempio, scadrà tra un anno:

   ```shell
   openssl x509 -req -days 365 -in localhost.csr -signkey localhostprivate.key -out localhost.crt
   ```

1. Converti la chiave privata in formato DER. Questo perché la procedura guidata SSL richiede che la chiave sia in formato DER:

   ```shell
   openssl pkcs8 -topk8 -inform PEM -outform DER -in localhostprivate.key -out localhostprivate.der -nocrypt
   ```

1. Infine, carica **localhostprivate.der** come chiave privata e **localhost.crt** come certificato SSL/TLS nel passaggio 2 della procedura guidata SSL/TLS grafica descritta all&#39;inizio di questa pagina.

### Aggiornamento della configurazione SSL/TLS tramite cURL {#updating-the-ssl-tls-configuration-via-curl}

>[!NOTE]
>
>Per un elenco centralizzato di comandi cURL utili nell&#39;AEM, vedere [Utilizzo di cURL con AEM](https://helpx.adobe.com/it/experience-manager/6-4/sites/administering/using/curl.html).

Puoi anche automatizzare la configurazione SSL/TLS utilizzando lo strumento cURL. Per eseguire questa operazione, invia i parametri di configurazione a questo URL:

*https://&lt;serveraddress>:&lt;serverport>/libs/granite/security/post/sslSetup.html*

Di seguito sono riportati i parametri che è possibile utilizzare per modificare le varie impostazioni nella procedura guidata di configurazione:

* `-F "keystorePassword=password"` - password del keystore;

* `-F "keystorePasswordConfirm=password"` - confermare la password del keystore;

* `-F "truststorePassword=password"` - password del truststore;

* `-F "truststorePasswordConfirm=password"` - confermare la password del truststore;

* `-F "privatekeyFile=@localhostprivate.der"` - specificare la chiave privata;

* `-F "certificateFile=@localhost.crt"` - specificare il certificato;

* `-F "httpsHostname=host.example.com"`- specificare il nome host;
* `-F "httpsPort=8443"`: la porta su cui lavorerà il listener HTTPS.

>[!NOTE]
>
>Il modo più veloce per eseguire cURL per automatizzare la configurazione SSL/TLS è quello di utilizzare la cartella in cui si trovano i file DER e CRT. In alternativa, è possibile specificare il percorso completo negli argomenti `privatekeyFile` e certificateFile.
>
>Per eseguire l&#39;aggiornamento, è inoltre necessario essere autenticati, quindi assicurarsi di aggiungere il comando cURL con il parametro `-u user:passeword`.
>
>Un comando post cURL corretto dovrebbe essere simile al seguente:

```shell
curl -u user:password -F "keystorePassword=password" -F "keystorePasswordConfirm=password" -F "truststorePassword=password" -F "truststorePasswordConfirm=password" -F "privatekeyFile=@localhostprivate.der" -F "certificateFile=@localhost.crt" -F "httpsHostname=host.example.com" -F "httpsPort=8443" https://host:port/libs/granite/security/post/sslSetup.html
```

#### Più certificati utilizzando cURL {#multiple-certificates-using-curl}

Puoi inviare al servlet una catena di certificati ripetendo il parametro certificateFile come segue:

`-F "certificateFile=@root.crt" -F "certificateFile=@localhost.crt"..`

Dopo aver eseguito il comando, verifica che tutti i certificati siano stati inseriti nel keystore. Controlla le voci **Registro chiavi** da:
[http://localhost:4502/libs/granite/security/content/v2/usereditor.html/home/users/system/security/ssl-service](http://localhost:4502/libs/granite/security/content/v2/usereditor.html/home/users/system/security/ssl-service)

### Abilitazione di una connessione TLS 1.3 {#enabling-tls-connection}

1. Passa alla console Web
1. Quindi, passa a **OSGi** - **Configurazione** - **Adobe Granite SSL Connector Factory**
1. Vai al campo **Suite di crittografia incluse** e aggiungi le seguenti voci. È possibile confermare ogni aggiunta premendo il pulsante &quot;**+**&quot; a sinistra del campo, dopo averle aggiunte:

   * `TLS_AES_256_GCM_SHA384`
   * `TLS_AES_128_GCM_SHA256`
   * `TLS_CHACHA20_POLY1305_SHA256`
   * `TLS_AES_128_CCM_SHA256`
   * `TLS_AES_128_CCM_8_SHA256`
