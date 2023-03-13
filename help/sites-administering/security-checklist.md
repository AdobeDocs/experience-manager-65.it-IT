---
title: Elenco di controllo della sicurezza
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
source-git-commit: 7efe4a011d831c34f6aafd877654e8b41fec96e0
workflow-type: tm+mt
source-wordcount: '2889'
ht-degree: 3%

---

# Elenco di controllo della sicurezza {#security-checklist}

Questa sezione descrive i vari passaggi da seguire per garantire la sicurezza dell’installazione dell’AEM durante l’installazione. L’elenco di controllo deve essere applicato dall’alto verso il basso.

>[!NOTE]
>
>Sono inoltre disponibili ulteriori informazioni sulle minacce più pericolose per la sicurezza pubblicate da [Apri progetto di protezione applicazione Web (OWASP)](https://owasp.org/www-project-top-ten/).

>[!NOTE]
>
>Sono disponibili alcuni [considerazioni sulla sicurezza](/help/sites-developing/dev-guidelines-bestpractices.md#security-considerations) applicabile nella fase di sviluppo.

## Principali misure di sicurezza {#main-security-measures}

### Eseguire AEM in modalità pronta per la produzione {#run-aem-in-production-ready-mode}

Per ulteriori informazioni, consulta [Esecuzione di AEM in modalità pronta per la produzione](/help/sites-administering/production-ready.md).

### Abilita HTTPS per la sicurezza del livello di trasporto {#enable-https-for-transport-layer-security}

Per poter disporre di un’istanza protetta, è obbligatorio abilitare il livello di trasporto HTTPS sia sulle istanze di authoring che su quelle di pubblicazione.

>[!NOTE]
>
>Consulta la [Abilitazione di HTTP su SSL](/help/sites-administering/ssl-by-default.md) per ulteriori informazioni.

### Installare gli hotfix di sicurezza {#install-security-hotfixes}

Assicurati di aver installato la versione più recente [Hotfix di sicurezza forniti da Adobe](https://helpx.adobe.com/it/experience-manager/kb/aem63-available-hotfixes.html).

### Modificare le password predefinite per gli account amministratore di AEM e OSGi Console {#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts}

L&#39;Adobe consiglia vivamente di modificare la password per il privilegiato dopo l&#39;installazione [**AEM** `admin` account](#changing-the-aem-admin-password) su tutte le istanze.

Tali account includono:

* L&#39;AEM `admin` account

   Dopo aver modificato la password per l’account amministratore AEM, dovrai utilizzare la nuova password per accedere a CRX.

* Il `admin` password per la console Web OSGi

   Questa modifica verrà applicata anche all’account amministratore utilizzato per accedere alla console web, pertanto dovrai utilizzare la stessa password per accedere a tale account.

Questi due account utilizzano credenziali separate e disporre di password distinte e sicure per ciascuno è fondamentale per una distribuzione sicura.

#### Modifica della password amministratore AEM {#changing-the-aem-admin-password}

La password dell&#39;account amministratore dell&#39;AEM può essere modificata tramite [Operazioni Granite - Utenti](/help/sites-administering/granite-user-group-admin.md) console.

Qui puoi modificare il `admin` account e [cambiare la password](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user).

>[!NOTE]
>
>La modifica dell’account amministratore comporta anche la modifica dell’account della console web OSGi. Dopo aver modificato l’account amministratore, devi impostare l’account OSGi su un valore diverso.

#### Importanza della modifica della password della console Web OSGi {#importance-of-changing-the-osgi-web-console-password}

A parte l&#39;AEM `admin` account, se non si modifica la password predefinita per la password della console web OSGi, si possono verificare le seguenti situazioni:

* Esposizione del server con una password predefinita durante l&#39;avvio e l&#39;arresto (che può richiedere alcuni minuti per i server di grandi dimensioni);
* Esposizione del server quando l’archivio è inattivo/il bundle di riavvio e OSGI è in esecuzione.

Per ulteriori informazioni sulla modifica della password della console Web, consulta [Modifica della password amministratore per la console Web OSGi](/help/sites-administering/security-checklist.md#changing-the-osgi-web-console-admin-password) di seguito.

#### Modifica della password amministratore per la console Web OSGi {#changing-the-osgi-web-console-admin-password}

È inoltre necessario modificare la password utilizzata per accedere alla console Web. Questa operazione viene eseguita con un [Configurazione OSGI](/help/sites-deploying/configuring-osgi.md) per aggiornare le seguenti proprietà del **Console di gestione Apache Felix OSGi**:

* **Nome utente** e **Password**, le credenziali per accedere alla console di gestione web Apache Felix.
È necessario modificare la password *dopo* l’installazione iniziale per garantire la sicurezza dell’istanza.

Per effettuare questo collegamento:

>[!NOTE]
>
>Consulta [Configurazione OSGI](/help/sites-deploying/configuring-osgi.md) per informazioni dettagliate sulla configurazione delle impostazioni OSGi.

1. Utilizzo di **Strumenti**, **Operazioni** aprire il menu **Console web** e passare alla **Configurazione** sezione.
Ad esempio, in corrispondenza di `<server>:<port>/system/console/configMgr`.
1. Passa alla voce e aprila per **Console di gestione Apache Felix OSGi**.
1. Modificare il **nome utente** e **password**.

   ![chlimage_1-3](assets/chlimage_1-3.png)

1. Seleziona **Salva**.

### Implementare un gestore degli errori personalizzato {#implement-custom-error-handler}

L’Adobe consiglia di definire pagine personalizzate del gestore degli errori, in particolare per i codici di risposta HTTP 404 e 500, al fine di evitare la divulgazione di informazioni.

>[!NOTE]
>
>Consulta [Come posso creare script personalizzati o gestori di errori](https://helpx.adobe.com/experience-manager/kb/CustomErrorHandling.html) articolo della knowledge base per ulteriori dettagli.

### Elenco di controllo completo della sicurezza di Dispatcher {#complete-dispatcher-security-checklist}

AEM Dispatcher è un elemento fondamentale dell’infrastruttura. Adobe consiglia vivamente di completare il [elenco di controllo della sicurezza di dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/security-checklist.html?lang=it#getting-started).

>[!CAUTION]
>
>Con Dispatcher devi disattivare il selettore &quot;.form&quot;.

## Passaggi della verifica {#verification-steps}

### Configurare gli utenti di replica e trasporto {#configure-replication-and-transport-users}

Un&#39;installazione standard di AEM specifica `admin` come utente per le credenziali di trasporto all’interno del predefinito [agenti di replica](/help/sites-deploying/replication.md). Inoltre, l’utente amministratore viene utilizzato per determinare l’origine della replica sul sistema di authoring.

Per motivi di sicurezza, entrambi dovrebbero essere modificati per riflettere il caso d’uso specifico in questione, tenendo presenti i due aspetti seguenti:

* Il **utente trasporto** non deve essere l’utente amministratore. Piuttosto, imposta un utente sul sistema di pubblicazione che dispone solo dei diritti di accesso alle parti pertinenti del sistema di pubblicazione e utilizza le credenziali di tale utente per il trasporto.

   Puoi iniziare dall’utente di ricezione della replica in bundle e configurare i diritti di accesso di questo utente in base alla tua situazione

* Il **utente di replica** o **ID utente agente** inoltre, non deve essere l’utente amministratore, ma un utente in grado di visualizzare solo il contenuto che deve essere replicato. L’utente di replica viene utilizzato per raccogliere il contenuto da replicare sul sistema di authoring prima che venga inviato all’editore.

### Verifica i controlli di integrità della sicurezza del dashboard operazioni {#check-the-operations-dashboard-security-health-checks}

AEM6 introduce il nuovo dashboard delle operazioni, volto ad aiutare gli operatori di sistema a risolvere i problemi e a monitorare lo stato di un’istanza.

La dashboard viene inoltre fornita con una raccolta di controlli di integrità della sicurezza. Si consiglia di controllare lo stato di tutti i controlli di integrità della sicurezza prima di andare &quot;live&quot; con l’istanza di produzione. Per ulteriori informazioni, consultare [Documentazione del dashboard operazioni](/help/sites-administering/operations-dashboard.md).

### Controlla se il contenuto di esempio è presente {#check-if-example-content-is-present}

Tutti i contenuti e gli utenti di esempio (ad esempio il progetto e i relativi componenti) devono essere disinstallati ed eliminati completamente in un Geometrixx produttivo prima di renderlo accessibile al pubblico.

>[!NOTE]
>
>Le applicazioni We.Retail di esempio vengono rimosse se questa istanza è in esecuzione in [Modalità pronta per la produzione](/help/sites-administering/production-ready.md). In caso contrario, puoi disinstallare il contenuto di esempio da Gestione pacchetti, quindi cercare e disinstallare tutti i pacchetti We.Retail. Per ulteriori informazioni, consulta [Utilizzare I Pacchetti](package-manager.md).

### Verifica se i bundle di sviluppo CRX sono presenti {#check-if-the-crx-development-bundles-are-present}

Prima di renderli accessibili, questi bundle OSGi di sviluppo devono essere disinstallati sia sui sistemi produttivi di authoring che su quelli di pubblicazione.

* Adobe di supporto per CRXDE (com.adobe.granite.crxde-support)
* Adobe Granite CRX Explorer (com.adobe.granite.crx-explorer)
* Adobe Granite CRXDE Lite (com.adobe.granite.crxde-lite)

### Verifica se il bundle di sviluppo Sling è presente {#check-if-the-sling-development-bundle-is-present}

Il [Strumenti per sviluppatori AEM per Eclipse](/help/sites-developing/aem-eclipse.md) implementa l’installazione del supporto per gli strumenti Apache Sling (org.apache.sling.tooling.support.install).

Prima di renderli accessibili, questo bundle OSGi deve essere disinstallato sui sistemi produttivi sia di authoring che di pubblicazione.

### Protect contro il rischio di false richieste tra siti diversi {#protect-against-cross-site-request-forgery}

#### Il framework di protezione CSRF {#the-csrf-protection-framework}

L’AEM 6.1 viene fornito con un meccanismo che aiuta a proteggere da attacchi di tipo Cross-Site Request Forgery, chiamato **Framework di protezione CSRF**. Per ulteriori informazioni su come utilizzarlo, consulta [documentazione](/help/sites-developing/csrf-protection.md).

#### Il filtro Sling Referrer {#the-sling-referrer-filter}

Per risolvere i problemi di sicurezza noti con Cross-Site Request Forgery (CSRF) in CRX WebDAV e Apache Sling è necessario aggiungere configurazioni per il filtro Referrer per poterlo utilizzare.

Il servizio di filtro dei referenti è un servizio OSGi che consente di configurare:

* quali metodi http filtrare
* se è consentita un’intestazione referente vuota
* e un elenco di server da consentire in aggiunta all’host del server.

   Per impostazione predefinita, tutte le varianti di localhost e i nomi host correnti a cui è associato il server sono inclusi nell&#39;elenco.

Per configurare il servizio filtro referenti:

1. Apri la console Apache Felix (**Configurazioni**) in:

   `https://<server>:<port_number>/system/console/configMgr`

1. Accedi come `admin`.
1. In **Configurazioni** , selezionare:

   `Apache Sling Referrer Filter`

1. In `Allow Hosts` , immettere tutti gli host consentiti come referrer. Ogni voce deve essere del modulo

   &lt;protocol>://&lt;server>:&lt;port>

   Esempio:

   * `https://allowed.server:80` consente tutte le richieste provenienti da questo server con la porta specificata.
   * Se desideri anche consentire le richieste https, devi immettere una seconda riga.
   * Se consenti tutte le porte da tale server, puoi utilizzare `0` come numero di porta.

1. Controlla la `Allow Empty` , se desideri consentire intestazioni referente vuote/mancanti.

   >[!CAUTION]
   >
   >Si consiglia di fornire un referente mentre si utilizzano strumenti della riga di comando come `cURL` invece di consentire un valore vuoto in quanto potrebbe esporre il sistema ad attacchi CSRF.

1. Modifica i metodi da utilizzare per i controlli con `Filter Methods` campo.

1. Clic **Salva** per salvare le modifiche.

### Impostazioni OSGI {#osgi-settings}

Alcune impostazioni OSGI sono impostate per impostazione predefinita per consentire un debug più semplice dell’applicazione. Queste devono essere modificate sulle istanze produttive di pubblicazione e authoring per evitare che le informazioni interne trapelino al pubblico.

>[!NOTE]
>
>Tutte le impostazioni seguenti a eccezione di **Filtro di debug Day CQ WCM** sono automaticamente coperti dal [Modalità pronta per la produzione](/help/sites-administering/production-ready.md). Per questo motivo, consigliamo di rivedere tutte le impostazioni prima di distribuire l’istanza in un ambiente produttivo.

Per ciascuno dei seguenti servizi è necessario modificare le impostazioni specificate:

* [Adobe Granite HTML Library Manager](/help/sites-deploying/osgi-configuration-settings.md#day-cq-html-library-manager):

   * abilita **Minimizza** (per rimuovere i caratteri CRLF e gli spazi vuoti).
   * abilita **Gzip** (per consentire l’estrazione e l’accesso ai file con una sola richiesta).
   * disable **Debug**
   * disable **Tempistica**

* [Filtro di debug Day CQ WCM](/help/sites-deploying/osgi-configuration-settings.md#day-cq-wcm-debug-filter):

   * deseleziona **Abilita**

* [Filtro WCM Day CQ](/help/sites-deploying/osgi-configuration-settings.md):

   * solo in pubblicazione, imposta **Modalità WCM** a &quot;disabilitato&quot;

* [Gestore script Java Apache Sling](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-javascript-handler):

   * disable **Genera informazioni di debug**

* [Gestore script Apache Sling JSP](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-jsp-script-handler):

   * disable **Genera informazioni di debug**
   * disable **Contenuto mappato**

Per maggiori dettagli vedi [Impostazioni configurazione OSGi](/help/sites-deploying/osgi-configuration-settings.md).

Quando si lavora con l’AEM, esistono diversi metodi per gestire le impostazioni di configurazione per tali servizi; vedi [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per ulteriori dettagli e le pratiche consigliate.

## Letture ulteriori {#further-readings}

### Mitigare gli attacchi Denial of Service (DoS) {#mitigate-denial-of-service-dos-attacks}

Un attacco Denial of Service (DoS) è un tentativo di rendere la risorsa di un computer indisponibile per gli utenti a cui è destinata. Ciò avviene spesso sovraccaricando la risorsa, ad esempio:

* Con una marea di richieste da una fonte esterna.
* Con una richiesta di informazioni superiore a quelle che il sistema è in grado di fornire.

   Ad esempio, una rappresentazione JSON dell’intero archivio.

* Richiedendo una pagina di contenuto con un numero illimitato di URL, l’URL può includere un handle, alcuni selettori, un’estensione e un suffisso, ciascuno dei quali può essere modificato.

   Ad esempio: `.../en.html` può essere richiesto anche come:

   * `.../en.ExtensionDosAttack`
   * `.../en.SelectorDosAttack.html`
   * `.../en.html/SuffixDosAttack`

   Tutte le varianti valide (ad es. restituiscono un `200` e sono configurati per essere memorizzati in cache) verranno memorizzati in cache da Dispatcher, portando a un file system completo e a nessun servizio per ulteriori richieste.

Ci sono molti punti di configurazione per prevenire questi attacchi, qui si discute solo di quelli direttamente legati all&#39;AEM.

**Configurazione di Sling per impedire i DoS**

Sling è *incentrato sui contenuti*. Ciò significa che l’elaborazione si concentra sul contenuto, in quanto ogni richiesta (HTTP) è mappata sul contenuto sotto forma di risorsa JCR (un nodo dell’archivio):

* La prima destinazione è la risorsa (nodo JCR) contenente il contenuto.
* In secondo luogo, il renderer, o script, si trova dalle proprietà della risorsa in combinazione con alcune parti della richiesta (ad esempio, selettori e/o estensione).

>[!NOTE]
>
>Questo argomento è trattato più dettagliatamente in [Elaborazione richiesta Sling](/help/sites-developing/the-basics.md#sling-request-processing).

Questo approccio rende Sling molto potente e molto flessibile, ma come sempre è la flessibilità che deve essere gestita con attenzione.

Per evitare l&#39;uso improprio del DoS:

1. Incorpora i controlli a livello di applicazione; a causa del numero di varianti possibili, non è possibile impostare una configurazione predefinita.

   Nell’applicazione dovresti:

   * Controlla i selettori nell’applicazione, in modo da *solo* distribuisci i selettori espliciti necessari e restituisce `404` per tutti gli altri.
   * Impedisci l’output di un numero illimitato di nodi di contenuto.

1. Controlla la configurazione dei renderer predefiniti, che può rappresentare un’area problematica.

   * In particolare, il renderer JSON che può trasmettere la struttura ad albero su più livelli.

      Ad esempio:

      `http://localhost:4502/.json`

      potrebbe scaricare l’intero archivio in una rappresentazione JSON. Ciò causerebbe problemi significativi al server. Per questo motivo Sling imposta un limite al numero massimo di risultati. Per limitare la profondità del rendering JSON, puoi impostare il valore per:

      **Max risultati JSON** ( `json.maximumresults`)

      nella configurazione per [Apache Sling GET Servlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet). Quando questo limite viene superato, il rendering verrà compresso. Il valore predefinito per Sling in AEM è `1000`.

   * Come misura preventiva, disattiva gli altri renderer predefiniti (HTML, testo normale, XML). Di nuovo configurando [Apache Sling GET Servlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet).
   >[!CAUTION]
   >
   >Non disabilitare il renderer JSON, necessario per il normale funzionamento dell’AEM.

1. Utilizza un firewall per filtrare l’accesso all’istanza.

   * L’utilizzo di un firewall a livello di sistema operativo è necessario per filtrare l’accesso ai punti dell’istanza che, se lasciati non protetti, potrebbero causare attacchi Denial of Service.

**Attenuare i DoS causati dall&#39;utilizzo dei selettori di moduli**

>[!NOTE]
>
>Questa mitigazione deve essere eseguita solo sugli ambienti AEM che non utilizzano Forms.

Poiché l&#39;AEM non fornisce indici predefiniti per `FormChooserServlet`, l’utilizzo di selettori di moduli nelle query attiverà un costoso attraversamento dell’archivio, solitamente bloccando l’istanza AEM. I selettori di moduli possono essere rilevati dalla presenza di **&amp;ast;.form.&amp;ast;** stringa nelle query.

Per ovviare a questo problema, effettua le seguenti operazioni:

1. Passa alla console Web puntando il browser su *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*

1. Cerca **Servlet selettore modulo WCM Day CQ**
1. Dopo aver fatto clic sulla voce, disattiva la **Ricerca avanzata richiesta** nella finestra seguente.

1. Fai clic su **Salva**.

**Attenuazione rispetto ai DoS causati dal servlet di download delle risorse**

Il servlet di download delle risorse predefinito consente agli utenti autenticati di inviare richieste di download simultanee di dimensioni arbitrarie per creare file ZIP delle risorse. La creazione di grandi archivi ZIP può sovraccaricare il server e la rete. Per attenuare un potenziale rischio Denial of Service (DoS) causato da questo comportamento, `AssetDownloadServlet` Il componente OSGi è disabilitato per impostazione predefinita il [!DNL Experience Manager] istanza di pubblicazione. È abilitato su [!DNL Experience Manager] per impostazione predefinita.

Se non hai bisogno della funzionalità di download, disattiva il servlet per le distribuzioni di authoring e pubblicazione. Se la configurazione richiede che la funzionalità di download delle risorse sia abilitata, consulta [questo articolo](/help/assets/download-assets-from-aem.md) per ulteriori informazioni. Inoltre, puoi definire un limite massimo di download supportato dalla tua implementazione.

### Disattiva WebDAV {#disable-webdav}

WebDAV deve essere disattivato sia nell&#39;ambiente di authoring che in quello di pubblicazione. Per farlo, arresta i bundle OSGi appropriati.

1. Connetti a **Console di gestione Felix** esecuzione:

   `https://<*host*>:<*port*>/system/console`

   Esempio `http://localhost:4503/system/console/bundles`.

1. Nell’elenco dei bundle, individua il bundle denominato:

   `Apache Sling Simple WebDAV Access to repositories (org.apache.sling.jcr.webdav)`

1. Fai clic sul pulsante Interrompi (nella colonna Azioni) per arrestare questo bundle.

1. Sempre nell’elenco dei bundle, trova il bundle denominato:

   `Apache Sling DavEx Access to repositories (org.apache.sling.jcr.davex)`

1. Fai clic sul pulsante Interrompi per arrestare questo bundle.

   >[!NOTE]
   >
   >Non è necessario riavviare l’AEM.

### Verifica Di Non Divulgare Informazioni Personalmente Identificabili Nel Percorso Home Degli Utenti {#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path}

È importante proteggere gli utenti accertandosi di non esporre informazioni personali identificabili nel percorso principale degli utenti dell’archivio.

A partire da AEM 6.1, il modo in cui i nomi dei nodi ID degli utenti (noti anche come autorizzabili) vengono memorizzati è cambiato con una nuova implementazione della `AuthorizableNodeName` di rete. La nuova interfaccia non esporrà più l’ID utente nel nome del nodo, ma genererà invece un nome casuale.

Non è necessario eseguire alcuna configurazione per abilitarla, in quanto ora questo è il modo predefinito per generare ID autorizzabili nell’AEM.

Anche se non consigliato, puoi disattivarlo nel caso sia necessaria la vecchia implementazione per compatibilità con le applicazioni esistenti. A tale scopo, è necessario:

1. Vai alla console web e rimuovi la voce** org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName** dalla proprietà **requiredServicePids** in **Apache Jackrabbit Oak SecurityProvider**.

   Puoi anche trovare il provider della sicurezza Oak cercando **org.apache.jackrabbit.oak.security.internal.SecurityProviderRegistration** PID nelle configurazioni OSGi.

1. Elimina **Nome nodo casuale autorizzabile Apache Jackrabbit Oak** Configurazione OSGi dalla console Web.

   Per una ricerca più semplice, tieni presente che il PID per questa configurazione è **org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**.

>[!NOTE]
>
>Per ulteriori informazioni, consulta la documentazione di Oak su [Generazione nome nodo autorizzabile](https://jackrabbit.apache.org/oak/docs/security/user/authorizablenodename.html).

### Previeni il clickjacking {#prevent-clickjacking}

Per prevenire il clickjacking, ti consigliamo di configurare il server web per fornire l’intestazione HTTP `X-FRAME-OPTIONS` impostata su `SAMEORIGIN`.

Per ulteriori [informazioni sul clickjacking, vedi il sito OWASP](https://www.owasp.org/index.php/Clickjacking).

### Assicurati Di Replicare Correttamente Le Chiavi Di Crittografia Quando Necessario {#make-sure-you-properly-replicate-encryption-keys-when-needed}

Alcune funzionalità AEM e alcuni schemi di autenticazione richiedono la replica delle chiavi di crittografia in tutte le istanze AEM.

Prima di procedere, tieni presente che la replica delle chiavi viene eseguita in modo diverso tra le versioni, in quanto il modo in cui vengono memorizzate le chiavi varia tra la versione 6.3 e quelle precedenti.

Per ulteriori informazioni, consulta di seguito.

#### Replica delle chiavi per AEM 6.3 {#replicating-keys-for-aem}

Mentre nelle versioni precedenti le chiavi di replica venivano memorizzate nell’archivio, a partire da AEM 6.3 vengono memorizzate nel file system.

Pertanto, per replicare le chiavi in più istanze, è necessario copiarle dall’istanza di origine alla posizione delle istanze di destinazione nel file system.

In particolare, devi:

1. Accedere all’istanza AEM, in genere un’istanza Autore, che contiene il materiale chiave da copiare;
1. Individua il bundle com.adobe.granite.crypto.file nel file system locale. Ad esempio, in questo percorso:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`

   Il `bundle.info` all’interno di ogni cartella identificherà il nome del bundle.

1. Passa alla cartella dati. Esempio:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Copiare i file HMAC e master.
1. Quindi, vai all’istanza di destinazione in cui desideri duplicare la chiave HMAC e passa alla cartella dati. Esempio:

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Incolla i due file copiati in precedenza.
1. [Aggiorna il pacchetto di crittografia](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) se l’istanza di destinazione è già in esecuzione.
1. Ripeti i passaggi precedenti per tutte le istanze in cui desideri replicare la chiave.

>[!NOTE]
>
>Puoi ripristinare il metodo di memorizzazione delle chiavi precedente alla 6.3 aggiungendo il seguente parametro alla prima installazione dell’AEM:
>
>`-Dcom.adobe.granite.crypto.file.disable=true`

#### Replica delle chiavi per AEM 6.2 e versioni precedenti {#replicating-keys-for-aem-and-older-versions}

In AEM 6.2 e versioni precedenti, le chiavi sono memorizzate nell’archivio sotto `/etc/key` nodo.

Il modo consigliato per replicare in modo sicuro le chiavi nelle istanze consiste nel replicare solo questo nodo. È possibile replicare in modo selettivo i nodi tramite CRXDE Lite:

1. Apri CRXDE Lite da *https://&lt;serveraddress>:4502/crx/de/index.jsp*
1. Seleziona la `/etc/key` nodo.
1. Vai a **Replica** scheda.
1. Premere il tasto **Replica** pulsante.

### Esegui un test di penetrazione {#perform-a-penetration-test}

Adobe consiglia vivamente di eseguire un test di penetrazione dell’infrastruttura AEM prima di procedere alla produzione.

### Best practice per lo sviluppo {#development-best-practices}

È fondamentale che i nuovi sviluppi seguano [Best practice per la sicurezza](/help/sites-developing/security.md) per garantire la sicurezza dell’ambiente AEM.
