---
title: Espressioni modulo adattivo
seo-title: Espressioni modulo adattivo
description: Utilizzare espressioni di moduli adattivi per aggiungere la convalida, il calcolo automatico e attivare o disattivare la visibilità di una sezione.
seo-description: Utilizzare espressioni di moduli adattivi per aggiungere la convalida, il calcolo automatico e attivare o disattivare la visibilità di una sezione.
uuid: c274dce5-8b87-472f-bff5-53b246fa6584
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 2fd2276e-cfe3-47ad-94c1-9c7af56b7a17
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2766'
ht-degree: 0%

---


# Espressioni modulo adattivo{#adaptive-form-expressions}

I moduli adattivi offrono agli utenti finali un&#39;esperienza di compilazione dei moduli ottimizzata e semplificata grazie a funzionalità di scripting dinamico. Consente di scrivere espressioni per aggiungere vari comportamenti, ad esempio campi e pannelli di visualizzazione o di visualizzazione dinamici. Consente inoltre di aggiungere campi calcolati, rendere i campi di sola lettura, aggiungere logica di convalida e molto altro ancora. Il comportamento dinamico si basa sull&#39;input dell&#39;utente o sui dati precompilati.

JavaScript è il linguaggio di espressione dei moduli adattivi. Tutte le espressioni sono espressioni JavaScript valide e utilizzano API per modelli di script di moduli adattivi. Queste espressioni restituiscono valori di determinati tipi. Per l&#39;elenco completo delle classi, degli eventi, degli oggetti e delle API pubbliche dei moduli adattivi, consultare il documento Riferimento API della libreria [JavaScript per i moduli](https://helpx.adobe.com/aem-forms/6/javascript-api/index.html)adattivi.

## Procedure ottimali per la scrittura di espressioni {#best-practices-for-writing-expressions}

* Durante la scrittura di espressioni, per accedere a campi e pannelli è possibile utilizzare il nome del campo o del pannello. Per accedere al valore di un campo, utilizzare la proprietà value. Esempio, `field1.value`
* Utilizzare nomi univoci per campi e pannelli all&#39;interno del modulo. Consente di evitare possibili conflitti con i nomi dei campi utilizzati durante la scrittura delle espressioni.
* Durante la scrittura di espressioni con più righe, utilizzate un punto e virgola per terminare un&#39;istruzione.

## Procedure ottimali per le espressioni che coinvolgono il pannello ripetuto {#best-practices-for-expressions-involving-repeating-panel}

I pannelli ripetuti sono istanze di un pannello che vengono aggiunte o rimosse in modo dinamico mediante l&#39;API di script o dati precompilati. Per informazioni dettagliate sull&#39;uso del pannello ripetuto, vedere [Creazione di moduli con sezioni](/help/forms/using/creating-forms-repeatable-sections.md)ripetibili.

* Per creare un pannello ripetuto, nella finestra di dialogo del pannello aprite le impostazioni e impostate il valore del campo conteggio massimo su più di 1.
* Il valore del conteggio minimo delle impostazioni di ripetizione del pannello può essere uno o più, ma non può essere maggiore del valore massimo del conteggio.
* Quando un&#39;espressione fa riferimento a un campo del pannello ripetuto, i nomi dei campi nell&#39;espressione vengono risolti nell&#39;elemento ripetuto più vicino.
* I moduli adattivi offrono alcune funzioni speciali per semplificare il calcolo dei pannelli ripetibili, ad esempio somma, conteggio, min, max, filtro e molto altro. Per l&#39;elenco completo delle funzioni, consultare il riferimento API della libreria [JavaScript per i moduli adattivi](https://helpx.adobe.com/aem-forms/6/javascript-api/af.html)
* Le API per la modifica delle istanze del pannello ripetuto sono:

   * Per aggiungere un’istanza di pannello: `panel1.instanceManager.addInstance()`
   * Per ottenere un indice di ripetizione del pannello: `panel1.instanceIndex`
   * Per ottenere instanceManager di un pannello: `_panel1 or panel1.instanceManager`
   * Per rimuovere un’istanza di un pannello: `_panel1.removeInstance(panel1.instanceIndex)`

## Tipi di espressione {#expression-types}

Nei moduli adattivi è possibile scrivere espressioni per aggiungere comportamenti quali mostrare/nascondere campi e pannelli dinamici. È inoltre possibile scrivere espressioni per aggiungere campi calcolati, rendere i campi di sola lettura, la logica di convalida e molto altro ancora. I moduli adattivi supportano le seguenti espressioni:

* **[Espressioni](#access-expression-enablement-expression)**di accesso: per attivare/disattivare un campo.
* **[Calcola espressioni](#calculate-expression)**: per calcolare automaticamente il valore di un campo.
* **[Espressione](#click-expression)**di clic: per gestire le azioni in caso di clic su un pulsante.
* **[Script](#initialization-script)di inizializzazione:**eseguire un&#39;azione all&#39;inizializzazione di un campo.
* **[Espressione](#options-expression)**Opzioni: per compilare in modo dinamico un elenco a discesa.
* **[Espressione](#summary)**di riepilogo: per calcolare in modo dinamico il titolo di un pannello a soffietto.
* **[Convalidare le espressioni](#validate-expression)**: per convalidare un campo.
* **[Script](#value-commit-script)di conferma del valore:**per modificare i componenti di un modulo dopo la modifica del valore di un campo.
* **[Espressione](#visibility-expression)**di visibilità: per controllare la visibilità di un campo e di un pannello.
* **[Espressione](#step-completion-expression)**completamento passaggio: per impedire che un utente passi al passaggio successivo di una procedura guidata.

### Espressione di accesso (espressione di abilitazione) {#access-expression-enablement-expression}

È possibile utilizzare l&#39;espressione access per abilitare o disabilitare un campo. Se l&#39;espressione utilizza il valore di un campo, ogni volta che il valore del campo cambia l&#39;espressione viene riattivata.

**Si applica a**: fields

**Tipo** di restituzione: L&#39;espressione restituisce un valore booleano che rappresenta se il campo è abilitato o disabilitato. **true** indica che il campo è abilitato e **false** indica che il campo è disabilitato.

**Esempio**: Per abilitare un campo solo quando il valore di **field1** è impostato su **X**, l&#39;espressione di accesso è: `field1.value == "X"`

### Calcola espressione {#calculate-expression}

L&#39;espressione calculate viene utilizzata per calcolare automaticamente il valore di un campo utilizzando un&#39;espressione. In genere, tale espressione utilizza la proprietà value di un altro campo. Esempio, `field2.value + field3.value`. Ogni volta che il valore `field2`o `field3`cambia, l&#39;espressione viene riattivata e il valore viene ricalcolato.

**Si applica a**: fields

**Tipo** di restituzione: L&#39;espressione restituisce un valore compatibile con il campo in cui viene visualizzato il risultato dell&#39;espressione (ad esempio, decimale).

**Esempio**: L&#39;espressione calculate per mostrare la somma di due campi in **field1** è:
`field2.value + field3.value`

### Click Expression {#click-expression}

L&#39;espressione click gestisce le azioni eseguite sull&#39;evento click di un pulsante. GuideBridge fornisce API che eseguono varie funzioni, ad esempio invia, convalida, utilizzate insieme all&#39;espressione click. Per un elenco completo delle API, consultate API [GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html).

**Si applica a**: Campi pulsante

**Tipo** di restituzione: L&#39;espressione click non restituisce alcun valore. Se una qualsiasi espressione restituisce un valore, il valore viene ignorato.

**Esempio**: Per compilare una casella di testo **textbox1** nell&#39;azione clic di un pulsante con **AEM Forms** di valore, l&#39;espressione click del pulsante è `textbox1.value="AEM Forms"`

### Script di inizializzazione {#initialization-script}

Lo script di inizializzazione viene attivato quando viene inizializzato un modulo adattivo. A seconda degli scenari, lo script di inizializzazione si comporta come segue:

* Quando si esegue il rendering di un modulo adattivo senza precompilazione dati, lo script di inizializzazione viene eseguito dopo l&#39;inizializzazione del modulo.
* Quando viene eseguito il rendering di un modulo adattivo con una precompilazione dei dati, lo script viene eseguito al termine dell&#39;operazione di precompilazione.
* Quando viene attivata la riconvalida lato server di un modulo adattivo, viene eseguito lo script di inizializzazione.

**Si applica a:** campi e pannello

**Tipo di restituzione:** L&#39;espressione script di inizializzazione non restituisce alcun valore. Se una qualsiasi espressione restituisce un valore, il valore viene ignorato.

**Esempio:** In uno scenario di pre-compilazione dei dati, per compilare i campi con il valore predefinito `'Adaptive Forms'` quando il relativo valore viene salvato come null, l&#39;espressione script di inizializzazione è:
`if(this.value==null) this.value='Adaptive Forms';`

### Espressione Opzioni {#options-expression}

L&#39;espressione options viene utilizzata per compilare dinamicamente le opzioni di un campo elenco a discesa.

**Si applica a**: campi elenco a discesa

**Tipo** di restituzione: L&#39;espressione options restituisce un array di valori stringa. Ogni valore può essere una semplice stringa, ad esempio **Maschio**, o in un formato di coppia chiave=valore, ad esempio **1=Maschio**

**Esempio**: Per compilare il valore di un campo, in base al valore di un altro campo, fornire un&#39;espressione di opzioni semplice. Ad esempio, per compilare un campo, **Numero di bambini**, in base allo Stato **** civile espresso in un altro campo, l&#39;espressione è:

**`marital_status.value == "married" ? ["1=One", "2=two"] : ["0=Zero"]`.**

Ogni volta che il valore del campo **marital_status** cambia, l&#39;espressione viene riattivata. È inoltre possibile compilare il menu a discesa da un servizio REST. Per informazioni dettagliate, consultate Compilazione [dinamica di menu a discesa](../../forms/using/dynamically-populate-dropdowns.md).

### Espressione di riepilogo {#summary}

L&#39;espressione Summary calcola dinamicamente il titolo di un pannello secondario di un pannello di layout a soffietto. È possibile specificare l&#39;espressione Summary in una regola, che utilizza un campo modulo o una logica personalizzata per valutare il titolo. L&#39;espressione viene eseguita quando il modulo viene inizializzato. Se si sta precompilando un modulo, l&#39;espressione viene eseguita dopo che i dati sono stati precompilati o quando il valore dei campi dipendenti utilizzati nell&#39;espressione cambia.

L&#39;espressione Summary viene in genere utilizzata per gli elementi secondari ripetuti di un pannello di layout a soffietto per fornire un titolo significativo a ciascun pannello secondario.

**Si applica a:** Pannelli che sono elementi figlio diretti di un pannello il cui layout è configurato come Accordion.

**Tipo di restituzione:** L&#39;espressione restituisce un elemento String che diventa il titolo dell&#39;elemento Accordion.

**Esempio:** &quot;Numero account: &quot;+ textbox1.value

### Convalida espressione {#validate-expression}

L&#39;espressione validate viene utilizzata per convalidare i campi utilizzando l&#39;espressione specificata. In genere, tali espressioni utilizzano espressioni regolari insieme al valore del campo per convalidare un campo. L&#39;espressione viene riattivata e lo stato di convalida del campo viene ricalcolato in seguito a qualsiasi modifica del valore di un campo.

**Si applica a**: fields

**Tipo** di restituzione: L&#39;espressione restituisce un valore booleano che rappresenta lo stato di convalida del campo. Il valore **false** rappresenta che il campo non è valido e **true** rappresenta la validità del campo.
**Esempio**: Per un campo che rappresenta il codice postale del Regno Unito, l&#39;espressione di convalida è:

(**this.value** &amp;&amp; `this.value.match(/^(GIR 0AA|[A-Z]{1,2}\d[A-Z0-9]? ?[0-9][A-Z]{2}\s*)$/i) == null) ? false : true`

Nell&#39;esempio precedente, se il valore non vuoto non corrisponde al pattern, l&#39;espressione restituisce **false** per indicare che il campo non è valido.

>[!NOTE]
>
>Se si scrive un&#39;espressione di convalida per un campo non obbligatorio o obbligatorio, l&#39;espressione viene valutata indipendentemente dallo stato di visibilità del campo. Per arrestare la convalida dei campi nascosti, impostare su true la proprietà validationsDisabled nello script di inizializzazione o di conferma del valore. Esempio, `this.validationsDisabled=true`

### Script per conferma del valore {#value-commit-script}

Lo script Value Commit viene attivato quando:

* Un utente modifica il valore di un campo dall’interfaccia utente.
* Il valore di un campo viene modificato a livello di programmazione a causa di una modifica in un altro campo.

**Si applica a:** fields

**Tipo di restituzione:** L&#39;espressione script commit del valore non restituisce alcun valore. Se una qualsiasi espressione restituisce un valore, il valore viene ignorato.

**Esempio:** Per convertire in maiuscolo le lettere maiuscole degli alfabeti immessi nel campo in corrispondenza di commit, il valore commit dell&#39;espressione è:
`this.value=this.value.toUpperCase()`

>[!NOTE]
>
>È possibile disabilitare l&#39;esecuzione dello script di commit dei valori quando il valore di un campo viene modificato a livello di programmazione. A questo scopo, andate al https://&#39;[server]:[port]&#39;/system/console/configMgr e modificate la versione **dei moduli adattivi per compatibilità** con **i AEM Forms 6.1**. In seguito, lo script Value Commit viene eseguito solo quando l&#39;utente modifica il valore del campo dall&#39;interfaccia utente.

### Espressione di visibilità {#visibility-expression}

L&#39;espressione Visibilità viene utilizzata per controllare la visibilità di campo/pannello. In genere, l&#39;espressione di visibilità utilizza la proprietà value di un campo e viene riattivata ogni volta che il valore cambia.

**Si applica a**: campi e pannello

**Tipo** di restituzione: L&#39;espressione restituisce un valore booleano che rappresenta il campo o il pannello visibile o meno. **false** indica che il campo o il pannello non è visibile e true indica che il campo o il pannello è visibile.

**Esempio**: Per un pannello che diventa visibile solo se il valore di **field1** è impostato su **Maschio**, l&#39;espressione di visibilità è: `field1.value == "Male"`

### Espressione completamento passaggio {#step-completion-expression}

L&#39;espressione completamento passaggi viene utilizzata per impedire all&#39;utente di passare al passaggio successivo di un layout della procedura guidata. Queste espressioni vengono utilizzate quando i pannelli dispongono di un layout guidato (moduli con più fasi che mostrano un passaggio alla volta). L&#39;utente può passare al passaggio successivo, al pannello o alla sottosezione solo se tutti i valori richiesti nella sezione corrente sono pieni e validi.

**Si applica a**: Pannelli con layout dell&#39;elemento impostato sulla procedura guidata.

**Tipo** di restituzione: L&#39;espressione restituisce un valore booleano che rappresenta il pannello corrente valido o meno. **True** indica che il pannello corrente è valido e che l&#39;utente può passare al pannello successivo.

**Esempio**: In un modulo organizzato in vari pannelli, prima di passare al pannello successivo viene convalidato il pannello corrente. In tali casi, vengono utilizzate le espressioni di completamento dei passaggi. In genere, queste espressioni utilizzano l&#39;API validate di GuideBridge. Un esempio di espressione completamento passo è:
`window.guideBridge.validate([],this.panel.navigationContext.currentItem.somExpression)`

## Convalida nel modulo adattivo {#validations-in-adaptive-form}

Esistono diversi metodi per aggiungere la convalida dei campi a un modulo adattivo. Se su un campo viene aggiunto un controllo di convalida, **True** indica che il valore immesso nel campo è valido. **False** indica che il valore non è valido. Se si esegue il tab-in e out di un campo, il messaggio di errore non viene generato.

I metodi per aggiungere le convalide a un campo sono:

### Obbligatorio {#required}

Per rendere obbligatorio un componente, nella finestra di dialogo **Modifica** del componente potete selezionare l’opzione **Titolo e testo > Obbligatorio**. È inoltre possibile aggiungere il messaggio **** richiesto appropriato (facoltativo). .

### Pattern di convalida {#validation-patterns}

Per un campo sono disponibili più pattern di convalida della casella. Per selezionare un pattern di convalida, nella finestra di dialogo **Modifica** del componente individuare la sezione **Pattern** e selezionare **i pattern**. È possibile creare un pattern di convalida personalizzato in una casella di testo **Pattern** . Lo stato di convalida viene restituito **True** solo se i dati compilati sono conformi al pattern di convalida, altrimenti viene restituito **False** . Per creare un pattern di convalida personalizzato, vedere Supporto della clausola [illustrazione per i moduli](/help/forms/using/picture-clause-support.md)HTML5.

### Espressioni convalida {#validation-expressions}

La convalida di un campo può anche essere calcolata utilizzando espressioni presenti in diversi campi. Queste espressioni sono scritte all&#39;interno del campo **Script** convalida della scheda **Script** della finestra di dialogo **Modifica** del componente. Lo stato di convalida di un campo dipende dal valore restituito dall&#39;espressione. Per informazioni su come scrivere tali espressioni, vedere [Convalida espressione](../../forms/using/adaptive-form-expressions.md#p-validate-expression-p).

## Informazioni aggiuntive {#additional-information}

### Utilizzo del formato di visualizzazione dei campi {#using-field-display-format}

Formato di visualizzazione può essere utilizzato per visualizzare i dati in diversi formati. Ad esempio, è possibile utilizzare il formato di visualizzazione per visualizzare un numero di telefono con trattini, formattare il codice ZIP o selezionare la data. Questi pattern di visualizzazione possono essere selezionati dalla sezione **Pattern** della finestra di dialogo Modifica di un componente. È possibile creare pattern di visualizzazione personalizzati simili ai pattern di convalida indicati in precedenza.

### GuideBridge - API ed eventi {#guidebridge-apis-and-events}

GuideBridge è un insieme di API che possono essere utilizzate per interagire con i moduli adattivi nel modello di memoria in un browser. Per un&#39;introduzione dettagliata all&#39;API di Guide Bridge, ai metodi di classe, agli eventi esposti, vedere Riferimento API [JavaScript Library per i moduli](https://helpx.adobe.com/aem-forms/6/javascript-api/)adattivi.

>[!NOTE]
>
>È consigliabile non utilizzare i listener di eventi GuideBridge nelle espressioni.

#### Utilizzo di GuideBridge in varie espressioni {#guidebridge-usage-in-various-expressions}

* Per reimpostare i campi modulo, è possibile attivare `guideBridge.reset()` l&#39;API facendo clic sull&#39;espressione di un pulsante. Analogamente, esiste un&#39;API submit che può essere chiamata come espressione click `guideBridge.submit()`**.**

* Potete utilizzare l&#39; `setFocus()` API per impostare lo stato attivo su vari campi o pannelli (poiché lo stato attivo del pannello è impostato automaticamente sul primo campo). `setFocus()`offre un’ampia gamma di opzioni per la navigazione tra i pannelli, la navigazione precedente/successiva, l’impostazione dello stato attivo per un particolare campo e molte altre. Ad esempio, per passare al pannello successivo, potete usare: `guideBridge.setFocus(this.panel.somExpression, 'nextItem').`

* Per convalidare un modulo adattivo o i relativi pannelli specifici, utilizzare `guideBridge.validate(errorList, somExpression).`

#### Utilizzo di GuideBridge all’esterno delle espressioni  {#using-guidebridge-outside-expressions-nbsp}

Potete anche utilizzare le API GuideBridge al di fuori delle espressioni. Ad esempio, è possibile utilizzare l&#39;API GuideBridge per impostare la comunicazione tra l&#39;HTML della pagina che ospita il modulo adattivo e il modello di modulo. Inoltre, è possibile impostare il valore che proviene dall&#39;elemento padre di Iframe che ospita il modulo.

Per utilizzare l’API GuideBridge per gli esempi di cui sopra, acquisite un’istanza di GuideBridge. Per acquisire l&#39;istanza, ascoltare l&#39; `bridgeInitializeStart`evento di un `window`oggetto:

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
>In AEM, è buona norma scrivere il codice in una libreria client e includerlo nella pagina (header.jsp o piè di pagina.jsp della pagina)

Per utilizzare GuideBridge dopo l&#39;inizializzazione del modulo (l&#39; `bridgeInitializeComplete` evento viene inviato), è necessario utilizzare l&#39;istanza GuideBridge `window.guideBridge`. Potete verificare lo stato di inizializzazione di GuideBridge utilizzando l&#39; `guideBride.isConnected` API.

#### Eventi GuideBridge {#guidebridge-events}

GuideBridge fornisce inoltre alcuni eventi per gli script esterni nella pagina host. Gli script esterni possono ascoltare questi eventi ed eseguire varie operazioni. Ad esempio, ogni volta che il nome utente in un modulo cambia, cambia anche il nome visualizzato nell’intestazione della pagina. Per ulteriori dettagli su tali eventi, vedere Riferimento API della libreria [JavaScript per i moduli](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html)adattivi.

Utilizzare il codice seguente per registrare i gestori:

```javascript
guideBridge.on("elementValueChanged", function (event, data)  {

      // execute some logic when value of a field is changed

});
```

### Creazione di pattern personalizzati per un campo {#creating-custom-patterns-for-a-field}

Come già detto, i moduli adattivi consentono all&#39;autore di fornire pattern per la convalida o i formati di visualizzazione. Oltre a utilizzare i pattern predefiniti, è possibile definire pattern personalizzati riutilizzabili per un componente modulo adattivo. Ad esempio, è possibile definire un campo di testo o un campo numerico. Una volta definiti, è possibile utilizzare questi pattern in tutti i moduli per il tipo di componente specificato. Ad esempio, è possibile creare un pattern personalizzato per un campo di testo e utilizzarlo nei campi di testo dei moduli adattivi. È possibile selezionare il pattern personalizzato accedendo alla sezione del pattern nella finestra di dialogo di modifica di un componente. Per informazioni dettagliate sulla definizione o il formato del pattern, vedere Supporto della clausola [illustrazione per i moduli](/help/forms/using/picture-clause-support.md)HTML5.

Per creare un pattern personalizzato per un tipo di campo specifico e riutilizzarlo per altri campi dello stesso tipo, procedere come segue:

1. Passa a CRXDE Lite nell’istanza di authoring.
1. Create una cartella per mantenere i pattern personalizzati. Nella directory /apps, create un nodo di tipo sling:folder. Ad esempio, creare un nodo con il nome `customPatterns`. Sotto questo nodo, creare un altro nodo di tipo `nt:unstructed` e denominarlo `textboxpatterns`. Questo nodo contiene i vari pattern personalizzati che si desidera aggiungere.
1. Aprire la scheda Proprietà del nodo creato. Ad esempio, aprire la scheda Proprietà di `textboxpatterns`. Aggiungete la `guideComponentType` proprietà a questo nodo e impostatene il valore su *fd/af/components/formatter/guideTextBox*.

1. Il valore di questa proprietà varia a seconda del campo per il quale si desidera definire i pattern. Per i campi numerici, il valore della `guideComponentType` proprietà è *fd/af/components/formatter/guideNumericBox*. Il valore del campo Datepicker è *fd/af/components/formatter/guideDatepicker*.
&quot;
1. È possibile aggiungere un pattern personalizzato assegnando una proprietà al `textboxpatterns` nodo. Aggiungete una proprietà con un nome (ad esempio `pattern1`) e impostatene il valore sul pattern da aggiungere. Ad esempio, aggiungere una proprietà `pattern1` con il valore Fax=text{99-999-999999}. Il pattern è disponibile per tutte le caselle di testo utilizzate nei moduli adattivi.

   ![Creazione di pattern personalizzati per i campi in CrxDe](assets/creating-custom-patterns.png)

   Creazione di pattern personalizzati

