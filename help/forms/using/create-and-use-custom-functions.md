---
title: Creare e aggiungere funzioni personalizzate in un modulo adattivo
description: AEM Forms supporta funzioni personalizzate che consentono agli utenti di creare e utilizzare le proprie funzioni all’interno dell’editor di regole.
keywords: Aggiungi una funzione personalizzata, utilizza una funzione personalizzata, crea una funzione personalizzata, utilizza la funzione personalizzata nell’editor di regole.
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms, Core Components
exl-id: a328b4a8-e8dd-42a0-b73b-94e76c7692a8
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 1%

---


# Funzioni personalizzate in Forms adattivo (componenti core)

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/create-and-use-custom-functions) |
| AEM 6.5 | Questo articolo |

## Introduzione

In AEM Forms 6.5 è stata introdotta la possibilità di definire funzioni JavaScript da utilizzare per definire regole di business complesse tramite l’editor di regole. AEM Forms fornisce una serie di funzioni personalizzate pronte all’uso, ma sarà necessario definire funzioni personalizzate e utilizzarle in più moduli.

Le funzioni personalizzate estendono le funzionalità dei moduli facilitando la manipolazione e l’elaborazione dei dati immessi per soddisfare requisiti specifici. Consentono inoltre di modificare dinamicamente il comportamento delle forme in base a criteri predefiniti.
In Adaptive Forms, puoi utilizzare funzioni personalizzate all’interno del [editor di regole di un modulo adattivo](/help/forms/using/rule-editor.md) per creare regole di convalida specifiche per i campi modulo.
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
* **Convalida dei dati**: le funzioni personalizzate ti consentono di eseguire controlli personalizzati sugli input dei moduli e fornire messaggi di errore specifici.
* **Comportamento dinamico**: le funzioni personalizzate consentono di controllare il comportamento dinamico dei moduli in base a condizioni specifiche. Ad esempio, è possibile visualizzare/nascondere campi, modificare i valori dei campi o modificare dinamicamente la logica del modulo.
* **Integrazione**: puoi utilizzare funzioni personalizzate da integrare con API o servizi esterni. Consente di recuperare dati da origini esterne, inviare dati agli endpoint Rest esterni o eseguire azioni personalizzate basate su eventi esterni.

## Note JS supportate

Assicurati che la funzione personalizzata che scrivi sia accompagnata dai `jsdoc` sopra di esso, nel caso, si richiede la configurazione personalizzata e la descrizione. Esistono diversi modi per dichiarare una funzione in `JavaScript,` I commenti e consentono di tenere traccia delle funzioni. Per ulteriori informazioni, consulta [usejsdoc.org](https://jsdoc.app/).

Supportato `jsdoc` tag:

* **Privato**
Sintassi: `@private`
Una funzione privata non è inclusa come funzione personalizzata.

* **Nome**
Sintassi: `@name funcName <Function Name>`
In alternativa `,` puoi utilizzare: `@function funcName <Function Name>` **o** `@func` `funcName <Function Name>`.
  `funcName` è il nome della funzione (non sono consentiti spazi).
  `<Function Name>` è il nome visualizzato della funzione.

* **Membro**
Sintassi: `@memberof namespace`
Associa uno spazio dei nomi alla funzione.

* **Parametro**
Sintassi: `@param {type} name <Parameter Description>`
In alternativa, puoi utilizzare: `@argument` `{type} name <Parameter Description>` **o** `@arg` `{type}` `name <Parameter Description>`.
Mostra i parametri utilizzati dalla funzione. Una funzione può avere più tag di parametri, uno per ogni parametro in ordine di occorrenza.
  `{type}` rappresenta il tipo di parametro. I tipi di parametri consentiti sono:

   1. stringa
   2. numero
   3. booleano
   4. ambito

  L’ambito viene utilizzato per fare riferimento ai campi di un modulo adattivo. Quando un modulo utilizza il caricamento lento, è possibile utilizzare `scope` per accedere ai relativi campi. È possibile accedere ai campi quando sono caricati o se sono contrassegnati come globali.

  Tutti gli altri tipi di parametri sono classificati in una delle categorie precedenti. Nessuno non è supportato. Accertati di selezionare uno dei tipi riportati sopra. I tipi non fanno distinzione tra maiuscole e minuscole. Il parametro non può contenere spazi `name`. `<Parameter Descrption>` `<parameter>  can have multiple words. </parameter>`

* **Tipo restituito**
Sintassi: `@return {type}`
In alternativa, puoi utilizzare `@returns {type}`.
Aggiunge informazioni sulla funzione, ad esempio l&#39;obiettivo.
{type} rappresenta il tipo restituito della funzione. I tipi restituiti consentiti sono:

   1. stringa
   1. numero
   1. booleano

  Tutti gli altri tipi di reso sono classificati in una delle categorie precedenti. Nessuno non è supportato. Accertati di selezionare uno dei tipi riportati sopra. I tipi restituiti non fanno distinzione tra maiuscole e minuscole.

* **Questo**
Sintassi: `@this currentComponent`

  Utilizza @this per fare riferimento al componente Modulo adattivo su cui è scritta la regola.

  L’esempio seguente è basato sul valore del campo. Nell&#39;esempio seguente, la regola nasconde un campo nel modulo. Il `this` parte di `this.value` fa riferimento al componente modulo adattivo sottostante, su cui viene scritta la regola.

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

**Espressione di funzione e istruzione**

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
1. Creare una cartella in `/apps` cartella. Ad esempio, crea una cartella denominata come `experience-league`.
1. Salva le modifiche.
1. Passa alla cartella creata e crea un nodo di tipo `cq:ClientLibraryFolder` as `clientlibs`.
1. Passa alla nuova `clientlibs` cartella e aggiungi `allowProxy` e `categories` proprietà:

   ![Proprietà del nodo della libreria personalizzata](/help/forms/using/assets/customlibrary-catproperties.png)

   >[!NOTE]
   >
   > Puoi fornire qualsiasi nome al posto di `customfunctionsdemo`.

1. Salva le modifiche.

1. Crea una cartella denominata `js` sotto `clientlibs` cartella.
1. Creare un file JavaScript denominato `functions.js` sotto `js` cartella
1. Crea un file denominato `js.txt` sotto `clientlibs` cartella.
1. Salva le modifiche.
La struttura di cartelle creata è simile alla seguente:

   ![Struttura delle cartelle della libreria client creata](/help/forms/using/assets/clientlibrary_folderstructure.png)
1. Fai doppio clic su `functions.js` per aprire l’editor. Il file contiene il codice per la funzione personalizzata.
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
1. Accedi a `js.txt` e aggiungi il seguente codice:

   ```javascript
       #base=js
       functions.js
   ```

1. Salva il `js.txt` file.

Puoi consultare quanto segue [funzione personalizzata](/help/forms/using/assets/customfunction.zip) cartella. Scarica e installa questa cartella nella tua istanza AEM.

Ora è possibile utilizzare la funzione personalizzata nel modulo adattivo aggiungendo la libreria client.

## Aggiungere una libreria client in un modulo adattivo{#use-custom-function}

Dopo aver implementato la libreria client nell’ambiente Forms CS, utilizzane le funzionalità nel modulo adattivo. Per aggiungere la libreria client al modulo adattivo

1. Apri il modulo in modalità di modifica. Per aprire un modulo in modalità di modifica, selezionare un modulo e selezionare **[!UICONTROL Modifica]**.
1. Apri il browser Contenuto e seleziona la **[!UICONTROL Contenitore guida]** componente del modulo adattivo.
1. Fai clic sull’icona delle proprietà del Contenitore guida. Viene visualizzata la finestra di dialogo Contenitore modulo adattivo (Adaptive Form Container).
1. Apri **[!UICONTROL Base]** e seleziona il nome del **[!UICONTROL categoria libreria client]** dall’elenco a discesa (in questo caso, seleziona `customfunctionscategory`).

   ![Aggiunta della libreria client della funzione personalizzata](/help/forms/using//assets/custom-function-category-name-core-component.png)

1. Clic **[!UICONTROL Fine]** .

Ora puoi creare una regola per utilizzare funzioni personalizzate nell’editor di regole:

![Aggiunta della libreria client della funzione personalizzata](/help/forms/using//assets/calculateage-customfunction.png)

Ora vediamo come configurare e utilizzare una funzione personalizzata utilizzando [Servizio Invoke dell’editor di regole in AEM Forms](/help//forms/using/rule-editor.md).
