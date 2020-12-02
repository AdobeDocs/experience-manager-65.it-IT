---
title: Rendering HTML Forms con barre degli strumenti personalizzate
seo-title: Rendering HTML Forms con barre degli strumenti personalizzate
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


# Rendering HTML Forms con barre degli strumenti personalizzate {#rendering-html-forms-with-customtoolbars}

## Rendering HTML Forms con barre degli strumenti personalizzate {#rendering-html-forms-with-custom-toolbars}

Il servizio Forms consente di personalizzare una barra degli strumenti rappresentata con un modulo HTML. È possibile personalizzare una barra degli strumenti per modificarne l&#39;aspetto sovrascrivendo gli stili CSS predefiniti e per aggiungere un comportamento dinamico sovrascrivendo gli script Java. Una barra degli strumenti è personalizzata utilizzando un file XML denominato fscmenu.xml. Per impostazione predefinita, il servizio Forms recupera il file da una posizione URI specificata internamente.

>[!NOTE]
>
>Questa posizione URI si trova nel file adobe-forms-core.jar, che si trova nel file adobe-forms-dsc.jar. Il file adobe-forms-dsc.jar si trova in C:\Adobe\Adobe_Experience_Manager_forms\ folder (C:\ is the installation directory). Potete utilizzare uno strumento di estrazione file, ad esempio Win RAR, per aprire l&#39;adobe.

Potete copiare il file fscmenu.xml da questa posizione, modificarlo per soddisfare i requisiti, quindi inserirlo in una posizione URI personalizzata. Quindi, utilizzando l&#39;API di Forms Service, impostate le opzioni di esecuzione che determinano l&#39;utilizzo del servizio Forms da parte del file fscmenu.xml dal percorso specificato. Queste azioni generano il rendering di un modulo HTML con una barra degli strumenti personalizzata da parte del servizio Forms.

Oltre al file fscmenu.xml, dovete anche ottenere i file seguenti:

* fscmenu.js
* fscattachments.js
* fscmenu.css
* fscmenu-v.css
* fscmenu-ie.css
* fscdialog.css

fscJS è lo script Java associato a ciascun nodo. È necessario fornire uno per il nodo `div#fscmenu` ed eventualmente per i nodi `ul#fscmenuItem`. I file JS implementano la funzionalità di base della barra degli strumenti e i file predefiniti funzionano.

fscCSS è un foglio di stile associato a un particolare nodo. Gli stili nei file CSS specificano l&#39;aspetto della barra degli strumenti. ** fscVCSS è un foglio di stile per una barra degli strumenti verticale, che viene visualizzata a sinistra del modulo HTML di cui è stato effettuato il rendering. ** fscIECSSè un foglio di stile utilizzato per i moduli HTML di cui viene eseguito il rendering in Internet Explorer.

Verificate che tutti i file di cui sopra siano citati nel file fscmenu.xml. In altre parole, nel file fscmenu.xml, specificate i percorsi URI per puntare a questi file in modo che il servizio Forms possa individuarli. Per impostazione predefinita, questi file sono disponibili nelle posizioni URI a partire dalle parole chiave interne `FSWebRoot` o `ApplicationWebRoot`.

Per personalizzare la barra degli strumenti, sostituire le parole chiave utilizzando la parola chiave esterna `FSToolBarURI`. Questa parola chiave rappresenta l’URI passato al servizio Forms in fase di esecuzione (questo approccio viene mostrato più avanti in questa sezione).

Potete anche specificare le posizioni assolute di questi file JS e CSS, ad esempio https://www.mycompany.com/scripts/misc/fscmenu.js. In questa situazione, non è necessario utilizzare la parola chiave `FSToolBarURI`.

>[!NOTE]
>
>Non è consigliabile utilizzare diversi metodi per fare riferimento a tali file. In altre parole, tutti gli URI devono essere citati utilizzando la parola chiave `FSToolBarURI` o una posizione assoluta.

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

* Modificate i valori degli attributi `fscJS`, `fscCSS`, `fscVCSS`, `fscIECSS` (nel file fscmenu.xml) per riflettere le posizioni personalizzate dei file a cui si fa riferimento utilizzando uno dei metodi descritti in questa sezione (ad esempio, `fscJS="FSToolBarURI/scripts/fscmenu.js"`).
* Devono essere specificati tutti i file CSS e JS. Se nessuno dei file viene modificato, immettete quello predefinito nel percorso personalizzato. Potete ottenere i file predefiniti aprendo vari file come descritto in questa sezione.
* È consentito fornire un riferimento assoluto (ad esempio, https://www.example.com/scripts/custom-vertical-fscmenu.css) per qualsiasi file.
* I file JS e CSS richiesti dal nodo `div#fscmenu` sono essenziali per la funzionalità della barra degli strumenti. I singoli nodi `ul#fscmenuItem` possono avere o non avere file JS o CSS supportati.

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

Inoltre, specificate un valore di impostazione internazionale valido richiamando il metodo `setLocale` dell&#39;oggetto `HTMLRenderSpec` e passando un valore di stringa che specifica il valore delle impostazioni internazionali. Ad esempio, passare `fr_FR` per specificare il francese. Il servizio Forms è fornito con barre degli strumenti localizzate.

>[!NOTE]
>
>Prima di eseguire il rendering di un modulo HTML che utilizza una barra degli strumenti personalizzata, è necessario conoscere il rendering dei moduli HTML. (Vedere [Rendering di Forms come HTML](/help/forms/developing/rendering-forms-html.md).)

Per ulteriori informazioni sul servizio Forms, vedere [Guida di riferimento dei servizi per  AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per eseguire il rendering di un modulo HTML che contiene una barra degli strumenti personalizzata, effettuare le seguenti operazioni:

1. Includere i file di progetto.
1. Creare un oggetto Forms Java API.
1. Fate riferimento a un file XML personalizzato del menu di scelta rapida.
1. Eseguire il rendering di un modulo HTML.
1. Scrivere il flusso di dati del modulo nel browser Web del client.

**Includi file di progetto**

Includete i file necessari nel progetto di sviluppo. Se create un&#39;applicazione client utilizzando Java, includete i file JAR necessari. Se utilizzate i servizi Web, includete i file proxy.

**Creare un oggetto API Forms Java**

Prima di eseguire un&#39;operazione supportata dal servizio Forms a livello di programmazione, è necessario creare un oggetto client Forms.

**Riferimento a un file XML personalizzato di fscmenu**

Per eseguire il rendering di un modulo HTML che contiene una barra degli strumenti personalizzata, fare riferimento a un file XML fscmenu che descrive la barra degli strumenti. In questa sezione sono riportati due esempi di un file XML fscmenu. Inoltre, accertatevi che il file fscmenu.xml specifichi correttamente le posizioni di tutti i file di riferimento. Come indicato in precedenza in questa sezione, accertatevi che a tutti i file facciano riferimento la parola chiave `FSToolBarURI` o le relative posizioni assolute.

**Eseguire il rendering di un modulo HTML**

Per eseguire il rendering di un modulo HTML, specificare una struttura del modulo creata in Designer e salvata come file XDP. Selezionare anche un tipo di trasformazione HTML. Ad esempio, potete specificare il tipo di trasformazione HTML che esegue il rendering di un HTML dinamico per Internet Explorer 5.0 o versione successiva.

Il rendering di un modulo HTML richiede anche valori, ad esempio valori URI per il rendering di altri tipi di modulo.

**Scrivere il flusso di dati del modulo nel browser Web del client**

Quando il servizio Forms esegue il rendering di un modulo HTML, restituisce un flusso di dati del modulo che è necessario scrivere nel browser Web del client per rendere il modulo HTML visibile agli utenti.

**Consulta anche**

[Eseguire il rendering di un modulo HTML con una barra degli strumenti personalizzata utilizzando l&#39;API Java](#render-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Rendering di un modulo HTML con una barra degli strumenti personalizzata tramite l&#39;API del servizio Web](#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Avvio rapido di Forms Service API](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendering di PDF forms interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Rendering di Forms come HTML](/help/forms/developing/rendering-forms-html.md)

[Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Eseguire il rendering di un modulo HTML con una barra degli strumenti personalizzata utilizzando l&#39;API Java {#render-an-html-form-with-a-custom-toolbar-using-the-java-api}

Eseguire il rendering di un modulo HTML contenente una barra degli strumenti personalizzata utilizzando l&#39;API di Forms Service (Java):

1. Includi file di progetto

   Includete file JAR client, ad esempio adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API Forms Java

   * Creare un oggetto `ServiceClientFactory` che contiene le proprietà di connessione.
   * Creare un oggetto `FormsServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Riferimento a un file XML personalizzato di fscmenu

   * Creare un oggetto `HTMLRenderSpec` utilizzando il relativo costruttore.
   * Per eseguire il rendering di un modulo HTML con una barra degli strumenti, richiamare il metodo `HTMLRenderSpec` dell&#39;oggetto `setHTMLToolbar` e passare un valore enum &lt;a2/>. `HTMLToolbar` Ad esempio, per visualizzare una barra degli strumenti HTML verticale, passare `HTMLToolbar.Vertical`.
   * Specificare la posizione del file XML fscmenu richiamando il metodo `HTMLRenderSpec` dell&#39;oggetto &lt;a1/> e passando un valore di stringa che specifica la posizione URI del file XML.`setToolbarURI`
   * Se applicabile, impostare il valore delle impostazioni internazionali richiamando il metodo `setLocale` dell&#39;oggetto `HTMLRenderSpec` e passando un valore di stringa che specifica il valore delle impostazioni internazionali. Il valore predefinito è Inglese.

   >[!NOTE]
   >
   >Gli avvii rapidi associati a questa sezione impostano questo valore su `fr_FR`*.*

1. Eseguire il rendering di un modulo HTML

   Richiamare il metodo `FormsServiceClient` dell&#39;oggetto `renderHTMLForm` e trasmettere i seguenti valori:

   * Una stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, è necessario specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un valore enum `TransformTo` che specifica il tipo di preferenza HTML. Ad esempio, per eseguire il rendering di un modulo HTML compatibile con HTML dinamico per Internet Explorer 5.0 o versione successiva, specificare `TransformTo.MSDHTML`.
   * Un oggetto `com.adobe.idp.Document` che contiene i dati da unire al modulo. Se non si desidera unire i dati, passare un oggetto `com.adobe.idp.Document` vuoto.
   * L&#39;oggetto `HTMLRenderSpec` che memorizza le opzioni di runtime HTML.
   * Un valore di stringa che specifica il valore dell&#39;intestazione `HTTP_USER_AGENT`, ad esempio `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * Un oggetto `URLSpec` che memorizza i valori URI necessari per eseguire il rendering di un modulo HTML.
   * Un oggetto `java.util.HashMap` che memorizza gli allegati. Si tratta di un parametro facoltativo e è possibile specificare `null` se non si desidera allegare file al modulo.

   Il metodo `renderHTMLForm` restituisce un oggetto `FormsResult` contenente un flusso di dati del modulo che deve essere scritto nel browser Web del client.

1. Scrivere il flusso di dati del modulo nel browser Web del client

   * Creare un oggetto `com.adobe.idp.Document` richiamando il metodo `FormsResult` object ‘s `getOutputContent`.
   * Ottenere il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document` richiamandone il metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamandone il metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web del client richiamando il metodo `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream`.
   * Creare un oggetto `java.io.InputStream` richiamando il metodo `com.adobe.idp.Document` dell&#39;oggetto `getInputStream`.
   * Creare un array di byte e compilarlo con il flusso di dati del modulo richiamando il metodo `InputStream` dell&#39;oggetto `read` e passando l&#39;array di byte come argomento.
   * Richiamare il metodo `javax.servlet.ServletOutputStream` dell&#39;oggetto `write` per inviare il flusso di dati del modulo al browser Web del client. Passate l&#39;array di byte al metodo `write`.

**Consulta anche**

[Avvio rapido (modalità SOAP): Rendering di un modulo HTML con una barra degli strumenti personalizzata tramite l&#39;API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Inclusione  file libreria Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rendering di un modulo HTML con una barra degli strumenti personalizzata mediante l&#39;API del servizio Web {#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api}

Eseguire il rendering di un modulo HTML che contiene una barra degli strumenti personalizzata utilizzando l&#39;API di Forms Service (servizio Web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio WSDL di Forms.
   * Includete le classi proxy Java nel percorso della classe.

1. Creare un oggetto API Forms Java

   Creare un oggetto `FormsService` e impostare i valori di autenticazione.

1. Riferimento a un file XML personalizzato di fscmenu

   * Creare un oggetto `HTMLRenderSpec` utilizzando il relativo costruttore.
   * Per eseguire il rendering di un modulo HTML con una barra degli strumenti, richiamare il metodo `HTMLRenderSpec` dell&#39;oggetto `setHTMLToolbar` e passare un valore enum &lt;a2/>. `HTMLToolbar` Ad esempio, per visualizzare una barra degli strumenti HTML verticale, passare `HTMLToolbar.Vertical`.
   * Specificare la posizione del file XML fscmenu richiamando il metodo `HTMLRenderSpec` dell&#39;oggetto &lt;a1/> e passando un valore di stringa che specifica la posizione URI del file XML.`setToolbarURI`
   * Se applicabile, impostare il valore delle impostazioni internazionali richiamando il metodo `setLocale` dell&#39;oggetto `HTMLRenderSpec` e passando un valore di stringa che specifica il valore delle impostazioni internazionali. Il valore predefinito è Inglese.

   >[!NOTE]
   >
   >Gli avvii rapidi associati a questa sezione impostano questo valore su `fr_FR`*.*

1. Eseguire il rendering di un modulo HTML

   Richiamare il metodo `FormsService` dell&#39;oggetto `renderHTMLForm` e trasmettere i seguenti valori:

   * Una stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura del modulo che fa parte di un&#39;applicazione Forms, è necessario specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Un valore enum `TransformTo` che specifica il tipo di preferenza HTML. Ad esempio, per eseguire il rendering di un modulo HTML compatibile con HTML dinamico per Internet Explorer 5.0 o versione successiva, specificare `TransformTo.MSDHTML`.
   * Un oggetto `BLOB` che contiene i dati da unire al modulo. Se non si desidera unire i dati, passare `null`.
   * L&#39;oggetto `HTMLRenderSpec` che memorizza le opzioni di runtime HTML.
   * Un valore di stringa che specifica il valore dell&#39;intestazione `HTTP_USER_AGENT`, ad esempio `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322`). Se non si desidera impostare questo valore, è possibile passare una stringa vuota.
   * Un oggetto `URLSpec` che memorizza i valori URI necessari per eseguire il rendering di un modulo HTML.
   * Un oggetto `java.util.HashMap` che memorizza gli allegati. Questo parametro è facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.
   * Un oggetto `com.adobe.idp.services.holders.BLOBHolder` vuoto compilato dal metodo `renderHTMLForm`. Questo valore del parametro memorizza il modulo di cui è stato effettuato il rendering.
   * Un oggetto `com.adobe.idp.services.holders.BLOBHolder` vuoto compilato dal metodo `renderHTMLForm`. Questo parametro memorizza i dati XML di output.
   * Un oggetto `javax.xml.rpc.holders.LongHolder` vuoto compilato dal metodo `renderHTMLForm`. Questo argomento memorizza il numero di pagine nel modulo.
   * Un oggetto `javax.xml.rpc.holders.StringHolder` vuoto compilato dal metodo `renderHTMLForm`. Questo argomento memorizza il valore delle impostazioni internazionali.
   * Un oggetto `javax.xml.rpc.holders.StringHolder` vuoto compilato dal metodo `renderHTMLForm`. Questo argomento memorizza il valore di rendering HTML utilizzato.
   * Un oggetto `com.adobe.idp.services.holders.FormsResultHolder` vuoto che conterrà i risultati dell&#39;operazione.

   Il metodo `renderHTMLForm` compila l&#39;oggetto `com.adobe.idp.services.holders.FormsResultHolder` passato come ultimo valore argomento con un flusso di dati del modulo che deve essere scritto nel browser Web del client.

1. Scrivere il flusso di dati del modulo nel browser Web del client

   * Creare un oggetto `FormResult` ottenendo il valore del membro di dati `com.adobe.idp.services.holders.FormsResultHolder` dell&#39;oggetto `value`.
   * Creare un oggetto `BLOB` contenente dati del modulo richiamando il metodo `FormsResult` dell&#39;oggetto `getOutputContent`.
   * Ottenere il tipo di contenuto dell&#39;oggetto `BLOB` richiamandone il metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamandone il metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `BLOB`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web del client richiamando il metodo `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `getOutputStream`.
   * Creare un array di byte e compilarlo richiamando il metodo `BLOB` dell&#39;oggetto `getBinaryData`. Questa attività assegna il contenuto dell&#39;oggetto `FormsResult` all&#39;array di byte.
   * Richiamare il metodo `javax.servlet.http.HttpServletResponse` dell&#39;oggetto `write` per inviare il flusso di dati del modulo al browser Web del client. Passate l&#39;array di byte al metodo `write`.

**Consulta anche**

[Richiamo  AEM Forms con codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
