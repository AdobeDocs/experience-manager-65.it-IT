---
title: Rendering di Forms HTML con barre degli strumenti personalizzate
seo-title: Rendering di Forms HTML con barre degli strumenti personalizzate
description: Utilizza il servizio Forms per personalizzare una barra degli strumenti di cui è eseguito il rendering con un modulo HTML. È possibile eseguire il rendering di un modulo HTML con una barra degli strumenti personalizzata utilizzando l’API Java e un’API di servizio Web.
seo-description: Utilizza il servizio Forms per personalizzare una barra degli strumenti di cui è eseguito il rendering con un modulo HTML. È possibile eseguire il rendering di un modulo HTML con una barra degli strumenti personalizzata utilizzando l’API Java e un’API di servizio Web.
uuid: b9c9464e-ff19-4051-a39b-4ec71c512d10
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 7eb0e8a8-d76a-43f7-a012-c21157b14cd4
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2385'
ht-degree: 0%

---


# Rendering di Forms HTML con barre degli strumenti personalizzate {#rendering-html-forms-with-customtoolbars}

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

fscJS è lo script Java associato a ciascun nodo. È necessario fornirne uno per il nodo `div#fscmenu` ed eventualmente per i nodi `ul#fscmenuItem`. I file JS implementano la funzionalità di base della barra degli strumenti e i file predefiniti funzionano.

fscCSS è un foglio di stile associato a un particolare nodo. Gli stili nei file CSS specificano l’aspetto della barra degli strumenti. ** fscVCSSè un foglio di stile per una barra degli strumenti verticale, visualizzato a sinistra del modulo HTML di cui è stato eseguito il rendering. ** fscIECSSè un foglio di stile utilizzato per i moduli HTML di cui viene eseguito il rendering in Internet Explorer.

Assicurati che tutti i file di cui sopra siano referenziati nel file fscmenu.xml. In altre parole, nel file fscmenu.xml, specifica le posizioni URI da cui puntare a questi file in modo che il servizio Forms possa individuarli. Per impostazione predefinita, questi file sono disponibili in posizioni URI che iniziano con parole chiave interne `FSWebRoot` o `ApplicationWebRoot`.

Per personalizzare la barra degli strumenti, sostituisci le parole chiave utilizzando la parola chiave esterna `FSToolBarURI`. Questa parola chiave rappresenta l’URI passato al servizio Forms in fase di esecuzione (questo approccio viene mostrato più avanti in questa sezione).

Puoi anche specificare le posizioni assolute di questi file JS e CSS, ad esempio https://www.mycompany.com/scripts/misc/fscmenu.js. In questa situazione, non è necessario utilizzare la parola chiave `FSToolBarURI`.

>[!NOTE]
>
>Si sconsiglia di combinare i modi in cui si fa riferimento a questi file. In altre parole, tutti gli URI devono essere referenziati utilizzando la parola chiave `FSToolBarURI` o una posizione assoluta.

Puoi ottenere i file JS e CSS aprendo il file adobe-forms-&lt;appserver>.ear. All’interno di questo file, apri adobe-forms-res.war. Tutti questi file si trovano nel file WAR. Il file adobe-forms-&lt;appserver>.ear si trova nella cartella di installazione dei moduli AEM (C:\ is the installation directory). Puoi aprire adobe-forms-&lt;appserver>.ear utilizzando uno strumento di estrazione file come WinRAR.

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

* Modifica i valori degli attributi `fscJS`, `fscCSS`, `fscVCSS`, `fscIECSS` (nel file fscmenu.xml) per riflettere le posizioni personalizzate dei file a cui si fa riferimento utilizzando uno dei metodi descritti in questa sezione (ad esempio, `fscJS="FSToolBarURI/scripts/fscmenu.js"`).
* Tutti i file CSS e JS devono essere specificati. Se nessuno dei file viene modificato, inserisci quello predefinito nel percorso personalizzato. È possibile ottenere i file predefiniti aprendo vari file come descritto in questa sezione.
* È consentito fornire un riferimento assoluto (ad esempio, https://www.example.com/scripts/custom-vertical-fscmenu.css) per qualsiasi file.
* I file JS e CSS richiesti dal nodo `div#fscmenu` sono essenziali per la funzionalità della barra degli strumenti. I singoli nodi `ul#fscmenuItem` possono avere o meno file JS o CSS di supporto.

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

Inoltre, specificare un valore di impostazione internazionale valido richiamando il metodo `setLocale` dell&#39;oggetto `HTMLRenderSpec` e passando un valore di stringa che specifichi il valore di impostazione internazionale. Ad esempio, passare `fr_FR` per specificare francese. Il servizio Forms è fornito con barre degli strumenti localizzate.

>[!NOTE]
>
>Prima di eseguire il rendering di un modulo HTML che utilizza una barra degli strumenti personalizzata, è necessario conoscere il rendering dei moduli HTML. (Vedere [Rendering di Forms come HTML](/help/forms/developing/rendering-forms-html.md).)

Per ulteriori informazioni sul servizio Forms, consulta [Riferimento servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

Per eseguire il rendering di un modulo HTML che contiene una barra degli strumenti personalizzata, fare riferimento a un file XML fscmenu che descrive la barra degli strumenti. (Questa sezione fornisce due esempi di un file XML fscmenu.) Inoltre, assicurati che il file fscmenu.xml specifichi correttamente le posizioni di tutti i file di riferimento. Come menzionato in precedenza in questa sezione, assicurati che a tutti i file venga fatto riferimento dalla parola chiave `FSToolBarURI` o dalle relative posizioni assolute.

**Rendering di un modulo HTML**

Per eseguire il rendering di un modulo HTML, specificare una struttura del modulo creata in Designer e salvata come file XDP. Seleziona anche un tipo di trasformazione HTML. Ad esempio, è possibile specificare il tipo di trasformazione HTML che esegue il rendering di un HTML dinamico per Internet Explorer 5.0 o versione successiva.

Il rendering di un modulo HTML richiede anche valori, ad esempio valori URI per il rendering di altri tipi di modulo.

**Scrivere il flusso di dati del modulo sul browser Web client**

Quando il servizio Forms esegue il rendering di un modulo HTML, restituisce un flusso di dati del modulo che è necessario scrivere nel browser Web del client per rendere il modulo HTML visibile agli utenti.

**Consulta anche**

[Eseguire il rendering di un modulo HTML con una barra degli strumenti personalizzata utilizzando l’API Java](#render-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Rendering di un modulo HTML con una barra degli strumenti personalizzata utilizzando l’API del servizio Web](#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido API di Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendering di PDF forms interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Rendering di Forms come HTML](/help/forms/developing/rendering-forms-html.md)

[Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Eseguire il rendering di un modulo HTML con una barra degli strumenti personalizzata utilizzando l’API Java {#render-an-html-form-with-a-custom-toolbar-using-the-java-api}

Eseguire il rendering di un modulo HTML contenente una barra degli strumenti personalizzata utilizzando l’API di servizio Forms (Java):

1. Includi file di progetto

   Includi file JAR client, come adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API Java di Forms

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `FormsServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Riferimento a un file XML personalizzato fscmenu

   * Creare un oggetto `HTMLRenderSpec` utilizzando il relativo costruttore.
   * Per eseguire il rendering di un modulo HTML con una barra degli strumenti, richiamare il metodo `setHTMLToolbar` dell’oggetto `HTMLToolbar` e passare un valore di enum `HTMLRenderSpec`. Ad esempio, per visualizzare una barra degli strumenti HTML verticale, passa `HTMLToolbar.Vertical`.
   * Specificare la posizione del file XML fscmenu richiamando il metodo `setToolbarURI` dell&#39;oggetto `HTMLRenderSpec` e passando un valore di stringa che specifica la posizione URI del file XML.
   * Se applicabile, impostare il valore delle impostazioni internazionali richiamando il metodo `setLocale` dell&#39;oggetto `HTMLRenderSpec` e passando un valore stringa che specifichi il valore delle impostazioni internazionali. Il valore predefinito è Inglese.

   >[!NOTE]
   >
   >Il valore di Avvio rapido associato a questa sezione viene impostato su `fr_FR`*.*

1. Rendering di un modulo HTML

   Richiama il metodo `renderHTMLForm` dell&#39;oggetto `FormsServiceClient` e passa i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, assicurarsi di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Valore enum `TransformTo` che specifica il tipo di preferenza HTML. Ad esempio, per eseguire il rendering di un modulo HTML compatibile con HTML dinamico per Internet Explorer 5.0 o versione successiva, specificare `TransformTo.MSDHTML`.
   * Un oggetto `com.adobe.idp.Document` contenente i dati da unire al modulo. Se non si desidera unire i dati, passare un oggetto `com.adobe.idp.Document` vuoto.
   * L&#39;oggetto `HTMLRenderSpec` che memorizza le opzioni di runtime HTML.
   * Valore stringa che specifica il valore di intestazione `HTTP_USER_AGENT`, ad esempio `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * Un oggetto `URLSpec` che memorizza i valori URI necessari per il rendering di un modulo HTML.
   * Un oggetto `java.util.HashMap` che memorizza gli allegati di file. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.

   Il metodo `renderHTMLForm` restituisce un oggetto `FormsResult` contenente un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo sul browser Web client

   * Creare un oggetto `com.adobe.idp.Document` richiamando il metodo `FormsResult` object ‘s `getOutputContent` .
   * Ottenere il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document` richiamandone il metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamandone il metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il metodo `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream`.
   * Creare un oggetto `java.io.InputStream` richiamando il metodo `com.adobe.idp.Document` dell&#39;oggetto `getInputStream`.
   * Creare una matrice di byte e compilarla con il flusso di dati del modulo richiamando il metodo `InputStream` dell&#39;oggetto `read` e passando la matrice di byte come argomento.
   * Richiamare il metodo `write` dell’oggetto `javax.servlet.ServletOutputStream` per inviare il flusso di dati del modulo al browser Web client. Passa l&#39;array di byte al metodo `write` .

**Consulta anche**

[Avvio rapido (modalità SOAP): Rendering di un modulo HTML con una barra degli strumenti personalizzata tramite l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rendering di un modulo HTML con una barra degli strumenti personalizzata utilizzando l’API del servizio Web {#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api}

Eseguire il rendering di un modulo HTML che contiene una barra degli strumenti personalizzata utilizzando l’API del servizio Forms (servizio Web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio WSDL di Forms.
   * Includi le classi proxy Java nel percorso della classe.

1. Creare un oggetto API Java di Forms

   Creare un oggetto `FormsService` e impostare i valori di autenticazione.

1. Riferimento a un file XML personalizzato fscmenu

   * Creare un oggetto `HTMLRenderSpec` utilizzando il relativo costruttore.
   * Per eseguire il rendering di un modulo HTML con una barra degli strumenti, richiamare il metodo `setHTMLToolbar` dell’oggetto `HTMLToolbar` e passare un valore di enum `HTMLRenderSpec`. Ad esempio, per visualizzare una barra degli strumenti HTML verticale, passa `HTMLToolbar.Vertical`.
   * Specificare la posizione del file XML fscmenu richiamando il metodo `setToolbarURI` dell&#39;oggetto `HTMLRenderSpec` e passando un valore di stringa che specifica la posizione URI del file XML.
   * Se applicabile, impostare il valore delle impostazioni internazionali richiamando il metodo `setLocale` dell&#39;oggetto `HTMLRenderSpec` e passando un valore stringa che specifichi il valore delle impostazioni internazionali. Il valore predefinito è Inglese.

   >[!NOTE]
   >
   >Il valore di Avvio rapido associato a questa sezione viene impostato su `fr_FR`*.*

1. Rendering di un modulo HTML

   Richiama il metodo `renderHTMLForm` dell&#39;oggetto `FormsService` e passa i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, assicurarsi di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Valore enum `TransformTo` che specifica il tipo di preferenza HTML. Ad esempio, per eseguire il rendering di un modulo HTML compatibile con HTML dinamico per Internet Explorer 5.0 o versione successiva, specificare `TransformTo.MSDHTML`.
   * Un oggetto `BLOB` contenente i dati da unire al modulo. Se non desideri unire i dati, passa `null`.
   * L&#39;oggetto `HTMLRenderSpec` che memorizza le opzioni di runtime HTML.
   * Valore stringa che specifica il valore di intestazione `HTTP_USER_AGENT`, ad esempio `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322`). Se non si desidera impostare questo valore, è possibile passare una stringa vuota.
   * Un oggetto `URLSpec` che memorizza i valori URI necessari per il rendering di un modulo HTML.
   * Un oggetto `java.util.HashMap` che memorizza gli allegati di file. Questo parametro è facoltativo ed è possibile specificare `null` se non si intende allegare file al modulo.
   * Un oggetto `com.adobe.idp.services.holders.BLOBHolder` vuoto compilato dal metodo `renderHTMLForm`. Questo valore del parametro memorizza il modulo di cui è stato effettuato il rendering.
   * Un oggetto `com.adobe.idp.services.holders.BLOBHolder` vuoto compilato dal metodo `renderHTMLForm`. Questo parametro memorizza i dati XML di output.
   * Un oggetto `javax.xml.rpc.holders.LongHolder` vuoto compilato dal metodo `renderHTMLForm`. Questo argomento memorizza il numero di pagine nel modulo.
   * Un oggetto `javax.xml.rpc.holders.StringHolder` vuoto compilato dal metodo `renderHTMLForm`. Questo argomento memorizza il valore delle impostazioni internazionali.
   * Un oggetto `javax.xml.rpc.holders.StringHolder` vuoto compilato dal metodo `renderHTMLForm`. Questo argomento memorizza il valore di rendering HTML utilizzato.
   * Un oggetto `com.adobe.idp.services.holders.FormsResultHolder` vuoto che conterrà i risultati dell&#39;operazione.

   Il metodo `renderHTMLForm` popola l&#39;oggetto `com.adobe.idp.services.holders.FormsResultHolder` passato come ultimo valore dell&#39;argomento con un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo sul browser Web client

   * Creare un oggetto `FormResult` ottenendo il valore del membro dati `com.adobe.idp.services.holders.FormsResultHolder` dell&#39;oggetto `value`.
   * Creare un oggetto `BLOB` che contiene dati del modulo richiamando il metodo `FormsResult` dell&#39;oggetto `getOutputContent`.
   * Ottenere il tipo di contenuto dell&#39;oggetto `BLOB` richiamandone il metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamandone il metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `BLOB`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il metodo `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream`.
   * Creare una matrice di byte e compilarla richiamando il metodo `getBinaryData` dell&#39;oggetto `BLOB`. Questa attività assegna il contenuto dell&#39;oggetto `FormsResult` all&#39;array di byte.
   * Richiamare il metodo `write` dell’oggetto `javax.servlet.http.HttpServletResponse` per inviare il flusso di dati del modulo al browser Web client. Passa l&#39;array di byte al metodo `write` .

**Consulta anche**

[Richiamo di AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
