---
title: Creazione di modelli di flussi di lavoro
seo-title: Creazione di modelli di flussi di lavoro
description: Puoi creare un modello di flusso di lavoro per definire la serie di passaggi eseguiti quando un utente avvia il flusso di lavoro.
seo-description: Puoi creare un modello di flusso di lavoro per definire la serie di passaggi eseguiti quando un utente avvia il flusso di lavoro.
uuid: 31071d3a-d6d5-4476-9ac0-7b335de406d9
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: c097b60f-bcdf-45de-babe-b4c2e2b746a1
docset: aem65
exl-id: 6790202f-0542-4779-b3ce-d394cdba77b4
source-git-commit: 840ea373537799af995c3b8ce0c8bf575752775b
workflow-type: tm+mt
source-wordcount: '2485'
ht-degree: 2%

---

# Creazione di modelli di flussi di lavoro{#creating-workflow-models}

>[!CAUTION]
>
>Per l&#39;utilizzo dell&#39;interfaccia classica, consulta la [documentazione AEM 6.3](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/workflows-models.html) come riferimento.

Puoi creare un [modello di flusso di lavoro](/help/sites-developing/workflows.md#model) per definire la serie di passaggi eseguiti quando un utente avvia il flusso di lavoro. Puoi anche definire le proprietà del modello, ad esempio se il flusso di lavoro è transitorio o se utilizza più risorse.

Quando un utente avvia un flusso di lavoro, viene avviata un’istanza; si tratta del modello runtime corrispondente, creato quando [Sincronizza](#sync-your-workflow-generate-a-runtime-model) le modifiche.

## Creazione di un nuovo flusso di lavoro {#creating-a-new-workflow}

Quando crei un nuovo modello di flusso di lavoro, questo contiene:

* I passaggi, **Inizio flusso** e **Fine flusso**.
che rappresentano l’inizio e la fine del flusso di lavoro. Questi passaggi sono obbligatori e non possono essere modificati/rimossi.
* Un passaggio di esempio **Participant** denominato **Step 1**.
Questo passaggio è configurato per assegnare un elemento di lavoro all’iniziatore del flusso di lavoro. Modifica o elimina questo passaggio e aggiungi i passaggi necessari.

Per creare un nuovo flusso di lavoro con l’editor:

1. Apri la console **Modelli di flusso di lavoro** ; tramite **Strumenti**, **Flusso di lavoro**, **Modelli** o, ad esempio: [https://localhost:4502/aem/workflow](https://localhost:4502/aem/workflow)
1. Seleziona **Crea**, quindi **Crea modello**.
1. Viene visualizzata la finestra di dialogo **Aggiungi modello flusso di lavoro** . Immetti i valori **Titolo** e **Nome** (facoltativo) prima di selezionare **Fine**.
1. Il nuovo modello è elencato nella console **Modelli di flusso di lavoro** .
1. Seleziona il nuovo flusso di lavoro, quindi utilizza [**Modifica** per aprirlo per la configurazione](#editinganexistingworkflow):
   ![wf-01](assets/wf-01.png)

>[!NOTE]
>
>Se crei modelli a livello di programmazione (utilizzando un pacchetto crx) puoi anche creare una sottocartella in:
>
>`/var/workflow/models`
>
>Esempio, `/var/workflow/models/prototypes`
>
>Questa cartella può quindi essere utilizzata per [gestire l&#39;accesso ai modelli in quella cartella](/help/sites-administering/workflows-managing.md#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that).

## Modifica di un flusso di lavoro {#editing-a-workflow}

Puoi modificare qualsiasi modello di flusso di lavoro esistente in modo da:

* [definire ](#addingasteptoamodel-) i passaggi e  [i relativi parametri](#configuring-a-workflow-step)
* configura le proprietà del flusso di lavoro, tra cui [stage](#configuring-workflow-stages-that-show-workflow-progress), [se il flusso di lavoro è transitorio](#creatingatransientworkflow-) e/o [utilizza più risorse](#configuring-a-workflow-for-multi-resource-support)

La modifica di un flusso di lavoro [**Predefinito e/o Legacy** (preconfigurato)](#editing-a-default-or-legacy-workflow-for-the-first-time) ha un passaggio aggiuntivo, per garantire che venga effettuata una [copia sicura](/help/sites-developing/workflows-best-practices.md#locations-workflow-models) prima di apportare le modifiche.

Al termine degli aggiornamenti del flusso di lavoro, è necessario utilizzare **Sincronizza** per **Generare un modello runtime**. Per ulteriori informazioni, consulta [Sincronizza il flusso di lavoro](#sync-your-workflow-generate-a-runtime-model) .

### Sincronizza il flusso di lavoro - Genera un modello runtime {#sync-your-workflow-generate-a-runtime-model}

**La sincronizzazione**  (a destra nella barra degli strumenti dell’editor) genera un modello  [runtime](/help/sites-developing/workflows.md#runtime-model). Il modello di runtime è il modello effettivamente utilizzato quando un utente avvia un flusso di lavoro. Se non **Sincronizza** le modifiche, queste non saranno disponibili in fase di esecuzione.

Quando apporti modifiche al flusso di lavoro (o a qualsiasi altro utente) devi utilizzare **Sincronizza** per generare un modello di runtime, anche quando le singole finestre di dialogo (ad esempio, per i passaggi) dispongono di opzioni di salvataggio personalizzate.

Quando le modifiche vengono sincronizzate con il modello di runtime (salvato), viene visualizzato **Sincronizzato**.

Alcuni passaggi dispongono di campi obbligatori e/o di una convalida integrata. Quando queste condizioni non vengono soddisfatte, viene visualizzato un errore quando si tenta di **Sincronizzare** il modello. Ad esempio, quando non è stato definito alcun partecipante per un passaggio **Partecipante**:

![wf-21](assets/wf-21.png)

### Modifica di un flusso di lavoro predefinito o legacy per la prima volta {#editing-a-default-or-legacy-workflow-for-the-first-time}

Quando si apre un modello [Predefinito e/o Legacy](/help/sites-developing/workflows.md#workflow-types) per la modifica:

* Il browser Passaggi non è disponibile (lato sinistro).
* È disponibile un’azione **Modifica** nella barra degli strumenti (a destra).
* Inizialmente il modello e le sue proprietà vengono presentate in modalità di sola lettura come segue:
   * I flussi di lavoro predefiniti si trovano in `/libs`
   * I flussi di lavoro legacy si trovano in `/etc`
Selezione 
**** Modifica:
* prendere una copia del flusso di lavoro in `/conf`
* rendere disponibile il browser Passaggi
* consente di apportare modifiche

>[!NOTE]
>
>Per ulteriori informazioni, consulta [Posizioni dei modelli di flussi di lavoro](/help/sites-developing/workflows-best-practices.md#locations-workflow-models) .

![wf-22](assets/wf-22.png)

### Aggiunta di un passaggio a un modello {#adding-a-step-to-a-model}

Sarà necessario aggiungere passaggi al modello per rappresentare l’attività da eseguire. Ogni passaggio esegue un’attività specifica. Una selezione di componenti passo è disponibile in un’istanza AEM standard.

Quando modifichi un modello, i passaggi disponibili vengono visualizzati nei vari gruppi del **browser Passaggi**. Esempio:

![wf-10](assets/wf-10.png)

>[!NOTE]
>
>Per informazioni sui componenti del passaggio principale installati con AEM, consulta [Riferimento passaggi flusso di lavoro](/help/sites-developing/workflows-step-ref.md).

Per aggiungere passaggi al modello di flusso di lavoro:

1. Apri un modello di flusso di lavoro esistente da modificare. Dalla console **Modello flussi di lavoro**, seleziona il modello richiesto, quindi **Modifica**.
1. Apri il browser Passaggi; utilizzando **Attiva/disattiva pannello laterale**, all&#39;estrema sinistra della barra degli strumenti superiore. È possibile:

   * **** Filtrare per passaggi specifici.
   * Utilizza il selettore a discesa per limitare la selezione a un gruppo specifico di passaggi.
   * Seleziona l&#39;icona Mostra descrizione ![wf-stepinfo-icon](assets/wf-stepinfo-icon.png) per visualizzare ulteriori dettagli sul passaggio appropriato.

   ![wf-02](assets/wf-02.png)

1. Trascina i passaggi appropriati nella posizione desiderata nel modello.

   Ad esempio, un **Passaggio partecipante**.

   Una volta aggiunto al flusso, puoi [configurare il passaggio](#configuring-a-workflow-step).

   ![wf-03](assets/wf-03.png)

1. Aggiungi tutti i passaggi necessari o altri aggiornamenti.

   In fase di esecuzione, i passaggi vengono eseguiti nell’ordine in cui compaiono nel modello. Dopo aver aggiunto i componenti passo, potete trascinarli in una posizione diversa nel modello.

   È inoltre possibile copiare, tagliare, incollare, raggruppare o eliminare i passaggi esistenti; come con l&#39; [editor di pagine.](/help/sites-authoring/editing-content.md)

   È inoltre possibile comprimere/espandere i passaggi suddivisi utilizzando l’opzione della barra degli strumenti: ![wf-comprimseexpand-toolbar-icon](assets/wf-collapseexpand-toolbar-icon.png)

1. Conferma le modifiche con **Sincronizza** (barra degli strumenti dell&#39;editor) per generare il modello di runtime.

   Per ulteriori informazioni, consulta [Sincronizza il flusso di lavoro](#sync-your-workflow-generate-a-runtime-model) .

### Configurazione di un passaggio del flusso di lavoro {#configuring-a-workflow-step}

È possibile **configurare** e personalizzare il comportamento di un passaggio del flusso di lavoro utilizzando le finestre di dialogo **Proprietà passaggio**.

1. Per aprire la finestra di dialogo **Proprietà passaggio** per un passaggio:

   * Tocca o fai clic sul passaggio* nel modello di flusso di lavoro e seleziona **Configura** dalla barra degli strumenti del componente.

   * Fare doppio clic sul passaggio.
   >[!NOTE]
   >
   >Per informazioni sui componenti del passaggio principale installati con AEM, consulta [Riferimento passaggi flusso di lavoro](/help/sites-developing/workflows-step-ref.md).

1. Configura le **Proprietà passaggio** come richiesto; le proprietà disponibili dipendono dal tipo di passaggio, possono essere disponibili anche diverse schede. Ad esempio, il **Passaggio partecipante** predefinito, presente in un nuovo flusso di lavoro come `Step 1`:

   ![wf-11](assets/wf-11.png)

1. Conferma gli aggiornamenti con il segno di spunta.
1. Conferma le modifiche con **Sincronizza** (barra degli strumenti dell&#39;editor) per generare il modello di runtime.

   Per ulteriori informazioni, consulta [Sincronizza il flusso di lavoro](#sync-your-workflow-generate-a-runtime-model) .

### Creazione di un flusso di lavoro transitorio {#creating-a-transient-workflow}

Puoi creare un modello di flusso di lavoro [Transitent](/help/sites-developing/workflows.md#transient-workflows) quando crei un nuovo modello o modificane uno esistente:

1. Apri il modello di flusso di lavoro per [modificare](#editinganexistingworkflow).
1. Seleziona **Proprietà modello flusso di lavoro** dalla barra degli strumenti.
1. Nella finestra di dialogo attiva **Flusso di lavoro transitorio** (o disattiva se necessario):

   ![wf-07](assets/wf-07.png)

1. Conferma la modifica con **Salva e chiudi**; seguita da **Sincronizza** (barra degli strumenti dell&#39;editor) per generare il modello di runtime.

   Per ulteriori informazioni, consulta [Sincronizza il flusso di lavoro](#sync-your-workflow-generate-a-runtime-model) .

>[!NOTE]
>
>Quando esegui un flusso di lavoro in modalità [transient](/help/sites-developing/workflows.md#transient-workflows) AEM non memorizza alcuna cronologia del flusso di lavoro. Pertanto, [Timeline](/help/sites-authoring/basic-handling.md#timeline) non visualizza alcuna informazione relativa a tale flusso di lavoro.

## Rendere disponibili i modelli di flusso di lavoro nell’interfaccia utente touch {#classic2touchui}

Se un modello di flusso di lavoro è presente nell&#39;interfaccia classica, ma manca nel menu a comparsa di selezione nella barra **[!UICONTROL Timeline]** dell&#39;interfaccia utente touch, segui la configurazione per renderlo disponibile. I passaggi seguenti illustrano l&#39;utilizzo del modello di flusso di lavoro denominato **[!UICONTROL Richiesta di attivazione]**.

1. Verifica che il modello non sia disponibile nell’interfaccia utente touch. Accedi a una risorsa utilizzando il percorso `/assets.html/content/dam` . Seleziona una risorsa. Apri **[!UICONTROL Timeline]** nella barra a sinistra. Fare clic su **[!UICONTROL Avvia flusso di lavoro]** e confermare che il modello **[!UICONTROL Richiedi attivazione]** non è presente nell&#39;elenco a comparsa.

1. Passa a **[!UICONTROL Strumenti > Generale > Assegnazione tag]**. Seleziona **[!UICONTROL Flusso di lavoro]**.

1. Seleziona **[!UICONTROL Crea > Crea tag]**. Imposta **[!UICONTROL Titolo]** come `DAM` e **[!UICONTROL Nome]** come `dam`. Seleziona **[!UICONTROL Invia]**.
   ![Crea tag nel modello di flusso di lavoro](assets/workflow_create_tag.png)

1. Passa a **[!UICONTROL Strumenti > Flusso di lavoro > Modelli]**. Seleziona **[!UICONTROL Richiesta di attivazione]**, quindi seleziona **[!UICONTROL Modifica]**.

1. Seleziona **[!UICONTROL Modifica]**, apri il menu **[!UICONTROL Informazioni pagina]** e da lì seleziona **[!UICONTROL Apri proprietà]** e vai alla scheda **[!UICONTROL Base]** (se non è già aperta).

1. Aggiungi `Workflow : DAM` al campo **[!UICONTROL Tag]** . Conferma la selezione con il segno di spunta (segno di spunta).

1. Conferma l’aggiunta del tag con **[!UICONTROL Salva e chiudi]**.
   ![Modifica proprietà pagina del modello](assets/workflow_model_edit_activation1.png)

1. Completa il processo con **[!UICONTROL Sincronizza]**. Il flusso di lavoro è ora disponibile nell’interfaccia touch.

### Configurazione di un flusso di lavoro per il supporto di più risorse {#configuring-a-workflow-for-multi-resource-support}

Puoi configurare un modello di flusso di lavoro per [Supporto risorse multiple](/help/sites-developing/workflows.md#multi-resource-support) durante la creazione di un nuovo modello o modificandone uno esistente:

1. Apri il modello di flusso di lavoro per [modificare](#editinganexistingworkflow).
1. Seleziona **Proprietà modello flusso di lavoro** dalla barra degli strumenti.

1. Nella finestra di dialogo attiva **Supporto risorse multiple** (o disattiva se necessario):

   ![wf-08](assets/wf-08.png)

1. Conferma la modifica con **Salva e chiudi**; seguita da **Sincronizza** (barra degli strumenti dell&#39;editor) per generare il modello di runtime.

   Per ulteriori informazioni, consulta [Sincronizza il flusso di lavoro](#sync-your-workflow-generate-a-runtime-model) .

### Configurazione delle fasi del flusso di lavoro (che mostrano l’avanzamento del flusso di lavoro) {#configuring-workflow-stages-that-show-workflow-progress}

[Le ](/help/sites-developing/workflows.md#workflow-stages) fasi del flusso di lavoro consentono di visualizzare l’avanzamento di un flusso di lavoro durante la gestione delle attività.

>[!CAUTION]
>
>Se le fasi del flusso di lavoro sono definite in **Proprietà pagina** ma non vengono utilizzate per nessuno dei passaggi del flusso di lavoro, la barra di avanzamento non mostrerà alcun avanzamento (indipendentemente dal passaggio del flusso di lavoro corrente).

Le fasi da rendere disponibili sono definite nei modelli di flusso di lavoro; i modelli di flusso di lavoro esistenti possono essere aggiornati per includere le definizioni degli stadi. Puoi definire un numero qualsiasi di fasi per il modello di flusso di lavoro.

Per definire **Stadi** per il flusso di lavoro:

1. Apri il modello di flusso di lavoro per la modifica.
1. Seleziona **Proprietà modello flusso di lavoro** dalla barra degli strumenti. Quindi apri la scheda **Stadi** .
1. Aggiungi (e posiziona) i **Stadi** richiesti. Puoi definire un numero qualsiasi di fasi per il modello di flusso di lavoro.

   Esempio:

   ![wf-08-1](assets/wf-08-1.png)

1. Fai clic su **Salva e chiudi** per salvare le proprietà.
1. Assegna un passaggio a ciascuno dei passaggi del modello di flusso di lavoro. Esempio:

   ![wf-09](assets/wf-09.png)

   Un passaggio può essere assegnato a più passaggi. Esempio:

   | **Incremento** | **Stadio** |
   |---|---|
   | Passaggio 1 | Crea |
   | Passaggio 2 | Crea |
   | Passaggio 3 | Recensione |
   | Passaggio 4 | Approva |
   | Passaggio 5 | Approva |
   | Passaggio 6 | Completa |

1. Conferma le modifiche con **Sincronizza** (barra degli strumenti dell&#39;editor) per generare il modello di runtime.

   Per ulteriori informazioni, consulta [Sincronizza il flusso di lavoro](#sync-your-workflow-generate-a-runtime-model) .

## Esportazione di un modello di flusso di lavoro in un pacchetto {#exporting-a-workflow-model-in-a-package}

Per esportare un modello di flusso di lavoro in un pacchetto:

1. Crea un nuovo pacchetto utilizzando [Gestione pacchetti](/help/sites-administering/package-manager.md#package-manager):

   1. Passa a Gestione pacchetti tramite **Strumenti**, **Implementazione**, **Pacchetti**.

   1. Fai clic su **Crea pacchetto**.
   1. Specifica il **Nome pacchetto** e tutti gli altri dettagli richiesti.
   1. Fai clic su **OK**.

1. Fai clic su **Modifica** sulla barra degli strumenti del nuovo pacchetto.

1. Apri la scheda **Filtri** .

1. Seleziona **Aggiungi filtro** e specifica il percorso del modello di flusso di lavoro *progettazione*:

   `/conf/global/settings/workflow/models/<*your-model-name*>`

   Fare clic su **Fine**.

1. Seleziona **Aggiungi filtro** e specifica il percorso del modello di flusso di lavoro *runtime*:

   `/var/workflow/models/<*your-model-name*>`

   Fare clic su **Fine**.

1. Aggiungi altri filtri per gli script personalizzati utilizzati dal modello.
1. Fai clic su **Salva** per confermare le definizioni dei filtri.
1. Seleziona **Build** dalla barra degli strumenti della definizione del pacchetto.
1. Seleziona **Scarica** dalla barra degli strumenti del pacchetto.

## Utilizzo dei flussi di lavoro per elaborare gli invii di moduli {#using-workflows-to-process-form-submissions}

È possibile configurare un modulo da elaborare dal flusso di lavoro selezionato. Quando gli utenti inviano il modulo, viene creata una nuova istanza di flusso di lavoro con i dati dell’invio del modulo come payload.

Per configurare il flusso di lavoro da utilizzare con il modulo:

1. Crea una nuova pagina e aprila per la modifica.
1. Aggiungete un componente **Modulo** alla pagina.
1. **** Configura il componente  **Modulo** iniziale visualizzato nella pagina.
1. Utilizza **Avvia flusso di lavoro** per selezionare il flusso di lavoro desiderato tra quelli disponibili:

   ![wf-12](assets/wf-12.png)

1. Confermare la nuova configurazione del modulo con un segno di spunta.

## Verifica dei flussi di lavoro {#testing-workflows}

È buona prassi testare un flusso di lavoro per utilizzare diversi tipi di payload; compresi i tipi diversi da quello per il quale è stato sviluppato. Ad esempio, se vuoi che il flusso di lavoro gestisca le risorse, testalo impostando una pagina come payload e accertati che non generi errori.

Ad esempio, verifica il nuovo flusso di lavoro come segue:

1. [Avvia il ](/help/sites-administering/workflows-starting.md) modello di flusso di lavoro dalla console.
1. Definisci il **Payload** e conferma.

1. Esegui le azioni necessarie affinché il flusso di lavoro proceda.
1. Monitora i file di registro mentre il flusso di lavoro è in esecuzione.

È inoltre possibile configurare AEM per visualizzare i messaggi **DEBUG** nei file di registro. Per ulteriori informazioni, consulta [Logging](/help/sites-deploying/configure-logging.md) e al termine dello sviluppo, reimposta il **Livello di log** su **Info**.

## Esempi {#examples}

### Esempio: Creazione di un flusso di lavoro (semplice) per accettare o rifiutare una richiesta di pubblicazione {#example-creating-a-simple-workflow-to-accept-or-reject-a-request-for-publication}

Per illustrare alcune delle possibilità di creazione di un flusso di lavoro, nell’esempio seguente viene creata una variante del flusso di lavoro `Publish Example` .

1. [Crea un nuovo modello](#creating-a-new-workflow) di flusso di lavoro.

   Il nuovo flusso di lavoro conterrà:

   * **Avvio del flusso**
   * `Step 1`
   * **Fine del flusso**

1. Elimina `Step 1` (in quanto si tratta del tipo di passaggio errato per questo esempio):

   * Fai clic sul passaggio e seleziona **Elimina** dalla barra degli strumenti del componente. Conferma l’azione.

1. Dalla selezione **Flusso di lavoro** del browser dei passaggi, trascina un **Passaggio partecipante** nel flusso di lavoro e posizionalo tra **Inizio flusso** e **Fine flusso**.
1. Per aprire la finestra di dialogo delle proprietà:

   * Fai clic sul passaggio del partecipante e seleziona **Configura** dalla barra degli strumenti del componente.
   * Fare doppio clic sul passaggio del partecipante.

1. Nella scheda **Comune** immetti `Validate Content` sia per **Titolo** che per **Descrizione**.
1. Apri la scheda **Utente/gruppo** :

   * Attiva **Notifica all&#39;utente tramite e-mail**.
   * Selezionare `Administrator` ( `admin`) per il campo **Utente/Gruppo**.

   >[!NOTE]
   >
   >Per inviare e-mail, [è necessario configurare i dettagli del servizio e dell&#39;account utente ](/help/sites-administering/notification.md).

1. Conferma gli aggiornamenti con il segno di spunta.

   Verrai riportato alla panoramica del modello di flusso di lavoro, in cui il passaggio del partecipante sarà stato rinominato in `Validate Content`.

1. Trascina un elemento **O Split** nel flusso di lavoro e posizionalo tra `Validate Content` e **Fine flusso**.
1. Apri **O Split** per la configurazione.
1. Configurazione:

   * **Comune**: specificare il nome della divisione.
   * **Filiale 1**: selezionare  **Percorso predefinito**.

   * **Filiale 2**: assicurarsi che  **i** router predefiniti non siano selezionati.

1. Conferma gli aggiornamenti di **OR Split**.
1. Trascina un **Passaggio partecipante** nel ramo a sinistra, apri le proprietà, specifica i seguenti valori, quindi conferma le modifiche:

   * **Titolo**: `Reject Publish Request`

   * **Utente/gruppo**: ad esempio,  `projects-administrators`

   * **Invia una notifica all’utente via e-mail**: Attiva per ricevere notifiche dall’utente tramite e-mail.

1. Trascina un **Passaggio processo** nel ramo di destra, apri le proprietà, specifica i seguenti valori, quindi conferma le modifiche:

   * **Titolo**: `Publish Page as Requested`

   * **Processo**: seleziona  `Activate Page`. Questa procedura pubblica la pagina selezionata alle istanze dell’editore.

1. Fai clic su **Sincronizza** (barra degli strumenti dell&#39;editor) per generare il modello di runtime.

   Per ulteriori informazioni, consulta [Sincronizza il flusso di lavoro](#sync-your-workflow-generate-a-runtime-model) .

   Il nuovo modello di flusso di lavoro sarà simile al seguente:

   ![wf-13](assets/wf-13.png)

1. Applica questo flusso di lavoro alla pagina in modo che quando l&#39;utente passa al passaggio **Completa** **Convalida contenuto**, possa selezionare se desidera **Pubblicare pagina come richiesto** o **Rifiuta richiesta di pubblicazione**.

   ![chlimage_1-72](assets/chlimage_1-72.png)

### Esempio: Definizione di una regola per una divisione OR utilizzando lo script ECMA {#defineruleecmascript}

**I passaggi** iniziali o parziali consentono di introdurre nel flusso di lavoro i percorsi di elaborazione condizionale.

Per definire una regola OR, procedere come segue:

1. Creare due script e salvarli nell&#39;archivio, ad esempio in:

   `/apps/myapp/workflow/scripts`

   >[!NOTE]
   >
   >Gli script devono avere una funzione [`check()`](#function-check) che restituisce un valore booleano.

1. Modifica il flusso di lavoro e aggiungi **OR Split** al modello.
1. Modifica le proprietà di **Ramo 1** di **O Dividi**:

   * Definiscilo come **Percorso predefinito** impostando il valore **Valore** su `true`.

   * Come **Regola**, imposta il percorso dello script. Esempio:
      `/apps/myapp/workflow/scripts/myscript1.ecma`
   >[!NOTE]
   >
   >Se necessario, puoi cambiare l’ordine del ramo.

1. Modifica le proprietà della **Ramo 2** del **O Dividi**.

   * Come **Regola**, imposta il percorso dell&#39;altro script. Esempio:
      `/apps/myapp/workflow/scripts/myscript2.ecma`

1. Imposta le proprietà dei singoli passaggi in ciascun ramo. Assicurati che il valore **Utente/Gruppo** sia impostato.
1. Fai clic su **Sincronizza** (barra degli strumenti dell&#39;editor) per mantenere le modifiche al modello di runtime.

   Per ulteriori informazioni, consulta [Sincronizza il flusso di lavoro](#sync-your-workflow-generate-a-runtime-model) .

#### Funzione Check() {#function-check}

>[!NOTE]
>
>Vedere [Uso di ECMAScript](/help/sites-developing/workflows-customizing-extending.md#using-ecmascript).

Il seguente script di esempio restituisce `true` se il nodo è un `JCR_PATH` situato sotto `/content/we-retail/us/en`:

```
function check() {
    if (workflowData.getPayloadType() == "JCR_PATH") {
      var path = workflowData.getPayload().toString();
      var node = jcrSession.getItem(path);

      if (node.getPath().indexOf("/content/we-retail/us/en") >= 0) {
       return true;
      } else {
       return false;
      }
     } else {
      return false;
     }
}
```

### Esempio: Richiesta di attivazione personalizzata {#example-customized-request-for-activation}

Puoi personalizzare uno qualsiasi dei flussi di lavoro predefiniti. Per ottenere un comportamento personalizzato sovrapponi i dettagli del flusso di lavoro appropriato.

Ad esempio, **Richiesta di attivazione**. Questo flusso di lavoro viene utilizzato per la pubblicazione di pagine all’interno di **Sites** e viene attivato automaticamente quando un autore di contenuti non dispone dei diritti di replica appropriati. Per ulteriori informazioni, consulta [Personalizzazione dell’authoring delle pagine - Personalizzazione della richiesta di attivazione del flusso di lavoro](/help/sites-developing/customizing-page-authoring-touch.md#customizing-the-request-for-activation-workflow) .
