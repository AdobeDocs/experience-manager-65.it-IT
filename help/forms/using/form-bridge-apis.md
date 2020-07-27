---
title: API Form Bridge per moduli HTML5
seo-title: API Form Bridge per moduli HTML5
description: Le applicazioni esterne utilizzano l'API FormBridge per connettersi al modulo mobile XFA. L'API invia un evento FormBridgeInitialized nella finestra principale.
seo-description: Le applicazioni esterne utilizzano l'API FormBridge per connettersi al modulo mobile XFA. L'API invia un evento FormBridgeInitialized nella finestra principale.
uuid: 0db22649-522b-4857-9ffd-826c52381d15
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: developer-reference
discoiquuid: c05c9911-7c49-4342-89de-61b8b9953c83
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 0%

---


# API Form Bridge per moduli HTML5 {#form-bridge-apis-for-html-forms}

È possibile utilizzare le API Form Bridge per aprire un canale di comunicazione tra i moduli HTML5 basati su XFA e le applicazioni. Le API Form Bridge forniscono un&#39;API **connect** per creare la connessione.

L&#39;API **connect** accetta un gestore come argomento. Dopo che è stata creata una connessione corretta tra il modulo HTML5 basato su XFA e il Form Bridge, l&#39;handle viene richiamato.

Per creare la connessione è possibile utilizzare il seguente codice di esempio.

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

## API Form Bridge disponibile  {#available-form-bridge-api-nbsp}

**getBridgeVersion()**

Restituisce il numero di versione della libreria Script

* **Input**: None
* **Output**: Numero di versione della libreria Script
* **Errori**: None

**isConnected()** Controlla se lo stato del modulo è stato inizializzato

* **Input**: None
* **Output**: **True** se lo stato del modulo XFA è stato inizializzato

* **Errori**: None

**connect(handler, context)** Esegue una connessione a FormBridge ed esegue la funzione dopo la connessione e l&#39;inizializzazione dello stato del modulo

* **Input**:

   * **handler**: Funzione da eseguire dopo la connessione di Form Bridge
   * **contesto**: L&#39;oggetto a cui è impostato il contesto (this) della funzione *handler* .

* **Output**: None
* **Errore**: None

**getDataXML(options)** Restituisce i dati del modulo corrente in formato XML

* **Input:**

   * **opzioni:** Oggetto JavaScript contenente le proprietà seguenti:

      * **Errore**: Funzione gestore errori
      * **success**: Funzione gestore di successo. A questa funzione viene passato un oggetto contenente XML nella proprietà *data* .
      * **contesto**: L&#39;oggetto a cui è impostato il contesto (questo) della funzione *success*
      * **validationChecker**: Funzione da chiamare per verificare gli errori di convalida ricevuti dal server. Alla funzione di convalida viene passato un array di stringhe di errore.
      * **formState**: Lo stato JSON del modulo XFA per il quale è necessario restituire i dati XML. Se non viene specificato, restituisce l&#39;XML dei dati per il modulo attualmente rappresentato.

* **Output:** None
* **Errore:** None

**registerConfig(configName, config)** Registra le configurazioni utente/portale specifiche con FormBridge. Queste configurazioni ignorano le configurazioni predefinite. Le configurazioni supportate sono specificate nella sezione di configurazione.

* **Input:**

   * **configName:** Nome della configurazione da ignorare

      * **widgetConfig:** Consente all&#39;utente di ignorare i widget predefiniti nel modulo con widget personalizzati. La configurazione viene sostituita come segue:

         *formBridge.registerConfig(&quot;widgetConfig&quot;:{/&amp;ast;configuration&amp;ast;/})*

      * **pagingConfig:** Consente all&#39;utente di ignorare il comportamento predefinito del rendering solo della prima pagina. La configurazione viene sostituita come segue:

         *window.formBridge.registerConfig(&quot;pagingConfig&quot;:{pagingDisabled: &lt;true | false>, shrinkPageDisabled: &lt;true | false> }).*

      * **LoggingConfig:** Consente all&#39;utente di ignorare il livello di registrazione, disabilitare la registrazione per una categoria o se visualizzare la console dei registri o inviare al server. La configurazione può essere ignorata e sostituita come segue:

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

      * **SubmitServiceProxyConfig:** Consentire agli utenti di registrare i servizi proxy di invio e registrazione.

         ```javascript
         window.formBridge.registerConfig("submitServiceProxyConfig",
         {
         "submitServiceProxy" : "`<submitServiceProxy>`",
         "logServiceProxy": "`<logServiceProxy>`",
         "submitUrl" : "`<submitUrl>`"
         });
         ```
   * **config:** Valore della configurazione



* **Output:** Oggetto contenente il valore originale della configurazione nella proprietà *data* .

* **Errore:** None

**hideFields(fieldArray)** Nasconde i campi le cui espressioni Som sono fornite in fieldArray. Imposta la proprietà presence dei campi specificati su invisibile

* **Input:**

   * **fieldArray:** Array di espressioni Som per i campi da nascondere

* **Output:** None
* **Errore:** None

**showFields(fieldArray)** Mostra i campi le cui espressioni Som sono fornite in fieldArray. Imposta la proprietà presence dei campi forniti su visible

* **Input:**

   * **fieldArray:** Array di espressioni Som per i campi da visualizzare

* **Output:** None
* **Errore:** None

**hideSubmitButtons()** Nasconde tutti i pulsanti Invia del modulo

* **Input**: None
* **Output**: None
* **Errore**: Genera un&#39;eccezione se Stato modulo non è inizializzato

**getFormState()** Restituisce il JSON che rappresenta lo stato del modulo

* **Ingresso:** None
* **Output:** Oggetto contenente JSON che rappresenta lo stato del modulo corrente nella proprietà *data* .

* **Errore:** None

**restoreFormState(options)** Ripristina lo stato del modulo dallo stato JSON fornito nell&#39;oggetto options. Lo stato viene applicato e i gestori di errori o di successo vengono chiamati al termine dell&#39;operazione

* **Input:**

   * **Opzioni:** Oggetto JavaScript contenente le proprietà seguenti:

      * **Errore**: Funzione gestore errori
      * **success**: Funzione gestore di successo
      * **contesto**: L&#39;oggetto a cui è impostato il contesto (questo) della funzione *success*
      * **formState**: Stato JSON del modulo. Il modulo viene ripristinato allo stato JSON.

* **Output:** None
* **Errore:** None

**setFocus (som)** Imposta lo stato attivo sul campo specificato nell&#39;espressione Som

* **Ingresso:** Espressione del campo su cui impostare lo stato attivo
* **Output:** None
* **Errore:** Genera un&#39;eccezione in caso di espressione Som non corretta

**setFieldValue (som, value)** Imposta il valore dei campi per le espressioni Som date

* **Input:**

   * **som:** Array contenente le espressioni Som del campo. La stessa espressione per impostare il valore dei campi.
   * **value:** Array contenente valori corrispondenti alle espressioni Som fornite in un **** array. Se il tipo di dati del valore non è lo stesso di fieldType, il valore non viene modificato.

* **Output:** None
* **Errore:** Genera un&#39;eccezione nel caso di un&#39;espressione Som non corretta

**getFieldValue (som)** Restituisce il valore dei campi per le espressioni Som specificate

* **Ingresso:** Array contenente le espressioni Som dei campi il cui valore deve essere recuperato
* **Output:** Oggetto contenente il risultato come Array nella proprietà **data** .

* **Errore:** None

### Esempio di API getFieldValue() {#example-of-nbsp-getfieldvalue-api}

```JavaScript
var a =  formBridge.getFieldValue(“xfa.form.form1.Subform1.TextField”);
if(a.errors) {
    var err;
     while((err = a.getNextMessage()) != null)
               alert(a.message)
} else {
   alert(a.data[0])
}
```

**getFieldProperties(som, proprietà)** Recupera l&#39;elenco di valori per la proprietà data dei campi specificati nelle espressioni Som

* **Input:**

   * **som:** Array contenente le espressioni Som per i campi
   * **proprietà**: Nome della proprietà il cui valore è obbligatorio

* **Output:** Oggetto contenente il risultato come Array nella proprietà *data*

* **Errore:** None

**setFieldProperties(som, property, values)** Imposta il valore della proprietà data per tutti i campi specificati nelle espressioni Som

* **Input:**

   * **som:** Array contenente le espressioni Som dei campi il cui valore deve essere impostato
   * **proprietà**: Proprietà il cui valore deve essere impostato
   * **value:** Array contenente i valori della proprietà data per i campi specificati nelle espressioni Som

* **Output:** None
* **Errore:** None

## Esempio di utilizzo dell&#39;API Form Bridge {#sample-usage-of-form-bridge-api}

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
