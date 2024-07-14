---
title: Impostazioni configurazione OSGi
description: Questo articolo descrive le impostazioni di configurazione OSGi (elencate in base al bundle) rilevanti per l’implementazione del progetto. L'elenco funge da orientamento e non è esaustivo.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
docset: aem65
feature: Configuring
exl-id: 19eedcf2-140a-452d-aa8f-6fd7f219e5f8
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '3360'
ht-degree: 0%

---

# Impostazioni configurazione OSGi{#osgi-configuration-settings}

[OSGi](https://www.osgi.org/) è un elemento fondamentale nello stack tecnologico dell&#39;AEM. Viene utilizzato per controllare i bundle compositi dell&#39;AEM e la loro configurazione.

OSGi &quot;*fornisce le primitive standardizzate che consentono di creare applicazioni a partire da componenti di piccole dimensioni, riutilizzabili e collaborativi. Questi componenti possono essere composti in un&#39;applicazione e distribuiti*&quot;.

Questa funzionalità consente una facile gestione dei bundle, poiché possono essere arrestati, installati e avviati singolarmente. Le interdipendenze vengono gestite automaticamente. Ogni componente OSGi (vedi la [specifica OSGi](https://docs.osgi.org/specification/)) è contenuto in uno dei vari bundle. Quando si lavora con AEM, esistono diversi metodi per gestire le impostazioni di configurazione per tali bundle; vedi [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per ulteriori dettagli e le procedure consigliate.

Le seguenti impostazioni di configurazione OSGi (elencate in base al bundle) sono rilevanti per l’implementazione del progetto. Non tutte le impostazioni elencate devono essere regolate, alcune sono menzionate per aiutarti a capire come funziona l&#39;AEM.

>[!CAUTION]
>
>L&#39;elenco funge da orientamento e non è esaustivo. Non sono elencati tutti i bundle, né tutti i parametri per alcuni dei bundle che lo sono.
>
>La configurazione necessaria varia da progetto a progetto.
>
>Per informazioni dettagliate sui parametri, consulta la console Web per i valori utilizzati.

>[!NOTE]
>
>È possibile utilizzare lo strumento Diff. configurazione OSGi, parte di [Strumenti AEM](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17488.html), per elencare le configurazioni OSGi predefinite.

>[!NOTE]
>
>Ulteriori pacchetti potrebbero essere necessari per specifiche aree di funzionalità all&#39;interno dell&#39;AEM. In questi casi, i dettagli di configurazione si trovano nella pagina relativa alle funzionalità appropriate.

**Listener eventi di replica AEM** Configura:

* **Modalità di esecuzione**, in cui gli eventi di replica vengono distribuiti ai listener. Ad esempio, se è definito come autore, è il sistema che &quot;avvia&quot; la replica.

* Aggiungere la modalità di esecuzione **pubblicazione** se il codice del progetto elabora gli eventi di replica (replica inversa) in un ambiente di pubblicazione. Ad esempio, quando Dispatcher viene utilizzato per eseguire il flushing dall’ambiente di pubblicazione o quando si verifica la replica standard in altre istanze di pubblicazione.

**Listener modifiche archivio AEM** Configura:

* I **Percorsi**, percorsi in cui eseguire l&#39;ascolto degli eventi del repository pronti per la distribuzione.

**Archivio client CRX Sling** Configura l&#39;accesso all&#39;archivio dei contenuti sottostante.

* La **password amministratore** deve essere modificata dopo l&#39;installazione per garantire la [sicurezza](/help/sites-administering/security-checklist.md) dell&#39;istanza.
* Altre modifiche non dovrebbero essere necessarie e occorre prestare attenzione in quanto possono influire sull’accesso all’archivio.

**Console di gestione OSGi Apache Felix** Configura:

* **Plug-in**, gli elementi di navigazione principali (plug-in della console) disponibili nella **Console di gestione Web Apache Felix** come elementi di menu di livello principale. Disattiva qualsiasi elemento non necessario in quanto ciascuno richiede spazio e risorse.

>[!CAUTION]
>
>Assicurati di configurare quanto segue:
>
>**Nome utente** e **Password**, le credenziali per accedere alla Console di gestione Web Apache Felix.
>La password deve essere modificata dopo l&#39;installazione iniziale per garantire la [sicurezza](/help/sites-administering/security-checklist.md) dell&#39;istanza.

>[!NOTE]
>
>Questa configurazione deve essere effettuata utilizzando la console Felix in base alle esigenze all’avvio, prima che l’archivio sia disponibile.

**Logger dati della richiesta personalizzabile Apache Sling** Configura:

* **Nome logger** e **Formato registro** per configurare il percorso e il formato della registrazione delle richieste e degli accessi (impostazione predefinita: `request.log`). Questo file di registro è essenziale per l’analisi delle prestazioni o delle funzionalità di debug relative alla catena web. È associata al [Logger richieste Sling di Apache](#apacheslingrequestlogger).

Consulta [Registrazione AEM](/help/sites-deploying/configure-logging.md) e [Registrazione Sling](https://sling.apache.org/documentation/development/logging.html).

**Pool di thread eventi Sling Apache** Configura:

* **Dimensione minima del pool** e **Dimensione massima del pool**, ovvero la dimensione del pool utilizzata per contenere i thread evento.

* **Dimensione coda**, la dimensione massima della coda del thread se il pool è esaurito.
Il valore consigliato è `-1` perché imposta la coda su illimitato. Se viene fissato un limite, potrebbero verificarsi perdite al superamento di tale limite.

* La modifica di queste impostazioni può migliorare le prestazioni in scenari con un numero elevato di eventi. Ad esempio, un uso intensivo di DAM AEM o di Workflow.
* I valori specifici dello scenario devono essere stabiliti utilizzando test.
* Queste impostazioni possono influire sulle prestazioni dell’istanza, pertanto non modificarle senza un motivo valido e la dovuta considerazione.

**Apache Sling GET Servlet** Configura alcuni aspetti del rendering:

* **Indice automatico** per abilitare/disabilitare il rendering della directory per la navigazione.
* **Abilita** (o disabilita) le rappresentazioni predefinite, ad esempio **HTML**, **Testo normale**, **JSON** o **XML**.
Non disabilitare JSON.

>[!NOTE]
>
>Questa impostazione viene configurata automaticamente per le istanze di produzione se si esegue AEM in [modalità pronta per la produzione](/help/sites-administering/production-ready.md).

**Gestore JavaScript Apache Sling** Configura le impostazioni per la compilazione di file Java come script (servlet).

Alcune impostazioni possono influire sulle prestazioni. Se possibile, disabilita queste impostazioni, in particolare per un’istanza di produzione.

* **VM Source** e **VM di destinazione**, definire la versione JDK utilizzata come JVM di runtime

* per le istanze di produzione:

   * disabilita **Genera informazioni debug**

**Programma di installazione di Apache Sling JCR** Questi parametri probabilmente non richiedono configurazione, ma possono essere utili per lo sviluppo o il debug. Ad esempio, le cartelle di installazione possono essere utili per l&#39;archiviazione o l&#39;estrazione o per la creazione di un pacchetto.

* **Nome delle cartelle di installazione regexp** e **Profondità massima gerarchia delle cartelle di installazione** - Specificare dove e a quale profondità vengono cercate le risorse da installare nelle cartelle del repository. Quando viene utilizzato un carattere jolly (come in .&#42;/install) vengono cercate tutte le corrispondenze appropriate, ad esempio `/libs/sling/install` e `/libs/cq/core/install`.

* **Percorso di ricerca**, elenco di percorsi che jcrinstall cerca le risorse da installare, con un numero che indica il fattore di ponderazione per il percorso.

**Gestore eventi processo Sling Apache** Configura i parametri che gestiscono la pianificazione dei processi:

* **Intervallo tentativi**, **Numero massimo tentativi**, **Numero massimo processi paralleli**, **Tempo di attesa conferma**, tra gli altri.

* La modifica di queste impostazioni può migliorare le prestazioni in scenari con un numero elevato di processi, ad esempio l’utilizzo intensivo di DAM e Flussi di lavoro AEM.
* I valori specifici dello scenario devono essere stabiliti utilizzando test.
* Non modificare queste impostazioni senza motivo, cambiale solo dopo la dovuta considerazione.

**Apache Sling JSP Script Handler** Configura le impostazioni relative alle prestazioni per il gestore di script JSP. Per migliorare le prestazioni, disattiva il più possibile.

In particolare, per le istanze di produzione:

* disabilita **Genera informazioni debug**
* disabilita **Mantieni Java™** generato
* disabilita **Contenuto mappato**
* disabilita **Visualizza frammenti Source**

>[!NOTE]
>
>Questa impostazione viene configurata automaticamente per le istanze di produzione se si esegue AEM in [modalità pronta per la produzione](/help/sites-administering/production-ready.md).

**Configurazione registrazione Sling Apache** Configura:

* **Livello di registro** e **File di registro**, per definire la posizione e il livello di registro della configurazione di registrazione centrale (error.log). Il livello può essere impostato su uno di `DEBUG`, `INFO`, `WARN`, `ERROR` e `FATAL`.

* **Numero di file di registro** e **Soglia file di registro** per definire la dimensione e la rotazione della versione del file di registro.

* **Pattern messaggi** definisce il formato dei messaggi di registro.

Consulta [Registrazione AEM](/help/sites-deploying/configure-logging.md#global-logging) e [Registrazione Sling](https://sling.apache.org/documentation/development/logging.html).

**Configurazione logger registrazione Sling Apache (Configurazione factory)** Configura:

* **Livello registro**, **File registro** e **Formato messaggio** per definire i dettagli del file registro e dei messaggi.

* **Logger** per definire la categoria; ad esempio, log solo per com.day.cq.

* Utilizzando **Configurazioni di fabbrica**, è possibile aggiungere un numero qualsiasi di configurazioni aggiuntive per soddisfare i vari livelli e categorie di registro necessari.
* Tali configurazioni sono utili durante lo sviluppo; ad esempio, per registrare i messaggi di TRACE per un servizio specifico in un file di registro specifico.
* Tali configurazioni sono utili in un ambiente di produzione; ad esempio, per registrare messaggi su un servizio specifico in un singolo file di registro per un monitoraggio più semplice.

Consulta [Registrazione AEM](/help/sites-deploying/configure-logging.md) e [Registrazione Sling](https://sling.apache.org/documentation/development/logging.html).

**Configurazione writer registrazione Sling Apache (Configurazione factory)** Configura:

* **File di log** per definire l&#39;esistenza di un file di log.
* **Numero di file di registro** per definire la rotazione della versione.

* Il writer può essere utilizzato da una configurazione del logger di registrazione **Apache Sling**.

* Tali configurazioni sono utili durante lo sviluppo; ad esempio, per registrare i messaggi di TRACE per un servizio specifico in un file di registro specifico.
* Tali configurazioni sono utili in un ambiente di produzione; ad esempio, per registrare messaggi su un servizio specifico in un singolo file di registro per un monitoraggio più semplice.

Consulta [Registrazione AEM](/help/sites-deploying/configure-logging.md) e [Registrazione Sling](https://sling.apache.org/documentation/development/logging.html).

**Apache Sling Main Servlet** Configura:

* **Numero di chiamate per richiesta** e **Profondità di ricorsione** per proteggere il sistema da ricorsioni infinite e chiamate di script eccessive.

**Apache Sling MIME Type Service** Configura:

* **Tipi MIME** per aggiungere al sistema i tipi richiesti dal progetto. Questa operazione consente a una richiesta `GET` su un file di impostare l&#39;intestazione del tipo di contenuto corretta per il collegamento del tipo di file e dell&#39;applicazione.

**Filtro referrer Apache Sling** Per risolvere problemi di sicurezza noti con CSRF (Cross-Site Request Forgery) in CRX WebDAV e Apache Sling, è necessario configurare il filtro Referrer.

Il servizio di filtro dei referenti è un servizio OSGi che consente di configurare:

* quali metodi http filtrare
* se è consentita un’intestazione referente vuota
* e un elenco di server da consentire in aggiunta all’host del server.

Per ulteriori dettagli, vedi l&#39;[elenco di controllo della sicurezza - Problemi relativi a false richieste tra siti](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery).

>[!NOTE]
>
>Il filtro Apache Sling Referrer dipende dall’installazione di un pacchetto di correzione rapida.

**Logger richieste Sling Apache** Configura:

* vari parametri per definire la modalità di registrazione delle richieste.
* **Abilita registro richieste**, per abilitare o disabilitare.

* **Abilita log degli accessi**, per abilitare o disabilitare.

Associato al [Logger dati della richiesta personalizzabile Apache Sling](#apacheslingcustomizablerequestdatalogger).

Consulta [Registrazione AEM](/help/sites-deploying/configure-logging.md) e [Registrazione Sling](https://sling.apache.org/documentation/development/logging.html).

**Apache Sling Resource Resolver Factory** Configura gli aspetti centrali della risoluzione delle risorse Sling:

* **Percorsi di ricerca risorse**, aggiungere percorsi specifici del progetto (ma non rimuovere `/libs` o `/apps`).

* **URL virtuali** per definire le mappature degli URL personalizzati.

* **Mappature URL** per definire eventuali alias. Ad esempio, da `/content` a `/`.

* **Posizione mappatura**, la configurazione mappatore esternalizzata in `/etc/map`.

* Utilizzare l&#39;installazione locale, ad esempio `https://localhost:4502/system/console/jcrresolver`, per determinare quale Resource Resolver è attivo.

Vedere: [https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution).

>[!CAUTION]
>
>Configura queste opzioni nell’archivio.
>
>In caso contrario, le modifiche apportate alle **mappature URL** tramite la console Felix potrebbero essere sovrascritte dall&#39;AEM al prossimo avvio.

**Apache Sling Servlet/Script Resolver e Error Handler** Il servlet Sling e lo script Resolver dispongono di più attività:

1. Viene utilizzato come `ServletResolver` per selezionare il servlet o lo script da chiamare per gestire la richiesta.

1. Agisce come `SlingScriptResolver`.

1. Gestisce la gestione degli errori implementando l&#39;interfaccia `ErrorHandler` utilizzando lo stesso algoritmo per selezionare servlet e script di gestione degli errori utilizzato per risolvere servlet e script di elaborazione delle richieste.

È possibile impostare vari parametri, tra cui:

* **Percorsi di esecuzione** - Elenca i percorsi per la ricerca di script eseguibili. Configurando percorsi specifici, puoi limitare quali script possono essere eseguiti. Se non è configurato alcun percorso, viene utilizzato il valore predefinito ( `/` = root), che consente l&#39;esecuzione di tutti gli script.
Se un valore di percorso configurato termina con una barra, la ricerca viene eseguita nell&#39;intera sottostruttura. Senza una barra finale di questo tipo, lo script viene eseguito solo se corrisponde esattamente.

* **Utente script** - Questa proprietà facoltativa può specificare l&#39;account utente del repository utilizzato per la lettura degli script. Se non viene specificato alcun account, per impostazione predefinita viene utilizzato l&#39;utente `admin`.

* **Estensioni predefinite** - Elenco di estensioni per le quali viene utilizzato il comportamento predefinito. L’ultimo segmento di percorso del tipo di risorsa può essere utilizzato come nome dello script.

**Configurazione proxy dei componenti HTTP Apache** - Configurazione proxy per tutto il codice che utilizza il client HTTP Apache, utilizzata quando viene creato un HTTP. Ad esempio, durante la replica.

Durante la creazione di una configurazione, non modificare la configurazione di fabbrica. Creare una configurazione di fabbrica per questo componente utilizzando il gestore della configurazione disponibile qui: **https://localhost:4502/system/console/configMgr/**. La configurazione proxy è disponibile in **org.apache.http.proxyconfigurator.**

>[!NOTE]
>
>In AEM 6.0 e versioni precedenti, il proxy era configurato nel client HTTP Day Commons. A partire da AEM 6.1 e versioni successive, la configurazione proxy è stata spostata nella &quot;Configurazione proxy dei componenti HTTP Apache&quot; invece della configurazione &quot;Client HTTP Day Commons&quot;.

**Day CQ Antispam** Configura il servizio anti-spam (Akismet) utilizzato. Questa funzione richiede la registrazione di quanto segue:

* **Provider**
* **Chiave API**
* **URL registrato**

**Adobe Granite HTML Library Manager** Configura per controllare la gestione delle librerie client (css o js), incluso, ad esempio, il modo in cui viene visualizzata la struttura sottostante.

* Per le istanze di produzione:

   * abilita **Minify** (per rimuovere i caratteri CRLF e gli spazi vuoti).
   * abilita **Gzip** (per consentire l&#39;accesso e la visualizzazione dei file con una richiesta).
   * disabilita **Debug**
   * disabilita **Intervallo**

* Per lo sviluppo JS (in particolare durante il debug/debug del firewall):

   * disabilita **Minify**
   * abilitare **Debug** per separare i file per il debug e utilizzarli con il bug di attivazione.
   * abilita **Timing** se ti interessa la tempistica.
   * abilita la console **Debug** per visualizzare i messaggi del registro della console JS.

>[!CAUTION]
>
>Quando si modifica l&#39;impostazione per **Minify** o **Gzip**, eliminare il contenuto della cache clientlibs. Per ulteriori informazioni, vedere l&#39;[articolo della Knowledge Base](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16543.html).

>[!NOTE]
>
>Questa impostazione viene configurata automaticamente per le istanze di produzione se si esegue AEM in [modalità pronta per la produzione](/help/sites-administering/production-ready.md).

**Gestione autenticazione intestazione HTTP Day CQ** Impostazioni a livello di sistema per il metodo di autenticazione di base della richiesta HTTP.

Quando si utilizzano [gruppi di utenti chiusi](/help/sites-administering/cug.md), è possibile configurare, tra gli altri, quanto segue:

* **Area di autenticazione HTTP**
* **Pagina di accesso predefinita**

**Day CQ Link Checker Service** Verifica e, se necessario, configura:

* **Periodo di pianificazione** per definire l&#39;intervallo in cui i collegamenti esterni devono essere controllati automaticamente.

* Selezionare **Intervallo tolleranza collegamenti non valido** per il periodo dopo il quale un collegamento esterno non riuscito viene considerato non valido.
* **Modelli sostituzione verifica collegamenti**, per definire eventuali percorsi da escludere dal controllo collegamenti.

**Attività Verifica collegamenti Day CQ** Configura le impostazioni per un&#39;attività Verifica collegamenti singolo (un&#39;attività che controlla un collegamento esterno):

* Controlla gli intervalli definiti in **Intervallo test collegamento valido** e **Intervallo test collegamento non valido**

* I vari parametri relativi ai proxy per l&#39;accesso a Internet e NTLM necessari per l&#39;accesso esterno durante la verifica di un collegamento.

**Day CQ Mail Service** Configura il nome host e i dettagli di accesso per il server di posta. Consulta la sezione Configurazione del servizio di posta.

**Newsletter Day CQ MCM** Configura le varie impostazioni utilizzate con la newsletter.

**Mappatura radice Day CQ** Configura:

* **Percorso di destinazione** a cui viene reindirizzata una richiesta a &quot; `/`&quot;.

Nell’AEM sono disponibili due interfacce:

* l’interfaccia touch è quella standard
* e l’interfaccia classica obsoleta è ancora completamente operativa

Utilizzando AEM Root Mapping puoi configurare l’interfaccia utente che desideri impostare come predefinita per la tua istanza:

* Per impostare l&#39;interfaccia touch come interfaccia utente predefinita, il percorso di destinazione **Target** deve puntare a:

  ```shell
     /projects.html
  ```

* Per impostare l&#39;interfaccia classica come interfaccia utente predefinita, il percorso **Target** deve puntare a:

  ```shell
     /welcome.html
  ```

>[!NOTE]
>
>In un’installazione standard, l’interfaccia touch è quella predefinita.

**Adobe gestore autenticazione SSO Granite** - Configurare i dettagli SSO (Single Sign-On). Questi dettagli sono spesso necessari nelle impostazioni di authoring Enterprise, spesso con LDAP.

Sono disponibili diverse proprietà di configurazione:

* **Percorso**
Percorso per cui è attivo il gestore di autenticazione. Se questo parametro viene lasciato vuoto, il gestore di autenticazione viene disabilitato. Ad esempio, il percorso / determina l’utilizzo del gestore di autenticazione per l’intero archivio.

* **Classifica dei servizi**
Il valore Classifica servizio framework OSGi viene utilizzato per indicare l’ordine utilizzato per chiamare questo servizio. Questo valore è un `int` in cui i valori più alti indicano una precedenza maggiore.
Il valore predefinito è `0`.

* **Nomi intestazione**
Nomi delle intestazioni che potrebbero contenere un ID utente.

* **Nomi cookie**
Nomi dei cookie che potrebbero contenere un ID utente.

* **Nomi Parametri**
Nomi dei parametri di richiesta che potrebbero fornire l’ID utente.

* **Mappa utente**
Per gli utenti selezionati, il nome utente estratto dalla richiesta HTTP può essere sostituito con uno diverso nell’oggetto credenziali. La mappatura è definita qui. Se il nome utente `admin` viene visualizzato su entrambi i lati della mappa, la mappatura viene ignorata. Il carattere &quot;=&quot; deve essere preceduta da &quot;\&quot;.

* **Formato**
Indica il formato in cui viene fornito l’ID utente. Usa:

   * `Basic` se l&#39;ID utente è codificato nel formato di autenticazione HTTP Basic
   * `AsIs` se l&#39;ID utente viene fornito in testo normale o qualsiasi valore di espressione regolare applicato deve essere utilizzato così com&#39;è o qualsiasi espressione regolare

**Day CQ WCM Debug Filter** Questo è utile per lo sviluppo in quanto consente l&#39;utilizzo di suffissi quali ?debug=layout durante l&#39;accesso a una pagina. Ad esempio, https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layout fornisce informazioni di layout che possono essere di interesse per lo sviluppatore.

* Per garantire prestazioni e sicurezza, disattiva nelle istanze di produzione.

**Filtro WCM Day CQ** Configura:

* **Modalità WCM** per definire la modalità predefinita.
* In un&#39;istanza Autore, questa modalità potrebbe essere `edit`, `disable,preview` o `analytics`.
È possibile accedere alle altre modalità dalla barra laterale oppure utilizzare il suffisso `?wcmmode=disabled` per emulare un ambiente di produzione.

* In un&#39;istanza di pubblicazione, questa modalità deve essere impostata su `disabled` per garantire che nessun&#39;altra modalità sia accessibile.

>[!NOTE]
>
>Questa impostazione viene configurata automaticamente per le istanze di produzione se si esegue AEM in [modalità pronta per la produzione](/help/sites-administering/production-ready.md).

Configuratore verifica collegamenti WCM CQ **Day** Configura:

* **Elenco di configurazioni di riscrittura** per specificare un elenco di posizioni per le configurazioni di verifica collegamenti basate sul contenuto. Le configurazioni possono essere basate sulla modalità di esecuzione. Questo fatto è importante per distinguere tra ambienti di authoring e di pubblicazione, in quanto le impostazioni del Link Checker possono essere diverse.

**Day CQ WCM Page Manager Factory** Configura:

* **Controllo attivazione sottoalbero pagine** per consentire a un utente (senza autorizzazioni di replica) di eliminare o spostare pagine (anche se le pagine non sono attivate).

**Day CQ WCM Page Processor** Configura:

* **Percorsi**, un elenco di posizioni in cui il sistema ascolta le modifiche della pagina prima di attivare `jcr:Event`.

**Tracciamento impression pagina di Adobe** Per un&#39;istanza Autore, configura come segue:

* **sling.auth.requirements**: impostare il valore di questa proprietà su `-/libs/wcm/stats/tracker`

>[!CAUTION]
>
>Questa configurazione consente richieste anonime al servizio di tracciamento.

>[!NOTE]
>
>Per ulteriori informazioni, vedere [Impression pagina](/help/sites-deploying/configuring.md#enabling-page-impressions).

**Statistiche pagina WCM CQ Day** Per un&#39;istanza Publish, configura:

* **URL per l&#39;invio dei dati** per configurare l&#39;URL utilizzato per tenere traccia delle statistiche di pagina (è fondamentale se una richiesta di tracciamento viene eseguita tramite Dispatcher); ad esempio, il valore predefinito è `https://localhost:4502/libs/wcm/stats/tracker`.

* **Script di tracciamento abilitato** per abilitare ( `true`) o disabilitare ( `false`) l&#39;inclusione dello script di tracciamento nelle pagine. Il valore predefinito è `false`.

>[!NOTE]
>
>Per ulteriori informazioni, vedere [Impression pagina](/help/sites-deploying/configuring.md#enabling-page-impressions).

**Day CQ WCM Version Manager** controlla se e come le versioni vengono gestite nel sistema:

* **Crea versione per attivazione**, abilitata in un&#39;installazione standard
* **Abilita rimozione**

* **Percorsi di eliminazione**, i percorsi cercati da un&#39;azione di ricerca.
* **Percorsi di controllo delle versioni impliciti**, i percorsi in cui è attivo il controllo delle versioni implicito.

* **Età massima versione**, l&#39;età massima (in giorni) di una versione

* **Numero massimo versioni**, il numero massimo di versioni da mantenere

Per ulteriori informazioni, vedere [Rimozione della versione](/help/sites-deploying/version-purging.md).

**Servizio di notifica e-mail flusso di lavoro Day CQ** Configura le impostazioni e-mail per le notifiche inviate da un flusso di lavoro.

**Fabbrica parser HTML rewriter CQ**

Controlla il parser HTML per il rewriter CQ.

* **Tag aggiuntivi da elaborare** - È possibile aggiungere o rimuovere i tag HTML da elaborare tramite il parser. Per impostazione predefinita, vengono elaborati i seguenti tag: A,IMG,AREA,FORM,BASE,LINK,SCRIPT,BODY,HEAD.
* **Mantieni Camel Case** - Per impostazione predefinita, il parser HTML converte gli attributi in Camel Case (ad esempio, `eBay`) in caratteri minuscoli (ad esempio, `ebay`). È possibile disattivare questa impostazione per mantenere gli attributi Camel Case. Questa impostazione è utile quando si utilizzano framework frontend come Angular 2.

**Pool connessioni JDBC Day Commons** Configura l&#39;accesso a un database esterno utilizzato come origine per il contenuto.

Configurazione di fabbrica, che consente di configurare più istanze.

**Rewriter CDN** La comunicazione tra AEM e una rete CDN deve essere garantita in modo che le risorse o i file binari vengano consegnati a un utente finale in modo sicuro. Questo processo prevede le due attività seguenti:

* La prima volta (o dopo la scadenza nella cache) si accede alla risorsa dall’AEM tramite la rete CDN.
* Accesso sicuro alla risorsa memorizzata nella cache in CDN. Una volta che la risorsa è memorizzata nella cache in CDN, la richiesta non viene inviata a AEM e tutti gli utenti che hanno accesso a tale risorsa in devono essere serviti da CDN.

AEM fornisce un rewriter per riscrivere gli URL delle risorse interne in URL CDN esterni. Riscrive i collegamenti da passare alla rete CDN, inclusa una firma JWS, e scade per consentire l’accesso sicuro alla risorsa. Questa funzione deve essere utilizzata nelle istanze di authoring.

Il flusso complessivo è il seguente:

1. L’utente si autentica con AEM e richiede una pagina con risorse.
1. La pagina richiesta contiene una risorsa simile a `/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png`
1. Il rewriter trasforma il collegamento in un URL CDN contenente una firma JWS:
   `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`

1. Il browser dell’utente inoltra quindi la richiesta di risorsa al server CDN
1. La rete CDN deve essere configurata per inoltrare la richiesta a AEM insieme al parametro `cdn_sign`.
1. Un gestore di autenticazione convalida il parametro `cdn_sign` e restituisce la risorsa alla rete CDN che viene quindi consegnata all&#39;utente

Il flusso tra il browser dell’utente, la rete CDN e l’AEM può essere visualizzato come segue.

![chlimage_1-8](assets/chlimage_1-8.png)

>[!NOTE]
>
>Questa funzione è abilitata solo per le istanze di creazione AEM.

**CDNConfigServiceImpl** fornisce configurazioni CDN

È possibile abilitare la funzionalità di riscrittura CDN fornendo il nome del dominio di distribuzione **CDN** nella configurazione per com.adobe.cq.cdn.rewriter.impl.CDNConfigServiceImpl.

Il servizio contiene anche altre opzioni di configurazione come abilitare/disabilitare la riscrittura CDN, prefissi di percorso per i quali viene eseguita la riscrittura CDN, valori TTL e protocollo (HTTP o HTTPS).

**CDNRewriter** Un rewriter per la riscrittura degli URL immagine interni in URL CDN

Il valore **Tag Attributes** in com.adobe.cq.cdn.rewriter.impl.CDNRewriter può essere definito in modo che vengano riscritti solo i collegamenti immagine selettivi.
