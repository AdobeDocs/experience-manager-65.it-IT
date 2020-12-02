---
title: Sviluppo di Forms (interfaccia classica)
seo-title: Sviluppo di Forms (interfaccia classica)
description: Scopri come sviluppare moduli
seo-description: Scopri come sviluppare moduli
uuid: 33859f29-edc5-4bd5-a634-35549f3b5ccf
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 6ee3bd3b-51d1-462f-b12e-3cbe24898b85
docset: aem65
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '1952'
ht-degree: 18%

---


# Sviluppo di Forms (interfaccia classica){#developing-forms-classic-ui}

La struttura di base di un modulo è la seguente:

* Inizio modulo
* Elementi modulo
* Fine modulo

Tutti questi sono realizzati con una serie di componenti [Form ](/help/sites-authoring/default-components.md#form) predefiniti, disponibili in un&#39;installazione AEM standard.

Oltre a [sviluppare nuovi componenti](/help/sites-developing/developing-components-samples.md) da utilizzare nei moduli, è possibile:

* [Precaricare il modulo con i valori](#preloading-form-values)
* [Precarica (alcuni campi con più valori)](#preloading-form-fields-with-multiple-values)
* [Sviluppare nuove azioni](#developing-your-own-form-actions)
* [Sviluppare nuovi vincoli](#developing-your-own-form-constraints)
* [Mostrare o nascondere campi modulo specifici](#showing-and-hiding-form-components)

[Utilizzare ](#developing-scripts-for-use-with-forms) gli script per estendere le funzionalità laddove necessario.

>[!NOTE]
>
>Questo documento si concentra sullo sviluppo di moduli utilizzando [Foundation Components](/help/sites-authoring/default-components-foundation.md) nell&#39;interfaccia classica.  Adobe consiglia di utilizzare i nuovi [Componenti core](https://docs.adobe.com/content/help/it-IT/experience-manager-core-components/using/introduction.html) e [Nascondi condizioni](/help/sites-developing/hide-conditions.md) per lo sviluppo di moduli nell&#39;interfaccia touch.

## Precaricamento dei valori del modulo {#preloading-form-values}

Il componente Inizio modulo fornisce un campo per il percorso **Load Path**, un percorso facoltativo che punta a un nodo nella directory archivio.

Percorso di caricamento è il percorso delle proprietà nodo utilizzato per caricare valori predefiniti in più campi del modulo.

Si tratta di un campo facoltativo, per specificare il percorso di un nodo nella directory archivio. Quando alcune proprietà di questo nodo corrispondono ai nomi dei campi, i relativi campi del modulo vengono precompilati con il valore della proprietà corrispondente. In assenza di proprietà corrispondenti, il campo contiene il valore predefinito.

>[!NOTE]
>
>Un&#39;azione [modulo](#developing-your-own-form-actions) può anche impostare la risorsa da cui caricare i valori iniziali. Questa operazione viene eseguita utilizzando `FormsHelper#setFormLoadResource` all&#39;interno di `init.jsp`.
>
>Solo se non è impostato, l&#39;autore compilerà il modulo dal percorso impostato nel componente Modulo iniziale.

### Precaricamento dei campi modulo con più valori {#preloading-form-fields-with-multiple-values}

Diversi campi modulo dispongono anche del percorso di caricamento **Elementi**, anch&#39;esso un percorso facoltativo che punta a un nodo nella directory archivio.

Il **Percorso di caricamento elementi** è il percorso delle proprietà nodo utilizzato per caricare valori predefiniti in tale campo specifico del modulo, ad esempio un [elenco a discesa](/help/sites-authoring/default-components-foundation.md#dropdown-list), [gruppo di caselle di controllo](/help/sites-authoring/default-components-foundation.md#checkbox-group) o un [gruppo di pulsanti di scelta](/help/sites-authoring/default-components-foundation.md#radio-group).

#### Esempio: precaricamento di un elenco a discesa con più valori {#example-preloading-a-dropdown-list-with-multiple-values}

Un elenco a discesa più essere configurato con una serie di valori da selezionare.

**Percorso di caricamento elementi** può essere utilizzato per accedere a un elenco da una cartella della directory archivio e precaricarlo nel campo:

1. Creare una nuova cartella sling ( `sling:Folder`)
ad esempio, `/etc/designs/<myDesign>/formlistvalues`

1. Aggiungete una nuova proprietà (ad esempio, `myList`) di tipo stringa multivalore ( `String[]`) per contenere l&#39;elenco di elementi a discesa. Il contenuto può essere importato anche utilizzando uno script, ad esempio con uno script JSP o cURL in uno script shell.

1. Utilizzare il percorso completo nel campo **Percorso di caricamento elementi**:
ad esempio, `/etc/designs/geometrixx/formlistvalues/myList`

Tenere presente che se i valori in `String[]` sono formattati come segue:

* `AL=Alabama`
* `AK=Alaska`
* *etc.*

aem quindi generare l’elenco come:

* `<option value="AL">Alabama</option>`
* `<option value="AK">Alaska</option>`

Questa funzione può, ad esempio, essere utilizzata in un ambiente multilingue.

### Sviluppo di azioni modulo personalizzate {#developing-your-own-form-actions}

Un modulo richiede un’azione Un&#39;azione definisce l&#39;operazione che viene eseguita quando il modulo viene inviato con i dati utente.

Una serie di azioni vengono fornite con un&#39;installazione standard AEM, che è possibile vedere in:

`/libs/foundation/components/form/actions`

e nell&#39;elenco **Action Type** del componente **Form**:

![chlimage_1-8](assets/chlimage_1-8.png)

Questa sezione illustra come sviluppare un’azione per il modulo personalizzata da includere in questo elenco.

Puoi aggiungere la tua azione in `/apps` come segue:

1. Creare un nodo di tipo `sling:Folder`. Specificate un nome che rifletta l’azione da implementare.

   Esempio:

   `/apps/myProject/components/customFormAction`

1. In questo nodo definire le seguenti proprietà, quindi fare clic su **Salva tutto** per mantenere invariate le modifiche:

   * `sling:resourceType` - impostata come  `foundation/components/form/action`

   * `componentGroup` - Definisci come  `.hidden`

   * Facoltativamente:

      * `jcr:title` - specifica un titolo di tua scelta, che verrà visualizzato nell&#39;elenco a discesa di selezione. Se non è impostato, viene visualizzato il nome del nodo

      * `jcr:description` - inserire una descrizione della scelta

1. Nella cartella create un nodo di finestra di dialogo:

   1. Aggiungere i campi in modo che l&#39;autore possa modificare la finestra di dialogo dei moduli una volta selezionata l&#39;azione.

1. Nella cartella create:

   1. Uno script di pubblicazione.
Il nome dello script è `post.POST.<extension>`, ad esempio `post.POST.jsp`
Lo script post viene richiamato quando un modulo viene inviato per elaborare il modulo, contiene il codice che gestisce i dati provenienti dal modulo 
`POST`.

   1. Aggiungere uno script in avanti che viene richiamato all&#39;invio del modulo.
Il nome dello script è `forward.<extension`>, ad esempio `forward.jsp`
Questo script può definire un percorso. La richiesta corrente viene quindi inoltrata al percorso specificato.
   La chiamata necessaria è `FormsHelper#setForwardPath` (2 varianti). Un caso tipico consiste nell&#39;eseguire alcune operazioni di convalida, o logica, per individuare il percorso di destinazione e quindi inoltrarlo a tale percorso, consentendo al servlet Sling POST predefinito di eseguire la memorizzazione effettiva in JCR.

   Potrebbe anche essere presente un altro servlet che esegue l&#39;elaborazione effettiva, in tal caso l&#39;azione del modulo e il `forward.jsp` fungerebbero solo da codice &quot;colla&quot;. Un esempio è rappresentato dall&#39;azione di posta elettronica in `/libs/foundation/components/form/actions/mail`, che inoltra i dettagli a `<currentpath>.mail.html`posizione di un servlet di posta.

   Quindi:

   * a `post.POST.jsp` è utile per le piccole operazioni che vengono eseguite completamente dall&#39;azione stessa
   * mentre il `forward.jsp` è utile quando è richiesta solo la delega.

   L&#39;ordine di esecuzione degli script è il seguente:

   * Al momento del rendering del modulo ( `GET`):

      1. `init.jsp`
      1. per tutti i vincoli del campo: `clientvalidation.jsp`
      1. convalida del moduloRT: `clientvalidation.jsp`
      1. il modulo viene caricato tramite la risorsa di caricamento, se impostato
      1. `addfields.jsp` durante il rendering  `<form></form>`
   * durante la gestione di un modulo `POST`:

      1. `init.jsp`
      1. per tutti i vincoli del campo: `servervalidation.jsp`
      1. convalida del moduloRT: `servervalidation.jsp`
      1. `forward.jsp`
      1. se è stato impostato un percorso avanti ( `FormsHelper.setForwardPath`), inoltrate la richiesta, quindi chiamate `cleanup.jsp`

      1. se non è stato impostato alcun percorso in avanti, chiamare `post.POST.jsp` (termina qui, nessun percorso `cleanup.jsp` chiamato)




1. Anche nella cartella aggiungete facoltativamente:

   1. Uno script per l&#39;aggiunta di campi.
Il nome dello script è `addfields.<extension>`, ad esempio `addfields.jsp`
Uno script addfields viene richiamato subito dopo la scrittura dell&#39;HTML per l&#39;avvio del modulo. Questo consente di aggiungere campi di input personalizzati o altri elementi HTML di questo tipo all&#39;interno del modulo.

   1. Uno script di inizializzazione.
Il nome dello script è `init.<extension>`, ad esempio `init.jsp`
Questo script viene richiamato quando si esegue il rendering del modulo. Può essere utilizzato per inizializzare specifiche delle azioni. &quot;

   1. Uno script di pulizia.
Il nome dello script è `cleanup.<extension>`, ad esempio `cleanup.jsp`
Questo script può essere utilizzato per eseguire la pulizia.

1. Utilizzate il componente **Forms** in un parsys. Il menu a discesa **Tipo azione** ora include la nuova azione.

   >[!NOTE]
   >
   >Per visualizzare le azioni predefinite che fanno parte del prodotto:
   >
   >
   >`/libs/foundation/components/form/actions`

### Sviluppo di vincoli di modulo personalizzati {#developing-your-own-form-constraints}

I vincoli possono essere imposti a due livelli:

* Per [singoli campi (vedere la procedura seguente)](#constraints-for-individual-fields)
* Come [convalida form-global](#form-global-constraints)

#### Vincoli per i singoli campi {#constraints-for-individual-fields}

È possibile aggiungere vincoli personalizzati per un singolo campo (in `/apps`) come segue:

1. Creare un nodo di tipo `sling:Folder`. Specificare un nome che rifletta il vincolo da implementare.

   Esempio:

   `/apps/myProject/components/customFormConstraint`

1. In questo nodo definire le seguenti proprietà, quindi fare clic su **Salva tutto** per mantenere invariate le modifiche:

   * `sling:resourceType` - impostare  `foundation/components/form/constraint`

   * `constraintMessage` - un messaggio personalizzato che verrà visualizzato se il campo non è valido, in base al vincolo, all&#39;invio del modulo

   * Facoltativamente:

      * `jcr:title` - specifica un titolo di tua scelta, che verrà visualizzato nell&#39;elenco di selezione. Se non è impostato, viene visualizzato il nome del nodo
      * `hint` - ulteriori informazioni, per l&#39;utente, su come utilizzare il campo

1. All&#39;interno di questa cartella possono essere necessari i seguenti script:

   * Uno script di convalida client:
Il nome dello script è `clientvalidation.<extension>`, ad esempio `clientvalidation.jsp`
Viene richiamato quando viene eseguito il rendering del campo modulo. Può essere utilizzato per creare JavaScript client per convalidare il campo sul client.

   * Uno script di convalida server:
Il nome dello script è `servervalidation.<extension>`, ad esempio `servervalidation.jsp`
Viene richiamato all’invio del modulo. Può essere utilizzato per convalidare il campo sul server dopo l&#39;invio.

>[!NOTE]
>
>I vincoli di esempio sono elencati di seguito:
>
>`/libs/foundation/components/form/constraints`

#### Vincoli globali modulo {#form-global-constraints}

La convalida globale del modulo viene specificata configurando un tipo di risorsa nel componente Modulo iniziale ( `validationRT`). Esempio:

`apps/myProject/components/form/validation`

Potete quindi definire:

* a `clientvalidation.jsp` - iniettato dopo gli script di convalida client del campo
* e un `servervalidation.jsp` - chiamato anche dopo la convalida del singolo server di campi su un `POST`.

### Visualizzazione e disattivazione dei componenti del modulo {#showing-and-hiding-form-components}

È possibile configurare il modulo in modo da mostrare o nascondere i componenti in base al valore di altri campi del modulo.

La modifica della visibilità di un campo modulo è utile se il campo è richiesto solo in presenza di particolari condizioni. Ad esempio, in un modulo di feedback, può essere presente una domanda che chiede al cliente se desidera ricevere per e-mail informazioni sui prodotti. Se il cliente risponde Sì, compare un campo di testo per l’inserimento dell’indirizzo e-mail.

Utilizzare la finestra di dialogo **Modifica regole mostra/nascondi** per specificare le condizioni in cui un componente del modulo viene visualizzato o nascosto.

![showhideeditor](assets/showhideeditor.png)

Utilizzate i campi nella parte superiore della finestra di dialogo per specificare le seguenti informazioni:

* Se si specificano le condizioni per nascondere o mostrare il componente.
* Se qualsiasi o tutte le condizioni devono essere soddisfatte per mostrare o nascondere il componente.

Una o più condizioni vengono visualizzate al di sotto di questi campi. Una condizione prevede il confronto del valore di un altro componente (dello tesso modulo) con un particolare valore. Se il valore effettivo inserito nel campo soddisfa la condizione, questa viene considerata true (vera). Le condizioni includono le seguenti informazioni:

* Il Titolo del campo che si sta verificando.
* Un operatore.
* Un valore rispetto al quale viene confrontato il valore del campo.

Ad esempio, un componente Gruppo pulsanti di scelta con il titolo `Receive email notifications?`* * contiene i pulsanti di scelta `Yes` e `No`. Un componente Campo di testo con il titolo di `Email Address` utilizza la seguente condizione in modo che sia visibile se è selezionato `Yes`:

![showhidecondition](assets/showhidecondition.png)

In Javascript, per fare riferimento ai campi, nelle condizioni viene utilizzato il valore della proprietà Nome elemento. Nell&#39;esempio precedente, la proprietà Nome elemento del componente Gruppo pulsanti di scelta è `contact`. Il seguente codice rappresenta il codice JavaScript per questo esempio:

`((contact == "Yes"))`

**Per visualizzare o nascondere un componente modulo:**

1. Modificare il componente modulo specifico.

1. Selezionare **Mostra/Nascondi** per aprire la finestra di dialogo **Modifica Mostra/Nascondi regole**:

   * Nel primo elenco a discesa, selezionare **Mostra** o **Nascondi** per specificare se le condizioni determinano se mostrare o nascondere il componente.

   * Nell&#39;elenco a discesa alla fine della riga superiore, seleziona:

      * **all** - se tutte le condizioni devono essere soddisfatte per mostrare o nascondere il componente
      * **any** - se solo una o più condizioni devono essere soddisfatte per mostrare o nascondere il componente
   * Nella riga condizione (una è presentata come impostazione predefinita), selezionate un componente, un operatore e specificate un valore.
   * Se necessario, aggiungere altre condizioni facendo clic su **Aggiungi condizione**.

   Esempio:

   ![chlimage_1-9](assets/chlimage_1-9.png)

1. Fare clic su **OK** per salvare la definizione.

1. Dopo aver salvato la definizione, accanto all&#39;opzione **Mostra/Nascondi** nelle proprietà del componente modulo viene visualizzato un collegamento **Modifica regole**. Fare clic su questo collegamento per aprire la finestra di dialogo **Modifica Mostra/Nascondi regole** per apportare le modifiche.

   Fare clic su **OK** per salvare tutte le modifiche.

   ![chlimage_1-10](assets/chlimage_1-10.png)

   >[!CAUTION]
   >
   >Gli effetti delle definizioni Mostra/Nascondi possono essere visti e testati:
   >
   >
   >
   >    * in modalità **Anteprima** nell’ambiente di authoring (per la prima volta che si passa all’anteprima, è necessario ricaricare la pagina)
      >
      >    
   * sull’ambiente di pubblicazione


#### Gestione dei riferimenti di componenti interrotti {#handling-broken-component-references}

Per le condizioni mostra/nascondi viene utilizzato il valore della proprietà Nome elemento per fare riferimento ad altri componenti del modulo. La configurazione Mostra/Nascondi non è valida se una delle condizioni fa riferimento a un componente eliminato o per il quale è stata modificata la proprietà Nome elemento. Se si verifica questa situazione, è necessario aggiornare manualmente le condizioni; in caso contrario si verificherà un errore durante il caricamento del modulo.

Se la configurazione Mostra/Nascondi non è valida, la configurazione viene fornita solo come codice JavaScript. Modificate il codice per correggere i problemi. Nel codice viene usata la proprietà Nome elemento impostata originariamente per fare riferimento ai componenti.

### Sviluppo di script da utilizzare con Forms {#developing-scripts-for-use-with-forms}

Per ulteriori informazioni sugli elementi API utilizzabili per la scrittura di script, vedere gli [javadocs correlati a form](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/foundation/forms/package-summary.html).

È possibile utilizzare questa opzione per azioni quali la chiamata di un servizio prima dell&#39;invio del modulo e l&#39;annullamento del servizio in caso di errore:

* Definire il tipo di risorsa di convalida
* Includere uno script per la convalida:

   * In JSP, richiamare il servizio Web e creare un oggetto `com.day.cq.wcm.foundation.forms.ValidationInfo` contenente i messaggi di errore. Se si verificano degli errori, i dati del modulo non verranno inviati.
