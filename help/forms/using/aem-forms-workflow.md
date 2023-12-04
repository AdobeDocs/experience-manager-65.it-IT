---
title: Flusso di lavoro incentrato su Forms su OSGi
description: Utilizza AEM Forms Workflow per automatizzare e creare rapidamente revisioni e approvazioni per avviare i servizi di documentazione
topic-tags: publish, document_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: c3e5f8fc-d2b9-4f76-9a3d-4bc5733f5a5c
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '3667'
ht-degree: 1%

---

# Flusso di lavoro incentrato su Forms su OSGi{#forms-centric-workflow-on-osgi}

![immagine protagonista](do-not-localize/header.png)

Le aziende raccolgono dati da centinaia e migliaia di moduli, da vari sistemi back-end e da origini dati online o offline. Hanno anche un set dinamico di utenti per prendere decisioni sui dati, che comporta processi iterativi di revisione e approvazione.

Oltre ai flussi di lavoro di revisione e approvazione per il pubblico interno ed esterno, le grandi organizzazioni e le aziende hanno attività ripetitive. Ad esempio, la conversione di un documento PDF in un altro formato. Se eseguite manualmente, queste attività richiedono molto tempo e risorse. Le aziende hanno anche l&#39;obbligo legale di firmare digitalmente un documento e archiviare i dati dei moduli per un successivo utilizzo in formati predefiniti.

## Introduzione al flusso di lavoro incentrato su Forms su OSGi {#introduction-to-forms-centric-workflow-on-osgi}

Puoi utilizzare i flussi di lavoro dell’AEM per creare rapidamente flussi di lavoro adattivi basati su moduli. Questi flussi di lavoro possono essere utilizzati per revisioni e approvazioni, flussi di processi aziendali, per avviare servizi documentali, per l’integrazione con il flusso di lavoro della firma di Adobe Sign e per operazioni simili. Ad esempio, l&#39;elaborazione dell&#39;applicazione della carta di credito, il dipendente lascia i flussi di lavoro di approvazione, salvando un modulo come documento PDF. Inoltre, questi flussi di lavoro possono essere utilizzati all’interno di un’organizzazione o attraverso un firewall di rete.

Con un flusso di lavoro incentrato su Forms su OSGi, puoi creare e distribuire rapidamente flussi di lavoro per varie attività sullo stack OSGi, senza dover installare la funzionalità completa di gestione dei processi sullo stack JEE. Lo sviluppo e la gestione dei flussi di lavoro si basano sulle familiari funzionalità del Flusso di lavoro AEM e della Casella in entrata AEM. I flussi di lavoro costituiscono la base per automatizzare i processi aziendali reali che si estendono su più sistemi software, reti, reparti e persino organizzazioni.

Una volta configurati, questi flussi di lavoro possono essere attivati manualmente per completare un processo definito o essere eseguiti a livello di programmazione quando gli utenti inviano un modulo o [gestione della corrispondenza](/help/forms/using/cm-overview.md) lettera. Grazie alle migliorate funzionalità del flusso di lavoro dell’AEM, AEM Forms offre due funzionalità distinte, ma simili. Come parte della strategia di implementazione, devi decidere quale funziona per te. Vedi un [confronto](capabilities-osgi-jee-workflows.md) dei flussi di lavoro AEM incentrati su Forms su OSGi e Gestione dei processi su JEE. Inoltre, per la topologia di distribuzione, vedi, [Architettura e topologie di implementazione per AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

Estensione del flusso di lavoro incentrato su Forms per OSGi [Casella in entrata AEM](/help/sites-authoring/inbox.md) e fornisce componenti aggiuntivi (passaggi) che consentono all’editor di flussi di lavoro AEM di aggiungere supporto per flussi di lavoro incentrati su AEM Forms. La Casella in entrata AEM estesa ha funzionalità simili a [AEM Forms Workspace](introduction-html-workspace.md). Oltre a gestire flussi di lavoro incentrati sulla persona (approvazione, revisione e così via), puoi utilizzare flussi di lavoro AEM per automatizzare [servizi documentali](/help/sites-developing/workflows-step-ref.md)documenti relativi alle operazioni (ad esempio Generate PDF) e alla firma elettronica (Adobe Sign).

Tutti i passaggi del flusso di lavoro di AEM Forms supportano l’utilizzo di variabili. Le variabili consentono ai passaggi del flusso di lavoro di conservare e trasmettere metadati tra i passaggi in fase di esecuzione. Puoi creare diversi tipi di variabili per memorizzare diversi tipi di dati. Puoi anche creare raccolte di variabili (array) per memorizzare più istanze di dati correlati dello stesso tipo. In genere, si utilizza una variabile o una raccolta di variabili quando è necessario prendere una decisione in base al valore in essa contenuto o per memorizzare le informazioni necessarie in un secondo momento di un processo. Per ulteriori informazioni sull’utilizzo delle variabili in questi componenti del flusso di lavoro incentrati su Forms (passaggi), consulta [Flusso di lavoro incentrato su Forms su OSGi - Riferimento passaggio](../../forms/using/aem-forms-workflow-step-reference.md). Per informazioni sulla creazione e la gestione delle variabili, consulta [Variabili nei flussi di lavoro AEM](../../forms/using/variable-in-aem-workflows.md).

Il diagramma seguente illustra la procedura end-to-end per creare, eseguire e monitorare un flusso di lavoro incentrato su Forms su OSGi.

![introduction-to-aem-forms-workflow](assets/introduction-to-aem-forms-workflow.jpg)

## Prima di iniziare {#before-you-start}

* Un flusso di lavoro è una rappresentazione di un processo aziendale reale. Tenere pronto il processo aziendale reale e l&#39;elenco dei partecipanti al processo aziendale. Inoltre, tieni il materiale collaterale (moduli adattivi, documenti PDF e altro) pronto prima di iniziare a creare un flusso di lavoro.
* Un flusso di lavoro può avere più fasi. Queste fasi vengono visualizzate nella Casella in entrata AEM e aiutano a segnalare l’avanzamento del flusso di lavoro. Dividere il processo aziendale in fasi logiche.
* Puoi configurare il passaggio di assegnazione delle attività dei flussi di lavoro AEM per inviare notifiche e-mail agli utenti o agli assegnatari. Quindi, [abilitare le notifiche e-mail](#configure-email-service).
* Un flusso di lavoro può inoltre utilizzare il segno Adobe per le firme digitali. Se prevedi di utilizzare Adobe Sign in un flusso di lavoro, il [configurare Adobe Sign per AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md) prima di utilizzarlo in un flusso di lavoro.

## Creare un modello di flusso di lavoro {#create-a-workflow-model}

Un modello di flusso di lavoro è costituito dalla logica e dal flusso di un processo aziendale. È costituito da una serie di passaggi. Questi passaggi sono componenti dell’AEM. Puoi estendere i passaggi del flusso di lavoro con parametri e script per fornire più funzionalità e controllo, in base alle esigenze. AEM Forms fornisce alcuni passaggi in aggiunta ai passaggi predefiniti dell’AEM. Per un elenco dettagliato delle fasi di AEM e AEM Forms, vedi [Riferimento della fase del flusso di lavoro AEM](/help/sites-developing/workflows-step-ref.md) e [Flusso di lavoro incentrato su Forms su OSGi - Riferimento passaggio](../../forms/using/aem-forms-workflow.md).

L’AEM fornisce un’interfaccia utente intuitiva per creare un modello di flusso di lavoro utilizzando i passaggi del flusso di lavoro forniti. Per istruzioni dettagliate sulla creazione di un modello di flusso di lavoro, consulta [Creazione di modelli di flussi di lavoro](/help/sites-developing/workflows-models.md). L’esempio seguente fornisce istruzioni dettagliate per creare un modello di flusso di lavoro per un flusso di lavoro di approvazione e revisione:

>[!NOTE]
>
>Per creare o modificare un modello di flusso di lavoro è necessario essere membri del gruppo editor flusso di lavoro.

### Creare un modello per un flusso di lavoro di approvazione e revisione {#create-a-model-for-an-approval-and-review-workflow}

I flussi di lavoro di approvazione e revisione sono per le attività che richiedono l’intervento umano per prendere decisioni. L’esempio seguente crea un modello di flusso di lavoro per una richiesta di prestito ipotecario che deve essere compilata da un agente bancario di front-office. Una volta compilata, la domanda viene inviata per l’approvazione. Successivamente, la domanda approvata viene inviata al richiedente per le firme elettroniche utilizzando Adobe Sign.

L’esempio è disponibile come pacchetto allegato di seguito. Importa e installa l’esempio utilizzando Gestione pacchetti. Per creare manualmente il modello di flusso di lavoro per l&#39;applicazione, è inoltre possibile effettuare le operazioni riportate di seguito.

Nell&#39;esempio viene creato un modello di flusso di lavoro per una richiesta di mutuo che deve essere compilata da un agente bancario di front-office. Una volta compilata, la domanda viene inviata per l&#39;approvazione. Successivamente, l’applicazione approvata viene inviata al cliente per le firme elettroniche utilizzando Adobe Sign. Puoi importare e installare l’esempio utilizzando Gestione pacchetti.

[Ottieni file](assets/example-mortgage-loan-application.zip)

1. Apri la console Modelli di flusso di lavoro. L’URL predefinito è `https://[server]:[port]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models`
1. Seleziona **Crea**, quindi **Crea modello**. Viene visualizzata la finestra di dialogo Aggiungi modello flusso di lavoro.
1. Inserisci il **Titolo** e **Nome** (facoltativo). Ad esempio, una richiesta di ipoteca. Seleziona **Fine**.
1. Seleziona il modello di flusso di lavoro appena creato e seleziona **Modifica**. Ora è possibile aggiungere passaggi del flusso di lavoro per creare una logica di business. La prima volta che crei un modello di flusso di lavoro, contiene:

   * I passaggi: Inizio flusso e Fine flusso. Questi passaggi rappresentano l’inizio e la fine del flusso di lavoro. Questi passaggi sono necessari e non possono essere modificati o rimossi.
   * Un esempio di passaggio Partecipante denominato Passaggio 1. Questo passaggio è configurato per assegnare un elemento di lavoro all’utente amministratore. Rimuovi questo passaggio.

1. Abilita le notifiche e-mail. Puoi configurare il flusso di lavoro incentrato su Forms su OSGi per inviare notifiche e-mail agli utenti o agli assegnatari. Per abilitare le notifiche e-mail, effettua le seguenti configurazioni:

   1. Vai a Gestione configurazione AEM all’indirizzo `https://[server]:[port]/system/console/configMgr`.
   1. Apri **[!UICONTROL Day CQ Mail Service]** configurazione. Specifica un valore per **[!UICONTROL Nome host del server SMTP]**, **[!UICONTROL porta del server SMTP,]** e **[!UICONTROL Indirizzo &quot;Da&quot;]** campi. Fai clic su **[!UICONTROL Salva]**.
   1. Apri **[!UICONTROL Day CQ Link Externalizer]** configurazione. In **[!UICONTROL Domini]** , specificare il nome host/indirizzo IP effettivo e il numero di porta per le istanze locali, di authoring e di pubblicazione. Fai clic su **[!UICONTROL Salva]**.

1. Creare fasi del flusso di lavoro. Un flusso di lavoro può avere più fasi. Queste fasi vengono visualizzate nella casella in entrata AEM e segnalano l’avanzamento del flusso di lavoro.

   Per definire uno stadio, selezionare ![info-circle](assets/info-circle.png) per aprire le proprietà del modello di flusso di lavoro, aprire **Fasi** , aggiungere fasi per il modello di flusso di lavoro e selezionare **Salva e chiudi**. Nell&#39;esempio di richiesta di mutuo, creare fasi: richiesta di prestito, stato della richiesta di prestito, documenti da firmare e documento di prestito firmato.

1. Trascina la selezione **Assegna attività** passa al modello di flusso di lavoro. Rendete il primo passo del modello.

   Il componente Assegna attività assegna l’attività, creata da un flusso di lavoro, a un utente o a un gruppo. Oltre ad assegnare l’attività, puoi utilizzare il componente per specificare un modulo adattivo o un PDF non interattivo per l’attività. Il modulo adattivo è necessario per accettare l’input degli utenti e dei PDF non interattivi, oppure un modulo adattivo di sola lettura viene utilizzato per i flussi di lavoro di sola revisione.

   È inoltre possibile utilizzare il passaggio per controllare il comportamento dell&#39;attività. Ad esempio, la creazione di un documento di record automatico, l’assegnazione dell’attività a un utente o gruppo specifico, il percorso dei dati inviati, il percorso dei dati da precompilare e le azioni predefinite. Per informazioni dettagliate sulle opzioni del passaggio Assegna attività, vedere [Flusso di lavoro incentrato su Forms su OSGi - Riferimento passaggio](../../forms/using/aem-forms-workflow.md) documento.

   ![workflow-editor](assets/workflow-editor.png)

   Per l’esempio di applicazione ipotecaria, configura la fase Assegna attività per utilizzare un modulo adattivo di sola lettura e visualizzare un documento PDF una volta completata l’attività. Inoltre, seleziona un gruppo di utenti autorizzato ad approvare la richiesta di prestito. Il giorno **Azioni** , disabilita la **Invia** opzione. Creare un **actionTaken** variabile del tipo di dati String e specificare la variabile come **Variabile percorso**. Ad esempio, actionTaken. Aggiungere inoltre le route di approvazione e rifiuto. I percorsi vengono visualizzati come azioni separate (pulsanti) nella casella in entrata AEM. Il flusso di lavoro seleziona un ramo in base all’azione (pulsante) toccata da un utente.

   Puoi importare il pacchetto di esempio, disponibile per il download all’inizio della sezione, per il set completo di valori di tutti i campi della fase assegna attività configurata, ad esempio, applicazione ipotecaria.

1. Trascina il componente Divisione OR dal browser dei passaggi al modello di flusso di lavoro. La suddivisione OR crea una suddivisione nel flusso di lavoro, dopo la quale è attivo un solo ramo. Questo passaggio ti consente di introdurre nel flusso di lavoro i percorsi di elaborazione condizionale. Puoi aggiungere i passaggi del flusso di lavoro a ogni ramo in base alle esigenze.

   È possibile definire un&#39;espressione di indirizzamento per un ramo utilizzando una definizione di regola, uno script ECMA o uno script esterno.

   Utilizza l’editor espressioni per creare espressioni di indirizzamento per Ramo 1 e Ramo 2. Queste espressioni di indirizzamento aiutano a scegliere un ramo in base all’azione dell’utente nella casella in entrata AEM.

   **Espressione di indirizzamento per ramo 1**

   Quando un utente tocca **Approva** nella casella in entrata AEM, è attivato il ramo 1.

   ![Esempio di suddivisione OR](assets/orsplit_branch1_active_new.png)

   **Espressione di indirizzamento per il ramo 2**

   Quando un utente tocca **Rifiuta** nella casella in entrata AEM è attivato il ramo 2.

   ![Esempio di suddivisione OR](assets/orsplit_branch2_active_new.png)

   Per informazioni sulla creazione di espressioni di indirizzamento tramite variabili, vedere [Variabili nei flussi di lavoro di AEM Forms](../../forms/using/variable-in-aem-workflows.md).

1. Aggiungi altri passaggi del flusso di lavoro per creare la logica di business.

   Per l&#39;esempio del mutuo, aggiungere un documento di record generato, due passaggi dell&#39;attività assegnati e un passaggio del documento di firma al ramo 1 del modello, come illustrato nell&#39;immagine seguente. Un passaggio dell’attività di assegnazione consiste nel visualizzare e inviare **documenti di prestito da firmare al richiedente** e un altro componente assegna attività è **per visualizzare i documenti firmati**. Aggiungete inoltre un componente Assegna attività al ramo 2. Viene attivato quando un utente tocca Rifiuta nella casella in entrata AEM.

   Per il set completo di valori di tutti i campi dei passaggi dell’attività Assegna, del passaggio del documento record e del passaggio del documento firma configurati, ad esempio, per l’applicazione ipotecaria, importa il pacchetto di esempio, disponibile per il download all’inizio di questa sezione.

   Il modello di flusso di lavoro è pronto. Puoi avviare il flusso di lavoro attraverso vari metodi. Per ulteriori informazioni, consulta [Avviare un flusso di lavoro incentrato su Forms su OSGi](#launch).

   ![workflow-editor-mortgage](assets/workflow-editor-mortgage.png)

## Creazione di un&#39;applicazione per flussi di lavoro incentrata su Forms {#create-a-forms-centric-workflow-application}

L’applicazione è il modulo adattivo associato al flusso di lavoro. Quando un’applicazione viene inviata tramite Casella in entrata, avvia il flusso di lavoro associato. Per rendere un flusso di lavoro Forms disponibile come applicazione nella casella in entrata AEM e nell’app AEM Forms, effettua le seguenti operazioni per creare un’applicazione per flusso di lavoro:

>[!NOTE]
>
>Per poter creare e gestire le applicazioni del flusso di lavoro è necessario essere membri del gruppo fd-administrator.

1. Nell’istanza di authoring dell’AEM, vai a ![tools-1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL Gestisci applicazione flusso di lavoro]** e tocchi **[!UICONTROL Crea]**.
1. Nella finestra Crea applicazione flusso di lavoro, specificare gli input per i campi seguenti e toccare **Crea**. Viene creata una nuova applicazione, che viene elencata nella schermata Applicazioni flusso di lavoro.

<table>
 <tbody>
  <tr>
   <td>Campo</td>
   <td>Descrizione</td>
  </tr>
  <tr>
   <td>Titolo</td>
   <td>Il titolo è visibile nella casella in entrata AEM e consente agli utenti di scegliere un’applicazione. Tienilo descrittivo. Ad esempio, l'applicazione di apertura del conto di risparmio.<br /> </td>
  </tr>
  <tr>
   <td>Nome </td>
   <td>Specificare il nome dell'applicazione. Tutti i caratteri diversi da lettere, numeri, trattini e caratteri di sottolineatura vengono sostituiti da trattini. </td>
  </tr>
  <tr>
   <td>Descrizione</td>
   <td>La descrizione è visibile nella casella in entrata AEM. Fornisci informazioni dettagliate sull’applicazione nei campi di descrizione. Ad esempio, Scopo dell’applicazione.<br /> </td>
  </tr>
  <tr>
   <td>Modulo adattivo</td>
   <td><p>Specifica il percorso di un modulo adattivo. Quando un utente avvia un’applicazione, viene visualizzato il modulo adattivo specificato.</p> <p><strong>Nota</strong>: le applicazioni per flussi di lavoro non supportano moduli e documenti PDF che hanno una lunghezza superiore a una pagina o richiedono lo scorrimento su Apple iPad. Quando un’applicazione viene aperta su Apple iPad e il modulo adattivo o il documento PDF è più lungo di una pagina, i campi modulo e il contenuto della seconda pagina vengono persi.</p> </td>
  </tr>
  <tr>
   <td>Gruppo di accesso</td>
   <td><p>Selezionare un gruppo. L'applicazione è visibile nella casella in entrata AEM solo per i membri del gruppo selezionato. L’opzione gruppo di accesso rende disponibili per la selezione tutti i gruppi del gruppo flusso di lavoro-utenti. </p> <br /> </td>
  </tr>
  <tr>
   <td>Servizio preriempimento</td>
   <td>Seleziona un <a href="../../forms/using/prepopulate-adaptive-form-fields.md#aem-forms-custom-prefill-service" target="_blank">servizio preriempimento</a> per il modulo adattivo.<br /> </td>
  </tr>
  <tr>
   <td>Modello flusso di lavoro</td>
   <td>Seleziona un <a href="../../forms/using/aem-forms-workflow.md#create-a-workflow-model">modello di flusso di lavoro</a> per l'applicazione. Un modello di flusso di lavoro è costituito dalla logica e dal flusso del processo aziendale. </td>
  </tr>
  <tr>
   <td>Percorso del file di dati</td>
   <td>Specifica il percorso del file di dati in crx-repository. Il percorso è relativo al payload del modulo adattivo e contiene il nome del file di dati. Includi sempre il nome completo del file, inclusa l’estensione, se applicabile. Ad esempio, [payload]/data.xml. </td>
  </tr>
  <tr>
   <td>Percorso allegato</td>
   <td>Specifica il percorso della cartella degli allegati in crx-repository. Il percorso dell'allegato è relativo alla posizione del payload. Ad esempio, [payload]/data.xml. </td>
  </tr>
  <tr>
   <td>Percorso del documento record</td>
   <td>Specifica il percorso del file del documento record nell’archivio crx. Il percorso è relativo alla posizione del payload del modulo adattivo. Includi sempre il nome completo del file, inclusa l’estensione, se applicabile. Ad esempio, [payload]/DOR/creditcard.pdf.</td>
  </tr>
 </tbody>
</table>

## Avviare un flusso di lavoro incentrato su Forms su OSGi {#launch}

Puoi avviare o attivare un flusso di lavoro incentrato su Forms:

* [Invio di una domanda dalla casella in entrata AEM](#inbox)
* [Invio di un’applicazione dall’app AEM Forms](#afa)

* [Invio di un modulo adattivo](#af)
* [Utilizzo della cartella controllata](#watched)

* [Invio di una comunicazione interattiva o di una lettera](#letter)

### Invio di una domanda dalla casella in entrata AEM {#inbox}

L&#39;applicazione del flusso di lavoro creata è disponibile come applicazione nella cartella Posta in arrivo. Gli utenti membri del gruppo flusso di lavoro-utenti possono compilare e inviare l’applicazione che attiva il flusso di lavoro associato. Per informazioni sull&#39;utilizzo della Casella in entrata AEM per inviare applicazioni e gestire attività, vedere [Gestione delle applicazioni e delle attività di Forms nella casella in entrata AEM](../../forms/using/manage-applications-inbox.md).

### Invio di un’applicazione dall’app AEM Forms {#afa}

L’app AEM Forms si sincronizza con un server AEM Forms e ti consente di modificare i dati del modulo, le attività, le applicazioni del flusso di lavoro e le informazioni salvate (bozze/modelli) nel tuo account. Per ulteriori informazioni, consulta [app AEM Forms](/help/forms/using/aem-forms-app.md) e articoli correlati.

### Invio di un modulo adattivo {#af}

È possibile configurare le azioni di invio di un modulo adattivo in modo da avviare un flusso di lavoro al momento dell’invio del modulo adattivo. I moduli adattivi forniscono **Richiama un flusso di lavoro AEM** azione di invio per avviare un flusso di lavoro al momento dell’invio di un modulo adattivo. Per informazioni dettagliate sull’azione di invio, consulta [Configurazione dell’azione Invia](../../forms/using/configuring-submit-actions.md). Per inviare un modulo adattivo tramite l’app AEM Forms, abilita Sincronizza con l’app AEM Forms nelle proprietà del modulo adattivo.

Puoi configurare un modulo adattivo per sincronizzare, inviare e attivare un flusso di lavoro dall’app AEM Forms. Per ulteriori informazioni, consulta [utilizzo di un modulo](/help/forms/using/working-with-form.md).

### Utilizzo di una cartella controllata {#watched}

Un amministratore (membro del gruppo fd-administrators) può configurare una cartella di rete per eseguire un flusso di lavoro preconfigurato quando un utente inserisce un file (ad esempio un file PDF) nella cartella. Al termine del flusso di lavoro, è possibile salvare il file dei risultati in una cartella di output specificata. Tale cartella è nota come [Cartella controllata](../../forms/using/watched-folder-in-aem-forms.md). Per configurare una cartella controllata per avviare un flusso di lavoro, effettua le seguenti operazioni:

1. Nell’istanza di authoring dell’AEM, vai a ![tools-1](assets/tools-1.png) > **[!UICONTROL Forms]** > **[!UICONTROL Configura cartella controllata]**. Viene visualizzato un elenco delle cartelle controllate già configurate.
1. Seleziona **[!UICONTROL Nuovo]**. Viene visualizzato un elenco di campi. Specifica un valore per i campi seguenti per configurare una cartella controllata per un flusso di lavoro:

<table>
 <tbody>
  <tr>
   <td>Campo</td>
   <td>Descrizione</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Nome</code></td>
   <td>Specifica il nome della cartella controllata. Questo campo supporta solo caratteri alfanumerici.</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Percorso</code></td>
   <td>Specifica il percorso fisico della cartella controllata. In un ambiente cluster utilizzare una cartella di rete condivisa accessibile dal nodo cluster AEM.</td>
  </tr>
  <tr>
   <td><span class="uicontrol">Elabora file tramite</code></td>
   <td>Seleziona la <span class="uicontrol">Flusso di lavoro </code>opzione. </td>
  </tr>
  <tr>
   <td><span class="uicontrol">Modello flusso di lavoro</code></td>
   <td>Seleziona un modello di flusso di lavoro.<br /> </td>
  </tr>
  <tr>
   <td><span class="uicontrol">Motivo file di output</code></td>
   <td>Specificare la struttura di directory per i file e le directory di output. È inoltre possibile specificare <a href="/help/forms/using/admin-help/configuring-watched-folder-endpoints.md" target="_blank">pattern per file e directory di output</a>.</td>
  </tr>
 </tbody>
</table>

1. Seleziona **Avanzate**. Specifica un valore per il campo seguente e tocca **Crea**. La cartella controllata è configurata per avviare un flusso di lavoro. Ora, ogni volta che un file viene inserito nella directory di input della cartella controllata, viene attivato il flusso di lavoro specificato.

   | Campo | Descrizione |
   |---|---|
   | Filtro servizio mappatura payload | Quando crei una cartella controllata, questa crea una struttura di cartelle nell’archivio crx. La struttura di cartelle può fungere da payload per il flusso di lavoro. Puoi scrivere uno script per mappare un flusso di lavoro AEM in modo da accettare gli input dalla struttura di cartelle controllata. È disponibile un’implementazione pronta all’uso, elencata nel filtro Payload Mapper. Se non disponi di un’implementazione personalizzata, seleziona l’implementazione predefinita. |

   La scheda Avanzate contiene altri campi. La maggior parte di questi campi contiene un valore predefinito. Per informazioni su tutti i campi, consulta [Creare o configurare una cartella controllata](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md) articolo.

### Invio di una comunicazione interattiva o di una lettera {#letter}

Puoi associare ed eseguire un flusso di lavoro incentrato su Forms su OSGi all’invio di una comunicazione interattiva o di una lettera. Nella gestione della corrispondenza i flussi di lavoro vengono utilizzati per la post-elaborazione di comunicazioni e lettere interattive. Ad esempio, l&#39;invio di e-mail, la stampa, il fax o l&#39;archiviazione di lettere finali. Per i passaggi dettagliati, consulta [Post-elaborazione di comunicazioni e lettere interattive](../../forms/using/submit-letter-topostprocess.md).

## Configurazioni aggiuntive {#additional-configurations}

### Configurare il servizio e-mail {#configure-email-service}

Puoi utilizzare i passaggi Assegna attività e Invia e-mail dei Flussi di lavoro AEM per inviare un’e-mail. Per specificare i server e-mail e le altre configurazioni necessarie per l’invio delle e-mail, effettua le seguenti operazioni:

1. Vai a Gestione configurazione AEM all’indirizzo `https://[server]:[port]/system/console/configMgr`.
1. Apri **[!UICONTROL Day CQ Mail Service]** configurazione. Specifica un valore per **[!UICONTROL Nome host del server SMTP]**, **[!UICONTROL porta del server SMTP,]** e **[!UICONTROL Indirizzo &quot;Da&quot;]** campi. Fai clic su **[!UICONTROL Salva]**.
1. Apri **[!UICONTROL Day CQ Link Externalizer]** configurazione. In **[!UICONTROL Domini]** , specificare il nome host/indirizzo IP effettivo e il numero di porta per le istanze locali, di authoring e di pubblicazione. Fai clic su **[!UICONTROL Salva]**.

### Rimuovi istanze flusso di lavoro {#purge-workflow-instances}

La riduzione al minimo del numero di istanze del flusso di lavoro aumenta le prestazioni del motore del flusso di lavoro, in modo da poter eliminare regolarmente dall’archivio le istanze del flusso di lavoro completate o in esecuzione. Per informazioni dettagliate, consulta [Rimozione regolare delle istanze del flusso di lavoro](/help/sites-administering/workflows-administering.md#regular) rimozione delle istanze del flusso di lavoro.

## Parametrizza i dati sensibili per le variabili del flusso di lavoro e memorizzali in archivi di dati esterni {#externalize-wf-variables}

Qualsiasi dato inviato da moduli adattivi a [!DNL Experience Manager] I flussi di lavoro possono contenere dati PII (personalmente identificabili) o SPD (Sensitive Personal Data, dati personali sensibili) degli utenti finali della tua azienda. Tuttavia, non è obbligatorio archiviare i dati in [!DNL Adobe Experience Manager] [Archivio JCR](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-jcr.html). È possibile esternalizzare l’archiviazione dei dati degli utenti finali nell’archiviazione dei dati gestita (ad esempio, l’archiviazione BLOB di Azure) parametrizzando le informazioni in [variabili del flusso di lavoro](/help/forms/using/variable-in-aem-workflows.md).

In un [!DNL Adobe Experience Manager] Flusso di lavoro di Forms, i dati vengono elaborati e trasmessi attraverso una serie di passaggi del flusso di lavoro tramite variabili di flusso di lavoro. Queste variabili sono proprietà denominate o coppie chiave-valore memorizzate nel nodo di metadati delle istanze del flusso di lavoro; ad esempio, `/var/workflow/instances/<serverid>/<datebucket>/<uniquenameof model>_<id>/data/metaData`. Queste variabili del flusso di lavoro possono essere esternalizzate in un archivio separato diverso da JCR e quindi elaborate da [!DNL Adobe Experience Manager] flussi di lavoro. [!DNL Adobe Experience Manager] fornisce API `[!UICONTROL UserMetaDataPersistenceProvider]` per memorizzare le variabili del flusso di lavoro nell’archiviazione esterna gestita. Per ulteriori informazioni sull’utilizzo delle variabili del flusso di lavoro per gli archivi dati di proprietà del cliente in [!DNL Adobe Experience Manager], vedi [Amministrare le variabili del flusso di lavoro per gli archivi dati esterni](/help/sites-administering/workflows-administering.md#using-workflow-variables-customer-datastore).
[!DNL Adobe] fornisce quanto segue [esempio](https://github.com/adobe/workflow-variable-externalizer) per memorizzare le variabili dalla mappa dei metadati del flusso di lavoro all’archiviazione BLOB di Azure, utilizzando l’API [UserMetaDataPersistenceProvider](https://github.com/adobe/workflow-variable-externalizer/blob/master/README.md). Su righe simili puoi utilizzare l’esempio come guida da utilizzare [UserMetaDataPersistenceProvider] API per esternalizzare le variabili del flusso di lavoro in qualsiasi altra archiviazione dati esterna a [!DNL Adobe Experience Manager] e gestirli allo stesso modo.

>[!NOTE]
>
>Quando memorizzi le variabili del flusso di lavoro in un’archiviazione dati esterna, fai riferimento ai puntatori nella [linee guida per i flussi di lavoro archiviazione dati esterna](#guidelines-workflows-external-data-storage).

### Installare l’implementazione dell’esempio API del flusso di lavoro

Per memorizzare le variabili del flusso di lavoro nell’archiviazione BLOB di Azure gestita:
1. Installare [esempio](https://github.com/adobe/workflow-variable-externalizer) API del flusso di lavoro [UserMetaDataPersistenceProvider](https://github.com/adobe/workflow-variable-externalizer/blob/master/README.md) come segue:

   1. Esegui nella directory principale del progetto il comando `mvn clean install` con Maven 3.

   1. Per distribuire il bundle e il pacchetto di contenuti all’autore, esegui `mvn clean install -PautoInstallPackage`.

   1. Per distribuire solo il bundle all’autore, esegui `mvn clean install -PautoInstallBundle`.

1. Inizializza le seguenti proprietà nel file di configurazione OSGi di Externalizer in `ui.config` pacchetto di contenuti:

   ```JQL
      accountKey=""
      accountName=""
      endpointSuffix=""
      containerName=""
      protocol=""
   ```

Di seguito sono riportati gli scopi (ed esempi) di queste proprietà:

* **accountKey** è la chiave segreta per autorizzare l’accesso.

* **accountName** è l’account di azure in cui devono essere memorizzati i dati.

* **endpointSuffix** ad esempio: `core.windows.net`.

* **containerName** è il contenitore nell’account in cui devono essere memorizzati i dati. L&#39;esempio presuppone che il contenitore sia esistente.

* **protocollo** ad esempio: `https` o `http`.

1. Configurare il modello di flusso di lavoro in [!DNL Adobe Experience Manager]. Per informazioni su come configurare il modello di flusso di lavoro per un archivio esterno, consulta [Configurare il modello di flusso di lavoro](#configure-aem-wf-model).

### Configurare il modello di flusso di lavoro in [!DNL Adobe Experience Manager] per l’archiviazione di dati esterni {#configure-aem-wf-model}

Per configurare un modello di flusso di lavoro AEM per un’archiviazione dati esterna:

1. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Flusso di lavoro]** > **[!UICONTROL Modelli]**.

1. Selezionate un nome di modello e selezionate **[!UICONTROL Modifica]**.

1. Seleziona l’icona Informazioni pagina e fai clic su **[!UICONTROL Apri proprietà]**.

1. Seleziona **[!UICONTROL Esternalizzare l’archiviazione dei dati del flusso di lavoro]**.

1. Seleziona **[!UICONTROL Salva e chiudi]** per salvare le proprietà.

### Linee guida per i flussi di lavoro AEM per l’archiviazione di dati esterni {#guidelines-workflows-external-data-storage}

Di seguito sono riportate le linee guida per l’utilizzo di [!DNL Adobe Experience Manager] flussi di lavoro e archiviazione dati in archivi dati esterni (ad esempio, server di archiviazione Microsoft Azure):

* Utilizza le variabili per memorizzare i dati durante la definizione dei file di dati di input e output e degli allegati nei passaggi del modello di flusso di lavoro. Non selezionare **[!UICONTROL Relativo al payload]** e **[!UICONTROL Disponibile in un percorso assoluto]** opzioni. Il **[!UICONTROL Relativo al payload]** e **[!UICONTROL Disponibile in un percorso assoluto]** le opzioni non vengono visualizzate automaticamente una volta [configurare un [!DNL Adobe Experience Manager] modello di flusso di lavoro per archiviazione dati esterna](#configure-aem-wf-model).

* Utilizza le variabili per memorizzare file di dati e allegati durante l’invio di un modulo adattivo a un flusso di lavoro AEM. Non selezionare **[!UICONTROL Relativo al payload]** durante l’invio di un modulo adattivo a un [!DNL Adobe Experience Manager] flusso di lavoro. Il **[!UICONTROL Relativo al payload]** non viene visualizzata automaticamente [configurare un [!DNL Adobe Experience Manager] modello di flusso di lavoro per archiviazione dati esterna](#configure-aem-wf-model).

* Non utilizzare un [!DNL Adobe Experience Manager] passaggio del flusso di lavoro in un modello di flusso di lavoro per memorizzare i dati in [!UICONTROL CRX DE] archivio.

* Quando [configurare un [!DNL Adobe Experience Manager] modello di flusso di lavoro per archiviazione dati esterna](#configure-aem-wf-model), non creare colonne personalizzate per [!DNL Adobe Experience Manager] [!UICONTROL Casella in entrata] poiché i valori delle colonne personalizzate non vengono recuperati se l’elemento di lavoro nella [!DNL Adobe Experience Manager] [!UICONTROL Casella in entrata] appartiene a un flusso di lavoro contrassegnato per l’archiviazione esterna.
