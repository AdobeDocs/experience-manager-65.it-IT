---
title: Espressioni modulo adattivo
description: Utilizza le espressioni per moduli adattivi per aggiungere convalida, calcolo e attivare o disattivare automaticamente la visibilità di una sezione.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms, Foundation Components
exl-id: 048bd9e8-ef34-40fb-9f46-73743d7b47c8
source-git-commit: 4ecdcb2659b26043f95ba1dc3e907c33f65b8834
workflow-type: tm+mt
source-wordcount: '2781'
ht-degree: 0%

---

# Espressioni modulo adattivo{#adaptive-form-expressions}

<span class="preview"> L’Adobe consiglia di utilizzare l’acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

I moduli adattivi offrono un’esperienza di compilazione dei moduli ottimizzata e semplificata per gli utenti finali con funzionalità di scripting dinamico. Consente di scrivere espressioni per aggiungere vari comportamenti, ad esempio mostrare/nascondere campi e pannelli dinamici. Consente inoltre di aggiungere campi calcolati, rendere i campi di sola lettura, aggiungere logica di convalida e molto altro. Il comportamento dinamico si basa sull’input dell’utente o sui dati precompilati.

JavaScript è il linguaggio di espressione dei moduli adattivi. Tutte le espressioni sono espressioni JavaScript valide e utilizzano API di modelli di script per moduli adattivi. Queste espressioni restituiscono valori di determinati tipi. Per l’elenco completo delle classi, degli eventi, degli oggetti e delle API pubbliche dei moduli adattivi, consulta [Riferimento API della libreria JavaScript per i moduli adattivi](https://helpx.adobe.com/experience-manager/6-5/forms/javascript-api/index.html).

## Best practice per la scrittura di espressioni {#best-practices-for-writing-expressions}

* Durante la scrittura di espressioni, per accedere a campi e pannelli è possibile utilizzare il nome del campo o del pannello. Per accedere al valore di un campo, utilizzare la proprietà value. Ad esempio `field1.value`
* Utilizza nomi univoci per campi e pannelli nel modulo. Consente di evitare possibili conflitti con i nomi dei campi utilizzati durante la scrittura delle espressioni.
* Durante la scrittura di espressioni su più righe, utilizzare un punto e virgola per terminare un&#39;istruzione.

## Best practice per le espressioni che coinvolgono il pannello ripetuto {#best-practices-for-expressions-involving-repeating-panel}

I pannelli ripetuti sono istanze di un pannello che vengono aggiunte o rimosse dinamicamente, utilizzando API di script o dati precompilati. Per informazioni dettagliate sull’utilizzo del pannello ripetuto, consulta [creazione di moduli con sezioni ripetibili](/help/forms/using/creating-forms-repeatable-sections.md).

* Per creare un pannello ripetuto, nella finestra di dialogo del pannello, apri le impostazioni e imposta il valore del campo conteggio massimo su più di 1.
* Il valore di conteggio minimo delle impostazioni di ripetizione del pannello può essere uno o più ma non può essere superiore al valore di conteggio massimo.
* Quando un’espressione fa riferimento a un campo di un pannello ripetuto, i nomi dei campi nell’espressione vengono risolti nell’elemento ripetuto più vicino.
* I moduli adattivi forniscono alcune funzioni speciali per semplificare il calcolo per i pannelli ripetibili come somma, conteggio, min, max, filtro e molte altre. Per l’elenco completo delle funzioni, consulta [Riferimento API della libreria JavaScript per i moduli adattivi](https://helpx.adobe.com/aem-forms/6/javascript-api/af.html)
* Le API per la manipolazione delle istanze del pannello ripetuto sono:

   * Per aggiungere un’istanza del pannello: `panel1.instanceManager.addInstance()`
   * Per ottenere un indice di ripetizione del pannello: `panel1.instanceIndex`
   * Per ottenere l’instanceManager di un pannello: `_panel1 or panel1.instanceManager`
   * Per rimuovere un’istanza di un pannello: `_panel1.removeInstance(panel1.instanceIndex)`

## Tipi di espressioni {#expression-types}

Nei moduli adattivi, puoi scrivere espressioni per aggiungere comportamenti quali mostrare/nascondere campi e pannelli dinamici. È inoltre possibile scrivere espressioni per aggiungere campi calcolati, rendere i campi di sola lettura, logica di convalida e molto altro. I moduli adattivi supportano le seguenti espressioni:

* **[Accedere alle espressioni](#access-expression-enablement-expression)**: per abilitare/disabilitare un campo.
* **[Calcolare le espressioni](#calculate-expression)**: per calcolare automaticamente il valore di un campo.
* **[Espressione clic](#click-expression)**: per gestire le azioni all’evento clic di un pulsante.
* **[Script di inizializzazione](#initialization-script):** eseguire un&#39;azione all&#39;inizializzazione di un campo.
* **[Espressione Options](#options-expression)**: per compilare in modo dinamico un elenco a discesa.
* **[Espressione di riepilogo](#summary)**: per calcolare dinamicamente il titolo di un pannello a soffietto.
* **[Convalidare espressioni](#validate-expression)**: per convalidare un campo.
* **[Script per conferma valore](#value-commit-script):** per modificare i componenti di un modulo dopo la modifica del valore di un campo.
* **[Espressione di visibilità](#visibility-expression)**: per controllare la visibilità di un campo e di un pannello.
* **[Espressione di completamento passaggio](#step-completion-expression)**: per impedire a un utente di passare al passaggio successivo di una procedura guidata.

### Espressione di accesso (espressione di abilitazione) {#access-expression-enablement-expression}

È possibile utilizzare l&#39;espressione di accesso per attivare o disattivare un campo. Se l’espressione utilizza il valore di un campo, ogni volta che il valore del campo cambia l’espressione viene riattivata.

**Applicabile a**: campi

**Tipo restituito**: l’espressione restituisce un valore booleano che indica se il campo è abilitato o disabilitato. **true** indica che il campo è abilitato e **false** indica che il campo è disabilitato.

**Esempio**: per abilitare un campo solo quando il valore di **campo1** è impostato su **X**, l’espressione di accesso è: `field1.value == "X"`

### Calcola espressione {#calculate-expression}

L’espressione di calcolo viene utilizzata per calcolare automaticamente il valore di un campo utilizzando un’espressione. In genere, tali espressioni utilizzano la proprietà value di altri campi. Ad esempio: `field2.value + field3.value`. Ogni volta che il valore `field2`o `field3`, l&#39;espressione viene riattivata e il valore viene ricalcolato.

**Applicabile a**: campi

**Tipo restituito**: l’espressione restituisce un valore compatibile con il campo in cui viene visualizzato il risultato dell’espressione (ad esempio, decimale).

**Esempio**: l’espressione di calcolo per mostrare la somma di due campi in **campo1** è:
`field2.value + field3.value`

### Espressione clic {#click-expression}

L&#39;espressione click gestisce le azioni eseguite sull&#39;evento click di un pulsante. GuideBridge fornisce le API per eseguire varie funzioni, ad esempio l&#39;invio e la convalida, utilizzate insieme all&#39;espressione di clic. Per un elenco completo delle API, consulta [API di GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html).

**Applicabile a**: campi pulsante

**Tipo restituito**: l’espressione di clic non restituisce alcun valore. Se un’espressione restituisce un valore, questo viene ignorato.

**Esempio**: per compilare una casella di testo **casella di testo1** sull’azione clic di un pulsante con valore **AEM Forms**, l’espressione di clic del pulsante è `textbox1.value="AEM Forms"`

### Script di inizializzazione {#initialization-script}

Lo script di inizializzazione viene attivato quando viene inizializzato un modulo adattivo. A seconda degli scenari, lo script di inizializzazione si comporta nel modo seguente:

* Quando si esegue il rendering di un modulo adattivo senza precompilazione dei dati, lo script di inizializzazione viene eseguito dopo l’inizializzazione del modulo.
* Quando si esegue il rendering di un modulo adattivo con una precompilazione di dati, lo script viene eseguito al termine dell’operazione di precompilazione.
* Quando viene attivata la riconvalida lato server di un modulo adattivo, viene eseguito lo script di inizializzazione.

**Si applica a:** campi e pannello

**Tipo di ritorno:** L&#39;espressione dello script di inizializzazione non restituisce alcun valore. Se un’espressione restituisce un valore, questo viene ignorato.

**Esempio:** In uno scenario di precompilazione dei dati, per popolare i campi con il valore predefinito `'Adaptive Forms'` quando il valore viene salvato come null, l&#39;espressione dello script di inizializzazione è:
`if(this.value==null) this.value='Adaptive Forms';`

### Espressione opzioni {#options-expression}

L’espressione options viene utilizzata per riempire dinamicamente le opzioni di un campo elenco a discesa.

**Applicabile a**: campi elenco a discesa

**Tipo restituito**: l’espressione options restituisce una matrice di valori stringa. Ogni valore può essere una stringa semplice, ad esempio **Maschio**, o in un formato coppia chiave=valore, ad esempio **1=Maschio**

**Esempio**: per popolare il valore di un campo, in base al valore di un altro campo, fornisci un’espressione di opzioni semplice. Ad esempio, per compilare un campo: **Numero di bambini**, in base alla **Stato civile** espresso in un altro campo, l’espressione è:

**`marital_status.value == "married" ? ["1=One", "2=two"] : ["0=Zero"]`.**

Ogni volta che il valore **marital_status** modifica il campo, l’espressione viene riattivata. Puoi anche popolare il menu a discesa da un servizio REST. Per informazioni dettagliate, consulta [Menu a discesa a compilazione dinamica](../../forms/using/dynamically-populate-dropdowns.md).

### Espressione di riepilogo {#summary}

L’espressione Riepilogo calcola dinamicamente il titolo di un pannello secondario di un pannello di layout del Pannello a soffietto. È possibile specificare l’espressione Summary in una regola, che utilizza un campo modulo o una logica personalizzata per valutare il titolo. L&#39;espressione viene eseguita quando il modulo viene inizializzato. Se si sta precompilando un modulo, l&#39;espressione viene eseguita dopo che i dati sono stati precompilati o quando il valore dei campi dipendenti utilizzati nell&#39;espressione cambia.

L’espressione Riepilogo viene in genere utilizzata per ripetere gli elementi secondari di un pannello di layout del Pannello a soffietto in modo da fornire un titolo significativo a ciascun pannello secondario.

**Si applica a:** Pannelli figli diretti di un pannello il cui layout è configurato come Pannello a soffietto.

**Tipo di ritorno:** L’espressione restituisce un elemento String che diventa il titolo del Pannello a soffietto.

**Esempio:** &quot;Numero account : &quot; + textbox1.value

### Convalida espressione {#validate-expression}

L’espressione di convalida viene utilizzata per convalidare i campi utilizzando l’espressione specificata. In genere, tali espressioni utilizzano espressioni regolari insieme al valore del campo per convalidare un campo. L’espressione viene riattivata e lo stato di convalida del campo viene ricalcolato in base a qualsiasi modifica del valore di un campo.

**Applicabile a**: campi

**Tipo restituito**: l’espressione restituisce un valore booleano che rappresenta lo stato di convalida del campo. Il valore **false** indica che il campo non è valido e **true** indica che il campo è valido.
**Esempio**: per un campo che rappresenta il codice postale del Regno Unito, l’espressione di convalida è:

(**this.value** &amp;&amp; `this.value.match(/^(GIR 0AA|[A-Z]{1,2}\d[A-Z0-9]? ?[0-9][A-Z]{2}\s*)$/i) == null) ? false : true`

Nell’esempio precedente, se il valore non vuoto non corrisponde al modello, l’espressione restituisce **false** per indicare che il campo non è valido.

>[!NOTE]
>
>Se scrivi un’espressione di convalida per un campo non obbligatorio o obbligatorio, l’espressione viene valutata indipendentemente dallo stato di visibilità del campo. Per interrompere la convalida dei campi nascosti, impostare la proprietà validationsDisabled nello script di inizializzazione o di conferma del valore su true. Ad esempio `this.validationsDisabled=true`

### Script per conferma del valore {#value-commit-script}

Lo script di conferma del valore viene attivato quando:

* Un utente modifica il valore di un campo dall’interfaccia utente.
* Il valore di un campo cambia a livello di programmazione a causa della modifica di un altro campo.

**Si applica a:** campi

**Tipo di ritorno:** L&#39;espressione dello script di commit del valore non restituisce alcun valore. Se un’espressione restituisce un valore, questo viene ignorato.

**Esempio:** Per convertire le maiuscole e minuscole degli alfabeti immessi nel campo in lettere maiuscole durante il commit, l&#39;espressione di commit del valore è:
`this.value=this.value.toUpperCase()`

>[!NOTE]
>
>È possibile disattivare l&#39;esecuzione dello script di commit del valore quando il valore di un campo viene modificato a livello di programmazione. A tale scopo, visitare il sito https://&#39;[server]:[porta]&#39;/system/console/configMgr and change **Versione Forms adattiva per la compatibilità** a **AEM Forms 6.1**. Successivamente, lo script di conferma del valore viene eseguito solo quando l’utente modifica il valore del campo dall’interfaccia utente.

### Espressione di visibilità {#visibility-expression}

L’espressione Visibilità viene utilizzata per controllare la visibilità del campo o del pannello. In genere, l’espressione di visibilità utilizza la proprietà value di un campo e viene riattivata ogni volta che tale valore cambia.

**Applicabile a**: campi e pannello

**Tipo restituito**: l’espressione restituisce un valore booleano, che rappresenta se il campo o il pannello è visibile o meno. **false** indica che il campo o il pannello non è visibile e true indica che il campo o il pannello è visibile.

**Esempio**: per un pannello che diventa visibile solo se il valore di **campo1** è impostato su **Maschio**, l’espressione di visibilità è: `field1.value == "Male"`

### Espressione di completamento passaggio {#step-completion-expression}

L’espressione di completamento del passaggio viene utilizzata per impedire a un utente di passare al passaggio successivo di un layout della procedura guidata. Queste espressioni vengono utilizzate quando i pannelli hanno un layout guidato (moduli con più passaggi che mostrano un passaggio alla volta). L’utente può passare al passaggio successivo, al pannello o alla sottosezione solo se tutti i valori richiesti nella sezione corrente sono compilati e validi.

**Applicabile a**: pannelli con il layout dell&#39;elemento impostato su procedura guidata.

**Tipo restituito**: l’espressione restituisce un valore booleano, che rappresenta se il pannello corrente è valido o meno. **Vero** indica che il pannello corrente è valido e l’utente può passare al pannello successivo.

**Esempio**: in un modulo organizzato in vari pannelli, prima di passare al pannello successivo il pannello corrente viene convalidato. In questi casi, vengono utilizzate le espressioni di completamento del passaggio. In genere, queste espressioni utilizzano l&#39;API di convalida GuideBridge. Un esempio di espressione di completamento del passaggio è:
`window.guideBridge.validate([],this.panel.navigationContext.currentItem.somExpression)`

## Convalide in modulo adattivo {#validations-in-adaptive-form}

Esistono più metodi per aggiungere la convalida di un campo a un modulo adattivo. Se viene aggiunto un controllo di convalida a un campo, **Vero** indica che il valore immesso nel campo è valido. **Falso** indica che il valore non è valido. Se passi da un campo a un altro, il messaggio di errore non viene generato.

I metodi per aggiungere convalide a un campo sono:

### Obbligatorio {#required}

Per rendere obbligatorio un componente, in **Modifica** del componente, puoi selezionare l’opzione **Titolo e testo > Obbligatorio**. È inoltre possibile aggiungere la **messaggio richiesto** (facoltativo).

### Modelli di convalida {#validation-patterns}

Per un campo sono disponibili più modelli di convalida predefiniti. Per selezionare un pattern di convalida, nella **Modifica** del componente, individua il **Pattern** sezione e seleziona **pattern**. È possibile creare un proprio pattern di convalida personalizzato in un **Pattern** casella di testo. Viene restituito lo stato di convalida **Vero** solo se i dati compilati sono conformi al modello di convalida, altrimenti **Falso** viene restituito. Per scrivere un proprio modello di convalida personalizzato, vedere [Supporto delle clausole di immagine per i moduli HTML5](/help/forms/using/picture-clause-support.md).

### Espressioni di convalida {#validation-expressions}

La convalida di un campo può essere calcolata anche utilizzando espressioni su campi diversi. Queste espressioni sono scritte all’interno di **Script di convalida** campo del **Script** scheda di **Modifica** del componente. Lo stato di convalida di un campo dipende dal valore restituito dall&#39;espressione. Per informazioni su come scrivere tali espressioni, consulta [Convalida espressione](../../forms/using/adaptive-form-expressions.md#p-validate-expression-p).

## Informazioni aggiuntive {#additional-information}

### Utilizzo del formato di visualizzazione dei campi {#using-field-display-format}

Formato di visualizzazione può essere utilizzato per visualizzare i dati in formati diversi. Ad esempio, puoi utilizzare il formato di visualizzazione per visualizzare un numero di telefono con trattini, formato del CAP o selezione data. Questi modelli di visualizzazione possono essere selezionati dalla **Pattern** nella finestra di dialogo per modifica di un componente. È possibile scrivere modelli di visualizzazione personalizzati simili ai modelli di convalida indicati in precedenza.

### GuideBridge - API ed eventi {#guidebridge-apis-and-events}

GuideBridge è una raccolta di API che possono essere utilizzate per interagire con i moduli adattivi nel modello di memoria in un browser. Per un&#39;introduzione dettagliata all&#39;API di Guide Bridge, ai metodi di classe e agli eventi esposti, vedere [Riferimento API della libreria JavaScript per i moduli adattivi](https://helpx.adobe.com/aem-forms/6/javascript-api/).

>[!NOTE]
>
>Si consiglia di non utilizzare i listener di eventi GuideBridge nelle espressioni.

#### Utilizzo di GuideBridge in varie espressioni {#guidebridge-usage-in-various-expressions}

* Per reimpostare i campi modulo, puoi attivare `guideBridge.reset()` API sull’espressione di clic di un pulsante. Allo stesso modo, esiste un’API di invio che può essere chiamata come espressione di clic `guideBridge.submit()`**.**

* È possibile utilizzare `setFocus()` API per impostare lo stato attivo su vari campi o pannelli (per il pannello lo stato attivo è impostato automaticamente sul primo campo). `setFocus()`offre un’ampia gamma di opzioni per la navigazione, ad esempio navigazione tra i pannelli, attraversamento precedente/successivo, impostazione dello stato attivo su un particolare campo e molto altro. Ad esempio, per passare al pannello successivo, puoi utilizzare: `guideBridge.setFocus(this.panel.somExpression, 'nextItem').`

* Per convalidare un modulo adattivo o i relativi pannelli specifici, utilizza `guideBridge.validate(errorList, somExpression).`

#### Utilizzo di GuideBridge all&#39;esterno delle espressioni  {#using-guidebridge-outside-expressions-nbsp}

È inoltre possibile utilizzare le API GuideBridge al di fuori delle espressioni. È possibile, ad esempio, utilizzare l’API GuideBridge per impostare la comunicazione tra il HTML della pagina che ospita il modulo adattivo e il modello di modulo. Inoltre, puoi impostare il valore proveniente dall’elemento padre dell’Iframe che ospita il modulo.

Per utilizzare l&#39;API GuideBridge per l&#39;esempio sopra riportato, acquisire un&#39;istanza di GuideBridge. Per acquisire l’istanza, ascolta `bridgeInitializeStart`evento di un `window`oggetto:

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
>In AEM, è buona prassi scrivere il codice in una clientLib e includerlo nella pagina (header.jsp o footer.jsp della pagina)

Per utilizzare GuideBridge dopo l&#39;inizializzazione del modulo (il `bridgeInitializeComplete` viene inviato), ottenere l&#39;istanza di GuideBridge utilizzando `window.guideBridge`. È possibile controllare lo stato di inizializzazione di GuideBridge utilizzando `guideBride.isConnected` API.

#### Eventi GuideBridge {#guidebridge-events}

GuideBridge fornisce inoltre alcuni eventi per gli script esterni nella pagina di hosting. Gli script esterni possono ascoltare questi eventi ed eseguire varie operazioni. Ad esempio, ogni volta che il nome utente di un modulo cambia, cambia anche il nome visualizzato nell’intestazione della pagina. Per maggiori dettagli su tali eventi, vedi [Riferimento API della libreria JavaScript per i moduli adattivi](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html).

Utilizza il seguente codice per registrare i gestori:

```javascript
guideBridge.on("elementValueChanged", function (event, data)  {

      // execute some logic when value of a field is changed

});
```

### Creazione di pattern personalizzati per un campo {#creating-custom-patterns-for-a-field}

Come accennato in precedenza, i moduli adattivi consentono all’autore di fornire modelli per la convalida o i formati di visualizzazione. Oltre a utilizzare motivi predefiniti, è possibile definire un motivo personalizzato riutilizzabile per un componente modulo adattivo. È ad esempio possibile definire un campo di testo o un campo numerico. Una volta definiti, è possibile utilizzare questi pattern in tutte le maschere per il tipo di componente specificato. Ad esempio, puoi creare un motivo personalizzato per un campo di testo e utilizzarlo nei campi di testo dei moduli adattivi. Potete selezionare il pattern personalizzato accedendo alla relativa sezione nella finestra di dialogo per modifica di un componente. Per informazioni dettagliate sulla definizione o il formato del motivo, vedere [Supporto delle clausole di immagine per i moduli HTML5](/help/forms/using/picture-clause-support.md).

Per creare un pattern personalizzato per un tipo di campo specifico e riutilizzarlo per altri campi dello stesso tipo, effettua le seguenti operazioni:

1. Passa a CRXDE Liti nell’istanza di authoring.
1. Crea una cartella per mantenere i modelli personalizzati. Nella directory /apps, crea un nodo di tipo sling:folder. Ad esempio, crea un nodo con il nome `customPatterns`. Sotto questo nodo, crea un altro nodo di tipo `nt:unstructed` e denominalo `textboxpatterns`. Questo nodo contiene i vari modelli personalizzati che desideri aggiungere.
1. Apri la scheda Proprietà del nodo creato. Ad esempio, apri la scheda Proprietà di `textboxpatterns`. Aggiungi il `guideComponentType` su questo nodo e impostarne il valore su *fd/af/components/formatter/guideTextBox*.

1. Il valore di questa proprietà varia a seconda del campo per il quale si desidera definire i modelli. Per un campo numerico, il valore della proprietà `guideComponentType` la proprietà è *fd/af/components/formatter/guideNumericBox*. Il valore del campo Datepicker è *fd/af/components/formatter/guideDatepicker*. &quot;
1. È possibile aggiungere un pattern personalizzato assegnando una proprietà al `textboxpatterns` nodo. Aggiungi una proprietà con un nome (ad esempio, `pattern1`) e impostarne il valore sul pattern da aggiungere. Ad esempio, aggiungi una proprietà `pattern1` con valore Fax=text{99-999-9999999}. Il pattern è disponibile per tutte le caselle di testo utilizzate in Adaptive Forms.

   ![Creazione di modelli personalizzati per i campi in CrxDe](assets/creating-custom-patterns.png)

   Creazione di pattern personalizzati
