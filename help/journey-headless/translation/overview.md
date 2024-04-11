---
title: Percorso di traduzione headless di AEM
description: Inizia qui per un percorso guidato alla traduzione di contenuti headless utilizzando i potenti strumenti di traduzione di AEM.
exl-id: 1a9d4c88-b676-4168-a9ef-7d218b39129f
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,Language Copy
role: Admin, Architect,Data Architect,Developer,User,Leader
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 93%

---

# Percorso di traduzione headless di AEM {#aem-headless-translation-journey}

Inizia qui per un percorso guidato alla traduzione di contenuti headless utilizzando i potenti strumenti di traduzione di AEM.

## Introduzione {#introduction}

L’implementazione headless sta diventando sempre più importante per la distribuzione di esperienze al pubblico, ovunque si trovino e indipendentemente dal canale, dall’area geografica o dalle impostazioni internazionali.

L’implementazione headless ignora la gestione di pagine e componenti come avviene nelle soluzioni full-stack e si concentra sulla creazione dei frammenti di contenuto riutilizzabili e indipendenti dal canale, che possono essere distribuiti in modalità cross-channel. Utilizzando i potenti strumenti di traduzione di AEM, questi frammenti riutilizzabili possono essere facilmente tradotti e consegnati al pubblico ovunque si trovi.

Questa guida affronta i più importanti argomenti relativi alla traduzione headless. Dopo aver concluso il percorso:

* Avrai una panoramica della distribuzione headless dei contenuti.
* Avrai informazioni di base sulle funzioni headless di AEM.
* Comprenderai le funzioni di traduzione di AEM e in che modo si relazionano con il contenuto headless.
* Avrai la possibilità di iniziare a tradurre i tuoi contenuti headless.

L’obiettivo è quello di darti ampie informazioni sulla tecnologia headless, su come funzionano i contenuti headless di AEM e come tradurli. Se non hai familiarità con nessuno di questi argomenti, questo è il posto giusto per iniziare.

Se conosci già AEM, i contenuti headless e la traduzione, potresti avere già le conoscenze di base di questo percorso. In caso affermativo, considera la possibilità di fare riferimento alla nostra documentazione tecnica collegata alla [sezione delle risorse aggiuntive più avanti.](#additional-resources)

## Percorsi di documentazione AEM {#documentation-journeys}

[Un percorso di documentazione](/help/journey-documentation/home.md) unisce molti argomenti e caratteristiche diversi e forse complicati, fornendo un resoconto che aiuta il lettore, che potrebbe essere un nuovo utente di AEM, a capire e risolvere un problema di business dall’inizio alla fine, supponendo una conoscenza minima pregressa dell’argomento o di AEM.

I percorsi di documentazione sono progettati in base ai principi delle best practice, alla luce delle ultime ricerche condotte da Adobe, della comprovata esperienza nell’implementazione da parte di consulenti di Adobe e del feedback raccolto sui progetti della clientela.

Se desideri sapere come Adobe consiglia di risolvere dei casi di business headless con AEM, inizia con i [Percorsi AEM Headless](/help/journey-headless/overview.md).

## Pubblico {#audience}

Questo percorso è progettato per la persona specialista di traduzione, spesso denominata Project Manager di traduzione o TPM. Questo percorso descrive i requisiti, i passaggi e l’approccio per tradurre i contenuti headless in AEM. Il percorso può definire utenti supplementari con cui lo specialista della traduzione deve interagire, ma il punto di vista per il percorso è quello dello specialista della traduzione.

Questo percorso presuppone che il lettore abbia esperienza nella traduzione dei contenuti su un sistema CMS di grandi dimensioni, ma non presuppone alcuna conoscenza della tecnologia headless di AEM.

Di seguito sono riportati gli utenti tipo che interagiscono in questo percorso.

| Persona | Descrizione | Ruolo nel percorso |
|---|---|---|
| Specialista di traduzione | Definisce il contenuto da tradurre e gestisce i flussi di lavoro relativi | Pubblico di questo percorso |
| Autore del contenuto | Crea e gestisce i contenuti consegnati come headless | Gli autori dei contenuti creano i contenuti che devono essere tradotti dallo specialista della traduzione. |
| Amministratore | Gestisce l’impostazione e la configurazione di base di AEM | Lo specialista di traduzione collabora con l’amministratore per apportare le modifiche di configurazione necessarie per la traduzione, ad esempio per l’installazione di un connettore di traduzione. |
| Architetto dei contenuti | Analizza i requisiti dei dati che devono essere distribuiti in modo headless e definisce la struttura per questi dati | Gli esperti di traduzione collaborano con l’architetto dei contenuti per definirne l’organizzazione in modo che possano essere facilmente tradotti. |

Le informazioni in questo percorso possono essere utili a tutti gli utenti, ma alcune possono essere superflue per determinati ruoli. Rimani sintonizzato per [i prossimi percorsi che includeranno ruoli aggiuntivi.](/help/journey-documentation/home.md#journeys)

## Percorso di traduzione headless {#the-journey}

In questo percorso esplorerai molti argomenti. I seguenti articoli forniscono informazioni fondamentali sulla traduzione dei contenuti headless in AEM e si collegano alla documentazione tecnica dettagliata.

Sebbene tu possa accedere direttamente a una sezione specifica del percorso, molti concetti si basano su quelli degli articoli precedenti. Pertanto, se non possiedi nessuna conoscenza della traduzione in AEM, Adobe ti consiglia di di cominciare dalla parte iniziale e di avanzare progressivamente.

| # | Articolo | Descrizione |
|---|---|---|
| 0 | Percorso di traduzione headless di AEM | Questo documento |
| 1 | [Scopri i contenuti headless e come tradurli in AEM](learn-about.md) | Imparare i concetti headless, come si mappano su AEM e la teoria della traduzione in AEM. |
| 2 | [Guida introduttiva alla traduzione headless in AEM](getting-started.md) | Scopri come organizzare i contenuti headless e come funzionano gli strumenti di traduzione di AEM. |
| 3 | [Configurare l’integrazione della traduzione](configure-connector.md) | Scopri come connettere AEM a un servizio di traduzione. |
| 4 | [Configurare le regole di traduzione](translation-rules.md) | Scopri come definire le regole di traduzione per identificare i contenuti per la traduzione. |
| 5 | [Tradurre il contenuto](translate-content.md) | Utilizzare l’integrazione della traduzione e le regole per tradurre il contenuto headless. |
| 6 | [Pubblicare contenuti tradotti](publish-content.md) | Scopri come pubblicare il contenuto tradotto e aggiornare la traduzione quando il contenuto sottostante viene aggiornato. |

## Novità {#what-is-next}

È ora possibile iniziare a utilizzare il percorso di traduzione headless di Adobe. Ti invitiamo a continuare nella parte successiva del percorso e a leggere l’articolo [Scopri i contenuti headless e come tradurli in AEM](learn-about.md)

## Risorse aggiuntive {#additional-resources}

I percorsi di documentazione mostrano come AEM risolve un problema aziendale fornendo una spiegazione che ti guida attraverso processi e funzionalità complessi e interrelati. Un percorso illustra il funzionamento congiunto di più funzioni per soddisfare le esigenze di un’unica azienda.

I percorsi sono progettati per resistere da soli. Tuttavia, diverse di esse possono essere correlate tra loro. Dai un’occhiata ai percorsi aggiuntivi per ulteriori informazioni su come interagiscono le potenti funzioni di AEM.

* [Percorso di authoring headless](/help/journey-headless/author/overview.md): inizia qui un percorso guidato attraverso le potenti e flessibili funzionalità headless di AEM, le potenzialità e i modi in cui modellare i contenuti sul tuo primo progetto headless.
* [Percorso Architect headless](/help/journey-headless/architect/overview.md) - Inizia qui per un’introduzione alle potenti e flessibili funzionalità headless di Adobe Experience Manager e per vedere come modellare i contenuti per il tuo progetto.
* [Percorso per sviluppatori AEM headless](/help/journey-headless/developer/overview.md): inizia qui un percorso guidato per scoprire le potenti e flessibili funzionalità headless di AEM, le loro caratteristiche e come sfruttarle nel tuo primo progetto.
* [Documentazione tecnica AEM](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=it) - Se hai già una solida conoscenza delle tecnologie AEM e headless, potresti voler consultare direttamente i nostri documenti tecnici approfonditi.
   * [Introduzione ad AEM come CMS headless](/help/sites-developing/headless/introduction.md)
* [Tutorial AEM headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=it): se preferisci imparare con la pratica e hai capacità tecniche, segui i nostri tutorial pratici organizzati per API e framework, che esplorano la creazione e l’utilizzo di applicazioni basate su AEM Headless.
* Il [Portale per sviluppatori AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=it)
