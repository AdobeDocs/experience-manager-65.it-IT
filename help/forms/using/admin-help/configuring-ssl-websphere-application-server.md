---
title: Configurazione di SSL per WebSphere Application Server
seo-title: Configuring SSL for WebSphere Application Server
description: Scopri come configurare SSL per WebSphere Application Server.
seo-description: Learn how to configure SSL for WebSphere Application Server.
uuid: f939a806-346e-41e0-b2c0-6d0ba83f8f6f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7c0efcb3-5b07-4090-9119-b7318c8b7980
exl-id: b0786b52-879e-4a24-9cc9-bd9dcb2473cc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 1%

---

# Configurazione di SSL per WebSphere Application Server {#configuring-ssl-for-websphere-application-server}

Questa sezione include i passaggi seguenti per configurare SSL con il server applicazioni IBM WebSphere.

## Creazione di un account utente locale su WebSphere {#creating-a-local-user-account-on-websphere}

Per abilitare SSL, WebSphere richiede l&#39;accesso a un account utente nel registro utenti del sistema operativo locale che dispone dell&#39;autorizzazione per amministrare il sistema:

* (Windows) Crea un nuovo utente Windows che fa parte del gruppo Administrators e ha il privilegio di agire come parte del sistema operativo. (Vedi [Creare un utente Windows per WebSphere](configuring-ssl-websphere-application-server.md#create-a-windows-user-for-websphere).)
* (Linux, UNIX) L&#39;utente può essere un utente root o un altro utente con privilegi root. Quando si abilita SSL su WebSphere, utilizzare l&#39;identificazione del server e la password di questo utente.

### Creare un utente Linux o UNIX per WebSphere {#create-a-linux-or-unix-user-for-websphere}

1. Accedi come utente principale.
1. Crea un utente immettendo il seguente comando in un prompt dei comandi:

   * (Linux e Sun Solaris) `useradd`
   * (IBM AIX) `mkuser`

1. Impostare la password del nuovo utente immettendo `passwd` nel prompt dei comandi.
1. (Linux e Solaris) Crea un file di password shadow immettendo `pwconv` (senza parametri) nel prompt dei comandi.

   >[!NOTE]
   >
   >(Linux e Solaris) Affinché il Registro di sistema di sicurezza locale del sistema operativo del sistema operativo WebSphere Application Server funzioni, deve esistere un file di password shadow. Il nome del file della password shadow è in genere **/etc/shadow** e si basa sul file /etc/passwd. Se il file di password shadow non esiste, si verifica un errore dopo aver abilitato la sicurezza globale e configurato il registro utente come sistema operativo locale.

1. Apri il file di gruppo dalla directory /etc in un editor di testo.
1. Aggiungi l&#39;utente creato al passaggio 2 al `root` gruppo.
1. Salva e chiudi il file 
1. (UNIX con SSL abilitato) Avvia e arresta WebSphere come utente principale.

### Creare un utente Windows per WebSphere {#create-a-windows-user-for-websphere}

1. Accedi a Windows utilizzando un account utente amministratore.
1. Seleziona **Start > Pannello di controllo Campaign > Strumenti di amministrazione > Gestione computer > Utenti e gruppi locali**.
1. Fai clic con il pulsante destro del mouse su Utenti e seleziona **Nuovo utente**.
1. Digitare un nome utente e una password nelle caselle appropriate e digitare tutte le altre informazioni necessarie nelle caselle rimanenti.
1. Deseleziona **L&#39;Utente Deve Cambiare Password Al Successivo Accesso**, fai clic su **Crea**, quindi fai clic su **Chiudi**.
1. Fai clic su **Utenti**, fai clic con il pulsante destro del mouse sull’utente appena creato e seleziona **Proprietà**.
1. Fai clic sul pulsante **Membro di** , quindi fai clic su **Aggiungi**.
1. Nella casella Immettere i nomi degli oggetti da selezionare digitare `Administrators`, fai clic su Controlla nomi per verificare che il nome del gruppo sia corretto.
1. Fai clic su **OK** quindi fai clic su **OK** di nuovo.
1. Seleziona **Start > Pannello di controllo Campaign > Strumenti di amministrazione > Criteri di sicurezza locali > Criteri locali**.
1. Fare clic su Assegnazione diritti utente, quindi fare clic con il pulsante destro del mouse su Agisci come parte del sistema operativo e selezionare Proprietà.
1. Fai clic su **Aggiungi utente o gruppo**.
1. Nella casella Immettere i nomi degli oggetti da selezionare digitare il nome dell&#39;utente creato al punto 4, fare clic su **Controlla nomi** per verificare che il nome sia corretto, quindi fare clic su **OK**.
1. Fai clic su **OK** per chiudere la funzione Agisci come parte della finestra di dialogo Proprietà sistema operativo.

### Configura WebSphere per utilizzare l&#39;utente appena creato come amministratore {#configure-websphere-to-use-the-newly-created-user-as-administrator}

1. Assicurati che WebSphere sia in esecuzione.
1. Nella console amministrativa di WebSphere, selezionare **Sicurezza > Sicurezza globale**.
1. In Sicurezza amministrativa, selezionare **Ruoli utente amministrativi**.
1. Fai clic su Aggiungi ed effettua le seguenti operazioni:

   1. Tipo **&amp;ast;** nella casella di ricerca e fare clic su ricerca.
   1. Fai clic su **Amministratore** in ruoli.
   1. Aggiungi l’utente appena creato a Mapped (Mappato) al ruolo e mappalo all’amministratore.

1. Fai clic su **OK** e salva le modifiche.
1. Riavvia il profilo WebSphere.

## Abilita protezione amministrativa {#enable-administrative-security}

1. Nella console amministrativa di WebSphere, selezionare **Sicurezza > Sicurezza globale**.
1. Fai clic su **Configurazione guidata sicurezza**.
1. Assicurati **Abilita protezione applicazione** la casella di controllo è abilitata. Fai clic su **Avanti**.
1. Seleziona **Repository federati** e fai clic su **Successivo**.
1. Specificare le credenziali da impostare e fare clic su **Successivo**.
1. Fai clic su **Fine**.
1. Riavvia il profilo WebSphere.

   WebSphere inizierà a utilizzare il keystore e il truststore predefiniti.

## Abilita SSL (chiave personalizzata e truststore) {#enable-ssl-custom-key-and-truststore}

Puoi creare TrustStore e keystores utilizzando l&#39;utility ikeyman o admin console. Per il corretto funzionamento di ikeyman, assicurarsi che il percorso di installazione di WebSphere non contenga parentesi.

1. Nella console amministrativa di WebSphere, selezionare **Sicurezza > Certificato SSL e gestione delle chiavi**.
1. Fai clic su **Registro chiavi e certificati** alla voce Articoli correlati.
1. In **Uso chiave dell&#39;archivio** a discesa, assicurati che **Keyshop SSL** è selezionato. Fai clic su **Nuovo**.
1. Digitare un nome logico e una descrizione.
1. Specifica il percorso in cui desideri creare il tuo keystore. Se hai già creato un keystore tramite ikeyman, specifica il percorso del file keystore.
1. Specifica e conferma la password.
1. Scegli il tipo di archivio chiavi e fai clic su **Applica**.
1. Salva la configurazione master.
1. Fai clic su **Certificato personale**.
1. Se hai aggiunto un keystore già creato utilizzando ikeyman, verrà visualizzato il certificato. In caso contrario, è necessario aggiungere un nuovo certificato autofirmato eseguendo i seguenti passaggi:

   1. Seleziona **Crea > Certificato autofirmato**.
   1. Specificare i valori appropriati nel modulo del certificato. Assicurati di mantenere l&#39;alias e il nome comune come nome di dominio completo del computer.
   1. Fai clic su **Applica**.

1. Ripetere i passaggi da 2 a 10 per creare un truststore.

## Applica il keystore personalizzato e il truststore al server {#apply-custom-keystore-and-truststore-to-the-server}

1. Nella console amministrativa di WebSphere, selezionare **Sicurezza > Certificato SSL e gestione delle chiavi**.
1. Fai clic su **Gestione della configurazione di sicurezza dell’endpoint**. Viene visualizzata la mappa della topologia locale.
1. In Inbound, seleziona figlio diretto dei nodi.
1. In Articoli correlati, selezionare **Configurazioni SSL**.
1. Seleziona **NodeDefaultSSLSetting**.
1. Dall’elenco a discesa nome e nome dell’archivio chiavi, seleziona l’archivio dati e l’archivio chiavi personalizzati che hai creato.
1. Fai clic su **Applica**.
1. Salva la configurazione master.
1. Riavvia il profilo WebSphere.

   Il tuo profilo ora viene eseguito sulle impostazioni SSL personalizzate e sul certificato.

## Abilitazione del supporto per gli elementi nativi dei moduli AEM {#enabling-support-for-aem-forms-natives}

1. Nella console amministrativa di WebSphere, selezionare **Sicurezza > Sicurezza globale**.
1. Nella sezione Autenticazione , espandi **Sicurezza RMI/IIOP** e fai clic su **Comunicazioni in entrata CSIv2**.
1. Assicurati che **Supportato da SSL** è selezionato nell’elenco a discesa Trasporto .
1. Riavvia il profilo WebSphere.

## Configurazione di WebSphere per convertire gli URL che iniziano con https {#configuring-websphere-to-convert-urls-that-begins-with-https}

Per convertire un URL che inizia con https, aggiungi un certificato Signer per tale URL al server WebSphere.

**Creare un certificato del firmatario per un sito abilitato https**

1. Assicurati che WebSphere sia in esecuzione.
1. Nella console di amministrazione di WebSphere, passa ai certificati del firmatario, quindi fai clic su Protezione > Certificato SSL e gestione chiavi > Archivio chiavi e certificati > NodeDefaultTrustStore > Certificati del firmatario.
1. Fai clic su Recupera da porta ed esegui le seguenti attività:

   * Nella casella Host , digita l’URL. Ad esempio, digitare `www.paypal.com`.
   * Nella casella Porta digitare `443`. Questa porta è la porta SSL predefinita.
   * Nella casella Alias, digitare un alias.

1. Fai clic su Recupera informazioni firmatario e verifica che le informazioni siano recuperate.
1. Fare clic su Applica e quindi su Salva.

La conversione da HTML a PDF dal sito di cui viene aggiunto il certificato ora funziona dal servizio Generate PDF .

>[!NOTE]
>
>Affinché un&#39;applicazione possa connettersi a siti SSL dall&#39;interno di WebSphere, è necessario un certificato Signer. Viene utilizzato da Java Secure Socket Extensions (JSSE) per convalidare i certificati inviati dal lato remoto durante un handshake SSL.

## Configurazione delle porte dinamiche {#configuring-dynamic-ports}

IBM WebSphere non consente più chiamate a ORB.init() quando la sicurezza globale è abilitata. Per informazioni sulla restrizione permanente, consulta https://www-01.ibm.com/support/docview.wss?uid=swg1PK58704.

Esegui i seguenti passaggi per impostare la porta come dinamica e risolvere il problema:

1. Nella console amministrativa di WebSphere, selezionare **Server** > **Tipi di server** > **Server applicazioni WebSphere**.
1. Nella sezione Preferenze, seleziona il server.
1. In **Configurazione** sotto **Comunicazioni** sezione, espandi **Porte** e fai clic su **Dettagli**.
1. Fare clic sui seguenti nomi di porta, modificare il **numero di porta** a 0, quindi fai clic su **OK**.

   * `ORB_LISTENER_ADDRESS`
   * `SAS_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_MUTUALAUTH_LISTENER_ADDRESS`

## Configura il file sling.properties {#configure-the-sling-properties-file}

1. Apri `[aem-forms_root]`\crx-repository\launchpad\sling.properties file per la modifica.
1. Individua il `sling.bootdelegation.ibm` e aggiungi `com.ibm.websphere.ssl.*`al relativo campo valore. Il campo aggiornato ha un aspetto simile al seguente:

   ```shell
   sling.bootdelegation.ibm=com.ibm.xml.*, com.ibm.websphere.ssl.*
   ```

1. Salva il file e riavvia il server.
