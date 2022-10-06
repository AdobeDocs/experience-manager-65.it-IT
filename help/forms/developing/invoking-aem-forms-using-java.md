---
title: Richiamo di AEM Forms tramite JavaAPI
seo-title: Invoking AEM Forms using the JavaAPI
description: Utilizza l'API Java di AEM Forms per il protocollo di trasporto RMI per la chiamata remota, il trasporto VM per la chiamata locale, SOAP per la chiamata remota, l'autenticazione diversa, come nome utente e password, e le richieste di chiamata sincrone e asincrona.
seo-description: Use the AEM Forms Java API for RMI transport protocol for remote invocation, VM transport for local invocation, SOAP for remote invocation, different authentication, such as user name and password, and synchronous and asynchronous invocation requests.
uuid: 5e2fef2a-05f3-4283-8fd3-2d7dca411000
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 0e6e7850-6137-42c5-b8e2-d4e352fddae2
role: Developer
exl-id: 036c35c1-1be7-4825-bbb6-ea025e49c6f6
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '5398'
ht-degree: 0%

---

# Richiamo di AEM Forms tramite l’API Java {#invoking-aem-forms-using-the-javaapi}

**Esempi ed esempi in questo documento sono solo per AEM Forms in ambiente JEE.**

AEM Forms può essere richiamato utilizzando l’API Java di AEM Forms. Quando utilizzi l’API Java di AEM Forms, puoi utilizzare l’API di richiamo o le librerie client Java. Le librerie client Java sono disponibili per servizi come il servizio Rights Management. Queste API fortemente tipizzate consentono di sviluppare applicazioni Java che richiamano AEM Forms.

L&#39;API di richiamo sono classi che si trovano nella `com.adobe.idp.dsc` pacchetto. Utilizzando queste classi, puoi inviare una richiesta di chiamata direttamente a un servizio e gestire una risposta di chiamata restituita. Utilizza l’API di richiamo per invocare processi di breve durata o di lunga durata creati utilizzando Workbench.

Il modo consigliato per richiamare un servizio in modo programmatico è quello di utilizzare una libreria client Java corrispondente al servizio anziché l’API di chiamata. Ad esempio, per richiamare il servizio Crittografia, utilizzare la libreria client del servizio Crittografia. Per eseguire un&#39;operazione del servizio di cifratura, richiamare un metodo appartenente all&#39;oggetto client del servizio di cifratura. È possibile crittografare un documento PDF con una password richiamando il `EncryptionServiceClient` dell’oggetto `encryptPDFUsingPassword` metodo .

L’API Java supporta le seguenti funzioni:

* Protocollo di trasporto RMI per chiamata remota
* Trasporto VM per chiamata locale
* SOAP per chiamata remota
* Autenticazione diversa, ad esempio nome utente e password
* Richieste di chiamata sincrone e asincrona

[Inclusione dei file libreria Java di AEM Forms](#including-aem-forms-java-library-files)

[Richiamo dei processi a lunga durata incentrati sull&#39;uomo](invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Richiamo di AEM Forms tramite i servizi web](/help/forms/developing/invoking-aem-forms-using-web.md)

[Impostazione delle proprietà di connessione](#setting-connection-properties)

[Trasmissione di dati ai servizi AEM Forms tramite l’API Java](#passing-data-to-aem-forms-services-using-the-java-api)

[Richiamo di un servizio tramite una libreria client Java](#invoking-a-service-using-a-java-client-library)

[Richiamare un processo di breve durata utilizzando l’API di richiamo](#invoking-a-short-lived-process-using-the-invocation-api)

[Creazione di un&#39;applicazione web Java che richiama un processo longevo incentrato sull&#39;uomo](/help/forms/developing/invoking-human-centric-long-lived.md)

## Inclusione dei file libreria Java di AEM Forms {#including-aem-forms-java-library-files}

Per richiamare un servizio AEM Forms a livello di programmazione utilizzando l’API Java, includi i file di libreria richiesti (file JAR) nel percorso di classe del progetto Java. I file JAR inclusi nel percorso di classe dell&#39;applicazione client dipendono da diversi fattori:

* Servizio AEM Forms da richiamare. Un&#39;applicazione client può richiamare uno o più servizi.
* Modalità in cui si desidera richiamare un servizio AEM Forms. È possibile utilizzare la modalità EJB o SOAP. (Vedi [Impostazione delle proprietà di connessione](invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>(Solo chiavi in mano) Avvia il server AEM Forms con il comando `standalone.bat -b <Server IP> -c lc_turnkey.xml` per specificare un IP server per EJB

* Server dell&#39;applicazione J2EE su cui viene distribuito AEM Forms.

### File JAR specifici del servizio {#service-specific-jar-files}

Nella tabella seguente sono elencati i file JAR necessari per richiamare i servizi AEM Forms.

<table>
 <thead>
  <tr>
   <th><p>File</p></th>
   <th><p>Descrizione</p></th>
   <th><p>Dove si trova</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>adobe-livecycle-client.jar</p></td>
   <td><p>Deve essere sempre incluso nel percorso classe di un'applicazione client Java.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-usermanager-client.jar</p></td>
   <td><p>Deve essere sempre incluso nel percorso classe di un'applicazione client Java.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-utilities.jar</p></td>
   <td><p>Deve essere sempre incluso nel percorso classe di un'applicazione client Java.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk//client-libs/&lt;app server=""&gt;</p></td>
  </tr>
  <tr>
   <td><p>adobe-applicationmanager-client-sdk.jar</p></td>
   <td><p>Richiesto per richiamare il servizio Application Manager.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-assembler-client.jar</p></td>
   <td><p>Richiesto per richiamare il servizio Assembler. </p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-backup-restore-client-sdk.jar</p></td>
   <td><p>Richiesto per richiamare l'API del servizio Backup e ripristino.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-barcodedforms-client.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio moduli con codice a barre. </p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-convertpdf-client.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio Convert PDF. </p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-distiller-client.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio Distiller.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-docconverter-client.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio DocConverter.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-contentservices-client.jar</p></td>
   <td><p>Richiesto per richiamare il servizio Gestione documenti.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-encryption-client.jar</p></td>
   <td><p>Richiesto per richiamare il servizio di cifratura.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-forms-client.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio Forms.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-formdataintegration-client.jar</p></td>
   <td><p>Richiesto per richiamare il servizio di integrazione dei dati del modulo.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generatepdf-client.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio Generate PDF.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-generate3dpdf-client.jar</p></td>
   <td><p>Richiesto per richiamare il servizio Generate 3D PDF.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-jobmanager-client-sdk.jar</p></td>
   <td><p>Richiesto per richiamare il servizio Job Manager. </p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-output-client.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio Output.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-pdfutility-client.jar</p></td>
   <td><p>Richiesto per richiamare il servizio Utilità di PDF o Utilità di XMP.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-reader-extensions-client.jar</p></td>
   <td><p>Richiesto per richiamare il servizio Acrobat Reader DC extensions.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-repository-client.jar</p><p>commons-codec-1.3.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio Repository.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs\thirdparty</p></td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><p>adobe-rightsmanagement-client.jar</p></li>
     <li><p>namespace.jar</p></li>
     <li><p>jaxb-api.jar</p></li>
     <li><p>jaxb-impl.jar</p></li>
     <li><p>jaxb-libs.jar</p></li>
     <li><p>jaxb-xjc.jar</p></li>
     <li><p>relaxngDatatype.jar</p></li>
     <li><p>xsdlib.jar</p></li>
    </ul></td>
   <td><p>Obbligatorio per richiamare il servizio Rights Management.</p><p>Se AEM Forms è implementato su JBoss, includi tutti questi file. </p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p><p>Directory lib specifica per JBoss</p></td>
  </tr>
  <tr>
   <td><p>adobe-signatures-client.jar</p></td>
   <td><p>Obbligatorio per richiamare il servizio Firma.</p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-taskmanager-client-sdk.jar</p></td>
   <td><p>Richiesto per richiamare il servizio Task Manager. </p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
  <tr>
   <td><p>adobe-truststore-client.jar</p></td>
   <td><p>Richiesto per richiamare il servizio Trust Store. </p></td>
   <td><p>&lt;<i>directory di installazione</i>&gt;/sdk/client-libs/common</p></td>
  </tr>
 </tbody>
</table>

### Modalità di connessione e file JAR dell&#39;applicazione J2EE {#connection-mode-and-j2ee-application-jar-files}

Nella tabella seguente sono elencati i file JAR che dipendono dalla modalità di connessione e il server dell&#39;applicazione J2EE su cui viene distribuito AEM Forms.

<table>
 <thead>
  <tr>
   <th><p>File</p> </th>
   <th><p>Descrizione</p> </th>
   <th><p>Dove si trova</p> </th>
  </tr>
 &lt;/thead align="left"&gt;
 <tbody>
  <tr>
   <td>
    <ul>
     <li><p>activation.jar</p> </li>
     <li><p>axis.jar</p> </li>
     <li><p>commons-codec-1.3.jar</p> </li>
     <li><p>commons-collections-3.1.jar</p> </li>
     <li><p>commons-discovery.jar</p> </li>
     <li><p>commons-logging.jar</p> </li>
     <li><p>dom3-xml-apis-2.5.0.jar</p> </li>
     <li><p>jaxen-1.1-beta-9.jar</p> </li>
     <li><p>jaxrpc.jar</p> </li>
     <li><p>log4j.jar</p> </li>
     <li><p>mail.jar</p> </li>
     <li><p>saaj.jar</p> </li>
     <li><p>wsdl4j.jar</p> </li>
     <li><p>xalan.jar</p> </li>
     <li><p>xbean.jar</p> </li>
    </ul>
    <ul>
     <li>xercesImpl.jar<br /> </li>
     <li>commons-httpclient-3.1.jar</li>
    </ul> <p> </p> </td>
   <td><p>se AEM Forms viene richiamato utilizzando la modalità SOAP, includi questi file JAR.</p> </td>
   <td><p>&lt;<em>directory di installazione</em>&gt;/sdk/client-libs/thirdparty</p> </td>
  </tr>
  <tr>
   <td><p> jboss-client.jar</p> </td>
   <td><p>se AEM Forms è distribuito su JBoss Application Server, includi questo file JAR.</p> <p>Le classi richieste non verranno trovate dal classloader se jboss-client.jar e i jar a cui si fa riferimento non sono co-localizzati.</p> </td>
   <td><p>Directory lib client JBoss</p> <p>Se distribuisci l’applicazione client sullo stesso server applicativo J2EE, non è necessario includere questo file.</p> </td>
  </tr>
  <tr>
   <td><p>wlclient.jar</p> </td>
   <td><p>se AEM Forms è implementato su BEA WebLogic Server®, includi questo file JAR.</p> </td>
   <td><p>Directory lib specifica per WebLogic</p> <p>Se distribuisci l’applicazione client sullo stesso server applicativo J2EE, non è necessario includere questo file.</p> </td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><p>com.ibm.ws.admin.client_6.1.0.jar</p> </li>
     <li><p>com.ibm.ws.webservices.thinclient_6.1.0.jar</p> </li>
    </ul> </td>
   <td>
    <ul>
     <li><p>se AEM Forms è distribuito su WebSphere Application Server, includi questi file JAR.</p> </li>
     <li><p>(com.ibm.ws.webservices.thinclient_6.1.0.jar è necessario per la chiamata al servizio Web).</p> </li>
    </ul> </td>
   <td><p>Directory lib specifica per WebSphere (<em>[WAS_HOME]</em>/runtime)</p> <p>Se si distribuisce l'applicazione client sullo stesso server applicativo J2EE, non è necessario includere questi file.</p> </td>
  </tr>
 </tbody>
</table>

### Richiamo degli scenari {#invoking-scenarios}

La tabella seguente specifica gli scenari di chiamata ed elenca i file JAR necessari per richiamare AEM Forms con successo.

<table>
 <thead>
  <tr>
   <th><p>Servizi</p> </th>
   <th><p>Modalità di incitazione</p> </th>
   <th><p>Server applicazioni J2EE</p> </th>
   <th><p>File JAR richiesti</p> </th>
  </tr>
 &lt;/thead align="left"&gt;
 <tbody>
  <tr>
   <td><p>Servizio Forms</p> </td>
   <td><p>EJB</p> </td>
   <td><p>JBoss</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
    </ul>
    <ul>
     <li>jboss-client.jar</li>
    </ul>
    <ul>
     <li>adobe-forms-client.jar<br /> </li>
     <li>commons-httpclient-3.1.jar</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Servizio Forms</p> <p>Servizio estensioni Acrobat Reader DC</p> <p>Servizio di firma</p> </td>
   <td><p>EJB</p> </td>
   <td><p>JBoss</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
    </ul>
    <ul>
     <li>jboss-client.jar<br /> </li>
     <li>commons-httpclient-3.1.jar</li>
    </ul>
    <ul>
     <li><p>adobe-forms-client.jar</p> </li>
     <li><p>adobe-reader-extensions-client.jar</p> </li>
     <li><p>adobe-signatures-client.jar</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Servizio Forms</p> </td>
   <td><p>SOAP</p> </td>
   <td><p>WebLogic</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
     <li><p>wlclient.jar</p> </li>
     <li><p>activation.jar</p> </li>
     <li><p>axis.jar</p> </li>
     <li><p>commons-codec-1.3.jar</p> </li>
     <li><p>commons-collections-3.1.jar</p> </li>
     <li><p>commons-discovery.jar</p> </li>
     <li><p>commons-logging.jar</p> </li>
     <li><p>dom3-xml-apis-2.5.0.jar</p> </li>
     <li><p>jai_imageio.jar</p> </li>
     <li><p>jaxen-1.1-beta-9.jar</p> </li>
     <li><p>jaxrpc.jar</p> </li>
     <li><p>log4j.jar</p> </li>
     <li><p>mail.jar</p> </li>
     <li><p>saaj.jar</p> </li>
     <li><p>wsdl4j.jar</p> </li>
     <li><p>xalan.jar</p> </li>
     <li><p>xbean.jar</p> </li>
     <li><p>xercesImpl.jar</p> </li>
     <li><p>adobe-forms-client.jar</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Servizio Forms</p> <p>Servizio estensioni Acrobat Reader DC</p> <p>Servizio di firma</p> </td>
   <td><p>SOAP</p> </td>
   <td><p>WebLogic</p> </td>
   <td>
    <ul>
     <li><p>adobe-livecycle-client.jar</p> </li>
     <li><p>adobe-usermanager-client.jar</p> </li>
     <li><p>wlclient.jar</p> </li>
     <li><p>activation.jar</p> </li>
     <li><p>axis.jar</p> </li>
     <li><p>commons-codec-1.3.jar</p> </li>
     <li><p>commons-collections-3.1.jar</p> </li>
     <li><p>commons-discovery.jar</p> </li>
     <li><p>commons-logging.jar</p> </li>
     <li><p>dom3-xml-apis-2.5.0.jar</p> </li>
     <li><p>jai_imageio.jar</p> </li>
     <li><p>jaxen-1.1-beta-9.jar</p> </li>
     <li><p>jaxrpc.jar</p> </li>
     <li><p>log4j.jar</p> </li>
     <li><p>mail.jar</p> </li>
     <li><p>saaj.jar</p> </li>
     <li><p>wsdl4j.jar</p> </li>
     <li><p>xalan.jar</p> </li>
     <li><p>xbean.jar</p> </li>
     <li><p>xercesImpl.jar</p> </li>
     <li><p>adobe-forms-client.jar</p> </li>
     <li><p>adobe-reader-extensions-client.jar</p> </li>
     <li><p>adobe-signatures-client.jar</p> </li>
    </ul> </td>
  </tr> xmp-uti
 </tbody>
</table>

### Aggiornamento dei file JAR {#upgrading-jar-files}

Se esegui l’aggiornamento da LiveCycle ad AEM Forms, si consiglia di includere i file JAR di AEM Forms nel percorso di classe del progetto Java. Ad esempio, se utilizzi servizi come il servizio Rights Management, incontri un problema di compatibilità se non includi file JAR AEM Forms nel percorso della classe.

Presupponendo che tu stia eseguendo l’aggiornamento ad AEM Forms. Per utilizzare un&#39;applicazione Java che richiama il servizio Rights Management, includi le versioni AEM Forms dei seguenti file JAR:

* adobe-rightsmanagement-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar

**Consulta anche**

[Richiamo di AEM Forms tramite l’API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Impostazione delle proprietà di connessione](invoking-aem-forms-using-java.md#setting-connection-properties)

[Trasmissione di dati ai servizi AEM Forms tramite l’API Java](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Richiamo di un servizio tramite una libreria client Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Impostazione delle proprietà di connessione {#setting-connection-properties}

È possibile impostare le proprietà di connessione per richiamare AEM Forms quando si utilizza l’API Java. Quando si impostano le proprietà di connessione, specificare se richiamare i servizi in remoto o in locale, nonché specificare la modalità di connessione e i valori di autenticazione. I valori di autenticazione sono necessari se la sicurezza del servizio è abilitata. Tuttavia, se la sicurezza del servizio è disabilitata, non è necessario specificare i valori di autenticazione.

La modalità di connessione può essere SOAP o EJB. La modalità EJB utilizza il protocollo RMI/IIOP e le prestazioni della modalità EJB sono migliori delle prestazioni della modalità SOAP. La modalità SOAP viene utilizzata per eliminare una dipendenza da un server applicativo J2EE o quando si trova un firewall tra AEM Forms e l’applicazione client. La modalità SOAP utilizza il protocollo https come trasporto sottostante e può comunicare tra i limiti del firewall. Se né una dipendenza da un server applicazioni J2EE né un firewall sono un problema, si consiglia di utilizzare la modalità EJB.

Per richiamare correttamente un servizio AEM Forms, imposta le seguenti proprietà di connessione:

* **DSC_DEFAULT_EJB_ENDPOINT:** Se utilizzi la modalità di connessione EJB, questo valore rappresenta l’URL del server dell’applicazione J2EE in cui viene distribuito AEM Forms. Per richiamare AEM Forms in remoto, specifica il nome del server dell&#39;applicazione J2EE in cui viene distribuito AEM Forms. Se l&#39;applicazione client si trova sullo stesso server applicativo J2EE, è possibile specificare `localhost`. A seconda del server applicazioni J2EE su cui è distribuito AEM Forms, specifica uno dei seguenti valori:

   * JBoss: `https://<ServerName>:8080 (default port)`
   * WebSphere: `iiop://<ServerName>:2809 (default port)`
   * WebLogic: `t3://<ServerName>:7001 (default port)`

* **DSC_DEFAULT_SOAP_ENDPOINT**: Se si utilizza la modalità di connessione SOAP, questo valore rappresenta l’endpoint a cui viene inviata una richiesta di chiamata. Per richiamare AEM Forms in remoto, specifica il nome del server dell&#39;applicazione J2EE in cui viene distribuito AEM Forms. Se l&#39;applicazione client si trova sullo stesso server applicativo J2EE, è possibile specificare `localhost` (ad esempio, `http://localhost:8080`.)

   * Valore della porta `8080` è applicabile se l’applicazione J2EE è JBoss. Se il server applicazioni J2EE è IBM® WebSphere®, utilizza la porta `9080`. Allo stesso modo, se il server dell&#39;applicazione J2EE è WebLogic, utilizza la porta `7001`. Questi valori sono valori di porta predefiniti. Se si modifica il valore della porta, utilizzare il numero di porta applicabile.)

* **DSC_TRANSPORT_PROTOCOL**: Se utilizzi la modalità di connessione EJB, specifica `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` per questo valore. Se si utilizza la modalità di connessione SOAP, specificare `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`.
* **DSC_SERVER_TYPE**: Specifica il server applicazioni J2EE in cui viene distribuito AEM Forms. I valori validi sono `JBoss`, `WebSphere`, `WebLogic`.

   * Se si imposta questa proprietà di connessione su `WebSphere`, `java.naming.factory.initial` è impostato su `com.ibm.ws.naming.util.WsnInitCtxFactory`.
   * Se si imposta questa proprietà di connessione su `WebLogic`, `java.naming.factory.initial` è impostato su `weblogic.jndi.WLInitialContextFactory`.
   * Analogamente, se si imposta questa proprietà di connessione su `JBoss`, `java.naming.factory.initial` è impostato su `org.jnp.interfaces.NamingContextFactory`.
   * È possibile impostare `java.naming.factory.initial` su un valore che soddisfa le tue esigenze se non desideri utilizzare i valori predefiniti.

   >[!NOTE]
   >
   >Invece di utilizzare una stringa per impostare `DSC_SERVER_TYPE` proprietà di connessione, è possibile utilizzare un membro statico del `ServiceClientFactoryProperties` classe. È possibile utilizzare i seguenti valori: `ServiceClientFactoryProperties.DSC_WEBSPHERE_SERVER_TYPE`, `ServiceClientFactoryProperties.DSC_WEBLOGIC_SERVER_TYPE`oppure `ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE`.

* **DSC_CREDENTIAL_USERNAME:** Specifica il nome utente del modulo AEM. Affinché un utente possa richiamare correttamente un servizio AEM Forms, deve disporre del ruolo Utente servizi . Un utente può anche avere un altro ruolo che include l&#39;autorizzazione Richiamo assistenza. In caso contrario, viene generata un&#39;eccezione quando si tenta di richiamare un servizio. Se la protezione del servizio è disabilitata, non è necessario specificare questa proprietà di connessione.
* **DSC_CREDENTIAL_PASSWORD:** Specifica il valore della password corrispondente. Se la protezione del servizio è disabilitata, non è necessario specificare questa proprietà di connessione.
* **DSC_REQUEST_TIMEOUT:** Il limite di timeout predefinito della richiesta SOAP è di 1200000 millisecondi (20 minuti). A volte, una richiesta può richiedere più tempo per completare l’operazione. Ad esempio, una richiesta SOAP che recupera un set di record di grandi dimensioni può richiedere un limite di timeout più lungo. È possibile utilizzare `ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT` per aumentare il limite di timeout della richiesta per le richieste SOAP.

   **nota**: Solo le chiamate basate su SOAP supportano la proprietà DSC_REQUEST_TIMEOUT .

Per impostare le proprietà di connessione, eseguire le operazioni seguenti:

1. Crea un `java.util.Properties` utilizzando il relativo costruttore.
1. Per impostare `DSC_DEFAULT_EJB_ENDPOINT` proprietà di connessione, richiamare `java.util.Properties` dell’oggetto `setProperty` e passare i seguenti valori:

   * La `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT` valore di enumerazione
   * Valore stringa che specifica l&#39;URL del server dell&#39;applicazione J2EE che ospita AEM Forms

   >[!NOTE]
   >
   >Se si utilizza la modalità di connessione SOAP, specificare la `ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT` valore di enumerazione invece del `ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT` valore di enumerazione.

1. Per impostare `DSC_TRANSPORT_PROTOCOL` proprietà di connessione, richiamare `java.util.Properties` dell’oggetto `setProperty` e passare i seguenti valori:

   * La `ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL` valore di enumerazione
   * La `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` valore di enumerazione

   >[!NOTE]
   >
   >Se si utilizza la modalità di connessione SOAP, specificare la `ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL`valore di enumerazione invece del `ServiceClientFactoryProperties.DSC_EJB_PROTOCOL` valore di enumerazione.

1. Per impostare `DSC_SERVER_TYPE` proprietà di connessione, richiamare `java.util.Properties` dell’oggetto `setProperty` e passare i seguenti valori:

   * La `ServiceClientFactoryProperties.DSC_SERVER_TYPE`valore di enumerazione
   * Un valore stringa che specifica il server applicazioni J2EE che ospita AEM Forms (ad esempio, se AEM Forms è distribuito su JBoss, specificare `JBoss`).

      1. Per impostare `DSC_CREDENTIAL_USERNAME` proprietà di connessione, richiamare `java.util.Properties` dell’oggetto `setProperty` e passare i seguenti valori:
   * La `ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME` valore di enumerazione
   * Valore stringa che specifica il nome utente necessario per richiamare AEM Forms

      1. Per impostare `DSC_CREDENTIAL_PASSWORD` proprietà di connessione, richiamare `java.util.Properties` dell’oggetto `setProperty` e passare i seguenti valori:
   * La `ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD` valore di enumerazione
   * Valore stringa che specifica il valore della password corrispondente



**Impostazione della modalità di connessione EJB per JBoss**

L&#39;esempio di codice Java seguente imposta le proprietà di connessione per richiamare AEM Forms distribuito su JBoss e utilizzando la modalità di connessione EJB.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "https://<hostname>:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DOCUMENT_HTTP_ENDPOINT,"https://<hostname>:8080");
```

**Impostazione della modalità di connessione EJB per WebLogic**

L&#39;esempio di codice Java seguente imposta le proprietà di connessione per richiamare AEM Forms distribuito su WebLogic e utilizzando la modalità di connessione EJB.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "t3://localhost:7001");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebLogic");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**Impostazione della modalità di connessione EJB per WebSphere**

L&#39;esempio di codice Java seguente imposta le proprietà di connessione per richiamare AEM Forms distribuito su WebSphere e utilizzando la modalità di connessione EJB.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "iiop://localhost:2809");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "WebSphere");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

**Impostazione della modalità di connessione SOAP**

L&#39;esempio di codice Java seguente imposta le proprietà di connessione in modalità SOAP per richiamare AEM Forms distribuito su JBoss.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://localhost:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
```

>[!NOTE]
>
>Se selezioni la modalità di connessione SOAP, assicurati di includere ulteriori file JAR nel percorso di classe dell’applicazione client.

**Impostazione delle proprietà di connessione quando la protezione del servizio è disabilitata**

L&#39;esempio di codice Java seguente imposta le proprietà di connessione necessarie per richiamare AEM Forms distribuito su JBoss Application Server e quando la sicurezza del servizio è disabilitata.

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://localhost:1099");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
```

>[!NOTE]
>
>Tutti i Java Quick Starts associati alla programmazione con AEM Forms mostrano le impostazioni di connessione EJB e SOAP.

**Impostazione della modalità di connessione SOAP con limite di timeout della richiesta personalizzato**

```java
 Properties ConnectionProps = new Properties();
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "http://localhost:8080");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
 ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
ConnectionProps.setProperty(ServiceClientFactoryProperties.DSC_REQUEST_TIMEOUT, "1800000"); // Request timeout limit 30 Minutes
```

**Utilizzo di un oggetto Context per richiamare AEM Forms**

Puoi utilizzare un `com.adobe.idp.Context` per richiamare un servizio AEM Forms con un utente autenticato (il `com.adobe.idp.Context` rappresenta un utente autenticato). Quando si utilizza un `com.adobe.idp.Context` non è necessario impostare `DSC_CREDENTIAL_USERNAME` o `DSC_CREDENTIAL_PASSWORD` proprietà. Puoi ottenere un `com.adobe.idp.Context` durante l&#39;autenticazione degli utenti utilizzando il `AuthenticationManagerServiceClient` dell’oggetto `authenticate` metodo .

La `authenticate` restituisce un `AuthResult` oggetto che contiene i risultati dell&#39;autenticazione. Puoi creare una `com.adobe.idp.Context` richiamando il relativo costruttore. Quindi invoca il `com.adobe.idp.Context` dell’oggetto `initPrincipal` e passare il `AuthResult` come mostrato nel codice seguente:

```java
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
```

Invece di impostare `DSC_CREDENTIAL_USERNAME` o `DSC_CREDENTIAL_PASSWORD` è possibile richiamare le proprietà `ServiceClientFactory` dell’oggetto `setContext` e passare il `com.adobe.idp.Context` oggetto. Quando utilizzi un utente di moduli AEM per richiamare un servizio, assicurati che il ruolo sia denominato `Services User` necessaria per richiamare un servizio AEM Forms.

L&#39;esempio di codice seguente mostra come utilizzare un `com.adobe.idp.Context` oggetto all&#39;interno delle impostazioni di connessione utilizzate per creare un `EncryptionServiceClient` oggetto.

```java
 //Authenticate a user and use the Context object within connection settings
 // Authenticate the user
 String username = "wblue";
 String password = "password";
 AuthResult authResult = authClient.authenticate(username, password.getBytes());
 
 //Set a Content object that represents the authenticated user
 //Use the Context object to invoke the Encryption service
 Context myCtx = new Context();
 myCtx.initPrincipal(authResult);
 
 //Set connection settings
 Properties connectionProps = new Properties();
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://<server>:1099");
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL, ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE);
 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DOCUMENT_HTTP_ENDPOINT,"jnp://<server>:1099");

 
 //Create a ServiceClientFactory object
 ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 myFactory.setContext(myCtx);
 
 //Create an EncryptionServiceClient object
 EncryptionServiceClient encryptClient  = new EncryptionServiceClient(myFactory);
```

>[!NOTE]
>
>Per informazioni complete sull&#39;autenticazione di un utente, vedi [Autenticazione degli utenti](/help/forms/developing/users.md#authenticating-users).

### Richiamo degli scenari {#invoking_scenarios-1}

In questa sezione sono descritti i seguenti scenari di chiamata:

* Un&#39;applicazione client in esecuzione nella propria macchina virtuale Java (JVM) richiama un&#39;istanza autonoma di AEM Forms.
* Un&#39;applicazione client in esecuzione nella propria JVM richiama le istanze AEM Forms del cluster.

### Applicazione client che richiama un&#39;istanza autonoma di AEM Forms {#client-application-invoking-a-stand-alone-aem-forms-instance}

Il diagramma seguente mostra un&#39;applicazione client in esecuzione nella propria JVM e che richiama un&#39;istanza autonoma di AEM Forms.

In questo scenario, un&#39;applicazione client è in esecuzione nella propria JVM e richiama i servizi AEM Forms.

>[!NOTE]
>
>Questo scenario è lo scenario di richiamo su cui si basano tutti gli avvii rapidi.

### Applicazione client che richiama istanze AEM Forms in cluster {#client-application-invoking-clustered-aem-forms-instances}

Il diagramma seguente mostra un&#39;applicazione client in esecuzione nella propria JVM e che richiama le istanze AEM Forms situate in un cluster.

Questo scenario è simile a un&#39;applicazione client che richiama un&#39;istanza autonoma di AEM Forms. Tuttavia, l’URL del provider è diverso. Se un&#39;applicazione client desidera connettersi a un server applicativo J2EE specifico, l&#39;applicazione deve modificare l&#39;URL per fare riferimento al server applicativo J2EE specifico.

Non è consigliabile fare riferimento a un server applicazioni J2EE specifico perché la connessione tra l&#39;applicazione client e AEM Forms viene terminata se il server applicazioni si arresta. È consigliabile che l&#39;URL del provider faccia riferimento a un gestore JNDI a livello di cella, invece di un server applicativo J2EE specifico.

Le applicazioni client che utilizzano la modalità di connessione SOAP possono utilizzare la porta di bilanciamento del carico HTTP per il cluster. Le applicazioni client che utilizzano la modalità di connessione EJB possono connettersi alla porta EJB di un server applicativo J2EE specifico. Questa azione gestisce il bilanciamento del carico tra i nodi del cluster.

**WebSphere**

L&#39;esempio seguente mostra il contenuto di un file jndi.properties utilizzato per connettersi ad AEM Forms distribuito su WebSphere.

```ini
 java.naming.factory.initial=com.ibm.websphere.naming.
 WsnInitialContextFactory
 java.naming.provider.url=corbaloc::appserver1:9810,:appserver2:9810
```

**WebLogic**

L’esempio seguente mostra il contenuto di un file jndi.properties utilizzato per connettersi ad AEM Forms distribuito su WebLogic.

```ini
 java.naming.factory.initial=weblogic.jndi.WLInitialContextFactory
 java.naming.provider.url=t3://appserver1:8001, appserver2:8001
```

**JBoss**

L&#39;esempio seguente mostra il contenuto di un file jndi.properties utilizzato per connettersi ad AEM Forms distribuito su JBoss.

```ini
 java.naming.factory.initial= org.jnp.interfaces.NamingContextFactory
 java.naming.provider.url= jnp://appserver1:1099, appserver2:1099,
 appserver3:1099
```

>[!NOTE]
>
>Rivolgersi all&#39;amministratore per determinare il nome e il numero di porta dell&#39;applicazione J2EE.

**Consulta anche**

[Inclusione dei file libreria Java di AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Trasmissione di dati ai servizi AEM Forms tramite l’API Java](invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)

[Richiamo di un servizio tramite una libreria client Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Trasmissione di dati ai servizi AEM Forms tramite l’API Java {#passing-data-to-aem-forms-services-using-the-java-api}

Le operazioni del servizio AEM Forms in genere consumano o producono documenti PDF. Quando si richiama un servizio, a volte è necessario passare al servizio un documento PDF (o altri tipi di documento come i dati XML). Allo stesso modo, a volte è necessario gestire un documento PDF restituito dal servizio. La classe Java che ti consente di trasmettere dati a e dai servizi AEM Forms è `com.adobe.idp.Document`.

I servizi AEM Forms non accettano un documento PDF come altri tipi di dati, ad esempio un `java.io.InputStream` oggetto o array di byte. A `com.adobe.idp.Document` L&#39;oggetto può essere utilizzato anche per trasmettere ai servizi altri tipi di dati, ad esempio dati XML.

A `com.adobe.idp.Document` l&#39;oggetto è un tipo serializzabile Java, quindi può essere trasmesso sopra una chiamata RMI. Il lato ricevente può essere collocato (lo stesso host, lo stesso caricatore di classe), locale (lo stesso host, un caricatore di classe diverso) o remoto (un host diverso). Il passaggio del contenuto del documento è ottimizzato per ogni caso. Ad esempio, se il mittente e il destinatario si trovano sullo stesso host, il contenuto viene trasmesso su un file system locale. (In alcuni casi, i documenti possono essere passati in memoria.)

A seconda del `com.adobe.idp.Document` dimensioni dell’oggetto, i dati vengono trasferiti all’interno della `com.adobe.idp.Document` o memorizzati nel file system del server. Le risorse di deposito temporaneo occupate da `com.adobe.idp.Document` vengono rimossi automaticamente al momento della `com.adobe.idp.Document` smaltimento. (Vedi [Disposizione degli oggetti documento](invoking-aem-forms-using-java.md#disposing-document-objects).)

A volte è necessario conoscere il tipo di contenuto di un `com.adobe.idp.Document` prima di passare a un servizio. Ad esempio, se un’operazione richiede un tipo di contenuto specifico, ad esempio `application/pdf`, è consigliabile determinare il tipo di contenuto. (Vedi [Determinazione del tipo di contenuto di un documento](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document).)

La `com.adobe.idp.Document` tenta di determinare il tipo di contenuto utilizzando i dati forniti. Se non è possibile recuperare il tipo di contenuto dai dati forniti (ad esempio, quando i dati sono stati forniti come matrice di byte), impostare il tipo di contenuto. Per impostare il tipo di contenuto, richiama il `com.adobe.idp.Document` dell’oggetto `setContentType` metodo . (Vedi [Determinazione del tipo di contenuto di un documento](invoking-aem-forms-using-java.md#determining-the-content-type-of-a-document))

Se i file collaterali risiedono sullo stesso file system, creazione di un `com.adobe.idp.Document` l&#39;oggetto è più veloce. Se i file collaterali risiedono su file system remoti, è necessario eseguire un&#39;operazione di copia che influisce sulle prestazioni.

Un&#39;applicazione può contenere `com.adobe.idp.Document` e `org.w3c.dom.Document` tipi di dati. Tuttavia, assicurati di qualificare completamente il `org.w3c.dom.Document` tipo di dati. Per informazioni sulla conversione di un `org.w3c.dom.Document` oggetto a un `com.adobe.idp.Document` oggetto, vedere [Avvio rapido (modalità EJB): Precompilazione di Forms con layout fluidi tramite l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api).

>[!NOTE]
>
>Per evitare una perdita di memoria in WebLogic durante l’utilizzo di un `com.adobe.idp.Document` leggere le informazioni del documento in blocchi di 2048 byte o meno. Ad esempio, il codice seguente legge le informazioni del documento in blocchi di 2048 byte:

```java
        // Set up the chunk size to prevent a potential memory leak
        int buffSize = 2048;
 
        // Determine the total number of bytes to read
        int docLength = (int) inDoc.length();
        byte [] byteDoc = new byte[docLength];
 
        // Set up the reading position
        int pos = 0;
 
        // Loop through the document information, 2048 bytes at a time
        while (docLength > 0) {
      // Read the next chunk of information
            int toRead = Math.min(buffSize, docLength);
            int bytesRead = inDoc.read(pos, byteDoc, pos, toRead);
 
            // Handle the exception in case data retrieval failed
            if (bytesRead == -1) {
 
                inDoc.doneReading();
                inDoc.dispose();
                throw new RuntimeException("Data retrieval failed!");
 
            }
 
             // Update the reading position and number of bytes remaining
             pos += bytesRead;
             docLength -= bytesRead;
 
        }
 
        // The document information has been successfully read
        inDoc.doneReading();
        inDoc.dispose();
```

**Consulta anche**

[Richiamo di AEM Forms tramite l’API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Impostazione delle proprietà di connessione](invoking-aem-forms-using-java.md#setting-connection-properties)

### Creazione di documenti {#creating-documents}

Crea un `com.adobe.idp.Document` prima di richiamare un&#39;operazione di servizio che richiede un documento PDF (o altri tipi di documento) come valore di input. La `com.adobe.idp.Document` La classe fornisce costruttori che consentono di creare un documento dai seguenti tipi di contenuto:

* Matrice a byte
* Una esistente `com.adobe.idp.Document` oggetto
* A `java.io.File` oggetto
* A `java.io.InputStream` oggetto
* A `java.net.URL` oggetto

#### Creazione di un documento basato su una matrice di byte {#creating-a-document-based-on-a-byte-array}

Nell&#39;esempio di codice seguente viene creato un `com.adobe.idp.Document` oggetto basato su un array di byte.

**Creazione di un oggetto Document basato su un array di byte**

```java
 Document myPDFDocument = new Document(myByteArray);
```

#### Creazione di un documento basato su un altro documento {#creating-a-document-based-on-another-document}

Nell&#39;esempio di codice seguente viene creato un `com.adobe.idp.Document` oggetto basato su un altro `com.adobe.idp.Document` oggetto.

**Creazione di un oggetto Document basato su un altro documento**

```java
 //Create a Document object based on a byte array
 InputStream is = new FileInputStream("C:\\Map.pdf");
 int len = is.available();
 byte [] myByteArray = new byte[len];
 int i = 0;
 while (i < len) {
       i += is.read(myByteArray, i, len);
 }
 Document myPDFDocument = new Document(myByteArray);
 
 //Create another Document object
 Document anotherDocument = new Document(myPDFDocument);
```

#### Creazione di un documento basato su un file {#creating-a-document-based-on-a-file}

Nell&#39;esempio di codice seguente viene creato un `com.adobe.idp.Document` oggetto basato su un file PDF denominato *map.pdf*. Questo file si trova nella directory principale del disco rigido C. Questo costruttore tenta di impostare il tipo di contenuto MIME del `com.adobe.idp.Document` utilizzando l&#39;estensione del nome del file.

La `com.adobe.idp.Document` costruttore che accetta un `java.io.File` accetta anche un parametro booleano. Impostando questo parametro su `true`, `com.adobe.idp.Document` elimina il file. Questa azione significa che non è necessario rimuovere il file dopo averlo trasmesso al `com.adobe.idp.Document` costruttore.

Impostazione del parametro su `false` significa che mantieni la proprietà del file. Impostazione del parametro su `true` è più efficiente. Il motivo è che `com.adobe.idp.Document` è possibile spostare il file direttamente nell&#39;area gestita locale anziché copiarlo (che è più lento).

**Creazione di un oggetto Document basato su un file PDF**

```java
 //Create a Document object based on the map.pdf source file
 File mySourceMap = new File("C:\\map.pdf");
 Document myPDFDocument = new Document(mySourceMap,true);
```

#### Creazione di un documento basato su un oggetto InputStream {#creating-a-document-based-on-an-inputstream-object}

Il seguente esempio di codice Java crea un `com.adobe.idp.Document` oggetto basato su un `java.io.InputStream` oggetto.

**Creazione di un documento basato su un oggetto InputStream**

```java
 //Create a Document object based on an InputStream object
 InputStream is = new FileInputStream("C:\\Map.pdf");
 Document myPDFDocument = new Document(is);
```

#### Creazione di un documento basato sul contenuto accessibile da un URL {#creating-a-document-based-on-content-accessible-from-an-url}

Il seguente esempio di codice Java crea un `com.adobe.idp.Document` oggetto basato su un file PDF denominato *map.pdf*. Questo file si trova all&#39;interno di un&#39;applicazione Web denominata `WebApp` che è in esecuzione `localhost`. Questo costruttore tenta di impostare il `com.adobe.idp.Document` tipo di contenuto MIME dell’oggetto utilizzando il tipo di contenuto restituito con il protocollo URL.

L’URL fornito al `com.adobe.idp.Document` l&#39;oggetto viene sempre letto sul lato in cui l&#39;originale `com.adobe.idp.Document` viene creato, come illustrato in questo esempio:

```java
     Document doc = new Document(new java.net.URL("file:c:/temp/input.pdf"));
```

Il file c:/temp/input.pdf deve trovarsi sul computer client (non sul computer server). Il computer client è il punto in cui l’URL viene letto e il punto in cui viene visualizzata la `com.adobe.idp.Document` oggetto creato.

**Creazione di un documento basato sul contenuto accessibile da un URL**

```java
 //Create a Document object based on a java.net.URL object
 URL myURL = new URL("http", "localhost", 8080,"/WebApp/map.pdf");
 
 //Create another Document object
 Document myPDFDocument = new Document(myURL);
```

**Consulta anche**

[Richiamo di AEM Forms tramite l’API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Impostazione delle proprietà di connessione](invoking-aem-forms-using-java.md#setting-connection-properties)

### Gestione dei documenti restituiti {#handling-returned-documents}

Le operazioni del servizio che restituiscono un documento PDF (o altri tipi di dati come i dati XML) come valore di output restituiscono un valore `com.adobe.idp.Document` oggetto. Dopo aver ricevuto un `com.adobe.idp.Document` è possibile convertirlo nei seguenti formati:

* A `java.io.File` oggetto
* A `java.io.InputStream` oggetto
* Matrice a byte

La seguente riga di codice converte un `com.adobe.idp.Document` oggetto a un `java.io.InputStream` oggetto. Supponiamo che `myPDFDocument` rappresenta `com.adobe.idp.Document` oggetto:

```java
     java.io.InputStream resultStream = myDocument.getInputStream();
```

Allo stesso modo, puoi copiare il contenuto di un `com.adobe.idp.Document` in un file locale eseguendo le seguenti operazioni:

1. Crea un `java.io.File` oggetto.
1. Richiama il `com.adobe.idp.Document` dell’oggetto `copyToFile` e passare il `java.io.File`oggetto.

Nell&#39;esempio di codice seguente viene copiato il contenuto di un `com.adobe.idp.Document` a un file denominato *AnotherMap.pdf*.

**Copia del contenuto di un oggetto documento in un file**

```java
 File outFile = new File("C:\\AnotherMap.pdf");
 myDocument.copyToFile (outFile);
```

**Consulta anche**

[Richiamo di AEM Forms tramite l’API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Impostazione delle proprietà di connessione](invoking-aem-forms-using-java.md#setting-connection-properties)

### Determinazione del tipo di contenuto di un documento {#determining-the-content-type-of-a-document}

Determinare il tipo MIME di un `com.adobe.idp.Document` richiamando l&#39;oggetto `com.adobe.idp.Document` dell’oggetto `getContentType` metodo . Questo metodo restituisce un valore stringa che specifica il tipo di contenuto del `com.adobe.idp.Document` oggetto. La tabella seguente descrive i diversi tipi di contenuto restituiti da AEM Forms.

<table>
 <thead>
  <tr>
   <th><p>Tipo MIME</p></th>
   <th><p>Descrizione</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>application/pdf</code></p></td>
   <td><p>documento PDF</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xdp+xml</code></p></td>
   <td><p>XML Data Packaging (XDP), utilizzato per i moduli XML Forms Architecture (XFA) esportati</p></td>
  </tr>
  <tr>
   <td><p><code>text/xml</code></p></td>
   <td><p>Segnalibri, allegati o altri documenti XML</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.fdf</code></p></td>
   <td><p>Formato dati Forms (FDF), utilizzato per i moduli Acrobat esportati</p></td>
  </tr>
  <tr>
   <td><p><code>application/vnd.adobe.xfdf</code></p></td>
   <td><p>XML Forms Data Format (XFDF), utilizzato per i moduli Acrobat esportati</p></td>
  </tr>
  <tr>
   <td><p><code>application/rdf+xml</code></p></td>
   <td><p>Formato dati RTF e XML</p></td>
  </tr>
  <tr>
   <td><p><code>application/octet-stream</code></p></td>
   <td><p>Formato dati generico</p></td>
  </tr>
  <tr>
   <td><p><code>NULL</code></p></td>
   <td><p>Tipo MIME non specificato</p></td>
  </tr>
 </tbody>
</table>

Nell&#39;esempio di codice seguente viene determinato il tipo di contenuto di un `com.adobe.idp.Document` oggetto.

**Determinazione del tipo di contenuto di un oggetto Document**

```java
 //Determine the content type of the Document object
 String ct = myDocument.getContentType();
 System.out.println("The content type of the Document object is " +ct);
```

**Consulta anche**

[Richiamo di AEM Forms tramite l’API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Impostazione delle proprietà di connessione](invoking-aem-forms-using-java.md#setting-connection-properties)

### Disposizione degli oggetti documento {#disposing-document-objects}

Quando non è più necessario un `Document` Si consiglia di eliminarlo richiamandone l&#39;oggetto `dispose` metodo . Ogni `Document` l&#39;oggetto consuma un descrittore di file e fino a 75 MB di spazio RAM sulla piattaforma host dell&#39;applicazione. Se `Document` l&#39;oggetto non viene eliminato, quindi il processo di raccolta Java Garage lo dispone. Tuttavia, eliminandolo prima utilizzando il `dispose` è possibile liberare la memoria occupata dal `Document` oggetto.

**Consulta anche**

[Richiamo di AEM Forms tramite l’API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Richiamo di un servizio tramite una libreria client Java](invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)

## Richiamo di un servizio tramite una libreria client Java {#invoking-a-service-using-a-java-client-library}

Le operazioni del servizio AEM Forms possono essere richiamate utilizzando l’API fortemente tipizzata di un servizio, nota come libreria client Java. A *Libreria client Java* è un insieme di classi concrete che forniscono accesso ai servizi distribuiti nel contenitore di servizi. Creare un&#39;istanza di un oggetto Java che rappresenta il servizio da richiamare invece di creare un `InvocationRequest` mediante l’API di incitazione. L’API di vocazione viene utilizzata per richiamare i processi creati in Workbench, ad esempio quelli di lunga durata. (Vedi [Richiamo dei processi a lunga durata incentrati sull&#39;uomo](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).)

Per eseguire un&#39;operazione del servizio, richiamare un metodo che appartiene all&#39;oggetto Java. Una libreria client Java contiene metodi che in genere mappano uno a uno con le operazioni del servizio. Quando utilizzi una libreria client Java, imposta le proprietà di connessione richieste. (Vedi [Impostazione delle proprietà di connessione](invoking-aem-forms-using-java.md#setting-connection-properties).)

Dopo aver impostato le proprietà di connessione, crea un `ServiceClientFactory` oggetto utilizzato per creare un&#39;istanza di un oggetto Java che consente di richiamare un servizio. Ogni servizio con una libreria client Java ha un oggetto client corrispondente. Ad esempio, per richiamare il servizio Repository, crea un `ResourceRepositoryClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto. La `ServiceClientFactory` L&#39;oggetto è responsabile della gestione delle impostazioni di connessione necessarie per richiamare i servizi AEM Forms.

Anche se si ottiene un `ServiceClientFactory` è generalmente veloce, un certo sovraccarico è coinvolto quando la fabbrica viene utilizzata per la prima volta. Questo oggetto è ottimizzato per il riutilizzo e quindi, quando possibile, utilizza lo stesso `ServiceClientFactory` quando si creano più oggetti client Java. Cioè, non creare un separato `ServiceClientFactory` oggetto per ogni oggetto libreria client creato.

È presente un&#39;impostazione User Manager che controlla la durata dell&#39;asserzione SAML che si trova all&#39;interno della `com.adobe.idp.Context` oggetto che influisce sul `ServiceClientFactory` oggetto. Questa impostazione controlla tutti i tempi di vita del contesto di autenticazione in AEM Forms, comprese tutte le chiamate eseguite utilizzando l&#39;API Java. Per impostazione predefinita, il periodo di tempo in cui un `ServiceCleintFactory` L&#39;oggetto può essere utilizzato per due ore.

>[!NOTE]
>
>Per spiegare come richiamare un servizio utilizzando l’API Java, il servizio Repository `writeResource` si richiama . Questa operazione inserisce una nuova risorsa nell’archivio.

Puoi richiamare il servizio Repository utilizzando una libreria client Java ed eseguendo i seguenti passaggi:

1. Includi file JAR client, come adobe-repository-client.jar, nel percorso di classe del progetto Java. Per informazioni sulla posizione di questi file, vedi [Inclusione dei file libreria Java di AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).
1. Imposta le proprietà di connessione necessarie per richiamare un servizio.
1. Crea un `ServiceClientFactory` richiamando l&#39;oggetto `ServiceClientFactory` statico dell’oggetto `createInstance` e passare `java.util.Properties` oggetto contenente le proprietà di connessione.
1. Crea un `ResourceRepositoryClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto. Utilizza la `ResourceRepositoryClient` oggetto per richiamare le operazioni del servizio Repository.
1. Crea un `RepositoryInfomodelFactoryBean` utilizzando il relativo costruttore e passando `null`. Questo oggetto consente di creare un `Resource` che rappresenta il contenuto aggiunto all&#39;archivio.
1. Crea un `Resource` richiamando l&#39;oggetto `RepositoryInfomodelFactoryBean` dell’oggetto `newImage` e passando i seguenti valori:

   * Un valore ID univoco specificando `new Id()`.
   * Un valore UUID univoco specificando `new Lid()`.
   * Nome della risorsa. È possibile specificare il nome del file XDP.

   Imposta il valore restituito su `Resource`.

1. Crea un `ResourceContent` richiamando l&#39;oggetto `RepositoryInfomodelFactoryBean` dell’oggetto `newImage` e il cast del valore restituito su `ResourceContent`. Questo oggetto rappresenta il contenuto aggiunto alla directory archivio.
1. Crea un `com.adobe.idp.Document` passare un oggetto `java.io.FileInputStream` oggetto che memorizza il file XDP da aggiungere all&#39;archivio. (Vedi [Creazione di un documento basato su un oggetto InputStream](invoking-aem-forms-using-java.md#creating-a-document-based-on-an-inputstream-object).)
1. Aggiungi il contenuto del `com.adobe.idp.Document` dell&#39;oggetto `ResourceContent` richiamando l&#39;oggetto `ResourceContent` dell’oggetto `setDataDocument` metodo . Passa la `com.adobe.idp.Document` oggetto.
1. Imposta il tipo MIME del file XDP da aggiungere all&#39;archivio richiamando il `ResourceContent` dell’oggetto `setMimeType` metodo e passaggio `application/vnd.adobe.xdp+xml`.
1. Aggiungi il contenuto del `ResourceContent` dell&#39;oggetto `Resource` richiamando l&#39;oggetto `Resource` oggetto ‘s `setContent` e passare `ResourceContent` oggetto.
1. Aggiungi una descrizione della risorsa richiamando il `Resource` oggetto ‘s `setDescription` e passare un valore stringa che rappresenta una descrizione della risorsa.
1. Aggiungere la struttura del modulo all’archivio richiamando il `ResourceRepositoryClient` dell’oggetto `writeResource` e passando i seguenti valori:

   * Valore stringa che specifica il percorso della raccolta di risorse contenente la nuova risorsa
   * La `Resource` oggetto creato

**Consulta anche**

[Avvio rapido (modalità EJB): Scrittura di una risorsa tramite l’API Java](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[Richiamo di AEM Forms tramite l’API Java](invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)

[Inclusione dei file libreria Java di AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

## Richiamare un processo di breve durata utilizzando l’API di richiamo {#invoking-a-short-lived-process-using-the-invocation-api}

Puoi richiamare un processo di breve durata utilizzando l’API Java Invocation. Quando invochi un processo di breve durata utilizzando l’API di richiamo, trasmetti i valori dei parametri richiesti utilizzando un `java.util.HashMap` oggetto. Per ogni parametro da passare a un servizio, richiama il `java.util.HashMap` dell’oggetto `put` e specifica la coppia nome-valore richiesta dal servizio per eseguire l&#39;operazione specificata. Specifica il nome esatto dei parametri che appartengono al processo di breve durata.

>[!NOTE]
>
>Per informazioni sull&#39;avvio di un processo di lunga durata, vedi [Richiamo dei processi a lunga durata incentrati sull&#39;uomo](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes).

La discussione qui riguarda l&#39;utilizzo dell&#39;API di vocazione per invocare il seguente processo AEM Forms di breve durata denominato `MyApplication/EncryptDocument`.

>[!NOTE]
>
>Questo processo non è basato su un processo AEM Forms esistente. Per seguire l&#39;esempio di codice, crea un processo denominato `MyApplication/EncryptDocument` utilizzo di Workbench. (Vedi [Utilizzo di Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63).)

Quando si richiama questo processo, vengono eseguite le azioni seguenti:

1. Ottiene il documento PDF non protetto passato al processo. Questa azione si basa sul `SetValue` funzionamento. Il parametro di input per questo processo è un `document` variabile di processo denominata `inDoc`.
1. Cifra il documento PDF con una password. Questa azione si basa sul `PasswordEncryptPDF` funzionamento. Il documento PDF crittografato con password viene restituito in una variabile di processo denominata `outDoc`.

### Richiamare il processo di breve durata MyApplication/EncryptDocument utilizzando l&#39;API di chiamata Java {#invoke-the-myapplication-encryptdocument-short-lived-process-using-the-java-invocation-api}

Richiama il `MyApplication/EncryptDocument` processo di breve durata tramite l’API di chiamata Java:

1. Includi file JAR client, come adobe-livecycle-client.jar, nel percorso di classe del progetto Java. (Vedi [Inclusione dei file libreria Java di AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).)
1. Crea un `ServiceClientFactory` oggetto contenente le proprietà di connessione. (Vedi [Impostazione delle proprietà di connessione](invoking-aem-forms-using-java.md#setting-connection-properties).)
1. Crea un `ServiceClient` utilizzando il relativo costruttore e passando `ServiceClientFactory` oggetto. A `ServiceClient` consente di richiamare un&#39;operazione del servizio. Gestisce attività quali l&#39;individuazione, l&#39;invio e l&#39;indirizzamento delle richieste di chiamata.
1. Crea un `java.util.HashMap` utilizzando il relativo costruttore.
1. Richiama il `java.util.HashMap` dell’oggetto `put` metodo per ogni parametro di input da passare al processo longevo. Perché `MyApplication/EncryptDocument` il processo di breve durata richiede un parametro di input di tipo `Document`, è sufficiente richiamare `put` , come illustrato nell&#39;esempio seguente.

   ```java
    //Create a Map object to store the parameter value for inDoc
    Map params = new HashMap();
    InputStream inFile = new FileInputStream("C:\\Adobe\Loan.pdf");
    Document inDoc = new Document(inFile);
    params.put("inDoc", inDoc);
   ```

1. Crea un `InvocationRequest` richiamando l&#39;oggetto `ServiceClientFactory` dell’oggetto `createInvocationRequest` e passando i seguenti valori:

   * Valore stringa che specifica il nome del processo a lunga durata da richiamare. Per richiamare `MyApplication/EncryptDocument` processo, specificare `MyApplication/EncryptDocument`.
   * Valore stringa che rappresenta il nome dell&#39;operazione di processo. In genere, il nome di un&#39;operazione di processo di breve durata è `invoke`.
   * La `java.util.HashMap` oggetto contenente i valori dei parametri richiesti dall&#39;operazione del servizio.
   * Un valore booleano che specifica `true`, che crea una richiesta sincrona (questo valore è applicabile per richiamare un processo di breve durata).

1. Invia la richiesta di chiamata al servizio richiamando il `ServiceClient` dell’oggetto `invoke` e passare `InvocationRequest` oggetto. La `invoke` restituisce un `InvocationReponse` oggetto.

   >[!NOTE]
   >
   >Un processo a lungo termine può essere invocato passando il valore `false`come quarto parametro del `createInvocationRequest` metodo . Passaggio del valore `false`*crea una richiesta asincrona.*

1. Recupera il valore restituito del processo richiamando il `InvocationReponse` dell’oggetto `getOutputParameter` e passare un valore stringa che specifica il nome del parametro di output. In questa situazione, specificare `outDoc` ( `outDoc` è il nome del parametro di output per il `MyApplication/EncryptDocument` processo). Imposta il valore restituito su `Document`, come illustrato nell’esempio seguente.

   ```java
    InvocationResponse response = myServiceClient.invoke(request);
    Document encryptDoc = (Document) response.getOutputParameter("outDoc");
   ```

1. Crea un `java.io.File` e assicurati che l&#39;estensione del file sia .pdf.
1. Richiama il `com.adobe.idp.Document` dell’oggetto `copyToFile` per copiare il contenuto del `com.adobe.idp.Document` al file. Assicurati di utilizzare `com.adobe.idp.Document` oggetto restituito da `getOutputParameter` metodo .

**Consulta anche**

[Avvio rapido: Richiamare un processo di breve durata utilizzando l’API di richiamo](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-using-the-invocation-api)

[Richiamo dei processi a lunga durata incentrati sull&#39;uomo](/help/forms/developing/invoking-human-centric-long-lived.md#invoking-human-centric-long-lived-processes)

[Inclusione dei file libreria Java di AEM Forms](invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
