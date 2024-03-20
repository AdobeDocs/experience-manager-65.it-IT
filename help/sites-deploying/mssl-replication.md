---
title: Replica tramite SSL reciproco
description: Scopri come configurare l’AEM in modo che un agente di replica nell’istanza di authoring utilizzi SSL reciproco (MSSL) per connettersi all’istanza di pubblicazione. Utilizzando MSSL, l’agente di replica e il servizio HTTP sull’istanza Publish utilizzano i certificati per autenticarsi a vicenda.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
feature: Configuring
exl-id: 0a8d7831-d076-45cf-835c-8063ee13d6ba
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1319'
ht-degree: 4%

---

# Replica tramite SSL reciproco{#replicating-using-mutual-ssl}

Configura AEM in modo che un agente di replica nell’istanza di authoring utilizzi SSL reciproco (MSSL) per connettersi all’istanza di pubblicazione. Utilizzando MSSL, l’agente di replica e il servizio HTTP sull’istanza Publish utilizzano i certificati per autenticarsi a vicenda.

La configurazione di MSSL per la replica prevede l’esecuzione dei seguenti passaggi:

1. Crea o ottieni chiavi e certificati privati per le istanze di authoring e pubblicazione.
1. Installa le chiavi e i certificati nelle istanze di authoring e pubblicazione:

   * Autore: chiave privata dell’autore e certificato di pubblicazione.
   * Publish (Pubblicazione): chiave privata di pubblicazione e certificato dell’autore. Il certificato è associato all’account utente autenticato con l’agente di replica.

1. Configura il servizio HTTP basato su Jetty nell’istanza Publish.
1. Configura le proprietà di trasporto e SSL dell’agente di replica.

![chlimage_1-64](assets/chlimage_1-64.png)

Determinare quale account utente esegue la replica. Durante l’installazione del certificato dell’autore attendibile nell’istanza di pubblicazione, il certificato è associato a questo account utente.

## Ottenimento o creazione di credenziali per MSSL {#obtaining-or-creating-credentials-for-mssl}

È necessario disporre di una chiave privata e di un certificato pubblico per le istanze di authoring e pubblicazione:

* Le chiavi private devono essere contenute nel formato pkcs#12 o JKS.
* I certificati devono essere in formato PKCS#12 o JKS. È inoltre possibile aggiungere al Granite Truststore un certificato contenuto in formato &quot;CER&quot;.
* I certificati possono essere autofirmati o firmati da una CA riconosciuta.

### Formato JKS {#jks-format}

Genera una chiave privata e un certificato in formato JKS. La chiave privata viene memorizzata in un file KeyStore e il certificato viene memorizzato in un file TrustStore. Utilizzare [Java `keytool`](https://docs.oracle.com/javase/7/docs/technotes/tools/solaris/keytool.html) per creare entrambi.

Segui i passaggi seguenti utilizzando Java `keytool` per creare la chiave privata e le credenziali:

1. Genera una coppia di chiavi pubblica-privata in un KeyStore.
1. Creare o ottenere il certificato:

   * Autofirmato: esporta il certificato dal registro chiavi.
   * Firma CA: genera una richiesta di certificato e la invia alla CA.

1. Importa il certificato in un TrustStore.

Utilizza la procedura seguente per creare una chiave privata e un certificato autofirmato sia per le istanze di authoring che per quelle di pubblicazione. Utilizzare valori diversi per le opzioni dei comandi.

1. Aprire una finestra o un terminale della riga di comando. Per creare la coppia di chiavi pubblica-privata, immetti il comando seguente, utilizzando i valori delle opzioni della tabella seguente:

   ```shell
   keytool -genkeypair -keyalg RSA -validity 3650 -alias alias -keystore keystorename.keystore  -keypass key_password -storepass  store_password -dname "CN=Host Name, OU=Group Name, O=Company Name,L=City Name, S=State, C=Country_ Code"
   ```

   | Opzione | Autore | Pubblicazione |
   |---|---|---|
   | -alias | author | pubblicazione |
   | -keystore | author.keystore | publish.keystore |

1. Per esportare il certificato, immetti il comando seguente utilizzando i valori di opzione della tabella seguente:

   ```shell
   keytool -exportcert -alias alias -file cert_file -storetype jks -keystore keystore -storepass store_password
   ```

   | Opzione | Autore | Pubblicazione |
   |---|---|---|
   | -alias | author | pubblicazione |
   | -file | author.cer | publish.cer |
   | -keystore | author.keystore | publish.keystore |

### Formato pkcs#12 {#pkcs-format}

Genera una chiave privata e un certificato in formato pkcs#12. Utilizzare [openSSL](https://www.openssl.org/) per generarli. Per generare una chiave privata e una richiesta di certificato, utilizza la procedura descritta di seguito. Per ottenere il certificato, firma la richiesta con la tua chiave privata (certificato autofirmato) o invia la richiesta a una CA. Quindi, genera l’archivio pkcs#12 che contiene la chiave privata e il certificato.

1. Aprire una finestra o un terminale della riga di comando. Per creare la chiave privata, immetti il comando seguente, utilizzando i valori delle opzioni della tabella seguente:

   ```shell
   openssl genrsa -out keyname.key 2048
   ```

   | Opzione | Autore | Pubblicazione |
   |---|---|---|
   | -out | author.key | publish.key |

1. Per generare una richiesta di certificato, immetti il comando seguente, utilizzando i valori di opzione della tabella seguente:

   ```shell
   openssl req -new -key keyname.key -out key_request.csr
   ```

   | Opzione | Autore | Pubblicazione |
   |---|---|---|
   | -key | author.key | publish.key |
   | -out | author_request.csr | publish_request.csr |

   Firma la richiesta di certificato o la invia a una CA.

1. Per firmare la richiesta di certificato, immetti il comando seguente, utilizzando i valori delle opzioni della tabella seguente:

   ```shell
   openssl x509 -req -days 3650 -in key_request.csr -signkey keyname.key -out certificate.cer
   ```

   | Opzione | Autore | Pubblicazione |
   |---|---|---|
   | -signkey | author.key | publish.key |
   | -in | author_request.csr | publish_request.csr |
   | -out | author.cer | publish.cer |

1. Per aggiungere la chiave privata e il certificato firmato a un file pkcs#12, immetti il comando seguente, utilizzando i valori delle opzioni della tabella seguente:

   ```shell
   openssl pkcs12 -keypbe PBE-SHA1-3DES -certpbe PBE-SHA1-3DES -export -in certificate.cer -inkey keyname.key -out pkcs12_archive.pfx -name "alias"
   ```

   | Opzione | Autore | Pubblicazione |
   |---|---|---|
   | -inkey | author.key | publish.key |
   | -out | author.pfx | publish.pfx |
   | -in | author.cer | publish.cer |
   | -name | author | pubblicazione |

## Installare la chiave privata e TrustStore in Author {#install-the-private-key-and-truststore-on-author}

Installa i seguenti elementi nell’istanza di authoring:

* Chiave privata dell’istanza di authoring.
* Certificato dell’istanza Publish.

Per eseguire la procedura seguente, devi aver effettuato l’accesso come amministratore dell’istanza di authoring.

### Installare la chiave privata di authoring {#install-the-author-private-key}

1. Apri la pagina Gestione utente per l’istanza di authoring. ([http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html))
1. Per aprire le proprietà dell&#39;account utente, fare clic sul nome utente.
1. Se nell&#39;area Impostazioni account viene visualizzato il collegamento Crea registro chiavi, fare clic sul collegamento. Configurare una password e fare clic su OK.
1. Nell&#39;area Impostazioni account fare clic su Gestisci registro chiavi.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. Fai Clic Su Aggiungi Chiave Privata Da File Archivio Chiavi.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. Fai clic su Seleziona file archivio chiavi, quindi cerca e seleziona il file author.keystore o il file author.pfx se utilizzi pkcs#12, quindi fai clic su Apri.
1. Immettere un alias e la password per l&#39;archivio chiavi. Immetti l’alias e la password per la chiave privata, quindi fai clic su Invia.
1. Chiudere la finestra di dialogo Gestione registro chiavi.

   ![chlimage_1-67](assets/chlimage_1-67.png)

### Installare il certificato di pubblicazione {#install-the-publish-certificate}

1. Apri la pagina Gestione utente per l’istanza di authoring. ([http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html))
1. Per aprire le proprietà dell&#39;account utente, fare clic sul nome utente.
1. Se nell&#39;area Impostazioni account viene visualizzato il collegamento Crea TrustStore, fare clic sul collegamento, creare una password per il TrustStore e fare clic su OK.
1. Nell&#39;area Impostazioni account fare clic su Gestisci TrustStore.
1. Fare clic su Aggiungi certificato da file CER.

   ![chlimage_1-68](assets/chlimage_1-68.png)

1. Deseleziona l’opzione Mappa certificato a utente. Fai clic su Seleziona file di certificato, seleziona publish.cer, quindi fai clic su Apri.
1. Chiudere la finestra di dialogo Gestione TrustStore.

   ![chlimage_1-69](assets/chlimage_1-69.png)

## Installa chiave privata e TrustStore durante la pubblicazione {#install-private-key-and-truststore-on-publish}

Installa i seguenti elementi nell’istanza di pubblicazione:

* Chiave privata dell’istanza Publish.
* Certificato dell’istanza di authoring. Associa il certificato all’utente utilizzato per eseguire le richieste di replica.

Per eseguire la procedura seguente, devi aver effettuato l’accesso come amministratore dell’istanza Publish.

### Installare la chiave privata di pubblicazione {#install-the-publish-private-key}

1. Apri la pagina Gestione utente per l’istanza Publish. ([http://localhost:4503/libs/granite/security/content/useradmin.html](http://localhost:4503/libs/granite/security/content/useradmin.html))
1. Per aprire le proprietà dell&#39;account utente, fare clic sul nome utente.
1. Se nell&#39;area Impostazioni account viene visualizzato il collegamento Crea registro chiavi, fare clic sul collegamento. Configurare una password e fare clic su OK.
1. Nell&#39;area Impostazioni account fare clic su Gestisci registro chiavi.
1. Fai Clic Su Aggiungi Chiave Privata Da File Archivio Chiavi.
1. Fai clic su Seleziona file archivio chiavi, quindi cerca e seleziona il file publish.keystore o publish.pfx se utilizzi pkcs#12, quindi fai clic su Apri.
1. Immettere un alias e la password per l&#39;archivio chiavi. Immetti l’alias e la password per la chiave privata, quindi fai clic su Invia.
1. Chiudere la finestra di dialogo Gestione registro chiavi.

### Installare il certificato di authoring {#install-the-author-certificate}

1. Apri la pagina Gestione utente per l’istanza Publish. ([http://localhost:4503/libs/granite/security/content/useradmin.html](http://localhost:4503/libs/granite/security/content/useradmin.html))
1. Se nell&#39;area Archivio fonti attendibili globale viene visualizzato il collegamento Crea TrustStore, fare clic sul collegamento, creare una password per il TrustStore e fare clic su OK.
1. Nell&#39;area Impostazioni account fare clic su Gestisci TrustStore.
1. Fare clic su Aggiungi certificato da file CER.
1. Accertati che l’opzione Mappa certificato a utente sia selezionata. Fai clic su Seleziona file di certificato, seleziona author.cer, quindi fai clic su Apri.
1. Fare clic su Invia, quindi chiudere la finestra di dialogo Gestione TrustStore.

## Configurare il servizio HTTP al momento della pubblicazione {#configure-the-http-service-on-publish}

Configura le proprietà del servizio HTTP basato su Jetty Apache Felix sull’istanza Publish in modo che utilizzi HTTPS durante l’accesso a Granite Keystore. Il PID del servizio è `org.apache.felix.http`.

Nella tabella seguente sono elencate le proprietà OSGi che è necessario configurare per l’utilizzo della console web.

| Nome proprietà nella console web | Nome proprietà OSGi | Valore |
|---|---|---|
| Abilita HTTPS | org.apache.felix.https.enable | vero |
| Abilita HTTPS all&#39;utilizzo di Granite KeyStore | org.apache.felix.https.use.granite.keystore | vero |
| Porta HTTPS | org.osgi.service.http.port.secure | 8443 (o altra porta desiderata) |
| Certificato client | org.apache.felix.https.clientcertificate | &quot;Certificato client richiesto&quot; |

## Configurare l’agente di replica durante l’authoring {#configure-the-replication-agent-on-author}

Configura l’agente di replica nell’istanza di authoring per utilizzare il protocollo HTTPS durante la connessione all’istanza di pubblicazione. Per informazioni complete sulla configurazione degli agenti di replica, consulta [Configurazione degli agenti di replica](/help/sites-deploying/replication.md#configuring-your-replication-agents).

Per abilitare MSSL, configura le proprietà nella scheda Trasporto in base alla tabella seguente:

<table>
 <tbody>
  <tr>
   <th>Proprietà</th>
   <th>Valore</th>
  </tr>
  <tr>
   <td>URI</td>
   <td><p>https://server_name:SSL_port/bin/receive?sling:authRequestLogin=1</p> <p>Ad esempio:</p> <p>http://localhost:8443/bin/receive?sling:authRequestLogin=1</p> </td>
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

Dopo aver configurato l’agente di replica, verifica la connessione per determinare se MSSL è configurato correttamente.

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
