---
title: Traduci contenuto
description: Utilizza il connettore di traduzione e le regole per tradurre i contenuti headless.
index: true
hide: false
hidefromtoc: false
source-git-commit: 7cf68868e0963930bde9fcda647822a03914b61d
workflow-type: tm+mt
source-wordcount: '2174'
ht-degree: 0%

---

# Traduci contenuto {#translate-content}

Utilizza il connettore di traduzione e le regole per tradurre i contenuti headless.

## La storia finora {#story-so-far}

Nel documento precedente del percorso di traduzione senza testa AEM, [Configurare le regole di traduzione](translation-rules.md) hai imparato a utilizzare AEM regole di traduzione per identificare il contenuto di traduzione. Ora dovresti:

* Comprendi cosa fanno le regole di traduzione.
* Puoi definire le tue regole di traduzione.

Ora che le regole del connettore e delle traduzioni sono configurate, questo articolo ti guida attraverso il passaggio successivo per tradurre i tuoi contenuti headless.

## Obiettivo {#objective}

Questo documento ti aiuta a capire come utilizzare AEM progetti di traduzione insieme al connettore e le regole di traduzione per tradurre il contenuto. Dopo aver letto questo documento è necessario:

* Scopri cos’è un progetto di traduzione.
* Potrai creare nuovi progetti di traduzione.
* Utilizza i progetti di traduzione per tradurre i tuoi contenuti headless.

## Creazione di un progetto di traduzione {#creating-translation-project}

I progetti di traduzione consentono di gestire la traduzione di contenuti AEM headless. Un progetto di traduzione raccoglie i contenuti da tradurre in altre lingue in un unico luogo per una visione centrale del lavoro di traduzione.

Quando il contenuto viene aggiunto a un progetto di traduzione, per esso viene creato un processo di traduzione. I processi forniscono i comandi e le informazioni sullo stato utilizzati per gestire i flussi di lavoro di traduzione umana e di traduzione automatica che vengono eseguiti sulle risorse.

I progetti di traduzione possono essere creati in due modi:

1. Seleziona la directory principale della lingua del contenuto e fai AEM creare automaticamente il progetto di traduzione in base al percorso del contenuto.
1. Crea un progetto vuoto e seleziona manualmente il contenuto da aggiungere al progetto di traduzione

Entrambi sono approcci validi di solito solo diversi in base alla persona che esegue la traduzione:

* Il modulo TPM (Translation Project Manager) richiede spesso la flessibilità di selezionare manualmente il contenuto nel progetto di traduzione.
* Se il proprietario del contenuto è anche responsabile della traduzione, è spesso più semplice AEM creare automaticamente il progetto in base al percorso del contenuto selezionato.

Entrambi gli approcci sono esaminati nelle sezioni seguenti.

### Creazione automatica di un progetto di traduzione in base al percorso del contenuto {#automatically-creating}

Per i proprietari dei contenuti che sono anche responsabili della traduzione, spesso è più semplice AEM creare automaticamente il progetto di traduzione. Per fare in modo AEM creare automaticamente un progetto di traduzione basato sul percorso del contenuto:

1. Passa a **Navigazione** -> **Risorse** -> **File**. Il contenuto headless in AEM viene memorizzato come risorse note come Frammenti di contenuto.
1. Seleziona la directory principale della lingua del progetto. In questo caso abbiamo selezionato `/content/dam/wknd/en`.
1. Tocca o fai clic sul selettore della barra e mostra il **Riferimenti** pannello.
1. Tocca o fai clic su **Copie per lingua**.
1. Controlla la **Copie per lingua** casella di controllo.
1. Espandi la sezione . **Aggiorna copie per lingua** nella parte inferiore del pannello dei riferimenti.
1. In **Progetto** a discesa, seleziona **Crea progetti di traduzione**.
1. Fornisci un titolo appropriato per il progetto di traduzione.
1. Tocca o fai clic su **Inizio**.

![Crea un progetto di traduzione](assets/create-translation-project.png)

Viene visualizzato un messaggio che informa che il progetto è stato creato.

>[!NOTE]
>
>Si presume che la necessaria struttura linguistica per le lingue di traduzione sia già stata creata come parte del [definizione della struttura del contenuto.](getting-started.md#content-structure) Questo dovrebbe essere fatto in collaborazione con l&#39;architetto dei contenuti.
>
>Se le cartelle della lingua non vengono create in anticipo, non sarà possibile creare copie della lingua come descritto nei passaggi precedenti.

### Creazione manuale di un progetto di traduzione selezionandone il contenuto {#manually-creating}

Per i project manager di traduzione, spesso è necessario selezionare manualmente contenuti specifici da includere in un progetto di traduzione. Per creare un progetto di traduzione manuale di questo tipo, è necessario iniziare creando un progetto vuoto e quindi selezionare il contenuto da aggiungere.

1. Passa a **Navigazione** -> **Progetti**.
1. Tocca o fai clic su **Crea** -> **Cartella** per creare una cartella per i progetti.
   * Questo è facoltativo, ma utile per organizzare le attività di traduzione.
1. In **Crea cartella** aggiungi una finestra **Titolo** per la cartella, quindi tocca o fai clic su **Crea**.

   ![Crea cartella di progetto](assets/create-project-folder.png)

1. Tocca o fai clic sulla cartella per aprire la cartella.
1. Nella nuova cartella del progetto, tocca o fai clic su **Crea** -> **Progetto**.
1. I progetti si basano su modelli. Tocca o fai clic sul pulsante **Progetto di traduzione** modello per selezionarlo, quindi tocca o fai clic su **Successivo**.

   ![Seleziona modello di progetto di traduzione](assets/select-translation-project-template.png)

1. Sulla **Base** , immetti un nome per il nuovo progetto.

   ![Scheda di base del progetto](assets/project-basic-tab.png)

1. Sulla **Avanzate** , utilizza **Lingua di destinazione** menu a discesa per selezionare le lingue in cui tradurre il contenuto. Tocca o fai clic su **Crea**.

   ![Scheda avanzata del progetto](assets/project-advanced-tab.png)

1. Tocca o fai clic su **Apri** nella finestra di dialogo di conferma.

   ![Finestra di dialogo di conferma del progetto](assets/project-confirmation-dialog.png)

Il progetto è stato creato, ma non contiene alcun contenuto da tradurre. Nella sezione successiva viene illustrato come è strutturato il progetto e come aggiungere contenuti.

## Utilizzo di un progetto di traduzione {#using-translation-project}

I progetti di traduzione sono progettati per raccogliere tutti i contenuti e le attività relativi a uno sforzo di traduzione in un unico luogo per rendere la traduzione semplice e facile da gestire.

Per visualizzare il progetto di traduzione:

1. Passa a **Navigazione** -> **Progetti**.
1. Tocca o fai clic sul progetto creato nella sezione precedente.

![Progetto di traduzione](assets/translation-project.png)

Il progetto è diviso in più schede.

* **Riepilogo** - Questa scheda mostra le informazioni di intestazione di base del progetto, inclusi il proprietario, la lingua e il provider di traduzione.
* **Processo di traduzione** - Questa scheda o queste schede mostrano una panoramica del processo di traduzione effettivo, compreso lo stato, il numero di risorse, ecc. In genere esiste un processo per lingua con il codice della lingua ISO-2 aggiunto al nome del processo.
* **Team** - Questa scheda mostra gli utenti che stanno collaborando a questo progetto di traduzione. Questo percorso non tratta questo argomento.
* **Attività** - Attività aggiuntive associate alla traduzione del contenuto, ad esempio per eseguire elementi o elementi del flusso di lavoro. Questo percorso non tratta questo argomento.

La modalità di utilizzo di un progetto di traduzione dipende da come è stato creato: automaticamente tramite AEM o manualmente.

### Utilizzo di un progetto di traduzione creato automaticamente {#using-automatic-project}

Quando crei automaticamente il progetto di traduzione, AEM valuta il contenuto headless nel percorso selezionato in base alle regole di traduzione definite in precedenza. Sulla base di tale valutazione, estrae il contenuto che richiede la traduzione in un nuovo progetto di traduzione.

Per visualizzare i dettagli del contenuto headless incluso in questo progetto:

1. Tocca o fai clic sul pulsante con i puntini di sospensione nella parte inferiore del **Processo di traduzione** il Card.
1. La **Processo di traduzione** in finestra vengono elencati tutti gli elementi del processo.
   ![Dettagli del lavoro di traduzione](assets/translation-job-detail.png)
1. Tocca o fai clic su una riga per visualizzare i dettagli di tale riga, tenendo presente che una riga può rappresentare più elementi di contenuto da tradurre.
1. Tocca o fai clic sulla casella di controllo della selezione di un elemento per visualizzare ulteriori opzioni, ad esempio l’opzione per eliminarlo dal processo o visualizzarlo nelle console Frammenti di contenuto o Risorse .
   ![Opzioni del lavoro di traduzione](assets/translation-job-options.png)

In genere il contenuto del processo di traduzione inizia nel **Bozza** come indicato dal **Stato** nella colonna **Processo di traduzione** finestra.

Per avviare il processo di traduzione, torna alla panoramica del progetto di traduzione e tocca o fai clic sul pulsante con freccia nella parte superiore della **Processo di traduzione** scheda e seleziona **Inizio**.

![Avvia processo di traduzione](assets/start-translation-job.png)

AEM ora comunica con la configurazione di traduzione e il connettore per inviare il contenuto al servizio di traduzione. Per visualizzare l’avanzamento della traduzione, torna alla sezione **Processo di traduzione** visualizzazione della finestra **Stato** colonna delle voci.

![Processo di traduzione approvato](assets/translation-job-approved.png)

Le traduzioni automatiche ritornano automaticamente con uno stato di **Approvato**. La traduzione umana consente una maggiore interazione, ma va oltre lo scopo di questo percorso.

### Utilizzo di un progetto di traduzione creato manualmente {#using-manual-project}

Quando crei manualmente un progetto di traduzione, AEM crea i processi necessari, ma non seleziona automaticamente alcun contenuto da includere. Questo consente al project manager di traduzione di scegliere e scegliere il contenuto da tradurre.

Per aggiungere contenuto a un processo di traduzione:

1. Tocca o fai clic sul pulsante con i puntini di sospensione nella parte inferiore di uno dei **Processo di traduzione** carte.
1. Vedi che il processo non contiene contenuto. Tocca o fai clic sul pulsante **Aggiungi** nella parte superiore della finestra e quindi **Risorse/pagine** dal menu a discesa.

   ![Processo di traduzione vuoto](assets/empty-translation-job.png)

1. Viene visualizzato un browser percorsi che consente di selezionare in modo specifico quale contenuto aggiungere. Individua il contenuto e tocca o fai clic per selezionare.

   ![Browser del percorso](assets/path-browser.png)

1. Tocca o fai clic su **Seleziona** per aggiungere il contenuto selezionato al processo.
1. In **Traduci** finestra di dialogo, specificare **Crea copia in lingua**.

   ![Crea copia per lingua](assets/translate-copy-master.png)

1. Il contenuto è ora incluso nel processo.

   ![Contenuto aggiunto al processo di traduzione](assets/content-added.png)

1. Tocca o fai clic sulla casella di controllo della selezione di un elemento per visualizzare ulteriori opzioni, ad esempio l’opzione per eliminarlo dal processo o visualizzarlo nelle console Frammenti di contenuto o Risorse .
   ![Opzioni del lavoro di traduzione](assets/translation-job-options-manual.png)

1. Ripeti questi passaggi per includere nel processo tutto il contenuto necessario.

>[!TIP]
>
>Il browser Percorsi è un potente strumento che consente di cercare, filtrare e navigare nel contenuto. Tocca o fai clic sul pulsante **Solo contenuto/Filtri** per attivare/disattivare il pannello laterale e visualizzare filtri avanzati, ad esempio **Data di modifica** o **Stato della traduzione**.
>
>Per ulteriori informazioni sul browser percorsi in [sezione risorse aggiuntive.](#additional-resources)

Puoi utilizzare i passaggi precedenti per aggiungere il contenuto necessario a tutte le lingue (processi) per il progetto. Dopo aver selezionato tutti i contenuti, puoi avviare la traduzione.

In genere il contenuto del processo di traduzione inizia nel **Bozza** come indicato dal **Stato** nella colonna **Processo di traduzione** finestra.

Per avviare il processo di traduzione, torna alla panoramica del progetto di traduzione e tocca o fai clic sul pulsante con freccia nella parte superiore della **Processo di traduzione** scheda e seleziona **Inizio**.

![Avvia processo di traduzione](assets/start-translation-job-manual.png)

AEM ora comunica con la configurazione di traduzione e il connettore per inviare il contenuto al servizio di traduzione. Per visualizzare l’avanzamento della traduzione, torna alla sezione **Processo di traduzione** visualizzazione della finestra **Stato** colonna delle voci.

![Processo di traduzione approvato](assets/translation-job-approved-manual.png)

Le traduzioni automatiche ritornano automaticamente con uno stato di **Approvato**. La traduzione umana consente una maggiore interazione, ma va oltre lo scopo di questo percorso.

## Revisione dei contenuti tradotti {#reviewing}

[Come visto in precedenza,](#using-translation-project) il contenuto tradotto automaticamente torna in AEM con lo stato **Approvato** poiché si presume che, poiché si utilizza la traduzione automatica, non è necessario alcun intervento umano. Tuttavia è ancora possibile rivedere il contenuto tradotto.

Basta andare al processo di traduzione completato e selezionare una riga toccando o facendo clic sulla casella di controllo. Icona **Mostra nel frammento di contenuto** nella barra degli strumenti.

![Mostra nel frammento di contenuto](assets/reveal-in-content-fragment.png)

Tocca o fai clic su tale icona per aprire il frammento di contenuto tradotto nella console dell’editor per visualizzare i dettagli del contenuto tradotto.

![Un frammento di contenuto tradotto](assets/translated-content-fragment.png)

Se necessario, puoi modificare ulteriormente il frammento di contenuto, disponendo delle autorizzazioni necessarie, ma la modifica dei frammenti di contenuto va oltre l’ambito di questo percorso. Vedi la [Risorse aggiuntive](#additional-resources) sezione alla fine di questo documento per ulteriori informazioni su questo argomento.

Lo scopo del progetto è quello di raccogliere tutte le risorse relative a una traduzione in un unico luogo per un facile accesso e una chiara panoramica. Tuttavia, come puoi vedere visualizzando i dettagli di un elemento tradotto, le traduzioni stesse scorrono nuovamente nella cartella delle risorse del linguaggio di traduzione. In questo esempio la cartella è

```text
/content/dam/wknd/es
```

Se passi a questa cartella tramite **Navigazione** -> **Risorse** -> **File**, vengono visualizzati i contenuti tradotti.

![Struttura delle cartelle di contenuto tradotto](assets/translated-file-content.png)

AEM framework di traduzione riceve le traduzioni dal connettore di traduzione e quindi crea automaticamente la struttura del contenuto in base alla directory principale della lingua e utilizzando le traduzioni fornite dal connettore.

È importante comprendere che questo contenuto non viene pubblicato e quindi non è disponibile per i servizi headless. Impareremo a conoscere questa struttura autore-pubblicazione e vedremo come pubblicare i nostri contenuti tradotti nel prossimo passaggio del percorso di traduzione.

## Traduzione manuale {#human-translation}

Se il servizio di traduzione fornisce la traduzione umana, il processo di revisione offre più opzioni. Ad esempio, le traduzioni arrivano nuovamente nel progetto con lo stato **Bozza** e deve essere rivisto e approvato o rifiutato manualmente.

La traduzione umana va oltre l&#39;ambito di questo percorso di localizzazione. Vedi la [Risorse aggiuntive](#additional-resources) sezione alla fine di questo documento per ulteriori informazioni su questo argomento. Tuttavia, oltre alle opzioni di approvazione aggiuntive, il flusso di lavoro per le traduzioni umane è lo stesso delle traduzioni automatiche descritto in questo percorso.

## Novità {#what-is-next}

Ora che hai completato questa parte del percorso di traduzione headless dovresti:

* Scopri cos’è un progetto di traduzione.
* Potrai creare nuovi progetti di traduzione.
* Utilizza i progetti di traduzione per tradurre i tuoi contenuti headless.

Sviluppa questa conoscenza e continua il tuo percorso di traduzione senza testa AEM prossimo revisione del documento [Pubblicare contenuti tradotti](publish-content.md) dove imparerai a pubblicare i contenuti tradotti e come aggiornare tali traduzioni man mano che il contenuto principale della lingua cambia.

## Risorse aggiuntive {#additional-resources}

Mentre si consiglia di passare alla parte successiva del percorso di traduzione headless rivedendo il documento [Pubblicare contenuti tradotti,](publish-content.md) di seguito sono riportate alcune risorse aggiuntive facoltative che approfondiscono alcuni concetti menzionati in questo documento, ma non è necessario che continuino sul percorso headless.

* [Gestione dei progetti di traduzione](/help/sites-administering/tc-manage.md) - Scopri i dettagli dei progetti di traduzione e le funzioni aggiuntive, come i flussi di lavoro di traduzione umana e i progetti multilingue.
* [Ambiente e strumenti di authoring](/help/sites-authoring/author-environment-tools.md##path-selection) - AEM offre diversi meccanismi per organizzare e modificare i contenuti, tra cui un browser con percorso affidabile.
