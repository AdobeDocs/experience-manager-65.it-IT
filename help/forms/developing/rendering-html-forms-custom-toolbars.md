---
title: Rendering di HTML Forms con CustomToolbars
description: Utilizza il servizio Forms per personalizzare una barra degli strumenti di cui viene eseguito il rendering con un modulo di HTML. Puoi eseguire il rendering di un modulo HTML con una barra degli strumenti personalizzata utilizzando l’API Java e un’API di servizio web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 0b992b1c-3878-447a-bccc-7034aa3e98bc
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2328'
ht-degree: 0%

---

# Rendering di HTML Forms con CustomToolbars {#rendering-html-forms-with-customtoolbars}

**Gli esempi e gli esempi contenuti in questo documento sono solo per AEM Forms in ambiente JEE.**

## Rendering di HTML Forms con barre degli strumenti personalizzate {#rendering-html-forms-with-custom-toolbars}

Il servizio Forms consente di personalizzare una barra degli strumenti di cui viene eseguito il rendering con un modulo di HTML. È possibile personalizzare una barra degli strumenti per modificarne l’aspetto ignorando gli stili CSS predefiniti e per aggiungere un comportamento dinamico ignorando gli script Java. Una barra degli strumenti viene personalizzata utilizzando un file XML denominato fscmenu.xml. Per impostazione predefinita, il servizio Forms recupera il file da un percorso URI specificato internamente.

>[!NOTE]
>
>Questa posizione URI si trova nel file adobe-forms-core.jar, che si trova nel file adobe-forms-dsc.jar. Il file adobe-forms-dsc.jar si trova nella cartella C:\Adobe\Adobe_Experience_Manager_forms\ (C:\ è la directory di installazione). Per aprire Adobe, puoi utilizzare uno strumento di estrazione file, ad esempio Win RAR.

È possibile copiare il file fscmenu.xml da questa posizione, modificarlo in base alle proprie esigenze e quindi inserirlo in una posizione URI personalizzata. Quindi, utilizzando l’API del servizio Forms, imposta le opzioni di runtime che fanno sì che il servizio Forms utilizzi il file fscmenu.xml dalla posizione specificata. Il servizio Forms esegue il rendering di un modulo HTML con una barra degli strumenti personalizzata.

Oltre al file fscmenu.xml, è necessario ottenere i seguenti file:

* fscmenu.js
* fscattachments.js
* fscmenu.css
* fscmenu-v.css
* fscmenu-ie.css
* fscdialog.css

fscJS è lo script Java associato a ciascun nodo. È necessario fornirne uno per il nodo `div#fscmenu` e facoltativamente per i nodi `ul#fscmenuItem`. I file JS implementano le funzionalità principali della barra degli strumenti e funzionano i file predefiniti.

fscCSS è un foglio di stile associato a un nodo specifico. Gli stili nei file CSS specificano l&#39;aspetto della barra degli strumenti. *fscVCSS* è un foglio di stile per una barra degli strumenti verticale, visualizzato a sinistra del modulo HTML sottoposto a rendering. *fscIECSS* è un foglio di stile utilizzato per i moduli HTML di cui è stato eseguito il rendering in Internet Explorer.

Verificare che nel file fscmenu.xml sia presente un riferimento a tutti i file sopra indicati. In altre parole, nel file fscmenu.xml, specificare i percorsi URI per puntare a questi file in modo che il servizio Forms possa individuarli. Per impostazione predefinita, questi file sono disponibili nelle posizioni URI a partire dalle parole chiave interne `FSWebRoot` o `ApplicationWebRoot`.

Per personalizzare la barra degli strumenti, sostituire le parole chiave utilizzando la parola chiave esterna `FSToolBarURI`. Questa parola chiave rappresenta l’URI passato al servizio Forms in fase di esecuzione (questo approccio viene illustrato più avanti in questa sezione).

Puoi anche specificare le posizioni assolute di questi file JS e CSS, ad esempio https://www.mycompany.com/scripts/misc/fscmenu.js. In questa situazione, non è necessario utilizzare la parola chiave `FSToolBarURI`.

>[!NOTE]
>
>Non è consigliabile combinare i modi in cui si fa riferimento a questi file. In altre parole, è necessario fare riferimento a tutti gli URI utilizzando la parola chiave `FSToolBarURI` o una posizione assoluta.

Per ottenere i file JS e CSS, apri il file adobe-forms-&lt;appserver>.ear. All’interno di questo file, apri adobe-forms-res.war. Tutti questi file sono nel file WAR. Il file adobe-forms-&lt;appserver>.ear si trova nella cartella di installazione di AEM forms (C:\ è la directory di installazione). Puoi aprire adobe-forms-&lt;appserver>.ear utilizzando uno strumento di estrazione file come WinRAR.

La sintassi XML seguente mostra un esempio di file fscmenu.xml.

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

* Modificare i valori degli attributi `fscJS`, `fscCSS`, `fscVCSS`, `fscIECSS` (nel file fscmenu.xml) in modo da riflettere le posizioni personalizzate dei file di riferimento utilizzando uno dei metodi descritti in questa sezione (ad esempio, `fscJS="FSToolBarURI/scripts/fscmenu.js"`).
* Specificare tutti i file CSS e JS. Se nessuno dei file viene modificato, fornisci quello predefinito nel percorso personalizzato. È possibile ottenere i file predefiniti aprendo vari file come descritto in questa sezione.
* È consentito fornire un riferimento assoluto (ad esempio, https://www.example.com/scripts/custom-vertical-fscmenu.css) per qualsiasi file.
* I file JS e CSS necessari per il nodo `div#fscmenu` sono essenziali per la funzionalità della barra degli strumenti. I singoli nodi `ul#fscmenuItem` possono avere o meno file JS o CSS supportati.

**Modifica del valore locale**

Durante la personalizzazione di una barra degli strumenti, è possibile modificare il valore locale della barra degli strumenti. In altre parole, è possibile visualizzarlo in un&#39;altra lingua. La figura seguente mostra una barra degli strumenti personalizzata visualizzata in francese.

>[!NOTE]
>
>Non è possibile creare una barra degli strumenti personalizzata in più lingue. Le barre degli strumenti non possono utilizzare file XML diversi in base alle impostazioni internazionali.

Per modificare il valore locale di una barra degli strumenti, verificare che il file fscmenu.xml contenga la lingua che si desidera visualizzare. La sintassi XML seguente mostra il file fscmenu.xml utilizzato per visualizzare una barra degli strumenti francese.

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
>Gli avvii rapidi associati a questa sezione utilizzano questo file XML per visualizzare una barra degli strumenti personalizzata francese, come illustrato nella figura precedente.

Specificare inoltre un valore valido per le impostazioni locali richiamando il metodo `setLocale` dell&#39;oggetto `HTMLRenderSpec` e passando un valore stringa che specifichi il valore delle impostazioni locali. Ad esempio, passare `fr_FR` per specificare il francese. Il servizio Forms è fornito con barre degli strumenti localizzate.

>[!NOTE]
>
>Prima di eseguire il rendering di un modulo HTML che utilizza una barra degli strumenti personalizzata, è necessario conoscere il rendering dei moduli HTML. (Vedi [Rendering di Forms come HTML](/help/forms/developing/rendering-forms-html.md).)

Per ulteriori informazioni sul servizio Forms, vedere [Riferimento ai servizi per AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Riepilogo dei passaggi {#summary-of-steps}

Per eseguire il rendering di un modulo di HTML contenente una barra degli strumenti personalizzata, eseguire le operazioni seguenti:

1. Includi file di progetto.
1. Crea un oggetto API Java di Forms.
1. Fai riferimento a un file XML fscmenu personalizzato.
1. Eseguire il rendering di un modulo HTML.
1. Scrivere il flusso di dati del modulo nel browser Web client.

**Includi file di progetto**

Includi i file necessari nel progetto di sviluppo. Se stai creando un’applicazione client utilizzando Java, includi i file JAR necessari. Se si utilizzano servizi Web, includere i file proxy.

**Creare un oggetto API Java di Forms**

Prima di poter eseguire a livello di programmazione un&#39;operazione supportata dal servizio Forms, è necessario creare un oggetto client Forms.

**Riferimento a un file XML fscmenu personalizzato**

Per eseguire il rendering di un modulo HTML contenente una barra degli strumenti personalizzata, fare riferimento a un file XML fscmenu che descrive la barra degli strumenti. In questa sezione vengono forniti due esempi di file XML fscmenu. Verificare inoltre che il file fscmenu.xml specifichi correttamente le posizioni di tutti i file di riferimento. Come indicato in precedenza in questa sezione, accertarsi che la parola chiave `FSToolBarURI` o le relative posizioni assolute facciano riferimento a tutti i file.

**Eseguire il rendering di un modulo HTML**

Per eseguire il rendering di un modulo HTML, specifica una struttura di modulo creata in Designer e salvata come file XDP. Selezionate anche un tipo di trasformazione HTML. È ad esempio possibile specificare il tipo di trasformazione HTML che esegue il rendering di un HTML dinamico per Internet Explorer 5.0 o versione successiva.

Il rendering di un modulo HTML richiede anche valori, ad esempio valori URI per il rendering di altri tipi di modulo.

**Scrivere il flusso di dati del modulo nel browser Web client**

Quando il servizio Forms esegue il rendering di un modulo HTML, restituisce un flusso di dati del modulo che è necessario scrivere nel browser Web client per rendere il modulo HTML visibile agli utenti.

**Consulta anche**

[Eseguire il rendering di un modulo HTML con una barra degli strumenti personalizzata utilizzando l’API Java](#render-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Rendering di un modulo HTML con una barra degli strumenti personalizzata tramite l’API del servizio web](#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Guida introduttiva all’API di servizio Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Rendering dei PDF forms interattivi](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Rendering di Forms come HTML](/help/forms/developing/rendering-forms-html.md)

[Creazione di applicazioni Web per il rendering di Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Eseguire il rendering di un modulo HTML con una barra degli strumenti personalizzata utilizzando l’API Java {#render-an-html-form-with-a-custom-toolbar-using-the-java-api}

Esegui il rendering di un modulo HTML contenente una barra degli strumenti personalizzata utilizzando l’API dei servizi Forms (Java):

1. Includi file di progetto

   Includi i file JAR client, ad esempio adobe-forms-client.jar, nel percorso di classe del progetto Java.

1. Creare un oggetto API Java di Forms

   * Creare un oggetto `ServiceClientFactory` contenente le proprietà di connessione.
   * Creare un oggetto `FormsServiceClient` utilizzando il relativo costruttore e passando l&#39;oggetto `ServiceClientFactory`.

1. Riferimento a un file XML fscmenu personalizzato

   * Creare un oggetto `HTMLRenderSpec` utilizzando il relativo costruttore.
   * Per eseguire il rendering di un modulo HTML con una barra degli strumenti, richiamare il metodo `setHTMLToolbar` dell&#39;oggetto `HTMLRenderSpec` e passare un valore enum `HTMLToolbar`. Ad esempio, per visualizzare una barra degli strumenti HTML verticale, passare `HTMLToolbar.Vertical`.
   * Specificare la posizione del file XML fscmenu richiamando il metodo `setToolbarURI` dell&#39;oggetto `HTMLRenderSpec` e passando un valore stringa che specifica la posizione URI del file XML.
   * Se applicabile, impostare il valore delle impostazioni locali richiamando il metodo `setLocale` dell&#39;oggetto `HTMLRenderSpec` e passando un valore stringa che specifica il valore delle impostazioni locali. Il valore predefinito è Inglese.

   >[!NOTE]
   >
   >Il valore di Avvio rapido associato a questa sezione è `fr_FR`*.*

1. Rendering di un modulo HTML

   Richiama il metodo `renderHTMLForm` dell&#39;oggetto `FormsServiceClient` e passa i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura di modulo che fa parte di un&#39;applicazione Forms, assicurarsi di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Valore enum `TransformTo` che specifica il tipo di preferenza HTML. Per eseguire, ad esempio, il rendering di un modulo di HTML compatibile con dynamic HTML per Internet Explorer 5.0 o versione successiva, specificare `TransformTo.MSDHTML`.
   * Oggetto `com.adobe.idp.Document` contenente dati da unire al modulo. Se non si desidera unire i dati, passare un oggetto `com.adobe.idp.Document` vuoto.
   * L&#39;oggetto `HTMLRenderSpec` che memorizza le opzioni di runtime di HTML.
   * Valore stringa che specifica il valore dell&#39;intestazione `HTTP_USER_AGENT`, ad esempio `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * Oggetto `URLSpec` che memorizza i valori URI necessari per il rendering di un modulo HTML.
   * Oggetto `java.util.HashMap` che memorizza gli allegati. Questo è un parametro facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.

   Il metodo `renderHTMLForm` restituisce un oggetto `FormsResult` che contiene un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo nel browser Web client

   * Creare un oggetto `com.adobe.idp.Document` richiamando il metodo `getOutputContent` dell&#39;oggetto `FormsResult`.
   * Ottenere il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document` richiamando il relativo metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamando il relativo metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `com.adobe.idp.Document`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il metodo `getOutputStream` dell&#39;oggetto `javax.servlet.http.HttpServletResponse`.
   * Creare un oggetto `java.io.InputStream` richiamando il metodo `getInputStream` dell&#39;oggetto `com.adobe.idp.Document`.
   * Creare una matrice di byte e popolarla con il flusso di dati del modulo richiamando il metodo `read` dell&#39;oggetto `InputStream` e passando la matrice di byte come argomento.
   * Richiama il metodo `write` dell&#39;oggetto `javax.servlet.ServletOutputStream` per inviare il flusso di dati del modulo al browser Web client. Passare la matrice di byte al metodo `write`.

**Consulta anche**

[Guida rapida (modalità SOAP): rendering di un modulo HTML con una barra degli strumenti personalizzata tramite API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Inclusione dei file della libreria Java di AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Impostazione delle proprietà di connessione](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Rendering di un modulo HTML con una barra degli strumenti personalizzata tramite l’API del servizio web {#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api}

Esegui il rendering di un modulo di HTML contenente una barra degli strumenti personalizzata utilizzando l’API dei servizi Forms (servizio web):

1. Includi file di progetto

   * Creare classi proxy Java che utilizzano il servizio Forms WSDL.
   * Includi le classi proxy Java nel percorso della classe.

1. Creare un oggetto API Java di Forms

   Creare un oggetto `FormsService` e impostare i valori di autenticazione.

1. Riferimento a un file XML fscmenu personalizzato

   * Creare un oggetto `HTMLRenderSpec` utilizzando il relativo costruttore.
   * Per eseguire il rendering di un modulo HTML con una barra degli strumenti, richiamare il metodo `setHTMLToolbar` dell&#39;oggetto `HTMLRenderSpec` e passare un valore enum `HTMLToolbar`. Ad esempio, per visualizzare una barra degli strumenti HTML verticale, passare `HTMLToolbar.Vertical`.
   * Specificare la posizione del file XML fscmenu richiamando il metodo `setToolbarURI` dell&#39;oggetto `HTMLRenderSpec` e passando un valore stringa che specifica la posizione URI del file XML.
   * Se applicabile, impostare il valore delle impostazioni locali richiamando il metodo `setLocale` dell&#39;oggetto `HTMLRenderSpec` e passando un valore stringa che specifica il valore delle impostazioni locali. Il valore predefinito è Inglese.

   >[!NOTE]
   >
   >Il valore di Avvio rapido associato a questa sezione è `fr_FR`*.*

1. Rendering di un modulo HTML

   Richiama il metodo `renderHTMLForm` dell&#39;oggetto `FormsService` e passa i seguenti valori:

   * Valore stringa che specifica il nome della struttura del modulo, inclusa l&#39;estensione del nome file. Se si fa riferimento a una struttura di modulo che fa parte di un&#39;applicazione Forms, assicurarsi di specificare il percorso completo, ad esempio `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Valore enum `TransformTo` che specifica il tipo di preferenza HTML. Per eseguire, ad esempio, il rendering di un modulo di HTML compatibile con dynamic HTML per Internet Explorer 5.0 o versione successiva, specificare `TransformTo.MSDHTML`.
   * Oggetto `BLOB` contenente dati da unire al modulo. Se non si desidera unire i dati, passare `null`.
   * L&#39;oggetto `HTMLRenderSpec` che memorizza le opzioni di runtime di HTML.
   * Valore stringa che specifica il valore dell&#39;intestazione `HTTP_USER_AGENT`, ad esempio `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322`). Se non si desidera impostare questo valore, è possibile passare una stringa vuota.
   * Oggetto `URLSpec` che memorizza i valori URI necessari per il rendering di un modulo HTML.
   * Oggetto `java.util.HashMap` che memorizza gli allegati. Questo parametro è facoltativo ed è possibile specificare `null` se non si desidera allegare file al modulo.
   * Oggetto `com.adobe.idp.services.holders.BLOBHolder` vuoto popolato dal metodo `renderHTMLForm`. Questo valore di parametro memorizza il modulo di cui è stato eseguito il rendering.
   * Oggetto `com.adobe.idp.services.holders.BLOBHolder` vuoto popolato dal metodo `renderHTMLForm`. Questo parametro memorizza i dati XML di output.
   * Oggetto `javax.xml.rpc.holders.LongHolder` vuoto popolato dal metodo `renderHTMLForm`. Questo argomento memorizza il numero di pagine nel modulo.
   * Oggetto `javax.xml.rpc.holders.StringHolder` vuoto popolato dal metodo `renderHTMLForm`. Questo argomento memorizza il valore locale.
   * Oggetto `javax.xml.rpc.holders.StringHolder` vuoto popolato dal metodo `renderHTMLForm`. Questo argomento memorizza il valore di rendering HTML utilizzato.
   * Oggetto `com.adobe.idp.services.holders.FormsResultHolder` vuoto che conterrà i risultati dell&#39;operazione.

   Il metodo `renderHTMLForm` popola l&#39;oggetto `com.adobe.idp.services.holders.FormsResultHolder` passato come ultimo valore di argomento con un flusso di dati del modulo che deve essere scritto nel browser Web client.

1. Scrivere il flusso di dati del modulo nel browser Web client

   * Creare un oggetto `FormResult` ottenendo il valore del membro dati `value` dell&#39;oggetto `com.adobe.idp.services.holders.FormsResultHolder`.
   * Creare un oggetto `BLOB` contenente dati del modulo richiamando il metodo `getOutputContent` dell&#39;oggetto `FormsResult`.
   * Ottenere il tipo di contenuto dell&#39;oggetto `BLOB` richiamando il relativo metodo `getContentType`.
   * Impostare il tipo di contenuto dell&#39;oggetto `javax.servlet.http.HttpServletResponse` richiamando il relativo metodo `setContentType` e passando il tipo di contenuto dell&#39;oggetto `BLOB`.
   * Creare un oggetto `javax.servlet.ServletOutputStream` utilizzato per scrivere il flusso di dati del modulo nel browser Web client richiamando il metodo `getOutputStream` dell&#39;oggetto `javax.servlet.http.HttpServletResponse`.
   * Creare una matrice di byte e popolarla richiamando il metodo `getBinaryData` dell&#39;oggetto `BLOB`. Questa attività assegna il contenuto dell&#39;oggetto `FormsResult` alla matrice di byte.
   * Richiama il metodo `write` dell&#39;oggetto `javax.servlet.http.HttpServletResponse` per inviare il flusso di dati del modulo al browser Web client. Passare la matrice di byte al metodo `write`.

**Consulta anche**

[Richiamare AEM Forms utilizzando la codifica Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
