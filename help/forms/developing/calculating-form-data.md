---
title: Calcolo dati modulo
seo-title: Calculating Form Data
description: Utilizzare il servizio Forms per calcolare i valori immessi da un utente in un modulo e visualizzare i risultati. Il servizio Forms calcola i valori utilizzando l’API Java e l’API del servizio web.
seo-description: Use the Forms service to calculate values that a user enters into a form and display the results. Forms service calculates the values using the Java API and Web Service API.
uuid: ccd85bc7-8ccc-44d9-9424-dfc1f603e688
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: b4f57e42-60a6-407d-9764-15a11615827d
role: Developer
exl-id: 28abf044-6c8e-4578-ae2e-54cdbd694c5f
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1878'
ht-degree: 1%

---

# Calcolo dati modulo {#calculating-form-data}

**Gli esempi e gli esempi contenuti in questo documento sono solo per l’ambiente AEM Forms su JEE.**

Il servizio Forms può calcolare i valori immessi da un utente in un modulo e visualizzarne i risultati. Per calcolare i dati del modulo, è necessario eseguire due attività. Innanzitutto, è possibile creare uno script di progettazione del modulo che calcola i dati del modulo. La progettazione di un modulo supporta tre tipi di script. Un tipo di script viene eseguito sul client, un altro sul server e il terzo sul server e sul client. Il tipo di script descritto in questo argomento viene eseguito sul server. I calcoli lato server sono supportati per le trasformazioni HTML, PDF e guida ai moduli (obsolete).

Come parte del processo di progettazione del modulo, è possibile utilizzare calcoli e script per fornire un’esperienza utente più ricca. È possibile aggiungere calcoli e script alla maggior parte dei campi e degli oggetti del modulo. È necessario creare uno script di progettazione del modulo per eseguire operazioni di calcolo sui dati immessi da un utente in un modulo interattivo.

L’utente immette i valori nel modulo e fa clic sul pulsante Calcola per visualizzare i risultati. Il processo seguente descrive un esempio di applicazione che consente a un utente di calcolare i dati:

* L’utente accede a una pagina HTML denominata StartLoan.html che funge da pagina iniziale dell’applicazione web. Questa pagina richiama un servlet Java denominato `GetLoanForm`.
* Il `GetLoanForm` servlet esegue il rendering di un modulo prestito. Questo modulo contiene uno script, campi interattivi, un pulsante di calcolo e un pulsante di invio.
* L’utente immette i valori nei campi del modulo e fa clic sul pulsante Calcola. Il modulo viene inviato al `CalculateData` Servlet Java in cui viene eseguito lo script. Il modulo viene inviato nuovamente all’utente con i risultati del calcolo visualizzati nel modulo.
* L’utente continua a immettere e calcolare i valori fino a quando non viene visualizzato un risultato soddisfacente. Al termine dell’operazione, l’utente fa clic sul pulsante Invia per elaborare il modulo. Il modulo viene inviato a un altro servlet Java denominato `ProcessForm` che è responsabile del recupero dei dati inviati. (vedere [Gestione dei Forms inviati](/help/forms/developing/rendering-forms.md#handling-submitted-forms).)


Il diagramma seguente mostra il flusso logico dell’applicazione.

![cf_cf_finsrv_loancalcapp_v1](assets/cf_cf_finsrv_loancalcapp_v1.png)

Nella tabella seguente vengono descritti i passaggi del diagramma.

<table>
 <thead>
  <tr>
   <th><p>Passaggio</p></th>
   <th><p>Descrizione</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>Il <code>GetLoanForm</code> Java Servlet viene richiamato dalla pagina iniziale di HTML. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Il <code>GetLoanForm</code> Java Servlet utilizza l’API client del servizio Forms per eseguire il rendering del modulo di prestito sul browser web client. La differenza tra il rendering di un modulo che contiene uno script configurato per l'esecuzione sul server e il rendering di un modulo che non contiene uno script consiste nel fatto che è necessario specificare la posizione di destinazione utilizzata per eseguire lo script. Se non si specifica un percorso di destinazione, non viene eseguito uno script configurato per l'esecuzione sul server. Ad esempio, considera l’applicazione introdotta in questa sezione. Il <code>CalculateData</code> Java Servlet è il percorso di destinazione in cui viene eseguito lo script.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>L’utente immette i dati nei campi interattivi e fa clic sul pulsante Calcola. Il modulo viene inviato al <code>CalculateData</code> Java Servlet, dove viene eseguito lo script. </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Viene eseguito il rendering del modulo nel browser web con i risultati del calcolo visualizzati nel modulo. </p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>Quando i valori sono soddisfacenti, l’utente fa clic sul pulsante Invia. Il modulo viene inviato a un altro servlet Java denominato <code>ProcessForm</code>.</p></td>
  </tr>
 </tbody>
</table>

In genere, un modulo inviato come contenuto PDF contiene script eseguiti sul client. Tuttavia, è anche possibile eseguire calcoli lato server. Impossibile utilizzare un pulsante Invia per calcolare gli script. In questa situazione, i calcoli non vengono eseguiti perché il servizio Forms considera l’interazione completa.

Per illustrare l&#39;utilizzo di uno script di progettazione di un modulo, in questa sezione viene esaminato un semplice modulo interattivo contenente uno script configurato per l&#39;esecuzione sul server. Nel diagramma seguente viene illustrata una struttura di modulo contenente uno script che consente di aggiungere valori immessi da un utente nei primi due campi e di visualizzare il risultato nel terzo campo.

![cf_cf_caldata](assets/cf_cf_caldata.png)

**R.** Campo denominato NumericField1 **B.** Campo denominato NumericField2 **C.** Campo denominato NumericField3

La sintassi dello script in questa struttura di modulo è la seguente:

```javascript
     NumericField3 = NumericField2 + NumericField1
```

In questa struttura di modulo, il pulsante Calcola è un pulsante di comando e lo script si trova nel `Click` evento. Quando un utente immette valori nei primi due campi (NumericField1 e NumericField2) e fa clic sul pulsante Calcola, il modulo viene inviato al servizio Forms, dove viene eseguito lo script. Il servizio Forms restituisce il modulo al dispositivo client con i risultati del calcolo visualizzati nel campo NumericField3.

>[!NOTE]
>
>Per informazioni sulla creazione di uno script di progettazione del modulo, vedere [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63_it).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, consulta [Guida di riferimento dei servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per calcolare i dati del modulo, effettuare le seguenti operazioni:

1. Includi file di progetto.
1. Crea un oggetto API client di Forms.
1. Recuperare un modulo contenente uno script di calcolo.
1. Riscrivere il flusso di dati del modulo nel browser Web client

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, accertati di includere i file proxy.

**Creare un oggetto API client di Forms**

Prima di poter eseguire a livello di programmazione un&#39;operazione API client del servizio Forms, è necessario creare un client del servizio Forms. Se utilizzi l’API Java, crea un’ `FormsServiceClient` oggetto. Se utilizzi l’API del servizio web Forms, crea un’ `FormsServiceService` oggetto.

**Recuperare un modulo contenente uno script di calcolo**

Utilizzare l&#39;API client del servizio Forms per creare una logica dell&#39;applicazione che gestisce un modulo contenente uno script configurato per l&#39;esecuzione sul server. Il processo è simile alla gestione di un modulo inviato. (vedere [Gestione dei Forms inviati](/help/forms/developing/handling-submitted-forms.md).)

Verifica che lo stato di elaborazione associato al modulo inviato sia `1` `(Calculate)`, il che significa che il servizio Forms sta eseguendo un’operazione di calcolo sui dati del modulo e che i risultati devono essere riscritti all’utente. In questa situazione, uno script configurato per l&#39;esecuzione sul server viene eseguito automaticamente.

**Riscrivere il flusso di dati del modulo nel browser Web client**

Dopo aver verificato che lo stato di elaborazione associato a un modulo inviato sia `1`, è necessario riscrivere i risultati nel browser Web client. Quando viene visualizzato il modulo, il valore calcolato viene visualizzato nel campo o nei campi appropriati.

**Consulta anche**

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[Calcolare i dati del modulo utilizzando l’API Java](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-java-api)
[Calcolare i dati del modulo utilizzando l’API del servizio web](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-web-service-api)
[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
[Guida introduttiva all’API di servizio Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)
[Rendering dei PDF forms interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md)
[Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Calcolare i dati del modulo utilizzando l’API Java {#calculate-form-data-using-the-java-api}

Calcola i dati del modulo utilizzando l’API Forms (Java):

1. Includi file di progetto

   Includi i file JAR client, ad esempio adobe-forms-client.jar nel percorso di classe del progetto Java.

1. Creare un oggetto API client di Forms

   * Creare un `ServiceClientFactory` oggetto che contiene proprietà di connessione.
   * Creare un `FormsServiceClient` mediante il costruttore e passando il `ServiceClientFactory` oggetto.

1. Recuperare un modulo contenente uno script di calcolo

   * Per recuperare i dati del modulo che contengono uno script di calcolo, creare un `com.adobe.idp.Document` mediante il costruttore e richiamando l&#39;oggetto `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getInputStream` metodo dall&#39;interno del costruttore.
   * Richiama `FormsServiceClient` dell&#39;oggetto `processFormSubmission` e trasmettere i seguenti valori:

      * Il `com.adobe.idp.Document` oggetto che contiene i dati del modulo.
      * Valore stringa che specifica le variabili di ambiente, incluse tutte le intestazioni HTTP rilevanti. Specificare il tipo di contenuto da gestire specificando uno o più valori per `CONTENT_TYPE` variabile di ambiente. Ad esempio, per gestire i dati XML e PDF, specificare il seguente valore stringa per questo parametro: `CONTENT_TYPE=application/xml&CONTENT_TYPE=application/pdf`
      * Un valore stringa che specifica il `HTTP_USER_AGENT` valore intestazione; ad esempio, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * A `RenderOptionsSpec` oggetto che memorizza le opzioni di runtime.

     Il `processFormSubmission` il metodo restituisce un `FormsResult` oggetto contenente i risultati dell’invio del modulo.

   * Verificare che lo stato di elaborazione associato a un modulo inviato sia `1` richiamando il `FormsResult` dell&#39;oggetto `getAction` metodo. Se questo metodo restituisce il valore `1`, il calcolo è stato eseguito e i dati possono essere scritti nuovamente sul browser web client.

1. Riscrivere il flusso di dati del modulo nel browser Web client

   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per inviare un flusso di dati modulo al browser web client.
   * Creare un `com.adobe.idp.Document` oggetto richiamando il `FormsResult` oggetto &quot;s `getOutputContent` metodo.
   * Creare un `java.io.InputStream` oggetto richiamando il `com.adobe.idp.Document` dell&#39;oggetto `getInputStream` metodo.
   * Creare una matrice di byte e popolarla con il flusso di dati del modulo richiamando `InputStream` dell&#39;oggetto `read` e passando la matrice di byte come argomento.
   * Richiama `javax.servlet.ServletOutputStream` dell&#39;oggetto `write` metodo per inviare il flusso di dati del modulo al browser web client. Passare la matrice di byte al `write` metodo.

**Consulta anche**


[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Calcolare i dati del modulo utilizzando l’API del servizio web {#calculate-form-data-using-the-web-service-api}

Calcola i dati del modulo utilizzando l’API di Forms (servizio web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio Forms WSDL.
   * Includi le classi proxy Java nel percorso della classe.

1. Creare un oggetto API client di Forms

   Creare un `FormsService` e impostare i valori di autenticazione.

1. Recuperare un modulo contenente uno script di calcolo

   * Per recuperare i dati del modulo inviati a un servlet Java, crea un `BLOB` mediante il costruttore.
   * Creare un `java.io.InputStream` oggetto utilizzando `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getInputStream` metodo.
   * Creare un `java.io.ByteArrayOutputStream` dell&#39;oggetto utilizzando il relativo costruttore e passando la lunghezza del `java.io.InputStream` oggetto.
   * Copia il contenuto del `java.io.InputStream` oggetto in `java.io.ByteArrayOutputStream` oggetto.
   * Creare una matrice di byte richiamando `java.io.ByteArrayOutputStream` dell&#39;oggetto `toByteArray` metodo.
   * Popolare il `BLOB` oggetto richiamando il relativo `setBinaryData` e passando la matrice di byte come argomento.
   * Creare un `RenderOptionsSpec` mediante il costruttore. Impostare il valore locale richiamando `RenderOptionsSpec` dell&#39;oggetto `setLocale` e passando un valore stringa che specifica il valore locale.
   * Richiama `FormsServiceClient` dell&#39;oggetto `processFormSubmission` e trasmettere i seguenti valori:

      * Il `BLOB` oggetto che contiene i dati del modulo.
      * Valore stringa che specifica che le variabili di ambiente includono tutte le intestazioni HTTP pertinenti. Ad esempio, puoi specificare il seguente valore stringa: `HTTP_REFERER=referrer&HTTP_CONNECTION=keep-alive&CONTENT_TYPE=application/xml`
      * Un valore stringa che specifica il `HTTP_USER_AGENT` valore intestazione; ad esempio, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * A `RenderOptionsSpec` oggetto che memorizza le opzioni di runtime. Per ulteriori informazioni, .
      * Un campo vuoto `BLOBHolder` oggetto popolato dal metodo.
      * Un campo vuoto `javax.xml.rpc.holders.StringHolder` oggetto popolato dal metodo.
      * Un campo vuoto `BLOBHolder` oggetto popolato dal metodo.
      * Un campo vuoto `BLOBHolder` oggetto popolato dal metodo.
      * Un campo vuoto `javax.xml.rpc.holders.ShortHolder` oggetto popolato dal metodo.
      * Un campo vuoto `MyArrayOf_xsd_anyTypeHolder` oggetto popolato dal metodo. Questo parametro viene utilizzato per memorizzare gli allegati dei file inviati insieme al modulo.
      * Un campo vuoto `FormsResultHolder` oggetto popolato dal metodo con il modulo inviato.

     Il `processFormSubmission` il metodo compila `FormsResultHolder` con i risultati dell&#39;invio del modulo. Il `processFormSubmission` il metodo restituisce un `FormsResult` oggetto contenente i risultati dell’invio del modulo.

   * Verificare che lo stato di elaborazione associato a un modulo inviato sia `1` richiamando il `FormsResult` dell&#39;oggetto `getAction` metodo. Se questo metodo restituisce il valore `1`, il calcolo è stato eseguito e i dati possono essere scritti nuovamente sul browser web client.

1. Riscrivere il flusso di dati del modulo nel browser Web client

   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per inviare un flusso di dati modulo al browser web client.
   * Creare un `BLOB` oggetto che contiene i dati del modulo richiamando `FormsResult` dell&#39;oggetto `getOutputContent` metodo.
   * Creare una matrice di byte e popolarla richiamando il `BLOB` dell&#39;oggetto `getBinaryData` metodo. Questa attività assegna il contenuto del `FormsResult` alla matrice di byte.
   * Richiama `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `write` metodo per inviare il flusso di dati del modulo al browser web client. Passare la matrice di byte al `write` metodo.

**Vedi anche**
[Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
