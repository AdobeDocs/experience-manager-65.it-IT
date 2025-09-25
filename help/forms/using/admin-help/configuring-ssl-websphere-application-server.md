---
title: Configurare SSL per il server applicazioni WebSphere
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
workflow-type: ht
source-wordcount: '1220'
ht-degree: 100%

---

# Configurare SSL per il server applicazioni WebSphere {#configuring-ssl-for-websphere-application-server}

In questa sezione sono descritti i passaggi per configurare SSL con il server applicazioni WebSphere di IBM.

## Creare un account utente locale in WebSphere {#creating-a-local-user-account-on-websphere}

Per abilitare SSL, WebSphere deve accedere a un account utente nel registro utenti del sistema operativo locale che dispone dell’autorizzazione per gestire il sistema:

* (Windows) Crea un utente di Windows che faccia parte del gruppo degli amministratori e che disponga dei privilegi necessari per operare a livello di sistema operativo. (Consulta [Creare un utente Windows per WebSphere](configuring-ssl-websphere-application-server.md#create-a-windows-user-for-websphere).)
* (Linux, UNIX) L’utente può essere un utente principale o un altro utente con privilegi illimitati. Quando abiliti SSL su WebSphere, utilizza l’identificazione del server e la password di questo utente.

### Creare un utente Linux o UNIX per WebSphere {#create-a-linux-or-unix-user-for-websphere}

1. Accedi come utente root.
1. Per creare un utente, immetti il comando seguente in un prompt dei comandi:

   * (Linux e Sun Solaris) `useradd`
   * (IBM AIX) `mkuser`

1. Imposta la password del nuovo utente immettendo `passwd` nel prompt dei comandi.
1. (Linux e Solaris) Crea un file di password crittografate immettendo `pwconv` (senza parametri) nel prompt dei comandi.

   >[!NOTE]
   >
   >(Linux e Solaris) Affinché il registro di sicurezza del sistema operativo locale del server applicazioni WebSphere funzioni correttamente, è necessario che esista un file di password crittografate. Il file di password crittografate è in genere denominato **/etc/shadow** ed è basato sul file /etc/passwd. Se il file di password crittografate non esiste, si verificherà un errore dopo l’abilitazione della sicurezza globale e la configurazione del registro utenti come sistema operativo locale.

1. Apri il file di gruppo dalla directory /etc in un editor di testo.
1. Aggiungi al gruppo `root` l’utente creato al punto 2.
1. Salva e chiudi il file.
1. (UNIX con SSL abilitato) Avvia e arresta WebSphere come utente root.

### Creare un utente Windows per WebSphere {#create-a-windows-user-for-websphere}

1. Accedi a Windows utilizzando un account utente amministratore.
1. Seleziona **Start > Pannello di controllo > Strumenti di amministrazione > Gestione computer > Utenti e gruppi locali**.
1. Fai clic con il pulsante destro del mouse su Utenti e seleziona **Nuovo utente**.
1. Digita un nome utente e una password nelle caselle corrispondenti e digita tutte le altre informazioni necessarie nelle altre caselle.
1. Deseleziona **L’utente deve modificare la password al prossimo accesso**, fai clic su **Crea**, quindi su **Chiudi**.
1. Fai clic su **Utenti**, fai clic con il pulsante destro del mouse sull’utente creato e seleziona **Proprietà**.
1. Fai clic sulla scheda **Membro di**, quindi su **Aggiungi**.
1. Nella casella Immetti i nomi degli oggetti da selezionare digita `Administrators` e fai clic su Controlla nomi per verificare che il nome del gruppo sia corretto.
1. Fai clic su **OK**, quindi di nuovo su **OK**.
1. Seleziona **Start > Pannello di controllo > Strumenti di amministrazione > Criteri di sicurezza locali > Criteri locali**.
1. Fai clic su Assegnazione diritti utente, quindi fai clic con il pulsante destro del mouse su Agisci come parte del sistema operativo e seleziona Proprietà.
1. Fai clic su **Aggiungi utente o gruppo**
1. Nella casella Immetti i nomi degli oggetti da selezionare digita il nome dell’utente creato al punto 4 e fai clic su **Controlla nomi** per verificare che il nome sia corretto, quindi fai clic su **OK**.
1. Fai clic su **OK** per chiudere la finestra di dialogo Proprietà di Agisci come parte del sistema operativo.

### Configurare WebSphere per l’utilizzo dell’utente appena creato come amministratore {#configure-websphere-to-use-the-newly-created-user-as-administrator}

1. Assicurati che WebSphere sia in esecuzione.
1. Nella console di amministrazione di WebSphere, seleziona **Sicurezza > Sicurezza globale**.
1. In Sicurezza amministrativa, seleziona **Ruoli utente amministrativi**.
1. Fai clic su Aggiungi e procedi come segue:

   1. Digita **&amp;ast;** nella casella di ricerca e fai clic su Cerca.
   1. Alla voce Ruoli, fai clic su **Amministratore**.
   1. Aggiungi l’utente appena creato al ruolo Mappato a e mappalo come Amministratore.

1. Fai clic su **OK** per salvare le modifiche.
1. Riavvia il profilo WebSphere.

## Abilita sicurezza amministrativa {#enable-administrative-security}

1. Nella console di amministrazione di WebSphere, seleziona **Protezione > Protezione globale**.
1. Fai clic su **Procedura guidata per la configurazione della protezione**.
1. Verifica che la casella di controllo **Abilita sicurezza applicazione** sia abilitata. Fai clic su **Avanti**.
1. Seleziona **Archivi federati** e fai clic su **Avanti**.
1. Specifica le credenziali da impostare e fai clic su **Avanti**.
1. Fai clic su **Fine**.
1. Riavvia il profilo WebSphere.

   WebSphere inizia a utilizzare il keystore e il truststore predefiniti.

## Abilita SSL (chiave e truststore personalizzati) {#enable-ssl-custom-key-and-truststore}

I TrustStore e i keystore possono essere creati utilizzando l’utilità ikeyman o Admin Console. Per il corretto funzionamento di ikeyman, verifica che il percorso di installazione di WebSphere non contenga parentesi.

1. Nella console di amministrazione di WebSphere, seleziona **Sicurezza > Certificato SSL e gestione chiavi**.
1. Fai clic su **Keystore e certificati** in Elementi correlati.
1. Nel menu a discesa **Utilizzi keystore**, accertati che sia selezionato **Keystore SSL**. Fai clic su **Nuovo**.
1. Digita un nome logico e una descrizione.
1. Specifica il percorso in cui desideri creare il keystore. Se hai già creato un keystore tramite ikeyman, specifica il percorso del file keystore.
1. Specifica e conferma la password.
1. Scegli il tipo di keystore e fai clic su **Applica**.
1. Salva la configurazione.
1. Fai clic su **Certificato personale**.
1. Se hai già aggiunto un keystore utilizzando ikeyman, verrà visualizzato il certificato. In caso contrario, devi aggiungere un nuovo certificato autofirmato eseguendo i seguenti passaggi:

   1. Seleziona **Crea > Certificato autofirmato**.
   1. Specifica i valori appropriati nel modulo del certificato. Accertati di mantenere Alias e nome comune come nome di dominio completo del computer.
   1. Fai clic su **Applica**.

1. Ripeti i passaggi da 2 a 10 per creare un truststore.

## Applica keystore e truststore personalizzati al server {#apply-custom-keystore-and-truststore-to-the-server}

1. Nella console di amministrazione di WebSphere, seleziona **Sicurezza > Certificato SSL e gestione chiavi**.
1. Fai clic su **Gestisci configurazione di sicurezza dell’endpoint**. Si apre la mappa topologica locale.
1. Sotto In entrata, seleziona l’elemento secondario diretto dei nodi.
1. In Elementi correlati seleziona **Configurazioni SSL**.
1. Seleziona **NodeDefaultSSLSetting**.
1. Dagli elenchi a discesa relativi a nome truststore e nome keystore, seleziona il truststore e il keystore personalizzati creati.
1. Fai clic su **Applica**.
1. Salva la configurazione.
1. Riavvia il profilo WebSphere.

   Il profilo ora viene eseguito con impostazioni SSL personalizzate e il certificato.

## Abilitazione del supporto per i moduli AEM Forms {#enabling-support-for-aem-forms-natives}

1. Nella console di amministrazione di WebSphere, seleziona **Sicurezza > Sicurezza globale**.
1. Nella sezione Autenticazione espandi **Sicurezza RMI/IIOP** e fai clic su **Comunicazioni CSIv2 in entrata**.
1. Verifica che **SSL-supported** sia selezionato nell’elenco a discesa Trasporto.
1. Riavvia il profilo WebSphere.

## Configurazione di WebSphere per la conversione degli URL che iniziano con https {#configuring-websphere-to-convert-urls-that-begins-with-https}

Per convertire un URL che inizia con https, aggiungi un certificato Firmatario per tale URL al server WebSphere.

**Crea un certificato Firmatario per un sito abilitato per https**

1. Assicurati che WebSphere sia in esecuzione.
1. Nella console di amministrazione di WebSphere passa a Certificati firmatario e quindi fai clic su Protezione > Certificato SSL e gestione chiavi > Archivi chiavi e certificati > NodeDefaultTrustStore > Certificati firmatario.
1. Fai clic su Recupera dalla porta ed esegui le operazioni seguenti:

   * Nella casella Host digita l’URL. Digitare, ad esempio, `www.paypal.com`.
   * Nella casella Porta digita `443`. Questa porta è la porta SSL predefinita.
   * Nella casella Alias digita un alias.

1. Fai clic su Recupera informazioni firmatario, quindi verifica che le informazioni vengano recuperate.
1. Fai clic su Applica e quindi su Salva.

La conversione da HTML a PDF dal sito di cui è stato aggiunto il certificato ora funziona dal servizio Genera PDF.

>[!NOTE]
>
>Affinché un’applicazione possa connettersi ai siti SSL dall’interno di WebSphere, è necessario un certificato del firmatario. Viene utilizzato da Java Secure Socket Extensions (JSSE) per convalidare i certificati inviati dal lato remoto della connessione durante un handshake SSL.

## Configurazione delle porte dinamiche {#configuring-dynamic-ports}

IBM WebSphere non consente più chiamate a ORB.init() quando è abilitata la sicurezza globale. Per maggiori informazioni sulla restrizione permanente, consulta https://www-01.ibm.com/support/docview.wss?uid=swg1PK58704.

Per impostare la porta come dinamica e risolvere il problema, effettua le seguenti operazioni:

1. Nella console di amministrazione di WebSphere, seleziona **Server** > **Tipi di server** > **Server applicazioni WebSphere**.
1. Nella sezione Preferenze, seleziona il server.
1. Nella scheda **Configurazione**, nella sezione **Comunicazioni**, espandi **Porte** e fai clic su **Dettagli**.
1. Fai clic sui seguenti nomi della porta, cambia il **numero di porta** in 0 e fai clic su **OK**.

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

1. Salva il file e riavvia il server.
