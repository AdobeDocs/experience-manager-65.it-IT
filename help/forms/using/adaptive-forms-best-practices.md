---
title: 'Procedure consigliate per l''utilizzo dei moduli adattivi '
seo-title: 'Procedure consigliate per l''utilizzo dei moduli adattivi '
description: Illustra le best practice per configurare un progetto AEM Forms , sviluppare moduli adattivi e ottimizzare le prestazioni  sistema AEM Forms.
seo-description: Illustra le best practice per configurare un progetto AEM Forms , sviluppare moduli adattivi e ottimizzare le prestazioni  sistema AEM Forms.
uuid: ed95fc64-56b3-4ea1-a5ba-2e96953fca56
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 43c431e4-5286-4f4e-b94f-5a7451c4a22c
translation-type: tm+mt
source-git-commit: 615b0db6da0986d7a74c42ec0d0e14bad7ede168
workflow-type: tm+mt
source-wordcount: '4296'
ht-degree: 0%

---


# Procedure consigliate per l&#39;utilizzo dei moduli adattivi{#best-practices-for-working-with-adaptive-forms} 

## Panoramica {#overview}

I moduli Adobe Experience Manager (AEM) consentono di trasformare transazioni complesse in esperienze digitali semplici e coinvolgenti. Tuttavia, richiede uno sforzo concertato per implementare, costruire, eseguire e mantenere un ecosistema AEM Forms efficiente e produttivo .

Questo documento contiene le linee guida e le raccomandazioni che gli amministratori, gli autori e gli sviluppatori di moduli possono trarre vantaggio dall&#39;utilizzo di  AEM Forms, in particolare dei componenti per moduli adattivi. Vengono illustrate le procedure ottimali, dalla configurazione di un progetto di sviluppo di moduli alla configurazione, personalizzazione, authoring e ottimizzazione  AEM Forms. Queste best practice collettivamente contribuiscono alle prestazioni complessive dell&#39;ecosistema  AEM Forms.

Inoltre, di seguito sono riportate alcune letture consigliate per le best practice generali AEM:

* [Best practice: Implementazione e manutenzione AEM](/help/sites-deploying/best-practices.md)
* [Best practice: Creazione di contenuti](/help/sites-authoring/best-practices.md)
* [Best practice: AEM di amministrazione](/help/sites-administering/administer-best-practices.md)
* [Best practice: Sviluppo di soluzioni](/help/sites-developing/best-practices.md)

## Configurare e configurare  AEM Forms {#set-up-and-configure-aem-forms}

### Impostazione del progetto di sviluppo dei moduli {#setting-up-forms-development-project}

Una struttura di progetto semplificata e standardizzata può ridurre notevolmente gli sforzi di sviluppo e manutenzione. Apache Maven è uno strumento open source consigliato per la costruzione AEM progetti.

* Utilizzate Apache Maven `aem-project-archetype` per creare e gestire la struttura per AEM progetto. Crea struttura e modelli consigliati per il progetto AEM. Inoltre, fornisce l&#39;automazione delle build e i sistemi di controllo delle modifiche per aiutare a gestire il progetto.

   * Utilizzate il comando maven `archetype:generate` per generare la struttura iniziale.
   * Utilizzate il comando maven `eclipse:eclipse` per generare i file del progetto eclissi e importare il progetto in eclissi.

Per ulteriori informazioni, vedere [Come creare progetti AEM con Apache Maven](/help/sites-developing/ht-projects-maven.md).

* Lo strumento FileVault o VLT consente di mappare il contenuto di un&#39;istanza CRX o AEM al file system. Fornisce operazioni di gestione del controllo delle modifiche, ad esempio il check-in e il check-out del contenuto del progetto AEM. Vedere [Come utilizzare lo strumento VLT](/help/sites-developing/ht-vlttool.md).

* Se si utilizza un ambiente di sviluppo integrato con Eclipse, è possibile utilizzare AEM strumenti per sviluppatori per integrare perfettamente Eclipse IDE con AEM istanze per creare AEM applicazioni. Per informazioni dettagliate, consultate [AEM strumenti di sviluppo per Eclipse](/help/sites-developing/aem-eclipse.md).

* Non archiviate alcun contenuto o apportate modifiche nella cartella /libs. Create sovrapposizioni nelle cartelle /app per estendere o sovrascrivere le funzionalità predefinite.

* Quando create pacchetti per spostare il contenuto, accertatevi che i percorsi dei filtri del pacchetto siano corretti e che vengano menzionati solo i percorsi richiesti.

* Non archiviate alcun contenuto o apportate modifiche nella cartella /libs. Create sovrapposizioni nelle cartelle /app per estendere o sovrascrivere le funzionalità predefinite.

* Definite le dipendenze corrette per i pacchetti per imporre un ordine/sequenza di installazione predeterminata.

* Non creare alcun nodo di riferimento in /libs o /apps.

### Pianificazione dell&#39;ambiente di authoring {#planning-for-authoring-environment}

Una volta configurato il progetto AEM, definire la strategia per la creazione e la personalizzazione di modelli e componenti per moduli adattivi.

* Un modello di modulo adattivo è una pagina AEM specializzata che definisce la struttura e le informazioni a piè di pagina dell&#39;intestazione di un modulo adattivo. Un modello dispone di layout, stili e struttura di base preconfigurati per un modulo adattivo.  AEM Forms fornisce modelli e componenti predefiniti utilizzabili per la creazione di moduli adattivi. Tuttavia, potete creare modelli e componenti personalizzati in base alle vostre esigenze. È consigliabile raccogliere i requisiti per i modelli e i componenti aggiuntivi necessari nei moduli adattivi. Per informazioni dettagliate, vedere [Personalizzazione di moduli e componenti adattivi](/help/forms/using/adaptive-forms-best-practices.md#customize-components).
*  AEM Forms consente di creare moduli adattivi basati sui seguenti modelli di modulo. I modelli di modulo fungono da interfaccia per lo scambio di dati tra un modulo e un sistema AEM e forniscono una struttura basata su XML per il flusso di dati all&#39;interno e all&#39;esterno di un modulo adattivo. Inoltre, i modelli di modulo impongono regole e vincoli ai moduli adattivi sotto forma di vincoli di schema e XFA.

   * **Nessuno**: I moduli adattivi creati con questa opzione non utilizzano alcun modello di modulo. I dati XML generati da tali moduli hanno una struttura semplice con campi e valori corrispondenti.
   * **Schema** XML o JSON: Gli schemi XML e JSON rappresentano la struttura in cui i dati vengono prodotti o consumati dal sistema back-end della tua organizzazione. È possibile associare uno schema a un modulo adattivo e utilizzarne gli elementi per aggiungere contenuto dinamico al modulo adattivo. Gli elementi dello schema sono disponibili nella scheda Oggetto modello dati del browser del contenuto per la creazione di moduli adattivi. È possibile trascinare gli elementi dello schema per creare il modulo.
   * **Modello** di modulo XFA: Si tratta di un modello di modulo ideale per gli investimenti in moduli HTML5 basati su XFA. Fornisce un modo diretto per convertire i moduli basati su XFA in moduli adattivi. Eventuali regole XFA esistenti vengono conservate nei moduli adattivi associati. I moduli adattivi risultanti supportano i costrutti XFA, ad esempio convalide, eventi, proprietà e pattern.
   * **Modello** dati modulo: Si tratta di un modello di modulo preferenziale se si desidera integrare i sistemi di back-end come database, servizi Web e AEM profilo utente per precompilare i moduli adattivi e riscrivere i dati dei moduli inviati nei sistemi di back-end. L&#39;Editor modello dati modulo consente di definire e configurare entità e servizi in un modello dati modulo che è possibile utilizzare per creare moduli adattivi. Per ulteriori informazioni, vedere [ Integrazione dei dati AEM Forms](/help/forms/using/data-integration.md).

È importante scegliere con attenzione il modello di dati che non solo soddisfa le vostre esigenze ma che estenda gli investimenti esistenti in risorse XFA e XSD, se presenti. È consigliabile utilizzare il modello XSD per creare modelli di modulo, in quanto l&#39;XML generato contiene dati in base al percorso XPATH definito dallo schema. L&#39;utilizzo del modello XSD come scelta predefinita per il modello dati del modulo è utile anche perché consente di separare la struttura del modulo dal sistema back-end che elabora e consuma i dati e migliora le prestazioni del modulo grazie a una mappatura da uno a un campo del modulo. Inoltre, BindRef del campo può essere impostato come XPATH del valore dei dati in XML.

Per ulteriori informazioni, vedere [Creare un modulo adattivo](/help/forms/using/creating-adaptive-form.md).

* Esistono alcune sezioni comuni tra i moduli adattivi. Potete identificarli e definire una strategia per promuovere il riutilizzo dei contenuti. I moduli adattivi consentono di creare frammenti autonomi e di riutilizzarli in più moduli. È inoltre possibile salvare un pannello in un modulo adattivo come frammento. Qualsiasi modifica apportata a un frammento si riflette in tutti i moduli associati. Questo consente di ridurre i tempi di authoring e assicura la coerenza tra i diversi moduli. Inoltre, l&#39;uso dei frammenti rende i moduli adattivi leggeri e offre una migliore esperienza di authoring, in particolare per i moduli di grandi dimensioni. Per ulteriori informazioni, vedere [Frammenti modulo adattivi](/help/forms/using/adaptive-form-fragments.md).

### Personalizzazione di moduli e componenti adattivi {#customize-components}

*  AEM Forms offre modelli di modulo adattivo predefiniti che è possibile utilizzare per creare moduli adattivi. Potete anche creare dei modelli personalizzati. AEM fornisce modelli statici e modificabili.

   * I modelli statici sono definiti e configurati dagli sviluppatori.
   * I modelli modificabili vengono creati dagli autori che utilizzano l’editor modelli. L’editor modelli consente di definire una struttura di base e il contenuto iniziale in un modello. Qualsiasi modifica apportata al livello struttura si riflette in tutti i moduli che utilizzano tale modello. Il contenuto iniziale può includere tema preconfigurato, servizio di precompilazione, azione di invio e così via. Tuttavia, queste impostazioni possono essere modificate per un modulo utilizzando l&#39;editor del modulo. Per ulteriori informazioni, vedere [Modelli di moduli adattivi](/help/forms/using/template-editor.md).

* Per creare lo stile di un&#39;istanza di campo o pannello specifica, utilizzate lo stile in linea [](/help/forms/using/inline-style-adaptive-forms.md). In alternativa, potete definire una classe in un file CSS e specificare il nome della classe nella proprietà Classe CSS del componente.
* Includere una libreria client in un componente per applicare in modo coerente gli stili ai moduli adattivi o ai frammenti che utilizzano tale componente. Per ulteriori informazioni, vedere [Creare un componente per pagina di modulo adattivo](/help/forms/using/custom-adaptive-forms-templates.md).
* Applicare gli stili definiti in una libreria client per selezionare i moduli adattivi specificando il percorso della libreria client nel campo del percorso del file CSS nelle proprietà del contenitore di moduli adattivi.
* Per creare una libreria client degli stili, è possibile configurare il file CSS personalizzato nella clientlib di base dell&#39;Editor tema o nelle proprietà del contenitore del modulo.
* I moduli adattivi forniscono layout di pannelli, ad esempio reattivi, a schede, a soffietto e con procedure guidate, per controllare il layout dei componenti modulo in un pannello. È possibile creare layout di pannelli personalizzati e renderli disponibili per l&#39;uso da parte degli autori di moduli. Per ulteriori informazioni, vedere [Creazione di componenti di layout personalizzati per i moduli adattivi](/help/forms/using/custom-layout-components-forms.md).
* È inoltre possibile personalizzare componenti per moduli adattivi specifici come campi e layout del pannello.

   * Utilizzate la funzionalità [Overlay](/help/sites-developing/overlays.md) di AEM per modificare una copia di un componente. Non è consigliabile modificare i componenti predefiniti.
   * Per personalizzare il layout dei componenti per moduli adattivi forniti con il prodotto in /libs, [creare componenti per layout personalizzati](/help/forms/using/custom-layout-components-forms.md) in aggiunta ai [layout predefiniti](/help/forms/using/layout-capabilities-adaptive-forms.md).
   * Introducete interattività personalizzate creando widget o apparenze personalizzati. Non è consigliabile modificare i componenti predefiniti. Per ulteriori informazioni, vedere [Struttura di aspetto](/help/forms/using/introduction-widgets.md).

* Per informazioni sulla gestione dei dati PII, vedere [Gestione delle informazioni personali](/help/forms/using/adaptive-forms-best-practices.md#p-handling-personally-identifiable-information-p).

## Creazione di moduli adattivi {#author-adaptive-forms}

### Utilizzo dell&#39;interfaccia touch per l&#39;authoring {#using-touch-optimized-ui-for-authoring}

* Utilizzare il browser Oggetti nella barra laterale per accedere rapidamente ai campi all&#39;interno della gerarchia del modulo. È possibile utilizzare la casella di ricerca per cercare gli oggetti nel modulo o nella struttura ad albero degli oggetti per spostarsi da un oggetto all&#39;altro.
* Per visualizzare e modificare le proprietà di un componente nel browser Componenti nella barra laterale, selezionate il componente e fate clic su ![cmppr-1](assets/cmppr-1.png). È inoltre possibile fare doppio clic su un componente per visualizzarne le proprietà nel browser delle proprietà.
* Utilizzare le scelte rapide da tastiera per eseguire azioni rapide sui moduli. Vedere [ Scelte rapide da tastiera AEM Forms](/help/forms/using/keyboard-shortcuts.md).

* I componenti per moduli adattivi sono consigliati per essere utilizzati solo nelle pagine per moduli adattivi. I componenti dipendono dalla gerarchia padre. Non utilizzarli quindi in una pagina AEM.

Consultare inoltre le descrizioni dei componenti e le procedure ottimali in [Introduzione alla creazione di moduli adattivi](/help/forms/using/introduction-forms-authoring.md).

### Uso delle regole nei moduli adattivi {#using-rules-in-adaptive-forms}

 AEM Forms fornisce un [editor di regole](/help/forms/using/rule-editor.md) che consente di creare regole per aggiungere comportamenti dinamici ai componenti per moduli adattivi. Utilizzando queste regole, è possibile valutare le condizioni e attivare azioni sui componenti, come mostrare o nascondere campi, calcolare i valori, modificare l&#39;elenco a discesa in modo dinamico e così via.

L&#39;editor di regole fornisce un editor visivo e un editor di codice per la scrittura di regole. Quando si scrivono regole in modalità editor di codice, tenere in considerazione quanto segue:

* Utilizzare nomi univoci e significativi per i campi e i componenti del modulo per evitare possibili conflitti durante la scrittura delle regole.
* Utilizzare l&#39;operatore `this` per fare riferimento a se stesso in un&#39;espressione di regola. La regola rimane valida anche se il nome del componente cambia. Esempio, `field1.valueCommit script: this.value > 10`.

* Utilizzare i nomi dei componenti per fare riferimento ad altri componenti del modulo. Utilizzare la proprietà `value` per recuperare il valore di un campo o di un componente. Esempio, `field1.value`.

* Per evitare conflitti, fai riferimento ai componenti in base a una gerarchia univoca relativa. Esempio, `parentName.fieldName`.

* Quando si gestiscono regole complesse o comunemente utilizzate, è consigliabile scrivere logica aziendale come funzioni in una libreria client separata che è possibile specificare e riutilizzare tra i moduli adattivi. La libreria client deve essere una libreria standalone e non deve avere dipendenze esterne, ad eccezione di jQuery e Underscore.js. È inoltre possibile utilizzare la libreria client per applicare la [riconvalida lato server](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form) dei dati del modulo inviati.
* I moduli adattivi forniscono una serie di API utilizzabili per comunicare con i moduli adattivi ed eseguire azioni su di essi. Alcune delle API chiave sono le seguenti. Per ulteriori informazioni, vedere [Riferimento API della libreria JavaScript per Forms](https://adobe.com/go/learn_aemforms_documentation_63) adattivo.

   * `guideBridge.reset()`: Ripristina un modulo.
   * `guideBridge.submit()`: Invia un modulo.
   * `guideBridge.setFocus(somExp, focusOption, runCompletionExp)`: Imposta lo stato attivo su un campo.
   * `guideBridge.validate(errorList, somExpression, focus)`: Convalida un modulo.
   * `guideBridge.getDataXML(options)`: Ottiene i dati del modulo come XML.
   * `guideBridge.resolveNode(somExpression)`: Ottiene un oggetto modulo.
   * `guideBridge.setProperty(somList, propertyName, valueList)`: Imposta la proprietà di un oggetto modulo.
   * È inoltre possibile utilizzare le seguenti proprietà del campo:

      * `field.value` per modificare il valore di un campo.
      * f `ield.enabled` per abilitare/disabilitare un campo.
      * `field.visible` per modificare la visibilità di un campo.

* Gli autori di moduli adattivi potrebbero dover scrivere codice JavaScript per creare logica aziendale in un modulo. JavaScript è potente ed efficace, ma potrebbe compromettere le aspettative di sicurezza. Pertanto, è necessario assicurarsi che l&#39;autore del modulo sia una persona affidabile e che vi siano processi per rivedere e approvare il codice JavaScript prima che il modulo venga messo in produzione. L&#39;amministratore può limitare l&#39;accesso all&#39;editor delle regole ai gruppi di utenti in base al loro ruolo o funzione. Consultate [Concedere l&#39;accesso all&#39;editor di regole a gruppi di utenti selezionati](/help/forms/using/rule-editor-access-user-groups.md).
* È possibile utilizzare le espressioni nelle regole per rendere dinamici i moduli adattivi. Tutte le espressioni sono espressioni JavaScript valide e utilizzano API per modelli di script di moduli adattivi. Queste espressioni restituiscono valori di determinati tipi. Per ulteriori informazioni sulle espressioni e sulle best practice che le circondano, vedere [Espressioni di moduli adattivi](/help/forms/using/adaptive-form-expressions.md).

### Utilizzo dei temi {#working-with-themes}

L&#39;opzione Adattata per i temi consente di creare stili riutilizzabili che possono essere applicati ai diversi moduli per ottenere un aspetto e uno stile coerenti. È consigliabile utilizzare Temi per definire lo stile dei componenti e dei pannelli dei moduli. Di seguito sono riportate alcune best practice relative ai temi:

* Utilizzate la libreria di risorse per applicare rapidamente stili di testo, sfondo e immagini. Quando uno stile viene aggiunto nella libreria delle risorse, è disponibile per altri temi e nella modalità stile dell&#39;editor di moduli.
* Applicate impostazioni globali come il font e lo sfondo della pagina utilizzando il selettore a livello di pagina.
* Utilizzate le librerie client per importare stili esistenti o avanzati nei temi.
* È possibile ignorare lo stile per campi, pannelli o pulsanti specifici in un livello dello stile del modulo.
* Se un tema non soddisfa i requisiti di stile, è possibile utilizzare classi predefinite come guideFieldNode, guideFieldLabel, guideFieldWidget e guidePanelNode per applicare uno stile comune ai moduli.

Per ulteriori informazioni, vedere [Temi](/help/forms/using/themes.md).

### Ottimizzazione delle prestazioni di moduli grandi e complessi {#optimizing-performance-of-large-and-complex-forms}

Gli autori e gli utenti finali dei moduli in genere si trovano di fronte a problemi di prestazioni durante il caricamento di moduli di grandi dimensioni in modalità di creazione o in fase di esecuzione. Con l&#39;aumento del numero di oggetti (campi e pannelli) nel modulo, l&#39;esperienza di creazione e esecuzione inizia a diminuire. Consente inoltre a più autori di collaborare e creare contemporaneamente un modulo.

Per risolvere i problemi di prestazioni relativi ai moduli di grandi dimensioni, attenersi alle procedure ottimali riportate di seguito.

* È consigliabile creare moduli adattivi utilizzando il modello dati del modulo XSD anche durante la conversione di un XFA in un modulo adattivo, se possibile.
* Includere solo i campi e i pannelli nei moduli adattivi che acquisiscono informazioni dall&#39;utente. Considerate la possibilità di mantenere minimi i contenuti statici oppure utilizzate gli URL per aprirli in una finestra separata.
* Anche se ogni modulo è progettato per uno scopo specifico, nella maggior parte dei moduli sono presenti alcuni segmenti comuni. Ad esempio, dati personali, indirizzo, dati di lavoro e così via. Creare [frammenti di modulo adattivo](/help/forms/using/adaptive-form-fragments.md) per elementi e sezioni di modulo comuni e utilizzarli tra i vari moduli. È inoltre possibile salvare un pannello in un modulo esistente come frammento. Qualsiasi modifica apportata a un frammento si riflette in tutti i moduli adattivi associati. Promuove la creazione collaborativa in quanto più autori possono lavorare contemporaneamente su diversi frammenti che costituiscono un modulo.

   * Analogamente ai moduli adattivi, si consiglia di definire nella libreria client tutti gli script personalizzati e di stile specifici per i frammenti utilizzando la finestra di dialogo del contenitore dei frammenti. Inoltre, provare a creare frammenti autosufficienti che non dipendono da oggetti esterni.
   * Evitare di utilizzare script tra frammenti. Se all&#39;esterno del frammento è presente un oggetto a cui è necessario fare riferimento, provare a renderlo parte del modulo principale. Se l&#39;oggetto deve ancora risiedere in un altro frammento, fare riferimento ad esso con il nome corrispondente nello script.

* Per salvare periodicamente il modulo adattivo e consentire agli utenti di rivederlo in un secondo momento per completare il modulo, utilizzare Salva e riprendi con salvataggio automatico.
* Configurare i frammenti per il caricamento lento. In fase di esecuzione, i frammenti contrassegnati per il caricamento vengono sottoposti a rendering solo quando sono obbligatori. Riduce notevolmente il tempo di caricamento dei moduli di grandi dimensioni. È inoltre supportata nei frammenti con pannelli ripetibili. Per ulteriori informazioni, vedere [Configurare il caricamento pigro](/help/forms/using/lazy-loading-adaptive-forms.md).

   * Non configurate il caricamento pigro sui frammenti in un layout griglia reattivo o nel primo pannello.
   * I componenti Allegati e Termini e Condizioni del file non sono supportati nei frammenti caricati lentamente.
   * Contrassegnare un valore in un pannello caricato in modo pigro come Usa valore globale se tale valore viene utilizzato in un&#39;altra parte del modulo in modo che il valore sia disponibile per l&#39;utilizzo quando il pannello contenitore viene scaricato.
   * Valutare la possibilità di scrivere regole di visibilità per i frammenti da mostrare o nascondere in base a una condizione.

### Precompilazione dei moduli adattivi {#prefilling-adaptive-forms}

È possibile precompilare i campi modulo adattivo con i dati recuperati dal back-end per consentire agli utenti di compilare rapidamente il modulo ed evitare errori di digitazione.

*  AEM Forms fornisce un servizio di precompilazione per leggere i dati da un file XML di dati predefiniti e precompilare i campi di un modulo adattivo con il contenuto nel file XML di precompilazione.
* L&#39;XML dei dati di precompilazione deve essere conforme allo schema del modello di modulo associato al modulo adattivo.
* Includere le sezioni `afBoundedData` e `afUnBoundedData` nel file XML di precompilazione per precompilare i campi associati e non associati in un modulo adattivo.

* Per i moduli adattivi basati sul modello di dati del modulo,  AEM Forms fornisce il servizio di precompilazione dei modelli di dati del modulo. Il servizio precompila le query sulle origini dati per gli oggetti del modello dati nel modulo adattivo e precompila i valori dei campi durante il rendering del modulo.
* È inoltre possibile utilizzare i moduli adattivi per la precompilazione di file, crx, servizi o protocolli http.
*  AEM Forms supporta servizi di precompilazione personalizzati che è possibile collegare come servizio OSGi per precompilare i moduli adattivi.

Per ulteriori informazioni, vedere [Precompila campi modulo adattivo](/help/forms/using/prepopulate-adaptive-form-fields.md).

### Firma e invio di moduli adattivi {#signing-and-submitting-adaptive-forms}

I moduli adattivi richiedono azioni di invio per elaborare i dati specificati dall&#39;utente. Un&#39;azione Invia determina l&#39;attività eseguita sui dati inviati utilizzando un modulo adattivo.

* Nei moduli adattivi sono disponibili diverse azioni di invio. Per informazioni dettagliate, vedere [Configurazione dell&#39;azione di invio](/help/forms/using/configuring-submit-actions.md).
* È possibile scrivere un&#39;azione di invio personalizzata se le azioni di invio predefinite non soddisfano il caso d&#39;uso. Per ulteriori informazioni, vedere [Scrittura di un&#39;azione di invio personalizzata per i moduli adattivi](/help/forms/using/custom-submit-action-form.md).
* Includi convalide lato server per impedire l&#39;invio di dati non validi.

È possibile sfruttare l&#39;esperienza con più firme di  Adobe Sign nei moduli adattivi. Durante la configurazione  Adobe Sign nei moduli adattivi, tenere presente quanto segue. Per informazioni dettagliate, vedere [Utilizzo  Adobe Sign in un modulo adattivo](/help/forms/using/working-with-adobe-sign.md).

*  modulo adattivo abilitato per Adobe Sign viene inviato solo dopo che tutti i firmatari avranno firmato il modulo. Forms viene visualizzato nello stato Firma in sospeso finché il modulo non viene firmato da tutti i firmatari.
* Al momento dell&#39;invio è possibile configurare l&#39;esperienza di firma all&#39;interno del modulo o reindirizzare i firmatari a una pagina di firma.
* Configura l&#39;esperienza di firma sequenziale o parallela, a seconda delle necessità.

### Generazione del documento di record {#generating-document-of-record}

Un documento record (DoR) è una versione PDF appiattita di un modulo adattivo che può essere stampato, firmato o archiviato.

* A seconda del modello di dati del modulo su cui si basa un modulo adattivo, è possibile configurare un modello per il DoR nel modo seguente:

   * **Modello** di modulo XFA: Utilizzare il file XDP associato come modello DoR.
   * **Schema** XSD: Utilizzare il modello XFA associato che utilizza lo stesso schema XML utilizzato dal modulo adattivo.
   * **Nessuno**: Utilizzare il DoR generato automaticamente.

* È possibile configurare intestazione, piè di pagina, immagini, colore, font e così via direttamente dalla scheda Documento di registrazione dell’editor di moduli adattivi.
* Utilizzare `DoRService` per generare il DoR a livello di programmazione.
* Escludere i campi nascosti dal DoR.
* Utilizzare il parametro di richiesta `afAcceptLang` per visualizzare il DoR in un&#39;altra lingua.

### Debug e verifica dei moduli adattivi {#debugging-and-testing-adaptive-forms}

[AEM Chrome Plug-](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/) in è un&#39;estensione del browser per Google Chrome che fornisce strumenti per il debug dei moduli adattivi. Gli autori e gli sviluppatori di moduli possono utilizzare questi strumenti per:

* Identificazione dei colli di bottiglia e ottimizzazione delle prestazioni del rendering del modulo
* Debug di parole chiave ed errori bindRef nel modulo
* Attivare e configurare i registri
* Debug di regole e script nel modulo
* Esplora e scopri le API guideBridge

Per ulteriori informazioni, vedere [AEM plug-in Chrome - Modulo adattivo](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/adaptive-form/).

Calvin SDK è un&#39;API di utilità per gli sviluppatori di Forms adattivi per testare l&#39;Forms adattivo. Calvin SDK è basato sul [framework di test di Hobbes.js](https://docs.adobe.com/docs/en/aem/6-3/develop/ref/test-api/index.html). Potete utilizzare il framework per verificare quanto segue:

* Esperienza di rappresentazione di un modulo adattivo
* Esperienza di precompilazione di un modulo adattivo
* Invio dell&#39;esperienza di un modulo adattivo
* Regole di espressione
* Convalide
* Caricamento Lazy

Per ulteriori informazioni, vedere [Verificare automaticamente i moduli adattivi](/help/forms/using/calvin.md).

### Convalida dei moduli adattivi AEM server {#validating-adaptive-forms-on-aem-server}

Le convalide lato server sono necessarie per evitare qualsiasi tentativo di bypassare le convalide sul client e qualsiasi possibile compromesso tra l&#39;invio di dati e le violazioni delle regole aziendali. Le convalide lato server vengono eseguite sul server caricando la libreria client richiesta.

* Includere funzioni in una libreria client per la convalida delle espressioni nei moduli adattivi e specificare la libreria client nella finestra di dialogo del contenitore di moduli adattivi. Per ulteriori informazioni, vedere [Ripristino lato server](/help/forms/using/configuring-submit-actions.md#p-server-side-revalidation-in-adaptive-form-p).
* La convalida sul lato server convalida il modello di modulo. È consigliabile creare una libreria client separata per le convalide e non combinarla con altri elementi come lo stile HTML e la manipolazione DOM nella stessa libreria client.

### Localizzazione di moduli adattivi {#localizing-adaptive-forms}

AEM fornisce flussi di lavoro di traduzione che è possibile utilizzare per localizzare i moduli adattivi. Per informazioni, vedere [Utilizzo AEM flusso di lavoro di traduzione per localizzare moduli adattivi](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md).

Di seguito sono riportate alcune best practice per la localizzazione di moduli adattivi:

* Utilizzare frammenti di modulo adattivi per elementi comuni all&#39;interno dei moduli e localizzare i frammenti. In questo modo, è possibile localizzare un frammento una sola volta e lo si riflette in tutti i moduli in cui viene utilizzato il frammento localizzato.
* Eventuali modifiche, come l’aggiunta di un nuovo componente o l’applicazione di uno script in un modulo localizzato, non vengono localizzate automaticamente. Pertanto, è necessario finalizzare un modulo prima di localizzarlo per evitare più cicli di localizzazione.
* Utilizzare il parametro di richiesta `afAcceptLang` per ignorare le impostazioni internazionali del browser ed eseguire il rendering del modulo nelle impostazioni internazionali specificate. Ad esempio, l&#39;URL seguente imporrà il rendering del modulo in lingua giapponese, indipendentemente dalle impostazioni internazionali specificate nel browser:

   `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

*  AEM Forms supporta attualmente la localizzazione di contenuti di moduli adattivi in inglese (en), spagnolo (es), francese (fr), italiano (it), tedesco (de), giapponese (ja), portoghese-brasiliano (pt-BR), cinese (zh-CN), cinese-Taiwan (zh-TW) e coreano (ko-KR). Tuttavia, è possibile aggiungere il supporto per le nuove impostazioni internazionali per i moduli adattivi in fase di esecuzione. Per ulteriori informazioni, vedere [Supporto di nuove impostazioni internazionali per la localizzazione dei moduli adattivi](/help/forms/using/supporting-new-language-localization.md).

## Prepara progetto moduli per la produzione {#prepare-forms-project-for-production}

### Aggiunta del server di elaborazione moduli {#adding-forms-processing-server}

È possibile configurare un&#39;istanza aggiuntiva  server AEM Forms che si trova dietro il firewall in un&#39;area protetta. Potete utilizzare questa istanza per:

* **Elaborazione** batch: processi periodici o pianificati in batch con carichi elevati. Ad esempio, la stampa di istruzioni, la generazione di corrispondenze e l&#39;utilizzo di servizi di documentazione come PDF Generator, Output e Assembler.
* **Memorizzazione dei dati** PII: Salvare i dati PII sul server di elaborazione. Non è richiesto se si sta già utilizzando un provider di memorizzazione personalizzato per la memorizzazione dei dati PII.

### Spostamento del progetto in un altro ambiente {#moving-project-to-another-environment}

Spesso è necessario spostare i progetti AEM da un ambiente all&#39;altro. Alcuni degli elementi chiave da ricordare durante lo spostamento sono i seguenti:

* Esegui il backup delle librerie client, del codice personalizzato e delle configurazioni esistenti.
* Distribuire pacchetti di prodotti e patch manualmente e nell&#39;ordine specificato nel nuovo ambiente.
* Distribuite i pacchetti di codice e i bundle specifici del progetto manualmente e come pacchetto o pacchetto separato sul nuovo server AEM.
* (*AEM Forms su JEE solo*) Distribuire manualmente LCA e DSC sul server di Forms Workflow.
* Utilizzate la funzionalità [Export-Import](/help/forms/using/import-export-forms-templates.md) per spostare le risorse nel nuovo ambiente. Potete inoltre configurare l&#39;agente di replica e pubblicare le risorse.
* Quando eseguite l&#39;aggiornamento, sostituite tutte le API e le funzionalità obsolete con nuove API e funzionalità.

### Configurazione AEM {#configuring-aem}

Di seguito sono riportate alcune best practice per configurare AEM per migliorare le prestazioni complessive:

* Abilita la compressione libreria client HTML per JavaScript e CSS dalla console Flash. Vedere [Clientlibs spiegato da esempio](https://blogs.adobe.com/experiencedelivers/experience-management/clientlibs-explained-example/).
* Memorizza nella cache tutte le librerie client in `/etc.clientlibs/fd` e tutte le librerie client personalizzate aggiuntive nel dispatcher AEM per aumentare la capacità di risposta e la sicurezza dei moduli pubblicati. Per ulteriori informazioni, vedere [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html).

* Non memorizzare nella cache i percorsi `/content/forms/af/` e `/content/dam/formsanddocuments/*`. per informazioni dettagliate sulla configurazione del caching dei moduli adattivi, vedere [Memorizzazione nella cache dei moduli adattivi](/help/forms/using/configure-adaptive-forms-cache.md).

* Abilitare l&#39;HTML tramite il modulo di compressione del server Web. Per ulteriori informazioni, vedere [Ottimizzazione delle prestazioni di  server AEM Forms](/help/forms/using/performance-tuning-aem-forms.md).
* Aumentare le chiamate per la configurazione delle richieste per i moduli di grandi dimensioni. Vedere [Ottimizzazione delle prestazioni di moduli grandi e complessi](/help/forms/using/adaptive-forms-best-practices.md#optimizing-performance-of-large-and-complex-forms).
* Creare [pagine di errore personalizzate visualizzate dal gestore di errori](https://helpx.adobe.com/experience-manager/6-2/sites-developing/customizing-errorhandler-pages.html).
* Server AEM Forms  sicuro.

   * Utilizzate la modalità di esecuzione `nosamplecontent` per garantire che non siano presenti contenuti di esempio e utenti di esempio distribuiti nel server di produzione. Vedere [AEM in esecuzione in modalità pronta per la produzione](/help/sites-administering/production-ready.md).

* Le dimensioni dell&#39;heap devono essere pari ad almeno 8 GB. Per altre impostazioni, vedere [Ottimizzazione delle prestazioni di  server AEM Forms](/help/forms/using/performance-tuning-aem-forms.md).
* Utilizzate le sessioni utente del servizio invece delle sessioni di amministrazione per eseguire le attività a livello di servizio. Per ulteriori informazioni, vedere [Autenticazione dei servizi](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html).

>[!VIDEO](https://vimeo.com/)

### Configurazione della memorizzazione esterna per le bozze e i dati dei moduli inviati {#external-storage}

In un ambiente di produzione, si consiglia di non memorizzare i dati del modulo inviato AEM repository. L&#39;implementazione predefinita delle azioni di invio Forms Portal Store, Store Content e Store PDF consente di archiviare i dati del modulo AEM archivio. Tali azioni di invio sono destinate solo a scopo dimostrativo. Inoltre, per impostazione predefinita, le funzioni Salva e Riprendi e Salva automaticamente utilizzano l&#39;archiviazione del portale. Considerate pertanto le seguenti raccomandazioni:

* **Memorizzazione dei dati** bozza: Se si utilizza la funzione Bozza di moduli adattivi, è necessario implementare un&#39;interfaccia SPI (Service Provider Interface) personalizzata per memorizzare i dati bozza in un archivio più sicuro, come il database. Per ulteriori informazioni, vedere [Esempio per l&#39;integrazione del componente per bozze e invii con il database](/help/forms/using/integrate-draft-submission-database.md).

* **Memorizzazione dei dati** di invio: Se si utilizza l&#39;archivio di invio di Form Portal, è necessario implementare un SPI personalizzato per memorizzare i dati di invio in un database. Per un&#39;integrazione di esempio, vedere [Esempio per l&#39;integrazione del componente bozze e invii con database](/help/forms/using/integrate-draft-submission-database.md).

   È inoltre possibile scrivere un&#39;azione di invio personalizzata per memorizzare i dati e gli allegati del modulo in un archivio protetto. Per ulteriori informazioni, vedere [Scrittura di un&#39;azione di invio personalizzata per i moduli adattivi](/help/forms/using/custom-submit-action-form.md).

* **Lunghezza dell&#39;ID** bozza: Quando si salva un modulo adattivo come bozza, viene generato un ID bozza per identificare in modo univoco la bozza. Il valore minimo per la lunghezza del campo ID bozza è 26 caratteri.  Adobe consiglia di impostare la lunghezza dell&#39;ID bozza su 26 o più caratteri.

### Gestione delle informazioni personali identificabili {#handling-personally-identifiable-information}

Una delle sfide principali per le organizzazioni è come gestire i dati personali (PII). Di seguito sono riportate alcune best practice utili per gestire tali dati:

* Utilizzare un archivio esterno protetto, come il database, per memorizzare i dati dei moduli bozza e inviati. Vedere [Configurazione della memorizzazione esterna per le bozze e i dati dei moduli inviati](/help/forms/using/adaptive-forms-best-practices.md#external-storage).
* Utilizza il componente Modulo termini e condizioni per ottenere il consenso esplicito dell’utente prima di attivare il salvataggio automatico. In questo caso, abilitate il salvataggio automatico solo quando l&#39;utente accetta le condizioni del componente Condizioni generali.

