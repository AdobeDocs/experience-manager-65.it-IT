---
title: Creazione di modelli di flussi di lavoro
description: Puoi creare un modello di flusso di lavoro per definire la serie di passaggi che vengono eseguiti quando un utente avvia il flusso di lavoro.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
docset: aem65
exl-id: 6790202f-0542-4779-b3ce-d394cdba77b4
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2451'
ht-degree: 2%

---

# Creazione di modelli di flussi di lavoro{#creating-workflow-models}

>[!CAUTION]
>
>Per utilizzare l’interfaccia classica, consulta [Documentazione di AEM 6.3](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/workflows-models.html) per riferimento.

Si crea un [modello di flusso di lavoro](/help/sites-developing/workflows.md#model) per definire la serie di passaggi eseguiti all’avvio del flusso di lavoro da parte di un utente. Puoi anche definire le proprietà del modello, ad esempio se il flusso di lavoro è transitorio o utilizza più risorse.

Quando un utente avvia un flusso di lavoro, viene avviata un’istanza; si tratta del modello di runtime corrispondente, creato quando [Sincronizza](#sync-your-workflow-generate-a-runtime-model) le tue modifiche.

## Creazione di un nuovo flusso di lavoro {#creating-a-new-workflow}

La prima volta che crei un modello di flusso di lavoro, contiene:

* I passaggi, **Inizio flusso** e **Fine flusso**.
Questi rappresentano l’inizio e la fine del flusso di lavoro. Questi passaggi sono necessari e non possono essere modificati/rimossi.
* Un esempio **Partecipante** passaggio denominato **Passaggio 1**.
Questo passaggio è configurato per assegnare un elemento di lavoro all&#39;iniziatore del flusso di lavoro. Modifica o elimina questo passaggio e aggiungi i passaggi richiesti.

Per creare un flusso di lavoro con l’editor:

1. Apri **Modelli flusso di lavoro** console; tramite **Strumenti**, **Flusso di lavoro**, **Modelli** o, ad esempio: [https://localhost:4502/aem/workflow](https://localhost:4502/aem/workflow)
1. Seleziona **Crea**, quindi **Crea modello**.
1. Il **Aggiungi modello flusso di lavoro** viene visualizzata. Inserisci il **Titolo** e **Nome** (facoltativo) prima di selezionare **Fine**.
1. Il nuovo modello è elencato nel **Modelli flusso di lavoro** console.
1. Seleziona il nuovo flusso di lavoro, quindi utilizza [**Modifica** per aprirlo per la configurazione](#editinganexistingworkflow):
   ![wf-01](assets/wf-01.png)

>[!NOTE]
>
>Se crei modelli a livello di programmazione (utilizzando un pacchetto crx), puoi anche creare una sottocartella all’interno di:
>
>`/var/workflow/models`
>
>Ad esempio `/var/workflow/models/prototypes`
>
>Questa cartella può quindi essere utilizzata per [gestione dell’accesso ai modelli in tale cartella](/help/sites-administering/workflows-managing.md#create-a-subfolder-in-var-workflow-models-and-apply-the-acl-to-that).

## Modifica di un flusso di lavoro {#editing-a-workflow}

Puoi modificare qualsiasi modello di flusso di lavoro esistente in:

* [definire i passaggi](#addingasteptoamodel-) e i loro [parametri](#configuring-a-workflow-step)
* configurare le proprietà del flusso di lavoro, tra cui [stadi](#configuring-workflow-stages-that-show-workflow-progress), [se il flusso di lavoro è transitorio](#creatingatransientworkflow-) e/o [utilizza più risorse](#configuring-a-workflow-for-multi-resource-support)

Modifica di un [**Predefinito e/o legacy** flusso di lavoro (preconfigurato)](#editing-a-default-or-legacy-workflow-for-the-first-time) dispone di un passaggio aggiuntivo per garantire che [copia sicura](/help/sites-developing/workflows-best-practices.md#locations-workflow-models) viene eseguita prima delle modifiche.

Una volta completati gli aggiornamenti del flusso di lavoro, devi utilizzare **Sincronizza** a **Generare un modello runtime**. Consulta [Sincronizza il flusso di lavoro](#sync-your-workflow-generate-a-runtime-model) per i dettagli.

### Sincronizzare il flusso di lavoro - Generare un modello di runtime {#sync-your-workflow-generate-a-runtime-model}

**Sincronizza** (nella barra degli strumenti dell’editor) genera un [modello runtime](/help/sites-developing/workflows.md#runtime-model). Il modello di runtime è il modello effettivamente utilizzato quando un utente avvia un flusso di lavoro. In caso contrario **Sincronizza** le modifiche, quindi non saranno disponibili in fase di runtime.

Quando apporti modifiche al flusso di lavoro (o a qualsiasi altro utente) devi utilizzare **Sincronizza** per generare un modello di runtime, anche quando le singole finestre di dialogo (ad esempio, per i passaggi) dispongono di opzioni di salvataggio proprie.

Quando le modifiche vengono sincronizzate con il modello di runtime (salvato), **Sincronizzato** viene invece visualizzato.

Alcuni passaggi dispongono di campi obbligatori e/o di una convalida incorporata. Quando queste condizioni non vengono soddisfatte, viene visualizzato un errore quando si tenta di **Sincronizza** il modello. Ad esempio, se non è stato definito alcun partecipante per un **Partecipante** passaggio:

![wf-21](assets/wf-21.png)

### Modifica di un flusso di lavoro predefinito o legacy per la prima volta {#editing-a-default-or-legacy-workflow-for-the-first-time}

All&#39;apertura di un [Modello predefinito e/o legacy](/help/sites-developing/workflows.md#workflow-types) per la modifica:

* Il browser Passaggi non è disponibile (lato sinistro).
* È presente un **Modifica** nella barra degli strumenti (a destra).
* Inizialmente il modello e le relative proprietà vengono presentati in modalità di sola lettura come:
   * I flussi di lavoro predefiniti sono in `/libs`
   * I flussi di lavoro legacy sono in `/etc`
Selezione **Modifica** consente di:
* copia del flusso di lavoro in `/conf`
* rendere disponibile il browser Passaggi
* consente di apportare modifiche

>[!NOTE]
>
>Consulta [Posizioni dei modelli di workflow](/help/sites-developing/workflows-best-practices.md#locations-workflow-models) per ulteriori informazioni.

![wf-22](assets/wf-22.png)

### Aggiunta di un passaggio a un modello {#adding-a-step-to-a-model}

Devi aggiungere dei passaggi al modello per rappresentare l&#39;attività da eseguire: ogni passaggio esegue un&#39;attività specifica. Una selezione di componenti step è disponibile in un’istanza AEM standard.

Quando modificate un modello, i passi disponibili vengono visualizzati nei vari gruppi della **Browser Passaggi**. Ad esempio:

![wf-10](assets/wf-10.png)

>[!NOTE]
>
>Per informazioni sui componenti della fase principale installati con AEM, consulta [Riferimento passaggi flusso di lavoro](/help/sites-developing/workflows-step-ref.md).

Per aggiungere passaggi al modello di flusso di lavoro:

1. Apri un modello di flusso di lavoro esistente per la modifica. Dalla sezione **Modello flussi di lavoro** , seleziona il modello richiesto, quindi **Modifica**.
1. Apri il browser Passaggi; utilizzando **Attiva/Disattiva pannello laterale**, all’estrema sinistra della barra degli strumenti superiore. È possibile:

   * **Filtro** per passaggi specifici.
   * Utilizza il selettore a discesa per limitare la selezione a un gruppo specifico di passaggi.
   * Seleziona l’icona Mostra descrizione ![wf-stepinfo-icon](assets/wf-stepinfo-icon.png) per visualizzare ulteriori dettagli sul passaggio appropriato.

   ![wf-02](assets/wf-02.png)

1. Trascinate i passi appropriati nella posizione desiderata nel modello.

   Ad esempio, un **Passaggio partecipante**.

   Una volta aggiunto al flusso è possibile: [configurare il passaggio](#configuring-a-workflow-step).

   ![wf-03](assets/wf-03.png)

1. Aggiungi tutti i passaggi, o altri aggiornamenti, necessari.

   In fase di esecuzione, i passi vengono eseguiti nell&#39;ordine in cui vengono visualizzati nel modello. Dopo aver aggiunto i componenti del passo, potete trascinarli in una posizione diversa nel modello.

   È inoltre possibile copiare, tagliare, incollare, raggruppare o eliminare passaggi esistenti, come con [Editor pagina.](/help/sites-authoring/editing-content.md)

   I passaggi di suddivisione possono anche essere compressi o espansi utilizzando l’opzione della barra degli strumenti: ![wf-collapseexpand-toolbar-icon](assets/wf-collapseexpand-toolbar-icon.png)

1. Conferma le modifiche con **Sincronizza** (barra degli strumenti dell’editor) per generare il modello runtime.

   Consulta [Sincronizza il flusso di lavoro](#sync-your-workflow-generate-a-runtime-model) per i dettagli.

### Configurazione di un passaggio del flusso di lavoro {#configuring-a-workflow-step}

È possibile **Configura** e personalizzare il comportamento di un passaggio del flusso di lavoro utilizzando **Proprietà passaggio** .

1. Per aprire **Proprietà passaggio** per un passaggio:

   * Tocca o fai clic sul passaggio* *nel modello di flusso di lavoro e seleziona **Configura** dalla barra degli strumenti del componente.

   * Fare doppio clic sul passaggio.

   >[!NOTE]
   >
   >Per informazioni sui componenti della fase principale installati con AEM, consulta [Riferimento passaggi flusso di lavoro](/help/sites-developing/workflows-step-ref.md).

1. Configurare **Proprietà passaggio** se necessario; le proprietà disponibili dipendono dal tipo di passaggio, potrebbero anche essere disponibili diverse schede. Ad esempio, il valore predefinito **Passaggio partecipante**, presente in un nuovo flusso di lavoro come `Step 1`:

   ![wf-11](assets/wf-11.png)

1. Conferma gli aggiornamenti selezionando.
1. Conferma le modifiche con **Sincronizza** (barra degli strumenti dell’editor) per generare il modello runtime.

   Consulta [Sincronizza il flusso di lavoro](#sync-your-workflow-generate-a-runtime-model) per i dettagli.

### Creazione di un flusso di lavoro transitorio {#creating-a-transient-workflow}

Puoi creare una [Transitorio](/help/sites-developing/workflows.md#transient-workflows) modello di flusso di lavoro durante la creazione di un modello o modificandone uno esistente:

1. Apri il modello di flusso di lavoro per [modifica](#editinganexistingworkflow).
1. Seleziona **Proprietà modello flusso di lavoro** dalla barra degli strumenti.
1. Nella finestra di dialogo attiva **Flusso di lavoro transitorio** (o disattivarla se necessario):

   ![wf-07](assets/wf-07.png)

1. Conferma la modifica con **Salva e chiudi**; seguito da **Sincronizza** (barra degli strumenti dell’editor) per generare il modello runtime.

   Consulta [Sincronizza il flusso di lavoro](#sync-your-workflow-generate-a-runtime-model) per i dettagli.

>[!NOTE]
>
>Quando esegui un flusso di lavoro in [transitorio](/help/sites-developing/workflows.md#transient-workflows) modalità AEM non memorizza alcuna cronologia del flusso di lavoro. Pertanto, [Timeline](/help/sites-authoring/basic-handling.md#timeline) non visualizza alcuna informazione correlata a tale flusso di lavoro.

## Rendere disponibili i modelli di flusso di lavoro nell’interfaccia utente touch {#classic2touchui}

Se un modello di flusso di lavoro è presente nell’interfaccia classica, ma non è presente nel menu a comparsa di selezione nella **[!UICONTROL Timeline]** dell’interfaccia utente touch, quindi segui la configurazione per renderla disponibile. I passaggi seguenti illustrano l’utilizzo del modello di flusso di lavoro denominato **[!UICONTROL Richiesta di attivazione]**.

1. Verifica che il modello non sia disponibile nell’interfaccia utente touch. Accedere a una risorsa tramite `/assets.html/content/dam` percorso. Seleziona una risorsa. Apri **[!UICONTROL Timeline]** nella barra a sinistra. Clic **[!UICONTROL Avvia flusso di lavoro]** e confermare che **[!UICONTROL Richiesta di attivazione]** il modello non è presente nell’elenco a comparsa.

1. Naviga **[!UICONTROL Strumenti > Generale > Assegnazione tag]**. Seleziona **[!UICONTROL Flusso di lavoro]**.

1. Seleziona **[!UICONTROL Crea > Crea tag]**. Imposta **[!UICONTROL Titolo]** as `DAM` e **[!UICONTROL Nome]** as `dam`. Seleziona **[!UICONTROL Invia]**.
   ![Crea tag nel modello di flusso di lavoro](assets/workflow_create_tag.png)

1. Accedi a **[!UICONTROL Strumenti > Workflow > Modelli]**. Seleziona **[!UICONTROL Richiesta di attivazione]**, quindi seleziona **[!UICONTROL Modifica]**.

1. Seleziona **[!UICONTROL Modifica]**, apri **[!UICONTROL Informazioni pagina]** e da qui selezionare **[!UICONTROL Apri proprietà]** e vai al **[!UICONTROL Base]** (se non è già aperta).

1. Aggiungi `Workflow : DAM` a **[!UICONTROL Tag]** campo. Conferma la selezione selezionando (segno di spunta).

1. Conferma l’aggiunta del tag con **[!UICONTROL Salva e chiudi]**.
   ![Modifica proprietà pagina del modello](assets/workflow_model_edit_activation1.png)

1. Completa il processo con **[!UICONTROL Sincronizza]**. Il flusso di lavoro è ora disponibile nell’interfaccia utente touch.

### Configurazione di un flusso di lavoro per il supporto di più risorse {#configuring-a-workflow-for-multi-resource-support}

Puoi configurare un modello di flusso di lavoro per [Supporto di più risorse](/help/sites-developing/workflows.md#multi-resource-support) durante la creazione di un modello o modificandone uno esistente:

1. Apri il modello di flusso di lavoro per [modifica](#editinganexistingworkflow).
1. Seleziona **Proprietà modello flusso di lavoro** dalla barra degli strumenti.

1. Nella finestra di dialogo attiva **Supporto di più risorse** (o disattivarla se necessario):

   ![wf-08](assets/wf-08.png)

1. Conferma la modifica con **Salva e chiudi**; seguito da **Sincronizza** (barra degli strumenti dell’editor) per generare il modello runtime.

   Consulta [Sincronizza il flusso di lavoro](#sync-your-workflow-generate-a-runtime-model) per i dettagli.

### Configurazione delle fasi del flusso di lavoro (che mostrano l’avanzamento del flusso di lavoro) {#configuring-workflow-stages-that-show-workflow-progress}

[Fasi flusso di lavoro](/help/sites-developing/workflows.md#workflow-stages) visualizzare l’avanzamento di un flusso di lavoro durante la gestione delle attività.

>[!CAUTION]
>
>Se le fasi del flusso di lavoro sono definite **Proprietà pagina**, ma non viene utilizzato per nessuno dei passaggi del flusso di lavoro, la barra di avanzamento non mostra alcun avanzamento (indipendentemente dal passaggio del flusso di lavoro corrente).

Le fasi da rendere disponibili sono definite nei modelli di flusso di lavoro; i modelli di flusso di lavoro esistenti possono essere aggiornati per includere le definizioni delle fasi. È possibile definire un numero qualsiasi di fasi per il modello di flusso di lavoro.

Per definire **Fasi** per il workflow:

1. Apri il modello di flusso di lavoro per la modifica.
1. Seleziona **Proprietà modello flusso di lavoro** dalla barra degli strumenti. Quindi apri la **Fasi** scheda.
1. Aggiungi (e posiziona) il necessario **Fasi**. È possibile definire un numero qualsiasi di fasi per il modello di flusso di lavoro.

   Ad esempio:

   ![wf-08-1](assets/wf-08-1.png)

1. Clic **Salva e chiudi** per salvare le proprietà.
1. Assegna una fase a ciascuno dei passaggi nel modello di flusso di lavoro. Ad esempio:

   ![wf-09](assets/wf-09.png)

   È possibile assegnare una fase a più fasi. Ad esempio:

   | **Passaggio** | **Ambiente di staging** |
   |---|---|
   | Passaggio 1 | Creare |
   | Passaggio 2 | Creare |
   | Passaggio 3 | Recensione |
   | Passaggio 4 | Approva |
   | Passaggio 5 | Approva |
   | Passaggio 6 | Completa |

1. Conferma le modifiche con **Sincronizza** (barra degli strumenti dell’editor) per generare il modello runtime.

   Consulta [Sincronizza il flusso di lavoro](#sync-your-workflow-generate-a-runtime-model) per i dettagli.

## Esportazione di un modello di flusso di lavoro in un pacchetto {#exporting-a-workflow-model-in-a-package}

Per esportare un modello di flusso di lavoro in un pacchetto:

1. Creare un pacchetto utilizzando [Gestione pacchetti](/help/sites-administering/package-manager.md#package-manager):

   1. Passa a Gestione pacchetti tramite **Strumenti**, **Distribuzione**, **Pacchetti**.

   1. Clic **Crea pacchetto**.
   1. Specifica la **Nome pacchetto**, ed eventuali altri dettagli richiesti.
   1. Fai clic su **OK**.

1. Clic **Modifica** sulla barra degli strumenti del nuovo pacchetto.

1. Apri **Filtri** scheda.

1. Seleziona **Aggiungi filtro** e specifica il percorso del modello di flusso di lavoro *progettazione*:

   `/conf/global/settings/workflow/models/<*your-model-name*>`

   Clic **Fine**.

1. Seleziona **Aggiungi filtro** e specifica il percorso del *runtime* modello flusso di lavoro:

   `/var/workflow/models/<*your-model-name*>`

   Clic **Fine**.

1. Aggiungi altri filtri per gli script personalizzati utilizzati dal modello.
1. Clic **Salva** per confermare le definizioni dei filtri.
1. Seleziona **Genera** dalla barra degli strumenti della definizione del pacchetto.
1. Seleziona **Scarica** dalla barra degli strumenti del pacchetto.

## Utilizzo dei flussi di lavoro per elaborare gli invii dei moduli {#using-workflows-to-process-form-submissions}

È possibile configurare un modulo da elaborare tramite il flusso di lavoro selezionato. Quando gli utenti inviano il modulo, viene creata una nuova istanza di flusso di lavoro con i dati dell’invio del modulo come payload.

Per configurare il flusso di lavoro da utilizzare con il modulo:

1. Crea una pagina e aprila per la modifica.
1. Aggiungi un **Modulo** alla pagina.
1. **Configura** il **Inizio modulo** componente visualizzato nella pagina.
1. Utilizzare **Avvia flusso di lavoro** per selezionare il flusso di lavoro desiderato tra quelli disponibili:

   ![wf-12](assets/wf-12.png)

1. Conferma la nuova configurazione del modulo selezionando.

## Verifica dei flussi di lavoro {#testing-workflows}

È buona prassi quando si esegue il test di un flusso di lavoro per utilizzare diversi tipi di payload, inclusi quelli diversi da quello per cui è stato sviluppato. Ad esempio, se desideri che il flusso di lavoro gestisca le risorse, testa impostando una pagina come payload e assicurati che non generi errori.

Ad esempio, prova il nuovo flusso di lavoro come segue:

1. [Avvia il modello di flusso di lavoro](/help/sites-administering/workflows-starting.md) dalla console.
1. Definisci il **Payload** e confermare.

1. Intraprende le azioni necessarie in modo che il flusso di lavoro proceda.
1. Monitora i file di registro durante l’esecuzione del flusso di lavoro.

Puoi anche configurare l’AEM per la visualizzazione **DEBUG** messaggi nei file di registro. Consulta [Registrazione](/help/sites-deploying/configure-logging.md) per ulteriori informazioni e al termine dello sviluppo, impostare **Livello registro** torna a **Info**.

## Esempi {#examples}

### Esempio: creazione di un flusso di lavoro (semplice) per accettare o rifiutare una richiesta di pubblicazione {#example-creating-a-simple-workflow-to-accept-or-reject-a-request-for-publication}

Per illustrare alcune delle possibilità di creazione di un flusso di lavoro, nell&#39;esempio seguente viene creata una variante di `Publish Example` flusso di lavoro.

1. [Creare un modello di flusso di lavoro](#creating-a-new-workflow).

   Il nuovo flusso di lavoro conterrà:

   * **Avvio del flusso**
   * `Step 1`
   * **Fine del flusso**

1. Elimina `Step 1` (in quanto si tratta del tipo di passaggio errato per questo esempio):

   * Fai clic sul passaggio e seleziona **Elimina** dalla barra degli strumenti del componente. Conferma l’azione.

1. Dalla sezione **Flusso di lavoro** selezione dei passaggi, trascina un **Passaggio partecipante** nel flusso di lavoro e posizionarlo tra **Inizio flusso** e **Fine flusso**.
1. Per aprire la finestra di dialogo delle proprietà:

   * Fai clic sul passaggio partecipante e seleziona **Configura** dalla barra degli strumenti del componente.
   * Fare doppio clic sul passaggio partecipante.

1. In **Comune** scheda immetti `Validate Content` per entrambi i **Titolo** e **Descrizione**.
1. Apri **Utente/Gruppo** scheda:

   * Attiva **Notifica all&#39;utente via e-mail**.
   * Seleziona `Administrator` ( `admin`) per **Utente/Gruppo** campo.

   >[!NOTE]
   >
   >Per l’invio delle e-mail, [è necessario configurare il servizio di posta e i dettagli dell&#39;account utente](/help/sites-administering/notification.md).

1. Conferma gli aggiornamenti selezionando.

   Tornerai alla panoramica del modello di flusso di lavoro. Il passaggio partecipante sarà stato rinominato in `Validate Content`.

1. Trascina una **Suddivisione O** nel flusso di lavoro e posizionarlo tra `Validate Content` e **Fine flusso**.
1. Apri **Suddivisione O** per la configurazione.
1. Configurare:

   * **Comune**: specifica il nome della divisione.
   * **Ramo 1**: seleziona **Percorso predefinito**.

   * **Ramo 2**: assicurare **Percorso predefinito** non è selezionato.

1. Conferma gli aggiornamenti a **Suddivisione O**.
1. Trascina un **Passaggio partecipante** nel ramo sinistro, apri le proprietà, specifica i seguenti valori, quindi conferma le modifiche:

   * **Titolo**: `Reject Publish Request`

   * **Utente/Gruppo**: ad esempio, `projects-administrators`

   * **Notifica all&#39;utente via e-mail**: attiva questa opzione per inviare all’utente una notifica via e-mail.

1. Trascina un **Passaggio processo** nel ramo destro, apri le proprietà, specifica i seguenti valori, quindi conferma le modifiche:

   * **Titolo**: `Publish Page as Requested`

   * **Processo**: seleziona `Activate Page`. Questo processo pubblica la pagina selezionata nelle istanze dell’editore.

1. Clic **Sincronizza** (barra degli strumenti dell’editor) per generare il modello runtime.

   Consulta [Sincronizza il flusso di lavoro](#sync-your-workflow-generate-a-runtime-model) per i dettagli.

   Il nuovo modello di flusso di lavoro sarà simile al seguente:

   ![wf-13](assets/wf-13.png)

1. Applica questo flusso di lavoro alla pagina, in modo che quando l’utente si sposta in **Completa** il **Convalida contenuto** , è possibile scegliere se **Pubblica pagina come richiesto**, o **Rifiuta richiesta di pubblicazione**.

   ![chlimage_1-72](assets/chlimage_1-72.png)

### Esempio: definizione di una regola per una suddivisione OR utilizzando lo script ECMA {#defineruleecmascript}

**Suddivisione O** I passaggi ti consentono di introdurre nel flusso di lavoro i percorsi di elaborazione condizionale.

Per definire una regola OR, procedere come segue:

1. Crea due script e salvali nell’archivio, ad esempio, in:

   `/apps/myapp/workflow/scripts`

   >[!NOTE]
   >
   >Gli script devono avere [funzione `check()`](#function-check) che restituisce un valore booleano.

1. Modifica il flusso di lavoro e aggiungi **Suddivisione O** al modello.
1. Modifica le proprietà di **Ramo 1** del **Suddivisione O**:

   * Definisci come **Percorso predefinito** impostando **Valore** a `true`.

   * As **Regola**, imposta il percorso dello script. Ad esempio:
     `/apps/myapp/workflow/scripts/myscript1.ecma`

   >[!NOTE]
   >
   >Se necessario, puoi cambiare l’ordine della filiale.

1. Modifica le proprietà del **Ramo 2** del **Suddivisione O**.

   * As **Regola**, imposta il percorso dell&#39;altro script. Ad esempio:
     `/apps/myapp/workflow/scripts/myscript2.ecma`

1. Imposta le proprietà dei singoli passaggi in ciascun ramo. Assicurati che le **Utente/Gruppo** è impostato.
1. Clic **Sincronizza** (barra degli strumenti dell’editor) per mantenere le modifiche apportate al modello di runtime.

   Consulta [Sincronizza il flusso di lavoro](#sync-your-workflow-generate-a-runtime-model) per i dettagli.

#### Function Check() {#function-check}

>[!NOTE]
>
>Consulta [Utilizzo di ECMAScript](/help/sites-developing/workflows-customizing-extending.md#using-ecmascript).

Lo script di esempio seguente restituisce `true` se il nodo è un `JCR_PATH` situato in `/content/we-retail/us/en`:

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

### Esempio: richiesta di attivazione personalizzata {#example-customized-request-for-activation}

Puoi personalizzare qualsiasi flusso di lavoro predefinito. Per ottenere un comportamento personalizzato, puoi sovrapporre i dettagli del flusso di lavoro appropriato.

Ad esempio: **Richiesta di attivazione**. Questo flusso di lavoro viene utilizzato per la pubblicazione di pagine in **Sites** e viene attivato automaticamente quando un autore di contenuti non dispone dei diritti di replica appropriati. Consulta [Personalizzazione dell’authoring delle pagine - Personalizzazione del flusso di lavoro di richiesta di attivazione](/help/sites-developing/customizing-page-authoring-touch.md#customizing-the-request-for-activation-workflow) per ulteriori dettagli.
