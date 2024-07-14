---
title: Configurazione di SSL per l'Application Server WebSphere
description: Scopri come configurare SSL per il server applicazioni WebSphere.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: b0786b52-879e-4a24-9cc9-bd9dcb2473cc
solution: Experience Manager, Experience Manager Forms
feature: Document Security
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 0%

---

# Configurazione di SSL per l&#39;Application Server WebSphere {#configuring-ssl-for-websphere-application-server}

In questa sezione sono descritti i passaggi seguenti per configurare SSL con l&#39;Application Server IBM WebSphere.

## Creazione di un account utente locale in WebSphere {#creating-a-local-user-account-on-websphere}

Per abilitare SSL, WebSphere deve accedere a un account utente nel registro utenti del sistema operativo locale che dispone dell&#39;autorizzazione per amministrare il sistema:

* (Windows) Creare un utente di Windows che faccia parte del gruppo Administrators e che disponga dei privilegi necessari per operare come parte del sistema operativo. (Vedi [Creare un utente Windows per WebSphere](configuring-ssl-websphere-application-server.md#create-a-windows-user-for-websphere).)
* (Linux, UNIX) L&#39;utente può essere un utente root o un altro utente con privilegi root. Quando si abilita SSL su WebSphere, utilizzare l&#39;identificazione del server e la password dell&#39;utente.

### Creare un utente Linux o UNIX per WebSphere {#create-a-linux-or-unix-user-for-websphere}

1. Accedi come utente principale.
1. Crea un utente immettendo il comando seguente in un prompt dei comandi:

   * (Linux e Sun Solaris) `useradd`
   * (IBM AIX) `mkuser`

1. Impostare il password del nuovo utente immettendo `passwd` il prompt dei comandi.
1. (Linux e Solaris) Crea un file shadow password immettendo `pwconv` (senza parametri) nel prompt dei comandi.

   >[!NOTE]
   >
   >(Linux e Solaris) Affinché il registro di sicurezza del sistema operativo locale di WebSphere Application Server funzioni, è necessario che esista un file shadow password. Il file shadow password è solitamente denominato **/etc/shadow** ed è basato sul file /etc/passwd. Se il file shadow password non esiste, si verifica un errore dopo l&#39;abilitazione della protezione globale e la configurazione del registro di utente come sistema operativo locale.

1. Aprire il file di gruppo dalla directory /etc in un editor di testo.
1. Aggiungi al `root` gruppo il utente creato nel passaggio 2.
1. Salva e chiudi il file.
1. (UNIX con SSL abilitato) Avviare e arrestare WebSphere come utente root.

### Creare un utente Windows per WebSphere {#create-a-windows-user-for-websphere}

1. Accedere a Windows utilizzando un account utente amministratore.
1. Selezionare **Start > Pannello di controllo Campaign > Strumenti di amministrazione > Gestione computer > Utenti e gruppi locali**.
1. Fare clic con il pulsante destro del mouse su Utenti e selezionare **Nuovo utente**.
1. Digitare un nome utente e una password nelle caselle corrispondenti e digitare tutte le altre informazioni necessarie nelle caselle rimanenti.
1. Deseleziona **L&#39;utente deve modificare la password al prossimo accesso**, fai clic su **Crea**, quindi fai clic su **Chiudi**.
1. Fai clic su **Utenti**, fai clic con il pulsante destro del mouse sull&#39;utente creato e seleziona **Proprietà**.
1. Fare clic sulla scheda **Membro di** e quindi su **Aggiungi**.
1. Nella casella Immettere i nomi degli oggetti da selezionare digitare `Administrators` e fare clic su Controlla nomi per verificare che il nome del gruppo sia corretto.
1. Fare clic su **OK** e quindi di nuovo su **OK**.
1. Selezionare **Start > Pannello di controllo Campaign > Strumenti di amministrazione > Criteri di protezione locali > Criteri locali**.
1. Fare clic su Assegnazione diritti utente, quindi fare clic con il pulsante destro del mouse su Agisci come parte del sistema operativo e selezionare Proprietà.
1. Fare clic su **Aggiungi utente o gruppo**.
1. Nella casella Immettere i nomi degli oggetti da selezionare digitare il nome dell&#39;utente creato al passaggio 4, fare clic su **Controlla nomi** per verificare che il nome sia corretto e quindi fare clic su **OK**.
1. Fare clic su **OK** per chiudere la finestra di dialogo Agisci come parte delle proprietà del sistema operativo.

### Configurare WebSphere per l&#39;utilizzo dell&#39;utente appena creato come amministratore {#configure-websphere-to-use-the-newly-created-user-as-administrator}

1. Verificare che WebSphere sia in esecuzione.
1. Nella console di amministrazione di WebSphere, selezionare **Sicurezza > Sicurezza globale**.
1. In Protezione amministrativa, selezionare **Ruoli utente amministrativi**.
1. Fai clic su Aggiungi ed effettua le seguenti operazioni:

   1. Digitare **&amp;ast;** nella casella di ricerca e fare clic su Cerca.
   1. Fare clic su **Amministratore** in Ruoli.
   1. Aggiungi l’utente appena creato al ruolo Mappato a e mappalo ad Amministratore.

1. Fai clic su **OK** e salva le modifiche.
1. Riavviare il profilo WebSphere.

## Abilita sicurezza amministrativa {#enable-administrative-security}

1. Nella console di amministrazione di WebSphere, selezionare **Sicurezza > Sicurezza globale**.
1. Fare clic su **Configurazione guidata protezione**.
1. Verificare che la casella di controllo **Abilita sicurezza applicazione** sia abilitata. Fai clic su **Avanti**.
1. Seleziona **Archivi federati** e fai clic su **Avanti**.
1. Specificare le credenziali da impostare e fare clic su **Avanti**.
1. Fare clic su **Fine**.
1. Riavviare il profilo WebSphere.

   WebSphere inizia a utilizzare il keystore e il truststore predefiniti.

## Abilita SSL (chiave personalizzata e truststore) {#enable-ssl-custom-key-and-truststore}

I TrustStore e i keystore possono essere creati utilizzando l&#39;utilità ikeyman o Admin Console. Per il corretto funzionamento di ikeyman, verificare che il percorso di installazione di WebSphere non contenga parentesi.

1. Nella console di amministrazione di WebSphere, selezionare **Sicurezza > Certificato SSL e gestione chiavi**.
1. Fare clic su **Registri chiavi e certificati** in Elementi correlati.
1. Nel menu a discesa **Utilizzi archivio chiavi**, accertati che sia selezionato **Archivio chiavi SSL**. Fare clic su **Nuovo**.
1. Digitare un nome logico e una descrizione.
1. Specifica il percorso in cui desideri creare il keystore. Se avete già creato un keystore tramite ikeyman, specificate il percorso del file keystore.
1. Specifica e conferma la password.
1. Scegliere il tipo di keystore e fare clic su **Applica**.
1. Salva la configurazione principale.
1. Fare clic su **Certificato personale**.
1. Se hai già aggiunto un keystore utilizzando ikeyman, verrà visualizzato il certificato. In caso contrario, devi aggiungere un nuovo certificato autofirmato eseguendo i seguenti passaggi:

   1. Selezionare **Crea > Certificato** autofirmato.
   1. Specificare i valori appropriati nel modulo del certificato. Assicurarsi di mantenere Alias e nome comune come nome di dominio completo della macchina.
   1. Fai clic su **Applica**.

1. Ripeti i passaggi da 2 a 10 per creare un truststore.

## Applica keystore personalizzato e truststore al server {#apply-custom-keystore-and-truststore-to-the-server}

1. Nella console di amministrazione di WebSphere, selezionare **Sicurezza > gestione dei certificati SSL e delle chiavi**.
1. Fare clic su **Gestisci configurazione** sicurezza endpoint. Viene visualizzata la mappa della topologia locale.
1. In In entrata selezionare figlio diretto dei nodi.
1. In Elementi correlati, selezionare **Configurazioni SSL**.
1. Selezionare **NodeDeafultSSLSetting**.
1. Dall&#39;elenco a discesa nome truststore e nome keystore, selezionare il truststore personalizzato e il keystore creato.
1. Fai clic su **Applica**.
1. Salva la configurazione principale.
1. Riavviare il profilo WebSphere.

   Il profilo ora viene eseguito con impostazioni SSL personalizzate e il certificato.

## Abilitazione del supporto per i moduli AEM nativi {#enabling-support-for-aem-forms-natives}

1. Nella console di amministrazione di WebSphere, selezionare **Sicurezza > Sicurezza globale**.
1. Nella sezione Autenticazione espandere **Protezione RMI/IIOP** e fare clic su **Comunicazioni in entrata CSIv2**.
1. Verificare che **SSL-supported** sia selezionato nell&#39;elenco a discesa Trasporto.
1. Riavviare il profilo WebSphere.

## Configurazione di WebSphere per la conversione degli URL che iniziano con https {#configuring-websphere-to-convert-urls-that-begins-with-https}

Per convertire un URL che inizia con https, aggiungere un certificato Firmatario per tale URL al server WebSphere.

**Creare un certificato firmatario per un sito abilitato per https**

1. Verificare che WebSphere sia in esecuzione.
1. In WebSphere Administrative Console passare a Certificati firmatario e quindi fare clic su Protezione > Certificato SSL e gestione chiavi > Archivi chiavi e certificati > NodeDefaultTrustStore > Certificati firmatari.
1. Fare clic su Recupera dalla porta ed eseguire le operazioni seguenti:

   * Nella casella Host digitare l&#39;URL. Digitare ad esempio `www.paypal.com`.
   * Nella casella Porta digitare `443`. Questa porta è la porta SSL predefinita.
   * Nella casella Alias digitare un alias.

1. Fare clic su Recupera informazioni firmatario, quindi verificare che le informazioni vengano recuperate.
1. Fare clic su Applica e quindi su Salva.

La conversione da HTML a PDF dal sito di cui è stato aggiunto il certificato ora funziona dal servizio Genera PDF.

>[!NOTE]
>
>Affinché un&#39;applicazione possa connettersi ai siti SSL dall&#39;interno di WebSphere, è necessario un certificato del firmatario. Viene utilizzato da Java Secure Socket Extensions (JSSE) per convalidare i certificati inviati dal lato remoto della connessione durante un handshake SSL.

## Configurazione delle porte dinamiche {#configuring-dynamic-ports}

IBM WebSphere non consente più chiamate a ORB.init() quando la sicurezza globale è abilitata. Per maggiori informazioni sulla restrizione permanente, consulta https://www-01.ibm.com/support/docview.wss?uid=swg1PK58704.

Per impostare la porta come dinamica e risolvere il problema, effettuare le seguenti operazioni:

1. Nella console di amministrazione di WebSphere, selezionare **Server** > **Tipi di server** > **Server applicazioni WebSphere**.
1. Nella sezione Preferenze, seleziona il server.
1. Nella scheda **Configurazione**, nella sezione **Comunicazioni**, espandi **Porte** e fai clic su **Dettagli**.
1. Fare clic sui seguenti nomi di porta, modificare **numero di porta** in 0 e fare clic su **OK**.

   * `ORB_LISTENER_ADDRESS`
   * `SAS_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_MUTUALAUTH_LISTENER_ADDRESS`

## Configurare il file sling.properties {#configure-the-sling-properties-file}

1. Apri il file `[aem-forms_root]`\crx-repository\launchpad\sling.properties per la modifica.
1. Individua la proprietà `sling.bootdelegation.ibm` e aggiungi `com.ibm.websphere.ssl.*` al relativo campo del valore. Il campo aggiornato è simile al seguente:

   ```shell
   sling.bootdelegation.ibm=com.ibm.xml.*, com.ibm.websphere.ssl.*
   ```

1. Salvare il file e riavviare il server.
