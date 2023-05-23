---
title: Precompilare i campi del modulo adattivo
seo-title: Prefill adaptive form fields
description: Utilizza i dati esistenti per precompilare i campi di un modulo adattivo.
seo-description: With adaptive forms, you users can prefill basic information in a form by logging in with their social profiles. This article describes how you can accomplish this.
uuid: 574de83a-7b5b-4a1f-ad37-b9717e5c14f1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 7139a0e6-0e37-477c-9e0b-aa356991d040
docset: aem65
feature: Adaptive Forms
exl-id: 29cbc330-7b3d-457e-ba4a-7ce6091f3836
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2169'
ht-degree: 0%

---

# Precompilare i campi del modulo adattivo{#prefill-adaptive-form-fields}

## Introduzione {#introduction}

È possibile precompilare i campi di un modulo adattivo utilizzando dati esistenti. Quando un utente apre un modulo, i valori di tali campi vengono precompilati. Per precompilare i dati in un modulo adattivo, rendi i dati utente disponibili come XML/JSON precompilato nel formato conforme alla struttura dati precompilata dei moduli adattivi.

## Struttura dei dati preriempimento {#the-prefill-structure}

Un modulo adattivo può contenere una combinazione di campi associati e non associati. I campi associati sono campi trascinati dalla scheda Content Finder e che contengono elementi non vuoti `bindRef` valore della proprietà nella finestra di dialogo di modifica del campo. I campi non associati vengono trascinati direttamente dal browser componenti della barra laterale e hanno un `bindRef` valore.

Puoi precompilare sia i campi associati che quelli non associati di un modulo adattivo. I dati di precompilazione contengono le sezioni afBoundData e afUnBoundData per precompilare sia i campi associati che quelli non associati di un modulo adattivo. Il `afBoundData` contiene i dati di precompilazione per i campi e i pannelli associati. Questi dati devono essere conformi allo schema del modello di modulo associato:

* Per i moduli adattivi che utilizzano [Modello di modulo XFA](../../forms/using/prepopulate-adaptive-form-fields.md), utilizza il file XML di precompilazione conforme allo schema dati del modello XFA.
* Per i moduli adattivi che utilizzano [Schema XML](#xml-schema-af), utilizza il file XML di precompilazione conforme alla struttura dello schema XML.
* Per i moduli adattivi che utilizzano [Schema JSON](#json-schema-based-adaptive-forms), utilizza il JSON di precompilazione conforme allo schema JSON.
* Per i moduli adattivi che utilizzano lo schema FDM, utilizza il JSON di precompilazione conforme allo schema FDM.
* Per moduli adattivi con [nessun modello modulo](#adaptive-form-with-no-form-model), non sono presenti dati associati. Ogni campo è un campo non associato e viene precompilato utilizzando l&#39;XML non associato.

### Esempio di struttura XML di preriempimento {#sample-prefill-xml-structure}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<afData>
  <afBoundData>
     <employeeData>
        .
     </employeeData>
  </afBoundData>

  <afUnboundData>
    <data>
      <textbox>Hello World</textbox>
         .
         .
      <numericbox>12</numericbox>
         . 
         .              
    </data>
  </afUnboundData>
</afData>
```

### Esempio di struttura JSON di preriempimento {#sample-prefill-json-structure}

```javascript
{
   "afBoundData": {
      "employeeData": { }
   },
   "afUnboundData": {
      "data": {
         "textbox": "Hello World",
         "numericbox": "12"
      }
   }
}
```

Per i campi associati con lo stesso bindref o campi non associati con lo stesso nome, i dati specificati nel tag XML o nell’oggetto JSON vengono compilati in tutti i campi. Ad esempio, due campi in un modulo sono mappati al nome `textbox` nei dati di precompilazione. Durante il runtime, se il primo campo della casella di testo contiene &quot;A&quot;, nella seconda casella di testo viene automaticamente inserito &quot;A&quot;. Questo collegamento è denominato collegamento in tempo reale di campi modulo adattivo.

### Modulo adattivo che utilizza il modello di modulo XFA {#xfa-based-af}

La struttura dell’XML di precompilazione e dell’XML inviato per i moduli adattivi basati su XFA è la seguente:

* **Precompila struttura XML**: l’XML di precompilazione per il modulo adattivo basato su XFA deve essere conforme allo schema di dati del modello di modulo XFA. Per precompilare i campi non associati, racchiudi la struttura XML precompilata in `/afData/afBoundData` tag.

* **Struttura XML inviata**: quando non viene utilizzato alcun XML di precompilazione, l’XML inviato contiene dati sia per i campi associati che per quelli non associati in `afData` tag wrapper. Se si utilizza un XML di precompilazione, il codice XML inviato ha la stessa struttura del codice XML di precompilazione. Se l&#39;XML di precompilazione inizia con `afData` principale, anche l&#39;XML di output ha lo stesso formato. Se il file XML di precompilazione non contiene `afData/afBoundData`wrapper e inizia direttamente dal tag principale dello schema, come `employeeData`, anche il codice XML inviato inizia con `employeeData` tag.

Prefill-Submit-Data-ContentPackage.zip

[Ottieni file](assets/prefill-submit-data-contentpackage.zip)
Campione contenente i dati di precompilazione e i dati inviati

### Moduli adattivi basati su schema XML  {#xml-schema-af}

Di seguito è illustrata la struttura dell&#39;XML di precompilazione e dell&#39;XML inviato per i moduli adattivi basati su schema XML.

* **Precompila struttura XML**: l&#39;XML di precompilazione deve essere conforme allo schema XML associato. Per precompilare i campi non associati, racchiudi la struttura XML di precompilazione nel tag /afData/afBoundData.
* **Struttura XML inviata**: se non viene utilizzato alcun XML di precompilazione, l’XML inviato contiene dati sia per i campi associati che per quelli non associati in `afData` tag wrapper. Se si utilizza il codice XML di precompilazione, il codice XML inviato ha la stessa struttura del codice XML di precompilazione. Se l&#39;XML di precompilazione inizia con `afData` principale, l&#39;XML di output ha lo stesso formato. Se il file XML di precompilazione non contiene `afData/afBoundData` wrapper e inizia direttamente dal tag principale dello schema, come `employeeData`, anche il codice XML inviato inizia con `employeeData` tag.

```xml
<?xml version="1.0" encoding="utf-8" ?> 
<xs:schema targetNamespace="https://adobe.com/sample.xsd"
            xmlns="https://adobe.com/sample.xsd"
            xmlns:xs="https://www.w3.org/2001/XMLSchema">
 
    <xs:element name="sample" type="SampleType"/>
         
    <xs:complexType name="SampleType">
        <xs:sequence>
            <xs:element name="noOfProjectsAssigned" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>
</xs:schema>
```

Per i campi il cui modello è lo schema XML, i dati vengono precompilati nel `afBoundData` come mostrato nel codice XML di esempio seguente. Può essere utilizzato per precompilare un modulo adattivo con uno o più campi di testo non associati.

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <textbox>Ignorance is bliss :) </textbox>
    </data>
  </afUnboundData>
  <afBoundData>
    <data>
      <noOfProjectsAssigned>twelve</noOfProjectsAssigned>
    </data>
  </afBoundData>
</afData>
```

>[!NOTE]
>
>Si consiglia di non utilizzare campi non associati nei pannelli associati (pannelli con `bindRef` creato trascinando i componenti dalla barra laterale o dalla scheda Origini dati). Potrebbe causare la perdita di dati di questi campi non associati. Inoltre, si consiglia di assegnare nomi univoci ai campi nel modulo, in particolare per i campi non associati.

#### Esempio senza afData e wrapper afBoundData {#an-example-without-afdata-and-afbounddata-wrapper}

```xml
<?xml version="1.0" encoding="UTF-8"?><config>
 <assignmentDetails descriptionOfAssignment="Some Science Project" durationOfAssignment="34" financeRelatedProject="1" name="Lisa" numberOfMentees="1"/>
 <assignmentDetails descriptionOfAssignment="Kidding, right?" durationOfAssignment="4" financeRelatedProject="1" name="House" numberOfMentees="3"/>
</config>
```

### Moduli adattivi basati su schema JSON {#json-schema-based-adaptive-forms}

Per i moduli adattivi basati sullo schema JSON, di seguito è descritta la struttura del JSON precompilato e del JSON inviato. Per ulteriori informazioni, consulta [Creazione di moduli adattivi tramite schema JSON](../../forms/using/adaptive-form-json-schema-form-model.md).

* **Precompilare la struttura JSON**: il JSON di precompilazione deve essere conforme allo schema JSON associato. Facoltativamente, può essere racchiuso nell&#39;oggetto /afData/afBoundData se desideri precompilare anche i campi non associati.
* **Struttura JSON inviata**: se non viene utilizzato alcun JSON di precompilazione, il JSON inviato contiene dati sia per i campi associati che per quelli non associati nel tag wrapper afData. Se si utilizza il JSON di precompilazione, il JSON inviato ha la stessa struttura del JSON di precompilazione. Se il JSON di precompilazione inizia con l’oggetto principale afData, il JSON di output ha lo stesso formato. Se il JSON di precompilazione non ha il wrapper afData/afBoundData e inizia direttamente dall’oggetto principale dello schema, come utente, anche il JSON inviato inizia con l’oggetto utente.

```json
{
    "id": "https://some.site.somewhere/entry-schema#",
    "$schema": "https://json-schema.org/draft-04/schema#",
    "type": "object",
    "properties": {
        "address": {
            "type": "object",
            "properties": { 
    "name": {
     "type": "string"
    },
    "age": {
     "type": "integer"
}}}}}
```

Per i campi che utilizzano il modello di schema JSON, i dati vengono precompilati nell’oggetto afBoundData come mostrato nel JSON di esempio di seguito. Può essere utilizzato per precompilare un modulo adattivo con uno o più campi di testo non associati. Di seguito è riportato un esempio di dati con `afData/afBoundData` wrapper:

```json
{
  "afData": {
    "afUnboundData": {
      "data": { "textbox": "Ignorance is bliss :) " }
    },
    "afBoundData": {
      "data": { {
   "user": {
    "address": {
     "city": "Noida",
     "country": "India"
}}}}}}}
```

Di seguito è riportato un esempio senza `afData/afBoundData` wrapper:

```json
{
 "user": {
  "address": {
   "city": "Noida",
   "country": "India"
}}}
```

>[!NOTE]
>
>L’utilizzo di campi non associati nei pannelli associati (pannelli con bindRef non vuoto creati trascinando componenti dalla barra laterale o dalla scheda Origini dati) è **non** consigliato in quanto potrebbe causare la perdita di dati dei campi non associati. Si consiglia di avere nomi di campo univoci nel modulo, in particolare per i campi non associati.

### Modulo adattivo senza modello di modulo {#adaptive-form-with-no-form-model}

Per i moduli adattivi senza modello di modulo, i dati per tutti i campi si trovano sotto `<data>` tag di `<afUnboundData> tag`.

Inoltre, prendi nota di quanto segue:

I tag XML per i dati utente inviati per vari campi vengono generati utilizzando il nome dei campi. Pertanto, i nomi dei campi devono essere univoci.

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <radiobutton>2</radiobutton>
      <repeatable_panel_no_form_model>
        <numericbox>12</numericbox>
      </repeatable_panel_no_form_model>
      <repeatable_panel_no_form_model>
        <numericbox>21</numericbox>
      </repeatable_panel_no_form_model>
      <checkbox>2</checkbox>
      <textbox>Nopes</textbox>
    </data>
  </afUnboundData>
  <afBoundData/>
</afData>
```

## Configurazione del servizio di precompilazione tramite Configuration Manager {#configuring-prefill-service-using-configuration-manager}

Per abilitare il servizio di precompilazione, specifica Configurazione predefinita servizio di precompilazione nella configurazione della console web AEM. Per configurare il servizio di precompilazione, effettua le seguenti operazioni:

>[!NOTE]
>
>La Configurazione del servizio di precompilazione è applicabile ai moduli adattivi, ai moduli HTML5 e ai set di moduli HTML5.

1. Apri **[!UICONTROL Configurazione della console web Adobe Experience Manager]** utilizzando l’URL:\
   https://&lt;server>:&lt;port>/system/console/configMgr
1. Cerca e apri **[!UICONTROL Configurazione predefinita servizio preriempimento]**.

   ![Configurazione preriempimento](assets/prefill_config_new.png)

1. Immetti la posizione dei dati o un’espressione regex (espressione regolare) per il **Percorsi dei file di dati**. Di seguito sono riportati alcuni esempi di percorsi validi per i file di dati:

   * file:///C:/Users/public/Document/Prefill/.&#42;
   * https://localhost:8000/somesamplexmlfile.xml
   >[!NOTE]
   >
   >Per impostazione predefinita, la precompilazione è consentita tramite file crx per tutti i tipi di Forms adattivo (XSD, XDP, JSON, FDM e non basati su modello modulo). La precompilazione è consentita solo con file JSON e XML.

1. Il servizio di precompilazione è ora configurato per il modulo.

   >[!NOTE]
   >
   >Il protocollo crx si occupa della sicurezza dei dati precompilati ed è quindi consentito per impostazione predefinita. La precompilazione tramite altri protocolli utilizzando regex generico potrebbe causare vulnerabilità. Nella configurazione, specifica una configurazione URL sicura per proteggere i dati.

## Il curioso caso dei pannelli ripetibili {#the-curious-case-of-repeatable-panels}

In genere, i campi associati (schema modulo) e non associati vengono creati nello stesso modulo adattivo, ma di seguito sono riportate alcune eccezioni nel caso in cui i campi associati siano ripetibili:

* I pannelli ripetibili non associati non sono supportati per i moduli adattivi che utilizzano il modello di modulo XFA, XSD, lo schema JSON o lo schema FDM.
* Non utilizzare campi non associati nei pannelli ripetibili associati.

>[!NOTE]
>
>Di regola, non combinare campi associati e non associati se sono intersecati in dati compilati dall’utente finale in campi non associati. Se possibile, è necessario modificare lo schema o il modello di modulo XFA e aggiungere una voce per i campi non associati, in modo che anch&#39;esso diventi associato e i relativi dati siano disponibili come altri campi nei dati inviati.

## Protocolli supportati per la precompilazione dei dati utente {#supported-protocols-for-prefilling-user-data}

I moduli adattivi possono essere precompilati con i dati utente in formato dati precompilati tramite i seguenti protocolli se configurati con regex valido:

### Il protocollo crx:// {#the-crx-protocol}

```http
https://localhost:4502/content/forms/af/xml.html?wcmmode=disabled&dataRef=crx:///tmp/fd/af/myassets/sample.xml
```

Il nodo specificato deve avere una proprietà denominata `jcr:data` e conserva i dati.

### Il protocollo file://  {#the-file-protocol-nbsp}

```http
https://localhost:4502/content/forms/af/someAF.html?wcmmode=disabled&dataRef=file:///C:/Users/form-user/Downloads/somesamplexml.xml
```

Il file di riferimento deve trovarsi sullo stesso server.

### Il protocollo https:// {#the-http-protocol}

```http
https://localhost:4502/content/forms/af/xml.html?wcmmode=disabled&dataRef=https://localhost:8000/somesamplexmlfile.xml
```

### Il protocollo service:// {#the-service-protocol}

```http
https://localhost:4502/content/forms/af/abc.html?wcmmode=disabled&dataRef=service://[SERVICE_NAME]/[IDENTIFIER]
```

* SERVICE_NAME fa riferimento al nome del servizio di precompilazione OSGI. Fai riferimento a [Creare ed eseguire un servizio di precompilazione](../../forms/using/prepopulate-adaptive-form-fields.md#create-and-run-a-prefill-service).
* IDENTIFIER rimanda a tutti i metadati richiesti dal servizio di precompilazione OSGI per recuperare i dati di precompilazione. Un identificatore dell’utente connesso è un esempio di metadati che potrebbe essere utilizzato.

>[!NOTE]
>
>Il passaggio dei parametri di autenticazione non è supportato.

### Impostazione dell’attributo dei dati in slingRequest {#setting-data-attribute-in-slingrequest}

È inoltre possibile impostare `data` attributo in `slingRequest`, in cui `data` attribute è una stringa contenente XML o JSON, come illustrato nel codice di esempio seguente (ad esempio, per XML):

```javascript
<%
           String dataXML="<afData>" +
                            "<afUnboundData>" +
                                "<data>" +
                                    "<first_name>"+ "Tyler" + "</first_name>" +
                                    "<last_name>"+ "Durden " + "</last_name>" +
                                    "<gender>"+ "Male" + "</gender>" +
                                    "<location>"+ "Texas" + "</location>" +
                                    "</data>" +
                            "</afUnboundData>" +
                        "</afData>";
        slingRequest.setAttribute("data", dataXML);
%>
```

Puoi scrivere una stringa XML o JSON semplice contenente tutti i tuoi dati e impostarla in slingRequest. Puoi eseguire facilmente questa operazione nel JSP di rendering per qualsiasi componente che desideri includere nella pagina in cui puoi impostare l’attributo dati slingRequest.

Ad esempio, dove desideri una progettazione specifica per la pagina con un tipo specifico di intestazione. Per ottenere questo risultato, puoi scrivere il tuo `header.jsp`, che puoi includere nel componente Pagina e impostare `data` attributo.

Un altro buon esempio è un caso d’uso in cui si desidera precompilare i dati all’accesso tramite account social come Facebook, Twitter o LinkedIn. In questo caso, puoi includere una semplice JSP in `header.jsp`, che recupera i dati dall’account utente e imposta il parametro di dati.

prefill-page component.zip

[Ottieni file](assets/prefill-page-component.zip)
Esempio di prefill.jsp nel componente pagina

## Servizio di preriempimento personalizzato AEM Forms {#aem-forms-custom-prefill-service}

Puoi utilizzare il servizio di preriempimento personalizzato per gli scenari in cui si leggono costantemente i dati da un’origine predefinita. Il servizio di precompilazione legge i dati dalle origini dati definite e precompila i campi del modulo adattivo con il contenuto del file di dati di precompilazione. Consente inoltre di associare in modo permanente i dati precompilati a un modulo adattivo.

### Creare ed eseguire un servizio di precompilazione {#create-and-run-a-prefill-service}

Il servizio di precompilazione è un servizio OSGi ed è fornito tramite bundle OSGi. Crea il bundle OSGi, caricalo e installalo nei bundle di AEM Forms. Prima di iniziare a creare il bundle:

* [Scaricare l’SDK del client di AEM Forms](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)
* Scarica il pacchetto boilerplate

* Inserisci il file di dati (dati di precompilazione) nel crx-repository. È possibile inserire il file in qualsiasi posizione nella cartella \content del repository crx.

[Ottieni file](assets/prefill-sumbit-xmlsandcontentpackage.zip)

#### Creare un servizio di preriempimento {#create-a-prefill-service}

Il pacchetto boilerplate (esempio di pacchetto di servizio di preriempimento) contiene un esempio di implementazione del servizio di preriempimento AEM Forms. Apri il pacchetto boilerplate in un editor di codice. Ad esempio, apri il progetto boilerplate in Eclipse per la modifica. Dopo aver aperto il pacchetto boilerplate in un editor di codice, esegui i seguenti passaggi per creare il servizio.

1. Apri il file src\main\java\com\adobe\test\Prefill.java per la modifica.
1. Nel codice, imposta il valore di:

   * `nodePath:` La variabile del percorso del nodo che punta alla posizione dell’archivio crx contiene il percorso del file di dati (precaricamento). Ad esempio, /content/prefilldata.xml
   * `label:` Il parametro label specifica il nome visualizzato del servizio. Ad esempio, Servizio di precompilazione predefinito

1. Salva e chiudi `Prefill.java` file.
1. Aggiungi il `AEM Forms Client SDK` nel percorso di build del progetto boilerplate.
1. Compila il progetto e crea il file .jar per il bundle.

#### Avviare e utilizzare il servizio di precompilazione {#start-and-use-the-prefill-service}

Per avviare il servizio di precompilazione, carica il file JAR su AEM Forms Web Console e attiva il servizio. Ora il servizio inizia a essere visualizzato nell’editor di moduli adattivi. Per associare un servizio di precompilazione a un modulo adattivo:

1. Apri il modulo adattivo in Forms Editor e apri il pannello Proprietà del Contenitore modulo.
1. Nella console Proprietà, passa a Contenitore AEM Forms > Base > Servizio preriempimento.
1. Seleziona il servizio di preriempimento predefinito e fai clic su **[!UICONTROL Salva]**. Il servizio è associato al modulo.

## Precompila dati sul client {#prefill-at-client}

Quando si precompila un modulo adattivo, il server AEM Forms unisce i dati con un modulo adattivo e consegna all’utente il modulo compilato. Per impostazione predefinita, l&#39;operazione di unione dati viene eseguita nel server.

Puoi configurare il server AEM Forms in modo che esegua l’azione di unione dati sul client anziché sul server. Riduce in modo significativo il tempo necessario per precompilare ed eseguire il rendering dei moduli adattivi. Per impostazione predefinita, la funzione è disabilitata. È possibile abilitarlo dalla riga di comando o da Configuration Manager.

* Per attivare o disattivare da Gestione configurazione:
   1. Apri Gestione configurazione AEM.
   1. Individuare e aprire il modulo adattivo e la configurazione del canale web di comunicazione interattiva
   1. Abilita l’opzione Configuration.af.clientside.datamerge.enabled.name
* Per attivare o disattivare dalla riga di comando:
   * Per abilitare questa funzione, esegui il seguente comando cURL:
      `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=true \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`

   * Per disattivare, eseguire il seguente comando cURL:
      `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=false \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`
   Per sfruttare appieno l’opzione di precompilazione dei dati nel client, aggiorna il servizio di precompilazione per restituire [FileAttachmentMap](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html) e [ContestoPersonalizzato](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html)
