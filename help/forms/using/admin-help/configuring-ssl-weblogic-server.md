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
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 1%

---


# Configurazione di SSL per il server WebLogic {#configuring-ssl-for-weblogic-server}

Per configurare SSL sul server WebLogic, è necessaria una credenziale SSL per l’autenticazione. Per creare una credenziale è possibile utilizzare lo strumento chiave Java per eseguire le seguenti attività:

* Crea una coppia di chiavi pubblica/privata, racchiude la chiave pubblica in un certificato autofirmato X.509 v1 memorizzato come catena di certificati a elemento singolo, quindi archivia la catena di certificati e la chiave privata in un nuovo keystore. Questo keystore è l’archivio chiavi di identità personalizzata del server dell’applicazione.
* Estrai il certificato e inseriscilo in un nuovo keystore. Questo keystore è l&#39;archivio chiavi personalizzato del server applicazioni.

Quindi, configura WebLogic in modo che utilizzi l’archivio chiavi Custom Identity e l’archivio chiavi Custom Trust creati. Inoltre, disattiva la funzionalità Verifica nome host WebLogic perché il nome distinto utilizzato per creare i file del keystore non includeva il nome del computer che ospita WebLogic.

## Creazione di una credenziale SSL da utilizzare sul server WebLogic {#creating-an-ssl-credential-for-use-on-weblogic-server}

Il comando keytool si trova in genere nella directory Java jre/bin e deve includere diverse opzioni e valori di opzione, elencati nella tabella seguente.

<table>
 <thead>
  <tr>
   <th><p>Opzione Keytool</p></th>
   <th><p>Descrizione</p></th>
   <th><p>Valore opzione</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>-alias</p></td>
   <td><p>L'alias del keystore.</p></td>
   <td>
    <ul>
     <li><p>Archivio chiavi identità personalizzato: <code>ads-credentials</code></p></li>
     <li><p>Archivio chiavi di attendibilità personalizzato: <code>bedrock</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keyalg</p></td>
   <td><p>L’algoritmo da utilizzare per generare la coppia di chiavi.</p></td>
   <td><p>RSA</p><p>Puoi utilizzare un algoritmo diverso, a seconda dei criteri aziendali.</p></td>
  </tr>
  <tr>
   <td><p>-keystore</p></td>
   <td><p>Posizione e nome del file dell'archivio chiavi.</p><p>La posizione può includere il percorso assoluto del file. Oppure può essere relativo alla directory corrente del prompt dei comandi in cui è inserito il comando keytool.</p></td>
   <td>
    <ul>
     <li><p>Archivio chiavi identità personalizzato: <code>[</code><i>appserverdomain<code>]</code></i><code>/adobe/</code><i>[nome server]</i><code>/ads-ssl.jks</code></p></li>
     <li><p>Archivio chiavi di attendibilità personalizzato: <code>[</code><i>appserverdomain<code>]</code></i><code>/adobe/</code><i>[nome server]</i><code>/ads-ca.jks</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-file</p></td>
   <td><p>Posizione e nome del file del certificato.</p></td>
   <td><code> ads-ca.cer</code></td>
  </tr>
  <tr>
   <td><p>-Validità</p></td>
   <td><p>Il numero di giorni in cui il certificato è considerato valido.</p></td>
   <td><p>3650</p><p>Puoi utilizzare un valore diverso, a seconda della politica aziendale.</p></td>
  </tr>
  <tr>
   <td><p>-storepass</p></td>
   <td><p>La password che protegge il contenuto del keystore. </p></td>
   <td>
    <ul>
     <li><p>Archivio chiavi identità personalizzato: La password del keystore deve corrispondere alla password delle credenziali SSL specificata per il componente Trust Store di Administration Console.</p></li>
     <li><p>Archivio chiavi di attendibilità personalizzato: Utilizza la stessa password utilizzata per l’archivio chiavi di identità personalizzata.</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keypass</p></td>
   <td><p>Password che protegge la chiave privata della coppia di chiavi.</p></td>
   <td><p>Utilizza la stessa password utilizzata per <code>-storepass</code> opzione . La password della chiave deve contenere almeno sei caratteri.</p></td>
  </tr>
  <tr>
   <td><p>-dname</p></td>
   <td><p>Nome distinto che identifica la persona proprietaria del keystore.</p></td>
   <td><p><code>"CN=</code><code>[User name]</code><code>,OU=</code><code>[Group Name]</code><code>, O=</code><code>[Company Name]</code><code>, L=</code><code>[City Name]</code><code>, S=</code><code>[State or province]</code><code>, C=</code><code>[Country Code]</code><code>"</code></p>
    <ul>
     <li><p><code><i>[User name]</i></code> è l'identificazione dell'utente proprietario dell'archivio chiavi.</p></li>
     <li><p><code><i>[Group Name]</i></code> è l'identificazione del gruppo aziendale a cui appartiene il proprietario del keystore.</p></li>
     <li><p><code><i>[Company Name]</i></code> è il nome dell’organizzazione.</p></li>
     <li><p><code><i>[City Name]</i></code> è la città in cui si trova l’organizzazione.</p></li>
     <li><p><code><i>[State or province]</i></code> è lo stato o la provincia in cui si trova l'organizzazione.</p></li>
     <li><p><code><i>[Country Code]</i></code> è il codice a due lettere per il paese in cui si trova l'organizzazione.</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

Per ulteriori informazioni sull&#39;utilizzo del comando keytool, vedere il file keytool.html che fa parte della documentazione JDK.

## Creare gli archivi chiavi di identità personalizzata e di attendibilità {#create-the-custom-identity-and-trust-keystores}

1. Da un prompt dei comandi, passa a *[appserverdomain]*/adobe/*[nome server]*.
1. Immetti il seguente comando:

   `[JAVA_HOME]/bin/keytool -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass store_password -keypass key_password -dname "CN=Hostname, OU=Group Name, O=Company Name, L=City Name, S=State,C=Country Code`

   >[!NOTE]
   >
   >Sostituisci `[JAVA_HOME]`*con la directory in cui è installato JDK e sostituisci il testo in corsivo con i valori corrispondenti al tuo ambiente.*

   Esempio:

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass P@ssw0rd -keypass P@ssw0rd -dname "CN=wasnode01, OU=LC, O=Adobe, L=Noida, S=UP,C=91
   ```

   Il file del keystore di identità personalizzata denominato &quot;ads-credentials.jks&quot; viene creato in [appserverdomain]/adobe/[nome server] directory.

1. Estrai il certificato dall&#39;archivio chiavi ads-credentials immettendo il seguente comando:

   [JAVA_HOME]`/bin/keytool -export -v -alias ads-credentials`

   `-file "ads-ca.cer" -keystore "ads-credentials.jks"`

   `-storepass` `*store*`*_**password**

   >[!NOTE]
   >
   >Sostituisci `[JAVA_HOME]` con la directory in cui è installato JDK e sostituire `store`*_* `password`* con la password per l’archivio chiavi di identità personalizzata.*

   Esempio:

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -export -v -alias ads-credentials -file "ads-ca.cer" -keystore "ads-credentials.jks" -storepass P@ssw0rd
   ```

   Il file di certificato denominato &quot;ads-ca.cer&quot; viene creato nel [appserverdomain]/adobe/[*nome server*] directory.

1. Copia il file ads-ca.cer in qualsiasi computer host che necessita di una comunicazione sicura con il server applicazioni.
1. Inserire il certificato in un nuovo file dell&#39;archivio chiavi (l&#39;archivio chiavi personalizzato) immettendo il seguente comando:

   [JAVA_HOME] `/bin/keytool -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass store_password -keypass key_password`

   >[!NOTE]
   >
   >Sostituisci `[JAVA_HOME]` con la directory in cui è installato JDK e sostituire `store`*_* `password` e `key`*_* `password` *con le tue password.*

   Esempio:

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass Password1 -keypass Password1
   ```

Il file del keystore personalizzato denominato &quot;ads-ca.jks&quot; viene creato in [appserverdomain]/adobe/&#39;server&#39;.

Configura WebLogic in modo che utilizzi l’archivio chiavi Custom Identity e l’archivio chiavi Custom Trust creati. Inoltre, disattiva la funzionalità Verifica nome host WebLogic perché il nome distinto utilizzato per creare i file del keystore non includeva il nome del computer che ospita WebLogic Server.

## Configurare WebLogic per l’utilizzo di SSL {#configure-weblogic-to-use-ssl}

1. Avvia la console di amministrazione del server WebLogic digitando `https://`*[nome host ]*`:7001/console` nella riga URL di un browser web.
1. In Ambiente, in Configurazioni dominio, seleziona **Server > &#39;server&#39; > Configurazione > Generale**.
1. In Generale, in Configurazione, assicurati che **Porta di ascolto abilitata** e **Porta di ascolto SSL abilitata** sono selezionati. Se non è abilitata, procedi come segue:

   1. In Centro modifiche fare clic su **Blocco e modifica** per modificare selezioni e valori.
   1. Controlla la **Porta di ascolto abilitata** e **Porta di ascolto SSL abilitata** caselle di controllo.

1. Se questo server è un server gestito, cambia Porta di ascolto in un valore di porta non utilizzato (ad esempio 8001) e Porta di ascolto SSL in un valore di porta non utilizzato (ad esempio 8002). Su un server autonomo, la porta SSL predefinita è 7002.
1. Fai clic su **Configurazione della versione**.
1. In Ambiente, in Configurazioni dominio, fai clic su **Server > [*Server gestito*] > Configurazione > Generale**.
1. In Generale, in Configurazione, selezionare **Principali**.
1. In Centro modifiche fare clic su **Blocco e modifica** per modificare selezioni e valori.
1. Fai clic su **Modifica** per ottenere l’elenco a discesa keystore e selezionare **Identità personalizzata e attendibilità personalizzata**.
1. In Identità, specifica i seguenti valori:

   **Keystore di identità personalizzato**: *[appserverdomain]*/adobe/*[nome server]*/ads-credentials.jks , dove *[appserverdomain] *è il percorso effettivo e *[nome server]* è il nome dell&#39;application server.

   **Tipo di archivio chiavi personalizzato**: JKS

   **Password dell’archivio chiavi personalizzata**: *password* (password del keystore di identità personalizzata)

1. In Trust, specificare i seguenti valori:

   **Nome file dell&#39;archivio chiavi di attendibilità personalizzato**: `*[appserverdomain]*/adobe/*'server'*/ads-ca.jks`, dove `*[appserverdomain]*` è il percorso effettivo

   **Tipo di chiave trust personalizzato**: JKS

   **Frase di passaggio dell&#39;archivio chiavi personalizzato**: *password* (password della chiave di attendibilità personalizzata)

1. In Generale, in Configurazione, selezionare **SSL**.
1. Per impostazione predefinita, l’archivio chiavi è selezionato per le posizioni Identità e Affidabilità. In caso contrario, cambialo in keystore.
1. In Identità, specifica i seguenti valori:

   **Alias chiave privata**: ads-credentials

   **Passphrase**: *password*

1. Fai clic su **Configurazione della versione**.

## Disattiva la funzione di verifica del nome host {#disable-the-hostname-verification-feature}

1. Nella scheda Configurazione, fai clic su SSL.
1. In Avanzate, selezionare Nessuno dall’elenco Verifica nome host.

   Se la verifica del nome host non è disabilitata, il nome comune (CN) deve contenere il nome host del server.

1. In Cambia centro fare clic su Blocca e modifica per modificare selezioni e valori.
1. Riavvia il server applicazioni.

