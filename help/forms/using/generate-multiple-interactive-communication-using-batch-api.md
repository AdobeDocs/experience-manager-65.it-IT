---
title: Utilizzare l’API Batch per generare più comunicazioni interattive
description: Utilizzare l’API Batch per generare più comunicazioni interattive
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communication
feature: Interactive Communication
exl-id: f65d8eb9-4d2c-4a6e-825f-45bcfaa7ca75
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2206'
ht-degree: 1%

---

# Generare più comunicazioni interattive utilizzando API Batch {#use-batch-api-to-generate-multiple-ic}

Puoi utilizzare l’API Batch per produrre più comunicazioni interattive da un modello. Il modello è una comunicazione interattiva senza alcun dato. L’API Batch combina i dati con un modello per produrre una comunicazione interattiva. L’API è utile nella produzione di massa di comunicazioni interattive. Ad esempio, bollette telefoniche, estratti conto delle carte di credito per più clienti.

L’API Batch accetta i record (dati) in formato JSON e da un modello di dati del modulo. Il numero di comunicazioni interattive prodotte è uguale ai record specificati nel file JSON di input nel Form Data Model configurato. Puoi utilizzare l’API per produrre sia l’output Stampa che quello Web. L&#39;opzione PRINT produce un documento PDF e l&#39;opzione WEB produce i dati in formato JSON per ogni singolo record.

## Utilizzo dell’API Batch {#using-the-batch-api}

Puoi utilizzare l’API Batch in combinazione con Cartelle controllate o come API REST indipendente. Puoi configurare un modello, un tipo di output (HTML, PRINT o Both), una lingua, un servizio di precompilazione e un nome per le comunicazioni interattive generate per utilizzare l’API Batch.

È possibile combinare un record con un modello di comunicazione interattiva per produrre una comunicazione interattiva. Le API batch possono leggere i record (dati per modelli di comunicazione interattivi) direttamente da un file JSON o da un’origine dati esterna accessibile tramite il modello dati del modulo. È possibile mantenere ogni record in un file JSON separato o creare un array JSON per mantenere tutti i record in un singolo file.

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

### Utilizzo dell’API Batch con le cartelle controllate {#using-the-batch-api-watched-folders}

Per semplificare l’esperienza dell’API, AEM Forms fornisce automaticamente un servizio Cartella controllata configurato per l’utilizzo dell’API Batch. Puoi accedere al servizio tramite l’interfaccia utente di AEM Forms per generare più comunicazioni interattive. Puoi anche creare servizi personalizzati in base alle tue esigenze. Per utilizzare l’API Batch con la cartella Watched, puoi utilizzare i metodi seguenti:

* Specifica i dati di input (record) in formato file JSON per produrre una comunicazione interattiva
* Utilizzare i dati di input (record) salvati in un&#39;origine dati esterna e a cui si accede tramite un modello dati del modulo per produrre una comunicazione interattiva

#### Specifica i record di dati di input in formato file JSON per produrre una comunicazione interattiva {#specify-input-data-in-JSON-file-format}

È possibile combinare un record con un modello di comunicazione interattiva per produrre una comunicazione interattiva. Puoi creare un file JSON separato per ogni record oppure un array JSON per mantenere tutti i record in un singolo file:

Per creare una comunicazione interattiva dai record salvati in un file JSON:

1. Creare un [Cartella controllata](/help/forms/using/creating-configure-watched-folder.md) e configuralo per utilizzare l’API Batch:
   1. Accedi all’istanza Autore AEM Forms.
   1. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Forms]** > **[!UICONTROL Configura cartella controllata]**. Tocca **[!UICONTROL Nuovo]**.
   1. Specifica la **[!UICONTROL Nome]** e fisica **[!UICONTROL Percorso]** della cartella. Esempio: `c:\batchprocessing`.
   1. Seleziona la **[!UICONTROL Servizio]** opzione in **[!UICONTROL Elabora file tramite]** campo.
   1. Seleziona la **[!UICONTROL com.adobe.fd.ccm.multichannel.batch.impl.service.InteractiveCommunicationBatchServiceImpl]** servizio in **[!UICONTROL Nome servizio]** campo.
   1. Specifica un **[!UICONTROL Pattern file di output]**. Ad esempio, %F/ [pattern](https://helpx.adobe.com/experience-manager/6-5/forms/using/admin-help/configuring-watched-folder-endpoints.html#about_file_patterns) specifica che la cartella controllata può trovare i file di input in una sottocartella della cartella controllata\input.
1. Configura parametri avanzati:
   1. Apri **[!UICONTROL Avanzate]** e aggiungi le seguenti proprietà personalizzate:

      | Proprietà | Tipo | Descrizione |
      |--- |--- |--- |
      | templatePath | Stringa | Specifica il percorso del modello di comunicazione interattiva da utilizzare. Ad esempio, /content/dam/formsanddocuments/testsample/media. È una proprietà obbligatoria. |
      | recordPath | Stringa | Il valore del campo recordPath consente di impostare il nome di una comunicazione interattiva. È possibile impostare il percorso di un campo di un record come valore del campo recordPath. Ad esempio, se specifichi /employee/Id, il valore del campo id diventa il nome della comunicazione interattiva corrispondente. Il valore predefinito è casuale [UUID casuale](https://docs.oracle.com/javase/7/docs/api/java/util/UUID.html#randomUUID()). |
      | usePrefillService | Booleano | Imposta il valore su False. Puoi utilizzare il parametro usePrefillService per precompilare la comunicazione interattiva con i dati recuperati dal servizio precompilato configurato per la comunicazione interattiva corrispondente. Quando usePrefillService è impostato su true, i dati JSON di input (per ogni record) vengono trattati come argomenti FDM. Il valore predefinito è false. |
      | batchType | Stringa | Impostate il valore su PRINT, WEB o WEB_AND_PRINT. Il valore predefinito è WEB_AND_PRINT. |
      | lingua | Stringa | Specifica le impostazioni locali della comunicazione interattiva di output. Il servizio preconfigurato non utilizza l’opzione internazionale, ma puoi creare un servizio personalizzato per generare comunicazioni interattive localizzate. Il valore predefinito è en_US |

   1. Tocca **[!UICONTROL Crea]** Viene creata la cartella controllata.
1. Utilizza la cartella controllata per generare la comunicazione interattiva:
   1. Apri la cartella controllata. Passare alla cartella di input.
   1. Crea una cartella nella cartella di input e inserisci il file JSON nella cartella appena creata.
   1. Attendi che la cartella controllata elabori il file. All&#39;avvio dell&#39;elaborazione, il file di input e la sottocartella contenente il file vengono spostati nella cartella di gestione temporanea.
   1. Apri la cartella di output per visualizzare l’output:
      * Quando specifichi l’opzione STAMPA in Configurazione cartella controllata, viene generato l’output PDF per la comunicazione interattiva.
      * Quando specifichi l’opzione WEB in Configurazione cartella controllata, viene generato un file JSON per record. Puoi utilizzare il file JSON per [precompilare un modello web](#web-template).
      * Quando si specificano le opzioni PRINT e WEB, vengono generati sia i documenti PDF che un file JSON per record.

#### Utilizzare i dati di input salvati in un&#39;origine dati esterna e a cui si accede tramite il modello dati del modulo per produrre una comunicazione interattiva {#use-fdm-as-data-source}

I dati (record) salvati in un&#39;origine dati esterna vengono combinati con un modello di comunicazione interattiva per produrre una comunicazione interattiva. Quando si crea una comunicazione interattiva, questa viene connessa a un&#39;origine dati esterna tramite un modello dati modulo (FDM) per accedere ai dati. Puoi configurare il servizio di elaborazione batch delle cartelle controllate per recuperare i dati utilizzando lo stesso modello dati del modulo da un’origine dati esterna. A [creare una comunicazione interattiva da record salvati in un&#39;origine dati esterna](/help/forms/using/work-with-form-data-model.md):

1. Configura il modello dati modulo del modello:
   1. Apri il modello dati modulo associato al modello di comunicazione interattiva.
   1. Seleziona l’OGGETTO MODELLO DI LIVELLO SUPERIORE e tocca Modifica proprietà.
   1. Seleziona Recupera o ottieni servizio dal campo Servizio di lettura nel riquadro Modifica proprietà.
   1. Tocca l’icona a forma di matita per l’argomento del servizio di lettura per associare l’argomento a un attributo di richiesta e specificare il valore di associazione. L&#39;argomento del servizio viene associato all&#39;attributo di associazione o al valore letterale specificato, che viene passato al servizio come argomento per recuperare i dettagli associati al valore specificato dall&#39;origine dati.

      <br>
        In questo esempio, l'argomento id prende il valore dell'attributo id del profilo utente e lo trasmette come argomento al servizio di lettura. Lettura e restituzione dei valori delle proprietà associate dall'oggetto modello dati dipendente per l'ID specificato. Pertanto, se si specifica 00250 nel campo ID del modulo, il servizio di lettura leggerà i dettagli del dipendente con 00250 ID dipendente.
        <br>

      ![Configurare l’attributo della richiesta](assets/request-attribute.png)

   1. Salva proprietà e modello dati modulo.
1. Configura valore per attributo richiesta:
   1. Crea un file .json sul file system e aprilo per la modifica.
   1. Crea un array JSON e specifica l’attributo principale per recuperare i dati dal modello dati del modulo. Ad esempio, il seguente JSON richiede a FDM di inviare dati di record in cui l’ID è 27126 o 27127:

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

   1. Salva e chiudi il file 

1. Creare un [Cartella controllata](/help/forms/using/creating-configure-watched-folder.md) e configuralo per utilizzare il servizio API Batch:
   1. Accedi all’istanza Autore AEM Forms.
   1. Accedi a **[!UICONTROL Strumenti]** > **[!UICONTROL Forms]** > **[!UICONTROL Configura cartella controllata]**. Tocca **[!UICONTROL Nuovo]**.
   1. Specifica la **[!UICONTROL Nome]** e fisica **[!UICONTROL Percorso]** della cartella. Esempio: `c:\batchprocessing`.
   1. Seleziona la **[!UICONTROL Servizio]** opzione in **[!UICONTROL Elabora file tramite]** campo.
   1. Seleziona la **[!UICONTROL com.adobe.fd.ccm.multichannel.batch.impl.service.InteractiveCommunicationBatchServiceImpl]** servizio in **[!UICONTROL Nome servizio]** campo.
   1. Specifica un **[!UICONTROL Pattern file di output]**. Ad esempio, %F/ [pattern](https://helpx.adobe.com/experience-manager/6-5/forms/using/admin-help/configuring-watched-folder-endpoints.html#about_file_patterns) specifica che la cartella controllata può trovare i file di input in una sottocartella della cartella controllata\input.
1. Configura parametri avanzati:
   1. Apri **[!UICONTROL Avanzate]** e aggiungi le seguenti proprietà personalizzate:

      | Proprietà | Tipo | Descrizione |
      |--- |--- |--- |
      | templatePath | Stringa | Specifica il percorso del modello di comunicazione interattiva da utilizzare. Ad esempio, /content/dam/formsanddocuments/testsample/media. È una proprietà obbligatoria. |
      | recordPath | Stringa | Il valore del campo recordPath consente di impostare il nome di una comunicazione interattiva. È possibile impostare il percorso di un campo di un record come valore del campo recordPath. Ad esempio, se specifichi /employee/Id, il valore del campo id diventa il nome della comunicazione interattiva corrispondente. Il valore predefinito è casuale [UUID casuale](https://docs.oracle.com/javase/7/docs/api/java/util/UUID.html#randomUUID()). |  |
      | usePrefillService | Booleano | Imposta il valore su True. Il valore predefinito è false.  Quando il valore è impostato su true, l’API Batch legge i dati dal modello dati del modulo configurato e li inserisce nella comunicazione interattiva. Quando usePrefillService è impostato su true, i dati JSON di input (per ogni record) vengono trattati come argomenti FDM. |
      | batchType | Stringa | Impostate il valore su PRINT, WEB o WEB_AND_PRINT. Il valore predefinito è WEB_AND_PRINT. |
      | lingua | Stringa | Specifica le impostazioni locali della comunicazione interattiva di output. Il servizio preconfigurato non utilizza l’opzione internazionale, ma puoi creare un servizio personalizzato per generare comunicazioni interattive localizzate. Il valore di default è en_US. |

   1. Tocca **[!UICONTROL Crea]** Viene creata la cartella controllata.
1. Utilizza la cartella controllata per generare la comunicazione interattiva:
   1. Apri la cartella controllata. Passare alla cartella di input.
   1. Crea una cartella nella cartella di input. Posiziona il file JSON creato al passaggio 2 nella cartella appena creata.
   1. Attendi che la cartella controllata elabori il file. All&#39;avvio dell&#39;elaborazione, il file di input e la sottocartella contenente il file vengono spostati nella cartella di gestione temporanea.
   1. Apri la cartella di output per visualizzare l’output:
      * Quando specifichi l’opzione STAMPA in Configurazione cartella controllata, viene generato l’output PDF per la comunicazione interattiva.
      * Quando specifichi l’opzione WEB in Configurazione cartella controllata, viene generato un file JSON per record. Puoi utilizzare il file JSON per [precompilare un modello web](#web-template).
      * Quando si specificano le opzioni PRINT e WEB, vengono generati sia i documenti PDF che un file JSON per record.

## Richiama l’API Batch utilizzando le richieste REST

Puoi richiamare [API Batch](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/index.html) tramite richieste di trasferimento dello stato di rappresentanza (REST). Ti consente di fornire un endpoint REST ad altri utenti per accedere all’API e configurare i tuoi metodi per l’elaborazione, l’archiviazione e la personalizzazione della comunicazione interattiva. Puoi sviluppare un servlet Java personalizzato per distribuire l’API sull’istanza AEM.

Prima di distribuire il servlet Java, accertati di disporre di una comunicazione interattiva e che i file di dati corrispondenti siano pronti. Per creare e distribuire il servlet Java, effettua le seguenti operazioni:

1. Accedi all’istanza dell’AEM e crea una comunicazione interattiva. Per utilizzare la comunicazione interattiva indicata nel codice di esempio riportato di seguito: [fai clic qui](assets/SimpleMediumIC.zip).
1. [Creare e distribuire un progetto AEM con Apache Maven](https://helpx.adobe.com/experience-manager/using/maven_arch13.html) sull’istanza AEM.
1. Aggiungi [AEM Forms Client SDK versione 6.0.12](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) o più avanti nell’elenco delle dipendenze del file POM del progetto AEM. Ad esempio:

   ```xml
       <dependency>
           <groupId>com.adobe.aemfd</groupId>
           <artifactId>aemfd-client-sdk</artifactId>
           <version>6.0.122</version>
       </dependency>
   ```

1. Apri il progetto Java, crea un file .java, ad esempio CCMBatchServlet.java. Aggiungi al file il codice seguente:

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
   * Quando si specifica l&#39;opzione WEB, viene generato un file JSON per record. Puoi utilizzare il file JSON per [precompilare un modello web](#web-template).
   * Quando si specificano le opzioni PRINT e WEB, vengono generati sia i documenti PDF che un file JSON per record.

1. [Utilizza Maven per distribuire il codice aggiornato all’istanza AEM](https://helpx.adobe.com/experience-manager/using/maven_arch13.html#BuildtheOSGibundleusingMaven).
1. Richiama l’API batch per generare la comunicazione interattiva. L’API batch stampa restituisce un flusso di file PDF e .json a seconda del numero di record. Puoi utilizzare il file JSON per [precompilare un modello web](#web-template). Se utilizzi il codice riportato sopra, l’API viene distribuita in `http://localhost:4502/bin/batchServlet`. Il codice stampa e restituisce un flusso di un file PDF e un file JSON.

### Precompilare un modello web {#web-template}

Quando imposti batchType per il rendering del canale web, l’API genera un file JSON per ogni record di dati. Per unire il file JSON al canale web corrispondente per generare una comunicazione interattiva, puoi utilizzare la sintassi seguente:

**Sintassi**
`http://host:port/<template-path>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=<guide-merged-json-path>`

**Esempio**
Se il file JSON si trova in `C:\batch\mergedJsonPath.json` e utilizzi il seguente modello di comunicazione interattiva: `http://host:port/content/dam/formsanddocuments/testsample/mediumic/jcr:content?channel=web`

Quindi, il seguente URL sul nodo di pubblicazione mostra il canale web della comunicazione interattiva
`http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=file:///C:/batch/mergedJsonData.json`

Oltre a salvare i dati sul file system, memorizzi i file JSON nell’archivio CRX, nel file system o sul server web, oppure puoi accedere ai dati tramite il servizio di precaricamento OSGI. Sintassi per unire i dati utilizzando vari protocolli:

* **Protocollo CRX**
  `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=crx:///tmp/fd/af/mergedJsonData.json`

* **Protocollo file**
  `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=file:///C:/Users/af/mergedJsonData.json`

* **Protocollo del servizio di preriempimento**
  `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=service://[SERVICE_NAME]/[IDENTIFIER]`

  SERVICE_NAME fa riferimento al nome del servizio di precompilazione OSGI. Consulta Creare ed eseguire un servizio di precompilazione.

  IDENTIFIER rimanda a tutti i metadati richiesti dal servizio di precompilazione OSGI per recuperare i dati di precompilazione. Un identificatore dell’utente connesso è un esempio di metadati che potrebbe essere utilizzato.

* **protocollo HTTP**
  `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=http://localhost:8000/somesamplexmlfile.xml`

>[!NOTE]
>
>Per impostazione predefinita, è abilitato solo il protocollo CRX. Per abilitare altri protocolli supportati, consulta [Configurazione del servizio di precompilazione tramite Configuration Manager](https://helpx.adobe.com/experience-manager/6-5/forms/using/prepopulate-adaptive-form-fields.html#ConfiguringprefillserviceusingConfigurationManager).
