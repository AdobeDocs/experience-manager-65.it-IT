---
title: Configurazione di SSL per WebSphere Application Server
seo-title: Configurazione di SSL per WebSphere Application Server
description: Scoprite come configurare SSL per WebSphere Application Server.
seo-description: Scoprite come configurare SSL per WebSphere Application Server.
uuid: f939a806-346e-41e0-b2c0-6d0ba83f8f6f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7c0efcb3-5b07-4090-9119-b7318c8b7980
translation-type: tm+mt
source-git-commit: 998a127ce00c6cbb3db3a81d8a89d97ab9ef7469
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 0%

---


# Configurazione di SSL per il server applicazioni WebSphere {#configuring-ssl-for-websphere-application-server}

Questa sezione include i passaggi seguenti per configurare SSL con il server applicazioni IBM WebSphere.

## Creazione di un account utente locale in WebSphere {#creating-a-local-user-account-on-websphere}

Per abilitare SSL, WebSphere richiede l&#39;accesso a un account utente nel registro utenti del sistema operativo locale che dispone dell&#39;autorizzazione per amministrare il sistema:

* (Windows) Create un nuovo utente Windows appartenente al gruppo Amministratori e dotato del privilegio di agire come parte del sistema operativo. (Vedere [Creare un utente Windows per WebSphere](configuring-ssl-websphere-application-server.md#create-a-windows-user-for-websphere).)
* (Linux, UNIX) L&#39;utente può essere un utente principale o un altro utente con privilegi di root. Quando si abilita SSL su WebSphere, utilizzare l&#39;identificazione del server e la password di questo utente.

### Creare un utente Linux o UNIX per WebSphere {#create-a-linux-or-unix-user-for-websphere}

1. Accedete come utente principale.
1. Create un utente immettendo il seguente comando in un prompt dei comandi:

   * (Linux e Sun Solaris) `useradd`
   * (IBM AIX) `mkuser`

1. Impostate la password del nuovo utente immettendo `passwd` nel prompt dei comandi.
1. (Linux e Solaris) Create un file di password shadow immettendo `pwconv` (senza parametri) nel prompt dei comandi.

   >[!NOTE]
   >
   >(Linux e Solaris) Per il funzionamento del Registro di sistema di sicurezza del sistema operativo locale del server applicazioni WebSphere, è necessario che esista un file di password shadow. Il file della password shadow è in genere denominato **/etc/shadow** e si basa sul file /etc/passwd. Se il file della password shadow non esiste, si verifica un errore dopo l&#39;attivazione della protezione globale e la configurazione del Registro di sistema come sistema operativo locale.

1. Aprite il file del gruppo dalla directory /etc in un editor di testo.
1. Aggiungete l&#39;utente creato al passaggio 2 al gruppo `root`.
1. Salvate e chiudete il file.
1. (UNIX con SSL abilitato) Avviare e arrestare WebSphere come utente principale.

### Creare un utente Windows per WebSphere {#create-a-windows-user-for-websphere}

1. Effettuate l&#39;accesso a Windows utilizzando un account utente amministratore.
1. Selezionare **Start > Pannello di controllo Campaign > Strumenti di amministrazione > Gestione computer > Utenti e gruppi locali**.
1. Fare clic con il pulsante destro del mouse su Utenti e selezionare **Nuovo utente**.
1. Digitate un nome utente e una password nelle caselle appropriate e digitate tutte le altre informazioni necessarie nelle caselle rimanenti.
1. Deselezionare **L&#39;utente deve cambiare la password al login successivo**, fare clic su **Crea**, quindi su **Chiudi**.
1. Fare clic su **Utenti**, fare clic con il pulsante destro del mouse sull&#39;utente appena creato e selezionare **Proprietà**.
1. Fare clic sulla scheda **Membro di**, quindi fare clic su **Aggiungi**.
1. Nella casella Immettere i nomi degli oggetti da selezionare, digitare `Administrators`, fare clic su Controlla nomi per verificare che il nome del gruppo sia corretto.
1. Fare clic su **OK**, quindi fare di nuovo clic su **OK**.
1. Selezionare **Start > Pannello di controllo Campaign > Strumenti di amministrazione > Criteri di sicurezza locali > Criteri locali**.
1. Fate clic su Assegnazione diritti utente, quindi fate clic con il pulsante destro del mouse su Agisci come parte del sistema operativo e selezionate Proprietà.
1. Fare clic su **Aggiungi utente o gruppo**.
1. Nella casella Immettere i nomi degli oggetti da selezionare, digitare il nome dell&#39;utente creato al punto 4, fare clic su **Controlla nomi** per verificare che il nome sia corretto, quindi fare clic su **OK**.
1. Fare clic su **OK** per chiudere la finestra di dialogo Agisci come parte della finestra di dialogo Proprietà sistema operativo.

### Configurare WebSphere per utilizzare l&#39;utente appena creato come Amministratore {#configure-websphere-to-use-the-newly-created-user-as-administrator}

1. Assicurarsi che WebSphere sia in esecuzione.
1. Nella console di amministrazione di WebSphere, selezionare **Protezione > Sicurezza globale**.
1. In Sicurezza amministrativa, selezionare **Ruoli utente amministrativi**.
1. Fate clic su Aggiungi ed effettuate le seguenti operazioni:

   1. Digitare **&amp;ast;** nella casella di ricerca e fare clic su Cerca.
   1. Fare clic su **Amministratore** in ruoli.
   1. Aggiungete l’utente appena creato a Mappato al ruolo e mapparlo ad Amministratore.

1. Fare clic su **OK** e salvare le modifiche.
1. Riavviare il profilo WebSphere.

## Abilita protezione amministrativa {#enable-administrative-security}

1. Nella console di amministrazione di WebSphere, selezionare **Protezione > Sicurezza globale**.
1. Fare clic su **Configurazione guidata sicurezza**.
1. Assicurarsi che la casella di controllo **Abilita protezione applicazione** sia abilitata. Fai clic su **Avanti**.
1. Selezionare **Federated Repository** e fare clic su **Next**.
1. Specificare le credenziali da impostare e fare clic su **Avanti**.
1. Fare clic su **Fine**.
1. Riavviare il profilo WebSphere.

   WebSphere inizierà a utilizzare l&#39;archivio di chiavi e l&#39;archivio di trust predefiniti.

## Abilita SSL (chiave personalizzata e trust store) {#enable-ssl-custom-key-and-truststore}

Truststore e keystore possono essere creati utilizzando l&#39;utility ikeyman o admin console. Per garantire il corretto funzionamento di ikeyman, verificare che il percorso di installazione di WebSphere non contenga parentesi.

1. Nella console di amministrazione di WebSphere, selezionare **Protezione > Certificato SSL e gestione chiavi**.
1. Fare clic su **Keystores and certificates** in Elementi correlati.
1. Nel menu a discesa **Uso dell&#39;archivio chiavi**, assicurarsi che sia selezionata l&#39;opzione **Keystores SSL**. Fai clic su **Nuovo**.
1. Digitare un nome logico e una descrizione.
1. Specificate il percorso in cui desiderate creare l&#39;archivio chiavi. Se avete già creato un archivio di chiavi tramite ikeyman, specificate il percorso del file dell&#39;archivio di chiavi.
1. Specificate e confermate la password.
1. Scegliete il tipo di archivio di chiavi e fate clic su **Applica**.
1. Salvate la configurazione principale.
1. Fare clic su **Certificato personale**.
1. Se hai già creato un archivio chiavi con ikeyman, verrà visualizzato il certificato. In caso contrario, è necessario aggiungere un nuovo certificato autofirmato eseguendo la procedura seguente:

   1. Selezionare **Crea > Certificato autofirmato**.
   1. Specificare i valori appropriati nel modulo del certificato. Assicurarsi di mantenere Alias e nome comune come nome di dominio completo del computer.
   1. Fare clic su **Applica**.

1. Ripetete i passaggi da 2 a 10 per creare un trust store.

## Applicare l&#39;archivio chiavi personalizzato e l&#39;archivio attendibili al server {#apply-custom-keystore-and-truststore-to-the-server}

1. Nella console di amministrazione di WebSphere, selezionare **Protezione > Certificato SSL e gestione chiavi**.
1. Fare clic su **Gestisci configurazione protezione endpoint**. Viene visualizzata la mappa topologia locale.
1. In Inbound (In entrata), selezionare direct child of nodes (figlio diretto dei nodi).
1. In Elementi correlati, selezionare **Configurazioni SSL**.
1. Selezionare **NodeDeafultSSLSetting**.
1. Negli elenchi a discesa Nome e Nome archivio chiavi, selezionate l&#39;archivio di dati attendibili e l&#39;archivio di chiavi personalizzato che avete creato.
1. Fare clic su **Applica**.
1. Salvate la configurazione principale.
1. Riavviare il profilo WebSphere.

   Il profilo ora viene eseguito in base alle impostazioni SSL personalizzate e al certificato.

## Abilitazione del supporto per AEM moduli nativi {#enabling-support-for-aem-forms-natives}

1. Nella console di amministrazione di WebSphere, selezionare **Protezione > Sicurezza globale**.
1. Nella sezione Autenticazione, espandere **Protezione RMI/IIOP** e fare clic su **Comunicazioni in ingresso CSIv2**.
1. Assicurarsi che l&#39;opzione **SSL-supported** sia selezionata nell&#39;elenco a discesa Trasporto.
1. Riavviare il profilo WebSphere.

## Configurazione di WebSphere per convertire gli URL che iniziano con https {#configuring-websphere-to-convert-urls-that-begins-with-https}

Per convertire un URL che inizia con https, aggiungi un certificato del firmatario per tale URL al server WebSphere.

**Creare un certificato del firmatario per un sito abilitato per https**

1. Assicurarsi che WebSphere sia in esecuzione.
1. Nella console di amministrazione di WebSphere, passare ai certificati del firmatario, quindi fare clic su Protezione > Certificato SSL e gestione chiave > Archivi e certificati chiave > NodeDefaultTrustStore > Certificati del firmatario.
1. Fate clic su Recupera da porta ed eseguite le seguenti operazioni:

   * Nella casella Host, digitate l&#39;URL. Ad esempio, digitare `www.paypal.com`.
   * Nella casella Porta digitare `443`. Questa porta è la porta SSL predefinita.
   * Nella casella Alias digitare un alias.

1. Fate clic su Recupera informazioni firmatario, quindi verificate che le informazioni vengano recuperate.
1. Fate clic su Applica, quindi su Salva.

La conversione da HTML a PDF dal sito il cui certificato è stato aggiunto ora funziona dal servizio Genera PDF.

>[!NOTE]
>
>Affinché un&#39;applicazione possa connettersi a siti SSL da WebSphere, è necessario un certificato del firmatario. Viene utilizzato da Java Secure Socket Extensions (JSSE) per convalidare i certificati inviati dal lato remoto durante un handshake SSL.

## Configurazione delle porte dinamiche {#configuring-dynamic-ports}

IBM WebSphere non consente più chiamate a ORB.init() quando la sicurezza globale è abilitata. Per informazioni sulla restrizione permanente, consultate https://www-01.ibm.com/support/docview.wss?uid=swg1PK58704.

Per impostare la porta come dinamica e risolvere il problema, effettuate le seguenti operazioni:

1. Nella console di amministrazione di WebSphere, selezionare **Server** > **Tipi di server** > **Server applicazioni WebSphere**.
1. Nella sezione Preferenze, selezionate il server.
1. Nella scheda **Configurazione**, nella sezione **Comunicazioni**, espandere **Porte** e fare clic su **Dettagli**.
1. Fare clic sui seguenti nomi di porta, modificare il numero di porta **a1/> in 0, quindi fare clic su** OK **.**

   * `ORB_LISTENER_ADDRESS`
   * `SAS_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_MUTUALAUTH_LISTENER_ADDRESS`

## Configurare il file sling.properties {#configure-the-sling-properties-file}

1. Aprire il file `[aem-forms_root]`\crx-repository\launchpad\sling.properties per la modifica.
1. Individuare la proprietà `sling.bootdelegation.ibm` e aggiungere `com.ibm.websphere.ssl.*`al relativo campo valore. Il campo aggiornato sarà simile al seguente:

   ```shell
   sling.bootdelegation.ibm=com.ibm.xml.*, com.ibm.websphere.ssl.*
   ```

1. Salva il file e riavvia il server.

