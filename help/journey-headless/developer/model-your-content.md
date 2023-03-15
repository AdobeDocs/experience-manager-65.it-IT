---
title: Come modellare il contenuto
description: In questa parte del Percorso per sviluppatori di AEM headless, scopri come modellare i contenuti per la distribuzione AEM headless utilizzando la modellazione dei contenuti con modelli di frammenti di contenuto e frammenti di contenuto.
exl-id: f75b433f-5a81-4259-a9f5-b58954b87970
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1826'
ht-degree: 99%

---

# Come modellare il contenuto {#model-your-content}

In questa parte del [Percorso per sviluppatori di AEM headless](overview.md), puoi imparare a modellare la struttura del contenuto. Quindi realizza quella struttura per Adobe Experience Manager (AEM) utilizzando Modelli per frammenti di contenuto e Frammenti di contenuto, da riutilizzare tra i canali.

## Percorso affrontato finora {#story-so-far}

All’inizio [Scopri lo sviluppo di CMS headless](learn-about.md) si è occupato della consegna di contenuti headless e la ragione per cui dovrebbero essere utilizzati. In seguito la [Guida introduttiva a AEM headless ](getting-started.md) ha descritto AEM headless nel contesto del tuo progetto.

Nel documento precedente del percorso di AEM headless, [Percorso della tua prima esperienza con AEM headless](path-to-first-experience.md), hai quindi appreso i passaggi necessari per implementare il primo progetto. Dopo averlo letto dovresti:

* comprendere importanti considerazioni sulla pianificazione per la progettazione dei contenuti
* comprendere i passaggi per implementare headless in base ai requisiti del livello di integrazione.
* impostare gli strumenti e le configurazioni AEM necessarie.
* Conoscere le best practice per semplificare il tuo percorso headless, garantire la distribuzione rapida dei contenuti e l’efficienza nella loro generazione.

Questo articolo si basa su questi fondamentali in modo da capire come preparare il tuo progetto AEM headless.

## Obiettivo {#objective}

* **Pubblico**: principiante
* **Obiettivo**: scopri come modellare la struttura del contenuto, quindi realizzare tale struttura utilizzando i Modelli per frammenti di contenuto di AEM e i Frammenti di contenuto:
   * Introduzione dei concetti e della terminologia relativi alla modellazione di dati/contenuti.
   * Scopri perché è necessaria la modellazione dei contenuti per la distribuzione di contenuti headless.
   * Scopri come realizzare questa struttura utilizzando Modelli di frammenti di contenuto di AEM (e creare contenuti con Frammenti di contenuto).
   * Scopri come modellare il contenuto; principi con campioni di base.

>[!NOTE]
>
>La modellazione dei dati è un campo molto vasto, poiché viene utilizzata durante lo sviluppo di database relazionali. Ci sono molti libri e fonti di informazione online, disponibili.
>
>Prenderemo in considerazione solo gli aspetti di interesse nella modellazione dei dati da utilizzare con AEM headless.

## Modellazione dei contenuti {#content-modeling}

*Il mondo là fuori è grande e brutto*.

Forse sì, forse no, ma certamente è grande e ***complicato*** e la modellazione dei dati viene utilizzata per definire una rappresentazione semplificata di una sottosezione molto (molto) piccola, utilizzando le informazioni specifiche necessarie per un determinato scopo.

>[!NOTE]
>
>Poiché AEM ha a che fare con i contenuti, ci riferiamo alla modellazione dei dati come modellazione dei contenuti.

Esempio:

Ci sono molte scuole, ma tutte hanno varie cose in comune:

* Una posizione
* Un dirigente scolastico
* Molti insegnanti
* Molti membri del personale non docente
* Molti studenti
* Molti ex-insegnanti
* Molti ex allievi
* Molte classi
* Molti (molti) libri
* Molti (molti) pezzi di attrezzatura
* Molte attività extra curriculari
* e così via....

La lista può sembrare infinita anche facendo un esempio così piccolo. Ma se si vuole soltanto che l’applicazione esegua un’attività semplice, è necessario limitare le informazioni alle risorse essenziali.

Ad esempio, pubblicità di eventi speciali per tutte le scuole della zona:

* Nome della scuola
* Posizione della scuola
* Dirigente scolastico
* Tipo di evento
* Data dell’evento
* Insegnante che organizza l’evento

### Concetti {#concepts}

Le informazioni da descrivere sono denominate **Entità**: fondamentalmente le “cose” di cui vogliamo memorizzare le informazioni.

Le informazioni che vogliamo memorizzare sono gli **Attributi** (proprietà), ad esempio Nome e Qualifiche per gli insegnanti.

Poi ci sono varie **Relazioni** tra le entità. Per esempio, di solito una scuola ha un solo preside e molti insegnanti (e di solito il preside è anche un insegnante).

Il processo di analisi e definizione di queste informazioni, insieme alle relazioni tra di esse, è chiamato **Modellazione dei contenuti**.

### Funzioni di base {#basics}

Spesso è necessario iniziare disegnando uno **Schema concettuale** che descrive le entità e le loro relazioni. Di solito questo schema è di alto livello (concettuale).

Dopo aver fissato lo schema concettuale è possibile tradurre i modelli in uno **Schema logico** che descrive le entità, gli attributi e le relazioni. A questo livello, è necessario esaminare attentamente le definizioni per eliminare la duplicazione e ottimizzare la progettazione.

>[!NOTE]
>
>A volte questi due passaggi vengono uniti, spesso a seconda della complessità dello scenario.

Ad esempio, sono necessarie entità separate per `Head Teacher` e `Teacher` o è sufficiente un attributo aggiuntivo sul modello `Teacher`?

### Garantire l’integrità dei dati {#data-integrity}

L’integrità dei dati è necessaria per garantire l’accuratezza e la coerenza dei contenuti durante l’intero ciclo di vita. Ciò include la garanzia che gli autori dei contenuti possano capire facilmente cosa archiviare e dove, per cui sono fondamentali i seguenti elementi:

* una struttura chiara
* una struttura il più concisa possibile (senza sacrificare la precisione)
* la convalida dei singoli campi
* all’occorrenza, limitare il contenuto di campi specifici a ciò che è significativo

### Eliminazione della ridondanza dei dati {#data-redundancy}

La ridondanza dei dati si verifica quando le stesse informazioni vengono memorizzate due volte nella struttura del contenuto. Questo dovrebbe essere evitato in quanto può generare confusione durante la creazione del contenuto ed errori durante l’esecuzione di query; per non parlare dell’uso improprio dello spazio di archiviazione.

### Ottimizzazione e prestazioni {#optimization-and-performance}

Ottimizzando la struttura è possibile migliorare le prestazioni, sia per la creazione di contenuti che per l’esecuzione di query.

È tutta una questione di equilibrio, ma la creazione di una struttura troppo complessa o con troppi livelli può:

* creare confusione per gli autori che generano i contenuti.

* penalizzare notevolmente le prestazioni se la query deve accedere a più frammenti di contenuto nidificati (a cui si fa riferimento) per recuperare il contenuto richiesto.

## Modellazione dei contenuti per AEM Headless {#content-modeling-for-aem-headless}

La Modellazione dati è un insieme di tecniche consolidate, spesso utilizzate quando si sviluppano database relazionali, quindi cosa significa Modellazione dei contenuti per AEM Headless?

### Perché? {#why}

Per garantire che l’applicazione possa richiedere e ricevere in modo coerente ed efficiente il contenuto richiesto da AEM, questo contenuto deve essere strutturato.

Ciò significa che l’applicazione conosce in anticipo la forma della risposta e quindi come elaborarla. Questo è molto più semplice della ricezione di contenuti in formato libero, che devono essere analizzati per determinare cosa contengono e quindi come possono essere utilizzati.

### Introduzione a Come? {#how}

AEM utilizza Frammenti di contenuto per fornire le strutture necessarie per la distribuzione headless dei contenuti alle applicazioni.

La struttura del modello di contenuto è:

* realizzata secondo la definizione del modello per frammenti di contenuto,
* utilizzata come base dei frammenti di contenuto impiegati per la generazione dei contenuti.

>[!NOTE]
>
>I modelli per frammenti di contenuto vengono utilizzati anche come base degli schemi GraphQL AEM, utilizzati per recuperare i contenuti. Ulteriori informazioni su questo argomento in una sessione successiva.

Le richieste di contenuti vengono effettuate utilizzando l’API GraphQL di AEM, un’implementazione personalizzata dell’API GraphQL standard. L’API GraphQL di AEM consente di eseguire query (complesse) sui Frammenti di contenuto; ogni query è basata su un tipo di modello specifico.

Il contenuto restituito può quindi essere utilizzato dalle applicazioni.

## Creazione della struttura con modelli per frammenti di contenuto {#create-structure-content-fragment-models}

I modelli per frammenti di contenuto forniscono vari meccanismi che consentono di definire la struttura del contenuto.

Un modello per frammento di contenuto descrive un’entità.

>[!NOTE]
>È necessario abilitare la funzionalità Frammento di contenuto nel browser di configurazione in modo da poter creare nuovi modelli.

>[!TIP]
>
>Il modello deve essere denominato in modo che l’autore del contenuto sappia quale modello selezionare durante la creazione di un frammento di contenuto.

All’interno di un modello:

1. **Tipi di dati** consente di definire i singoli attributi.
Ad esempio, definisci il campo contenente il nome di un insegnante come **Testo** e i relativi anni di servizio come **Numero**.
1. I tipi di dati **Riferimento contenuto** e **Riferimento frammento** consentono di creare relazioni con altri contenuti all’interno di AEM.
1. Il tipo di dati **Riferimento frammento** consente di realizzare più livelli di struttura nidificando i frammenti di contenuto (in base al tipo di modello). Questo è fondamentale per la modellazione dei contenuti.

Ad esempio:
![Modellazione dei contenuti con frammenti di contenuto](assets/headless-modeling-01.png "Modellazione dei contenuti con frammenti di contenuto")

### Tipi di dati {#data-types}

AEM fornisce i seguenti tipi di dati per modellare il contenuto:

* Testo su riga singola
* Testo su più righe
* Numero
* Booleano
* Data e ora
* Enumerazione
* Tag
* Riferimento contenuto
* Riferimento frammento
* Oggetto JSON

### Riferimenti e contenuto nidificato {#references-nested-content}

Due tipi di dati forniscono riferimenti a contenuti esterni a uno specifico frammento:

* **Riferimento contenuto**
Fornisce un semplice riferimento ad altri contenuti di qualsiasi tipo.
Ad esempio, è possibile fare riferimento a un’immagine in una posizione specifica.

* **Riferimento frammento**
Fornisce riferimenti ad altri frammenti di contenuto.
Questo tipo di riferimento viene utilizzato per creare contenuti nidificati, introducendo le relazioni necessarie per modellare il contenuto.
Il tipo di dati può essere configurato in modo da consentire agli autori di frammenti di:
   * Modificare direttamente il frammento a cui si fa riferimento.
   * Creare un nuovo frammento di contenuto basato sul modello appropriato

### Creazione di modelli per frammenti di contenuto {#creating-content-fragment-models}

All’inizio è necessario abilitare i modelli per frammenti di contenuto per il sito, questo avviene nel Browser configurazioni; sotto Strumenti -> Generale -> Browser configurazioni. Puoi scegliere di configurare la voce globale oppure creare una nuova configurazione. Esempio:

![Definire la configurazione](assets/cfm-configuration.png)

>[!NOTE]
>
>Consulta Risorse aggiuntive - Frammenti di contenuto nel Browser configurazioni

È quindi possibile creare modelli per frammenti di contenuto e definire la struttura. Questa operazione può essere eseguita in Strumenti -> Risorse -> Modelli per frammenti di contenuto. Esempio:

![Modello per frammenti di contenuto](assets/cfm-model.png)

>[!NOTE]
>
>Consulta Risorse aggiuntive - Modelli per frammenti di contenuto.

## Uso del modello per creare contenuti con frammenti di contenuto {#use-content-to-author-content}

I frammenti di contenuto vengono creati in base a un modello per frammenti di contenuto. Il modello fornisce la struttura, il frammento ospita il contenuto.

### Selezione del modello appropriato {#select-model}

Il primo passaggio per creare effettivamente il contenuto è la creazione di un frammento di contenuto. Questa operazione viene eseguita utilizzando Crea -> Frammento di contenuto nella cartella richiesta in Risorse -> File. La procedura guidata ti condurrà attraverso i passaggi.

Un frammento di contenuto si basa su un modello per frammento di contenuto specifico, selezionato come primo passaggio del processo di creazione.

### Creazione e modifica di contenuti strutturati {#create-edit-structured-content}

Una volta creato il frammento, è possibile aprirlo nell’Editor frammento di contenuto. È possibile:

* modificare il contenuto in modalità normale o a schermo intero.
* formattare il contenuto come Testo completo, Testo normale o Markdown.
* Creare e gestire le varianti dei contenuti.
* Associare contenuto.
* Modificare i metadati.
* Mostrare la struttura ad albero.
* Visualizzare un’anteprima della rappresentazione JSON.

### Creare frammenti di contenuto {#creating-content-fragments}

Dopo aver selezionato il modello appropriato, nell’Editor frammento di contenuto viene aperto un frammento di contenuto per la modifica:

![Editor frammento di contenuto](assets/cfm-editor.png)

>[!NOTE]
>
>Consultare Risorse aggiuntive - Utilizzo di frammenti di contenuto.

## Guida introduttiva con alcuni esempi {#getting-started-examples}

<!--
tbc...
...and/or see the structures covered for the GraphQL samples...
...will those (ever) be delivered as an official sample package?
-->

Per una struttura di base come esempio, vedere Struttura dei frammenti di contenuto di esempio.

## Passaggio successivo {#whats-next}

Ora che hai imparato a modellare la tua struttura e a creare contenuti basandoti su di essa, il passaggio successivo è: [Scoprire come utilizzare le query GraphQL per accedere e recuperare il contenuto dei frammenti di contenuto](access-your-content.md). Questo introduce la descrizione di GraphQL, quindi osserva alcune query di esempio per vedere come funzionano in pratica.

## Risorse aggiuntive {#additional-resources}

* [Utilizzo di frammenti di contenuto](/help/assets/content-fragments/content-fragments.md): la pagina iniziale per i frammenti di contenuto
   * [Frammenti di contenuto nel Browser configurazioni](/help/assets/content-fragments/content-fragments-configuration-browser.md): abilitare la funzionalità Frammento di contenuto nel browser configurazioni
   * [Modelli per frammenti di contenuto](/help/assets/content-fragments/content-fragments-models.md): creazione e modifica di modelli per frammenti di contenuto
   * [Gestione dei frammenti di contenuto](/help/assets/content-fragments/content-fragments-managing.md): creazione e authoring dei frammenti di contenuto; questa pagina ti porterà ad altre sezioni dettagliate
* [Schemi GraphQL AEM](access-your-content.md): come GraphQL realizza i modelli
* [La struttura del frammento di contenuto di esempio](/help/assets/content-fragments/content-fragments-graphql-samples.md#content-fragment-structure-graphql)
* [Guida introduttiva di AEM Headless](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=it): una breve serie di esercitazioni video che offre una panoramica dell’utilizzo delle funzioni headless in AEM, inclusa la modellazione dei contenuti e GraphQL
   * [Nozioni di base sulla modellazione di GraphQL](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/video-series/modeling-basics.html?lang=it): scopri come definire e inserire i frammenti di contenuto in Adobe Experience Manager (AEM) per l’utilizzo con GraphQL.
