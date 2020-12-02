---
title: Precompila campi modulo adattivo
seo-title: Precompila campi modulo adattivo
description: Utilizzare i dati esistenti per precompilare i campi di un modulo adattivo.
seo-description: Con i moduli adattivi, gli utenti possono precompilare le informazioni di base in un modulo accedendo ai propri profili sociali. In questo articolo viene descritto come ottenere questo risultato.
uuid: 574de83a-7b5b-4a1f-ad37-b9717e5c14f1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 7139a0e6-0e37-477c-9e0b-aa356991d040
docset: aem65
translation-type: tm+mt
source-git-commit: 12b2b73b6363c90d784527b260d664e48c746496
workflow-type: tm+mt
source-wordcount: '2200'
ht-degree: 0%

---


# Precompila campi modulo adattivo{#prefill-adaptive-form-fields}

## Introduzione {#introduction}

È possibile precompilare i campi di un modulo adattivo utilizzando i dati esistenti. Quando un utente apre un modulo, i valori di tali campi vengono precompilati. Per precompilare i dati in un modulo adattivo, rendere disponibili i dati utente come precompilare XML / JSON nel formato che aderisce alla precompilazione della struttura di dati dei moduli adattivi.

## Struttura dei dati di precompilazione {#the-prefill-structure}

Un modulo adattivo può contenere diversi campi associati o non associati. I campi associati sono campi trascinati dalla scheda Content Finder e contengono un valore di proprietà `bindRef` non vuoto nella finestra di dialogo di modifica del campo. I campi non associati vengono trascinati direttamente dal Browser componenti della barra laterale e hanno un valore `bindRef` vuoto.

È possibile precompilare i campi associati e non associati di un modulo adattivo. I dati di precompilazione contengono le sezioni afBoundData e afUnBoundData per precompilare i campi associati e non associati di un modulo adattivo. La sezione `afBoundData` contiene i dati di precompilazione per i campi e i pannelli associati. Questi dati devono essere conformi allo schema del modello di modulo associato:

* Per i moduli adattivi che utilizzano il modello di modulo [XFA](../../forms/using/prepopulate-adaptive-form-fields.md), utilizzare il codice XML di precompilazione conforme allo schema dati del modello XFA.
* Per i moduli adattivi che utilizzano [schema XML](#xml-schema-af), utilizzare il file XML di precompilazione conforme alla struttura dello schema XML.
* Per i moduli adattivi che utilizzano lo schema [JSON](#json-schema-based-adaptive-forms), utilizzare il JSON precompilatore conforme allo schema JSON.
* Per i moduli adattivi che utilizzano lo schema FDM, utilizzare il JSON di precompilazione conforme allo schema FDM.
* Per i moduli adattivi con [nessun modello di modulo](#adaptive-form-with-no-form-model), non sono presenti dati associati. Ogni campo è un campo non associato ed è precompilato utilizzando l&#39;XML non associato.

### Esempio di struttura XML precompilata {#sample-prefill-xml-structure}

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

### Esempio di struttura JSON precompilata {#sample-prefill-json-structure}

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

Per i campi associati con lo stesso binding o campi non associati con lo stesso nome, i dati specificati nel tag XML o nell&#39;oggetto JSON vengono compilati in tutti i campi. Ad esempio, due campi in un modulo vengono mappati sul nome `textbox` nei dati di precompilazione. Durante il runtime, se il primo campo casella di testo contiene &quot;A&quot;, viene automaticamente inserito &quot;A&quot; nella seconda casella di testo. Questo collegamento è denominato collegamento attivo di campi modulo adattivi.

### Modulo adattivo che utilizza il modello di modulo XFA {#xfa-based-af}

La struttura dell&#39;XML di precompilazione e dell&#39;XML inviato per i moduli adattivi basati su XFA è la seguente:

* **Precompila struttura** XML: Il codice XML di precompilazione per il modulo adattivo basato su XFA deve essere conforme allo schema dati del modello di modulo XFA. Per precompilare i campi non associati, racchiudere la struttura XML di precompilazione nel tag `/afData/afBoundData`.

* **Struttura** XML inviata: Se non viene utilizzato alcun XML di precompilazione, l&#39;XML inviato contiene i dati per i campi associati e non associati nel tag  `afData` wrapper. Se si utilizza un XML di precompilazione, l&#39;XML inviato ha la stessa struttura dell&#39;XML di precompilazione. Se l&#39;XML di precompilazione inizia con il tag principale `afData`, anche l&#39;XML di output ha lo stesso formato. Se l&#39;XML di precompilazione non contiene il wrapper `afData/afBoundData`e inizia direttamente dal tag principale dello schema come `employeeData`, anche l&#39;XML inviato inizia con il tag `employeeData`.

Prefill-Submit-Data-ContentPackage.zip

[Get ](assets/prefill-submit-data-contentpackage.zip)
FileSample contenente dati di precompilazione e dati inviati

### Moduli adattivi basati sullo schema XML  {#xml-schema-af}

La struttura del file XML precompilato e del file XML inviato per i moduli adattivi basati sullo schema XML è la seguente:

* **Precompila struttura** XML: L&#39;XML di precompilazione deve essere conforme allo schema XML associato. Per precompilare i campi non associati, racchiudere la struttura XML di precompilazione nel tag /afData/afBoundData.
* **Struttura** XML inviata: se non viene utilizzato alcun XML di precompilazione, l&#39;XML inviato contiene i dati per i campi associati e non associati nel tag  `afData` wrapper. Se si utilizza l&#39;XML di precompilazione, l&#39;XML inviato ha la stessa struttura dell&#39;XML di precompilazione. Se l&#39;XML di precompilazione inizia con il tag principale `afData`, l&#39;XML di output ha lo stesso formato. Se l&#39;XML di precompilazione non contiene il wrapper `afData/afBoundData` e inizia direttamente dal tag principale dello schema come `employeeData`, anche l&#39;XML inviato inizia con il tag `employeeData`.

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

Per i campi il cui modello è lo schema XML, i dati vengono precompilati nel tag `afBoundData` come mostrato nell&#39;XML di esempio seguente. Può essere utilizzato per precompilare un modulo adattivo con uno o più campi di testo non associati.

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
>È consigliabile non utilizzare i campi non associati nei pannelli associati (pannelli con `bindRef` non vuoti creati trascinando i componenti dalla barra laterale o dalla scheda Origini dati). Può causare la perdita di dati di questi campi non associati. Inoltre, si consiglia di assegnare nomi univoci ai campi del modulo, in particolare per i campi non associati.

#### Un esempio senza afData e afBoundData wrapper {#an-example-without-afdata-and-afbounddata-wrapper}

```xml
<?xml version="1.0" encoding="UTF-8"?><config>
 <assignmentDetails descriptionOfAssignment="Some Science Project" durationOfAssignment="34" financeRelatedProject="1" name="Lisa" numberOfMentees="1"/>
 <assignmentDetails descriptionOfAssignment="Kidding, right?" durationOfAssignment="4" financeRelatedProject="1" name="House" numberOfMentees="3"/>
</config>
```

### Moduli adattivi basati sullo schema JSON {#json-schema-based-adaptive-forms}

Per i moduli adattivi basati sullo schema JSON, la struttura di precompila JSON e invia JSON è descritta di seguito. Per ulteriori informazioni, vedere [Creazione di moduli adattivi con lo schema JSON](../../forms/using/adaptive-form-json-schema-form-model.md).

* **Precompila struttura** JSON: Il JSON di precompilazione deve essere conforme allo schema JSON associato. Facoltativamente, è possibile racchiudere l&#39;oggetto /afData/afBoundData se si desidera precompilare anche i campi non associati.
* **Struttura** JSON inviata: se non viene utilizzato alcun JSON di precompilazione, il JSON inviato contiene i dati per i campi associati e non associati nel tag wrapper afData. Se viene utilizzato il JSON di precompilazione, il JSON inviato ha la stessa struttura del JSON di precompilazione. Se il JSON di precompilazione inizia con l&#39;oggetto radice afData, il JSON di output ha lo stesso formato. Se il JSON di precompilazione non dispone del wrapper afData/afBoundData e inizia direttamente dall&#39;oggetto principale dello schema, ad esempio l&#39;utente, anche il JSON inviato inizia con l&#39;oggetto utente.

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

Per i campi che utilizzano il modello di schema JSON, i dati vengono precompilati nell&#39;oggetto afBoundData come illustrato nell&#39;esempio JSON riportato di seguito. Può essere utilizzato per precompilare un modulo adattivo con uno o più campi di testo non associati. Di seguito è riportato un esempio di dati con il wrapper `afData/afBoundData`:

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
>L&#39;utilizzo di campi non associati nei pannelli associati (pannelli con bindRef non vuoti creati trascinando componenti dalla barra laterale o dalla scheda Origini dati) è **non** consigliato in quanto potrebbe causare la perdita di dati dei campi non associati. È consigliabile assegnare nomi di campo univoci all&#39;interno del modulo, in particolare per i campi non associati.

### Modulo adattivo senza modello di modulo {#adaptive-form-with-no-form-model}

Per i moduli adattivi senza modello di modulo, i dati per tutti i campi si trovano sotto il tag `<data>` di `<afUnboundData> tag`.

Inoltre, prendete nota di quanto segue:

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

Per abilitare il servizio di precompilazione, specificate la Configurazione predefinita del servizio di precompilazione nella Configurazione AEM console Web. Per configurare il servizio Precompila, effettuate le seguenti operazioni:

>[!NOTE]
>
>Precompila configurazione del servizio è applicabile ai moduli adattivi, ai moduli HTML5 e ai set di moduli HTML5.

1. Apri **[!UICONTROL Configurazione console Web Adobe Experience Manager]** utilizzando l&#39;URL:\
   https://&lt;server>:&lt;porta>/sistema/console/configMgr
1. Cercare e aprire **[!UICONTROL Configurazione predefinita del servizio di precompilazione]**.

   ![Configurazione precompilata](assets/prefill_config_new.png)

1. Immettere la posizione dei dati o un regex (espressione regolare) per le **posizioni dei file di dati**. Alcuni esempi di percorsi validi per i file di dati sono:

   * file:///C:/Users/public/Document/Prefill/.*
   * https://localhost:8000/somesamplexmlfile.xml

   >[!NOTE]
   >
   >Per impostazione predefinita, la precompilazione è consentita tramite file crx per tutti i tipi di Forms adattivo (XSD, XDP, JSON, FDM e nessun modello di modulo). La precompilazione è consentita solo per i file JSON e XML.

1. Il servizio di precompilazione è ora configurato per il modulo.

   >[!NOTE]
   >
   >Il protocollo crx si occupa della protezione dei dati precompilati e, di conseguenza, è consentito per impostazione predefinita. La precompilazione tramite altri protocolli utilizzando regex generico potrebbe causare vulnerabilità. Nella configurazione, specificate una configurazione URL protetta per la protezione dei dati.

## Il curioso caso di pannelli ripetibili {#the-curious-case-of-repeatable-panels}

In genere, i campi associati (schema modulo) e non associati sono creati nello stesso modulo adattivo, ma le seguenti eccezioni sono alcune nel caso in cui il binding sia ripetibile:

* I pannelli ripetibili non associati non sono supportati per i moduli adattivi che utilizzano il modello di modulo XFA, lo schema XSD, JSON o FDM.
* Non utilizzare campi non associati in pannelli ripetibili associati.

>[!NOTE]
>
>Di regola, non utilizzare campi associati o non associati se questi sono intersecati in dati compilati dall&#39;utente finale in campi non associati. Se possibile, è necessario modificare lo schema o il modello di modulo XFA e aggiungere una voce per i campi non associati, in modo che anch&#39;esso venga associato e i relativi dati siano disponibili come altri campi nei dati inviati.

## Protocolli supportati per la precompilazione dei dati utente {#supported-protocols-for-prefilling-user-data}

I moduli adattivi possono essere precompilati con dati utente in formato precompilato tramite i seguenti protocolli, se configurati con regex valido:

### Il protocollo crx:// {#the-crx-protocol}

```http
https://localhost:4502/content/forms/af/xml.html?wcmmode=disabled&dataRef=crx:///tmp/fd/af/myassets/sample.xml
```

Il nodo specificato deve avere una proprietà denominata `jcr:data` e contenere i dati.

### Il protocollo file://  {#the-file-protocol-nbsp}

```http
https://localhost:4502/content/forms/af/someAF.html?wcmmode=disabled&dataRef=file:///C:/Users/form-user/Downloads/somesamplexml.xml
```

Il file di cui si fa riferimento deve trovarsi sullo stesso server.

### Il protocollo https:// {#the-http-protocol}

```http
https://localhost:4502/content/forms/af/xml.html?wcmmode=disabled&dataRef=https://localhost:8000/somesamplexmlfile.xml
```

### Il protocollo service:// {#the-service-protocol}

```http
https://localhost:4502/content/forms/af/abc.html?wcmmode=disabled&dataRef=service://[SERVICE_NAME]/[IDENTIFIER]
```

* SERVICE_NAME fa riferimento al nome del servizio di precompilazione OSGI. Fare riferimento a [Creare ed eseguire un servizio di precompilazione](../../forms/using/prepopulate-adaptive-form-fields.md#create-and-run-a-prefill-service).
* IDENTIFIER fa riferimento a tutti i metadati richiesti dal servizio di precompilazione OSGI per recuperare i dati di precompilazione. Un identificatore per l’utente connesso è un esempio di metadati che possono essere utilizzati.

>[!NOTE]
>
>La trasmissione dei parametri di autenticazione non è supportata.

### Impostazione dell&#39;attributo di dati in slingRequest {#setting-data-attribute-in-slingrequest}

Potete anche impostare l&#39;attributo `data` in `slingRequest`, dove l&#39;attributo `data` è una stringa contenente XML o JSON, come illustrato nel codice di esempio seguente (Esempio per XML):

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

È possibile scrivere una semplice stringa XML o JSON contenente tutti i dati e impostarla in slingRequest. Questo può essere facilmente fatto nel JSP del renderer per qualsiasi componente, che si desidera includere nella pagina in cui è possibile impostare l&#39;attributo dati slingRequest.

Ad esempio, dove si desidera creare una progettazione specifica per la pagina con un tipo specifico di intestazione. A tal fine, è possibile scrivere un `header.jsp` personalizzato, che può essere incluso nel componente della pagina e impostare l&#39;attributo `data`.

Un altro buon esempio è il caso di utilizzo in cui si desidera precompilare i dati di accesso tramite account social come Facebook, Twitter o LinkedIn. In questo caso, è possibile includere un semplice JSP in `header.jsp`, che raccoglie i dati dall&#39;account utente e imposta il parametro data.

precompila pagina component.zip

[Get ](assets/prefill-page-component.zip)
FileSample prefill.jsp nel componente pagina

##  servizio di precompilazione personalizzato AEM Forms {#aem-forms-custom-prefill-service}

Potete utilizzare il servizio di precompilazione personalizzato per gli scenari, in cui leggete costantemente i dati da un&#39;origine predefinita. Il servizio di precompilazione legge i dati da origini dati definite e compila i campi del modulo adattivo con il contenuto del file di dati di precompilazione. Consente inoltre di associare in modo permanente i dati precompilati a un modulo adattivo.

### Creare ed eseguire un servizio di precompilazione {#create-and-run-a-prefill-service}

Il servizio di precompilazione è un servizio OSGi e viene fornito tramite il pacchetto OSGi. Potete creare il bundle OSGi, caricarlo e installarlo  bundle AEM Forms. Prima di iniziare a creare il bundle:

* [Download dell&#39;SDK del client AEM Forms ](https://helpx.adobe.com/it/aem-forms/kb/aem-forms-releases.html)
* Scarica il pacchetto ricorrenti

* Inserire il file di dati (dati di precompilazione) nell&#39;archivio crx. È possibile posizionare il file in qualsiasi posizione nella cartella \contents di crx-repository.

[Ottieni file](assets/prefill-sumbit-xmlsandcontentpackage.zip)

#### Creare un servizio di precompilazione {#create-a-prefill-service}

Il pacchetto standard (pacchetto del servizio di precompilazione di esempio) contiene un esempio di implementazione  servizio di precompilazione AEM Forms. Aprite il pacchetto ricorrenti in un editor di codice. Ad esempio, apri il progetto ricorrenti in Eclipse per la modifica. Dopo aver aperto il pacchetto standard in un editor di codice, eseguite i seguenti passaggi per creare il servizio.

1. Aprite il file src\main\java\com\adobe\test\Prefill.java per la modifica.
1. Nel codice, imposta il valore di:

   * `nodePath:` La variabile del percorso del nodo che punta alla posizione del repository crx contiene il percorso del file di dati (precompila). Ad esempio, /content/prefilldata.xml
   * `label:` Il parametro label specifica il nome visualizzato del servizio. Ad esempio, Prefill Service predefinito

1. Salvate e chiudete il file `Prefill.java`.
1. Aggiungete il pacchetto `AEM Forms Client SDK` al percorso di compilazione del progetto ricorrenti.
1. Compilate il progetto e create il .jar per il bundle.

#### Avviare e utilizzare il servizio di precompilazione {#start-and-use-the-prefill-service}

Per avviare il servizio di precompilazione, caricate il file JAR  AEM Forms Web Console e attivate il servizio. Ora, il servizio inizia a comparire nell&#39;editor di moduli adattivi. Per associare un servizio di precompilazione a un modulo adattivo:

1. Aprire il modulo adattivo in Forms Editor e aprire il pannello Proprietà per il contenitore del modulo.
1. Nella console Proprietà, accedete a  contenitore AEM Forms > Base > Precompila servizio.
1. Selezionate il servizio di precompilazione predefinito e fate clic su **[!UICONTROL Salva]**. Il servizio è associato al modulo.

## Precompilare i dati nel client {#prefill-at-client}

Quando si precompila un modulo adattivo, il server AEM Forms  unisce i dati a un modulo adattivo e invia il modulo compilato. Per impostazione predefinita, l&#39;azione di unione dei dati viene eseguita sul server.

È possibile configurare il server AEM Forms  per eseguire l&#39;azione di unione dati sul client anziché sul server. Riduce notevolmente il tempo necessario per precompilare ed eseguire il rendering dei moduli adattivi. Per impostazione predefinita, la funzione è disattivata. È possibile attivarla da Gestione configurazione o dalla riga di comando.

* Per attivare o disattivare da Gestione configurazione:
   1. Aprite AEM Configuration Manager.
   1. Individuare e aprire la configurazione del canale Web per moduli adattivi e comunicazioni interattive
   1. Abilitate l’opzione Configuration.af.clientside.datamerge.enabled.name
* Per abilitare o disabilitare dalla riga di comando:
   * Per attivare, eseguite il seguente comando cURL:
      `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=true \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`

   * Per disattivare, eseguite il seguente comando cURL:
      `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=false \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`
   Per sfruttare appieno l&#39;opzione di precompilazione dei dati in corrispondenza del client, aggiornate il servizio di precompilazione in modo che restituisca [FileAttachmentMap](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html) e [CustomContext](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html)