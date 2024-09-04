---
title: Creare e aggiungere funzioni personalizzate in un modulo adattivo
description: AEM Forms supporta funzioni personalizzate che consentono agli utenti di creare e utilizzare le proprie funzioni all’interno dell’editor di regole.
feature: Adaptive Forms, Foundation Components
role: Admin, User, Developer
source-git-commit: f63dcd7edca640cee47c8f615d1675ef5052953c
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 0%

---

# Funzioni personalizzate in Adaptive Forms

## Introduzione

In AEM Forms 6.5 è stata introdotta la possibilità di definire funzioni di JavaScript che possono essere utilizzate per definire regole di business complesse utilizzando l’editor di regole. AEM Forms fornisce una serie di funzioni personalizzate pronte all’uso, ma sarà necessario definire funzioni personalizzate e utilizzarle in più moduli.

Le funzioni personalizzate estendono le funzionalità dei moduli facilitando la manipolazione e l’elaborazione dei dati immessi per soddisfare requisiti specifici. Consentono inoltre di modificare dinamicamente il comportamento delle forme in base a criteri predefiniti.
In Forms adattivo, puoi utilizzare funzioni personalizzate nell&#39;editor di regole [di un modulo adattivo](/help/forms/using/rule-editor.md) per creare regole di convalida specifiche per i campi modulo.
Comprendiamo l’utilizzo della funzione personalizzata, in cui gli utenti immettono l’indirizzo e-mail e desideri che l’indirizzo e-mail inserito segua un formato specifico (contiene il simbolo &quot;@&quot; e un nome di dominio). Crea una funzione personalizzata come &quot;ValidateEmail&quot; che accetta l’indirizzo e-mail come input e restituisce true se è valido, altrimenti restituisce false.

```javascript
function ValidateEmail(inputText)
{
    var email = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/;
    if(inputText.value.match(email))
        {
            alert("Valid email address!");
            return true;
        }
    else
    {
        alert("Invalid email address!");
        return false;
    }
}
```

Nell’esempio precedente, quando l’utente tenta di inviare il modulo, viene richiamata la funzione personalizzata &quot;ValidateEmail&quot; per verificare se l’indirizzo e-mail inserito è valido.

## Utilizzo di funzioni personalizzate {#uses-of-custom-function}

L’utilizzo di funzioni personalizzate in Adaptive Forms offre i seguenti vantaggi:

* **Manipolazione dei dati**: le funzioni personalizzate manipolano ed elaborano i dati immessi nei campi dei moduli.
* **Convalida dei dati**: le funzioni personalizzate consentono di eseguire controlli personalizzati sugli input dei moduli e di fornire messaggi di errore specifici.
* **Comportamento dinamico**: le funzioni personalizzate consentono di controllare il comportamento dinamico dei moduli in base a condizioni specifiche. Ad esempio, è possibile visualizzare/nascondere campi, modificare i valori dei campi o modificare dinamicamente la logica del modulo.
* **Integrazione**: è possibile utilizzare funzioni personalizzate da integrare con API o servizi esterni. Consente di recuperare dati da origini esterne, inviare dati agli endpoint Rest esterni o eseguire azioni personalizzate basate su eventi esterni.

## Note JS supportate

Assicurarsi che la funzione personalizzata scritta sia accompagnata dal `jsdoc` sopra di essa, nel caso sia necessaria una configurazione e una descrizione personalizzate. Esistono diversi modi per dichiarare una funzione in `JavaScript,` e i commenti consentono di tenere traccia delle funzioni. Per ulteriori informazioni, vedere [usejsdoc.org](https://jsdoc.app/).

`jsdoc` tag supportati:

* **Privato**
Sintassi: `@private`
Una funzione privata non è inclusa come funzione personalizzata.

* **Nome**
Sintassi: `@name funcName <Function Name>`
In alternativa `,` puoi utilizzare: `@function funcName <Function Name>` **or** `@func` `funcName <Function Name>`.
  `funcName` è il nome della funzione (non sono consentiti spazi).
  `<Function Name>` è il nome visualizzato della funzione.

* **Membro**
Sintassi: `@memberof namespace`
Associa uno spazio dei nomi alla funzione.

* **Parametro**
Sintassi: `@param {type} name <Parameter Description>`
In alternativa, è possibile utilizzare: `@argument` `{type} name <Parameter Description>` **or** `@arg` `{type}` `name <Parameter Description>`.
Mostra i parametri utilizzati dalla funzione. Una funzione può avere più tag di parametri, uno per ogni parametro in ordine di occorrenza.
  `{type}` rappresenta il tipo di parametro. I tipi di parametri consentiti sono:

   1. stringa
   2. numero
   3. booleano
   4. ambito

  L’ambito viene utilizzato per fare riferimento ai campi di un modulo adattivo. Quando un modulo utilizza il caricamento lento, è possibile utilizzare `scope` per accedere ai relativi campi. È possibile accedere ai campi quando sono caricati o se sono contrassegnati come globali.

  Tutti gli altri tipi di parametri sono classificati in una delle categorie precedenti. Nessuno non è supportato. Accertati di selezionare uno dei tipi riportati sopra. I tipi non fanno distinzione tra maiuscole e minuscole. Spazi non consentiti nel parametro `name`. `<Parameter Descrption>` `<parameter>  can have multiple words. </parameter>`

* **Tipo restituito**
Sintassi: `@return {type}`
In alternativa, è possibile utilizzare `@returns {type}`.
Aggiunge informazioni sulla funzione, ad esempio l&#39;obiettivo.
{type} rappresenta il tipo restituito della funzione. I tipi restituiti consentiti sono:

   1. stringa
   1. numero
   1. booleano

  Tutti gli altri tipi di reso sono classificati in una delle categorie precedenti. Nessuno non è supportato. Accertati di selezionare uno dei tipi riportati sopra. I tipi restituiti non fanno distinzione tra maiuscole e minuscole.

* **Questo**
Sintassi: `@this currentComponent`

  Utilizza @this per fare riferimento al componente Modulo adattivo su cui è scritta la regola.

  L’esempio seguente è basato sul valore del campo. Nell&#39;esempio seguente, la regola nasconde un campo nel modulo. La parte `this` di `this.value` fa riferimento al componente del modulo adattivo sottostante, sul quale viene scritta la regola.

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
  >I commenti prima della funzione personalizzata vengono utilizzati per il riepilogo. Il riepilogo può estendersi su più righe fino a quando non viene rilevato un tag. Limita le dimensioni a un singolo per una descrizione concisa nel generatore di regole.

## Tipi supportati da dichiarazione di funzione {#function-declaration-supported-types}

**Istruzione Function**

```javascript
function area(len) {
    return len*len;
}
```

Questa funzione è inclusa senza `jsdoc` commenti.

**Espressione funzione**

```javascript
var area;
//Some codes later
/** */
area = function(len) {
    return len*len;
};
```

**Espressione funzione e istruzione**

```javascript
var b={};
/** */
b.area = function(len) {
    return len*len;
}
```

**Dichiarazione di funzione come variabile**

```javascript
/** */
var x1,
    area = function(len) {
        return len*len;
    },
    x2 =5, x3 =true;
```

Limitazione: la funzione personalizzata seleziona solo la prima dichiarazione di funzione dall’elenco delle variabili, se presente insieme. È possibile utilizzare l&#39;espressione di funzione per ogni funzione dichiarata.

**Dichiarazione di funzione come oggetto**

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

## Creare una funzione personalizzata {#create-custom-function}

Per creare una funzione personalizzata, effettuare le seguenti operazioni:

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
1. Crea un file JavaScript denominato `functions.js` nella cartella `js`
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

## Aggiungere una libreria client in un modulo adattivo{#use-custom-function}

Dopo aver implementato la libreria client nell’ambiente Forms CS, utilizzane le funzionalità nel modulo adattivo. Per aggiungere la libreria client al modulo adattivo

1. Apri il modulo in modalità di modifica. Per aprire un modulo in modalità di modifica, selezionare un modulo e selezionare **[!UICONTROL Modifica]**.
1. Apri il browser Contenuto e seleziona il componente **[!UICONTROL Contenitore guida]** del modulo adattivo.
1. Fai clic sull’icona delle proprietà del Contenitore guida. Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).
1. Apri la scheda **[!UICONTROL Base]** e seleziona il nome della **[!UICONTROL categoria di librerie client]** dall&#39;elenco a discesa (in questo caso, seleziona `customfunctionscategory`).

   ![Aggiunta della libreria client della funzione personalizzata](/help/forms/using//assets/custom-function-category-name-core-component.png)

1. Fai clic su **[!UICONTROL Fine]**.

Ora puoi creare una regola per utilizzare funzioni personalizzate nell’editor di regole:

![Aggiunta della libreria client della funzione personalizzata](/help/forms/using//assets/calculateage-customfunction.png)

Ora vediamo come configurare e utilizzare una funzione personalizzata utilizzando il servizio Invoke dell&#39;editor di regole [in AEM Forms](/help//forms/using/rule-editor.md).
