---
title: Tradurre il contenuto
description: Utilizza il connettore di traduzione e le regole per tradurre il contenuto headless.
exl-id: a2c2bb9f-97b9-42fd-9bd1-e75c113fb514
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '2115'
ht-degree: 66%

---

# Tradurre il contenuto {#translate-content}

Utilizza l’integrazione e le regole di traduzione per tradurre i contenuti headless.

## Percorso affrontato finora {#story-so-far}

Nel documento precedente del percorso di traduzione headless dell&#39;AEM, [Configurare le regole di traduzione](translation-rules.md) hai imparato a utilizzare le regole di traduzione AEM per identificare il contenuto da tradurre. Ora dovresti:

* Comprendere come funzionano le regole di traduzione.
* Essere in grado di definire le tue regole di traduzione.

Ora che le regole del connettore e delle traduzioni sono configurate, questo articolo illustra il passaggio successivo per la traduzione dei contenuti headless.

## Obiettivo {#objective}

Questo documento ti aiuta a capire come utilizzare i progetti di traduzione AEM insieme al connettore e le regole di traduzione per tradurre il contenuto. Dopo aver letto questo documento, dovresti effettuare le seguenti operazioni:

* Sapere cos’è un progetto di traduzione.
* Crea progetti di traduzione.
* Utilizzare i progetti di traduzione per tradurre i contenuti headless.

## Creazione di un progetto di traduzione {#creating-translation-project}

I progetti di traduzione consentono di gestire la traduzione dei contenuti AEM headless. Un progetto di traduzione raccoglie i contenuti da tradurre in altre lingue in un unico luogo per una visione globale dell’attività di traduzione.

Quando il contenuto è aggiunto a un progetto di traduzione, viene creato un lavoro di traduzione. I processi forniscono i comandi e le informazioni sullo stato, utili per gestire i flussi di lavoro di traduzione umana e automatica che vengono eseguiti sulle risorse.

I progetti di traduzione possono essere creati in due modi:

1. Seleziona la lingua root del contenuto e fai creare automaticamente ad AEM il progetto di traduzione in base al percorso del contenuto.
1. Crea un progetto vuoto e seleziona manualmente il contenuto da aggiungere al progetto di traduzione

Entrambi gli approcci sono validi e si differenziano solo in base alla persona che esegue la traduzione:

* Il TPM (Translation Project Manager) richiede spesso la flessibilità di selezionare manualmente il contenuto nel progetto di traduzione.
* Se il proprietario del contenuto è anche responsabile della traduzione, è spesso più semplice lasciare che AEM crei automaticamente il progetto in base al percorso del contenuto selezionato.

Entrambi gli approcci sono esaminati nelle sezioni seguenti.

### Creazione automatica di un progetto di traduzione in base al percorso del contenuto {#automatically-creating}

Per i proprietari di contenuti che sono anche responsabili della traduzione, spesso è più facile che AEM crei automaticamente il progetto. Per fare in modo che AEM crei automaticamente un progetto di traduzione basato sul percorso del contenuto:

1. Accedi a **Navigazione** > **Risorse** > **File**. Tieni presente che il contenuto headless in AEM viene memorizzato come risorse note come Frammenti di contenuto.
1. Seleziona la directory principale della lingua del progetto. In questo caso, `/content/dam/wknd/en` è selezionato.
1. Fai clic sul selettore della barra e mostra **Riferimenti** pannello.
1. Clic **Copie per lingua**.
1. Seleziona la casella di spunta delle **Copie in lingua**.
1. Espandi la sezione **Aggiorna copie in lingua** nella parte inferiore del pannello dei riferimenti.
1. Nel menu a discesa **Progetto**, seleziona **Crea progetto di traduzione**.
1. Fornisci un titolo appropriato per il progetto di traduzione.
1. Clic **Inizio**.

![Crea un progetto di traduzione](assets/create-translation-project.png)

Viene visualizzato un messaggio che informa che il progetto è stato creato.

>[!NOTE]
>
>Si presume che la struttura linguistica necessaria per le lingue di traduzione sia già stata creata come parte della [definizione della struttura del contenuto.](getting-started.md#content-structure) Questo dovrebbe essere fatto in collaborazione con l&#39;architetto dei contenuti.
>
>Se le cartelle della lingua non vengono create in anticipo, non sarà possibile creare copie in lingua come descritto nei passaggi precedenti.

### Creazione manuale di un progetto di traduzione selezionandone il contenuto {#manually-creating}

Per i translation project manager, spesso è necessario selezionare manualmente contenuti specifici da includere in un progetto di traduzione. Per creare un progetto di traduzione manuale di questo tipo, devi iniziare creando un progetto vuoto e quindi selezionare il contenuto da aggiungere.

1. Accedi a **Navigazione** > **Progetti**.
1. Clic **Crea** > **Cartella** per creare una cartella per i progetti.
   * Questo è facoltativo, ma utile per organizzare le attività di traduzione.
1. In **Crea cartella** finestra, aggiungi un **Titolo** per la cartella, quindi fare clic su **Crea**.

   ![Crea cartella di progetto](assets/create-project-folder.png)

1. Fai clic sulla cartella per aprirla.
1. Nella nuova cartella del progetto, fai clic su **Crea** > **Progetto**.
1. I progetti si basano su modelli. Fai clic su **Progetto di traduzione** per selezionarlo e quindi fare clic su **Successivo**.

   ![Seleziona modello di progetto di traduzione](assets/select-translation-project-template.png)

1. Sulla scheda **Informazioni base**, immetti un nome per il nuovo progetto.

   ![Scheda informazioni base del progetto](assets/project-basic-tab.png)

1. Il giorno **Avanzate** , utilizza la scheda **Lingua di destinazione** per selezionare le lingue in cui tradurre il contenuto. Fai clic su **Crea**.

   ![Scheda avanzate del progetto](assets/project-advanced-tab.png)

1. Clic **Apri** nella finestra di dialogo di conferma.

   ![Finestra di conferma del progetto](assets/project-confirmation-dialog.png)

Il progetto è stato creato, ma non contiene alcun contenuto da tradurre. Nella sezione successiva viene illustrato come è strutturato il progetto e come aggiungere contenuti.

## Utilizzo di un progetto di traduzione {#using-translation-project}

I progetti di traduzione sono progettati per raccogliere tutti i contenuti e le attività relativi a un lavoro di traduzione in un unico luogo per rendere la traduzione semplice e facile da gestire.

Per visualizzare il progetto di traduzione:

1. Accedi a **Navigazione** > **Progetti**.
1. Fai clic sul progetto creato nella sezione precedente.

![Progetto di traduzione](assets/translation-project.png)

Il progetto è diviso in più schede.

* **Riepilogo**: questa scheda mostra le informazioni di intestazione di base del progetto, inclusi il proprietario, la lingua e il provider di traduzione.
* **Lavoro di traduzione** - Questa scheda o queste schede mostrano una panoramica del lavoro di traduzione effettivo, compreso lo stato, il numero di risorse e così via. In genere esiste un lavoro per lingua con il codice della lingua ISO-2 aggiunto al nome del processo.
* **Team**: questa scheda mostra gli utenti che stanno collaborando a questo progetto di traduzione. Questo percorso non tratta questo argomento.
* **Attività**: attività aggiuntive associate alla traduzione del contenuto, ad esempio per eseguire elementi o elementi del flusso di lavoro. Questo percorso non tratta questo argomento.

La modalità di utilizzo di un progetto di traduzione dipende da come è stato creato: automaticamente tramite AEM o manualmente.

### Utilizzo di un progetto di traduzione creato automaticamente {#using-automatic-project}

Quando crei automaticamente il progetto di traduzione, AEM valuta il contenuto headless nel percorso selezionato in base alle regole di traduzione definite in precedenza. Sulla base di tale valutazione, estrae il contenuto che richiede la traduzione in un nuovo progetto di traduzione.

Per visualizzare i dettagli del contenuto headless incluso in questo progetto:

1. Fai clic sul pulsante con i puntini di sospensione nella parte inferiore della sezione **Lavoro di traduzione** Card.
1. Nella finestra **Lavoro di traduzione** vengono elencati tutti gli elementi del lavoro.
   ![Dettagli del lavoro di traduzione](assets/translation-job-detail.png)
1. Fai clic su una riga per visualizzarne i dettagli, tenendo presente che può rappresentare più elementi di contenuto da tradurre.
1. Fai clic sulla casella di controllo di selezione di un elemento per visualizzare ulteriori opzioni, ad esempio l’opzione per eliminarlo dal processo o visualizzarlo nelle console Frammenti di contenuto o Risorse.
   ![Opzioni del lavoro di traduzione](assets/translation-job-options.png)

In genere il contenuto del lavoro di traduzione inizia nello stato **Bozza** come indicato dalla colonna **Stato** nella finestra **Lavoro di traduzione**.

Per avviare il lavoro di traduzione, torna alla panoramica del progetto di traduzione e fai clic sul pulsante con la freccia nella parte superiore della **Lavoro di traduzione** e seleziona **Inizio**.

![Avviare il lavoro di traduzione](assets/start-translation-job.png)

AEM ora comunica con la configurazione di traduzione e il connettore per inviare il contenuto al servizio di traduzione. Per visualizzare l’avanzamento della traduzione, torna alla finestra **Lavoro di traduzione** e controlla la colonna **Stato** delle voci.

![Lavoro di traduzione approvato](assets/translation-job-approved.png)

Le traduzioni automatiche risultano automaticamente con lo stato **Approvato**. La traduzione umana consente una maggiore interazione, ma va oltre lo scopo di questo percorso.

### Utilizzo di un progetto di traduzione creato manualmente {#using-manual-project}

Quando crei manualmente un progetto di traduzione, AEM crea i processi necessari, ma non seleziona automaticamente alcun contenuto da includervi. Questo consente al project manager di traduzione di scegliere il contenuto da tradurre.

Per aggiungere contenuto a un lavoro di traduzione:

1. Fai clic sul pulsante con i puntini di sospensione nella parte inferiore di uno dei **Lavoro di traduzione** schede.
1. Vedi che il lavoro non presenta contenuto. Fai clic su **Aggiungi** nella parte superiore della finestra e quindi **Risorse/Pagine** dal menu a discesa.

   ![Lavoro di traduzione vuoto](assets/empty-translation-job.png)

1. Viene visualizzato un browser del percorso che consente di selezionare in modo specifico quale contenuto aggiungere. Individua il contenuto e fai clic per selezionarlo.

   ![Browser del percorso](assets/path-browser.png)

1. Clic **Seleziona** per aggiungere il contenuto selezionato al processo.
1. Nella finestra di dialogo **Traduci**, specifica **Crea copia in lingua**.

   ![Crea copia per lingua](assets/translate-copy-master.png)

1. Il contenuto è ora incluso nel lavoro.

   ![Contenuto aggiunto al lavoro di traduzione](assets/content-added.png)

1. Fai clic sulla casella di controllo di selezione di un elemento per visualizzare ulteriori opzioni, ad esempio l’opzione per eliminarlo dal processo o visualizzarlo nelle console Frammenti di contenuto o Risorse.
   ![Opzioni del lavoro di traduzione](assets/translation-job-options-manual.png)

1. Ripeti questi passaggi per includere nel lavoro tutto il contenuto necessario.

>[!TIP]
>
>Il browser del percorso è un potente strumento che consente di cercare, filtrare e navigare nel contenuto. Fai clic su **Solo contenuto/Filtri** per attivare/disattivare il pannello laterale e visualizzare filtri avanzati, ad esempio **Data di modifica** o **Stato traduzione**.
>
>Scopri di più sul browser del percorso nella [sezione Risorse aggiuntive.](#additional-resources)

Puoi utilizzare i passaggi precedenti per aggiungere il contenuto necessario in tutte le lingue (processi) per il progetto. Dopo aver selezionato tutto il contenuto, puoi avviare la traduzione.

In genere il contenuto del lavoro di traduzione inizia nello stato **Bozza** come indicato dalla colonna **Stato** nella finestra **Lavoro di traduzione**.

Per avviare il lavoro di traduzione, torna alla panoramica del progetto di traduzione e fai clic sul pulsante con la freccia nella parte superiore della **Lavoro di traduzione** e seleziona **Inizio**.

![Avviare il lavoro di traduzione](assets/start-translation-job-manual.png)

AEM ora comunica con la configurazione di traduzione e il connettore per inviare il contenuto al servizio di traduzione. Per visualizzare l’avanzamento della traduzione, torna alla finestra **Lavoro di traduzione** e controlla la colonna **Stato** delle voci.

![Lavoro di traduzione approvato](assets/translation-job-approved-manual.png)

Le traduzioni automatiche risultano automaticamente con lo stato **Approvato**. La traduzione umana consente una maggiore interazione, ma va oltre lo scopo di questo percorso.

## Revisione dei contenuti tradotti {#reviewing}

[Come visto in precedenza,](#using-translation-project) i contenuti tradotti automaticamente tornano nell’AEM con lo stato **Approvato** poiché si presume che, poiché si utilizza la traduzione automatica, non sia necessario alcun intervento umano. Tuttavia, è ancora possibile rivedere il contenuto tradotto.

Basta andare al lavoro di traduzione completato e selezionare una riga toccando o facendo clic sulla casella di spunta. L’icona **Mostra in Frammenti di contenuto** si trova nella barra degli strumenti.

![Mostra in Frammenti di contenuto](assets/reveal-in-content-fragment.png)

Fai clic su tale icona per aprire il frammento di contenuto tradotto nella console dell’editor per visualizzare i dettagli del contenuto tradotto.

![Un frammento di contenuto tradotto](assets/translated-content-fragment.png)

Puoi modificare ulteriormente il frammento di contenuto se necessario, purché tu disponga delle autorizzazioni richieste, ma la modifica dei frammenti di contenuto non rientra negli obiettivi di questo percorso. Consulta la sezione [Risorse aggiuntive](#additional-resources) alla fine di questo documento per ulteriori informazioni su questo argomento.

Lo scopo del progetto è quello di raccogliere tutte le risorse relative a una traduzione in un unico luogo per un accesso facile e una panoramica chiara. Tuttavia, come puoi comprendere visualizzando i dettagli di un elemento tradotto, le traduzioni stesse vengono reintegrate nella cartella delle risorse della lingua di traduzione. In questo esempio, la cartella è:

```text
/content/dam/wknd/es
```

Se passi a questa cartella tramite **Navigazione** > **Risorse** > **File**, vengono visualizzati i contenuti tradotti.

![Struttura delle cartelle di contenuto tradotto](assets/translated-file-content.png)

Il Translation Framework AEM riceve le traduzioni dal connettore e quindi crea automaticamente la struttura del contenuto in base alla lingua root, utilizzando le traduzioni fornite.

È importante comprendere che questo contenuto non è pubblicato e, quindi, non è disponibile per i servizi headless. Scopri questa struttura autore-pubblicazione e scopri come pubblicare i contenuti tradotti nel passaggio successivo del percorso di traduzione.

## Traduzione manuale {#human-translation}

Se il servizio di traduzione fornisce una traduzione umana, il processo di revisione presenta più opzioni. Ad esempio, le traduzioni arrivano nuovamente nel progetto con lo stato **Bozza** e devono essere riviste e approvate o rifiutate manualmente.

La traduzione umana va oltre lo scopo di questo percorso di localizzazione. Consulta la sezione [Risorse aggiuntive](#additional-resources) alla fine di questo documento per ulteriori informazioni su questo argomento. Tuttavia, oltre alle opzioni di approvazione aggiuntive, il flusso di lavoro per le traduzioni umane è lo stesso delle traduzioni automatiche descritto in questo percorso.

## Novità {#what-is-next}

Ora che hai completato questa parte del percorso di traduzione headless, dovresti essere in grado di effettuare le seguenti operazioni:

* Sapere cos’è un progetto di traduzione.
* Crea progetti di traduzione.
* Utilizzare i progetti di traduzione per tradurre i contenuti headless.

Approfondisci l&#39;argomento e continua il tuo percorso di traduzione headless AEM esaminando il documento [Pubblicare contenuti tradotti](publish-content.md) dove scopri come pubblicare i contenuti tradotti e come aggiornare tali traduzioni man mano che il contenuto della lingua root cambia.

## Risorse aggiuntive {#additional-resources}

Sebbene sia raccomandato passare alla parte successiva del percorso di traduzione headless esaminando il documento [Pubblicare il contenuto tradotto,](publish-content.md) di seguito sono riportate alcune risorse aggiuntive facoltative che approfondiscono alcuni concetti menzionati in questo documento, ma non sono necessarie per continuare il percorso headless.

* [Gestione dei progetti di traduzione](/help/sites-administering/tc-manage.md): scopri i dettagli dei progetti di traduzione e le funzioni aggiuntive, come i flussi di lavoro di traduzione umana e i progetti multilingue.
* [Strumenti e ambiente di authoring](/help/sites-authoring/author-environment-tools.md#path-selection): AEM offre diversi meccanismi per organizzare e modificare i contenuti, tra cui un browser del percorso affidabile.
