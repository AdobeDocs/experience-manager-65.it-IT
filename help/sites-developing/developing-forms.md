---
title: Sviluppo di Forms (interfaccia classica)
seo-title: Developing Forms (Classic UI)
description: Scopri come sviluppare moduli per l’interfaccia classica di Adobe Experience Manager
seo-description: Learn how to develop forms
uuid: 33859f29-edc5-4bd5-a634-35549f3b5ccf
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 6ee3bd3b-51d1-462f-b12e-3cbe24898b85
docset: aem65
exl-id: f43e9491-aa8f-40af-9800-123695142559
source-git-commit: b703f356f9475eeeafb1d5408c650d9c6971a804
workflow-type: tm+mt
source-wordcount: '1953'
ht-degree: 0%

---

# Sviluppo di Forms (interfaccia classica){#developing-forms-classic-ui}

La struttura di base di un modulo è la seguente:

* Inizio modulo
* Elementi modulo
* Fine modulo

Tutti questi elementi vengono realizzati con una serie di impostazioni predefinite [Componenti del modulo](/help/sites-authoring/default-components.md#form), disponibile in un&#39;installazione standard per AEM.

Oltre a [sviluppo di nuovi componenti](/help/sites-developing/developing-components-samples.md) per l&#39;utilizzo nei moduli è inoltre possibile:

* [Precarica il modulo con i valori](#preloading-form-values)
* [Precarica (determinati) campi con più valori](#preloading-form-fields-with-multiple-values)
* [Sviluppare nuove azioni](#developing-your-own-form-actions)
* [Sviluppare nuovi vincoli](#developing-your-own-form-constraints)
* [Mostrare o nascondere campi modulo specifici](#showing-and-hiding-form-components)

[Utilizzo degli script](#developing-scripts-for-use-with-forms) per estendere la funzionalità, se necessario.

>[!NOTE]
>
>Questo documento si concentra sullo sviluppo di moduli utilizzando [Componenti di base](/help/sites-authoring/default-components-foundation.md) nell’interfaccia classica. L’Adobe consiglia di sfruttare il nuovo [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) e [Nascondi condizioni](/help/sites-developing/hide-conditions.md) per lo sviluppo di moduli nell’interfaccia utente touch.

## Precaricamento dei valori modulo {#preloading-form-values}

Il componente di inizio modulo fornisce un campo per **Percorso di caricamento**: percorso facoltativo che punta a un nodo nell’archivio.

Il percorso di caricamento è il percorso delle proprietà del nodo utilizzato per caricare valori predefiniti in più campi del modulo.

Questo è un campo facoltativo che specifica il percorso di un nodo nell’archivio. Se le proprietà di questo nodo corrispondono ai nomi dei campi, i campi appropriati del modulo vengono precaricati con il valore di tali proprietà. Se non esiste alcuna corrispondenza, il campo contiene il valore predefinito.

>[!NOTE]
>
>A [azione modulo](#developing-your-own-form-actions) può anche impostare la risorsa da cui caricare i valori iniziali. Questa operazione viene eseguita utilizzando `FormsHelper#setFormLoadResource` interno `init.jsp`.
>
>Solo se non è impostato, il modulo verrà popolato dal percorso impostato nel componente modulo iniziale dall’autore.

### Precaricamento dei campi modulo con più valori {#preloading-form-fields-with-multiple-values}

Vari campi del modulo presentano anche **Percorso di caricamento elementi**, di nuovo un percorso facoltativo che punta a un nodo nell’archivio.

Il **Percorso di caricamento elementi** è il percorso delle proprietà del nodo utilizzato per caricare valori predefiniti in quel campo specifico del modulo, ad esempio [elenco a discesa](/help/sites-authoring/default-components-foundation.md#dropdown-list), [gruppo di caselle di controllo](/help/sites-authoring/default-components-foundation.md#checkbox-group) o [gruppo radio](/help/sites-authoring/default-components-foundation.md#radio-group).

#### Esempio: precaricamento di un elenco a discesa con più valori {#example-preloading-a-dropdown-list-with-multiple-values}

È possibile configurare un elenco a discesa con l’intervallo di valori desiderato.

Il **Percorso di caricamento elementi** può essere utilizzato per accedere a un elenco da una cartella nel repository e precaricarli nel campo:

1. Crea una nuova cartella Sling ( `sling:Folder`) ad esempio, `/etc/designs/<myDesign>/formlistvalues`

1. Aggiungi una nuova proprietà (ad esempio, `myList`) di tipo stringa con più valori ( `String[]`) per contenere l&#39;elenco degli elementi a discesa. Il contenuto può essere importato anche utilizzando uno script, ad esempio con uno script JSP o cURL in uno script shell.

1. Utilizza il percorso completo in **Percorso di caricamento elementi** campo: ad esempio, `/etc/designs/geometrixx/formlistvalues/myList`

Tieni presente che se i valori in `String[]` sono dei formattati come segue:

* `AL=Alabama`
* `AK=Alaska`
* ecc.

l’AEM genererà l’elenco come:

* `<option value="AL">Alabama</option>`
* `<option value="AK">Alaska</option>`

Questa funzione può, ad esempio, essere utilizzata in un ambiente multilingue.

### Sviluppo di azioni personalizzate per i moduli {#developing-your-own-form-actions}

Un modulo richiede un&#39;azione. Un&#39;azione definisce l&#39;operazione eseguita quando il modulo viene inviato con i dati utente.

Una serie di azioni è fornita con un impianto AEM standard, come si può vedere in:

`/libs/foundation/components/form/actions`

e nella **Tipo di azione** elenco dei **Modulo** componente:

![chlimage_1-8](assets/chlimage_1-8.png)

In questa sezione viene illustrato come sviluppare un&#39;azione modulo personalizzata da includere nell&#39;elenco.

Puoi aggiungere una tua azione in `/apps` come segue:

1. Creare un nodo di tipo `sling:Folder`. Specifica un nome che rifletta l’azione da implementare.

   Ad esempio:

   `/apps/myProject/components/customFormAction`

1. Su questo nodo definisci le seguenti proprietà, quindi fai clic su **Salva tutto** per mantenere le modifiche:

   * `sling:resourceType` - imposta come `foundation/components/form/action`

   * `componentGroup` - definisci come `.hidden`

   * Facoltativamente:

      * `jcr:title` : specifica un titolo che verrà visualizzato nell’elenco a discesa di selezione. Se non è impostato, viene visualizzato il nome del nodo

      * `jcr:description` - immettere una descrizione di propria scelta

1. Nella cartella crea un nodo di dialogo:

   1. Aggiungi i campi in modo che l’autore possa modificare la finestra di dialogo dei moduli una volta scelta l’azione.

1. Nella cartella crea:

   1. Uno script post.
Il nome dello script è `post.POST.<extension>`ad esempio: `post.POST.jsp`
Lo script post viene richiamato quando un modulo viene inviato per elaborare il modulo, contiene il codice che gestisce i dati provenienti dal modulo `POST`.

   1. Aggiungi uno script di inoltro che viene richiamato al momento dell’invio del modulo.
Il nome dello script è `forward.<extension`>, ad esempio `forward.jsp`
Questo script può definire un percorso. La richiesta corrente viene quindi inoltrata al percorso specificato.

   La chiamata necessaria è `FormsHelper#setForwardPath` (2 varianti). Un caso tipico è quello di eseguire una convalida, o logica, per trovare il percorso di destinazione e quindi inoltrarlo a tale percorso, consentendo al servlet Sling POST predefinito di eseguire l’archiviazione effettiva in JCR.

   Potrebbe anche essere presente un altro servlet che esegue l’elaborazione effettiva, in questo caso l’azione modulo e `forward.jsp` fungerebbe solo da codice &quot;colla&quot;. Un esempio è l’azione e-mail in `/libs/foundation/components/form/actions/mail`, che inoltra i dettagli a `<currentpath>.mail.html`posizione di un servlet di posta.

   Quindi:

   * a `post.POST.jsp` è utile per piccole operazioni eseguite completamente dall&#39;azione stessa
   * mentre `forward.jsp` è utile quando è richiesta solo la delega.

   L’ordine di esecuzione per gli script è:

   * Al rendering del modulo ( `GET`):

      1. `init.jsp`
      1. per tutti i vincoli del campo: `clientvalidation.jsp`
      1. validationRT del modulo: `clientvalidation.jsp`
      1. il modulo viene caricato tramite la risorsa di caricamento se impostata
      1. `addfields.jsp` durante il rendering interno `<form></form>`

   * durante la gestione di un modulo `POST`:

      1. `init.jsp`
      1. per tutti i vincoli del campo: `servervalidation.jsp`
      1. validationRT del modulo: `servervalidation.jsp`
      1. `forward.jsp`
      1. se è stato impostato un percorso di inoltro ( `FormsHelper.setForwardPath`), inoltra la richiesta, quindi chiama `cleanup.jsp`

      1. se non è stato impostato alcun percorso di inoltro, invoca `post.POST.jsp` (termina qui, no `cleanup.jsp` chiamato)

1. Sempre nella cartella, se lo desideri, aggiungi:

   1. Script per l’aggiunta di campi.
Il nome dello script è `addfields.<extension>`ad esempio: `addfields.jsp`
Un `addfields` lo script viene richiamato immediatamente dopo la scrittura del HTML per l&#39;inizio del modulo. Questo consente all’azione di aggiungere campi di input personalizzati o altri HTML di questo tipo all’interno del modulo.

   1. Uno script di inizializzazione.
Il nome dello script è `init.<extension>`ad esempio: `init.jsp`
Questo script viene richiamato al momento del rendering del modulo. Può essere utilizzato per inizializzare le specifiche dell’azione.

   1. Uno script di pulizia.
Il nome dello script è `cleanup.<extension>`ad esempio: `cleanup.jsp`
Questo script può essere utilizzato per eseguire la pulizia.

1. Utilizza il **Forms** componente in un parsys. Il **Tipo di azione** Il menu a discesa includerà ora la nuova azione.

   >[!NOTE]
   >
   >Per visualizzare le azioni predefinite che fanno parte del prodotto:
   >
   >
   >`/libs/foundation/components/form/actions`

### Sviluppo di vincoli di modulo personalizzati {#developing-your-own-form-constraints}

I vincoli possono essere imposti a due livelli:

* Per [singoli campi (vedere la procedura seguente)](#constraints-for-individual-fields)
* As [convalida globale del modulo](#form-global-constraints)

#### Vincoli per singoli campi {#constraints-for-individual-fields}

È possibile aggiungere vincoli personalizzati per un singolo campo (in `/apps`) come segue:

1. Creare un nodo di tipo `sling:Folder`. Specificare un nome che rifletta il vincolo da implementare.

   Ad esempio:

   `/apps/myProject/components/customFormConstraint`

1. Su questo nodo definisci le seguenti proprietà, quindi fai clic su **Salva tutto** per mantenere le modifiche:

   * `sling:resourceType` - impostato su `foundation/components/form/constraint`

   * `constraintMessage` - un messaggio personalizzato che verrà visualizzato se il campo non è valido, in base al vincolo, al momento dell’invio del modulo

   * Facoltativamente:

      * `jcr:title` : specifica un titolo desiderato, da visualizzare nell’elenco di selezione. Se non è impostato, viene visualizzato il nome del nodo
      * `hint` - ulteriori informazioni, destinate all&#39;utente, su come utilizzare il campo

1. All&#39;interno di questa cartella, possono essere necessari i seguenti script:

   * Uno script di convalida client: il nome dello script è `clientvalidation.<extension>`ad esempio: `clientvalidation.jsp`
Viene richiamato quando viene eseguito il rendering del campo modulo. Può essere utilizzato per creare JavaScript client per convalidare il campo sul client.

   * Uno script di convalida del server: il nome dello script è `servervalidation.<extension>`ad esempio: `servervalidation.jsp`
Viene richiamato al momento dell’invio del modulo. Può essere utilizzato per convalidare il campo sul server dopo l’invio.

>[!NOTE]
>
>I vincoli di esempio sono disponibili in:
>
>`/libs/foundation/components/form/constraints`

#### Vincoli globali del modulo {#form-global-constraints}

La convalida globale del modulo viene specificata configurando un tipo di risorsa nel componente modulo iniziale ( `validationRT`). Ad esempio:

`apps/myProject/components/form/validation`

Puoi quindi definire:

* a `clientvalidation.jsp` : inserito dopo gli script di convalida client del campo
* e un `servervalidation.jsp` - chiamato anche dopo le convalide dei singoli server di campo su un `POST`.

### Mostrare e nascondere i componenti del modulo {#showing-and-hiding-form-components}

È possibile configurare il modulo in modo da mostrare o nascondere i componenti del modulo in base al valore degli altri campi del modulo.

La modifica della visibilità di un campo modulo è utile quando il campo è necessario solo in determinate condizioni. Ad esempio, in un modulo di feedback, una domanda chiede ai clienti se desiderano ricevere informazioni sui prodotti tramite e-mail. Selezionando sì, viene visualizzato un campo di testo che consente al cliente di digitare il proprio indirizzo e-mail.

Utilizza il **Modifica Regole Mostra/Nascondi** per specificare le condizioni in cui un componente modulo viene visualizzato o nascosto.

![showhideeditor](assets/showhideeditor.png)

Utilizzare i campi nella parte superiore della finestra di dialogo per specificare le informazioni seguenti:

* Indica se si stanno specificando le condizioni per nascondere o visualizzare il componente.
* Indica se una o tutte le condizioni devono essere true per mostrare o nascondere il componente.

Sotto questi campi vengono visualizzate una o più condizioni. Una condizione confronta il valore di un altro componente del modulo (nello stesso modulo) con un valore. Se il valore effettivo nel campo soddisfa la condizione, la condizione restituisce true. Le condizioni includono le seguenti informazioni:

* Titolo del campo modulo che viene testato.
* Un operatore.
* Viene confrontato un valore con il valore del campo.

Ad esempio, un componente Gruppo pulsanti di scelta con il titolo `Receive email notifications?`* * contiene `Yes` e `No` pulsanti di scelta. Un componente Campo di testo con il titolo `Email Address` utilizza la seguente condizione per essere visibile se `Yes` è selezionato:

![showhidecondition](assets/showhidecondition.png)

In JavaScript, le condizioni utilizzano il valore della proprietà Nome elemento per fare riferimento ai campi. Nell&#39;esempio precedente, la proprietà Nome elemento del componente Gruppo pulsanti di scelta è `contact`. Il codice seguente è il codice JavaScript equivalente per tale esempio:

`((contact == "Yes"))`

**Per mostrare o nascondere un componente modulo:**

1. Modifica il componente modulo specifico.

1. Seleziona **Mostra/Nascondi** per aprire **Modifica regole Mostra/Nascondi** finestra di dialogo:

   * Nel primo elenco a discesa, seleziona **Spettacolo** o **Nascondi** per specificare se le condizioni determinano se mostrare o nascondere il componente.

   * Nell’elenco a discesa alla fine della riga superiore, seleziona:

      * **tutto** - se tutte le condizioni devono essere true per mostrare o nascondere il componente
      * **qualsiasi** - se solo una o più condizioni devono essere soddisfatte per mostrare o nascondere il componente

   * Nella riga della condizione, visualizzata come predefinita, selezionare un componente, un operatore e quindi specificare un valore.
   * Se necessario, aggiungi altre condizioni facendo clic su **Aggiungi condizione**.

   Ad esempio:

   ![chlimage_1-9](assets/chlimage_1-9.png)

1. Clic **OK** per salvare la definizione.

1. Dopo aver salvato la definizione, **Modifica regole** viene visualizzato accanto al **Mostra/Nascondi** nelle proprietà del componente modulo. Fai clic su questo collegamento per aprire **Modifica regole Mostra/Nascondi** per apportare modifiche.

   Clic **OK** per salvare tutte le modifiche.

   ![chlimage_1-10](assets/chlimage_1-10.png)

   >[!CAUTION]
   >
   >Gli effetti delle definizioni Mostra/Nascondi possono essere visualizzati e testati:
   >
   >* in **Anteprima** modalità nell’ambiente di authoring (richiede un ricaricamento della pagina al primo passaggio all’anteprima)
   >
   >* sull’ambiente di pubblicazione

#### Gestione dei riferimenti ai componenti interrotti {#handling-broken-component-references}

Le condizioni Show/hide utilizzano il valore della proprietà Element Name per fare riferimento ad altri componenti del modulo. La configurazione Mostra/Nascondi non è valida quando una delle condizioni fa riferimento a un componente eliminato o la cui proprietà Nome elemento è stata modificata. Quando si verifica questa situazione, è necessario aggiornare manualmente le condizioni o si verifica un errore durante il caricamento del modulo.

Quando la configurazione Mostra/Nascondi non è valida, viene fornita solo come codice JavaScript. Modifica il codice per risolvere i problemi. Il codice utilizza la proprietà Nome elemento utilizzata in origine per fare riferimento ai componenti.

### Sviluppo di script da utilizzare con Forms {#developing-scripts-for-use-with-forms}

Per ulteriori informazioni sugli elementi API che possono essere utilizzati durante la scrittura di script, vedi [javadoc relativi ai moduli](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/foundation/forms/package-summary.html).

È possibile utilizzarlo per azioni quali la chiamata di un servizio prima dell’invio del modulo e l’annullamento del servizio in caso di errore:

* Definire il tipo di risorsa di convalida
* Includi uno script per la convalida:

   * Nella JSP, chiama il servizio web e crea un’ `com.day.cq.wcm.foundation.forms.ValidationInfo` oggetto contenente i messaggi di errore. In caso di errori, i dati del modulo non verranno registrati.
