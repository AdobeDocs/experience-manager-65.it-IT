---
title: Concetti di base sulla configurazione
description: Scopri come configurare Adobe Experience Manager per i tuoi requisiti specifici.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: 3777a1ba-cc4e-41b9-9098-236f8141925f
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2116'
ht-degree: 1%

---

# Concetti di base sulla configurazione{#basic-configuration-concepts}

Adobe Experience Manager (AEM) viene installato con le impostazioni predefinite per tutti i parametri che consentono l’esecuzione &quot;pronta all’uso&quot;. Tuttavia, puoi configurare l’AEM in base a esigenze specifiche.

Ci sono molti aspetti dell&#39;AEM che possono essere configurati:

* Alcuni sono [di solito configurato per ogni installazione del progetto](#primary-configuration-considerations) e devono essere rivisti per confermare se sono applicabili al tuo progetto.
* [Altre configurazioni](#further-configuration-considerations) possono essere comuni ma non obbligatori, relativi a caratteristiche o prestazioni e stabilità del sistema.
* Altre sono necessarie solo per determinate funzioni facoltative dell’AEM (documentate insieme alla funzione appropriata).

A seconda della configurazione specifica, queste modifiche possono essere apportate utilizzando:

* **Console web di Adobe CQ**

  Si tratta di una posizione standard per la configurazione di bundle e servizi OSGi.

  Consulta [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per ulteriori dettagli e pratiche consigliate.

* **Archivio**

  Nell’archivio è disponibile un sottoinsieme di configurazioni OSGi. In questo modo, la copia o la replica del contenuto dell’archivio ricrea configurazioni identiche. Puoi anche aggiungere all’archivio le tue configurazioni, a seconda della modalità di esecuzione.

  Consulta [Configurazione OSGi nell’archivio](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) e in particolare [Aggiunta di una nuova configurazione all’archivio](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository) per ulteriori dettagli.

* **File system**

  Alcuni file di configurazione risiedono nel file system.

* **WCM AEM**

  È possibile configurare vari aspetti all’interno di AEM WCM stesso, molti dei quali utilizzando [Strumenti](/help/sites-administering/tools-consoles.md) ad esempio gli agenti di replica.

>[!NOTE]
>
>Quando si lavora con Adobe Experience Manager, sono disponibili diversi metodi di gestione delle impostazioni di configurazione per i servizi OSGi (nodi della console o dell’archivio).
>
>Consulta [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per informazioni dettagliate.

>[!NOTE]
>
>La configurazione dell’AEM è semplice. Tuttavia, tieni presente che alcune modifiche possono avere un impatto importante sulle applicazioni. Per questo motivo, assicurati di disporre dell’esperienza e delle conoscenze necessarie prima di iniziare a configurare l’AEM e di apportare solo le modifiche che sai essere necessarie. Eventuali modifiche apportate tramite la console OSGi sono **immediatamente** applicato al sistema in esecuzione (non è richiesto alcun riavvio).

## Considerazioni sulla configurazione primaria {#primary-configuration-considerations}

Questo elenco descrive le aree principali che sono comunemente configurate per ogni nuovo progetto. Non tutti sono necessari, ma l’elenco deve essere letto e rivisto per vedere cosa è applicabile al progetto.

L’elenco offre una breve panoramica di ogni aspetto della configurazione, con collegamenti alle pagine che forniscono dettagli completi.

### Elenco di controllo della sicurezza {#security-checklist}

Diversi problemi di configurazione chiave sono elencati in [Elenco di controllo della sicurezza](/help/sites-administering/security-checklist.md). Assicurarsi di leggere questo documento e di eseguire tutte le azioni necessarie per l&#39;installazione.

### Configurazione dell’interfaccia utente predefinita: touch o classica {#configuring-the-default-ui-touch-optimized-or-classic}

Sono disponibili due interfacce utente per l’utilizzo in AEM:

* Interfaccia touch
* Interfaccia classica

Puoi configurare l’interfaccia utente necessaria utilizzando [Mappatura radice](/help/sites-deploying/osgi-configuration-settings.md).

>[!NOTE]
>
>Ulteriori informazioni sulla selezione dell’interfaccia utente sono disponibili in [Selezione dell’interfaccia utente](/help/sites-authoring/select-ui.md).

### IPv4 e IPv6 {#ipv-and-ipv}

Tutti gli elementi dell’AEM (ad esempio, l’archivio e Dispatcher) possono essere installati nelle reti IPv4 e IPv6.

Il funzionamento è semplice in quanto non è richiesta alcuna configurazione speciale; quando necessario, è sufficiente specificare un indirizzo IP utilizzando il formato appropriato al tipo di rete in uso.

Ciò significa che, quando è necessario specificare un indirizzo IP, è possibile selezionare (come richiesto) tra:

* un indirizzo IPv6

  ad esempio, `https://[ab12::34c5:6d7:8e90:1234]:4502`

* un indirizzo IPv4

  ad esempio, `https://123.1.1.4:4502`

* un nome server

  ad esempio, `https://www.yourserver.com:4502`

* il caso predefinito di `localhost` verrà interpretato per le installazioni di rete IPv4 e IPv6

  ad esempio, `http://localhost:4502`

### Rimozione versione {#version-purging}

In un’installazione standard, AEM crea una versione di una pagina o di un nodo ogni volta che attivi una pagina (dopo l’aggiornamento del contenuto). Puoi anche creare versioni aggiuntive su richiesta utilizzando **Controllo delle versioni** della barra laterale. Tutte queste versioni vengono memorizzate nell’archivio e possono essere ripristinate, se necessario.

Queste versioni non vengono mai eliminate, pertanto le dimensioni dell’archivio aumentano nel tempo e devono quindi essere gestite.

Consulta [Rimozione versione](/help/sites-deploying/version-purging.md) per maggiori dettagli, in particolare [Gestione versioni](/help/sites-deploying/version-purging.md#version-manager) per informazioni dettagliate su come configurare AEM per eliminare le versioni precedenti quando viene creata una nuova versione.

### Registrazione {#logging}

L’AEM ti offre la possibilità di configurare:

* parametri globali per il servizio di registrazione centrale
* richiedere la registrazione dei dati; una configurazione di registrazione specializzata per le informazioni sulla richiesta
* impostazioni specifiche per i singoli servizi; ad esempio, un singolo file di registro e un formato per i messaggi di registro

Consulta [Registrazione](/help/sites-deploying/configure-logging.md) per informazioni dettagliate.

### Modalità di esecuzione {#run-modes}

Le modalità di esecuzione consentono di regolare l’istanza AEM per uno scopo specifico. Ad esempio, creazione o pubblicazione, test, sviluppo o Intranet e così via.

A tal fine, si definiscono insiemi di parametri di configurazione per ogni modalità di esecuzione. Un set di base di parametri di configurazione viene applicato a tutte le modalità di esecuzione e puoi quindi regolare altri set in base allo scopo dell’ambiente specifico. Queste vengono quindi applicate come richiesto.

Tutte le impostazioni di configurazione vengono memorizzate in un unico repository e attivate impostando **Modalità di esecuzione**.

Consulta [Modalità di esecuzione](/help/sites-deploying/configure-runmodes.md) per informazioni dettagliate.

### Single Sign-On {#single-sign-on}

Single Sign-On (SSO) consente a un utente di accedere a più sistemi dopo aver fornito le credenziali di autenticazione, ad esempio un nome utente e una password. L&#39;autenticazione viene eseguita da un sistema separato, denominato autenticatore attendibile, che fornisce agli Experienci Manager le credenziali utente. Experience Manager verifica e applica le autorizzazioni di accesso per l’utente (ovvero, determina quali risorse l’utente può accedere).

Consulta [Single Sign-On](/help/sites-deploying/single-sign-on.md) per ulteriori dettagli.

### Mappatura delle risorse {#resource-mapping}

La mappatura delle risorse viene utilizzata per definire reindirizzamenti, URL personalizzati e host virtuali per l’AEM.

Ad esempio, puoi utilizzare queste mappature per:

* Aggiungi il prefisso a tutte le richieste `/content` in modo che la struttura interna sia nascosta ai visitatori del sito web.
* Definisci un reindirizzamento in modo che tutte le richieste a `/content/en/gateway` pagina del sito web vengono reindirizzati a `https://gbiv.com/`.

Consulta [Mappatura delle risorse](/help/sites-deploying/resource-mapping.md) per ulteriori dettagli.

### Agenti di replica, replica inversa e replica {#replication-reverse-replication-and-replication-agents}

Gli agenti di replica sono centrali per l’AEM in quanto il meccanismo utilizzato per:

* [Pubblica (attiva)](/help/sites-authoring/publishing-pages.md) contenuti da un ambiente di authoring a uno di pubblicazione.
* Svuota esplicitamente il contenuto dalla cache di Dispatcher.
* Restituisce l’input dell’utente (ad esempio, l’input del modulo) dall’ambiente di pubblicazione all’ambiente di authoring (sotto il controllo dell’ambiente di authoring).

Per ulteriori dettagli, consulta [Replica](/help/sites-deploying/replication.md).

### Impostazioni configurazione OSGi {#osgi-configuration-settings}

[OSGi](https://www.osgi.org/) è un elemento fondamentale nello stack tecnologico dell’AEM. Viene utilizzato per controllare i bundle compositi dell&#39;AEM e la loro configurazione.

Consulta [Impostazioni di configurazione OSGi](/help/sites-deploying/osgi-configuration-settings.md) per un elenco dei vari bundle rilevanti per l’implementazione del progetto (elencati per bundle). Non tutte le impostazioni elencate devono essere regolate, alcune sono menzionate per aiutarti a capire come funziona l&#39;AEM.

Quando si lavora con l’AEM, esistono diversi metodi per gestire le impostazioni di configurazione per tali servizi; vedi [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) per ulteriori dettagli e le pratiche consigliate.

### Configurazione di LDAP {#configuring-ldap}

L&#39;autenticazione LDAP è necessaria per autenticare gli utenti archiviati in una directory LDAP (centrale) come Active Directory. Questo consente di ridurre lo sforzo necessario per gestire gli account utente.

L’autenticazione LDAP si verifica a livello di repository, pertanto viene gestita direttamente dall’archivio. Per maggiori dettagli, vedi [Configurazione di LDAP con AEM](/help/sites-administering/ldap-config.md).

Per la gestione degli utenti all’interno dell’AEM (inclusa l’assegnazione dei diritti di accesso), consulta [Amministrazione utenti e sicurezza](/help/sites-administering/security.md).

### Configurazione del Dispatcher {#configuring-the-dispatcher}

Dispatcher è lo strumento di Adobe Experience Manager per la memorizzazione in cache, il bilanciamento del carico o entrambi. Può essere utilizzato con un server web di classe enterprise.

Consulta [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=it) per maggiori dettagli, in particolare [Configurazione del Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=it) per ulteriori dettagli sulla configurazione.

### Configurazione del connettore di LiveCycle AEM {#configuring-aem-livecycle-connector}

Con il rilascio dei servizi di documentazione AEM e della sicurezza dei documenti AEM, l&#39;AEM ha ora la capacità di richiamare i servizi di documentazione di LiveCycle per eseguire il rendering di un modulo XFA, convertire un documento in PDF e proteggere un documento tramite policy. Consulta [Connettore LiveCycle AEM](https://helpx.adobe.com/livecycle/help/aem/aem-livecycle-connector.html) per ulteriori dettagli.

### Offload dei processi e amministrazione della topologia {#job-offloading-and-topology-administration}

[Offload](/help/sites-deploying/offloading.md) distribuisce le attività di elaborazione tra le istanze Experienci Manager in una topologia. L&#39;offload consente di utilizzare istanze di Experience Manager specifiche per l&#39;esecuzione di tipi specifici di elaborazione. L&#39;elaborazione specializzata consente di ottimizzare l&#39;utilizzo delle risorse server disponibili.

Le topologie sono cluster Experienci Manager liberamente accoppiati che partecipano all&#39;offload. Un cluster è costituito da una o più istanze del server di Experience Manager (una singola istanza viene considerata un cluster).

Per ulteriori informazioni su come visualizzare o modificare l&#39;appartenenza alla topologia, consultare [Amministrazione delle topologie](/help/sites-deploying/offloading.md#administering-topologies) sezione.

### Configurazione della console di benvenuto {#configuring-the-welcome-console}

La console Benvenuti dell’interfaccia classica fornisce un elenco di collegamenti alle varie console e funzionalità dell’AEM.

È possibile configurare i collegamenti visibili, vedi [Configurazione della console di benvenuto](/help/sites-developing/customizing-the-welcome-console.md) per ulteriori dettagli.

### Configurazione per le prestazioni {#configuring-for-performance}

[Prestazioni](/help/sites-deploying/configuring-performance.md) è la chiave del tuo progetto. Alcuni aspetti dell’AEM (e/o dell’archivio sottostante) possono essere configurati per ottimizzare le prestazioni.

Consulta [Configurazione per le prestazioni](/help/sites-deploying/configuring-performance.md#configuring-for-performance) per ulteriori dettagli.

<!--delete ### Scaling {#scaling}

Scaling a CQ installation correctly depends greatly on the details of your particular use case. A detailed discussion of solution patterns for various situations can be found in [Scaling CQ](/help/sites-deploying/scaling.md).-->

### Archivio dati condiviso {#shared-data-store}

L’archivio dati del repository viene utilizzato per scaricare l’archiviazione di file binari di grandi dimensioni dal repository specifico di un’area separata, in modo che più istanze dello stesso file binario (ad esempio un’immagine) all’interno della struttura del repository vengano memorizzate una sola volta.

Questa funzione &quot;store-once, reference-many-times&quot; può essere estesa per servire non solo una singola struttura dell’archivio ma archivi completamente separati, configurando l’archivio dati di ciascuno di essi in modo che faccia riferimento alla stessa posizione del file system condiviso.

Tale archivio dati può essere condiviso tra nodi diversi nello stesso cluster, istanze di pubblicazione e/o authoring diverse nella stessa installazione o istanze completamente separate in installazioni diverse.

Per ulteriori informazioni, consulta [Configurazione degli archivi dati e degli archivi nodi](/help/sites-deploying/data-store-config.md).

## Ulteriori considerazioni sulla configurazione {#further-configuration-considerations}

### Abilitazione di HTTP su SSL {#enabling-http-over-ssl}

Puoi abilitare HTTP su SSL per utilizzare connessioni più sicure ai server.

Consulta [Abilitazione di HTTP su SSL](/help/sites-administering/ssl-by-default.md) per ulteriori dettagli.

### Portali e portlet AEM {#aem-portals-and-portlets}

Un portale è un&#39;applicazione Web che offre personalizzazione, Single Sign-On, integrazione di contenuti da origini diverse e ospita il livello di presentazione dei sistemi informativi. Il componente portlet consente inoltre di incorporare un portlet sulla pagina. Per accedere al contenuto fornito da CQ5 WCM, il server portale può essere dotato del portlet Director del portale CQ5. Per eseguire questa operazione, installare, configurare e aggiungere il portlet alla pagina del portale.

Consulta [Portale e portlet](/help/sites-administering/aem-as-portal.md) per ulteriori dettagli.

### Scadenza degli oggetti statici {#expiration-of-static-objects}

Gli oggetti statici, ad esempio le icone, non vengono modificati. Pertanto, il sistema deve essere configurato in modo che non scadano (per un periodo di tempo ragionevole) e in modo da ridurre il traffico non necessario.

Consulta [Scadenza degli oggetti statici](/help/sites-deploying/expiration-static-objects.md) per ulteriori dettagli.

### File aperti nel processo Java™ {#open-files-in-the-java-process}

Ogni processo Java™ può accedere ai file, il che richiede risorse di sistema. Per questo motivo, viene definito un limite massimo per il numero di file a cui ogni processo può accedere contemporaneamente. Se questo valore viene superato, può verificarsi un errore di eccezione.

Se il processo AEM supera questo limite massimo, il messaggio &quot; `too many open files`&quot; viene visualizzato in `error.log`.

Per evitare tali eccezioni, eseguire le operazioni seguenti:

1. Verifica quanti file aperti vengono utilizzati dal processo AEM.

   Questo controllo dipende dalla piattaforma su cui è in esecuzione l’istanza. È possibile utilizzare utilità quali lsof (UNIX®) o Process Explorer (Windows).

   Questo valore deve essere monitorato durante lo sviluppo e il test per:

   * conferma la chiusura dei file come richiesto
   * per determinare il valore massimo necessario (in varie circostanze)

1. Imposta il massimo consentito.

   Il nuovo valore dovrebbe tener conto sia delle esigenze attuali che di eventuali picchi futuri, per cui è consigliabile raddoppiare le esigenze attuali.

   Per impostazione predefinita, `serverctl` configura `CQ_MAX_OPEN_FILES` a `8192`; ciò dovrebbe essere sufficiente per la maggior parte degli scenari.

### Configurazione dell’editor Rich Text {#configuring-the-rich-text-editor}

Il **Editor Rich Text** (**RTE**) offre agli autori un&#39;ampia gamma di [funzionalità](/help/sites-authoring/rich-text-editor.md) per modificare il contenuto testuale, fornendo icone, caselle di selezione e menu per un’esperienza WYSIWYG.

Consulta [Configurazione dell’editor Rich Text](/help/sites-administering/rich-text-editor.md) per ulteriori dettagli.

### Configurazione dell’annullamento per la modifica delle pagine {#configuring-undo-for-page-editing}

Esistono diverse proprietà che controllano il comportamento dei comandi Annulla e Ripristina per la modifica delle pagine. Questi possono essere configurati, vedi [Configurazione dell’annullamento per la modifica delle pagine](/help/sites-administering/config-undo.md) per ulteriori dettagli.

### Configurazione del componente video {#configuring-the-video-component}

Il [Componente video](/help/sites-authoring/default-components-foundation.md#video) consente di inserire nella pagina un elemento video predefinito e pronto all’uso.

Affinché la trascodifica venga eseguita correttamente, l’amministratore deve [Installare FFmpeg](/help/sites-administering/config-video.md#install-ffmpeg) separatamente. Possono inoltre [Configurare i profili video](/help/sites-administering/config-video.md#configure-video-profiles) da utilizzare con elementi html5.

### Configurazione e personalizzazione dei rapporti {#configuring-and-customizing-reports}

Per facilitare il monitoraggio e l’analisi dello stato dell’istanza, CQ fornisce una selezione di rapporti predefiniti che possono essere configurati in base ai singoli requisiti:

Consulta la [Nozioni di base sulla personalizzazione dei rapporti](/help/sites-administering/reporting.md#the-basics-of-report-customization) per ulteriori dettagli.

### Configurazione delle notifiche e-mail {#configuring-email-notification}

CQ invia notifiche e-mail agli utenti che:

* Si sono abbonati a eventi di pagina, ad esempio modifiche o repliche.
* Ti sei iscritto agli eventi del forum.
* Devi eseguire un passaggio in un flusso di lavoro.

Consulta [Configurazione delle notifiche e-mail](/help/sites-administering/notification.md) per ulteriori dettagli.

### Abilitazione delle impressioni di pagina {#enabling-page-impressions}

Le impression di pagina vengono visualizzate in **Impression** della console classica dell’interfaccia utente siteadmin. Per abilitare l’acquisizione delle impression di pagina, configura quanto segue:

* Nell’istanza di pubblicazione:

   * [Statistiche pagina WCM Day CQ](/help/sites-deploying/osgi-configuration-settings.md)

* Nell’istanza di authoring:

   * [Tracciamento impression pagina di Adobe](/help/sites-deploying/osgi-configuration-settings.md)

>[!CAUTION]
>
>La configurazione di Adobe Page Impressions Tracker nell’ambiente di authoring consente richieste anonime al servizio di tracciamento.
