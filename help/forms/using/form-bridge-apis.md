---
title: API di bridge per moduli HTML5
description: Le applicazioni esterne utilizzano l’API FormBridge per connettersi al modulo mobile XFA. L'API invia un evento FormBridgeInitialized nella finestra padre.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: developer-reference
exl-id: b598ef47-49ff-4806-8cc7-4394aa068eaa
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 0%

---

# API di bridge per moduli HTML5 {#form-bridge-apis-for-html-forms}

È possibile utilizzare le API di Forms Bridge per aprire un canale di comunicazione tra moduli HTML5 basati su XFA e le applicazioni. Le API di Forms Bridge forniscono una **connetti** API per creare la connessione.

Il **connetti** L’API accetta un gestore come argomento. Dopo aver creato una connessione tra il modulo HTML5 basato su XFA e il bridge di moduli, viene richiamato l&#39;handle.

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

## API bridge modulo disponibile  {#available-form-bridge-api-nbsp}

**getBridgeVersion()**

Restituisce il numero di versione della libreria Script

* **Input**: nessuna
* **Output**: numero di versione della libreria Scripting
* **Errori**: nessuna

**isConnected()** Verifica se lo stato del modulo è stato inizializzato

* **Input**: nessuna
* **Output**: **Vero** se lo stato del modulo XFA è stato inizializzato

* **Errori**: nessuna

**connect(handler, context)** Effettua una connessione a FormBridge ed esegue la funzione dopo aver stabilito la connessione e aver inizializzato Form State

* **Input**:

   * **handler**: funzione da eseguire dopo la connessione del bridge di moduli
   * **contesto**: l’oggetto a cui è associato il contesto (this) del *handler* funzione.

* **Output**: nessuna
* **Errore**: nessuna

**getDataXML(options)** Restituisce i dati del modulo corrente in formato XML

* **Input:**

   * **opzioni:** Oggetto JavaScript contenente le seguenti proprietà:

      * **Errore**: Funzione gestore errori
      * **success**: funzione di gestore di successo. Questa funzione viene passata come oggetto contenente XML in *dati* proprietà.
      * **contesto**: l’oggetto a cui è associato il contesto (this) del *success* funzione impostata
      * **validationChecker**: funzione da chiamare per controllare gli errori di convalida ricevuti dal server. Alla funzione di convalida viene passata una matrice di stringhe di errore.
      * **formState**: stato JSON del modulo XFA per il quale deve essere restituito l’XML dati. Se non viene specificato, verrà restituito il codice XML dei dati per il modulo di cui è stato eseguito il rendering.

* **Output:** Nessuno
* **Errore:** Nessuno

**registerConfig(configName, config)** Registra le configurazioni specifiche di utenti/portali con FormBridge. Queste configurazioni sostituiscono quelle predefinite. Le configurazioni supportate sono specificate nella sezione di configurazione.

* **Input:**

   * **configName:** Nome della configurazione da ignorare

      * **widgetConfig:** Consente all&#39;utente di sostituire i widget predefiniti nel modulo con widget personalizzati. La configurazione viene sovrascritta come segue:

        *formBridge.registerConfig(&quot;widgetConfig&quot;:{/&amp;ast;configuration&amp;ast;/})*

      * **pagingConfig:** Consente all&#39;utente di ignorare il comportamento predefinito del rendering solo della prima pagina. La configurazione viene sovrascritta come segue:

        *window.formBridge.registerConfig(&quot;pagingConfig&quot;:{pagingDisabled: &lt;true false=&quot;&quot;>, shrinkPageDisabled: &lt;true false=&quot;&quot;> }).*

      * **LoggingConfig** Consente all’utente di ignorare il livello di registrazione, disabilitare la registrazione per una categoria, visualizzare la console dei registri o inviare dati al server. La configurazione può essere sovrascritta come segue:

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

* **Output:** Oggetto contenente il valore originale della configurazione in *dati* proprietà.

* **Errore:** Nessuno

**hideFields(fieldArray)** Nasconde i campi le cui espressioni Som vengono fornite in fieldArray. Imposta la proprietà di presenza dei campi specificati su invisibile

* **Input:**

   * **fieldArray:** Array di alcune espressioni per i campi da nascondere

* **Output:** Nessuno
* **Errore:** Nessuno

**showFields(fieldArray)** Mostra i campi le cui espressioni Som vengono fornite in fieldArray. Imposta la proprietà di presenza dei campi forniti su visibile

* **Input:**

   * **fieldArray:** Array di alcune espressioni per i campi da visualizzare

* **Output:** Nessuno
* **Errore:** Nessuno

**hideSubmitButtons()** Nasconde tutti i pulsanti di invio nel modulo

* **Input**: nessuna
* **Output**: nessuna
* **Errore**: genera un&#39;eccezione se lo stato del modulo non è inizializzato

**getFormState()** Restituisce il JSON che rappresenta lo stato del modulo

* **Input:** Nessuno
* **Output:** Oggetto contenente JSON che rappresenta lo stato corrente del modulo in *dati* proprietà.

* **Errore:** Nessuno

**restoreFormState(options)** Ripristina lo stato del modulo dallo stato JSON fornito nell’oggetto options. Lo stato viene applicato e gli handler di esito positivo o di errore vengono chiamati al termine dell&#39;operazione

* **Input:**

   * **Opzioni:** Oggetto JavaScript contenente le seguenti proprietà:

      * **Errore**: Funzione gestore errori
      * **success**: funzione gestore di successo
      * **contesto**: l’oggetto a cui è associato il contesto (this) del *success* funzione impostata
      * **formState**: stato JSON del modulo. Il modulo viene ripristinato allo stato JSON.

* **Output:** Nessuno
* **Errore:** Nessuno

**setFocus (som)** Imposta lo stato attivo sul campo specificato nell&#39;espressione Som

* **Input:** Espressione del campo su cui impostare lo stato attivo
* **Output:** Nessuno
* **Errore:** Genera un&#39;eccezione se è presente un&#39;espressione Som errata

**setFieldValue (som, value)** Imposta il valore dei campi per le espressioni Som specificate

* **Input:**

   * **som:** Array contenente alcune espressioni del campo. L’espressione som per impostare il valore dei campi.
   * **valore:** Matrice contenente i valori corrispondenti alle espressioni Som fornite in una **som** array. Se il tipo di dati del valore non è uguale a fieldType, il valore non viene modificato.

* **Output:** Nessuno
* **Errore:** Genera un&#39;eccezione se è presente un&#39;espressione Som errata

**getFieldValue (som)** Restituisce il valore dei campi per le espressioni Som specificate

* **Input:** Array contenente alcune espressioni dei campi il cui valore deve essere recuperato
* **Output:** Oggetto contenente il risultato come array in **dati** proprietà.

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

**getFieldProperties(som, proprietà)** Recupera l’elenco di valori per la proprietà specificata dei campi specificati nelle espressioni Som

* **Input:**

   * **som:** Array contenente alcune espressioni per i campi
   * **proprietà**: nome della proprietà il cui valore è obbligatorio

* **Output:** Oggetto contenente il risultato come array in *dati* proprietà

* **Errore:** Nessuno

**setFieldProperties(som, property, values)** Imposta il valore della proprietà specificata per tutti i campi specificati nelle espressioni Som

* **Input:**

   * **som:** Array contenente alcune espressioni dei campi il cui valore deve essere impostato
   * **proprietà**: proprietà il cui valore deve essere impostato
   * **valore:** Array contenente i valori della proprietà specificata per i campi specificati nelle espressioni Som

* **Output:** Nessuno
* **Errore:** Nessuno

## Esempio di utilizzo dell’API di bridge per moduli {#sample-usage-of-form-bridge-api}

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
