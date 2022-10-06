---
title: Rendering di HTML Forms con barre degli strumenti personalizzate
seo-title: Rendering HTML Forms with CustomToolbars
description: Utilizzare il servizio Forms per personalizzare una barra degli strumenti di cui è eseguito il rendering con un modulo HTML. È possibile eseguire il rendering di un modulo HTML con una barra degli strumenti personalizzata utilizzando l’API Java e un’API di servizio Web.
seo-description: Use the Forms service to customize a toolbar that is rendered with an HTML form. You can render an HTML Form with a custom toolbar using the Java API and a Web Service API.
uuid: b9c9464e-ff19-4051-a39b-4ec71c512d10
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 7eb0e8a8-d76a-43f7-a012-c21157b14cd4
role: Developer
exl-id: 0b992b1c-3878-447a-bccc-7034aa3e98bc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2345'
ht-degree: 0%

---

# Rendering di HTML Forms con barre degli strumenti personalizzate {#rendering-html-forms-with-customtoolbars}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

## Rendering di HTML Forms con barre degli strumenti personalizzate {#rendering-html-forms-with-custom-toolbars}

Il servizio Forms consente di personalizzare una barra degli strumenti di cui è eseguito il rendering con un modulo HTML. È possibile personalizzare una barra degli strumenti per modificarne l’aspetto ignorando gli stili CSS predefiniti e per aggiungere comportamenti dinamici ignorando gli script Java. Una barra degli strumenti viene personalizzata utilizzando un file XML denominato fscmenu.xml. Per impostazione predefinita, il servizio Forms recupera il file da una posizione URI specificata internamente.

>[!NOTE]
>
>Questa posizione URI si trova nel file adobe-forms-core.jar, che si trova nel file adobe-forms-dsc.jar . Il file adobe-forms-dsc.jar si trova in C:\Adobe\Adobe_Experience_Manager_forms\ folder (C:\ is the installation directory). Puoi utilizzare uno strumento di estrazione file, ad esempio Win RAR, per aprire adobe.

È possibile copiare il file fscmenu.xml da questa posizione, modificarlo per soddisfare le proprie esigenze e quindi inserirlo in una posizione URI personalizzata. Quindi, utilizzando l&#39;API del servizio Forms, imposta le opzioni di esecuzione che si traducono nel servizio Forms utilizzando il file fscmenu.xml dal percorso specificato. Queste azioni consentono al servizio Forms di eseguire il rendering di un modulo HTML con una barra degli strumenti personalizzata.

Oltre al file fscmenu.xml, è necessario ottenere anche i seguenti file:

* fscmenu.js
* fscattachments.js
* fscmenu.css
* fscmenu-v.css
* fscmenu-ie.css
* fscdialog.css

fscJS è lo script Java associato a ciascun nodo. È necessario fornire uno per il `div#fscmenu` nodo e facoltativamente per `ul#fscmenuItem` nodi. I file JS implementano la funzionalità di base della barra degli strumenti e i file predefiniti funzionano.

fscCSS è un foglio di stile associato a un particolare nodo. Gli stili nei file CSS specificano l’aspetto della barra degli strumenti. *fscVCSS* è un foglio di stile per una barra degli strumenti verticale, visualizzato a sinistra del modulo HTML di cui è stato effettuato il rendering. *fscIECSS* è un foglio di stile utilizzato per i moduli di HTML sottoposti a rendering in Internet Explorer.

Assicurati che tutti i file di cui sopra siano referenziati nel file fscmenu.xml. In altre parole, nel file fscmenu.xml, specifica le posizioni URI da cui puntare a questi file in modo che il servizio Forms possa individuarli. Per impostazione predefinita, questi file sono disponibili in posizioni URI che iniziano con parole chiave interne `FSWebRoot` o `ApplicationWebRoot`.

Per personalizzare la barra degli strumenti, sostituisci le parole chiave utilizzando la parola chiave esterna `FSToolBarURI`. Questa parola chiave rappresenta l’URI passato al servizio Forms in fase di esecuzione (questo approccio viene mostrato più avanti in questa sezione).

Puoi anche specificare le posizioni assolute di questi file JS e CSS, ad esempio https://www.mycompany.com/scripts/misc/fscmenu.js. In questa situazione, non è necessario utilizzare il `FSToolBarURI` keyword.

>[!NOTE]
>
>Si sconsiglia di combinare i modi in cui si fa riferimento a questi file. In altre parole, tutti gli URI devono essere referenziati utilizzando `FSToolBarURI` parola chiave o posizione assoluta.

Puoi ottenere i file JS e CSS aprendo adobe-forms-&lt;appserver>file .ear. All’interno di questo file, apri adobe-forms-res.war. Tutti questi file si trovano nel file WAR. Adobe-forms-&lt;appserver>Il file .ear si trova nella cartella di installazione dei moduli AEM (C:\ is the installation directory). Puoi aprire adobe-forms-&lt;appserver>.ear utilizzando uno strumento di estrazione file come WinRAR.

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

* Modificare i valori di `fscJS`, `fscCSS`, `fscVCSS`, `fscIECSS` attributi (nel file fscmenu.xml) per riflettere le posizioni personalizzate dei file a cui si fa riferimento utilizzando uno dei metodi descritti in questa sezione (ad esempio, `fscJS="FSToolBarURI/scripts/fscmenu.js"`).
* Tutti i file CSS e JS devono essere specificati. Se nessuno dei file viene modificato, inserisci quello predefinito nel percorso personalizzato. È possibile ottenere i file predefiniti aprendo vari file come descritto in questa sezione.
* È consentito fornire un riferimento assoluto (ad esempio, https://www.example.com/scripts/custom-vertical-fscmenu.css) per qualsiasi file.
* I file JS e CSS che `div#fscmenu` le richieste dei nodi sono essenziali per la funzionalità della barra degli strumenti. Individuale `ul#fscmenuItem` I nodi possono avere o meno file JS o CSS di supporto.

**Modifica del valore locale**

Per personalizzare una barra degli strumenti, puoi modificare il valore delle impostazioni internazionali della barra degli strumenti. Cioè, potete visualizzarlo in un&#39;altra lingua. La figura seguente mostra una barra degli strumenti personalizzata visualizzata in francese.

>[!NOTE]
>
>Non è possibile creare una barra degli strumenti personalizzata in più lingue. Le barre degli strumenti non possono utilizzare file XML diversi in base alle impostazioni internazionali.

Per modificare il valore delle impostazioni internazionali di una barra degli strumenti, assicurarsi che il file fscmenu.xml contenga la lingua che si desidera visualizzare. La sintassi XML seguente mostra il file fscmenu.xml utilizzato per visualizzare una barra degli strumenti francese.

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

Inoltre, specifica un valore di impostazione internazionale valido richiamando il `HTMLRenderSpec` dell’oggetto `setLocale` e passare un valore stringa che specifica il valore delle impostazioni internazionali. Ad esempio, passa `fr_FR` per specificare il francese. Il servizio Forms è fornito con barre degli strumenti localizzate.

>[!NOTE]
>
>Prima di eseguire il rendering di un modulo HTML che utilizza una barra degli strumenti personalizzata, è necessario sapere come viene eseguito il rendering dei moduli di HTML. (Vedi [Rendering di Forms as HTML](/help/forms/developing/rendering-forms-html.md).)

Per ulteriori informazioni sul servizio Forms, vedi [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per eseguire il rendering di un modulo HTML contenente una barra degli strumenti personalizzata, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Crea un oggetto API Java Forms.
1. Fare riferimento a un file XML personalizzato fscmenu.
1. Eseguire il rendering di un modulo HTML.
1. Scrivere il flusso di dati del modulo sul browser Web client.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un&#39;applicazione client utilizzando Java, includi i file JAR necessari. Se utilizzi i servizi web, includi i file proxy.

**Creare un oggetto API Java di Forms**

Prima di poter eseguire in modo programmatico un’operazione supportata dal servizio Forms, è necessario creare un oggetto client Forms.

**Riferimento a un file XML personalizzato fscmenu**

Per eseguire il rendering di un modulo HTML contenente una barra degli strumenti personalizzata, fare riferimento a un file XML fscmenu che descrive la barra degli strumenti. (Questa sezione fornisce due esempi di un file XML fscmenu.) Inoltre, assicurati che il file fscmenu.xml specifichi correttamente le posizioni di tutti i file di riferimento. Come indicato in precedenza in questa sezione, assicurati che a tutti i file venga fatto riferimento da `FSToolBarURI` Parola chiave o le loro posizioni assolute.

**Rendering di un modulo HTML**

Per eseguire il rendering di un modulo HTML, specificare una struttura del modulo creata in Designer e salvata come file XDP. Selezionare anche un tipo di trasformazione HTML. Ad esempio, è possibile specificare il tipo di trasformazione HTML che esegue il rendering di un HTML dinamico per Internet Explorer 5.0 o versione successiva.

Il rendering di un modulo HTML richiede anche valori, ad esempio valori URI per il rendering di altri tipi di modulo.

**Scrivere il flusso di dati del modulo sul browser Web client**

Quando il servizio Forms esegue il rendering di un modulo HTML, restituisce un flusso di dati del modulo che è necessario scrivere nel browser Web del client per rendere il modulo HTML visibile agli utenti.

**Consulta anche**

[Eseguire il rendering di un modulo HTML con una barra degli strumenti personalizzata utilizzando l’API Java](#render-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Rendering di un modulo HTML con una barra degli strumenti personalizzata tramite l’API del servizio Web](#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendering di PDF forms interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Rendering di Forms as HTML](/help/forms/developing/rendering-forms-html.md)

[Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Eseguire il rendering di un modulo HTML con una barra degli strumenti personalizzata utilizzando l’API Java {#render-an-html-form-with-a-custom-toolbar-using-the-java-api}

Eseguire il rendering di un modulo HTML contenente una barra degli strumenti personalizzata utilizzando l’API del servizio Forms (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API Java di Forms

   * Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione.
   * Crea un `FormsServiceClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto.

1. Riferimento a un file XML personalizzato fscmenu

   * Crea un `HTMLRenderSpec` utilizzando il relativo costruttore.
   * Per eseguire il rendering di un modulo HTML con una barra degli strumenti, richiamare `HTMLRenderSpec` dell’oggetto `setHTMLToolbar` e passare un `HTMLToolbar` valore enum. Ad esempio, per visualizzare una barra degli strumenti verticale di HTML, passare `HTMLToolbar.Vertical`.
   * Specificare la posizione del file XML fscmenu richiamando il `HTMLRenderSpec` dell’oggetto `setToolbarURI` e passare un valore stringa che specifica la posizione URI del file XML.
   * Se applicabile, imposta il valore delle impostazioni internazionali richiamando il `HTMLRenderSpec` dell’oggetto `setLocale` e passare un valore stringa che specifica il valore delle impostazioni internazionali. Il valore predefinito è Inglese.

   >[!NOTE]
   >
   >Gli avvii rapidi associati a questa sezione impostano questo valore su `fr_FR`*.*

1. Rendering di un modulo HTML

   Richiama il `FormsServiceClient` dell’oggetto `renderHTMLForm` e passare i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, verificare di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` valore enum che specifica il tipo di preferenza HTML. Ad esempio, per eseguire il rendering di un modulo HTML compatibile con Dynamic HTML per Internet Explorer 5.0 o versione successiva, specificare `TransformTo.MSDHTML`.
   * A `com.adobe.idp.Document` oggetto contenente i dati da unire al modulo. Se non si desidera unire i dati, passare un valore vuoto `com.adobe.idp.Document` oggetto.
   * La `HTMLRenderSpec` oggetto che memorizza le opzioni di runtime di HTML.
   * Un valore stringa che specifica la variabile `HTTP_USER_AGENT` valore di intestazione, ad esempio `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * A `URLSpec` oggetto che memorizza i valori URI necessari per eseguire il rendering di un modulo HTML.
   * A `java.util.HashMap` oggetto che memorizza gli allegati di file. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.

   La `renderHTMLForm` restituisce un `FormsResult` oggetto che contiene un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo sul browser Web client

   * Crea un `com.adobe.idp.Document` richiamando l&#39;oggetto `FormsResult` oggetto ‘s `getOutputContent` metodo .
   * Ottieni il tipo di contenuto del `com.adobe.idp.Document` richiamandone l&#39;oggetto `getContentType` metodo .
   * Imposta la `javax.servlet.http.HttpServletResponse` tipo di contenuto dell’oggetto richiamandone il tipo `setContentType` e passare il tipo di contenuto `com.adobe.idp.Document` oggetto.
   * Crea un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il `javax.servlet.http.HttpServletResponse` dell’oggetto `getOutputStream` metodo .
   * Crea un `java.io.InputStream` richiamando l&#39;oggetto `com.adobe.idp.Document` dell’oggetto `getInputStream` metodo .
   * Creare un array di byte e compilarlo con il flusso di dati del modulo richiamando il `InputStream` dell’oggetto `read` e passare l&#39;array di byte come argomento.
   * Richiama il `javax.servlet.ServletOutputStream` dell’oggetto `write` per inviare il flusso di dati del modulo al browser Web client. Passa l&#39;array di byte al `write` metodo .

**Consulta anche**

[Avvio rapido (modalità SOAP): Rendering di un modulo HTML con una barra degli strumenti personalizzata tramite l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rendering di un modulo HTML con una barra degli strumenti personalizzata tramite l’API del servizio Web {#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api}

Eseguire il rendering di un modulo HTML contenente una barra degli strumenti personalizzata utilizzando l’API del servizio Forms (servizio Web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio WSDL di Forms.
   * Includi le classi proxy Java nel percorso della classe.

1. Creare un oggetto API Java di Forms

   Crea un `FormsService` e impostare i valori di autenticazione.

1. Riferimento a un file XML personalizzato fscmenu

   * Crea un `HTMLRenderSpec` utilizzando il relativo costruttore.
   * Per eseguire il rendering di un modulo HTML con una barra degli strumenti, richiamare `HTMLRenderSpec` dell’oggetto `setHTMLToolbar` e passare un `HTMLToolbar` valore enum. Ad esempio, per visualizzare una barra degli strumenti verticale di HTML, passare `HTMLToolbar.Vertical`.
   * Specificare la posizione del file XML fscmenu richiamando il `HTMLRenderSpec` dell’oggetto `setToolbarURI` e passare un valore stringa che specifica la posizione URI del file XML.
   * Se applicabile, imposta il valore delle impostazioni internazionali richiamando il `HTMLRenderSpec` dell’oggetto `setLocale` e passare un valore stringa che specifica il valore delle impostazioni internazionali. Il valore predefinito è Inglese.

   >[!NOTE]
   >
   >Gli avvii rapidi associati a questa sezione impostano questo valore su `fr_FR`*.*

1. Rendering di un modulo HTML

   Richiama il `FormsService` dell’oggetto `renderHTMLForm` e passare i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, verificare di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` valore enum che specifica il tipo di preferenza HTML. Ad esempio, per eseguire il rendering di un modulo HTML compatibile con Dynamic HTML per Internet Explorer 5.0 o versione successiva, specificare `TransformTo.MSDHTML`.
   * A `BLOB` oggetto contenente i dati da unire al modulo. Se non si desidera unire i dati, passare `null`.
   * La `HTMLRenderSpec` oggetto che memorizza le opzioni di runtime di HTML.
   * Un valore stringa che specifica la variabile `HTTP_USER_AGENT` valore di intestazione, ad esempio `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322`). Se non si desidera impostare questo valore, è possibile passare una stringa vuota.
   * A `URLSpec` oggetto che memorizza i valori URI necessari per eseguire il rendering di un modulo HTML.
   * A `java.util.HashMap` oggetto che memorizza gli allegati di file. Questo parametro è facoltativo ed è possibile specificare `null` se non si intende allegare file al modulo.
   * Un vuoto `com.adobe.idp.services.holders.BLOBHolder` oggetto popolato da `renderHTMLForm` metodo . Questo valore del parametro memorizza il modulo di cui è stato effettuato il rendering.
   * Un vuoto `com.adobe.idp.services.holders.BLOBHolder` oggetto popolato da `renderHTMLForm` metodo . Questo parametro memorizza i dati XML di output.
   * Un vuoto `javax.xml.rpc.holders.LongHolder` oggetto popolato da `renderHTMLForm` metodo . Questo argomento memorizza il numero di pagine nel modulo.
   * Un vuoto `javax.xml.rpc.holders.StringHolder` oggetto popolato da `renderHTMLForm` metodo . Questo argomento memorizza il valore delle impostazioni internazionali.
   * Un vuoto `javax.xml.rpc.holders.StringHolder` oggetto popolato da `renderHTMLForm` metodo . Questo argomento memorizza il valore di rendering di HTML utilizzato.
   * Un vuoto `com.adobe.idp.services.holders.FormsResultHolder` oggetto che conterrà i risultati dell&#39;operazione.

   La `renderHTMLForm` popola il `com.adobe.idp.services.holders.FormsResultHolder` oggetto passato come ultimo valore argomento con un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo sul browser Web client

   * Crea un `FormResult` ottenendo il valore del `com.adobe.idp.services.holders.FormsResultHolder` dell’oggetto `value` membro dati.
   * Crea un `BLOB` oggetto che contiene i dati del modulo richiamando il `FormsResult` dell’oggetto `getOutputContent` metodo .
   * Ottieni il tipo di contenuto del `BLOB` richiamandone l&#39;oggetto `getContentType` metodo .
   * Imposta la `javax.servlet.http.HttpServletResponse` tipo di contenuto dell’oggetto richiamandone il tipo `setContentType` e passare il tipo di contenuto `BLOB` oggetto.
   * Crea un `javax.servlet.ServletOutputStream` oggetto utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il `javax.servlet.http.HttpServletResponse` dell’oggetto `getOutputStream` metodo .
   * Creare un array di byte e compilarlo richiamando il `BLOB` dell’oggetto `getBinaryData` metodo . Questa attività assegna il contenuto del `FormsResult` all&#39;array di byte.
   * Richiama il `javax.servlet.http.HttpServletResponse` dell’oggetto `write` per inviare il flusso di dati del modulo al browser Web client. Passa l&#39;array di byte al `write` metodo .

**Consulta anche**

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
