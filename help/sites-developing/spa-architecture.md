---
title: Sviluppo di SPA per AEM
seo-title: Sviluppo di SPA per AEM
description: Questo articolo presenta domande importanti da considerare quando uno sviluppatore front-end si impegna a sviluppare un SPA per AEM e fornisce una panoramica dell'architettura di AEM rispetto a SPA da tenere presente quando si distribuisce un SPA sviluppato su AEM.
seo-description: Questo articolo presenta domande importanti da considerare quando uno sviluppatore front-end si impegna a sviluppare un SPA per AEM e fornisce una panoramica dell'architettura di AEM rispetto a SPA da tenere presente quando si distribuisce un SPA sviluppato su AEM.
uuid: 6673a041-c557-4968-ae54-4cd5b9f56251
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9584392a-d8a3-45a4-9cdf-fd211c8e6091
docset: aem65
translation-type: tm+mt
source-git-commit: 590dc4464182d4baf8293e7bb0774ce92971c0af
workflow-type: tm+mt
source-wordcount: '2122'
ht-degree: 0%

---


# Sviluppo SPA per AEM{#developing-spas-for-aem}

Le applicazioni a pagina singola (SPA) possono offrire esperienze coinvolgenti agli utenti di siti Web. Gli sviluppatori desiderano essere in grado di creare siti utilizzando SPA framework e gli autori desiderano modificare i contenuti all&#39;interno di AEM per un sito creato utilizzando tali framework.

Questo articolo presenta domande importanti da considerare quando uno sviluppatore front-end si impegna a sviluppare un SPA per AEM e fornisce una panoramica dell&#39;architettura di AEM per quanto riguarda la distribuzione SPA su AEM.

>[!NOTE]
>
>SPA Editor è la soluzione consigliata per i progetti che richiedono SPA rendering lato client basato su framework (ad es. React o Angular).

## Principi di sviluppo SPA per AEM {#spa-development-principles-for-aem}

Lo sviluppo di applicazioni a pagina singola in AEM presuppone che lo sviluppatore front-end rispetti le best practice standard per la creazione di un SPA. Se uno sviluppatore front-end segue queste best practice generali e alcuni principi AEM specifici, il SPA funzionerà con [AEM e le relative funzionalità di authoring dei contenuti](/help/sites-developing/spa-walkthrough.md#content-editing-experience-with-spa).

* **[Portabilità](/help/sites-developing/spa-architecture.md#portability) -** Come con qualsiasi componente, i componenti devono essere costruiti per essere il più possibile portatili. Il SPA deve essere realizzato con componenti portabili e riutilizzabili.
* **[AEM struttura](/help/sites-developing/spa-architecture.md#aem-drives-site-structure)**  del sito: lo sviluppatore front-end crea componenti e possiede la propria struttura interna, ma si basa su AEM per definire la struttura del contenuto del sito.
* **[Rendering](/help/sites-developing/spa-architecture.md#dynamic-rendering)**  dinamico: tutto il rendering deve essere dinamico.
* **[Routing](#dynamic-routing)  dinamico -** Il SPA è responsabile del routing e AEM lo ascolta e recupera in base ad esso. Anche l&#39;indirizzamento deve essere dinamico.

Se tenete in mente questi principi mentre sviluppate il SPA, sarà quanto più flessibile e affidabile possibile, consentendo al contempo tutte le funzionalità di authoring AEM supportate.

Se non è necessario supportare AEM funzioni di authoring, potrebbe essere necessario considerare un modello di progettazione [SPA diverso](/help/sites-developing/spa-architecture.md#spa-design-models).

### Portabilità {#portability}

Come per lo sviluppo di qualsiasi componente, i componenti devono essere progettati in modo da massimizzarne la portabilità. Eventuali schemi che contrastino con la portabilità o riutilizzabilità dei componenti dovrebbero essere evitati per garantire compatibilità, flessibilità e manutenibilità in futuro.

Le SPA risultanti devono essere realizzate con componenti altamente portatili e riutilizzabili.

### AEM struttura del sito {#aem-drives-site-structure}

Lo sviluppatore front-end deve considerare se stesso come responsabile della creazione di una libreria di componenti SPA utilizzati per creare l&#39;app. Lo sviluppatore front-end ha il controllo completo della struttura interna dei componenti. [Tuttavia AEM possiede sempre la struttura del sito.](/help/sites-developing/spa-overview.md)

Questo significa che lo sviluppatore front-end può aggiungere il contenuto del cliente prima o dopo il punto di ingresso dei componenti e può anche effettuare chiamate di terze parti all’interno del componente. Tuttavia, lo sviluppatore front-end non ha il controllo completo del modo in cui i componenti vengono nidificati, ad esempio.

### Rendering dinamico {#dynamic-rendering}

Il SPA dovrebbe basarsi solo sul rendering dinamico del contenuto. Questa è l&#39;aspettativa predefinita in cui AEM recupera e visualizza tutti gli elementi secondari della struttura del contenuto. [](/help/sites-developing/spa-architecture.md#portability)

Qualsiasi rendering esplicito che punti a contenuto specifico viene considerato come rendering statico e, anche se supportato, non sarà compatibile con AEM funzioni di authoring dei contenuti. Ciò va anche contro il principio di [portabilità](/help/sites-developing/spa-architecture.md#portability).

### Routing dinamico {#dynamic-routing}

Come per il rendering, anche tutti i routing devono essere dinamici. In AEM, [il SPA deve sempre essere proprietario del routing](/help/sites-developing/spa-routing.md) e AEM ascoltare e recuperare il contenuto in base ad esso.

Qualsiasi routing statico funziona in base al principio [di portabilità](/help/sites-developing/spa-architecture.md#portability) e limita l&#39;autore in quanto non è compatibile con le funzioni di authoring dei contenuti di AEM. Ad esempio, con l&#39;indirizzamento statico, se l&#39;autore del contenuto desidera modificare una route o una pagina, deve chiedere allo sviluppatore front-end di farlo.

## AEM Project Archetype {#aem-project-archetype}

Qualsiasi progetto AEM deve sfruttare il [AEM Project Archetype](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/developing/archetype/overview.html), che supporta SPA progetti utilizzando React o Angular e sfrutta l&#39;SDK SPA.

## Modelli di progettazione SPA {#spa-design-models}

Se vengono seguiti i principi di sviluppo di SPA in AEM[, il SPA funzionerà con tutte le funzioni AEM di authoring dei contenuti supportate. ](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)[](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)

Ci possono essere tuttavia dei casi in cui ciò non è del tutto necessario. La tabella seguente fornisce una panoramica dei vari modelli di progettazione, dei relativi vantaggi e dei relativi svantaggi.

<table>
 <tbody>
  <tr>
   <th><strong>Modello di progettazione<br /> </strong></th>
   <th><strong>Vantaggi</strong></th>
   <th><strong>Svantaggi</strong></th>
  </tr>
  <tr>
   <td>AEM viene utilizzato come CMS headless senza utilizzare il framework SDK dell'editor <a href="/help/sites-developing/spa-reference-materials.md">SPA.</a></td>
   <td>Lo sviluppatore front-end ha il controllo completo sull'app.</td>
   <td><p>Gli autori dei contenuti non possono sfruttare AEM'esperienza di authoring dei contenuti.</p> <p>Il codice non è né portatile né riutilizzabile se contiene riferimenti statici o routing.</p> <p>Non consente l'utilizzo dell'editor modelli, pertanto lo sviluppatore front-end deve mantenere i modelli modificabili tramite JCR.</p> </td>
  </tr>
  <tr>
   <td>Lo sviluppatore front-end utilizza il framework SDK dell’editor SPA, ma apre solo alcune aree all’autore del contenuto.</td>
   <td>Lo sviluppatore mantiene il controllo sull'app abilitando solo l'authoring nelle aree limitate dell'app.</td>
   <td><p>Gli autori dei contenuti sono limitati a una serie limitata di esperienze di authoring AEM contenuto.</p> <p>Il codice non può essere portatile né riutilizzabile se contiene riferimenti statici o routing.</p> <p>Non consente l'utilizzo dell'editor modelli, pertanto lo sviluppatore front-end deve mantenere i modelli modificabili tramite JCR.</p> </td>
  </tr>
  <tr>
   <td>Il progetto sfrutta appieno l’SDK dell’editor SPA e i componenti frontend sono sviluppati come libreria e la struttura del contenuto dell’app è delegata a AEM.</td>
   <td><p>L'app è riutilizzabile e portatile.</p> <p>L'autore del contenuto può modificare l'app utilizzando AEM'esperienza di creazione del contenuto.<br /> </p> <p>Il SPA è compatibile con l’editor modelli.</p> </td>
   <td><p>Lo sviluppatore non ha il controllo della struttura dell'app e della parte di contenuto delegata a AEM.</p> <p>Lo sviluppatore può comunque riservare aree dell'app per il contenuto che non deve essere creato utilizzando AEM.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Anche se tutti i modelli sono supportati in AEM, solo implementando il terzo (e quindi seguendo i principi di sviluppo [SPA consigliati in AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)) gli autori dei contenuti potranno interagire con e modificare il contenuto del SPA in AEM come sono abituati.
>[](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)

## Migrazione SPA esistente a AEM {#migrating-existing-spas-to-aem}

In genere, se il tuo SPA segue i [SPA Principi di sviluppo per AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem), il tuo SPA funzionerà in AEM e sarà modificabile utilizzando l&#39;SPA Editor.

Seguite questi passaggi per rendere il vostro SPA esistente pronto per lavorare con AEM.

1. **I componenti JS sono modulari.**

   Renderli in grado di essere sottoposti a rendering in qualsiasi ordine, posizione e dimensione.
1. **Utilizza i contenitori forniti dal nostro SDK per inserire i componenti sullo schermo.**

   AEM fornisce un componente per il sistema di paragrafi e pagine da usare.
1. **Create un componente AEM per ciascun componente JS.**

   I componenti AEM definiscono la finestra di dialogo e l’output JSON.

## Istruzioni per gli sviluppatori front-end {#instructions-for-front-end-developers}

Il compito principale nell&#39;affidare a uno sviluppatore front-end la creazione di un SPA per AEM è quello di concordare i componenti e i relativi modelli JSON.

Di seguito è riportato un profilo dei passi che uno sviluppatore front-end deve seguire nello sviluppo di un SPA per AEM.

1. **Concordare sui componenti e il relativo modello JSON**

   Gli sviluppatori front-end e gli sviluppatori di back-end AEM devono concordare su quali componenti sono necessari e un modello, per cui esiste una corrispondenza uno-a-uno tra SPA componenti e i componenti back-end.

   AEM componenti sono ancora necessari principalmente per fornire finestre di dialogo di modifica ed esportare il modello di componente.

1. **In React components, accedere al modello tramite`this.props.cqModel`**

   Una volta che i componenti sono concordati e il modello JSON è in atto, lo sviluppatore front-end è libero di sviluppare il SPA e può semplicemente accedere al modello JSON tramite `this.props.cqModel`.

1. **Implementare il  `render()` metodo del componente**

   Lo sviluppatore front-end implementa il metodo `render()` nel modo in cui lo ritiene idoneo e può utilizzare i campi della proprietà `cqModel`. Questo produce il DOM e i frammenti HTML che verranno inseriti nella pagina. Questo è il modo standard per creare un&#39;app in React.

1. **Mappa il componente sul tipo di risorsa AEM tramite`MapTo()`**

   La mappatura memorizza le classi di componenti e viene utilizzata internamente dal componente `Container` fornito per recuperare e creare istanze dinamiche dei componenti in base al tipo di risorsa specificato.

   Questo serve come &quot;colla&quot; tra front-end e back-end in modo che l&#39;editor sappia quali componenti corrispondono.

   Gli `Page` e `ResponsiveGrid` sono esempi di classi che estendono la base `Container`.

1. **Definire il componente  `EditConfig` come parametro`MapTo()`**

   Questo parametro è necessario per indicare all’editor in che modo il componente deve essere nominato fino a quando non viene ancora eseguito il rendering o non ha contenuto da riprodurre.

1. **Estende la  `Container` classe fornita per pagine e contenitori**

   Le pagine e i sistemi paragrafo devono estendere questa classe in modo che la delega ai componenti interni funzioni come previsto.

1. **Implementate una soluzione di routing che utilizza l’ `History` API HTML5.**

   Quando la `ModelRouter` è abilitata, la chiamata delle funzioni `pushState` e `replaceState` attiverà una richiesta alla `PageModelManager` per recuperare un frammento mancante del modello.

   La versione corrente di `ModelRouter` supporta solo l&#39;uso di URL che puntano al percorso effettivo delle risorse dei punti di ingresso del modello Sling. Non supporta l’uso di URL personalizzati o alias.

   È possibile disabilitare o configurare `ModelRouter` per ignorare un elenco di espressioni regolari.

## AEM-agnostico {#aem-agnostic}

Questi blocchi di codice illustrano come i componenti React e Angular non necessitano di elementi  Adobe o AEM specifici.

* Tutto ciò che si trova all&#39;interno del componente JavaScript è AEMagnostico.
* Ciò che è specifico di AEM è che il componente JS deve essere mappato a un componente AEM con l’helper MapTo.

![screen_shot_2018-12-11at144019](assets/screen_shot_2018-12-11at144019.png)

Il supporto `MapTo` è la &quot;colla&quot; che permette di associare i componenti back-end e front-end:

* Indica al contenitore JS (o al sistema di paragrafi JS) quale componente JS è responsabile per il rendering di ciascuno dei componenti presenti nel JSON.
* Aggiunge all’HTML un attributo di dati HTML di cui il componente JS esegue il rendering, in modo che l’Editor di SPA sappia quale finestra di dialogo visualizzare all’autore durante la modifica del componente.

Per ulteriori informazioni sull&#39;utilizzo di `MapTo` e sulla creazione di SPA per AEM in generale, consultate la Guida introduttiva per il framework scelto.

* [Guida introduttiva alla SPA in AEM - React](/help/sites-developing/spa-getting-started-react.md)
* [Guida introduttiva a SPA in AEM - Angular](/help/sites-developing/spa-getting-started-angular.md)

## Architettura AEM e SPA {#aem-architecture-and-spas}

L’architettura generale di AEM, inclusi gli ambienti di sviluppo, creazione e pubblicazione, non cambia quando si utilizza SPA. Tuttavia, è utile comprendere in che modo SPA sviluppo si inserisce in questa architettura.

![screen_shot_2018-12-11at145348](assets/screen_shot_2018-12-11at145348.png)

* **Ambiente di generazione**

   Qui si trova l’origine dell’applicazione SPA e l’origine del componente.

   * Il generatore clientlib NPM crea una libreria client dal progetto SPA.
   * Tale libreria verrà scattata da Maven e distribuita dal plug-in Maven Build insieme al componente in AEM Author.

* **AEM Author**

   Il contenuto viene creato sull’autore AEM, inclusa la SPA di authoring.

   Quando un SPA viene modificato utilizzando l’editor SPA nell’ambiente di authoring:

   1. Il SPA richiede l’HTML esterno.
   1. Il CSS viene caricato.
   1. Viene caricato il codice JavaScript dell&#39;applicazione SPA.
   1. Quando l&#39;applicazione SPA viene eseguita, viene richiesto il JSON, che consente all&#39;app di creare il DOM della pagina, inclusi gli attributi `cq-data`.
   1. Questi attributi `cq-data` consentono all&#39;editor di caricare informazioni aggiuntive sulla pagina in modo da sapere quali configurazioni di modifica sono disponibili per i componenti.

* **AEM Publish**

   In questa area vengono pubblicati per l’uso pubblico i contenuti creati e le librerie compilate, inclusi SPA artifact dell’applicazione, clientlibs e componenti.

* **Dispatcher/CDN**

   Il dispatcher funge da livello di caching dei AEM per i visitatori del sito.

   * Le richieste vengono elaborate in modo simile a come si trovano in AEM Author, ma non vi sono richieste di informazioni sulla pagina, poiché ciò è necessario solo per l&#39;editor.
   * Javascript, CSS, JSON e HTML sono memorizzati nella cache, ottimizzando la pagina per una distribuzione rapida.

>[!NOTE]
>
>All&#39;interno AEM non è necessario eseguire meccanismi di creazione Javascript o eseguire lo stesso Javascript. AEM ospita solo gli artifact compilati dall&#39;applicazione SPA.

## Passaggi successivi {#next-steps}

Per una panoramica di come è strutturata una SPA semplice in AEM e come funziona, consultate la guida introduttiva per [React](/help/sites-developing/spa-getting-started-react.md) e [Angular](/help/sites-developing/spa-getting-started-angular.md).

Per una guida passo-passo alla creazione di SPA personali, vedere la [Guida introduttiva all&#39;editor SPA AEM - Esercitazione eventi WKND](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html).

Per ulteriori dettagli sulla mappatura del modello dinamico a componente e sul suo funzionamento all&#39;interno SPA in AEM, vedere l&#39;articolo [Mappatura del modello dinamico a componente per SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

Se desideri implementare SPA in AEM per un framework diverso da React o Angular o desideri semplicemente approfondire il funzionamento dell&#39;SDK SPA per AEM, fai riferimento all&#39;articolo [SPA Blueprint](/help/sites-developing/spa-blueprint.md).
