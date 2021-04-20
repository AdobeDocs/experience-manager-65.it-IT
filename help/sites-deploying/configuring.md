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
feature: Configuring
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2133'
ht-degree: 1%

---


# Concetti di configurazione di base{#basic-configuration-concepts}

Adobe Experience Manager (AEM) è installato con le impostazioni predefinite per tutti i parametri che gli consentono di eseguire &quot;out of the box&quot;. Tuttavia, puoi configurare AEM per i tuoi requisiti specifici.

È possibile configurare diversi aspetti di AEM:

* Alcuni sono [configurati comunemente per ogni installazione di progetto](#primary-configuration-considerations) e devono essere esaminati per verificare se sono applicabili o meno al progetto.
* [Ulteriori ](#further-configuration-considerations) configurazioni possono essere comuni ma non obbligatorie; relative alle funzioni o alle prestazioni e alla stabilità del sistema.
* Altri sono necessari solo per alcune funzioni facoltative di AEM (documentate insieme alla funzione appropriata).

A seconda della configurazione specifica, queste modifiche possono essere effettuate utilizzando:

* **Console web Adobe CQ**

   Si tratta di una posizione standard per la configurazione dei bundle e dei servizi OSGi.

   Per ulteriori dettagli e pratiche consigliate, consulta [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) .

* **Archivio**

   Un sottoinsieme di configurazioni OSGi è disponibile nell’archivio. In questo modo, la copia o la replica dei contenuti dell’archivio ricrea configurazioni identiche. Puoi anche aggiungere configurazioni personalizzate, a seconda della modalità di esecuzione, all’archivio.

   Per ulteriori informazioni, consulta [Configurazione OSGi nel Repository](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) e in particolare [Aggiunta di una nuova configurazione al Repository](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository) .

* **File system**

   Alcuni file di configurazione risiedono nel file system.

* **WCM AEM**

   Diversi aspetti possono essere configurati all&#39;interno AEM WCM stesso, molti utilizzando la console [Strumenti](/help/sites-administering/tools-consoles.md); ad esempio, agenti di replica.

>[!NOTE]
>
>Quando lavori con Adobe Experience Manager, esistono diversi metodi per gestire le impostazioni di configurazione per i servizi OSGi (nodi console o archivio).
>
>Per informazioni dettagliate, consulta [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) .

>[!NOTE]
>
>La configurazione di AEM è semplice, ma devi tenere presente che:
>
>Alcune modifiche possono avere un impatto importante sulle applicazioni. Per questo motivo, assicurati di disporre dell’esperienza e delle conoscenze necessarie prima di iniziare a configurare AEM e di apportare solo le modifiche che sai essere necessarie. Tutte le modifiche effettuate tramite la console OSGi vengono applicate **immediatamente** al sistema in esecuzione (non è necessario riavviare il sistema).

## Considerazioni sulla configurazione principale {#primary-configuration-considerations}

Questo elenco descrive le aree principali comunemente configurate per ogni nuovo progetto. Non tutti sono necessari, ma l’elenco deve essere letto e rivisto per vedere cosa è applicabile al progetto.

L’elenco fornisce una breve panoramica di ogni aspetto della configurazione, oltre ai collegamenti alle pagine che forniscono dettagli completi.

### Lista di controllo protezione {#security-checklist}

Diversi problemi di configurazione chiave sono elencati nella [Lista di controllo sicurezza](/help/sites-administering/security-checklist.md). Assicurati di leggere questo e di prendere tutte le misure necessarie per la tua installazione.

### Configurazione dell’interfaccia utente predefinita - Ottimizzato per touch o Classic {#configuring-the-default-ui-touch-optimized-or-classic}

Sono disponibili due interfacce utente per AEM:

* Interfaccia touch
* L&#39;interfaccia classica

Puoi configurare l&#39;interfaccia utente necessaria utilizzando [Mappatura della directory principale](/help/sites-deploying/osgi-configuration-settings.md).

>[!NOTE]
>
>Ulteriori informazioni sulla selezione dell&#39;interfaccia sono disponibili in [Selezione dell&#39;interfaccia utente](/help/sites-authoring/select-ui.md).

### IPv4 e IPv6 {#ipv-and-ipv}

Tutti gli elementi di AEM (ad esempio l’archivio, il Dispatcher, ecc.) possono essere installati nelle reti IPv4 e IPv6.

Il funzionamento è semplice in quanto non è necessaria alcuna configurazione speciale, quando necessario è possibile specificare un indirizzo IP utilizzando il formato appropriato per il tipo di rete.

Ciò significa che, quando è necessario specificare un indirizzo IP, è possibile selezionare (come richiesto) da:

* un indirizzo IPv6

   ad esempio `https://[ab12::34c5:6d7:8e90:1234]:4502`

* un indirizzo IPv4

   ad esempio `https://123.1.1.4:4502`

* un nome server

   ad esempio, `https://www.yourserver.com:4502`

* il caso predefinito di `localhost` verrà interpretato sia per le installazioni di rete IPv4 che IPv6

   ad esempio, `http://localhost:4502`

### Rimozione della versione {#version-purging}

In un’installazione standard AEM crea una nuova versione di una pagina o di un nodo ogni volta che si attiva una pagina (dopo aver aggiornato il contenuto).Puoi anche creare versioni aggiuntive su richiesta utilizzando la scheda **Gestione versioni** della barra laterale. Tutte queste versioni sono memorizzate nell’archivio e possono essere ripristinate se necessario.

Queste versioni non vengono mai eliminate, pertanto la dimensione dell’archivio aumenterà nel tempo e deve quindi essere gestita.

Per informazioni dettagliate, consulta [Version Purging](/help/sites-deploying/version-purging.md) , in particolare [Version Manager](/help/sites-deploying/version-purging.md#version-manager) per informazioni su come configurare AEM per eliminare le versioni precedenti quando viene creata una nuova versione.

### Registrazione {#logging}

AEM offre la possibilità di configurare:

* parametri globali per il servizio di registrazione centrale
* richiedere la registrazione dei dati; una configurazione di registrazione specializzata per le informazioni di richiesta
* impostazioni specifiche per i singoli servizi; ad esempio, un singolo file di log e un formato per i messaggi di log

Per informazioni dettagliate, consulta [Logging](/help/sites-deploying/configure-logging.md) .

### Modalità di esecuzione {#run-modes}

Le modalità di esecuzione ti consentono di regolare la tua istanza AEM per uno scopo specifico; ad esempio autore o pubblicazione, test, sviluppo o intranet, ecc.

Questo viene fatto definendo raccolte di parametri di configurazione per ogni modalità di esecuzione. Viene applicato un set di parametri di configurazione di base per tutte le modalità di esecuzione, quindi è possibile regolare set aggiuntivi in base allo scopo del proprio ambiente specifico. Vengono quindi applicate come necessario.

Tutte le impostazioni di configurazione sono memorizzate nell&#39;unico archivio e attivate impostando la **Modalità di esecuzione**.

Per informazioni dettagliate, consulta [Modalità di esecuzione](/help/sites-deploying/configure-runmodes.md) .

### Single Sign On {#single-sign-on}

L&#39;accesso Single Sign On (SSO) consente a un utente di accedere a più sistemi dopo aver fornito le credenziali di autenticazione (ad esempio un nome utente e una password) una volta. Un sistema separato (noto come autenticatore affidabile) esegue l&#39;autenticazione e fornisce Experienci Manager con le credenziali utente. Experience Manager controlla e applica le autorizzazioni di accesso per l’utente (ovvero determina a quali risorse l’utente può accedere).

Per ulteriori informazioni, consulta [Single Sign On](/help/sites-deploying/single-sign-on.md) .

### Mappatura risorse {#resource-mapping}

La mappatura delle risorse viene utilizzata per definire reindirizzamenti, URL personalizzati e host virtuali per AEM.

Ad esempio, puoi utilizzare queste mappature per:

* Aggiungi il prefisso `/content` a tutte le richieste affinché la struttura interna sia nascosta ai visitatori del tuo sito web.
* Definisci un reindirizzamento in modo che tutte le richieste alla pagina `/content/en/gateway` del sito web vengano reindirizzate a `https://gbiv.com/`.

Per ulteriori informazioni, consulta [Mappatura risorse](/help/sites-deploying/resource-mapping.md) .

### Agenti di replica, replica inversa e replica {#replication-reverse-replication-and-replication-agents}

Gli agenti di replica sono fondamentali per AEM come meccanismo utilizzato per:

* [Pubblicare (attivare)](/help/sites-authoring/publishing-pages.md) contenuti da un autore a un ambiente di pubblicazione.
* Esegui lo scaricamento esplicito del contenuto dalla cache del Dispatcher.
* Restituisci l’input dell’utente (ad esempio, l’input del modulo) dall’ambiente di pubblicazione all’ambiente di authoring (sotto il controllo dell’ambiente di authoring).

Per ulteriori dettagli, vedere [Replica](/help/sites-deploying/replication.md).

### Impostazioni di configurazione OSGi {#osgi-configuration-settings}

[](https://www.osgi.org/) OSGiè un elemento fondamentale nello stack tecnologico di AEM. Viene utilizzato per controllare i bundle compositi di AEM e la loro configurazione.

Consulta [Impostazioni di configurazione OSGi](/help/sites-deploying/osgi-configuration-settings.md) per un elenco dei vari bundle rilevanti per l&#39;implementazione del progetto (elencati in base al bundle). Non tutte le impostazioni elencate devono essere regolate, alcune sono menzionate per aiutarti a capire come funziona AEM.

Quando si lavora con AEM esistono diversi metodi per gestire le impostazioni di configurazione di tali servizi; per ulteriori dettagli e pratiche consigliate, consulta [Configurazione di OSGi](/help/sites-deploying/configuring-osgi.md) .

### Configurazione di LDAP {#configuring-ldap}

L&#39;autenticazione LDAP è necessaria per autenticare gli utenti memorizzati in una directory LDAP (centrale) come Active Directory. Questo consente di ridurre lo sforzo necessario per gestire gli account utente.

L&#39;autenticazione LDAP avviene a livello di archivio, quindi viene gestita direttamente dall&#39;archivio. Per ulteriori dettagli, consulta [Configurazione di LDAP con AEM](/help/sites-administering/ldap-config.md).

Per la gestione degli utenti in AEM (inclusa l&#39;assegnazione dei diritti di accesso), consulta [Amministrazione degli utenti e sicurezza](/help/sites-administering/security.md).

### Configurazione del Dispatcher {#configuring-the-dispatcher}

Dispatcher è uno strumento di caching e/o bilanciamento del carico Adobe Experience Manager che può essere utilizzato insieme a un server web di classe enterprise.

Per ulteriori informazioni sulla configurazione, consulta [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) .[](https://helpx.adobe.com/it/experience-manager/dispatcher/using/dispatcher-configuration.html)

### Configurazione AEM connettore LiveCycle {#configuring-aem-livecycle-connector}

Con il rilascio dei servizi di documenti AEM e di sicurezza dei documenti AEM, ora è possibile richiamare i servizi di documenti di LiveCycle per eseguire il rendering di un modulo XFA, convertire un documento in PDF e proteggere un documento tramite criteri. Per ulteriori informazioni, leggere [AEM connettore LiveCycle](https://helpx.adobe.com/livecycle/help/aem/aem-livecycle-connector.html).

### Offload e amministrazione della topologia del lavoro {#job-offloading-and-topology-administration}

[](/help/sites-deploying/offloading.md) Offload distribuisce le attività di elaborazione che corrispondono a istanze di Experience Manager in una topologia. Con lo scaricamento, è possibile utilizzare istanze di Experience Manager specifiche per eseguire tipi specifici di elaborazione. L&#39;elaborazione specializzata consente di ottimizzare l&#39;utilizzo delle risorse server disponibili.

Le topologie sono cluster di Experienci Manager ad accoppiamento approssimativo che partecipano allo scarico. Un cluster è costituito da una o più istanze del server Experience Manager (una singola istanza è considerata un cluster).

Per ulteriori informazioni su come visualizzare o modificare l&#39;appartenenza alla topologia, consulta la sezione [Amministrazione delle topologie](/help/sites-deploying/offloading.md#administering-topologies) .

### Configurazione della console di benvenuto {#configuring-the-welcome-console}

La console Benvenuto nell’interfaccia classica offre un elenco di collegamenti alle varie console e funzionalità di AEM.

Per ulteriori informazioni, è possibile configurare i collegamenti visibili, consulta [Configurazione della console di benvenuto](/help/sites-developing/customizing-the-welcome-console.md) .

### Configurazione per le prestazioni {#configuring-for-performance}

[](/help/sites-deploying/configuring-performance.md) Le prestazioni sono la chiave del progetto. Alcuni aspetti di AEM (e/o dell’archivio sottostante) possono essere configurati per ottimizzare le prestazioni.

Per ulteriori informazioni, consulta [Configurazione per Performance](/help/sites-deploying/configuring-performance.md#configuring-for-performance) .

<!--delete ### Scaling {#scaling}

Scaling a CQ installation correctly depends greatly on the details of your particular use case. A detailed discussion of solution patterns for various situations can be found in [Scaling CQ](/help/sites-deploying/scaling.md).-->

### Archivio dati condiviso {#shared-data-store}

L&#39;archivio dati dell&#39;archivio viene utilizzato per scaricare l&#39;archiviazione dei file binari di grandi dimensioni dall&#39;archivio appropriato a un&#39;area separata, in modo che più istanze dello stesso file binario (un&#39;immagine, ad esempio) all&#39;interno della struttura dell&#39;archivio vengano memorizzate una sola volta.

Questa funzione &quot;store-once, reference-many-times&quot; può essere estesa per servire non solo un singolo archivio, ma archivi completamente separati, configurando l&#39;archivio dati di ciascuno per fare riferimento alla stessa posizione del file system condiviso.

Tale archivio dati può essere condiviso tra nodi diversi nello stesso cluster, diverse istanze di pubblicazione e/o authoring nella stessa installazione o anche istanze completamente separate in installazioni diverse.

Per ulteriori informazioni, consulta [Configurazione di archivi dati e archivi di nodi](/help/sites-deploying/data-store-config.md).

## Ulteriori considerazioni sulla configurazione {#further-configuration-considerations}

### Abilitazione di HTTP su SSL {#enabling-http-over-ssl}

Puoi abilitare HTTP su SSL per utilizzare connessioni più sicure ai server.

Per ulteriori informazioni, consulta [Abilitazione di HTTP su SSL](/help/sites-administering/ssl-by-default.md) .

### Portali AEM e portlet {#aem-portals-and-portlets}

Un portale è un’applicazione web che offre personalizzazione, accesso singolo, integrazione dei contenuti da diverse sorgenti e ospita il livello di presentazione dei sistemi informativi. Il componente portlet consente inoltre di incorporare un portlet nella pagina. Per accedere ai contenuti forniti da CQ5 WCM, il server portale può essere installato con il Portlet Director del Portale CQ5. Puoi eseguire questa operazione installando, configurando e aggiungendo il portlet alla pagina del portale.

Per ulteriori informazioni, consulta [Portale e portlet](/help/sites-administering/aem-as-portal.md) .

### Scadenza degli oggetti statici {#expiration-of-static-objects}

Gli oggetti statici (ad esempio, le icone) non cambiano. Pertanto, il sistema deve essere configurato in modo che non scadano (per un periodo di tempo ragionevole) e quindi riducano il traffico inutile.

Per ulteriori informazioni, vedere [Scadenza degli oggetti statici](/help/sites-deploying/expiration-static-objects.md) .

### Apri i file nel processo Java {#open-files-in-the-java-process}

Ogni processo java può accedere ai file - questo richiede risorse di sistema. Per questo motivo viene definito un limite superiore per il numero di file a cui ogni processo può accedere contemporaneamente. Se viene superato, può verificarsi un errore di eccezione.

Se il processo di AEM supera questo massimo, il messaggio &quot; `too many open files`&quot; verrà visualizzato in `error.log`.

Per evitare tali eccezioni è necessario:

1. Controlla quanti file aperti vengono utilizzati dal processo di AEM.

   La modalità di questo controllo dipende dalla piattaforma su cui viene eseguita l’istanza. È possibile utilizzare utility quali lsof (Unix) o Process Explorer (Windows).

   Questo valore deve essere monitorato durante lo sviluppo e il test per:

   * conferma la chiusura dei file come richiesto
   * per determinare il valore massimo necessario (in varie circostanze)

1. Imposta il massimo consentito.

   Il nuovo valore dovrebbe tener conto sia delle esigenze attuali che di eventuali picchi futuri, per cui è opportuno raddoppiare le esigenze attuali.

   Per impostazione predefinita, `serverctl` configura `CQ_MAX_OPEN_FILES` in `8192`; questo dovrebbe essere sufficiente per la maggior parte degli scenari.

### Configurazione dell’editor Rich Text {#configuring-the-rich-text-editor}

L’ **Editor Rich Text** (**RTE**) offre agli autori un’ampia gamma di [funzionalità](/help/sites-authoring/rich-text-editor.md) per la modifica del contenuto testuale; fornendo loro icone, caselle di selezione e menu per un’esperienza WYSIWYG.

Per ulteriori informazioni, consulta [Configurazione dell’editor Rich Text](/help/sites-administering/rich-text-editor.md) .

### Configurazione di Annulla per la modifica delle pagine {#configuring-undo-for-page-editing}

Esistono diverse proprietà che controllano il comportamento dei comandi Annulla e Ripristina per la modifica delle pagine. Per ulteriori informazioni, consulta [Configurazione dell’annullamento per la modifica delle pagine](/help/sites-administering/config-undo.md) .

### Configurazione del componente video {#configuring-the-video-component}

Il [componente Video](/help/sites-authoring/default-components-foundation.md#video) consente di inserire un elemento video predefinito sulla pagina.

Tenete presente che, per una transcodifica corretta, è necessario installare separatamente [FFmpeg. ](/help/sites-administering/config-video.md#install-ffmpeg) Possono anche [configurare i profili video](/help/sites-administering/config-video.md#configure-video-profiles) per l&#39;utilizzo con elementi html5.

### Configurazione e personalizzazione dei report {#configuring-and-customizing-reports}

Per aiutarti a monitorare e analizzare lo stato dell’istanza, CQ fornisce una selezione di rapporti predefiniti che possono essere configurati per le tue esigenze individuali:

Per ulteriori informazioni, consulta le [Nozioni di base sulla personalizzazione dei rapporti](/help/sites-administering/reporting.md#the-basics-of-report-customization) .

### Configurazione della notifica e-mail {#configuring-email-notification}

CQ invia notifiche e-mail agli utenti che:

* Si è iscritto a eventi di pagina, ad esempio modifiche o replica.
* Si sono abbonati agli eventi del forum.
* Eseguire un passaggio in un flusso di lavoro.

Per ulteriori informazioni, consulta [Configurazione notifica e-mail](/help/sites-administering/notification.md) .

### Abilitazione delle impressioni di pagina {#enabling-page-impressions}

Le impression di pagina vengono visualizzate nella colonna **Impression** della console di amministrazione del sito dell’interfaccia classica. Per abilitare l’acquisizione delle impression di pagina è necessario configurare quanto segue:

* Nell’istanza di pubblicazione:

   * [Statistiche pagina di CQ WCM](/help/sites-deploying/osgi-configuration-settings.md)

* Nell’istanza dell’autore:

   * [Adobe Traccia impressioni pagina](/help/sites-deploying/osgi-configuration-settings.md)

>[!CAUTION]
>
>La configurazione di Adobe Page Impression Tracker nell’ambiente di authoring consentirà richieste anonime al servizio di tracciamento.

