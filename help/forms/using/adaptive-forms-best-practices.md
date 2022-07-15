---
title: 'Procedure consigliate per l''utilizzo dei moduli adattivi '
seo-title: Best practices for working with adaptive forms
description: Illustra le best practice per la configurazione di un progetto AEM Forms, lo sviluppo di moduli adattivi e l’ottimizzazione delle prestazioni per il sistema AEM Forms.
seo-description: Explains best practices for setting up an AEM Forms project, developing adaptive forms, and optimizing the performance for AEM Forms system.
uuid: ed95fc64-56b3-4ea1-a5ba-2e96953fca56
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 43c431e4-5286-4f4e-b94f-5a7451c4a22c
feature: Adaptive Forms
exl-id: 5c75ce70-983e-4431-a13f-2c4c219e8dde
source-git-commit: 0f1724cbb7ef4fec366fb8b63511a981b47b5429
workflow-type: tm+mt
source-wordcount: '4322'
ht-degree: 0%

---

# Procedure consigliate per l&#39;utilizzo dei moduli adattivi  {#best-practices-for-working-with-adaptive-forms}

## Panoramica {#overview}

I moduli di Adobe Experience Manager (AEM) consentono di trasformare transazioni complesse in esperienze digitali semplici e accattivanti. Tuttavia, richiede uno sforzo concertato per implementare, costruire, eseguire e mantenere un ecosistema AEM Forms efficiente e produttivo.

Questo documento fornisce linee guida e consigli di cui possono trarre vantaggio gli amministratori, gli autori e gli sviluppatori di moduli quando si lavora con AEM Forms, in particolare il componente Moduli adattivi. Descrive le best practice, dalla configurazione di un progetto di sviluppo di moduli alla configurazione, personalizzazione, authoring e ottimizzazione di AEM Forms. Queste best practice contribuiscono collettivamente alle prestazioni complessive dell’ecosistema AEM Forms.

Inoltre, ecco alcune letture consigliate per le best practice generali AEM:

* [Best practice: Distribuzione e manutenzione AEM](/help/sites-deploying/best-practices.md)
* [Best practice: Creazione di contenuti](/help/sites-authoring/best-practices.md)
* [Best practice: Amministrazione AEM](/help/sites-administering/administer-best-practices.md)
* [Best practice: Sviluppo di soluzioni](/help/sites-developing/best-practices.md)

## Configurazione e configurazione di AEM Forms {#set-up-and-configure-aem-forms}

### Impostazione del progetto di sviluppo dei moduli {#setting-up-forms-development-project}

Una struttura di progetto semplificata e standardizzata può ridurre notevolmente gli sforzi di sviluppo e manutenzione. Apache Maven è uno strumento open source consigliato per la creazione di progetti AEM.

* Usa Apache Maven `aem-project-archetype` per creare e gestire la struttura del progetto AEM. Crea la struttura e i modelli consigliati per il progetto AEM. Inoltre, fornisce automazione della creazione e sistemi di controllo delle modifiche per aiutare a gestire il progetto.

   * Usa il Maven `archetype:generate` per generare la struttura iniziale.
   * Usa Maven `eclipse:eclipse` per generare i file del progetto eclipse e importare il progetto in eclipse.

Per ulteriori informazioni, consulta [Come creare progetti AEM utilizzando Apache Maven](/help/sites-developing/ht-projects-maven.md).

* Lo strumento FileVault o VLT ti aiuta a mappare il contenuto di un&#39;istanza CRX o AEM al tuo file system. Fornisce operazioni di gestione del controllo delle modifiche, ad esempio il check-in e il check-out del contenuto del progetto AEM. Vedi [Come utilizzare lo strumento VLT](/help/sites-developing/ht-vlttool.md).

* Se utilizzi un ambiente di sviluppo integrato con Eclipse, puoi utilizzare AEM strumenti per sviluppatori per un’integrazione diretta di Eclipse IDE con istanze AEM per creare applicazioni AEM. Per maggiori dettagli, vedi [AEM strumenti per sviluppatori per Eclipse](/help/sites-developing/aem-eclipse.md).

* Non memorizzare alcun contenuto o apportare modifiche nella cartella /libs. Crea sovrapposizioni nelle cartelle /app per estendere o sovrascrivere le funzionalità predefinite.

* Quando crei pacchetti per spostare il contenuto, assicurati che i percorsi dei filtri dei pacchetti siano corretti e che vengano menzionati solo i percorsi richiesti.

* Non memorizzare alcun contenuto o apportare modifiche nella cartella /libs. Crea sovrapposizioni nelle cartelle /app per estendere o sovrascrivere le funzionalità predefinite.

* Definire le dipendenze corrette per i pacchetti per forzare un ordine/sequenza di installazione predeterminato.

* Non creare alcun nodo di riferimento in /libs o /apps.

### Pianificazione dell’ambiente di authoring {#planning-for-authoring-environment}

Una volta impostato il progetto AEM, definisci la strategia per la creazione e la personalizzazione di modelli e componenti per moduli adattivi.

* Un modello di modulo adattivo è una pagina AEM specializzata che definisce la struttura e le informazioni a piè di pagina dell’intestazione di un modulo adattivo. Un modello dispone di layout, stili e struttura di base preconfigurati per un modulo adattivo. AEM Forms fornisce modelli e componenti predefiniti che è possibile utilizzare per creare moduli adattivi. Tuttavia, puoi creare modelli e componenti personalizzati in base alle tue esigenze. È consigliabile raccogliere i requisiti per modelli e componenti aggiuntivi necessari nei moduli adattivi. Per maggiori dettagli, vedi [Personalizzazione di moduli e componenti adattivi](/help/forms/using/adaptive-forms-best-practices.md#customize-components).
* AEM Forms consente di creare moduli adattivi basati sui seguenti modelli di modulo. I modelli di modulo fungono da interfaccia per lo scambio di dati tra un modulo e un sistema AEM e forniscono una struttura basata su XML per lo scorrimento dei dati all’interno e all’esterno di un modulo adattivo. Inoltre, i modelli di modulo impongono regole e vincoli ai moduli adattivi sotto forma di vincoli di schema e XFA.

   * **Nessuno**: I moduli adattivi creati con questa opzione non utilizzano modelli di modulo. I dati XML generati da tali moduli hanno una struttura piatta con campi e valori corrispondenti.
   * **Schema XML o JSON**: Gli schemi XML e JSON rappresentano la struttura in cui i dati vengono prodotti o utilizzati dal sistema back-end della tua organizzazione. È possibile associare uno schema a un modulo adattivo e utilizzarne gli elementi per aggiungere contenuto dinamico al modulo adattivo. Gli elementi dello schema sono disponibili nella scheda Oggetto modello dati del browser del contenuto per la creazione di moduli adattivi. È possibile trascinare gli elementi dello schema per creare il modulo.
   * **Modello di modulo XFA**: Si tratta di un modello di modulo ideale per gli investimenti in moduli HTML5 basati su XFA. Fornisce un modo diretto per convertire i moduli basati su XFA in moduli adattivi. Eventuali regole XFA esistenti vengono mantenute nei moduli adattivi associati. I moduli adattivi risultanti supportano i costrutti XFA, ad esempio convalide, eventi, proprietà e pattern.
   * **Modello dati modulo**: Si tratta di un modello di modulo preferito se si desidera integrare i sistemi di backend come database, servizi web e profilo utente AEM per precompilare moduli adattivi e riscrivere i dati del modulo inviati nei sistemi di back-end. Un editor per modelli di dati per moduli consente di definire e configurare entità e servizi in un modello di dati modulo che può essere utilizzato per creare moduli adattivi. Per ulteriori informazioni, consulta [Integrazione dei dati di AEM Forms](/help/forms/using/data-integration.md).

È importante scegliere attentamente il modello dati che non solo soddisfa le tue esigenze ma estende gli investimenti esistenti in risorse XFA e XSD, se presenti. Si consiglia di utilizzare il modello XSD per creare modelli di modulo, in quanto l’XML generato contiene dati in base a XPATH definito dallo schema. L’utilizzo di XSD Model come scelta predefinita per Form Data Model è utile anche perché consente di separare la struttura del modulo dal sistema back-end che elabora e consuma i dati e migliora le prestazioni del modulo a causa della mappatura da uno a un campo del modulo. Inoltre, BindRef del campo può essere reso XPATH del suo valore di dati in XML.

Per ulteriori informazioni, consulta [Creare un modulo adattivo](/help/forms/using/creating-adaptive-form.md).

* Esistono alcune sezioni comuni nei moduli adattivi. Puoi identificarli e definire una strategia per promuovere il riutilizzo dei contenuti. I moduli adattivi consentono di creare frammenti autonomi e riutilizzarli tra i diversi moduli. È inoltre possibile salvare un pannello in un modulo adattivo come frammento. Qualsiasi modifica apportata a un frammento si riflette in tutti i moduli associati. Consente di ridurre i tempi di creazione e assicura la coerenza tra i vari moduli. Inoltre, l’utilizzo dei frammenti rende i moduli adattivi leggeri e consente di migliorare l’esperienza di authoring, in particolare per i moduli di grandi dimensioni. Per ulteriori informazioni, consulta [Frammenti di moduli adattivi](/help/forms/using/adaptive-form-fragments.md).

### Personalizzazione di moduli e componenti adattivi {#customize-components}

* AEM Forms offre modelli di moduli adattivi pronti all’uso che è possibile utilizzare per creare moduli adattivi. Puoi anche creare modelli personalizzati. AEM fornisce modelli statici e modificabili.

   * I modelli statici sono definiti e configurati dagli sviluppatori.
   * I modelli modificabili vengono creati dagli autori che utilizzano l’editor modelli. L’editor modelli ti consente di definire una struttura di base e il contenuto iniziale in un modello. Qualsiasi modifica nel livello struttura viene riflessa in tutti i moduli che utilizzano tale modello. Il contenuto iniziale può includere un tema preconfigurato, un servizio di precompilazione, un’azione di invio e così via. Tuttavia, queste impostazioni possono essere modificate per un modulo utilizzando l’editor di moduli. Per ulteriori informazioni, consulta [Modelli di modulo adattivi](/help/forms/using/template-editor.md).

* Per creare lo stile di un campo o di un’istanza di pannello specifica, utilizza [stile in linea](/help/forms/using/inline-style-adaptive-forms.md). In alternativa, puoi definire una classe in un file CSS e specificare il nome della classe nella proprietà Classe CSS del componente.
* Includi una libreria client in un componente per applicare in modo coerente gli stili nei moduli adattivi o nei frammenti che utilizzano tale componente. Per ulteriori informazioni, consulta [Creare un componente per la pagina di un modulo adattivo](/help/forms/using/custom-adaptive-forms-templates.md).
* Applica gli stili definiti in una libreria client per selezionare i moduli adattivi specificando il percorso della libreria client nel campo Percorso file CSS nelle proprietà del contenitore di moduli adattivi.
* Per creare una libreria client degli stili, puoi configurare il file CSS personalizzato nella clientlib di base dell’Editor tema o nelle proprietà del contenitore modulo .
* I moduli adattivi forniscono layout di pannelli, ad esempio reattivi, a schede, a soffietto e procedure guidate, per controllare il layout dei componenti modulo in un pannello. È possibile creare layout di pannelli personalizzati e renderli disponibili per l’uso da parte degli autori dei moduli. Per ulteriori informazioni, consulta [Creazione di componenti di layout personalizzati per i moduli adattivi](/help/forms/using/custom-layout-components-forms.md).
* È inoltre possibile personalizzare specifici componenti per moduli adattivi, come campi e layout dei pannelli.

   * Utilizza la [Sovrapposizione](/help/sites-developing/overlays.md) funzionalità di AEM per modificare una copia di un componente. Si sconsiglia di modificare i componenti predefiniti.
   * Per personalizzare il layout dei componenti per moduli adattivi predefiniti in /libs, [creare componenti layout personalizzati](/help/forms/using/custom-layout-components-forms.md) oltre al [layout predefiniti](/help/forms/using/layout-capabilities-adaptive-forms.md).
   * Introduci interattività personalizzate creando widget o apparenze personalizzati. Si sconsiglia di modificare i componenti predefiniti. Per ulteriori informazioni, consulta [Struttura dell&#39;aspetto](/help/forms/using/introduction-widgets.md).

* Vedi [Trattamento di informazioni personali identificabili](/help/forms/using/adaptive-forms-best-practices.md#p-handling-personally-identifiable-information-p) per raccomandazioni sulla gestione dei dati PII.

## Creare moduli adattivi {#author-adaptive-forms}

### Utilizzo dell’interfaccia touch per l’authoring {#using-touch-optimized-ui-for-authoring}

* Utilizzare il browser Oggetti nella barra laterale per accedere rapidamente ai campi della gerarchia del modulo. È possibile utilizzare la casella di ricerca per cercare gli oggetti nel modulo o nella struttura degli oggetti per spostarsi da un oggetto all’altro.
* Per visualizzare e modificare le proprietà di un componente nel browser Componenti nella barra laterale, selezionalo e fai clic su ![cmppr-1](assets/cmppr-1.png). Puoi anche fare doppio clic su un componente per visualizzarne le proprietà nel browser delle proprietà.
* Utilizzare le scelte rapide da tastiera per eseguire azioni rapide sui moduli. Vedi [Scelte rapide da tastiera di AEM Forms](/help/forms/using/keyboard-shortcuts.md).

* I componenti per moduli adattivi sono consigliati per l’uso unicamente nelle pagine dei moduli adattivi. I componenti dipendono dalla gerarchia padre. Pertanto, non utilizzarli in una pagina AEM.

Consulta anche le descrizioni dei componenti e le best practice in [Introduzione alla creazione di moduli adattivi](/help/forms/using/introduction-forms-authoring.md).

### Uso delle regole nei moduli adattivi {#using-rules-in-adaptive-forms}

AEM Forms fornisce un [editor di regole](/help/forms/using/rule-editor.md) che consente di creare regole per aggiungere comportamenti dinamici ai componenti dei moduli adattivi. Utilizzando queste regole, puoi valutare le condizioni e attivare azioni sui componenti, ad esempio mostrare o nascondere campi, calcolare valori, modificare dinamicamente l’elenco a discesa e così via.

L’editor di regole fornisce un editor visivo e un editor di codice per la scrittura di regole. Quando scrivi regole utilizzando la modalità editor di codice , tieni presente quanto segue:

* Utilizza nomi significativi e univoci per i campi e i componenti del modulo per evitare possibili conflitti durante la scrittura delle regole.
* Utilizzo `this` di un componente per fare riferimento a se stesso in un&#39;espressione di una regola. La regola rimane valida anche se il nome del componente cambia. Esempio, `field1.valueCommit script: this.value > 10`.

* Utilizzare i nomi dei componenti quando si fa riferimento ad altri componenti del modulo. Utilizza la `value` per recuperare il valore di un campo o di un componente. Esempio, `field1.value`.

* Per evitare conflitti, fai riferimento ai componenti in base a una gerarchia univoca relativa. Esempio, `parentName.fieldName`.

* Quando si gestiscono regole complesse o comunemente utilizzate, è consigliabile scrivere regole di business logic come funzioni in una libreria client separata che è possibile specificare e riutilizzare nei moduli adattivi. La libreria client deve essere una libreria indipendente e non deve avere dipendenze esterne, ad eccezione di jQuery e Underscore.js. Puoi inoltre utilizzare la libreria client per applicare [riconvalida lato server](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form) dei dati del modulo inviati.
* I moduli adattivi forniscono un set di API che è possibile utilizzare per comunicare ed eseguire azioni sui moduli adattivi. Alcune delle API chiave sono le seguenti. Per ulteriori informazioni, consulta [Riferimento API della libreria JavaScript per Forms adattivo](https://adobe.com/go/learn_aemforms_documentation_63).

   * `guideBridge.reset()`: Reimposta un modulo.
   * `guideBridge.submit()`: Invia un modulo.
   * `guideBridge.setFocus(somExp, focusOption, runCompletionExp)`: Imposta lo stato attivo su un campo.
   * `guideBridge.validate(errorList, somExpression, focus)`: Convalida un modulo.
   * `guideBridge.getDataXML(options)`: Ottiene i dati del modulo come XML.
   * `guideBridge.resolveNode(somExpression)`: Ottiene un oggetto modulo.
   * `guideBridge.setProperty(somList, propertyName, valueList)`: Imposta la proprietà di un oggetto modulo.
   * Inoltre, è possibile utilizzare le seguenti proprietà del campo:

      * `field.value` per modificare il valore di un campo.
      * `field.enabled` per abilitare/disabilitare un campo.
      * `field.visible` per modificare la visibilità di un campo.

* Gli autori di moduli adattivi potrebbero dover scrivere codice JavaScript per creare logica di business in un modulo. Anche se JavaScript è potente ed efficace, è probabile che possa compromettere le aspettative di sicurezza. Pertanto, è necessario assicurarsi che l’autore del modulo sia una persona affidabile e che siano disponibili processi per la revisione e l’approvazione del codice JavaScript prima che un modulo venga messo in produzione. L’amministratore può limitare l’accesso all’editor di regole ai gruppi di utenti in base al loro ruolo o funzione. Vedi [Concedere l’accesso all’editor di regole a specifici gruppi di utenti](/help/forms/using/rule-editor-access-user-groups.md).
* È possibile utilizzare le espressioni nelle regole per rendere dinamici i moduli adattivi. Tutte le espressioni sono espressioni JavaScript valide e utilizzano API modello di script per moduli adattivi. Queste espressioni restituiscono valori di determinati tipi. Per ulteriori informazioni sulle espressioni e sulle best practice relative, consulta [Espressioni di moduli adattivi](/help/forms/using/adaptive-form-expressions.md).

### Utilizzo dei temi {#working-with-themes}

L’opzione Adattivo per i temi consente di creare stili riutilizzabili che possono essere applicati ai diversi moduli per un aspetto e uno stile coerenti. Si consiglia di utilizzare i temi per definire lo stile dei componenti e dei pannelli dei moduli. Di seguito sono riportate alcune best practice relative ai temi:

* Utilizza la libreria risorse per applicare rapidamente stili di testo, sfondo e immagini. Quando si aggiunge uno stile nella libreria delle risorse, questo è disponibile per altri temi e nella modalità stile dell’editor moduli.
* Applicare impostazioni globali come il font e lo sfondo della pagina utilizzando il selettore a livello di pagina.
* Utilizza le librerie client per importare stili esistenti o avanzati nei tuoi temi.
* È possibile sostituire lo stile per campi, pannelli o pulsanti specifici in un livello di stile modulo.
* Se un tema non soddisfa i requisiti di stile, è possibile utilizzare classi predefinite quali guideFieldNode, guideFieldLabel, guideFieldWidget e guidePanelNode per applicare stili comuni ai moduli.

Per ulteriori informazioni, consulta [Temi](/help/forms/using/themes.md).

### Ottimizzazione delle prestazioni di moduli grandi e complessi {#optimizing-performance-of-large-and-complex-forms}

Gli autori e gli utenti finali dei moduli in genere riscontrano problemi di prestazioni durante il caricamento di moduli di grandi dimensioni in modalità di authoring o in fase di runtime. Con l’aumentare del numero di oggetti (campi e pannelli) nel modulo, l’esperienza di authoring e runtime inizia a peggiorare. Inoltre, impedisce a più autori di collaborare e creare un modulo contemporaneamente.

Per risolvere i problemi di prestazioni con i moduli di grandi dimensioni, considera le seguenti best practice:

* Si consiglia di creare moduli adattivi utilizzando il modello dati del modulo XSD anche durante la conversione di un XFA in modulo adattivo, se possibile.
* Includi solo i campi e i pannelli nei moduli adattivi che acquisiscono informazioni dall’utente. Considera la possibilità di mantenere un contenuto statico minimo o di utilizzare URL per aprirlo in una finestra separata.
* Sebbene ogni modulo sia progettato per uno scopo specifico, nella maggior parte dei moduli sono presenti alcuni segmenti comuni. Ad esempio, dati personali, indirizzo, dati sul lavoro e così via. Crea [frammenti di modulo adattivi](/help/forms/using/adaptive-form-fragments.md) per gli elementi e le sezioni dei moduli comuni e per utilizzarli tra i vari moduli. È inoltre possibile salvare un pannello in un modulo esistente come frammento. Qualsiasi modifica apportata a un frammento si riflette in tutti i moduli adattivi associati. Promuove la creazione collaborativa in quanto più autori possono lavorare contemporaneamente su diversi frammenti che compongono un modulo.

   * Analogamente ai moduli adattivi, è consigliabile che tutti gli script personalizzati e di stile specifici per i frammenti siano definiti nella libreria client tramite la finestra di dialogo del contenitore frammenti. Inoltre, provare a creare frammenti autosufficienti che non dipendono da oggetti esterni.
   * Evitare di utilizzare script con più frammenti. Se al di fuori del frammento è presente un oggetto a cui è necessario fare riferimento, provare a renderlo parte del modulo principale. Se l’oggetto deve ancora trovarsi in un altro frammento, fare riferimento a esso in base al nome nello script.

* Utilizza Salva e riprendi con salvataggio automatico per salvare periodicamente il modulo adattivo e consentire agli utenti di rivederlo in un secondo momento per completare il modulo.
* Configura i frammenti da caricare in modo lento. In fase di runtime, il rendering dei frammenti contrassegnati per il caricamento lento viene eseguito solo quando sono richiesti. Riduce notevolmente il tempo di caricamento dei moduli di grandi dimensioni. È supportato anche nei frammenti con pannelli ripetibili. Per ulteriori informazioni, consulta [Configurare il caricamento lento](/help/forms/using/lazy-loading-adaptive-forms.md).

   * Non configurare il caricamento lento sui frammenti in un layout a griglia reattiva o nel primo pannello.
   * I componenti Allegati file e Termini e condizioni non sono supportati nei frammenti caricati in modo lento.
   * Contrassegna un valore in un pannello caricato lento come Usa valore globale se tale valore viene utilizzato in un’altra parte del modulo in modo che il valore sia disponibile per l’uso quando il pannello contenitore viene scaricato.
   * È consigliabile scrivere regole di visibilità per i frammenti che devono essere visualizzati o nascosti in base a una condizione.
* Imposta il valore della **Numero di chiamate per richiesta** in **Servlet principale Apache Sling** a un numero abbastanza grande. Consente al server Forms di consentire chiamate aggiuntive. La configurazione visualizza un valore predefinito di 1500. Il valore, 1500 chiamate, è per altri componenti di Experience Manager come Sites e Assets. Il valore predefinito impostato per i moduli adattivi è 20000. Se incontri il `too many calls` errore nei registri o impossibile eseguire il rendering del modulo. Per risolvere il problema, provare ad aumentare il valore a un numero elevato. Se il numero di chiamate è superiore a 20000, il modulo è complesso e potrebbe essere necessario un po&#39; di tempo per eseguirne il rendering nel browser. Ciò si verifica solo al primo caricamento del modulo, dopo che il modulo è stato memorizzato nella cache e una volta che il modulo è stato memorizzato nella cache, le prestazioni non subiscono alcun impatto significativo.

### Precompilazione dei moduli adattivi {#prefilling-adaptive-forms}

È possibile precompilare i campi del modulo adattivo con i dati recuperati dal backend per consentire agli utenti di compilare rapidamente il modulo ed evitare errori di digitazione.

* AEM Forms fornisce un servizio di precompilazione per leggere i dati da un file XML di dati predefinito e precompilare i campi di un modulo adattivo con il contenuto del file XML di precompilazione.
* L’XML dei dati di precompilazione deve essere conforme allo schema del modello di modulo associato al modulo adattivo.
* Includi `afBoundedData` e `afUnBoundedData` le sezioni nel file XML di precompilazione consentono di precompilare i campi associati e non associati in un modulo adattivo.

* Per i moduli adattivi basati sul modello di dati del modulo, AEM Forms fornisce il servizio di precompilazione del modello di dati del modulo predefinito. Il servizio di precompilazione esegue una query sulle origini dati per gli oggetti del modello dati nel modulo adattivo e precompila i valori dei campi durante il rendering del modulo.
* È inoltre possibile utilizzare i moduli adattivi di precompilazione di file, crx, service o protocolli http.
* AEM Forms supporta i servizi di precompilazione personalizzati che è possibile collegare come servizio OSGi per precompilare i moduli adattivi.

Per ulteriori informazioni, consulta [Precompilare i campi del modulo adattivo](/help/forms/using/prepopulate-adaptive-form-fields.md).

### Firma e invio di moduli adattivi {#signing-and-submitting-adaptive-forms}

I moduli adattivi richiedono azioni di invio per elaborare i dati specificati dall’utente. Un’azione Invia determina l’attività eseguita sui dati inviati utilizzando un modulo adattivo.

* Nei moduli adattivi sono disponibili diverse azioni di invio pronte all’uso. Per maggiori dettagli, vedi [Configurazione dell’azione Invia](/help/forms/using/configuring-submit-actions.md).
* È possibile scrivere un’azione di invio personalizzata se le azioni di invio predefinite non soddisfano il caso d’uso. Per ulteriori informazioni, consulta [Scrittura di un’azione di invio personalizzata per i moduli adattivi](/help/forms/using/custom-submit-action-form.md).
* Includi convalide lato server per impedire l’invio di dati non validi.

Puoi sfruttare l’esperienza con più firme di Adobe Sign nei moduli adattivi. Quando configuri Adobe Sign nei moduli adattivi, considera quanto segue. Per maggiori dettagli, vedi [Utilizzo di Adobe Sign in un modulo adattivo](/help/forms/using/working-with-adobe-sign.md).

* Il modulo adattivo abilitato per Adobe Sign viene inviato solo dopo che tutti i firmatari hanno firmato il modulo. Forms viene visualizzato in modalità Firma in sospeso finché il modulo non viene firmato da tutti i firmatari.
* È possibile configurare l’esperienza di firma in un modulo o reindirizzare i firmatari a una pagina di firma al momento dell’invio.
* Configura l’esperienza di firma sequenziale o parallela, a seconda delle necessità.

### Generazione del documento di record {#generating-document-of-record}

Un documento di record (DoR) è una versione PDF appiattita di un modulo adattivo che è possibile stampare, firmare o archiviare.

* A seconda del modello dati del modulo su cui si basa un modulo adattivo, è possibile configurare un modello per DoR come segue:

   * **Modello di modulo XFA**: Utilizza il file XDP associato come modello DoR.
   * **Schema XSD**: Utilizza il modello XFA associato che utilizza lo stesso schema XML utilizzato dal modulo adattivo.
   * **Nessuno**: Utilizza il DoR generato automaticamente.

* Configura intestazione, piè di pagina, immagini, colore, font e così via direttamente dalla scheda Documento di record dell’editor di moduli adattivi.
* Utilizzo `DoRService` per generare il DoR a livello di programmazione.
* Escludere i campi nascosti dal DoR.
* Utilizzo `afAcceptLang` richiedere il parametro per visualizzare DoR in un&#39;altra impostazione internazionale.

### Debug e verifica dei moduli adattivi {#debugging-and-testing-adaptive-forms}

[Plug-in di AEM Chrome](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/) è un’estensione del browser per Google Chrome che fornisce strumenti per il debug dei moduli adattivi. Gli autori e gli sviluppatori di moduli possono utilizzare questi strumenti per:

* Identificare i colli di bottiglia e ottimizzare le prestazioni del rendering del modulo
* Debug delle parole chiave ed errori bindRef nel modulo
* Abilitare e configurare i registri
* Debug di regole e script nel modulo
* Scopri e scopri le API di guideBridge

Per ulteriori informazioni, consulta [Plug-in di AEM Chrome - Modulo adattivo](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/adaptive-form/).

### Convalida dei moduli adattivi AEM server {#validating-adaptive-forms-on-aem-server}

Le convalide lato server sono necessarie per evitare qualsiasi tentativo di bypassare le convalide sul client e qualsiasi possibile compromesso tra l’invio di dati e le violazioni delle regole aziendali. Le convalide lato server vengono eseguite sul server caricando la libreria client richiesta.

* Includi funzioni in una libreria client per la convalida delle espressioni nei moduli adattivi e specifica la libreria client nella finestra di dialogo del contenitore di moduli adattivi. Per ulteriori informazioni, consulta [Riconvalida lato server](/help/forms/using/configuring-submit-actions.md#p-server-side-revalidation-in-adaptive-form-p).
* La convalida lato server convalida il modello di modulo. È consigliabile creare una libreria client separata per le convalide e non combinarla con altri elementi, come lo stile di HTML e la manipolazione DOM nella stessa libreria client.

### Localizzazione dei moduli adattivi {#localizing-adaptive-forms}

AEM fornisce flussi di lavoro di traduzione che è possibile utilizzare per localizzare i moduli adattivi. Per informazioni, consulta [Utilizzo AEM flusso di lavoro di traduzione per localizzare i moduli adattivi](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md).

Di seguito sono riportate alcune best practice per la localizzazione di moduli adattivi:

* Utilizzare frammenti di modulo adattivo per elementi comuni nei moduli e localizzare i frammenti. Il frammento viene localizzato una volta e viene riflesso in tutti i moduli in cui viene utilizzato il frammento localizzato.
* Eventuali modifiche, ad esempio l’aggiunta di un nuovo componente o l’applicazione di uno script in un modulo localizzato, non vengono localizzate automaticamente. Pertanto, è necessario finalizzare un modulo prima di localizzarlo per evitare più cicli di localizzazione.
* Utilizzo `afAcceptLang` richiede un parametro per ignorare le impostazioni internazionali del browser ed eseguire il rendering del modulo nelle impostazioni internazionali specificate. Ad esempio, con il seguente URL verrà eseguito il rendering del modulo nelle impostazioni internazionali giapponesi, indipendentemente dalle impostazioni internazionali specificate nell’impostazione del browser:

   `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

* AEM Forms supporta attualmente la localizzazione di contenuti di moduli adattivi nelle impostazioni internazionali inglese (en), spagnolo (es), francese (fr), italiano (it), tedesco (de), giapponese (ja), portoghese-brasiliano (pt-BR), cinese (zh-CN), cinese-Taiwan (zh-TW) e coreano (ko-KR). Tuttavia, è possibile aggiungere il supporto per nuove impostazioni internazionali per i moduli adattivi in fase di esecuzione. Per ulteriori informazioni, consulta [Supporto di nuove impostazioni internazionali per la localizzazione di moduli adattivi](/help/forms/using/supporting-new-language-localization.md).

## Preparare un progetto di moduli per la produzione {#prepare-forms-project-for-production}

### Aggiunta di un server di elaborazione moduli {#adding-forms-processing-server}

È possibile configurare un&#39;istanza aggiuntiva del server AEM Forms che si trova dietro il firewall in un&#39;area protetta. Puoi utilizzare questa istanza per:

* **Elaborazione batch**: lavori ricorrenti o pianificati in batch con carico elevato. Ad esempio, la stampa di istruzioni, la generazione di corrispondenze e l’utilizzo di servizi per documenti quali PDF Generator, Output e Assembler.
* **Memorizzazione dei dati PII**: Salva i dati PII sul server di elaborazione. Non è necessario se si utilizza già un provider di archiviazione personalizzato per la memorizzazione dei dati PII.

### Spostamento di un progetto in un altro ambiente {#moving-project-to-another-environment}

Spesso è necessario spostare i progetti AEM da un ambiente all’altro. Alcune delle cose chiave da ricordare quando ci si sposta sono le seguenti:

* Esegui il backup delle librerie client, del codice personalizzato e delle configurazioni esistenti.
* Distribuisci pacchetti di prodotti e patch manualmente e nell’ordine specificato nel nuovo ambiente.
* Distribuisci manualmente pacchetti e bundle di codice specifici per il progetto e come pacchetto o bundle separato sul nuovo server AEM.
* (*AEM Forms solo su JEE*) Distribuire manualmente LCA e DSC sul server di Forms Workflow.
* Utilizzo [Export-Import](/help/forms/using/import-export-forms-templates.md) per spostare le risorse nel nuovo ambiente. Puoi anche configurare l’agente di replica e pubblicare le risorse.
* Quando esegui l’aggiornamento, sostituisci tutte le API e funzionalità obsolete con nuove API e funzionalità.

### Configurazione di AEM {#configuring-aem}

Di seguito sono riportate alcune best practice per configurare AEM per migliorare le prestazioni complessive:

* Abilita la compressione della libreria client HTML per JavaScript e CSS dalla console Felix.
* Memorizza in cache tutte le librerie client in `/etc.clientlibs/fd` ed eventuali librerie client personalizzate aggiuntive sul dispatcher AEM per aumentare la reattività e la sicurezza dei moduli pubblicati. Per ulteriori informazioni, consulta [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html).

* Non memorizzare in cache `/content/forms/af/` e `/content/dam/formsanddocuments/*` percorsi. per informazioni dettagliate sulla configurazione della memorizzazione in cache dei moduli adattivi, consulta [Memorizzazione in cache dei moduli adattivi](/help/forms/using/configure-adaptive-forms-cache.md).

* Abilita HTML tramite il modulo di compressione del server web. Per ulteriori informazioni, consulta [Ottimizzazione delle prestazioni del server AEM Forms](/help/forms/using/performance-tuning-aem-forms.md).
* Aumenta le chiamate per configurazione richiesta per i moduli di grandi dimensioni. Vedi [Ottimizzazione delle prestazioni di moduli grandi e complessi](/help/forms/using/adaptive-forms-best-practices.md#optimizing-performance-of-large-and-complex-forms).
* Crea [pagine di errore personalizzate visualizzate dal gestore di errori](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/customizing-errorhandler-pages.html).
* Server AEM Forms protetto.

   * Utilizzo `nosamplecontent` modalità di esecuzione per garantire che non vi siano utenti di esempio e di esempio distribuiti sul server di produzione. Vedi [Esecuzione di AEM in modalità pronta per la produzione](/help/sites-administering/production-ready.md).

* Mantenere la dimensione dell&#39;heap ad un minimo di 8 GB. Per altre impostazioni, vedi [Ottimizzazione delle prestazioni del server AEM Forms](/help/forms/using/performance-tuning-aem-forms.md).
* Utilizza le sessioni utente del servizio invece delle sessioni di amministrazione per eseguire attività a livello di servizio. Per ulteriori informazioni, consulta [Autenticazione del servizio](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html).

>[!VIDEO](https://vimeo.com/)

### Configurazione dell’archiviazione esterna per le bozze e i dati dei moduli inviati {#external-storage}

In un ambiente di produzione, si consiglia di non archiviare i dati del modulo inviati in AEM archivio. L’implementazione predefinita delle azioni di invio Forms Portal Store, Store Content e Store PDF memorizza i dati del modulo nell’archivio AEM. Queste azioni di invio sono intese solo a scopo dimostrativo. Inoltre, le funzioni Salva e Riprendi e Salva automaticamente utilizzano l&#39;archiviazione del portale per impostazione predefinita. Considera pertanto le seguenti raccomandazioni:

* **Memorizzazione dei dati bozze**: Se si utilizza la funzione Bozza di moduli adattivi, è necessario implementare un&#39;interfaccia SPI (Service Provider Interface) personalizzata per memorizzare i dati bozza in un archivio più sicuro, come il database. Per ulteriori informazioni, consulta [Esempio per l&#39;integrazione del componente bozze e invii con il database](/help/forms/using/integrate-draft-submission-database.md).

* **Memorizzazione dei dati di invio**: Se si utilizza Form Portal Submit Store, è necessario implementare un SPI personalizzato per memorizzare i dati di invio in un database. Vedi [Esempio per l&#39;integrazione del componente bozze e invii con il database](/help/forms/using/integrate-draft-submission-database.md) per un’integrazione di esempio.

   È inoltre possibile scrivere un’azione di invio personalizzata che memorizza i dati del modulo e l’allegato in un archivio protetto. Vedi [Scrittura di un’azione di invio personalizzata per i moduli adattivi](/help/forms/using/custom-submit-action-form.md) per ulteriori informazioni.

* **Lunghezza bozza ID**: Quando salvi un modulo adattivo come bozza, viene generato un ID bozza per identificare in modo univoco la bozza. Il valore minimo per la lunghezza della bozza del campo ID è di 26 caratteri. Adobe consiglia di impostare la lunghezza della bozza dell&#39;ID su 26 o più caratteri.

### Trattamento di informazioni personali identificabili {#handling-personally-identifiable-information}

Una delle principali sfide per le organizzazioni è come gestire i dati personali identificabili (PII). Di seguito sono riportate alcune best practice per gestire questi dati:

* Utilizzare un archivio sicuro ed esterno come database per memorizzare i dati dai moduli bozza e inviati. Vedi [Configurazione dell’archiviazione esterna per le bozze e i dati dei moduli inviati](/help/forms/using/adaptive-forms-best-practices.md#external-storage).
* Utilizza il componente Modulo Termini e Condizioni per ottenere il consenso esplicito dell’utente prima di abilitare il salvataggio automatico. In questo caso, abilita il salvataggio automatico solo quando l’utente accetta le condizioni nel componente Termini e condizioni.
