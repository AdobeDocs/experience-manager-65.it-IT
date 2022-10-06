---
title: Impostazioni di configurazione OSGi
seo-title: OSGi Configuration Settings
description: Questo articolo descrive le impostazioni di configurazione OSGi (elencate in base al bundle) rilevanti per l'implementazione del progetto. L’elenco funge da linea guida e non è esaustivo.
seo-description: This article details the OSGi configuration settings (listed according to bundle) that are relevant to project implementation. The list acts as a guideline and it is not exhaustive.
uuid: 192d3287-ec99-403b-bab0-45721e4e3abd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: ed3a858c-7a43-4515-a2ff-43ca465c7d7d
docset: aem65
feature: Configuring
exl-id: 19eedcf2-140a-452d-aa8f-6fd7f219e5f8
source-git-commit: 71c318e59f39b091f52650853be2d472354c2f1c
workflow-type: tm+mt
source-wordcount: '3474'
ht-degree: 0%

---

# Impostazioni di configurazione OSGi{#osgi-configuration-settings}

[OSGi](https://www.osgi.org/) è un elemento fondamentale nello stack tecnologico di AEM. Viene utilizzato per controllare i bundle compositi di AEM e la loro configurazione.

OSGi &quot;*fornisce le primitive standardizzate che consentono di costruire applicazioni a partire da componenti di piccole dimensioni, riutilizzabili e collaborative. Questi componenti possono essere composti in un’applicazione e distribuiti*&quot;.

Questo consente una facile gestione dei bundle in quanto possono essere arrestati, installati, avviati individualmente. Le interdipendenze vengono gestite automaticamente. Ogni componente OSGi (vedi la [Specifiche OSGi](https://www.osgi.org/Specifications/HomePage)) è contenuta in uno dei vari bundle. Quando lavori con AEM esistono diversi metodi per gestire le impostazioni di configurazione per tali bundle; vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per ulteriori dettagli e procedure consigliate.

Le seguenti impostazioni di configurazione OSGi (elencate in base al bundle) sono rilevanti per l&#39;implementazione del progetto. Non tutte le impostazioni elencate devono essere regolate, alcune sono menzionate per aiutarti a capire come funziona AEM.

>[!CAUTION]
>
>L’elenco è inteso come linea guida e non è esaustivo. Non tutti i bundle sono elencati, né tutti i parametri per alcuni dei bundle che sono.
>
>La configurazione necessaria varia da progetto a progetto.
>
>Per i valori utilizzati e per informazioni dettagliate sui parametri, consultate la console Web .

>[!NOTE]
>
>Lo strumento OSGi Configuration Diff, parte del [Strumenti AEM](https://helpx.adobe.com/experience-manager/kb/tools/aem-tools.html), può essere utilizzato per elencare le configurazioni OSGi predefinite.

>[!NOTE]
>
>Possono essere necessari ulteriori bundle per aree specifiche di funzionalità all&#39;interno di AEM. In questi casi, i dettagli di configurazione si trovano sulla pagina in relazione alla funzionalità appropriata.

**Listener di eventi di replica AEM** Configura:

* La **Modalità di esecuzione**, in cui gli eventi di replica verranno distribuiti agli ascoltatori. Ad esempio, se definito come autore, questo è il sistema che &quot;avvia&quot; la replica.

* Modalità di esecuzione **pubblicare** deve essere aggiunto se il codice del progetto elabora eventi di replica (replica inversa) in un ambiente di pubblicazione. Ad esempio, quando il dispatcher viene utilizzato per lo scaricamento dall’ambiente di pubblicazione o quando si verifica la replica standard ad altre istanze di pubblicazione.

**AEM listener di modifiche all&#39;archivio** Configura:

* La **Percorsi**, posizioni per ascoltare gli eventi dell’archivio pronti per la distribuzione.

**Archivio client CRX Sling** Configura l’accesso all’archivio dei contenuti sottostante.

* La **Password amministratore** devono essere modificate dopo l&#39;installazione per garantire che [sicurezza](/help/sites-administering/security-checklist.md) della tua istanza.
* Altre modifiche non dovrebbero essere necessarie e occorre prestare attenzione in quanto possono influenzare l’accesso all’archivio.

**Console di gestione Apache Felix OSGi** Configura:

* **Plug-in**, gli elementi di navigazione principali (plug-in della console) disponibili nella **Console di gestione web Apache Felix** come voci di menu di livello principale. Disabilita le risorse e gli spazi necessari per ciascuna operazione non necessaria.

>[!CAUTION]
>
>Assicurati di configurare quanto segue:
>
>**Nome utente** e **Password**, le credenziali per l&#39;accesso alla console di gestione web Apache Felix stessa.
>La password deve essere modificata dopo l&#39;installazione iniziale per garantire che [sicurezza](/help/sites-administering/security-checklist.md) della tua istanza.

>[!NOTE]
>
>Questa configurazione deve essere effettuata utilizzando la console Felix come necessario all&#39;avvio, prima che l&#39;archivio sia disponibile.

**Apache Sling Registratore dati di richiesta personalizzabile** Configura:

* **Nome logger** e **Formato del registro** per configurare la posizione e il formato della richiesta e la registrazione degli accessi (impostazione predefinita: `request.log`). Questo file di registro è essenziale per l’analisi delle prestazioni o delle funzionalità di debug correlate alla catena web.
Questa è associata al [Registratore di richieste Apache Sling](#apacheslingrequestlogger).

Per ulteriori informazioni consulta [Registrazione AEM](/help/sites-deploying/configure-logging.md) e [Registrazione Sling](https://sling.apache.org/site/logging.html).

**Pool di thread di eventi Apache Sling** Configura:

* **Dimensione min. pool** e **Dimensione massima pool**, la dimensione del pool utilizzato per contenere i thread di evento.

* **Dimensione coda**, la dimensione massima della coda del thread se il pool è esaurito.
Il valore consigliato è `-1` imposta la coda su illimitata; se viene fissato un limite, le perdite potrebbero verificarsi in caso di superamento.

* La modifica di queste impostazioni può migliorare le prestazioni in scenari con un numero elevato di eventi; ad esempio, un utilizzo intensivo di DAM o Workflow AEM.
* I valori specifici dello scenario devono essere stabiliti utilizzando i test.
* Queste impostazioni possono influire sulle prestazioni dell&#39;istanza, pertanto non modificarle senza motivo e con la dovuta considerazione.

**Servlet Apache Sling GET** Configura alcuni aspetti del rendering:

* **Indice automatico** per abilitare/disabilitare il rendering della directory per la navigazione.
* **Abilita** (o disattivare) rendering predefiniti, ad esempio **HTML**, **Testo normale**, **JSON** o **XML**.
Non devi disabilitare JSON.

>[!NOTE]
>
>Questa impostazione viene configurata automaticamente per le istanze di produzione se esegui AEM in [Modalità pronta per la produzione](/help/sites-administering/production-ready.md).

**Apache Sling Java Script Handler** Configura le impostazioni per la compilazione dei file .java come script (servlets).

Alcune impostazioni possono influire sulle prestazioni, che devono essere disattivate ove possibile, in particolare per un&#39;istanza di produzione.

* **VM di origine** e **VM di destinazione**, definisci la versione JDK come utilizzata come JVM di runtime

* per le istanze di produzione:

   * disable **Genera informazioni di debug**

**Programma di installazione di JCR Apache Sling** Questi parametri probabilmente non necessitano di configurazione, ma possono essere utili per sapere quando si sviluppano o eseguono il debug. Ad esempio, le cartelle di installazione possono essere utili per il check-in/out o la creazione di un pacchetto.

* **Nome delle cartelle di installazione regexp** e **Profondità massima della gerarchia delle cartelle di installazione** - specificare dove e a quale profondità vengono cercate le risorse da installare nelle cartelle dell&#39;archivio. Quando viene utilizzato un carattere jolly (come in .&#42;/install) verranno cercate tutte le corrispondenze appropriate, ad esempio: `/libs/sling/install` e `/libs/cq/core/install`.

* **Percorso di ricerca**, elenco di percorsi che jcrinstall cerca le risorse da installare, insieme a un numero che indica il fattore di ponderazione per quel percorso.

**Apache Sling Job Event Handler** Configura i parametri per la gestione della pianificazione dei processi:

* **Intervallo tentativi**, **Numero massimo tentativi**, **Processi paralleli massimi**, **Conferma del tempo di attesa**, tra gli altri.

* La modifica di queste impostazioni può migliorare le prestazioni in scenari con un numero elevato di posti di lavoro; ad esempio, un utilizzo intensivo di DAM AEM e flussi di lavoro.
* I valori specifici dello scenario devono essere stabiliti utilizzando i test.
* Non modificare queste impostazioni senza motivo, ma solo dopo aver tenuto in debita considerazione.

**Apache Sling JSP Script Handler** Configura le impostazioni relative alle prestazioni per il gestore di script JSP. Per migliorare le prestazioni è necessario disattivare il più possibile.

In particolare per le istanze di produzione:

* disable **Genera informazioni di debug**
* disable **Mantieni Java generato**
* disable **Contenuto mappato**
* disable **Visualizza frammenti di origine**

>[!NOTE]
>
>Questa impostazione viene configurata automaticamente per le istanze di produzione se esegui AEM in [Modalità pronta per la produzione](/help/sites-administering/production-ready.md).

**Configurazione della registrazione Apache Sling** Configura:

* **Livello di log** e **File di log**, per definire la posizione e il livello di registro della configurazione di registrazione centrale (error.log). Il livello può essere impostato su uno `DEBUG`, `INFO`, `WARN`, `ERROR` e `FATAL`.

* **Numero di file di registro** e **Soglia file di registro** per definire le dimensioni e la rotazione della versione del file di registro.

* **Pattern messaggio** definisce il formato dei messaggi di log.

Per ulteriori informazioni consulta [Registrazione AEM](/help/sites-deploying/configure-logging.md#global-logging) e [Registrazione Sling](https://sling.apache.org/site/logging.html).

**Configurazione del logger di registrazione Apache Sling (configurazione di fabbrica)** Configura:

* **Livello di log**, **File di log** e **Formato del messaggio** per definire i dettagli del file di registro e dei messaggi.

* **Registratore** definire la categoria; ad esempio, registra solo per com.day.cq.

* Utilizzando **Configurazioni di fabbrica**, è possibile aggiungere un numero qualsiasi di configurazioni aggiuntive per soddisfare i vari livelli di registro e le varie categorie necessarie.
* Tali configurazioni sono utili durante lo sviluppo; ad esempio, per registrare i messaggi di TRACE per un servizio specifico in un file di registro specifico.
* Tali configurazioni sono utili in un ambiente di produzione; ad esempio, per avere messaggi su un servizio specifico registrati in un singolo file di log per un monitoraggio più semplice.

Per ulteriori informazioni consulta [Registrazione AEM](/help/sites-deploying/configure-logging.md) e [Registrazione Sling](https://sling.apache.org/site/logging.html).

**Configurazione dello scrittore di registrazione Apache Sling (configurazione di fabbrica)** Configura:

* **File di log** per definire l’esistenza di un file di registro.
* **Numero di file di registro** per definire la rotazione di versione.

* Lo scrittore può essere utilizzato da un **Configurazione del logger di registrazione Sling di Apache** configurazione.

* Tali configurazioni sono utili durante lo sviluppo; ad esempio, per registrare i messaggi di TRACE per un servizio specifico in un file di registro specifico.
* Tali configurazioni sono utili in un ambiente di produzione; ad esempio, per avere messaggi su un servizio specifico registrati in un singolo file di log per un monitoraggio più semplice.

Per ulteriori informazioni consulta [Registrazione AEM](/help/sites-deploying/configure-logging.md) e [Registrazione Sling](https://sling.apache.org/site/logging.html).

**Servlet principale Apache Sling** Configura:

* **Numero di chiamate per richiesta** e **Profondità di ricursione** per proteggere il sistema da infinite chiamate di ricorsione ed eccessive chiamate di script.

**Servizio di tipo MIME Apache Sling** Configura:

* **Tipi MIME** per aggiungere al sistema quelli richiesti dal progetto. Ciò consente di `GET` su un file per impostare l&#39;intestazione corretta del tipo di contenuto per il collegamento del tipo di file e dell&#39;applicazione.

**Filtro di riferimento Apache Sling** Per risolvere problemi di sicurezza noti con Cross-Site Request Forgery (CSRF) in CRX WebDAV e Apache Sling è necessario configurare il filtro Referrer.

Il servizio filtro referrer è un servizio OSGi che consente di configurare:

* quali metodi http devono essere filtrati
* se è consentita un&#39;intestazione referrer vuota
* e un elenco di server da consentire oltre all&#39;host del server.

Consulta la sezione [Lista di controllo sicurezza - Problemi relativi alla falsificazione delle richieste tra siti diversi](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) per ulteriori dettagli.

>[!NOTE]
>
>Il filtro di riferimento Apache Sling dipende dall&#39;installazione di un pacchetto di correzione rapida.

**Registratore di richieste Apache Sling** Configura:

* vari parametri per definire la modalità di registrazione delle richieste.
* **Abilita registro richieste**, per abilitare o disabilitare.

* **Abilita log di accesso**, per abilitare o disabilitare.

Questa è associata al [Apache Sling Registratore dati di richiesta personalizzabile](#apacheslingcustomizablerequestdatalogger).

Per ulteriori informazioni consulta [Registrazione AEM](/help/sites-deploying/configure-logging.md) e [Registrazione Sling](https://sling.apache.org/site/logging.html).

**Factory di Apache Sling Resource Resolver** Configura gli aspetti centrali della risoluzione delle risorse Sling:

* **Percorso di ricerca risorse**(s), aggiungi eventuali percorsi specifici del progetto (ma non rimuovi `/libs` o `/apps`).

* **URL virtuali** per definire le mappature degli URL personalizzati.

* **Mappature URL** definire eventuali alias; ad esempio da `/content` a `/`.

* **Posizione mappatura**, la configurazione mappatore esternalizzata in `/etc/map`.

* Utilizza l’installazione locale (ad esempio, utilizza `https://localhost:4502/system/console/jcrresolver`) per determinare quale Resource Resolver è attivo.

Per ulteriori informazioni, consulta: [https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution).

>[!CAUTION]
>
>In particolare queste opzioni devono essere configurate nell’archivio.
>
>In caso contrario vengono apportate modifiche a **Mappature URL** l’utilizzo della console Felix potrebbe essere sovrascritto da AEM all’avvio successivo.

**Apache Sling Servlet/Script Resolver e Error Handler** Il servlet Sling e il risolutore script hanno più attività:

1. Viene utilizzato come `ServletResolver` per selezionare il servlet o lo script da chiamare per gestire la richiesta.

1. Agisce come `SlingScriptResolver`.

1. Gestisce la gestione degli errori implementando `ErrorHandler` interfaccia che utilizza lo stesso algoritmo per selezionare i servlet e gli script di gestione degli errori utilizzati per risolvere i servlet e gli script di elaborazione delle richieste.

È possibile impostare diversi parametri, tra cui:

* **Percorsi di esecuzione** elenca i percorsi per la ricerca di script eseguibili; configurando percorsi specifici è possibile limitare gli script eseguibili. Se non è configurato alcun percorso, viene utilizzata l&#39;impostazione predefinita ( `/` = root), questo consente l&#39;esecuzione di tutti gli script.
Se un valore del percorso configurato termina con una barra, viene eseguita la ricerca nell’intero sottoalbero. Senza una tale barra finale lo script verrà eseguito solo se si tratta di una corrispondenza esatta.

* **Utente script** - questa proprietà opzionale può specificare l&#39;account utente dell&#39;archivio utilizzato per leggere gli script. Se non viene specificato alcun account, `admin` l&#39;utente viene utilizzato per impostazione predefinita.

* **Estensioni predefinite** Elenco di estensioni per le quali verrà utilizzato il comportamento predefinito. Questo significa che l’ultimo segmento del percorso del tipo di risorsa può essere utilizzato come nome dello script.

**Configurazione proxy dei componenti HTTP Apache** Configurazione proxy per tutto il codice che utilizza il client HTTP Apache, utilizzato quando viene effettuato un HTTP; ad esempio in caso di replica.

Durante la creazione di una nuova configurazione, non apportare modifiche alla configurazione di fabbrica, ma creare una nuova configurazione di fabbrica per questo componente utilizzando il gestore di configurazione disponibile qui: **https://localhost:4502/system/console/configMgr/**. La configurazione proxy è disponibile in **org.apache.http.proxyconfigurator.**

>[!NOTE]
>
>In AEM 6.0 e versioni precedenti il proxy era configurato nel client HTTP Day Commons. A partire da AEM 6.1 e versioni successive, la configurazione proxy è stata spostata nella configurazione proxy &quot;Apache HTTP Components Proxy Configuration&quot; invece della configurazione &quot;Day Commons HTTP Client&quot;.

**Antispam Day CQ** Configura il servizio anti-spam (Akismet) utilizzato. A tal fine è necessario registrare i seguenti dati:

* **Provider**
* **Chiave API**
* **URL registrato**

**Adobe Granite HTML Library Manager** Configura questa opzione per controllare la gestione delle librerie client (css o js); incluso, ad esempio, il modo in cui viene vista la struttura sottostante.

* Per le istanze di produzione:

   * abilita **Miniatura** (per rimuovere CRLF e gli spazi bianchi).
   * abilita **Gzip** (per consentire l’accesso ai file tramite gzip con una richiesta).
   * disable **Debug**
   * disable **Tempi**

* Per lo sviluppo JS (in particolare quando si esegue il firebugging/debug):

   * disable **Miniatura**
   * abilita **Debug** per separare i file per il debug e utilizzarli con firebug.
   * abilita **Tempi** in caso di interesse a tempo.
   * abilita **Debug** per visualizzare i messaggi di log della console JS.

>[!CAUTION]
>
>Quando si modifica l&#39;impostazione per **Miniatura** o **Gzip** dovrai anche eliminare il contenuto di `/var/clientlibs`. Si tratta di una versione cache delle clientlibs e verrà ricreata quando richiesto.

>[!NOTE]
>
>Questa impostazione viene configurata automaticamente per le istanze di produzione se esegui AEM in [Modalità pronta per la produzione](/help/sites-administering/production-ready.md).

**Day CQ HTTP Header Authentication Handler** Impostazioni a livello di sistema per il metodo di autenticazione di base della richiesta HTTP.

Quando utilizzi [gruppi di utenti chiusi](/help/sites-administering/cug.md) puoi configurare (tra gli altri):

* **realm HTTP**
* La **Pagina di accesso predefinita**

**Servizio Day CQ Link Checker** Controlla e, se necessario, configura:

* **Periodo di pianificazione** per definire l’intervallo in cui i collegamenti esterni devono essere controllati automaticamente.

* Controlla **Intervallo di tolleranza del collegamento non valido** per il periodo in cui un collegamento esterno non riuscito è considerato non valido.
* **Modelli di sostituzione del controllo dei collegamenti**, per definire eventuali percorsi da escludere dal controllo dei collegamenti.

**Attività Day CQ Link Checker** Configura le impostazioni per una singola attività di controllo collegamenti (un’attività che controlla un collegamento esterno):

* Controlla gli intervalli definiti in **Intervallo di test del collegamento corretto** e **Intervallo di test del collegamento non valido**

* I vari parametri relativi ai proxy per l’accesso a Internet e NTLM che sono necessari per l’accesso esterno durante il controllo di un collegamento.

**Servizio e-mail Day CQ** Configura il nome host e i dettagli di accesso per il server di posta. Consulta la sezione Configurazione del servizio e-mail .

**Newsletter Day CQ MCM** Configura le varie impostazioni utilizzate con la newsletter.

**Mappatura della radice CQ del giorno** Configura:

* **Percorso di Target** per definire dove inviare una richiesta a &quot; `/`&quot; verrà reindirizzato a.

Sono disponibili due interfacce in AEM:

* l’interfaccia touch è l’interfaccia standard
* e l’interfaccia classica obsoleta è ancora completamente operativa

Utilizzando AEM mappatura principale puoi configurare l’interfaccia utente che desideri usare come predefinita per l’istanza:

* Per utilizzare l’interfaccia touch come interfaccia predefinita **Percorso di Target** indicare:

   ```shell
      /projects.html
   ```

* Per impostare l’interfaccia classica come interfaccia predefinita **Percorso di Target** indicare:

   ```shell
      /welcome.html
   ```

>[!NOTE]
>
>Con un’installazione standard, l’interfaccia touch è l’interfaccia predefinita.

**Gestore autenticazione SSO di Adobe Granite** Configurare i dettagli Single Sign On (SSO); sono spesso necessarie nelle configurazioni dell&#39;autore aziendale, spesso in combinazione con LDAP.

Sono disponibili diverse proprietà di configurazione:

* **Percorso**
Percorso per il quale il gestore di autenticazione è attivo. Se questo parametro viene lasciato vuoto, il gestore di autenticazione viene disabilitato. Ad esempio, il percorso / fa sì che il gestore di autenticazione sia utilizzato per l&#39;intero archivio.

* **Classifica dei servizi**
Il valore di Classifica del servizio Framework OSGi viene utilizzato per indicare l&#39;ordine utilizzato per chiamare questo servizio. Questo è un 
`int` in cui i valori superiori indicano una precedenza superiore.
Il valore predefinito è `0`.

* **Nomi delle intestazioni**
I nomi delle intestazioni che potrebbero contenere un ID utente.

* **Nomi dei cookie**
I nomi dei cookie che potrebbero contenere un ID utente.

* **Nomi dei parametri**
I nomi dei parametri di richiesta che potrebbero fornire l&#39;ID utente.

* **Mappa utente**
Per gli utenti selezionati, il nome utente estratto dalla richiesta HTTP può essere sostituito con uno diverso nell’oggetto credenziali. La mappatura è definita qui. Se il nome utente 
`admin` viene visualizzata su entrambi i lati della mappa, la mappatura verrà ignorata. Tieni presente che il carattere &quot;=&quot; deve essere annullato con un carattere iniziale &quot;\&quot;.

* **Formato**
Indica il formato in cui viene fornito l&#39;ID utente. Utilizzare:

   * `Basic` se l&#39;ID utente è codificato nel formato di autenticazione HTTP Basic
   * `AsIs` se l&#39;ID utente viene fornito in testo normale o se un valore di espressione regolare applicata deve essere utilizzato così com&#39;è o qualsiasi espressione regolare

**Filtro di debug Day CQ WCM** Questo è utile quando si sviluppa perché consente l&#39;uso di suffissi come ?debug=layout quando si accede a una pagina. Ad esempio, https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layout fornirà informazioni sul layout di potenziale interesse per lo sviluppatore.

* Disabilita questa opzione nelle istanze di produzione per garantire prestazioni e sicurezza.

**Filtro WCM Day CQ** Configura:

* **Modalità WCM **per definire il modo predefinito.
* In un&#39;istanza dell&#39;autore, potrebbe essere `edit`, `disable,preview` o `analytics`.
È possibile accedere alle altre modalità dalla barra laterale o dal suffisso `?wcmmode=disabled` può essere utilizzato per emulare un ambiente di produzione.

* In un&#39;istanza di pubblicazione questa deve essere impostata su `disabled` per garantire che nessun&#39;altra modalità sia accessibile.

>[!NOTE]
>
>Questa impostazione viene configurata automaticamente per le istanze di produzione se esegui AEM in [Modalità pronta per la produzione](/help/sites-administering/production-ready.md).

**Configuratore Day CQ WCM Link Checker** Configura:

* **Elenco delle configurazioni di riscrittura** per specificare un elenco di posizioni per le configurazioni del linkchecker basato su contenuti. Le configurazioni possono essere basate sulla modalità di esecuzione; questo è importante per distinguere tra ambienti di authoring e di pubblicazione, in quanto le impostazioni del linkchecker possono variare.

**Day CQ WCM Page Manager Factory** Configura:

* **Controllo attivazione sottoalbero pagina** per consentire a un utente (senza autorizzazioni di replica) di eliminare o spostare pagine (anche se le pagine non sono attivate).

**Processore pagina CQ WCM Day** Configura:

* **Percorsi**, un elenco delle posizioni in cui il sistema ascolta le modifiche di pagina prima di attivare un `jcr:Event`.

**Adobe Tracciamento impressioni pagina** Per un&#39;istanza di authoring configura:

* **sling.auth.requirements**: imposta il valore di questa proprietà su `-/libs/wcm/stats/tracker`

>[!CAUTION]
>
>Questa configurazione consentirà richieste anonime al servizio di tracciamento.

>[!NOTE]
>
>Vedi [Impressioni pagina](/help/sites-deploying/configuring.md#enabling-page-impressions) per ulteriori informazioni.

**Statistiche pagina di CQ WCM** Per un&#39;istanza di pubblicazione, configura:

* **URL per l’invio dei dati** configurare l’URL utilizzato per monitorare le statistiche della pagina (è fondamentale se una richiesta di tracciamento passa attraverso il dispatcher); ad esempio, il valore predefinito è `https://localhost:4502/libs/wcm/stats/tracker`.

* **Script di tracciamento abilitato** per attivare ( `true`) o disattiva ( `false`) l’inclusione dello script di tracciamento nelle pagine. Il valore predefinito è `false`.

>[!NOTE]
>
>Vedi [Impressioni pagina](/help/sites-deploying/configuring.md#enabling-page-impressions) per ulteriori informazioni.

**Day CQ WCM Version Manager** Controlla se e come vengono gestite le versioni nel tuo sistema:

* **Crea versione su attivazione**, abilitato in un’installazione standard
* **Abilita eliminazione**

* **Elimina percorsi**, i percorsi in cui un’azione di ricerca eseguirà la ricerca
* **Percorsi di controllo delle versioni impliciti**, i percorsi in cui è attivo il controllo delle versioni implicite.

* **Età massima della versione**, l&#39;età massima (in giorni) di una versione

* **Numero massimo di versioni**, il numero massimo di versioni da mantenere

Vedi [Rimozione delle versioni](/help/sites-deploying/version-purging.md) per ulteriori informazioni.

**Servizio notifiche e-mail flusso di lavoro del giorno CQ** Configura le impostazioni e-mail per le notifiche inviate da un flusso di lavoro.

**CQ Rewriter HTML Parser Factory**

Controlla il parser HTML per il rewriter CQ.

* **Tag aggiuntivi da elaborare** - È possibile aggiungere o rimuovere tag HTML da elaborare dal parser. Per impostazione predefinita, vengono elaborati i seguenti tag: A,IMG,AREA,MODULO,BASE,COLLEGAMENTO,SCRIPT,CORPO,HEAD.
* **Custodia per camper** - Per impostazione predefinita, il parser HTML converte gli attributi in cammello (ad esempio eBay) in minuscolo (ad esempio ebay). È possibile disattivarlo per mantenere gli attributi della maiuscola. Questa funzione è utile quando si utilizzano framework frontend come l’Angular 2.

**Pool di connessioni JDBC Day Commons** Configura l&#39;accesso a un database esterno utilizzato come origine per il contenuto.

Questa è una configurazione di fabbrica, quindi è possibile configurare più istanze.

**Rewriter CDN** La comunicazione tra AEM e una rete CDN deve essere assicurata in modo che le risorse/i file binari siano consegnati all’utente finale in modo sicuro. Sono necessarie due attività:

* Accedere alla risorsa da AEM tramite la rete CDN la prima volta (o dopo la sua scadenza nella cache).
* Accedere alla risorsa memorizzata nella cache CDN in modo sicuro poiché una volta che la risorsa è memorizzata nella cache CDN, la richiesta non verrà visualizzata in AEM e tutti gli utenti che hanno accesso a tale risorsa su dovranno essere serviti da CDN.

AEM fornisce un rewriter per riscrivere gli URL delle risorse interne in URL CDN esterni. Riscrive i collegamenti da trasmettere alla rete CDN, inclusa una firma JWS, e scade il tempo necessario per consentire l’accesso sicuro alla risorsa. Questa funzione deve essere utilizzata nelle istanze di authoring.

Il flusso complessivo è il seguente:

1. L’utente si autentica con AEM e richiede una pagina con risorse.
1. La pagina richiesta contiene una risorsa simile a `/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png`
1. Rewriter trasforma il collegamento a un URL CDN contenente una firma JWS:
   `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`

1. Il browser dell’utente inoltra quindi la richiesta di risorse al server CDN
1. CDN deve essere configurato per inoltrare la richiesta a AEM insieme al `cdn_sign` parametro .
1. Un gestore di autenticazione convalida il `cdn_sign` e restituisce la risorsa a CDN che viene quindi consegnata all’utente

Il flusso tra il browser dell’utente, la CDN e la AEM può essere visualizzato come segue.

![chlimage_1-8](assets/chlimage_1-8.png)

>[!NOTE]
>
>Al momento questa funzione è abilitata solo per AEM istanze dell’autore.

**CDNConfigServiceImpl** Fornisce configurazioni CDN

La funzione di riscrittura CDN può essere attivata fornendo **Nome del dominio di distribuzione CDN** nella configurazione per com.adobe.cq.cdn.rewriter.impl.CDNConfigServiceImpl.

Il servizio contiene anche altre opzioni di configurazione come l&#39;attivazione/disattivazione della riscrittura CDN, i prefissi di percorso per i quali viene eseguita la riscrittura CDN, i valori TTL e il protocollo (HTTP o HTTPS).

**CDNRewriter** Un rewriter per la riscrittura degli URL di immagini interni agli URL CDN

La **Attributi del tag** è possibile definire il valore in com.adobe.cq.cdn.rewriter.impl.CDNRewriter in modo che vengano riscritti solo i collegamenti immagine selettivi.
