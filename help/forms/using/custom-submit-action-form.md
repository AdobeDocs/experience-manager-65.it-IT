---
title: Scrittura di un'azione di invio personalizzata per i moduli adattivi
seo-title: Scrittura di un'azione di invio personalizzata per i moduli adattivi
description: ' AEM Forms consente di creare un''azione di invio personalizzata per i moduli adattivi. Questo articolo descrive la procedura per aggiungere un''azione Invia personalizzata per i moduli adattivi.'
seo-description: ' AEM Forms consente di creare un''azione di invio personalizzata per i moduli adattivi. Questo articolo descrive la procedura per aggiungere un''azione Invia personalizzata per i moduli adattivi.'
uuid: fd8e1dac-b997-4e86-aaf6-3507edcb3070
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 2a2e1156-4a54-4b0a-981c-d527fe22a27e
docset: aem65
translation-type: tm+mt
source-git-commit: a399b2cb2e0ae4f045f7e0fddf378fdcd80bb848
workflow-type: tm+mt
source-wordcount: '1661'
ht-degree: 0%

---


# Scrittura di un&#39;azione di invio personalizzata per i moduli adattivi{#writing-custom-submit-action-for-adaptive-forms}

I moduli adattivi richiedono azioni di invio per elaborare i dati specificati dall&#39;utente. Un&#39;azione Invia determina l&#39;attività eseguita sui dati inviati utilizzando un modulo adattivo. Adobe Experience Manager (AEM) include [Azioni di invio OOTB](../../forms/using/configuring-submit-actions.md) che illustrano le attività personalizzate che è possibile eseguire utilizzando i dati inviati dall&#39;utente. Ad esempio, è possibile eseguire attività quali inviare e-mail o memorizzare i dati.

## Flusso di lavoro per un&#39;azione di invio {#workflow-for-a-submit-action}

Il diagramma di flusso rappresenta il flusso di lavoro per un&#39;azione di invio che viene attivata quando si fa clic sul pulsante **[!UICONTROL Invia]** in un modulo adattivo. I file nel componente File allegato vengono caricati sul server e i dati del modulo vengono aggiornati con gli URL dei file caricati. All&#39;interno del client, i dati vengono memorizzati nel formato JSON. Il client invia una richiesta Ajax a un servlet interno che massaggia i dati specificati e li restituisce in formato XML. Il client raccoglie questi dati con i campi delle azioni. Invia i dati al servlet finale (servlet di invio guida) tramite un&#39;azione di invio del modulo. Quindi, il servlet inoltra il controllo all&#39;azione Invia. L’azione Invia può inoltrare la richiesta a un’altra risorsa sling oppure reindirizzare il browser a un altro URL.

![Diagramma di flusso che illustra il flusso di lavoro per l’azione Invia](assets/diagram1.png)

### Formato dati XML {#xml-data-format}

I dati XML vengono inviati al servlet utilizzando il parametro di richiesta **`jcr:data`**. Le azioni di invio possono accedere al parametro per elaborare i dati. Il codice seguente descrive il formato dei dati XML. I campi associati al modello Modulo vengono visualizzati nella sezione **`afBoundData`**. I campi non associati vengono visualizzati nella sezione `afUnoundData`. Per ulteriori informazioni sul formato del file `data.xml`, vedere [Introduzione alla precompilazione dei campi modulo adattivo](../../forms/using/prepopulate-adaptive-form-fields.md).

```xml
<?xml ?>
<afData>
<afUnboundData>
<data>
<field1>value</field2>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
<repeatablePanel>
    <field2>value</field2>
</repeatablePanel>
</data>
</afUnboundData>
<afBoundData>
<!-- xml corresponding to the Form Model /XML Schema -->
</afBoundData>
</afData>
```

### Campi azione {#action-fields}

Un&#39;azione Invia può aggiungere campi di input nascosti (utilizzando il tag HTML [input](https://developer.mozilla.org/en/docs/Web/HTML/Element/Input)) al modulo HTML di cui è stato effettuato il rendering. Questi campi nascosti possono contenere valori necessari durante l&#39;elaborazione dell&#39;invio del modulo. Quando si invia il modulo, questi valori dei campi vengono riportati come parametri di richiesta che l&#39;azione Invia può utilizzare durante la gestione dell&#39;invio. I campi di input sono denominati campi azione.

Ad esempio, un&#39;azione Invia che acquisisce anche il tempo necessario per compilare un modulo può aggiungere i campi di input nascosti `startTime` e `endTime`.

Uno script può fornire i valori dei campi `startTime` e `endTime` rispettivamente durante il rendering del modulo e prima dell&#39;invio. Lo script di azione Invia `post.jsp` può quindi accedere a questi campi utilizzando i parametri della richiesta e calcolare il tempo totale necessario per compilare il modulo.

### Allegati file {#file-attachments}

Le azioni di invio possono inoltre utilizzare gli allegati caricati mediante il componente File allegato. Gli script di azione Invia possono accedere a questi file utilizzando l&#39;API sling [RequestParameter](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html). Il metodo [isFormField](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#isFormField()) dell&#39;API consente di identificare se il parametro della richiesta è un file o un campo del modulo. È possibile iterare i parametri Request in un&#39;azione Submit per identificare i parametri File Attachment.

Il seguente codice di esempio identifica gli allegati nella richiesta. Successivamente, legge i dati nel file utilizzando l&#39; [Get API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/request/RequestParameter.html#get()). Infine, crea un oggetto Document utilizzando i dati e lo aggiunge a un elenco.

```java
RequestParameterMap requestParameterMap = slingRequest.getRequestParameterMap();
for (Map.Entry<String, RequestParameter[]> param : requestParameterMap.entrySet()) {
    RequestParameter rpm = param.getValue()[0];
    if(!rpm.isFormField()) {
        fileAttachments.add(new Document(rpm.get()));
    }
}
```

### Percorso avanti e URL di reindirizzamento {#forward-path-and-redirect-url}

Dopo aver eseguito l’azione richiesta, il servlet Invia inoltra la richiesta al percorso successivo. Un&#39;azione utilizza l&#39;API setForwardPath per impostare il percorso in avanti nel servlet di invio della guida.

Se l’azione non fornisce un percorso in avanti, il servlet Invia reindirizzerà il browser utilizzando l’URL di reindirizzamento. L’autore configura l’URL di reindirizzamento utilizzando la configurazione Pagina di ringraziamento nella finestra di dialogo Modifica modulo adattivo. Potete inoltre configurare l’URL di reindirizzamento mediante l’azione Invia o l’API setRedirectUrl nel servlet di invio della guida. Potete inoltre configurare i parametri Request inviati all’URL Redirect utilizzando l’API setRedirectParameters nel servlet Guide Submit.

>[!NOTE]
>
>Un autore fornisce l’URL di reindirizzamento (utilizzando la configurazione della pagina di ringraziamento). [Le ](../../forms/using/configuring-submit-actions.md) azioni di invio OOTB utilizzano l&#39;URL di reindirizzamento per reindirizzare il browser dalla risorsa a cui fa riferimento il percorso successivo.
>
>È possibile scrivere un&#39;azione di invio personalizzata per inoltrare una richiesta a una risorsa o a un servlet.  Adobe consiglia che lo script che esegue la gestione delle risorse per il percorso successivo reindirizzi la richiesta all&#39;URL di reindirizzamento al termine dell&#39;elaborazione.

## Invia azione {#submit-action}

Un’azione Invia è una sling:Folder che include quanto segue:

* **addfields.jsp**: Questo script fornisce i campi di azione che vengono aggiunti al file HTML durante la rappresentazione. Utilizzare questo script per aggiungere i parametri di input nascosti richiesti durante l&#39;invio nello script post.POST.jsp.
* **dialog.xml**: Questo script è simile alla finestra di dialogo del componente CQ. Fornisce informazioni di configurazione personalizzate dall’autore. I campi vengono visualizzati nella scheda Azioni invio della finestra di dialogo Modifica modulo adattivo quando si seleziona l&#39;azione Invia.
* **post.POST.jsp**: Il servlet di invio richiama questo script con i dati inviati e i dati aggiuntivi nelle sezioni precedenti. Qualsiasi riferimento all&#39;esecuzione di un&#39;azione in questa pagina implica l&#39;esecuzione dello script post.POST.jsp. Per registrare l’azione Invia con i moduli adattivi da visualizzare nella finestra di dialogo Modifica modulo adattivo, aggiungere le seguenti proprietà a sling:Folder:

   * **** guideComponentType String e value  **fd/af/components/guidesubmittype**
   * **** guideDataModelof type String che specifica il tipo di modulo adattivo per il quale è applicabile l&#39;azione Invia. **xfais** supportato per i moduli adattivi basati su XFA, mentre  **** xsdis è supportato per i moduli adattivi basati su XSD. **Le** origini sono supportate per i moduli adattivi che non utilizzano XDP o XSD. Per visualizzare l&#39;azione su più tipi di moduli adattivi, aggiungere le stringhe corrispondenti. Separate ogni stringa con una virgola. Ad esempio, per rendere visibile un&#39;azione nei moduli adattivi basati su XFA e XSD, specificare i valori **xfa** e **xsd** rispettivamente.

   * **jcr:** description di tipo String. Il valore di questa proprietà viene visualizzato nell&#39;elenco delle azioni di invio nella scheda Azioni di invio della finestra di dialogo Modifica modulo adattivo. Le azioni OOTB sono presenti nell&#39;archivio CRX nel percorso **/libs/fd/af/components/guidesubmittype**.

## Creazione di un&#39;azione di invio personalizzata {#creating-a-custom-submit-action}

Effettuare le seguenti operazioni per creare un&#39;azione Invia personalizzata che salva i dati nell&#39;archivio CRX e quindi invia un&#39;e-mail. Il modulo adattivo contiene il contenuto OOTB Submit action Store (obsoleto) che salva i dati nell&#39;archivio CRX. CQ fornisce inoltre un&#39;API [Mail](https://docs.adobe.com/docs/en/cq/current/javadoc/com/day/cq/mailer/package-summary.html) che può essere utilizzata per inviare e-mail. Prima di utilizzare l&#39;API Mail, [configurare](https://docs.adobe.com/docs/en/cq/current/administering/notification.html?wcmmode=disabled#Configuring the Mail Service) il servizio Day CQ Mail tramite la console di sistema. È possibile riutilizzare l&#39;azione Archivia contenuto (obsoleto) per memorizzare i dati nella directory archivio. L’azione Contenuto store (obsoleto) è disponibile nel percorso /libs/fd/af/components/guidesubmittype/store dell’archivio CRX.

1. Accedete al CRXDE Lite all&#39;URL https://&lt;server>:&lt;porta>/crx/de/index.jsp. Create un nodo con la proprietà sling:Folder e name store_and_mail nella cartella /apps/custom_submit_action. Create la cartella custom_submit_action se non esiste già.

   ![Screenshot raffigurante la creazione di un nodo con la proprietà sling:Folder](assets/step1.png)

1. **Immettete i campi di configurazione obbligatori.**

   Aggiungete la configurazione necessaria per l&#39;azione Store. Copiate il nodo **cq:dialog** dell&#39;azione Store da /libs/fd/af/components/guidesubmittype/store nella cartella dell&#39;azione in /apps/custom_submit_action/store_and_email.

   ![Screenshot che mostra la copia del nodo della finestra di dialogo nella cartella action](assets/step2.png)

1. **Immettete i campi di configurazione per richiedere all’autore la configurazione dell’e-mail.**

   Il modulo adattivo fornisce inoltre un&#39;azione E-mail che invia messaggi e-mail agli utenti. Personalizza questa azione in base alle tue esigenze. Andate a /libs/fd/af/components/guidesubmittype/email/dialog. Copiare i nodi all&#39;interno del nodo cq:dialog nel nodo cq:dialog dell&#39;azione di invio (/apps/custom_submit_action/store_and_email/dialog).

   ![Personalizzazione dell’azione e-mail](assets/step3.png)

1. **Rendete disponibile l’azione nella finestra di dialogo Modifica modulo adattivo.**

   Aggiungi le seguenti proprietà nel nodo store_and_email:

   * **** guideComponentType  **** Stringhe e value  **fd/af/components/guidesubmittype**

   * **** guideDataModeler di tipo  **** Stringling e valore  **xfa, xsd, di base**

   * **jcr:** descrizione di tipo  **** Stringhe e valore  **Store e Azione e-mail**

1. Aprire qualsiasi modulo adattivo. Fate clic sul pulsante **Modifica** accanto a **Avvia** per aprire la finestra di dialogo **Modifica** del contenitore di moduli adattivi. La nuova azione viene visualizzata nella scheda **Invia azioni**. Selezionando **Archivia e invia per e-mail azioni** viene visualizzata la configurazione aggiunta nel nodo della finestra di dialogo.

   ![Finestra di dialogo di configurazione dell&#39;azione Invia](assets/store_and_email_submit_action_dialog.jpg)

1. **Utilizzare l&#39;azione per completare un&#39;attività.**

   Aggiungere lo script post.POST.jsp all&#39;azione. (/apps/custom_submit_action/store_and_mail/).

   Eseguire l&#39;azione OOOTB Store (script post.POST.jsp). Utilizzate l&#39;API [FormsHelper.runAction](https://docs.adobe.com/docs/en/cq/current/javadoc/com/day/cq/wcm/foundation/forms/FormsHelper.html#runAction(java.lang.String, java.lang.String, org.apache.sling.api.resource.Resource, org.apache.sling.api.SlingHttpServletRequest, org.apache.sling.api.SlingHttpServletResponse) che CQ fornisce nel codice per eseguire l&#39;azione Store . Aggiungi il seguente codice nel file JSP:

   `FormsHelper.runAction("/libs/fd/af/components/guidesubmittype/store", "post", resource, slingRequest, slingResponse);`

   Per inviare l&#39;e-mail, il codice legge l&#39;indirizzo e-mail del destinatario dalla configurazione. Per recuperare il valore di configurazione nello script dell&#39;azione, leggere le proprietà della risorsa corrente utilizzando il codice seguente. Allo stesso modo, potete leggere gli altri file di configurazione.

   `ValueMap properties = ResourceUtil.getValueMap(resource);`

   `String mailTo = properties.get("mailTo");`

   Infine, utilizzate l&#39;API di CQ Mail per inviare l&#39;e-mail. Utilizzate la classe [SimpleEmail](https://commons.apache.org/proper/commons-email/apidocs/org/apache/commons/mail/SimpleEmail.html) per creare l&#39;oggetto Email come illustrato di seguito:

   >[!NOTE]
   >
   >Assicurarsi che il file JSP abbia il nome post.POST.jsp.

   ```java
   <%@include file="/libs/fd/af/components/guidesglobal.jsp" %>
   <%@page import="com.day.cq.wcm.foundation.forms.FormsHelper,
          org.apache.sling.api.resource.ResourceUtil,
          org.apache.sling.api.resource.ValueMap,
                   com.day.cq.mailer.MessageGatewayService,
     com.day.cq.mailer.MessageGateway,
     org.apache.commons.mail.Email,
                   org.apache.commons.mail.SimpleEmail" %>
   <%@taglib prefix="sling"
                   uri="https://sling.apache.org/taglibs/sling/1.0" %>
   <%@taglib prefix="cq"
                   uri="https://www.day.com/taglibs/cq/1.0"
   %>
   <cq:defineObjects/>
   <sling:defineObjects/>
   <%
           String storeContent =
                       "/libs/fd/af/components/guidesubmittype/store";
           FormsHelper.runAction(storeContent, "post", resource,
                                   slingRequest, slingResponse);
    ValueMap props = ResourceUtil.getValueMap(resource);
    Email email = new SimpleEmail();
    String[] mailTo = props.get("mailto", new String[0]);
    email.setFrom((String)props.get("from"));
           for (String toAddr : mailTo) {
               email.addTo(toAddr);
      }
    email.setMsg((String)props.get("template"));
    email.setSubject((String)props.get("subject"));
    MessageGatewayService messageGatewayService =
                       sling.getService(MessageGatewayService.class);
    MessageGateway messageGateway =
                   messageGatewayService.getGateway(SimpleEmail.class);
    messageGateway.send(email);
   %>
   ```

   Selezionate l’azione nel modulo adattivo. L’azione invia un messaggio e-mail e memorizza i dati.

