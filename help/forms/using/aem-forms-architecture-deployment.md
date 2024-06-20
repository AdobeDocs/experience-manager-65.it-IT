---
title: Architettura e topologie di implementazione per AEM Forms
description: Dettagli dell’architettura di AEM Forms e topologie consigliate per clienti AEM nuovi ed esistenti e per l’aggiornamento dal LiveCycle ES4 ad AEM Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
role: Admin
exl-id: d4421d46-cfc9-424e-8a88-9d0a2994a5cf
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, Foundation Components
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '2469'
ht-degree: 0%

---

# Architettura e topologie di implementazione per AEM Forms {#architecture-and-deployment-topologies-for-aem-forms}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/aem-forms-cloud-service-architecture.html) |
| AEM 6.5 | Questo articolo |

## Architettura {#architecture}

AEM Forms è un’applicazione implementata nell’AEM come pacchetto AEM. Il pacchetto è noto come pacchetto del componente aggiuntivo AEM Forms. Il pacchetto del componente aggiuntivo AEM Forms contiene sia i servizi (provider API) distribuiti nel contenitore OSGi dell’AEM che i servlet o le JSP (che forniscono funzionalità API sia front-end che REST) gestiti dal framework Sling dell’AEM. Il diagramma seguente illustra questa configurazione:

![architettura](assets/architecture.png)

L’architettura di AEM Forms include i seguenti componenti:

* **Servizi principali dell’AEM:** Servizi di base forniti dall&#39;AEM a un&#39;applicazione implementata. Questi servizi includono un archivio di contenuti conforme a JCR, un contenitore di servizi OSGI, un motore di flusso di lavoro, un archivio fonti attendibili, un archivio chiavi e così via. Questi servizi sono disponibili per l’applicazione AEM Forms ma non sono forniti dai pacchetti AEM Forms. Questi servizi sono parte integrante dello stack globale dell’AEM e vari componenti AEM Forms utilizzano tali servizi.
* **Servizi Forms:** Fornisce funzionalità relative ai moduli, ad esempio creazione, assemblaggio, distribuzione e archiviazione di documenti PDF, aggiunta di firme digitali per limitare l’accesso ai documenti e decodifica di moduli con codice a barre. Questi servizi sono pubblicamente disponibili per l’utilizzo da parte del codice personalizzato distribuito congiuntamente nell’AEM.
* **Livello web:** JSP o servlet, costruiti su servizi comuni e forms, che forniscono le seguenti funzionalità:

   * **Creazione front-end**: interfaccia utente per la creazione e la gestione dei moduli per la creazione e la gestione dei moduli.
   * **Rendering e invio modulo front-end**: interfaccia utente finale per gli utenti finali di AEM Forms (ad esempio, i cittadini che accedono a un sito web governativo). In questo modo è possibile visualizzare la copia trasformata di un modulo (in un browser Web) e le funzionalità di invio.
   * **API REST**: JSP e servlet esportano un sottoinsieme di servizi Forms per l’utilizzo remoto da parte di client basati su HTTP, come l’SDK mobile di Forms.

**AEM Forms su OSGi:** Un ambiente AEM Forms su OSGi è il pacchetto standard AEM Author o AEM Publish con AEM Forms distribuito su di esso. Puoi eseguire AEM Forms su OSGi in un [ambiente server singolo, farm e configurazioni cluster](/help/sites-deploying/recommended-deploys.md). La configurazione del cluster è disponibile solo per le istanze di creazione AEM.

**AEM Forms su JEE:** AEM Forms su JEE è un server AEM Forms in esecuzione sullo stack JEE. Dispone di AEM Author con pacchetti di componenti aggiuntivi AEM Forms e funzionalità AEM Forms JEE aggiuntive co-implementate in un singolo stack JEE in esecuzione su un server applicazioni. Puoi eseguire AEM Forms su JEE in configurazioni a server singolo e cluster. AEM Forms su JEE è necessario solo per eseguire la sicurezza dei documenti, la gestione dei processi e per i clienti di LiveCycle che eseguono l’aggiornamento ad AEM Forms. Di seguito sono riportati alcuni scenari aggiuntivi per utilizzare AEM Forms su JEE:

* **Supporto di HTML Workspace (per i clienti che utilizzano HTML Workspace):** AEM Forms su JEE abilita il single sign-on con le istanze di elaborazione, fornisce determinate risorse sottoposte a rendering nelle istanze di elaborazione e gestisce l’invio dei moduli sottoposti a rendering nell’area di lavoro di HTML.
* **Elaborazione avanzata di dati aggiuntivi per moduli/comunicazioni interattive**: AEM Forms su JEE può essere utilizzato per elaborare ulteriormente i dati di comunicazione interattivi o dei moduli (e per salvare i risultati in un archivio dati appropriato) in casi d’uso complessi in cui sono necessarie funzionalità avanzate di gestione dei processi.

AEM Forms su JEE include anche i seguenti servizi di supporto per i componenti dell’AEM:

* **Gestione integrata degli utenti:** Consente agli utenti di AEM Forms su JEE di essere riconosciuti come moduli AEM dagli utenti OSGi e consente di abilitare l’SSO sia per gli utenti OSGi che per gli utenti JEE. Ciò è necessario per gli scenari in cui è richiesto il single sign-on tra i moduli AEM su OSGi e AEM Forms su JEE (ad esempio, HTML Workspace).
* **Hosting risorse:** AEM Forms su JEE può fornire risorse (ad esempio, moduli HTML5) di cui è stato eseguito il rendering su AEM Forms su OSGi.

L’interfaccia utente di authoring di AEM Forms non supporta la creazione di documenti di record (DOR), PDF forms e HTML5 Forms. Tali risorse sono progettate utilizzando l’applicazione autonoma Forms Designer e caricate singolarmente in AEM Forms Manager. In alternativa, per AEM Forms su JEE, i moduli possono essere progettati come risorse di applicazioni (in AEM Forms Workbench) e distribuiti in AEM Forms sul server JEE.

AEM Forms su OSGi e AEM Forms su JEE dispongono entrambi di funzionalità per i flussi di lavoro. Puoi creare e distribuire rapidamente flussi di lavoro di base per varie attività sui moduli AEM su OSGi, senza dover installare la funzionalità completa di gestione dei processi di AEM Forms su JEE. C&#39;è una certa differenza nel [funzioni del flusso di lavoro incentrato su moduli in AEM Forms su OSGi e funzionalità di gestione dei processi di AEM Forms su JEE](capabilities-osgi-jee-workflows.md). Lo sviluppo e la gestione di flussi di lavoro incentrati sui moduli su AEM Forms su OSGi utilizza le familiari funzionalità del flusso di lavoro AEM e della casella in entrata AEM.

## Terminologie {#terminologies}

L’immagine seguente mostra diverse configurazioni del server AEM Form e i relativi componenti utilizzati in una tipica implementazione di AEM Forms:

![aem_forms_-_consigliata topologia](assets/aem_forms_-_recommendedtopology.png)

**Autore:** Un’istanza di authoring è un server AEM Forms in esecuzione nella modalità di esecuzione Autore standard. Può essere AEM Forms su JEE o AEM Forms su ambiente OSGi. È destinato agli utenti interni, ai progettisti di moduli e comunicazioni interattive e agli sviluppatori. Abilita le seguenti funzionalità:

* **Authoring e gestione di moduli e comunicazioni interattive:** I designer e gli sviluppatori possono creare e modificare moduli adattivi e comunicazioni interattive, caricare altri tipi di moduli creati esternamente, ad esempio moduli creati in Adobe Forms Designer, e gestire queste risorse tramite la console Forms Manager.
* **Pubblicazione di moduli e comunicazioni interattive:** Le risorse in hosting su un’istanza di authoring possono essere pubblicate su un’istanza di pubblicazione per eseguire operazioni di runtime. La pubblicazione delle risorse utilizza le funzioni di replica dell’AEM. L’Adobe consiglia di configurare un agente di replica in tutte le istanze di authoring per inviare manualmente i moduli pubblicati alle istanze di elaborazione, e di configurare un altro agente di replica per le istanze di elaborazione con *Alla ricezione* trigger abilitato per replicare automaticamente i moduli ricevuti nelle istanze di pubblicazione.

**Pubblicazione:** Un’istanza di pubblicazione è un server AEM Forms in esecuzione nella modalità di esecuzione standard di Publish. Le istanze di Publish sono destinate agli utenti finali di applicazioni basate su moduli, ad esempio gli utenti che accedono a un sito Web pubblico e inviano moduli. Abilita le seguenti funzionalità:

* Rendering e invio di Forms per gli utenti finali.
* Trasporto dei dati grezzi del modulo inviati alle istanze di elaborazione per ulteriore elaborazione e archiviazione nel sistema di registrazione finale. L’implementazione predefinita fornita in AEM Forms utilizza le funzionalità di replica inversa dell’AEM. È inoltre disponibile un’implementazione alternativa per inviare direttamente i dati del modulo ai server di elaborazione anziché salvarli prima in locale (quest’ultimo è un prerequisito per l’attivazione della replica inversa). I clienti che hanno dubbi sull’archiviazione di dati potenzialmente sensibili sulle istanze di pubblicazione possono partecipare [implementazione alternativa](/help/forms/using/configuring-draft-submission-storage.md), poiché le istanze di elaborazione si trovano in genere in un’area più sicura.
* Rendering e invio di comunicazioni e lettere interattive: una comunicazione e una lettera interattive vengono sottoposte a rendering sulle istanze di pubblicazione e i dati corrispondenti vengono inviati alle istanze di elaborazione per l’archiviazione e la post-elaborazione. I dati possono essere salvati localmente in un’istanza di pubblicazione e replicati in modo inverso in un’istanza di elaborazione (opzione predefinita) in un secondo momento, oppure inviati direttamente all’istanza di elaborazione senza salvarli nell’istanza di pubblicazione. Quest’ultima implementazione è utile per i clienti attenti alla sicurezza.

**Elaborazione:** Un’istanza di AEM Forms in esecuzione in modalità di esecuzione Creazione senza utenti assegnati al gruppo Forms-Manager. Puoi distribuire AEM Forms su JEE o AEM Forms su OSGi come istanza di elaborazione. Gli utenti non vengono assegnati per garantire che le attività di authoring e gestione dei moduli non vengano eseguite sull’istanza Elaborazione e si verifichino solo sull’istanza Autore. Un’istanza di elaborazione abilita le seguenti funzionalità:

* **Elaborazione dei dati del modulo non elaborati provenienti da un’istanza Publish:** Ciò si ottiene principalmente su un’istanza di elaborazione tramite flussi di lavoro AEM che si attivano quando i dati arrivano. I flussi di lavoro possono utilizzare il passaggio Modello dati modulo fornito come strumento pronto all’uso per archiviare i dati o il documento in un archivio dati appropriato.
* **Archiviazione sicura dei dati dei moduli**: l’elaborazione fornisce un archivio dietro il firewall per i dati dei moduli non elaborati isolati dagli utenti. Né i progettisti di moduli nell’istanza di authoring né gli utenti finali nell’istanza di Publish possono accedere a questo archivio.

  >[!NOTE]
  >
  >L’Adobe consiglia di utilizzare un archivio dati di terze parti per salvare i dati elaborati finali invece di utilizzare l’archivio AEM.

* **Archiviazione e post-elaborazione dei dati di corrispondenza provenienti da un’istanza Publish:** I flussi di lavoro AEM eseguono la post-elaborazione opzionale delle definizioni di lettere corrispondenti. Questi flussi di lavoro possono salvare i dati elaborati finali in appositi archivi di dati esterni.

* **Hosting di HTML Workspace**: un’istanza di elaborazione ospita il front-end per HTML Workspace. HTML Workspace fornisce l’interfaccia utente per l’assegnazione di attività/gruppi associata ai processi di revisione e approvazione.

Un’istanza di elaborazione è configurata per l’esecuzione in modalità di esecuzione Creazione perché:

* Consente la replica inversa dei dati dei moduli non elaborati da un’istanza Publish. Il gestore di archiviazione dati predefinito richiede la funzionalità di replica inversa.
* I flussi di lavoro AEM, che rappresentano il mezzo principale di elaborazione dei dati in formato non elaborato provenienti da un’istanza di Publish, sono consigliati per l’esecuzione su un sistema di tipo Author.

## Topologie fisiche di esempio per AEM Forms su JEE {#sample-physical-topologies-for-aem-forms-on-jee}

Le topologie AEM Forms su JEE consigliate di seguito sono principalmente per i clienti che eseguono l’aggiornamento da LiveCycle o da una versione precedente di AEM Forms su JEE. L’Adobe consiglia di utilizzare AEM Forms su OSGi per le nuove installazioni. Una nuova installazione di AEM Forms su JEE è consigliata solo per l’utilizzo delle funzionalità di Document Security e Process Management.

### Topologia per l’utilizzo dei servizi documentali o delle funzionalità di protezione dei documenti {#topology-for-using-document-services-or-document-security-capabilities}

I clienti AEM Forms che intendono utilizzare solo servizi documentali o funzionalità di sicurezza dei documenti possono avere una topologia simile a quella visualizzata di seguito. Questa topologia consiglia di utilizzare una singola istanza di AEM Forms. Se necessario, puoi anche creare un cluster o una farm di server AEM Forms. Questa topologia è consigliata quando la maggior parte degli utenti accede alle funzionalità del server AEM Forms a livello di programmazione e l’intervento tramite l’interfaccia utente è minimo. La topologia è utile nelle operazioni di elaborazione in batch dei servizi documentali. Ad esempio, utilizzando il servizio di output per creare centinaia di documenti PDF non modificabili su base giornaliera.

AEM Forms consente di configurare ed eseguire tutte le funzionalità da un singolo server, ma è necessario eseguire la pianificazione della capacità, il bilanciamento del carico e la configurazione di server dedicati per funzionalità specifiche in un ambiente di produzione. Ad esempio, per un ambiente che utilizza il servizio PDF Generator per convertire migliaia di pagine al giorno e aggiungere firme digitali per limitare l’accesso ai documenti, configura server AEM Forms separati per il servizio PDF Generator e le funzionalità di firma digitale. Consente di fornire prestazioni ottimali e scalare i server in modo indipendente l&#39;uno dall&#39;altro.

![funzionalità di base](assets/basic-features.png)

### Topologia per l&#39;utilizzo di AEM Forms Process Management {#topology-for-using-aem-forms-process-management}

I clienti di AEM Forms che intendono utilizzare le funzioni di gestione dei processi di AEM Forms, ad esempio HTML Workspace, possono avere una topologia simile a quella visualizzata di seguito. Il server AEM Forms su JEE può trovarsi in una configurazione con un singolo server o cluster.

Se si esegue l’aggiornamento dal LiveCycle ES4, questa topologia rispecchia fedelmente quella già esistente nel LiveCycle, ad eccezione dell’aggiunta dell’istanza di creazione AEM integrata in AEM Forms su JEE. Inoltre, non vi è alcuna modifica dei requisiti di clustering per i clienti che eseguono un aggiornamento. Se utilizzavi AEM Forms in un ambiente cluster, puoi continuare con lo stesso in AEM 6.5 Forms. Per una nuova installazione di AEM Forms of JEE per l’utilizzo di HTML Workspace, è necessario eseguire l’istanza di authoring AEM integrata nell’ambiente JEE.

L’archivio dati modulo è un archivio dati di terze parti utilizzato per memorizzare i dati elaborati finali dei moduli e delle comunicazioni interattive. Questo è un elemento facoltativo nella topologia. Se necessario, puoi anche scegliere di impostare un’istanza di elaborazione e utilizzare il relativo archivio come sistema di registrazione finale.

![topology_for_usinghtmlworkspaceandformsapp](assets/topology_for_usinghtmlworkspaceandformsapp.png)

La topologia è consigliata ai clienti che intendono utilizzare AEM Forms sul server JEE per le funzionalità di gestione dei processi (HTML Workspace) senza ricorrere a processi di post-elaborazione, moduli adattivi, moduli HTML5 e funzionalità di comunicazione interattiva.

### Topologia per l’utilizzo di moduli adattivi, moduli HTML5, funzionalità di comunicazione interattiva {#topology-for-using-adaptive-forms-html-forms-interactive-communication-capabilities}

I clienti di AEM Forms che intendono utilizzare le funzionalità di acquisizione dati di AEM Forms, ad esempio moduli adattivi, HTML5 Forms e PDF forms, possono avere una topologia simile a quella visualizzata di seguito. Questa topologia è consigliata anche per l’utilizzo delle funzionalità di comunicazione interattiva di AEM Forms.

![topologia per l’utilizzo di moduli osgi](assets/topology-for-using-forms-osgi-modules.png)

Puoi apportare le seguenti modifiche/personalizzazioni alla topologia suggerita:

* L’utilizzo di HTML Workspace e dell’app AEM Forms richiede un’istanza di authoring o elaborazione AEM. È possibile utilizzare l’istanza di authoring dell’AEM integrata in AEM Forms sul server JEE invece di configurare un altro server di authoring dell’AEM esterno.
* Un’istanza di elaborazione o authoring AEM è necessaria solo per i flussi di lavoro incentrati su Forms su OSGi, moduli adattivi, portale dei moduli e comunicazione interattiva.
* l’interfaccia utente interattiva dell’agente di comunicazione viene generalmente eseguita all’interno dell’organizzazione. Pertanto, puoi mantenere un server di pubblicazione per l’interfaccia utente dell’agente all’interno della rete privata.
* I moduli AEM sull’istanza OSGi integrata nel server AEM Forms su JEE possono anche eseguire flussi di lavoro incentrati su Forms su OSGi e cartelle controllate.

## Topologie fisiche di esempio per l’utilizzo di AEM Forms su OSGi {#sample-physical-topologies-for-using-aem-forms-on-osgi}

### Topologia per l’acquisizione dei dati, la comunicazione interattiva e il flusso di lavoro incentrato sui moduli sulle funzionalità OSGi {#topology-for-data-capture-interactive-communication-form-centric-workflow-on-osgi-capabilities}

I clienti di AEM Forms che intendono utilizzare le funzionalità di acquisizione dati di AEM Forms, ad esempio moduli adattivi, HTML5 Forms e PDF forms, possono avere una topologia simile a quella visualizzata di seguito. Questa topologia è consigliata anche per l’utilizzo di comunicazioni interattive e flussi di lavoro incentrati su Forms sulle funzionalità OSGi, ad esempio per l’utilizzo della casella in entrata AEM e dell’app AEM Forms per i flussi di lavoro dei processi aziendali.

![interactive-use-CASES-af-cm-osgi-workflow](assets/interactive-use-cases-af-cm-osgi-workflow.png)

### Topologia per l’utilizzo delle funzionalità delle cartelle controllate per l’elaborazione batch offline {#topology-for-using-watched-folder-capabilities-for-offline-batch-processing}

I clienti di AEM Forms che intendono utilizzare le cartelle controllate per l’elaborazione in batch possono avere una topologia simile a quella visualizzata di seguito. Nella topologia viene visualizzato un ambiente cluster, ma si decide di utilizzare una singola istanza o una farm di server AEM Forms a seconda del carico. L’origine dati di terze parti è il tuo sistema di registrazione. Funge da origine di input per le cartelle controllate. La topologia visualizza anche l&#39;output sotto forma di file stampato. Puoi anche memorizzare il contenuto di output in un file system, inviarlo tramite e-mail e utilizzare altri metodi personalizzati per l’utilizzo dell’output.

![offline-batch-processing-via-watched-folders](assets/offline-batch-processing-via-watched-folders.png)

### Topologia per l’utilizzo delle funzionalità dei servizi basati su documenti per l’elaborazione offline basata su API {#topology-for-using-document-services-capabilities-for-offline-api-based-processing}

I clienti AEM Forms che intendono utilizzare solo la funzionalità servizi documentali possono avere una topologia simile a quella visualizzata di seguito. Questa topologia consiglia di utilizzare un cluster di AEM Forms sui server OSGi. Questa topologia è consigliata quando la maggior parte degli utenti accede a livello di programmazione (utilizzando le API) al server AEM Forms e l’intervento tramite l’interfaccia utente è minimo. La topologia è molto utile in più scenari di client software. Ad esempio, più clienti che utilizzano il servizio PDF Generator possono creare documenti PDF su richiesta.

Anche se AEM Forms consente di impostare ed eseguire tutte le funzionalità da un singolo server, è necessario eseguire la pianificazione della capacità, il bilanciamento del carico e la configurazione di server dedicati per funzionalità specifiche in un ambiente di produzione. Ad esempio, per un ambiente che utilizza il servizio PDF Generator per convertire migliaia di pagine al giorno e più moduli adattivi per l’acquisizione dei dati, configura server AEM Forms separati per il servizio PDF Generator e le funzionalità dei moduli adattivi. Consente di fornire prestazioni ottimali e scalare i server in modo indipendente l&#39;uno dall&#39;altro.

![offline-api-based-processing](assets/offline-api-based-processing.png)
