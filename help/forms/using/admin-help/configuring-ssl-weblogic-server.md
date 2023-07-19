---
title: Configurazione di SSL per il server WebLogic
seo-title: Configuring SSL for WebLogic Server
description: Scopri come creare una credenziale SSL da utilizzare sul server WebLogic e come configurare SSL per il server WebLogic.
seo-description: Learn how to create an SSL credential for use on WebLogic server and how to configure SSL for WebLogic Server.
uuid: 8ee979fd-2615-451b-a607-4f73ecfed4f9
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 968c2574-ec9a-45ca-9c64-66f4caeec285
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 0%

---


# Configurazione di SSL per il server WebLogic {#configuring-ssl-for-weblogic-server}

Per configurare SSL sul server WebLogic, è necessaria una credenziale SSL per l&#39;autenticazione. Per creare una credenziale, è possibile utilizzare Java Keytool per eseguire le operazioni seguenti:

* Crea una coppia di chiavi pubblica/privata, racchiudi la chiave pubblica in un certificato autofirmato X.509 v1 memorizzato come catena di certificati a elemento singolo e quindi archivia la catena di certificati e la chiave privata in un nuovo keystore. Questo keystore è il keystore di identità personalizzato del server applicazioni.
* Estrai il certificato e inseriscilo in un nuovo keystore. Questo keystore è il keystore di trust personalizzato del server applicazioni.

Quindi, configurare WebLogic in modo che utilizzi il keystore Identità personalizzata e il keystore Trust personalizzato creati. Inoltre, disabilitare la funzione di verifica del nome host WebLogic perché il nome distinto utilizzato per creare i file del keystore non includeva il nome del computer che ospita WebLogic.

## Creazione di credenziali SSL da utilizzare sul server WebLogic {#creating-an-ssl-credential-for-use-on-weblogic-server}

Il comando keytool si trova in genere nella directory Java jre/bin e deve includere diverse opzioni e valori di opzione, elencati nella tabella seguente.

<table>
 <thead>
  <tr>
   <th><p>Opzione strumento chiave</p></th>
   <th><p>Descrizione</p></th>
   <th><p>Valore opzione</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>-alias</p></td>
   <td><p>Alias del keystore.</p></td>
   <td>
    <ul>
     <li><p>Key store identità personalizzato: <code>ads-credentials</code></p></li>
     <li><p>KeyStore attendibilità personalizzato: <code>bedrock</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keyalg</p></td>
   <td><p>Algoritmo da utilizzare per generare la coppia di chiavi.</p></td>
   <td><p>RSA</p><p>Puoi utilizzare un algoritmo diverso a seconda della politica della tua azienda.</p></td>
  </tr>
  <tr>
   <td><p>-keystore</p></td>
   <td><p>Posizione e nome del file keystore.</p><p>La posizione può includere il percorso assoluto del file. Oppure, può essere relativa alla directory corrente del prompt dei comandi in cui viene immesso il comando keytool.</p></td>
   <td>
    <ul>
     <li><p>Key store identità personalizzato: <code>[</code><i>appserverdomain<code>]</code></i><code>/adobe/</code><i>[nome server]</i><code>/ads-ssl.jks</code></p></li>
     <li><p>KeyStore attendibilità personalizzato: <code>[</code><i>appserverdomain<code>]</code></i><code>/adobe/</code><i>[nome server]</i><code>/ads-ca.jks</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-file</p></td>
   <td><p>Posizione e nome del file del certificato.</p></td>
   <td><code> ads-ca.cer</code></td>
  </tr>
  <tr>
   <td><p>-validità</p></td>
   <td><p>Il numero di giorni in cui il certificato è considerato valido.</p></td>
   <td><p>3650</p><p>Puoi utilizzare un valore diverso, a seconda della politica aziendale.</p></td>
  </tr>
  <tr>
   <td><p>-storepass</p></td>
   <td><p>La password che protegge il contenuto del keystore. </p></td>
   <td>
    <ul>
     <li><p>KeyStore identità personalizzata: la password del keystore deve corrispondere alla password delle credenziali SSL specificata per il componente Trust Store della console di amministrazione.</p></li>
     <li><p>KeyStore di attendibilità personalizzato: utilizza la stessa password utilizzata per il keystore di identità personalizzato.</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-esclusione</p></td>
   <td><p>Password che protegge la chiave privata della coppia di chiavi.</p></td>
   <td><p>Utilizza la stessa password utilizzata per il <code>-storepass</code> opzione. La password della chiave deve contenere almeno sei caratteri.</p></td>
  </tr>
  <tr>
   <td><p>-dname</p></td>
   <td><p>Il nome distinto che identifica la persona a cui appartiene il keystore.</p></td>
   <td><p><code>"CN=</code><code>[User name]</code><code>,OU=</code><code>[Group Name]</code><code>, O=</code><code>[Company Name]</code><code>, L=</code><code>[City Name]</code><code>, S=</code><code>[State or province]</code><code>, C=</code><code>[Country Code]</code><code>"</code></p>
    <ul>
     <li><p><code><i>[User name]</i></code> è l'identificazione dell'utente a cui appartiene il keystore.</p></li>
     <li><p><code><i>[Group Name]</i></code> è l’identificazione del gruppo aziendale a cui appartiene il proprietario del keystore.</p></li>
     <li><p><code><i>[Company Name]</i></code> è il nome dell’organizzazione.</p></li>
     <li><p><code><i>[City Name]</i></code> è la città in cui si trova l’organizzazione.</p></li>
     <li><p><code><i>[State or province]</i></code> è lo stato o la provincia in cui si trova l’organizzazione.</p></li>
     <li><p><code><i>[Country Code]</i></code> è il codice di due lettere per il paese in cui si trova l’organizzazione.</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

Per ulteriori informazioni sull&#39;utilizzo del comando keytool, vedere il file keytool.html incluso nella documentazione di JDK.

## Creare i keystore di identità e attendibilità personalizzati {#create-the-custom-identity-and-trust-keystores}

1. Dal prompt dei comandi passare a *[appserverdomain]*/adobe/*[nome server]*.
1. Immetti il comando seguente:

   `[JAVA_HOME]/bin/keytool -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass store_password -keypass key_password -dname "CN=Hostname, OU=Group Name, O=Company Name, L=City Name, S=State,C=Country Code`

   >[!NOTE]
   >
   >Sostituisci `[JAVA_HOME]`*con la directory in cui è installato JDK e sostituisci il testo in corsivo con i valori corrispondenti all’ambiente.*

   Ad esempio:

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass P@ssw0rd -keypass P@ssw0rd -dname "CN=wasnode01, OU=LC, O=Adobe, L=Noida, S=UP,C=91
   ```

   Il file keystore di identità personalizzato denominato &quot;ads-credentials.jks&quot; viene creato nel file [appserverdomain]/adobe/[nome server] directory.

1. Estrai il certificato dal keystore ads-credentials immettendo il comando seguente:

   [JAVA_HOME]`/bin/keytool -export -v -alias ads-credentials`

   `-file "ads-ca.cer" -keystore "ads-credentials.jks"`

   `-storepass` `*store*`*_**password**

   >[!NOTE]
   >
   >Sostituisci `[JAVA_HOME]` con la directory in cui è installato JDK e sostituire `store`*_* `password`* con la password per il keystore Custom Identity.*

   Ad esempio:

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -export -v -alias ads-credentials -file "ads-ca.cer" -keystore "ads-credentials.jks" -storepass P@ssw0rd
   ```

   Il file di certificato denominato &quot;ads-ca.cer&quot; viene creato in [appserverdomain]/adobe/[*nome server*] directory.

1. Copiare il file ads-ca.cer in tutti i computer host che richiedono una comunicazione sicura con il server applicazioni.
1. Inserire il certificato in un nuovo file keystore (il keystore di trust personalizzato) immettendo il comando seguente:

   [JAVA_HOME] `/bin/keytool -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass store_password -keypass key_password`

   >[!NOTE]
   >
   >Sostituisci `[JAVA_HOME]` con la directory in cui è installato JDK e sostituire `store`*_* `password` e `key`*_* `password` *con le tue password.*

   Ad esempio:

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass Password1 -keypass Password1
   ```

Il file keystore Trust personalizzato denominato &quot;ads-ca.jks&quot; viene creato nel [appserverdomain]directory /adobe/&#39;server&#39;.

Configurare WebLogic in modo che utilizzi il keystore Identità personalizzata e il keystore Trust personalizzato creati. Disattivare inoltre la funzione di verifica del nome host WebLogic perché il nome distinto utilizzato per creare i file del keystore non include il nome del computer che ospita WebLogic Server.

## Configurare WebLogic per l&#39;utilizzo di SSL {#configure-weblogic-to-use-ssl}

1. Avviare la console di amministrazione del server WebLogic digitando `https://`*[nome host ]*`:7001/console` nella riga URL di un browser web.
1. In Ambiente, in Configurazioni dominio, seleziona **Server > &#39;server&#39; > Configurazione > Generale**.
1. In Generale, in Configurazione, assicurati che **Porta di ascolto abilitata** e **Porta di ascolto SSL abilitata** sono selezionati. Se non è abilitata, effettuare le seguenti operazioni:

   1. Sotto Cambia centro, fare clic su **Blocca e modifica** per modificare selezioni e valori.
   1. Controlla la **Porta di ascolto abilitata** e **Porta di ascolto SSL abilitata** caselle di controllo.

1. Se il server è un server gestito, impostare la porta di ascolto su un valore di porta inutilizzato (ad esempio 8001) e la porta di ascolto SSL su un valore di porta inutilizzato (ad esempio 8002). In un server autonomo, la porta SSL predefinita è 7002.
1. Clic **Configurazione della versione**.
1. In Ambiente, in Configurazioni dominio, fai clic su **Server > [*Server gestito*] > Configurazione > Generale**.
1. In Generale, in Configurazione, seleziona **Negozi chiavi**.
1. Sotto Cambia centro, fare clic su **Blocca e modifica** per modificare selezioni e valori.
1. Clic **Cambia** per ottenere l&#39;elenco keystore come elenco a discesa e selezionare **Identità Personalizzata E Attendibilità Personalizzata**.
1. In Identità (Identity), specificate i seguenti valori:

   **Key store identità personalizzato**: *[appserverdomain]*/adobe/*[nome server]*/ads-credentials.jks, dove *[appserverdomain] *è il percorso effettivo e *[nome server]* è il nome del server applicazioni.

   **Tipo di registro chiavi identità personalizzato**: JKS

   **Passphrase KeyStore identità personalizzata**: *mypassword* (password del keystore di identità personalizzata)

1. In Considera attendibile specificare i valori seguenti:

   **Nome file KeyStore attendibilità personalizzato**: `*[appserverdomain]*/adobe/*'server'*/ads-ca.jks`, dove `*[appserverdomain]*` è il percorso effettivo

   **Tipo di keystore di attendibilità personalizzato**: JKS

   **Passphrase KeyStore attendibile personalizzata**: *mypassword* (password chiave di trust personalizzata)

1. In Generale, in Configurazione, seleziona **SSL**.
1. Per impostazione predefinita, l&#39;opzione Registro chiavi è selezionata per le posizioni di identità e attendibilità. In caso contrario, modificarlo in keystore.
1. In Identità (Identity), specificate i seguenti valori:

   **Alias chiave privata**: ads-credentials

   **Passphrase**: *mypassword*

1. Clic **Configurazione della versione**.

## Disattiva la funzione di verifica del nome host {#disable-the-hostname-verification-feature}

1. Nella scheda Configurazione, fai clic su SSL.
1. In Avanzate, seleziona Nessuno dall’elenco Verifica nome host.

   Se la verifica del nome host non è disattivata, il nome comune (CN) deve contenere il nome host del server.

1. In Cambia centro fare clic su Blocca e modifica per modificare selezioni e valori.
1. Riavviare il server applicazioni.

