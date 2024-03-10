---
title: Best practice per l’utilizzo dei moduli adattivi
description: Spiega le best practice per la configurazione di un progetto AEM Forms, lo sviluppo di moduli adattivi e l’ottimizzazione delle prestazioni del sistema AEM Forms.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
feature: Adaptive Forms, Foundation Components
exl-id: 5c75ce70-983e-4431-a13f-2c4c219e8dde
source-git-commit: f349c8fd9c370ba589d217cd3b1d0521ae5c5597
workflow-type: tm+mt
source-wordcount: '4668'
ht-degree: 0%

---

# Best practice per l’utilizzo dei moduli adattivi {#best-practices-for-working-with-adaptive-forms}

<span class="preview"> L’Adobe consiglia di utilizzare l’acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

## Panoramica {#overview}

I moduli di Adobe Experience Manager (AEM) possono aiutarti a trasformare transazioni complesse in esperienze digitali semplici e deliziose. Tuttavia, richiede uno sforzo concertato per implementare, generare, eseguire e mantenere un ecosistema AEM Forms efficiente e produttivo.

Questo documento fornisce linee guida e consigli di cui possono beneficiare amministratori, autori e sviluppatori di Forms quando lavorano con AEM Forms, in particolare con il componente Moduli adattivi. Descrive le best practice, dall’impostazione di un progetto di sviluppo di moduli alla configurazione, alla personalizzazione, all’authoring e all’ottimizzazione di AEM Forms. Queste best practice contribuiscono collettivamente alle prestazioni complessive dell’ecosistema AEM Forms.

Inoltre, di seguito sono riportate alcune indicazioni consigliate sulle best practice generali per l’AEM:

* [Best practice: distribuzione e manutenzione dell’AEM](/help/sites-deploying/best-practices.md)
* [Best practice: authoring dei contenuti](/help/sites-authoring/best-practices.md)
* [Best practice: amministrazione dell’AEM](/help/sites-administering/administer-best-practices.md)
* [Best practice: sviluppo di soluzioni](/help/sites-developing/best-practices.md)

## Configurare AEM Forms {#set-up-and-configure-aem-forms}

### Configurazione del progetto di sviluppo dei moduli {#setting-up-forms-development-project}

Una struttura di progetto semplificata e standardizzata può ridurre notevolmente gli sforzi di sviluppo e manutenzione. Apache Maven è uno strumento open source consigliato per la creazione di progetti AEM.

* Utilizzare Apache Maven `aem-project-archetype` creare e gestire la struttura del progetto AEM. Crea la struttura e i modelli consigliati per il progetto AEM. Inoltre, fornisce sistemi di automazione della build e di controllo delle modifiche per facilitare la gestione del progetto.

   * Utilizzare Maven `archetype:generate` per generare la struttura iniziale.
   * Usa Maven `eclipse:eclipse` per generare i file di progetto dell&#39;eclisse e importare il progetto in eclissi.

Per ulteriori informazioni, consulta [Come creare progetti AEM con Apache Maven](/help/sites-developing/ht-projects-maven.md).

* Lo strumento FileVault o VLT consente di mappare il contenuto di un&#39;istanza CRX o AEM al file system. Fornisce operazioni di gestione del controllo delle modifiche, come il check-in e il check-out del contenuto del progetto AEM. Consulta [Come utilizzare lo strumento VLT](/help/sites-developing/ht-vlttool.md).

* Se utilizzi un ambiente di sviluppo integrato con Eclipse, puoi utilizzare gli strumenti per sviluppatori AEM per integrare perfettamente Eclipse IDE con le istanze AEM per creare applicazioni AEM. Per ulteriori informazioni, consulta [Strumenti per sviluppatori AEM per Eclipse](/help/sites-developing/aem-eclipse.md).

* Non memorizzare alcun contenuto e non apportare modifiche nella cartella /libs. Crea sovrapposizioni nelle cartelle /app per estendere o sovrascrivere le funzionalità predefinite.

* Quando crei pacchetti per spostare il contenuto, assicurati che i percorsi dei filtri dei pacchetti siano corretti e che siano menzionati solo i percorsi richiesti.

* Non memorizzare alcun contenuto e non apportare modifiche nella cartella /libs. Crea sovrapposizioni nelle cartelle /app per estendere o sovrascrivere le funzionalità predefinite.

* Definire le dipendenze corrette per i pacchetti in modo da forzare un ordine/sequenza di installazione predeterminato.

* Non creare nodi referenziabili in /libs o /apps.

### Pianificazione per l’ambiente di authoring {#planning-for-authoring-environment}

Dopo aver configurato il progetto AEM, definisci la strategia per l’authoring e la personalizzazione dei modelli e dei componenti dei moduli adattivi.

* Un modello di modulo adattivo è una pagina AEM specializzata che definisce la struttura e le informazioni intestazione-piè di pagina di un modulo adattivo. Un modello presenta layout, stili e struttura di base preconfigurati per un modulo adattivo. AEM Forms fornisce modelli e componenti pronti all’uso che puoi utilizzare per la creazione di moduli adattivi. Tuttavia, puoi creare modelli e componenti personalizzati in base alle tue esigenze. Si consiglia di raccogliere i requisiti per i modelli e i componenti aggiuntivi necessari nei moduli adattivi. Per ulteriori informazioni, consulta [Personalizzazione di moduli e componenti adattivi](/help/forms/using/adaptive-forms-best-practices.md#customize-components).
* AEM Forms consente di creare moduli adattivi basati sui seguenti modelli di moduli. I modelli di modulo fungono da interfaccia per lo scambio di dati tra un modulo e un sistema AEM e forniscono una struttura basata su XML per il flusso di dati all’interno e all’esterno di un modulo adattivo. Inoltre, i modelli di modulo impongono regole e vincoli ai moduli adattivi sotto forma di vincoli di schema e XFA.

   * **Nessuno**: i moduli adattivi creati con questa opzione non utilizzano alcun modello di modulo. I dati XML generati da tali moduli hanno una struttura piatta con campi e valori corrispondenti.
   * **Schema XML o JSON**: gli schemi XML e JSON rappresentano la struttura in cui i dati vengono prodotti o utilizzati dal sistema back-end dell’organizzazione. È possibile associare uno schema a un modulo adattivo e utilizzarne gli elementi per aggiungere contenuto dinamico al modulo adattivo. Gli elementi dello schema sono disponibili nella scheda Oggetto modello dati del browser dei contenuti per la creazione di moduli adattivi. Puoi trascinare gli elementi dello schema per creare il modulo.
   * **Modello di modulo XFA**: è un modello di modulo ideale se disponi di investimenti in moduli HTML5 basati su XFA. Fornisce un modo diretto per convertire i moduli basati su XFA in moduli adattivi. Eventuali regole XFA esistenti vengono mantenute nei moduli adattivi associati. I moduli adattivi risultanti supportano i costrutti XFA, ad esempio convalide, eventi, proprietà e modelli.
   * **Modello dati modulo**: si tratta di un modello di modulo preferito se desideri integrare sistemi back-end come database, servizi web e profilo utente AEM per precompilare moduli adattivi e riscrivere i dati dei moduli inviati nei sistemi back-end. L’editor modello dati modulo consente di definire e configurare entità e servizi in un modello dati modulo da utilizzare per creare moduli adattivi. Per ulteriori informazioni, consulta [Integrazione dei dati di AEM Forms](/help/forms/using/data-integration.md).

È importante scegliere con attenzione il modello dati che non solo soddisfa le tue esigenze, ma estende gli investimenti esistenti in risorse XFA e XSD, se presenti. Utilizzare il modello XSD per creare modelli di modulo, in quanto l&#39;XML generato contiene dati in base all&#39;XPATH definito dallo schema. L’utilizzo del modello XSD come scelta predefinita per il modello dati del modulo è utile anche perché disaccoppia la progettazione del modulo dal sistema back-end che elabora e utilizza i dati e migliora le prestazioni del modulo grazie alla mappatura uno a uno dei campi del modulo. Inoltre, BindRef del campo può essere reso l’XPATH del relativo valore dati in XML.

Per ulteriori informazioni, consulta [Creare un modulo adattivo](/help/forms/using/creating-adaptive-form.md).

* Esistono alcune sezioni comuni tra i moduli adattivi. Puoi identificarli e definire una strategia per promuovere il riutilizzo dei contenuti. I moduli adattivi consentono di creare frammenti autonomi e riutilizzarli in tutti i moduli. È inoltre possibile salvare un pannello in un modulo adattivo come frammento. Qualsiasi modifica apportata a un frammento si riflette in tutte le maschere associate. Consente di ridurre i tempi di authoring e garantisce la coerenza tra i moduli. Inoltre, l’utilizzo dei frammenti rende leggeri i moduli adattivi, offrendo in tal modo una migliore esperienza di authoring, soprattutto per le forme di grandi dimensioni. Per ulteriori informazioni, consulta [Frammenti di moduli adattivi](/help/forms/using/adaptive-form-fragments.md).

### Personalizzazione di moduli e componenti adattivi {#customize-components}

* AEM Forms fornisce modelli di moduli adattivi pronti all’uso che è possibile utilizzare per creare moduli adattivi. Puoi anche creare modelli personalizzati. L’AEM fornisce modelli statici e modificabili.

   * I modelli statici sono definiti e configurati dagli sviluppatori.
   * I modelli modificabili vengono creati dagli autori mediante l’editor di modelli. L’editor modelli ti consente di definire una struttura di base e il contenuto iniziale in un modello. Qualsiasi modifica nel livello struttura si riflette in tutti i moduli che utilizzano tale modello. Il contenuto iniziale può includere un tema preconfigurato, un servizio di precompilazione, un’azione di invio e così via. Tuttavia, queste impostazioni possono essere modificate per un modulo utilizzando l’editor di moduli. Per ulteriori informazioni, consulta [Modelli di modulo adattivo](/help/forms/using/template-editor.md).

* Per assegnare uno stile a un campo o a un’istanza di pannello specifica, utilizza [stile in linea](/help/forms/using/inline-style-adaptive-forms.md). In alternativa, puoi definire una classe in un file CSS e specificare il nome della classe nella proprietà Classe CSS del componente.
* Includi una libreria client in un componente per applicare in modo coerente gli stili tra i moduli adattivi o i frammenti che utilizzano tale componente. Per ulteriori informazioni, consulta [Creare un componente pagina modulo adattivo](/help/forms/using/custom-adaptive-forms-templates.md).
* Applica gli stili definiti in una libreria client per selezionare i moduli adattivi specificando il percorso della libreria client nel campo Percorso file CSS nelle proprietà del contenitore di moduli adattivi.
* Per creare una libreria client degli stili, puoi configurare il file CSS personalizzato nella libreria client di base dell’Editor temi o nelle proprietà Contenitore modulo.
* I moduli adattivi forniscono layout di pannello, ad esempio reattivi, a schede, fisarmoniche e procedura guidata, per controllare il layout dei componenti del modulo in un pannello. È possibile creare layout di pannello personalizzati e renderli disponibili per l&#39;utilizzo da parte degli autori di moduli. Per ulteriori informazioni, consulta [Creazione di componenti di layout personalizzati per i moduli adattivi](/help/forms/using/custom-layout-components-forms.md).
* Puoi anche personalizzare specifici componenti del modulo adattivo, come campi e layout del pannello.

   * Utilizza il [Sovrapposizione](/help/sites-developing/overlays.md) funzionalità dell’AEM per modificare una copia di un componente. Si sconsiglia di modificare i componenti predefiniti.
   * Per personalizzare il layout dei componenti predefiniti dei moduli adattivi in /libs, [creare componenti di layout personalizzati](/help/forms/using/custom-layout-components-forms.md) oltre al [layout predefiniti](/help/forms/using/layout-capabilities-adaptive-forms.md).
   * Introdurre interattività personalizzate creando widget o aspetti personalizzati. Si sconsiglia di modificare i componenti predefiniti. Per ulteriori informazioni, consulta [Framework aspetto](/help/forms/using/introduction-widgets.md).

* Consulta [Trattamento di informazioni personali](/help/forms/using/adaptive-forms-best-practices.md#p-handling-personally-identifiable-information-p) per raccomandazioni sulla gestione dei dati PII.

### Creazione di modelli di modulo

Puoi creare un modulo adattivo utilizzando i modelli di modulo abilitati in **Browser configurazioni**. Per attivare i modelli di modulo, vedere [Creazione di un modello di modulo adattivo](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/creating-your-first-adaptive-form/create-adaptive-form-template.html?lang=en).

I modelli di modulo possono essere caricati anche da pacchetti di moduli adattivi creati in un altro computer di authoring. I modelli di modulo sono resi disponibili mediante l&#39;installazione di [pacchetti aemforms-references-*](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en). Alcune delle best practice consigliate sono:

* Il **nosamplecontent** La modalità di esecuzione è consigliata solo per i nodi di authoring e non di pubblicazione.
* L’authoring di risorse come moduli adattivi, temi, modelli o configurazioni cloud viene eseguito solo sui nodi di authoring, che possono essere pubblicati sui nodi di pubblicazione configurati.
Per ulteriori informazioni, consulta [Pubblicazione e annullamento della pubblicazione di moduli e documenti](https://experienceleague.adobe.com/docs/experience-manager-65/forms/publish-process-aem-forms/publishing-unpublishing-forms.html?lang=en)
* Il pacchetto aggiuntivo Forms è necessario per il supporto delle operazioni di authoring e pubblicazione dei servizi documentali; può quindi essere considerato una dipendenza.
Se desideri solo modelli di esempio, temi e pacchetti DOR relativi a Forms, puoi scaricarli da [pacchetti aemforms-references-*](https://experienceleague.adobe.com/docs/experience-manager-65/forms/publish-process-aem-forms/publishing-unpublishing-forms.html?lang=en).

Per ulteriori informazioni, consulta le best practice in [Introduzione all’authoring di moduli adattivi](/help/forms/using/introduction-forms-authoring.md).

## Creare moduli adattivi {#author-adaptive-forms}

### Utilizzo dell’interfaccia touch per l’authoring {#using-touch-optimized-ui-for-authoring}

* Utilizza il browser Oggetti nella barra laterale per accedere rapidamente ai campi in fondo alla gerarchia del modulo. È possibile utilizzare la casella di ricerca per cercare oggetti nel modulo o nella struttura ad albero degli oggetti per spostarsi da un oggetto all&#39;altro.
* Per visualizzare e modificare le proprietà di un componente nel browser Componenti nella barra laterale, seleziona il componente e fai clic su ![cmppr-1](assets/cmppr-1.png). Puoi anche fare doppio clic su un componente per visualizzarne le proprietà nel browser delle proprietà.
* Utilizzare le scelte rapide da tastiera per eseguire azioni rapide sui moduli. Consulta [Scelte rapide da tastiera per AEM Forms](/help/forms/using/keyboard-shortcuts.md).

* L’utilizzo dei componenti di moduli adattivi è consigliato solo nelle pagine di moduli adattivi. I componenti dipendono dalla gerarchia principale. Pertanto, non utilizzarli in una pagina AEM.

Inoltre, consulta Descrizioni dei componenti e best practice in [Introduzione all’authoring di moduli adattivi](/help/forms/using/introduction-forms-authoring.md).

### Utilizzo delle regole nei moduli adattivi {#using-rules-in-adaptive-forms}

AEM Forms fornisce una [editor di regole](/help/forms/using/rule-editor.md) che consente di creare regole per aggiungere un comportamento dinamico ai componenti di moduli adattivi. Utilizzando queste regole, puoi valutare le condizioni e attivare azioni sui componenti, ad esempio mostrare o nascondere i campi, calcolare i valori, modificare dinamicamente l’elenco a discesa e così via.

L’editor di regole fornisce un editor visivo e un editor di codice per la scrittura di regole. Quando scrivi le regole utilizzando la modalità editor di codice, tieni presente quanto segue:

* Utilizza nomi significativi e univoci per i campi modulo e i componenti per evitare possibili conflitti durante la scrittura delle regole.
* Utilizzare `this` affinché un componente faccia riferimento a se stesso in un&#39;espressione di regola. In questo modo la regola rimane valida anche se il nome del componente cambia. Esempio: `field1.valueCommit script: this.value > 10`.

* Utilizza i nomi dei componenti quando fai riferimento ad altri componenti del modulo. Utilizza il `value` per recuperare il valore di un campo o di un componente. Esempio: `field1.value`.

* Per evitare conflitti, fai riferimento ai componenti per gerarchia univoca relativa. Esempio: `parentName.fieldName`.

* Quando gestisci regole complesse o di uso comune, considera la scrittura di regole business come funzioni in una libreria client separata che puoi specificare e riutilizzare nei moduli adattivi. La libreria client deve essere una libreria indipendente e non deve avere dipendenze esterne, ad eccezione di jQuery e Underscore.js. Puoi anche utilizzare la libreria client per applicare [riconvalida lato server](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form) dei dati modulo inviati.
* I moduli adattivi forniscono un set di API che è possibile utilizzare per comunicare con ed eseguire azioni sui moduli adattivi. Alcune delle API chiave sono le seguenti. Per ulteriori informazioni, consulta [Riferimento API della libreria JavaScript per Adaptive Forms](https://adobe.com/go/learn_aemforms_documentation_63).

   * `guideBridge.reset()`: reimposta un modulo.
   * `guideBridge.submit()`: invia un modulo.
   * `guideBridge.setFocus(somExp, focusOption, runCompletionExp)`: imposta lo stato attivo su un campo.
   * `guideBridge.validate(errorList, somExpression, focus)`: convalida un modulo.
   * `guideBridge.getDataXML(options)`: ottiene i dati del modulo come XML.
   * `guideBridge.resolveNode(somExpression)`: ottiene un oggetto modulo.
   * `guideBridge.setProperty(somList, propertyName, valueList)`: imposta la proprietà di un oggetto modulo.
   * Inoltre, puoi utilizzare le seguenti proprietà del campo:

      * `field.value` per modificare il valore di un campo.
      * `field.enabled` per attivare/disattivare un campo.
      * `field.visible` per modificare la visibilità di un campo.

* Gli autori di moduli adattivi potrebbero dover scrivere codice JavaScript per creare una logica di business in un modulo. Anche se JavaScript è potente ed efficace, è probabile che possa compromettere le aspettative di sicurezza. Pertanto, devi assicurarti che l’autore del modulo sia un utente fidato e che esistano processi per rivedere e approvare il codice JavaScript prima che un modulo venga messo in produzione. L’amministratore può limitare l’accesso all’editor di regole ai gruppi di utenti in base al loro ruolo o funzione. Consulta [Concedere l’accesso all’editor di regole a specifici gruppi di utenti](/help/forms/using/rule-editor-access-user-groups.md).
* È possibile utilizzare le espressioni nelle regole per rendere dinamici i moduli adattivi. Tutte le espressioni sono espressioni JavaScript valide e utilizzano API di modelli di script per moduli adattivi. Queste espressioni restituiscono valori di determinati tipi. Per ulteriori informazioni sulle espressioni e sulle relative best practice, consulta [Espressioni modulo adattivo](/help/forms/using/adaptive-form-expressions.md).

* L’Adobe consiglia di utilizzare operazioni sincrone JavaScript anziché asincrone durante la creazione di regole con l’editor di regole. L&#39;uso di operazioni asincrone è fortemente sconsigliato. Tuttavia, se ti trovi in una situazione in cui le operazioni asincrone sono inevitabili, è essenziale implementare le funzioni di chiusura JavaScript. In questo modo, puoi proteggere efficacemente da potenziali condizioni di concorrenza, garantendo prestazioni ottimali alle tue implementazioni di regole e mantenendo la stabilità nell’intero processo.

  Ad esempio, supponiamo che sia necessario recuperare dati da un’API esterna e quindi applicare alcune regole in base a tali dati. Utilizziamo una chiusura per gestire la chiamata API asincrona e ci assicuriamo che le regole vengano applicate dopo il recupero dei dati. Di seguito è riportato un codice di esempio:

  ```JavaScript
       function fetchDataFromAPI(apiEndpoint, callback) {
        // Simulate asynchronous API call with setTimeout
        setTimeout(() => {
          // Assuming the API call is successful, we receive some data
          const data = {
            someValue: 42,
          };
          // Invoke the callback with the fetched data
          callback(data);
        }, 2000); // Simulate a 2-second delay for the API call
      }
      // Rule implementation using Closure
      function ruleImplementation(apiEndpoint) {
        // Using a closure to handle the asynchronous API call and rule application
        // say you have set this value in street field inside address panel
        var streetField = address.street;
        fetchDataFromAPI(apiEndpoint, (data) => {
          streetField.value = data.someValue;
        });
      }
      // Example usage of the rule implementation
      const apiEndpoint = "https://example-api.com/data";
      ruleImplementation(apiEndpoint);
  ```

  In questo esempio, `fetchDataFromAPI` simula una chiamata API asincrona utilizzando `setTimeout`. Una volta recuperati i dati, richiama la funzione di callback fornita, che è la chiusura per gestire la successiva applicazione della regola. Il `ruleImplementation` contiene la logica della regola.


### Utilizzo dei temi {#working-with-themes}

Adattivo per i temi consente di creare stili riutilizzabili che possono essere applicati tra i moduli per ottenere un aspetto e uno stile coerenti. Utilizzate i temi per definire lo stile dei componenti modulo e dei pannelli. Di seguito sono riportate alcune best practice relative ai temi:

* Utilizza la libreria delle risorse per applicare rapidamente stili di testo, sfondo e immagini. Quando uno stile viene aggiunto nella libreria delle risorse, è disponibile per altri temi e nella modalità di stile dell’editor di moduli.
* Applica impostazioni globali come font e sfondo della pagina utilizzando il selettore a livello di pagina.
* Utilizza le librerie client per importare nei temi gli stili esistenti o avanzati.
* È possibile modificare lo stile per campi, pannelli o pulsanti specifici in un livello di stile modulo.
* Se un tema non soddisfa i requisiti di stile, è possibile utilizzare classi predefinite quali guideFieldNode, guideFieldLabel, guideFieldWidget e guidePanelNode per applicare uno stile comune ai moduli.

Per ulteriori informazioni, consulta [Temi](/help/forms/using/themes.md).

### Ottimizzazione delle prestazioni di moduli complessi e di grandi dimensioni {#optimizing-performance-of-large-and-complex-forms}

Gli autori e gli utenti finali di moduli in genere riscontrano problemi di prestazioni quando caricano moduli di grandi dimensioni in modalità di authoring o in fase di esecuzione. Con l’aumento del numero di oggetti (campi e pannelli) nei moduli, l’esperienza di authoring e runtime inizia a peggiorare. Inoltre, impedisce a più autori di collaborare e creare un modulo contemporaneamente.

Per risolvere i problemi di prestazioni con i moduli di grandi dimensioni, considera le seguenti best practice:

* Si consiglia di creare moduli adattivi utilizzando il modello dati del modulo XSD anche quando si converte un XFA in modulo adattivo, se possibile.
* Includi solo i campi e i pannelli nei moduli adattivi che acquisiscono informazioni dall’utente. Valuta se mantenere minimo il contenuto statico o utilizza URL per aprirli in una finestra separata.
* Anche se ogni modulo è progettato per uno scopo specifico, nella maggior parte dei moduli sono presenti alcuni segmenti comuni. Ad esempio, dati personali, indirizzo, dettagli sull’impiego e così via. Crea [frammenti di moduli adattivi](/help/forms/using/adaptive-form-fragments.md) per gli elementi e le sezioni dei moduli comuni e utilizzarli in tutti i moduli. È inoltre possibile salvare un pannello in un modulo esistente come frammento. Qualsiasi modifica in un frammento si riflette in tutti i moduli adattivi associati. Promuove l’authoring collaborativo in quanto più autori possono lavorare contemporaneamente su diversi frammenti che compongono un modulo.

   * Analogamente ai moduli adattivi, si consiglia di definire nella libreria client tutti gli stili e gli script personalizzati specifici del frammento, utilizzando la finestra di dialogo del contenitore di frammenti. Inoltre, prova a creare frammenti autosufficienti che non dipendono da oggetti esterni.
   * Evita l’utilizzo di script per più frammenti. Se è presente un oggetto esterno al frammento a cui si deve fare riferimento, provare a rendere tale oggetto parte del modulo principale. Se l’oggetto deve ancora trovarsi in un altro frammento, fai riferimento a esso con il relativo nome nello script.

* Utilizza Salva e riprendi con salvataggio automatico per salvare periodicamente il modulo adattivo e consentire agli utenti di visitarlo nuovamente in un secondo momento per completare il modulo.
* Configura i frammenti per caricarli in modo differito. In fase di runtime, il rendering del frammento contrassegnato per il caricamento in modo differito viene eseguito solo quando necessario. Riduce in modo significativo il tempo di caricamento per i moduli di grandi dimensioni. È supportato anche nei frammenti con pannelli ripetibili. Per ulteriori informazioni, consulta [Configurare il caricamento lento](/help/forms/using/lazy-loading-adaptive-forms.md).

   * Non configurare il caricamento lento sui frammenti in un layout di griglia reattiva o nel primo pannello.
   * I componenti Allegato file e Termini e condizioni non sono supportati nei frammenti caricati in modo differito.
   * Contrassegna un valore in un pannello con caricamento lazy come Usa valore a livello globale se tale valore viene utilizzato in un’altra parte del modulo in modo che sia disponibile per l’uso quando il pannello che lo contiene viene scaricato.
   * È consigliabile scrivere regole di visibilità per i frammenti che devono essere visualizzati o nascosti in base a una condizione.
* Imposta il valore del **Numero di chiamate per richiesta** nel **Servlet principale Apache Sling** a un numero abbastanza elevato. Consente al server Forms di consentire chiamate aggiuntive. Nella configurazione viene visualizzato il valore predefinito 1500. Il valore, 1500 chiamate, è per altri componenti di Experience Manager come Sites e Assets. Il set di valori predefinito per i moduli adattivi è 20000. Se si incontra il `too many calls` errore nei registri o se il rendering del modulo non riesce, prova ad aumentare il valore a un numero elevato per risolvere il problema. Se il numero di chiamate supera i 20000, significa che il modulo è complesso e potrebbe richiedere un po’ di tempo per il rendering nel browser. Questo accade solo la prima volta che il modulo viene caricato, dopo che il modulo è stato memorizzato nella cache e una volta memorizzato nella cache, non vi è alcun impatto significativo sulle prestazioni.

### Precompilazione dei moduli adattivi {#prefilling-adaptive-forms}

Puoi precompilare i campi dei moduli adattivi con dati recuperati dal backend per consentire agli utenti di compilare rapidamente il modulo ed evitare errori di digitazione.

* AEM Forms fornisce un servizio di precompilazione per leggere i dati da un file XML di dati predefinito e precompilare i campi di un modulo adattivo con il contenuto del file XML precompilato.
* L’XML dei dati di precompilazione deve essere conforme allo schema del modello di modulo associato al modulo adattivo.
* Includi `afBoundedData` e `afUnBoundedData` sezioni nel file XML precompilato per precompilare sia i campi associati che quelli non associati in un modulo adattivo.

* Per i moduli adattivi basati sul modello di dati del modulo, AEM Forms fornisce il servizio predefinito Modello dati modulo. Il servizio di precompilazione interroga le origini dati per gli oggetti modello dati nel modulo adattivo e i valori dei campi di precompilazione durante il rendering del modulo.
* Puoi anche utilizzare i protocolli file, crx, service o http per precompilare i moduli adattivi.
* AEM Forms supporta servizi di precompilazione personalizzati che è possibile collegare come servizio OSGi per precompilare i moduli adattivi.

Per ulteriori informazioni, consulta [Precompilare i campi del modulo adattivo](/help/forms/using/prepopulate-adaptive-form-fields.md).

### Firma e invio di moduli adattivi {#signing-and-submitting-adaptive-forms}

I moduli adattivi richiedono azioni di invio per elaborare i dati specificati dall’utente. Un’azione Invia determina il task eseguito sui dati inviati tramite un modulo adattivo.

* Nei moduli adattivi sono disponibili diverse azioni di invio pronte all’uso. Per ulteriori informazioni, consulta [Configurazione dell’azione Invia](/help/forms/using/configuring-submit-actions.md).
* Se le azioni di invio predefinite non soddisfano il caso d’uso, puoi scrivere un’azione di invio personalizzata. Per ulteriori informazioni, consulta [Scrittura dell’azione di invio personalizzata per i moduli adattivi](/help/forms/using/custom-submit-action-form.md).
* Includi convalide lato server per impedire l’invio di dati non validi.

Puoi utilizzare l’esperienza multi-firma di Adobe Sign nei moduli adattivi. Quando configuri Adobe Sign nei moduli adattivi, tieni presente quanto segue. Per ulteriori informazioni, consulta [Utilizzo di Adobe Sign in un modulo adattivo](/help/forms/using/working-with-adobe-sign.md).

* Il modulo adattivo abilitato per Adobe Sign viene inviato solo dopo che tutti i firmatari hanno firmato il modulo. Forms viene visualizzato nello stato In sospeso fino a quando il modulo non viene firmato da tutti i firmatari.
* Al momento dell’invio, puoi configurare l’esperienza di firma nei moduli o reindirizzare i firmatari a una pagina di firma.
* Configura l’esperienza di firma sequenziale o parallela, a seconda delle necessità.

### Generazione del documento record {#generating-document-of-record}

Un documento di record (DoR) è una versione appiattita di un modulo adattivo che può essere stampata, firmata o archiviata da un PDF.

* A seconda del modello di dati del modulo su cui si basa un modulo adattivo, è possibile configurare un modello per DoR come segue:

   * **Modello di modulo XFA**: utilizza il file XDP associato come modello DoR.
   * **Schema XSD**: utilizza il modello XFA associato che utilizza lo stesso schema XML utilizzato dal modulo adattivo.
   * **Nessuno**: utilizza DoR generato automaticamente.

* Configura intestazione, piè di pagina, immagini, colore, font e così via direttamente dalla scheda Documento di record dell’editor di moduli adattivi.
* Utilizzare `DoRService` per generare il DoR a livello di programmazione.
* Escludere i campi nascosti dal DoR.
* Utilizzare `afAcceptLang` richiedi il parametro per visualizzare il DoR in un&#39;altra lingua.

### Debug e test dei moduli adattivi {#debugging-and-testing-adaptive-forms}

[Plug-in AEM Chrome](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/) è un’estensione del browser per Google Chrome che fornisce strumenti per il debug dei moduli adattivi. Gli autori e gli sviluppatori di moduli possono utilizzare questi strumenti per:

* Identificare i colli di bottiglia e ottimizzare le prestazioni del rendering dei moduli
* Parole chiave di debug ed errori bindRef nel modulo
* Abilitare e configurare i registri
* Debug di regole e script nel modulo
* Esplora e scopri le API guideBridge

Per ulteriori informazioni, consulta [Plug-in di AEM Chrome - Modulo adattivo](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/adaptive-form/).

### Convalida dei moduli adattivi sul server AEM {#validating-adaptive-forms-on-aem-server}

Le convalide lato server sono necessarie per evitare tentativi di aggirare le convalide sul client e possibili compromissioni dell’invio dei dati e violazioni delle regole aziendali. Le convalide lato server vengono eseguite sul server caricando la libreria client richiesta.

* Includi funzioni in una libreria client per la convalida delle espressioni nei moduli adattivi e specifica la libreria client nella finestra di dialogo del contenitore di moduli adattivi. Per ulteriori informazioni, consulta [Riconvalida lato server](/help/forms/using/configuring-submit-actions.md#p-server-side-revalidation-in-adaptive-form-p).
* La convalida lato server convalida il modello del modulo. Si consiglia di creare una libreria client separata per le convalide e non combinarla con altri elementi come lo stile HTML e la manipolazione DOM nella stessa libreria client.

### Localizzazione di moduli adattivi {#localizing-adaptive-forms}

AEM fornisce flussi di lavoro di traduzione che è possibile utilizzare per localizzare i moduli adattivi. Per informazioni, consulta [Utilizzo del flusso di lavoro di traduzione dell’AEM per localizzare i moduli adattivi](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md).

Di seguito sono riportate alcune best practice per la localizzazione dei moduli adattivi:

* Utilizza frammenti di modulo adattivi per elementi comuni a più moduli e localizza frammenti. In questo modo è possibile localizzare un frammento una volta e rifletterlo in tutte le forme in cui viene utilizzato il frammento localizzato.
* Eventuali modifiche, come l’aggiunta di un nuovo componente o l’applicazione di uno script in un modulo localizzato, non vengono localizzate automaticamente. Pertanto, è necessario finalizzare un modulo prima di localizzarlo per evitare più cicli di localizzazione.
* Utilizzare `afAcceptLang` parametro di richiesta per ignorare le impostazioni locali del browser ed eseguire il rendering del modulo nelle impostazioni locali specificate. Ad esempio, il seguente URL viene forzato a eseguire il rendering del modulo nelle impostazioni locali giapponesi, indipendentemente dalle impostazioni locali specificate nell’impostazione del browser:

  `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

* AEM Forms attualmente supporta la localizzazione dei contenuti dei moduli adattivi nelle lingue inglese (en), spagnolo (es), francese (fr), italiano (it), tedesco (de), giapponese (ja), portoghese-brasiliano (pt-BR), cinese (zh-CN), cinese-Taiwan (zh-TW) e coreano (ko-KR). Tuttavia, è possibile aggiungere il supporto per nuove lingue per i moduli adattivi in fase di esecuzione. Per ulteriori informazioni, consulta [Supporto di nuove lingue per la localizzazione di moduli adattivi](/help/forms/using/supporting-new-language-localization.md).

## Prepara progetto Forms per la produzione {#prepare-forms-project-for-production}

### Aggiunta del server di elaborazione dei moduli {#adding-forms-processing-server}

Puoi configurare un’ulteriore istanza del server AEM Forms che si trova dietro il firewall in un’area protetta. Puoi utilizzare questa istanza per:

* **Elaborazione batch**: processi ricorrenti o pianificati in batch con carico elevato. Ad esempio, la stampa di istruzioni, la generazione di corrispondenze e l&#39;utilizzo di servizi per la gestione dei documenti come PDF Generator, Output e Assembler.
* **Memorizzazione dei dati PII**: salva i dati PII sul server di elaborazione. Non è necessario se utilizzi già un provider di archiviazione personalizzato per l’archiviazione dei dati PII.

### Spostamento di un progetto in un altro ambiente {#moving-project-to-another-environment}

Spesso è necessario spostare i progetti AEM da un ambiente all’altro. Di seguito sono riportati alcuni aspetti fondamentali da tenere presenti durante lo spostamento:

* Esegui il backup delle librerie client esistenti, del codice personalizzato e delle configurazioni.
* Distribuire pacchetti e patch di prodotto manualmente e nell&#39;ordine specificato nel nuovo ambiente.
* Distribuisci manualmente pacchetti di codice e bundle specifici del progetto e come pacchetto o bundle separato sul nuovo server AEM.
* (*Solo AEM Forms su JEE*) Distribuire manualmente LCA e DSC sul server di Forms Workflow.
* Utilizzare [Export-Import](/help/forms/using/import-export-forms-templates.md) per spostare le risorse nel nuovo ambiente. Puoi anche configurare l’agente di replica e pubblicare le risorse.
* Quando esegui l’aggiornamento, sostituisci tutte le API e le funzioni obsolete con nuove API e funzioni.

### Configurazione dell’AEM {#configuring-aem}

Di seguito sono riportate alcune best practice per configurare l’AEM in modo da migliorare le prestazioni complessive:

* Abilita la compressione della libreria client HTML per JavaScript e CSS dalla console Felix.
* Memorizza nella cache tutte le librerie client in `/etc.clientlibs/fd` e qualsiasi libreria client aggiuntiva personalizzata in AEM dispatcher per aumentare la reattività e la sicurezza dei moduli pubblicati. Per ulteriori informazioni, consulta [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html).

* Non memorizzare in cache `/content/forms/af/` e `/content/dam/formsanddocuments/*` percorsi. per informazioni dettagliate sulla configurazione della memorizzazione in cache dei moduli adattivi, consulta [Memorizzazione in cache dei moduli adattivi](/help/forms/using/configure-adaptive-forms-cache.md).

* Abilita HTML tramite il modulo di compressione del server web. Per ulteriori informazioni, consulta [Ottimizzazione delle prestazioni del server AEM Forms](/help/forms/using/performance-tuning-aem-forms.md).
* Aumentare le chiamate per configurazione di richiesta per i moduli di grandi dimensioni. Consulta [Ottimizzazione delle prestazioni di moduli complessi e di grandi dimensioni](/help/forms/using/adaptive-forms-best-practices.md#optimizing-performance-of-large-and-complex-forms).
* Crea [pagine di errore personalizzate visualizzate dal gestore degli errori](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/customizing-errorhandler-pages.html).
* Server AEM Forms protetto.

   * Utilizzare `nosamplecontent` modalità di esecuzione per garantire che non siano presenti contenuti di esempio e utenti di esempio distribuiti sul server di produzione. Consulta [Esecuzione di AEM in modalità pronta per la produzione](/help/sites-administering/production-ready.md).

* Mantenere le dimensioni heap su un minimo di 8 GB. Per altre impostazioni, consulta [Ottimizzazione delle prestazioni del server AEM Forms](/help/forms/using/performance-tuning-aem-forms.md).
* Utilizzare le sessioni utente di servizio anziché le sessioni di amministrazione per eseguire attività a livello di servizio. Per ulteriori informazioni, consulta [Autenticazione del servizio](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html).

>[!VIDEO](https://vimeo.com/)

### Configurazione dell’archiviazione esterna per le bozze e i dati dei moduli inviati {#external-storage}

In un ambiente di produzione, si consiglia di non archiviare i dati del modulo inviati nell’archivio AEM. L&#39;implementazione predefinita delle azioni di invio Forms Portal Store, Store Content e Store PDF consente di memorizzare i dati del modulo nell&#39;archivio AEM. Queste azioni di invio sono intese solo a scopo dimostrativo. Inoltre, le funzioni Salva e Riprendi e Salvataggio automatico utilizzano l&#39;archiviazione del portale per impostazione predefinita. Pertanto, considera le seguenti raccomandazioni:

* **Memorizzazione dei dati delle bozze**: se utilizzi la funzione Bozza dei moduli adattivi, devi implementare un’interfaccia personalizzata Service Provide Interface (SPI) per memorizzare i dati in formato bozza in un’archiviazione più sicura, ad esempio nel database. Per ulteriori informazioni, consulta [Esempio per integrare il componente Bozze e invii con il database](/help/forms/using/integrate-draft-submission-database.md).

* **Memorizzazione dei dati di invio**: se utilizzi l’archivio di invio del portale dei moduli, devi implementare un SPI personalizzato per memorizzare i dati di invio in un database. Consulta [Esempio per integrare il componente Bozze e invii con il database](/help/forms/using/integrate-draft-submission-database.md) per un esempio di integrazione.

  È inoltre possibile scrivere un&#39;azione di invio personalizzata che memorizzi i dati del modulo e l&#39;allegato in un archivio protetto. Consulta [Scrittura dell’azione di invio personalizzata per i moduli adattivi](/help/forms/using/custom-submit-action-form.md) per ulteriori informazioni.

* **Lunghezza ID bozza**: quando salvi un modulo adattivo come bozza, viene generato un ID bozza per identificare la bozza in modo univoco. Il valore minimo per la lunghezza del campo ID bozza è di 26 caratteri. L&#39;Adobe consiglia di impostare la lunghezza dell&#39;ID bozza su 26 o più caratteri.

### Trattamento di informazioni personali {#handling-personally-identifiable-information}

Una delle sfide principali per le organizzazioni è la gestione dei dati personali (PII, personally identifiable). Di seguito sono riportate alcune best practice per la gestione di tali dati:

* Utilizza un archivio esterno sicuro come il database per memorizzare i dati delle bozze e dei moduli inviati. Consulta [Configurazione dell’archiviazione esterna per le bozze e i dati dei moduli inviati](/help/forms/using/adaptive-forms-best-practices.md#external-storage).
* Utilizza il componente modulo Termini e condizioni per ottenere il consenso esplicito dell’utente prima di abilitare il salvataggio automatico. In questo caso, abilita il salvataggio automatico solo quando l’utente accetta le condizioni nel componente Termini e condizioni.


