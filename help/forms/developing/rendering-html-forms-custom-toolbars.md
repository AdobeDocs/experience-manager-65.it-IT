---
title: Rendering di moduli HTML con barre degli strumenti personalizzate
seo-title: Rendering di moduli HTML con barre degli strumenti personalizzate
description: 'null'
seo-description: 'null'
uuid: b9c9464e-ff19-4051-a39b-4ec71c512d10
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 7eb0e8a8-d76a-43f7-a012-c21157b14cd4
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2304'
ht-degree: 0%

---


# Rendering di moduli HTML con barre degli strumenti personalizzate {#rendering-html-forms-with-customtoolbars}

## Rendering di moduli HTML con barre degli strumenti personalizzate {#rendering-html-forms-with-custom-toolbars}

Il servizio Forms consente di personalizzare una barra degli strumenti rappresentata con un modulo HTML. È possibile personalizzare una barra degli strumenti per modificarne l&#39;aspetto sovrascrivendo gli stili CSS predefiniti e per aggiungere un comportamento dinamico sovrascrivendo gli script Java. Una barra degli strumenti è personalizzata utilizzando un file XML denominato fscmenu.xml. Per impostazione predefinita, il servizio Forms recupera il file da una posizione URI specificata internamente.

>[!NOTE]
>
>Questa posizione URI si trova nel file adobe-forms-core.jar, che si trova nel file adobe-forms-dsc.jar. Il file adobe-forms-dsc.jar si trova in C:\Adobe\Adobe_Experience_Manager_forms\ folder (C:\ is the installation directory). Potete utilizzare uno strumento di estrazione file, ad esempio Win RAR, per aprire l&#39;adobe.

Potete copiare il file fscmenu.xml da questa posizione, modificarlo per soddisfare i requisiti, quindi inserirlo in una posizione URI personalizzata. Quindi, utilizzando l&#39;API Forms Service, impostare le opzioni di esecuzione che determinano l&#39;utilizzo del servizio Forms da parte del file fscmenu.xml dal percorso specificato. Queste azioni consentono al servizio Forms di eseguire il rendering di un modulo HTML con una barra degli strumenti personalizzata.

Oltre al file fscmenu.xml, dovete anche ottenere i file seguenti:

* fscmenu.js
* fscattachments.js
* fscmenu.css
* fscmenu-v.css
* fscmenu-ie.css
* fscdialog.css

fscJS è lo script Java associato a ciascun nodo. È necessario fornire uno per il `div#fscmenu` nodo ed eventualmente per `ul#fscmenuItem` i nodi. I file JS implementano la funzionalità di base della barra degli strumenti e i file predefiniti funzionano.

fscCSS è un foglio di stile associato a un particolare nodo. Gli stili nei file CSS specificano l&#39;aspetto della barra degli strumenti. *fscVCSS* è un foglio di stile per una barra degli strumenti verticale, che viene visualizzata a sinistra del modulo HTML di cui è stato effettuato il rendering. *fscIECSS* è un foglio di stile utilizzato per i moduli HTML di cui viene eseguito il rendering in Internet Explorer.

Verificate che tutti i file di cui sopra siano citati nel file fscmenu.xml. In altre parole, nel file fscmenu.xml, specificate i percorsi URI in modo che il servizio Forms possa individuarli. Per impostazione predefinita, questi file sono disponibili nelle posizioni URI a partire da parole chiave interne `FSWebRoot` o `ApplicationWebRoot`.

Per personalizzare la barra degli strumenti, sostituire le parole chiave utilizzando la parola chiave esterna `FSToolBarURI`. Questa parola chiave rappresenta l’URI passato al servizio Forms in fase di esecuzione (questo approccio è illustrato più avanti in questa sezione).

Potete anche specificare le posizioni assolute di questi file JS e CSS, ad esempio https://www.mycompany.com/scripts/misc/fscmenu.js. In questa situazione, non è necessario utilizzare la `FSToolBarURI` parola chiave.

>[!NOTE]
>
>Non è consigliabile utilizzare diversi metodi per fare riferimento a tali file. In altre parole, tutti gli URI devono essere citati utilizzando la `FSToolBarURI` parola chiave o una posizione assoluta.

Per ottenere i file JS e CSS, aprite il file adobe-forms-&lt;appserver>.ear. All&#39;interno di questo file, apri adobe-forms-res.war. Tutti questi file si trovano nel file WAR. Il file adobe-forms-&lt;appserver>.ear si trova nella cartella di installazione dei moduli AEM (C:\ is the installation directory). È possibile aprire adobe-forms-&lt;appserver>.ear utilizzando uno strumento di estrazione file come WinRAR.

La sintassi XML seguente mostra un file fscmenu.xml di esempio.

```html
 <div id="fscmenu" fscJS="FSToolBarURI/scripts/fscmenu.js" fscCSS="FSToolBarURI/fscmenu.css" fscVCSS="FSToolBarURI/fscmenu-v.css" fscIECSS="FSToolBarURI/fscmenu-ie.css">
         <ul class="fscmenuItem" id="Home">
             <li>
                 <a href="#" fscTarget="_top" tabindex="1">Home</a>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Upload" fscJS="FSToolBarURI/scripts/fscattachments.js" fscCSS="FSToolBarURI/fscdialog.css">
             <li>
                 <a tabindex="2">Upload Attachments</a>
                 <ul class="fscmenuPopup" id="fscUploadAttachments">
                     <li>
                         <a href="javascript:doUploadDialog();" tabindex="3">Add ...</a>
                     </li>
                     <li>
                         <a href="javascript:doDeleteDialog();" tabindex="4">Delete ...</a>
                     </li>
                 </ul>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Download">
             <li>
                 <a tabindex="100">Download Attachments</a>
                 <ul class="fscmenuPopup">
                     <li>
                         <a tabindex="101">None available</a>
                     </li>
                 </ul>
             </li>
         </ul>
     </div>
```

>[!NOTE]
>
>Il testo in grassetto rappresenta gli URI dei file CSS e JS a cui è necessario fare riferimento.

Gli elementi seguenti descrivono come personalizzare una barra degli strumenti:

* Modificate i valori degli attributi `fscJS`, `fscCSS`, `fscVCSS`, `fscIECSS` (nel file fscmenu.xml) per riflettere le posizioni personalizzate dei file a cui viene fatto riferimento, utilizzando uno dei metodi descritti in questa sezione (ad esempio, `fscJS="FSToolBarURI/scripts/fscmenu.js"`).
* Devono essere specificati tutti i file CSS e JS. Se nessuno dei file viene modificato, immettete quello predefinito nel percorso personalizzato. Potete ottenere i file predefiniti aprendo vari file come descritto in questa sezione.
* È consentito fornire un riferimento assoluto (ad esempio, https://www.example.com/scripts/custom-vertical-fscmenu.css) per qualsiasi file.
* I file JS e CSS richiesti dal `div#fscmenu` nodo sono essenziali per la funzionalità della barra degli strumenti. I singoli `ul#fscmenuItem` nodi possono avere o meno file JS o CSS supportati.

**Modifica del valore locale**

Come parte della personalizzazione di una barra degli strumenti, è possibile modificare il valore delle impostazioni internazionali della barra degli strumenti. Ovvero, potete visualizzarlo in un&#39;altra lingua. L&#39;illustrazione seguente mostra una barra degli strumenti personalizzata visualizzata in francese.

>[!NOTE]
>
>Non è possibile creare una barra degli strumenti personalizzata in più lingue. Le barre degli strumenti non possono utilizzare file XML diversi in base alle impostazioni internazionali.

Per modificare il valore delle impostazioni internazionali di una barra degli strumenti, accertatevi che il file fscmenu.xml contenga la lingua da visualizzare. La sintassi XML seguente mostra il file fscmenu.xml utilizzato per visualizzare una barra degli strumenti francese.

```html
 <div id="fscmenu" fscJS="FSToolBarURI/scripts/fscmenu.js" fscCSS="FSToolBarURI/fscmenu.css" fscVCSS="FSToolBarURI/fscmenu-v.css" fscIECSS="FSToolBarURI/fscmenu-ie.css">
         <ul class="fscmenuItem" id="Home">
             <li>
                 <a href="#" fscTarget="_top" tabindex="1">Accueil</a>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Upload" fscJS="FSToolBarURI/scripts/fscattachments.js" fscCSS="FSToolBarURI/fscdialog.css">
             <li>
                 <a tabindex="2">Télécharger les pièces jointes</a>
                 <ul class="fscmenuPopup" id="fscUploadAttachments">
                     <li>
                         <a href="javascript:doUploadDialog();" tabindex="3">Ajouter...</a>
                     </li>
                     <li>
                         <a href="javascript:doDeleteDialog();" tabindex="4">Supprimer...</a>
                     </li>
                 </ul>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Download">
             <li>
                 <a tabindex="100">Télécharger les pièces jointes</a>
                 <ul class="fscmenuPopup">
                     <li>
                         <a tabindex="101">Aucune disponible</a>
                     </li>
                 </ul>
             </li>
         </ul>
     </div>
```

>[!NOTE]
>
>Gli avvii rapidi associati a questa sezione utilizzano questo file XML per visualizzare una barra degli strumenti personalizzata francese, come illustrato nell&#39;illustrazione precedente.

Inoltre, specificate un valore di impostazione internazionale valido richiamando il metodo dell&#39; `HTMLRenderSpec` oggetto `setLocale` e passando un valore di stringa che specifica il valore di impostazione internazionale. Ad esempio, passare `fr_FR` per specificare il francese. Il servizio Forms è fornito di barre degli strumenti localizzate.

>[!NOTE]
>
>Prima di eseguire il rendering di un modulo HTML che utilizza una barra degli strumenti personalizzata, è necessario conoscere il rendering dei moduli HTML. (Vedere [Rendering dei moduli come HTML](/help/forms/developing/rendering-forms-html.md).)

Per ulteriori informazioni sul servizio Forms, vedere Riferimento [servizi per gli AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per eseguire il rendering di un modulo HTML che contiene una barra degli strumenti personalizzata, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto API Java di Forms.
1. Fate riferimento a un file XML personalizzato del menu di scelta rapida.
1. Eseguire il rendering di un modulo HTML.
1. Scrivere il flusso di dati del modulo nel browser Web del client.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, includete i file proxy.

**Creare un oggetto API Java Forms**

Prima di eseguire un&#39;operazione supportata dal servizio Forms a livello di programmazione, è necessario creare un oggetto client Forms.

**Riferimento a un file XML personalizzato di fscmenu**

Per eseguire il rendering di un modulo HTML che contiene una barra degli strumenti personalizzata, fare riferimento a un file XML fscmenu che descrive la barra degli strumenti. In questa sezione sono riportati due esempi di un file XML fscmenu. Inoltre, accertatevi che il file fscmenu.xml specifichi correttamente le posizioni di tutti i file di riferimento. Come indicato in precedenza in questa sezione, accertatevi che a tutti i file facciano riferimento la parola chiave o le relative posizioni assolute. `FSToolBarURI`

**Eseguire il rendering di un modulo HTML**

Per eseguire il rendering di un modulo HTML, specificare una struttura del modulo creata in Designer e salvata come file XDP. Selezionare anche un tipo di trasformazione HTML. Ad esempio, potete specificare il tipo di trasformazione HTML che esegue il rendering di un HTML dinamico per Internet Explorer 5.0 o versione successiva.

Il rendering di un modulo HTML richiede anche valori, ad esempio valori URI per il rendering di altri tipi di modulo.

**Scrivere il flusso di dati del modulo nel browser Web del client**

Quando il servizio Forms esegue il rendering di un modulo HTML, restituisce un flusso di dati del modulo che è necessario scrivere nel browser Web del client per rendere il modulo HTML visibile agli utenti.

**Consulta anche**

[Rendering di un modulo HTML con una barra degli strumenti personalizzata tramite l&#39;API Java](#render-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Rendering di un modulo HTML con una barra degli strumenti personalizzata tramite l&#39;API del servizio Web](#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido dell&#39;API di Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendering di PDF forms interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Rendering dei moduli come HTML](/help/forms/developing/rendering-forms-html.md)

[Creazione di applicazioni Web per il rendering di moduli](/help/forms/developing/creating-web-applications-renders-forms.md)

### Rendering di un modulo HTML con una barra degli strumenti personalizzata tramite l&#39;API Java {#render-an-html-form-with-a-custom-toolbar-using-the-java-api}

Eseguire il rendering di un modulo HTML contenente una barra degli strumenti personalizzata utilizzando l&#39;API Forms Service (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API Java Forms

   * Creare un `ServiceClientFactory` oggetto che contenga proprietà di connessione.
   * Creare un `FormsServiceClient` oggetto utilizzando il relativo costruttore e passando l&#39; `ServiceClientFactory` oggetto.

1. Riferimento a un file XML personalizzato di fscmenu

   * Creare un `HTMLRenderSpec` oggetto utilizzando il relativo costruttore.
   * Per eseguire il rendering di un modulo HTML con una barra degli strumenti, richiamare il metodo dell&#39; `HTMLRenderSpec` oggetto `setHTMLToolbar` e passare un valore `HTMLToolbar` enum. Ad esempio, per visualizzare una barra degli strumenti HTML verticale, passare `HTMLToolbar.Vertical`.
   * Specificare la posizione del file XML fscmenu richiamando il metodo dell&#39; `HTMLRenderSpec` oggetto `setToolbarURI` e passando un valore di stringa che specifica la posizione URI del file XML.
   * Se applicabile, impostare il valore delle impostazioni internazionali richiamando il metodo dell&#39; `HTMLRenderSpec` `setLocale` oggetto e passando un valore di stringa che specifica il valore delle impostazioni internazionali. Il valore predefinito è Inglese.

   >[!NOTE]
   >
   >Gli avvii rapidi associati a questa sezione impostano questo valore su `fr_FR`*.*

1. Eseguire il rendering di un modulo HTML

   Richiama il metodo dell’ `FormsServiceClient` oggetto `renderHTMLForm` e passa i seguenti valori:

   * Una stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, è necessario specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un valore `TransformTo` enum che specifica il tipo di preferenza HTML. Ad esempio, per eseguire il rendering di un modulo HTML compatibile con HTML dinamico per Internet Explorer 5.0 o versione successiva, specificare `TransformTo.MSDHTML`.
   * Un `com.adobe.idp.Document` oggetto che contiene i dati da unire al modulo. Se non si desidera unire i dati, passare un `com.adobe.idp.Document` oggetto vuoto.
   * L&#39; `HTMLRenderSpec` oggetto che memorizza le opzioni di runtime HTML.
   * Una stringa che specifica il valore dell&#39; `HTTP_USER_AGENT` intestazione, ad esempio `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * Un `URLSpec` oggetto che memorizza i valori URI necessari per eseguire il rendering di un modulo HTML.
   * Un `java.util.HashMap` oggetto che memorizza gli allegati. Si tratta di un parametro facoltativo e è possibile specificare `null` se non si desidera allegare file al modulo.

   Il `renderHTMLForm` metodo restituisce un `FormsResult` oggetto che contiene un flusso di dati del modulo che deve essere scritto nel browser Web del client.

1. Scrivere il flusso di dati del modulo nel browser Web del client

   * Creare un `com.adobe.idp.Document` oggetto richiamando il `FormsResult` metodo ‘s `getOutputContent` .
   * Ottenere il tipo di contenuto dell&#39; `com.adobe.idp.Document` oggetto richiamandone il `getContentType` metodo.
   * Impostare il tipo di contenuto dell&#39; `javax.servlet.http.HttpServletResponse` oggetto richiamandone `setContentType` il metodo e passando il tipo di contenuto dell&#39; `com.adobe.idp.Document` oggetto.
   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser Web del client richiamando il metodo dell&#39; `javax.servlet.http.HttpServletResponse` oggetto `getOutputStream` .
   * Creare un `java.io.InputStream` oggetto richiamando il `com.adobe.idp.Document` metodo dell&#39; `getInputStream` oggetto.
   * Creare un array di byte e compilarlo con il flusso di dati del modulo richiamando il metodo dell&#39; `InputStream` oggetto `read` e passando l&#39;array di byte come argomento.
   * Richiamare il metodo dell&#39; `javax.servlet.ServletOutputStream` oggetto `write` per inviare il flusso di dati del modulo al browser Web del client. Passa l&#39;array di byte al `write` metodo.

**Consulta anche**

[Avvio rapido (modalità SOAP): Rendering di un modulo HTML con una barra degli strumenti personalizzata tramite l&#39;API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Inclusione di file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rendering di un modulo HTML con una barra degli strumenti personalizzata tramite l&#39;API del servizio Web {#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api}

Eseguire il rendering di un modulo HTML che contiene una barra degli strumenti personalizzata utilizzando l&#39;API di Forms Service (servizio Web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il WSDL del servizio Forms.
   * Includete le classi proxy Java nel percorso della classe.

1. Creare un oggetto API Java Forms

   Creare un `FormsService` oggetto e impostare i valori di autenticazione.

1. Riferimento a un file XML personalizzato di fscmenu

   * Creare un `HTMLRenderSpec` oggetto utilizzando il relativo costruttore.
   * Per eseguire il rendering di un modulo HTML con una barra degli strumenti, richiamare il metodo dell&#39; `HTMLRenderSpec` oggetto `setHTMLToolbar` e passare un valore `HTMLToolbar` enum. Ad esempio, per visualizzare una barra degli strumenti HTML verticale, passare `HTMLToolbar.Vertical`.
   * Specificare la posizione del file XML fscmenu richiamando il metodo dell&#39; `HTMLRenderSpec` oggetto `setToolbarURI` e passando un valore di stringa che specifica la posizione URI del file XML.
   * Se applicabile, impostare il valore delle impostazioni internazionali richiamando il metodo dell&#39; `HTMLRenderSpec` `setLocale` oggetto e passando un valore di stringa che specifica il valore delle impostazioni internazionali. Il valore predefinito è Inglese.

   >[!NOTE]
   >
   >Gli avvii rapidi associati a questa sezione impostano questo valore su `fr_FR`*.*

1. Eseguire il rendering di un modulo HTML

   Richiama il metodo dell’ `FormsService` oggetto `renderHTMLForm` e passa i seguenti valori:

   * Una stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, è necessario specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un valore `TransformTo` enum che specifica il tipo di preferenza HTML. Ad esempio, per eseguire il rendering di un modulo HTML compatibile con HTML dinamico per Internet Explorer 5.0 o versione successiva, specificare `TransformTo.MSDHTML`.
   * Un `BLOB` oggetto che contiene i dati da unire al modulo. Se non si desidera unire i dati, passare `null`.
   * L&#39; `HTMLRenderSpec` oggetto che memorizza le opzioni di runtime HTML.
   * Un valore di stringa che specifica il valore dell&#39; `HTTP_USER_AGENT` intestazione, ad esempio `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322`). Se non si desidera impostare questo valore, è possibile passare una stringa vuota.
   * Un `URLSpec` oggetto che memorizza i valori URI necessari per eseguire il rendering di un modulo HTML.
   * Un `java.util.HashMap` oggetto che memorizza gli allegati. Questo parametro è facoltativo e si può specificare `null` se non si desidera allegare file al modulo.
   * Un oggetto vuoto `com.adobe.idp.services.holders.BLOBHolder` compilato dal `renderHTMLForm` metodo. Questo valore del parametro memorizza il modulo di cui è stato effettuato il rendering.
   * Un oggetto vuoto `com.adobe.idp.services.holders.BLOBHolder` compilato dal `renderHTMLForm` metodo. Questo parametro memorizza i dati XML di output.
   * Un oggetto vuoto `javax.xml.rpc.holders.LongHolder` compilato dal `renderHTMLForm` metodo. Questo argomento memorizza il numero di pagine nel modulo.
   * Un oggetto vuoto `javax.xml.rpc.holders.StringHolder` compilato dal `renderHTMLForm` metodo. Questo argomento memorizza il valore delle impostazioni internazionali.
   * Un oggetto vuoto `javax.xml.rpc.holders.StringHolder` compilato dal `renderHTMLForm` metodo. Questo argomento memorizza il valore di rendering HTML utilizzato.
   * Un oggetto vuoto `com.adobe.idp.services.holders.FormsResultHolder` che conterrà i risultati dell&#39;operazione.

   Il `renderHTMLForm` metodo compila l&#39; `com.adobe.idp.services.holders.FormsResultHolder` oggetto passato come valore dell&#39;ultimo argomento con un flusso di dati del modulo che deve essere scritto nel browser Web del client.

1. Scrivere il flusso di dati del modulo nel browser Web del client

   * Creare un `FormResult` oggetto ottenendo il valore del membro `com.adobe.idp.services.holders.FormsResultHolder` dati dell&#39; `value` oggetto.
   * Creare un `BLOB` oggetto che contenga dati del modulo richiamando il `FormsResult` metodo dell&#39; `getOutputContent` oggetto.
   * Ottenere il tipo di contenuto dell&#39; `BLOB` oggetto richiamandone il `getContentType` metodo.
   * Impostare il tipo di contenuto dell&#39; `javax.servlet.http.HttpServletResponse` oggetto richiamandone `setContentType` il metodo e passando il tipo di contenuto dell&#39; `BLOB` oggetto.
   * Creare un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser Web del client richiamando il metodo dell&#39; `javax.servlet.http.HttpServletResponse` oggetto `getOutputStream` .
   * Creare un array di byte e compilarlo richiamando il metodo dell&#39; `BLOB` oggetto `getBinaryData` . Questa attività assegna il contenuto dell&#39; `FormsResult` oggetto all&#39;array di byte.
   * Richiamare il metodo dell&#39; `javax.servlet.http.HttpServletResponse` oggetto `write` per inviare il flusso di dati del modulo al browser Web del client. Passa l&#39;array di byte al `write` metodo.

**Consulta anche**

[Chiamata di AEM Forms mediante codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
