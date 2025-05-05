---
title: Creare e aggiungere funzioni personalizzate in un modulo adattivo
description: AEM Forms supporta funzioni personalizzate che consentono agli utenti di creare e utilizzare le proprie funzioni all’interno dell’editor di regole.
keywords: Aggiungi una funzione personalizzata, utilizza una funzione personalizzata, crea una funzione personalizzata, utilizza la funzione personalizzata nell’editor di regole.
content-type: reference
feature: Adaptive Forms, Core Components
role: Admin, User, Developer
exl-id: 00073e3a-f1b5-4c42-9fea-4a14b8a22c81
source-git-commit: 7f1283898cbeebdedb7bdea6f0a8d9db567617ee
workflow-type: tm+mt
source-wordcount: '3385'
ht-degree: 0%

---

# Funzioni personalizzate nei componenti core di Forms adattivi

Questo articolo descrive la creazione di funzioni personalizzate con il componente core Modulo adattivo più recente dotato delle funzioni più recenti, ad esempio:

* Funzione di memorizzazione in cache per funzioni personalizzate
* Supporto globale di oggetti di ambito e oggetti di campo per le funzioni personalizzate
* Supporto per le funzioni JavaScript moderne come le funzioni let e arrow (supporto ES10)

Assicurati di impostare la [versione più recente del modulo](https://github.com/adobe/aem-core-forms-components/tree/release/650) nell&#39;ambiente dei Componenti core AEM Forms per utilizzare le funzioni più recenti in Funzioni personalizzate. </span>


| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM 6.5 | Questo articolo |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/it/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/create-and-use-custom-functions) |

## Introduzione

AEM Forms 6.5 include funzioni JavaScript che ti consentono di definire regole di business complesse utilizzando l’editor di regole. AEM Forms offre diverse funzioni personalizzate predefinite; tuttavia, in molti casi è necessario definire funzioni personalizzate da utilizzare in più moduli. Queste funzioni personalizzate migliorano le funzionalità dei moduli consentendo la manipolazione e l&#39;elaborazione dei dati immessi per soddisfare requisiti specifici. Consentono inoltre di modificare dinamicamente il comportamento della forma in base ai criteri predefiniti.

### Utilizzo di funzioni personalizzate {#uses-of-custom-function}

I vantaggi dell’utilizzo di funzioni personalizzate nei componenti core di Forms adattivi sono:


* **Gestione dei dati**: le funzioni personalizzate gestiscono ed elaborano i dati immessi nei campi dei moduli.
* **Elaborazione dei dati**: le funzioni personalizzate consentono di elaborare i dati immessi nei campi dei moduli.
* **Convalida dei dati**: le funzioni personalizzate consentono di eseguire controlli personalizzati sugli input dei moduli e di fornire messaggi di errore specifici.
* **Comportamento dinamico**: le funzioni personalizzate consentono di controllare il comportamento dinamico dei moduli in base a condizioni specifiche. Ad esempio, è possibile visualizzare/nascondere campi, modificare i valori dei campi o modificare dinamicamente la logica del modulo.
* **Integrazione**: è possibile utilizzare funzioni personalizzate da integrare con API o servizi esterni. Consente di recuperare dati da origini esterne, inviare dati agli endpoint Rest esterni o eseguire azioni personalizzate basate su eventi esterni.

Le funzioni personalizzate sono essenzialmente librerie client aggiunte al file JavaScript. Una volta creata, la funzione personalizzata diventa disponibile nell’editor di regole per la selezione da parte dell’utente in un modulo adattivo. Le funzioni personalizzate sono identificate dalle annotazioni di JavaScript nell’editor di regole.

### Annotazioni di JavaScript supportate per la funzione personalizzata {#js-annotations}

**Le annotazioni di JavaScript forniscono metadati per il codice JavaScript**. Include commenti che iniziano con simboli specifici, ad esempio `/**` e `@`. Le annotazioni forniscono informazioni importanti su funzioni, variabili e altri elementi nel codice. Il modulo adattivo supporta le seguenti annotazioni di JavaScript per le funzioni personalizzate:

#### Nome

**Name** viene utilizzato per identificare la funzione personalizzata nell&#39;editor di regole di un modulo adattivo. Per denominare una funzione personalizzata vengono utilizzate le sintassi seguenti:

* `@name [functionName] <Function Name>`
* `@function [functionName] <Function Name>`
* `@func [functionName] <Function Name>`

>[!NOTE]
>`[functionName]` è il nome della funzione. Gli spazi non sono consentiti.
>`<Function Name>` è il nome visualizzato della funzione nell’editor di regole di Adaptive Forms.
>Se il nome della funzione è identico al nome della funzione stessa, è possibile omettere `[functionName]` dalla sintassi.

#### Parametro

Il **parametro** è un elenco di argomenti utilizzati dalle funzioni personalizzate. Una funzione può supportare più parametri. Le seguenti sintassi vengono utilizzate per definire un parametro in una funzione personalizzata:

* `@param {type} name <Parameter Description>`
* `@argument` `{type} name <Parameter Description>`
* `@arg` `{type}` `name <Parameter Description>`

  `{type}` rappresenta il tipo di parametro. I tipi di parametri consentiti sono:

   * string (stringa): rappresenta un singolo valore di stringa.
   * number: rappresenta un singolo valore numerico.
   * booleano: rappresenta un singolo valore booleano (true o false).
   * stringa[]: rappresenta una matrice di valori stringa.
   * number[]: rappresenta una matrice di valori numerici.
   * booleano[]: rappresenta una matrice di valori booleani.
   * data: rappresenta un singolo valore di data.
   * data[]: rappresenta una matrice di valori di data.
   * array: rappresenta una matrice generica contenente valori di vari tipi.
   * object: rappresenta un oggetto modulo passato a una funzione personalizzata anziché passare direttamente il relativo valore.
   * ambito: rappresenta l&#39;oggetto globals, che contiene variabili di sola lettura quali istanze di moduli, istanze di campi di destinazione e metodi per l&#39;esecuzione di modifiche di moduli nelle funzioni personalizzate. Viene dichiarato come ultimo parametro nelle annotazioni di JavaScript e non è visibile all’editor di regole di un modulo adattivo. Il parametro scope accede all&#39;oggetto del modulo o del componente per attivare la regola o l&#39;evento necessario per l&#39;elaborazione del modulo. Per ulteriori informazioni sull&#39;oggetto Globals e su come utilizzarlo, [fare clic qui](/help/forms/using/create-and-use-custom-functions-core-components.md#field-and-global-scope-objects-in-custom-functions-support-field-and-global-objects)

Il tipo di parametro è **senza distinzione tra maiuscole e minuscole** e non sono consentiti spazi nel nome del parametro.

`<Parameter Description>` contiene dettagli sullo scopo del parametro. Può avere più parole.

<!--

**Optional Parameters**
By default, all parameters are mandatory. You can define a parameter as optional by either adding `=` after the parameter type or enclosing the parameter name in `[]`. Parameters defined as optional in JavaScript annotations are displayed as optional in the rule editor.
To define a variable as an optional parameter, you can use the any of the following syntaxes:
  
* `@param {type=} Input1`

In the above line of code, `Input1` is an optional parameter without any default value. To declare optional parameter with default value:

`@param {string=<value>} input1`
        
`input1` as an optional parameter with the default value set to `value`. 

* `@param {type} [Input1]`

In the above line of code, `Input1` is an optional parameter without any default value. To declare optional parameter with default value:

`@param {array} [input1=<value>]`

    `input1` is an optional parameter of array type with the default value set to `value`. 
    Ensure that the parameter type is enclosed in curly brackets {} and the parameter name is enclosed in square brackets []. 

Consider the following code snippet, where input2 is defined as an optional parameter:

```javascript

        /**
         * optional parameter function
         * @name OptionalParameterFunction
         * @param {string} input1 
         * @param {string=} input2 
         * @return {string}
        */
        function OptionalParameterFunction(input1, input2) {
        let result = "Result: ";
        result += input1;
        if (input2 !== null) {
            result += " " + input2;
        }
        return result;
        }
```

The following illustration displays using the `OptionalParameterFunction` csutom function in the rule editor:

![Optional or required parameters ](/help/forms/using/assets/optional-default-params.png)

You can save the rule without specifying a value for required parameters, but the rule is not executed and displays a warning message as:

![incomplete rule warning](/help/forms/using/assets/incomplete-rule.png)

When user leaves the optional parameter empty, then the "Undefined" value is passed to the custom function for the optional parameter.

To learn more about how to define optional parameters in JSDocs, [click here](https://jsdoc.app/tags-param).

-->

#### Tipo restituito

Il tipo restituito specifica il tipo di valore restituito dalla funzione personalizzata dopo l&#39;esecuzione. Le seguenti sintassi vengono utilizzate per definire un tipo restituito in una funzione personalizzata:

* `@return {type}`
* `@returns {type}`
  `{type}` rappresenta il tipo restituito della funzione. I tipi restituiti consentiti sono:
* string (stringa): rappresenta un singolo valore di stringa.
* number: rappresenta un singolo valore numerico.
* booleano: rappresenta un singolo valore booleano (true o false).
* stringa[]: rappresenta una matrice di valori stringa.
* number[]: rappresenta una matrice di valori numerici.
* booleano[]: rappresenta una matrice di valori booleani.
* data: rappresenta un singolo valore di data.
* data[]: rappresenta una matrice di valori di data.
* array: rappresenta una matrice generica contenente valori di vari tipi.
* object: rappresenta direttamente l&#39;oggetto modulo anziché il relativo valore.

Il tipo restituito non fa distinzione tra maiuscole e minuscole.

#### Privata

La funzione personalizzata, dichiarata come privata, non viene visualizzata nell’elenco delle funzioni personalizzate nell’editor delle regole di un modulo adattivo. Per impostazione predefinita, le funzioni personalizzate sono pubbliche. La sintassi per dichiarare la funzione personalizzata come privata è `@private`.

<!--
#### Member

  Syntax: `@memberof namespace`
  Attaches a namespace to the function.
-->

<!--

#### This

   Syntax: `@this currentComponent`

   Use @this to refer to the Adaptive Form component on which the rule is written. 
  
   The following example is based on the field value. In the following example, the rule hides a field in the form. The `this` portion of `this.value` refers to underlying Adaptive Form component, on which the rule is written.

   ```
      /**
      * @function myTestFunction
      * @this currentComponent
      * @param {scope} scope in which code inside function will be executed.
      */
      myTestFunction = function (scope) {
         if(this.value == "O"){
               scope.age.visible = true;
         } else {
            scope.age.visible = false;
         }
      }

   ```

    >[!NOTE]
    >
    >Comments before custom function are used for summary. Summary can extend to multiple lines until a tag is encountered. Limit the size to a single for a concise description in the rule builder.

-->

<!--

## Function declaration supported types {#function-declaration-supported-types}

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
-->

## Linee guida per la creazione di funzioni personalizzate {#considerations}

Per elencare le funzioni personalizzate nell’editor di regole, puoi utilizzare uno dei seguenti formati:

### Istruzione function con o senza commenti jsdoc

Puoi creare una funzione personalizzata con o senza commenti jsdoc.

```javascript
    function functionName(parameters) 
        {
            // code to be executed
        }
```

Se l’utente non aggiunge annotazioni JavaScript alla funzione personalizzata, questa viene elencata nell’editor di regole in base al nome della funzione. Tuttavia, si consiglia di includere annotazioni JavaScript per migliorare la leggibilità delle funzioni personalizzate.


### Funzione freccia con annotazioni o commenti JavaScript obbligatori

È possibile creare una funzione personalizzata con una sintassi della funzione freccia:

```javascript
    /**
    * test function
    * @name testFunction 
    * @param {string} a parameter description
    * @param {string=} b parameter description
    * @return {string}
    */
    testFunction = (a, b) => {
    return a + b;
    };
    /** */
    testFunction1=(a) => (return a)
    /** */
    testFunction2 = a => a + 100;
    
```

Se l’utente non aggiunge annotazioni JavaScript alla funzione personalizzata, la funzione personalizzata non viene elencata nell’editor di regole di un modulo adattivo.

### Espressione di funzione con annotazioni o commenti JavaScript obbligatori

Per elencare le funzioni personalizzate nell’editor di regole di un modulo adattivo, crea funzioni personalizzate nel formato seguente:

```javascript
    /**
    * test function
    * @name testFunction 
    * @param {string} input1 parameter description
    * @param {string=} input2 parameter description
    * @return {string}
    */
    testFunction = function(input1,input2)
        {
            // code to be executed
        }
```

Se l’utente non aggiunge annotazioni JavaScript alla funzione personalizzata, la funzione personalizzata non viene elencata nell’editor di regole di un modulo adattivo.

### Prerequisiti per creare una funzione personalizzata

Prima di iniziare ad aggiungere una funzione personalizzata al Forms adattivo, accertati di aver installato sul computer il seguente software:

* **Editor di testo normale (IDE)**: mentre qualsiasi editor di testo normale può funzionare, un ambiente di sviluppo integrato (IDE) come Microsoft Visual Studio Code offre funzionalità avanzate per semplificare la modifica.

* **Git:** Questo sistema di controllo della versione è necessario per la gestione delle modifiche al codice. Se non lo hai installato, scaricalo da https://git-scm.com.


## Creare una funzione personalizzata {#create-custom-function}

I passaggi per creare funzioni personalizzate sono i seguenti:
1. [Crea una libreria lato client utilizzando l&#39;archetipo di progetto AEM e aggiungi una funzione personalizzata](#create-client-library-archetype)
OPPURE
   [Creare funzioni personalizzate tramite CRXDE](#create-add-custom-function)
1. [Aggiungere una libreria client a un modulo adattivo](#add-client-library)
1. [Utilizzare una funzione personalizzata in un modulo adattivo](#use-custom-functions)


### Creare una libreria client utilizzando l’archetipo di progetto AEM{#create-client-library-archetype}

È possibile aggiungere funzioni personalizzate aggiungendo una libreria client al progetto creato [utilizzando l&#39;archetipo di progetto AEM](https://experienceleague.adobe.com/it/docs/experience-manager-core-components/using/developing/archetype/using#getting-started).
Se hai un progetto esistente <!--and have already the project structure as shown in the image below,--> puoi aggiungere direttamente [funzioni personalizzate](#create-add-custom-function) al progetto locale.

<!--![custom fuction folder structure](assets/custom-library-folder-structure.png)-->

Dopo aver creato un progetto di Archetipo o aver utilizzato un progetto esistente, crea una libreria client. Per creare una libreria client, effettua le seguenti operazioni:

**Aggiungi una cartella della libreria client**

Per aggiungere una nuova cartella della libreria client alla [directory del progetto AEM], eseguire la procedura seguente:

1. Apri la [directory del progetto AEM] in un editor.

   ![struttura cartella funzioni personalizzata](assets/custom-library-folder-structure.png)

1. Individuare `ui.apps`.
1. Aggiungi nuova cartella. Aggiungere ad esempio una cartella denominata `experience-league`.
1. Passare alla cartella `/experience-league/` e aggiungere `ClientLibraryFolder`. Creare ad esempio una cartella della libreria client denominata `customclientlibs`.

   Posizione: `[AEM project directory]/ui.apps/src/main/content/jcr_root/apps/`

**Aggiungi file e cartelle alla cartella Libreria client**

Aggiungi quanto segue alla cartella della libreria client aggiunta:

* `.content.xml` file
* `js.txt` file
* Cartella `js`

`Location is: [AEMaaCS project directory]/ui.apps/src/main/content/jcr_root/apps/experience-league/customclientlibs/`

1. In `.content.xml` aggiungi le seguenti righe di codice:

   ```javascript
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
   jcr:primaryType="cq:ClientLibraryFolder"
   categories="[customfunctionscategory]"/>
   ```

   >[!NOTE]
   >
   > È possibile scegliere qualsiasi nome per la proprietà `client library folder` e `categories`.

1. In `js.txt` aggiungi le seguenti righe di codice:

   ```javascript
         #base=js
       function.js
   ```

1. Nella cartella `js`, aggiungi il file javascript come `function.js` che include le funzioni personalizzate:

   ```javascript
   /**
       * Calculates Age
       * @name calculateAge
       * @param {object} field
       * @return {string} 
   */
   
   function calculateAge(field) {
   var dob = new Date(field);
   var now = new Date();
   
   var age = now.getFullYear() - dob.getFullYear();
   var monthDiff = now.getMonth() - dob.getMonth();
   
   if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
   age--;
   }
   
   return age;
   }
   ```

1. Salva i file.

![struttura cartella funzioni personalizzata](assets/custom-function-added-files.png)

**Includi la nuova cartella nel file filter.xml**:

1. Passa al file `/ui.apps/src/main/content/META-INF/vault/filter.xml` nella directory del progetto [AEMaaCS].

1. Apri il file e aggiungi la seguente riga alla fine:

   `<filter root="/apps/experience-league" />`
1. Salva il file.

   ![filtro funzione personalizzato xml](assets/custom-function-filterxml.png)

1. Crea la cartella della libreria client appena creata nell&#39;ambiente AEM seguendo i passaggi indicati nella [sezione Come generare](https://github.com/adobe/aem-project-archetype/tree/develop/src/main/archetype#how-to-build).

## Creare e distribuire funzioni personalizzate tramite CRXDE{#create-add-custom-function}

Se utilizzi il componente aggiuntivo AEM Forms e Forms più recente, puoi creare una funzione personalizzata tramite CRXDE per utilizzare gli ultimi aggiornamenti delle funzioni personalizzate. A tale scopo, effettuare le seguenti operazioni:

<!--![custom fuction folder structure](assets/custom-library-folder-structure.png)-->


1. Accedi a `http://server:port/crx/de/index.jsp#`.
1. Creare una cartella nella cartella `/apps`. Creare ad esempio una cartella denominata `experience-league`.
1. Salva le modifiche.
1. Passare alla cartella creata e creare un nodo di tipo `cq:ClientLibraryFolder` come `clientlibs`.
1. Passare alla cartella `clientlibs` appena creata e aggiungere le proprietà `allowProxy` e `categories`:

   ![Proprietà nodo libreria personalizzato](/help/forms/using/assets/customlibrary-catproperties.png)

   >[!NOTE]
   >
   > È possibile specificare qualsiasi nome al posto di `customfunctionsdemo`.

1. Salva le modifiche.

1. Creare una cartella denominata `js` nella cartella `clientlibs`.
1. Creare un file JavaScript denominato `functions.js` nella cartella `js`.
1. Creare un file denominato `js.txt` nella cartella `clientlibs`.
1. Salva le modifiche.
La struttura di cartelle creata è simile alla seguente:

   ![Struttura cartella della libreria client creata](/help/forms/using/assets/clientlibrary_folderstructure.png)
1. Fare doppio clic sul file `functions.js` per aprire l&#39;editor. Il file contiene il codice per la funzione personalizzata.
Aggiungiamo il seguente codice al file JavaScript per calcolare l’età in base alla data di nascita (AAAA-MM-GG).

   ```javascript
       /**
            * Calculates Age
            * @name calculateAge 
            * @return {string} 
       */
   
       function calculateAge(dateOfBirthString) {
       var dob = new Date(dateOfBirthString);
       var now = new Date();
   
       var age = now.getFullYear() - dob.getFullYear();
       var monthDiff = now.getMonth() - dob.getMonth();
   
       if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
       age--;
       }
   
       return age;
       }
   ```

1. Salva `function.js`.
1. Passare a `js.txt` e aggiungere il codice seguente:

   ```javascript
       #base=js
       functions.js
   ```

1. Salva il file `js.txt`.

È possibile fare riferimento alla seguente cartella [funzione personalizzata](/help/forms/using/assets/customfunction.zip). Scarica e installa questa cartella nella tua istanza AEM.

Ora è possibile utilizzare la funzione personalizzata nel modulo adattivo aggiungendo la libreria client.

## Aggiungere una libreria client in un modulo adattivo{#add-client-library}

Dopo aver implementato la libreria client nell’ambiente AEM Forms, utilizzane le funzionalità nel modulo adattivo. Per aggiungere la libreria client al modulo adattivo

1. Apri il modulo in modalità di modifica. Per aprire un modulo in modalità di modifica, selezionare un modulo e selezionare **[!UICONTROL Modifica]**.
1. Apri il browser Contenuto e seleziona il componente **[!UICONTROL Contenitore guida]** del modulo adattivo.
1. Fai clic sull’icona delle proprietà del Contenitore guida. Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).
1. Apri la scheda **[!UICONTROL Base]** e seleziona il nome della **[!UICONTROL categoria di librerie client]** dall&#39;elenco a discesa (in questo caso, seleziona `customfunctionscategory`).

   ![Aggiunta della libreria client della funzione personalizzata](/help/forms/using//assets/custom-function-category-name-core-component.png)

1. Fai clic su **[!UICONTROL Fine]**.

Ora puoi creare una regola per utilizzare funzioni personalizzate nell’editor di regole:

![Aggiunta della libreria client della funzione personalizzata](/help/forms/using//assets/calculateage-customfunction.png)

Ora vediamo come configurare e utilizzare una funzione personalizzata utilizzando il servizio Invoke dell&#39;editor di regole [in AEM Forms 6.5](/help/forms/using/rule-editor-core-components.md#invoke-form-data-model-service-invoke)

## Utilizzo di una funzione personalizzata in un modulo adattivo {#use-custom-functions}

In un modulo adattivo, puoi utilizzare [funzioni personalizzate all&#39;interno dell&#39;editor di regole](/help/forms/using/rule-editor-core-components.md).
Aggiungiamo il codice seguente al file JavaScript (`Function.js` file) per calcolare l&#39;età in base alla data di nascita (AAAA-MM-GG). Creare una funzione personalizzata come `calculateAge()` che utilizza come input la data di nascita e restituisce l&#39;età:

```javascript
    /**
        * Calculates Age
        * @name calculateAge
        * @param {object} field
        * @return {string} 
    */

    function calculateAge(field) {
    var dob = new Date(field);
    var now = new Date();

    var age = now.getFullYear() - dob.getFullYear();
    var monthDiff = now.getMonth() - dob.getMonth();

    if (monthDiff < 0 || (monthDiff === 0 && now.getDate() < dob.getDate())) {
    age--;
    }

    return age;
    }
```

Nell&#39;esempio precedente, quando l&#39;utente immette la data di nascita nel formato (AAAA-MM-GG), la funzione personalizzata `calculateAge` viene richiamata e restituisce l&#39;età.

![Funzione personalizzata Calcola età nell&#39;editor di regole](/help/forms/using/assets/custom-function-calculate-age.png)

Visualizziamo in anteprima il modulo per osservare come le funzioni personalizzate vengono implementate tramite l’editor di regole:

![Funzione personalizzata Calcola età nell&#39;editor di regole Anteprima modulo](/help/forms/using/assets/custom-function-age-calculate-form.png)

>[!NOTE]
>
> Puoi fare riferimento alla seguente cartella [funzioni personalizzate](/help/forms/using/assets/customfunctions.zip). Scarica e installa questa cartella nella tua istanza AEM utilizzando [Gestione pacchetti](https://experienceleague.adobe.com/it/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager).

### Supporto delle funzioni asincrone nelle funzioni personalizzate {#support-of-async-functions}

Le funzioni personalizzate asincrone non vengono visualizzate nell’elenco dell’editor di regole. Tuttavia, è possibile richiamare funzioni asincrone all’interno di funzioni personalizzate create utilizzando espressioni di funzioni sincrone.

![Sincronizza e sincronizza funzione personalizzata](/help/forms/using/assets/workflow-for-sync-async-custom-fumction.png)

>[!NOTE]
>
> Il vantaggio di chiamare funzioni asincrone nelle funzioni personalizzate è che le funzioni asincrone consentono l’esecuzione simultanea di più attività, con il risultato di ogni funzione utilizzata all’interno delle funzioni personalizzate.

Osserva il codice seguente per scoprire come richiamare funzioni asincrone utilizzando funzioni personalizzate:

```javascript
    
    async function asyncFunction() {
    const response = await fetch('https://petstore.swagger.io/v2/store/inventory');
    const data = await response.json();
    return data;
    }

    /**
    * callAsyncFunction
    * @name callAsyncFunction callAsyncFunction
    */
    function callAsyncFunction() {
    asyncFunction()
        .then(responseData => {
        console.log('Response data:', responseData);
        })
        .catch(error => {
         console.error('Error:', error);
    });
}
```

Nell&#39;esempio precedente, la funzione asyncFunction è un `asynchronous function`. Esegue un&#39;operazione asincrona effettuando una richiesta `GET` a `https://petstore.swagger.io/v2/store/inventory`. Attende la risposta utilizzando `await`, analizza il corpo della risposta come JSON utilizzando `response.json()`, quindi restituisce i dati. La funzione `callAsyncFunction` è una funzione personalizzata sincrona che richiama la funzione `asyncFunction` e visualizza i dati di risposta nella console. Sebbene la funzione `callAsyncFunction` sia sincrona, chiama la funzione asyncFunction asincrona e gestisce il risultato con `then` e `catch` istruzioni.

Per vedere come funziona, aggiungiamo un pulsante e creiamo una regola per il pulsante che richiama la funzione asincrona al clic di un pulsante.

![creazione regola per funzione asincrona](/help/forms/using/assets/rule-for-async-funct.png)

Fare riferimento all&#39;illustrazione della finestra della console seguente per dimostrare che quando l&#39;utente fa clic sul pulsante `Fetch`, viene richiamata la funzione personalizzata `callAsyncFunction`, che a sua volta chiama una funzione asincrona `asyncFunction`. Inspect mostra la finestra della console per visualizzare la risposta al clic del pulsante:

![Finestra della console](/help/forms/using/assets/async-custom-funct-console.png)

Approfondiamo le funzioni personalizzate.

## Varie funzioni per funzioni personalizzate

È possibile utilizzare funzioni personalizzate per aggiungere caratteristiche personalizzate ai moduli. Queste funzioni supportano varie funzionalità, ad esempio l’utilizzo di campi specifici, l’utilizzo di campi globali o la memorizzazione in cache. Questa flessibilità consente di personalizzare i moduli in base ai requisiti aziendali.

### Oggetti di ambito Field e Global nelle funzioni personalizzate {#support-field-and-global-objects}

Gli oggetti Field fanno riferimento ai singoli componenti o elementi di un modulo, ad esempio campi di testo e caselle di controllo. L&#39;oggetto Globals contiene variabili di sola lettura quali l&#39;istanza del modulo, l&#39;istanza del campo di destinazione e i metodi per apportare modifiche al modulo nelle funzioni personalizzate.

>[!NOTE]
>
> `param {scope} globals` deve essere l&#39;ultimo parametro e non viene visualizzato nell&#39;editor di regole di un modulo adattivo.

<!-- Let us look at the following code snippet:

```JavaScript
   
    /**
    * updateDateTime
    * @name updateDateTime
    * @param {object} field
    * @param {scope} globals
    */
    function updateDateTime(field, globals) {
    // Accessing the Date object from the global scope
    var currentDate = new Date();
    // Formatting the date and time
    var formattedDateTime = currentDate.toLocaleString();
    // Updating the field value with the formatted date and time using setProperty.
    globals.functions.setProperty(field, {value: formattedDateTime});
    }
```

In the above code snippet, a custom function named `updateDateTime` takes parameters such as a field object and a global object. The field represents the textbox object where the formatted date and time value is displayed within the form. -->

Scopri in che modo le funzioni personalizzate utilizzano gli oggetti field e global con l&#39;aiuto di un modulo `Contact Us` che utilizza casi d&#39;uso diversi.

![Modulo per contattarci](/help/forms/using/assets/contact-us-form.png)

#### **Caso d&#39;uso**: mostra un pannello utilizzando la regola `SetProperty`

Aggiungere il codice seguente nella funzione personalizzata come descritto nella sezione [create-custom-function](#create-custom-function) per impostare il campo modulo come `Required`.

```javascript
    
    /**
    * enablePanel
    * @name enablePanel
    * @param {object} field1
    * @param {object} field2
    * @param {scope} globals 
    */

    function enablePanel(field1,field2, globals)
    {
       if(globals.functions.validate(field1).length === 0)
       {
       globals.functions.setProperty(field2, {visible: true});
       }
    }
```

>[!NOTE]
>
> * È possibile configurare le proprietà del campo utilizzando le proprietà disponibili in `[form-path]/jcr:content/guideContainer.model.json`.
> * Le modifiche apportate al modulo utilizzando il metodo `setProperty` dell&#39;oggetto Globals sono di natura asincrona e non vengono applicate durante l&#39;esecuzione della funzione personalizzata.

In questo esempio, la convalida del pannello `personaldetails` viene eseguita facendo clic sul pulsante. Se non vengono rilevati errori nel pannello, un altro pannello, il pannello `feedback`, diventa visibile al clic del pulsante.

Creiamo una regola per il pulsante `Next`, che convalida il pannello `personaldetails` e rende visibile il pannello `feedback` quando l&#39;utente fa clic sul pulsante `Next`.

![Imposta proprietà](/help/forms/using/assets/custom-function-set-property.png)

Fare riferimento all&#39;illustrazione seguente per dimostrare dove viene convalidato il pannello `personaldetails` facendo clic sul pulsante `Next`. Se tutti i campi all&#39;interno di `personaldetails` sono convalidati, il pannello `feedback` diventa visibile.

![Imposta anteprima modulo proprietà](/help/forms/using/assets/set-property-form-preview.png)

Se nei campi del pannello `personaldetails` sono presenti errori, questi vengono visualizzati a livello di campo facendo clic sul pulsante `Next` e il pannello `feedback` rimane invisibile.

![Imposta anteprima modulo proprietà](/help/forms/using/assets/set-property-panel.png)

#### **Caso d&#39;uso**: convalidare il campo.

Aggiungi il seguente codice nella funzione personalizzata come descritto nella sezione [create-custom-function](#create-custom-function) per convalidare il campo.

```javascript
    /**
    * validateField
    * @name validateField
    * @param {object} field
    * @param {scope} globals
    */
    function validateField(field,globals)
    {
    
        globals.functions.validate(field);
    
    }   
```

>[!NOTE]
>
> Se nella funzione `validate()` non viene passato alcun argomento, il modulo viene convalidato.

In questo esempio, al campo `contact` viene applicato un pattern di convalida personalizzato. Gli utenti devono immettere un numero di telefono che inizia con `10` seguito da `8` cifre. Se l&#39;utente immette un numero di telefono che non inizia con `10` o che contiene più o meno di `8` cifre, viene visualizzato un messaggio di errore di convalida al clic del pulsante:

![Modello di convalida indirizzo e-mail](/help/forms/using/assets/custom-function-validation-pattern.png)

Il passaggio successivo consiste nel creare una regola per il pulsante `Next` che convalida il campo `contact` al clic del pulsante.

![Modello di convalida](/help/forms/using/assets/custom-function-validate.png)

Fare riferimento all&#39;illustrazione seguente per dimostrare che se l&#39;utente immette un numero di telefono che non inizia con `10`, viene visualizzato un messaggio di errore a livello di campo:

![Modello di convalida indirizzo e-mail](/help/forms/using/assets/custom-function-validate-error-message.png)

Se l&#39;utente immette un numero di telefono valido e tutti i campi nel pannello `personaldetails` sono convalidati, il pannello `feedback` viene visualizzato sullo schermo:

![Modello di convalida indirizzo e-mail](/help/forms/using/assets/validate-form-preview-form.png)

#### **Caso d&#39;uso**: reimpostare un pannello

Aggiungi il seguente codice nella funzione personalizzata, come descritto nella sezione [create-custom-function](#create-custom-function), per ripristinare il pannello.

```javascript
    /**
    * resetField
    * @name  resetField
    * @param {string} input1
    * @param {object} field
    * @param {scope} globals 
    */
    function  resetField(field,globals)
    {
    
        globals.functions.reset(field);
    
    }
```

>[!NOTE]
>
> Se nella funzione `reset()` non viene passato alcun argomento, il modulo viene convalidato.

In questo esempio, il pannello `personaldetails` viene ripristinato facendo clic sul pulsante `Clear`. Il passaggio successivo consiste nel creare una regola per il pulsante `Clear` che ripristini il pannello al clic del pulsante.

![Cancella pulsante](/help/forms/using/assets/custom-function-reset-field.png)

Vedere l&#39;illustrazione seguente per mostrare che se l&#39;utente fa clic sul pulsante `clear`, il pannello `personaldetails` viene ripristinato:

![Reimposta modulo](assets/custom-function-reset-form.png)

#### **Caso d&#39;uso**: per visualizzare un messaggio personalizzato a livello di campo e contrassegnare il campo come non valido

È possibile utilizzare la funzione `markFieldAsInvalid()` per definire un campo come non valido e impostare un messaggio di errore personalizzato a livello di campo. Il valore `fieldIdentifier` può essere `fieldId`, `field qualifiedName` o `field dataRef`. Il valore dell&#39;oggetto denominato `option` può essere `{useId: true}`, `{useQualifiedName: true}` o `{useDataRef: true}`.
Le sintassi utilizzate per contrassegnare il campo come non valido e impostare un messaggio personalizzato sono:

* `globals.functions.markFieldAsInvalid(field.$id,"[custom message]",{useId: true});`
* `globals.functions.markFieldAsInvalid(field.$qualifiedName, "[custom message]", {useQualifiedName: true});`
* `globals.functions.markFieldAsInvalid(field.$dataRef, "[custom message]", {useDataRef: true});`

Aggiungi il seguente codice nella funzione personalizzata, come descritto nella sezione [create-custom-function](#create-custom-function), per abilitare il messaggio personalizzato a livello di campo.

```javascript
    /**
    * customMessage
    * @name customMessage
    * @param {object} field
    * @param {scope} globals 
    */
    function customMessage(field, globals) {
    const minLength = 15;
    const comments = field.$value.trim();
    if (comments.length < minLength) {
        globals.functions.markFieldAsInvalid(field.$id, "Comments must be at least 15 characters long.", { useId: true });
    }
}
```

In questo esempio, se l&#39;utente immette meno di 15 caratteri nella casella di testo dei commenti, viene visualizzato un messaggio personalizzato a livello di campo.

Il passaggio successivo consiste nel creare una regola per il campo `comments`:

![Contrassegna il campo come non valido](/help/forms/using/assets/custom-function-invalid-field.png)

Vedere la dimostrazione seguente per visualizzare che l&#39;immissione di un feedback negativo nel campo `comments` attiva la visualizzazione di un messaggio personalizzato a livello di campo:

![Contrassegna il campo come modulo di anteprima non valido](/help/forms/using/assets/custom-function-invalidfield-form.png)

Se l’utente immette più di 15 caratteri nella casella di testo Commenti, il campo viene convalidato e il modulo viene inviato:

![Contrassegna il campo come modulo di anteprima valido](/help/forms/using/assets/custom-function-validfield-form.png)


#### **Caso d&#39;uso**: invio dei dati modificati al server

La seguente riga di codice:
`globals.functions.submitForm(globals.functions.exportData(), false);` viene utilizzato per inviare i dati del modulo dopo la manipolazione.
* Il primo argomento è costituito dai dati da inviare.
* Il secondo argomento indica se il modulo deve essere convalidato prima dell&#39;invio. È `optional` ed è impostato come `true` per impostazione predefinita.
* Il terzo argomento è `contentType` dell&#39;inoltro, che è anche facoltativo con il valore predefinito `multipart/form-data`. Gli altri valori possono essere `application/json` e `application/x-www-form-urlencoded`.

Aggiungi il seguente codice nella funzione personalizzata, come descritto nella sezione [create-custom-function](#create-custom-function), per inviare i dati manipolati sul server:

```javascript
    /**
    * submitData
    * @name submitData
    * @param {object} field
    * @param {scope} globals 
    */
    function submitData(globals)
    {
    
    var data = globals.functions.exportData();
    if(!data.comments) {
    data.comments = 'NA';
    }
    console.log('After update:{}',data);
    globals.functions.submitForm(data, false);
    }
```

In questo esempio, se l&#39;utente lascia vuota la casella di testo `comments`, `NA` viene inviato al server al momento dell&#39;invio del modulo.

Creare una regola per il pulsante `Submit` che invia i dati:

![Invia dati](/help/forms/using/assets/custom-function-submit-data.png)

Fare riferimento all&#39;illustrazione di `console window` seguente per dimostrare che se l&#39;utente lascia vuota la casella di testo `comments`, il valore `NA` viene inviato nel server:

![Invia dati nella finestra della console](/help/forms/using/assets/custom-function-submit-data-form.png)

È inoltre possibile esaminare la finestra della console per visualizzare i dati inviati al server:

![Dati Inspect nella finestra della console](/help/forms/using/assets/custom-function-submit-data-console-data.png)

<!--

#### **Use Case**: Display form submission and failure messages for custom submit action 

Add the following line of code as explained in the [create-custom-function ](#create-custom-function) section, to customize the submission or failure message for form submissions and display the form submission messages in a modal box:

```javascript
/**
 * Handles the success response after a form submission.
 *
 * @param {scope} globals - This object contains a read-only form instance, target field instance, triggered event, and methods for performing form modifications within custom functions.
 * @returns {void}
 */
function customSubmitSuccessHandler(globals) {
    var event = globals.event;
    var submitSuccessResponse = event.payload.body;
    var form = globals.form;

    if (submitSuccessResponse) {
        if (submitSuccessResponse.redirectUrl) {
            window.location.href = encodeURI(submitSuccessResponse.redirectUrl);
        } else if (submitSuccessResponse.thankYouMessage) {
            showModal("success", submitSuccessResponse.thankYouMessage);
        }
    }
}

/**
 * Handles the error response after a form submission.
 *
 * @param {string} customSubmitErrorMessage - The custom error message.
 * @param {scope} globals - This object contains a read-only form instance, target field instance, triggered event, and methods for performing form modifications within custom functions.
 * @returns {void}
 */
function customSubmitErrorHandler(customSubmitErrorMessage, globals) {
    showModal("error", customSubmitErrorMessage);
}
function showModal(type, message) {
    // Remove any existing modals
    var existingModal = document.getElementById("modal");
    if (existingModal) {
        existingModal.remove();
    }

    // Create the modal dialog
    var modal = document.createElement("div");
    modal.setAttribute("id", "modal");
    modal.setAttribute("class", "modal");

    // Create the modal content
    var modalContent = document.createElement("div");
    modalContent.setAttribute("class", "modal-content");

    // Create the modal header
    var modalHeader = document.createElement("div");
    modalHeader.setAttribute("class", "modal-header");
    modalHeader.innerHTML = "<h2>" + (type === "success" ? "Thank You" : "Error") + "</h2>";

    // Create the modal body
    var modalBody = document.createElement("div");
    modalBody.setAttribute("class", "modal-body");
    modalBody.innerHTML = "<p class='" + type + "-message'>" + message + "</p>";

    // Create the modal footer
    var modalFooter = document.createElement("div");
    modalFooter.setAttribute("class", "modal-footer");

    // Create the close button
    var closeButton = document.createElement("button");
    closeButton.setAttribute("class", "close-button");
    closeButton.innerHTML = "Close";
    closeButton.onclick = function() {
        modal.remove();
    };

    // Append the elements to the modal content
    modalFooter.appendChild(closeButton);
    modalContent.appendChild(modalHeader);
    modalContent.appendChild(modalBody);
    modalContent.appendChild(modalFooter);

    // Append the modal content to the modal
    modal.appendChild(modalContent);

    // Append the modal to the document body
    document.body.appendChild(modal);
}
```

In this example, when the user uses the `customSubmitSuccessHandler` and `customSubmitErrorHandler` custom functions, the success and failure messages are displayed in a modal. The JavaScript function `showModal(type, message)` is used to dynamically create and display a modal dialog box on a screen.

Now, create a rule for successful form submission:

![Form submission success](/help/forms/using/assets/form-submission-success.png)

Refer to the illustration below to demonstrate that when the form is submitted successfully, the success message is displayed in a modal:

![Form submission success message](/help/forms/using/assets/form-submission-success-message.png )
 
Similarly, let us create a rule for failed form submissions:

![Form submission fail](/help/forms/using/assets/form-submission-fail.png)

Refer to the illustration below to demonstrate that when the form submission fails, the error message is displayed in a modal:

![Form submission fail message](/help/forms/using/assets/form-submission-fail-message.png )

To display form submission success and failure in a default manner, the `Default submit Form Success Handler` and `Default submit Form Error Handler` functions are available out of the box.

In case, the custom submit action fails to perform as expected in existing AEM projects or forms, refer to the [troubleshooting](#troubleshooting) section.

-->

## Supporto della memorizzazione in cache per la funzione personalizzata

Forms adattivo implementa il caching per le funzioni personalizzate per migliorare il tempo di risposta durante il recupero dell’elenco delle funzioni personalizzate nell’editor di regole. Nel file `error.log` viene visualizzato il messaggio `Fetched following custom functions list from cache`.

![funzione personalizzata con supporto cache](/help/forms/using/assets/custom-function-cache-error.png)

Se le funzioni personalizzate vengono modificate, la memorizzazione in cache viene invalidata e analizzata.

## Risoluzione dei problemi {#troubleshooting}

* L&#39;utente deve verificare che il componente core [e la versione della specifica siano impostati sulla versione più recente](https://github.com/adobe/aem-core-forms-components/tree/release/650). Tuttavia, per i progetti e i moduli AEM esistenti, vi sono ulteriori passi da seguire:

   * Per il progetto AEM, l&#39;utente deve sostituire tutte le istanze di `submitForm('custom:submitSuccess', 'custom:submitError')` con `submitForm()` e distribuire il progetto.

   * Per i moduli esistenti, se i gestori di invio personalizzati non funzionano correttamente, l&#39;utente deve aprire e salvare la regola `submitForm` sul pulsante **Invia** utilizzando l&#39;editor di regole. Questa azione sostituisce la regola esistente di `submitForm('custom:submitSuccess', 'custom:submitError')` con `submitForm()` nel modulo.


* Se il file JavaScript contenente il codice per le funzioni personalizzate presenta un errore, le funzioni personalizzate non sono elencate nell’editor delle regole di un modulo adattivo. Per verificare l&#39;elenco delle funzioni personalizzate, è possibile individuare l&#39;errore nel file `error.log`. In caso di errore, l’elenco delle funzioni personalizzate appare vuoto:

  ![file di log degli errori](/help/forms/using/assets/custom-function-list-error-file.png)

  In caso di errore, la funzione personalizzata viene recuperata e visualizzata nel file `error.log`. Nel file `error.log` viene visualizzato il messaggio `Fetched following custom functions list`:

  ![file di registro errori con funzione personalizzata appropriata](/help/forms/using/assets/custom-function-list-fetched-in-error.png)

## Considerazioni

* `parameter type` e `return type` non supportano `None`.

* Le funzioni non supportate nell&#39;elenco delle funzioni personalizzate sono:
   * Funzioni del generatore
   * Funzioni Async/Await
   * Definizioni dei metodi
   * Metodi di classe
   * Parametri predefiniti
   * Parametri rimanenti
