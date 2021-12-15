---
title: Facoltativo - Come creare applicazioni a pagina singola (SPA) con AEM
description: In questa continuazione opzionale del Percorso di sviluppatori AEM headless, scopri come AEM combinare la distribuzione headless con le tradizionali funzioni CMS full-stack e come creare SPA modificabili utilizzando AEM framework di editor di contenuti.
exl-id: d74848f2-683e-49e1-9374-32596ca5d7d7
source-git-commit: 7b97bc0ffb0df6641ae71fa36c459f1368052e12
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 0%

---

# Come creare applicazioni a pagina singola (SPA) con AEM {#create-spa}

In questa continuazione facoltativa del [AEM Percorso di sviluppo headless,](overview.md) scopri come AEM combinare la distribuzione headless con le tradizionali funzioni CMS full-stack e come creare SPA modificabili utilizzando AEM framework di editor SPA, nonché integrare SPA esterne per abilitare le funzionalità di modifica.

## La storia finora {#story-so-far}

A questo punto, avresti dovuto completare l&#39;intero [AEM Percorso di sviluppatori headless](overview.md) e comprendere le nozioni di base sulla consegna headless in AEM, compresa la comprensione di:

* Differenza tra distribuzione headless e headful dei contenuti.
* AEM senza testa.
* Come organizzare e AEM il progetto Headless.
* Come creare contenuti headless in AEM.
* Come recuperare e aggiornare il contenuto headless in AEM.
* Come andare a vivere con un progetto senza testa AEM.

Così ora o siete andati a vivere con il vostro primo progetto AEM Headless o avete tutta la conoscenza necessaria per farlo. Congratulazioni!

Allora perché leggete questa ulteriore, facoltativa continuazione del percorso? Probabilmente lo ricorderai nel [Introduzione](getting-started.md#integration-levels) abbiamo discusso brevemente come AEM supporta non solo la consegna headless e i modelli tradizionali full-stack, ma anche i modelli ibridi che combinano i vantaggi di entrambi. Anche se non il modello tradizionale senza testa, questi modelli ibridi possono offrire una flessibilità senza precedenti a determinati progetti.

Questo articolo si basa sulla tua conoscenza di AEM Headless esplorando in dettaglio come creare applicazioni a pagina singola (SPA) che sono effettivamente modificabili in AEM. In questo modo è possibile creare contenuti e distribuirli senza problemi a un SPA, ma SPA modificabili in AEM.

## Obiettivo {#objective}

Questo documento ti aiuta a capire come vengono sviluppate le applicazioni a pagina singola utilizzando il framework dell’editor SPA AEM. Dopo aver letto questo documento è necessario:

* Comprendere la funzione di base dell’Editor SPA.
* Conoscere i requisiti per la costruzione di un SPA completamente modificabile per AEM.
* Scopri come integrare SPA esterni in AEM.
* Comprendere come deve essere implementato o meno il rendering lato server.

## Requisiti e prerequisiti {#requirements-prerequisites}

Ci sono diversi requisiti prima di iniziare a lavorare con SPA in AEM.

### Conoscenza {#knowledge}

* Creare esperienze di sviluppo SPA con i framework React o Angular
* AEM di base per la creazione di frammenti di contenuto e l’utilizzo dell’editor
* Assicurati di rivedere il documento [Cefalea e senza testa in AEM](/help/sites-developing/headful-headless.md) per comprendere i diversi livelli di integrazione SPA possibile.

### Strumenti {#tools}

* Accesso alla sandbox per i test di distribuzione del progetto
* Istanza di sviluppo locale per la modellazione e il test dei dati
* SPA esterna esistente (facoltativo, a seconda del modello di integrazione scelto)
* Archetipo progetto AEM

## Cos&#39;è un SPA? {#what-is-a-spa}

Un’applicazione a pagina singola (SPA) differisce da una pagina convenzionale in quanto viene sottoposta a rendering lato client ed è principalmente guidata da Javascript, basandosi sulle chiamate Ajax per caricare i dati e aggiornare dinamicamente la pagina. La maggior parte o tutto il contenuto viene recuperato una volta in un singolo caricamento di pagina con risorse aggiuntive caricate in modo asincrono in base alle esigenze, in base all’interazione dell’utente con la pagina.

Questo riduce la necessità di aggiornare le pagine e presenta all’utente un’esperienza fluida, rapida e più simile a un’esperienza nativa per le app.

L’editor di SPA AEM consente agli sviluppatori front-end di creare SPA che possono essere integrati in un sito AEM, consentendo agli autori di contenuti di modificare il contenuto SPA con la stessa facilità con cui sono presenti altri contenuti AEM.

## Perché un SPA? {#why-spa}

Essendo più veloce, fluida e più simile a un&#39;applicazione nativa, un SPA diventa un&#39;esperienza molto attraente non solo per il visitatore della pagina web, ma anche per gli esperti di marketing e gli sviluppatori a causa della natura del funzionamento di SPA.

Per una descrizione completa delle SPA e del motivo per cui utilizzarle, consulta la sezione [risorse aggiuntive](#additional-resources) per i collegamenti a una documentazione più dettagliata.

## AEM gestisce SPA

Lo sviluppo di applicazioni a pagina singola in AEM presuppone che lo sviluppatore front-end osservi le best practice standard durante la creazione di un SPA. Se in qualità di sviluppatore front-end segui queste best practice generali e alcuni principi specifici per AEM, il tuo SPA funzionerà con AEM e le sue funzionalità di creazione dei contenuti.

* **Portabilità** - Come per tutti i componenti, i componenti SPA devono essere costruiti in modo da essere il più possibile portatili. La SPA deve essere realizzata con componenti portabili e riutilizzabili.
* **Struttura del sito AEM** - Lo sviluppatore front-end crea componenti e possiede la propria struttura interna, ma si basa su AEM per definire la struttura dei contenuti del sito.
* **Rendering dinamico** - Il rendering deve essere dinamico.
* **Routing dinamico** - Il SPA è responsabile del percorso e AEM lo ascolta e recupera in base ad esso. Anche qualsiasi indirizzamento deve essere dinamico.

Per una descrizione completa delle SPA di AEM, consulta la sezione [risorse aggiuntive](#additional-resources) per i collegamenti a una documentazione più dettagliata.

## Editor SPA AEM {#aem-spa-editor}

I siti costruiti utilizzando framework SPA comuni come React e Angular caricano il contenuto tramite JSON dinamico e non forniscono la struttura di HTML necessaria affinché l’Editor pagina AEM possa inserire controlli di modifica.

Per abilitare la modifica di SPA all’interno di AEM, è necessaria una mappatura tra l’output JSON dell’SPA e il modello di contenuto nell’archivio AEM per salvare le modifiche al contenuto.

SPA supporto in AEM introduce un livello JS sottile che interagisce con il codice JS SPA caricato nell’Editor pagina con cui è possibile inviare eventi e attivare la posizione dei controlli di modifica per consentire la modifica nel contesto. Questa funzione si basa sul concetto di endpoint API di Content Services, in quanto il contenuto del SPA deve essere caricato tramite Content Services.

Per una descrizione completa dell’editor di SPA AEM, consulta la sezione [risorse aggiuntive](#additional-resources) per i collegamenti a una documentazione più dettagliata.

## Alloggio SPA esistenti {#existing-spas}

Se disponi di un SPA esistente, AEM supporta l’incorporazione in AEM in modo che sia visibile agli autori di contenuti nell’editor AEM. Questo può essere molto utile per visualizzare il contenuto che stanno creando tramite Frammenti di contenuto nel contesto dell’applicazione finale in cui verrà utilizzato.

Inoltre, con solo piccole modifiche, puoi abilitare una certa capacità di modifica al SPA esterno all’interno dell’editor di AEM.

Il componente RemotePage consente il rendering di un SPA esterno in AEM.

Per una descrizione completa di come rendere modificabile un SPA esterno in AEM, consulta la sezione [risorse aggiuntive](#additional-resources) per i collegamenti a una documentazione più dettagliata.

## Novità {#what-is-next}

Per iniziare a sviluppare un proprio SPA per AEM, controlla i seguenti documenti:

* [Tutorial WKND SPA](/help/sites-developing/spa-wknd.md)
* [Guida introduttiva a React](/help/sites-developing/spa-getting-started-react.md)
* [Guida introduttiva all&#39;utilizzo di Angular](/help/sites-developing/spa-getting-started-angular.md)

Se devi adattare un SPA esistente per utilizzarlo in AEM, controlla i seguenti documenti:

* [Componente RemotePage](/help/sites-developing/spa-remote-page.md)
* [Modifica di un SPA esterno in AEM](/help/sites-developing/spa-edit-external.md)

Vedi sotto [risorse aggiuntive](#additional-resources) questo può portare a SPA argomenti in AEM.

## Risorse aggiuntive {#additional-resources}

Di seguito sono riportate alcune risorse aggiuntive che approfondiscono alcuni concetti menzionati in questo documento.

* [Cefalea e senza testa in AEM](/help/sites-developing/headful-headless.md) - Descrizione dei diversi modelli di consegna disponibili in AEM
* [Introduzione SPA e Procedura dettagliata.](/help/sites-developing/spa-walkthrough.md) - Una buona introduzione a SPA in AEM
* [Sviluppo di SPA per AEM](/help/sites-developing/spa-architecture.md) - Linee guida su come sviluppare SPA per AEM
* [Panoramica dell’editor di SPA](/help/sites-developing/spa-overview.md) - Dettagli sul funzionamento dell&#39;editor SPA
* [Rendering lato server](/help/sites-developing/spa-ssr.md) - Come configurare SSR per AEM SPA
* [Documenti di riferimento SPA](/help/sites-developing/spa-reference-materials.md) - Riferimenti e collegamenti API JavaScript a progetti open source AEM GitHub
* [Frammenti di contenuto](/help/assets/content-fragments/content-fragments.md) - Come creare frammenti di contenuto
* [Archetipo di progetto AEM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) - Modello Maven che crea un progetto Adobe Experience Manager (AEM) minimale basato su best practice come punto di partenza per il sito web
