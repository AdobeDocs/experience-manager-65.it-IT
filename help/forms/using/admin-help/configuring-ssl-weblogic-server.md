---
title: Configurazione di SSL per il server WebLogic
seo-title: Configurazione di SSL per il server WebLogic
description: Scoprite come creare una credenziale SSL da utilizzare sul server WebLogic e come configurare SSL per il server WebLogic.
seo-description: Scoprite come creare una credenziale SSL da utilizzare sul server WebLogic e come configurare SSL per il server WebLogic.
uuid: 8ee979fd-2615-451b-a607-4f73ecfed4f9
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 968c2574-ec9a-45ca-9c64-66f4caeec285
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 1%

---


# Configurazione di SSL per il server WebLogic {#configuring-ssl-for-weblogic-server}

Per configurare SSL sul server WebLogic, è necessario disporre di una credenziale SSL per l&#39;autenticazione. Per creare una credenziale è possibile utilizzare Java keytool per eseguire le seguenti operazioni:

* Create una coppia chiave pubblica/privata, racchiudete la chiave pubblica in un certificato autofirmato X.509 v1 memorizzato come catena di certificati a elemento singolo, quindi archiviate la catena di certificati e la chiave privata in un nuovo archivio chiavi. Questo archivio di chiavi è l&#39;archivio di chiavi Identità personalizzata del server dell&#39;applicazione.
* Estrarre il certificato e inserirlo in un nuovo archivio di chiavi. Questo keystore è l&#39;archivio chiavi Trust personalizzato del server dell&#39;applicazione.

Quindi, configurare WebLogic in modo che utilizzi l&#39;archivio chiavi identità personalizzata e l&#39;archivio chiavi trust personalizzato creato. Inoltre, disabilitare la funzione di verifica del nome host WebLogic perché il nome distinto utilizzato per creare i file dell&#39;archivio di chiavi non includeva il nome del computer che ospita WebLogic.

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
   <td><p>L'alias dell'archivio di chiavi.</p></td>
   <td>
    <ul>
     <li><p>Keystore identità personalizzata: <code>ads-credentials</code></p></li>
     <li><p>Keystore Trust personalizzato: <code>bedrock</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keyalg</p></td>
   <td><p>Algoritmo da utilizzare per generare la coppia di chiavi.</p></td>
   <td><p>RSA</p><p>Potete utilizzare un algoritmo diverso, a seconda dei criteri aziendali.</p></td>
  </tr>
  <tr>
   <td><p>-keystore</p></td>
   <td><p>Posizione e nome del file keystore.</p><p>La posizione può includere il percorso assoluto del file. Oppure può essere relativo alla directory corrente del prompt dei comandi in cui è immesso il comando keytool.</p></td>
   <td>
    <ul>
     <li><p>Keystore identità personalizzata: <code>[</code><i>appserverdomain<code>]</code></i><code>/adobe/</code><i>[nome server]</i><code>/ads-ssl.jks</code></p></li>
     <li><p>Keystore Trust personalizzato: <code>[</code><i>appserverdomain<code>]</code></i><code>/adobe/</code><i>[nome server]</i><code>/ads-ca.jks</code></p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-file</p></td>
   <td><p>Posizione e nome del file del certificato.</p></td>
   <td><code> ads-ca.cer</code></td>
  </tr>
  <tr>
   <td><p>-validation</p></td>
   <td><p>Il numero di giorni in cui il certificato è considerato valido.</p></td>
   <td><p>3650</p><p>Potete usare un valore diverso, a seconda dei criteri aziendali.</p></td>
  </tr>
  <tr>
   <td><p>-storepass</p></td>
   <td><p>La password che protegge il contenuto dell'archivio di chiavi. </p></td>
   <td>
    <ul>
     <li><p>Keystore identità personalizzata: La password dell'archivio chiavi deve corrispondere alla password della credenziale SSL specificata per il componente Store attendibile della console di amministrazione.</p></li>
     <li><p>Keystore Trust personalizzato: Utilizzate la stessa password utilizzata per l'archivio di chiavi Identità personalizzata.</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>-keypass</p></td>
   <td><p>La password che protegge la chiave privata della coppia di chiavi.</p></td>
   <td><p>Utilizzate la stessa password utilizzata per l' <code>-storepass</code> opzione. La password della chiave deve contenere almeno sei caratteri.</p></td>
  </tr>
  <tr>
   <td><p>-dname</p></td>
   <td><p>Nome distinto che identifica la persona proprietaria dell'archivio di chiavi.</p></td>
   <td><p><code>"CN=</code><code>[User name]</code><code>,OU=</code><code>[Group Name]</code><code>, O=</code><code>[Company Name]</code><code>, L=</code><code>[City Name]</code><code>, S=</code><code>[State or province]</code><code>, C=</code><code>[Country Code]</code><code>"</code></p>
    <ul>
     <li><p><code><i>[User name]</i></code> è l'identificazione dell'utente proprietario dell'archivio di chiavi.</p></li>
     <li><p><code><i>[Group Name]</i></code> è l'identificazione del gruppo aziendale a cui appartiene il proprietario del keystore.</p></li>
     <li><p><code><i>[Company Name]</i></code> è il nome dell’organizzazione.</p></li>
     <li><p><code><i>[City Name]</i></code> è la città in cui si trova la vostra organizzazione.</p></li>
     <li><p><code><i>[State or province]</i></code> è lo stato o la provincia in cui si trova l’organizzazione.</p></li>
     <li><p><code><i>[Country Code]</i></code> è il codice di due lettere relativo al paese in cui si trova l'organizzazione.</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

Per ulteriori informazioni sull&#39;utilizzo del comando keytool, vedere il file keytool.html contenuto nella documentazione JDK.

## Creare gli archivi di chiavi Custom Identity and Trust {#create-the-custom-identity-and-trust-keystores}

1. Dal prompt dei comandi, andate a *[appserverdomain]*/adobe/*[server name]*.
1. Digitate il comando seguente:

   `[JAVA_HOME]/bin/keytool -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass store_password -keypass key_password -dname "CN=Hostname, OU=Group Name, O=Company Name, L=City Name, S=State,C=Country Code`

   >[!NOTE]
   >
   >Sostituire `[JAVA_HOME]`*con la directory in cui è installato il JDK e sostituire il testo in corsivo con valori che corrispondono al vostro ambiente.*

   Esempio:

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -genkey -v -alias ads-credentials -keyalg RSA -keystore "ads-credentials.jks" -validity 3650 -storepass P@ssw0rd -keypass P@ssw0rd -dname "CN=wasnode01, OU=LC, O=Adobe, L=Noida, S=UP,C=91
   ```

   Il file dell&#39;archivio di chiavi dell&#39;identità personalizzata denominato &quot;ads-Credits.jks&quot; viene creato nella directory [appserverdomain]/adobe/[server name] .

1. Estrarre il certificato dall&#39;archivio delle chiavi delle credenziali di annunci immettendo il seguente comando:

   [JAVA_HOME]`/bin/keytool -export -v -alias ads-credentials`

   `-file "ads-ca.cer" -keystore "ads-credentials.jks"`

   `-storepass` `*store*`*_**password**

   >[!NOTE]
   >
   >Sostituire `[JAVA_HOME]` con la directory in cui è installato il JDK e sostituire `store`*_* `password`* con la password per l&#39;archivio di chiavi Identità personalizzata.*

   Esempio:

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -export -v -alias ads-credentials -file "ads-ca.cer" -keystore "ads-credentials.jks" -storepass P@ssw0rd
   ```

   Il file del certificato denominato &quot;ads-ca.cer&quot; viene creato nella directory [appserverdomain]/adobe/[*server name*] .

1. Copiate il file ads-ca.cer nei computer host che richiedono una comunicazione sicura con il server dell&#39;applicazione.
1. Inserite il certificato in un nuovo file dell&#39;archivio chiavi (l&#39;archivio chiavi personalizzato) immettendo il seguente comando:

   [JAVA_HOME] `/bin/keytool -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass store_password -keypass key_password`

   >[!NOTE]
   >
   >Sostituire `[JAVA_HOME]` con la directory in cui è installato JDK e sostituire `store`*_* `password` e `key`*_* `password` *con le proprie password.*

   Esempio:

   ```java
   C:\Program Files\Java\jrockit-jdk1.6.0_24-R28\bin\keytool" -import -v -noprompt -alias bedrock -file "ads-ca.cer" -keystore "ads-ca.jks" -storepass Password1 -keypass Password1
   ```

Il file dell&#39;archivio chiavi personalizzato denominato &quot;ads-ca.jks&quot; viene creato nella directory [appserverdomain]/adobe/&#39;server&#39;.

Configurare WebLogic in modo che utilizzi l&#39;archivio chiavi identità personalizzata e l&#39;archivio chiavi trust personalizzato creato. Inoltre, disabilitare la funzione di verifica del nome host WebLogic perché il nome distinto utilizzato per creare i file dell&#39;archivio chiavi non includeva il nome del computer che ospita WebLogic Server.

## Configurare WebLogic per utilizzare SSL {#configure-weblogic-to-use-ssl}

1. Avviate la console di amministrazione di WebLogic Server digitando il nome `https://`*[]*host`:7001/console`nella riga URL di un browser Web.
1. In Ambiente, in Configurazioni dominio, selezionare **Server > &#39;server&#39; > Configurazione > Generale**.
1. In Generale, in Configuration (Configurazione), assicurarsi che la porta di **ascolto abilitata** e la porta di ascolto **SSL abilitata** siano selezionate. Se non è attivata, effettuate le seguenti operazioni:

   1. In Centro modifiche, fate clic su **Blocca e modifica** per modificare le selezioni e i valori.
   1. Selezionare le caselle di controllo Porta di **ascolto abilitata** e Porta di ascolto **SSL abilitata** .

1. Se il server è un server gestito, modificate Porta di ascolto in un valore di porta non utilizzato (ad esempio 8001) e Porta di ascolto SSL in un valore di porta non utilizzato (ad esempio 8002). Su un server autonomo, la porta SSL predefinita è 7002.
1. Fate clic su **Rilascia configurazione**.
1. In Ambiente, in Configurazioni dominio, fare clic su **Server > Server [*gestiti*]> Configurazione > Generale**.
1. In Generale, in Configurazione, selezionare **Keystores**.
1. In Centro modifiche, fate clic su **Blocca e modifica** per modificare le selezioni e i valori.
1. Fare clic su **Modifica** per ottenere l&#39;elenco a discesa degli archivi di chiavi e selezionare Identità **personalizzata e attendibilità** personalizzata.
1. In Identità, specificate i seguenti valori:

   **Keystore** identità personalizzata: *[appserverdomain]*/adobe/*[server name]*/ads-credentials.jks, dove *[appserverdomain] *è il percorso effettivo e il nome *[del]* server è il nome del server applicazione.

   **Tipo** archivio chiavi identità personalizzato: JKS

   **Passphrase** archivio chiavi identità personalizzata: *mypassword* (password dell&#39;archivio chiavi di identità personalizzata)

1. In Trust, specificate i seguenti valori:

   **Nome** file archivio chiavi trust personalizzato: `*[appserverdomain]*/adobe/*'server'*/ads-ca.jks`, dove `*[appserverdomain]*` è il percorso effettivo

   **Tipo** chiave trust personalizzato: JKS

   **Frase** Passaggio archivio chiavi trust personalizzato: *mypassword* (password della chiave di attendibilità personalizzata)

1. In Generale, in Configurazione, selezionate **SSL**.
1. Per impostazione predefinita, l&#39;opzione Keystore è selezionata per le posizioni di identità e attendibilità. In caso contrario, cambiatelo in keystore.
1. In Identità, specificate i seguenti valori:

   **Alias** chiave privata: ads-permissions

   **Passphrase**: *mypassword*

1. Fate clic su **Rilascia configurazione**.

## Disattiva la funzione di verifica del nome host {#disable-the-hostname-verification-feature}

1. Nella scheda Configurazione, fate clic su SSL.
1. In Avanzate, selezionate Nessuno dall&#39;elenco Verifica nome host.

   Se la verifica del nome host non è disabilitata, il nome comune (CN) deve contenere il nome host del server.

1. In Centro modifiche, fate clic su Blocca e modifica per modificare selezioni e valori.
1. Riavviate il server applicazione.

