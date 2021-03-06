---
title: Configurazione di SSL per il server applicazioni JBoss
seo-title: Configurazione di SSL per il server applicazioni JBoss
description: Scoprite come configurare SSL per il server applicazioni JBoss.
seo-description: Scoprite come configurare SSL per il server applicazioni JBoss.
uuid: 7c13cf00-ea89-4894-a4fc-aaeec7ae9f66
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c187daa4-41b7-47dc-9669-d7120850cafd
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---


# Configurazione di SSL per il server applicazioni JBoss {#configuring-ssl-for-jboss-application-server}

Per configurare SSL sul server applicazioni JBoss, è necessaria una credenziale SSL per l’autenticazione. È possibile utilizzare lo strumento chiave Java per creare una credenziale o richiedere e importare una credenziale da un&#39;autorità di certificazione (CA). È quindi necessario abilitare SSL su JBoss.

È possibile eseguire keytool utilizzando un singolo comando che include tutte le informazioni necessarie per creare l&#39;archivio di chiavi.

In questa procedura:

* `[appserver root]` è la directory principale del server applicazioni che esegue AEM moduli.
* `[type]` è un nome di cartella che varia a seconda del tipo di installazione eseguito.

## Creare una credenziale SSL {#create-an-ssl-credential}

1. Al prompt dei comandi, andate a *[JAVA HOME]*/bin e digitate il comando seguente per creare la credenziale e l&#39;archivio di chiavi:

   `keytool -genkey -dname "CN=`*Host* `, OU=`*NameGroup* `, O=`*NameCompany* `,L=`*NameCity* `, S=`** `, C=`NameStateCountry Code&quot;  `-alias "AEMForms Cert"` `-keyalg RSA -keypass`*key_* `-keystore`*passwordkeystorename* `.keystore`

   >[!NOTE]
   >
   >Sostituire `[JAVA_HOME]` con la directory in cui è installato JDK e sostituire il testo in corsivo con valori corrispondenti all&#39;ambiente in uso. Nome host è il nome di dominio completo del server applicazione.

1. Inserire il simbolo `keystore_password` quando viene richiesta una password. La password per l&#39;archivio di chiavi e la chiave devono essere identiche.

   >[!NOTE]
   >
   >La `keystore_password` *inserita in questo passaggio può essere la stessa password (key_password) immessa nel passaggio 1, oppure può essere diversa.*

1. Copiare il *keystorename*.keystore nella directory `[appserver root]/server/[type]/conf` digitando uno dei seguenti comandi:

   * (Windows Single Server) `copy` `keystorename.keystore[appserver root]\standalone\configuration`
   * (Cluster Windows Server) copia `keystorename.keystore[appserver root]\domain\configuration`
   * (Linux Single Server) `cp keystorename.keystore [appserver root]/standalone/configuration`
   * (cluster di server Linux) `cp <em>keystorename</em>.keystore<em>[appserver root]</em>/domain/configuration`


1. Esportate il file del certificato digitando il comando seguente:

   * (Server singolo) `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/standalone/configuration/keystorename.keystore`
   * (Cluster server) `keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer -keystore [appserver root]/domain/configuration/keystorename.keystore`

1. Immettere la *keystore_password* quando viene richiesta una password.
1. Copiate il file AEMForms_cert.cer nella directory *[appserver root] \conf* digitando il seguente comando:

   * (Windows Single Server) `copy AEMForms_cert.cer [appserver root]\standalone\configuration`
   * (Cluster Windows Server) `copy AEMForms_cert.cer [appserver root]\domain\configuration`
   * (Linux Single Server) `cp AEMForms _cert.cer [appserver root]\standalone\configuration`
   * (cluster di server Linux) `cp AEMForms _cert.cer [appserver root]\domain\configuration`

1. Visualizzate il contenuto del certificato digitando il comando seguente:

   * `keytool -printcert -v -file [appserver root]\standalone\configuration\AEMForms_cert.cer`
   * `keytool -printcert -v -file [appserver root]\domain\configuration\AEMForms_cert.cer`

1. Per fornire l&#39;accesso in scrittura al file cacerts in `[JAVA_HOME]\jre\lib\security`, se necessario, eseguire l&#39;operazione seguente:

   * (Windows) Fare clic con il pulsante destro del mouse sul file cacerts e selezionare Proprietà, quindi deselezionare l&#39;attributo di sola lettura.
   * (Linux) Tipo `chmod 777 cacerts`

1. Importa il certificato digitando il comando seguente:

   `keytool -import -alias “AEMForms Cert” -file`*AEMForms_* `.cer -keystore`*certJAVA_HOME* `\jre\lib\security\cacerts`

1. Digitare `changeit` come password. Questa password è la password predefinita per un&#39;installazione Java e può essere stata modificata dall&#39;amministratore di sistema.
1. Quando viene richiesto `Trust this certificate? [no]`:, digitare `yes`. Viene visualizzata la conferma &quot;Certificato aggiunto all&#39;archivio chiavi&quot;.
1. Se si esegue la connessione SSL da Workbench, installare il certificato nel computer Workbench.
1. In un editor di testo, aprite i file seguenti per la modifica:

   * Server singolo - `[appserver root]`/standalone/configuration/lc_&lt;nome file/chiave inglese>.xml

   * Cluster server - `[appserver root]`/domain/configuration/host.xml

   * Cluster server - `[appserver root]`/domain/configuration/domain_&lt;nome file>.xml

1. 
   * **Per un singolo server,** nel file lc_&lt;dbaname>.xml aggiungete quanto segue dopo la  &lt;security-realms> sezione:

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMformsCert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   Individuare la sezione `<server>` presente dopo il seguente codice:

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   Aggiungete quanto segue alla sezione &lt;server> presente dopo il codice precedente:

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

   * **Per il cluster di server,** nella directory principale  [appserver]\domain\configuration\host.xml su tutti i nodi, aggiungere quanto segue dopo  &lt;security-realms> la sezione:

   ```xml
   <security-realm name="SSLRealm">
   <server-identities>
   <ssl>
   <keystore path="C:/Adobe/Adobe_Experience_Manager_Forms/jboss/standalone/configuration/aemformses.keystore" keystore-password="changeit" alias="AEMForms Cert" key-password="changeit"/>
   </ssl>
   </server-identities>
   </security-realm>
   ```

   Nel nodo principale del cluster di server, nella directory [host ]\domain\configuration\domain_&lt;dbname>.xml, individuare la sezione &lt;server> presente dopo il seguente codice:

   `<http-listener name="default" socket-binding="http" redirect-socket="https" max-post-size="104857600"/>`

   Aggiungete quanto segue alla sezione &lt;server> presente dopo il codice precedente:

   ```xml
   <https-listener name="default-secure" socket-binding="https" security-realm="SSLRealm"/>
   ```

1. Modificate il valore per l&#39;attributo `keystoreFile` e l&#39;attributo `keystorePass` nella password dell&#39;archivio di chiavi specificata al momento della creazione dell&#39;archivio di chiavi.
1. Riavviate il server applicazione:

   * Per gli impianti chiavi in mano:

      * Dal Pannello di controllo Campaign Windows, fare clic su Strumenti di amministrazione, quindi fare clic su Servizi.
      * Selezionare JBoss per i moduli Adobe Experience Manager.
      * Selezionare Azione > Interrompi.
      * Attendere che lo stato del servizio venga visualizzato come interrotto.
      * Selezionare Azione > Avvia.
   * Per  Adobe installazioni JBoss preconfigurate o configurate manualmente:

      * Dal prompt dei comandi, andate a *`[appserver root]`*/bin.
      * Arrestate il server immettendo il seguente comando:

         * (Windows) `shutdown.bat -S`
         * (Linux) `./shutdown.sh -S`
      * Attendere che il processo JBoss sia completamente spento (quando il processo JBoss restituisce il controllo al terminale in cui è stato avviato).
      * Avviate il server immettendo il seguente comando:

         * (Windows) `run.bat -c <profile>`
         * (Linux) `./run.sh -c <profile>`



1. Per accedere alla console di amministrazione tramite SSL, digita `https://[host name]:'port'/adminui` in un browser Web:

   La porta SSL predefinita per JBoss è 8443. Da qui in avanti, specificare questa porta per accedere AEM moduli.

## Richiesta di una credenziale da una CA {#request-a-credential-from-a-ca}

1. Al prompt dei comandi, andate a *[JAVA HOME]*/bin e digitate il comando seguente per creare l&#39;archivio di chiavi e la chiave:

   `keytool -genkey -dname "CN=`*Host* `, OU=`*NameGroup* `, O=`*NameCompany* `, L=`*NameCity* `, S=`** `, C=`*NameStateCountry Code*&quot;  `-alias "AEMForms Cert"` `-keyalg RSA -keypass`-*key_* `-keystore`*passwordkeystorename* `.keystore`

   >[!NOTE]
   >
   >Sostituire *`[JAVA_HOME]`* con la directory in cui è installato JDK e sostituire il testo in corsivo con valori corrispondenti all&#39;ambiente in uso.

1. Digitate il comando seguente per generare una richiesta di certificato da inviare all’autorità di certificazione:

   `keytool -certreq -alias` &quot;AEMForms Cert&quot;  `-keystore`** `.keystore -file`*keystorenameAEMFormscertRequest.csr*

1. Una volta soddisfatta la richiesta di un file di certificato, completate la procedura successiva.

## Utilizzare una credenziale ottenuta da una CA per abilitare SSL {#use-a-credential-obtained-from-a-ca-to-enable-ssl}

1. Al prompt dei comandi, passare a *`[JAVA HOME]`*/bin e digitare il comando seguente per importare il certificato radice della CA con cui è stato firmato il CSR:

   `keytool -import -trustcacerts -file` rootcert.pem -keystore` keystorename.keystore -alias root`

   Se il certificato principale non è presente nel browser, importatelo.

   >[!NOTE]
   >
   >Sostituire *`[JAVA_HOME]`con la directory in cui è installato il JDK e sostituire il testo in corsivo con valori corrispondenti all&#39;ambiente.*

1. Al prompt dei comandi, andate a *`[JAVA HOME]`*/bin e digitate il comando seguente per importare la credenziale nell&#39;archivio chiavi:

   `keytool -import -trustcacerts -file`** `.crt -keystore`*CACertificateNamekeystorename* `.keystore`

   >[!NOTE]
   >
   >* Sostituire `[JAVA_HOME]` con la directory in cui è installato JDK e sostituire il testo in corsivo con valori corrispondenti all&#39;ambiente in uso.
   >* Il certificato CA firmato importato sostituirà un certificato pubblico autofirmato, se esistente.


1. Completate i passaggi da 13 a 18 di Creazione di una credenziale SSL.
