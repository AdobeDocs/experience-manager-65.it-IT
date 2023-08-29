---
title: Aggiungere un gestore degli errori personalizzato in Forms adattivo basato su Componenti core per Forms adattivo AEM
seo-title: Error Handlers in Adaptive Forms for AEM Adaptive Forms core components
description: AEM Forms fornisce gestori predefiniti di errori e operazioni riuscite per un modulo che utilizza l’endpoint REST configurato per richiamare un servizio esterno. Puoi aggiungere un gestore degli errori predefinito e personalizzato in un modulo adattivo AEM.
seo-description: Error handler function and Rule Editor in Adaptive Forms core components helps you to effectively manage and customize error handling. You can add a default error handler as well as custom error handler in an AEM Adaptive Form.
keywords: Aggiungi un gestore degli errori personalizzato, aggiungi un gestore degli errori predefinito, aggiungi un gestore degli errori nel modulo, utilizza il servizio invoke dell’editor delle regole per aggiungere un gestore degli errori personalizzato, configura l’editor delle regole per aggiungere un gestore degli errori personalizzato, aggiungi un gestore degli errori personalizzato utilizzando l’editor delle regole
contentOwner: Ruchita Srivastav
content-type: reference
feature: Adaptive Forms
source-git-commit: 28cc10b79d2ac8cf12ddfd0bf7d1a8e013fe6238
workflow-type: tm+mt
source-wordcount: '2284'
ht-degree: 1%

---


# Gestori di errori in Forms adattivo (componenti core) {#error-handlers-in-adaptive-form}

AEM Forms fornisce gestori predefiniti di successo e di errori per l’invio di moduli. Fornisce inoltre funzionalità per personalizzare le funzioni del gestore degli errori. Ad esempio, puoi richiamare un flusso di lavoro personalizzato nel back-end per codici di errore specifici o informare il cliente che il servizio non è disponibile. I gestori sono funzioni lato client che vengono eseguite in base alla risposta del server. Quando un servizio esterno viene richiamato utilizzando le API, i dati vengono trasmessi al server per la convalida, che restituisce una risposta al client con informazioni sull’evento di successo o errore per l’invio. Le informazioni vengono passate come parametri al gestore pertinente per eseguire la funzione. Un gestore degli errori consente di gestire e visualizzare gli errori o i problemi di convalida rilevati.

![flusso di lavoro del gestore degli errori per informazioni su come aggiungere un gestore degli errori personalizzato nei moduli](/help/forms/using/assets/error-handler-workflow.png)

Il modulo adattivo convalida gli input forniti nei campi in base a criteri di convalida predefiniti e verifica la presenza di vari errori restituiti dall’endpoint REST configurato per richiamare un servizio esterno. È possibile impostare i criteri di convalida in base all’origine dati utilizzata con il modulo adattivo. Ad esempio, se utilizzi i servizi web RESTful come origine dati, puoi definire i criteri di convalida in un file di definizione Swagger.

Se i valori di input soddisfano i criteri di convalida, vengono inviati all’origine dati, altrimenti nel modulo adattivo viene visualizzato un messaggio di errore tramite un gestore degli errori. Simile a questo approccio, Forms adattivo si integra con gestori di errori personalizzati per eseguire le convalide dei dati. Se i valori di input non soddisfano i criteri di convalida, i messaggi di errore vengono visualizzati a livello di campo nel modulo adattivo. Ciò si verifica quando il messaggio di errore di convalida restituito dal server è nel formato di messaggio standard.


## Utilizzo dei gestori di errori {#uses-of-error-handler}

I gestori di errori vengono utilizzati per vari scopi. Di seguito sono elencati alcuni degli utilizzi delle funzioni di gestione degli errori:

* **Esegui convalida**: la gestione degli errori inizia con la convalida degli input dell’utente in base a regole o criteri predefiniti. Quando gli utenti compilano un modulo adattivo, il gestore degli errori convalida l’input per garantire che soddisfi il formato, la lunghezza o qualsiasi altro vincolo richiesto.

* **Fornire feedback in tempo reale**: quando viene rilevato un errore, il gestore degli errori visualizza un feedback immediato all’utente, ad esempio messaggi di errore in linea sotto i campi del modulo corrispondenti. Questo feedback consente agli utenti di identificare e correggere gli errori senza dover inviare il modulo e attendere una risposta.


* **Visualizzare messaggi di errore**: quando un invio di un modulo adattivo rileva un errore di convalida, il gestore degli errori visualizza un messaggio di errore appropriato. I messaggi di errore devono essere chiari, concisi ed evidenziati nei campi specifici che richiedono attenzione.

* **Evidenzia il campo errato**: per attirare l’attenzione dell’utente su campi non corretti specifici, il gestore degli errori evidenzia o distingue visivamente i campi corrispondenti. Viene eseguita modificando il colore di sfondo, aggiungendo un&#39;icona o un bordo o qualsiasi altro segnale visivo che consenta agli utenti di individuare e risolvere rapidamente gli errori.


## Formato della risposta di errore/errore {#failure-response-format}

Un modulo adattivo visualizza gli errori a livello di campo se i messaggi di errore di convalida del server sono nel seguente formato standard.
Il codice riportato di seguito illustra la struttura di risposta dei guasti esistente:

```javascript
   {
    errorCausedBy : "SERVER_SIDE_VALIDATION/SERVICE_INVOCATION_FAILURE"
    errors : [
        {
             errorMessage / errorMessages : <validationMsg> / [<validationMsg>, <validationMsg>]
        }
    ]
    originCode : <target error Code>
    originMessage : <unstructured error message returned by service>
    }
```


Dove:

* `errorCausedBy` descrive il motivo dell’errore.
* `errors` menziona il nome del campo qualificato dei campi che non hanno soddisfatto i criteri di convalida insieme al messaggio di errore di convalida.
* `originCode` aggiunto dall’AEM e contiene il codice di stato http restituito dal servizio esterno.
* `originMessage` aggiunto dall’AEM e contiene i dati non elaborati sull’errore restituiti dal servizio esterno.

Con i miglioramenti delle funzioni e i successivi aggiornamenti delle versioni di AEM Forms, la struttura di risposta dei guasti esistente è stata modificata in un nuovo formato basato su RFC7807, compatibile con le versioni precedenti della struttura di risposta dei guasti esistente:

```javascript
    {
        "type": "SERVER_SIDE_VALIDATION/FORM_SUBMISSION/SERVICE_INVOCATION/FAILURE/VALIDATION_ERROR", (required)
        "title": "Server side validation failed/Third party service invocation failed", (optional)
        "detail": "", (optional)
        "instance": "", (optional)
        "validationErrors" : [ (required)
            {
                "fieldName":"<qualified fieldname of the field whose data sent is invalid>",
                "dataRef":<JSONPath (or XPath) of the data element which is invalid>
                "details": ["Error Message(s) for the field"] (required)
    
            }
        ],
        "originCode": <Origin http status code>, (optional - in case of SERVER_SIDE_VALIDATION)
        "originMessage" : "<unstructured error message returned by service>" (optional - in case of SERVER_SIDE_VALIDATION)
    }
```


>[!NOTE]
>
> * Assicurati che la struttura della risposta all’errore includa **fieldName** o **dataRef**.
> * Assicurati che **ContentType** l’intestazione è **application/problem+json**.

Dove:
* `type (required)` specifica il tipo di errore. Può corrispondere a uno dei seguenti valori:
   * `SERVER_SIDE_VALIDATION` indica un errore dovuto alla convalida lato server.
   * `FORM_SUBMISSION` indica un errore durante l’invio del modulo
   * `SERVICE_INVOCATION` indica un errore durante una chiamata di un servizio di terze parti.
   * `FAILURE` indica un errore generale.
   * `VALIDATION_ERROR` indica un errore dovuto a un errore di convalida.

* `title (optional)` fornisce un titolo o una breve descrizione dell’errore.
* `detail (optional)` fornisce ulteriori dettagli sull’errore, se necessario.
* `instance (optional)` rappresenta un&#39;istanza o un identificatore associato all&#39;errore e consente di tenere traccia o identificare l&#39;occorrenza specifica dell&#39;errore.
* `validationErrors (required)` contiene informazioni sugli errori di convalida. Include i campi seguenti:
   * `fieldname` cita il nome del campo qualificato dei campi che non soddisfano i criteri di convalida.
   * `dataRef` rappresenta il percorso JSON o XPath dei campi che non hanno superato la convalida.
   * `details` contiene il messaggio di errore di convalida con il campo errato.
* `originCode (optional)` aggiunto dall’AEM e contiene il codice di stato http restituito dal servizio esterno
* `originMessage (optional)` aggiunto dall’AEM e contiene i dati non elaborati sull’errore restituiti dal servizio esterno.

### Formato risposta errore di esempio {#sample-error-response-format}

Alcune delle opzioni per visualizzare le risposte di errore sono:

+++  In base alla proprietà fieldName del modulo adattivo


* **`Header:`** `content-type:application/problem+json`
* **`Response:`**

  ```javascript
          {
              "type": "VALIDATION_ERROR",
              "validationErrors": [
              {
              "fieldName": "$form.PetId",
              "dataRef": "",
              "details": [
              "Invalid ID supplied. Provided value is not correct!"
          ]
          }
          ]}
  ```


+++


+++ In base alla proprietà dataRef del modulo adattivo

* **`Header:`** `content-type:application/problem+json`
* **`Response:`**

  ```javascript
      {
          "type": "VALIDATION_ERROR",
          "validationErrors": [
          {
              "fieldName": "",
              "dataRef": "$.Pet.id",
              "details": [
              "Invalid ID supplied. Provided value is not correct!"
              ]
              }
      ]}
  ```

+++

## Prerequisiti {#prerequisites}

Prima di utilizzare il gestore degli errori in un Forms adattivo:

* [Abilitare i componenti core Forms adattivi per il tuo ambiente AEM Cloud Service](enable-adaptive-forms-core-components.md).
* Conoscenza di base per [creare una funzione personalizzata](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/adaptive-forms/custom-functions-aem-forms.html?lang=en#:~:text=AEM%20Forms%206.5%20introduced%20the,use%20them%20across%20multiple%20forms.).
* Installa la versione più recente di [Apache Maven](https://maven.apache.org/download.cgi).

## Aggiungi gestore errori tramite l’Editor regole {#add-error-handler-using-rule-editor}

Utilizzo di [Servizio di richiamo dell’editor di regole](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=en#invoke) , è possibile definire i criteri di convalida in base all&#39;origine dati utilizzata con il modulo adattivo. Se si utilizzano i servizi Web RESTful come origine dati, è possibile definire i criteri di convalida in un file di definizione Swagger. Utilizzando le funzioni di gestore degli errori e l’editor di regole in Adaptive Forms, puoi gestire e personalizzare in modo efficace la gestione degli errori. Definisci le condizioni utilizzando l’Editor regole e configura le azioni da eseguire quando la regola viene attivata. Il modulo adattivo convalida gli input immessi nei campi in base a criteri di convalida predefiniti. Se i valori di input non soddisfano i criteri di convalida, i messaggi di errore vengono visualizzati a livello di campo in un modulo adattivo.

>[!NOTE]
>
> * Per utilizzare i gestori di errori con l’azione Richiama del servizio dell’editor di regole, configura Forms adattivo con un modello di dati del modulo.
> * Se la risposta di errore si trova nello schema standard, viene fornito un gestore degli errori predefinito per visualizzare i messaggi di errore sui campi. È inoltre possibile chiamare il gestore degli errori predefinito dalla funzione del gestore degli errori personalizzato.

Utilizzando l’editor di regole, puoi:

* [Aggiungi funzione gestore errori predefinita](#add-default-errror-handler)
* [Aggiungi funzione di gestione degli errori personalizzata](#add-custom-errror-handler)


### Aggiungi funzione gestore errori predefinita {#add-default-errror-handler}

È supportato un gestore degli errori predefinito per visualizzare i messaggi di errore sui campi se la risposta di errore si trova nello schema standard o in un errore di convalida lato server.
Per informazioni su come utilizzare un gestore degli errori predefinito utilizzando [Servizio di richiamo dell’editor di regole](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=en#invoke) , ad esempio un semplice modulo adattivo con due campi, **ID animale domestico** e **Nome animale domestico** e utilizza un gestore degli errori predefinito in corrispondenza di **ID animale domestico** per verificare la presenza di vari errori restituiti dall’endpoint REST configurato per richiamare un servizio esterno, ad esempio, `200 - OK`,`404 - Not Found`, `400 - Bad Request`. Per aggiungere un gestore degli errori predefinito tramite l’azione Richiama servizio dell’editor di regole, esegui i passaggi seguenti:

1. Apri un modulo adattivo in modalità di authoring, seleziona un componente modulo e tocca **[!UICONTROL Editor regole]** per aprire l’editor di regole.
1. Tocca **[!UICONTROL Crea]**.
1. Creare una condizione in **Quando** sezione della regola. Ad esempio: **Quando[Nome del campo ID animale domestico]** è stato modificato. Seleziona viene modificato dal **Seleziona stato** elenco a discesa.
1. In **Then** sezione, seleziona **[!UICONTROL Richiama servizio]** dal **Seleziona azione** elenco a discesa.
1. Seleziona un **Servizio post** e le associazioni di dati corrispondenti dalla **Input** sezione. Ad esempio, per convalidare **ID animale domestico**, seleziona un **Servizio post** as **GET /pet/{petId}** e seleziona **ID animale domestico** nel **Input** sezione.
1. Seleziona le associazioni di dati da **Output** sezione. Seleziona **Nome animale domestico** nel **Output** sezione.
1. Seleziona **[!UICONTROL Gestore errori predefinito]** dal **Gestore errori** sezione.
1. Clic **[!UICONTROL Fine]**.

![aggiungere un gestore errori predefinito per i controlli di convalida dei campi in un modulo](/help/forms/using/assets/default-error-handler.png)

Come risultato di questa regola, i valori immessi per **ID animale domestico** verifica la convalida per **Nome animale domestico** utilizzo di un servizio esterno richiamato dall’endpoint REST. Se i criteri di convalida basati sull’origine dati non riescono, i messaggi di errore vengono visualizzati a livello di campo.

![visualizza il messaggio di errore predefinito quando si aggiunge un gestore degli errori predefinito in un modulo per gestire le risposte di errore](/help/forms/using/assets/default-error-message.png)

### Aggiungi funzione di gestione degli errori personalizzata {#add-custom-errror-handler}

È possibile aggiungere una funzione di gestione degli errori personalizzata per eseguire alcune delle azioni seguenti:

* gestisce le risposte di errore che utilizzano risposte di errore non standard o standard. È importante notare che queste risposte di errore non standard non sono conformi al [schema standard di risposte di errore](#failure-response-format).
* invia eventi di analytics a qualsiasi piattaforma di analytics. Ad esempio, Adobe Analytics.
* visualizza la finestra di dialogo modale con messaggi di errore.

Oltre alle azioni menzionate, i gestori degli errori personalizzati possono essere utilizzati per eseguire funzioni personalizzate che soddisfano requisiti utente specifici.

Il gestore degli errori personalizzati è una funzione (libreria client) progettata per rispondere agli errori restituiti da un servizio esterno e fornire una risposta personalizzata agli utenti finali. Qualsiasi libreria client con annotazione `@errorHandler` è considerata una funzione di gestione degli errori personalizzata. Questa annotazione consente di identificare la funzione di gestione degli errori specificata in `.js` file.

Per informazioni su come creare e utilizzare un gestore degli errori personalizzato utilizzando [Servizio Invoke dell&#39;editor di regole](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html?lang=en#invoke) , prendiamo un esempio di modulo adattivo con due campi, **ID animale domestico** e **Nome animale domestico** e utilizza un gestore degli errori personalizzato in corrispondenza di **ID animale domestico** per verificare la presenza di vari errori restituiti dall’endpoint REST configurato per richiamare un servizio esterno, ad esempio, `200 - OK`,`404 - Not Found`, `400 - Bad Request`.

Per aggiungere e utilizzare un gestore di errori personalizzato in un modulo adattivo, effettua le seguenti operazioni:

1. [Creare un gestore degli errori personalizzato](#create-custom-error-message)
1. [Utilizza l’Editor regole per configurare un gestore degli errori personalizzato](#use-custom-error-handler)

#### 1. Creare un gestore degli errori personalizzato {#create-custom-error-message}

Per creare una funzione di errore personalizzata, effettuare le seguenti operazioni:

1. Accedi a `http://server:port/crx/de/index.jsp#`.
1. Creare una cartella in `/apps` cartella. Ad esempio, crea una cartella denominata come `experience-league`.
1. Salva le modifiche.
1. Passa alla cartella creata e crea un nodo di tipo `cq:ClientLibraryFolder` as `clientlibs`.
1. Passa alla nuova `clientlibs` cartella e aggiungi `allowProxy` e `categories` proprietà:

   ![Proprietà del nodo della libreria personalizzata](/help/forms/using/assets/customlibrary-properties.png)

   >[!NOTE]
   >
   > Puoi fornire qualsiasi nome al posto di `customfunctionsdemo`.

1. Salva le modifiche.

1. Crea una cartella denominata `js` sotto `clientlibs` cartella.
1. Creare un file JavaScript denominato `functions.js` sotto `js` cartella
1. Crea un file denominato `js.txt` sotto `clientlibs` cartella.
1. Salva le modifiche.
La struttura di cartelle creata è simile alla seguente:

   ![Struttura delle cartelle della libreria client creata](/help/forms/using/assets/customclientlibrary_folderstructure.png)
1. Fai doppio clic su `functions.js` per aprire l’editor. Il file contiene il codice per il gestore degli errori personalizzato.
Aggiungiamo il seguente codice al file JavaScript per visualizzare la risposta e le intestazioni, ricevute dall’endpoint del servizio REST, nella console del browser.

   ```javascript
       /** 
       Custom Error handler
       * @name customErrorHandler Custom Error Handler Function
       * @errorHandler
       */
       function customErrorHandler(response, headers, globals)
       {
           console.log("Custom Error Handler processing start...");
           console.log("response:"+JSON.stringify(response));
           console.log("headers:"+JSON.stringify(headers));
           alert("CustomErrorHandler - Please enter valid PetId.")
           globals.invoke('defaultErrorHandler',response, headers)
           console.log("Custom Error Handler processing end...");
       }
   ```

   Per chiamare il gestore errori predefinito dal gestore errori personalizzato, viene utilizzata la seguente riga del codice di esempio:
   `globals.invoke('defaultErrorHandler',response, headers) `

1. Salva `function.js`.
1. Accedi a `js.txt` e aggiungi il seguente codice:

   ```javascript
       #base=js
       functions.js
   ```

1. Salva il `js.txt` file.

Ora vediamo come configurare e utilizzare un gestore di errori personalizzato utilizzando il servizio Invoke dell’editor di regole in AEM Forms.

#### 2. Utilizza l’Editor regole per configurare un gestore degli errori personalizzato {#use-custom-error-handler}

Prima di implementare il gestore degli errori personalizzato in un modulo adattivo, assicurati che il nome della libreria client nel **[!UICONTROL Categoria libreria client]** allinea con il nome specificato nell&#39;opzione categorie della `.content.xml` file.

![Aggiunta del nome della libreria client nella configurazione del contenitore di moduli adattivi](/help/forms/using/assets/client-library-category-name-core-component.png)

In questo caso, il nome della libreria client viene fornito come `customfunctionsdemo` nel `.content.xml` file.

Per utilizzare un gestore degli errori personalizzato utilizzando **[!UICONTROL Servizio di richiamo dell’editor di regole]** azione:

1. Apri un modulo adattivo in modalità di authoring, seleziona un componente modulo e tocca **[!UICONTROL Editor regole]** per aprire l’editor di regole.
1. Tocca **[!UICONTROL Crea]**.
1. Creare una condizione in **Quando** sezione della regola. Ad esempio, Quando **[Nome del campo ID animale domestico]** è stato modificato, seleziona **è stato modificato** dal **Seleziona stato** elenco a discesa.
1. In **Then** sezione, seleziona **[!UICONTROL Richiama servizio]** dal **Seleziona azione** elenco a discesa.
1. Seleziona un **Servizio post** e le associazioni di dati corrispondenti dalla **Input** sezione. Ad esempio, per convalidare **ID animale domestico**, seleziona un **Servizio post** as **GET /pet/{petId}** e seleziona **ID animale domestico** nel **Input** sezione.
1. Seleziona le associazioni di dati da **Output** sezione. Ad esempio, seleziona **Nome animale domestico** nel **Output** sezione.
1. Seleziona **[!UICONTROL Gestore errori personalizzato]** dal **[!UICONTROL Gestore errori]** sezione.
1. Clic **[!UICONTROL Fine]**.

![aggiungere un gestore degli errori personalizzato in un modulo per gestire le risposte di errore](/help/forms/using/assets/custom-error-handler.png)

Come risultato di questa regola, i valori immessi per **ID animale domestico** verifica la convalida per **Nome animale domestico** utilizzo di un servizio esterno richiamato dall’endpoint REST. Se i criteri di convalida basati sull’origine dati non riescono, i messaggi di errore vengono visualizzati a livello di campo.

![aggiungere un gestore degli errori personalizzato in un modulo per gestire le risposte di errore](/help/forms/using/assets/custom-error-handler-message-core-component.png)

Apri la console del browser e controlla la risposta e l’intestazione, ricevute dall’endpoint del servizio REST, per il messaggio di errore di convalida.

La funzione del gestore degli errori personalizzato è responsabile dell’esecuzione di azioni aggiuntive, ad esempio la visualizzazione di una finestra di dialogo modale o l’invio di un evento di analisi, in base alla risposta all’errore. Una funzione di gestione degli errori personalizzata offre la flessibilità necessaria per adattare la gestione degli errori ai requisiti utente specifici.
