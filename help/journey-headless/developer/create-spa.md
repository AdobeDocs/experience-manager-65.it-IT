---
title: Facoltativo - Come creare applicazioni a pagina singola (SPA) con AEM
description: In questa continuazione facoltativa del Percorso per sviluppatori AEM headless, scoprirai come AEM riesce a unire la distribuzione headless con le tradizionali funzioni di un CMS full-stack e come tu puoi creare SPA modificabili utilizzando il framework editor di SPA di AEM.
exl-id: 91eadda2-b881-4e4a-867f-8c5c54e8f8b4
source-git-commit: a2ababa9dd9115e963b91a7271d204d287557c40
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 100%

---

# Come creare applicazioni a pagina singola (SPA) con AEM {#create-spa}

In questa continuazione facoltativa del [Percorso per sviluppatori AEM headless,](overview.md) scoprirai come AEM riesce a unire la distribuzione headless con le tradizionali funzioni di un CMS full-stack e come tu puoi creare SPA modificabili utilizzando il framework editor di SPA di AEM, nonché integrare SPA esterne per abilitare le funzionalità di modifica, quando richiesto.

## Percorso affrontato finora {#story-so-far}

A questo punto, avresti dovuto completare l’intero [Percorso per sviluppatori headless AEM](overview.md) e dovresti aver appreso le nozioni di base sulla distribuzione headless in AEM, oltre ad aver compreso:

* La differenza tra distribuzione headless e headful dei contenuti.
* Le funzionalità headless di AEM.
* Come organizzare un progetto AEM headless.
* Come creare contenuti headless in AEM.
* Come recuperare e aggiornare il contenuto headless in AEM.
* Come pubblicare con un progetto AEM headless.

Così ora o hai già pubblicato il tuo primo progetto AEM Headless o possiedi tutte le conoscenze necessarie per realizzarlo. Congratulazioni. 

Allora perché stai leggendo questa ulteriore continuazione facoltativa del percorso? Probabilmente ricordi che nell’[Introduzione](getting-started.md#integration-levels) abbiamo discusso brevemente di come AEM supporta non solo la distribuzione headless e i modelli tradizionali full-stack, ma anche i modelli ibridi che uniscono i vantaggi di entrambi. Anche se non può farlo il modello tradizionale headless, questi modelli ibridi possono offrire una grandissima flessibilità per determinati progetti.

Questo articolo si basa sulla tua conoscenza di AEM Headless per comprendere meglio come creare applicazioni a pagina singola (SPA) che siano effettivamente modificabili in AEM. In questo modo è possibile creare contenuti e distribuirli in modo headless in una SPA, ma tale SPA è modificabile in AEM.

## Obiettivo {#objective}

Questo documento ti aiuta a capire come vengono sviluppate le applicazioni a pagina singola utilizzando il framework editor di SPA di AEM. Dopo aver letto questo documento dovresti:

* Avere compreso le funzioni di base dell’Editor di SPA.
* Conoscere i requisiti per creare una SPA completamente modificabile per AEM.
* Avere compreso come integrare SPA esterne in AEM.
* Avere compreso come deve essere implementato o meno il rendering lato server.

## Requisiti e prerequisiti {#requirements-prerequisites}

Molti sono i requisiti da soddisfare prima di iniziare a lavorare con le SPA in AEM.

### Conoscenza {#knowledge}

* Esperienza di sviluppo nella creazione di SPA con i framework React o Angular
* Competenze di base in AEM per la creazione di frammenti di contenuto e l’utilizzo dell’editor
* Rivedi il documento [Headful e headless in AEM](/help/sites-developing/headful-headless.md) per comprendere i diversi livelli di integrazione possibili delle SPA.

### Strumenti {#tools}

* Accesso alla sandbox per testare la distribuzione del progetto
* Istanza di sviluppo locale per la modellazione dei dati e il testing
* SPA esterna esistente (facoltativa, a seconda del modello di integrazione scelto)
* Archetipo progetto AEM

## Cos’è una SPA? {#what-is-a-spa}

Un’applicazione a pagina singola (SPA) è diversa da una pagina convenzionale in quanto viene sottoposta a rendering lato client ed è principalmente basata su Javascript, utilizza le chiamate Ajax per caricare i dati e aggiornare dinamicamente la pagina. La maggior parte o tutto il contenuto viene recuperato una volta nel caricamento di una singola pagina con risorse aggiuntive caricate in modo asincrono in base alle esigenze, a seconda dell’interazione dell’utente con la pagina.

Questo riduce la necessità di aggiornare le pagine e offre all’utente un’esperienza caratterizzata da fluidità e rapidità, che si rivela più simile all’esperienza assicurata da un’app nativa.

L’editor AEM di SPA consente agli sviluppatori front-end di creare SPA che possono essere integrate in un sito AEM, permettendo agli autori dei contenuti di modificare il contenuto delle SPA con la stessa facilità con cui sono modificati altri contenuti AEM.

## Perché una SPA? {#why-spa}

Essendo più veloce, fluida e più simile a un’applicazione nativa, una SPA diventa un’esperienza molto piacevole non solo per il visitatore della pagina web, ma anche per gli esperti di marketing e gli sviluppatori grazie al tipo di funzionamento delle SPA.

Per una descrizione completa delle SPA e del motivo per cui utilizzarle, consulta la sezione [risorse aggiuntive](#additional-resources): troverai i collegamenti a una documentazione più dettagliata.

## Come AEM gestisce le SPA

Lo sviluppo di applicazioni a pagina singola in AEM presuppone che lo sviluppatore front-end osservi le best practice standard durante la creazione di una SPA. Se in qualità di sviluppatore front-end segui queste best practice generali e alcuni principi specifici per AEM, la tua SPA funzionerà con AEM e con le sue funzionalità di creazione dei contenuti.

* **Portabilità** - Come per qualunque componente, i componenti SPA devono essere costruiti in modo da essere il più possibile portatili. La SPA deve essere realizzata con componenti portabili e riutilizzabili.
* **AEM definisce la struttura del sito** - Lo sviluppatore front-end crea componenti e possiede la loro struttura interna, ma si basa su AEM per definire la struttura dei contenuti del sito.
* **Rendering dinamico** - Tutto il rendering deve essere dinamico.
* **Routing dinamico** - La SPA è responsabile del routing e AEM lo ascolta ed esegue il recupero in base ad esso. Anche altri routing devono essere dinamici.

Per una descrizione completa di come AEM gestisce le SPA, consulta la sezione [risorse aggiuntive](#additional-resources) per i collegamenti a una documentazione più dettagliata.

## Editor SPA di AEM  {#aem-spa-editor}

I siti costruiti utilizzando framework SPA comuni come React e Angular caricano il contenuto tramite JSON dinamico e non forniscono la struttura di HTML necessaria affinché l’editor pagina di AEM possa inserire controlli di modifica.

Per abilitare la modifica delle SPA all’interno di AEM, è necessaria una mappatura tra l’output JSON della SPA e il modello di contenuto nell’archivio AEM per salvare le modifiche al contenuto.

Il supporto SPA in AEM introduce un livello JS sottile che interagisce con il codice JS SPA caricato nell’Editor pagina con cui è possibile inviare eventi e attivare la posizione dei controlli di modifica per consentire la modifica nel contesto. Questa funzione si basa sul concetto di endpoint API di Content Services, in quanto il contenuto dell’SPA deve essere caricato tramite Content Services.

Per una descrizione completa dell’editor di SPA AEM, consulta la sezione [risorse aggiuntive](#additional-resources) per i collegamenti a una documentazione più dettagliata.

## Alloggio SPA esistenti {#existing-spas}

Se disponi di un SPA esistente, AEM supporta l’incorporazione in AEM, in modo che sia visibile agli autori di contenuti nell’Editor AEM. Questo può essere molto utile per visualizzare il contenuto che si sta creando tramite Frammenti di contenuto nel contesto dell’applicazione finale in cui verrà utilizzato.

Inoltre, con solo piccole modifiche, si può abilitare una certa capacità di modifica all’SPA esterno all’interno dell’Editor AEM.

Il componente RemotePage consente il rendering di un SPA esterno in AEM.

Per una descrizione completa di come rendere modificabile un SPA esterno in AEM, consulta la sezione [risorse aggiuntive](#additional-resources) per i collegamenti a una documentazione più dettagliata.

## Passaggio successivo {#what-is-next}

Per iniziare a sviluppare un proprio SPA per AEM, controlla i seguenti documenti:

* [Tutorial WKND per SPA](/help/sites-developing/spa-wknd.md)
* [Guida introduttiva all’utilizzo di React](/help/sites-developing/spa-getting-started-react.md)
* [Guida introduttiva all’utilizzo di Angular](/help/sites-developing/spa-getting-started-angular.md)

Se devi adattare un SPA esistente per utilizzarlo in AEM, controlla i seguenti documenti:

* [Componente RemotePage](/help/sites-developing/spa-remote-page.md)
* [Modifica di uno SPA esterno in AEM](/help/sites-developing/spa-edit-external.md)

Vedi sotto le [risorse aggiuntive](#additional-resources) che possono farti approfondire argomenti SPA in AEM.

## Risorse aggiuntive {#additional-resources}

Di seguito sono riportate alcune risorse aggiuntive che approfondiscono alcuni concetti menzionati in questo documento.

* [Headful e headless in AEM](/help/sites-developing/headful-headless.md): descrizione dei diversi modelli di distribuzione disponibili in AEM
* [Introduzione a SPA e procedura dettagliata.](/help/sites-developing/spa-walkthrough.md) - Una buona introduzione a SPA in AEM
* [Sviluppo di SPA per AEM](/help/sites-developing/spa-architecture.md): linee guida su come sviluppare SPA per AEM
* [Panoramica dell’editor di SPA](/help/sites-developing/spa-overview.md): dettagli sul funzionamento dell&#39;editor SPA
* [Rendering lato server](/help/sites-developing/spa-ssr.md): come configurare SSR per SPA AEM
* [Documenti di riferimento SPA](/help/sites-developing/spa-reference-materials.md): riferimenti e collegamenti API JavaScript a progetti open source GitHub SPA AEM
* [Frammenti di contenuto](/help/assets/content-fragments/content-fragments.md): come creare frammenti di contenuto
* [L’Archetipo di progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=it) è un modello Maven che crea un progetto AEM minimo basato sulle best practice di Adobe Experience Manager (AEM) come punto di partenza per il tuo sito web
