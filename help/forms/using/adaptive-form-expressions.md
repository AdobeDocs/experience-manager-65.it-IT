---
title: Espressioni dei moduli adattivi
seo-title: Adaptive Form Expressions
description: Utilizzare espressioni di moduli adattivi per aggiungere la convalida, il calcolo e la visibilità automatica di una sezione attiva o disattivata.
seo-description: Use adaptive forms expressions to add automatic validation, calculation, and turn visibility of a section on or off.
uuid: c274dce5-8b87-472f-bff5-53b246fa6584
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 2fd2276e-cfe3-47ad-94c1-9c7af56b7a17
docset: aem65
feature: Adaptive Forms
exl-id: 048bd9e8-ef34-40fb-9f46-73743d7b47c8
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2746'
ht-degree: 0%

---

# Espressioni dei moduli adattivi{#adaptive-form-expressions}

I moduli adattivi forniscono agli utenti finali con capacità di scripting dinamiche un’esperienza di compilazione dei moduli ottimizzata e semplificata. Consente di scrivere espressioni per aggiungere vari comportamenti, ad esempio campi e pannelli dinamici Mostra/Nascondi. Consente inoltre di aggiungere campi calcolati, rendere i campi di sola lettura, aggiungere logica di convalida e molto altro. Il comportamento dinamico si basa sull’input dell’utente o sui dati precompilati.

JavaScript è il linguaggio di espressione dei moduli adattivi. Tutte le espressioni sono espressioni JavaScript valide e utilizzano API modello di script per moduli adattivi. Queste espressioni restituiscono valori di determinati tipi. Per l’elenco completo delle classi, degli eventi, degli oggetti e delle API pubbliche dei moduli adattivi, consulta [Riferimento API della libreria JavaScript per i moduli adattivi](https://helpx.adobe.com/experience-manager/6-5/forms/javascript-api/index.html).

## Best practice per la scrittura di espressioni {#best-practices-for-writing-expressions}

* Durante la scrittura di espressioni, per accedere a campi e pannelli è possibile utilizzare il nome del campo o del pannello. Per accedere al valore di un campo, utilizzare la proprietà value . Esempio, `field1.value`
* Utilizzare nomi univoci per campi e pannelli in tutto il modulo. Consente di evitare eventuali conflitti con i nomi di campo utilizzati durante la scrittura di espressioni.
* Durante la scrittura di espressioni con più righe, utilizzare un punto e virgola per terminare un&#39;istruzione.

## Procedure consigliate per le espressioni che coinvolgono il pannello ripetuto {#best-practices-for-expressions-involving-repeating-panel}

I pannelli ripetuti sono istanze di un pannello che viene aggiunto o rimosso dinamicamente utilizzando API di script o dati precompilati. Per informazioni dettagliate sull&#39;utilizzo del pannello ripetuto, vedere [creazione di moduli con sezioni ripetibili](/help/forms/using/creating-forms-repeatable-sections.md).

* Per creare un pannello ripetuto, nella finestra di dialogo del pannello aprire le impostazioni e impostare il valore del campo conteggio massimo su più di 1.
* Il valore del conteggio minimo delle impostazioni di ripetizione del pannello può essere uno o più ma non può essere più del valore del conteggio massimo.
* Quando un&#39;espressione fa riferimento a un campo di un pannello ripetuto, i nomi di campo nell&#39;espressione vengono risolti nell&#39;elemento ripetuto più vicino.
* I moduli adattivi offrono alcune funzioni speciali per semplificare il calcolo per pannelli ripetibili quali somma, conteggio, min, max, filtro e molto altro. Per l&#39;elenco completo delle funzioni, vedi [Riferimento API della libreria JavaScript per i moduli adattivi](https://helpx.adobe.com/aem-forms/6/javascript-api/af.html)
* Le API per la manipolazione delle istanze di un pannello ripetuto sono:

   * Per aggiungere un’istanza di un pannello: `panel1.instanceManager.addInstance()`
   * Per ottenere un indice di ripetizione del pannello: `panel1.instanceIndex`
   * Per ottenere instanceManager di un pannello: `_panel1 or panel1.instanceManager`
   * Per rimuovere un’istanza di un pannello: `_panel1.removeInstance(panel1.instanceIndex)`

## Tipi di espressione {#expression-types}

Nei moduli adattivi è possibile scrivere espressioni per aggiungere comportamenti quali campi e pannelli dinamici Mostra/Nascondi. È inoltre possibile scrivere espressioni per aggiungere campi calcolati, rendere i campi di sola lettura, la logica di convalida e molto altro ancora. I moduli adattivi supportano le seguenti espressioni:

* **[Espressioni di accesso](#access-expression-enablement-expression)**: per abilitare/disabilitare un campo.
* **[Calcolare espressioni](#calculate-expression)**: per calcolare automaticamente il valore di un campo.
* **[Espressione clic](#click-expression)**: per gestire le azioni in caso di clic su un pulsante.
* **[Script di inizializzazione](#initialization-script):** eseguire un&#39;azione all&#39;inizializzazione di un campo.
* **[Espressione Options](#options-expression)**: per compilare dinamicamente un elenco a discesa.
* **[Espressione di riepilogo](#summary)**: per calcolare dinamicamente il titolo di un pannello a soffietto.
* **[Convalidare espressioni](#validate-expression)**: per convalidare un campo.
* **[Script di commit dei valori](#value-commit-script):** per modificare i componenti di un modulo dopo la modifica del valore di un campo.
* **[Espressione di visibilità](#visibility-expression)**: per controllare la visibilità di un campo e di un pannello.
* **[Espressione completamento passaggio](#step-completion-expression)**: per evitare che un utente passi al passaggio successivo di una procedura guidata.

### Espressione di accesso (espressione di abilitazione) {#access-expression-enablement-expression}

Puoi utilizzare l’espressione di accesso per abilitare o disabilitare un campo. Se l&#39;espressione utilizza il valore di un campo, ogni volta che il valore del campo cambia l&#39;espressione viene riattivata.

**Si applica a**: field

**Tipo di ritorno**: L&#39;espressione restituisce un valore booleano che indica se il campo è abilitato o disabilitato. **true** rappresenta che il campo è abilitato e **false** rappresenta il campo disabilitato.

**Esempio**: Per abilitare un campo solo quando il valore di **field1** è impostato su **X**, l&#39;espressione di accesso è: `field1.value == "X"`

### Calcola espressione {#calculate-expression}

L&#39;espressione calculate viene utilizzata per calcolare automaticamente il valore di un campo utilizzando un&#39;espressione. In genere, tale espressione utilizza la proprietà value di un altro campo. Esempio, `field2.value + field3.value`. Ogniqualvolta il valore del `field2`o `field3`cambia, l&#39;espressione viene riattivata e il valore viene ricalcolato.

**Si applica a**: field

**Tipo di ritorno**: L&#39;espressione restituisce un valore compatibile con il campo in cui viene visualizzato il risultato dell&#39;espressione (ad esempio, decimale).

**Esempio**: L&#39;espressione calculate per visualizzare la somma di due campi in **field1** è:
`field2.value + field3.value`

### Espressione di clic {#click-expression}

L&#39;espressione click gestisce le azioni eseguite sull&#39;evento click di un pulsante. Con GuideBridge è possibile eseguire varie funzioni, ad esempio inviare, convalidare e utilizzare l’espressione di clic. Per un elenco completo delle API, vedi [API di GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html).

**Si applica a**: Campi pulsante

**Tipo di ritorno**: L&#39;espressione click non restituisce alcun valore. Se un&#39;espressione restituisce un valore, il valore viene ignorato.

**Esempio**: Compilazione di una casella di testo **textbox1** sull’azione di clic di un pulsante con valore **AEM Forms**, l’espressione di clic del pulsante è `textbox1.value="AEM Forms"`

### Script di inizializzazione {#initialization-script}

Lo script di inizializzazione viene attivato quando viene inizializzato un modulo adattivo. A seconda degli scenari, lo script di inizializzazione si comporta nel modo seguente:

* Quando si esegue il rendering di un modulo adattivo senza precompilazione dei dati, lo script di inizializzazione viene eseguito dopo l&#39;inizializzazione del modulo.
* Quando viene eseguito il rendering di un modulo adattivo con una precompilazione dei dati, lo script viene eseguito al termine dell&#39;operazione di precompilazione.
* Quando si attiva la riconvalida lato server di un modulo adattivo, viene eseguito lo script di inizializzazione.

**Si applica a:** campi e pannelli

**Tipo di ritorno:** L&#39;espressione script di inizializzazione non restituisce alcun valore. Se un&#39;espressione restituisce un valore, il valore viene ignorato.

**Esempio:** In uno scenario di precompilazione dei dati, per compilare i campi con il valore predefinito `'Adaptive Forms'` quando il loro valore viene salvato come nullo, l&#39;espressione dello script di inizializzazione è:
`if(this.value==null) this.value='Adaptive Forms';`

### Espressione Opzioni {#options-expression}

L&#39;espressione options viene utilizzata per compilare dinamicamente le opzioni di un campo elenco a discesa.

**Si applica a**: campi elenco a discesa

**Tipo di ritorno**: L&#39;espressione options restituisce una matrice di valori stringa. Ogni valore può essere una stringa semplice, ad esempio **Maschio** o in un formato di coppia key=value, ad esempio **1=Maschio**

**Esempio**: Per compilare il valore di un campo, in base al valore di un altro campo, fornire un&#39;espressione di opzioni semplici. Ad esempio, per compilare un campo, **Numero di bambini**, in base **Stato civile** espresso in un altro campo, l’espressione è:

**`marital_status.value == "married" ? ["1=One", "2=two"] : ["0=Zero"]`.**

Ogni volta che il valore di **marital_status** cambia campo, l’espressione viene riattivata. Puoi anche compilare il menu a discesa da un servizio REST. Per informazioni dettagliate, consulta [Compilazione dinamica di elenchi a discesa](../../forms/using/dynamically-populate-dropdowns.md).

### Espressione di riepilogo {#summary}

L&#39;espressione Summary calcola dinamicamente il titolo di un pannello secondario di un pannello di layout a soffietto. È possibile specificare l&#39;espressione Summary in una regola che utilizza un campo modulo o una logica personalizzata per valutare il titolo. L&#39;espressione viene eseguita quando il modulo viene inizializzato. Se si sta precompilando un modulo, l’espressione viene eseguita dopo la precompilazione dei dati o quando viene modificato il valore dei campi dipendenti utilizzati nell’espressione.

L’espressione Riepilogo viene in genere utilizzata per gli elementi secondari ripetuti di un pannello di layout a soffietto per fornire un titolo significativo a ciascun pannello secondario.

**Si applica a:** Pannelli figli diretti di un pannello il cui layout è configurato come pannello a soffietto.

**Tipo di ritorno:** L&#39;espressione restituisce un elemento String che diventa il titolo del pannello a soffietto.

**Esempio:** &quot;Numero di conto: &quot; + textbox1.value

### Convalida espressione {#validate-expression}

L’espressione validate viene utilizzata per convalidare i campi utilizzando l’espressione specificata. In genere, tali espressioni utilizzano espressioni regolari insieme al valore del campo per convalidare un campo. L’espressione viene riattivata e lo stato di convalida del campo viene ricalcolato in caso di modifica del valore di un campo.

**Si applica a**: field

**Tipo di ritorno**: L&#39;espressione restituisce un valore booleano che rappresenta lo stato di convalida del campo. Il valore **false** rappresenta che il campo non è valido e **true** rappresenta la validità del campo.
**Esempio**: Per un campo che rappresenta il codice postale del Regno Unito, l&#39;espressione di convalida è:

(**this.value** &amp;&amp; `this.value.match(/^(GIR 0AA|[A-Z]{1,2}\d[A-Z0-9]? ?[0-9][A-Z]{2}\s*)$/i) == null) ? false : true`

Nell&#39;esempio precedente, se il valore non vuoto non corrisponde al pattern, l&#39;espressione restituisce **false** per indicare che il campo non è valido.

>[!NOTE]
>
>Se si scrive un&#39;espressione di convalida per un campo non obbligatorio o obbligatorio, l&#39;espressione viene valutata indipendentemente dallo stato di visibilità del campo. Per interrompere la convalida dei campi nascosti, impostare la proprietà validationsDisabled nello script di inizializzazione o di conferma del valore su true. Esempio, `this.validationsDisabled=true`

### Script per conferma del valore {#value-commit-script}

Lo script Value Commit viene attivato quando:

* Un utente modifica il valore di un campo dall’interfaccia utente.
* Il valore di un campo cambia a livello di programmazione a causa di una modifica in un altro campo.

**Si applica a:** field

**Tipo di ritorno:** L&#39;espressione script di commit del valore non restituisce alcun valore. Se un&#39;espressione restituisce un valore, il valore viene ignorato.

**Esempio:** Per convertire il caso degli alfabeti immessi nel campo in maiuscolo al momento del commit, il valore dell&#39;espressione commit è:
`this.value=this.value.toUpperCase()`

>[!NOTE]
>
>È possibile disattivare l’esecuzione dello script di commit dei valori quando il valore di un campo viene modificato a livello di programmazione. Per farlo, vai su https://&#39;[server]:[porta]&#39;/system/console/configMgr e modifica **Versione Forms adattiva per la compatibilità** a **AEM Forms 6.1**. Successivamente, lo script di commit dei valori viene eseguito solo quando l&#39;utente modifica il valore del campo dall&#39;interfaccia utente.

### Espressione di visibilità {#visibility-expression}

L’espressione Visibilità viene utilizzata per controllare la visibilità del campo o del pannello. In genere, l&#39;espressione di visibilità utilizza la proprietà value di un campo e viene riattivata ogni volta che tale valore cambia.

**Si applica a**: campi e pannelli

**Tipo di ritorno**: L&#39;espressione restituisce un valore booleano che rappresenta il campo o il pannello visibile o meno. **false** indica che il campo o il pannello non è visibile e che il valore true rappresenta che il campo o il pannello è visibile.

**Esempio**: Per un pannello che diventa visibile solo se il valore di **field1** è impostato su **Maschio**, l’espressione di visibilità è: `field1.value == "Male"`

### Espressione completamento passaggio {#step-completion-expression}

L&#39;espressione completamento passaggi viene utilizzata per impedire all&#39;utente di passare al passaggio successivo di un layout della procedura guidata. Queste espressioni vengono utilizzate quando i pannelli dispongono di un layout guidato (moduli con più passaggi che mostrano un passaggio alla volta). L’utente può passare al passaggio successivo, al pannello o alla sottosezione solo se tutti i valori richiesti nella sezione corrente sono riempiti e validi.

**Si applica a**: Pannelli con layout di elemento impostato sulla procedura guidata.

**Tipo di ritorno**: L&#39;espressione restituisce un valore booleano che rappresenta il pannello corrente valido o meno. **True** indica che il pannello corrente è valido e che l’utente può passare al pannello successivo.

**Esempio**: In un modulo organizzato in vari pannelli, prima di passare al pannello successivo viene convalidato il pannello corrente. In questi casi, vengono utilizzate le espressioni di completamento dei passaggi. In genere, queste espressioni utilizzano l’API di convalida GuideBridge. Un esempio di espressione di completamento del passaggio è:
`window.guideBridge.validate([],this.panel.navigationContext.currentItem.somExpression)`

## Convalida in modulo adattivo {#validations-in-adaptive-form}

Esistono diversi metodi per aggiungere la convalida dei campi a un modulo adattivo. Se in un campo viene aggiunto un controllo di convalida, **True** rappresenta che il valore immesso nel campo è valido. **False** rappresenta che il valore non è valido. Se passi il tasto Tab all’interno e all’esterno di un campo, il messaggio di errore non viene generato.

I metodi per aggiungere convalide a un campo sono i seguenti:

### Obbligatorio {#required}

Per rendere obbligatorio un componente, nella **Modifica** finestra di dialogo del componente, è possibile selezionare l’opzione **Titolo e testo > Obbligatorio**. È inoltre possibile aggiungere il **messaggio obbligatorio** (facoltativo). .

### Pattern di convalida {#validation-patterns}

Per un campo sono disponibili più pattern di convalida predefiniti. Per selezionare un pattern di convalida, nella **Modifica** finestra di dialogo del componente, individua il **Pattern** e seleziona **pattern**. È possibile creare un pattern di convalida personalizzato in un **Pattern** casella di testo. Viene restituito lo stato di convalida **True** solo se i dati compilati sono conformi al pattern di convalida, altrimenti **False** viene restituito . Per creare un pattern di convalida personalizzato, consultare [Supporto della clausola immagine per i moduli HTML5](/help/forms/using/picture-clause-support.md).

### Espressioni di convalida {#validation-expressions}

È inoltre possibile calcolare la convalida di un campo utilizzando espressioni in campi diversi. Queste espressioni sono scritte all&#39;interno di **Script di convalida** campo **Script** scheda di **Modifica** finestra di dialogo del componente. Lo stato di convalida di un campo dipende dal valore restituito dall’espressione. Per informazioni su come scrivere tali espressioni, consulta [Convalida espressione](../../forms/using/adaptive-form-expressions.md#p-validate-expression-p).

## Informazioni aggiuntive {#additional-information}

### Utilizzo del formato di visualizzazione dei campi {#using-field-display-format}

Il formato di visualizzazione può essere utilizzato per visualizzare i dati in diversi formati. Ad esempio, è possibile utilizzare il formato di visualizzazione per visualizzare un numero di telefono con trattini, formattare il codice postale o selezionare la data. Questi modelli di visualizzazione possono essere selezionati **Pattern** della finestra di dialogo Modifica di un componente. È possibile scrivere pattern di visualizzazione personalizzati simili ai pattern di convalida sopra menzionati.

### GuideBridge - API ed eventi {#guidebridge-apis-and-events}

GuideBridge è una raccolta di API che possono essere utilizzate per interagire con i moduli adattivi nel modello di memoria in un browser. Per un’introduzione dettagliata all’API Guide Bridge, ai metodi di classe, agli eventi esposti, vedi [Riferimento API della libreria JavaScript per i moduli adattivi](https://helpx.adobe.com/aem-forms/6/javascript-api/).

>[!NOTE]
>
>Si consiglia di non utilizzare i listener di eventi GuideBridge nelle espressioni.

#### Utilizzo di GuideBridge in varie espressioni {#guidebridge-usage-in-various-expressions}

* Per reimpostare i campi modulo, è possibile attivare `guideBridge.reset()` API sull’espressione di clic di un pulsante. Analogamente, esiste un’API di invio che può essere chiamata come espressione di clic `guideBridge.submit()`**.**

* È possibile utilizzare `setFocus()` API per impostare lo stato attivo su vari campi o pannelli (per lo stato attivo del pannello è impostato automaticamente sul primo campo). `setFocus()`offre un’ampia gamma di opzioni per la navigazione, ad esempio tra pannelli, attraversamento precedente/successivo, l’impostazione dello stato attivo su un particolare campo e molte altre ancora. Ad esempio, per passare al pannello successivo, puoi utilizzare: `guideBridge.setFocus(this.panel.somExpression, 'nextItem').`

* Per convalidare un modulo adattivo o i relativi pannelli specifici, utilizza `guideBridge.validate(errorList, somExpression).`

#### Utilizzo di GuideBridge all’esterno delle espressioni  {#using-guidebridge-outside-expressions-nbsp}

È inoltre possibile utilizzare le API GuideBridge al di fuori delle espressioni. Ad esempio, è possibile utilizzare l’API GuideBridge per impostare la comunicazione tra il HTML di pagina che ospita il modulo adattivo e il modello di modulo. Inoltre, è possibile impostare il valore proveniente dall’elemento padre di Iframe che ospita il modulo.

Per utilizzare l’API GuideBridge per l’esempio precedente, acquisire un’istanza di GuideBridge. Per acquisire l&#39;istanza, ascolta `bridgeInitializeStart`evento `window`oggetto:

```javascript
window.addEventListener("bridgeInitializeStart", function(evnt) {

     // get hold of the guideBridge object

     var gb = evnt.detail.guideBridge;

     //wait for the completion of AF

     gb.connect(function (){

        //this function will be called after Adaptive Form is initialized

     })

})
```

>[!NOTE]
>
>In AEM, è buona prassi scrivere il codice in un clientLib e includerlo nella pagina (header.jsp o footer.jsp della pagina)

Per utilizzare GuideBridge dopo l’inizializzazione del modulo (il `bridgeInitializeComplete` viene inviato l&#39;evento), ottieni l&#39;istanza GuideBridge utilizzando `window.guideBridge`. È possibile controllare lo stato di inizializzazione di GuideBridge utilizzando `guideBride.isConnected` API.

#### Eventi GuideBridge {#guidebridge-events}

GuideBridge fornisce inoltre alcuni eventi per gli script esterni nella pagina di hosting. Gli script esterni possono ascoltare questi eventi ed eseguire varie operazioni. Ad esempio, ogni volta che il nome utente in un modulo cambia, cambia anche il nome visualizzato nell’intestazione della pagina. Per maggiori dettagli su tali eventi, vedi [Riferimento API della libreria JavaScript per i moduli adattivi](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html).

Utilizza il codice seguente per registrare i gestori:

```javascript
guideBridge.on("elementValueChanged", function (event, data)  {

      // execute some logic when value of a field is changed

});
```

### Creazione di pattern personalizzati per un campo {#creating-custom-patterns-for-a-field}

Come indicato in precedenza, i moduli adattivi consentono all’autore di fornire pattern per la convalida o i formati di visualizzazione. Oltre a utilizzare pattern predefiniti, è possibile definire pattern personalizzati riutilizzabili per un componente modulo adattivo. Ad esempio, è possibile definire un campo di testo o un campo numerico. Una volta definiti, è possibile utilizzare questi pattern in tutti i moduli per uno specifico tipo di componente. Ad esempio, è possibile creare un pattern personalizzato per un campo di testo e utilizzarlo nei campi di testo nei relativi moduli adattivi. È possibile selezionare il pattern personalizzato accedendo alla sezione del pattern nella finestra di dialogo di modifica di un componente. Per informazioni dettagliate sulla definizione o sul formato del pattern, consulta [Supporto della clausola immagine per i moduli HTML5](/help/forms/using/picture-clause-support.md).

Per creare un pattern personalizzato per un tipo di campo specifico e riutilizzarlo per altri campi dello stesso tipo, effettua le seguenti operazioni:

1. Passa ad CRXDE Lite nell’istanza di authoring.
1. Crea una cartella per mantenere i pattern personalizzati. Sotto la directory /apps , crea un nodo di tipo sling:folder. Ad esempio, crea un nodo con il nome `customPatterns`. Sotto questo nodo, crea un altro nodo di tipo `nt:unstructed` e denominalo `textboxpatterns`. Questo nodo contiene i vari pattern personalizzati che si desidera aggiungere.
1. Apri la scheda Proprietà del nodo creato. Ad esempio, apri la scheda Proprietà di `textboxpatterns`. Aggiungi il `guideComponentType` a questo nodo e imposta il suo valore su *fd/af/components/formatter/guideTextBox*.

1. Il valore di questa proprietà varia a seconda del campo per il quale si desidera definire i pattern. Per il campo numerico, il valore del `guideComponentType` è *fd/af/components/formatter/guideNumericBox*. Il valore del campo Datepicker è *fd/af/components/formatter/guideDatepicker*. &quot;
1. È possibile aggiungere un pattern personalizzato assegnando una proprietà al `textboxpatterns` nodo. Aggiungi una proprietà con un nome (ad esempio `pattern1`) e impostarne il valore sul pattern che si desidera aggiungere. Ad esempio, aggiungi una proprietà `pattern1` con valore Fax=text{99-999-999999}. Il pattern è disponibile per tutte le caselle di testo utilizzate in Forms adattivo.

   ![Creazione di pattern personalizzati per i campi in CrxDe](assets/creating-custom-patterns.png)

   Creazione di pattern personalizzati
