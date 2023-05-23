---
title: Pubblicare contenuti tradotti
description: Scopri come pubblicare i contenuti tradotti e aggiornare le traduzioni come aggiornamenti dei contenuti.
exl-id: 32c387fe-fa1b-499b-861f-b4822f5e139e
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1378'
ht-degree: 97%

---

# Pubblicare contenuti tradotti {#publish-content}

Scopri come pubblicare i contenuti tradotti e aggiornare le traduzioni come aggiornamenti dei contenuti.

## La storia finora {#story-so-far}

Nel documento precedente del percorso di traduzione di AEM headless, [Traduci contenuto,](configure-connector.md) hai imparato a utilizzare i progetti di traduzione in AEM per tradurre i contenuti headless. Ora dovresti:

* Sapere cos’è un progetto di traduzione.
* Essere in grado di creare nuovi progetti di traduzione.
* Utilizzare i progetti di traduzione per tradurre i contenuti headless.

Una volta completata la traduzione iniziale, questo articolo illustra il passaggio successivo per la pubblicazione di tale contenuto e le operazioni da eseguire per aggiornare le traduzioni quando il contenuto sottostante nella directory principale della lingua cambia.

## Obiettivo {#objective}

Questo documento è utile per comprendere come pubblicare contenuti headless in AEM e come creare un flusso di lavoro continuo per mantenere le traduzioni aggiornate. Dopo aver letto questo documento, dovresti:

* Comprendere il modello di pubblicazione dell’autore di AEM.
* Sapere come pubblicare i contenuti tradotti.
* Essere in grado di implementare un modello di aggiornamento continuo per i contenuti tradotti.

## Modello di pubblicazione dell’autore di AEM {#author-publish}

Prima di pubblicare i contenuti, è utile comprendere il modello di pubblicazione dell’autore di AEM. In parole povere, AEM divide gli utenti del sistema in due gruppi.

1. Coloro che creano e gestiscono il contenuto e il sistema
1. Coloro che utilizzano il contenuto del sistema

AEM è quindi fisicamente separato in due istanze.

1. L’istanza dell’**autore** è il sistema in cui autori e amministratori di contenuti lavorano per creare e gestire i contenuti.
1. L’istanza di **pubblicazione** è il sistema che consegna il contenuto ai consumatori.

Per essere disponibile per il consumo, dopo essere stato creato sull’istanza dell’autore, il contenuto deve essere trasferito nell’istanza di pubblicazione. Il processo di trasferimento dall’autore alla pubblicazione viene chiamato **pubblicazione**.

## Pubblicazione del contenuto tradotto {#publishing}

Quando si è soddisfatti dello stato dei contenuti tradotti, si devono pubblicare in modo che i servizi headless possano utilizzarli. Questa attività di solito non è responsabilità dello specialista della traduzione, ma è documentata qui per illustrare il flusso di lavoro completo.

>[!NOTE]
>
>Generalmente, quando la traduzione è completa, lo specialista delle traduzioni informa i proprietari dei contenuti che le traduzioni sono pronte per la pubblicazione. Quindi i proprietari dei contenuti li pubblicano.
>
>Le seguenti fasi sono fornite per completezza.

Il modo più semplice per pubblicare le traduzioni è passare alla cartella risorse del progetto.

```text
/content/dam/<your-project>/
```

In questo percorso sono presenti sottocartelle per ogni lingua di traduzione e puoi scegliere quale pubblicare.

1. Vai su **Navigazione** -> **Risorse** -> **File** e apri la cartella del progetto.
1. Qui puoi vedere la cartella principale della lingua e tutte le altre cartelle della lingua. Seleziona la lingua o le lingue localizzate da pubblicare.
   ![Seleziona cartella della lingua](assets/select-language-folder.png)
1. Tocca o fai clic su **Gestisci pubblicazione**.
1. Nella finestra **Gestisci pubblicazione**, assicurati che **Pubblica** sia selezionato automaticamente in **Azione** e che **Adesso** sia selezionato in **Pianificazione**. Tocca o fai clic su **Avanti**.
   ![Opzioni di Gestisci pubblicazione](assets/manage-publication-options.png)
1. Nella prossima finestra **Gestisci pubblicazione**, conferma che i percorsi corretti siano selezionati. Tocca o fai clic su **Pubblica**.
   ![Ambito di Gestisci pubblicazione](assets/manage-publication-scope.png)
1. L’AEM conferma l’azione di pubblicazione con un messaggio a comparsa nella parte superiore dello schermo.
   ![Banner risorse pubblicate](assets/resources-published-message.png)

Il contenuto headless tradotto è ora pubblicato. È ora possibile accedervi e utilizzarli dai servizi headless.

>[!TIP]
>
>Per pubblicare più traduzioni contemporaneamente, è possibile selezionare più elementi (ad esempio cartelle multilingue) durante la pubblicazione.

Quando si pubblicano i contenuti, sono disponibili opzioni aggiuntive, ad esempio per pianificare un’ora di pubblicazione, che vanno oltre l’ambito di questo percorso. Per ulteriori informazioni, consulta la sezione [Risorse aggiuntive](#additional-resources) alla fine del documento.

## Aggiornamento del contenuto tradotto {#updating-translations}

La traduzione è raramente un esercizio occasionale. In genere, al termine della traduzione iniziale, gli autori dei contenuti continuano ad aggiungere e modificare il contenuto nella directory principale della lingua. Questo significa che devi aggiornare anche il contenuto tradotto.

I requisiti specifici del progetto definiscono la frequenza con cui devi aggiornare le traduzioni e quale processo decisionale viene seguito prima di eseguire un aggiornamento. Una volta che hai deciso di aggiornare le traduzioni, il processo in AEM è molto semplice. Poiché la traduzione iniziale era basata su un progetto di traduzione, lo sono anche gli aggiornamenti.

Tuttavia, come in precedenza, il processo varia leggermente se si sceglie di creare il progetto di traduzione automaticamente o manualmente.

### Aggiornamento di un progetto di traduzione creato automaticamente {#updating-automatic-project}

1. Passa a **Navigazione** -> **Risorse** -> **File**. Tieni presente che il contenuto headless in AEM viene memorizzato come risorse note come Frammenti di contenuto.
1. Seleziona la directory principale della lingua del progetto. In questo caso abbiamo selezionato `/content/dam/wknd/en`.
1. Tocca o fai clic sul selettore della barra e mostra il pannello **Riferimenti**.
1. Tocca o fai clic su **Copie in lingua**.
1. Seleziona la casella di spunta delle **Copie in lingua**.
1. Espandi la sezione **Aggiorna copie per lingua** nella parte inferiore del pannello dei riferimenti.
1. Nel menu a discesa **Progetto**, seleziona **Aggiungi a un progetto di traduzione esistente**.
1. Nel menu a discesa **Progetto di traduzione esistente**, seleziona il progetto creato per la traduzione iniziale.
1. Tocca o fai clic su **Inizia**.

![Aggiungi elementi al progetto di traduzione esistente](assets/add-to-existing-project.png)

Il contenuto viene aggiunto al progetto di traduzione esistente. Per visualizzare il progetto di traduzione:

1. Passa a **Navigazione** -> **Progetti**.
1. Tocca o fai clic sul progetto appena aggiornato.
1. Tocca o fai clic sulla lingua o su una delle lingue aggiornate.

Al progetto vengono aggiunte le nuove schede dei processi, in base alle necessità.

<!--
You see that a new job card was added to the project. In this example, another Spanish translation was added.

![Additional translation job added](assets/additional-translation-job.png)
-->

Noterai che le statistiche elencate nella nuova scheda (numero di risorse e frammenti di contenuto) sono diverse. Questo perché AEM riconosce ciò che è cambiato dopo l’ultima traduzione e include solo il contenuto che deve essere tradotto. Ciò include la ritraduzione dei contenuti aggiornati e la prima traduzione dei nuovi contenuti.

Da questo punto, [inizia e gestisci il tuo processo di traduzione proprio come hai fatto con l’originale.](translate-content.md#using-translation-project)

### Aggiornamento di un progetto di traduzione creato manualmente {#updating-manual-project}

Per aggiornare una traduzione è possibile aggiungere al progetto esistente un nuovo processo responsabile della traduzione del contenuto aggiornato.

1. Passa a **Navigazione** -> **Progetti**.
1. Tocca o fai clic sul progetto da aggiornare.
1. Tocca o fai clic sul pulsante **Aggiungi** nella parte superiore della finestra.
1. Nella finestra **Aggiungi riquadro**, tocca o fai clic su **Processo di traduzione** e poi **Invia**.

   ![Aggiungi riquadro](assets/add-translation-job-tile.png)

1. Sulla scheda del nuovo processo di traduzione, tocca o fai clic sul pulsante con freccia in alto nella scheda e seleziona **Aggiorna destinazione** per definire la lingua di destinazione del nuovo processo.

   ![Aggiorna destinazione](assets/update-target.png)

1. Nella finestra di dialogo **Seleziona la lingua di destinazione** utilizza l’elenco a discesa per selezionare la lingua e tocca o fai clic su **Fine**.

   ![Seleziona lingua di destinazione](assets/select-target-language.png)

1. Una volta impostata la lingua di destinazione del nuovo processo di traduzione, tocca o fai clic sul pulsante con i puntini di sospensione nella parte inferiore della scheda del processo per visualizzarne i dettagli.
1. Il processo è vuoto al momento della creazione. Aggiungi contenuto al processo toccando o facendo clic sul pulsante **Aggiungi** e utilizzando il browser del percorso [come in precedenza durante la creazione del progetto di traduzione.](translate-content.md##manually-creating)

>[!TIP]
>
>I potenti filtri del browser del percorso possono essere utili di nuovo per trovare solo il contenuto aggiornato.
>
>Per ulteriori informazioni sul browser percorsi, consulta la [sezione risorse aggiuntive.](#additional-resources)

Da questo punto, [inizia e gestisci il tuo processo di traduzione proprio come hai fatto con l’originale.](translate-content.md#using-translation-project)

## Fine del percorso? {#end-of-journey}

Congratulazioni. Hai completato il percorso di traduzione headless. Ora dovresti:

* Avrai una panoramica della distribuzione headless dei contenuti.
* avere una comprensione di base delle funzionalità headless di AEM.
* Comprenderai le funzioni di traduzione di AEM e in che modo si relazionano con il contenuto headless.
* Avrai la possibilità di iniziare a tradurre i tuoi contenuti headless.

essere in grado di tradurre i tuoi contenuti headless in AEM. Tuttavia AEM è uno strumento potente e ci sono molte opzioni aggiuntive disponibili. Consulta alcune delle risorse aggiuntive disponibili nella [sezione Risorse aggiuntive](#additional-resources) per ulteriori informazioni sulle funzioni visualizzate in questo percorso.

## Risorse aggiuntive {#additional-resources}

* [Gestione dei progetti di traduzione](/help/sites-administering/tc-manage.md) - Scopri i dettagli dei progetti di traduzione e le funzioni aggiuntive, come i flussi di lavoro di traduzione umana e i progetti multilingue.
* [Concetti di authoring](/help/sites-authoring/author.md) - Scopri il modello dell’autore e di pubblicazione di AEM più dettagliatamente. Questo documento si concentra sull’authoring delle pagine anziché sui frammenti di contenuto, ma la teoria è ancora valida.
* [Pubblicazione delle pagine](/help/sites-authoring/publishing-pages.md) - Scopri le funzioni aggiuntive disponibili per la pubblicazione dei contenuti. Questo documento si concentra sull’authoring delle pagine anziché sui frammenti di contenuto, ma la teoria è ancora valida.
* [Ambiente e strumenti di authoring](/help/sites-authoring/author-environment-tools.md##path-selection) - AEM offre diversi meccanismi per organizzare e modificare i contenuti, tra cui un browser con percorso affidabile.
