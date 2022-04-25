---
title: Sviluppo di Forms (interfaccia classica)
seo-title: Developing Forms (Classic UI)
description: Scopri come sviluppare moduli
seo-description: Learn how to develop forms
uuid: 33859f29-edc5-4bd5-a634-35549f3b5ccf
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 6ee3bd3b-51d1-462f-b12e-3cbe24898b85
docset: aem65
exl-id: f43e9491-aa8f-40af-9800-123695142559
source-git-commit: 4df14f837569997c3e4da8161ac2b099c39d89a6
workflow-type: tm+mt
source-wordcount: '1942'
ht-degree: 18%

---

# Sviluppo di Forms (interfaccia classica){#developing-forms-classic-ui}

La struttura di base di un modulo è la seguente:

* Inizio modulo
* Elementi modulo
* Fine modulo

Tutte queste operazioni sono realizzate con una serie di default [Componenti per moduli](/help/sites-authoring/default-components.md#form)disponibile in un’installazione standard AEM.

Oltre a [sviluppo di nuovi componenti](/help/sites-developing/developing-components-samples.md) per l’uso sui moduli è inoltre possibile:

* [Caricare il modulo con i valori](#preloading-form-values)
* [Precaricare (determinati) campi con più valori](#preloading-form-fields-with-multiple-values)
* [Sviluppare nuove azioni](#developing-your-own-form-actions)
* [Sviluppare nuovi vincoli](#developing-your-own-form-constraints)
* [Mostra o nasconde campi modulo specifici](#showing-and-hiding-form-components)

[Uso degli script](#developing-scripts-for-use-with-forms) per estendere le funzionalità, se necessario.

>[!NOTE]
>
>Questo documento si concentra sullo sviluppo di moduli utilizzando [Componenti di base](/help/sites-authoring/default-components-foundation.md) nell’interfaccia classica. L&#39;Adobe consiglia di sfruttare il nuovo [Componenti core](https://docs.adobe.com/content/help/it/experience-manager-core-components/using/introduction.html) e [Nascondi condizioni](/help/sites-developing/hide-conditions.md) per lo sviluppo di moduli nell’interfaccia touch.

## Precaricamento dei valori dei moduli {#preloading-form-values}

Il componente Inizio modulo fornisce un campo per **Percorso di caricamento**, un percorso facoltativo che punta a un nodo nel repository.

Percorso di caricamento è il percorso delle proprietà del nodo utilizzato per caricare valori predefiniti in più campi del modulo.

Si tratta di un campo facoltativo, per specificare il percorso di un nodo nella directory archivio. Quando alcune proprietà di questo nodo corrispondono ai nomi dei campi, i relativi campi del modulo vengono precompilati con il valore della proprietà corrispondente. In assenza di proprietà corrispondenti, il campo contiene il valore predefinito.

>[!NOTE]
>
>A [azione modulo](#developing-your-own-form-actions) può anche impostare la risorsa da cui caricare i valori iniziali. Questa operazione viene eseguita utilizzando `FormsHelper#setFormLoadResource` interno `init.jsp`.
>
>Solo in caso contrario, l’autore compilerà il modulo dal percorso impostato nel componente modulo iniziale.

### Precaricamento dei campi modulo con più valori {#preloading-form-fields-with-multiple-values}

Anche i vari campi del modulo hanno la **Percorso di caricamento elementi**, di nuovo un percorso facoltativo che punta a un nodo nella directory archivio.

La **Percorso di caricamento elementi** è il percorso delle proprietà nodo utilizzato per caricare valori predefiniti in quel campo specifico del modulo, ad esempio un [elenco a discesa](/help/sites-authoring/default-components-foundation.md#dropdown-list), [gruppo di caselle di controllo](/help/sites-authoring/default-components-foundation.md#checkbox-group) o [gruppo radio](/help/sites-authoring/default-components-foundation.md#radio-group).

#### Esempio: precaricamento di un elenco a discesa con più valori {#example-preloading-a-dropdown-list-with-multiple-values}

Un elenco a discesa più essere configurato con una serie di valori da selezionare.

La **Percorso di caricamento elementi** può essere utilizzato per accedere a un elenco da una cartella del repository e precaricarlo nel campo :

1. Crea una nuova cartella sling ( `sling:Folder`), ad esempio, `/etc/designs/<myDesign>/formlistvalues`

1. Aggiungi una nuova proprietà (ad esempio, `myList`) di tipo stringa con più valori ( `String[]`) per contenere l’elenco degli elementi a discesa. Il contenuto può anche essere importato utilizzando uno script, ad esempio con uno script JSP o cURL in uno script shell.

1. Utilizza il percorso completo nel **Percorso di caricamento elementi** campo: ad esempio, `/etc/designs/geometrixx/formlistvalues/myList`

Tieni presente che se i valori in `String[]` sono di formato come indicato di seguito:

* `AL=Alabama`
* `AK=Alaska`
* ecc.

AEM quindi genera l’elenco come:

* `<option value="AL">Alabama</option>`
* `<option value="AK">Alaska</option>`

Questa funzione può, ad esempio, essere utilizzata in un’impostazione multilingue.

### Sviluppo di azioni modulo personalizzate {#developing-your-own-form-actions}

Un modulo richiede un’azione Un’azione definisce l’operazione eseguita quando il modulo viene inviato insieme ai dati utente.

Una serie di azioni sono fornite con un&#39;installazione standard AEM, che può essere visto in:

`/libs/foundation/components/form/actions`

e **Tipo di azione** elenco **Modulo** componente:

![chlimage_1-8](assets/chlimage_1-8.png)

Questa sezione illustra come sviluppare un’azione modulo personalizzata da includere in questo elenco.

Puoi aggiungere la tua azione in `/apps` come segue:

1. Crea un nodo di tipo `sling:Folder`. Specifica un nome che rifletta l’azione da implementare.

   Esempio:

   `/apps/myProject/components/customFormAction`

1. In questo nodo definire le seguenti proprietà, quindi fare clic su **Salva tutto** per mantenere le modifiche:

   * `sling:resourceType` - impostato come `foundation/components/form/action`

   * `componentGroup` - definire come `.hidden`

   * Facoltativamente:

      * `jcr:title` - specifica un titolo a tua scelta, che verrà visualizzato nell’elenco a discesa di selezione. Se non è impostato, viene visualizzato il nome del nodo

      * `jcr:description` - inserire una descrizione della scelta

1. Nella cartella crea un nodo di dialogo:

   1. Aggiungi i campi in modo che l’autore possa modificare la finestra di dialogo dei moduli una volta selezionata l’azione.

1. Nella cartella crea:

   1. Uno script.
Il nome dello script è `post.POST.<extension>`ad esempio `post.POST.jsp`
Lo script post viene richiamato quando un modulo viene inviato per elaborare il modulo e contiene il codice che gestisce i dati in arrivo dal modulo 
`POST`.

   1. Aggiungere uno script in avanti che viene richiamato quando il modulo viene inviato.
Il nome dello script è `forward.<extension`>, ad esempio `forward.jsp`
Questo script può definire un percorso. La richiesta corrente viene quindi inoltrata al percorso specificato.
   La chiamata necessaria è `FormsHelper#setForwardPath` (2 varianti). Un caso tipico è quello di eseguire una convalida, o logica, per trovare il percorso di destinazione e quindi inoltrarlo a tale percorso, lasciando che il servlet Sling POST predefinito esegua l’archiviazione effettiva in JCR.

   Può essere presente anche un altro servlet che esegue l’elaborazione effettiva, in tal caso l’azione modulo e il `forward.jsp` agisce solo come codice &quot;colla&quot;. Un esempio è rappresentato dall’azione di posta in `/libs/foundation/components/form/actions/mail`, che comunica i dettagli a `<currentpath>.mail.html`dove si trova un servlet di posta.

   Quindi:

   * a `post.POST.jsp` è utile per le piccole operazioni che sono completamente svolte dall&#39;azione stessa
   * mentre `forward.jsp` è utile quando è richiesta solo la delega.

   L’ordine di esecuzione degli script è il seguente:

   * Al momento del rendering del modulo ( `GET`):

      1. `init.jsp`
      1. per tutti i vincoli del campo: `clientvalidation.jsp`
      1. convalida del moduloRT: `clientvalidation.jsp`
      1. il modulo viene caricato tramite la risorsa di caricamento se impostato
      1. `addfields.jsp` durante il rendering `<form></form>`
   * al momento della gestione di un modulo `POST`:

      1. `init.jsp`
      1. per tutti i vincoli del campo: `servervalidation.jsp`
      1. convalida del moduloRT: `servervalidation.jsp`
      1. `forward.jsp`
      1. se è stato impostato un percorso avanti ( `FormsHelper.setForwardPath`), inoltra la richiesta, quindi chiama `cleanup.jsp`

      1. se non è stato impostato alcun percorso in avanti, chiama `post.POST.jsp` (finisce qui, no `cleanup.jsp` chiamato)




1. Aggiungi nuovamente nella cartella facoltativamente:

   1. Uno script per l’aggiunta di campi.
Il nome dello script è `addfields.<extension>`ad esempio `addfields.jsp`
Un 
`addfields` lo script viene richiamato immediatamente dopo la scrittura di HTML per l’avvio del modulo. Questo consente di aggiungere campi di input personalizzati o altri HTML all’interno del modulo.

   1. Uno script di inizializzazione.
Il nome dello script è `init.<extension>`ad esempio `init.jsp`
Questo script viene richiamato quando si esegue il rendering del modulo. Può essere utilizzato per inizializzare le specifiche delle azioni.

   1. Uno script di pulizia.
Il nome dello script è `cleanup.<extension>`ad esempio `cleanup.jsp`
Questo script può essere utilizzato per eseguire la pulizia.

1. Utilizza la **Forms** in un parsys. La **Tipo di azione** La nuova azione verrà ora inclusa nel menu a discesa.

   >[!NOTE]
   >
   >Per visualizzare le azioni predefinite che fanno parte del prodotto:
   >
   >
   >`/libs/foundation/components/form/actions`

### Sviluppo di vincoli modulo personalizzati {#developing-your-own-form-constraints}

I vincoli possono essere imposti a due livelli:

* Per [singoli campi (vedere la procedura seguente)](#constraints-for-individual-fields)
* Come [convalida globale dei moduli](#form-global-constraints)

#### Vincoli per i singoli campi {#constraints-for-individual-fields}

Puoi aggiungere vincoli personalizzati per un singolo campo (in `/apps`) come segue:

1. Crea un nodo di tipo `sling:Folder`. Specifica un nome che rifletta il vincolo da implementare.

   Esempio:

   `/apps/myProject/components/customFormConstraint`

1. In questo nodo definire le seguenti proprietà, quindi fare clic su **Salva tutto** per mantenere le modifiche:

   * `sling:resourceType` - impostare `foundation/components/form/constraint`

   * `constraintMessage` - un messaggio personalizzato che verrà visualizzato se il campo non è valido, in base al vincolo, al momento dell&#39;invio del modulo

   * Facoltativamente:

      * `jcr:title` - specifica un titolo a tua scelta, che verrà visualizzato nell’elenco di selezione. Se non è impostato, viene visualizzato il nome del nodo
      * `hint` - ulteriori informazioni, per l&#39;utente, su come utilizzare il campo

1. All’interno di questa cartella possono essere necessari i seguenti script:

   * Uno script di convalida client: Il nome dello script è `clientvalidation.<extension>`ad esempio `clientvalidation.jsp`
Viene richiamato quando viene eseguito il rendering del campo modulo. Può essere utilizzato per creare JavaScript client per convalidare il campo sul client.

   * Uno script di convalida server: Il nome dello script è `servervalidation.<extension>`ad esempio `servervalidation.jsp`
Viene richiamato quando il modulo viene inviato. Può essere utilizzato per convalidare il campo sul server dopo l’invio.

>[!NOTE]
>
>I vincoli di esempio sono visibili in:
>
>`/libs/foundation/components/form/constraints`

#### Vincoli globali modulo {#form-global-constraints}

La convalida globale del modulo viene specificata configurando un tipo di risorsa nel componente modulo iniziale ( `validationRT`). Esempio:

`apps/myProject/components/form/validation`

Puoi quindi definire:

* a `clientvalidation.jsp` - inserito dopo gli script di convalida client del campo
* e `servervalidation.jsp` - chiamato anche dopo le convalide dei singoli server di campi su un `POST`.

### Mostrare e nascondere i componenti di un modulo {#showing-and-hiding-form-components}

È possibile configurare il modulo in modo da mostrare o nascondere i componenti in base al valore di altri campi del modulo.

La modifica della visibilità di un campo modulo è utile se il campo è richiesto solo in presenza di particolari condizioni. Ad esempio, in un modulo di feedback, può essere presente una domanda che chiede al cliente se desidera ricevere per e-mail informazioni sui prodotti. Se il cliente risponde Sì, compare un campo di testo per l’inserimento dell’indirizzo e-mail.

Utilizza la **Modifica regole mostra/nascondi** per specificare le condizioni in cui un componente modulo viene visualizzato o nascosto.

![redattore](assets/showhideeditor.png)

Utilizzate i campi nella parte superiore della finestra di dialogo per specificare le seguenti informazioni:

* Se si specificano le condizioni per nascondere o mostrare il componente.
* Se qualsiasi o tutte le condizioni devono essere soddisfatte per mostrare o nascondere il componente.

Una o più condizioni vengono visualizzate al di sotto di questi campi. Una condizione prevede il confronto del valore di un altro componente (dello tesso modulo) con un particolare valore. Se il valore effettivo inserito nel campo soddisfa la condizione, questa viene considerata true (vera). Le condizioni includono le seguenti informazioni:

* Il Titolo del campo che si sta verificando.
* Un operatore.
* Un valore rispetto al quale viene confrontato il valore del campo.

Ad esempio, un componente Gruppo pulsanti di scelta con il titolo `Receive email notifications?`* contiene `Yes` e `No` pulsanti di scelta. Componente Campo di testo con il titolo `Email Address` utilizza la seguente condizione in modo che sia visibile se `Yes` è selezionato:

![condizione minima](assets/showhidecondition.png)

In Javascript, per fare riferimento ai campi, nelle condizioni viene utilizzato il valore della proprietà Nome elemento. Nell’esempio precedente, la proprietà Nome elemento del componente Gruppo pulsanti di scelta è `contact`. Il seguente codice rappresenta il codice JavaScript per questo esempio:

`((contact == "Yes"))`

**Per visualizzare o nascondere un componente di un modulo:**

1. Modifica il componente modulo specifico.

1. Seleziona **Mostra/Nascondi** per aprire **Modifica regole mostra/nascondi** finestra di dialogo:

   * Nel primo elenco a discesa, seleziona una delle seguenti opzioni **Mostra** o **Nascondi** per specificare se le condizioni determinano se mostrare o nascondere il componente.

   * Nell’elenco a discesa alla fine della riga superiore seleziona:

      * **tutto** - se tutte le condizioni devono essere soddisfatte per mostrare o nascondere il componente
      * **qualsiasi** - se solo una o più condizioni devono essere soddisfatte per mostrare o nascondere il componente
   * Nella riga della condizione (una è presentata come predefinita) seleziona un componente, un operatore e specifica un valore.
   * Aggiungi altre condizioni se necessario facendo clic su **Aggiungi condizione**.

   Esempio:

   ![chlimage_1-9](assets/chlimage_1-9.png)

1. Fai clic su **OK** per salvare la definizione.

1. Dopo aver salvato la definizione, **Modifica regole** accanto al **Mostra/Nascondi** nelle proprietà del componente modulo. Fai clic su questo collegamento per aprire **Modifica regole mostra/nascondi** per apportare modifiche.

   Fai clic su **OK** per salvare tutte le modifiche.

   ![chlimage_1-10](assets/chlimage_1-10.png)

   >[!CAUTION]
   >
   >Gli effetti delle definizioni Mostra/Nascondi possono essere visti e testati:
   >
   >* in **Anteprima** nell’ambiente di authoring (richiede un ricaricamento della pagina quando si passa alla prima anteprima)
   >
   >* sull’ambiente di pubblicazione


#### Gestione dei riferimenti ai componenti interrotti {#handling-broken-component-references}

Per le condizioni mostra/nascondi viene utilizzato il valore della proprietà Nome elemento per fare riferimento ad altri componenti del modulo. La configurazione Mostra/Nascondi non è valida se una delle condizioni fa riferimento a un componente eliminato o per il quale è stata modificata la proprietà Nome elemento. Se si verifica questa situazione, è necessario aggiornare manualmente le condizioni; in caso contrario si verificherà un errore durante il caricamento del modulo.

Se la configurazione Mostra/Nascondi non è valida, la configurazione viene fornita solo come codice JavaScript. Modificate il codice per correggere i problemi. Nel codice viene usata la proprietà Nome elemento impostata originariamente per fare riferimento ai componenti.

### Sviluppo di script da utilizzare con Forms {#developing-scripts-for-use-with-forms}

Per ulteriori informazioni sugli elementi API utilizzabili per la scrittura di script, consulta la sezione [javadocs relativi ai moduli](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/foundation/forms/package-summary.html).

È possibile utilizzarlo per azioni quali la chiamata di un servizio prima dell’invio del modulo e l’annullamento del servizio in caso di errore:

* Definire il tipo di risorsa di convalida
* Includi uno script per la convalida:

   * In JSP, richiamare il servizio Web e creare un oggetto `com.day.cq.wcm.foundation.forms.ValidationInfo` contenente i messaggi di errore. Se si verificano degli errori, i dati del modulo non verranno inviati.
