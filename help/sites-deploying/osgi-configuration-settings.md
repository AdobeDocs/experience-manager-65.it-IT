---
title: Impostazioni di configurazione OSGi
seo-title: Impostazioni di configurazione OSGi
description: Questo articolo descrive le impostazioni di configurazione OSGi (elencate in base al bundle) rilevanti per l’implementazione del progetto. L'elenco funge da orientamento e non è esaustivo.
seo-description: Questo articolo descrive le impostazioni di configurazione OSGi (elencate in base al bundle) rilevanti per l’implementazione del progetto. L'elenco funge da orientamento e non è esaustivo.
uuid: 192d3287-ec99-403b-bab0-45721e4e3abd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: ed3a858c-7a43-4515-a2ff-43ca465c7d7d
docset: aem65
translation-type: tm+mt
source-git-commit: 474fc122f557f32d34fddd9d35a113431f6ce491
workflow-type: tm+mt
source-wordcount: '3805'
ht-degree: 0%

---


# Impostazioni di configurazione OSGi{#osgi-configuration-settings}

[](https://www.osgi.org/) OSGiè un elemento fondamentale nello stack tecnologico di AEM. Viene utilizzato per controllare i bundle compositi di AEM e la loro configurazione.

OSGi &quot;*fornisce le primitive standardizzate che consentono di creare applicazioni da componenti piccoli, riutilizzabili e collaborativi. Questi componenti possono essere composti in un&#39;applicazione e distribuiti*&quot;.

In questo modo è possibile gestire facilmente i bundle in quanto possono essere arrestati, installati e avviati individualmente. Le interdipendenze vengono gestite automaticamente. Ciascun componente OSGi (vedere la [specifica OSGi](https://www.osgi.org/Specifications/HomePage)) è contenuto in uno dei vari bundle. Quando lavorate con AEM esistono diversi metodi per gestire le impostazioni di configurazione per tali bundle; per ulteriori informazioni e procedure consigliate, vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md).

Le seguenti impostazioni di configurazione OSGi (elencate in base al bundle) sono rilevanti per l’implementazione del progetto. Non tutte le impostazioni elencate devono essere regolate, alcune sono menzionate per aiutarvi a capire come AEM funziona.

>[!CAUTION]
>
>L&#39;elenco è inteso come orientamento e non è esaustivo. Non tutti i bundle sono elencati, né tutti i parametri per alcuni dei bundle.
>
>La configurazione necessaria varia da progetto a progetto.
>
>Consultate la console Web per i valori utilizzati e per informazioni dettagliate sui parametri.

>[!NOTE]
>
>Lo strumento di configurazione OSGi Diff, che fa parte di [AEM Tools](https://helpx.adobe.com/experience-manager/kb/tools/aem-tools.html), può essere utilizzato per elencare le configurazioni OSGi predefinite.

>[!NOTE]
>
>Possono essere necessari ulteriori pacchetti per aree specifiche di funzionalità all&#39;interno di AEM. In questi casi, i dettagli di configurazione sono disponibili sulla pagina relativa alla funzionalità appropriata.

**AEM** Listener eventi di replicaConfigure:

* La **Modalità di esecuzione**, in cui gli eventi di replica verranno distribuiti ai listener. Ad esempio, se definito come autore, questo è il sistema che &quot;avvia&quot; la replica.

* È necessario aggiungere la modalità di esecuzione **publish** se il codice del progetto elabora eventi di replica (replica inversa) in un ambiente di pubblicazione. Ad esempio, quando il dispatcher viene utilizzato per cancellare dall’ambiente di pubblicazione o quando si verifica la replica standard ad altre istanze di pubblicazione.

**AEM repository modifica** listenerConfigure:

* Le **Percorsi**, posizioni in cui ascoltare gli eventi del repository pronti per la distribuzione.

**CRX Sling Client** RepositoryConfigurare l&#39;accesso all&#39;archivio del contenuto sottostante.

* La **Password amministratore** deve essere modificata dopo l&#39;installazione per garantire la [protezione](/help/sites-administering/security-checklist.md) dell&#39;istanza.
* Le altre modifiche non dovrebbero essere necessarie e occorre prestare attenzione in quanto possono influenzare l&#39;accesso al repository.

**Wiki Mail** ServiceConfigura le impostazioni e-mail per le e-mail inviate da un wiki.

**Apache Felix OSGi Management** ConsoleConfigura:

* **Plugins**, gli elementi di navigazione principali (plug-in di console) per essere disponibili nelle voci di menu di livello principale  **Apache Felix Web Management** Consoleas. Disattivate tutte le risorse non necessarie, poiché ciascuna richiede spazio e risorse.

>[!CAUTION]
>
>Assicuratevi di configurare quanto segue:
>
>**Nome utente** e  **password**, le credenziali per accedere alla console di gestione Web Apache Felix stessa.
>La password deve essere modificata dopo l&#39;installazione iniziale per garantire la [sicurezza](/help/sites-administering/security-checklist.md) dell&#39;istanza.

>[!NOTE]
>
>Questa configurazione deve essere eseguita utilizzando la console Felix come necessario all’avvio, prima che la directory archivio sia disponibile.

**Apache Sling Custom Request Data** LoggerConfigure:

* **Logger** Name e  **Log** Forconfigurano la posizione e il formato della registrazione delle richieste e degli accessi (impostazione predefinita:  `request.log`). Questo file di registro è essenziale per analizzare le prestazioni o le funzionalità di debug relative alla catena Web.
Questo è associato al [Registratore di richieste Apache Sling](#apacheslingrequestlogger).

Per ulteriori informazioni, vedere [AEM Logging](/help/sites-deploying/configure-logging.md) e [Sling Logging](https://sling.apache.org/site/logging.html).

**Apache Sling Eventing Thread** PoolConfigure:

* **Dimensione** pool minima e  **Dimensione** pool massima, dimensione del pool utilizzato per contenere i thread dell&#39;evento.

* **Dimensione** coda, dimensione massima della coda di thread se il pool è esaurito.
Il valore consigliato è `-1` in quanto imposta la coda su illimitato; se viene fissato un limite, le perdite potrebbero verificarsi in caso di superamento.

* La modifica di tali impostazioni può facilitare le prestazioni in situazioni con un elevato numero di eventi; ad esempio, utilizzo intensivo AEM DAM o Workflow.
* I valori specifici dello scenario devono essere determinati utilizzando i test.
* Queste impostazioni possono influire sulle prestazioni dell&#39;istanza, pertanto non devono essere modificate senza motivo e con la dovuta considerazione.

**Apache Sling GET** ServletConfigura alcuni aspetti del rendering:

* **Auto** Indexto per abilitare/disabilitare il rendering della directory per la navigazione.
* **Abilitare**  (o disabilitare) le rappresentazioni predefinite, ad esempio  **HMTL**,  **Testo** normale,  **** JSONo  **XML**.
Non devi disabilitare JSON.

>[!NOTE]
>
>Questa impostazione viene configurata automaticamente per le istanze di produzione se si esegue AEM in [Modalità pronta produzione](/help/sites-administering/production-ready.md).

**Apache Sling Java Script** HandlerConfigura le impostazioni per la compilazione dei file .java come script (servlet).

Alcune impostazioni possono influire sulle prestazioni, che dovrebbero essere disattivate ove possibile, in particolare per un&#39;istanza di produzione.

* S **VM di origine** e **VM di destinazione** definiscono la versione JDK come utilizzata come JVM di runtime

* per le istanze di produzione:

   * disabilitare **Generate Debug Info**

**Apache Sling JCR** InstallerQuesti parametri probabilmente non richiedono la configurazione, ma possono essere utili per sapere quando si sviluppano o si eseguono operazioni di debug. Ad esempio, le cartelle di installazione possono essere utili per archiviare o creare un pacchetto.

* **Nome delle cartelle di installazione** regespandere la gerarchia  **Massima profondità delle cartelle**  di installazione- specificare dove e a quale profondità vengono cercate le risorse da installare nelle cartelle del repository. Quando viene utilizzato un carattere jolly (come in .*/install) verranno cercate tutte le corrispondenze appropriate, ad esempio `/libs/sling/install` e `/libs/cq/core/install`.

* **Percorso** di ricerca, elenco di percorsi che jcrinstall cerca le risorse da installare, insieme a un numero che indica il fattore di ponderazione per tale percorso.

**Apache Sling Job Event** HandlerConfigura i parametri per la gestione della programmazione dei processi:

* **Intervallo** tentativi,  **tentativi** massimi,  **massimi processi** paralleli, tempo **di attesa** riconoscimento, tra gli altri.

* La modifica di tali impostazioni può migliorare le prestazioni in scenari con un elevato numero di processi; ad esempio, l&#39;utilizzo intensivo di AEM DAM e Flussi di lavoro.
* I valori specifici dello scenario devono essere determinati utilizzando i test.
* Non modificate queste impostazioni senza motivo, ma modificate solo dopo aver tenuto in debita considerazione.

**Apache Sling JSP Script** HandlerConfigurare le impostazioni relative alle prestazioni per il gestore di script JSP. Per migliorare le prestazioni è necessario disattivare il più possibile.

In particolare per le istanze di produzione:

* disabilitare **Generate Debug Info**
* disattiva **Mantieni Java generato**
* disattiva **Contenuto mappato**
* disattiva **Visualizza frammenti di origine**

>[!NOTE]
>
>Questa impostazione viene configurata automaticamente per le istanze di produzione se si esegue AEM in [Modalità pronta produzione](/help/sites-administering/production-ready.md).

**Apache Sling Logging** ConfigurationConfigure:

* **Registrare** Leveland  **Log File**, per definire la posizione e il livello di registro della configurazione di registrazione centrale (error.log). Il livello può essere impostato su uno dei valori `DEBUG`, `INFO`, `WARN`, `ERROR` e `FATAL`.

* **Numero di** file di registro e  **soglia file di registro** per definire la dimensione e la rotazione della versione del file di registro.

* **I** pattern dei messaggi definiscono il formato dei messaggi di registro.

Per ulteriori informazioni, vedere [AEM Logging](/help/sites-deploying/configure-logging.md#global-logging) e [Sling Logging](https://sling.apache.org/site/logging.html).

**Configurazione Del Registratore Di Registrazione Apache Sling (Configurazione Di Fabbrica)** Configurare:

* **Livello** di registro,  **File** di registro e  **Messaggio** Forper definire i dettagli del file di registro e dei messaggi.

* **** Loggerto per definire la categoria; ad esempio, solo log per com.day.cq.

* Utilizzando **Configurazioni fabbrica**, è possibile aggiungere un numero qualsiasi di configurazioni aggiuntive per soddisfare i vari livelli di registro e le categorie necessarie.
* Tali configurazioni sono utili durante lo sviluppo; ad esempio, per registrare i messaggi TRACE per un servizio specifico in un file di registro specifico.
* Tali configurazioni sono utili in un ambiente di produzione; ad esempio, per avere messaggi su un servizio specifico registrato in un singolo file di registro per un monitoraggio più semplice.

Per ulteriori informazioni, vedere [AEM Logging](/help/sites-deploying/configure-logging.md) e [Sling Logging](https://sling.apache.org/site/logging.html).

**Configurazione Del Registratore Di Registrazione Apache Sling (Configurazione Di Fabbrica)** Configurare:

* **File di registro per definire** l’esistenza di un file di registro.
* **Numero di** file di registro per definire la rotazione della versione.

* Il writer può essere utilizzato da una configurazione **Apache Sling Logging Logging Logger Configuration**.

* Tali configurazioni sono utili durante lo sviluppo; ad esempio, per registrare i messaggi TRACE per un servizio specifico in un file di registro specifico.
* Tali configurazioni sono utili in un ambiente di produzione; ad esempio, per avere messaggi su un servizio specifico registrato in un singolo file di registro per un monitoraggio più semplice.

Per ulteriori informazioni, vedere [AEM Logging](/help/sites-deploying/configure-logging.md) e [Sling Logging](https://sling.apache.org/site/logging.html).

**Apache Sling Main** ServletConfigure:

* **Numero di chiamate per** richiesta e  **profondità** di ricorsione per proteggere il sistema da infinite chiamate di script e ricorsività.

**Apache Sling MIME Type** ServiceConfigure:

* **Tipi MIME** da aggiungere al sistema quelli richiesti dal progetto. Questo consente a una richiesta `GET` su un file di impostare l&#39;intestazione del tipo di contenuto corretta per il collegamento del tipo di file e dell&#39;applicazione.

**Apache Sling Referrer** FilterPer risolvere problemi noti di sicurezza con CSRF (Cross-Site Request Forgery) in CRX WebDAV e Apache Sling è necessario configurare il filtro Referrer.

Il servizio filtro di riferimento è un servizio OSGi che consente di configurare:

* quali metodi http devono essere filtrati
* se è consentita un&#39;intestazione di referente vuota
* e un elenco di server da consentire oltre all&#39;host del server.

Per ulteriori informazioni, vedere l&#39; [Elenco di controllo per la protezione - Problemi con la contraffazione delle richieste tra siti](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery).

>[!NOTE]
>
>Il filtro di riferimento Apache Sling dipende dall&#39;installazione di un pacchetto di correzione rapida.

**Apache Sling Request** LoggerConfigure:

* vari parametri per definire il modo in cui vengono registrate le richieste.
* **Per attivare o disattivare l’opzione Richiedi registro**.

* **Abilita registro** di accesso per abilitare o disabilitare.

Questo è associato al [Apache Sling Custom Request Data Logger](#apacheslingcustomizablerequestdatalogger).

Per ulteriori informazioni, vedere [AEM Logging](/help/sites-deploying/configure-logging.md) e [Sling Logging](https://sling.apache.org/site/logging.html).

**Apache Sling Resource Resolver** FactoryConfigurare gli aspetti centrali della risoluzione delle risorse Sling:

* **Percorso** di ricerca delle risorse, aggiungere eventuali percorsi specifici del progetto (ma non rimuovere  `/libs` o  `/apps`).

* **URL virtuali** per definire le mappature degli URL personalizzati.

* **Mappatura URL** per definire eventuali alias; ad esempio da  `/content` a  `/`.

* **Posizione** mappatura, la configurazione mappatore esternalizzata in  `/etc/map`.

* Utilizzare l&#39;installazione locale (ad esempio, utilizzare `https://localhost:4502/system/console/jcrresolver`) per determinare quale Resource Resolver è attivo.

Per ulteriori informazioni, consulta: [https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution).

>[!CAUTION]
>
>In particolare queste opzioni devono essere configurate nella directory archivio.
>
>In caso contrario, le modifiche apportate a **Mappature URL** mediante la console Felix potrebbero essere sovrascritte da AEM all&#39;avvio successivo.

**Risolutore Servlet/Script Apache Sling e** Gestore erroriSling Servlet e Script Resolver dispone di più attività:

1. Viene utilizzato come `ServletResolver` per selezionare il Servlet o lo Script da chiamare per gestire la richiesta.

1. Funziona come `SlingScriptResolver`.

1. Gestisce la gestione degli errori implementando l&#39;interfaccia `ErrorHandler` utilizzando lo stesso algoritmo per selezionare i servlet e gli script di gestione degli errori utilizzato per risolvere i servlet e gli script di elaborazione delle richieste.

È possibile impostare diversi parametri, tra cui:

* **I** percorsi di esecuzione elencano i percorsi per la ricerca di script eseguibili; configurando percorsi specifici è possibile limitare gli script che è possibile eseguire. Se non è configurato alcun percorso, viene utilizzato il valore predefinito ( `/` = root), che consente l&#39;esecuzione di tutti gli script.
Se un valore di percorso configurato termina con una barra, viene eseguita la ricerca nell&#39;intero sottoalbero. Senza una barra finale di questo tipo, lo script verrà eseguito solo se si tratta di una corrispondenza esatta.

* **Utente**  script: questa proprietà facoltativa può specificare l&#39;account utente dell&#39;archivio utilizzato per leggere gli script. Se non viene specificato alcun account, per impostazione predefinita viene utilizzato l&#39;utente `admin`.

* **** Estensioni predefinite: elenco di estensioni per le quali verrà utilizzato il comportamento predefinito. Questo significa che l&#39;ultimo segmento del percorso del tipo di risorsa può essere utilizzato come nome di script.

**Day Commons GFX Font** HelperDurante il rendering di elementi grafici è possibile utilizzare DrawText per incorporare testo. Per questo è anche possibile installare i font personalizzati:

* Definire il **Percorso font** da ricercare per i font specifici del progetto.
Esempio, `/apps/myapp/fonts`.

**Configurazione proxy** dei componenti Apache HTTPConfigurazione proxy per tutto il codice che utilizza il client Apache HTTP, utilizzata quando viene creato un HTTP; ad esempio durante la replica.

Quando create una nuova configurazione, non apportate modifiche alla configurazione di fabbrica, ma create una nuova configurazione di fabbrica per questo componente utilizzando il gestore di configurazione disponibile qui: **https://localhost:4502/system/console/configMgr/**. La configurazione proxy è disponibile in **org.apache.http.proxyconfigurator.**

>[!NOTE]
>
>In AEM 6.0 e versioni precedenti il proxy era configurato nel client HTTP Day Commons. A partire AEM 6.1 e versioni successive, la configurazione proxy è stata spostata nella configurazione proxy dei componenti Apache HTTP invece della configurazione &#39;Day Commons HTTP Client&#39;.

**Giorno CQ** AntispamConfigurare il servizio anti-spam (Akismet) utilizzato. A tal fine è necessario registrare:

* **Provider**
* **Chiave API**
* **URL registrato**

**Adobe Granite HTML Library** ManagerConfigurate questa opzione per controllare la gestione delle librerie client (css o js); incluso, ad esempio, il modo in cui viene vista la struttura sottostante.

* Per le istanze di produzione:

   * abilitare **Minify** (per rimuovere CRLF e spazi bianchi).
   * abilitare **Gzip** (per consentire lo scorrimento e l&#39;accesso ai file con una sola richiesta).
   * disable **Debug**
   * disattiva **Timing**

* Per lo sviluppo JS (in particolare quando si esegue il firebugging/debug):

   * disable **Minify**
   * abilitare **Debug** per separare i file per il debug e l&#39;utilizzo con firebug.
   * abilitare **Timing** nel caso di interesse nei tempi.
   * abilitare la console **Debug** per visualizzare i messaggi di registro della console JS.

>[!CAUTION]
>
>Quando si modifica l&#39;impostazione per **Minify** o **Gzip** sarà necessario eliminare anche il contenuto di `/var/clientlibs`. Questa è una versione memorizzata nella cache dei clientlibs e verrà ricreata quando richiesto.

>[!NOTE]
>
>Questa impostazione viene configurata automaticamente per le istanze di produzione se si esegue AEM in [Modalità pronta produzione](/help/sites-administering/production-ready.md).

**Day CQ HTTP Header Authentication** HandlerImpostazioni a livello di sistema per il metodo di autenticazione di base della richiesta HTTP.

Quando si utilizza [gruppi di utenti chiusi](/help/sites-administering/cug.md) è possibile configurare (tra gli altri):

* **Realm HTTP**
* La **pagina di accesso predefinita**

**Day CQ Link Checker** ServiceCheck e, se necessario, configurare:

* **Pianificatore** Periodico per definire l&#39;intervallo in cui i collegamenti esterni devono essere controllati automaticamente.

* Selezionare **Intervallo tolleranza collegamento errato** per il periodo in cui un collegamento esterno non riuscito viene considerato non valido.
* **Sovrascrivi pattern** di controllo collegamento per definire eventuali percorsi da escludere dal controllo dei collegamenti.

**Attività Controllo collegamenti CQ Day** TaskConfigurazione delle impostazioni per un’unica attività di controllo collegamenti (un’attività che controlla un collegamento esterno):

* Controllare gli intervalli definiti in **intervallo di test dei collegamenti buoni** e **intervallo di test collegamenti non validi**

* I vari parametri relativi ai proxy per l&#39;accesso a Internet e NTLM che sono necessari per l&#39;accesso esterno durante il controllo di un collegamento.

**Day CQ Mail** ServiceConfigurare il nome host e i dettagli di accesso per il server di posta. Fare riferimento alla sezione Configurazione del servizio e-mail.

**Day CQ MCM** NewsletterConfigurate le varie impostazioni utilizzate con la newsletter.

**Day CQ Root** MappingConfigure:

* **Percorso di destinazione** per definire la destinazione di reindirizzamento di una richiesta a &quot;  `/`&quot;.

Sono disponibili due interfacce in AEM:

* l’interfaccia touch è l’interfaccia standard
* e l&#39;interfaccia classica obsoleta è ancora completamente operativa

Utilizzando AEM mappatura radice è possibile configurare l’interfaccia che si desidera utilizzare come predefinita per l’istanza:

* Per avere l&#39;interfaccia touch come interfaccia predefinita, **Target Path** deve puntare a:

   ```
      /projects.html
   ```

* Per avere l&#39;interfaccia classica come interfaccia predefinita, **Target Path** deve puntare a:

   ```
      /welcome.html
   ```

>[!NOTE]
>
>Con un’installazione standard, l’interfaccia touch è l’interfaccia predefinita.

**Adobe** gestore autenticazione SSO GraniteConfigurare i dettagli Single Sign On (SSO); spesso sono necessarie nelle impostazioni di authoring aziendale, spesso in combinazione con LDAP.

Sono disponibili diverse proprietà di configurazione:

* ****
PathPath per il quale è attivo questo gestore di autenticazione. Se questo parametro viene lasciato vuoto, il gestore di autenticazione viene disabilitato. Ad esempio, il percorso / causa l&#39;utilizzo del gestore di autenticazione per l&#39;intero repository.

* **Il valore**
RankingOSGi Framework Service Ranking viene utilizzato per indicare l&#39;ordine utilizzato per chiamare questo servizio. Questa è una 
`int` dove i valori più alti indicano una precedenza maggiore.
Il valore predefinito è `0`.

* **Nomi**
delle intestazioniI nomi delle intestazioni che possono contenere un ID utente.

* **Cookie**
Names: i nomi dei cookie che possono contenere un ID utente.

* **Nomi**
dei parametri: i nomi dei parametri di richiesta che potrebbero fornire l&#39;ID utente.

* **Mappa utente:**
per gli utenti selezionati, il nome utente estratto dalla richiesta HTTP può essere sostituito con uno diverso nell&#39;oggetto credenziali. La mappatura è definita qui. Se il nome utente 
`admin` viene visualizzata su entrambi i lati della mappa. La mappatura verrà ignorata. Tenere presente che il carattere &quot;=&quot; deve essere preceduto da un carattere &quot;\&quot; iniziale.

* ****
Formato: indica il formato in cui viene fornito l&#39;ID utente. Utilizzo:

   * `Basic` se l&#39;ID utente è codificato nel formato di autenticazione di base HTTP
   * `AsIs` se l&#39;ID utente è fornito in testo normale o se qualsiasi espressione regolare applicata deve essere utilizzata come tale o qualsiasi espressione regolare

**Day CQ WCM Debug** FilterQuesto è utile quando si sviluppa in quanto consente l&#39;utilizzo di suffissi come ?debug=layout quando si accede a una pagina. Ad esempio, https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layout fornirà informazioni sul layout che potrebbero interessare allo sviluppatore.

* Disattivate questa opzione nelle istanze di produzione per garantire prestazioni e protezione.

**Day CQ WCM** FilterConfigure:

* **Modalità WCM **per definire il modo predefinito.
* In un&#39;istanza di authoring potrebbe essere `edit`, `disable,preview` o `analytics`.
È possibile accedere alle altre modalità dalla barra laterale oppure utilizzare il suffisso `?wcmmode=disabled` per emulare un ambiente di produzione.

* In un&#39;istanza di pubblicazione, questo deve essere impostato su `disabled` per garantire che nessun&#39;altra modalità sia accessibile.

>[!NOTE]
>
>Questa impostazione viene configurata automaticamente per le istanze di produzione se si esegue AEM in [Modalità pronta produzione](/help/sites-administering/production-ready.md).

**Day CQ WCM Link Checker** ConfiguratorConfigure:

* **Elenco delle** configurazioni di riscrittura per specificare un elenco di posizioni per le configurazioni del controllo dei collegamenti basate su contenuto. Le configurazioni possono essere basate sulla modalità di esecuzione; è importante distinguere tra ambienti di creazione e pubblicazione, in quanto le impostazioni del controllo dei collegamenti possono essere diverse.

**Day CQ WCM Page** ProcessorConfigure:

* **Percorsi**, un elenco di posizioni in cui il sistema ascolta le modifiche apportate alla pagina prima di attivare un  `jcr:Event`.

**Adobe** Tracker impression paginaPer un’istanza di creazione configurate:

* **sling.auth.requirements**: imposta il valore di questa proprietà su  `-/libs/wcm/stats/tracker`

>[!CAUTION]
>
>Questa configurazione consente richieste anonime al servizio di tracciamento.

>[!NOTE]
>
>Per ulteriori informazioni, vedere [Page Impression](/help/sites-deploying/configuring.md#enabling-page-impressions).

**Day CQ WCM Page** StatisticsPer un’istanza di pubblicazione configurare:

* **l’URL per l’invio** dei dati consente di configurare l’URL utilizzato per monitorare le statistiche delle pagine (è fondamentale se una richiesta di tracciamento passa attraverso il dispatcher); ad esempio, il valore predefinito è  `https://localhost:4502/libs/wcm/stats/tracker`.

* **Script di tracciamento** abilitato per abilitare (  `true`) o disabilitare (  `false`) l&#39;inclusione dello script di tracciamento nelle pagine. Il valore predefinito è `false`.

>[!NOTE]
>
>Per ulteriori informazioni, vedere [Page Impression](/help/sites-deploying/configuring.md#enabling-page-impressions).

**Day CQ WCM Version** ManagerControl se e come vengono gestite le versioni nel sistema:

* **Crea versione all&#39;attivazione**, abilitata in un&#39;installazione standard
* **Abilita rimozione forzata**

* **Elimina percorsi**, percorsi che verranno cercati in un’azione di ricerca
* **Percorsi** di controllo delle versioni impliciti, i percorsi in cui è attivo il controllo delle versioni implicite.

* **Massima età** versione, età massima (in giorni) di una versione

* **Numero massimo di versioni**, il numero massimo di versioni da mantenere

Per ulteriori informazioni, vedere [Version Purging](/help/sites-deploying/version-purging.md).

**Giorno CQ Workflow Email Notification** ServiceConfigurare le impostazioni e-mail per le notifiche inviate da un flusso di lavoro.

**Day CQSE HTTP** ServiceControllare il motore servlet CQ:

* **NIO per HTTP, **Se utilizzare o meno NIO per HTTP. Valori predefiniti per true. Utilizzata solo se HTTP è abilitato.
* **Timeout connessione, **Timeout connessione in millisecondi. Questa proprietà si applica sia alle connessioni HTTP che a quelle HTTPS. Il valore predefinito è 60 secondi.

* **Abilita HTTPS,** indipendentemente dal fatto che HTTPS sia abilitato o meno. Il valore predefinito è false.
* **Timeout** sessione, durata predefinita di una sessione HTTP specificata in minuti. Se il timeout è pari a 0 o inferiore, le sessioni non avranno mai un timeout. Il valore predefinito è 10 minuti.
* **Debug Logging**, se scrivere o meno messaggi di livello DEBUG. Il valore predefinito è false.
* **Dimensioni** buffer richieste, Dimensione del buffer per le richieste in byte. Il valore predefinito è 8 KB.
* **Numero massimo di thread**, numero massimo di thread da utilizzare per gestire le richieste. Il valore predefinito è 200.

Le seguenti proprietà sono valide solo se HTTPS è abilitato.

* **Porta** HTTPS, porta da ascoltare per la richiesta HTTPS. Valore predefinito 433.
* **NIO per HTTPS**, se utilizzare o meno NIO per HTTP. Il valore predefinito è il valore della proprietà NIO per HTTP.
* **Keystore**, percorso assoluto dell&#39;archivio chiavi da utilizzare per HTTPS. Obbligatorio se HTTPS è abilitato.
* **Password** archivio chiavi, Password per accedere al Keystore.
* **Alias** chiave, alias della chiave segreta in Keystore.
* **Password** chiave, Password per sbloccare la chiave segreta in Keystore.
* **Certificato** client, requisito per la fornitura di un certificato valido da parte del client. Il valore predefinito è none.

Per informazioni sulle opzioni relative a SSL e per una descrizione completa dell&#39;attivazione di HTTPS per CQSE, vedere anche [Abilitazione di HTTP su SSL](/help/sites-administering/ssl-by-default.md).

**CQ Rewriter HTML Parser Factory**

Controlla il parser HTML per la riscrittura CQ.

* **Tag aggiuntivi da elaborare** : è possibile aggiungere o rimuovere tag HTML da elaborare dal parser. Per impostazione predefinita, vengono elaborati i seguenti tag: A,IMG,AREA,MODULO,BASE,COLLEGAMENTO,SCRIPT,CORPO,HEAD.
* **Mantieni caso**  del cammello - Per impostazione predefinita, il parser HTML converte gli attributi in caso di cammello (ad es. eBay) in lettere maiuscole (ad es. ebay). È possibile disattivare questa opzione per mantenere gli attributi della cassa del cammello. Questa funzione è utile quando si utilizzano strutture frontali come Angular 2.

**Day Commons JDBC Connections** PoolConfigura l&#39;accesso a un database esterno utilizzato come origine per il contenuto.

Questa è una configurazione di fabbrica, in modo che possano essere configurate più istanze.

**Adobe CQ Media DPS Sessions** ServiceGestire le sessioni DPS da utilizzare con le pubblicazioni.

In particolare è possibile definire `dps.session.service.url.name`: il valore predefinito è impostato su [https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions](https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions)

**CDN** RewriterLa comunicazione tra AEM e CDN deve essere garantita in modo che le risorse/i file binari vengano consegnati all’utente finale in modo sicuro. Sono necessarie due attività:

* Accesso alla risorsa da AEM tramite CDN la prima volta (o dopo la scadenza nella cache).
* Accedere alla risorsa nella cache CDN in modo sicuro, dal momento che una volta che la risorsa è memorizzata nella cache CDN, la richiesta non verrà AEM e tutti gli utenti che hanno accesso a tale risorsa dovranno essere serviti dalla rete CDN.

AEM riscrittura degli URL delle risorse interne agli URL CDN esterni. Riscrive i collegamenti da trasmettere alla CDN, inclusa una firma JWS, e il tempo di scadenza per consentire l’accesso sicuro alla risorsa. Questa funzione deve essere utilizzata per le istanze di authoring.

Il flusso complessivo è il seguente:

1. L’utente si autentica con AEM e richiede una pagina con risorse.
1. La pagina richiesta contiene una risorsa simile a `/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png`
1. Rewriter trasforma il collegamento a un URL CDN contenente una firma JWS:
   `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`

1. Il browser dell’utente inoltra la richiesta di risorse al server CDN
1. CDN deve essere configurato per inoltrare la richiesta al AEM insieme al parametro `cdn_sign`.
1. Un gestore di autenticazione convalida il parametro `cdn_sign` e restituisce la risorsa a CDN, che viene quindi consegnata all&#39;utente

Il flusso tra il browser dell&#39;utente, la CDN e AEM può essere visualizzato come segue.

![chlimage_1-8](assets/chlimage_1-8.png)

>[!NOTE]
>
>Al momento questa funzione è abilitata solo per AEM istanze dell’autore.

**** CDNConfigServiceImplFornisce le configurazioni CDN

La funzione di riscrittura CDN può essere attivata fornendo **Nome del dominio di distribuzione CDN** nella configurazione per com.adobe.cq.cdn.rewriter.impl.CDNConfigServiceImpl.

Il servizio contiene anche altre opzioni di configurazione come abilitare/disabilitare la riscrittura CDN, i prefissi di percorso per i quali viene eseguita la riscrittura CDN, i valori TTL e il protocollo (HTTP o HTTPS).

**** CDNRewriterUn rewriter per la riscrittura degli URL immagine interni agli URL CDN

È possibile definire il valore **Tag Attributes** in com.adobe.cq.cdn.rewriter.impl.CDNRewriter in modo che vengano riscritti solo i collegamenti immagine selettivi.
