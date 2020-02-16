---
title: Sviluppo ed estensione dei flussi di lavoro
seo-title: Sviluppo ed estensione dei flussi di lavoro
description: AEM offre diversi strumenti e risorse per la creazione di modelli di workflow, lo sviluppo di passaggi di workflow e l’interazione programmatica con i flussi di lavoro
seo-description: AEM offre diversi strumenti e risorse per la creazione di modelli di workflow, lo sviluppo di passaggi di workflow e l’interazione programmatica con i flussi di lavoro
uuid: 5a857589-3b13-4519-bda2-b1dab6005550
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 8954e3df-3afa-4d53-a7e1-255f3b8f499f
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6

---


# Sviluppo ed estensione dei flussi di lavoro{#developing-and-extending-workflows}

AEM offre diversi strumenti e risorse per la creazione di modelli di workflow, lo sviluppo di passaggi di workflow e l’interazione programmatica con i flussi di lavoro.

I flussi di lavoro consentono di automatizzare i processi per la gestione delle risorse e la pubblicazione dei contenuti nell’ambiente AEM. I flussi di lavoro sono composti da una serie di passaggi, ciascuno dei quali esegue un&#39;attività discreta. È possibile utilizzare i dati di logica e runtime per decidere quando continuare un processo e selezionare il passaggio successivo da uno dei diversi passaggi possibili.

Ad esempio, i processi aziendali per la creazione e la pubblicazione di pagine Web includono le attività di approvazione e di disconnessione di vari partecipanti. Questi processi possono essere modellati utilizzando i flussi di lavoro AEM e applicati a contenuti specifici.

Gli aspetti chiave sono trattati di seguito, mentre le pagine seguenti descrivono ulteriori dettagli:

* [Creazione di modelli di flussi di lavoro](/help/sites-developing/workflows-models.md)
* [Estensione della funzionalità del flusso di lavoro](/help/sites-developing/workflows-customizing-extending.md)
* [Interazione con flussi di lavoro a livello di programmazione](/help/sites-developing/workflows-program-interaction.md)
* [Riferimento passo flusso di lavoro](/help/sites-developing/workflows-step-ref.md)
* [Riferimento processo di workflow](/help/sites-developing/workflows-process-ref.md)
* [Best practice per i flussi di lavoro](/help/sites-developing/workflows-best-practices.md)

>[!NOTE]
>
>Per informazioni su:
>
>* Partecipare ai flussi di lavoro, vedere [Uso dei flussi di lavoro](/help/sites-authoring/workflows.md).
>* Amministrazione dei flussi di lavoro e delle istanze dei flussi di lavoro, consulta [Amministrazione dei flussi di lavoro](/help/sites-administering/workflows.md).
>* Per un articolo della community end-to-end, consultate [Modifica delle risorse digitali tramite flussi di lavoro Adobe Experience Manager.](https://helpx.adobe.com/experience-manager/using/modify_asset_workflow.html)
>* Consultate il webinar [Ask the AEM Experts on Workflows (Chiedi agli esperti di AEM sui flussi di lavoro)](https://bit.ly/ATACE218).
>* Per un articolo della community end-to-end, consultate [Creazione di un passaggio](https://helpx.adobe.com/experience-manager/using/dynamic-steps-aem63.html)personalizzato per i partecipanti dinamici di Adobe Experience Manager 6.3.
>* Modifiche alle posizioni delle informazioni consultate Ristrutturazione [repository in AEM 6.5](/help/sites-deploying/repository-restructuring.md) e Best practice per i [flussi di lavoro - Posizioni](/help/sites-developing/workflows-best-practices.md#locations).
>



## Modello {#model}

Un elemento `WorkflowModel` rappresenta una definizione (modello) di un flusso di lavoro. È fatta di `WorkflowNodes` e `WorkflowTransitions`. Le transizioni collegano i nodi e definiscono il *flusso*. Il modello ha sempre un nodo iniziale e un nodo finale.

### Modello runtime {#runtime-model}

I modelli di workflow sono dotati di versioni. Quando si esegue un&#39;istanza di workflow, verrà utilizzato (e mantenuto) il modello runtime del flusso di lavoro (come disponibile al momento dell&#39;avvio del flusso di lavoro).

Un modello runtime viene [generato quando si attiva la **sincronizzazione** nell&#39;editor](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model)del modello di workflow.

Le modifiche al modello di flusso di lavoro che si verificano e/o ai modelli di runtime generati, *dopo* l&#39;avvio dell&#39;istanza specifica non verranno applicate all&#39;istanza.

>[!CAUTION]
>
>Le fasi eseguite sono quelle definite dal modello [](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model)runtime; questo viene generato al momento dell&#39;attivazione dell&#39;azione **Sinc** nell&#39;editor del modello di workflow.
>
>Se il modello del flusso di lavoro viene modificato dopo questo momento (senza attivare la **sincronizzazione** ), l&#39;istanza runtime non riflette tali modifiche. Solo i modelli di runtime generati dopo l&#39;aggiornamento rifletteranno le modifiche. Le eccezioni sono gli script ECMA sottostanti, che vengono conservati solo una volta apportate le modifiche.

### Incremento {#step}

Ciascun passaggio esegue un task discreto. Esistono diversi tipi di passaggi per il flusso di lavoro:

* Partecipante (utente/gruppo): Questi passaggi generano un elemento di lavoro e lo assegnano a un utente o a un gruppo. Un utente deve completare l’elemento di lavoro per far avanzare il flusso di lavoro.
* Processo (script, chiamata del metodo Java): Questi passaggi vengono eseguiti automaticamente dal sistema. Uno script ECMA o una classe Java implementa il passaggio. I servizi possono essere sviluppati per ascoltare eventi di flusso di lavoro speciali ed eseguire attività in base alla logica aziendale.
* Contenitore (flusso di lavoro secondario): Questo tipo di passaggio avvia un altro modello di workflow.
* O Dividi/Unisci: Utilizzare la logica per decidere quale passaggio eseguire successivamente nel flusso di lavoro.
* Dividi/Iscriviti: Consente l&#39;esecuzione simultanea di più passaggi.

Tutti i passaggi condividono le seguenti proprietà comuni: `Autoadvance` e `Timeout` avvisi (script).

### Transizione {#transition}

Un `WorkflowTransition` rappresenta una transizione tra due `WorkflowNodes` di `WorkflowModel`.

* Definisce il collegamento tra due passaggi consecutivi.
* È possibile applicare delle regole.

### Elemento di lavoro {#workitem}

Un `WorkItem` è l&#39;unità che viene passata attraverso un&#39; `Workflow` istanza di un `WorkflowModel`. Contiene il `WorkflowData` fatto che l’istanza agisce e un riferimento al passaggio del flusso di lavoro sottostante `WorkflowNode` che descrive il passaggio del flusso di lavoro sottostante.

* Viene utilizzato per identificare l’attività e viene inserito nella rispettiva inbox.
* Un’istanza di workflow può avere uno o più `WorkItems` contemporaneamente (a seconda del modello di workflow).
* Fa riferimento `WorkItem` all’istanza del flusso di lavoro.
* Nella directory archivio il file `WorkItem` viene memorizzato sotto l’istanza del flusso di lavoro.

### Payload {#payload}

Fa riferimento alla risorsa da aggiornare tramite un flusso di lavoro.

L&#39;implementazione del payload fa riferimento a una risorsa nell&#39;archivio (per percorso, UUID o URL) o da un oggetto Java serializzato. Il riferimento a una risorsa nell&#39;archivio è molto flessibile e in combinazione con l&#39;imbragatura molto produttiva; ad esempio, è possibile eseguire il rendering del nodo di riferimento come modulo.

### Ciclo {#lifecycle}

Viene creato quando si avvia un nuovo flusso di lavoro (scegliendo il modello di flusso di lavoro corrispondente e definendo il payload) e termina quando viene elaborato il nodo finale.

In un’istanza del flusso di lavoro è possibile effettuare le seguenti operazioni:

* Termina
* Sospendi
* Riprendi
* Riavvia

Le istanze completate e terminate vengono archiviate.

### Casella in entrata {#inbox}

Ogni account utente dispone di una propria casella in entrata del flusso di lavoro in cui `WorkItems` sono accessibili le relative risorse.

Le proprietà `WorkItems` vengono assegnate direttamente all&#39;account utente o al gruppo al quale appartengono.

### Tipi di flussi di lavoro {#workflow-types}

Esistono vari tipi di flussi di lavoro, come indicato nella console Modelli flusso di lavoro:

![wf-aggiornato-03](assets/wf-upgraded-03.png)

* **Impostazione predefinita**

   Questi sono i flussi di lavoro forniti con il prodotto, inclusi in un’istanza standard di AEM.

* Flussi di lavoro personalizzati (nessun indicatore nella console)

   Si tratta di flussi di lavoro creati come nuovi o da flussi di lavoro forniti con le personalizzazioni.

* **Legacy**

   Flussi di lavoro creati con una versione precedente di AEM. Questi possono essere mantenuti durante un aggiornamento o esportati come pacchetto di workflow dalla versione precedente, quindi importati nella nuova versione.

### Flussi di lavoro transitori {#transient-workflows}

I flussi di lavoro standard salvano le informazioni di runtime (cronologia) durante la loro esecuzione. Potete anche definire un modello di workflow come **Temporaneo** per evitare che tale cronologia venga mantenuta. Questa funzione è utilizzata per ottimizzare le prestazioni in modo da risparmiare/evitare il tempo/le risorse utilizzati per mantenere le informazioni.

I flussi di lavoro transitori possono essere utilizzati per qualsiasi flusso di lavoro che:

* vengono eseguite spesso.
* non è necessaria la cronologia del flusso di lavoro.

Sono stati introdotti flussi di lavoro transitori per il caricamento di un gran numero di risorse, dove le informazioni sulle risorse sono importanti, ma non la cronologia del runtime del flusso di lavoro.

>[!NOTE]
>
>Per ulteriori informazioni, consultate [Creazione di un flusso di lavoro](/help/sites-developing/workflows-models.md#creating-a-transient-workflow) transitorio.

>[!CAUTION]
>
>Quando un modello di workflow è stato contrassegnato come Temporaneo, esistono alcuni scenari in cui le informazioni di runtime rimarranno persistenti:
>
>* Il tipo di payload (ad esempio, video) richiede passaggi esterni per l&#39;elaborazione; in tali casi, la cronologia del runtime è necessaria per la conferma dello stato.
>* Il flusso di lavoro entra in un **AND Split**; in tali casi, la cronologia del runtime è necessaria per la conferma dello stato.
>* Quando il flusso di lavoro transitorio entra in un passaggio partecipante, cambia la modalità (in fase di esecuzione) in non transitoria; mentre l&#39;attività viene passata a una persona, la storia deve essere persistente
>



>[!CAUTION]
>
>All&#39;interno di un flusso di lavoro transitorio non è necessario utilizzare un **passaggio** Goto.
>
>Questo accade perché **Goto Step** crea un processo Sling per continuare il flusso di lavoro al `goto` punto. In questo modo viene ignorato lo scopo di rendere il flusso di lavoro transitorio e viene generato un errore nel file di registro.
>
>Per prendere decisioni in un flusso di lavoro transitorio è possibile utilizzare la divisione **** OR.

>[!NOTE]
>
>Per ulteriori informazioni sull’impatto dei flussi di lavoro transitori sulle prestazioni delle risorse, consultate [Best practice per le risorse](/help/assets/performance-tuning-guidelines.md#transient-workflows) .

### Supporto risorse multiple {#multi-resource-support}

Attivando il supporto **per risorse** multiple per il modello di flusso di lavoro, verrà avviata una singola istanza del flusso di lavoro anche quando si selezionano più risorse; verranno allegati come pacchetto.

Se il supporto **per risorse** multiple non è attivato per il modello di flusso di lavoro e sono selezionate più risorse, verrà avviata una singola istanza del flusso di lavoro per ciascuna risorsa.

>[!NOTE]
>
>Per ulteriori informazioni, consulta [Configurazione di un flusso di lavoro per Supporto](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support) risorse multiple.

### Fasi del flusso di lavoro {#workflow-stages}

Le fasi del flusso di lavoro consentono di visualizzare l’avanzamento di un flusso di lavoro durante la gestione delle attività. Possono essere utilizzati per fornire una panoramica della portata del flusso di lavoro attraverso l&#39;elaborazione, ad esempio quando il flusso di lavoro viene eseguito, l&#39;utente può visualizzare i progressi descritti da **Stage** (anziché da un singolo passaggio).

Poiché i singoli nomi dei passaggi possono essere specifici e tecnici, i nomi degli stage possono essere definiti per fornire una visione concettuale dell’avanzamento del flusso di lavoro.

Ad esempio, per un flusso di lavoro con sei fasi e quattro fasi:

1. Potete [configurare le fasi del flusso di lavoro (che mostrano l’avanzamento del flusso di lavoro) e quindi assegnare lo stadio appropriato a ciascun passaggio del flusso di lavoro](/help/sites-developing/workflows-models.md#configuring-workflow-stages-that-show-workflow-progress):

   * È possibile creare più nomi di fase.
   * A ogni passaggio viene quindi assegnato un singolo nome di fase (un nome di fase può essere assegnato a uno o più passaggi).
   | **Nome passo** | **Stage (assegnato al passaggio)** |
   |---|---|
   | Passaggio 1 | Crea |
   | Passaggio 2 | Crea |
   | Passaggio 3 | Recensione |
   | Passaggio 4 | Approva |
   | Passaggio 5 | Completa |
   | Passaggio 6 | Completa |

1. Quando il flusso di lavoro viene eseguito, l&#39;utente può visualizzare l&#39;avanzamento in base ai nomi dello stage (invece dei nomi dei passaggi). L&#39;avanzamento del flusso di lavoro verrà visualizzato nella scheda [WORKFLOW INFO della finestra dei dettagli dell&#39;attività dell&#39;elemento](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions) di lavoro elencato nella [Casella in entrata](/help/sites-authoring/inbox.md).

### Flussi di lavoro e moduli {#workflows-and-forms}

In genere, i flussi di lavoro vengono utilizzati per elaborare gli invii di moduli in AEM. Può trattarsi dei componenti [core dei componenti](https://helpx.adobe.com/experience-manager/core-components/using/form-container.html) modulo disponibili in un’istanza standard di AEM o con la soluzione [](/help/forms/using/aem-forms-workflow.md)AEM Forms.

Durante la creazione di un nuovo modulo, l&#39;invio del modulo può essere facilmente associato a un modello di workflow; ad esempio per memorizzare il contenuto in una determinata posizione dell&#39;archivio o per notificare all&#39;utente l&#39;invio del modulo e il relativo contenuto.

### Flussi di lavoro e traduzione {#workflows-and-translation}

I flussi di lavoro sono anche parte integrante del processo di [traduzione](/help/sites-administering/translation.md) .
