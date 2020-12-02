---
title: Replica mediante SSL reciproco
seo-title: Replica mediante SSL reciproco
description: Scoprite come configurare AEM in modo che un agente di replica nell’istanza di creazione utilizzi SSL (MSSL) reciproco per connettersi all’istanza di pubblicazione. Utilizzando MSSL, l’agente di replica e il servizio HTTP nell’istanza di pubblicazione utilizzano i certificati per l’autenticazione reciproca.
seo-description: Scoprite come configurare AEM in modo che un agente di replica nell’istanza di creazione utilizzi SSL (MSSL) reciproco per connettersi all’istanza di pubblicazione. Utilizzando MSSL, l’agente di replica e il servizio HTTP nell’istanza di pubblicazione utilizzano i certificati per l’autenticazione reciproca.
uuid: f4bc5e61-a58c-4fd2-9a24-b31e0c032c15
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 8bc307d9-fa5c-44c0-bff9-2d68d32a253b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1456'
ht-degree: 3%

---


# Replica con SSL reciproco{#replicating-using-mutual-ssl}

Configurate AEM in modo che un agente di replica nell’istanza di creazione utilizzi SSL (MSSL) reciproco per connettersi all’istanza di pubblicazione. Utilizzando MSSL, l’agente di replica e il servizio HTTP nell’istanza di pubblicazione utilizzano i certificati per l’autenticazione reciproca.

La configurazione di MSSL per la replica prevede l&#39;esecuzione dei seguenti passaggi:

1. Create o ottenete chiavi e certificati privati per le istanze di creazione e pubblicazione.
1. Installate le chiavi e i certificati nelle istanze di creazione e pubblicazione:

   * Autore: Chiave privata dell&#39;autore e certificato di pubblicazione.
   * Pubblicato: Chiave privata di Publish e certificato di Autore. Il certificato è associato all&#39;account utente autenticato con l&#39;agente di replica.

1. Configurare il servizio HTTP basato su Jetty sull’istanza Pubblica.
1. Configurare le proprietà di trasporto e SSL dell&#39;agente di replica.

![chlimage_1-64](assets/chlimage_1-64.png)

È necessario determinare l&#39;account utente che esegue la replica. Durante l&#39;installazione del certificato di authoring attendibile nell&#39;istanza di pubblicazione, il certificato è associato a questo account utente.

## Ottenimento o creazione di credenziali per MSSL {#obtaining-or-creating-credentials-for-mssl}

È necessario disporre di una chiave privata e di un certificato pubblico per le istanze di creazione e pubblicazione:

* Le chiavi private devono essere contenute nel formato pkcs#12 o JKS.
* I certificati devono essere contenuti nel formato pkcs#12 o JKS. È inoltre possibile aggiungere al Granite Truststore anche certificati contenuti in formato &quot;CER&quot;.
* I certificati possono essere autofirmati o firmati da una CA riconosciuta.

### Formato JKS {#jks-format}

Generate una chiave privata e un certificato in formato JKS. La chiave privata è memorizzata in un file KeyStore e il certificato è memorizzato in un file TrustStore. Utilizzate [Java `keytool`](https://docs.oracle.com/javase/7/docs/technotes/tools/solaris/keytool.html) per creare entrambi.

Per creare la chiave privata e la credenziale, eseguite i seguenti passaggi utilizzando Java `keytool`:

1. Generare una coppia di chiavi pubblica-privata in un KeyStore.
1. Create o ottenete il certificato:

   * Autofirmato: Esportate il certificato da KeyStore.
   * Firma CA: Generare una richiesta di certificato e inviarla alla CA.

1. Importa il certificato in un TrustStore.

Per creare una chiave privata e un certificato autofirmato per entrambe le istanze di creazione e pubblicazione, utilizzate la procedura seguente. Utilizzare valori diversi per le opzioni di comando di conseguenza.

1. Aprire una finestra della riga di comando o un terminale. Per creare la coppia di chiavi pubblica-privata, immettete il comando seguente, utilizzando i valori delle opzioni della tabella seguente:

   ```shell
   keytool -genkeypair -keyalg RSA -validity 3650 -alias alias -keystore keystorename.keystore  -keypass key_password -storepass  store_password -dname "CN=Host Name, OU=Group Name, O=Company Name,L=City Name, S=State, C=Country_ Code"
   ```

   | Opzione | Autore | Pubblicazione |
   |---|---|---|
   | -alias | author | pubblicazione |
   | -keystore | author.keystore | publish.keystore |

1. Per esportare il certificato, immettete il comando seguente utilizzando i valori delle opzioni della tabella seguente:

   ```shell
   keytool -exportcert -alias alias -file cert_file -storetype jks -keystore keystore -storepass store_password
   ```

   | Opzione | Autore | Pubblicazione |
   |---|---|---|
   | -alias | author | pubblicazione |
   | -file | author.cer | publish.cer |
   | -keystore | author.keystore | publish.keystore |

### pkcs#12 Formato {#pkcs-format}

Generate una chiave privata e un certificato in formato pkcs#12. Utilizzate [openSSL](https://www.openssl.org/) per generarli. Utilizzate la procedura seguente per generare una chiave privata e una richiesta di certificato. Per ottenere il certificato, firmate la richiesta con la vostra chiave privata (certificato autofirmato) o inviate la richiesta a una CA. Quindi, generate l&#39;archivio pkcs#12 che contiene la chiave privata e il certificato.

1. Aprire una finestra della riga di comando o un terminale. Per creare la chiave privata, immettete il comando seguente, utilizzando i valori delle opzioni della tabella seguente:

   ```shell
   openssl genrsa -out keyname.key 2048
   ```

   | Opzione | Autore | Pubblicazione |
   |---|---|---|
   | -out | author.key | publish.key |

1. Per generare una richiesta di certificato, immettete il comando seguente, utilizzando i valori delle opzioni della tabella seguente:

   ```shell
   openssl req -new -key keyname.key -out key_request.csr
   ```

   | Opzione | Autore | Pubblicazione |
   |---|---|---|
   | -key | author.key | publish.key |
   | -out | author_request.csr | publish_request.csr |

   Firmare la richiesta del certificato o inviare la richiesta a una CA.

1. Per firmare la richiesta del certificato, immettete il comando seguente, utilizzando i valori delle opzioni della tabella seguente:

   ```shell
   openssl x509 -req -days 3650 -in key_request.csr -signkey keyname.key -out certificate.cer
   ```

   | Opzione | Autore | Pubblicazione |
   |---|---|---|
   | -signkey | author.key | publish.key |
   | -in | author_request.csr | publish_request.csr |
   | -out | author.cer | publish.cer |

1. Per aggiungere la chiave privata e il certificato firmato a un file pkcs#12, immettete il comando seguente, utilizzando i valori delle opzioni della tabella seguente:

   ```shell
   openssl pkcs12 -keypbe PBE-SHA1-3DES -certpbe PBE-SHA1-3DES -export -in certificate.cer -inkey keyname.key -out pkcs12_archive.pfx -name "alias"
   ```

   | Opzione | Autore | Pubblicazione |
   |---|---|---|
   | -inkey | author.key | publish.key |
   | -out | author.pfx | publish.pfx |
   | -in | author.cer | publish.cer |
   | -name | author | pubblicazione |

## Installare la chiave privata e TrustStore sull&#39;autore {#install-the-private-key-and-truststore-on-author}

Installate i seguenti elementi nell’istanza di creazione:

* La chiave privata dell’istanza di creazione.
* Il certificato dell’istanza di pubblicazione.

Per eseguire la procedura seguente, è necessario aver effettuato l’accesso come amministratore dell’istanza di creazione.

### Installare la chiave privata Author {#install-the-author-private-key}

1. Aprite la pagina Gestione utente per l’istanza di creazione. ([http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html))
1. Per aprire le proprietà dell’account utente, toccate o fate clic sul nome utente.
1. Se nell&#39;area Impostazioni account viene visualizzato il collegamento Create KeyStore, fate clic sul collegamento. Configurare una password e fare clic su OK.
1. Nell&#39;area Impostazioni account, fate clic su Gestisci archivio chiavi.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. Fare Clic Su Aggiungi Chiave Privata Dal File Dell&#39;Archivio Chiave.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. Fate clic su Seleziona file archivio chiavi, quindi individuate e selezionate il file author.keystore o il file author.pfx se utilizzate pkcs#12, quindi fate clic su Apri.
1. Immettere un alias e la password per l&#39;archivio chiavi. Immettete l’alias e la password per la chiave privata, quindi fate clic su Invia.
1. Chiudere la finestra di dialogo Gestione archivio chiavi.

   ![chlimage_1-67](assets/chlimage_1-67.png)

### Installare il certificato di pubblicazione {#install-the-publish-certificate}

1. Aprite la pagina Gestione utente per l’istanza di creazione. ([http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html))
1. Per aprire le proprietà dell’account utente, toccate o fate clic sul nome utente.
1. Se nell&#39;area Impostazioni account viene visualizzato il collegamento Create TrustStore, fate clic sul collegamento, create una password per TrustStore e fate clic su OK.
1. Nell&#39;area Impostazioni account, fate clic su Gestisci TrustStore.
1. Fare clic su Aggiungi certificato da file CER.

   ![chlimage_1-68](assets/chlimage_1-68.png)

1. Deselezionate l’opzione Mappa certificato all’utente. Fate clic su Seleziona file certificato, selezionate publish.cer e fate clic su Apri.
1. Chiudere la finestra di dialogo Gestione TrustStore.

   ![chlimage_1-69](assets/chlimage_1-69.png)

## Installa la chiave privata e TrustStore su Pubblica {#install-private-key-and-truststore-on-publish}

Installate i seguenti elementi nell’istanza di pubblicazione:

* La chiave privata dell’istanza di pubblicazione.
* Il certificato dell’istanza di creazione. Associate il certificato all&#39;utente utilizzato per eseguire le richieste di replica.

Per eseguire la procedura seguente, è necessario aver eseguito l’accesso come amministratore dell’istanza di pubblicazione.

### Installare la chiave privata di pubblicazione {#install-the-publish-private-key}

1. Aprite la pagina Gestione utente per l’istanza di pubblicazione. ([http://localhost:4503/libs/granite/security/content/useradmin.html](http://localhost:4503/libs/granite/security/content/useradmin.html))
1. Per aprire le proprietà dell’account utente, toccate o fate clic sul nome utente.
1. Se nell&#39;area Impostazioni account viene visualizzato il collegamento Create KeyStore, fate clic sul collegamento. Configurare una password e fare clic su OK.
1. Nell&#39;area Impostazioni account, fate clic su Gestisci archivio chiavi.
1. Fare Clic Su Aggiungi Chiave Privata Dal File Dell&#39;Archivio Chiave.
1. Fate clic su Seleziona file archivio chiavi, quindi individuate e selezionate il file publish.keystore o il file publish.pfx se utilizzate pkcs#12, quindi fate clic su Apri.
1. Immettere un alias e la password per l&#39;archivio chiavi. Immettete l’alias e la password per la chiave privata, quindi fate clic su Invia.
1. Chiudere la finestra di dialogo Gestione archivio chiavi.

### Installare il certificato di authoring {#install-the-author-certificate}

1. Aprite la pagina Gestione utente per l’istanza di pubblicazione. ([http://localhost:4503/libs/granite/security/content/useradmin.html](http://localhost:4503/libs/granite/security/content/useradmin.html))
1. Individuate l&#39;account utente utilizzato per eseguire le richieste di replica, quindi toccate o fate clic sul nome utente.
1. Se nell&#39;area Impostazioni account viene visualizzato il collegamento Create TrustStore, fate clic sul collegamento, create una password per TrustStore e fate clic su OK.
1. Nell&#39;area Impostazioni account, fate clic su Gestisci TrustStore.
1. Fare clic su Aggiungi certificato da file CER.
1. Accertatevi che l&#39;opzione Mappa certificato all&#39;utente sia selezionata. Fate clic su Seleziona file certificato, selezionate author.cer, quindi fate clic su Apri.
1. Fare clic su Invia, quindi chiudere la finestra di dialogo Gestione TrustStore.

## Configurare il servizio HTTP su Pubblica {#configure-the-http-service-on-publish}

Configurate le proprietà del servizio HTTP Apache Felix Jetty Basato sull’istanza di pubblicazione in modo che utilizzi HTTPS durante l’accesso a Granite Keystore. Il PID del servizio è `org.apache.felix.http`.

Nella tabella seguente sono elencate le proprietà OSGi che è necessario configurare se si utilizza la console Web.

| Nome proprietà sulla console Web | Nome proprietà OSGi | Valore |
|---|---|---|
| Abilita HTTPS | org.apache.felix.https.enable | vero |
| Abilita HTTPS per utilizzare Granite KeyStore | org.apache.felix.https.use.granite.keystore | vero |
| Porta HTTPS | org.osgi.service.http.port.secure | 8443 (o altra porta desiderata) |
| Certificato client | org.apache.felix.https.clientcertificate | &quot;Certificato client desiderato&quot; |

## Configurare l&#39;agente di replica sull&#39;autore {#configure-the-replication-agent-on-author}

Configurate l&#39;agente di replica nell&#39;istanza di creazione in modo che utilizzi il protocollo HTTPS quando ci si connette all&#39;istanza di pubblicazione. Per informazioni complete sulla configurazione degli agenti di replica, vedere [Configurazione degli agenti di replica](/help/sites-deploying/replication.md#configuring-your-replication-agents).

Per abilitare MSSL, configura le proprietà nella scheda Trasporto in base alla tabella seguente:

<table>
 <tbody>
  <tr>
   <th>Proprietà</th>
   <th>Valore</th>
  </tr>
  <tr>
   <td>URI</td>
   <td><p>https://server_name:SSL_port/bin/receive?sling:authRequestLogin=1</p> <p>Esempio:</p> <p>http://localhost:8443/bin/receive?sling:authRequestLogin=1</p> </td>
  </tr>
  <tr>
   <td>User</td>
   <td>Nessun valore</td>
  </tr>
  <tr>
   <td>Password</td>
   <td>Nessun valore</td>
  </tr>
  <tr>
   <td>SSL</td>
   <td>Autenticazione client</td>
  </tr>
 </tbody>
</table>

![chlimage_1-70](assets/chlimage_1-70.png)

Dopo aver configurato l&#39;agente di replica, verificate la connessione per determinare se MSSL è configurato correttamente.

```xml
29.08.2014 14:02:46 - Create new HttpClient for Default Agent
29.08.2014 14:02:46 - * HTTP Version: 1.1
29.08.2014 14:02:46 - * Using Client Auth SSL configuration *
29.08.2014 14:02:46 - adding header: Action:Test
29.08.2014 14:02:46 - adding header: Path:/content
29.08.2014 14:02:46 - adding header: Handle:/content
29.08.2014 14:02:46 - deserialize content for delivery
29.08.2014 14:02:46 - No message body: Content ReplicationContent.VOID is empty
29.08.2014 14:02:46 - Sending POST request to http://localhost:8443/bin/receive?sling:authRequestLogin=1
29.08.2014 14:02:46 - sent. Response: 200 OK
29.08.2014 14:02:46 - ------------------------------------------------
29.08.2014 14:02:46 - Sending message to localhost:8443
29.08.2014 14:02:46 - >> POST /bin/receive HTTP/1.0
29.08.2014 14:02:46 - >> Action: Test
29.08.2014 14:02:46 - >> Path: /content
29.08.2014 14:02:46 - >> Handle: /content
29.08.2014 14:02:46 - >> Referer: about:blank
29.08.2014 14:02:46 - >> Content-Length: 0
29.08.2014 14:02:46 - >> Content-Type: application/octet-stream
29.08.2014 14:02:46 - --
29.08.2014 14:02:46 - << HTTP/1.1 200 OK
29.08.2014 14:02:46 - << Connection: Keep-Alive
29.08.2014 14:02:46 - << Server: Day-Servlet-Engine/4.1.64
29.08.2014 14:02:46 - << Content-Type: text/plain;charset=utf-8
29.08.2014 14:02:46 - << Content-Length: 26
29.08.2014 14:02:46 - << Date: Fri, 29 Aug 2014 18:02:46 GMT
29.08.2014 14:02:46 - << Set-Cookie: login-token=3529326c-1500-4888-a4a3-93d299726f28%3ac8be86c6-04bb-4d18-80d6-91278e08d720_98797d969258a669%3acrx.default; Path=/; HttpOnly; Secure
29.08.2014 14:02:46 - << Set-Cookie: cq-authoring-mode=CLASSIC; Path=/; Secure
29.08.2014 14:02:46 - <<
29.08.2014 14:02:46 - << R
29.08.2014 14:02:46 - << eplicationAction TEST ok.
29.08.2014 14:02:46 - Message sent.
29.08.2014 14:02:46 - ------------------------------------------------
29.08.2014 14:02:46 - Replication (TEST) of /content successful.
Replication test succeeded
```

