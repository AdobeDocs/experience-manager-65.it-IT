---
title: Lista di controllo sicurezza
seo-title: Security Checklist
description: Scopri le varie considerazioni sulla sicurezza durante la configurazione e la distribuzione di AEM.
seo-description: Learn about the various security considerations when configuring and deploying AEM.
uuid: 8e293316-4177-4271-87c6-9dc1a2e85a07
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: de7d7209-c194-4d19-853b-468ebf3fa4b2
docset: aem65
exl-id: 314a6409-398c-470b-8799-0c4e6f745141
feature: Security
source-git-commit: f60d3049b10a8ec500dd0cd4b1b5d4efbe415d84
workflow-type: tm+mt
source-wordcount: '2859'
ht-degree: 3%

---

# Lista di controllo sicurezza {#security-checklist}

Questa sezione descrive vari passaggi da seguire per garantire che l’installazione AEM sia sicura quando distribuita. La lista di controllo deve essere applicata dall’alto verso il basso.

>[!NOTE]
>
>Sono inoltre disponibili ulteriori informazioni sulle minacce per la sicurezza più pericolose pubblicate da [Open Web Application Security Project (OWASP)](https://owasp.org/www-project-top-ten/).

>[!NOTE]
>
>Nella fase di sviluppo sono disponibili alcune [considerazioni sulla sicurezza](/help/sites-developing/dev-guidelines-bestpractices.md#security-considerations) aggiuntive.

## Principali misure di sicurezza {#main-security-measures}

### Eseguire AEM in modalità pronta per la produzione {#run-aem-in-production-ready-mode}

Per ulteriori informazioni, consulta [Esecuzione AEM in modalità pronta per la produzione](/help/sites-administering/production-ready.md).

### Abilita HTTPS per la sicurezza del livello di trasporto {#enable-https-for-transport-layer-security}

Per disporre di un’istanza sicura, è obbligatorio abilitare il livello di trasporto HTTPS sia sulle istanze di authoring che di pubblicazione.

>[!NOTE]
>
>Per ulteriori informazioni, consulta la sezione [Abilitazione di HTTP su SSL](/help/sites-administering/ssl-by-default.md) .

### Installare gli hotfix di sicurezza {#install-security-hotfixes}

Assicurati di aver installato gli [Hotfix di sicurezza più recenti forniti da Adobe](https://helpx.adobe.com/it/experience-manager/kb/aem63-available-hotfixes.html).

### Modificare le password predefinite per gli account di amministrazione della console AEM e OSGi {#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts}

L&#39;Adobe consiglia vivamente di modificare dopo l&#39;installazione la password per gli account [**AEM** `admin`](#changing-the-aem-admin-password) con privilegi (su tutte le istanze).

Tali account includono:

* L&#39;account AEM `admin`

   Dopo aver cambiato la password per l&#39;account amministratore AEM, dovrai usare la nuova password quando accedi a CRX.

* Password `admin` per la console Web OSGi

   Questa modifica verrà applicata anche all’account amministratore utilizzato per accedere alla console Web, quindi dovrai usare la stessa password per accedervi.

Questi due account utilizzano credenziali separate e dispongono di una password distinta e sicura per ciascuno di essi è fondamentale per una distribuzione sicura.

#### Modifica della password dell&#39;amministratore AEM {#changing-the-aem-admin-password}

La password per l&#39;account amministratore AEM può essere modificata tramite la console [Operazioni Granite - Utenti](/help/sites-administering/granite-user-group-admin.md) .

Qui puoi modificare l&#39;account `admin` e [modificare la password](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user).

>[!NOTE]
>
>La modifica dell’account amministratore comporta anche la modifica dell’account della console Web OSGi. Dopo aver cambiato l&#39;account amministratore, devi quindi cambiare l&#39;account OSGi in qualcosa di diverso.

#### Importanza della modifica della password della console Web OSGi {#importance-of-changing-the-osgi-web-console-password}

Oltre all&#39;account AEM `admin`, la mancata modifica della password predefinita per la console Web OSGi può portare a:

* Esposizione del server con una password predefinita durante l&#39;avvio e lo spegnimento (che può richiedere minuti per i server di grandi dimensioni);
* Esposizione del server quando l&#39;archivio è inattivo/riavvio del bundle - e OSGI è in esecuzione.

Per ulteriori informazioni sulla modifica della password della console Web, consulta [Modifica della password dell’amministratore della console Web OSGi](/help/sites-administering/security-checklist.md#changing-the-osgi-web-console-admin-password) di seguito.

#### Modifica della password dell’amministratore della console Web OSGi {#changing-the-osgi-web-console-admin-password}

È inoltre necessario modificare la password utilizzata per accedere alla console Web. A questo scopo, configura le seguenti proprietà della [Console di gestione Apache Felix OSGi](/help/sites-deploying/osgi-configuration-settings.md):

**Nome utente** e  **password**, le credenziali per l&#39;accesso alla console di gestione Web Apache Felix stessa.
La password deve essere modificata dopo l’installazione iniziale per garantire la sicurezza dell’istanza.

Per effettuare questo collegamento:

1. Passa alla console Web all’indirizzo `<server>:<port>/system/console/configMgr`.
1. Passa a **Apache Felix OSGi Management Console** e modifica il **nome utente** e la **password**.

   ![chlimage_1-3](assets/chlimage_1-3.png)

1. Fai clic su **Salva**.

### Implementare un gestore di errori personalizzato {#implement-custom-error-handler}

Adobe consiglia di definire pagine personalizzate del gestore di errori, in particolare per i codici di risposta HTTP 404 e 500, al fine di impedire la divulgazione delle informazioni.

>[!NOTE]
>
>Per ulteriori informazioni, consulta l&#39;articolo della knowledge base [Come creare script personalizzati o gestori di errori](https://helpx.adobe.com/experience-manager/kb/CustomErrorHandling.html) .

### Elenco di controllo completo della sicurezza del dispatcher {#complete-dispatcher-security-checklist}

AEM Dispatcher è un elemento critico dell’infrastruttura. L&#39;Adobe consiglia vivamente di completare la [lista di controllo della sicurezza del dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/security-checklist.html?lang=it#getting-started).

>[!CAUTION]
>
>Utilizzando Dispatcher è necessario disabilitare il selettore &quot;.form&quot;.

## Passaggi di verifica {#verification-steps}

### Configurare gli utenti di replica e trasporto {#configure-replication-and-transport-users}

Un&#39;installazione standard di AEM specifica `admin` come utente per le credenziali di trasporto all&#39;interno dei [agenti di replica](/help/sites-deploying/replication.md) predefiniti. Inoltre, l&#39;utente amministratore viene utilizzato per avviare la replica sul sistema di authoring.

Per motivi di sicurezza, è opportuno modificare entrambe le opzioni per riflettere il caso d’uso specifico in questione, tenendo presenti i due aspetti seguenti:

* L&#39; **utente di trasporto** non deve essere l&#39;utente amministratore. Piuttosto, imposta un utente sul sistema di pubblicazione che dispone solo dei diritti di accesso alle parti rilevanti del sistema di pubblicazione e utilizza le credenziali dell&#39;utente per il trasporto.

   Puoi iniziare dall&#39;utente destinatario della replica in bundle e configurare i diritti di accesso di questo utente in modo che corrispondano alla tua situazione

* Anche l&#39; **utente di replica** o **ID utente agente** non deve essere l&#39;utente amministratore, ma un utente che può visualizzare solo il contenuto che deve essere replicato. L’utente di replica viene utilizzato per raccogliere il contenuto da replicare sul sistema dell’autore prima che venga inviato all’editore.

### Controlla i controlli di stato della sicurezza del dashboard delle operazioni {#check-the-operations-dashboard-security-health-checks}

AEM 6 introduce il nuovo dashboard delle operazioni, volto ad aiutare gli operatori del sistema a risolvere i problemi e monitorare lo stato di un&#39;istanza.

Il dashboard viene fornito anche con una raccolta di controlli di integrità della sicurezza. È consigliabile controllare lo stato di tutti i controlli di integrità della sicurezza prima di iniziare a lavorare con l&#39;istanza di produzione. Per ulteriori informazioni, consulta la [documentazione del dashboard delle operazioni](/help/sites-administering/operations-dashboard.md).

### Controlla se il contenuto di esempio è presente {#check-if-example-content-is-present}

Tutti i contenuti e gli utenti di esempio (ad esempio il progetto Geometrixx e i relativi componenti) devono essere disinstallati ed eliminati completamente in un sistema produttivo prima di renderlo accessibile al pubblico.

>[!NOTE]
>
>Le applicazioni We.Retail di esempio vengono rimosse se questa istanza è in esecuzione in [Modalità pronta per la produzione](/help/sites-administering/production-ready.md). Se, per qualsiasi motivo, non è il caso, è possibile disinstallare il contenuto di esempio andando a Gestione pacchetti, quindi cercando e disinstallando tutti i pacchetti We.Retail. Per ulteriori informazioni, consulta [Utilizzare i pacchetti](package-manager.md).

### Controlla se i bundle di sviluppo CRX sono presenti {#check-if-the-crx-development-bundles-are-present}

Questi bundle OSGi di sviluppo devono essere disinstallati sia sui sistemi produttivi di authoring che di pubblicazione prima di renderli accessibili.

* Supporto Adobe CRXDE (com.adobe.granite.crxde-support)
* Adobe Granite CRX Explorer (com.adobe.granite.crx-explorer)
* Adobe Granite CRXDE Lite (com.adobe.granite.crxde-lite)

### Controlla se il bundle di sviluppo Sling è presente {#check-if-the-sling-development-bundle-is-present}

Il [AEM Developer Tools per Eclipse](/help/sites-developing/aem-eclipse.md) implementa l&#39;installazione del supporto per gli strumenti Sling di Apache (org.apache.sling.tooling.support.install).

Questo bundle OSGi deve essere disinstallato sui sistemi produttivi di authoring e pubblicazione prima di renderli accessibili.

### Protect contro la falsificazione delle richieste intersito {#protect-against-cross-site-request-forgery}

#### Quadro di riferimento per la protezione del CSRF {#the-csrf-protection-framework}

AEM 6.1 viene fornito con un meccanismo che aiuta a proteggere dagli attacchi Cross-Site Request Forgery, denominato **CSRF Protection Framework**. Per ulteriori informazioni su come usarlo, consulta la [documentazione](/help/sites-developing/csrf-protection.md).

#### Filtro Sling Referrer {#the-sling-referrer-filter}

Per risolvere problemi di sicurezza noti con Cross-Site Request Forgery (CSRF) in CRX WebDAV e Apache Sling è necessario aggiungere configurazioni per il filtro Referrer per utilizzarlo.

Il servizio filtro referrer è un servizio OSGi che consente di configurare:

* quali metodi http devono essere filtrati
* se è consentita un&#39;intestazione referrer vuota
* e un elenco di server da consentire oltre all&#39;host del server.

   Per impostazione predefinita, nell’elenco sono presenti tutte le varianti di localhost e i nomi host correnti a cui è associato il server.

Per configurare il servizio filtro referrer:

1. Apri la console Apache Felix (**Configurazioni**) all&#39;indirizzo:

   `https://<server>:<port_number>/system/console/configMgr`

1. Accedi come `admin`.
1. Nel menu **Configurazioni**, seleziona:

   `Apache Sling Referrer Filter`

1. Nel campo `Allow Hosts` , immetti tutti gli host consentiti come referrer. Ogni voce deve essere del modulo

   &lt;protocol>://&lt;server>:&lt;port>

   Esempio:

   * `https://allowed.server:80` consente tutte le richieste da questo server con la porta specificata.
   * Se desideri anche consentire le richieste https, devi immettere una seconda riga.
   * Se consenti tutte le porte da quel server, puoi utilizzare `0` come numero di porta.

1. Seleziona il campo `Allow Empty` per consentire intestazioni di referente vuote o mancanti.

   >[!CAUTION]
   >
   >Si consiglia di fornire un referente quando si utilizzano strumenti della riga di comando come `cURL` invece di consentire un valore vuoto, in quanto potrebbe esporre il sistema ad attacchi CSRF.

1. Modifica i metodi che questo filtro deve utilizzare per i controlli con il campo `Filter Methods` .

1. Fai clic su **Salva** per salvare le modifiche.

### Impostazioni OSGI {#osgi-settings}

Alcune impostazioni OSGI sono impostate per impostazione predefinita per consentire un debug più semplice dell&#39;applicazione. Queste devono essere modificate nelle istanze produttive di pubblicazione e authoring per evitare che le informazioni interne vengano divulgate al pubblico.

>[!NOTE]
>
>Tutte le impostazioni seguenti, ad eccezione di **Day CQ WCM Debug Filter**, sono automaticamente coperte dalla [Modalità pronta per la produzione](/help/sites-administering/production-ready.md). Per questo motivo, consigliamo di rivedere tutte le impostazioni prima di distribuire l’istanza in un ambiente produttivo.

Per ciascuno dei servizi seguenti è necessario modificare le impostazioni specificate:

* [Adobe Granite HTML Library Manager](/help/sites-deploying/osgi-configuration-settings.md#day-cq-html-library-manager):

   * abilita **Minify** (per rimuovere CRLF e caratteri di spazio vuoto).
   * abilita **Gzip** (per consentire l&#39;gzip dei file e l&#39;accesso con una richiesta).
   * disattiva **Debug**
   * disattiva **Timing**

* [Filtro](/help/sites-deploying/osgi-configuration-settings.md#day-cq-wcm-debug-filter) di debug Day CQ WCM:

   * deseleziona **Abilita**

* [Filtro](/help/sites-deploying/osgi-configuration-settings.md) WCM Day CQ:

   * solo per la pubblicazione, imposta **Modalità WCM** su &quot;disabilitata&quot;

* [Gestore](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-javascript-handler) Java Script Apache Sling:

   * disattiva **Genera informazioni di debug**

* [Gestore](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-jsp-script-handler) script JSP Apache Sling:

   * disattiva **Genera informazioni di debug**
   * disattiva **Contenuto mappato**

Per ulteriori dettagli, consulta [Impostazioni di configurazione OSGi](/help/sites-deploying/osgi-configuration-settings.md).

Quando si lavora con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; per ulteriori dettagli e pratiche consigliate, consulta [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) .

## Ulteriori letture {#further-readings}

### Riduzione degli attacchi di tipo DoS (Denial of Service) {#mitigate-denial-of-service-dos-attacks}

Un attacco Denial of Service (DoS) è un tentativo di rendere la risorsa di un computer indisponibile per gli utenti a cui è destinata. Questo viene spesso fatto sovraccaricando la risorsa; ad esempio:

* Con un flusso di richieste da una fonte esterna.
* Con una richiesta di più informazioni di quelle che il sistema può consegnare correttamente.

   Ad esempio, una rappresentazione JSON dell’intero archivio.

* Richiedendo una pagina di contenuto con un numero illimitato di URL, l’URL può includere un handle, alcuni selettori, un’estensione e un suffisso, ciascuno dei quali può essere modificato.

   Ad esempio, `.../en.html` può essere richiesto anche come:

   * `.../en.ExtensionDosAttack`
   * `.../en.SelectorDosAttack.html`
   * `.../en.html/SuffixDosAttack`

   Tutte le varianti valide (ad esempio, restituire una risposta `200` e sono configurate per la memorizzazione nella cache) verranno memorizzate nella cache dal dispatcher, in modo da ottenere un file system completo e nessun servizio per ulteriori richieste.

Ci sono molti punti di configurazione per prevenire tali attacchi, qui discutiamo solo di quelli direttamente collegati a AEM.

**Configurazione di Sling per impedire il DoS**

Sling è *incentrato sul contenuto*. Ciò significa che l’elaborazione è incentrata sul contenuto, in quanto ogni richiesta (HTTP) viene mappata sul contenuto sotto forma di una risorsa JCR (un nodo di archivio):

* Il primo target è la risorsa (nodo JCR) che contiene il contenuto.
* In secondo luogo, il renderer, o script, si trova dalle proprietà della risorsa in combinazione con alcune parti della richiesta (ad esempio selettori e/o estensione).

>[!NOTE]
>
>Questa sezione viene descritta più dettagliatamente in [Elaborazione delle richieste Sling](/help/sites-developing/the-basics.md#sling-request-processing).

Questo approccio rende Sling molto potente e molto flessibile, ma come sempre è la flessibilità che deve essere gestita con attenzione.

Per evitare l&#39;uso improprio di DoS è possibile:

1. Incorporare controlli a livello di applicazione; a causa del numero di varianti possibili, una configurazione predefinita non è fattibile.

   Nella tua applicazione devi:

   * Controlla i selettori nell&#39;applicazione, in modo che *solo* serva i selettori espliciti necessari e restituisca `404` per tutti gli altri.
   * Impedisci l’output di un numero illimitato di nodi di contenuto.

1. Controlla la configurazione dei moduli di rendering predefiniti, che possono essere un’area problematica.

   * In particolare, il modulo di rendering JSON che può trasmettere la struttura ad albero su più livelli.

      Ad esempio, la richiesta:

      `http://localhost:4502/.json`

      potrebbe scaricare l’intero archivio in una rappresentazione JSON. Questo causerebbe gravi problemi al server. Per questo motivo Sling imposta un limite al numero di risultati massimi. Per limitare la profondità del rendering JSON, puoi impostare il valore per:

      **Risultati massimi JSON** (  `json.maximumresults`)

      nella configurazione del [Servlet Apache Sling GET](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet). Quando questo limite viene superato, il rendering viene compresso. Il valore predefinito per Sling in AEM è `1000`.

   * Come misura preventiva, disattiva gli altri render predefiniti (HTML, testo normale, XML). Di nuovo configurando il [Servlet Apache Sling GET](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet).
   >[!CAUTION]
   >
   >Non disabilitare il renderer JSON, è necessario per il normale funzionamento di AEM.

1. Utilizza un firewall per filtrare l’accesso all’istanza.

   * L&#39;utilizzo di un firewall a livello di sistema operativo è necessario per filtrare l&#39;accesso ai punti dell&#39;istanza che potrebbero causare attacchi di tipo Denial of Service se lasciato non protetto.

**Riduzione degli errori di DoS causati dall’utilizzo di selettori di moduli**

>[!NOTE]
>
>Questa mitigazione deve essere eseguita solo su ambienti AEM che non utilizzano Forms.

Poiché AEM non fornisce indici predefiniti per il `FormChooserServlet`, l’utilizzo di selettori di moduli nelle query innescherà un costoso attraversamento dell’archivio, solitamente bloccando l’istanza AEM. I selettori dei moduli possono essere rilevati dalla presenza di **&amp;ast;.form.Stringa &amp;ast;** nelle query.

Per attenuarlo, segui i passaggi seguenti:

1. Vai alla console Web puntando il browser su *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*

1. Cerca **Day CQ WCM Form Chooser Servlet**
1. Dopo aver fatto clic sulla voce, disattiva la **Richiesta di ricerca avanzata** nella finestra seguente.

1. Fai clic su **Salva**.

**Riduzione del numero di DoS causato dal servlet di download delle risorse**

Il servlet di download delle risorse predefinito consente agli utenti autenticati di emettere richieste di download simultanee di grandi dimensioni arbitrarie per creare file ZIP di risorse. La creazione di grandi archivi ZIP può sovraccaricare il server e la rete. Per attenuare un potenziale rischio di Denial of Service (DoS) causato da questo comportamento, il componente `AssetDownloadServlet` OSGi è disabilitato per impostazione predefinita nell&#39;istanza di pubblicazione [!DNL Experience Manager]. Per impostazione predefinita è abilitata nell’istanza di authoring [!DNL Experience Manager] .

Se non hai bisogno della funzionalità di download, disattiva il servlet nelle distribuzioni di authoring e pubblicazione. Se la configurazione richiede che la funzionalità di download delle risorse sia abilitata, consulta [questo articolo](/help/assets/download-assets-from-aem.md) per ulteriori informazioni. Inoltre, puoi definire un limite massimo di download supportato dalla distribuzione.

### Disattiva WebDAV {#disable-webdav}

WebDAV deve essere disabilitato sia negli ambienti di authoring che di pubblicazione. Questo può essere fatto arrestando i bundle OSGi appropriati.

1. Connettiti alla **Felix Management Console** in esecuzione su:

   `https://<*host*>:<*port*>/system/console`

   Esempio `http://localhost:4503/system/console/bundles`.

1. Nell’elenco dei bundle, trova il bundle denominato:

   `Apache Sling Simple WebDAV Access to repositories (org.apache.sling.jcr.webdav)`

1. Fai clic sul pulsante di arresto (nella colonna Azioni) per arrestare questo bundle.

1. Di nuovo nell&#39;elenco dei bundle, trova il bundle chiamato:

   `Apache Sling DavEx Access to repositories (org.apache.sling.jcr.davex)`

1. Fai clic sul pulsante di arresto per arrestare il bundle.

   >[!NOTE]
   >
   >Non è necessario riavviare AEM.

### Verifica Di Non Divulgare Informazioni Personalmente Identificabili Nel Percorso Home Dell’Utente {#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path}

È importante proteggere gli utenti assicurandosi di non esporre informazioni personali identificabili nel percorso home degli utenti dell’archivio.

A partire da AEM 6.1, il modo in cui vengono memorizzati i nomi dei nodi ID utente (noti anche come autorizzabili) viene modificato con una nuova implementazione dell&#39;interfaccia `AuthorizableNodeName` . La nuova interfaccia non espone più l’ID utente nel nome del nodo, ma genera un nome casuale.

Per abilitarlo, non è necessario eseguire alcuna configurazione, in quanto è ora il modo predefinito per generare ID autorizzabili in AEM.

Anche se non consigliato, puoi disattivarlo nel caso in cui sia necessaria la vecchia implementazione per garantire la compatibilità con le applicazioni esistenti. Per eseguire questa operazione, è necessario:

1. Vai alla Console web e rimuovi la voce** org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName** dalla proprietà **requiredServicePids** in **Apache Jackrabbit Oak SecurityProvider**.

   Puoi anche trovare il provider di sicurezza Oak cercando il PID **org.apache.jackrabbit.oak.security.internal.SecurityProviderRegistration** nelle configurazioni OSGi.

1. Elimina la configurazione **Apache Jackrabbit Oak Random Authorizable Node Name** OSGi dalla Web Console.

   Per una ricerca più semplice, tieni presente che il PID per questa configurazione è **org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**.

>[!NOTE]
>
>Per ulteriori informazioni, consulta la documentazione Oak su [Generazione nome nodo autorizzabile](https://jackrabbit.apache.org/oak/docs/security/user/authorizablenodename.html).

### Previeni il clickjacking {#prevent-clickjacking}

Per prevenire il clickjacking, ti consigliamo di configurare il server web per fornire l’intestazione HTTP `X-FRAME-OPTIONS` impostata su `SAMEORIGIN`.

Per ulteriori [informazioni sul clickjacking, vedi il sito OWASP](https://www.owasp.org/index.php/Clickjacking).

### Assicurati Di Replicare Correttamente Le Chiavi Di Crittografia Quando Necessario {#make-sure-you-properly-replicate-encryption-keys-when-needed}

Alcune funzioni AEM e schemi di autenticazione richiedono la replica delle chiavi di crittografia in tutte le istanze AEM.

Prima di eseguire questa operazione, tieni presente che la replica chiave viene eseguita in modo diverso tra le versioni, perché il modo in cui le chiavi vengono memorizzate è diverso tra le versioni 6.3 e precedenti.

Per ulteriori informazioni, consulta di seguito.

#### Replica delle chiavi per AEM 6.3 {#replicating-keys-for-aem}

Mentre nelle versioni precedenti le chiavi di replica venivano memorizzate nell&#39;archivio, a partire da AEM 6.3 vengono memorizzate nel filesystem.

Pertanto, per replicare le chiavi tra le istanze è necessario copiarle dall&#39;istanza sorgente alla posizione delle istanze di destinazione sul file system.

In particolare, devi:

1. Accedi all&#39;istanza AEM, in genere un&#39;istanza dell&#39;autore, che contiene il materiale chiave da copiare;
1. Individua il bundle com.adobe.granite.crypto.file nel file system locale. Ad esempio, sotto questo percorso:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`

   Il file `bundle.info` all&#39;interno di ogni cartella identificherà il nome del bundle.

1. Passa alla cartella dati. Esempio:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Copiare i file HMAC e master.
1. Quindi, vai all&#39;istanza di destinazione a cui desideri duplicare la chiave HMAC e passa alla cartella dei dati. Esempio:

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Incolla i due file copiati in precedenza.
1. [Aggiorna il Crypto ](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) Bundlese l&#39;istanza di destinazione è già in esecuzione.
1. Ripeti i passaggi precedenti per tutte le istanze a cui desideri replicare la chiave.

>[!NOTE]
>
>Per ripristinare il metodo precedente alla versione 6.3 di memorizzazione delle chiavi, aggiungi il parametro seguente al primo avvio dell&#39;installazione di AEM:
>
>`-Dcom.adobe.granite.crypto.file.disable=true`

#### Replica delle chiavi per le versioni AEM 6.2 e precedenti {#replicating-keys-for-aem-and-older-versions}

Nelle versioni AEM 6.2 e precedenti, le chiavi sono memorizzate nell&#39;archivio sotto il nodo `/etc/key` .

Il modo consigliato per replicare in modo sicuro le chiavi nelle istanze è quello di replicare solo questo nodo. È possibile replicare in modo selettivo i nodi tramite CRXDE Lite:

1. Apri CRXDE Lite andando su *https://&lt;serveraddress>:4502/crx/de/index.jsp*
1. Selezionare il nodo `/etc/key`.
1. Passa alla scheda **Replica** .
1. Premere il tasto **Replica**.

### Esegui un test di penetrazione {#perform-a-penetration-test}

Adobe consiglia vivamente di eseguire un test di penetrazione dell’infrastruttura AEM prima di procedere alla produzione.

### Tecniche consigliate per lo sviluppo {#development-best-practices}

È fondamentale che i nuovi sviluppi seguano le [best practice sulla sicurezza](/help/sites-developing/security.md) per garantire che l&#39;ambiente AEM rimanga sicuro.
