---
title: Guida introduttiva ad AEM Headless
description: In questa parte del Percorso di sviluppo headless AEM, scopri AEM prerequisiti headless.
source-git-commit: 919cef01470dd930884e97b15f2d40a38872c0d0
workflow-type: tm+mt
source-wordcount: '3031'
ht-degree: 1%

---

# Guida introduttiva ad AEM Headless {#getting-started}

In questa parte del [AEM Percorso di sviluppo headless,](overview.md) scopri cosa è necessario per avviare il tuo progetto con AEM Headless.

## La storia finora {#story-so-far}

Nel documento precedente del percorso senza testa AEM, [Scopri lo sviluppo di CMS Headless](learn-about.md) hai imparato la teoria di base su cosa sia un CMS headless e dovresti ora:

* Comprendere i concetti e la terminologia di base per la distribuzione di contenuti headless
* Capire perché e quando è richiesto un headless
* Conoscere ad alto livello come vengono utilizzati i concetti senza testa e come si relazionano

Questo articolo si basa su questi elementi fondamentali per comprendere come utilizzare AEM per implementare una soluzione headless.

## Obiettivo {#objective}

Questo documento ti aiuta a capire AEM Headless nel contesto del tuo progetto. Dopo la lettura è necessario:

* Comprendere le nozioni di base AEM funzioni headless.
* Conoscere i prerequisiti per l&#39;utilizzo di AEM funzionalità headless.
* Presta attenzione AEM livelli di integrazione headless.
* Puoi definire il tuo progetto in termini di ambito.

## Nozioni di base su AEM {#aem-basics}

Prima di poter definire il progetto headless all’interno di AEM, è importante comprendere alcuni concetti AEM di base.

### Istanza autore {#author}

Al più semplice, AEM consiste di un&#39;istanza dell&#39;autore e di un [pubblica istanza](#publish) che collaborano per creare, gestire e pubblicare i contenuti.

Il contenuto inizia nell’istanza di authoring. In questo caso gli autori dei contenuti creano i propri contenuti. L’ambiente di authoring offre agli autori diversi strumenti per creare, organizzare e riutilizzare i contenuti.

### Pubblica istanza {#publish}

Una volta creato il contenuto nell’istanza di authoring, deve essere pubblicato per essere disponibile ad altri servizi da utilizzare. Un’istanza di pubblicazione contiene tutti i contenuti pubblicati.

### Replica {#replication}

La replica è l’atto di trasferire il contenuto dall’istanza di authoring all’istanza di pubblicazione. Questa operazione viene eseguita automaticamente da AEM quando un autore o un altro utente con i diritti appropriati pubblica il contenuto.

### Riepilogo delle AEM di base {#aem-basics-summary}

Al livello più semplice, la creazione di esperienze digitali in AEM richiede i seguenti passaggi:

1. Gli autori dei contenuti creano i contenuti headless nell’istanza di authoring.
1. Quando il contenuto è pronto, viene replicato nell’istanza di pubblicazione.
1. Puoi quindi chiamare le API per recuperare questo contenuto.

AEM Headless sviluppa questa base tecnica offrendo potenti strumenti per gestire contenuti headless che è [descritto nella sezione successiva.](#aem-headless-basics)

## Nozioni di base AEM senza testa {#aem-headless-basics}

Le funzionalità headless di AEM si basano su alcune funzioni chiave. Questi sono spiegati in dettaglio nelle parti successive del percorso. Ora è importante solo conoscere le basi di ciò che fanno e di ciò che vengono chiamati.

### Modelli per frammenti di contenuto {#content-fragment-models}

I modelli per frammenti di contenuto definiscono la struttura dei dati e del contenuto creati e gestiti in AEM. Servono come una sorta di impalcatura per i vostri contenuti. Quando scegli di creare un contenuto, gli autori selezionano tra i modelli di frammento di contenuto definiti, che li guida nella creazione di contenuti.

### Frammenti di contenuto {#content-fragments}

I frammenti di contenuto consentono di progettare, creare, curare e pubblicare contenuti indipendenti dalla pagina. Consentono di preparare i contenuti pronti per l’uso in più posizioni e su più canali.

I frammenti di contenuto contengono contenuto strutturato e possono essere consegnati in formato JSON.

### API GraphQL e REST {#apis}

Per modificare il contenuto senza problemi, AEM offre due solide API.

* L’API GraphQL consente di creare richieste di accesso e distribuzione di frammenti di contenuto.
* L’API REST di Assets consente di creare e modificare frammenti di contenuto (e altre risorse).

Scoprirai queste API e come utilizzarle in una parte successiva del percorso AEM headless. Oppure fai riferimento al [risorse aggiuntive](#additional-resources) per ulteriore documentazione.

## Livelli di integrazione headless {#integration-levels}

AEM supporta sia i modelli full headless che quelli tradizionali full stack o headful di un CMS. Tuttavia AEM offre non solo queste due opzioni esclusive, ma anche la possibilità di supportare modelli ibridi che combinano i vantaggi di entrambi, offrendo una flessibilità unica per il vostro progetto headless.

Al fine di garantire la comprensione dei concetti headless, questo Percorso AEM Headless Developer si concentra sul modello headless puro per consentirti di iniziare a lavorare il prima possibile senza codifica in AEM.

Tuttavia, è necessario essere consapevoli delle possibilità ibride aggiuntive aperte a voi una volta compreso AEM caratteristiche headless. Questi casi sono indicati di seguito per la vostra consapevolezza. Al termine del percorso, riceverai informazioni più dettagliate su questi concetti nel caso in cui sia necessaria tale flessibilità per il tuo progetto.

### Esiste già un consumo esterno di contenuto headless, ad esempio una singola applicazione pagina (SPA). {#already-have-a-spa}

Supponiamo che i requisiti di base per la distribuzione dei contenuti da AEM a un servizio esterno esistente siano minimi.

#### Livello 1: Integrazione dei frammenti di contenuto - Modello tradizionale headless {#level-1}

Questo livello di integrazione è il modello headless tradizionale e consente agli autori di contenuti di creare contenuti in AEM e distribuirli senza problemi a qualsiasi numero di servizi esterni tramite GraphQL o di modificarli da servizi esterni tramite l’API Assets. Non è richiesta alcuna codifica in AEM.

In questo modello, AEM viene utilizzato solo per creare e distribuire il contenuto utilizzando AEM Frammenti di contenuto. Il rendering e l’interazione con il contenuto vengono delegati all’applicazione esterna che consuma, spesso un’applicazione a pagina singola (SPA).

#### Livello 2: Incorpora il SPA in AEM - Modello ibrido {#level-2}

Questo livello di integrazione si basa sul primo livello, ma consente anche di incorporare in AEM l’applicazione esterna (SPA) in modo che gli autori dei contenuti possano visualizzare il contenuto nel contesto dell’applicazione esterna in AEM. L&#39;applicazione può anche supportare la modifica limitata dell&#39;applicazione esterna in AEM.

Questo livello offre il vantaggio di consentire agli autori di contenuti di creare in modo flessibile i contenuti in AEM in modo headful, con i contenuti contestuali presentati con un SPA esterno incorporato, e allo stesso tempo consegnarli senza problemi.

#### Livello 3: Incorpora e abilita completamente SPA in AEM - Modello ibrido {#level-3}

Questo livello di integrazione si basa sul secondo livello, consentendo la modifica della maggior parte dei contenuti del SPA esterno in AEM.

### Non disponi ancora di un consumatore esterno del contenuto headless, ad esempio un’applicazione a pagina singola (SPA). {#do-not-have-a-spa}

Se l’obiettivo è quello di creare un nuovo SPA che consuma senza problemi contenuti da AEM, puoi utilizzare funzioni quali Frammenti di contenuto per gestire i contenuti headless e creare un SPA con AEM framework dell’editor SPA.

Utilizzando l’editor di SPA, il SPA non solo consuma contenuti da AEM, ma è anche completamente modificabile all’interno di AEM dagli autori di contenuti, offrendoti la flessibilità della distribuzione headless e della modifica contestuale in AEM.

## Requisiti e prerequisiti {#requirements-prerequisites}

Ci sono diversi requisiti prima di iniziare il progetto di AEM headless.

### Conoscenza {#knowledge}

* GraphQL
* Creare esperienze di sviluppo SPA con i framework React o Angular
* AEM di base per la creazione di frammenti di contenuto e l’utilizzo dell’editor

### Strumenti {#tools}

* Accesso alla sandbox per i test di distribuzione del progetto
* Istanza di sviluppo locale per la modellazione e il test dei dati
* SPA esterna esistente o altro consumatore del contenuto AEM headless

## Definizione del progetto {#defining-your-project}

Per ogni progetto di successo è importante definire chiaramente non solo i requisiti del progetto, ma anche i ruoli e le responsabilità.

### Ambito {#scope}

È importante disporre di un ambito di applicazione chiaramente definito per il progetto. Ambito informa i criteri di accettazione e consente di stabilire una definizione di fatto.

La prima domanda che dovete fare è &quot;Cosa sto cercando di ottenere con AEM Headless?&quot; In generale, la risposta dovrebbe essere che in futuro disponi o disporrai di un’applicazione di esperienza che hai creato con i tuoi strumenti di sviluppo e non con AEM. Questa applicazione di esperienza potrebbe essere un’app mobile, un sito web o qualsiasi altra applicazione per l’esperienza con i clienti finali. L’obiettivo per utilizzare AEM Headless è quello di alimentare l’applicazione di esperienza con contenuti creati, memorizzati e gestiti in AEM con API all’avanguardia che richiamerebbero AEM Headless per recuperare contenuti o persino contenuti CRUD completamente direttamente dall’applicazione di esperienza. Se questo non è quello che si sta cercando di fare, probabilmente si desidera [torna alla documentazione AEM](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=it) e trova la sezione che meglio si adatta a ciò che desideri realizzare.

### Ruoli e responsabilità {#roles-responsibilities}

I ruoli di ogni singolo progetto variano, ma quelli importanti da considerare nel contenuto di AEM sviluppo headless sono:

* [Administrator](#administrator)
* [Autore del contenuto](#content-author)
* [Architetto dei contenuti](#content-architect)
* [Developer (Sviluppatore)](#developer)

#### Amministratore {#administrator}

L&#39;amministratore è responsabile della configurazione e della configurazione di base del sistema. Ad esempio, l’amministratore configura l’organizzazione all’interno del sistema di gestione utenti di Adobe, denominato Identity Management System (IMS). L’amministratore è il primo utente dell’organizzazione a ricevere un invito e-mail da Adobe dopo che l’organizzazione è stata creata per Adobe in IMS. L’amministratore può accedere a IMS e aggiungere utenti di altri utenti.

Una volta configurati dall’amministratore, gli utenti ricevono le autorizzazioni per accedere a tutte le risorse di AEM per svolgere il loro lavoro come collaboratori per la distribuzione dell’applicazione di esperienza utilizzando AEM Headless.

L’amministratore deve essere l’utente che configura AEM e prepara l’ambiente di runtime per abilitare [autori di contenuti](#content-author) per creare e aggiornare contenuti e [sviluppatori](#developer) per utilizzare API che recuperano o modificano il contenuto per le applicazioni di esperienza.

#### Autore del contenuto {#content-author}

Gli autori dei contenuti creano e gestiscono i contenuti consegnati senza problemi da AEM. Gli autori di contenuti utilizzano funzioni AEM quali Frammenti di contenuto e la console Risorse per gestirne i contenuti.

Gli autori dei contenuti devono tenere presenti le seguenti best practice.

#### Piano di traduzione {#translation}

Piano per la traduzione all&#39;inizio del progetto. Considera &quot;Specialista della traduzione&quot; come un personaggio distinto la cui responsabilità è quella di definire quali contenuti dovrebbero essere tradotti e quali no, e quali contenuti tradotti possono essere modificati dai produttori di contenuti regionali o locali.

Crea un piano per la traduzione dei contenuti necessaria.

* Hai bisogno di lingue diverse o anche lingue diverse da adottare per le specifiche regionali?
* È necessario che contenuti rich media come immagini o video siano diversi per diverse impostazioni internazionali?

Fai clic sul flusso di lavoro di aggiornamento dei contenuti . Qual è il processo di approvazione che il sistema deve supportare? È possibile utilizzare AEM flussi di lavoro per automatizzare questo processo?

Tieni presente che [gerarchia dei contenuti](#content-hierarchy) può essere sfruttato per semplificare la traduzione.

Consulta la sezione [risorse aggiuntive](#additional-resources) sezione per la documentazione aggiuntiva sui flussi di lavoro AEM e gli strumenti di traduzione, compresi i collegamenti al Percorso di traduzione AEM headless.

##### Utilizzo della gerarchia dei contenuti {#content-hierarchy}

La gerarchia delle cartelle può risolvere due problemi principali relativi alla gestione dei contenuti:

* [Traduzione](#translation) - AEM gestire la traduzione dei contenuti mantenendo copie dei contenuti in cartelle specifiche delle impostazioni internazionali.
* Organizzazione : le cartelle vengono utilizzate per definire una gerarchia di contenuti necessaria per supportare le esigenze di traduzione e per gestire in modo logico i frammenti di contenuto.

AEM consente una struttura dei contenuti flessibile e una gerarchia può essere arbitrariamente grande. Tuttavia è importante rendersi conto che eventuali modifiche nella struttura delle cartelle possono avere conseguenze indesiderate per le query esistenti che [basati sul percorso del contenuto.](#developer) Pertanto, una gerarchia ben definita, chiaramente definita in anticipo, può essere utile per gli autori dei contenuti.

Le cartelle possono anche essere limitate per consentire solo alcuni tipi di contenuto (in base a Modelli per frammenti di contenuto). Si consiglia di specificare sempre in modo esplicito quali modelli sono consentiti per tutte le cartelle nella gerarchia. Specifica del contenuto consentito per una determinata cartella:

* Impedisce agli autori di contenuti di creare contenuti che non appartengono alla cartella.
* Ottimizza il processo di creazione dei contenuti filtrando i tipi di contenuto consentiti nella cartella durante la creazione per mostrare solo i tipi di contenuto validi.

La creazione di una struttura di contenuto appropriata rende più facile coordinare l’authoring di contenuti headless tra i diversi canali al fine di ottimizzare il riutilizzo dei contenuti. L’utilizzo dei contenuti su più canali migliora notevolmente l’efficienza della produzione dei contenuti e la gestione delle modifiche.

##### Stabilire buone convenzioni di denominazione {#naming-conventions}

I nomi dei frammenti di contenuto devono essere descrittivi per gli autori dei contenuti. AEM gestisce in modo trasparente l’escape e/o il troncamento dei nomi utilizzati a livello di archivio. Pertanto, i nomi logici forniti dagli autori dei contenuti devono essere sempre leggibili e rappresentare i contenuti.

* Nome non valido: `cta_btn_1`
* Nome: `Call To Action Button`

Consulta la sezione [risorse aggiuntive](#additional-resources) per ulteriore documentazione sulle convenzioni di denominazione AEM pagina.

##### Non estendere la nidificazione dei contenuti {#content-nesting}

[Frammenti di contenuto](#content-fragments) vengono utilizzati in AEM per creare contenuti headless. AEM supporta fino a dieci livelli di nidificazione dei contenuti per i frammenti di contenuto. Tuttavia è importante tenere presente che AEM risolvere in modo iterativo ogni riferimento definito nel frammento di contenuto padre, quindi verificare se in tutti gli elementi di pari livello sono presenti riferimenti figlio. Queste operazioni possono aumentare rapidamente e diventare un problema di prestazioni.

Come regola generale, i riferimenti ai frammenti di contenuto non devono essere nidificati oltre i cinque livelli.

#### Architetto dei contenuti {#content-architect}

Gli architetti di contenuti analizzano i requisiti dei dati da distribuire senza problemi e definiscono la struttura di tali dati. Queste strutture sono chiamate [Modelli per frammenti di contenuto](#content-fragment-models) in AEM. I modelli per frammenti di contenuto vengono utilizzati come base per i frammenti di contenuto creati dagli autori dei contenuti.

Un approccio utile nella definizione dei modelli di frammento di contenuto consiste nel creare modelli da associare ai componenti UX delle applicazioni che utilizzano il contenuto.

Poiché gli autori dei contenuti interagiscono continuamente con i modelli durante la creazione di nuovi contenuti, l’allineamento dei modelli all’UX li aiuta a visualizzare l’esperienza digitale risultante. Facendo un ulteriore passo avanti, puoi assegnare icone ai Modelli di frammento di contenuto che rappresentano l’elemento UX in modo che gli autori possano selezionare in modo intuitivo il modello corretto in base ai suggerimenti visivi.

#### Developer (Sviluppatore) {#developer}

Gli sviluppatori sono responsabili di unire i contenuti creati senza problemi AEM al consumatore di tali contenuti, che spesso possono essere un’applicazione a pagina singola (SPA), un’app web progressiva (PWA), un negozio di web o un altro servizio esterno a AEM.

GraphQL funge da &quot;colla&quot; tra AEM e consumatori di contenuti headless. GraphQL è la lingua che richiede AEM per il contenuto necessario.

Gli sviluppatori devono tenere presenti alcuni consigli di base durante la pianificazione delle query:

* Le query non devono basarsi su un percorso fisso (`ByPath`) per recuperare i frammenti di contenuto.
   * [Gli autori dei contenuti dispongono del controllo completo sulla gerarchia dei frammenti di contenuto](#content-hierarchy) e potrebbe apportare modifiche che potrebbero interrompere tale query.
   * Le query devono invece optare per i riferimenti al modello di frammento di contenuto con parametri di query dinamici per filtrare i risultati e generare il payload desiderato.
* Per ottenere le migliori prestazioni delle query, utilizza sempre query persistenti in AEM. Questi sono trattati più avanti nel percorso.
* GraphQL è dichiarativo seguendo il motto &quot;Chiedi esattamente quello che ti serve, e ottieni esattamente quello.&quot; Ciò significa che, quando si creano query GraphQL, evita sempre `select *`Query di tipo -che è possibile creare in un database relazionale.

Per [tipica implementazione headless utilizzando AEM,](#level-1) lo sviluppatore non richiede alcuna conoscenza della AEM di codifica.

### Requisiti di prestazioni {#performance-requirements}

Affinché un progetto abbia successo, le prestazioni devono essere considerate prima di creare qualsiasi contenuto.

Devi comprendere le aspettative degli utenti/visitatori e progettarle. Impostare gli obiettivi del livello di servizio (SLOs) e misurarli per capire se si soddisfano le aspettative degli utenti.

#### Pattern di traffico {#traffic-patterns}

Per capire il traffico e i modelli di traffico inizia raccogliendo ciò che si sa dal passato e poi proiettare verso la crescita prevista nei prossimi anni. Alcune delle variabili più importanti da considerare:

* Quante chiamate API si aspettano all’ora/giorno/mese ed è possibile ottenere picchi e stagionalità?
* Quanti autori di contenuti diversi esistono?
* Quanti autori di contenuti prevedete di lavorare contemporaneamente?
* Qual è la frequenza degli aggiornamenti dei contenuti?
* Quanti modelli di contenuto sono necessari?
* Quante istanze di modelli sono necessarie?

#### Aggiorna frequenza {#update-frequency}

Spesso diverse sezioni di esperienze hanno diverse frequenze di aggiornamenti dei contenuti. È importante per poter perfezionare le configurazioni di CDN e cache. Questo è anche un importante contributo per [Architetti dei contenuti](#content-architects) mentre progettano modelli per rappresentare il tuo contenuto. Considera:

* Alcuni tipi di contenuto devono scadere dopo un determinato periodo di tempo?
* Esistono elementi specifici dell’utente e quindi non possono essere memorizzati nella cache?

## Novità {#what-is-next}

Dopo aver completato questa parte del Percorso di sviluppatori AEM Headless, devi:

* Comprendere le nozioni di base AEM funzioni headless.
* Conoscere i prerequisiti per l&#39;utilizzo di AEM funzionalità headless.
* Presta attenzione AEM livelli di integrazione headless.
* Puoi definire il tuo progetto in termini di ambito.

Continua il tuo percorso AEM headless rivedendo il documento successivo [Percorso per la prima esperienza con AEM Headless](path-to-first-experience.md) dove imparerai a configurare gli strumenti necessari e come iniziare a pensare alla modellazione dei tuoi dati in AEM.

## Risorse aggiuntive {#additional-resources}

Mentre è consigliabile passare alla parte successiva del percorso di sviluppo headless rivedendo il documento [Percorso alla tua prima esperienza utilizzando AEM Headless,](path-to-first-experience.md) di seguito sono riportate alcune risorse aggiuntive facoltative che approfondiscono alcuni concetti menzionati in questo documento, ma non è necessario che continuino sul percorso headless.

* [AEM Percorso di traduzione headless](/help/journey-headless/translation/overview.md) - Questo percorso di documentazione ti offre un’ampia comprensione della tecnologia headless, di come AEM i contenuti headless e di come tradurli.
* [AEM Tutorials headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html) - Segui questi tutorial pratici per scoprire come utilizzare le varie opzioni per distribuire contenuti agli endpoint headless con AEM e scegliere quello che fa per te.
* [Gestione dei contenuti headless tramite API GraphQL](https://experienceleague.adobe.com/?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;launch=ExperienceManager-D-1-2020.1.headless#courses) - Segui questo corso per una panoramica dell’API GraphQL implementata in AEM. È necessaria l’autenticazione tramite AdobeID.
* [Guide AEM WKND - GraphQL](https://github.com/adobe/aem-guides-wknd-graphql) - Questo progetto GitHub include applicazioni di esempio che evidenziano AEM API GraphQL.
* [Authoring dei concetti](/help/sites-authoring/author.md) - Documentazione tecnica per l&#39;ambiente di authoring dei AEM, compresi i dettagli sull&#39;impostazione di authoring-pubblicazione
* [Pubblicazione delle pagine](/help/sites-authoring/publishing-pages.md) - Documentazione tecnica per la pubblicazione dei contenuti su AEM
* [Convenzioni di denominazione](/help/sites-developing/naming-conventions.md) - Documentazione tecnica sulle restrizioni di denominazione delle pagine in AEM
* [Gestione multisito e traduzione](/help/sites-administering/msm-and-translation.md) - Documentazione tecnica su AEM potenti funzioni di traduzione
* [Flussi di lavoro AEM](/help/sites-authoring/workflows.md) - Documentazione tecnica su come automatizzare i flussi di lavoro in AEM
* [Frammenti di contenuto](/help/assets/content-fragments/content-fragments.md) - Documentazione tecnica per i frammenti di contenuto.
* [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md) - Documentazione tecnica per i modelli di frammenti di contenuto.
* [Documentazione tecnica di GraphQL](https://graphql.org) - Definizione GraphQL (collegamento esterno)
* [API GraphQL](/help/assets/content-fragments/graphql-api-content-fragments.md) - Documentazione tecnica che spiega come creare richieste di accesso e distribuzione di frammenti di contenuto
* [API REST di Assets](/help/assets/assets-api-content-fragments.md) - Documentazione tecnica che spiega come creare e modificare Frammenti di contenuto (e altre risorse)
* [Query persistenti](/help/assets/content-fragments/graphql-api-content-fragments.md#persisted-queries-caching) - Documentazione tecnica sulle query persistenti in AEM
* [Cefalea e senza testa in AEM](/help/sites-developing/headful-headless.md) - Una discussione completa sui livelli di integrazione headless disponibili in AEM
