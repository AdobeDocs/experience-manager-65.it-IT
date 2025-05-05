---
title: Elenco di controllo della sicurezza
description: Scopri le varie considerazioni sulla sicurezza durante la configurazione e la distribuzione di AEM.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
exl-id: 314a6409-398c-470b-8799-0c4e6f745141
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin,Developer
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '2959'
ht-degree: 1%

---

# Elenco di controllo della sicurezza {#security-checklist}

Questa sezione descrive i vari passaggi da seguire per garantire la sicurezza dell’installazione dell’AEM durante l’installazione. L’elenco di controllo deve essere applicato dall’alto verso il basso.

>[!NOTE]
>
>Sono inoltre disponibili ulteriori informazioni sulle minacce più pericolose per la sicurezza pubblicate da [Open Web Application Security Project (OWASP)](https://owasp.org/www-project-top-ten/).

>[!NOTE]
>
>Ci sono alcune [considerazioni di sicurezza](/help/sites-developing/dev-guidelines-bestpractices.md#security-considerations) aggiuntive applicabili alla fase di sviluppo.

## Principali misure di sicurezza {#main-security-measures}

### Eseguire AEM in modalità pronta per la produzione {#run-aem-in-production-ready-mode}

Per ulteriori informazioni, vedere [Esecuzione di AEM in modalità pronta per la produzione](/help/sites-administering/production-ready.md).

### Abilita HTTPS per la sicurezza del livello di trasporto {#enable-https-for-transport-layer-security}

Per poter disporre di un’istanza protetta, è obbligatorio abilitare il livello di trasporto HTTPS sia sulle istanze di authoring che su quelle di pubblicazione.

>[!NOTE]
>
>Per ulteriori informazioni, vedere la sezione [Abilitazione di HTTP su SSL](/help/sites-administering/ssl-by-default.md).

### Installare gli hotfix di sicurezza {#install-security-hotfixes}

Assicurati di aver installato gli [aggiornamenti rapidi per la sicurezza forniti dall&#39;Adobe](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=it).

### Modificare le password predefinite per gli account amministratore di AEM e OSGi Console {#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts}

L&#39;Adobe consiglia dopo l&#39;installazione di modificare la password per gli account [**AEM** `admin` ](#changing-the-aem-admin-password) con privilegi (su tutte le istanze).

Tali account includono:

* Account `admin` dell&#39;AEM

  Dopo aver modificato la password per l&#39;account amministratore AEM, utilizzare la nuova password per accedere a CRX.

* La password `admin` per la console Web OSGi

  Questa modifica viene applicata anche all’account amministratore utilizzato per accedere alla console Web, pertanto utilizza la stessa password per l’accesso.

Questi due account utilizzano credenziali separate e disporre di password distinte e sicure per ciascuno è fondamentale per una distribuzione sicura.

#### Modifica della password amministratore AEM {#changing-the-aem-admin-password}

La password per l&#39;account amministratore AEM può essere modificata tramite la console [Granite Operations - Users](/help/sites-administering/granite-user-group-admin.md).

Qui puoi modificare l&#39;account `admin` e [cambiare la password](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user).

>[!NOTE]
>
>La modifica dell’account amministratore comporta anche la modifica dell’account della console web OSGi. Dopo aver modificato l’account amministratore, devi impostare l’account OSGi su un valore diverso.

#### Importanza della modifica della password della console Web OSGi {#importance-of-changing-the-osgi-web-console-password}

A parte l&#39;account AEM `admin`, se non si modifica la password predefinita per la console Web OSGi è possibile che:

* Esposizione del server con una password predefinita durante l&#39;avvio e l&#39;arresto (che può richiedere alcuni minuti per i server di grandi dimensioni);
* Esposizione del server quando l’archivio è inattivo/il bundle di riavvio e OSGI è in esecuzione.

Per ulteriori informazioni sulla modifica della password della console Web, vedere [Modifica della password dell&#39;amministratore della console Web OSGi](/help/sites-administering/security-checklist.md#changing-the-osgi-web-console-admin-password) di seguito.

#### Modifica della password amministratore per la console Web OSGi {#changing-the-osgi-web-console-admin-password}

Modifica la password utilizzata per accedere alla console Web. Utilizza una [configurazione OSGI](/help/sites-deploying/configuring-osgi.md) per aggiornare le seguenti proprietà della **console di gestione Apache Felix OSGi**:

* **Nome utente** e **Password**, le credenziali per accedere alla Console di gestione Web Apache Felix.
La password deve essere cambiata *dopo* l&#39;installazione iniziale per garantire la sicurezza dell&#39;istanza.

>[!NOTE]
>
>Per informazioni dettagliate sulla configurazione delle impostazioni OSGi, consulta [Configurazione OSGi](/help/sites-deploying/configuring-osgi.md).

**Per modificare la password amministratore della console Web OSGi**:

1. Utilizzando il menu **Strumenti**, **Operazioni**, apri la **console Web** e passa alla sezione **Configurazione**.
Ad esempio, alle `<server>:<port>/system/console/configMgr`.
1. Passare alla voce **Console di gestione OSGi Apache Felix** e aprirla.
1. Modifica il **nome utente** e la **password**.

   ![chlimage_1-3](assets/chlimage_1-3.png)

1. Seleziona **Salva**.

### Implementare un gestore degli errori personalizzato {#implement-custom-error-handler}

L’Adobe consiglia di definire pagine personalizzate del gestore degli errori, in particolare per i codici di risposta HTTP 404 e 500, per impedire la divulgazione delle informazioni.

>[!NOTE]
>
>Per ulteriori dettagli, vedere [Come creare script personalizzati o gestori di errori](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/full-stack/custom-error-page.html?lang=it).

### Completa elenco di controllo della sicurezza di Dispatcher {#complete-dispatcher-security-checklist}

AEM Dispatcher è un componente fondamentale dell&#39;infrastruttura aziendale. L&#39;Adobe consiglia di completare l&#39;[elenco di controllo della sicurezza di Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/security-checklist.html?lang=it).

>[!CAUTION]
>
>Con Dispatcher è necessario disattivare il selettore &quot;.form&quot;.

## Passaggi della verifica {#verification-steps}

### Configurare gli utenti di replica e trasporto {#configure-replication-and-transport-users}

Un&#39;installazione standard di AEM specifica `admin` come utente per le credenziali di trasporto all&#39;interno dei [agenti di replica](/help/sites-deploying/replication.md) predefiniti. Inoltre, l’utente amministratore viene utilizzato per determinare l’origine della replica sul sistema di authoring.

Per motivi di sicurezza, entrambi dovrebbero essere modificati per riflettere il caso d’uso specifico in questione, tenendo presenti i due aspetti seguenti:

* L&#39;**utente trasporto** non deve essere l&#39;utente amministratore. Piuttosto, imposta un utente sul sistema di pubblicazione che dispone solo dei diritti di accesso alle parti pertinenti del sistema di pubblicazione e utilizza le credenziali di tale utente per il trasporto.

  Puoi iniziare dall’utente di ricezione della replica in bundle e configurare i diritti di accesso di questo utente in base alla tua situazione

* Anche l&#39;**utente di replica** o l&#39;**ID utente agente** non deve essere l&#39;utente amministratore, ma un utente in grado di visualizzare solo il contenuto replicato. L’utente di replica viene utilizzato per raccogliere il contenuto da replicare sul sistema di authoring prima che venga inviato all’editore.

### Verifica i controlli di integrità della sicurezza del dashboard operazioni {#check-the-operations-dashboard-security-health-checks}

AEM6 introduce il nuovo dashboard delle operazioni, volto ad aiutare gli operatori di sistema a risolvere i problemi e a monitorare lo stato di un’istanza.

La dashboard viene inoltre fornita con una raccolta di controlli di integrità della sicurezza. Si consiglia di controllare lo stato di tutti i controlli di integrità della sicurezza prima di andare &quot;live&quot; con l’istanza di produzione. Per ulteriori informazioni, consultare la [documentazione del dashboard operazioni](/help/sites-administering/operations-dashboard.md).

### Controlla se il contenuto di esempio è presente {#check-if-example-content-is-present}

Tutti gli utenti e i contenuti di esempio (ad esempio, il progetto e i relativi componenti) devono essere disinstallati ed eliminati completamente in un Geometrixx produttivo prima di renderlo accessibile al pubblico.

>[!NOTE]
>
>Le applicazioni `We.Retail` di esempio vengono rimosse se questa istanza è in esecuzione in [modalità pronta per la produzione](/help/sites-administering/production-ready.md). In caso contrario, è possibile disinstallare il contenuto di esempio da Gestione pacchetti, quindi cercare e disinstallare tutti i `We.Retail` pacchetti.

Vedi [Operazioni Con I Pacchetti](package-manager.md).

### Verifica se i bundle di sviluppo CRX sono presenti {#check-if-the-crx-development-bundles-are-present}

Prima di renderli accessibili, questi bundle OSGi di sviluppo devono essere disinstallati sia sui sistemi produttivi di authoring che su quelli di pubblicazione.

* Adobe di supporto per CRXDE (com.adobe.granite.crxde-support)
* Adobe Granite CRX Explorer (com.adobe.granite.crx-explorer)
* Adobe Granite CRXDE Lite (com.adobe.granite.crxde-lite)

### Verifica se il bundle di sviluppo Sling è presente {#check-if-the-sling-development-bundle-is-present}

Gli [strumenti per sviluppatori AEM](/help/sites-developing/aem-eclipse.md) distribuiscono l&#39;installazione del supporto per gli strumenti Sling di Apache (org.apache.sling.tooling.support.install).

Prima di renderli accessibili, questo bundle OSGi deve essere disinstallato sui sistemi produttivi sia di authoring che di pubblicazione.

### Protect contro il rischio di false richieste tra siti diversi {#protect-against-cross-site-request-forgery}

#### Il framework di protezione CSRF {#the-csrf-protection-framework}

AEM 6.1 viene fornito con un meccanismo che aiuta a proteggere da attacchi Cross-Site Request Forgery, denominato **CSRF Protection Framework**. Per ulteriori informazioni su come utilizzarla, consulta la [documentazione](/help/sites-developing/csrf-protection.md).

#### Il filtro Sling Referrer {#the-sling-referrer-filter}

Per risolvere i problemi di sicurezza noti con Cross-Site Request Forgery (CSRF) in CRX WebDAV e Apache Sling, aggiungi le configurazioni per il filtro Referrer per utilizzarlo.

Il servizio di filtro dei referenti è un servizio OSGi che consente di configurare quanto segue:

* quali metodi http filtrare
* se è consentita un’intestazione referente vuota
* e un elenco di server da consentire in aggiunta all’host del server.

  Per impostazione predefinita, tutte le varianti di localhost e i nomi host correnti a cui è associato il server sono inclusi nell&#39;elenco.

Per configurare il servizio filtro referenti:

1. Apri la console Apache Felix (**Configurazioni**) in:

   `https://<server>:<port_number>/system/console/configMgr`

1. Accedi come `admin`.
1. Nel menu **Configurazioni**, seleziona:

   `Apache Sling Referrer Filter`

1. Nel campo `Allow Hosts`, immettere tutti gli host consentiti come referrer. Ogni voce deve essere nel modulo

   &lt;protocollo>://&lt;server>:&lt;porta>

   Ad esempio:

   * `https://allowed.server:80` consente tutte le richieste provenienti da questo server con la porta specificata.
   * Se desideri anche consentire le richieste https, devi immettere una seconda riga.
   * Se si consentono tutte le porte da tale server, è possibile utilizzare `0` come numero di porta.

1. Se vuoi consentire intestazioni referente vuote o mancanti, seleziona il campo `Allow Empty`.

   >[!CAUTION]
   >
   >L&#39;Adobe consiglia di fornire un referente durante l&#39;utilizzo di strumenti della riga di comando come `cURL` invece di consentire un valore vuoto in quanto potrebbe esporre il sistema ad attacchi CSRF.

1. Modificare i metodi utilizzati da questo filtro per i controlli con il campo `Filter Methods`.

1. Fai clic su **Salva** per salvare le modifiche.

### Impostazioni OSGI {#osgi-settings}

Alcune impostazioni OSGI sono impostate per impostazione predefinita per consentire un debug più semplice dell’applicazione. Modifica tali impostazioni sulle istanze produttive di pubblicazione e authoring per evitare la perdita di informazioni interne al pubblico.

>[!NOTE]
>
>Tutte le impostazioni seguenti, ad eccezione di **The Day CQ WCM Debug Filter**, sono coperte automaticamente dalla [modalità pronta per la produzione](/help/sites-administering/production-ready.md). Di conseguenza, Adobe consiglia di rivedere tutte le impostazioni prima di distribuire l’istanza in un ambiente produttivo.

È necessario modificare le impostazioni specificate per ciascuno dei servizi seguenti:

* [Adobe Granite HTML Library Manager](/help/sites-deploying/osgi-configuration-settings.md#day-cq-html-library-manager):

   * abilita **Minify** (per rimuovere i caratteri CRLF e gli spazi vuoti).
   * abilita **Gzip** (per consentire l&#39;accesso e la visualizzazione dei file con una richiesta).
   * disabilita **Debug**
   * disabilita **Intervallo**

* [Filtro di debug WCM Day CQ](/help/sites-deploying/osgi-configuration-settings.md#day-cq-wcm-debug-filter):

   * deseleziona **Abilita**

* [Filtro WCM Day CQ](/help/sites-deploying/osgi-configuration-settings.md):

   * solo per pubblicazione, impostare **Modalità WCM** su &quot;disabilitato&quot;

* [Gestore JavaScript Apache Sling](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-javascript-handler):

   * disabilita **Genera informazioni debug**

* [Gestore script JSP Apache Sling](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-jsp-script-handler):

   * disabilita **Genera informazioni debug**
   * disabilita **Contenuto mappato**

Consulta [Impostazioni configurazione OSGi](/help/sites-deploying/osgi-configuration-settings.md).

Quando si lavora con AEM, esistono diversi metodi per gestire le impostazioni di configurazione per tali servizi; vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per ulteriori dettagli e le procedure consigliate.

## Letture ulteriori {#further-readings}

### Mitigare gli attacchi Denial of Service (DoS) {#mitigate-denial-of-service-dos-attacks}

Un attacco Denial of Service (DoS) è un tentativo di rendere una risorsa del computer non disponibile per gli utenti a cui è destinata. Questo attacco viene spesso eseguito sovraccaricando la risorsa, ad esempio:

* Un flusso di richieste provenienti da una sorgente esterna.
* Una richiesta di informazioni superiore a quelle che il sistema è in grado di fornire.

  Ad esempio, una rappresentazione JSON dell’intero archivio.

* Richiedendo una pagina di contenuto con un numero illimitato di URL, l’URL può includere un handle, alcuni selettori, un’estensione e un suffisso, ciascuno dei quali può essere modificato.

  Ad esempio, `.../en.html` può anche essere richiesto come:

   * `.../en.ExtensionDosAttack`
   * `.../en.SelectorDosAttack.html`
   * `.../en.html/SuffixDosAttack`

  Tutte le varianti valide (ad esempio, restituiscono una risposta `200` e sono configurate per essere memorizzate nella cache) vengono memorizzate nella cache da Dispatcher, portando a un file system completo e a nessun servizio per ulteriori richieste.

Ci sono molti punti di configurazione per prevenire questi attacchi, ma solo i punti che si riferiscono all&#39;AEM sono discussi qui.

**Configurazione di Sling per impedire DoS**

Sling è *incentrato sul contenuto*. L’elaborazione si concentra sul contenuto, in quanto ogni richiesta (HTTP) viene mappata sul contenuto sotto forma di risorsa JCR (un nodo dell’archivio):

* La prima destinazione è la risorsa (nodo JCR) contenente il contenuto.
* In secondo luogo, il renderer, o script, si trova dalle proprietà della risorsa con alcune parti della richiesta (ad esempio, selettori e/o estensione).

Per ulteriori informazioni, vedere [Elaborazione richiesta Sling](/help/sites-developing/the-basics.md#sling-request-processing).

Questo approccio rende Sling potente e flessibile, ma come sempre è la flessibilità che deve essere gestita con attenzione.

Per evitare l&#39;uso improprio del DoS, è possibile effettuare le seguenti operazioni:

1. Incorporare controlli a livello di applicazione. A causa del numero di varianti possibili, non è possibile effettuare una configurazione predefinita.

   Nell’applicazione dovresti:

   * Controlla i selettori nell&#39;applicazione, in modo da *solo* distribuire i selettori espliciti necessari e restituire `404` per tutti gli altri.
   * Impedisci l’output di un numero illimitato di nodi di contenuto.

1. Controlla la configurazione dei renderer predefiniti, che può rappresentare un’area problematica.

   * In particolare, il renderer JSON trasmette la struttura ad albero su più livelli.

     Ad esempio:

     `http://localhost:4502/.json`

     potrebbe scaricare l’intero archivio in una rappresentazione JSON, il che potrebbe causare problemi significativi al server. Per questo motivo, Sling imposta un limite al numero di risultati massimi. Per limitare la profondità del rendering JSON, imposta il valore per quanto segue:

     **Risultati Max JSON** (`json.maximumresults`)

     nella configurazione per [Apache Sling GET Servlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet). Quando questo limite viene superato, il rendering viene compresso. Il valore predefinito per Sling in AEM è `1000`.

   * Come misura preventiva, disattivate gli altri renderer predefiniti (HTML, testo normale, XML). Di nuovo, configurando [Apache Sling GET Servlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet).

   >[!CAUTION]
   >
   >Non disabilitare il renderer JSON perché è necessario per il normale funzionamento dell’AEM.

1. Utilizza un firewall per filtrare l’accesso all’istanza.

   * L’utilizzo di un firewall a livello di sistema operativo è necessario per filtrare l’accesso ai punti dell’istanza che, se lasciati non protetti, potrebbero causare attacchi Denial of Service.

**Attenuare i DoS causati dall&#39;utilizzo dei selettori di moduli**

>[!NOTE]
>
>Questa mitigazione deve essere eseguita solo sugli ambienti AEM che non utilizzano Forms.

Poiché l&#39;AEM non fornisce indici predefiniti per `FormChooserServlet`, l&#39;utilizzo di selettori di moduli nelle query può determinare un costoso attraversamento dell&#39;archivio, in genere bloccando l&#39;istanza dell&#39;AEM. I selettori di moduli possono essere rilevati dalla presenza di **&ast;.form.&ast;** stringa nelle query.

Per attenuare questo problema, puoi effettuare le seguenti operazioni:

1. Passa alla console Web puntando il browser su *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*

1. Cerca **Day CQ WCM Form Chooser Servlet**
1. Dopo aver fatto clic sulla voce, disabilitare **Ricerca avanzata richiesta** nella finestra seguente.

1. Fai clic su **Salva**.

**Attenuazione rispetto ai DoS causati dal servlet di download risorse**

Il servlet di download delle risorse predefinito consente agli utenti autenticati di inviare richieste di download simultanee di grandi dimensioni e arbitrarie per creare file ZIP delle risorse. La creazione di grandi archivi ZIP può sovraccaricare il server e la rete. Per attenuare un potenziale rischio Denial of Service (DoS) causato da questo comportamento, il componente OSGi `AssetDownloadServlet` è disabilitato per impostazione predefinita nell&#39;istanza di pubblicazione [!DNL Experience Manager]. Per impostazione predefinita, è abilitato nell&#39;istanza di authoring [!DNL Experience Manager].

Se non hai bisogno della funzionalità di download, disabilita il servlet nelle distribuzioni di authoring e pubblicazione. Se la configurazione richiede che la funzionalità di download delle risorse sia abilitata, consulta [Scaricare risorse da Adobe Experience Manager](/help/assets/download-assets-from-aem.md) per ulteriori informazioni. Inoltre, puoi definire un limite massimo di download supportato dalla tua implementazione.

### Disattiva WebDAV {#disable-webdav}

Arresta i bundle OSGi appropriati per disabilitare WebDAV negli ambienti di authoring e di pubblicazione.

1. Connettersi alla **Console di gestione Felix** in esecuzione su:

   `https://<*host*>:<*port*>/system/console`

   Esempio: `http://localhost:4503/system/console/bundles`.

1. Nell’elenco dei bundle, individua il bundle denominato:

   `Apache Sling Simple WebDAV Access to repositories (org.apache.sling.jcr.webdav)`

1. Per arrestare questo bundle, nella colonna Azioni, fai clic sul pulsante Interrompi.

1. Di nuovo, nell’elenco dei bundle, individua il bundle denominato:

   `Apache Sling DavEx Access to repositories (org.apache.sling.jcr.davex)`

1. Per arrestare questo bundle, fai clic sul pulsante Stop.

   >[!NOTE]
   >
   >Non è necessario riavviare l’AEM.

### Verifica Di Non Divulgare Informazioni Personalmente Identificabili Nel Percorso Home Degli Utenti {#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path}

È importante proteggere gli utenti accertandosi di non esporre informazioni personali identificabili nel percorso principale degli utenti dell’archivio.

A partire da AEM 6.1, il modo in cui i nomi dei nodi ID degli utenti (noti anche come autorizzabili) vengono memorizzati viene modificato con una nuova implementazione dell&#39;interfaccia `AuthorizableNodeName`. La nuova interfaccia non espone più l’ID utente nel nome del nodo, ma genera invece un nome casuale.

Non è necessario eseguire alcuna configurazione per abilitarla, perché è ora il modo predefinito per generare ID autorizzabili nell’AEM.

Anche se non consigliato, puoi disattivarlo nel caso sia necessaria la vecchia implementazione per compatibilità con le applicazioni esistenti. A tale scopo, è necessario effettuare le seguenti operazioni:

1. Vai alla console Web e rimuovi la voce **&#x200B; org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName** dalla proprietà **requiredServicePids** in **Apache Jackrabbit Oak SecurityProvider**.

   Puoi anche trovare il provider della sicurezza Oak cercando il PID **org.apache.jackrabbit.oak.security.internal.SecurityProviderRegistration** nelle configurazioni OSGi.

1. Elimina la configurazione OSGi **Apache Jackrabbit Oak Random Authorizable Node Name** dalla console Web.

   Per una ricerca più semplice, il PID per questa configurazione è **org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**.

>[!NOTE]
>
>Per ulteriori informazioni, consulta la documentazione di Oak su [Authorizable Node Name Generation](https://jackrabbit.apache.org/oak/docs/security/user/authorizablenodename.html).

### Pacchetto di protezione autorizzazioni anonime {#anonymous-permission-hardening-package}

Per impostazione predefinita, l&#39;AEM memorizza i metadati di sistema, ad esempio `jcr:createdBy` o `jcr:lastModifiedBy`, come proprietà del nodo, accanto al contenuto normale, nell&#39;archivio. A seconda della configurazione e dell’impostazione del controllo di accesso, in alcuni casi questo potrebbe causare l’esposizione di informazioni personali (PII, personally identifiable information), ad esempio, quando tali nodi vengono riprodotti come JSON o XML non elaborati.

Come tutti i dati dell’archivio, queste proprietà sono mediate dallo stack di autorizzazione di Oak. L&#39;accesso ad esse dovrebbe essere limitato conformemente al principio del minimo privilegio.

Per supportare questa funzione, Adobe fornisce un pacchetto di protezione delle autorizzazioni come base su cui i clienti possono basarsi. Funziona installando una voce di controllo di accesso &quot;nega&quot; nella directory principale dell’archivio, limitando l’accesso anonimo alle proprietà di sistema comunemente utilizzate. Il pacchetto può essere [scaricato](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/helper/anonymous-permissions-pkg-0.1.2.zip) e installato in tutte le versioni supportate di AEM.

Per illustrare le modifiche, possiamo confrontare le proprietà del nodo che possono essere visualizzate in modo anonimo prima di installare il pacchetto:

![Prima di installare il pacchetto](/help/sites-administering/assets/before_resized.png)

con quelli visualizzabili dopo l&#39;installazione del pacchetto, dove `jcr:createdBy` e `jcr:lastModifiedBy` non sono visibili:

![Dopo l&#39;installazione del pacchetto](/help/sites-administering/assets/after_resized.png)

Per ulteriori informazioni, consulta le note sulla versione del pacchetto.

### Previeni il clickjacking {#prevent-clickjacking}

Per prevenire gli attacchi clickjacking, Adobe consiglia di configurare il server web in modo da fornire l’`X-FRAME-OPTIONS`intestazione HTTP impostata su `SAMEORIGIN`.

Per ulteriori informazioni sul clickjacking, consulta il [sito OWASP](https://www.owasp.org/index.php/Clickjacking).

### Assicurati Di Replicare Correttamente Le Chiavi Di Crittografia Quando Necessario {#make-sure-you-properly-replicate-encryption-keys-when-needed}

Alcune funzionalità AEM e alcuni schemi di autenticazione richiedono la replica delle chiavi di crittografia in tutte le istanze AEM.

Prima di procedere, la replica delle chiavi viene eseguita in modo diverso tra le versioni, poiché il modo in cui le chiavi vengono memorizzate è diverso tra la versione 6.3 e le versioni precedenti.

Per ulteriori informazioni, consulta di seguito.

#### Replica delle chiavi per AEM 6.3 {#replicating-keys-for-aem}

Mentre nelle versioni precedenti le chiavi di replica venivano memorizzate nell’archivio, a partire da AEM 6.3 vengono memorizzate nel file system.

Pertanto, per replicare le chiavi tra le istanze, copiale dall’istanza di origine nella posizione delle istanze di destinazione sul file system.

In particolare, devi effettuare le seguenti operazioni:

1. Accedere all’istanza dell’AEM, in genere un’istanza di authoring, che contiene il materiale chiave da copiare;
1. Individua il bundle com.adobe.granite.crypto.file nel file system locale. Ad esempio, in questo percorso:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`

   Il file `bundle.info` in ogni cartella identifica il nome del bundle.

1. Passa alla cartella dati. Ad esempio:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Copiare i file HMAC e master.
1. Quindi, vai all’istanza di destinazione in cui desideri duplicare la chiave HMAC e passa alla cartella dati. Ad esempio:

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Incolla i due file copiati in precedenza.
1. [Aggiornare il bundle di crittografia](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) se l&#39;istanza di destinazione è già in esecuzione.
1. Ripeti i passaggi precedenti per tutte le istanze a cui desideri replicare la chiave.

#### Replica delle chiavi per AEM 6.2 e versioni precedenti {#replicating-keys-for-aem-and-older-versions}

In AEM 6.2 e versioni precedenti, le chiavi vengono memorizzate nell&#39;archivio sotto il nodo `/etc/key`.

Il modo consigliato per replicare in modo sicuro le chiavi nelle istanze consiste nel replicare solo questo nodo. È possibile replicare in modo selettivo i nodi tramite CRXDE Lite:

1. Apri CRXDE Lite andando in *`https://&lt;serveraddress&gt;:4502/crx/de/index.jsp`*
1. Selezionare il nodo `/etc/key`.
1. Passare alla scheda **Replica**.
1. Premere il pulsante **Replica**.

### Eseguire un test di penetrazione {#perform-a-penetration-test}

L’Adobe consiglia di eseguire un test di penetrazione dell’infrastruttura AEM prima di procedere alla produzione.

### Best practice per lo sviluppo {#development-best-practices}

È fondamentale che i nuovi sviluppi seguano le [Best practice per la sicurezza](/help/sites-developing/security.md) per garantire che l&#39;ambiente AEM rimanga sicuro.
