---
title: Elenco di controllo protezione
seo-title: Elenco di controllo protezione
description: Scoprite le varie considerazioni di sicurezza per la configurazione e la distribuzione dei AEM.
seo-description: Scoprite le varie considerazioni di sicurezza per la configurazione e la distribuzione dei AEM.
uuid: 8e293316-4177-4271-87c6-9dc1a2e85a07
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: de7d7209-c194-4d19-853b-468ebf3fa4b2
docset: aem65
translation-type: tm+mt
source-git-commit: 474fc122f557f32d34fddd9d35a113431f6ce491
workflow-type: tm+mt
source-wordcount: '2841'
ht-degree: 0%

---


# Elenco di controllo protezione {#security-checklist}

Questa sezione descrive i vari passaggi da effettuare per garantire che l&#39;installazione AEM sia sicura quando distribuita. L&#39;elenco di controllo deve essere applicato dall&#39;alto verso il basso.

>[!NOTE]
>
>Ulteriori informazioni [sono disponibili anche sulle minacce alla sicurezza più pericolose come pubblicato da Open Web Application Security Project (OWASP)](https://www.owasp.org/index.php/OWASP_Top_Ten_Project).

>[!NOTE]
>
>Nella fase di sviluppo sono disponibili alcune considerazioni aggiuntive relative alla [sicurezza](/help/sites-developing/dev-guidelines-bestpractices.md#security-considerations).

## Principali misure di sicurezza {#main-security-measures}

### Eseguire AEM in modalità pronta produzione {#run-aem-in-production-ready-mode}

Per ulteriori informazioni, vedere [Esecuzione AEM in modalità pronta per la produzione](/help/sites-administering/production-ready.md).

### Abilita HTTPS per la sicurezza del livello di trasporto {#enable-https-for-transport-layer-security}

L&#39;abilitazione del livello di trasporto HTTPS sia sulle istanze di creazione che di pubblicazione è obbligatoria per disporre di un&#39;istanza protetta.

>[!NOTE]
>
>Per ulteriori informazioni, vedere la sezione [Abilitazione di HTTP su SSL](/help/sites-administering/ssl-by-default.md).

### Installazione degli hotfix di sicurezza {#install-security-hotfixes}

Assicurarsi di aver installato gli [hotfix di sicurezza più recenti forniti da  Adobe](https://helpx.adobe.com/it/experience-manager/kb/aem63-available-hotfixes.html).

### Modificare le password predefinite per gli account amministratore di AEM e console OSGi {#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts}

 Adobe consiglia vivamente di cambiare la password per gli account [**AEM** `admin` ](#changing-the-aem-admin-password) privilegiati dopo l&#39;installazione (in tutte le istanze).

Questi account includono:

* L&#39;account AEM `admin`

   Dopo aver modificato la password dell&#39;account amministratore AEM, dovrete utilizzare la nuova password per accedere a CRX.

* La `admin` password per la console Web OSGi

   Questa modifica verrà applicata anche all&#39;account amministratore utilizzato per accedere alla console Web, pertanto dovrete utilizzare la stessa password per accedervi.

Questi due account utilizzano credenziali separate e dispongono di una password distinta e complessa per ciascuno di essi è fondamentale per una distribuzione protetta.

#### Modifica della password amministratore AEM {#changing-the-aem-admin-password}

La password per l&#39;account amministratore AEM può essere modificata tramite la console [Granite Operations - Users](/help/sites-administering/granite-user-group-admin.md).

Qui è possibile modificare l&#39;account `admin` e [cambiare la password](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user).

>[!NOTE]
>
>Modificando l’account amministratore viene modificato anche l’account della console Web OSGi. Dopo aver modificato l’account amministratore, dovete cambiare l’account OSGi in qualcosa di diverso.

#### Importanza della modifica della password della console Web OSGi {#importance-of-changing-the-osgi-web-console-password}

A parte l&#39;account AEM `admin`, la mancata modifica della password predefinita per la console Web OSGi può portare a:

* Esposizione del server con una password predefinita durante l&#39;avvio e lo spegnimento (che può richiedere minuti per i server di grandi dimensioni);
* Esposizione del server quando il repository è inattivo/riavviato e OSGI è in esecuzione.

Per ulteriori informazioni sulla modifica della password della console Web, vedere [Modifica della password amministratore della console Web OSGi](/help/sites-administering/security-checklist.md#changing-the-osgi-web-console-admin-password) di seguito.

#### Modifica della password amministratore della console Web OSGi {#changing-the-osgi-web-console-admin-password}

È inoltre necessario modificare la password utilizzata per accedere alla console Web. A tal fine, è possibile configurare le seguenti proprietà della [console di gestione Apache Felix OSGi](/help/sites-deploying/osgi-configuration-settings.md):

**Nome utente** e  **password**, le credenziali per accedere alla console di gestione Web Apache Felix stessa.
La password deve essere modificata dopo l’installazione iniziale per garantire la sicurezza dell’istanza.

Per effettuare ciò:

1. Andate alla console Web all&#39;indirizzo `<server>:<port>/system/console/configMgr`.
1. Andate a **Apache Felix OSGi Management Console** e modificate i **nomi utente** e **password**.

   ![chlimage_1-3](assets/chlimage_1-3.png)

1. Fai clic su **Salva**.

### Implementazione del gestore errori personalizzato {#implement-custom-error-handler}

 Adobe consiglia di definire pagine del gestore di errori personalizzate, in particolare per i codici di risposta HTTP 404 e 500 al fine di impedire la divulgazione delle informazioni.

>[!NOTE]
>
>Per ulteriori informazioni, vedere [Come creare script personalizzati o gestori di errori](https://helpx.adobe.com/experience-manager/kb/CustomErrorHandling.html) articolo della knowledge base.

### Elenco di controllo completo per la protezione del dispatcher {#complete-dispatcher-security-checklist}

AEM Dispatcher è un elemento fondamentale dell&#39;infrastruttura.  Adobe consiglia vivamente di completare la [lista di controllo della protezione del dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/security-checklist.html).

>[!CAUTION]
>
>Utilizzando il dispatcher è necessario disabilitare il selettore &quot;.form&quot;.

## Passaggi di verifica {#verification-steps}

### Configurare gli utenti di replica e trasporto {#configure-replication-and-transport-users}

Un&#39;installazione standard di AEM specifica `admin` come utente per le credenziali di trasporto all&#39;interno degli [agenti di replica ](/help/sites-deploying/replication.md) predefiniti. Inoltre, l&#39;utente amministratore viene utilizzato per eseguire la replica nel sistema di creazione.

Per motivi di sicurezza, è opportuno modificare entrambe le opzioni in modo da riflettere il caso d’uso specifico in questione, tenendo presenti i due aspetti seguenti:

* L&#39; **utente di trasporto** non deve essere l&#39;utente amministratore. Configurate invece un utente nel sistema di pubblicazione che disponga solo dei diritti di accesso alle porzioni pertinenti del sistema di pubblicazione e utilizzate le credenziali dell&#39;utente per il trasporto.

   È possibile iniziare dall&#39;utente del ricevitore di replica in bundle e configurare i diritti di accesso dell&#39;utente in modo che corrispondano alla propria situazione

* Anche l&#39; **utente di replica** o **ID utente agente** non deve essere l&#39;utente amministratore, ma un utente che può visualizzare solo il contenuto che deve essere replicato. L&#39;utente di replica viene utilizzato per raccogliere il contenuto da replicare nel sistema di creazione prima che venga inviato all&#39;editore.

### Controllare gli stati di sicurezza del dashboard delle operazioni {#check-the-operations-dashboard-security-health-checks}

AEM 6 introduce il nuovo modulo di analisi delle operazioni, volto ad aiutare gli operatori del sistema a risolvere i problemi e a monitorare lo stato di un&#39;istanza.

Il dashboard include anche una raccolta di controlli di stato di sicurezza. Si consiglia di controllare lo stato di tutti i controlli di stato di protezione prima di iniziare a vivere con l&#39;istanza di produzione. Per ulteriori informazioni, consultare la [documentazione del dashboard operativo](/help/sites-administering/operations-dashboard.md).

### Controllare se il contenuto di esempio è presente {#check-if-example-content-is-present}

Tutti i contenuti e gli utenti di esempio (ad esempio il progetto di Geometrixx e i relativi componenti) devono essere disinstallati ed eliminati completamente in un sistema produttivo prima di renderlo accessibile al pubblico.

>[!NOTE]
>
>Le applicazioni We.Retail di esempio vengono rimosse se l&#39;istanza è in esecuzione in [Modalità pronta per la produzione](/help/sites-administering/production-ready.md). Se, per qualsiasi motivo, non è così, potete disinstallare il contenuto di esempio andando a Gestione pacchetti, quindi cercando e disinstallando tutti i pacchetti We.Retail. Per ulteriori informazioni, vedere [Operazioni con i pacchetti](package-manager.md).

### Verificate la presenza dei bundle di sviluppo CRX {#check-if-the-crx-development-bundles-are-present}

I bundle OSGi di sviluppo devono essere disinstallati sia nei sistemi produttivi di creazione che di pubblicazione prima di renderli accessibili.

*  supporto CRXDE Adobe (com.adobe.granite.crxde-support)
*  Adobe Granite CRX Explorer (com.adobe.granite.crx-explorer)
*  Adobe Granite CRXDE Lite (com.adobe.granite.crxde-lite)

### Verificare la presenza del bundle di sviluppo Sling {#check-if-the-sling-development-bundle-is-present}

Gli [AEM Developer Tools for Eclipse](/help/sites-developing/aem-eclipse.md) distribuiscono l&#39;installazione del supporto Apache Sling Tooling (org.apache.sling.tooling.support.install).

Prima di renderli accessibili, questo bundle OSGi deve essere disinstallato nei sistemi produttivi di creazione e pubblicazione.

### Protect contro la contraffazione delle richieste tra siti {#protect-against-cross-site-request-forgery}

#### Quadro di protezione CSRF {#the-csrf-protection-framework}

AEM 6.1 viene fornito con un meccanismo che aiuta a proteggere contro gli attacchi di contraffazione delle richieste cross-site, denominato **CSRF Protection Framework**. Per ulteriori informazioni su come utilizzarlo, consultare la [documentazione](/help/sites-developing/csrf-protection.md).

#### Filtro Sling Referrer {#the-sling-referrer-filter}

Per risolvere problemi noti di sicurezza con CSRF (Cross-Site Request Forgery) in CRX WebDAV e Apache Sling, è necessario aggiungere configurazioni per il filtro Referrer per utilizzarlo.

Il servizio filtro di riferimento è un servizio OSGi che consente di configurare:

* quali metodi http devono essere filtrati
* se è consentita un&#39;intestazione di referente vuota
* e un elenco di server da consentire oltre all&#39;host del server.

   Per impostazione predefinita, tutte le varianti di localhost e i nomi host correnti che il server è associato sono nell&#39;elenco.

Per configurare il servizio filtro di riferimento:

1. Aprite la console Apache Felix (**Configurations**) all&#39;indirizzo:

   `https://<server>:<port_number>/system/console/configMgr`

1. Effettuate l&#39;accesso come `admin`.
1. Nel menu **Configurazioni**, selezionare:

   `Apache Sling Referrer Filter`

1. Nel campo `Allow Hosts`, immettere tutti gli host consentiti come referente. Ogni voce deve essere del modulo

   &lt;protocol>://&lt;server>:&lt;port>

   Esempio:

   * `https://allowed.server:80` consente tutte le richieste da questo server con la porta specificata.
   * Se desiderate anche consentire le richieste https, dovete immettere una seconda riga.
   * Se consentite tutte le porte da tale server, potete utilizzare `0` come numero di porta.

1. Controllare il campo `Allow Empty` se si desidera consentire intestazioni referrer vuote o mancanti.

   >[!CAUTION]
   >
   >Si consiglia di fornire un referente durante l&#39;utilizzo di strumenti della riga di comando come `cURL` invece di consentire un valore vuoto in quanto potrebbe esporre il sistema agli attacchi CSRF.

1. Modificate i metodi che questo filtro deve utilizzare per i controlli con il campo `Filter Methods`.

1. Fare clic su **Salva** per salvare le modifiche.

### Impostazioni OSGI {#osgi-settings}

Alcune impostazioni OSGI sono impostate per impostazione predefinita per consentire un debug più semplice dell’applicazione. Per evitare che le informazioni interne vengano divulgate al pubblico, è necessario modificare le istanze produttive di pubblicazione e creazione.

>[!NOTE]
>
>Tutte le seguenti impostazioni, ad eccezione di **Il giorno CQ WCM Debug Filter** vengono automaticamente coperte dalla [Modalità pronta per la produzione](/help/sites-administering/production-ready.md). Per questo motivo, consigliamo di rivedere tutte le impostazioni prima di distribuire l&#39;istanza in un ambiente produttivo.

Per ciascuno dei seguenti servizi è necessario modificare le impostazioni specificate:

* [ Adobe Granite HTML Library Manager](/help/sites-deploying/osgi-configuration-settings.md#day-cq-html-library-manager):

   * abilitare **Minify** (per rimuovere CRLF e spazi bianchi).
   * abilitare **Gzip** (per consentire lo scorrimento e l&#39;accesso ai file con una sola richiesta).
   * disable **Debug**
   * disattiva **Timing**

* [Filtro](/help/sites-deploying/osgi-configuration-settings.md#day-cq-wcm-debug-filter) debug CQ WCM Day:

   * deselezionare **Abilita**

* [Filtro](/help/sites-deploying/osgi-configuration-settings.md) WCM CQ Day:

   * solo per la pubblicazione, impostare la modalità **WCM** su &quot;disabled&quot;

* [Gestore](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-javascript-handler) Java Script Apache Sling:

   * disabilitare **Generate Debug Info**

* [Gestore](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-jsp-script-handler) script JSP Apache Sling:

   * disabilitare **Generate Debug Info**
   * disattiva **Contenuto mappato**

Per ulteriori dettagli, vedere [Impostazioni di configurazione OSGi](/help/sites-deploying/osgi-configuration-settings.md).

Quando lavorate con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; per ulteriori informazioni e procedure consigliate, vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md).

## Ulteriori letture {#further-readings}

### Riduzione degli attacchi Denial of Service (DoS) {#mitigate-denial-of-service-dos-attacks}

Un attacco Denial of Service (DoS) è un tentativo di rendere una risorsa computer non disponibile agli utenti previsti. Questo avviene spesso sovraccaricando la risorsa; ad esempio:

* Con un&#39;ondata di richieste da una fonte esterna.
* Con una richiesta di maggiori informazioni, il sistema è in grado di fornire con successo.

   Ad esempio, una rappresentazione JSON dell’intero repository.

* Richiedendo una pagina di contenuto con un numero illimitato di URL, l&#39;URL può includere un handle, alcuni selettori, un&#39;estensione e un suffisso, ciascuno dei quali può essere modificato.

   Ad esempio, `.../en.html` può essere richiesto anche come:

   * `.../en.ExtensionDosAttack`
   * `.../en.SelectorDosAttack.html`
   * `.../en.html/SuffixDosAttack`

   Tutte le varianti valide (ad esempio, restituire una risposta `200` e configurate per la memorizzazione nella cache) verranno memorizzate nella cache dal dispatcher, portando alla fine a un file system completo e a nessun servizio per ulteriori richieste.

Ci sono molti punti di configurazione per prevenire tali attacchi, qui discutiamo solo di quelli direttamente collegati a AEM.

**Configurazione di Sling per impedire il DoS**

Sling è *incentrato sul contenuto*. Ciò significa che l&#39;elaborazione è incentrata sul contenuto, in quanto ogni richiesta (HTTP) viene mappata sul contenuto sotto forma di risorsa JCR (un nodo del repository):

* La prima destinazione è la risorsa (nodo JCR) che contiene il contenuto.
* In secondo luogo, il renderer, o script, si trova dalle proprietà delle risorse in combinazione con alcune parti della richiesta (ad es. selettori e/o estensione).

>[!NOTE]
>
>Questo argomento viene trattato più dettagliatamente in [Sling Request Processing](/help/sites-developing/the-basics.md#sling-request-processing).

Questo approccio rende Sling molto potente e molto flessibile, ma come sempre è la flessibilità che deve essere gestita con attenzione.

Per evitare l&#39;uso improprio dei DoS è possibile:

1. incorporare controlli a livello di applicazione; a causa del numero di variazioni possibili, una configurazione predefinita non è fattibile.

   Nell’applicazione è necessario:

   * Controllare i selettori nell&#39;applicazione, in modo che *only* servano i selettori espliciti necessari e restituiscano `404` per tutti gli altri.
   * Impedire l&#39;output di un numero illimitato di nodi di contenuto.

1. Controllare la configurazione dei renderer predefiniti, che possono essere un&#39;area problematica.

   * In particolare, il renderer JSON che può trasmettere la struttura ad albero su più livelli.

      Ad esempio, la richiesta:

      `http://localhost:4502/.json`

      potrebbe scaricare l&#39;intero repository in una rappresentazione JSON. Ciò causerebbe gravi problemi al server. Per questo motivo Sling imposta un limite al numero massimo di risultati. Per limitare la profondità del rendering JSON potete impostare il valore per:

      **JSON Max result** (  `json.maximumresults`)

      nella configurazione per il servlet [Apache Sling GET](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet). Quando questo limite viene superato, il rendering viene compresso. Il valore predefinito per Sling within AEM è `200`.

   * Come misura preventiva, disattivate gli altri renderer predefiniti (HTML, testo normale, XML). Di nuovo, configurando il servlet [Apache Sling GET](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet).
   >[!CAUTION]
   >
   >Non disattivate il renderer JSON. Questo è richiesto per il normale funzionamento di AEM.

1. Usate un firewall per filtrare l’accesso all’istanza.

   * L&#39;uso di un firewall a livello di sistema operativo è necessario per filtrare l&#39;accesso ai punti dell&#39;istanza che potrebbero causare attacchi di tipo Denial of Service se lasciato non protetto.

**Ottimizzazione rispetto a DoS causata dall&#39;utilizzo dei selettori del modulo**

>[!NOTE]
>
>Questa limitazione deve essere eseguita solo in ambienti AEM che non utilizzano Forms.

Poiché AEM non fornisce indici out-of-the box per la `FormChooserServlet`, l&#39;utilizzo di selettori di moduli nelle query attiverà un lungo attraversamento del repository, in genere bloccando l&#39;istanza AEM. I selettori dei moduli possono essere rilevati dalla presenza del modulo **&amp;ast;.form.&amp;ast;** stringa nelle query.

Per attenuare questo problema, attenetevi alla procedura seguente:

1. Andate alla console Web puntando il browser su *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*

1. Cerca **Giorno CQ WCM Form Chooser Servlet**
1. Dopo aver fatto clic sulla voce, disattivate la **Ricerca avanzata richiesta** nella finestra seguente.

1. Fai clic su **Salva**.

**Mitigare contro i DoS causati dal servlet di download delle risorse**

Il servlet di download delle risorse predefinito AEM consente agli utenti autenticati di emettere richieste di download simultanee di grandi dimensioni per la creazione di file ZIP di risorse visibili agli utenti che possono sovraccaricare il server e/o la rete.

Per attenuare i potenziali rischi DoS causati da questa funzione, il componente `AssetDownloadServlet` OSGi è disabilitato per impostazione predefinita per le istanze di pubblicazione nelle versioni AEM più recenti.

Se la configurazione richiede l’attivazione del server di download delle risorse, consultate [questo articolo](/help/assets/download-assets-from-aem.md) per ulteriori informazioni.

### Disattiva WebDAV {#disable-webdav}

WebDAV deve essere disattivato sia negli ambienti di creazione che di pubblicazione. A tale scopo, potete arrestare i bundle OSGi appropriati.

1. Connettiti alla **console di gestione Flash** in esecuzione su:

   `https://<*host*>:<*port*>/system/console`

   Esempio `http://localhost:4503/system/console/bundles`.

1. Nell’elenco dei bundle, individua il bundle denominato:

   `Apache Sling Simple WebDAV Access to repositories (org.apache.sling.jcr.webdav)`

1. Fate clic sul pulsante Interrompi (nella colonna Azioni) per arrestare il bundle.

1. Di nuovo nell&#39;elenco dei bundle, trovate il bundle denominato:

   `Apache Sling DavEx Access to repositories (org.apache.sling.jcr.davex)`

1. Fate clic sul pulsante Interrompi per arrestare il bundle.

   >[!NOTE]
   >
   >Non è necessario riavviare il AEM.

### Verifica Di Non Essere In Grado Di Rivelare Informazioni Personalmente Identificabili Nel Percorso Home Degli Utenti {#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path}

È importante proteggere gli utenti accertandosi di non esporre alcuna informazione personale nel percorso principale degli utenti del repository.

A partire da AEM 6.1, il modo in cui vengono memorizzati i nomi dei nodi ID dell&#39;utente (denominati anche autorizzabili) viene modificato con una nuova implementazione dell&#39;interfaccia `AuthorizableNodeName`. La nuova interfaccia non esporrà più l&#39;ID utente nel nome del nodo, ma genererà un nome casuale.

Per abilitarlo, non è necessario eseguire alcuna configurazione, in quanto si tratta del metodo predefinito per generare ID autorizzabili in AEM.

Anche se non consigliato, potete disattivarlo nel caso in cui sia necessaria la vecchia implementazione per garantire la compatibilità con le applicazioni esistenti. A tale scopo, è necessario:

1. Andate alla console Web e rimuovete la voce** org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName** dalla proprietà **RequiredServicePids** in **Apache Jackrabbit Oak SecurityProvider**.

   È inoltre possibile trovare il provider di sicurezza Oak cercando il PID **org.apache.jackrabbit.oak.security.internal.SecurityProviderRegistration** nelle configurazioni OSGi.

1. Eliminate dalla console Web la configurazione **Apache Jackrabbit Oak Random Authorizable Node Name** OSGi.

   Per una ricerca più semplice, il PID di questa configurazione è **org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**.

>[!NOTE]
>
>Per ulteriori informazioni, consultare la documentazione Oak in [Authorizable Node Name Generation](https://jackrabbit.apache.org/oak/docs/security/user/authorizablenodename.html).

### Impedisci il clickjacking {#prevent-clickjacking}

Per evitare il clickjacking, si consiglia di configurare il server Web in modo che fornisca l&#39;intestazione HTTP `X-FRAME-OPTIONS` impostata su `SAMEORIGIN`.

Per ulteriori [informazioni sul clickjacking, vedere il sito OWASP](https://www.owasp.org/index.php/Clickjacking).

### Verificare Di Replicare Correttamente Le Chiavi Di Cifratura Quando Necessario {#make-sure-you-properly-replicate-encryption-keys-when-needed}

Alcune funzioni AEM e schemi di autenticazione richiedono la replica delle chiavi di crittografia in tutte AEM istanze.

Prima di eseguire questa operazione, tenere presente che la replica chiave viene eseguita in modo diverso tra le versioni, perché il modo in cui le chiavi vengono memorizzate è diverso tra la versione 6.3 e le versioni precedenti.

Per ulteriori informazioni, vedi sotto.

#### Tasti di replica per AEM 6.3 {#replicating-keys-for-aem}

Nelle versioni precedenti le chiavi di replica venivano memorizzate nella directory archivio, a partire da AEM 6.3 vengono memorizzate nel file system.

Pertanto, per replicare le chiavi tra le istanze è necessario copiarle dall&#39;istanza di origine alla posizione delle istanze di destinazione nel file system.

Più specificamente, è necessario:

1. accedere all&#39;istanza AEM, in genere un&#39;istanza di creazione, che contiene il materiale chiave da copiare;
1. Individuate il bundle com.adobe.granite.crypto.file nel file system locale. Ad esempio, in questo percorso:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`

   Il file `bundle.info` all&#39;interno di ciascuna cartella identificherà il nome del bundle.

1. Passa alla cartella dei dati. Esempio:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Copiate i file HMAC e master.
1. Quindi, passate all&#39;istanza di destinazione alla quale desiderate duplicare la chiave HMAC e individuate la cartella di dati. Esempio:

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Incollate i due file precedentemente copiati.
1. [Aggiornate Crypto ](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) Bundlese l&#39;istanza di destinazione è già in esecuzione.
1. Ripetere i passaggi indicati sopra per tutte le istanze in cui si desidera replicare la chiave.

>[!NOTE]
>
>È possibile ripristinare il metodo pre 6.3 di memorizzazione delle chiavi aggiungendo il parametro seguente al primo AEM di installazione:
>
>`-Dcom.adobe.granite.crypto.file.disable=true`

#### Tasti di replica per AEM 6.2 e versioni precedenti {#replicating-keys-for-aem-and-older-versions}

Nelle versioni AEM 6.2 e precedenti, le chiavi sono memorizzate nella directory archivio sotto il nodo `/etc/key`.

Il modo consigliato per replicare in modo sicuro le chiavi nelle istanze consiste solo nel replicare questo nodo. È possibile replicare in modo selettivo i nodi tramite CRXDE Lite:

1. Aprire il CRXDE Lite andando su *https://&lt;serveraddress>:4502/crx/de/index.jsp*
1. Selezionare il nodo `/etc/key`.
1. Fare clic sulla scheda **Replica**.
1. Premere il tasto **Replica**.

### Eseguire un test di penetrazione {#perform-a-penetration-test}

 Adobe consiglia vivamente di eseguire un test di penetrazione dell&#39;infrastruttura AEM prima di continuare la produzione.

### Tecniche consigliate per lo sviluppo {#development-best-practices}

È fondamentale che i nuovi sviluppi seguano le [Best practice di sicurezza](/help/sites-developing/security.md) per garantire che l&#39;ambiente AEM rimanga al sicuro.
