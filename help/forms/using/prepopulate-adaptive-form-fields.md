---
title: Precompilare i campi del modulo adattivo
seo-title: Precompilare i campi del modulo adattivo
description: Utilizza i dati esistenti per precompilare i campi di un modulo adattivo.
seo-description: Con i moduli adattivi, gli utenti possono precompilare le informazioni di base in un modulo accedendo con i propri profili social. Questo articolo descrive come eseguire questa operazione.
uuid: 574de83a-7b5b-4a1f-ad37-b9717e5c14f1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 7139a0e6-0e37-477c-9e0b-aa356991d040
docset: aem65
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2202'
ht-degree: 0%

---


# Precompilare i campi del modulo adattivo{#prefill-adaptive-form-fields}

## Introduzione {#introduction}

È possibile precompilare i campi di un modulo adattivo utilizzando i dati esistenti. Quando un utente apre un modulo, i valori relativi a tali campi vengono precompilati. Per precompilare i dati in un modulo adattivo, rendi disponibili i dati utente come XML / JSON di precompilazione nel formato che corrisponde alla precompilazione della struttura dati dei moduli adattivi.

## Struttura dei dati di precompilazione {#the-prefill-structure}

Un modulo adattivo può contenere diversi campi associati o non associati. I campi associati sono campi trascinati dalla scheda Content Finder e contengono un valore di proprietà `bindRef` non vuoto nella finestra di dialogo di modifica del campo. I campi non associati vengono trascinati direttamente dal browser componenti della barra laterale e hanno un valore `bindRef` vuoto.

È possibile precompilare i campi associati e non associati di un modulo adattivo. I dati di precompilazione contengono le sezioni afBoundData e afUnBoundData per precompilare i campi associati e non associati di un modulo adattivo. La sezione `afBoundData` contiene i dati di precompilazione per i campi e i pannelli associati. Questi dati devono essere conformi allo schema del modello di modulo associato:

* Per i moduli adattivi che utilizzano il [modello di modulo XFA](../../forms/using/prepopulate-adaptive-form-fields.md), utilizzare il file XML di precompilazione conforme allo schema dati del modello XFA.
* Per i moduli adattivi che utilizzano [schema XML](#xml-schema-af), utilizzare il file XML di precompilazione conforme alla struttura dello schema XML.
* Per i moduli adattivi che utilizzano [schema JSON](#json-schema-based-adaptive-forms), utilizza il JSON di precompilazione conforme allo schema JSON.
* Per i moduli adattivi che utilizzano lo schema FDM, utilizza il JSON di precompilazione conforme con lo schema FDM.
* Per i moduli adattivi con [nessun modello di modulo](#adaptive-form-with-no-form-model), non sono presenti dati associati. Ogni campo è un campo non associato ed è precompilato utilizzando l’XML non associato.

### Struttura XML di precompilazione di esempio {#sample-prefill-xml-structure}

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

### Struttura JSON di precompilazione di esempio {#sample-prefill-json-structure}

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

Per i campi associati con lo stesso binding o campi non associati con lo stesso nome, i dati specificati nel tag XML o nell’oggetto JSON vengono compilati in tutti i campi. Ad esempio, due campi di un modulo vengono mappati sul nome `textbox` nei dati di precompilazione. Durante il runtime, se il primo campo casella di testo contiene &quot;A&quot;, viene automaticamente inserito &quot;A&quot; nella seconda casella di testo. Questo collegamento è denominato collegamento in tempo reale dei campi del modulo adattivo.

### Modulo adattivo che utilizza il modello di modulo XFA {#xfa-based-af}

La struttura dell’XML di precompilazione e dell’XML inviato per i moduli adattivi basati su XFA è la seguente:

* **Struttura** XML di precompilazione: Il codice XML di precompilazione per il modulo adattivo basato su XFA deve essere conforme allo schema dati del modello di modulo XFA. Per precompilare i campi non associati, racchiudi la struttura XML di precompilazione nel tag `/afData/afBoundData` .

* **Struttura** XML inviata: Se non viene utilizzato alcun XML di precompilazione, l’XML inviato contiene i dati per i campi associati e non associati nel tag  `afData` wrapper. Se viene utilizzato un XML di precompilazione, l&#39;XML inviato ha la stessa struttura dell&#39;XML di precompilazione. Se l&#39;XML di precompilazione inizia con il tag radice `afData`, anche l&#39;XML di output ha lo stesso formato. Se l&#39;XML di precompilazione non ha `afData/afBoundData`wrapper e inizia invece direttamente dal tag principale dello schema come `employeeData`, anche l&#39;XML inviato inizia con il tag `employeeData` .

Prefill-Submit-Data-ContentPackage.zip

[Get ](assets/prefill-submit-data-contentpackage.zip)
FileSample contenente dati di precompilazione e dati inviati

### Moduli adattivi basati su schema XML  {#xml-schema-af}

La struttura dell’XML di precompilazione e dell’XML inviato per i moduli adattivi basati sullo schema XML è la seguente:

* **Struttura** XML di precompilazione: L&#39;XML di precompilazione deve essere conforme allo schema XML associato. Per precompilare i campi non associati, racchiudi la struttura XML di precompilazione nel tag /afData/afBoundData .
* **Struttura** XML inviata: se non viene utilizzato alcun XML di precompilazione, l’XML inviato contiene i dati per i campi associati e non associati nel tag  `afData` wrapper. Se viene utilizzato il codice XML di precompilazione, il codice XML inviato ha la stessa struttura del codice XML di precompilazione. Se l&#39;XML di precompilazione inizia con il tag radice `afData`, l&#39;XML di output ha lo stesso formato. Se l&#39;XML di precompilazione non ha il wrapper `afData/afBoundData` e inizia invece direttamente dal tag principale dello schema come `employeeData`, anche l&#39;XML inviato inizia con il tag `employeeData` .

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

Per i campi il cui modello è lo schema XML, i dati vengono precompilati nel tag `afBoundData` come mostrato nell’XML di esempio riportato di seguito. Può essere utilizzato per precompilare un modulo adattivo con uno o più campi di testo non associati.

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
>Si consiglia di non utilizzare campi non associati nei pannelli associati (pannelli con `bindRef` non vuoto che è stato creato trascinando i componenti dalla barra laterale o dalla scheda Origini dati). Può causare la perdita di dati di questi campi non associati. Inoltre, è consigliabile che i nomi dei campi siano univoci all’interno del modulo, in particolare per i campi non associati.

#### Un esempio senza afData e afBoundData wrapper {#an-example-without-afdata-and-afbounddata-wrapper}

```xml
<?xml version="1.0" encoding="UTF-8"?><config>
 <assignmentDetails descriptionOfAssignment="Some Science Project" durationOfAssignment="34" financeRelatedProject="1" name="Lisa" numberOfMentees="1"/>
 <assignmentDetails descriptionOfAssignment="Kidding, right?" durationOfAssignment="4" financeRelatedProject="1" name="House" numberOfMentees="3"/>
</config>
```

### Moduli adattivi basati su schema JSON {#json-schema-based-adaptive-forms}

Per i moduli adattivi basati sullo schema JSON, la struttura di precompilare JSON e inviare JSON è descritta di seguito. Per ulteriori informazioni, consulta [Creazione di moduli adattivi con schema JSON](../../forms/using/adaptive-form-json-schema-form-model.md).

* **Struttura** JSON di precompilazione: Il JSON di precompilazione deve essere conforme allo schema JSON associato. Facoltativamente, può essere racchiuso nell&#39;oggetto /afData/afBoundData se si desidera precompilare anche i campi non associati.
* **Struttura** JSON inviata: se non viene utilizzato alcun JSON di precompilazione, il JSON inviato contiene i dati per i campi associati e non associati nel tag wrapper afData. Se si utilizza il JSON di precompilazione, il JSON inviato ha la stessa struttura del JSON di precompilazione. Se il JSON di precompilazione inizia con l&#39;oggetto radice afData, il JSON di output ha lo stesso formato. Se il JSON di precompilazione non dispone del wrapper afData/afBoundData e inizia invece direttamente dall’oggetto principale dello schema, come l’utente, anche il JSON inviato inizia con l’oggetto utente.

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

Per i campi che utilizzano il modello di schema JSON, i dati vengono precompilati nell&#39;oggetto afBoundData come mostrato nel JSON di esempio riportato di seguito. Può essere utilizzato per precompilare un modulo adattivo con uno o più campi di testo non associati. Di seguito è riportato un esempio di dati con wrapper `afData/afBoundData`:

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

Di seguito è riportato un esempio senza wrapper `afData/afBoundData`:

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
>L’utilizzo di campi non associati nei pannelli associati (pannelli con bindRef non vuoti creati trascinando componenti dalla barra laterale o dalla scheda Origini dati) è **non** consigliato in quanto potrebbe causare la perdita di dati dei campi non associati. È consigliabile assegnare nomi di campo univoci all’interno del modulo, in particolare per i campi non associati.

### Modulo adattivo senza modello di modulo {#adaptive-form-with-no-form-model}

Per i moduli adattivi privi di modello di modulo, i dati di tutti i campi si trovano sotto il tag `<data>` di `<afUnboundData> tag`.

Inoltre, prendere nota dei seguenti elementi:

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

## Configurazione del servizio di precompilazione utilizzando Configuration Manager {#configuring-prefill-service-using-configuration-manager}

Per abilitare il servizio di precompilazione, specifica la configurazione predefinita del servizio di precompilazione nella configurazione della console Web AEM. Per configurare il servizio di precompilazione, effettua le seguenti operazioni:

>[!NOTE]
>
>La configurazione del servizio di precompilazione è applicabile ai moduli adattivi, ai moduli HTML5 e ai set di moduli HTML5.

1. Apri **[!UICONTROL Configurazione console Web Adobe Experience Manager]** utilizzando l&#39;URL:\
   https://&lt;server>:&lt;port>/system/console/configMgr
1. Cerca e apri **[!UICONTROL Configurazione predefinita servizio di precompilazione]**.

   ![Configurazione della precompilazione](assets/prefill_config_new.png)

1. Immetti la posizione dei dati o un regex (espressione regolare) per le **Posizioni dei file di dati**. Esempi di percorsi di file di dati validi:

   * file:///C:/Users/public/Document/Prefill/.*
   * https://localhost:8000/somesamplexmlfile.xml

   >[!NOTE]
   >
   >Per impostazione predefinita, la precompilazione è consentita tramite file crx per tutti i tipi di Forms adattivo (XSD, XDP, JSON, FDM e senza modello di modulo). La precompilazione è consentita solo con file JSON e XML.

1. Il servizio di precompilazione è ora configurato per il modulo.

   >[!NOTE]
   >
   >Il protocollo crx si occupa della sicurezza dei dati precompilati e, quindi, è consentito per impostazione predefinita. Precompilazione tramite altri protocolli utilizzando regex generico potrebbe causare vulnerabilità. Nella configurazione , specifica una configurazione URL sicura per la protezione dei dati.

## Il curioso caso di pannelli ripetibili {#the-curious-case-of-repeatable-panels}

In genere, i campi associati (schema modulo) e non associati sono creati nello stesso modulo adattivo, ma le seguenti sono alcune eccezioni nel caso in cui il binding sia ripetibile:

* I pannelli ripetibili non associati non sono supportati per i moduli adattivi che utilizzano il modello di modulo XFA, lo schema XSD, JSON o lo schema FDM.
* Non utilizzare campi non associati in pannelli ripetibili associati.

>[!NOTE]
>
>Di regola, non combinare campi associati e non associati se sono intersecati in dati compilati dall’utente finale in campi non associati. Se possibile, è necessario modificare lo schema o il modello di modulo XFA e aggiungere una voce per i campi non associati, in modo che anch’esso diventi associato e i relativi dati siano disponibili come altri campi nei dati inviati.

## Protocolli supportati per la precompilazione dei dati utente {#supported-protocols-for-prefilling-user-data}

I moduli adattivi possono essere precompilati con i dati utente in formato precompilato tramite i seguenti protocolli, se configurati con regex valido:

### Protocollo crx:// {#the-crx-protocol}

```http
https://localhost:4502/content/forms/af/xml.html?wcmmode=disabled&dataRef=crx:///tmp/fd/af/myassets/sample.xml
```

Il nodo specificato deve avere una proprietà denominata `jcr:data` e contenere i dati.

### Protocollo file://  {#the-file-protocol-nbsp}

```http
https://localhost:4502/content/forms/af/someAF.html?wcmmode=disabled&dataRef=file:///C:/Users/form-user/Downloads/somesamplexml.xml
```

Il file di cui si fa riferimento deve trovarsi sullo stesso server.

### Protocollo https:// {#the-http-protocol}

```http
https://localhost:4502/content/forms/af/xml.html?wcmmode=disabled&dataRef=https://localhost:8000/somesamplexmlfile.xml
```

### Protocollo service:// {#the-service-protocol}

```http
https://localhost:4502/content/forms/af/abc.html?wcmmode=disabled&dataRef=service://[SERVICE_NAME]/[IDENTIFIER]
```

* SERVICE_NAME fa riferimento al nome del servizio di precompilazione OSGI. Fai riferimento a [Creare ed eseguire un servizio di precompilazione](../../forms/using/prepopulate-adaptive-form-fields.md#create-and-run-a-prefill-service).
* IDENTIFIER fa riferimento a tutti i metadati richiesti dal servizio di precompilazione OSGI per recuperare i dati di precompilazione. Un identificatore dell&#39;utente connesso è un esempio di metadati che possono essere utilizzati.

>[!NOTE]
>
>Il passaggio dei parametri di autenticazione non è supportato.

### Impostazione dell&#39;attributo dei dati in slingRequest {#setting-data-attribute-in-slingrequest}

Puoi anche impostare l&#39;attributo `data` in `slingRequest`, dove l&#39;attributo `data` è una stringa contenente XML o JSON, come mostrato nel codice di esempio seguente (Esempio per XML):

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

È possibile scrivere una stringa XML o JSON semplice contenente tutti i dati e impostarla in slingRequest. Questo può essere facilmente fatto nel tuo modulo di rendering JSP per qualsiasi componente, che desideri includere nella pagina in cui puoi impostare l&#39;attributo di dati slingRequest.

Ad esempio, dove vuoi creare una progettazione specifica per la pagina con un tipo specifico di intestazione. A questo scopo, è possibile scrivere il proprio `header.jsp`, che può essere incluso nel componente della pagina e impostare l&#39;attributo `data` .

Un altro buon esempio è un caso d&#39;uso in cui si desidera precompilare i dati di accesso attraverso account social come Facebook, Twitter o LinkedIn. In questo caso, puoi includere un semplice JSP in `header.jsp`, che recupera i dati dall’account utente e imposta il parametro dei dati.

precompila pagina component.zip

[Ottieni ](assets/prefill-page-component.zip)
FileSample prefill.jsp nel componente pagina

## Servizio di precompilazione personalizzato AEM Forms {#aem-forms-custom-prefill-service}

È possibile utilizzare il servizio di precompilazione personalizzato per gli scenari, in cui si leggono costantemente i dati da un’origine predefinita. Il servizio di precompilazione legge i dati da origini dati definite ed esegue la precompilazione dei campi del modulo adattivo con il contenuto del file di dati di precompilazione. Inoltre, consente di associare in modo permanente i dati precompilati a un modulo adattivo.

### Creare ed eseguire un servizio di precompilazione {#create-and-run-a-prefill-service}

Il servizio di precompilazione è un servizio OSGi e viene fornito tramite il bundle OSGi. Puoi creare il bundle OSGi, caricarlo e installarlo nei bundle AEM Forms. Prima di iniziare a creare il bundle:

* [Scaricare l’SDK client di AEM Forms](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html)
* Scarica il pacchetto caldaia

* Posiziona il file di dati (dati di precompilazione) nell&#39;archivio crx. Puoi posizionare il file in qualsiasi posizione nella cartella \content di crx-repository.

[Ottieni file](assets/prefill-sumbit-xmlsandcontentpackage.zip)

#### Crea un servizio di precompilazione {#create-a-prefill-service}

Il pacchetto ricorrenti (pacchetto del servizio di precompilazione di esempio) contiene un esempio di implementazione del servizio di precompilazione AEM Forms. Apri il pacchetto ricorrenti in un editor di codice. Ad esempio, apri il progetto ricorrenti in Eclipse per la modifica. Dopo aver aperto il pacchetto ricorrenti in un editor di codice, esegui i seguenti passaggi per creare il servizio.

1. Apri il file src\main\java\com\adobe\test\Prefill.java per la modifica.
1. Nel codice, imposta il valore di:

   * `nodePath:` La variabile del percorso del nodo che punta alla posizione dell&#39;archivio crx contiene il percorso del file di dati (prefill). Ad esempio, /content/prefilldata.xml
   * `label:` Il parametro label specifica il nome visualizzato del servizio. Ad esempio, Servizio di precompilazione predefinito

1. Salva e chiudi il file `Prefill.java`.
1. Aggiungi il pacchetto `AEM Forms Client SDK` al percorso di compilazione del progetto ricorrenti.
1. Compila il progetto e crea il .jar per il bundle.

#### Avvia e utilizza il servizio di precompilazione {#start-and-use-the-prefill-service}

Per avviare il servizio di precompilazione, carica il file JAR nella console Web AEM Forms e attiva il servizio. Ora, il servizio inizia a comparire nell’editor di moduli adattivi. Per associare un servizio di precompilazione a un modulo adattivo:

1. Apri il modulo adattivo in Forms Editor e apri il pannello Proprietà per il contenitore modulo.
1. Nella console Proprietà , passa al contenitore AEM Forms > Base > Servizio di precompilazione.
1. Selezionare il servizio di precompilazione predefinito e fare clic su **[!UICONTROL Salva]**. Il servizio è associato al modulo.

## Precompilazione dei dati sul client {#prefill-at-client}

Quando si precompila un modulo adattivo, il server AEM Forms unisce i dati con un modulo adattivo e consegna il modulo compilato. Per impostazione predefinita, l’azione di unione dati viene eseguita sul server.

È possibile configurare il server AEM Forms per eseguire l’azione di unione dati sul client anziché sul server. Riduce notevolmente il tempo necessario per precompilare ed eseguire il rendering dei moduli adattivi. Per impostazione predefinita, la funzione è disabilitata. È possibile abilitarlo da Configuration Manager o dalla riga di comando.

* Per abilitare o disabilitare la gestione della configurazione:
   1. Apri Gestione configurazione AEM.
   1. Individua e apri la configurazione del modulo adattivo e del canale web di comunicazione interattiva
   1. Abilita l’opzione Configuration.af.clientside.datamerge.enabled.name
* Per attivare o disattivare dalla riga di comando:
   * Per abilitare, esegui il seguente comando cURL:
      `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=true \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`

   * Per disattivare, esegui il seguente comando cURL:
      `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=false \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`
   Per sfruttare appieno l&#39;opzione di precompilazione dei dati sul client, aggiorna il servizio di precompilazione per restituire [FileAttachmentMap](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html) e [CustomContext](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html)