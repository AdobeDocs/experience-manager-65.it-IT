---
title: SSL per impostazione predefinita
seo-title: SSL per impostazione predefinita
description: Scoprite come utilizzare SSL per impostazione predefinita in AEM.
seo-description: Scoprite come utilizzare SSL per impostazione predefinita in AEM.
uuid: 2fbfd020-1d33-4b22-b963-c698e62f5bf6
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
discoiquuid: 68077369-0549-4c0f-901b-952e323013ea
docset: aem65
translation-type: tm+mt
source-git-commit: 4b965d8f7814816126601f6366c1ba313e404538
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---


# SSL Per impostazione predefinita{#ssl-by-default}

Nel tentativo di migliorare continuamente la sicurezza dei AEM,  Adobe ha introdotto una funzione chiamata SSL By Default. Lo scopo è incoraggiare l&#39;uso di HTTPS per connettersi alle istanze AEM.

## Abilitazione di SSL per impostazione predefinita {#enabling-ssl-by-default}

Per iniziare a configurare SSL per impostazione predefinita, fai clic sul messaggio Inbox corrispondente nella schermata iniziale AEM. Per raggiungere la casella in entrata, premere l&#39;icona a forma di campana nell&#39;angolo superiore destro dello schermo. Quindi fare clic su **Visualizza tutto**. Verrà visualizzato un elenco di tutti gli avvisi ordinati in una vista a elenco.

Nell&#39;elenco, selezionare e aprire l&#39;avviso **Configura HTTPS**:

![chlimage_1-103](assets/chlimage_1-103.png)

>[!NOTE]
>
>Se l&#39;avviso **Configura HTTPS** non è presente nella casella in entrata, è possibile accedere direttamente alla procedura guidata HTTPS andando a *<http://serveraddress:serverport/libs/granite/security/content/sslConfig.html?item=configuration%2fconfiguressl&_charset_=utf-8>*

Per questa funzione è stato creato un utente di servizio denominato **ssl-service**. Una volta aperto l’avviso, verrà visualizzata la seguente procedura guidata di configurazione:

1. Innanzitutto, impostare le credenziali store. Queste sono le credenziali per l&#39;archivio chiavi dell&#39;utente di sistema **ssl-service** che conterrà la chiave privata e l&#39;archivio delle credenziali per il listener HTTPS.

   ![chlimage_1-104](assets/chlimage_1-104.png)

1. Una volta immesse le credenziali, fate clic su **Next** nell&#39;angolo superiore destro della pagina. Quindi, caricate la chiave privata e il certificato associati per la connessione SSL.

   ![chlimage_1-105](assets/chlimage_1-105.png)

   >[!NOTE]
   >
   >Per informazioni su come generare una chiave privata e un certificato da utilizzare con la procedura guidata, vedere [questa procedura](/help/sites-administering/ssl-by-default.md#generating-a-private-key-certificate-pair-to-use-with-the-wizard) di seguito.

1. Infine, specificate il nome host HTTPS e la porta TCP per il listener HTTPS.

   ![screen_shot_2018-07-25at31658pm](assets/screen_shot_2018-07-25at31658pm.png)

## Automatizzazione SSL per impostazione predefinita {#automating-ssl-by-default}

Sono disponibili tre modi per automatizzare SSL per impostazione predefinita.

### Tramite POST HTTP {#via-http-post}

Il primo metodo prevede l&#39;invio al server SSLSetup utilizzato dalla procedura guidata di configurazione:

```shell
POST /libs/granite/security/post/sslSetup.html
```

Puoi utilizzare il payload seguente nel tuo POST per automatizzare la configurazione:

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

Il servlet, come qualsiasi servlet POST Sling, risponderà con 200 OK o con un codice di stato HTTP di errore. Potete trovare i dettagli sullo stato nel corpo HTML della risposta.

Di seguito sono riportati alcuni esempi sia di una risposta corretta che di un errore.

**ESEMPIO**  DI SUCCESSO(status = 200):

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

**ESEMPIO**  DI ERRORE (stato = 500):

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

### Via pacchetto {#via-package}

In alternativa, potete automatizzare la configurazione SSL caricando un pacchetto che contiene già i seguenti elementi richiesti:

* Keystore dell&#39;utente ssl-service. Questo si trova in */home/users/system/security/ssl-service/keystore* nella directory archivio.
* La configurazione `GraniteSslConnectorFactory`

### Generazione di una coppia chiave/certificato privata da utilizzare con la procedura guidata {#generating-a-private-key-certificate-pair-to-use-with-the-wizard}

Di seguito è riportato un esempio per la creazione di un certificato autofirmato in formato DER utilizzabile dalla procedura guidata SSL.

>[!NOTE]
>
>L&#39;uso di un certificato autofirmato è ad esempio solo a scopo e non deve essere utilizzato in produzione.

1. Innanzitutto, create la chiave privata:

   ```shell
   openssl genrsa -aes256 -out localhostprivate.key 4096
   openssl rsa -in localhostprivate.key -out localhostprivate.key
   ```

1. Quindi, generate una richiesta di firma dei certificati (CSR) utilizzando la chiave privata:

   ```shell
   openssl req -sha256 -new -key localhostprivate.key -out localhost.csr -subj '/CN=localhost'
   ```

1. Generate il certificato SSL e firmatelo con la chiave privata. In questo esempio, scadrà tra un anno:

   ```shell
   openssl x509 -req -days 365 -in localhost.csr -signkey localhostprivate.key -out localhost.crt
   ```

Converti la chiave privata in formato DER. Questo perché la procedura guidata SSL richiede che la chiave sia in formato DER:

```shell
openssl pkcs8 -topk8 -inform PEM -outform DER -in localhostprivate.key -out localhostprivate.der -nocrypt
```

Infine, caricate **localhostprivate.der** come Chiave privata e **localhost.crt** come Certificato SSL al punto 2 della procedura guidata SSL grafica descritta all&#39;inizio di questa pagina.

### Aggiornamento della configurazione SSL tramite cURL {#updating-the-ssl-configuration-via-curl}

>[!NOTE]
>
>Per un elenco centralizzato di utili comandi cURL in AEM, vedere [Utilizzo di cURL con AEM](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/curl.html).

Potete anche automatizzare la configurazione SSL usando lo strumento cURL. A questo scopo, potete inserire i parametri di configurazione nel seguente URL:

*https://&lt;serveraddress>:&lt;serverport>/libs/granite/security/post/sslSetup.html*

Di seguito sono riportati i parametri che potete usare per modificare le varie impostazioni della procedura guidata di configurazione:

* `-F "keystorePassword=password"` - la password del keystore;

* `-F "keystorePasswordConfirm=password"` - confermare la password del keystore;

* `-F "truststorePassword=password"` - la password del trust store;

* `-F "truststorePasswordConfirm=password"` - confermare la password dell&#39;archivio attendibili;

* `-F "privatekeyFile=@localhostprivate.der"` - specificare la chiave privata;

* `-F "certificateFile=@localhost.crt"` - specificare il certificato;

* `-F "httpsHostname=host.example.com"`- specificare il nome host;
* `-F "httpsPort=8443"` - la porta su cui lavorerà il listener HTTPS.

>[!NOTE]
>
>Il modo più veloce per eseguire cURL per automatizzare la configurazione SSL è dalla cartella in cui si trovano i file DER e CRT. In alternativa, è possibile specificare il percorso completo negli argomenti `privatekeyFile` e certificateFile.
>
>È inoltre necessario essere autenticati per eseguire l&#39;aggiornamento, quindi assicurarsi di aggiungere il comando cURL con il parametro `-u user:passeword`.
>
>Il comando cURL post corretto dovrebbe essere simile al seguente:

```shell
curl -u user:password -F "keystorePassword=password" -F "keystorePasswordConfirm=password" -F "truststorePassword=password" -F "truststorePasswordConfirm=password" -F "privatekeyFile=@localhostprivate.der" -F "certificateFile=@localhost.crt" -F "httpsHostname=host.example.com" -F "httpsPort=8443" https://host:port/libs/granite/security/post/sslSetup.html
```

#### Più certificati utilizzando cURL {#multiple-certificates-using-curl}

Potete inviare il servlet a una catena di certificati ripetendo il parametro certificateFile come segue:

`-F "certificateFile=@root.crt" -F "certificateFile=@localhost.crt"..`

Dopo aver eseguito il comando, verificate che tutti i certificati siano stati inviati all&#39;archivio chiavi. Controllare l&#39;archivio di chiavi da:
[http://localhost:4502/libs/granite/security/content/userEditor.html/home/users/system/security/ssl-service](http://localhost:4502/libs/granite/security/content/userEditor.html/home/users/system/security/ssl-service)
