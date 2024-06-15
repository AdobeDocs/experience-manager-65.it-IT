---
title: Come si utilizza l’Editor regole per aggiungere regole ai campi del modulo per aggiungere un comportamento dinamico e creare una logica complessa in un modulo adattivo basato su componenti core?
description: L’editor di regole di Forms adattivo consente di aggiungere un comportamento dinamico e di creare logiche complesse nei moduli senza la necessità di codificare o scrivere script.
feature: Adaptive Forms, Core Components
role: User
level: Beginner, Intermediate
source-git-commit: f633fdfda531cc29ce6274e0367708cc4909a0cd
workflow-type: tm+mt
source-wordcount: '5588'
ht-degree: 1%

---

# Aggiungere regole a un componente core modulo adattivo {#adaptive-forms-rule-editor}

Questo articolo contiene le funzioni più recenti dell’Editor regole di Adaptive Forms Core Components, che sono:
* Supporto per l’implementazione di condizioni nidificate con la funzionalità When-then-else
* Convalidare o reimpostare pannelli e moduli, inclusi i campi
* Supporto di funzioni JavaScript moderne, come le funzioni let e arrow (supporto ES10) all’interno delle funzioni personalizzate.

La funzione Editor regole facilita la scrittura di regole su oggetti Modulo adattivo da parte di utenti aziendali e sviluppatori di Forms. Queste regole definiscono le azioni da attivare sugli oggetti modulo in base alle condizioni preimpostate, agli input dell&#39;utente e alle azioni dell&#39;utente sul modulo. Consente di semplificare ulteriormente l’esperienza di compilazione dei moduli, garantendo precisione e velocità.

L’editor di regole fornisce un’interfaccia utente intuitiva e semplificata per scrivere regole. L’editor di regole offre un editor visivo per tutti gli utenti.<!-- In addition, only for forms power users, rule editor provides a code editor to write rules and scripts. --> Alcune delle azioni chiave eseguite sugli oggetti Modulo adattivo tramite Regole sono:

* Mostrare o nascondere un oggetto
* Attivare o disattivare un oggetto
* Impostare un valore per un oggetto
* Convalidare il valore di un oggetto
* Eseguire funzioni per calcolare il valore di un oggetto
* Richiamare un modello dati del modulo (FDM) ed eseguire un’operazione
* Impostare la proprietà di un oggetto

<!-- Rule editor replaces the scripting capabilities in [!DNL Experience Manager 6.1 Forms] and earlier releases. However, your existing scripts are preserved in the new rule editor. For more information about working with existing scripts in the rule editor, see [Impact of rule editor on existing scripts](rule-editor.md#p-impact-of-rule-editor-on-existing-scripts-p). -->

Utenti aggiunti al `forms-power-users` possono creare gli script e modificare quelli esistenti. Utenti in `forms-users group` può utilizzare gli script ma non crearli o modificarli.

## Informazioni su una regola {#understanding-a-rule}

Una regola è una combinazione di azioni e condizioni. Nell’editor delle regole, le azioni includono attività quali nascondere, mostrare, abilitare, disabilitare o calcolare il valore di un oggetto in un modulo. Le condizioni sono espressioni booleane che vengono valutate eseguendo controlli e operazioni sullo stato, sul valore o sulla proprietà di un oggetto modulo. Le azioni vengono eseguite in base al valore ( `True` o `False`) restituita valutando una condizione.

L’editor di regole fornisce un set di tipi di regole predefiniti, ad esempio When, Show, Hide, Enable, Disable, Set Value Of e Validate, per facilitare la scrittura delle regole. Ogni tipo di regola ti consente di definire condizioni e azioni in una regola. Il documento spiega ulteriormente ogni tipo di regola nei dettagli.

Una regola segue in genere uno dei seguenti costrutti:

**Condizione-Azione** In questo costrutto, una regola definisce prima una condizione seguita da un’azione da attivare. Il costrutto è paragonabile a `if-then statement` nei linguaggi di programmazione.

Nell’editor delle regole, il **Quando** tipo di regola applica il costrutto condizione-azione.

**Action-Condition** In questo costrutto, una regola definisce prima un’azione da attivare seguita da condizioni per la valutazione. Un’altra variante di questo costrutto è action-condition-alternate action, che definisce anche un’azione alternativa da attivare se la condizione restituisce False.

I tipi di regola Mostra, Nascondi, Abilita, Disabilita, Imposta valore di e Convalida nell&#39;Editor regole impongono `action-condition` costrutto regola. Per impostazione predefinita, l&#39;azione alternativa per Mostra è Nascondi e per Abilita è Disabilita e viceversa. Non è possibile modificare l&#39;azione alternativa predefinita.

>[!NOTE]
>
>I tipi di regole disponibili, incluse le condizioni e le azioni definite nell&#39;editor di regole, dipendono anche dal tipo di oggetto modulo su cui si sta creando una regola. Nell&#39;editor delle regole vengono visualizzati solo i tipi di regole e le opzioni validi per la scrittura di istruzioni di condizione e azione per un particolare tipo di oggetto modulo. Ad esempio, non vengono visualizzati i tipi Convalida e Imposta valore di per un oggetto pannello.

Per ulteriori informazioni sui tipi di regole disponibili nell’editor di regole, consulta [Tipi di regole disponibili nell’editor di regole](rule-editor.md#p-available-rule-types-in-rule-editor-p).

### Linee guida per la scelta di un costrutto regola {#guidelines-for-choosing-a-rule-construct}

Sebbene sia possibile ottenere la maggior parte dei casi d’uso utilizzando qualsiasi costrutto di regola, di seguito sono riportate alcune linee guida per scegliere un costrutto rispetto a un altro. Per ulteriori informazioni sulle regole disponibili nell’editor di regole, consulta [Tipi di regole disponibili nell’editor di regole](rule-editor.md#p-available-rule-types-in-rule-editor-p).

* Una regola tipica del pollice durante la creazione di una regola è pensarla nel contesto dell&#39;oggetto su cui si sta scrivendo una regola. Si supponga di voler nascondere o visualizzare un campo B in base al valore specificato dall&#39;utente nel campo A. In questo caso, si sta valutando una condizione nel campo A e, in base al valore restituito, si sta attivando un&#39;azione nel campo B.

  Pertanto, se stai scrivendo una regola sul campo B (l’oggetto su cui stai valutando una condizione), utilizza `condition-action` costrutto o `When` tipo di regola. Analogamente, utilizza `action-condition` costruire o `Show or Hide` tipo di regola nel campo A.

* A volte, è necessario eseguire più azioni in base a una condizione. In questi casi, si consiglia di utilizzare il `condition-action` costruzione. In questo costrutto, puoi valutare una condizione una sola volta e specificare più istruzioni di azione.

  Ad esempio, per nascondere i campi B, C e D in base alla condizione che verifica il valore specificato dall&#39;utente nel campo A, scrivere una regola con il costrutto condizione-azione o il tipo di regola When nel campo A e specificare azioni per controllare la visibilità dei campi B, C e D. In caso contrario, sono necessarie tre regole separate per i campi B, C e D, in cui ogni regola controlla la condizione e mostra o nasconde il rispettivo campo. In questo esempio, è più efficiente scrivere il tipo di regola When su un oggetto anziché Show o Hide su tre oggetti.

* Per attivare un’azione in base a più condizioni, si consiglia di utilizzare il costrutto azione-condizione. Ad esempio, per mostrare e nascondere il campo A valutando le condizioni nei campi B, C e D, utilizzare Mostra o Nascondi tipo di regola nel campo A.
* Utilizza il costrutto condizione-azione o condizione azione se la regola contiene un’azione per una condizione.
* Se una regola verifica la presenza di una condizione ed esegue immediatamente un&#39;azione quando fornisce un valore in un campo o esce da un campo, si consiglia di scrivere una regola con il costrutto condizione-azione o il tipo di regola When nel campo in cui viene valutata la condizione.
* La condizione nella regola When viene valutata quando un utente modifica il valore dell&#39;oggetto su cui viene applicata la regola When. Tuttavia, se desideri che l’azione si attivi quando il valore cambia sul lato server, come per il prepopolamento del valore, è consigliabile scrivere una regola When che attivi l’azione quando il campo viene inizializzato.
* Quando si scrivono regole per gli oggetti menu a discesa, pulsanti di scelta o caselle di controllo, le opzioni o i valori di tali oggetti modulo nel modulo vengono precompilati nell’editor di regole.

## Tipi di operatori ed eventi disponibili nell’editor di regole {#available-operator-types-and-events-in-rule-editor}

L’editor di regole fornisce i seguenti operatori logici ed eventi utilizzando i quali è possibile creare regole.

* **È uguale a**
* **Non è uguale a**
* **Inizia con**
* **Termina con**
* **Contiene**
* **Non contiene**
* **È vuoto**
* **Non è vuoto**
* **Ha selezionato:** Restituisce true quando l’utente seleziona una particolare opzione per una casella di controllo, un elenco a discesa o un pulsante di scelta.
* **È inizializzato (evento):** Restituisce true quando viene eseguito il rendering di un oggetto modulo nel browser.
* **Viene modificato (evento):** Restituisce true quando l&#39;utente modifica il valore immesso o l&#39;opzione selezionata per un oggetto modulo.

<!--
* **Navigation(event):** Returns true when the user clicks a navigation object. Navigation objects are used to move between panels. 
* **Step Completion(event):** Returns true when a step of a rule completes.
* **Successful Submission(event):** Returns true on successful submission of data to a form data model.
* **Error in Submission(event):**  Returns true on unsuccessful submission of data to a form data model. -->

## Tipi di regole disponibili nell’editor di regole {#available-rule-types-in-rule-editor}

L’editor di regole fornisce un set di tipi di regole predefiniti che è possibile utilizzare per scrivere regole. Esaminiamo in dettaglio ogni tipo di regola. Per ulteriori informazioni sulla scrittura di regole nell’editor di regole, consulta [Scrivi regole](rule-editor.md#p-write-rules-p).

### [!UICONTROL Quando] {#whenruletype}

Il **[!UICONTROL Quando]** il tipo di regola segue **condizione-azione-azione-azione alternativa** costrutto della regola o, a volte, solo **condizione-azione** costruzione. In questo tipo di regola, devi innanzitutto specificare una condizione per la valutazione seguita da un&#39;azione da attivare se la condizione viene soddisfatta ( `True`). Quando si utilizza il tipo di regola When, è possibile utilizzare più operatori AND e OR per creare [espressioni nidificate](#nestedexpressions).

Utilizzando il tipo di regola When, è possibile valutare una condizione in un oggetto modulo ed eseguire azioni su uno o più oggetti.

In parole semplici, una regola When tipica è strutturata come segue:

`When on Object A:`

`(Condition 1 AND Condition 2 OR Condition 3) is TRUE;`

`Then, do the following:`

`Action 2 on Object B;`
`AND`
`Action 3 on Object C`;

`Else, do the following:`

`Action 2 on Object C;`
_

Quando si dispone di un componente con più valori, ad esempio pulsanti di scelta o elenco, durante la creazione di una regola per tale componente le opzioni vengono recuperate e rese disponibili automaticamente al creatore della regola. Non è necessario digitare nuovamente i valori delle opzioni.

Ad esempio, un elenco include quattro opzioni: Rosso, Blu, Verde e Giallo. Durante la creazione della regola, le opzioni (pulsanti di scelta) vengono recuperate automaticamente e rese disponibili al creatore della regola come segue:

![Opzioni per la visualizzazione di più valori](assets/multivaluefcdisplaysoptions.png)

Durante la scrittura di una regola When, puoi attivare l&#39;azione Cancella valore di. `Clear Value Of` cancella il valore dell&#39;oggetto specificato. Avendo `Clear Value of` come opzione nell&#39;istruzione When consente di creare condizioni complesse con più campi. È possibile aggiungere l&#39;istruzione Else per aggiungere ulteriori condizioni.

![Cancella valore di](assets/clearvalueof.png)

>[!NOTE]
>
> Quando il tipo di regola supporta solo istruzioni then-else a livello singolo.

#### Più campi consentiti in [!UICONTROL Quando] {#allowed-multiple-fields}

In **Quando** condizione, puoi aggiungere altri campi oltre al campo a cui viene applicata la regola.

Ad esempio, utilizzando il tipo di regola When, è possibile valutare una condizione su diversi oggetti modulo ed eseguire l&#39;azione:

`When:`

`(Object A Condition 1)`

`AND/OR`

`(Object B Condtion 2)`

`Then, do the following:`

`Action 1 on Object A`

_

![Più campi consentiti in Quando](/help/forms/using/assets/allowed-multiple-field-when.png)




##### Considerazioni durante l’utilizzo di più campi consentiti nella funzione condizione When

* Assicurati che [il componente core e la versione della specifica sono impostati sulla versione più recente](https://github.com/adobe/aem-core-forms-components/tree/release/650) per utilizzare questa funzione nell’editor di regole.
* Se le regole vengono applicate a campi diversi all’interno della condizione When, la regola viene attivata anche se solo uno di questi campi viene modificato.


<!--
* It is not possible to add multiple fields in the When condition while applying rules to a button.

##### To enable Allowed Multiple fields in When condition feature

Allowed Multiple fields in When condition feature is disabled by default. To enable this feature, add a custom property at the template policy:

1. Open the corresponding template associated with an Adaptive Form in the template editor.
1. Select the existing policy as **formcontainer-policy**.
1. Navigate to the **[!UICONTROL Structure]**  view and, from the **[!UICONTROL Allowed Components]** list, open the **[!UICONTROL Adaptive Forms Container]** policy.
1. Go to the **[!UICONTROL Custom Properties]** tab and to add a custom property, click **[!UICONTROL Add]**.
1. Specify the **Group Name** of your choice. For example, in our case, we added the group name as **allowedfeature**.
1. Add the **key** and **value** pair as follows:
   * key: fd:changeEventBehaviour
   * value: deps
1. Click **[!UICONTROL Done]**. -->

Se nella funzione Condizione When sono presenti più campi consentiti, segui i passaggi di risoluzione dei problemi descritti di seguito.

1. Apri il modulo in modalità di modifica.
1. Apri il browser Contenuto e seleziona la **[!UICONTROL Contenitore guida]** componente del modulo adattivo.
1. Fai clic sulle proprietà Contenitore guida ![Proprietà guida](/help/forms/using/assets/configure-icon.svg) icona. Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).
1. Fai clic su Fine e salva di nuovo la finestra di dialogo.

**[!UICONTROL Nascondi]** Nasconde l&#39;oggetto specificato.

**[!UICONTROL Spettacolo]** Mostra l&#39;oggetto specificato.

**[!UICONTROL Abilita]** Attiva l&#39;oggetto specificato.

**[!UICONTROL Disattiva]** Disattiva l&#39;oggetto specificato.

**[!UICONTROL Richiama servizio]** Richiama un servizio configurato in un modello dati modulo (FDM). Quando scegli l’operazione Richiama servizio, viene visualizzato un campo. Quando tocca il campo, vengono visualizzati tutti i servizi configurati in tutti i modelli di dati del modulo (FDM) sul [!DNL Experience Manager] dell&#39;istanza. Quando si sceglie un servizio Modello dati modulo, vengono visualizzati più campi in cui è possibile mappare gli oggetti modulo con i parametri di input e output per il servizio specificato. Vedi regola di esempio per richiamare i servizi del modello dati modulo (FDM).

Oltre al servizio Modello dati modulo, è possibile specificare un URL WSDL diretto per richiamare un servizio Web. Tuttavia, un servizio di modello dati modulo presenta molti vantaggi e l’approccio consigliato per richiamare un servizio.

Per ulteriori informazioni sulla configurazione dei servizi nel modello dati modulo (FDM), consulta [[!DNL Experience Manager Forms] Integrazione dei dati](data-integration.md).

**[!UICONTROL Imposta valore di]** Calcola e imposta il valore dell&#39;oggetto specificato. È possibile impostare il valore dell&#39;oggetto su una stringa, il valore di un altro oggetto, il valore calcolato utilizzando un&#39;espressione matematica o una funzione, il valore di una proprietà di un oggetto o il valore di output di un servizio Form Data Model configurato. Quando si sceglie l&#39;opzione Servizio Web, vengono visualizzati tutti i servizi configurati in tutti i modelli di dati del modulo (FDM) nel [!DNL Experience Manager] dell&#39;istanza. Quando si sceglie un servizio Modello dati modulo, vengono visualizzati più campi in cui è possibile mappare gli oggetti modulo con i parametri di input e output per il servizio specificato.

Per ulteriori informazioni sulla configurazione dei servizi nel modello dati modulo (FDM), consulta [[!DNL Experience Manager Forms] Integrazione dei dati](data-integration.md).

Il **[!UICONTROL Imposta proprietà]** tipo di regola consente di impostare il valore di una proprietà dell&#39;oggetto specificato in base a un&#39;azione condizione. È possibile impostare la proprietà su una delle seguenti opzioni:
* visibile (booleano)
* label.value (Stringa)
* label.visible (booleano)
* description (String)
* abilitato (booleano)
* readOnly (booleano)
* obbligatorio (booleano)
* screenReaderText (stringa)
* valido (booleano)
* errorMessage (stringa)
* impostazione predefinita (numero, stringa, data)
* enumNames (stringa)[])
* chartType (String)

Ad esempio, consente di definire regole per visualizzare la casella di testo quando si fa clic su un pulsante. Per definire una regola è possibile utilizzare una funzione personalizzata, un oggetto modulo, una proprietà oggetto o un output di servizio.

![Imposta proprietà](assets/set_property_rule_new.png)

Per definire una regola basata su una funzione personalizzata, seleziona **[!UICONTROL Uscita funzione]** dall&#39;elenco a discesa e trascinare una funzione personalizzata dall&#39;elenco **[!UICONTROL Funzioni]** scheda. Se l&#39;azione della condizione viene soddisfatta, la casella di immissione testo diventa visibile.

Per definire una regola basata su un oggetto modulo, selezionare **[!UICONTROL Oggetto modulo]** dall&#39;elenco a discesa e trascinare un oggetto modulo dal **[!UICONTROL Oggetti modulo]** scheda. Se l’azione della condizione viene soddisfatta, la casella di immissione testo diventa visibile nel modulo adattivo.

Una regola Imposta proprietà basata su una proprietà oggetto consente di rendere visibile la casella di input di testo in un modulo adattivo basato su un’altra proprietà oggetto inclusa nel modulo adattivo.

La figura seguente illustra un esempio di attivazione dinamica della casella di controllo in base al fatto che la casella di testo è nascosta o visualizzata in un modulo adattivo:

![Object, proprietà](assets/object_property_set_property_new.png)

**[!UICONTROL Cancella valore di]** Cancella il valore dell&#39;oggetto specificato.

**[!UICONTROL Imposta Fuoco]** Imposta lo stato attivo sull&#39;oggetto specificato.

**[!UICONTROL Invia modulo]** Invia il modulo.

**[!UICONTROL Reimposta]** Reimposta il modulo o l&#39;oggetto specificato.

**[!UICONTROL Convalida]** Convalida il modulo o l&#39;oggetto specificato.

**[!UICONTROL Aggiungi istanza]** Aggiunge un&#39;istanza del pannello o della riga di tabella ripetibile specificata.

**[!UICONTROL Rimuovi istanza]** Rimuove un&#39;istanza del pannello o della riga di tabella ripetibile specificata.

**[!UICONTROL Uscita funzione]** Definisce una regola basata su funzioni predefinite o personalizzate.

**[!UICONTROL Accedi a]** Passa ad altro <!--Interactive Communications,--> Forms adattivo, altre risorse come immagini o frammenti di documento o un URL esterno. <!-- For more information, see [Add button to the Interactive Communication](create-interactive-communication.md#addbuttontothewebchannel). -->

**[!UICONTROL Evento di invio]** Attiva azioni o comportamenti specifici in base a condizioni o eventi predefiniti.


### [!UICONTROL Imposta valore di] {#set-value-of}

Il **[!UICONTROL Imposta valore di]** tipo di regola consente di impostare il valore di un oggetto modulo a seconda che la condizione specificata sia soddisfatta o meno. Il valore può essere impostato sul valore di un altro oggetto, una stringa letterale, un valore derivato da un&#39;espressione matematica o una funzione, un valore di una proprietà di un altro oggetto o l&#39;output di un servizio del modello di dati modulo. Analogamente, è possibile verificare la presenza di una condizione su un componente, una stringa, una proprietà o valori derivati da una funzione o un&#39;espressione matematica.

Il **Imposta valore di** il tipo di regola non è disponibile per tutti gli oggetti modulo, ad esempio pannelli e pulsanti della barra degli strumenti. Una regola Set Value Of standard ha la seguente struttura:

Imposta il valore dell&#39;oggetto A su:

(stringa ABC) OR (proprietà dell&#39;oggetto X dell&#39;oggetto C) OR (valore di una funzione) OR (valore di un&#39;espressione matematica) OR (valore di output di un servizio di modello dati);

Quando (facoltativo):

(Condizione 1 E Condizione 2 E Condizione 3) è VERO;

Nell&#39;esempio seguente viene selezionato il valore di `Question2` as `True` e impostato il valore di `Result` as `correct`.

![Set-value-web-service](assets/set-value-web-service.png)

Esempio di Set Valore regola mediante l&#39;utilizzo del servizio Form Data Model.

### [!UICONTROL Mostrare] {#show}

Utilizzo di **[!UICONTROL Spettacolo]** tipo di regola, è possibile scrivere una regola per mostrare o nascondere un oggetto modulo a seconda che una condizione sia soddisfatta o meno. Il tipo di regola Mostra attiva anche l’azione Nascondi se la condizione non viene soddisfatta o restituisce `False`.

Una regola Show tipica è strutturata come segue:

`Show Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Hide Object A;`

### [!UICONTROL Nascondi] {#hide}

Simile al tipo di regola Mostra, puoi utilizzare **[!UICONTROL Nascondi]** tipo di regola per mostrare o nascondere un oggetto modulo in base al soddisfacimento o meno di una condizione. Il tipo di regola Nascondi attiva anche l&#39;azione Mostra nel caso in cui la condizione non sia soddisfatta o restituisca `False`.

Una tipica regola Nascondi è strutturata come segue:

`Hide Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Show Object A;`

### [!UICONTROL Abilita] {#enable}

Il **[!UICONTROL Abilita]** tipo di regola consente di abilitare o disabilitare un oggetto modulo a seconda che una condizione sia soddisfatta o meno. Il tipo di regola Enable attiva anche l&#39;azione Disable nel caso in cui la condizione non sia soddisfatta o restituisca `False`.

Una regola di abilitazione tipica è strutturata come segue:

`Enable Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Disable Object A;`

### [!UICONTROL Disattiva] {#disable}

Simile al tipo di regola Abilita, il **[!UICONTROL Disattiva]** tipo di regola consente di abilitare o disabilitare un oggetto modulo a seconda che una condizione sia soddisfatta o meno. Il tipo di regola Disable attiva anche l’azione Enable nel caso in cui la condizione non sia soddisfatta o restituisca `False`.

Una regola di Disattivazione tipica è strutturata come segue:

`Disable Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Enable Object A;`

### [!UICONTROL Convalida] {#validate}

Il **[!UICONTROL Convalida]** tipo di regola convalida il valore in un campo utilizzando un&#39;espressione. È ad esempio possibile scrivere un&#39;espressione per verificare che la casella di testo per specificare il nome non contenga caratteri o numeri speciali.

Una regola di convalida tipica è strutturata come segue:

`Validate Object A;`

`Using:`

`(Expression 1 AND Expression 2 AND Expression 3) is TRUE;`

>[!NOTE]
>
>Se il valore specificato non è conforme alla regola di convalida, è possibile visualizzare un messaggio di convalida per l&#39;utente. Puoi specificare il messaggio nel **[!UICONTROL Messaggio di convalida script]** nelle proprietà del componente nella barra laterale.

![Convalida script](assets/script-validation.png)

<!--
### [!UICONTROL Set Options Of] {#setoptionsof}

The **[!UICONTROL Set Options Of]** rule type enables you to define rules to add check boxes dynamically to the Adaptive Form. You can use a Form Data Model or a custom function to define the rule.

To define a rule based on a custom function, select **[!UICONTROL Function Output]** from the drop-down list, and drag-and-drop a custom function from the **[!UICONTROL Functions]** tab. The number of checkboxes defined in the custom function are added to the Adaptive Form.

![Custom Functions](assets/custom_functions_set_options_new.png)

To create a custom function, see [custom functions in rule editor](#custom-functions).

To define a rule based on a form data model:

1. Select **[!UICONTROL Service Output]** from the drop-down list.
1. Select the data model object.
1. Select a data model object property from the **[!UICONTROL Display Value]** drop-down list. The number of checkboxes in the Adaptive Form is derived from the number of instances defined for that property in the database.
1. Select a data model object property from the **[!UICONTROL Save Value]** drop-down list.

![FDM set options](assets/fdm_set_options_new.png) -->

## Interfaccia utente dell’editor di regole {#understanding-the-rule-editor-user-interface}

L’editor di regole fornisce un’interfaccia utente completa ma semplice per scrivere e gestire le regole. Puoi avviare l’interfaccia utente dell’editor di regole da un modulo adattivo in modalità di authoring.

Per avviare l’interfaccia utente dell’editor di regole:

1. Apri un modulo adattivo in modalità di authoring.
1. Selezionare l&#39;oggetto modulo per il quale si desidera scrivere una regola e nella barra degli strumenti del componente selezionare ![edit-rules](assets/edit-rules-icon.svg). Viene visualizzata l’interfaccia utente dell’editor di regole.

   ![create-rules](assets/create-rules.png)

   Tutte le regole esistenti sugli oggetti modulo selezionati sono elencate in questa visualizzazione. Per informazioni sulla gestione delle regole esistenti, consulta [Gestisci regole](rule-editor.md#p-manage-rules-p).

1. Seleziona **[!UICONTROL Crea]** per scrivere una nuova regola. L’editor visivo dell’interfaccia utente dell’editor di regole si apre per impostazione predefinita quando si avvia l’editor di regole la prima volta.

   ![Interfaccia utente dell’editor delle regole](assets/rule-editor-ui.png)

Esaminiamo in dettaglio ogni componente dell’interfaccia utente dell’editor di regole.

### A. Visualizzazione delle regole dei componenti {#a-component-rule-display}

Visualizza il titolo dell&#39;oggetto modulo adattivo tramite il quale è stato avviato l&#39;editor di regole e il tipo di regola attualmente selezionato. Nell’esempio precedente, l’editor di regole viene avviato da un oggetto Modulo adattivo denominato Domanda 1 e il tipo di regola selezionato è Quando.

### B. Oggetti e funzioni del modulo {#b-form-objects-and-functions-br}

Il riquadro a sinistra nell’interfaccia utente dell’editor di regole include due schede: **[!UICONTROL Oggetti Forms]** e **[!UICONTROL Funzioni]**.

La scheda Oggetti modulo mostra una vista gerarchica di tutti gli oggetti contenuti nel modulo adattivo. Visualizza il titolo e il tipo degli oggetti. Durante la scrittura di una regola, è possibile trascinare gli oggetti modulo nell’editor di regole. Quando si trascina un oggetto o una funzione in un segnaposto durante la creazione o la modifica di una regola, il segnaposto assume automaticamente il tipo di valore appropriato.

Gli oggetti modulo a cui sono applicate una o più regole valide sono contrassegnati da un punto verde. Se una delle regole applicate a un oggetto modulo non è valida, l&#39;oggetto modulo viene contrassegnato con un punto giallo.

La scheda Funzioni include un set di funzioni incorporate, ad esempio Somma di, Min di, Max di, Media di, Numero di e Convalida modulo. È possibile utilizzare queste funzioni per calcolare i valori nei pannelli e nelle righe di tabella ripetibili e utilizzarli nelle istruzioni di azione e condizione durante la scrittura delle regole. Tuttavia, puoi anche creare funzioni personalizzate.

Nella figura sono illustrate alcune delle funzioni elencate di seguito:

![Scheda Funzioni](assets/functions.png)

>[!NOTE]
>
>È possibile eseguire la ricerca di testo su oggetti e funzioni, nomi e titoli nelle schede Oggetti e funzioni di Forms.

Nell&#39;albero sinistro degli oggetti modulo è possibile selezionare gli oggetti modulo per visualizzare le regole applicate a ciascuno degli oggetti. Non solo è possibile spostarsi tra le regole dei vari oggetti modulo, ma è anche possibile copiare e incollare le regole tra gli oggetti modulo. Per ulteriori informazioni, consulta [Regole di copia e incolla](rule-editor.md#p-copy-paste-rules-p).

### C. Attivazione/disattivazione di funzioni e oggetti modulo {#c-form-objects-and-functions-toggle-br}

Quando viene toccato, questo pulsante attiva o disattiva il riquadro delle funzioni e degli oggetti del modulo.

### D. Editor di regole visive {#visual-rule-editor}

L’editor di regole visive è l’area in cui si scrivono le regole nella modalità editor visivo dell’interfaccia utente dell’editor di regole. Ti consente di selezionare un tipo di regola e di definire di conseguenza condizioni e azioni. Quando si definiscono condizioni e azioni in una regola, è possibile trascinare gli oggetti modulo e le funzioni dal riquadro Oggetti modulo e funzioni.

Per ulteriori informazioni sull’utilizzo dell’editor di regole visive, consulta [Scrivi regole](rule-editor.md#p-write-rules-p).
<!-- 
### E. Visual-code editors switcher {#e-visual-code-editors-switcher}

Users in the forms-power-users group can access code editor. For other users, code editor is not available. If you have the rights, you can switch from visual editor mode to code editor mode of the rule editor, and conversely, using the switcher right above the rule editor. When you launch rule editor the first time, it opens in the visual editor mode. You can write rules in the visual editor mode or switch to the code editor mode to write a rule script. However, note that if you modify a rule or write a rule in code editor, you cannot switch back to the visual editor for that rule unless you clear the code editor.

[!DNL Experience Manager Forms] tracks the rule editor mode you used last to write a rule. When you launch the rule editor next time, it opens in that mode. However, you can also configure a default mode to open the rule editor in the specified mode. To do so:

1. Go to [!DNL Experience Manager] web console at `https://[host]:[port]/system/console/configMgr`.
1. Click to edit **[!UICONTROL Adaptive Form Configuration Service]**.
1. choose **[!UICONTROL Visual Editor]** or **[!UICONTROL Code Editor]** from the **[!UICONTROL Default Mode for Rule Editor]** drop-down

1. Click **[!UICONTROL Save]**.
-->

### E. Tasti Done e cancel {#done-and-cancel-buttons}

Il **[!UICONTROL Fine]** per salvare una regola. È possibile salvare una regola incompleta. Tuttavia, gli incompleti vengono non valido e non vengono eseguiti. Le regole salvate in un oggetto modulo vengono elencate quando si lanciare la regola editor successiva dallo stesso oggetto modulo. È possibile gestire regole esistenti in questa visualizzazione. Per ulteriori informazioni, vedere [Gestire le regole](rule-editor.md#p-manage-rules-p).

Il **[!UICONTROL Annulla]** pulsante elimina tutte le modifiche apportate a un regola e chiude il regola editor.

## Scrivere regole {#write-rules}

È possibile scrivere regole utilizzando i regola editor visivi <!-- or the code editor. When you launch the rule editor the first time, it opens in the visual editor mode. You can switch to the code editor mode and write rules. However, if you write or modify a rule in code editor, you cannot switch to the visual editor for that rule unless you clear the code editor. When you launch the rule editor next time, it opens in the mode that you used last to create rule. -->

Vediamo innanzitutto come scrivere regole utilizzando l’editor visivo.

### Utilizzo dell’editor visivo {#using-visual-editor}

Comprendiamo come creare una regola nell’editor visivo utilizzando il seguente modulo di esempio.

![Create-rule-example](assets/create-rule-example.png)

La sezione Requisiti di prestito nel modulo di applicazione di prestito di esempio richiede ai richiedenti di specificare il proprio stato civile, lo stipendio e, se sposati, lo stipendio del coniuge. In base agli input dell’utente, la regola calcola l’importo di idoneità al prestito e viene visualizzata nel campo Idoneità al prestito. Per implementare lo scenario, applica le seguenti regole:

* Il campo Stipendio coniuge viene visualizzato solo quando lo stato civile è sposato.
* L’importo di ammissibilità al prestito è pari al 50% dello stipendio totale.

Per scrivere le regole, effettua le seguenti operazioni:

1. Innanzitutto, scrivi la regola per controllare la visibilità del campo Stipendio coniuge in base all’opzione selezionata dall’utente per il pulsante di opzione Stato civile.

   Apri il modulo di richiesta di prestito in modalità di creazione. Seleziona la **[!UICONTROL Stato civile]** componente e seleziona ![edit-rules](assets/edit-rules-icon.svg). Quindi, seleziona **[!UICONTROL Crea]** per avviare l’editor di regole.

   ![write-rules-visual-editor-1](assets/write-rules-visual-editor-1-cc.png)

   Quando si avvia l&#39;editor di regole, la regola When è selezionata per impostazione predefinita. Inoltre, l&#39;oggetto modulo (in questo caso, Stato civile) da cui è stato avviato l&#39;editor di regole è specificato nell&#39;istruzione When.

   Sebbene non sia possibile modificare l&#39;oggetto selezionato, è possibile utilizzare l&#39;elenco a discesa delle regole, come illustrato di seguito, per selezionare un altro tipo di regola. Se desideri creare una regola su un altro oggetto, seleziona Annulla per uscire dall’editor di regole e riavviarlo dall’oggetto modulo desiderato.

1. Seleziona **[!UICONTROL Seleziona stato]** a discesa e selezionare **[!UICONTROL è uguale a]**. Il **[!UICONTROL Inserisci una stringa]** viene visualizzato.

   ![write-rules-visual-editor-2](assets/write-rules-visual-editor-2-cc.png)

<!--  In the Marital Status radio button, **[!UICONTROL Married]** and **[!UICONTROL Single]** options are assigned **0** and **1** values, respectively. You can verify assigned values in the Title tab of the Edit radio button dialog as shown below.

   ![Radio button values from rule editor](assets/radio-button-values.png)-->

1. In **[!UICONTROL Inserisci una stringa]** nella regola, seleziona **Coniugato** dal menu a discesa.

   ![write-rules-visual-editor-4](assets/write-rules-visual-editor-4-cc.png)

   La condizione è stata definita come `When Marital Status is equal to Married`. Quindi, definisci l’azione da eseguire se questa condizione è True.

1. Nell&#39;istruzione Then, selezionare **[!UICONTROL Spettacolo]** dal **[!UICONTROL Seleziona azione]** a discesa.

   ![write-rules-visual-editor-5](assets/write-rules-visual-editor-5-cc.png)

1. Trascina la selezione **[!UICONTROL Stipendio coniuge]** dalla scheda Oggetti modulo nella **[!UICONTROL Rilascia l&#39;oggetto o seleziona qui]** campo. In alternativa, seleziona la **[!UICONTROL Rilascia l&#39;oggetto o seleziona qui]** e selezionare il **[!UICONTROL Stipendio coniuge]** dal menu a comparsa, che elenca tutti gli oggetti modulo del modulo.

   ![write-rules-visual-editor-6](assets/write-rules-visual-editor-6-cc.png)

   Quindi, definisci l’azione da eseguire se questa condizione è False.
1. Clic **[!UICONTROL Aggiungi sezione Else]** per aggiungere un&#39;altra condizione per **[!UICONTROL Stipendio coniuge]** nel caso in cui si seleziona Stato civile come singolo.

   ![when-else](assets/when-else.png)

1. Nell&#39;istruzione Else, selezionare **[!UICONTROL Nascondi]** dal **[!UICONTROL Seleziona azione]** a discesa.
   ![when-else](assets/when-else-1.png)

1. Trascina la selezione **[!UICONTROL Stipendio coniuge]** dalla scheda Oggetti modulo nella **[!UICONTROL Rilascia l&#39;oggetto o seleziona qui]** campo. In alternativa, seleziona la **[!UICONTROL Rilascia l&#39;oggetto o seleziona qui]** e selezionare il **[!UICONTROL Stipendio coniuge]** dal menu a comparsa, che elenca tutti gli oggetti modulo del modulo.
   ![when-else](assets/when-else-2.png)

   La regola viene visualizzata come segue nell’editor di regole.

   ![write-rules-visual-editor-7](assets/write-rules-visual-editor-7-cc.png)



1. Seleziona **[!UICONTROL Fine]** per salvare la regola.

<!--
1. Repeat steps 1 through 5 to define another rule to hide the Spouse Salary field if the marital Status is Single. The rule appears as follows in the rule editor.

   ![write-rules-visual-editor-8](assets/write-rules-visual-editor-8-cc.png) -->

>[!NOTE]
>
> In alternativa, è possibile scrivere una regola Mostra nel campo Stipendio coniuge, anziché una regola Quando nel campo Stato civile, per implementare lo stesso comportamento.

![write-rules-visual-editor-9](assets/write-rules-visual-editor-9-cc.png)

1. Scrivere quindi una regola per calcolare l&#39;importo dell&#39;idoneità al prestito, che corrisponde al 50% dello stipendio totale, e visualizzarlo nel campo Idoneità al prestito. Per ottenere questo risultato, crea **[!UICONTROL Imposta valore di]** regole sul campo Ammissibilità al prestito.

   In modalità authoring, seleziona la **[!UICONTROL Ammissibilità al prestito]** e seleziona ![edit-rules](assets/edit-rules-icon.svg). Quindi, seleziona **[!UICONTROL Crea]** per avviare l’editor di regole.

1. Seleziona **[!UICONTROL Imposta valore di]** regola dal menu a discesa regola.

   ![write-rules-visual-editor-10](assets/write-rules-visual-editor-10-cc.png)

1. Seleziona **[!UICONTROL Seleziona opzione]** e seleziona **[!UICONTROL Espressione matematica]**. Viene aperto un campo per scrivere espressioni matematiche.

   ![write-rules-visual-editor-11](assets/write-rules-visual-editor-11-cc.png)

1. Nel campo espressione:

   * Seleziona o trascina dalla scheda Oggetto Forms il **[!UICONTROL Salario]** campo nel primo **[!UICONTROL Rilascia l&#39;oggetto o seleziona qui]** campo.

   * Seleziona **[!UICONTROL Più]** dal **[!UICONTROL Seleziona operatore]** campo.

   * Seleziona o trascina dalla scheda Oggetto Forms il **[!UICONTROL Stipendio coniuge]** campo nell&#39;altro **[!UICONTROL Rilascia l&#39;oggetto o seleziona qui]** campo.

   ![write-rules-visual-editor-12](assets/write-rules-visual-editor-12.png)

1. Quindi, seleziona nell’area evidenziata intorno al campo espressione e seleziona **[!UICONTROL Estendi estensione]**.

   ![write-rules-visual-editor-13](assets/write-rules-visual-editor-13-cc.png)

   Nel campo espressione estesa, seleziona **[!UICONTROL diviso per]** dal **[!UICONTROL Seleziona operatore]** campo e **[!UICONTROL Numero]** dal **[!UICONTROL Seleziona opzione]** campo. Quindi, specifica **[!UICONTROL 2]** nel campo numerico.

   ![write-rules-visual-editor-14](assets/write-rules-visual-editor-14-cc.png)

   >[!NOTE]
   >
   >È possibile creare espressioni complesse utilizzando componenti, funzioni, espressioni matematiche e valori di proprietà dal campo Seleziona opzione.

   Successivo, creare una condizione che, quando restituisce True, viene eseguita l&#39;espressione.

1. Selezionare **[!UICONTROL Aggiungi condizione]** per aggiungere un&#39;istruzione Quando.

   ![write-rules-visual-editor-15](assets/write-rules-visual-editor-15-cc.png)

   Nell&#39;istruzione When:

   * Seleziona o trascina dalla scheda Oggetto Forms il **[!UICONTROL Stato civile]** campo nel primo **[!UICONTROL Rilascia l&#39;oggetto o seleziona qui]** campo.

   * Seleziona **[!UICONTROL è uguale a]** dal **[!UICONTROL Seleziona operatore]** campo.

   * Seleziona stringa nell’altro **[!UICONTROL Rilascia l&#39;oggetto o seleziona qui]** e specificare **[!UICONTROL Coniugato]** nel **[!UICONTROL Inserisci una stringa]** campo.

   La regola viene infine visualizzata come segue nell’editor di regole.  ![write-rules-visual-editor-16](assets/write-rules-visual-editor-16-cc.png)

1. Seleziona **[!UICONTROL Fine]**. Salva la regola.

1. Ripetere i passaggi da 7 a 14 per definire un&#39;altra regola per calcolare l&#39;idoneità al prestito se lo stato civile è Single. La regola viene visualizzata come segue nell’editor di regole.

   ![write-rules-visual-editor-17](assets/write-rules-visual-editor-17-cc.png)

In alternativa, è possibile utilizzare la regola Imposta valore di per calcolare l&#39;idoneità al prestito nella regola Quando creata per mostrare-nascondere il campo Stipendio coniuge. La regola combinata risultante quando Stato civile è Singolo viene visualizzata come segue nell’editor delle regole.

![write-rules-visual-editor-18](assets/write-rules-visual-editor-18-cc.png)

È possibile scrivere una regola combinata per controllare la visibilità del campo Stipendio coniuge e calcolare l&#39;idoneità al prestito quando lo stato civile è Sposato utilizzando la condizione Else.

![write-rules-visual-editor-19](assets/write-rules-visual-editor-19-cc.png)


<!-- ### Using code editor {#using-code-editor}

Users added to the forms-power-users group can use code editor. The rule editor auto generates the JavaScript code for any rule you create using visual editor. You can switch from visual editor to the code editor to view the generated code. However, if you modify the rule code in the code editor, you cannot switch back to the visual editor. If you prefer writing rules in code editor rather than visual editor, you can write rules afresh in the code editor. The visual-code editors switcher helps you switch between the two modes.

The code editor JavaScript is the expression language of Adaptive Forms. All the expressions are valid JavaScript expressions and use Adaptive Forms scripting model APIs. These expressions return values of certain types. For the complete list of Adaptive Forms classes, events, objects, and public APIs, see [JavaScript Library API reference for Adaptive Forms](https://helpx.adobe.com/experience-manager/6-5/forms/javascript-api/index.html).

For more information about guidelines to write rules in the code editor, see [Adaptive Form Expressions](adaptive-form-expressions.md).

While writing JavaScript code in the rule editor, the following visual cues help you with the structure and syntax:

* Syntax highlights

* Auto Indentation

* Hints and suggestions for Form objects, functions, and their properties

* Auto completion of form component names and common JavaScript functions

![javascriptruleeditor](assets/javascriptruleeditor.png)
-->

#### Funzioni personalizzate nell’editor di regole {#custom-functions}

Oltre alle funzioni predefinite, come *Somma di* che sono elencati in **Output funzioni**, nell’editor delle regole puoi anche utilizzare funzioni personalizzate. L’editor di regole supporta la sintassi JavaScript ECMAScript 2019 per gli script e le funzioni personalizzate. Per istruzioni sulla creazione di funzioni personalizzate, consulta l’articolo [Funzioni personalizzate in Adaptive Forms](/help/forms/using/create-and-use-custom-functions-core-components.md)

<!--

Ensure that the function you write is accompanied by the `jsdoc` above it. Adaptive Form supports the various [JavaScript annotations for custom functions](/help/forms/create-and-use-custom-functions.md#js-annotations).

For more information, see [jsdoc.app](https://jsdoc.app/).

Accompanying `jsdoc` is required:

* If you want custom configuration and description
* Because there are multiple ways to declare a function in `JavaScript,` and comments let you keep a track of the functions.

Supported `jsdoc` tags:

* **Private**
  Syntax: `@private`
  A private function is not included as a custom function.

* **Name**
  Syntax: `@name funcName <Function Name>`
  Alternatively `,` you can use: `@function funcName <Function Name>` **or** `@func` `funcName <Function Name>`.
  `funcName` is the name of the function (no spaces allowed).
  `<Function Name>` is the display name of the function.

* **Parameter**
  Syntax: `@param {type} name <Parameter Description>`
  Alternatively, you can use: `@argument` `{type} name <Parameter Description>` **or** `@arg` `{type}` `name <Parameter Description>`.
  Shows parameters used by the function. A function can have multiple parameter tags, one tag for each parameter in the order of occurrence.
  `{type}` represents parameter type. Allowed parameter types are:

    1. string
    2. number
    3. boolean
    4. scope
    5. string[]
    6. number[]
    7. boolean[]
    8. date
    9. date[]
    10. array
    11. object

   `scope` refers to a special globals object which is provided by forms runtime. It must be the last parameter and is not be visible to the user in the rule editor. You can use scope to access readable form and field proxy object to read properties, event which triggered the rule and a set of functions to manipulate the form.

   `object` type is used to pass readable field object in parameter to a custom function instead of passing the value.

   All parameter types are categorized under one of the above. None is not supported. Ensure that you select one of the types above. Types are not case-sensitive. Spaces are not allowed in the parameter name.  Parameter description can have multiple words.

* **Optional Parameter**
Syntax: `@param {type=} name <Parameter Description>` 
Alternatively, you can use: `@param {type} [name] <Parameter Description>`
By default all parameters are mandatory. You can mark a parameter optional by adding `=` in type of the parameter or by putting param name in square brackets.
   
   For example, let us declare `Input1` as optional parameter:
    * `@param {type=} Input1`
    * `@param {type} [Input1]`

* **Return Type**
  Syntax: `@return {type}`
  Alternatively, you can use `@returns {type}`.
  Adds information about the function, such as its objective.
  {type} represents the return type of the function. Allowed return types are:

    1. string
    2. number
    3. boolean
    4. string[]
    5. number[]
    6. boolean[]
    7. date
    8. date[]
    9. array
    10. object

  All other return types are categorized under one of the above. None is not supported. Ensure that you select one of the types above. Return types are not case-sensitive.

**Adding a custom function**

For example, you want to add a custom function which calculates area of a square. Side length is the user input to the custom function, which is accepted using a numeric box in your form. The calculated output is displayed in another numeric box in your form. To add a custom function, you have to first create a client library, and then add it to the CRX repository.

To create a client library and add it in the CRX repository, perform the following steps:

1. Create a client library. For more information, see [Using Client-Side Libraries](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html#developing).
2. In CRXDE, add a property `categories`with string type value as `customfunction` to the `clientlib` folder.

   >[!NOTE]
   >
   >`customfunction`is an example category. You can choose any name for the category you create in the `clientlib`folder.

After you have added your client library in the CRX repository, use it in your Adaptive Form. It lets you use your custom function as a rule in your form. To add the client library in your Adaptive Form, perform the following steps:

1. Open your form in edit mode.
   To open a form in edit mode, select a form and select **[!UICONTROL Open]**.
1. In the edit mode, select a component, then select ![field-level](assets/select_parent_icon.svg) &gt; **[!UICONTROL Adaptive Form Container]**, and then select ![cmppr](assets/configure-icon.svg).
1. In the sidebar, under Name of Client Library, add your client library. ( `customfunction` in the example.)

   ![Adding the custom function client library](assets/clientlib.png)

1. Select the input numeric box, and select ![edit-rules](assets/edit-rules-icon.svg) to open the rule editor.
1. Select **[!UICONTROL Create Rule]**. Using options shown below, create a rule to save the squared value of the input in the Output field of your form.

   [![Using custom functions to create a rule](assets/add_custom_rule_new.png)](assets/add-custom-rule.png)
  
1. Select **[!UICONTROL Done]**. Your custom function is added.

   >[!NOTE]
   >
   > To invoke a form data model from rule editor using custom functions, [see here](/help/forms/using-form-data-model.md#invoke-services-in-adaptive-forms-using-rules-invoke-services). 

#### Function declaration supported types {#function-declaration-supported-types}

**Function Statement**

```javascript
function area(len) {
    return len*len;
}
```

This function is included without `jsdoc` comments.

**Function Expression**

```javascript
var area;
//Some codes later
/** */
area = function(len) {
    return len*len;
};
```

**Function Expression and Statement**

```javascript
var b={};
/** */
b.area = function(len) {
    return len*len;
}
```

**Function Declaration as Variable**

```javascript
/** */
var x1,
    area = function(len) {
        return len*len;
    },
    x2 =5, x3 =true;
```

Limitation: custom function picks only the first function declaration from the variable list, if together. You can use function expression for every function declared.

**Function Declaration as Object**

```javascript
var c = {
    b : {
        /** */
        area : function(len) {
            return len*len;
        }
    }
};
```

>[!NOTE]
>
>Ensure that you use `jsdoc` for every custom function. Although `jsdoc`comments are encouraged, include an empty `jsdoc`comment to mark your function as custom function. It enables default handling of your custom function.

-->

## Gestisci regole {#manage-rules}

Tutte le regole esistenti su un oggetto modulo vengono elencate quando si seleziona l&#39;oggetto e si seleziona ![edit-rules1](assets/edit-rules-icon.svg). Puoi visualizzare il titolo e un’anteprima del riepilogo delle regole. Inoltre, l’interfaccia utente consente di espandere e visualizzare il riepilogo completo delle regole, modificarne l’ordine, modificarne le regole ed eliminarle.

![Regole elenco](assets/list-rules-cc.png)

Puoi eseguire le seguenti azioni sulle regole:

* **Espandi/Comprimi**: la colonna Contenuto nell’elenco delle regole visualizza il contenuto della regola. Se l&#39;intero contenuto della regola non è visibile nella vista predefinita, seleziona ![expand-rule-content](assets/Smock_ChevronDown.svg) per espanderlo.

* **Riordina**: tutte le nuove regole create vengono impilate nella parte inferiore dell’elenco di regole. Le regole vengono eseguite dall&#39;alto verso il basso. La regola in alto viene eseguita per prima, seguita da altre regole dello stesso tipo. Ad esempio, se disponi di regole When, Show, Enable e When rispettivamente in prima, seconda, terza e quarta posizione dall&#39;alto, la regola When nella parte superiore viene eseguita per prima seguita dalla regola When nella quarta posizione. Vengono quindi eseguite le regole Mostra e Abilita.
Per modificare l’ordine di una regola, tocca ![sort-rules](assets/sort-rules.svg) o trascinarlo nell&#39;ordine desiderato nell&#39;elenco.

* **Modifica**: per modificare una regola, seleziona la casella di controllo accanto al titolo della regola. Vengono visualizzate le opzioni per modificare ed eliminare la regola. Seleziona **[!UICONTROL Modifica]** per aprire la regola selezionata nell’editor di regole <!-- in visual  or code editor mode depending on the mode used to create the rule -->.

* **Elimina**: per eliminare una regola, selezionala e seleziona **[!UICONTROL Elimina]**.

* **Attiva/Disattiva**: quando devi sospendere temporaneamente l’utilizzo di una regola, puoi selezionare una o più regole e selezionare **[!UICONTROL Disattiva]** nella barra degli strumenti Azioni per disattivarli. Se una regola è disabilitata, non viene eseguita in fase di esecuzione. Per abilitare una regola disabilitata, selezionala e seleziona Abilita nella barra degli strumenti delle azioni. La colonna di stato della regola indica se la regola è abilitata o disabilitata.

![Disattiva regola](assets/disablerule-cc.png)

## Regole di copia e incolla {#copy-paste-rules}

Per risparmiare tempo, puoi copiare e incollare una regola da un campo ad altri campi simili.

Per copiare e incollare le regole, effettuare le seguenti operazioni:

1. Seleziona l’oggetto modulo da cui desideri copiare una regola, quindi nella barra degli strumenti del componente seleziona ![modifica regola](assets/edit-rules-icon.svg). Viene visualizzata l’interfaccia utente dell’editor di regole con l’oggetto modulo selezionato e le regole esistenti.

   ![copia regola](assets/copyrule.png)

   Per informazioni sulla gestione delle regole esistenti, consulta [Gestisci regole](rule-editor.md#p-manage-rules-p).

1. Selezionare la casella di controllo accanto al titolo della regola per visualizzare le opzioni per la gestione della regola. Seleziona **[!UICONTROL Copia]**.

   ![copyrule2](assets/copyrule2.png)

1. Selezionare un altro oggetto modulo in cui si desidera incollare la regola e selezionare **[!UICONTROL Incolla]**. Inoltre, puoi modificare la regola per apportarvi modifiche.

   >[!NOTE]
   >
   >È possibile incollare una regola in un altro oggetto modulo solo se tale oggetto supporta l&#39;evento della regola copiata. Ad esempio, un pulsante supporta l’evento clic. È possibile incollare una regola con un evento clic su un pulsante ma non su una casella di controllo.

1. Seleziona **[!UICONTROL Fine]** per salvare la regola.

## Espressioni nidificate {#nestedexpressions}

L’editor di regole consente di utilizzare più operatori AND e OR per creare regole nidificate. È possibile combinare più operatori AND e OR nelle regole.

Di seguito è riportato un esempio di regola nidificata che visualizza un messaggio per l’utente sull’idoneità per la custodia di un bambino quando vengono soddisfatte le condizioni richieste.

![Espressione complessa](assets/complexexpression.png)

Puoi anche trascinare le condizioni all’interno di una regola per modificarla. Seleziona e passa il puntatore sull&#39;handle ( ![maniglia](assets/drag-handle.svg)) prima di una condizione. Una volta che il puntatore si trasforma nel simbolo della mano, come illustrato di seguito, trascinare e rilasciare la condizione in qualsiasi punto della regola. La struttura della regola cambia.

![Trascinamento della selezione](assets/drag-and-drop.png)

## Condizioni dell&#39;espressione data {#dateexpression}

La regola editor consente di utilizzare i confronti di date per creare condizioni.

Di seguito è riportata una condizione di esempio che visualizza un oggetto di testo statico se l&#39;ipoteca sulla casa è già stata presa, che il utente indica compilando il campo data.

Quando la data di ipoteca dell&#39;immobile compilata dal utente è passata, il modulo adattivo visualizza una nota sul calcolo del reddito. Nella regola seguente viene confrontata la data compilata dall&#39;utente con la data corrente e se la data compilata dal utente è precedente alla data corrente, nel modulo viene visualizzato il messaggio di testo (denominato Reddito).

![Condizione espressione data](assets/dateexpressioncondition.png)

Quando la data di compilazione è precedente alla data corrente, nel modulo viene visualizzato il messaggio di testo (Entrate) nel modo seguente:

![Condizione espressione data soddisfatta](assets/dateexpressionconditionmet.png)

## Condizioni di confronto dei numeri {#number-comparison-conditions}

L’editor di regole consente di creare condizioni che confrontano due numeri.

Di seguito è riportata una condizione di esempio che visualizza un oggetto di testo statico se il numero di mesi in cui un richiedente soggiorna all&#39;indirizzo corrente è inferiore a 36.

![Condizione di confronto dei numeri](assets/numbercomparisoncondition.png)

Quando l’utente indica di vivere all’attuale indirizzo residenziale per meno di 36 mesi, il modulo mostra una notifica che indica che è possibile richiedere più prove di residenza.

![È richiesta un’altra bozza](assets/additionalproofrequested.png)

<!-- ## Impact of rule editor on existing scripts {#impact-of-rule-editor-on-existing-scripts}

In [!DNL Experience Manager Forms] versions prior to [!DNL Experience Manager 6.1 Forms] feature pack 1, form authors and developers used to write expressions in the Scripts tab of the Edit component dialog to add dynamic behavior to Adaptive Forms. The Scripts tab is now replaced by the rule editor.

Any scripts or expressions that you must have written in the Scripts tab are available in the rule editor. While you cannot view or edit them in visual editor, if you are a part of the forms-power-users group you can edit scripts in code editor. -->

## Regole di esempio {#example}

### Richiama servizio modello dati modulo {#invoke}

Considerare un servizio Web `GetInterestRates` che prende l&#39;importo del prestito, la locazione e il punteggio di credito del richiedente come input e restituisce un piano di prestito che include l&#39;importo dell&#39;IME e il tasso di interesse. È possibile creare un modello dati modulo (FDM) utilizzando il servizio Web come origine dati. Si aggiungono oggetti modello dati e un `get` servizio al modello di modulo. Il servizio viene visualizzato nella scheda Servizi del modello dati del modulo (FDM). Quindi, crea un modulo adattivo che includa i campi dagli oggetti modello dati per acquisire gli input dell’utente per l’importo del prestito, la durata e il punteggio di credito. Aggiungi un pulsante che attiva il servizio web per recuperare i dettagli del piano. L’output viene compilato nei campi appropriati.

La regola seguente mostra come configurare l’azione Richiama servizio per eseguire lo scenario di esempio.

![Example-invoke-services](assets/example-invoke-services.png)

>[!NOTE]
>
>Se l’input è di tipo array, i campi che supportano gli array sono visibili nella sezione a discesa Output.

### Attivazione di più azioni tramite la regola When {#triggering-multiple-actions-using-the-when-rule}

In un modulo di richiesta di prestito, si desidera stabilire se il richiedente è un cliente esistente o meno. In base alle informazioni fornite dall&#39;utente, il campo ID cliente deve essere visualizzato o nascosto. Inoltre, se l’utente è un cliente esistente, imposta il campo ID cliente come elemento attivo. Il modulo di richiesta di prestito presenta le seguenti componenti:

* Un pulsante di opzione, **[!UICONTROL Sei già un cliente del Geometrixx?]**, che fornisce [!UICONTROL Sì] e [!UICONTROL No] opzioni. Il valore di Sì è **0** e No è **1**.

* Un campo di testo, **[!UICONTROL ID cliente Geometrixx]**, per specificare l&#39;ID cliente.

Quando scrivi una regola When sul pulsante di scelta per implementare questo comportamento, la regola viene visualizzata come segue nell’editor di regole visive.

![When-rule-example](assets/when-rule-example.png)

Regola nell’editor visivo

Nella regola di esempio, l&#39;istruzione nella sezione When è la condizione che, quando restituisce True, esegue le azioni specificate nella sezione Then.

<!-- The rule appears as follows in the code editor.

![when-rule-example-code](assets/when-rule-example-code.png) 

Rule in the code editor -->

### Utilizzo di un output di funzione in una regola {#using-a-function-output-in-a-rule}

In un modulo ordine fornitore è disponibile la tabella seguente, in cui gli utenti compilano i propri ordini. In questa tabella:

* La prima riga è ripetibile, in modo che gli utenti possano ordinare più prodotti e specificare quantità diverse. Il nome elemento è `Row1`.
* Il titolo della cella nella colonna Quantità prodotto della riga ripetibile è Quantità. Il nome elemento per questa cella è `productquantity`.
* La seconda riga della tabella non è ripetibile e il titolo della cella nella colonna Quantità prodotto di questa riga è Quantità totale.

![Esempio-tabella-funzione](assets/example-function-table.png)

**R.** Riga 1 **B.** Quantità **C.** Quantità totale

Ora si desidera aggiungere le quantità specificate nella colonna Quantità prodotto per tutti i prodotti e visualizzare la somma nella cella Quantità totale. È possibile ottenere tale somma scrivendo una regola Imposta valore di nella cella Quantità totale come illustrato di seguito.

![Esempio-funzione-output](assets/example-function-output.png)

Regola nell’editor visivo

<!-- he rule appears as follows in the code editor.

![example-function-output-code](assets/example-function-output-code.png)

Rule in the code editor -->

### Convalida di un valore di campo tramite espressione {#validating-a-field-value-using-expression}

Nel modulo dell&#39;ordine di acquisto illustrato nell&#39;esempio precedente, si desidera impedire agli utenti di ordinare più di una quantità di qualsiasi prodotto il cui prezzo sia superiore a 10000. Per eseguire questa convalida, è possibile scrivere una regola di convalida come illustrato di seguito.

![Esempio di convalida](assets/example-validate.png)
Regola nell’editor visivo

<!-- The rule appears as follows in the code editor.

![example-validate-code](assets/example-validate-code.png)

Rule in the code editor -->
