---
title: Concetti di configurazione di base
seo-title: Concetti di configurazione di base
description: Scopri come configurare AEM.
seo-description: Scopri come configurare AEM.
uuid: edcdd4bd-5917-417e-8913-40d488383ea9
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 2673ea92-1651-4b1b-9aac-f4ba8b36782e
translation-type: tm+mt
source-git-commit: 8f35717324cd2c1524fb2cf931b3ce21be05729a
workflow-type: tm+mt
source-wordcount: '2132'
ht-degree: 1%

---


# Concetti di configurazione di base{#basic-configuration-concepts}

Adobe Experience Manager (AEM) è installato con le impostazioni predefinite per tutti i parametri che gli consentono di eseguire &quot;out of the box&quot;. Tuttavia, puoi configurare AEM per i tuoi requisiti specifici.

Sono disponibili diversi aspetti di AEM che possono essere configurati:

* Alcuni sono [comunemente configurati per ogni installazione di progetto](#primary-configuration-considerations) e devono essere revisionati per confermare se sono o meno applicabili al progetto.
* [Ulteriori ](#further-configuration-considerations) configurazioni possono essere comuni ma non obbligatorie; relative alle funzioni, oppure alle prestazioni e alla stabilità del sistema.
* Altri sono richiesti solo per alcune funzioni opzionali di AEM (documentate insieme alla funzione appropriata).

A seconda della configurazione specifica, queste modifiche possono essere effettuate utilizzando:

* **della console Web di Adobe CQ**

   Si tratta di una posizione standard per la configurazione dei bundle e dei servizi OSGi.

   Per ulteriori informazioni e procedure consigliate, vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md).

* **Archivio**

   Un sottoinsieme di configurazioni OSGi è disponibile nella directory archivio. In questo modo, copiando o replicando i contenuti del repository si ricreano configurazioni identiche. È inoltre possibile aggiungere configurazioni personalizzate, a seconda della modalità di esecuzione, alla directory archivio.

   Per ulteriori informazioni, vedere [Configurazione OSGi nell&#39;archivio](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) e in particolare [Aggiunta di una nuova configurazione all&#39;archivio](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository).

* **File system**

   Alcuni file di configurazione risiedono nel file system.

* **WCM AEM**

   Diversi aspetti possono essere configurati all&#39;interno AEM WCM stesso, molti dei quali utilizzando la console [Strumenti](/help/sites-administering/tools-consoles.md); ad esempio, agenti di replica.

>[!NOTE]
>
>Quando lavorate con Adobe Experience Manager, esistono diversi metodi per gestire le impostazioni di configurazione per i servizi OSGi (nodi console o repository).
>
>Per informazioni dettagliate, vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md).

>[!NOTE]
>
>La configurazione AEM è semplice, ma è necessario essere consapevoli che:
>
>Alcune modifiche possono avere un impatto importante sulle applicazioni. Per questo motivo, accertati di disporre dell’esperienza e delle conoscenze necessarie prima di iniziare a configurare AEM e di apportare solo le modifiche che sai essere necessarie. Eventuali modifiche effettuate tramite la console OSGi vengono applicate al sistema in esecuzione **immediatamente** (non è necessario riavviare il sistema).

## Considerazioni sulla configurazione principale {#primary-configuration-considerations}

Questo elenco descrive le aree principali comunemente configurate per ogni nuovo progetto. Non tutti sono necessari, ma l&#39;elenco deve essere letto e rivisto per vedere cosa è applicabile al progetto.

L&#39;elenco fornisce una breve panoramica di ogni aspetto della configurazione, insieme ai collegamenti alle pagine che forniscono dettagli completi.

### Elenco di controllo protezione {#security-checklist}

Diversi problemi di configurazione chiave sono elencati nella [lista di controllo della sicurezza](/help/sites-administering/security-checklist.md). Accertarsi di leggere questo documento e di intraprendere le azioni necessarie per l&#39;installazione.

### Configurazione dell&#39;interfaccia utente predefinita - Ottimizzato per il tocco o Classic {#configuring-the-default-ui-touch-optimized-or-classic}

Sono disponibili due interfacce AEM:

* Interfaccia touch
* L&#39;interfaccia classica

È possibile configurare l&#39;interfaccia utente richiesta utilizzando [Mappatura radice](/help/sites-deploying/osgi-configuration-settings.md).

>[!NOTE]
>
>Ulteriori informazioni sulla selezione dell&#39;interfaccia sono disponibili in [Selezione dell&#39;interfaccia utente](/help/sites-authoring/select-ui.md).

### IPv4 e IPv6 {#ipv-and-ipv}

Tutti gli elementi di AEM (ad es. archivio, Dispatcher, ecc.) possono essere installati nelle reti IPv4 e IPv6.

Il funzionamento è semplice in quanto non è necessaria alcuna configurazione speciale, se necessario è possibile specificare semplicemente un indirizzo IP utilizzando il formato appropriato per il tipo di rete.

Ciò significa che, quando è necessario specificare un indirizzo IP, è possibile selezionare (come richiesto) da:

* un indirizzo IPv6

   ad esempio `https://[ab12::34c5:6d7:8e90:1234]:4502`

* un indirizzo IPv4

   ad esempio `https://123.1.1.4:4502`

* un nome server

   ad esempio, `https://www.yourserver.com:4502`

* il caso predefinito di `localhost` verrà interpretato per le installazioni di rete IPv4 e IPv6

   ad esempio, `http://localhost:4502`

### Rimozione delle versioni {#version-purging}

In un’installazione standard AEM creare una nuova versione di una pagina o di un nodo ogni volta che si attiva una pagina (dopo l’aggiornamento del contenuto). È inoltre possibile creare versioni aggiuntive su richiesta utilizzando la scheda **Gestione versioni** della barra laterale. Tutte queste versioni sono memorizzate nella directory archivio e possono essere ripristinate se necessario.

Queste versioni non vengono mai eliminate, pertanto la dimensione del repository aumenterà nel tempo e dovrà essere gestita.

Per informazioni dettagliate, consultate [Version Purging](/help/sites-deploying/version-purging.md), in particolare [Version Manager](/help/sites-deploying/version-purging.md#version-manager) per informazioni dettagliate su come configurare AEM per eliminare le versioni precedenti al momento della creazione di una nuova versione.

### Registrazione {#logging}

AEM offre la possibilità di configurare:

* parametri globali per il servizio di registrazione centrale
* richiedere la registrazione dei dati; una configurazione di registrazione specializzata per le informazioni di richiesta
* impostazioni specifiche per i singoli servizi; ad esempio, un singolo file di registro e un formato per i messaggi di registro

Per informazioni dettagliate, vedere [Registrazione](/help/sites-deploying/configure-logging.md).

### Modalità di esecuzione {#run-modes}

Le modalità di esecuzione consentono di sintonizzare l’istanza di AEM per uno scopo specifico; ad esempio autore o pubblicazione, test, sviluppo o Intranet, ecc.

Questo viene fatto definendo raccolte di parametri di configurazione per ogni modalità di esecuzione. Per tutte le modalità di esecuzione viene applicato un set di parametri di configurazione di base, che consente di sintonizzare ulteriori set in base alle esigenze specifiche dell&#39;ambiente. Questi vengono quindi applicati secondo necessità.

Tutte le impostazioni di configurazione sono memorizzate nell&#39;unico repository e attivate impostando la **Modalità di esecuzione**.

Per informazioni dettagliate, vedere [Modalità di esecuzione](/help/sites-deploying/configure-runmodes.md).

### Single Sign On {#single-sign-on}

Single Sign On (SSO) consente a un utente di accedere a più sistemi dopo aver fornito le credenziali di autenticazione (ad esempio un nome utente e una password) una volta. Un sistema separato (noto come autenticatore affidabile) esegue l&#39;autenticazione e fornisce  Experience Manager con le credenziali utente.  Experience Manager verifica e applica le autorizzazioni di accesso per l’utente (ossia determina a quali risorse l’utente può accedere).

Per ulteriori informazioni, vedere [Single Sign On](/help/sites-deploying/single-sign-on.md).

### Mapping risorse {#resource-mapping}

La mappatura delle risorse viene utilizzata per definire reindirizzamenti, URL personalizzati e host virtuali per AEM.

Ad esempio, è possibile utilizzare queste mappature per:

* Aggiungi un prefisso a tutte le richieste con `/content` in modo che la struttura interna sia nascosta ai visitatori del sito Web.
* Definite un reindirizzamento in modo che tutte le richieste alla pagina `/content/en/gateway` del sito Web vengano reindirizzate a `https://gbiv.com/`.

Per ulteriori informazioni, vedere [Mappatura risorse](/help/sites-deploying/resource-mapping.md).

### Replica, agenti replica inversa e replica {#replication-reverse-replication-and-replication-agents}

Gli agenti di replica sono fondamentali per AEM come meccanismo utilizzato per:

* [Pubblicare (attivare) ](/help/sites-authoring/publishing-pages.md) il contenuto da un autore a un ambiente di pubblicazione.
* Elimina esplicitamente il contenuto dalla cache del dispatcher.
* Restituire l’input dell’utente (ad esempio, l’input del modulo) dall’ambiente di pubblicazione all’ambiente di authoring (controllato dall’ambiente di authoring).

Per ulteriori dettagli, vedere [Replica](/help/sites-deploying/replication.md).

### Impostazioni di configurazione OSGi {#osgi-configuration-settings}

[](https://www.osgi.org/) OSGiè un elemento fondamentale nello stack tecnologico di AEM. Viene utilizzato per controllare i bundle compositi di AEM e la loro configurazione.

Per un elenco dei vari bundle rilevanti per l&#39;implementazione del progetto, consultate [Impostazioni di configurazione OSGi](/help/sites-deploying/osgi-configuration-settings.md) (elencati in base al bundle). Non tutte le impostazioni elencate devono essere regolate, alcune sono menzionate per aiutarvi a capire come AEM funziona.

Quando lavorate con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; per ulteriori informazioni e procedure consigliate, vedere [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md).

### Configurazione di LDAP {#configuring-ldap}

L’autenticazione LDAP è necessaria per autenticare gli utenti memorizzati in una directory LDAP (centrale) come Active Directory. Questo consente di ridurre gli sforzi necessari per gestire gli account utente.

L’autenticazione LDAP viene eseguita a livello di repository, pertanto viene gestita direttamente dall’archivio. Per ulteriori dettagli, consultate [Configurazione di LDAP con AEM](/help/sites-administering/ldap-config.md).

Per la gestione degli utenti in AEM (inclusa l&#39;assegnazione dei diritti di accesso), vedete [Amministrazione utente e sicurezza](/help/sites-administering/security.md).

### Configurazione del dispatcher {#configuring-the-dispatcher}

Dispatcher è uno strumento di cache e/o bilanciamento del carico Adobe Experience Manager che può essere utilizzato insieme a un server Web di classe enterprise.

Per ulteriori informazioni, vedere [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html), in particolare [Configuring the Dispatcher](https://helpx.adobe.com/it/experience-manager/dispatcher/using/dispatcher-configuration.html).

### Configurazione AEM connettore LiveCycle {#configuring-aem-livecycle-connector}

Con il rilascio dei servizi AEM Doc e AEM Doc Security, ora è possibile richiamare i servizi LiveCycle doc per eseguire il rendering di un modulo XFA, convertire un documento in PDF e proteggere un documento tramite criterio. Per ulteriori informazioni, leggere [AEM connettore LiveCycle](https://helpx.adobe.com/livecycle/help/aem/aem-livecycle-connector.html).

### Download e amministrazione della topologia del processo {#job-offloading-and-topology-administration}

[](/help/sites-deploying/offloading.md) Offload distribuisce le attività di elaborazione  istanze di Experienci Manager in una topologia. Con lo scaricamento, potete utilizzare istanze di Experienci Manager  specifiche per eseguire specifici tipi di elaborazione. L&#39;elaborazione specializzata consente di ottimizzare l&#39;utilizzo delle risorse server disponibili.

Le topologie sono cluster di Experienci Manager  a accoppiamento approssimativo che partecipano allo scarico. Un cluster è costituito da una o più istanze  server di Experience Manager (una singola istanza è considerata un cluster).

Per ulteriori informazioni su come visualizzare o modificare l&#39;appartenenza alla topologia, consultare la sezione [Amministrazione delle topologie](/help/sites-deploying/offloading.md#administering-topologies).

### Configurazione della console di benvenuto {#configuring-the-welcome-console}

La console Benvenuto nell’interfaccia classica offre un elenco di collegamenti alle varie console e funzionalità presenti in AEM.

È possibile configurare i collegamenti visibili. Per ulteriori informazioni, vedere [Configurazione della console di benvenuto](/help/sites-developing/customizing-the-welcome-console.md).

### Configurazione per prestazioni {#configuring-for-performance}

[Le ](/help/sites-deploying/configuring-performance.md) prestazioni sono la chiave del progetto. Alcuni aspetti di AEM (e/o del repository sottostante) possono essere configurati per ottimizzare le prestazioni.

Per ulteriori informazioni, vedere [Configurazione per Performance](/help/sites-deploying/configuring-performance.md#configuring-for-performance).

<!--delete ### Scaling {#scaling}

Scaling a CQ installation correctly depends greatly on the details of your particular use case. A detailed discussion of solution patterns for various situations can be found in [Scaling CQ](/help/sites-deploying/scaling.md).-->

### Archivio dati condiviso {#shared-data-store}

L&#39;archivio dati dell&#39;archivio viene utilizzato per scaricare l&#39;archivio dei file binari di grandi dimensioni dall&#39;archivio proprio in un&#39;area separata, in modo che più istanze dello stesso binario (ad esempio un&#39;immagine) all&#39;interno della struttura dell&#39;archivio vengano archiviate solo una volta.

Questa funzione &quot;store-once, reference-many&quot; può essere estesa non solo a un unico archivio ad albero, ma anche a repository completamente separati, configurando l&#39;archivio dati di ciascuno per fare riferimento alla stessa posizione del file system condiviso.

Tale archivio di dati può essere condiviso tra nodi diversi nello stesso cluster, istanze di pubblicazione e/o creazione diverse nella stessa installazione o addirittura istanze completamente separate in installazioni diverse.

Per ulteriori informazioni, vedere [Configurazione di archivi dati e archivi nodo](/help/sites-deploying/data-store-config.md).

## Ulteriori considerazioni sulla configurazione {#further-configuration-considerations}

### Abilitazione di HTTP su SSL {#enabling-http-over-ssl}

È possibile abilitare HTTP su SSL per utilizzare connessioni più sicure ai server.

Per ulteriori informazioni, vedere [Abilitazione di HTTP su SSL](/help/sites-administering/ssl-by-default.md).

### Portali AEM e portlet {#aem-portals-and-portlets}

Un portale è un&#39;applicazione Web che offre personalizzazione, single sign-on, integrazione dei contenuti da origini diverse e ospita il livello di presentazione dei sistemi informativi. Il componente portlet consente inoltre di incorporare una portlet nella pagina. Per accedere al contenuto fornito da CQ5 WCM, il server portale può essere dotato del Portlet Director CQ5 Portal. A tale scopo, è possibile installare, configurare e aggiungere il portlet alla pagina del portale.

Per ulteriori informazioni, vedere [Portale e portlet](/help/sites-administering/aem-as-portal.md).

### Scadenza degli oggetti statici {#expiration-of-static-objects}

Gli oggetti statici (ad esempio, le icone) non vengono modificati. Pertanto, il sistema deve essere configurato in modo che non scada (per un periodo di tempo ragionevole) e quindi riduca il traffico inutile.

Per ulteriori informazioni, vedere [Scadenza di oggetti statici](/help/sites-deploying/expiration-static-objects.md).

### Aprire i file nel processo Java {#open-files-in-the-java-process}

Ogni processo Java può accedere ai file, che richiede risorse di sistema. Per questo motivo viene definito un limite superiore relativo al numero di file a cui ogni processo può accedere contemporaneamente. Se questo viene superato, può verificarsi un errore di eccezione.

Se il processo di AEM supera questo limite massimo, il messaggio &quot; `too many open files`&quot; verrà visualizzato in `error.log`.

Per evitare tali eccezioni è necessario:

1. Controllate quanti file aperti vengono usati dal processo di AEM.

   La modalità di esecuzione di questo controllo dipende dalla piattaforma su cui viene eseguita l&#39;istanza. È possibile utilizzare utility quali lsof (Unix) o Process Explorer (Windows).

   Questo valore deve essere monitorato durante lo sviluppo e il test per:

   * confermare la chiusura dei file come necessario
   * per determinare il valore massimo necessario (in varie circostanze)

1. Impostare il massimo consentito.

   Il nuovo valore dovrebbe tener conto sia delle esigenze attuali che di eventuali picchi futuri, per cui è consigliabile raddoppiare le esigenze attuali.

   Per impostazione predefinita, `serverctl` configura `CQ_MAX_OPEN_FILES` in `8192`; questo dovrebbe essere sufficiente per la maggior parte degli scenari.

### Configurazione dell&#39;editor Rich Text {#configuring-the-rich-text-editor}

L&#39; **Editor Rich Text** (**RTE**) offre agli autori un&#39;ampia gamma di [funzionalità](/help/sites-authoring/rich-text-editor.md) per la modifica del contenuto testuale; fornendo loro icone, caselle di selezione e menu per un&#39;esperienza WYSIWYG.

Per ulteriori informazioni, vedere [Configurazione dell&#39;editor Rich Text](/help/sites-administering/rich-text-editor.md).

### Configurazione dell&#39;annullamento per la modifica delle pagine {#configuring-undo-for-page-editing}

Esistono diverse proprietà che controllano il funzionamento dei comandi Annulla e Ripristina per la modifica delle pagine. Per ulteriori informazioni, vedere [Configurazione dell&#39;annullamento per la modifica delle pagine](/help/sites-administering/config-undo.md).

### Configurazione del componente video {#configuring-the-video-component}

Il [componente Video](/help/sites-authoring/default-components-foundation.md#video) consente di inserire un elemento video predefinito e predefinito nella pagina.

Tenete presente che, per una transcodifica corretta, è necessario installare separatamente [FFmpeg. ](/help/sites-administering/config-video.md#install-ffmpeg) Possono inoltre [Configurare i profili video](/help/sites-administering/config-video.md#configure-video-profiles) per l&#39;utilizzo con gli elementi html5.

### Configurazione e personalizzazione dei report {#configuring-and-customizing-reports}

Per monitorare e analizzare lo stato dell’istanza, CQ offre una selezione di rapporti predefiniti che possono essere configurati in base alle esigenze specifiche dell’utente:

Per ulteriori informazioni, vedere [Nozioni di base sulla personalizzazione dei report](/help/sites-administering/reporting.md#the-basics-of-report-customization).

### Configurazione della notifica e-mail {#configuring-email-notification}

CQ invia notifiche e-mail agli utenti che:

* Hanno effettuato la sottoscrizione a eventi di pagina, ad esempio modifiche o replica.
* Hanno effettuato la sottoscrizione agli eventi forum.
* Eseguire un passaggio in un flusso di lavoro.

Per ulteriori informazioni, vedere [Configurazione delle notifiche e-mail](/help/sites-administering/notification.md).

### Abilitazione delle impression pagina {#enabling-page-impressions}

Le impression pagina vengono visualizzate nella colonna **Impression** della classica console di amministrazione del sito dell&#39;interfaccia utente. Per attivare l’acquisizione delle impression della pagina è necessario configurare:

* Nell’istanza di pubblicazione:

   * [Statistiche pagina CQ WCM giorno](/help/sites-deploying/osgi-configuration-settings.md)

* Nell’istanza di creazione:

   * [ Adobe - Tracciamento impression pagina](/help/sites-deploying/osgi-configuration-settings.md)

>[!CAUTION]
>
>La configurazione di  Adobe Page Impression Tracker nell&#39;ambiente di authoring consentirà richieste anonime al servizio di tracciamento.

