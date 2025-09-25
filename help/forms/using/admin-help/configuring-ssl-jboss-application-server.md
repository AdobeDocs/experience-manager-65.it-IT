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
workflow-type: ht
source-wordcount: '904'
ht-degree: 100%

---

# Configurazione di SSL per il server applicazioni JBoss {#configuring-ssl-for-jboss-application-server}

Per configurare SSL sul server applicazioni JBoss, è necessaria una credenziale SSL per l’autenticazione. Puoi utilizzare lo strumento Java Keytool per creare una credenziale o per richiedere e importare una credenziale da un’autorità di certificazione (CA). Devi quindi abilitare SSL su JBoss.

Puoi eseguire lo strumento Keytool utilizzando un singolo comando che include tutte le informazioni necessarie per creare l’archivio chiavi.

In questa procedura:

* `[appserver root]` è la directory home del server applicazioni che esegue AEM Forms.
* `[type]` è il nome di una cartella che varia a seconda del tipo di installazione eseguita.

## Creare una credenziale SSL {#create-an-ssl-credential}

1. Al prompt dei comandi passa a *[JAVA HOME]*/bin e digita il comando seguente per creare le credenziali e il registro chiavi:

   `keytool -genkey -dname "CN=`*Nome host* `, OU=`*Nome gruppo* `, O=`*Nome società* `,L=`*Nome città* `, S=`*Stato* `, C=`Codice paese” `-alias "AEMForms Cert"` `-keyalg RSA -keypass`*key_password* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >Sostituisci `[JAVA_HOME]` con la directory in cui è installato JDK e sostituisci il testo in corsivo con i valori corrispondenti all’ambiente. Nome host è il nome di dominio completo del server applicazioni.

1. Immetti `keystore_password` quando viene richiesta una password. La password per il registro chiavi e la chiave devono essere identiche.

   >[!NOTE]
   >
   >La `keystore_password` *immessa in questo passaggio può essere la stessa password (key_password) immessa nel passaggio 1 oppure può essere diversa.*

1. Copia *keystorename*.keystore nella directory `[appserver root]/server/[type]/conf` digitando uno dei comandi seguenti:

   * (Server Windows singolo) `copy` `keystorename.keystore[appserver root]\standalone\configuration`
   * (Cluster di server Windows) copia `keystorename.keystore[appserver root]\domain\configuration`
   * (Server Linux singolo) `cp keystorename.keystore [appserver root]/standalone/configuration`
   * (Cluster di server Linux) `cp <em>keystorename</em>.keystore<em>[appserver root]</em>/domain/configuration`


1. Esporta il file del certificato digitando il comando seguente:

   * (Server singolo) `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/standalone/configuration/keystorename.keystore`
   * (Cluster di server) `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/domain/configuration/keystorename.keystore`

1. Immetti *keystore_password* quando viene richiesta una password.
1. Copia il file AEMForms_cert.cer nella directory *[appserver root] \conf* digitando il comando seguente:

   * (Server Windows singolo) `copy AEMForms_cert.cer [appserver root]\standalone\configuration`
   * (Cluster di server Windows) `copy AEMForms_cert.cer [appserver root]\domain\configuration`
   * (Server Linux singolo) `cp AEMForms _cert.cer [appserver root]\standalone\configuration`
   * (Cluster di server Linux) `cp AEMForms _cert.cer [appserver root]\domain\configuration`

1. Visualizza il contenuto del certificato digitando il comando seguente:

   * `keytool -printcert -v -file [appserver root]\standalone\configuration\AEMForms_cert.cer`
   * `keytool -printcert -v -file [appserver root]\domain\configuration\AEMForms_cert.cer`

1. Per fornire l’accesso di scrittura al file cacerts in `[JAVA_HOME]\jre\lib\security`, se necessario, esegui l’attività seguente:

   * (Windows) Fai clic con il pulsante destro del mouse sul file cacerts e seleziona Proprietà, quindi deseleziona l’attributo Sola lettura.
   * (Linux) Digita `chmod 777 cacerts`

1. Importa il certificato digitando il comando seguente:

   `keytool -import -alias "AEMForms Cert" -file`*AEMForms_cert* `.cer -keystore`*JAVA_HOME* `\jre\lib\security\cacerts`

1. Digita `changeit` come password. Questa password è la password predefinita per un’installazione Java e potrebbe essere stata modificata dall’amministratore di sistema.
1. Quando viene richiesto `Trust this certificate? [no]`, digita `yes`. Viene visualizzata la conferma “Certificato aggiunto al registro chiavi”.
1. Se ti connetti tramite SSL da Workbench, installa il certificato sul computer Workbench.
1. In un editor di testo, apri i seguenti file per la modifica:

   * Server singolo - `[appserver root]`/standalone/configuration/lc_&lt;dbname/turnkey>.xml

   * Cluster di server - `[appserver root]`/domain/configuration/host.xml

   * Cluster di server - `[appserver root]`/domain/configuration/domain_&lt;dbname>.xml

1. * **Per il server singolo,** nel file lc_&lt;dbaname/tunkey>.xml, aggiungi quanto segue dopo la sezione &lt;security-realms>:

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

   Aggiungi quanto segue alla sezione &lt;server> che si trova dopo il codice precedente:

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

   * **Per il cluster di server,** nella [directory principale appserver]\domain\configuration\host.xml su tutti i nodi, aggiungi quanto segue dopo la sezione &lt;security-realms>:

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMForms Cert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   Nel nodo principale del cluster di server, nella [directory principale appserver]\domain\configuration\domain_&lt;dbname>.xml, individua la sezione &lt;server> dopo il codice seguente:

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   Aggiungi quanto segue alla sezione &lt;server> che si trova dopo il codice precedente:

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

1. Modifica il valore per l’attributo `keystoreFile` e l’attributo `keystorePass` nella password del registro chiavi specificata al momento della creazione del registro chiavi.
1. Riavvia il server applicazioni:

   * Per le installazioni preconfigurate:

      * Nel Pannello di controllo di Windows fai clic su Strumenti di amministrazione e quindi su Servizi.
      * Seleziona JBoss per Adobe Experience Manager Forms.
      * Seleziona Azione > Interrompi.
      * Attendere che lo stato del servizio venga visualizzato come interrotto.
      * Seleziona Azione > Avvia.

   * Per le installazioni JBoss preconfigurate da Adobe o configurate manualmente:

      * Dal prompt dei comandi passa a *`[appserver root]`*/bin.
      * Arresta il server immettendo il comando seguente:

         * (Windows) `shutdown.bat -S`
         * (Linux) `./shutdown.sh -S`

      * Attendi che il processo JBoss venga arrestato completamente (quando il processo JBoss restituisce il controllo al terminale in cui è stato avviato).
      * Avvia il server immettendo il comando seguente:

         * (Windows) `run.bat -c <profile>`
         * (Linux) `./run.sh -c <profile>`

1. Per accedere alla console di amministrazione tramite SSL, digita `https://[host name]:'port'/adminui` in un browser web:

   La porta SSL predefinita per JBoss è 8443. Da qui in poi, specifica questa porta per l’accesso ad AEM Forms.

## Richiedere credenziali da un’autorità di certificazione (CA) {#request-a-credential-from-a-ca}

1. Da un prompt dei comandi passa a *[JAVA HOME]*/bin e digita il comando seguente per creare l’archivio chiavi e la chiave:

   `keytool -genkey -dname "CN=`*Nome host* `, OU=`*Nome gruppo* `, O=`*Nome società* `, L=`*Nome città* `, S=`*Stato* `, C=`*Codice paese*“” `-alias "AEMForms Cert"` `-keyalg RSA -keypass`-*password_chiave* `-keystore`*nome_archivio_chiavi* `.keystore`

   >[!NOTE]
   >
   >Sostituisci *`[JAVA_HOME]`* con la directory in cui è installato JDK e sostituisci il testo in corsivo con i valori corrispondenti all’ambiente.

1. Digita il comando seguente per generare una richiesta di certificato da inviare all’autorità di certificazione:

   `keytool -certreq -alias` “Certificato AEMForms” `-keystore`*nome_archivio_chiavi* `.keystore -file`*AEMFormscertRequest.csr*

1. Quando la richiesta di un file di certificato è soddisfatta, completa la procedura successiva.

## Utilizzare una credenziale ottenuta da una CA per abilitare SSL {#use-a-credential-obtained-from-a-ca-to-enable-ssl}

1. In un prompt dei comandi passa a *`[JAVA HOME]`*/bin e digita il comando seguente per importare il certificato radice della CA con cui è stata firmata la CSR:

   `keytool -import -trustcacerts -file` rootcert.pem -keystore` keystorename.keystore -alias root`

   Se il certificato radice non è presente nel browser, importalo anche lì.

   >[!NOTE]
   >
   >Sostituisci *`[JAVA_HOME]`con la directory in cui è installato JDK e sostituisci il testo in corsivo con i valori corrispondenti all’ambiente.*

1. In un prompt dei comandi passa a *`[JAVA HOME]`*/bin e digita il comando seguente per importare le credenziali nell’archivio chiavi:

   `keytool -import -trustcacerts -file`*NomeCertificatoCA* `.crt -keystore`*nomearchiviochiavi* `.keystore`

   >[!NOTE]
   >
   >* Sostituisci `[JAVA_HOME]` con la directory in cui è installato JDK e sostituisci il testo in corsivo con i valori corrispondenti all’ambiente.
   >* Il certificato firmato dalla CA importato sostituirà un certificato pubblico autofirmato, se esistente.

1. Completa i passaggi 13-18 di Creare una credenziale SSL.
