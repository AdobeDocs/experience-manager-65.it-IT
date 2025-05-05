---
title: Sviluppo ed estensione dei flussi di lavoro
description: L’AEM fornisce diversi strumenti e risorse per creare modelli di flusso di lavoro, sviluppare passaggi del flusso di lavoro e interagire in modo programmatico con i flussi di lavoro
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 041b1767-8b6c-4887-a70d-abc96a116976
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1460'
ht-degree: 3%

---


# Sviluppo ed estensione dei flussi di lavoro{#developing-and-extending-workflows}

L’AEM fornisce diversi strumenti e risorse per creare modelli di flusso di lavoro, sviluppare passaggi del flusso di lavoro e interagire in modo programmatico con i flussi di lavoro.

I flussi di lavoro consentono di automatizzare i processi per la gestione delle risorse e la pubblicazione dei contenuti nell’ambiente AEM. I flussi di lavoro sono composti da una serie di passaggi, ognuno dei quali esegue un task discreto. È possibile utilizzare dati logici e di runtime per decidere quando un processo può continuare e selezionare il passaggio successivo da uno dei vari passaggi possibili.

Ad esempio, i processi aziendali per la creazione e la pubblicazione di pagine Web includono attività di approvazione e approvazione da parte di vari partecipanti. Questi processi possono essere modellati utilizzando i flussi di lavoro dell’AEM e applicati a contenuti specifici.

Gli aspetti principali sono trattati di seguito, mentre le pagine che seguono forniscono ulteriori dettagli:

* [Creazione di modelli di flussi di lavoro](/help/sites-developing/workflows-models.md)
* [Estensione della funzionalità per flussi di lavoro](/help/sites-developing/workflows-customizing-extending.md)
* [Interazione con i flussi di lavoro a livello di programmazione](/help/sites-developing/workflows-program-interaction.md)
* [Guida di riferimento per i passaggi dei flussi di lavoro](/help/sites-developing/workflows-step-ref.md)
* [Guida di riferimento per il processo dei flusso di lavoro](/help/sites-developing/workflows-process-ref.md)
* [Best practice per i flussi di lavoro](/help/sites-developing/workflows-best-practices.md)

>[!NOTE]
>
>Per informazioni su:
>
>* Partecipazione ai flussi di lavoro, vedi [Utilizzo dei flussi di lavoro](/help/sites-authoring/workflows.md).
>* Per l&#39;amministrazione dei flussi di lavoro e delle istanze dei flussi di lavoro, vedere [Amministrazione dei flussi di lavoro](/help/sites-administering/workflows.md).
>* Per un articolo della community end-to-end, vedi [Modifica di Digital Assets tramite i flussi di lavoro di Adobe Experience Manager.](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-workflow.html?lang=it)
>* Guarda il webinar [Ask the AEM Experts webinar on Workflows](https://communities.adobeconnect.com/p5s33iburd54/) (Domande agli esperti sui flussi di lavoro).
>* Le modifiche alle posizioni delle informazioni sono riportate in [Ristrutturazione dell&#39;archivio in AEM 6.5](/help/sites-deploying/repository-restructuring.md) e [Best practice per i flussi di lavoro - Posizioni](/help/sites-developing/workflows-best-practices.md#locations).
>

## Modello {#model}

Un `WorkflowModel` rappresenta una definizione (modello) di un flusso di lavoro. È composto da `WorkflowNodes` e `WorkflowTransitions`. Le transizioni connettono i nodi e definiscono il *flusso*. Il modello ha sempre un nodo iniziale e un nodo finale.

### Modello runtime {#runtime-model}

I modelli di flusso di lavoro sono dotati di versione. Quando esegui un’istanza di flusso di lavoro, questa utilizza e mantiene il modello di runtime del flusso di lavoro, come disponibile al momento in cui il flusso di lavoro è stato avviato.

Un modello runtime è [generato quando **Sync** viene attivato nell&#39;editor modelli flusso di lavoro](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model).

Le modifiche al modello di flusso di lavoro che si verificano o ai modelli di runtime generati, o a entrambi, *dopo* l&#39;avvio dell&#39;istanza specifica non vengono applicate a tale istanza.

>[!CAUTION]
>
>I passaggi eseguiti sono definiti dal [modello di runtime](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model), generato al momento dell&#39;attivazione dell&#39;azione **Sync** nell&#39;editor modelli di flusso di lavoro.
>
>Se il modello di flusso di lavoro viene modificato dopo questo momento (senza che **Sync** venga attivato), l&#39;istanza di runtime non riflette tali modifiche. Solo i modelli di runtime generati dopo l’aggiornamento riflettono le modifiche. Le eccezioni sono gli script ECMA sottostanti, che vengono mantenuti una sola volta in modo che tali modifiche vengano apportate.

### Passaggio {#step}

Ogni fase esegue un&#39;attività discreta. Esistono diversi tipi di passaggi del flusso di lavoro:

* Partecipante (utente/gruppo): questi passaggi generano un elemento di lavoro e lo assegnano a un utente o a un gruppo. Per far avanzare il flusso di lavoro, l’utente deve completare l’elemento di lavoro.
* Processo (script, chiamata al metodo Java™): questi passaggi vengono eseguiti automaticamente dal sistema. Uno script ECMA o una classe Java™ implementa il passaggio. I servizi possono essere sviluppati per ascoltare eventi speciali del flusso di lavoro ed eseguire attività in base alla logica di business.
* Contenitore (flusso di lavoro secondario): questo tipo di passaggio avvia un altro modello di flusso di lavoro.
* OR Split/Join: utilizza la logica per decidere quale passaggio eseguire successivamente nel flusso di lavoro.
* AND Split/Join: consente l&#39;esecuzione simultanea di più passaggi.

Tutti i passaggi condividono le seguenti proprietà comuni: `Autoadvance` e `Timeout` avvisi (scriptable).

### Transizione {#transition}

Un `WorkflowTransition` rappresenta una transizione tra due `WorkflowNodes` di un `WorkflowModel`.

* Definisce il collegamento tra due passaggi consecutivi.
* È possibile applicare delle regole.

### Elemento di lavoro {#workitem}

Un `WorkItem` è l&#39;unità passata tramite un&#39;istanza `Workflow` di un `WorkflowModel`. Contiene `WorkflowData` su cui agisce l&#39;istanza e un riferimento a `WorkflowNode` che descrive il passaggio del flusso di lavoro sottostante.

* Viene utilizzato per identificare l’attività e viene inserito nella rispettiva casella in entrata.
* Un&#39;istanza di flusso di lavoro può avere uno o più `WorkItems` contemporaneamente (a seconda del modello di flusso di lavoro).
* `WorkItem` fa riferimento all&#39;istanza del flusso di lavoro.
* Nell&#39;archivio, `WorkItem` è memorizzato sotto l&#39;istanza del flusso di lavoro.

### Payload {#payload}

Fa riferimento alla risorsa che deve essere avanzata tramite un flusso di lavoro.

L’implementazione del payload fa riferimento a una risorsa nell’archivio (per percorso, UUID o URL) o da un oggetto Java™ serializzato. Il riferimento a una risorsa nell’archivio è flessibile e produttivo, con sling produttivo. Ad esempio, è possibile eseguire il rendering del nodo a cui si fa riferimento come modulo.

### Ciclo di vita {#lifecycle}

Viene creato all’avvio di un nuovo flusso di lavoro (scegliendo il rispettivo modello di flusso di lavoro e definendo il payload) e termina quando il nodo finale viene elaborato.

In un’istanza di flusso di lavoro sono possibili le seguenti azioni:

* Termina
* Sospendi
* Riprendi
* Riavvia

Le istanze completate e terminate vengono archiviate.

### Casella in entrata {#inbox}

Ogni account utente dispone di una propria casella in entrata del flusso di lavoro in cui sono accessibili i `WorkItems` assegnati.

I `WorkItems` sono assegnati direttamente all&#39;account utente o al gruppo a cui appartengono.

### Tipi di flusso di lavoro {#workflow-types}

Esistono vari tipi di flusso di lavoro, come indicato nella console Modelli di flusso di lavoro:

![wf-upgrade-03](assets/wf-upgraded-03.png)

* **Predefinito**

  Questi tipi sono i flussi di lavoro predefiniti inclusi in un’istanza AEM standard.

* Flussi di lavoro personalizzati (nessun indicatore nella console)

  Questi flussi di lavoro sono stati creati come nuovi o da flussi di lavoro predefiniti che sono stati sovrapposti con le personalizzazioni.

* **Legacy**

  Flussi di lavoro creati in una versione precedente dell’AEM. Questi flussi di lavoro possono essere mantenuti durante un aggiornamento, oppure esportati come pacchetto di flusso di lavoro dalla versione precedente, quindi importati nella nuova versione.

### Flussi di lavoro transitori {#transient-workflows}

I flussi di lavoro standard salvano le informazioni di runtime (cronologia) durante l’esecuzione. Puoi anche definire un modello di flusso di lavoro come **Transitorio** per evitare che la cronologia venga mantenuta. Questo flusso di lavoro viene utilizzato per l&#39;ottimizzazione delle prestazioni, in quanto consente di risparmiare tempo e risorse utilizzati per la persistenza delle informazioni.

I flussi di lavoro transitori possono essere utilizzati per qualsiasi flusso di lavoro che:

* vengono eseguiti spesso.
* non è necessaria la cronologia del flusso di lavoro.

Sono stati introdotti flussi di lavoro transitori per il caricamento di molte risorse, in cui le informazioni sulle risorse sono importanti, ma non la cronologia di runtime del flusso di lavoro.

>[!NOTE]
>
>Per ulteriori dettagli, vedere [Creazione di un flusso di lavoro transitorio](/help/sites-developing/workflows-models.md#creating-a-transient-workflow).

>[!CAUTION]
>
>Quando un modello di flusso di lavoro è contrassegnato come transitorio, esistono alcuni scenari in cui le informazioni di runtime devono essere ancora persistenti:
>
>* Il tipo di payload (ad esempio, video) richiede passaggi esterni per l’elaborazione; in questi casi, per la conferma dello stato è necessaria la cronologia di runtime.
>* Il flusso di lavoro immette una suddivisione **AND**. In questi casi, per la conferma dello stato è necessaria la cronologia di runtime.
>* Quando il flusso di lavoro transitorio entra in un passaggio partecipante, in fase di esecuzione passa alla modalità non transitorio. Poiché l’attività viene passata a una persona, la cronologia deve essere persistente.
>

>[!CAUTION]
>
>All&#39;interno di un flusso di lavoro transitorio, non utilizzare un **Passaggio precedente**.
>
>Il motivo è che il **passaggio Vai** crea un processo Sling per continuare il flusso di lavoro al punto `goto`. Tale operazione vanifica lo scopo di rendere transitorio il flusso di lavoro e genera un errore nel file di registro.
>
>Utilizza **OR Split** per effettuare scelte all&#39;interno di un flusso di lavoro transitorio.

>[!NOTE]
>
>Consulta [Best practice per Assets](/help/assets/performance-tuning-guidelines.md#transient-workflows) per ulteriori informazioni sull&#39;impatto dei flussi di lavoro transitori sulle prestazioni delle risorse.

### Supporto risorse multiple {#multi-resource-support}

L&#39;attivazione di **Supporto risorse multiple** per il modello di flusso di lavoro comporta l&#39;avvio di una singola istanza di flusso di lavoro anche quando si selezionano più risorse. Ciascuno è allegato come pacchetto.

Se **Supporto risorse multiple** non è attivato per il modello di flusso di lavoro e sono selezionate più risorse, viene avviata una singola istanza di flusso di lavoro per ogni risorsa.

>[!NOTE]
>
>Per ulteriori dettagli, vedere [Configurazione di un flusso di lavoro per Supporto risorse multiple](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support).

### Fasi flusso di lavoro {#workflow-stages}

Le fasi del flusso di lavoro consentono di visualizzare l’avanzamento di un flusso di lavoro durante la gestione delle attività. Possono essere utilizzati per fornire una panoramica della distanza del flusso di lavoro attraverso l’elaborazione. Durante l&#39;esecuzione del flusso di lavoro, l&#39;utente può visualizzare l&#39;avanzamento descritto da **Fase** (anziché da un singolo passaggio).

Poiché i singoli nomi di fase possono essere specifici e tecnici, è possibile definirli per fornire una visione concettuale dell’avanzamento del flusso di lavoro.

Ad esempio, per un flusso di lavoro con sei passaggi e quattro fasi:

1. È possibile [configurare le fasi del flusso di lavoro (che mostrano l&#39;avanzamento del flusso di lavoro) e quindi assegnare la fase appropriata a ogni passaggio del flusso di lavoro](/help/sites-developing/workflows-models.md#configuring-workflow-stages-that-show-workflow-progress):

   * È possibile creare più nomi di fase.
   * A ogni passo viene quindi assegnato un nome di stadio (un nome di stadio può essere assegnato a uno o più passi).

   | **Nome passaggio** | **Fase (assegnata al passaggio)** |
   |---|---|
   | Passaggio 1 | Creare |
   | Passaggio 2 | Creare |
   | Passaggio 3 | Rivedi |
   | Passaggio 4 | Approva |
   | Passaggio 5 | Completato |
   | Passaggio 6 | Completato |

1. Quando il flusso di lavoro viene eseguito, l’utente può visualizzare l’avanzamento in base ai nomi degli stadi (anziché ai nomi dei passaggi). L&#39;avanzamento del flusso di lavoro viene visualizzato nella scheda [INFORMAZIONI FLUSSO DI LAVORO della finestra dei dettagli attività dell&#39;elemento del flusso di lavoro](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions) elencato nella [Posta in arrivo](/help/sites-authoring/inbox.md).

### Flussi di lavoro e Forms {#workflows-and-forms}

In genere, i flussi di lavoro vengono utilizzati per elaborare l’invio dei moduli in AEM. Può essere con i [componenti core modulo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-container.html?lang=it) disponibili in un&#39;istanza AEM standard o con la [soluzione AEM Forms](/help/forms/using/aem-forms-workflow.md).

Durante la creazione di un modulo, l’invio del modulo può essere facilmente associato a un modello di flusso di lavoro. Ad esempio, per archiviare il contenuto in una posizione specifica del repository o per notificare a un utente l&#39;invio del modulo e il relativo contenuto.

### Flussi di lavoro e traduzione {#workflows-and-translation}

I flussi di lavoro fanno anche parte del processo [Traduzione](/help/sites-administering/translation.md).
