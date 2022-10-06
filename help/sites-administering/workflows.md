---
title: Amministrazione dei flussi di lavoro
seo-title: Administering Workflows
description: Scopri come amministrare i flussi di lavoro in AEM.
seo-description: Learn how to administer workflows in AEM.
uuid: d000a13c-97cb-4b1b-809e-6c3eb0d675e8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 4b09cd44-434e-4834-bc0d-c9c082a4ba5a
exl-id: 10eecfb8-d43d-4f01-9778-87c752dee64c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 2%

---

# Amministrazione dei flussi di lavoro{#administering-workflows}

I flussi di lavoro consentono di automatizzare le attività di Adobe Experience Manager (AEM). Flussi di lavoro:

* È costituito da una serie di passaggi eseguiti in un ordine specifico.

   * Ogni passaggio esegue un’attività distinta; come l’attesa dell’input dell’utente, l’attivazione di una pagina o l’invio di un messaggio e-mail.

* Può interagire con le risorse nell’archivio, gli account utente e i servizi AEM.
* Può coordinare attività complesse che coinvolgono qualsiasi aspetto del AEM.

I processi aziendali stabiliti dalla tua organizzazione possono essere rappresentati come flussi di lavoro. Ad esempio, il processo di pubblicazione dei contenuti del sito web include in genere passaggi quali l’approvazione e l’approvazione da parte di vari soggetti interessati. Questi processi possono essere implementati come flussi di lavoro AEM e applicati a pagine di contenuto e risorse.

* [Avvio dei flussi di lavoro](/help/sites-administering/workflows-starting.md)
* [Amministrazione delle istanze dei flussi di lavoro](/help/sites-administering/workflows-administering.md)
* [Gestione dell’accesso ai flussi di lavoro](/help/sites-administering/workflows-managing.md)

>[!NOTE]
>
>Per ulteriori informazioni, consulta:
>
>* Applicazione e partecipazione ai flussi di lavoro: [Utilizzo dei flussi di lavoro](/help/sites-authoring/workflows.md).
>* Creazione di modelli di flusso di lavoro ed estensione della funzionalità del flusso di lavoro: [Sviluppo ed estensione dei flussi di lavoro](/help/sites-developing/workflows.md).
>* Miglioramento delle prestazioni dei flussi di lavoro che utilizzano risorse server significative: [Elaborazione simultanea del flusso di lavoro](/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing).
>


## Modelli e istanze di flussi di lavoro {#workflow-models-and-instances}

[Modelli di flusso di lavoro](/help/sites-developing/workflows.md#model) AEM sono la rappresentazione e l&#39;implementazione dei processi aziendali:

* In genere agiscono su pagine o risorse per ottenere un risultato specifico.
* Queste pagine e/o risorse sono denominate payload del flusso di lavoro.
* I modelli di flusso di lavoro consistono in una serie di passaggi che eseguono un&#39;attività specifica.
* Il payload viene passato da un passaggio all’altro mentre il flusso di lavoro progredisce.

Quando viene avviato (eseguito) un modello di flusso di lavoro, viene creata un’istanza di flusso di lavoro. Un modello di flusso di lavoro può essere avviato più volte, ogni volta che si genera un’istanza di flusso di lavoro distinta. Per ogni istanza, vengono eseguiti i passaggi definiti dal modello di flusso di lavoro.

>[!CAUTION]
>
>I passaggi eseguiti sono quelli definiti dal modello di flusso di lavoro *al momento della generazione dell’istanza*. Vedi [Sviluppo dei flussi di lavoro](/help/sites-developing/workflows.md#model) per ulteriori dettagli.

Le istanze del flusso di lavoro procedono nel seguente ciclo di vita:

1. Il modello di flusso di lavoro viene avviato e viene creata e eseguita un’istanza di flusso di lavoro.

   1. Il payload dell’istanza del flusso di lavoro viene identificato all’avvio del modello.
   1. L&#39;istanza è effettivamente una copia del modello (come al momento della creazione).
   1. AEM autori, amministratori o servizi possono avviare modelli di flusso di lavoro.

1. Viene eseguito il primo passaggio del modello di flusso di lavoro.
1. Il passaggio viene completato e il motore del flusso di lavoro utilizza il modello per determinare il passaggio successivo da eseguire.
1. I passaggi successivi nel modello di flusso di lavoro vengono eseguiti e completati.
1. Una volta completato il passaggio finale, l’istanza del flusso di lavoro viene completata e quindi archiviata.

Vengono forniti molti modelli di flusso di lavoro utili con AEM. Inoltre, gli sviluppatori della tua organizzazione possono creare modelli di flusso di lavoro personalizzati, personalizzati in base alle esigenze specifiche dei tuoi processi aziendali.

## Passaggi del flusso di lavoro {#workflow-steps}

Quando i passaggi del flusso di lavoro vengono eseguiti, sono associati a un’istanza di flusso di lavoro. La cronologia di un&#39;istanza di flusso di lavoro include informazioni su ogni passaggio eseguito per l&#39;istanza. Queste informazioni sono utili per indagare i problemi che si verificano durante l’esecuzione.

Un utente o un servizio esegue passaggi del flusso di lavoro, a seconda del tipo di passaggio:

* Quando un utente esegue un passaggio, gli viene assegnato un elemento di lavoro inserito nella propria casella in entrata. L’utente è responsabile del completamento manuale del passaggio in modo che l’istanza del flusso di lavoro progredisca.
* Quando un servizio esegue un passaggio, al completamento l&#39;istanza del flusso di lavoro procede automaticamente al passaggio successivo.

>[!NOTE]
>
>Se si verifica un errore, l’implementazione del servizio/passaggio deve gestire il comportamento per uno scenario di errore. Il motore del flusso di lavoro stesso riproverà il processo, quindi registrerà un errore e interromperà l’istanza.

## Stato e azioni del flusso di lavoro {#workflow-status-and-actions}

Un flusso di lavoro può avere uno dei seguenti stati:

* **IN ESECUZIONE**: L’istanza del flusso di lavoro è in esecuzione.
* **COMPLETATO**: L&#39;istanza del flusso di lavoro è stata terminata.

* **SOSPESO**: Segna il flusso di lavoro come sospeso. Tuttavia, consulta la nota di attenzione riportata di seguito su un problema relativo a questo stato.
* **ABORTO**: L&#39;istanza del flusso di lavoro è stata terminata.
* **SCALA**: La progressione dell&#39;istanza del flusso di lavoro richiede l&#39;esecuzione di un processo in background, tuttavia il processo non può essere trovato nel sistema. Questa situazione può verificarsi quando si verifica un errore durante l’esecuzione del flusso di lavoro.

>[!NOTE]
>
>Quando l&#39;esecuzione di un passaggio del processo genera errori, il passaggio viene visualizzato nella casella in entrata dell&#39;amministratore e lo stato del flusso di lavoro è **IN ESECUZIONE**.

A seconda dello stato corrente, è possibile eseguire azioni sulle istanze del flusso di lavoro in esecuzione quando è necessario intervenire nella normale progressione di un’istanza di flusso di lavoro:

* **Sospendi**: La sospensione modifica lo stato del flusso di lavoro in Sospeso. Vedi Cautela di seguito:

>[!CAUTION]
>
>Il problema noto è se si contrassegna uno stato del flusso di lavoro come &quot;Sospendi&quot;. In questo stato è possibile intervenire sugli elementi del flusso di lavoro sospeso in una casella in entrata.

* **Riprendi**: Riavvia un flusso di lavoro sospeso nello stesso punto di esecuzione in cui è stato sospeso, utilizzando la stessa configurazione.
* **Termina**: Termina l’esecuzione del flusso di lavoro e cambia lo stato in **ABORTO**. Impossibile riavviare un&#39;istanza di flusso di lavoro interrotta.
