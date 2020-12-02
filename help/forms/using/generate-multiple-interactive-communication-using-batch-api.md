---
title: Utilizzare l'API Batch per generare più comunicazioni interattive
description: Utilizzare l'API Batch per generare più comunicazioni interattive
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communication
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2237'
ht-degree: 1%

---


# Generazione di più comunicazioni interattive mediante l&#39;API Batch {#use-batch-api-to-generate-multiple-ic}

Potete utilizzare l&#39;API Batch per produrre più comunicazioni interattive da un modello. Il modello è una comunicazione interattiva senza alcun dato. L&#39;API Batch combina i dati con un modello per produrre una comunicazione interattiva. L&#39;API è utile nella produzione di massa di comunicazioni interattive. Ad esempio, bollette telefoniche, estratti conto della carta di credito per più clienti.

L&#39;API Batch accetta i record (dati) in formato JSON e da un modello dati modulo. Il numero di comunicazioni interattive prodotte è uguale ai record specificati nel file JSON di input nel modello dati modulo configurato. Potete utilizzare l&#39;API per produrre sia output di stampa che output Web. L&#39;opzione STAMPA produce un documento PDF e l&#39;opzione WEB produce dati in formato JSON per ciascun record.

## Utilizzo dell&#39;API Batch {#using-the-batch-api}

Potete utilizzare l&#39;API Batch insieme alle cartelle esaminate o come API di riposo standalone. Potete configurare un modello, un tipo di output (HTML, PRINT o Entrambi), impostazioni internazionali, un servizio di precompilazione e un nome per le comunicazioni interattive generate per l&#39;utilizzo dell&#39;API Batch.

È possibile combinare un record con un modello di comunicazione interattiva per produrre una comunicazione interattiva. Le API Batch possono leggere i record (dati per i modelli di comunicazione interattivi) direttamente da un file JSON o da un&#39;origine dati esterna a cui si accede tramite il modello dati del modulo. È possibile conservare ciascun record in un file JSON separato o creare un array JSON per conservare tutti i record in un unico file.

**Un singolo record in un file JSON**

```json
{
   "employee": {
       "name": "Sara",
       "id": 3,
       "mobileNo": 9871996463,
       "age": 37
   }
}
```

**Più record in un file JSON**

```json
[{
   "employee": {
       "name": "John",
       "id": 1,
       "mobileNo": 9871996461,
       "age": 39
   }
},{
   "employee": {
       "name": "Jacob",
       "id": 2,
       "mobileNo": 9871996462,
       "age": 38
   }
},{
   "employee": {
       "name": "Sara",
       "id": 3,
       "mobileNo": 9871996463,
       "age": 37
   }
}]
```

### Utilizzo dell&#39;API Batch con le cartelle esaminate {#using-the-batch-api-watched-folders}

Per semplificare l&#39;utilizzo dell&#39;API,  AEM Forms fornisce un servizio Cartella esaminata configurato per l&#39;utilizzo dell&#39;API Batch, out-of-box. Potete accedere al servizio tramite &#39;interfaccia utente di AEM Forms per generare più comunicazioni interattive. Potete anche creare servizi personalizzati in base alle vostre esigenze. Potete utilizzare i metodi elencati di seguito per utilizzare l&#39;API Batch con la cartella esaminata:

* Specificare i dati di input (record) in formato JSON per produrre una comunicazione interattiva
* Utilizzare i dati di input (record) salvati in un&#39;origine dati esterna ed accessibili tramite un modello dati modulo per produrre una comunicazione interattiva

#### Specificare i record di dati di input nel formato di file JSON per produrre una comunicazione interattiva {#specify-input-data-in-JSON-file-format}

È possibile combinare un record con un modello di comunicazione interattiva per produrre una comunicazione interattiva. Potete creare un file JSON separato per ciascun record o creare un array JSON per conservare tutti i record in un unico file:

Per creare una comunicazione interattiva dai record salvati in un file JSON:

1. Create una [cartella esaminata](https://docs.adobe.com/content/help/en/experience-manager-64/forms/publish-process-aem-forms/creating-configure-watched-folder.html) e configuratela per utilizzare l&#39;API Batch:
   1. Accedete ’istanza di creazione AEM Forms.
   1. Passare a **[!UICONTROL Strumenti]** > **[!UICONTROL Forms]** > **[!UICONTROL Configura cartella esaminata]**. Toccate **[!UICONTROL Nuovo]**.
   1. Specificare il **[!UICONTROL Nome]** e il percorso **[!UICONTROL fisico]** della cartella. Esempio, `c:\batchprocessing`.
   1. Selezionare l&#39;opzione **[!UICONTROL Service]** nel campo **[!UICONTROL Process File Using]**.
   1. Selezionare il servizio **[!UICONTROL com.adobe.fd.ccm.multicanale.batch.impl.service.InteractiveCommunicationBatchServiceImpl]** nel campo **[!UICONTROL Nome servizio]**.
   1. Specificare un **[!UICONTROL Pattern file di output]**. Ad esempio, il %F/ [pattern](https://helpx.adobe.com/experience-manager/6-5/forms/using/admin-help/configuring-watched-folder-endpoints.html#about_file_patterns) specifica che la cartella esaminata può trovare i file di input in una sottocartella della cartella Watched Folder\input.
1. Configurare i parametri avanzati:
   1. Aprite la scheda **[!UICONTROL Avanzate]** e aggiungete le seguenti proprietà personalizzate:

      | Proprietà | Tipo | Descrizione |
      |--- |--- |--- |
      | templatePath | Stringa | Specificate il percorso del modello di comunicazione interattiva da utilizzare. Ad esempio, /content/dam/formsanddocuments/testsample/mediumic. È una proprietà obbligatoria. |
      | recordPath | Stringa | Il valore del campo recordPath consente di impostare il nome di una comunicazione interattiva. È possibile impostare il percorso di un campo di un record come valore del campo recordPath. Ad esempio, se specificate /dipendente/Id, il valore del campo id diventa nome per la corrispondente comunicazione interattiva. Il valore predefinito è un UUID casuale [casuale](https://docs.oracle.com/javase/7/docs/api/java/util/UUID.html#randomUUID()). |
      | usePrefillService | Booleano | Impostare il valore su False. Potete utilizzare il parametro usePrefillService per precompilare la comunicazione interattiva con i dati recuperati dal servizio di precompilazione configurato per la comunicazione interattiva corrispondente. Quando usePrefillService è impostato su true, i dati JSON di input (per ciascun record) vengono trattati come argomenti FDM. Il valore predefinito è false. |
      | batchType | Stringa | Impostare il valore su STAMPA, WEB o WEB_AND_PRINT. Il valore predefinito è WEB_AND_PRINT. |
      | locale | Stringa | Specificate le impostazioni internazionali della comunicazione interattiva di output. Il servizio out-of-the-box non utilizza l&#39;opzione delle impostazioni internazionali, ma è possibile creare un servizio personalizzato per generare comunicazioni interattive localizzate. Il valore predefinito è en_US |

   1. Toccate **[!UICONTROL Crea]** La cartella esaminata viene creata.
1. Utilizzate la cartella esaminata per generare comunicazioni interattive:
   1. Aprite la cartella esaminata. Passate alla cartella di input.
   1. Create una cartella nella cartella di input e inserite il file JSON nella nuova cartella creata.
   1. Attendete che la cartella esaminata elabori il file. All&#39;avvio dell&#39;elaborazione, il file di input e la sottocartella contenente il file vengono spostati nella cartella di gestione temporanea.
   1. Aprite la cartella di output per visualizzare l’output:
      * Quando si specifica l&#39;opzione PRINT in Configurazione cartelle esaminate, viene generato l&#39;output PDF per la comunicazione interattiva.
      * Quando specificate l&#39;opzione WEB in Configurazione cartelle esaminate, viene generato un file JSON per record. Potete utilizzare il file JSON per [precompilare un modello Web](#web-template).
      * Quando si specificano sia le opzioni STAMPA che WEB, vengono generati sia i documenti PDF che un file JSON per record.

#### Utilizzare i dati di input salvati in un&#39;origine dati esterna e accessibili tramite il modello dati del modulo per produrre una comunicazione interattiva {#use-fdm-as-data-source}

È possibile combinare i dati (record) salvati in un&#39;origine dati esterna con un modello di comunicazione interattiva per produrre una comunicazione interattiva. Quando si crea una comunicazione interattiva, è possibile collegarla a un&#39;origine dati esterna tramite un modello dati modulo (FDM) per accedere ai dati. È possibile configurare il servizio di elaborazione batch Cartelle esaminate per recuperare i dati utilizzando lo stesso modello dati modulo da un&#39;origine dati esterna. Per [creare una comunicazione interattiva dai record salvati in un&#39;origine dati esterna](https://docs.adobe.com/content/help/en/experience-manager-64/forms/form-data-model/work-with-form-data-model.html):

1. Configurare il modello dati modulo del modello:
   1. Aprire il modello dati modulo associato al modello di comunicazione interattiva.
   1. Selezionare l&#39;OGGETTO MODELLO DI LIVELLO SUPERIORE e toccare Modifica proprietà.
   1. Selezionare il recupero o ottenere il servizio dal campo Servizio lettura nel riquadro Modifica proprietà.
   1. Toccate l&#39;icona a forma di matita per l&#39;argomento del servizio di lettura per associare l&#39;argomento a un attributo di richiesta e specificare il valore di binding. Questo vincola l&#39;argomento del servizio all&#39;attributo di binding o al valore letterale specificato, che viene passato al servizio come argomento per recuperare i dettagli associati al valore specificato dall&#39;origine dati.

      <br>
        In questo esempio, l'argomento id prende il valore dell'attributo id del profilo utente e lo trasmette come argomento al servizio di lettura. Leggerà e restituirà i valori delle proprietà associate dall'oggetto modello dati dipendente per l'ID specificato. Pertanto, se si specifica 00250 nel campo id del modulo, il servizio di lettura leggerà i dettagli del dipendente con ID dipendente 00250.
        <br>

      ![Configura attributo richiesta](assets/request-attribute.png)

   1. Salvare le proprietà e il modello dati modulo.
1. Configura valore per attributo richiesta:
   1. Create un file .json sul file system e apritelo per la modifica.
   1. Create un array JSON e specificate l&#39;attributo principale per recuperare i dati dal modello dati del modulo. Ad esempio, il seguente JSON richiede a FDM di inviare dati di record dove id è 27126 o 27127:

      ```json
          [
              {
                  "id": 27126
              },
              {
                  "id": 27127
              }
          ]
      ```

   1. Salvate e chiudete il file.

1. Create una [cartella esaminata](https://docs.adobe.com/content/help/en/experience-manager-64/forms/publish-process-aem-forms/creating-configure-watched-folder.html) e configuratela per utilizzare il servizio API Batch:
   1. Accedete ’istanza di creazione AEM Forms.
   1. Passare a **[!UICONTROL Strumenti]** > **[!UICONTROL Forms]** > **[!UICONTROL Configura cartella esaminata]**. Toccate **[!UICONTROL Nuovo]**.
   1. Specificare il **[!UICONTROL Nome]** e il percorso **[!UICONTROL fisico]** della cartella. Esempio, `c:\batchprocessing`.
   1. Selezionare l&#39;opzione **[!UICONTROL Service]** nel campo **[!UICONTROL Process File Using]**.
   1. Selezionare il servizio **[!UICONTROL com.adobe.fd.ccm.multicanale.batch.impl.service.InteractiveCommunicationBatchServiceImpl]** nel campo **[!UICONTROL Nome servizio]**.
   1. Specificare un **[!UICONTROL Pattern file di output]**. Ad esempio, il %F/ [pattern](https://helpx.adobe.com/experience-manager/6-5/forms/using/admin-help/configuring-watched-folder-endpoints.html#about_file_patterns) specifica che la cartella esaminata può trovare i file di input in una sottocartella della cartella Watched Folder\input.
1. Configurare i parametri avanzati:
   1. Aprite la scheda **[!UICONTROL Avanzate]** e aggiungete le seguenti proprietà personalizzate:

      | Proprietà | Tipo | Descrizione |
      |--- |--- |--- |
      | templatePath | Stringa | Specificate il percorso del modello di comunicazione interattiva da utilizzare. Ad esempio, /content/dam/formsanddocuments/testsample/mediumic. È una proprietà obbligatoria. |
      | recordPath | Stringa | Il valore del campo recordPath consente di impostare il nome di una comunicazione interattiva. È possibile impostare il percorso di un campo di un record come valore del campo recordPath. Ad esempio, se specificate /dipendente/Id, il valore del campo id diventa nome per la corrispondente comunicazione interattiva. Il valore predefinito è un UUID casuale [casuale](https://docs.oracle.com/javase/7/docs/api/java/util/UUID.html#randomUUID()). |  |
      | usePrefillService | Booleano | Impostate il valore su True. Il valore predefinito è false.  Quando il valore è impostato su true, l&#39;API Batch legge i dati dal modello dati modulo configurato e li riempie alla comunicazione interattiva. Quando usePrefillService è impostato su true, i dati JSON di input (per ciascun record) vengono trattati come argomenti FDM. |
      | batchType | Stringa | Impostare il valore su STAMPA, WEB o WEB_AND_PRINT. Il valore predefinito è WEB_AND_PRINT. |
      | locale | Stringa | Specificate le impostazioni internazionali della comunicazione interattiva di output. Il servizio out-of-the-box non utilizza l&#39;opzione delle impostazioni internazionali, ma è possibile creare un servizio personalizzato per generare comunicazioni interattive localizzate. Il valore predefinito è en_US. |

   1. Toccate **[!UICONTROL Crea]** La cartella esaminata viene creata.
1. Utilizzate la cartella esaminata per generare comunicazioni interattive:
   1. Aprite la cartella esaminata. Passate alla cartella di input.
   1. Create una cartella nella cartella di input. Inserite il file JSON creato al punto 2 nella nuova cartella creata.
   1. Attendete che la cartella esaminata elabori il file. All&#39;avvio dell&#39;elaborazione, il file di input e la sottocartella contenente il file vengono spostati nella cartella di gestione temporanea.
   1. Aprite la cartella di output per visualizzare l’output:
      * Quando si specifica l&#39;opzione PRINT in Configurazione cartelle esaminate, viene generato l&#39;output PDF per la comunicazione interattiva.
      * Quando specificate l&#39;opzione WEB in Configurazione cartelle esaminate, viene generato un file JSON per record. Potete utilizzare il file JSON per [precompilare un modello Web](#web-template).
      * Quando si specificano sia le opzioni STAMPA che WEB, vengono generati sia i documenti PDF che un file JSON per record.

## Richiama l&#39;API Batch utilizzando le richieste REST

È possibile richiamare [l&#39;API Batch](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/index.html) tramite le richieste di trasferimento dello stato di rappresentanza (REST). Consente di fornire un endpoint REST ad altri utenti per accedere all&#39;API e configurare i propri metodi per l&#39;elaborazione, la memorizzazione e la personalizzazione delle comunicazioni interattive. Potete sviluppare un servlet Java personalizzato per distribuire l&#39;API nell&#39;istanza AEM.

Prima di distribuire il servlet Java, accertatevi di disporre di una comunicazione interattiva e che i file di dati corrispondenti siano pronti. Per creare e distribuire il servlet Java, effettuate le seguenti operazioni:

1. Accedete all&#39;istanza AEM e create una comunicazione interattiva. Per utilizzare la comunicazione interattiva indicata nel codice di esempio riportato di seguito, [fare clic qui](assets/SimpleMediumIC.zip).
1. [Create e implementate un progetto AEM utilizzando l&#39;istanza di AEM Apache ](https://helpx.adobe.com/experience-manager/using/maven_arch13.html) Mavenon.
1. Aggiungi [ AEM Forms Client SDK versione 6.0.12](https://repo.adobe.com/nexus/content/repositories/public/com/adobe/aemfd/aemfd-client-sdk/) o successiva nell&#39;elenco delle dipendenze del file POM del progetto AEM. Esempio,

   ```xml
       <dependency>
           <groupId>com.adobe.aemfd</groupId>
           <artifactId>aemfd-client-sdk</artifactId>
           <version>6.0.122</version>
       </dependency>
   ```

1. Aprite il progetto Java, create un file .java, ad esempio CCMBatchServlet.java. Aggiungi al file il codice seguente:

   ```java
           package com.adobe.fd.ccm.multichannel.batch.integration;
   
           import java.io.File;
           import java.io.FileInputStream;
           import java.io.FileOutputStream;
           import java.io.IOException;
           import java.io.InputStream;
           import java.io.PrintWriter;
           import java.util.List;
           import javax.servlet.Servlet;
           import org.apache.commons.io.IOUtils;
           import org.apache.sling.api.SlingHttpServletRequest;
           import org.apache.sling.api.SlingHttpServletResponse;
           import org.apache.sling.api.servlets.SlingAllMethodsServlet;
           import org.json.JSONArray;
           import org.json.JSONObject;
           import org.osgi.service.component.annotations.Component;
           import org.osgi.service.component.annotations.Reference;
   
           import com.adobe.fd.ccm.multichannel.batch.api.builder.BatchConfigBuilder;
           import com.adobe.fd.ccm.multichannel.batch.api.factory.BatchComponentBuilderFactory;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchConfig;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchInput;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchResult;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchType;
           import com.adobe.fd.ccm.multichannel.batch.api.model.RecordResult;
           import com.adobe.fd.ccm.multichannel.batch.api.model.RenditionResult;
           import com.adobe.fd.ccm.multichannel.batch.api.service.BatchGeneratorService;
           import com.adobe.fd.ccm.multichannel.batch.util.BatchConstants;
           import java.util.Date;
   
   
           @Component(service=Servlet.class,
           property={
                   "sling.servlet.methods=GET",
                   "sling.servlet.paths="+ "/bin/batchServlet"
           })
           public class CCMBatchServlet extends SlingAllMethodsServlet {
   
               @Reference
               private BatchGeneratorService batchGeneratorService;
               @Reference
               private BatchComponentBuilderFactory batchBuilderFactory;
               public void doGet(SlingHttpServletRequest req, SlingHttpServletResponse resp) {
                   try {
                       executeBatch(req,resp);
                   } catch (Exception e) {
                       e.printStackTrace();
                   }
               }
               private void executeBatch(SlingHttpServletRequest req, SlingHttpServletResponse resp) throws Exception {
                   int count = 0;
                   JSONArray inputJSONArray = new JSONArray();
                   String filePath = req.getParameter("filePath");
                   InputStream is = new FileInputStream(filePath);
                   String data = IOUtils.toString(is);
                   try {
                       // If input file is json object, then create json object and add in json array, if not then try for json array
                       JSONObject inputJSON = new JSONObject(data);
                       inputJSONArray.put(inputJSON);
                   } catch (Exception e) {
                       try {
                           // If input file is json array, then iterate and add all objects into inputJsonArray otherwise throw exception
                           JSONArray inputArray = new JSONArray(data);
                           for(int i=0;i<inputArray.length();i++) {
                               inputJSONArray.put(inputArray.getJSONObject(i));
                           }
                       } catch (Exception ex) {
                           throw new Exception("Invalid JSON Data. File name : " + filePath, ex);
                       }
                   }
                   BatchInput batchInput = batchBuilderFactory.getBatchInputBuilder().setData(inputJSONArray).setTemplatePath("/content/dam/formsanddocuments/[path of the interactive communcation]").build();
                   BatchConfig batchConfig = batchBuilderFactory.getBatchConfigBuilder().setBatchType(BatchType.WEB_AND_PRINT).build();
                   BatchResult batchResult = batchGeneratorService.generateBatch(batchInput, batchConfig);
                   List<RecordResult> recordList = batchResult.getRecordResults();
                   JSONObject result = new JSONObject();
                   for (RecordResult recordResult : recordList) {
                       String recordId = recordResult.getRecordID();
                       for (RenditionResult renditionResult : recordResult.getRenditionResults()) {
                           if (renditionResult.isRecordPassed()) {
                               InputStream output = renditionResult.getDocumentStream().getInputStream();
                               result.put(recordId +"_"+renditionResult.getContentType(), output);
   
                               Date date= new Date();
                               long time = date.getTime();
   
                               // Print output
                               if(getFileExtension(renditionResult.getContentType()).equalsIgnoreCase(".json")) {
                                   File file = new File(time + getFileExtension(renditionResult.getContentType()));
                                   copyInputStreamToFile(output, file);
                               } else
                               {
                                   File file = new File(time + getFileExtension(renditionResult.getContentType()));
                                   copyInputStreamToFile(output, file);
                               }
                           }
                       }
                   }
                   PrintWriter writer = resp.getWriter();
                   JSONObject resultObj = new JSONObject();
                   resultObj.put("result", result);
                   writer.write(resultObj.toString());
               }
   
   
               private static void copyInputStreamToFile(InputStream inputStream, File file)
                       throws IOException {
   
                       try (FileOutputStream outputStream = new FileOutputStream(file)) {
   
                           int read;
                           byte[] bytes = new byte[1024];
   
                           while ((read = inputStream.read(bytes)) != -1) {
                               outputStream.write(bytes, 0, read);
                           }
   
                       }
   
                   }
   
   
               private String getFileExtension(String contentType) {
                   if (contentType.endsWith(BatchConstants.JSON)) {
                       return ".json";
                   } else return ".pdf";
               }
   
   
           }
   ```

1. Nel codice precedente, sostituisci il percorso del modello (setTemplatePath) con il percorso del modello e imposta il valore dell’API setBatchType:
   * Quando si specifica l&#39;opzione PRINT, viene generato l&#39;output PDF per la comunicazione interattiva.
   * Quando specificate l&#39;opzione WEB, viene generato un file JSON per record. Potete utilizzare il file JSON per [precompilare un modello Web](#web-template).
   * Quando si specificano sia le opzioni STAMPA che WEB, vengono generati sia i documenti PDF che un file JSON per record.

1. [Utilizzate maven per distribuire il codice aggiornato all&#39;istanza](https://helpx.adobe.com/experience-manager/using/maven_arch13.html#BuildtheOSGibundleusingMaven) AEM.
1. Richiamate l&#39;API batch per generare la comunicazione interattiva. L&#39;API batch consente di stampare un flusso di file PDF e .json in base al numero di record. Potete utilizzare il file JSON per [precompilare un modello Web](#web-template). Se utilizzate il codice riportato sopra, l&#39;API viene distribuita in `http://localhost:4502/bin/batchServlet`. Il codice stampa e restituisce un flusso di file PDF e JSON.

### Pre-compilare un modello Web {#web-template}

Quando impostate batchType per eseguire il rendering del canale Web, l&#39;API genera un file JSON per ogni record di dati. Per unire il file JSON con il canale Web corrispondente, potete usare la sintassi seguente per generare una comunicazione interattiva:

**Sintassi**
`http://host:port/<template-path>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=<guide-merged-json-path>`

****
Esempio: se il file JSON si trova in corrispondenza  `C:\batch\mergedJsonPath.json` e utilizzate il seguente modello di comunicazione interattiva:  `http://host:port/content/dam/formsanddocuments/testsample/mediumic/jcr:content?channel=web`

Quindi, il seguente URL sul nodo di pubblicazione visualizza il canale Web della comunicazione interattiva
`http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=file:///C:/batch/mergedJsonData.json`

Oltre a salvare i dati sul file system, si memorizzano i file JSON nel repository CRX, nel file system, nel server Web o possono accedere ai dati tramite il servizio di precompilazione OSGI. Sintassi per l&#39;unione dei dati tramite vari protocolli:

* **Protocollo CRX**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=crx:///tmp/fd/af/mergedJsonData.json`

* **Protocollo file**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=file:///C:/Users/af/mergedJsonData.json`

* **Protocollo Prefill Service**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=service://[SERVICE_NAME]/[IDENTIFIER]`

   SERVICE_NAME fa riferimento al nome del servizio di precompilazione OSGI. Fate riferimento a Creare ed eseguire un servizio di precompilazione.

   IDENTIFIER fa riferimento a tutti i metadati richiesti dal servizio di precompilazione OSGI per recuperare i dati di precompilazione. Un identificatore per l’utente connesso è un esempio di metadati che possono essere utilizzati.

* **protocollo HTTP**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=http://localhost:8000/somesamplexmlfile.xml`

>[!NOTE]
>
>Solo il protocollo CRX è abilitato per impostazione predefinita. Per abilitare altri protocolli supportati, vedere [Configurazione del servizio di precompilazione tramite Configuration Manager](https://helpx.adobe.com/experience-manager/6-5/forms/using/prepopulate-adaptive-form-fields.html#ConfiguringprefillserviceusingConfigurationManager).
