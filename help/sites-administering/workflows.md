---
title: Amministrazione dei flussi di lavoro
seo-title: Amministrazione dei flussi di lavoro
description: Scopri come amministrare i flussi di lavoro in AEM.
seo-description: Scopri come amministrare i flussi di lavoro in AEM.
uuid: d000a13c-97cb-4b1b-809e-6c3eb0d675e8
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 4b09cd44-434e-4834-bc0d-c9c082a4ba5a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---


# Amministrazione dei flussi di lavoro{#administering-workflows}

I flussi di lavoro consentono di automatizzare le attività di Adobe Experience Manager (AEM). Flussi di lavoro:

* Consiste in una serie di passaggi eseguiti in un ordine specifico.

   * Ciascuna fase svolge un&#39;attività distinta; ad esempio in attesa di input da parte dell’utente, attivazione di una pagina o invio di un messaggio e-mail.

* Può interagire con le risorse presenti nell’archivio, gli account utente e i servizi AEM.
* Può coordinare attività complesse che coinvolgono qualsiasi aspetto di AEM.

I processi aziendali stabiliti dalla tua organizzazione possono essere rappresentati come flussi di lavoro. Ad esempio, il processo di pubblicazione dei contenuti di un sito Web in genere include passaggi quali l&#39;approvazione e l&#39;accesso da parte di vari soggetti interessati. Questi processi possono essere implementati AEM flussi di lavoro e applicati a pagine e risorse di contenuto.

* [Avvio dei flussi di lavoro](/help/sites-administering/workflows-starting.md)
* [Amministrazione delle istanze dei flussi di lavoro](/help/sites-administering/workflows-administering.md)
* [Gestione dell&#39;accesso ai flussi di lavoro](/help/sites-administering/workflows-managing.md)

>[!NOTE]
>
>Per ulteriori informazioni, consulta:
>
>* Applicazione e partecipazione ai flussi di lavoro: [Lavorare con flussi di lavoro](/help/sites-authoring/workflows.md).
>* Creazione di modelli di workflow ed estensione delle funzionalità dei flussi di lavoro: [Sviluppo ed estensione dei flussi di lavoro](/help/sites-developing/workflows.md).
>* Miglioramento delle prestazioni dei flussi di lavoro che utilizzano importanti risorse server: [Elaborazione flusso di lavoro simultanea](/help/sites-deploying/configuring-performance.md#concurrent-workflow-processing).

>



## Modelli e istanze del flusso di lavoro {#workflow-models-and-instances}

[I ](/help/sites-developing/workflows.md#model) modelli di flusso di lavoro AEM sono la rappresentazione e l&#39;implementazione dei processi aziendali:

* In genere agiscono su pagine o risorse per ottenere un risultato specifico.
* Queste pagine e/o risorse sono denominate payload del flusso di lavoro.
* I modelli di workflow sono composti da una serie di passaggi che eseguono un&#39;attività specifica.
* Il payload viene passato da un passaggio all&#39;altro mentre il flusso di lavoro avanza.

Quando un modello di workflow viene avviato (eseguito), viene creata un&#39;istanza di workflow. Un modello di workflow può essere avviato più volte, ogni volta che si genera un&#39;istanza di workflow distinta. Per ogni istanza, vengono eseguiti i passaggi definiti dal modello di workflow.

>[!CAUTION]
>
>I passaggi eseguiti sono quelli definiti dal modello di flusso di lavoro *al momento della generazione dell&#39;istanza*. Per ulteriori informazioni, vedere [Sviluppo di flussi di lavoro](/help/sites-developing/workflows.md#model).

Le istanze del flusso di lavoro procedono nel seguente ciclo di vita:

1. Il modello del flusso di lavoro viene avviato e viene creata e eseguita un&#39;istanza del flusso di lavoro.

   1. Il payload dell&#39;istanza del flusso di lavoro viene identificato all&#39;avvio del modello.
   1. L&#39;istanza è di fatto una copia del modello (come al momento della creazione).
   1. AEM autori, amministratori o servizi possono avviare modelli di workflow.

1. Viene eseguito il primo passaggio del modello di workflow.
1. Il passaggio viene completato e il motore del flusso di lavoro utilizza il modello per determinare il passaggio successivo da eseguire.
1. I passaggi successivi nel modello di workflow vengono eseguiti e completati.
1. Al termine del passaggio finale, l’istanza del flusso di lavoro viene completata e quindi archiviata.

Sono disponibili numerosi modelli di workflow utili con AEM. Inoltre, gli sviluppatori della vostra organizzazione possono creare modelli di flusso di lavoro personalizzati, in base alle esigenze specifiche dei vostri processi aziendali.

## Passaggi del flusso di lavoro {#workflow-steps}

Quando vengono eseguiti, i passaggi del flusso di lavoro sono associati a un&#39;istanza del flusso di lavoro. La cronologia di un&#39;istanza del flusso di lavoro include informazioni su ogni passaggio eseguito per l&#39;istanza. Queste informazioni sono utili per indagare sui problemi che si verificano durante l&#39;esecuzione.

Un utente o un servizio esegue i passaggi del flusso di lavoro, a seconda del tipo di passaggio:

* Quando un utente esegue un passaggio, gli viene assegnato un elemento di lavoro inserito nella propria casella in entrata. L’utente deve completare manualmente il passaggio in modo che l’istanza del flusso di lavoro continui.
* Quando un servizio esegue un passaggio, al completamento l&#39;istanza del flusso di lavoro procede automaticamente al passaggio successivo.

>[!NOTE]
>
>Se si verifica un errore, l&#39;implementazione di servizio/passaggio deve gestire il comportamento per uno scenario di errore. Il motore del flusso di lavoro stesso riproverà il processo, quindi registrerà un errore e interromperà l&#39;istanza.

## Stato del flusso di lavoro e azioni {#workflow-status-and-actions}

Un flusso di lavoro può avere uno dei seguenti stati:

* **ESECUZIONE**: L&#39;istanza del flusso di lavoro è in esecuzione.
* **COMPLETATO**: L&#39;istanza del flusso di lavoro è stata terminata.

* **SOSPESO**: L&#39;istanza del flusso di lavoro è stata sospesa.
* **ABORTO**: L&#39;istanza del flusso di lavoro è stata terminata.
* **STALLO**: La progressione dell&#39;istanza del flusso di lavoro richiede l&#39;esecuzione di un processo in background, ma il processo non può essere trovato nel sistema. Questa situazione può verificarsi quando si verifica un errore durante l&#39;esecuzione del flusso di lavoro.

>[!NOTE]
>
>Quando l&#39;esecuzione di un passaggio di processo genera errori, il passaggio viene visualizzato nella casella in entrata dell&#39;amministratore e lo stato del flusso di lavoro è **ESECUZIONE**.

A seconda dello stato corrente, potete eseguire azioni sulle istanze del flusso di lavoro in esecuzione quando è necessario intervenire nella progressione normale di un’istanza del flusso di lavoro:

* **Sospendi**: Arresta temporaneamente l&#39;esecuzione del flusso di lavoro. La sospensione è utile in casi eccezionali in cui non si desidera che il flusso di lavoro continui, ad esempio per la manutenzione. La sospensione modifica lo stato del flusso di lavoro in Sospeso.
* **Riprendi**: Riavvia un flusso di lavoro sospeso nello stesso punto di esecuzione in cui è stato sospeso, utilizzando la stessa configurazione.
* **Termina**: Termina l&#39;esecuzione del flusso di lavoro e cambia lo stato in  **ABORTED**. Impossibile riavviare un&#39;istanza del flusso di lavoro interrotta.

