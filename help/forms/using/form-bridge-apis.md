---
title: API Bridge per moduli HTML5
description: Le applicazioni esterne utilizzano l’API FormBridge per connettersi al modulo mobile XFA. L'API invia un evento FormBridgeInitialized nella finestra padre.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: developer-reference
exl-id: b598ef47-49ff-4806-8cc7-4394aa068eaa
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 0%

---

# API Bridge per moduli HTML5 {#form-bridge-apis-for-html-forms}

Puoi utilizzare le API Bridge per moduli per aprire un canale di comunicazione tra moduli HTML5 basati su XFA e le tue applicazioni. Le API di Bridge Form forniscono un&#39;API **connect** per creare la connessione.

L&#39;API **connect** accetta un gestore come argomento. Dopo aver creato una connessione tra il modulo HTML5 basato su XFA e Form Bridge, viene richiamato l’handle.

Per creare la connessione, puoi utilizzare il seguente codice di esempio.

```javascript
// Example showing how to connect to FormBridge
window.addEventListener("FormBridgeInitialized",
                                function(event) {
                                    var fb = event.detail.formBridge;
                                    fb.connect(function() {
                                           //use form bridge functions
                         })
                            })
```

>[!NOTE]
>
>Assicurarsi di creare una connessione prima di includere il file formRuntime.jsp.

## API Bridge modulo disponibile  {#available-form-bridge-api-nbsp}

**getBridgeVersion()**

Restituisce il numero di versione della libreria Script

* **Input**: nessuno
* **Output**: numero di versione della libreria di script
* **Errori**: nessuno

**isConnected()** Controlla se lo stato del modulo è stato inizializzato

* **Input**: nessuno
* **Output**: **True** se lo stato del modulo XFA è stato inizializzato

* **Errori**: nessuno

**connect(handler, context)** Effettua una connessione a FormBridge ed esegue la funzione dopo aver stabilito la connessione e aver inizializzato lo stato del modulo

* **Input**:

   * **gestore**: funzione da eseguire dopo la connessione a Form Bridge
   * **contesto**: l&#39;oggetto su cui è impostato il contesto (this) della funzione *handler*.

* **Output**: nessuno
* **Errore**: nessuno

**getDataXML(options)** Restituisce i dati del modulo corrente in formato XML

* **Input:**

   * **opzioni:** oggetto JavaScript contenente le proprietà seguenti:

      * **Errore**: funzione gestore errori
      * **success**: funzione gestore operazioni riuscite. Questa funzione ha passato un oggetto contenente XML nella proprietà *data*.
      * **contesto**: l&#39;oggetto su cui è impostato il contesto (questo) della funzione *success*
      * **validationChecker**: Funzione da chiamare per controllare gli errori di convalida ricevuti dal server. Alla funzione di convalida viene passata una matrice di stringhe di errore.
      * **formState**: lo stato JSON del modulo XFA per il quale deve essere restituito l&#39;XML dati. Se non viene specificato, verrà restituito il codice XML dei dati per il modulo di cui è stato eseguito il rendering.

* **Output:** Nessuno
* **Errore:** Nessuno

**registerConfig(configName, config)** Registra le configurazioni specifiche di utenti/portali con FormBridge. Queste configurazioni sostituiscono quelle predefinite. Le configurazioni supportate sono specificate nella sezione di configurazione.

* **Input:**

   * **configName:** Nome della configurazione da ignorare

      * **widgetConfig:** consente all&#39;utente di sostituire i widget predefiniti nel modulo con widget personalizzati. La configurazione viene sovrascritta come segue:

        *formBridge.registerConfig(&quot;widgetConfig&quot;:{/&amp;ast;configuration&amp;ast;/})*

      * **pagingConfig:** consente all&#39;utente di ignorare il comportamento predefinito del rendering solo della prima pagina. La configurazione viene sovrascritta come segue:

        *window.formBridge.registerConfig(&quot;pagingConfig&quot;:{pagingDisabled: &lt;true | false>, shrinkPageDisabled: &lt;true | false> }).*

      * **LoggingConfig:** consente all&#39;utente di ignorare il livello di registrazione, disabilitare la registrazione per una categoria, visualizzare la console dei registri o inviare messaggi al server. La configurazione può essere sovrascritta come segue:

     ```javascript
     formBridge.registerConfig{
       "LoggerConfig" : {
     {
     "on":`<true *| *false>`,
     "category":`<array of categories>`,
     "level":`<level of categories>`, "
     type":`<"console"/"server"/"both">`
     }
       }
     ```

      * **SubmitServiceProxyConfig:** Consenti agli utenti di registrare i servizi proxy di invio e logger.

        ```javascript
        window.formBridge.registerConfig("submitServiceProxyConfig",
        {
        "submitServiceProxy" : "`<submitServiceProxy>`",
        "logServiceProxy": "`<logServiceProxy>`",
        "submitUrl" : "`<submitUrl>`"
        });
        ```

   * **config:** Valore della configurazione

* **Output:** oggetto contenente il valore originale della configurazione nella proprietà *data*.

* **Errore:** Nessuno

**hideFields(fieldArray)** Nasconde i campi le cui espressioni Som vengono fornite in fieldArray. Imposta la proprietà di presenza dei campi specificati su invisibile

* **Input:**

   * **fieldArray:** Array di espressioni Som per i campi da nascondere

* **Output:** Nessuno
* **Errore:** Nessuno

**showFields(fieldArray)** Visualizza i campi le cui espressioni Som vengono fornite in fieldArray. Imposta la proprietà di presenza dei campi forniti su visibile

* **Input:**

   * **fieldArray:** Array di espressioni Som per i campi da visualizzare

* **Output:** Nessuno
* **Errore:** Nessuno

**hideSubmitButtons()** Nasconde tutti i pulsanti di invio nel modulo

* **Input**: nessuno
* **Output**: nessuno
* **Errore**: genera un&#39;eccezione se lo stato del modulo non è inizializzato

**getFormState()** Restituisce il JSON che rappresenta lo stato del modulo

* **Input:** Nessuno
* **Output:** oggetto contenente JSON che rappresenta lo stato corrente del modulo nella proprietà *data*.

* **Errore:** Nessuno

**restoreFormState(options)** Ripristina lo stato del modulo dallo stato JSON fornito nell&#39;oggetto options. Lo stato viene applicato e gli handler di esito positivo o di errore vengono chiamati al termine dell&#39;operazione

* **Input:**

   * **Opzioni:** oggetto JavaScript contenente le proprietà seguenti:

      * **Errore**: funzione gestore errori
      * **success**: funzione gestore operazioni riuscite
      * **contesto**: l&#39;oggetto su cui è impostato il contesto (questo) della funzione *success*
      * **formState**: stato JSON del modulo. Il modulo viene ripristinato allo stato JSON.

* **Output:** Nessuno
* **Errore:** Nessuno

**setFocus (som)** Imposta lo stato attivo sul campo specificato nell&#39;espressione Som

* **Input:** Espressione del campo su cui impostare lo stato attivo
* **Output:** Nessuno
* **Errore:** genera un&#39;eccezione se è presente un&#39;espressione Som non corretta

**setFieldValue (som, value)** Imposta il valore dei campi per le espressioni Som specificate

* **Input:**

   * **som:** Array contenente alcune espressioni del campo. L’espressione som per impostare il valore dei campi.
   * **valore:** Array contenente i valori corrispondenti alle espressioni Som fornite in un array **som**. Se il tipo di dati del valore non è uguale a fieldType, il valore non viene modificato.

* **Output:** Nessuno
* **Errore:** genera un&#39;eccezione se è presente un&#39;espressione Som non corretta

**getFieldValue (som)** Restituisce il valore dei campi per le espressioni Som specificate

* **Input:** Array contenente alcune espressioni dei campi il cui valore deve essere recuperato
* **Output:** Oggetto contenente il risultato come matrice nella proprietà **data**.

* **Errore:** Nessuno

### Esempio di API getFieldValue() {#example-of-nbsp-getfieldvalue-api}

```JavaScript
var a =  formBridge.getFieldValue("xfa.form.form1.Subform1.TextField");
if(a.errors) {
    var err;
     while((err = a.getNextMessage()) != null)
               alert(a.message)
} else {
   alert(a.data[0])
}
```

**getFieldProperties(som, property)** Recupera l&#39;elenco di valori per la proprietà specificata dei campi specificati nelle espressioni Som

* **Input:**

   * **som:** Array contenente espressioni Som per i campi
   * **proprietà**: nome della proprietà il cui valore è obbligatorio

* **Output:** Oggetto contenente il risultato come array nella proprietà *data*

* **Errore:** Nessuno

**setFieldProperties(som, property, values)** Imposta il valore della proprietà specificata per tutti i campi specificati nelle espressioni Som

* **Input:**

   * **som:** Array contenente alcune espressioni dei campi il cui valore deve essere impostato
   * **proprietà**: proprietà il cui valore deve essere impostato
   * **valore:** Array contenente i valori della proprietà specificata per i campi specificati nelle espressioni Som

* **Output:** Nessuno
* **Errore:** Nessuno

## Utilizzo di esempio dell’API Bridge del modulo {#sample-usage-of-form-bridge-api}

```JavaScript
// Example 1: FormBridge.restoreFormState
  function loadFormState() {
    var suc = function(obj) {
             //success
            }
    var err = function(obj) {
           while(var t = obj.getNextMessage()) {
         $("#errorDiv").append("<div>"+t.message+"</div>");
           }
           }
        var _formState = // load form state from storage
    formBridge.restoreFormState({success:suc,error:err,formState:_formState}); // not passing a context means that this will be formBridge itself. Validation errors will be checked.
  }

//--------------------------------------------------------------------------------------------------

//Example 2: FormBridge.submitForm
  function SubmitForm() {
    var suc = function(obj) {
             var data = obj.data;
         // submit the data to a url;
            }
    var err = function(obj) {
           while(var t = obj.getNextMessage()) {
         $("#errorDiv").append("<div>"+t.message+"</div>");
           }
           }
    formBridge.submitForm({success:suc,error:err}); // not passing a context means that this will be formBridge itself. Validation errors will be checked.
  }
```
