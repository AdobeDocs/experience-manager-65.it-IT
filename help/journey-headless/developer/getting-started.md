---
title: Guida introduttiva ad AEM Headless
description: In questa parte del Percorso per sviluppatori headless di AEM, approfondire i prerequisiti headless di AEM.
exl-id: a94794a4-bf8b-4f3b-a761-3f02feedd5c0
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '3032'
ht-degree: 92%

---

# Guida introduttiva ad AEM Headless {#getting-started}

In questa parte del [Percorso per sviluppatori headless di AEM,](overview.md) scopri cosa è necessario per avviare il tuo progetto con AEM headless.

## Percorso affrontato finora {#story-so-far}

Nel documento precedente del percorso AEM headless, [Informazioni sullo sviluppo headless di CMS](learn-about.md), hai imparato la teoria di base su cosa sia un CMS headless e ora dovresti:

* Comprendere i concetti e la terminologia di base per la distribuzione di contenuti headless
* Capire perché e quando è richiesto un headless
* Conoscere ad alto livello come vengono utilizzati i concetti headless e come si relazionano

Questo articolo si basa su questi elementi fondamentali per comprendere come utilizzare AEM per implementare una soluzione headless.

## Obiettivo {#objective}

Questo documento ti aiuta a capire AEM headless nel contesto del tuo progetto. Dopo la lettura dovresti:

* Comprendere le nozioni di base delle funzioni headless di AEM.
* Conoscere i prerequisiti per l’utilizzo delle funzionalità headless di AEM.
* Essere a conoscenza dei livelli di integrazione headless di AEM.
* Essere in grado di definire il tuo progetto in termini di ambito.

## Nozioni di base su AEM {#aem-basics}

Prima di poter definire il progetto headless all’interno di AEM, è importante comprendere alcuni concetti di base su AEM.

### Istanza di authoring {#author}

Fondamentalmente, AEM consiste di un’istanza di authoring e di un’[istanza di pubblicazione](#publish) che collaborano per creare, gestire e pubblicare i contenuti.

Il contenuto inizia nell’istanza di authoring. Ed è qui che gli autori dei contenuti creano i propri contenuti. L’ambiente di authoring offre agli autori diversi strumenti per creare, organizzare e riutilizzare i contenuti.

### Istanza di pubblicazione {#publish}

Una volta creato il contenuto nell’istanza di authoring, deve essere pubblicato per essere disponibile e utilizzabile da altri servizi. Un’istanza di pubblicazione contiene tutti i contenuti già pubblicati.

### Replica {#replication}

La replica è l’atto di trasferire il contenuto dall’istanza di authoring all’istanza di pubblicazione. Questa operazione viene eseguita automaticamente da AEM quando un autore o un altro utente con i diritti appropriati pubblica il contenuto.

### Riepilogo delle nozioni di base su AEM {#aem-basics-summary}

Al livello più semplice, la creazione di esperienze digitali in AEM richiede i seguenti passaggi:

1. Gli autori dei contenuti creano i contenuti headless nell’istanza di authoring.
1. Quando il contenuto è pronto, viene replicato nell’istanza di pubblicazione.
1. È possibile, quindi, richiamare le API per recuperare questo contenuto.

AEM headless sviluppa questa base tecnica offrendo strumenti potenti per gestire contenuti headless che saranno [descritti nella sezione successiva.](#aem-headless-basics)

## Nozioni di base su AEM headless {#aem-headless-basics}

Le funzionalità headless di AEM si basano su poche funzioni chiave. Queste sono spiegate in dettaglio nelle parti successive del percorso. Ora è importante conoscere solo le basi di ciò che fanno e come vengono chiamate.

### Modelli per frammenti di contenuto {#content-fragment-models}

I modelli per frammenti di contenuto definiscono la struttura dei dati e del contenuto che puoi creare e gestire in AEM. Servono come una sorta di impalcatura per i tuoi contenuti. Quando si sceglie di creare i contenuti, gli autori selezionano dai modelli per frammenti di contenuto da te definiti, che li guidano nella creazione del contenuto.

### Frammenti di contenuto {#content-fragments}

I frammenti di contenuto ti consentono di progettare, creare, curare e pubblicare contenuti indipendenti dalle pagine. Consentono di preparare contenuti pronti per l&#39;uso in più posizioni e su più canali.

I Frammenti di contenuto contengono contenuto strutturato e possono essere consegnati in formato JSON.

### API GraphQL e REST {#apis}

Per modificare il contenuto senza problemi, AEM offre due solide API.

* L’API GraphQL consente di creare richieste per accedere e distribuire frammenti di contenuto.
* L’API REST di Assets consente di creare e modificare frammenti di contenuto (e altre risorse).

Scoprirai di più su queste API e come utilizzarle in una parte successiva del percorso AEM headless. Oppure, consulta la [risorse aggiuntive](#additional-resources) per ulteriore documentazione, vedere la sezione seguente.

## Livelli di integrazione headless {#integration-levels}

AEM supporta sia i modelli di CMS full headless che quelli tradizionali full stack o headful. Tuttavia AEM offre non solo queste due opzioni esclusive, ma anche la possibilità di supportare modelli ibridi che combinano i vantaggi di entrambi, offrendo una flessibilità unica per il vostro progetto headless.

Al fine di garantire la comprensione dei concetti headless, questo Percorso per sviluppatori headless di AEM si concentra sul modello headless puro per consentirti di iniziare a lavorare il prima possibile senza conoscere il codice in AEM.

Tuttavia, è necessario essere consapevoli delle possibilità ibride aggiuntive disponibili una volta comprese le caratteristiche di AEM headless. Questi casi sono indicati di seguito perché possiate prenderne visione. Al termine del percorso, riceverai informazioni più dettagliate su questi concetti nel caso in cui sia necessaria tale flessibilità per il tuo progetto.

### È possibile già un utilizzo esterno del contenuto headless, ad esempio un’applicazione a pagina singola (SPA). {#already-have-a-spa}

Supponiamo che il requisito di base sia almeno distribuire dei contenuti da AEM a un servizio esterno esistente.

#### Livello 1: integrazione dei frammenti di contenuto - Modello tradizionale headless {#level-1}

Questo livello di integrazione è il modello headless tradizionale e consente agli autori di contenuti di creare contenuti in AEM e distribuirli senza problemi a qualsiasi numero di servizi esterni tramite GraphQL o di modificarli da servizi esterni tramite l’API di Assets. Non è richiesta alcuna codifica in AEM.

In questo modello, AEM viene utilizzato solo per creare e distribuire il contenuto utilizzando Frammenti di contenuto AEM. Il rendering e l’interazione con il contenuto vengono delegati all’applicazione esterna utilizzata, spesso un’applicazione a pagina singola (SPA).

#### Livello 2: incorporare la SPA in AEM - Modello ibrido {#level-2}

Questo livello di integrazione si basa sul primo livello, ma consente anche di incorporare in AEM l’applicazione esterna (SPA) in modo che gli autori dei contenuti possano visualizzare il contenuto nel contesto dell’applicazione esterna in AEM. L’applicazione può anche supportare la modifica limitata dell’applicazione esterna in AEM.

Questo livello offre il vantaggio di consentire agli autori di contenuti di creare in modo flessibile i contenuti in AEM in modo headful, con i contenuti presentati nel contesto con una SPA esterna incorporata, e allo stesso tempo distribuire il contenuto in modo headless.

#### Livello 3: incorpora e abilita completamente la SPA in AEM - Modello ibrido {#level-3}

Questo livello di integrazione si basa sul livello 2, consentendo la modifica della maggior parte dei contenuti della SPA esterna in AEM.

### Non è possibile un utilizzo esterno del contenuto headless, ad esempio un’applicazione a pagina singola (SPA). {#do-not-have-a-spa}

Se il tuo obiettivo è quello di creare un SPA che utilizzi senza intestazione i contenuti dell’AEM, puoi utilizzare funzioni quali Frammenti di contenuto per gestire i contenuti headless e anche creare un SPA con il framework dell’Editor SPA dell’AEM.

Con l’editor SPA, la SPA non solo utilizza contenuti di AEM, ma è anche completamente modificabile all’interno di AEM dagli autori di contenuti, offrendoti la flessibilità della distribuzione headless e della modifica nel contesto in AEM.

## Requisiti e prerequisiti {#requirements-prerequisites}

Ci sono diversi requisiti prima di iniziare il tuo progetto per AEM headless.

### Conoscenza {#knowledge}

* GraphQL
* Esperienza di sviluppo nella creazione di SPA con i framework React o Angular
* Competenze di base in AEM per la creazione di frammenti di contenuto e l’utilizzo dell’editor

### Strumenti {#tools}

* Accesso alla sandbox per testare la distribuzione del progetto
* Istanza di sviluppo locale per la modellazione dei dati e il testing
* SPA esterna esistente o altro consumatore del contenuto AEM headless

## Definizione del progetto {#defining-your-project}

Per ogni progetto riuscito è importante definire chiaramente non solo i requisiti del progetto, ma anche i ruoli e le responsabilità.

### Ambito {#scope}

È importante disporre di un ambito chiaramente definito per il progetto. L’ambito informa i criteri di accettazione e consente di stabilire una definizione di completato.

La prima domanda che dovete porre è “Cosa sto cercando di fare con AEM headless?” In generale, la risposta dovrebbe essere che in futuro si dispone o si disporrà di un’applicazione Experience creata con i propri strumenti di sviluppo e non con l’AEM. Questa applicazione di esperienza potrebbe essere un’app mobile, un sito web o qualsiasi altra applicazione di esperienza rivolta ai clienti e alle clienti finali. L’obiettivo nell’utilizzo di AEM headless è alimentare l’applicazione di esperienza con contenuti creati, memorizzati e gestiti in AEM con API all’avanguardia che richiamerebbero AEM headless per recuperare contenuti o persino contenuti completamente CRUD direttamente dall’applicazione di esperienza. Se questo non è quello che stai cercando di fare, probabilmente vorrai [tornare indietro per consultare la documentazione AEM](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=it) e trovare la sezione che meglio si adatta a ciò che desideri realizzare.

### Ruoli e responsabilità {#roles-responsibilities}

I ruoli di ogni singolo progetto variano, ma quelli importanti da considerare nel contenuto dello sviluppo AEM headless sono:

* [Amministratore](#administrator)
* [Autore del contenuto](#content-author)
* [Architetto dei contenuti](#content-architect)
* [Sviluppatore](#developer)

#### Amministratore {#administrator}

L’amministratore è responsabile dell’impostazione e della configurazione di base del sistema. Ad esempio, l’amministratore configura l’organizzazione all’interno del sistema di gestione utenti di Adobe, denominato Identity Management System (IMS). L’amministratore è il primo utente dell’organizzazione a ricevere un invito e-mail da Adobe dopo che l’organizzazione è stata creata da Adobe in IMS. L’amministratore può accedere a IMS e aggiungere utenti di altri utenti tipo.

Una volta configurati dall’amministratore, agli utenti vengono concesse le autorizzazioni di accesso a tutte le risorse AEM per svolgere il loro lavoro di collaboratori per la distribuzione dell’applicazione Experience tramite AEM Headless.

L’amministratore deve essere l’utente che configura AEM e prepara l’ambiente di esecuzione per abilitare gli [autori di contenuti](#content-author) a creare e aggiornare contenuti e gli [sviluppatori](#developer) a utilizzare le API che recuperano o modificano il contenuto per le applicazioni di esperienza.

#### Autore del contenuto {#content-author}

Gli autori dei contenuti creano e gestiscono i contenuti distribuiti in modo headless da AEM. Gli autori dei contenuti utilizzano funzioni di AEM come Frammenti di contenuto e la console Assets per gestirne i contenuti.

Gli autori dei contenuti devono tenere presenti le seguenti best practice.

#### Pianificare la traduzione {#translation}

Pianificare la traduzione all’inizio del progetto. Considerare “specialista della traduzione” colui o colei come utente tipo separato a cui spetta definire quale contenuto dovrebbe essere tradotto e quale no, e quale contenuto tradotto potrebbe essere modificato dai produttori di contenuti regionali o locali.

Creare un piano su quali contenuti devono essere tradotti.

* Hai bisogno di lingue diverse o anche di una lingua da adottare per caratteristiche regionali specifiche?
* È necessario che contenuti multimediali complessi come immagini o video siano diversi per impostazioni internazionali diverse?

Procedere con sicurezza sul flusso di lavoro di aggiornamento dei contenuti. Quale processo di approvazione deve supportare il sistema? È possibile utilizzare i flussi di lavoro AEM per automatizzare questo processo?

Tieni presente che la [gerarchia dei contenuti](#content-hierarchy) può essere sfruttata per semplificare la traduzione.

Consulta la sezione [risorse aggiuntive](#additional-resources) per ulteriore documentazione sui flussi di lavoro AEM e gli strumenti di traduzione, compresi i collegamenti al Percorso di traduzione headless di AEM.

##### Sfruttamento della gerarchia dei contenuti {#content-hierarchy}

La gerarchia delle cartelle può affrontare due problemi principali relativi alla gestione dei contenuti:

* [Traduzione](#translation): AEM gestisce la traduzione dei contenuti mantenendone delle copie in cartelle specifiche delle impostazioni locali.
* Organizzazione: le cartelle vengono utilizzate per definire una gerarchia di contenuti necessaria per supportare le esigenze di traduzione e per gestire in modo logico i frammenti di contenuto.

AEM consente una struttura dei contenuti flessibile e una gerarchia può essere arbitrariamente grande. Tuttavia è importante rendersi conto che eventuali modifiche nella struttura delle cartelle possono avere conseguenze indesiderate per le query esistenti che [si basano sul percorso del contenuto.](#developer) Pertanto, una gerarchia ben definita, chiaramente impostata in anticipo, può essere utile per gli autori dei contenuti.

Le cartelle possono anche essere limitate per consentire solo alcuni tipi di contenuto (in base ai Modelli per frammenti di contenuto). Si consiglia di specificare sempre in modo esplicito quali modelli sono consentiti per tutte le cartelle nella gerarchia. Specifica del contenuto consentito per una determinata cartella:

* Impedisce agli autori di contenuti di creare contenuti che non appartengono alla cartella.
* Ottimizza il processo di creazione dei contenuti filtrando i tipi di contenuto consentiti nella cartella durante la creazione per mostrare solo i tipi di contenuto validi.

Creando una struttura di contenuto appropriata, diventa più semplice coordinare l’authoring dei contenuti headless tra i canali per massimizzare il riutilizzo dei contenuti. L’utilizzo dei contenuti su più canali migliora notevolmente l’efficienza della produzione dei contenuti e la gestione delle modifiche.

##### Stabilire buone convenzioni di denominazione {#naming-conventions}

I nomi dei frammenti di contenuto devono essere descrittivi per gli autori dei contenuti. AEM gestisce in modo trasparente l’escape e/o il troncamento dei nomi degli ID utilizzati a livello di archivio. Pertanto, i nomi logici forniti dagli autori dei contenuti dovrebbero essere sempre leggibili e rappresentare i contenuti.

* Nome non corretto: `cta_btn_1`
* Nome corretto: `Call To Action Button`

Consulta la sezione [risorse aggiuntive](#additional-resources) per ulteriore documentazione sulle convenzioni di denominazione della pagina AEM.

##### Non estendere troppo la nidificazione dei contenuti {#content-nesting}

I [Frammenti di contenuto](#content-fragments) vengono utilizzati in AEM per creare contenuti headless. AEM supporta fino a dieci livelli di nidificazione dei contenuti per i frammenti di contenuto. Tuttavia è importante tenere presente che AEM deve risolvere in modo iterativo ogni riferimento definito nel frammento di contenuto principale, quindi verificare se in tutti gli elementi di pari livello sono presenti riferimenti figlio. Queste operazioni possono sommarsi rapidamente e provocare un problema di prestazioni.

Come regola generale, i riferimenti ai frammenti di contenuto non dovrebbero essere nidificati oltre i cinque livelli.

#### Architetto dei contenuti {#content-architect}

Gli architetti o architette dei contenuti analizzano i requisiti dei dati che devono essere consegnati in modalità headless e ne definisce la struttura. Queste strutture sono chiamate [Modelli per frammenti di contenuto](#content-fragment-models) in AEM. I modelli per frammenti di contenuto vengono utilizzati come base per i frammenti di contenuto creati dagli autori dei contenuti.

Un approccio utile nella definizione dei modelli per frammenti di contenuto consiste nel creare modelli da associare ai componenti UX delle applicazioni che utilizzano il contenuto.

Poiché gli autori dei contenuti interagiscono continuamente con i modelli durante la creazione di nuovi contenuti, l’allineamento dei modelli all’UX li aiuta a visualizzare l’esperienza digitale risultante. Facendo un ulteriore passo avanti, puoi assegnare icone ai Modelli per frammenti di contenuto che rappresentano l’elemento UX in modo che gli autori possano selezionare in modo intuitivo il modello corretto in base ai suggerimenti visivi.

#### Sviluppatore {#developer}

È compito degli sviluppatori unire i contenuti creati in modalità headless in AEM al consumatore di tali contenuti, che spesso possono essere un’applicazione a pagina singola (SPA), un’app web progressiva (PWA), un negozio di web o un altro servizio esterno a AEM.

GraphQL funge da “colla” tra AEM e i consumatori di contenuti headless. GraphQL è la lingua per la ricerca in AEM del contenuto necessario.

Gli sviluppatori devono tenere presenti alcuni consigli di base durante la pianificazione delle query:

* Le query non devono basarsi su un percorso fisso (`ByPath`) per recuperare i frammenti di contenuto.
   * [Gli autori dei contenuti dispongono del controllo completo sulla gerarchia dei frammenti di contenuto](#content-hierarchy) e potrebbero apportare modifiche tali da interrompere la query.
   * Le query devono invece optare per i riferimenti al modello per frammento di contenuto con parametri di query dinamici per filtrare i risultati e generare il payload desiderato.
* Per ottenere le migliori prestazioni delle query, utilizza sempre query persistenti in AEM. Queste sono trattate più avanti nel percorso.
* GraphQL è dichiarativo secondo il motto “Chiedi esattamente ciò di cui hai bisogno, e ottieni esattamente quello.” Ciò significa che, durante la creazione di query GraphQL, devi evitare sempre query di tipo `select *` che è possibile creare in un database relazionale.

Per una [tipica implementazione headless con l’utilizzo di AEM,](#level-1) lo sviluppatore non deve necessariamente conoscere la codifica di AEM.

### Requisiti di prestazioni {#performance-requirements}

Affinché un progetto abbia successo, prima di creare qualsiasi contenuto devono essere considerate le prestazioni.

Devi comprendere le aspettative degli utenti/visitatori e realizzare il progetto di conseguenza. Impostare gli obiettivi del livello di servizio (SLO) e misurarli per capire se si soddisfano le aspettative degli utenti.

#### Modelli di traffico {#traffic-patterns}

Per capire il traffico e i modelli di traffico inizia raccogliendo ciò che sai del passato e poi proiettati verso la crescita prevista negli anni successivi. Alcune delle variabili più importanti da considerare:

* Quante chiamate API ci si aspetta all’ora/giorno/mese, ed esiste il potenziale per picchi e stagionalità?
* Di quanti autori di contenuti diversi si dispone?
* Con quanti autori di contenuti si prevede di lavorare contemporaneamente?
* Qual è la frequenza degli aggiornamenti dei contenuti?
* Quanti modelli di contenuto sono necessari?
* Quante istanze di modelli sono necessarie?

#### Frequenza di aggiornamento {#update-frequency}

Spesso, nelle diverse sezioni di esperienze la frequenza di aggiornamento dei contenuti è diversa. È importante comprendere questo aspetto per poter ottimizzare le configurazioni della CDN e della cache. Questo è anche un importante contributo per gli [Architetti dei contenuti](#content-architects) quando progettano modelli per rappresentare il tuo contenuto. Ritieni che:

* Alcuni tipi di contenuto debbano scadere dopo un determinato periodo di tempo?
* Esistano elementi specifici di un utente e, quindi, non possano essere memorizzati nella cache?

## Passaggio successivo {#what-is-next}

Ora che hai completato questa parte del percorso per sviluppatori headless di AEM, dovresti:

* Comprendere le nozioni di base delle funzioni headless di AEM.
* Conoscere i prerequisiti per l’utilizzo delle funzionalità headless di AEM.
* Essere a conoscenza dei livelli di integrazione headless di AEM.
* Essere in grado di definire il tuo progetto in termini di ambito.

Continua il tuo percorso AEM headless rivedendo il documento successivo [Percorso per la prima esperienza con AEM Headless](path-to-first-experience.md) dove imparerai a configurare gli strumenti necessari e come iniziare a pensare alla modellazione dei tuoi dati in AEM.

## Risorse aggiuntive {#additional-resources}

Mentre si raccomanda di spostarsi nella parte successiva del percorso per lo sviluppo headless esaminando il documento [Percorso per la prima esperienza con AEM Headless,](path-to-first-experience.md) di seguito si trovano alcune risorse aggiuntive e facoltative per approfondire alcuni concetti menzionati in questo documento, ma non sono richieste per continuare il percorso headless.

* [Headful e Headless in AEM](/help/sites-developing/headful-headless.md) - Una discussione completa sui livelli di integrazione headless disponibili in AEM

* Un [Introduzione all’AEM come CMS headless](/help/sites-developing/headless/introduction.md)

* [Percorso di traduzione AEM headless](/help/journey-headless/translation/overview.md) - Questo percorso di documentazione ti consente di comprendere meglio la tecnologia headless, come AEM gestisce i contenuti headless e come tu puoi tradurli.

* [Esercitazioni di AEM Headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=it) - Segui queste esercitazioni pratiche per scoprire come utilizzare le varie opzioni per distribuire contenuti agli endpoint headless con AEM e scegliere quello adatto a te.
* [Gestione dei contenuti headless tramite le API GraphQL](https://experienceleague.adobe.com/?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;launch=ExperienceManager-D-1-2020.1.headless&amp;lang=it#courses) - Segui questo corso per una panoramica dell’API GraphQL implementata in AEM. È necessaria l’autenticazione tramite AdobeID.
* [Guida AEM WKND - GraphQL](https://github.com/adobe/aem-guides-wknd-graphql) - Questo progetto GitHub include applicazioni di esempio che mettono in evidenza le API GraphQL di AEM.
* [Concetti sull’authoring](/help/sites-authoring/author.md) - Documentazione tecnica per l’ambiente di authoring di AEM, compresi i dettagli sull’impostazione di authoring-pubblicazione
* [Pubblicazione delle pagine](/help/sites-authoring/publishing-pages.md) - Documentazione tecnica per la pubblicazione dei contenuti su AEM
* [Convenzioni di denominazione](/help/sites-developing/naming-conventions.md) - Documentazione tecnica sulle restrizioni di denominazione delle pagine in AEM
* [Gestore multisito e traduzione](/help/sites-administering/msm-and-translation.md) - Documentazione tecnica sulle potenti funzioni di traduzione di AEM
* [Flussi di lavoro AEM](/help/sites-authoring/workflows.md) - Documentazione tecnica su come automatizzare i flussi di lavoro in AEM
* [Frammenti di contenuto](/help/assets/content-fragments/content-fragments.md) - Documentazione tecnica per i frammenti di contenuto.
* [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md) - Documentazione tecnica per i modelli per frammenti di contenuto.
* [Documentazione tecnica GraphQL](https://graphql.org) - Definizione di GraphQL (collegamento esterno)
* [API GraphQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) - Documentazione tecnica che spiega come creare richieste di accesso e distribuire frammenti di contenuto
* [API REST di Assets](/help/assets/assets-api-content-fragments.md) - Documentazione tecnica che spiega come creare e modificare Frammenti di contenuto (e altre risorse)
* [Query persistenti](/help/sites-developing/headless/graphql-api/persisted-queries.md) - Documentazione tecnica sulle query persistenti in AEM
* Il [Portale per sviluppatori AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=it)