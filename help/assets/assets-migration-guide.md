---
title: Migrare le risorse in blocco
description: Descrive come inserire risorse in  [!DNL Adobe Experience Manager], applicare metadati, generare rappresentazioni e attivarle nelle istanze di pubblicazione.
contentOwner: AG
role: Architect, Admin
feature: Migration,Renditions,Asset Management
exl-id: 184f1645-894a-43c1-85f5-8e0d2d77aa73
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1739'
ht-degree: 6%

---

# Migrazione di risorse in blocco {#assets-migration-guide}

Durante la migrazione delle risorse in [!DNL Adobe Experience Manager], è necessario prendere in considerazione diversi passaggi. L&#39;estrazione di risorse e metadati dalla home corrente esula dall&#39;ambito di questo documento in quanto varia ampiamente tra le implementazioni, ma questo documento descrive come inserire queste risorse in [!DNL Experience Manager], applicarne i metadati, generare rappresentazioni e attivarle per pubblicare le istanze.

## Prerequisiti {#prerequisites}

Prima di eseguire effettivamente uno dei passaggi di questa metodologia, rivedere e implementare le linee guida in [suggerimenti per l&#39;ottimizzazione delle prestazioni di Assets](performance-tuning-guidelines.md). Molti dei passaggi, come la configurazione del numero massimo di processi simultanei, migliorano notevolmente la stabilità del server e le prestazioni sotto carico. Altri passaggi, come la configurazione di un archivio dati file, sono molto più difficili da eseguire dopo il caricamento del sistema con le risorse.

>[!NOTE]
>
>I seguenti strumenti di migrazione delle risorse non fanno parte di [!DNL Experience Manager] e non sono supportati da Adobe:
>
>* ACS AEM Tools Tag Maker
>* Importazione risorse CSV strumenti AEM ACS
>* Gestione flusso di lavoro in blocco ACS Commons
>* ACS Commons Fast Action Manager
>* Flusso di lavoro sintetico
>
>Questo software è open source ed è coperto dalla [Licenza Apache v2](https://adobe-consulting-services.github.io/pages/license.html). Per porre una domanda o segnalare un problema, visita rispettivamente [GitHub Issues for ACS AEM Tools](https://github.com/Adobe-Consulting-Services/acs-aem-commons/issues) e [ACS AEM Commons](https://github.com/Adobe-Consulting-Services/acs-aem-tools/issues).

## Migra a [!DNL Experience Manager] {#migrating-to-aem}

La migrazione delle risorse a [!DNL Experience Manager] richiede diversi passaggi e deve essere vista come un processo graduale. Le fasi della migrazione sono le seguenti:

1. Disattiva i flussi di lavoro.
1. Carica i tag.
1. Acquisire le risorse.
1. Elabora rappresentazioni.
1. Attivare le risorse.
1. Abilitare i flussi di lavoro.

![chlimage_1-223](assets/chlimage_1-223.png)

### Disattiva flussi di lavoro {#disabling-workflows}

Prima di avviare la migrazione, disabilita i moduli di avvio per il flusso di lavoro [!UICONTROL Risorsa di aggiornamento DAM]. È meglio acquisire tutte le risorse nel sistema ed eseguire quindi i flussi di lavoro in batch. Se sei già attivo durante la migrazione, puoi pianificare l’esecuzione di queste attività fuori orario.

### Carica tag {#loading-tags}

È possibile che sia già stata impostata una tassonomia dei tag da applicare alle immagini. Strumenti come Importazione risorse CSV e Supporto di [!DNL Experience Manager] per i profili di metadati possono automatizzare il processo di applicazione dei tag alle risorse, ma i tag devono essere caricati nel sistema. La funzionalità [Strumenti AEM ACS Tag Maker](https://adobe-consulting-services.github.io/acs-aem-tools/features/tag-maker/index.html) consente di popolare i tag utilizzando un foglio di calcolo di Microsoft Excel caricato nel sistema.

### Acquisire risorse {#ingesting-assets}

Prestazioni e stabilità sono fattori importanti da considerare al momento dell’acquisizione delle risorse nel sistema. Poiché si sta caricando una grande quantità di dati nel sistema, è necessario assicurarsi che il sistema funzioni correttamente per ridurre al minimo il tempo necessario ed evitare di sovraccaricare il sistema, con conseguente possibile arresto anomalo del sistema, soprattutto nei sistemi già in produzione.

Esistono due approcci per caricare le risorse nel sistema: un approccio basato su push utilizzando HTTP o un approccio basato su pull utilizzando le API JCR.

#### Invia tramite HTTP {#pushing-through-http}

Il team Managed Services di Adobe utilizza uno strumento denominato Glutton per caricare i dati negli ambienti dei clienti. Glutton è una piccola applicazione Java che carica tutte le risorse da una directory a un&#39;altra in una distribuzione di [!DNL Experience Manager]. Al posto di Glutton, puoi anche utilizzare strumenti come script Perl per pubblicare le risorse nell’archivio.

Esistono due principali svantaggi nell’utilizzo dell’approccio push attraverso https:

1. Le risorse devono essere trasmesse al server tramite HTTP. Questo richiede un po’ di sovraccarico e richiede molto tempo, prolungando così il tempo necessario per eseguire la migrazione.
1. Se disponi di tag e metadati personalizzati che devono essere applicati alle risorse, questo approccio richiede un secondo processo personalizzato da eseguire per applicare i metadati alle risorse una volta importate.

L’altro approccio per acquisire le risorse consiste nell’estrarre le risorse dal file system locale. Tuttavia, se non riesci a ottenere un’unità esterna o una condivisione di rete montata sul server per eseguire un approccio basato su pull, la pubblicazione delle risorse su HTTP è l’opzione migliore.

#### Recupera dal file system locale {#pulling-from-the-local-filesystem}

La funzione di importazione risorse CSV degli strumenti AEM di [ACS](https://adobe-consulting-services.github.io/acs-aem-tools/features/csv-asset-importer/index.html) richiama le risorse dal file system e i metadati delle risorse da un file CSV per l&#39;importazione delle risorse. L’API di Experience Manager Asset Manager viene utilizzata per importare le risorse nel sistema e applicare le proprietà dei metadati configurate. Idealmente, le risorse vengono installate sul server tramite un file di rete o un&#39;unità esterna.

Poiché le risorse non devono essere trasmesse in rete, le prestazioni complessive migliorano notevolmente e questo metodo è generalmente considerato il modo più efficiente per caricare le risorse nell’archivio. Inoltre, poiché lo strumento supporta l’acquisizione dei metadati, puoi importare tutte le risorse e i metadati in un singolo passaggio anziché creare anche un secondo passaggio per applicare i metadati tramite uno strumento separato.

### Elabora rappresentazioni {#processing-renditions}

Dopo aver caricato le risorse nel sistema, devi elaborarle tramite il flusso di lavoro [!UICONTROL Risorsa di aggiornamento DAM] per estrarre i metadati e generare le rappresentazioni. Prima di eseguire questo passaggio, devi duplicare e modificare il flusso di lavoro [!UICONTROL Risorsa di aggiornamento DAM] in base alle tue esigenze. Il flusso di lavoro preconfigurato contiene molti passaggi che potrebbero non essere necessari, ad esempio la generazione PTIFF di Dynamic Medie o l&#39;integrazione di [!DNL InDesign Server].

Dopo aver configurato il flusso di lavoro in base alle tue esigenze, puoi eseguirlo in due modi:

1. L&#39;approccio più semplice è [Gestione flusso di lavoro in blocco di ACS Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/bulk-workflow-manager.html). Questo strumento consente di eseguire una query ed elaborarne i risultati tramite un flusso di lavoro. Sono disponibili opzioni per impostare anche le dimensioni del batch.
1. Puoi utilizzare [ACS Commons Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) insieme a [Synthetic Workflows](https://adobe-consulting-services.github.io/acs-aem-commons/features/synthetic-workflow.html) (Flussi di lavoro sintetici). Questo approccio è molto più complesso, ma consente di rimuovere il sovraccarico del motore del flusso di lavoro [!DNL Experience Manager] ottimizzando l&#39;utilizzo delle risorse del server. Inoltre, Fast Action Manager migliora ulteriormente le prestazioni monitorando dinamicamente le risorse del server e riducendo il carico posizionato sul sistema. Gli script di esempio sono stati forniti nella pagina delle funzioni di ACS Commons.

### Attivare risorse {#activating-assets}

Per le distribuzioni che hanno un livello di pubblicazione, devi attivare le risorse nella farm di pubblicazione. Adobe consiglia di eseguire più di una singola istanza Publish, ma è più efficiente replicare tutte le risorse in una singola istanza Publish e quindi clonarla. Quando attivi un numero elevato di risorse, dopo l’attivazione di una struttura ad albero potrebbe essere necessario intervenire. Ecco perché: quando si attivano le attivazioni, gli elementi vengono aggiunti alla coda dei processi/eventi Sling. Quando la dimensione di questa coda inizia a superare circa 40.000 elementi, l’elaborazione rallenta notevolmente. Quando la dimensione di questa coda supera i 100.000 elementi, la stabilità del sistema inizia a risentirne.

Per risolvere il problema, è possibile utilizzare [Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) per gestire la replica delle risorse. Questo funziona senza utilizzare le code Sling, riducendo il sovraccarico e riducendo al contempo il carico di lavoro per evitare che il server diventi sovraccarico. Un esempio dell’utilizzo di FAM per gestire la replica è riportato nella pagina della documentazione della funzione.

Le altre opzioni per spostare le risorse nella farm di pubblicazione includono l’utilizzo di [vlt-rcp](https://jackrabbit.apache.org/filevault/rcp.html) o [oak-run](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run), forniti come strumenti nell’ambito di Jackrabbit. Un&#39;altra opzione consiste nell&#39;utilizzare uno strumento open-source per l&#39;infrastruttura [!DNL Experience Manager] denominato [Grabbit](https://github.com/TWCable/grabbit), che promette prestazioni più veloci rispetto a vlt.

Per uno qualsiasi di questi approcci, è opportuno notare che le risorse sull’istanza di authoring non vengono visualizzate come attivate. Per gestire il contrassegno di queste risorse con lo stato di attivazione corretto, è necessario eseguire anche uno script per contrassegnare le risorse come attivate.

>[!NOTE]
>
>Adobe non gestisce o supporta Grabbit.

### Clona Publish {#cloning-publish}

Dopo l’attivazione delle risorse, puoi clonare l’istanza di pubblicazione per creare tutte le copie necessarie per la distribuzione. La clonazione di un server è abbastanza semplice, ma ci sono alcuni passaggi importanti da ricordare. Per clonare la pubblicazione:

1. Eseguire il backup dell&#39;istanza di origine e dell&#39;archivio dati.
1. Ripristina il backup dell’istanza e dell’archivio dati nel percorso di destinazione. I passaggi seguenti si riferiscono tutti a questa nuova istanza.
1. Eseguire una ricerca del file system in `crx-quickstart/launchpad/felix` per `sling.id`. Elimina questo file.
1. Nel percorso della directory principale dell&#39;archivio dati individuare ed eliminare i file `repository-XXX`.
1. Modificare `crx-quickstart/install/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` e `crx-quickstart/launchpad/config/org/apache/jackrabbit/oak/plugins/blob/datastore/FileDataStore.config` per indicare la posizione dell&#39;archivio dati nel nuovo ambiente.
1. Avvia l’ambiente.
1. Aggiorna la configurazione di eventuali agenti di replica sugli autori in modo che puntino alle istanze di pubblicazione corrette o agli agenti di svuotamento del dispatcher sulla nuova istanza in modo che puntino ai dispatcher corretti per il nuovo ambiente.

### Abilitare i flussi di lavoro {#enabling-workflows}

Dopo aver completato la migrazione, i moduli di avvio per i flussi di lavoro [!UICONTROL Risorsa di aggiornamento DAM] devono essere riabilitati per supportare la generazione di rendering e l&#39;estrazione di metadati per l&#39;utilizzo quotidiano del sistema.

## Esegui migrazione tra [!DNL Experience Manager] implementazioni {#migrating-between-aem-instances}

Anche se non è così comune, a volte è necessario eseguire la migrazione di grandi quantità di dati da una distribuzione di [!DNL Experience Manager] a un&#39;altra; ad esempio, quando si esegue un aggiornamento di [!DNL Experience Manager], aggiornare l&#39;hardware o eseguire la migrazione a un nuovo centro dati, ad esempio con una migrazione AMS.

In questo caso, le risorse sono già compilate con metadati e le rappresentazioni sono già generate. Puoi semplicemente concentrarti sullo spostamento delle risorse da un’istanza all’altra. Durante la migrazione tra la distribuzione di [!DNL Experience Manager], eseguire i passaggi seguenti:

1. Disabilita flussi di lavoro: poiché stai eseguendo la migrazione delle rappresentazioni insieme alle nostre risorse, vuoi disabilitare i moduli di avvio dei flussi di lavoro per il flusso di lavoro [!UICONTROL Aggiorna risorsa DAM].

1. Migra tag: poiché sono già presenti tag caricati nella distribuzione di origine [!DNL Experience Manager], è possibile generarli in un pacchetto di contenuti e installare il pacchetto nell&#39;istanza di destinazione.

1. Migra risorse: sono disponibili due strumenti consigliati per spostare le risorse da una distribuzione [!DNL Experience Manager] a un&#39;altra:

   * **Copia remota Vault** o vlt rcp, consente di utilizzare vlt in una rete. È possibile specificare una directory di origine e di destinazione e scaricare tutti i dati del repository da un&#39;istanza e caricarli nell&#39;altra. RCP Vlt documentato in [https://jackrabbit.apache.org/filevault/rcp.html](https://jackrabbit.apache.org/filevault/rcp.html)
   * **Grabbit** è uno strumento di sincronizzazione dei contenuti open source sviluppato da Time Warner Cable per l&#39;implementazione di [!DNL Experience Manager]. Poiché utilizza flussi di dati continui, rispetto a vlt rcp, ha una latenza inferiore e richiede un miglioramento della velocità da due a dieci volte più veloce di vlt rcp. Grabbit supporta inoltre la sincronizzazione solo del contenuto delta, che consente di sincronizzare le modifiche dopo il completamento di un passaggio di migrazione iniziale.

1. Attiva risorse: segui le istruzioni per [l&#39;attivazione delle risorse](#activating-assets) documentate per la migrazione iniziale a [!DNL Experience Manager].

1. Pubblicazione duplicata: come per una nuova migrazione, caricare una singola istanza di pubblicazione e clonarla è più efficiente che attivare il contenuto su entrambi i nodi. Vedere [Clonazione di Publish.](#cloning-publish)

1. Abilita flussi di lavoro: dopo aver completato la migrazione, riabilita i moduli di avvio per il flusso di lavoro [!UICONTROL Risorsa di aggiornamento DAM] per supportare la generazione di rendering e l&#39;estrazione di metadati per l&#39;utilizzo quotidiano continuo del sistema.
