---
title: Sviluppo di app SPA per AEM
seo-title: Sviluppo di app SPA per AEM
description: Questo articolo presenta domande importanti da tenere in considerazione quando uno sviluppatore front-end si impegna a sviluppare un'app SPA per AEM, oltre a fornire una panoramica dell'architettura di AEM rispetto alle ZPS da tenere presente quando implementa un'app SPA sviluppata su AEM.
seo-description: Questo articolo presenta domande importanti da tenere in considerazione quando uno sviluppatore front-end si impegna a sviluppare un'app SPA per AEM, oltre a fornire una panoramica dell'architettura di AEM rispetto alle ZPS da tenere presente quando implementa un'app SPA sviluppata su AEM.
uuid: 6673a041-c557-4968-ae54-4cd5b9f56251
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9584392a-d8a3-45a4-9cdf-fd211c8e6091
docset: aem65
translation-type: tm+mt
source-git-commit: 590dc4464182d4baf8293e7bb0774ce92971c0af

---


# Sviluppo di app SPA per AEM{#developing-spas-for-aem}

Le applicazioni SPA (Single Page Applications) possono offrire esperienze coinvolgenti agli utenti di siti Web. Gli sviluppatori desiderano essere in grado di creare siti utilizzando i framework SPA e gli autori desiderano modificare facilmente i contenuti in AEM per un sito creato utilizzando tali framework.

Questo articolo presenta domande importanti da tenere in considerazione quando uno sviluppatore front-end si impegna a sviluppare un&#39;app SPA per AEM e fornisce una panoramica dell&#39;architettura di AEM rispetto alla distribuzione di app SPA su AEM.

>[!NOTE]
>
>SPA Editor è la soluzione consigliata per i progetti che richiedono il rendering lato client basato su SPA (ad esempio React o Angular).

## Principi di sviluppo SPA per AEM {#spa-development-principles-for-aem}

Lo sviluppo di applicazioni a pagina singola in AEM presuppone che lo sviluppatore front-end rispetti le best practice standard per la creazione di un&#39;app SPA. Se come sviluppatore front-end segui queste best practice generali e pochi principi specifici di AEM, l’app SPA funzionerà con [AEM e le sue funzionalità](/help/sites-developing/spa-walkthrough.md#content-editing-experience-with-spa)di authoring dei contenuti.

* **[Portabilità](/help/sites-developing/spa-architecture.md#portability)- Come per tutti i componenti,**i componenti devono essere costruiti per essere il più possibile portatili. La SPA deve essere realizzata con componenti portabili e riutilizzabili.
* **[AEM Drives Site Structure](/help/sites-developing/spa-architecture.md#aem-drives-site-structure)**- Lo sviluppatore front-end crea componenti e ne possiede la struttura interna, ma si basa su AEM per definire la struttura del contenuto del sito.
* **[Rendering](/help/sites-developing/spa-architecture.md#dynamic-rendering)**dinamico - Il rendering deve essere dinamico.
* **[Routing](#dynamic-routing)dinamico -**L&#39;SPA è responsabile del routing e AEM lo ascolta e recupera in base ad esso. Anche l&#39;indirizzamento deve essere dinamico.

Se tenete presenti questi principi nello sviluppo dell’app, sarà quanto più flessibile e affidabile possibile, consentendo al contempo tutte le funzionalità di authoring AEM supportate.

Se non è necessario supportare le funzioni di authoring di AEM, potrebbe essere necessario considerare un modello [di progettazione](/help/sites-developing/spa-architecture.md#spa-design-models)SPA diverso.

### Portabilità {#portability}

Come per lo sviluppo di qualsiasi componente, i componenti devono essere progettati in modo da massimizzarne la portabilità. Eventuali schemi che si oppongono alla portabilità o alla riutilizzabilità dei componenti dovrebbero essere evitati per garantire compatibilità, flessibilità e manutenibilità in futuro.

La SPA risultante deve essere realizzata con componenti altamente portatili e riutilizzabili.

### Struttura del sito basata su AEM {#aem-drives-site-structure}

Lo sviluppatore front-end deve considerare se stesso come responsabile della creazione di una libreria di componenti SPA utilizzati per creare l&#39;app. Lo sviluppatore front-end ha il controllo completo della struttura interna dei componenti. [Tuttavia, AEM è sempre proprietaria della struttura del sito.](/help/sites-developing/spa-overview.md)

Questo significa che lo sviluppatore front-end può aggiungere il contenuto del cliente prima o dopo il punto di ingresso dei componenti e può anche effettuare chiamate di terze parti all’interno del componente. Tuttavia, lo sviluppatore front-end non ha il controllo completo del modo in cui i componenti vengono nidificati, ad esempio.

### Rendering dinamico {#dynamic-rendering}

L&#39;area SPA deve basarsi solo sul rendering dinamico dei contenuti. Questa è l’aspettativa predefinita in cui AEM recupera e riproduce tutti gli elementi secondari della struttura del contenuto. [](/help/sites-developing/spa-architecture.md#portability)

Qualsiasi rendering esplicito che punti a contenuti specifici è considerato rendering statico e, sebbene supportato, non sarà compatibile con le funzioni di authoring dei contenuti di AEM. Ciò va anche contro il principio di [portabilità](/help/sites-developing/spa-architecture.md#portability).

### Routing dinamico {#dynamic-routing}

Come per il rendering, anche tutti i routing devono essere dinamici. In AEM, [l’app SPA deve essere sempre proprietaria dell’instradamento](/help/sites-developing/spa-routing.md) e AEM lo ascolta e recupera contenuti basati su di esso.

Qualsiasi routing statico funziona in base al [principio di portabilità](/help/sites-developing/spa-architecture.md#portability) e limita l’autore in quanto non è compatibile con le funzioni di authoring dei contenuti di AEM. Ad esempio, con l&#39;indirizzamento statico, se l&#39;autore del contenuto desidera modificare una route o una pagina, deve chiedere allo sviluppatore front-end di farlo.

## AEM Project Archetype {#aem-project-archetype}

Qualsiasi progetto AEM deve sfruttare il tipo di archivio dei progetti [AEM](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/developing/archetype/overview.html), che supporta i progetti SPA mediante React o Angular e sfrutta l’SDK SPA.

## Modelli di progettazione SPA {#spa-design-models}

Se vengono seguiti i [principi dello sviluppo di app per app in AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem) , l’app SPA funzionerà con tutte le funzioni di authoring dei contenuti AEM supportate. [](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)

Ci possono essere tuttavia dei casi in cui ciò non è del tutto necessario. La tabella seguente fornisce una panoramica dei vari modelli di progettazione, dei relativi vantaggi e dei relativi svantaggi.

<table>
 <tbody>
  <tr>
   <th><strong>Modello di progettazione<br /> </strong></th>
   <th><strong>Vantaggi</strong></th>
   <th><strong>Svantaggi</strong></th>
  </tr>
  <tr>
   <td>AEM viene utilizzato come CMS headless senza utilizzare il framework SDK dell’editor <a href="/help/sites-developing/spa-reference-materials.md">SPA.</a></td>
   <td>Lo sviluppatore front-end ha il controllo completo sull'app.</td>
   <td><p>Gli autori dei contenuti non possono sfruttare l'esperienza di authoring dei contenuti di AEM.</p> <p>Il codice non è né portatile né riutilizzabile se contiene riferimenti statici o routing.</p> <p>Non consente l'utilizzo dell'editor modelli, pertanto lo sviluppatore front-end deve mantenere i modelli modificabili tramite JCR.</p> </td>
  </tr>
  <tr>
   <td>Lo sviluppatore front-end utilizza il framework SPA Editor SDK, ma apre solo alcune aree all’autore del contenuto.</td>
   <td>Lo sviluppatore mantiene il controllo sull'app abilitando solo l'authoring nelle aree limitate dell'app.</td>
   <td><p>Gli autori dei contenuti sono limitati a una serie limitata di esperienze di authoring dei contenuti di AEM.</p> <p>Il codice non può essere portatile né riutilizzabile se contiene riferimenti statici o routing.</p> <p>Non consente l'utilizzo dell'editor modelli, pertanto lo sviluppatore front-end deve mantenere i modelli modificabili tramite JCR.</p> </td>
  </tr>
  <tr>
   <td>Il progetto sfrutta appieno l’SDK dell’editor SPA e i componenti frontend sono sviluppati come libreria e la struttura del contenuto dell’app è delegata ad AEM.</td>
   <td><p>L'app è riutilizzabile e portatile.</p> <p>L'autore del contenuto può modificare l'app utilizzando l'esperienza di authoring dei contenuti di AEM.<br /> </p> <p>L'SPA è compatibile con l'editor modelli.</p> </td>
   <td><p>Lo sviluppatore non ha il controllo della struttura dell'app e della parte di contenuto delegata ad AEM.</p> <p>Lo sviluppatore può comunque riservare aree dell’app per il contenuto che non deve essere creato tramite AEM.</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Sebbene tutti i modelli siano supportati in AEM, solo implementando il terzo (e quindi seguendo i principi di sviluppo [SPA consigliati in AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)) gli autori dei contenuti potranno interagire con e modificare i contenuti dell’SPA in AEM così come sono abituati.
>[](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem)

## Migrazione di SPA esistenti ad AEM {#migrating-existing-spas-to-aem}

In genere, se la tua SPA rispetta i principi di sviluppo [SPA per AEM](/help/sites-developing/spa-architecture.md#spa-development-principles-for-aem), la tua SPA lavorerà in AEM e potrà essere modificata utilizzando AEM SPA Editor.

Segui questi passaggi per rendere l’app SPA esistente pronta per l’utilizzo con AEM.

1. **I componenti JS sono modulari.**

   Renderli in grado di essere sottoposti a rendering in qualsiasi ordine, posizione e dimensione.
1. **Utilizza i contenitori forniti dal nostro SDK per inserire i componenti sullo schermo.**

   In AEM è disponibile un componente del sistema paragrafo e della pagina da usare.
1. **Create un componente AEM per ciascun componente JS.**

   I componenti AEM definiscono la finestra di dialogo e l’output JSON.

## Istruzioni per gli sviluppatori front-end {#instructions-for-front-end-developers}

L’attività principale per coinvolgere uno sviluppatore front-end nella creazione di un’app SPA per AEM consiste nell’accordarsi sui componenti e sui modelli JSON.

Di seguito è riportato un profilo dei passi che uno sviluppatore front-end deve seguire nello sviluppo di un&#39;app SPA per AEM.

1. **Concordare sui componenti e il relativo modello JSON**

   Gli sviluppatori front-end e gli sviluppatori back-end AEM devono concordare su quali componenti sono necessari e un modello, per cui esiste una corrispondenza uno-a-uno tra i componenti SPA e i componenti back-end.

   I componenti AEM sono ancora necessari soprattutto per fornire finestre di dialogo di modifica ed esportare il modello di componente.

1. **In React components, accedere al modello tramite`this.props.cqModel`**

   Una volta che i componenti sono concordati e il modello JSON è in atto, lo sviluppatore front-end è libero di sviluppare l&#39;SPA e può semplicemente accedere al modello JSON tramite `this.props.cqModel`.

1. **Implementare il metodo del`render()`componente**

   Lo sviluppatore front-end implementa il `render()` metodo nel modo in cui lo ritiene opportuno e può utilizzare i campi della `cqModel` proprietà. Questo produce il DOM e i frammenti HTML che verranno inseriti nella pagina. Questo è il modo standard per creare un&#39;app in React.

1. **Mappa il componente sul tipo di risorsa AEM tramite`MapTo()`**

   La mappatura memorizza le classi di componenti e viene utilizzata internamente dal `Container` componente fornito per recuperare e creare in modo dinamico le istanze dei componenti in base al tipo di risorsa specificato.

   Questo serve come &quot;colla&quot; tra front-end e back-end in modo che l&#39;editor sappia quali componenti corrispondono.

   Gli esempi `Page` e `ResponsiveGrid` sono buoni di classi che estendono la base `Container`.

1. **Definite il componente come`EditConfig`parametro in`MapTo()`**

   Questo parametro è necessario per indicare all’editor in che modo il componente deve essere nominato fino a quando non viene ancora eseguito il rendering o non ha contenuto da riprodurre.

1. **Estende la`Container`classe fornita per pagine e contenitori**

   Le pagine e i sistemi paragrafo devono estendere questa classe in modo che la delega ai componenti interni funzioni come previsto.

1. **Implementate una soluzione di routing che utilizza l’`History`API HTML5.**

   Quando `ModelRouter` è abilitata, la chiamata delle funzioni `pushState` e `replaceState` attiverà una richiesta `PageModelManager` per recuperare un frammento mancante del modello.

   La versione corrente dell&#39; `ModelRouter` unico supporto per l&#39;uso di URL che puntano al percorso effettivo delle risorse dei punti di ingresso del modello Sling. Non supporta l’uso di URL personalizzati o alias.

   È `ModelRouter` possibile disabilitare o configurare in modo da ignorare un elenco di espressioni regolari.

## AEM-Agnostic {#aem-agnostic}

Questi blocchi di codice illustrano come i componenti React e Angular non necessitano di elementi specifici di Adobe o AEM.

* Tutto ciò che si trova all’interno del componente JavaScript è agnostico di AEM.
* Ciò che è specifico di AEM è che il componente JS deve essere mappato a un componente AEM con l’helper MapTo.

![screen_shot_2018-12-11at144019](assets/screen_shot_2018-12-11at144019.png)

L&#39; `MapTo` aiutante è la &quot;colla&quot; che permette di combinare i componenti back-end e front-end:

* Indica al contenitore JS (o al sistema di paragrafi JS) quale componente JS è responsabile per il rendering di ciascuno dei componenti presenti nel JSON.
* Aggiunge un attributo di dati HTML al codice HTML rappresentato dal componente JS, in modo che l’editor SPA sappia quale finestra di dialogo visualizzare all’autore quando modifica il componente.

Per ulteriori informazioni sull’utilizzo `MapTo` e la creazione di app SPA per AEM in generale, consulta la Guida introduttiva per il framework scelto.

* [Guida introduttiva all’app SPA in AEM - React](/help/sites-developing/spa-getting-started-react.md)
* [Guida introduttiva alle app SPA in AEM - Angular](/help/sites-developing/spa-getting-started-angular.md)

## Architettura AEM e SPA {#aem-architecture-and-spas}

L’architettura generale di AEM, compresi gli ambienti di sviluppo, authoring e pubblicazione, non cambia quando si utilizzano gli ZPS. Tuttavia, è utile comprendere in che modo lo sviluppo SPA si inserisce in questa architettura.

![screen_shot_2018-12-11at145348](assets/screen_shot_2018-12-11at145348.png)

* **Ambiente di generazione**

   Qui si trova l&#39;origine dell&#39;applicazione SPA e l&#39;origine del componente.

   * Il generatore clientlib NPM crea una libreria client dal progetto SPA.
   * Tale libreria verrà scattata da Maven e distribuita dal plug-in Maven Build insieme al componente in AEM Author.

* **AEM Author**

   Il contenuto viene creato sull’autore di AEM, inclusa la creazione di SPA.

   Quando si modifica un&#39;app SPA utilizzando l&#39;editor SPA nell&#39;ambiente di authoring:

   1. SPA richiede l’HTML esterno.
   1. Il CSS viene caricato.
   1. Viene caricato il codice JavaScript dell’applicazione SPA.
   1. Quando l&#39;applicazione SPA viene eseguita, viene richiesto l&#39;JSON, che consente all&#39;app di creare il DOM della pagina, inclusi gli `cq-data` attributi.
   1. Questi `cq-data` attributi consentono all’editor di caricare informazioni aggiuntive sulla pagina, in modo da sapere quali configurazioni di modifica sono disponibili per i componenti.

* **AEM Publish**

   Qui vengono pubblicati per l’uso pubblico i contenuti creati e le librerie compilate, inclusi gli artefatti dell’applicazione SPA, i clientlibs e i componenti.

* **Dispatcher/CDN**

   Il dispatcher funge da livello di caching di AEM per i visitatori del sito.

   * Le richieste vengono elaborate in modo simile a come si trovano in AEM Author, ma non vi sono richieste di informazioni sulla pagina, poiché ciò è necessario solo per l&#39;editor.
   * Javascript, CSS, JSON e HTML sono memorizzati nella cache, ottimizzando la pagina per una distribuzione rapida.

>[!NOTE]
>
>All’interno di AEM non è necessario eseguire meccanismi di creazione Javascript o eseguire il codice JavaScript stesso. AEM ospita solo gli artifact compilati dall’applicazione SPA.

## Passaggi successivi {#next-steps}

Per una panoramica della struttura e del funzionamento di un semplice SPA in AEM, consulta la guida introduttiva per [React](/help/sites-developing/spa-getting-started-react.md) e [Angular](/help/sites-developing/spa-getting-started-angular.md).

Per una guida passo-passo alla creazione di un vostro SPA, consultate la [Guida introduttiva all’Editor AEM SPA - Esercitazione](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html)sugli eventi WKND.

Per ulteriori dettagli sulla mappatura del modello dinamico a componente e sul suo funzionamento all’interno degli SPA in AEM, consultate l’articolo Mappatura [dinamica da modello a componente per gli SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

Se desideri implementare gli SPA in AEM per un framework diverso da React o Angular o vuoi semplicemente approfondire il funzionamento dell’SDK SPA per AEM, consulta l’articolo [SPA Blueprint](/help/sites-developing/spa-blueprint.md) .
