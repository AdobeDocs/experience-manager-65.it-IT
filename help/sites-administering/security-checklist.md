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
source-git-commit: f23adcf200b625e2ab2a766460c41fd7e38fae83
workflow-type: tm+mt
source-wordcount: '2986'
ht-degree: 1%

---

# Lista di controllo sicurezza {#security-checklist}

Questa sezione descrive vari passaggi da seguire per garantire che l’installazione AEM sia sicura quando distribuita. La lista di controllo deve essere applicata dall’alto verso il basso.

>[!NOTE]
>
>Sono inoltre disponibili ulteriori informazioni sulle minacce più pericolose per la sicurezza, pubblicate da [Apri progetto di sicurezza dell&#39;applicazione Web (OWASP)](https://owasp.org/www-project-top-ten/).

>[!NOTE]
>
>Sono disponibili alcuni [considerazioni di sicurezza](/help/sites-developing/dev-guidelines-bestpractices.md#security-considerations) applicabile nella fase di sviluppo.

## Principali misure di sicurezza {#main-security-measures}

### Eseguire AEM in modalità pronta per la produzione {#run-aem-in-production-ready-mode}

Per ulteriori informazioni, consulta [Esecuzione di AEM in modalità pronta per la produzione](/help/sites-administering/production-ready.md).

### Abilita HTTPS per la sicurezza del livello di trasporto {#enable-https-for-transport-layer-security}

Per disporre di un’istanza sicura, è obbligatorio abilitare il livello di trasporto HTTPS sia sulle istanze di authoring che di pubblicazione.

>[!NOTE]
>
>Consulta la sezione [Abilitazione di HTTP su SSL](/help/sites-administering/ssl-by-default.md) per ulteriori informazioni.

### Installare gli hotfix di sicurezza {#install-security-hotfixes}

Assicurati di aver installato la versione più recente [Hotfix di sicurezza forniti da Adobe](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=it).

### Modificare le password predefinite per gli account di amministrazione della console AEM e OSGi {#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts}

Dopo l&#39;installazione, Adobe consiglia di modificare la password per i privilegi [**AEM** `admin` account](#changing-the-aem-admin-password) (su tutte le istanze).

Tali account includono:

* AEM `admin` account

   Dopo aver cambiato la password per l&#39;account amministratore AEM, utilizza la nuova password quando accedi a CRX.

* La `admin` password per la console Web OSGi

   Questa modifica viene applicata anche all’account amministratore utilizzato per accedere alla console Web, quindi utilizza la stessa password per accedervi.

Questi due account utilizzano credenziali separate e dispongono di una password distinta e sicura per ciascuno di essi è fondamentale per una distribuzione sicura.

#### Modifica della password dell&#39;amministratore AEM {#changing-the-aem-admin-password}

La password dell&#39;account amministratore AEM può essere modificata tramite il [Operazioni Granite - Utenti](/help/sites-administering/granite-user-group-admin.md) console.

Qui puoi modificare il `admin` conto e [cambiare la password](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user).

>[!NOTE]
>
>La modifica dell’account amministratore comporta anche la modifica dell’account della console Web OSGi. Dopo aver cambiato l&#39;account amministratore, devi quindi cambiare l&#39;account OSGi in qualcosa di diverso.

#### Importanza della modifica della password della console Web OSGi {#importance-of-changing-the-osgi-web-console-password}

A parte il AEM `admin` account, la mancata modifica della password predefinita per la console Web OSGi può portare a:

* Esposizione del server con una password predefinita durante l&#39;avvio e lo spegnimento (che può richiedere minuti per i server di grandi dimensioni);
* Esposizione del server quando l&#39;archivio è inattivo/riavvio del bundle - e OSGI è in esecuzione.

Per ulteriori informazioni sulla modifica della password della console Web, consulta [Modifica della password dell’amministratore della console Web OSGi](/help/sites-administering/security-checklist.md#changing-the-osgi-web-console-admin-password) sotto.

#### Modifica della password dell’amministratore della console Web OSGi {#changing-the-osgi-web-console-admin-password}

Modificare la password utilizzata per accedere alla console Web. Utilizza un [Configurazione OSGI](/help/sites-deploying/configuring-osgi.md) per aggiornare le seguenti proprietà del **Console di gestione Apache Felix OSGi**:

* **Nome utente** e **Password**, le credenziali per l&#39;accesso alla console di gestione web Apache Felix stessa.
La password deve essere modificata *dopo* l’installazione iniziale per garantire la sicurezza dell’istanza.

>[!NOTE]
>
>Vedi [Configurazione OSGI](/help/sites-deploying/configuring-osgi.md) per informazioni dettagliate sulla configurazione delle impostazioni OSGi.

**Per modificare la password dell&#39;amministratore della console Web OSGi**:

1. Utilizzo della **Strumenti**, **Operazioni** aprire il menu **Console web** e naviga fino al **Configurazione** sezione .
Ad esempio, in `<server>:<port>/system/console/configMgr`.
1. Accedi alla voce e aprila per **Console di gestione Apache Felix OSGi**.
1. Modificare la **nome utente** e **password**.

   ![chlimage_1-3](assets/chlimage_1-3.png)

1. Seleziona **Salva**.

### Implementare un gestore di errori personalizzato {#implement-custom-error-handler}

Adobe consiglia di definire pagine personalizzate del gestore di errori, in particolare per i codici di risposta HTTP 404 e 500 per impedire la divulgazione delle informazioni.

>[!NOTE]
>
>Vedi [Come creare script personalizzati o gestori di errori](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/full-stack/custom-error-page.html?lang=en) per ulteriori dettagli.

### Elenco di controllo completo della sicurezza del dispatcher {#complete-dispatcher-security-checklist}

AEM Dispatcher è un elemento critico dell’infrastruttura. L’Adobe consiglia di completare il [Elenco di controllo della sicurezza del Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/security-checklist.html?lang=en).

>[!CAUTION]
>
>Utilizzando Dispatcher è necessario disabilitare il selettore &quot;.form&quot;.

## Passaggi di verifica {#verification-steps}

### Configurare gli utenti di replica e trasporto {#configure-replication-and-transport-users}

Un&#39;installazione standard di AEM specifica `admin` come utente per le credenziali di trasporto all’interno del valore predefinito [agenti di replica](/help/sites-deploying/replication.md). Inoltre, l&#39;utente amministratore viene utilizzato per avviare la replica sul sistema di authoring.

Per motivi di sicurezza, è opportuno modificare entrambe le opzioni per riflettere il caso d’uso specifico in questione, tenendo presenti i due aspetti seguenti:

* La **utente del trasporto** non deve essere l&#39;utente amministratore. Piuttosto, imposta un utente sul sistema di pubblicazione che dispone solo dei diritti di accesso alle parti rilevanti del sistema di pubblicazione e utilizza le credenziali dell&#39;utente per il trasporto.

   Puoi iniziare dall&#39;utente destinatario della replica in bundle e configurare i diritti di accesso di questo utente in modo che corrispondano alla tua situazione

* La **utente di replica** o **ID utente agente** non deve essere anche l&#39;utente amministratore, ma un utente che può visualizzare solo il contenuto replicato. L’utente di replica viene utilizzato per raccogliere il contenuto da replicare sul sistema dell’autore prima che venga inviato all’editore.

### Controlla i controlli di stato della sicurezza del dashboard delle operazioni {#check-the-operations-dashboard-security-health-checks}

AEM 6 introduce il nuovo dashboard delle operazioni, volto ad aiutare gli operatori del sistema a risolvere i problemi e monitorare lo stato di un&#39;istanza.

Il dashboard viene fornito anche con una raccolta di controlli dello stato di sicurezza. È consigliabile controllare lo stato di tutti i controlli di integrità della sicurezza prima di iniziare a lavorare con l&#39;istanza di produzione. Per ulteriori informazioni, consulta la [Documentazione del dashboard delle operazioni](/help/sites-administering/operations-dashboard.md).

### Controlla se il contenuto di esempio è presente {#check-if-example-content-is-present}

Tutti i contenuti e gli utenti di esempio (ad esempio, il progetto Geometrixx e i relativi componenti) devono essere disinstallati ed eliminati completamente in un sistema produttivo prima di renderlo accessibile al pubblico.

>[!NOTE]
>
>Il campione `We.Retail` le applicazioni vengono rimosse se questa istanza è in esecuzione in [Modalità pronta per la produzione](/help/sites-administering/production-ready.md). In caso contrario, è possibile disinstallare il contenuto di esempio accedendo a Gestione pacchetti e quindi ricercando e disinstallando tutte le `We.Retail` pacchetti.

Vedi [Utilizzare i pacchetti](package-manager.md).

### Controlla se i bundle di sviluppo CRX sono presenti {#check-if-the-crx-development-bundles-are-present}

Questi bundle OSGi di sviluppo devono essere disinstallati sia sui sistemi produttivi di authoring che di pubblicazione prima di renderli accessibili.

* Supporto Adobe CRXDE (com.adobe.granite.crxde-support)
* Adobe Granite CRX Explorer (com.adobe.granite.crx-explorer)
* Adobe Granite CRXDE Lite (com.adobe.granite.crxde-lite)

### Controlla se il bundle di sviluppo Sling è presente {#check-if-the-sling-development-bundle-is-present}

La [Strumenti per sviluppatori AEM](/help/sites-developing/aem-eclipse.md) implementa il supporto per l’installazione di strumenti Apache Sling (org.apache.sling.tooling.support.install).

Questo bundle OSGi deve essere disinstallato sui sistemi produttivi di authoring e pubblicazione prima di renderli accessibili.

### Protect contro la falsificazione delle richieste intersito {#protect-against-cross-site-request-forgery}

#### Quadro di riferimento per la protezione del CSRF {#the-csrf-protection-framework}

AEM 6.1 viene fornito con un meccanismo che aiuta a proteggere dagli attacchi Cross-Site Request Forgery, denominato **Quadro di protezione CSRF**. Per ulteriori informazioni su come utilizzarlo, consulta la [documentazione](/help/sites-developing/csrf-protection.md).

#### Filtro Sling Referrer {#the-sling-referrer-filter}

Per risolvere problemi di sicurezza noti con Cross-Site Request Forgery (CSRF) in CRX WebDAV e Apache Sling, aggiungi configurazioni per il filtro Referrer per utilizzarlo.

Il servizio filtro referrer è un servizio OSGi che consente di configurare quanto segue:

* quali metodi http devono essere filtrati
* se è consentita un&#39;intestazione referrer vuota
* e un elenco di server da consentire oltre all&#39;host del server.

   Per impostazione predefinita, nell’elenco sono presenti tutte le varianti di localhost e i nomi host correnti a cui è associato il server.

Per configurare il servizio filtro referrer:

1. Apri la console Apache Felix (**Configurazioni**) all&#39;indirizzo:

   `https://<server>:<port_number>/system/console/configMgr`

1. Accedi come `admin`.
1. In **Configurazioni** seleziona il menu:

   `Apache Sling Referrer Filter`

1. In `Allow Hosts` immetti tutti gli host consentiti come referrer. Ogni voce deve essere del modulo

   &lt;protocol>://&lt;server>:&lt;port>

   Esempio:

   * `https://allowed.server:80` consente tutte le richieste da questo server con la porta specificata.
   * Se desideri anche consentire le richieste https, devi immettere una seconda riga.
   * Se si consentono tutte le porte da quel server, è possibile utilizzare `0` come numero di porta.

1. Controlla la `Allow Empty` se desideri consentire intestazioni referrer vuote o mancanti.

   >[!CAUTION]
   >
   >Adobe consiglia di fornire un referente durante l&#39;utilizzo di strumenti della riga di comando come `cURL` invece di consentire un valore vuoto in quanto potrebbe esporre il sistema agli attacchi CSRF.

1. Modifica i metodi utilizzati da questo filtro per i controlli con `Filter Methods` campo .

1. Fai clic su **Salva** per salvare le modifiche.

### Impostazioni OSGI {#osgi-settings}

Alcune impostazioni OSGI sono impostate per impostazione predefinita per consentire un debug più semplice dell&#39;applicazione. Modifica tali impostazioni nelle istanze produttive di pubblicazione e authoring per evitare che le informazioni interne vengano divulgate al pubblico.

>[!NOTE]
>
>Tutte le impostazioni seguenti, tranne **Filtro di debug Day CQ WCM** sono automaticamente coperti dal [Modalità pronta per la produzione](/help/sites-administering/production-ready.md). Di conseguenza, Adobe consiglia di rivedere tutte le impostazioni prima di distribuire l’istanza in un ambiente produttivo.

Per ciascuno dei servizi seguenti, è necessario modificare le impostazioni specificate:

* [Adobe Granite HTML Library Manager](/help/sites-deploying/osgi-configuration-settings.md#day-cq-html-library-manager):

   * abilita **Miniatura** (per rimuovere CRLF e gli spazi bianchi).
   * abilita **Gzip** (per consentire l’accesso ai file tramite gzip con una richiesta).
   * disable **Debug**
   * disable **Tempi**

* [Filtro di debug Day CQ WCM](/help/sites-deploying/osgi-configuration-settings.md#day-cq-wcm-debug-filter):

   * deseleziona **Abilita**

* [Filtro WCM Day CQ](/help/sites-deploying/osgi-configuration-settings.md):

   * solo per pubblicazione, imposta **Modalità WCM** a &quot;disabilitato&quot;

* [Gestore JavaScript Apache Sling](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-javascript-handler):

   * disable **Genera informazioni di debug**

* [Apache Sling JSP Script Handler](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-jsp-script-handler):

   * disable **Genera informazioni di debug**
   * disable **Contenuto mappato**

Vedi [Impostazioni di configurazione OSGi](/help/sites-deploying/osgi-configuration-settings.md).

Quando si lavora con AEM, esistono diversi metodi per gestire le impostazioni di configurazione per tali servizi; vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per ulteriori dettagli e procedure consigliate.

## Ulteriori letture {#further-readings}

### Riduzione degli attacchi di tipo DoS (Denial of Service) {#mitigate-denial-of-service-dos-attacks}

Un attacco Denial of Service (DoS) è un tentativo di rendere la risorsa di un computer indisponibile per gli utenti a cui è destinata. Questo attacco viene spesso fatto sovraccaricando la risorsa; ad esempio:

* Un flusso di richieste da una fonte esterna.
* Una richiesta di più informazioni di quelle che il sistema può fornire correttamente.

   Ad esempio, una rappresentazione JSON dell’intero archivio.

* Richiedendo una pagina di contenuto con un numero illimitato di URL, l’URL può includere un handle, alcuni selettori, un’estensione e un suffisso, ciascuno dei quali può essere modificato.

   Ad esempio: `.../en.html` può anche essere richiesto come:

   * `.../en.ExtensionDosAttack`
   * `.../en.SelectorDosAttack.html`
   * `.../en.html/SuffixDosAttack`

   Tutte le varianti valide (ad esempio, restituisce un `200` response e sono configurati per essere memorizzati nella cache) sono memorizzati in cache da Dispatcher, con conseguente creazione di un file system completo e nessun servizio per ulteriori richieste.

Ci sono molti punti di configurazione per prevenire tali attacchi, ma solo i punti che si riferiscono a AEM sono discussi qui.

**Configurazione di Sling per impedire il DoS**

Sling è *incentrato sul contenuto*. L’elaborazione è incentrata sul contenuto, in quanto ogni richiesta (HTTP) viene mappata sul contenuto sotto forma di una risorsa JCR (un nodo di archivio):

* Il primo target è la risorsa (nodo JCR) che contiene il contenuto.
* In secondo luogo, il renderer, o script, si trova dalle proprietà della risorsa con alcune parti della richiesta (ad esempio, selettori e/o estensione).

Vedi [Elaborazione delle richieste Sling](/help/sites-developing/the-basics.md#sling-request-processing) per ulteriori informazioni.

Questo approccio rende Sling potente e flessibile, ma come sempre è la flessibilità che deve essere gestita con attenzione.

Per evitare l&#39;uso improprio di DoS, è possibile effettuare le seguenti operazioni:

1. Incorpora controlli a livello di applicazione. A causa del numero di varianti possibile, una configurazione predefinita non è fattibile.

   Nella tua applicazione devi:

   * Controlla i selettori nell&#39;applicazione, in modo che tu *only* serve i selettori espliciti necessari e restituisce `404` per tutti gli altri.
   * Impedisci l’output di un numero illimitato di nodi di contenuto.

1. Controlla la configurazione dei moduli di rendering predefiniti, che possono essere un’area problematica.

   * In particolare, il modulo di rendering JSON passa la struttura ad albero su più livelli.

      Ad esempio, la richiesta:

      `http://localhost:4502/.json`

      potrebbe scaricare l’intero archivio in una rappresentazione JSON che può causare gravi problemi al server. Per questo motivo, Sling imposta un limite sul numero di risultati massimi. Per limitare la profondità del rendering JSON, imposta il valore per quanto segue:

      **Risultati massimi JSON** ( `json.maximumresults`)

      nella configurazione per [Servlet Apache Sling GET](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet). Quando questo limite viene superato, il rendering viene compresso. Il valore predefinito per Sling in AEM è `1000`.

   * Come misura preventiva, è necessario disattivare gli altri moduli di rendering predefiniti (HTML, testo normale, XML). Anche in questo caso, configurando il [Servlet Apache Sling GET](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet).
   >[!CAUTION]
   >
   >Non disabilitare il renderer JSON perché è necessario per il normale funzionamento di AEM.

1. Utilizza un firewall per filtrare l’accesso all’istanza.

   * L&#39;utilizzo di un firewall a livello di sistema operativo è necessario per filtrare l&#39;accesso ai punti dell&#39;istanza che potrebbero causare attacchi di tipo Denial of Service se lasciato senza protezione.

**Riduzione degli errori di DoS causati dall’utilizzo di selettori di moduli**

>[!NOTE]
>
>Questa mitigazione deve essere eseguita solo su ambienti AEM che non utilizzano Forms.

Poiché AEM non fornisce indici predefiniti per il `FormChooserServlet`, l’utilizzo di selettori di moduli nelle query può attivare un costoso attraversamento dell’archivio, solitamente bloccando l’istanza AEM. I selettori di moduli possono essere rilevati dalla presenza di **&amp;ast;.form.&amp;ast;** stringa nelle query.

Per attenuare questo problema, puoi effettuare le seguenti operazioni:

1. Passa alla console Web puntando il browser verso *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*

1. Cerca **Servizio di selezione moduli di CQ WCM Day**
1. Dopo aver fatto clic sulla voce, disattiva la **Ricerca avanzata richiesta** nella finestra seguente.

1. Fai clic su **Salva**.

**Riduzione del numero di DoS causato dal servlet di download delle risorse**

Il servlet di download delle risorse predefinito consente agli utenti autenticati di emettere richieste di download arbitrariamente grandi e simultanee per creare file ZIP di risorse. La creazione di grandi archivi ZIP può sovraccaricare il server e la rete. Per attenuare il rischio potenziale di diniego del servizio (DoS) causato da questo comportamento, `AssetDownloadServlet` Il componente OSGi è disabilitato per impostazione predefinita su [!DNL Experience Manager] pubblica istanza. È attivato su [!DNL Experience Manager] istanza di authoring per impostazione predefinita.

Se non hai bisogno della funzionalità di download, disattiva il servlet nelle distribuzioni di authoring e pubblicazione. Se la configurazione richiede l’abilitazione della funzionalità di download delle risorse, consulta [articolo](/help/assets/download-assets-from-aem.md) per ulteriori informazioni. Inoltre, puoi definire un limite massimo di download supportato dalla distribuzione.

### Disattiva WebDAV {#disable-webdav}

Disattiva WebDAV sia negli ambienti di authoring che di pubblicazione arrestando i bundle OSGi appropriati.

1. Collega a **Console di gestione Felix** in esecuzione:

   `https://<*host*>:<*port*>/system/console`

   Esempio: `http://localhost:4503/system/console/bundles`.

1. Nell’elenco dei bundle, trova il bundle denominato:

   `Apache Sling Simple WebDAV Access to repositories (org.apache.sling.jcr.webdav)`

1. Per arrestare questo bundle, nella colonna Azioni fare clic sul pulsante di arresto.

1. Di nuovo, nell&#39;elenco dei bundle, trova il bundle denominato:

   `Apache Sling DavEx Access to repositories (org.apache.sling.jcr.davex)`

1. Per interrompere il bundle, fai clic sul pulsante di arresto.

   >[!NOTE]
   >
   >Non è necessario riavviare AEM.

### Verifica Di Non Divulgare Informazioni Personalmente Identificabili Nel Percorso Home Dell’Utente {#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path}

È importante proteggere gli utenti assicurandosi di non esporre informazioni personali identificabili nel percorso home degli utenti dell’archivio.

A partire AEM 6.1, il modo in cui vengono memorizzati i nomi dei nodi ID utente (noti anche come autorizzabili) viene modificato con una nuova implementazione del `AuthorizableNodeName` interfaccia. La nuova interfaccia non espone più l’ID utente nel nome del nodo, ma genera un nome casuale.

Non è necessario eseguire alcuna configurazione per abilitarla, perché ora è il modo predefinito per generare ID autorizzabili in AEM.

Anche se non consigliato, puoi disattivarlo nel caso in cui sia necessaria la vecchia implementazione per garantire la compatibilità con le applicazioni esistenti. Per eseguire questa operazione, è necessario effettuare le seguenti operazioni:

1. Vai alla Console web e rimuovi la voce** org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName** dalla proprietà **requiredServicePids** in **Apache Jackrabbit Oak SecurityProvider**.

   Puoi anche trovare il provider di sicurezza Oak cercando il **org.apache.jackrabbit.oak.security.internal.SecurityProviderRegistration** PID nelle configurazioni OSGi.

1. Elimina **Nome nodo Apache Jackrabbit Oak casuale autorizzabile** Configurazione OSGi dalla console Web.

   Per una ricerca più semplice, il PID di questa configurazione è **org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**.

>[!NOTE]
>
>Per ulteriori informazioni, consulta la documentazione Oak su [Generazione di nomi di nodo autorizzati](https://jackrabbit.apache.org/oak/docs/security/user/authorizablenodename.html).

### Pacchetto di indurimento delle autorizzazioni anonime {#anonymous-permission-hardening-package}

Per impostazione predefinita, AEM memorizza i metadati del sistema, ad esempio `jcr:createdBy` o `jcr:lastModifiedBy` come proprietà del nodo, accanto al contenuto regolare, nell’archivio. A seconda della configurazione e della configurazione del controllo di accesso, in alcuni casi ciò potrebbe portare all’esposizione di informazioni personali identificabili (PII), ad esempio quando tali nodi vengono sottoposti a rendering come JSON o XML non elaborati.

Come tutti i dati dell&#39;archivio, queste proprietà sono mediate dallo stack di autorizzazioni Oak. L&#39;accesso ad essi dovrebbe essere limitato in base al principio del minimo privilegio.

Per supportare questo, Adobe fornisce un pacchetto di protezione delle autorizzazioni come base su cui i clienti possono basarsi. Funziona installando una voce di controllo accessi &quot;negati&quot; nella directory principale dell&#39;archivio, limitando l&#39;accesso anonimo alle proprietà di sistema comunemente utilizzate. Il pacchetto è disponibile per il download [qui](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/helper/anonymous-permissions-pkg-0.1.2.zip) e può essere installato su tutte le versioni supportate di AEM. Per ulteriori informazioni, consulta le note sulla versione .

### Previeni il clickjacking {#prevent-clickjacking}

Per evitare il clickjacking, Adobe consiglia di configurare il server web in modo che fornisca `X-FRAME-OPTIONS` intestazione HTTP impostata su `SAMEORIGIN`.

Per ulteriori informazioni sul clickjacking, consulta la sezione [Sito OWASP](https://www.owasp.org/index.php/Clickjacking).

### Assicurati Di Replicare Correttamente Le Chiavi Di Crittografia Quando Necessario {#make-sure-you-properly-replicate-encryption-keys-when-needed}

Alcune funzioni AEM e schemi di autenticazione richiedono la replica delle chiavi di crittografia in tutte le istanze AEM.

Prima di eseguire questa operazione, la replica chiave viene eseguita in modo diverso tra le versioni, perché il modo in cui le chiavi vengono memorizzate è diverso tra le versioni 6.3 e precedenti.

Per ulteriori informazioni, consulta di seguito.

#### Replica delle chiavi per AEM 6.3 {#replicating-keys-for-aem}

Mentre nelle versioni precedenti le chiavi di replica venivano memorizzate nell&#39;archivio, a partire da AEM 6.3 vengono memorizzate nel filesystem.

Pertanto, per replicare le chiavi tra le istanze, copiale dall&#39;istanza di origine alla posizione delle istanze di destinazione sul file system.

In particolare, devi effettuare le seguenti operazioni:

1. Accedi all&#39;istanza AEM, in genere un&#39;istanza dell&#39;autore, che contiene il materiale chiave da copiare;
1. Individua il bundle com.adobe.granite.crypto.file nel file system locale. Ad esempio, sotto questo percorso:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`

   La `bundle.info` all’interno di ogni cartella identifica il nome del bundle.

1. Passa alla cartella dati. Esempio:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Copiare i file HMAC e master.
1. Quindi, vai all&#39;istanza di destinazione a cui desideri duplicare la chiave HMAC e passa alla cartella dei dati. Esempio:

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Incolla i due file copiati in precedenza.
1. [Aggiorna il bundle Crypto](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) se l’istanza target è già in esecuzione.
1. Ripeti i passaggi precedenti per tutte le istanze in cui desideri replicare la chiave.

>[!NOTE]
>
>Per ripristinare il metodo di memorizzazione delle chiavi precedente alla versione 6.3, aggiungi il parametro seguente al primo avvio dell&#39;installazione di AEM:
>
>`-Dcom.adobe.granite.crypto.file.disable=true`

#### Replica delle chiavi per le versioni AEM 6.2 e precedenti {#replicating-keys-for-aem-and-older-versions}

Nelle versioni AEM 6.2 e precedenti, le chiavi sono memorizzate nell&#39;archivio sotto `/etc/key` nodo.

Il modo consigliato per replicare in modo sicuro le chiavi nelle istanze è quello di replicare solo questo nodo. È possibile replicare in modo selettivo i nodi tramite CRXDE Lite:

1. Apri CRXDE Lite andando in *`https://&lt;serveraddress&gt;:4502/crx/de/index.jsp`*
1. Seleziona la `/etc/key` nodo.
1. Vai a **Replica** scheda .
1. Premere **Replica** pulsante .

### Esegui un test di penetrazione {#perform-a-penetration-test}

Adobe consiglia di eseguire un test di penetrazione dell&#39;infrastruttura AEM prima di procedere alla produzione.

### Tecniche consigliate per lo sviluppo {#development-best-practices}

È fondamentale che il nuovo sviluppo segua la [Tecniche consigliate per la sicurezza](/help/sites-developing/security.md) per garantire che l’ambiente AEM rimanga sicuro.
