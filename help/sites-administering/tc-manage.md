---
title: Gestione dei progetti di traduzione
seo-title: Gestione dei progetti di traduzione
description: Scopri come gestire i progetti di traduzione in AEM.
seo-description: Scopri come gestire i progetti di traduzione in AEM.
uuid: f6f79b5b-dc08-4dde-b464-719345d233a6
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: c8672774-6911-497d-837b-1e5953c4226a
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d
workflow-type: tm+mt
source-wordcount: '3427'
ht-degree: 2%

---


# Gestione di progetti di traduzione{#managing-translation-projects}

Dopo aver preparato il contenuto per la traduzione, è necessario completare la struttura della lingua creando copie della lingua mancanti e creare progetti di traduzione.

I progetti di traduzione consentono di gestire la traduzione del contenuto AEM. Un progetto di traduzione è un tipo di AEM [progetto](/help/sites-authoring/projects.md) che contiene risorse da tradurre in altre lingue. Queste risorse sono le pagine e le risorse delle [copie della lingua](/help/sites-administering/tc-prep.md) create dal master della lingua.

Quando le risorse vengono aggiunte a un progetto di traduzione, per esse viene creato un processo di traduzione. I processi forniscono i comandi e le informazioni sullo stato utilizzati per gestire i flussi di lavoro di traduzione umana e traduzione automatica eseguiti sulle risorse.

>[!NOTE]
>
>Un progetto di traduzione può contenere più processi di traduzione.

I progetti di traduzione sono elementi a lungo termine, definiti per lingua e metodo/provider di traduzione per allinearsi con la governance organizzativa per la globalizzazione. Devono essere iniziati una volta, durante la traduzione iniziale o manualmente, e rimanere in vigore per tutte le attività di aggiornamento del contenuto e della traduzione.

I progetti e i processi di traduzione vengono creati con flussi di lavoro di preparazione della traduzione. Questi flussi di lavoro dispongono di tre opzioni sia per la traduzione iniziale (Create&amp;Translate) che per gli aggiornamenti (Update Translation):

1. [Crea nuovo progetto](#creating-translation-projects-using-the-references-panel)
1. [Aggiungi a progetto esistente](#adding-pages-to-a-translation-project)
1. [Solo struttura contenuto](#creating-the-structure-of-a-language-copy)

>[!NOTE]
>
>L&#39;opzione 3 non è correlata al lavoro/progetto di traduzione. Consente di copiare il contenuto e le modifiche strutturali nel master lingua in copie (non tradotte) della lingua. È possibile utilizzare questa opzione per mantenere sincronizzati i master delle lingue, anche senza traduzione.

## Esecuzione di traduzioni iniziali e aggiornamento delle traduzioni esistenti {#performing-initial-translations-and-updating-existing-translations}

AEM rileva se viene creato un progetto di traduzione per la traduzione iniziale del contenuto o per aggiornare le copie già tradotte. Quando create un progetto di traduzione per una pagina e indicate le copie della lingua per cui state traducendo, AEM rileva se la pagina di origine esiste già nelle copie della lingua di destinazione:

* **La copia della lingua non include la pagina:** AEM considera questa situazione come la traduzione iniziale. La pagina viene immediatamente copiata nella copia della lingua e inclusa nel progetto. Quando la pagina tradotta viene importata in AEM, AEM la copia direttamente nella copia della lingua.
* **La copia della lingua include già la pagina:** AEM considera questa situazione come una traduzione aggiornata. Viene creato un lancio e al lancio viene aggiunta una copia della pagina, che viene inclusa nel progetto. Gli avvii consentono di rivedere le traduzioni aggiornate prima di eseguire il commit nella copia della lingua:

   * Quando la pagina tradotta viene importata in AEM, sovrascrive la pagina nel lancio.
   * La pagina tradotta sovrascrive la copia della lingua solo quando il lancio viene promosso.

Ad esempio, per la traduzione in francese della lingua master /content/geometrixx/en viene creata la radice del linguaggio /content/geometrixx/en. Non ci sono altre pagine nella copia in lingua francese.

* Viene creato un progetto di traduzione per la pagina /content/geometrixx/en/products e per tutte le pagine figlie, per la copia in lingua francese. Poiché la copia della lingua non include la pagina /content/geometrixx/fr/products, AEM copia immediatamente la pagina /content/geometrixx/en/products e tutte le pagine figlie nella copia in lingua francese. Le copie sono incluse anche nel progetto di traduzione.
* Viene creato un progetto di traduzione per la pagina /content/geometrixx/en e per tutte le pagine figlie, per la copia in lingua francese. Poiché la copia della lingua include la pagina che corrisponde alla pagina /content/geometrixx/en (la lingua principale), AEM copia la pagina /content/geometrixx/en e tutte le pagine figlie e le aggiunge a un lancio. Le copie sono incluse anche nel progetto di traduzione.

## Creazione di progetti di traduzione mediante il pannello Riferimenti {#creating-translation-projects-using-the-references-panel}

Create progetti di traduzione in modo da poter eseguire e gestire il flusso di lavoro per tradurre le risorse del vostro master lingua. Quando create dei progetti, specificate la pagina nel master della lingua che state traducendo e le copie della lingua per cui state eseguendo la traduzione:

* La configurazione cloud del framework di integrazione della traduzione associato alla pagina selezionata determina molte proprietà dei progetti di traduzione, ad esempio il flusso di lavoro di traduzione da utilizzare.
* Viene creato un progetto per ogni copia della lingua selezionata.
* Una copia della pagina selezionata e delle risorse associate viene creata e aggiunta a ciascun progetto. Queste copie vengono successivamente inviate al provider di traduzione per la traduzione.

È possibile specificare che sono selezionate anche le pagine figlie della pagina selezionata. In questo caso, a ciascun progetto vengono aggiunte anche copie delle pagine figlie, in modo che vengano tradotte. Quando delle pagine figlie sono associate a diverse configurazioni del framework di integrazione della traduzione, AEM crea altri progetti.

È inoltre possibile [creare manualmente progetti di traduzione](#creating-a-translation-project-using-the-projects-console).

**Traduzioni iniziali e aggiornamento traduzioni**

Il pannello Riferimenti indica se si stanno aggiornando le copie della lingua esistenti o se si sta creando la prima versione delle copie della lingua. Quando esiste una copia della lingua per la pagina selezionata, viene visualizzata la scheda Aggiorna copie lingua per consentire l&#39;accesso ai comandi relativi al progetto.

![chlimage_1-239](assets/chlimage_1-239.png)

Dopo la traduzione, è possibile [rivedere la traduzione](#reviewing-and-promoting-updated-content) prima di sovrascrivere la copia della lingua con essa. Se non esiste una copia della lingua per la pagina selezionata, viene visualizzata la scheda Crea e traduci per consentire l&#39;accesso ai comandi relativi al progetto.

![chlimage_1-240](assets/chlimage_1-240.png)

### Crea progetti di traduzione per una nuova copia della lingua {#create-translation-projects-for-a-new-language-copy}

1. Utilizzate la console Siti per selezionare la pagina che state aggiungendo ai progetti di traduzione.

   Ad esempio, per tradurre le pagine inglesi di Demo Site, selezionare Geometrixx Demo Site > English.

1. Sulla barra degli strumenti, fare clic o toccare Riferimenti.

   ![chlimage_1-241](assets/chlimage_1-241.png)

1. Selezionare Copie per lingua, quindi selezionare le copie per le quali si stanno traducendo le pagine di origine.
1. Toccate o fate clic su Crea e traslazione, quindi configurate il processo di traduzione:

   * Utilizzate il menu a discesa Lingue per selezionare una copia della lingua per la quale desiderate tradurre. Selezionate le lingue aggiuntive desiderate. Le lingue visualizzate nell&#39;elenco corrispondono alle [radici della lingua create](/help/sites-administering/tc-prep.md#creating-a-language-root).
   * Per tradurre la pagina selezionata e tutte le pagine figlie, selezionare Seleziona tutte le sottopagine. Per tradurre solo la pagina selezionata, deselezionare l’opzione.
   * Per Progetto, selezionate Crea nuovo progetto di traduzione.
   * Digitate un nome per il progetto.

   ![chlimage_1-242](assets/chlimage_1-242.png)

1. Tocca o fai clic su Crea.

### Crea progetti di traduzione per una copia lingua esistente {#create-translation-projects-for-an-existing-language-copy}

1. Utilizzate la console Siti per selezionare la pagina che state aggiungendo ai progetti di traduzione.

   Ad esempio, per tradurre le pagine inglesi di Demo Site, selezionare Geometrixx Demo Site > English.

1. Sulla barra degli strumenti, fare clic o toccare Riferimenti.

   ![chlimage_1-243](assets/chlimage_1-243.png)

1. Selezionare Copie per lingua, quindi selezionare le copie per le quali si stanno traducendo le pagine di origine.
1. Tocca o fai clic su Aggiorna Copie lingua e configura il processo di traduzione:

   * Per tradurre la pagina selezionata e tutte le pagine figlie, selezionare Seleziona tutte le sottopagine. Per tradurre solo la pagina selezionata, deselezionare l’opzione.
   * Per Progetto, selezionate Crea nuovo progetto di traduzione.
   * Digitate un nome per il progetto.

   ![chlimage_1-244](assets/chlimage_1-244.png)

1. Tocca o fai clic su Avvia.

## Aggiunta di pagine a un progetto di traduzione {#adding-pages-to-a-translation-project}

Dopo aver creato un progetto di traduzione, puoi utilizzare il riquadro Risorse per aggiungere pagine al progetto. L’aggiunta di pagine è utile quando si includono pagine da rami diversi nello stesso progetto.

Quando aggiungete delle pagine a un progetto di traduzione, le pagine vengono incluse in un nuovo processo di traduzione. È inoltre possibile [aggiungere pagine a un processo esistente](#adding-pages-assets-to-a-translation-job).

Come per la creazione di un nuovo progetto, quando si aggiungono pagine, le copie delle pagine vengono aggiunte a un lancio quando necessario per evitare di sovrascrivere le copie della lingua esistenti. (Vedere [Creazione di progetti di traduzione per copie di lingua esistenti](#performing-initial-translations-and-updating-existing-translations).)

1. Utilizzate la console Siti per selezionare la pagina che state aggiungendo al progetto di traduzione.

   Ad esempio, per tradurre le pagine inglesi di Demo Site, selezionare Geometrixx Demo Site > English.

1. Sulla barra degli strumenti, fare clic o toccare Riferimenti.

   ![chlimage_1-245](assets/chlimage_1-245.png)

1. Selezionare Copie per lingua, quindi selezionare le copie per le quali si stanno traducendo le pagine di origine.

   ![chlimage_1-35](assets/chlimage_1-35.jpeg)

1. Tocca o fai clic su Aggiorna Copie lingua, quindi configura le proprietà:

   * Per tradurre la pagina selezionata e tutte le pagine figlie, selezionare Seleziona tutte le sottopagine. Per tradurre solo la pagina selezionata, deselezionare l’opzione.
   * Per Progetto, selezionare Aggiungi a progetto di traduzione esistente.
   * Selezionate il progetto.

   >[!NOTE]
   >
   >La lingua di destinazione impostata nel progetto di traduzione deve corrispondere al percorso della copia della lingua, come mostrato nel pannello Riferimenti.

   ![chlimage_1-36](assets/chlimage_1-36.jpeg)

1. Tocca o fai clic su Avvia.

## Aggiunta di pagine/risorse a un processo di traduzione {#adding-pages-assets-to-a-translation-job}

Potete aggiungere pagine, risorse, tag o dizionari i18n al processo di traduzione del progetto di traduzione. Per aggiungere pagine o risorse:

1. Nella parte inferiore della sezione Processo di traduzione del progetto di traduzione, fate clic o toccate i puntini di sospensione.

   ![chlimage_1-246](assets/chlimage_1-246.png)

1. Tocca o fai clic su Aggiungi e pagine/risorse.

   ![chlimage_1-247](assets/chlimage_1-247.png)

1. Selezionate l&#39;elemento superiore del ramo che desiderate aggiungere, quindi toccate o fate clic sull&#39;icona del segno di spunta. Potete selezionare più utenti.

   ![chlimage_1-248](assets/chlimage_1-248.png)

1. In alternativa, potete selezionare l’icona di ricerca per cercare facilmente le pagine o le risorse da aggiungere al processo di traduzione.

   ![chlimage_1-249](assets/chlimage_1-249.png)

Le pagine e/o le risorse vengono aggiunte al processo di traduzione.

## Aggiunta di dizionari i18n a un processo di traduzione {#adding-i-n-dictionaries-to-a-translation-job}

Potete aggiungere pagine, risorse, tag o dizionari i18n al processo di traduzione del progetto di traduzione. Per aggiungere un dizionario i18n:

1. Nella parte inferiore della sezione Processo di traduzione del progetto di traduzione, fate clic o toccate i puntini di sospensione.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. Tocca o fai clic su Aggiungi e Dizionario I18N.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Selezionate il dizionario che desiderate aggiungere, quindi fate clic o toccate il pulsante Aggiungi.

   ![chlimage_1-252](assets/chlimage_1-252.png)

Il tuo dizionario ora è nel tuo lavoro di traduzione.

![chlimage_1-253](assets/chlimage_1-253.png)

>[!NOTE]
>
>Per ulteriori informazioni sui dizionari i18n, consultare [Using Translator to Manage Dictionaries](/help/sites-developing/i18n-translator.md) (Utilizzo di Translator per gestire i dizionari).

## Aggiunta di tag a un processo di traduzione {#adding-tags-to-a-translation-job}

Potete aggiungere pagine, risorse, tag o dizionari i18n al processo di traduzione del progetto di traduzione. Per aggiungere tag:

1. Nella parte inferiore della sezione Processo di traduzione del progetto di traduzione, fate clic o toccate i puntini di sospensione.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. Tocca o fai clic su Aggiungi, quindi su Tag.

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. Selezionate i tag da aggiungere, quindi toccate o fate clic sull&#39;icona del segno di spunta. Potete selezionare più utenti.

   ![chlimage_1-256](assets/chlimage_1-256.png)

I tag vengono ora aggiunti al processo di traduzione.

![chlimage_1-257](assets/chlimage_1-257.png)

## Visualizzazione dei dettagli del progetto di traduzione {#seeing-translation-project-details}

Il riquadro Riepilogo conversione contiene le proprietà configurate per un progetto di traduzione. Oltre alle informazioni generali [sul progetto](/help/sites-authoring/projects.md#project-info), la scheda Traduzione contiene proprietà specifiche per la traduzione:

* Lingua di origine: Lingua delle pagine che vengono tradotte.
* Lingua di destinazione: Lingua in cui vengono tradotte le pagine.
* Metodo di traduzione: Flusso di lavoro di traduzione. È supportata la traduzione umana o la traduzione automatica.
* Provider di traduzione: Provider di servizi di traduzione che esegue la traduzione.
* Categoria contenuto: (Traduzione automatica) La categoria di contenuto utilizzata per la traduzione.
* Configurazione cloud: Configurazione cloud per il connettore del servizio di traduzione utilizzato per il progetto.

Quando un progetto viene creato utilizzando il riquadro Risorse di una pagina, queste proprietà vengono configurate automaticamente in base alle proprietà della pagina di origine.

![chlimage_1-258](assets/chlimage_1-258.png)

## Monitoraggio dello stato di un processo di traduzione {#monitoring-the-status-of-a-translation-job}

La sezione Processo di traduzione di un progetto di traduzione fornisce lo stato di un processo di traduzione, nonché il numero di pagine e risorse del processo.

![chlimage_1-259](assets/chlimage_1-259.png)

La tabella seguente descrive ogni stato che un processo o un elemento del processo può avere:

| Stato | Descrizione |
|---|---|
| Bozza | Il processo di traduzione non è stato avviato. I processi di conversione sono nello stato DRAFT al momento della creazione. |
| Inviato | I file nel processo di traduzione hanno questo stato quando sono stati correttamente inviati al servizio di traduzione. Questo stato può verificarsi dopo l&#39;attivazione del comando Request Scope o del comando Start. |
| Conteggio richiesto | Per il flusso di lavoro di traduzione umana, i file del processo sono stati inviati al fornitore della traduzione per l’ambito. Questo stato viene visualizzato dopo che è stato emesso il comando Ambito richiesta. |
| Conteggio completato | Il fornitore ha eseguito l&#39;ambito del processo di traduzione. |
| Impegnato per la traduzione | Il proprietario del progetto ha accettato l&#39;ambito. Questo stato indica che il fornitore della traduzione deve iniziare a tradurre i file nel processo. |
| Traduzione in corso | Per un processo, la traduzione di uno o più file nel processo non è ancora completa. Per un elemento del processo, l’elemento viene convertito. |
| Tradotto | Per un processo, la traduzione di tutti i file nel processo è completa. Per un elemento del processo, l’elemento viene convertito. |
| Pronto per la revisione | L’elemento nel processo viene convertito e il file è stato importato in AEM. |
| Completa | Il proprietario del progetto ha indicato che il contratto di traduzione è completo. |
| Annulla | Indica che il fornitore della traduzione deve smettere di lavorare su un processo di traduzione. |
| Aggiornamento errore | Si è verificato un errore durante il trasferimento dei file tra AEM e il servizio di traduzione. |
| Stato sconosciuto | Errore sconosciuto. |

Per visualizzare lo stato di ciascun file nel processo, toccate o fate clic sui puntini di sospensione nella parte inferiore della sezione.

## Impostazione della data di scadenza dei processi di traduzione {#setting-the-due-date-of-translation-jobs}

Specificare la data prima della quale il fornitore della traduzione deve restituire i file convertiti. Potete impostare la data di scadenza per il progetto o per un processo specifico:

* **Progetto: i processi di** traduzione nel progetto ereditano la data di scadenza.
* **Processo:** la data di scadenza impostata per il processo ha la priorità sulla data di scadenza impostata per il progetto.

L&#39;impostazione della data di scadenza funziona correttamente solo quando il fornitore di traduzione utilizzato supporta questa funzione.

La procedura seguente imposta la data di scadenza per un progetto.

1. Tocca o fai clic sui puntini di sospensione nella parte inferiore della sezione Riepilogo traduzione.

   ![chlimage_1-260](assets/chlimage_1-260.png)

1. Nella scheda Base, utilizzare il selettore data della proprietà Data scadenza per selezionare la data di scadenza.

   ![chlimage_1-261](assets/chlimage_1-261.png)

1. Tocca o fai clic su Fine.

La procedura seguente imposta la data di scadenza per un processo di traduzione.

1. Nella sezione Processo di traduzione, tocca o fai clic sul menu dei comandi, quindi tocca o fai clic su Data scadenza.

   ![chlimage_1-262](assets/chlimage_1-262.png)

1. Nella finestra di dialogo, fare clic o toccare l&#39;icona del calendario, quindi selezionare la data e l&#39;ora da utilizzare come data di scadenza, quindi fare clic su Salva.

   ![chlimage_1-263](assets/chlimage_1-263.png)

## Applicazione dell&#39;ambito a un processo di traduzione {#scoping-a-translation-job}

Ambito di un processo di traduzione per ottenere una stima del costo della traduzione dal provider del servizio di traduzione. Quando eseguite l’ambito di un processo, i file sorgente vengono inviati al fornitore di traduzione che confronta il testo con il proprio pool di traduzioni memorizzate (memoria di traduzione). In genere, l&#39;ambito corrisponde al numero di parole che devono essere tradotte.

Per ottenere ulteriori informazioni sui risultati dell&#39;ambito, contattare il fornitore della traduzione.

>[!NOTE]
>
>L&#39;ambito è facoltativo. Potete avviare un processo di traduzione senza ambito.

Quando eseguite l’ambito di un processo di traduzione, lo stato del processo è `Scope Requested`. Quando il fornitore di traduzione restituisce l&#39;ambito, lo stato viene cambiato in `Scope Completed`. Al termine dell&#39;ambito è possibile utilizzare il comando Mostra ambito per controllare i risultati dell&#39;ambito.

L&#39;ambito funziona correttamente solo quando il fornitore di traduzione che utilizzi supporta questa funzione.

1. Nella console Progetti, aprite il progetto di traduzione.
1. Nella sezione Processo di traduzione, tocca o fai clic sul menu dei comandi, quindi tocca o fai clic su Richiedi ambito.

   ![chlimage_1-264](assets/chlimage_1-264.png)

1. Quando lo stato del processo cambia in SCOPE_COMPLETED, nella sezione Processo di traduzione fate clic o toccate il menu dei comandi, quindi fate clic o toccate Mostra ambito.

## Avvio di un processo di traduzione {#starting-a-translation-job}

Avviate un processo di traduzione per tradurre le pagine di origine nella lingua di destinazione. La conversione viene eseguita in base ai valori delle proprietà della sezione Riepilogo conversione.

Dopo aver avviato il processo di traduzione, il riquadro Processo di traduzione mostra lo stato di traduzione in corso.

![chlimage_1-265](assets/chlimage_1-265.png)

1. Nella console Progetti, aprite il progetto di traduzione.
1. Nella sezione Processo di traduzione, tocca o fai clic sul menu dei comandi, quindi tocca o fai clic su Avvia.

   ![chlimage_1-266](assets/chlimage_1-266.png)

1. Nella finestra di dialogo Azione che conferma l’avvio della traduzione, fate clic o toccate Chiudi.

## Annullamento di un processo di traduzione {#canceling-a-translation-job}

Annullate un processo di traduzione per arrestare il processo di traduzione e impedire al fornitore di traduzione di eseguire ulteriori traduzioni. Potete annullare un processo quando il processo ha lo stato `Committed For Translation` o `Translation In Progress`.

1. Nella console Progetti, aprite il progetto di traduzione.
1. Nella sezione Processo di traduzione, tocca o fai clic sul menu dei comandi, quindi tocca o fai clic su Annulla.
1. Nella finestra di dialogo Azione che conferma l’annullamento della traduzione, fate clic o toccate OK.

## Accetta/Rifiuta flusso di lavoro {#accept-reject-workflow}

Quando il contenuto torna dopo la traduzione ed è in stato Pronto per la revisione, potete eseguire il processo di traduzione e accettare/rifiutare il contenuto.

![chlimage_1-267](assets/chlimage_1-267.png)

Se selezionate Rifiuta traduzione, potete aggiungere un commento.

![chlimage_1-268](assets/chlimage_1-268.png)

Il rifiuto del contenuto lo invia nuovamente al fornitore di traduzione, dove sarà in grado di visualizzare il commento.

## Revisione e promozione dei contenuti aggiornati {#reviewing-and-promoting-updated-content}

Quando il contenuto viene tradotto per una copia esistente della lingua, rivedete le traduzioni, apportate le modifiche se necessario, quindi promuovete le traduzioni per spostarlo nella copia della lingua. Potete esaminare i file convertiti quando il processo di traduzione mostra lo stato Pronto per la revisione.

![chlimage_1-269](assets/chlimage_1-269.png)

1. Selezionate la pagina nello schema lingua, toccate o fate clic su Riferimenti, quindi fate clic o toccate Copie lingua.
1. Tocca o fai clic sulla copia della lingua per eseguire la revisione.

   ![chlimage_1-270](assets/chlimage_1-270.png)

1. Tocca o fai clic su Avvia per visualizzare i comandi relativi al lancio.

   ![chlimage_1-271](assets/chlimage_1-271.png)

1. Per aprire la copia del lancio della pagina per esaminare e modificare il contenuto, fate clic su Apri pagina.
1. Dopo aver rivisto il contenuto e apportato le modifiche necessarie, per promuovere la copia del lancio fate clic su Promuovi.
1. Nella pagina Promuovi lancio, specificate le pagine da promuovere, quindi toccate o fate clic su Promuovi.

## Confronto delle copie delle lingue {#comparing-language-copies}

Per confrontare le copie della lingua con la lingua principale:

1. Nella console **Siti**, passare alla copia della lingua da confrontare.
1. Aprite il pannello **[Riferimenti](/help/sites-authoring/basic-handling.md#references)**.
1. Sotto l&#39;intestazione **Copie** selezionare **Copie lingua.**
1. Selezionare la copia della lingua desiderata e quindi fare clic su **Compare to Master **o **Compare to Previous **se applicabile.

   ![chlimage_1-37](assets/chlimage_1-37.jpeg)

1. Le due pagine (di lancio e di origine) verranno aperte una accanto all&#39;altra.

   Per informazioni complete sull&#39;utilizzo di questa funzionalità, consulta [Differenze tra pagine](/help/sites-authoring/page-diff.md).

## Completamento e archiviazione dei processi di traduzione {#completing-and-archiving-translation-jobs}

Completate un processo di traduzione dopo aver rivisto i file convertiti dal fornitore. Per i flussi di lavoro di traduzione umana, il completamento di una traduzione indica al fornitore che il contratto di traduzione è stato soddisfatto e che devono salvare la traduzione nella propria memoria di traduzione.

Dopo aver completato il processo, il processo ha lo stato Completato.

![chlimage_1-272](assets/chlimage_1-272.png)

Dopo il completamento, archiviate un processo di traduzione e non dovrete più visualizzare i dettagli sullo stato del processo. Quando archiviate il processo, la sezione Processo di traduzione viene rimossa dal progetto.

## Creazione della struttura di una copia della lingua {#creating-the-structure-of-a-language-copy}

Compilate la copia per lingua in modo che contenga il contenuto della lingua principale che state traducendo. Prima di compilare la copia per lingua, è necessario che sia stata creata [la lingua principale](/help/sites-administering/tc-prep.md#creating-a-language-root) della copia per lingua.

1. Utilizzare la console Siti per selezionare la lingua principale della lingua principale utilizzata come origine. Ad esempio, per tradurre le pagine inglesi del Sito Demo di Geometrixx, selezionare Contenuto > Sito Demo di Geometrixx > Inglese.
1. Sulla barra degli strumenti, fare clic o toccare Riferimenti.

   ![chlimage_1-273](assets/chlimage_1-273.png)

1. Selezionare Copie per lingua, quindi selezionare le copie per lingua da compilare.

   ![chlimage_1-38](assets/chlimage_1-38.jpeg)

1. Tocca o fai clic su Aggiorna copie lingua per visualizzare gli strumenti di conversione e configurare le proprietà:

   * Selezionare l&#39;opzione Seleziona tutte le sottopagine.
   * Per Progetto, selezionate Crea solo struttura.

   ![chlimage_1-39](assets/chlimage_1-39.jpeg)

1. Tocca o fai clic su Avvia.

## Creazione di un progetto di traduzione tramite la console Progetti {#creating-a-translation-project-using-the-projects-console}

Se preferite usare la console Progetti, potete creare manualmente un progetto di traduzione.

Quando si crea manualmente un progetto di traduzione, è necessario fornire valori per le seguenti proprietà relative alla conversione oltre alle proprietà [di base](/help/sites-authoring/touch-ui-managing-projects.md#creating-a-project):

* **Nome:Nome** progetto.
* **Lingua di origine:** la lingua del contenuto di origine.
* **Lingua di destinazione:** la lingua in cui viene tradotto il contenuto.
* **Metodo di traduzione:** selezionate Traduzione umana per indicare che la traduzione deve essere eseguita manualmente.

1. Nella barra degli strumenti della console Progetti, fate clic o toccate Crea.
1. Selezionate il modello Progetto di traduzione e quindi fate clic o toccate Avanti.
1. Immettete i valori per le proprietà Base.
1. Tocca o fai clic su Avanzate e specifica i valori per le proprietà di conversione.
1. Tocca o fai clic su Crea. Nella casella di conferma, fate clic o toccate Fine per tornare alla console Progetti oppure toccate o fate clic su Apri progetto per aprire e iniziare a gestire il progetto.

## Esportazione di un processo di conversione {#exporting-a-translation-job}

È possibile scaricare il contenuto di un processo di traduzione, ad esempio per inviarlo a un provider di traduzione che non è integrato con AEM tramite un connettore, o per revisionare il contenuto.

1. Dal menu a discesa della sezione Processo di traduzione, fate clic o toccate Esporta.
1. Nella finestra di dialogo Esporta, fate clic su o toccate Scarica file esportato e, se necessario, usate la finestra di dialogo del browser Web per salvare il file.
1. Nella finestra di dialogo Esporta, fate clic o toccate Chiudi.

## Importazione di un processo di conversione {#importing-a-translation-job}

È possibile importare contenuti tradotti in AEM, ad esempio quando il provider di traduzioni li invia a voi perché non sono integrati con AEM tramite un connettore.

1. Dal menu a discesa della sezione Processo di traduzione, fate clic o toccate Importa.
1. Utilizzate la finestra di dialogo del browser Web per selezionare il file da importare.
1. Nella finestra di dialogo Importa, fare clic su o toccare Chiudi.

