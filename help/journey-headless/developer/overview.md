---
title: Percorso per sviluppatori headless di AEM
description: Documentazione di CMS headless AEM. Inizia qui per un percorso guidato attraverso le potenti e flessibili funzionalità headless dell’AEM, le loro caratteristiche e come sfruttarle nei tuoi progetti.
exl-id: f24fb308-daa7-426f-ba45-37a236b5a500
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1212'
ht-degree: 77%

---

# Percorso per sviluppatori headless di AEM {#aem-headless-developer-journey}

Inizia qui per un percorso guidato attraverso le potenti e flessibili funzionalità headless dell’AEM, le loro caratteristiche e come sfruttarle per il tuo primo progetto di sviluppo headless. Questo percorso fornisce tutta la documentazione headless AEM necessaria per sviluppare la prima applicazione headless.

## Introduzione {#introduction}

L’implementazione headless ignora la gestione di pagine e componenti come avviene nelle soluzioni full-stack e si concentra sulla creazione dei frammenti di contenuto riutilizzabili e indipendenti dal canale, che possono essere distribuiti in modalità cross-channel. Si tratta di un modello di sviluppo dinamico e moderno per implementare esperienze digitali.

Questa guida illustra gli argomenti più importanti sull’implementazione headless in AEM, in modo che al termine dell’operazione:

* Comprenderai appieno cosa è la distribuzione di contenuti headless e i relativi vantaggi.
* Scoprirai le funzioni headless di AEM e come funzionano insieme per offrire un’esperienza headless.
* Avrai la possibilità di compiere i primi passi per implementare il primo progetto headless di AEM.

## Percorsi di documentazione AEM {#documentation-journeys}

[Un percorso di documentazione](/help/journey-documentation/home.md) unisce molti argomenti e caratteristiche diversi e forse complicati, fornendo un resoconto che aiuta il lettore, che potrebbe essere un nuovo utente di AEM, a capire e risolvere un problema di business dall’inizio alla fine, supponendo una conoscenza minima pregressa dell’argomento o di AEM.

I percorsi di documentazione sono progettati in base ai principi delle best practice, alla luce delle ultime ricerche condotte da Adobe, della comprovata esperienza nell’implementazione da parte di consulenti di Adobe e del feedback raccolto sui progetti dei clienti.

Se desideri sapere come Adobe consiglia di risolvere dei casi di business headless con AEM, inizia con i [Percorsi AEM Headless](/help/journey-headless/home.md).

>[!TIP]
>
>Se preferisci **imparare facendo** e sono tecnicamente inclini, visita i tutorial headless dell’AEM, organizzati per API e framework e disponibili nel [Sezione Risorse aggiuntive](#additional-resources) alla fine del presente documento.

## Pubblico {#audience}

Questo percorso è progettato per l’utente tipo sviluppatore, esponendo i requisiti, i passaggi e l’approccio di un progetto AEM Headless dal punto di vista dello sviluppatore. Il percorso definisce gli utenti tipo aggiuntivi con cui lo sviluppatore deve interagire per un progetto di successo, ma il punto di vista del percorso è quello dello sviluppatore.

Di seguito sono riportati gli utenti tipo che interagiscono in questo percorso.

| Persona | Descrizione | Mansione in questo percorso |
|---|---|---|
| Sviluppatore (pubblico target) | Ha esperienza nello sviluppo di applicazioni headless che utilizzano contenuti provenienti da diverse fonti | Pubblico target di questo percorso |
| Autore del contenuto | Crea e gestisce contenuti che vengono distribuiti in modo headless | Gli autori dei contenuti creano contenuti che lo sviluppatore distribuisce in modo headless. |
| Amministratore | Gestisce l’impostazione e la configurazione di base di AEM | Lo sviluppatore collabora con l’amministratore per apportare le modifiche di configurazione necessarie per lo sviluppo. |
| Architetto dei contenuti | Analizza i requisiti dei dati che devono essere distribuiti in modo headless e definisce la struttura per questi dati | Gli sviluppatori lavorano con l’architect dei contenuti per comprendere la struttura dei dati e i requisiti necessari per distribuirli in modo headless. |

Le informazioni in questo percorso possono ovviamente essere utili a tutti gli utenti, ma alcune possono essere superflue per determinati ruoli. Rimani sintonizzato per [i prossimi percorsi che includeranno ruoli aggiuntivi.](/help/journey-documentation/home.md#journeys)

## Percorso per sviluppatori headless {#the-journey}

In questo percorso esplorerai molti argomenti. La lettura degli articoli seguenti fornirà le conoscenze di base sui contenuti headless in AEM e il collegamento all’approfondita documentazione tecnica.

Sebbene tu possa accedere direttamente a una sezione specifica del percorso, molti concetti si basano su quelli degli articoli precedenti. Pertanto, se sei un nuovo utente di headless in AEM, Adobe consiglia di iniziare dall’inizio e procedere in sequenza.

| # | Articolo | Descrizione |
|---|---|---|
| 0 | Percorso per sviluppatori headless di AEM | Questo documento |
| 1 | [Informazioni sullo sviluppo headless di CMS](learn-about.md) | Scopri la tecnologia headless e quando usarla. |
| 2 | [Guida introduttiva ad AEM Headless](getting-started.md) | Scopri i prerequisiti headless di AEM |
| 3 | [Percorso della tua prima esperienza con AEM Headless](path-to-first-experience.md) | Imposta l’ambiente di sviluppo e scopri come integrare un’app semplice con AEM Headless |
| 4 | [Come modellare il contenuto](model-your-content.md) | Scopri come modellare la struttura del contenuto. Quindi realizza quella struttura per Adobe Experience Manager (AEM) utilizzando Modelli per frammenti di contenuto e Frammenti di contenuto, da riutilizzare tra i canali. |
| 5 | [Come accedere al contenuto tramite API di consegna AEM](access-your-content.md) | Scopri come utilizzare le query GraphQL per accedere al contenuto dei frammenti di contenuto. |
| 6 | [Come aggiornare il contenuto tramite API di AEM Assets](update-your-content.md) | Scopri come utilizzare l’API REST per accedere e aggiornare il contenuto dei frammenti di contenuto. |
| 7 | [Come raggruppare la tua app e i tuoi contenuti in AEM Headless](put-it-all-together.md) | Scopri come prendere il progetto AEM e prepararlo per pubblicare con l’SDK headless di AEM. |
| 8 | [Come effettuare il Go Live con la tua applicazione headless](go-live.md) | Scopri come distribuire l’applicazione in tempo reale, inserire il codice locale in Git e spostarlo in Cloud Manager Git per la pipeline CI/CD. |
| 9 | [Facoltativo - Come creare applicazioni a pagina singola (SPA) con AEM](create-spa.md) | Una volta comprese le funzioni headless dell’AEM, scopri come combinare la distribuzione headful e headless e come creare SPA modificabile utilizzando il framework dell’Editor SPA dell’AEM. |

## Passaggio successivo {#what-is-next}

Ora sei pronto per iniziare il tuo percorso in Adobe headless. Ti invitiamo a continuare con la prossima parte del percorso e leggere l&#39;articolo [Scopri lo sviluppo headless di CMS.](learn-about.md)

### Scegli la tua avventura {#choose-your-path}

Tuttavia, Adobe vuole che tu abbia successo mentre inizi con il tuo progetto headless AEM, indipendentemente dal tuo stile di apprendimento. Quindi, per favore, prendete in considerazione queste due opzioni.

* Se preferisci continuare su **scopri i concetti headless e le tecnologie headless di AEM**, dovresti continuare il tuo percorso AEM headless come consigliato nella prossima revisione del documento [Come modellare il contenuto come modelli di contenuto AEM](model-your-content.md) dove viene illustrato come modellare la struttura del contenuto in AEM.
* Se preferisci **imparare facendo**, puoi passare alla [Guida introduttiva ai tutorial pratici headless di AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=it) dove puoi passare direttamente allo sviluppo headless di AEM implementando un semplice progetto per esporre il contenuto headless di AEM.

## Risorse aggiuntive {#additional-resources}

I percorsi di documentazione mostrano come AEM risolve un problema aziendale fornendo una spiegazione che ti guida attraverso processi e funzionalità complessi e interrelati. Un percorso illustra il funzionamento congiunto di più funzioni per soddisfare le esigenze di un’unica azienda.

Poiché tali percorsi sono progettati per essere indipendenti l’uno dall’altro. Tuttavia alcuni di essi possono essere correlati tra loro. Dai un’occhiata ai percorsi aggiuntivi per ulteriori informazioni su come interagiscono le potenti funzioni di AEM.

* [Tutorial AEM headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=it): se preferisci imparare facendo e hai capacità tecniche, segui i nostri tutorial pratici organizzati per API e framework, che esplorano la creazione e l’utilizzo di applicazioni create su AEM Headless.
* [Percorso di traduzione headless AEM](/help/journey-headless/translation/overview.md) - questo percorso di documentazione ti offre un’ampia comprensione della tecnologia headless, di come AEM si serve di contenuti headless e di come tradurli.
* [Percorso di authoring headless](/help/journey-headless/author/overview.md): inizia qui un percorso guidato attraverso le potenti e flessibili funzionalità headless di AEM, le potenzialità e i modi in cui modellare i contenuti sul tuo primo progetto headless.
* [Percorso Architect headless](/help/journey-headless/architect/overview.md) - Inizia qui per un’introduzione alle potenti e flessibili funzionalità headless di Adobe Experience Manager e per vedere come modellare i contenuti per il tuo progetto.
* [Documentazione tecnica AEM ](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=it): se hai già una solida conoscenza delle tecnologie AEM e headless, potresti voler consultare direttamente i nostri documenti tecnici approfonditi.
