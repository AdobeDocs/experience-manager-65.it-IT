---
title: AEM Percorso di sviluppatori headless
description: Documentazione AEM CMS headless. Inizia qui per un percorso guidato attraverso le potenti e flessibili funzionalità di AEM, le loro capacità e come sfruttarle per il tuo primo progetto di sviluppo.
source-git-commit: 0458a811b5bd062abbe8a42ec141bc786491e19e
workflow-type: tm+mt
source-wordcount: '1179'
ht-degree: 2%

---

# AEM Percorso di sviluppatori headless {#aem-headless-developer-journey}

Inizia qui per un percorso guidato attraverso le potenti e flessibili funzionalità di AEM, le loro capacità e come sfruttarle sul tuo primo progetto di sviluppo headless. Questo percorso offre tutta la documentazione headless AEM necessaria per sviluppare la tua prima applicazione headless.

## Introduzione {#introduction}

L’implementazione headless dimentica la gestione delle pagine e dei componenti come avviene nelle soluzioni stack complete e si concentra sulla creazione di frammenti di contenuto riutilizzabili e neutri per i canali e sulla loro distribuzione cross-channel. Si tratta di un modello di sviluppo moderno e dinamico per l&#39;implementazione delle esperienze digitali.

Questa guida ti guida attraverso gli argomenti di implementazione più headless in AEM, in modo che al momento del completamento:

* Comprendi appieno cosa è la distribuzione di contenuti headless e i relativi vantaggi.
* Scopri AEM funzioni headless e come funzionano insieme per offrire un’esperienza headless.
* Avere la possibilità di compiere i primi passi per implementare il primo progetto senza testa AEM.

## percorsi di documentazione AEM {#documentation-journeys}

[Un Percorso di documentazione](/help/journey-documentation/home.md) unisce molti argomenti e caratteristiche diversi e forse complicati fornendo una narrazione che aiuta il lettore, che può essere nuovo a AEM, capire e risolvere un problema di business dall&#39;inizio alla fine, assumendo al contempo un argomento preliminare minimo o AEM conoscenza.

I Percorsi di documentazione sono progettati in base ai principi delle best practice, alla luce delle ultime ricerche condotte da Adobe, della comprovata esperienza nell’implementazione da parte di consulenti di Adobe e del feedback dai progetti dei clienti.

Se desideri sapere come Adobe consiglia di risolvere i casi aziendali headless con AEM, [AEM Percorsi headless](/help/journey-headless/home.md) sono dove iniziare.

>[!TIP]
>
> Se preferisci **imparare facendo** e sono tecnicamente inclinati, visita i tutorial AEM Headless, organizzati per API e framework e disponibili in [Sezione Risorse aggiuntive](#additional-resources) alla fine del presente documento.

## Pubblico {#audience}

Questo percorso è progettato per l’utente tipo sviluppatore, esponendo i requisiti, i passaggi e l’approccio di un progetto AEM Headless dal punto di vista dello sviluppatore. Il percorso definisce gli utenti tipo aggiuntivi con cui lo sviluppatore deve interagire per un progetto di successo, ma il punto di vista del percorso è quello dello sviluppatore.

Di seguito sono riportati gli utenti tipo che interagiscono in questo percorso.

| Persona | Descrizione | Ruolo in questo Percorso |
|---|---|---|
| Sviluppatore (pubblico target) | Ha esperienza nello sviluppo di applicazioni headless che utilizzano contenuti provenienti da diverse fonti | Pubblico di destinazione di questo percorso |
| Autore del contenuto | Crea e gestisce contenuti distribuiti senza problemi | Gli autori dei contenuti creano contenuti che lo sviluppatore offre senza problemi. |
| Administrator | Gestisce la configurazione e la configurazione di base di AEM | Lo sviluppatore collabora con l’amministratore per apportare le modifiche di configurazione necessarie per lo sviluppo. |
| Architetto dei contenuti | Analizza i requisiti dei dati che devono essere consegnati senza problemi e definisce la struttura di tali dati | Gli sviluppatori lavorano con l’architetto dei contenuti per comprendere la struttura dei dati e i requisiti necessari per distribuirli senza problemi. |

Le informazioni in questo percorso possono ovviamente essere utili a tutti gli utenti, ma alcune informazioni possono essere superflue a determinati ruoli. Rimani sintonizzato per [percorsi successivi che includeranno ruoli aggiuntivi.](/help/journey-documentation/home.md#journeys)

## Percorso di sviluppatori headless {#the-journey}

Esplorerai molti argomenti in questo percorso. I seguenti articoli ti offrono conoscenze fondamentali sui headless in AEM e ti collegano alla documentazione tecnica dettagliata.

Anche se puoi passare direttamente a una particolare parte del percorso, molti concetti si basano su quelli degli articoli precedenti. Pertanto, se sei nuovo a headless in AEM, ti consigliamo di iniziare dall’inizio e procedere in sequenza.

| # | Articolo | Descrizione |
|---|---|---|
| 0 | AEM Percorso di sviluppatori headless | Questo documento |
| 1 | [Scopri lo sviluppo headless di CMS](learn-about.md) | Scopri la tecnologia headless e quando usarla. |
| 2 | [Guida introduttiva ad AEM Headless](getting-started.md) | Scopri AEM prerequisiti headless |
| 3 | [Percorso della tua prima esperienza con AEM Headless](path-to-first-experience.md) | Imposta l’ambiente di sviluppo e scopri come integrare un’app semplice con AEM Headless |
| 4 | [Come modellare il contenuto](model-your-content.md) | Scopri come modellare la struttura del contenuto. Quindi realizza quella struttura per Adobe Experience Manager (AEM) utilizzando Modelli per frammenti di contenuto e Frammenti di contenuto, da riutilizzare tra i canali. |
| 5 | [Come accedere ai contenuti tramite API di consegna AEM](access-your-content.md) | Scopri come utilizzare le query GraphQL per accedere al contenuto dei frammenti di contenuto. |
| 6 | [Come aggiornare i contenuti tramite API di AEM Assets](update-your-content.md) | Scopri come utilizzare l’API REST per accedere e aggiornare il contenuto dei frammenti di contenuto. |
| 7 | [Come mettere tutto insieme - la tua app e il tuo contenuto in AEM Headless](put-it-all-together.md) | Scopri come prendere il progetto AEM e prepararlo per diventare live con l’SDK senza titolo AEM. |
| 8 | [Facoltativo - Come creare applicazioni a pagina singola (SPA) con AEM](create-spa.md) | Una volta comprese AEM funzionalità headless, scopri come combinare consegne headful e headless e come creare SPA modificabili utilizzando AEM framework di Editor. |

<!-- HM-Links
|8|[How to go live with your headless application](go-live.md)|Learn how to deploy application live and take your local code in Git and move it to Cloud Manager Git for CI/CD pipeline.|
|9|[Optional - How to create single page applications (SPAs) with AEM](create-spa.md)|Once you understand AEM's headless features, explore how to combine headful and headless delivery and learn how you can create editable SPAs using AEM's SPA Editor framework.|
-->

## Novità {#what-is-next}

Ora sei pronto per iniziare sul tuo percorso headless Adobe. Ti invitiamo a continuare nella parte successiva del percorso e a leggere l&#39;articolo [Scopri lo sviluppo headless di CMS.](learn-about.md)

### Scegli la tua avventura {#choose-your-path}

Tuttavia, Adobe vuole che tu abbia successo quando inizi a lavorare con il tuo progetto AEM Headless, indipendentemente dal tuo stile di apprendimento. Considerate quindi queste due opzioni.

* Se preferisci continuare a **scopri i concetti senza testa e le tecnologie senza testa AEM**, dovresti continuare il tuo percorso AEM headless come consigliato nella prossima revisione del documento [Come modellare il contenuto come modelli di contenuto AEM](model-your-content.md) dove viene illustrato come modellare la struttura del contenuto in AEM.
* Se preferisci **imparare facendo**, puoi passare alla [Guida introduttiva a AEM tutorial pratico headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) dove puoi passare direttamente AEM sviluppo Headless implementando un semplice progetto per esporre AEM contenuto headless.

## Risorse aggiuntive {#additional-resources}

I percorsi di documentazione mostrano come AEM risolvere un problema aziendale fornendo una narrazione che ti guida attraverso processi e funzionalità complessi e intercorrelati. Un percorso illustra il funzionamento congiunto di più funzioni per soddisfare le esigenze di un&#39;unica azienda.

Come tali percorsi sono progettati per stare da soli. Tuttavia alcuni di essi possono essere correlati tra loro. Consulta questi percorsi aggiuntivi per ulteriori informazioni su come AEM funzioni avanzate funzionano insieme.

* [Esercitazioni AEM headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html) - Se preferisci imparare facendo e sei tecnicamente inclinato, segui i nostri tutorial pratici organizzati da API e framework, che esplorano la creazione e l&#39;utilizzo di applicazioni create su AEM Headless.
* [AEM Percorso di traduzione headless](/help/journey-headless/translation/overview.md) - Questo percorso di documentazione ti offre un’ampia comprensione della tecnologia headless, di come AEM i contenuti headless e di come tradurli.
* [Percorso di authoring headless](/help/journey-headless/author/overview.md) - Inizia qui per un percorso guidato attraverso le potenti e flessibili funzionalità di AEM, le loro capacità e come modellare i contenuti sul tuo primo progetto headless.
* [Percorso architetto headless](/help/journey-headless/architect/overview.md) - Inizia qui per un’introduzione alle funzioni potenti, flessibili e headless di Adobe Experience Manager e a come modellare i contenuti per il tuo progetto.
* [Documentazione tecnica AEM](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=it) - Se hai già una comprensione ferma delle tecnologie AEM e headless, potresti voler consultare direttamente i nostri documenti tecnici approfonditi.
