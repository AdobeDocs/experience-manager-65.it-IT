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

[OSGi](https://www.osgi.org/) è un elemento fondamentale nello stack tecnologico di AEM. Viene utilizzato per controllare i bundle compositi di AEM e la loro configurazione.

OSGi &quot;*fornisce le primitive standardizzate che consentono di creare applicazioni da componenti piccoli, riutilizzabili e collaborativi. Questi componenti possono essere composti in un&#39;applicazione e distribuiti*&quot;.

In questo modo è possibile gestire facilmente i bundle in quanto possono essere arrestati, installati e avviati individualmente. Le interdipendenze vengono gestite automaticamente. Ciascun componente OSGi (consultate la specifica [](https://www.osgi.org/Specifications/HomePage)OSGi) è contenuto in uno dei vari bundle. When working with AEM there are several methods of managing the configuration settings for such bundles; see [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for more details and the recommended practices.

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
>Lo strumento di configurazione OSGi Diff, che fa parte degli strumenti [di](https://helpx.adobe.com/experience-manager/kb/tools/aem-tools.html)AEM, può essere utilizzato per elencare le configurazioni OSGi predefinite.

>[!NOTE]
>
>Possono essere necessari ulteriori pacchetti per aree specifiche di funzionalità all&#39;interno di AEM. In questi casi, i dettagli di configurazione sono disponibili sulla pagina relativa alla funzionalità appropriata.

**AEM del listener** eventi di replica:

* Modalità di **esecuzione**, in cui gli eventi di replica verranno distribuiti ai listener. Ad esempio, se definito come autore, questo è il sistema che &quot;avvia&quot; la replica.

* È necessario aggiungere la modalità di esecuzione **pubblicazione** se il codice del progetto elabora gli eventi di replica (replica inversa) in un ambiente di pubblicazione. Ad esempio, quando il dispatcher viene utilizzato per cancellare dall’ambiente di pubblicazione o quando si verifica la replica standard ad altre istanze di pubblicazione.

**AEM listener** delle modifiche del repository Configurare:

* I **percorsi**, le posizioni in cui ascoltare gli eventi del repository pronti per la distribuzione.

**Repository** client CRX Sling Configura l&#39;accesso all&#39;archivio dei contenuti sottostante.

* Dopo l&#39;installazione, la password **** amministratore deve essere modificata per garantire la [sicurezza](/help/sites-administering/security-checklist.md) dell&#39;istanza.
* Le altre modifiche non dovrebbero essere necessarie e occorre prestare attenzione in quanto possono influenzare l&#39;accesso al repository.

**Servizio** Wiki Mail Configura le impostazioni e-mail per le e-mail inviate da un wiki.

**Console** di gestione Apache Felix OSGi:

* **Plugins**, gli elementi di navigazione principali (plug-in di console) che saranno disponibili nella console **di gestione Web** Apache Felix come voci di menu di livello principale. Disattivate tutte le risorse non necessarie, poiché ciascuna richiede spazio e risorse.

>[!CAUTION]
>
>Assicuratevi di configurare quanto segue:
>
>**Nome** utente e **password**, le credenziali per accedere alla console di gestione Web Apache Felix stessa.
>La password deve essere modificata dopo l&#39;installazione iniziale per garantire la [sicurezza](/help/sites-administering/security-checklist.md) dell&#39;istanza.

>[!NOTE]
>
>Questa configurazione deve essere eseguita utilizzando la console Felix come necessario all’avvio, prima che la directory archivio sia disponibile.

**Apache Sling Custom Request Data Logger** Configure:

* **Nome** del logger e formato **del** registro per configurare la posizione e il formato della richiesta e la registrazione degli accessi (impostazione predefinita: `request.log`). Questo file di registro è essenziale per analizzare le prestazioni o le funzionalità di debug relative alla catena Web.
Questa funzione è associata al [registratore](#apacheslingrequestlogger)Apache Sling Request.

Per ulteriori informazioni, consultate [AEM Registrazione](/help/sites-deploying/configure-logging.md) e Registrazione [Sling](https://sling.apache.org/site/logging.html).

**Apache Sling Eventing Thread Pool** Configura:

* **Dimensione** pool minima e Dimensione **pool** massima, dimensione del pool utilizzato per ospitare i thread dell&#39;evento.

* **Dimensione**coda, dimensione massima della coda di thread se il pool è esaurito.
Il valore consigliato è `-1` in quanto questo imposta la coda su illimitato; se viene fissato un limite, le perdite potrebbero verificarsi in caso di superamento.

* La modifica di tali impostazioni può facilitare le prestazioni in situazioni con un elevato numero di eventi; ad esempio, utilizzo intensivo AEM DAM o Workflow.
* I valori specifici dello scenario devono essere determinati utilizzando i test.
* Queste impostazioni possono influire sulle prestazioni dell&#39;istanza, pertanto non devono essere modificate senza motivo e con la dovuta considerazione.

**Servlet** GET Apache Sling Configura alcuni aspetti del rendering:

* **Indice** automatico per abilitare/disabilitare il rendering della directory per la navigazione.
* **Abilitare** (o disabilitare) le rappresentazioni predefinite, come **HMTL**, **Plain Text**, **JSON** o **XML**.
Non devi disabilitare JSON.

>[!NOTE]
>
>Questa impostazione viene configurata automaticamente per le istanze di produzione se si esegue AEM in modalità [](/help/sites-administering/production-ready.md)Produzione pronta.

**Apache Sling Java Script Handler** Configurare le impostazioni per la compilazione dei file .java come script (servlet).

Alcune impostazioni possono influire sulle prestazioni, che dovrebbero essere disattivate ove possibile, in particolare per un&#39;istanza di produzione.

* VM **di** origine e VM **di** destinazione, definire la versione JDK come utilizzata come JVM di runtime

* per le istanze di produzione:

   * disabilita **Genera informazioni di debug**

**Programma di installazione** Apache Sling JCR Questi parametri probabilmente non richiedono la configurazione, ma possono essere utili per sapere quando si sviluppano o si eseguono operazioni di debug. Ad esempio, le cartelle di installazione possono essere utili per archiviare o creare un pacchetto.

* **Cartelle di installazione nome regexp** e profondità **massima gerarchica delle cartelle** di installazione - specificare dove e a quale profondità vengono cercate le risorse da installare nelle cartelle repository. Quando viene utilizzato un carattere jolly (come in .*/install) verranno cercate tutte le corrispondenze appropriate, ad esempio `/libs/sling/install` e `/libs/cq/core/install`.

* **Percorso** di ricerca, elenco di percorsi che jcrinstall cerca le risorse da installare, insieme a un numero che indica il fattore di ponderazione per tale percorso.

**Gestore** eventi processo Apache Sling Configura i parametri per la gestione della pianificazione dei processi:

* **Intervallo** tentativi, **tentativi** massimi, **massimi processi** paralleli, tempo **di attesa** riconoscimento, tra gli altri.

* La modifica di tali impostazioni può migliorare le prestazioni in scenari con un elevato numero di processi; ad esempio, l&#39;utilizzo intensivo di AEM DAM e Flussi di lavoro.
* I valori specifici dello scenario devono essere determinati utilizzando i test.
* Non modificate queste impostazioni senza motivo, ma modificate solo dopo aver tenuto in debita considerazione.

**Apache Sling JSP Script Handler** Configurare le impostazioni relative alle prestazioni per il gestore di script JSP. Per migliorare le prestazioni è necessario disattivare il più possibile.

In particolare per le istanze di produzione:

* disabilita **Genera informazioni di debug**
* disattiva **Mantieni Java Generato**
* disabilita contenuto **mappato**
* disabilita frammenti **di origine visualizzati**

>[!NOTE]
>
>Questa impostazione viene configurata automaticamente per le istanze di produzione se si esegue AEM in modalità [](/help/sites-administering/production-ready.md)Produzione pronta.

**Configurazione** Registrazione Apache Sling:

* **Livello** di registro e file **di** registro, per definire la posizione e il livello di registro della configurazione di registrazione centrale (error.log). Il livello può essere impostato su uno di `DEBUG`, `INFO`, `WARN`, `ERROR` e `FATAL`.

* **Numero di file** di registro e soglia **file di** registro per definire la dimensione e la rotazione della versione del file di registro.

* **Pattern** messaggio definisce il formato dei messaggi di registro.

Per ulteriori informazioni, consultate [AEM Registrazione](/help/sites-deploying/configure-logging.md#global-logging) e Registrazione [Sling](https://sling.apache.org/site/logging.html).

**Configurazione Del Registratore Di Registrazione Apache Sling (Configurazione Di Fabbrica)** :

* **Livello** di registro, **file** di registro e formato **del** messaggio per definire i dettagli del file di registro e dei messaggi.

* **Registratore** per definire la categoria; ad esempio, solo log per com.day.cq.

* Utilizzando le configurazioni **di** fabbrica, è possibile aggiungere un numero qualsiasi di configurazioni aggiuntive per soddisfare i vari livelli di registro e categorie richiesti.
* Tali configurazioni sono utili durante lo sviluppo; ad esempio, per registrare i messaggi TRACE per un servizio specifico in un file di registro specifico.
* Tali configurazioni sono utili in un ambiente di produzione; ad esempio, per avere messaggi su un servizio specifico registrato in un singolo file di registro per un monitoraggio più semplice.

Per ulteriori informazioni, consultate [AEM Registrazione](/help/sites-deploying/configure-logging.md) e Registrazione [Sling](https://sling.apache.org/site/logging.html).

**Configurazione dello scrittore di registrazione Apache Sling (configurazione di fabbrica)** :

* **File** di registro per definire l’esistenza di un file di registro.
* **Numero di file** di registro per definire la rotazione della versione.

* Il writer può essere utilizzato da una configurazione **Apache Sling Logging Logging Logger Configuration** .

* Tali configurazioni sono utili durante lo sviluppo; ad esempio, per registrare i messaggi TRACE per un servizio specifico in un file di registro specifico.
* Tali configurazioni sono utili in un ambiente di produzione; ad esempio, per avere messaggi su un servizio specifico registrato in un singolo file di registro per un monitoraggio più semplice.

Per ulteriori informazioni, consultate [AEM Registrazione](/help/sites-deploying/configure-logging.md) e Registrazione [Sling](https://sling.apache.org/site/logging.html).

**Apache Sling Main Servlet** Configure:

* **Numero di chiamate per richiesta** e profondità **di** ricorsione per proteggere il sistema da infinite chiamate di ricorsione ed eccessive chiamate di script.

**Apache Sling MIME Type Service** Configure:

* **Tipi** MIME per aggiungere al sistema quelli richiesti dal progetto. Questo consente a una `GET` richiesta su un file di impostare l&#39;intestazione corretta del tipo di contenuto per il collegamento del tipo di file e dell&#39;applicazione.

**Filtro** di riferimento Apache Sling Per risolvere problemi noti di sicurezza con CSRF (Cross-Site Request Forgery) in CRX WebDAV e Apache Sling è necessario configurare il filtro di riferimento.

Il servizio filtro di riferimento è un servizio OSGi che consente di configurare:

* quali metodi http devono essere filtrati
* se è consentita un&#39;intestazione di referente vuota
* e un elenco di server da consentire oltre all&#39;host del server.

Per ulteriori informazioni, consultate l&#39;elenco di controllo [della sicurezza - Problemi con la falsificazione](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) delle richieste intersito.

>[!NOTE]
>
>Il filtro di riferimento Apache Sling dipende dall&#39;installazione di un pacchetto di correzione rapida.

**Apache Sling Request Logger** Configure:

* vari parametri per definire il modo in cui vengono registrate le richieste.
* **Per attivare o disattivare l’opzione Richiedi registro**.

* **Abilita registro** di accesso per abilitare o disabilitare.

Questa funzione è associata al [registratore](#apacheslingcustomizablerequestdatalogger)dati di richiesta personalizzabile Apache Sling.

Per ulteriori informazioni, consultate [AEM Registrazione](/help/sites-deploying/configure-logging.md) e Registrazione [Sling](https://sling.apache.org/site/logging.html).

**Apache Sling Resource Resolver Factory** Configurare gli aspetti centrali della risoluzione delle risorse Sling:

* **Percorso** di ricerca delle risorse, aggiungere eventuali percorsi specifici del progetto (ma non rimuovere `/libs` o `/apps`).

* **URL** virtuali per definire le mappature degli URL personalizzati.

* **Mappature** URL per definire eventuali alias; ad esempio da `/content` a `/`.

* **Posizione** mappatura, la configurazione mappatore esternalizzata in `/etc/map`.

* Utilizzare l&#39;installazione locale (ad esempio, utilizzare `https://localhost:4502/system/console/jcrresolver`) per determinare quale Risolutore risorse è attivo.

Per ulteriori informazioni, consulta: [https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution).

>[!CAUTION]
>
>In particolare queste opzioni devono essere configurate nella directory archivio.
>
>In caso contrario, le modifiche apportate alle mappature **** URL mediante la console Felix potrebbero essere sovrascritte da AEM all’avvio successivo.

**Risolutore Servlet/Script Apache Sling e Gestore** errori Il Servlet Sling e il Risolutore script hanno più attività:

1. Viene utilizzato come `ServletResolver` strumento per selezionare il Servlet o lo Script da chiamare per gestire la richiesta.

1. Agisce come il `SlingScriptResolver`.

1. Gestisce la gestione degli errori implementando l&#39; `ErrorHandler` interfaccia utilizzando lo stesso algoritmo per selezionare i servlet e gli script di gestione degli errori utilizzati per risolvere i servlet e gli script di elaborazione delle richieste.

È possibile impostare diversi parametri, tra cui:

* **Percorsi** di esecuzione elenca i percorsi per la ricerca di script eseguibili; configurando percorsi specifici è possibile limitare gli script che è possibile eseguire. Se non è configurato alcun percorso, viene utilizzata l&#39;impostazione predefinita ( `/` = root), che consente l&#39;esecuzione di tutti gli script.
Se un valore di percorso configurato termina con una barra, viene eseguita la ricerca nell&#39;intero sottoalbero. Senza una barra finale di questo tipo, lo script verrà eseguito solo se si tratta di una corrispondenza esatta.

* **Utente** script: questa proprietà facoltativa può specificare l&#39;account utente dell&#39;archivio utilizzato per leggere gli script. Se non viene specificato alcun account, l&#39; `admin` utente viene utilizzato per impostazione predefinita.

* **Estensioni** predefinite Elenco di estensioni per le quali verrà utilizzato il comportamento predefinito. Questo significa che l&#39;ultimo segmento del percorso del tipo di risorsa può essere utilizzato come nome di script.

**Day Commons GFX Font Helper** Quando si esegue il rendering di elementi grafici è possibile utilizzare DrawText per incorporare testo. Per questo è anche possibile installare i font personalizzati:

* Definire il Percorso **** font da cercare per i font specifici del progetto.
Esempio, `/apps/myapp/fonts`.

**Configurazione proxy di configurazione** proxy dei componenti Apache HTTP per tutto il codice che utilizza il client Apache HTTP, utilizzato quando viene creato un HTTP; ad esempio durante la replica.

Quando create una nuova configurazione, non apportate modifiche alla configurazione di fabbrica, ma create una nuova configurazione di fabbrica per questo componente utilizzando il gestore di configurazione disponibile qui: **https://localhost:4502/system/console/configMgr/**. La configurazione proxy è disponibile in **org.apache.http.proxyconfigurator.**

>[!NOTE]
>
>In AEM 6.0 e versioni precedenti il proxy era configurato nel client HTTP Day Commons. A partire AEM 6.1 e versioni successive, la configurazione proxy è stata spostata nella configurazione proxy dei componenti Apache HTTP invece della configurazione &#39;Day Commons HTTP Client&#39;.

**Day CQ Antispam** Configurare il servizio anti-spam (Akismet) utilizzato. A tal fine è necessario registrare:

* **Provider**
* **Chiave API**
* **URL registrato**

**Adobe Granite HTML Library Manager** Configurate questa opzione per controllare la gestione delle librerie client (css o js); incluso, ad esempio, il modo in cui viene vista la struttura sottostante.

* Per le istanze di produzione:

   * abilitate **Minify** (per rimuovere CRLF e spazi bianchi).
   * abilitare **Gzip** (per consentire la creazione di gzip dei file e l’accesso tramite una sola richiesta).
   * disable **Debug**
   * disattiva **temporizzazione**

* Per lo sviluppo JS (in particolare quando si esegue il firebugging/debug):

   * disable **Minify**
   * abilita **Debug** per separare i file per il debug e usa con firebug.
   * abilitare **Timing** in caso di interesse nel tempo.
   * abilitare la console **Debug** per visualizzare i messaggi di registro della console JS.

>[!CAUTION]
>
>Quando modificate l’impostazione per **Minify** o **Gzip** , dovrete anche eliminare il contenuto di `/var/clientlibs`. Questa è una versione memorizzata nella cache dei clientlibs e verrà ricreata quando richiesto.

>[!NOTE]
>
>Questa impostazione viene configurata automaticamente per le istanze di produzione se si esegue AEM in modalità [](/help/sites-administering/production-ready.md)Produzione pronta.

**Day CQ HTTP Header Authentication Handler** Impostazioni a livello di sistema per il metodo di autenticazione di base della richiesta HTTP.

Quando utilizzate gruppi [di utenti](/help/sites-administering/cug.md) chiusi potete configurare (tra gli altri):

* **Realm HTTP**
* Pagina di accesso **predefinita**

**Day CQ Link Checker Service** Check e, se necessario, configurare:

* **Periodo** di pianificazione per definire l&#39;intervallo in cui i collegamenti esterni devono essere controllati automaticamente.

* Selezionare Intervallo **tolleranza collegamento** non valido per il periodo in cui un collegamento esterno non riuscito viene considerato non valido.
* **Sovrascrivi pattern** di controllo collegamento per definire eventuali percorsi da escludere dal controllo dei collegamenti.

**Day CQ Link Checker Task** Configura le impostazioni per una singola attività di controllo collegamenti (un’attività che controlla un collegamento esterno):

* Controllare gli intervalli definiti in **Buono intervallo** di test dei collegamenti e Intervallo di test dei collegamenti **non valido**

* I vari parametri relativi ai proxy per l&#39;accesso a Internet e NTLM che sono necessari per l&#39;accesso esterno durante il controllo di un collegamento.

**Day CQ Mail Service** Configurare il nome host e i dettagli di accesso per il server di posta. Fare riferimento alla sezione Configurazione del servizio e-mail.

**Day CQ MCM Newsletter** Configurare le varie impostazioni utilizzate con la newsletter.

**Configurazione della mappatura** radice di CQ Day:

* **Percorso** di destinazione per definire la destinazione di reindirizzamento di una richiesta a &quot; `/`&quot;.

Sono disponibili due interfacce in AEM:

* l’interfaccia touch è l’interfaccia standard
* e l&#39;interfaccia classica obsoleta è ancora completamente operativa

Utilizzando AEM mappatura radice è possibile configurare l’interfaccia che si desidera utilizzare come predefinita per l’istanza:

* Affinché l’interfaccia touch sia l’interfaccia predefinita, **Target Path** deve puntare a:

   ```
      /projects.html
   ```

* Affinché l’interfaccia classica sia l’interfaccia predefinita, il percorso **di** Target deve puntare a:

   ```
      /welcome.html
   ```

>[!NOTE]
>
>Con un’installazione standard, l’interfaccia touch è l’interfaccia predefinita.

**Adobe del gestore** autenticazione SSO Granite Configurare i dettagli SSO (Single Sign On); spesso sono necessarie nelle impostazioni di authoring aziendale, spesso in combinazione con LDAP.

Sono disponibili diverse proprietà di configurazione:

* **Percorso** Percorso per il quale il gestore di autenticazione è attivo. Se questo parametro viene lasciato vuoto, il gestore di autenticazione viene disabilitato. Ad esempio, il percorso / causa l&#39;utilizzo del gestore di autenticazione per l&#39;intero repository.

* **Il valore di classificazione del servizio** OSGi Framework Service Ranking viene utilizzato per indicare l&#39;ordine utilizzato per chiamare questo servizio. Questa è una 
`int` dove i valori più alti indicano una precedenza maggiore.
Il valore predefinito è `0`.

* **Nomi** intestazione I nomi delle intestazioni che possono contenere un ID utente.

* **Nomi** dei cookie I nomi dei cookie che possono contenere un ID utente.

* **Nomi** dei parametri I nomi dei parametri di richiesta che potrebbero fornire l&#39;ID utente.

* **Mappa** utente Per gli utenti selezionati, il nome utente estratto dalla richiesta HTTP può essere sostituito con uno diverso nell&#39;oggetto credenziali. La mappatura è definita qui. Se il nome utente 
`admin` viene visualizzata su entrambi i lati della mappa. La mappatura verrà ignorata. Tenere presente che il carattere &quot;=&quot; deve essere preceduto da un carattere &quot;\&quot; iniziale.

* **Formato** Indica il formato in cui viene fornito l&#39;ID utente. Utilizzo:

   * `Basic` se l&#39;ID utente è codificato nel formato di autenticazione di base HTTP
   * `AsIs` se l&#39;ID utente è fornito in testo normale o se qualsiasi espressione regolare applicata deve essere utilizzata come tale o qualsiasi espressione regolare

**Day CQ WCM Debug Filter** Questo è utile quando si sviluppa in quanto consente l&#39;utilizzo di suffissi come ?debug=layout quando si accede a una pagina. Ad esempio, https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layout fornirà informazioni sul layout che potrebbero interessare allo sviluppatore.

* Disattivate questa opzione nelle istanze di produzione per garantire prestazioni e protezione.

**Configurazione filtro** CQ WCM Day:

* **Modalità WCM **per definire il modo predefinito.
* In un’istanza di authoring questo potrebbe essere `edit`, `disable,preview` o `analytics`.
È possibile accedere alle altre modalità dalla barra laterale, oppure il suffisso `?wcmmode=disabled` può essere utilizzato per emulare un ambiente di produzione.

* In un’istanza di pubblicazione questo deve essere impostato in modo `disabled` da assicurare che nessun’altra modalità sia accessibile.

>[!NOTE]
>
>Questa impostazione viene configurata automaticamente per le istanze di produzione se si esegue AEM in modalità [](/help/sites-administering/production-ready.md)Produzione pronta.

**Configurazione** controllo collegamenti CQ WCM Day:

* **Elenco delle configurazioni** di riscrittura per specificare un elenco di posizioni per le configurazioni del controllo dei collegamenti basate su contenuto. Le configurazioni possono essere basate sulla modalità di esecuzione; è importante distinguere tra ambienti di creazione e pubblicazione, in quanto le impostazioni del controllo dei collegamenti possono essere diverse.

**Configurazione del processore** di pagina CQ WCM Day:

* **Percorsi**, un elenco di posizioni in cui il sistema ascolta le modifiche apportate alla pagina prima di attivare un `jcr:Event`.

**Adobe Page Impression Tracker** Per un’istanza di creazione configurate:

* **sling.auth.requirements**: imposta il valore di questa proprietà su `-/libs/wcm/stats/tracker`

>[!CAUTION]
>
>Questa configurazione consente richieste anonime al servizio di tracciamento.

>[!NOTE]
>
>Per ulteriori informazioni, consulta [Impressioni](/help/sites-deploying/configuring.md#enabling-page-impressions) pagina.

**Statistiche** pagina CQ WCM giorno Per un’istanza di pubblicazione configurare:

* **URL per l’invio di dati** per configurare l’URL utilizzato per il tracciamento delle statistiche delle pagine (è fondamentale se una richiesta di tracciamento passa attraverso il dispatcher); ad esempio, il valore predefinito è `https://localhost:4502/libs/wcm/stats/tracker`.

* **Script di tracciamento abilitato** per abilitare ( `true`) o disabilitare ( `false`) l&#39;inclusione dello script di tracciamento nelle pagine. Il valore predefinito è `false`.

>[!NOTE]
>
>Per ulteriori informazioni, consulta [Impressioni](/help/sites-deploying/configuring.md#enabling-page-impressions) pagina.

**Day CQ WCM Version Manager** Control se e come vengono gestite le versioni nel sistema:

* **Crea versione all&#39;attivazione**, abilitata in un&#39;installazione standard
* **Abilita rimozione forzata**

* **Elimina percorsi**, percorsi che verranno cercati in un’azione di ricerca
* **Percorsi** di controllo delle versioni impliciti, i percorsi in cui è attivo il controllo delle versioni implicite.

* **Massima età** versione, età massima (in giorni) di una versione

* **Numero massimo di versioni**, il numero massimo di versioni da mantenere

Per ulteriori informazioni, consulta [Scorrimento](/help/sites-deploying/version-purging.md) delle versioni.

**Servizio** di notifica e-mail flusso di lavoro Day CQ Configura le impostazioni e-mail per le notifiche inviate da un flusso di lavoro.

**Day CQSE HTTP Service** Control the CQ Servlet Engine:

* **NIO per HTTP, **Se utilizzare o meno NIO per HTTP. Valori predefiniti per true. Utilizzata solo se HTTP è abilitato.
* **Timeout connessione, **Timeout connessione in millisecondi. Questa proprietà si applica sia alle connessioni HTTP che a quelle HTTPS. Il valore predefinito è 60 secondi.

* **Abilita HTTPS,** se HTTPS è abilitato o meno. Il valore predefinito è false.
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

Consultate anche [Abilitazione di HTTP su SSL](/help/sites-administering/ssl-by-default.md) per informazioni dettagliate sulle opzioni relative a SSL e una descrizione completa su come abilitare HTTPS per CQSE.

**CQ Rewriter HTML Parser Factory**

Controlla il parser HTML per la riscrittura CQ.

* **Tag aggiuntivi da elaborare** - È possibile aggiungere o rimuovere tag HTML da elaborare dal parser. Per impostazione predefinita, vengono elaborati i seguenti tag: A,IMG,AREA,MODULO,BASE,COLLEGAMENTO,SCRIPT,CORPO,HEAD.
* **Mantieni cassa** del cammello - Per impostazione predefinita, il parser HTML converte gli attributi in caso di cammello (ad es. eBay) in lettere maiuscole (ad es. ebay). È possibile disattivare questa opzione per mantenere gli attributi della cassa del cammello. Questa funzione è utile quando si utilizzano strutture frontali come Angular 2.

**Day Commons JDBC Connection Pool** Configura l&#39;accesso a un database esterno utilizzato come origine per il contenuto.

Questa è una configurazione di fabbrica, in modo che possano essere configurate più istanze.

**Adobe CQ Media DPS Sessions Service** Gestire le sessioni DPS da utilizzare con le pubblicazioni.

In particolare, potete definire `dps.session.service.url.name`: il valore predefinito è [https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions](https://dpsapi2.digitalpublishing.acrobat.com/webservices/sessions)

**La comunicazione CDN** Rewriter tra AEM e CDN deve essere garantita in modo che le risorse/i file binari vengano consegnati all’utente finale in modo sicuro. Sono necessarie due attività:

* Accesso alla risorsa da AEM tramite CDN la prima volta (o dopo la scadenza nella cache).
* Accedere alla risorsa nella cache CDN in modo sicuro, dal momento che una volta che la risorsa è memorizzata nella cache CDN, la richiesta non verrà AEM e tutti gli utenti che hanno accesso a tale risorsa dovranno essere serviti dalla rete CDN.

AEM riscrittura degli URL delle risorse interne agli URL CDN esterni. Riscrive i collegamenti da trasmettere alla CDN, inclusa una firma JWS, e il tempo di scadenza per consentire l’accesso sicuro alla risorsa. Questa funzione deve essere utilizzata per le istanze di authoring.

Il flusso complessivo è il seguente:

1. L’utente si autentica con AEM e richiede una pagina con risorse.
1. La pagina richiesta contiene una risorsa simile a `/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png`
1. Rewriter trasforma il collegamento a un URL CDN contenente una firma JWS:
   `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`

1. Il browser dell’utente inoltra la richiesta di risorse al server CDN
1. La rete CDN deve essere configurata per inoltrare la richiesta al AEM insieme al `cdn_sign` parametro.
1. Un gestore di autenticazione convalida il `cdn_sign` parametro e restituisce la risorsa alla rete CDN che viene quindi consegnata all’utente

Il flusso tra il browser dell&#39;utente, la CDN e AEM può essere visualizzato come segue.

![chlimage_1-8](assets/chlimage_1-8.png)

>[!NOTE]
>
>Al momento questa funzione è abilitata solo per AEM istanze dell’autore.

**CDNConfigServiceImpl** Fornisce le configurazioni CDN

La funzione di riscrittura CDN può essere attivata fornendo il nome **del dominio di distribuzione** CDN nella configurazione per com.adobe.cq.cdn.rewriter.impl.CDNConfigServiceImpl.

Il servizio contiene anche altre opzioni di configurazione come abilitare/disabilitare la riscrittura CDN, i prefissi di percorso per i quali viene eseguita la riscrittura CDN, i valori TTL e il protocollo (HTTP o HTTPS).

**CDNRewriter** Una riscrittura per la riscrittura degli URL immagine interni agli URL CDN

È possibile definire il valore **Tag Attributes** in com.adobe.cq.cdn.rewriter.impl.CDNRewriter in modo che vengano riscritti solo i collegamenti immagine selettivi.
