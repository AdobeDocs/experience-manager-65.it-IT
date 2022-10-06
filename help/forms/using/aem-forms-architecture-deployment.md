---
title: Architettura e topologie di implementazione per AEM Forms
seo-title: Architecture and deployment topologies for AEM Forms
description: Dettagli dell’architettura per AEM Forms e topologie consigliate per clienti e clienti AEM nuovi ed esistenti che eseguono l’aggiornamento da LiveCycle ES4 ad AEM Forms.
seo-description: Architecture details for AEM Forms and recommended topologies for new and existing AEM customers and customers upgrading from LiveCycle ES4 to AEM Forms.
uuid: 90baa57a-4785-4b49-844c-a44717d3c12d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: 0156b5c3-3bef-4213-9ada-c7b6ae96ada4
role: Admin
exl-id: d4421d46-cfc9-424e-8a88-9d0a2994a5cf
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '2460'
ht-degree: 0%

---

# Architettura e topologie di implementazione per AEM Forms {#architecture-and-deployment-topologies-for-aem-forms}

## Architettura {#architecture}

AEM Forms è un&#39;applicazione distribuita in AEM come pacchetto AEM. Il pacchetto è noto come pacchetto aggiuntivo di AEM Forms. Il pacchetto aggiuntivo di AEM Forms contiene sia i servizi (provider API), distribuiti nel contenitore OSGi AEM, sia i servlet o i JSP (che forniscono funzionalità front-end e API REST) gestiti dal framework Sling AEM. Il diagramma seguente illustra questa configurazione:

![architettura](assets/architecture.png)

L’architettura di AEM Forms include i seguenti componenti:

* **Servizi di base AEM:** Servizi di base AEM forniti a un&#39;applicazione distribuita. Questi servizi includono un archivio di contenuti conforme a JCR, un contenitore di servizi OSGI, un motore di flusso di lavoro, un archivio di fiducia, un archivio chiavi e così via. Questi servizi sono disponibili per l’applicazione AEM Forms ma non sono forniti dai pacchetti AEM Forms. Questi servizi sono parte integrante dello stack di AEM complessivo e questi servizi sono utilizzati da vari componenti di AEM Forms.
* **Servizi Forms:** Offre funzionalità correlate ai moduli, quali creazione, assemblaggio, distribuzione e archiviazione di documenti PDF, aggiunta di firme digitali per limitare l’accesso ai documenti e decodifica di moduli con codice a barre. Questi servizi sono disponibili al pubblico per il consumo tramite codice personalizzato co-distribuito in AEM.
* **Livello Web:** JSP o servlet, costruiti sopra i servizi comuni e forms, che forniscono le seguenti funzionalità:

   * **Fronte di authoring**: Interfaccia utente per la creazione e la gestione dei moduli.
   * **Rendering del modulo e front-end di invio**: Interfaccia utente finale da utilizzare per gli utenti finali dell’AEM Forms (ad esempio, i cittadini che accedono a un sito web governativo). Questo fornisce il rendering del modulo (visualizzazione del modulo in un browser web) e le funzionalità di invio.
   * **API REST**: I JSP e i servlet esportano un sottoinsieme di servizi dei moduli per l’utilizzo remoto da parte di client basati su HTTP, ad esempio l’SDK per dispositivi mobili Forms.

**AEM Forms su OSGi:** Un AEM Forms nell’ambiente OSGi è un pacchetto standard AEM Author o AEM Publish con AEM Forms implementato su di esso. Puoi eseguire AEM Forms su OSGi in un [ambiente server singolo, configurazione farm e cluster](/help/sites-deploying/recommended-deploys.md). La configurazione del cluster è disponibile solo per le istanze di AEM Author.

**AEM Forms su JEE:** AEM Forms on JEE è il server AEM Forms in esecuzione sullo stack JEE. Dispone di AEM Author con pacchetti aggiuntivi di AEM Forms e di funzionalità JEE aggiuntive di AEM Forms implementate congiuntamente su un singolo stack JEE in esecuzione su un server applicativo. Puoi eseguire AEM Forms su JEE in configurazioni a server singolo e cluster. AEM Forms su JEE è necessario solo per eseguire la sicurezza dei documenti, la gestione dei processi e, ad LiveCycle, per i clienti che eseguono l’aggiornamento ad AEM Forms. Di seguito sono riportati alcuni scenari aggiuntivi per utilizzare AEM Forms su JEE:

* **Supporto per l’area di lavoro di HTML (per i clienti che utilizzano l’area di lavoro di HTML):** AEM Forms su JEE abilita il single sign-on con le istanze di elaborazione, distribuisce determinate risorse sottoposte a rendering nelle istanze di elaborazione e gestisce l’invio di moduli sottoposti a rendering nell’area di lavoro di HTML.
* **Elaborazione avanzata dei dati di comunicazione interattiva/modulo avanzata**: AEM Forms su JEE può essere utilizzato per elaborare ulteriormente i dati di comunicazione interattiva/modulo (e per salvare i risultati in un archivio dati adatto) in casi d’uso complessi in cui sono necessarie funzionalità avanzate di gestione dei processi.

AEM Forms su JEE include anche i seguenti servizi di supporto per i componenti AEM:

* **Gestione utente integrata:** Consente agli utenti di AEM Forms su JEE di essere riconosciuti come moduli AEM sugli utenti OSGi e aiuta ad abilitare SSO per gli utenti OSGi e JEE. Questo è necessario per gli scenari in cui è richiesto il single sign-on tra moduli AEM su OSGi e AEM Forms su JEE (ad esempio, nell’area di lavoro di HTML).
* **Hosting delle risorse:** AEM Forms su JEE può servire le risorse (ad esempio, HTML5 forms) sottoposte a rendering su AEM Forms su OSGi.

L’interfaccia utente per l’authoring di AEM Forms non supporta la creazione di DOR (Document of Record), PDF forms e HTML5 Forms. Tali risorse sono progettate utilizzando l’applicazione autonoma Forms Designer e caricate singolarmente in AEM Forms Manager. In alternativa, per AEM Forms su JEE, i moduli possono essere progettati come risorse dell’applicazione (in AEM Forms Workbench) e distribuiti in AEM Forms sul server JEE.

AEM Forms su OSGi e AEM Forms su JEE dispongono entrambe di funzionalità di flusso di lavoro. È possibile creare e distribuire rapidamente flussi di lavoro di base per varie attività sui moduli di AEM su OSGi, senza dover installare la funzionalità di gestione dei processi completa di AEM Forms su JEE. C&#39;è qualche differenza nel [funzioni del flusso di lavoro incentrato sui moduli su AEM Forms su OSGi e funzionalità di gestione dei processi di AEM Forms su JEE](capabilities-osgi-jee-workflows.md). Lo sviluppo e la gestione di flussi di lavoro incentrati su moduli su AEM Forms su OSGi utilizza le funzionalità familiari AEM Workflow e AEM Inbox.

## Terminologie {#terminologies}

L’immagine seguente mostra diverse configurazioni AEM server Form e relativi componenti utilizzati in una tipica implementazione AEM Forms:

![aem_forms_-_recommendations_topology](assets/aem_forms_-_recommendedtopology.png)

**Autore:** Un’istanza di authoring è un server AEM Forms in esecuzione nella modalità standard di esecuzione di Author. Può essere AEM Forms su JEE o AEM Forms su ambiente OSGi. È destinato agli utenti interni, ai progettisti e agli sviluppatori di comunicazioni interattive e ai moduli. Abilita le seguenti funzionalità:

* **Creazione e gestione di moduli e comunicazioni interattive:** Designer e sviluppatori possono creare e modificare moduli adattivi e comunicazioni interattive, caricare altri tipi di moduli creati esternamente, ad esempio moduli creati in Adobe Forms Designer e gestire tali risorse utilizzando la console Forms Manager.
* **Pubblicazione di moduli e comunicazioni interattive:** Le risorse ospitate in un’istanza dell’autore possono essere pubblicate in un’istanza di pubblicazione per eseguire operazioni di runtime. La pubblicazione delle risorse utilizza le funzioni di replica di AEM. L’Adobe consiglia di configurare un agente di replica su tutte le istanze dell’autore in modo da inviare manualmente i moduli pubblicati alle istanze di elaborazione e di configurare un altro agente di replica per le istanze di elaborazione con il *Al ricevimento* attivatore abilitato per replicare automaticamente i moduli ricevuti per pubblicare le istanze.

**Pubblica:** Un’istanza di pubblicazione è un server AEM Forms in esecuzione nella modalità di esecuzione standard di Publish. Le istanze di pubblicazione sono destinate agli utenti finali di applicazioni basate su moduli, ad esempio gli utenti che accedono a un sito web pubblico e inviano moduli. Abilita le seguenti funzionalità:

* Rendering e invio di Forms per gli utenti finali.
* Trasporto dei dati del modulo non elaborati inviati alle istanze di elaborazione per ulteriore elaborazione e archiviazione nel sistema di registrazione finale. L’implementazione predefinita fornita in AEM Forms si basa sulle funzionalità di replica inversa di AEM. È inoltre disponibile un’implementazione alternativa per inviare direttamente i dati del modulo ai server di elaborazione anziché salvarli per primi localmente (quest’ultimo è un prerequisito per l’attivazione della replica inversa). I clienti che nutrono dubbi sull’archiviazione di dati potenzialmente sensibili sulle istanze di pubblicazione possono intervenire per questo [implementazione alternativa](/help/forms/using/configuring-draft-submission-storage.md), poiché le istanze di elaborazione si trovano in genere in un’area più sicura.
* Rendering e invio di comunicazioni e lettere interattive: Viene eseguito il rendering di una comunicazione interattiva e di una lettera sulle istanze di pubblicazione e i dati corrispondenti vengono inviati alle istanze di elaborazione per l’archiviazione e la post-elaborazione. I dati possono essere salvati localmente in un&#39;istanza di pubblicazione e replicati in modo inverso in un&#39;istanza di elaborazione (opzione predefinita) in un secondo momento, oppure inviati direttamente all&#39;istanza di elaborazione senza salvare nell&#39;istanza di pubblicazione. Quest&#39;ultima implementazione è utile per i clienti attenti alla sicurezza.

**Elaborazione:** Un’istanza di AEM Forms in esecuzione in modalità di esecuzione Author senza che nessun utente sia assegnato al gruppo forms-manager. Puoi distribuire AEM Forms su JEE o AEM Forms su OSGi come istanza di elaborazione. Gli utenti non sono assegnati per garantire che le attività di authoring e gestione dei moduli non vengano eseguite sull’istanza di elaborazione e vengano eseguite solo sull’istanza di authoring. Un’istanza di elaborazione abilita le seguenti funzionalità:

* **Elaborazione dei dati del modulo non elaborato provenienti da un’istanza Publish:** Questo si ottiene principalmente su un’istanza di elaborazione tramite flussi di lavoro AEM che si attivano quando i dati arrivano. I flussi di lavoro possono utilizzare il passaggio Modello dati modulo fornito come predefinito per archiviare i dati o il documento in un archivio dati appropriato.
* **Memorizzazione sicura dei dati del modulo**: L’elaborazione fornisce un archivio dietro il firewall per i dati dei moduli non elaborati che sono isolati dagli utenti. Né i form designer sull&#39;istanza Author né gli utenti finali sull&#39;istanza Publish possono accedere a questo archivio.

   >[!NOTE]
   >
   > Adobe consiglia di utilizzare un archivio dati di terze parti per salvare i dati elaborati finali invece di utilizzare AEM archivio.

* **Archiviazione e post-elaborazione dei dati della corrispondenza provenienti da un’istanza Publish:** I flussi di lavoro AEM eseguono la post-elaborazione opzionale delle definizioni di lettere corrispondenti. Questi flussi di lavoro possono salvare i dati elaborati finali in archivi di dati esterni adeguati.

* **Hosting in HTML Workspace**: Un’istanza di elaborazione ospita il front-end per HTML Workspace. L’area di lavoro di HTML fornisce l’interfaccia utente per l’assegnazione di attività/gruppi associati per i processi di revisione e approvazione.

Un’istanza di elaborazione è configurata per l’esecuzione in modalità di esecuzione dell’autore perché:

* Consente la replica inversa dei dati del modulo non elaborato da un’istanza Publish. Il gestore di archiviazione dati predefinito richiede la funzione di replica inversa.
* Si consiglia di eseguire flussi di lavoro AEM, che sono il mezzo principale per elaborare i dati modulo non elaborati provenienti da un’istanza di pubblicazione, in un sistema in stile autore.

## Topologie fisiche di esempio per AEM Forms su JEE {#sample-physical-topologies-for-aem-forms-on-jee}

Le topologie AEM Forms on JEE consigliate di seguito sono principalmente per i clienti che eseguono l’aggiornamento dal LiveCycle o da una versione precedente di AEM Forms su JEE. Adobe consiglia di utilizzare AEM Forms su OSGi per nuove installazioni. Una nuova installazione di AEM Forms su JEE è consigliata solo per l’utilizzo delle funzionalità di Document Security e Process Management.

### Topologia per l’utilizzo di document services o funzionalità di protezione dei documenti {#topology-for-using-document-services-or-document-security-capabilities}

I clienti AEM Forms che intendono utilizzare solo le funzionalità di document services o document security possono disporre di una topologia simile a quella riportata di seguito. Questa topologia consiglia di utilizzare una singola istanza di AEM Forms. Se necessario, puoi anche creare un cluster o una farm di server AEM Forms. Questa topologia è consigliata quando la maggior parte degli utenti dispone di funzionalità di accesso programmatico del server AEM Forms e l’intervento tramite l’interfaccia utente è minimo. La topologia è utile nelle operazioni di elaborazione batch di document services. Ad esempio, utilizzando il servizio di output è possibile creare centinaia di documenti PDF non modificabili su base giornaliera.

Sebbene AEM Forms ti consenta di configurare ed eseguire tutte le funzionalità da un singolo server, è comunque necessario eseguire la pianificazione della capacità, il bilanciamento del carico e configurare server dedicati per funzionalità specifiche in un ambiente di produzione. Ad esempio, per un ambiente che utilizza il servizio PDF Generator per convertire migliaia di pagine al giorno e aggiungere firme digitali per limitare l’accesso ai documenti, impostare server AEM Forms separati per il servizio PDF Generator e le funzionalità di firma digitale. Consente di fornire prestazioni ottimali e di scalare i server in modo indipendente l&#39;uno dall&#39;altro.

![funzioni di base](assets/basic-features.png)

### Topologia per l’utilizzo della gestione dei processi di AEM Forms {#topology-for-using-aem-forms-process-management}

I clienti di AEM Forms che intendono utilizzare le funzioni di gestione dei processi di AEM Forms, ad esempio, HTML Workspace possono disporre di una topologia simile a quella riportata di seguito. Il server AEM Forms su JEE può trovarsi in una singola configurazione server o cluster.

Se esegui l’aggiornamento da LiveCycle ES4, questa topologia rispecchia fedelmente ciò che hai già in LiveCycle, fatta eccezione per l’aggiunta di AEM Author incorporato ad AEM Forms su JEE. Inoltre, non vi è alcuna modifica nei requisiti di clustering per i clienti che eseguono un aggiornamento. Se utilizzi AEM Forms in un ambiente cluster, puoi continuare con lo stesso in Forms 6.5 AEM. Per una nuova installazione di AEM Forms di JEE per l’utilizzo di HTML Workspace, è necessario eseguire AEM’istanza di authoring integrata nell’ambiente JEE.

L’archivio dati del modulo è un archivio dati di terze parti utilizzato per memorizzare i dati elaborati finali di moduli e comunicazioni interattive. Questo è un elemento facoltativo nella topologia. Puoi anche scegliere di impostare un’istanza di elaborazione e utilizzare il relativo archivio come sistema di registrazione finale, se necessario.

![topology_for_usinghtmlworkspaceandformsapp](assets/topology_for_usinghtmlworkspaceandformsapp.png)

La topologia è consigliata ai clienti che pianificano l’utilizzo di AEM Forms sul server JEE per le funzionalità di gestione dei processi (HTML Workspace) senza utilizzare funzionalità di post-elaborazione, moduli adattivi, moduli HTML5 e comunicazioni interattive.

### Topologia per l’utilizzo di moduli adattivi, moduli HTML5, funzionalità di comunicazione interattiva {#topology-for-using-adaptive-forms-html-forms-interactive-communication-capabilities}

I clienti AEM Forms che intendono utilizzare le funzionalità di acquisizione dati di AEM Forms, ad esempio moduli adattivi, HTML5 Forms, PDF forms, possono avere una topologia simile a quella mostrata di seguito. Questa topologia è consigliata anche per l’utilizzo delle funzionalità di comunicazione interattiva di AEM Forms.

![topologia-for-using-forms-osgi-modules](assets/topology-for-using-forms-osgi-modules.png)

Puoi apportare le seguenti modifiche/personalizzazioni alla topologia suggerita sopra:

* L’utilizzo dell’app HTML Workspace e AEM Forms richiede un’istanza di authoring o elaborazione AEM. È possibile utilizzare l’istanza di authoring AEM integrata in AEM Forms sul server JEE invece di configurare un server di authoring AEM esterno aggiuntivo.
* Un’istanza di authoring o elaborazione AEM è necessaria solo per i flussi di lavoro Forms incentrati su OSGi, moduli adattivi, portale moduli e comunicazione interattiva.
* l&#39;interfaccia utente dell&#39;agente di comunicazione interattivo viene generalmente eseguita all&#39;interno dell&#39;organizzazione. È quindi possibile mantenere un server di pubblicazione per l&#39;interfaccia utente dell&#39;agente all&#39;interno della rete privata.
* I moduli AEM sull’istanza OSGi incorporati in AEM Forms sul server JEE possono inoltre eseguire flussi di lavoro Forms incentrati su OSGi e cartelle controllate.

## Topologie fisiche di esempio per l’utilizzo di AEM Forms su OSGi {#sample-physical-topologies-for-using-aem-forms-on-osgi}

### Topologia per l&#39;acquisizione dei dati, comunicazione interattiva, Flusso di lavoro incentrato sui moduli sulle funzionalità OSGi {#topology-for-data-capture-interactive-communication-form-centric-workflow-on-osgi-capabilities}

I clienti AEM Forms che intendono utilizzare le funzionalità di acquisizione dati di AEM Forms, ad esempio moduli adattivi, HTML5 Forms, PDF forms, possono avere una topologia simile a quella mostrata di seguito. Questa topologia è consigliata anche per l’utilizzo delle comunicazioni interattive e dei flussi di lavoro Forms-Centric su OSGi, ad esempio, per l’utilizzo AEM Posta in arrivo e AEM Forms App per i flussi di lavoro dei processi aziendali.

![workflow interattivo-use-cases-af-cm-osgi-workflow](assets/interactive-use-cases-af-cm-osgi-workflow.png)

### Topologia per l&#39;utilizzo delle funzionalità delle cartelle controllate per l&#39;elaborazione batch offline {#topology-for-using-watched-folder-capabilities-for-offline-batch-processing}

I clienti AEM Forms che pianificano l’utilizzo di Cartelle controllate per l’elaborazione batch possono avere una topologia simile a quella riportata di seguito. La topologia visualizza un ambiente cluster, ma decidi di utilizzare una singola istanza o una farm di server AEM Forms a seconda del carico. L’origine dati di terze parti è il tuo sistema di record. Funge da origine di input per le cartelle controllate. La topologia visualizza anche l’output sotto forma di file stampato. È inoltre possibile archiviare il contenuto di output in un file system, inviarlo tramite e-mail e utilizzare altri metodi personalizzati per utilizzare l’output.

![offline-batch-processing-via-guardata-folder](assets/offline-batch-processing-via-watched-folders.png)

### Topologia per l’utilizzo delle funzionalità di document services per l’elaborazione offline basata su API {#topology-for-using-document-services-capabilities-for-offline-api-based-processing}

I clienti AEM Forms che intendono utilizzare solo la funzionalità document services possono disporre di una topologia simile a quella riportata di seguito. Questa topologia consiglia di utilizzare un cluster di AEM Forms sui server OSGi. Questa topologia è consigliata quando la maggior parte degli utenti dispone di funzionalità di accesso programmatiche (utilizzando API) del server AEM Forms e l’intervento tramite l’interfaccia utente è minimo. La topologia è abbastanza utile in scenari client software multipli. Ad esempio, più client che utilizzano il servizio PDF Generator per creare documenti PDF su richiesta.

Sebbene AEM Forms ti consenta di configurare ed eseguire tutte le funzionalità da un singolo server, devi eseguire la pianificazione della capacità, il bilanciamento del carico e configurare server dedicati per funzionalità specifiche in un ambiente di produzione. Ad esempio, per un ambiente che utilizza il servizio PDF Generator per convertire migliaia di pagine al giorno e più moduli adattivi per l’acquisizione dei dati, configura server AEM Forms separati per il servizio PDF Generator e le funzionalità dei moduli adattivi. Consente di fornire prestazioni ottimali e di scalare i server in modo indipendente l&#39;uno dall&#39;altro.

![elaborazione basata su api offline](assets/offline-api-based-processing.png)
