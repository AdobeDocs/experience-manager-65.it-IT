---
title: API di Form Bridge per moduli HTML5
seo-title: Form Bridge APIs for HTML5 forms
description: Le applicazioni esterne utilizzano l’API FormBridge per connettersi al modulo mobile XFA. L'API invia un evento FormBridgeInitialized nella finestra principale.
seo-description: External applications use the FormBridge API to connect to the XFA Mobile Form. The API dispatches a FormBridgeInitialized event on the parent window.
uuid: 0db22649-522b-4857-9ffd-826c52381d15
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: developer-reference
discoiquuid: c05c9911-7c49-4342-89de-61b8b9953c83
exl-id: b598ef47-49ff-4806-8cc7-4394aa068eaa
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 0%

---

# API di Form Bridge per moduli HTML5 {#form-bridge-apis-for-html-forms}

È possibile utilizzare le API Form Bridge per aprire un canale di comunicazione tra un modulo HTML5 basato su XFA e le applicazioni. Le API di Form Bridge forniscono un **connect** API per creare la connessione.

La **connect** L&#39;API accetta un gestore come argomento. Dopo la creazione di una connessione corretta tra il modulo HTML5 basato su XFA e il Form Bridge, viene richiamato l&#39;handle.

Puoi usare il seguente codice di esempio per creare la connessione.

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

## API disponibile per Form Bridge  {#available-form-bridge-api-nbsp}

**getBridgeVersion()**

Restituisce il numero di versione della libreria di script

* **Ingresso**: Nessuno
* **Uscita**: Numero di versione della libreria di script
* **Errori**: Nessuno

**isConnected()** Controlla se lo stato del modulo è stato inizializzato

* **Ingresso**: Nessuno
* **Uscita**: **True** se lo stato del modulo XFA è stato inizializzato

* **Errori**: Nessuno

**connect(handler, context)** Esegue una connessione a FormBridge ed esegue la funzione dopo la connessione e l&#39;inizializzazione di Form State

* **Input**:

   * **handler**: Funzione da eseguire dopo la connessione di Form Bridge
   * **contesto**: L&#39;oggetto a cui il contesto (questo) del *handler* sono impostati.

* **Uscita**: Nessuno
* **Errore**: Nessuno

**getDataXML(options)** Restituisce i dati del modulo corrente in formato XML

* **Input:**

   * **opzioni:** Oggetto JavaScript contenente le proprietà seguenti:

      * **Errore**: Funzione Error Handler
      * **success**: Funzione del gestore di successo. A questa funzione viene passato un oggetto contenente XML in *dati* proprietà.
      * **contesto**: L&#39;oggetto a cui il contesto (questo) del *success* funzione impostata
      * **validationChecker**: Funzione da chiamare per controllare gli errori di convalida ricevuti dal server. Alla funzione di convalida viene passato un array di stringhe di errore.
      * **formState**: Lo stato JSON del modulo XFA per il quale deve essere restituito XML di dati. Se non viene specificato, restituisce l’XML dei dati per il modulo attualmente sottoposto a rendering.

* **Uscita:** Nessuno
* **Errore:** Nessuno

**registerConfig(configName, config)** Registra le configurazioni specifiche di utente/portale con FormBridge. Queste configurazioni sostituiscono le configurazioni predefinite. Le configurazioni supportate sono specificate nella sezione di configurazione .

* **Ingresso:**

   * **configName:** Nome della configurazione da sovrascrivere

      * **widgetConfig:** Consente all’utente di sostituire i widget predefiniti nel modulo con widget personalizzati. La configurazione viene ignorata come segue:

         *formBridge.registerConfig(&quot;widgetConfig&quot;:{/&amp;ast;configuration&amp;ast;/})*

      * **pagingConfig:** Consente all’utente di ignorare il comportamento predefinito del rendering solo della prima pagina. La configurazione viene ignorata come segue:

         *window.formBridge.registerConfig(&quot;pagingConfig&quot;:{pagingDisabled: &lt;true false=&quot;&quot;>, shrinkPageDisabled: &lt;true false=&quot;&quot;> }).*

      * **LoggingConfig:** Consente all’utente di ignorare il livello di registrazione, disattivare la registrazione per una categoria o se visualizzare la console dei registri o inviare al server. La configurazione può essere ignorata come segue:

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

      * **SubmitServiceProxyConfig:** Consenti agli utenti di registrare i servizi proxy di invio e registrazione.

         ```javascript
         window.formBridge.registerConfig("submitServiceProxyConfig",
         {
         "submitServiceProxy" : "`<submitServiceProxy>`",
         "logServiceProxy": "`<logServiceProxy>`",
         "submitUrl" : "`<submitUrl>`"
         });
         ```
   * **config:** Valore della configurazione



* **Uscita:** Oggetto contenente il valore originale della configurazione in *dati* proprietà.

* **Errore:** Nessuno

**hideFields(fieldArray)** Nasconde i campi di cui sono fornite le espressioni Som nel campoArray. Imposta la proprietà presence dei campi specificati su invisible

* **Ingresso:**

   * **fieldArray:** Array di espressioni Som per i campi da nascondere

* **Uscita:** Nessuno
* **Errore:** Nessuno

**showFields(fieldArray)** Mostra i campi di cui sono fornite le espressioni Som nel campoArray. Imposta la proprietà presence dei campi forniti su visible

* **Ingresso:**

   * **fieldArray:** Array di espressioni Som per i campi da visualizzare

* **Uscita:** Nessuno
* **Errore:** Nessuno

**hideSubmitButtons()** Nasconde tutti i pulsanti di invio del modulo

* **Ingresso**: Nessuno
* **Uscita**: Nessuno
* **Errore**: Genera un&#39;eccezione se Stato modulo non è inizializzato

**getFormState()** Restituisce il JSON che rappresenta lo stato del modulo

* **Ingresso:** Nessuno
* **Uscita:** Oggetto contenente JSON che rappresenta lo stato del modulo corrente in *dati* proprietà.

* **Errore:** Nessuno

**restoreFormState(options)** Ripristina lo stato del modulo dallo stato JSON fornito nell’oggetto options . Lo stato viene applicato e i gestori di errori o di successo vengono chiamati al termine dell’operazione

* **Ingresso:**

   * **Opzioni:** Oggetto JavaScript contenente le proprietà seguenti:

      * **Errore**: Funzione Error Handler
      * **success**: Funzione handler di successo
      * **contesto**: L&#39;oggetto a cui il contesto (questo) del *success* sono impostate
      * **formState**: Stato JSON del modulo. Il modulo viene ripristinato allo stato JSON.

* **Uscita:** Nessuno
* **Errore:** Nessuno

**setFocus (som)** Imposta lo stato attivo sul campo specificato nell&#39;espressione Som

* **Ingresso:** Espressione del campo su cui impostare lo stato attivo
* **Uscita:** Nessuno
* **Errore:** Genera un&#39;eccezione in caso di espressione Som errata

**setFieldValue (som, value)** Imposta il valore dei campi per le espressioni Som specificate

* **Ingresso:**

   * **som:** Array contenente espressioni Som del campo. La stessa espressione per impostare il valore dei campi.
   * **valore:** Array contenente valori corrispondenti alle espressioni Som fornite in un **som** array. Se il tipo di dati del valore non è lo stesso di fieldType, il valore non viene modificato.

* **Uscita:** Nessuno
* **Errore:** Genera un’eccezione nel caso di un’espressione Som errata

**getFieldValue (som)** Restituisce il valore dei campi per le espressioni Som specificate

* **Ingresso:** Array contenente espressioni Som dei campi il cui valore deve essere recuperato
* **Uscita:** Oggetto contenente il risultato come Array in **dati** proprietà.

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

**getFieldProperties(som, proprietà)** Recupera l’elenco dei valori per la proprietà specificata dei campi specificati nelle espressioni Som

* **Ingresso:**

   * **som:** Array contenente espressioni Som per i campi
   * **property**: Nome della proprietà il cui valore è obbligatorio

* **Uscita:** Oggetto contenente il risultato come Array in *dati* property

* **Errore:** Nessuno

**setFieldProperties(som, property, values)** Imposta il valore della proprietà specificata per tutti i campi specificati nelle espressioni Som

* **Ingresso:**

   * **som:** Array contenente espressioni Som dei campi il cui valore deve essere impostato
   * **property**: Proprietà il cui valore deve essere impostato
   * **valore:** Array contenente i valori della proprietà specificata per i campi specificati nelle espressioni Som

* **Uscita:** Nessuno
* **Errore:** Nessuno

## Utilizzo di esempio dell’API di Form Bridge {#sample-usage-of-form-bridge-api}

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
