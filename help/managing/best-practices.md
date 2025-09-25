---
title: Gestione dei progetti - Elenco di controllo delle best practice
description: La gestione di un progetto per l’implementazione di Adobe Experience Manager (AEM) richiede pianificazione e comprensione. Gli elenchi di controllo del progetto sono un set di best practice per la consegna dei progetti. Queste guide presentano tutte le fasi del ciclo di vita del progetto e un monitoraggio di alto livello dello stato.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MANAGING
topic-tags: managing-checklist, introduction
content-type: reference
docset: aem65
exl-id: 94b91996-d2b2-4d4a-b770-334cfa2dc0b7
solution: Experience Manager, Experience Manager 6.5
feature: Compliance
role: Admin,Architect,Data Architect,Developer,Leader
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: ht
source-wordcount: '3212'
ht-degree: 100%

---

# Gestione dei progetti - Elenco di controllo delle best practice{#managing-projects-best-practices-checklist}

La gestione di un progetto per l’implementazione di Adobe Experience Manager (AEM) richiede pianificazione e comprensione, in modo da conoscere i problemi e le decisioni (correlate) da prendere prima e durante l’implementazione del progetto.

Per aiutarti, le best practice consistono in:

* Un [elenco di controllo interattivo](/help/managing/best-practices-checklist.md) che ti consente di tenere traccia e monitorare l’avanzamento con queste best practice.

   * Definiscono gli input e i risultati in base a fase, milestone e utente tipo.
   * Forniscono panoramiche automatizzate (qualità, integrità e completezza) per indicare lo stato di avanzamento e l’integrità del progetto.

* Documentazione basata sull’[elenco di controllo](/help/managing/best-practices-checklist.md) che descrive:

   * Analisi [Heartbeat del progetto](#projectheartbeat).
   * Panoramica dello [Stato per ruolo](#status-by-role).
   * [Fasi e milestone](#phases-and-milestones).
   * [Utente tipo chiave](#persona) e il relativo coinvolgimento in ogni fase (rilevante).
   * Un [Glossario](/help/managing/best-practices-glossary.md) dei [Documenti e risultati richiesti](#required-documents-and-deliverables).

* [Ulteriore materiale di riferimento](/help/managing/best-practices-further-reference.md) per fornire ulteriori dettagli su aree specifiche.

## Dashboard heartbeat del progetto {#project-heartbeat-dashboard}

Il foglio di lavoro **Heartbeat del progetto** fornisce una panoramica grafica delle metriche critiche per il progetto:

* **Qualità fase**

   * Indica la qualità dei [documenti e risultati richiesti](#required-documents-and-deliverables) nel progetto.

* **Integrità fase**

   * Un indicatore di stato di alto livello per il progetto; utile per evidenziare le aree che potrebbero essere a rischio.

* **Completezza fase**

   * In qualsiasi momento durante il progetto, indica quanto è già stato completato per ogni fase del progetto.

## Stato per ruolo {#status-by-role}

Il foglio di lavoro **Stato per ruolo** mostra un raggruppamento dettagliato di [**Integrità**, **Qualità e **Completezza**](#projectheartbeat) per **[Fase](#phases-and-milestones)** e **[Utente tipo](#persona)**.

## Fasi e milestone {#phases-and-milestones}

Il piano del progetto è suddiviso in fasi distinte (di alto livello).

Ogni fase contiene le proprie milestone. Per ogni [utente tipo](#persona) (o ruolo), vengono elencate le milestone pertinenti e i documenti necessari per produrre i risultati definiti.

>[!NOTE]
>
>Non esiste una relazione diretta 1:1 tra i singoli documenti richiesti e i risultati.

### Preparazione {#preparation}

La preparazione del progetto costituisce la base dell’intero progetto. Definisci i requisiti chiave insieme a obiettivi e aspettative chiari per:

* **Base logica aziendale**

   * Le ragioni fondamentali e la giustificazione per intraprendere il progetto.

* **Ambito e pianificazione**

   * Dovrebbe essere reso disponibile un ambito di base e una pianificazione approssimativa per definire ciò che è necessario ed entro quale arco temporale; se questo aiuta a chiarire la situazione, puoi anche definire cosa non rientra nell’ambito.

Il modo in cui prepari, pianifichi ed esegui il progetto e implementi la soluzione è influenzato dalle restrizioni in cui operi. Ad esempio, budget fisso, timeline fissa, quantità di contenuti, qualità richiesta.

Come sempre, la regolazione di uno qualsiasi dei fattori influisce sugli altri. Ad esempio, riducendo il tempo, ma richiedendo lo stesso livello di qualità, è probabile che il prezzo aumenti e che venga ridotta la quantità di contenuti gestibili. Il budget è spesso un fattore chiave, per cui tali relazioni non possono essere dimenticate.

I quattro fattori:

![projectphases_fourphases](assets/projectphases_fourphases.png)

#### Milestone {#milestones}

* **Convalida**

  In questa fase, devi convalidare e confermare gli obiettivi del progetto, ad esempio:

   * Cosa intendi raggiungere/fornire?
   * Chi ne beneficia?
   * Qual è l’ambito?

      * Se aiuta a chiarire la situazione, puoi anche definire che cosa non rientra nell’ambito.

   * Come definiresti il successo?
   * Come si misura il successo?
   * Quali sono i requisiti aziendali e tecnici?
   * Esistono sistemi legacy da sostituire e, in caso affermativo, vi sono dati da migrare?
   * Chi è coinvolto?
   * Come si misura il progresso?
   * Con quale frequenza esamini i progressi compiuti nel corso del progetto?

* **Budget**

  Prima di iniziare un progetto è necessario avere una stima affidabile e realistica dei costi di implementazione:

   * Utilizza le informazioni della milestone di convalida come base per le stime.
   * Esegui delle stime realistiche.
   * Considera e rispetta linee guida, processi o restrizioni a cui il cliente è soggetto.
   * Nel caso in cui in futuro fosse necessario rivedere o perfezionare il budget, prendi in considerazione processi di emergenza e revisione.
   * Tieni presente che i costi possono presentarsi in molte forme, tra cui acquisti, utilizzo di risorse e tariffe.

### Pianificazione {#planning}

La pianificazione del progetto consolida la preparazione. Dovresti iniziare a convertire obiettivi e aspettative in una roadmap ben definita e costituita da compiti concreti, usando una comunicazione chiara ed effettuando revisioni rigorose per misurare i progressi.

#### Milestone {#milestones-1}

* **Consegna**

  Un passaggio di consegne pulito assicura che la persona o i gruppi appropriati siano consapevoli delle loro responsabilità all’interno del progetto.

  Dovrebbero essere forniti/generati dettagli completi per garantire che abbiano una piena comprensione di tutti gli aspetti pertinenti, tra cui la roadmap, l’ambito di applicazione, gli obiettivi, i requisiti e i KPI.

* **Valutazione dei rischi**

  Per evitare spiacevoli sorprese, utilizza la valutazione del rischio per identificare e quantificare i rischi potenziali, insieme al loro impatto e alla loro probabilità.

  Ciò dovrebbe essere fatto nelle prime fasi del ciclo di vita del progetto per garantire che eventuali vulnerabilità siano identificate e valutate. In base ai risultati, puoi riferire alle parti interessate se è possibile implementare tutti i requisiti e, se necessario, pianificare l’adozione e il monitoraggio di azioni appropriate.

* **Comunicazione**

  La comunicazione è sempre fondamentale per il successo di qualsiasi progetto. Comunica in modo chiaro ed efficiente per garantire che tutti siano:

   * Lavorare per raggiungere gli stessi obiettivi di base
   * Dalla stessa base di informazioni
   * Con gli stessi canali

* **Avvio**

  L’incontro iniziale è usato per aumentare la consapevolezza in merito all’inizio del progetto. Si tratta di una buona opportunità per:

   * Invitare tutte le parti interessate (o almeno i rappresentanti dei gruppi).
   * Presentare i fatti chiave del progetto.
   * Rispondere alle domande.
   * Assicurarsi che tutti abbiano la stessa knowledge base.
   * Ottenere la conferma che tutti coloro che saranno coinvolti si impegneranno. Questo obiettivo dovrà essere guadagnato.

      * Coinvolgendo i protagonisti (inclusi i potenziali autori) fin dall’inizio del progetto, aumenti le possibilità che si impegnino per il progetto.

### Preparazione allo sviluppo {#development-preparation}

Pianificare lo sviluppo è fondamentale per garantire che il progetto sia basato su una progettazione solida da parte di un team con le conoscenze richieste.

#### Milestone {#milestones-2}

* **Team di sviluppo con personale e formazione**

  Prima di iniziare un progetto, è necessario assicurarsi che il team di sviluppo disponga di personale appropriato e che tutti i membri del team siano formati per l’attività in corso.

* **Architettura dei contenuti**

  L’architettura dei contenuti definisce e descrive l’architettura futura del contenuto, tra cui:

   * Struttura contenuto, incluse le risorse
   * Strutture di base, incluse le campagne e così via.
   * Strutture multisito e multilingue (MSM, traduzione e così via)
   * Contenuti di supporto (inclusi tag e concetti di tag)
   * Strategie di caching e riutilizzo dei contenuti

* **Architettura di sistema**

  L’architettura del sistema definisce la visualizzazione concettuale del sistema, che include (tra le altre informazioni):

   * [Struttura di sistema](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) per tutti gli ambienti richiesti
   * Sottosistemi
   * Sistemi di terze parti
   * Interfacce; hardware, software e interazione umana
   * Server per ogni ambiente; consulta le [Specifiche tecniche](/help/sites-deploying/technical-requirements.md) e le [Linee guida per il dimensionamento hardware](/help/managing/hardware-sizing-guidelines.md)

   * Processi per ogni ambiente; ad esempio, requisiti di installazione e manutenzione
   * Attività di manutenzione (Datastore GC, ottimizzazione TarPM e così via)
   * Memorizzazione in cache di [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=it)
   * [Cluster](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) di Publish/Authorshare
   * Prestazioni lato client (minimizzazione JS, concat, sprite css, numero totale di richieste http e non solo)

* **Architettura applicazione**

  L’architettura dell’applicazione definisce e descrive il comportamento delle applicazioni proposte.

  È incentrata su:

   * Le modalità in cui interagiscono tra loro e con gli utenti.
   * I dati che devono essere utilizzati e prodotti dalle applicazioni, anziché la loro struttura interna.

  Le definizioni dovrebbero comprendere:

   * Struttura del codice di base per il progetto
   * Artefatti di codice (bundle, pacchetti e così via)
   * Raggruppamenti dei modelli/componenti e delle loro relazioni
   * Dettagli di alto livello delle personalizzazioni richieste (le sovrapposizioni specifiche verranno riportate in seguito)
   * Progettazione dei flussi di lavoro richiesti dalla soluzione (ad esempio creazione, approvazione, pubblicazione, trasformazioni, importazioni ed esportazioni di contenuti)
   * Particolare attenzione per qualsiasi modulo complesso, come MSM, Commerce, integrazione di terze parti

* **Integrazione dei sistemi**

  L’integrazione dei sistemi richiede di pianificare (quindi implementare):

   * Come tutti i sottosistemi e le [integrazioni di soluzioni](/help/sites-administering/integration.md) sono riuniti per funzionare come un unico sistema coerente
   * Come vengono integrati i sistemi di terze parti, insieme a eventuali considerazioni speciali, come stato offline/online, lato client/lato browser o gestione del fallover quando un sistema di terze parti è inattivo

* **Concetto del test**

  Prima di iniziare lo sviluppo, devi elaborare un concetto approfondito e completo di tutti i requisiti di [test](/help/sites-developing/planning.md) per il tuo progetto.

  Dovrebbe includere:

   * Dettagli di tutti i test da eseguire
   * Preparazione di qualsiasi contenuto necessario per tali test
   * Informazioni sugli strumenti di test da utilizzare
   * Indicazione di alto livello di chi sarà coinvolto nei test; in particolare gruppi al di fuori del team di controllo qualità
   * Dettagli dell’automazione dei test; ad esempio, con la modalità Selenium o AEM Developer

* **Progettazione dell’esperienza**

  La progettazione dell’esperienza (XD) prevede la progettazione dell’esperienza utente per la tua soluzione.

  L’esperienza utente deve essere analizzata e sviluppata sia per gli autori che per gli utenti finali del sito web.

* **Configurazione assistenza**

  Prima dello sviluppo, è necessario impostare tutti i processi di supporto necessari per distribuire, rilasciare, testare e segnalare i problemi.

  Consulta anche il [portale di supporto Adobe](https://experienceleague.adobe.com/it?support-solution=General&support-tab=homehome?lang=it#support).

### Pianificazione delle operazioni e operazioni {#operations-planning-and-operations}

Allo stesso modo, le operazioni devono essere pianificate in modo appropriato per garantire la disponibilità degli ambienti necessari per tutte le fasi del ciclo di vita del progetto. Sono inoltre necessari i processi appropriati per la loro gestione.

#### Milestone {#milestones-3}

* **Autorizzazioni**

  È necessario pianificare e quindi implementare un concetto di ruoli e diritti per tutti gli utenti/gruppi che utilizzeranno la soluzione.

  Ad esempio:

   * Un elenco di ruoli (ovvero gruppi) con definizioni di accesso `read`/ `write` per ciascuno

   * La definizione dell’utilizzo dei privilegi che influiscono sull’ambiente di pubblicazione; ad esempio, `replicate`
   * Per gli utenti con privilegi minimi, i flussi di lavoro devono essere definiti
   * Gli utenti del gruppo `editor` non devono avere diritti `admin` né far parte del gruppo `administrators`

  Per ulteriori informazioni, consulta [Amministrazione utenti e sicurezza](/help/sites-administering/security.md).

* **Monitoraggio e manutenzione**

  Il monitoraggio e la manutenzione sono aspetti chiave per garantire il corretto funzionamento della soluzione una volta pubblicata. A questo scopo è necessario definire:

   * Cosa deve essere monitorato
   * Mansioni di manutenzione periodica e in casi speciali

  Per ulteriori informazioni, consulta anche [Monitoraggio e manutenzione](/help/sites-deploying/monitoring-and-maintaining.md).

* **Migrazione**

  Qualsiasi contenuto del sistema legacy deve essere rivisto e convalidato per la migrazione.

* **Piano di ripristino**

  Assicurati di disporre di un piano di ripristino. In situazioni di emergenza, questo deve essere disponibile per garantire l’utilizzo in produzione di AEM... Questo dovrebbe riguardare situazioni come backup, ripristino, blocco e altre.

### Sviluppo {#development}

Lo sviluppo è una fase cruciale che richiede qualcosa di più di una semplice codifica.

#### Milestone {#milestones-4}

* **Ambiente di sviluppo**

  Pianifica e documenta l’ambiente di sviluppo, tra cui:

   * Architettura
   * [Strumenti di sviluppo](/help/sites-developing/dev-tools.md)

      * Un ambiente tipico è costituito da:

         * un sistema di tracciamento dei problemi, ad esempio Jira
         * un IDE, ad esempio Eclipse
         * uno strumento di gestione della build, ad esempio Maven
         * uno strumento per l’integrazione continua, ad esempio Jenkins
         * uno strumento per il controllo delle versioni, ad esempio GIT/SVN
         * un gestore dell’archivio di artefatti di build, ad esempio Archiva/Nexus

   * Integrazione/dipendenze software di terze parti
   * [Integrazione/dipendenze della soluzione](/help/sites-administering/integration.md)
   * Cadenza dell’implementazione

* **Sistema di test**

  Pianifica e documenta l’ambiente di test, tra cui:

   * Architettura
   * Dipendenze dalle build di sviluppo; incluse le build notturne
   * Possibilità o limitazioni di testare l’integrazione/le dipendenze del software di terze parti
   * Strumenti di test
   * Strategia di test automatizzati

* **Sistema di produzione**

  Pianifica e documenta l’ambiente di produzione, tra cui:

   * Architettura
   * Cadenza dell’implementazione
   * Integrazione/dipendenze software di terze parti
   * Configurazione di sicurezza
   * Prestazioni della linea di base verificate eseguendo i [test da carico estremo](/help/sites-developing/tough-day.md) nella configurazione di produzione
   * Requisiti per i test delle prestazioni; consulta [Best practice per la garanzia di qualità](/help/sites-deploying/configuring-performance.md#best-practices-for-quality-assurance)

* **Integrazione**

  Pianifica, documenta e verifica tutti gli aspetti del sistema e dell’[integrazione della soluzione](/help/sites-administering/integration.md), tra cui:

   * Una strategia di test automatizzati
   * Processi automatizzati per [spostare le applicazioni dallo sviluppo al test, quindi alla produzione](/help/managing/enterprise-devops.md#code-movement)
   * Processi automatizzati per [spostare il contenuto dalla produzione al test e allo sviluppo](/help/managing/enterprise-devops.md#content-movement)

* **Migrazione**

  Pianifica, documenta e verifica tutti gli aspetti della migrazione dei contenuti, tra cui:

   * Architettura dei contenuti
   * Strategia di migrazione

* **Comunicazione**

  Assicurati che tutti i membri del gruppo e l’utente tipo del progetto siano tenuti aggiornati, se necessario.

* **Documentazione**

  Documenta completamente la soluzione, inclusi:

   * Manuale operativo
   * Eventuali personalizzazioni che possono influire sugli aggiornamenti
   * Note sulla versione

### Prestazioni e test {#performance-and-testing}

Una volta disponibile, la nuova applicazione deve essere sottoposta a test rigorosi, sia per la funzionalità che per le [prestazioni](/help/sites-deploying/configuring-performance.md).

>[!NOTE]
>
>A qualsiasi team di test deve essere consentito di rimanere neutrale e di fornire i risultati dei test.
>
>È responsabilità del project manager valutare le eventuali implicazioni dei risultati e decidere le azioni appropriate da intraprendere.

#### Milestone {#milestones-5}

* **Test di accettazione per l’utente finale**

  [Il test di accettazione utente](/help/sites-developing/acceptance-signoff.md) (UAT) è fondamentale per garantire che:

   * La soluzione soddisfi le esigenze di utenti/clienti
   * Il cliente/gli utenti accettino la soluzione (funzione, progettazione e prestazioni)

  Dovrebbe essere presente una checklist formalizzata per il passaggio del cliente; idealmente automatizzata ed eseguita di notte su un’istantanea. I risultati devono essere inviati al project manager e al team di sviluppo

* **Test di prestazioni e di carico**

  I test di prestazioni e di carico vengono utilizzati per garantire che la soluzione soddisfi i livelli di prestazioni richiesti, a carichi medi e di picco.

  Per ulteriori informazioni sui test delle prestazioni, consulta:

   * [Test delle prestazioni](/help/sites-deploying/configuring-performance.md)
   * [Pianificazione ed esecuzione dei test](/help/sites-developing/planning.md)

   * [Linee guida sulle prestazioni di base](/help/sites-deploying/configuring-performance.md#basic-performance-guidelines)

  >[!NOTE]
  >
  >Il processo deve essere continuato durante il normale utilizzo di AEM, ma queste fasi iniziali sono le più importanti.

### Rollout {#rollout}

Il rollout della nuova applicazione richiede un’attenta pianificazione per garantire una pubblicazione senza problemi. Ciò include la conferma di un elevato livello di sicurezza, la formazione di tutti i potenziali utenti e l’esecuzione di più cicli di prova per confermare che tutti i problemi siano stati risolti.

#### Milestone {#milestones-6}

* **Preparazione**

  La preparazione e la pianificazione contribuiranno a garantire un rollout senza problemi.

* **Formazione**

  Assicurati che tutto il personale coinvolto abbia ricevuto una formazione adeguata.

  Consulta [Adobe Experience Manager](https://training.adobe.com/training/courses.html#solution=adobeExperienceManager) nel catalogo dei corsi.

* **Amministratori con formazione**

  Assicurati che gli amministratori della soluzione abbiano:

   * Ricevuto una formazione
   * Ricevuto materiale di formazione adeguato
   * Ricevuto la documentazione appropriata

* **Utenti con formazione**

  Assicurati che gli autori abbiano:

   * Ricevuto una formazione
   * Ricevuto materiale di formazione adeguato
   * Ricevuto la documentazione appropriata, ad esempio la Guida utente

* **Test di penetrazione**

  I test di penetrazione simulano un attacco a un sistema informatico per identificare potenziali punti deboli nella sicurezza.

* **Test di penetrazione/sicurezza**

  Per garantire la sicurezza della soluzione, esegui test di penetrazione specifici oltre a una gamma più ampia di test sulla sicurezza.

  Per ulteriori dettagli, consulta l’[elenco di controllo della sicurezza](/help/sites-administering/security-checklist.md).

### Pubblicazione {#go-live}

Desideri che la tua pubblicazione sia la più semplice possibile. Anche in questo caso, i passaggi finali devono essere pianificati per un’esecuzione senza problemi.

#### Milestone {#milestones-7}

* **Preparazione**

  La preparazione e la pianificazione contribuiranno a garantire una pubblicazione senza intoppi.

* **Sicurezza**

  Conferma la sicurezza della soluzione per gli utenti interni ed esterni e per i relativi contenuti.

* **Regresso**

  Assicurati che tutti i sistemi, le procedure e i meccanismi necessari per il regresso siano operativi prima della pubblicazione.

* **Supporto**

  Assicurati che i servizi di supporto siano pronti a intervenire.

* **Transizione**

  Pianifica ed esegui la transizione all’ambiente e agli utenti di produzione.

* **Rollout**

  Prepara ed esegui gli smoke test.

## Utente tipo {#persona}

Gli elenchi di controllo sono progettati in base all’utente tipo. Si tratta dei ruoli con un coinvolgimento significativo nel ciclo di vita del progetto.

Ci sono anche alcuni [altri utenti tipo](#other-persona) coinvolti in attività specifiche.

### Sponsor del progetto {#project-sponsor}

Lo sponsor del progetto è:

* Responsabile della redazione/presentazione del caso di business del progetto.
* Essenziale per plasmare e definire l’ambito del progetto, compresi:

   * la definizione e i criteri della buona riuscita
   * i KPI principali

* Fornisci i milestone principali in base alla roadmap del client.

### Project Manager {#project-manager}

Il project manager è:

* Responsabile della consegna complessiva del progetto in base ai requisiti (ad esempio, ambito, KPI, criteri di buona riuscita e definizione) forniti dallo sponsor del progetto.
* Responsabile della definizione del budget e delle risorse del progetto in base a tale budget.
* Il punto di comunicazione principale per tutti gli utenti tipo coinvolti nel progetto.

### Architetto {#architect}

L’architetto della soluzione:

* È responsabile del design di alto livello della soluzione e del sistema.
* Consente di definire la strategia di implementazione per AEM. Ad esempio, se implementare un’installazione in cluster, uno standby a freddo o quando è necessaria una rete per la consegna dei contenuti (Content Delivery Network, CDN).
* Definisce inoltre l’architettura della soluzione AEM in base ai requisiti del client. Può includere il concetto di ruoli utente (con i relativi diritti), la relazione tra modelli e componenti o quando utilizzare la gestione multisito.

### Analista aziendale {#business-analyst}

L’analista aziendale:

* È principalmente responsabile della raccolta e dell’analisi dei requisiti di alto livello, per poi trasformarli in specifiche:

   * per il project manager affinché li utilizzi durante la pianificazione dello sviluppo
   * per il team di sviluppo affinché possa lavorarci durante la progettazione e lo sviluppo.

* Collabora strettamente con il client per analizzare i requisiti. Questi requisiti vengono confrontati con:

   * La definizione di buona riuscita.
   * I criteri per la buona riuscita.
   * KPI (sia aziendali sia basati sulle prestazioni).

### Lead di sviluppo {#development-lead}

Il lead di sviluppo:

* È responsabile dell’esecuzione tecnica del progetto.
* È responsabile della selezione di una metodologia di sviluppo conforme ai requisiti del client.
* Delinea la strategia di sviluppo:

   * garantendo l’allineamento con i KPI aziendali e basati sulle prestazioni
   * tenendo conto dei criteri di buona riuscita e della definizione

* Collabora strettamente con l’architetto (in particolare durante la definizione della strategia di sviluppo per AEM) per definire aspetti quali la relazione tra modelli e componenti, la strategia di integrazione per applicazioni di terze parti ed eventuali funzionalità specializzate.

### Lead di qualità {#quality-lead}

Il lead di qualità:

* È responsabile della qualità dell’esecuzione; si assicura che soddisfi i criteri per la buona riuscita e tutti i KPI definiti dal client.
* Definisce le metriche della qualità, si allinea con tutte le parti interessate, elabora i piani di test e ne assicura l’esecuzione.
* Crea e consegna rapporti alle parti interessate del progetto.

### Tecnico di sistema {#system-engineer}

Il tecnico di sistema:

* È responsabile della supervisione dell’infrastruttura del progetto.
* È responsabile di:

   * configurare gli ambienti interni di sviluppo e di test
   * abbinare tali sistemi ai sistemi del client

* Fornisce consigli sull’hardware, monitora le varie implementazioni e offre supporto operativo sia prima che dopo la pubblicazione.

### Lead di sicurezza {#security-lead}

Il lead di sicurezza:

* È responsabile del concetto di sicurezza generale della soluzione, verificando che sia allineata a eventuali requisiti e criteri del client.
* Mette in atto il concetto di sicurezza, operazioni di sicurezza e offre consigli per qualsiasi concetto di sicurezza basato su hardware, ad esempio zone e firewall.

### Altri utenti tipo {#other-persona}

* Stakeholder

   * Persone (spesso dell’azienda) che hanno un interesse (partecipazione) alla buona riuscita del progetto. Spesso contribuiscono al bilancio.

* Legale

   * Durante la negoziazione dei contratti è richiesta una consulenza legale.

* Formatori

   * A seconda delle dimensioni e della natura del progetto, i formatori specializzati possono essere utilizzati per sviluppare e presentare sessioni di formazione ai gruppi pertinenti.

* Autori di contenuti tecnici

   * A seconda delle dimensioni e della natura del progetto, gli autori di contenuti tecnici specializzati possono essere utilizzati per redigere linee guida e manuali per gruppi specifici. Ad esempio, un manuale di manutenzione per gli amministratori di sistema o una guida utente per gli autori di contenuti.

* Amministratori di sistema

   * Responsabile del funzionamento continuo del sistema.

* Autori e utenti finali

   * Persone che utilizzano il sistema per creare e gestire il contenuto del sito web.

## Documenti richiesti e risultati {#required-documents-and-deliverables}

Gli elenchi di controllo coprono i **documenti richiesti** e i **risultati** per ogni milestone.

* Non esiste alcuna relazione :1 tra questi documenti; ad esempio, un gruppo di documenti richiesti può produrre un singolo risultato.
* Un risultato da un utente tipo può essere un documento richiesto per un altro utente tipo durante la stessa milestone.

### Documenti richiesti {#required-documents}

I **documenti richiesti** sono necessari all’utente tipo appropriato durante la produzione dei risultati.

Per ogni **documento richiesto**, l’utente tipo deve indicare:

* **Sì/No**: se è stato ricevuto.
* **1-3**: indicazione della qualità del documento ricevuto.

### Risultati {#deliverables}

Per ogni milestone, l’utente tipo appropriato è responsabile della consegna di specifici documenti e, di conseguenza, di adempiere alle proprie responsabilità relative a una determinata milestone.

Per ogni **risultato**, l’utente tipo deve indicare:

* **Sì/No**: se è stato completato.

I risultati vengono spesso utilizzati come **Documenti richiesti** per la milestone corrente o successiva.

## Best practice correlate {#related-best-practices}

Per le best practice sull’implementazione, l’amministrazione, lo sviluppo o l’authoring, consulta quanto segue:

* Altre best practice e linee guida relative alla gestione di un progetto AEM:
   * [Linee guida per le dimensioni dell’hardware](/help/managing/hardware-sizing-guidelines.md)
   * [DevOps aziendale](/help/managing/enterprise-devops.md)
   * [Best practice per la gestione di SEO e URL](/help/managing/seo-and-url-management.md)
   * [AEM e le Linee guida di accessibilità dei contenuti web](/help/managing/web-accessibility.md)
   * [Regolamento generale sulla protezione dei dati](/help/managing/data-protection-and-privacy.md)* [Implementazione e manutenzione delle best practice](/help/sites-deploying/best-practices.md)
* [Amministrazione delle best practice](/help/sites-administering/administer-best-practices.md)
* [Sviluppo delle best practice](/help/sites-developing/best-practices.md)
* [Authoring delle best practice](/help/sites-authoring/best-practices.md)

## Aree principali della documentazione {#key-documentation-areas}

* Documentazione di AEM
Inoltre, le seguenti sezioni della documentazione di AEM sono di particolare interesse (tuttavia, questo elenco non è esaustivo):

   * [Protezione](/help/sites-developing/security.md)
   * [Distribuzioni consigliate](/help/sites-deploying/recommended-deploys.md)
   * [DevOps aziendale](/help/managing/enterprise-devops.md)
   * [Dimensionamento hardware](/help/managing/hardware-sizing-guidelines.md)
   * Concetti di AEM:

      * [Sviluppo: nozioni di base](/help/sites-developing/the-basics.md)
      * [Concetti MSM](/help/sites-administering/msm.md)
      * [HTML Template Language (HTL)](https://experienceleague.adobe.com/it/docs/experience-manager-htl/content/overview)

* Documentazione correlata

   * Adobe Experience Cloud: [pianificazione per Adobe Experience Cloud](https://experienceleague.adobe.com/it/docs/core-services/interface/services/overview)
