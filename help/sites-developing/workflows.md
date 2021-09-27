---
title: Sviluppo ed estensione dei flussi di lavoro
seo-title: Developing and Extending Workflows
description: AEM fornisce diversi strumenti e risorse per la creazione di modelli di flusso di lavoro, lo sviluppo di passaggi del flusso di lavoro e per l’interazione programmatica con i flussi di lavoro
seo-description: AEM provides several tools and resources for creating workflow models, developing workflow steps, and for programmatically interacting with workflows
uuid: 5a857589-3b13-4519-bda2-b1dab6005550
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 8954e3df-3afa-4d53-a7e1-255f3b8f499f
exl-id: 041b1767-8b6c-4887-a70d-abc96a116976
source-git-commit: 82b9b852fa3134f140f8de0bad229282979c8a30
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 3%

---


# Sviluppo ed estensione dei flussi di lavoro{#developing-and-extending-workflows}

AEM fornisce diversi strumenti e risorse per la creazione di modelli di flusso di lavoro, lo sviluppo di passaggi del flusso di lavoro e per l’interazione programmatica con i flussi di lavoro.

I flussi di lavoro consentono di automatizzare i processi per la gestione delle risorse e la pubblicazione dei contenuti nell’ambiente AEM. I flussi di lavoro sono composti da una serie di passaggi, ciascuno dei quali esegue un’attività discreta. Puoi utilizzare i dati di logica e runtime per decidere quando un processo può continuare e selezionare il passaggio successivo tra uno dei diversi passaggi possibili.

Ad esempio, i processi aziendali per la creazione e la pubblicazione di pagine web includono le attività di approvazione e disconnessione di diversi partecipanti. Questi processi possono essere modellati utilizzando flussi di lavoro AEM e applicati a contenuti specifici.

Gli aspetti principali sono trattati di seguito, mentre le pagine che seguono illustrano ulteriori dettagli:

* [Creazione di modelli di flussi di lavoro](/help/sites-developing/workflows-models.md)
* [Estensione della funzionalità per flussi di lavoro](/help/sites-developing/workflows-customizing-extending.md)
* [Interazione con flussi di lavoro a livello di programmazione](/help/sites-developing/workflows-program-interaction.md)
* [Guida di riferimento per i passaggi dei flussi di lavoro](/help/sites-developing/workflows-step-ref.md)
* [Guida di riferimento per il processo dei flusso di lavoro](/help/sites-developing/workflows-process-ref.md)
* [Best practice per i flussi di lavoro](/help/sites-developing/workflows-best-practices.md)

>[!NOTE]
>
>Per informazioni su:
>
>* Partecipare ai flussi di lavoro, consulta [Utilizzo di flussi di lavoro](/help/sites-authoring/workflows.md).
>* Amministrazione dei flussi di lavoro e delle istanze dei flussi di lavoro, consulta [Amministrazione dei flussi di lavoro](/help/sites-administering/workflows.md).
>* Per un articolo della community end-to-end, consulta [Modifica delle risorse digitali tramite flussi di lavoro Adobe Experience Manager.](https://helpx.adobe.com/experience-manager/using/modify_asset_workflow.html)
>* Consulta il [Webinar Chiedi agli esperti AEM sui flussi di lavoro](https://bit.ly/ATACE218).
>* Per un articolo della community end-to-end, consulta [Creazione di un passaggio di partecipante dinamico Adobe Experience Manager 6.3 personalizzato](https://helpx.adobe.com/experience-manager/using/dynamic-steps-aem63.html).
>* Modifiche alla posizione delle informazioni vedi [Ristrutturazione dell&#39;archivio in AEM 6.5](/help/sites-deploying/repository-restructuring.md) e [Best practice per i flussi di lavoro - Posizioni](/help/sites-developing/workflows-best-practices.md#locations).

>


## Modello {#model}

Un `WorkflowModel` rappresenta una definizione (modello) di un flusso di lavoro. È costituito da `WorkflowNodes` e `WorkflowTransitions`. Le transizioni collegano i nodi e definiscono il *flusso*. Il modello ha sempre un nodo iniziale e un nodo finale.

### Modello runtime {#runtime-model}

Le versioni dei modelli di flusso di lavoro sono impostate. Quando esegui un’istanza di flusso di lavoro, utilizza (e mantieni) il modello di runtime del flusso di lavoro (come disponibile al momento dell’avvio del flusso di lavoro).

Un modello di runtime viene [generato quando **Sync** viene attivato nell&#39;editor del modello di flusso di lavoro](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model).

Le modifiche al modello di flusso di lavoro che si verificano e/o ai modelli di runtime generati *dopo* l’avvio dell’istanza specifica non verranno applicate a tale istanza.

>[!CAUTION]
>
>I passaggi eseguiti sono quelli definiti dal [modello di runtime](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model); questo viene generato al momento dell&#39;attivazione dell&#39;azione **Sync** nell&#39;editor del modello di flusso di lavoro.
>
>Se il modello di flusso di lavoro viene modificato dopo questo momento (senza che **Sincronizza** venga attivato), l&#39;istanza di runtime non rifletterà tali modifiche. Le modifiche verranno applicate solo ai modelli di runtime generati dopo l’aggiornamento. Le eccezioni sono gli script ECMA sottostanti, che vengono conservati solo una volta che vengono effettuate le modifiche.

### Incremento {#step}

Ogni passaggio esegue un task discreto. Esistono diversi tipi di passaggi del flusso di lavoro:

* Partecipante (utente/gruppo): Questi passaggi generano un elemento di lavoro e lo assegnano a un utente o a un gruppo. Un utente deve completare l’elemento di lavoro per far avanzare il flusso di lavoro.
* Processo (script, chiamata del metodo Java): Questi passaggi vengono eseguiti automaticamente dal sistema. Uno script ECMA o una classe Java implementa il passaggio . I servizi possono essere sviluppati per ascoltare eventi speciali del flusso di lavoro ed eseguire attività in base alla logica di business.
* Contenitore (flusso di lavoro secondario): Questo tipo di passaggio avvia un altro modello di flusso di lavoro.
* O Dividi/Unisci: Utilizza la logica per decidere quale passaggio eseguire successivamente nel flusso di lavoro.
* AND Split/Join: Consente l’esecuzione simultanea di più passaggi.

Tutti i passaggi condividono le seguenti proprietà comuni: Avvisi `Autoadvance` e `Timeout` (scrivibili).

### Transizione {#transition}

Un `WorkflowTransition` rappresenta una transizione tra due `WorkflowNodes` di un elemento `WorkflowModel`.

* Definisce il collegamento tra due passaggi consecutivi.
* È possibile applicare delle regole.

### Elemento di lavoro {#workitem}

Un `WorkItem` è l&#39;unità che viene passata attraverso un&#39;istanza `Workflow` di un `WorkflowModel`. Contiene il `WorkflowData` su cui agisce l&#39;istanza e un riferimento al `WorkflowNode` che descrive il passaggio del flusso di lavoro sottostante.

* Viene utilizzato per identificare l’attività e viene inserito nella relativa casella in entrata.
* Un’istanza di flusso di lavoro può avere uno o più `WorkItems` contemporaneamente (a seconda del modello di flusso di lavoro).
* Il `WorkItem` fa riferimento all&#39;istanza del flusso di lavoro.
* Nell’archivio il `WorkItem` viene memorizzato sotto l’istanza del flusso di lavoro.

### Payload {#payload}

Fa riferimento alla risorsa che deve essere avanzata tramite un flusso di lavoro.

L’implementazione del payload fa riferimento a una risorsa nell’archivio (per percorso, UUID o URL) o da un oggetto java serializzato. Il riferimento a una risorsa nell’archivio è molto flessibile e in combinazione con sling molto produttivo; ad esempio, è possibile eseguire il rendering del nodo di riferimento come modulo.

### Ciclo di vita {#lifecycle}

Viene creato all’avvio di un nuovo flusso di lavoro (scegliendo il rispettivo modello di flusso di lavoro e definendo il payload) e termina quando il nodo finale viene elaborato.

Le seguenti azioni sono possibili su un&#39;istanza di flusso di lavoro:

* Termina
* Sospendi
* Riprendi
* Riavvia

Le istanze completate e terminate vengono archiviate.

### Casella in entrata {#inbox}

Ogni account utente dispone di una propria casella in entrata del flusso di lavoro in cui le `WorkItems` assegnate sono accessibili.

Le `WorkItems` vengono assegnate direttamente all’account utente o al gruppo a cui appartengono.

### Tipi di flussi di lavoro {#workflow-types}

Esistono vari tipi di flussi di lavoro come indicato nella console Modelli di flusso di lavoro :

![wf-aggiornato-03](assets/wf-upgraded-03.png)

* **Impostazione predefinita**

   Si tratta dei flussi di lavoro preconfigurati inclusi in un’istanza AEM standard.

* Flussi di lavoro personalizzati (nessun indicatore nella console)

   Si tratta di flussi di lavoro che sono stati creati come nuovi o da flussi di lavoro preconfigurati sovrapposti alle personalizzazioni.

* **Legacy**

   Flussi di lavoro creati in una versione precedente di AEM. Questi possono essere mantenuti durante un aggiornamento o esportati come pacchetto di flusso di lavoro dalla versione precedente, quindi importati nella nuova versione.

### Flussi di lavoro transitori {#transient-workflows}

I flussi di lavoro standard salvano informazioni di runtime (cronologia) durante la loro esecuzione. Puoi anche definire un modello di flusso di lavoro come **Transitent** per evitare che tale cronologia venga mantenuta. Viene utilizzato per ottimizzare le prestazioni in quanto consente di risparmiare/evitare il tempo/le risorse utilizzate per mantenere le informazioni.

I flussi di lavoro transitori possono essere utilizzati per qualsiasi flusso di lavoro che:

* vengono eseguiti spesso.
* non è necessaria la cronologia del flusso di lavoro.

Sono stati introdotti flussi di lavoro transitori per il caricamento di un numero elevato di risorse, dove le informazioni sulle risorse sono importanti, ma non la cronologia del runtime del flusso di lavoro.

>[!NOTE]
>
>Per ulteriori informazioni, consulta [Creazione di un flusso di lavoro transitorio](/help/sites-developing/workflows-models.md#creating-a-transient-workflow) .

>[!CAUTION]
>
>Quando un modello di flusso di lavoro è stato contrassegnato come transitorio, ci sono alcuni scenari in cui le informazioni di runtime verranno comunque mantenute:
>
>* Il tipo di payload (ad esempio, video) richiede passaggi esterni per l’elaborazione; in questi casi la cronologia di runtime è necessaria per la conferma dello stato.
>* Il flusso di lavoro immette un **AND Split**; in questi casi la cronologia di runtime è necessaria per la conferma dello stato.
>* Quando il flusso di lavoro transitorio entra in un passaggio partecipante, cambia la modalità (in fase di runtime) in non transitoria; quando l&#39;attività viene passata a una persona, la cronologia deve essere persistente

>


>[!CAUTION]
>
>All&#39;interno di un flusso di lavoro transitorio non utilizzare un **Passaggio**.
>
>Questo è come il **Passaggio** crea un processo sling per continuare il flusso di lavoro al punto `goto` . In questo modo viene battuto lo scopo di rendere il flusso di lavoro transitorio e viene generato un errore nel file di registro.
>
>Per prendere decisioni in un flusso di lavoro transitorio è possibile utilizzare **OR Split**.

>[!NOTE]
>
>Per ulteriori informazioni sull’impatto dei flussi di lavoro transitori sulle prestazioni delle risorse, consulta [Best practice per le risorse](/help/assets/performance-tuning-guidelines.md#transient-workflows) .

### Supporto risorse multiple {#multi-resource-support}

Attivando **Supporto risorse multiple** per il modello di flusso di lavoro, viene avviata una singola istanza di flusso di lavoro anche quando selezioni più risorse; questi saranno allegati come pacchetto.

Se **Supporto risorse multiple** non è attivato per il modello di flusso di lavoro e sono selezionate più risorse, verrà avviata una singola istanza di flusso di lavoro per ogni risorsa.

>[!NOTE]
>
>Per ulteriori informazioni, consulta [Configurazione di un flusso di lavoro per il supporto di più risorse](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support) .

### Fasi del flusso di lavoro {#workflow-stages}

Le fasi del flusso di lavoro consentono di visualizzare l’avanzamento di un flusso di lavoro durante la gestione delle attività. Possono essere utilizzati per fornire una panoramica della portata del flusso di lavoro durante l’elaborazione, ad esempio quando viene eseguito il flusso di lavoro, e per visualizzare lo stato di avanzamento descritto da **Stage** (anziché da un singolo passaggio).

Poiché i singoli nomi dei passaggi possono essere specifici e tecnici, i nomi degli stadi possono essere definiti in modo da fornire una visione concettuale dell’avanzamento del flusso di lavoro.

Ad esempio, per un flusso di lavoro con sei passaggi e quattro passaggi:

1. Puoi [configurare le fasi del flusso di lavoro (che mostrano l&#39;avanzamento del flusso di lavoro) e quindi assegnare lo stadio appropriato a ogni passaggio del flusso di lavoro](/help/sites-developing/workflows-models.md#configuring-workflow-stages-that-show-workflow-progress):

   * È possibile creare più nomi di stage.
   * A ogni passaggio viene quindi assegnato un nome di singola area di visualizzazione (un nome di area di visualizzazione può essere assegnato a uno o più passaggi).

   | **Nome passaggio** | **Stage (assegnato al passaggio)** |
   |---|---|
   | Passaggio 1 | Crea |
   | Passaggio 2 | Crea |
   | Passaggio 3 | Recensione |
   | Passaggio 4 | Approva |
   | Passaggio 5 | Completa |
   | Passaggio 6 | Completa |

1. Quando il flusso di lavoro viene eseguito, l’utente può visualizzare l’avanzamento in base ai nomi dello stage (anziché ai nomi dei passaggi). L&#39;avanzamento del flusso di lavoro verrà visualizzato nella scheda [INFORMAZIONI FLUSSO DI LAVORO della finestra dei dettagli dell&#39;attività dell&#39;elemento di lavoro](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions) elencato in [Casella in entrata](/help/sites-authoring/inbox.md).

### Flussi di lavoro e Forms {#workflows-and-forms}

In genere, i flussi di lavoro vengono utilizzati per elaborare gli invii dei moduli in AEM. Questo può avvenire con i [componenti core del modulo componenti](https://helpx.adobe.com/experience-manager/core-components/using/form-container.html) disponibili in un&#39;istanza AEM standard o con la [soluzione AEM Forms](/help/forms/using/aem-forms-workflow.md).

Durante la creazione di un nuovo modulo, l’invio del modulo può essere facilmente associato a un modello di flusso di lavoro; ad esempio, per memorizzare il contenuto in una particolare posizione dell’archivio o per informare un utente dell’invio del modulo e del relativo contenuto.

### Flussi di lavoro e traduzione {#workflows-and-translation}

I flussi di lavoro sono anche parte integrante del processo [Traduzione](/help/sites-administering/translation.md).
