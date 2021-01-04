---
title: Calcolo dei dati del modulo
seo-title: Calcolo dei dati del modulo
description: Utilizzare il servizio Forms per calcolare i valori immessi dall'utente in un modulo e visualizzare i risultati. Il servizio Forms calcola i valori utilizzando l'API Java e l'API del servizio Web.
seo-description: Utilizzare il servizio Forms per calcolare i valori immessi dall'utente in un modulo e visualizzare i risultati. Il servizio Forms calcola i valori utilizzando l'API Java e l'API del servizio Web.
uuid: ccd85bc7-8ccc-44d9-9424-dfc1f603e688
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: b4f57e42-60a6-407d-9764-15a11615827d
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '1902'
ht-degree: 0%

---


# Calcolo dei dati del modulo {#calculating-form-data}

Il servizio Forms può calcolare i valori immessi dall&#39;utente in un modulo e visualizzare i risultati. Per calcolare i dati del modulo, è necessario eseguire due operazioni. Innanzitutto, si crea uno script della struttura del modulo che calcola i dati del modulo. Una struttura del modulo supporta tre tipi di script. Un tipo di script viene eseguito sul client, un altro sul server e il terzo tipo viene eseguito sia sul server che sul client. Il tipo di script descritto in questo argomento viene eseguito sul server. I calcoli sul lato server sono supportati per le trasformazioni HTML, PDF e della guida ai moduli (obsoleto).

Durante il processo di progettazione del modulo è possibile utilizzare calcoli e script per migliorare l&#39;esperienza dell&#39;utente. I calcoli e gli script possono essere aggiunti alla maggior parte dei campi e degli oggetti modulo. È necessario creare uno script della struttura del modulo per eseguire operazioni di calcolo sui dati immessi dall&#39;utente in un modulo interattivo.

L&#39;utente immette dei valori nel modulo e fa clic sul pulsante Calcola per visualizzare i risultati. Il seguente processo descrive un&#39;applicazione di esempio che consente a un utente di calcolare i dati:

* L&#39;utente accede a una pagina HTML denominata StartLoan.html che funge da pagina iniziale dell&#39;applicazione Web. Questa pagina richiama un servlet Java denominato `GetLoanForm`.
* Il servlet `GetLoanForm` esegue il rendering di un modulo di prestito. Questo modulo contiene uno script, campi interattivi, un pulsante di calcolo e un pulsante di invio.
* L&#39;utente immette valori nei campi del modulo e fa clic sul pulsante Calcola. Il modulo viene inviato al servlet Java `CalculateData` in cui viene eseguito lo script. Il modulo viene inviato all&#39;utente con i risultati di calcolo visualizzati nel modulo.
* L&#39;utente continua a immettere e calcolare i valori finché non viene visualizzato un risultato soddisfacente. Una volta soddisfatto, l&#39;utente fa clic sul pulsante Invia per elaborare il modulo. Il modulo viene inviato a un altro Servlet Java denominato `ProcessForm` responsabile del recupero dei dati inviati. (Vedere [Gestione di Forms](/help/forms/developing/rendering-forms.md#handling-submitted-forms) inviato.)


Il diagramma seguente mostra il flusso logico dell&#39;applicazione.

![cf_cf_finsrv_loancalcapp_v1](assets/cf_cf_finsrv_loancalcapp_v1.png)

La tabella seguente descrive i passaggi descritti in questo diagramma.

<table>
 <thead>
  <tr>
   <th><p>Incremento</p></th>
   <th><p>Descrizione</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>Il servlet Java <code>GetLoanForm</code> viene richiamato dalla pagina iniziale HTML. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Il servlet <code>GetLoanForm</code> Java utilizza l'API client del servizio Forms per eseguire il rendering del modulo di prestito nel browser Web del client. La differenza tra il rendering di un modulo che contiene uno script configurato per l'esecuzione sul server e il rendering di un modulo che non contiene uno script sta nel fatto che è necessario specificare il percorso di destinazione utilizzato per eseguire lo script. Se non viene specificata una posizione di destinazione, non viene eseguito uno script configurato per l'esecuzione sul server. Ad esempio, considerare l'applicazione introdotta in questa sezione. Il servlet Java <code>CalculateData</code> è il percorso di destinazione in cui viene eseguito lo script.</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>L'utente immette i dati in campi interattivi e fa clic sul pulsante Calcola. Il modulo viene inviato al servlet Java <code>CalculateData</code> in cui viene eseguito lo script. </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Il modulo viene riprodotto nel browser Web con i risultati dei calcoli visualizzati nel modulo. </p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>Quando i valori sono soddisfacenti, l'utente fa clic sul pulsante Invia. Il modulo viene inviato a un altro servlet Java denominato <code>ProcessForm</code>.</p></td>
  </tr>
 </tbody>
</table>

In genere, un modulo inviato come contenuto PDF contiene script eseguiti sul client. È tuttavia possibile eseguire anche calcoli sul lato server. Non è possibile utilizzare un pulsante Invia per calcolare gli script. In questa situazione, i calcoli non vengono eseguiti perché il servizio Forms ritiene che l&#39;interazione sia completa.

Per illustrare l&#39;uso di uno script della struttura del modulo, in questa sezione viene esaminato un semplice modulo interattivo contenente uno script configurato per l&#39;esecuzione sul server. Il diagramma seguente mostra una struttura del modulo contenente uno script che aggiunge valori immessi dall&#39;utente nei primi due campi e visualizza il risultato nel terzo campo.

![cf_cf_caldata](assets/cf_cf_caldata.png)

**A.** Un campo denominato NumericField1  **B.** A campo denominato NumericField2  **C.** A campo denominato NumericField3

La sintassi dello script in questa struttura del modulo è la seguente:

```javascript
     NumericField3 = NumericField2 + NumericField1
```

In questa struttura del modulo, il pulsante Calcola è un pulsante di comando e lo script si trova nell&#39;evento `Click` del pulsante. Quando un utente immette valori nei primi due campi (NumericField1 e NumericField2) e fa clic sul pulsante Calcola, il modulo viene inviato al servizio Forms, dove viene eseguito lo script. Il servizio Forms esegue il rendering del modulo sul dispositivo client con i risultati del calcolo visualizzato nel campo NumericField3.

>[!NOTE]
>
>Per informazioni sulla creazione di uno script per la struttura del modulo, vedere [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

>[!NOTE]
>
>Per ulteriori informazioni sul servizio Forms, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Riepilogo dei passaggi {#summary-of-steps}

Per calcolare i dati del modulo, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto Forms Client API.
1. Recuperare un modulo contenente uno script di calcolo.
1. Reinserire il flusso di dati del modulo nel browser Web del client

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, accertatevi di includere i file proxy.

**Creare un oggetto Forms Client API**

Prima di eseguire un&#39;operazione API client di Forms Service a livello di programmazione, è necessario creare un client di servizi Forms. Se utilizzate l&#39;API Java, create un oggetto `FormsServiceClient`. Se utilizzate l&#39;API del servizio Web di Forms, create un oggetto `FormsServiceService`.

**Recuperare un modulo contenente uno script di calcolo**

È possibile utilizzare Forms Service Client API per creare una logica applicativa che gestisce un modulo contenente uno script configurato per l&#39;esecuzione sul server. Il processo è simile alla gestione di un modulo inviato. (Vedere [Gestione di Forms](/help/forms/developing/handling-submitted-forms.md) inviato.)

Verificare che lo stato di elaborazione associato al modulo inviato sia `1` `(Calculate)`, ovvero che il servizio Forms stia eseguendo un&#39;operazione di calcolo sui dati del modulo e che i risultati debbano essere riscritti all&#39;utente. In questa situazione, viene eseguito automaticamente uno script configurato per l&#39;esecuzione sul server.

**Reinserire il flusso di dati del modulo nel browser Web del client**

Dopo aver verificato che lo stato di elaborazione associato a un modulo inviato sia `1`, è necessario riscrivere i risultati nel browser Web del client. Quando il modulo viene visualizzato, il valore calcolato viene visualizzato nei campi appropriati.

**Consulta anche**

[Inclusione  ](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[file di libreria AEM Forms JavaCalcolare i dati del modulo utilizzando Java ](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-java-api)
[APICalculate i dati del modulo utilizzando il servizio Web ](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-web-service-api)
[APISetting connection ](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
[propertiesForms Service API Quick ](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)
[StartsRendering Interactive PDF ](/help/forms/developing/rendering-interactive-pdf-forms.md)
[FormsCreazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Calcola i dati del modulo utilizzando l&#39;API Java {#calculate-form-data-using-the-java-api}

Calcola i dati del modulo utilizzando l&#39;API Forms (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-forms-client.jar nel percorso di classe del progetto Java.

1. Creare un oggetto Forms Client API

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `FormsServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Recuperare un modulo contenente uno script di calcolo

   * Per recuperare i dati del modulo che contengono uno script di calcolo, creare un oggetto `com.adobe.idp.Document` utilizzando il relativo costruttore e richiamando il metodo `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getInputStream` dall&#39;interno del costruttore.
   * Richiamare il metodo `FormsServiceClient` dell&#39;oggetto `processFormSubmission` e trasmettere i seguenti valori:

      * L&#39;oggetto `com.adobe.idp.Document` che contiene i dati del modulo.
      * Valore stringa che specifica le variabili di ambiente, comprese tutte le intestazioni HTTP rilevanti. È necessario specificare il tipo di contenuto da gestire specificando uno o più valori per la variabile di ambiente `CONTENT_TYPE`. Ad esempio, per gestire i dati XML e PDF, specificare il seguente valore di stringa per questo parametro: `CONTENT_TYPE=application/xml&CONTENT_TYPE=application/pdf`
      * Un valore di stringa che specifica il valore di intestazione `HTTP_USER_AGENT`; ad esempio, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * Un oggetto `RenderOptionsSpec` che memorizza le opzioni di esecuzione.

      Il metodo `processFormSubmission` restituisce un oggetto `FormsResult` contenente i risultati dell&#39;invio del modulo.

   * Verificare che lo stato di elaborazione associato a un modulo inviato sia `1` richiamando il metodo `FormsResult` dell&#39;oggetto `getAction`. Se questo metodo restituisce il valore `1`, il calcolo è stato eseguito e i dati possono essere riscritti nel browser Web del client.


1. Reinserire il flusso di dati del modulo nel browser Web del client

   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per inviare un flusso di dati del modulo al browser Web del client.
   * Creare un oggetto `com.adobe.idp.Document` richiamando il metodo `FormsResult` object ‘s `getOutputContent`.
   * Creare un oggetto `java.io.InputStream` richiamando il metodo `com.adobe.idp.Document` dell&#39;oggetto `getInputStream`.
   * Creare un array di byte e compilarlo con il flusso di dati del modulo richiamando il metodo `InputStream` dell&#39;oggetto `read` e passando l&#39;array di byte come argomento.
   * Richiamare il metodo `javax.servlet.ServletOutputStream` dell&#39;oggetto `write` per inviare il flusso di dati del modulo al browser Web del client. Passate l&#39;array di byte al metodo `write`.

**Consulta anche**


[Inclusione  ](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[file libreria AEM Forms JavaImpostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Calcola i dati del modulo utilizzando l&#39;API del servizio Web {#calculate-form-data-using-the-web-service-api}

Calcola i dati del modulo utilizzando l&#39;API Forms (servizio Web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio WSDL di Forms.
   * Includete le classi proxy Java nel percorso della classe.

1. Creare un oggetto Forms Client API

   Creare un oggetto `FormsService` e impostare i valori di autenticazione.

1. Recuperare un modulo contenente uno script di calcolo

   * Per recuperare i dati del modulo inviati a un Servlet Java, creare un oggetto `BLOB` utilizzando il relativo costruttore.
   * Creare un oggetto `java.io.InputStream` utilizzando il metodo `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getInputStream`.
   * Creare un oggetto `java.io.ByteArrayOutputStream` utilizzando il relativo costruttore e passando la lunghezza dell&#39;oggetto `java.io.InputStream`.
   * Copiare il contenuto dell&#39;oggetto `java.io.InputStream` nell&#39;oggetto `java.io.ByteArrayOutputStream`.
   * Creare un array di byte richiamando il metodo `java.io.ByteArrayOutputStream` dell&#39;oggetto `toByteArray`.
   * Compilare l&#39;oggetto `BLOB` richiamandone il metodo `setBinaryData` e passando l&#39;array di byte come argomento.
   * Creare un oggetto `RenderOptionsSpec` utilizzando il relativo costruttore. Impostare il valore delle impostazioni internazionali richiamando il metodo `setLocale` dell&#39;oggetto `RenderOptionsSpec` e passando un valore di stringa che specifica il valore delle impostazioni internazionali.
   * Richiamare il metodo `FormsServiceClient` dell&#39;oggetto `processFormSubmission` e trasmettere i seguenti valori:

      * L&#39;oggetto `BLOB` che contiene i dati del modulo.
      * Un valore di stringa che specifica le variabili di ambiente includeva tutte le intestazioni HTTP rilevanti. Ad esempio, è possibile specificare il seguente valore di stringa: `HTTP_REFERER=referrer&HTTP_CONNECTION=keep-alive&CONTENT_TYPE=application/xml`
      * Un valore di stringa che specifica il valore di intestazione `HTTP_USER_AGENT`; ad esempio, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * Un oggetto `RenderOptionsSpec` che memorizza le opzioni di esecuzione. Per ulteriori informazioni, .
      * Un oggetto `BLOBHolder` vuoto compilato dal metodo.
      * Un oggetto `javax.xml.rpc.holders.StringHolder` vuoto compilato dal metodo.
      * Un oggetto `BLOBHolder` vuoto compilato dal metodo.
      * Un oggetto `BLOBHolder` vuoto compilato dal metodo.
      * Un oggetto `javax.xml.rpc.holders.ShortHolder` vuoto compilato dal metodo.
      * Un oggetto `MyArrayOf_xsd_anyTypeHolder` vuoto compilato dal metodo. Questo parametro viene utilizzato per memorizzare gli allegati inviati insieme al modulo.
      * Un oggetto `FormsResultHolder` vuoto compilato dal metodo con il modulo inviato.

      Il metodo `processFormSubmission` popola il parametro `FormsResultHolder` con i risultati dell&#39;invio del modulo. Il metodo `processFormSubmission` restituisce un oggetto `FormsResult` contenente i risultati dell&#39;invio del modulo.

   * Verificare che lo stato di elaborazione associato a un modulo inviato sia `1` richiamando il metodo `FormsResult` dell&#39;oggetto `getAction`. Se questo metodo restituisce il valore `1`, il calcolo è stato eseguito e i dati possono essere riscritti nel browser Web del client.


1. Reinserire il flusso di dati del modulo nel browser Web del client

   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per inviare un flusso di dati del modulo al browser Web del client.
   * Creare un oggetto `BLOB` contenente dati del modulo richiamando il metodo `FormsResult` dell&#39;oggetto `getOutputContent`.
   * Creare un array di byte e compilarlo richiamando il metodo `BLOB` dell&#39;oggetto `getBinaryData`. Questa attività assegna il contenuto dell&#39;oggetto `FormsResult` all&#39;array di byte.
   * Richiamare il metodo `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `write` per inviare il flusso di dati del modulo al browser Web del client. Passate l&#39;array di byte al metodo `write`.

**Vedere**
[ancheRichiamo  AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
