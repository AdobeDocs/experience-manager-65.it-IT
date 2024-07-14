---
title: Configurazione di SSL per il server applicazioni JBoss
description: Scopri come configurare SSL per il server applicazioni JBoss.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 8eb4f691-a66b-498e-8114-307221f63718
solution: Experience Manager, Experience Manager Forms
feature: Document Security
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 0%

---

# Configurazione di SSL per il server applicazioni JBoss {#configuring-ssl-for-jboss-application-server}

Per configurare SSL sul server applicazioni JBoss, è necessaria una credenziale SSL per l&#39;autenticazione. È possibile utilizzare lo strumento chiave Java per creare una credenziale o per richiedere e importare una credenziale da un&#39;autorità di certificazione (CA). Devi quindi abilitare SSL su JBoss.

È possibile eseguire keytool utilizzando un singolo comando che include tutte le informazioni necessarie per creare il keystore.

In questa procedura:

* `[appserver root]` è la home directory del server applicazioni che esegue i moduli AEM.
* `[type]` è un nome di cartella che varia a seconda del tipo di installazione eseguita.

## Creare una credenziale SSL {#create-an-ssl-credential}

1. Al prompt dei comandi passare alla *[JAVA HOME]*/bin e digitare il comando seguente per creare le credenziali e il keystore:

   `keytool -genkey -dname "CN=`*Nome host* `, OU=`*Nome gruppo* `, O=`*Nome società* `,L=`*Nome città* `, S=`*Stato* `, C=`Codice paese&quot; `-alias "AEMForms Cert"` `-keyalg RSA -keypass`*password_chiave* `-keystore`*nomechiave* `.keystore`

   >[!NOTE]
   >
   >Sostituisci `[JAVA_HOME]` con la directory in cui è installato JDK e sostituisci il testo in corsivo con i valori corrispondenti all&#39;ambiente. Nome host è il nome di dominio completo del server applicazioni.

1. Immettere `keystore_password` quando viene richiesta una password. La password per il keystore e la chiave devono essere identiche.

   >[!NOTE]
   >
   >Il `keystore_password` *immesso in questo passaggio può essere la stessa password (key_password) immessa nel passaggio 1 oppure può essere diverso.*

1. Copiare il file *keystorename*.keystore nella directory `[appserver root]/server/[type]/conf` digitando uno dei comandi seguenti:

   * (Windows Server Singolo) `copy` `keystorename.keystore[appserver root]\standalone\configuration`
   * (cluster Windows Server) copia `keystorename.keystore[appserver root]\domain\configuration`
   * (server singolo Linux) `cp keystorename.keystore [appserver root]/standalone/configuration`
   * (cluster di server Linux) `cp <em>keystorename</em>.keystore<em>[appserver root]</em>/domain/configuration`


1. Esporta il file del certificato digitando il comando seguente:

   * (Server singolo) `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/standalone/configuration/keystorename.keystore`
   * (cluster di server) `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/domain/configuration/keystorename.keystore`

1. Immetti *keystore_password* quando viene richiesta una password.
1. Copiare il file AEMForms_cert.cer nella directory principale *[appserver] \conf* digitando il comando seguente:

   * (Windows Server Singolo) `copy AEMForms_cert.cer [appserver root]\standalone\configuration`
   * (cluster Windows Server) `copy AEMForms_cert.cer [appserver root]\domain\configuration`
   * (server singolo Linux) `cp AEMForms _cert.cer [appserver root]\standalone\configuration`
   * (cluster di server Linux) `cp AEMForms _cert.cer [appserver root]\domain\configuration`

1. Visualizza il contenuto del certificato digitando il comando seguente:

   * `keytool -printcert -v -file [appserver root]\standalone\configuration\AEMForms_cert.cer`
   * `keytool -printcert -v -file [appserver root]\domain\configuration\AEMForms_cert.cer`

1. Per fornire l&#39;accesso in scrittura al file cacerts in `[JAVA_HOME]\jre\lib\security`, se necessario, eseguire l&#39;attività seguente:

   * (Windows) Fare clic con il pulsante destro del mouse sul file cacerts e selezionare Proprietà, quindi deselezionare l&#39;attributo di sola lettura.
   * (Linux) Tipo `chmod 777 cacerts`

1. Importa il certificato digitando il comando seguente:

   `keytool -import -alias "AEMForms Cert" -file`*AEMForms_cert* `.cer -keystore`*JAVA_HOME* `\jre\lib\security\cacerts`

1. Digitare `changeit` come password. Questa password è la password predefinita per un&#39;installazione Java e potrebbe essere stata modificata dall&#39;amministratore di sistema.
1. Quando viene richiesto `Trust this certificate? [no]`, digitare `yes`. Viene visualizzata la conferma &quot;Certificato aggiunto al keystore&quot;.
1. Se ti connetti tramite SSL da Workbench, installa il certificato sul computer Workbench.
1. In un editor di testo, apri i seguenti file per la modifica:

   * Server singolo - `[appserver root]`/standalone/configuration/lc_&lt;dbname/turnkey>.xml

   * Cluster server - `[appserver root]`/domain/configuration/host.xml

   * Cluster server - `[appserver root]`/dominio/configurazione/dominio_&lt;dbname>.xml

1. 
   * **Per il server singolo,** nel file lc_&lt;dbaname/tunkey>.xml, aggiungere quanto segue dopo la sezione &lt;security-realms>:

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMformsCert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   Individua la sezione `<server>` presente dopo il seguente codice:

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   Aggiungi quanto segue alla sezione &lt;server> presente dopo il codice precedente:

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

   * **Per il cluster di server,** nella [radice appserver]\domain\configuration\host.xml su tutti i nodi, aggiungere quanto segue dopo la sezione &lt;security-realms>:

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMForms Cert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   Nel nodo principale del cluster di server, nella [directory principale del server applicazioni]\domain\configuration\domain_&lt;dbname>.xml, individuare la sezione &lt;server> presente dopo il codice seguente:

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   Aggiungi quanto segue alla sezione &lt;server> presente dopo il codice precedente:

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

1. Modificare il valore per l&#39;attributo `keystoreFile` e l&#39;attributo `keystorePass` nella password del keystore specificata al momento della creazione del keystore.
1. Riavviare il server applicazioni:

   * Per le installazioni chiavi in mano:

      * Nel Pannello di controllo Campaign Windows fare clic su Strumenti di amministrazione e quindi su Servizi.
      * Selezionare JBoss per Adobe Experience Manager Form.
      * Selezionare Azione > Interrompi.
      * Attendere che lo stato del servizio venga visualizzato come arrestato.
      * Selezionare Azione > Avvia.

   * Ad Adobe, installazioni JBoss preconfigurate o configurate manualmente:

      * Dal prompt dei comandi passare a *`[appserver root]`*/bin.
      * Arrestare il server immettendo il comando seguente:

         * (Windows) `shutdown.bat -S`
         * (Linux) `./shutdown.sh -S`

      * Attendi che il processo JBoss sia stato completamente arrestato (quando il processo JBoss restituisce il controllo al terminale in cui è stato avviato).
      * Avviare il server immettendo il comando seguente:

         * (Windows) `run.bat -c <profile>`
         * (Linux) `./run.sh -c <profile>`

1. Per accedere alla console di amministrazione tramite SSL, digitare `https://[host name]:'port'/adminui` in un browser Web:

   La porta SSL predefinita per JBoss è 8443. Da qui in poi, specificare questa porta per l&#39;accesso ai moduli AEM.

## Richiedi credenziali da una CA {#request-a-credential-from-a-ca}

1. Al prompt dei comandi passare a *[JAVA HOME]*/bin e digitare il comando seguente per creare il keystore e la chiave:

   `keytool -genkey -dname "CN=`*Nome host* `, OU=`*Nome gruppo* `, O=`*Nome società* `, L=`*Nome città* `, S=`*Stato* `, C=`*Codice paese*&quot; `-alias "AEMForms Cert"` `-keyalg RSA -keypass`-*password_chiave* `-keystore`*nomechiave* `.keystore`

   >[!NOTE]
   >
   >Sostituisci *`[JAVA_HOME]`* con la directory in cui è installato JDK e sostituisci il testo in corsivo con i valori corrispondenti all&#39;ambiente.

1. Digitare il comando seguente per generare una richiesta di certificato da inviare all&#39;autorità di certificazione:

   `keytool -certreq -alias` &quot;Certificato AEMForms&quot; `-keystore`*nomechiave* `.keystore -file`*RichiestaAEMFormscert.csr*

1. Quando la richiesta di un file di certificato è soddisfatta, completare la procedura successiva.

## Utilizzare una credenziale ottenuta da una CA per abilitare SSL {#use-a-credential-obtained-from-a-ca-to-enable-ssl}

1. Al prompt dei comandi passare a *`[JAVA HOME]`*/bin e digitare il comando seguente per importare il certificato radice della CA con cui è stata firmata la CSR:

   `keytool -import -trustcacerts -file` rootcert.pem -keystore` keystorename.keystore -alias root`

   Se il certificato radice non è nel browser, importalo anche lì.

   >[!NOTE]
   >
   >Sostituisci *`[JAVA_HOME]`con la directory in cui è installato JDK e sostituisci il testo in corsivo con i valori corrispondenti all&#39;ambiente.*

1. Al prompt dei comandi passare a *`[JAVA HOME]`*/bin e digitare il comando seguente per importare le credenziali nel keystore:

   `keytool -import -trustcacerts -file`*NomeCertificatoCAC* `.crt -keystore`*nomearchivioChiave* `.keystore`

   >[!NOTE]
   >
   >* Sostituisci `[JAVA_HOME]` con la directory in cui è installato JDK e sostituisci il testo in corsivo con i valori corrispondenti all&#39;ambiente.
   >* Il certificato firmato CA importato sostituirà un certificato pubblico autofirmato, se esistente.

1. Completare i passaggi 13-18 di Creare una credenziale SSL.
